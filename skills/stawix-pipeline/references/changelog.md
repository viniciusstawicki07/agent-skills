# CHANGELOG (Keep a Changelog)

Arquivo `CHANGELOG.md` na raiz, no formato https://keepachangelog.com/pt-BR/1.1.0/. Se o projeto não tiver um, crie a partir de `templates/CHANGELOG.md`.

## Estrutura

```markdown
## [Unreleased]

### Added
- Exportação de notas em PDF (#24)

### Fixed
- Upload de XML acima de 5 MB (#25)

## [1.4.2] - 2026-10-05
...
```

## Categorias

| Categoria | Para |
| --- | --- |
| `Added` | Funcionalidades novas |
| `Changed` | Mudanças em funcionalidades existentes |
| `Deprecated` | O que vai ser removido |
| `Removed` | O que foi removido |
| `Fixed` | Correções de bugs |
| `Security` | Correções de vulnerabilidades |

## Regras

- Uma linha por mudança, escrita para quem usa o software, não para quem lê o código.
- Sempre com o número do card no fim: `(#24)`.
- Toda entrada nova vai em `[Unreleased]`; versões fechadas não são editadas.
- Datas no formato `AAAA-MM-DD`; versão mais recente no topo.
- Mudança só de teste, lint ou formatação não precisa de entrada.
