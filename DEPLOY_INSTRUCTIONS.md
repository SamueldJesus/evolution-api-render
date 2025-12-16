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

## 📋 Instruções para Deploy no Render.com

### Passo 1: Criar Banco de Dados PostgreSQL no Render
**IMPORTANTE**: Você deve criar um banco PostgreSQL ANTES do Web Service.

1. No Render Dashboard, clique em "New" → "PostgreSQL"
2. Configure:
   - **Name**: evolution-api-db
   - **Database**: evolution_db
   - **User**: evolution (ou outro nome)
   - **Password**: [defina uma senha segura]
3. Clique em "Create Database"
4. **ANOTE A CONNECTION STRING** (ex: `postgresql://user:pass@host:port/db`)

### Passo 2: Deploy no Render.com
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

### Passo 3: Configurar Variáveis de Ambiente

**No painel do seu Web Service, vá para "Environment" e configure:**

#### Configurações Obrigatórias:
```env
# BANCO DE DADOS (use a connection string do banco que você criou)
DATABASE_PROVIDER=postgresql
DATABASE_CONNECTION_URI=postgresql://evolution:[SUA_SENHA]@[HOST]:5432/evolution_db?schema=evolution_api
DATABASE_CONNECTION_CLIENT_NAME=evolution_exchange

# CONFIGURAÇÕES BÁSICAS
SERVER_NAME=evolution
CORS_ORIGIN=*

# CACHE (usar cache local para simplicidade)
CACHE_REDIS_ENABLED=false
CACHE_LOCAL_ENABLED=true

# AUTENTICAÇÃO
AUTHENTICATION_API_KEY=429683C4C977415CAAFCCE10F7D57E11
AUTHENTICATION_EXPOSE_IN_FETCH_INSTANCES=true

# DESABILITAR INTEGRAÇÕES DESNECESSÁRIAS
RABBITMQ_ENABLED=false
WEBSOCKET_ENABLED=false
PUSHER_ENABLED=false
KAFKA_ENABLED=false
SQS_ENABLED=false
NATS_ENABLED=false
TYPEBOT_ENABLED=false
CHATWOOT_ENABLED=false
OPENAI_ENABLED=false
DIFY_ENABLED=false
N8N_ENABLED=false
EVOAI_ENABLED=false
FLOWISE_ENABLED=false

# LOGS (reduzir para produção)
LOG_LEVEL=ERROR,WARN,INFO
LOG_COLOR=false
TELEMETRY_ENABLED=false
```

#### Configurações Adicionais (Opcional):
```env
# IDIOMA
LANGUAGE=pt

# CONFIGURAÇÕES DE WHATSAPP
CONFIG_SESSION_PHONE_CLIENT=Evolution API
CONFIG_SESSION_PHONE_NAME=Chrome
QRCODE_LIMIT=30

# CONFIGURAÇÕES DE SALVAMENTO
DATABASE_SAVE_DATA_INSTANCE=true
DATABASE_SAVE_DATA_NEW_MESSAGE=true
DATABASE_SAVE_MESSAGE_UPDATE=true
DATABASE_SAVE_DATA_CONTACTS=true
DATABASE_SAVE_DATA_CHATS=true
DATABASE_SAVE_DATA_LABELS=true
DATABASE_SAVE_DATA_HISTORIC=true
DATABASE_SAVE_IS_ON_WHATSAPP=true
DATABASE_SAVE_IS_ON_WHATSAPP_DAYS=7
DATABASE_DELETE_MESSAGE=true

# CONFIGURAÇÕES GERAIS
DEL_INSTANCE=false
EVENT_EMITTER_MAX_LISTENERS=50
```

### Passo 4: Deploy e Verificação

1. **Deploy**: Clique em "Create" e aguarde o deploy completar
2. **Teste**: Acesse a URL fornecida pelo Render (ex: `https://evolution-api.onrender.com`)
3. **Verifique**: Teste se a API responde em `/health` ou `/status`

## 🚨 Solução para Erro "Database provider invalid"

Se você receber o erro `Database provider invalid`, certifique-se de:

1. ✅ **Configurar `DATABASE_PROVIDER=postgresql`** (exatamente assim, minúsculas)
2. ✅ **Fornecer `DATABASE_CONNECTION_URI`** válida
3. ✅ **Criar o banco PostgreSQL primeiro** no Render
4. ✅ **Aguardar o banco estar ativo** antes de fazer deploy do Web Service

## 📁 Arquivos de Referência

- **`.env.render`**: Arquivo com todas as configurações comentadas
- **`src/config/env.config.ts`**: Código modificado para porta dinâmica

## 📞 Suporte

Se encontrar problemas:

1. **Erro "Database provider invalid"**:
   - Verifique se `DATABASE_PROVIDER=postgresql` está definido
   - Confirme se o banco PostgreSQL está ativo
   - Valide a `DATABASE_CONNECTION_URI`

2. **Erro de porta**:
   - O código já está configurado para usar `PORT` automaticamente
   - Não defina `SERVER_PORT` manualmente no Render

3. **Verificar logs**:
   - No painel do Render, vá em "Logs" para ver erros
   - Confirme se todas as variáveis de ambiente estão definidas

---
**Modificado em**: 16/12/2025
**Status**: Pronto para deploy no Render.com com solução para erro de banco
