# NYU-HPC

## NYU langone - Bigpurple

Accessing your account using Mac terminal:
~~~
ssh UserName@bigpurple.nyumc.org
~~~
Then enter your password. 
To avoid entering password each time you want to use your HPC account, generate a ssh key:
~~~
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
~~~
Replace "your_email@example.com" with your actual email address. This email is used as a label for your key, making it easier to identify its purpose later.

