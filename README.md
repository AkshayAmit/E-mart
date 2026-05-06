# E-mart Daily Needs

Full-stack daily-needs e-commerce app with a static HTML/CSS/JavaScript frontend and a Node.js, Express, MongoDB, JWT, and Stripe backend.

## Project Structure

```text
E-mart/
  frontend/
    index.html
    cart.html
    checkout.html
    login.html
    signup.html
    admin.html
    success.html
    failure.html
    style.css
    script.js
  backend/
    server.js
    package.json
    package-lock.json
    config/
    middleware/
    models/
    routes/
    utils/
    database/
      sampleProducts.js
      seed.js
  .env
  .env.example
  render.yaml
```

## Run Locally

1. Open this folder in VS Code.
2. Install backend dependencies:

```bash
cd backend
npm install
```

3. Update the root `.env` with your real values:

```text
MONGO_URI=your-mongodb-connection-string
JWT_SECRET=your-long-random-secret
STRIPE_KEY=your-stripe-secret-key
STRIPE_WEBHOOK_SECRET=your-stripe-webhook-secret
CLIENT_URL=http://localhost:5000
CORS_ORIGIN=http://localhost:5000
```

4. Seed starter products if `AUTO_SEED_PRODUCTS` is not enabled:

```bash
npm run seed
```

5. Start the app:

```bash
npm start
```

6. Open:

```text
http://localhost:5000
```

## Admin Login

Customers cannot see admin access in the shop UI. The server creates or updates one admin account from these `.env` values when it starts:

```text
ADMIN_EMAIL=admin@emart.local
ADMIN_PASSWORD=ChangeMeAdmin123
ADMIN_NAME=E-mart Admin
```

Open the private admin login page directly:

```text
http://localhost:5000/admin-login.html
```

After login, the admin can manage products at:

```text
http://localhost:5000/admin.html
```

## Render Deployment

Use these Render settings:

```text
Service Type: Web Service
Root Directory: backend
Build Command: npm install
Start Command: npm start
Health Check Path: /api/health
```

Add these environment variables in Render:

```text
MONGO_URI=your-mongodb-connection-string
JWT_SECRET=your-long-random-secret
STRIPE_KEY=your-stripe-secret-key
STRIPE_WEBHOOK_SECRET=your-stripe-webhook-secret
CLIENT_URL=https://your-service-name.onrender.com
CORS_ORIGIN=https://your-service-name.onrender.com
ADMIN_EMAIL=admin@yourdomain.com
ADMIN_PASSWORD=your-admin-password
ADMIN_NAME=E-mart Admin
AUTO_SEED_PRODUCTS=true
```

## Stripe Webhooks

For local webhook testing, install the Stripe CLI and forward events:

```bash
stripe listen --forward-to localhost:5000/api/payments/webhook
```

Copy the generated `whsec_...` value into `STRIPE_WEBHOOK_SECRET`.

## API Summary

- `POST /api/auth/signup`
- `POST /api/auth/login`
- `GET /api/auth/me`
- `GET /api/products`
- `POST /api/products` admin
- `PUT /api/products/:id` admin
- `DELETE /api/products/:id` admin
- `GET /api/cart`
- `POST /api/cart/items`
- `PATCH /api/cart/items/:productId`
- `DELETE /api/cart/items/:productId`
- `POST /api/orders`
- `GET /api/orders/my`
- `POST /api/payments/create-checkout-session`
- `GET /api/payments/success?session_id=...`
- `POST /api/payments/failure/:orderId`
- `POST /api/payments/webhook`
