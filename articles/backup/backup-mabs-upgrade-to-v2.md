---
title: Server di Backup di Azure v2 aaaInstall | Documenti Microsoft
description: "Il server di Backup di Azure v2 offre funzionalità avanzate di backup per la protezione di VM, file e cartelle, carichi di lavoro e altro ancora. Informazioni su come tooAzure tooinstall o aggiornare il Server di Backup v2."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: masaran;markgal
ms.openlocfilehash: 5b1699dadd3a173f1c0ef91a1a600bc5e12f20ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="install-azure-backup-server-v2"></a>Installare il server di Backup di Azure v2

Il server di Backup di Azure consente di proteggere macchine virtuali (VM), carichi di lavoro, file e cartelle, e altro ancora. Il server di Backup di Azure v2 si basa sul server di Backup di Azure v1 e offre nuove funzionalità che non sono disponibili nella v1. Per un confronto delle funzionalità fra la v1 e la v2, vedere [Matrice di protezione del server di Backup di Azure](backup-mabs-protection-matrix.md). 

funzionalità aggiuntive di Hello v2 Server Backup sono un aggiornamento da Server di Backup v1. Tuttavia, il server di backup v1 non è un prerequisito per l'installazione del server di backup v2. Se si desidera tooupgrade dal Server di Backup v1 tooBackup v2 Server, installare v2 Server di Backup nel server di protezione hello Backup Server. Le impostazioni del server di backup esistenti rimangono invariate.

È possibile installare il server di backup v2 in Windows Server 2012 R2 o in Windows Server 2016. tootake le nuove funzionalità quali la archiviazione System Center 2016 Data Protection Manager moderno Backup, è necessario installare il Server di Backup v2 in Windows Server 2016. Prima di aggiornare tooor install v2 Backup Server, informazioni hello [prerequisiti di installazione](https://docs.microsoft.com/system-center/dpm/install-dpm#setup-prerequisites).

> [!NOTE]
> Server di Backup di Azure è hello stessa codebase come System Center Data Protection Manager. Backup Server v1 è equivalente tooData Protection Manager 2012 R2 e v2 Server Backup è equivalente tooData Protection Manager 2016. In questo articolo fa riferimento in alcuni casi la documentazione di Data Protection Manager hello.
>
>

## <a name="upgrade-backup-server-toov2"></a>Aggiornamento Server di Backup toov2
tooupgrade dal Server di Backup v1 tooBackup v2 Server, assicurarsi che l'installazione contenga gli aggiornamenti necessario hello:

- [Aggiornare gli agenti protezione hello](backup-mabs-upgrade-to-v2.md#update-the-dpm-protection-agent) su hello server protetti.
- Eseguire l'aggiornamento di Windows Server 2012 R2 tooWindows Server 2016.
- Aggiornare Azure Backup Server Remote Administrator in tutti i server di produzione.
- Verificare che i backup sono impostati toocontinue senza dover riavviare il server di produzione.


### <a name="upgrade-steps-for-backup-server-v2"></a>Passaggi di aggiornamento per il server di backup v2

1. Nell'area Download, hello [scaricare installazione guidata di aggiornamento hello](https://go.microsoft.com/fwlink/?LinkId=626082).

2. Dopo l'installazione guidata di hello estrazione, assicurarsi che **eseguire setup.exe** è selezionata, quindi fare clic **fine**.

  ![Programma di installazione - Eseguire il programma di installazione](./media/backup-mabs-upgrade-to-v2/run-setup.png)

3. Nella procedura guidata di Microsoft Azure Backup Server hello, in **installare**selezionare **il Server di Backup di Microsoft Azure**.

  ![Programma di installazione - Selezionare cosa installare](./media/backup-mabs-upgrade-to-v2/mabs-installer-s1.png)

4. In hello **iniziale** pagina, rivedere gli avvisi di hello e quindi selezionare **Avanti**.

  ![Programma di installazione - Pagina di benvenuto](./media/backup-mabs-upgrade-to-v2/mabs-installer-s2.png)

5. installazione guidata di Hello esegue controlli dei prerequisiti toomake che può aggiornare l'ambiente. In hello **Prerequisite Checks** selezionare **controllare**.

  ![Programma di installazione - Pagina del controllo dei prerequisiti](./media/backup-mabs-upgrade-to-v2/mabs-installer-s3-perform-checks.png)

6. L'ambiente deve superare i controlli dei prerequisiti hello. Se l'ambiente non superano i controlli di hello, tenere presente hello e correggerli. Selezionare quindi **Controlla di nuovo**. Dopo avere passato i controlli dei prerequisiti hello, selezionare **Avanti**.

  ![Programma di installazione - Pulsante per ripetere il controllo](./media/backup-mabs-upgrade-to-v2/mabs-installer-s4-pass-checks.png)

7. In hello **impostazioni SQL** pagina, l'opzione hello rilevanti per l'installazione di SQL e quindi selezionare **controlla e installa**.

  ![Programma di installazione - Pagina delle impostazioni di SQL](./media/backup-mabs-upgrade-to-v2/mabs-installer-s5-sql-settings.png)

  controlli Hello potrebbero richiedere alcuni minuti. Quando i controlli di hello sono finiti, selezionare **Avanti**.

  ![Programma di installazione - Controllo delle impostazioni di SQL e pulsante di installazione](./media/backup-mabs-upgrade-to-v2/mabs-installer-s5a-check-and fix-settings.png)

8. In hello **le impostazioni di installazione** pagina di qualsiasi percorso toohello modifiche in cui è installato il Server di Backup, o toohello percorso dei file temporanei. Selezionare **Avanti**.

  ![Programma di installazione - Pagina delle impostazioni di installazione](./media/backup-mabs-upgrade-to-v2/mabs-installer-s6-installation-settings.png)

9. toofinish hello installazione guidata selezionare **fine**.

  ![Programma di installazione - Fine](./media/backup-mabs-upgrade-to-v2/run-setup.png)



## <a name="add-storage-for-modern-backup-storage"></a>Aggiungere spazio di archiviazione per Modern Backup Storage

l'efficienza di archiviazione di backup tooimprove, v2 Server di Backup aggiunge supporto per i volumi. Come il server di backup v1, la v2 supporta i dischi.

### <a name="add-volumes-and-disks"></a>Aggiungere volumi e dischi
Se si eseguono Backup Server v2 in Windows Server 2016, è possibile utilizzare dati di backup di volumi toostore. I volumi consentono di risparmiare spazio di archiviazione e offrono backup più veloci. Poiché i volumi sono tooBackup nuovo Server, è necessario aggiungerli. 

Quando si aggiunge un Server di tooBackup volume, è possibile assegnare un nome descrittivo volume hello. Fare clic su hello **nome descrittivo** colonna del volume hello desiderato tooname. È possibile modificare il nome di hello in un secondo momento, se necessario. È inoltre possibile utilizzare PowerShell tooadd o modificare i nomi descrittivi per i volumi.

un volume nella Console di amministrazione di hello tooadd:

1. Nella Console di amministrazione di Server di Backup di Azure hello, selezionare **Management** > **archiviazione su disco** > **Aggiungi**.

    ![Procedura guidata Aggiungi archiviazione su disco hello aperto](./media//backup-mabs-upgrade-to-v2/open-add-disk-storage-wizard.png)

    Verrà visualizzata una procedura guidata Aggiungi archiviazione su disco hello.

2. In hello **aggiungere archiviazione su disco** pagina hello **volumi disponibili** , selezionare un volume e quindi selezionare **Aggiungi**.
3. In hello **selezionato volumi** , immettere un nome descrittivo per il volume di hello e quindi selezionare **OK**.

      ![Procedura guidata Aggiungi spazio di archiviazione su disco - Aggiungi volume](./media/backup-mabs-upgrade-to-v2/add-volume.png)

  Se si desidera tooadd un disco, disco hello deve appartenere a gruppo protezione dati tooa legacy di archiviazione. Tali dischi possono essere usati solo per questi gruppi protezione dati. Se Backup Server non dispone di origini che hanno la protezione legacy, non è elencato disco hello.

  Per ulteriori informazioni sull'aggiunta di dischi, vedere [aggiungere dischi di archiviazione legacy tooincrease](http://docs.microsoft.com/system-center/dpm/upgrade-to-dpm-2016#adding-disks-to-increase-legacy-storage). È possibile assegnare un nome descrittivo al disco.


### <a name="assign-workloads-toovolumes"></a>Assegnare i carichi di lavoro toovolumes

Nel Server di Backup, specificare carichi di lavoro assegnati toowhich volumi. Ad esempio, è possibile impostare costosa volumi che supportano un numero elevato di operazioni di input/output al secondo (IOPS) toostore soli i carichi di lavoro che richiedono frequenti backup volumi elevati. Un esempio è SQL Server con i log delle transazioni.

#### <a name="update-dpmdiskstorage"></a>Update-DPMDiskStorage

proprietà hello tooupdate volume nel pool di archiviazione hello nel Server di Backup, utilizzare il cmdlet di PowerShell hello DPMDiskStorage di aggiornamento.

Sintassi:

`Parameter Set: Volume`

```
Update-DPMDiskStorage [-Volume] <Volume> [[-FriendlyName] <String> ] [[-DatasourceType] <VolumeTag[]> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```

Tutte le modifiche apportate tramite PowerShell vengono riflesse in hello dell'interfaccia utente.


## <a name="protect-data-sources"></a>Proteggere le origini dati
toobegin proteggono le origini dati, creare un gruppo protezione dati. Hello seguendo i passaggi evidenziazione modifiche o aggiunte toohello nuovo guidata gruppo protezione dati.

toocreate un gruppo protezione dati:

1. Nella Console di amministrazione di Server di Backup hello, selezionare **protezione**.

2. Sulla barra multifunzione dello strumento di hello, selezionare **New**.

    Verrà visualizzata una procedura guidata Crea nuovo gruppo protezione dati hello.

  ![Procedura guidata Crea nuovo gruppo protezione dati](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-1.png)

3. In hello **iniziale** selezionare **Avanti**.
4. In hello **Selezione tipo di gruppo protezione dati** pagina, selezionare il tipo di hello del gruppo protezione dati desiderato toocreate e quindi selezionare **Avanti**.

  ![Pagina Seleziona tipo di gruppo di protezione dati](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-2.png)

5. In hello **Seleziona membri del gruppo** pagina hello **membri disponibili** riquadro, i membri di hello sono elencati gli agenti protezione. Per questo esempio, selezionare il volume D:\ ed E:\ e li aggiunge toohello **i membri selezionati** riquadro. Selezionare **Avanti**.

  ![Pagina Seleziona membri del gruppo](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-3.png)

6. In hello **Selezione metodo protezione dati** pagina, immettere un **nome del gruppo protezione dati**, selezionare il metodo di protezione hello e quindi selezionare **Avanti**. Se si desidera protezione a breve termine, è necessario selezionare hello **disco** metodo di backup.

  ![Pagina Seleziona metodo protezione dati](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-4.png)

7. In hello **Specifica obiettivi a breve termine** , hello selezionare i dettagli della pagina per **mantenimento** e **frequenza di sincronizzazione**. Quindi selezionare **Avanti**. Facoltativamente, toochange hello pianificazione quando i punti di ripristino vengono prelevati, selezionare **modifica**.

  ![Pagina Specifica obiettivi a breve termine](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-5.png)

8. In hello **Verifica allocazione archiviazione dischi** pagina, esaminare i dettagli sulle origini dati hello è stata selezionata, le dimensioni e i valori per il provisioning di hello spazio toobe e hello volume di archiviazione di destinazione.

  ![Pagina di verifica allocazione dell'archiviazione su disco](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-6.png)

  Volumi di archiviazione si basano sull'allocazione di volume del carico di lavoro hello (impostato tramite PowerShell) e hello spazio di archiviazione disponibile. È possibile modificare i volumi di archiviazione hello selezionando altri volumi nel menu a discesa hello. Se si modifica il valore di hello per **archiviazione di destinazione**, hello valore per **archiviazione su disco disponibile** modificata in modo dinamico i valori tooreflect in **spazio** e **Underprovisioned spazio**.

  Se le origini dati hello crescere come pianificato, hello valore per hello **Underprovisioned spazio** colonna **archiviazione su disco disponibile** riflette hello quantità di spazio di archiviazione aggiuntivo è sufficiente. Utilizzare questo piano toohelp valore le esigenze di archiviazione per i backup smooth. Se il valore di hello è zero, non esistono alcun potenziali problemi di archiviazione in futuro hello. Se il valore di hello è un numero diverso da zero, non è sufficiente spazio di archiviazione allocato (basato su protezione hello e criteri di quelle dei dati dei membri protetti).

  ![Spazio di archiviazione su disco sottoallocato](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-7.png)

   toofinish la creazione di una procedura guidata hello completo, gruppo protezione dati.

## <a name="migrate-legacy-storage-toomodern-backup-storage"></a>Eseguire la migrazione archiviazione legacy tooModern archiviazione dei Backup
Dopo aver aggiornato tooor install v2 Server Backup e hello aggiornamento del sistema operativo tooWindows Server 2016, aggiornare il toouse di gruppi protezione dati moderni archiviazione dei Backup. Per impostazione predefinita, i gruppi protezione dati non vengono modificati. Continuano toofunction che sono stati inizialmente impostate. 

L'aggiornamento di gruppi di protezione toouse moderna archiviazione dei Backup è facoltativo. gruppo di protezione dati hello tooupdate, arrestare la protezione di tutte le origini dati utilizzando hello opzione di mantenimento dei dati. Aggiungere quindi hello dati origini tooa nuovo gruppo protezione dati.

1. Nella Console di amministrazione di hello, selezionare hello **protezione** funzionalità. In hello **membro del gruppo protezione dati** elenco, fare doppio clic su membro hello e quindi selezionare **Arresta protezione dati del membro**.

  ![Arresto della protezione del membro](http://docs.microsoft.com/system-center/dpm/media/upgrade-to-dpm-2016/dpm-2016-stop-protection1.png)

2. In hello **rimuovere dal gruppo** la finestra di dialogo, lo spazio su disco utilizzato hello di revisione e hello spazio disponibile per il pool di archiviazione hello. valore predefinito di Hello è tooleave hello punti di ripristino disco hello e consentire loro tooexpire per criteri di conservazione associati. Fare clic su **OK**.

  Se si desidera il pool di archiviazione disponibile toohello tooimmediately restituito hello utilizzato disco spazio, selezionare hello **Elimina replica su disco** dati di backup di casella di controllo toodelete hello (e i punti di ripristino) associata a tale membro.

  ![Rimozione dalla finestra di dialogo del gruppo](http://docs.microsoft.com/system-center/dpm/media/upgrade-to-dpm-2016/dpm-2016-retain-data.png)

3. Creare un gruppo protezione dati che usa Modern Backup Storage. Includere origini dati hello non protetto.


## <a name="add-disks-tooincrease-legacy-storage"></a>Aggiungere spazio di archiviazione dischi tooincrease legacy

Se si desidera toouse archiviazione legacy con il Server di Backup, si potrebbe essere necessario archiviazione legacy di tooadd dischi tooincrease. 

archiviazione su disco tooadd:

1. Nella Console di amministrazione di hello, selezionare **Management** > **archiviazione su disco** > **Aggiungi**.

    ![Finestra di dialogo Aggiungi spazio di archiviazione su disco](http://docs.microsoft.com/system-center/dpm/media/upgrade-to-dpm-2016/dpm-2016-add-disk-storage.png)

4. In hello **aggiungere archiviazione su disco** finestra di dialogo Seleziona **aggiungere dischi**.

5. Nell'elenco di hello dei dischi disponibili, selezionare i dischi di hello da tooadd, selezionare **Aggiungi**, quindi selezionare **OK**.

## <a name="update-hello-data-protection-manager-protection-agent"></a>Aggiornare l'agente protezione Data Protection Manager di hello

Backup Server Usa l'agente protezione di System Center Data Protection Manager hello per gli aggiornamenti. Se si sta aggiornando un agente protezione che non sia connessa toohello rete, è possibile utilizzare hello Console di amministrazione di Data Protection Manager toocomplete un aggiornamento dell'agente connesso. È necessario aggiornare l'agente protezione hello in un ambiente di dominio non attivo. Fino al computer client hello rete toohello connesso, Console di amministrazione di Data Protection Manager viene illustrato l'aggiornamento dell'agente protezione che hello hello è in sospeso.

Hello sezioni seguenti descrivono come tooupdate gli agenti di protezione per i computer client connessi e i computer client che non si è connessi.

### <a name="update-a-protection-agent-for-a-connected-client-computer"></a>Aggiornare un agente protezione per un computer client connesso

1. Nella Console di amministrazione di Server di Backup hello, selezionare **Management** > **agenti**.

2. Nel riquadro di visualizzazione hello, selezionare i computer client hello per cui si desidera l'agente di protezione tooupdate hello.

  > [!NOTE]
  > Hello **aggiornamenti agente** colonna indica quando un aggiornamento dell'agente protezione è disponibile per ogni computer protetto. In hello **azioni** riquadro, hello **aggiornamento** azione è disponibile solo quando è selezionato un computer protetto e sono disponibili aggiornamenti.
  >
  >

3. tooinstall aggiornare gli agenti protezione nei computer selezionato hello, hello **azioni** riquadro, selezionare **aggiornamento**.

### <a name="update-a-protection-agent-on-a-client-computer-that-is-not-connected"></a>Aggiornare un agente protezione in un computer client non connesso

1. Nella Console di amministrazione di Server di Backup hello, selezionare **Management** > **agenti**.

2. Nel riquadro di visualizzazione hello, selezionare i computer client hello per cui si desidera l'agente di protezione tooupdate hello.

  > [!NOTE]
   > Hello **aggiornamenti agente** colonna indica quando un aggiornamento dell'agente protezione è disponibile per ogni computer protetto. In hello **azioni** riquadro, hello **aggiornamento** azione non è disponibile quando si seleziona un computer protetto, a meno che non sono disponibili aggiornamenti.
  >
  >

3. tooinstall aggiornare gli agenti protezione nei computer hello selezionato, selezionare **aggiornamento**.

4. Per un computer client che non è connesso rete toohello, fino al computer hello rete toohello connesso, hello **lo stato dell'agente** colonna viene visualizzato lo stato **aggiornamento in sospeso**.

  Dopo che un computer client è connesso toohello dalla rete, hello **aggiornamenti agente** colonna per i computer client hello viene visualizzato lo stato **aggiornamento**.
  
### <a name="move-legacy-protection-groups-from-old-version-and-sync-hello-new-version-with-azure"></a>Spostare i gruppi protezione dati legacy da precedente e la nuova versione hello sincronizzazione con Azure

Una volta che vengono aggiornati sia il Server di Backup di Azure e hello del sistema operativo, si è pronti tooprotect nuove origini dati mediante spazio di memorizzazione Backup moderne. Origini dati, tuttavia è già protetto continuerà toobe protette hello legacy modo come fossero nel Server di Backup di Azure, ma tutti nuovo gruppo protezione dati utilizzerà moderna archiviazione dei Backup.

I passaggi successivi sono origini dati toomigrate dalla modalità legacy protezione tooModern archiviazione di backup.

• Aggiungere hello nuovi volumi toohello pool di archiviazione DPM e assegnare i tag di origine di dati e i nomi descrittivi se lo si desidera.
• Per ogni origine dati che è in modalità legacy, arresta la protezione delle origini dati hello e "Mantieni dati protetti".  Questo permetterà il ripristino dei vecchi punti di recupero dopo la migrazione.

• Creare un nuovo gruppo protezione dati e selezionare le origini dati hello che sono toobe memorizzati nel nuovo formato.
• DPM eseguirà una copia della replica di archiviazione dei backup legacy hello in hello volume di archiviazione di Backup più recenti in locale.
Nota: questo verrà considerato un processo dell'operazione successiva al ripristino • Tutti i nuovi punti di sincronizzazione e recupero verranno quindi archiviati nell'archiviazione dei backup moderna.
• Vecchi punti di ripristino saranno eliminati che sono in scadenza e alla fine di liberare spazio su disco hello.
• Dopo tutti i volumi legacy hello vengono eliminati dalla risorsa di archiviazione precedente hello, disco hello possono essere rimossi dal sistema di backup e hello Azure.
• Eseguire un backup di hello Azure DPMDB.

Parte 2:-elementi importanti > hello nuovo server dovrà essere toobe denominato stesso come server di Backup di Azure originale hello. Non è possibile modificare il nome di hello del server di backup Azure nuovo hello se si desidera toouse precedente pool di archiviazione e i punti di ripristino tooretain DPMDB - deve avere il backup di DPMDB sarà necessario ripristinare toobe

1) Arresto hello server di backup di Azure originale o portarlo off transito hello.
2) Reimpostare l'account del computer hello in active directory.
3) Installare Server 2016 nel nuovo computer e il nome hello stesso nome di computer come server di Backup di Azure originale hello.
4) Creare un join hello dominio
5) Installare il server di Backup di Azure V2 (spostare i dischi del pool di archiviazione DPM dal vecchio server ed eseguire l'importazione)
6) Ripristinare hello DPMDB eseguita dalla fine della parte 2
7) Collega archiviazione hello da hello originale backup toohello nuovo server.
8) Dal ripristino di SQL hello DPMDB
9) Dalla riga di comando di amministratore nel nuovo server cd tooMicrosoft Backup di Azure installare posizione e la cartella bin

Esempio di percorso: C:\windows\system32>cd "c:\Programmi\Microsoft Azure Backup\DPM\DPM\bin\"
backup tooAzure eseguire DPMSYNC-SYNC

10) Eseguire DPMSYNC-SYNC Nota Se è stato aggiunto nuovo pool di archiviazione di DPM toohello dischi anziché spostare hello quelle meno recenti, quindi eseguire DPMSYNC - Reallocatereplica

## <a name="new-powershell-cmdlets-in-v2"></a>Nuovi cmdlet PowerShell della v2

Quando si installa il server di Backup di Azure v2, sono disponibili due nuovi cmdlet: 
* [Mount-DPMRecoveryPoint](https://technet.microsoft.com/library/mt787159.aspx)
* [Dismount-DPMRecoveryPoint](https://technet.microsoft.com/library/mt787158.aspx)

## <a name="next-steps"></a>Passaggi successivi

Informazioni su come tooprepare il server o iniziare a proteggere un carico di lavoro:
- [Preparare i carichi di lavoro del server di backup](backup-azure-microsoft-azure-backup.md)
- [Utilizzare tooback Server di Backup di un server VMware](backup-azure-backup-server-vmware.md)
- [Usare Backup Server tooback verticale di SQL Server](backup-azure-sql-mabs.md)
- [Usare Modern Backup Storage con il server di backup](backup-mabs-add-storage.md)

