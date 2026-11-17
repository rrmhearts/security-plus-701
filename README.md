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

* **Maximum tolerable downtime (MTD)** is the longest period of time that a business function outage may occur for without causing irrecoverable business failure.
* **Recovery time objective (RTO)** is the period following a disaster that an individual IT system may remain offline.
* **Work Recovery Time (WRT).** Following systems recovery, there may be additional work to reintegrate different systems, test overall functionality, and brief system users on any changes or different working practices so that the business function is again fully supported.
* **Recovery point objective (RPO)** is the amount of data loss that a system can sustain, measured in time.
* **Mean time between failures (MTBF)** represents the expected lifetime of a product. The calculation for MTBF is the total operational time divided by the number of failures. For example, if you have 10 appliances that run for 50 hours and two of them fail, the MTBF is 250 hours/failure (10*50)/2.
* **Mean time to repair (MTTR)** is a measure of the time taken to correct a fault so that the system is restored to full operation. This can also be described as mean time to replace or recover. MTTR is calculated as the total number of hours of unplanned maintenance divided by the number of failure incidents. This average value can be used to estimate whether a recovery time objective (RTO) is achievable.

## Incident Response Processes

Preparation, Detection, Analysis, Containment, Eradication, Recovery, Lessons Learned

## Ports

Common network services use standard ports assigned through the Service Name and Transport Protocol Port Number Registry (IANA), split into well-known (0–1023), registered (1024–49151), and dynamic/private (49152–65535) ranges.

### File Transfer & Remote Access

* 20 (TCP/UDP): FTP Data — file transfer data channel
* 21 (TCP): FTP Control — file transfer commands and authentication
* 22 (TCP): SSH / SCP / SFTP — encrypted remote login and file transfer
* 23 (TCP): Telnet — unencrypted remote terminal access
* 69 (UDP): TFTP — lightweight, unauthenticated file transfer
* 445 (TCP): SMB — Windows file and printer sharing
* 3389 (TCP/UDP): RDP — Remote Desktop Protocol
* 5900 (TCP): VNC — remote desktop sharing

### Web & Network Infrastructure

* 53 (TCP/UDP): DNS — domain name resolution
* 67 / 68 (UDP): DHCP — automatic IP address assignment (67 server, 68 client)
* 80 (TCP): HTTP — unencrypted web traffic
* 123 (UDP): NTP — Network Time Protocol clock synchronization
* 161 / 162 (UDP): SNMP — network device monitoring and traps
* 179 (TCP): BGP — Border Gateway Protocol routing
* 443 (TCP/UDP): HTTPS — encrypted web traffic (TLS; UDP used for HTTP/3 / QUIC)
* 8080 / 8443 (TCP): Alternate HTTP / HTTPS — proxies, development servers, and management panels

### Email

* 25 (TCP): SMTP — mail transfer between servers
* 110 (TCP): POP3 — unencrypted email retrieval
* 143 (TCP): IMAP — unencrypted mailbox access
* 465 / 587 (TCP): SMTPS / Submission — secure email sending
* 993 (TCP): IMAPS — encrypted IMAP
* 995 (TCP): POP3S — encrypted POP3

### Directory, Auth & Databases

* 88 (TCP/UDP): Kerberos — network authentication
* 135 (TCP): MS RPC Endpoint Mapper — Windows remote procedure calls
* 389 / 636 (TCP/UDP): LDAP / LDAPS — directory services (636 over SSL/TLS)
* 1433 (TCP): Microsoft SQL Server — default database port
* 3306 (TCP): MySQL — default database port
* 5432 (TCP): PostgreSQL — default database port


For the Security+ exam, CompTIA tests ports primarily by asking you to identify secure alternatives to insecure protocols, or by asking which port you need to block or allow on a firewall configuration.

Here are the absolute must-know ports, grouped exactly how they will test you on them.

### The Secure vs. Insecure Pairs

The exam will frequently give you a scenario where a company is using an insecure protocol and ask you which port should be opened to replace it with the secure version.

| Insecure Protocol | Insecure Port | Secure Alternative | Secure Port | Exam Context |
| --- | --- | --- | --- | --- |
| **Telnet** | 23 | **SSH** | 22 | Always replace Telnet with SSH for remote command-line access. |
| **HTTP** | 80 | **HTTPS** | 443 | HTTPS uses TLS (SSL is deprecated). |
| **FTP** | 20, 21 | **SFTP** | 22 | SFTP runs over SSH. *(Note: FTPS uses ports 989/990 but SFTP is tested more often).* |
| **LDAP** | 389 | **LDAPS** | 636 | Used for querying Active Directory. LDAPS adds SSL/TLS encryption. |
| **IMAP** | 143 | **IMAPS** | 993 | IMAP keeps email on the server; IMAPS encrypts that connection. |
| **POP3** | 110 | **POP3S** | 995 | POP3 downloads email to the client; POP3S encrypts that connection. |

## Highly Tested Infrastructure Ports

You must know these to interpret firewall Access Control Lists (ACLs) and identify network attacks.

| Protocol | Port | UDP/TCP | Why CompTIA Tests It |
| --- | --- | --- | --- |
| **DNS** | 53 | TCP / UDP | Used in DNS poisoning and DNS amplification (DDoS) attacks. |
| **DHCP** | 67, 68 | UDP | Port 67 is the server, 68 is the client. Associated with DHCP spoofing and starvation attacks. |
| **TFTP** | 69 | UDP | Trivial FTP. Requires no authentication. If you see this open on an exam firewall log, it is a massive security risk. |
| **NTP** | 123 | UDP | Network Time Protocol. Critical for cryptography and digital certificates (if time is out of sync, certificates fail). |
| **SNMP** | 161, 162 | UDP | Used to monitor network devices. SNMPv1 and v2 are insecure; you must use **SNMPv3** for secure authentication and encryption. |
| **SMB** | 445 | TCP | Server Message Block (Windows file sharing). This is the primary vector for ransomware lateral movement (like WannaCry). |
| **RDP** | 3389 | TCP | Remote Desktop Protocol. A massive target for brute-force attacks; should never be exposed directly to the open internet. |
| **SMTP** | 25 | TCP | Unencrypted email routing. Secure mail submission typically uses port 587. |

## Forensics: Order of Volatility

When collecting evidence, always collect the most volatile data first before it is lost or overwritten.

1. **CPU Registers and Cache Memory** (Highly volatile, lasts nanoseconds)
2. **Routing Table, ARP Cache, Process Table, Kernel Statistics**
3. **RAM (Random Access Memory)**
4. **Temporary File Systems / Swap Space / Pagefile**
5. **Local Disk** (Hard drives, SSDs)
6. **Remote Logging and Monitoring Data**
7. **Physical Configuration and Network Topologies**
8. **Archival Media** (Backups, DVDs, tapes)

## Cryptography Algorithms

A common trap on the exam is mixing up Symmetric, Asymmetric, and Hashing algorithms.

### Symmetric Algorithms (Same key for encrypt/decrypt - fast, good for bulk data)

* **AES** (Advanced Encryption Standard - current gold standard)
* **DES / 3DES** (Legacy)
* **Blowfish / Twofish**
* **RC4** (Stream cipher, deprecated/insecure)

### Asymmetric Algorithms (Public/Private key pair - slower, good for key exchange & digital signatures)

* **RSA** (Rivest-Shamir-Adleman - relies on factoring large prime numbers)
* **ECC** (Elliptic Curve Cryptography - highly efficient, ideal for mobile/IoT devices)
* **Diffie-Hellman** (Used specifically for secure key exchange over an insecure network)
* **DSA** (Digital Signature Algorithm)

### Hashing Algorithms (One-way mathematical function - provides integrity)

* **SHA-1, SHA-2, SHA-3** (Secure Hash Algorithm)
* **MD5** (Message Digest 5 - fast but collision-prone/deprecated)
* **RIPEMD**

## Access Control Models

How operating systems and software restrict access to objects.

* **MAC (Mandatory Access Control):** Strictest model. Uses security clearances (Confidential, Secret, Top Secret) and data labels. Users cannot change access policies. Common in government/military.
* **DAC (Discretionary Access Control):** Flexible model. The creator/owner of the data decides who gets access. Used in standard Windows/macOS operating systems.
* **RBAC (Role-Based Access Control):** Access is based on the user's job function or role (e.g., HR, IT, Finance) rather than individual identity. Easiest for managing high turnover.
* **ABAC (Attribute-Based Access Control):** Next-gen model. Grants access based on specific attributes like time of day, location, device health, and network type. Commonly used with Zero Trust architectures.
* **RuBAC (Rule-Based Access Control):** Access is determined by system-enforced rules, such as firewall ACLs or router configurations.

## Authentication Factors (MFA)

Multi-Factor Authentication requires at least two *different* categories from this list (e.g., two passwords is just single-factor).

* **Something you know:** Password, PIN, security question.
* **Something you have:** Smart card, hardware token (YubiKey), smartphone (Authenticator app).
* **Something you are:** Biometrics (fingerprint, retina scan, facial recognition).
* **Somewhere you are:** Geolocation, IP address, GPS data.
* **Something you do:** Keystroke dynamics, behavioral patterns, signature.

## Cloud Security & Architecture Models

* **IaaS (Infrastructure as a Service):** Vendor provides hardware, network, and hypervisor. You manage OS, applications, and data (e.g., AWS EC2, Azure VMs).
* **PaaS (Platform as a Service):** Vendor manages hardware and OS. You only manage the application and data (e.g., AWS Elastic Beanstalk, Heroku).
* **SaaS (Software as a Service):** Vendor manages everything. You only manage your user accounts and data inputs (e.g., Microsoft 365, Salesforce).
* **Public Cloud:** Multi-tenant, shared over the internet.
* **Private Cloud:** Single-tenant, dedicated infrastructure for one organization.
* **Hybrid Cloud:** Mix of public and private clouds (e.g., keeping sensitive data on a private cloud while using public cloud for heavy compute bursts).
* **Community Cloud:** Infrastructure shared among organizations with common goals or compliance needs (e.g., universities or government agencies).

## Data Roles and Responsibilities

Understanding who is legally and operationally responsible for data.

* **Data Owner:** The senior executive/management ultimately legally responsible for the data and for deciding its classification level.
* **Data Controller:** Determines the "why" and "how" personal data is processed (crucial concept in GDPR).
* **Data Processor:** A third-party entity that processes data on behalf of the Data Controller (e.g., a cloud service provider hosting the database).
* **Data Custodian (or Steward):** The IT staff member who implements the technical controls (backups, encryption, access management) mandated by the Data Owner.

## CompTIA Troubleshooting Methodology

You will see scenario-based questions asking what a technician should do *next* based on this exact sequence.

1. **Identify the problem:** Gather information, duplicate the problem if possible, and question users.
2. **Establish a theory of probable cause:** Consider multiple approaches, starting with the obvious.
3. **Test the theory to determine the cause:** Once the theory is confirmed, determine the next steps. If it is incorrect, re-establish a new theory.
4. **Establish a plan of action:** Figure out how to resolve the problem and identify any potential negative effects of your fix.
5. **Implement the solution or escalate:** Apply the fix yourself, or pass it up to a higher tier if you lack permissions or resources.
6. **Verify full system functionality:** Test the system and, if applicable, implement preventive measures.
7. **Document findings, actions, and outcomes:** Add the issue and solution to the knowledge base.

## The Cyber Kill Chain (Lockheed Martin)

This framework describes the sequential phases an external attacker goes through to infiltrate a network and steal data.

1. **Reconnaissance:** The attacker gathers information on the target (e.g., harvesting email addresses, finding open ports).
2. **Weaponization:** The attacker creates a malicious payload tailored to the target's vulnerabilities (e.g., crafting a malicious PDF).
3. **Delivery:** The weapon is transmitted to the target (e.g., sending a phishing email or hosting it on a compromised website).
4. **Exploitation:** The malicious code is triggered on the victim's machine.
5. **Installation:** The malware installs a backdoor or persistence mechanism to ensure the attacker maintains access.
6. **Command and Control (C2):** The compromised system reaches out to the attacker's server to receive instructions.
7. **Actions on Objectives:** The attacker achieves their final goal (e.g., data exfiltration, ransomware encryption, destruction).

## Penetration Testing Phases

While similar to the Kill Chain, this represents the authorized, ethical hacking process.

1. **Planning and Scoping:** Defining the rules of engagement, target boundaries, and getting legal authorization (sign-off).
2. **Information Gathering / Reconnaissance:** OSINT (Open Source Intelligence) and passive gathering.
3. **Scanning and Enumeration:** Active probing of the network for open ports, services, and known vulnerabilities.
4. **Exploitation:** Actively attacking the discovered vulnerabilities to gain unauthorized access.
5. **Post-Exploitation:** Privilege escalation, pivoting to other internal systems, and establishing persistence.
6. **Reporting:** Documenting the successful exploits, business impact, and mitigation recommendations.

## The Data Lifecycle

Organizations must apply different security controls depending on where data is in this sequence.

1. **Create / Collect:** Data is generated or acquired (classify and tag data at this stage).
2. **Store:** Data is committed to storage (apply encryption at rest and access controls).
3. **Use:** Data is viewed, processed, or modified in active memory (apply endpoint protection and encryption in use).
4. **Share:** Data is exchanged between users or organizations (apply encryption in transit and DLP).
5. **Archive:** Data is moved to long-term storage for compliance or legal reasons.
6. **Destroy:** Data is permanently wiped or physically destroyed when no longer needed (crypto-erasure, shredding, degaussing).

## Digital Forensics Process

If an incident escalates to a legal or criminal investigation, this order ensures evidence remains admissible in court.

1. **Identification:** Recognizing that an incident has occurred and identifying potential evidence.
2. **Collection:** Gathering the evidence according to the Order of Volatility. *This is where the Chain of Custody document is initiated.*
3. **Analysis:** Examining the collected data using forensic tools (always analyzing a bit-by-bit copy, never the original data).
4. **Reporting:** Presenting the findings in a formal document suitable for management or a court of law.

## The Access Control Flow (IAAA)

The logical progression of how systems grant user access.

1. **Identification:** A user claims an identity (e.g., typing in a username or swiping an ID card).
2. **Authentication:** The system verifies the identity (e.g., entering a password or providing a fingerprint).
3. **Authorization:** The system checks what that authenticated user is allowed to do (e.g., applying Read/Write permissions).
4. **Accounting:** The system tracks and logs the user's actions (e.g., generating audit logs of accessed files).