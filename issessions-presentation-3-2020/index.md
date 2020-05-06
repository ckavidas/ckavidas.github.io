# A little something about homelabs @ ISSessions 3/27/2020

<!--more-->
![Banner](/images/categories/presentation.png)

___

## Intro

Sheridan College's __ISSessions__ club is a bi-weekly (during the school year) meetup. The meetup brings students from Sheridan's information security program as well as alumni together to talk about security. Luckily they sometimes stream their meetups on Youtube which allows me to participate.

The meetups follow a specific process:
* Anouncements with their president ([@louailoopdidoop](https://twitter.com/louailoopdidoop))
* News with [@NickInfoSec](https://twitter.com/NickInfoSec) and Adam
* A project den segment hosted by various individuals talking about projects they are working on.
* A networking component at the local bar or in our case because of quarantine: Kahoot quizzes & Jackbox Party Games

Due to the Covid 19 situation, [@louailoopdidoop](https://twitter.com/louailoopdidoop) asked me if I could help them with the project den segment as the scheduled presenter could not attend. I was hesistant at first but I wanted to help out so I accepted. There were some technical difficulties during the presentation which is why I will summarize the presentation in a blog format. 

You can also find the video  on the [ISSessions Youtube Channel](https://www.youtube.com/watch?v=KRTICiIjSCQ)
___
## What is a Homelab?

The best definition I could find is:
* A safe place for you to experiment with IT stuff (Hardware and Software) example:
    * Servers (Rackmount or otherwise, configuring RAID, etc.)
    * Networking equipment (Routers, Switches, Firewalls, IDS/IPS)
    * Platforms and software packages (Testing ESXI versus Proxmox, learning new technologies etc.)

I think this definition is ok, I would say more importantly is that it enables __project based learning__. Sometimes a project is needed to apply the skills you are developing and retain that knowledge. Another reason might be just to set up something cool at home. For example why pay for spotify when you can run your own music streaming service?
___
## How much does it cost?

Short answer: Depends on your needs.

Some people are part of the school of thought that a homelab should comprise of old server equipment, some of are the school of thought that you should make the most with what you got. I can see a benefit in both, if "money was no object" I would build a homelab with real server equipment. But as a student it might be best to explore cheaper alternatives.

The basic components of a homelab are just two items:
* A "server" (it could just be a dedicated computer for hosting your services)
* A separate network from the rest of your home network.

### Server equipment examples:
Rackmount server:
* Dell R720 servers (used on ebay for anywhere from $700-$1500 depending on configuration)
Tower servers:
* Dell PowerEdge T620 (priced similar to the R720)
* Some people opt to build their own tower server, there are two routes:
    * Buy the components of a tower server such as a motherboard (likely from super micro), the CPUs and memory from ebay. I personally went down this path and built two servers each costing aproximately $300 barebones (without factoring in storage)
    * Buy into the more recent Intel Core I7/AMD Ryzen systems and build a "gaming PC without an expensive GPU" and use that as a server. It is a viable option, you lose some server features such as ECC Registered memory but again it all circles back to what your needs are.

Switches:
* TP-Link JetStream 24-Port Gigabit Managed Switch 4 SFP ports (New on ebay for $130-180)

Routers:
* Most recommend either installing pfsense on a small form factor PC such as the HP T610 or building your own pfsense box using the lowest power CPU you can find that supports AES-NI (example: Intel Pentium G4400 or AMD Athlon 3000g). Another option is to buy older generation PFSense routers on ebay or buy PFSense routers off Ali Express. I am personally exploring the DIY track.

### Budget Homelab
What you need is entirely dependent on what it is that you want to do. Here are some examples of equipment that can satisfy your needs while costing significantly less.
* Dell Optiplex 7020 desktops or small form factor machines work great as a budget server.
* The Intel NUC is a low power but very powerful device, it is on the expensive side however.
* Raspberry Pi and Odroid system-on-a-chip devices work great as either small linux boxes or as clusters.
* Various wireless routers that you can find at your local thrift store may be compatible with custom firmwares such as Open-WRT, DD-WRT or Tomato. These firmwares may give you some of the networking features you are looking for such as vlans, port mirroring or VPN. (Your mileage may varry on that last one)
___
## Homelab Software
The hardware of a homelab is only 1/2 of the work, the second part is setting up the software.
Virtualization:
* VMWare ESXI (The most popular hypervisor with homelab users, some features are paid only.)
* XCP-NG (Open source XEN server, rising in popularity.)
* Proxmox (Open source KVM based virtualization software, my personal favorite.)
* $Your-favorite-linux-distro + KVM (for example: Centos + KVM)

Container software:
* Docker for micro services
* LXC/LXD for micro system virtualization

Networking software:
* Pfsense (The most popular open source firewall distribution, feature rich)
* VYOS (Software router, has a cisco like interface so if you are used to that you will fit right in.)
* Security Onion (Network Sensor and analysis OS, comes with snort/suricata/zeek/wazuh and ELK stack.)
___
## What do people use their homelab for?
Here are some of the top homelab uses that I found on reddit.
* VPN Services (OpenVPN, Wireguard)
* Media Servers (Plex, Emby, Sonarr, Airsonic etc.)
* Game servers (Minecraft, Counter Strike Global Offensive, Team Fortress 2, etc.)
* Learning new technologies (Kubernetes, OSQuery, Zeek etc.)
* Development environment (create a development environment for project based learning)
* Backup server

___
## Some things that I run in my homelab:
* VMs from my classes, CTF club stuff, etc.
* Security test network (Windows server, Windows 10, ELK stack, etc.)
* Freenas
* Airsonic (Music streaming service)
* Pihole (ad-blocking DNS server)
* Wireguard VPN (main VPN)
* OpenVPN (failover VPN)

___
## Closing Remarks
I would like to thank everyone who attended the meetup and survived the technical difficulties. __ISSessions__ is a great meetup and I wish I could attend every time (unfortunately the Trafalgar campus is too far to make that trip.) I would like to give a special thanks to:
* [@louailoopdidoop](https://twitter.com/louailoopdidoop) for inviting me to speak
* [@NickInfoSec](https://twitter.com/NickInfoSec) for changing the slides for me when technical difficulties came up.
* And the rest of the __ISSessions team__ for helping get everything set up and hosting the games after the presentation.
