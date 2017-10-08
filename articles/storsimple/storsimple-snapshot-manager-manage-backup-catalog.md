---
title: catalogo di backup di Snapshot Manager aaaStorSimple | Documenti Microsoft
description: Descrive come toouse hello tooview snap-in MMC di StorSimple Snapshot Manager e gestire hello catalogo di backup.
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: 6abdbfd2-22ce-45a5-aa15-38fae4c8f4ec
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: 173410095bcec7948d780d7fc258d2e3670bde8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-toomanage-hello-backup-catalog"></a>Catalogo di backup hello toomanage usare Gestione Snapshot StorSimple

## <a name="overview"></a>Panoramica
la funzione principale Hello di StorSimple Snapshot Manager è tooallow si toocreate coerenti con l'applicazione copie di backup di volumi StorSimple sotto forma di hello di snapshot. Gli snapshot vengono quindi elencati in un file XML denominato *catalogo di backup*. catalogo di backup Hello organizza gli snapshot per gruppo di volumi e quindi per snapshot locale o cloud.

In questa esercitazione viene illustrato come utilizzare hello **catalogo di Backup** hello toocomplete di nodo seguenti attività:

* Ripristino di un volume
* Clonazione di un volume o di un gruppo di volumi
* Eliminazione di un backup
* Recupero di un file
* Ripristinare il database di gestione Snapshot Storsimple hello

È possibile visualizzare un catalogo di backup hello espandendo hello **catalogo di Backup** nodo hello **ambito** riquadro e quindi espandere il gruppo di volumi hello.

* Se si fa clic sul nome gruppo di volumi hello, hello **risultati** riquadro mostra il numero di hello di snapshot locali e cloud disponibile per il gruppo di volumi hello. 
* Se si fa clic **Snapshot locale** o **Snapshot Cloud**, hello **risultati** riquadro vengono visualizzate le seguenti informazioni su ogni backup snapshot hello (a seconda del **Visualizzazione** impostazioni):
  
  * **Nome** : hello ora hello dello snapshot.
  * **Tipo** : se si tratta di uno snapshot locale o cloud.
  * **Proprietario** : proprietario del contenuto hello. 
  * **Disponibile** : indica se hello snapshot è attualmente disponibile. **True** indica tale snapshot hello è disponibile e può essere ripristinato; **False** indica tale snapshot hello non è più disponibile. 
  * **Importare** : indica se il backup di hello è stato importato. **True** indica che il backup hello è stato importato da hello Gestione dispositivi StorSimple servizio nel dispositivo di hello hello ora è stato configurato in Gestione Snapshot StorSimple. **False** indica che non è stato importato, ma è stato creato da Gestione Snapshot StorSimple. (È possibile identificare facilmente un gruppo di volumi importati perché viene aggiunto un suffisso che identifica il dispositivo hello da cui è stato importato il gruppo di volumi hello.)
    
    ![Catalogo di backup](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Backup_catalog.png)
* Se si espande **Snapshot locale** o **Snapshot Cloud**, quindi fare clic su un nome di un singolo snapshot e hello **risultati** riquadro vengono visualizzate le seguenti informazioni su hello hello snapshot selezionato:
  
  * **Nome** : hello volume identificato dalla lettera di unità. 
  * **Nome locale** : il nome locale di hello dell'unità di hello (se disponibile). 
  * **Dispositivo** : hello nome di dispositivo hello quali hello contiene volume. 
  * **Disponibile** : indica se hello snapshot è attualmente disponibile. **True** indica tale snapshot hello è disponibile e può essere ripristinato; **False** indica tale snapshot hello non è più disponibile. 

## <a name="restore-a-volume"></a>Ripristino di un volume
Utilizzare hello seguendo procedure toorestore un volume dal backup.

#### <a name="prerequisites"></a>Prerequisiti
Se non è già stato fatto, creare un volume e il gruppo di volumi e quindi eliminare il volume di hello. Per impostazione predefinita, gestione Snapshot StorSimple esegue il backup di un volume prima di autorizzarne toobe eliminato. Questo accorgimento evita la perdita di dati se il volume di hello venga eliminato per errore o se i dati di hello toobe recuperato per qualsiasi motivo. 

Gestione Snapshot StorSimple Visualizza hello segue messaggio durante la creazione di backup precauzionale hello.

![Messaggio di snapshot automatico](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Automatic_snap.png) 

> [!IMPORTANT]
> Non è possibile eliminare un volume che fa parte di un gruppo di volumi. non è disponibile l'opzione di eliminazione Hello. <br>
> 
> 

#### <a name="toorestore-a-volume"></a>toorestore un volume
1. Fare clic su hello icona sul desktop toostart gestione Snapshot StorSimple. 
2. In hello **ambito** riquadro espandere hello **catalogo di Backup** nodo, espandere un gruppo di volumi e quindi fare clic su **gli snapshot locali** o **gli snapshot Cloud**. Viene visualizzato un elenco di snapshot di backup in hello **risultati** riquadro.
3. Trova hello backup che si desidera toorestore pulsante destro del mouse e quindi fare clic su **ripristinare**.
   
    ![Ripristino del catalogo di backup](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Restore_BU_catalog.png) 
4. Nella pagina di conferma hello, esaminare i dettagli di hello, digitare **conferma**, quindi fare clic su **OK**. Gestione Snapshot StorSimple Usa volume hello di hello toorestore backup.
   
    ![Ripristino del messaggio di conferma](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Restore_volume_msg.png) 
5. È possibile monitorare l'azione di ripristino hello mentre è in esecuzione. In hello **ambito** riquadro espandere hello **processi** nodo e quindi fare clic su **esecuzione**. vengono visualizzati i dettagli dei processi Hello in hello **risultati** riquadro. Al termine il processo di ripristino di hello, i dettagli dei processi hello sono trasferito toohello **ultime 24 ore** elenco.

## <a name="clone-a-volume-or-volume-group"></a>Clonazione di un volume o di un gruppo di volumi
Utilizzare hello seguendo procedure toocreate duplicato (clone) di un gruppo di volumi o il volume.

#### <a name="tooclone-a-volume-or-volume-group"></a>tooclone un volume o gruppo di volumi
1. Fare clic su hello icona sul desktop toostart gestione Snapshot StorSimple.
2. In hello **ambito** riquadro espandere hello **catalogo di Backup** nodo, espandere un gruppo di volumi e quindi fare clic su **gli snapshot Cloud**. Viene visualizzato un elenco di backup in hello **risultati** riquadro.
3. Trovare il volume di hello o un gruppo di volumi che desidera tooclone, volume hello pulsante destro del mouse o nome gruppo di volumi e fare clic su **Clone**. Hello **Clona Snapshot nel Cloud** viene visualizzata la finestra di dialogo.
   
    ![Clonazione di uno snapshot cloud](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Clone.png) 
4. Hello completo **Clona Snapshot nel Cloud** la finestra di dialogo come segue: 
   
   1. In hello **nome** casella di testo, digitare un nome per hello clonato volume. Questo nome verrà visualizzato in hello **volumi** nodo. 
   2. (Facoltativo) selezionare **unità**, quindi selezionare una lettera di unità dall'elenco a discesa hello.
   3. (Facoltativo) selezionare **cartella (NTFS)**, digitare un percorso o fare clic su Sfoglia e selezionare il percorso della cartella hello. 
   4. Fare clic su **Crea**.
5. Al termine dell'operazione hello processo di clonazione, è necessario inizializzare il volume clonato hello. Avviare Server Manager, quindi avviare Gestione disco. Per istruzioni dettagliate, vedere [Montaggio volumi](storsimple-snapshot-manager-manage-volumes.md#mount-volumes). Dopo l'inizializzazione, verrà elencato il volume di hello in hello **volumi** nodo hello **ambito** riquadro. Se non è possibile visualizzare volume hello elencati, aggiornare l'elenco di hello dei volumi (hello rapida **volumi** nodo e quindi fare clic su **aggiornamento**).

## <a name="delete-a-backup"></a>Eliminazione di un backup
Utilizzare hello seguendo procedure toodelete uno snapshot dal catalogo di backup hello. 

> [!NOTE]
> Se si elimina uno snapshot, hello associati snapshot hello dati di backup. Tuttavia, il processo di hello di pulizia dei dati dal cloud hello potrebbe richiedere alcuni minuti.<br>


#### <a name="toodelete-a-backup"></a>toodelete una copia di backup
1. Fare clic su hello icona sul desktop toostart gestione Snapshot StorSimple.
2. In hello **ambito** riquadro espandere hello **catalogo di Backup** nodo, espandere un gruppo di volumi e quindi fare clic su **gli snapshot locali** o **gli snapshot Cloud**. Viene visualizzato un elenco di snapshot in hello **risultati** riquadro.
3. Snapshot di hello pulsante destro del mouse si desidera toodelete e quindi fare clic su **eliminare**.
4. Quando viene visualizzato il messaggio di conferma di hello, fare clic su **OK**.

## <a name="recover-a-file"></a>Recupero di un file
Se un file viene accidentalmente eliminato da un volume, è possibile ripristinare file hello recuperando uno snapshot antecedente l'eliminazione di hello, hello snapshot toocreate utilizzando un clone del volume hello e quindi copiando il file hello da hello volume originale di toohello volume clonato.

#### <a name="prerequisites"></a>Prerequisiti
Prima di iniziare, assicurarsi di disporre di un backup corrente del gruppo di volumi hello. Eliminare quindi un file archiviato in uno dei volumi hello in tale gruppo di volumi. Infine, utilizzare hello seguente hello toorestore passaggi eliminato i file dal backup. 

#### <a name="toorecover-a-deleted-file"></a>toorecover un file eliminato
1. Fare clic sull'icona di gestione Snapshot StorSimple hello sul desktop. verrà visualizzata la finestra di console di gestione Snapshot StorSimple Hello. 
2. In hello **ambito** riquadro espandere hello **catalogo di Backup** nodo e passare tooa snapshot che contiene file hello eliminato. In genere, è necessario selezionare uno snapshot creato appena prima dell'eliminazione di hello.
3. Trova hello volume che si desidera tooclone, pulsante destro del mouse e scegliere **Clone**. Hello **Clona Snapshot nel Cloud** viene visualizzata la finestra di dialogo.
   
    ![Clonazione di uno snapshot cloud](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Clone.png) 
4. Hello completo **Clona Snapshot nel Cloud** la finestra di dialogo come segue: 
   
   1. In hello **nome** casella di testo, digitare un nome per hello clonato volume. Questo nome verrà visualizzato in hello **volumi** nodo. 
   2. (Facoltativo) Selezionare **unità**, quindi selezionare una lettera di unità dall'elenco a discesa hello. 
   3. (Facoltativo) Selezionare **cartella (NTFS)**e digitare il percorso della cartella oppure fare clic su **Sfoglia** e selezionare il percorso della cartella hello. 
   4. Fare clic su **Crea**. 
5. Al termine dell'operazione hello processo di clonazione, è necessario inizializzare il volume clonato hello. Avviare Server Manager, quindi avviare Gestione disco. Per istruzioni dettagliate, vedere [Montaggio volumi](storsimple-snapshot-manager-manage-volumes.md#mount-volumes). Dopo l'inizializzazione, verrà elencato il volume di hello in hello **volumi** nodo hello **ambito** riquadro. 
   
    Se non è possibile visualizzare volume hello elencati, aggiornare l'elenco di hello dei volumi (hello rapida **volumi** nodo e quindi fare clic su **aggiornamento**).
6. Cartella NTFS hello aperto che contiene il volume clonato hello, espandere hello **volumi** nodo e quindi aprire hello clonato volume. Trovare il file hello che si desidera toorecover e copiarlo toohello volume principale.
7. Dopo aver ripristinato il file hello, è possibile eliminare una cartella NTFS hello che contiene il volume clonato hello.

## <a name="restore-hello-storsimple-snapshot-manager-database"></a>Ripristinare il database di gestione Snapshot StorSimple hello
È consigliabile eseguire regolarmente il backup del database di gestione Snapshot StorSimple hello nel computer host hello. Se si verifica un'emergenza o computer host hello non riesce per qualsiasi motivo, è quindi possibile ripristinarlo da backup hello. Creare i backup del database hello è un processo manuale.

#### <a name="tooback-up-and-restore-hello-database"></a>tooback backup e ripristino del database di hello
1. Interrompi servizio di gestione Microsoft StorSimple hello:
   
   1. Avviare Server Manager.
   2. Nel dashboard di Server Manager hello, su hello **strumenti** dal menu **servizi**.
   3. In hello **servizi** finestra, seleziona hello **servizio di gestione Microsoft StorSimple**.
   4. In hello destro in riquadro **servizio di gestione Microsoft StorSimple**, fare clic su **arrestare servizio hello**.
2. Nel computer host hello, esplorare tooC:\ProgramData\Microsoft\StorSimple\BACatalog. 
   
   > [!NOTE]
   > ProgramData è una cartella nascosta.
   > 
   > 
3. Trovare i file XML di catalogo hello, copia file hello e archivio hello copia in un percorso sicuro o nel cloud hello. Se l'host di hello non riesce, è possibile utilizzare questo file di backup toohelp Ripristina hello criteri di backup creati in StorSimple Snapshot Manager.
   
    ![File del catalogo di backup di Azure StorSimple](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_bacatalog.png)
4. Riavviare il servizio di gestione di Microsoft StorSimple hello: 
   
   1. Nel dashboard di Server Manager hello, su hello **strumenti** dal menu **servizi**.
   2. In hello **servizi** finestra, seleziona hello **servizio di gestione Microsoft StorSimple**.
   3. In hello destro in riquadro **servizio di gestione Microsoft StorSimple**, fare clic su **riavviare servizio hello**.
5. Nel computer host hello, esplorare tooC:\ProgramData\Microsoft\StorSimple\BACatalog. 
6. Eliminare il file XML di catalogo hello e sostituirlo con la versione di backup hello creato. 
7. Fare clic su hello desktop gestione Snapshot StorSimple icona toostart gestione Snapshot StorSimple. 

## <a name="next-steps"></a>Passaggi successivi
* Altre informazioni, vedere [utilizzando Gestione Snapshot StorSimple tooadminister la soluzione StorSimple](storsimple-snapshot-manager-admin.md).
* Ulteriori informazioni sulle [attività e sui flussi di lavoro di StorSimple Snapshot Manager](storsimple-snapshot-manager-admin.md#storsimple-snapshot-manager-tasks-and-workflows).

