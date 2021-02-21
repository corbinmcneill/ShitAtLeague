# You're Shit At League

A web application to query by League of Legends summoner name to display player statistics. Strong focus
is drawn to poor performances, with witty / insulting quips added to demoralize you.

## Stats to flame for

- rank
- K/D/A
- Down in gold
- Down in experience
- Solo Killed
- Vision
- etc.

## Idea

Metrics return a score from -1 to 1, where 1 is good and -1 is bad. Should try and be uniformly
distributed. Some metrics target players, and some metrics target teams. When looking for things to flame
for, search for the lowest self scores and highest opponent scores. Note: we should probably bias towards
bad self stats. **Additive offset?**

## Backend

### API

Single endpoint. Just query by summonerID / region. Return a `List[GameType]` sorted by score.

A `GameType` contains:
- Score
- Basic stats
- List[Highlights]
  - Statistic
  - Quip (optional)

### Architecture

- Lambda?
- Database for caching?
- OpenAPI public

## Front End / Data Presentation
- Floating Cells
- Links to matches? [op.gg](https://op.gg)?
- Context? How we avoid the shitty text of "7 games ago you had this pretty bad vision score". It  seems
  pretty unconvincing.
  - Show last 10 games always and highlight bad stats on a game by game basis.
  - Only focus on bad trends? Link to specific games where the trend was displayed?
- Floating Cells scaled by relevance.
  - Each floating cell is a game.
  - Low Relevance games are small (faded / translucent) and only show K/D/A and Champion / Role
  - High Relevance games are big
    - k/D/a is highlighted (big emphasis on deaths)
    - "SOLO KILLED [X Times [by Y different people]]"
    - Formatted as STATLINE followed by insult quote.
      