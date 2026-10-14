# SC MART Working MVP

## Run on your computer
Requirements: Node.js 20+ and npm.
1. Extract this ZIP.
2. Copy `.env.example` to `.env`.
3. Change `JWT_SECRET` to a long random secret (32+ characters). Set a private `ADMIN_EMAIL` and `ADMIN_PASSWORD` (at least 12 characters).
4. In the extracted folder run `npm install` then `npm start`.
5. Open http://localhost:3000.

The first run creates the Super Admin account from `.env`. Keep these credentials private. SQLite data is stored in `data/scmart.db`.

## Features implemented
- Town-filtered shop/product listings, category filters and search
- Customer, Shop Owner and Rider registration with hashed passwords
- JWT sessions, server-side role checks and basic login rate limiting
- Shop/Rider registration pending Admin approval
- Admin application approve/reject and overview dashboard
- Approved Shop Owners can add products
- Customer COD checkout, stock checks and stock deduction
- Orders containing products from different shops split into separate shop orders
- Role-filtered order lists
- SQLite database and audit logs

## Not ready for public launch yet
- Phone OTP/SMS and email verification are not connected; login uses a password with email or phone identifier.
- Online payment gateway is intentionally disabled until a Sri Lankan provider is chosen and server-side verification/webhooks are implemented.
- Rider assignment/status workflow, delivery fees, verified zone polygons, email/SMS notifications, password reset, refunds, image uploads, backups, monitoring, privacy/terms and a security review remain to be implemented.
- Demo products are in one clearly labelled demo shop in Gelioya. Remove before launch.
- Town filtering uses shop town, not a verified delivery-zone map.
- Production needs HTTPS, managed hosting/database, secret management, restricted CORS, backups, and testing.

## Main API
`GET /api/health`, `/api/towns`, `/api/products`, `/api/shops`
`POST /api/auth/register`, `/api/auth/login`; `GET /api/me`
`POST /api/products` (approved shop owner)
`POST /api/orders` (customer; COD)
`GET /api/orders` (role-filtered)
`GET /api/admin/applications`, `POST /api/admin/applications/:id/decision`, `GET /api/admin/overview`

Protected endpoints require `Authorization: Bearer <token>`.
