---
title: "aaaPlan capacità e scalabilità per VMware replica tooAzure con Azure Site Recovery | Documenti Microsoft"
description: "Utilizzare questa capacità tooplan articolo e la scala per la replica delle macchine virtuali VMware tooAzure con Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 0a1cd8eb-a8f7-4228-ab84-9449e0b2887b
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/24/2017
ms.author: rayne
ms.openlocfilehash: 7ca9147d1b4611f6b4a67c3de3f27fb9878f4c4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="plan-capacity-and-scaling-for-vmware-replication-with-azure-site-recovery"></a>Pianificare la capacità e la scalabilità per la replica VMware con Azure Site Recovery

Utilizzare questo toofigure articolo pianificazione della capacità e scalabilità, la replica di macchine virtuali VMware in locale e server fisici tooAzure con [Azure Site Recovery](site-recovery-overview.md).

## <a name="how-do-i-start-capacity-planning"></a>Come si inizia per pianificare la capacità?

Raccogliere informazioni sull'ambiente di replica eseguendo hello [pianificazione della distribuzione di ripristino del sito Azure](https://aka.ms/asr-deployment-planner-doc) per la replica VMware. [Altre informazioni](site-recovery-deployment-planner.md) su questo strumento. È possibile ottenere informazioni sulle macchine virtuali compatibili e non, i dischi per ogni macchina virtuale e la varianza di dati per ogni disco. strumento Hello riguarda anche i requisiti di larghezza di banda di rete e hello necessario per il failover della replica e di test ha esito positivo dell'infrastruttura di Azure.

## <a name="capacity-considerations"></a>Considerazioni sulla capacità

**Componente** | **Dettagli** |
--- | --- | ---
**Replica** | **Frequenza di modifica massimo giornaliero:** un computer protetto è possibile utilizzare solo un server di elaborazione e un server singolo processo può gestire un tasso di modifica giornaliero backup too2 TB. 2 TB, pertanto è modifica dei dati di giornaliera massima hello frequenza con cui è supportato per un computer protetto.<br/><br/> **Velocità effettiva massima:** un computer replicato può appartenere tooone account di archiviazione in Azure. Un account di archiviazione standard può gestire un massimo di 20.000 richieste al secondo, si consiglia di mantenere il numero di hello di operazioni di input/output al secondo (IOPS) tra un too20 macchina di origine, 000. Ad esempio, se si dispone di una macchina di origine con 5 dischi e ogni disco genera 120 IOPS (dimensioni di 8 KB) nel computer di origine hello, sarà all'interno di hello Azure limite di IOPS disco pari a 500. (numero hello di account di archiviazione richiesto è macchina di origine totale toohello uguale IOPS, diviso per 20.000).
**Server di configurazione** | il server di configurazione di Hello dovrebbe essere capacità di frequenza giornaliera modifica di toohandle in grado di hello in tutti i carichi di lavoro in esecuzione in macchine virtuali protette e deve toocontinuously della larghezza di banda sufficiente replicare dati tooAzure archiviazione.<br/><br/> Come procedura consigliata, individuare il server di configurazione hello in hello stessa rete e segmento LAN come hello macchine da tooprotect. Sono reperibili in una rete diversa, ma le macchine da tooprotect devono avere tooit di visibilità livello rete 3.<br/><br/> Dimensioni consigliate per il server di configurazione di hello sono riepilogati nella tabella hello nella seguente sezione hello.
**Server di elaborazione** | primo server di elaborazione Hello è installato per impostazione predefinita nel server di configurazione hello. È possibile distribuire processo aggiuntivo server tooscale l'ambiente. <br/><br/> server di elaborazione Hello riceve i dati di replica da macchine virtuali protette e ottimizzata con la memorizzazione nella cache, la compressione e crittografia. Viene quindi inviato tooAzure dati hello. computer server di processo Hello deve avere sufficiente tooperform risorse queste attività.<br/><br/> server di elaborazione Hello utilizza una cache basata su disco. Utilizzare un disco separato della cache di 600 GB o più modifiche di dati toohandle archiviate nell'evento hello di un collo di bottiglia di rete o di interruzione.

## <a name="size-recommendations-for-hello-configuration-server"></a>Dimensioni consigliate per il server di configurazione di hello

**CPU** | **Memoria** | **Dimensione disco cache** | **Frequenza di modifica dei dati** | **Computer protetti**
--- | --- | --- | --- | ---
8 vCPU (2 socket * 4 core a 2.5 gigahertz [GHz]) | 16 GB | 300 GB | 500 GB o inferiore | Replicare meno di 100 computer.
12 vCPU (2 socket * 6 core a 2,5 GHz) | 18 GB | 600 GB | 500 GB too1 TB | Replicare tra 100 e 150 computer.
16 vCPU (2 socket * 8 core a 2,5 GHz) | 32 GB | 1 TB | 1 TB too2 TB | Replicare tra 150 e 200 computer.
Distribuire un altro server di elaborazione | | | Superiore a 2 TB | Distribuire i server di elaborazione aggiuntive se si esegue la replica di più di 200 macchine, o se i dati giornalieri hello modifica frequenza supera i 2 TB.

Dove:

* Ogni computer di origine è configurato con 3 dischi da 100 GB.
* La risorsa di archiviazione di benchmarking usata per le misurazioni del disco della cache è di 8 unità SAS a 10.000 RPM con RAID 10.

## <a name="size-recommendations-for-hello-process-server"></a>Dimensioni consigliate per il server di elaborazione hello

Se è necessario tooprotect più di 200 macchine o modifiche giornaliere hello è maggiore di 2 TB, è possibile aggiungere server toohandle hello replica il caricamento del processo. tooscale out, è possibile:

* Aumentare il numero di hello del server di configurazione. Ad esempio, è possibile proteggere le macchine too400 con due server di configurazione.
* Aggiungere ulteriori server di elaborazione e usare questi server di configurazione toohandle hello traffico anziché (o in aggiunta a).

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


## <a name="control-network-bandwidth"></a>Controllare la larghezza di banda della rete

Dopo aver utilizzato hello [strumento di pianificazione della distribuzione hello](site-recovery-deployment-planner.md) toocalculate hello larghezza di banda necessaria per la replica (la replica iniziale hello e quindi delta), è possibile controllare hello quantità di larghezza di banda utilizzata per la replica con un paio opzioni:

* **Limitazione della larghezza di banda**: VMware che vengono replicati tooAzure del traffico tramite un server di processo specifico. È possibile limitare la larghezza di banda su computer hello in esecuzione come server di elaborazione.
* **Influiscono sulla larghezza di banda**: È possibile influenzare la larghezza di banda hello utilizzata per la replica con un paio di chiavi del Registro di sistema:
  * Hello **Backup\UploadThreadsPerVM Azure HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows** valore del Registro di sistema specifica il numero di hello di thread utilizzati per il trasferimento di dati (la replica iniziale o delta) di un disco. Un valore maggiore aumenta hello larghezza di banda utilizzata per la replica.
  * Hello **Backup\DownloadThreadsPerVM Azure HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows** specifica hello numero di thread utilizzati per il trasferimento dei dati durante il failback.

### <a name="throttle-bandwidth"></a>Limitare la larghezza di banda

1. Aprire hello snap-in MMC di Backup di Azure nel ruolo di macchina hello come server di elaborazione hello. Per impostazione predefinita, un collegamento per il Backup è disponibile sul desktop hello o nella seguente cartella hello: C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.
2. Hello nello snap-in, fare clic su **Modifica proprietà**.

    ![Proprietà di toochange snap-in Opzioni di schermata di MMC di Backup Azure](./media/site-recovery-vmware-to-azure/throttle1.png)
3. In hello **limitazione** , selezionare **abilitare la limitazione per le operazioni di backup all'utilizzo della larghezza di banda di internet**. Impostare i limiti di hello per lavoro e non lavorative ore. Valori validi sono compresi 512 Mbps di too102 Kbps al secondo.

    ![Screenshot della finestra di dialogo Proprietà di Azure Backup](./media/site-recovery-vmware-to-azure/throttle2.png)

È inoltre possibile utilizzare hello [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) tooset limitazione delle richieste di cmdlet. Di seguito è riportato un esempio:

    $mon = [System.DayOfWeek]::Monday
    $tue = [System.DayOfWeek]::Tuesday
    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth  (512*1024) -NonWorkHourBandwidth (2048*1024)

**Set-OBMachineSetting -NoThrottle** indica che non è necessaria alcuna limitazione.

### <a name="influence-network-bandwidth-for-a-vm"></a>Influire sulla larghezza di banda della rete per una VM

1. Nel Registro di sistema della macchina virtuale di hello, passare troppo**Backup\Replication Azure HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows**.
   * il traffico di larghezza di banda hello tooinfluence su un disco di replica, modificare il valore di hello di **UploadThreadsPerVM**, o creare la chiave di hello se non esiste.
   * larghezza di banda hello tooinfluence per il traffico di failback da Azure, modificare il valore di hello di **DownloadThreadsPerVM**.
2. valore predefinito di Hello è 4. In una rete di "provisioning eccessivo", queste chiavi del Registro di sistema devono essere modificate dai valori predefiniti di hello. Hello massimo è 32. Monitorare il traffico toooptimize hello valore.


## <a name="deploy-additional-process-servers"></a>Distribuire server di elaborazione aggiuntivi

Se si tooscale orizzontalmente la distribuzione oltre 200 macchine di origine, o si dispone di un totale giornaliero varianza del tasso di più di 2 TB, è necessario volume di traffico hello toohandle server processo aggiuntivo. Seguire queste istruzioni tooset dei server di elaborazione hello. Dopo aver configurato il server di hello, eseguire la migrazione toouse macchine di origine è.

1. In **server di ripristino del sito**, fare clic su server di configurazione hello e quindi fare clic su **Server di elaborazione**.

    ![Schermata di Site Recovery server opzione tooadd un server di elaborazione](./media/site-recovery-vmware-to-azure/migrate-ps1.png)
2. In **Tipo di server** fare clic su **Process server (on-premises)** (Server di elaborazione (locale)).

    ![Screenshot della finestra di dialogo Server di elaborazione](./media/site-recovery-vmware-to-azure/migrate-ps2.png)
3. Scaricare il file di installazione unificata di Site Recovery hello ed eseguirlo tooinstall hello processo server. Verrà inoltre registrata nell'insieme di credenziali hello.
4. In **prima di iniziare**selezionare **aggiungere processo aggiuntivo server tooscale distribuzione**.
5. Creazione guidata hello completo in hello allo stesso modo, si ha quando si [impostare](#step-2-set-up-the-source-environment) server di configurazione hello.

    ![Screenshot della procedura guidata per l'installazione unificata di Azure Site Recovery](./media/site-recovery-vmware-to-azure/add-ps1.png)
6. In **i dettagli di configurazione Server**, specificare l'indirizzo IP hello hello del server di configurazione e hello passphrase. passphrase hello tooobtain, eseguire **[SiteRecoveryInstallationFolder]\home\sysystems\bin\genpassphrase.exe-n** nel server di configurazione hello.

    ![Screenshot della pagina dei dettagli del server di configurazione](./media/site-recovery-vmware-to-azure/add-ps2.png)

### <a name="migrate-machines-toouse-hello-new-process-server"></a>Eseguire la migrazione di macchine toouse hello nuovo server di elaborazione
1. In **impostazioni** > **server di ripristino del sito**, fare clic su server di configurazione hello e quindi espandere **elaborare server**.

    ![Screenshot della finestra di dialogo Server di elaborazione](./media/site-recovery-vmware-to-azure/migrate-ps2.png)
2. Fare doppio clic su server di elaborazione hello attualmente in uso e fare clic su **commutatore**.

    ![Screenshot della finestra di dialogo Server di configurazione](./media/site-recovery-vmware-to-azure/migrate-ps3.png)
3. In **il server di elaborazione di destinazione selezionare**selezionare hello nuovo server di elaborazione toouse desiderato e quindi selezionare le macchine virtuali hello server hello gestirà. Fare clic su hello icona tooget informazioni sui server hello. toohelp verificare le decisioni di caricamento, hello Media dello spazio è sufficiente tooreplicate viene visualizzato ogni macchina virtuale selezionata toohello nuovo server di elaborazione. Fare clic su hello segno di spunta toostart replica toohello nuovo server di elaborazione.


## <a name="next-steps"></a>Passaggi successivi

Scaricare ed eseguire hello [pianificazione della distribuzione di ripristino del sito Azure](https://aka.ms/asr-deployment-planner)
