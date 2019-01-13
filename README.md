# SQL_project

1/what are the top 5 longest songs that customer buy ?

/* Query 1 - query used for the first insight */
select  i.billingcountry,
max(t.milliseconds) as max_milliseconds
from Track t 
join InvoiceLine il
on t.trackid=il.InvoiceLineid
join Invoice i
on il.invoicelineid=i.invoiceid
join customer c
on i.invoiceid=c.customerid
group by i.billingcountry
order by max(t.milliseconds) des
climit 5;

2/What are the top cities who have most quantity ?

/* Query 2 - query used for the first insight */
select i.billingcountry,
sum(il.quantity)
from Invoice i
join InvoiceLine il
ON i.invoiceid=il.InvoiceLineid 
join Customer c 
ON il.invoicelineid=c.customerid 
group by  i.billingcountry
order by sum(il.quantity) desc
limit 5;

3/How	 many customer for each employee ?

/* Query 3 - query used for the first insight */
select e.firstname, count(c.customerid)
from Customer c 
join  Employee e
on e.employeeid = c.supportrepid 
group by 1
order by 2;

4/In which country  most popular music ?

/* Query 4 - query used for the first insight */
select i.billingcountry , g.name ,count(g.name)
from invoice i
join InvoiceLine il 
on i.invoiceid=il.InvoiceLineid
join track t 
on il.InvoiceLineid=t.Trackid
join Genre g
on t.trackid = g.Genreid
group by i.billingcountry 
order by count(g.name) desc;
