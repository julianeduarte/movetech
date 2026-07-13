# Laboratório: Seu Primeiro Repositório

Este repositório contém o passo a passo para o ciclo completo de versionamento inicial utilizando Git e GitHub. 

## 📋 Pré-requisitos
- Git instalado na máquina (verifique com `git --version`).
- Conta no GitHub criada e autenticada.

---

## 🚀 Passo a Passo

### 1. Criar o repositório no GitHub
Crie um repositório público vazio no GitHub, que será o ponto de partida do projeto.
- Acesse [github.com](https://github.com), clique em **"+"** (canto superior direito) e vá em **"New repository"**.
- Preencha os campos:
  - **Owner:** selecione sua conta pessoal do GitHub.
  - **Repository name:** `meu-repositorio`
  - **Visibility:** Public
  - **Initialize this repository with a README:** marque esta opção.
- Clique em **"Create repository"**.

O GitHub criará o repositório com um arquivo `README.md` inicial.

### 2. Clonar o repositório para sua máquina
Traga o repositório remoto para o seu computador, criando uma cópia local com todo o histórico.
- Na página do seu repositório, clique em **"Code"** e copie a URL HTTPS.
- No terminal do seu computador, execute:

```bash
git clone https://github.com/SEU_USUARIO/meu-repositorio.git
cd meu-repositorio
```
Verifique o histórico inicial:
```bash
git log --oneline
```

### 3. Fazer o primeiro commit
Abra o arquivo `README.md` em qualquer editor de texto e adicione uma linha descrevendo o repositório. Salve o arquivo.

Verifique o que mudou:
```bash
git status
```

Prepare a alteração e faça o commit:
```bash
git add README.md
git commit -m "docs: descreve o repositório no README"
```

### 4. Criar uma branch de funcionalidade
Antes de qualquer nova tarefa, crie uma branch separada. Isso mantém a `main` estável.
```bash
git checkout -b feature/adiciona-gitignore
```

Crie um arquivo `.gitignore` para proteger arquivos sensíveis e temporários:
```bash
cat > .gitignore << 'EOF'
__pycache__/
.env
*.pyc
.venv/
EOF
```

Faça o commit do `.gitignore` na nova branch:
```bash
git add .gitignore
git commit -m "chore: adiciona .gitignore"
```

### 5. Dar push da branch para o GitHub
Envie a branch para o repositório remoto para que ela fique visível no GitHub:
```bash
git push -u origin feature/adiciona-gitignore
```
*💡 Ponto de reflexão: o comando `git push -u origin <branch>` configura o rastreamento entre a branch local e a remota. Nas próximas vezes, basta digitar `git push`.*

> **Nota:** Não abra o Pull Request ainda, isso será feito no Lab 2.

---

## ✅ Checklist Rápido de Comandos

```bash
# 1. Clonar o repositório
git clone https://github.com/SEU_USUARIO/meu-repositorio.git
cd meu-repositorio

# 2. Verificar histórico
git log --oneline

# 3. Primeiro commit
git add README.md
git commit -m "docs: descreve o repositório no README"

# 4. Criar branch
git checkout -b feature/adiciona-gitignore

# 5. Commit na branch
git add .gitignore
git commit -m "chore: adiciona .gitignore"

# 6. Enviar branch ao GitHub
git push -u origin feature/adiciona-gitignore
```
