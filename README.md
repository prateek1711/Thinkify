# Thinkify

Thinkify is a modern full-stack web application built using the MERN stack (MongoDB, Express, React, Node.js) with Vite and Material UI.

---

## 📁 Project Structure

```text
Thinkify/
├── client/                 # React frontend powered by Vite
│   ├── .env.example        # Client environment variables template
│   ├── src/                # Frontend source code
│   └── package.json
├── server/                 # Express & Node.js backend
│   ├── .env.example        # Server environment variables template
│   ├── config/             # Database connection
│   ├── controller/         # API controllers
│   ├── middleware/         # Auth & upload middleware
│   ├── models/             # Mongoose schemas
│   ├── routes/             # Express routes
│   └── package.json
└── README.md
```

---

## 🛠️ Prerequisites

Make sure you have installed:
- [Node.js](https://nodejs.org/) (v18 or higher recommended)
- [npm](https://www.npmjs.com/) (comes with Node.js)
- [MongoDB](https://www.mongodb.com/) (Local MongoDB Community Server or MongoDB Atlas cloud URI)

---

## ⚙️ Environment Variables Setup

Both the `server` and `client` require environment variables to run properly.

### 1. Server Environment (`server/.env`)

In the `server` directory, copy `.env.example` to create your `.env` file:

```bash
cd server
copy .env.example .env     # Windows Command Prompt
# or
cp .env.example .env       # PowerShell / macOS / Linux
```

Configure the following variables in `server/.env`:

| Variable | Description | Default / Example |
| :--- | :--- | :--- |
| `PORT` | Port for the backend server | `3000` |
| `CLIENT_URL` | Frontend URL allowed by CORS | `http://localhost:5173` |
| `DATABASE_URL` | MongoDB connection string | `mongodb+srv://<username>:<password>@cluster0.mongodb.net/?appName=Cluster0` or `mongodb://localhost:27017` |
| `DATABASE_NAME` | Name of the database | `thinkify` |
| `BCRYPT_GEN_SALT_NUMBER` | Bcrypt salt hashing rounds | `10` |
| `JWT_SECRET_KEY` | Secret key for JWT signing | `your_jwt_secret_key` |
| `COOKIE_EXPIRES` | Cookie and token duration | `5d` |
| `COOKIE_KEY` | Authentication cookie identifier | `thinkify` |
| `UPLOAD_DIRECTORY` | Upload directory for images | `uploads` |

### 2. Client Environment (`client/.env`)

In the `client` directory, copy `.env.example` to create your `.env` file:

```bash
cd client
copy .env.example .env     # Windows Command Prompt
# or
cp .env.example .env       # PowerShell / macOS / Linux
```

Configure the following variables in `client/.env`:

| Variable | Description | Local Development Value |
| :--- | :--- | :--- |
| `VITE_SERVER_ENDPOINT` | Backend API base URL | `http://localhost:3000/api` |
| `VITE_TOKEN_KEY` | Storage key for JWT token | `thinkify` |
| `VITE_COOKIE_KEY` | Storage key for authentication cookie | `thinkify` |
| `VITE_USER_ROLE` | Storage key for user role | `role` |
| `VITE_USER_KEY` | Storage key for user identifier | `role` |
| `VITE_COOKIE_EXPIRES` | Cookie expiration period in days | `1` |

> **Note:** For local development, `VITE_SERVER_ENDPOINT` points to `http://localhost:3000/api`. When deploying to Vercel or any cloud hosting, update this to your deployed backend URL (e.g., `https://your-server.vercel.app/api`).

---

## 🚀 Running the Project Locally

Follow these steps to run the application on your computer:

### Step 1: Start the Backend Server

Open a terminal in the project root:

```bash
cd server
npm install
npm run dev
```

The server will start listening at:
`http://localhost:3000`

### Step 2: Start the Frontend Client

Open a **separate terminal** in the project root:

```bash
cd client
npm install
npm run dev
```

Vite will start the development server at:
`http://localhost:5173`

Open `http://localhost:5173` in your browser to view and interact with the application.

---

## 📜 Available Scripts

### Server (`/server`)
- `npm run dev`: Runs the backend in watch mode (auto-restarts on code changes).
- `npm start`: Starts the backend server with Node.js.

### Client (`/client`)
- `npm run dev`: Starts the Vite development server with Hot Module Replacement (HMR).
- `npm run build`: Compiles and bundles production-ready frontend assets into `/dist`.
- `npm run preview`: Locally previews the production build.

---

## 🌐 Production Deployment Guide

Deploying **Backend on Render** and **Frontend on Vercel**:

### 1. Deploy Backend to Render

1. Log in to [Render](https://render.com).
2. Click **New +** and select **Web Service**.
3. Connect your GitHub repository.
4. Fill in the service configuration:
   - **Name**: `thinkify-server`
   - **Root Directory**: `server`
   - **Runtime**: `Node`
   - **Build Command**: `npm install`
   - **Start Command**: `npm start`
   - **Instance Type**: `Free`
5. Under **Environment Variables**, add:
   - `PORT`: `10000`
   - `DATABASE_URL`: Your MongoDB Atlas connection URI
   - `DATABASE_NAME`: `thinkify`
   - `BCRYPT_GEN_SALT_NUMBER`: `10`
   - `JWT_SECRET_KEY`: A strong random string
   - `COOKIE_EXPIRES`: `5d`
   - `COOKIE_KEY`: `thinkify`
   - `UPLOAD_DIRECTORY`: `uploads`
   - `CLIENT_URL`: `https://your-client-app.vercel.app` (or leave empty initially)
6. In **MongoDB Atlas**, go to **Network Access** and ensure `0.0.0.0/0` (allow access from anywhere) is enabled.
7. Click **Create Web Service**.
8. Once deployed, copy your Render server URL (e.g., `https://thinkify-server-xxxx.onrender.com`). Your API endpoint is:
   `https://thinkify-server-xxxx.onrender.com/api`

### 2. Deploy Frontend to Vercel

1. Log in to [Vercel](https://vercel.com).
2. Click **Add New...** -> **Project**.
3. Import your GitHub repository.
4. In the project settings:
   - **Framework Preset**: `Vite`
   - **Root Directory**: Click **Edit** and choose `client`
5. Under **Environment Variables**, add:
   - `VITE_SERVER_ENDPOINT`: `https://thinkify-server-xxxx.onrender.com/api` (Render backend URL + `/api`)
   - `VITE_TOKEN_KEY`: `thinkify`
   - `VITE_COOKIE_KEY`: `thinkify`
   - `VITE_USER_ROLE`: `role`
   - `VITE_USER_KEY`: `role`
   - `VITE_COOKIE_EXPIRES`: `1`
6. Click **Deploy**.
7. Once deployed, open your Vercel URL to access your live application.

