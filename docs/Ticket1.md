Ticket : 1
Actual cause
  loadStatsFromServer() typo, fetched stat instead of stats, which was outlined in index.ts
File / function:
  src/screens/MenuScreen/MenuScreenController
What was wrong:
  loadStatsFromServer couldn't load stats from api, which set response to always 'null', causing view to display 'Stats unavailable' 
Fix
How did you find it?
  
Hypothesis testing
What hypothesis ultimately led you to identify the buggy code, and why?
  I hypothesized that since the bug was being shown on the menu screen, that the 'Stats unavailable' message was located in MenuScreenView. 
Backward tracing
Symptom:
  updateStats returned "Stats unavailable which meant stats == null.
Traced back to:
  MenuScreenController, where stats was intialized by loadStatsFromServer
Traced back to:
  loadStatsFromServer, where response was fetched from "/api/stat"
Traced back to:
  index.ts, which gets "/api/stats"
Buggy code:
  const response = await fetch("/api/stat");
Confirming the fix
  After inputting given timestamp and score into leaderboard.json, menu screen now displays stat information.
