---
title: aaaQuickstart - cluster Kubernetes di Azure per Windows | Documenti Microsoft
description: Consente di capire velocemente toocreate un cluster Kubernetes per i contenitori di Windows nel servizio contenitore di Azure con hello CLI di Azure.
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: 85fe65a46ae8c78797e8a8a097c2a37f06329335
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-kubernetes-cluster-for-windows-containers"></a>Distribuire cluster Kubernetes per contenitori Windows

Hello CLI di Azure viene utilizzato toocreate e gestire le risorse di Azure dalla riga di comando hello o negli script. Questa guida descrive con hello Azure CLI toodeploy un [Kubernetes](https://kubernetes.io/docs/home/) cluster nel [servizio contenitore di Azure](../container-service-intro.md). Dopo aver distribuito il cluster hello, ci si connette tooit con hello Kubernetes `kubectl` strumento da riga di comando e distribuire il primo contenitore di Windows.

Se non si ha una sottoscrizione di Azure, creare un [account gratuito](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) prima di iniziare.

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Se si sceglie tooinstall e utilizza hello CLI in locale, questa Guida rapida richiede che sia in esecuzione hello Azure CLI versione 2.0.4 o versioni successive. Eseguire `az --version` versione hello toofind. Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli). 

> [!NOTE]
> Il supporto per i contenitori Windows in Kubernetes nel servizio contenitore di Azure è disponibile in versione di anteprima. 
>

## <a name="create-a-resource-group"></a>Creare un gruppo di risorse

Creare un gruppo di risorse con hello [gruppo az creare](/cli/azure/group#create) comando. Un gruppo di risorse di Azure è un gruppo logico in cui le risorse di Azure vengono distribuite e gestite. 

esempio Hello crea un gruppo di risorse denominato *myResourceGroup* in hello *eastus* percorso.

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-kubernetes-cluster"></a>Creare un cluster Kubernetes
Creare un cluster di Kubernetes nel servizio contenitore di Azure con hello [az acs creare](/cli/azure/acs#create) comando. 

esempio Hello crea un cluster denominato *myK8sCluster* con uno Linux master nodo e due nodi di agente di Windows. Questo esempio crea SSH master Linux toohello tooconnect necessari di chiavi. Questo esempio viene utilizzato *azureuser* per un nome utente amministrativo e *myPassword12* come password hello nei nodi di Windows hello. Aggiornare questi ambiente appropriato tooyour toosomething di valori. 



```azurecli-interactive 
az acs create --orchestrator-type=kubernetes \
    --resource-group myResourceGroup \
    --name=myK8sCluster \
    --agent-count=2 \
    --generate-ssh-keys \
    --windows --admin-username azureuser \
    --admin-password myPassword12
```

Dopo alcuni minuti, hello comando viene completato e vengono visualizzate informazioni sulla distribuzione.

## <a name="install-kubectl"></a>Installare kubectl

tooconnect toohello Kubernetes cluster da computer client, utilizzare [ `kubectl` ](https://kubernetes.io/docs/user-guide/kubectl/), client di hello Kubernetes della riga di comando. 

Se si usa Azure CloudShell, `kubectl` è già installato. Se si desidera tooinstall in locale, può utilizzare hello [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) comando.

Hello seguente installa esempio CLI di Azure `kubectl` tooyour sistema. In Windows eseguire questo comando come amministratore.

```azurecli-interactive 
az acs kubernetes install-cli
```


## <a name="connect-with-kubectl"></a>Connettersi con kubectl

tooconfigure `kubectl` tooconnect tooyour Kubernetes cluster, eseguire hello [az acs kubernetes get-credenziali](/cli/azure/acs/kubernetes#get-credentials) comando. Hello esempio download di configurazione del cluster per il cluster Kubernetes hello.

```azurecli-interactive 
az acs kubernetes get-credentials --resource-group=myResourceGroup --name=myK8sCluster
```

tooverify cluster tooyour hello connessione dal computer, provare a eseguire:

```azurecli-interactive
kubectl get nodes
```

`kubectl`Elenca i nodi master e l'agente di hello.

```azurecli-interactive
NAME                    STATUS                     AGE       VERSION
k8s-agent-98dc3136-0    Ready                      5m        v1.5.3
k8s-agent-98dc3136-1    Ready                      5m        v1.5.3
k8s-master-98dc3136-0   Ready,SchedulingDisabled   5m        v1.5.3

```

## <a name="deploy-a-windows-iis-container"></a>Distribuire un contenitore IIS Windows

È possibile eseguire un contenitore Docker all'interno di un *pod* Kubernetes, che contiene uno o più contenitori. 

Questo esempio di base viene utilizzato un toospecify file JSON un contenitore di Microsoft Internet Information Server (IIS) e quindi crea pod hello utilizzando hello `kubctl apply` comando. 

Creare un file locale denominato `iis.json` e hello copia seguendo il testo. Questo file indica Kubernetes toorun IIS in Windows Server 2016 Nano Server, usando un'immagine di contenitore pubblico da [Hub Docker](https://hub.docker.com/r/nanoserver/iis/). contenitore di Hello Usa la porta 80, ma inizialmente è accessibile solo all'interno di rete di cluster hello.

 ```JSON
 {
  "apiVersion": "v1",
  "kind": "Pod",
  "metadata": {
    "name": "iis",
    "labels": {
      "name": "iis"
    }
  },
  "spec": {
    "containers": [
      {
        "name": "iis",
        "image": "nanoserver/iis",
        "ports": [
          {
          "containerPort": 80
          }
        ]
      }
    ],
    "nodeSelector": {
     "beta.kubernetes.io/os": "windows"
     }
   }
 }
 ```

pod hello toostart, di tipo:
  
```azurecli-interactive
kubectl apply -f iis.json
```  

distribuzione di hello tootrack, tipo:
  
```azurecli-interactive
kubectl get pods
```

Durante la distribuzione di pod hello, lo stato di hello è `ContainerCreating`. Può richiedere alcuni minuti per hello di hello contenitore tooenter `Running` stato.

```azurecli-interactive
NAME     READY        STATUS        RESTARTS    AGE
iis      1/1          Running       0           32s
```

## <a name="view-hello-iis-welcome-page"></a>Hello Visualizza la pagina iniziale di IIS

tooexpose pod toohello HelloWorld con un indirizzo IP pubblico, hello tipo comando seguente:

```azurecli-interactive
kubectl expose pods iis --port=80 --type=LoadBalancer
```

Con questo comando, Kubernetes crea un servizio e un [regola di bilanciamento del carico di Azure](container-service-kubernetes-load-balancing.md) con un indirizzo IP pubblico per il servizio di hello. 

Eseguire hello seguente lo stato del comando toosee hello del servizio hello.

```azurecli-interactive
kubectl get svc
```

Indirizzo IP hello viene inizialmente visualizzato come `pending`. Dopo alcuni minuti, hello indirizzo IP esterno di hello `iis` pod è impostato:
  
```azurecli-interactive
NAME         CLUSTER-IP     EXTERNAL-IP     PORT(S)        AGE       
kubernetes   10.0.0.1       <none>          443/TCP        21h       
iis          10.0.111.25    13.64.158.233   80/TCP         22m
```

È possibile utilizzare le scelte toosee hello IIS pagina iniziale predefinita di un browser web all'indirizzo IP esterno hello:

![Immagine di esplorazione tooIIS](./media/container-service-kubernetes-windows-walkthrough/kubernetes-iis.png)  


## <a name="delete-cluster"></a>Eliminare il cluster
Quando il cluster hello non è più necessario, è possibile utilizzare hello [eliminazione gruppo az](/cli/azure/group#delete) comandi gruppo di risorse hello tooremove, il servizio contenitore e tutte le relative risorse.

```azurecli-interactive 
az group delete --name myResourceGroup
```


## <a name="next-steps"></a>Passaggi successivi

In questa guida introduttiva è stato distribuito un cluster Kubernetes, è stata eseguita la connessione con `kubectl` ed è stato distribuito un pod con un contenitore IIS. toolearn ulteriori informazioni su servizio di contenitore di Azure, continuare toohello Kubernetes esercitazione.

> [!div class="nextstepaction"]
> [Gestire un cluster Kubernetes ACS](container-service-tutorial-kubernetes-prepare-app.md)
