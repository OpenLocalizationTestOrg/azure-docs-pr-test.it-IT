---
title: aaaStorSimple volumi e gestione Snapshot | Documenti Microsoft
description: Viene descritto come toouse hello tooview snap-in MMC di StorSimple Snapshot Manager e gestire volumi e backup tooconfigure.
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 78896323-e57c-431e-bbe2-0cbde1cf43a2
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 04/18/2016
ms.author: v-sharos
ms.openlocfilehash: b8ce102d082b7c773d667a9d3ec747be9e1d3064
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-tooview-and-manage-volumes"></a>Utilizzare Gestione Snapshot StorSimple tooview e gestire volumi
## <a name="overview"></a>Panoramica
È possibile usare Gestione Snapshot StorSimple hello **volumi** nodo (in hello **ambito** riquadro) tooselect volumi e visualizzare le relative informazioni. Hello volumi vengono presentati come unità che corrispondono toohello volumi montati dall'host hello. Hello **volumi** nodo vengono mostrati i volumi locali e tipi di volume supportati da StorSimple, ad esempio volumi individuati tramite l'utilizzo di hello di iSCSI e un dispositivo. 

Per ulteriori informazioni sui volumi supportati, visitare troppo[il supporto per più tipi di volume](storsimple-what-is-snapshot-manager.md#support-for-multiple-volume-types).

![Elenco volumi nel riquadro dei Risultati](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Volume_node.png)

Hello **volumi** nodo consente inoltre di eseguire nuovamente la scansione o eliminare i volumi dopo li individua gestione Snapshot StorSimple. 

Questo tutorial spiega come montare, inizializzare e formattare volumi e quindi usare StorSimple Snapshot Manager per:

* Visualizzare informazioni sui volumi 
* Eliminare volumi
* Ripetere la scansione dei volumi 
* Configurare un volume di base e una copia di backup
* Configurare un volume con mirroring dinamico e una copia di backup

> [!NOTE]
> Tutti i hello **Volume** nodo sono inoltre disponibili nelle azioni hello **azioni** riquadro.
> 
> 

## <a name="mount-volumes"></a>Montare i volumi
Hello utilizzare seguendo procedure toomount, inizializzare e formattare volumi StorSimple. Questa procedura utilizza Gestione disco, un'utilità di sistema per la gestione dei dischi rigidi e i volumi corrispondenti hello o partizioni. Per ulteriori informazioni su Gestione disco, andare troppo[Gestione disco](https://technet.microsoft.com/library/cc770943.aspx) nel sito Web Microsoft TechNet hello.

#### <a name="toomount-volumes"></a>volumi toomount
1. Nel computer host avviare l'iniziatore iSCSI Microsoft di hello.
2. Specificare uno degli indirizzi IP dell'interfaccia di hello come portale destinazione hello o indirizzo IP di individuazione e connettere il dispositivo toohello. Dopo aver hello dispositivo è connesso, volumi hello sarà accessibile tooyour sistema di Windows. Per ulteriori informazioni sull'uso dell'iniziatore iSCSI Microsoft di hello, visitare toohello sezione "Connessione tooan dispositivo di destinazione iSCSI" in [installazione e configurazione iniziatore iSCSI Microsoft][1].
3. Utilizzare una delle seguenti opzioni toostart Gestione disco hello:
   
   * Digitare Diskmgmt.msc hello **eseguire** casella.
   * Avviare Server Manager, espandere hello **archiviazione** nodo e quindi selezionare **Gestione disco**.
   * Avviare **strumenti di amministrazione**, espandere hello **Gestione Computer** nodo e quindi selezionare **Gestione disco**. 
     
     > [!NOTE]
     > È necessario utilizzare i privilegi di amministratore toorun Gestione disco.
     > 
     > 
4. Eseguire uno o più volumi hello online:
   
   1. In Gestione disco, fare doppio clic su un volume contrassegnato **Offline**.
   2. Scegliere **Riattiva disco specificato**. deve essere contrassegnato come disco Hello **Online** dopo disco hello viene riattivato.
5. Inizializzare i volumi di hello:
   
   1. Fare doppio clic su volumi hello individuato.
   2. Selezionare menu hello **Inizializza disco**.
   3. In hello **Inizializza disco** della finestra di dialogo dischi selezionare hello che desidera tooinitialize e quindi fare clic su **OK**.
6. Formattare volumi semplici:
   
   1. Fare doppio clic su un volume che si desidera tooformat.
   2. Selezionare menu hello **nuovo Volume semplice**.
   3. Utilizzare il volume hello tooformat di hello nuovo Volume semplice procedura guidata:
      
      * Specificare la dimensione del volume hello.
      * Specificare una lettera di unità.
      * Selezionare file system NTFS hello.
      * Specificare una dimensione unità di allocazione pari a 64 KB.
      * Eseguire una formattazione veloce.
7. Formattare volumi con più partizioni. Per istruzioni, vedere la sezione toohello, "Partizioni e volumi" in [implementazione di Gestione disco](https://msdn.microsoft.com/library/dd163556.aspx).

## <a name="view-information-about-your-volumes"></a>Visualizzare informazioni sui volumi
Utilizzare le seguenti procedure tooview informazioni sulle locale e sui volumi StorSimple di Azure hello.

#### <a name="tooview-volume-information"></a>informazioni sul volume tooview
1. Fare clic su hello icona sul desktop toostart gestione Snapshot StorSimple. 
2. In hello **ambito** riquadro, fare clic su hello **volumi** nodo. Viene visualizzato un elenco di volumi locali e montati, inclusi tutti i volumi StorSimple di Azure, in hello **risultati** riquadro. Hello colonne hello **risultati** riquadro sono configurabili. (Hello rapida **volumi** nodo, seleziona **vista**, quindi selezionare **Aggiungi/Rimuovi colonne**.)
   
    ![Configurare le colonne di hello](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_View_volumes.png)
   
   | Colonna risultati | Descrizione |
   |:--- |:--- |
   |  Nome |Hello **nome** colonna contiene volume tooeach individuati lettera di unità hello. |
   |  Dispositivo |Hello **dispositivo** colonna contiene l'indirizzo IP di hello del computer host di hello dispositivo toohello connesso. |
   |  Nome Dispositivo Volume |Hello **nome Volume dispositivo** colonna contiene il nome di hello di hello dispositivo volume toowhich hello selezionata appartiene volume. Questo è il nome di volume hello definito nel portale di Azure per il volume specifico hello. |
   |  Percorsi di accesso |Hello **percorsi di accesso** colonna Visualizza hello accesso percorso toohello volume. Si tratta di hello unità lettera o punto di montaggio in cui hello volume sia accessibile nel computer host hello. |

## <a name="delete-a-volume"></a>Eliminare un volume
Utilizzare hello seguendo procedure toodelete un volume da StorSimple Snapshot Manager.

> [!NOTE]
> Non è possibile eliminare un volume se fa parte di un gruppo di volumi. (opzione di eliminazione hello non è disponibile per i volumi che sono membri di un gruppo di volumi.) È necessario eliminare il volume hello toodelete di hello volume intero gruppo.

#### <a name="toodelete-a-volume"></a>toodelete un volume
1. Fare clic su hello icona sul desktop toostart gestione Snapshot StorSimple.
2. In hello **ambito** riquadro, fare clic su hello **volumi** nodo. 
3. In hello **risultati** riquadro, volume hello rapida che si desidera toodelete.
4. Scegliere dal menu hello **eliminare**. 
   
    ![Eliminare un volume](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Delete_volume.png) 
5. Hello **Elimina Volume** viene visualizzata la finestra di dialogo. Tipo **conferma** in hello casella di testo e quindi fare clic su **OK**.
6. Come impostazione predefinita, StorSimple Snapshot Manager esegue il backup di un volume prima di eliminarlo. Questa precauzione consente di evitare la perdita di dati se l'eliminazione di hello sia stata non intenzionale. Gestione Snapshot StorSimple consente di visualizzare un **Snapshot automatico** messaggio di stato durante l'esecuzione del backup volume hello. 
   
    ![Messaggio di snapshot automatico](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Automatic_snap.png) 

## <a name="rescan-volumes"></a>Ripetere la scansione dei volumi
Utilizzare hello seguendo procedure toorescan hello volumi connessi tooStorSimple gestione Snapshot.

#### <a name="toorescan-hello-volumes"></a>volumi hello toorescan
1. Fare clic su hello icona sul desktop toostart gestione Snapshot StorSimple.
2. In hello **ambito** riquadro destro **volumi**, quindi fare clic su **Ripeti analisi dei volumi**.
   
    ![Ripetere la scansione dei volumi](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Rescan_volumes.png)
   
    Questa procedura Sincronizza l'elenco dei volumi hello con StorSimple Snapshot Manager. Si rifletteranno le modifiche, ad esempio volumi nuovi o eliminati, nei risultati di hello.

## <a name="configure-and-back-up-a-basic-volume"></a>Configurare ed eseguire il backup di un volume di base
Utilizzare hello seguendo procedure tooconfigure un backup di un volume di base, quindi avviare immediatamente un backup o creare un criterio per i backup pianificati.

### <a name="prerequisites"></a>Prerequisiti
Prima di iniziare:

* Assicurarsi che il dispositivo StorSimple hello e computer host siano configurati correttamente. Per ulteriori informazioni, visitare troppo[distribuire il dispositivo StorSimple locale](storsimple-deployment-walkthrough-u2.md).
* Installare e configurare Snapshot StorSimple Manager. Per ulteriori informazioni, visitare troppo[distribuire StorSimple Snapshot Manager](storsimple-snapshot-manager-deployment.md).

#### <a name="tooconfigure-backup-of-a-basic-volume"></a>tooconfigure backup di un volume di base
1. Creare un volume di base nel dispositivo StorSimple hello.
2. Montare, inizializzare e formattare il volume di hello, come descritto in [montare i volumi](#mount-volumes). 
3. Fare clic sull'icona di gestione Snapshot StorSimple hello sul desktop. verrà visualizzata la finestra di gestione Snapshot StorSimple Hello. 
4. In hello **ambito** riquadro, hello rapida **volumi** nodo e quindi selezionare **Ripeti analisi dei volumi**. Al termine dell'analisi di hello, un elenco di volumi deve essere visualizzato in hello **risultati** riquadro. 
5. In hello **risultati** riquadro volume hello e quindi scegliere **Crea gruppo di volumi**. 
   
    ![Crea gruppo di volumi](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Create_volume_group.png) 
6. In hello **Crea gruppo di volumi** nella finestra di dialogo digitare un nome per il gruppo di volumi di hello, assegnare tooit volumi e quindi fare clic su **OK**.
7. In hello **ambito** riquadro espandere hello **gruppi di volumi** nodo. nuovo gruppo di volumi Hello dovrebbe essere visualizzato sotto hello **gruppi di volumi** nodo. 
8. Fare clic sul nome del gruppo di volumi hello.
   
   * Fare clic su un processo interattivo di backup (su richiesta), toostart **Esegui Backup**. 
   * Fare clic su un backup automatico, tooschedule **Crea criteri di Backup**. In hello **generale** pagina, selezionare un gruppo di volumi dall'elenco di hello. In hello **pianificazione** pagina, immettere i dettagli della pianificazione hello. Al termine, fare clic su **OK**. 
9. tooconfirm che hello processo di backup è stato avviato, espandere hello **processi** nodo hello **ambito** riquadro, quindi fare clic su hello **esecuzione** nodo. viene visualizzato l'elenco di Hello di processi in esecuzione in hello **risultati** riquadro. 

## <a name="configure-and-back-up-a-dynamic-mirrored-volume"></a>Configurare ed eseguire il backup di un volume con mirroring dinamico
Completare hello successivo backup tooconfigure passaggi di un volume con mirroring dinamico:

* Passaggio 1: Utilizzare Gestione disco toocreate un volume con mirroring dinamico. 
* Passaggio 2: Tooconfigure usare Gestione Snapshot StorSimple backup.

### <a name="prerequisites"></a>Prerequisiti
Prima di iniziare:

* Assicurarsi che il dispositivo StorSimple hello e computer host siano configurati correttamente. Per ulteriori informazioni, visitare troppo[distribuire il dispositivo StorSimple locale](storsimple-8000-deployment-walkthrough-u2.md).
* Installare e configurare Snapshot StorSimple Manager. Per ulteriori informazioni, visitare troppo[distribuire StorSimple Snapshot Manager](storsimple-snapshot-manager-deployment.md).
* Configurare due volumi nel dispositivo StorSimple hello. (Negli esempi di hello, sono disponibili volumi di hello **disco 1** e **disco 2**.) 

### <a name="step-1-use-disk-management-toocreate-a-dynamic-mirrored-volume"></a>Passaggio 1: Utilizzare Gestione disco toocreate un volume con mirroring dinamico
Gestione disco è un'utilità di sistema per la gestione dei dischi rigidi e i volumi di hello o partizioni in essi contenuti. Per ulteriori informazioni su Gestione disco, andare troppo[Gestione disco](https://technet.microsoft.com/library/cc770943.aspx) nel sito Web Microsoft TechNet hello.

#### <a name="toocreate-a-dynamic-mirrored-volume"></a>toocreate un volume con mirroring dinamico
1. Utilizzare una delle seguenti opzioni toostart Gestione disco hello: 
   
   * Aprire hello **eseguire** digitare **Diskmgmt.msc**, e premere INVIO.
   * Avviare Server Manager, espandere hello **archiviazione** nodo e quindi selezionare **Gestione disco**. 
   * Avviare **strumenti di amministrazione**, espandere hello **Gestione Computer** nodo e quindi selezionare **Gestione disco**. 
2. Assicurarsi di disporre di due volumi disponibili nel dispositivo StorSimple hello. (Nell'esempio hello sono volumi disponibili hello **disco 1** e **disco 2**.) 
3. Nella finestra Gestione disco hello, nella colonna a destra del riquadro inferiore hello, hello destro **disco 1** e selezionare **nuovo Volume con mirroring**. 
   
    ![Nuovo volume con mirroring](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_New_mirrored_volume.png) 
4. In hello **nuovo Volume con mirroring** pagina della procedura guidata, fare clic su **Avanti**.
5. In hello **Seleziona dischi** selezionare **disco 2** in hello **selezionati** riquadro, fare clic su **Aggiungi**e quindi fare clic su **Avanti**. 
6. In hello **Assegna lettera di unità o percorso** pagina, accettare le impostazioni predefinite hello e quindi fare clic su **Avanti**. 
7. In hello **formatta Volume** pagina hello **dimensioni unità di allocazione** , quindi selezionare **64K**. Seleziona hello **eseguire una formattazione veloce** casella di controllo e quindi fare clic su **Avanti**. 
8. In hello **completamento hello nuovo Volume con mirroring** pagina, rivedere le impostazioni e quindi fare clic su **fine**. 
9. Viene visualizzato un messaggio tooindicate che hello disco di base sarà convertito tooa disco dinamico. Fare clic su **Sì**.
   
    ![Messaggi di conversione del disco dinamico](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Disk_management_msg.png) 
10. In Gestione disco, verificare che Disco 1 e Disco 2 vengano visualizzati come volumi con mirroring dinamico. (**Dinamica** dovrebbe essere visualizzato nella colonna Stato hello e colore della barra di capacità hello debba modificare toored, indicare un volume con mirroring.) 
    
    ![Dischi dinamici con mirroring di Gestione disco](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Verify_dynamic_disks_2.png) 

### <a name="step-2-use-storsimple-snapshot-manager-tooconfigure-backup"></a>Passaggio 2: Usare Gestione Snapshot StorSimple tooconfigure backup
Utilizzare hello seguendo procedure tooconfigure un volume con mirroring dinamico, quindi avviare immediatamente un backup o creare un criterio per i backup pianificati.

#### <a name="tooconfigure-backup-of-a-dynamic-mirrored-volume"></a>tooconfigure backup di un volume con mirroring dinamico
1. Fare clic sull'icona di gestione Snapshot StorSimple hello sul desktop. verrà visualizzata la finestra di gestione Snapshot StorSimple Hello. 
2. In hello **ambito** riquadro, hello rapida **volumi** nodo e selezionare **Ripeti analisi dei volumi**. Al termine dell'analisi di hello, un elenco di volumi deve essere visualizzato in hello **risultati** riquadro. volume con mirroring dinamico Hello è elencato come un singolo volume. 
3. In hello **risultati** riquadro destro volume con mirroring dinamico hello e quindi fare clic su **Crea gruppo di volumi**. 
4. In hello **Crea gruppo di volumi** nella finestra di dialogo digitare un nome per il gruppo di volumi hello assegnare hello volume con mirroring dinamico toothis gruppo e quindi fare clic su **OK**. 
5. In hello **ambito** riquadro espandere hello **gruppi di volumi** nodo. nuovo gruppo di volumi Hello dovrebbe essere visualizzato sotto hello **gruppi di volumi** nodo. 
6. Fare clic sul nome del gruppo di volumi hello. 
   
   * Fare clic su un processo interattivo di backup (su richiesta), toostart **Esegui Backup**. 
   * Fare clic su un backup automatico, tooschedule **Crea criteri di Backup**. In hello **generale** pagina, il gruppo di volumi hello selezionare dall'elenco di hello. In hello **pianificazione** pagina, immettere i dettagli della pianificazione hello. Al termine, fare clic su **OK**. 
7. È possibile monitorare i processi di backup hello mentre è in esecuzione. In hello **ambito** riquadro espandere hello **processi** nodo e quindi fare clic su **esecuzione**, vengono visualizzati i dettagli dei processi hello in hello **risultati** riquadro. Termine del processo di backup hello, dettagli hello vengono trasferito toohello **ultime 24** ore di lavoro elenco. 

## <a name="next-steps"></a>Passaggi successivi
* Informazioni su come troppo[usare Gestione Snapshot StorSimple tooadminister la soluzione StorSimple](storsimple-snapshot-manager-admin.md).
* Informazioni su come troppo[toocreate StorSimple Snapshot Manager di utilizzare e gestire gruppi di volumi](storsimple-snapshot-manager-manage-volume-groups.md).

<!--Reference links-->
[1]: https://msdn.microsoft.com/library/ee338480(v=ws.10).aspx
