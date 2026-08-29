# VTU Complete — Next.js 14 + Supabase + Paystack + VTpass Sandbox

## Deploy
1. Create a Supabase project.
2. Run `supabase/schema.sql` in Supabase SQL Editor.
3. Create a Supabase Auth user for yourself and copy its UUID into the final `admin_users` SQL statement.
4. Create a Paystack test account/key and configure the webhook URL as `https://YOUR-VERCEL-DOMAIN/api/wallet/verify`.
5. Get VTpass Sandbox credentials.
6. Copy `.env.example` to `.env.local` for local development or add the same variables in Vercel.
7. Deploy the repository to Vercel. Vercel Cron calls `/api/cron/verify-pending` every 5 minutes in production.

## Required environment variables
- SUPABASE_URL
- SUPABASE_SERVICE_KEY
- VTPASS_API_KEY
- VTPASS_SECRET_KEY
- PAYSTACK_SECRET_KEY
- APP_URL
- CRON_SECRET

`SUPABASE_SERVICE_KEY` is server-only and must never be put in client code.

## Admin
After signing up, get the user's UUID from Supabase Authentication > Users, then run:

```sql
insert into public.admin_users(user_id) values('YOUR-USER-UUID');
```

Then open `/admin` after logging in.

## Important
VTpass is configured to `https://sandbox.vtpass.com/api`. Change the base URL in `lib/vtpass.ts` only when moving to VTpass Live and use Live credentials.

Paystack webhook signature is validated before crediting a wallet. Wallet debits and refunds are performed by PostgreSQL functions with row locks so simultaneous purchases cannot spend the same balance twice.

## eeodata business details
- App name: eeodata
- WhatsApp: +2349072428695
- Email: eeodata@gmail.com
- App icon: `app/icon.png` / `public/eeodata-icon.png`
