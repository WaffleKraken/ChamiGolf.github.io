# Red & Gold Golf

A 3D, Chaminade-themed golf game that runs in any browser. Everything is in one file, index.html, with no install and no build step.

Play it at https://chamigolf.github.io/


## How to play

- Check PIN at the top for yards to the hole, then pick a club. Tap the club name to open your bag, or use the arrow buttons.
- Swipe left or right to aim. MAP shows the whole hole, and you can tap it to aim.
- Press the ball and pull back. Every shot works like putting: the tag next to the ball shows your swing % (100% = the club's full distance) with a rough distance guide underneath.
- Let go in the bright gold zone for a perfect strike.
- Putting: aim exactly with the ◀ AIM ▶ buttons in the bottom-left corner (hold to keep turning) or the left/right arrow keys (Shift = bigger steps; up/down arrows change club). Wind never moves a putt (it barely touches little chips either).
- Momentum: 3 holes in a row with no bogey adds +20% to hole payouts, then +20% more per hole you keep it going, with no limit. A bogey ends it.
- Rough cuts distance 15% and sand cuts it 40% (less with the Sand Wedge). The driver only gets its full distance off a tee: hit it off the fairway (or anywhere else) and it loses 20%. Watch the wind arrow.
- After every shot the game picks the club whose full swing finishes closest to the hole. On doglegs it only plays to the corner when trees block the line to the hole.
- Water and out of bounds cost a stroke. Cart paths are concrete: the ball kicks up and skips off them.
- Left-handed? Switch hands in the Golfer tab.
- Golf ball colours are free: pick a preset or mix any colour with the R/G/B sliders in Golfer > Ball (alignment lines still cost money).
- On the first tee, Mr. Haslbaur (3C Par Three) and Mr. Garner (Chami Links Crimson) pop up in the bottom-left corner with a word of encouragement (tap to dismiss; they leave after your tee shot).
- Hole payouts: hole-in-one $1,500 · albatross $1,000 · eagle $250 · birdie $100 · par $25 · bogey or worse $0.
- Driving Range (Play tab): a bucket of 30 balls and eight target greens from 50 to 270 yds, each with a bucket in the middle. In the bucket pays $70 to $202 (by distance), inside the inner ring $12 to $27, on the target green $4 to $8, and every target hit in a row adds +10% (up to +50%). Range money is capped at $1,500 a day. Floating money, cash-register sounds, confetti for a bucket and a summary card (hits, buckets, best streak, closest, longest drive) at the end.
- Updates: the What's New pop-up shows the update number, and "📜 Previous updates" (also under Stats) lists every update.

## Courses

3C Par Three (where everyone starts) → Chami Links Crimson (6 holes) → Chami Links Gold (Bethpage Black's front nine, 9 holes) → Chami Links Black (all 18 holes of Bethpage Black, the hardest course), plus TPC Saragosa, Farbor Lake, Meribah Country Club, Brothers Hollow and Deans Valley (its 18th hole is Room 23), Gold Star Mini Golf, the Driving Range and the Daily Closest to the Pin.

Gold Star Mini Golf was reworked on Oct 20 2026 (par 41: 13 par 2s and 5 par 3s). Golfers were birdieing the old par 3s, so every hole was balanced with a computer golfer that takes thousands of simulated putts per hole: a good player now averages about 2.1 to 2.4 on the par 2s and 2.6 to 3.1 on the par 3s (Zig Zag, Windmill Alley, Snake Pass, The Slalom and the Grand Gold Star finale).

## Clubs and upgrades

- Each club has three upgrades, up to level 5 each: Power (+4% distance), Accuracy (+1.6% gold zone, and misses 8% straighter) and Control (needle 12% slower). Levels cost $400 / $900 / $1,800 / $3,500 / $6,000 (Power 20% more). A stat can only go one level past the club's lowest stat.
- Lots of club models to buy in every slot, and club colours (buy a colour once, paint any club).
- Customization is 30% off (Oct 20 2026): outfit colours, outfits, club colours, ball lines and the custom bag logo ($7,000). `LOOK_SALE` in index.html sets the discount.

## Online

- Daily Tournaments for every course, mini golf and Closest to the Pin. No sign-in needed to post: you just need a name (anyone still called "Player" is asked for one).
- Sign in with Google to save progress to the cloud and play friends. Progress follows your Google account to every device: the game checks for newer progress whenever you come back to it (and never saves an older copy over a newer one), and Golfer > account has a ☁️ Sync now button with the last sync time. Guest progress stays on that one device.
- Premium badges (Creator's Pick, Daily Champion, Hole in One) show next to your name on the leaderboards. Only the Creator's Pick tile shows how many golfers have it. Creator's Pick goes to golfers who helped make the game or had a suggestion added.
- Daily Champion counts your wins: the number of days you finished 1st (any Daily Tournament or Closest to the Pin) shows next to the 🏆, in the header, in the Golfer tab and next to your name on every leaderboard.
- Leaderboard Season 4 started Oct 20 2026: every board (all-time, daily tournaments, Closest to the Pin and holes in one) starts fresh. Old scores stay in the database but aren't shown. To start another season, change `SEASON` and `SEASON_START` in index.html.
- Unlockable outfits: the Senior Sweater (within 10 feet in the Daily Closest to the Pin) and the Masters Outfit (par or better at Chami Links Black).
- Reloaded mid-round? Keep playing, finish the round early (paid for the holes you played), or quit.

## Play Friends

- Sign in, create a match and send your friends the 6-character match code (or tap Share invite link in the lobby). Friend lists and friend codes were taken out on Oct 20 2026: everything is joined by code.
- **1v1**: stroke play for a wager ($0 up to what you have), 3, 6 or 9 holes. Tied? Sudden-death playoff holes.
- **2v2**: scramble, alt shot or best ball. **Foursome**: own ball (1v1v1v1, up to 4 golfers, lowest total wins the pot) or a 2 v 2 scramble. The host sets one buy-in that every golfer pays; a pop-up confirms it when you join, and you can't join without enough money.
- Everyone gets the same wind. Winners split the pot. Quitting a match forfeits it for your team.

## Anti-cheat and creator tools

Everything below runs inside the game on each player's device, plus the Firebase rules on the server. (A browser game can never be 100% cheat-proof, since the code runs on the player's device; this stack catches the ways players actually cheat and makes the rest a lot of work.)

**Three levels**

- **Hard ban, no appeal** (the game's code was messed with): a script injected into the page, a script added from an outside website or a `data:`/`blob:`/`javascript:` source, built-in browser functions swapped out (`Math.random`, `Date.now`, `performance.now`, `requestAnimationFrame`, `setTimeout`, `setInterval`, `JSON.parse/stringify`, `localStorage` get/set, `Math.hypot/sqrt`, or `Function.toString` replaced to hide it), and a modified copy of the game running anywhere but chamigolf.github.io (a saved copy opened from a file counts). The ban screen says the ban is final.
- **Ban right away, can appeal** (everything else strong): the save edited by hand (in the game or from another tab), $5,000+ showing up in the bank that the game never paid out (at once or in total), a bank bigger than everything ever earned, money + gear worth more than everything earned, 4+ aces in a round, 4 aces in a row, an ace on a 420+ yd hole, a round 10+ under (or under by the number of holes), a round finished impossibly fast, a bot (40+ taps/keys made by a script), an automated browser (webdriver), a speed hack (the game clock running faster or slower than real time) and a browser extension adding a script to the game. The golfer can send **one appeal** (up to 300 characters) from the ban screen.
- **Flagged for review** (not banned): every hole in one (with career aces, club, swing and the card), albatrosses, hole-outs from 120+ yds, 75+ ft putts, low rounds, 2+ aces / 3+ eagles / 3+ chip-ins in a round, rounds played fast, 90%+ PERFECT swings in a round or 25 in a row, shots that fly far past the club's distance, 450+ yd drives, a few scripted taps, the same pull-back or hold time 6 times in a row (macros), the game open in two tabs, the game frozen 8+ seconds twice mid-round while on screen (the debugger), extension frames, earning $25,000+ in an hour, and big or forfeited friends-match pots.

**Flagged rounds come with their scorecard.** Any flag raised during a round carries the card so far (and which hole it happened on), and when a flagged round ends the finished scorecard is sent too. In 🚩 Cheat flags, **📋 Round** shows that round's card (and its final card); **📋 All** shows every scorecard the golfer has (from their ban note, flags and Google cloud save).

**Appeals.** 📨 Appeals in the creator tools lists every appeal (waiting ones first) with the ban reason, the golfer's message and 📋 scorecards. ✅ Unban lifts the ban (they can play within about 15 minutes; old scores don't come back) and ✕ Turn down makes it final (they see that on their ban screen). Manual bans ask whether the golfer can appeal. Bans show "final" or "can appeal".

**Banned golfers are taken off every leaderboard**: their scores are deleted (all-time, the last week of daily tournaments and Closest to the Pin) and a small banned list (`meta/bannedList`) hides them from every board, the tournament leaders and the prize payouts. Their holes in one are hidden too. This also cleans up auto-bans whenever the creator tools are opened.

**Server side (firestore.rules)**: only you can write your own save, scores and flags; the cloud bank can never be more than $5,000 over everything earned; scores and names are range-checked and filtered; score times must be within 2 days of now; boards only accept a better score; banned golfers can't post; only the creator's verified Google account can ban, unban, delete scores or give badges; a golfer's own game can make its auto-ban harsher but never softer; appeals need an existing ban that allows them.

**Other**: flags made before the game is online wait in a queue; the game keeps each golfer's last 15 scorecards (sent with an auto-ban, or the next time a creator-banned golfer's game checks in).

- The creator's account (🛡️ button on the home screen) has Find a player (search by name, give or take back Creator's Pick 🎁, ban), 🎯 Holes in one (every ace from the last 3 days with each golfer's career total, 📋 scorecards, ban), 🚩 Cheat flags (filters for aces, interference/tampering and money; 📋 Round and 📋 All), 📨 Appeals, ⛔ Bans (with 📋 scorecards) and the leaderboards (remove a score, ban, 🎁).
- Player counts, players online and rounds played are in Google Analytics.

## Updates and pop-ups

- To announce an update to players, edit `NEWS_VER` and the `NEWS` list in index.html. Each golfer sees it once. Only list things players can see (nothing about anti-cheat or creator tools).
- **Every release:** bump `GAME_VER` in index.html and `"game"` in `version.json` to the same value (and `"news"` / `"num"` to match `NEWS_VER` / `NEWS_NUM` when there's a What's New). Games that are already open check `version.json` every 5 minutes and when the player comes back to the game, then show an "🔄 Update ready · Reload now" pop-up on the home screen (never mid-round). Add each update to the `UPDATES` list too (the "📜 Previous updates" page).
- New players get a welcome pointing them to the 3C Par Three, plus one-time tips the first time they open Clubs and Golfer.

## Firebase free plan

The game is built to stay on the free Spark plan (50,000 reads and 20,000 writes a day; on Spark Firebase never charges, it just pauses online features until midnight Pacific if a limit is hit):

- Cloud saves (Google sign-in) go up only when a round ends, after buying something or collecting winnings, and when the game is closed. The device always saves instantly.
- Leaderboards are remembered for 5 minutes, even through a reload. Your own new score is added to the remembered board instead of downloading it again, and posting skips the "current best" lookup.
- Today's tournaments card only loads when someone taps "See today's leaders" (then it's remembered for 10 minutes).
- Today's holes-in-one are one record per day (the creator tools read the last 3 days).
- The banned list is one record (1 read per visit, remembered for 30 minutes).
- The Creator's Pick count loads once per visit; the ban check runs every 15 minutes.
- Play Friends is joined by match code only (no friend codes or invite inbox to watch). Stroke play and best ball send one score per hole; scramble and alt shot send every shot because players take turns.
- Cloud saves check for newer progress at most once a minute when you come back to the game (1 read).
- No "last seen" notes or daily counters: those stats come from Google Analytics.
- The creator's Find a player search uses a tiny player directory: one record per golfer, written only when they first pick a name or change it.

## Google Analytics

On, with Measurement ID `G-4D02FQ9XMJ` (`GA_ID` in index.html). Players online, players per day, new players, rounds started and finished, aces and Closest to the Pin shots show up in Google Analytics (Firebase console > Analytics, or analytics.google.com). It's free and doesn't count against Firebase's database limits.

## Firebase setup

1. Publish the rules in `firestore.rules` (Firebase console > Firestore Database > Rules > Publish). **Publish them again for update 2.0 (Oct 20 2026)**: it adds appeals, scorecards on cheat flags, the hard-ban mark and the Daily Champion win count. (Until you do, appeals can't be sent; scores and flags still post without the new fields.)
2. Turn on guest sign-in: Firebase console > Authentication > Sign-in method > **Anonymous** > Enable. (Without it, only Google-signed-in players can post scores.)

ChamiCards will be back.

## License

MIT
