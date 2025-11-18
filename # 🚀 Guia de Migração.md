# 🚀 Guia de Migração - GitHub para GitLab SpecialDog

<div align="center">

![GitLab](https://img.shields.io/badge/GitLab-FC6D26?style=for-the-badge&logo=gitlab&logoColor=white)
![Status](https://img.shields.io/badge/Status-Ativo-success?style=for-the-badge)

**SpecialDog Company - Departamento de TI**

---

</div>

## 📢 Comunicado Importante

Realizamos a **migração do nosso servidor de repositórios Git** para uma nova infraestrutura GitLab mais robusta e atualizada. 

**A partir de agora:**
- ✅ **Usaremos:** GitLab SpecialDog (`gitlab.manfrim.com.br`)
- ❌ **Descontinuado:** GitHub (não será mais utilizado)

---

## 🎯 Ações Necessárias

### ⚠️ IMPORTANTE - Verifique Seus Projetos

1. **Acesse:** https://gitlab.manfrim.com.br
2. **Faça login** com suas credenciais (veja abaixo)
3. **Verifique se todos os seus projetos estão no novo GitLab**
4. **Caso algum projeto não esteja lá:**
   - Crie o repositório no novo GitLab
   - Faça a migração seguindo os passos deste guia

---

## 🔑 Credenciais de Acesso

**URL do GitLab:** https://gitlab.manfrim.com.br

**Suas credenciais de acesso:**
- **Usuário:** `seu.nome` (exemplo: `leonardo.dalcorso`)
- **Senha temporária:** `123@mudar`

### ⚠️ Primeiro Acesso

1. Faça login com a senha temporária `123@mudar`
2. O sistema irá solicitar que você **altere sua senha**
3. **Escolha uma senha forte** (mínimo 8 caracteres, com letras, números e símbolos)
4. Recomendamos usar um gerenciador de senhas

---

## 🔧 Configuração Inicial

### 1️⃣ Atualizar Configuração Global do Git

Antes de começar, configure seu nome e email no Git (caso ainda não tenha feito):

#### No Windows (PowerShell/CMD):
```bash
git config --global user.name "Seu Nome Completo"
git config --global user.email "seu.email@manfrim.com.br"
```

#### No Mac/Linux (Terminal):
```bash
git config --global user.name "Seu Nome Completo"
git config --global user.email "seu.email@manfrim.com.br"
```

### 2️⃣ Verificar Configurações
```bash
git config --global --list
```

---

## 🔐 Autenticação - Escolha Seu Método

Você pode autenticar no GitLab de duas formas:

### Opção A: HTTPS com Personal Access Token (Recomendado) 🌟

**Vantagens:** Fácil de configurar, funciona em qualquer lugar

#### Passo 1: Criar Token de Acesso

1. Acesse: https://gitlab.manfrim.com.br
2. Clique no seu **avatar** (canto superior direito)
3. Vá em **Preferences** → **Access Tokens**
4. Preencha:
   - **Token name:** `Meu Computador` (ou nome que identifique)
   - **Expiration date:** Escolha uma data futura (ex: 1 ano)
   - **Scopes:** Marque:
     - ✅ `read_repository`
     - ✅ `write_repository`
5. Clique em **"Create personal access token"**
6. **⚠️ COPIE O TOKEN!** (ele só aparece uma vez)

#### Passo 2: Usar o Token

Quando fizer `git clone`, `git push` ou `git pull`, use:

**Usuário:** Seu username do GitLab  
**Senha:** Cole o token que você copiou

**Dica:** O Git vai salvar suas credenciais automaticamente no Windows e Mac.

---

### Opção B: SSH (Para Usuários Avançados) 🔑

**Vantagens:** Mais seguro, não precisa digitar senha

#### Passo 1: Verificar se Já Tem Chave SSH

**Windows (PowerShell):**
```powershell
ls ~\.ssh\
```

**Mac/Linux (Terminal):**
```bash
ls -la ~/.ssh/
```

Se ver arquivos `id_rsa` e `id_rsa.pub` (ou `id_ed25519`), você já tem uma chave!

#### Passo 2: Criar Nova Chave SSH (se não tiver)

**Windows (PowerShell) / Mac / Linux:**
```bash
ssh-keygen -t ed25519 -C "seu.email@manfrim.com.br"
```

Pressione `Enter` três vezes (aceita o local padrão e sem senha)

#### Passo 3: Copiar a Chave Pública

**Windows (PowerShell):**
```powershell
Get-Content ~\.ssh\id_ed25519.pub | clip
```

**Mac:**
```bash
pbcopy < ~/.ssh/id_ed25519.pub
```

**Linux:**
```bash
cat ~/.ssh/id_ed25519.pub
# Copie o conteúdo manualmente
```

#### Passo 4: Adicionar Chave no GitLab

1. Acesse: https://gitlab.manfrim.com.br
2. Clique no seu **avatar** → **Preferences**
3. Vá em **SSH Keys** (menu lateral)
4. Cole a chave no campo **"Key"**
5. Dê um título: `Meu Computador - Windows` (ou Mac/Linux)
6. Clique em **"Add key"**

#### Passo 5: Testar Conexão SSH

```bash
ssh -T git@gitlab.manfrim.com.br
```

Se aparecer `Welcome to GitLab, @seu-usuario!` está funcionando! ✅

---

## 📦 Migração de Projetos Existentes

### Cenário 1: Projeto Que Já Está no Novo GitLab

Se o projeto já foi migrado pela equipe de TI:

```bash
# 1. Entre na pasta do projeto
cd /caminho/do/seu/projeto

# 2. Remover remote antigo (GitHub)
git remote remove origin

# 3. Adicionar novo remote (GitLab)
git remote add origin https://gitlab.manfrim.com.br/seu-usuario/nome-do-projeto.git

# 4. Verificar
git remote -v

# 5. Fazer push
git push -u origin main
```

**⚠️ Nota:** Se sua branch principal se chama `master` em vez de `main`, use `master` nos comandos.

---

### Cenário 2: Projeto Que NÃO Está no GitLab (Precisa Criar)

#### Passo 1: Criar Repositório no GitLab

1. Acesse: https://gitlab.manfrim.com.br
2. Clique no **"+"** (canto superior direito)
3. Clique em **"New project/repository"**
4. Selecione **"Create blank project"**
5. Preencha:
   - **Project name:** Nome do projeto
   - **Visibility Level:** Private (ou conforme necessário)
6. **⚠️ DESMARQUE** "Initialize repository with a README"
7. Clique em **"Create project"**
8. **Copie a URL** que aparece (será algo como: `https://gitlab.manfrim.com.br/seu-usuario/projeto.git`)

#### Passo 2: Migrar o Código

```bash
# 1. Entre na pasta do projeto
cd /caminho/do/seu/projeto

# 2. Verificar remote atual
git remote -v

# 3. Renomear remote antigo (backup)
git remote rename origin github-old

# 4. Adicionar novo remote GitLab
git remote add origin https://gitlab.manfrim.com.br/seu-usuario/nome-do-projeto.git

# 5. Verificar
git remote -v

# 6. Fazer push de todas as branches
git push -u origin --all

# 7. Fazer push de todas as tags
git push -u origin --tags

# 8. Remover remote antigo (opcional)
git remote remove github-old
```

---

### Cenário 3: Clonar Projeto Novo do GitLab

Para começar a trabalhar em um projeto que já está no GitLab:

#### Com HTTPS:
```bash
git clone https://gitlab.manfrim.com.br/usuario/nome-do-projeto.git
cd nome-do-projeto
```

#### Com SSH:
```bash
git clone git@gitlab.manfrim.com.br:usuario/nome-do-projeto.git
cd nome-do-projeto
```

---

## 🔄 Fluxo de Trabalho Diário

Seu fluxo de trabalho continua o mesmo:

```bash
# 1. Atualizar seu código local
git pull origin main

# 2. Criar uma branch para sua feature
git checkout -b minha-feature

# 3. Fazer suas alterações e commits
git add .
git commit -m "Descrição das alterações"

# 4. Enviar para o GitLab
git push origin minha-feature

# 5. Criar Merge Request no GitLab
# Acesse o GitLab e clique no botão "Create merge request"
```

---

## 🛠️ Configuração de IDEs

### Visual Studio Code

1. **Instale a extensão:** GitLab Workflow
2. **Configure:**
   - Abra Command Palette (`Ctrl+Shift+P` ou `Cmd+Shift+P`)
   - Digite: `GitLab: Set GitLab Personal Access Token`
   - Cole seu token do GitLab

### Visual Studio

1. Vá em **Tools** → **Options** → **Source Control** → **Git Global Settings**
2. Configure o remote do projeto para o novo GitLab
3. Use suas credenciais (usuário + token) quando solicitado

### IntelliJ / PyCharm / WebStorm

1. Vá em **File** → **Settings** → **Version Control** → **Git**
2. Configure o remote do projeto
3. Quando solicitar credenciais, use: usuário + token

---

## ❓ Perguntas Frequentes (FAQ)

### 1. Perdi meu token de acesso, e agora?

Crie um novo token seguindo os passos em "Criar Token de Acesso". Você pode ter múltiplos tokens ativos.

### 2. Como sei qual é minha branch principal? `main` ou `master`?

```bash
git branch
# A branch com * é a atual
# Ou veja no GitLab em: Project → Repository → Branches
```

### 3. Esqueci minha senha do GitLab

1. Acesse: https://gitlab.manfrim.com.br
2. Clique em **"Forgot your password?"**
3. Digite seu email `@manfrim.com.br`
4. Siga as instruções do email

### 4. Meu `git push` está pedindo senha o tempo todo

**Windows:** O Git Credential Manager deve salvar automaticamente. Se não estiver funcionando:
```bash
git config --global credential.helper manager
```

**Mac:**
```bash
git config --global credential.helper osxkeychain
```

**Linux:**
```bash
git config --global credential.helper store
```

### 5. Como converter meu projeto de HTTPS para SSH (ou vice-versa)?

**De HTTPS para SSH:**
```bash
git remote set-url origin git@gitlab.manfrim.com.br:usuario/projeto.git
```

**De SSH para HTTPS:**
```bash
git remote set-url origin https://gitlab.manfrim.com.br/usuario/projeto.git
```

### 6. Preciso migrar histórico de Issues e Pull Requests?

Apenas o código é migrado automaticamente. Issues e Pull Requests precisam ser migrados manualmente ou via API. Contate a equipe de TI se precisar migrar histórico completo.

---

## 🆘 Comandos Úteis de Troubleshooting

### Verificar status do repositório
```bash
git status
```

### Ver remotes configurados
```bash
git remote -v
```

### Ver configuração do Git
```bash
git config --list
```

### Limpar credenciais salvas (Windows)
```powershell
cmdkey /list
# Procure por gitlab.manfrim.com.br e delete:
cmdkey /delete:git:https://gitlab.manfrim.com.br
```

### Limpar credenciais salvas (Mac)
```bash
# Abra "Keychain Access" e procure por gitlab.manfrim.com.br
# Ou via terminal:
git credential-osxkeychain erase
# Digite: protocol=https
# Digite: host=gitlab.manfrim.com.br
# Pressione Enter duas vezes
```

### Forçar nova autenticação
```bash
git config --global --unset credential.helper
git pull
# Vai pedir credenciais novamente
git config --global credential.helper manager  # Windows
# ou
git config --global credential.helper osxkeychain  # Mac
```

---

## 📋 Checklist de Migração

Use este checklist para garantir que tudo está configurado:

- [ ] Fiz login no GitLab pela primeira vez
- [ ] Alterei minha senha temporária
- [ ] Configurei meu nome e email no Git
- [ ] Escolhi meu método de autenticação (HTTPS Token ou SSH)
- [ ] Criei meu Personal Access Token (se usar HTTPS) OU
- [ ] Configurei minhas chaves SSH (se usar SSH)
- [ ] Verifiquei que todos os meus projetos estão no GitLab
- [ ] Atualizei os remotes dos meus projetos locais
- [ ] Testei fazer push/pull em pelo menos um projeto
- [ ] Configurei minha IDE favorita para usar o GitLab

---

## 📞 Suporte

### Precisa de Ajuda?

**Equipe de TI - SpecialDog**

📧 **Email:** leonardo.dalcorso@manfrim.com.br  ou joao.takayasu@manfrim.co,.br
📱 **Telefone:** Ramal 3080

**Horário de Atendimento:** Segunda a Sexta, 8h às 18h

---

## 📚 Recursos Adicionais

### Documentação Oficial
- [GitLab User Docs](https://docs.gitlab.com/ee/user/)
- [Git Basics](https://git-scm.com/book/en/v2/Getting-Started-Git-Basics)


---

## 📌 Termo de Uso

Ao utilizar o GitLab SpecialDog, você concorda com nossos [Termos de Uso dos Repositórios](link-para-termo).

**Principais pontos:**
- Todo código é propriedade da SpecialDog Company
- Não compartilhe credenciais ou código fora da empresa
- Use apenas para propósitos autorizados
- Mantenha suas credenciais seguras

---

<div align="center">

## ✅ Migração Concluída com Sucesso!

**Bem-vindo(a) ao GitLab SpecialDog!** 🐕

Agora você está pronto(a) para trabalhar no nosso novo ambiente de desenvolvimento.

Se tiver qualquer dúvida, não hesite em contatar a equipe de TI.

---

**SpecialDog Company**  
*Inovação e Qualidade em Desenvolvimento*

© 2025 - Todos os direitos reservados

</div>
