# V0.21 historical media delivery

These holdings belong to a separate viewing/listening gallery, as approved by the user. They are dated in the catalogue and must not be presented as films or records available during the 1885 story.

## Holdings and provenance

| Holding | Publication | Local duration | Bytes | Primary catalogue |
|---|---|---:|---:|---|
| The Great Train Robbery | 1903 | 10:30 | 54,927,744 | [Library of Congress](https://www.loc.gov/item/00694220/) |
| Jack and the Beanstalk | 1902 | 8:46 | 46,287,563 | [Library of Congress](https://www.loc.gov/item/00694228/) |
| Mr. Thomas Cat — Edison Grand Concert Band | Dec. 1900 | 2:16 | 1,634,014 | [NPS, EDIS 4795 / B-517](https://www.nps.gov/edis/learn/photosmultimedia/recordings.htm) |
| Spring of Love — Eugene Jaudas and Louis Atz | June 1903 | 2:18 | 1,668,182 | [NPS, EDIS 4791 / 8404](https://www.nps.gov/edis/learn/photosmultimedia/popular-instrumental-and-ragtime.htm) |
| Stars and Stripes Forever March — Sousa's Band | Nov. 1909 | 4:32 | 3,269,070 | [NPS, EDIS 36682 / 4M-285](https://www.nps.gov/edis/learn/photosmultimedia/recordings.htm) |

Film files come from the Internet Archive silent-film collection, not from a successful direct LoC download. Exact download URLs, byte counts, SHA-256 hashes, stream details, and full-decode results are in `media-provenance.json`; the two Archive metadata responses are preserved alongside it. NPS MP3s are unchanged downloads from the official park website.

The original 1902/1903 films are U.S. public-domain works. LoC provides the film identity, publication dates and [collection rights statement](https://www.loc.gov/item/00694220/?loclr=blogloc). Both downloaded films have **no audio stream**, avoiding distribution of a later accompanist's score. The Jack copy has a restoration credit card mentioning music, but the delivered file is silent. Credit: Library of Congress, Motion Picture, Broadcasting, and Recorded Sound Division.

The three historic recordings were published before 1923. The U.S. Copyright Office explains that this category entered the U.S. public domain on January 1, 2022 ([official letter](https://www.copyright.gov/laws/hearings/letter-to-senator-udall-on-noncommercial-use-exception.pdf)). Transfers are credited to Thomas Edison National Historical Park, National Park Service. This is a U.S. rights assessment, not an assertion that every NPS web asset or every jurisdiction has identical terms.

LoC's Jack record specifically does **not** confirm the commonly repeated George S. Fleming credit; the game therefore credits Edwin S. Porter and Arthur White. Local file durations differ from LoC's timings at archival projection speeds. Footage was not stretched to satisfy a target length, and the catalogue displays the measured local duration.

## Player implementation

- `MediaRoom.tsx`: separate film catalogue/cloth projection view and custom gramophone catalogue/player. Props: `kind`, `lang`, `onClose`, `volume?`, `onPlaybackChange?`.
- `media-catalog.ts`: localized titles, dates, credits, summaries, source URL and offline file locations. Replace/add a holding here without rewriting the player.
- `media-controller.ts`: one owned stream, explicit play/pause/selection, stale-promise suppression, visibility pause/resume, volume and complete disposal. Opening the catalogue does not set or preload a media source.
- Films have no native controls, seeking, pause, volume, picture-in-picture or remote-playback UI. Only leave is available during playback. End/error states allow another play attempt.
- Records use game-art play/pause and next buttons. Parent App owns background-music suppression through `onPlaybackChange` and passes global audio settings via `volume`.

## Art

Generated with the current built-in image tool. Existing cinema illustration was used only as a style reference. No reference-library files were modified.

`scene-screening-room-v21.png` is the original generated **1672×941** image; runtime WebP preserves these dimensions. It is a small, frontal, wood-and-curtain picture hall with a blank screen. A 4K result was requested but not returned; this asset is not claimed to be native 4K. The projection area was checked visually in the browser and preserves film aspect ratio with `object-fit: contain`.

`ui-guide-arrow-v21.png` is the original transparent arrow; runtime export is 512×512 WebP. The coarse cream-paper arrow is symmetrical and has no text or baked interface. `asset-fragment.json` provides hashes and runtime dimensions for the parent asset manifest.

## Validation

2026-10-14: all five delivered files fully decoded through ffmpeg with exit 0 and no error output. Film files stay under 100 MB and all MP3s under 5 MB. The train film is 54.9 MB; Jack is 46.3 MB, preserving the downloaded archival copies.

`node node_modules/tsx/dist/cli.mjs --test tests/v21-media.test.ts`: four tests passed, covering payload limits, no initial streaming, play/pause/replay/next, stale callbacks, visibility handling, teardown, errors and volume.

Actual browser verification: first film played with `currentTime=6.496`, `duration=630.53`, `paused=false`, `controls=false`; its video fitted the painted screen correctly. Final screenshot capture and second-film/gramophone UI checks are handed to the parent after concurrent CUA sessions interfered. Do not use the stale `cinema-playing.png` captured during a hot reload as cinema evidence.
