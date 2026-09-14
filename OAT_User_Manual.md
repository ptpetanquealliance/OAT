# OAT (Outil d'attribution des terrains) User Manual

### A Guide for Tournament Directors

Welcome to OAT. This tool is designed to help you run fair, balanced, and dynamic Pétanque tournaments. It solves one of the biggest headaches for any tournament director: making sure teams don't get "stuck" playing on the same courts, or the same type of terrain, all day long.

You don't need any technical background to use this. If you can fill out a spreadsheet or send an email, you can run a tournament with OAT. This guide walks you through setup, running a tournament round by round, understanding the settings that control how courts get assigned, and — if you ever need to run two tournaments at once — how to set that up too.

---

## 1. Getting Started: The Basics

OAT is a single web page. Everything happens in your browser — there's nothing to install, no account to create, and once the page has loaded, you don't need an internet connection to keep using it. You can run an entire tournament from a laptop sitting on a picnic table with no wifi in sight.

You'll get to the page by opening the `OAT.html` file (double-click it, or drag it into a browser window). Any modern browser works — Chrome, Safari, Firefox, Edge.

### The Setup Phase (Before the Tournament Begins)

When you first open OAT, you'll see the **Tournament Setup** box on the left side of the screen.

**Number of Courts Available** Enter the total number of physical courts you have set up for the day (e.g., `12`).

**Define Court Surfaces** *(optional)* If your courts have different types of terrain, tell OAT about it here. Type the surface name, a colon, then a comma-separated list of the court numbers that share that surface:

```
Large Gravel: 1, 2, 3
Oyster Shell: 4, 5, 6
Sand: 7, 8
```

If all your courts are the same, just leave this box blank — OAT will treat every court as identical.

> **Tip:** You can come back and edit this at any time between rounds, for example if a court becomes unplayable and you need to relabel or remove it from a surface group.

---

## 2. Running a Round

Once setup is done, running each round takes three steps.

### Step 1: Enter the Match Pairings

In the **Match Pairings (Current Round)** box, type each match on its own line, in the format `Team A, Team B`:

```
The Rollers, Iron Boules
Paris Pointers, BYE
```

If a team has a bye this round, type `BYE` (any capitalization works) as their opponent — OAT will record it and won't assign them a court.

Doubles teams: if you play doubles ("doublette"), write a team's name as both players separated by a slash, e.g. `Bob/Bill`:

```
Bob/Bill, Sarah/Sam
Mike/Tom, Jane/Amy
```

**Important:** OAT decides where teams play, not who plays whom. You still need to work out the matchups yourself (Swiss system, random draw, whatever your tournament format calls for), and then paste those pairings into OAT.

### Shortcut: "Auto-format list into pairs"

If you'd rather paste a flat list instead of typing out `Team A, Team B` and commas yourself, click "Auto-format list into pairs". It understands three different paste styles, and you can mix them freely in the same paste:

**1. One team per line.** OAT pairs them up automatically — line 1 with line 2, line 3 with line 4, and so on — adding a BYE for anyone left over:

```
The Rollers
Iron Boules
Paris Pointers
```

becomes

```
The Rollers, Iron Boules
Paris Pointers, BYE
```

**2. Doubles teams already written inline**, using the Bob/Bill slash format from above. Each slash-containing line is recognized as one complete team and paired with the next one:

```
Bob/Bill
Sarah/Sam
```

becomes

```
Bob/Bill, Sarah/Sam
```

**3. Doubles teams split across three lines**, with a lone `/` on its own line acting as the separator between two players. This is common if your registration list exports one name per line with a blank or divider row between partners:

```
Abe
/
Bob
Ed
/
Fred
```

becomes

```
Abe/Bob, Ed/Fred
```

This one is recognized automatically — you don't need to check any box for it.

**4. One player per line, with no slash anywhere** — used when your roster export has zero indication of who's partnered with whom, just a flat list of names. In this case (and only this case), check the box under the Auto-format button labeled "List is one player per line — combine every 2 into a doubles team (Bob/Bill)" first. This tells OAT to combine every 2 consecutive player names into one team before pairing those teams into matches:

```
Bob
Bill
Sarah
Sam
```

with the checkbox on, becomes

```
Bob/Bill, Sarah/Sam
```

> Leave the checkbox unchecked for singles play, or whenever your pasted list already has team names on their own lines (styles 1–3 above). It only matters for style 4, where there'd otherwise be no way to tell a player list apart from a team list.

### Step 2: Click "Assign Courts & Balance Pairs"

OAT looks at every team's history — which courts and surfaces they've already played — and works out the single best combination of courts for this round's matches, aiming for the lowest possible amount of "unfairness" across everyone at once (more on exactly how in Section 3).

### Step 3: Read the Results

The Current Round Assignments table tells you exactly where to send each match. The Team History Map further down updates automatically, so you can see, at a glance, everywhere every team has played all day.

If something's wrong with what you typed, OAT will tell you rather than guessing:

- "Not enough courts to accommodate all matches" — you have more matches than courts. Add courts, or make sure any byes are marked `BYE`.
- "[Team] appears in more than one match this round" — the same team name shows up twice in your pairings, probably a copy-paste slip. Fix the pairing list and try again.
- "Algorithm failed to find a valid court for…" — usually means your Court Usage Cap (see below) is too strict for the number of rounds you're running. Raise the cap, or add more courts.

---

## 3. Understanding the Algorithm & Constraint Settings

Think of the algorithm as a strict referee handing out penalty points to different possible court assignments. For the round you're about to run, it works out the penalty score for every possible combination of matches and courts, and picks the single combination with the lowest total score. It isn't just optimizing one match at a time — it's weighing the whole round together, so that fixing one team's court doesn't accidentally create a worse problem for another team on the same round.

You control what the referee cares about most by adjusting the settings below. You do not need to touch any of these to run a good tournament — the defaults are sensible for most club-level events. Adjust them only if something about your venue or format calls for it.

### Showcase Courts

**What it does:** Tries hard to place the very first match in your pairings list (the top line — usually your top-ranked matchup) onto one of the court numbers you list here. **When to use it:** You have a "center court" or spectator court and want the featured match played there for the crowd. **How to set it:** Enter court numbers separated by commas, e.g. `1, 2`. **Suggested value:** Leave blank unless you have a specific showcase court. If you do, just list it — there's no "wrong" number of courts to include.

### Court Usage Cap

**What it does:** A hard limit on how many total times any single court can be used across the entire tournament, all rounds combined. **When to use it:** If a particular court has a bad slope, poor lighting, or you simply have more courts than matches most rounds and want to retire the worst ones early. **Suggested value:** Set it to something generous like 5 or higher if you just want courts used roughly evenly. Only lower it to 1 or 2 for a specific court you want to protect from overuse — and if you do, make sure you still have enough total court-uses across the tournament to fit every round, or OAT will tell you it can't find a valid assignment.

### Consecutive Court Penalty

**What it does:** The cost of making a team play the exact same physical court two rounds in a row. **Recommended value:** 100 (high). You almost never want a team stuck on Court 4 for two straight games — a high score tells the algorithm to avoid this at nearly any cost. **When you might lower it:** Only if you have very few courts relative to the number of teams, where some repetition is unavoidable and you'd rather the algorithm not fight so hard against it (fighting harder elsewhere can sometimes produce worse trade-offs when courts are extremely tight).

### Consecutive Surface Penalty

**What it does:** The cost of making a team play the same type of terrain twice in a row (e.g., Oyster Shell followed by Oyster Shell, even on a different court). **Recommended value:** 40 (medium). Variety is good, but occasionally the math makes a back-to-back surface repeat unavoidable. Keeping this lower than the Consecutive Court Penalty means the algorithm will choose to repeat a surface type before it ever forces a team onto the exact same court twice. **When you might raise it:** If your surfaces genuinely play very differently (say, one is much slower or bumpier) and you want variety enforced more strictly than the default.

### Historical Court Penalty

**What it does:** The cost of sending a team back to a court they've already played earlier in the day — not the round right before, but any prior round (e.g., Court 3 in Round 1, and Court 3 again in Round 4). **Recommended value:** 15 (low). It's mildly annoying to return to an old court, but usually fine, especially later in a long tournament when some repeats become unavoidable. **When you might raise it:** Larger tournaments with many rounds, where you want to actively spread teams across as many different courts as possible over the whole day.

### Surface Frequency Penalty

**What it does:** A running multiplier — every time a team plays on a given surface (say, "Large Gravel"), this penalty is added to any future proposed assignment on that same surface. The more times they've played it, the more the algorithm nudges them elsewhere. **Recommended value:** 5. Gently steers teams toward surfaces they haven't experienced yet, without overriding the stronger, more important rules above about not repeating the exact same court or surface back-to-back. **When you might raise it:** If you have three or more very different surface types and want to make sure everyone samples all of them over the course of the day, rather than mostly sticking to one or two.

### A quick reference table

| Setting | What it controls | Default | When to change it |
|---|---|---|---|
| Showcase Courts | Puts the top match on a center court | *(blank)* | You have a spectator/center court |
| Court Usage Cap | Max total uses per court, all rounds | 5 | A court is unsafe/undesirable, or you want stricter even-use |
| Consecutive Court Penalty | Avoids same court twice in a row | 100 | Rarely — courts are extremely limited |
| Consecutive Surface Penalty | Avoids same surface twice in a row | 40 | Surfaces play very differently |
| Historical Court Penalty | Avoids repeating an old court later | 15 | Long tournaments, many rounds |
| Surface Frequency Penalty | Spreads play across all surfaces over time | 5 | 3+ very different surface types |

One more thing worth knowing: every one of these boxes accepts `0` if you genuinely want to switch a rule off entirely — for example, setting the Surface Frequency Penalty to `0` if surface variety doesn't matter to you at all. You don't need to leave a box blank to disable it.

---

## 4. Saving Your Data (And How Not to Lose It!)

OAT automatically saves your progress every time you make a change. Look for the green "Local Storage Active" badge in the top right — it'll briefly flash blue and say "Saved to Storage" each time something is recorded.

Here's the catch: because OAT runs entirely in your browser with no central server, your data lives in that browser's **Local Storage** — essentially a small filing cabinet attached to that one browser, on that one device.

- **Do not** clear your browser history or cache during the tournament — this deletes everything OAT has saved.
- **Do not** switch browsers (say, from Safari to Chrome) or switch devices (laptop to phone) mid-tournament. The data doesn't travel with you; it stays on the device and browser where you started.
- **If you accidentally close the tab or refresh the page — don't panic.** Just reopen the file. Your tournament will be exactly where you left it.

---

## 5. Running Multiple Tournaments at Once

Sometimes you need two tournaments running side by side — a Morning Bracket and an Afternoon Bracket, or an A-Flight and a B-Flight happening at the same time.

Here's the problem: because OAT saves everything to your browser's Local Storage, if you simply open the OAT page in a second browser tab, it will overwrite your first tournament's data. Both tabs would be reading and writing to the exact same filing cabinet.

The fix is to make each tournament its own separate copy of the page, each writing to its *own* filing cabinet. Here's exactly how, step by step — no coding knowledge required, just careful copy/paste.

### Step-by-step: Setting up a second tournament

1. Make a copy of your `OAT.html` file. Find the file on your computer, right-click it, and choose "Copy," then "Paste" in the same folder. Your computer will likely create something like `OAT copy.html`.

2. Rename the new copy to something obvious. Something like `OAT-Afternoon.html` or `OAT-BFlight.html` — anything that clearly tells the two files apart later.

3. Open the new file in a plain text editor — not a word processor.
   - Windows: right-click the file → Open with → Notepad.
   - Mac: right-click the file → Open with → TextEdit (if TextEdit opens it in rich-text mode and it looks like a formatted document rather than plain code, go to TextEdit's Format menu and choose Make Plain Text first).

   Do not open it in Microsoft Word or Google Docs — those will add hidden formatting that breaks the file.

4. Find the storage key line. Use your editor's Find feature (Ctrl+F on Windows, Cmd+F on Mac) and search for:

   ```
   STORAGE_KEY
   ```

   You'll land on a line that looks like this:

   ```javascript
   const STORAGE_KEY = 'oat_v2_State';
   ```

5. Change the text inside the quotes to something unique to this tournament. For example:

   ```javascript
   const STORAGE_KEY = 'oat_Afternoon_State';
   ```

   Only the text between the quote marks needs to change — leave everything else on that line exactly as it is.

6. Save the file, then close your text editor.

You now have two completely independent tournaments. Open `OAT.html` and `OAT-Afternoon.html` in your browser at the same time (in two different tabs, or two different windows) — because they each have a different `STORAGE_KEY`, they'll save their data into two separate filing cabinets in your browser and will never interfere with each other.

Repeat the same steps for a third, fourth, or however many simultaneous tournaments you need — just make sure every copy gets its own unique key.

> **Heads up:** the storage key only affects where a tournament's data is saved — it doesn't change anything about how the tool looks or works. If you ever open a copy and it looks empty even though you expect prior rounds, double check you're opening the same copy of the file you were using before (with the same key), not a fresh duplicate.

### Quick Troubleshooting Reference

| What you see | What it means | What to do |
|---|---|---|
| "Not enough courts to accommodate all matches" | More matches than available courts | Add courts, or double check every bye is marked BYE |
| "[Team] appears in more than one match this round" | Same team listed in two pairings | Check for a typo or duplicate line in your pairings |
| "Algorithm failed to find a valid court for…" | Usually the Court Usage Cap is too strict | Raise the Court Usage Cap, or add more courts |
| Second tournament shows the first tournament's data | Both copies share the same storage key | Follow Section 5 to give the new copy its own unique key |
| Data disappeared entirely | Browser cache/history was cleared, or you switched browser/device | Unfortunately Local Storage data can't be recovered once cleared — this is why it's worth avoiding clearing history mid-tournament |

Good luck with your tournament — and remember, OAT handles the court math so you can focus on everything else.
