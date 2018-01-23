---
layout: default
title: Replacing a Wildcard Certificate
categories:
  - blog
tags:
  - dns
  - python
  - software
  - tls
---

Quick, your wildcard certificate is expiring in two weeks, and it needs to be replaced on all the servers its been copied to in the past three years. Unfortunately, there's no record of who did what where, and too many servers to check manually.

Here's how I approached this problem.

## Tools
* Linux - bash and coreutils
* bind-utils
* Python 3 and its OpenSSL library
* My script [check-ssl-thumbprints.py](https://github.com/benformosa/Toolbox/blob/master/check-ssl-thumbprints.py).

Install on Ubuntu with:
```bash
apt install bind9utils python3 python3-openssl
wget https://github.com/benformosa/Toolbox/blob/master/check-ssl-thumbprints.py
```

## Process
Let's say I have a certificate for `*.example.com`, which has a thumbprint starting with `AA:BB:CC`.
1. Get a copy of the internal and external zone files. I use split-horizon DNS with our external DNS hosted by a service provider, and our internal DNS running on Active Directory.  
Request a dump from the service provider. They can give me a BIND zone file, `external_example_dns.txt`.  
Use Windows DNS tools to get a zone file from AD, `internal_example_dns.txt`:
```cmd
dnscmd /ZoneExport example.com internal_example_dns.txt
```
2. From the zone file, create a list of hostnames which would be valid for the wildcard certificate. This means exactly one label in front of the base name, e.g. **www**.example.com.  Optionally, set `SUBDOMAIN` to filter out a single subdomain from the zone.
```bash
ZONE=example.com
SUBDOMAIN=example.com
ZONEFILE=external_example_dns.txt
HOSTFILE=external_example_hostnames.txt
REGEX="^[[:alnum:]]+\.$(echo $SUBDOMAIN | sed 's/\./\\./g')"
named-compilezone -o - $ZONE $ZONEFILE |  # compile to a canonical zonefile format
    grep -E $REGEX |                      # grep for matching hostnames
    grep -E 'IN (A|CNAME)' |              # grep for A or CNAME records
    tr -s '[:blank:]' ' ' |
    cut -d' ' -f1 |                       # grab the hostnames only
    sed 's/\.$//g' |                      # strip the trailing dot
    tr '[:upper:]' '[:lower:]' |          # lowercase everything
    sort -u > $HOSTFILE                     # sort, remove duplicates, output to file
```
5. Attempt to connect to each host on port 443 and get the certificate.
```bash
check-ssl-thumbprints.py external_example_hostnames.txt > external_example_thumbprints.csv
```
6. Filter for sites with HTTPS, which have the expiring certificate.
```bash
grep -vE '^hostname,ipaddress|No connection' external_example_thumbprints.csv | grep 'AA:BB:CC' | sort -t',' -k1
```

## Outcome
At this point, I copied the output into a spreadsheet where I could record the actual hostname of each HTTPS endpoint, and the paths to the certificate files and configuration files. I'm fairly confident that this method identified all the hosts that I need to replace the certificate on. However, any host that has the certificate but on an invalid hostname (e.g. foo.bar.example.com, or without a hostname) won't be identified.
