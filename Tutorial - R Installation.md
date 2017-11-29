# OVERVIEW

To install **RStudio Server**, **R**, **Shiny Server**, **Shiny** on an **Amazon Linux AMI** using User Data, connect to the Instance using **PuTTY**/**WinSCP** via SSH from Windows and access **RStudio**/**Shiny** using a web browser.



## Phase 1: Launching the Linux Instance

1. Use the *Launch Instance* wizard to set up **Amazon Linux AMI 2017.09.1 (HVM), SSD Volume Type - ami-1a962263**. 
2. In *Configure Instance Details*, Set *Auto-assign Public IP* to “Enable”, copy the scripts from 'Script_File.md' and paste in the *User Data* textbox, under *Advance Details*. (The script also creates a new user and password to access **RStudio**. You can update the user credentials with your preferred details).
3. 
   In *Configure Security Group*, add "HTTP" (Port 80) to the preexisting *SSH* rule (Port 22). Also add new rules ("Custom TCP Rule") to open ports 8787 for **RStudio Server** and 3838 for **Shiny Server**. Select “Anywhere” as Source for all four rules.
4. Launch the Instance.
5. If you create a new Key Pair, don't forget to download it to your local machine.



## Phase 2: Connect Using PuTTY/WinSCP

1. Download and install **PuTTY** and **WinSCP**.
2. Connect to the Instance using **PuTTY**. (First, you need to convert the .pem Key Pair to .ppk, which is the **PuTTY** compatible equivalent. You will use **PuTTYGen** for this). <https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/putty.html#putty-scp>
3. Next, using **WinSCP**, transfer the .pem file from your local Windows machine to the root directory of the Linux instance. Refer to this guide for details: <https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/putty.html#Transfer_WinSCP>
4. Return to the **PuTTY** terminal and type the following command to ensure that the key is not publicly viewable, lest SSH will not work:

```
chmod 400 key_name.pem
```

5. Use the this command to connect to the instance:

```
ssh -i "key_name.pem" ec2-user@instance_public_dns
```



## Phase 3: Web Browser Access

1. Navigate to *<u>public_dns:8787</u>* on your browser to open **RStudio** or *<u>public_dns:3838</u>* to open **Shiny**

2. Login with the user credentials created in Phase 1.

3. If you can't login, restart **RStudio** with this command and refer to the link below for possible user account management actions to be taken, including changing passwords, creating new users, viewing existing users, etc.;

   ```
   sudo restart rstudio-server
   ```

    <https://askubuntu.com/questions/410244/a-command-to-list-all-users-and-how-to-add-delete-modify-users>

   ​
