---
title: un volume StorSimple da backup aaaRestore | Documenti Microsoft
description: Viene illustrato come toouse hello toorestore pagina di StorSimple Manager servizio catalogo di Backup un volume StorSimple da un set di backup.
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 6f289c39-96c7-4d57-b68a-4bc2e99aef9d
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 03/22/2017
ms.author: alkohli
ms.openlocfilehash: c2e38765e750749f5764b5cbf2167d3cd5edfe5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="restore-a-storsimple-volume-from-a-backup-set-update-2"></a>Ripristinare un volume StorSimple da un set di backup (aggiornamento 2)
[!INCLUDE [storsimple-version-selector-restore-from-backup](../../includes/storsimple-version-selector-restore-from-backup.md)]

## <a name="overview"></a>Panoramica
Hello **catalogo di Backup** pagina vengono visualizzati tutti i set di backup di hello che vengono creati quando sono stati eseguiti backup manuali o automatizzati. Utilizzare toolist questa pagina e gestire i backup, eseguire il ripristino da un set di backup o clonare un volume.

 ![Pagina catalogo di backup](./media/storsimple-restore-from-backup-set-u2/restore.png)

In questa esercitazione viene illustrato come hello toouse **catalogo di Backup** pagina toorestore del dispositivo da un set di backup.

È possibile ripristinare un volume da un backup locale o cloud. In entrambi i casi, l'operazione di ripristino hello attiva volume hello online immediatamente mentre i dati vengono scaricati in background hello. 

## <a name="before-you-restore"></a>Prima di avviare il ripristino
Prima di iniziare un'operazione di ripristino, è necessario tenere di hello seguenti avvertenze:

* **Portare offline il volume di hello** : portare hello volume offline nell'host sia hello e hello dispositivo prima di avviare l'operazione di ripristino hello. Anche se l'operazione di ripristino di hello attiva automaticamente online volume hello sul dispositivo hello, è necessario riportare manualmente online dispositivo hello in host hello. È possibile portare online volume hello in host hello quando il volume hello è online su dispositivo hello. (Non è necessario toowait fino a quando non viene completata l'operazione di ripristino hello.) Per le procedure, andare troppo[portare offline un volume](storsimple-manage-volumes-u2.md#take-a-volume-offline).
* **Tipo di volume dopo il ripristino** – volumi eliminato vengono ripristinati in base al tipo di hello nello snapshot hello. I volumi aggiunti in locale vengono ripristinati come volumi aggiunti in locale, mentre i volumi a livelli vengono ripristinati come volumi a livelli.
  
    Per i volumi esistenti di tipo di utilizzo del volume hello corrente hello esegue l'override di tipo hello che viene archiviato nello snapshot hello. Ad esempio, se si ripristina un volume da uno snapshot che sia stato eseguito mentre il tipo di volume hello è stata a livelli e che tipo di volume sia in locale bloccata (a causa di operazione di conversione tooa), quindi viene ripristinato il volume di hello come volume aggiunto in locale. Analogamente, se un volume aggiunto in locale esistente viene espanso e successivamente ripristinare da un vecchio snapshot eseguito quando il volume di hello è minore, hello volume ripristinato mantiene dimensioni espanse corrente hello.
  
    Non è possibile convertire un volume da un volume aggiunto in locale tooa volume a livelli o _viceversa_ mentre viene ripristinato il volume di hello. Attendere il termine dell'operazione di ripristino hello e quindi è possibile convertire tipo tooanother di hello volume. Per informazioni sulla conversione di un volume, andare troppo[modificare il tipo di volume hello](storsimple-manage-volumes-u2.md#change-the-volume-type). 
* **Hello dimensioni del volume viene riflessa nel volume ripristinato hello** : si tratta di un fattore importante se si desidera ripristinare un volume aggiunto in locale che è stato eliminato (perché sono stato effettuato il provisioning volumi aggiunti in locale). Assicurarsi di disporre di spazio sufficiente prima di tentare di toorestore un volume aggiunto in locale che in precedenza è stato eliminato. 
* **Durante il processo di ripristino non è possibile espandere un volume** : attendere il termine dell'operazione di ripristino hello prima di tentare di volume hello tooexpand. Per informazioni sull'espansione di un volume, andare troppo[modificare un volume](storsimple-manage-volumes-u2.md#modify-a-volume).
* **È possibile eseguire un backup mentre si esegue il ripristino un volume locale** : per le procedure andare troppo[utilizzare criteri toomanage del servizio StorSimple Manager hello backup](storsimple-manage-backup-policies.md).
* **È possibile annullare un'operazione di ripristino** : se si annulla il processo di ripristino di hello, quindi volume hello viene eseguito il rollback dello stato toohello in cui era prima ripristino hello è stata avviata. Per le procedure, andare troppo[annullare un processo](storsimple-manage-jobs-u2.md#cancel-a-job).

## <a name="how-does-restore-work"></a>Funzionamento del ripristino
Per i dispositivi che eseguono la versione Update 4 o successiva, viene implementato un ripristino basato su mappa termica. Come hello host richiede i dati tooaccess a raggiungere il dispositivo di hello, queste richieste vengono rilevate e viene creato un heatmap. Percentuale elevata comporta i blocchi di dati con calore superiore mentre inferiore frequenza richieste traduce toochunks con calore inferiore. È necessario accedere hello dati almeno due volte toobe contrassegnato come _frequente_. Anche un file modificato viene contrassegnato come _ad accesso frequente_. Dopo aver avviato il ripristino di hello, si verificherà in base alle heatmap hello reidratazione proattiva dei dati. Per le versioni precedenti a Update 4, i dati di hello è stati scaricati durante il ripristino solo l'accesso. 

Il rilevamento basato su mappa termica è abilitato solo per i volumi a livelli, mentre i volumi aggiunti in locale non sono supportati. Ripristino basato su Heatmap inoltre non è supportato quando si clona un dispositivo tooanother volume. Se è presente un'operazione di ripristino sul posto e uno snapshot locale per hello volume toobe ripristinato esiste nel dispositivo hello, quindi è non riattivare (come i dati sono già disponibili in locale). Per impostazione predefinita, quando si ripristina, hello reidratazione i processi vengono avviati che reidratare in modo proattivo i dati in base alle hello heatmap. Nell'aggiornamento 4, i cmdlet di Windows PowerShell possono essere utilizzato tooquery reidratazione processi in esecuzione, annullare un processo di riattivazione e ottenere hello lo stato del processo reidratazione hello.

* `Get-HcsRehydrationJob`-Questo cmdlet Ottiene lo stato di hello del processo reidratazione hello. Viene generato un singolo processo di riattivazione per un volume.
* `Set-HcsRehydrationJob`-Questo cmdlet consente toopause, arrestare e riprendere il processo di riattivazione hello, se la riattivazione hello è in corso. 

Per ulteriori informazioni sui cmdlet di riattivazione, andare troppo[riferimento ai cmdlet di Windows PowerShell per StorSimple](https://technet.microsoft.com/library/dn688168.aspx).

Con la riattivazione automatica, le prestazioni di lettura temporanee sono in genere più elevate. Hello magniutde effettivi miglioramenti dipende da vari fattori, ad esempio il criterio di accesso, varianza dei dati e il tipo di dati. toocancel un processo di riattivazione, è possibile utilizzare i cmdlet di PowerShell hello. Se si desiderano toopermanently disabilita i processi reidratazione per tutti i ripristini future hello, contattare il supporto Microsoft.

## <a name="how-toouse-hello-backup-catalog"></a>Come toouse hello catalogo di backup
Hello **catalogo di Backup** pagina fornisce una query che consente di toonarrow la selezione di set di backup. È possibile filtrare hello set di backup che vengono recuperati in base a hello seguenti parametri:

* **Dispositivo** : dispositivo hello in cui hello è stato creato il set di backup.
* **Criteri di backup** o **volume** : hello criteri di backup o di volume associato a questo set di backup.
* **Da** e **a** : hello intervallo di data e ora, quando i set di backup hello è stato creato.

Hello set di backup filtrati possono quindi essere caratterizzati in base a hello gli attributi seguenti:

* **Nome** : hello nome del criterio di backup hello o volume associato al set di backup hello.
* **Dimensioni** : hello dimensioni effettive hello del set di backup.
* **Creare in** : hello data e l'ora di creazione dei backup hello. 
* **Tipo** : i set di backup possono essere snapshot in locale o del cloud. Uno snapshot locale è un backup di tutti i dati di volume archiviati localmente nel dispositivo hello. Uno snapshot nel cloud si riferisce toohello backup dei dati di volume che risiedono nel cloud hello. Gli snapshot in locale forniscono un accesso più rapido, mentre gli snapshot del cloud vengono scelti per la resilienza dei dati.
* **Avviato da** : hello backup possono essere avviati automaticamente in base tooa pianificazione o manualmente dall'utente. (È possibile utilizzare i backup tooschedule un criterio di backup. In alternativa, è possibile utilizzare hello **eseguire backup** opzione tootake un backup interattivo.)

## <a name="how-toorestore-your-storsimple-volume-from-a-backup"></a>Come toorestore il volume StorSimple da un backup
È possibile utilizzare hello **catalogo di Backup** pagina toorestore il volume StorSimple da un backup specifico. Tenere presente, tuttavia, il ripristino di un volume verrà ripristinato hello volume toohello stato quando è stato eseguito il backup di hello. I dati che è stato aggiunto dopo l'operazione di backup hello verranno persi.

> [!WARNING]
> Ripristino da un backup sostituisce i volumi esistenti da un backup hello hello. Questo può causare la perdita di hello di tutti i dati dopo che è stato eseguito il backup di hello è stato scritto.
> 
> 

### <a name="toorestore-your-volume"></a>toorestore il volume
1. Nella pagina del servizio StorSimple Manager hello, fare clic su hello **catalogo di Backup** scheda.
   
    ![Catalogo di backup](./media/storsimple-restore-from-backup-set-u2/restore.png)
2. Procedura di selezione di un set di backup:
   
   1. Selezionare i dispositivi appropriati hello.
   2. Nell'elenco a discesa hello, scegliere hello volumi o criteri di backup per il backup di hello che si desidera tooselect.
   3. Specificare l'intervallo di tempo hello.
   4. Fare clic sull'icona di controllo hello ![icona del segno di spunta](./media/storsimple-restore-from-backup-set-u2/HCS_CheckIcon.png) tooexecute questa query.
      
      Hello i backup associati hello selezionato volumi o criteri di backup dovrebbero essere visualizzato nell'elenco di hello dei set di backup.
3. Espandere i volumi hello set di backup tooview hello associata. Questi volumi devono essere portati offline sull'host di hello e dispositivo prima di poter ripristinare. Accedere ai volumi hello in hello **contenitori di volumi** pagina e quindi seguire i passaggi di hello in [portare offline un volume](storsimple-manage-volumes-u2.md#take-a-volume-offline) tootake non in linea.
   
   > [!IMPORTANT]
   > Assicurarsi di avere eseguito hello volumi sull'host hello in primo luogo, prima di portare offline i volumi di hello sul dispositivo hello. Se non si adotta volumi hello offline nell'host di hello, potenzialmente provocare il danneggiamento toodata.
   > 
   > 
4. Spostarsi indietro toohello **catalogo di Backup** e selezionare un set di backup.
5. Fare clic su **ripristinare** nella parte inferiore di hello della pagina hello.
6. Viene chiesto di confermare l'operazione. Hello revisione ripristinare le informazioni e quindi selezionare hello casella di controllo di conferma.
   
    ![Pagina di conferma](./media/storsimple-restore-from-backup-set-u2/ConfirmRestore.png)
7. Fare clic sull'icona di controllo hello ![il segno di spunta](./media/storsimple-restore-from-backup-set-u2/HCS_CheckIcon.png). Viene avviato un processo di ripristino. È possibile visualizzare il processo di hello accedendo hello **processi** pagina. 
8. Dopo il ripristino di hello, è possibile verificare che il contenuto di hello dei volumi è sostituito dai volumi backup hello.

![Video disponibile](./media/storsimple-restore-from-backup-set-u2/Video_icon.png)**Video disponibile**

Fare clic su un video che illustra come usare clone hello e ripristinare le funzionalità nei file eliminato toorecover StorSimple, toowatch [qui](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/).

## <a name="if-hello-restore-fails"></a>Se hello ripristino ha esito negativo
Viene visualizzato un avviso se hello Ripristina l'operazione ha esito negativo per qualsiasi motivo. In questo caso, l'aggiornamento hello elenco di backup tooverify che hello backup è ancora valido. Se si esegue il ripristino dal cloud hello hello backup è valido, quindi problemi di connettività problema potrebbero essere causato hello. 

hello toocomplete operazione di ripristino, portare hello volume offline nell'host di hello e ripetere l'operazione di ripristino hello. I dati di volume toohello modifiche che sono stati eseguiti durante il processo di ripristino hello andranno persi.

## <a name="next-steps"></a>Passaggi successivi
* Informazioni su come troppo[volumi StorSimple gestire](storsimple-manage-volumes-u2.md).
* Informazioni su come troppo[utilizzare hello tooadminister servizio StorSimple Manager dispositivo StorSimple](storsimple-manager-service-administration.md).

