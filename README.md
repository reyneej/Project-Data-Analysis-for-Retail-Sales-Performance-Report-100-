# Project-Data-Analysis-for-Retail-Sales-Performance-Report-100-
Dataset Brief
Dataset yang digunakan berisi transaksi dari tahun 2009 sampai dengan tahun 2012 dengan jumlah raw data sebanyak 5500, termasuk di dalamnya order status yang terbagi menjadi order finished, order returned dan order cancelled

Adapun dataset yang sudah diberikan dan akan digunakan pada project ini berisi data sebagai berikut.
- OrderID
- Order Status
- Customer
- Order Date
- Order Quantity
- Sales
- Discount %
- Discount
- Product Category
- Product Sub-Category
Nama tabel yang akan digunakan pada project ini adalah dqlab_sales_store.

## 1. Overall Performance by Year
Buatlah Query dengan menggunakan SQL untuk mendapatkan total penjualan (sales) dan jumlah order (number_of_order) dari tahun 2009 sampai 2012 (years).

    select YEAR(order_date) years, sum(sales) sales, COUNT(order_id) number_of_order
    from dqlab_sales_store
    WHERE  YEAR(order_date) BETWEEN 2009 AND 2012
        AND order_status = 'Order Finished'
    group by years
    ORDER BY 1 ASC
Output:

<img width="229" height="120" alt="image" src="https://github.com/user-attachments/assets/2993358a-da03-468f-a47a-ca1ee579865f" />

## Overall Performance by Product Sub Category
Buatlah Query dengan menggunakan SQL untuk mendapatkan total penjualan (sales) berdasarkan sub category dari produk (product_sub_category) pada tahun 2011 dan 2012 saja.

    SELECT 
        YEAR(order_date) AS years,
        product_sub_category,
        SUM(sales) AS sales
    FROM 
        dqlab_sales_store
    WHERE 
        YEAR(order_date) BETWEEN 2011 AND 2012
        AND order_status = 'Order Finished'
    GROUP BY 
        YEAR(order_date),
        product_sub_category
    ORDER BY 
        years ASC,
        sales DESC;
Output:

<img width="308" height="496" alt="image" src="https://github.com/user-attachments/assets/b40f61d1-2dc8-41c6-b884-cfe2c914f9c7" />

## 2. Promotion Effectiveness and Efficiency by Years
Efektifitas dan efisiensi dari promosi yang dilakukan akan dianalisa berdasarkan Burn Rate yaitu dengan membandigkan total value promosi yang dikeluarkan terhadap total sales yang diperoleh.
Formula untuk burn rate : (total discount / total sales) * 100

Buatkan Derived Tables untuk menghitung total sales (sales) dan total discount (promotion_value) berdasarkan tahun(years) dan formulasikan persentase burn rate nya (burn_rate_percentage).

    SELECT
        YEAR(order_date) AS years,
        SUM(sales) AS sales,
        SUM(discount_value) AS promotion_value,
        ROUND(SUM(discount_value) / SUM(sales) * 100, 2) AS burn_rate_percentage
    FROM dqlab_sales_store
    WHERE order_status = 'Order Finished'
    GROUP BY YEAR(order_date)
    ORDER BY years;
Output:

<img width="362" height="112" alt="image" src="https://github.com/user-attachments/assets/4c291bfb-0bb0-4e72-a973-a362a3724fa2" />

## Promotion Effectiveness and Efficiency by Product Sub Category

    SELECT
        YEAR(order_date) AS years,
        product_sub_category,
        product_category,
        SUM(sales) AS sales,
        SUM(discount_value) AS promotion_value,
        ROUND(SUM(discount_value) / SUM(sales) * 100, 2) AS burn_rate_percentage
    FROM dqlab_sales_store
    WHERE order_status = 'Order Finished'
    	AND   YEAR(order_date) = 2012
    GROUP BY 
        YEAR(order_date)
    	, 
        product_sub_category, 
        product_category
    ORDER BY 
    	sales DESC;
Output:

<img width="646" height="303" alt="image" src="https://github.com/user-attachments/assets/f7a1cb57-5b67-4fa5-a250-38d7df257b5f" />

## 3. Customers Transactions per Year
DQLab Store ingin mengetahui jumlah customer (number_of_customer) yang bertransaksi setiap tahun dari 2009 sampai 2012 (years).

    SELECT YEAR(order_date) years, count(distinct customer) number_of_customer
    FROM dqlab_sales_store
    WHERE YEAR(order_date)  BETWEEN 2009 AND 2012
    	AND order_status= 'Order Finished'
    GROUP BY YEAR(order_date)
    order by YEAR(order_date) ASC;
Output:

<img width="178" height="109" alt="image" src="https://github.com/user-attachments/assets/eb13a331-e378-4dc8-bb5a-5c1204542806" />



