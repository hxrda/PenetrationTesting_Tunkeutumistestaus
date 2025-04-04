# X) Summaries/ Tiivistelmät

## OWASP 2021: OWASP Top 10:2021

[A01:2021 – Broken Access Control](https://owasp.org/Top10/A01_2021-Broken_Access_Control/)

-	Broken access control is ranked 1st in the 2021 list of top 10 web application security risks. It’s a major security risk found in 94% of evaluated web applications.
-	Broken access control occurs when users can access data or perform actions beyond their intended permissions. Proper enforcement of restrictions ensures users can only interact within their designated access levels.
  
-	Common vulnerabilities include:  
    -	Failure to enforce the principle of least privilege or deny-by-default policies, allowing users to gain more access than necessary.
    -	Privilege escalation by tampering with tokens (e.g., JWTs, access control tokens), cookies, or hidden fields to access admin-level functions.
    -	Bypassing restrictions by modifying URLs, API requests, or the application's internal state.
    -	CORS misconfigurations, permitting access from unauthorized or untrusted origins/domains.

-	Prevention:
    -	Enforce access control on the server side (or in serverless APIs) to prevent attackers from bypassing checks or manipulating metadata.
    -	Deny access by default.
    -	Centralize access control mechanisms and apply them consistently throughout the application.
    -	Monitor, log, and restrict access attempts. Alert admins to suspicious patterns, such as repeated failures.
    -	Invalidate session tokens after logout to prevent unauthorized reuse.

[A10:2021 – Server-Side Request Forgery (SSRF)](https://owasp.org/Top10/A10_2021-Server-Side_Request_Forgery_%28SSRF%29/ )

- SSFR ranks 10th  in the 2021 OWASP Top 10 list. While it currently has a low incidence rate (2.72%), its severity/impact is growing higher. The incidence rate of SSRFs is expected to increase in the future.
- SSRF occurs when a web app lets users request external resources but doesn’t properly check/validate the URLs provided by the users. This potentially allows attackers to trick the app into sending requests to unexpected destinations even within protected networks.
- Modern web applications are more susceptible to SSRFs.
  
- Prevention:
    - **Network level defense:** Enforce strict network segmentation and "deny by default" firewall rules to block unnecessary internal traffic and limit the impact of SSRF.
    - **Application level defense:** At the application level, validate and sanitize user inputs, allow only trusted URLs (positive allow list for URL schemas, port, destination), and disable HTTP redirections.
    - **Other security measures:**  Avoid placing security-critical services on exposed/front systems and use encryption for sensitive internal traffic.


## PortSwigger Academy: 

[Insecure direct object references (IDOR)](https://portswigger.net/web-security/access-control/idor)

- A type of access control vulnerability 
- Occurs when a web application directly accesses data, resources, or functions based on user-supplied input.
- Without proper access controls, attackers can exploit this vulnerability by altering user-controlled input/ parameter values to access or modify unauthorized information. Changing URL parameters is a common use case
- Impact: Can lead to horizontal or vertical privilege escalation  
- Examples:
    - **Direct references to database objects:** e.g. if a URL uses `…?customer_number=132355` for retrieving account details, the customer number can be changed to access other customers’ data.
    - **Direct references to static files:** e.g. if files are stored with predictable names (e.g., `/12144.txt`), the filename in the URL can be modified to access sensitive information.


[Path traversal](https://portswigger.net/web-security/file-path-traversal)

- A type of access control vulnerability.
- Allows attackers to access (read or sometimes write) arbitrary files on a server beyond their intended access permissions. These files include e.g., application data, credentials, and system files.
- Exploited by manipulating URL file paths using valid directory traversal sequences (e.g., `../`) to access files at unintended locations. The sequence `../` is valid within a file path and moves up one level in the directory structure.  
    - Example: A URL request like `?filename=../../../etc/passwd` can retrieve files from the server’s root directory.

- Common prevention measures: Avoiding using user input in file paths, validating input against a whitelist or permitted content, ensuring the resolved file path remains within the intended directory.
- While many applications implement defenses against path traversal attacks, but various techniques exist to bypass them
- Valid directory traversal sequences:
    - `../` Works for both Unix-based & Windows systems
    - `..\` Windows systems only


[Server-side request forgery (SSRF)](https://portswigger.net/web-security/ssrf)
-

[Cross-site scripting](https://portswigger.net/web-security/cross-site-scripting)
-

[Server-side template injection (SSTI)](https://portswigger.net/web-security/server-side-template-injection)
-

## References/ Lähteet:
- A01:2021 - Broken Access Control at https://owasp.org/Top10/A01_2021-Broken_Access_Control/
- A10:2021 - Server-Side Request Forgery (SSRF) at https://owasp.org/Top10/A10_2021-Server-Side_Request_Forgery_%28SSRF%29/
- Insecure direct object reference (IDOR) at https://portswigger.net/web-security/access-control/idor
- Path traversal at https://portswigger.net/web-security/file-path-traversal
- Server-side request forgery (SSRF) at https://portswigger.net/web-security/ssrf
- Cross-site scripting at https://portswigger.net/web-security/cross-site-scripting
- Server-side template injection (SSTI) at https://portswigger.net/web-security/server-side-template-injection

# A) Totally Legit Sertificate. Asenna OWASP ZAP, generoi CA-sertifikaatti, ja asenna se selaimeesi. Laita ZAP proxyksi selaimeesi. Laita ZAP sieppaamaan myös kuvat, niitä tarvitaan tämän kerran kotitehtävissä. Osoita, että hakupyynnöt ilmestyvät ZAP:n käyttöliittymään.

## References/ Lähteet:

# B) Kettumaista. Asenna "FoxyProxy Standard" Firefox Addon, ja lisää ZAP proxyksi siihen. Käytä FoxyProxyn "Patterns" -toimintoa, niin että vain valitsemasi weppisivut ohjataan Proxyyn.

## References/ Lähteet: 

# C-J) PortSwigger Labs. Ratkaise tehtävät. Selitä ratkaisusi: mitä palvelimella tapahtuu, mitä eri osat tekevät, miten hyökkäys löytyi, mistä vika johtuu.

## References/ Lähteet: 

#K) Asenna pencode ja muunna sillä jokin merkkijono (encode a string).

## References/ Lähteet:

# I) Mitmproxy. Asenna MitmProxy. Esittele sitä terminaalissa (TUI). Ota TLS-purku käyttöön. Poimi historiasta hakupyyntö, muokkaa sitä ja lähetä uudelleen.

## References/ Lähteet:

# M) Ratkaise lisää PortSwigger Labs -tehtäviä. Kannattaa tehdä helpoimmat "Apprentice" -tason tehtävät ensin.

## References/ Lähteet:


# Tehtävänanto:
- Karvinen 2025 - Tunkeutumistestaus at https://terokarvinen.com/tunkeutumistestaus/
