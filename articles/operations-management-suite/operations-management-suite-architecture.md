---
title: aaaOperations architettura Management Suite (OMS) | Documenti Microsoft
description: "Microsoft Operations Management Suite (OMS) è la soluzione Microsoft per la gestione IT basata sul cloud che consente di gestire e proteggere l'infrastruttura locale e cloud.  In questo articolo identifica diversi servizi hello inclusi in OMS e vengono forniti i collegamenti tootheir dettagliate contenuto."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 40e41686-7e35-4d85-bbe8-edbcb295a534
ms.service: operations-management-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/11/2017
ms.author: bwren
ms.openlocfilehash: fa3227aa9c19219009ebe363b7fd2d6565cec59c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="oms-architecture"></a>Architettura di OMS
[Operations Management Suite (OMS)](https://azure.microsoft.com/documentation/services/operations-management-suite/) è una raccolta di servizi basati sul cloud per la gestione di ambienti locali e cloud.  Questo articolo descrive hello diversi in locale e i componenti di cloud di OMS e la relativa architettura di elaborazione del cloud di livello elevato.  È possibile consultare la documentazione di toohello per ogni servizio per altri dettagli.

## <a name="log-analytics"></a>Log Analytics
Tutti i dati raccolti da [Log Analitica](https://azure.microsoft.com/documentation/services/log-analytics/) viene archiviato nel repository OMS hello che è ospitato in Azure.  Origini connesse generano i dati raccolti nel repository OMS hello.  Sono attualmente supportati tre tipi di origini connesse.

* Un agente installato in un [Windows](../log-analytics/log-analytics-windows-agents.md) o [Linux](../log-analytics/log-analytics-linux-agents.md) computer connessi direttamente tooOMS.
* Un gruppo di gestione di System Center Operations Manager (SCOM) [connesso tooLog Analitica](../log-analytics/log-analytics-om-agents.md) .  Agenti SCOM continuano toocommunicate con server di gestione che inoltrano i dati di prestazioni tooLog Analitica ed eventi.
* Un [account di archiviazione di Azure](../log-analytics/log-analytics-azure-storage.md) che raccoglie i dati di [Diagnostica di Azure](../cloud-services/cloud-services-dotnet-diagnostics.md) da un ruolo di lavoro, da un ruolo Web o da una macchina virtuale di Azure.

Origini dati definiscono dati hello Analitica Log raccolti da origini connesse, inclusi i registri eventi e contatori delle prestazioni.  Soluzioni di aggiungere funzionalità tooOMS e possono essere facilmente aggiunte tooyour dell'area di lavoro da hello [OMS Solutions Gallery](../log-analytics/log-analytics-add-solutions.md).  Alcune soluzioni possono richiedere una connessione diretta tooLog Analitica, dagli agenti SCOM, mentre altri potrebbero richiedere toobe un agente aggiuntivo installato.

Log Analitica dispone di un portale basato sul web che è possibile utilizzare le risorse di OMS toomanage, aggiungere e configurare soluzioni OMS e visualizzare e analizzare i dati nel repository OMS hello.

![Architettura di alto livello di Log Analytics](media/operations-management-suite-architecture/log-analytics.png)

## <a name="azure-automation"></a>Automazione di Azure
[I runbook di automazione Azure](http://azure.microsoft.com/documentation/services/automation) vengono eseguiti nel cloud di Azure hello e possono accedere alle risorse che sono in Azure, in altri servizi cloud o accessibili dalla rete Internet pubblica hello.  È anche possibile designare computer locali nel data center locale tramite [ruoli di lavoro ibridi per runbook](../automation/automation-hybrid-runbook-worker.md) per consentire ai runbook di accedere alle risorse locali.

[Le configurazioni DSC](../automation/automation-dsc-overview.md) archiviati in automazione di Azure possono essere applicati direttamente tooAzure le macchine virtuali.  Altre macchine fisiche e virtuali possono richiedere configurazioni da server di pull DSC di automazione di Azure hello.

Automazione di Azure offre una soluzione OMS che Visualizza statistiche e collegamenti toolaunch hello portale di Azure per qualsiasi operazione.

![Architettura di alto livello di Automazione di Azure](media/operations-management-suite-architecture/automation.png)

## <a name="azure-backup"></a>Backup di Azure
I dati protetti in [Backup di Azure](http://azure.microsoft.com/documentation/services/backup) vengono archiviati in un insieme di credenziali di backup che si trova in una determinata area geografica.  Hello dati vengono replicati in hello stessa area geografica e, in base al tipo di hello dell'insieme di credenziali, possono essere replicati tooanother area per una maggiore ridondanza.

Backup di Azure prevede tre scenari fondamentali.

* Computer Windows con l'agente di Backup di Azure.  In questo modo è toobackup file e cartelle da qualsiasi client o server Windows direttamente tooyour insieme di credenziali di backup Azure.  
* System Center Data Protection Manager (DPM) o server di Backup di Microsoft Azure. In questo modo si tooleverage Data Protection Manager o Server di Backup di Microsoft Azure toobackup file e cartelle inoltre tooapplication i carichi di lavoro, ad esempio archiviazione toolocal SQL e SharePoint e quindi replicare tooyour insieme di credenziali di backup Azure.
* Estensioni delle macchine virtuali di Azure.  In questo modo toobackup tooyour di macchine virtuali di Azure dell'insieme di credenziali di Azure backup.

Backup di Azure offre una soluzione OMS che Visualizza statistiche e collegamenti toolaunch hello portale di Azure per qualsiasi operazione.

![Architettura di alto livello di Backup di Azure](media/operations-management-suite-architecture/backup.png)

## <a name="azure-site-recovery"></a>Azure Site Recovery
[Azure Site Recovery](http://azure.microsoft.com/documentation/services/site-recovery) coordina la replica, il failover e il failback di macchine virtuali e server fisici. Dati di replica vengono scambiati tra host Hyper-V, hypervisor VMware e server fisici in Data Center primari e secondari oppure tra Data Center hello e archiviazione di Azure.  Site Recovery archivia i metadati in insiemi di credenziali che si trovano in una determinata area geografica di Azure. Nessun dato replicato viene archiviato dal servizio Site Recovery hello.

Azure Site Recovery prevede tre scenari di replica fondamentali.

**Replica di macchine virtuali Hyper-V**

* Se le macchine virtuali Hyper-V vengono gestite nei cloud VMM, è possibile replicare l'archiviazione di dati secondari tooa center o tooAzure.  Replica tooAzure è su una connessione internet sicura.  Data Center secondario tooa di replica viene eseguita tramite hello LAN.
* Se le macchine virtuali Hyper-V non sono gestite da VMM, è possibile replicare tooAzure esclusivamente all'archiviazione.  Replica tooAzure è su una connessione internet sicura.

**Replica di macchine virtuali VMware**

* È possibile replicare VMware le macchine virtuali tooa Data Center secondario che esegue VMware o tooAzure di archiviazione.  Replica tooAzure può essere eseguita tramite una VPN site-to-site o ExpressRoute di Azure o una connessione Internet sicura. Data Center secondario tooa di replica viene eseguita tramite il canale dati di InMage Scout hello.

**Replica di server fisici Windows e Linux** 

* È possibile replicare i server fisici tooa Data Center o tooAzure archiviazione secondaria. Replica tooAzure può essere eseguita tramite una VPN site-to-site o ExpressRoute di Azure o una connessione Internet sicura. Data Center secondario tooa di replica viene eseguita tramite il canale dati di InMage Scout hello.  Azure Site Recovery dispone di una soluzione OMS che visualizza alcune statistiche, ma è necessario utilizzare hello portale di Azure per qualsiasi operazione.

![Architettura di alto livello di Azure Site Recovery](media/operations-management-suite-architecture/site-recovery.png)

## <a name="next-steps"></a>Passaggi successivi
* Informazioni su [Log Analytics](http://azure.microsoft.com/documentation/services/log-analytics)
* Informazioni su [Automazione di Azure](https://azure.microsoft.com/documentation/services/automation)
* Informazioni su [Backup di Azure](http://azure.microsoft.com/documentation/services/backup)
* Informazioni su [Azure Site Recovery](http://azure.microsoft.com/documentation/services/site-recovery)

