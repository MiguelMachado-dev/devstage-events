# CodeCraft Summit 2025

[![TypeScript](https://img.shields.io/badge/TypeScript-5.0+-blue.svg)](https://www.typescriptlang.org/)
[![Next.js](https://img.shields.io/badge/Next.js-16.0-black.svg)](https://nextjs.org/)
[![Fastify](https://img.shields.io/badge/Fastify-5.6+-green.svg)](https://www.fastify.io/)
[![Licença](https://img.shields.io/badge/Licença-ISC-purple.svg)](LICENSE)

> **English:** [English Documentation](../README.md)

Um sistema completo de gerenciamento de eventos para o CodeCraft Summit 2025, featuring inscrições de usuários, rastreamento de indicações e rankings em tempo real. Construído com tecnologias de ponta e projetado para escalabilidade e performance.

## 🚀 Visão Geral do Projeto

O CodeCraft Summit 2025 é uma plataforma abrangente de gerenciamento de eventos que possibilita inscrições de usuários e rastreamento de indicações. O sistema featuring um sofisticado programa de indicações baseado em convites onde participantes podem ganhar pontos ao convidar outras pessoas, competir em rankings e acompanhar suas estatísticas em tempo real.

### Recursos Principais

- **🎫 Sistema Inteligente de Inscrição** - Inscrição simplificada de usuários com validação de formulários
- **🔗 Programa de Indicações** - Rastreamento de convites com links únicos e análise de cliques
- **🏆 Rankings em Tempo Real** - Leaderboard dinâmico mostrando os melhores indicadores
- **📊 Análises Pessoais** - Dashboard de estatísticas individuais para cada inscrito
- **📱 Design Responsivo** - Abordagem mobile-first com componentes UI bonitos
- **🔒 APIs Type-Safe** - Backend totalmente tipado com validação Zod
- **⚡ Alta Performance** - Queries de banco de dados otimizadas com caching

## 🏗️ Arquitetura

Este projeto segue uma estrutura moderna de monorepo com clara separação entre frontend e backend:

```
devstage-events/
├── web/                 # Aplicação frontend Next.js 16
│   ├── src/
│   │   ├── app/        # Páginas e layouts do App Router
│   │   ├── components/ # Componentes UI reutilizáveis
│   │   ├── http/       # Cliente API com tipos gerados
│   │   └── assets/     # Assets estáticos e imagens
│   └── orval.config.ts # Config de geração de cliente OpenAPI
├── server/              # API backend Fastify
│   ├── src/
│   │   ├── routes/     # Definições de endpoints API
│   │   ├── functions/  # Funções de lógica de negócio
│   │   ├── drizzle/    # Schema e migrações do banco de dados
│   │   └── redis/      # Configuração do cliente Redis
│   └── env.ts          # Validação de variáveis de ambiente
└── docs/               # Documentação
```

## 🛠️ Stack Tecnológico

### Frontend (Next.js 16)
- **Framework**: Next.js 16 com App Router
- **Linguagem**: TypeScript 5.0+
- **Estilização**: Tailwind CSS 4.1 com sistema de design personalizado
- **Componentes UI**: Biblioteca de componentes personalizados com ícones Lucide React
- **Formulários**: React Hook Form com validação Zod
- **Cliente HTTP**: Gerado automaticamente a partir da especificação OpenAPI usando Orval
- **Linting**: Biome para formatação e linting de código

### Backend (Fastify)
- **Framework**: Fastify 5.6 com type provider Zod
- **Linguagem**: TypeScript 5.9+
- **Banco de Dados**: PostgreSQL com Drizzle ORM
- **Cache**: Redis para otimização de performance
- **Documentação API**: OpenAPI 3.0 com Swagger UI
- **Validação**: Schemas Zod para validação de request/response
- **Qualidade de Código**: Biome para formatação consistente de código

### Infraestrutura e Ferramentas
- **Gerenciador de Pacotes**: npm
- **Ferramentas de Build**: tsup para backend, Next.js para frontend
- **Desenvolvimento**: tsx para hot reloading durante desenvolvimento
- **Migrações de Banco de Dados**: Drizzle Kit
- **Ambiente**: Validação de variáveis de ambiente com Zod
- **Containerização**: Docker Compose para serviços de banco de dados (PostgreSQL & Redis)

## 📋 Pré-requisitos

Antes de executar este projeto, certifique-se de ter o seguinte instalado:

- **Node.js** 18.0 ou superior
- **PostgreSQL** 13 ou superior (ou use Docker)
- **Redis** 6 ou superior (ou use Docker)
- **npm** (vem com Node.js)
- **Docker** (opcional, para serviços de banco de dados)
- **Docker Compose** (opcional, para serviços de banco de dados)

## 🚀 Início Rápido

### Opção 1: Usando Docker para Serviços de Banco de Dados (Recomendado)

A maneira mais fácil de rodar PostgreSQL e Redis é usando Docker Compose:

```bash
# Inicie serviços de banco de dados (PostgreSQL e Redis)
cd server
docker compose up -d

# Visualize logs
docker compose logs -f

# Pare serviços de banco de dados
docker compose down
```

### Opção 2: Desenvolvimento Local

### 1. Clone o Repositório

```bash
git clone https://github.com/MiguelMachado-dev/devstage-events.git
cd devstage-events
```

### 2. Instale as Dependências

```bash
# Instale dependências do backend
cd server
npm install

# Instale dependências do frontend
cd ../web
npm install
```

### 3. Configuração do Ambiente

Crie arquivos de ambiente para ambos os serviços:

**Ambiente Backend** (`server/.env`):
```env
PORT=3333
POSTGRES_URL=postgresql://docker:docker@localhost:5432/connect
REDIS_URL=redis://localhost:6379
WEB_URL=http://localhost:3000
```

**Ambiente Frontend** (`web/.env.local`):
```env
NEXT_PUBLIC_API_URL=http://localhost:3333
```

### 4. Configuração do Banco de Dados

Se você estiver usando Docker Compose para serviços de banco de dados, os bancos já estão configurados. Apenas execute as migrações:

```bash
cd server
npx drizzle-kit push
```

Se você preferir usar instalações locais de banco de dados, atualize o `POSTGRES_URL` e `REDIS_URL` no seu arquivo `.env` correspondemente.

### 5. Inicie os Servidores de Desenvolvimento

Execute ambos os serviços em terminais separados:

```bash
# Terminal 1: Inicie o servidor backend
cd server
npm run dev

# Terminal 2: Inicie o servidor frontend
cd web
npm run dev
```

A aplicação estará disponível em:
- **Frontend**: http://localhost:3000
- **Backend API**: http://localhost:3333
- **Documentação API**: http://localhost:3333/docs

## 🎯 Guia de Uso

### Fluxo de Registro de Usuário

1. **Página Inicial**: Usuários acessam a landing page com informações do evento
2. **Registro**: Preenchem o formulário de inscrição com nome e email
3. **Link de Indicação**: Recebem um link único de indicação após registro bem-sucedido
4. **Compartilhe e Acompanhe**: Compartilham o link de indicação e acompanham os convites
5. **Rankings**: Visualizam rankings em tempo real e estatísticas pessoais

### Endpoints da API

A API fornece os seguintes endpoints:

- `POST /subscriptions` - Registrar novo inscrito
- `GET /invites/{subscriberId}` - Acessar link de indicação (redireciona para site principal)
- `GET /subscribers/{subscriberId}/ranking/clicks` - Obter contagem de cliques para indicações
- `GET /subscribers/{subscriberId}/ranking/count` - Obter contagem de indicações
- `GET /subscribers/{subscriberId}/ranking/position` - Obter posição no ranking
- `GET /ranking` - Obter ranking de melhores indicadores

### Recursos de Desenvolvimento

- **Hot Reloading**: Tanto frontend quanto backend suportam hot reloading durante desenvolvimento
- **Type Safety**: Suporte completo TypeScript com tipos de API gerados
- **Documentação API**: Swagger UI interativo disponível em `/docs`
- **Migrações de Banco**: Drizzle Kit para gerenciamento de schema
- **Formatação de Código**: Formatação automática de código com Biome

## 🔧 Configuração

### Configuração do Banco de Dados

O projeto usa PostgreSQL como banco de dados principal. A conexão é configurada através de variáveis de ambiente:

```typescript
// server/env.ts
const envSchema = z.object({
  POSTGRES_URL: z.url(),
  // ... outras variáveis
})
```

### Configuração Redis

Redis é usado para cache e otimização de performance:

```typescript
// server/src/redis/client.ts
import Redis from 'ioredis'
export const redis = new Redis(process.env.REDIS_URL)
```

### Documentação da API

O backend gera automaticamente documentação OpenAPI. Acesse em:
- **Swagger UI**: http://localhost:3333/docs
- **OpenAPI JSON**: http://localhost:3333/docs/json

## 🧪 Fluxo de Trabalho de Desenvolvimento

### Qualidade do Código

Este projeto usa Biome para formatação e linting de código:

```bash
# Formatar código
npx biome format --write .

# Verificar qualidade do código
npx biome check .
```

### Migrações do Banco de Dados

Para gerenciar mudanças no schema do banco de dados:

```bash
# Gerar migrações
npx drizzle-kit generate

# Aplicar migrações
npx drizzle-kit push

# Visualizar migrações
npx drizzle-kit studio
```

### Geração de Cliente API

O cliente API do frontend é gerado automaticamente a partir da especificação OpenAPI:

```bash
cd web
npx orval
```

## 📦 Build & Deploy

### Build de Produção

```bash
# Build do backend
cd server
npm run build

# Build do frontend
cd ../web
npm run build
```

### Considerações de Deploy

- Certifique-se de que todas as variáveis de ambiente estão configuradas em produção
- Execute migrações do banco de dados antes de iniciar a aplicação
- Configure configurações CORS adequadas para o domínio frontend
- Configure Redis para cache de produção
- Considere usar CDN para assets estáticos
- Use HTTPS e configure certificados SSL
- Configure monitoramento e logging adequados
- Configure estratégias de backup para PostgreSQL

### Docker Compose para Serviços de Banco de Dados

O projeto inclui configuração Docker Compose para fácil configuração de banco de dados:

#### Serviços Disponíveis

- **service-pg**: Banco de dados PostgreSQL (porta 5432)
- **service-redis**: Cache Redis (porta 6379)

#### Variáveis de Ambiente do Banco de Dados

```bash
# Banco de Dados (PostgreSQL)
POSTGRES_USER=docker
POSTGRES_PASSWORD=docker
POSTGRES_DB=connect

# Redis
ALLOW_EMPTY_PASSWORD=yes
```

#### Usando Docker Compose

```bash
# Inicie serviços de banco de dados
cd server
docker compose up -d

# Visualize logs
docker compose logs -f

# Pare serviços
docker compose down
```

## 🔍 Monitoramento & Debug

### Health Checks

A API fornece health checks integrados. Monitore:
- Conectividade do banco de dados
- Status da conexão Redis
- Tempos de resposta da API

### Logging

A aplicação usa console logging em desenvolvimento. Para produção:
- Implemente structured logging
- Configure agregação de logs
- Monitore taxas de erro e métricas de performance

## 🤝 Contribuindo

1. Fork o repositório
2. Crie um branch de feature (`git checkout -b feature/amazing-feature`)
3. Faça suas mudanças
4. Execute testes e linting (`npx biome check .`)
5. Comite suas mudanças (`git commit -m 'Add some amazing feature'`)
6. Push para o branch (`git push origin feature/amazing-feature`)
7. Abra um Pull Request

## 📄 Licença

Este projeto está licenciado sob a Licença ISC - veja o arquivo [LICENSE](LICENSE) para detalhes.

## 🙋‍♂️ Suporte

Para suporte e perguntas:
- Crie uma issue no repositório
- Verifique a documentação da API em `/docs`
- Revise os comentários de código e definições de tipo

---

**Construído com ❤️ para a comunidade do CodeCraft Summit 2025**
