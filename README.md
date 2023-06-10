# thelook_ecommerce EDA

---

## Dataset

Dataset yang digunakan adalah "thelook_ecommerce" yang tersedia di platform [BigQuery](https://console.cloud.google.com/bigquery?project=rock-wonder-317907&ws=!1m4!1m3!3m2!1sbigquery-public-data!2sthelook_ecommerce). Dataset ini terdiri dari beberapa tabel yang saling terhubung, antara lain "inventory_items" dan "order_items". Tabel "inventory_items" berisi informasi tentang produk-produk yang tersedia dalam inventaris toko, seperti ID produk, harga, kategori, nama produk, dan lainnya. Tabel "order_items" berisi detail transaksi, termasuk ID produk, status transaksi, tanggal pengiriman, harga penjualan, dan lainnya.
Berikut adalah deskripsi atribut yang terdapat dalam dataset ini:

## Objective

Tujuan dari menggunakan dataset "thelook_ecommerce" ini adalah untuk melakukan analisis terhadap permasalahan “Shipping and Stock Performance Review on Q1 - Q2 2023”.

## Query Filtering
```sql
SELECT
    a.product_id,
    b.inventory_item_id,
    b.status,
    b.created_at,
    b.shipped_at,
    b.delivered_at,
    b.returned_at,
    b.sale_price,
    a.cost,
    a.product_category,
    a.product_name,
    a.product_retail_price,
    a.product_department,
    a.product_distribution_center_id
FROM
    `bigquery-public-data.thelook_ecommerce.inventory_items` a
INNER JOIN
    `bigquery-public-data.thelook_ecommerce.order_items` b
ON
    a.id = b.inventory_item_id
WHERE
    b.shipped_at BETWEEN '2023-01-01' AND '2023-06-30'
    AND EXTRACT(YEAR FROM b.shipped_at) = 2023
```