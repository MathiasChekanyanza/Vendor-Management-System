# Vendor Management System — Single-file app

This repository contains a single-file, production-ready Vendor Management System (`index.html`) that persists vendor records in `localStorage` and is ready to deploy to GitHub Pages.

Features
- Add / edit / delete vendors (name, address, phone, optional site image)
- Search/filter vendors by name / address / phone
- Responsive card grid layout (mobile-first)
 - Responsive card grid layout (mobile-first)
 - Export vendors to CSV (images excluded from CSV)
 - Images stored as base64 (max 2 MB)
- Static demo login (admin / admin123) — stored in sessionStorage

Quick deploy (recommended)
1. Commit and push this repository to GitHub (create a repo if needed). Replace `<git-remote-url>` with your repository URL.

```powershell
git add .
git commit -m "Add vendor management single-file app"
git branch -M main
git remote add origin <git-remote-url>
git push -u origin main
```

2. The repository includes a GitHub Actions workflow that will publish the repository root to GitHub Pages whenever you push to `main` or `master`. The workflow uses the official `actions/upload-pages-artifact` and `actions/deploy-pages` actions.

3. After the workflow runs (check the Actions tab), your site will be available at:

- For project pages: https://<your-github-username>.github.io/<repo-name>/
- For user/org pages (if repository is `username.github.io`): https://<your-github-username>.github.io/

If you prefer manual Pages settings, you can also enable GitHub Pages from repository Settings -> Pages, but the included workflow automates deployment.

Notes & tips
- To remove the demo login, edit `index.html` and remove the `#loginModal` block and the initial login check (or set `sessionStorage.setItem('vms_logged_in','true')` in the console).
 - Vendor localStorage keys use the pattern `vendor:vendor_TIMESTAMP`. Each vendor object contains: id, name, address, phone, activity (what they do), image (base64 or empty), cameraImage (base64 or empty), createdAt, updatedAt.
 - Exported CSV includes the following columns: id, name, address, phone, activity, createdAt, updatedAt (images are excluded from CSV).
- Storing many or large images in localStorage can exhaust quota — consider server-side storage for production.

Troubleshooting
- If the Pages workflow doesn't deploy, open the Actions tab and inspect the `Deploy static site to GitHub Pages` run for errors.
- Make sure your repository is public or Pages is enabled for private repos in your settings.

Want me to also add:
- a storage adapter to swap `localStorage` for a `window.storage` host API? (yes/no)
- a demo-data import UI or sample data? (yes/no)
