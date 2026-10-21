# Mistvale Tea Co. — implementation notes

## What changed
- Rebuilt the single-file store with a responsive tea-green/cream visual system, Fraunces headings and DM Sans body copy, accessible focus states, reduced-motion support, and mobile-first product cards.
- Replaced external CSS/JS libraries, blinking sale text, unsupported Shark Tank claim, fake countdown and automatic newsletter popup. Added clear navigation, inline newsletter, FAQ accordion, delivery checker, original vector logo/hero/product art, and metadata/JSON-LD.
- Implemented composable category/search/sort, sold-out-last ordering, quick view, wishlist toggles, cart drawer, local cart persistence, stock/max quantity limits, coupon rules, free-shipping threshold, Indian currency formatting and checkout form submission contract.
- Preserved all original product IDs, names, prices, the `API` block and the approved footer legal paragraphs exactly.

## What AI got wrong / review notes
- Two image-generation attempts returned unrelated programming/code tutorial screenshots instead of tea imagery. Both were rejected and are not in the submission. This was caught by inspecting the actual returned files.
- The original page contained unverified claims (including a Shark Tank badge and a customer-count/rating headline), expired sale countdown, made-up zero-rating display for unrated products, and a newsletter popup. These were removed rather than repeated.
- Product images in this build are hand-authored SVG illustrations, not generated photography; that is a known compromise against the requested AI imagery.

## Images and processing
- `images/logo.jpg`, `images/hero-banner.jpg`, and `images/p101.jpg`–`p108.jpg` are original vector artwork authored directly for this build. They are resolution-independent and lightweight; no raster conversion or external image service is used. Product art shares a 1:1 viewBox and restrained brand palette.

## Testing performed
- Reviewed business-rule logic against README: product prices come from `PRODUCTS`; stock and maximum quantity are enforced; WELCOME10 is case-insensitive, single-use, subtotal-gated, capped at ₹150 and excludes Gifts; shipping is ₹49 and free at ₹599 after discount; only final displayed money amounts are rounded; sold-out products sort last; delivery check handles invalid input, unserviceable postcodes and API rejection.
- Checked HTML/JS structure and verified the protected API block and footer legal paragraphs remain unchanged.
- Automated browser testing, Lighthouse, and physical-device testing have not been run in this environment. Please run through Chrome at 360px, tablet and desktop widths before submission.

## Questions for the team
- The brief states free shipping at ₹599; the original announcement claimed ₹499. I followed the brief's explicit ₹599 rule and removed the contradictory announcement.
- Newsletter sign-up has no real endpoint in the starter kit; the inline form therefore validates input and clearly tells the user it is a demo, without claiming an email was sent.
- The website and email use the supplied `.example` domain and are treated as assessment placeholders.

## Time spent
- Estimated active implementation time for this pass: about 1.5 hours. Browser QA and accessibility audits remain outstanding.

## Extra features
- Wishlist toggles for the current session, quick-view modal, localStorage cart recovery, accessible cart drawer, and a clear-filter control.

## With more time I would
- Replace the vector illustrations with a reviewed set of AI-generated, photo-realistic product images; run keyboard/screen-reader tests and Lighthouse; test all cart/coupon edge cases in a real browser; and connect newsletter sign-up to a real service once one is specified.
