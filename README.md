# Multi-Vendor E-commerce Website

A full-stack multi-vendor marketplace built with **Laravel 10**. Vendors sell their own products, customers shop and pay with Stripe or cash on delivery, and admins manage the catalog, orders, content and staff permissions from one dashboard.

<!-- Add 2–3 screenshots here, e.g.:
![Home page](docs/screenshots/home.png)
![Admin dashboard](docs/screenshots/admin.png)
-->

## Features

### Three roles, three dashboards
Access is split by role (`admin`, `vendor`, `user`) with a custom role middleware. Admin staff get finer-grained roles and permissions through `spatie/laravel-permission`.

### Customers
- Browse by category and subcategory, filter on the shop page, live AJAX search and product quick view
- Cart with quantity updates and coupon codes, plus a wishlist and product comparison
- Checkout with shipping address (country → city → region) and payment by **Stripe** or **cash on delivery**
- Order confirmation email and notification, order history, order tracking and **PDF invoices**
- Product reviews, published after admin approval

### Vendors
- Apply to become a vendor; an admin approves or deactivates the account
- Manage their own products: thumbnail and multiple images, activate or deactivate, edit, delete
- See orders and reviews for their products

### Admins
- **Catalog:** brands, categories, subcategories, products and stock
- **Orders:** pending → confirmed → processing → delivered workflow
- **Reports:** orders by date, month, year or customer
- **Marketing and content:** home sliders, banners, coupons and a blog with categories
- **Settings:** shipping areas, site settings and SEO settings
- **People:** customers, vendors, admin users, roles and permissions

## Tech stack

| Layer | Tools |
|---|---|
| Backend | PHP 8.1+, Laravel 10, Eloquent ORM, MySQL |
| Frontend | Blade, Tailwind CSS, Alpine.js, Vite, AJAX (axios) |
| Auth | Laravel Breeze, custom role middleware, spatie/laravel-permission |
| Payments | Stripe |
| Other | DomPDF (invoices), Intervention Image (image resizing), Laravel Mail and Notifications, shopping cart package |

## Getting started

**Requirements:** PHP 8.1+, Composer, Node.js and npm, MySQL.

```bash
git clone https://github.com/hayaokar200/Multi-Vendor-Ecommerce-Website.git
cd Multi-Vendor-Ecommerce-Website

composer install
npm install

cp .env.example .env
php artisan key:generate
```

Edit `.env`:

```env
DB_DATABASE=your_database
DB_USERNAME=your_user
DB_PASSWORD=your_password

# Stripe test keys from https://dashboard.stripe.com/test/apikeys
STRIPE_KEY=pk_test_...
STRIPE_SECRET=sk_test_...

# Any SMTP service works; Mailtrap is handy for local testing
MAIL_HOST=...
MAIL_USERNAME=...
MAIL_PASSWORD=...
```

Create the tables and demo users, then run the app:

```bash
php artisan migrate --seed
npm run dev          # or: npm run build
php artisan serve
```

Open http://127.0.0.1:8000.

### Demo accounts (local only)

| Role | Email | Password | Login page |
|---|---|---|---|
| Admin | admin@hotmail.com | 111 | `/admin/login` |
| Vendor | vendor@hotmail.com | 111 | `/vendor/login` |
| Customer | user@hotmail.com | 111 | `/login` |

These come from `database/seeders/UsersTableSeeder.php`. Change them before deploying anywhere public.

## Project structure

```
app/Http/Controllers/
├── Backend/      # admin: catalog, blog, reports, roles, settings, shipping
├── Frontend/     # home page, product pages, cart
├── User/         # checkout, Stripe and cash orders, reviews
└── ...           # admin, vendor, user, orders, coupons, wishlist, compare
app/Http/Middleware/Role.php   # role-based access
app/Mail, app/Notifications    # order emails and notifications
resources/views/               # admin, vendor, frontend and auth Blade views
routes/web.php                 # all web routes, grouped by role
```

## Author

**Haya Okar** · [LinkedIn](https://www.linkedin.com/in/haya-okar-66766a243/) · [GitHub](https://github.com/hayaokar200)
