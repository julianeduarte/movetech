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
```

✅ **Resultado esperado — o `.gitignore` agora está na `main` local:**
```text
Updating a1b2c3d..b3c4d5e
Fast-forward
 .gitignore | 4 ++++
```

---

## 4. Provocar e resolver um conflito de merge

Conflitos acontecem quando duas pessoas alteram a mesma linha do mesmo arquivo. Vamos simular isso:

Crie duas branches a partir da `main`, ambas alterando a mesma linha do `README.md`:
```bash
git checkout main
git checkout -b branch-A
```

Edite a última linha do `README.md`, escreva: *"Versão A do repositório."*
```bash
git add README.md
git commit -m "docs: versão A"
```

Volte para a `main` e crie a `branch-B` com uma alteração conflitante na mesma linha:
```bash
git checkout main
git checkout -b branch-B
```

Edite a mesma última linha do `README.md`, escreva: *"Versão B do repositório."*
```bash
git add README.md
git commit -m "docs: versão B"
```

Faça o merge da `branch-A` na `main` (vai direto, sem conflito):
```bash
git checkout main
git merge branch-A
```

Agora tente fazer o merge da `branch-B` (aqui surge o conflito):
```bash
git merge branch-B
```

⚠️ **Resultado esperado:**
```text
CONFLICT (content): Merge conflict in README.md
Automatic merge failed; fix conflicts and then commit the result.
```

Abra o `README.md` — o Git marcou o conflito:
```text
<<<<<<< HEAD
Versão A do repositório.
=======
Versão B do repositório.
>>>>>>> branch-B
```

**Edite o arquivo para resolver:** escolha uma versão (ou combine as duas) e remova as marcações. Por exemplo:
*Versão final do repositório (A + B combinados).*

Finalize o merge:
```bash
git add README.md
git commit -m "merge: resolve conflito entre branch-A e branch-B"
```

✅ **Resultado esperado:** `[main c4d5e6f] merge: resolve conflito entre branch-A e branch-B`

---

## 5. Reverter uma alteração com `git revert`

Se um commit com problema chegar à `main`, o `git revert` cria um novo commit que desfaz as alterações — sem reescrever o histórico.

Primeiro, crie um commit para reverter. Adicione uma linha qualquer ao `README.md`:
```bash
echo "Linha adicionada por engano." >> README.md
git add README.md
git commit -m "chore: linha adicionada por engano"
```

Verifique o histórico para confirmar que o commit está no topo:
```bash
git log --oneline
```

✅ **Resultado esperado — o commit novo aparece em HEAD:**
```text
a1b2c3d (HEAD -> main) chore: linha adicionada por engano
b3c4d5e merge: resolve conflito entre branch-A e branch-B
...
```

Agora reverta o commit do topo do histórico:
```bash
git revert HEAD --no-edit
```

✅ **Resultado esperado — um novo commit de reversão é criado automaticamente:**
```text
[main d5e6f7g] Revert "chore: linha adicionada por engano"
 1 file changed, 1 deletion(-)
```

Envie a `main` atualizada para o GitHub:
```bash
git push
```

> 🛡️ **Ponto importante:** `git revert` não apaga o histórico — apenas adiciona um commit que desfaz as alterações. Isso é seguro para branches compartilhadas.
>
> 💡 **Por que `HEAD` e não o hash?** `git revert HEAD` desfaz sempre o commit mais recente. Usar o hash de um commit mais antigo pode falhar se o conteúdo do arquivo já foi modificado por commits posteriores.

---

## ✅ Checklist Rápido

```bash
# Após merge, atualizar a main local
git checkout main && git pull

# Simular conflito
git checkout -b branch-A
# edite README.md → git add . → git commit -m 'docs: versão A'
git checkout main
git checkout -b branch-B
# edite a mesma linha → git add . → git commit -m 'docs: versão B'
git checkout main && git merge branch-A
git merge branch-B
# edite README.md (remove marcações) → git add README.md → git commit -m 'merge: resolve conflito'

# Reverter o commit mais recente
echo "Linha adicionada por engano." >> README.md
git add README.md && git commit -m "chore: linha adicionada por engano"
git revert HEAD --no-edit
git push
```
