# StudioSpace

**A creative-space marketplace for people who make things.** StudioSpace connects filmmakers, photographers, podcasters, musicians, and other creators with production-ready spaces listed by independent hosts.

**Live website:** [studiospace-client-seven.vercel.app](https://studiospace-client-seven.vercel.app)
**Client repository:** [github.com/kaziaurpon/studiospace-client](https://github.com/kaziaurpon/studiospace-client)
**API repository:** [github.com/kaziaurpon/studiospace-server](https://github.com/kaziaurpon/studiospace-server)

## Product highlights

- Browse studios for photography, film, podcasts, music, and art workshops.
- Search listings and filter by category; open each listing for its images, host details, amenities, capacity, and pricing.
- Register or sign in with email and password, or use Google sign-in when OAuth is configured.
- Create, update, and remove studio listings, with host information attached to each listing.
- Submit booking requests with a date, time range, crew size, and production notes.
- Track booking status, cancel pending requests, and download a booking receipt as a PDF.
- Prevent confirmed time-slot conflicts and let hosts review, confirm, or complete booking requests.
- Save studios to a personal wishlist and leave reviews for visited spaces.
- Use the app on mobile or desktop, with light and dark themes.

## Technology

- **Frontend:** React, JavaScript, Vite, React Router
- **Styling and UI:** Custom CSS, Lucide React, Swiper, Sonner
- **PDF receipts:** jsPDF
- **Authentication:** JWT sessions in HTTPOnly cookies; Google Identity Services support
- **Backend and data:** Express.js API with MongoDB — see the [server README](https://github.com/kaziaurpon/studiospace-server#readme)
- **Hosting:** Vercel for the client; the API is configured separately

## Run locally

### Prerequisites

- Node.js and npm
- MongoDB running locally or a MongoDB Atlas connection string
- Google OAuth credentials only if you want to enable Google sign-in

Clone both repositories into the same parent folder:

```bash
git clone https://github.com/kaziaurpon/studiospace-client.git
git clone https://github.com/kaziaurpon/studiospace-server.git
```

### 1. Configure and start the API

In a terminal:

```bash
cd studiospace-server
touch .env
```

Add the following to `studiospace-server/.env`, replacing the MongoDB URI and JWT secret with your own values:

```env
PORT=5001
MONGODB_URI=mongodb://127.0.0.1:27017
MONGODB_DB=studiospace
JWT_SECRET=replace-with-a-random-secret-of-at-least-32-characters
CLIENT_URL=http://localhost:5173
NODE_ENV=development
GOOGLE_CLIENT_ID=your-google-oauth-client-id.apps.googleusercontent.com
```

Then install dependencies and start the API:

```bash
npm install
npm run dev
```

The API runs at `http://localhost:5001` by default.

### 2. Configure and start the client

Open a second terminal:

```bash
cd studiospace-client
touch .env
```

Add the following to `studiospace-client/.env`:

```env
VITE_API_URL=http://localhost:5001/api
VITE_IMGBB_API_KEY=your-imgbb-api-key
VITE_GOOGLE_CLIENT_ID=your-google-oauth-client-id.apps.googleusercontent.com
```

`VITE_IMGBB_API_KEY` and Google sign-in are optional. For Google sign-in, use the same OAuth client ID on client and server and authorize `http://localhost:5173` in Google Cloud Console.

Start the client:

```bash
npm install
npm run dev
```

Open [http://localhost:5173](http://localhost:5173). Keep `.env` private; it is excluded from Git.

## Examiner test account

Use this account to review signed-in features on the live website:

- **Email:** `aurafumee@gmail.com`
- **Password:** `AAAaaa`

The account is provided for project assessment. Please do not change its credentials or add personal information.

## Deployment

The client is deployed on Vercel. Its `vercel.json` rewrite supports direct loading and refresh on React Router routes. Configure these variables in the Vercel project settings:

- `VITE_API_URL` — deployed API URL ending in `/api`.
- `VITE_GOOGLE_CLIENT_ID` — optional Google Web OAuth client ID.
- `VITE_IMGBB_API_KEY` — optional ImgBB upload key.

Configure `MONGODB_URI`, `JWT_SECRET`, `CLIENT_URL`, and optionally `GOOGLE_CLIENT_ID` in the API host settings. See the [server deployment notes](https://github.com/kaziaurpon/studiospace-server#deploy-on-render).
