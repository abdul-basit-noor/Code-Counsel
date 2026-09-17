# Code Counsel — Website

A 4-page responsive site: `index.html`, `services.html`, `about.html`, `contact.html`, sharing `css/style.css` and `js/main.js`.

## About "fullstack" on GitHub Pages

GitHub Pages only serves static files — there's no server, database, or backend code running behind it. So this site is built as a static site with one piece of real, working functionality added on top: the contact form, which posts to **Formspree** (a free third-party form backend) instead of needing your own server. That's the practical way to get a working "send us a message" feature on GitHub Pages without a backend.

If you later want an actual backend (a database of leads, an admin dashboard, custom email logic), that needs separate hosting (e.g. Render, Railway, a VPS) — GitHub Pages can't run it, but this site can still be the front end for it.

## 1. Connect the contact form (2 minutes)

1. Go to [formspree.io](https://formspree.io) and create a free account.
2. Create a new form, copy the endpoint it gives you (looks like `https://formspree.io/f/abcd1234`).
3. In `contact.html`, find:
   ```html
   <form id="contact-form" action="https://formspree.io/f/your-form-id" method="POST">
   ```
   Replace `your-form-id` with your real endpoint.
4. Formspree will send a confirmation email the first time someone submits — click the link to activate the form.

Until you do this, the form shows a message telling the visitor it isn't configured yet, instead of failing silently.

## 2. Add your logo

Drop a logo file into `images/` and reference it in each page's `<header>` if you want an image mark instead of the text wordmark currently used. The current design uses a text logo, so this step is optional.

## 3. Deploy to GitHub Pages

1. Create a new repository on GitHub (e.g. `codecounsel-site`).
2. Upload every file in this folder, **keeping the folder structure** (`css/`, `js/`, `images/` as subfolders — don't flatten them).
   - Easiest: on the repo page, click "Add file" → "Upload files", drag the whole folder contents in.
   - Or via git:
     ```bash
     git init
     git add .
     git commit -m "Initial site"
     git branch -M main
     git remote add origin https://github.com/<your-username>/<repo-name>.git
     git push -u origin main
     ```
3. In the repository, go to **Settings → Pages**.
4. Under "Build and deployment", set **Source** to "Deploy from a branch", branch `main`, folder `/ (root)`.
5. Save. GitHub will give you a URL like `https://<your-username>.github.io/<repo-name>/` within a minute or two.

## 4. Custom domain (optional)

If you want a domain like `codecounsel.pk` instead of the github.io URL:
1. Add a `CNAME` file to the repo root containing just your domain, e.g. `codecounsel.pk`.
2. At your domain registrar, point the domain's DNS to GitHub Pages (an `A` record to GitHub's IPs, or a `CNAME` record for a subdomain) — GitHub's Pages settings page shows you the exact records once you enter the domain there.

## File structure

```
codecounsel-site/
├── index.html
├── services.html
├── about.html
├── contact.html
├── css/
│   └── style.css
├── js/
│   └── main.js
├── images/
│   └── (add your logo here, optional)
└── README.md
```

## Editing content later

All four pages share the same header/nav and footer markup (plain HTML, no templating — that's a GitHub Pages constraint without adding a build step). If you edit the phone number, email, or footer text, update it in all four files, or ask Claude to do a find-and-replace across the folder.
