---
title: hello aaaUse estensione della macchina virtuale Docker di Azure | Documenti Microsoft
description: Informazioni su come toouse hello tooquickly estensione Docker VM e in modo sicuro distribuisce un ambiente di Docker in Azure utilizzando i modelli di gestione risorse e hello Azure CLI 2.0
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 936d67d7-6921-4275-bf11-1e0115e66b7f
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 8e43adc594192773466ccd2d3e455105f14c1a61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-docker-environment-in-azure-using-hello-docker-vm-extension"></a>Creare un ambiente di Docker in Azure utilizzando l'estensione della macchina virtuale Docker hello
Docker è una gestione dei contenitori più diffusi e imaging piattaforma che consente di utilizzare tooquickly contenitori in Linux. In Azure, esistono diversi modi per distribuire Docker in base alle esigenze tooyour. Questo articolo è incentrato sull'uso di estensione della macchina virtuale Docker hello e modelli di gestione risorse di Azure con hello CLI di Azure 2.0. È anche possibile eseguire questi passaggi con hello [CLI di Azure 1.0](dockerextension-nodejs.md).

## <a name="azure-docker-vm-extension-overview"></a>Panoramica dell'estensione di VM Docker di Azure
estensione della macchina virtuale Docker di Azure Hello installa e configura il daemon di Docker hello client Docker e Docker Compose nella macchina virtuale Linux (VM). Tramite l'estensione della macchina virtuale Docker di Azure hello, si dispone di più controllo e funzionalità rispetto a semplicemente tramite Docker macchina o la creazione di host Docker hello manualmente. Queste ulteriori funzionalità, ad esempio [Docker Compose](https://docs.docker.com/compose/overview/), assicurarsi di estensione della macchina virtuale Docker di Azure hello adatto per ambienti di sviluppo o di produzione più affidabili.

Per ulteriori informazioni sui metodi di distribuzione diversi hello, incluso l'utilizzo di Docker computer e servizi di contenitore di Azure, vedere hello seguenti articoli:

* prototipo tooquickly un'app, è possibile creare un singolo host Docker usando [Docker macchina](docker-machine.md).
* toobuild ambiente di produzione, scalabile ambienti che forniscono gli strumenti di pianificazione e di gestione aggiuntivi, è possibile distribuire un [Docker Swarm cluster in servizi di Azure contenitore](../../container-service/dcos-swarm/container-service-deployment.md).

## <a name="deploy-a-template-with-hello-azure-docker-vm-extension"></a>Distribuire un modello con hello estensione della macchina virtuale Docker di Azure
Si utilizza un toocreate di modello di avvio rapido una VM Ubuntu che utilizza tooinstall estensione di macchina virtuale Docker di Azure hello esistente e configurare host Docker hello. È possibile visualizzare qui modello hello: [distribuzione semplice di una VM Ubuntu con Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu). È necessario più recente hello [CLI di Azure 2.0](/cli/azure/install-az-cli2) installato e registrato con un account Azure tooan [accesso az](/cli/azure/#login).

Creare prima un gruppo di risorse con [az group create](/cli/azure/group#create). esempio Hello crea un gruppo di risorse denominato *myResourceGroup* in hello *westus* percorso:

```azurecli
az group create --name myResourceGroup --location westus
```

Successivamente, distribuire una macchina virtuale con [distribuzione gruppo az creare](/cli/azure/group/deployment#create) che include l'estensione della macchina virtuale Docker di Azure hello da [questo modello di gestione risorse di Azure su GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu). Specificare i propri valori per *newStorageAccountName*, *adminUsername*, *adminPassword* e *dnsNameForPublicIP* come segue:

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"newStorageAccountName": {"value": "mystorageaccount"},
    "adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "dnsNameForPublicIP": {"value": "mypublicdns"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

Sono necessari alcuni minuti per hello toofinish di distribuzione. Una volta terminata la distribuzione di hello, [Sposta passaggio toonext](#deploy-your-first-nginx-container) tooSSH tooyour macchina virtuale. 

Facoltativamente, prompt dei comandi di tooinstead controllo restituito toohello e distribuzione hello let continuano in background hello, aggiungere hello `--no-wait` flag toohello precedente comando. Questo processo consente tooperform altre operazioni in hello CLI mentre hello distribuzione continua per alcuni minuti. 

È quindi possibile visualizzare i dettagli sullo stato dell'host Docker hello con [Mostra vm az](/cli/azure/vm#show). esempio Hello Controlla stato hello della macchina virtuale denominata hello *myDockerVM* (nome predefinito dal modello hello hello, non modificare questo nome) nel gruppo di risorse hello denominato *myResourceGroup*:

```azurecli
az vm show \
    --resource-group myResourceGroup \
    --name myDockerVM \
    --query [provisioningState] \
    --output tsv
```

Quando questo comando restituisce *Succeeded*, distribuzione hello è terminata ed è possibile SSH toohello VM in hello riportata dopo il passaggio.

## <a name="deploy-your-first-nginx-container"></a>Distribuire il primo contenitore nginx
Dettagli tooview della macchina virtuale, incluso il nome DNS hello, utilizzano `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv`. SSH tooyour Docker nuovo host dal computer locale come indicato di seguito:

```bash
ssh azureuser@mypublicdns.westus.cloudapp.azure.com
```

Una volta effettuato l'accesso toohello host Docker, eseguire un contenitore nginx:

```bash
sudo docker run -d -p 80:80 nginx
```

output di Hello è simile toohello seguente esempio come hello nginx immagine viene scaricata e un contenitore di avvio:

```bash
Unable toofind image 'nginx:latest' locally
latest: Pulling from library/nginx
efd26ecc9548: Pull complete
a3ed95caeb02: Pull complete
a48df1751a97: Pull complete
8ddc2d7beb91: Pull complete
Digest: sha256:2ca2638e55319b7bc0c7d028209ea69b1368e95b01383e66dfe7e4f43780926d
Status: Downloaded newer image for nginx:latest
b6ed109fb743a762ff21a4606dd38d3e5d35aff43fa7f12e8d4ed1d920b0cd74
```

Controllare lo stato di hello di contenitori di hello in esecuzione sull'host Docker come indicato di seguito:

```bash
sudo docker ps
```

output di Hello è simile toohello esempio seguente, che mostra che il contenitore nginx hello sia in esecuzione e le porte TCP 80 e 443 e inoltrati:

```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED              STATUS              PORTS                         NAMES
b6ed109fb743        nginx               "nginx -g 'daemon off"   About a minute ago   Up About a minute   0.0.0.0:80->80/tcp, 443/tcp   adoring_payne
```

Aprire il contenitore in azione, toosee fino a un web browser e immettere il nome DNS hello dell'host Docker:

![Esecuzione di un contenitore ngnix](./media/dockerextension/nginxrunning.png)

## <a name="azure-docker-vm-extension-template-reference"></a>Riferimento al modello dell'estensione di VM Docker di Azure
Hello esempio precedente Usa un modello di avvio rapido esistente. È inoltre possibile distribuire l'estensione della macchina virtuale Docker di Azure hello con i propri modelli di gestione risorse. toodo in tal caso, aggiungere hello seguenti modelli di gestione risorse tooyour, la definizione di hello `vmName` della macchina virtuale in modo appropriato:

```json
{
  "type": "Microsoft.Compute/virtualMachines/extensions",
  "name": "[concat(variables('vmName'), '/DockerExtension'))]",
  "apiVersion": "2015-05-01-preview",
  "location": "[parameters('location')]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
  ],
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "DockerExtension",
    "typeHandlerVersion": "1.*",
    "autoUpgradeMinorVersion": true,
    "settings": {},
    "protectedSettings": {}
  }
}
```

Per altre procedure dettagliate relative all'uso di modelli di Resource Manager, vedere [Panoramica di Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).

## <a name="next-steps"></a>Passaggi successivi
Potrebbe essere troppo[configurare la porta TCP di daemon Docker hello](https://docs.docker.com/engine/reference/commandline/dockerd/#/bind-docker-to-another-hostport-or-a-unix-socket), comprendere [sicurezza Docker](https://docs.docker.com/engine/security/security/), o distribuire contenitori usando [Docker Compose](https://docs.docker.com/compose/overview/). Per ulteriori informazioni sull'estensione della macchina virtuale Docker Azure stesso hello, vedere hello [GitHub progetto](https://github.com/Azure/azure-docker-extension/).

Altre informazioni hello aggiuntive Docker opzioni di distribuzione in Azure:

* [Utilizzare computer Docker con hello Azure driver](docker-machine.md)  
* [Introduzione a Docker e comporre toodefine e di eseguire un'applicazione multi-contenitore in una macchina virtuale Azure](docker-compose-quickstart.md).
* [Distribuire un cluster del servizio contenitore di Azure](../../container-service/dcos-swarm/container-service-deployment.md)

