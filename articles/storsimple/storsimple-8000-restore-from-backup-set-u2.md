---
title: un volume dal backup su una serie StorSimple 8000 aaaRestore | Documenti Microsoft
description: Viene illustrato come toouse hello toorestore catalogo di Backup del servizio di gestione di dispositivi StorSimple un volume StorSimple da un set di backup.
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
ms.date: 05/23/2017
ms.author: alkohli
ms.openlocfilehash: 0fe2e4c23a23c75ce4058a8531356c94c973c6f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="restore-a-storsimple-volume-from-a-backup-set"></a>Ripristinare un volume StorSimple da un set di backup

## <a name="overview"></a>Panoramica

Questa esercitazione vengono descritti l'operazione di ripristino hello eseguita su un dispositivo StorSimple serie 8000 utilizzando un set di backup esistente. Hello utilizzare **catalogo di Backup** pannello toorestore un volume da una variabile locale o backup nel cloud. Hello **catalogo di Backup** pannello vengono visualizzati tutti i set di backup di hello che vengono creati quando sono stati eseguiti backup manuali o automatizzati. operazione di ripristino Hello da un set di backup attiva volume hello online immediatamente mentre i dati vengono scaricati in background hello.

Un'operazione di ripristino di un metodo alternativo toostart è toogo troppo**dispositivi > [dispositivo] > volumi**. In hello **volumi** pannello selezionare un volume, tooinvoke hello menu di scelta rapida, quindi **ripristinare**.

## <a name="before-you-restore"></a>Prima di avviare il ripristino

Prima di avviare un ripristino, è possibile esaminare hello seguenti avvertenze:

* **È necessario portare offline il volume di hello** : portare hello volume offline nell'host sia hello e hello dispositivo prima di avviare l'operazione di ripristino hello. Anche se l'operazione di ripristino di hello attiva automaticamente online volume hello sul dispositivo hello, è necessario riportare manualmente online dispositivo hello in host hello. È possibile portare online volume hello in host hello come volume hello è online su dispositivo hello. (Non è necessario toowait fino a quando non viene completata l'operazione di ripristino hello.) Per le procedure, andare troppo[portare offline un volume](storsimple-8000-manage-volumes-u2.md#take-a-volume-offline).

* **Tipo di volume dopo il ripristino** : volumi eliminato vengono ripristinati in base al tipo di hello nello snapshot hello; ovvero i volumi sono stati aggiunti in locale vengono ripristinati come volumi aggiunti in locale e i volumi che sono stati a livelli vengono ripristinati come i volumi a livelli.

    Per i volumi esistenti di tipo di utilizzo del volume hello corrente hello esegue l'override di tipo hello che viene archiviato nello snapshot hello. Ad esempio, se si ripristina un volume da uno snapshot che sia stato eseguito mentre il tipo di volume hello è stata a livelli e che tipo di volume ora localmente bloccato (scadenza tooa operazione di conversione eseguita), quindi volume hello verrà ripristinato come volume aggiunto in locale. Analogamente, se un volume aggiunto in locale esistente è stato espanso e successivamente ripristinare da un vecchio snapshot eseguito quando il volume di hello è minore, hello volume ripristinato conserverà dimensioni espanse corrente hello.

    È non è possibile convertire un volume da un volume aggiunto in locale tooa volume a livelli o da un tooa volume aggiunto in locale a livelli volume mentre viene ripristinato il volume di hello. Attendere il termine dell'operazione di ripristino hello e quindi è possibile convertire tipo tooanother di hello volume. Per informazioni sulla conversione di un volume, andare troppo[modificare il tipo di volume hello](storsimple-8000-manage-volumes-u2.md#change-the-volume-type). 

* **Hello dimensioni del volume viene riflessa nel volume ripristinato hello** : si tratta di un fattore importante se si desidera ripristinare un volume aggiunto in locale che è stato eliminato (perché sono stato effettuato il provisioning volumi aggiunti in locale). Assicurarsi di disporre di spazio sufficiente prima di tentare di toorestore un volume aggiunto in locale che in precedenza è stato eliminato.

* **Durante il processo di ripristino non è possibile espandere un volume** : attendere il termine dell'operazione di ripristino hello prima di tentare di volume hello tooexpand. Per informazioni sull'espansione di un volume, andare troppo[modificare un volume](storsimple-8000-manage-volumes-u2.md#modify-a-volume).

* **È possibile eseguire un backup durante il ripristino di un volume locale** : per le procedure andare troppo[utilizzare criteri toomanage del servizio gestione di dispositivi StorSimple hello backup](storsimple-8000-manage-backup-policies-u2.md).

* **È possibile annullare un'operazione di ripristino** : se si annulla il processo di ripristino di hello, quindi volume hello verrà rollback toohello stato in cui era prima che si è iniziata l'operazione di ripristino hello. Per le procedure, andare troppo[annullare un processo](storsimple-8000-manage-jobs-u2.md#cancel-a-job).

## <a name="how-does-restore-work"></a>Funzionamento del ripristino

Per i dispositivi che eseguono la versione Update 4 o successiva, viene implementato un ripristino basato su mappa termica. Come hello host richiede i dati tooaccess a raggiungere il dispositivo di hello, queste richieste vengono rilevate e viene creato un heatmap. Percentuale elevata comporta i blocchi di dati con calore superiore mentre inferiore frequenza richieste traduce toochunks con calore inferiore. È necessario accedere hello dati almeno due volte toobe contrassegnato come _frequente_. Anche un file modificato viene contrassegnato come _ad accesso frequente_. Dopo aver avviato il ripristino di hello, si verificherà in base alle heatmap hello reidratazione proattiva dei dati. Per le versioni precedenti a Update 4, i dati di hello viene scaricati durante il ripristino solo l'accesso.

Hello seguenti avvertenze si applica le operazioni di ripristino basato su tooheatmap:

* Il rilevamento basato su mappa termica è abilitato solo per i volumi a livelli, mentre i volumi aggiunti in locale non sono supportati.

* Ripristino basato su Heatmap non è supportato quando si clona un dispositivo tooanother volume. 

* Se è presente un'operazione di ripristino sul posto e uno snapshot locale per hello volume toobe ripristinato esiste nel dispositivo hello, quindi è non riattivare (come i dati sono già disponibili in locale). 

* Per impostazione predefinita, quando si ripristina, hello reidratazione i processi vengono avviati che reidratare in modo proattivo i dati in base alle hello heatmap. 

Nell'aggiornamento 4, i cmdlet di Windows PowerShell possono essere utilizzato tooquery reidratazione processi in esecuzione, annullare un processo di riattivazione e ottenere hello lo stato del processo reidratazione hello.

* `Get-HcsRehydrationJob`-Questo cmdlet Ottiene lo stato di hello del processo reidratazione hello. Viene generato un singolo processo di riattivazione per un volume.

* `Set-HcsRehydrationJob`-Questo cmdlet consente toopause, arrestare e riprendere il processo di riattivazione hello, se la riattivazione hello è in corso.

Per ulteriori informazioni sui cmdlet di riattivazione, andare troppo[riferimento ai cmdlet di Windows PowerShell per StorSimple](https://technet.microsoft.com/library/dn688168.aspx).

Con la riattivazione automatica, le prestazioni di lettura temporanee sono in genere più elevate. Hello magniutde effettivi miglioramenti dipende da vari fattori, ad esempio il criterio di accesso, varianza dei dati e il tipo di dati. 

toocancel un processo di riattivazione, è possibile utilizzare i cmdlet di PowerShell hello. Se si desiderano i processi di reidratazione disable toopermanently per tutti hello ripristini future, [contattare il supporto Microsoft](storsimple-8000-contact-microsoft-support.md).

## <a name="how-toouse-hello-backup-catalog"></a>Come toouse hello catalogo di backup

Hello **catalogo di Backup** pannello fornisce una query che consente di toonarrow la selezione di set di backup. È possibile filtrare hello set di backup che vengono recuperati in base a hello seguenti parametri:

* **Intervallo di tempo** : hello intervallo di data e ora, quando i set di backup hello è stato creato.
* **Dispositivo** : dispositivo hello in cui hello è stato creato il set di backup.
* **Criteri di backup** o **Volume** : hello criteri di backup o di volume associato a questo set di backup.

Hello set di backup filtrati possono quindi essere caratterizzati in base a hello gli attributi seguenti:

* **Nome** : hello nome del criterio di backup hello o volume associato al set di backup hello.
* **Tipo** : i set di backup possono essere snapshot in locale o del cloud. Uno snapshot locale è un backup di tutti i dati di volume archiviati localmente nel dispositivo hello, mentre uno snapshot nel cloud si riferisce toohello backup dei dati di volume che risiedono nel cloud hello. Gli snapshot in locale forniscono un accesso più rapido, mentre gli snapshot del cloud vengono scelti per la resilienza dei dati.
* **Dimensioni** : hello dimensioni effettive hello del set di backup.
* **Creare in** : hello data e l'ora di creazione dei backup hello. 
* **Volumi** -numero di volumi associati al set di backup hello hello.
* **Avviato** : hello backup possono essere avviati automaticamente in base tooa pianificazione o manualmente dall'utente. (È possibile utilizzare i backup tooschedule un criterio di backup. In alternativa, è possibile utilizzare hello **eseguire backup** opzione tootake un backup su richiesta o interattivo..)

## <a name="how-toorestore-your-storsimple-volume-from-a-backup"></a>Come toorestore il volume StorSimple da un backup

È possibile utilizzare hello **catalogo di Backup** pannello toorestore il volume StorSimple da un backup specifico. Tenere presente, tuttavia, il ripristino di un volume verrà ripristinato lo stato di toohello volume hello che si trovava quando è stato eseguito il backup di hello. Tutti i dati che è stato aggiunto dopo l'operazione di backup hello andranno persi.

> [!WARNING]
> Ripristino da un backup sostituirà i volumi esistenti da un backup hello hello. Questo può causare la perdita di hello di tutti i dati dopo che è stato eseguito il backup di hello è stato scritto.


### <a name="toorestore-your-volume"></a>toorestore il volume
1. Il servizio di gestione di dispositivi StorSimple tooyour, quindi fare clic su **catalogo di Backup**.

2. Procedura di selezione di un set di backup:
   
   1. Specificare l'intervallo di tempo hello.
   2. Selezionare i dispositivi appropriati hello.
   3. Nell'elenco a discesa hello, scegliere hello volumi o criteri di backup per il backup di hello che si desidera tooselect.
   4. Fare clic su **applica** tooexecute questa query.

    Hello i backup associati hello selezionato volumi o criteri di backup dovrebbero essere visualizzato nell'elenco di hello dei set di backup.
   
    ![Elenco di set di backup](./media/storsimple-8000-restore-from-backup-set-u2/bucatalog.png)     
     
3. Espandere i volumi hello set di backup tooview hello associata. Questi volumi devono essere portati offline sull'host di hello e dispositivo prima di poter ripristinare. Accedere ai volumi hello in hello **volumi** pannello del dispositivo e quindi hello seguire i passaggi [portare offline un volume](storsimple-8000-manage-volumes-u2.md#take-a-volume-offline) tootake non in linea.
   
   > [!IMPORTANT]
   > Assicurarsi di avere eseguito hello volumi sull'host hello in primo luogo, prima di portare offline i volumi di hello sul dispositivo hello. Se non si adotta volumi hello offline nell'host di hello, potenzialmente provocare il danneggiamento toodata.
   
4. Spostarsi indietro toohello **catalogo di Backup** e selezionare un set di backup. Il pulsante destro e quindi selezionare il menu di scelta rapida hello **ripristinare**.

    ![Elenco di set di backup](./media/storsimple-8000-restore-from-backup-set-u2/restorebu1.png)

5. Verrà richiesto di confermare. Hello revisione ripristinare le informazioni e quindi selezionare hello casella di controllo di conferma.
   
    ![Pagina di conferma](./media/storsimple-8000-restore-from-backup-set-u2/restorebu2.png)

7.  Fare clic su **Ripristina**. Avvia un processo di ripristino che è possibile visualizzare accedendo hello **processi** pagina.

    ![Pagina di conferma](./media/storsimple-8000-restore-from-backup-set-u2/restorebu5.png)

8. Dopo il ripristino di hello, verificare che il contenuto di hello dei volumi è sostituito dai volumi backup hello.


## <a name="if-hello-restore-fails"></a>Se hello ripristino ha esito negativo

Si riceverà un avviso se hello Ripristina l'operazione ha esito negativo per qualsiasi motivo. In questo caso, l'aggiornamento hello elenco di backup tooverify che hello backup è ancora valido. Se si esegue il ripristino dal cloud hello hello backup è valido, quindi problemi di connettività problema potrebbero essere causato hello.

hello toocomplete operazione di ripristino, portare hello volume offline nell'host di hello e ripetere l'operazione di ripristino hello. Si noti che i dati di volume toohello modifiche che sono stati eseguiti durante hello processo di ripristino andrà perso.

## <a name="next-steps"></a>Passaggi successivi
* Informazioni su come troppo[volumi StorSimple gestire](storsimple-8000-manage-volumes-u2.md).
* Informazioni su come troppo[utilizzare hello tooadminister servizio di gestione di dispositivi StorSimple dispositivo StorSimple](storsimple-8000-manager-service-administration.md).

