# SQL_Project_Music_Store_Analysis
## SQL project to analyze online music store data

### This project is for beginners and will teach you how to analyze the music playlist database. You can examine the dataset with SQL and help the store understand its business growth by answering simple questions.

# Database and Tools
 ### Database - music store database
 ### Database schema
<img width="594" alt="schema_diagram" src="https://user-images.githubusercontent.com/108074039/226102431-30b03b67-09ad-4910-a099-9c011e928099.png">

# DATA ANALYSIS
### Note: 
this project is done in google cloud big query console . According to big query syntax , 
each time the table has to be referred by the project and the dataset name preceding it , followed by a dot notation.
 
 ## Here are some of the important questions to be asked in order to discover some insights from this dataset.
 
 ###  *Question-1*  who is the senior most employee based on job title?

   select concat(first_name," ",last_name)as name_of_senior_most_employee, from `my-portfolio-project-380610.music_dataset.employee` 
   order by levels desc limit 1 
   
   
   
   
   
   
   ###  *Question-2* which countries have the most invoices?

SELECT billing_country as country,count(*) as number_of_invoices
FROM `my-portfolio-project-380610.music_dataset.invoice`
group by billing_country
order by number_of_invoices desc limit 1






#### in the output we can  see that usa has the maximum number of invoices


###  *Question-3*   Which city has the best customers? We would like to throw a promotional Music Festival in the city we made the most money. 
###                 Write a query that returns one city that has the highest sum of invoice totals. 
###                 Return both the city name & sum of all invoice totals .


SELECT billing_city as city ,round(sum(total)) as total_sales 
FROM `my-portfolio-project-380610.music_dataset.invoice` 
group by city 
order by total_sales desc limit 5

#### The output shows  the top five cities in terms of sales , prague being on top.






###  *Question-4*  Who is the best customer? The customer who has spent the most money will be declared the best customer. 
###                Write a query that returns the person who has spent the most money.

#### /* note:For this , we will use the customer table data but it alone does not have sales information along with 
#### the customer information , we will have to join it with the invoice table , for the total sales data , in the 'total'column.*/



SELECT  concat(first_name," ",last_name)as customer_name,round(sum(total),2) as total_money_spent 
FROM `my-portfolio-project-380610.music_dataset.customers` as customers
join  `my-portfolio-project-380610.music_dataset.invoice` as invoice
on customers.customer_id=invoice.customer_id group by customer_name
order by total_money_spent desc 
limit 1 


#### hence , as seen from the output, František Wichterlová is the best customer.






###  *Question-5* Return all the track names that have a song length longer than the average song length. 
###               Return the Name and Milliseconds for each track. Order by the song length with the longest songs listed first. */

SELECT name as name_of_track , milliseconds as track_duration FROM `my-portfolio-project-380610.music_dataset.track`as track 
where milliseconds > (select avg(milliseconds) from `my-portfolio-project-380610.music_dataset.track`)
order by track_duration desc
  
  
  
  
  
  
  
  
  
  
  
  
 ### *Question-6*  Write query to return the email, first name, last name, & Genre of all Rock Music listeners. 
 ###                Return your list ordered alphabetically by email starting with A. 




/*Explaination - we have to pull out customer information from customer table , along with the genre they listen to , from the genre table . 
since we cannot join customer and genre table directly (no common column ), we have to join first
customer table with invoice table with 'customer_id' THEN
invoice table with invoice line table with 'invoice_id' column . Then,
invoice line table with track table with 'track_id' column. Then finally , 
Track table with genre table with 'genre id '.*/




SELECT distinct concat(first_name," ",last_name) as name , email,genre.name as genre  FROM `my-portfolio-project-380610.music_dataset.customers`as customers join
`my-portfolio-project-380610.music_dataset.invoice` as invoice on customers.customer_id = invoice.customer_id
join `my-portfolio-project-380610.music_dataset.invoice_line`as invoice_line on invoice.invoice_id = invoice_line.invoice_id
join `my-portfolio-project-380610.music_dataset.track` as track on invoice_line.track_id = track.track_id
join `my-portfolio-project-380610.music_dataset.genre` as genre on track.genre_id = genre.genre_id
where genre.name='Rock'
order by email












### *Question-7*  Let's invite the artists who have written the most rock music in our dataset. 
###               Write a query that returns the Artist name and total track count of the top 10 rock bands.




/* Explaination - Again , like the previous query , we need data from two tables for this - artist table for artist names and 
genre table for the genre name but we cannot directly join them . If we check the schema diagram ,
 artist and genre table are connected by the album and track table .

 so , this is how we go about it.

 First , we join artist table with album table with 'artist_id' Then , 
 we join album table with the track table with 'album_id'. Then , finally ,
 we join track table with 'genre' table with 'genre_id'.*/






SELECT artist.name as artist_name,count(artist.name) as total_track_count
 FROM `my-portfolio-project-380610.music_dataset.artist`as artist
 join `my-portfolio-project-380610.music_dataset.project_tables` as album on artist.artist_id = album.artist_id
 join `my-portfolio-project-380610.music_dataset.track` as track on album.album_id = track.album_id
 join `my-portfolio-project-380610.music_dataset.genre` as genre on track.genre_id = genre.genre_id
 where genre.name='Rock'
 group by artist_name
 order by 2 desc
 limit 10

 #### now we can see top 10 artists and their total track count in the output.



### Thank you for reading.Let me know any if you have any feedbacks or suggestions. 

### contact me:
### [Linkedin](https://www.linkedin.com/in/ishita-arora-51616b1b3/)| [Instagram](https://www.instagram.com/windy_pooh101/)|[gmail](aroraishita596@gmail.com)


	
