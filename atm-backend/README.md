# 🏧 Projeto de um Simulador de ATM para a ByteBank - Backend API

## 📋 Descrição

Este é um desafio de desenvolvimento backend para criar uma API REST de um caixa eletrônico (ATM) utilizando **Node.js vanilla** (sem frameworks). A API deve fornecer todos os endpoints necessários para integração com o frontend do projeto [`atm-frontend`](../atm-frontend/).

## 🎯 Objetivos do Desafio

Desenvolver uma API REST que simule as operações de um caixa eletrônico com as seguintes funcionalidades:

### 1. 🔐 Sistema de Autenticação
- **POST** `/api/auth/login` - Login com conta corrente/CPF + senha
- **POST** `/api/auth/logout` - Logout e invalidação de sessão
- **GET** `/api/auth/validate` - Validação de token de sessão

### 2. 💰 Gerenciamento de Conta
- **GET** `/api/account/balance` - Consultar saldo atual
- **GET** `/api/account/info` - Informações da conta

### 3. 📄 Extrato e Transações
- **GET** `/api/account/statement` - Extrato de transações
- **GET** `/api/account/statement/:period` - Extrato por período

### 4. 💸 Operações Bancárias
- **POST** `/api/transaction/withdraw` - Realizar saque
- **POST** `/api/transaction/deposit` - Realizar depósito
- **GET** `/api/transaction/history` - Histórico de transações

## 🛠️ Tecnologias Utilizadas

- **Node.js**: Runtime JavaScript
- **Módulos Nativos**:
  - `http` - Servidor HTTP
  - `url` - Manipulação de URLs
  - `crypto` - Criptografia e hashing
  - `fs` - Sistema de arquivos (para persistência simples)
  - `path` - Manipulação de caminhos
- **JSON** - Armazenamento de dados (simulando banco de dados)

## 📁 Estrutura de Arquivos Sugerida

```
atm-backend/
├── server.js              # Servidor principal
├── routes/
│   ├── auth.js            # Rotas de autenticação
│   ├── account.js         # Rotas de conta
│   └── transaction.js     # Rotas de transações
├── middleware/
│   ├── auth.js            # Middleware de autenticação
│   ├── cors.js            # Middleware de CORS
│   └── validation.js      # Middleware de validação
├── services/
│   ├── authService.js     # Lógica de autenticação
│   ├── accountService.js  # Lógica de conta
│   └── transactionService.js # Lógica de transações
├── utils/
│   ├── database.js        # Simulação de banco de dados
│   ├── validators.js      # Validadores
│   └── helpers.js         # Funções auxiliares
├── data/
│   ├── users.json         # Dados dos usuários
│   ├── accounts.json      # Dados das contas
│   └── transactions.json  # Dados das transações
├── config/
│   └── config.js          # Configurações da aplicação
└── README.md
```

## 🔧 Configuração e Execução

### Pré-requisitos
- Node.js (versão 20 ou superior)
- npm

### Como executar
1. Clone o repositório
2. Navegue até a pasta `atm-backend`
3. Execute `npm init -y` (se necessário)
4. Execute `node server.js`
5. A API estará disponível em `http://localhost:3000`

### Variáveis de Ambiente
Crie um arquivo `.env` ou configure diretamente no código:

```javascript
const CONFIG = {
  PORT: process.env.PORT || 3000,
  JWT_SECRET: process.env.JWT_SECRET || 'atm-secret-key-2025',
  SESSION_TIMEOUT: 30 * 60 * 1000, // 30 minutos
  MAX_WITHDRAW: 1000.00,
  MIN_WITHDRAW: 10.00,
  MIN_DEPOSIT: 1.00
};
```

## 🌐 Documentação da API

### 🔐 Autenticação

#### POST `/api/auth/login`
Autentica o usuário com CPF.
**Request Body:**
```json
{
    "cpf": "123.456.789-00",
    "password": "1234"
}
```
```

**Response Success (200):**
```json
{
  "success": true,
  "message": "Login realizado com sucesso",
  "data": {
    "token": "jwt-token-here",
    "user": {
      "id": "user-id",
      "name": "João Silva",
      "account": "12345-6"
    }
  }
}
```

**Response Error (401):**
```json
{
  "success": false,
  "message": "Credenciais inválidas",
  "error": "INVALID_CREDENTIALS"
}
```

#### POST `/api/auth/logout`
Realiza logout e invalida o token.

**Headers:**
```
Authorization: Bearer jwt-token-here
```

**Response (200):**
```json
{
  "success": true,
  "message": "Logout realizado com sucesso"
}
```

### 💰 Conta

#### GET `/api/account/balance`
Consulta o saldo atual da conta.

**Headers:**
```
Authorization: Bearer jwt-token-here
```

**Response (200):**
```json
{
  "success": true,
  "data": {
    "balance": 1500.75,
    "account": "12345-6",
    "lastUpdate": "2025-07-31T10:30:00Z"
  }
}
```

#### GET `/api/account/info`
Retorna informações da conta.

**Headers:**
```
Authorization: Bearer jwt-token-here
```

**Response (200):**
```json
{
    "success": true,
    "data": {
        "account": "12345-6",
        "name": "João Silva",
        "cpf": "123.456.789-00",
        "type": "Conta Corrente",
        "agency": "0001"
    }
}
```

### 📄 Extrato

#### GET `/api/account/statement`
Retorna o extrato das últimas transações.

**Query Parameters:**
- `limit` (opcional): Número de transações (padrão: 10)
- `page` (opcional): Página para paginação (padrão: 1)

**Response (200):**
```json
{
  "success": true,
  "data": {
    "transactions": [
      {
        "id": "txn-001",
        "type": "withdraw",
        "amount": 100.00,
        "date": "2025-07-31T09:15:00Z",
        "description": "Saque em Caixa Eletrônico"
      },
      {
        "id": "txn-002",
        "type": "deposit",
        "amount": 500.00,
        "date": "2025-07-30T14:20:00Z",
        "description": "Depósito em Conta"
      }
    ],
    "pagination": {
      "currentPage": 1,
      "totalPages": 3,
      "totalItems": 25
    }
  }
}
```

### 💸 Transações

#### POST `/api/transaction/withdraw`
Realiza um saque.

**Request Body:**
```json
{
  "amount": 100.00,
  "password": "1234"
}
```

**Response Success (200):**
```json
{
  "success": true,
  "message": "Saque realizado com sucesso",
  "data": {
    "transactionId": "txn-003",
    "amount": 100.00,
    "newBalance": 1400.75,
    "notes": {
      "50": 2,
      "0": 0
    },
    "timestamp": "2025-07-31T11:00:00Z"
  }
}
```

**Response Error (400):**
```json
{
  "success": false,
  "message": "Saldo insuficiente",
  "error": "INSUFFICIENT_FUNDS"
}
```

#### POST `/api/transaction/deposit`
Realiza um depósito.

**Request Body:**
```json
{
  "amount": 200.00
}
```

**Response (200):**
```json
{
  "success": true,
  "message": "Depósito realizado com sucesso",
  "data": {
    "transactionId": "txn-004",
    "amount": 200.00,
    "newBalance": 1700.75,
    "timestamp": "2025-07-31T11:05:00Z"
  }
}
```

## 💾 Estrutura de Dados

### Usuários (users.json)
```json
[
  {
    "id": "user-001",
    "name": "João Silva",
    "cpf": "123.456.789-00",
    "account": "12345-6",
    "agency": "0001",
    "password": "hashed-password",
    "active": true,
    "createdAt": "2025-01-01T00:00:00Z"
  }
]
```

### Contas (accounts.json)
```json
[
  {
    "id": "acc-001",
    "userId": "user-001",
    "account": "12345-6",
    "agency": "0001",
    "balance": 1500.75,
    "type": "corrente",
    "status": "active"
  }
]
```

### Transações (transactions.json)
```json
[
  {
    "id": "txn-001",
    "accountId": "acc-001",
    "type": "withdraw",
    "amount": 100.00,
    "balanceBefore": 1600.75,
    "balanceAfter": 1500.75,
    "timestamp": "2025-07-31T09:15:00Z",
    "description": "Saque em Caixa Eletrônico"
  }
]
```

## 🛡️ Segurança

### Implementações Obrigatórias
- **Hash de senhas** com crypto nativo
- **JWT tokens** para autenticação
- **Rate limiting** para login
- **Validação de entrada** rigorosa
- **CORS** configurado adequadamente
- **Timeout de sessão** automático

### Exemplo de Hash de Senha
```javascript
const crypto = require('crypto');

function hashPassword(password, salt) {
  return crypto.pbkdf2Sync(password, salt, 1000, 64, 'sha512').toString('hex');
}

function generateSalt() {
  return crypto.randomBytes(16).toString('hex');
}
```

## ✅ Critérios de Avaliação

### Funcionalidade (40%)
- [ ] Todos os endpoints implementados
- [ ] Autenticação JWT funcional
- [ ] Operações bancárias corretas
- [ ] Tratamento de erros adequado
- [ ] Validação de dados de entrada

### Código (30%)
- [ ] Estrutura modular e organizada
- [ ] Código limpo e legível
- [ ] Boas práticas de Node.js
- [ ] Comentários quando necessário
- [ ] Tratamento de exceções

### Segurança (20%)
- [ ] Senhas hasheadas
- [ ] Tokens JWT seguros
- [ ] Validação de entrada
- [ ] Rate limiting implementado
- [ ] CORS configurado

### Integração (10%)
- [ ] Comunicação perfeita com frontend
- [ ] Headers HTTP corretos
- [ ] Formato de resposta consistente
- [ ] Códigos de status apropriados

## 🚀 Funcionalidades Extras (Opcionais)

- 📊 **Logging** detalhado de operações
- 🔄 **Rate limiting** por IP/usuário
- 📧 **Notificações** de transações
- 💳 **Múltiplas contas** por usuário
- 🏦 **Simulação de diferentes bancos**
- 📈 **Relatórios** de uso da API
- 🔐 **2FA** (Two-Factor Authentication)
- 📱 **Webhook** para notificações

## 📚 Conceitos Importantes

### Node.js Vanilla
- Módulo `http` para servidor
- Módulo `url` para roteamento
- Módulo `crypto` para segurança
- Módulo `fs` para persistência
- Stream e Buffer handling

### Padrões de API REST
- Status codes apropriados
- Estrutura de resposta consistente
- Versionamento de API
- Documentação clara

## 🎯 Exemplo de Implementação Básica

### Servidor Principal (server.js)
```javascript
const http = require('http');
const url = require('url');
const authRoutes = require('./routes/auth');
const accountRoutes = require('./routes/account');
const transactionRoutes = require('./routes/transaction');
const corsMiddleware = require('./middleware/cors');

const PORT = 3000;

const server = http.createServer((req, res) => {
  corsMiddleware(req, res);
  
  const parsedUrl = url.parse(req.url, true);
  const path = parsedUrl.pathname;
  const method = req.method;

  // Roteamento simples
  if (path.startsWith('/api/auth')) {
    authRoutes(req, res, path, method);
  } else if (path.startsWith('/api/account')) {
    accountRoutes(req, res, path, method);
  } else if (path.startsWith('/api/transaction')) {
    transactionRoutes(req, res, path, method);
  } else {
    res.writeHead(404, { 'Content-Type': 'application/json' });
    res.end(JSON.stringify({ success: false, message: 'Endpoint não encontrado' }));
  }
});

server.listen(PORT, () => {
  console.log(`🏧 ATM API rodando em http://localhost:${PORT}`);
});
```

## 🤝 Contribuição

Este é um projeto de desafio individual, mas sinta-se à vontade para:
- Melhorar a documentação da API
- Adicionar novos endpoints
- Otimizar performance
- Implementar testes

## 📄 Licença

Este projeto é de uso educacional e está disponível sob licença MIT.

---

**Boa sorte com o desafio! 🚀**

> Lembre-se: O objetivo é demonstrar conhecimento em Node.js vanilla, criação de APIs REST, autenticação JWT e integração com frontend. Foque na qualidade do código e na segurança das operações bancárias!