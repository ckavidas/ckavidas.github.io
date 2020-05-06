# Intro to CTF presentation @ CSHUB 3/13/2020

<!--more-->
![Banner](/images/categories/presentation.png)

___

## Intro

On Saturday January 25th 2020 I participated in __CyberSci__ which is a CTF competition for College/University students. Seneca College did very well at this competition (my team got 4th place, my class mates got 1st). After the event I networked with some students who are part of the __York University Computing Students Hub__. They mentioned that they were interested in learning more about CTF competitions as this was one of their first CTF competitions. I agreed to help out and on March 13th 2020 I presented to the club an introduction to CTF competitions.

Unfortunately due to concerns surrounding Covid 19 attendance was low, so I will summarize the presentation here.
___
## Why do a CTF competition?

A CTF competition is a great place to meet new people (who are most likely in tech), have fun solving challenges and make learning new skills fun. Whats in it for you is an afternoon of fun, often times with free food and a relaxing environment where you can challenge yourself at your own pace. 

Some might be scared off because they think they are not good enough, I would encourage those people to just "dive in" and go into the competition with the mindset that they are here to have fun. You might not place well but if you continue to develop your skills you will get better!
___
## What is a CTF competition?

Short answer: Gamified computer problem solving.

In CTF competitions you compete with other groups of people solving computer challenges. There are two main styles of CTF competitions;
* The __Jeopardy__ style competition: Solve challenges across many categories for increasing points based on difficulty
* The __Attack and/or Defend__ style competition: Use the skills you have developed to attack a box, sometimes comes with a defend component.

The most popular style is the Jeopardy style competition, it has the lowest barrier of entry due to the large amount of challenges available to you. Some Jeopardy style competitions have incentives to complete challenges fast, making points for challenges worth less and less as more people solve them.

### Types of Challenges
An example of some of the challenges you might find:
* Linux shell challenges
    * Example: Brute forcing a password protected zip, finding the flag in a file with ~10k lines.
    * Tools: john, hashcat, grep, awk, strings etc.
* Cryptography challenges
    * Example: Flag is encrypted using ROT13
    * Tools: tr, openssl
* Steganography challenges
    * Example: Flag is stored in an image or a mp3
    * Tools: exifdata, stegotool, xxd, strings etc.
* Digital forensics
    * Example: Flag is stored in a file in a 1 gb disk image.
    * Tools: Autopsy, scalpel, foremost, xxd, etc.
* Reverse engineering / Binary exploitation
    * Example: Flag is printed if you enter the correct password or password is stored in /root/flag.txt and the binary provided to you has a SUID bit set.
    * Tools: Gdb, IDA pro, pwntools, strings, objdump
* Web hacking challenges
    * Example: Use SQL injection to get the flag from the table flags or the flag is printed back if your username is john (where you don't know john's password)
    * Tools: Burp suite, Zap proxy, sqlmap, curl
* Packet analysis challenges
    * Example: Flag is stored in a packet inside of a packet capture (either as TCP data, UDP data or maybe a specific protocol like DNS or HTTP)
    * Tools: Wireshark, tshark, ngrep, tcpflow, strings
* Programming challenges / Source code challenges
    * Example: You have a python script that checks for a password, the password is encrypted already, analyze the code and reverse engineer what the password is. The password is the flag.
    * Tools: Your favorite text editor :sunglasses:
___
## How to practice or participate?

The best way to practice is to just start playing!

### Some places you can practice:
* Wargames like  overthewire's [Bandit](https://overthewire.org/wargames/bandit/) and [Leviathan](https://overthewire.org/wargames/leviathan/)
* Online CTF's like [RingZer0 CTF](https://ringzer0ctf.com/) or [picoCTF](https://picoctf.com/)
* Vulnerable applications like [Juice Shop,](https://owasp.org/www-project-juice-shop/) [Webgoat](https://owasp.org/www-project-webgoat/) and [Google Gruyere](https://google-gruyere.appspot.com/)
* Vulnerable Boxes on [Vulnhub](https://www.vulnhub.com/) or [Hack the Box](https://www.hackthebox.eu/)
* Online CTF platforms like [CTFtime](https://ctftime.org/) will show you upcoming live CTF competitions that you can participate in from home.
### Some places you can find CTF competitions:
* Security conferences like Hackfest and Northsec
* Various Bsides conferences
* Some schools run CTF competitions (for example Sheridan College)
* A special mention goes to Tracelabs for their Missing Persons OSINT CTFs
* In person CTF competitions are also advertised on CTFtime
___
## Closing Remarks
As the former president of Seneca College's Capture the Flag club I would like to thank __York University__ and the staff at __CyberSci__ for putting on a great competition. I would also like to thank the __York University Computing Students Hub__ for inviting me to present. Unfortunately due to the Covid 19 situation the attendance was not as high as we would have liked but those that came out had fun.
