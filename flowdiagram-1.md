# Reverse Shell 101

Description of a standard reverse shell setup

```mermaid
sequenceDiagram        
    participant MDET as Malicious Dev Env Terminal
    participant K as Kali     
    participant MD as Malicious developer       
    autonumber

    MD ->> K: Open Netcat    
    activate  K
        loop wait for connection
            K ->> K: Listen on port 900x  
        end      
        MD ->> MDET: open reverse Shell with Powershell
        activate MDET
            MDET ->> K: Connect
            K ->> MDET: Take control over MDET
            note over K, MDET: Kali has control over dev environment
            MD ->> K: 
            note over MD, MDET: Malicious Dev can execute commands from Kali on the terminal
        deactivate MDET
    deactivate K
```
