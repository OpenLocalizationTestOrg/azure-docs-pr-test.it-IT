---
title: "aaaPlan capacità e scalabilità per tooAzure replica server fisico con Azure Site Recovery | Documenti Microsoft"
description: "Utilizzare questa capacità tooplan articolo e la scala per la replica tooAzure server fisici Windows/Linux con Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 554f59ee-0b49-4779-9737-90cb601ef6fe
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/27/2017
ms.author: rayne
ms.openlocfilehash: 209980963c07d13e15802a5da44769ac559217d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="step-3-plan-capacity-and-scaling-for-physical-server-tooazure-replication"></a>Passaggio 3: Pianificare la capacità e scalabilità per la replica tooAzure server fisico

Utilizzare toofigure questo articolo le capacità e scalabilità, quando si esegue la replica locale tooAzure server fisici Windows/Linux con [Azure Site Recovery](site-recovery-overview.md).

Inviare commenti e domande nella parte inferiore di hello di questo articolo, o di hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="plan-deployment-capacity"></a>Pianificare la capacità di distribuzione

1. Leggere questo [articolo](site-recovery-plan-capacity-vmware.md) toolearn sulla stima dei requisiti della replica e istruzioni per il ridimensionamento componenti Site Recovery.
2. Lettura considerazioni hello sotto toolearn sui componenti server di scalabilità e il controllo della larghezza di banda computer replicato.

## <a name="replication-considerations"></a>Considerazioni sulla replica

Utilizzare queste toofigure considerazioni requisiti server replicato.

**Componente** | **Dettagli** 
--- | --- 
**Replica** | **Frequenza di modifica massimo giornaliero:** un computer protetto è possibile utilizzare solo un server di elaborazione e un server singolo processo può gestire un tasso di modifica giornaliero backup too2 TB. 2 TB, pertanto è modifica dei dati di giornaliera massima hello frequenza con cui è supportato per un computer protetto.<br/><br/> **Velocità effettiva massima:** un computer replicato può appartenere tooone account di archiviazione in Azure. Un account di archiviazione standard può gestire un massimo di 20.000 richieste al secondo, si consiglia di mantenere il numero di hello di operazioni di input/output al secondo (IOPS) tra un too20 macchina di origine, 000. Ad esempio, se si dispone di una macchina di origine con 5 dischi e ogni disco genera 120 IOPS (dimensioni di 8 KB) nel computer di origine hello, sarà all'interno di hello Azure limite di IOPS disco pari a 500. (numero hello di account di archiviazione richiesto è macchina di origine totale toohello uguale IOPS, diviso per 20.000).

## <a name="configuration-server-capacity"></a>Capacità del server di configurazione

il server di configurazione di Hello dovrebbe essere capacità di frequenza giornaliera modifica di toohandle in grado di hello in tutti i carichi di lavoro in esecuzione in macchine virtuali protette e deve toocontinuously della larghezza di banda sufficiente replicare dati tooAzure archiviazione.

Come procedura consigliata, individuare il server di configurazione hello in hello stessa rete e segmento LAN come hello macchine da tooprotect. Sono reperibili in una rete diversa, ma le macchine da tooprotect devono avere tooit di visibilità livello rete 3.

## <a name="sizing-recommendations"></a>Consigli sul ridimensionamento

tabella Hello sono riepilogati i requisiti di ridimensionamento in base alle CPU.

**CPU** | **Memoria** | **Dimensione disco cache** | **Frequenza di modifica dei dati** | **Computer protetti**
--- | --- | --- | --- | ---
8 vCPU (2 socket * 4 core a 2.5 gigahertz [GHz]) | 16 GB | 300 GB | 500 GB o inferiore | Replicare meno di 100 computer.
12 vCPU (2 socket * 6 core a 2,5 GHz) | 18 GB | 600 GB | 500 GB too1 TB | Replicare tra 100 e 150 computer.
16 vCPU (2 socket * 8 core a 2,5 GHz) | 32 GB | 1 TB | 1 TB too2 TB | Replicare tra 150 e 200 computer.
Distribuire un altro server di elaborazione | | | Superiore a 2 TB | Distribuire i server di elaborazione aggiuntive se si esegue la replica di più di 200 macchine, o se i dati giornalieri hello modifica frequenza supera i 2 TB.

Dove:

* Ogni computer di origine è configurato con 3 dischi da 100 GB.
* La risorsa di archiviazione di benchmarking usata per le misurazioni del disco della cache è di 8 unità SAS a 10.000 RPM con RAID 10.

## <a name="process-server-capacity"></a>Capacità del server di elaborazione


server di elaborazione Hello riceve i dati di replica da macchine virtuali protette e ottimizzata con la memorizzazione nella cache, la compressione e crittografia. Viene quindi inviato tooAzure dati hello.

- computer server di processo Hello deve avere sufficiente tooperform risorse queste attività.
- primo server di elaborazione Hello è installato per impostazione predefinita nel server di configurazione hello. È possibile distribuire processo aggiuntivo server tooscale l'ambiente.
- server di elaborazione Hello utilizza una cache basata su disco. Utilizzare un disco separato della cache di 600 GB o più modifiche di dati toohandle archiviate nell'evento hello di un collo di bottiglia di rete o di interruzione.
- Se è necessario tooprotect più di 200 macchine o modifiche giornaliere hello è maggiore di 2 TB, è possibile aggiungere server toohandle hello replica il caricamento del processo. tooscale out, è possibile:
    - Aumentare il numero di hello del server di configurazione. Ad esempio, è possibile proteggere le macchine too400 con due server di configurazione.
    - Aggiungere ulteriori server di elaborazione e usare questi server di configurazione toohandle hello traffico anziché (o in aggiunta a).


### <a name="example-process-server-scaling"></a>Ridimensionamento del server di elaborazione di esempio

Hello nella tabella seguente viene descritto uno scenario in cui:

* Non si prevede server di configurazione hello toouse come un server di elaborazione.
* È stato configurato un server di elaborazione aggiuntivo.
* Server di elaborazione aggiuntive di macchine virtuali protette toouse hello configurati.
* Ogni computer di origine protetto è configurato con tre dischi da 100 GB.

**Server di configurazione** | **Server di elaborazione aggiuntivo** | **Dimensione disco cache** | **Frequenza di modifica dei dati** | **Computer protetti**
--- | --- | --- | --- | ---
8 vCPU (2 socket * 4 core a 2,5 GHz), 16 GB di memoria | 4 vCPU (2 socket * 2 core a 2,5 GHz), 8 GB di memoria | 300 GB | 250 GB o inferiore | Eseguire la replica di un massimo di 85 macchine.
8 vCPU (2 socket * 4 core a 2,5 GHz), 16 GB di memoria | 8 vCPU (2 socket * 4 core a 2,5 GHz), 12 GB di memoria | 600 GB | 250 GB too1 TB | Replicare tra 85 e 150 computer.
12 vCPU (2 socket * 6 core a 2,5 GHz), 18 GB di memoria | 12 vCPU (2 socket * 6 core a 2,5 GHz), 24 GB di memoria | 1 TB | 1 TB too2 TB | Replicare tra 150 e 225 computer.

modo Hello in cui si modifica la scala dei server varia a seconda delle proprie preferenze per un modello di scalabilità verticale o orizzontale.  L'aumento delle prestazioni si ottiene distribuendo alcuni server di configurazione e di elaborazione avanzati, mentre l'aumento del numero di istanze si ottiene distribuendo più server con meno risorse. Ad esempio, se è necessario tooprotect 220 macchine, è possibile eseguire una delle seguenti hello:

* Impostare il server di configurazione hello con un server di elaborazione aggiuntive con CPU virtuali 12, 24 GB di memoria, 18 GB di memoria e CPU virtuali 12. Configurare macchine virtuali protette toouse hello processo aggiuntivo solo server.
* Consente di impostare due server di configurazione (2 x 8 CPU virtuali, 16 GB di RAM) e due i server di elaborazione aggiuntive (CPU 1x8 virtuali e le macchine [220] 4 CPU virtuali x 1 toohandle 135 + 85). Configurare macchine virtuali protette toouse hello processo aggiuntivo solo i server.

## <a name="deploy-additional-process-servers"></a>Distribuire server di elaborazione aggiuntivi

1. Seguire [queste istruzioni](site-recovery-vmware-setup-azure-ps-resource-manager.md) tooset di un server di elaborazione aggiuntive.
2. Se non si dispone di hello passphrase, eseguire **[SiteRecoveryInstallationFolder]\home\sysystems\bin\genpassphrase.exe-n** su hello configurazione server tooget è.
3. Dopo aver configurato il server di elaborazione hello, eseguire la migrazione toouse macchine di origine è.

    1. In **impostazioni** > **server di ripristino del sito**, fare clic su server di configurazione hello > **elaborare server**.
    2. Server di elaborazione rapida hello attualmente in uso > **commutatore**.
    3. In **il server di elaborazione di destinazione selezionare**, selezionare i server di elaborazione hello toouse desiderati e selezionare le macchine virtuali hello server hello gestirà.
    4. Fare clic sull'icona informazioni hello. toohelp verificare le decisioni di caricamento, hello Media dello spazio è sufficiente tooreplicate ogni VM toohello nuovo server di elaborazione selezionato viene visualizzato.
    5. Fare clic su hello segno di spunta toostart replica toohello nuovo server di elaborazione.

## <a name="control-network-bandwidth"></a>Controllare la larghezza di banda della rete

Dopo aver eseguito [strumento di pianificazione della distribuzione hello](site-recovery-deployment-planner.md) toocalculate hello larghezza di banda necessaria per la replica (la replica iniziale hello e quindi delta), è possibile controllare hello quantità di larghezza di banda utilizzata per la replica con due opzioni:

* **Limitazione della larghezza di banda**: VMware che vengono replicati tooAzure del traffico tramite un server di processo specifico. È possibile limitare la larghezza di banda su computer hello in esecuzione come server di elaborazione.
* **Influiscono sulla larghezza di banda**: È possibile influenzare la larghezza di banda hello utilizzata per la replica con un paio di chiavi del Registro di sistema:
  * Hello **Backup\UploadThreadsPerVM Azure HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows** valore del Registro di sistema specifica il numero di hello di thread utilizzati per il trasferimento di dati (la replica iniziale o delta) di un disco. Un valore maggiore aumenta hello larghezza di banda utilizzata per la replica.
  * Hello **Backup\DownloadThreadsPerVM Azure HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows** specifica hello numero di thread utilizzati per il trasferimento dei dati durante il failback.

### <a name="throttle-bandwidth"></a>Limitare la larghezza di banda

1. Aprire hello snap-in MMC di Backup di Azure nel ruolo di macchina hello come server di elaborazione hello. Per impostazione predefinita, un collegamento per il Backup è disponibile sul desktop hello o nella seguente cartella hello: C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.
2. Hello nello snap-in, fare clic su **Modifica proprietà**.
3. In hello **limitazione** , selezionare **abilitare la limitazione per le operazioni di backup all'utilizzo della larghezza di banda di internet**.
4. Impostare i limiti di hello per lavoro e non lavorative ore. Valori validi sono compresi 512 Mbps di too102 Kbps al secondo.

    ![Limitazione](./media/physical-walkthrough-capacity/throttle2.png)

È inoltre possibile utilizzare hello [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) tooset limitazione delle richieste di cmdlet. Di seguito è riportato un esempio:

    $mon = [System.DayOfWeek]::Monday
    $tue = [System.DayOfWeek]::Tuesday
    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth  (512*1024) -NonWorkHourBandwidth (2048*1024)

**Set-OBMachineSetting -NoThrottle** indica che non è necessaria alcuna limitazione.

### <a name="influence-network-bandwidth-for-a-vm"></a>Influire sulla larghezza di banda della rete per una VM

1. Nel Registro di sistema di hello macchina virtuale, andare troppo**Backup\Replication Azure HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows**.
   * il traffico di larghezza di banda hello tooinfluence su un disco di replica, modificare il valore di hello di **UploadThreadsPerVM**, o creare la chiave di hello se non esiste.
   * larghezza di banda hello tooinfluence per il traffico di failback da Azure, modificare il valore di hello di **DownloadThreadsPerVM**.
2. valore predefinito di Hello è 4. In una rete con provisioning eccessivo è necessario modificare queste chiavi del Registro di sistema. Hello massimo è 32. Monitorare il traffico toooptimize hello valore.




## <a name="next-steps"></a>Passaggi successivi

Andare troppo[passaggio 4: pianificare la rete](physical-walkthrough-network.md).
