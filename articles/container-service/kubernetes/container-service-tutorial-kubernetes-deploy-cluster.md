---
title: esercitazione per il servizio contenitore aaaAzure - distribuire Cluster | Documenti Microsoft
description: Esercitazione sul servizio contenitore di Azure - Distribuire un cluster
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
ms.date: 08/21/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: c4c8cc95c88d9c2077d0322f57e5d3159e2dd0ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-kubernetes-cluster-in-azure-container-service"></a>Distribuire un cluster Kubernetes nel servizio contenitore di Azure

Kubernetes fornisce una piattaforma distribuita per applicazioni in contenitori. Con il servizio contenitore di Azure, il provisioning di un cluster Kubernetes pronto per la produzione è semplice e rapido. In questa esercitazione, parte 3 di 7, viene distribuito un cluster Kubernetes del servizio contenitore di Azure. I passaggi completati comprendono:

> [!div class="checklist"]
> * Distribuzione di un cluster del servizio contenitore di Azure Kubernetes
> * Installazione di hello Kubernetes CLI (kubectl)
> * Configurazione di kubectl

Nelle esercitazioni successive, hello Azure voto applicazione viene distribuita cluster toohello, scalato, aggiornate e Operations Management Suite è cluster Kubernetes di hello toomonitor configurato.

## <a name="before-you-begin"></a>Prima di iniziare

Nelle esercitazioni precedenti, un'immagine contenitore è stata creata e caricato l'istanza del Registro di sistema di Azure contenitore tooan. Se si è già questi passaggi e si desidera toofollow lungo, restituire troppo[esercitazione 1: creare le immagini contenitore](./container-service-tutorial-kubernetes-prepare-app.md).

## <a name="create-kubernetes-cluster"></a>Creare un cluster Kubernetes

In hello [esercitazione precedente](./container-service-tutorial-kubernetes-prepare-acr.md), un gruppo di risorse denominato *myResourceGroup* è stato creato. Se questa operazione non è stata ancora eseguita, creare ora il gruppo di risorse.

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```

Creare un cluster di Kubernetes nel servizio contenitore di Azure con hello [az acs creare](/cli/azure/acs#create) comando. 

esempio Hello crea un cluster denominato *myK8sCluster* con uno Linux master nodo e i tre nodi di agente di Linux.

```azurecli-interactive 
az acs create --orchestrator-type=kubernetes --resource-group myResourceGroup --name=myK8SCluster --generate-ssh-keys 
```

Dopo alcuni minuti, completamento del comando hello e restituisce json formattato informazioni sulla distribuzione di hello ACS.

## <a name="install-hello-kubectl-cli"></a>Installare hello kubectl CLI

tooconnect toohello Kubernetes cluster da computer client, utilizzare [kubectl](https://kubernetes.io/docs/user-guide/kubectl/), client di hello Kubernetes della riga di comando. 

Se si usa Azure CloudShell, `kubectl` è già installato. Se si desidera tooinstall utilizzi localmente, hello [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) comando.

Se in esecuzione Linux o Mac OS, potrebbe essere toorun con sudo. In Windows accertarsi che la shell sia stata eseguita come amministratore.

```azurecli-interactive 
az acs kubernetes install-cli 
```

In Windows, è l'installazione predefinita di hello *c:\program files (x86)\kubectl.exe*. Potrebbe essere necessario tooadd questo percorso di file toohello Windows. 

## <a name="connect-with-kubectl"></a>Connettersi con kubectl

tooconfigure `kubectl` tooconnect tooyour Kubernetes cluster, eseguire hello [az acs kubernetes get-credenziali](/cli/azure/acs/kubernetes#get-credentials) comando.

```azurecli-interactive 
az acs kubernetes get-credentials --resource-group=myResourceGroup --name=myK8SCluster
```

tooverify hello connessione tooyour cluster esegue hello [kubectl ottenere nodi](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) comando.

```azurecli-interactive
kubectl get nodes
```

Output:

```bash
NAME                    STATUS                     AGE       VERSION
k8s-agent-98dc3136-0    Ready                      5m        v1.6.2
k8s-agent-98dc3136-1    Ready                      5m        v1.6.2
k8s-agent-98dc3136-2    Ready                      5m        v1.6.2
k8s-master-98dc3136-0   Ready,SchedulingDisabled   5m        v1.6.2
```

Al termine dell'esercitazione, sarà disponibile un cluster Kubernetes del servizio contenitore di Azure pronto per i carichi di lavoro. Nelle esercitazioni successive, un'applicazione multi-contenitore è distribuito toothis cluster, la scalabilità, aggiornate e monitorati.

## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione è stato distribuito un cluster Kubernetes del servizio contenitore di Azure. sono stata completata Hello alla procedura seguente:

> [!div class="checklist"]
> * Distribuzione di un cluster Kubernets del servizio contenitore di Azure
> * Hello installato Kubernetes CLI (kubectl)
> * Configurazione di kubectl

Spostare toohello Avanti toolearn esercitazione sull'esecuzione dell'applicazione in cluster hello.

> [!div class="nextstepaction"]
> [Distribuire un'applicazione in Kubernetes](./container-service-tutorial-kubernetes-deploy-application.md)
