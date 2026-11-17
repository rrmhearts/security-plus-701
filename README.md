# Security Plus 701 Exam

Material for studying. Review these!

## Basics

### Security Control Categories

Managerial, Operational, Technical, Physical

### Control Functional Types

Preventative, Detective, Corrective, Directive (enforces), Deterrent (discourages), Compensating (substitutes)

### Risk Management

Risk Analysis, Risk Assessment, Quantitative Analysis (single vs annualized Loss Expectancy), Qualitative Analysis

Responses: Avoid, Accept, Mitigate, Transfer

Key Risk Indicators (KRIs) are critical predictive indicators organizations use to monitor and predict potential risks. 

* Maximum tolerable downtime (MTD) is the longest period of time that a business function outage may occur for without causing irrecoverable business failure.
* Recovery time objective (RTO) is the period following a disaster that an individual IT system may remain offline. 
* Work Recovery Time (WRT). Following systems recovery, there may be additional work to reintegrate different systems, test overall functionality, and brief system users on any changes or different working practices so that the business function is again fully supported.
* Recovery point objective (RPO) is the amount of data loss that a system can sustain, measured in time. 
* Mean time between failures (MTBF) represents the expected lifetime of a product. The calculation for MTBF is the total operational time divided by the number of failures. For example, if you have 10 appliances that run for 50 hours and two of them fail, the MTBF is 250 hours/failure (10\*50)/2.
* Mean time to repair (MTTR) is a measure of the time taken to correct a fault so that the system is restored to full operation. This can also be described as mean time to replace or recover. MTTR is calculated as the total number of hours of unplanned maintenance divided by the number of failure incidents. This average value can be used to estimate whether a recovery time objective (RTO) is achievable.

## Incident Response Processes

Preparation, Detection, Analysis, Containment, Eradication, Recovery, Lessons Learned

## Ports

Common network services use standard ports assigned through the Service Name and Transport Protocol Port Number Registry (IANA), split into well-known (0–1023), registered (1024–49151), and dynamic/private (49152–65535) ranges.

File Transfer \& Remote Access

• 20 (TCP/UDP): FTP Data — file transfer data channel
• 21 (TCP): FTP Control — file transfer commands and authentication
• 22 (TCP): SSH / SCP / SFTP — encrypted remote login and file transfer
• 23 (TCP): Telnet — unencrypted remote terminal access
• 69 (UDP): TFTP — lightweight, unauthenticated file transfer
• 445 (TCP): SMB — Windows file and printer sharing
• 3389 (TCP/UDP): RDP — Remote Desktop Protocol
• 5900 (TCP): VNC — remote desktop sharing

Web \& Network Infrastructure

• 53 (TCP/UDP): DNS — domain name resolution
• 67 / 68 (UDP): DHCP — automatic IP address assignment (67 server, 68 client)
• 80 (TCP): HTTP — unencrypted web traffic
• 123 (UDP): NTP — Network Time Protocol clock synchronization
• 161 / 162 (UDP): SNMP — network device monitoring and traps
• 179 (TCP): BGP — Border Gateway Protocol routing
• 443 (TCP/UDP): HTTPS — encrypted web traffic (TLS; UDP used for HTTP/3 / QUIC)
• 8080 / 8443 (TCP): Alternate HTTP / HTTPS — proxies, development servers, and management panels

Email

• 25 (TCP): SMTP — mail transfer between servers
• 110 (TCP): POP3 — unencrypted email retrieval
• 143 (TCP): IMAP — unencrypted mailbox access
• 465 / 587 (TCP): SMTPS / Submission — secure email sending
• 993 (TCP): IMAPS — encrypted IMAP
• 995 (TCP): POP3S — encrypted POP3

Directory, Auth \& Databases

• 88 (TCP/UDP): Kerberos — network authentication
• 135 (TCP): MS RPC Endpoint Mapper — Windows remote procedure calls
• 389 / 636 (TCP/UDP): LDAP / LDAPS — directory services (636 over SSL/TLS)
• 1433 (TCP): Microsoft SQL Server — default database port
• 3306 (TCP): MySQL — default database port
• 5432 (TCP): PostgreSQL — default database port

For full technical port tables and protocol assignments, see the List of TCP and UDP port numbers or Microsoft's Service overview and network port requirements guide.

