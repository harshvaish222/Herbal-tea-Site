# AI prompt log and implementation notes

This implementation was created by editing the supplied `index.html` against `README(2).md` and `BRAND(1).md`. The image-generation tool returned unrelated code/tutorial screenshots instead of tea imagery on two attempts; those outputs were rejected and are not included. The supplied prompts from the previous planning response were suggested prompts, not all actually executed; they are therefore not falsely recorded as used prompts here.

## Prompts
- Tool: ChatGPT (GPT-6)
- Type: code
- 

## Prompt 1 — Audit the existing code
Review the existing index.html, BRAND.md, and README.md for the Mistvale Tea Co. online store assessment.

Do not modify any files yet. Inspect the HTML, CSS, and JavaScript, especially the product rendering, search, filters, sorting, quick view, cart, coupons, delivery checker, newsletter, countdown, and checkout.

Identify every functional bug you can find, including bugs involving asynchronous search responses, empty localStorage, incorrect array sorting, product stock limits, cart quantity calculations, repeated event listeners, discount calculations, shipping thresholds, and checkout submission.

Compare the implementation against every business rule and design constraint in README.md and BRAND.md.

Return:
1. A prioritized bug list.
2. The affected functions or sections.
3. The expected behavior.
4. A proposed implementation plan.

Do not change product IDs, names, or prices in PRODUCTS. Do not modify the API object or approved footer legal text. Keep all application CSS and JavaScript inside index.html. Do not add frameworks or libraries.

## Prompt 2 - Fix product search, filtering and sorting
Fix the product discovery functionality in index.html.

Requirements:
- Search product names and descriptions using the existing API.search() method.
- Handle asynchronous search responses safely so an older, slower request cannot overwrite newer results.
- An empty search must show products matching the selected category and sort order.
- Fix the category filter so All shows every category and Black, Green, Herbal, and Gifts work correctly.
- Search, category filtering, and sorting must work together without resetting one another.
- Implement correct numeric ascending and descending price sorting and alphabetical name sorting.
- Sold-out products must always appear last, regardless of the selected sort order.
- Handle no-result searches with a useful empty state.
- Prevent unsafe or incorrect array-index checks.
- Avoid adding unnecessary event listeners or third-party dependencies.

Keep the original PRODUCTS data unchanged. Do not modify the API object. Preserve the single-file HTML/CSS/JavaScript requirement. Test combinations of search, filters, and sorting.

## Prompt 3 — Fix product cards, quick view and wishlist
Repair and improve the product card rendering, quick-view modal, and wishlist in index.html.

Requirements:
- Each product card must display its correct image, name, description, category, and INR price.
- Display ratings and review counts only for products that actually have rating data. Do not invent ratings or review counts.
- Sold-out products must have a visible Sold out status and a disabled Add to cart button.
- Fix product image click handlers so each image opens the correct product in quick view. Do not use an incorrect loop index or stale variable.
- Add accessible buttons for opening and closing quick view, with Escape-key support, appropriate dialog semantics, focus handling, and mobile-friendly sizing.
- Make wishlist controls operate on the individual product rather than toggling every heart simultaneously. Persist wishlist state using localStorage if practical.
- Add visible feedback when a product is added to the cart.
- Use safe DOM construction or correctly escaped values.
- Maintain consistent card heights and keyboard accessibility.

Keep PRODUCTS unchanged and use plain HTML, CSS, and JavaScript without frameworks.

## Prompt 4 — Repair the cart calculations and quantity controls
Completely audit and repair the shopping cart logic in index.html while preserving the existing PRODUCTS data, API object, and checkout form contract.

Business rules:
1. Product prices must always come from PRODUCTS, never from displayed text.
2. A shopper may purchase no more than 5 units of a product or more than its available stock.
3. Sold-out products cannot be added.
4. Initialize the cart safely when localStorage is empty, missing, invalid JSON, or contains stale data.
5. Validate saved cart entries against PRODUCTS and ensure quantities are valid integers.
6. Adding a product must increment the existing quantity correctly or create a new line.
7. Plus and minus buttons must update quantities correctly. Never allow a quantity below 1; provide an accessible remove action.
8. Removing a product must remove only that line.
9. Recalculate cart count using total units, not the number of distinct product lines.
10. Display subtotal, shipping, discount, and final total accurately.
11. Format all currency using the Indian locale, with the ₹ symbol and Indian digit grouping.
12. Render an informative empty-cart state.
13. Ensure event handlers are not repeatedly registered every time the cart renders.
14. Update localStorage and the cart UI consistently after each change.

Use ₹49 shipping, with free shipping determined by the assessment's post-discount threshold of ₹599. Do not alter product IDs, names, prices, the API object, or the checkout form. Explain the corrections and test multiple cart lines, quantity limits, empty carts, and invalid saved data.

## Prompt 5 — Fix coupon logic, totals and checkout
Implement the coupon, pricing, shipping, and checkout rules specified in README.md.

Coupon requirements:
- The coupon code is WELCOME10 and matching is case-insensitive.
- The cart subtotal must be at least ₹399 to qualify.
- Gift boxes, identified by category Gifts, are excluded from the discount.
- Apply 10% off eligible product lines, capped at ₹150 per order.
- Applying the coupon repeatedly must never stack discounts.
- Recalculate the discount correctly when quantities change or items are removed.
- Show helpful inline feedback for invalid, ineligible, and successfully applied coupons.
- Ensure the displayed applied state cannot become inconsistent with the actual calculation.

Pricing requirements:
- Use original prices from PRODUCTS.
- Keep intermediate calculations accurate and round only the final total to the nearest rupee.
- Shipping is ₹49 unless the amount after discount reaches ₹599, in which case it is free.
- Format amounts as Indian rupees with Indian digit grouping.

Checkout requirements:
- Keep the existing checkout form ID, action URL, POST method, and fields named items and coupon.
- When Checkout is clicked, populate items with a JSON array such as [{"id":101,"qty":2}] and coupon with the applied code or an empty string.
- Do not replace checkout submission with a fake alert or simulate an order success.
- Prevent checkout with an empty cart and provide an accessible explanation.
- Prevent accidental duplicate submission.

Do not change the PRODUCTS data, API object, or approved footer legal text. Return the corrected implementation and explain edge cases tested.

## Prompt 6 — Fix delivery checking and newsletter
Fix the delivery checker and newsletter form in index.html.

Delivery checker:
- Continue using the existing API.checkPincode() method without changing the API object.
- Validate input and handle rejected promises.
- Show a helpful inline error for an invalid six-digit Indian pincode.
- Show the estimated delivery time in working days when serviceable.
- Show a clear not-serviceable message when the API returns serviceable:false.
- Ensure the interface never remains stuck on Checking.
- Handle repeated requests safely and communicate loading state accessibly.
- Avoid unsafe innerHTML for user-provided values.

Newsletter:
- Replace the existing placeholder-only input with a properly labeled email field.
- Validate email input using HTML validation and JavaScript.
- Show accessible inline errors and a clear success state.
- Do not invent backend subscription functionality or claim that an email was actually sent when no subscription API exists.
- Remove the automatically appearing newsletter popup. Keep newsletter signup inline as required by BRAND.md.
- Make all controls keyboard accessible.

Preserve the existing API object and all business facts. Use plain JavaScript, semantic HTML, and CSS.

## Prompt 7 — Create the premium visual design
Redesign the entire visual system of the Mistvale Tea Co. storefront in index.html using BRAND.md as the strict design specification.

Brand:
- Tea green #1f3d2b, leaf #4f7942, cream #f6f1e7, parchment #ebe2cf, saffron #d9962b, ink #1b1b1b, and error #b3261e.
- Define all brand colours as CSS custom properties. Do not introduce unrelated colours.
- Use exactly two Google Font families, loaded through one Google Fonts link with display=swap: Fraunces for headings and DM Sans for body text.
- Body text 16px, small text at least 14px, h3 20–24px, h2 28–40px, and h1 40–64px using clamp().
- Content max-width 1200px and spacing based on 8px increments.
- Use one consistent corner radius across the site.

Replace the existing amateur design with a calm, premium, earthy aesthetic inspired by tea gardens, natural light, linen, wood, and stone.

Implement:
- Refined announcement strip and header.
- Simple text-and-leaf Mistvale logo.
- Clear, responsive navigation and cart indicator.
- Elegant hero with one clear value proposition and one primary Shop the teas CTA.
- Trust strip based only on verified company facts.
- Polished product cards with consistent proportions and visible controls.
- Attractive delivery checker, review section, FAQ, newsletter, and footer.
- Clear hover, active, disabled, and focus-visible states.
- Buttons at least 44px tall.
- Subtle 150–300ms transitions on specific properties, never transition:all.
- prefers-reduced-motion support.

Remove Comic Sans, neon colours, unrelated fonts, Font Awesome, animate.css, jQuery, marquee effects, blinking elements, exaggerated animations, fake sale countdowns, fake awards, and unverified marketing claims.

Keep all CSS and JavaScript inside index.html. Do not add frameworks or external JavaScript libraries. Preserve the business rules and legal footer text exactly.

## Prompt 8 — Make the layout mobile responsive
Improve the responsive layout of index.html for the Mistvale Tea Co. store.

Test and optimize the layout for widths of 360px, 375px, 390px, 768px, 1024px, and 1440px.

Requirements:
- No horizontal page scrolling at any viewport.
- Use a centered maximum content width of 1200px with 16px side padding on phones.
- Display two product columns on phones, three on medium screens, and four on larger screens where space permits.
- Keep product cards visually consistent in height.
- Ensure product images maintain a square aspect ratio and use object-fit:cover.
- Stack hero content appropriately on mobile and ensure the primary CTA remains visible.
- Make navigation, search, filter controls, sorting, cart drawer, quick view, delivery checker, FAQ, and newsletter usable with touch.
- Ensure the cart and modal fit within the viewport and their contents remain scrollable when needed.
- All important controls must have at least 44px touch targets.
- Avoid fixed widths that cause overflow.
- Add responsive typography with clamp().
- Respect prefers-reduced-motion.

Do not add frameworks or external JavaScript libraries. Keep CSS inside index.html and preserve all working JavaScript and business rules. Report any remaining layout issues after checking the specified widths.

## Prompt 9 — Add the required sections and accessible FAQ
Complete the required storefront sections in index.html in the exact order specified by BRAND.md:

1. Optional announcement strip with one short, truthful line.
2. Header with logo, navigation, search access, and a cart button with item count.
3. Hero with a clear value proposition, one primary Shop the teas CTA, at most one secondary CTA, and an image.
4. Trust strip with three or four short, verifiable promises.
5. Shop with category filters, search, sorting, and product grid.
6. Delivery checker.
7. The three existing customer review quotes.
8. FAQ as an accessible accordion.
9. Inline newsletter signup.
10. Footer with verified company contact details and the existing legal text.

Use the six approved FAQ questions and answers from BRAND.md exactly. The FAQ accordion must work with keyboard input, use buttons with aria-expanded and aria-controls, and maintain visible focus states.

Do not invent testimonials, ratings, review counts, delivery promises, awards, discounts, or company facts. Only two products have real ratings, and the three existing review quotes must not be given invented numerical ratings.

Correct the footer spelling to Mistvale where the brand name is displayed, but preserve the approved legal paragraph exactly, including its existing wording and copyright text.

Use semantic HTML and maintain a logical heading hierarchy. Keep everything in the single index.html file without frameworks.

## Prompt 10 — Add SEO and structured data
Make index.html SEO-ready according to BRAND.md and README.md.

Requirements:
- Write a unique 50–60 character title and a 120–160 character meta description.
- Add a canonical link using the provided website URL, https://mistvale.example.
- Add Open Graph and Twitter card metadata.
- Use exactly one H1 and a logical H2/H3 hierarchy.
- Add JSON-LD structured data for Organization or OnlineStore using only verified company facts in BRAND.md.
- Add Product structured data for all eight products, including prices in INR and availability derived from stock.
- Include aggregate rating data only where genuine rating information exists in PRODUCTS. Never invent ratings, reviews, or counts.
- Add FAQPage JSON-LD using the six approved FAQ questions and answers in BRAND.md.
- Keep structured data synchronized with the actual page content and original product data.
- Ensure JSON-LD is valid JSON and safely serialized.
- Include descriptive alt text for meaningful images and use empty alt text for purely decorative imagery.
- Do not add unsupported SEO claims, invented addresses, false offers, or fabricated company facts.

Preserve the single-file constraint and do not change the PRODUCTS IDs, names, or prices. Explain how to validate the resulting metadata and JSON-LD.

## Prompt 11 — Accessibility and performance audit
Audit and improve accessibility and performance in the completed Mistvale Tea Co. index.html.

Accessibility:
- Use semantic HTML and accessible names for every interactive element.
- Ensure all functionality works with keyboard only.
- Add visible :focus-visible states and do not remove outlines without replacement.
- Use proper labels, accessible inline validation, and appropriate live regions for cart, search, delivery, and newsletter updates.
- Make modals and the cart drawer keyboard accessible, with Escape handling and focus management.
- Ensure body text contrast meets WCAG AA, at least 4.5:1.
- Respect prefers-reduced-motion.
- Keep touch targets at least 44px tall.

Performance:
- Remove unused dependencies, including jQuery, Font Awesome, and animate.css.
- Avoid unnecessary reflows, duplicated event listeners, and excessive DOM rendering.
- Add width and height or aspect-ratio to images to prevent layout shifts.
- Lazy-load below-the-fold product images and avoid lazy-loading the main hero image.
- Use optimized WebP assets and descriptive alt text.
- Keep all CSS and JavaScript inside index.html.
- Do not introduce frameworks or unnecessary dependencies.

Provide a checklist of the remaining issues and suggest how to validate them with browser developer tools, Lighthouse, and keyboard-only testing. Do not claim tests were run unless you actually ran them.
