---
title: "raccomandazioni di Advisor la disponibilità elevata aaaAzure | Documenti Microsoft"
description: "Usare Azure Advisor tooimprove la disponibilità elevata delle distribuzioni di Azure."
services: advisor
documentationcenter: NA
author: kumudd
manager: carmonm
editor: 
ms.assetid: 
ms.service: advisor
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/16/2016
ms.author: kumud
ms.openlocfilehash: 3ac75ce401271f0212d198d7a7dc75ab702b6eda
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="advisor-high-availability-recommendations"></a>Consigli di Advisor sulla disponibilità elevata

Preparazione di Azure consente di verificare e migliorare la continuità hello delle applicazioni business-critical. È possibile ottenere indicazioni relative a disponibilità elevata da Advisor dal hello **la disponibilità elevata** scheda dashboard Advisor hello.

![Pulsante disponibilità elevata nel dashboard di Advisor hello](./media/advisor-high-availability-recommendations/advisor-high-availability-tab.png)


## <a name="ensure-virtual-machine-fault-tolerance"></a>Garantire la tolleranza di errore delle macchine virtuali

Advisor identifica le macchine virtuali che non fanno parte di un set di disponibilità e consiglia di trasferirle in un set di disponibilità. Per fornire ridondanza tooyour applicazione, si consiglia di raggruppare due o più macchine virtuali in un set di disponibilità. Questa configurazione assicura che durante un evento di manutenzione pianificato o non pianificato, almeno una macchina virtuale sia disponibile e soddisfa hello macchina virtuale di Azure contratto di servizio. È possibile scegliere entrambi toocreate un set di disponibilità per hello macchina virtuale o tooadd hello macchina virtuale tooan set di disponibilità esistente.

> [!NOTE]
> Se si sceglie toocreate una disponibilità impostato, è necessario aggiungere almeno una macchina virtuale più al suo interno. Si consiglia di raggruppare due o più macchine virtuali in un disponibilità impostare tooensure durante un'interruzione del servizio è disponibile almeno un computer.

![Consiglio di Advisor: per la ridondanza delle macchine virtuali usare i set di disponibilità](./media/advisor-high-availability-recommendations/advisor-high-availability-create-availability-set.png)

## <a name="ensure-availability-set-fault-tolerance"></a>Garantire la tolleranza di errore del set di disponibilità 

Advisor identifica i set di disponibilità che contengono una singola macchina virtuale e consiglia di aggiungere uno o più tooit di macchine virtuali. Per fornire ridondanza tooyour applicazione, si consiglia di raggruppare due o più macchine virtuali in un set di disponibilità. Questa configurazione assicura che durante un evento di manutenzione pianificato o non pianificato, almeno una macchina virtuale sia disponibile e soddisfa hello macchina virtuale di Azure contratto di servizio. È possibile scegliere entrambi toocreate una macchina virtuale o toouse una macchina virtuale esistente e tooadd è toohello set di disponibilità.  

![Indicazione: aggiungere uno o più set di disponibilità toothis di macchine virtuali](./media/advisor-high-availability-recommendations/advisor-high-availability-add-vm-to-availability-set.png)


## <a name="ensure-application-gateway-fault-tolerance"></a>Garantire la tolleranza di errore del gateway applicazione
la continuità aziendale di hello tooensure di applicazioni mission-critical supportate da gateway per applicazioni, Advisor identifica le istanze del gateway applicazioni non sono configurate per la tolleranza di errore, pertanto si consiglia di azioni di correzione da eseguire . Advisor identifica i gateway applicazione di medie o grandi dimensioni a istanza singola e consiglia di aggiungere almeno un'altra istanza. Inoltre, identifica instance singolo o più piccola applicazione gateway e consiglia toomedium la migrazione o SKU di grandi dimensioni. Advisor consiglia tooensure queste azioni che le istanze del gateway applicazione sono toosatisfy configurato hello SLA i requisiti correnti per tali risorse.

![Consiglio di Advisor: distribuire due o più istanze di gateway applicazione di medie o grandi dimensioni](./media/advisor-high-availability-recommendations/advisor-high-availability-application-gateway.png)

## <a name="improve-hello-performance-and-reliability-of-virtual-machine-disks"></a>Migliorare le prestazioni di hello e affidabilità dei dischi della macchina virtuale

Advisor identifica le macchine virtuali con dischi standard e consiglia di aggiornare i dischi toopremium.
 
Archiviazione Premium di Azure offre prestazioni elevate e supporto per dischi a bassa latenza per le macchine virtuali che eseguono carichi di lavoro con attività di I/O intensive. I dischi delle macchine virtuali che usano account di Archiviazione Premium memorizzano i dati in unità SSD. Per prestazioni ottimali di hello per l'applicazione, è consigliabile eseguire la migrazione i dischi di macchina virtuale che richiedono archiviazione toopremium IOPS elevata. 

Se i dischi non richiedono un numero elevato di operazioni di I/O al secondo, è possibile limitare i costi mantenendoli nel servizio di archiviazione Standard. L'archiviazione Standard memorizza i dati dei dischi delle macchine virtuali nelle unità disco rigido anziché nelle unità SSD. È possibile scegliere toomigrate i dischi toopremium dischi di macchina virtuale. I dischi Premium sono supportati nella maggior parte degli SKU delle macchine virtuali. Tuttavia, in alcuni casi, se si desidera che i dischi premium toouse, potrebbe essere tooupgrade la macchina virtuale SKU anche.

![Indicazione: migliorare l'affidabilità di hello i dischi di macchina virtuale, effettuare l'aggiornamento toopremium dischi](./media/advisor-high-availability-recommendations/advisor-high-availability-upgrade-to-premium-disks.png)

## <a name="protect-your-virtual-machine-data-from-accidental-deletion"></a>Proteggere i dati delle macchine virtuali da eliminazioni accidentali
Advisor identifica le macchine virtuali in cui il backup non è abilitato e consiglia di abilitare il backup. Configurazione del backup di macchina virtuale garantisce la disponibilità dei dati aziendali critici hello e offre protezione da eliminazioni accidentali o danneggiamento.

![Indicazione: configurare i dati critici di tooprotect backup di macchine virtuali](./media/advisor-high-availability-recommendations/advisor-high-availability-virtual-machine-backup.png)

## <a name="access-high-availability-recommendations-in-advisor"></a>Accedere ai consigli sulla disponibilità elevata in Advisor

1. Accedi toohello [portale di Azure](https://portal.azure.com).

2. Nel riquadro di sinistra hello, fare clic su **più servizi**.

3. Hello servizio dei menu, in **monitoraggio e gestione**, fare clic su **Advisor Azure**.  
 Hello Advisor dashboard viene visualizzato.

4. Nel dashboard di Advisor hello, fare clic su hello **la disponibilità elevata** scheda e quindi selezionare hello sottoscrizione per cui si desidera tooreceive indicazioni.

> [!NOTE]
> tooaccess raccomandazioni di Advisor, è innanzitutto necessario *registrare la sottoscrizione* con Advisor. Una sottoscrizione viene registrata quando un *sottoscrizione proprietario* avvia hello hello di dashboard e fa clic su Advisor **consigli** pulsante. Si tratta di un'*operazione una tantum*. Dopo la sottoscrizione hello è registrata, è possibile accedere raccomandazioni di Advisor come *proprietario*, *collaboratore*, o *lettore* per una sottoscrizione, un gruppo di risorse, o risorsa specifica.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sui consigli di Advisor, vedere:
* [Introduzione tooAzure Advisor](advisor-overview.md)
* [Introduzione ad Advisor](advisor-get-started.md)
* [Advisor Cost recommendations](advisor-performance-recommendations.md) (Consigli di Advisor sui costi)
* [Advisor Performance recommendations](advisor-performance-recommendations.md) (Consigli di Advisor sulle prestazioni)
* [Advisor Security recommendations](advisor-security-recommendations.md) (Consigli di Advisor sulla sicurezza)

