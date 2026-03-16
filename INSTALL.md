# Pick Your Feral — Shopify Install Guide

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
