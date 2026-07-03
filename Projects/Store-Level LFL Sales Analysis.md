### Store-Level LFL Sales Analysis

This SQL query was used to calculate store-level Like-for-Like (LFL) sales performance for the last completed fiscal month.

The query compares sales from the latest completed fiscal month with sales from the same fiscal month of the previous fiscal year. The calculation is performed at the store level and excludes unrelated product categories to keep the comparison consistent.

The final output shows current year sales, previous year sales, and the LFL percentage change for each store.

#### SQL Query

```sql
WITH LastFiscalMonth AS 
(
    -- Знаходимо останній завершений фіскальний місяць
    SELECT MAX(FiscalMonthKey) AS LastFiscalMonthKey
    FROM [CompanyDW].[dbo].[DimDate]
    WHERE DateID < CAST(GETDATE() AS date)
),
Sale_CY AS 
(
    -- Продажі за останній фіскальний місяць (поточний рік)
    SELECT 
        fs.StoreID,
        d.FiscalMonthKey,
        d.FiscalMonthName,
        SUM(fs.SalesAmountUahNoTax) AS SalesCY
    FROM [CompanyDW].[dbo].[FactSales] fs
    INNER JOIN [CompanyDW].[dbo].[DimDate] d
        ON fs.DateKey = d.DateKey
    INNER JOIN [CompanyDW].[Dimension].[Products_mtz] p
        ON fs.ProductID = p.ProductID
    INNER JOIN [CompanyDW].[dbo].[DimProductsCatPrice] c
        ON p.CatPriceID = c.CatPriceID
    CROSS JOIN LastFiscalMonth l
    WHERE d.FiscalMonthKey = l.LastFiscalMonthKey
      AND c.IsRelatedID = 0
    GROUP BY fs.StoreID, d.FiscalMonthKey, d.FiscalMonthName
),
Sale_PY AS
(
    -- Продажі за той самий фіскальний місяць минулого року
    SELECT 
        fs.StoreID,
        d.FiscalMonthKey,
        d.FiscalMonthName,
        SUM(fs.SalesAmountUahNoTax) AS SalesPY
    FROM [CompanyDW].[dbo].[FactSales] fs
    INNER JOIN [CompanyDW].[dbo].[DimDate] d
        ON fs.DateKey = d.DateKey
    INNER JOIN [CompanyDW].[Dimension].[Products_mtz] p
        ON fs.ProductID = p.ProductID
    INNER JOIN [CompanyDW].[dbo].[DimProductsCatPrice] c
        ON p.CatPriceID = c.CatPriceID
    CROSS JOIN LastFiscalMonth l
    INNER JOIN [CompanyDW].[dbo].[DimDate] d_curr 
        ON d_curr.FiscalMonthKey = l.LastFiscalMonthKey
    WHERE d.FiscalYear = d_curr.FiscalYear - 1
      AND d.FiscalMonth = d_curr.FiscalMonth
      AND c.IsRelatedID = 0
    GROUP BY fs.StoreID, d.FiscalMonthKey, d.FiscalMonthName
)
SELECT
    cy.StoreID,
    cy.FiscalMonthName,
    cy.SalesCY AS LFLПродСум_CY,
    py.SalesPY AS LFLПродСум_PY,
    CASE 
        WHEN py.SalesPY = 0 THEN NULL
        ELSE CAST(cy.SalesCY AS FLOAT) / py.SalesPY - 1
    END AS [LFL %]
FROM Sale_CY cy
LEFT JOIN Sale_PY py
    ON cy.StoreID = py.StoreID
ORDER BY cy.StoreID;
