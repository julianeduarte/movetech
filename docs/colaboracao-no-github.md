# 🤝 Colaboração no GitHub

Este passo a passo cobre o fluxo colaborativo de desenvolvimento com Git e GitHub:
- Abrir um Pull Request a partir da branch criada no Lab 1.
- Revisar o código e aprovar o Pull Request.
- Fazer o merge na `main`.
- Provocar e resolver um conflito de merge.
- Reverter uma alteração com `git revert`.

> **⚠️ Pré-requisito:** Lab H1 - Lab 1 concluído. A branch `feature/adiciona-gitignore` deve existir no seu repositório do GitHub.

---

## 1. Abrir um Pull Request

Um Pull Request (PR) é a forma de propor que suas alterações entrem na branch principal. No GitHub, qualquer pessoa pode revisar e comentar antes do merge.

👣 **Passo a passo:** 
Acesse seu repositório no GitHub → clique em **"Compare & pull request"** (banner amarelo) ou vá em **Pull requests** → **"New pull request"**.

**Preencha os campos:**
- **Base:** `main`
- **Compare:** `feature/adiciona-gitignore`
- **Título:** `chore: adiciona .gitignore`
- **Descrição:** Adiciona `.gitignore` com entradas para `__pycache__`, `.env` e `.venv`.

Clique em **"Create pull request"**.

> 💡 **Nota:** O GitHub exibe as alterações feitas, arquivo por arquivo, na aba *"Files changed"*.

---

## 2. Revisar o código (Code Review)

Em times reais, outra pessoa sempre revisa o PR antes do merge — ninguém aprova o próprio trabalho. Neste lab, um colega vai revisar o seu PR (o facilitador vai organizar os pares/grupos na aula).

**O revisor deve:**
1. Acessar o link do PR que você vai compartilhar → ir na aba **"Files changed"**.
2. Passar o mouse sobre uma linha do `.gitignore` → clicar no ícone **"+" azul** → escrever um comentário como: *"Adicionar também `node_modules/` caso o projeto ganhe frontend no futuro."*
3. Clicar em **"Start a review"** → **"Finish your review"** → selecionar **"Approve"** → **"Submit review"**.

✅ **Resultado esperado:** o PR mostra um selo verde *"✓ 1 approving review"*.

> 🔒 **Por que não dá para aprovar o próprio PR?** 
> O GitHub bloqueia auto-aprovação por design — code review só tem valor quando é feito por outra pessoa.

---

## 3. Fazer o merge

Com a revisão aprovada, faça o merge da branch na `main`:

👣 Na página do PR → clique em **"Merge pull request"** → **"Confirm merge"**.

✅ **Resultado esperado:** mensagem *"Pull request successfully merged and closed"*.

Atualize sua cópia local da `main`:
```bash
git checkout main
git pull
