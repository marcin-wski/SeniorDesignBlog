# What is DNS

The Domain Name System (DNS) is essentially the phonebook of the Internet and allows us, humans, to easily navigate to different servers, websites, and other online resources. To access information online, like csun.edu or dmv.ca.gov, we need those domain names, otherwise we would have to remember each IP address, where IP stands for Internet Protocol, for each server, each website we want to access.

Each device or other resource connected to the Internet has a unique IP address which other machines use to find the device. Our browser upon entering the name of the website reaches out to the DNS server it has configured to ask for the IP address of the resource we attempt to access and the DNS server checks its records for that specific IP and translates it so that our browser can use it. Essentially the DNS servers eliminate the need for humans to memorize IP addresses such as 192.168.1.1 (in IPv4), or more complex newer alphanumeric IP addresses such as 2400:cb00:2048:1::c629:d7a2 (in IPv6).

# How does DNS work

The process of DNS resolution involves converting a hostname or domain name (such as csun.edu) into a browser-friendly IP address (such as 130.166.72.60). An IP address is given to each device on the Internet, and that address is necessary to find the appropriate Internet device - like a street address is used to find a particular home or a phone number to find a particular business in a phone book.

When a user wants to load a webpage a translation must occur between what a user types into their web browser (csun.edu) and the machine-friendly address necessary to locate that site (130.166.72.60)

For the web browser, the DNS lookup occurs “behind the scenes” and requires no further interaction from the user’s computer apart from the initial request. That is unless the DNS server is wrongly configured on your own computer and you are asking a DNS server that cannot connect to the wider Internet

# Step of a DNS lookup

- A user types ‘example.com’ into a web browser and the query travels into the Internet and is received by a DNS recursive resolver.
- The resolver then queries a DNS root nameserver (.).
- The root server then responds to the resolver with the address of a Top Level Domain (TLD) DNS server (such as .com or .net), which stores the information for its domains. When searching for example.com, our request is pointed toward the .com TLD.
- The resolver then makes a request to the .com TLD.
- The TLD server then responds with the IP address of the domain’s nameserver, example.com.
- Lastly, the recursive resolver sends a query to the domain’s nameserver.
- The IP address for example.com is then returned to the resolver from the nameserver.
- The DNS resolver then responds to the web browser with the IP address of the domain requested initially.
- The browser makes a HTTP request to the IP address.
- The server at that IP returns the webpage to be rendered in the browser.

# Why is DNS important

As stated above the DNS is necessary for us to avoid memorizing hundreds or thousands or IPs for every resource we want to use. Without it to go to csun.edu we would need to know the precise IP of the CSUN web server hosting csun.edu, which now appears to be 130.166.238.195. Can you get to csun.edu using just the IP? Yes, but why?

When a DNS "goes down" and becomes inaccessible (like we've seen a few times in recent history) the network traffic essentially stops. Browsers cannot access online resources, we cannot "find" the websites we want to reach, businesses cannot operate properly as network traffic does not reach their websites, their servers, their phones etc. To avoid that many large businesses have their own internal DNS servers that are used to route the traffic only internally throughout the company so that even when there is a major issue on the Internet the internal functions of the company do not stop. This helps those businesses to avoid phones not able to connect to the network, IT departments not able to get to their monitoring tools and their internal servers, applications still working etc.

Aside from DNS servers being inaccessible there is another risk of malware pointing your searches to a wrong DNS server, set up by malicious agents (ie. hackers). For example someone can point your computer to a fake DNS server that has IP addresses that look and act like the site you’re trying to access but actually aren’t that site at all. For example you might type into your browser the name of your bank to check your finances and the DNS server takes it to a wrong, malicious site. It looks the same, it asks you for your password just like your actual bank site, but when you put your credentials in the people behind it take your credentials, log into your actual bank... and all your money now belongs to them.

Another issue is "DNS replication." For internal DNS servers outside hackers don't necessarily know what is on your internal network and even if they do have accesses to the network it might take them a very long time to map it properly. For attacks like that every second counts, and so to make their lives easier the attackers will first identify the internal DNS server and then attempt to replicate your DNS zones. Through that replication (if successful) the attacker now is in possession of all your internal IP addresses and domain names, and is able to get to these sites or server a lot quicker

# Some of the common attacks involving DNS
## DNS spoofing/cache poisoning

This is an attack where forged DNS data is introduced into a DNS resolver’s cache, resulting in the resolver returning an incorrect IP address for a domain. Instead of going to the correct website, traffic can be diverted to a malicious machine or anywhere else the attacker desires; often this will be a replica of the original site used for malicious purposes such as distributing malware or collecting login information.

## DNS tunnelling

This attack uses other protocols to tunnel through DNS queries and responses. Attackers can use SSH, TCP, or HTTP to pass malware or stolen information into DNS queries, undetected by most firewalls.

## DNS hijacking

In DNS hijacking the attacker redirects queries to a different domain name server. This can be done either with malware or with the unauthorized modification of a DNS server. Although the result is similar to that of DNS spoofing, this is a fundamentally different attack because it targets the DNS record of the website on the nameserver, rather than a resolver’s cache.

## Random subdomain attack

In this case, the attacker sends DNS queries for several random, non-existent subdomains of one legitimate site. The goal is to create a denial-of-service for the domain’s authoritative nameserver, making it impossible to lookup the website from the nameserver. As a side effect, the ISP serving the attacker may also be impacted, as their recursive resolver's cache will be loaded with bad requests.
