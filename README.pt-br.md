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
| `specsmith-init` | Copia o scaffold `specs/` (README + templates em branco) pro seu projeto, pra que o fluxo spec-driven tenha uma casa local. Opcional — a `prompt-grill` funciona sem ele. |

## Instalação

No Claude Code:

```
/plugin marketplace add murilobauck/specsmith
/plugin install specsmith@specsmith
```

Depois de instalar, as skills ficam disponíveis globalmente em qualquer
projeto — sem passo de cópia ou geração por projeto.

## Recomendado: leve o scaffold specs/ pro projeto

O Specsmith funciona de cara (a `prompt-grill` carrega a estrutura da spec
sozinha). Mas pra melhores resultados, coloque o scaffold `specs/` no seu
projeto, pra que o README e os templates de `plan.md` / `tasks.md` morem no seu
repo e o time inteiro veja o método:

```
/specsmith-init
```

Isso copia `specs/README.md` e `specs/_template/` pra raiz do seu projeto, sem
sobrescrever nada que já exista. Você também pode copiar a pasta `specs/` deste
repo manualmente, se preferir.

## Começando

1. (Opcional, mas recomendado) Rode `/specsmith-init` pra criar o scaffold `specs/`.
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

No roadmap:

- **Suporte ao Antigravity** — um release futuro vai disponibilizar o Specsmith
  também pro Antigravity, não só pro Claude Code.

## Licença

[MIT](./LICENSE)
