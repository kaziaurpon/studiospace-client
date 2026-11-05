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
touch .env
```

Add these settings to `server/.env` (replace the MongoDB URI and secret with your own values):

```env
PORT=5001
MONGODB_URI=mongodb://127.0.0.1:27017
MONGODB_DB=studiospace
JWT_SECRET=replace-with-a-random-secret-of-at-least-32-characters
CLIENT_URL=http://localhost:5173
NODE_ENV=development
GOOGLE_CLIENT_ID=your-google-oauth-client-id.apps.googleusercontent.com
```

Google sign-in is optional; use your Google Web OAuth client ID to enable it.

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
touch .env
```

Add these settings to `client/.env`:

```env
VITE_API_URL=http://localhost:5001/api
VITE_IMGBB_API_KEY=your-imgbb-api-key
VITE_GOOGLE_CLIENT_ID=your-google-oauth-client-id.apps.googleusercontent.com
```

Google sign-in and the ImgBB upload key are optional. For Google sign-in, use the matching OAuth client ID and add `http://localhost:5173` to its authorized JavaScript origins.

```bash
npm install
npm run dev
```

Open `http://localhost:5173`.

## Examiner access

Use this dedicated account to review authenticated features on the live website:

- **Email:** `aurafumee@gmail.com`
- **Password:** `AAAaaa`

This account is for assessment only. Do not add personal data or reuse this password on any other service.

## Deployment notes

The client is a Vite single-page app. `vercel.json` rewrites route requests to `index.html`, allowing React Router routes to reload directly. Configure these variables in Vercel:

- `VITE_API_URL`: deployed API origin ending in `/api`.
- `VITE_GOOGLE_CLIENT_ID`: Google Web OAuth client ID (optional if Google sign-in is not used).
- `VITE_IMGBB_API_KEY`: ImgBB upload key (optional).

On the API host, configure `MONGODB_URI`, `JWT_SECRET`, `CLIENT_URL`, and, when using Google sign-in, `GOOGLE_CLIENT_ID`. Keep `.env` files and credentials out of Git.
