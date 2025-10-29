# A. Choix de l'algorithme de chiffrement

🌞 Déterminer quel algorithme de chiffrement utiliser pour vos clés

Pour chiffrer mes clés j'ai utilisé ed25519


- Pourquoi éviter RSA comme algorithme de chiffrement pour nos clés
[https://devblogs.microsoft.com/devops/ssh-rsa-deprecation]

-Pourquoi utiliser ED25519 comme algorithme de chiffrement pour mes clés.
[https://www.brandonchecketts.com/archives/ssh-ed25519-key-best-practices-for-2025#:~:text=Although%20the%20256-bit%20ed25519,a%20similar%20level%20of%20security.]



## B. Génération de votre paire de clés

🌞 Générer une paire de clés pour ce TP


```sh

PS C:\Users\eliot> ssh-keygen -t ed25519 -f "$HOME\.ssh\cloud_tp"
Generating public/private ed25519 key pair.
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in C:\Users\eliot\.ssh\cloud_tp
Your public key has been saved in C:\Users\eliot\.ssh\cloud_tp.pub
The key fingerprint is:
SHA256:FgbwS/B285olDce33cxlnD2ypw6U6zaeUka3hqInggA eliot@pbl233
The key's randomart image is:
+--[ED25519 256]--+
|    o..          |
|     + . .     .o|
|      = * o .. o=|
|E    o + B o.+o=o|
|.     . S =o+.o.+|
| .     . *.+.oo  |
|  . .   + +o..   |
|   . . o o.o+    |
|      . o ++..   |
+----[SHA256]-----+
PS C:\Users\eliot>

```

## C. Agent SSH

🌞 Configurer un agent SSH sur votre poste

```sh
PS C:\WINDOWS\system32> Get-Service ssh-agent

Status   Name               DisplayName
------   ----               -----------
Stopped  ssh-agent          OpenSSH Authentication Agent


PS C:\WINDOWS\system32> Set-Service -Name ssh-agent -StartupType Automatic
PS C:\WINDOWS\system32> Start-Service ssh-agent
PS C:\WINDOWS\system32> Get-Service ssh-agent

Status   Name               DisplayName
------   ----               -----------
Running  ssh-agent          OpenSSH Authentication Agent
```

```sh
PS C:\Users\eliot> Start-Service "ssh-agent"
PS C:\Users\eliot> Get-Service "ssh-agent"

Status   Name               DisplayName
------   ----               -----------
Running  ssh-agent          OpenSSH Authentication Agent
```
Ajout de la clé 

```sh
PS C:\Users\eliot> ssh-add "$HOME\.ssh\cloud_tp"
Enter passphrase for C:\Users\eliot\.ssh\cloud_tp:
Identity added: C:\Users\eliot\.ssh\cloud_tp (eliot@pbl233)


PS C:\Users\eliot> ls .ssh


    Répertoire : C:\Users\eliot\.ssh


Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
-a----        29/10/2025     21:47            444 cloud_tp
-a----        29/10/2025     21:47             95 cloud_tp.pub
-a----        23/09/2025     14:20            843 known_hosts
-a----        23/09/2025     14:20             97 known_hosts.old

```


🌞 Créez une VM depuis le Azure CLI : azure1.tp1

```sh


```
