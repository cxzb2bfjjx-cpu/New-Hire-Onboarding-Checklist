# New Hire Onboarding Checklist

A single-file, no-server onboarding checklist for new employees. Everything —
the progress bar, the 50 expandable checklist items, employee progress
tracking, and the password-protected admin editor — lives in one
self-contained `index.html` you can share via email, Google Drive, SharePoint,
or a shared network folder.

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
  instructions**. Whatever you type in that box is shown to employees: a full
  URL (`https://...` or `www....`) becomes a clickable link displaying that
  address; anything else is shown as plain text (e.g. "Ask your manager for
  access"). Leave it blank to show nothing.
- **Add** items (the "+ Add checklist item" button), **delete** items (✕),
  and **reorder** them (▲ ▼) — so the list can grow past 50 or shrink as
  your onboarding process evolves

### Publishing your changes (important!)

Because there is no server, edits made in the browser only exist in your
session until you bake them into a file:

1. Make your edits in admin mode.
2. Click **⬇ Download updated checklist**. This downloads a fresh
   `new-hire-onboarding-checklist.html` with your content (and password)
   permanently embedded.
3. Distribute **that downloaded file** to employees — it replaces the old
   one.

If you close the page with unsaved edits, they're kept as a draft in your
browser and you'll be offered the chance to restore them the next time you
log in to admin mode on the same device.

### Importing content from a saved file (upgrades & recovery)

Your content lives **inside the file copy you saved**, not in any server.
So if you get a newer version of this tool (with new features) but it shows
the blank sample items, you don't have to re-type anything:

1. Open the new file and log in to admin mode.
2. Click **⬆ Import from saved file** and choose the checklist file you
   saved earlier (the `.html` you downloaded, or a JSON export of it).
3. All your content — title, welcome message, every item's title/link/
   description, and your admin password — loads into the new version.
4. Click **⬇ Download updated checklist** to save the merged file, and
   distribute that.

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

If you later buy a real domain (e.g. `azlungonboarding.com`), enter it in
the **Custom domain** box on that same *Settings → Pages* screen and follow
GitHub's DNS prompts — everything else stays the same.

### Updating the live site

Once hosted, "distribute the new file" becomes "replace the file in the repo":

1. In admin mode, click **⬇ Download updated checklist**.
2. Rename the download to `index.html`.
3. On GitHub (`main` branch): *Add file → Upload files* → drop in
   `index.html` → **Commit changes**. The live site updates within a couple
   of minutes; employees just refresh the page and their progress is kept.

> Note: a GitHub Pages site is publicly reachable by anyone who has the
> URL, even though it's unlisted. Keep that in mind for what you put in
> descriptions and links.

## Security note

The admin password is stored as a SHA-256 hash inside the file, so it isn't
readable in plain text. However, this is a client-side tool: a technically
savvy user could inspect the file's source. Treat the lock as a strong
deterrent for normal use — appropriate for an internal onboarding
checklist — not as protection for sensitive data. Don't put secrets in the
descriptions or links.

## Development

No build step, no dependencies. The file is plain HTML/CSS/JS; checklist
content lives in the JSON block tagged `id="checklist-config"` near the top
of `index.html`, which you can also edit directly in a text editor if you
prefer that over admin mode.
