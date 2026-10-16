# Setup Surface Separation

**Last updated:** 2026-09-10

## Purpose

Grabio setup was originally concentrated in Store Profile. It is now split into three setup surfaces for performance, clarity, and long-term modularity. Future agents must keep these surfaces separate.

## The Three Setup Surfaces

| Surface | Purpose | Primary files | Owns |
|---|---|---|---|
| Store Profile setup | Business identity and operational defaults | `src/pages/admin/AdminProfile.tsx`, `src/types/storeProfile.ts` | Store name, contact info, public shop logo, currency, tax basics, payment gateways, product categories, package/account settings |
| Invoice document setup | A4/PDF invoice, estimate, and finance document branding | `src/pages/admin/finance/BusinessFinanceInvoiceTemplateSetup.tsx`, `src/lib/financeDocumentSettings.ts`, `src/lib/invoiceTemplateMap.ts` | Document logo, document company name, document address, document tax ID, A4 invoice template style, document colors/signature when added |
| Website template setup | Storefront theme, public website layout, visual sections | `src/pages/admin/AdminTemplates.tsx`, `src/pages/admin/ThemeEditor.tsx`, builder/theme helpers | Storefront template, theme colors, section order, hero layout, product display, gallery, background, website visual style |

## Ownership Rules

1. Store Profile must not become the place for every setup setting.
2. Invoice document setup owns A4/PDF document appearance and document-specific identity.
3. Website template setup owns storefront appearance and public website layout.
4. Shared fields may be used as fallback display only, but the UI must clearly show where the authoritative setting is edited.
5. If a field affects more than one surface, document the source of truth and fallback order.
6. No page should silently write fields owned by another setup surface unless the helper is explicitly designed as a compatibility bridge.

## Current Review Findings

### Store Profile

Current state:

- Store Profile still loads and saves many fields from `storeProfiles`.
- It includes business identity, shop logo, payment gateway settings, system preferences, product categories, invoice numbering, and tax number.
- It already includes UI copy pointing users to Theme Editor and Business Finance for visual/document templates.

Risk:

- Store Profile is still too broad and can become the old all-in-one setup again.

### Invoice Document Setup

Current state:

- `BusinessFinanceInvoiceTemplateSetup.tsx` separately edits `financeDocumentSettings`.
- It owns document logo, document company name, document address, document tax ID, and A4 template style.
- `updateFinanceDocumentSettings()` writes `financeDocumentSettings` and also maps the document template back to top-level `invoiceTemplate` for compatibility.
- `resolveA4DocumentBranding()` still falls back to Store Profile fields such as `logo`, `name`, `location`, `taxNumber`, `phone`, `email`, `website`, and `slogan`.

Risk:

- Compatibility fallback is acceptable, but future agents must not confuse fallback fields with invoice-document ownership.
- Top-level `invoiceTemplate` remains a legacy bridge and should not be treated as the primary invoice setup source.

### Website Template Setup

Current state:

- `ThemeEditor.tsx` owns storefront theme and layout fields such as `template`, `templateColors`, `heroLayout`, `productDisplayType`, `contactFormStyle`, `storeBackgroundImage`, `galleryImages`, `sectionOrder`, `menuStyle`, and visual style.
- `AdminTemplates.tsx` is still present and may overlap with Theme Editor.

Risk:

- Website template ownership is split between legacy template setup and the newer Theme Editor.
- Future work should clarify whether `AdminTemplates.tsx` is legacy, entry point, or still authoritative for any fields.

## Known Misplacement / Review Items

1. **Invoice numbering remains in Store Profile.**
   - Fields: `invoiceNumberPrefix`, `lastInvoiceNumber`.
   - Current UI: `AdminProfile.tsx` section titled "Invoice numbering".
   - Current order code: `AdminOrders.tsx` reads and increments these fields.
   - Required decision: move invoice numbering to Invoice/Finance settings, or document that order numbering is an operational store setting separate from A4 template.

2. **Tax number exists in Store Profile and Invoice Document Setup fallback.**
   - Store Profile field: `taxNumber`.
   - Invoice document field: `financeDocumentSettings.documentTaxId`.
   - Required decision: Store Profile tax number should be legal/business default; Invoice Document Setup can override document tax display.

3. **Logo ownership is split by intent.**
   - Store Profile: `logo`, `logoUrl` for shop/website header.
   - Invoice Document Setup: `financeDocumentSettings.documentLogo` for A4/PDF.
   - Required rule: never reuse shop logo as document logo except fallback preview/default.

4. **Website template setup may be split between `AdminTemplates.tsx` and `ThemeEditor.tsx`.**
   - Required review: decide which page is the authoritative website template setup surface.

5. **Payment gateway setup is in Store Profile.**
   - This may be acceptable as operational profile setup, but payment availability must also be reflected consistently in checkout, cart/card page, app, and POS.

## Required Fix Plan Before Coding

1. Define field ownership table in code comments/types if needed.
2. Move or redirect invoice numbering from Store Profile if Finance owns it.
3. Keep `financeDocumentSettings` as the primary source for A4/PDF template setup.
4. Treat top-level `invoiceTemplate` as a compatibility bridge until migrated.
5. Clarify `AdminTemplates.tsx` vs `ThemeEditor.tsx` ownership.
6. Add UI links between the three surfaces:
   - Store Profile -> Website Theme.
   - Store Profile -> Invoice Documents.
   - Invoice Documents -> Store Profile for fallback business identity.
   - Website Theme -> Store Profile for shop logo/business name.
7. Verify no save path overwrites another surface's owned fields.

## Future-Agent Gate

Before changing Store Profile, Invoice Template setup, or Website Template setup, answer:

1. Which setup surface owns this field?
2. Is this field source of truth or fallback?
3. Which pages read it?
4. Which pages write it?
5. Does mobile or POS read it?
6. Does a script/backfill write it?
7. Does NIPCO invoice-template lock apply?
8. What docs were updated?

If ownership is unclear, stop and update this page before implementation.
