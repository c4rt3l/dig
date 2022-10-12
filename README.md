What is DIG command?
DIG command (Domain Information Groper command) is a network tool with a basic command-line interface that serves for making different DNS (domain name system) queries. You can use the DIG command to:

Diagnose your name servers. Check all of them or each individual server and their response.
Check all of the available DNS records or individual DNS records and their parameters.
Trace IP addresses and see the hostnames that correspond to them.
Do a query through a specific port that you want to use.
See the TTL value of the DNS records and know, how often, do they refresh.
Trace the route of a DNS query.
You can find the DIG command pre-installed on most Linux distros. You can easily install it on macOS, too with brew, and get the DIG command on Windows 10 with bind9.

How does it work?
The DIG command works by performing a DNS query from your device to the targeted IP address or hostname. The query will first arrive at your ISP’s recursive name servers. If there, it has your answer, it will return it fast. If no, your query will be re-routed in search of the answer. There could be another recursive DNS server that can answer the query, or it could arrive to the authoritative DNS name server, who for sure will have the answer, and you will get your DNS query resolved.  


How to install the Dig command?

Here are the 10 most used DIG commands
Here you have 10 examples of DIG command. We will use example.com as a hostname and 1.2.3.4. as an IP address. Feel free to try these commands with the domain and IP address you want by simply changing the text before you try.  

Open the Terminal application. We need it to write and execute the DIG command there.

1. How to find the website’s IP address?
Find the IP address of a particular domain name that you want to know. You can use the DIG command, without any additional option, which is:

dig example.com

It will do a DNS query, looking for the A records. They have the IP addresses which correspond to the domain name form the query.

The following dig command will give you a lot of extra information too. Data like the version of the DIG command you are using, a header that shows you what you did and who answered you, the port and protocol you used (usually UDP), the time it took for the query, the TTL of the record, and the server which answered you.

If you don’t want so much information, go for the short answer of just the IP address with this command:

Command Line:

$ dig example.com +short

Output:

1.2.3.4

The result will be just the IP address.

Looking for e great DNS service provider? Test ClouDNS for free!

2. How to find the name servers, responsible for your domain?
See all the name servers, in a list, for the particular domain. We will dig for the NS records, and again we will use the +short option to get just the name servers without extra data.

Command Line:

$ dig NS example.com +short

Output:

ns1.example.com.

ns2.example.com.

ns3.example.com.

ns4.example.com.

You want to see if all of the name servers are listed. If one is not showing, it means there are problems with it, and you will need to troubleshoot the problem further.

3. What is the delegation path to your DNS Zone?
See the delegation patch from the root server to your DNS zone. You can make a trace request and see the path, starting from the root server to your DNS zone.

We will use the option +trace.

Command Line:

$ dig example.com +trace

Output:

; <<>> DiG 9.9.5-3ubuntu0.7-Ubuntu <<>> example.com +trace

;; global options: +cmd

. 3493 IN NS a.root-servers.net.

. 3493 IN NS b.root-servers.net.

. 3493 IN NS c.root-servers.net.

. 3493 IN NS d.root-servers.net.

. 3493 IN NS e.root-servers.net.

. 3493 IN NS f.root-servers.net.

. 3493 IN NS g.root-servers.net.

. 3493 IN NS h.root-servers.net.

. 3493 IN NS i.root-servers.net.

. 3493 IN NS j.root-servers.net.

. 3493 IN NS k.root-servers.net.

. 3493 IN NS l.root-servers.net.

. 3493 IN NS m.root-servers.net.

;; Received 397 bytes from 127.0.1.1#53(127.0.1.1) in 466 ms

com. 172800 IN NS a.gtld-servers.net.

com. 172800 IN NS b.gtld-servers.net.

com. 172800 IN NS c.gtld-servers.net.

com. 172800 IN NS d.gtld-servers.net.

com. 172800 IN NS e.gtld-servers.net.

com. 172800 IN NS f.gtld-servers.net.

com. 172800 IN NS g.gtld-servers.net.

com. 172800 IN NS h.gtld-servers.net.

com. 172800 IN NS i.gtld-servers.net.

com. 172800 IN NS j.gtld-servers.net.

com. 172800 IN NS k.gtld-servers.net.

com. 172800 IN NS l.gtld-servers.net.

com. 172800 IN NS m.gtld-servers.net.

;; Received 734 bytes from 192.203.230.10#53(e.root-servers.net) in 496 ms

example.com. 172800 IN NS ns2.example.com.

example.com. 172800 IN NS ns1.example.com.

example.com. 172800 IN NS ns3.example.com.

example.com. 172800 IN NS ns4.example.com.

;; Received 660 bytes from 192.55.83.30#53(m.gtld-servers.net) in 229 ms

example.com. 300 IN A 1.2.3.4

example.com. 300 IN NS ns1.example.com

example.com. 300 IN NS ns2.example.com

example.com. 300 IN NS ns3.example.com

example.com. 300 IN NS ns4.example.com

;; Received 44 bytes from 216.239.34.10#53(ns2.example.com) in 40 ms

The answer will show you the route that a typical DNS query goes. You can see the hops and detect a problem, and where exactly the requests get lost.

4. Which is the responsible mail server for your domain?
Check the responsible mail servers for accepting emails.

Command Line:

$ dig MX example.com +short

Output:

1 ASPMX.L.GOOGLE.COM.

5 ALT1.ASPMX.L.GOOGLE.COM.

5 ALT2.ASPMX.L.GOOGLE.COM.

10 ALT3.ASPMX.L.GOOGLE.COM.

10 ALT4.ASPMX.L.GOOGLE.COM.

This query will be directed to the MX records. Inside them, we want to see if the mail servers are all showing and if the MX records are pointed correctly.

5. With which IP address a domain name is assciated with?
Reverse DNS check, IP address to hostname. You can also perform the reverse DNS check and see to which hostname does an IP address belongs. For this purpose, the domain owner needs to have PTR DNS records with the IP address and pointed correctly.

Command Line:

$ dig -x 1.2.3.4

Output:

example.com

6. Which are the name servers, responsible for the TLDs (top-level domains)?
See the name servers, list of all of them, of the TLD you put in the query. Yes, you can also do this and check the name servers of a TLD like COM, EU, US, ASIA, or another.

The DIG command will be similar to the previous, but instead of a complete domain name, we will just put the TLD. In this case, “com”.

Command Line:

dig NS com +short

Output:

j.gtld-servers.net.

a.gtld-servers.net.

i.gtld-servers.net.

d.gtld-servers.net.

f.gtld-servers.net.

b.gtld-servers.net.

h.gtld-servers.net.

e.gtld-servers.net.

m.gtld-servers.net.

k.gtld-servers.net.

c.gtld-servers.net.

g.gtld-servers.net.

l.gtld-servers.net.

7. How to check if your DNS zone is synchonized over all authoritative name servers?
Command Line:

$ dig example.com +nssearch

Output:

SOA ns1.example.com. dns-admin.example.com. 2016042102 7200 1800 1209600 300 from server ns3.example.com in 14 ms.

SOA ns1.example.com. dns-admin.example.com. 2016042102 7200 1800 1209600 300 from server ns2.example.com in 22 ms.

SOA ns1.example.com. dns-admin.example.com. 2016042102 7200 1800 1209600 300 from server ns4.example.com in 88 ms.

SOA ns1.example.com. dns-admin.example.com. 2016042102 7200 1800 1209600 300 from server ns1.example.com in 125 ms.

Verify if your DNS zone is synchronized in all authoritative name server. This is a way to check the SOA records and see if their data matches. If your DNS zones are not synchronized, you will need to manually manage and update them. 

8. How can I check when the cache of an answer will expire?
See when the cache with the answer will expire.

Command Line:

$ dig example.com +noall +answer

Output:

;; global options: +cmd

example.com. 109 IN A 1.2.3.4

example.com. 109 IN A 1.2.3.4;; ->>HEADERexample.com. 109 IN A 1.2.3.4

example.com. 109 IN A 1.2.3.4

The additional options will remove unwanted information and just show the answer that we want, the TTL value for the A record. This value represents time in seconds, for how long it is still valid.

9. How to check is a zone existing on a name server?
Look if a zone exists on a particular name server. We want to see the SOA record again, but we will specify with “@” symbol on which name server we are searching for it. In this case, the name server is “ns1.example.com”.

Command Line:

$ dig SOA example.com @ns1.example.com 

You could get one of three results:

NOERROR – yes, the zone exists.
NXDOMAIN – no, it does not.
REFUSED – the name server does not want to answer.
10. How to check which value is in cache in a given resolver?
Check what a particular resolver has in its cache memory. We will use Google’s DNS resolver (8.8.8.8) to see what it has for our domain name.

Command Line:

$ dig example.com @8.8.8.8

Output:

;; global options: +cmd

;; Got answer:

;; ->>HEADER<;; flags: qr rd ra; QUERY: 1, ANSWER: 6, AUTHORITY: 0, ADDITIONAL: 0

;; QUESTION SECTION:

;google.com. IN A

;; ANSWER SECTION:

example.com. 300 IN A 1.2.3.4

example.com. 300 IN A 1.2.3.4

example.com. 300 IN A 1.2.3.4

example.com. 300 IN A 1.2.3.4

example.com. 300 IN A 1.2.3.4

example.com. 300 IN A 1.2.3.4

You will see the A records, with their values.

Conclusion
Troubleshooting with the DIG command is easy and fast. Use it for quick DNS diagnostic of DNS records and name servers. Find the problem and later fix it.
