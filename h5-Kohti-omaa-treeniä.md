# X) Summaries / Tiivistelmät

## Start Your Research with a Review Article

- A **review article** synthesizes existing research on a topic. It provides an overview of current knowledge, common research methods, open questions, and suggestions for future directions/research.
- Starting with a review article is the most efficient way to build a strong foundational understanding of a new topic/ field.
  
- **Guidelines for selecting articles/papers:**
	- Choose recent publications, preferably published within the last two years
	- Choose articles published in esteemed, peer-reviewed journals with a solid reputation, assessed through classification systems like the **JUFO rating** (levels 1–3) or the **Impact Factor (IF)**.
   
- **Tools for finding and assessing articles:**
	- **[Google Scholar](https://scholar.google.com/ncr)**: Search for articles by combining a topic with the word "review." To access more full-text articles for free, add your university in Settings → Library Links.
	- **[JUFO portal](https://jfp.csc.fi/jufoportal)**: A classification system for checking the quality/ reputation of publication channels. Journals rated JUFO 1, 2, or 3 are considered good-quality publications. 


## A Systematic Literature Review on the Characteristics and Effectiveness of Web Application Vulnerability Scanners 

JUFO Classification: Level 1 (Published in IEEE Access)

The summary is based on a surface-level review of the article rather than an in-depth study of its contents (Article length: 20 pages)

**Purpose and scope:**
- A systematic literature review of Web Application Vulnerability Scanners (WVSs), which are currently the primary tools used to detect vulnerabilities in web applications.
- Focus on:
	- Identifying the most researched/cited WVSs.
		- 30 scanners identified across 90 academic research papers.
	- Examining technical characteristics of these scanners.
	- Evaluating the effectiveness of these scanners in detecting common web vulnerabilities, especially those listed in the OWASP Top 10.

**Key findings:**
- Very few academic studies evaluate WVS features and detection capabilities in depth. Only 12 out of the 30 identified scanners were assessed for performance, and technical characteristics were often not included in academic sources.
- Most performance evaluations tested for only two OWASP Top 10 vulnerability types: SQL Injection (SQLi) and Cross-Site Scripting (XSS). Only one study evaluated a scanner against six OWASP vulnerability types.
- Reported vulnerability detection rates across WVSs varied significantly between studies:
	- SQLi: 0%–100%
	- XSS: 6%–100%

- The inconsistent results may be partially explained by the absence of standard benchmark web applications in evaluations. Most studies used non-standard applications, which makes replication difficult. Additionally, a lack of standardized terminology limits comparability.
- Due to large discrepancies in reported results, the WVSs cannot be reliably compared, and their effectiveness in detecting vulnerabilities remains questionable.
- As it stands in academic literature, no published evaluations exist that assess the usability or quality-of-use of WVSs.

**Recommendations for future research:**
- Developent of standard benchmark web applications to evaluate WVSs against all OWASP Top 10 vulnerabilities.
- Standardized evaluations using common vulnerability categories (e.g., OWASP) and consistent terminology/nomenclature.
- Inclusion of usability and quality-of-use assessments for WVS’s.


## References / Lähteet:
- Karvinen 2025: Start Your Research with a Review Article at https://terokarvinen.com/review-article/ 
- Alazmi, S. and De Leon, D.C., 2022. A systematic literature review on the characteristics and effectiveness of web application vulnerability scanners. IEEe Access, 10, pp.33200-33219.


# Establishing a VPN Connection to HackTheBox

**1. Download the OpenVPN configuration file from the HackTheBox website**
	![openvpn](images/h5-images/o_1.png)     

**2. Start the OpenVPN connection & wait for the initialization sequence to complete**

- `sudo openvpn ~/Downloads/starting_point_RH2025.ovpn`

**3. Verify VPN Connection**
- Check IP interfaces with `ifconfig` or `ip a`. A new interface `tun0` should be added.

	![openvpn](images/h5-images/o_3.png)

- Ping the HTB VPN gateway to confirm connection to the vpn server
	- `ping 10.10.16.1`
	![openvpn](images/h5-images/o_4.png)     

**4. Route/force all traffic through VPN only (pevent packet leaks)**

**Note:** These instructions for steps 4, 5, 7 were generated using ChatGPT 

- Add an iptables rule to block non-VPN traffic:
	- `sudo iptables -I OUTPUT ! -o tun0 -m conntrack --ctstate NEW -j DROP`
		- `-I OUTPUT` Inserts the rule into the OUTPUT chain, which controls outgoing traffic
		- `! -o tun0 `Applies/matches to traffic not going out through the `tun0` VPN interface.
		- `-m conntrack --ctstate NEW ` Matches new outbound connections (not ongoing/established ones)
		- `-j DROP` Drops/blocks any traffic that matches the above.
    
- This should ensure no traffic escapes outside the VPN tunnel.

**5. Confirm that all traffic is routed through the VPN (check for leaks)**

- Run ping tests - ping the internet and target network (HTB VPN Gateway):
	![openvpn](images/h5-images/o_6.png)
    
	![openvpn](images/h5-images/o_10.png)
 
	![openvpn](images/h5-images/o_8.png)     

**6. Confirm connection to the target machine**

- Ping the IP of the spawned HTB machine before proceeding with the associated tasks: `ping {target_IP}`

	![openvpn](images/h5-images/a_0.png) 
	
	![openvpn](images/h5-images/b_0.png)     

**7. Optional: revert iptables rule (undo VPN traffic restriction)**

- By default, iptables rules are stored in memory and won’t persist over system reboots.
- Reference for manual removal of the rule:
	- `sudo iptables -D OUTPUT ! -o tun0 -m conntrack --ctstate NEW -j DROP`

## References / Lähteet:
- Gordon, J. (2025). Introduction to Starting Point | Hack The Box Help Center. Available at: https://help.hackthebox.com/en/articles/6007919-introduction-to-starting-point#h_519931c2d4
- OpenAI (2025) ChatGPT response to user prompt on how to route/force all traffic through a VPN tunnel only to prevent packet leaks.

# A) HTB Dancing. Ratkaise HackTheBox.com: Starting Point: Tier 0: Dancing.
-
## References / Lähteet:


# B) HTB Responder. Ratkaise HackTheBox.com: Starting Point: Tier 1: Responder.
-
## References / Lähteet:
-

# C) Vapaaehtoinen (TBA?)
-
# D) Vapaaehtoinen (TBA?)
-
# E) Vapaaehtoinen (TBA?)
-



# Tehtävänanto:
- Karvinen 2025 - Tunkeutumistestaus at https://terokarvinen.com/tunkeutumistestaus/#h5-kohti-omaa-treenia

