# StudioSpace Client

React + Vite frontend for the StudioSpace creative-studio marketplace.

## Local setup

1. Copy `.env.example` to `.env`.
2. Set `VITE_API_URL=http://localhost:5001/api`.
3. Add `VITE_GOOGLE_CLIENT_ID` from the Google Cloud Web OAuth client. Add the current local Vite origin (for example `http://localhost:5173`) to that OAuth client's Authorized JavaScript origins.
4. Optionally set `VITE_IMGBB_API_KEY` for direct image uploads.
5. Run `npm install` and `npm run dev`.

Keep `.env` private; never commit it. The client uses the Express API with credentialed HTTP-only session cookies.

## Vercel deployment

Import this repository into Vercel. The Vite build command is `npm run build`, and the output directory is `dist`. `vercel.json` rewrites deep links to `index.html` for React Router.

Set these Vercel environment variables for Production, Preview, and Development as needed:

- `VITE_API_URL`: the deployed Render API URL ending in `/api`.
- `VITE_GOOGLE_CLIENT_ID`: the Google Web OAuth client ID.
- `VITE_IMGBB_API_KEY`: optional public upload key.

After deployment, add the Vercel site origin to the OAuth client's Authorized JavaScript origins. Set the exact Vercel origin as the Render service's `CLIENT_URL` so CORS and session cookies work.

## Live app

To be added after deployment.
