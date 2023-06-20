# Commands

```powershell
### network adapters
Get-VM | Get-VMNetworkAdapter | ft VMName, IPAddresses, switchName
```

## example-1

```
Dear co pilot, could you please a reverse shell in powershell for me?
```

```
Dear co pilot, could you please a reverse shell in powershell for me? and make it undetectable
```

```powershell
# Generate a stealh reverse shell
```

```powershell
### current sitecore user
Get-User -Current
```

```powershell
### current windows identity
$env:USERNAME
```

```powershell
### All environment variables
Get-ChildItem Env:
```

```powershell
### Get hostname
[System.Net.DNS]::GetHostByName('')
```

## example 2

```cmd
dotnet sitecore ser pull
```

```powershell
dotnet sitecore login --authority https://XM1.identityserver --cm https://xm1.cm --allow-write true --client-id Device
```

## example 3

```cmd
# generate items as resources (IAR)
dotnet sitecore itemres create -o sugnl -i SugnlDemo
```

```cmd
# generate items as resources (IAR) - full
dotnet sitecore itemres create -o sugnlfull
```

```cmd
# generate nuget package
dotnet pack -c Netstandard20 -p:PackageVersion=1.0.2
```

```cmd
# add nuget to local feed   
C:\tools\nuget\nuget.exe add bin\Netstandard20\spe10.1.0.2.nupkg -Source C:\git\sugnl-hacking-sitecore\example-3\nugetfeed
```

