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
-

## The Ultimate Kali Linux Book: Understanding Active Directory
-

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
