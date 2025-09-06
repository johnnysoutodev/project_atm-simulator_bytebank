# Documentação da API - Simulador de ATM da ByteBank

## Visão Geral
Este documento fornece informações abrangentes sobre os endpoints da API disponíveis no sistema Simulador de ATM ByteBank.

## URL Base
```
http://localhost:8080/api
```

## Autenticação
Todos os endpoints da API requerem autenticação adequada. Inclua o seguinte cabeçalho em suas requisições:
```
Authorization: Bearer <seu-token>
```

## Endpoints

### Gerenciamento de Contas

#### GET /accounts
Recuperar todas as contas
- **Método:** GET
- **URL:** `/accounts`
- **Resposta:** Array de objetos de conta
- **Códigos de Status:**
    - 200: Sucesso
    - 401: Não autorizado

#### GET /accounts/{id}
Recuperar conta específica por ID
- **Método:** GET
- **URL:** `/accounts/{id}`
- **Parâmetros:**
    - `id` (caminho): ID da conta
- **Resposta:** Objeto da conta
- **Códigos de Status:**
    - 200: Sucesso
    - 404: Conta não encontrada
    - 401: Não autorizado

#### POST /accounts
Criar nova conta
- **Método:** POST
- **URL:** `/accounts`
- **Corpo da Requisição:**
```json
{
    "accountNumber": "string",
    "holderName": "string",
    "initialBalance": "number"
}
```
- **Resposta:** Objeto da conta criada
- **Códigos de Status:**
    - 201: Criado
    - 400: Requisição inválida
    - 401: Não autorizado

### Transações

#### POST /transactions/deposit
Realizar um depósito
- **Método:** POST
- **URL:** `/transactions/deposit`
- **Corpo da Requisição:**
```json
{
    "accountId": "string",
    "amount": "number"
}
```
- **Resposta:** Confirmação da transação
- **Códigos de Status:**
    - 200: Sucesso
    - 400: Valor inválido
    - 404: Conta não encontrada

#### POST /transactions/withdraw
Realizar um saque
- **Método:** POST
- **URL:** `/transactions/withdraw`
- **Corpo da Requisição:**
```json
{
    "accountId": "string",
    "amount": "number"
}
```
- **Resposta:** Confirmação da transação
- **Códigos de Status:**
    - 200: Sucesso
    - 400: Saldo insuficiente ou valor inválido
    - 404: Conta não encontrada

#### GET /transactions/history/{accountId}
Obter histórico de transações
- **Método:** GET
- **URL:** `/transactions/history/{accountId}`
- **Parâmetros:**
    - `accountId` (caminho): ID da conta
- **Resposta:** Array de objetos de transação
- **Códigos de Status:**
    - 200: Sucesso
    - 404: Conta não encontrada

## Respostas de Erro
Todas as respostas de erro seguem este formato:
```json
{
    "error": "Mensagem de erro",
    "code": "CODIGO_DO_ERRO",
    "timestamp": "2023-01-01T00:00:00Z"
}
```

## Limitação de Taxa
As requisições da API são limitadas a 100 requisições por minuto por endereço IP.

## Contato
Para suporte da API, entre em contato com a equipe de desenvolvimento.
