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
aprovada.

## O que vem na caixa

| Skill | O que faz |
|---|---|
| `prompt-grill` | Interroga um pedido vago uma pergunta por vez até poder ser escrito como uma spec assertiva, e então gera `specs/<feature>/spec.md`. |
| `dev-lifecycle` | A fonte única da mecânica git: branch a partir de `develop`, Conventional Commits, um commit por task, gates verdes, e um PR que pausa pra sua aprovação. |

O plugin também distribui o scaffold `specs/` (um README explicando o ciclo e um
`_template/` em branco) pra que qualquer projeto receba a estrutura do método de
graça.

## Instalação

No Claude Code:

```
/plugin marketplace add murilobauck/specsmith
/plugin install specsmith@specsmith
```

Depois de instalar, as duas skills ficam disponíveis globalmente em qualquer
projeto — sem passo de cópia ou geração por projeto.

## Começando

1. Rode o `prompt-grill` (ou só diga "me entrevista sobre X"). Ele conduz a
   entrevista e escreve `specs/<feature>/spec.md`.
2. Com a spec aprovada, escreva `plan.md` (copie de `specs/_template/plan.md`).
3. Com o plano aprovado, quebre em `tasks.md` (copie de
   `specs/_template/tasks.md`).
4. Implemente task por task. O `dev-lifecycle` cuida da branch, dos commits e do PR.

## Sobre o fluxo de git

O `dev-lifecycle` vem como um fluxo de referência opinativo (branches baseadas em
`develop`, Conventional Commits, PR pausado pra aprovação). Times que usam um
modelo de git diferente devem adaptar as fases de kickoff e close — não há
parametrização automática na v1.

## Licença

[MIT](./LICENSE)
