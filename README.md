# GlobalSent backend

This bundle contains the uploaded `server.js`, a Node package manifest, and a Render Blueprint.

## Deploy prerequisites
- A PostgreSQL database and its connection string.
- Access to the GitHub repository and Render account.

## Deploy
1. Upload these files to the root of `nmjeeva34-spec/globalsent-backend` (replace `server.js` only if you intend to use the uploaded version).
2. In Render, create a Blueprint from this repository or create a Node Web Service.
3. Configure `DATABASE_URL` privately in Render. Do not put secrets in GitHub or send them in chat.
4. Ensure `ALLOWED_ORIGINS` matches the exact deployed frontend origin.
5. After deploy, visit `/api/health`; success requires `{"ok":true,"service":"globalsent-auth","database":"connected","realPaymentsEnabled":false}`.

## Important
This backend implements signup/signin and `/api/auth/me`; it does not implement email verification or real payments.
The frontend must use the deployed backend URL (not `localhost`) for API calls.
