# Getting laikadc.com Live (GitHub Pages)

Free hosting on your existing GitHub account, domain stays at GoDaddy. ~20 minutes of work, then up to an hour of DNS wait.

## Step 1 — Create the repository

1. Go to https://github.com/new
2. Repository name: `laikadc` (anything works). Visibility: **Public** (required for free Pages).
3. Check "Add a README file" (this makes the next step easier), then **Create repository**.

## Step 2 — Upload the site files

1. In the new repo, click **Add file → Upload files**.
2. Open the `laikadc-site` folder on your Mac in Finder. Select `index.html` and the `assets` folder and drag them both into the upload area. (Chrome preserves the folder structure; you should see `index.html` plus `assets/...` files listed. Don't upload this guide.)
3. Click **Commit changes**.
4. Verify the repo now shows `index.html` at the top level and an `assets/` folder — not a `laikadc-site/` wrapper folder. If everything ended up inside `laikadc-site/`, delete and re-upload the contents rather than the folder itself.

## Step 3 — Turn on GitHub Pages

1. In the repo: **Settings → Pages** (left sidebar).
2. Under "Build and deployment": Source = **Deploy from a branch**, Branch = **main**, folder = **/ (root)**. Save.
3. Wait ~1–2 minutes, refresh the page. You'll see "Your site is live at `https://YOURUSERNAME.github.io/laikadc/`". Open it and check everything looks right.

## Step 4 — Point laikadc.com at it

**In GitHub** (Settings → Pages → Custom domain):

1. Enter `laikadc.com` → Save. GitHub adds a `CNAME` file to the repo — leave it there.
2. It will show "DNS check unsuccessful" until you finish the GoDaddy side. That's expected.

**In GoDaddy** (My Products → laikadc.com → DNS / Manage DNS):

1. Delete the existing **A record** for `@` (usually "Parked").
2. Add four **A records**, each with Name `@`, TTL default:
   - `185.199.108.153`
   - `185.199.109.153`
   - `185.199.110.153`
   - `185.199.111.153`
3. Add/edit the **CNAME record** for `www` → value `YOURUSERNAME.github.io` (your username, NOT the repo name, no https://).
4. If GoDaddy shows any "Forwarding" set up for the domain, remove it.

**Back in GitHub** (Settings → Pages):

1. Wait 15–60 minutes for DNS to propagate, then click the check/retry next to the custom domain. It should turn green.
2. Check **Enforce HTTPS** (may take a few more minutes to become available while GitHub issues the certificate).
3. Done: `https://laikadc.com` and `https://www.laikadc.com` both serve the site.

## Step 5 — Set up arcady@laikadc.com

The site's contact buttons point to `arcady@laikadc.com`:

- **Free (forwarding):** GoDaddy → your domain → look for **Email Forwarding** (free with most GoDaddy domains). Create `arcady@laikadc.com` → forward to `asosinov@gmail.com`. To reply *from* the address, add it in Gmail: Settings → Accounts → "Send mail as".
- **Paid (real mailbox):** Google Workspace (~$7/user/mo). Better long-term for a real company.

Note: email forwarding uses MX records, which are separate from the A/CNAME records above — website and email don't interfere with each other.

## Updating the site later

Repo → open `index.html` → pencil icon to edit in place, or **Add file → Upload files** to replace files (same-named files are overwritten). Every commit republishes automatically in ~1 minute.

## Troubleshooting

- **404 at laikadc.com but github.io URL works:** DNS hasn't propagated, or the A records are wrong. Check with https://dnschecker.org (search `laikadc.com`, type A — should show the 185.199.x.x IPs).
- **"Enforce HTTPS" greyed out:** wait — the certificate issues only after the DNS check passes.
- **Site loads without styling/images:** the `assets` folder didn't upload at the repo root. Repo must show `index.html` and `assets/` side by side.
- **Custom domain resets after a new upload:** the `CNAME` file got deleted — re-add the custom domain in Settings → Pages.
