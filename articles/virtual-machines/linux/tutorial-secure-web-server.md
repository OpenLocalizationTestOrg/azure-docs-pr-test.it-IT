---
title: un server web con SSL certificati in Azure aaaSecure | Documenti Microsoft
description: Informazioni su come certificati del server web di toosecure hello NGINX con SSL in una VM Linux in Azure
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
ms.date: 07/17/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: d3a62d77ac05c9aa2a44356b7c8e44cb485b81aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="secure-a-web-server-with-ssl-certificates-on-a-linux-virtual-machine-in-azure"></a>Proteggere un server Web con i certificati SSL in una macchina virtuale Linux in Azure
server web toosecure, un certificato in un secondo momento SSL (Secure Sockets) può essere utilizzato il traffico web tooencrypt. Questi certificati SSL possono essere archiviati nell'insieme di credenziali chiave di Azure e consentono le distribuzioni sicure di certificati tooLinux le macchine virtuali (VM) in Azure. In questa esercitazione si apprenderà come:

> [!div class="checklist"]
> * Creare un Azure Key Vault
> * Generare o caricare un insieme di credenziali chiave di toohello certificato
> * Creare una macchina virtuale e installare il server web NGINX di hello
> * Inserire il certificato di hello nella VM hello e configura NGINX con un binding SSL

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Se si sceglie tooinstall e utilizza hello CLI in locale, questa esercitazione, è necessario che sia in esecuzione hello Azure CLI versione 2.0.4 o versioni successive. Eseguire `az --version` versione hello toofind. Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).  


## <a name="overview"></a>Panoramica
Azure Key Vault consente di proteggere chiavi di crittografia, chiavi private, certificati e password. Insieme di credenziali chiave consente di ottimizzare processo di gestione dei certificati hello e consente il controllo toomaintain delle chiavi che accedono a tali certificati. È possibile creare un certificato autofirmato in Key Vault o caricarne uno esistente, un certificato attendibile di cui si è già proprietari.

Invece di usare un'immagine di macchina virtuale personalizzata che include certificati incorporati, si inseriscono i certificati in una macchina virtuale in esecuzione. Questo processo assicura che i certificati più aggiornati di hello siano installati in un server web durante la distribuzione. Se si rinnovare o sostituire un certificato, non è inoltre necessario toocreate una nuova immagine di macchina virtuale personalizzata. i certificati più recenti di Hello vengono inseriti automaticamente durante la creazione di macchine virtuali aggiuntive. Durante l'intero processo hello, i certificati di hello mai lasciare hello piattaforma Azure o vengono esposti in uno script, una cronologia della riga di comando o un modello.


## <a name="create-an-azure-key-vault"></a>Creare un Azure Key Vault
Per poter creare un insieme di credenziali delle chiavi e i certificati, è prima necessario creare un gruppo di risorse con il comando [az group create](/cli/azure/group#create). esempio Hello crea un gruppo di risorse denominato *myResourceGroupSecureWeb* in hello *eastus* percorso:

```azurecli-interactive 
az group create --name myResourceGroupSecureWeb --location eastus
```

Creare quindi un insieme di credenziali delle chiavi con il comando [az keyvault create](/cli/azure/keyvault#create) e abilitarlo all'uso quando si distribuisce una macchina virtuale. Ogni Key Vault deve avere un nome univoco in lettere minuscole. Sostituire  *<mykeyvault>*  in hello esempio con il proprio nome univoco di insieme di credenziali chiave seguente:

```azurecli-interactive 
keyvault_name=<mykeyvault>
az keyvault create \
    --resource-group myResourceGroupSecureWeb \
    --name $keyvault_name \
    --enabled-for-deployment
```

## <a name="generate-a-certificate-and-store-in-key-vault"></a>Generare un certificato e archiviarlo in Key Vault
Per la produzione è necessario importare un certificato valido firmato da un provider attendibile con il comando [az keyvault certificate import](/cli/azure/certificate#import). Per questa esercitazione, hello esempio seguente viene illustrato come è possibile generare un certificato autofirmato con [certificato keyvault az creare](/cli/azure/certificate#create) che utilizza criteri di certificato predefiniti hello:

```azurecli-interactive 
az keyvault certificate create \
    --vault-name $keyvault_name \
    --name mycert \
    --policy "$(az keyvault certificate get-default-policy)"
```

### <a name="prepare-a-certificate-for-use-with-a-vm"></a>Preparare un certificato per l'uso con una macchina virtuale
certificato di hello toouse durante hello VM creare il processo, ottenere l'ID di hello del certificato con [az keyvault elenco-versioni del segreto](/cli/azure/keyvault/secret#list-versions). Convertire certificato hello con [az vm segreto formato](/cli/azure/vm#format-secret). Hello di esempio seguente assegna l'output di hello di toovariables questi comandi per facilitare l'utilizzo in hello passaggi successivi:

```azurecli-interactive 
secret=$(az keyvault secret list-versions \
          --vault-name $keyvault_name \
          --name mycert \
          --query "[?attributes.enabled].id" --output tsv)
vm_secret=$(az vm format-secret --secret "$secret")
```

### <a name="create-a-cloud-init-config-toosecure-nginx"></a>Creare un toosecure configurazione cloud init NGINX
[Cloud init](https://cloudinit.readthedocs.io) è una VM Linux toocustomize un approccio ampiamente usato all'avvio per hello prima volta. È possibile utilizzare pacchetti tooinstall cloud init e scrittura dei file, o gli utenti tooconfigure e sicurezza. Come cloud-inizializzazione viene eseguita durante il processo di avvio iniziale hello, non sono ulteriori passaggi o la configurazione obbligatoria tooapply gli agenti.

Quando si crea una macchina virtuale, i certificati e chiavi vengono archiviate in hello protetto *var/lib/waagent/* directory. aggiunta di tooautomate hello toohello certificato VM e configurazione hello del server web, utilizzare cloud init. In questo esempio è di installare e configurare i server web NGINX di hello. È possibile utilizzare hello stesso processo tooinstall e configurare Apache. 

Creare un file denominato *cloud-init-web-server.txt* e Incolla hello seguente configurazione:

```yaml
#cloud-config
package_upgrade: true
packages:
  - nginx
write_files:
  - owner: www-data:www-data
  - path: /etc/nginx/sites-available/default
    content: |
      server {
        listen 443 ssl;
        ssl_certificate /etc/nginx/ssl/mycert.cert;
        ssl_certificate_key /etc/nginx/ssl/mycert.prv;
      }
runcmd:
  - secretsname=$(find /var/lib/waagent/ -name "*.prv" | cut -c -57)
  - mkdir /etc/nginx/ssl
  - cp $secretsname.crt /etc/nginx/ssl/mycert.cert
  - cp $secretsname.prv /etc/nginx/ssl/mycert.prv
  - service nginx restart
```

### <a name="create-a-secure-vm"></a>Creare una macchina virtuale sicura
Creare quindi una macchina virtuale con il comando [az vm create](/cli/azure/vm#create). dati del certificato Hello viene inseriti dall'insieme di credenziali chiave con hello `--secrets` parametro. Passare in configurazione cloud init hello con hello `--custom-data` parametro:

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupSecureWeb \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init-web-server.txt \
    --secrets "$vm_secret"
```

Sono necessari alcuni minuti per hello VM toobe creato, tooinstall pacchetti hello e toostart app hello. Dopo aver creato hello VM, prendere nota di hello `publicIpAddress` visualizzato da hello CLI di Azure. Questo indirizzo viene utilizzato tooaccess del sito in un web browser.

tooallow secure tooreach traffico web la macchina virtuale, aprire la porta 443 da hello Internet con [az vm open-porta](/cli/azure/vm#open-port):

```azurecli-interactive 
az vm open-port \
    --resource-group myResourceGroupSecureWeb \
    --name myVM \
    --port 443
```


### <a name="test-hello-secure-web-app"></a>App web in modo sicuro hello di test
È ora possibile aprire un web browser e immettere *https://<publicIpAddress>*  nella barra degli indirizzi hello. Fornire la propria pubblico indirizzo IP da hello VM creare il processo. Se è stato utilizzato un certificato autofirmato, è necessario accettare l'avviso di sicurezza hello:

![Accettare l'avviso di sicurezza del Web browser](./media/tutorial-secure-web-server/browser-warning.png)

Il sito NGINX protetto viene quindi visualizzato come hello di esempio seguente:

![Visualizzare il sito protetto NGINX in esecuzione](./media/tutorial-secure-web-server/secured-nginx.png)


## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione si è protetto un server Web NGINX con un certificato SSL archiviato in Azure Key Vault. Si è appreso come:

> [!div class="checklist"]
> * Creare un Azure Key Vault
> * Generare o caricare un insieme di credenziali chiave di toohello certificato
> * Creare una macchina virtuale e installare il server web NGINX di hello
> * Inserire il certificato di hello nella VM hello e configura NGINX con un binding SSL

Seguire questo toosee di collegamento incorporati gli esempi di script di macchina virtuale.

> [!div class="nextstepaction"]
> [Esempi di script delle macchine virtuali Windows](./cli-samples.md)