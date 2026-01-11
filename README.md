/* Supply Chain Risk Audit - Master Script
Author: Rajesh N
*/

-- Step 1: Create the flags using a CTE
WITH audit_base AS (
  '''SELECT 
    *,
    CASE WHEN Days_Actual > Days_Scheduled THEN 1 ELSE 0 END AS is_late,
    CASE WHEN Order_Status = 'SUSPECTED_FRAUD' THEN 1 ELSE 0 END AS is_fraud
  FROM `my-project-0209-483609.Supply_Chain_Audit.audit_raw`
)

-- Step 2: Aggregating Profit and Risk by Region
SELECT 
  Order_Region,
  SUM(Order_Profit_Per_Order) AS total_profit,
  SUM(is_late) AS total_late_orders
FROM audit_base
GROUP BY Order_Region
ORDER BY total_profit DESC;
'''
