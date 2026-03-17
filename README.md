# Backend App

A Node.js + Express backend app with EJS views for admin management and API endpoints for store, authentication, and orders.

## Tech Stack

- Node.js (ES modules)
- Express 5
- EJS + express-ejs-layouts
- MongoDB + Mongoose
- Session auth for admin pages
- JWT auth for user order APIs

## Project Structure

- `config/` - database connection
- `controllers/` - route handlers
- `middleware/` - session/JWT auth guards
- `models/` - Mongoose schemas
- `routes/` - route modules
- `views/` - EJS templates
- `public/` - static assets

## Prerequisites

- Node.js 20+
- npm
- MongoDB connection string

## Environment Variables

Create a `.env` file in the project root:

```env
MONGO_URI=mongodb+srv://<user>:<password>@<cluster>/<database>
```

## Installation

```bash
npm install
```

## Run Locally

```bash
node index.js
```

Server starts on:

- `http://localhost:5000`

## Authentication Model

- Admin pages use `express-session`:
  - Login from `/auth/login`
  - Protected admin routes:
    - `/`
    - `/products/*`
    - `/users/*`
- User APIs use JWT in `Authorization: Bearer <token>`:
  - `/orders/*`

## Main Routes

### Auth

- `GET /auth/login` - Login page
- `POST /auth/login` - Admin login
- `GET /auth/register` - Register page
- `POST /auth/register` - Create user/admin record (depending on submitted role)
- `GET /auth/logout` - Logout admin session
- `POST /auth/signup` - API signup
- `POST /auth/signin` - API signin (returns JWT)

### Store

- `GET /store` - Public product listing

### Products (Admin)

- `GET /products` - List products
- `GET /products/add` - Add form
- `POST /products/add` - Create product
- `GET /products/:id/edit` - Edit form
- `POST /products/:id/save` - Update product
- `GET /products/:id/delete` - Delete product

### Users (Admin)

- `GET /users` - List users
- `GET /users/add` - Add form
- `POST /users/add` - Create user
- `GET /users/:id/edit` - Edit form
- `POST /users/:id/save` - Update user
- `GET /users/:id/delete` - Delete user

### Orders (JWT protected)

- `POST /orders` - Place order
- `GET /orders/:email` - Fetch orders by user email

## CI

A GitHub Actions workflow is provided at `.github/workflows/ci.yml`.

It runs on push and pull requests to:

- install dependencies (`npm ci`)
- validate JavaScript syntax with `node --check`

## Notes

- Current `npm test` script is a placeholder and exits with failure by default.
- App currently uses hardcoded secrets in code for session/JWT; move these to environment variables for production.