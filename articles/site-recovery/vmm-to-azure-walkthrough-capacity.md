---
title: "aaaPlan capacità e scalabilità per la macchina virtuale Hyper-V replica (con VMM) tooAzure con Azure Site Recovery | Documenti Microsoft"
description: "Utilizzare questa capacità tooplan articolo e la scala quando la replica delle macchine virtuali Hyper-V in VMM cloud tooAzure, con Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 41c3c83e-6b1a-496a-8179-498c552ef0c7
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 9818ada9bb21f60ac00b3894696201b06630cb2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="step-3-plan-capacity-and-scaling-for-hyper-v-with-vmm-tooazure-replication"></a>Passaggio 3: Pianificare la capacità e scalabilità per la replica Hyper-V (con VMM) tooAzure

Dopo aver esaminato hello [prerequisiti di distribuzione](vmm-to-azure-walkthrough-prerequisites.md), utilizzare toofigure questo articolo out pianificazione della capacità e scalabilità, la replica locale di macchine virtuali Hyper-V tooAzure cloud di System Center Virtual Machine Manager (VMM), con [Azure Site Recovery](site-recovery-overview.md).

Dopo aver letto questo articolo, inviare eventuali commenti nella parte inferiore di hello o porre domande tecniche su hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="how-do-i-start-capacity-planning"></a>Come si inizia per pianificare la capacità?


Raccogliere informazioni l'ambiente di replica e la capacità di piano utilizzando i dati di hello, insieme alle considerazioni di hello evidenziati in questo articolo.


## <a name="gather-information"></a>Raccogliere informazioni

1. Raccogliere informazioni sull'ambiente di replica, incluse le macchine virtuali, i dischi per ogni macchina virtuale e le risorse di archiviazione per ogni disco.
2. Identificare la frequenza di modifica giornaliera (varianza) per i dati replicati. Scaricare hello [strumento la pianificazione della capacità di Hyper-V](https://www.microsoft.com/download/details.aspx?id=39057) frequenza di modifica tooget hello. È consigliabile che eseguire questo strumento su un toocapture settimana medie.
 

## <a name="figure-out-capacity"></a>Calcolare la capacità

In base alle informazioni di hello che la raccolta di dati, si esegue hello [strumento pianificazione della capacità di ripristino sito](http://aka.ms/asr-capacity-planner-excel) tooanalyze l'ambiente di origine e i carichi di lavoro, stimare le esigenze di larghezza di banda e risorse del server per il percorso di origine hello e hello risorse (macchine virtuali e archiviazione e così via), che è necessario che nel percorso di destinazione hello. È possibile eseguire lo strumento hello in due modi:

- Pianificazione rapida: lo strumento hello in questa modalità le proiezioni di rete e server tooget in base a un numero medio di macchine virtuali, dischi, archiviazione e frequenza di modifica.
- Modalità di pianificazione: eseguire lo strumento hello in questa modalità e fornire i dettagli di ogni carico di lavoro a livello di macchina virtuale. Analizzare la compatibilità della macchina virtuale e ottenere le proiezioni di rete e server.

Eseguire lo strumento hello:

1. Scaricare hello [strumento](http://aka.ms/asr-capacity-planner-excel)
2. pianificazione di hello toorun rapido, seguire [queste istruzioni](site-recovery-capacity-planner.md#run-the-quick-planner), scenario selezionare hello e **tooAzure Hyper-V**.
3. toorun hello planner dettagliato, attenersi alla [queste istruzioni](site-recovery-capacity-planner.md#run-the-detailed-planner), uno scenario selezionare hello e **tooAzure Hyper-V**.

## <a name="control-network-bandwidth"></a>Controllare la larghezza di banda della rete

Dopo aver calcolato hello di banda che richiesta, è necessario un paio di opzioni per la quantità di hello controllo della larghezza di banda utilizzata per la replica:

* **Limitazione della larghezza di banda**: Hyper-V che vengono replicati tooAzure del traffico tramite uno specifico host Hyper-V. È possibile limitare la larghezza di banda nel server host hello.
* **Influiscono sulla larghezza di banda**: È possibile influenzare la larghezza di banda hello utilizzata per la replica con un paio di chiavi del Registro di sistema.

### <a name="throttle-bandwidth"></a>Limitare la larghezza di banda
1. Aprire hello MMC di Backup di Microsoft Azure snap-nel server host Hyper-V di hello. Per impostazione predefinita, un collegamento per il Backup di Microsoft Azure è disponibile sul desktop hello o in C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.
2. Nello snap-in hello fare clic su **Modifica proprietà**.
3. In hello **limitazione** scheda selezionare **abilitare la limitazione per le operazioni di backup all'utilizzo della larghezza di banda di internet**e impostare i limiti di hello per lavoro e non lavorative ore. Valori validi sono compresi 512 Mbps di too102 Kbps al secondo.

    ![Limitare la larghezza di banda](./media/vmm-to-azure-walkthrough-capacity/throttle2.png)

È inoltre possibile utilizzare hello [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) tooset limitazione delle richieste di cmdlet. Di seguito è riportato un esempio:

    $mon = [System.DayOfWeek]::Monday
    $tue = [System.DayOfWeek]::Tuesday
    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth  (512*1024) -NonWorkHourBandwidth (2048*1024)

**Set-OBMachineSetting -NoThrottle** indica che non è necessaria alcuna limitazione.

### <a name="influence-network-bandwidth"></a>Influire sulla larghezza di banda di rete
1. Nel Registro di sistema hello passare troppo**Backup\Replication Azure HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows**.
   * il traffico di larghezza di banda hello tooinfluence su un disco di replica, modificare hello valore hello **UploadThreadsPerVM**, o creare la chiave di hello se non esiste.
   * larghezza di banda hello tooinfluence per il traffico di failback da Azure, modificare il valore di hello **DownloadThreadsPerVM**.
2. valore predefinito di Hello è 4. In una rete di "provisioning eccessivo", queste chiavi del Registro di sistema devono essere modificate dai valori predefiniti di hello. Hello massimo è 32. Monitorare il traffico toooptimize hello valore.

## <a name="next-steps"></a>Passaggi successivi

Andare troppo[passaggio 4: pianificare la rete](vmm-to-azure-walkthrough-network.md).
