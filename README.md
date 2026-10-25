# My Business (my_cart)

Next.js frontend + Express API + MySQL.

## Run locally

The backend creates the `my_platform` database tables automatically and stores users, products, orders, order items, and workflow timestamps in MySQL.

1. Start MySQL and set the values from `.env.example` in your environment. The current defaults are `root`, `rescue1122`, and `my_platform`.
2. Start the API with `npm.cmd run server` (http://localhost:5000, check `/api/health`).
3. Start the frontend in another terminal with `npm.cmd run dev` (http://localhost:3000).

For production: `npm.cmd run build`, then `npm.cmd start`.

## How the frontend is laid out

- `src/app/` - Next.js App Router.
  - `page.jsx` renders the signed-in app (`src/App.jsx`) in the browser only. It keeps its hash routes: `#/home`, `#/shop`, `#/admin/...`.
  - `products/` - public, server-rendered catalogue (`/products`, `/products/<id>`) that search engines can index. "Buy now" links to `/#/shop/<id>`, which opens that product after sign-in.
  - `sitemap.js`, `robots.js` - `/sitemap.xml` and `/robots.txt`.
- `src/screens/` - the customer, retailer, delivery and admin workspaces. (Not named `pages/`, because Next.js would treat that folder as routes.)
- `src/lib/catalog.js` - server-side reads from the Express API for the public pages.

## Environment

| Variable | Used by | Default |
|---|---|---|
| `NEXT_PUBLIC_API_URL` | browser -> API | `http://<host>:5000/api` |
| `API_URL` | Next.js server -> API | `http://localhost:5000/api` |
| `SITE_URL` | sitemap, canonical links, share previews | `http://localhost:3000` |
