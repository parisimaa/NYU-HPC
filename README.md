# NYU-HPC

## NYU langone - Bigpurple

Accessing your account using Mac terminal:
~~~
ssh UserName@bigpurple.nyumc.org
~~~
Then enter your password. \
To avoid entering password each time you want to use your HPC account, generate a SSH key:
~~~
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
~~~
Replace "your_email@example.com" with your actual email address. This email is used as a label for your key, making it easier to identify its purpose later.\
Press Enter to Accept the Default File Location. \
Enter a Secure Passphrase (Press Enter to skip this part) \
Display your public SSH key:
~~~
cat ~/.ssh/id_rsa.pub
~~~
Copy it to the clipboard:
~~~
pbcopy < ~/.ssh/id_rsa.pub
~~~


