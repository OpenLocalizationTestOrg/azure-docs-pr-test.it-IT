---
title: cluster di Azure Kubernetes aaaMonitor - Operations Manager | Documenti Microsoft
description: Monitoraggio di cluster Kubernetes nel servizio contenitore di Azure con Microsoft Operations Management Suite
services: container-service
documentationcenter: 
author: bburns
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
ms.date: 12/09/2016
ms.author: bburns
ms.custom: mvc
ms.openlocfilehash: 7474ee1571134ffe43ff8e4041cf5a64f5635bb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-microsoft-operations-management-suite-oms"></a>Monitorare un cluster del servizio contenitore di Azure con Microsoft Operations Management Suite (OMS)

## <a name="prerequisites"></a>Prerequisiti
Si presume che questa procedura dettagliata abbia [creato un cluster Kubernetes mediante il servizio contenitore di Azure](container-service-kubernetes-walkthrough.md).

Inoltre, presuppone di aver hello `az` cli di Azure e `kubectl` installati gli strumenti.

È possibile verificare se si dispone di hello `az` strumento installato eseguendo:

```console
$ az --version
```

Se non si dispone di hello `az` strumento installato, non esistono istruzioni [qui](https://github.com/azure/azure-cli#installation).  
In alternativa, è possibile utilizzare [Azure Cloud Shell](https://docs.microsoft.com/en-us/azure/cloud-shell/overview), che dispone di hello `az` cli di Azure e `kubectl` strumenti già installati.  

È possibile verificare se si dispone di hello `kubectl` strumento installato eseguendo:

```console
$ kubectl version
```

Se `kubectl` non è installato, è possibile eseguire:
```console
$ az acs kubernetes install-cli
```

tootest se si dispongono di chiavi kubernetes installate nello strumento di kubectl è possibile eseguire:
```console
$ kubectl get nodes
```

Se hello sopra errori comando, sono necessarie le chiavi di cluster di tooinstall kubernetes nello strumento di kubectl desiderato. È possibile farlo con hello comando seguente:
```console
RESOURCE_GROUP=my-resource-group
CLUSTER_NAME=my-acs-name
az acs kubernetes get-credentials --resource-group=$RESOURCE_GROUP --name=$CLUSTER_NAME
```

## <a name="monitoring-containers-with-operations-management-suite-oms"></a>Monitoraggio dei contenitori con Operations Management Suite (OMS)

Microsoft Operations Management (OMS) è la soluzione Microsoft per la gestione IT basata sul cloud che consente di gestire e proteggere l'infrastruttura locale e cloud. Soluzione di contenitore è una soluzione Analitica di Log di OMS, che consente di visualizzare l'inventario contenitore hello, prestazioni e i log in un'unica posizione. È possibile audit, risoluzione dei contenitori di visualizzazione dei log di hello in posizione centralizzata e trovare rumore utilizzo in eccesso contenitore in un host.

![](media/container-service-monitoring-oms/image1.png)

Per ulteriori informazioni sulla soluzione di contenitore, vedere toothe [contenitore soluzione Log Analitica](../../log-analytics/log-analytics-containers.md).

## <a name="installing-oms-on-kubernetes"></a>Installazione di OMS in Kubernetes

### <a name="obtain-your-workspace-id-and-key"></a>Ottenere l'ID e la chiave dell'area di lavoro
Per hello servizio toohello tootalk dell'agente OMS deve toobe configurato con un id area di lavoro e una chiave dell'area di lavoro. id tooget hello e la chiave è necessario un OMS toocreate account in <https://mms.microsoft.com>. Seguire hello passaggi toocreate un account. Dopo aver terminato la creazione di account di hello, è necessario tooobtain l'id e la chiave facendo **impostazioni**, quindi **Connected Sources**e quindi **server Linux**, come illustrato di seguito.

 ![](media/container-service-monitoring-oms/image5.png)

### <a name="install-hello-oms-agent-using-a-daemonset"></a>Installare l'agente OMS hello utilizzando un DaemonSet
DaemonSets vengono utilizzati da Kubernetes toorun una singola istanza di un contenitore in ogni host in cluster hello.
Sono ideali per l'esecuzione di agenti di monitoraggio.

Ecco hello [file DaemonSet YAML](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes). Salvare il file tooa denominato `oms-daemonset.yaml` e sostituire i valori segnaposto hello per `WSID` e `KEY` con l'id area di lavoro e la chiave nel file hello.

Dopo aver aggiunto l'ID e la configurazione di DaemonSet toohello chiave, è possibile installare l'agente OMS hello in cluster con hello `kubectl` strumento da riga di comando:

```console
$ kubectl create -f oms-daemonset.yaml
```

### <a name="installing-hello-oms-agent-using-a-kubernetes-secret"></a>Installazione agente OMS hello utilizzando un segreto Kubernetes
tooprotect l'ID area di lavoro OMS e la chiave è possibile utilizzare Kubernetes segreto come parte del file DaemonSet YAML.

 - Copia script hello, file di modello segreta e hello file DaemonSet YAML (da [repository](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes)) e assicurarsi che siano presenti hello stessa directory. 
      - Script per la generazione di segreti: secret-gen.sh
      - Modello di segreto: secret-template.yaml
   - File DaemonSet YAML: omsagent-ds-secrets.yaml
 - Eseguire script hello. script Hello verrà chiesta hello ID area di lavoro OMS e la chiave primaria. Inserire che e script hello creerà un file di secret yaml in modo da eseguire.   
   ```
   #> sudo bash ./secret-gen.sh 
   ```

   - Creare pod segreti hello eseguendo hello:``` kubectl create -f omsagentsecret.yaml ```
 
   - toocheck, eseguire hello seguente: 

   ``` 
   root@ubuntu16-13db:~# kubectl get secrets
   NAME                  TYPE                                  DATA      AGE
   default-token-gvl91   kubernetes.io/service-account-token   3         50d
   omsagent-secret       Opaque                                2         1d
   root@ubuntu16-13db:~# kubectl describe secrets omsagent-secret
   Name:           omsagent-secret
   Namespace:      default
   Labels:         <none>
   Annotations:    <none>

   Type:   Opaque

   Data
   ====
   WSID:   36 bytes
   KEY:    88 bytes 
   ```
 
  - Creare il DaemonSet dell'agente OMS eseguendo l'istruzione ``` kubectl create -f omsagent-ds-secrets.yaml ```

### <a name="conclusion"></a>Conclusione
L'operazione è terminata. Dopo alcuni minuti, si dovrebbe essere toosee in grado di dati che passano tooyour dashboard OMS.
