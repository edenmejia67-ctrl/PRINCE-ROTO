# Dapdap High School – Security Visitor Notification System

A simple, single-page web app for the school guard to register visitors, check them out, and notify the teacher or office they came to see. Built with plain HTML, CSS and JavaScript. No install and no build step.

## Files

| File | What it is |
|---|---|
| `index.html` | The whole app (layout, styles, logic) |
| `README.md` | This guide |

## Run it

1. Download or clone this repo.
2. Double-click `index.html`. It opens in your browser.
3. Demo login: **guard** / **guard123**

## Put it online with GitHub Pages

1. Create a new repository and upload `index.html` and `README.md`.
2. Go to **Settings → Pages**.
3. Under **Branch**, choose `main` and `/ (root)`, then **Save**.
4. After about a minute your site is live at `https://<your-username>.github.io/<repo-name>/`.

## How the guard uses it

1. **Register Visitor** – type the name and contact number, pick the purpose and the teacher or office from the dropdown. Date and time in are filled in automatically.
2. Press **Register**. A notification for the chosen teacher or office is created.
3. When the visitor leaves, press **Check out** on the Dashboard or Visitor Records page. The time out is saved.
4. **Visitor Records** has a search box and a date range. **Settings** switches the language between English and Tagalog.

## Current limits (the database comes later)

- Data is saved in the browser (`localStorage`), so it stays on one computer. Sample visitors are preloaded; **Settings → Reset demo data** restores them.
- Teachers do not receive notifications on their own devices yet. This needs the shared database.
- The **Scan QR Code** button is a placeholder.
- The school seal is a drawn stand-in. Replace the `SEAL` constant in `index.html` with your real logo.

## Connecting a database later

Everything the app reads or writes goes through a few places in the `<script>`:

| What | Where | Shape |
|---|---|---|
| Teachers and offices | `FAC` array | list of strings |
| Visitors | `V` array, saved by `save()` | `{id, name, contact, purpose, person, tin, tout}` (`tin` and `tout` are ISO date strings, `tout` is `null` while inside) |
| Notifications | `N` array, saved by `save()` | `{id, vid, read}` (`vid` is the visitor id) |

Swap `ld()`, `sv()` and `save()` for calls to your database (for example Supabase or Firebase) and subscribe to changes so the dashboard and notifications update live.

## Customize

- **Colors, radius, shadow:** the variables at the top of the `<style>` block (`--nav`, `--pri`, `--line`, `--sh`).
- **Wording and Tagalog translations:** the `T` object in the script.
- **Purposes of visit:** the `PUR` array and the `p_...` entries in `T`.

## Design notes

The layout follows the supplied Dapdap mockup (login, dashboard, register, records, notifications). The four reference screens were used for mood and details, and the "looks like AI" problem was handled with a short rule set.

**What came from each reference**

| Reference | Borrowed |
|---|---|
| Blue glass fintech app | Rounded-square icon tiles, a navy panel with a curved edge, soft blue-tinted background |
| Dark VPN app | A floating pill navigation bar (used on phones and tablets), one calm status color per state |
| Visitor app (shield login) | Curved edge on the login panel, avatar initials in lists |
| Soft blue clinic app | Pill tab bar, generous padding, light line icons, big readable headings |

**Rules used to avoid the generic AI look**

1. **One palette, tinted neutrals.** Navy, one bright blue, and blue-gray greys. No pure black or pure gray. Red is only for "new", green only for "inside".
2. **Different radius for different jobs.** Buttons and inputs 10px, cards 14px, dialogs 18px, small tags 6px. Not the same giant radius everywhere.
3. **Borders show structure, shadows show depth.** Every card has a thin border and one very light shadow. No glow, no heavy drop shadows, no frosted-glass blur.
4. **No decoration that says nothing.** No emoji, no random sparkline charts, no gradient buttons, no "Welcome back 👋". Every number on screen is real data.
5. **A real typeface with weight contrast.** Plus Jakarta Sans, with heavy headings and numbers, regular body text, and tabular digits so times line up.
6. **One icon style.** All icons are the same 2px line style. Nothing mixed.
7. **All the states exist.** Hover, keyboard focus ring, pressed, empty list message, and a confirmation toast after each action.
8. **Spacing on a 4/8 px rhythm.** Related things are grouped with space first, not boxes inside boxes.
9. **Readable and accessible.** Text meets contrast guidelines, status is shown with a dot and a word (not color alone), controls are keyboard reachable, and motion is minimal and switches off for people who ask for reduced motion.
10. **Built for the guard's job.** Dropdowns instead of typing names, automatic time, one main action per screen, and big tap targets on a tablet.

**Quick check before shipping a screen:** squint at it. Is there one clear main action? Are there more than two border radii or more than one shadow style? Is anything there only to look fancy? If yes, remove it.

Sources read while preparing these notes: [anti-patterns in AI-generated interfaces](https://www.mintlify.com/pbakaus/impeccable/concepts/anti-patterns), [how to make AI UI feel less generic (daisyUI)](https://trends.daisyui.com/how-to-make-ai-ui-less-generic/), [How to Make AI UI Look Less Generic (SuperDesign)](https://www.superdesign.dev/blog/how-to-make-ai-ui-look-less-generic), and [Breaking the AI-generated UI curse (DEV)](https://dev.to/a_shokn/how-to-break-the-ai-generated-ui-curse-your-guide-to-authentic-professional-design-2en).

Reference screenshots belong to their original designers and were used for inspiration only.
