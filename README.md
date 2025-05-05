<div align="center">
  
  ![born2beroote](https://github.com/user-attachments/assets/714acb59-4011-469e-9127-2abfa9379501)
</div>

## Born2beRoot
Born2beRoot is a system administration and security project from 42 School. The goal is to set up a secure Linux virtual machine (VM) using a strict set of guidelines involving user management, firewall configuration, secure SSH access, and system monitoring.

<div align="center">
  
| Grade                                                             | Evaluation Information           |
| :---------------------------------------------------------------- | :------------------------------- |
| <img src="https://img.shields.io/badge/Born2beroot--not--submitted-lightgrey"/>  | `3 peers` `30 mins` `moulinette` |
</div>

## ✨ Features
   - Secure SSH Configuration
   - Firewall Setup with UFW
   - User and Group Management
   - Password Policy Enforcement
   - LVM (Logical Volume Management)
   - System Monitoring Script
   - Cron Job Automation
   - Sudo Usage Logging
   - Network & System Info Reporting

 ## VM Integrity Verification and Setup Guide
Since in this project I built my VM and delivered the signature for the .vdi file, I will leave a guideline to help you replicate the process and ensure the integrity of the virtual machine as well.
I did it withut bonus

### Install the ISO
- [ ] Go to this website to download the ISO for Debian : `https://www.debian.org/CD/netinst/` and install netinstCD image amd64
### Creating the Virtual Machine 🛠
- [ ] Open **VirtualBox** and click `new`;
- [ ] Give the VM a name;
- [ ] Store the VM inside `/sgoinfre/` directory;
- [ ] Select total amount of RAM to reserve for the machine;
- [ ] Create a new hard drive for the VM;
- [ ] Make the hard drive a **VDI** archive;
- [ ] Make the hard drive's memory dynamically allocated;
- [ ] Allocate 20 GB;
- [ ] Click `Create`;
- [ ] Go to `Settings` and click on `Storage`;
- [ ] Select the empty drive 💿 and click `Choose a disk file`;
- [ ] Select the `Debian ISO` that you downloaded and click `Open`, then click `ok`;
- [ ] Start the VM;
      
### Installing Debian 🌀

- [ ] Select `Install` from the Debian GNU/Linux menu;
- [ ] Set the language to `English`;
- [ ] Set the location to `Other`;
- [ ] Set continent to `Europe`;
- [ ] Set country to `Portugal`;
- [ ] Set locales to `United States`;
- [ ] Set keyboard to `American English`;
- [ ] Set a `hostname` for the VM:
> [!IMPORTANT]
> <kbd>**hostname**</kbd>:
> `dda-fons42`;
- [ ] Leave network settings blank (not required by the subject);
- [ ] Set password for `root` user;
> [!IMPORTANT]
> <kbd>Root Password</kbd> :
>
> `Daniel42beRoot`
- [ ] Set user full name for user: `dda-fons`;
- [ ] Set user username: `dda-fons`;
- [ ] Set user password;
> [!IMPORTANT]
> <kbd>User Password</kbd> :
>
> `Daniel42beUser`
- [ ] Set clock to Lisbon;

### Partitioning the Disk
- [ ] Select `Manual` partition method;
- [ ] Select the available volume;
> [!Note]
> The volume name may differ from system to system. Example:
>
> `SCSI1 (0,0,0) (sda) - 33.1 GB ATA VBOX HARDDISK`
- [ ] Confirm the creation of a new empty partition;

#### Create Primary Partition
- [ ] Select `FREE SPACE`;
- [ ] Create a new partition;
- [ ] Make the partition size `500m`:
- [ ] Set partition type to `Primary`;
- [ ] Set location for the new partition to `Beginning`;
- [ ] Set Mount point: `/boot`;
- [ ] Select `Done setting up the partition`;

#### Create Logical Partition
- [ ] Select `FREE SPACE` again;
- [ ] Create a new partition;
- [ ] Set the size to `max`;
- [ ] Set partition type to `Logical`;
- [ ] Set Mount point to: `Do not mount it`;
- [ ] Select `Done setting up the partition`;

#### Encrypting Volumes
- [ ] Click `Configure encrypted volumes`;
- [ ] Accept confirmation message;
- [ ] Click `Create encrypted volumes`;
- [ ] Select device `/dev/sda5`for encryption;
- [ ] Select `Done setting up the partition`;
- [ ] Select `Finish`;
- [ ] Accept confirmation message to encrypt;
- [ ] Hit `Cancel` because there's nothing to encrypt;
- [ ] Set encryption passphrase;
> [!IMPORTANT]
> <kbd>User Password</kbd> 
> 
> `Daniel42beCrypt`

#### Configure Logical Volume Manager
- [ ] Click `Configure Logical Volume Manager`;
- [ ] Accept confirmation message;
- [ ] Click `Create volume group`;
- [ ] Set the name to `LVMGroup`;
- [ ] Select partition to store the group: `/dev/mapper/sda5_crypt`;

#### Create Logical Partitions
- [ ] Select `Create Logical Volume`;
- [ ] Select group: `LVMGroup`;
- [ ] Set the name of the logical volume: `root`;
- [ ] Set it's size to: `10g`;
- [ ] Select `Create logical volume`;
- [ ] Select group: `LVMGroup`;
- [ ] Set the name of the logical volume: `swap`;
- [ ] Set it's size to: `5g`;
- [ ] Select `Create logical volume`;
- [ ] Select group: `LVMGroup`;
- [ ] Set the name of the logical volume: `home`;
- [ ] Set it's size to: `5g`;
      
#### Setting Mount Points
- [ ] Select partition #1, `home`;
- [ ] Set `Use as` to `Ext4`;
- [ ] Set Mount Point: `/home`;
- [ ] Select `Done setting up the partition`;
- [ ] Select partition #1, `root`;
- [ ] Set `Use as` to `Ext4`;
- [ ] Set Mount Point: `/`;
- [ ] Select `Done setting up the partition`;
- [ ] Select partition #1, `swap`;
- [ ] Set `Use as` to `swap area`;

#### Setting up Package Manager and the bootloader

- [ ] Accept confirmation message;
- [ ] Say **NO** to additional packages;
- [ ] Select country;
- [ ] Set Debian archive mirror package manager: `deb.debian.org`;
- [ ] Leave HTTP proxy empty and click `Continue`;
- [ ] Say **NO** to the popularity contest;
- [ ] Remove all software options and press `Continue`;
- [ ] Say `Yes` to the installation of **GRUB boot loader**;
- [ ] Select device to install the bootloader: `/dev/sda (ata_VBOX_HARDDISK)`;
- [ ] Select `Continue`;



## Virtual Machine Setup ⚙️


### Login into the system
- [ ] Enter encryption password;
- [ ] Enter user and password;
### Installing **sudo** & configuring groups and users
- [ ] Switch user to `root`:
```sh
su -
```
- [ ] Insert `root` password;
- [ ] To install **sudo** run:
```sh
apt install sudo
```
- [ ] Reboot the machine with the following command:
```sh
sudo reboot
```
- [ ] Login again with `user` and switch to `root`;
- [ ] Check **sudo**'s version with the command:
```sh
sudo -V
```

> [!Note]
> This command displays the currently installed version of **sudo** (and other extra info like which plugins are installed);

- [ ] Create a new user;
```sh
sudo adduser <login>
```

> [!Important]
> User Credentials
> 
> login: `daniel`
>
> password: `Daniel42beUser`

- [ ] Create a new group `user42`:
```sh
sudo addgroup user42
```
- [ ] Include `dda-fons` on both `sudo` and `user42` groups:
```sh
sudo adduser <user> <groupname>
```

>[!Important] 
> To check user groups and their users either:
>
> Switch user to `root`:
>
> - `getent group`;
>
> - `getent group <groupname>`;
>  > Filters `getent` output;

#### Installing **SSH**
- [ ] Update the system package manager:
```sh
sudo apt update
```

- [ ] Install **OpenSSH**:
```sh
sudo apt install openssh-server`
```

- [ ] When asked for confirmation type `Y`;

> [!Note]
> To check the state of the system's **SSH** service:
>
> - `sudo service ssh status`;
>
> The service must be shown as `Active`;


#### Installing **vim**
- [ ] Run the command:
```sh
sudo apt install vim
```

#### Configuring **SSH**
- [ ] If not `root` switch to it with `su`;
- [ ] Open `sshd_config` with vim:
```sh
vim /etc/ssh/sshd_config
```

- [ ] Set Port to `Port 4242`
- [ ] Set `PermitRootLogin no`
- [ ] Save changes and close file;
- [ ] Restart and update the **SSH** service:
```sh
sudo service ssh restart
```
- [ ] Check service's state with:
```sh
sudo service ssh status
```

#### Installing & Configuring **UFW** 🔥🧱

- [ ] Install **UFW** packages:
```sh
sudo apt install ufw
```
- [ ] Start **UFW** using the command
```sh
sudo ufw enable
```

- [ ] Configure **Firewall** to accept connections on 4242 port
```sh
sudo ufw allow 4242
```

- [ ] Check the current state of the firewall
```sh
sudo ufw status
```

> [!Note]
> Alternatively the firewall's state can be checked with
>
> - `sudo ufw status verbose`
> - `sudo ufw status numbered`

#### Connecting via **SSH**
- [ ] Get **VM**'s IP:
```sh
hostname -I
```
- [ ] Close the VM and go to `Settings`;
- [ ] Click on `Network`, then `Advanced`; 
- [ ] Change `Attached to:` from `NAT` to `Bridged Adapter`;
- [ ] Click `OK`;
- [ ] Re-open the **VM** and decrypt it:
- [ ] Open a terminal and connect to the **VM**:
```sh
ssh dda-fons@10.11.241.242 -p 4242
```
- [ ] To close the connection:
```sh
exit
```

#### Configuring **sudo** policies and log
- [ ] Create the following file:
```sh
touch /etc/sudoers.d/sudo_config
```

> [!Note]
> This file will store the system's **sudo** policy

- [ ] Open `sudo_config` to setup policy
```sh
vim /etc/sudoers.d/sudo_config
```

- [ ] Add the following Defaults to the file:
```
Defaults  passwd_tries=3
Defaults  badpass_message="Wrong password bruh, try again:"
Defaults  logfile="/var/log/sudo/sudo_config"
Defaults  log_input, log_output
Defaults  iolog_dir="/var/log/sudo"
Defaults  requiretty
Defaults  secure_path="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin"
```

> [!Note]
> `passwd_tries`=> total tried for entering **sudo** password;
>
> `badpass_message` => Message to be printed when password is wrong;
>
> `logfile` => Set custom log file for **sudo**;
>
> `log_input, log_output` => What will be logged;
>
> `iolog_dir` => Path where I/O logs will be stored;
>
> `requiretty`=> Enables **sudo** invocation from a real **TTY** but not through methods such as **cron** or **cgi-bin**;
>
> `secure_path` => The **PATH** used for every command run with **sudo**:
>
> > - Used when a system admin doesn't trust **sudo** users to have a secure **PATH** environment variable;
> > - Separates `root path` from `user path`;

- [ ] Create the following directory:
```sh
mkdir /var/log/sudo
```

> [!Note]
> This folder will store the system's **sudo** log


#### Change **hostname**  (for the defense)
- [ ] Check current **hostname**:
```sh
hostnamectl
```

- [ ] Change **hostname**:
```sh
hostnamectl set-hostname <hostname>
```

- [ ] Edit **/etc/hosts**
```sh
sudo vim /etc/hosts
```

- [ ] Change **old_hostname** to **new_hostname**
```sh
127.0.0.1 localhost
127.0.0.1 new_hostname
```
- [ ] Reboot and check for change:
```sh
sudo reboot hostnamectl
```

#### Configuring Password Policy 🔑
- [ ] Open `login.defs`:
```sh
vim /etc/login.defs
```

- [ ] Set `PASS_MAX_DAYS`to 30;
- [ ] Set `PASS_MIN_DAYS` to 2;
- [ ] Set `PASS_WARN_AGE` to 7;
- [ ] Update already created user's password policy:
```sh
chage -M 30 -m 2 -W 7
# or
passwd -x 30 -n 2 -w 7
```
- [ ] Install **libpam-pwquality**:
```sh
sudo apt install libpam-pwquality
```
- [ ] Configure **libpam-pwquality**:
```sh
sudo vim /etc/pam.d/common-password
```

- [ ] On the `per-package` section after `retry=3` add the following as inline options
```
minlen=10
ucredit=-1
dcredit=-1
lcredit=-1
maxrepeat=3
reject_username
difok=7
enforce_for_root
```
> [!Important]
>
> `minlen` => Minimum characters a password must have;
>
> `ucredit` => Password must contain at least one Uppercase char; must be set with a `-` sign to reference the lower bound; if set with `+` defines an upper bound;
>
> `dcredit` => Password must contain at least one `digit`;
>
> `lcredit` => Password must contain at least one `lowercase` letter;
>
> `maxrepeat` => Password must not repeat the same character consecutively `n` number of times;
>
> `reject_username` => Password must not contain the username;
>
> `difok` => Password must contain at least `n` different characters from the previously used password;
>
> `enforce_for_root` => Implement password policy to root;

### Monitoring Script 🚨

#### Get System Info
- [ ] Get system **Architecture** info:
```sh
uname -a
```
- [ ] Get system's number of **Physical Cores**:
```sh
grep "physical id" /proc/cpuinfo | wc -l
```
- [ ] Get system's number of **Virtual Cores**:
```sh
grep processor /proc/cpuinfo | wc -l
```
- [ ] Get amount of used **RAM**:
```sh
free --mega | awk '$1 == "Mem:" {print $3}'
```
- [ ] Get total amount of memory in the system:
```sh
free --mega | awk '$1 == "Mem:" {print $2}'
```
- [ ] Get used memory percentage:
```sh
free --mega | awk '$1 == "Mem:" {printf("(%.2f%%)\n", $3/$2*100)}'
```


> [!Note]
> Command: `awk`
> **awk** filters **free**'s output by checking if `$1` (first word) on each line equals (for instance) `"Mem:"`, and print only the lines that meet this condition;

> [!Note]
> Command: `free`
> for more on the **free** command;

- [ ] Get amount of used disk memory:
```sh
df -Bm | grep "/dev/" | grep -v "/boot" | awk '{used += $3} END {print used}'
```
- [ ] Get system's total Disk space:
```sh
df -m | grep "/dev/" | grep -v "/boot/" | awk '{total_mem += $2} END {printf ("%.0fGb\n"), total_mem/1024}'
```

- [ ] Get used memory percentage
```sh
df -m | grep "/dev/" | grep -v "/boot" | awk '{used += $3} {total += $2} END {printf("(%d%%)\n"), used/total*100}'
```

> [!Note]
> Command: `df`
>
> - Stands for `Disk Filesystem` command; 
> - Prints a summary about disk usage;
> - The `-m` flag prints prints result in MB;

> [!Note]
> Command: `grep`
> - Filter output with **grep** to select only lines containing `/dev/`;
> - To exclude lines containing `/boot/` call [[grep]] with the `-v` flag;

> [!Note] 
> Command `awk`
> - `awk '{memory_use += $3} END {print memory_use}'` gets the sum of the values on the 3rd column of each line and prints the final result;
>

##### CPU Information
- [ ] Get percentage of **CPU** usage:
```sh
vmstat 1 4 | tail -1 | awk '{print $15}'
# or
top -bn1 | tail +8 | awk '{ cpul += $9 } END { printf("%.1f"), cpul }'
```

> [!Note] 
> Command: `vmstat`
>
> `vmstat` reports information with details about the processes , memory usage, CPU activity, system status, etc.
> - The options `1 4` define an interval in seconds

> [!Note] 
> Command: `tail`
>
> The **tail** command when used with the `-1` flag outputs only the last line received from the previous command;

___
##### Last Reboot
- [ ] Get Date and Time of last reboot:
```sh
who -b | awk '$1 == "system" {print $3 " " $4}'
```

> [!Note] 
> Command: `who`
>
> The command `who` when used with the `-b` flag prints the date and time of the last boot.

___
##### **LVM** check
- [ ] Check if **LVM** is active:
```sh
if [ $(lsblk | grep "lvm" | wc -l) -gt 0 ]; then echo yes; else echo no; fi
```

> [!Important]
> - `$(...)` is a command substitution;
> Executes the command inside the parentheses and replaces it with it's output;
> - In bash the `-gt` flag is the `Greater Than` **Comparison Operator** used for arithmetic operations in bash scripting;

> [!Note]
> Command: `lsblk`
>
> The `lsblk` command displays information about all available block devices (Hard Drives, SSDs, memories, etc)

___
##### **TCP** connection
- [ ] Check for the number of established **TCP** connections:
```sh
ss -ta | grep ESTAB | wc -l
```

> [!Note]
> Command: `ss`
>
> The `ss` command (replacing the now obsolete **netstat**) is a utility to investigate sockets; It can display more **TCP** and state information than other tools.

___
##### Number of users
- [ ] Get number of users:
```sh
users | wc -w
```

> [!Note]
> Command: `users`
>
> The command `users` displays the number of users define for the system;


##### **IP Address** & **MAC**
- [ ] Get host IP address
```sh
hostname -I
```
- [ ] Get the MAC address
```sh
ip link | grep "link/ether" | awk '{print $2}'
```

> [!Note]
> Command: `hostname`
> 
> To change `hostname` edit
> - `vim /etc/hosts`
> and
> - `vim /etc/hostname`
>


##### Number of commands invoked by `sudo`
- [ ] Get number of commands invoked by `sudo`
```sh
journalctl _COMM=sudo | grep COMMAND | wc -l
```

> [!Note]
> Command: `journaclctl`
> 
> The command `journaclctl` collects and manages system logs;
> - `_COMM=sudo` filters out everything but `sudo` executions;

#### **Put monitoring script together**

- [ ] To test the script execute:
```sh
sudo /home/dda-fons.sh
```

#### **Crontab**
- [ ] Edit the `crontab` file
```sh
sudo crontab -u root -e
```
- [ ] Configure a script to execute every 10 minutes:
```sh
*/10 * * * * sh /home/dda-fons/monitoring.sh
```
- [ ] To make it be precise to the minute edit `crontab` to run `sleep.sh` script to delay the monitoring dump
```sh
*/10 * * * * sh /home/dda-fons/sleep.sh; sh /home/dda-fons/monitoring.sh
```

> [!Note] 
> Research **Swap Partition**
> Research **Ext4**

