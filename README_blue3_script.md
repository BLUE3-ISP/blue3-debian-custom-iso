# Provisionamento pós-instalação

Fonte: [blue3/blue3_script.sh](blue3/blue3_script.sh), revisão de 15/10/2026.
O builder da ISO, o preseed e este script têm contratos separados; o README
principal descreve a montagem/instalação. Este guia não certifica um boot real.

## Entradas e fluxo

O script exige `/root/.env` e o carrega com `source`/export. Ele precisa conter a
URL base da API PHPIPAM e a credencial usadas nas chamadas do script. O
[template](blue3/.env.example) descreve essas chaves; não publique seus valores.
O preseed atual tenta produzir `/root/.env` a partir de `blue3/env`, ausente no
clone. Decidir transporte/injeção de segredo antes de distribuir uma imagem;
a cópia genérica do builder não inclui dotfiles.

1. Lista interfaces com nome iniciado em `en` ou `eth` e solicita um índice.
2. Sobrescreve `/etc/network/interfaces` com uma rede bootstrap fixa no código;
   troca resolv.conf e testa alcance do DNS de bootstrap.
3. Instala curl, jq, ipcalc, vlan e Git se algum não estiver instalado.
4. Solicita hostname e domínio (default `b3.local`) e consulta o hostname no IPAM.
5. Usa o primeiro endereço retornado, consulta subnet/máscara/gateway e pergunta
   se deve configurar VLAN quando há vlanId.
6. Atualiza hostname, `/etc/hosts`, DNS e rede estática; marca resolv.conf imutável
   e reinicia a interface. A disponibilidade do gateway é testada por ping.
7. Clona ou atualiza `/root/Linux-Start` do GitHub e executa `start.sh` quando existe.
   Esse código externo não é pinado nem faz parte deste repositório.

Não há contrato de flags, modo não interativo, seleção automática segura de interface,
rollback de rede ou criação de cadastro no IPAM. Reexecutar pode repetir alterações.
O arquivo log é `/var/log/blue3-install.log`; não anexe conteúdo sensível sem revisão.

## Operação e evidências necessárias

A unit [service.one_shot](blue3/service.one_shot) chama o script como oneshot,
mas não declara terminal interativo nem um marcador persistente de “já concluído”.
`RemainAfterExit=true` não torna o serviço uma única execução para sempre: se
habilitado, pode ser iniciado de novo num boot seguinte.

Antes de homologar, demonstrar com conta/VM de teste: payload correto, ambiente
privado protegido, entrada interativa ou mecanismo alternativo aprovado, interface
válida, respostas IPAM completas, VLAN e rota/DNS finais, SSH preservado e retorno
após novo boot. Conservar console e recuperação de rede fora do acesso SSH.

A revisão não consultou o IPAM, clonou Linux-Start, executou primeiro boot ou
alterou rede. Os problemas de origem estão no [relatório](docs/REVISAO-20261015.md).
