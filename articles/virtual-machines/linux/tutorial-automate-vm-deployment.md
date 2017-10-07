---
title: aaaCustomize una VM Linux al primo avvio in Azure | Documenti Microsoft
description: Informazioni su come toouse cloud-init e hello macchine virtuali Linux di insieme di credenziali chiave toocustomze prima volta che eseguiranno l'avvio in Azure
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/11/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: 280189723ac0205226f9c0068bd605da13249ace
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocustomize-a-linux-virtual-machine-on-first-boot"></a>Come toocustomize una macchina virtuale Linux al primo avvio
In un'esercitazione precedente, si è appreso come tooSSH tooa virtual machine (VM) e installare manualmente NGINX. in genere desiderata toocreate macchine virtuali in modo rapido e coerenza, qualche forma di automazione. Un comune toocustomize approccio una macchina virtuale al primo avvio viene toouse [cloud init](https://cloudinit.readthedocs.io). In questa esercitazione si apprenderà come:

> [!div class="checklist"]
> * Creare un file di configurazione cloud-init
> * Creare una macchina virtuale che usa un file cloud-init
> * Visualizzare un'app Node.js in esecuzione dopo la creazione della macchina virtuale hello
> * Utilizzare l'archivio certificati di chiave dell'insieme di credenziali toosecurely
> * Automatizzare le distribuzioni sicure di NGINX con cloud-init


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Se si sceglie tooinstall e utilizza hello CLI in locale, questa esercitazione, è necessario che sia in esecuzione hello Azure CLI versione 2.0.4 o versioni successive. Eseguire `az --version` versione hello toofind. Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).  



## <a name="cloud-init-overview"></a>Panoramica di cloud-init
[Cloud init](https://cloudinit.readthedocs.io) è una VM Linux toocustomize un approccio ampiamente usato all'avvio per hello prima volta. È possibile utilizzare pacchetti tooinstall cloud init e scrittura dei file, o gli utenti tooconfigure e sicurezza. Come cloud-inizializzazione viene eseguita durante il processo di avvio iniziale hello, non sono ulteriori passaggi o la configurazione obbligatoria tooapply gli agenti.

Cloud-init funziona anche fra distribuzioni. Ad esempio, non si usa **installazione apt get** o **yum installare** tooinstall un pacchetto. In alternativa è possibile definire un elenco di pacchetti tooinstall. Cloud init utilizza automaticamente lo strumento di gestione di hello pacchetto nativo per distribuzione hello selezionate.

È in uso di nostri partner tooget cloud-init inclusi e l'utilizzo delle immagini hello che forniscono tooAzure. Hello nella tabella seguente sono illustrati hello corrente cloud init disponibilità le immagini della piattaforma Azure:

| Alias | Autore | Offerta | SKU | Versione |
|:--- |:--- |:--- |:--- |:--- |:--- |
| UbuntuLTS |Canonical |UbuntuServer |16.04-LTS |più recenti |
| UbuntuLTS |Canonical |UbuntuServer |14.04.5-LTS |più recenti |
| CoreOS |CoreOS |CoreOS |Stabile |più recenti |


## <a name="create-cloud-init-config-file"></a>Creare un file di configurazione cloud-init
cloud toosee-init in azione, creare una macchina virtuale che installa NGINX ed esegue una semplice app Node.js 'Hello World'. Hello seguente configurazione cloud init installa i pacchetti hello necessario, crea un'app Node.js, quindi inizializza e avvia l'applicazione hello.

Nella shell corrente, creare un file denominato *cloud init.txt* e Incolla hello seguente configurazione. Ad esempio, creare file hello in hello Shell Cloud non presenti nel computer locale. È possibile usare qualsiasi editor. Immettere `sensible-editor cloud-init.txt` toocreate hello file e visualizzare un elenco degli editor disponibili. Assicurarsi che tale file intero cloud-init hello viene copiato correttamente, soprattutto hello prima riga:

```yaml
#cloud-config
package_upgrade: true
packages:
  - nginx
  - nodejs
  - npm
write_files:
  - owner: www-data:www-data
  - path: /etc/nginx/sites-available/default
    content: |
      server {
        listen 80;
        location / {
          proxy_pass http://localhost:3000;
          proxy_http_version 1.1;
          proxy_set_header Upgrade $http_upgrade;
          proxy_set_header Connection keep-alive;
          proxy_set_header Host $host;
          proxy_cache_bypass $http_upgrade;
        }
      }
  - owner: azureuser:azureuser
  - path: /home/azureuser/myapp/index.js
    content: |
      var express = require('express')
      var app = express()
      var os = require('os');
      app.get('/', function (req, res) {
        res.send('Hello World from host ' + os.hostname() + '!')
      })
      app.listen(3000, function () {
        console.log('Hello world app listening on port 3000!')
      })
runcmd:
  - service nginx restart
  - cd "/home/azureuser/myapp"
  - npm init
  - npm install express -y
  - nodejs index.js
```

Per altre informazioni sulle opzioni di configurazione di cloud-init, vedere gli [esempi di configurazione di cloud-init](https://cloudinit.readthedocs.io/en/latest/topics/examples.html).

## <a name="create-virtual-machine"></a>Crea macchina virtuale
Per poter creare una macchina virtuale è prima necessario creare un gruppo di risorse con il comando [az group create](/cli/azure/group#create). esempio Hello crea un gruppo di risorse denominato *myResourceGroupAutomate* in hello *eastus* percorso:

```azurecli-interactive 
az group create --name myResourceGroupAutomate --location eastus
```

Creare quindi una macchina virtuale con il comando [az vm create](/cli/azure/vm#create). Hello utilizzare `--custom-data` toopass parametro nel file di configurazione cloud init. Fornire hello percorso completo toohello *cloud init.txt* configurazione se è stato salvato il file hello all'esterno delle directory di lavoro attuale. esempio Hello crea una macchina virtuale denominata *myAutomatedVM*:

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupAutomate \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

Sono necessari alcuni minuti per hello VM toobe creato, tooinstall pacchetti hello e toostart app hello. Sono presenti attività in background che continuare toorun dopo hello CLI di Azure restituisce toohello prompt. Potrebbe essere un altro paio di minuti prima di poter accedere app hello. Dopo aver creato hello VM, prendere nota di hello `publicIpAddress` visualizzato da hello CLI di Azure. Questo indirizzo è utilizzato tooaccess hello Node.js app tramite un web browser.

tooallow web tooreach traffico la macchina virtuale, aprire la porta 80 da hello Internet con [az vm open-porta](/cli/azure/vm#open-port):

```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroupAutomate --name myVM
```

## <a name="test-web-app"></a>Testare l'app Web
È ora possibile aprire un web browser e immettere *http://<publicIpAddress>*  nella barra degli indirizzi hello. Fornire la propria pubblico indirizzo IP da hello VM creare il processo. App Node.js viene visualizzato come hello di esempio seguente:

![Visualizzare il sito NGINX in esecuzione](./media/tutorial-automate-vm-deployment/nginx.png)


## <a name="inject-certificates-from-key-vault"></a>Inserire certificati da Key Vault
Questa sezione facoltativa Mostra come è possibile in modo sicuro archiviare i certificati nell'insieme di credenziali chiave di Azure e li inserire durante la distribuzione di macchine Virtuali hello. Invece di usare un'immagine personalizzata che include i certificati di hello baked-in, questo processo assicura che i certificati più aggiornati di hello vengono inseriti tooa VM al primo avvio. Durante il processo di hello mai certificato hello lascia hello piattaforma Azure o è esposto in uno script, una cronologia della riga di comando o un modello.

Azure Key Vault consente di proteggere chiavi crittografiche e segreti, come certificati e password. Insieme di credenziali chiave consente di semplificare il processo di gestione delle chiavi hello e consente il controllo toomaintain di chiavi per l'accesso e crittografare i dati. Questo scenario presenta alcuni toocreate concetti chiave dell'insieme di credenziali e utilizzare un certificato, anche se non viene fornita una panoramica completa sulla toouse insieme di credenziali chiave.

Hello alla procedura seguente mostra come è possibile:

- Creare un Azure Key Vault
- Generare o caricare un insieme di credenziali chiave di toohello certificato
- Creare una chiave privata da tooinject certificato hello in tooa VM
- Creare una macchina virtuale e inserire il certificato di hello

### <a name="create-an-azure-key-vault"></a>Creare un Azure Key Vault
Innanzitutto, creare un Key Vault con il comando [az keyvault create](/cli/azure/keyvault#create) e abilitarlo all'uso quando si distribuisce una macchina virtuale. Ogni Key Vault deve avere un nome univoco in lettere minuscole. Sostituire *mykeyvault* in hello esempio con il proprio nome univoco di insieme di credenziali chiave seguente:

```azurecli-interactive 
keyvault_name=mykeyvault
az keyvault create \
    --resource-group myResourceGroupAutomate \
    --name $keyvault_name \
    --enabled-for-deployment
```

### <a name="generate-certificate-and-store-in-key-vault"></a>Generare certificati e archiviarli in Key Vault
Per la produzione è necessario importare un certificato valido firmato da un provider attendibile con il comando [az keyvault certificate import](/cli/azure/keyvault/certificate#import). Per questa esercitazione, hello esempio seguente viene illustrato come è possibile generare un certificato autofirmato con [certificato keyvault az creare](/cli/azure/keyvault/certificate#create) che utilizza criteri di certificato predefiniti hello:

```azurecli-interactive 
az keyvault certificate create \
    --vault-name $keyvault_name \
    --name mycert \
    --policy "$(az keyvault certificate get-default-policy)"
```


### <a name="prepare-certificate-for-use-with-vm"></a>Preparare i certificati per l'uso con macchine virtuali
certificato di hello toouse durante hello VM creare il processo, ottenere l'ID di hello del certificato con [az keyvault elenco-versioni del segreto](/cli/azure/keyvault/secret#list-versions). Hello VM deve certificato hello in un determinato formato tooinject non all'avvio del sistema, quindi convertire certificato hello con [az vm segreto formato](/cli/azure/vm#format-secret). Hello di esempio seguente assegna l'output di hello di toovariables questi comandi per facilitare l'utilizzo in hello passaggi successivi:

```azurecli-interactive 
secret=$(az keyvault secret list-versions \
          --vault-name $keyvault_name \
          --name mycert \
          --query "[?attributes.enabled].id" --output tsv)
vm_secret=$(az vm format-secret --secret "$secret")
```


### <a name="create-cloud-init-config-toosecure-nginx"></a>Creare cloud init configurazione toosecure NGINX
Quando si crea una macchina virtuale, i certificati e chiavi vengono archiviate in hello protetto *var/lib/waagent/* directory. tooautomate aggiunta hello certificato toohello macchina virtuale e la configurazione NGINX, è possibile utilizzare una configurazione cloud-init aggiornata dall'esempio precedente hello.

Creare un file denominato *cloud-init-secured.txt* e Incolla hello seguente configurazione. Nuovamente, se si utilizza hello Shell Cloud, creare il file di configurazione cloud init hello non esiste e non nel computer locale. Utilizzare `sensible-editor cloud-init-secured.txt` toocreate hello file e visualizzare un elenco degli editor disponibili. Assicurarsi che tale file intero cloud-init hello viene copiato correttamente, soprattutto hello prima riga:

```yaml
#cloud-config
package_upgrade: true
packages:
  - nginx
  - nodejs
  - npm
write_files:
  - owner: www-data:www-data
  - path: /etc/nginx/sites-available/default
    content: |
      server {
        listen 80;
        listen 443 ssl;
        ssl_certificate /etc/nginx/ssl/mycert.cert;
        ssl_certificate_key /etc/nginx/ssl/mycert.prv;
        location / {
          proxy_pass http://localhost:3000;
          proxy_http_version 1.1;
          proxy_set_header Upgrade $http_upgrade;
          proxy_set_header Connection keep-alive;
          proxy_set_header Host $host;
          proxy_cache_bypass $http_upgrade;
        }
      }
  - owner: azureuser:azureuser
  - path: /home/azureuser/myapp/index.js
    content: |
      var express = require('express')
      var app = express()
      var os = require('os');
      app.get('/', function (req, res) {
        res.send('Hello World from host ' + os.hostname() + '!')
      })
      app.listen(3000, function () {
        console.log('Hello world app listening on port 3000!')
      })
runcmd:
  - secretsname=$(find /var/lib/waagent/ -name "*.prv" | cut -c -57)
  - mkdir /etc/nginx/ssl
  - cp $secretsname.crt /etc/nginx/ssl/mycert.cert
  - cp $secretsname.prv /etc/nginx/ssl/mycert.prv
  - service nginx restart
  - cd "/home/azureuser/myapp"
  - npm init
  - npm install express -y
  - nodejs index.js
```

### <a name="create-secure-vm"></a>Creare una macchina virtuale protetta
Creare quindi una macchina virtuale con il comando [az vm create](/cli/azure/vm#create). dati del certificato Hello viene inseriti dall'insieme di credenziali chiave con hello `--secrets` parametro. Nell'esempio precedente hello, è anche passare nella configurazione cloud init hello con hello `--custom-data` parametro:

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupAutomate \
    --name myVMSecured \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init-secured.txt \
    --secrets "$vm_secret"
```

Sono necessari alcuni minuti per hello VM toobe creato, tooinstall pacchetti hello e toostart app hello. Sono presenti attività in background che continuare toorun dopo hello CLI di Azure restituisce toohello prompt. Potrebbe essere un altro paio di minuti prima di poter accedere app hello. Dopo aver creato hello VM, prendere nota di hello `publicIpAddress` visualizzato da hello CLI di Azure. Questo indirizzo è utilizzato tooaccess hello Node.js app tramite un web browser.

tooallow secure tooreach traffico web la macchina virtuale, aprire la porta 443 da hello Internet con [az vm open-porta](/cli/azure/vm#open-port):

```azurecli-interactive 
az vm open-port \
    --resource-group myResourceGroupAutomate \
    --name myVMSecured \
    --port 443
```

### <a name="test-secure-web-app"></a>Testare l'applicazione Web protetta
È ora possibile aprire un web browser e immettere *https://<publicIpAddress>*  nella barra degli indirizzi hello. Fornire la propria pubblico indirizzo IP da hello VM creare il processo. Se è stato utilizzato un certificato autofirmato, è necessario accettare l'avviso di sicurezza hello:

![Accettare l'avviso di sicurezza del Web browser](./media/tutorial-automate-vm-deployment/browser-warning.png)

Il sito NGINX e Node.js app viene quindi visualizzata come hello di esempio seguente:

![Visualizzare il sito protetto NGINX in esecuzione](./media/tutorial-automate-vm-deployment/secured-nginx.png)


## <a name="next-steps"></a>Passaggi successivi
In questa esercitazione vengono configurate macchine virtuali al primo avvio con cloud-init. Si è appreso come:

> [!div class="checklist"]
> * Creare un file di configurazione cloud-init
> * Creare una macchina virtuale che usa un file cloud-init
> * Visualizzare un'app Node.js in esecuzione dopo la creazione della macchina virtuale hello
> * Utilizzare l'archivio certificati di chiave dell'insieme di credenziali toosecurely
> * Automatizzare le distribuzioni sicure di NGINX con cloud-init

Spostare toolearn esercitazione successiva toohello come toocreate immagini di macchina virtuale personalizzate.

> [!div class="nextstepaction"]
> [Creare un'immagine di VM personalizzata](./tutorial-custom-images.md)
