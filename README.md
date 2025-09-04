# 📘 Checklist de Offboarding IAM

## 🔐 Sobre o projeto
Este é um **aplicativo web simples para checklist de offboarding em IAM**.  
O objetivo é permitir o cadastro de colaboradores em processo de desligamento e acompanhar os itens críticos do offboarding, como revogação de acessos e recuperação de ativos.

Tecnologias utilizadas:
- **HTML + TailwindCSS** (interface)
- **Firebase Firestore** (armazenamento de dados em tempo real)
- **Firebase Authentication** (login anônimo para sessão)
- **GitHub Pages** (deploy do app)

---

## 🚀 Como rodar localmente
1. Baixe o código:
   ```bash
   git clone https://github.com/SEU_USUARIO/offboarding-iam.git
   cd offboarding-iam
   ```

2. Abra o projeto no **VS Code**:
   ```bash
   code .
   ```

3. Clique duas vezes em `index.html` e abra no navegador para testar localmente.  
   (Lembre-se: sem configurar o Firebase, o app não listará colaboradores).

---

## 🔧 Configuração do Firebase

### 1. Criar projeto no Firebase
- Acesse [console.firebase.google.com](https://console.firebase.google.com/).  
- Clique em **Adicionar projeto**.  
- Defina um nome (ex: `offboarding-iam`).  
- Ative o **Firestore Database** (modo de teste para começar).  

### 2. Registrar app web
- No menu do projeto, vá em **Configurações do Projeto > Suas Apps > Adicionar app > Web**.  
- Copie a configuração do **SDK Web** (vai parecer algo assim):

```js
const firebaseConfig = {
  apiKey: "AIza....",
  authDomain: "offboarding-iam.firebaseapp.com",
  projectId: "offboarding-iam",
  storageBucket: "offboarding-iam.appspot.com",
  messagingSenderId: "1234567890",
  appId: "1:1234567890:web:abcdef123456"
};
```

### 3. Editar o código
No arquivo `index.html`, procure este trecho:

```js
const appId = typeof __app_id !== 'undefined' ? __app_id : 'default-app-id';
const firebaseConfig = JSON.parse(typeof __firebase_config !== 'undefined' ? __firebase_config : '{}');
```

👉 Substitua por:

```js
const appId = "offboarding-iam"; // nome fixo ou do seu projeto
const firebaseConfig = {
  apiKey: "SUA_API_KEY",
  authDomain: "SEU_PROJETO.firebaseapp.com",
  projectId: "SEU_PROJETO",
  storageBucket: "SEU_PROJETO.appspot.com",
  messagingSenderId: "1234567890",
  appId: "1:1234567890:web:abcdef123456"
};
```

---

## 🌐 Publicação no GitHub Pages
1. Crie um repositório no GitHub: `offboarding-iam`.  
2. No VS Code:
   ```bash
   git init
   git branch -M main
   git add .
   git commit -m "Primeira versão"
   git remote add origin https://github.com/SEU_USUARIO/offboarding-iam.git
   git push -u origin main
   ```
3. Vá em **Settings > Pages > Source** e escolha:
   - Branch: `main`  
   - Pasta: `/ (root)`  

O app ficará disponível em:  
👉 `https://SEU_USUARIO.github.io/offboarding-iam`

---

## ✅ Checklist de Offboarding no App
- Desativar contas no AD/LDAP  
- Revogar acessos a SaaS (e-mail, VPN, ERP, CRM)  
- Remover MFA, tokens e apps autenticadores  
- Recuperar ativos (notebooks, crachás, tokens físicos)  
- Registrar logs e evidências para auditoria  

---

## 🔒 Boas práticas de IAM
- Nunca exponha **API keys privadas** em repositórios públicos.  
- Se for usar em produção, configure **regras de segurança do Firestore**.  
- Considere autenticação mais robusta (ex: SSO, integração com IdP).  
