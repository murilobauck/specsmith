# Specsmith

> 🇺🇸 [English version](./README.md)

**Um kit de desenvolvimento spec-driven para o [Claude Code](https://code.claude.com).**

Ferramentas de IA pra código dão resultados inconsistentes quando você as conduz
de forma ad hoc. O Specsmith empacota um método que funciona na prática:
interrogar o pedido até ele ficar inequívoco, escrever um `spec.md`, depois
`plan.md`, depois `tasks.md`, e então executar com higiene de git disciplinada.
Ele vem como um plugin instalável do Claude Code — duas skills mais um scaffold
`specs/` que amarra tudo.

## Para quem é

Devs já confortáveis com o Claude Code que querem um caminho comprovado de um
pedido vago até código entregue e revisado, sem perder o rigor no caminho.

## O método

```
spec.md (aprovado)  →  plan.md (aprovado, declara a branch)  →  tasks.md  →
kickoff (branch)  →  código (1 commit por task)  →  close (testes/CI → push → PR draft, pausa)
```

Nunca pule direto pra implementação. Cada etapa só avança quando a anterior está
aprovada. Quando estão, o agente coda de forma **autônoma** — aplicando **KISS,
YAGNI, DRY e SoC** ao código que escreve e refatorando qualquer violação antes de
cada commit, sem parar pra perguntar.

## O que vem na caixa

| Skill | O que faz |
|---|---|
| `prompt-grill` | Interroga um pedido vago uma pergunta por vez até poder ser escrito como uma spec assertiva, e então gera `specs/<feature>/spec.md`. |
| `dev-lifecycle` | A fonte única da mecânica git: branch a partir de `develop`, Conventional Commits, um commit por task, gates verdes, e um PR que pausa pra sua aprovação. Também carrega os princípios de código (KISS, YAGNI, DRY, SoC) que o agente auto-aplica ao escrever cada task. |
| `specsmith-init` | Copia o scaffold `specs/` (README + templates validados de spec, plan e tasks) pro seu projeto, pra que o fluxo spec-driven tenha uma casa local. Opcional — a `prompt-grill` funciona sem ele. |

## Instalação

**Outras IDEs** (Antigravity, Cursor, Vscode, etc.) — veja abaixo ↓

**Claude Code** — via marketplace de plugins:

```text
/plugin marketplace add murilobauck/specsmith
/plugin install specsmith@specsmith
```

Depois de instalar, as skills ficam disponíveis globalmente em qualquer
projeto — sem passo de cópia ou geração por projeto. Para também criar o
scaffold `specs/` no projeto, rode `/specsmith-init`.

### Instalando em IDEs

Cole o prompt abaixo no seu agente. Ele vai buscar as duas skills no GitHub,
gravá-las em `.specsmith/` no seu projeto e criar o scaffold `specs/` —
sem passos manuais.

```text
Instale o Specsmith neste projeto seguindo estes passos:

1. Busque https://raw.githubusercontent.com/murilobauck/specsmith/main/skills/dev-lifecycle/SKILL.md
   e grave o conteúdo em .specsmith/dev-lifecycle.md na raiz do projeto atual.

2. Busque https://raw.githubusercontent.com/murilobauck/specsmith/main/skills/prompt-grill/SKILL.md
   e grave o conteúdo em .specsmith/prompt-grill.md na raiz do projeto atual.

3. Busque https://raw.githubusercontent.com/murilobauck/specsmith/main/specs/README.md
   e grave em specs/README.md (pule se o arquivo já existir).

4. Busque https://raw.githubusercontent.com/murilobauck/specsmith/main/specs/_template/spec.md
   e grave em specs/_template/spec.md (pule se já existir).

5. Busque https://raw.githubusercontent.com/murilobauck/specsmith/main/specs/_template/plan.md
   e grave em specs/_template/plan.md (pule se já existir).

6. Busque https://raw.githubusercontent.com/murilobauck/specsmith/main/specs/_template/tasks.md
   e grave em specs/_template/tasks.md (pule se já existir).

Após concluir todos os passos, leia .specsmith/prompt-grill.md e .specsmith/dev-lifecycle.md
para estar pronto para usá-los. Confirme quais arquivos foram criados.
```

## Começando

1. (Opcional, mas recomendado) Rode `/specsmith-init` pra criar o scaffold `specs/` (Claude Code apenas).
2. Rode o `prompt-grill` (ou só diga "me entrevista sobre X"). Ele conduz a
   entrevista e escreve `specs/<feature>/spec.md`.
3. Com a spec aprovada, escreva `plan.md` (copie de `specs/_template/plan.md`).
4. Com o plano aprovado, quebre em `tasks.md` (copie de
   `specs/_template/tasks.md`).
5. Implemente task por task. O `dev-lifecycle` cuida da branch, dos commits e do PR.

## Sobre o fluxo de git

O `dev-lifecycle` vem como um fluxo de referência opinativo (branches baseadas em
`develop`, Conventional Commits, PR pausado pra aprovação). Times que usam um
modelo de git diferente devem adaptar as fases de kickoff e close — não há
parametrização automática na v1.

## Status & roadmap

**v0.1 — MVP inicial.** Este primeiro release é deliberadamente minimalista:
entrega o método (as duas skills core + o scaffold) pra ser validado e refinado
no uso real antes de crescer. Espere que a superfície evolua conforme o feedback.

## Licença

[MIT](./LICENSE)
