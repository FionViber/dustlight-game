# V0.27 Falling Blocks rule and license review

Reviewed 2026-10-19 before implementation. Player-facing names are 俄罗斯方块 (Chinese) / Falling Blocks (English). This is an independent leisure game, not an 1885 historical activity.

Primary implementation inspected: Jake Gordon and contributors, [javascript-tetris repository](https://github.com/jakesgordon/javascript-tetris), [actual implementation](https://github.com/jakesgordon/javascript-tetris/blob/master/index.html), and [MIT license](https://github.com/jakesgordon/javascript-tetris/blob/master/LICENSE). The source demonstrates a 10×20 well, seven four-square shapes, collision checks, rotated forms, a finite random piece pool, gravity, row compaction and a next-piece preview. Its author explicitly lists touch and high scores as future work. Its existing skin, texture, markup, source code and assets were not imported.

The MIT file identifies Jake Gordon and contributors (2011–2016), permits reuse/modification/distribution, and requires retaining its notices for copied substantial software. We reviewed the implementation as evidence for rules and independently wrote a typed pure state engine and Dustlight UI. No third-party runtime code or visual content is shipped from this project; therefore no copied MIT software notice is needed in the runtime. The links remain in provenance.

## Independent rules selected

- 10 columns × 20 visible rows; seven tetrominoes. Rotation is mathematical in a 3×3 square (I in 4×4, O fixed). A short ordered set of horizontal and upward corrections handles walls and floor. This is a documented modest wall/floor kick system, not a claim of official SRS or branded tournament compliance.
- Fisher–Yates seven-bag: exactly one of each shape per bag. A saved queue carries the remaining pieces across save/load; the next three are shown. This differs deliberately from the reference's four-copies-per-shape random pool.
- A 500 ms grounded lock delay, with at most 15 successful grounded movement/rotation resets. Gravity starts at 850 ms/row, becomes 0.82 times as long every ten lines, and bottoms out at 80 ms/row. A new/held piece starts with a fresh timer. Backgrounding pauses; there is no catch-up burst on return.
- Score per simultaneous 1/2/3/4 lines is 100/300/500/800 times the pre-clear level. Soft drop awards 1 per traveled cell; hard drop awards 2. Soft drop never locks immediately; hard drop locks precisely one piece. Holding Space cannot repeatedly hard-drop newly spawned pieces.
- Hold once per piece, reset orientation on swap; ghost landing outline; full top-row detection; stable compaction; blocked spawn or locking above the ceiling ends the round. A hold that cannot spawn also ends the round.
- Arrows/WASD, Q/Z reverse turn, C hold, Space hard drop, P/Enter pause. On-screen image controls and conservative tap/swipe gestures. Restart uses the existing shared confirmation. Auto pause on blur, hidden tab, view exit, modal suspension, and restored saves. Starting and pointer controls return focus to the board; deliberately Tab-focused buttons keep ordinary keyboard activation.
- Score, lines, best score/lines, lifetime cleared rows/four-line clears, board, active piece, queue and held piece are saved through the existing world-neutral minigames commit. Timer/animation frames never enter the save.

The board frame is newly generated `board-falling-v27`. Blocks reuse the existing square slot art with restrained translucent colors; all labels are live text in the supplied font. The image is shown with its native aspect and a separate 250×500 playable grid. No borrowed website skin or external runtime requests.

Verification: engine cases are in `tests/v27-falling-blocks.test.ts`; parent integration owns production/browser validation, including shared world pause, save/load, keyboard, actual artwork safe area and existing minigame regressions.
