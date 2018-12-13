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

## 5. Select and count

1.
```

```

2.
```

```

3.
```

```


4.
```

```

5.
```

```

6.
```

```


7.
```

```

8.
```

```

## 6. Join

1.
```

```

2.
```

```

3.
```

```


4.
```

```

5.
```

```

6.
```

```


7.
```

```

8.
```

```

9.
```

```

10.
```

```

11.
```

```

12.
```

```

13.
```

```

## 7. More join

1.
```

```

2.
```

```

3.
```

```


4.
```

```

5.
```

```

6.
```

```


7.
```

```

8.
```

```

9.
```

```

10.
```

```

11.
```

```

12.
```

```

13.
```

```

14.
```

```

15.
```

```


## 8. Using null

1.
```

```

2.
```

```

3.
```

```


4.
```

```

5.
```

```

6.
```

```


7.
```

```

8.
```

```

9.
```

```

10.
```

```


## 9. Self Join

1.
```

```

2.
```

```

3.
```

```


4.
```

```

5.
```

```

6.
```

```


7.
```

```

8.
```

```

9.
```

```

10.
```

```
