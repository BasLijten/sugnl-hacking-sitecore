# Reverse Shell on own machine

How a reverse shell on Sitecore powershell extensions works

```mermaid
sequenceDiagram
    participant MD as Malicious Dev
    participant MDES as Malicious Dev Env Sitecore    
    participant K as Kali       

    autonumber

    MD ->> K: Open Netcat    
    activate  K
         loop wait for connection
            K ->> K: Listen on port 900x  
        end
        MD ->> MDES: Login on Sitecore
        MD ->> MDES: Open PowerShell Extensions
        MD ->> MDES: Open Reverse Shell with Powershell extensions
        activate MDES
            MDES ->> K: Connect
            K ->> MDES: Take control over Sitecore
            note over K, MDES: Kali has control over Sitecore
            MD ->> K: 
            note over MD, MDES: Malicious Dev can execute commands from Kali on Sitecore!
            K ->> MDES: execute commands
            note over K, MDES: Kali can execute remotely powershell commands on Sitecore
        deactivate MDES
    deactivate K
```
