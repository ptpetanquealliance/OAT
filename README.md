# OAT — Outil d'attribution des terrains

**OAT** (French for "Terrain Assignment Tool") is a free, single-file web app that helps Pétanque tournament directors assign matches to courts round by round — automatically balancing court usage, surface variety, and repeat play so no team gets stuck on the same court or terrain all day.

There's nothing to install and no account to create. Open the page in a browser, and it runs entirely on your device — including offline, with no internet connection required after the initial load.

## Getting started

1. Download [`OAT.html`](./OAT.html).
2. Open it in any modern browser (Chrome, Safari, Firefox, Edge) — double-click the file, or drag it into a browser window.
3. Enter your number of courts, optionally define court surfaces, and start pasting in match pairings round by round.

For full instructions — running a round, understanding the constraint settings, saving data safely, and running multiple tournaments at once — see the [User Manual](./OAT_User_Manual.md) (also available as [PDF](./OAT_User_Manual.pdf)).

## How it works

Each round, OAT takes your list of match pairings and works out the single best combination of courts for the *entire* round at once, rather than assigning courts one match at a time. It scores every possible match-to-court combination using a set of configurable penalties, then solves for the lowest-cost overall assignment with the Hungarian algorithm (Kuhn–Munkres). Penalties account for:

- Playing the same court two rounds in a row
- Playing the same surface type two rounds in a row
- Returning to a court played earlier in the tournament
- How often a team has played on a given surface
- A configurable per-court usage cap
- Optional "showcase courts" that pull top-seeded matches toward a center/spectator court

All of these weights are adjustable in the UI, with sensible defaults for most club-level events.

## Data & privacy

OAT keeps all tournament data in your browser's local storage — there is no server, no account, and no data ever leaves your device. This also means your data lives only in the browser and device you started on; see the [User Manual](./OAT_User_Manual.md#4-saving-your-data-and-how-not-to-lose-it) for tips on avoiding data loss and running multiple simultaneous tournaments.

## License

Released under the [MIT License](./LICENSE).
