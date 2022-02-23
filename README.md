# Checking_SSH
Checking how to generate the SSH key and use it to have a remote access

# <p align="center"><https://jumpcloud-1.wistia.com/medias/5usy6ga9lo?wvideo=5usy6ga9lo>

Secure Shell (SSH) is a way to connect securely between the local desktop/laptop to the remote server. E.g., secuely connecting the local repository to the remote repository in github server using SSH key. 
  
# Q. How does SSH work?
Ans. SSH has two programs - SSH Client and SSH Server, SSH Client belongs to the local machine while SSH Server belongs to the remte repository. SSH Server in remote repository is daemon i.e, always looking for the request from SSH client through TCP/IP ports. 
  
https://www.youtube.com/watch?v=2QXkrLVsRmk  When local machine ask for connection to the remote server it ask for the credentials the key, once we have the connection then we have the access to the remote server. Our terminal changes from the local machine the server specific pwd. 
  

# Q. What is Daemon?
Ans. In multitasking computer operating systems, a daemon (/ˈdiːmən/ or /ˈdeɪmən/)[1] is a computer program that runs as a background process, rather than being under the direct control of an interactive user. Traditionally, the process names of a daemon end with the letter d, for clarification that the process is in fact a daemon, and for differentiation between a daemon and a normal computer program. For example, syslogd is a daemon that implements system logging facility, and sshd is a daemon that serves incoming SSH connections. https://en.wikipedia.org/wiki/Daemon_(computing)
 
  
# SSH best example is to create the VM Ubuntu and then connect it remotely from the local machine. We can simply use the password of remote server (here the Ubuntu VM) to connect to it from the local macine. 
  ## Commands to do that are: 
    1. Remote Server should have Open SSH Sever installed: Debian uses # openssh-server or # openssh-client  
    2. Good to update and upgrade the system.
  sudo apt update && sudo apt upgrade (Recommended to do everytime we login) 
  
    3. To install the opensshserver on remote server (Ubuntu VM in our case) 
  sudo apt install openssh-server
  
    4. To check whether the openssh-server is running or not
  sudo systemctl status ssh       (It should run in case if it doen't get active, to start the ssh daemon run the command: sudo systemctl enable --now ssh) 
  
    5. Usually the OS like Ubuntu does have the firewall installed, and in this case we need to say the firewall to allow our ssh connection to set between the remote sever and the local machine. 
  
  sudo systemctl status ufw         (Checks for the status of Ufw-the firewall for ubuntu, whether its runnning or not)
  
  sudo ufw allow ssh                (Allows the ssh connection across the firewall)
  
   6. For now we have the running daemon ready for the accepting the connection from our local machine if we have the right credentials. 
   7. On local machine: connect using 
  
  sudo ssh user@ipaddress    
  
  - Here the User is the local machine and the ipaddress is of the remote machine. To chekc ip address of remote machine use: 
  ip a   
 or 
  ip addr show | grep "inet "
  
                                 ip address e.g., it will look of this format- 192.168.122.122 
  
   8. Now conect using:
  
  sudo ssh vikas@192.168.122.122
  
   9. It will ask for the password for the user on the remote server:  Give hte password and it done. 
   10. Remote SSH Connection set bbetween the local machine and the remote server (Ubuntu VM in our case). 
   11. Verify your connection to remote server checking the files and even here once can change the bash file:
 
  ls -la To list all file and folders)
 
  vim .bashrc (to look and if want to change the bash file.)
  
   12. To get out of the remote server and again use th elocal machine:
  
  exit
  
  
# SSH key-pair (private and public key to have a secure connection): The way to avoid the passwords. If there exists match of public and private key the ssh connection works. Though to initialize the SSH connection we need to enter the password of remote server first time later the private-public key pairing works passwordless.  
 
  ## Commands and steps to do that:
  
    1. To generate the ssh key: use ssh keygen
  ssh-keygen -t ed25519 -f ~/.ssh/xxx      
  
  Explaination:  -t for type, -f for file to store the ssh key in location (home directory) with the name xxx, SSH public key called xxx.pub
  
  Passphrase: One can add Passphrase as the second layer of security after key pair matching. Its a string. 
  
    2. Now copy the public key to the remote server using : ssh-copy-id
  $ ssh-copy-id -i ~/.ssh/xxx.pub user@ipaddress   
  or 
  $ ssh-copy-id user@ipaddress
   
  Explaination: Copying the ssh public id to the remote ipaddress. -i is to point at the right key here the public key.
  
    3. Now lets set the remote connection to the remote server using the private key:
  $ ssh -i ~/.ssh/lan user@ipaddress
  
    4. Check the user to verify that we are working on the remote server:
  whoami
>> user
  
    5. Now to enter the remote server:
  $ssh user@ipaddress 
  
  Will ask for the passphrase if set, otherwise will enter automatically to the remote server. 
  
 
 # For the SSH connection made by the key pairing one can stop the password authentication based SSH connection to the remote server: (Only the system with the keys will have connection)
  ## To do that we need to do the following step: 
  
  1. sudo vim /etc/ssh/sshd_config   
  
  Explaination: We are changing the content of ssh configuration file using the text editor: Vim we can use others as well example, gedit or nano. 
  
  2. Search for password using: 
  /Password
  
  3. Channge the PasswordAuthentication:
  Uncomment it and set it to no
  
 it will look like: PasswordAuthentication no
  
  4. To make the changes work we need to reload the ssh:
  
 $sudo systemctl reload ssh
   
  
