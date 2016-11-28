# Overview
- [X] cleanup
- [X] Make sections
- [X] Cluster informations in the notes   

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
Since I was more and more often in our office in Munich the last few weeks, I decided to tryout NixOS on an old MacBook Air. NixOS is a Linux distribution, that makes it easy to configure your machine over some nix-configuration Files. I used the chance to cleanup some stuff, make some necessary backups and to give pass a try. Pass is a lightweight tool to handle your passwordmanagment on the command line, you can find more information about it at https://www.passwordstore.org.

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

```shell
$ pass init <gpgid>
```

Pass will automatically encrypt your password store with the gpgid and create a ./password-store in your home directory. Now you can start inserting new passwords, or setting up git by using:

```shell
$ pass git init
```

After that, pass will keep track of what you are doing. Whenever you do some basic updating within your pass database, pass will update the changes on your git working tree. So you can at least have a bit a track about your passwords, and what happened to them from time to time. After that, you can start inserting passwords using:

```shell
$ pass insert service-you-use-and-have-a-password-for
```

Listing all your services in your password-store is done by using: 

```shell
$ pass ls
```
You could also do something like: "pass insert FOLDER/service". This can be useuful to group your passwords for different customers, in private and business or whatever fits your needs. Whenever you want to retrieve your password from your password store, you just have to type:

```shell
$ pass service-you-use-and-have-a-password-for
```

This will print your password to the stdout and you could copy it to your clipboard. A better way is to use the -c flag:

```shell
$ pass -c service-you-use-and-have-a-password-for
```

This will silently copy your password to your clipboard, ready to be pasted. The best about the -c flag is, that your password will be deleted after 45 seconds from your clipboard. Not much time, but just enough to say to oneself, I could at least wait until the password is removed before getting myself a coffee. 

Pass also lets you genrate new passwords. Being honest, there is no need for you, to ever see a password, or that you have one you can remember. Using a password store keeps your head free of lots of passwords and makes it easier for you to have passwords not being brute forced. Generating new passwords in pass works as follows:

```shell
$ pass generate FOLDER/service-you-want-a-new-password-for 64
```

Deleting them works like expected: 

```shell
$ pass rm FOLDER/password-you-are-not-using-anymore
```

Giving the generate command the -c flag writes your new password directly to your clipboard again. The 64 stands for the length the generated password will have in the end. You can just paste it to the new service you are subscribing to. This can be useful to have at least passwords with a minimum strength against brute force attacks.
Having strong passwords is one way to protect your data and especialy your customers data. Another thing you should do is to change your passwords every once in a while. KeePass had a way to set an expirationdate to your passwords. A functionality, that is pretty nice, if you use it. I never did and thought, I would never use it. The important thing for me in frequently changing passwords is doing it witch ease. Pass feels easy to use and keeps an eye on the things, KeePass didn't for me. 
If you have any experiences with pass, or have any passwordmanager worth giving a try, let me know in a comment. 

EOF

