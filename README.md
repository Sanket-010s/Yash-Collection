# Yash Clothing — Custom T-Shirt Brand Platform

Mobile-first D2C e-commerce platform for buying and designing custom T-shirts.

## Project Structure

```
/
├── store/          # Customer storefront (Next.js 14, JavaScript)
├── admin/          # Admin panel (React + Vite, Tailwind CSS)
├── backend/        # API server (FastAPI, SQLAlchemy, async)
└── Documentation/
```

---

## Features

### Customer Store (`store/`)

**Pages**
- `/` — Home / landing
- `/shop` — Product listing with browse/filter
- `/product/[id]` — Product detail
- `/customize` — T-shirt canvas editor (Fabric.js)
- `/cart` — Shopping cart
- `/checkout` — Address + payment flow
- `/orders` — Order history
- `/wishlist` — Saved products
- `/profile` — Account details
- `/auth/login` & `/auth/register` — Auth

**Capabilities**
- Guest and logged-in checkout
- Persistent cart via Zustand
- Wishlist management
- Design draft saved in state
- Razorpay payment integration
- Invoice download after order
- Responsive with bottom navigation on mobile

---

### Admin Panel (`admin/`)

**Pages**
- `/` — Dashboard with live stats
- `/products` — Product listing
- `/products/add` & `/products/:id/edit` — Add / edit products with variant manager and image uploader
- `/orders` — Order listing with status/date filters and pagination
- `/orders/:id` — Full order detail (items, address, payment, invoice)
- `/invoices` — Invoice listing and download
- `/coupons` — Coupon management (create, toggle, delete)
- `/login` — Admin authentication

**Capabilities**
- JWT-protected routes (admin role required)
- Dashboard stats: orders today, revenue today, revenue this month, pending orders, low-stock variants
- Update order status
- Manage product variants (size, color, stock, price)
- Cloudinary image upload
- Mobile-friendly with sidebar + bottom nav

---

### Backend API (`backend/`)

**Auth** — `POST /api/auth/register`, `POST /api/auth/login`, `GET /api/auth/me`

**Products** — `GET /api/products`, `GET /api/products/{id}`

**Cart** — `GET /api/cart`, `POST /api/cart`, `DELETE /api/cart/{item_id}`

**Orders** — `POST /api/orders`, `GET /api/orders`, `GET /api/orders/{id}`

**Payment** — `POST /api/payment/create`, `POST /api/payment/verify` (Razorpay)

**Invoices** — `GET /api/invoices/{order_id}` (PDF generation via ReportLab)

**Addresses** — `GET/POST/PUT/DELETE /api/addresses`

**Wishlist** — `GET/POST/DELETE /api/wishlist`

**Designs** — `GET/POST /api/designs` (saved canvas designs)

**Coupons** — `GET/POST/PUT/DELETE /api/coupons` (admin)

**Admin** — `GET /api/admin/orders`, `GET /api/admin/orders/{id}`, `PUT /api/admin/orders/{id}/status`, `GET /api/admin/stats`

**Other**
- SQLite (dev) / PostgreSQL (prod) via SQLAlchemy async
- Alembic migrations
- Auto-seed sample products on first run
- Cloudinary for image storage
- Email service (order confirmation)
- Pricing service (variant-based calculation)

---

## Local Setup

### Backend

```bash
cd backend
python -m venv venv
venv\Scripts\activate
pip install -r requirements.txt
copy .env.example .env
uvicorn main:app --reload
```

Runs at `http://localhost:8000` — API docs at `/docs`

### Store

```bash
cd store
npm install
copy .env.example .env.local
npm run dev
```

Runs at `http://localhost:3000`

### Admin

```bash
cd admin
npm install
copy .env.example .env
npm run dev
```

Runs at `http://localhost:5173`

---

## Status & Known Limitations

- Payment verification uses Razorpay — requires live keys for real transactions.
- Invoice PDFs are generated server-side and stored in `backend/tmp_invoices/`.
- Email sending requires SMTP credentials in `.env`.
- Admin authentication uses a static admin flag on the user model (no separate admin creation UI yet).

## Next Build Targets

1. Admin user management (create/deactivate accounts).
2. Analytics charts on dashboard.
3. Push notifications for order status updates.
4. Tests for auth, products, and order creation.
