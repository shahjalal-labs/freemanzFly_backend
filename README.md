# FreemanZ Fly Backend - Aviation Commerce & Training Platform API

<p align="center">
  <img src="assets/banner.svg" alt="freemanzFly_backend Banner" width="100%">
</p>

<p align="center">
  <a href="https://nodejs.org"><img src="https://img.shields.io/badge/Node.js-20.x-green?style=for-the-badge&logo=node.js" alt="Node.js"></a>
  <a href="https://expressjs.com"><img src="https://img.shields.io/badge/Express-4.21-black?style=for-the-badge&logo=express" alt="Express"></a>
  <a href="https://www.typescriptlang.org"><img src="https://img.shields.io/badge/TypeScript-5.x-3178C6?style=for-the-badge&logo=typescript" alt="TypeScript"></a>
  <a href="https://www.prisma.io"><img src="https://img.shields.io/badge/Prisma-6.x-2D3748?style=for-the-badge&logo=prisma" alt="Prisma"></a>
  <a href="https://www.mongodb.com"><img src="https://img.shields.io/badge/MongoDB-Atlas-47A248?style=for-the-badge&logo=mongodb" alt="MongoDB"></a>
  <a href="https://bullmq.io"><img src="https://img.shields.io/badge/BullMQ-5.x-FF4500?style=for-the-badge&logo=redis" alt="BullMQ"></a>
  <a href="LICENSE"><img src="https://img.shields.io/badge/License-ISC-blue?style=for-the-badge" alt="License"></a>
</p>

---

## 📖 Overview

**freemanzFly_backend** is FreemanZ Fly Backend (`freemanzFly_backend`) is a mission-critical e-commerce and pilot training platform API built with Node.js, Express.js, TypeScript, and Prisma ORM with MongoDB. The service manages flight gear inventories, coupon promotions, secure order fulfillment, customer reviews, DigitalOcean Spaces asset storage, and automated worker notification queues.

---

## ⚡ Key Features

- ✈️ **Pilot & Flight Gear E-Commerce:** Product catalog management with SKU tracking, categories, discounts, and inventory controls.
- 🎟️ **Promotional Coupon System:** Flexible coupon validation engine supporting percentage discounts, fixed reductions, and expiration controls.
- 📦 **Order Lifecycle & Shipping:** Automated checkout workflows, multi-address shipping book, status updates, and tracking.
- ⭐ **Customer Reviews & Feedback:** Verified purchaser reviews, star ratings, and moderation queues.
- 📬 **Asynchronous Email & Worker Queues:** Background workers powered by BullMQ and Redis for transaction confirmations and flight alerts.
- ☁️ **DigitalOcean Spaces CDN:** AWS S3-compatible media storage with automated ffmpeg/ffprobe asset processing.

---

## 🏗️ System Architecture

```mermaid
flowchart TD
    Client[Web & Mobile Applications] -->|HTTPS REST| Router[Express Application Router]

    subgraph Security ["Security & Validation"]
        Router --> Auth[JWT Auth Guard]
        Router --> Validate[Zod Request Schema Validation]
    end

    subgraph Controllers ["Domain Modules"]
        Auth --> AuthMod[Authentication & User Profile]
        Validate --> ProductMod[Product Catalog & Inventory]
        Validate --> CouponMod[Coupon & Discount Engine]
        Validate --> OrderMod[Order Management & Shipping]
        Validate --> ReviewMod[Review & Rating Service]
    end

    subgraph Storage ["Data & Media Pipeline"]
        Controllers --> Prisma[Prisma ORM Client]
        Prisma --> MongoDB[(MongoDB Cluster)]
        Controllers --> S3[DigitalOcean Spaces S3 API]
    end

    subgraph Workers ["Background Tasks"]
        OrderMod --> BullMQ[BullMQ Redis Queue]
        BullMQ --> EmailWorker[Nodemailer Email Worker]
    end
```

---

## 📂 Directory Structure

```text
.
├── src/
│   ├── app/
│   ├── components/
│   └── ...
├── assets/
│   └── banner.svg
├── .env.example
├── .gitignore
├── package.json
├── README.md
└── LICENSE
```

---

## 🛠️ Tech Stack & Dependencies

| Layer / Library | Version | Description |
|---|---|---|
| **Express.js** | `v4.21` | Core HTTP application framework |
| **TypeScript** | `v5.x` | Type-safe runtime architecture |
| **Prisma ORM** | `v6.x` | MongoDB schema definition and client queries |
| **BullMQ** | `v5.x` | High-performance background job processing with Redis |
| **AWS SDK (S3 Client)** | `v3.x` | Object storage handling for DigitalOcean Spaces |
| **Fluent FFmpeg** | `v2.1` | Media asset validation and transcoding |
| **Nodemailer** | `v6.x` | Automated transactional email dispatch |

---

## ⚙️ Environment Variables

Create a `.env` file in the project root based on the provided sample:

```bash
cp .env.example .env
```

Configurable variables:

```env
PORT=5000
NODE_ENV=development
DATABASE_URL=mongodb+srv://<username>:<password>@cluster.mongodb.net/freemanzfly?retryWrites=true&w=majority

JWT_SECRET=super_secret_jwt_key_here
JWT_EXPIRES_IN=7d
REFRESH_TOKEN_SECRET=super_secret_refresh_key_here
REFRESH_TOKEN_EXPIRES_IN=30d

# Redis / BullMQ
REDIS_HOST=127.0.0.1
REDIS_PORT=6379

# DigitalOcean Spaces / S3
DO_SPACES_ENDPOINT=https://nyc3.digitaloceanspaces.com
DO_SPACES_KEY=your_do_spaces_key
DO_SPACES_SECRET=your_do_spaces_secret
DO_SPACES_BUCKET=freemanzfly-storage

# SMTP
EMAIL_HOST=smtp.gmail.com
EMAIL_PORT=587
EMAIL_USER=notifications@freemanzfly.com
EMAIL_PASS=your_email_password
```

---

## 🚀 Getting Started

### Prerequisites

- Node.js (v20.x or higher recommended)
- Package Manager (`npm`, `yarn`, or `pnpm`)

### Installation

```bash
# Clone repository
git clone https://github.com/shahjalal-labs/freemanzFly_backend.git
cd freemanzFly_backend

# Install dependencies
npm install
```

### Running Locally

```bash
# Start development server
npm run dev
# or for backend services
npm run start:dev
```

### Building for Production

```bash
# Create production build
npm run build

# Start production server
npm start
```

---

## 📄 License

This project is licensed under the [ISC License](LICENSE).
