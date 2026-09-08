# blue3-debian-custom-iso — Instructions for Claude Code

<!--
  The content below the H1 is duplicated between CLAUDE.md (read by Claude Code)
  and AGENTS.md (read by other tooling, agents.md standard) — keep the two
  byte-identical below the H1. If you edit one, edit the other.
-->

> This repository follows the samirhvbr/Blue3 documentation and versioning
> standard. The norm lives once, at
> **[samirhvbr/repodocs](https://github.com/samirhvbr/repodocs)** — read it
> there; do not copy it here.
>
> Commits: `X.Y.Z - description in English (US)`, with the version coming from
> `version.md` and bumped in the same commit. Conventional Commits prefixes
> (`feat:`, `fix:`, `chore:`) and vague messages are forbidden.

---

<!-- COMMIT-RULE:repodocs -->

## Commits — you commit, and nothing is delivered until you have

> Marked echo. The single source is **[samirhvbr/repodocs](https://github.com/samirhvbr/repodocs/blob/master/docs/versioning.md#who-commits-and-when)**
> — change it there, not here. This block is regenerated.

**Committing is your job.** Not "leave the tree ready and something downstream
packages it" — you run `git commit`, and `git push`, as the last step of the work
you were asked to do. The COMMITTER skill that used to commit on an agent's
behalf is `enabled: false` in every repository of this fleet since 03/09/2026;
what is left of it is a kill-switch, not a scheduler. **If you do not commit,
nobody does.**

**Do not report a task as finished before the commit exists.** "Done",
"delivered", "concluded" mean the work is in `git log` — never that it is sitting
uncommitted where only this session can see it. The commit is the last step *of
the task*, not a follow-up for someone else. If you are about to write
"finished", commit first, then write it.

**Push is part of the delivery, and a refused push is the one place a human enters.**
Commit *and* push, every delivery — a clean push needs nobody's permission and is never
held back for review. When the push is **refused** (conflict, non-fast-forward, protected
branch), stop there and say so: never force, never rewrite history to get past it, never
invent a merge resolution you have not verified. The gate is the refused push, not the
commit.

**Every commit obeys the versioning rules**, with no exception:

- Subject `X.Y.Z - short description in English (US)`, the version taken from
  `version.md` and **bumped in the same commit**.
- The `CHANGELOG.md` entry is written first — its `## X.Y.Z - description`
  heading *is* the subject.
- No Conventional Commits prefix (`feat:`, `fix:`, `chore:`) and no vague
  subject ("update", "ajuste", "wip", "changes", "several improvements").

**The bump is the one clause a repository may override — in writing.** If this
repository's own documentation says the version is stamped some other way, and says
why, follow that. Otherwise the line above applies to you. An override nobody wrote
down is not an exception. Nothing else in this block bends: the changelog entry, the
subject, the language, one subject per commit, and committing before you report done
all hold regardless.

**All of this governs the repositories we own.** In a repository that is not
ours, the host's commit convention governs instead — their subject line, in
their language. `X.Y.Z` is meaningless where there is no `version.md` of ours,
and there is no version there for us to bump. Our versioning rules govern our
remotes, not every remote we can push to.

**One subject per commit.** The subject has to describe the whole commit
honestly. The moment your description needs an "and" to be true, it is two
commits.

**Split a large delivery into blocks.** A complex task is committed as a series
of commits grouped by subject, each small enough to be described in one line and
read on its own. They may share a version — bump `version.md` in the first and
repeat the number in the rest; two commits carrying one version is expected, not
a mistake. **Splitting is the default** for anything non-trivial, because the
history is the documentation of *how* the work was done, and one commit touching
six unrelated subjects documents none of them.

**The standard you are keeping:** someone reading `git log` alone — a year from
now, without the conversation that produced the work — can say what happened,
when, why, and at which version. If your commit would fail that test, it is too
big or its subject is too vague, and both are fixed the same way.

<!-- /COMMIT-RULE -->

---

<!-- LANGUAGE-RULE:repodocs -->

## Idioma — este repositório é escrito em português

> Eco marcado. A fonte única é **[samirhvbr/repodocs](https://github.com/samirhvbr/repodocs/blob/master/docs/conventions.md#the-blue3-internal-repositories-are-written-in-portuguese)**
> — mude lá, não aqui. Este bloco é regenerado.

**Tudo que vive neste repositório, ou na interface do GitHub em volta dele, é
escrito em português**: documentos, **mensagens de commit**, títulos e corpos de
pull request, issues, comentários de código, entradas de changelog, notas de
release.

Este é um dos dois repositórios-exceção da regra de inglês da frota, e a
fronteira é o **dono no GitHub**: `BLUE3-ISP/*`, `samirhvbr/blue3-intranet` e
`samirhvbr/blue3-ai-login`. O motivo é o leitor: ninguém de fora da empresa abre
estes repositórios, e boa parte do que se escreve neles é raciocínio operacional
— um incidente, uma fila, um runbook — onde a precisão da frase é o valor.
Traduzir custa mais do que rende.

**Só o idioma muda.** Formato do commit: `X.Y.Z - descrição curta em português`.
A versão vem do `version.md` e é bumpada no mesmo commit. Prefixos de
Conventional Commits (`feat:`, `fix:`, `chore:`) e mensagens vagas de uma
palavra continuam proibidos, um assunto por commit continua valendo, e a entrada
do `CHANGELOG.md` continua sendo escrita antes — o cabeçalho dela **é** o
subject.

**Identificadores de código são em inglês**, aqui como em qualquer repositório
da frota.

O histórico não se reescreve: mensagem em inglês que já está no log fica como
está.

**A `.continue/` é fila, não registro.** Um documento só sai dela quando a coisa
que ele descreve **existe** — tamanho, idioma e desalinho não são condição de
saída. *Produzir* um item da fila é fazer a coisa existir, não editar, traduzir
ou promover o documento; apagá-lo é o último passo do commit que carrega o
trabalho. **Nunca esvazie essa pasta como arrumação.**

**Num repositório que não é nosso, a convenção do upstream vence** — o idioma e
o formato do commit. Abrir um pull request ou uma issue num repositório de
terceiro faz de nós convidados, e convidado escreve na língua da casa. Nosso
`X.Y.Z - descrição` não significa nada lá: eles não têm um `version.md` nosso, e
não há versão nossa para bumpar. Quando não der para saber, escreva **inglês
(US)** — é a regra da casa da frota.

<!-- /LANGUAGE-RULE -->

<!-- QUEUE-RULE:repodocs -->

## A fila esvazia por produção, e por mais nada

> Eco marcado. A fonte única é **[samirhvbr/repodocs](https://github.com/samirhvbr/repodocs/blob/master/docs/conventions.md#1-continue-is-the-queue--docs-is-what-has-been-produced)**
> — mude lá, não aqui. Este bloco é regenerado.

**A `.continue/` guarda trabalho que ainda não existe.** Um documento só sai dela
quando — e **somente quando** — a coisa que ele descreve **existe**. Tamanho não
é condição de saída. Idade, idioma, desalinho, fim de sessão e agente que teria
escrito diferente também não.

> `tela.md` diz *"uma tela preta com uma bola amarela no meio"*. Ele sai da fila
> quando existir uma tela preta com uma bola amarela. Até lá ele fica, do
> tamanho que for, na forma em que estiver — porque até lá ele é o único lugar
> onde essa tela existe.

**"Produzir" um item da fila é fazer a coisa existir.** Não é editar o
documento, não é traduzir, não é promover para `docs/`. O documento é a
especificação; a entrega é a coisa. Apagar o documento é o **último passo do
commit que carrega o trabalho** — nunca um passo sozinho.

**Nunca esvazie essa pasta como arrumação.** Um item apagado sem o trabalho
feito destrói o único artefato que um projeto tem antes de ter código — e o que
costuma ficar no lugar é pior que a perda: uma página em `docs/` descrevendo uma
tela que ninguém construiu, indistinguível de uma que descreve algo que existe.
Se um plano precisa aparecer em `docs/` antes de ser construído, ele é
`PROPOSED`, nunca `ACTIVE`.

**A regra da meia página é sobre registro que foi parar na fila**, e sobre nada
mais. Ela não tem opinião sobre o tamanho de uma especificação de coisa não
feita: um brief de 1.300 linhas sobre algo que não existe está no único lugar
onde pode estar. Item longo é projeto com muita coisa por construir.

<!-- /QUEUE-RULE -->

<!-- RELEASES-RULE:repodocs -->

## Releases — the `version.md` on GitHub is what the Releases show

> Marked echo. The single source is **[samirhvbr/repodocs](https://github.com/samirhvbr/repodocs/blob/master/docs/versioning.md)**
> — change it there, not here. This block is regenerated.

**The `version.md` of the default branch, on GitHub, is what the GitHub Releases
must show.** The local checkout does not enter the calculation: it can be behind,
ahead or mid-work, and none of that is published — GitHub cannot tag a commit it
does not have.

**The bump and the Release are one act.** A commit that bumps `version.md` is not
finished until that version has a tag, a published Release, and the **`Latest`
badge on it** — the same push, not "later". A badge sitting on an older release
tells whoever looks that the project is at a version it is not.

- `.github/workflows/release.yml` does it on any push that touches `version.md`.
- `./tools/release.sh` does it by hand. It is **idempotent and self-healing**:
  it publishes whatever is missing and moves a drifted badge back. Running it is
  always safe, so it is both the check and the fix.

A PR publishes nothing while it is a PR. The moment it merges, the push moves
`version.md` on the default branch and the Release becomes that version.

Tag and Release title are the **bare version — no `v` prefix**.

<!-- /RELEASES-RULE -->
