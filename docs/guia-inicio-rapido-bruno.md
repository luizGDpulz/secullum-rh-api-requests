# 🚀 Guia de Início Rápido no Bruno

Este guia leva você do zero até a primeira requisição funcionando na API de Integração Externa do Secullum Ponto Web.

---

## 1. Pré-requisitos

1. **Bruno** instalado ([download oficial](https://www.usebruno.com/downloads)).
2. **Git** instalado (ou **GitHub Desktop** / **VS Code**, se preferir interface gráfica).
3. Credenciais de acesso de integração externa do cliente (`username` e `password`).

---

## 2. Clonar e abrir a coleção

1. Escolha uma pasta fixa no seu computador (ex.: `C:\Dev\` ou `~/dev/`) e clone o repositório:
   ```bash
   git clone https://github.com/luizGDpulz/secullum-rh-api-requests.git
   ```
2. Abra o **Bruno**.
3. Clique em **Open Collection** e selecione a pasta `bruno/` dentro de `secullum-rh-api-requests`.

---

## 3. Configurar credenciais sem conflito no Git

Para evitar que suas senhas ou alterações locais bloqueiem futuras atualizações (`git pull`):

### Opção A — Criar um Environment Local (Recomendado)
1. No canto superior direito do Bruno, abra o seletor de **Environments**.
2. Copie o conteúdo de `Secullum Ponto Web (Produção)` (arquivo `bruno/environments/Producao.yml`) ou crie um novo environment chamado **`Producao.local`** (o arquivo será salvo como `Producao.local.yml`, que já está no `.gitignore`).
3. Preencha **`username`** e **`password`** e salve.

### Opção B — Usar variáveis temporárias (Runtime)
- Se você preferir não salvar a senha em disco, preencha `username` e `password` apenas na sessão atual ou na aba **Vars** sem commitar alterações.

---

## 4. Fluxo de Autenticação (Obrigatório antes de testar)

Toda chamada na API do Ponto Web precisa de duas coisas: **Token Bearer** e **ID do Banco (`secullumidbancoselecionado`)**.

1. Abra a pasta **`01-autenticacao-e-selecao-de-banco`**.
2. Execute **`01-token`** (`POST /Token`):
   - Deve retornar **Status `200`**.
   - O script automático já salva o `access_token` na collection e no environment ativo.
3. Execute **`03-listar-bancos`** (`GET /ContasSecullumExterno/ListarBancos`):
   - Deve retornar **Status `200`** com a lista de bancos do usuário.
   - O script automático salva o **primeiro banco** em `selected_bank_id`.
   - **Cliente com mais de um banco?** Abra a aba **Console** (ou Timeline) do Bruno após rodar `Listar Bancos` — o script imprime todos os bancos disponíveis com `id`, `identificador` e `nome`. Copie o `id` desejado e cole na variável `selected_bank_id` do seu environment.

---

## 5. Testando os endpoints

Agora basta abrir qualquer pasta (`04-batidas`, `08-empresas`, `12-funcionarios`, etc.) e clicar em **Send**:

- **Listagens (`GET`):** os filtros opcionais vêm **desmarcados** por padrão para facilitar o teste rápido. Se precisar filtrar por CPF, PIS ou CNPJ, basta marcar a caixa de seleção do parâmetro na aba **Params**.
- **Criação/Edição (`POST`):** revise o JSON na aba **Body** antes de enviar — os exemplos usam variáveis como `{{empresa_documento}}` e `{{funcionario_cpf}}`.
