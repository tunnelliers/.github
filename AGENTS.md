# tunnelliers/.github — profil public de l'org et workflows partagés

- **PUBLIC repo**: everything here is visible to the world. Never put secrets, ids of private experiences, internal
  links or unreleased game details here.
- `profile/README.md` = the org's public page. `.github/workflows/luau-ci.yml` = reusable Luau CI (Rokit authenticated
  with the workflow token, Rojo build, typecheck); keep it in sync with `games/.github/workflows/ci.yml` when the
  install or build steps change there. Issue / PR templates also live here.

<!-- tunnelliers-team-rules:start -->
## Tunnelliers Studio — team rules (for EVERY AI: Claude, Codex, Cursor, Gemini, Copilot...)
Source: `tunnelliers/studio` → `plugins/tunnelliers/team-rules.md`. Copied into every repo's `AGENTS.md` by
`studio/tools/sync_agents.py`. Never edit the copy: edit the source, run the sync, open the PRs.

### Who you work for
Two "vibe coders", not developers: the studio owner (GitHub `bayromest`) and Théo (GitHub `LaTheorieBrutale`,
Roblox BrutalTheoryFR). They say WHAT they want; you do ALL the technical work (git, PRs, tests, CI, Rojo, Studio,
Blender) yourself, without asking them to type commands, and report in simple French with no unexplained jargon.
Both work with AI on the same games at the same time: these rules are the shared contract between their AIs.

### Where things live (never mix them)
| What | Where |
|---|---|
| Game scripts (source of truth) | GitHub `tunnelliers/games` → `games/<game>/src/`, pushed into Studio by Rojo |
| Map, GUIs, models, values, sounds | the Roblox place itself (Team Create) |
| Blender art | GitLab `tunnelliers/<game>-art` (Git LFS + locks), never on GitHub |
| AI rules, skills, onboarding, setup check | GitHub `tunnelliers/studio` |
| Notes + shared decisions log | GitHub `tunnelliers/vault` (`Studio/Decisions.md`) |
| Discord bot | GitHub `tunnelliers/discord-bot` |
Local clones: `D:\a\projects\tunnelliers\<repo>` (art: `CE_ART_DIR`). Every repo: `AGENTS.md` = the instructions
(`CLAUDE.md` only imports it). All commands (tests, checks, Open Cloud): `games/AGENTS.md`. Free tools only.

### Automatic, every time (do it without being asked)
- **Start**: `git pull --ff-only` in the repo you work in (Claude's plugin already pulls every clean clone on `main`
  at session start and says so). Then `gh pr list --repo tunnelliers/<repo>` and, for art, `git lfs locks`: if the
  OTHER person has open work on the same files, say so before touching them.
- **Finish the whole loop yourself**: branch → commit → push → PR → wait for CI (`gh pr checks --watch`) → squash merge
  → `git switch main && git pull`. Merge without asking when CI is green, unless the human said "wait" or the change
  needs a human check in Studio first (then say exactly what to test).
- **Keep the AI context up to date in the SAME PR**: if your change alters how something works, where it lives, a
  command, a rule or a gotcha, update the `AGENTS.md` that describes it (and `vault/Studio/Decisions.md` for a team
  decision). An `AGENTS.md` that lies is worse than none. A rule a script can check → `games/tools/checks.py`.
- **End**: PR merged (or open with the reason), locks released, Rojo not left broken, and a 3-line French summary:
  what changed, what the human must do (test? publish?), what is not done.

### Golden rules (breaking one can destroy the other person's work)
1. **Game scripts are edited in the repo files, never in Studio.** Rojo overwrites Studio edits.
2. **`git pull` before connecting Rojo; the Rojo change list must be EMPTY (or exactly what you expect).** With Team
   Create, older local files overwrite the other person's newer scripts. Unsure → Abort, run the drift check (`ROJO.md`).
3. **Never switch branches (`switch`, `checkout`, `stash`) while `rojo serve` runs** on that checkout (stop it, or
   `git worktree add`).
4. **One branch + one PR per change, CI green, squash merge.** Never push to `main` (GitHub Free can't block it: it is
   on you). Only exceptions: `vault` notes (Obsidian pushes them) and small doc fixes in the art repo. Stage files by
   name, never blind `git add -A`.
5. **Publishing the place = Studio only, by a human, after saying it on Discord.** Never from CI (the Open Cloud upload
   replaces the whole place and drops unions). After a publish: `gh workflow run opencloud.yml --repo tunnelliers/games -f action=restart`.
6. **`.blend`: `git lfs lock <file>` before editing, push, `git lfs unlock <file>`.** Unlock before the day ends.
   Textures go in the project's `textures/`, never an add-on folder.
7. **Secrets never go in a chat, a repo file, or a command you write.** The human sets them:
   `gh secret set NAME --repo tunnelliers/<repo>` (repo secrets: GitHub Free private repos can't read org secrets).
   Someone pasted a key → tell them to regenerate it.
8. Never chain a destructive command after a check with `&&`; never kill processes by image name; look before deleting.
9. Game code: comments in French; player-facing text in simple, correct English.

### Shared memory
Team knowledge goes where BOTH AIs read it, in a PR: the right `AGENTS.md`, a skill in `studio`, or a dated line in
`vault/Studio/Decisions.md`. Your private memory (if your tool has one) is only for facts about THIS PC.
Setup problem on a PC → run `tunnelliers-doctor` (Claude plugin) or `bash studio/plugins/tunnelliers/bin/tunnelliers-doctor`.
<!-- tunnelliers-team-rules:end -->
