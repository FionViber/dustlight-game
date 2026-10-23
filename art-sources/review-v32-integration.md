# V0.32 — Entrances, railway travel and indoor post

## Delivered scope

The existing twelve scene paintings were individually audited for door readability. Focused native-resolution edits close secondary depot doors and open a larger central public entry; the post-office door, school central door and church tower door now open, while the store side delivery door and waiting-room storeroom close. Already unambiguous exits and non-navigable closed doors are retained. No floating door markers were added. Current native paintings remain 5760×2160.

A new postal lobby uses twelve native 1254×1254 generated detail tiles, assembled without enlargement. Original-position exit and counter cutouts provide interaction; the counter front occludes the clerk. A visible-counter-over-hidden-actor interaction defect was found in browser QA and fixed in the shared scene handler.

Postal letters can only be collected inside the post office. Outdoor sacks are decoration. Arrival remains silent; collected letters retain arrival/collection dates and enter the scrapbook once. Ruth now appears behind the service opening, and Elsie stands clear of the exterior doorway.

The railway panel now uses an extensible destination catalogue; only the existing New York home visit is enabled. Its one-calendar-month journey and $100 gameplay fare are unchanged. The lost-property ledger is a separate open book on the waiting-room luggage cart. Its reference to the object below it now says trunk, matching the painting.

## Evidence and limits

569 tests, TypeScript and 19 production-resource checks pass. Browser QA covers physical door clicks, English railway panel, rapid double departure (only one month charged), actual indoor postal counter click overlapping the clerk silhouette, collect twice prevention, empty inbox, restored interior save, and Chinese postal layout. Scene screenshots are in previews/v32; specific screenshot notes are in work/v32/UI_QA.md.

Historical postal service evidence comes from the 1885 general-delivery notice in the University of South Carolina newspaper archive. Later western interior descriptions and museum objects inform plausible furnishings; this is an authored reconstruction, not an exact surveyed 1885 Carson interior. See v32/door-audit-fixes/door-audit.md and v32/post-interior/REPORT.md for sources, generation prompts and pixel checks.

Original artwork and the previous V0.31 ZIP are retained. New approved art is centrally browsable in art-library using verified same-volume hardlinks; this is not claimed as additional disk savings. No reference originals were modified. The production release is the same static file set online and offline. Native file:// browser automation remains unavailable; static file compatibility is covered by loader/packaging checks and same-file HTTP browsing, not claimed as a native file protocol run.

This bounded change does not complete deferred four-season/night artwork, wider travel destinations, future family story hooks, actual voice acting or Steam packaging.
