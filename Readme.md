
# Comandos apt-install

- apt install sudo
- apt install iputils-ping
- apt install iputils-tracepath
- apt install traceroute
- apt install mtr
- apt install net-tools
- apt install ifupdown
- apt install dnsutils
- apt install ifplugd
- apt install whois
- apt install curl
- apt install wget

# Comprobación dig

 dig google.es

; <<>> DiG 9.16.1-Ubuntu <<>> google.es  
;; global options: +cmd  
;; Got answer:  
;; ->>HEADER<<- opcode: QUERY, status: SERVFAIL, id: 64882  
;; flags: qr rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:  
; EDNS: version: 0, flags:; udp: 1232  
; COOKIE: 06a64a5d38f98a7001000000617027b88b58323ca29ea502 (good)  
;; QUESTION SECTION:  
;google.es.                     IN      A

;; Query time: 520 msec  
**;; SERVER: 172.23.0.3#53(172.23.0.3)**   
;; WHEN: Wed Oct 20 16:29:12 CEST 2021  
;; MSG SIZE  rcvd: 66  

abcdefg