# Query yang paling banyak berjalan saat double PO tanggal 15 maret

---
## 1. Query ini bisa dicek apakah ada yang belum terindex
```
SELECT
  DISTINCT `pod`.`product_id`,
  `po`.`po_id`,
  `po`.`estimate_group_id`,
  `po`.`po_number`,
  `po`.`status_id` as `status_po_id`,
  `pos`.`status_name` as `status_po_name`,
  `po`.`sent_sap`,
  `po`.`notes` as `remarks`
FROM
  `purchase_order` `po`
  JOIN `purchase_order_detail` `pod` ON `po`.`po_id` = `pod`.`po_id`
  JOIN `purchase_order_status` `pos` ON `pos`.`status_id` = `po`.`status_id`
WHERE
  `po`.`estimate_group_id` = '2404672'
```
### Detail
![image](https://github.com/user-attachments/assets/f26ce457-651f-4d7f-b310-6482e9b2438d)




## 2. Query ini bisa dicek apakah ada yang terindex dan perlu penambaha where statment date saat halamannya dibuka
```
SELECT
  ifnull(sum(e.quantity * e.price), 0) as price
FROM
  `estimate_order_detail` `e`
  JOIN `estimate_order` `eo` ON `eo`.`estimate_order_id` = `e`.`estimate_order_id`
  JOIN `product_depo` `pd` ON `pd`.`product_id` = `e`.`product_id`
  and `pd`.`depo_id` = `e`.`depo_id`
WHERE
  `eo`.`estimate_order_group_id` = '2412431'
  AND `pd`.`is_active` = 1
  AND `e`.`product_id` IN(
    '19',
    '24',
    '26',
    '119',
    '121',
    '124',
    '156',
    '223'
  )
```
### Detail
<img width="1143" alt="image" src="https://github.com/user-attachments/assets/6c5933a9-a00b-4841-8f4f-adcbb0ad9b9f" />

## 3. Query ini bisa dicek apakah ada yang terindex 
```
SELECT
  DISTINCT `egb`.`group_brand_id`,
  `egb`.`group_brand_name`
FROM
  `estimate_order_group_brand` `egb`
WHERE
  `egb`.`estimate_order_group_id` = '2400183'
```
### Detail
<img width="1145" alt="image" src="https://github.com/user-attachments/assets/711b3f50-e97d-4814-91a6-842ff3974cb3" />

## 4. Query ini bisa dicek apakah ada yang terindex dan perlu penambaha where statment date saat halamannya dibuka
```
  SELECT
  `d`.`dropping_number`,
  `dd`.`product_id`,
  `dd`.`qty_drop`
FROM
  `dropping` `d`
  JOIN `dropping_detail` `dd` ON `d`.`dropping_id` = `dd`.`dropping_id`
WHERE
  `d`.`dropping_number` = '407090895222062208570733'
  AND `dd`.`product_id` = '120'
  ```

### Detail
<img width="1145" alt="image" src="https://github.com/user-attachments/assets/2aa8e471-90b6-4bad-b6b1-3d864100d6d2" />

