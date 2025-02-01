# Penetration-Testing-Project-0x24-RedTeam-VS-BlueTeam
# Technical Detailed Description of the Penetration Testing Report
# 1. Introduction
The penetration testing report, prepared by 0xMekawyRedTeam.FCDS, documents a comprehensive security assessment conducted for Saber’s Team between December 20, 2024, and December 25, 2024. The assessment focused on identifying vulnerabilities in both the internal network and web application environments. The report outlines the methodologies, tools, vulnerabilities discovered, and recommendations for remediation.

#2. Scope of Engagement
The engagement was divided into two primary phases:

1. Internal Network Vulnerability Assessment (NVA/PT): Focused on identifying vulnerabilities within the internal network, including servers, databases, and network infrastructure.

2. Web Application Assessment: Targeted the web application hosted at http://michaelwassef-001-site1.anytempurl.com/, written in ASP.NET and using MSSQL as the backend database.

The scope included:

1. Network Subnets: 192.168.10.0/24 and 192.168.30.0/24.

2. Web Application: The application had multiple roles (unauthenticated, user, admin), and role-based testing was performed.

3. Exclusions: Denial of Service (DoS) attacks and phishing/social engineering were excluded per client request.

# 3. Methodology
The penetration testing followed a structured methodology based on industry standards such as OWASP, PTES, NIST SP 800-115, and OSTMM. The process was divided into the following phases:

1. Reconnaissance:

- Passive reconnaissance using tools like Shodan, DNSRecon, and Amass.

- Subdomain enumeration and SSL/TLS certificate inspection.

- DNS brute-forcing with tools like dnstwist and nmap.

2. Scanning & Enumeration:

- Nmap for port scanning and service identification.

- Nikto for web server vulnerability scanning.

- Gobuster for directory brute-forcing.

- TestSSL.sh for identifying weak SSL/TLS configurations.

3. Exploitation:

- Manual and automated exploitation using tools like Burp Suite, Metasploit, and SQLmap.

- Focused on vulnerabilities such as IDOR, Race Conditions, and SQL Injection.

4. Post-Exploitation:

- Privilege escalation using tools like Linpeas.

- Data exfiltration and password cracking using John the Ripper, Steghide, and Stegcracker.

5. Reporting & Remediation:

- Detailed documentation of vulnerabilities, including proof of concept (PoC) and remediation recommendations.

# 4. Tools Used
The assessment utilized a variety of industry-standard tools, categorized by their purpose:

1. Reconnaissance:	Shodan, Sublist3r, DNSRecon, DNStwist, Whatweb, Dnslookup
2. Scanning & Enumeration:	Nmap, SSLscan, Dirb, Gobuster, Amass, Nikto, Oneforall
3. Exploitation:	SQLmap, Burp Suite Pro, Metasploit, Hydra, Medusa, Stegcracker, Hashcat
4. Post-Exploitation:	Linpeas, Enumpeas, Les.sh, Steghide, Simple HTTP Server
5. Password Cracking:	Hashcat, John the Ripper, Hydra, Medusa
Custom Scripting	Custom Python and Bash scripts for automating specific attack vectors

# 5. Vulnerabilities Discovered
The assessment identified several critical vulnerabilities, categorized by severity:

5.1 Web Application Vulnerabilities
1. Insecure Direct Object Reference (IDOR):

- Location: /Students/EditStudentProfile

- Description: An attacker could modify the students_ID parameter in the request to access or edit any student's profile.

- CVSS Score: 9.1 (Critical)

- Impact: Unauthorized access to sensitive student information (names, phone numbers, birth dates, passwords).

- Recommendation: Implement proper access controls, validate input parameters, and use indirect references.

2. Race Condition:

- Location: /Courses/Details/AddCourse

- Description: Multiple concurrent requests to the AddCourse endpoint could lead to duplicate course entries or data inconsistency.

- CVSS Score: 7.1 (High)

- Impact: Data inconsistency, system performance degradation, and incorrect reporting.

- Recommendation: Implement proper synchronization mechanisms and enforce unique constraints in the database.

# 5.2 Internal Network Vulnerabilities
1. Brute-Forcing SSH Password:

- Description: Weak SSH credentials allowed the team to brute-force the password (0xAl3aref) and gain access to the target machine (192.168.10.7).

- Impact: Unauthorized access to the internal network.

- Recommendation: Enforce strong password policies and implement multi-factor authentication (MFA).

2. Data Exfiltration:

- Description: The team discovered a hidden directory (.Flag(DummyFlag)) containing a Secret.zip file. After cracking the password (cocaine), they extracted an image (7ambola.jpg) with steganographically hidden data.

- Impact: Sensitive data leakage.

- Recommendation: Regularly audit file systems for hidden files and implement data loss prevention (DLP) mechanisms.

3. Steganography:

- Description: The team used Steghide and Stegcracker to extract a hidden flag (FL4G(L37'5_50LV3_57EG4NOGRAPHY)) from the image.

- Impact: Sensitive data leakage.

- Recommendation: Monitor for steganographic techniques and restrict the upload of suspicious files.

# 6. Failed Exploitation Attempts
Several exploitation attempts were unsuccessful, including:

1. SQL Injection: The target application was resistant to SQL injection attacks, possibly due to input validation or WAF protections.

2. FTP Access: Attempts to gain FTP access on the web server failed.

3. Accessing Web.Config File: The team was unable to access the web.config file, indicating proper file permissions.

4. Payload Delivery: Attempts to deliver a payload using Metasploit and Msfvenom were unsuccessful.
# 7. Conclusion
The penetration testing revealed critical vulnerabilities in both the web application and internal network. The implementation of the provided recommendations will significantly enhance Saber’s Team’s security posture. However, it is crucial to recognize that security is an ongoing process, and regular assessments are necessary to defend against evolving threats.
