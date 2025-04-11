# X) Summaries / Tiivistelmät

## Find Hidden Web Directories - Fuzz URLs with ffuf

- Ffuf is a fast, full featured web fuzzer tool that automates fuzzing.
- Ffuf can be used to find hidden paths on web servers: directories or files (e.g /secret, /.svn /admin). Ffuf can also fuzz: request headers, POST parameters, query strings etc.
- Ffuf uses wordlists/dictionaries in the discovery process by replacing a placeholder (FUZZ) in the target URL with each word from the list. It systematically tries every word in place of FUZZ to identify valid endpoints or params.
- Ffuf utilizes wordlists in the discovery process. It inserts each word from the wordlist (FUZZ = placeholder where each word goes) tries all the words from the list in place of FUZZ, like: into the target that’s being tested.

- **How to use ffuff:**
    - Note: detailed installation in task A)
    1.	Set up a target that mimics a web server with hidden paths/directories. (A  downloadable practice target is provided in the materials.)
    2.	Install ffuf
    3.	Download & use a wordlist/dictionary. 
    4.	Run ffuf on the target using a wordlist/dictionary. E.g. basic command for directory discovery: `ffuf -w <wordlist> -u <target-url>/FUZZ`
    5.	Results can be verified with browser or CURL
       
- **Filtering noise: unwanted HTTP responses:**
    - The target may respond with HTTP 200 OK for everything (including non-existent pages: “Nothing, nil, null, nada”), creating false positives. 
    - The solution is to filter out the unwanted responses based on common characteristics.
    - Filter options, e.g.:
        - `-fc`: filter by HTTP response status code
        - `-fs`: filter by HTTP response size (in bytes)
        - `-fw `: filter by number of words in the response
        - `-fl`: filter by number of lines


## ffuf README.md
- (TAI Still Fuzzing Faster (U fool). In HelSec Virtual meetup #1.)


## References / Lähteet:
- Karvinen 2023: Find Hidden Web Directories - Fuzz URLs with ffuf at https://terokarvinen.com/2023/fuzz-urls-find-hidden-directories/ 
- Hoikkala 2023: ffuf README.md at https://github.com/ffuf/ffuf/blob/master/README.md 
(- Hoikkala "joohoi" 2020: Still Fuzzing Faster (U fool). HelSec Virtual meetup #1 at https://www.youtube.com/watch?v=mbmsT3AhwWU )



# A) Fuzzzz. Ratkaise dirfuz-1 artikkelista Karvinen 2023: Find Hidden Web Directories - Fuzz URLs with ffuf.
-


## References / Lähteet:
- Karvinen 2023: Find Hidden Web Directories - Fuzz URLs with ffuf at https://terokarvinen.com/2023/fuzz-urls-find-hidden-directories/

# B) Fuff me. Asenna FuffMe-harjoitusmaali. Karvinen 2023: Fuffme - Install Web Fuzzing Target on Debian
-

## References / Lähteet:
-Karvinen 2023: Fuffme - Install Web Fuzzing Target on Debian at https://terokarvinen.com/2023/fuffme-web-fuzzing-target-debian/ 


# C-I) Ratkaise FuffMe harjoitukset

-
### C) Basic Content Discovery
## D) Content Discovery With Recursion
## E) Content Discovery With File Extensions
## F) No 404 Status
## G) Param Mining
## H) Rate Limited
## I) Subdomains - Virtual Host Enumeration

## References / Lähteet:
- Karvinen 2023: Fuffme - Install Web Fuzzing Target on Debian at https://terokarvinen.com/2023/fuffme-web-fuzzing-target-debian/ 


# Tehtävänanto:
- Karvinen 2025 - Tunkeutumistestaus at https://terokarvinen.com/tunkeutumistestaus/#h3-fuzzy
