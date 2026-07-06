# Flowtive — deploy guide (Vercel)

This folder has everything you need:
- `index.html` — the site
- `api/chat.js` — a secure serverless function that talks to Anthropic on your behalf
- `package.json` — lets Vercel recognize the project

Your Anthropic API key never touches the browser. It only lives on Vercel's server, in an environment variable.

## 1. Get an Anthropic API key
Go to https://console.anthropic.com → API Keys → Create Key. Copy it (starts with `sk-ant-...`).

## 2. Create a free Vercel account
Go to https://vercel.com and sign up (GitHub login is easiest).

## 3. Deploy this folder
Easiest path — no command line needed:
1. Create a new GitHub repository and upload this whole folder to it (drag and drop on github.com works fine).
2. In Vercel, click **Add New → Project**, and import that GitHub repo.
3. Vercel will auto-detect it. Click **Deploy**.

(If you prefer the command line instead: install the Vercel CLI with `npm i -g vercel`, then run `vercel` from inside this folder and follow the prompts.)

## 4. Add your API key as an environment variable
1. In your Vercel project, go to **Settings → Environment Variables**.
2. Add a new variable:
   - Name: `ANTHROPIC_API_KEY`
   - Value: your key from step 1
3. Redeploy the project (Vercel → Deployments → click the "..." on the latest one → Redeploy) so it picks up the new variable.

## 5. Done
Visit the live URL Vercel gives you (something like `flowtive.vercel.app`). The "Try it yourself" box in the demo section will now call your own backend, which securely calls Anthropic using your key.

## Notes
- You can later connect a custom domain (like `flowtive.com`) under **Settings → Domains** in Vercel — free, just point your DNS at it.
- If the try-it box ever shows a connection error, check **Vercel → Deployments → Functions logs** for `api/chat.js` — it will tell you exactly what went wrong (usually a missing or incorrect API key).
