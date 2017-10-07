---
title: esercitazione per il servizio contenitore aaaAzure - applicazioni su larga scala | Documenti Microsoft
description: Esercitazione per il servizio contenitore di Azure - Scalare un'applicazione
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, contenitori, microservizi, Kubernetes, Azure
ms.assetid: 
ms.service: container-service
ms.devlang: aurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: 29571eef0fd91bd6b40f00d8c018539f320179bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="scale-kubernetes-pods-and-kubernetes-infrastructure"></a>Scalare i pod e l'infrastruttura Kubernetes

Se ci ha seguito esercitazioni hello, si dispone di un lavoro Kubernetes cluster nel servizio contenitore di Azure e hello Azure voto app è stata distribuita. 

In questa esercitazione, parte 5, 7, scalabilità POD hello in app hello si cerca la scalabilità automatica pod. Verrà inoltre descritto come numero di hello tooscale di macchina virtuale di Azure agente nodi toochange hello capacità del cluster per ospitare i carichi di lavoro. Le attività completate comprendono:

> [!div class="checklist"]
> * Scalabilità manuale di pod Kubernetes
> * Configurazione di scalabilità automatica POD esecuzione front-end di hello app
> * Ridimensionare i nodi di hello Kubernetes agente di Azure

Nelle esercitazioni successive, viene aggiornato l'applicazione Azure voto hello e Operations Management Suite sono configurati cluster di Kubernetes toomonitor hello.

## <a name="before-you-begin"></a>Prima di iniziare

Nelle esercitazioni precedenti, un'applicazione è stata distribuita in un'immagine contenitore, questa immagine caricata tooAzure contenitore del Registro di sistema e un cluster Kubernetes creato. un'applicazione Hello quindi è stata eseguita nel cluster Kubernetes hello. Se si è già questi passaggi e si desidera toofollow lungo, restituire toohello [esercitazione 1: creare le immagini contenitore](./container-service-tutorial-kubernetes-prepare-app.md). 

Il requisito minimo per questa esercitazione è un cluster Kubernetes con un'applicazione in esecuzione.

## <a name="manually-scale-pods"></a>Scalare manualmente i pod

Finora, hello Azure voto front-end e l'istanza di Redis sono stati distribuiti, ognuno con una singola replica. tooverify, eseguire hello [kubectl ottenere](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) comando.

```azurecli-interactive
kubectl get pods
```

Output:

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-2549686872-4d2r5   1/1       Running   0          31m
azure-vote-front-848767080-tf34m   1/1       Running   0          31m
```

Modificare manualmente il numero di hello di POD in hello `azure-vote-front` distribuzione utilizzando hello [scala kubectl](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#scale) comando. Questo esempio si aumentano too5 numero hello.

```azurecli-interactive
kubectl scale --replicas=5 deployment/azure-vote-front
```

Eseguire [kubectl ottenere POD](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) tooverify che Kubernetes crea POD hello. Dopo un minuto, eseguono POD aggiuntive hello:

```azurecli-interactive
kubectl get pods
```

Output:

```bash
NAME                                READY     STATUS    RESTARTS   AGE
azure-vote-back-2606967446-nmpcf    1/1       Running   0          15m
azure-vote-front-3309479140-2hfh0   1/1       Running   0          3m
azure-vote-front-3309479140-bzt05   1/1       Running   0          3m
azure-vote-front-3309479140-fvcvm   1/1       Running   0          3m
azure-vote-front-3309479140-hrbf2   1/1       Running   0          15m
azure-vote-front-3309479140-qphz8   1/1       Running   0          3m
```

## <a name="autoscale-pods"></a>Scalare automaticamente i pod

Supporta Kubernetes [il ridimensionamento orizzontale pod](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/) POD in una distribuzione a seconda della CPU o altri numerosi hello tooadjust selezionare metriche. 

toouse hello autoscaler, l'unità deve avere le richieste di CPU e i limiti definiti. In hello `azure-vote-front` distribuzione, hello CPU richieste 0,25 contenitore front-end, con un limite pari a 0,5 della CPU. le impostazioni di Hello è simile:

```YAML
resources:
  requests:
     cpu: 250m
  limits:
     cpu: 500m
```

esempio Hello utilizza hello [scalabilità automatica kubectl](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#autoscale) comando tooautoscale hello numero di unità in hello `azure-vote-front` distribuzione. In questo caso, se l'utilizzo della CPU superiore al 50%, hello autoscaler aumenta hello POD tooa massimo 10.


```azurecli-interactive
kubectl autoscale deployment azure-vote-front --cpu-percent=50 --min=3 --max=10
```

stato di hello toosee di autoscaler hello, eseguire hello comando seguente:

```azurecli-interactive
kubectl get hpa
```

Output:

```bash
NAME               REFERENCE                     TARGETS    MINPODS   MAXPODS   REPLICAS   AGE
azure-vote-front   Deployment/azure-vote-front   0% / 50%   3         10        3          2m
```

Dopo alcuni minuti, con un carico minimo sull'app Azure voto hello, numero di hello di repliche pod riduce automaticamente too3.

## <a name="scale-hello-agents"></a>Agenti di hello scala

Se è stato creato il cluster Kubernetes utilizzando i comandi predefiniti nell'esercitazione precedente hello, dispone di tre nodi di agente. Se si prevede più o meno contenitore i carichi di lavoro nel cluster, è possibile modificare manualmente il numero di hello degli agenti. Hello utilizzare [az acs scalare](/cli/azure/acs#scale) comando e specificare il numero di hello di agenti con hello `--new-agent-count` parametro.

esempio Hello aumenta il numero di hello di agente too4 di nodi nel cluster Kubernetes hello denominato *myK8sCluster*. comando Hello accetta un paio di minuti toocomplete.

```azurecli-interactive
az acs scale --resource-group=myResourceGroup --name=myK8SCluster --new-agent-count 4
```

Hello output del comando Mostra il numero di hello dell'agente nodi valore hello `agentPoolProfiles:count`:

```azurecli
{
  "agentPoolProfiles": [
    {
      "count": 4,
      "dnsPrefix": "myK8SCluster-myK8SCluster-e44f25-k8s-agents",
      "fqdn": "",
      "name": "agentpools",
      "vmSize": "Standard_D2_v2"
    }
  ],
...

```

## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione sono state usate diverse funzionalità di scalabilità nel cluster Kubernetes. Le attività descritte includevano:

> [!div class="checklist"]
> * Scalabilità manuale di pod Kubernetes
> * Configurazione di scalabilità automatica POD esecuzione front-end di hello app
> * Ridimensionare i nodi di hello Kubernetes agente di Azure

Spostare toohello Avanti toolearn esercitazione sull'aggiornamento dell'applicazione in Kubernetes.

> [!div class="nextstepaction"]
> [Aggiornare un'applicazione in Kubernetes](./container-service-tutorial-kubernetes-app-update.md)

