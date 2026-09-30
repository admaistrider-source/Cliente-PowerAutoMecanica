# Time de agentes de desenvolvimento

Seis subagentes do Claude Code para o sistema da Powers Auto Mecânica: clientes, veículos, ordens de serviço, orçamentos, estoque de peças e agendamentos.

| Agente | Papel | Modelo | Edita código? |
|---|---|---|---|
| `arquiteto` | Planeja a funcionalidade e divide as tarefas | opus | Só documentos em `docs/` |
| `backend` | Banco, migrações, APIs e regras de negócio | sonnet | Sim |
| `frontend` | Telas, formulários e fluxos | sonnet | Sim |
| `devops` | Ambientes, deploy, CI/CD, backups e monitoramento | sonnet | Sim (infraestrutura) |
| `qa-testes` | Testes e reprodução de bugs | sonnet | Só testes |
| `revisor-codigo` | Revisão antes do merge | opus | Não |

## Estrutura
```
Agentes de desenvolvimento/
├── README.md
└── .claude/
    └── agents/
        ├── arquiteto.md
        ├── backend.md
        ├── devops.md
        ├── frontend.md
        ├── qa-testes.md
        └── revisor-codigo.md
```

## Instalação
1. Copie a pasta `.claude/` para a raiz do repositório do projeto. O Claude Code carrega os agentes automaticamente; confira com `/agents`.
2. Crie na raiz do repositório um `CLAUDE.md` com o conteúdo da seção "Contexto do projeto" abaixo. Os agentes leem stack, comandos e convenções de lá.

## Como usar
Peça pelo nome ou deixe o Claude escolher pela descrição:

```
Use o arquiteto para planejar o cadastro de ordens de serviço.
Use o backend para implementar as tarefas 1 a 3 do plano.
Use o frontend para a tela de orçamento.
Use o devops para configurar o CI e o deploy de homologação.
Use o qa-testes para testar o fluxo da OS de ponta a ponta.
Use o revisor-codigo para revisar as mudanças antes do PR.
```

Fluxo recomendado para cada funcionalidade: `arquiteto` planeja → `backend`, `frontend` e `devops` implementam (podem rodar em paralelo) → `qa-testes` testa → `revisor-codigo` revisa.
Planos em `docs/planos/`, decisões em `docs/decisoes/`.

## Contexto do projeto

### Stack
A definir. Sugestão padrão até decisão em contrário: Next.js + TypeScript, PostgreSQL (Supabase ou Prisma), Tailwind, Vitest e Playwright.

### Comandos
Preencher quando o projeto for criado (instalar, rodar, testar, lint, typecheck, deploy).

### Convenções
- Interface e documentação em português do Brasil.
- Valores monetários nunca em float.
- Dados pessoais (CPF, telefone) fora dos logs.

## Personalização
- Quando a stack for definida, atualize as seções Stack e Comandos (aqui e no `CLAUDE.md` do repositório).
- Para trocar o modelo de um agente, edite o campo `model:` no topo do arquivo.
