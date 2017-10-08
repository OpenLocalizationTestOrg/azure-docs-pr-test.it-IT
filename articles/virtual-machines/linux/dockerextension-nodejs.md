---
title: hello aaaUse estensione della macchina virtuale Docker di Azure con hello Azure CLI 1.0 | Documenti Microsoft
description: Informazioni su come toouse hello tooquickly estensione VM Docker e distribuire in modo sicuro un ambiente di Docker in Azure utilizzando i modelli di gestione risorse.
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 2133cdb1af741fe30093910fae5c3b2c91e8d5fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-docker-environment-in-azure-using-hello-docker-vm-extension-with-hello-azure-cli-10"></a>Creare un ambiente di Docker in Azure utilizzando l'estensione della macchina virtuale Docker hello con hello Azure CLI 1.0
Docker è una gestione dei contenitori più diffusi e immagini piattaforma che consente di utilizzare tooquickly contenitori in Linux (e anche Windows). In Azure, esistono diversi modi per distribuire Docker in base alle esigenze tooyour. In questo articolo è incentrato sull'uso di estensione della macchina virtuale Docker hello e modelli di gestione risorse di Azure. 

Per ulteriori informazioni sui metodi di distribuzione diversi hello, incluso l'utilizzo di Docker computer e servizi di contenitore di Azure, vedere hello seguenti articoli:

* prototipo tooquickly un'app, è possibile creare un singolo host Docker usando [Docker macchina](docker-machine.md).
* Per gli ambienti più grandi e più stabili, è possibile utilizzare l'estensione della macchina virtuale Docker di Azure hello, che supporta inoltre [Docker Compose](https://docs.docker.com/compose/overview/) toogenerate le distribuzioni di contenitore coerente. Questo articolo presenta utilizzando l'estensione della macchina virtuale Docker di Azure hello.
* toobuild ambiente di produzione, scalabile ambienti che forniscono gli strumenti di pianificazione e di gestione aggiuntivi, è possibile distribuire un [Docker Swarm cluster in servizi di Azure contenitore](../../container-service/dcos-swarm/container-service-deployment.md).

## <a name="cli-versions-toocomplete-hello-task"></a>Attività hello toocomplete versioni CLI
È possibile completare l'attività hello utilizzando una delle seguenti versioni CLI hello:

- [Azure CLI 1.0](#azure-docker-vm-extension-overview) : l'interfaccia CLI per hello classic risorse Gestione modelli di distribuzione e (in questo articolo)
- [Azure CLI 2.0](dockerextension.md) -la prossima generazione CLI per modello di distribuzione di gestione risorse hello 

## <a name="azure-docker-vm-extension-overview"></a>Panoramica dell'estensione di VM Docker di Azure
estensione della macchina virtuale Docker di Azure Hello installa e configura il daemon di Docker hello client Docker e Docker Compose nella macchina virtuale Linux (VM). Tramite l'estensione della macchina virtuale Docker di Azure hello, si dispone di più controllo e funzionalità rispetto a semplicemente tramite Docker macchina o la creazione di host Docker hello manualmente. Queste ulteriori funzionalità, ad esempio [Docker Compose](https://docs.docker.com/compose/overview/), assicurarsi di estensione della macchina virtuale Docker di Azure hello adatto per ambienti di sviluppo o di produzione più affidabili.

Modelli di gestione risorse di Azure definiscono l'intera struttura di hello dell'ambiente. I modelli consentono di toocreate e configurare le risorse, ad esempio host Docker hello macchine virtuali, archiviazione, i controlli di accesso basato sui ruoli (RBAC) e diagnostica. È possibile riutilizzare le distribuzioni di modelli toocreate aggiuntive in modo coerente. Per altre informazioni su Azure Resource Manager e relativi modelli, vedere la [Panoramica di Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md). 

## <a name="deploy-a-template-with-hello-azure-docker-vm-extension"></a>Distribuire un modello con hello estensione della macchina virtuale Docker di Azure
Si utilizza un toocreate di modello di avvio rapido una VM Ubuntu che utilizza tooinstall estensione di macchina virtuale Docker di Azure hello esistente e configurare host Docker hello. È possibile visualizzare qui modello hello: [distribuzione semplice di una VM Ubuntu con Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu). 

È necessario hello [CLI di Azure più recenti](../../cli-install-nodejs.md) installato e registrato con modalità di gestione risorse di hello come indicato di seguito:

```azurecli
azure config mode arm
```

Distribuire il modello di hello utilizzando hello CLI di Azure, specificare il modello di hello URI. esempio Hello crea un gruppo di risorse denominato *myResourceGroup* in hello *westus* percorso. Usare il nome e la posizione del gruppo di risorse nel modo seguente:

```azurecli
azure group create \
    --name myResourceGroup \
    --location westus \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

Risposte hello richieste tooname account di archiviazione, fornire un nome utente e una password e specificare un nome DNS. Hello l'output è simile toohello seguente esempio:

```azurecli
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Updating resource group myResourceGroup
info:    Updated resource group myResourceGroup
info:    Supply values for hello following parameters
newStorageAccountName: mystorageaccount
adminUsername: azureuser
adminPassword: P@ssword!
dnsNameForPublicIP: mypublicidns
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "azuredeploy"
data:    Id:                  /subscriptions/guid/resourceGroups/myResourceGroup
data:    Name:                myResourceGroup
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags: null
data:
info:    group create command OK
```

Hello CLI di Azure restituisce toohello prompt dopo pochi secondi, ma l'host Docker ancora viene creato e configurato da hello estensione della macchina virtuale Docker di Azure. Sono necessari alcuni minuti per hello toofinish di distribuzione. È possibile visualizzare i dettagli sullo stato dell'host Docker hello utilizzando hello `azure vm show` comando.

esempio Hello Controlla stato hello della macchina virtuale denominata hello *myDockerVM* (nome predefinito dal modello hello hello, non modificare questo nome) nel gruppo di risorse hello denominato *myResourceGroup*. Immettere il nome di hello hello del gruppo di risorse creato nel passaggio precedente hello:

```azurecli
azure vm show --resource-group myResourceGroup --name myDockerVM
```

output di hello Hello `azure vm show` è simile toohello seguente esempio di comando:

```azurecli
info:    Executing command vm show
+ Looking up hello VM "myDockerVM"
+ Looking up hello NIC "myVMNicD"
+ Looking up hello public ip "myPublicIPD"
data:    Id                              :/subscriptions/guid/resourceGroups/myresourcegroup/providers/Microsoft.Compute/virtualMachines/MyDockerVM
data:    ProvisioningState               :Succeeded
data:    Name                            :MyDockerVM
data:    Location                        :westus
data:    Type                            :Microsoft.Compute/virtualMachines
[...]
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Primary                   :true
data:          MAC Address               :00-0D-3A-33-D3-95
data:          Provisioning State        :Succeeded
data:          Name                      :myVMNicD
data:          Location                  :westus
data:            Public IP address       :13.91.107.235
data:            FQDN                    :mypublicdns.westus.cloudapp.azure.com
data:
data:    Diagnostics Instance View:
info:    vm show command OK
```

Parte superiore di hello di output di hello, vedrai hello **ProvisioningState** di hello macchina virtuale. Quando si visualizza *Succeeded*, distribuzione hello è terminata ed è possibile SSH toohello macchina virtuale.

Verso la fine hello dell'output di hello, *FQDN* Visualizza hello nome di dominio completo dell'host Docker. Questo nome di dominio completo è ciò che si usa tooSSH tooyour Docker host hello rimanenti passaggi.

## <a name="deploy-your-first-nginx-container"></a>Distribuire il primo contenitore nginx
Una volta distribuzione hello è stata completata, SSH tooyour nuovo host Docker da un computer locale. Immettere il nome utente e l'FQDN nel modo seguente:

```bash
ssh ops@mypublicdns.westus.cloudapp.azure.com
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

Aprire il contenitore in azione, toosee fino a un web browser e immettere il nome FQDN hello dell'host Docker:

![Esecuzione di un contenitore ngnix](./media/dockerextension/nginxrunning.png)

## <a name="azure-docker-vm-extension-template-reference"></a>Riferimento al modello dell'estensione di VM Docker di Azure
Hello esempio precedente Usa un modello di avvio rapido esistente. È inoltre possibile distribuire l'estensione della macchina virtuale Docker di Azure hello con i propri modelli di gestione risorse. toodo in tal caso, aggiungere hello seguenti modelli di gestione risorse tooyour, la definizione di hello *vmName* della macchina virtuale in modo appropriato:

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
    "typeHandlerVersion": "1.1",
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

