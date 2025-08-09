# World Rugby ranking calculator

Exploration of future World Rugby rankings based on game result predictions.

## Input files

We need to input files: current rankings, and a list of fixtures.

### Initial rankings

Current rankings are provided as a TSV file with no header. Each row contains a country and its ranking points. Countries are typically sorted in decreasing order of ranking points, but this is not a requirement.

Two files are given in the repository: `rankings_mens.tsv` and `rankings_womens.tsv`. They are the complete rankings as of 4 August 2025.

### Fixtures

The fixture list is provided as another TSV file with no header. Each row represents one fixture. The fixture can be in the past, or in the future. 

When a fixture result is known, the row contains six elements: team A, team  B, flag 1, flag 2, the score for team A, and the score for team B. The first flag indicates whether the fixture is a home game for team A (*home*) or is played at a neutral venue (*neutral*). The second flag indicates whether the fixture is a World Cup game (*RWC*) or not (*standard*).

When a fixture result is not know, the row contains eight elements. The first four elements are still the two teams and the two flags, with the same meanings. They are followed by five values that represent predicted probabilities for all possible outcomes: team A winning by strictly more than 15 points, team A winning by up to 15 points, a draw, team B winning by up to 15 points, and team B winning by strictly more than 15 points. Altogether they need to add up to 1.

The fixture list is not assumed to be an exhaustive list of all international games. It is a selection of fixtures of interest. As such, the method calculates ranking points for all the teams that are part of the fixture list, but does not necessarily produces an 'exact' ranking (in the sense of being complete).
Of course, if the list happens to be exhaustive, then all countries have updated points and the rankings are complete.

The fixtures are assumed to be listed in chronological order.

Rows starting with '#' are comments and are ignored.

### Calculation method

...