---
title: 80,443 (Web)
parent: Ports
nav_order: 1
---

- Check `robots.txt`, `sitemap.xml`, `.htaccess`, `.htpasswd`
- Directory discovery (Gobuster): `gobuster dir -w /usr/share/seclists/Discovery/Web-Content/raft-medium-words.txt -x html,php,txt -b 403,404 -u target -f --proxy socks5://IP:PORT --no-tls-validation -U username -P password --exclude-length xx`
- Directory discovery (Dirb): `dirb http://IP -r -z 10` (remove -r for recursive scan)
- Directory discovery (ffuf): `ffuf -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-small.txt:FUZZ -u http://SERVER_IP:PORT/FUZZ -recursion -recursion-depth 1 -e .php -v`
- Web scanner (Nikto): `nikto -host=http://IP`
- Subdomain discovery: `gobuster vhost -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt -u http://thetoppers.htb`
- Subdomain discovery (DNS): `gobuster dns -i -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt -d thetoppers.htb`
- Subdomain discovery (ffuf): `ffuf -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt -H "Host: FUZZ.thetoppers.htb" -u http://10.129.109.151 -mc all -fs 11952` (if add to /etc/hosts, can just use -u and the hostname. mc all is to see all HTTP response code. fs 11952 is filter out response size)
- Wordpress specific: `wpscan --no-update -e ap,at,cb,dbe,u --url IP/xxx --disable-tls-checks` (xxx might be blog or something) Normal quick scan just use `wpscan --no-update -e vp,u --url IP/xxx`
- Wordpress plugin version (not 100% can): `http://IP/wp-content/plugins/pluginname/readme.txt`
