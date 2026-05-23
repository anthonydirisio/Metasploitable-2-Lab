# Exploiting an Open SSH Port
## Initial Port Scan Including Service Versions
- I ran an Nmap scan on the vulnerable host to enumerate open ports and see what services are running on those ports. I also ran the command to identify the service versions, which can greatly help reveal any known vulnerabilities a specific service version may have that could be exploitable. Old unpatched service versions may have publicly known vulnerabilities that when taken advantage of, can be incredibly useful to an attacker.  

<img width="480" height="573.75" alt="port service-enum" src="https://github.com/user-attachments/assets/3fc34044-e293-4616-8d8b-d2069d812082" />

- As the header states, I will be exploiting port 22/SSH in this lab.


## SSH Brute Force Attack
- My first step was locating which metasploit module I wanted to use to run this attack. I used auxiliary/scanner/ssh/ssh_login. I then created two short text files to pass into the module, one containing usernames named users.txt, and one with passwords named pass.txt. Each list has the corresponding correct credential, that when run in the attack, will return a success.

<img width="186" height="261" alt="SSH-users pass txtfiles" src="https://github.com/user-attachments/assets/78f9fba5-e1a2-400d-b4e7-dbf95059be9c" />    

- I then set all of parameters I needed to run the exploit. I set the pass.txt file I created as the PASS_FILE, my users.txt file as USER_FILE, set the RHOSTS as the metasploitable machine, and then changed VERBOSE to true to see each attempt printed in the terminal.
<img width="417" height="629" alt="ssh_loginexploit_set" src="https://github.com/user-attachments/assets/23ffbfa0-4c1f-43cd-97f7-b635d993d869" />  

- Upon execution, metsploit tested each username against each password until it reached a successful combination, against the target machine on port 22/SSH. Eventually I hit a successsful combination and confirmed a set of valid credentials.  

<img width="496" height="341" alt="SSH-exploit-success" src="https://github.com/user-attachments/assets/13a56e4e-8b2d-4bf8-a6c5-db30420a1a1b" />  

- Next, I tried authenticating to the host over SSH with the credentials, and after changing the encryption type, was able to successfully login with remote shell capabilities.  

<img width="655.5" height="466.5" alt="successful-ssh-shell" src="https://github.com/user-attachments/assets/9dce1e8e-c7f0-4625-a3bc-419d446ff04e" />  

## CONCLUSION
Strong password policies are crucial in any aspect of security, and can make or break any network. In a real-world environment, I would want to verify if this host is intended to have an open SSH port or not. If not, my recommendation is of course, to close it. Regardless, after identifying this very weak username/password combination, stricter password policies should be implemented, enforce an account lockout policy, enforce MFA for every user, or even implement SSH key based authentication instead of password based, for a higher level of security!
