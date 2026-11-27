# 🔄 Guia de Atualização para o Time de Suporte

Sempre que novos endpoints, correções de payload ou ajustes no Swagger forem publicados neste repositório, você pode atualizar sua coleção em segundos.

---

## ⭐ Forma Recomendada: `git pull` (Automático no Bruno)

Como o Bruno lê os arquivos `.yml` diretamente da pasta no seu computador, você **nunca precisa reimportar nada**.

### Pelo Terminal (Windows / Linux / macOS)
Entre na pasta onde você clonou o projeto e execute:
```bash
git pull
```

### Pelo GitHub Desktop ou VS Code
1. Abra o repositório no **GitHub Desktop** (ou VS Code).
2. Clique em **Fetch origin** → **Pull origin**.

Assim que o comando terminar, o Bruno já reflete todas as alterações imediatamente.

---

## 🛡️ Como evitar conflitos ao atualizar?

As variáveis `username`, `password` e `access_token` já são **Secrets** no Bruno, então preenchê-las na aba **Secrets** não altera nenhum arquivo do repositório.

Se você quiser alterar outras variáveis (como `data_inicio`, `funcionario_cpf`, etc.) sem risco de conflito no `git pull`:
1. Use um environment com sufixo **`.local.yml`** (ex.: `Producao.local.yml`), pois ele é ignorado pelo `.gitignore`.
2. Se você acabou editando `Producao.yml` sem querer e o `git pull` reclamar, limpe a alteração local antes de puxar:
   ```bash
   git checkout -- bruno/environments/Producao.yml
   git pull
   ```

---

## 📦 Alternativa sem Git (Download ZIP)

Se alguém do time não quiser instalar o Git:
1. Acesse a página do repositório no GitHub.
2. Clique em **Code → Download ZIP** (ou baixe a última **Release**).
3. Extraia a pasta `bruno/` substituindo a anterior.
4. *(Atenção)* Se você tinha um environment `Producao.local.yml` salvo, faça backup dele antes de substituir a pasta inteira.
