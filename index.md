# Overview
- [ ] cleanup
- [ ] Make sections
- [ ] Cluster informations in the notes   

## Introduction
--- 
NOTES
---
- The reason why i changed from keepass to pass
- I started using NixOS more and more frequently
- Thought about leaving keepass behind and use pass in future to get my passwordmanagement right
---
RAW
---
Since I was more and more often in our office in Munich the last few weeks, I decided to tryout NixOS on an old MacBook Air. NixOS is a Linux distribution, that makes it easy to configure your machine over some nix-Configuration Files. I used the chance to cleanup some stuff, make some necessary backups and to give pass a try.Pass is [ pass.org? ] a lightweight tool, to handle your passwordmanagment on the command line.

## My problems with KeePass
---
NOTES
---
- What is KeePass?
- KeePass as something, that can solve a problem and did it for me the last year
- Problems:
	- I caught myself leaving the database open
	- Changing passwords felt hard and exhausting
	- KeePass made crazy stuff whenever you disconnected a second screen
- It felt uncomfy for me, as I got more and more comfortable using the command line
---
RAW
---
KeePass is a pretty good tool, to have at least a password management, that mostly nobody else in the real world has. Think about your passwords, there will be at least one, or was one, you can remember, because it is some simple setup of a name or a pin. Working with customer data, what we do nearly every day at mayflower, means, we have at least to try to keep this data save from being leaked, or fall into wrong hands. I recently started feeling more and more uncomfortable using KeePass. The main reason was my way of using it. The Problem was, that I still had the chance of doing it wrong. Whenever I needed a password, I started KeePass, look up the entry and copied and pasted it to the input form. That worked quit good in the first place. After some months, I caught myself more and more often without closing the database after I used a password. My thought was, even if I setup the best encryption for my KeePass-Database, someone standing next to me could easily get access. I needed to take myself the possibility to get lazy doing such a pity with such important things. Another reason was, that KeePass on Mac was unusable after disconnecting a second screen. KeePass always assumed, the second screen is still there and made it impossible to look up entries.

 
## Pass the commfy command line way
At Mayflower, we try to do our best to keep our data, and especially our customers data safe from being exploited. One way to keep the risk of getting hacked low is to use strong passwords and change them often. I recently started using more and more command-line tools and like how they do easy things, the easy way, without tons of way to configure. In the end I just want a password. And I really don't mind how my password looks like. The important thing about passwords, is that nobody else can ever know them. The best way to get a password, nobody else could ever imagine, is to use some kind of password generator. KeePass has a nice looking graphical UI, that is pretty useful, to configure special passwords, which neeild to exclude some chars. Pass on the other hand is just a command line interface, with the perfect balance of making it easy to update passwords or generate new ones within seconds. Another thing about pass is, that you can copy your pass words silently to your clipboard, for 45 Seconds. So, even if someone is in the room, he won't never ever see your password, if you manage to keep him away from your laptop the next 45 Seconds. My solution pass:



## Getting started with pass
---
NOTES
---
- What I want, having people using pass afterwards
	What would you need? 
		- How to get pass?
		- How to initialise password store
		- How to setup git integration
		- Inserting passwords
		- Retriving passwords and especialy the -c flag
		- Removing old passwords
		- List your passwords
- GPG topic as a second article after this one
- Thoughts about changing passwords frequently
---
RAW
---

To get pass visit https://www.passwordstore.org/ and follow the installation guide. On NixOS just add pass to your environment and rebuild your configuration. When your are done, you have to initialize a new password store by typing:

$ pass init <gpgid>

pass will automatically encrypt your password store with gpg and creates a ./password-store in your home directory. Now you can start inserting new passwords, or setting up git by using:

$ pass git init

After that, pass will keep track of what you are doing. Whenever you do some basic updating within your pass database, pass will update these change on your git working tree for you. So you can at least have a bit a track about your passwords, and what happened to from time to time. After that, you can start inserting passwords using:

$ pass insert Folder/example-host-password

I am looking for a consist way to handle my password-account. Feel free to contribute your way of handling. After that you can print your password to the console by using:

$ pass Folder/example-host-password

HopeFullySecretPassword

I mostly use pass with the -c flag, keeping the requested password 45 seconds on your clipboard. Not much time, but just enough, to don't leave the laptop for a coffee break or something else. Pass will synchronously track with git, that you have added "Folder/example-host-password" to your password store.Whenever you want to add a new password to your password-store and you don't want to think about how it looks like, at least it has a chance of not getting brute-forced within seconds, you can use:

$ pass generate -c Folder/example-host-password 64

The number says, how long the password should be. The -c Flag copies the new generated password directly to your clipboard and will also delete it after 45 Seconds again. This makes it easy to update old passwords with new, generated ones. With: 

$ pass rm Folder/password-name

you can remove old passwords.

A problem pass isn't solving is, that KeePass gave me the possibility to remind me after a bit of a time to change my password, that I never used. What I try, for me, even if it sound like dividing by zero, is to have inconsistencies within password naming convention, leaving it open how I will name them in the end. Maybe I will track them by date, or just switch between uppercase and lowercase, just to trigger myself, to change the rest, to get consistency into my password-store.

 

 

 

 

 

 

 

 

 


