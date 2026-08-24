# Staging preview channel — Google sign-in

**Symptom:** Google login fails on Firebase Hosting preview URLs like  
`https://market-flow-7b074--staging-76tya5kx.web.app`

**Cause:** That hostname must be allowlisted in **two** places (prod `grabio.space` already is):

1. **Firebase Console** → Authentication → **Settings** → **Authorized domains** → Add:
   - `market-flow-7b074--staging-76tya5kx.web.app`
   - (If the channel ID changes after recreating the channel, add the new `--staging-XXXX.web.app` host.)

2. **Google Cloud Console** → APIs & Services → **Credentials** → Web client used by Firebase (OAuth 2.0) → **Authorized JavaScript origins** → Add:
   - `https://market-flow-7b074--staging-76tya5kx.web.app`

Redirect URI stays `https://market-flow-7b074.firebaseapp.com/__/auth/handler` (already configured).

**App behavior:** Main app `src/lib/firebase.ts` uses `market-flow-7b074.firebaseapp.com` as `authDomain` on preview hosts. **Staging deploy (2026-07-25):** preview hosts use **`signInWithPopup`** instead of redirect (`src/lib/googleAuth.ts`).

**If popup still fails (`auth/unauthorized-domain` or Google popup error):** GCP → Credentials → **Web client** (Firebase) → **Authorized JavaScript origins** → add `https://market-flow-7b074--staging-76tya5kx.web.app`. Firebase authorized domain is already set (verified via Identity Toolkit API).

**Sync script:** `node scripts/syncFirebaseAuthorizedDomains.cjs`

**Workarounds until allowlisted:**
- Test on **prod** `https://grabio.space` (Phase 1 Bank Rec live).
- Or local `npm run dev` on `localhost` (usually already authorized).

**Ref:** [[Decision-Log/2026-07-25-bank-reconciliation-phased-plan]]
