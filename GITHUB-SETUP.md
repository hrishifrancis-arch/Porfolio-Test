# Getting your portfolio live

Everything on your side happens in the browser — nothing to install, no command line.
Budget about fifteen minutes, most of it waiting for a confirmation email.

**What it costs: nothing.** GitHub Pages is free and permanent, with no trial and no
monthly fee.

---

## Where your site will live

GitHub stores the site's files and serves them to the internet. Once it's set up, your
portfolio will be at:

**`https://<your-username>.github.io`**

For example, the username `hrishifrancis` gives you `https://hrishifrancis.github.io`.
That's a real, permanent address you can put on your résumé and LinkedIn the same day,
with HTTPS (the padlock) included.

---

## Step 1 — Create your GitHub account

1. Go to **https://github.com/signup**.
2. Enter your email, choose a password, and pick a username.

   > **Choose the username carefully — it becomes your website address.**
   > `hrishifrancis` → `hrishifrancis.github.io`. Use lowercase letters, ideally with no
   > numbers or underscores. This is the one decision here that's awkward to change later.

3. Use an email you'll keep after graduation (a personal address, not only
   `@purdue.edu`), and verify it. GitHub won't publish a site from an unverified account.
4. The **free** plan is all you need. Skip any prompt to upgrade.
5. Turn on two-factor authentication: profile photo (top right) → **Settings** →
   **Password and authentication** → **Enable two-factor authentication**.

**Send Joon your username** once this is done.

---

## Step 2 — Create the repository

A repository is the folder GitHub publishes your site from.

1. Click **+** (top right) → **New repository**.
2. **Repository name:** your username followed by `.github.io`, exactly:

   ```
   <your-username>.github.io
   ```

   > This name is a requirement, not a style choice. It tells GitHub to publish at the
   > root of your address. Any other name puts the site in a sub-folder and breaks the
   > "page not found" page.

3. **Visibility: Public.** Free accounts can only publish from public repositories.
   Everything in it is already public on the site anyway.
4. Leave **Add a README file** unchecked.
5. Click **Create repository**.

---

## Step 3 — Give Joon access to upload the site

1. In your new repository, click **Settings** (the tab row near the top).
2. In the left sidebar, click **Collaborators** → **Add people**.
3. Enter **`joonyoung82`** and confirm.

Joon accepts, uploads the site, and tells you when it's in. Collaborator access lets Joon
add and change files; it does **not** allow changing your settings, rename the
repository, or delete it. You can remove Joon from the same screen whenever you like, and
the repository stays entirely yours.

---

## Step 4 — Switch the website on

This has to be you, because publishing is an owner-only setting.

1. In the repository, go to **Settings** → **Pages** (left sidebar).
2. Under **Build and deployment** → **Source**, choose **Deploy from a branch**.
3. **Branch:** `main`, folder **`/ (root)`** → **Save**.
4. Wait one to two minutes and refresh. A banner appears: *"Your site is live at
   https://<your-username>.github.io"*.
5. Tick **Enforce HTTPS** if it isn't already ticked.

---

## Step 5 — Activate the contact form (one time)

The contact page has a message form. It's free and needs no account, but it has to be
switched on once:

1. Open your live site → **Contact** → send yourself a test message.
2. Check the inbox of the email shown on the Contact page (and the spam folder) for an
   email from **FormSubmit**, and click **Activate Form**.
3. Send one more test message. It should now arrive in your inbox.

Until you click that link, the form shows "Couldn't send just now" — nothing is lost,
visitors can still email you directly.

---

## Step 6 — Check it

On your phone and your laptop:

- [ ] Home loads, and **View projects** goes to the three case studies
- [ ] Each case study opens, and images enlarge when you tap them
- [ ] **CAD Lab** filters work
- [ ] **Download résumé** gives you the PDF
- [ ] The contact form delivers a message (after Step 5)

Then put the address on your résumé and your LinkedIn profile (Contact info →
Website).

---

## Making changes later

Send changes to Joon. The site is built from source files, so edits go through a quick
rebuild rather than editing the pages directly on GitHub — that keeps every page's
navigation, images and footer in sync.

To update just your résumé yourself: in the repository, open the `assets` folder →
**Add file** → **Upload files** → upload the new PDF named exactly
`Hrishi-Francis-Resume.pdf` → **Commit changes**. The site picks it up in a minute or two.

**Please don't delete** the `src`, `tools` or `assets` folders — the site is built
from them.

---

## What you own when this is finished

- The GitHub account, with your email and two-factor authentication
- The repository — remove Joon as a collaborator and Joon has no access at all
- The website address, free and permanent
- The code: plain HTML, CSS and JavaScript with no paid services and nothing that can
  be switched off. The whole site also runs unchanged on Netlify, Cloudflare Pages or
  any ordinary web host.
