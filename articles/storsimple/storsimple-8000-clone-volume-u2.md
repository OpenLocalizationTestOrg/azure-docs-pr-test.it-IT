---
title: un volume su StorSimple serie 8000 aaaClone | Documenti Microsoft
description: Descrive l'utilizzo e i tipi di clone diversi hello e viene illustrato come utilizzare tooclone un set di backup di un singolo volume in un dispositivo StorSimple serie 8000.
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
ms.date: 07/26/2017
ms.author: alkohli
ms.openlocfilehash: 4f7e1f62f17c7b2bd72820a00a5ab87b7e192332
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-in-azure-portal-tooclone-a-volume"></a>Utilizzare il servizio di gestione di dispositivi StorSimple hello in tooclone portale Azure un volume

## <a name="overview"></a>Panoramica

In questa esercitazione viene illustrato come utilizzare tooclone un set di backup di un singolo volume tramite hello **catalogo di Backup** blade. Viene inoltre spiegato come differenza hello *temporanei* e *permanente* cloni. linee guida di Hello in questa esercitazione si applicano periferica di serie StorSimple 8000 hello tooall esecuzione Update 3 o versione successiva.

servizio di gestione di dispositivi StorSimple Hello **catalogo di Backup** pannello vengono visualizzati tutti i set di backup di hello che vengono creati quando sono stati eseguiti backup manuali o automatizzati. È quindi possibile selezionare un volume in tooclone un set di backup.

 ![Elenco di set di backup](./media/storsimple-8000-clone-volume-u2/bucatalog.png)

## <a name="considerations-for-cloning-a-volume"></a>Considerazioni per la clonazione di un volume

Prendere in considerazione le seguenti informazioni quando si clona un volume hello.

- Un clone si comporta in hello stesso come un volume normale. Qualsiasi operazione che è possibile in un volume è disponibile per il clone hello.

- Il monitoraggio e il backup predefinito vengono disabilitati automaticamente in un volume clonato. È necessario un volume clonato tooconfigure per tutti i backup.

- Un volume aggiunto in locale viene clonato come volume a livelli. Se è necessario hello toobe volume clonato aggiunto in locale, è possibile convertire volume di hello clone tooa aggiunto in locale dopo l'operazione di clonazione hello è stato completato correttamente. Per informazioni sulla conversione di un tooa volume a livelli localmente aggiunta volume, andare troppo[modificare il tipo di volume hello](storsimple-8000-manage-volumes-u2.md#change-the-volume-type).

- Se si tenta di tooconvert che un volume clonato da toolocally a più livelli bloccato immediatamente dopo la clonazione (quando è ancora un clone temporaneo), conversione di hello non riesce con hello seguente messaggio di errore:

    `Unable toomodify hello usage type for volume {0}. This can happen if hello volume being modified is a transient clone and hasn’t been made permanent. Take a cloud snapshot of this volume and then retry hello modify operation.`

    Questo errore si verifica solo se la clonazione in tooa altro dispositivo. È possibile convertire correttamente hello volume toolocally aggiunto se è prima di convertire un clone permanente hello clone temporaneo tooa. Uno snapshot cloud di hello clone temporaneo tooconvert è tooa un clone permanente.

## <a name="create-a-clone-of-a-volume"></a>Creare un clone di un volume

È possibile creare un clone in hello anche un'applicazione cloud stesso dispositivo o un altro dispositivo utilizzando una variabile locale o snapshot cloud.

procedura Hello riportata di seguito viene descritto come eseguire il backup del catalogo toocreate un clone da hello.  Un clone di un metodo alternativo tooinitiate è toogo troppo**volumi**, selezionare un volume, quindi fare doppio clic su menu di scelta rapida tooinvoke hello e selezionare **Clone**.

Eseguire i seguenti passaggi toocreate un clone del volume di dal catalogo di backup hello hello.

#### <a name="tooclone-a-volume"></a>tooclone un volume

1. Il servizio di gestione di dispositivi StorSimple tooyour, quindi fare clic su **catalogo di Backup**.

2. Procedura di selezione di un set di backup:
   
   1. Selezionare i dispositivi appropriati hello.
   2. Nell'elenco a discesa hello, scegliere hello volumi o criteri di backup per il backup di hello che si desidera tooselect.
   3. Specificare l'intervallo di tempo hello.
   4. Fare clic su **applica** tooexecute questa query.

    Hello i backup associati hello selezionato volumi o criteri di backup dovrebbero essere visualizzato nell'elenco di hello dei set di backup.
   
    ![Elenco di set di backup](./media/storsimple-8000-clone-volume-u2/bucatalog.png)
     
3. Espandere i volumi hello set di backup tooview hello associata. Questi volumi devono essere portati offline sull'host di hello e dispositivo prima di poter ripristinare. Accedere ai volumi hello in hello **volumi** pannello del dispositivo e quindi hello seguire i passaggi [portare offline un volume](storsimple-8000-manage-volumes-u2.md#take-a-volume-offline) tootake non in linea.
   
   > [!IMPORTANT]
   > Assicurarsi di avere eseguito hello volumi sull'host hello in primo luogo, prima di portare offline i volumi di hello sul dispositivo hello. Se non si adotta volumi hello offline nell'host di hello, potenzialmente provocare il danneggiamento toodata.
   
4. Spostarsi indietro toohello **catalogo di Backup** e selezionare un volume in un set di backup. Il pulsante destro e quindi selezionare il menu di scelta rapida hello **Clone**.

   ![Elenco di set di backup](./media/storsimple-8000-clone-volume-u2/clonevol3b.png) 

3. In hello **Clone** pannello hello i passaggi seguenti:
   
    1. Identificare un dispositivo di destinazione. Questo è il percorso di hello in cui verrà creato il clone hello. È possibile scegliere hello stesso dispositivo o specificare un altro dispositivo.

      > [!NOTE]
      > Assicurarsi che la capacità di hello richiesta per il clone hello è inferiore rispetto alla capacità di hello disponibile nel dispositivo di destinazione hello.
       
    2. Specificare un nome volume univoco per il clone. nome Hello deve essere compresa tra 3 e 127 caratteri.
      
        > [!NOTE]
        > Hello **Clone Volume come** campo sarà **a livelli** anche se la clonazione di un volume aggiunto in locale. Non è possibile modificare questa impostazione. Tuttavia, se è necessario hello toobe volume clonato anche aggiunto in locale, è possibile convertire volume di hello clone tooa aggiunto in locale dopo aver creato correttamente clone hello. Per informazioni sulla conversione di un tooa volume a livelli localmente aggiunta volume, andare troppo[modificare il tipo di volume hello](storsimple-8000-manage-volumes-u2.md#change-the-volume-type).
          
    3. In **connesso host**, specificare un record di controllo di accesso (ACR) per il clone hello. È possibile aggiungere un nuovo ACR o selezionare dall'elenco esistente di hello. Hello ACR determineranno quali host possono accedere ai clone.
      
        ![Elenco di set di backup](./media/storsimple-8000-clone-volume-u2/clonevol3a.png) 

    4. Fare clic su **Clone** operazione hello toocomplete.

4. Viene avviato un processo di clonazione e ricevere notifiche quando clone hello viene creato correttamente. Fare clic sulla notifica del processo hello o andare troppo**processi** processo di clonazione hello toomonitor blade.

    ![Elenco di set di backup](./media/storsimple-8000-clone-volume-u2/clonevol5.png)

7. Dopo aver completato il processo di clonazione hello, andare tooyour dispositivo e quindi fare clic su **volumi**. Nell'elenco di hello di volumi, dovrebbe essere clone hello appena creata in hello stesso contenitore del volume contenente il volume di origine hello.

    ![Elenco di set di backup](./media/storsimple-8000-clone-volume-u2/clonevol6.png)

Un clone creato in questo modo è un clone temporaneo. Per ulteriori informazioni sui tipi di cloni, vedere [Cloni temporanei e cloni permanenti](#transient-vs-permanent-clones).


## <a name="transient-vs-permanent-clones"></a>Cloni temporanei e cloni permanenti
I cloni temporanei vengono creati solo quando si clona tooanother dispositivo. È possibile clonare un volume specifico da un set di backup tooa altro dispositivo gestito da Gestione dispositivi StorSimple hello. nel volume originale hello riferimenti toohello dati clone temporaneo Hello che utilizza tale tooread dati e la scrittura in locale nel dispositivo di destinazione hello.

Dopo l'esecuzione di uno snapshot nel cloud di un clone temporaneo, clone risultante hello è un *permanente* clone. Durante questo processo, una copia dei dati hello viene creata nel cloud hello e hello toocopy ora che questi dati sono determinati dalle dimensioni hello dei dati hello e hello Azure latenze (si tratta di una copia di Azure in Azure). Questo processo può richiedere giorni tooweeks. clone temporaneo Hello diventa un clone permanente e non dispone di tutti i riferimenti toohello originale volume i dati da cui è stato clonato.

## <a name="scenarios-for-transient-and-permanent-clones"></a>Scenari per cloni temporanei e cloni permanenti
Hello le sezioni seguenti descrivono situazioni di esempio in cui è possibile utilizzare i cloni temporanei e permanenti.

### <a name="item-level-recovery-with-a-transient-clone"></a>Ripristino a livello di elemento con un clone temporaneo
È necessario un file di presentazione di Microsoft PowerPoint uno anni toorecover. L'amministratore IT identifica hello di backup specifico da quel momento e quindi filtri hello volume. Hello amministratore quindi Clona volume hello, individua il file hello che si sta cercando e glielo tooyou. In questo scenario viene utilizzato un clone temporaneo.

### <a name="testing-in-hello-production-environment-with-a-permanent-clone"></a>Test nell'ambiente di produzione hello con un clone permanente
È necessario un bug di testing nell'ambiente di produzione hello tooverify. Creare un clone del volume hello nell'ambiente di produzione hello e quindi eseguire uno snapshot cloud di questo toocreate clone un volume clonato indipendente. In questo scenario viene utilizzato un clone permanente.

## <a name="next-steps"></a>Passaggi successivi
* Informazioni su come troppo[ripristinare un volume StorSimple da un set di backup](storsimple-8000-restore-from-backup-set-u2.md).
* Informazioni su come troppo[utilizzare hello tooadminister servizio di gestione di dispositivi StorSimple dispositivo StorSimple](storsimple-8000-manager-service-administration.md).

