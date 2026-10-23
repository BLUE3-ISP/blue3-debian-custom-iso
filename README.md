# Blue3 Debian Custom ISO

Material para remasterizar uma ISO Debian com preseed e arquivos de configuração
Blue3. A arquitetura tem três etapas independentes: geração da imagem,
instalação automatizada no disco e provisionamento do sistema instalado via PHPIPAM.
Revisão de fonte em 15/10/2026, base `f1c0ae7` (`0.1.13`).

## Componentes e estado real

| Componente | Responsabilidade |
|---|---|
| [script-iso.sh](script-iso.sh) | Extrai ISO, copia payload, modifica initrds/menus, recria md5sum e gera imagem híbrida |
| [blue3/preseed.cfg](blue3/preseed.cfg) | Locale, rede do instalador, contas, particionamento, pacotes e late_command |
| [blue3/blue3_script.sh](blue3/blue3_script.sh) | Rede bootstrap, interface/hostname interativos, consulta PHPIPAM, VLAN opcional e rede definitiva |
| [blue3/service.one_shot](blue3/service.one_shot) | Unit oneshot que tenta executar o provisionamento no boot |
| `blue3/ssh/`, `bashrc`, MOTD e banners | Payload de personalização do sistema |
| `blue3/grub.cfg`, `blue3.png` | Entram na ISO junto com o resto de `blue3/` (`cp -a`), mas o build não instala esse `grub.cfg` como menu de boot: a variável `GRUB_SRC` é definida e não é usada; o build altera os menus extraídos da ISO base |

O clone tem um template `.env.example`, mas o preseed exige um arquivo chamado
**`/cdrom/blue3/env`** que não é versionado. Também referencia `sources.list`
ausente. Uma imagem construída não comprova que o late_command e o primeiro boot
funcionam. Veja os [bloqueios e decisões](docs/REVISAO-20261015.md) antes de selecionar
esta base para uma instalação.

## Ambiente de build

O script é voltado a Linux, Bash e ferramentas GNU. Usa xorriso, cpio, gzip/zcat,
md5sum, find/xargs/sed e sudo; os componentes BIOS/UEFI esperados precisam existir
na ISO base. O código usa `install.amd`, ISOLINUX e `boot/grub/efi.img`: não promete
compatibilidade com qualquer netinst, DVD, arquitetura ou formato de initrd.

O diretório **`BASE_DIR` é fixo no código** (`script-iso.sh:19`, um caminho absoluto de
quem montou o build). Executar de outra pasta não o muda; em outra máquina, edite essa
linha antes de rodar. Nesse diretório o script espera `debian.iso` e a pasta `blue3/`. `BUILD_USER` e `BUILD_GROUP`
podem vir do ambiente; controlam o dono dos arquivos, não a raiz do build.

A execução operacional é `sudo bash script-iso.sh` no host preparado. Antes dela,
o operador precisa revisar caminhos, permissões, insumos e credenciais. Ela apaga
`isofiles/` e a saída de mesmo dia, altera uma área temporária fixa e gera
`blue3-debian-YYYYMMDD.iso`, acrescentando logs a `custom.log`. Não há dry-run,
lock, checksum externo do insumo ou aceitação automática em VM. Esta revisão não
gerou uma ISO, usou sudo ou instalou um sistema.

## Instalação automatizada

O preseed configura pt_BR/teclado US, nome/domínio iniciais, rede do instalador
desabilitada e `apt-setup/use_mirror=false`. Portanto não basta escolher uma ISO
mínima e presumir que todos os pacotes extras estarão disponíveis offline.
A configuração de mirror existe, mas não demonstra que será usado nessa etapa.

**O alvo de particionamento é `/dev/sda`, com confirmação automática.** O layout
propõe GPT/EFI, `/boot` ext4, swap LVM, raiz XFS e volumes Btrfs em `/var`,
`/var/log` e `/tmp`. Não inicialize essa instalação num disco com dados a preservar.
Antes da implantação, a receita precisa ser validada no modo de firmware e na mídia
escolhidos. Os valores de conta/SSH embarcados também precisam de revisão específica;
nenhuma credencial real é reproduzida nesta documentação.

O late_command copia payload para `/target`: script/env, banners, rede, resolv.conf,
SSH e bashrc; ajusta permissões e tenta habilitar SSH e o serviço de primeiro boot.
O nome do fragmento versionado é `ssh/ipath.conf` (não `ipauth.conf`). Quem copia os
`.conf` por glob (`cp -a /cdrom/blue3/ssh/*.conf`, com `|| true`) é o late_command do
preseed durante a instalação, não o `script-iso.sh`. Falhas toleradas nessa etapa não
são validação.

## Primeiro boot, operação e recuperação

Consulte o [guia do provisionamento](README_blue3_script.md) para interface,
PHPIPAM, hostname, VLAN, rede e Linux-Start. Esse script é interativo, embora a unit
não configure stdin/TTY. Não há evidência nesta revisão de que esse contrato funcione
sem operador. A máquina pode trocar de IP e interromper o acesso remoto.

Preserve uma VM/disco descartável para homologação e uma cópia recuperável das
configurações do sistema antes de provisionar. O builder não implementa rollback do
disco instalado. Registre separadamente build da ISO, boot BIOS/UEFI, conclusão do
installer, aplicação de payload e aceitação do primeiro boot.

Os tempos anotados na documentação anterior (VM 8 vCPU/8 GiB/SSD 60 GB: 3min33s
em Hyper-V/Windows Server 2022 e 3min10s em Proxmox 9.1) são relatos históricos,
sem repetição ou homologação de desempenho nesta revisão.

## Verificação e contribuição

```bash
for script in script-iso.sh blue3/blue3_script.sh; do
  bash -n "$script" || break
done
```

Esse comando confere sintaxe shell (o `break` interrompe no primeiro erro sem fechar o
terminal, o que um `exit` faria); não executa build, preseed, rede ou systemd.
O workflow versionado é de release, sem teste de instalação. Os insumos e a imagem
final precisam de identificação/checksum e prova no alvo em um trabalho separado.
[AGENTS.md](AGENTS.md) governs contributions, written in English (US) from 0.1.14 on;
[version.md](version.md) exempts documentation fixes from a bump.
O histórico útil foi preservado sem tratar intenções antigas como comportamento confirmado.
