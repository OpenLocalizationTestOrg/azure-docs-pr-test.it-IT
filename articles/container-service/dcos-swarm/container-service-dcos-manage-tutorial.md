---
title: esercitazione per il servizio contenitore aaaAzure - controller di dominio di gestione del sistema operativo | Documenti Microsoft
description: Esercitazione sul servizio contenitore di Azure - Gestire DC/OS
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, contenitori, Micro-Service, Kubernetes, DC/OS, Azure
ms.assetid: 
ms.service: container-service
ms.devlang: azurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/17/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: b91c433bfd7e48ec405cc62be1486d9d4662839d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-service-tutorial---manage-dcos"></a>Esercitazione sul servizio contenitore di Azure - Gestire DC/OS

DC/OS fornisce una piattaforma distribuita per l'esecuzione di applicazioni in contenitori e moderne. Con il servizio contenitore di Azure, il provisioning di un cluster DC/OS pronto per la produzione è semplice e rapido. Questo passaggi di base di informazioni di avvio rapido necessari toodeploy un cluster di controller di dominio o del sistema operativo e un carico di lavoro di base esecuzione.

> [!div class="checklist"]
> * Creare un cluster DC/OS del servizio contenitore di Azure
> * Connettere il cluster toohello
> * Installare controller di dominio/OS CLI hello
> * Distribuire un cluster di toohello applicazione
> * Scalabilità di un'applicazione in cluster hello
> * Ridimensionare i nodi del cluster hello controller di dominio o del sistema operativo
> * Gestione di base di DC/OS
> * Eliminare il cluster di controller di dominio/OS hello

Questa esercitazione richiede hello Azure CLI versione 2.0.4 o versioni successive. Eseguire `az --version` versione hello toofind. Se è necessario tooupgrade, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="create-dcos-cluster"></a>Creare un cluster DC/OS

Innanzitutto, creare un gruppo di risorse con hello [gruppo az creare](/cli/azure/group#create) comando. Un gruppo di risorse di Azure è un contenitore logico in cui le risorse di Azure vengono distribuite e gestite. 

esempio Hello crea un gruppo di risorse denominato *myResourceGroup* in hello *westeurope* percorso.

```azurecli
az group create --name myResourceGroup --location westeurope
```

Successivamente, creare un cluster di controller di dominio o del sistema operativo con hello [az acs creare](/cli/azure/acs#create) comando.

esempio Hello crea un cluster di controller di dominio o del sistema operativo denominato *myDCOSCluster* e crea le chiavi SSH se non esiste già. toouse uno specifico set di chiavi, utilizzare hello `--ssh-key-value` opzione.  

```azurecli
az acs create \
  --orchestrator-type dcos \
  --resource-group myResourceGroup \
  --name myDCOSCluster \
  --generate-ssh-keys
```

Dopo alcuni minuti, comando hello completa e restituisce informazioni sulla distribuzione di hello.

## <a name="connect-toodcos-cluster"></a>Connettere il cluster tooDC/OS

Dopo aver creato un cluster DC/OS, è possibile accedervi tramite un tunnel SSH. Comando che segue di esecuzione hello tooreturn hello indirizzo IP pubblico del database master di controller di dominio/OS hello. Questo indirizzo IP è archiviato in una variabile e usato nel passaggio successivo hello.

```azurecli
ip=$(az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-master')].[ipAddress]" -o tsv)
```

toocreate hello tunnel SSH, eseguire hello comando seguente e istruzioni hello sullo schermo. Se la porta 80 è già in uso, il comando hello ha esito negativo. Hello aggiornamento tunneled tooone porta non è in uso, ad esempio `85:localhost:80`. 

```azurecli
sudo ssh -i ~/.ssh/id_rsa -fNL 80:localhost:80 -p 2200 azureuser@$ip
```

## <a name="install-dcos-cli"></a>Installare l'interfaccia della riga di comando di DC/OS

Installare hello cli di controller di dominio/OS utilizzando hello [az acs dcos install-cli](/azure/acs/dcos#install-cli) comando. Se si utilizza Azure CloudShell, hello CLI di controller di dominio o del sistema operativo è già installato. Se si esegue hello CLI di Azure in macOS o Linux, potrebbe essere comando hello toorun con sudo.

```azurecli
az acs dcos install-cli
```

Prima di hello che CLI può essere utilizzato con i cluster di hello, deve essere tunnel SSH di hello toouse configurato. toodo in tal caso, eseguire hello comando seguente, modificare la porta hello se necessario.

```azurecli
dcos config set core.dcos_url http://localhost
```

## <a name="run-an-application"></a>Eseguire un'applicazione

valore predefinito di Hello meccanismo per un cluster ACS controller di dominio o del sistema operativo di pianificazione è maratona. Maratona toostart utilizzata un'applicazione e gestire lo stato di hello di un'applicazione hello nel cluster di controller di dominio/OS hello. tooschedule un'applicazione tramite maratona, creare un file denominato **maratona app.json**, e hello copia seguendo contenuto al suo interno. 

```json
{
  "id": "demo-app-private",
  "cmd": null,
  "cpus": 1,
  "mem": 32,
  "disk": 0,
  "instances": 1,
  "container": {
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        {
          "containerPort": 80,
          "protocol": "tcp",
          "name": "80",
          "labels": null
        }
      ]
    },
    "type": "DOCKER"
  }
}
```

Eseguire hello successivo comando tooschedule hello applicazione toorun nel cluster di controller di dominio/OS hello.

```azurecli
dcos marathon app add marathon-app.json
```

stato della distribuzione toosee hello per le app di hello, eseguire hello comando seguente.

```azurecli
dcos marathon app list
```

Quando hello **attività** passa il valore di colonna da *0/1* troppo*1/1*, la distribuzione di applicazioni è stata completata.

```azurecli
ID     MEM  CPUS  TASKS  HEALTH  DEPLOYMENT  WAITING  CONTAINER  CMD   
/test   32   1     0/1    ---       ---      False      DOCKER   None
```

## <a name="scale-marathon-application"></a>Ridimensionare l'applicazione Marathon

Nell'esempio precedente hello è stata creata un'applicazione a istanza singola. Questa distribuzione in modo che siano disponibili, tre istanze di un'applicazione hello aprire hello tooupdate **maratona app.json** file e aggiornare hello istanza proprietà too3.

```json
{
  "id": "demo-app-private",
  "cmd": null,
  "cpus": 1,
  "mem": 32,
  "disk": 0,
  "instances": 3,
  "container": {
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        {
          "containerPort": 80,
          "protocol": "tcp",
          "name": "80",
          "labels": null
        }
      ]
    },
    "type": "DOCKER"
  }
}
```

Aggiornare l'applicazione hello utilizzando hello `dcos marathon app update` comando.

```azurecli
dcos marathon app update demo-app-private < marathon-app.json
```

stato della distribuzione toosee hello per le app di hello, eseguire hello comando seguente.

```azurecli
dcos marathon app list
```

Quando hello **attività** passa il valore di colonna da *1/3* troppo*3/1*, la distribuzione di applicazioni è stata completata.

```azurecli
ID     MEM  CPUS  TASKS  HEALTH  DEPLOYMENT  WAITING  CONTAINER  CMD   
/test   32   1     1/3    ---       ---      False      DOCKER   None
```

## <a name="run-internet-accessible-app"></a>Eseguire un'app accessibile su Internet

Hello ACS controller di dominio o del sistema operativo cluster include due set di nodi, una pubblica accessibile su internet di hello e una privata che non è accessibile su internet di hello. set predefinito di Hello è nodi privata hello, che è stato usato nell'ultimo esempio hello.

un'applicazione accessibile toomake in hello internet, distribuirle toohello set di nodi pubblici. toodo, valutare hello `acceptedResourceRoles` il valore dell'oggetto `slave_public`.

Creare un file denominato **nginx public.json** e hello copia seguendo contenuto al suo interno.

```json
{
  "id": "demo-app",
  "cmd": null,
  "cpus": 1,
  "mem": 32,
  "disk": 0,
  "instances": 1,
  "container": {
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        {
          "containerPort": 80,
          "hostPort": 80,
          "protocol": "tcp",
          "name": "80",
          "labels": null
        }
      ]
    },
    "type": "DOCKER"
  },
  "acceptedResourceRoles": [
    "slave_public"
  ]
}
```

Eseguire hello successivo comando tooschedule hello applicazione toorun nel cluster di controller di dominio/OS hello.

```azurecli 
dcos marathon app add nginx-public.json
```

Ottenere l'indirizzo IP pubblico hello degli agenti di cluster pubblica hello controller di dominio o del sistema operativo.

```azurecli 
az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-agent')].[ipAddress]" -o tsv
```

Esplorazione toothis indirizzo restituisce sito NGINX di hello predefinito.

![NGINX](./media/container-service-dcos-manage-tutorial/nginx.png)

## <a name="scale-dcos-cluster"></a>Ridimensionare il cluster DC/OS

Negli esempi precedenti hello, un'applicazione è stato ridimensionato toomultiple istanza. infrastruttura di controller di dominio/OS Hello può anche essere scalato tooprovide più o meno capacità di calcolo. Questa operazione viene eseguita con hello [az acs scalare]() comando. 

numero corrente di hello toosee degli agenti di controller di dominio o del sistema operativo, utilizzare hello [az acs Mostra](/cli/azure/acs#show) comando.

```azurecli
az acs show --resource-group myResourceGroup --name myDCOSCluster --query "agentPoolProfiles[0].count"
```

tooincrease hello too5 count, utilizzare hello [az acs scalare](/cli/azure/acs#scale) comando. 

```azurecli
az acs scale --resource-group myResourceGroup --name myDCOSCluster --new-agent-count 5
```

## <a name="delete-dcos-cluster"></a>Eliminare il cluster DC/OS

Quando non è più necessario, è possibile utilizzare hello [eliminazione gruppo az](/cli/azure/group#delete) comandi tooremove gruppo di risorse hello, cluster/OS di controller di dominio e tutte le relative risorse.

```azurecli 
az group delete --name myResourceGroup --no-wait
```

## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione, si è appreso sulle attività di gestione di controller di dominio o del sistema operativo base inclusi hello seguenti. 

> [!div class="checklist"]
> * Creare un cluster DC/OS del servizio contenitore di Azure
> * Connettere il cluster toohello
> * Installare controller di dominio/OS CLI hello
> * Distribuire un cluster di toohello applicazione
> * Scalabilità di un'applicazione in cluster hello
> * Ridimensionare i nodi del cluster hello controller di dominio o del sistema operativo
> * Eliminare il cluster di controller di dominio/OS hello

Anticipo toohello successivo dell'esercitazione toolearn su caricare l'applicazione di bilanciamento del carico nel controller di dominio o sistema operativo in Azure. 

> [!div class="nextstepaction"]
> [Bilanciare il carico delle applicazioni](container-service-load-balancing.md)