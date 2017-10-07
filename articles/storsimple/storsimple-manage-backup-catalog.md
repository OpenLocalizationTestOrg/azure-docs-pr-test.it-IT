---
title: aaaManage il catalogo di backup di StorSimple | Documenti Microsoft
description: Viene illustrato come toouse hello StorSimple Manager servizio catalogo di Backup pagina toolist, selezionare ed eliminare i set di backup per un volume.
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: ad81bee9-fe43-40b3-a384-b15fb274ecd9
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 04/28/2016
ms.author: v-sharos
ms.openlocfilehash: 14f565c174a10da2c9e2f934a533a5e493f77226
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-your-backup-catalog"></a>Utilizzare toomanage servizio StorSimple Manager di hello il catalogo di backup
## <a name="overview"></a>Panoramica
servizio StorSimple Manager Hello **catalogo di Backup** pagina vengono visualizzati tutti i set di backup di hello che vengono creati quando sono stati eseguiti backup manuale o pianificato. È possibile utilizzare tutti i backup hello di toolist questa pagina per un criterio di backup o un volume, seleziona o eliminare i backup, o utilizzare un backup toorestore o clonare un volume.

In questa esercitazione viene illustrato come eliminare toolist e selezionare un set di backup. toolearn come toorestore il dispositivo di backup, andare troppo[ripristinare il dispositivo da un set di backup](storsimple-restore-from-backup-set.md). toolearn come tooclone un volume, andare troppo[clonare un volume StorSimple](storsimple-clone-volume.md).

![Catalogo di backup](./media/storsimple-manage-backup-catalog/backupcatalog.png) 

Hello **catalogo di Backup** pagina fornisce un toonarrow query la selezione di set di backup. È possibile filtrare i set di backup hello che vengono recuperati, in base a hello seguenti parametri:

* **Dispositivo** : dispositivo hello in cui hello è stato creato il set di backup.
* **Eseguire il backup dei criteri o Volume** : hello criteri di backup o di volume associato a questo set di backup.
* **Da e a** : hello intervallo di data e ora, quando i set di backup hello è stato creato.

Hello set di backup filtrati possono quindi essere caratterizzati in base a hello gli attributi seguenti:

* **Nome** : hello nome del criterio di backup hello o volume associato al set di backup hello.
* **Dimensioni** : hello dimensioni effettive hello del set di backup.
* **Data creazione** : hello data e l'ora di creazione dei backup hello. 
* **Tipo** : i set di backup possono essere snapshot in locale o del cloud. Uno snapshot locale è un backup di tutti i dati di volume archiviati localmente nel dispositivo hello, mentre uno snapshot nel cloud si riferisce toohello backup dei dati di volume che risiedono nel cloud hello. Gli snapshot in locale forniscono un accesso più rapido, mentre gli snapshot del cloud vengono scelti per la resilienza dei dati.
* **Avviato da** : hello backup possono essere avviati automaticamente da una pianificazione o manualmente dall'utente. È possibile utilizzare i backup tooschedule un criterio di backup. In alternativa, è possibile utilizzare hello **eseguire backup** opzione tootake un backup manuale.

## <a name="list-backup-sets-for-a-volume"></a>Elencare i set di backup per un volume
Questa procedura completa di hello toolist tutti i backup di hello per un volume.

#### <a name="toolist-backup-sets"></a>set di backup toolist
1. Nella pagina del servizio StorSimple Manager hello, fare clic su hello **catalogo di Backup** scheda.
2. Hello selezioni dei filtri come indicato di seguito:
   
   1. Selezionare i dispositivi appropriati hello.
   2. Nell'elenco a discesa hello, scegliere un volume di tooview backup hello corrispondente hello.
   3. Specificare l'intervallo di tempo hello.
   4. Fare clic sull'icona di controllo hello ![Icona del segno di spunta](./media/storsimple-manage-backup-catalog/HCS_CheckIcon.png) tooexecute questa query.
      
      i backup di Hello associati volume hello selezionato verrà visualizzato nell'elenco di hello dei set di backup.

## <a name="select-a-backup-set"></a>Selezionare un set di backup
Completare hello seguendo i passaggi tooselect del set di un backup per un volume o criteri di backup.

#### <a name="tooselect-a-backup-set"></a>tooselect un set di backup
1. Nella pagina del servizio StorSimple Manager hello, fare clic su hello **catalogo di Backup** scheda.
2. Hello selezioni dei filtri come indicato di seguito:
   
   1. Selezionare i dispositivi appropriati hello.
   2. Nell'elenco a discesa hello, scegliere hello volumi o criteri di backup per il backup di hello che si desidera tooselect.
   3. Specificare l'intervallo di tempo hello.
   4. Fare clic sull'icona di controllo hello ![Icona del segno di spunta](./media/storsimple-manage-backup-catalog/HCS_CheckIcon.png) tooexecute questa query.
      
      Hello i backup associati hello selezionato volumi o criteri di backup dovrebbero essere visualizzato nell'elenco di hello dei set di backup.
3. Selezionare ed espandere un set di backup Hello **ripristinare** e **eliminare** vengono visualizzate le opzioni nella parte inferiore di hello della pagina hello. È possibile eseguire una di queste azioni nel set di backup hello selezionato.

## <a name="delete-a-backup-set"></a>Eliminare un set di backup
Eliminare un backup quando non si desidera più tooretain hello dei dati. Eseguire hello seguendo i passaggi toodelete un set di backup.

#### <a name="toodelete-a-backup-set"></a>toodelete un set di backup
1. Nella pagina del servizio StorSimple Manager hello, fare clic su hello **scheda catalogo di Backup**.
2. Hello selezioni dei filtri come indicato di seguito:
   
   1. Selezionare i dispositivi appropriati hello.
   2. Nell'elenco a discesa hello, scegliere hello volumi o criteri di backup per il backup di hello che si desidera tooselect.
   3. Specificare l'intervallo di tempo hello.
   4. Fare clic sull'icona di controllo hello ![Icona del segno di spunta](./media/storsimple-manage-backup-catalog/HCS_CheckIcon.png) tooexecute questa query.
      
      Hello i backup associati hello selezionato volumi o criteri di backup dovrebbero essere visualizzato nell'elenco di hello dei set di backup.
3. Selezionare ed espandere un set di backup Hello **ripristinare** e **eliminare** vengono visualizzate le opzioni nella parte inferiore di hello della pagina hello. Fare clic su **Elimina**.
4. Si riceverà la notifica quando l'eliminazione di hello è in corso e quando ha terminato correttamente. Dopo l'eliminazione di hello, refresh query hello in questa pagina. set di backup Hello eliminato non verrà più visualizzato nell'elenco di hello dei set di backup.

## <a name="next-steps"></a>Passaggi successivi
* Informazioni su come troppo[utilizzare hello toorestore catalogo di backup del dispositivo da un set di backup](storsimple-restore-from-backup-set.md).
* Informazioni su come troppo[utilizzare hello tooadminister servizio StorSimple Manager dispositivo StorSimple](storsimple-manager-service-administration.md).

