# NYU-HPC

## Login HPC account:
Accessing your account using Mac terminal:
~~~
ssh YourNYUNetID@bigpurple.nyumc.org (NYU Langone HPC)
~~~
~~~
ssh YourNYUNetID@greene.hpc.nyu.edu (NYU Tandon HPC)
~~~
Then enter your password. \
(The setting up process for both HPCs are the same)

## Use SSH Keys for Authentication:
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

## Remote access to HPC using Visual Studio:
First make sure your VPN is connected to the NYU. \
For Greene you need Cisco Any Connect and for Bigpurple you need BIG-IP Edge. \
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

## Writing and submitting a job:
You submit the job with sbatch:
~~~
$ sbatch myscript.s or myscript.sh
~~~
And monitor its progress with:
~~~
$ squeue -u UserName
~~~
Cancel a specific job if you know the ID:
~~~
scancel JOB_ID
~~~
Cancel all your jobs that you have submitted:
~~~
scancel -u YOUR_USERNAME
~~~

## Load an environment (conda/venv):
When you open your notebook (.ipynb) on VScode on top right there is an option which allows you to choose your environment. \
You either create one or use the existing environments. \
If the environmnet you are looking to use is not in the list of search bar follow the following instruction: 
1) Make sure you already installed Python and Anaconda on your system.
2) press F1 and type "Python: Select Interpreter".
3) In the opened window select "Enter interpreter Path...".
4) Paste the sys path to the environment you wish to use.

To install a package within an environment, follow these three steps: 
~~~
module purge
module load condaenvs/new/YourEnvironment
pip install Package
~~~
## Singularity container: 
To install a package within an existing container, do the following: 
(you can check the slurm file for correct paths) 
~~~
module purge
module load singularity/3.7.1  # Depending on the singularity you are using
singularity exec --bind /gpfs/scratch/pa2297:/gpfs/scratch/pa2297
# Alternative : singularity exec --nv --bind /gpfs/scratch/pa2297 /gpfs/scratch/pa2297/Singularity/tf_lu.sif /bin/bash
> /gpfs/scratch/pa2297/Singularity/tf_lu…sif\
> /bin/bash
Apptainer> python -m pip install --user Package
exit
~~~
## Error: 
1. "Pylance has crashed. Would you like to try using a Node.js executable to run the language server?"
 <img width="600" alt="Screenshot 2024-04-10 at 11 10 25 PM" src="https://github.com/parisimaa/NYU-HPC/assets/54392924/119f38fe-0863-495e-a3a7-bd36cf37661a">

If your Pylance and kernel crash constantly when running notebooks check the following. \
In VScode check your "Workspace Environment", you should be able to see all the packages within that environment. If packages are not there, either install or change to another existing environment consisting all necessary packages. \
To shift to another workspace, look for "Python: Select Interpreter " in your search bar and choose envo that has all you need to run code. \
Also check if the packages you are using are compatible with eachother. 

2. "Could not establish connection to "nyu-langone-hpc": Failed to install the VS Code Server" \
To resolve this simply in command pallete look for "Remote-SSH: Kill VS Code Server on Host..." and then try to reconnect again. 

## Move specific directories from home directory to lab space:
~~~
mv ~/.local <location in lab directory>
ln -s <location in lab directory>/.local ~/.local
~~~
You can do for, .local, .conda, and .vscode-server
## Resources:
1. [NYU HPC Greene - Slurm](https://sites.google.com/nyu.edu/nyu-hpc/training-support/general-hpc-topics/slurm-submitting-jobs)
2. [Singularity Tutorial](https://singularity-tutorial.github.io/02-basic-usage/)
3. [Python Environments in VScode](https://code.visualstudio.com/docs/python/environments)
4. [GPU-based Jupyter using Docker](https://cschranz.medium.com/set-up-your-own-gpu-based-jupyterlab-e0d45fcacf43)


## Contact:
Parisima Abdali: Pa2297@nyu.edu


