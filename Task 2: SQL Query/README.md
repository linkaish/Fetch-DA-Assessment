## Part A & B
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

## Part C & D
```sql
SELECT AVG(CASE WHEN rewardsReceiptStatus = "Finished" THEN totalSpent END) AS accepted_avg_spend,
	   AVG(CASE WHEN rewardsReceiptStatus = "Rejected" THEN totalSpent END) AS rejected_avg_spend,
       AVG(CASE WHEN rewardsReceiptStatus = "Finished" THEN purchasedItemCount END) AS accepted_item_count,
	   AVG(CASE WHEN rewardsReceiptStatus = "Rejected" THEN purchasedItemCount END) AS rejected_item_count
FROM receipts;
```

## Part E
```sql
SELECT brandId, name
FROM mydb.brands b
INNER JOIN receiptItem ri
	ON b.barcode = ri.barcode
INNER JOIN receipts r
	ON ri.receiptId = r.receiptId
INNER JOIN users u
	ON r.userId = u.userId
WHERE u.createdDate >= DATE_SUB(CURDATE(), INTERVAL 6 MONTH)
GROUP BY 1, 2
ORDER BY SUM(ri.quantityPurchased * ri.finalPrice) DESC
LIMIT 1;
```

## Part F
```sql
SELECT brandId, name
FROM brands b
INNER JOIN receiptItem ri
	ON b.barcode = ri.barcode
INNER JOIN receipts r
	ON ri.receiptId = r.receiptId
INNER JOIN users u
	ON r.userId = u.userId
WHERE u.createdDate >= DATE_SUB(CURDATE(), INTERVAL 6 MONTH)
GROUP BY 1, 2
ORDER BY COUNT(DISTINCT r.receiptId) DESC
LIMIT 1;
```
