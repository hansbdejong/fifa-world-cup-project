# fifa-world-cup-project

For the course Databases and Information Systems (CIS 550), we designed and built a full stack web application to query and display data from all World Cups. An experienced teaching assistant for this course called our project "insane", telling us that our project was the best project they had ever seen for this course. I took the lead for this project.

We cleaned and merged datasets from multiple sources (including web scraping) and then designed and created our normalized (Third Normal Form) SQL database that we deployed on AWS RDS. The frontend was built using React and Material UI. Users can explore past World Cup results, zoom in to individual match statistics, find player and country statistics, explore individual stadiums, and gain insights such as top scorers and timing of goals.

**Skills:** Database Design, Web Scraping, Entity Resolution, DataGrip, SQL, AWS, RDS, JavaScript, HTML, CSS, React, Express, Node.js, Material UI, Leaflet.js

### Figure 1:
Select World Cup for overall stats and matches.

<br>

<p align="center">
  <img src="https://github.com/hansbdejong/fifa-world-cup-project/blob/main/fifa-world-cup-gifs/world-cups.gif" 
        width="70%" height="70%">
</p>

<br>

### Figure 2:
Search by national team, shows most important stats for that team.

<br>

<p align="center">
  <img src="https://github.com/hansbdejong/fifa-world-cup-project/blob/main/fifa-world-cup-gifs/national-teams.gif" 
        width="70%" height="70%">
</p>

<br>

### Figure 3:
Search by player, shows most important stats for that player.

<br>

<p align="center">
  <img src="https://github.com/hansbdejong/fifa-world-cup-project/blob/main/fifa-world-cup-gifs/player-search.gif" 
        width="70%" height="70%">
</p>

<br>

### Figure 4:
Detailed match stats.

<br>

<p align="center">
  <img src="https://github.com/hansbdejong/fifa-world-cup-project/blob/main/fifa-world-cup-gifs/match-view.gif" 
        width="70%" height="70%">
</p>

<br>

### Figure 5:
Search by stadium, shows most important stats for that stadium.

<br>

<p align="center">
  <img src="https://github.com/hansbdejong/fifa-world-cup-project/blob/main/fifa-world-cup-gifs/stadiums.gif" 
        width="70%" height="70%">
</p>

<br>

### Figure 6:
Search for all matches between two national teams.

<br>

<p align="center">
  <img src="https://github.com/hansbdejong/fifa-world-cup-project/blob/main/fifa-world-cup-gifs/head-to-head.gif" 
        width="70%" height="70%">
</p>

<br>

### Figure 7:
Search for top scorers by national team and/or year.

<br>

<p align="center">
  <img src="https://github.com/hansbdejong/fifa-world-cup-project/blob/main/fifa-world-cup-gifs/top-scorers.gif" 
        width="70%" height="70%">
</p>

<br>

### Figure 8:
Examine timing of goals by national team and/or year.

<br>

<p align="center">
  <img src="https://github.com/hansbdejong/fifa-world-cup-project/blob/main/fifa-world-cup-gifs/timing-of-goals.gif" 
        width="70%" height="70%">
</p>

<br>

### Figure 9:
All time world cup standings.

<br>

<p align="center">
  <img src="https://github.com/hansbdejong/fifa-world-cup-project/blob/main/fifa-world-cup-gifs/all-time-table.gif" 
        width="70%" height="70%">
</p>

<br>

## API Details

### GET /world-cups
**Description:** Returns all of the years that the World Cup has been played <br>
**Parameters:** None <br>
**Response:** An array of objects in the following form: <br>
{ <br>
"year": INT <br>
} <br>

### GET /teams
**Description:** Returns all teams that have ever played in a World Cup <br>
**Parameters:** None <br>
**Response:** An array of objects in the following form: <br>
{ <br>
"country_code": STRING(3), <br>
"country_name": STRING, <br>
"flag_url_low_res": STRING <br>
} <br>

### GET /search/players
**Description:** Returns a list of players matching the passed in optional parameters <br>
**Parameters:** Name (Query, Optional, String), Year (Query, Optional, Int), Country code (Query,
Optional, String(3)) <br>
**Response:** An array of objects with the following form: <br>
{<br>
"id": INT,<br>
"player_name": STRING,<br>
"country_code": STRING(3),<br>
"country_name": STRING,<br>
"position": STRING,<br>
"year": STRING,<br>
"flag_url": STRING<br>
}<br>

### GET /filter/years
**Description:** Gets all World Cup years formatted for autocomplete <br>
**Parameters:** None <br>
**Response:** An array of objects with the following form: <br>
{ <br>
"label": STRING <br>
}<br>

### GET /filter/countries<br>
**Description:** Gets all World Cup countries formatted for search autocomplete<br>
**Parameters:** None<br>
**Response:** An array of objects with the following form:<br>
{<br>
"label": STRING,<br>
"country_code": STRING(3)<br>
}<br>

### GET /top-scorer/wc/:year
**Description:** Returns the top 4 scorers for any particular world cup<br>
**Parameters:** Year (Path, Required, Int)<br>
**Response:** An array of four objects with the following form:<br>
{<br>
"goals": INT,<br>
"player_name": STRING,<br>
"player_id": INT<br>
}<br>

### GET /top-teams/:year
**Description:** Returns the top 4 teams for any particular world cup <br>
**Parameters:** Year (Path, Required, Int) <br>
**Response:** An array of objects with the following form: <br>
{ <br>
"country_name": STRING, <br>
"flag_url": STRING,<br>
"country_code": STRING(3)<br>
}<br>

### GET /matches/wc/:year
**Description:** Returns all the matches for a world cup<br>
**Parameters:** Year (Path, Required, Int)<br>
**Response:** An array of objects with the following form:<br>
{<br>
"stage": STRING,<br>
"stage_id": INT,<br>
"date": STRING,<br>
"homeTeamName": STRING,<br>
"homeTeamCode": STRING(3),<br>
"awayTeamName": STRING,<br>
"awayTeamCode": STRING(3),<br>
"homeTeamFlag": STRING,<br>
"awayTeamFlag": STRING,<br>
"homeTeamGoals": INT,<br>
"awayTeamGoals": INT,<br>
"winCondition": STRING,<br>
"matchId": INT<br>
}<br>

### GET /team/overall-stats/:country
**Description:** The overall statistics for a specified country <br>
**Parameters:** Country (Path, Required, String(3)) <br>
**Response:** An array of objects with the form: <br>
{<br>
"country_name": STRING,<br>
"games_played": INT,<br>
"wins": INT,<br>
"draws": INT,<br>
"losses": INT,<br>
"goals_scored": INT,<br>
"goals_conceded": INT,<br>
"flag_url": STRING<br>
}<br>

### GET /team/standings-by-wc/:country
**Description:** Returns the standings for a country by each world cup in which they participated<br>
**Parameters:** Country (Path, Required, String(3))<br>
**Response:** An array of objects with the following form:<br>
{<br>
"year": INT,<br>
"stage": STRING,<br>
"first": STRING(3),<br>
"second": STRING(3),<br>
"third": STRING(3),<br>
"fourth": STRING(3)<br>
}<br>

### GET /team/top-scorers/:country
**Description:** Top scorers for a country across ALL world cups<br>
**Parameters:** Country (Path, Required, String(3))<br>
**Response:** An array of objects with the following form:<br>
{<br>
"player_name": STRING,<br>
"player_id": INT,<br>
"world_cups_played": STRING,<br>
"games_played": INT,<br>
"goals": INT<br>
}<br>

### GET /team/all-matches/:country
**Description:** Returns all matches across all world cups in which the country played<br>
**Parameters:** Country (Path, Required, String(3))<br>
**Response:** An array of objects with the following form:<br>
{<br>
"year": INT,<br>
"stage": STRING,<br>
"date": STRING,<br>
"homeTeamName": STRING,<br>
"homeTeamCode": STRING(3),<br>
"awayTeamName": STRING,<br>
"awayTeamCode": STRING(3),<br>
"homeTeamFlag": STRING,<br>
"awayTeamFlag": STRING,<br>
"homeTeamGoals": INT,<br>
"awayTeamGoals": INT,<br>
"winCondition": STRING,<br>
"matchId": INT<br>
}<br>

### GET /player/overall-stats/:playerId
**Description:** Overall sta\s for the specific player<br>
**Parameters:** Player ID (Path, Required, Int)<br>
**Response:** An array with an object with the following form:<br>
{<br>
"player_name": STRING,<br>
"borndate": STRING,<br>
"Position": STRING,<br>
"JerseyNumber": STRING,<br>
"country": STRING,<br>
"worldcupsplayed": STRING,<br>
"TotalGames": INT,<br>
"wins": INT,<br>
"losses": INT,<br>
"draws": INT,<br>
"goals": INT,<br>
"YellowCards": INT,<br>
"RedCards": INT,<br>
"clubteams": STRING,<br>
"flag_url": STRING<br>
}<br>

### GET /player/matches/:playerId
**Description:** All the matches in which the player has taken part<br>
**Parameters:** Player ID (Path, Required, Int)<br>
**Response:** An array of objects with the following form:<br>
{<br>
"match_id": INT,<br>
"goals": INT,<br>
"year": INT,<br>
"date": STRING,<br>
"stage": STRING,<br>
"home_team_name": STRING,<br>
"home_team_code": STRING(3),<br>
"away_team_name": STRING,<br>
"away_team_code": STRING(3),<br>
"home_team_goals": INT,<br>
"away_team_goals": INT,<br>
"home_team_flag": STRING,<br>
"away_team_flag": STRING,<br>
"win_conditions": STRING<br>
}<br>

### GET /stadiums
**Description:** Returns the latitude, longitude, and high-level data about all world cup stadiums<br>
**Parameters:** None<br>
**Response:** An array of objects with the following form:<br>
{<br>
"stadium_id": INT,<br>
"stadiumName": STRING,<br>
"stadiumLat": FLOAT,<br>
"stadiumLong": FLOAT,<br>
"country": STRING,<br>
"city": STRING,<br>
"lifetimeGoals": INT,<br>
"yearsHosted": STRING,<br>
"lifetimeMatches": INT,<br>
"flag": STRING<br>
}<br>

### GET /stadiums/:stadiumId
**Description:** Returns detailed statistics about a specific world cup stadium<br>
**Parameters:** Stadium ID (Path, Required, Int)<br>
**Response:** An array with an object with the form:<br>
{<br>
"stadiumId": INT,<br>
"stadiumName": STRING,<br>
"country": STRING,<br>
"city": STRING,<br>
"lifetimeGoals": INT,<br>
"yearsHosted": STRING,<br>
"lifetimeMatches": INT,<br>
"yellowCards": INT,<br>
"redCards": INT,<br>
"flag": STRING,<br>
"topScorer": STRING<br>
}<br>

### GET stadiums/matches/:stadiumId
**Description:** Returns all the matches that occured at a specific stadium<br>
**Parameters:** Stadium ID (Path, Required, Int)<br>
**Response:** An array of objects with the following form:<br>
{<br>
"stage": STRING,<br>
"date": STRING,<br>
"year": INT,<br>
"homeTeamName": STRING,<br>
"homeCountryCode": STRING(3),<br>
"awayTeamName": STRING,<br>
"awayCountryCode": STRING(3),<br>
"homeTeamFlag": STRING,<br>
"awayTeamFlag": STRING,<br>
"homeTeamGoals": INT,<br>
"awayTeamGoals": INT,<br>
"winCondition": STRING,<br>
"match_id": INT<br>
}<br>

### GET /all-time-table
**Description:** Returns all data associated with all teams ever to perform in the world cup<br>
**Parameters:** None<br>
**Response:** An array of objects with the following form:<br>
{<br>
"country_code": STRING(3),<br>
"team": STRING,<br>
"matches": INT,<br>
"win": INT,<br>
"loss": INT,<br>
"draw": INT,<br>
"goals": INT,<br>
"concedes": INT,<br>
"diff": INT,<br>
"points": INT,<br>
"flag_url_low_res": STRING<br>
}<br>

### GET /head-to-head
**Description:** Returns all time performance data across two teams that are passed in <br>
**Parameters:** team1 (Query, Optional, String(3)), team2 (Query, Optional, String(3)) <br>
**Response:** An array of objects with the following form: <br>
{<br>
"win_conditions": STRING,<br>
"homeTeamCode": STRING(3),<br>
"awayTeamCode": STRING(3),<br>
"year": INT,<br>
"date": STRING,<br>
"stage": STRING,<br>
"homeTeamName": STRING,<br>
"homeTeamGoals": INT,<br>
"awayTeamName": STRING,<br>
"awayTeamGoals": INT,<br>
"homeTeamFlag": STRING,<br>
"awayTeamFlag": STRING,<br>
"matchId": INT<br>
}<br>

### GET /search/top-scorers
**Description:** Returns the top scorers across all world cups filtered on the optional country and
year parameters<br>
**Parameters:** year (Query, Optional, Int), country (Query, Optional, String(3))<br>
**Response:** An array of objects with the following form:<br>
{<br>
"id": INT,<br>
"player_name": STRING,<br>
"year": STRING,<br>
"goals": INT,<br>
"flag_url": STRING,<br>
"country_name": STRING,<br>
"country_code": STRING(3)<br>
}<br>

### GET /goal-timings
**Description:** Returns all data about the time at which goals were scored across matches filtered
on the year and country optionally passed in<br>
**Parameters:** year (Query, Optional, Int), country (Query, Optional, String(3))<br>
**Response:** An array of objects with the following form:<br>
{<br>
"zero": INT,<br>
"sixteen": INT,<br>
"thirtyone": INT,<br>
"fortysix": INT,<br>
"sixtyone": INT,<br>
"seventysix": INT,<br>
"extra_time": INT<br>
}<br>

### GET /match/overview/:id
**Description:** Returns overview data about a specific match<br>
**Parameters:** ID (Path, Required, Int)<br>
**Response:** An array with an object with the following form:<br>
{<br>
"year": INT,<br>
"date": STRING,<br>
"stage": STRING,<br>
"win_conditions": STRING,<br>
"home_team_code": STRING(3),<br>
"home_team_name": STRING,<br>
"home_team_flag_url": STRING,<br>
"home_team_goals": INT,<br>
"away_team_code": STRING(3),<br>
"away_team_name": STRING,<br>
"away_team_flag_url": STRING,<br>
"away_team_goals": INT,<br>
"home_manager": STRING,<br>
"away_manager": STRING,<br>
"stadium_name": STRING,<br>
"stadium_id": INT,<br>
"attendance": INT,<br>
"referee": STRING,<br>
"referee_country": STRING,<br>
"assistant_1": STRING,<br>
"assistant_1_country": STRING,<br>
"assistant_2": STRING,<br>
"assistant_2_country": STRING<br>
}<br>

### GET /match/home-team-scorers/:id
**Description:** Returns an array of all players on home team that scored<br>
**Parameters:** ID (Path, Required, Int)<br>
**Response:** An array of objects with the form:<br>
{<br>
"player_name": STRING,<br>
"minute": INT<br>
}<br>

### GET /match/away-team-scorers/:id
**Description:** Returns an array of all players on away team that scored<br>
**Parameters:** ID (Path, Required, Int)<br>
**Response:** An array of objects with the form:<br>
{<br>
"player_name": STRING,<br>
"minute": INT<br>
}<br>

### GET /match/home-team-roster/:id
**Description:** Returns the home team roster with events<br>
**Parameters:** ID (Path, Required, Int)<br>
**Response:** An array of objects with the following form:<br>
{<br>
"player_name": STRING,<br>
"player_id": INT,<br>
"jersey_number": INT,<br>
"red_card": INT,<br>
"yellow_card": INT,<br>
"second_yellow_card": INT,<br>
"sub_in": INT,<br>
"sub_out": INT,<br>
"Captain": STRING<br>
}<br>

### GET /match/away-team-roster/:id
**Description:** Returns the away team roster with events<br>
**Parameters:** ID (Path, Required, Int)<br>
**Response:** An array of objects with the following form:<br>
{<br>
"player_name": STRING,<br>
"player_id": INT,<br>
"jersey_number": INT,<br>
"red_card": INT,<br>
"yellow_card": INT,<br>
"second_yellow_card": INT,<br>
"sub_in": INT,<br>
"sub_out": INT,<br>
"Captain": STRING<br>
}<br>






