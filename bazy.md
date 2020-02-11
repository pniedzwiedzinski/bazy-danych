# Bazy danych


#### Aliasy w intersect
```sql
SELECT orderid AS 'Label tylko w pierwszym selectie'
FROM [Order Details]
WHERE productid = 1
INTERSECT
SELECT orderid
FROM [Order Details]
WHERE productid = 5
```

#### Exists
```sql
SELECT orderid
FROM [Order Details] a
WHERE productid = 1
AND EXISTS (
SELECT orderid
FROM [Order Details] b
WHERE productid = 5
AND a.orderid = b.orderid
)
```

#### WITH AS
```sql
WITH products AS (SELECT CustomerId, ProductID
FROM [Order Details] od
JOIN [Orders] o ON o.[OrderID] = od.[OrderID])

SELECT CustomerId from products
WHERE products.ProductID = 1
INTERSECT
SELECT CustomerId from products
WHERE products.ProductID = 5

-- LUB

WITH products AS (SELECT CustomerId, ProductID
FROM [Order Details] od
JOIN [Orders] o ON o.[OrderID] = od.[OrderID])

SELECT DISTINCT CustomerId
FROM products od
WHERE od.ProductID = 1
AND EXISTS(
    SELECT CustomerId
    FROM products od2
    WHERE od.CustomerId = od2.CustomerId
    AND od2.ProductID = 5
)
```
