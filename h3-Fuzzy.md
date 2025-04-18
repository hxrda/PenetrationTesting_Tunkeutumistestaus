# X) Summaries / Tiivistelmät

## Find Hidden Web Directories - Fuzz URLs with ffuf

- Ffuf is a fast, full featured web fuzzer tool that automates fuzzing.
  
- Ffuf can be used to find hidden paths on web servers: directories or files (e.g /secret, /.svn /admin). Ffuf can also fuzz: request headers, POST parameters, query strings etc.
  
- Ffuf uses wordlists/dictionaries in the discovery process by replacing a placeholder (FUZZ) in the target URL with each word from the list. It systematically tries every word in place of FUZZ to identify valid endpoints or params.
  
- Ffuf utilizes wordlists in the discovery process. It inserts each word from the wordlist (FUZZ = placeholder where each word goes) tries all the words from the list in place of FUZZ, like: into the target that’s being tested.

**<ins>How to use ffuff</ins>:**
- Note: detailed installation in task A)
  
1.	Set up a target that mimics a web server with hidden paths/directories. (A  downloadable practice target is provided in the materials.)
2.	Install ffuf
3.	Download & use a wordlist/dictionary. 
4.	Run ffuf on the target using a wordlist/dictionary. E.g. basic command for directory discovery: `ffuf -w <wordlist> -u <target-url>/FUZZ`
5.	Results can be verified with browser or CURL
       
**<ins>Filtering noise: unwanted HTTP responses:</ins>**
- The target may respond with HTTP 200 OK for everything (including non-existent pages: “Nothing, nil, null, nada”), creating false positives. 
- The solution is to filter out the unwanted responses based on common characteristics.

- Filter options, e.g.:
    - `-fc`: filter by HTTP response status code
    - `-fs`: filter by HTTP response size (in bytes)
    - `-fw `: filter by number of words in the response
    - `-fl`: filter by number of lines


## ffuf README.md

**<ins>Basic usage:</ins>**

- Keywords:
  - `FUZZ` The main placeholder used in ffuf. Wherever the FUZZ -keyword is placed, the tool will substitute it with values from a wordlist. Can be used anywhere in the URL (`-u`), headers (`-h`) or POST data (`-d`)
    
- Options:
  - The readme.md and the help page (`ffuf -h`) provide a comprehensive list of options to use with ffuf
  - Includes options for HTTP, matchers, filters, inputs, outputs and other general options.  

**<ins>Advanced usage & detailed documentation:</ins>**

- ffuf wiki at https://github.com/ffuf/ffuf/wiki
- ffuf guide with real life usage examples by Michael Skelton at https://codingo.io/tools/ffuf/bounty/2020/09/17/everything-you-need-to-know-about-ffuf.html 

**<ins>Usage examples:</ins>**

- **1. Directory discovery**: `ffuf -w /path/to/wordlist -u https://target/FUZZ`
  
- **2. Virtual host discovery** to find hidden subdomains /virtual hosts on a server by fuzzing the Host – header: `ffuf -w /path/to/vhost/wordlist -u https://target -H "Host: FUZZ" -fs 4242`

- **3. GET parameter fuzzing**:
  - Fuzz parameter names: `ffuf -w /path/to/paramnames.txt -u https://target/script.php?FUZZ=test_value -fs 4242`
  - Fuzz parameter values (when param name is known): `ffuf -w /path/to/values.txt -u https://target/script.php?valid_name=FUZZ -fc 401`
    
- **4. POST data fuzzing**: `ffuf -w /path/to/postdata.txt -X POST -d "username=admin\&password=FUZZ" -u https://target/login.php -fc 401`
  
- **5. Execution time limit with maxtime (stops the fuzzing process after a specified time in seconds)**: 
  - Stop entire process (global):`ffuf -w /path/to/wordlist -u https://target/FUZZ -maxtime 60`
  - Stop current job, continue with next one: `ffuf -w /path/to/wordlist -u https://target/FUZZ -maxtime-job 60 -recursion -recursion-depth 2`
    
- **6. Using external mutator (script or program)** to modify or mutate the input data before sending it to the target, instead of generating values internally.


**<ins>Configurations:</ins>**

- The ffuf -tool checks for a default configuration file `ffufrc` which defines how  fuzzing should behave. The default config path is: `$XDG_CONFIG_HOME/ffuf/ffufrc`
- Configuration options provided on the CLI override the ones loaded from the default ffufrc file (except those allowing multiple values, like `-H`). 

**<ins>Interactive mode:</ins>**

- A feature that lets the user interact with the running ffuf scan in real-time. It allows adjustments to the scan through pausing the process instead of having to restart the whole scan.
- The interactive mode can be accessesd by pressing `ENTER` during ffuf execution,


## References / Lähteet:
- Karvinen 2023: Find Hidden Web Directories - Fuzz URLs with ffuf at https://terokarvinen.com/2023/fuzz-urls-find-hidden-directories/ 
- Hoikkala 2023: ffuf README.md at https://github.com/ffuf/ffuf/blob/master/README.md 



# A) Fuzzzz. Ratkaise dirfuz-1 artikkelista Find Hidden Web Directories - Fuzz URLs with ffuf.

**<ins>1. Set up a target:</ins>**

Download & run a local dummy server (dirfuzt-1) that mimics a web server with hidden directories:
- `wget https://terokarvinen.com/2023/fuzz-urls-find-hidden-directories/dirfuzt-1`
- `chmod 744 dirfuzt-1`  change permissions
- `./dirfuzt-1` run the server
  
  ![FUFF](images/h3-images/a_1.png)   
  
  ![FUFF](images/h3-images/a_11.png)        

Access the dummy locally from the browser & verify that the test environment works: 
- `http://127.0.0.2:8000`
  
  ![FUFF](images/h3-images/a_2.png)        

**<ins>2. Install ffuf</ins>**

Download and extract a release of ffuf:
-  `wget https://github.com/ffuf/ffuf/releases/download/v2.1.0/ffuf_2.1.0_linux_amd64.tar.gz` (latest release)
- `tar -xf ffuf_2.1.0_linux_amd64.tar.gz`
  
  ![FUFF](images/h3-images/a_3.png)        

Run the ffuf tool to test that it works:
- `./ffuf` (from current directory)

  ![FUFF](images/h3-images/a_4.png)        

**<ins>3. Download & use a wordlist/dictionary. </ins>**

- Selected dictionary: Seclists
- `wget https://raw.githubusercontent.com/danielmiessler/SecLists/master/Discovery/Web-Content/common.txt`
- `head -3 common.txt ` Shows the first 3 lines of the .txt file & provides a quick preview of 
- ` wc -l common.txt `  Counts the number of lines (entries) in common.txt. Each entry represents a URL /path tested with fuzzing.
  
  ![FUFF](images/h3-images/a_5.png)        

**<ins>4. Run Ffuf on the target </ins>**

Disconnect the internet (to avoid leaking packets to the Internet)

Check ffuf parameters:
- `./ffuf` 
- `./ffuf |& less` Paginates the output
  
Run Ffuf on the target:
- `./ffuf -w common.txt -u http://127.0.0.2:8000/FUZZ`
  - The command replaces `FUZZ`placeholder with each word in the common.txt dictionary and sends requests to the specified target.
  - `w` Refers to the wordlist to be used
  - `u` Refers to the target URL
  
  ![FUFF](images/h3-images/a_6.png)      

Filter out noise/false positives:
- The target returns a long list of results including false positives (non-existent pages giving HTTP status 200 OK). The false positives will be filtered out from the results based on common qualities, in this case the HTTP response size which is 154 bytes (other commonalities incl. words and lines). 
- ` ./ffuf -w common.txt -u http://127.0.0.2:8000/FUZZ -fs 154 `
  
  ![FUFF](images/h3-images/a_7.png)    
 
**<ins>5. Verify results with browser or CURL</ins>**

- Admin page: 
  - Browser - `http://127.0.0.2:8000/wp-admin`
  - CURL  - `curl http://127.0.0.2:8000/wp-admin`

- Version control (git) related pages:
  - Browser - `http://127.0.0.2:8000/.git`, `http://127.0.0.2:8000/.git/logs`  etc.
  - CURL - ` curl http://127.0.0.2:8000/.git/index`, ` curl http://127.0.0.2:8000/.git/logs`etc.
    
  ![FUFF](images/h3-images/a_8.png)        
  ![FUFF](images/h3-images/a_9.png)        
  ![FUFF](images/h3-images/a_15.png)

The hidden directories have been fuzzed succesfully. 


## References / Lähteet:
- Karvinen 2023: Find Hidden Web Directories - Fuzz URLs with ffuf at https://terokarvinen.com/2023/fuzz-urls-find-hidden-directories/

# B) Fuff me. Asenna FuffMe-harjoitusmaali. 

**<ins>Install prerequisites for the FfufMe target:</ins>**  

- `sudo apt-get update`
- `sudo apt-get install docker.io git` 
  - Installs Docker and Git. Reference materials include “ffuf” in the installation, but that is excluded here as it has already been installed in task A.
    
- If docker service isn’t automatically started: ` sudo systemctl start docker `

**<ins>Build practice target Docker container: </ins>**

  - `git clone https://github.com/adamtlangley/ffufme`
  - `cd ffufme/`
  - `sudo docker build -t ffufme .`

**<ins>Run the FuffMe - local practice target: </ins>**

- `sudo docker run -d -p 80:80 ffufme`

**<ins>Verify successful installation / that the target works: </ins>**

- Browser: `http://localhost`
- CURL: `curl localhost` or `curl -si localhost|grep title`
  
  ![FUFF](images/h3-images/b_1.png)
  ![FUFF](images/h3-images/b_2.png)
  ![FUFF](images/h3-images/b_3.png)
  
- **Note:** ZAP prozy needs to be disabled in FoxyProxy. Otherwise the browser gives the error: “The proxy server is refusing connections. Firefox is configured to use a prozxy server that is refusing connections”.
  
**<ins> Install wordlists/dictionaries : </ins>**
  
The dictionaries will be installed inside a new directory within the home directory:

    mkdir $HOME/wordlists
    cd $HOME/wordlists
    wget http://ffuf.me/wordlist/common.txt
    wget http://ffuf.me/wordlist/parameters.txt
    wget http://ffuf.me/wordlist/subdomains.txt
    cd -


## References / Lähteet:
-Karvinen 2023: Fuffme - Install Web Fuzzing Target on Debian at https://terokarvinen.com/2023/fuffme-web-fuzzing-target-debian/ 


# C-I) Ratkaise FuffMe harjoitukset

## C) Basic Content Discovery

**Command:**
- `ffuf -w $HOME/wordlists/common.txt -u http://localhost/cd/basic/FUZZ`
  
- **Note**: This task was partially covered in the provided materials for setting up the Ffufme target. The only difference from the example materials is to change the domain part (ffuf.me in http://ffuf.me/cd/basic/FUZZ) to localhost since the former results in an error.

  ![FUFF](images/h3-images/c_1.png)
  
**Results:**
- Paths discovered: `class` & `development.log`
  
  ![FUFF](images/h3-images/c_2.png)

**Verifying in browser or with curl:**
   
   ![FUFF](images/h3-images/c_3.png)
    
   ![FUFF](images/h3-images/c_4.png)

## D) Content Discovery With Recursion

**Command:**
- `ffuf -w ~/wordlists/common.txt -recursion -u http://localhost/cd/recursion/FUZZ `

- Performs recursive content discovery.
- The `-recursion` flag enables ffuf to automatically scan inside the directories it discovers. I.e., if a directory is found, ffuf will continue to fuzz inside it and further inside any subdirectories until no new results/subdirectories/paths are found.

**Results:**
- Discovered paths (within a nested directory structure): `/admin`, `/admin/users` and `/admin/users/96`
  
  ![FUFF](images/h3-images/d_1.png)

**Verifying in browser or with curl:**

  ![FUFF](images/h3-images/d_2.png)


## E) Content Discovery With File Extensions

**Command:**
- `ffuf -w ~/wordlists/common.txt -e .log -u http://localhost/cd/ext/logs/FUZZ `
  
- Discovers files with specific extensions (e.g. .log).
- The `-e` flag appends the specified file extension(s) to each word in the wordlist. In this case, `.log` is added to every entry in common.txt, so ffuf will look for paths like /logs/debug.log, /logs/error.log, etc.

**Results:**
- Discovered one matching file:`/logs/users.log`
  
  ![FUFF](images/h3-images/e_1.png)

**Verifying in browser or with curl:**
  
  ![FUFF](images/h3-images/e_2.png)

## F) No 404 Status

**Command:**
- **Basic ffuf scan:** `ffuf -w ~/wordlists/common.txt -u http://localhost/cd/no404/FUZZ`
- **Filtered ffuf scan:** `ffuf -w ~/wordlists/common.txt -u http://localhost/cd/no404/FUZZ -fs 669`
  
- Some web servers return a `200 OK` status along with a "Page Not Found" message for non-existent pages, instead of a HTTP `404 Not Found` status. This results in false positives in fuzzing.
  
  ![FUFF](images/h3-images/f_1.png)
  …
  
  ![FUFF](images/h3-images/f_11.png)
  …
  
  ![FUFF](images/h3-images/f_12.png)

- The false positives can be filtered out based on common characteristics, in this case the response size of of 669 bytes.
- The `-fs` flag excludes/filters out results of the specified byte size.

**Results:**
- Discovered one matching result: `/secret`
  
  ![FUFF](images/h3-images/f_3.png)

**Verifying in browser or with curl:**

  ![FUFF](images/h3-images/f_4.png)


## G) Param Mining

**Command:**
- The URL  `http://localhost/cd/param/data` returns an HTTP status code 400 Bad Request, with a message "Required parameter missing". This suggests the server is expecting a GET parameter which is missing from the initial URL.

  ![FUFF](images/h3-images/g_1.png)

- **GET parameter fuzzing:** `ffuf -w ~/wordlists/parameters.txt -u http://localhost/cd/param/data?FUZZ=1
- GET parameter fuzzing is similar to directory fuzzing, but targets URL parameters/parameter name instead (`-u https://target-url?FUZZ=test_value`). The FUZZ keyword is placed where the parameter name would go, while 1 is a test value.
- If the correct parameter is found, the server should return a HTTP 200 OK response and no more show the "missing parameter" message.
  
**Results:**
- Parameter found: `debug`
  
  ![FUFF](images/h3-images/g_2.png)

**Verifying in browser or with curl:**

  ![FUFF](images/h3-images/g_3.png)


## H) Rate Limited

**Command:**
- **Initial fuzzing:** `ffuf -w ~/wordlists/common.txt -u http://localhost/cd/rate/FUZZ -mc 200,429`
  
  ![FUFF](images/h3-images/h_1.png)

- **Rate limited fuzzing:** `ffuf -w ~/wordlists/common.txt -t 5 -p 0.1 -u http://localhost/cd/rate/FUZZ -mc 200,429`
  
- Some services are rate limited, meaning only certain amount of requests per second are allowed. In this case, the server limits the number of requests to 50 per second, exceeding that will result in 429 errors.
- The `-p 0.1` flag adds a 0.1 second delay between each request per thread and the `-t 5` flag runs 5 threads in parallel (default: 40). Combined, the total number of requests is kept around 50/s.
- The `mc 200,429` flag tells ffuf to only display HTTP 200 OK and 429 Too Many Requests responses.

**Results:**
- Discovered directory: `/oracle`
- The scan is much slower due to the rate limit.
  
  ![FUFF](images/h3-images/h_2.png)

**Verifying in browser or with curl:**

  ![FUFF](images/h3-images/h_3.png)


## I) Subdomains - Virtual Host Enumeration

**Command:**
- **Basic virtual host discovery:** `ffuf -w ~/wordlists/subdomains.txt -H "Host: FUZZ.ffuf.me" -u http://localhost `
- **Filtered virtual host discovery:** `ffuf -w ~/wordlists/subdomains.txt -H "Host: FUZZ.ffuf.me" -u http://localhost -fs 1495 `
  
- In this case, the fuzzing targets virtual host-based subdomains. The wordlist is injected into the Host header as the subdomain (e.g. Host: redhat.ffuf.me).
- `H "Host: FUZZ.ffuf.me"` inserts each entry in the wordlist as a subdomain.
- Irrelevant responses (size of 1495 bytes) are filtered out with the `-fs` flag.
  
**Results:**
- Discovered valid subdomain: `redhat` (`redhat.ffuf.me`)
  
  ![FUFF](images/h3-images/i_1.png)
  
  ![FUFF](images/h3-images/i_2.png)

**Verifying in browser or with curl:**  

  ![FUFF](images/h3-images/i_3.png)


## References / Lähteet:
- Karvinen 2023: Fuffme - Install Web Fuzzing Target on Debian at https://terokarvinen.com/2023/fuffme-web-fuzzing-target-debian/ 
- Hoikkala 2023: ffuf README.md at https://github.com/ffuf/ffuf/blob/master/README.md
- Langley, A. (2025). FFUF.me - Target practice for ffuf.  Available at: http://ffuf.me/
  

# Tehtävänanto:
- Karvinen 2025 - Tunkeutumistestaus at https://terokarvinen.com/tunkeutumistestaus/#h3-fuzzy
