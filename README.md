# TSC AutoCombat — ToB (64-bit)

A combat bot for **The Second Calling**, where every character is three classes
at once. It runs all three for you: casts your spells, fires your AAs and
discs, pulls, controls your pets, keeps your boxes together and sits to med
when it is safe. Everything is set up in one in-game window — no macros to
write.

This is the build for the **ToB client** (64-bit). It is a **complete
MacroQuest** with the tool already in it: download it, run `MacroQuest.exe`,
and log in.

Still on the old RoF2 client? Use [TSC-AutoCombat](https://github.com/Aoezpz/TSC-AutoCombat) instead.

# ⬇ [Download the latest release](https://github.com/Aoezpz/TSC-AutoCombat-ToB/releases/latest)

Grab the zip from the **Assets** list on that page.
([every release](https://github.com/Aoezpz/TSC-AutoCombat-ToB/releases))

> **Test build — the first one for ToB.** It has had very little time in game.
> Please report anything that looks wrong rather than assuming it is meant to
> work that way.

**Server rules:** MacroQuest and this bot are allowed on The Second Calling.
Warping and other exploits are not.

---

## Install

1. **Download the zip above** and extract it somewhere like `C:\TSC-AutoCombat-ToB`.
   (Or `git clone` this repository — same files.)
2. **Add that folder to your antivirus exclusions.** Every MacroQuest build
   trips Defender and SmartScreen; this one is no different.
3. **Get the zone navmeshes** — they are not in the download (2 GB, and they
   do not compress). Either copy `resources\MQ2Nav` from a MacroQuest install
   you already have (your RoF2 TSC-AutoCombat folder has them), or run
   `MeshUpdater.exe` from this folder. Without them the bot still fights, but
   it cannot path: no pulling, no chasing, no return-to-camp.
4. **Run `MacroQuest.exe`** from this folder, then start the ToB client and log in.

The tool opens by itself when you enter the world. If you close it, type `/ac`.

---

## First run

1. **Check your classes.** The header shows the three it detected, each in its
   house color — melee red, priest silver, caster blue. It reads them from your
   Inventory window (`NEC/WIZ/MAG`). Wrong or only one? Re-detect under
   **Settings → General**.
2. **Set up what to cast.** Work through the tabs: **Spell Gems**, **Abilities**,
   **AAs**, **Discs**, **Clickies**. Each entry gets a plain rule for when to
   fire — *Target HP below 90%*, *My HP below 40%*, *Missing buff*, *Always*.
   **Import Bar** on the Spell Gems tab fills the list from whatever you have
   memorized.
3. **Pick a mode** on the **Control** tab and press **START**.

Your setup saves itself to `config\` and reloads next time. One file per
character, so boxes never overwrite each other.

---

## Modes

| Mode | Use it when | What it does |
|---|---|---|
| **Manual** | You want to drive | You move and pick targets; it fights, heals and casts. |
| **Puller · Camp** | You are the puller | Runs out, tags a mob, brings it back to camp, kills it there. |
| **Puller · Hunt** | Solo roaming | Wanders and kills mobs where they stand, inside an anchor circle. |
| **Assist · Chase** | Boxed melee | Follows the main assist and attacks their target. |
| **Assist · Camp** | Boxed, holding a spot | Stays at camp, fights what comes in. |
| **Assist · Backline** | Boxed healers and casters | Holds at range, never walks into melee. |

Set the main assist with `/ac ma <name>` or on the Control tab. **Combat style**
(`/ac style melee|ranged|spell`) decides whether you close to melee, shoot a
bow, or stand off and only cast.

---

## Commands

`/ac help` prints the full list in game.

| Command | What it does |
|---|---|
| `/ac` | Start or pause |
| `/ac run` / `/ac pause` | Start / pause |
| `/ac manual`, `/ac puller camp`, `/ac puller hunt`, `/ac assist chase`, `/ac assist camp`, `/ac backline` | Switch mode |
| `/ac ma <name>` | Set the main assist |
| `/ac burn` | Toggle burn mode — fires everything marked *Burn Only* |
| `/ac memall` | Memorize any missing spells |
| `/ac importbar` | Build the spell list from your memorized gems |
| `/ac style melee\|ranged\|spell` | Set combat style |
| `/ac wp add` / `/ac wp clear` | Add a patrol waypoint here / clear the route |
| `/ac net <all\|zone\|group\|Name> <command>` | Run a command on your other boxes |
| `/ac compact` | Shrink to the mini strip |
| `/ac scale 1.25` | Make every window bigger or smaller |
| `/ac status` | Print what the bot is doing |
| `/tscacrun` | Start / pause — bind this to a key |

`/tscac` works anywhere `/ac` does.

---

## Box Network

Your characters on one PC talk to each other over MacroQuest Actors — nothing
extra to install. Assist boxes follow the main assist's real target, two
pullers stay off each other's mobs, boxes count as allies for buff requests,
and `/ac net all burn on` runs a command on every one of them. Settings live
under **Settings → Box Network**.

---

## Known issues (ToB test build)

- **TSC windows draw on top of EverQuest's windows** while MacroQuest is
  loaded. Harmless; a fix belongs in the TSC client.
- **Navmeshes** come from the RoF2 era. A zone with no mesh, or one whose
  map changed, will not path — the **Status** tab tells you.

---

## When something goes wrong

- **Not moving or pulling?** Check the **Status** tab. It shows whether MQ2Nav
  and MQ2MoveUtils are loaded and whether the zone has a navmesh, with buttons
  to load or reload them. No navmesh is the usual answer — see step 3 above.
- **Stuck on terrain?** It remembers where it got stuck and routes around it
  next time. Clear those spots under **Settings → Navigation**.
- **Reporting a bug:** turn on **Log To File** (`/ac log on`), and when it
  happens run `/ac dump`. Attach the files from the `Logs\` folder. `/ac debug`
  prints extra detail to chat.
- **Want to see every ability as it fires?** Turn on **Debug Mode**
  (`/ac debug`). Normally each AA, disc, skill and clickie is recorded quietly
  in the log — `/ac dump` still shows exactly what went off.
- **"MacroQuest version mismatch" or a crash on startup?** This MacroQuest is
  built for the ToB client only. Another MacroQuest — including the RoF2
  TSC-AutoCombat — will not load into it. Use the one in this folder, and run
  it with the ToB client.
- **Where does MacroQuest's output go?** To the **MacroQuest console** — press
  <kbd>Ctrl</kbd>+<kbd>`</kbd> to show or hide it. `/mqconsole clear` empties
  it. MacroQuest's old `MQ` chat window is switched **off** on purpose; if you
  want it back anyway: `/plugin mq2chatwnd load`.

---

## Where your files live

| File | What it holds |
|---|---|
| `config\tscac_loadout_TSCTOB_<char>.lua` | Each character's settings. Never overwritten by an update. |
| `config\tscac_data.lua` | Spell, disc and AA lists for all 16 classes. |
| `Logs\tscac_*.log` | Diagnostic logs, when Log To File is on. |
| `lua\tscac.lua` | The engine. |
| `lua\tscac\` | Box Network and the logger. |
| `resources\MQ2Nav\` | Zone navmeshes — you supply these. |

Coming from RoF2? Your old setups do not load by themselves. Copy
`tscac_loadout__<char>.lua` from the RoF2 folder into `config\` here and
rename it to `tscac_loadout_TSCTOB_<char>.lua`.

To update: pull (or download the ZIP again) and overwrite. Your `config\`
loadouts are ignored by git and will not be touched.

---

## Credits and source

Built on the engine of an open-source MacroQuest combat bot, stripped down to
the bot itself and rebuilt for this server: its own theme, the trio's house
colors, and none of the companion windows (chat, map, DPS meter, inventory
and the rest) that belong to other tools.

MacroQuest and its plugins are third-party software. MacroQuest is licensed
under the GNU GPL v2 — see `resources\LICENSE.md` and `resources\CHANGELOG.md`.
The binaries here are built, unmodified, from:

| Component | Source |
|---|---|
| MacroQuest (`emu-tob`) | [macroquest/macroquest @ a264d120](https://github.com/macroquest/macroquest/tree/a264d120) |
| eqlib (`emu-tob`) | [macroquest/eqlib @ 16db84cc](https://github.com/macroquest/eqlib/tree/16db84cc17fe628d6d8e34e7694b35f16fdf0c14) |
| MQ2Nav | [brainiac/MQ2Nav @ 0472ae4](https://github.com/brainiac/MQ2Nav/tree/0472ae475c56db34cb03dc31bb4d0d88ad6096df) |
| MQ2MoveUtils | [RedGuides/MQ2MoveUtils @ 4c142d3](https://github.com/RedGuides/MQ2MoveUtils/tree/4c142d3) |
