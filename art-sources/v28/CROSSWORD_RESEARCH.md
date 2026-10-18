# V0.28 English crosswords

Reviewed 2026-10-19. All puzzle content, clues, controls and feedback remain English in both game languages. This is an independent pastime, not a claim that newspaper crosswords were available in the 1885 story setting.

## Primary implementation reference

- [Exolve, original repository by Viresh Ratnakar](https://github.com/viresh-ratnakar/exolve)
- [Exolve MIT license](https://github.com/viresh-ratnakar/exolve/blob/master/LICENSE)
- [Exolve documentation](https://github.com/viresh-ratnakar/exolve/blob/master/README.md)

The review informed familiar crossword interaction: numbered starts, separate Across and Down clues, shared crossing letters, selection of an entire answer, typing and directional movement, checking and explicit reveal assistance. Exolve also documents a compact A–Z on-screen keyboard. No Exolve code, puzzle, clue text, stylesheet or visual asset was copied or included. Dustlight's engine and React view are independently implemented, use existing local illustrated board/button/slot assets and make no external runtime requests.

## Puzzle construction

Three original 5×5 blocked mini crosswords were constructed for this release. They have 19 white cells and ten distinct answers each, 180-degree block symmetry, one connected white area, answers of three to five letters, and every white cell crossed in both directions. Across and Down do not repeat the same answer. Every clue was written for this release in plain English; there are no borrowed newspaper puzzles, proprietary clue collections, invented abbreviations or cryptic-clue conventions.

Construction scratch work used a small independent constraint search and manual selection/review of the resulting ordinary words. A research-only [common-word frequency list](https://github.com/first20hours/google-10000-english) helped find possible crossings; its [license note](https://github.com/first20hours/google-10000-english/blob/master/LICENSE.md) was checked. That corpus, its frequencies, and its files are **not distributed**. Only the selected ordinary words and our newly composed grids/clues are part of the game. Scratch files remain outside outputs, in work/v28/crossword.

| Sheet | Across answers | Down answers in clue-number order |
|---|---|---|
| The Quiet Mile | THE, WEST, OASIS, TALE, YET | TWO, HEAT, ESSAY, TILE, SET |
| Table Talk | CAT, RACE, PASTA, AGES, YES | CASES, ACTS, TEA, RAGE, PAY |
| Out and About | SEA, ARTS, WALKS, SAIL, SPY | SAW, ERAS, ATLAS, SKIP, SLY |

Table Talk's first three Down starts are on the top row, before the starts in the left two columns. Its clue order is therefore CASES, ACTS, TEA, RAGE, PAY, not left-to-right column order. The tests explicitly bind all thirty numbered clues to their intended answer and a distinguishing clue phrase to catch this class of construction mistake.

## Rules and persistence

- Click a clue or square; clicking the current square toggles Across/Down. A–Z fills one letter and advances to the next empty square in the answer. Arrow keys move spatially, Space switches direction, Enter selects the next clue, and Backspace/Delete erase. The same letters are available on illustrated screen keys.
- Check reports wrong filled letters without revealing their solution. Reveal letter supplies one missing/incorrect letter in the selected word, visibly in green ink. Blank cells are not reported as errors.
- All three sheets retain letters, selection, direction, checks and assistance when switching sheets and across saves. Restart clears only the current sheet; solved IDs and the unique completion count remain. Completing the same sheet repeatedly cannot generate extra completion credit.
- The crossword is deterministic and world-neutral. It uses the existing modal pause, save and minigame integration; no story time, stamina, satiety or money is spent.
- The 820×820 illustrated board and wide clue/input column fit the full-screen 1920×1080 minigame stage. Existing shared illustrated controls and custom ScrollArea are reused. Hover does not move controls or play sound.

## Verification

Nine engine tests pass: grid validity/connectivity/checking/symmetry, explicit thirty-clue mapping, typed crossing letters, direction/navigation/black cells, wrong-letter checking and correction, reveal/save behavior, sheet persistence, unique completion/reset semantics, and canonical save decoding. Root's three V0.28 integration tests also pass with the real save model and achievements. TypeScript passes after component integration. Visual QA belongs to the integrated full-screen build and is recorded by the release owner.
