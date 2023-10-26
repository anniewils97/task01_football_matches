# Football Matches - Tasks

Each of the questions/tasks below can be answered using a `SELECT` query. When you find a solution copy it into the code block under the question before pushing your solution to GitHub.

1) Find all the matches from 2017.

```sql
SELECT * FROM matches WHERE season = 2017;


```

2) Find all the matches featuring Barcelona.

```sql
SELECT * FROM matches WHERE hometeam = 'Barcelona' OR awayteam = 'Barcelona';


```

3) What are the names of the Scottish divisions included?

```sql
SELECT DISTINCT name FROM divisions WHERE name LIKE '%Scottish%';

```

4) Find the value of the `code` for the `Bundesliga` division. Use that code to find out how many matches Freiburg have played in that division. HINT: You will need to query both tables

```sql
-- SELECT * FROM divisions WHERE name = 'Bundesliga';
-- SELECT * FROM matches WHERE division_code = 'D1' AND (hometeam = 'Freiburg' OR awayteam = 'Freiburg');
SELECT COUNT(*) FROM matches WHERE division_code = 'D1' AND (hometeam = 'Freiburg' OR awayteam = 'Freiburg');



```

5)  Find the teams which include the word "City" in their name. HINT: Not every team has been entered into the database with their full name, eg. `Norwich City` are listed as `Norwich`. If your query is correct it should return four teams.

```sql
SELECT DISTINCT hometeam FROM matches WHERE hometeam LIKE '%City%';


```

6) How many different teams have played in matches recorded in a French division?

```sql
-- SELECT * FROM divisions WHERE country = 'France';
-- SELECT * FROM matches WHERE division_code IN('F1', 'F2'); all the matches played in a French division
-- SELECT DISTINCT hometeam FROM matches WHERE division_code IN ('F1', 'F2'); all the unique teams
SELECT COUNT(DISTINCT hometeam) FROM matches WHERE division_code IN('F1', 'F2');

```

7) Have Huddersfield played Swansea in any of the recorded matches?

```sql
-- all the actual matches they've played in together
SELECT * FROM matches WHERE hometeam = 'Huddersfield' AND awayteam = 'Swansea' OR hometeam = 'Swansea' AND awayteam = 'Huddersfield';
-- the number of matches playe together
SELECT COUNT(*) FROM matches WHERE hometeam = 'Huddersfield' AND awayteam = 'Swansea' OR hometeam = 'Swansea' AND awayteam = 'Huddersfield';


```

8) How many draws were there in the `Eredivisie` between 2010 and 2015?

```sql
-- getting the division code
-- SELECT * FROM divisions WHERE name = 'Eredivisie';
-- all the draws (431) in full for Eredivisie between those dates
SELECT * FROM matches WHERE division_code = 'N1' AND (season BETWEEN 2010 AND 2015) AND (ftr = 'D');
-- the count of 431
SELECT COUNT(*) FROM matches WHERE division_code = 'N1' AND (season BETWEEN 2010 AND 2015) AND (ftr = 'D');


```

9) Select the matches played in the Premier League in order of total goals scored (`fthg` + `ftag`) from highest to lowest. When two matches have the same total the match with more home goals (`fthg`) should come first. 

```sql
-- SELECT *, (fthg + ftag) AS Sum FROM matches WHERE division_code = 'E0';
-- -- first attempt at combining goals
-- SELECT SUM(fthg) AS total FROM matches WHERE division_code = 'E0'
-- UNION ALL
-- SELECT SUM(ftag) AS total FROM matches WHERE division_code = 'E0';
-- -- second attempt at combining goals + ordering
-- SELECT 'total' AS source, SUM(fthg + ftag) AS total FROM matches WHERE division_code = 'E0' ORDER BY total DESC;
-- -- order of totals goals in DESC fashion.
-- SELECT fthg + ftag AS sum_of_goals FROM matches WHERE division_code = 'E0' ORDER BY sum_of_goals DESC;
-- now full answer
SELECT fthg + ftag AS sum_of_goals FROM matches WHERE division_code = 'E0' ORDER BY sum_of_goals DESC, fthg DESC;

```

10) Find the name of the division in which the most goals were scored in a single season and the year in which it happened.

```sql
SELECT division_code, season, SUM(fthg + ftag) AS sum_of_goals FROM matches GROUP BY division_code, season ORDER BY sum_of_goals DESC;
-- unfinished
```

### Useful Resources

- [Filtering results](https://www.w3schools.com/sql/sql_where.asp)
- [Ordering results](https://www.w3schools.com/sql/sql_orderby.asp)
- [Grouping results](https://www.w3schools.com/sql/sql_groupby.asp)