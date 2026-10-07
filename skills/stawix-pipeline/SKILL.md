---
name: stawix-pipeline
description: Fluxo de desenvolvimento do Vinicius para este projeto. Use ao iniciar ou terminar qualquer tarefa de código, corrigir bugs, atualizar CHANGELOG, fechar versão, sugerir tag semântica ou gerar comandos de commit e push. Atualiza o Skyle via MCP, segue SemVer, Keep a Changelog e as políticas de código do projeto, e nunca faz commit sozinho.
---

# Pipeline de desenvolvimento (Stawix)

Fluxo: **Skyle → código → CHANGELOG → versão semântica → comandos git → deploy (manual)**. A memória das sessões fica no ai-memory, capturada automaticamente pelos hooks.

## Regras que nunca mudam

1. **Nunca execute** `git commit`, `git push`, `git tag`, `git merge` nem abra PR. Gere os comandos e entregue ao Vinicius.
2. **Sempre atualize o `CHANGELOG.md`** em toda mudança de código ou de comportamento (veja `references/changelog.md`).
3. **Siga as políticas de código** em `references/politicas-codigo.md`.
4. **Deploy é manual.** Não rode deploy, pipeline ou publicação.

## Ao iniciar uma tarefa

1. Descubra o slug do projeto na linha `## Skyle (projeto: <slug>)` do `AGENTS.md`.
2. Se o MCP do Skyle estiver disponível, chame `skyle_start(projeto, card)` com o número do card, ou com `titulo` se o card não existir. Não leia o kanban antes.
3. Se a tarefa for "corrija os bugs", chame `next_bug(projeto)` e trabalhe um bug por vez, até vir vazio.
4. Não registre nada manualmente no ai-memory: os hooks já capturam a sessão. Use a busca do ai-memory só se precisar de contexto de sessões anteriores.

## Ao terminar uma tarefa

1. Rode os testes e o lint do que mudou.
2. Adicione a entrada no `CHANGELOG.md`, em `[Unreleased]`, na categoria certa, com `(#<card>)` no fim.
3. Chame `skyle_done(projeto, card, resumo, proximo, changelog)`:
   - `resumo`: uma frase com o que foi feito.
   - `proximo`: uma frase com o próximo passo.
   - `changelog`: a linha exata que você adicionou.
   Se o MCP do Skyle não estiver disponível, siga sem ele e escreva o resumo e o próximo passo na resposta.
4. Entregue os comandos de commit, sem executar:

```bash
git add <arquivos alterados>
git commit -m "<tipo>(<escopo>): <descrição curta> (#<card>)"
git push
```

Tipos de commit: `feat`, `fix`, `docs`, `refactor`, `test`, `chore`, `perf`. Mudança incompatível leva `!` depois do tipo (`feat!:`).

## Ao fechar uma versão (só quando o Vinicius pedir)

1. Leia `[Unreleased]` e proponha o incremento pelas regras de `references/semver.md`, explicando em uma linha por quê.
2. Depois da confirmação:
   - mova `[Unreleased]` para `## [X.Y.Z] - AAAA-MM-DD` e deixe um `[Unreleased]` vazio no topo;
   - atualize a versão no manifesto do projeto (`pyproject.toml`, `pubspec.yaml`, `package.json` ou equivalente);
   - atualize os links de comparação no fim do CHANGELOG, se existirem.
3. Entregue os comandos, sem executar:

```bash
git add CHANGELOG.md <manifesto>
git commit -m "chore(release): vX.Y.Z"
git tag -a vX.Y.Z -m "vX.Y.Z"
git push && git push origin vX.Y.Z
```

4. Lembre que o deploy é o próximo passo, feito pelo Vinicius.

## Respostas

Curtas e em português. Ao final de cada tarefa: o que foi feito, o próximo passo e os comandos.
