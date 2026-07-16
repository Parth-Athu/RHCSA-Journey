CH-1 Introduction to Vim and ssh

Bash shell ( Bourne again shell )
tilde= home directory


administrator=root

command syntax in linux

command [option/argument] [target in form of path]
 type of command written 

# command 
#command option 
#command argument 
# command option argument 

there is help available for each command in two ways
1) command name --help = this will show all availble options for each command
2) man command name = displays manual page of each command

--> Basic commands in Linux:
1) ls = lists all content of the working directory
2) ls -l = long lists the working directory
3) ls -a = lists the directory including hidden files and directories
4) ls -t = lists the directory according to time frame we can see latest modified/created files at the top of the list by using this command
5) touch = create blank file
syntax: touch [filename/path]
6) mkdir = creates blank directory
syntax: mkdir [directory name/path]
7) rm = removes file
syntax: rm [filename/path]
8)rmdir = removes blank directory
rmdir [directory name/path]
9)rm -rf = forcedfully remove file or directory
rm -rf [file/directory name/path]
10) cat = read file content on terminal
11) head = read first 10 lines of file on terminal
12) tail = read last 10 lines of file on terminal
13) echo = insert some text string into some file or terminal.
 

we have a one tool before ssh named -> talent -> they also work as a ssh but when they create network in plain text
---------------------------------------------------------------------------------------------------
ssh
secure shell
program is used to take remote connection to any system

syntax: ssh [username]@[machine name(hostname)/ip address]
case-1: to get remote connection of any user without entering password

--> first generate keys in ssh
--> ssh-keygen 
--> newly created keys can be found in .ssh folder
then copy the created keys to that user of the machine whom we have to take remote connection.
by command:
ssh-copy-id remote username@remotemachine hostname/ip address
then do ssh to that remote user. 

case-2 : passphrase key generation: passphrase is password of the key to add an extra layer of security to the keys.

procedure for generation passphrase keys:
--> ssh-keygen
--> enter passphrase
--> enter passphrase again
now key with passprase would be generated 
--> next step is to send that key to that remote machine
--> ssh-copy-id remote username@remotemachine hostname/ip address
--> then do ssh to remote user you will notice that every time now we have to enter passphrase of key to enter into the server.

case-3 entering into remote server without entering passphrase of the key:

--> to overcome this situation we have to establish a process named as ssh-agent 
--> ssh-agent is the background process which enters the security credentials on behalf of the user so if we assign passphrase of the key to that agent we dont have to enter it at the time of the remote connection.
--> to enable ssh agent use command
eval $(ssh-agent)
then you will find that ssh agent process is running with some specific process id
--> next step is to assign passphrase to the ssh agent by this command
ssh-add .ssh/private key name
--> after adding security credentials to agent we can connect to remote machine without entering passphrase 


----------------------------------------------------------------------------------------------------
Non-interactive key (non-default)

step-1 generate non interactive key:
ssh-keygen -f .ssh/mykey enter

here f is used to forcedfully create non-default key 

step-2 copy this key to a remote user
ssh-copy-id -i .ssh/mykey.pub username@hostname

here -i is used for case ignorance of default key name.





















