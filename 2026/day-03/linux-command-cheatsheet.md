# Day 03 of linux practice 
# Linux Commands Cheat Sheet

Simple and useful Linux commands for daily practice.


# File System Commands

`pwd`  
Show current directory location.

`ls`  
List files and folders.

`ls -la`  
Show all files with permissions.

`cd folder_name`  
Move into a folder.

`cd ..`  
Go back one directory.

`mkdir demo`  
Create a new folder.

`touch file.txt`  
Create a new file.

`cp file1.txt file2.txt`  
Copy a file.

`mv old.txt new.txt`  
Rename or move a file.

`rm file.txt`  
Delete a file.

`rm -r folder_name`  
Delete a folder recursively.

`cat file.txt`  
View file content.

`nano file.txt`  
Open file in nano editor.

`vim file.txt`  
Open file in vim editor.

`find . -name file.txt`  
Search file in current directory.

`chmod 400 key.pem`  
Change file permissions.

`df -h`  
Check disk space.

`du -sh folder_name`  
Check folder size.


#  Process Management Commands

`ps aux`  
Show running processes.

`top`  
Monitor live running processes.

`htop`  
Interactive process viewer.

`kill PID`  
Stop a process using process ID.

`kill -9 PID`  
Force stop a process.

`jobs`  
Show background jobs.

`bg`  
Run process in background.

`fg`  
Bring background process to foreground.

`nohup command &`  
Run process after logout.

`free -h`  
Check RAM usage.

`uptime`  
Show system uptime.


#  Networking Commands

`ping google.com`  
Check internet connectivity.

`ip addr`  
Show IP address details.

`curl https://example.com`  
Fetch website response.

`dig google.com`  
Check DNS information.

`netstat -tulnp`  
Show open ports.

`ss -tulnp`  
Display listening ports.

`traceroute google.com`  
Trace network route.

`wget URL`  
Download file from internet.


#  User & Permission Commands

`whoami`  
Show current logged-in user.

`sudo command`  
Run command as administrator.

`passwd`  
Change user password.

`id`  
Show user ID and group ID.


#  Package Management Commands

`sudo apt update`  
Update package list.

`sudo apt upgrade`  
Upgrade installed packages.

`sudo apt install nginx`  
Install a package.

`sudo apt remove nginx`  
Remove a package.


