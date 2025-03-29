# X) Summaries/ Tiivistelmät

## 1. Herrasmieshakkerit - Haavoittuvuuksien metsästäjä, vieraana Harry Sintonen | 0x23 

Harry Sintonen on tunnettu hakkeri, joka on löytänyt poikkeuksellisen monta korkean profiilin tietoturvahaavoittuvuutta. Hänellä on laaja kokemus sekä ohjelmisto- ja laitehaavoittuvuuksista että reaalimaailman tietoturvamurroista.
  
<ins>Kohteen valinta:</ins>  
- Kohteena voi usein olla fyysinen laite, johon on päästy käsiksi esim. harrastemielessä, tai hiljattain uutisoitu sovellusjulkaisu.

<ins>Miten haavoittuvuuksia etsitään kohteen valinnan jälkeen:</ins>  
1. Ennen haavoittuvuuksien etsimistä, perehdy kohdelaitteen tai -sovelluksen yleiskuvaan: sen normaaliin käyttötarkoitukseen ja sisältyviin toiminnallisuuksiin. Kiinnitä huomiota poikkeavuuksiin tai ominaisuuksiin, jotka voivat toimia lähtökohtana haavoittuvuuksien etsinnälle tai joissa on aiemmin havaittu turvallisuuspuutteita.
   
2. Eri vaihtoehtoja etsiä haavoittuvuuksia:
  - Laiteohjelmiston (firmware) päivitykset: Lataa valmistajan tarjoama laiteohjelmiston päivitys, jos se on saatavilla. Tutki, miten ohjelmisto toimii laitteessa ja analysoi sitä tarkemmin. Tämä voi vaatia takaisinmallinnusta (reverse engineering) haavoittuvuuksien löytämiseksi.
  - Verkkoliikenne: Tarkista, onko liikenne salattua vai salaamatonta. Jos liikenne on salattua (esim. TLS), voit yrittää asettua liikenteen väliin ja analysoida, miten laite validoi yhteyksiä ja minkä kohteen kanssa laite kommunikoi.
  - Psykologinen näkökulma (tiimidynamiikka): Haavoittuvuuksia voi, joissain tapauksissa löytyä "tylsistä" ominaisuuksista, jos niiden toteutus on delegoitu kokemattomille kehittäjille kokeneempien sijaan.

<ins>Kuinka haavoittuvuuksien etsiminen on muuttunut:</ins>  
- Haavoittuvuuksien löytäminen on vaikeampaa kuin ennen. Helposti hyödynnettäviä haavoittuvuuksia on yhä harvemmassa, ja laitteiden tekninen tietoturva on kehittynyt merkittävästi.
- Modernit kehitysmenetelmät, frameworkit ja työkalut noudattavat oletuksena hyviä tietoturvakäytäntöjä, mikä tekee haavoittuvuuksien löytämisestä ja hyödyntämisestä huomattavasti vaikeampaa.
- Haavoittuvuuspalkkio-ohjelmat (bug bountyt) ovat parantaneet tietoturvan tasoa, koska suuri määrä asiantuntijoita analysoi järjestelmiä aktiivisesti.
- Fuzzing eli automatisoitu testaus osana sovelluskehitystä on parantanut sovellusten tietoturvaa ja harventanut yksinkertaisten haavoittuvuuksien löytymistä.
- Toisaalta, koska sovellukset ovat nykyään monimutkaisempia, myös hyökkäyspinta on laajentunut merkittävästi verrattuna aiempaan.

<ins>Tarinoita haavoittuvuuksien etsimisestä & löytämisestä:</ins>  
- Merkittäville haavoittuvuuksille annetaan CVE (Common Vulnerabilities and Exposures) -pisteytys, joka arvioi haavoittuvuuden vakavuuden asteikolla 0–10. Mitä korkeampi pisteytys, sitä vakavampi haavoittuvuus.
- Sintonen on löytänyt ja raportoinut useita kymmeniä CVE:itä/haavoittuvuuksia (arvio 40–50 kpl).
- Podcastissa käydään läpi muutamia esimerkkitapauksia.

## 
## The Art of Hacking - Active Reconnaissance

<ins>Phases of Reconnaissance</ins>  
- Reconnaissance = Tiedustelu
- The success of subsequent Intrusion Kill Chain phases depend on the completion and success of the Recon phase.
- The Active Recon phase follows immediately after Passive Recon. 

1. Passive Reconnaissance:  
  - Involves gathering information about target from publicly available sources (e.g. web searches, social media profiles etc.), without directly interacting with the target system.
  - Advantages include invisibility to the target system and legality. Cons include potentially inaccurate information.
  
2. Active Reconnaissance:
  - Involves direct, active interaction with the target system to gather more specific information. Includes e.g. port scanning or scanning for security vulnerabilities
  - Advantages include the accuracy of collected information. Cons include the higher risk of getting detected since direct contact is involved (e.g. visibility in logs, setting of alarms) and illegality.

<ins>Active Recon Methodology & tools</ins>
- A solid methodology is important for shifting through large amounts of data to select the right systems and services to attack. 
- Steps in the Active recon methodology:
1. Port scanning
    - Tools: Nmap, Masscan, Udpprotoscanner  
2. Web service review  
    - Tools: EyeWitness  
3. Vulnerability scanning  
    - Network vulnerability scanners: OpenVAS, Nmap (limited), Nessus, Nexpose, Qualys
    - Web vulnerability scanners: Nikto, WPScan, SQLMap, Burp Suite, Zed Attack Proxy


## KKO:2003:36

## References:
- Herrasmieshakkerit. (2022). Haavoittuvuuksien metsästäjä, vieraana Harry Sintonen | 0x23. Available at: https://podcasts.apple.com/fi/podcast/haavoittuvuuksien-mets%C3%A4st%C3%A4j%C3%A4-vieraana-harry-sintonen/id1479000931?i=1000588315329
- Hutchins et al 2011: Intelligence-Driven Computer Network Defense Informed by Analysis of Adversary Campaigns and Intrusion Kill Chains, chapters Abstract, 3.2 Intrusion Kill Chain.
- Santos et al: The Art of Hacking (Video Collection): 4.3 Surveying Essential Tools for Active Reconnaissance. Available at: https://learning.oreilly.com/videos/the-art-of/9780135767849/9780135767849-SPTT_04_00/ 
- Finlex. (2003). KKO:2003:36 | Ennakkopäätökset | Korkein oikeus | Finlex. Available at: https://finlex.fi/fi/oikeuskaytanto/korkein-oikeus/ennakkopaatokset/2003/36 

# A) Install Kali Virtual Machine / Asenna Kali virtuaalikoneeseen

## References:

# B) Irroita Kali-virtuaalikone verkosta.

## References:

# C) Porttiskannaa 1000 tavallisinta tcp-porttia omasta koneestasi

## References:

# D) Asenna kaksi vapaavalintaista daemonia. Skannaa uudelleen, analysoi ja selitä erot

## References:

# E) Asenna Metasploitable 2 virtuaalikoneeseen

## References:

# F) Tee koneiden välille virtuaaliverkko.

## References:

# G) Etsi Metasploitable porttiskannaamalla

## References:

# H) Porttiskannaa Metasploitable huolellisesti ja kaikki portit. Poimi 2-3 hyökkääjälle kiinnostavinta porttia

## References:
