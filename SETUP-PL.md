# Premier League 2026/27 Predictor — setup

This is the World Cup predictor rebuilt for the league. Same idea, same scoring, same PIN system. The one thing that has to be its own is the data store: a **new, separate Google Sheet**. If you point this at the World Cup sheet the two leaderboards will read each other's rows and both go wrong.

You do the four steps below once. After that the family just open the page.

## 1. Make the new sheet and paste the script

1. Go to sheets.new and give it a name like "PL 26/27 Predictor". This is a different file from the World Cup one.
2. Extensions > Apps Script. Delete whatever's in the editor.
3. Open `Code.gs` from this folder, copy all of it, paste it in, and save (the disk icon).

## 2. Deploy it and copy the URL

1. In the Apps Script editor: Deploy > New deployment.
2. Click the gear next to "Select type" and choose **Web app**.
3. Set **Execute as: Me**, **Who has access: Anyone**. Deploy.
4. Approve the permissions when Google asks (it's your own script talking to your own sheet).
5. Copy the **Web app URL**. It ends in `/exec`. That's the only thing you need from this step.

## 3. Wire the URL into the page

1. Open `index.html` in this folder in a text editor.
2. Near the top of the `<script>` block, find:

   ```
   const SCRIPT_URL = "";
   ```

3. Paste your `/exec` URL between the quotes and save. That's the connection made.

The players line is right underneath if you want to change who's in:

```
const PLAYERS = ["Scott", "Vickie", ...];
```

## 4. Put it somewhere the family can open

Same as the World Cup one. Either:

- **GitHub Pages** (recommended, it's what you already do): make a new repo, drop `index.html` in, turn on Pages, share the link. Keep it a separate repo from the World Cup so the two don't tread on each other. Upload `premier-league-24-25.jpg` into the same repo next to `index.html`, or the banner won't show.
- Or any static host, or even just send the `index.html` file round. It works from a plain file, it just won't share a live leaderboard unless everyone's hitting the same hosted copy pointed at the same sheet.

## How it works, quickly

- **One week at a time.** Only the current gameweek is open for picks. The next one appears on its own once the Friday deadline passes, which is when I also refresh that week's fixtures for any TV moves or postponements. Every fixture is already in the file, taken from the official list.
- **Predictions lock at 7:30pm on the Friday** of each gameweek, by themselves. Miss it and that week goes read-only.
- **Scoring** is the same as before: 3 for the exact score, 1 for the right result, 0 otherwise.
- **Money.** £2 a week per player: £1 into that week's prize for the weekly winner, £1 into the end-of-season pot. The Leaderboard shows both pots, worked out from the number of entries at £1 each. It's a running total for reference, it doesn't handle actual payments.
- **Leaderboard** has two parts. A weekly prize table that crowns each week's winner and shows the weekly pot, and a rolling season table that adds everything up and shows the season pot. The season table also counts how many weeks each person has topped.
- **Results** normally get entered by the results task (next section). The Results tab is a manual backup if you ever want to type a week in yourself. It needs your organiser PIN, which is set the first time you save.

## The results task

`pl-auto-results-task.md` in this folder is the brief for the automation that fills in full-time scores each week, the same way the World Cup one does. It can't run until this sheet is live, because it needs the `/exec` URL and the organiser PIN.

Once you've done steps 1 to 3, send me the `/exec` URL and I'll wire up the weekly task for you. Set the organiser PIN yourself by saving any week's results once on the Results tab, and tell me what it is (or reuse your World Cup organiser PIN). Don't put the PIN in the repo.

## Two things worth knowing

- **The season hasn't started.** Today everything is unlocked and the leaderboard is empty. That's correct. It fills in once GW1 is played on 21 August.
- **Reschedules.** The league moves kick-offs for TV all the time. The fixture *pairings* here are fixed and correct; a moved kick-off time won't break anything. The only real edge case is a match postponed out of its week entirely, which just shows no result until it's played. It doesn't corrupt anything.
