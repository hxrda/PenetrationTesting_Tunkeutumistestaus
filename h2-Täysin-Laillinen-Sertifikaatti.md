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

- 
## PortSwigger Academy: 

## References/ Lähteet:
- A01:2021 - Broken Access Control at https://owasp.org/Top10/A01_2021-Broken_Access_Control/
- A10:2021 - Server-Side Request Forgery (SSRF) at https://owasp.org/Top10/A10_2021-Server-Side_Request_Forgery_%28SSRF%29/ 

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
