# Changelog

Todas as mudanças relevantes deste repositório são registradas aqui.

O formato segue [Keep a Changelog](https://keepachangelog.com/pt-BR/1.1.0/) e o projeto usa [Versionamento Semântico](https://semver.org/lang/pt-BR/).

## [Unreleased]

### Changed

- `stawix-pipeline`: ao iniciar um card, ler o retorno do `skyle_start` e usar `skyle_card`/`skyle_anexo` quando a descrição vier cortada, houver anexos ou campos do bug; nunca abrir a interface do Skyle para ler um card.
- `stawix-pipeline`: ao fechar uma versão, atualizar também o selo de versão do `README.md`, se existir.
- `stawix-pipeline`: formato da tag configurável por projeto (`Formato de tag:` no `AGENTS.md`, senão o padrão das tags existentes, senão `vX.Y.Z`); comandos de release usam `<tag>`.
- `stawix-pipeline`: tarefas que alteram mais de um repositório atualizam o CHANGELOG e geram comandos de commit para cada repositório.
- `stawix-pipeline`: checklist do card no Skyle — `passos` no `skyle_start` para tarefas com mais de duas etapas e `skyle_passo` ao concluir cada etapa.
- `stawix-pipeline`: atualizar o Skyle a cada card concluído (`skyle_done` antes do próximo), sem acumular para o fim da conversa.

### Added

- Skill `stawix-pipeline`: integração com o Skyle via MCP, CHANGELOG no formato Keep a Changelog, versionamento semântico e geração de comandos git sem executá-los.
- README do repositório e da skill, com instalação por projeto para Claude Code e Codex.
- Licença MIT.
