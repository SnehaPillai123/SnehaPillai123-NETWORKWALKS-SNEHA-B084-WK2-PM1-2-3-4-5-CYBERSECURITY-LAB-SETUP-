# PENETRATION TESTING REPORT

### FOOTPRINTING & NETWORK SCANNING PHASES

W2-PM-FINAL \| CYBERSECURITY \| NETWORKWALKS

<table>
<colgroup>
<col style="width: 34%" />
<col style="width: 65%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Pentester Name<br />
(Cybersecurity Student)</strong></th>
<th><strong>Sneha Hariprasad Pillai</strong></th>
</tr>
<tr class="odd">
<th><strong>Program/Batch</strong></th>
<th>B084-Networkwalks</th>
</tr>
<tr class="header">
<th><strong>Date</strong></th>
<th>11 November 2026</th>
</tr>
<tr class="odd">
<th><strong>Modules completed</strong></th>
<th><p>W2-PM1 (Multiple kali tools),</p>
<p>W2-PM2 (GHDB),</p>
<p>W2-PM3 (Maltego),</p>
<p>W2-PM4 (theHARVESTER),</p>
<p>W2-PM5 (Zenmap Scanning)</p></th>
</tr>
<tr class="header">
<th><strong>Client/Target</strong></th>
<th><p>1. Networkwalks (secured written permission already)</p>
<p>2. My own local LAN Network (192.168.1.0/24)</p>
<p>3. Microsoft.com (example target specified in the W2-PM4 module; public data sources only)</p></th>
</tr>
<tr class="odd">
<th><strong>Permission secured from client?</strong></th>
<th>Yes</th>
</tr>
<tr class="header">
<th><strong>Phases covered</strong></th>
<th><p><strong>Phase 1:</strong> Reconnaissance &amp; Footprinting<br />
<strong>Phase 2:</strong> Scanning &amp; Network Discovery</p>
<p><strong>Phase 3-5:</strong> In Progress</p></th>
</tr>
</thead>
<tbody>
</tbody>
</table>

## 1. Liability Disclaimer

I have performed these activities only on the systems & devices where I had secured written permission or the devices/systems that I own myself. All these materials are for education and research purpose only. Do not use anything from here to break the law. The instructor, the authors and Networkwalks are not responsible for what you do with this knowledge. Every action you take is your own responsibility. Misuse can lead to criminal charges, heavy fines, loss of your job and a permanent record. In most countries unauthorised access is a crime even when nothing is damaged.

## 2. Introduction

This report covers footprinting the networkwalks.com domain using multiple Kali Linux tools (W2-PM1) and Maltego (W2-PM3), Google Hacking Database dorks (W2-PM2), theHarvester on microsoft.com (W2-PM4, the example target given in that module), and scanning my own local network with Zenmap (W2-PM5). Four modules cover the footprinting phase and one covers the scanning phase, so together they show how an attacker moves from gathering public information to mapping live hosts on a network. It is the Week 2 part of my ongoing internship program at Networkwalks.

The footprinting commands were run in Kali Linux (inside VirtualBox) and in Maltego Desktop on Windows. The GHDB dorks were searched through Google in a browser. The scanning was done on a Windows PC with Zenmap installed. Every step below includes the exact command used, the result I observed, a screenshot as evidence, and a short note on why the finding matters from an attacker’s point of view.

## 3. Tools Used

The table below lists each tool used in this report and its purpose.

| **Tool**                             | **Purpose**                                                                                                                                                   |
|--------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Kali Linux & Windows                 | Operating systems used for reconnaissance activities                                                                                                          |
| WHOIS                                | Find domain registration details (owner, dates, name servers).                                                                                                |
| whatweb                              | Fingerprint web technologies (server, CMS, plugins, IP).                                                                                                      |
| nslookup                             | Resolve the domain name to its IP address using DNS.                                                                                                          |
| curl -I                              | Read the HTTP response headers of the website.                                                                                                                |
| wafw00f                              | Detect whether a Web Application Firewall protects the site.                                                                                                  |
| dnsrecon                             | Enumerate all DNS records (NS, MX, SPF, TXT, SRV).                                                                                                            |
| Google Hacking Database (Exploit-DB) | Source of ready-made Google search queries (dorks).                                                                                                           |
| Google Search (dorks)                | Run the dorks to find publicly exposed devices and files without touching the target.                                                                         |
| Maltego Desktop 4.14.0               | Link-analysis tool; four email transforms (“To Emails @domain \[Search Engine\]”, From whois info, PGP and Search Engine) find e-mail addresses for a domain. |
| theHarvester 4.11.1                  | OSINT tool that gathers e-mails, hosts/sub-domains, IPs, ASNs and URLs from public sources.                                                                   |
| Windows CMD                          | Local IP and MAC address identification                                                                                                                       |
| Zenmap (Nmap GUI)                    | Scan the local subnet to find live hosts, IPs and MAC addresses.                                                                                              |

## 4. Activities Performed

## 4.1 Footprinting & Reconnaissance

I performed footprinting and reconnaissance using four modules: multiple Kali Linux tools (W2-PM1), Google Hacking Database dorks (W2-PM2), Maltego (W2-PM3) and theHarvester (W2-PM4). Each module was used to collect a different type of public information without attacking the target.

### 4.1.1 Multiple Kali Tools (W2-PM1) 

I performed reconnaissance against the networkwalks.com domain using six Kali Linux tools: **WHOIS, WhatWeb, Nslookup, Curl, Wafw00f and DNSRecon**.

First, I used **WHOIS** to obtain publicly available domain registration information and identify the domain’s name servers. The results provided information about the domain registration and hosting infrastructure.

I then used **WhatWeb** to identify technologies used by the website. The results identified **WordPress 7.1.4** and **WordPress Download Manager 3.3.76**, along with other information exposed by the website.

Using **Nslookup**, I resolved the domain name to its IP address. The result identified **192.232.216.135**.

I used **Curl** with the -I option to inspect the HTTP response headers. This provided additional information about the web application and exposed the WordPress REST API endpoint /wp-json/.

Next, I used **Wafw00f** to determine whether a Web Application Firewall was protecting the website. The result identified **ModSecurity (SpiderLabs)**.

Finally, I used **DNSRecon** to enumerate DNS records. The results provided information relating to name servers, mail servers, SPF/TXT records, service records and DNS software information.

### 4.1.2 Google Hacking Database (W2-PM2) 

I opened the GHDB on Exploit-DB, searched for relevant terms and copied the dorks one by one into Google. Google returned its indexed results, so the target systems were never contacted directly.

For Task 1, I used dorks such as intitle:"webcamXP" inurl:8080 to look for exposed camera pages. I recorded each link and its dork in the table. For Task 2, I used the dork intitle:index.of "parent directory" mathematics pdf to find open directories that list downloadable mathematics PDF ebooks. I recorded 10 listings with their links and dorks. The links are hidden with red bands in this public copy for safety. No usernames or passwords were needed or used.

### 4.1.3 Maltego (W2-PM3)

I created a new graph in Maltego Desktop, added a Domain entity named networkwalks.com and ran four email transforms: \[Utilities\] To Emails @domain \[Search Engine\], To Email address \[From whois info\], To Email Addresses \[PGP\] and To Email Addresses \[Search Engine\]. Every transform returned info@networkwalks.com, so it is the only public company address found. The whois transform also returned abuse@godaddy.com, which is the domain registrar’s abuse contact and not a Networkwalks mailbox. After all four runs, 148 credits remained.

Why it matters: a public contact address is normal for a business, but any published address can become a target for phishing or social engineering. It also confirms the naming convention used for the domain’s mailboxes. The registrar contact shows which provider holds the domain.

### 4.1.4 theHarvester (W2-PM4)

I first ran theHarvester against a single source (Baidu) to understand the output. I then ran it against all supported sources with a result limit of 50. The target was microsoft.com, as specified in the W2-PM4 module, using public data sources only.

> theHarvester -d microsoft.com -l 1000 -b baidu

Result: No IPs, e-mails, people or hosts were found. A single search engine returned nothing, which shows why several sources are normally combined.

> theHarvester -d microsoft.com -l 50 -b all

The summary of what the tool reported is below.

| **Item**                               | **Result**                                                                                                                                                            |
|----------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **ASNs found**                         | 9: AS8075 (Microsoft), AS13335 (Cloudflare), AS14618 (Amazon), AS16625 and AS20940 (Akamai), AS133618, AS206834, AS40034, AS47583                                     |
| **Interesting URLs**                   | 9 (including 4 Microsoft sign-in / OAuth URLs for QA and Intune applications that expose tenant and client IDs, plus mcp.microsoft.com, Azure Maps and privacy pages) |
| **IP addresses**                       | 58 (46 IPv4 and 12 IPv6)                                                                                                                                              |
| **E-mail addresses**                   | 3: dotnet-docker-bot@microsoft.com, opencode@microsoft.com, secure@microsoft.com                                                                                      |
| **People / LinkedIn**                  | None found                                                                                                                                                            |
| **Hosts / sub-domains**                | 9,490 found                                                                                                                                                           |
| **Hudson Rock (infostealer database)** | 621,809 total compromised credentials recorded for the domain, of which 16,601 employees and 600,418 users; 44 hosts extracted from employee URLs                     |
| **Windvane fallback**                  | No API key, so 14 sub-domains found with DNS pattern search                                                                                                           |

**What the 9,490 host names show.** I analysed the full host list in the saved output (the public copy in this repository is trimmed). The counts below are approximate and overlap, because one name can match several patterns.

| **Pattern in host name**        | **Approx. count** | **Meaning**                 |
|---------------------------------|-------------------|-----------------------------|
| contains “corp.microsoft.com”   | 3,300             | Corporate / internal naming |
| contains “redmond”              | 1,680             | Internal site naming        |
| contains “dev”                  | 950               | Development systems         |
| contains “test”                 | 510               | Test systems                |
| contains “ppe” (pre-production) | 510               | Pre-production systems      |
| contains “uat”                  | 230               | User-acceptance testing     |
| contains “api.”                 | 580               | API endpoints               |
| contains “login” or “auth”      | 120               | Authentication services     |

**Observations and limitations.**

- More than 30 data sources failed because no API key was configured (for example Shodan, Censys, VirusTotal, SecurityTrails, Hunter, GitHub and HaveIBeenPwned). They are marked “Missing API key” in the output. The results above come only from sources that work without a key, so a fully configured run would very likely return more.

- Fofa returned an invalid-credentials error, LeakIX returned “Incorrect API Key” and ThreatCrowd gave no response. These were skipped by the tool.

- The raw list contains noise that has to be validated manually, for example URL-encoding artefacts (2Fblogs.microsoft.com), GUID-style names and wildcard entries (\*.xxx). The list should not be treated as a confirmed asset inventory.

- Many names reveal internal, test and pre-production environments. An attacker can use them to guess naming conventions and pick weaker, less-monitored systems.

**Why it matters:** everything above was collected without sending a single packet to the target. An attacker could use the sub-domain list, IP ranges, ASNs and e-mail addresses to plan phishing, choose which systems to scan next, and prioritise forgotten test environments.

## 4.2 Network Scanning with Zenmap (W2-PM5)

For the second activity, I used **Zenmap** to perform network discovery on my local network. The practical required me to identify my local IP address and subnet, discover live hosts, identify their IP and MAC addresses, and generate a network topology.

I first used the Windows ipconfig command to identify my local IP address and LAN subnet. My Wi-Fi adapter has the IP address 192.168.1.6, subnet mask 255.255.255.0 and default gateway 192.168.1.1. I then entered the subnet 192.168.1.0/24 into Zenmap and selected **Ping Scan** to identify active hosts.

The scan (nmap -sn 192.168.1.0/24) identified six live hosts out of 256 addresses:

- 192.168.1.1 (the router, shown as “Unit”)

- 192.168.1.2

- 192.168.1.3

- 192.168.1.4

- 192.168.1.5

- 192.168.1.6 (my own PC, shown as host.docker.internal)

Zenmap does not list the MAC address of the scanning PC itself, so I read it with ipconfig /all (Wi-Fi adapter): D8:F3:BC:xx:xx:xx (last three bytes masked for privacy). The scan also returned five MAC addresses for the other devices:

- 2C:C1:F4:8A:AD:E1 (Nokia Solutions and Networks India)

- EE:1E:0F:18:B1:18

- 7A:6E:3F:BA:27:B0

- FE:33:2E:AF:65:B5

- 1A:95:EC:3B:28:3A

After completing the scan, I opened the **Topology** section in Zenmap, enabled the legend and saved the network topology in PDF format as required by the practical task (the saved file is included with this report as PM5_zenmap_topology.pdf). I also answered the questions on the Networkwalks Zenmap practice lab page.

## 5. Risk Analysis / Impact

Based on the information collected during the footprinting and network scanning activities, I identified the following potential risks.

| **\#** | **Risk / Finding**                                             | **Evidence / Observation**                                                                         | **Potential Impact**                                                                                            | **Risk Level** |
|--------|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------|----------------|
| 1      | Web technology information exposed                             | WhatWeb identified WordPress and WP Download Manager                                               | Attackers may use exposed technology/version information to identify software requiring further security review | **● Medium**   |
| 2      | Server IP address identifiable                                 | Nslookup resolved the domain to 192.232.216.135                                                    | Provides information about the network location of the web service                                              | **● Low**      |
| 3      | HTTP technical information exposed                             | Curl returned HTTP response headers and exposed /wp-json/                                          | May assist technology fingerprinting and further enumeration                                                    | **● Low**      |
| 4      | WAF technology identifiable                                    | Wafw00f identified ModSecurity (SpiderLabs)                                                        | Reveals information about the web application’s security architecture                                           | **● Low**      |
| 5      | DNS infrastructure information exposed                         | DNSRecon identified DNS, mail and service-related records                                          | DNS information can help build a broader infrastructure profile                                                 | **● Medium**   |
| 6      | Sensitive content discoverable through Google                  | GHDB dorks returned publicly indexed camera pages and open directory listings                      | Misconfigured systems can be found without contacting the target, which helps attackers choose victims          | **● Medium**   |
| 7      | Public e-mail address exposed                                  | Maltego found info@networkwalks.com                                                                | Can be targeted by phishing and social engineering                                                              | **● Low**      |
| 8      | Large number of sub-domains, including internal and test names | theHarvester returned 9,490 hosts for microsoft.com; thousands contain corp, dev, test, ppe or uat | Reveals naming conventions and non-production systems that may be less protected                                | **● Medium**   |
| 9      | Infrastructure details exposed                                 | 58 IP addresses and 9 ASNs found for microsoft.com                                                 | Helps an attacker map hosting and choose targets for later scanning                                             | **● Low**      |
| 10     | Credential exposure indicators                                 | Hudson Rock reported 621,809 compromised credentials linked to microsoft.com                       | Stolen credentials could allow account takeover if passwords are reused and MFA is missing                      | **● Medium**   |
| 11     | Multiple live hosts visible on local network                   | Zenmap identified six live hosts; four have unknown (randomised) MAC addresses                     | Unknown or unauthorized devices may potentially be present on a network                                         | **● Medium**   |

**Risk level key:** ● Critical ● Medium ● Low

The risks above are observations from the footprinting and scanning exercises, not confirmed vulnerabilities.

The practical exercises primarily involved information gathering and host discovery. No exploitation or vulnerability validation was performed as part of these two modules.

Therefore, the presence of information such as a software version, IP address or DNS record does not by itself mean that the system is vulnerable. Further authorized security testing would be required to confirm any actual vulnerability.

## 6. Recommendations

Based on the observations from these activities, I recommend the following security improvements:

1.  **Limit what is publicly discoverable.** Review which sub-domains, certificates and e-mail addresses are public. Avoid putting internal or test host names in public certificates where possible, and use wildcard or private certificate authorities for internal systems.

2.  **Use role-based mailboxes and protect them.** Keep public addresses such as info@ behind spam and phishing filtering, and train staff to recognise targeted phishing.

3.  **Retire or protect non-production systems.** Dev, test, pre-production and UAT systems should be removed when not needed, patched, and placed behind authentication or VPN.

4.  **Monitor for leaked credentials.** Enforce MFA, require password resets for accounts found in infostealer data, and monitor breach-intelligence sources.

5.  **Review OAuth application exposure.** Check that QA and test application registrations are restricted and do not allow unintended sign-ins.

6.  **Run OSINT checks on your own organisation regularly.** Run tools such as theHarvester with API keys configured and validate the results manually to remove false positives.

7.  **Search for your own exposed data.** Defenders should run Google dorks against their own domains to find exposed files, directories and devices before attackers do.

8.  **Scan your own network regularly.** Periodically run a discovery scan, compare the results with a known device list and investigate any unknown device.

9.  **Secure the home or office router.** Change default passwords, keep firmware updated, use WPA3/WPA2 and a guest network for visitors’ devices.

10. **Maintain network documentation.** Keep an updated list and topology diagram of devices and their MAC addresses.

11. **Test only with authorisation.** Reconnaissance and scanning should only be performed against systems and networks where permission has been given.

## 7. Conclusion

During Week 2 of my Cybersecurity & Ethical Hacking internship I completed practical activities covering footprinting, reconnaissance and network scanning.

In the footprinting activity I worked through four modules: multiple Kali tools (W2-PM1), GHDB (W2-PM2), Maltego (W2-PM3) and theHarvester (W2-PM4). I learned how WHOIS, WhatWeb, Nslookup, Curl, Wafw00f and DNSRecon each reveal a different part of a target, and how Google dorks can surface exposed devices and files without contacting the target. I used Maltego to find a public e-mail address for networkwalks.com and theHarvester to collect ASNs, IP addresses, e-mails, URLs and more than nine thousand host names for microsoft.com from public sources. I learned that many sources need API keys, that the output must be checked for false positives, and that even without touching a target an attacker can learn a great deal about its infrastructure.

In the network scanning activity I used ipconfig and Zenmap to identify my subnet (192.168.1.0/24), discover six live hosts, collect their IP and MAC addresses, and create a network topology. I also learned how to read MAC addresses: the router was identified by its vendor, while four devices use randomised MAC addresses.

I also learned that technical findings should be documented clearly. A good cybersecurity report should explain what was performed, what was discovered, what the observation means, what risk it may create, and what can be done to reduce that risk.

Finally, reconnaissance and scanning must always be performed within an authorised scope. These activities were completed as part of the assigned educational cybersecurity lab.

## 8. Evidences Collected

Text copies of the command outputs are in the [`outputs/`](outputs/) folder. The screenshots are in [`screenshots/`](screenshots/).

### PM1 - Multiple Kali tools

Full text output: [`outputs/W2-PM1_Kali_Tools_Output.txt`](outputs/W2-PM1_Kali_Tools_Output.txt)

![whois 1](screenshots/PM1_1_whois_a.png)
![whois 2](screenshots/PM1_1_whois_b.png)
![whois 3](screenshots/PM1_1_whois_c.png)
![whois 4](screenshots/PM1_1_whois_d.png)
![whatweb](screenshots/PM1_2_whatweb.png)
![nslookup, curl, wafw00f](screenshots/PM1_3-5_nslookup_curl_wafw00f.png)
![dnsrecon](screenshots/PM1_6_dnsrecon.png)

### PM2 - GHDB (links hidden with red bands for public sharing)

![Task 1 camera table](screenshots/PM2_task1_camera_table.png)
![Task 2 ebook table](screenshots/PM2_task2_ebook_table.png)

PDF copy: [`outputs/W2-PM2_GHDB_Tables_links_hidden.pdf`](outputs/W2-PM2_GHDB_Tables_links_hidden.pdf)

### PM3 - Maltego

![Maltego blank graph](screenshots/PM3_maltego_blank_graph.png)
![Maltego email transforms](screenshots/PM3_maltego_email_transforms_a.png)
![Maltego email transforms, all four finished](screenshots/PM3_maltego_email_transforms_b.png)

### PM4 - theHarvester

Text output: [`outputs/W2-PM4_theHarvester_Output_trimmed.txt`](outputs/W2-PM4_theHarvester_Output_trimmed.txt). The complete output contains 9,490 host names; this public copy keeps everything except the host list, which is cut after the first 50 names.

![theHarvester Baidu run](screenshots/PM4_theharvester_baidu.png)
![theHarvester all sources 1](screenshots/PM4_theharvester_all_a.png)
![theHarvester all sources 2](screenshots/PM4_theharvester_all_b.png)
![theHarvester all sources 3](screenshots/PM4_theharvester_all_c.png)

### PM5 - Zenmap network scan (IPv6 addresses, host name, DHCP IDs and the last three bytes of my own MAC addresses are hidden with red bands)

Saved topology PDF: [`outputs/PM5_zenmap_topology.pdf`](outputs/PM5_zenmap_topology.pdf)

![ipconfig](screenshots/PM5_ipconfig.png)
![ipconfig /all 1](screenshots/PM5_ipconfig_all_a.png)
![ipconfig /all 2](screenshots/PM5_ipconfig_all_b.png)
![ipconfig /all 3](screenshots/PM5_ipconfig_all_c.png)
![Zenmap ping scan](screenshots/PM5_zenmap_ping_scan.png)
![Topology legend](screenshots/PM5_topology_legend.png)
![Topology](screenshots/PM5_topology.png)

-End-

**👤 Author**

**Sneha Hariprasad Pillai**  
Cybersecurity Student B084

LinkedIn: [<u>https://www.linkedin.com/in/sneha-pillai-16994342a/</u>](https://www.linkedin.com/in/sneha-pillai-16994342a/)

**📌 Project Information**

**Program Name:** Cybersecurity program at Networkwalks \| **Week:** 02 \| **Repository:** GitHub
