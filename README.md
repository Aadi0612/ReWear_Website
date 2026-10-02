# 🌿 ReWear — Sustainable Clothing Swap & Circular Fashion Platform

[![Node.js](https://img.shields.io/badge/Node.js-v18+-green.svg)](https://nodejs.org/)
[![React](https://img.shields.io/badge/React-18-blue.svg)](https://react.dev/)
[![Vite](https://img.shields.io/badge/Vite-Build_Tool-646CFF.svg)](https://vitejs.dev/)
[![MongoDB](https://img.shields.io/badge/MongoDB-Database-47A248.svg)](https://www.mongodb.com/)
[![Socket.io](https://img.shields.io/badge/Socket.io-Real--Time-black.svg)](https://socket.io/)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

**ReWear** is a full-stack, community-driven platform designed to reduce textile waste and encourage sustainable fashion. Users can list unworn or gently used clothing, propose direct swaps, negotiate via real-time messaging, review swap partners, and track their personal and community-wide environmental sustainability metrics.

---

## 📑 Table of Contents

- [Features](#-features)
- [Tech Stack](#-tech-stack)
- [Architecture & Directory Structure](#-architecture--directory-structure)
- [Getting Started](#-getting-started)
  - [Prerequisites](#prerequisites)
  - [Environment Variables](#environment-variables)
  - [Installation & Local Setup](#installation--local-setup)
- [Database Seeding](#-database-seeding)
- [API Overview](#-api-overview)
- [Deployment](#-deployment)
- [Contributing](#-contributing)
- [License](#-license)

---

## ✨ Features

### 👤 User & Authentication
- **Secure Authentication**: JWT-based user authentication and session management via Passport.js.
- **Account Management**: Profile personalization, password reset workflows, and user activity history.

### 👗 Wardrobe Management & Marketplace
- **Item Listings**: Create, edit, and categorize items with multi-image Cloudinary upload and real-time progress indicators.
- **Search & Discovery**: Browse, filter, and inspect listings with item condition and sizing specifications.

### 🔄 Swap Negotiation & Exchange
- **Swap Requests**: Propose, accept, reject, or counter clothing swaps between users.
- **Real-Time Chat**: Live peer-to-peer messaging powered by Socket.io for coordinating logistics and item details.
- **Reputation & Feedback**: Post-swap reviews and ratings to foster trust within the community.

### 🌱 Sustainability Impact
- **Impact Tracking**: Calculate ecological metrics (such as water preserved, carbon emissions offset, and garments diverted from landfills).

### 🛡️ Administration & Moderation
- **Admin Dashboard**: Dedicated management portal to inspect swap transactions, manage user disputes, and moderate item listings.
- **Notifications**: In-app and email alert triggers for swap statuses and messages.

---

## 🛠 Tech Stack

### Frontend
- **Framework**: [React](https://reactjs.org/) (Vite bundler)
- **Routing**: React Router
- **State & Context**: Context API (`AuthContext`, `SocketContext`, `ChatContext`, `NotificationContext`)
- **Networking**: Axios, Socket.io-client
- **Styling**: Modern modular CSS / CSS3

### Backend
- **Runtime**: [Node.js](https://nodejs.org/) & [Express.js](https://expressjs.com/)
- **Database**: [MongoDB](https://www.mongodb.com/) via [Mongoose ODM](https://mongoosejs.com/)
- **Real-Time**: [Socket.io](https://socket.io/)
- **Authentication**: Passport.js, JSON Web Tokens (JWT), Bcrypt
- **Media Management**: Cloudinary API & Multer
- **Email Service**: Nodemailer

---

## 📂 Architecture & Directory Structure

```text
ReWear-main/
├── backend/
│   ├── config/             # Cloudinary, MongoDB, Mailer, and Passport configurations
│   ├── controllers/        # Route controllers (Auth, Item, Swap, Chat, Admin, etc.)
│   ├── middleware/         # Auth verification and global error handlers
│   ├── models/             # Mongoose schemas (User, Item, Swap, Review, Message, etc.)
│   ├── routes/             # RESTful endpoints
│   ├── sockets/            # Socket.io event listeners & emitters
│   ├── utils/              # Email templates, notification helpers, seed scripts
│   ├── server.js           # Server entry point
│   └── package.json
│
├── frontend/
│   ├── public/             # Static public assets
│   ├── src/
│   │   ├── assets/         # Icons, illustrations, and logos
│   │   ├── components/     # Reusable UI (Navbar, Footer, ItemCard, Modals, Loaders)
│   │   ├── context/        # React Context providers (Auth, Chat, Sockets, Notifications)
│   │   ├── pages/          # Application views (Browse, Dashboard, Admin, Chat, etc.)
│   │   ├── services/       # Axios API client instances
│   │   ├── App.jsx         # Root route configuration
│   │   └── main.jsx        # App entry point
│   ├── vite.config.js      # Vite configuration
│   └── package.json
│
└── scripts/
    └── generate-secrets.js # Helper utility to generate secure random keys
```

---

## 🚀 Getting Started

### Prerequisites

Ensure you have installed:
- **Node.js** (v18.0.0 or later)
- **npm** or **yarn**
- **MongoDB** instance (Local or [MongoDB Atlas](https://www.mongodb.com/atlas))
- **Cloudinary** account (for media storage)

---

### Environment Variables

#### 1. Backend (`backend/.env`)
Create a `.env` file inside the `backend/` directory by copying `.env.example`:

```bash
cp backend/.env.example backend/.env
```

Fill in the necessary values:

```env
PORT=5000
NODE_ENV=development
MONGO_URI=mongodb+srv://<username>:<password>@cluster.mongodb.net/rewear?retryWrites=true&w=majority
JWT_SECRET=your_super_secret_jwt_key
JWT_EXPIRE=7d

# Cloudinary
CLOUDINARY_CLOUD_NAME=your_cloud_name
CLOUDINARY_API_KEY=your_api_key
CLOUDINARY_API_SECRET=your_api_secret

# Mailer (SMTP / Nodemailer)
SMTP_HOST=smtp.mailtrap.io
SMTP_PORT=2525
SMTP_USER=your_smtp_user
SMTP_PASS=your_smtp_pass
FROM_EMAIL=noreply@rewear.com
FROM_NAME="ReWear Support"

# Client URL (for CORS)
CLIENT_URL=http://localhost:5173
```

> **Tip:** You can generate secure JWT and session secrets using the included utility:
> ```bash
> node scripts/generate-secrets.js
> ```

#### 2. Frontend (`frontend/.env`)
Create a `.env` file inside the `frontend/` directory:

```env
VITE_API_URL=http://localhost:5000/api
VITE_SOCKET_URL=http://localhost:5000
```

---

### Installation & Local Setup

#### Step 1: Clone the repository
```bash
git clone https://github.com/<your-username>/ReWear.git
cd ReWear
```

#### Step 2: Install dependencies & run backend
```bash
cd backend
npm install
npm run dev
```
The backend server should now run on `http://localhost:5000`.

#### Step 3: Install dependencies & run frontend
In a separate terminal:
```bash
cd frontend
npm install
npm run dev
```
The client app should now be live on `http://localhost:5173`.

---

## 🧪 Database Seeding

To populate your database with dummy users, categories, clothing items, and demo swap interactions:

```bash
cd backend
npm run seed
# or
node utils/seed.js
```

---

## 📡 API Overview

The backend exposes a REST API under the `/api` prefix:

| Endpoint Prefix | Description | Protected |
| :--- | :--- | :--- |
| `/api/auth` | User signup, signin, password recovery, session verification | Partial |
| `/api/items` | Clothing listings, filtering, image uploads, details | Partial |
| `/api/swaps` | Swap proposals, accept/counter/reject, status changes | Yes |
| `/api/messages` | Conversation threads and historical chat logs | Yes |
| `/api/notifications`| User alert retrieval, read/unread states | Yes |
| `/api/reviews` | Feedback and ratings submission for completed swaps | Yes |
| `/api/admin` | Swap moderation, user control, platform metrics | Admin Only |

---

## 🌐 Deployment

- **Backend**: Ready for deployment to platforms like [Render](https://render.com/), [Railway](https://railway.app/), or [Heroku]. Refer to `backend/DEPLOYMENT.md` for specific instructions.
- **Frontend**: Configured for continuous deployment via [Vercel](https://vercel.com/) (using `frontend/vercel.json`) or [Netlify](https://www.netlify.com/). Refer to `frontend/DEPLOYMENT.md`.

---

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. **Fork** the project repository.
2. Create your feature branch (`git checkout -b feature/AmazingFeature`).
3. Commit your modifications (`git commit -m 'Add some AmazingFeature'`).
4. Push to your branch (`git push origin feature/AmazingFeature`).
5. Open a **Pull Request**.

---

## 📄 License

Distributed under the MIT License. See `LICENSE` for more information.
