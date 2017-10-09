---
title: esercitazione backup di Azure StorSimple Virtual Array aaaMicrosoft | Documenti Microsoft
description: Viene descritto come tooback configurazione di StorSimple Virtual Array condivisioni e volumi.
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: e3cdcd9e-33b1-424d-82aa-b369d934067e
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7a015fd594f8f56c48fab149a2736be9dec2c24b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-shares-or-volumes-on-your-storsimple-virtual-array"></a>Eseguire il backup di condivisioni o volumi nell'array virtuale StorSimple

## <a name="overview"></a>Panoramica

Hello Array virtuale StorSimple è un ibrido cloud archiviazione nel dispositivo virtuale locale che può essere configurato come un file server o server iSCSI. array virtuale Hello consente backup pianificato e manuale di tutti i volumi o condivisioni hello hello utente toocreate sul dispositivo hello. Quando viene configurato come file server, consente anche il ripristino a livello di elemento. In questa esercitazione viene descritto come toocreate pianificata e backup manuali ed eseguire il ripristino a livello di elemento toorestore un file eliminato sull'array virtuale.

Questa esercitazione si applica matrici solo di toohello StorSimple virtuale. Per informazioni sulla 8000 serie, andare troppo[creare un backup per i dispositivi 8000 serie](storsimple-manage-backup-policies-u2.md)

## <a name="back-up-shares-and-volumes"></a>Backup di condivisioni e volumi

I backup garantiscono la protezione temporizzata, migliorano la recuperabilità e riducono al minimo i tempi di ripristino per le condivisioni e i volumi. È possibile eseguire il backup di una condivisione o di un volume sul dispositivo StorSimple in due modi: **Pianificato** o **Manuale**. Ciascuno dei metodi hello è descritto nelle seguenti sezioni hello.

## <a name="change-hello-backup-start-time"></a>Modificare l'ora di inizio backup hello

> [!NOTE]
> In questa versione, i backup pianificati vengono creati tramite un criterio predefinito che viene eseguito quotidianamente in un momento specificato ed esegue il backup di tutti i volumi o condivisioni hello dispositivo hello. Non è possibile toocreate criteri personalizzati per i backup pianificati in questo momento.


L'Array virtuale StorSimple è un criterio di backup predefinito che inizia in corrispondenza di un'ora specificata del giorno (22:30) ed esegue il backup di tutti i volumi o condivisioni hello dispositivo hello una volta al giorno. È possibile modificare il tempo di hello quali avvio del backup hello, ma la frequenza di hello e hello conservazione (che specifica il numero di hello di backup tooretain) non può essere modificato. Durante questi backup, il dispositivo virtuale intera hello viene eseguito il backup. Questo potrebbe potenzialmente hello delle prestazioni del dispositivo hello e influire sui carichi di lavoro hello distribuiti nel dispositivo hello. È pertanto consigliabile pianificare queste operazioni in orari di scarso traffico.

 ora di inizio di toochange hello predefinite di backup, eseguire i passaggi hello hello [portale di Azure](https://portal.azure.com/).

#### <a name="toochange-hello-start-time-for-hello-default-backup-policy"></a>hello toochange ora di inizio per criteri di backup predefinito hello

1. Andare troppo**dispositivi**. verrà visualizzato l'elenco di Hello di dispositivi registrati con il servizio di gestione di dispositivi StorSimple. 
   
    ![passare toodevices](./media/storsimple-virtual-array-backup/changebuschedule1.png)

2. Selezionare e fare clic sul dispositivo. Hello **impostazioni** pannello verrà visualizzato. Andare troppo**Gestisci > Criteri di Backup**.
   
    ![selezionare il dispositivo](./media/storsimple-virtual-array-backup/changebuschedule2.png)

3. In hello **criteri di Backup** pannello, ora di inizio predefinita hello è 22:30. È possibile specificare hello nuova ora di inizio per la pianificazione giornaliera hello nel fuso orario del dispositivo.
   
    ![passare toobackup criteri](./media/storsimple-virtual-array-backup/changebuschedule5.png)

4. Fare clic su **Salva**.

### <a name="take-a-manual-backup"></a>Creazione di un backup manuale

Inoltre tooscheduled backup, è possibile eseguire un backup manuale (su richiesta) di dati del dispositivo in qualsiasi momento.

#### <a name="toocreate-a-manual-backup"></a>toocreate un backup manuale

1. Andare troppo**dispositivi**. Selezionare il dispositivo e fare doppio clic su **...**  all'estrema destra hello nella riga selezionata hello. Selezionare il menu di scelta rapida hello **eseguire backup**.
   
    ![passare tootake backup](./media/storsimple-virtual-array-backup/takebackup1m.png)

2. In hello **eseguire backup** pannello, fare clic su **eseguire backup**. Si eseguirà il backup tutte le condivisioni in file server di hello hello o tutti i volumi di hello del server iSCSI. 
   
    ![avvio di backup](./media/storsimple-virtual-array-backup/takebackup2m.png)
   
    Viene avviato un backup su richiesta e visualizzata una notifica indicante che il processo di backup è in corso.
   
    ![avvio di backup](./media/storsimple-virtual-array-backup/takebackup3m.png) 
   
    Al termine il processo di hello, ricevono una notifica nuovamente. processo di backup di Hello viene quindi avviato.
   
    ![processo di backup creato](./media/storsimple-virtual-array-backup/takebackup4m.png)

3. stato di avanzamento hello tootrack di backup hello ed esaminare i dettagli dei processi hello, fare clic su notifica hello. Consente di andare troppo **dettagli del processo**.
   
     ![dettagli del processo di backup](./media/storsimple-virtual-array-backup/takebackup5m.png)

4. Dopo il backup di hello è completo, andare troppo**gestione > catalogo di Backup**. Verrà visualizzato uno snapshot nel cloud di tutte le condivisioni di hello (o i volumi) nel dispositivo.
   
    ![Backup completato](./media/storsimple-virtual-array-backup/takebackup19m.png) 

## <a name="view-existing-backups"></a>Visualizzare i backup esistenti
tooview hello i backup esistenti, eseguire operazioni nel portale di Azure hello hello.

#### <a name="tooview-existing-backups"></a>backup esistenti tooview

1. Andare troppo**dispositivi** blade. Selezionare e fare clic sul dispositivo. In hello **impostazioni** pannello andare troppo**gestione > catalogo di Backup**.
   
    ![Passare toobackup catalogo](./media/storsimple-virtual-array-backup/viewbackups1.png)
2. Specificare hello toobe criteri utilizzato per il filtro seguente:
   
    - **Intervallo di tempo**: può essere **Ultima ora**, **Ultime 24 ore**, **Ultimi 7 giorni**, **Ultimi 30 giorni**, **Ultimo anno** e **Data personalizzata**.
    
    - **Dispositivi** : selezionare dall'elenco di hello del file server o server iSCSI registrati con il servizio di gestione di dispositivi StorSimple.
   
    - **Avviato**: può essere **Pianificato** automaticamente tramite criteri di backup o avviato **Manualmente** dall'utente.
   
    ![Filtro backup](./media/storsimple-virtual-array-backup/viewbackups2.png)

3. Fare clic su **Apply**. Hello elenco filtrato di backup viene visualizzato in hello **catalogo di Backup** blade. Si noti che è possibile visualizzare solo 100 elementi di backup alla volta.
   
    ![Catalogo di backup aggiornato](./media/storsimple-virtual-array-backup/viewbackups3.png)

## <a name="next-steps"></a>Passaggi successivi

Scoprire di più su come [amministrazione StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).

