---
title: scenari di ripristino aaaDisaster per le macchine virtuali di Azure | Documenti Microsoft
description: Informazioni su quali toodo nell'evento hello che un'interruzione del servizio Azure influisce sulle macchine virtuali di Azure.
services: virtual-machines
documentationcenter: 
author: kmouss
manager: timlt
editor: 
ms.assetid: 65272148-ff06-4bce-91f1-851d706d4d40
ms.service: virtual-machines
ms.workload: virtual-machines
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: kmouss;aglick
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 839c6f9c51a7f35b48ef3636bc346eef332bb06d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="what-toodo-in-hello-event-that-an-azure-service-disruption-impacts-azure-vms"></a>Quali toodo nell'evento hello che un'interruzione del servizio Azure influisce sulle macchine virtuali di Azure
Microsoft, collaboriamo toomake disco che i servizi siano sempre disponibili tooyou quando necessario. Eventi imprevisti possono, tuttavia, causare interruzioni non pianificate dei servizi.

La connettività e la disponibilità dei servizi Microsoft sono garantite da un contratto di servizio. Hello contratto di servizio per i singoli servizi di Azure è reperibile in [contratti di servizio di Azure](https://azure.microsoft.com/support/legal/sla/).

Azure offre già diverse funzionalità della piattaforma predefinite che supportano applicazioni a disponibilità elevata. Per altre informazioni su questi servizi, vedere [Ripristino di emergenza e disponibilità elevata per le applicazioni basate su Microsoft Azure](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md).

Questo articolo descrive uno scenario di ripristino di emergenza true, quando un'intera area di cui si verifichi un'interruzione a causa di calamità naturale toomajor o interruzione del servizio di diffusione. Si tratta di occorrenze rare, ma è necessario preparare il possibilità hello che sia presente un'interruzione di un'intera area. Se un'intera regione di cui si verifichi un'interruzione del servizio, le copie con ridondanza locale hello dei dati sarebbe temporaneamente non disponibile. Se è stata abilitata la replica geografica, esistono altre tre copie dei BLOB e delle tabelle di Archiviazione di Azure memorizzate in un'area diversa. In caso di hello di una completa interruzione dell'alimentazione locale o di emergenza in cui hello area primaria non è recuperabile, Azure esegue nuovamente il mapping tutti Region hello DNS voci toohello replica geografica.

toohelp gestire queste occorrenze rare, forniamo hello seguenti linee guida per macchine virtuali di Azure nel caso di hello di un'interruzione del servizio di hello all'intera area in cui viene distribuita la macchina virtuale di Azure.

## <a name="option-1-initiate-a-failover-by-using-azure-site-recovery"></a>Opzione 1: avviare un failover con Azure Site Recovery
È possibile configurare Azure Site Recovery per le macchine virtuali in modo che sia possibile recuperare l'applicazione con un solo clic in pochi minuti. È possibile replicare tooAzure regione di propria scelta e aree toopaired senza restrizioni. Iniziare eseguendo [la replica delle macchine virtuali](https://aka.ms/a2a-getting-started). È possibile [creare un piano di ripristino](../site-recovery/site-recovery-create-recovery-plans.md) in modo che è possibile automatizzare hello intero processo di failover per l'applicazione. È possibile [il failover di test](../site-recovery/site-recovery-test-failover-to-azure.md) in anticipo senza conseguenze per la replica in corso di produzione dell'applicazione o hello. In caso di hello di un'interruzione di area primaria, appena [avviare un failover](../site-recovery/site-recovery-failover.md) e attivare l'applicazione nell'area di destinazione.


## <a name="option-2-wait-for-recovery"></a>Opzione 2: attendere il ripristino
In tal caso, non è necessaria alcuna azione da parte dell'utente. Sapere che stiamo lavorando attentamente toorestore disponibilità del servizio. È possibile visualizzare lo stato del servizio corrente hello nel nostro [Dashboard di integrità del servizio di Azure](https://azure.microsoft.com/status/).

Questo è migliore hello se non è di Azure Site Recovery, l'archiviazione con ridondanza geografica e accesso in lettura o interruzioni di archiviazione con ridondanza geografica toohello precedente. Se è stato configurato l'archiviazione con ridondanza geografica o l'archiviazione con ridondanza geografica e accesso in lettura per account di archiviazione hello in cui sono archiviati i dischi rigidi virtuali (VHD) la macchina virtuale, è possibile esaminare toorecover hello immagine di base del disco rigido virtuale e provare tooprovision una nuova macchina virtuale da esso. Questa non è un'opzione consigliata perché non offre alcuna garanzia di sincronizzazione dei dati. Di conseguenza, questa opzione non è garantita toowork.


> [!NOTE]
> Tenere presente che non è possibile controllare questo processo e che verrà eseguito solo in caso di interruzioni del servizio a livello di area. Per questo motivo, è necessario affidarsi anche altre strategie di backup specifiche dell'applicazione tooachieve hello massimo livello di disponibilità. Per ulteriori informazioni, vedere la sezione hello in [strategie dei dati per il ripristino di emergenza](https://docs.microsoft.com/azure/architecture/resiliency/disaster-recovery-azure-applications#data-strategies-for-disaster-recovery).
>
>

## <a name="next-steps"></a>Passaggi successivi

- Avviare [la protezione delle applicazioni in esecuzione sulle macchine virtuali di Azure](https://aka.ms/a2a-getting-started) usando Azure Site Recovery

- ulteriori informazioni sulla modalità tooimplement un ripristino di emergenza e la strategia di disponibilità elevata, vedere toolearn [il ripristino di emergenza e disponibilità elevata per applicazioni Azure](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md).

- toodevelop una conoscenza tecnica dettagliata delle funzionalità della piattaforma cloud, vedere [informazioni tecniche sulla resilienza Azure](../resiliency/resiliency-technical-guidance.md).


- Se le istruzioni di hello non crittografate o se si desidera che le operazioni di hello toodo Microsoft per conto dell'utente, contattare [il supporto tecnico](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade).
