---
title: aaaClone volume serie StorSimple 8000 | Documenti Microsoft
description: "Vengono descritti i tipi di clone diversi hello e quando toouse e viene spiegato come è possibile utilizzare tooclone un set di backup di un singolo volume."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 070ac53e-7388-4c48-b8a5-8ed7f9108b2c
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/26/2017
ms.author: alkohli
ms.openlocfilehash: f457625d2e3aa173f7ccf26984e1902a64e33b5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-tooclone-a-volume-update-2"></a>Utilizzare tooclone di servizio StorSimple Manager hello (Update 2) un volume
[!INCLUDE [storsimple-version-selector-clone-volume](../../includes/storsimple-version-selector-clone-volume.md)]

## <a name="overview"></a>Panoramica
servizio StorSimple Manager Hello **catalogo di Backup** pagina vengono visualizzati tutti i set di backup di hello che vengono creati quando sono stati eseguiti backup manuali o automatizzati. È possibile utilizzare tutti i backup hello di toolist questa pagina per un criterio di backup o un volume, seleziona o eliminare i backup, o utilizzare un backup toorestore o clonare un volume.

![Pagina catalogo di backup](./media/storsimple-clone-volume-u2/backupCatalog.png)  

In questa esercitazione viene illustrato come utilizzare tooclone un set di backup di un singolo volume. Viene inoltre spiegato come differenza hello *temporanei* e *permanente* cloni.

> [!NOTE]
> Un volume aggiunto in locale verrà duplicato come volume a livelli. Se è necessario hello toobe volume clonato aggiunto in locale, è possibile convertire volume di hello clone tooa aggiunto in locale dopo l'operazione di clonazione hello è stato completato correttamente. Per informazioni sulla conversione di un tooa volume a livelli localmente aggiunta volume, andare troppo[modificare il tipo di volume hello](storsimple-manage-volumes-u2.md#change-the-volume-type).
> 
> Se si tenta di tooconvert che un volume clonato da toolocally a più livelli bloccato immediatamente dopo la clonazione (quando è ancora un clone temporaneo), conversione hello avrà esito negativo con hello seguente messaggio di errore:
> 
> `Unable toomodify hello usage type for volume {0}. This can happen if hello volume being modified is a transient clone and hasn’t been made permanent. Take a cloud snapshot of this volume and then retry hello modify operation.` 
> 
> Questo errore si verifica solo se la clonazione in tooa altro dispositivo. È possibile convertire correttamente hello volume toolocally aggiunto se è prima di convertire un clone permanente hello clone temporaneo tooa. tooconvert hello clone temporaneo tooa permanente clonare, eseguire uno snapshot cloud di esso.
> 
> 

## <a name="create-a-clone-of-a-volume"></a>Creare un clone di un volume
È possibile creare un clone in hello stesso dispositivo, un altro dispositivo o persino una macchina virtuale tramite una variabile locale o snapshot cloud.

#### <a name="tooclone-a-volume"></a>tooclone un volume
1. Nella pagina del servizio StorSimple Manager hello, fare clic su hello **catalogo di Backup** e selezionare un set di backup.
2. Espandere i volumi hello set di backup tooview hello associata. Selezionare un volume dal set di backup hello.
   
     ![Clonare un volume](./media/storsimple-clone-volume-u2/CloneVol.png) 
3. Fare clic su **Clone** toobegin clonare il volume di hello selezionato.
4. Nella procedura guidata Clona Volume hello in **specificare nome e percorso**:
   
   1. Identificare un dispositivo di destinazione. Questo è il percorso di hello in cui verrà creato il clone hello. È possibile scegliere hello stesso dispositivo o specificare un altro dispositivo. Se si sceglie un volume associato altri provider di servizi cloud hello (non Azure), elenco a discesa elenco per il dispositivo di destinazione hello visualizzerà soltanto i dispositivi fisici. Non è possibile clonare un volume associato con altri provider di servizi cloud in un dispositivo virtuale.
      
      > [!NOTE]
      > Assicurarsi che la capacità di hello richiesta per il clone hello è inferiore rispetto alla capacità di hello disponibile nel dispositivo di destinazione hello.
      > 
      > 
   2. Specificare un nome volume univoco per il clone. nome Hello deve essere compresa tra 3 e 127 caratteri. 
      
      > [!NOTE]
      > Hello **Clone Volume come** campo sarà **a livelli** anche se la clonazione di un volume aggiunto in locale. Non è possibile modificare questa impostazione. Tuttavia, se è necessario hello toobe volume clonato anche aggiunto in locale, è possibile convertire volume di hello clone tooa aggiunto in locale dopo aver creato correttamente clone hello. Per informazioni sulla conversione di un tooa volume a livelli localmente aggiunta volume, andare troppo[modificare il tipo di volume hello](storsimple-manage-volumes-u2.md#change-the-volume-type).
      > 
      > 
      
        ![Clonazione guidata 1](./media/storsimple-clone-volume-u2/clone1.png) 
   3. Fare clic sull'icona di freccia hello ![icona a forma di freccia](./media/storsimple-clone-volume-u2/HCS_ArrowIcon.png) tooproceed toohello la pagina successiva.
5. In **Specificare gli host che possono utilizzare questo volume**:
   
   1. Specificare un record di controllo di accesso (ACR) per il clone hello. È possibile aggiungere un nuovo ACR o selezionare dall'elenco esistente di hello.
      
        ![Clonazione guidata 2](./media/storsimple-clone-volume-u2/clone2.png) 
   2. Fare clic sull'icona di controllo hello ![icona del segno di spunta](./media/storsimple-clone-volume-u2/HCS_CheckIcon.png)operazione di hello toocomplete.
6. Verrà avviato un processo di clonazione e riceverà una notifica quando viene creato correttamente clone hello. Fare clic su **Visualizza processo** toomonitor processo di clonazione hello in hello **processi** pagina. Verrà visualizzato hello segue messaggio al termine il processo di clonazione hello:
   
    ![Messaggio clone](./media/storsimple-clone-volume-u2/CloneMsg.png) 
7. Dopo aver hello processo di clonazione è completata:
   
   1. Passare toohello **dispositivi** pagina e seleziona hello **contenitori di volumi** scheda. 
   2. Selezionare contenitore del volume hello associato al volume di origine hello che è stato clonato. Nell'elenco di hello di volumi, dovrebbe essere clone hello appena creato.

> [!NOTE]
> Il monitoraggio e il backup predefinito vengono disabilitati automaticamente in un volume clonato.
> 
> 

Un clone creato in questo modo è un clone temporaneo. Per ulteriori informazioni sui tipi di cloni, vedere [Cloni temporanei e cloni permanenti](#transient-vs-permanent-clones).

Questo clone è ora un volume normale e qualsiasi operazione che è possibile in un volume saranno disponibili per il clone hello. Sarà necessario tooconfigure questo volume per tutti i backup.

## <a name="transient-vs-permanent-clones"></a>Cloni temporanei e cloni permanenti
I cloni temporanei vengono creati solo durante la clonazione tooa altro dispositivo. È possibile clonare un volume specifico da un set di backup tooa altro dispositivo gestito da hello StorSimple Manager. clone temporaneo Hello verrà hanno riferimenti toohello dati nel volume originale hello e verranno utilizzare tale tooread dati e scrivere localmente nel dispositivo di destinazione hello. 

Dopo l'esecuzione di uno snapshot nel cloud di un clone temporaneo, clone risultante hello sarà un *permanente* clone. Durante questo processo, una copia dei dati hello viene creata nel cloud hello e hello toocopy ora che questi dati sono determinati dalle dimensioni hello dei dati hello e hello Azure latenze (si tratta di una copia di Azure in Azure). Questo processo può richiedere giorni tooweeks. clone temporaneo Hello diventa un clone permanente in questo modo e non dispone di tutti i riferimenti toohello originale volume i dati da cui è stato clonato. 

## <a name="scenarios-for-transient-and-permanent-clones"></a>Scenari per cloni temporanei e cloni permanenti
Hello le sezioni seguenti descrivono situazioni di esempio in cui è possibile utilizzare i cloni temporanei e permanenti.

### <a name="item-level-recovery-with-a-transient-clone"></a>Ripristino a livello di elemento con un clone temporaneo
È necessario un file di presentazione di Microsoft PowerPoint uno anni toorecover. L'amministratore IT identifica hello di backup specifico da tale periodo di tempo e quindi filtri hello volume. Hello amministratore quindi Clona volume hello, individua il file hello che si sta cercando e glielo tooyou. In questo scenario viene utilizzato un clone temporaneo. 

![Video disponibile](./media/storsimple-clone-volume-u2/Video_icon.png)**Video disponibile**

Fare clic su un video che illustra come usare clone hello e ripristinare le funzionalità nei file eliminato toorecover StorSimple, toowatch [qui](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/).

### <a name="testing-in-hello-production-environment-with-a-permanent-clone"></a>Test nell'ambiente di produzione hello con un clone permanente
È necessario un bug di testing nell'ambiente di produzione hello tooverify. Creare un clone del volume hello nell'ambiente di produzione hello e quindi eseguire uno snapshot cloud di questo toocreate clone un volume clonato indipendente. In questo scenario viene utilizzato un clone permanente.  

## <a name="next-steps"></a>Passaggi successivi
* Informazioni su come troppo[ripristinare un volume StorSimple da un set di backup](storsimple-restore-from-backup-set-u2.md).
* Informazioni su come troppo[utilizzare hello tooadminister servizio StorSimple Manager dispositivo StorSimple](storsimple-manager-service-administration.md).

