# Business Intelligence Scenarios On _ADVENTUREWORKS2019_ Dataset
# Author: `Hamid Sourghali`

You can find some business insights in different areas listed below on 
====================================================================================
# `OVERVIEW ON InternetSales`
====================================================================================
### Sales Delta Month to Month comparison
```sql
SELECT 
    YEAR(OrderDate) AS OrderYear,
    MONTH(OrderDate) AS OrderMonth,
    SUM(SalesAmount) SUMSales,
    LAG(SUM(SalesAmount)) OVER(ORDER BY YEAR(OrderDate),  MONTH(OrderDate)) AS PreviousMonthSaleAmount,
    SUM(SalesAmount) -  LAG(SUM(SalesAmount)) OVER(ORDER  BY YEAR(OrderDate), MONTH(OrderDate)) AS SalesDelta
FROM 
    FactInternetSales s
GROUP BY
    YEAR(OrderDate),
    MONTH(OrderDate)
```
*Results*
| Year | Month | CurrentMonthSales | PreviousMonthSales  | SalesDelta|
|------|-------|-----------------------|------------------------|-------------------|
| 2010 | 12    | 43,421.0364           | NULL                   | NULL              |
| 2011 | 1     | 469,823.9148          | 43,421.0364            | 426,402.8784     |
| 2011 | 2     | 466,334.903           | 469,823.9148           | -3,489.0118      |
| 2011 | 3     | 485,198.6594          | 466,334.903            | 18,863.7564      |
| 2011 | 4     | 502,073.8458          | 485,198.6594           | 16,875.1864      |
| 2011 | 5     | 561,681.4758          | 502,073.8458           | 59,607.63        |
| 2011 | 6     | 737,839.8214          | 561,681.4758           | 176,158.3456     |
| 2011 | 7     | 596,746.5568          | 737,839.8214           | -141,093.2646    |
| 2011 | 8     | 614,557.935           | 596,746.5568           | 17,811.3782      |
| 2011 | 9     | 603,083.4976          | 614,557.935            | -11,474.4374     |
| 2011 | 10    | 708,208.0032          | 603,083.4976           | 105,124.5056     |
| 2011 | 11    | 660,545.8132          | 708,208.0032           | -47,662.19       |
| 2011 | 12    | 669,431.5031          | 660,545.8132           | 8,885.6899       |
| 2012 | 1     | 495,364.1261          | 669,431.5031           | -174,067.377     |
| 2012 | 2     | 506,994.1876          | 495,364.1261           | 11,630.0615      |
| 2012 | 3     | 373,483.0054          | 506,994.1876           | -133,511.1822    |
| 2012 | 4     | 400,335.6145          | 373,483.0054           | 26,852.6091      |
| 2012 | 5     | 358,877.8907          | 400,335.6145           | -41,457.7238     |
| 2012 | 6     | 555,160.1428          | 358,877.8907           | 196,282.2521     |
| 2012 | 7     | 444,558.2281          | 555,160.1428           | -110,601.9147    |
| 2012 | 8     | 523,917.3815          | 444,558.2281           | 79,359.1534      |
| 2012 | 9     | 486,177.4502          | 523,917.3815           | -37,739.9313     |
| 2012 | 10    | 535,159.4846          | 486,177.4502           | 48,982.0344      |
| 2012 | 11    | 537,955.517           | 535,159.4846           | 2,796.0324       |
| 2012 | 12    | 624,502.1667          | 537,955.517            | 86,546.6497      |
| 2013 | 1     | 857,689.91            | 624,502.1667           | 233,187.7433     |
| 2013 | 2     | 771,348.74            | 857,689.91             | -86,341.17       |
| 2013 | 3     | 1,049,907.39          | 771,348.74             | 278,558.65       |
| 2013 | 4     | 1,046,022.77          | 1,049,907.39           | -3,884.62        |
| 2013 | 5     | 1,284,592.93          | 1,046,022.77           | 238,570.16       |
| 2013 | 6    



### Month To Month comparison
```sql
SELECT 
    YEAR(OrderDate) AS OrderYear,
    MONTH(OrderDate) AS OrderMonth,
    AVG(SalesAmount) AS AverageSalesAmount,
    LAG(AVG(SalesAmount)) OVER(ORDER BY YEAR(OrderDate), MONTH(OrderDate)) AS PreviousMonthAverageSaleAmount,
    LEAD(AVG(SalesAmount)) OVER(ORDER BY YEAR(OrderDate), MONTH(OrderDate)) AS NextMonthAverageSaleAmount,
    CASE 
        WHEN AVG(SalesAmount) < LAG(AVG(SalesAmount)) OVER(ORDER BY YEAR(OrderDate), MONTH(OrderDate)) THEN 'Decreased'
        WHEN AVG(SalesAmount) > LEAD(AVG(SalesAmount)) OVER(ORDER BY YEAR(OrderDate), MONTH(OrderDate)) THEN 'Increased'
        ELSE 'Stable'
    END AS SalesTrend
FROM 
    FactInternetSales
GROUP BY
    YEAR(OrderDate),
    MONTH(OrderDate);
```
*Results*
| OrderYear | OrderMonth| AverageSalesAmount | PreviousMonthAverage| NextMonthAverage| SalesTrend    |
|------|-------|----------------|---------------|------------|----------|
| 2010 | 12    | 3101.5026      | NULL          | 3262.666   | Stable   |
| 2011 | 1     | 3262.666       | 3101.5026     | 3238.4368  | Increased|
| 2011 | 2     | 3238.4368      | 3262.666      | 3234.6577  | Decreased|
| 2011 | 3     | 3234.6577      | 3238.4368     | 3197.9225  | Decreased|
| 2011 | 4     | 3197.9225      | 3234.6577     | 3228.0544  | Decreased|
| 2011 | 5     | 3228.0544      | 3197.9225     | 3207.9992  | Increased|
| 2011 | 6     | 3207.9992      | 3228.0544     | 3174.1838  | Decreased|
| 2011 | 7     | 3174.1838      | 3207.9992     | 3184.238   | Decreased|
| 2011 | 8     | 3184.238       | 3174.1838     | 3259.9107  | Stable   |
| 2011 | 9     | 3259.9107      | 3184.238      | 3204.5611  | Increased|
| 2011 | 10    | 3204.5611      | 3259.9107     | 3175.701   | Decreased|
| 2011 | 11    | 3175.701       | 3204.5611     | 3015.4572  | Decreased|
| 2011 | 12    | 3015.4572      | 3175.701      | 1965.7306  | Decreased|
| 2012 | 1     | 1965.7306      | 3015.4572     | 1949.9776  | Decreased|
| 2012 | 2     | 1949.9776      | 1965.7306     | 1761.7122  | Decreased|
| 2012 | 3     | 1761.7122      | 1949.9776     | 1828.0165  | Decreased|
| 2012 | 4     | 1828.0165      | 1761.7122     | 1733.7096  | Increased|
| 2012 | 5     | 1733.7096      | 1828.0165     | 1745.7866  | Decreased|
| 2012 | 6     | 1745.7866      | 1733.7096     | 1807.1472  | Stable   |
| 2012 | 7     | 1807.1472      | 1745.7866     | 1782.0319  | Increased|
| 2012 | 8     | 1782.0319      | 1807.1472     | 1807.3511  | Decreased|
| 2012 | 9     | 1807.3511      | 1782.0319     | 1709.7747  | Increased|
| 2012 | 10    | 1709.7747      | 1807.3511     | 1660.3565  | Decreased|
| 2012 | 11    | 1660.3565      | 1709.7747     | 1292.9651  | Decreased|
| 2012 | 12    | 1292.9651      | 1660.3565     | 516.0589   | Decreased|
| 2013 | 1     | 516.0589       | 1292.9651     | 223.385    | Decreased|
| 2013 | 2     | 223.385        | 516.0589      | 256.8895   | Decreased|
| 2013 | 3     | 256.8895       | 223.385       | 262.8858   | Stable   |
| 2013 | 4     | 262.8858       | 256.8895      | 292.0193   | Stable   |
| 2013 | 5     | 292.0193       | 262.8858      | 327.0005   | Stable   |
| 2013 | 6     | 




### Running Totals
```sql
WITH RunningTotals AS (
    SELECT 
        st.SalesTerritoryRegion AS SalesTerritory,
        YEAR(sales.OrderDate) AS Year,
        SUM(sales.SalesAmount) AS TotalSalesRevenue,
        ROW_NUMBER() OVER(PARTITION BY st.SalesTerritoryRegion ORDER BY YEAR(sales.OrderDate)) AS RowNum
    FROM 
        FactInternetSales sales
    JOIN 
        DimSalesTerritory st ON sales.SalesTerritoryKey = st.SalesTerritoryKey
    GROUP BY 
        st.SalesTerritoryRegion, YEAR(sales.OrderDate)
)
SELECT 
    SalesTerritory,
    Year,
    TotalSalesRevenue,
    SUM(TotalSalesRevenue) OVER(PARTITION BY SalesTerritory ORDER BY Year ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) AS RunningTotal
FROM 
    RunningTotals
ORDER BY 
    SalesTerritory, Year;
```
*Results*
| SalesTerritory    | Year | SalesRevenue    | RunningTotal |
|----------------|------|------------------|----------------------|
| Australia      | 2010 | 20,909.78        | 20,909.78            |
| Australia      | 2011 | 2,563,732.2493   | 2,584,642.0293       |
| Australia      | 2012 | 2,128,407.4551   | 4,713,049.4844       |
| Australia      | 2013 | 4,339,443.38     | 9,052,492.8644       |
| Australia      | 2014 | 8,507.72         | 9,061,000.5844       |
| Canada         | 2010 | 3,578.27         | 3,578.27             |
| Canada         | 2011 | 571,571.7984     | 575,150.0684         |
| Canada         | 2012 | 307,604.5237     | 882,754.5921         |
| Canada         | 2013 | 1,085,632.65     | 1,968,387.2421       |
| Canada         | 2014 | 9,457.62         | 1,977,844.8621       |
| Central        | 2012 | 2,071.4196       | 2,071.4196           |
| Central        | 2013 | 929.41           | 3,000.8296           |
| France         | 2010 | 3,399.99         | 3,399.99             |
| France         | 2011 | 410,845.326      | 414,245.316          |
| France         | 2012 | 648,065.5383     | 1,062,310.8543       |
| France         | 2013 | 1,578,511.80     | 2,640,822.6543       |
| France         | 2014 | 3,195.06         | 2,644,017.7143       |
| Germany        | 2011 | 520,500.1642     | 520,500.1642         |
| Germany        | 2012 | 608,657.984      | 1,129,158.1482       |
| Germany        | 2013 | 1,761,876.36     | 2,891,034.5082       |
| Germany        | 2014 | 3,277.83         | 2,894,312.3382       |
| Northeast      | 2012 | 2,049.0982       | 2,049.0982           |
| Northeast      | 2013 | 4,483.37         | 6,532.4682           |
| Northwest      | 2010 | 3,399.99         | 3,399.99             |
| Northwest      | 2011 | 927,056.7613     | 930,456.7513         |
| Northwest      | 2012 | 619,068.4799     | 1,549,525.2312       |
| Northwest      | 2013 | 2,091,249.51     | 3,640,774.7412       |
| Northwest      | 2014 | 9,091.81         | 3,649,866.5512       |
| Southeast      | 2012 | 3,637.3996       | 3,637.3996           |
| Southeast      | 2013 | 8,526.47         | 12,163.8696          |
| Southeast      | 2014 | 74.98            | 12,238.8496          |
| Southwest      | 2010 | 11,433.9082      | 11,433.9082          |
| Southwest      | 2011 | 1,531,228.4113   | 1,542,662.3195       |
| Southwest      | 2012 | 810,222.3327     | 2,352,884.6522       |
| Southwest      | 2013 | 3,356,890.10     | 5,709,774.7522       |
| Southwest      | 2014 | 8,376.06         | 5,718,150.8122       |
| United Kingdom | 2010 | 699.0982         | 699.0982             |
| United Kingdom | 2011 | 550,591.2186     | 551,290.3168         |
| United Kingdom | 2012 | 712,700.9641     | 1,263,991.2809       |
| United Kingdom | 2013 |



### How does sales revenue vary across different sales territories?
```sql
    SELECT 
        st.SalesTerritoryRegion AS SalesTerritory,
        SUM(sales.SalesAmount) AS TotalSalesRevenue
    FROM 
        FactInternetSales sales
    JOIN 
        DimSalesTerritory st ON sales.SalesTerritoryKey = st.SalesTerritoryKey
    GROUP BY 
        st.SalesTerritoryRegion
    ORDER BY 
        TotalSalesRevenue DESC;
```
*Results*
| Country         | Revenue        |
|-----------------|----------------|
| Australia       | 9061000.5844   |
| Southwest       | 5718150.8122   |
| Northwest       | 3649866.5512   |
| United Kingdom  | 3391712.2109   |
| Germany         | 2894312.3382   |
| France          | 2644017.7143   |
| Canada          | 1977844.8621   |
| Southeast       | 12238.8496     |
| Northeast       | 6532.4682      |
| Central         | 3000.8296      |



### Transactions breakdown
```sql
SELECT 
      dc.CurrencyName,
      SUM(fis.SalesAmount) AS TotalSalesAmount,
      (SUM(fis.SalesAmount) / (SELECT SUM(SalesAmount) FROM FactInternetSales)) * 100 AS PercentageOfTotal
  FROM 
      FactInternetSales fis
  JOIN 
      DimCurrency dc ON fis.CurrencyKey = dc.CurrencyKey
  GROUP BY 
      dc.CurrencyName, fis.CurrencyKey
  ORDER BY 
      TotalSalesAmount DESC;
```

*Results*
| Currency             | TotalSalesAmount| PercentageOfTotal |
|----------------------|-----------------|-------------------|
| US Dollar            | 14693465.3186  | 50.04              |
| Australian Dollar    | 9051988.0844   | 30.83              |
| United Kingdom Pound | 3388349.6909   | 11.54              |
| Canadian Dollar      | 1806517.4446   | 6.15               |
| Deutsche Mark        | 237784.9902    | 0.80               |
| French Franc         | 180571.692     | 0.61               |



======================================================================================

# `Customer Analysis`

======================================================================================

### OVERVIEW On CUSTOMERS
```sql
SELECT
    CASE
        WHEN DATEDIFF(YEAR, dm.BirthDate, '2014-01-01') BETWEEN 0 AND 19 THEN 'Teenager'
        WHEN DATEDIFF(YEAR, dm.BirthDate, '2014-01-01') BETWEEN 20 AND 35 THEN 'Adult'
        WHEN DATEDIFF(YEAR, dm.BirthDate, '2014-01-01') BETWEEN 35 AND 50 THEN 'Middle Age'
        ELSE 'Senior'
    END AS AgeSegment,
    COUNT(DISTINCT a.CustomerKey) AS CustomerCount,
    SUM(CASE WHEN dm.Gender = 'M' THEN 1 ELSE 0 END) AS MaleCount,
    SUM(CASE WHEN dm.Gender = 'F' THEN 1 ELSE 0 END) AS FemaleCount,
    AVG(dm.YearlyIncome) AS AverageIncome,
    ROUND(AVG(CAST(dm.TotalChildren AS FLOAT)), 2) AS AverageChildren
FROM
    FactInternetSales a
JOIN
    DimCustomer dm ON dm.CustomerKey = a.CustomerKey
GROUP BY
    CASE
        WHEN DATEDIFF(YEAR, dm.BirthDate, '2014-01-01') BETWEEN 0 AND 19 THEN 'Teenager'
        WHEN DATEDIFF(YEAR, dm.BirthDate, '2014-01-01') BETWEEN 20 AND 35 THEN 'Adult'
        WHEN DATEDIFF(YEAR, dm.BirthDate, '2014-01-01') BETWEEN 35 AND 50 THEN 'Middle Age'
        ELSE 'Senior'
    END;
```
*Results*
| Age Group  | CustomerCount    | MaleCount    | FemaleCount         | AverageIncome       | AverageChildren  |
|------------|------------------|--------------|---------------------|---------------------|------------------|
| Senior     | 5,586            | 9,208        | 8,827               | 65,491.5442         | 2.77             |
| Middle Age | 8,510            | 14,077       | 14,228              | 62,241.3001         | 1.83             |
| Adult      | 4,388            | 7,096        | 6,962               | 47,217.9541         | 0.71             |



### How Customers are spread 
```sql
  SELECT 
      dg.EnglishCountryRegionName,
      COUNT(*) AS TotalCustomers,
      ROUND((COUNT(*) * 100.0) / (SELECT COUNT(*) FROM DimCustomer), 1) AS PercentageOfTotal
  FROM 
      DimCustomer dc
  JOIN 
      DimGeography dg ON dc.GeographyKey = dg.GeographyKey
  GROUP BY 
      dg.EnglishCountryRegionName
  ORDER BY 
      TotalCustomers DESC;
````
*Results*
| Country         | TotalCustmers         |        PercentageOfTotal               
|-----------------|-----------------------|---------------------------------|
| United States   | 7,819                 | 42.30                           |
| Australia       | 3,591                 | 19.40                           |
| United Kingdom  | 1,913                 | 10.30                           |
| France          | 1,810                 | 9.80                            |
| Germany         | 1,780                 | 9.60                            |
| Canada          | 1,571                 | 8.50                            |


### How many customers had puchased more than 95 percentile of all customers?
``` sql
WITH CustomerSales AS (
    SELECT
        c.CustomerKey,
        SUM(s.SalesAmount) AS TotalPurchaseAmount
    FROM
        FactInternetSales s
    JOIN
        DimCustomer c ON s.CustomerKey = c.CustomerKey
    GROUP BY
        c.CustomerKey
),
Percentile AS (
    SELECT TOP 1
        PERCENTILE_CONT(0.95) WITHIN GROUP (ORDER BY TotalPurchaseAmount) OVER () AS NinetyFifthPercentileAmount
    FROM
        CustomerSales
),
FinalResult AS (
    SELECT
        COUNT(*) AS TotalCustomers
    FROM
        CustomerSales cs
    JOIN
        Percentile p ON cs.TotalPurchaseAmount > p.NinetyFifthPercentileAmount
)
SELECT TotalCustomers
FROM FinalResult;
```


*Results*
|    | TotalCustomers |
|----|----------------|
|    |      915       |



### Customers that purchase amount is more than 95 percentile?
```sql
    WITH CustomerSales AS (
        SELECT
            c.CustomerKey,
            c.FirstName,
            c.LastName,
            SUM(s.SalesAmount) AS TotalPurchaseAmount
        FROM
            FactInternetSales s
        JOIN
            DimCustomer c ON s.CustomerKey = c.CustomerKey
        GROUP BY
            c.CustomerKey, c.FirstName, c.LastName
    ),
    Percentile AS (
        SELECT top 1
            PERCENTILE_CONT(0.95) WITHIN GROUP (ORDER BY TotalPurchaseAmount) OVER () AS NinetyFifthPercentileAmount
        FROM
            CustomerSales
    )
    SELECT TOP 10
        
        cs.CustomerKey,
        cs.FirstName,
        cs.LastName,
        SUM(cs.TotalPurchaseAmount) AS TotalPurchaseAmount
    FROM
        CustomerSales cs
    JOIN
        Percentile p ON cs.TotalPurchaseAmount > p.NinetyFifthPercentileAmount
    GROUP BY
        cs.CustomerKey, cs.FirstName, cs.LastName
    ORDER BY
        TotalPurchaseAmount DESC;
```

*Results*
| ID    | First Name | Last Name  | Amount    |
|-------|------------|------------|-----------|
| 12301 | Nichole    | Nara       | 13295.38  |
| 12132 | Kaitlyn    | Henderson  | 13294.27  |
| 12308 | Margaret   | He         | 13269.27  |
| 12131 | Randall    | Dominguez  | 13265.99  |
| 12300 | Adriana    | Gonzalez   | 13242.70  |
| 12321 | Rosa       | Hu         | 13215.65  |
| 12124 | Brandi     | Gill       | 13195.64  |
| 12307 | Brad       | She        | 13173.19  |
| 12296 | Francisco  | Sara       | 13164.64  |
| 11433 | Maurice    | Shan       | 12909.6682|





### what cities are more valuable? having at least 10 customers with yearly income more than 50percentile
```sql
  SELECT TOP 10
      dst.SalesTerritoryRegion,
      dg.CountryRegionCode,
      dg.City,
      COUNT(dc.CustomerKey) AS CustomerCount,
      AVG(dc.YearlyIncome) AS AverageYearlyIncome
  FROM
      DimCustomer dc
  JOIN
      DimGeography dg ON dc.GeographyKey = dg.GeographyKey
  JOIN
      DimSalesTerritory dst ON dg.SalesTerritoryKey = dst.SalesTerritoryKey
  GROUP BY
      dst.SalesTerritoryRegion,
      dg.CountryRegionCode,
      dg.City
  HAVING
      AVG(dc.YearlyIncome) > (SELECT AVG(YearlyIncome) FROM DimCustomer)
      AND COUNT(dc.CustomerKey) > 10
  ORDER BY
      AverageYearlyIncome DESC;
```

*Results*
| Region         | Country         | City          | Quantity | Amount      |
|----------------|-----------------|---------------|----------|-------------|
| Southwest      | US              | Torrance      | 100      | 77000.00    |
| Southwest      | US              | Santa Cruz    | 92       | 75217.3913  |
| Southwest      | US              | San Gabriel   | 96       | 73750.00    |
| Southwest      | US              | Spring Valley | 91       | 72747.2527  |
| Southwest      | US              | Palo Alto     | 91       | 71978.0219  |
| Southwest      | US              | Santa Monica  | 91       | 71978.0219  |
| Southwest      | US              | San Diego     | 91       | 71758.2417  |
| Australia      | AU              | Darlinghurst  | 80       | 71125.00    |
| United Kingdom | GB              | Wokingham     | 30       | 70666.6666  |
| Southwest      | US              | Woodland Hills| 96       | 70416.6666  |





====================================================================================
# `PRODUCT ANALYSIS`
====================================================================================

### What is the total sales revenue for each product category?
```sql
    SELECT
        pc.EnglishProductCategoryName AS ProductCategory,
        SUM(sales.SalesAmount) AS TotalSalesRevenue
    FROM 
        FactInternetSales sales
    JOIN 
        DimProduct prod ON sales.ProductKey = prod.ProductKey
    JOIN 
        DimProductSubcategory sub ON prod.ProductSubcategoryKey = sub.ProductSubcategoryKey
    JOIN 
        DimProductCategory pc ON sub.ProductCategoryKey = pc.ProductCategoryKey
    GROUP BY 
        pc.EnglishProductCategoryName;

```
*Results*
| Product Category | Total Sales Revenue |
|------------------|---------------------|
| Accessories      | 700759.96           |
| Bikes            | 28318144.65         |
| Clothing         | 339772.61           |




### What is the total sales revenue for each product subcategory?


```sql
   SELECT 
        sub.EnglishProductSubcategoryName AS ProductSubcategory,
        SUM(sales.SalesAmount) AS TotalSalesRevenue
    FROM 
        FactInternetSales sales
    JOIN 
        DimProduct prod ON sales.ProductKey = prod.ProductKey
    JOIN 
        DimProductSubcategory sub ON prod.ProductSubcategoryKey = sub.ProductSubcategoryKey
    GROUP BY 
        sub.EnglishProductSubcategoryName
    ORDER BY 
        TotalSalesRevenue DESC;
```

*Results*
| Product Category    | Total Sales Revenue |
|---------------------|---------------------|
| Road Bikes          | 14520584.03         |
| Mountain Bikes      | 9952759.56          |
| Touring Bikes       | 3844801.05          |
| Tires and Tubes     | 245529.32           |
| Helmets             | 225335.60           |
| Jerseys             | 172950.68           |
| Shorts              | 71319.81            |
| Bottles and Cages   | 56798.19            |
| Fenders             | 46619.58            |
| Hydration Packs     | 40307.67            |
| Bike Stands         | 39591.00            |
| Bike Racks          | 39360.00            |
| Vests               | 35687.00            |
| Gloves              | 35020.70            |
| Caps                | 19688.10            |
| Cleaners            | 7218.60             |
| Socks               | 5106.32             |


### What are the top-selling products by revenue?

```sql
  SELECT TOP 10
      p.ProductKey,
      p.EnglishProductName AS ProductName,
      SUM(s.SalesAmount) AS TotalRevenue
  FROM 
      FactInternetSales s
  JOIN 
      DimProduct p ON s.ProductKey = p.ProductKey
  GROUP BY 
      p.ProductKey, p.EnglishProductName
  ORDER BY 
      TotalRevenue DESC;
```

*Results*
| ID   | Product                        | Sales      |
|------|--------------------------------|------------|
| 312  | Road-150 Red, 48               | 1205876.99 |
| 310  | Road-150 Red, 62               | 1202298.72 |
| 313  | Road-150 Red, 52               | 1080637.54 |
| 314  | Road-150 Red, 56               | 1055589.65 |
| 311  | Road-150 Red, 44               | 1005493.87 |
| 361  | Mountain-200 Black, 42         | 979960.73  |
| 353  | Mountain-200 Silver, 38        | 979035.78  |
| 363  | Mountain-200 Black, 46         | 961600.81  |
| 359  | Mountain-200 Black, 38         | 954715.84  |
| 357  | Mountain-200 Silver, 46        | 930315.99  |





====================================================================================
# `Reseller Analysis`
====================================================================================


### how resellers are spread in the world
```sql
SELECT 
    dg.EnglishCountryRegionName AS Country,
    COUNT(dr.ResellerKey) AS NumberOfResellers
FROM 
    DimReseller dr
JOIN 
    DimGeography dg ON dr.GeographyKey = dg.GeographyKey
GROUP BY 
    dg.EnglishCountryRegionName;
```
*Results*
| Country         |  NumberOfResellers  |
|-----------------|---------------------|
| Australia       | 40                  |
| Canada          | 114                 |
| France          | 40                  |
| Germany         | 40                  |
| United Kingdom  | 40                  |
| United States   | 427                 |


### Ressellers Order count based on year
```sql
  SELECT 
      YEAR(fs.OrderDate) AS Year,
      count(fs.SalesOrderNumber) AS Orders
  FROM 
      FactResellerSales fs
  JOIN 
      DimReseller dr ON fs.ResellerKey = dr.ResellerKey
  GROUP BY 
      YEAR(fs.OrderDate)
  ORDER BY 
      totalnumberofsales desc;
```
*Results*
| Year |     Orders       |
|------|------------------|
| 2013 | 28,540           |
| 2012 | 22,133           |
| 2011 | 9,830            |
| 2010 | 352              |



### which resseler had the total sales total order count and sales per order 

```sql
  SELECT TOP 10
      dr.ResellerKey,
      dr.ResellerName,
      SUM(fs.SalesAmount) AS TotalSales,
      COUNT(fs.SalesOrderNumber) AS TotalOrders,
      SUM(fs.SalesAmount) / COUNT(fs.SalesOrderNumber) AS SalesPerOrder
  FROM 
      FactResellerSales fs
  JOIN 
      DimReseller dr ON fs.ResellerKey = dr.ResellerKey
  WHERE 
      YEAR(fs.OrderDate) BETWEEN 2011 AND 2013
  GROUP BY 
      dr.ResellerKey, dr.ResellerName
  ORDER BY 
      TotalSales DESC;
```

*Results*
| ID   | ResellerName                         | TotalSales          | TotalOrders             | SalesPerOrder               |
|------|--------------------------------------|---------------------|-------------------------|-----------------------------|
| 697  | Brakes and Gears                     | 877,107.1923        | 298                     | 2,943.3127                  |
| 170  | Excellent Riding Supplies            | 853,849.1795        | 366                     | 2,332.9212                  |
| 678  | Vigorous Exercise Company            | 841,908.7708        | 530                     | 1,588.5071                  |
| 328  | Totes & Baskets Company              | 816,755.5763        | 436                     | 1,873.2926                  |
| 155  | Corner Bicycle Supply                | 787,773.0436        | 429                     | 1,836.3008                  |
| 514  | Retail Mall                          | 763,333.7391        | 422                     | 1,808.8477                  |
| 72   | Outdoor Equipment Store              | 746,317.5293        | 332                     | 2,247.9443                  |
| 433  | Thorough Parts and Repair Services   | 740,985.8338        | 358                     | 2,069.7928                  |
| 146  | Latest Sports Equipment              | 709,946.8654        | 322                     | 2,204.8039                  |
| 670  | First Bike Store                    | 706,148.4522        | 303                     | 2,330.5229                  |



### what product had been sold the most by resellers through past years
```sql
  SELECT 
      dp.ProductKey,
      dp.EnglishProductName AS ProductName,
      sb.EnglishProductSubcategoryName AS SubCategory,
      SUM(fs.SalesAmount) AS TotalSales
  FROM 
      FactResellerSales fs
  JOIN 
      DimProduct dp ON fs.ProductKey = dp.ProductKey
  JOIN
      DimProductSubcategory sb ON dp.ProductSubcategoryKey = sb.ProductSubcategoryKey
  WHERE 
      YEAR(fs.OrderDate) BETWEEN 2011 AND 2013
  GROUP BY 
      dp.ProductKey, dp.EnglishProductName, sb.EnglishProductSubcategoryName
  ORDER BY 
      TotalSales DESC
```
*Results*
| Product Key | ProductName                | Product Subcategory | TotalSales        |
|-------------|----------------------------|---------------------|-------------------|
| 359         | Mountain-200 Black, 38     | Mountain Bikes      | 1,634,647.9374    |
| 358         | Mountain-200 Black, 38     | Mountain Bikes      | 1,471,078.7218    |
| 583         | Road-350-W Yellow, 48      | Road Bikes          | 1,380,253.8772    |
| 576         | Touring-1000 Blue, 60      | Touring Bikes       | 1,370,784.2244    |
| 360         | Mountain-200 Black, 42     | Mountain Bikes      | 1,360,828.0194    |
| 361         | Mountain-200 Black, 42     | Mountain Bikes      | 1,285,524.6491    |
| 580         | Road-350-W Yellow, 40      | Road Bikes          | 1,238,754.6425    |
| 564         | Touring-1000 Yellow, 60    | Touring Bikes       | 1,184,363.3013    |
| 353         | Mountain-200 Silver, 38    | Mountain Bikes      | 1,181,945.8174    |
| 354         | Mountain-200 Silver, 42    | Mountain Bikes      | 1,175,932.5161    |





### What are the top-selling resseler in terms of sales amount in the last six months?
```sql
  SELECT TOP 10
      dr.ResellerKey,
      dr.ResellerName,
      SUM(fs.SalesAmount) AS TotalSalesAmount
  FROM 
      FactResellerSales fs
  JOIN 
      DimReseller dr ON fs.ResellerKey = dr.ResellerKey
  WHERE 
      fs.OrderDate >= DATEADD(MONTH, -6, '2013-12-31') -- Last six months relative to 31 Dec 2013
  GROUP BY 
      dr.ResellerKey, dr.ResellerName
  ORDER BY 
      TotalSalesAmount DESC;
```
*Results*

| ID   | Store Name                       | Total Sales Revenue |
|------|----------------------------------|---------------------|
| 85   | Roadway Bicycle Supply           | 220,496.658         |
| 599  | Westside Plaza                   | 210,647.4929        |
| 433  | Thorough Parts & Repair Services | 187,964.844         |
| 546  | Field Trip Store                 | 186,387.5613        |
| 697  | Brakes and Gears                 | 179,916.2877        |
| 193  | Perfect Toys                     | 175,358.3955        |
| 205  | Rally Master Company Inc         | 172,169.4612        |
| 448  | Action Bicycle Specialists       | 157,700.6035        |
| 230  | Global Bike Retailers            | 156,984.5148        |
| 10   | Rural Cycle Emporium             | 151,824.9944        |





### what employees had the best perfomance in past years
```sql
SELECT 
    de.EmployeeKey,
    CONCAT(de.FirstName, ' ', de.LastName) AS FullName,
    OrderCount,
    TotalSalesAmount,
    dst.SalesTerritoryCountry,
    CASE
        WHEN DATEDIFF(month, de.HireDate, COALESCE(de.EndDate, '2014-01-01')) <= 24 THEN 'Junior'
        WHEN DATEDIFF(month, de.HireDate, COALESCE(de.EndDate, '2014-01-01')) > 24 AND DATEDIFF(month, de.HireDate, COALESCE(de.EndDate, '2014-01-01')) <= 36 THEN 'Mid-Senior'
        ELSE 'Senior'
    END AS EmploymentStatus
FROM 
    DimEmployee de
JOIN 
    (SELECT TOP 10
        EmployeeKey,
        COUNT(*) AS OrderCount,
        SUM(SalesAmount) AS TotalSalesAmount
    FROM 
        FactResellerSales
    GROUP BY 
        EmployeeKey
    ORDER BY 
        OrderCount DESC,
        TotalSalesAmount DESC
    ) AS TopEmployee ON de.EmployeeKey = TopEmployee.EmployeeKey
JOIN 
    DimSalesTerritory dst ON de.SalesTerritoryKey = dst.SalesTerritoryKey;
```

*Results*
| ID   | FullName                      | OrderCount       | TotalSalesAmount    | Country        | EmploymentStatus|
|------|-------------------------------|------------------|---------------------|----------------|-----------------|
| 283  | Jillian Carson                | 7,825            | 10,065,803.5429     | United States  | Senior          |
| 282  | Linda Mitchell                | 7,107            | 10,367,007.4286     | United States  | Senior          |
| 281  | Michael Blythe                | 7,069            | 9,293,903.0055      | United States  | Senior          |
| 291  | Jae Pak                       | 6,738            | 8,503,338.6472      | United Kingdom | Mid-Senior      |
| 285  | Tsvi Reiter                   | 5,417            | 7,171,012.7514      | United States  | Senior          |
| 287  | Shu Ito                       | 4,545            | 6,427,005.5556      | United States  | Senior          |
| 288  | José Saraiva                  | 4,437            | 5,926,418.3574      | Canada         | Senior          |
| 292  | Ranjit Varkey Chudukatil      | 3,419            | 4,509,888.933       | France         | Mid-Senior      |
| 284  | Garrett Vargas                | 3,284            | 3,609,447.2163      | Canada         | Senior          |
| 289  | David Campbell                | 2,247            | 3,729,945.3501      | United States  | Senior          |



### find the ressellers that has sold more than 3 times of the sales avg of all resselers in the year 2013
```sql
  SELECT 
      frs.ResellerKey,
      rs.ResellerName,
      AVG(frs.SalesAmount) AS AverageSalesAmount
  FROM 
      FactResellerSales frs
  JOIN 
      DimReseller rs ON frs.ResellerKey = rs.ResellerKey
  JOIN
      DimDate dd ON frs.OrderDateKey = dd.DateKey
  WHERE
      dd.DateKey >= '20130101' AND dd.DateKey < '20140101'
  GROUP BY 
      frs.ResellerKey, rs.ResellerName   
  HAVING 
      AVG(frs.SalesAmount) > 3 *
      (SELECT AVG(AverageSalesAmount)
      FROM 
      (SELECT AVG(SalesAmount) AS AverageSalesAmount 
          FROM FactResellerSales
          JOIN DimDate dd ON FactResellerSales.OrderDateKey = dd.DateKey
          where dd.DateKey >= '20130101' AND dd.DateKey < '20140101'
          GROUP BY ResellerKey) 
          AS ResellerAverages)
  ORDER BY 
      AverageSalesAmount DESC;
```
*Results*
| ID   |   ResellerName                | AverageSales  |
|------|-------------------------------|---------------|
| 205  | Rally Master Company Inc      | 3,201.1797    |
| 193  | Perfect Toys                  | 3,179.1917    |
| 85   | Roadway Bicycle Supply        | 3,013.2527    |
| 72   | Outdoor Equipment Store       | 2,860.5687    |
| 154  | Camping and Sports Store      | 2,814.3424    |
| 499  | Racing Sales and Service      | 2,726.2211    |
| 97   | Mountain Bike Center          | 2,671.7174    |
| 697  | Brakes and Gears              | 2,666.0217    |



====================================================================================
# `Survey Analysis`
====================================================================================

### the number of distinct customer attended in surveys
```sql
SELECT COUNT(*) AS TotalCustomers
FROM (
    SELECT DISTINCT CustomerKey
    FROM FactSurveyResponse
    GROUP BY CustomerKey
) AS Subquery
```

*Results*
|      | TotalCustomers |
|------|----------------|
| 1    | 1656           |


### Lets check what percentage of customers has completed the surveys in 2012(the only year had survey)
```sql
SELECT 
    COUNT(*) AS TotalCustomersInSurveys,
    (SELECT COUNT(*) FROM DimCustomer) AS TotalCustomersInDimCustomer,
    CONCAT(
        CAST(CAST(COUNT(*) AS DECIMAL(10, 3)) / (SELECT COUNT(*) FROM DimCustomer) * 100 AS DECIMAL(10, 2)),
        '%'
    ) AS Ratio
FROM (
    SELECT DISTINCT CustomerKey
    FROM FactSurveyResponse
    GROUP BY CustomerKey
) AS Subquery;
```
*Results*
| TotalCustomersInSurveys| TotalCustomers    |     Ratio     |
|------------------------|-------------------|---------------|
|           1656         |        18484      |      8.96%    |


### what number and precentage of customers have attended surveys more than 3 times?
```sql
SELECT 
    COUNT(*) AS TotalCustomersInSurveys,
    (SELECT COUNT(*) FROM DimCustomer) AS TotalCustomersInDimCustomer,
    CONCAT(
        CAST(CAST(COUNT(*) AS DECIMAL(10, 3)) / (SELECT COUNT(*) FROM DimCustomer) * 100 AS DECIMAL(10, 2)),
        '%'
    ) AS Ratio
FROM (
    SELECT DISTINCT CustomerKey
    FROM FactSurveyResponse
    GROUP BY CustomerKey
    HAVING COUNT(*) >= 3
) AS Subquery;
```

*Results*
| TotalCustomersInSurveys| TotalCustomers    |     Ratio     |
|------------------------|-------------------|---------------|
|           131          |        18484      |      0.71%    |




### find the customers that had the most survey attendance
```sql
SELECT
    CONCAT(dc.FirstName, ' ', dc.LastName) AS FullName,
    TotalSurveys
FROM (
    SELECT
        CustomerKey,
        COUNT(*) AS TotalSurveys
    FROM
        FactSurveyResponse
    GROUP BY
        CustomerKey
    HAVING
        COUNT(*) >= 3
) AS SurveyCustomers
JOIN DimCustomer dc ON SurveyCustomers.CustomerKey = dc.CustomerKey
ORDER BY
    TotalSurveys DESC;
```

*Results*
| FullName       | Total |
|----------------|-------|
| Colin Chavez   |     5 |
| Meagan Prasad  |     4 |
| Renee Navarro  |     4 |
| Mandy She      |     4 |
| Natalie Nelson |     4 |
| Grace Murphy   |     4 |
| Ariana Stewart |     4 |
| Deanna Raman   |     4 |
| Gina Dominguez |     4 |
| Kristen Li     |     4 |



### campaigne to issue the gift card.. customers had at leats 3 surveys and more than 10 orders 
```sql
SELECT
    FullName,
    MAX(TotalSurveys) AS TotalSurveys,
    MAX(HasSalesInInternet) AS HasSalesInInternet,
    COUNT(*) AS InternetSales
FROM (
    SELECT
        CONCAT(dc.FirstName, ' ', dc.LastName) AS FullName,
        TotalSurveys,
        CASE WHEN fis.CustomerKey IS NOT NULL THEN 'Yes' ELSE 'No' END AS HasSalesInInternet
    FROM (
        SELECT CustomerKey, COUNT(*) AS TotalSurveys
        FROM FactSurveyResponse
        GROUP BY CustomerKey
        HAVING COUNT(*) >= 3
    ) AS SurveyCustomers
    JOIN DimCustomer dc ON SurveyCustomers.CustomerKey = dc.CustomerKey
    LEFT JOIN FactInternetSales fis ON dc.CustomerKey = fis.CustomerKey
) AS Subquery
GROUP BY FullName
HAVING COUNT(*) >= 10
ORDER BY InternetSales DESC;
```
*Results*
| FullName       | TotalSurveys | HasSalesInInternet | InternetSales |
|----------------|--------------|-----------|------------------|
| Jasmine Powell |     3        | Yes       |               36 |
| Arturo Sun     |     3        | Yes       |               30 |
| Carlos Hill    |     3        | Yes       |               13 |
| Jordan Griffin |     3        | Yes       |               12 |
| Noah Smith     |     3        | Yes       |               12 |
| Matthew Thomas |     3        | Yes       |               11 |
| Eugene Huang   |     3        | Yes       |               11 |



### count the number of survey attendance customers has based on their educational background
```sql
SELECT
    dc.EnglishEducation,
    COUNT(DISTINCT fsr.CustomerKey) AS SurveyAttendance,
    CAST((COUNT(DISTINCT fsr.CustomerKey) * 100.0) / (SELECT COUNT(DISTINCT CustomerKey) FROM FactSurveyResponse) AS DECIMAL(18, 2)) AS AttendancePrecentage,
    COUNT(DISTINCT dc2.CustomerKey) AS TotalNumbers,
    CAST(COUNT(DISTINCT dc2.CustomerKey) AS DECIMAL(18, 2)) / CAST((SELECT COUNT(DISTINCT dc2.CustomerKey) FROM DimCustomer dc2) AS DECIMAL(18, 2)) *100 AS TotalRatio
FROM
    FactSurveyResponse fsr
JOIN
    DimCustomer dc ON fsr.CustomerKey = dc.CustomerKey
LEFT JOIN
    DimCustomer dc2 ON dc.EnglishEducation = dc2.EnglishEducation
GROUP BY
    dc.EnglishEducation;
```
*Results*
| English Education     | Survey Attendance | Attendance Percentage | Total Numbers | Total Ratio |
|-----------------------|-------------------|-----------------------|---------------|-------------|
| High School           | 288               | 17.39                 | 3,294         | 17.82       |
| Partial High School   | 152               | 9.18                  | 1,581         | 8.55        |
| Partial College       | 430               | 25.97                 | 5,064         | 27.40       |
| Graduate Degree       | 243               | 14.67                 | 3,189         | 17.25       |
| Bachelors             | 543               | 32.79                 | 5,356         | 28.98       |





====================================================================================
# `Date Analysis`
====================================================================================

### which months had the most sales in previous years(excluding 2014 and 2010 because of short amount of data)
```sql
 WITH MonthlyOrderCounts AS (
      SELECT 
          YEAR(OrderDate) AS Year,
          MONTH(OrderDate) AS Month,
          dm.EnglishMonthName AS MonthName,
          COUNT(*) AS NumberOfOrders,
          ROW_NUMBER() OVER(PARTITION BY YEAR(OrderDate) ORDER BY COUNT(*) DESC) AS RN
      FROM 
          FactInternetSales s
      JOIN DimDate dm ON s.OrderDateKey =  dm.DateKey
      WHERE 
          YEAR(OrderDate) NOT IN (2010, 2014)
      GROUP BY 
          YEAR(OrderDate), MONTH(OrderDate), dm.EnglishMonthName
  )
  SELECT 
      Year,
      Month,
      MonthName,
      NumberOfOrders
  FROM 
      MonthlyOrderCounts
  WHERE 
      RN = 1;
```


*Results*
| Year | Month | Month Name | NumberOfOrder|
|------|-------|------------|--------------|
| 2011 | 6     | June       | 230          |
| 2012 | 12    | December   | 483          |
| 2013 | 12    | December   | 5520         |




### what days of the week had the most orders 
```sql
  WITH DailyOrderCounts AS (
      SELECT 
          YEAR(fs.OrderDate) AS Year,
          dd.EnglishDayNameOfWeek as day,
          COUNT(*) AS NumberOfOrders,
          ROW_NUMBER() OVER(PARTITION BY YEAR(fs.OrderDate) ORDER BY COUNT(*) DESC) AS RN
      FROM 
          FactInternetSales fs
      JOIN 
          DimDate dd ON fs.OrderDateKey = dd.DateKey
      WHERE 
          YEAR(fs.OrderDate) NOT IN (2010, 2014)
      GROUP BY 
          YEAR(fs.OrderDate), dd.EnglishDayNameOfWeek
  )
  SELECT 
      Year,
      day,
      NumberOfOrders
  FROM 
      DailyOrderCounts
  WHERE 
      RN = 1;
```
*Results*
| Year | Day of the Week | OrderCounts  |
|------|-----------------|--------------|
| 2011 | Saturday        | 334          |
| 2012 | Sunday          | 541          |
| 2013 | Tuesday         | 7824         |



====================================================================================
# `Reason Analysis`
====================================================================================

### compare the total orders without reasons to all orders
```sql
SELECT 
    COUNT(distinct fis.SalesOrderNumber) AS OrderWithoutReason,
    (SELECT COUNT(distinct FactInternetSales.SalesOrderNumber) FROM FactInternetSales) AS TotalOrders,
    ROUND(CAST(COUNT(distinct fis.SalesOrderNumber) AS FLOAT) / (SELECT COUNT(distinct FactInternetSales.SalesOrderNumber) FROM FactInternetSales), 3) * 100 AS PERCENTAGE
FROM 
    FactInternetSales fis
LEFT JOIN 
    FactInternetSalesReason fisr ON fis.SalesOrderNumber = fisr.SalesOrderNumber
WHERE 
    fisr.SalesOrderNumber IS NULL;
```
*Results*
| OrderWithoutReason | TotalOrders | PERCENTAGE |
|-----------------|---------|---------|
|    4647 |   27659 |    16.8 |



### what count of orders by subcategory had reasons
```sql
SELECT 
    dps.EnglishProductSubcategoryName,
    COUNT(DISTINCT fisr.SalesOrderNumber) AS OrderCountWithReason
FROM 
    FactInternetSalesReason fisr
INNER JOIN 
    FactInternetSales fis ON fisr.SalesOrderNumber = fis.SalesOrderNumber
JOIN 
    DimProduct dp ON fis.ProductKey = dp.ProductKey
JOIN 
    DimProductSubcategory dps ON dp.ProductSubcategoryKey = dps.ProductSubcategoryKey
GROUP BY 
    dps.EnglishProductSubcategoryName
ORDER BY 
    OrderCountWithReason DESC;
```
*Results*
| ProductSubCategory  | OrderCountWithReason |
|---------------------|-------------|
| Tires and Tubes     |       9650  |
| Helmets             |       5188  |
| Road Bikes          |       5036  |
| Bottles and Cages   |       4768  |
| Mountain Bikes      |       4221  |
| Jerseys             |       3068  |
| Caps                |       2190  |
| Fenders             |       2121  |
| Touring Bikes       |       1540  |
| Gloves              |       1430  |
| Shorts              |        913  |
| Cleaners            |        908  |
| Hydration Packs     |        714  |
| Socks               |        568  |
| Vests               |        461  |
| Bike Racks          |        288  |
| Bike Stands         |        227  |



### count the number of orders by reason
```sql
SELECT 
    frs.SalesReasonName,
    COUNT(distinct fis.SalesOrderNumber) AS OrderCount,
    SUM(fis.SalesAmount) AS SalesAmount,
    AVG(fis.SalesAmount) AS Average
FROM 
    FactInternetSales fis
JOIN 
    FactInternetSalesReason fisr ON fis.SalesOrderNumber = fisr.SalesOrderNumber
JOIN 
    DimSalesReason frs ON fisr.SalesReasonKey = frs.SalesReasonKey
GROUP BY 
    frs.SalesReasonName
ORDER BY 
    OrderCount DESC;
```
*Results*
| SalesReasonName             | OrderCount | SalesAmount    | Average|
|----------------------------|-------|----------------|-------------------|
| Price                      | 17,473| 37,044,489.16  | 247.5855          |
| On Promotion               | 3,515 | 12,260,556.5228| 588.827           |
| Manufacturer               | 1,746 | 6,151,585.73   | 3,132.1719        |
| Quality                    | 1,551 | 5,549,896.77   | 3,578.27          |
| Other                      | 1,395 | 814,566.98     | 74.2202           |
| Review                     | 1,245 | 2,308,802.2616| 932.4726          |
| Television Advertisement   | 722   | 28,057.93      | 37.6111           |


### the number of orders with and without promotion
```sql
  SELECT
      SUM(CASE WHEN PromotionKey = 1 THEN 1 ELSE 0 END) AS OrdersWithoutPromotion,
      SUM(CASE WHEN PromotionKey != 1 THEN 1 ELSE 0 END) AS OrdersWithPromotion
  FROM
      FactInternetSales;
```
*Results*
| OrdersWithoutPromotion | OrdersWithPromotion |
|------------------------|---------------------|
|         58247          |         2151        |

