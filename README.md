# GlobalSent authentication backend starter

This deployable starter implements signup, signin, a health check, and `/api/auth/me`.
It uses PostgreSQL, bcrypt password hashes, short-lived JWTs, Helmet, CORS, and auth rate limiting.

## Important limitations
- This is a starter, not a production-reviewed financial-services backend.
- Email verification, SMS OTP, password reset, MFA, KYC, admin authorization, and payments are NOT implemented here.
- Real-money payments remain disabled.
- Use HTTPS, keep secrets in the hosting provider's environment settings, and complete a security/privacy review before public launch.
- Do not commit `.env` or send passwords, database URLs, or JWT secrets in chat.

## Deploy from an Android phone (high-level)
1. Create a private GitHub repository and upload these files.
2. Create a PostgreSQL database with a managed provider such as Supabase. Copy its connection string privately.
3. Create a web service on Render from the GitHub repository.
4. Runtime: Node. Build command: `npm install`. Start command: `npm start`.
5. Add environment variables in Render:
   - `DATABASE_URL` = managed PostgreSQL connection string
   - `DATABASE_SSL` = `true`
   - `JWT_SECRET` = a long random secret (at least 32 characters)
   - `ALLOWED_ORIGINS` = the website origin where GlobalSent HTML will be hosted (for local `content://` HTML, browser CORS behavior can be inconsistent; host the HTML on HTTPS too)
6. Deploy. Open `https://YOUR-SERVICE.onrender.com/api/health`; expect JSON with `"ok": true`.
7. In GlobalSent, set **Account Verification → Backend API URL** to `https://YOUR-SERVICE.onrender.com` (no trailing slash), then use the API health check and test signup/signin.
8. Host the HTML on HTTPS (for example a static hosting service) and set `ALLOWED_ORIGINS` to that exact origin. Redeploy if environment settings change.

## Test payloads
Signup: `POST /api/auth/signup`
`{"name":"Test User","email":"test@example.com","password":"a-long-unique-password"}`

Signin: `POST /api/auth/signin`
`{"email":"test@example.com","password":"a-long-unique-password"}`

Never use a real personal password for testing.
