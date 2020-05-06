# Threat Defense Workshop with Trend Micro and DC416

<!--more-->
![Banner](/images/categories/workshop.png)

___

## Intro

On Saturday April 25th 2020 I participated in a threat defense workshop run by __Trend Micro__ and __Defcon Toronto__.

I was excited that the staff at __Defcon Toronto__ and __Trend Micro__ managed to keep the event going in light of the Covid 19 situation. I was not prepared for a CTF like competition but I rose to the occasion and worked with my team to finish in the top 10. 
___
## Review

It was a morning/afternoon of fun!

While I would have preferred a little more of a walkthrough of using __Trend Micro Deep Security__ we all had fun exploring and trying to figure things out. Based on my experience Deep Security is a feature rich tool which I only scratched the surface of in this workshop. Some of things I did in this workshop were:

* Find security events for a given host in Deep Security.
* Scan hosts for malware, investigate malware identified.
* Investigate firewall logs to identify command and control servers.
* As well as some CTF like challenges (discover the destination port for the C2 server, crack a zip file, etc.

Out of respect for the organizers and Trend Micro I will not post any guides or solutions to any of the challenges.
___
## Exploring Deep Security After the Workshop

Thankfully the organizers left all the materials online for one extra day so I can explore some of the bells and whistles of Deep Security. I am going in with the mindset that I am the one configuring Deep Security for an organization.


### Adding a computer to Deep Security

Accessing the __Computers__ page you can manage computers that are part of the Deep Security ecosystem. This includes an individual host or virtual machine, an AWS/Azure/vCloud/vCenter account or an Active Directory forest. There are three options when adding a computer:

![Trend Micro Deep Security Computers Tab](/images/threat-def-dc416-4-2020/computers-tab.png "Computers Tab")

* Server Initiated (Added through the computers page)
* Agent Initiated (Added by the agent using the agent software which you can download from Deep Security)
    * This can be disabled by Unchecking or restricting the __"Allow Agent-Initiated Activation"__ setting.
* Deployment scripts which can then be distributed using your configuration management suite of choice (Ansible, Chef, Puppet, etc.)

![Trend Micro Deep Security Deployment Script](/images/threat-def-dc416-4-2020/deployment-script.png "Example Linux Deployment Script, the lower 1/2 of the page is the script itself.")

### Forwarding Deep Security Events to existing infrastructure.

Since it is entirely possible that you already have security infrastructure before you adopted Deep Security there are options to forward Deep Security events via:
* Syslog (to either a syslog server or perhaps a logstash pipeline)
* AWS Simple Notification Service
* SNMP to something like Zabbix or Nagios

![Trend Micro Deep Security Forwarding Events](/images/threat-def-dc416-4-2020/forwarding-events.png "Forwarding Events Window")

### Building policies and rules for your computers.

The __Policies__ tab shows the different rules, lists (directories, IPs, Ports, etc.) and other settings that can be applied to a policy. This policy can then be applied to specific computers in your environment.

The different rule categories are:

* Firewall Rules
* Intrusion Prevention System Rules
* Integrity Monitoring Rules (File, Registry or custom rules using XML)
* Log inspection rules (Configure what service logs get ingested)
* Application Control Rules (Control what applications can run and under what conditions)

An example policy could be using Deep Security to configure the firewall as opposed to using group policy on windows hosts. Or logging file integrity changes for a specific application service directory.

![Trend Micro Deep Security Firewall Rules](/images/threat-def-dc416-4-2020/firewall-rules.png "Firewall Section of Policy Rules")

___
## Future works / ideas I would like to explore:
According to the documentation there is an API that can be used to operate essentially all of Deep Security. It even comes with a library you can use in Python, Java Script and Java. As I develop an understanding of security automation use cases I could see this being a useful tool.
___
## Closing Remarks
I would like to thank the group over at __Trend Micro and Defcon Toronto__ for putting this workshop together. If you live in the Greater Toronto Area I highly recommend you join the [Defcon Toronto](https://dc416.com) community. I would also like to give a special thanks to __Thomas__ and __Majid__ for being great team mates, even though we were short one person we did very well.

