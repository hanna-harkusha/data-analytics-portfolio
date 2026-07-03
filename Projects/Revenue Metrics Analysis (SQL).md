### SQL Code Description

This SQL code was used to prepare gaming payment data for revenue metrics analysis.

The first query joins paid user data with payment transactions and calculates the first and last payment date for each user. This provides a user-level view of payment activity together with profile attributes such as game name, language, age, and device type.

The second query aggregates revenue by user and payment month, then uses window functions to compare each month’s revenue with the previous paid month. Based on this comparison, the query calculates **Expansion MRR** and **Contraction MRR** only for consecutive payment months.

The final output helps analyze how user revenue changes over time and supports further calculation of product monetization metrics.
---
--- Q1---
SELECT 
    gpu.user_id, 
    gpu.game_name, 
    gpu.language, 
    gpu.has_older_device_model, 
    gpu.age, 
    MIN(gp.payment_date) AS first_date, 
    MAX(gp.payment_date) AS last_date
FROM 
    project.games_paid_users AS gpu
LEFT JOIN 
    project.games_payments AS gp USING (user_id) 
    
GROUP BY 
    gpu.user_id, 
    gpu.game_name, 
    gpu.language, 
    gpu.has_older_device_model, 
    gpu.age;

--- Q2---
with table_2 as(with table_1 as (
    SELECT 
        user_id, 
        game_name,  
        to_char(date_trunc('month', payment_date), 'YYYY-MM-DD') as payment_month, 
        sum(revenue_amount_usd) as revenue, 
        coalesce(LAG(sum(revenue_amount_usd), 1) OVER (PARTITION BY user_id ORDER BY date_trunc('month', payment_date)), 0) as prev_revenue,
        LAG(to_char(date_trunc('month', payment_date), 'YYYY-MM-DD'), 1) OVER (PARTITION BY user_id ORDER BY date_trunc('month', payment_date)) as prev_payment_month
    FROM 
        project.games_payments 
    GROUP BY 
        user_id, game_name, date_trunc('month', payment_date)    )

SELECT
    user_id, 
    game_name, 
    payment_month, 
    prev_payment_month,
    (DATE_PART('year', payment_month::timestamp) * 12 + DATE_PART('month', payment_month::timestamp)) -
       (DATE_PART('year', prev_payment_month::timestamp) * 12 + DATE_PART('month', prev_payment_month::timestamp)) AS month_difference,
    revenue, 
    prev_revenue
FROM 
    table_1 )
    
 SELECT   
    user_id, 
    game_name, 
    payment_month, 
    prev_payment_month,
    month_difference,
    revenue, 
    prev_revenue,
    case
        when revenue > prev_revenue and month_difference = 1
        then revenue - prev_revenue
        else 0
    end AS expansion_mrr,

    case
        when revenue < prev_revenue and month_difference = 1
        then prev_revenue - revenue
        else 0
    end AS contraction_mrr
    
FROM 
    table_2
ORDER BY 
    user_id, payment_month

---

> **SQL skills demonstrated:** joins, CTEs, aggregations, window functions, date functions, revenue metrics calculation
