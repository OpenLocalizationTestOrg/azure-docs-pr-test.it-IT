---
title: aaaMonitor Kubernetes Azure cluster con Datadog | Documenti Microsoft
description: Monitoraggio di un cluster Kubernetes nel servizio contenitore di Azure con Datadog
services: container-service
documentationcenter: 
author: bburns
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/09/2016
ms.author: bburns
ms.custom: mvc
ms.openlocfilehash: bccd8b59a048e0f791172fcfc4eeba6370dafcc0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-datadog"></a>Monitorare un cluster del servizio contenitore di Azure con Datadog

## <a name="prerequisites"></a>Prerequisiti
Si presume che questa procedura dettagliata abbia [creato un cluster Kubernetes mediante il servizio contenitore di Azure](container-service-kubernetes-walkthrough.md).

Inoltre, presuppone di aver hello `az` cli di Azure e `kubectl` installati gli strumenti.

È possibile verificare se si dispone di hello `az` strumento installato eseguendo:

```console
$ az --version
```

Se non si dispone di hello `az` strumento installato, non esistono istruzioni [qui](https://github.com/azure/azure-cli#installation).

È possibile verificare se si dispone di hello `kubectl` strumento installato eseguendo:

```console
$ kubectl version
```

Se `kubectl` non è installato, è possibile eseguire:

```console
$ az acs kubernetes install-cli
```

## <a name="datadog"></a>DataDog
Datadog è un servizio che raccoglie dati di monitoraggio dai contenitori all'interno del cluster del servizio contenitore di Azure. Datadog è dotato di un dashboard di integrazione Docker in cui è possibile visualizzare metriche specifiche all'interno dei propri contenitori. Le metriche raccolte dai contenitori sono organizzate per CPU, memoria, rete e I/O. Datadog suddivide le metriche in contenitori e immagini.

È innanzitutto necessario troppo[creare un account](https://www.datadoghq.com/lpg/)

## <a name="installing-hello-datadog-agent-with-a-daemonset"></a>L'installazione di hello Datadog agente con un DaemonSet
DaemonSets vengono utilizzati da Kubernetes toorun una singola istanza di un contenitore in ogni host in cluster hello.
Sono ideali per l'esecuzione di agenti di monitoraggio.

Dopo aver eseguito l'accesso in Datadog, è possibile seguire hello [Datadog istruzioni](https://app.datadoghq.com/account/settings#agent/kubernetes) tooinstall Datadog agenti nel cluster utilizzando un DaemonSet.

## <a name="conclusion"></a>Conclusioni
L'operazione è terminata. Una volta agenti hello siano attivi e in esecuzione è verranno visualizzati i dati nella console di hello in pochi minuti. È possibile visitare hello integrato [kubernetes dashboard](https://app.datadoghq.com/screen/integration/kubernetes) toosee un riepilogo del cluster.
