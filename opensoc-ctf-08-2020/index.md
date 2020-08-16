# OpenSOC CTF with Recon Infosec

<!--more-->
![Banner](/images/opensoc-ctf-2020/banner.png)

___

## Intro

On 08/08/2020 and 08/09/2020 I participated in the __OpenSOC CTF__ run by [__Recon Infosec__](https://twitter.com/recon_infosec). OpenSOC is an open source SOC cyber range running the following software suites:

* [Graylog](https://www.graylog.org/) as a SIEM 
	* [Kibana](https://www.elastic.co/kibana) was also offered as an optional frontend
* [Moloch](https://molo.ch/) as a network security monitoring solution
	* [Suricata](https://suricata-ids.org/) for network security alerts
* [Zeek](https://zeek.org/) for networking data
* [OsQuery](https://osquery.io/) for host information
* [Velociraptor](https://www.velocidex.com/) for host visibility
* [Thinkst Canary](https://canary.tools/) for Canary Tokens


The CTF is designed to help you learn about the amazing tools in the OpenSOC environment and show you what you can do without the expensive tools. There are storylines that you follow answering questions about what is going on through the usage of the tools listed above. Most storylines were around 70+ questions but you only get the questions one at a time. 

___
## Review

It was two days full of fun!

There were a handful of technical difficulties and the first day did end early as a result but it gave us an opportunity to stretch our legs. Most of the tools worked flawlessly with the exception of the main one (Graylog/Kibana) which got hammered the hardest throughout the event. One of my regrets was that I never got a chance to use Velociraptor or Thinkst Canary during the event. One of the main reasons for that was that we were able to find just about everything using just Graylog/Kibana, Moloch and OsQuery. The other challenge was that we needed to submit a ticket to get Velociraptor queries done which is hard when you aren't familiar with the tool.

The one question at a time method worked very well for our team, at some points we were answering questions before one of us could finish reading the question. It didn't hurt that I was already familiar with some of the tools (mainly Graylog and Kibana) as well as having a good idea of where to look for most challenges. Our team finished the second day in __29th place__ but I only have a screenshot from before we all decided to go to bed.

![Opensoc-Scoreboard-8-8-2020](/images/opensoc-ctf-2020/score.png "Our rank before we decided to go to bed.")

___
## Tips for the competition

If you ever get a chance to attend an OpenSOC event I highly recommend it. Here are some tips I can give for solving the challenges. Out of respect for __Recon Infosec__ I will not offer any spoilers.

#### TAKE NOTES!

* At the start of day 2 we didn't have notes and we spent at least an hour trying to continue the storyline we were on.
	
#### Use the surrounding events function in Graylog/Kibana

* Lets say the story up to this point shows that the attackers ran mimikatz on the machine. The next question might ask you to figure out where the attackers laterally moved to from there.
* Using the surrounding events function on the mimikatz event will show you events that happened shortly after. 
* You can filter the related events down to show you only __sysmon event ID 3__ to hunt for network connections. 
* You could also hunt for login events such as __event ID 4624__ to try and find out what user was compromised etc.
	
#### Use the saved searches function in Kibana

* There are types of logs you are going to be searching from constantly (example: windows logs or zeek conn.log etc.)
* You can save your search and open it up very quickly instead of trying to build queries from scratch.
* Unfortunately this was lost on the second day when they reset Kibana and made it read only.
	
#### Use the search bar for consistent items and the search box for unique items.

* In Kibana (sorry I don't have a screenshot of this) there is a search box and undernath that there is a bar of search terms. You could for example pin items consistent to the story line (file=winlogbeat, host=hr-12345, event_id=1, etc.) then use the search box to search for "malware.exe" to get very quick results.
* You can even have multiple items in the bar and toggle them on and off (example: a box for event ID 1, 3, 4624, etc.)
	
#### Use Virustotal!

* There were times in the competition where you would be asked specifics about a binary file on a given system. (Example: SHA256 hash or the name of this file)
* One option is to use OSQuery or Velociraptor to obtain this information but my prefered method was to use the MD5 hash obtained from sysmon logs and virustotal. 
	
#### Use OSQuery to get persistence data

* As I became familiar with the structure of the storylines I knew in the future I would get questions about persistence mechanisms.
* You can use OSQuery to obtain startup information, scheduled tasks and even WMI persistence data such as __filters, consumers and filter to consumer bindings__

___
## Future works / ideas I would like to explore:

* The competition environment made use of [__Zerotier__](https://www.zerotier.com/) to build a virtual network for us to access the tools/scoreboard. I have read the manual for Zerotier and hope to learn how to use it so I can share it with all of you.
* I would like to build my own OpenSOC environment but with some exceptions:
	* I personally prefer Kibana to Graylog
	* I would like to include [__Wazuh__](https://wazuh.com/) which is a host-based intrusion detection system.
	* I would like to build a Zeek Hunting dashboard in Kibana similar to what [__Security Onion__](https://securityonion.net/) has.
* Adversary simulation is something that is well documented, tools like [__Atomic Red Team__](https://github.com/redcanaryco/atomic-red-team) and [__Caldera__](https://github.com/mitre/caldera) exist for example. Simulating regular activity on the other hand is not something I have found a solution for. I will need to pick some people's brains to get an idea on how to do that without it being detectable by the log. (Imagine if all legitimate activity on some host was spawned by abc.exe, you could filter out all events where the parent process is abc.exe)

___
## Closing Remarks
I would like to thank the group over at [__Recon Infosec__](https://twitter.com/recon_infosec) for putting this event together, most notably [__@eric_capuano__](https://twitter.com/eric_capuano) and [__@shortxstack__](https://twitter.com/shortxstack). If you ever see an OpenSoc event happening, drop everything and go for it. I would also like to give a special thanks to my team mates __[Haydzx](https://twitter.com/haydnjohnson), TDotDavid and Buz__  for being excellent team mates, even though we were short one person we did incredibly well.

