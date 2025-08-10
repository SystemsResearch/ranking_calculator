# World Rugby ranking calculator

Exploration of future World Rugby rankings based on game result predictions.

## Input files

We need to input files: current rankings, and a list of fixtures.

### Initial rankings

Current rankings are provided as a TSV file with no header. 
Each row contains a country and its ranking points. Countries are typically sorted in decreasing order of ranking points, but this is not a requirement.

Two files are given in the repository: `rankings_mens.tsv` and `rankings_womens.tsv`. 
They are the complete rankings as of 4 August 2025.

### Fixtures

The fixture list is provided as another TSV file with no header. 
Each row represents one fixture. 
The fixture can be in the past, or in the future. 

When a fixture result is known, the row contains six elements: team A, team  B, flag 1, flag 2, the score for team A, and the score for team B. 
The first flag indicates whether the fixture is a home game for team A (*home*) or is played at a neutral venue (*neutral*). 
The second flag indicates whether the fixture is a World Cup game (*RWC*) or not (*standard*).

When a fixture result is not know, the row contains nine elements. 
The first four elements are still the two teams and the two flags, with the same meanings. 
They are followed by five values that represent predicted probabilities for all possible outcomes: team A winning by strictly more than 15 points, team A winning by up to 15 points, a draw, team B winning by up to 15 points, and team B winning by strictly more than 15 points. 
Altogether they need to add up to 1.

The fixture list is not assumed to be an exhaustive list of all international games. 
It is a selection of fixtures of interest. 
As such, the method calculates ranking points for all the teams that are part of the fixture list, but does not necessarily produces an 'exact' ranking (in the sense of being complete).
Of course, if the list happens to be exhaustive, then all countries have updated points and the rankings are complete.

The fixtures are assumed to be listed in chronological order.

Rows starting with '#' are comments and are ignored.

## Calculation method

The code reads the two input files and prepares the intial rankings and the fixture list. 
Then, it generates a number of simulations, as determined by the variable `n_sim`.

For each simulation, the process stays the same. We create a deep copy of the initial rankings, and go through the fixture list in order. 
For each game, we randomly generate an outcome based on the probabilities provided by the user in the fixture list. 
Based on the outcome of the game, we calculate the point exchange, update the ranking points for both teams, and move to the next game.

Once all the simulations are processed, we explore the results.
We look at the point distribution, the frequency at which a team finishes in the top 6, and which teams are most frequently ranked first.

## Additional comments

The probabilities given in the fixture list are not to be taken too seriously.
They are trying to find a balance between being conservative and still allowing for upsets, so that we can explore their impact on rankings.
They are not meant to reflect a detailed analysis on the probabilites for each game.
The entire point of the repository is for anyone to be able download the code, put their own values for the probabilities, and see the impact on rankings.

## Release notes

v0.2 - Numerical convertion brought earlier: faster, and allows for some input validation.

v0.1 - Initial implementation.