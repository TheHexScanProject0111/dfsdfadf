# HexScan ⛓️

A full-stack BNB Smart Chain (BSC) blockchain explorer with a real-time transaction indexer, built with TypeScript. Browse blocks, transactions, and accounts on the BNB Chain with a modern web interface backed by a high-performance indexing engine.

## What It Does

Index BSC blockchain data → Store & Process → Serve via API → Explore in Browser

- **Real-time Indexing**: Live BSC blockchain data ingestion via the `bsc-indexer` service
- **Full Explorer Frontend**: Browse blocks, transactions, and accounts through a clean web UI
- **REST API Backend**: Structured API endpoints for querying indexed blockchain data
- **Production Scale**: Handles BSC's high-throughput block production

## Features

- 🐋 **Whale Detection** — Flag and track large BNB/token transfers in real-time
- 🪙 **Token Filtering** — Filter and monitor activity for specific BEP-20 tokens across wallets
- 📈 **Whale Analytics** — Visualize whale movement patterns, accumulation, and distribution
- 🕵️ **Wallet Profiling** — Deep-dive into whale wallets — holdings, history, and connected addresses
- ⚡ **Real-time Indexing** — Capture whale movements the moment they hit the chain
- 🔗 **REST API** — Query whale transactions, top holders, and large transfers programmatically

## Project Structure

```
hexscan/
├── bnb-explorer-frontend/
│   ├── src/
│   │   ├── app/
│   │   │   ├── address/[address]/
│   │   │   ├── transactions/
│   │   │   ├── tx/[hash]/
│   │   │   ├── layout.tsx
│   │   │   └── page.tsx
│   │   ├── components/
│   │   │   ├── layout/
│   │   │   ├── AddressClient.tsx
│   │   │   ├── DashboardClient.tsx
│   │   │   ├── TransactionsClient.tsx
│   │   │   └── TxDetailClient.tsx
│   │   ├── hooks/
│   │   │   ├── useSocket.ts
│   │   │   ├── usePolling.ts
│   │   │   └── useDebouncedSearch.ts
│   │   ├── lib/
│   │   │   ├── api.ts
│   │   │   ├── constants.ts
│   │   │   ├── types.ts
│   │   │   └── utils.ts
│   ├── package.json
│   └── tailwind.config.ts
│
├── bnb-explorer-backend/
│   ├── src/
│   │   ├── index.ts
│   │   └── routes.ts
│   ├── prisma/
│   │   └── schema.prisma
│   ├── .env
│   ├── package.json
│   └── tsconfig.json
│
├── bsc-indexer/
│   ├── src/
│   │   ├── database/
│   │   │   ├── client.ts
│   │   │   └── schema.prisma
│   │   ├── processing/
│   │   │   ├── abi.ts
│   │   │   ├── dataHandler.ts
│   │   │   ├── filters.ts
│   │   │   └── logger.ts
│   │   ├── rpc/
│   │   │   ├── client.ts
│   │   │   └── subscriptions.ts
│   │   ├── types/
│   │   └── index.ts
│   ├── scripts/
│   │   ├── test-connection.ts
│   │   ├── database-test.ts
│   │   └── setup.sh
│   ├── .env
│   ├── docker-compose.yml
│   └── package.json
│
├── .gitignore
└── README.md
```

## Quick Start

### 1. Clone the Repository

```bash
git clone https://github.com/TheHexScanProject0111/dfsdfadf
cd dfsdfadf
```

### 2. Set Up the BSC Indexer

```bash
cd bsc-indexer
npm install

# Configure your RPC endpoint and database URL
cp .env.example .env

# Spin up Postgres
docker-compose up -d

# Push the Prisma schema
npx prisma db push --schema=src/database/schema.prisma

# Test connections
npx ts-node scripts/test-connection.ts
npx ts-node scripts/database-test.ts

# Start indexing
npm run dev
```

### 3. Set Up the Backend

```bash
cd bnb-explorer-backend
npm install
cp .env.example .env
npx prisma db push --schema=prisma/schema.prisma
npm run dev
```

### 4. Set Up the Frontend

```bash
cd bnb-explorer-frontend
npm install
cp .env.example .env
npm run dev
```

## Tech Stack

- **Frontend**: Next.js 14 (App Router) + Tailwind CSS
- **Backend**: Express.js + Socket.io
- **Indexer**: Custom BSC indexer via WebSocket (WSS) subscriptions
- **Database**: PostgreSQL + Prisma ORM
- **Language**: TypeScript
- **Infra**: Docker (Postgres), WebSockets for real-time updates

## Core Components

### BSC Indexer
Connects to a BSC node via WebSocket (WSS), streams new blocks and transactions in real-time, runs them through whale detection and token filtering logic, and writes structured data to PostgreSQL via Prisma. Includes rate-limit handling and configurable thresholds.

### Explorer Backend
An Express + Socket.io server that exposes REST endpoints with sorting and filtering, and pushes real-time updates to connected frontend clients over WebSockets.

### Explorer Frontend
A Next.js 14 dashboard with App Router — browse transactions, inspect addresses, view transaction details, and watch live whale activity via WebSocket-powered updates. Built with Tailwind CSS.

## Use Cases

- **Block Exploration**: Browse BSC blocks, view transaction lists, and inspect individual transfers
- **Transaction Lookup**: Search by transaction hash, block number, or account address
- **Account Monitoring**: View account balances, transaction history, and token holdings
- **Analytics**: Query indexed data for on-chain analytics and reporting
- **Development**: Use the API as a backend for dApps that need BSC chain data

## Environment Setup

**BSC Indexer** (`bsc-indexer/.env`)
```env
RPC_ENDPOINT="your_rpc_url"
DATABASE_URL="postgresql://user:pass@localhost:5432/bsc_explorer"
```

**Backend** (`bnb-explorer-backend/.env`)
```env
BACKEND_INTERNAL_URL="http://localhost:3001"
DATABASE_URL="postgresql://user:pass@localhost:5432/bsc_explorer"
```

**Frontend** (`bnb-explorer-frontend/.env`)
```env
NEXT_PUBLIC_API_URL="http://localhost:3001"
```

## Contributors

This project is maintained by 3 contributors.

## License

MIT License — feel free to use for commercial projects!

---

⭐ **Star HexScan** if you found it useful!

Built with ❤️ for the BNB Chain ecosystem