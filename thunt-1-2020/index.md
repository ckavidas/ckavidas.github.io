# Threat Hunting Workshop 1/18/2020

<!--more-->
![Banner](/images/thunt-1-2020/thunt_1-2020_banner.png)

___

## Intro

Hello Friends and Happy New Year!

On Saturday January 18th 2020 I participated in a threat hunting workshop run by __Black Hills Information Security__.

One of the infosec topics that I am interested in is threat hunting. The idea of searching for “suspicious activity” or indicators of compromise proactively. I was excited to find out that BHIS and Active Countermeasures were running a threat hunting training event for free. The course focuses primarily on network traffic analysis which is great for me because I am currently in a [course](https://ict.senecacollege.ca/course/spr600?q=course/spr600) focused on intrusion detection where packet analysis is important.
___
## Review

My experience was great!

I appreciated that [@Chris_Brenton](https://twitter.com/chris_brenton) focused a lot on process. A lot of times when there is a webinar the hosts focus extensibly on how the task is done from a technical standpoint without explaining what we are trying to do and why we are doing it. The tools change from workplace to workplace but the process almost always stays the same. There were technical difficulties and at one point the stream died but at the end of the day we all survived. They are running the same workshop in April and I recommend everyone check twitter and participate.
___
## Lessons Learned:

* A practical process flow of network based threat hunting (looking for persistent connections, automated beacons etc.)
* Detecting DNS tunneling / DNS C2 traffic
* SSL Fingerprinting with JA3
* How to analyze zeek capture files from the linux command line.
* How to analyze zeek capture files using rita.
___
## Example Lab Exercises:

### Finding Long Connections:

* The first step is to find out how long the capture file is. You can either use the __capinfos__ command or in the event that you do not have the package the same can be acheived using __tcpdump__ and __awk__.
```Bash
capinfos -ae example.pcap
tcpdump -tttt -n -r example.pcap | awk 'NR==1; END{PRINT}'
```
* The second step is to use __bro-cut__ to extract the source and destination IPs as well as the duration. In a zeek log those fields are __id.orig_h__, __id.resp_h__ and __duration__. Once you have extracted these fields you can pipe the output into sort and grab the first 10 lines using head.

```Bash
cat conn.log | bro-cut id.orig_h id.resp_h duration | sort -k3rn | head
```
![Grab the longest 10 connections](/images/thunt-1-2020/thunt-ex-1.PNG)
___
### Finding Potential Beacons
* A beacon is a host machine reaching out to a command and control server. A good first step in trying to find potential beacons is to look for source/destination IP pairs and get a count of how many packets were sent. The relevant fields for this would be source IP and destination IP but you should also consider size. A beacon will have a lot of packets but not a lot of bytes being transmitted (most of the packets will just be heartbeat). The first command I would use is to find the largest counts:
```Bash
cat conn.log | bro-cut id.orig_h id.resp_h | sort | uniq -c | head
```
![Find the largest counts](/images/thunt-1-2020/thunt-ex-2-s1.PNG)
* This will tell us how many connections were made for each pair. The top 3 results are the ones that need more investigation so I will check the size. For example lets use that first conversation with __192.168.88.2__ and __165.227.88.15__. We need to use __datamash__ to perform aggregate functions so we need to use __grep -v__ to remove lines that are empty as well as lines that have a - for data size.
```Bash
cat conn.log | bro-cut id.orig_h id.resp_h orig_bytes | grep 192.168.88.2 | grep 165.227.88.15 | sort | grep -v '^$' | grep -v '-' | datamash -g 1,2 max 3
```
![Investigating the connection between 192.168.88.2 and 165.227.88.15](/images/thunt-1-2020/thunt-ex-2-s1.PNG)
* As we can see __165.227.88.15__ has sent __3673 bytes__ and __192.168.88.2 has only sent 262 bytes__. When a pair of hosts send __108858 packets__ but only __3935 bytes__ of total data that leads me to beleive that these may be beacons which require additional investigation.
___
### Searching for command and control over DNS using RITA.
* __RITA (Real Intelligence Threat Analytics)__ is an open source framework for network traffic analysis from Active Countermeasures. RITA reads Bro/Zeek logs and has built in functions to do some of the tasks we worked on in the workshop (searching for beacons, dns tunneling etc.) RITA is much easier to use than the linux commands we were gluing together. 
* For example here is how you would search for DNS command and control or DNS tunneling using RITA.
![Finding the domains with the most requests](/images/thunt-1-2020/thunt-ex-3-s1.PNG)
* Lets drill down and see what some of these requests are going to __r-1x.com__
![DNS requests going to r-1x.com](/images/thunt-1-2020/thunt-ex-3-s2.PNG)
* As we can see the domain names being resolved are garbage, most likely command and control traffic.
* One added benefit of using RITA to analyze your Zeek logs is that it stores the Zeek logs in a database (mongodb) as opposed to reading the Zeek logs.
___
## Future works / ideas I would like to explore:
* Since the workshop focuses on network based threat hunting, I would like to explore EDR based threat hunting in the future.
* I would like to learn more about RITA, for example is it possible to build your own functions.
___
## Closing Remarks
I would like to thank the group over at __Black Hills Information Security__ for putting this workshop together. I highly recommend anyone interested in cybersecurity take a look at their youtube channel.
* [__@Chris_Brenton](https://twitter.com/Chris_Brenton)
* [__@strandjs](https://twitter.com/strandjs)
* __Shelby and Bill Sterns__ (Could not find their social links)

