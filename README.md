# Claude Harness

> Sistema de desenvolvimento disciplinado para o Claude — Plan → Work → Review → Release

O Claude Harness é um system prompt que transforma o Claude de um assistente reativo em um parceiro de desenvolvimento disciplinado. Ele impõe um ciclo estruturado com checkpoints obrigatórios que o Claude não pode contornar.

## Como funciona

O system prompt redefine o comportamento do Claude para desenvolvimento de software. Mensagens com prefixos `[HARNESS:FASE]` sinalizam em qual etapa o ciclo está. O Claude lê esses prefixos e opera de acordo. Os gates de aprovação pertencem ao humano — o Claude não avança fases por conta própria.

```
IDLE → PLANNING → WORK → REVIEW → RELEASED
         ↑ gate humano  ↑ gate humano  ↑ gate humano
```

## Funcionalidades

- **Fase PLANNING** — Claude produz resumo da spec, checklist de segurança, checklist de performance e tasks numeradas antes de escrever qualquer código
- **Fase WORK** — Claude implementa uma task por vez, nunca avançando sem confirmação humana explícita
- **Fase REVIEW** — Review estruturado em 4 perspectivas: Segurança, Performance, Qualidade de Código, Critérios de Aceitação
- **Fase RELEASE** — CHANGELOG, resumo de decisões de segurança, resumo de otimizações de performance
- **Gates** — Claude recusa pular fases. Tentativas de bypass retornam `⛔ HARNESS: ...`

## Setup

### 1. Crie um Project no claude.ai

Vá em **claude.ai → Projects → New Project**.

### 2. Adicione o system prompt

Copie o conteúdo de [`system-prompt.md`](./system-prompt.md) no campo **Project Instructions**.

### 3. Comece a usar

Abra qualquer chat dentro do projeto e descreva o que quer construir. O Claude seguirá o fluxo automaticamente.

## Gates — violações proibidas

| Tentativa | Resposta do Claude |
|-----------|-------------------|
| Implementar sem plano aprovado | `⛔ HARNESS: Crie e aprove um plano primeiro.` |
| Avançar task sem confirmação | `⛔ HARNESS: Aguardo confirmação da task atual.` |
| Fazer release sem review | `⛔ HARNESS: O review precisa ser concluído primeiro.` |
| Ignorar checklist de segurança | Não permitido — segurança é parte do entregável |

## Estrutura

```
claude-harness/
├── README.md
├── system-prompt.md   ← cole isso no Project Instructions
└── LICENSE
```

## Licença

Apache 2.0 — veja [LICENSE](./LICENSE)
