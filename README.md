# 🌞 SuunyMart — Summer eCommerce Platform

<p align="center">
  <img src="https://img.shields.io/badge/Next.js-16-black?style=for-the-badge&logo=next.js" alt="Next.js" />
  <img src="https://img.shields.io/badge/React-19-61DAFB?style=for-the-badge&logo=react&logoColor=black" alt="React" />
  <img src="https://img.shields.io/badge/TailwindCSS-4-38B2AC?style=for-the-badge&logo=tailwind-css&logoColor=white" alt="TailwindCSS" />
  <img src="https://img.shields.io/badge/DaisyUI-5-5A0EF8?style=for-the-badge" alt="DaisyUI" />
  <img src="https://img.shields.io/badge/BetterAuth-1.6-FF6F00?style=for-the-badge" alt="BetterAuth" />
  <img src="https://img.shields.io/badge/MongoDB-Atlas-47A248?style=for-the-badge&logo=mongodb&logoColor=white" alt="MongoDB" />
  <img src="https://img.shields.io/badge/Vercel-Deployed-000000?style=for-the-badge&logo=vercel" alt="Vercel" />
</p>

<p align="center">
  <a href="https://suunymart-orpin.vercel.app/"><img src="https://img.shields.io/badge/🌐%20Live%20Site-Visit%20Now-success?style=for-the-badge" alt="Live site" /></a>
  <a href="https://github.com/shihab-5/suunymart"><img src="https://img.shields.io/badge/📂%20Repository-View%20Code-blue?style=for-the-badge" alt="Repo" /></a>
</p>

---

## 📌 Project Name

**SuunyMart** — a modern summer-themed eCommerce platform.

## 🎯 Purpose

SuunyMart lets users explore and purchase seasonal products such as sunglasses, summer outfits, skincare, and beach accessories. Visitors can browse the catalog, view popular picks, read product details, and place orders **after authentication**. The project demonstrates a clean Next.js App Router setup with server-side session checks, route protection via Next.js middleware, and a full BetterAuth (email/password + Google) authentication flow backed by MongoDB.

## 🌐 Live URL

- **Production:** https://suunymart-orpin.vercel.app/
- **Repository:** https://github.com/shihab-5/suunymart

---

## ✨ Key Features

### 🧭 Navigation & Layout
- Persistent **Navbar + Footer** wrapping every route via the App Router root layout (`src/app/layout.js`).
- Dynamic Navbar:
  - **Logged out:** Login button.
  - **Logged in:** User avatar, greeting, and Logout button.
- Mobile-friendly responsive menu using DaisyUI dropdown.

### 🏠 Home Page (`/`)
- 🌅 **Hero banner** highlighting the summer sale.
- 🔥 **Popular Products** — pulls the first 3 products from `data.json` and renders them as cards with image, name, rating, price, and a *View Details* button.
- 💡 **Summer Care Tips** section.
- 🏷 **Top Brands** section.
- ✨ Lightweight CSS animations powered by `animate.css`.

### 📦 Products
- All products listed at **`/products`** (publicly accessible, fetched at request time from `data.json`).
- Product cards show image, name, rating, price, and a *View Details* CTA.
- Static product data lives in `public/data.json`.

### 🔒 Protected Product Details (`/products/[id]`)
- Implemented via **Next.js middleware** (`src/middleware.js`) that calls `auth.api.getSession()` from BetterAuth.
- Unauthenticated visitors are redirected to `/login`.
- Matcher protects `/profile` and `/products/<id>` (the `[id]` slug) **without** blocking the public `/products` listing.

### 🔐 Authentication (BetterAuth + MongoDB)
- **Email + Password** login & registration.
- **Google OAuth** (Sign in / Sign up with Google).
- Session-aware UI on both server and client:
  - Server components use `auth.api.getSession({ headers: await headers() })`.
  - Client components use `authClient.useSession()` from `better-auth/react`.
- Auth handler mounted at `src/app/api/auth/[...all]/route.js` via `toNextJsHandler(auth)`.
- MongoDB session/user persistence via `@better-auth/mongo-adapter`.

### 👤 Profile (`/profile`) — Protected
- Displays the logged-in user's avatar, name, and email.
- **Edit Profile** modal (DaisyUI dialog) for updating **name** and **profile image URL** using `authClient.updateUser()` (per the [BetterAuth Update User docs](https://better-auth.com/docs/concepts/users-accounts#update-user)).

### 🎨 UI / UX
- Tailwind CSS v4 + DaisyUI v5 for styling and components.
- Fully responsive across mobile, tablet, and desktop breakpoints.
- React Icons (`react-icons`) for consistent iconography.
- Lightweight entrance animations via `animate.css`.

---

## 🛠 Tech Stack

| Layer            | Technology                                    |
| ---------------- | --------------------------------------------- |
| Framework        | **Next.js 16** (App Router)                   |
| UI Library       | **React 19**                                  |
| Styling          | **Tailwind CSS v4**                           |
| Components       | **DaisyUI v5**                                |
| Authentication   | **BetterAuth** + **@better-auth/mongo-adapter** |
| Database         | **MongoDB** (Atlas-compatible)                |
| Forms            | **react-hook-form**                           |
| Icons            | **react-icons**                               |
| Animations       | **animate.css**                               |
| Marquee          | **react-fast-marquee**                        |
| Deployment       | **Vercel**                                    |

---

## 📦 NPM Packages

All packages are pinned in [`package.json`](./package.json).

### Runtime dependencies
| Package                       | Purpose                                          |
| ----------------------------- | ------------------------------------------------ |
| `next`                        | React framework with App Router & middleware     |
| `react`, `react-dom`          | UI runtime                                       |
| `better-auth`                 | Authentication (email/password + Google OAuth)   |
| `@better-auth/mongo-adapter`  | MongoDB adapter for BetterAuth                   |
| `mongodb`                     | Official MongoDB Node.js driver                  |
| `react-hook-form`             | Form state management & validation               |
| `react-icons`                 | Icon set (`FaStar`, `FaEdit`, etc.)              |
| `react-fast-marquee`          | Scrolling marquee for brand/banner sections      |
| `animate.css`                 | Drop-in CSS animation classes                    |

### Dev dependencies
| Package                | Purpose                            |
| ---------------------- | ---------------------------------- |
| `tailwindcss`          | Utility-first CSS                  |
| `@tailwindcss/postcss` | PostCSS plugin for Tailwind v4     |
| `daisyui`              | Component library on top of Tailwind |
| `eslint`               | Linting                            |
| `eslint-config-next`   | Next.js ESLint preset              |

---

## 📂 Folder Structure

```
suunymart/
├── public/
│   ├── data.json              # Static product catalog (6+ products)
│   ├── banner.png
│   ├── logo.png
│   └── *.svg
├── src/
│   ├── middleware.js          # Route protection (BetterAuth session check)
│   ├── lib/
│   │   ├── auth.js            # BetterAuth server config (Mongo + Google)
│   │   └── auth-client.js     # BetterAuth React client (useSession, signIn…)
│   ├── component/
│   │   ├── nav.jsx            # Top navbar (auth-aware)
│   │   ├── footer.jsx
│   │   ├── Navlink.jsx        # Active-aware nav link
│   │   ├── Popular.jsx        # Home: top 3 popular products
│   │   ├── Tips.jsx           # Home: summer care tips
│   │   ├── Top-brands.jsx     # Home: featured brands
│   │   └── Update.jsx         # Profile update modal
│   └── app/
│       ├── layout.js          # Root layout (Nav + Footer wrapper)
│       ├── page.jsx           # Home (/)
│       ├── loading.jsx        # Global loading UI
│       ├── not-found.jsx      # 404 page
│       ├── login/page.jsx     # /login
│       ├── register/page.jsx  # /register
│       ├── profile/page.jsx   # /profile (protected)
│       ├── products/
│       │   ├── page.jsx       # /products (public listing)
│       │   └── [id]/page.jsx  # /products/[id] (protected detail)
│       └── api/
│           └── auth/[...all]/route.js  # BetterAuth Next.js handler
├── eslint.config.mjs
├── next.config.mjs
├── postcss.config.mjs
├── tailwind.config.mjs
├── jsconfig.json
└── package.json
```

---

## 🛡 Route Protection (Middleware)

`src/middleware.js` runs on every request that matches `config.matcher`. It calls BetterAuth's `auth.api.getSession()` with the incoming request headers:

- If a session exists → `NextResponse.next()` (request continues).
- If no session → `NextResponse.redirect('/login')`.

```js
// src/middleware.js
export const config = {
  matcher: ["/profile", "/products/:id+"],
};
```

The matcher uses `/products/:id+` (one-or-more path segments) so:

| Route              | Protected? |
| ------------------ | ---------- |
| `/`                | ❌ public |
| `/products`        | ❌ public (listing stays open) |
| `/products/123`    | ✅ protected (the `[id]` slug detail) |
| `/profile`         | ✅ protected |
| `/login`, `/register` | ❌ public |

> ⚠️ **Important:** Next.js only recognizes a file named `middleware.{js,ts}` at the project (or `src/`) root, exporting a function literally named `middleware` (or `default`). Any other name silently becomes dead code.

---

## ⚙️ Local Development

### Prerequisites
- Node.js 18.18+ (Next.js 16 recommends Node 20+)
- A MongoDB connection string (Atlas or local)
- Google OAuth client credentials (for the “Continue with Google” button)

### Install & run

```bash
git clone https://github.com/shihab-5/suunymart.git
cd suunymart
npm install
npm run dev
```

The app starts on http://localhost:3000.

### Available scripts
| Command          | Description                          |
| ---------------- | ------------------------------------ |
| `npm run dev`    | Start the Next.js dev server         |
| `npm run build`  | Production build                     |
| `npm start`      | Run the production build             |
| `npm run lint`   | ESLint check                         |

---

## 🔐 Environment Variables

Create a `.env.local` file in the project root:

```bash
# MongoDB
MONGODB_URI="mongodb+srv://<user>:<pass>@<cluster>/?retryWrites=true&w=majority"

# BetterAuth — base URL of *this* app (used by the React client)
BETTER_AUTH_URL="http://localhost:3000"        # production: https://suunymart-orpin.vercel.app
BETTER_AUTH_SECRET="generate-a-long-random-string"

# Google OAuth
GOOGLE_CLIENT_ID="your-google-client-id"
GOOGLE_CLIENT_SECRET="your-google-client-secret"
```

Add these same variables in your Vercel project settings for production. The Google OAuth redirect URI must include:

```
https://<your-domain>/api/auth/callback/google
```

---

## 🧪 Manual Test Plan

1. **Public browsing** — visit `/` and `/products` while logged out; both should render.
2. **Protected slug** — while logged out, visit `/products/1` → should redirect to `/login`.
3. **Profile** — while logged out, visit `/profile` → should redirect to `/login`.
4. **Email register** — create an account at `/register`; you should land back on `/`.
5. **Email login** — log in at `/login`; the navbar should show your avatar and name.
6. **Google login** — click *Login with Google*; after the OAuth redirect you should be authenticated.
7. **Detail page (logged in)** — visit `/products/1` → full product details render.
8. **Profile update** — open *Edit Profile*, change name + image URL, submit, and verify the updated values on `/profile`.
9. **Logout** — click Logout; visiting `/profile` again should redirect to `/login`.

---

## 🌟 Future Improvements

- 🛒 Cart & checkout flow
- 💳 Payment gateway (Stripe / SSLCommerz)
- 🔍 Search, filtering, and category pages
- ⭐ Real reviews & ratings stored in MongoDB
- 📦 Order history per user

---

## 👨‍💻 Author

**Shihab Ul Islam** — CSE Student, building toward an ML engineering career.

---

## ⭐ Support

If you find this project useful:

- ⭐ Star the repo
- 🐛 Open issues for bugs / ideas
- 🍴 Fork & build your own version

<p align="center">🔥 Built with Next.js, BetterAuth, and a love for clean UI 🔥</p>
