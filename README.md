# New Hire Onboarding Checklist

A no-server onboarding checklist for new employees: a progress bar, expandable
checklist items, per-device progress tracking, and a password-protected admin
editor — all in plain HTML/CSS/JS.

Two files work together:

- **`index.html`** — the app (the code). It rarely needs to change.
- **`content.json`** — your content (titles, links, descriptions, the admin
  password hash). This is the only file you edit/replace to change what
  employees see.

When hosted on a website, `index.html` loads `content.json` **fresh on every
visit**, so updates can't get stuck behind a browser or Home-Screen cache, and
updating the code never wipes your content. If `index.html` is opened directly
from disk (no website), it falls back to a built-in copy of the content baked
into the page.

## For employees

1. Open `index.html` (or the file you were sent) in any modern browser —
   double-clicking it works; no installation needed.
2. Click any item to expand it and see what to do. Each item can show a
   clickable link to the resource, or — when there's no link — plain-text
   instructions for how to access it (some items have neither).
3. Tick **Mark as complete** on each item. The progress bar at the top
   updates automatically.
4. Progress is saved in the browser on that device, so you can close the
   page and pick up where you left off. **Reset my progress** (in the
   footer) clears your checkmarks.

Employees cannot change titles, links, or descriptions — content is
read-only without the admin password.

## For the admin (you)

### Unlock admin mode

Click **Admin** in the page footer and enter the password.

> **Default password: `ChangeMe123` — change it immediately** via the
> "Change admin password" button in the admin toolbar.

### What you can edit

- The checklist **title** and **welcome message**
- Each item's **title**, **description**, and **resource link or access
  instructions**. Whatever you type in that box is shown to employees: a web
  address — **with or without `https://`** (e.g. `intranet.acme.com/benefits`,
  `www.acme.com`, `mailto:hr@acme.com`) — becomes a clickable link; anything
  with spaces (e.g. "Ask your manager for access") is shown as plain text.
  A live preview under the box tells you which it will be. Leave it blank to
  show nothing.
- **Add** items (the "+ Add checklist item" button), **delete** items (✕),
  and **reorder** them (▲ ▼) — so the list can grow past 50 or shrink as
  your onboarding process evolves

### Publishing your changes (important!)

Edits made in admin mode live only in your browser until you save them to the
content file and upload it. The workflow is one small file:

1. Make your edits in admin mode.
2. Click **⬇ Download content file**. This downloads `content.json` with your
   content and password.
3. Upload that `content.json` to your site, replacing the old one (see
   *Hosting* below). **You do not need to touch `index.html`.**

Within moments, everyone — including phones with the page saved to their Home
Screen — sees the new content on their next visit, because the page always
loads `content.json` fresh.

> There is also a **Download standalone HTML** button. Use it only if you want
> a single self-contained file to open directly/offline (it bakes the content
> into the page). For a hosted site, use the content file.

If you close the page with unsaved edits, they're kept as a draft in your
browser and you'll be offered the chance to restore them the next time you
log in to admin mode on the same device.

### Importing content from a saved file (upgrades & recovery)

Your content lives **inside the file copy you saved**, not in any server.
So if you get a newer version of this tool (with new features) but it shows
the blank sample items, you don't have to re-type anything:

1. Open the new file and log in to admin mode.
2. Click **⬆ Import from saved file** and choose a checklist file you saved
   earlier — a `content.json` or a standalone `.html` you downloaded.
3. All your content — title, welcome message, every item's title/link/
   description, and your admin password — loads into the new version.
4. Click **⬇ Download content file** and upload the resulting `content.json`.

This is the supported way to carry your content forward across versions.

## Hosting on GitHub Pages

The checklist is set up to be hosted for free at:

> **https://cxzb2bfjjx-cpu.github.io/azlungonboarding/**

One-time setup (about 2 minutes, done in the GitHub web UI):

1. **Rename the repository to `azlungonboarding`** so the URL reads
   "azlungonboarding": *Settings → General → Repository name* → type
   `azlungonboarding` → **Rename**. (Skip this step and the URL is
   `https://cxzb2bfjjx-cpu.github.io/New-Hire-Onboarding-Checklist/` instead.)
2. **Make the repository public** if it is currently private (free GitHub
   accounts can only use Pages on public repos): *Settings → General →
   Danger Zone → Change visibility → Public*.
3. **Turn on Pages**: *Settings → Pages → Build and deployment* →
   Source: **Deploy from a branch** → Branch: **main**, folder: **/ (root)**
   → **Save**.
4. Wait a minute or two, then refresh the Pages settings page — your live
   URL appears at the top. Share that link with new hires.
5. (Optional) Set `main` as the default branch: *Settings → General →
   Default branch*.

Both `index.html` **and** `content.json` must be in the repo (they already
are). The page reads its content from `content.json` next to it.

If you later buy a real domain (e.g. `azlungonboarding.com`), enter it in
the **Custom domain** box on that same *Settings → Pages* screen and follow
GitHub's DNS prompts — everything else stays the same.

### Saving to a phone Home Screen

Employees can open the link in Safari/Chrome on their phone and choose **Add to
Home Screen** to get an app-like icon. Because the page reloads `content.json`
fresh each time, a Home-Screen copy still shows your latest content — it won't
get frozen on an old version.

### Updating the live site (the easy part)

To change content, you upload **only `content.json`** — never `index.html`:

1. In admin mode, click **⬇ Download content file** (`content.json`).
2. On GitHub (`main` branch): open the existing `content.json` → the **pencil
   (Edit)** icon, or use *Add file → Upload files* → drop in your new
   `content.json` → **Commit changes**.
3. The live site shows the new content on the next visit (usually seconds).
   Employees' saved progress is kept.

Because content lives in `content.json`, future updates to `index.html` (new
features, fixes) can never overwrite your content.

> Note: a GitHub Pages site is publicly reachable by anyone who has the
> URL, even though it's unlisted. The admin password hash and all content in
> `content.json` are readable by anyone who looks. Keep that in mind for what
> you put in descriptions and links.

## Security note

The admin password is stored as a SHA-256 hash inside the file, so it isn't
readable in plain text. However, this is a client-side tool: a technically
savvy user could inspect the file's source. Treat the lock as a strong
deterrent for normal use — appropriate for an internal onboarding
checklist — not as protection for sensitive data. Don't put secrets in the
descriptions or links.

## Development

No build step, no dependencies. `index.html` is plain HTML/CSS/JS. Content
lives in `content.json` (loaded at runtime when hosted); the `<script
id="checklist-config">` block inside `index.html` is only a fallback copy used
when the page is opened directly from disk. You can edit `content.json` by hand
in any text editor instead of using admin mode if you prefer — keep it valid
JSON with a top-level `items` array.
