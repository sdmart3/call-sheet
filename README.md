# Call Sheet

**Smarter coach suggestions for College Football 27 on PC.**

On the play-call screen the game suggests three plays. Normally those come only from the handful of plays your
playbook's gameplan lists for the situation. Call Sheet changes that:

- **Your whole playbook.** Suggestions can come from any play in your book. The gameplan plays still get a head
  start, so the game's own picks stay common.
- **Your rules.** A rulebook nudges the suggestions by situation: down, distance, field position, clock, score and
  timeouts. For example, "on 3rd & 1, favor power runs" or "in the red zone, fewer deep shots".
- **Game plans you can switch mid-game.** Make several game plans and swap between them during a game, from the
  editor or with a hotkey.
- **Play tags and a trick-play dial.** Tag plays (your created plays, a red-zone package, gadget plays), then turn
  them up or down with one number.
- **Defense too.** Rules can reweight your defensive suggestions for the look the offense shows.
- **Auto-playcall.** Let the CPU call your plays, and switch it on or off mid-game.

Call Sheet has three parts, and the editor installs all of them for you:

| Part | What it does |
|---|---|
| **Call Sheet editor** (`Call Sheet.exe`) | The desktop app. You set things up, write rules, build game plans, tag plays and preview suggestions here. |
| **Mod Manager plugin** | Starts Call Sheet when you launch the game from the Mod Manager. |
| **Call Sheet DLL** | Runs inside the game and shapes the suggestions. |

You don't need a `.fbmod`. Call Sheet works with the playbook you already play with.

> **Version 0.9.0 is a first prototype.** Some features haven't been tested in a real game yet. The
> [changelog](CHANGELOG.md) lists exactly which ones.

---

## What you need

- **College Football 27 on PC.**
- **The Mod Manager, version 1.1.0.6 or newer**, set up for College Football 27. Call Sheet only runs when you
  start the game from the Mod Manager.
- **Offline play only.** Call Sheet only changes offline games. A modded game can't play online anyway.

You don't need any other mod. If you use **Dynasty Hooks**, read [Standing aside for Dynasty Hooks](#standing-aside-for-dynasty-hooks)
first.

---

## Install

### With the editor (recommended)

1. Close the game.
2. Unzip the Call Sheet download anywhere you like (not into the Mod Manager or game folder), then open
   `Call Sheet.exe` in its `Call Sheet` folder.
3. The **Home** page opens on **First-run setup: Get Call Sheet ready in five steps**. Work through them:
   1. **Find the Mod Manager.** The editor looks for it on its own. If it guesses wrong or finds nothing, click
      **Choose the Mod Manager folder** and pick the folder that holds the Mod Manager program. If you pick the wrong
      folder, the editor tells you what you picked.
   2. **Find your saves.** This is where your playbooks (the `PBOOKOFF` / `PBOOKDEF` files) live. Call Sheet only
      reads them. If needed, use **Choose the saves folder**.
   3. **Install to the Mod Manager.** Click **Install Call Sheet**. This copies the plugin and the DLL into the Mod
      Manager's `Plugins` folder. Nothing in the game folder changes.
   4. **Pick your playbook.** Choose the offensive playbook you play with. The editor uses it to show play names,
      previews and game plans.
   5. **Pick a starter rulebook.** Choose one of the six starters (see [the rulebook guide](GUIDE-rulebooks.md#the-starter-rulebooks)),
      or click **Skip: I will write my own**.

You can change every choice later. The **Folders in use** card on Home shows each folder, with buttons to open,
change or reset it.

### By hand

The download includes a `Manual install` folder with a `Plugins` folder inside. Copy that `Plugins` folder into your Mod
Manager folder, so that you end up with:

```
<Mod Manager folder>\Plugins\CallSheetPlugin.dll
<Mod Manager folder>\Plugins\CallSheet\        (callsheet.dll, callsheet.ini, plugin.cfg, rulebooks\, tags\)
```

If the Mod Manager already has a `Plugins` folder, merge into it. Don't replace it, because other plugins live there
too.

### What gets installed

Everything lives inside the Mod Manager folder, under `Plugins\CallSheet\`:

| File or folder | What it is |
|---|---|
| `callsheet.dll` | The part that runs inside the game |
| `callsheet.ini` | Call Sheet's settings. The editor edits it for you. |
| `plugin.cfg` | Settings for the plugin that starts Call Sheet |
| `rulebooks\` | Your rulebooks. The six starters are included. |
| `tags\` | Your play tags files |
| `gameplans\` | Your game plans. This folder is created when you make your first one. |
| `callsheet.log`, `plugin.log`, `status.json` | Logs and live status. See [Logs](#logs-and-status). |

### Updating

When a newer editor is ready to install, Home shows **Update ready** and an **Update Call Sheet** button. Updating
never overwrites your settings, rulebooks, tags or game plans. New settings are added to your `callsheet.ini`, and a
backup of everything that changes goes to `%APPDATA%\CallSheet\backups\` first. Close the game before you update,
because the DLL can't be replaced while the game is using it.

---

## Your first game

1. Start College Football 27 **from the Mod Manager**, the way you always do.
2. Call Sheet loads about **30 seconds after the game starts**. The game's launcher needs that time to finish
   starting up. The Mod Manager's log shows a line like `Call Sheet: loads about 30 s after the game starts`.
3. Start an offline game and get to the play-call screen.
4. Look at the coach suggestions. You should start to see plays from across your book, shaped by your rulebook.
   Not just the same few gameplan plays every time.

Want to see why a play came up? Open the editor's **Live** page while you play. It shows the last snap Call Sheet
saw: first the plays the game actually put on your screen, in order, then the situation, the weights behind the draw
(with each play's chance to be on screen), and the rules that fired.

### Changes take effect on the next play

You can leave the game running while you edit. Call Sheet checks its settings, your active rulebook, tags and game
plan about once a second, and uses the new version **from the next play-call screen on**. You don't need to restart
anything, whether you switch a rulebook, change a weight or activate a game plan.

---

## How to tell it's working

- **The editor's top bar** shows a status pill: **Call Sheet active** while it's shaping your suggestions,
  **Starting...** while it loads, **Ready** when it's installed and waiting for the game, or **Standing aside** /
  **Switched off** / **Error in game**.
- **The Live page** shows the last snap: **Shown on screen** (the plays the game drew, in order), down and distance,
  the ball spot from your side, quarter and clock, score, the situation, the weights behind the draw, and **Rules that
  fired**. It updates every second while the game runs. On defense it names plays from your defensive playbook.
- **The Home page status card** says "The game is running and Call Sheet is shaping your coach suggestions."
- **`callsheet.log`** (in `Plugins\CallSheet\`) has an `install done` line soon after the game starts. If whole-book
  suggestions are on, you'll also see one line starting with `wholebook:` for each suggestion screen.

---

## Pages in the editor

| Page | What it's for |
|---|---|
| **Home** | Setup, status, install / update / uninstall, folders, the playbook mods that name your custom plays, and the Dynasty Hooks notice |
| **Suggestions** | The main switches and the weights behind whole-book suggestions (see below) |
| **Game Plans** | Make, edit and activate game plans, and set the switching hotkey. See [GUIDE-gameplans.md](GUIDE-gameplans.md). |
| **Rulebooks** | A visual rule builder plus a text editor, starters, import / export, and **Set as active**. See [GUIDE-rulebooks.md](GUIDE-rulebooks.md). |
| **Playbook & Tags** | Every play in your book (named, including the custom plays your playbook mods add), with filters, tagging, **Import tags...** and **Suggest tags**. See [GUIDE-tags.md](GUIDE-tags.md). |
| **Preview** | Set a situation on a field diagram and see the ranked suggestions, the weights and the rules that fired, without playing. Compare two setups side by side. |
| **Auto-playcall** | The on/off switch, its hotkey and the switch beep |
| **Live** | What was on your play-call screen on the last snap (**Shown on screen**), the weights behind it, plus the log |

### The Suggestions page

The suggestions are drawn by weight. A play with twice the weight comes up about twice as often. These settings
decide the weights:

| Setting | Default | What it means |
|---|---|---|
| **Call Sheet** (master switch) | On | Off: Call Sheet loads with the game but changes nothing |
| **Whole-book suggestions** | On | Suggestions can come from any play in your book, not only the gameplan plays for the situation. Offense. |
| **Whole-book suggestions on defense** (beta) | Off | Your defensive suggestions can come from any play in your defensive book that fits the offense's look. See below. |
| **Apply my rulebook** | On | Your active rulebook reshapes the suggestions every snap, on offense and defense |
| **Game plan head start** | 8 | A gameplan play starts at its game plan % times this. A play listed at 30 starts at 240. |
| **Base weight** | 10 | What every other play in the book starts with. 0 means only gameplan plays can come up. |
| **Book size reference** | 480 | Big books spread the base weight thinner, so the gameplan keeps its share. 0 turns this off. |
| **Repeat window** | 6 | How many of your recent offensive calls count as repeats |
| **Repeat damping** | 0.15 | A play you called within the window is multiplied by this, so the same call doesn't keep coming up. Lower means more variety. |

A few kinds of play are kept out of the whole-book draw unless the situation's gameplan already lists them: kicks,
punts, kneels, spikes, Hail Marys, fakes, and goal-line sets when you're farther out than the 5. Special situations,
such as field goals, punts, kickoffs and the last play of a half, keep the game's own list.

**On defense (beta, off by default).** The game's defensive situation is the offense's *look* (base, pass, trips,
run, empty, nickel, dime and so on). With **Whole-book suggestions on defense** on, every play in your defensive
book is scored for that look:

- The book's gameplan rows for the look (or the active game plan's `[def ...]` section) get the head start, with the
  same **Game plan head start** multiplier as the offense.
- The rest of the book joins at the **Base weight**, but only in the formations those rows use. If your Nickel rows
  are 4-2-5 and Nickel sets, the other 4-2-5 and Nickel plays come in; your 4-3 and Dime plays stay out for that
  look. That keeps the calls fitting the personnel on the field.
- Goal-line defense stays out unless the look is a goal-line look (or the ball is inside the 5), and punt-return,
  kick-return and field-goal defense stay out unless the look is one of those. Those special-teams looks keep the
  game's own list.
- Your `side=def` rules and the repeat damping (on your own defensive calls) apply on top.

Why it's worth trying: on its own, the game hands your first defensive suggestion a pool of every defensive play in
the book at the same weight (that is the "180 plays at 72" you may see on the Live page), so suggestion #1 is close
to a random play from the whole book. This switch scores that book instead.

It hasn't been proven in a real game yet, so it ships off. Turn it on in a game you don't care about first.

### The Auto-playcall page

With auto-playcall on, the CPU calls your plays every snap, on offense and defense. You still play the down. You can
flip it mid-game, for example to hand over a drive and take it back, and the change applies on the next snap. You can
also set a **Hotkey** to toggle it without leaving the game.

Know before you use it:

- **The hotkey** works while the game or Call Sheet is in front, with a short beep
  (switch the beep off on the same page).
- **It's both sides or nothing.** A separate offense / defense switch isn't possible yet.
- **It uses the game's own CPU play calling for your team.** The CPU picks with its own logic, not from your rules or
  game plan. A future option will make it pick from Call Sheet's suggestions instead.

---

## Standing aside for Dynasty Hooks

Dynasty Hooks can also run expanded coach suggestions. If both tried to change the suggestions at once, they would
collide. So **when Dynasty Hooks play calling is on, Call Sheet stays out of the way.** It doesn't load its hooks.
Nothing breaks: Dynasty Hooks keeps doing the play calling.

You'll see **Standing aside** in the editor's top bar, a notice on Home that names the Dynasty Hooks settings that are
on, and `"state":"standing_aside"` in `status.json`.

**To use Call Sheet instead:**

- **Easiest:** open the Dynasty Hooks settings app. Switch off whole-book suggestions, play-call rules and
  auto-playcall, then save.
- **Or by hand:** open Dynasty Hooks' `autoprogress.ini` (in its hooks folder, normally `Plugins\DynastyHooks\`
  inside the Mod Manager folder) and set these seven keys to `0` (a key that isn't in the file counts as `0`):

  ```
  wholebook_suggest = 0
  playcall_rules = 0
  auto_playcall = 0
  playcall_probe = 0
  wholebook_probe = 0
  auto_playcall_probe = 0
  auto_playcall_user = 0
  ```

  The first three are the switches in the settings app. The other four are advanced switches that use the same
  hooks, so they count too.

Then restart the game from the Mod Manager. Dynasty Hooks keeps doing everything else. The Home notice,
`plugin.log` and `callsheet.log` all name the keys that are on, and they check the same seven.

Run both on purpose? `plugin.cfg` has `respect_dynasty_hooks = 1`. Only set it to `0` if you're certain Dynasty Hooks
play calling is off. Otherwise the two will collide.

---

## Uninstall

**With the editor:** Home, then **Uninstall**. This removes the plugin and the DLL from the Mod Manager. Your
settings, rulebooks, tags and game plans go into a dated backup folder under `%APPDATA%\CallSheet\backups\`, so you
can bring them back later. Close the game first.

**By hand:** close the game, then delete `Plugins\CallSheetPlugin.dll` and the `Plugins\CallSheet\` folder from the
Mod Manager folder. Copy out `rulebooks\`, `tags\` and `gameplans\` first if you want to keep them.

**Remove the editor too:** delete the Call Sheet folder you run `Call Sheet.exe` from. The editor keeps its own
settings (folders, preferences, backups) in `%APPDATA%\CallSheet\`. Delete that folder too for a clean removal.

**Just want it off for a while?** You don't have to uninstall. Use the master switch on the Suggestions page
(`enabled = 0` in `callsheet.ini`), or set `plugin_enabled = 0` in `plugin.cfg` so the plugin doesn't load Call
Sheet at all.

---

## Logs and status

All three files are in `Plugins\CallSheet\` inside the Mod Manager folder. The editor's **Live** page shows them
for you, and its **Open the Call Sheet folder** button takes you there.

| File | Written by | What's in it |
|---|---|---|
| `plugin.log` | The plugin | Each launch: did the game start, did Call Sheet stand aside (and why), did the DLL load |
| `callsheet.log` | The DLL | Startup, which rulebook, tags and game plan loaded (and any skipped lines), switches you made, and one line per suggestion screen while whole-book logging is on |
| `status.json` | The DLL (or the plugin, if Call Sheet never loaded) | The live state the editor reads: active / starting / standing aside / switched off / error, plus the last snap |

The **Diagnostics** switches on the Suggestions page (**Log every suggestion list**, **Log rules**) write more
detail. They're handy while you check something, and you can switch them off afterwards.

---

## FAQ and troubleshooting

**Nothing changed in my suggestions.**
Check the top bar first.
- **Not installed** or **Not set up**: finish the setup on Home.
- **Standing aside**: see [Standing aside for Dynasty Hooks](#standing-aside-for-dynasty-hooks).
- **Switched off**: turn on the master switch on the Suggestions page.
- **Game running** or **Game running, Call Sheet off** while you play: Call Sheet didn't load or is switched off. Check the master switch, then open `plugin.log` (see the next questions).

Also make sure you started the game **from the Mod Manager**, and give it about 30 seconds after the game appears.

**`plugin.log` says "no new CollegeFB27.exe appeared".**
The game didn't start within 3 minutes of pressing Launch, or it was already running before you pressed Launch.
Close the game completely and launch it again from the Mod Manager. If your PC is slow to start the game, raise
`wait_game_sec` in `plugin.cfg`.

**`plugin.log` says "access denied".**
The game is running as administrator and the Mod Manager isn't. Run the Mod Manager as administrator too, or run
neither as administrator.

**My antivirus flagged a Call Sheet file.**
Here's what Call Sheet does. The plugin loads `callsheet.dll` into the game using standard, documented Windows
functions. There's no separate injector program: earlier tools shipped one, and antivirus products often flag
those. During development, Windows Defender didn't flag either file. Even so, any program that loads code into
another process can look suspicious to an antivirus.
- Get Call Sheet only from its official release page.
- If you trust your download, restore the file from quarantine and allow that one file (or the `Plugins\CallSheet\`
  folder) in your antivirus.
- Don't switch your antivirus off to make Call Sheet work.

**I changed a setting mid-game. When does it apply?**
On the next play-call screen. Call Sheet checks for changes about once a second.

**I play online.**
Call Sheet only changes offline games.

**The game updated and Call Sheet stopped working.**
Before Call Sheet changes anything in the game, it checks that the game's code is exactly what it was tested against.
After a game update that changes that code, Call Sheet refuses to change it, logs the reason in `callsheet.log`, and
your game runs normally without it. Watch for a Call Sheet update. Version 0.9.0 was checked against the game builds
of September 10, September 22 and October 1, 2026.

**The editor shows "play 4294812345" instead of names.**
Pick your playbook (on Home, Playbook & Tags, Preview or Live) so the editor can look the names up. Plays that a
playbook mod adds are named from the mod itself: check the **Playbook mods** card on Home. It lists the mods it read
from the Mod Manager's mods folder (and your Chalkboard plays). If your mods live somewhere else, use **Choose the
mods folder**, then **Rescan**. A play stays a number only when no mod on this PC adds it (for example a book built
with an older version of a mod).

**My rulebook line is ignored.**
The game skips any line it can't read completely, and never guesses. The Rulebooks page marks the line and says why,
and `callsheet.log` lists `line N skipped: <reason>`. See [why a line gets skipped](GUIDE-rulebooks.md#why-a-line-gets-skipped).

**My playbook is huge.**
Whole-book suggestions work with books of up to about 1,000 plays. For a bigger book, Call Sheet falls back to the
game's normal suggestions and says so in the log.

**Can Call Sheet add plays that aren't in my playbook?**
No. It only reweights plays that are already there. To get a play suggested, add it to your playbook first.

**Where do my files live, and are they safe during updates?**
They live in `Plugins\CallSheet\` (rulebooks, tags, game plans and `callsheet.ini`). Install and update never
overwrite them. When you delete or rename a rulebook or game plan in the editor, the old file goes into
`Plugins\CallSheet\backups\` first.
