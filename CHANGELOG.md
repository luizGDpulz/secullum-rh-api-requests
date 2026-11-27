# Changelog

Todas as mudanças relevantes deste repositório são documentadas neste arquivo.

O formato segue [Keep a Changelog](https://keepachangelog.com/pt-BR/1.0.0/) e este projeto adere ao [Versionamento Semântico](https://semver.org/lang/pt-BR/).

## [Não lançado]

## [1.0.0] - 2026-11-27

### Adicionado
- Coleção **Bruno** (OpenCollection YAML) completa com 63 requests cobrindo autenticação e todas as rotas do Swagger vivo da integração externa do Secullum RH.
- Guias práticos em [`docs/`](./docs/) para início rápido no Bruno, atualização contínua via `git pull` e troubleshooting.
- Capa SVG recortada ([`assets/cover.svg`](./assets/cover.svg)) e [`README.md`](./README.md) reestruturado com foco no Bruno e uso comunitário.
- Versão `1.0.0` definida em [`bruno/opencollection.yml`](./bruno/opencollection.yml).

### Alterado
- Parâmetros opcionais de filtro em 11 listagens `GET` desabilitados por padrão no Bruno e no Postman para execução com 1 clique.
- Scripts de `01-token.yml` e `03-listar-bancos.yml` aprimorados para gravar variáveis na collection e no environment ativo, além de listar bancos disponíveis no Console do Bruno.
- Environment do Bruno renomeado para `Secullum RH (Produção)` e `.gitignore` configurado para ignorar `*.local.yml` e `.env`.
- Artefatos secundários do Postman atualizados e renomeados para `secullum-rh.postman_collection.json` e `secullum-rh.postman_environment.json`.

### Removido
- Snapshot estático `swagger.json` local (substituído por referência direta ao Swagger vivo).

[Não lançado]: https://github.com/luizGDpulz/secullum-rh-api-requests/compare/v1.0.0...HEAD
[1.0.0]: https://github.com/luizGDpulz/secullum-rh-api-requests/releases/tag/v1.0.0
