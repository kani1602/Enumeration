# Explore Google hacking and enumeration 

# AIM:

To use Google for gathering information and perform enumeration of targets

## STEPS:

### Step 1:

Install kali linux either in partition or virtual box or in live mode

### Step 2:

Investigate on the various Google hacking keywords and enumeration tools as follows:


### Step 3:
Open terminal and try execute some kali linux commands

## Pen Test Tools Categories:  

| Operator    | Description                        | Example Usage           |
| ----------- | ---------------------------------- | ----------------------- |
| `site:`     | Search within a specific domain    | `site:example.com`      |
| `inurl:`    | Search in URL                      | `inurl:admin`           |
| `intitle:`  | Search in page title               | `intitle:"index of"`    |
| `filetype:` | Search by file type                | `filetype:pdf`          |
| `intext:`   | Search inside page text            | `intext:"confidential"` |
| `link:`     | Pages that link to a specific site | `link:example.com`      |
| `cache:`    | View cached version of a site      | `cache:example.com`     |
| `ext:`      | Same as filetype                   | `ext:xls`               |

 ## Architecture 
 ```
+----------------------+
|   Attacker / Hacker  |
|   (Browser & Google) |
+----------+-----------+
           |
           | Google Dork Queries
           v
+---------------------------+
|       Google Search       |
+---------------------------+
           |
           | Indexed Public Content
           v
+---------------------------+
|   Target Websites / Data  |
| - Leaked files            |
| - Open directories        |
| - Sensitive info          |
+---------------------------+

```

# Output:
## SITE
<img width="1280" height="638" alt="image" src="https://github.com/user-attachments/assets/450df5b6-7ba5-4578-9bac-2894f2685f98" />

## INTEXT
<img width="1280" height="638" alt="image" src="https://github.com/user-attachments/assets/f4848931-35b9-4ae3-b717-b82ec4efda16" />

## FILETYPE
<img width="1280" height="632" alt="image" src="https://github.com/user-attachments/assets/efc90b83-e6a7-4611-a770-ab64eaf53de2" />

## INURL
<img width="1919" height="950" alt="image" src="https://github.com/user-attachments/assets/a0d96a6b-860b-497e-99b1-e5acb58eab19" />

## inurl:index ofm
<img width="1890" height="952" alt="image" src="https://github.com/user-attachments/assets/9ac1e98d-fbe2-4621-b3e4-780a13bd9408" />

## link:example.com
<img width="1913" height="948" alt="image" src="https://github.com/user-attachments/assets/202d3a90-dfa6-4fc0-9793-e3576f884714" />

## cache:flipkart.com
<img width="1451" height="940" alt="image" src="https://github.com/user-attachments/assets/0c308af4-f350-4c29-a81c-a7fde75a9c87" />

### DNS Enumeration
<img width="1218" height="684" alt="image" src="https://github.com/user-attachments/assets/8fe79d5b-5266-4831-bc22-7947cef9a267" />

## DNS Recon

| Record Type | Meaning                        | Example Output                   |
| ----------- | ------------------------------ | -------------------------------- |
| A           | Host to IPv4 address           | `example.com -> 93.184.216.34`   |
| AAAA        | Host to IPv6 address           | `example.com -> ::1`             |
| MX          | Mail server info               | `mail.example.com`               |
| NS          | Name servers                   | `ns1.example.com`                |
| TXT         | Misc data (SPF, verifications) | `v=spf1 include:_spf.google.com` |
| CNAME       | Canonical names (aliases)      | `www -> example.com`             |

## Common Tools Used (Kali Linux)

| Tool           | Description                                | Usage Example                           |
| -------------- | ------------------------------------------ | --------------------------------------- |
| `nslookup`     | DNS lookup tool (simple queries)           | `nslookup example.com`                  |
| `dig`          | DNS lookup utility (detailed)              | `dig example.com any`                   |
| `host`         | Simple DNS querying tool                   | `host example.com`                      |
| `dnsenum`      | Perl script to enumerate DNS info          | `dnsenum example.com`                   |
| `fierce`       | DNS scanner to locate non-contiguous IPs   | `fierce -dns example.com`               |
| `dnsrecon`     | Powerful DNS enumeration script            | `dnsrecon -d example.com -a`            |
| `theHarvester` | Subdomain enumeration using search engines | `theHarvester -d example.com -b google` |


## OUTPUT:
### NSLOOKUP:
<img width="928" height="857" alt="image" src="https://github.com/user-attachments/assets/4a59fdb4-d715-4cd7-9124-5d1e3d419379" />

### DIG:
<img width="796" height="631" alt="image" src="https://github.com/user-attachments/assets/57e90025-25a5-4878-a941-979d7b52dc4b" />

### HOST:
<img width="765" height="636" alt="image" src="https://github.com/user-attachments/assets/8f0f7a95-0dcc-4e88-8cce-f046c1397cf4" />

### DNSENUM:
<img width="1218" height="684" alt="image" src="https://github.com/user-attachments/assets/0576517c-47f4-40d0-89a1-b4256fee1696" />

### FIERCE:
<img width="698" height="603" alt="image" src="https://github.com/user-attachments/assets/bf3e7e75-8a89-47c4-8553-48d85e52bd8a" />

### theharvester:
<img width="835" height="645" alt="image" src="https://github.com/user-attachments/assets/6408e918-a7e3-490c-a23a-18b876d0a553" />

## Architecture Diagram 
```
+-------------------+        +------------------+       +------------------+
|                   |        |                  |       |                  |
|   Attacker (You)  +------->|   Target Server   +<----->+    DNS Server    |
| Kali Linux / Parrot|       | (Mail / DNS Host) |       |  (Authoritative) |
+---------+---------+        +---------+--------+       +---------+--------+
          |                            ^                          ^
          |                            |                          |
          |                            |                          |
          |           +-----------------------------+            |
          |           |      Information Tools      |            |
          |           |-----------------------------|            |
          |           | smtp-user-enum              |            |
          |           | nmap --script smtp-enum-*   |            |
          |           | dnsenum                     |<-----------+
          |           +-----------------------------+
          |
          v
+-----------------------------+
|   Output/Report             |
|  - Usernames Found          |
|  - MX Records / Zones       |
|  - Subdomains / IPs         |
+-----------------------------+

```

## dnsenum
**Purpose:** A multithreaded Perl script to enumerate information from DNS servers.

**Use case:** Performs DNS zone transfers, brute force subdomains, and gather host IPs.

```
dnsenum example.com
```

## Output:
<img width="1218" height="684" alt="image" src="https://github.com/user-attachments/assets/837f9ebe-98f6-406b-a6e2-64d8a5b10b8d" />

## smtp-user-enum
**Purpose:** Standalone tool used to enumerate valid users by using the VRFY, EXPN, or RCPT TO commands.

**Use case:** Brute-forces SMTP to find users.

```
smtp-user-enum -M VRFY -U users.txt -t <target-ip>
```
  
## Output
<img width="920" height="385" alt="image" src="https://github.com/user-attachments/assets/cf29c043-766b-41e8-865e-7d9f71388623" />
 
## nmap –script smtp-enum-users.nse <hostname>

**Purpose:** Uses smtp-enum-users NSE script to enumerate valid users on an SMTP server.

**Use case:** Helps identify email accounts on mail servers.

```
nmap -p 25 --script smtp-enum-users.nse <target-ip>
```
## OUTPUT:
<img width="932" height="205" alt="image" src="https://github.com/user-attachments/assets/b3af4a0a-13a2-4969-a703-d354f0801776" />

## RESULT:
The Google hacking keywords and enumeration tools were identified and executed successfully
