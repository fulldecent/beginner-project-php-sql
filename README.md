# YOUR FIRST PHP+SQL DATABASE PROJECT

You will create a website that lists the all-time top 50 MLB players (by runs). An index page shows a list of these players, alphabetically by name. A separate page for each player shows fun statistics about that player.

## PREREQUESITES

You must have a basic understanding of HTML for this project.

## TECHNOLOGY STACK

Install PHP on your computer (you may already have it). Test that it works by creating a file: `index.php` containing `<?php echo 'Hello World' ?>` and then running `php -S localhost:8888` and opening a browser to [http://localhost:8888](http://localhost:8888).

Download this file [players.db](players.db).

Install SQLite on your computer (you may already have it). Test that it works by running `sqlite3 players.db .schema` which should print out the format of the data in the provided database (attached).

## WORK PLAN

**Create the view**

- [ ] Create a simple page `ricky-henderson.html` that displays the following information:

  | Name | Henderson, R |
  | ---- | ------------ |
  | Pos  | LF           |
  | G    | 3081         |
  | AB   | 10961        |
  | R    | 2295         |
  | H    | 3055         |
  | 2B   | 510          |
  | 3B   | 66           |
  | HR   | 297          |
  | RBI  | 1115         |
  | BB   | 2190         |
  | SO   | 1694         |
  | SB   | 1406         |
  | CS   | 335          |
  | AVG  | 0.279        |
  | OBP  | 0.401        |
  | SLG  | 0.419        |
  | OPS  | 0.82         |

  - You can learn what these stats mean by hovering over the table headngs at http://mlb.mlb.com/stats
  - Use Bootstrap or Bulma.

- [ ] Create a simple page `index.html` which lists the name of five baseball players you like and each one of them links to `ricky-henderson.html`.

- [ ] Rename `index.html` to `index.php` and `ricky-henderson.html` to `player.php`, keep your PHP server open so you can confirm these files still work.

- [ ] Use this code as a "mock" for your database query of all player names. This represents the format of data you will get later. Figure out how to weave this into your current code so that the PHP code creates the HTML code you want.

  ```php
  <?php
  $playerNames = ['Henderson, R', 'Batty McBatson', 'Pitcher DeSusa'];
  foreach ($playerNames as $playerName) {
  ?>
    
  <p>HERE IS A PLAYER: <?php echo $playerName; ?> </p>
  
  <?php
  }
  ?>
  ```

- [ ] Use this code as a mock for your database query about player details. Add the data from above in this mock and use the method below to weave the information "from the database" into your HTML.

  ```php
  <?php
  $playerName = 'Henderson, R';
  $playerDetails = ['Pos'=>'LF'];
  ?>
  
  <p>THE PLAYER NAME IS: <?php echo $playerName; ?> </p>
  <p>THE PLAYER POSITION IS: <?php echo $playerDetails['Pos']; ?> </p>
  ```


- [ ] Update `index.php` so that that the links go to like `player.php?player=Henderson, R`

**Create the model**

- [ ] Create a SQL query which extracts the names of all players in the provided database.

  ```sh
  # Hint: here's how you run a query, this one extract all data from the database
  sqlite3 -header players.db 'SELECT * FROM players'
  ```

- [ ] Create a SQL query which returns all data for the player `Henderson, R`.

**Create the controller**

- [ ] Read https://phpdelusions.net/pdo sections "Connecting. DSN" and "Running SELECT INSERT, UPDATE, or DELETE statements" to understand best practices we will use here. Today we will use a SELECT query and `fetchAll()` to get data into the variable (see "Getting a column").
- [ ] At the bottom of the `index.php` file, try to use the PHP Delusions technique, and the "all player names" query you developed to extract the data from the database into the variable `$playerNames`. 
- [ ] Use this code `<?php var_dump($playerNames); ?> ` in your code to inspect the contents of this variable.
- [ ] Make changes as needed until your variable has a format similar to the mock database query of player names above.
- [ ] Weave in this query to replace the mock.
- [ ] Do the same thing on `player.php` to query the database about `$playerName` (which happens to be `Henderson, R` right now). This will also require using a query that includes a `?` in it and the `exec([...])` command.


- [ ] Point your browser to `player.php?player=Henderson, R`, now we want the PHP page to extract that name. Here's how you do that*:

  ```php
  <p>You are searching for: <?php echo $_GET['player'] ; ?> </p>
  ```

  *There is a security vulnerability in this example. You can ignore it for now. The solution is to use `htmlspecialchars()`.* 

- [ ] Use the code `$playerName = $_GET['player']` to connect the name you are querying (in the `?player=…` part of the URL) with the query that selects data from the database.

## YOU'RE DONE

Review the things you have learned today: creating a dynamic web page, reading data from a database, and connecting the web page to the database so that your visitors can get various information.
