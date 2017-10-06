---
title: aaaAzure avvio rapido del servizio contenitore - distribuire controller di dominio o del sistema operativo Cluster | Documenti Microsoft
description: Guida rapida al servizio contenitore di Azure - Distribuire un cluster DC/OS
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
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/04/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: b961f15bd73deeafda5a3fc25ab53c839195219b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-dcos-cluster"></a>Distribuire un cluster DC/OS

DC/OS fornisce una piattaforma distribuita per l'esecuzione di applicazioni in contenitori e moderne. Con il servizio contenitore di Azure, il provisioning di un cluster DC/OS pronto per la produzione è semplice e rapido. Questo passaggi di base di avvio rapido dettagli hello necessari toodeploy un cluster di controller di dominio o del sistema operativo e un carico di lavoro di base esecuzione.

Se non si ha una sottoscrizione di Azure, creare un [account gratuito](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) prima di iniziare.

Questa esercitazione richiede hello Azure CLI versione 2.0.4 o versioni successive. Eseguire `az --version` versione hello toofind. Se è necessario tooupgrade, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="log-in-tooazure"></a>Accedi tooAzure 

Accedere alla sottoscrizione di Azure con hello tooyour [accesso az](/cli/azure/#login) comando e seguire hello le direzioni.

```azurecli
az login
```

## <a name="create-a-resource-group"></a>Creare un gruppo di risorse

Creare un gruppo di risorse con hello [gruppo az creare](/cli/azure/group#create) comando. Un gruppo di risorse di Azure è un contenitore logico in cui le risorse di Azure vengono distribuite e gestite. 

esempio Hello crea un gruppo di risorse denominato *myResourceGroup* in hello *eastus* percorso.

```azurecli
az group create --name myResourceGroup --location eastus
```

## <a name="create-dcos-cluster"></a>Creare un cluster DC/OS

Creare un cluster di controller di dominio o del sistema operativo con hello [az acs creare](/cli/azure/acs#create) comando.

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

può essere testato tunnel SSH Hello esplorando troppo`http://localhost`. Se una porta altro che è stata utilizzata 80, modificare toomatch percorso hello. 

Se tunnel SSH hello è stato creato correttamente, viene restituito il portale di controller di dominio/OS hello.

![Interfaccia utente di DC/OS](./media/container-service-dcos-quickstart/dcos-ui.png)

## <a name="install-dcos-cli"></a>Installare l'interfaccia della riga di comando di DC/OS

interfaccia della riga di comando DC/OS Hello è toomanage usato un cluster di controller di dominio o del sistema operativo da hello della riga di comando. Installare hello cli di controller di dominio/OS utilizzando hello [az acs dcos install-cli](/azure/acs/dcos#install-cli) comando. Se si utilizza Azure CloudShell, hello CLI di controller di dominio o del sistema operativo è già installato. 

Se si esegue hello CLI di Azure in macOS o Linux, potrebbe essere comando hello toorun con sudo.

```azurecli
az acs dcos install-cli
```

Prima di hello che CLI può essere utilizzato con i cluster di hello, deve essere tunnel SSH di hello toouse configurato. toodo in tal caso, eseguire hello comando seguente, modificare la porta hello se necessario.

```azurecli
dcos config set core.dcos_url http://localhost
```

## <a name="run-an-application"></a>Eseguire un'applicazione

valore predefinito di Hello meccanismo per un cluster ACS controller di dominio o del sistema operativo di pianificazione è maratona. Maratona toostart utilizzata un'applicazione e gestire lo stato di hello di un'applicazione hello nel cluster di controller di dominio/OS hello. tooschedule un'applicazione tramite maratona, creare un file denominato *maratona app.json*, e hello copia seguendo contenuto al suo interno. 

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
dcos marathon app add marathon-app.json
```

stato della distribuzione toosee hello per le app di hello, eseguire hello comando seguente.

```azurecli
dcos marathon app list
```

Quando hello **in attesa** passa il valore di colonna da *True* troppo*False*, la distribuzione di applicazioni è stata completata.

```azurecli
ID     MEM  CPUS  TASKS  HEALTH  DEPLOYMENT  WAITING  CONTAINER  CMD   
/test   32   1     1/1    ---       ---      False      DOCKER   None
```

Ottenere l'indirizzo IP pubblico hello degli agenti di hello controller di dominio o del sistema operativo cluster.

```azurecli
az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-agent')].[ipAddress]" -o tsv
```

Esplorazione toothis indirizzo restituisce sito NGINX di hello predefinito.

![NGINX](./media/container-service-dcos-quickstart/nginx.png)

## <a name="delete-dcos-cluster"></a>Eliminare il cluster DC/OS

Quando non è più necessario, è possibile utilizzare hello [eliminazione gruppo az](/cli/azure/group#delete) comandi tooremove gruppo di risorse hello, cluster/OS di controller di dominio e tutte le relative risorse.

```azurecli
az group delete --name myResourceGroup --no-wait
```

## <a name="next-steps"></a>Passaggi successivi

In questa Guida introduttiva, è stato distribuito un cluster di controller di dominio o del sistema operativo e l'esecuzione un semplice contenitore Docker in cluster hello. toolearn ulteriori informazioni su servizio di contenitore di Azure, continuare esercitazioni toohello ACS.

> [!div class="nextstepaction"]
> [Gestire un cluster DC/OS del servizio contenitore di Azure](container-service-dcos-manage-tutorial.md)