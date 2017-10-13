---
title: Operazioni di backup di StorSimple Snapshot Manager | Microsoft Docs
description: Viene descritto come usare lo snap-in MMC StorSimple Snapshot Manager per visualizzare e gestire i processi di backup pianificati, attualmente in esecuzione e completati.
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
ms.openlocfilehash: 03e306b62250f2bb033cc14e856a59760b5406c3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-storsimple-snapshot-manager-to-view-and-manage-backup-jobs"></a>Usare StorSimple Snapshot Manager per visualizzare e gestire i processi di backup

## <a name="overview"></a>Panoramica
Nel nodo **Processi** del riquadro **Ambito** vengono mostrate le attività di backup **pianificate**, delle **ultime 24 ore** e **in esecuzione** avviate in modo interattivo o da un criterio configurato. 

In questa esercitazione viene illustrato come usare il nodo **Processi** per visualizzare le informazioni sui processi di backup pianificati, recenti e attualmente in esecuzione. L'elenco dei processi e le informazioni corrispondenti vengono visualizzati nel riquadro **Risultati**. Inoltre, è possibile fare clic con il pulsante destro del mouse su un processo elencato e visualizzare un menu di scelta rapida in cui sono elencate le azioni disponibili.

## <a name="view-scheduled-jobs"></a>Visualizzazione dei processi pianificati
Utilizzare la procedura seguente per visualizzare i processi di backup pianificati.

#### <a name="to-view-scheduled-jobs"></a>Per visualizzare i processi pianificati
1. Fare clic sull’icona del desktop per avviare StorSimple Snapshot Manager. 
2. Nel riquadro **Ambito** espandere il nodo **Processi**, quindi fare clic su **Pianificati**. Nel riquadro **Risultati** vengono visualizzate le informazioni seguenti:
   
   * **Nome** : il nome dello snapshot pianificato
   * **Prossima esecuzione** : la data e l’ora del successivo snapshot pianificato.
   * **Ultima esecuzione** : la data e l'ora dello snapshot pianificato più recente.
     
     > [!NOTE]
     > Solo per gli snapshot monouso, il valore di **Prossima esecuzione** e **Ultima esecuzione** sarà lo stesso.
     
     ![Processi di backup pianificati](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_scheduled.png) 
3. Per eseguire azioni aggiuntive su un processo specifico, fare clic con il pulsante destro del mouse sul nome del processo nel riquadro **Risultati** e selezionare un’opzione del menu.

## <a name="view-recent-jobs"></a>Visualizzazione dei processi recenti
Utilizzare la procedura seguente per visualizzare i processi di backup e ripristino completati nelle ultime 24 ore.

#### <a name="to-view-recent-jobs"></a>Per visualizzare i processi recenti
1. Fare clic sull’icona del desktop per avviare StorSimple Snapshot Manager.
2. Nel riquadro **Ambito** espandere il nodo **Processi**, quindi fare clic su **Ultime 24 ore**. Nel riquadro **Risultati** vengono mostrati i processi di backup per le ultime 24 ore (per un massimo di 64 processi). Nel riquadro **Risultati** vengono visualizzate le informazioni seguenti, a seconda delle opzioni di **Visualizza** specificate:
   
   * **Nome** : il nome dello snapshot pianificato.
   * **Avviato** : la data e l’ora di avvio dello snapshot.
   * **Arrestato** : la data e l'ora in cui lo snapshot è stato completato o terminato.
   * **Trascorso**: la quantità di tempo che intercorre tra l'ora di **Avviato** e **Arrestato**.
   * **Stato** : lo stato del processo completato di recente. **Esito positivo** indica che il backup è stato creato correttamente. **Operazione non riuscita** indica che il processo non è stato eseguito correttamente.
   * **Informazioni** : il motivo dell'errore.
   * **Byte elaborati (MB)** : la quantità di dati del gruppo di volumi che è stata elaborata (in MB). 
     
     ![Processi eseguiti nelle ultime 24 ore](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_Last_24_hours.png) 
3. Per eseguire azioni aggiuntive su un processo specifico, fare clic con il pulsante destro del mouse sul nome del processo nel riquadro **Risultati** e selezionare un’opzione del menu.
   
    ![Eliminare un processo](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Delete_backup.png)

## <a name="view-currently-running-jobs"></a>Visualizzazione dei processi attualmente in esecuzione
Utilizzare la procedura seguente per visualizzare i processi attualmente in esecuzione.

#### <a name="to-view-currently-running-jobs"></a>Per visualizzare i processi attualmente in esecuzione
1. Fare clic sull’icona del desktop per avviare StorSimple Snapshot Manager.
2. Nel riquadro **Ambito** espandere il nodo **Processi**, quindi fare clic su **In esecuzione**. Nel riquadro **Risultati** vengono visualizzate le informazioni seguenti, a seconda delle opzioni di **Visualizza** specificate:
   
   * **Nome** : il nome dello snapshot pianificato.
   * **Avviato** : la data e l’ora di avvio dello snapshot.
   * **Checkpoint** : l'azione corrente del backup.
   * **Stato** : la percentuale di completamento.
   * **Trascorso** : la quantità di tempo trascorso dall'avvio del backup. 
   * **Velocità effettiva media (MB)** : rapporto tra i byte totali di dati elaborati e il tempo totale usato per l'elaborazione (MB).
   * **Byte elaborati (MB)** : totale dei byte di dati elaborati (in MB).
   * **Byte scritti (MB)** : totale dei byte scritti (in MB). Questo valore include i dati e i metadati e quindi in genere è maggiore rispetto al valore dei byte elaborati.
     
     ![Processi attualmente in esecuzione](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_running.png)
3. Per eseguire azioni aggiuntive su un processo specifico, fare clic con il pulsante destro del mouse sul nome del processo nel riquadro **Risultati** e selezionare un’opzione del menu.

## <a name="next-steps"></a>Passaggi successivi
* Informazioni su come [usare StorSimple Snapshot Manager per amministrare la soluzione di StorSimple](storsimple-snapshot-manager-admin.md).
* Informazioni su come [usare StorSimple Snapshot Manager per gestire il catalogo di backup](storsimple-snapshot-manager-manage-backup-catalog.md)

