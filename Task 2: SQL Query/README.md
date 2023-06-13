##Part A & B
```sql
SELECT brandId, 
	   name, 
       COUNT(DISTINCT CASE WHEN r.dateScanned >= DATE_SUB(CURDATE(), INTERVAL 1 MONTH) THEN r.receiptId END) AS recent_month_receipts_scanned,
       RANK() OVER(ORDER BY COUNT(DISTINCT CASE WHEN r.dateScanned >= DATE_SUB(CURDATE(), INTERVAL 1 MONTH) THEN r.receiptId END) DESC) AS recent_month_rnk,
       COUNT(DISTINCT CASE WHEN r.dateScanned >= DATE_SUB(CURDATE(), INTERVAL 2 MONTH) AND r.dateScanned < DATE_SUB(CURDATE(), INTERVAL 1 MONTH) THEN r.receiptId END) AS prev_month_receipts_scanned,
       RANK() OVER(ORDER BY COUNT(DISTINCT CASE WHEN r.dateScanned >= DATE_SUB(CURDATE(), INTERVAL 2 MONTH) AND r.dateScanned < DATE_SUB(CURDATE(), INTERVAL 1 MONTH) THEN r.receiptId END) DESC) AS prev_month_rnk
FROM brands b
INNER JOIN receiptItem ri
  ON b.barcode = ri.barcode
INNER JOIN receipts r
  ON r.receiptId = ri.receiptId
GROUP BY 1, 2
ORDER BY recent_month_rnk
LIMIT 5;
```
