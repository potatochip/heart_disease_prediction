## SQL Challenges
>Get your hands dirty with SQL.

You will use only SQL queries for this.

> A note: `SUM(double_faults)` sums the contents of an entire column.
> If, for each row, you want to add the field values from two columns,
> you can just do `SELECT name, double_faults + unforced_errors`



1) Using the same tennis data, find the number of matches played by each player in each tournament (remember that a player can be present as both player1 or player2)

```
select player, count(*)
    from ((select player1 as player from us_men_2013) union all (select player2 as player from us_men_2013)) all_us_men_players
    group by player order;
select player, count(*)
    from ((select player1 as player from us_ladies_2013) union all (select player2 as player from us_ladies_2013)) all_us_ladies_players
    group by player;
select player, count(*)
    from ((select player1 as player from wimbledon_ladies_2013) union all (select player2 as player from wimbldeon_ladies_2013)) all_wimbledon_ladies_players
    group by player;
select player, count(*)
    from ((select player1 as player from wimbledon_men_2013) union all (select player2 as player from wimbldeon_men_2013)) all_wimbledon_men_players
    group by player;
select player, count(*)
    from ((select player1 as player from french_ladies_2013) union all (select player2 as player from french_ladies_2013)) all_french_ladies_players
    group by player;
select player, count(*)
    from ((select player1 as player from french_men_2013) union all (select player2 as player from french_men_2013)) all_french_men_players
    group by player;
select player, count(*)
    from ((select player1 as player from aus_men_2013) union all (select player2 as player from aus_men_2013)) all_aus_men_players
    group by player;
select player, count(*)
    from ((select player1 as player from aus_ladies_2013) union all (select player2 as player from aus_ladies_2013)) all_aus_ladies_players
    group by player;
```

2) Who has played the most matches total in all of US Open, AUST Open, French Open? Answer this both for men and women.

```
CREATE TEMP TABLE aus_ladies AS
    (select player1 as player from aus_ladies_2013) union all (select player2 as player from aus_ladies_2013);
CREATE TEMP TABLE aus_men AS
    (select player1 as player from aus_men_2013) union all (select player2 as player from aus_men_2013);
CREATE TEMP TABLE us_ladies AS
    (select player1 as player from us_ladies_2013) union all (select player2 as player from us_ladies_2013);
CREATE TEMP TABLE us_men AS
    (select player1 as player from us_men_2013) union all (select player2 as player from us_men_2013);
CREATE TEMP TABLE wimbledon_ladies AS
    (select player1 as player from wimbledon_ladies_2013) union all (select player2 as player from wimbledon_ladies_2013);
CREATE TEMP TABLE wimbledon_men AS
    (select player1 as player from wimbledon_men_2013) union all (select player2 as player from wimbledon_men_2013);
CREATE TEMP TABLE french_ladies AS
    (select player1 as player from french_ladies_2013) union all (select player2 as player from french_ladies_2013);
CREATE TEMP TABLE french_men AS
    (select player1 as player from french_men_2013) union all (select player2 as player from french_men_2013);

CREATE TEMP TABLE all_the_ladies AS
    (select * from aus_ladies) union all (select * from us_ladies) union all (select * from french_ladies) union all (select * from wimbledon_ladies);
CREATE TEMP TABLE all_the_mens AS
    (select * from aus_men) union all (select * from us_men) union all (select * from french_men) union all (select * from wimbledon_men);

SELECT player, count(*) FROM all_the_ladies GROUP BY player ORDER BY count DESC LIMIT 1;
SELECT player, count(*) FROM all_the_mens GROUP BY player ORDER BY count DESC LIMIT 1;
```


3) Who has the highest first serve percentage? (Just the maximum value in a single match)

```
CREATE TEMP TABLE aus_ladies AS
    (select player1 as player, fsp_1 as fsp from aus_ladies_2013) union all (select player2 as player, fsp_2 as fsp from aus_ladies_2013);
CREATE TEMP TABLE aus_men AS
    (select player1 as player, fsp_1 as fsp from aus_men_2013) union all (select player2 as player, fsp_2 as fsp from aus_men_2013);
CREATE TEMP TABLE us_ladies AS
    (select player1 as player, fsp_1 as fsp from us_ladies_2013) union all (select player2 as player, fsp_2 as fsp from us_ladies_2013);
CREATE TEMP TABLE us_men AS
    (select player1 as player, fsp_1 as fsp from us_men_2013) union all (select player2 as player, fsp_2 as fsp from us_men_2013);
CREATE TEMP TABLE wimbledon_ladies AS
    (select player1 as player, fsp_1 as fsp from wimbledon_ladies_2013) union all (select player2 as player, fsp_2 as fsp from wimbledon_ladies_2013);
CREATE TEMP TABLE wimbledon_men AS
    (select player1 as player, fsp_1 as fsp from wimbledon_men_2013) union all (select player2 as player, fsp_2 as fsp from wimbledon_men_2013);
CREATE TEMP TABLE french_ladies AS
    (select player1 as player, fsp_1 as fsp from french_ladies_2013) union all (select player2 as player, fsp_2 as fsp from french_ladies_2013);
CREATE TEMP TABLE french_men AS
    (select player1 as player, fsp_1 as fsp from french_men_2013) union all (select player2 as player, fsp_2 as fsp from french_men_2013);

CREATE TEMP TABLE big_kahuna AS
    (select * from aus_ladies) union all (select * from us_ladies) union all (select * from french_ladies) union all (select * from wimbledon_ladies) union all (select * from aus_men) union all (select * from us_men) union all (select * from french_men) union all (select * from wimbledon_men);

SELECT * FROM big_kahuna ORDER BY fsp DESC LIMIT 1;
```


4) What are the unforced error percentages of the top three players with the most wins? (unforced error percentage is % of points lost due to unforced errors. In a match, you have fields for number of points won by each player, and number of unforced errors for each field).

```
CREATE TEMP TABLE aus_ladies AS
    (select player1 as player, ufe_1 as ufe, result from aus_ladies_2013) union all (select player2 as player, ufe_2 as ufe, result from aus_ladies_2013);
CREATE TEMP TABLE aus_men AS
    (select player1 as player, ufe_1 as ufe, result from aus_men_2013) union all (select player2 as player, ufe_2 as ufe, result from aus_men_2013);
CREATE TEMP TABLE us_ladies AS
    (select player1 as player, ufe_1 as ufe, result from us_ladies_2013) union all (select player2 as player, ufe_2 as ufe, result from us_ladies_2013);
CREATE TEMP TABLE us_men AS
    (select player1 as player, ufe_1 as ufe, result from us_men_2013) union all (select player2 as player, ufe_2 as ufe, result from us_men_2013);
CREATE TEMP TABLE wimbledon_ladies AS
    (select player1 as player, ufe_1 as ufe, result from wimbledon_ladies_2013) union all (select player2 as player, ufe_2 as ufe, result from wimbledon_ladies_2013);
CREATE TEMP TABLE wimbledon_men AS
    (select player1 as player, ufe_1 as ufe, result from wimbledon_men_2013) union all (select player2 as player, ufe_2 as ufe, result from wimbledon_men_2013);
CREATE TEMP TABLE french_ladies AS
    (select player1 as player, ufe_1 as ufe, result from french_ladies_2013) union all (select player2 as player, ufe_2 as u, result from french_ladies_2013);
CREATE TEMP TABLE french_men AS
    (select player1 as player, ufe_1 as ufe, result from french_men_2013) union all (select player2 as player, ufe_2 as ufe, result from french_men_2013);

CREATE TEMP TABLE big_kahuna AS
    (select * from aus_ladies) union all (select * from us_ladies) union all (select * from french_ladies) union all (select * from wimbledon_ladies) union all (select * from aus_men) union all (select * from us_men) union all (select * from french_men) union all (select * from wimbledon_men);

SELECT player, AVG(ufe) as ufe, SUM(result) AS wins FROM big_kahuna GROUP BY player ORDER BY wins DESC LIMIT 3;
```