# 🚀 Template Node.js + TypeScript + Docker

<div align="center">

![Node.js](https://img.shields.io/badge/Node.js-22-green)
![TypeScript](https://img.shields.io/badge/TypeScript-5.9-blue)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-15-blue)
![Docker](https://img.shields.io/badge/Docker-✓-blue)

**Template profissional para APIs Node.js com TypeScript, Docker, PostgreSQL e ambiente de desenvolvimento completo**
</div>

## ✨ Características

- ✅ **Node.js 22 + Express** - Servidor robusto e escalável
- ✅ **TypeScript** - Desenvolvimento tipado e seguro
- ✅ **Docker + Docker Compose** - Containers para desenvolvimento e produção
- ✅ **PostgreSQL 15** - Banco de dados relacional
- ✅ **Sequelize ORM** - Modelagem de dados com TypeScript
- ✅ **Jest + SuperTest** - Testes automatizados
- ✅ **ESLint + Prettier** - Padronização de código
- ✅ **SQLite** - Banco em memória para testes
- ✅ **Hot Reload** - Desenvolvimento com atualização automática
- ✅ **PGAdmin** - Interface web para gerenciar o PostgreSQL
- ✅ **Multi-ambiente** - Desenvolvimento, Teste e Produção

## 🏁 Começo Rápido

### 📋 Pré-requisitos

- [Docker](https://docs.docker.com/get-docker/) 
- [Docker Compose](https://docs.docker.com/compose/install/)
- [Node.js 18+](https://nodejs.org/) (opcional - para desenvolvimento local)

### 🚀 Início Rápido (3 minutos)

## 📋 Pré-requisitos

### Docker

### Docker Compose

### Node.js 18+ (opcional - para desenvolvimento local)

## 🚀 Início Rápido (Backend + Frontend)

Este comando inicia todos os serviços (Backend, DB, PGAdmin e Frontend) e o build das imagens:

```bash
# 1. Copiar o template
cp -r template-node-ts meu-projeto
cd meu-projeto

# 2. Configurar ambiente
cp .env.example .env              # Backend/Infra
cp frontend/.env.example frontend/.env # Frontend (variáveis públicas)

# 3. Executar o ambiente Full-Stack com Docker
docker compose up --build

# 4. Acessar a aplicação
# 🌐 Frontend (React): http://localhost:5173
# 🌐 API (Backend):    http://localhost:3000
# 📊 PGAdmin:         http://localhost:8080
```



## 🛠 Comandos Úteis

## 🐳 Docker Commands

```bash
# Iniciar ambiente Full-Stack (Backend, DB, Frontend)
docker compose up

# Iniciar APENAS o Backend e infra (ignora o frontend)
docker compose up --build app database pgadmin

# Iniciar em background
docker compose up -d

# Parar ambiente
docker compose down

# Parar e remover volumes (reset completo)
docker compose down -v

# Ver logs da aplicação (Backend)
docker compose logs app

# Ver logs do Frontend
docker compose logs frontend

```


## 🔧 Comandos no Container (Backend - Serviço app)

```bash
# Executar testes
docker compose exec app npm test

# ESLint
docker compose exec app npm run lint
docker compose exec app npm run lint:fix

# Formatação de código
docker compose exec app npm run format

# Migrações do banco
docker compose exec app npx sequelize-cli db:migrate
# ... (Outros comandos de Sequelize-CLI, conforme original) ...

# Acessar terminal do container (Backend)
docker compose exec app sh
```



## 🖼️ Comandos no Container (Frontend - Serviço frontend)

```bash
# Acessar terminal do container (Frontend)
docker compose exec frontend sh

# Instalar novas dependências no Frontend
docker compose exec frontend npm install nome-do-pacote

```



## ⚙️ Variáveis de Ambiente (Modularidade)

O template utiliza dois arquivos ```.env ``` separados para garantir a modularidade e segurança:

1. ```./.env``` (Raiz): Variáveis do Backend e Secretas (JWT_SECRET, Credenciais do DB, Portas).

2. ```./frontend/.env```: Variáveis Públicas do Frontend (VITE_APP_NAME, Feature Flags).

### Comunicação API (Docker vs Local):

O Docker Compose injeta a URL de API correta para o contêiner ```frontend``` no momento da execução, sobrescrevendo o ```localhost``` do arquivo ```frontend/.env```:

| Contexto| Variável VITE_API_URL| Destino |
|-------------|-------------|-------------|
| Rodando via Docker| http://app:3000/api| Comunicação interna entre containers      |
| Rodando Localmente    | [Dado 2 ](http://localhost:3000/api)     | Comunicação no Host (sua máquina)     |



## 🗄️ Banco de Dados

## 📊 PostgreSQL (Desenvolvimento/Produção)

### Credenciais Padrão:

```bash
DB_HOST=database # Nome do serviço Docker (interno)
DB_PORT=5432
DB_NAME=myapp
DB_USER=dev
DB_PASSWORD=dev123
```


## 🖥️ PGAdmin (Interface Web)

 - URL: http://localhost:8080

 - Email: admin@app.com

 - Senha: admin123

## Configuração do Servidor no PGAdmin:

 - Host: postgres_db

 - Port: 5432

 - Database: myapp

 - Username: dev

 - Password: dev123

## 🏗️ Estrutura do Projeto

```text
TEMPLATE-MODE-TS/
    ├── 📁 src/                  # Código Fonte do BACKEND
    │   ├── 🗄️ database/
    │   ├── 🎮 controllers/
    │   └── ... (Restante da estrutura Backend)
    ├── 📁 frontend/             # MÓDULO FRONTAL (Vite/React)
    │   ├── 📁 src/              # Código Fonte do Frontend
    │   ├── 📄 .env              # Variáveis Públicas do Frontend
    │   ├── 📄 vite.config.ts    # Configuração do Vite
    │   └── 🐳 Dockerfile.dev    # Dockerfile específico do Frontend
    ├── 📄 .env.example          # Variáveis do Backend/Infra
    ├── 📄 .dockerignore         # Ignora node_modules
    ├── 📄 .gitignore            # Ignora node_modules + frontend/node_modules
    ├── 🐳 docker-compose.yml     # Orquestrador FULL-STACK
    ├── 🐳 Dockerfile             # Dockerfile do Backend
    ├── ⚙️ package.json            # Dependências do Backend
    └── ⚙️ tsconfig.json           # Configuração TS do Backend
```




## 💻 Desenvolvimento Local (sem Docker)

Se você optar por rodar o Backend e o Frontend separadamente na sua máquina:

### 1. Iniciar Backend (com Docker infraestrutura):

```bash
# Sobe apenas o PostgreSQL e o PGAdmin
docker compose up -d database pgadmin
# Instala dependências do Backend
npm install
# Roda o backend
npm run dev
```



### 2. Iniciar Frontend (Localmente):

```bash
cd frontend
# Instala dependências do Frontend
npm install
# Roda o frontend (usando localhost:3000 conforme frontend/.env)
npm run dev
```


## 📄 Licença

Distribuído sob licença MIT. Veja LICENSE para mais informações.

## 👨‍💻 Autor

JOSÉ EDMAR DE SIQUEIRA -  GitHub: [@jesiqueira](https://github.com/jesiqueira)

🙏 Agradecimentos

- Express.js

- Sequelize

- Docker

- TypeScript

- Vite

- React

<div align="center">
⭐ Se este template foi útil, considere dar uma estrela no repositório!

🎯 Desenvolvido para acelerar seu desenvolvimento Node.js + TypeScript + React!

</div>