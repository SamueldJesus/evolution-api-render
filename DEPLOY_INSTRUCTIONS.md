# 🚀 Evolution API - Deploy no Render.com

## ✅ Modificações Realizadas

O Evolution API foi modificado com sucesso para ser compatível com o Render.com:

### 📝 Alteração Principal
- **Arquivo**: `src/config/env.config.ts`
- **Linha 450**: Modificação da configuração da porta para suportar variável `PORT` dinâmica
- **Antes**: `PORT: Number.parseInt(process.env.SERVER_PORT) || 8080,`
- **Depois**: `PORT: Number.parseInt(process.env.PORT || process.env.SERVER_PORT) || 8080,`

### 🎯 Como Funciona
1. **Render.com**: Usa automaticamente a variável `PORT` definida pelo Render
2. **Desenvolvimento Local**: Continua usando `SERVER_PORT` ou porta `8080`
3. **Fallback**: Se nenhuma variável estiver definida, usa porta `8080`

## 📋 Instruções para Upload no GitHub

### Passo 1: Criar Repositório
1. Vá para [GitHub.com](https://github.com)
2. Clique em "New repository"
3. Nome: `evolution-api-render`
4. Descrição: `Evolution API modificado para deploy no Render.com com configuração de porta dinâmica`
5. Marque como **Private**
6. NÃO inicialize com README (já temos código)
7. Clique em "Create repository"

### Passo 2: Conectar e Fazer Push
Execute estes comandos no terminal na pasta do projeto:

```bash
# Navegar para a pasta do projeto
cd /home/samueldjesus/evolution-api

# Adicionar o remote do seu repositório (substitua SEU_USUARIO)
git remote add origin https://github.com/SEU_USUARIO/evolution-api-render.git

# Fazer push para o GitHub
git push -u origin main
```

### Passo 3: Deploy no Render.com
1. Vá para [Render.com](https://render.com)
2. Conecte sua conta do GitHub
3. Clique em "New" → "Web Service"
4. Conecte seu repositório `evolution-api-render`
5. Configure:
   - **Name**: evolution-api
   - **Environment**: Node
   - **Build Command**: `npm install`
   - **Start Command**: `npm start`
6. Clique em "Create Web Service"

## 🛠️ Variáveis de Ambiente no Render

No Render, você pode definir as seguintes variáveis de ambiente:

```env
# Banco de dados (se necessário)
DATABASE_CONNECTION_URI=sua_string_de_conexao

# Outras configurações específicas
SERVER_NAME=evolution
CORS_ORIGIN=*
# etc...
```

## ✅ Verificação

Após o deploy, teste se está funcionando:
1. Acesse a URL fornecida pelo Render
2. Verifique se a API responde corretamente
3. Confirme que não há erros de porta

## 📞 Suporte

Se encontrar problemas:
1. Verifique os logs no painel do Render
2. Confirme se todas as variáveis de ambiente estão definidas
3. Teste localmente primeiro com `npm start`

---
**Modificado em**: 16/12/2025
**Status**: Pronto para deploy no Render.com
