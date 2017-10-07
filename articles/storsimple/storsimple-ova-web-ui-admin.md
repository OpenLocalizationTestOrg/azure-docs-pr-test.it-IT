---
title: web Array virtuale aaaStorSimple amministrazione dell'interfaccia utente | Documenti Microsoft
description: "Viene descritto come l'attività di amministrazione di base del dispositivo di tooperform tramite l'interfaccia utente web Array virtuale StorSimple di hello."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: ea65b4c7-a478-43e6-83df-1d9ea62916a6
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 12/1/2016
ms.author: alkohli
ms.openlocfilehash: 31a20a587c4302231f027fcf772a50df33b23407
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-web-ui-tooadminister-your-storsimple-virtual-array"></a>Utilizzare hello dell'interfaccia utente Web tooadminister l'Array virtuale StorSimple
![flusso del processo di installazione](./media/storsimple-ova-web-ui-admin/manage4.png)

## <a name="overview"></a>Panoramica
esercitazioni di Hello in questo articolo si applicano versione di disponibilità generale (GA) di toohello Microsoft Azure StorSimple Virtual Array (noto anche come hello StorSimple nel dispositivo virtuale locale) in esecuzione marzo 2016. Questo articolo descrive alcuni dei flussi di lavoro complessi hello e attività di gestione che possono essere eseguite su hello Array virtuale StorSimple. È possibile gestire hello StorSimple Array virtuale utilizzando l'interfaccia utente (tooas cui hello interfaccia utente del portale) del servizio StorSimple Manager hello e interfaccia utente web locale per il dispositivo hello hello. Questo articolo è incentrato sulle attività hello che è possibile eseguire tramite interfaccia utente web hello.

In questo articolo include hello seguenti esercitazioni:

* Ottenere la chiave di crittografia di hello servizio dati
* Risolvere i problemi relativi agli errori di installazione dell'interfaccia utente Web
* Generare un pacchetto di log
* Arrestare o riavviare il dispositivo

## <a name="get-hello-service-data-encryption-key"></a>Ottenere la chiave di crittografia di hello servizio dati
Una chiave DEK del servizio viene generata quando si registra il primo dispositivo con hello servizio StorSimple Manager. Questa chiave è quindi necessario con hello servizio registrazione tooregister chiave ulteriori dispositivi con hello servizio StorSimple Manager.

Se è stato smarrito la chiave DEK del servizio e tooretrieve necessario, eseguire l'esempio hello passaggi hello interfaccia web locale del dispositivo hello registrato con il servizio.

#### <a name="tooget-hello-service-data-encryption-key"></a>chiave di crittografia tooget hello servizio dati
1. Connettere l'interfaccia utente web locale toohello. Andare troppo**configurazione** > **le impostazioni del Cloud**.
2. Nella parte inferiore di hello della pagina hello, fare clic su **chiave DEK del servizio Get**. Viene visualizzata una chiave. Copiare e salvare questa chiave.
   
    ![ottenere la chiave DEK del servizio 1](./media/storsimple-ova-web-ui-admin/image27.png)

## <a name="troubleshoot-web-ui-setup-errors"></a>Risolvere i problemi relativi agli errori di installazione dell'interfaccia utente Web
In alcuni casi quando si configura il dispositivo di hello tramite web locale hello dell'interfaccia utente, verifichino errori. toodiagnose e risolvere questi errori, è possibile eseguire il test di diagnostica hello.

#### <a name="toorun-hello-diagnostic-tests"></a>test diagnostici hello toorun
1. In hello interfaccia utente web locale, andare troppo**Troubleshooting** > **test diagnostici**.
   
    ![eseguire diagnostica 1](./media/storsimple-ova-web-ui-admin/image29.png)
2. Nella parte inferiore di hello della pagina hello, fare clic su **eseguire i test diagnostici**. Verrà avviata test toodiagnose qualsiasi possibili problemi di rete, dispositivi, proxy web, ora o le impostazioni del cloud. Si riceverà una notifica che il dispositivo hello è in esecuzione di test.
3. Dopo aver completato il test di hello, hello risultati verranno visualizzati. Hello seguente esempio vengono illustrati hello risultati test di diagnostica. Si noti che le impostazioni di proxy web hello non sono state configurate su questo dispositivo, e di conseguenza, i test di proxy web hello non è stato eseguito. Tutti gli altri test per le impostazioni di rete, server DNS, di hello e le impostazioni dell'ora hanno avuto esito positivo.
   
    ![eseguire diagnostica 2](./media/storsimple-ova-web-ui-admin/image30.png)

## <a name="generate-a-log-package"></a>Generare un pacchetto di log
Un pacchetto di log è costituito da tutti i log rilevanti hello che consentono di supporto alla risoluzione dei problemi qualsiasi dispositivo. In questa versione, è possibile generare un pacchetto di log tramite l'interfaccia utente web locale hello.

#### <a name="toogenerate-hello-log-package"></a>pacchetto di log hello toogenerate
1. In hello interfaccia utente web locale, andare troppo**Troubleshooting** > **i registri di sistema**.
   
    ![generare pacchetto di log 1](./media/storsimple-ova-web-ui-admin/image31.png)
2. Nella parte inferiore di hello della pagina hello, fare clic su **creare il pacchetto di log**. Verrà creato un pacchetto di hello i registri di sistema. L'operazione richiede alcuni minuti.
   
    ![generare pacchetto di log 2](./media/storsimple-ova-web-ui-admin/image32.png)
   
    Dopo che viene creato correttamente i pacchetti hello e hello pagina verrà aggiornata ora hello tooindicate e data di creazione pacchetto hello si riceverà la notifica.
   
    ![generare pacchetto di log 3](./media/storsimple-ova-web-ui-admin/image33.png)
3. Fare clic su **Scarica pacchetto di log**. Un pacchetto compresso viene scaricato nel sistema.
   
    ![generare pacchetto di log 4](./media/storsimple-ova-web-ui-admin/image34.png)
4. È possibile decomprimere il pacchetto di log scaricati hello e visualizzare i file di registro di sistema hello.

## <a name="shut-down-and-restart-your-device"></a>Arrestare e riavviare il dispositivo
È possibile arrestare o riavviare il dispositivo virtuale utilizzando l'interfaccia utente web locale hello. È consigliabile che prima di riavviare, richiedere hello volumi o condivisioni a offline nell'host di hello e quindi hello dispositivo. Questa operazione consente di eliminare qualsiasi  rischio di danneggiamento dei dati. 

#### <a name="tooshut-down-your-virtual-device"></a>tooshut verso il basso il dispositivo virtuale
1. In hello interfaccia utente web locale, andare troppo**manutenzione** > **impostazioni di risparmio energia**.
2. Nella parte inferiore di hello della pagina hello, fare clic su **arresto**.
   
    ![arresto del dispositivo 1](./media/storsimple-ova-web-ui-admin/image36.png)
3. Verrà visualizzato un avviso che informa che un arresto del dispositivo hello interromperà tutti i/o in corso, risultante in un tempo di inattività. Fare clic sull'icona di controllo hello ![icona del segno di spunta](./media/storsimple-ova-web-ui-admin/image3.png).
   
    ![avviso di arresto del dispositivo](./media/storsimple-ova-web-ui-admin/image37.png)
   
    Si riceverà una notifica che è stata avviata la chiusura hello.
   
    ![arresto del dispositivo avviato](./media/storsimple-ova-web-ui-admin/image38.png)
   
    dispositivo Hello verrà arrestato. Se si desidera toostart il dispositivo, è necessario toodo che tramite hello Hyper-V Manager.

#### <a name="toorestart-your-virtual-device"></a>toorestart del dispositivo virtuale
1. In hello interfaccia utente web locale, andare troppo**manutenzione** > **impostazioni di risparmio energia**.
2. Nella parte inferiore di hello della pagina hello, fare clic su **riavviare**.
   
    ![riavvio del dispositivo](./media/storsimple-ova-web-ui-admin/image36.png)
3. Verrà visualizzato un avviso che informa che il dispositivo hello riavviare interromperà qualsiasi IOs in corso, risultante in un tempo di inattività. Fare clic sull'icona di controllo hello ![icona del segno di spunta](./media/storsimple-ova-web-ui-admin/image3.png).
   
    ![avviso di riavvio](./media/storsimple-ova-web-ui-admin/image37.png)
   
    Si riceverà una notifica che il riavvio hello è stato avviato.
   
    ![riavvio iniziato](./media/storsimple-ova-web-ui-admin/image39.png)
   
    Durante il riavvio di hello è in corso, si perderà hello connessione toohello dell'interfaccia utente. È possibile monitorare il riavvio di hello aggiornando periodicamente hello dell'interfaccia utente. In alternativa, è possibile monitorare lo stato di riavvio del dispositivo hello tramite hello Hyper-V Manager.

## <a name="next-steps"></a>Passaggi successivi
Informazioni su come troppo[utilizzare hello toomanage servizio StorSimple Manager dispositivo](storsimple-virtual-array-manager-service-administration.md).

