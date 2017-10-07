---
title: un backup di StorSimple Virtual Array aaaClone | Documenti Microsoft
description: Informazioni su come tooclone una copia di backup e ripristinare un file dall'Array virtuale StorSimple.
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: af6e979c-55e3-477c-b53e-a76a697f80c9
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/21/2016
ms.author: alkohli
ms.openlocfilehash: 21bfcae48ee07762179cf00ce842b6094abe18ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="clone-from-a-backup-of-your-storsimple-virtual-array"></a>Clonare da un backup dell'array virtuale StorSimple

## <a name="overview"></a>Panoramica

Questo articolo descrive come tooclone un set di backup dei volumi di condivisioni in Microsoft Azure StorSimple Virtual matrice dettagliate. backup clonato Hello è toorecover utilizzato un file eliminato o perso. articolo Hello include anche i passaggi dettagliati tooperform che un ripristino a livello di elemento nella matrice virtuale StorSimple configurato come un file server.

## <a name="clone-shares-from-a-backup-set"></a>Clonare condivisioni da un set di backup

**Prima di provare tooclone condivisioni, assicurarsi di disporre di sufficiente spazio su hello dispositivo toocomplete questa operazione.** tooclone da un backup, in hello [portale di Azure](https://portal.azure.com/), eseguire hello alla procedura seguente.

#### <a name="tooclone-a-share"></a>tooclone una condivisione

1. Sfoglia troppo**dispositivi** blade. Selezionare e fare clic sul dispositivo, quindi fare clic su **Condivisioni**. Selezionare condivisione hello che si desidera tooclone, hello condivisione tooinvoke hello menu di scelta rapida. Selezionare **Clona**.
   
   ![Clonare un backup](./media/storsimple-virtual-array-clone/cloneshare1.png)
2. In hello **Clone** pannello, fare clic su **Backup > selezionare** e quindi hello seguenti: 
   
   a.    Filtrare un backup su questo dispositivo in base all'intervallo di tempo hello. È possibile scegliere tra **Ultimi 7 giorni**, **Ultimi 30 giorni** e **Ultimo anno**.
   
   b.    Nell'elenco di hello di backup filtrati visualizzato, selezionare un tooclone dal backup.
   
   c.    Fare clic su **OK**.
   
   ![Clonare un backup](./media/storsimple-virtual-array-clone/cloneshare3.png)
3. In hello **Clone** pannello, fare clic su **le impostazioni di destinazione** e quindi hello seguenti:
   
   a.    Fornire un nome per la condivisione. nome della condivisione Hello deve contenere 3 e 127 caratteri.
   
   b.    Facoltativamente, fornire una descrizione per la condivisione di hello clonato.
   
   c.    È possibile modificare il tipo di hello della condivisione hello che si esegue il ripristino. Una condivisione a livelli viene clonata come condivisione a livelli e una condivisione aggiunta in locale come una condivisione aggiunta in locale.
   
   d.    capacità di Hello è impostata come dimensione toohello uguale della condivisione di hello da che la clonazione.
   
   e.    Assegnare gli amministratori di hello per questa condivisione. Dopo aver completato il clone hello sarà toomodify in grado di proprietà della condivisione hello tramite Esplora File.
   
   f.    Fare clic su **OK**.
   
   ![Clonare un backup](./media/storsimple-virtual-array-clone/cloneshare6.png)

4. Fare clic su **Clone** toostart un processo di clonazione. Dopo aver completato il processo di hello, viene avviata l'operazione di clonazione hello e si riceve una notifica. lo stato di avanzamento di toomonitor hello del clone, andare toohello **processi** pannello e fare clic su hello tooview processo i dettagli dei processi.
5. Dopo il clone hello viene creato correttamente, passare toohello Indietro **condivisioni** pannello nel dispositivo.
6. È ora possibile visualizzare nuova condivisione di clonato hello in elenco hello delle condivisioni nel dispositivo. Una condivisione a livelli viene clonata come condivisione a livelli e una condivisione aggiunta in locale come una condivisione aggiunta in locale.
   
   ![Clonare un backup](./media/storsimple-virtual-array-clone/cloneshare10.png)

## <a name="clone-volumes-from-a-backup-set"></a>Clonare volumi da un set di backup

tooclone da un backup, nel portale di Azure hello è tooperform passaggi simili toohello quelli quando si clona una condivisione. operazione di clonazione Hello cloni hello tooa backup nuovo volume hello stesso dispositivo virtuale. non è possibile clonare tooa altro dispositivo.

#### <a name="tooclone-a-volume"></a>tooclone un volume

1. Sfoglia troppo**dispositivi** blade. Selezionare e fare clic sul dispositivo e quindi fare clic su **Volumi**. Selezionare il volume hello che si desidera tooclone, hello volume tooinvoke hello menu di scelta rapida. Selezionare **Clona**.
   
   ![Clonare un volume](./media/storsimple-virtual-array-clone/clonevolume1.png)
2. In hello **Clone** pannello, fare clic su **Backup** e quindi hello seguenti: 
   
   a.    Filtrare un backup su questo dispositivo in base all'intervallo di tempo hello. È possibile scegliere tra **Ultimi 7 giorni**, **Ultimi 30 giorni** e **Ultimo anno**. 
   
   b.    Nell'elenco di hello di backup filtrati visualizzato, selezionare un tooclone dal backup.
   
   c.    Fare clic su **OK**.
   
   ![Clonare un backup](./media/storsimple-virtual-array-clone/clonevolume3.png)
3. In hello **Clone** pannello, fare clic su **le impostazioni del volume di destinazione** e quindi hello seguenti:
   
   a. nome del dispositivo Hello viene popolato automaticamente.
   
   b. Specificare un nome di volume per hello **volume clonato**. nome del volume Hello deve contenere 3 too127 caratteri.
   
   c. tipo di volume Hello viene impostata automaticamente volume originale toohello. Un volume a livelli viene clonato come volume a livelli e un volume aggiunto in locale come un volume aggiunto in locale.
   
   d. Per hello **connesso host**, fare clic su **selezionare**.
   
   ![Clonare un backup](./media/storsimple-virtual-array-clone/clonevolume4.png)
4. In hello **connesso host** pannello selezionare da un record esistente o aggiungere un nuovo record. tooadd un nuovo record, è necessario un nome ACR tooprovide e host hello IQN. Fare clic su **Seleziona**.
   
   ![Clonare un backup](./media/storsimple-virtual-array-clone/clonevolume5.png)
5. Fare clic su **Clone** toolaunch un processo di clonazione.
   
   ![Clonare un backup](./media/storsimple-virtual-array-clone/clonevolume6.png)  
6. Dopo aver creato il processo di clonazione hello, la clonazione verrà avviato. Una volta creato il clone hello, viene visualizzato nel Pannello di hello volumi nel dispositivo. Si noti che un volume a livelli viene clonato come volume a livelli e un volume aggiunto in locale come un volume aggiunto in locale.
   
   ![Clonare un backup](./media/storsimple-virtual-array-clone/clonevolume8.png)
7. Una volta volume hello visualizzata online nell'elenco di hello di volumi, volume hello è disponibile per l'utilizzo. Nell'host di iniziatore iSCSI hello, aggiornare l'elenco di hello di destinazioni nella finestra delle proprietà iniziatore iSCSI. Una nuova destinazione che contiene il nome di volume clonato hello dovrebbe essere visualizzato come "inattiva" nella colonna Stato hello.
8. Selezionare la destinazione hello e fare clic su **Connetti**. Dopo aver connesso toohello destinazione iniziatore hello, lo stato di hello debba modificare troppo**connesso**.
9. In hello **Gestione disco** finestra hello volumi montati vengono visualizzati come mostrato nella seguente figura hello. Mouse sul volume hello individuato (fare clic su nome hello del disco), quindi fare clic su **Online**.

> [!IMPORTANT]
> Quando durante il tentativo tooclone un volume o una condivisione da un set di backup, se il processo di clonazione hello non riesce, un volume di destinazione o una condivisione può comunque creato nel portale di hello. È importante eliminare questo volume di destinazione oppure condividere hello portale toominimize i futuri problemi causati da questo elemento.
> 
> 

## <a name="item-level-recovery-ilr"></a>Ripristino a livello di elemento (ILR)

Questa versione introduce hello a livello di elemento ripristino in un Array virtuale StorSimple configurato come un file server. funzionalità di Hello consente toodo ripristino granulare di file e cartelle da un backup nel cloud di hello tutte le condivisioni nel dispositivo StorSimple hello. Gli utenti possono recuperare i file eliminati dai backup recenti con un modello self-service.

Ogni condivisione presenta una *.backups* cartella che contiene i backup più recente di hello. È possibile passare toohello backup desiderata, copiare i file rilevanti e le cartelle dal backup hello e ripristinarli. Questa funzionalità Elimina tooadministrators chiamate per il ripristino dei file dai backup.

1. Quando si esegue hello ILR, è possibile visualizzare i backup hello tramite Esplora File. Fare clic su condivisione hello specifico da toolook al backup hello. Verrà visualizzato un *.backups* cartella creata nella condivisione di hello che archivia tutti i backup di hello. Espandere hello *.backups* backup hello tooview di cartelle. cartella Hello Mostra la visualizzazione esplosa hello dell'intera gerarchia backup di hello. Questa vista viene creata su richiesta e in genere accetta solo un paio di toocreate secondi.
   
   i backup ultime cinque Hello vengono visualizzati in questo modo e possono essere tooperform utilizzato un livello di elemento di ripristino. Hello cinque backup recenti includono entrambi hello pianificata e hello backup manuali.
   
   * **Backup pianificati** denominati &lt;Device name&gt;DailySchedule-YYYYMMDD-HHMMSS-UTC.
   * **Backup manuali** denominati Ad-hoc-YYYYMMDD-HHMMSS-UTC.
     
     ![](./media/storsimple-virtual-array-clone/image14.png)

2. Identificare i backup di hello contenente hello la versione più recente del file hello eliminato. Anche se il nome di cartella hello contiene un timestamp UTC in ognuna delle hello casi precedenti, ora di hello Creazione cartella quali hello è hello dispositivo effettivo ora in cui hello backup avviato. Utilizzare hello cartella timestamp toolocate e identificare i backup hello.

3. Individuare la cartella hello o file hello che si desidera toorestore nel backup hello identificato nel passaggio precedente hello. Nota che è possibile visualizzare solo i file di hello o le cartelle che si dispone di autorizzazioni. Se non è possibile accedere a determinati file o cartelle, contattare un amministratore della condivisione. messaggio per l'amministratore può utilizzare le autorizzazioni di condivisione hello tooedit Esplora File e fornire accesso toohello specifici file o cartella. È consigliabile che hello condivisione amministratore è un gruppo di utenti anziché un singolo utente.

4. Copiare il file hello o hello cartella toohello appropriate per la condivisione nel file server StorSimple.

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni su troppo[amministrare l'Array virtuale StorSimple tramite interfaccia utente web locale hello](storsimple-ova-web-ui-admin.md).

