---
title: aaaAzure gruppi contenitore di istanze di contenitori
description: Informazioni sul funzionamento di gruppi di contenitori in Istanze di contenitore di Azure
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 2b0e784609979045c8f77d7b6d0987ec3fee714c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="container-groups-in-azure-container-instances"></a>Gruppi di contenitori in Istanze di contenitore di Azure

risorsa di primo livello Hello in istanze di contenitori di Azure è un gruppo contenitore. Questo articolo descrive le caratteristiche dei gruppi di contenitori e i tipi di scenari possibili.

## <a name="how-a-container-group-works"></a>Come funziona un gruppo di contenitori

Un gruppo contenitore è una raccolta di contenitori che ottengano pianificati su hello stesso ospitare macchina e condividere un ciclo di vita, rete locale e i volumi di archiviazione. È simile toohello concetto di un *pod* in [Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod/) e [DC/OS](https://dcos.io/docs/1.9/deploying-services/pods/).

Hello diagramma seguente viene illustrato un esempio di un gruppo contenitore che include più contenitori.

![Esempio di un gruppo di contenitori][container-groups-example]

Si noti che:

- gruppo Hello viene pianificata su un computer singolo host.
- gruppo Hello espone un singolo indirizzo IP pubblico, con una porta esposto.
- gruppo Hello è costituito da due contenitori. Un contenitore è in ascolto sulla porta 80, mentre altri hello in ascolto sulla porta 5000.
- gruppo Hello include due condivisioni di file di Azure come volume mount e ogni contenitore Monta una delle condivisioni hello in locale.

### <a name="networking"></a>Rete

I gruppi di contenitori condividono un indirizzo IP e uno spazio dei nomi di porta su tale indirizzo IP. tooenable client esterni tooreach un contenitore all'interno di gruppo hello, è necessario esporre la porta hello sull'indirizzo IP hello e dal contenitore hello. Poiché i contenitori all'interno di gruppo hello condividono uno spazio dei nomi di porta, il mapping della porta non è supportato. Contenitori all'interno di un gruppo possono raggiungere tra loro tramite localhost sul hello le porte che è stata esposta, anche se queste porte non sono esposte esternamente sull'indirizzo IP del gruppo di hello.

### <a name="storage"></a>Archiviazione

È possibile specificare toomount volumi esterni all'interno di un gruppo contenitore. È possibile eseguire il mapping di tali volumi in percorsi specifici all'interno di contenitori di singoli hello in un gruppo.

## <a name="common-scenarios"></a>Scenari comuni

Contenitori a più gruppi sono utili nei casi in cui si desidera toodivide di una singola attività funzionale in un numero ridotto di immagini contenitore, che possono essere recapitati da team diversi e hanno requisiti di risorse separato. Un esempio di utilizzo può includere gli elementi seguenti:

- Un contenitore di applicazione e un contenitore di registrazione. contenitore di registrazione Hello raccoglie i log di hello e output metriche da principale dell'applicazione hello e li scrive archiviazione toolong termine.
- Un contenitore di applicazione e uno di monitoraggio. monitoraggio contenitore periodicamente Hello rende un tooensure applicazione toohello richiesta che è in esecuzione e risponde correttamente e genera un avviso in caso contrario.
- Un contenitore per un'applicazione web e un contenitore di estrarre contenuto più recente di hello dal controllo del codice sorgente.

## <a name="next-steps"></a>Passaggi successivi

Informazioni su come troppo[distribuire un gruppo multi-contenitore](container-instances-multi-container-group.md) con un modello di gestione risorse di Azure.

<!-- IMAGES -->

[container-groups-example]: ./media/container-instances-container-groups/container-groups-example.png