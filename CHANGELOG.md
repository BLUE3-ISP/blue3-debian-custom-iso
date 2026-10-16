# Changelog

## 0.1.13 - Corrige no README o papel do grub.cfg, quem copia os .conf do SSH e o caminho fixo do build

O README dizia que o build "não copia" o `grub.cfg`: ele entra na ISO com o resto de `blue3/`, só não é instalado como menu de boot (a variável `GRUB_SRC` não é usada). Dizia também que o build copia os `.conf` do SSH por glob; quem copia é o late_command do preseed. O caminho absoluto de `BASE_DIR` deixa de ser repetido no texto e passa a apontar para `script-iso.sh:19`. A conferência de sintaxe usa `break` em vez de `exit`, que fechava o terminal ao colar o trecho. Correção documental sem bump, conforme version.md.

## 0.1.13 - Corrige a conferência de sintaxe dos dois scripts

O `bash -n script-iso.sh blue3/blue3_script.sh` só conferia o primeiro arquivo (o segundo era lido como argumento do script). Troca por um laço que confere os dois. Correção documental sem bump, conforme version.md.

## 0.1.13 - Revisa o contrato da ISO e do provisionamento pós-instalação

Documenta entradas, layout suportado, build, preseed, rede/IPAM e primeiro boot. Corrige caminhos e payloads documentados e registra lacunas operacionais sem alterar scripts ou configurações. Versão mantida pela exceção documental local.

O histórico anterior permanece em `version.md` e no Git.
