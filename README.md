# Ankit AI Caller
Production-oriented MVP for legitimate, consent-aware local-business outreach and appointment booking for Ankit Design Studio in Darbhanga, Bihar.

## Stack
Next.js, TypeScript, React, Tailwind, Supabase Auth/Postgres/RLS, Zod, Lucide. Calling is provider-independent and has a mock provider.

## Run
Node 20+. Copy .env.example to .env.local. Keep DEMO_MODE=true. Run npm install, then npm run dev and open http://localhost:3000.

## Demo mode
Works without paid APIs. Includes fictional Darbhanga leads, dashboard metrics, lead management, simulated AI calls, Hindi/Hinglish transcript, interest/meeting detection, follow-ups, scripts, notifications and compliance UI. Demo calls enforce 09:00–19:00 IST and Do Not Call protection.

## Supabase
Create a project, configure NEXT_PUBLIC_SUPABASE_URL and NEXT_PUBLIC_SUPABASE_ANON_KEY, then run supabase/migrations/001_initial.sql. Use DEMO_MODE=false for production authentication/persistence.

## Real integrations
Calling: configure CALLING_PROVIDER, CALLING_API_KEY, CALLING_API_SECRET and CALLING_PHONE_NUMBER and implement the adapter in lib/calling.ts for a compliant provider. Verify webhook signatures before processing provider events.
AI: keep AI_API_KEY server-side and add a server AI adapter.
Google Calendar: configure GOOGLE_CLIENT_ID, GOOGLE_CLIENT_SECRET and GOOGLE_REDIRECT_URI; local calendar remains available if not connected.
Notifications: add server-side email/WhatsApp providers without exposing secrets.

## Security/compliance
Never expose secrets in NEXT_PUBLIC_ variables. Use Supabase RLS so users only see their data. The system identifies itself as AI, honors opt-outs, blocks Do Not Call leads, enforces configured calling hours and is designed for legitimate outreach, not spam. Confirm applicable Indian telecom/DND/consent requirements and provider rules before live calling.

## Production checklist
Add server-side daily call-rate limiting backed by DB, real AI provider, verified telephony adapter/webhooks, Google OAuth, notification providers, tests and CI. Run npm run typecheck, npm run lint and npm run build before deployment.