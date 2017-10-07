---
title: processi di backup di Snapshot Manager aaaStorSimple | Documenti Microsoft
description: Viene descritto come toouse hello tooview snap-in MMC di StorSimple Snapshot Manager e gestire i processi di backup pianificati, attualmente in esecuzione e completati.
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: bf4dcff6-c819-4766-b9d9-9922831cb200
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: 3dba0a2aa527d17d67130f537bcdce5722b05a76
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-tooview-and-manage-backup-jobs"></a>Utilizzare Gestione Snapshot StorSimple tooview e gestire i processi di backup

## <a name="overview"></a>Panoramica
Hello **processi** nodo hello **ambito** riquadro Mostra hello **pianificato**, **ultime 24 ore**, e **esecuzione**attività è stata avviata in modo interattivo o da criteri di configurazione di backup. 

In questa esercitazione viene illustrato come utilizzare hello **processi** informazioni toodisplay nodo sui processi di backup attualmente in esecuzione, pianificati e recenti. (elenco hello dei processi e delle informazioni corrispondenti vengono visualizzati nel hello **risultati** riquadro.) Inoltre, è possibile fare clic con il pulsante destro del mouse su un processo elencato e visualizzare un menu di scelta rapida in cui sono elencate le azioni disponibili.

## <a name="view-scheduled-jobs"></a>Visualizzazione dei processi pianificati
Hello utilizzare seguendo procedure tooview processi di backup pianificati.

#### <a name="tooview-scheduled-jobs"></a>processi pianificati tooview
1. Fare clic su hello icona sul desktop toostart gestione Snapshot StorSimple. 
2. In hello **ambito** riquadro espandere hello **processi** nodo e fare clic su **pianificato**. Hello seguenti informazioni nella hello **risultati** riquadro:
   
   * **Nome** : hello nome dello snapshot pianificato hello
   * **Prossima esecuzione** : hello data e ora del successivo snapshot pianificato hello
   * **Ultima esecuzione** : hello data e l'ora dello snapshot pianificato più recente di hello
     
     > [!NOTE]
     > Per gli snapshot soli monouso, hello **prossima esecuzione** e **ultima esecuzione** sarà hello stesso.
     
     ![Processi di backup pianificati](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_scheduled.png) 
3. tooperform azioni aggiuntive su un processo specifico, fare doppio clic su nome del processo hello in hello **risultati** riquadro e selezionare una delle opzioni di menu hello.

## <a name="view-recent-jobs"></a>Visualizzazione dei processi recenti
Utilizzare hello dopo il backup di routine tooview e ripristinare i processi completati nelle hello ultime 24 ore.

#### <a name="tooview-recent-jobs"></a>processi recenti tooview
1. Fare clic su hello icona sul desktop toostart gestione Snapshot StorSimple.
2. In hello **ambito** riquadro espandere hello **processi** nodo e fare clic su **ultime 24 ore**. Hello **risultati** riquadro vengono visualizzati i processi di backup per hello ultime 24 ore (tooa massimo di 64 processi). Hello seguenti informazioni nella hello **risultati** riquadro, a seconda di hello **vista** opzioni:
   
   * **Nome** : hello nome dello snapshot pianificato hello.
   * **Avvio** : hello data e l'ora di inizio snapshot hello.
   * **Arrestato** : hello data e l'ora dello snapshot hello completata o è stato terminato.
   * **Trascorso** : hello periodo di tempo tra hello **Started** e **arrestato** volte.
   * **Stato** : hello lo stato di processo hello completato di recente. **Esito positivo** indica che il backup hello è stato creato correttamente. **Non è stato possibile** indica che il processo di hello non è stato eseguito correttamente.
   * **Informazioni** : hello motivo dell'errore hello.
   * **Byte elaborati (MB)** : quantità di hello dei dati dal gruppo di volumi hello (in MB) è stato elaborato. 
     
     ![Processi eseguiti in hello ultime 24 ore](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_Last_24_hours.png) 
3. tooperform azioni aggiuntive su un processo specifico, fare doppio clic su nome del processo hello in hello **risultati** riquadro e selezionare una delle opzioni di menu hello.
   
    ![Eliminare un processo](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Delete_backup.png)

## <a name="view-currently-running-jobs"></a>Visualizzazione dei processi attualmente in esecuzione
Utilizzare hello seguenti processi tooview procedure attualmente in esecuzione.

#### <a name="tooview-currently-running-jobs"></a>tooview processi attualmente in esecuzione
1. Fare clic su hello icona sul desktop toostart gestione Snapshot StorSimple.
2. In hello **ambito** riquadro espandere hello **processi** nodo e fare clic su **esecuzione**. A seconda di hello **vista** opzioni specificate, le seguenti informazioni hello viene visualizzato in hello **risultati** riquadro:
   
   * **Nome** : hello nome dello snapshot pianificato hello.
   * **Avvio** : hello data e l'ora di inizio snapshot hello.
   * **Checkpoint** : azione corrente backup hello hello.
   * **Stato** : hello percentuale di completamento.
   * **Trascorso** : quantità di hello di tempo trascorso dall'inizio backup hello. 
   * **Velocità effettiva Media (MB)** : percentuale totale di byte di dati elaborati toothat del tempo totale impiegato per l'elaborazione (MB).
   * **Byte elaborati (MB)** : totale dei byte di dati elaborati (in MB).
   * **Byte scritti (MB)** : totale dei byte scritti (in MB). Include dati hello nonché i metadati di hello e pertanto è in genere maggiore di hello byte elaborati.
     
     ![Processi attualmente in esecuzione](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_running.png)
3. tooperform azioni aggiuntive su un processo specifico, fare doppio clic su nome del processo hello in hello **risultati** riquadro e selezionare una delle opzioni di menu hello.

## <a name="next-steps"></a>Passaggi successivi
* Informazioni su come troppo[usare Gestione Snapshot StorSimple tooadminister la soluzione StorSimple](storsimple-snapshot-manager-admin.md).
* Informazioni su come troppo[utilizzare catalogo di backup di gestione Snapshot StorSimple toomanage hello](storsimple-snapshot-manager-manage-backup-catalog.md).

