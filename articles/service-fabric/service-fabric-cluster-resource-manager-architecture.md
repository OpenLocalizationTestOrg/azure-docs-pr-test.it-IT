---
title: Architettura di gestione aaaResource | Documenti Microsoft
description: An architectural overview of Service Fabric Cluster Resource Manager.
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 6c4421f9-834b-450c-939f-1cb4ff456b9b
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 9ea80273d0566a2ac25143ada3662875656b57b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="cluster-resource-manager-architecture-overview"></a>Panoramica dell'architettura di Cluster Resource Manager
Hello gestione delle risorse Cluster di Service Fabric è un servizio centrale in esecuzione in cluster hello. Gestisce lo stato desiderato di hello dei servizi di hello cluster hello, in particolare con riguardo tooresource consumo e tutte le regole di selezione host. 

toomanage risorse hello del cluster, è necessario disporre di varie informazioni hello servizio di gestione delle risorse Cluster dell'infrastruttura:

- I servizi esistenti attualmente
- Ogni uso della risorsa della corrente del servizio (o per impostazione predefinito) 
- capacità del cluster rimanenti Hello 
- capacità di Hello di nodi hello hello cluster 
- quantità di Hello di risorse utilizzate in ogni nodo

utilizzo delle risorse di un determinato servizio Hello può cambiare nel tempo e servizi in genere si preoccupa più di un tipo di risorsa. Potrebbero essere misurate risorse reali e fisiche tra diversi servizi. I servizi possono tracciare metriche fisiche come il consumo di memoria e del disco. Più comunemente, i servizi potrebbero occuparsi anche di metriche logiche, ad esempio "WorkQueueDepth" o "TotalRequests". Metriche logiche e fisiche possono essere usate in hello dello stesso cluster. Metriche possono essere condivisi tra molti servizi o essere tooa specifico particolare servizio.

## <a name="other-considerations"></a>Altre considerazioni
Hello proprietari e operatori di cluster hello possono essere diversi da hello gli autori di servizio e di applicazione o in un oggetto sono minimo hello stesso persone che ricoprono diversi. Quando si sviluppa l'applicazione si conoscono alcuni aspetti riguardanti cosa è necessario. Si dispone di una stima di hello devono essere distribuiti come i diversi servizi e le risorse che verrà utilizzata. Ad esempio, livello web hello deve toorun su nodi esposti toohello Internet, mentre i servizi di database hello non dovrebbero. Ad esempio, servizi web hello probabilmente sono limitati della CPU e la rete, durante l'attenzione di hello dati livello servizi ulteriori informazioni su consumo di memoria e disco. Tuttavia, persona hello gestisce un evento imprevisto in tempo reale a sito per il servizio nell'ambiente di produzione, o che gestisce un servizio di aggiornamento toohello ha toodo un processo diverso e richiede strumenti diversi. 

I servizi e i cluster hello sono dinamici:

- numero di Hello di nodi nel cluster hello può aumentare e ridursi
- Nodi di diversi tipi e dimensioni possono essere aggiunti o rimossi
- I servizi possono essere creati e rimossi e le allocazioni delle risorse desiderate e le regole di selezione possono essere modificate
- Gli aggiornamenti o altre operazioni di gestione possono essere distribuite tramite cluster hello in un'applicazione hello sui livelli di infrastruttura
- Gli errori possono verificarsi in qualsiasi momento.

## <a name="cluster-resource-manager-components-and-data-flow"></a>Componenti di Cluster Resource Manager e flusso dei dati
Hello gestione delle risorse Cluster ha requisiti di hello tootrack di ogni servizio e hello l'utilizzo delle risorse per ogni oggetto di servizio all'interno di tali servizi. Gestione delle risorse Cluster Hello composta da due parti concettuale: agenti eseguiti in ogni nodo e un servizio a tolleranza di errore. agenti Hello ogni carico di tenere traccia del nodo vengono segnalati dai servizi, aggregazione e li segnala periodicamente. servizio di gestione delle risorse Cluster Hello aggrega tutte le informazioni dagli agenti locale hello hello e reagisce in base alla relativa configurazione corrente.

Diamo un'occhiata hello seguente diagramma:

<center>
![Architettura di Resource Balancer][Image1]
</center>

Durante il runtime possono essere apportate numerose modifiche. Ad esempio, si supponga che la quantità hello di risorse di alcuni servizi utilizzano le modifiche, alcuni errori di servizi, e alcuni nodi partecipare o uscire dai cluster hello. Tutte le modifiche di hello in un nodo vengono aggregate e inviate periodicamente del servizio di gestione delle risorse Cluster toohello (1,2) in cui sono nuovamente aggregati, analizzati e archiviati. Ogni pochi secondi che servizio esamina modifiche hello e determina se sono necessarie tutte le azioni (3). Ad esempio, potrebbe notare che sono stati aggiunti alcuni nodi vuoti toohello cluster. Di conseguenza, decide toomove alcuni nodi toothose servizi. Hello gestione delle risorse Cluster potrebbe si noti inoltre che un determinato nodo è sovraccarico o che determinati servizi riusciti o eliminate, liberando risorse in un' posizione.

Si esaminerà hello seguente diagramma e vedere le operazioni successive. Si supponga che hello gestione delle risorse Cluster determina che sono necessarie modifiche. Interagisce con altri system services (in particolare hello gestione Failover) toomake hello le modifiche necessarie. I comandi necessari hello vengono quindi inviati toohello nodi appropriati (4). Si supponga, ad esempio, hello Gestione risorse notato che è stato sottoposto a overload Nodo5 e pertanto deciso toomove servizio B da tooNode4 Nodo5. Alla fine di hello di riconfigurazione hello (5), il cluster hello è simile al seguente:

<center>
![Architettura di Resource Balancer][Image2]
</center>

## <a name="next-steps"></a>Passaggi successivi
- Hello gestione delle risorse Cluster dispone di numerose opzioni per la descrizione del cluster di hello. toofind ulteriori informazioni, consultare questo articolo in [che descrive un cluster di Service Fabric](./service-fabric-cluster-resource-manager-cluster-description.md)
- compiti primario di gestione risorse del Cluster di Hello sono ribilanciamento cluster hello e imporre regole di selezione host. Per altre informazioni sulla configurazione di questi comportamenti, vedere [bilanciamento del cluster di Service Fabric](./service-fabric-cluster-resource-manager-balancing.md)

[Image1]:./media/service-fabric-cluster-resource-manager-architecture/Service-Fabric-Resource-Manager-Architecture-Activity-1.png
[Image2]:./media/service-fabric-cluster-resource-manager-architecture/Service-Fabric-Resource-Manager-Architecture-Activity-2.png
