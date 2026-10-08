# Backend Financial Ledger & Double-Entry Accounting System 💳💸

A robust, production-grade Financial Ledger and Double-Entry Accounting backend service built using **Node.js**, **Express.js**, and **MongoDB**. Designed with strict data integrity, immutability, idempotency, and ACID transaction guarantees.

---

## 🌟 Key Architecture & Highlights

- **Double-Entry Bookkeeping System**: Every money transfer produces a paired `DEBIT` and `CREDIT` ledger entry, ensuring mathematical symmetry across all accounts.
- **Immutable Ledger Engine**: Enforces read-only schema immutability using Mongoose pre-hooks (`pre('updateOne')`, `pre('findOneAndUpdate')`, etc.). Historical ledger entries can never be modified or deleted.
- **Dynamic Balance Calculation**: Account balances are derived dynamically on read using MongoDB Aggregation Pipelines (`$group`, `$cond`, `$subtract`), preventing state drift and sync bugs.
- **ACID Transactions**: Multi-document transfer workflows run inside MongoDB Sessions (`startSession` / `commitTransaction`) for all-or-nothing atomicity.
- **Idempotency Safeguards**: Idempotency key tracking prevents double-spending and duplicate charges during network retries.
- **Authentication & Security**: JWT-based authentication stored in `httpOnly` cookies, password hashing with `bcryptjs`, and a token blacklist model for secure logouts.
- **Automated Email Receipts**: Real-time transaction and registration notifications powered by Nodemailer (OAuth2 integration).

---

## 🛠️ Tech Stack

- **Runtime**: Node.js
- **Framework**: Express.js
- **Database**: MongoDB & Mongoose
- **Authentication**: JSON Web Tokens (JWT), BcryptJS
- **Email Service**: Nodemailer (OAuth2)

---

## 🚀 Getting Started

### 1. Prerequisites
- Node.js (v16+ recommended)
- MongoDB instance running locally or via MongoDB Atlas

### 2. Installation & Setup

```bash
# Clone the repository
git clone https://github.com/srikanth26-hub/backend_project.git
cd backend_project

# Install dependencies
npm install
```

### 3. Environment Variables
Create a `.env` file in the root directory following `.env.example`:

```env
PORT=3000
MONGO_URI=mongodb://localhost:27017/backend-ledger
JWT_SECRET=your_secret_key
EMAIL_USER=your_email@gmail.com
CLIENT_ID=your_client_id
CLIENT_SECRET=your_client_secret
REFRESH_TOKEN=your_refresh_token
```

### 4. Running the Server

```bash
# Development mode
npm run dev

# Production mode
npm start
```

---

## 📌 API Endpoint Summary

### Auth Routes (`/api/auth`)
- `POST /api/auth/register` - User Registration
- `POST /api/auth/login` - User Login
- `POST /api/auth/logout` - User Logout (Blacklists token)

### Account Routes (`/api/accounts`)
- Account management & balance retrieval

### Transaction Routes (`/api/transactions`)
- `POST /api/transactions` - Process double-entry money transfer with idempotency key

---

## 📄 License
ISC
