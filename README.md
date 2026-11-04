# StudioSpace

**StudioSpace** is a creative-space marketplace where filmmakers, photographers, musicians, and other creators can discover and book studios, while hosts can list and manage their spaces.

## Live website

[Open StudioSpace](https://studiospace-client-seven.vercel.app)

## Highlights

- Browse and search studio listings by category, location, and price.
- View studio photos, amenities, host details, ratings, and guest reviews.
- Create an account with email/password or Google sign-in.
- Add, update, and delete studio listings with host ownership checks.
- Request bookings, track booking status, and cancel pending requests.
- Save favorite studios to a MongoDB-backed wishlist.
- Download an invoice for a confirmed booking.
- Switch between light and dark themes; layouts adapt to mobile and desktop.

## Technology

- **Frontend:** React, Vite, React Router, JavaScript, and CSS
- **UI and interactions:** Lucide icons, Swiper, and Sonner
- **PDF invoices:** jsPDF
- **API:** Express.js and MongoDB (see the [server README](https://github.com/kaziaurpon/studiospace-server#readme))
- **Authentication:** JWT in HTTPOnly cookies, with Google Identity Services support
- **Hosting:** Vercel for the client; the API can be hosted on Render

## Run locally

Clone both repositories into the same parent directory so the relative paths below work:

```bash
git clone https://github.com/kaziaurpon/studiospace-client.git
git clone https://github.com/kaziaurpon/studiospace-server.git
```

### 1. Start the API

```bash
cd ../studiospace-server
cp .env.example .env
```

Set `MONGODB_URI` and a random `JWT_SECRET` of at least 32 characters in `server/.env`. Set `CLIENT_URL=http://localhost:5173`. To enable Google sign-in locally, set `GOOGLE_CLIENT_ID` to your Google Web OAuth client ID.

Then install dependencies and start the API:

```bash
npm install
npm run dev
```

The API runs at `http://localhost:5001` by default.

### 2. Start the client

In a second terminal:

```bash
cd ../studiospace-client
cp .env.example .env
```

Set `VITE_API_URL=http://localhost:5001/api`. For Google sign-in, set the matching `VITE_GOOGLE_CLIENT_ID`; add `http://localhost:5173` to the OAuth client's authorized JavaScript origins. `VITE_IMGBB_API_KEY` is optional and enables direct studio-image uploads.

```bash
npm install
npm run dev
```

Open `http://localhost:5173`.

## Examiner access

A dedicated examiner account has **not** been provisioned. Use **Register** on the live website to create an account and test authenticated features. Do not use real personal information for assessment.

## Deployment notes

The client is a Vite single-page app. `vercel.json` rewrites route requests to `index.html`, allowing React Router routes to reload directly. Configure these variables in Vercel:

- `VITE_API_URL`: deployed API origin ending in `/api`.
- `VITE_GOOGLE_CLIENT_ID`: Google Web OAuth client ID (optional if Google sign-in is not used).
- `VITE_IMGBB_API_KEY`: ImgBB upload key (optional).

On the API host, configure `MONGODB_URI`, `JWT_SECRET`, `CLIENT_URL`, and, when using Google sign-in, `GOOGLE_CLIENT_ID`. Keep `.env` files and credentials out of Git.
