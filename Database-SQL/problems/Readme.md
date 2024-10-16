# SQL practice problems and solution from LeetCode

1. [Recyclable and Low Fat Products](https://leetcode.com/problems/recyclable-and-low-fat-products/)

```sql
SELECT product_id FROM Products WHERE low_fats = 'Y' AND recyclable = 'Y';
```

2. [Find Customer Referee](https://leetcode.com/problems/find-customer-referee/)

```sql
SELECT name FROM Customer WHERE referee_id != 2 OR referee_id IS NULL;
```

3. [Big Countries](https://leetcode.com/problems/big-countries/)

```sql
SELECT name, population, area FROM World 
WHERE population >= 25000000 OR area >= 3000000;
```

4. [Article Views I](https://leetcode.com/problems/article-views-i/)

```sql
SELECT DISTINCT author_id AS id 
FROM Views
WHERE author_id = viewer_id
ORDER BY id ASC;
```

5. [Invalid Tweets](https://leetcode.com/problems/invalid-tweets/)

```sql
SELECT tweet_id FROM Tweets
WHERE LENGTH(content) > 15;
```

6. []()

```sql

```
