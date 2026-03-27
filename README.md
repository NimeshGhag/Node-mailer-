# Node Mailer — Gmail OAuth2 Only

This project sends email using Gmail via OAuth2 only. The codebase is configured to obtain an OAuth2 access token and send mail with Nodemailer. Do not attempt to use plain SMTP credentials with this repository.

**Files:**

- [app.js](app.js) — example usage / entry point
- [email.js](email.js) — Gmail OAuth2 mail helper (creates access token and sends email)

**Prerequisites:**

- Node.js v14+ installed
- A Google Cloud OAuth 2.0 client (OAuth client ID + client secret)
- A refresh token for the sending Gmail account (see steps below)

**Required environment variables** (create a `.env` file at the project root):

- `EMAIL_USER` — sender Gmail address (e.g., you@gmail.com)
- `CLIENT_ID` — Google OAuth2 client ID
- `CLIENT_SECRET` — Google OAuth2 client secret
- `REFRESH_TOKEN` — OAuth2 refresh token for the sending account

Example `.env` (do not commit):

```
EMAIL_USER=you@gmail.com
CLIENT_ID=your-google-client-id
CLIENT_SECRET=your-google-client-secret
REFRESH_TOKEN=your-refresh-token
```

How to obtain a refresh token (brief):

- Create OAuth 2.0 credentials in Google Cloud Console (type: "Desktop app" or "Web application").
- Use the Google OAuth Playground or your own OAuth flow to request scopes `https://mail.google.com/` and obtain a refresh token for `EMAIL_USER`.

**Install dependencies**

```bash
npm install
```

If you add or update dependencies later, run `npm install` again. This project uses `nodemailer` and `googleapis` for OAuth2 token generation.

**Run**

```bash
node app.js
```

`app.js` triggers a test send via `email.js`. If the environment variables are set correctly the script will obtain an access token and send the message.

**Notes & troubleshooting**

- This repository is intentionally Gmail OAuth2-only. Do not try to use SMTP username/password; `email.js` expects `CLIENT_ID`, `CLIENT_SECRET`, `REFRESH_TOKEN`, and `EMAIL_USER`.
- If you see authentication errors, confirm the refresh token is valid and that the OAuth client and `EMAIL_USER` match the account used to generate the token.
- For local testing, the Google OAuth Playground is a quick way to exchange consent for a refresh token.

If you want, I can also add a `.env.example` file and update `package.json` to include `googleapis` explicitly. What would you like next?
