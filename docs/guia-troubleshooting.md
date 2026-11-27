# 🛠️ Troubleshooting & Dicas Rápidas (Suporte)

Problemas mais comuns ao testar a API do Secullum RH e como resolver rápido.

---

## 1. Erro `401 Unauthorized`
- **Causa mais comum:** o `access_token` expirou ou não foi gerado.
- **Solução:** rode novamente `01-autenticacao-e-selecao-de-banco/01-token` e tente a requisição de novo.
- **Se `01-token` também falhar:** confira se `username` e `password` estão corretos no environment selecionado (cuidado com espaços extras ao copiar/colar).

## 2. Erro `400` ou dados vazios mesmo com token válido
- **Verifique o banco selecionado:** confira se `selected_bank_id` está preenchido e corresponde ao banco correto do cliente.
  - Rode `01-autenticacao-e-selecao-de-banco/03-listar-bancos` e veja os IDs listados no Console do Bruno.
- **Verifique os filtros da URL:** nas requisições `GET`, se você marcou algum filtro opcional (`FuncionarioPis`, `FuncionarioCpf`, `cnpjCpf`, `descricao`), confirme se o valor na aba **Params** ou no Environment é realmente do cliente que você está testando (por padrão vêm preenchidos com valores fictícios como `12345678901`).

## 3. O cliente tem mais de um banco na mesma conta
- Ao rodar `03-listar-bancos`, o script salva automaticamente o **primeiro** banco (`res.body[0]`).
- Para testar outro banco:
  1. Veja a resposta JSON de `03-listar-bancos` (ou o Console do Bruno).
  2. Copie o `id` do banco desejado.
  3. Cole esse valor na variável `selected_bank_id` do seu environment.

## 4. Diferenças entre o Manual PDF e o Swagger
- O manual PDF da Secullum é mais antigo que o Swagger vivo da API.
- **Sempre confie no Swagger vivo** em caso de dúvida:
  - `IntegracaoExterna/Pendencias`: citada no PDF, mas não existe mais no Swagger atual.
  - `GravarLogsIniciarBkp` e `PontoOffline/AssinaturaArquivo/Assinar`: existem no Swagger atual, mas não constam no PDF.

## 5. Datas padrão nos filtros
- Variáveis como `data_inicio` (`2024-01-01`) e `data_fim` (`2024-01-31`) vêm com valores de exemplo.
- Ao testar `04-batidas` ou `11-fonte-de-dados`, ajuste `data_inicio` e `data_fim` no seu environment local para o período real do chamado.
