# Pocket Arcade — Privacy Policy (GitHub Pages)

This folder hosts the Pocket Arcade privacy policy as a single static
`index.html` page. Google Play and Apple both require a publicly reachable
privacy-policy URL in the store listing.

## Files in this folder

| File | Purpose | Public URL after deploy |
|---|---|---|
| `index.html` | Privacy Policy | `/` |
| `terms.html` | Terms of Service | `/terms.html` |
| `delete-account.html` | Account & data deletion request (Google Play / App Store required) | `/delete-account.html` |

## Host for free on GitHub Pages (3 minutes)

```bash
# 1. Create a brand-new public repo, e.g. "pocket-arcade-privacy"
#    (keep it empty on github.com — don't auto-init a README)

# 2. Copy this folder's index.html into that repo
cp index.html terms.html delete-account.html ~/code/pocket-arcade-privacy/
cd ~/code/pocket-arcade-privacy
git init
git add index.html terms.html delete-account.html
git commit -m "Add Pocket Arcade privacy policy, terms, and account deletion page"
git branch -M main
git remote add origin git@github.com:<your-username>/pocket-arcade-privacy.git
git push -u origin main

# 3. On github.com → Settings → Pages
#    • Source: Deploy from a branch
#    • Branch: main  (folder: /root)
#    • Save

# 4. In ~60 seconds, your policy is live at
#    https://<your-username>.github.io/pocket-arcade-privacy/
```

Paste those URLs into:

- **Google Play Console** → Policy → App content → Privacy policy URL
  (`https://<your-username>.github.io/pocket-arcade-privacy/`)
- **Google Play Console** → Policy → App content → **Data deletion** → "URL where users can request data deletion"
  (`https://<your-username>.github.io/pocket-arcade-privacy/delete-account.html`)
- **App Store Connect** → App Information → Privacy Policy URL
  (`https://<your-username>.github.io/pocket-arcade-privacy/`)
- **App Store Connect** → App Privacy → Account deletion URL (if your app supports accounts)
  (`https://<your-username>.github.io/pocket-arcade-privacy/delete-account.html`)

Whenever you update any HTML file, `git push` — GitHub Pages re-deploys
automatically within a minute.
