# Changelog

## 0.1.14 - the repository is written in English (US) from this version on, following its new owner on GitHub

On 23/10/2026 the repository moved from `BLUE3-ISP` to `samirhvbr`. The
language rule of [repodocs](https://github.com/samirhvbr/repodocs) is decided by
the owner on GitHub, and the Portuguese set is `BLUE3-ISP/*`,
`samirhvbr/blue3-intranet` and `samirhvbr/blue3-ai-login` — this repository is
no longer in it. Samir confirmed that reading the same day: it becomes English
(US). The local `origin` now points at `samirhvbr/blue3-debian-custom-iso`.

The previous commit swapped the marked blocks. This one fixes the text outside
the markers that still prescribed Portuguese:

- `CLAUDE.md` and `AGENTS.md` — the commit line of the preamble, and a new
  `Language` section at the top that records the switch, the date and the
  decision (the twins stay identical below the H1);
- `version.md` §2 — the commit format and its rules;
- `README.md` — the contribution sentence, which also stops saying contributions
  go through a pull request: the commit rule in `AGENTS.md` commits and pushes
  each delivery and asks for no PR.

`blue3/preseed.cfg` is not touched.

Nothing else is translated. The Portuguese commit messages already in `git log`
and the Portuguese documents already in the tree stay as they are until they are
next touched; the edit then comes out in English.

## 0.1.14 - the echo blocks switch to English (US), following the owner on GitHub

The marked rules in `CLAUDE.md` and `AGENTS.md` are rewritten from the single
source at [samirhvbr/repodocs](https://github.com/samirhvbr/repodocs), and this
time the variant changes: the repository carried the Portuguese blocks, and
`origin` now names `samirhvbr/blue3-debian-custom-iso`, which is outside the Portuguese set
(`BLUE3-ISP/*`, `samirhvbr/blue3-intranet`, `samirhvbr/blue3-ai-login`). The
language of a repository follows its owner on GitHub, so every block that has a
Portuguese variant arrives in English (US).

Only the blocks change in this commit. Text written outside the markers is the
repository's own, and history is not rewritten: Portuguese messages and
documents already there stay as they are until they are next touched.

## 0.1.13 - Corrige no README o papel do grub.cfg, quem copia os .conf do SSH e o caminho fixo do build

O README dizia que o build "não copia" o `grub.cfg`: ele entra na ISO com o resto de `blue3/`, só não é instalado como menu de boot (a variável `GRUB_SRC` não é usada). Dizia também que o build copia os `.conf` do SSH por glob; quem copia é o late_command do preseed. O caminho absoluto de `BASE_DIR` deixa de ser repetido no texto e passa a apontar para `script-iso.sh:19`. A conferência de sintaxe usa `break` em vez de `exit`, que fechava o terminal ao colar o trecho. Correção documental sem bump, conforme version.md.

## 0.1.13 - Corrige a conferência de sintaxe dos dois scripts

O `bash -n script-iso.sh blue3/blue3_script.sh` só conferia o primeiro arquivo (o segundo era lido como argumento do script). Troca por um laço que confere os dois. Correção documental sem bump, conforme version.md.

## 0.1.13 - Revisa o contrato da ISO e do provisionamento pós-instalação

Documenta entradas, layout suportado, build, preseed, rede/IPAM e primeiro boot. Corrige caminhos e payloads documentados e registra lacunas operacionais sem alterar scripts ou configurações. Versão mantida pela exceção documental local.

O histórico anterior permanece em `version.md` e no Git.
