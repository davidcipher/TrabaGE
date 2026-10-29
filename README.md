# TrabaGE

Employment PWA for Equatorial Guinea — "Where opportunities find you".

## Stack

- React 19 + Vite
- Tailwind CSS
- Supabase (Auth, DB, Storage)
- Web Push / VAPID (push) · Sentry (errors)

## Setup

```bash
npm install
cp .env.example .env.local
# Edit .env.local with your Supabase credentials
npm run dev
```

## Supabase

```bash
supabase link --project-ref YOUR_REF
supabase db push
supabase functions deploy send_auth_email --no-verify-jwt
supabase functions deploy send_push
supabase functions deploy send_welcome_email
```

### Authentication + welcome emails (Resend)

1. **Resend Dashboard**: verify the domain `trabage.org` and create an API key
2. **Edge Functions → Secrets**: `RESEND_API_KEY`, `RESEND_AUTH_FROM_EMAIL`, `RESEND_WELCOME_FROM_EMAIL`, `RESEND_FROM_NAME`, `SEND_EMAIL_HOOK_SECRET`, `WELCOME_WEBHOOK_SECRET`
3. **Authentication → Hooks → Send Email**: HTTPS → `send_auth_email` function URL → Generate Secret
4. **Database → Webhooks**: `INSERT` on `welcome_email_outbox` → `send_welcome_email`

## Scripts

| Command | Description |
|---------|-------------|
| `npm run dev` | Development server |
| `npm run build` | Production build |
| `npm run preview` | Preview the build |
