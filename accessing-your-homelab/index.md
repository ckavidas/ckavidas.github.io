# Accessing Your Homelab Remotely

<!--more-->
![Banner](/images/categories/guide.png)

___

## Intro

In a [previous post](https://ckavidas.github.io/issessions-presentation-3-2020/) I shared some example use cases for your homelab. One of the main reasons for having a homelab was to practice your technical skills and learn new things but one of the other reasons was to set up "something cool" such as:


* Media servers like Jellyfin, Plex, Emby, Sonarr, etc.
* Game servers for games like Minecraft, CSGO, TF2 and some other games like Fistful of Frags which I have been playing lately.
* Setting up a NAS to backup files
* Self-Hosting applications such as:
	* A SearX privacy respecting search engine.
	* A Nextcloud instance to host files and provide a syncable calendar and contact list.
	* A file syncing service such as Syncthing
	

One of the questions I get often in regards to setting up a homelab is how to access these services remotely. While it doesnt seem likely that you are going to be accessing your homelab outside of your home any time soon, I thought it would be a good time to explain the various options. 

___
## Option 1: Port Forwarding and Dynamic DNS

In this configuration you are going to expose a port on your firewall/modem/router depending on what devices you have in your lab then use destination NAT to forward packets from that port to a specific IP/Port. To reduce the complexity of having to remember your public IP address you utilize a dynamic DNS service such as duckdns to point `<your_domain_name>.duckdns.org` to your public IP address. This DNS service is dynamic and requires that you periodically update what your public IP address is because it is subject to change as a typical home user. 

![Example-01: Port Forwarding and Dynamic DNS](/images/accessing-your-homelab/example-01.png "In this example port 8020 on the modem/router combo is being forwarded to port 12322 on the Jellyfin VM.")


This method gets the job done but it comes with some security concerns:
* In the event that a vulnerability in this service is exploited an attacker may be able to laterally move inside your homelab network or even worse your home network. 
* The service is made available to all users over the internet which may lead to denial of service attacks or brute force attacks.

A variation of this option is to instead port forward just a VPN service which you would then connect to wherever you are. The same security concerns exists as above, however you can now access a plethora of services while only exposing a single port which is likely to be secure if kept up to date. 

![Example-02: Port Forwarding and Dynamic DNS + Wireguard](/images/accessing-your-homelab/example-02.png "In this example a Raspberry Pi has been added with wireguard configured on it")

___
## Option 2: ZeroTier

In my [post](https://ckavidas.github.io/opensoc-ctf-08-2020/) about the OpenSOC competition that I recently participated in I talked a little about ZeroTier. Described on their site as a "smart Ethernet switch for planet Earth" what ZeroTier does is build an overlay network or a distributed switch network over the internet with everything encrypted. This can be acheived by hosting the ZeroTier controller yourself on a cloud VPS or by using their hosted ZeroTier controllers with free and paid options depending on your needs. I won't go over all the details of how ZeroTier works, the ZeroTier [manual](https://www.zerotier.com/manual/#1) does a much better job at that. I will however give you a basic rundown of how you would use ZeroTier.

* Create an account with My.ZeroTier.com (you can use your google account as an identity provider if you like.)
    * Note: Only one account is necessary, this account is going to build/manage the network.
* Once logged in, go to the Networks tab and create a network
    * From here you can configure the network addresses you want clients to receive, configure routes (if using a hub/spoke model) or build flow rules. 
* After building your network install the ZeroTier client on your devices (Windows/Mac/Linux/IOS/Android)    
* On the device you would join the network that you created
    * Example on linux you would run the command `sudo zerotier-cli join 123456789ABCDEF0` where `123456789ABCDEF0` is the network ID of the network you created. 

And that is it! at least from the client side. From the My.Zerotier page you can build complex access policies, configure role based access control and even mirror traffic to another source. You can also redirect traffic or segregate traffic using multiple networks. 

![Example-03: Building a network with ZeroTier](/images/accessing-your-homelab/example-03.png "In this example the Jellyfin VM has ZeroTier installed and both clients can communicate via the ZeroTier network.")

___
## Option 3: Tailscale

Tailscale is a service similar to ZeroTier with the aim of being simpler to use. From a technical perspective Tailscale uses Wireguard as a data plane (that being where packets are being sent) with their Tailscale software acting as the control plane (managing IP addresses and access control policies). The difference between Tailscale and Zerotier is that Tailscale is a mesh network meaning that all nodes are connected to each other directly and the Tailscale software determines how a given peer can communicate to the other peers it is connected to. Tailscale also comes with some interesting features for example it has support for multiple SSO providers such as Google, Okta, Office 365, Azure Active Directory, etc. Tailscale is free for personal use with up to 100 devices. One of the disadvantages is that this free use is tied to a single SSO account, meaning that if you wanted to share a Homelab service with another person you would have to make a Google account for example and share this login with this other person. If you wanted to acheive this without sharing an SSO account it would cost $10 a month for each user. 

![Example-04: Building a network with Tailscale](/images/accessing-your-homelab/example-04.png "In this example the Jellyfin VM has Tailscale installed and both clients can communicate directly via a peer to peer network.")

___
## Option 4: Custom Hub/Spoke Network

Lets say you wanted all the features that ZeroTier provided you but you wanted to run it yourself. You could for example purchase a virtual private server from a cloud provider and configure Wireguard on this machine which will route between your device and the homelab services (or homelab network). From there you can configure a complex firewall policy as well as a dynamic DNS service or a domain name if your VPS has a static IP address. 

![Example-05: Building a custom hub/spoke network](/images/accessing-your-homelab/example-05.png "In this example both the Jellyfin VM and the laptop have a peer to peer connection to the VPS which routes their traffic.")

___
## Conclusion

In this article I demonstrated four options for you to connect to your homelab remotely. The question you might be asking is: "What is the best option" to which I would say it all depends on your needs.

* Would you like the entire internet population to access your service?
    * Consider using example 1 where we port forwarded the Jellyfin service.
* Would you like a select few individuals to access your service?
    * Consider using:
        * Zerotier especially if you would like to play around with flow rules.
        * Tailscale if these select few individuals are willing to pay $10 a month OR if everyone is willing to share a google account.
        * Custom hub/spoke network if you would like to play around with iptables rules. 
* Would you (and only you) like to access your service(s)?
    * Consider using tailscale for simplicity's sake. 
