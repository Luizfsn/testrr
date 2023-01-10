# testrr

**Basic Linux Networking Tools**

Show IP configuration:
# ip a l

Change IP/MAC address:
# ip link set dev eth0 down
# macchanger -m 23:05:13:37:42:21 eth0
# ip link set dev eth0 up

Static IP address configuration:
# ip addr add 10.5.23.42/24 dev eth0

DNS lookup:
# dig compass-security.com

Reverse DNS lookup:
# dig -x 10.5.23.42

**Information Gathering**

Find owner/contact of domain or IP address:
# whois compass-security.com

Get nameservers and test for DNS zone transfer:
# dig example.com ns
# dig example.com axfr @n1.example.com

Get hostnames from CT logs: Search for
%.compass-security.com on https://crt.sh.

Or using an nmap script:
# nmap -sn -Pn compass-security.com
--script hostmap-crtsh

Combine various sources for subdomain enum:
# amass enum -src -brute -min-forrecursive 2 -d compass-security.com

**TCP Tools**

Listen on TCP port:
# ncat -l -p 1337

Connect to TCP port:
# ncat 10.5.23.42 1337

**TLS Tools**

Create self-signed certificate:
# openssl req -x509 -newkey rsa:2048
-keyout key.pem -out cert.pem -nodes
-subj "/CN=example.org/"

Start TLS Server:
# ncat --ssl -l -p 1337 --ssl-cert
cert.pem --ssl-key key.pem

Connect to TLS service:
# ncat --ssl 10.5.23.42 1337

Connect to TLS service using openssl:
# openssl s_client -connect
10.5.23.42:1337

Show certificate details:
# openssl s_client -connect
10.5.23.42:1337 | openssl x509 -text

Test TLS server certificate and ciphers:
# sslyze --regular 10.5.23.42:443

TCP to TLS proxy:
# socat TCP-LISTEN:2305,fork,reuseaddr
ssl:example.com:443

- Online TLS tests:
▪ ssllabs.com, hardenize.com
