---
title: aaaStorSimple Array virtuale disaster recovery e failover del dispositivo | Documenti Microsoft
description: Per ulteriori informazioni su toofailover l'Array virtuale StorSimple.
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 3c1f9c62-af57-4634-a0d8-435522d969aa
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5f125efd1ffb94489cdfa7cfaafae7d57cc10131
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="disaster-recovery-and-device-failover-for-your-storsimple-virtual-array-via-azure-portal"></a>Ripristino di emergenza e failover del dispositivo per l'array virtuale StorSimple tramite il portale di Azure

## <a name="overview"></a>Panoramica
Questo articolo descrive il ripristino di emergenza hello per Microsoft Azure Array virtuale di StorSimple inclusi hello dettagliato le fasi toofail array virtuale tooanother. Toomove consente il failover dei dati da un *origine* dispositivo in hello datacenter tooa *destinazione* dispositivo. Hello dispositivo di destinazione può essere situato in hello stesso o in una posizione geografica diversa. failover del dispositivo Hello è per l'intero dispositivo hello. Durante il failover, i dati di cloud hello per dispositivo di origine hello cambiano toothat di proprietà del dispositivo di destinazione hello.

Questo articolo è applicabile tooStorSimple solo matrici virtuali. toofail su un dispositivo 8000 serie, andare troppo[dispositivo failover e ripristino di emergenza del dispositivo StorSimple](storsimple-device-failover-disaster-recovery.md).

## <a name="what-is-disaster-recovery-and-device-failover"></a>Che cos'è failover del dispositivo e il ripristino di emergenza?

In uno scenario di ripristino di emergenza di emergenza nel dispositivo primario hello smette di funzionare. In questo scenario, è possibile spostare i dati di cloud hello associati alla periferica tooanother di hello dispositivo non riuscita. È possibile utilizzare nel dispositivo primario hello come hello *origine* e specificare un altro dispositivo come hello *destinazione*. Questo processo è noto tooas hello *failover*. Durante il failover, tutte hello volumi o condivisioni hello hello dispositivo di origine modificare la proprietà e sono trasferiti toohello dispositivo di destinazione. Nessun filtro dei dati hello è consentito.

Ripristino di emergenza è modellata come un ripristino del dispositivo completo utilizzando calore hello mappa basata su più livelli e il rilevamento. Una mappa di calore viene definita tramite l'assegnazione di un toohello valore calore dati basati su lettura e scrittura di modelli. Eseguire il mapping questo calore quindi livelli hello innanzitutto più basso calore dati blocchi toohello cloud mantenendo i blocchi di dati elevata calore (più utilizzato) hello nel livello locale hello. Durante un ripristino di emergenza, StorSimple Usa toorestore mappa di calore hello e riattivare dati hello dal cloud hello. dispositivo Hello recupera tutti i volumi o condivisioni hello in hello ultima copia di backup recente (come stabilito internamente) ed esegue un ripristino da backup. array virtuale Hello gestisce l'intero processo di ripristino di emergenza hello.

> [!IMPORTANT]
> dispositivo di origine Hello viene eliminato alla fine di hello del failover del dispositivo e pertanto non è supportato un failback.
> 
> 

Ripristino di emergenza viene gestito tramite funzionalità di failover di hello dispositivo e può essere avviato da hello **dispositivi** blade. Questo pannello raccoglie servizio tutti hello StorSimple dispositivi tooyour connesso dispositivo StorSimple Manager. Per ogni dispositivo, è possibile vedere nome descrittivo hello, stato, capacità disponibile e massima, tipo e modello.

## <a name="prerequisites-for-device-failover"></a>Prerequisiti per il failover del dispositivo

### <a name="prerequisites"></a>Prerequisiti

Per un failover del dispositivo, verificare che hello seguenti prerequisiti siano soddisfatti:

* dispositivo di origine Hello deve toobe in un **Deactivated** stato.
* Hello dispositivo di destinazione deve tooshow backup come **pronto tooset backup** in hello portale di Azure. Eseguire il provisioning di un array virtuale di destinazione di hello capacità uguale o superiore. Utilizzare tooconfigure di interfaccia utente web locale hello e registrare correttamente array virtuale di destinazione hello.
  
  > [!IMPORTANT]
  > Non tentare tooconfigure hello virtuale dispositivo registrato tramite il servizio di hello. Nessuna configurazione del dispositivo deve essere eseguita tramite il servizio di hello.
  > 
  > 
* dispositivo di destinazione Hello devono avere lo stesso nome come dispositivo di origine hello hello.
* dispositivo di origine e destinazione Hello ha toobe hello stesso tipo. È possibile eseguire failover solo un array virtuale configurato come un file server tooanother file server. Hello stesso vale per un server iSCSI.
* Per un file server di ripristino di emergenza, è consigliabile unire in join toohello dispositivo di destinazione hello origine hello nello stesso dominio. Questa configurazione assicura che le autorizzazioni di condivisione hello vengono risolte automaticamente. Solo hello failover tooa dispositivo di destinazione in hello nello stesso dominio.
* i dispositivi di destinazione disponibili Hello per ripristino di emergenza sono dispositivi che hanno hello uguale o maggiore capacità rispetto toohello dispositivo di origine. Hello i dispositivi che sono connessi tooyour servizio ma che non soddisfano hello criteri di spazio sufficiente non sono disponibili come dispositivi di destinazione.

### <a name="other-considerations"></a>Altre considerazioni

* Per un failover pianificato 
  
  * Si consiglia di eseguire tutti i volumi di hello o condivisioni nel dispositivo di origine hello offline.
  * Si consiglia di eseguire un backup del dispositivo hello e quindi procedere con perdita di dati toominimize hello failover. 
* Per un failover non pianificato, il dispositivo di hello utilizza i dati più recenti backup toorestore hello hello.

### <a name="device-failover-prechecks"></a>Verifiche preliminari del failover del dispositivo

Prima di hello che avvia ripristino di emergenza, il dispositivo hello esegue prechecks. Queste verifiche consentono di ridurre il rischio di errori all'avvio del ripristino di emergenza. Hello prechecks includono:

* Convalida dell'account di archiviazione hello.
* Controllo hello tooAzure di connettività cloud.
* Verifica dello spazio disponibile nel dispositivo di destinazione hello.
* Per un volume di un dispositivo di origine del server iSCSI verifica della validità
  
  * dei nomi relativi a record di controllo di accesso validi
  * di IQN (lunghezza non superiore a 220 caratteri)
  * e di password CHAP (lunghezza di 12 e 16 caratteri).

Se uno di hello prechecks precedente non riesce, è possibile procedere con hello ripristino di emergenza. Risolvere questi problemi, quindi riprovare il ripristino di emergenza.

Al termine hello ripristino di emergenza, proprietà hello dei dati di cloud di hello sul dispositivo di origine hello è toohello trasferiti dispositivo di destinazione. dispositivo di origine Hello quindi non è più disponibile nel portale di hello. Accesso tooall hello volumi o condivisioni nel dispositivo di origine hello è bloccata e il dispositivo di destinazione hello diventa attivo.

> [!IMPORTANT]
> Se il dispositivo di hello non è più disponibile, hello macchina virtuale in cui è eseguito il provisioning nel sistema host hello è utilizzano risorse. Al termine del ripristino di emergenza hello correttamente, è possibile eliminare la macchina virtuale dal sistema host.
> 
> 

## <a name="fail-over-tooa-virtual-array"></a>Eseguire il failover array virtuale tooa

È consigliabile eseguire il provisioning, configurare e registrare un altro array virtuale StorSimple con il servizio Gestione dispositivi StorSimple prima di eseguire questa procedura.

> [!IMPORTANT]
> 
> * È possibile eseguire il failover da un dispositivo StorSimple serie 8000 dispositivo tooa 1200 virtuale.
> * È possibile eseguire il failover da dispositivo di elaborazione Standard FIPS (Federal Information) abilitato periferica virtuale tooanother FIPS abilitata o dispositivi non FIPS tooa distribuito nel portale amministrativo hello.


Eseguire hello seguendo i passaggi toorestore hello dispositivo tooa destinazione dispositivo virtuale StorSimple.

1. Eseguire il provisioning e configurare un dispositivo di destinazione che soddisfi hello [prerequisiti per il failover del dispositivo](#prerequisites). Completare la configurazione tramite l'interfaccia utente web locale hello hello e registrarlo tooyour servizio di gestione di dispositivi StorSimple. Se si crea un file server, passare toostep 1 di [configurato come file server](storsimple-virtual-array-deploy3-fs-setup.md#step-1-complete-the-local-web-ui-setup-and-register-your-device). Se la creazione di un server iSCSI passare toostep 1 di [configurato come server iSCSI](storsimple-virtual-array-deploy3-iscsi-setup.md#step-1-complete-the-local-web-ui-setup-and-register-your-device).

2. Richiedere volumi o condivisioni offline nell'host di hello. tootake hello volumi e delle condivisioni non in linea, fare riferimento le istruzioni specifiche del sistema operativo toohello per host hello. Se non è già offline, è necessario tootake tutti hello volumi e delle condivisioni non in linea sul dispositivo hello procedendo come indicato di seguito hello.
   
    1. Andare troppo**dispositivi** pannello e selezionare il dispositivo.
   
    2. Andare troppo**Impostazioni > Gestisci > condivisioni** (o **Impostazioni > Gestisci > volumi**). 
   
    3. Selezionare un volume o una condivisione, fare clic con il pulsante destro del mouse e selezionare **Porta offline**. 
   
    4. Quando viene richiesta la conferma, controllare **accetto impatto hello di disconnettere la condivisione.** 
   
    5. Fare clic su **Porta offline**.

3. Nel servizio di gestione di dispositivi StorSimple, andare troppo**gestione > dispositivi**. In hello **dispositivi** pannello, scegliere il dispositivo di origine.

4. Nel pannello **Dashboard dispositivo** fare clic su **Disattiva**.

5. In hello **disattiva** pannello, richiesta la conferma. La disattivazione del dispositivo è un processo *permanente* che non può essere annullato. Si è anche un promemoria tootake condivisioni/volumi offline nell'host di hello. Digitare hello dispositivo nome tooconfirm e fare clic su **disattiva**.
   
    ![](./media/storsimple-virtual-array-failover-dr/failover1.png)
6. Avvia la disattivazione di Hello. Dopo la disattivazione di hello è stata completata correttamente, si riceverà una notifica.
   
    ![](./media/storsimple-virtual-array-failover-dr/failover2.png)
7. Nella pagina di dispositivi hello, lo stato del dispositivo hello verrà modificata troppo**Deactivated**.
    ![](./media/storsimple-virtual-array-failover-dr/failover3.png)
8. In hello **dispositivi** pannello selezionare e fare clic su dispositivo hello origine disattivate per il failover. 
9. In hello **dashboard del dispositivo** pannello, fare clic su **failover**. 
10. In hello **failover dispositivo** pannello hello seguenti:
    
    1. campo di dispositivo di origine Hello viene popolato automaticamente. Si noti dimensioni totali dei dati hello per dispositivo di origine hello. dimensioni dei dati Hello devono essere inferiore alla capacità disponibile di hello sul dispositivo di destinazione hello. Esaminare i dettagli di hello associati hello dispositivo di origine, ad esempio nome del dispositivo, la capacità totale e hello nomi di condivisioni hello che è state eseguite il failover.

    2. Dall'elenco a discesa di hello dei dispositivi disponibili, scegliere un **dispositivo di destinazione**. Nell'elenco a discesa hello vengono visualizzati solo i dispositivi di hello che dispongano di capacità sufficiente.

    3. Verificare che **sono consapevole che questa operazione avrà esito negativo sul dispositivo di destinazione di dati toohello**. 

    4. Fare clic su **Effettua il failover**.
    
        ![](./media/storsimple-virtual-array-failover-dr/failover4.png)
11. Viene avviato un processo di failover e si riceverà una notifica. Andare troppo**dispositivi > processi** toomonitor hello failover.
    
     ![](./media/storsimple-virtual-array-failover-dr/failover5.png)
12. In hello **processi** pannello viene visualizzato un processo di failover creato per il dispositivo di origine hello. Questo processo esegue hello prechecks di ripristino di emergenza.
    
    ![](./media/storsimple-virtual-array-failover-dr/failover6.png)
    
     Dopo il ripristino di emergenza hello prechecks hanno esito positivo, il processo di failover di hello distribuirà i processi di ripristino per ogni condivisione o volume presente nel dispositivo di origine.
    
    ![](./media/storsimple-virtual-array-failover-dr/failover7.png)
13. Al termine del failover hello toohello completa, visita **dispositivi** blade.
    
    1. Selezionare e fare clic su dispositivo StorSimple hello che è stato usato come dispositivo di destinazione hello per il processo di failover di hello.
    2. Andare troppo**Impostazioni > Gestione > condivisioni** (o **volumi** se il server iSCSI). In hello **condivisioni** pannello, è possibile visualizzare tutte le condivisioni di hello (volumi) dispositivo precedente hello.
        ![](./media/storsimple-virtual-array-failover-dr/failover9.png)
14. È necessario troppo[creare un alias DNS](https://support.microsoft.com/kb/168322) in modo che tutte le applicazioni che si sta tentando di hello tooconnect può ottenere toohello reindirizzato nuovo dispositivo.

## <a name="errors-during-dr"></a>Errori durante il ripristino di emergenza

**Interruzione della connettività cloud durante il ripristino di emergenza**

Se connettività cloud hello interruzione dopo il ripristino di emergenza è stata avviata e prima del completamento, ripristino del dispositivo hello hello ripristino di emergenza avrà esito negativo. Si riceverà una notifica di errore. dispositivo di destinazione Hello per ripristino di emergenza è contrassegnato come *inutilizzabile.* Non è possibile utilizzare hello stesso dispositivo di destinazione per il servizio DRs future.

**Nessun dispositivo di destinazione compatibile**

Se i dispositivi di destinazione disponibili hello non dispone di spazio sufficiente, viene visualizzato un effetto toohello di errore che non sono presenti dispositivi di destinazione compatibile.

**Errori nelle verifiche preliminari**

Se non viene soddisfatta una delle prechecks hello, si notano precheck errori.

## <a name="business-continuity-disaster-recovery-bcdr"></a>Ripristino di emergenza di continuità aziendale (BCDR)

Uno scenario di ripristino di emergenza la continuità aziendale si verifica quando hello intero Data Center di Azure smette di funzionare. Ciò può influire sul servizio di gestione di dispositivi StorSimple e hello associati dispositivi StorSimple.

Se sono presenti dispositivi StorSimple registrati prima che si è verificato un problema grave, questi dispositivi StorSimple potrebbe essere necessario toobe eliminato. Dopo l'emergenza hello, è possibile ricreare e configurare i dispositivi.

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni su troppo[amministrare l'Array virtuale StorSimple tramite interfaccia utente web locale hello](storsimple-ova-web-ui-admin.md).

