# Reverse Shell on Other Sitecore development machine

```mermaid
sequenceDiagram
    participant MD as Malicious Dev    
    participant MDE as Malicions Dev Environment
    participant K as Kali      
    participant LD as Lead Dev
    participant LDE as Lead Dev
    participant G as Github            
    autonumber
    
    MD ->> MD: Create new branch
    MD ->> MDE: Create malicious powershell script in Sitecore
    MD ->> MDE: Create automated taskin Sitecore
    MD ->> G: Push branch    
    
    activate K    
        K ->> K: Listen on port 900x  
        LD ->> G: Pull Code
        LD ->> P: Run environment
        LD ->> P: publish all items
        note over LD, P: publish is done implicitly, dev likely doesn't check the code he pulls                          
        P ->> K: Open Reverse Shell with Powershell extensions
        activate P
            P ->> K: Connect
            K ->> P: Take control over Sitecore
            note over K, P: Kali has control over Sitecore
            MD ->> K: 
            note over MD, K: Malicious Dev can execute commands from Kali on Sitecore!
        deactivate P
    deactivate K
```