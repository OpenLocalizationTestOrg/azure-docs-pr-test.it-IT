---
title: i controller dei dispositivi serie StorSimple 8000 aaaManage | Documenti Microsoft
description: Informazioni su come toostop, riavviare, arrestare o reimpostare il controller del dispositivo StorSimple.
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/19/2017
ms.author: alkohli
ms.openlocfilehash: 5c59582b7ccf7cfeae9e7efbd0e4df9dc1d3871c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-storsimple-device-controllers"></a>Gestire i controller del dispositivo StorSimple

## <a name="overview"></a>Panoramica

In questa esercitazione vengono descritte diverse operazioni hello che possono essere eseguite sui controller di dispositivo StorSimple. i controller di Hello del dispositivo StorSimple sono controller ridondanti (peer) in una configurazione attiva-passiva. In un determinato momento, un solo controller è attivo ed elabora tutte le operazioni di rete e disco hello. Hello altro controller è in modalità passiva. Se il controller attivo hello non riesce, controller passivo hello automaticamente diventa attivo.

Questa esercitazione include i controller dei dispositivi hello toomanage istruzioni utilizzando il:

* **Controller** pannello per il dispositivo nel servizio di gestione di dispositivi StorSimple hello.
* Windows PowerShell per StorSimple.

Si consiglia di gestire i controller del dispositivo tramite il servizio di gestione di dispositivi StorSimple hello hello. Se un'azione può essere eseguita solo tramite Windows PowerShell per StorSimple, esercitazione hello prende nota di esso.

Dopo aver letto questa esercitazione, si sarà in grado di:

* Riavviare o arrestare il controller di un dispositivo StorSimple
* Arrestare un dispositivo StorSimple
* Reimpostare le impostazioni predefinite toofactory del dispositivo StorSimple

## <a name="restart-or-shut-down-a-single-controller"></a>Riavviare o arrestare un singolo controller
Il riavvio o l'arresto del controller non è richiesto come parte del funzionamento normale del sistema. Le operazioni di arresto per un singolo controller del dispositivo sono comuni solo nei casi in cui si richiede la sostituzione di un componente hardware mal funzionante del dispositivo. Il riavvio del controller potrebbe essere necessario anche quando le prestazioni sono influenzate dall'utilizzo eccessivo della memoria o da un controller che non funziona correttamente. È necessario anche toorestart un controller dopo la sostituzione, se si desidera tooenable e hello sostituito controller di test.

Il riavvio di un dispositivo non è iniziatori tooconnected arresto improvviso, presupponendo che il controller passivo hello è disponibile. Se un controller passivo non è disponibile o è spento, quindi riavviare hello active controller potrebbe causare interruzioni hello del servizio e tempi di inattività.

> [!IMPORTANT]
> * **Un controller in esecuzione non deve mai essere fisicamente rimosso poiché potrebbe causare una perdita di ridondanza e un maggior rischio di tempi di inattività.**
> * Hello procedura seguente si applica solo toohello dispositivo fisico StorSimple. Per informazioni su come toostart, arrestare e riavviare hello StorSimple Appliance di Cloud, vedere [utilizzano appliance di cloud hello](storsimple-8000-cloud-appliance-u2.md##work-with-the-storsimple-cloud-appliance).

È possibile riavviare o arrestare un controller di dispositivo singolo tramite hello portale di Azure del servizio di gestione di dispositivi StorSimple hello o Windows PowerShell per StorSimple.

eseguire i controller di dispositivo dal portale di Azure hello toomanage hello i passaggi seguenti.

#### <a name="toorestart-or-shut-down-a-controller-in-azure-portal"></a>toorestart o arresta un controller nel portale di Azure
1. Nel servizio di gestione di dispositivi StorSimple, andare troppo**dispositivi**. Selezionare il dispositivo dall'elenco di hello dei dispositivi. 

    ![Scegliere un dispositivo](./media/storsimple-8000-manage-device-controller/manage-controller1.png)

2. Andare troppo**Impostazioni > controller**.
   
    ![Verificare l'integrità dei controller del dispositivo StorSimple](./media/storsimple-8000-manage-device-controller/manage-controller2.png)
3. In hello **controller** pannello, verificare che sia stato hello di entrambi i controller sul dispositivo hello **integro**. Selezionare un controller, fare clic con il pulsante destro del mouse, quindi selezionare **Riavvia** o **Arresto**.

    ![Riavviare o arrestare il controller di un dispositivo StorSimple](./media/storsimple-8000-manage-device-controller/manage-controller3.png)

4. Un processo viene creato toorestart o arrestare il controller hello e vengono presentati gli avvisi applicabili, se presente. toomonitor hello riavvio o l'arresto, andare troppo**servizio > log attività** e quindi filtrare dal servizio tooyour specifico di parametri. Se un controller è stato arrestato, quindi sarà necessario toopush hello power pulsante tooturn su hello controller tooturn sul.

#### <a name="toorestart-or-shut-down-a-controller-in-windows-powershell-for-storsimple"></a>toorestart o arresta un controller in Windows PowerShell per StorSimple
Eseguire i seguenti passaggi tooshut verso il basso hello o riavviare un singolo controller sul dispositivo StorSimple da hello Windows PowerShell per StorSimple.

1. Dispositivo di hello accesso tramite la console seriale hello o una sessione telnet da un computer remoto. tooconnect tooController 0 o Controller 1, procedura hello [console seriale del dispositivo usare PuTTY tooconnect toohello](storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).
2. Nel menu della console seriale hello, selezionare l'opzione 1, **Accedi con accesso completo**.
3. Nel messaggio banner hello, prendere nota del controller hello troppo si è connessi (Controller 0 o Controller 1) e se è attiva hello o il controller passivo (standby) hello.
   
   * tooshut verso il basso un singolo controller, al prompt dei comandi hello, tipo:
     
       `Stop-HcsController`
     
       Questo chiude controller hello che si è connessi. Se si arresta controller attivo hello, dispositivo hello non riesce sul controller passivo toohello.

   * toorestart un controller, al prompt dei comandi hello, digitare:
     
       `Restart-HcsController`
     
       Controller hello che si è connessi verrà riavviato. Se si riavvia controller attivo hello, operazione non riesce sul controller passivo toohello prima di riavviare hello.

## <a name="shut-down-a-storsimple-device"></a>Arrestare un dispositivo StorSimple

Questa sezione viene illustrato come tooshut verso il basso in esecuzione o un dispositivo StorSimple non riuscito da un computer remoto. Un dispositivo è stato disattivato, dopo che entrambi i controller dei dispositivi hello vengono arrestati. Un arresto del dispositivo viene eseguito quando il dispositivo hello viene spostato fisicamente o viene messo fuori servizio.

> [!IMPORTANT]
> Prima di arrestare il dispositivo di hello, controllare l'integrità hello dei componenti del dispositivo hello. Passare tooyour dispositivo e quindi fare clic su **Impostazioni > lo stato di Hardware**. In hello **hardware e lo stato di integrità** pannello, verificare che lo stato di hello LED di tutti i componenti di hello sia verde. Solo un dispositivo integro avrà lo stato verde. Se il dispositivo è l'arresto tooreplace un componente non funzionante, verrà visualizzato un errore (rosso) o uno stato danneggiato (giallo) per hello i componenti corrispondenti.


#### <a name="tooshut-down-a-storsimple-device"></a>tooshut verso il basso un dispositivo StorSimple

1. Hello utilizzare [riavviare o arrestare un controller](#restart-or-shut-down-a-single-controller) tooidentify procedura e arresta il controller passivo hello del dispositivo. È possibile eseguire questa operazione in hello portale di Azure o in Windows PowerShell per StorSimple.
2. Ripetere hello sopra tooshut passaggio verso il basso controller attivo hello.
3. È necessario esaminare hello nuovamente al piano del dispositivo hello. Dopo due controller di hello vengono arrestati completamente, hello LED di stato di entrambi i controller hello deve essere di colore rosso lampeggiante. Se è necessario tooturn off dispositivo hello completamente in questo momento, hello capovolto interruttori di alimentazione di entrambi Power and Cooling Module (PCM) posizione OFF toohello. Questo necessario disattivare la periferica hello.

## <a name="reset-hello-device-toofactory-default-settings"></a>Ripristinare le impostazioni predefinite di hello dispositivo toofactory

> [!IMPORTANT]
> Se è necessario tooreset le impostazioni predefinite del dispositivo toofactory, contattare il supporto Microsoft. procedura Hello descritta di seguito deve essere utilizzato solo in combinazione con il supporto Microsoft.

Questa procedura viene descritto come tooreset le impostazioni predefinite di Microsoft Azure StorSimple dispositivo toofactory tramite Windows PowerShell per StorSimple.
Reimpostazione di un dispositivo rimuove tutti i dati e impostazioni dall'intero cluster di hello per impostazione predefinita.

Eseguire le impostazioni predefinite di Microsoft Azure StorSimple dispositivo toofactory di hello tooreset i passaggi seguenti:

### <a name="tooreset-hello-device-toodefault-settings-in-windows-powershell-for-storsimple"></a>tooreset hello toodefault impostazioni dei dispositivi in Windows PowerShell per StorSimple
1. Dispositivo di hello accesso tramite la console seriale. Controllare hello intestazione messaggio tooensure che si è connesso toohello **Active** controller.
2. Nel menu della console seriale hello, selezionare l'opzione 1, **Accedi con accesso completo**.
3. Al prompt dei comandi hello, digitare hello intero cluster hello tooreset comando seguente, la rimozione di tutte le impostazioni di dati, metadati e controller:
   
    `Reset-HcsFactoryDefault`
   
    tooinstead reimpostare un singolo controller, utilizzare hello [Reset-HcsFactoryDefault](http://technet.microsoft.com/library/dn688132.aspx) cmdlet con hello `-scope` parametro.)
   
    sistema di Hello verrà riavviato più volte. Verrà visualizzato un messaggio hello reimpostazione è stata completata. A seconda del modello di sistema di hello, può richiedere 45-60 minuti per un dispositivo 8100 e 60-90 minuti per un toofinish 8600 questo processo.
   
## <a name="questions-and-answers-about-managing-device-controllers"></a>Domande e risposte sulla gestione dei controller del dispositivo
In questa sezione, è stato riepilogate alcune delle domande frequenti hello per quanto riguarda la gestione dei controller del dispositivo StorSimple.

**D.** Cosa accade se entrambi hello controller del dispositivo sono integro e acceso in e riavviare o arrestare controller attivo hello?

**R.** Se entrambi i controller hello nel dispositivo sono integri e accesi, richiesta la conferma. È possibile scegliere di:

* **Riavvia controller attivo hello** : si riceve una notifica che causa il riavvio di un controller attivo hello dispositivo toofail sul controller passivo toohello. Riavvia controller Hello.
* **Arrestare il controller attivo** - viene ricevuta una notifica indicante che l'arresto del controller attivo determina tempi di inattività. È inoltre necessario toopush hello pulsante di alimentazione hello tooturn di dispositivo sul controller hello.

**D.** Cosa accade se hello il controller passivo del dispositivo è disponibile o è spento off e si riavvia o si arresta controller attivo hello?

**R.** Se il controller passivo hello nel dispositivo è disponibile o è spento e si sceglie di:

* **Riavvia controller attivo hello** – utente viene informato che funzionamento hello comporterà un'interruzione temporanea del servizio hello e viene chiesto di confermare.
* **Arrestare un controller attivo** : si riceve una notifica che continui hello operazione comporta tempi di inattività. È inoltre necessario pulsante di alimentazione toopush hello in uno o entrambi tooturn controller sul dispositivo hello. Viene chiesto di confermare l'operazione.

**D.** Se riavvio del controller hello o un arresto non è riuscita tooprogress?

**R.** Il riavvio o l'arresto di un controller può non riuscire se:

* Un aggiornamento del dispositivo è in corso.
* Un riavvio del controller è già in corso.
* Un arresto del controller è già in corso.

**D.** Come si capisce se un controller è stato riavviato o arrestato?

**R.** È possibile controllare lo stato del controller hello nel Pannello di Controller. stato del controller Hello indica se un controller è in corso di hello di riavviare o arrestare. Inoltre, hello **avvisi** pannello contiene un avviso informativo se controller hello viene riavviato o arrestato. le operazioni di riavvio e arresto controller Hello vengono anche registrate nei registri di hello dell'attività. Per ulteriori informazioni sui log dell'attività, andare troppo[visualizzare log attività hello](storsimple-8000-service-dashboard.md#view-the-activity-logs).

**D.** È qualsiasi toohello impatto i/o in seguito al failover del controller?

**R.** le connessioni TCP Hello tra gli iniziatori e controller attivo verranno reimpostate in seguito al failover del controller, ma verranno ristabilite non appena il controller passivo hello presuppone che l'operazione. Potrebbe esserci una pausa temporanea (meno di 30 secondi) nell'attività dei / o tra gli iniziatori e dispositivo hello hello durante questa operazione.

**D.** Come visualizzare il tooservice controller dopo che è stato arrestato e rimosso?

**R.** tooreturn tooservice un controller, è necessario inserirlo nello chassis hello come descritto in [sostituire un modulo controller sul dispositivo StorSimple](storsimple-8000-controller-replacement.md).

## <a name="next-steps"></a>Passaggi successivi
* Se si verificano problemi con i controller del dispositivo StorSimple che è possibile risolvere utilizzando procedure hello elencate in questa esercitazione, [contattare il supporto Microsoft](storsimple-8000-contact-microsoft-support.md).
* toolearn ulteriori informazioni sull'utilizzo del servizio di gestione di dispositivi StorSimple hello, andare troppo[utilizzare hello tooadminister servizio di gestione di dispositivi StorSimple dispositivo StorSimple](storsimple-8000-manager-service-administration.md).

