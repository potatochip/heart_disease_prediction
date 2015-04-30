## SQL Challenges

>Get your hands dirty with SQL.

You will use only SQL queries for this.

 * Using the same tennis data, find the number of matches played by
   each player in each tournament (remember that a player can be
   present as both player1 or player2)

* Who has played the most matches total in all of US Open, AUST Open,
  French Open? Answer this both for men and women.

* Who has the highest first serve percentage? (Just the maximum value
  in a single match)

* What are the unforced error percentages of the top three players
  with the most wins? (unforced error percentage is % of points lost
  due to unforced errors. In a match, you have fields for number of
  points won by each player, and number of unforced errors for each
  field).

> A note: `SUM(double_faults)` sums the contents of an entire column.
> If, for each row, you want to add the field values from two columns,
> you can just do `SELECT name, double_faults + unforced_errors`
