---
title: cluster di Azure Kubernetes aaaMonitor - Sysdig | Documenti Microsoft
description: Monitoraggio di cluster Kubernetes nel servizio contenitore di Azure con Sysdig
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
ms.openlocfilehash: a27813d01ee4624b9e993f6185169ad73aeec3a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-kubernetes-cluster-using-sysdig"></a>Monitorare un cluster Kubernetes del servizio contenitore di Azure con Sysdig

## <a name="prerequisites"></a>Prerequisiti
Si presume che questa procedura dettagliata abbia [creato un cluster Kubernetes mediante il servizio contenitore di Azure](container-service-kubernetes-walkthrough.md).

Inoltre, si presuppone di aver hello azure cli e kubectl installati gli strumenti.

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

## <a name="sysdig"></a>Sysdig
Sysdig è una società che offre uno strumento di monitoraggio esterno come servizio, che consente di monitorare i contenuti nel cluster Kubernetes in esecuzione in Azure. L'uso di Sysdig richiede un account Sysdig attivo.
È possibile iscriversi per creare un account nel rispettivo [sito](https://app.sysdigcloud.com).

Dopo aver eseguito il nel sito Web di toohello Sysdig cloud, fare clic sul nome utente e nella pagina di hello si dovrebbe visualizzare la "chiave di accesso". 

![Chiave API di Sysdig](./media/container-service-kubernetes-sysdig/sysdig2.png)

## <a name="installing-hello-sysdig-agents-tookubernetes"></a>L'installazione di hello Sysdig agenti tooKubernetes
i contenitori, Sysdig viene eseguito un processo in ogni computer utilizzando un Kubernetes toomonitor `DaemonSet`.
Gli oggetti DaemonSet sono oggetti API di Kubernetes che eseguono una singola istanza del contenitore per ogni macchina virtuale.
Sono ideali per l'installazione di strumenti quali l'agente di monitoraggio del Sysdig hello.

tooinstall hello Sysdig daemonset, è necessario innanzitutto scaricare [modello hello](https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml) da sysdig. Salvare il file come `sysdig-daemonset.yaml`.

In Linux e OS X è possibile eseguire:

```console
$ curl -O https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml
```

In PowerShell:

```console
$ Invoke-WebRequest -Uri https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml | Select-Object -ExpandProperty Content > sysdig-daemonset.yaml
```

Modificare quindi tooinsert tale file la chiave di accesso, che è stato ottenuto da account Sysdig.

Creare infine hello DaemonSet:

```console
$ kubectl create -f sysdig-daemonset.yaml
```

## <a name="view-your-monitoring"></a>Visualizzare il monitoraggio
Una volta installato e in esecuzione, gli agenti di hello devono pump tooSysdig indietro di dati.  Tornare indietro toothe [sysdig dashboard](https://app.sysdigcloud.com) dovrebbe essere possibile visualizzare informazioni ai contenitori.

È anche possibile installare dashboard specifici di Kubernetes tramite la [creazione guidata di un nuovo dashboard](https://app.sysdigcloud.com/#/dashboards/new).
