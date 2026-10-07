# Versionamento semântico

Formato `MAJOR.MINOR.PATCH`, tag `vX.Y.Z` (ver https://semver.org/lang/pt-BR/).

| Incremento | Quando | Exemplo |
| --- | --- | --- |
| MAJOR | Mudança incompatível: remove ou muda API, formato de dados, comportamento de que alguém depende, migração obrigatória | 1.4.2 → 2.0.0 |
| MINOR | Funcionalidade nova compatível com o que já existe | 1.4.2 → 1.5.0 |
| PATCH | Correção de bug ou ajuste interno sem mudança de comportamento esperado | 1.4.2 → 1.4.3 |

## Como decidir a partir do `[Unreleased]`

- Há item marcado como incompatível (`### Removed`, `BREAKING`, commit com `!`) → MAJOR.
- Senão, há algum `### Added` → MINOR.
- Senão (só `### Fixed`, `### Security`, `### Changed` interno) → PATCH.

## Antes da 1.0.0

Projetos em `0.y.z` ainda não têm API estável: mudança incompatível sobe o MINOR (0.4.0 → 0.5.0) e o resto sobe o PATCH. A `1.0.0` é decisão do Vinicius, quando o projeto entra em uso real.

## Pré-lançamentos

Use sufixos só se pedido: `1.5.0-beta.1`, `1.5.0-rc.1`.

## Nunca

- Reutilizar ou mover uma tag já publicada.
- Pular números sem motivo.
- Criar tag sem a seção correspondente no CHANGELOG.
