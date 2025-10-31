🌞 Prouvez que c'est effectif

```sh
PS C:\Users\eliot> curl http://meow-tp2.switzerlandnorth.cloudapp.azure.com:8000


StatusCode        : 200
StatusDescription : OK
Content           : <!DOCTYPE html>
                    <html lang="en">
                    <head>
                        <meta charset="UTF-8">
                        <meta name="viewport" content="width=device-width, initial-scale=1.0">
                        <title>Purr Messages - Cat Message Board</title>
                        <...
```
🌞 Tester cloud-init

en créant une nouvelle VM et en lui passant ce fichier cloud-init.txt au démarrage
pour ça, utilisez une commande az vm create
utilisez l'option --custom-data /path/to/cloud-init.txt

```sh
PS C:\Users\eliot\projet> az vm create --name azure1.tp2 --resource-group B2_TP_Final --image Ubuntu2204 --size Standard_B1s --custom-data "C:\Users\eliot\Desktop\cloud-init.txt"
The default value of '--size' will be changed to 'Standard_D2s_v5' from 'Standard_DS1_v2' in a future release.
{
  "fqdns": "",
  "id": "/subscriptions/4c96c3a3-9178-4d14-8c07-14013bafa4e6/resourceGroups/B2_TP_Final/providers/Microsoft.Compute/virtualMachines/azure1.tp2",
  "location": "switzerlandnorth",
  "macAddress": "7C-ED-8D-44-8C-CC",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.7",
  "publicIpAddress": "172.161.53.24",
  "resourceGroup": "B2_TP_Final"
}
```

🌞 Vérifier que cloud-init a bien fonctionné

connectez-vous en SSH à la VM nouvellement créée, directement sur le nouvel utilisateur créé par cloud-init
```sh

PS C:\Users\eliot\projet> ssh az3
The authenticity of host '10.0.0.7 (<no hostip for proxy command>)' can't be established.
ED25519 key fingerprint is SHA256:VTcT8fgcRzY9W2VlyZt3QgqCiGgYIz/SSutAHHPqurU.
This host key is known by the following other names/addresses:
    C:\Users\eliot/.ssh/known_hosts:18: 172.161.53.24
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '10.0.0.7' (ED25519) to the list of known hosts.
Welcome to Ubuntu 22.04.5 LTS (GNU/Linux 6.8.0-1041-azure x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/pro

 System information as of Fri Oct 31 07:28:02 UTC 2025

  System load:  0.0               Processes:             106
  Usage of /:   5.7% of 28.89GB   Users logged in:       0
  Memory usage: 33%               IPv4 address for eth0: 10.0.0.7
  Swap usage:   0%


Expanded Security Maintenance for Applications is not enabled.

0 updates can be applied immediately.

Enable ESM Apps to receive additional future security updates.
See https://ubuntu.com/esm or run: sudo pro status


The list of available updates is more than a week old.
To check for new updates run: sudo apt update
New release '24.04.3 LTS' available.
Run 'do-release-upgrade' to upgrade to it.


Last login: Fri Oct 31 07:23:52 2025 from 159.117.224.29
To run a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.

CR4CKITO@azure1:~$
```




🌞 Récupérer votre secret depuis la VM
```sh
PS C:\Users\eliot> az keyvault secret show --vault-name meowKeyVaultAzure1TP1 --name TestSecret --query value -o tsv
MaValeurDeTest123
```

🌞 Coder un ptit script bash : get_secrets.sh

il commence probablement par un az login --identity
il récupère le secret DB_PASSWORD (commande az, stocke dans une variable)
il l'injecte dans le fichier .env

commande sed ou autres
il remplace la valeur de DB_PASSWORD= par le secret récupéré avec la commande az

```sh
PS C:\Users\eliot\projet> & ".\scripts\get_secrets.ps1"
-> Tentative de connexion (Managed Identity si sur VM)...
az login --identity: OK (si sur VM)
-> Récupération du secret 'db-password' depuis le vault 'meowKeyVaultAzure1TP1'...
OK — .env mis à jour et sauvegarde créée : C:\Users\eliot\projet\.env.bak
PS C:\Users\eliot\projet>
```






