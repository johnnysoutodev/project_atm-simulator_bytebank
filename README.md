# 🏧 Projeto de um Simulador de ATM para a ByteBank

Um sistema completo de ATM desenvolvido com tecnologias nativas de JavaScript para a web.

## 📋 Sobre o Projeto

Este é um projeto de desafio que simula um caixa eletrônico bancário, composto por:

- **Frontend**: Interface web em HTML, CSS e JavaScript vanilla
- **Backend**: API REST em Node.js vanilla (sem frameworks)

## 🚀 Início Rápido

### Pré-requisitos
- Node.js 16+ instalado
- Navegador web moderno
- Git

### Executar o Projeto Completo

```bash
# 1. Clone o repositório
git clone https://github.com/johnnysoutodev/project_atm-simulador_bytebank.git
cd project_atm-simulador_bytebank

# 2. Instalar dependências do backend
cd atm-backend
npm install
cd ..

# 3. Executar apenas o backend
npm run start:backend

# 4. Em outro terminal, executar apenas o frontend
npm run start:frontend

# OU executar ambos simultaneamente
npm run dev
```

### Acesso
- **Frontend**: http://localhost:5500
- **Backend API**: http://localhost:3000
- **Documentação da API**: http://localhost:3000/docs

## 📁 Estrutura do Projeto

```
project_atm-simulator_bytebank/
├── atm-frontend/     # Interface do usuário (HTML/CSS/JS)
├── atm-backend/      # API REST (Node.js)
│   └── docs/         # Documentação da API
└── README.md         # Este arquivo
```

## 🧪 Contas de Teste

| CPF           | Senha | Saldo    |
|---------------|-------|----------|
| 123.456.789-00| 1234  | R$ 1.500,75 |
| 987.654.321-00| 5678  | R$ 2.300,50 |

## 📚 Documentação Detalhada

- [📖 Frontend - Guia de Desenvolvimento](./atm-frontend/README.md)
- [🔧 Backend - Documentação da API](./atm-backend/README.md)
- [🌐 Documentação da API](./atm-backend/docs/api-docs.md)
- [🚀 Guia de Deploy](./atm-backend/docs/deployment.md)

## 🎯 Funcionalidades

### ✅ Implementadas
- [ ] Login com CPF
- [ ] Consulta de saldo
- [ ] Extrato de transações
- [ ] Saque com validações
- [ ] Depósito
- [ ] Logout seguro
- [ ] API REST completa

### 🔄 Em Desenvolvimento
- [ ] Transferência entre contas
- [ ] Histórico detalhado
- [ ] Notificações em tempo real

## 🛠️ Tecnologias Utilizadas

### Frontend
- HTML5 semântico
- CSS3 com Flexbox/Grid
- JavaScript ES6+ vanilla
- Fetch API para requisições

### Backend
- Node.js vanilla
- Módulos nativos (http, fs, crypto)
- JSON para persistência
- JWT para autenticação

## 🧪 Como Testar

```bash
# Executar testes do backend
npm run test:backend

# Executar testes do frontend
npm run test:frontend

# Executar todos os testes
npm test
```

## 📦 Build e Deploy

```bash
# Build para produção
npm run build

# Deploy local
npm run deploy:local

# Deploy para Azure (exemplo)
npm run deploy:azure
```

## 🤝 Contribuindo

1. Fork o projeto
2. Crie uma branch para sua feature (`git checkout -b feature/nova-funcionalidade`)
3. Commit suas mudanças (`git commit -m 'Adiciona nova funcionalidade'`)
4. Push para a branch (`git push origin feature/nova-funcionalidade`)
5. Abra um Pull Request

## 📄 Licença

Este projeto está sob a licença MIT. Veja o arquivo [LICENSE](LICENSE) para mais detalhes.

## 👨‍💻 Autor

**Johnny Souto**
- GitHub: [@johnnysoutodev](https://github.com/johnnysoutodev)
- LinkedIn: [Johnny Souto](https://linkedin.com/in/johnnysouto)

---

⭐ Se este projeto te ajudou, considere dar uma estrela!