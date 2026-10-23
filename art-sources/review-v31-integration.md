# V0.31 — Home and post-office systems

Clara Ward's home is New York. The existing ticket ledger in the depot waiting room opens the home-trip offer. Its lost-property text remains accessible from that offer. The painted mailbag outside the post office opens the postal counter. Neither service is in the Field Companion menu.

A confirmed trip costs $100 in the initial balance and lasts one Gregorian calendar month, with month-end clamping. This is a gameplay fare, not a researched historical tariff. It includes ordinary meals and sleep: return stamina is 100 and fullness 60, existing illness durations advance, previous daily job allowances expire, and assigned cat work becomes ready without automatically claiming wages. The full round trip must fit before the campaign closes. The transaction records one journey, one charge and one diary entry, then returns to the station exterior. Confirmed travel uses the shared fade and scene-entry readiness gate.

An initial letter from Mother in New York arrives on game day 3 at 08:00. Arrival is silent and does not enter the diary, scrapbook, notice feed or a menu badge. Only the post office can reveal and collect waiting mail. Collection records one dated letter in the scrapbook's Letters category, retains sender/origin/arrival/collection dates, and uses the normal acquisition feed. Reopening the postal counter after collection shows an empty inbox; collected letters remain readable in the scrapbook. Postal panels pause the clock and settle one ordinary reading cost on close.

Future story content uses `postal.ts` letter definitions and stable scheduled delivery IDs, and `home-trip.ts` ordered home/return hook registry. Production home-event registry is intentionally empty. Hooks run in the final return transaction with both departure and return dates available; no playable New York scene or full family quest is claimed.

Verification:
- TypeScript passes. 562 automated tests pass, including 13 new tests for month boundaries, atomic payment, repeat actions, illness and daily systems, hooks, silent mail, pickup, capacity and save validation. An independent 125-case month/date probe also passed.
- 19 static/ephemeral HTTP production checks pass, including on-demand resource wrappers and unchanged original audio/media/font assets.
- Actual static-build browser test: Jan 2 → Feb 2, 1886; rapid double confirmation pays $100 once ($999 → $899), returns outdoors at the depot, and restores normal vitals. Reload returns to the menu and Continue restores the returned state.
- Chinese and English panel screenshots and postal collection/scrapbook review are recorded under `previews/v31`. See `work/v31/UI_QA.md` for bounded UI checks. No claim of exhaustive device or all-story-state coverage.

Historical research: `work/v31/home-post-audit.md` distinguishes contemporary rail/general-delivery evidence from gameplay choices. No new visual assets or changed source artwork. Native browser file-protocol QA remains unsupported by the browser tool; the shared portable build is checked through its existing automated local-resource tests and HTTP execution.
