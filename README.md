# Sankalp Creative Studio — custom full-stack store

## Run locally

Requires Node.js 20+. No npm dependencies.

macOS/Linux:
```sh
export ADMIN_PASSWORD='choose-a-long-random-password'
export RAZORPAY_KEY_ID='rzp_test_...'
export RAZORPAY_KEY_SECRET='...'
node server.js
```
Windows PowerShell:
```powershell
$env:ADMIN_PASSWORD='choose-a-long-random-password'
$env:RAZORPAY_KEY_ID='rzp_test_...'
$env:RAZORPAY_KEY_SECRET='...'
node server.js
```
Open http://localhost:3000 and http://localhost:3000/admin.html.

## Features

- Responsive custom storefront, categories, search and product customization
- Server-side product catalog and admin dashboard
- Private artwork upload (PNG/JPG/WEBP/PDF up to 5MB)
- Customer checkout with server-calculated order total and Razorpay order creation
- Server-side Razorpay signature verification plus payment lookup
- Bulk enquiry capture and order status management
- Persistent JSON file storage in `data/store.json`

## Important launch checklist

**This is an extensible MVP, not a production-hardened store.** Before taking real payments:

1. Configure production Razorpay credentials and verify the Razorpay account. Test the complete checkout flow in test mode first.
2. Deploy with HTTPS, a process manager, restricted file permissions and a secure secret manager.
3. Replace JSON storage with a transactional database (PostgreSQL), add concurrency protection, backups and migrations.
4. Add verified Razorpay webhooks, reconciliation for interrupted checkouts, idempotency and refund/cancellation workflows. An authorized payment is not always captured; ensure capture status is checked before fulfilment.
5. Replace single-password in-memory admin sessions with a production authentication system, role controls, audit logs, CSRF protection and login rate limiting.
6. Add upload scanning, retention and deletion policies; implement server-side access control to artwork. Uploaded files are not publicly served by this application.
7. Add tax/GST, shipping and pin-code rules, quantity-based pricing, product-specific configuration pricing, invoices, email/SMS notifications, returns/refunds policy, privacy policy and terms.
8. Add actual brand identity, company contact information, product photography, inventory and confirmed prices. Seed prices are illustrative.
9. Add automated tests, observability, monitoring, accessibility and security review.

**Pricing caveat:** The starter uses a product base unit price for checkout. Custom sizes, finishes, artwork and other choices are stored with the order but do **not** alter price. Configure a validated pricing engine or manual-quote workflow before selling options that change costs.

**Payment caveat:** Orders are not automatically recovered when a buyer closes the checkout window. Implement webhooks and reconciliation before launch. Admin status updates are operational controls, not proof of payment.
