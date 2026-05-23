# Exploiting an Open SSH Port
## Initial Port Scan Including Service Versions
I ran an Nmap scan on the vulnerable host to enumerate open ports, as well as their versions. Understanding what services are running as well as the versions can help me reveal any known vulnerabilities that may be exploitable.
<img width="640" height="765" alt="port service-enum" src="https://github.com/user-attachments/assets/3fc34044-e293-4616-8d8b-d2069d812082" />


## SSH Brute Force Attack
My first step was locating the module in metasploit to run this attack. I used auxiliary/scanner/ssh/ssh_login. I created two text files to pass into the module, one containing usernames, and one with passwords.  

<img width="186" height="261" alt="SSH-users pass txtfiles" src="https://github.com/user-attachments/assets/78f9fba5-e1a2-400d-b4e7-dbf95059be9c" />    

I then set all of parameters I needed to run the exploit. I set the password file I created as the PASS_FILE, my username list as USER_FILE, set the RHOSTS as the metasploitable machine, and then changed VERBOSE to true to see each attempt.
<img width="417" height="629" alt="ssh_loginexploit_set" src="https://github.com/user-attachments/assets/23ffbfa0-4c1f-43cd-97f7-b635d993d869" />  

I started the attack, and it tested user credential combinations using the text files, against the target machine on port 22/SSH. Eventually I hit a success and confirmed a set of valid credentials.  

<img width="496" height="341" alt="SSH-exploit-success" src="https://github.com/user-attachments/assets/13a56e4e-8b2d-4bf8-a6c5-db30420a1a1b" />  

I tried authenticating to the SSH server with the credentials, and after changing the encryption type, was able to successfully login with remote shell capabilities.  

<img width="874" height="622" alt="successful-ssh-shell" src="https://github.com/user-attachments/assets/9dce1e8e-c7f0-4625-a3bc-419d446ff04e" />  

- CONCLUSION -- Strong password policies are crucial in any aspect of security, and can make or break any network. In a real-world environment, after identifying this very weak username/password combination, my recommendation would be to enforce stricter password policies, or even implement SSH key based authentication for a hightened level of security.
