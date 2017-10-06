---
title: aaaManage il catalogo di backup di StorSimple | Documenti Microsoft
description: Viene illustrato come toouse hello toolist pagina di gestione di dispositivi StorSimple servizio catalogo di backup, selezionare ed eliminare i set di backup.
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/29/2017
ms.author: alkohli
ms.openlocfilehash: e464609e74409a06a198790719abd82ed03c03d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-your-backup-catalog"></a>Utilizzare toomanage servizio di gestione di dispositivi StorSimple hello il catalogo di backup
## <a name="overview"></a>Panoramica
servizio di gestione di dispositivi StorSimple Hello **catalogo di Backup** pannello vengono visualizzati tutti i set di backup di hello che vengono creati quando sono stati eseguiti backup manuale o pianificato. È possibile utilizzare tutti i backup hello di toolist questa pagina per un criterio di backup o un volume, seleziona o eliminare i backup, o utilizzare un backup toorestore o clonare un volume.

In questa esercitazione viene illustrato come eliminare toolist e selezionare un set di backup. toolearn come toorestore il dispositivo di backup, andare troppo[ripristinare il dispositivo da un set di backup](storsimple-8000-restore-from-backup-set-u2.md). toolearn come tooclone un volume, andare troppo[clonare un volume StorSimple](storsimple-8000-clone-volume-u2.md).

![Catalogo di backup](./media/storsimple-8000-manage-backup-catalog/bucatalog.png) 

Hello **catalogo di Backup** pannello fornisce un toonarrow query la selezione di set di backup. È possibile filtrare i set di backup hello che vengono recuperati, in base a hello seguenti parametri:

* **Dispositivo** : dispositivo hello in cui hello è stato creato il set di backup.
* **Criteri di backup o il Volume** : hello criteri di backup o di volume associato a questo set di backup.
* **Da e a** : hello intervallo di data e ora, quando i set di backup hello è stato creato.

Hello set di backup filtrati possono quindi essere caratterizzati in base a hello gli attributi seguenti:

* **Nome** : hello nome del criterio di backup hello o volume associato al set di backup hello.
* **Dimensioni** : hello dimensioni effettive hello del set di backup.
* **Data creazione** : hello data e l'ora di creazione dei backup hello. 
* **Tipo** : i set di backup possono essere snapshot in locale o del cloud. Uno snapshot locale è un backup di tutti i dati di volume archiviati localmente nel dispositivo hello, mentre uno snapshot nel cloud si riferisce toohello backup dei dati di volume che risiedono nel cloud hello. Gli snapshot in locale forniscono un accesso più rapido, mentre gli snapshot del cloud vengono scelti per la resilienza dei dati.
* **Avviato da** : hello backup possono essere avviati automaticamente da una pianificazione o manualmente dall'utente. È possibile utilizzare i backup tooschedule un criterio di backup. In alternativa, è possibile utilizzare hello **eseguire backup** opzione tootake un backup manuale.

## <a name="list-backup-sets-for-a-backup-policy"></a>Elencare i set di backup di un criterio di backup
Questa procedura completa di hello toolist tutti i backup di hello per un criterio di backup.

#### <a name="toolist-backup-sets"></a>set di backup toolist
1. Il servizio di gestione di dispositivi StorSimple tooyour, fare clic su **catalogo di Backup**.

2. Hello selezioni dei filtri come indicato di seguito:
   
   1. Specificare l'intervallo di tempo hello.
   2. Selezionare i dispositivi appropriati hello.
   3. Filtrare in base **criteri di Backup** tooview hello backup hello corrispondente.
   3. Selezionare dall'elenco a discesa dei criteri di backup hello **tutti** tooview tutti hello i backup selezionati hello dispositivo.
   4. Fare clic su **applica** tooexecute questa query.
      
      i backup Hello associati al criterio di backup hello selezionato verrà visualizzato nell'elenco di hello dei set di backup.

      ![Passare toobackup catalogo](./media/storsimple-8000-manage-backup-catalog/bucatalog1.png)

## <a name="select-a-backup-set"></a>Selezionare un set di backup
Completare hello seguendo i passaggi tooselect del set di un backup per un volume o criteri di backup.

#### <a name="tooselect-a-backup-set"></a>tooselect un set di backup
1. Il servizio di gestione di dispositivi StorSimple tooyour, fare clic su **catalogo di Backup**.
2. Hello selezioni dei filtri come indicato di seguito:
   
   1. Specificare l'intervallo di tempo hello. 
   2. Selezionare i dispositivi appropriati hello. 
   3. Filtrare in base volumi o criteri di backup per il backup di hello che si desidera tooselect.
   4. Fare clic su **applica** tooexecute questa query.
      
      Hello i backup associati hello selezionato volumi o criteri di backup dovrebbero essere visualizzato nell'elenco di hello dei set di backup.

      ![Passare toobackup catalogo](./media/storsimple-8000-manage-backup-catalog/bucatalog1.png)

3. Selezionare ed espandere un set di backup È ora possibile visualizzare i set di backup hello suddivisi in base volumi hello in esso contenuti. Hello **ripristinare** e **eliminare** opzioni sono disponibili tramite hello menu di scelta rapida (rapida) per i set di backup hello. È possibile eseguire una di queste azioni nel set di backup hello selezionato.

    ![Passare toobackup catalogo](./media/storsimple-8000-manage-backup-catalog/bucatalog2.png)

## <a name="delete-a-backup-set"></a>Eliminare un set di backup
Eliminare un backup quando non si desidera più tooretain hello dei dati. Eseguire hello seguendo i passaggi toodelete un set di backup.

#### <a name="toodelete-a-backup-set"></a>toodelete un set di backup
 Il servizio di gestione di dispositivi StorSimple tooyour, fare clic su **catalogo di Backup**.
2. Hello selezioni dei filtri come indicato di seguito:
   
   1. Specificare l'intervallo di tempo hello. 
   2. Selezionare i dispositivi appropriati hello. 
   3. Filtrare in base volumi o criteri di backup per il backup di hello che si desidera tooselect.
   4. Fare clic su **applica** tooexecute questa query.
      
      Hello i backup associati hello selezionato volumi o criteri di backup dovrebbero essere visualizzato nell'elenco di hello dei set di backup.

      ![Passare toobackup catalogo](./media/storsimple-8000-manage-backup-catalog/bucatalog1.png)

3. Selezionare ed espandere un set di backup È ora possibile visualizzare i set di backup hello suddivisi in base volumi hello in esso contenuti. Hello **ripristinare** e **eliminare** opzioni sono disponibili tramite hello menu di scelta rapida (rapida) per i set di backup hello. Fare doppio clic su set di backup selezionato hello e selezionare il menu di scelta rapida hello **eliminare**.

    ![Passare toobackup catalogo](./media/storsimple-8000-manage-backup-catalog/bucatalog3.png)

4. Quando viene richiesta la conferma, esaminare le informazioni visualizzata hello e fare clic su **eliminare**. backup selezionato Hello viene eliminato definitivamente.

    ![Passare toobackup catalogo](./media/storsimple-8000-manage-backup-catalog/bucatalog4.png)  

5. Si riceverà la notifica quando l'eliminazione di hello è in corso e quando ha terminato correttamente. Dopo l'eliminazione di hello, refresh query hello in questa pagina. set di backup Hello eliminato non verrà più visualizzato nell'elenco di hello dei set di backup.

    ![Passare toobackup catalogo](./media/storsimple-8000-manage-backup-catalog/bucatalog7.png)

## <a name="next-steps"></a>Passaggi successivi
* Informazioni su come troppo[utilizzare hello toorestore catalogo di backup del dispositivo da un set di backup](storsimple-8000-restore-from-backup-set-u2.md).
* Informazioni su come troppo[utilizzare hello tooadminister servizio di gestione di dispositivi StorSimple dispositivo StorSimple](storsimple-8000-manager-service-administration.md).

