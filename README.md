# SQL_Project_Music_Store_Analysis
## SQL project to analyze online music store data

### This project is for beginners and will teach you how to analyze the music playlist database. You can examine the dataset with SQL and help the store understand its business growth by answering simple questions.

# Database and Tools
 ### Database - music store database
 ### Database schema
<img width="594" alt="schema_diagram" src="https://user-images.githubusercontent.com/108074039/226102431-30b03b67-09ad-4910-a099-9c011e928099.png">

# DATA ANALYSIS
### Note: 
this project is done in google cloud big query console . Accoeding to big query syntax , 
each time the table has to be referred by the project and the dataset name preceding it , followed by a dot notation.
 
 ## Here are some of the important questions to be asked in order to discover some insights from this dataset.
 
 ###* *Question-1*  who is the senior most employee based on job title?

   select concat(first_name," ",last_name)as name_of_senior_most_employee, from `my-portfolio-project-380610.music_dataset.employee` 
   order by levels desc limit 1 


	
