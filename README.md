# Event Management System v4 - Docker, Background Jobs, Stripe Webhooks

This v4 includes everything from v3 plus:
- Dockerfiles for backend and frontend.
- docker-compose to run Postgres + Redis + Backend + Frontend.
- Background job processing with Bull + Redis for notifications and ticket generation.
- Stripe webhook handler that updates transactions/registrations and enqueues ticket generation jobs.
- Worker process runs inside backend container automatically when backend starts (single process model).

## Quick start (development)
Create a `.env` file in `backend/` (or set env vars) with at least:
```
JWT_SECRET=change_this_jwt_secret
ADMIN_SEED_EMAIL=admin@example.com
ADMIN_SEED_PASSWORD=ChangeMe123!
EMAIL_FROM=no-reply@example.com
SENDGRID_API_KEY=your_sendgrid_key_if_any
STRIPE_SECRET_KEY=your_stripe_key_if_any
STRIPE_WEBHOOK_SECRET=your_stripe_webhook_secret_if_any
```
Then from project root:
```bash
docker-compose up --build
```
- Backend: http://localhost:4000
- Frontend: http://localhost:5173 (served by nginx in container)

Notes:
- In production you should run worker as a separate process/replica. This scaffold runs worker inside backend for simplicity.
- Ensure you set real secrets and configure Stripe webhook URL to `http://<your-host>/api/payments/webhook` and set `STRIPE_WEBHOOK_SECRET` accordingly.

