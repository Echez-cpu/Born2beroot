🖥️ 42_IC_Ring01_Born2beRoot


Preface:
This is a guide to the Born2beRoot project, & was written using resources from several other guides, therefore the credit is to them.
The purpose of re-writing this updated guide is to edit some discrepencies that I've come across using some of the guides, & help prevent issues that I've had to troubleshoot.
Debian is the chosen Operating System for this project.


The Mandatory part of the subject.pdf involves using the Guided Partitioning Method of the Debian installation. The Bonus part of the subject.pdf involves using the Manual Partitioning Method. This guide has instructions for the Manual Partitioning Method, which I recommend you do from the start, thus passing you both the Mandatory part, and 1/3 of the Bonus part of Born2beRoot.


🔷 Outline of Steps:


Step 1: Download the Debian installer for your Virtual Machine (VM)
Step 2: Installing your VM

Step 3: Setting up your VM partitions


Step 4: Starting & setting up your VM


Step 5: Connecting to SSH


Step 6: Configuring your VM - Password Policy


Step 7: Creating user Groups

Step 8: Configuring your VM - User Priviledges


Step 9: Configuring your VM - Script Monitoring & Crontab


Step 10: Self-evaluation Checklist & Testing


Step 11: Retrieve the Signature of your machine’s virtual disk


Step 12: Evaluation Answers



🔷 Step 1: Download the Debian installer for your Virtual Machine (VM)
🔸 1.1: Debian
Click here to download Debian GNU/Linux
Scroll to the bottom of the page and select debian-mac-xx.x.x-amd64-netinst.iso



🔸 1.2: VM Directory (For 42Adelaide Students)
In iTerm2:
cd sgoinfre/students
mkdir <your_intra_username>
chmod 700 <your_intra_username>
Find your Debian download file from Step 1.1 and put that download in this sgoinfre/students/<your_intra_username> directory that you have just created (in iTerm2, open . to open/find the directory, & drag/drop your Debian download file in there).



🔸 1.3: Virtual Box
Open the Virtual Box application
🔷 Step 2: Installing your VM
Select New

Name and operating system:

Name: e.g. Born2beRoot
Machine Folder: /sgoinfre/students/<your_intra_username> (Do not type this in, use the drop down option.)
Type: Linux 
Version: Debian (64-bit)
Continue
Memory Size:

1024MB
Continue
Hard disk:

Select Create a Virtual Hard Disk Now
Create
Hard disk file type:

Select VDI (VirtualBox Disk Image)
Continue
Storage on physical hard disk:

Select Dyamically Allocated
Continue
File location and size:

8.00GB
Create
VM Storage:



Go to Settings
Select Storage
In the list of Storage Devices on the left, underneath "Controller: IDE", select the blue 💿 labeled "Empty"
Find "Optical Drive" under "Attributes" & click on the drop down menu. Select Choose a disk file...
Select the Debian Download file (.iso) from your /sgoinfre/students/<your_intra_usename> directory.
Open
Ok





🔷 Step 3: Setting up your VM partitions
Go to Start (The green arrow).


Note: you will only be able to use your Keyboard to operate your Virtual Machine.

Note: to increase the size of your VM window, go to the menu bar and either:

Select Scaled Mode (Host+C) then, with your mouse drag the VM window.
Select Virtual Screen 1 then, select Scale to 200% (autoscaled output)
Select Install (Do not select "Graphical install").


Select a language: English


Select your location: Australia


Configure the keyboard: American English


Configure the network:



Hostname: <your_intra_username42> (ensure "42" is at the end)
Domain name: leave blank
Set up users and passwords:





Root password: it is reccomended you use the same passwords for all passwords. Write it down should you forget it.
Full name for the new user: personally, I used <your_intra_username> without the "42".
Username for your account: <your_intra_username> without the "42".
Choose a password for the new user: use the same password as "Root password".
Partition disks:





🔸

Select Manual
Select SCSI1 (0,0,0) (sda) 8.6 GB ATA VBOX HARDDISK
Create new empty partition table on this device?: Yes
Select pri/log 8.6 GB FREE SPACE
How to use this free space: Create a new partition
New partition size: 500M
Type for the new partition: Primary
Location for the new partition: Beginning
Partition settings: Mount point:     /
Mount point for this partition: /boot - static files of the boot loader
Partition settings: Done setting up the partition





🔸

Select pri/log 8.6 GB FREE SPACE
How to use this free space: Create a new partition
New partition size: max
Type for the new partition: Logical
Partition settings: Mount point:     /
Mount point for this partition: Do not mount it
Partition settings: Done setting up the partition







🔸

Select Configure encrypted volumes
Write changes to disk and configure encrypted volumes?: Yes
Encryption configuration actions: Create encrypted volumes
Devices to encrypt: using to select/de-select, ensure that:
[ ] /dev/sda1 is de-selected
[*] /dev/sda5 is selected
Select Done setting up the partitions
Encryption configuration actions: Finish
Really erase the data on SCSI1 (0,0,0), partition #5 (sda)?: Yes
Encryption passphrase: Personally, I used the same password set previously, x2, to avoid forgetting it.





🔸

Select Configure the Logical Volume Manager
Write the changes to disks and configure LVM?: Yes
LVM configuration action: Create volume group
Volume group name: LVMGroup
Devices for th new volume group:
[*] /dev/mapper/sda5_crypt is selected

[ ] /dev/sda1 is de-selected



🔸

LVM configuration action: Create logical volume
Volume group: LVMGroup
Logical volume name: root
Logical volume size: 2G



🔸

LVM configuration action: Create logical volume
Volume group: LVMGroup
Logical volume name: swap
Logical volume size: 1024MB



🔸

LVM configuration action: Create logical volume
Volume group: LVMGroup
Logical volume name: home
Logical volume size: 1G


🔸

LVM configuration action: Create logical volume
Volume group: LVMGroup
Logical volume name: var
Logical volume size: 1G


🔸

LVM configuration action: Create logical volume
Volume group: LVMGroup
Logical volume name: srv
Logical volume size: 1G


🔸

LVM configuration action: Create logical volume
Volume group: LVMGroup
Logical volume name: tmp
Logical volume size: 1G



🔸

LVM configuration action: Create logical volume
Volume group: LVMGroup
Logical volume name: var-log (yes, type only one '-' which will be automatically updated to '--')
Logical volume size: 1056MB
LVM configuration action: Finish



🔸

Under the line with "LV home" in it, select #1
Partition settings: Use as:    do not use
How to use this partition: Ext4 journaling file system
Partition settings: Mount point:   none
Mount point for this partition: /home - user home directories
Partition settings: Done setting up the partition




🔸

Under the line with "LV root" in it, select #1
Partition settings: Use as:    do not use
How to use this partition: Ext4 journaling file system
Partition settings: Mount point:   none
Mount point for this partition: / - the root file system
Partition settings: Done setting up the partition




🔸

Under the line with "LV srv" in it, select #1
Partition settings: Use as:    do not use
How to use this partition: Ext4 journaling file system
Partition settings: Mount point:   none
Mount point for this partition: /srv - data for services provided by this system
Partition settings: Done setting up the partition



🔸

Under the line with "LV swap" in it, select #1
Partition settings: Use as:    do not use
How to use this partition: swap area
Partition settings: Done setting up the partition



🔸

Under the line with "LV tmp" in it, select #1
Partition settings: Use as:    do not use
How to use this partition: Ext4 journaling file system
Partition settings: Mount point:   none
Mount point for this partition: /tmp - temporary files
Partition settings: Done setting up the partition



🔸

Under the line with "LV var" in it, select #1
Partition settings: Use as:    do not use
How to use this partition: Ext4 journaling file system
Partition settings: Mount point:   none
Mount point for this partition: /var - variable data
Partition settings: Done setting up the partition




🔸

Under the line with "LV var-log" in it, select #1
Partition settings: Use as:    do not use
How to use this partition: Ext4 journaling file system
Partition settings: Mount point:   none
Mount point for this partition: Enter manually
Mount point for this partition: /var/log
Partition settings: Done setting up the partition
At the end of the list, select Finish partitioning and write changes to disk
Write the changes to disk?: Yes
Confugure the package manager:

Scan another CD or DVD?: No
Debian archive mirror country: Australia
Debian archive mirror: deb.debian.org
HTTP proxy information (blank for none): leave blank
Software selection:

Choose software to install: ensure all items are de-selected
GRUB boot loader:

Install the GRUB boot loader to the master boot record?: Yes
Device for boot loader installation: /dev/sda (ata-VBOX_HARDDISK_xxxxxxxxxx-xxxxxxxx)
Finish the installation:





Installation complete: Continue
🔷 Step 4: Starting & setting up your VM


🔸 4.1: Starting up your VM
At every start up, use your encryption password.
You can either:
Login as root or
Login as <your_intra_username>, then later use su - to log in as root if required.



🔸 4.2: Installing Sudo
Ensure you are logged in as root: su -
apt-get update -y
apt-get upgrade -y
apt install sudo
sudo usermod -aG sudo <your_intra_username> to add user in the group 'sudo'.
getent group sudo to check if user is in sudo group.
sudo visudo to open the sudoers file.
Find the line: # User privilege specification. Underneath that line, type <your_intra_username>  	ALL=(ALL) ALL



🔸 4.3: Installing Git
sudo apt-get install git -y




🔸 4.4: Installing Vim
sudo apt-get install vim -y



🔸 4.5: Installing & Configuring SSH (Secure Shell Host)
sudo apt install openssh-server
sudo systemctl status ssh to check SSH Server Status.
sudo vim /etc/ssh/sshd_config
Find the line #Port22. Edit it to Port 4242 without the '#' in front of it.
Save and Exit Vim. (Use :q then follow the prompts to save. ^ means <Ctrl>).
sudo service ssh restart to restart the SSH Service.




🔸 4.6: Installing & Configuring UFW (Uncomplicated Firewall)
sudo apt-get install ufw to install UFW.
sudo ufw enable to enable UFW.
sudo ufw status numbered to check the status of UFW.
sudo ufw allow ssh to configure the Rules.
sudo ufw allow 4242 to configure the Port Rules.
sudo ufw status numbered to check the status of UFW 4242 Port.





🔷 Step 5: Connecting to SSH
Note: press <command> on your Apple Keyboard & your mouse should re-appear

Go to your Virtual Box Program.
Click on your Virtual Machine and go to Settings
Go to Network
Select Adapter 1
Select Advanced
Click on Port Forwarding
Change the Host Port & Guest Port to 4242:
Name: Rule 1
Protocol: TCP
Host IP: (blank)
Host Port: 4242
Guest IP: (blank)
Guest Port: 4242
Ok
Go back to your Virtual Machine.
Check the file sshd_config via sudo vim /etc/ssh/sshd_config and make sure these two lines are uncommented and with the parameters:
13 Port 4242
32 PermitRootLogin no
sudo systemctl restart ssh to restart your SSH Server.
sudo service sshd status to check your SSH Status.
Open an iTerm & type ssh <your_intra_username>@127.0.0.1 -p 4242
Note: In case an error occurs, type rm ~/.ssh/known_hosts in your iTerm & then retype ssh <your_intra_username>@127.0.0.1 -p 4242
Type exit to quit your SSH iTerm Connection.
🔷 Step 6: Configuring your VM - Password Policy
sudo apt-get install libpam-pwquality to install Password Quality Checking Library
sudo vim /etc/pam.d/common-password
Find this line: password		requisite		pam_pwquality.so
Add to the end of that line minlen=10 ucredit=-1 dcredit=-1 lcredit=-1 maxrepeat=3 reject_username difok=7 enforce_for_root
The line should now look like this: password  requisite     pam_pwquality.so  retry=3 minlen=10 ucredit=-1 dcredit=-1 lcredit=-1 maxrepeat=3 reject_username difok=7 enforce_for_root
Exit & Save Vim
sudo vim /etc/login.defs to configure the Password Policy.
Find this part PASS_MAX_DAYS 9999 PASS_MIN_DAYS 0 PASS_WARN_AGE 7. Edit that part to:
PASS_MAX_DAYS 30
PASS_MIN_DAYS 2
PASS_WARN_AGE 7
sudo reboot to reboot the change affects.
🔷 Step 7: Creating user Groups
🔸 7.1: Creating a group
sudo groupadd user42 to create the group 'user42`.
getent group to check if the group has been created.
🔸 7.2: Group allocation
sudo usermod -aG user42 <your_intra_username> to add your username to the group 'user42' as per subject requirements.
getent group user42 to check if the user is in the group.
cut -d: -f1 /etc/passwd to check all local users.
🔷 Step 8: Configuring your VM - User Priviledges
🔸 8.1: Creating the sudo.log
cd ~/../
cd var/log
mkdir sudo
cd sudo
touch sudo.log
cd ~/../
🔸 8.2: Configuring the Sudoers Group
sudo visudo to open to Sudoers file.
Edit your sudoers file by adding the rest of the defaults so it should read like this:
Defaults	env_reset
Defaults	mail_badpass
Defaults	secure_path="/usr/local/sbin:/usr/local/bin:/usr/bin:/sbin:/bin"
Defaults	badpass_message="Password is wrong, please try again!"
Defaults	passwd_tries=3
Defaults	logfile="/var/log/sudo/sudo.log"
Defaults	log_input, log_output
Defaults	requiretty
🔷 Step 9: Configuring your VM - Script Monitoring & Crontab
🔸 9.1: Creating and configuring the monitoring.sh script
sudo apt-get install -y net-tools to install the netstat tools.

cd /usr/local/bin/

touch monitoring.sh

chmod 777 monitoring.sh to change file permissions to allow full permissions ("7") for -owner -group -all other users.

Open an iTerm2 & type ssh <your_intra_username>@127.0.0.1 -p 4242.

cd /usr/local/bin

vim monitoring.sh and paste into the vim monitoring.sh the following:

#!/bin/bash
arc=$(uname -a)
pcpu=$(grep "physical id" /proc/cpuinfo | sort | uniq | wc -l) 
vcpu=$(grep "^processor" /proc/cpuinfo | wc -l)
fram=$(free -m | awk '$1 == "Mem:" {print $2}')
uram=$(free -m | awk '$1 == "Mem:" {print $3}')
pram=$(free | awk '$1 == "Mem:" {printf("%.2f"), $3/$2*100}')
fdisk=$(df -BG | grep '^/dev/' | grep -v '/boot$' | awk '{ft += $2} END {print ft}')
udisk=$(df -BM | grep '^/dev/' | grep -v '/boot$' | awk '{ut += $3} END {print ut}')
pdisk=$(df -BM | grep '^/dev/' | grep -v '/boot$' | awk '{ut += $3} {ft+= $2} END {printf("%d"), ut/ft*100}')
cpul=$(top -bn1 | grep '^%Cpu' | cut -c 9- | xargs | awk '{printf("%.1f%%"), $1 + $3}')
lb=$(who -b | awk '$1 == "system" {print $3 " " $4}')
lvmu=$(if [ $(lsblk | grep "lvm" | wc -l) -eq 0 ]; then echo no; else echo yes; fi)
ctcp=$(ss -neopt state established | wc -l)
ulog=$(users | wc -w)
ip=$(hostname -I)
mac=$(ip link show | grep "ether" | awk '{print $2}')
cmds=$(journalctl _COMM=sudo | grep COMMAND | wc -l)
wall "	#Architecture: $arc
          #CPU physical: $pcpu
          #vCPU: $vcpu
          #Memory Usage: $uram/${fram}MB ($pram%)
          #Disk Usage: $udisk/${fdisk}Gb ($pdisk%)
          #CPU load: $cpul
          #Last boot: $lb
          #LVM use: $lvmu
          #Connections TCP: $ctcp ESTABLISHED
          #User log: $ulog
          #Network: IP $ip ($mac)
          #Sudo: $cmds cmd"
Save & Exit.

exit to exit the iTerm SSH Login.

Go back to your Virtual Machine.

sudo visudo to open your sudoers file

Find this line: %sudo ALL=(ALL:ALL) ALL. Underneath this line, add <your_intra_username ALL=(ALL) NOPASSWD: /usr/local/bin/monitoring.sh

Exit & Save.

sudo reboot to reboot sudo.

sudo /usr/local/bin/monitoring.sh to execute your script.

🔸 9.2: Configuring crontab
sudo crontab -u root -e to open the crontab and add a rule
At the end of the crontab, type */10 * * * * /usr/local/bin/monitoring.sh this means that every 10 mins, the monitoring.sh script will be broadcasted.
🔷 Step 10: Self-evaluation Checklist & Testing
Note: I recommend going through the checklist yourself to ensure everything works as it should, before retrieving the signature of your machines virtual disk.

🔸 10.1: Preliminary tests (for your peer evaluation)
 Git repository is sucessfully cloned.
 The Git repository contains a signature.txt file.
 cat signature.txt then cd/sgoinfre/students/<your_intra_username>/<your_VM_name> then cd <your_VM_name> then shasum <your_VM_name>.vdi The signature.txt against the students “.vdi” file is identical.
 Clone the VM then start it up.
🔸 10.2: General VM Setup
 sudo ufw status checks UFW service is started. Look for status: active
 sudo systemctl status ssh checks SSH service is started.
 lsb_release -a || cat /etc/os-release checks the chosen operating system (Debian or Rocky).
🔸 10.3: Mandatory Part (for your peer evaluation)
 During the defense, a script must display all information every 10 minutes.
 What is a Virtual Machine, & how does it work?
 What are the differences between Rocky & Debian?
 What is your choice of operating system & why?
 For Debian: what are the differences between aptitude and apt?
 What is APPArmor?
 All explanations are satisfactory (or evaluation stops here).
 What is LVM & what does it do?
 What is SSH & the value of using it?
 What is UFW & the value of using it?
 What is sudo?
🔸 10.4: Users & groups
 getent group sudo the students intra username must be present in the group sudo.
 getent group user42 the students intra username must be present in the group user42.
 sudo adduser <new_user> evaluator to create a new user e.g. testuser.
 sudo groupadd <groupname> evaluator to create a new group e.g. testgroup.
 sudo usermod -aG <groupname> <username> evaluator to add the new user to the new group.
 groups <username> checks the group the user belongs to.
🔸 10.5: Password policy
 sudo chage -l <username> checks the newly created user password follows the required policy (30 days max, 2 days min, 7 days warning).
 How do you implement the password policy?
 What are the advantages & disadvantages of the password policy?
🔸 10.6: Hostname and partitions
 hostnamectl checks the hostname of the machine is correctly formatted as follows: <student_login>42
 sudo hostnamectl set-hostname <new_hostname> evaluator to modify the hostname by replacing the login with theirs. Then, sudo reboot to restart the VM.
 On restart, if the hostname has not been updated, the evaluation stops here. Otherwise, the student logs back in (not the evaluator).
 sudo hostnamectl set-hostname <new_hostname> to restore the VM to the original hostname. Then, sudo reboot to restart the VM.
 lsblk to view the VM's partitions. Compare the output with the example given in the subject.pdf.
🔸 10.7: Sudo
 sudo visudo the student shows how to access the sudoers file.
 What is the sudoers file, & its purpose?
 cd /var/log/sudo verify the “/var/log/sudo/” directory exists.
 ls should show sudo.log file exists.
 cat sudo.log should display a history of the sudo command executions.
 Run any command using sudo. Check if the sudo.log file in the “/var/log/sudo/” directory have been updated.
🔸 10.8: UFW
 sudo ufw status numbered Lists the active rules in UFW. A rule must exist for port 4242.
 sudo ufw allow 8080 Adds a new rule to open port 8080. sudo ufw status numbered to check that this rule has been added by listing the active rules.
 Delete this new rule with the help of the student. sudo ufw delete 6 sudo ufw delete 3
🔸 10.9: SSH
 sudo service ssh status checks if its active & uses port 4242.
 In an iterm2, ssh <new_user>@127.0.0.1 -p 4242 evaluator to connect to SSH with their username. If connection successful, exit to exit the connection.
 ssh <your_intra_username42>@127.0.0.1 -p 4242 checks that the root user cannot connect to SSH. An error message "permission denied" should be displayed. Recall, <your_intra_username42> with the 42 in it is the root user. This is easily forgotten.
🔸 10.10: Script Monitoring
 What is the monitoring.sh script?
 What is the wall command?
 Ask to see the student's code for the script. cd /usr/local/bin then, vim monitoring.sh
 What is Cron & its purpose?
 sudo crontab -u root -e (change the 10 value to 1)
 The student being evaluated should make the script stop or start running without modifying the script itself. To check this, sudo reboot to restart the VM.
sudo /etc/init.d/cron stop
sudo /etc/init.d/cron start
🔷 Step 11: Retrieve the Signature of your machine’s virtual disk
log out & Power off your machine to close your VM. ⚠️ DO NOT RETRIEVE YOUR DISK'S SIGNATURE WITHOUT COMPLETING THIS STEP!⚠️
In iTerm2, cd /sgoinfre/students/<your_intra_username>/<your_VM_name> to go into the directory where your .vdi file is.
ls to view the .vdi file.
shasum <your_VM_name>.vdi to retrieve your VM's disk signature. (This can take up to several minutes.)
Copy and paste this into a signature.txt file at the root of your Git repository.
Clone your VM from VirtualBox.
Repeat steps 2 - 3 to ensure your signature.txt is identical to your <your_VM_name>.vdi before pushing for evaluation.
Note: Ensure your evaluator starts your VM Clone for evaluation to prevent your disk's signature from changing for the next evaluation.

🔷 Step 12: Evaluation Answers
A Virtual Machine (VM)
is like a computer within a computer.
a software based emulation of a physical computer system.
a VM is an isolated environment, seperate from your main computer system. Here, you can run different operating systems, software, applications, experiments, and tests without affecting your main computer.
a VM works by mimicking the hardware componenets of a physical computer: CPU, RAM, storage, and network interfaces, creating a virtualised environment that behaves like a physical computer. Back to Evaluation Checklist
The differences between Rocky and Debian
Debian has a community driven development model and a large community of contributers and users. Debian aims to be a universal Operating System, suitable for a wide range of use cases including desktop systems and personal servers. It adheres to the Free Software Principles (FSP): freedom to run, study, modify, and distribute software.
Rocky is led by the Rocky Enterprise Software Foundation that oversees the development and distribution of Rocky Linux. Rocky provides an enterprise-grade linux that serves as a drop-in replacement for CentOS. It is designed, developed and tested to meet the demands of larger scale businesses and organisations. Back to Evaluation Checklist
The subject.pdf reccommends Debian
for beginners in system administration, as setting up Rocky is more complex.
Debian is user-friendly.
Debian being older than Rockey, has a larger, active community of users and developers which means there is access to extensive documentation and resources for troubleshooting. Back to Evaluation Checklist
The difference between aptitude and apt
aptitude more advanced and interactive, while apt is simpler and more straightforward.
the main difference between aptitude and apt is how they handle package dependencies (other software needed for a program to work). aptitude is smarter at resolving complex dependencies and finding the best solution. It can suggest alternative options if there are conflicts between packages. apt, on the other hand, is simpler and more straightforward in resolving dependencies.
Another difference is how you use them. apt has shorter and easier-to-remember commands, like apt update or apt install, while aptitude uses slightly different commands like aptitude update or aptitude install.
aptitude has a special text interface that lets you browse and search for packages interactively, while apt doesn't have that feature. Back to Evaluation Checklist
AppArmor
provides an additional layer of defense by restricting an application's privileges and actions to only what is explicitly permitted by its security policy.
using AppArmor, system administrators and developers can enhance the security of their systems by limiting the potential impact of security breaches or unauthorized access to sensitive resources. It adds an extra layer of protection to help prevent applications from causing harm or accessing data they shouldn't have access to. Back to Evaluation Checklist
LVM
stands for Logical Volume Manager.
it allows the manipulation of partitions or logical volume on a storage device. Back to Evaluation Checklist
SSH
stands for Secure Shell.
an authentication mechanism between a client and a host.
uses encryption techniques so that all communication between clients and hosts is done in encyypted form, preventing unauthorised access, protecting sensitive data. Back to Evaluation Checklist
UFW
stands for Uncomplicated Firewall.
an interface that modifies the firewall of a device without compromising security.
used to configure which ports to allow connections, and which ports to close.
useful in conjunction with SSH. Back to Evaluation Checklist
Short for "superuser do"
sudo is a command used to execute other commands requiring higher priveledges and permissions.
allows a user with admin priveleges to temporarily gain "root" or superuser priveledges. Back to Evaluation Checklist
To set up the password policy
the command is sudo vim /etc/login.defs. Here we can adjust the frquency of:
the maximum number of days before a password expiry.
the minimum number of days allowed before the modification of a password.
the number of days before a user receives a warning message their password is to expire. Back to Evaluation Checklist
The advantages of the password policy
include increasing the security of the system.
the disadvantages include the challenge of having to change passwords if frequent, and it can be difficult to create new and different passwords each time. Back to Evaluation Checklist
The sudoers file
contains the configurations of user priveledges.
using the command sudo visudo opens the sudoer's fie, and here, you can edit user priveledges. Back to Evaluation Checklist
The monitoring.sh script
is used to monitor the performance and status of a server or system.
it gathers data on system resource utilizaiton (e.g. CPU, memory, disk usage), network traffic and other metrics. Back to Evaluation Checklist
The wall command
is used to broadcast a message (i.e. the monitoring.sh script) to all users currently logged on to the system. Back to Evaluation Checklist
Cron
from the Greek word "chronos", means the measure of time.
is a utility program that enables the scheduling of commands or scripts to run automatically at specified intervals.
crontab is the configuration file where you can specify the commands to run and when.
each asterisk *, accounts for: minute; hour; day; month; day of the week, in this order. Back to Evaluation Checklist
😎 Good luck!
