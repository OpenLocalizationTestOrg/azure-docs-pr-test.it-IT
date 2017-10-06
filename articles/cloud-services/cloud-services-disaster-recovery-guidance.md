---
title: toodo aaaWhat nell'evento hello di un'interruzione del servizio Azure che influisce su servizi Cloud di Azure | Documenti Microsoft
description: Informazioni su quali toodo nell'evento hello di un'interruzione del servizio Azure che influisce su servizi Cloud di Azure.
services: cloud-services
documentationcenter: 
author: mmccrory
manager: timlt
editor: 
ms.assetid: e52634ab-003d-4f1e-85fa-794f6cd12ce4
ms.service: cloud-services
ms.workload: cloud-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: mmccrory
ms.openlocfilehash: bb1f1835fc91a23772f81801b67d5786c190ba19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="what-toodo-in-hello-event-of-an-azure-service-disruption-that-impacts-azure-cloud-services"></a>Quali toodo nell'evento hello di un'interruzione del servizio Azure che influisce su servizi Cloud di Azure
Microsoft, collaboriamo toomake disco che i servizi siano sempre disponibili tooyou quando necessario. Eventi imprevisti possono, tuttavia, causare interruzioni non pianificate dei servizi.

La connettività e la disponibilità dei servizi Microsoft sono garantite da un contratto di servizio. Hello contratto di servizio per i singoli servizi di Azure è reperibile in [contratti di servizio di Azure](https://azure.microsoft.com/support/legal/sla/).

Azure offre già diverse funzionalità della piattaforma predefinite che supportano applicazioni a disponibilità elevata. Per altre informazioni su questi servizi, vedere [Ripristino di emergenza e disponibilità elevata per le applicazioni basate su Microsoft Azure](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md).

Questo articolo descrive uno scenario di ripristino di emergenza true, quando un'intera area di cui si verifichi un'interruzione a causa di calamità naturale toomajor o interruzione del servizio di diffusione. Si tratta di occorrenze rare, ma è necessario preparare il possibilità hello che sia presente un'interruzione di un'intera area. Se un'intera regione di cui si verifichi un'interruzione del servizio, le copie con ridondanza locale hello dei dati sarebbe temporaneamente non disponibile. Se è stata abilitata la replica geografica, esistono altre tre copie dei BLOB e delle tabelle di Archiviazione di Azure memorizzate in un'area diversa. In caso di hello di una completa interruzione dell'alimentazione locale o di emergenza in cui hello area primaria non è recuperabile, Azure esegue nuovamente il mapping tutti Region hello DNS voci toohello replica geografica.

> [!NOTE]
> Tenere presente che non è possibile controllare questo processo e che verrà eseguito solo in caso di interruzioni del servizio a livello di data center. Per questo motivo, è necessario affidarsi anche altre strategie di backup specifiche dell'applicazione tooachieve hello massimo livello di disponibilità. Per altre informazioni, vedere [Ripristino di emergenza e disponibilità elevata per le applicazioni basate su Microsoft Azure](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md). Se si desidera tooaffect in grado di toobe proprio failover, è possibile utilizzare hello tooconsider di [archiviazione con ridondanza geografica e accesso in lettura (RA-GRS)](../storage/common/storage-redundancy.md#read-access-geo-redundant-storage), che consente di creare una copia di sola lettura dei dati in un'altra area.
>
>


## <a name="option-1-use-a-backup-deployment-through-azure-traffic-manager"></a>Opzione 1: usare una distribuzione di backup tramite Gestione traffico di Azure
soluzione di ripristino di emergenza più affidabili Hello implica la gestione di più distribuzioni dell'applicazione in diverse aree, quindi l'uso di [Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md) toodirect il traffico tra esse. Gestione traffico di Azure fornisce più [i metodi di routing](../traffic-manager/traffic-manager-routing-methods.md), pertanto è possibile scegliere se toomanage le distribuzioni utilizzando un modello principale/backup o toosplit il traffico tra loro.

![Bilanciamento dei servizi cloud di Azure in diverse aree con Gestione traffico di Azure](./media/cloud-services-disaster-recovery-guidance/using-azure-traffic-manager.png)

Per hello più veloce risposta toohello perdita di una regione, è importante configurare Traffic Manager [monitoraggio degli endpoint](../traffic-manager/traffic-manager-monitoring.md).

## <a name="option-2-deploy-your-application-tooa-new-region"></a>Opzione 2: Distribuire la nuova area tooa di applicazione
La gestione di più distribuzioni attive, come descritto nella precedente opzione hello comporta costi aggiuntivi. Se l'obiettivo del tempo di ripristino (RTO) è sufficientemente flessibile e si dispone di codice originale hello o un pacchetto di servizi Cloud compilato, è possibile creare una nuova istanza dell'applicazione in un'altra area e aggiornare il DNS record toopoint toohello nuova distribuzione.

Per ulteriori informazioni su come toocreate e distribuire un'applicazione di servizio cloud, vedere [come toocreate e distribuire un servizio cloud](cloud-services-how-to-create-deploy-portal.md).

In base alle origini dati di applicazione, procedure di ripristino hello toocheck potrebbe essere necessario per l'origine dati dell'applicazione.

* Per le origini dati di archiviazione di Azure, vedere [replica di archiviazione Azure](../storage/common/storage-redundancy.md#read-access-geo-redundant-storage) toocheck su hello le opzioni disponibili in base a hello scelto il modello di replica per l'applicazione.
* Per le origini di Database SQL, leggere [Panoramica: Cloud di ripristino di emergenza di database e la continuità aziendale con il Database SQL](../sql-database/sql-database-business-continuity.md) toocheck sulle opzioni di hello sono disponibili in base a modello replica hello scelto per l'applicazione.


## <a name="option-3-wait-for-recovery"></a>Opzione 3: attendere il ripristino
In questo caso, è necessario alcun intervento da parte dell'utente, ma il servizio non sarà disponibile finché non viene ripristinato l'area di hello. È possibile visualizzare lo stato del servizio corrente hello in hello [Dashboard di integrità del servizio di Azure](https://azure.microsoft.com/status/).

## <a name="next-steps"></a>Passaggi successivi
ulteriori informazioni sulla modalità tooimplement un ripristino di emergenza e la strategia di disponibilità elevata, vedere toolearn [il ripristino di emergenza e disponibilità elevata per applicazioni Azure](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md).

toodevelop una conoscenza tecnica dettagliata delle funzionalità della piattaforma cloud, vedere [informazioni tecniche sulla resilienza Azure](../resiliency/resiliency-technical-guidance.md).
