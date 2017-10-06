---
title: aaaMonitor un Kubernetes Azure cluster con CoScale | Documenti Microsoft
description: Monitorare un cluster Kubernetes nel servizio contenitore di Azure tramite CoScale
services: container-service
documentationcenter: 
author: fryckbos
manager: 
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/22/2017
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: f835e82d2be3afe1d85070bd0bf69649cc6dd2ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-kubernetes-cluster-with-coscale"></a>Monitorare un cluster Kubernetes del servizio contenitore di Azure con CoScale

In questo articolo verrà illustrato come hello toodeploy [CoScale](https://www.coscale.com/) toomonitor agente tutti i nodi e i contenitori il Kubernetes cluster nel servizio contenitore di Azure. Per questa configurazione, è necessario un account con CoScale. 


## <a name="about-coscale"></a>Informazioni su CoScale 

CoScale è una piattaforma di monitoraggio che raccoglie metriche ed eventi da tutti i contenitori in diverse piattaforme di orchestrazione. CoScale offre il monitoraggio dello stack completo per gli ambienti Kubernetes. Fornisce visualizzazioni e analitica per tutti i livelli dello stack hello: hello OS, Kubernetes, Docker e applicazioni eseguiti all'interno di ai contenitori. CoScale offre diversi dashboard di monitoraggio predefinite e ha operatori tooallow rilevamento di anomalie predefiniti e problemi di infrastruttura e applicazione toofind sviluppatori veloci.

![Interfaccia utente di CoScale](./media/container-service-kubernetes-coscale/coscale.png)

Come illustrato in questo articolo, è possibile installare gli agenti in un toorun cluster Kubernetes CoScale come una soluzione SaaS. Se si desidera tookeep i dati localmente, CoScale è anche disponibile per l'installazione locale.


## <a name="prerequisites"></a>Prerequisiti

È innanzitutto necessario troppo[creare un account CoScale](https://www.coscale.com/free-trial).

Si presume che questa procedura dettagliata abbia [creato un cluster Kubernetes mediante il servizio contenitore di Azure](container-service-kubernetes-walkthrough.md).

Inoltre, presuppone di aver hello `az` CLI di Azure e `kubectl` installati gli strumenti.

È possibile verificare se si dispone di hello `az` strumento installato eseguendo:

```azurecli
az --version
```

Se non si dispone di hello `az` strumento installato, non esistono istruzioni [qui](/cli/azure/install-azure-cli).

È possibile verificare se si dispone di hello `kubectl` strumento installato eseguendo:

```bash
kubectl version
```

Se `kubectl` non è installato, è possibile eseguire:

```azurecli
az acs kubernetes install-cli
```

## <a name="installing-hello-coscale-agent-with-a-daemonset"></a>L'installazione dell'agente CoScale hello con un DaemonSet
[DaemonSets](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/) sono utilizzato da Kubernetes toorun una singola istanza di un contenitore in ogni host in cluster hello.
Sono ideali per l'esecuzione di agenti di monitoraggio, ad esempio agente CoScale hello.

Dopo l'accesso tooCoScale, visitare toohello [pagina agente](https://app.coscale.com/) agenti CoScale tooinstall nel cluster utilizzando un DaemonSet. Hello dell'interfaccia utente CoScale fornisce toocreate passaggi di configurazione guidata un agente e avvia il monitoraggio dei cluster Kubernetes completo.

![Configurazione dell'agente CoScale](./media/container-service-kubernetes-coscale/installation.png)

agente di hello toostart nel cluster hello, eseguire il comando hello fornito:

![Avviare l'agente CoScale hello](./media/container-service-kubernetes-coscale/agent_script.png)

L'operazione è terminata. Una volta agenti hello siano in esecuzione, verranno visualizzati i dati nella console di hello in pochi minuti. Visitare hello [pagina agente](https://app.coscale.com/) toosee un riepilogo del cluster, eseguire ulteriori passaggi di configurazione e visualizzare i dashboard, ad esempio hello **Kubernetes cluster Panoramica**.

![Panoramica del cluster Kubernetes](./media/container-service-kubernetes-coscale/dashboard_clusteroverview.png)

agente CoScale Hello viene distribuito automaticamente in nuovi computer nel cluster hello. Aggiornamenti agente Hello automaticamente quando viene rilasciata una nuova versione.


## <a name="next-steps"></a>Passaggi successivi

Vedere hello [CoScale documentazione](http://docs.coscale.com/) e [blog](https://www.coscale.com/blog) per ulteriori informazioni sulle soluzioni di monitoraggio CoScale. 

