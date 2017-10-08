---
title: un volume StorSimple da backup aaaRestore | Documenti Microsoft
description: Viene illustrato come toouse hello toorestore pagina di StorSimple Manager servizio catalogo di Backup un volume StorSimple da un set di backup.
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: b979782e-3184-4465-ad5f-e4516a5885d2
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: e0efa74b14603be41af0cfc5400de3c39ab8824e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="restore-a-storsimple-volume-from-a-backup-set"></a>Ripristinare un volume StorSimple da un set di backup
[!INCLUDE [storsimple-version-selector-restore-from-backup](../../includes/storsimple-version-selector-restore-from-backup.md)]

## <a name="overview"></a>Panoramica
Hello **catalogo di Backup** pagina vengono visualizzati tutti i set di backup di hello che vengono creati quando sono stati eseguiti backup manuali o automatizzati. È possibile utilizzare tutti i backup hello di toolist questa pagina per un criterio di backup o un volume, seleziona o eliminare i backup, o utilizzare un backup toorestore o clonare un volume.

 ![Pagina catalogo di backup](./media/storsimple-restore-from-backup-set/HCS_BackupCatalog.png)

In questa esercitazione viene illustrato come hello toouse **catalogo di Backup** pagina toorestore un volume nel dispositivo da un set di backup.

## <a name="how-toouse-hello-backup-catalog"></a>Come toouse hello catalogo di backup
Hello **catalogo di Backup** pagina fornisce una query che consente di toonarrow la selezione di set di backup. È possibile filtrare hello set di backup che vengono recuperati in base a hello seguenti parametri:

* **Dispositivo** : dispositivo hello in cui hello è stato creato il set di backup.
* **Criteri di backup** o **volume** : hello criteri di backup o di volume associato a questo set di backup.
* **Da** e **a** : hello intervallo di data e ora, quando i set di backup hello è stato creato.

Hello set di backup filtrati possono quindi essere caratterizzati in base a hello gli attributi seguenti:

* **Nome** : hello nome del criterio di backup hello o volume associato al set di backup hello.
* **Dimensioni** : hello dimensioni effettive hello del set di backup.
* **Creare in** : hello data e l'ora di creazione dei backup hello. 
* **Tipo** : i set di backup possono essere snapshot in locale o del cloud. Uno snapshot locale è un backup di tutti i dati di volume archiviati localmente nel dispositivo hello, mentre uno snapshot nel cloud si riferisce toohello backup dei dati di volume che risiedono nel cloud hello. Gli snapshot in locale forniscono un accesso più rapido, mentre gli snapshot del cloud vengono scelti per la resilienza dei dati.
* **Avviato da** : hello backup possono essere avviati automaticamente in base tooa pianificazione o manualmente dall'utente. (È possibile utilizzare i backup tooschedule un criterio di backup. In alternativa, è possibile utilizzare hello **eseguire backup** opzione tootake un backup interattivo.)

## <a name="how-toorestore-your-storsimple-volume-from-a-backup"></a>Come toorestore il volume StorSimple da un backup
È possibile utilizzare hello **catalogo di Backup** pagina toorestore il volume StorSimple da un backup specifico. 

> [!WARNING]
> Ripristino da un backup sostituirà i volumi esistenti da un backup hello hello. Questo può causare la perdita di hello di tutti i dati dopo che è stato eseguito il backup di hello è stato scritto.
> 
> 

Prima di avviare un ripristino in un volume, verificare che il volume di hello è offline. Sarà anche necessario innanzitutto tootake hello volume offline hello host e quindi hello dispositivo. Seguire i passaggi di hello in [portare offline un volume](storsimple-manage-volumes.md#take-a-volume-offline). Eseguire hello seguendo i passaggi toorestore un volume da un set di backup.

### <a name="toorestore-from-a-backup-set"></a>toorestore da un set di backup
1. Nella pagina del servizio StorSimple Manager hello, fare clic su hello **catalogo di Backup** scheda.
   
    ![Catalogo di backup](./media/storsimple-restore-from-backup-set/HCS_Restore.png)
2. Procedura di selezione di un set di backup:
   
   1. Selezionare i dispositivi appropriati hello.
   2. Nell'elenco a discesa hello, scegliere hello volumi o criteri di backup per il backup di hello che si desidera tooselect.
   3. Specificare l'intervallo di tempo hello.
   4. Fare clic sull'icona di controllo hello ![icona del segno di spunta](./media/storsimple-restore-from-backup-set/HCS_CheckIcon.png) tooexecute questa query.
      
      Hello i backup associati hello selezionato volumi o criteri di backup dovrebbero essere visualizzato nell'elenco di hello dei set di backup.
3. Espandere i volumi hello set di backup tooview hello associata. Questi volumi devono essere portati offline sull'host di hello e dispositivo prima di poter ripristinare. Seguire i passaggi di hello in [portare offline un volume](storsimple-manage-volumes.md#take-a-volume-offline).
   
   > [!IMPORTANT]
   > Assicurarsi di avere eseguito hello volumi sull'host hello in primo luogo, prima di portare offline i volumi di hello sul dispositivo hello. Se non si adotta volumi hello offline nell'host di hello, potenzialmente provocare il danneggiamento toodata.
   > 
   > 
4. Selezionare un set di backup. Fare clic su **ripristinare** nella parte inferiore di hello della pagina hello.
5. Verrà richiesto di confermare. 
   
    ![Pagina di conferma](./media/storsimple-restore-from-backup-set/HCS_ConfirmRestore.png)
6. Esaminare le informazioni di ripristino hello e fare clic sull'icona di controllo hello ![il segno di spunta](./media/storsimple-restore-from-backup-set/HCS_CheckIcon.png). Verrà avviato un processo di ripristino che è possibile visualizzare accedendo hello **processi** pagina. 
7. Dopo il ripristino di hello, è possibile verificare che il contenuto di hello dei volumi è sostituito dai volumi backup hello.

![Video disponibile](./media/storsimple-restore-from-backup-set/Video_icon.png)**Video disponibile**

Fare clic su un video che illustra come usare clone hello e ripristinare le funzionalità nei file eliminato toorecover StorSimple, toowatch [qui](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/).

## <a name="next-steps"></a>Passaggi successivi
* Informazioni su come troppo[volumi StorSimple gestire](storsimple-manage-volumes.md).
* Informazioni su come troppo[utilizzare hello tooadminister servizio StorSimple Manager dispositivo StorSimple](storsimple-manager-service-administration.md).

