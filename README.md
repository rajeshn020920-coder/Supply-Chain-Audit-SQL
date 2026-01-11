# Supply-Chain-Audit-SQL
audit_queries.sql
  '''SELECT 
  *,
  CASE WHEN Days_Actual > Days_Scheduled THEN 1 ELSE 0 END AS is_late,
  CASE WHEN Order_Status = 'SUSPECTED_FRAUD' THEN 1 ELSE 0 END AS is_fraud
  FROM my-project-0209-483609.Supply_Chain_Audit.audit_raw

  -- Aggregating Profit and Risk by Region
SELECT 
  Order_Region,
  SUM(Order_Profit_Per_Order) AS total_profit,
  SUM(is_late) AS total_late_orders
FROM `your_audit_table`
GROUP BY Order_Region
ORDER BY total_profit DESC;

-- Analyzing Failure Rates by Shipping Class
SELECT 
  Shipping_Mode,
  COUNT(*) AS total_orders,
  SUM(is_late) AS late_count
FROM `your_audit_table`
GROUP BY 1
ORDER BY late_count DESC;
'''
