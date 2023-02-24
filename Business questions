
# 3.1. In relation to the products:
# How many products of these tech categories have been sold (within the time window of the database snapshot)? What percentage does that represent from the overall number of products sold?

create table all_in2
select product_id, product_category_name_english,  product_weight_g, 
case when product_category_name_english ='computers' then 'tech' 
when product_category_name_english = 'computers_accessories' then 'tech'
when product_category_name_english = 'electronics' then 'tech'
when product_category_name_english = 'telephony' then 'tech'
when product_category_name_english = 'audio' then 'tech'
when product_category_name_english = 'tablets_printing_image' then 'tech'
when product_category_name_english = 'small_appliances' then 'tech'
when product_category_name_english = 'home_appliances' then 'tech'
when product_category_name_english = 'home_appliances_2' then 'tech'
when product_category_name_english = 'pc_gamer' then 'tech'
else 'non_tech'
end as tech_or_no
from products
left join product_category_name_translation as j
on products.product_category_name = j.product_category_name;

select * from order_reviews;
select tech_or_no, sum(review_score);


#both gives the same results
select count(order_id), product_category_name_english
from order_items as i
inner join all_in as a
on i.product_id = a.product_id
inner join orders as o
on o.order_id = i.order_id
where tech_or_no = 'tech' and order_status = 'delivered'
group by a.product_category_name_english
order by count(order_id) DESC;


#create table cat_quantity
select count(order_id) as 'Quantity', product_category_name_english as "Category"
from order_items as i
inner join products as p
on i.product_id = p.product_id
inner join product_category_name_translation as pt
on p.product_category_name = pt.product_category_name
where product_category_name_english = 'computers' or product_category_name_english = 'computers_accessories' or product_category_name_english= 'electronics' or product_category_name_english= 'telephony' or  product_category_name_english='audio' or product_category_name_english='tablets_printing_image' 
group by pt.product_category_name_english
order by count(order_id) DESC;

select sum(Quantity) from cat_quantity; # 15789
select count(*) from order_items; #112650


# Are expensive tech products popular? *
#create table popularity
select count(i.order_id),
case when price < 50 then '<50'
when 50 <= price and  price < 500 then '50-399'
when  500<= price and price < 1000 then '400-999'
when price >=1000 then '>1000'
end as 'Price_cat'
from order_items as i
left join all_in2 as t
on i.product_id = t.product_id
where tech_or_no = 'tech'
group by Price_cat;


# What’s the average price of the products being sold?
select avg(price), tech_or_no
from order_items as i
inner join all_in as t
on i.product_id = t.product_id
group by tech_or_no; # tech products average price is from order_items as '106.21626612249038'. non tech ~123.00714504199168


# 3.2. In relation to the sellers:
# How many months of data are included in the magist database?
 select * from orders;
 
 #create table max_min_date
 select min(order_purchase_timestamp) as ear_date, max(order_purchase_timestamp) as lat_date 
 from orders;
 select ((datediff(lat_date,ear_date))/30.4167)
 from max_min_date;  # '25.4137'
 
 #How many sellers are there? How many Tech sellers are there? What percentage of overall sellers are Tech sellers?
 
create table all_seller2
select seller_id,  order_id, price, freight_value, order_item_id, product_category_name_english,product_weight_g,tech_or_no
from order_items as o
left join all_in2
on o.product_id = all_in2.product_id;

#How many sellers are there?
select count(distinct seller_id)
from  all_seller2; # 3095
#How many Tech sellers are there?
select count(distinct seller_id)
from all_seller2
where tech_or_no = 'tech'; # 577
#What percentage of overall sellers are Tech sellers?  ok 15%

#What is the total amount earned by all sellers?
select sum(price) 
from order_items; #'13591643.701720357'

select sum(price)
from all_seller2; #13591643.701720357

#What is the total amount earned by all sellers? 
select sum(price)
from all_seller as a
left join orders as o
on a.order_id = o.order_id
where order_status = 'delivered'; # When I added that products have to be delivered: '13221498.112056851'

#What is the total amount earned by all Tech sellers?
select sum(price)
from all_seller as a
left join orders as o
on a.order_id = o.order_id
where order_status = 'delivered' and tech_or_no = 'tech'; # '1630411.9158651829'

# Can you work out the average monthly income of all sellers?   13221498.112056851 / 25.4137 = 520250.814012
# Can you work out the average monthly income of Tech sellers? 1630411.9158651829 / 25.4137 = 64154.84 
create table tech_prod_price_seller
select * from orders;
create table tech_prod_price_seller1
select sum(price),
case when order_purchase_timestamp like ('2016-09%') then '2016-09-01'
when order_purchase_timestamp like ('2016-10%') then '2016-10-01'
when order_purchase_timestamp like ('2016-11%') then '2016-11-01'
when order_purchase_timestamp like ('2016-12%') then '2016-12-01'
when order_purchase_timestamp like ('2017-01%') then '2017-01-01'
when order_purchase_timestamp like ('2017-02%') then '2017-02-01'
when order_purchase_timestamp like ('2017-03%') then '2017-03-01'
when order_purchase_timestamp like ('2017-04%') then '2017-04-01'
when order_purchase_timestamp like ('2017-05%') then '2017-05-01'
when order_purchase_timestamp like ('2017-06%') then '2017-06-01'
when order_purchase_timestamp like ('2017-07%') then '2017-07-01'
when order_purchase_timestamp like ('2017-08%') then '2017-08-01'
when order_purchase_timestamp like ('2017-09%') then '2017-09-01'
when order_purchase_timestamp like ('2017-10%') then '2017-10-01'
when order_purchase_timestamp like ('2017-11%') then '2017-11-01'
when order_purchase_timestamp like ('2017-12%') then '2017-12-01'
when order_purchase_timestamp like ('2018-01%') then '2018-01-01'
when order_purchase_timestamp like ('2018-02%') then '2018-02-01'
when order_purchase_timestamp like ('2018-03%') then '2018-03-01'
when order_purchase_timestamp like ('2018-04%') then '2018-04-01'
when order_purchase_timestamp like ('2018-05%') then '2018-05-01'
when order_purchase_timestamp like ('2018-06%') then '2018-06-01'
when order_purchase_timestamp like ('2018-07%') then '2018-07-01'
when order_purchase_timestamp like ('2018-08%') then '2018-08-01'
when order_purchase_timestamp like ('2018-09%') then '2018-09-01'
when order_purchase_timestamp like ('2018-10%') then '2018-10-01'
else 'later'
end as 'daten'
from all_seller2 as a
left join orders as o
on a.order_id = o.order_id
where order_status = 'delivered' and tech_or_no = 'tech'
group by daten; # '1630411.9158651829'
 
# 3.3. In relation to the delivery time:
# What’s the average time between the order being placed and the product being delivered?#
 
select datediff(order_delivered_customer_date, order_purchase_timestamp) as 'Delivery Time'
from orders
where order_status = 'delivered';

# What is avg delivery time?
select avg(datediff(order_delivered_customer_date, order_purchase_timestamp)) as 'Average Delivery Time'
from orders
where order_status = 'delivered';

# How many orders are delivered on time vs orders delivered with a delay? estimated date - delivery date

#create table dif_est_del as
select datediff(order_estimated_delivery_date, order_delivered_customer_date) as 'Difference_date_est'
from orders
where order_status ='delivered';

select * from dif_est_del;

  select count('Difference between estimated date and delivery time') as 'Amount of days without dalay',
  case when Difference_date_est > 0 then 'No delay'
  when Difference_date_est = 0 then 'On time'
  when Difference_date_est < 0 then 'Delayed'
  end as 'Order_status'
  from dif_est_del
  group by Order_status;


# Is there any pattern for delayed orders, e.g. big products being delayed more often?
create table dif_est_del_order_id
select datediff(order_estimated_delivery_date, order_delivered_customer_date) as 'Difference between estimated date and delivery time', order_id
from orders
where order_status ='delivered';

