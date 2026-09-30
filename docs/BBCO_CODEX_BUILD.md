# BBCO Codex Build Guide

1. Read `docs/BBCO_WEBSITE_SPEC_v1.md` first. Treat it as the source of truth.
2. Build **Week 1 only** unless the founder explicitly authorizes the next week.
3. Week 1 scope is:
   - authentication
   - Stripe Creator $29/month
   - Stripe Pro $99/month
   - $69 dummy one-off purchase
   - core entitlement data model
   - dummy ZIP
   - private object storage
   - expiring signed download URL
   - download event logging
   - certificate record / first certificate output
   - period-end cancellation that preserves historical records
4. Do not polish UI before the technical milestone works.
5. Do not invent pages, packs, plans, discounts, trials, DRM, team administration, APIs, or marketplace functionality.
6. Any item marked `COUNSEL` remains provisional. Build the architecture so final language/rules can be swapped without redesigning the data model.
7. The Week 1 acceptance test is:

   **pay → entitle → download dummy ZIP → issue certificate → cancel → preserve download/certificate history**
