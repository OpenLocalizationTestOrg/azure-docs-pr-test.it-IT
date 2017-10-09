---
title: aaaCreate Azure Service Fabric cluster in Windows Server e Linux | Documenti Microsoft
description: "I cluster di Service Fabric eseguiti nel Server di Windows e Linux, ovvero si sarà in grado di applicazioni di Service Fabric toodeploy e l'host remoto via Internet, è possibile eseguire Windows Server o Linux."
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
ms.date: 03/08/2017
ms.author: chackdan
ms.openlocfilehash: 46d5f3d019339c57a0024f5a9d47d9018cca01a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-service-fabric-clusters-on-windows-server-or-linux"></a>Creare cluster di Service Fabric in Windows Server o Linux
Un cluster di Azure Service Fabric è un set connesso in rete di macchine virtuali e computer fisici in cui vengono distribuiti e gestiti i microservizi. Un computer o una VM che fa parte di un cluster è chiamato nodo del cluster. I cluster possono essere ridimensionati toothousands dei nodi. Se si aggiunge di nuovo cluster di nodi toohello, Service Fabric eseguito il ribilanciamento delle istanze e le repliche delle partizioni servizio hello hello aumentato in nodi. Generale consente di migliorare le prestazioni dell'applicazione e riduce la contesa tra toomemory di accesso. Se non vengono utilizzati i nodi nel cluster hello hello in modo efficiente, è possibile ridurre il numero di hello di nodi nel cluster hello. Service Fabric eseguito nuovamente il ribilanciamento delle repliche di partizione hello e istanze in numero hello ridotto di nodi toomake meglio di hardware hello in ogni nodo.

Consente di Service Fabric per la creazione di hello di cluster di Service Fabric su eventuali macchine virtuali o computer che eseguono Windows Server o Linux. In altri termini in grado di toodeploy, eseguire le applicazioni di Service Fabric in qualsiasi ambiente in cui si dispone di un set di computer Windows Server o Linux che sono collegate tra loro, ovvero in locale, Microsoft Azure o con qualsiasi provider di cloud.

## <a name="create-service-fabric-clusters-on-azure"></a>Creare cluster di Service Fabric in Azure
Creazione di un cluster in Azure viene eseguita tramite un modello di risorsa o hello portale di Azure. Lettura [creare un cluster di Service Fabric utilizzando un modello di gestione risorse](service-fabric-cluster-creation-via-arm.md) o [creare un cluster di Service Fabric dal portale di Azure hello](service-fabric-cluster-creation-via-portal.md) per ulteriori informazioni.

## <a name="supported-operating-systems-for-clusters-on-azure"></a>Sistemi operativi supportati per i cluster in Azure
Si è in grado di toocreate cluster nelle macchine virtuali che eseguono tali sistemi operativi:

* Windows Server 2012 R2
* Windows Server 2016 
* Linux Ubuntu 16.04 (in anteprima pubblica) 

## <a name="create-service-fabric-standalone-clusters-on-premises-or-with-any-cloud-provider"></a>Creare cluster autonomi di Service Fabric in locale o con qualsiasi provider di cloud
Service Fabric fornisce un pacchetto di installazione per si toocreate autonoma dell'infrastruttura del servizio cluster locale o su qualsiasi provider di cloud

Per altre informazioni sulla configurazione di cluster autonomi di Service Fabric in Windows Server, vedere [Creazione di cluster di Service Fabric per Windows Server](service-fabric-cluster-creation-for-windows-server.md)

### <a name="any-cloud-deployments-vs-on-premises-deployments"></a>Confronto tra distribuzioni cloud e distribuzioni locali
il processo di Hello per la creazione di un cluster di Service Fabric locale è simile toohello processo di creazione di un cluster in qualsiasi cloud di propria scelta, con un set di macchine virtuali. Hello passaggi iniziali tooprovision hello macchine virtuali vengono gestite dal provider di cloud hello o nell'ambiente locale in uso. Dopo avere un set di macchine virtuali con connettività di rete abilitata tra di essi, quindi hello passaggi tooset pacchetto di Service Fabric hello, modificare le impostazioni del cluster hello ed eseguire la creazione di cluster hello e script di gestione sono identici. Ciò garantisce che la conoscenza e l'esperienza di gestione e la gestione dei cluster di Service Fabric è trasferibile quando si sceglie tootarget nuovi ambienti di hosting.

### <a name="benefits-of-creating-standalone-service-fabric-clusters"></a>Vantaggi della creazione di cluster autonomi di Service Fabric
* Si è gratuita toochoose qualsiasi cloud toohost provider del cluster.
* Applicazioni di Service Fabric, una volta scritte, è possibile eseguire in più ambienti di hosting con modifiche minime toono.
* Conoscenza della compilazione di applicazioni di Service Fabric esegue da un tooanother ambiente host.
* Esperienza di esecuzione e la gestione dell'infrastruttura del servizio cluster esegue su da un ambiente tooanother.
* Ampia copertura di clienti non limitata da vincoli dell'ambiente di hosting.
* Un ulteriore livello di affidabilità e protezione da interruzioni generalizzate esiste perché è possibile spostare i servizi di hello sull'ambiente di distribuzione tooanother se un data center o provider di cloud di blackout.

## <a name="supported-operating-systems-for-standalone-clusters"></a>Sistemi operativi supportati per i cluster autonomi
Si è in grado di toocreate cluster su macchine virtuali o computer che eseguono questi sistemi operativi:

* Windows Server 2012 R2
* Windows Server 2016 
* Linux (presto disponibile)

## <a name="advantages-of-service-fabric-clusters-on-azure-over-standalone-service-fabric-clusters-created-on-premises"></a>Vantaggi dei cluster di Service Fabric in Azure rispetto ai cluster autonomi di Service Fabric creati in locale
I cluster di Service Fabric in esecuzione in Azure offre vantaggi rispetto all'opzione hello locale, pertanto se non si dispone di esigenze specifiche per cui è in esecuzione i cluster, quindi è consigliabile eseguirli in Azure. In Azure, si forniscono l'integrazione con altri servizi, che rende le operazioni e gestione di cluster hello e rende più affidabile e la funzionalità di Azure.

* **Portale di Azure:** portale di Azure rende facile toocreate e gestire i cluster.
* **Gestione risorse di Azure:** utilizzo di gestione risorse di Azure consente una gestione semplificata di tutte le risorse usate dal cluster hello come un'unità e semplifica il rilevamento di costo e la fatturazione.
* **Cluster di Service Fabric come risorsa di Azure:** un cluster di Service Fabric è una risorsa di Azure Resource Manager, quindi è possibile modellarla in modo analogo alle altre risorse di Azure Resource Manager in Azure.
* **Integrazione con l'infrastruttura di Azure** Service Fabric interagisce con hello sottostante l'infrastruttura di Azure per sistema operativo, rete e altri aggiornamenti tooimprove disponibilità e affidabilità delle applicazioni.  
* **Diagnostica:** in Azure viene offerta l'integrazione con Diagnostica di Azure e Log Analytics.
* **La scalabilità automatica:** per i cluster in Azure, si forniscono funzionalità di scalabilità automatica incorporata scadenza set di scalabilità di tooVirtual macchina. In altri ambienti di cloud e locali, è possibile toobuild la propria funzionalità o un scala manualmente utilizzando le API che espone Service Fabric hello per la scalabilità dei cluster scalabilità automatica.

## <a name="next-steps"></a>Passaggi successivi

* Creare un cluster nelle VM o nei computer che eseguono Windows Server: [Creazione di cluster di Service Fabric per Windows Server](service-fabric-cluster-creation-for-windows-server.md)
* Creare un cluster nelle VM o nei computer che eseguono Linux: [Service Fabric su Linux](service-fabric-linux-overview.md)
* Informazioni sulle [opzioni di supporto di Service Fabric](service-fabric-support.md)

