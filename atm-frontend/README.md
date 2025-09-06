# 🏧 Projeto de um Simulador de ATM para a ByteBank - Frontend

## 📋 Descrição

Este é um desafio de desenvolvimento frontend para criar uma interface de um caixa eletrônico (ATM) utilizando apenas **HTML**, **CSS** e **JavaScript vanilla** (sem frameworks). O sistema deve simular as funcionalidades básicas de um ATM bancário e se conectar com a API backend desenvolvida no projeto [`atm-backend`](../atm-backend/).

## 🎯 Objetivos do Desafio

Desenvolver uma aplicação frontend que simule um caixa eletrônico com as seguintes funcionalidades:

### 1. 🔐 Tela de Login/Entrada
- Criar formulário de autenticação com duas opções:
  - **Opção 1**: Conta Corrente + Senha
  - **Opção 2**: CPF + Senha
- Validação dos campos obrigatórios
- Integração com API de autenticação do backend
- Tratamento de erros de login
- Interface responsiva e intuitiva

### 2. 🏠 Menu Principal
Após o login bem-sucedido, apresentar menu com as opções:
- 💰 Consultar Saldo
- 📄 Extrato
- 💸 Saque
- 💳 Depósito
- 🚪 Sair

### 3. 💰 Tela de Saldo
- Exibir saldo atual da conta
- Botão para voltar ao menu principal
- Animação de carregamento durante consulta

### 4. 📄 Tela de Extrato
- Listar últimas transações
- Mostrar data, tipo de operação e valor
- Filtro por período (opcional)
- Paginação para muitas transações

### 5. 💸 Tela de Saque
- Campo para inserir valor do saque
- Validação de valor mínimo/máximo
- Verificação de saldo suficiente
- Simulação de contagem de notas
- Confirmação da operação

### 6. 💳 Tela de Depósito
- Campo para inserir valor do depósito
- Validação de valor mínimo
- Confirmação da operação
- Atualização do saldo

### 7. 🚪 Tela de Saída/Logout
- Confirmação antes de sair
- Limpeza de dados da sessão
- Redirecionamento para tela de login

## 🛠️ Tecnologias Utilizadas

- **HTML5**: Estrutura semântica das páginas
- **CSS3**: Estilização e responsividade
  - Flexbox/Grid para layout
  - Media queries para responsividade
  - Animações e transições
- **JavaScript ES6+**: Lógica da aplicação
  - Fetch API para requisições HTTP
  - Local Storage para sessão
  - Manipulação do DOM
  - Async/Await para operações assíncronas

## 📁 Estrutura de Arquivos Sugerida

```
atm-frontend/
├── index.html
├── css/
│   ├── style.css
│   ├── login.css
│   ├── menu.css
│   └── components.css
├── js/
│   ├── app.js
│   ├── auth.js
│   ├── api.js
│   ├── components.js
│   └── utils.js
├── assets/
│   ├── images/
│   └── icons/
└── README.md
```

## 🔧 Configuração e Execução

### Pré-requisitos
- Navegador web moderno
- Servidor HTTP local (pode usar Live Server do VS Code)
- Backend ATM rodando (consulte [`atm-backend`](../atm-backend/))

### Como executar
1. Clone o repositório
2. Navegue até a pasta `atm-frontend`
3. Abra com Live Server ou servidor HTTP de sua preferência
4. Acesse `http://localhost:5500` (ou porta configurada)

## 🌐 Integração com Backend

### Endpoints da API
A aplicação deve se conectar com os seguintes endpoints do backend:

```javascript
// Configuração base da API
const API_BASE_URL = 'http://localhost:3000/api';

// Endpoints
POST /auth/login        // Autenticação
GET  /account/balance   // Consultar saldo
GET  /account/statement // Extrato
POST /transaction/withdraw  // Saque
POST /transaction/deposit   // Depósito
POST /auth/logout       // Logout
```

### Exemplo de Requisição
```javascript
// Exemplo de login
const login = async (credentials) => {
  try {
    const response = await fetch(`${API_BASE_URL}/auth/login`, {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
      },
      body: JSON.stringify(credentials)
    });
    
    if (!response.ok) throw new Error('Erro na autenticação');
    
    const data = await response.json();
    localStorage.setItem('token', data.token);
    return data;
  } catch (error) {
    console.error('Erro:', error);
    throw error;
  }
};
```

## 🎨 Requisitos de Design

### Interface do Usuário
- **Design responsivo** para desktop e mobile
- **Tema escuro/claro** do caixa eletrônico
- **Animações suaves** entre telas
- **Feedback visual** para ações do usuário
- **Loading states** durante requisições
- **Tratamento de erros** com mensagens claras

### Acessibilidade
- Navegação por teclado
- Textos alternativos para imagens
- Contraste adequado de cores
- Tamanhos de fonte legíveis

## ✅ Critérios de Avaliação

### Funcionalidade (40%)
- [ ] Login funcional com validação
- [ ] Todas as operações do ATM implementadas
- [ ] Integração completa com backend
- [ ] Tratamento adequado de erros
- [ ] Logout seguro

### Código (30%)
- [ ] HTML semântico e bem estruturado
- [ ] CSS organizado e reutilizável
- [ ] JavaScript modular e limpo
- [ ] Boas práticas de desenvolvimento
- [ ] Comentários quando necessário

### Interface (20%)
- [ ] Design intuitivo e profissional
- [ ] Responsividade em diferentes telas
- [ ] Animações e transições apropriadas
- [ ] Feedback visual adequado
- [ ] Experiência do usuário fluida

### Extras (10%)
- [ ] Implementação de recursos adicionais
- [ ] Otimizações de performance
- [ ] Testes unitários
- [ ] Documentação detalhada
- [ ] Deploy funcional

## 🚀 Funcionalidades Extras (Opcionais)

- 🔔 Notificações toast para operações
- 📱 PWA (Progressive Web App)
- 🎯 Teclado virtual numérico
- 🔒 Timeout de sessão por inatividade
- 📊 Gráficos de gastos mensais
- 🌙 Modo escuro/claro
- 🔊 Feedback sonoro para operações
- 📝 Histórico detalhado de transações

## 📚 Recursos de Aprendizado

### Conceitos Importantes
- **Fetch API** para requisições HTTP
- **LocalStorage** para persistência de dados
- **Event Listeners** para interações
- **Promises/Async-Await** para operações assíncronas
- **DOM Manipulation** para atualização da interface
- **CSS Grid/Flexbox** para layouts responsivos

### Dicas de Implementação
1. Comece com a estrutura HTML básica
2. Implemente o CSS mobile-first
3. Desenvolva as funcionalidades uma por vez
4. Teste cada funcionalidade antes de prosseguir
5. Mantenha o código organizado e comentado

## 🤝 Contribuição

Este é um projeto de desafio individual, mas sinta-se à vontade para:
- Melhorar a documentação
- Sugerir novas funcionalidades
- Reportar bugs encontrados
- Compartilhar soluções criativas

## 📄 Licença

Este projeto é de uso educacional e está disponível sob licença MIT.

---

**Boa sorte com o desafio! 🚀**

> Lembre-se: O objetivo é demonstrar conhecimento em tecnologias frontend básicas, integração com APIs e criação de interfaces intuitivas. Foque na qualidade do código e na experiência do usuário!