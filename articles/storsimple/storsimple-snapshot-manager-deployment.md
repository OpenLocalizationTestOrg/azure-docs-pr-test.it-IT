---
title: Gestione Snapshot StorSimple aaaDeploy | Documenti Microsoft
description: "Informazioni su come toodownload e installare hello StorSimple Snapshot Manager, uno snap-in MMC per la gestione delle funzionalità di protezione e il backup dei dati di StorSimple."
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: f0128f57-519e-49ec-9187-23575809cdbe
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: dd90cca2bbb3410bb8cd459fb1a3ff3fb5f2997b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-storsimple-snapshot-manager-mmc-snap-in"></a>Distribuire hello snap-in MMC di StorSimple Snapshot Manager

## <a name="overview"></a>Panoramica
Hello StorSimple Snapshot Manager è uno snap-in Microsoft Management Console (MMC) che semplifica la protezione dei dati e la gestione dei backup in un ambiente di Microsoft Azure StorSimple. Con StorSimple Snapshot Manager è possibile gestire Microsoft Azure StorSimple in locale e archiviare nella cloud come se fosse un sistema di archiviazione completamente integrato, semplificando i processi di backup e ripristino e riducendo i costi di conseguenza. 

In questa esercitazione vengono descritti i requisiti di configurazione, nonché le procedure per installare, rimuovere e aggiornare StorSimple Snapshot Manager.

> [!NOTE]
> * Non è possibile utilizzare toomanage gestione Snapshot StorSimple Microsoft Azure StorSimple Virtual Array (noto anche come StorSimple locale dispositivi virtuali).
> * Se si intende il dispositivo StorSimple tooinstall StorSimple Update 2, che toodownload hello versione più recente di StorSimple Snapshot Manager e installarlo **prima di installare l'aggiornamento 2 di StorSimple**. la versione più recente Hello di StorSimple Snapshot Manager è compatibile con le versioni precedenti e funziona con tutte le versioni rilasciate di Microsoft Azure StorSimple. Se si utilizza una versione precedente di hello di StorSimple Snapshot Manager, sarà necessario tooupdate it (non è necessario versione precedente di hello toouninstall prima di installare una nuova versione di hello).


## <a name="storsimple-snapshot-manager-installation"></a>Installazione di StorSimple Snapshot Manager
Gestione Snapshot StorSimple può essere installato nei computer che eseguono il sistema operativo Windows Server 2008 R2 SP1, Windows Server 2012 o Windows Server 2012 R2 di hello. Nei server che eseguono Windows 2008 R2, è necessario installare Windows Server 2008 SP1 e Windows Management Framework 3.0.

Prima di installare o aggiornare hello gestione Snapshot StorSimple snap-in per hello Microsoft Management Console (MMC), assicurarsi che il dispositivo di Microsoft Azure StorSimple hello e server host siano configurati correttamente.

## <a name="configure-prerequisites"></a>Configurazione dei prerequisiti
Hello seguenti passaggi forniscono una panoramica generale delle attività di configurazione che è necessario completare prima di installare Gestione Snapshot StorSimple hello. Per informazioni complete sulla configurazione  e sull’installazione di Microsoft Azure StorSimple, inclusi i requisiti di sistema e istruzioni dettagliate, vedere [Distribuire dispositivo StorSimple in locale](storsimple-8000-deployment-walkthrough-u2.md).

> [!IMPORTANT]
> Prima di iniziare, esaminare hello [elenco di controllo configurazione distribuzione](storsimple-8000-deployment-walkthrough-u2.md#deployment-configuration-checklist) ed e [prerequisiti di distribuzione](storsimple-8000-deployment-walkthrough-u2.md#deployment-prerequisites) in [distribuire il dispositivo StorSimple locale](storsimple-8000-deployment-walkthrough-u2.md).
> <br>
> 
> 

### <a name="before-you-install-storsimple-snapshot-manager"></a>Prima di installare StorSimple Snapshot Manager
1. Disimballare, montare e collegare il dispositivo di Microsoft Azure StorSimple hello, come descritto in [installare il dispositivo StorSimple 8100](storsimple-8100-hardware-installation.md) o [installare del dispositivo 8600 StorSimple](storsimple-8600-hardware-installation.md).
2. Assicurarsi che il computer host è in esecuzione uno dei seguenti sistemi operativi hello:
   
   * Windows Server 2008 R2 (nei server che eseguono Windows 2008 R2, è necessario inoltre installare Windows Server 2008 SP1 e Windows Management Framework 3.0)
   * Windows Server 2012
   * Windows Server 2012 R2
     
     Per un dispositivo virtuale StorSimple, host di hello deve essere una macchina virtuale di Microsoft Azure.
3. Verificare che siano soddisfatti tutti i requisiti di configurazione di Microsoft Azure StorSimple hello. Per informazioni dettagliate, vedere troppo[prerequisiti di distribuzione](storsimple-8000-deployment-walkthrough-u2.md#deployment-prerequisites).
4. Connetti l'host di toohello hello dispositivo ed eseguire la configurazione iniziale di hello. Per informazioni dettagliate, vedere troppo[passaggi di distribuzione](storsimple-8000-deployment-walkthrough-u2.md#deployment-steps).
5. Creare i volumi nel dispositivo hello, assegnarli toohello host e verificare che ospitano hello possibile montare e utilizzarli. Gestione Snapshot StorSimple supporta i seguenti tipi di volumi hello:
   
   * Volumi di base
   * Volumi semplici
   * Volumi dinamici
   * Volumi dinamici con mirroring (RAID 1)
   * Volumi condivisi del cluster
     
     Per informazioni sulla creazione di volumi nel dispositivo StorSimple hello o un dispositivo virtuale StorSimple, andare troppo[passaggio 6: creare un volume](storsimple-8000-deployment-walkthrough-u2.md#step-6-create-a-volume)nella [distribuire il dispositivo StorSimple locale](storsimple-8000-deployment-walkthrough-u2.md).

## <a name="install-a-new-storsimple-snapshot-manager"></a>Installare un nuovo StorSimple Snapshot Manager
Prima di installare Gestione Snapshot StorSimple, assicurarsi che i volumi di hello creato nel dispositivo StorSimple hello o un dispositivo virtuale StorSimple sono montati, inizializzati e formattati come descritto in [configurare i prerequisiti](#configure-prerequisites).

> [!IMPORTANT]
> * Per un dispositivo virtuale StorSimple, host di hello deve essere una macchina virtuale di Microsoft Azure. 
> * Hello host deve eseguire Windows 2008 R2, Windows Server 2012 o Windows Server 2012 R2. Se il server esegue Windows Server 2008 R2, è necessario installare anche Windows Server 2008 SP1 e Windows Management Framework 3.0.
> * È necessario configurare una connessione iSCSI dal dispositivo StorSimple toohello di hello host prima di poter connettere hello dispositivo tooStorSimple gestione Snapshot.

Seguire questi toocomplete passaggi una nuova installazione di StorSimple Snapshot Manager. Se si sta installando un aggiornamento, andare troppo[aggiornare o reinstallare Gestione Snapshot StorSimple](#upgrade-or-reinstall-storsimple-snapshot-manager).

* Passaggio 1: Installare StorSimple Snapshot Manager 
* Passaggio 2: Connettere il dispositivo di StorSimple Snapshot Manager tooa 
* Passaggio 3: Verificare dispositivo toohello di hello connessione 

### <a name="step-1-install-storsimple-snapshot-manager"></a>Passaggio 1: Installare StorSimple Snapshot Manager
Utilizzare hello seguendo i passaggi tooinstall gestione Snapshot StorSimple.

#### <a name="tooinstall-storsimple-snapshot-manager"></a>tooinstall gestione Snapshot StorSimple
1. Scaricare il software di gestione Snapshot StorSimple hello (andare troppo[gestione Snapshot StorSimple](https://www.microsoft.com/download/details.aspx?id=44220) nel Microsoft Download Center hello) e salvarlo in locale nell'host di hello.
2. In Esplora File, fare clic sulla cartella compressa hello e quindi fare clic su **estrarre tutti**.
3. In hello **cartelle estrarre compresse** finestra hello **selezionare una destinazione ed estrarre file** digitare o individuare il percorso di toohello in cui si desidera toobe toofile estratti.
   
    > [!IMPORTANT]
    > È necessario installarvi l'unità c: hello gestione Snapshot StorSimple.
    
4. Seleziona hello **Mostra estratti al termine dell'operazione** casella di controllo e quindi fare clic su **estrarre**.
   
    ![Estrarre la finestra di dialogo file](./media/storsimple-snapshot-manager-deployment/HCS_SSM_extract_files.png) 
5. Al termine dell'estrazione hello, verrà visualizzata la cartella di destinazione hello. Fare doppio clic sull'icona di programma di installazione applicazione hello che viene visualizzato nella cartella di destinazione hello.
6. Quando hello **installazione completata** messaggio viene visualizzato, fare clic su **Chiudi**. Icona di StorSimple Snapshot Manager hello dovrebbe essere sul desktop.
   
    ![icona del desktop](./media/storsimple-snapshot-manager-deployment/HCS_SSM_desktop_icon.png) 

### <a name="step-2-connect-storsimple-snapshot-manager-tooa-device"></a>Passaggio 2: Connettere il dispositivo di StorSimple Snapshot Manager tooa
Utilizzare hello seguendo i passaggi tooconnect dispositivo StorSimple tooa gestione Snapshot StorSimple.

#### <a name="tooconnect-storsimple-snapshot-manager-tooa-device"></a>dispositivo StorSimple Snapshot Manager tooa tooconnect
1. Fare clic sull'icona di gestione Snapshot StorSimple hello sul desktop. verrà visualizzata la finestra di gestione Snapshot StorSimple Hello. finestra Hello contiene un **ambito** riquadro un **risultati** riquadro e un **azioni** riquadro. 
   
    ![Interfaccia utente di StorSimple Snapshot Manager](./media/storsimple-snapshot-manager-deployment/HCS_SSM_gui_panes.png)
   
   * Hello **ambito** riquadro (hello a sinistra) contiene un elenco di nodi organizzati in una struttura ad albero. È possibile espandere alcuni nodi tooselect una vista o un nodo di dati specifici correlati toothat. Fare clic su hello freccia icona tooexpand o comprimere un nodo. Fare doppio clic su un elemento in hello **ambito** riquadro toosee un elenco di azioni disponibili per quell'elemento.
   * Hello **risultati** riquadro (riquadro centrale hello) contiene informazioni dettagliate sullo stato nodo hello, vista o i dati selezionati in hello **ambito** riquadro.
   * Hello **azioni** riquadro Elenca le operazioni di hello che è possibile eseguire nel nodo hello, vista o i dati selezionati in hello **ambito** riquadro.
     
     Per una descrizione completa dell'interfaccia utente di gestione Snapshot StorSimple hello, vedere [interfaccia utente di gestione Snapshot StorSimple](storsimple-use-snapshot-manager.md).
2. In hello **ambito** riquadro, hello rapida **dispositivi** nodo e quindi fare clic su **configurare un dispositivo**. Hello **configurare un dispositivo** viene visualizzata la finestra di dialogo.
   
    ![Configura un dispositivo](./media/storsimple-snapshot-manager-deployment/HCS_SSM_config_device.png) 
3. In hello **dispositivo** elenco casella, l'indirizzo IP di hello selezionare del dispositivo di Microsoft Azure StorSimple hello o del dispositivo virtuale. In hello **Password** casella di testo, la password di StorSimple Snapshot Manager hello tipo creato per il dispositivo di hello in hello portale di Azure. Fare clic su **OK**.
4. Gestione Snapshot StorSimple Cerca dispositivi hello identificato. Se il dispositivo hello è disponibile, gestione Snapshot StorSimple aggiunge una connessione. È possibile [verificare dispositivo toohello di connessione hello](#to-verify-the-connection) tooconfirm che hello connessione è stato aggiunto correttamente.
   
    Se il dispositivo hello è disponibile per qualsiasi motivo, gestione Snapshot StorSimple restituisce un messaggio di errore. Fare clic su **OK** tooclose hello messaggio di errore e quindi fare clic su **Annulla** tooclose hello **configurare un dispositivo** la finestra di dialogo.
5. Quando si connette il dispositivo tooa, StorSimple Snapshot Manager Importa ogni gruppo di volumi configurato per il dispositivo, purché hello volume gruppi abbiano backup associati. I gruppi di volumi che non dispongono di backup associati non vengono importati. Inoltre, non vengono importati i criteri di backup creati per un gruppo di volumi. toosee hello gruppi importati, fare doppio clic su hello superiore **gruppi di volumi** nodo hello **ambito** riquadro e fare clic su **attivare o disattivare i gruppi importati**.

### <a name="step-3-verify-hello-connection-toohello-device"></a>Passaggio 3: Verificare dispositivo toohello di hello connessione
Utilizzare hello seguendo i passaggi tooverify che Gestione Snapshot StorSimple è dispositivo StorSimple toohello connesso.

#### <a name="tooverify-hello-connection"></a>connessione hello tooverify
1. In hello **ambito** riquadro, fare clic su hello **dispositivi** nodo.
   
    ![Stato del dispositivo StorSimple Snapshot Manager](./media/storsimple-snapshot-manager-deployment/HCS_SSM_Device_status.png) 
2. Controllare hello **risultati** riquadro: 
   
   * Se viene visualizzato un indicatore verde sull'icona di dispositivo hello e **disponibile** viene visualizzato in hello **stato** colonna, quindi dispositivo hello è connesso. 
   * Se viene visualizzato un indicatore rosso sull'icona di dispositivo hello e non disponibile viene visualizzata in hello **stato** colonna, quindi dispositivo hello non è connesso. 
   * Se **aggiornamento** viene visualizzato in hello **stato** colonna, quindi StorSimple Snapshot Manager sta recuperando i gruppi di volumi e i relativi backup per un dispositivo connesso.

## <a name="upgrade-or-reinstall-storsimple-snapshot-manager"></a>Aggiorna o reinstalla StorSimple Snapshot Manager
È necessario disinstallare Gestione Snapshot StorSimple completamente prima di aggiornare o reinstallare il software di hello. 

Prima di reinstallare Gestione Snapshot StorSimple, eseguire il backup hello database di gestione Snapshot StorSimple esistente nel computer host hello. Questo Salva informazioni di configurazione e i criteri di backup hello in modo che è possibile ripristinare facilmente i dati dal backup.

Se si aggiorna o reinstalla StorSimple Snapshot Manager, attenersi alla seguente procedura:

* Passaggio 1: Disinstallare StorSimple Snapshot Manager 
* Passaggio 2: Eseguire il backup del database di gestione Snapshot StorSimple hello 
* Passaggio 3: Reinstallare Gestione Snapshot StorSimple e ripristinare i database di hello 

### <a name="step-1-uninstall-storsimple-snapshot-manager"></a>Passaggio 1: Disinstallare StorSimple Snapshot Manager
Utilizzare hello seguendo i passaggi toouninstall gestione Snapshot StorSimple.

#### <a name="toouninstall-storsimple-snapshot-manager"></a>toouninstall gestione Snapshot StorSimple
1. Nel computer host hello aprire hello **Pannello di controllo**, fare clic su **programmi**, quindi fare clic su **programmi e funzionalità**.
2. Nel riquadro di sinistra hello, fare clic su **Disinstalla o modifica programma**.
3. Fare clic con il pulsante destro del mouse su **StorSimple Snapshot Manager**, quindi fare clic su **Disisntalla**.
4. Verrà avviato il programma di installazione di gestione Snapshot StorSimple hello. Fare clic su **Modifica installazione** quindi fare clic su **Disinstalla**.
   
   > [!NOTE]
   > Se sono presenti processi MMC in esecuzione in background hello, ad esempio Gestione Snapshot StorSimple o Gestione disco, disinstalla hello avrà esito negativo e verrà visualizzato un messaggio tooclose tutte le istanze di MMC prima di tentano il programma di hello toouninstall. Selezionare **chiudere le applicazioni e tenta toorestart al termine dell'installazione viene completata automaticamente**, quindi fare clic su **OK**.
   > 
   > 
5. Quando si disinstalla hello processo è completato, un **installazione completata** messaggio viene visualizzato. Fare clic su **Close**.

### <a name="step-2-back-up-hello-storsimple-snapshot-manager-database"></a>Passaggio 2: Eseguire il backup del database di gestione Snapshot StorSimple hello
Utilizzare i seguenti passaggi toocreate hello e salvare una copia del database di gestione Snapshot StorSimple hello.

#### <a name="tooback-up-hello-database"></a>tooback backup database hello
1. Interrompi servizio di gestione Microsoft StorSimple hello:
   
   1. Avviare Server Manager.
   2. Nel Dashboard di Server Manager, di hello in hello **strumenti** dal menu **servizi**.
   3. In hello **servizi** selezionare **servizio di gestione Microsoft StorSimple**.
   4. In hello destro in riquadro **servizio di gestione Microsoft StorSimple**, fare clic su **arrestare servizio hello**.
      
        ![Arrestare il servizio di gestione di dispositivi StorSimple hello](./media/storsimple-snapshot-manager-deployment/HCS_SSM_stop_service.png)
2. Sfoglia tooC:\ProgramData\Microsoft\StorSimple\BACatalog. 
   
   > [!NOTE]
   > ProgramData è una cartella nascosta.
  
3. Trovare i file XML di catalogo hello, copia file hello e archivio hello copia in un percorso sicuro o nel cloud hello.
   
    ![File catalogo di backup di StorSimple](./media/storsimple-snapshot-manager-deployment/HCS_SSM_bacatalog.png)
4. Riavviare il servizio di gestione di Microsoft StorSimple hello: 
   
   1. Nel Dashboard di Server Manager, di hello in hello **strumenti** dal menu **servizi**.
   2. In hello **servizi** pagina, seleziona hello **il servizio di gestione di Microsoft StorSimple**e.
   3. In hello destro in riquadro **servizio di gestione Microsoft StorSimple**, fare clic su **riavviare servizio hello**. 

### <a name="step-3-reinstall-storsimple-snapshot-manager-and-restore-hello-database"></a>Passaggio 3: Reinstallare Gestione Snapshot StorSimple e ripristinare i database di hello
tooreinstall gestione Snapshot StorSimple, seguire i passaggi hello [installare un nuovo servizio Gestione Snapshot StorSimple](#install-a-new-storsimple-snapshot-manager). Utilizzare quindi hello seguenti database di gestione Snapshot StorSimple hello toorestore procedura.

#### <a name="toorestore-hello-database"></a>database hello toorestore
1. Interrompi servizio di gestione Microsoft StorSimple hello:
   
   1. Avviare Server Manager.
   2. Nel Dashboard di Server Manager, di hello in hello **strumenti** dal menu **servizi**.
   3. In hello **servizi** selezionare **servizio di gestione Microsoft StorSimple**.
   4. In hello destro in riquadro **servizio di gestione Microsoft StorSimple**, fare clic su **arrestare servizio hello**.
2. Sfoglia tooC:\ProgramData\Microsoft\StorSimple\BACatalog.
   
   > [!NOTE]
   > ProgramData è una cartella nascosta.
   > 
   > 
3. Eliminare il file XML di hello catalogo e sostituirlo con la versione di hello salvato in precedenza.
4. Riavviare il servizio di gestione di Microsoft StorSimple hello: 
   
   1. Nel Dashboard di Server Manager, di hello in hello **strumenti** dal menu **servizi**.
   2. In hello **servizi** selezionare **servizio di gestione Microsoft StorSimple**.
   3. In hello destro in riquadro **servizio di gestione Microsoft StorSimple**, fare clic su **riavviare servizio hello**.

## <a name="next-steps"></a>Passaggi successivi
* toolearn più su StorSimple Snapshot Manager, andare troppo[che cos'è Gestione Snapshot StorSimple?](storsimple-what-is-snapshot-manager.md).
* toolearn più sull'interfaccia utente di gestione Snapshot StorSimple hello, andare troppo[interfaccia utente di gestione Snapshot StorSimple](storsimple-use-snapshot-manager.md).
* toolearn ulteriori informazioni sull'utilizzo di gestione Snapshot StorSimple, andare troppo[tooadminister usare Gestione Snapshot StorSimple la soluzione StorSimple](storsimple-snapshot-manager-admin.md).

