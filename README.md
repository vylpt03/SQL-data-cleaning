# Overview
This is an educational project on data cleaning and preparation using SQL. The original database in CSV format is located in the file club_member_info.csv. Here, I will explore the steps that need to be applied to obtain a cleansed version of the dataset.
## Data Overview
<pre>Select * from club_member_info cmi 
limit 10;</pre>

|full_name|age|martial_status|email|phone|full_address|job_title|membership_date|
|---------|---|--------------|-----|-----|------------|---------|---------------|
|addie lush|40|married|alush0@shutterfly.com|254-389-8708|3226 Eastlawn Pass,Temple,Texas|Assistant Professor|7/31/2013|
|      ROCK CRADICK|46|married|rcradick1@newsvine.com|910-566-2007|4 Harbort Avenue,Fayetteville,North Carolina|Programmer III|5/27/2018|
|Sydel Sharvell|46|divorced|ssharvell2@amazon.co.jp|702-187-8715|4 School Place,Las Vegas,Nevada|Budget/Accounting Analyst I|10/6/2017|
|Constantin de la cruz|35||co3@bloglines.com|402-688-7162|6 Monument Crossing,Omaha,Nebraska|Desktop Support Technician|10/20/2015|
|  Gaylor Redhole|38|married|gredhole4@japanpost.jp|917-394-6001|88 Cherokee Pass,New York City,New York|Legal Assistant|5/29/2019|
|Wanda del mar       |44|single|wkunzel5@slideshare.net|937-467-6942|10864 Buhler Plaza,Hamilton,Ohio|Human Resources Assistant IV|3/24/2015|
|Joann Kenealy|41|married|jkenealy6@bloomberg.com|513-726-9885|733 Hagan Parkway,Cincinnati,Ohio|Accountant IV|4/17/2013|
|   Joete Cudiff|51|divorced|jcudiff7@ycombinator.com|616-617-0965|975 Dwight Plaza,Grand Rapids,Michigan|Research Nurse|11/16/2014|
|mendie alexandrescu|46|single|malexandrescu8@state.gov|504-918-4753|34 Delladonna Terrace,New Orleans,Louisiana|Systems Administrator III|3/12/1921|
| fey kloss|52|married|fkloss9@godaddy.com|808-177-0318|8976 Jackson Park,Honolulu,Hawaii|Chemical Engineer|11/5/2014|
# SQL-data-cleaning

## Create a new table for cleaning

<pre> CREATE TABLE club_member_info (
	full_name VARCHAR(50),
	age INTEGER,
	martial_status VARCHAR(50),
	email VARCHAR(50),
	phone VARCHAR(50),
	full_address VARCHAR(50),
	job_title VARCHAR(50),
	membership_date VARCHAR(50)
);</pre>

## Copy all value from original table
<pre>INSERT INTO club_member_info_cleaned
SELECT* FROM club_member_info;</pre>

## CLean the data
**Some issues with data:**
1. Inconsistent letter case (full_name column).
2. Leading and trailing whitespaces (full_name column).
3. Age out of realistic range (age column).

**Query**  
#### 1. Inconsistent letter case  
The use of uppercase and lowercase letters is not uniform.  
![image](https://github.com/user-attachments/assets/bcc02f74-9897-4e79-ad3b-51a4d7d11690)  
#### 2. Leading and trailing whitespaces
The unnecessary blank spaces that appear before or after the content in a cell.  
![image](https://github.com/user-attachments/assets/ce33c720-7456-4515-ac80-7b12e02205a4)

To fix issues 1 and 2, I combine both UPPER and TRIM in a  UPDATE statement for 'full_name' to upper all the letters and delete the unnecessary blank in a cell.
  <pre>UPDATE club_member_info_cleaned
SET full_name = UPPER(TRIM(full_name));</pre>
![image](https://github.com/user-attachments/assets/f1a910c2-c453-46d9-8cc6-b3bc895c3388)
> Result

#### 3. Age out of realistic range.
That the age mentioned is not believable—it's either too young or too old. I use the query below to check if the age is too young or too old.  

 <pre>SELECT *
FROM club_member_info cmi 
WHERE age < 0 OR age > 120;</pre>  
![image](https://github.com/user-attachments/assets/241494ed-03bb-4731-83f3-1bbeaaa20924)

To fix issue 3, I use below query to delete age data which is bigger than 120.  
<pre>DELETE FROM club_member_info_cleaned
WHERE age > 120;</pre>
