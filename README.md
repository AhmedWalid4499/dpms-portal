# DPMs Management Portal

A secure, role-based internal portal for the DPMs Management team — built as a single-page app deployable on GitHub Pages.

---

## 🚀 Quick Setup (5 Steps)

### Step 1 — Create Your GitHub Repository

1. Go to [github.com](https://github.com) and sign in
2. Click **New Repository**
3. Name it: `dpms-portal` (or any name you like)
4. Set it to **Private** (recommended) or Public
5. Click **Create Repository**

### Step 2 — Upload Files

Upload these files to your repo, keeping the folder structure:
```
dpms-portal/
├── index.html
├── data/
│   ├── users.json
│   ├── team.json
│   └── stats.json
└── README.md
```

### Step 3 — Create a GitHub Personal Access Token (PAT)

This token lets the portal save data back to your repo.

1. Go to **GitHub → Settings → Developer settings → Personal access tokens → Fine-grained tokens**
2. Click **Generate new token**
3. Set:
   - **Token name**: `dpms-portal-data`
   - **Expiration**: 1 year (or No expiration)
   - **Repository access**: Only select repositories → choose `dpms-portal`
   - **Permissions**: Under Repository permissions → **Contents** → `Read and write`
4. Click **Generate token**
5. **Copy the token now** — you won't see it again!

### Step 4 — Configure the Portal

Open `index.html` and find this section near the top (lines ~20–30):

```javascript
const GH_CONFIG = {
  owner:  'YOUR_GITHUB_USERNAME',   // Replace with your GitHub username
  repo:   'YOUR_REPO_NAME',         // Replace with your repo name (e.g. 'dpms-portal')
  branch: 'main',
  token:  'YOUR_GITHUB_PAT_TOKEN',  // Paste your PAT token here
  ...
};
```

Replace the three values with your actual username, repo name, and token.

### Step 5 — Enable GitHub Pages

1. Go to your repo → **Settings → Pages**
2. Under **Source**, select **Deploy from a branch**
3. Choose `main` branch, `/ (root)` folder
4. Click **Save**
5. Your portal will be live at: `https://YOUR_USERNAME.github.io/dpms-portal/`

> ⏱ First deployment takes ~2 minutes. Refresh if you see a 404.

---

## 👑 Admin Accounts

The following 4 email addresses are **permanently designated as Admin** accounts:

| Name | Email |
|------|-------|
| Peter Sabet | peter.sabet@orange.com |
| Karim Elzarka | karim.elzarka@orange.com |
| Maryam Etry | maryam.etry@orange.com |
| Mona Tamimy | mona.tamimy@orange.com |

**How Admin first login works:**
- Visit the portal and click **Sign In**
- Enter your `@orange.com` email and choose a password
- The portal will auto-create your admin account on first sign-in
- Your password is hashed (SHA-256) and stored securely in `users.json`

**Admin capabilities:**
- ✅ Add & remove team members
- ✅ View Budget page (hidden from Members)
- ✅ View Salaries page (hidden from Members)
- ✅ Manage all user accounts (activate/deactivate)
- ✅ Edit performance scores and statistics
- ✅ Add achievements

---

## 👤 Member Accounts

All other `@orange.com` users register themselves:
1. Go to the portal
2. Click **Create Account**
3. Fill in name, email, password, and squad
4. Account is created instantly with **Member** access

**Member capabilities:**
- ✅ View Home, Team, Squads, Statistics, Performance, Achievements
- ❌ Cannot see Budget or Salaries
- ❌ Cannot add/remove members
- ❌ Cannot edit data (view-only)

---

## 🌐 Public Access (Guest)

Anyone can browse the portal as a Guest without logging in:
- ✅ View Home page
- ✅ View Achievements page
- ❌ All other pages require login

---

## 📁 Data Files

All data is stored as JSON files in your repo:

| File | Contents |
|------|----------|
| `data/users.json` | Registered users & password hashes |
| `data/team.json` | Team members & squad configurations |
| `data/stats.json` | KPIs, performance scores, achievements, budget, salaries |

> **Note:** Without the GitHub token configured, the portal falls back to `localStorage` — data is saved in the browser only and won't sync across devices.

---

## 🔒 Security Notes

- Passwords are hashed using **SHA-256** (via browser's SubtleCrypto API) before storage
- Only `@orange.com` emails can register
- The GitHub PAT token is embedded in `index.html` — keep your repo **Private** to protect it
- For production use, consider using a backend service (Supabase, Firebase) for more secure auth
- Admin email list is hardcoded and cannot be changed by regular users

---

## 🛠 Customization

### Add More Admins
Find `ADMIN_EMAILS` in `index.html` and add emails:
```javascript
const ADMIN_EMAILS = [
  'peter.sabet@orange.com',
  'karim.elzarka@orange.com',
  'maryam.etry@orange.com',
  'mona.tamimy@orange.com',
  // 'new.admin@orange.com',  ← add here
];
```

### Add More Squads
Edit `data/team.json` and add to the `squads` array.

### Update Budget/Salaries
Log in as an Admin → click **Budget** or **Salaries** in the nav → **Edit** button.

### Update Performance Scores
Log in as Admin → **Performance** page → **Update Scores** button.

---

## 📞 Support

For issues with the portal, contact the Admin team or open a GitHub Issue in this repository.

---

*DPMs Management Portal · Orange Restricted · Private*
