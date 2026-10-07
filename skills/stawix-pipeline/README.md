# stawix-pipeline

Skill para Claude Code e Codex que aplica o fluxo de desenvolvimento da Stawix Tech em um projeto: atualizar o [Skyle](#skyle) via MCP, manter o `CHANGELOG.md` no formato Keep a Changelog, versionar com SemVer e entregar os comandos de git prontos, **sem nunca fazer commit, push ou tag sozinho**.

```
Skyle (MCP) → código → CHANGELOG.md → versão semântica → comandos git → deploy (manual)
                      └──────── memória das sessões no ai-memory ────────┘
```

## O que a skill faz

| Momento | O agente |
| --- | --- |
| Início da tarefa | Chama `skyle_start` no Skyle; em "corrija os bugs", chama `next_bug` e trabalha um por vez |
| Fim da tarefa | Roda testes e lint, adiciona a linha em `[Unreleased]` com `(#card)`, chama `skyle_done` e entrega `git add` / `git commit` / `git push` para você executar |
| Fechar versão (só quando pedido) | Propõe o incremento SemVer a partir do `[Unreleased]`, move a seção para `[X.Y.Z] - AAAA-MM-DD`, atualiza o manifesto e entrega os comandos de commit, `git tag` e push |
| Deploy | Nunca. Fica com você |

Sem o Skyle rodando, a skill pula as chamadas ao MCP e escreve o resumo e o próximo passo na resposta, então funciona desde já.

## Conteúdo

```
stawix-pipeline/
├── SKILL.md                     # instruções que o agente segue
├── references/
│   ├── semver.md                # quando subir MAJOR, MINOR ou PATCH
│   ├── changelog.md             # categorias e regras do Keep a Changelog
│   └── politicas-codigo.md      # políticas de código (a completar)
└── templates/
    ├── CHANGELOG.md             # modelo para projetos sem CHANGELOG
    └── AGENTS-bloco.md          # bloco para colar no AGENTS.md do projeto
```

## Instalação por projeto

A skill fica **dentro do projeto**, para só valer onde você quiser. Não instale em `~/.claude/skills`, que a ativaria em todos os projetos.

**PowerShell**, na raiz do projeto:

```powershell
$skill = "C:\Users\vinicius.muller\Documents\Projetos_Dev\03_Pessoal\agent-skills\skills\stawix-pipeline"
New-Item -ItemType Directory -Force .claude\skills, .codex\skills | Out-Null
Copy-Item -Recurse -Force $skill .claude\skills\
Copy-Item -Recurse -Force $skill .codex\skills\
Remove-Item .claude\skills\stawix-pipeline\README.md, .codex\skills\stawix-pipeline\README.md
```

**Bash / Git Bash**:

```bash
SKILL=/caminho/para/agent-skills/skills/stawix-pipeline
mkdir -p .claude/skills .codex/skills
cp -r "$SKILL" .claude/skills/ && cp -r "$SKILL" .codex/skills/
rm .claude/skills/stawix-pipeline/README.md .codex/skills/stawix-pipeline/README.md
```

Depois:

1. Cole o conteúdo de `templates/AGENTS-bloco.md` no `AGENTS.md` do projeto, trocando `<slug-do-projeto>` pelo slug do projeto no Skyle.
2. Se o projeto tiver `CLAUDE.md`, garanta a linha `@AGENTS.md` nele.
3. Se o projeto não tiver `CHANGELOG.md`, copie o de `templates/`.

| Agente | Pasta da skill no projeto |
| --- | --- |
| Claude Code | `.claude/skills/stawix-pipeline/` |
| Codex | `.codex/skills/stawix-pipeline/` |

## Uso

A skill é carregada sozinha quando a tarefa combina com a descrição dela (iniciar ou terminar tarefa, corrigir bugs, atualizar CHANGELOG, fechar versão). No Claude Code, também dá para chamar direto com `/stawix-pipeline`.

Exemplos de pedidos:

- "Implemente o card 24."
- "Leia os bugs e corrija."
- "Feche a versão." → o agente propõe, por exemplo, `1.4.2 → 1.5.0` e explica o motivo.

## Convenções

- **Tags:** `vX.Y.Z` (ex.: `v1.5.0`), anotadas.
- **Commits:** Conventional Commits — `feat`, `fix`, `docs`, `refactor`, `test`, `chore`, `perf`; `!` para mudança incompatível; número do card no fim, `(#24)`.
- **CHANGELOG:** uma linha por mudança, escrita para quem usa o software, sempre com `(#card)`.
- **Projetos `0.y.z`:** mudança incompatível sobe o MINOR; a `1.0.0` é decisão manual.

## Skyle

O Skyle (em desenvolvimento) é o painel visual de projetos que recebe as atualizações dos agentes (kanban, "onde parei", bugs, verificação de CHANGELOG). Ferramentas MCP usadas pela skill:

| Ferramenta | Uso |
| --- | --- |
| `skyle_start(projeto, card ou titulo)` | Card vai para "Em andamento" |
| `skyle_done(projeto, card, resumo, proximo, changelog)` | Card vai para "Em testes" e o "Onde parei" é atualizado |
| `next_bug(projeto)` | Pega o bug aberto de maior severidade |

## Atualizar a skill nos projetos

A cópia mestre é esta pasta. Depois de alterar, copie de novo para os projetos que usam a skill e registre a mudança no `CHANGELOG.md` deste repositório.
