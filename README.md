<h1>PicoCTF 2022 #49 SQL INJECTION (sqlilite)</h1>



<h2>Description</h2>

<img src="https://i.imgur.com/sbbCjaa.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>


What is Sql Injection?
 
SQL injection, also known as SQLI, is a common attack vector that uses malicious SQL code for backend database manipulation to access information that was not intended to be displayed. This information may include any number of items, including sensitive company data, user lists or private customer details.
The impact SQL injection can have on a business is far-reaching. A successful attack may result in the unauthorized viewing of user lists, the deletion of entire tables and, in certain cases, the attacker gaining administrative rights to a database, all of which are highly detrimental to a business.
LET'S BEGIN THE CTF 
The challenge of the CTF is to login in the website and capture the flag.
THis is what greets us when we start
<img src="https://i.imgur.com/vEZnY2h.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

So lets login with a random username and password

<img src="https://i.imgur.com/bMmwYqp.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
 
 
 
It gives a login failed message

<img src="https://i.imgur.com/RaqZCE3.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

We can see that the website is using single quotes “ ‘ “ to denote name and password, this is very useful information. This single quote is a string value.
SQL query: SELECT * FROM users WHERE name='superman' AND password='superman'
The above query also denotes that both the username and password needs to be true for the login to be successful. So now we may use some common sql injection payloads available on internet to see if we can bypass tha ‘AND’ condition and get an unauthorized login to work 

We go to this github

<img src="https://i.imgur.com/y9BfZ0w.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

We will try to use these to crack our challenge

<img src="https://i.imgur.com/IGXFJs9.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Lets use ‘ OR 1=1

<img src="https://i.imgur.com/YmV5XQZ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Didn't seem to do much, but it seems it broke the page as its not showing the login failed message

<img src="https://i.imgur.com/teIGfsR.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

We know that the sqlilite uses two -- ,so lets try use that

<img src="https://i.imgur.com/lCIkZIg.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Voila!

<img src="https://i.imgur.com/pyu64PO.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

But where is the flag, lets see the source code thats “Control+u” on the keyword.

<img src="https://i.imgur.com/SZc2eD7.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

And we have solved it.
Thanks for reading till here, Have a good day.



<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
