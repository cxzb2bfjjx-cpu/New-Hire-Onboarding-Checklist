# New Hire Onboarding Checklist

A single-file, no-server onboarding checklist for new employees. Everything —
the progress bar, the 50 expandable checklist items, employee progress
tracking, and the password-protected admin editor — lives in one
self-contained `index.html` you can share via email, Google Drive, SharePoint,
or a shared network folder.

## For employees

1. Open `index.html` (or the file you were sent) in any modern browser —
   double-clicking it works; no installation needed.
2. Click any item to expand it and see what to do, plus a link to the
   relevant company resource.
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
- Each item's **title**, **resource link**, and **description**
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
