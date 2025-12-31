# Google OAuth Setup (Lovable + Supabase)

This guide documents how to (re)configure Google sign-in for GradeKit using **Supabase Auth**.
Use this whenever Google login breaks after changes to domains, environments, or credentials.

---

## What You’ll Need

- A Supabase project (Auth enabled)
- A Google Cloud project
- Your Lovable runtime URL (the `*.lovableproject.com` app URL)
- Access to:
  - Supabase Dashboard
  - Google Cloud Console

---

## 1) Identify Your App URLs (Important)

Lovable has multiple URLs — only one matters for auth redirects.

✅ **Runtime app URL** (use this in Supabase URL allowlists):
- `https://<project-id>.lovableproject.com`

❌ Do NOT use these for auth:
- `https://lovable.dev/projects/...` (editor)
- “Share preview link” (expires / view-only)

---

## 2) Configure Supabase Auth URLs

Go to: **Supabase Dashboard → Authentication → URL Configuration**

### A) Site URL
Set to your Lovable runtime app URL:
- `https://<project-id>.lovableproject.com`

### B) Additional Redirect URLs
Add (one per line):
- `https://<project-id>.lovableproject.com`
- `https://<project-id>.lovableproject.com/*`

> Tip: Keep these updated when you publish or add a custom domain.

---

## 3) Enable Google Provider in Supabase

Go to: **Supabase Dashboard → Authentication → Providers → Google**

- Toggle **Enable**
- You will need:
  - Google **Client ID**
  - Google **Client Secret**

Also note the **Redirect URL** Supabase requires (you will paste this into Google):
- `https://<your-supabase-project-ref>.supabase.co/auth/v1/callback`

---

## 4) Create / Configure OAuth in Google Cloud Console

Go to: **Google Cloud Console → APIs & Services**

### A) OAuth Consent Screen
1. Open **OAuth consent screen**
2. User type: **External**
3. Fill required fields:
   - App name (e.g. GradeKit)
   - User support email
   - Developer contact email
4. Save

#### Testing Mode (Recommended during development)
- Add your email under **Test users**
  - Only test users can log in while in “Testing”.

### B) Create OAuth Client ID
1. Go to **Credentials**
2. Click **Create Credentials → OAuth client ID**
3. Application type: **Web application**
4. Add the authorised redirect URI:

✅ Add exactly:
- `https://<your-supabase-project-ref>.supabase.co/auth/v1/callback`

5. Create
6. Copy:
- Client ID
- Client Secret

---

## 5) Paste Credentials into Supabase

Back to: **Supabase → Authentication → Providers → Google**

- Paste the **Client ID**
- Paste the **Client Secret**
- Save

---

## 6) Verify It Works (Fast Checklist)

### A) Test the Supabase callback flow (optional but useful)
Open Google sign-in from your app and confirm you reach the account chooser.

### B) Test in Incognito
- Open your Lovable runtime app URL in an **Incognito** window
- Click **Continue with Google**
- Select an account
- Confirm you return to the app logged in

---

## Common Issues + Fixes

### “403: you do not have access”
Usually means:
- OAuth consent screen not set to **External**, OR
- Your account is not in **Test users**, OR
- You edited the wrong Google OAuth client, OR
- Redirect URI mismatch

Fix:
- Confirm consent screen is External
- Add your email to Test users
- Confirm redirect URI matches exactly:
  - `https://<supabase>.supabase.co/auth/v1/callback`

### Sign-in works but user returns logged out
Usually means Supabase redirect allowlist is missing your app URL.

Fix:
- Supabase → URL Configuration → add your Lovable runtime URL + wildcard.

### It works on desktop but not iOS Safari / Chrome iOS
Fix:
- Use redirect-based OAuth flows (no popups)
- Ensure URLs are correct and allowlisted in Supabase

---

## When You Publish / Add a Custom Domain

After publishing, add your production domain in Supabase:
- Authentication → URL Configuration
  - Site URL: `https://yourdomain.com`
  - Additional Redirect URLs: `https://yourdomain.com/*`

You can keep the `*.lovableproject.com` URL during transition, then remove later if desired.

---
