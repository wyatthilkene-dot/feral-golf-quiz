# Feral Golf — Shopify Install Guide

---

# Part 1 — Kyro Feral 3D Configurator

## Files

```
sections/ferrule-configurator.liquid      ← 3D configurator section
templates/page.ferrule-configurator.json  ← page template
models/ferrule.obj                        ← Pyramid model (upload as theme asset)
models/ferrule-dotted.obj                 ← Dimple model (upload as theme asset)
```

## Step 1 — Upload the OBJ Models as Theme Assets

1. Go to **Online Store → Themes → Edit code**
2. In the left sidebar, scroll down to **Assets**
3. Click **Add a new asset** → **Upload file**
4. Upload `models/ferrule.obj` — name must stay exactly `ferrule.obj`
5. Repeat for `models/ferrule-dotted.obj` — name must stay exactly `ferrule-dotted.obj`

> The section references these via `{{ 'ferrule.obj' | asset_url }}` — filenames must match exactly.

## Step 2 — Upload the Section

1. Under **Sections**, click **Add a new section**
2. Name it exactly: `ferrule-configurator`
3. Delete placeholder code, paste full contents of `sections/ferrule-configurator.liquid`
4. Click **Save**

## Step 3 — Upload the Page Template

1. Under **Templates**, click **Add a new template**
2. Choose **page**, name it exactly: `ferrule-configurator`
3. Delete placeholder code, paste full contents of `templates/page.ferrule-configurator.json`
4. Click **Save**

## Step 4 — Create the Page

1. Go to **Online Store → Pages → Add page**
2. Title: `Customize Your Ferrule` (or whatever you prefer)
3. In the **Theme template** dropdown, select **page.ferrule-configurator**
4. Click **Save**

## Troubleshooting — Configurator

| Issue | Fix |
|-------|-----|
| Models not loading | Confirm `ferrule.obj` / `ferrule-dotted.obj` exist under Assets with exact names |
| Blank page / JS error | Check browser console; likely a CDN block on Three.js — add CDN to CSP if needed |
| Configurator fills wrong height | Some themes add padding to sections; add `padding: 0` override to `.kyro-config-section` in theme CSS |

---

# Part 2 — Pick Your Feral Quiz

## Files

```
sections/pick-your-feral.liquid    ← quiz section (logic + UI + styles)
templates/page.pick-your-feral.json  ← page template that loads the section
```

---

## Step 1 — Upload the Section

1. Go to **Online Store → Themes**
2. Click **Actions → Edit code** on your active theme
3. In the left sidebar, under **Sections**, click **Add a new section**
4. Name it exactly: `pick-your-feral`
5. Delete any placeholder code, then paste the full contents of `sections/pick-your-feral.liquid`
6. Click **Save**

---

## Step 2 — Upload the Page Template

1. Still in the code editor, under **Templates**, click **Add a new template**
2. Choose **page** from the dropdown
3. Name it exactly: `pick-your-feral`
4. Delete any placeholder code, then paste the full contents of `templates/page.pick-your-feral.json`
5. Click **Save**

---

## Step 3 — Create the Page

1. Go to **Online Store → Pages**
2. Click **Add page**
3. Set **Title**: `Pick Your Feral`
4. In the **Theme template** dropdown (bottom right), select **page.pick-your-feral**
5. Leave the content area blank
6. Click **Save**

The page will now be live at: `https://www.feralgolfshop.com/pages/pick-your-feral`

---

## Step 4 — Add to Navigation (Optional)

1. Go to **Online Store → Navigation**
2. Open your main menu (or wherever you want to add the link)
3. Click **Add menu item**
4. Label: `Pick Your Feral` (or `Find Your Ferrule`, `Take the Quiz`, etc.)
5. Link: **Pages → Pick Your Feral**
6. Save

---

## Step 5 — Kyro Feral Product (When Ready)

The quiz already includes Kyro Feral as a "Coming Soon" card with an email notify modal.

When you're ready to launch it:

1. Create the product in Shopify with **handle** set to exactly: `kyro-feral-performance-ferrule`
   - Go to the product page → scroll to the bottom → find the **Search engine listing** section
   - The URL handle must match exactly or the AJAX fetch will fail
2. Once live, update the ferrule entry in `sections/pick-your-feral.liquid`:
   - Find `handle: 'kyro-feral-performance-ferrule'`
   - Change `comingSoon: true` to `comingSoon: false`
3. Save the section — the card will automatically switch from "Coming Soon" to a live product card

---

## Email Notify (Coming Soon Modal)

The notify modal currently submits to Shopify's built-in contact form (`/contact#contact_form`).

To connect to **Klaviyo** or another ESP instead:
- Find `id="pyf-notify-form"` in the section file
- Change the `action` attribute to your Klaviyo embed form URL
- Or swap the `fetch` call in `pyfSubmitNotify()` to hit your ESP's API

---

## Troubleshooting

| Issue | Fix |
|-------|-----|
| Products not loading | Check that product handles in `PYF_FERRULES` exactly match Shopify |
| Quiz doesn't appear | Make sure the page is using template `page.pick-your-feral` |
| Add to Cart fails | Ensure the product has active variants and is not draft/archived |
| Fonts not loading | Google Fonts CDN call is in the `<style>` block — check CSP headers |
| Kyro Feral card not showing | It always renders; `comingSoon: true` just changes the card UI |
