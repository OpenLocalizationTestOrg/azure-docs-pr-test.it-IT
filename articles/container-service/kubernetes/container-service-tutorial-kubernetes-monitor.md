---
title: esercitazione per il servizio contenitore aaaAzure - monitoraggio Kubernetes | Documenti Microsoft
description: Esercitazione sul servizio contenitore di Azure - Monitorare Kubernetes con Microsoft Operations Management Suite (OMS)
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
ms.openlocfilehash: 54fa789453768529deaf25d7575e5b21d0e41882
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-kubernetes-cluster-with-operations-management-suite"></a>Monitorare un cluster Kubernetes con Operations Management Suite

Il monitoraggio del cluster e dei contenitori Kubernetes è critico, soprattutto quando si gestisce un cluster di produzione su larga scala con più app. 

È possibile sfruttare diverse soluzioni di monitoraggio di Kubernetes, da Microsoft o da altri provider. In questa esercitazione, monitorare il cluster Kubernetes utilizzando hello contenitori soluzione in [Operations Management Suite](../../operations-management-suite/operations-management-suite-overview.md), soluzione di gestione IT Microsoft basata sul cloud. (hello soluzione contenitori OMS è in anteprima).

In questa esercitazione, parte 7 di sette, copre hello seguenti attività:

> [!div class="checklist"]
> * Ottenere le impostazioni dell'area di lavoro di OMS
> * Configurare gli agenti OMS nei nodi Kubernetes hello
> * Accedere a informazioni di monitoraggio nel portale di OMS hello o il portale di Azure

## <a name="before-you-begin"></a>Prima di iniziare

Nelle esercitazioni precedenti, un'applicazione è stata assemblata in immagini contenitore, queste immagini caricate tooAzure contenitore del Registro di sistema e un cluster Kubernetes creato. Se si è già questi passaggi e si desidera toofollow lungo, restituire troppo[esercitazione 1: creare le immagini contenitore](./container-service-tutorial-kubernetes-prepare-app.md). 

Come requisito minimo, questa esercitazione richiede un cluster Kubernetes con nodi di agente di Linux, e un account di Operations Management Suite (OMS). Se necessario, registrarsi per una [versione di valutazione gratuita di OMS](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial).

## <a name="get-workspace-settings"></a>Ottenere le impostazioni dell'area di lavoro

Quando è possibile accedere a hello [portale OMS](https://mms.microsoft.com), andare troppo**impostazioni** > **Connected Sources** > **server Linux**. Non esiste, è possibile trovare hello *ID area di lavoro* e un database primario o secondario *chiave dell'area di lavoro*. Prendere nota di questi valori, che è necessario tooset installare gli agenti OMS in cluster hello.

## <a name="set-up-oms-agents"></a>Configurare gli agenti OMS

Di seguito è riportato un tooset file YAML installare gli agenti OMS nei nodi del cluster Linux hello. Questa operazione crea un [DaemonSet](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/) di Kubernetes, che esegue un singolo pod identico in ogni nodo del cluster. risorsa DaemonSet Hello è ideale per la distribuzione di un agente di monitoraggio. 

Salvare i seguenti file di testo tooa denominato hello `oms-daemonset.yaml`e sostituire i valori segnaposto hello per *myWorkspaceID* e *myWorkspaceKey* con l'ID area di lavoro OMS e la chiave. (nell'ambiente di produzione, è possibile codificare questi valori come segreti).

```YAML
apiVersion: extensions/v1beta1
kind: DaemonSet
metadata:
 name: omsagent
spec:
 template:
  metadata:
   labels:
    app: omsagent
    agentVersion: v1.3.4-127
    dockerProviderVersion: 10.0.0-25
  spec:
   containers:
     - name: omsagent 
       image: "microsoft/oms"
       imagePullPolicy: Always
       env:
       - name: WSID
         value: myWorkspaceID
       - name: KEY 
         value: myWorkspaceKey
       - name: DOMAIN
         value: opinsights.azure.com
       securityContext:
         privileged: true
       ports:
       - containerPort: 25225
         protocol: TCP 
       - containerPort: 25224
         protocol: UDP
       volumeMounts:
        - mountPath: /var/run/docker.sock
          name: docker-sock
        - mountPath: /var/log 
          name: host-log
       livenessProbe:
        exec:
         command:
         - /bin/bash
         - -c
         - ps -ef | grep omsagent | grep -v "grep"
        initialDelaySeconds: 60
        periodSeconds: 60
   volumes:
    - name: docker-sock 
      hostPath:
       path: /var/run/docker.sock
    - name: host-log
      hostPath:
       path: /var/log
```

Creare hello DaemonSet con hello comando seguente:

```azurecli-interactive
kubectl create -f oms-daemonset.yaml
```

toosee tale hello DaemonSet viene creato, eseguire:

```azurecli-interactive
kubectl get daemonset
```

L'output è simile toohello seguenti:

```azurecli-interactive
NAME       DESIRED   CURRENT   READY     UP-TO-DATE   AVAILABLE   NODE-SELECTOR   AGE
omsagent   3         3         3         0            3           <none>          5m
```

Dopo che sono in esecuzione gli agenti di hello, sono necessari diversi minuti per OMS tooingest ed elaborare hello i dati.

## <a name="access-monitoring-data"></a>Accesso ai dati di monitoraggio

Visualizzare e analizzare i dati con hello di monitoraggio tipo contenitore hello OMS [soluzione contenitore](../../log-analytics/log-analytics-containers.md) nel portale di OMS hello o hello portale di Azure. 

soluzione di contenitore hello tooinstall hello [portale OMS](https://mms.microsoft.com), andare troppo**Solutions Gallery**. Aggiungere quindi la **Soluzione Contenitore**. In alternativa, aggiungere soluzioni contenitori hello da hello [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/microsoft.containersoms?tab=Overview).

Nel portale OMS hello, cercare un **contenitori** riquadro Riepilogo del dashboard OMS hello. Fare clic sul riquadro hello per dettagli, tra cui: utilizzo della CPU e memoria, errori, lo stato, inventario immagine ed eventi di contenitore. Per informazioni più granulari, fare clic su una riga in qualsiasi riquadro o eseguire una [ricerca log](../../log-analytics/log-analytics-log-searches.md).

![Dashboard dei contenitori nel portale OMS](./media/container-service-tutorial-kubernetes-monitor/oms-containers-dashboard.png)

Analogamente, nel portale di Azure hello, andare troppo**Analitica Log** e selezionare il nome dell'area di lavoro. hello toosee **contenitori** sezione di riepilogo, fare clic su **soluzioni** > **contenitori**. toosee dettagli, fare clic su riquadro hello.

Vedere hello [documentazione di Azure Log Analitica](../../log-analytics/index.md) per istruzioni dettagliate sulla query e analisi dei dati di monitoraggio.

## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione è stato monitorato il cluster di Kubernetes con OMS. Le attività descritte includevano:

> [!div class="checklist"]
> * Ottenere le impostazioni dell'area di lavoro di OMS
> * Configurare gli agenti OMS nei nodi Kubernetes hello
> * Accedere a informazioni di monitoraggio nel portale di OMS hello o il portale di Azure


Seguire questo toosee di collegamento incorporati gli esempi di script per il servizio contenitore.

> [!div class="nextstepaction"]
> [Esempi di script del servizio contenitore di Azure](cli-samples.md)
