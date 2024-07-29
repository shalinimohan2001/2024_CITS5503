---
title: 22997214_shalini_labs1_5

---

﻿<div style="display: flex; flex-direction: column; justify-content: center; align-items: center; height: 100vh;">

  <h2>Labs 1-5</h2>
  
  <p>Student ID: 22977214</p>
  <p>Student Name: Shalini Mohan</p>

</div>

# Lab 1

## AWS Account and Log in

### [1] Log into an IAM user account created for you on AWS.

After navigating to the following [link](https://489389878001.signin.aws.amazon.com/console) which will open a login portal for AWS. There will be three fillable data entry sections. The first of which will already be autofilled with the account root user id '489389878001'. Fill in the IAM user name and Password sections with the data received from the user's email. 
![image](https://hackmd.io/_uploads/r1Q8Y0EtC.png)
After the user clicks the 'Sign In' button, AWS verifies the details. The user will be prompted to change the default password into one of their own choice. I have chosen a strong password of 14 alphanumeric and symbolic characters that I have stored in my Password Manager. 

### [2] Search and open Identity Access Management

This will take you to the landing page for AWS, which is pictured below. To open the Identity Access Management (IAM) portal, the user can click the their email with their unique identifiable AWS number dropdown in the top-right hand corner > click Security credentials.
![image](https://hackmd.io/_uploads/S14Xc0VYC.png)

The user will need to scroll down until they see an area of the IAM portal that is headed with Access keys. They can create an access key using the 'Create access key' button. 
![image](https://hackmd.io/_uploads/rkZ_jRVK0.png)

This will take the user into an access key creation wizard, where the user can customise the user for their key. I have chosen to create an access key with the Command Line Interface (CLI) use case as this lab and the following ones will be completed using a Linux CLI.
![image](https://hackmd.io/_uploads/SJyWhANtA.png)

The user will need to note down and save using Amazon's access key best practices their newly created access key and secret access key at the last page of creation. I have saved these in an encrypted private file on my Password Manager. **If this information is lost, the user will need to make a new access key.**
![image](https://hackmd.io/_uploads/S1EL3R4t0.png)

## Set up recent Linux OSes
Since the machine I am using to complete these labs is running a Windows OS, I followed this [guide](https://canonical-ubuntu-wsl.readthedocs-hosted.com/en/latest/guides/install-ubuntu-wsl2) to install a Linux OS. I already had WSL installed on my machine, but for users without WSL installed, they can open up Command Prompt and type `wsl --install`
![image](https://hackmd.io/_uploads/S1mHTCNK0.png)

However, I did not have Ubuntu 20.04 installed as the lab has asked for, so I had to install it onto my WSL using `wsl --install -d Ubuntu-20.04`. 
- `--install`: flag for wsl to install the following command.
- `-d`: is a flag for wsl to select the Linux distrubution e.g., Ubuntu-20.04

![image](https://hackmd.io/_uploads/B1Q400NK0.png)

Once installed the user will be asked to create a login for their Ubuntu (when typing their password, the CLI will record the keyboard without displaying the characters visually for safety). After, the user will be logged into their chosen distribution.

**Before installing any packages to their new Linux distribution, the user should run the following commands to ensure that they are up-to-date with packages that come with the distribution.**
`sudo apt update`
This command updates the list of available packages and their versions stored in the system's package index. 
`sudo apt -y upgrade`
This command downloads new available packages to a user's distribution. 

* `sudo`: allows the command to run with elevated privileges. 
* `apt`: is short for Ubuntu's Advanced Packaging Tool which allows for the installation of new software packages, updating the package list index, upgrades to existing software packages, and upgrading the Ubuntu system.
* `update/upgrade`: Explained above.
* `-y`: flag in the command....

## Install Linux packages

### [1] Install Python 3.8.x
Ubuntu-20.04 distribution will come with Python 3.8.x pre-installed, but the user can check this using `python3 -V`. 
* `python3`: is the version of python installed on Ubuntu-20.04
* `-V`: flag that indicates which version of python is installed.
![image](https://hackmd.io/_uploads/rklQfJBtA.png)
Afterwhich, the user will need to install `pip3` using `sudo apt install -y python3-pip`, which is a tool that will allow them to install and manage python libraries. 

### [2] Install awscli

Using the newly install `pip3`, the user can install the awscli using `sudo apt install awscli`. This process will be long, and may ask the user to type Y/N at a certain point in the installation, the user must choose Y to continue the process. 
![image](https://hackmd.io/_uploads/SkfAf1StA.png)
The end of the installation will look like this:
![image](https://hackmd.io/_uploads/r1w7mkHt0.png)
Then run `pip3 install awscli --upgrade` to ensure that the awscli is on the latest version, as the installed package will be the last stable release, which may not have the features that are required for this lab and the following ones.
![image](https://hackmd.io/_uploads/Bk8OXyHYA.png)

### [3] Configure AWS
The user will need to now connect the AWS access key to the awscli using `aws cofigure`. The user will be prompted one at a time to enter the following information:
* AWS Access Key ID: the user can access this information using their AWS IAM portal, otherwise it will be defaulted to None.
* AWS Secret Access Key: the user will need to have saved this information when they first created their access key, otherwise it will be defaulted to None.
* Default region name: this I had taken from the row entry given in the labsheet corresponding to my UWA student number, otherwise it will be defaulted to None.
* Default output format: this I had taken from the labsheet, otherwise it will be defaulted to None. json formatting was chosen as it is easily manipulatable for python. 
![image](https://hackmd.io/_uploads/H1tq7yBtC.png)

### [4] Install boto3

This can be achieved using `pip3 install boto3`. boto3 is provides a Python API for AWS infrastructure service. This will be essential for future labs, but for this current lab all I needed was to create a table from the output of different endpoints and regions of an AWS EC2 instance. An EC2 or Elastic Compute Cloud instance is an Amazon virtual server.

## Test the installed environment

### [1] Test the AWS environment

The command to test the AWS environment is `aws ec2 describe-regions --output table`. It will output a table of the different AWS endpoints and the regions that AWS has named them. As defined by Amazon, an endpoint is a URL that serves as an entry point for an AWS web service. 
![image](https://hackmd.io/_uploads/B1y7U1rFR.png)


### [2] Test the Python environment

To test the Python environment, enter the python environment using `python3`, then run the following script:
```
# python library that provides an API for AWS infrastructure services. 
>>> import boto3
# ec2 is a variable that will hold the retrieved information about the ec2 from the boto3 client. 
>>> ec2 = boto3.client('ec2')
# ec2 can be manipulated using inbuilt functions from boto3, the response of which will be stored in another variable.
>>> response = ec2.describe_regions()
>>> print(response)
```
![image](https://hackmd.io/_uploads/r1BsvyBYR.png)


### [3] Write a Python script

In order to tabulate the un-tabulated response above to have 2 columns with Endpoint and RegionName. I needed to use a python library called 'tabulate'. Using`pip3 install tabulate` I downloaded the 'tabulate' python library that displays data in a tabular structure. This library extended the original python code, by extracting the regions and their endpoints and storing them into a two-dimensional array called 'table'. This table was tabulated using the tabulate library with the format 'pretty' for it to be easily human readable. 

```
import boto3
from tabulate import tabulate

ec2 = boto3.client('ec2')

response = ec2.describe_regions()

# Extract the regions and their endpoints into a two dimensional array for traversal and connection between the RegionName and Endpoint.
regions = response['Regions']
table = [[region['RegionName'], region['Endpoint']] for region in regions]

# Print the table using tabulate
print(tabulate(table, headers=["RegionName", "Endpoint"], tablefmt="pretty"))

```
![image](https://hackmd.io/_uploads/ByjuOyBY0.png)
<div style="page-break-after: always;"></div>

# Lab 2

<div style="page-break-after: always;"></div>

# Lab 3

<div style="page-break-after: always;"></div>

# Lab 4

<div style="page-break-after: always;"></div>

# Lab 5

