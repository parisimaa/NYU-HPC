# NYU-HPC

1) Login HPC account:\
Accessing your account using Mac terminal:
~~~
ssh YourNYUNetID@bigpurple.nyumc.org (NYU Langone HPC)
ssh YourNYUNetID@greene.hpc.nyu.edu (NYU Tandon HPC)
~~~
Then enter your password. \
(The setting up process for both HPCs are the same)

2) Use SSH Keys for Authentication:\
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
Now log in to your HPC account. Before appending your public SSH key to the ~/.ssh/authorized_keys file, ensure that the .ssh directory exists and has the correct permissions:
~~~
mkdir -p ~/.ssh
chmod 700 ~/.ssh
~~~
Open the authorized_keys file with a text editor available on the HPC system, such as 'nano' or 'vi':
~~~
vi ~/.ssh/authorized_keys
~~~
Go to the end of the line press i then Enter and paste the public SSH key there and go back by typing :wq \
type the following to check if the key is there:
~~~
cat ~/.ssh/id_rsa.pub
~~~
Check if you can login without password. 

3) Remote access to HPC using Visual Studio:\
Search for "Remote - SSH" and install the extension. \
Create a "New remote".\
Enter SSH UserName@bigpurple.nyumc.org in the search bar. \
Select directory /.ssh/config \
Add the following information in the new window and save it 
~~~
Host nyu-langone-hpc (Optional name)
  HostName bigpurple.nyumc.org
  User NetID
  ForwardAgent yes
  IdentityFile <private key>
~~~

Press "fn + F1" and look for "Remote-SSH: Connect to host..." and choose the config you created earlier. \
In the new window which is connected to the HPC you should be able to access your folders through search bar. 

## Contact:
Parisima Abdali: Pa2297@nyu.edu


