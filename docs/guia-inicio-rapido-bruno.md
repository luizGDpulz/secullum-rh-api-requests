# 🚀 Guia de Início Rápido no Bruno

Este guia leva você do zero até a primeira requisição funcionando na API de Integração Externa do Secullum RH.

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

As variáveis sensíveis (`username`, `password` e `access_token`) já vêm marcadas como **Secrets** (`secret: true`) no environment **Secullum RH (Produção)**. Isso significa que o Bruno **não grava seus valores no arquivo `.yml`**, mantendo-os salvos localmente de forma segura e sem sujar o Git!

### Opção A — Preencher na aba Secrets (Recomendado)
1. No canto superior direito do Bruno, selecione o environment **Secullum RH (Produção)**.
2. Clique no ícone de editar o environment e vá na aba **Secrets**.
3. Preencha **`username`** e **`password`** e clique em **Save**.

### Opção B — Criar um Environment Local (`*.local.yml`)
- Se você também quiser customizar outras variáveis padrão (como `data_inicio`, `data_fim`, `funcionario_cpf`) sem gerar conflito no `git pull`, crie um environment chamado **`Producao.local`** (salvo como `Producao.local.yml`, já ignorado pelo `.gitignore`).

---

## 4. Fluxo de Autenticação (Obrigatório antes de testar)

Toda chamada na API do Secullum RH precisa de duas coisas: **Token Bearer** e **ID do Banco (`secullumidbancoselecionado`)**.

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
