# Lemon Clicker Bug Report

**Name: Eric Murphy**,
**Tickets solved: 2** <!-- e.g. 1, 2, 3, 5, 6 (at least five) -->


---

## Ticket <1>: <Stats always say "Stats unavailable">

### Actual cause
loadStatsFromServer() typo, fetched stat instead of stats, which was outlined in index.ts
<!-- Which file and function was the bug in, and what was wrong with the code?
     Explain why that code produced the behavior described in the ticket. -->

**File / function:**
src/screens/MenuScreen/MenuScreenController
**What was wrong:**
loadStatsFromServer couldn't load stats from api, which set response to always 'null', causing view to display 'Stats unavailable'
### Fix
Changed 
<!-- What did you change, and why does that change fix the problem? -->
Changed /api/stat" to /api/stats", know fetch function accesses correct file.
### How did you find it?

#### Hypothesis testing

**What hypothesis ultimately led you to identify the buggy code, and why?**
I hypothesized that since the bug was being shown on the menu screen, that the 'Stats unavailable' message was located in MenuScreenView.
#### Backward tracing

<!-- Start from the symptom you saw and work backwards, one step at a time,
     until you reach the buggy line. For each step, note where you looked
     and what you saw there. Add steps as needed. -->

1. **Symptom:** <!-- what you saw, e.g. text on screen, console error -->
 updateStats returned "Stats unavailable which meant stats == null.
2. **Traced back to:** <!-- where that came from, e.g. a function, a request in the Network tab, a server log -->
MenuScreenController, where stats was intialized by loadStatsFromServer
3. **Traced back to:**
loadStatsFromServer, where response was fetched from "/api/stat"
4. **Traced back to:**
   index.ts, which gets "/api/stats" 
5. **Buggy code:** <!-- the file, function and line where the trace ended -->
src/screens/MenuScreen/MenuScreenController.ts: line 47
<!-- It is okay to use your judgement here in limiting the number of traceback steps. We want to understand your 


    reasoning for how you discovered where the bug was -->

### Confirming the fix

<!-- How did you confirm the problem is gone? -->
After inputting given timestamp and score into leaderboard.json, menu screen now displays stat information.

## Ticket <2>: <Best score always shows 0>

### Actual cause
<!-- Which file and function was the bug in, and what was wrong with the code?
     Explain why that code produced the behavior described in the ticket. -->
index.ts: app.get(), checks for entries.length < best, should be > best since best should be updated with the greatest score.

**File / function:**
server/index.ts
**What was wrong:**
Stats "Best" parameter always displayed zero despite the actual best score.
### Fix
<!-- What did you change, and why does that change fix the problem? -->
Changed if (entries[i].score < best) to if (entries[i].score > best)
### How did you find it?

#### Hypothesis testing

**What hypothesis ultimately led you to identify the buggy code, and why?**
I hypothesized that since the bug was being shown on the menu screen, MenuScreenView would contain the code that displays the best score.
#### Backward tracing

<!-- Start from the symptom you saw and work backwards, one step at a time,
     until you reach the buggy line. For each step, note where you looked
     and what you saw there. Add steps as needed. -->

1. **Symptom:** <!-- what you saw, e.g. text on screen, console error -->
      Best: ${stats.best} was displaying 0 
2. **Traced back to:** <!-- where that came from, e.g. a function, a request in the Network tab, a server log -->
index.ts: app.get() where stats is changed
3. **Buggy code:** <!-- the file, function and line where the trace ended -->
   index.ts: line 53
   if (entries[i].score > best) {
<!-- It is okay to use your judgement here in limiting the number of traceback steps. We want to understand your 


    reasoning for how you discovered where the bug was -->

### Confirming the fix

<!-- How did you confirm the problem is gone? -->
After inputting given timestamp and score into leaderboard.json, menu screen now displays Best: 19.
