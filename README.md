# sql_zoo
http://sqlzoo.net/wiki/SQL_Tutorial



## 1. Select basics

1.
```
SELECT population FROM world
  WHERE name = 'Germany'
```

2.
```
SELECT name, population FROM world
  WHERE name IN ('Sweden', 'Norway', 'Denmark');
```

3.
```
SELECT name, area FROM world
  WHERE area BETWEEN 200000 AND 250000
```

## 2. Select from world

1.
```
SELECT name, continent, population FROM world
```

2.
```
SELECT name FROM world
WHERE population >= 200000000
```

3.
```
SELECT name, (gdp / population) AS per_capita_gdp FROM world
WHERE population > 200000000
```

4.
```
SELECT name, (population / 1000000) AS population FROM world
WHERE continent = 'South America'
```

5.
```
SELECT name, population FROM world
WHERE name IN ('France', 'Germany', 'Italy');
```

6.
```
SELECT name FROM world 
WHERE name LIKE '%United%'
```

7.
```
SELECT name, population, area FROM world 
WHERE area > 3000000 
OR population > 250000000
```

8.
```
SELECT name, population, area FROM world
WHERE area > 3000000 
XOR population > 250000000
```

9.
```
SELECT name, ROUND(population / 1000000, 2), ROUND(gdp / 1000000000, 2) FROM world
WHERE continent = 'South America'
```

10.
```
SELECT name, ROUND((gdp / population), -3) AS per_capita_gdp FROM world 
WHERE gdp > 1000000000000
```

11.
```
SELECT name, capital FROM world 
WHERE LENGTH(name) = LENGTH(capital)
```

12.
```
SELECT name, capital FROM world
WHERE LEFT(name, 1) = LEFT(capital, 1)
AND NOT name = capital
```

13.
```
SELECT name FROM world 
WHERE name LIKE '%a%'
AND name LIKE '%e%'
AND name LIKE '%i%'
AND name LIKE '%o%'
AND name LIKE '%u%'
AND name NOT LIKE '% %'
```


## 3. Select from nobel

1.
```
SELECT yr, subject, winner
  FROM nobel
 WHERE yr = 1950
```
2.
```
SELECT winner
  FROM nobel
 WHERE yr = 1962
   AND subject = 'Literature'
```

3.
```
SELECT yr, subject
FROM nobel
WHERE winner = 'Albert Einstein';
```

4.
```
SELECT winner
FROM nobel
WHERE subject = 'Peace'
AND yr >= 2000;
```

5.
```
SELECT yr, subject, winner
FROM nobel
WHERE subject = 'Literature'
AND yr BETWEEN 1980 AND 1989;
```

6.
```
SELECT * FROM nobel
 WHERE winner IN ('Theodore Roosevelt',
                  'Woodrow Wilson',
                  'Jimmy Carter',
                  'Barack Obama')

```

7.
```
SELECT winner FROM nobel
WHERE winner LIKE 'John%';
```

8.
```
SELECT * FROM nobel
WHERE (subject = 'Physics' AND yr = 1980) 
OR (subject = 'Chemistry' AND yr = 1984)
```

9.
```
SELECT * FROM nobel
WHERE yr = 1980
AND NOT subject IN ('Chemistry', 'Medicine');
```

10.
```
SELECT * FROM nobel
WHERE (subject = 'Medicine' AND yr < 1910)
OR (subject = 'Literature' AND yr >= 2004)
```

11.
alt + 1 + 2 + 9 = ü (with num lock on)
```
SELECT * FROM nobel
WHERE winner = 'Peter Grünberg'; 
```

12.
```
SELECT * FROM nobel
WHERE winner = 'Eugene O\'neill';
```


13.
```
SELECT winner, yr, subject FROM nobel
WHERE winner LIKE 'Sir%'
```


14.
```
SELECT winner, subject
  FROM nobel
 WHERE yr=1984
 ORDER BY subject IN ('Physics','Chemistry'), subject,winner
```


## 4. Select in select

1.
```SELECT name FROM world
  WHERE population >
     (SELECT population FROM world
      WHERE name='Russia')

```

2.
```
SELECT name
FROM world
WHERE continent = 'Europe' AND
gdp/population > (SELECT gdp/population FROM world WHERE name = 'United Kingdom')
```

3.
```
SELECT name, continent FROM world 
WHERE continent IN (SELECT continent FROM world WHERE name IN ('Argentina', 'Australia')) 
ORDER BY name;
```


4.
```
SELECT name, population FROM world
WHERE population > (SELECT population FROM world WHERE name = 'Canada') 
AND population < (SELECT population FROM world WHERE name = 'Poland')
```

5.
```
SELECT name, CONCAT(ROUND(((population * 100) / (SELECT population FROM world WHERE name = 'Germany'))), '%') AS population FROM world
WHERE continent = 'Europe'
```

6.
```
SELECT name FROM world 
WHERE gdp > ALL(SELECT gdp FROM world WHERE gdp > 0 AND continent = 'Europe')
```


7.
```
SELECT continent, name, area FROM world x
  WHERE area >= ALL
    (SELECT area FROM world y
        WHERE y.continent=x.continent
          AND area >0)
```

8.
```
SELECT continent, name FROM world x
WHERE name <= ALL(SELECT name FROM world y WHERE x.continent = y.continent)
```

9.
```

```

10.
```

```

## 5. SUM and COUNT

1.
```
SELECT SUM(population)
FROM world
```

2.
```
SELECT DISTINCT continent
FROM world
```

3.
```
SELECT SUM(gdp)
FROM world
WHERE continent = 'Africa'
```


4.
```
SELECT COUNT(name)
FROM world
WHERE area >= 1000000
```

5.
```
SELECT SUM(population)
FROM world
WHERE name IN ('Estonia', 'Latvia', 'Lithuania')
```

6.
```
SELECT continent, COUNT(name)
FROM world
GROUP BY continent
```


7.
```
SELECT continent, COUNT(name)
FROM world
WHERE population >= 10000000
GROUP BY continent
```

8.
```
SELECT continent
FROM world
GROUP BY continent
HAVING SUM(population) >= 100000000
```

## 6. Join

1.
```
SELECT matchid, player FROM goal 
  WHERE teamid = 'GER'
```

2.
```
SELECT id, stadium, team1, team2
  FROM game
WHERE id = 1012
```

3.
```
SELECT player, teamid, stadium, mdate
  FROM game JOIN goal 
  ON game.id = goal.matchid
WHERE goal.teamid = 'GER'
```


4.
```
SELECT team1, team2, player
  FROM game 
JOIN goal 
  ON game.id = goal.matchid
WHERE goal.player LIKE 'Mario%'
```

5.
```
SELECT player, teamid, coach, gtime
  FROM goal 
 JOIN eteam
  ON goal.teamid = eteam.id
WHERE goal.gtime <= 10
```

6.
```
SELECT game.mdate, eteam.teamname
  FROM game
 JOIN eteam
  ON game.team1 = eteam.id
WHERE eteam.coach = 'Fernando Santos'
```


7.
```
SELECT player 
  FROM goal
 JOIN game
  ON goal.matchid = game.id  
WHERE game.stadium = 'National Stadium, Warsaw'
```

8.
```
SELECT DISTINCT player
  FROM game 
 JOIN goal 
  ON goal.matchid = game.id 
WHERE (game.team1 = 'GER' OR game.team2 = 'GER')
AND (goal.teamid != 'GER')
```

9.
```
SELECT teamname, COUNT(teamname) as goals
  FROM eteam 
 JOIN goal 
  ON id=teamid
GROUP BY teamname
```

10.
```
SELECT stadium, COUNT(player) as goals
  FROM game
 JOIN goal
  ON game.id = goal.matchid
GROUP BY stadium
```

11.
```
SELECT matchid, mdate, COUNT(teamid)
  FROM game 
 JOIN goal 
  ON matchid = id 
WHERE (team1 = 'POL' OR team2 = 'POL')
GROUP BY matchid, mdate
```

12.
```
SELECT matchid, mdate, COUNT(teamid)
  FROM game 
 JOIN goal 
  ON matchid = id 
WHERE teamid = 'GER'
GROUP BY matchid, mdate
```

13.
```

```

## 7. More join

1.
```
SELECT id, title
 FROM movie
 WHERE yr=1962
```

2.
```
SELECT yr
 FROM movie
 WHERE title = 'Citizen Kane'
```

3.
```
SELECT id, title, yr
 FROM movie
 WHERE title LIKE '%Star Trek%'
ORDER BY yr
```


4.
```
SELECT id
 FROM actor
 WHERE name = 'Glenn Close'
```

5.
```
SELECT id
 FROM movie
 WHERE title = 'Casablanca'
```

6.
```
SELECT name
 FROM actor
JOIN casting
 ON actor.id = casting.actorid
WHERE casting.movieid = 11768
```


7.
```
SELECT name
 FROM actor
JOIN casting
 ON actor.id = casting.actorid
JOIN movie
 ON movie.id = casting.movieid
WHERE movie.title = 'Alien'
```

8.
```
SELECT title
 FROM movie
JOIN casting
 ON movie.id = casting.movieid
JOIN actor
 ON casting.actorid = actor.id
WHERE actor.name = 'Harrison Ford'
```

9.
```
SELECT title
 FROM movie
JOIN casting
 ON movie.id = casting.movieid
JOIN actor
 ON casting.actorid = actor.id
WHERE actor.name = 'Harrison Ford' AND casting.ord != 1
```

10.
```
SELECT movie.title, actor.name
 FROM movie
JOIN casting
 ON movie.id = casting.movieid
JOIN actor
 ON casting.actorid = actor.id
WHERE movie.yr = 1962 AND casting.ord = 1
```

11.
```

SELECT yr, COUNT(title) AS movies
 FROM movie
JOIN casting
 ON movie.id = casting.movieid
JOIN actor
 ON casting.actorid = actor.id
WHERE name = 'John Travolta'
GROUP BY yr
HAVING movies = (
  SELECT MAX(c) FROM (
    SELECT yr, COUNT(title) AS c 
      FROM movie
      JOIN casting
       ON movie.id = casting.movieid
      JOIN actor
       ON casting.actorid = actor.id
      WHERE name = 'John Travolta'
      GROUP BY yr
  ) AS t
)
```

12.
```
SELECT title, name
FROM movie
  JOIN casting ON (movieid = movie.id AND ord = 1)
  JOIN actor ON (actorid = actor.id)
WHERE movie.id IN (
  SELECT movieid FROM casting
    WHERE actorid IN (
       SELECT id FROM actor
         WHERE name='Julie Andrews')
)
```

13.
```
SELECT actor.name FROM actor
  INNER JOIN casting
    ON casting.actorid = actor.id
  INNER JOIN movie
    ON casting.movieid = movie.id
WHERE casting.ord = 1
GROUP BY actor.name
HAVING COUNT(casting.movieid) >= 30
```

14.
```
SELECT movie.title, COUNT(casting.actorid) AS number_of_actors
 FROM movie
 JOIN casting
  ON casting.movieid = movie.id
WHERE yr = 1978
GROUP BY movie.title
ORDER BY number_of_actors DESC, movie.title ASC
```

15.
```

```


## 8. Using null

1.
```
SELECT name
 FROM teacher
WHERE dept IS NULL
```

2.
```
SELECT teacher.name, dept.name
 FROM teacher
INNER JOIN dept
 ON teacher.dept = dept.id
```

3.
```
SELECT teacher.name, dept.name FROM teacher
LEFT JOIN dept
ON teacher.dept = dept.id
```


4.
```
SELECT teacher.name, dept.name FROM teacher
RIGHT JOIN dept
ON teacher.dept = dept.id
```

5.
```
SELECT name, COALESCE(mobile, '07986 444 2266') AS phone
 FROM teacher
```

6.
```
SELECT teacher.name, COALESCE(dept.name, 'None') AS department_name
 FROM teacher
LEFT JOIN dept
 ON teacher.dept = dept.id
```


7.
```
SELECT COUNT(teacher.name) AS teachers, COUNT(teacher.mobile) AS mobile
 FROM teacher
```

8.
```
SELECT dept.name AS department, COUNT(teacher.name) AS staff
 FROM teacher
RIGHT JOIN dept
 ON dept.id = teacher.dept
GROUP BY dept.name
```

9.
```
SELECT teacher.name,
   CASE WHEN dept.id = 1 OR dept.id = 2 THEN ' Sci'
        ELSE ' Art'
   END
FROM teacher
 LEFT JOIN dept ON (teacher.dept = dept.id)

```

10.
```
SELECT teacher.name,
   CASE WHEN dept.id = 1 OR dept.id = 2 THEN ' Sci'
        WHEN dept.id = 3 THEN ' Art'
        ELSE ' None'
   END
FROM teacher
 LEFT JOIN dept ON (teacher.dept = dept.id)
```


## 9. Self Join

1.
```
SELECT COUNT(*) FROM stops
```

2.
```
SELECT id 
 FROM stops
WHERE name = 'Craiglockhart'
```

3.
```
SELECT stops.id, stops.name FROM route
INNER JOIN stops
ON stops.id = route.stop
WHERE company = 'LRT' AND num = 4
```


4.
```
SELECT company, num, COUNT(*) AS count
FROM route 
  WHERE stop=149 
   OR stop=53
GROUP BY company, num
HAVING count = 2
```

5.
```
SELECT a.company, a.num, a.stop, b.stop
FROM route a JOIN route b ON
  (a.company=b.company AND a.num=b.num)
WHERE a.stop = 53 AND b.stop = 149 
```

6.
```
SELECT a.company, a.num, stopa.name, stopb.name
FROM route a JOIN route b ON
  (a.company=b.company AND a.num=b.num)
  JOIN stops stopa ON (a.stop=stopa.id)
  JOIN stops stopb ON (b.stop=stopb.id)
WHERE stopa.name='Craiglockhart' AND stopb.name = 'London Road'
```


7.
```
SELECT a.company, a.num
 FROM route a 
  JOIN route b
    ON (a.company = b.company AND a.num = b.num)
  JOIN stops stopa ON (a.stop = stopa.id)
  JOIN stops stopb ON (b.stop = stopb.id)
 WHERE stopa.name = 'Haymarket' AND stopb.name = 'Leith'
 GROUP BY company, num
```

8.
```
SELECT a.company, a.num 
FROM route a
 JOIN route b
  ON a.company = b.company AND a.num = b.num
 JOIN stops stopa ON a.stop = stopa.id
 JOIN stops stopb ON b.stop = stopb.id
WHERE stopa.name = 'Craiglockhart' AND stopb.name = 'Tollcross'
GROUP BY a.company, a.num
```

9.
```
SELECT stopb.name, a.company, a.num
 FROM route a 
  JOIN route b ON (a.company = b.company AND a.num = b.num)
  JOIN stops stopa ON stopa.id = a.stop
  JOIN stops stopb ON stopb.id = b.stop
 WHERE a.company = 'LRT' AND stopa.name = 'Craiglockhart'
 GROUP BY company, num, name
 ORDER BY stopb.name ASC
```

10.
```

```
