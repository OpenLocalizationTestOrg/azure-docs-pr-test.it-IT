---
title: Creare cluster di Azure Service Fabric su Windows Server e Linux | Documentazione Microsoft
description: I cluster di Service Fabric vengono eseguiti in Windows Server e Linux, per poter distribuire e ospitare le applicazioni di Service Fabric in qualsiasi ambiente che esegue Windows Server o Linux.
services: service-fabric
documentationcenter: .net
author: Chackdan
manager: timlt
editor: 
ms.assetid: 19ca51e8-69b9-4952-b4b5-4bf04cded217
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 09/19/2017
ms.author: chackdan
ms.openlocfilehash: e3cfad19e42af24edd68befd7b1eac8cef41a1d6
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/11/2017
---
# <a name="create-service-fabric-clusters-on-windows-server-or-linux"></a>Creare cluster di Service Fabric in Windows Server o Linux
Un cluster di Azure Service Fabric è un set connesso in rete di macchine virtuali e computer fisici in cui vengono distribuiti e gestiti i microservizi. Un computer o una VM che fa parte di un cluster è chiamato nodo del cluster. I cluster possono essere ridimensionati fino a migliaia di nodi. Se si aggiungono nuovi nodi al cluster, Service Fabric ribilancia le repliche e le istanze di partizione del servizio nel numero incrementato di nodi. Le prestazioni complessive dell'applicazione migliorano e la contesa per l'accesso alla memoria si riduce. Se i nodi del cluster non vengono usati in modo efficiente, è possibile ridurre il numero di nodi del cluster. Service Fabric ribilancia di nuovo le repliche e le istanze di partizione nel numero ridotto di nodi per usare al meglio l'hardware in ogni nodo.

Service Fabric permette di creare cluster di Service Fabric in qualsiasi VM o computer con Windows Server o Linux in esecuzione. È quindi possibile distribuire ed eseguire applicazioni di Service Fabric in qualsiasi ambiente in cui è presente un set di computer Windows Server o Linux interconnessi, in locale, in Microsoft Azure o con qualsiasi provider di cloud.

## <a name="create-service-fabric-clusters-on-azure"></a>Creare cluster di Service Fabric in Azure
La creazione di un cluster in Azure viene eseguita tramite un modello di Resource Manager o il [portale di Azure](https://portal.azure.com). Per altre informazioni, vedere [Creare un cluster di Service Fabric cluster usando un modello di Resource Manager](service-fabric-cluster-creation-via-arm.md) o [Creare un cluster di Service Fabric dal portale di Azure](service-fabric-cluster-creation-via-portal.md).

## <a name="supported-operating-systems-for-clusters-on-azure"></a>Sistemi operativi supportati per i cluster in Azure
È possibile creare cluster in macchine virtuali che eseguono questi sistemi operativi:

* Windows Server 2012 R2
* Windows Server 2016 
* Linux Ubuntu 16.04  

## <a name="create-service-fabric-standalone-clusters-on-premises-or-with-any-cloud-provider"></a>Creare cluster autonomi di Service Fabric in locale o con qualsiasi provider di cloud
Service Fabric offre un pacchetto di installazione per creare cluster autonomi di Service Fabric in locale o con qualsiasi provider di cloud.

Per altre informazioni sulla configurazione di cluster autonomi di Service Fabric in Windows Server, vedere [Creazione di cluster di Service Fabric per Windows Server](service-fabric-cluster-creation-for-windows-server.md)

  > [!NOTE]
  > I cluster autonomi non sono attualmente supportati in Linux. Linux è supportato su cluster con un solo computer per lo sviluppo e più computer Linux di Azure.
  >

### <a name="any-cloud-deployments-vs-on-premises-deployments"></a>Confronto tra distribuzioni cloud e distribuzioni locali
Il processo di creazione di un cluster di Service Fabric locale è simile al processo di creazione di un cluster in qualsiasi ambiente cloud con un set di macchine virtuali. I passaggi iniziali per effettuare il provisioning delle macchine virtuali saranno controllati dal provider cloud o dall'ambiente locale corrente. Dopo aver ottenuto un set di macchine virtuali con connettività di rete abilitata, i passaggi successivi per configurare il pacchetto di Service Fabric, modificare le impostazioni del cluster ed eseguire gli script di creazione e gestione del cluster risulteranno identici. In questo modo, l'esperienza e le conoscenze relative all'uso e alla gestione dei cluster di Service Fabric potranno essere usate anche quando si scelgono nuovi ambienti host.

### <a name="benefits-of-creating-standalone-service-fabric-clusters"></a>Vantaggi della creazione di cluster autonomi di Service Fabric
* Per l'hosting di un cluster è possibile scegliere qualsiasi provider di cloud.
* Dopo essere state scritte, le applicazioni di Service Fabric possono essere eseguite in più ambienti di hosting senza alcuna modifica o con cambiamenti minimi.
* Le conoscenze acquisite nella creazione di applicazioni di Service Fabric saranno utili anche per altri ambienti di hosting.
* L'esperienza operativa derivata dall'esecuzione e dalla gestione di cluster di Service Fabric sarà utile anche per altri ambienti.
* Ampia copertura di clienti non limitata da vincoli dell'ambiente di hosting.
* Un livello aggiuntivo di affidabilità e protezione contro interruzioni generalizzate per consentire lo spostamento dei servizi in un altro ambiente di distribuzione in caso di blackout di un centro dati o del provider di servizi cloud.

## <a name="supported-operating-systems-for-standalone-clusters"></a>Sistemi operativi supportati per i cluster autonomi
È possibile creare cluster in macchine virtuali o in computer che eseguono questi sistemi operativi (Linux non è ancora supportato):

* Windows Server 2012 R2
* Windows Server 2016 

## <a name="advantages-of-service-fabric-clusters-on-azure-over-standalone-service-fabric-clusters-created-on-premises"></a>Vantaggi dei cluster di Service Fabric in Azure rispetto ai cluster autonomi di Service Fabric creati in locale
L'esecuzione di cluster di Service Fabric in Azure offre alcuni vantaggi rispetto all'opzione locale. Se non sono presenti esigenze specifiche in merito all'ambiente di esecuzione dei cluster, quindi, è preferibile eseguirli in Azure. Per semplificare e rendere più affidabili le operazioni e la gestione del cluster, in Azure viene offerta l'integrazione con altre funzionalità e servizi di Azure.

* **Portale di Azure:** il portale di Azure semplifica la creazione e la gestione dei cluster.
* **Gestione risorse di Azure:** l'uso di Gestione risorse di Azure consente di gestire facilmente tutte le risorse usate dal cluster come singola unità e semplifica il tracciamento dei costi e la fatturazione.
* **Cluster di Service Fabric come risorsa di Azure:** un cluster di Service Fabric è una risorsa di Azure, quindi è possibile modellarla in modo analogo alle altre risorse in Azure.
* **Integrazione con l'infrastruttura di Azure** Service Fabric si coordina con l'infrastruttura di Azure per il sistema operativo, la rete e altri aggiornamenti, in modo da migliorare la disponibilità e l'affidabilità delle applicazioni.  
* **Diagnostica:** in Azure viene offerta l'integrazione con Diagnostica di Azure e Log Analytics.
* **Ridimensionamento automatico:** per i cluster in Azure è disponibile la funzionalità predefinita di ridimensionamento automatico, grazie a set di ridimensionamento delle macchine virtuali. In locale e in altri ambienti cloud è necessario sviluppare una funzionalità di ridimensionamento automatico specifica oppure ridimensionare manualmente usando le API esposte da Service Fabric per il ridimensionamento dei cluster.

## <a name="next-steps"></a>Passaggi successivi

* Creare un cluster nelle VM o nei computer che eseguono Windows Server: [Creazione di cluster di Service Fabric per Windows Server](service-fabric-cluster-creation-for-windows-server.md)
* Creare un cluster nelle VM o nei computer che eseguono Linux: [Creare un cluster Linux](service-fabric-cluster-creation-via-portal.md)
* Informazioni sulle [opzioni di supporto di Service Fabric](service-fabric-support.md)

