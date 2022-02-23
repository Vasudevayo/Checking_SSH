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
  
  - Here the User is the local machine and the ipaddress is of the remote machine. To chekc ip address of remote machine use: ip a   
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
  
  
# SSH key-pair (private and public key to have a secure connection): The way to avoid the passwords. If there exists match of public and private key the ssh connection works. 
  ## Commands and steps to do that:
    1. 
    2. 
    3. 
    4. 
    5. 
    6.
    7. 
  
