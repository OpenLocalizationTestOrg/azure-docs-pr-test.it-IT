---
title: controller del dispositivo StorSimple aaaManage | Documenti Microsoft
description: Informazioni su come toostop, riavviare, arrestare o reimpostare il controller del dispositivo StorSimple.
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 4ee989d0-956f-4c14-951e-fd4e490ea09d
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/11/2016
ms.author: alkohli
ms.openlocfilehash: 9a86aa0f4a8fd96c36df206774972602c47a49a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-storsimple-device-controllers"></a>Gestire i controller del dispositivo StorSimple
## <a name="overview"></a>Panoramica
In questa esercitazione vengono descritte diverse operazioni hello che possono essere eseguite sui controller di dispositivo StorSimple. i controller di Hello del dispositivo StorSimple sono controller ridondanti (peer) in una configurazione attiva-passiva. In un determinato momento, un solo controller è attivo ed elabora tutte le operazioni di rete e disco hello. Hello altro controller è in modalità passiva. Se il controller attivo hello ha esito negativo, il controller passivo hello diventa attivo automaticamente.

Questa esercitazione include i controller dei dispositivi hello toomanage istruzioni utilizzando il:

* **Controller** sezione di hello **manutenzione** pagina hello servizio StorSimple Manager
* Windows PowerShell per StorSimple.

Si consiglia di gestire i controller del dispositivo tramite il servizio StorSimple Manager hello hello. Se un'azione può essere eseguita solo tramite Windows PowerShell per StorSimple, esercitazione hello prende nota di esso.

Dopo aver letto questa esercitazione, si sarà in grado di:

* Riavviare o arrestare il controller di un dispositivo StorSimple
* Arrestare un dispositivo StorSimple
* Reimpostare le impostazioni predefinite toofactory del dispositivo StorSimple

## <a name="restart-or-shut-down-a-single-controller"></a>Riavviare o arrestare un singolo controller
Il riavvio o l'arresto del controller non è richiesto come parte del funzionamento normale del sistema. Le operazioni di arresto per un singolo controller del dispositivo sono comuni solo nei casi in cui si richiede la sostituzione di un componente hardware mal funzionante del dispositivo. Il riavvio del controller potrebbe essere necessario anche quando le prestazioni sono influenzate dall'utilizzo eccessivo della memoria o da un controller che non funziona correttamente. È necessario anche toorestart un controller dopo la sostituzione, se si desidera tooenable e hello sostituito controller di test.

Il riavvio di un dispositivo non è iniziatori tooconnected arresto improvviso, presupponendo che il controller passivo hello è disponibile. Se un controller passivo non è disponibile o è spento, quindi riavviare hello active controller potrebbe causare interruzioni hello del servizio e tempi di inattività.

> [!IMPORTANT]
> * **Un controller in esecuzione non deve mai essere fisicamente rimosso poiché potrebbe causare una perdita di ridondanza e un maggior rischio di tempi di inattività.**
> * Hello procedura seguente si applica solo toohello dispositivo fisico StorSimple. Per informazioni su come toostart, arrestare e riavviare la periferica virtuale hello, vedere [funziona con dispositivo virtuale hello](storsimple-virtual-device-u2.md#work-with-the-storsimple-virtual-device).
> 
> 

È possibile riavviare o arrestare un controller di dispositivo singolo tramite hello portale di Azure classico del servizio StorSimple Manager hello o Windows PowerShell per StorSimple

eseguire i controller di dispositivo dal portale di Azure classico, hello toomanage hello i passaggi seguenti.

#### <a name="toorestart-or-shut-down-a-controller-in-classic-portal"></a>toorestart o arresta un controller nel portale classico
1. Passare troppo**dispositivi > manutenzione**.
2. Andare troppo**stato Hardware** e verificare che sia stato hello di entrambi i controller sul dispositivo hello **integro**.
   
    ![Verificare l'integrità dei controller del dispositivo StorSimple](./media/storsimple-manage-device-controller/IC766017.png)
3. Dal basso hello di hello **manutenzione** pagina, fare clic su **Gestisci controller**.
   
    ![Gestire i controller del dispositivo StorSimple](./media/storsimple-manage-device-controller/IC766018.png)</br>
   
   > [!NOTE]
   > Se non è possibile visualizzare **Gestisci controller**, è necessario tooinstall aggiornamenti. Per altre informazioni, vedere [Aggiornare il dispositivo StorSimple](storsimple-update-device.md).
   > 
   > 
4. In hello **Modifica impostazioni Controller** finestra di dialogo casella, hello seguenti:
   
   1. Da hello **seleziona Controller** elenco a discesa, selezionare hello del controller che si desidera toomanage. opzioni di Hello sono Controller 0 e Controller 1. Questi controller vengono identificati anche come attivo o passivo.
      
      > [!NOTE]
      > Un controller non può essere gestito se è disponibile o è spento e non verrà visualizzata nell'elenco a discesa hello.
      > 
      > 
   2. Da hello **selezionare un'azione** elenco a discesa scegliere **riavviare controller** o **arresta controller**.
      
       ![Riavviare il controller passivo del dispositivo StorSimple](./media/storsimple-manage-device-controller/IC766020.png)
   3. Fare clic sull'icona di controllo hello ![Icona del segno di spunta](./media/storsimple-manage-device-controller/IC740895.png).

Verrà riavviato o arrestato controller hello. tabella Hello riportata di seguito sono riepilogati i dettagli di hello di ciò che accade in base alle selezioni di hello sono state apportate in hello **Modifica impostazioni Controller** la finestra di dialogo.  

| N. selezione | Se si sceglie di... | Viene eseguita questa operazione. |
| --- | --- | --- |
| 1. |Riavviare il controller passivo hello. |Verrà creato un processo controller hello toorestart e riceverà una notifica dopo la creazione del processo hello. Verrà avviata hello riavvio del controller. È possibile monitorare il processo di riavvio hello accedendo **servizio > Dashboard > visualizzare log operazioni** e quindi filtrare in base al servizio tooyour specifico di parametri. |
| 2. |Riavviare il controller attivo di hello. |Verrà visualizzato hello seguente avviso: "Se si riavvia controller attivo hello, dispositivo hello avrà esito negativo sul controller passivo toohello. Si desidera toocontinue?" </br>Se si sceglie tooproceed con questa operazione, passaggi successivi di hello saranno identici toothose utilizzato toorestart hello il controller passivo (vedere la selezione 1). |
| 3. |Arrestare il controller passivo hello. |Verrà visualizzato hello seguente messaggio: "dopo l'arresto, sarà necessario toopush power hello pulsante tooturn il controller in. Non è che possibile tooshut verso il basso il controller?" </br>Se si sceglie tooproceed con questa operazione, passaggi successivi di hello saranno identici toothose utilizzato toorestart hello il controller passivo (vedere la selezione 1). |
| 4. |Arrestare il controller attivo di hello. |Verrà visualizzato hello seguente messaggio: "dopo l'arresto, sarà necessario toopush power hello pulsante tooturn il controller in. Non è che possibile tooshut verso il basso il controller?" </br>Se si sceglie tooproceed con questa operazione, passaggi successivi di hello saranno identici toothose utilizzato toorestart hello il controller passivo (vedere la selezione 1). |

#### <a name="toorestart-or-shut-down-a-controller-in-windows-powershell-for-storsimple"></a>toorestart o arresta un controller in Windows PowerShell per StorSimple
Eseguire i seguenti passaggi tooshut verso il basso hello o riavviare un singolo controller sul dispositivo StorSimple da hello portale di Azure classico.

1. Dispositivo di hello accesso tramite la console seriale hello o una sessione telnet da un computer remoto. Connettersi tooController 0 o Controller 1 dal seguente hello passi in [console seriale del dispositivo usare PuTTY tooconnect toohello](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).
2. Nel menu della console seriale hello, selezionare l'opzione 1, **Accedi con accesso completo**.
3. Nel messaggio banner hello, prendere nota del controller hello troppo si è connessi (Controller 0 o Controller 1) e se è attiva hello o il controller passivo (standby) hello.
   
   * tooshut verso il basso un singolo controller, al prompt dei comandi hello, tipo:
     
       `Stop-HcsController`
     
       Controller hello che si è connessi verrà arrestato. Se si arresta controller attivo hello, ne verrà eseguito sul controller passivo toohello prima della chiusura.
   * toorestart un controller, al prompt dei comandi hello, digitare:
     
       `Restart-HcsController`
     
       Controller hello che si è connessi verrà riavviato. Se si riavvia controller attivo hello, ne verrà eseguito il failover controller passivo toohello prima di riavviare hello.

## <a name="shut-down-a-storsimple-device"></a>Arrestare un dispositivo StorSimple
Questa sezione viene illustrato come tooshut verso il basso in esecuzione o un dispositivo StorSimple non riuscito da un computer remoto. Un dispositivo è stato disattivato dopo l'arresto di entrambi i controller dei dispositivi hello. Un arresto del dispositivo viene eseguito quando il dispositivo hello viene spostato fisicamente o viene messo fuori servizio.

> [!IMPORTANT]
> Prima di arrestare il dispositivo di hello, controllare l'integrità hello dei componenti del dispositivo hello. Passare troppo**dispositivi > manutenzione > stato dell'Hardware** e verificare che lo stato di hello LED di tutti i componenti di hello sia verde. Solo un dispositivo integro avrà lo stato verde. Se il dispositivo è l'arresto tooreplace un componente non funzionante, verrà visualizzato un errore (rosso) o uno stato danneggiato (giallo) per hello i componenti corrispondenti.
> 
> 

#### <a name="tooshut-down-a-storsimple-device"></a>tooshut verso il basso un dispositivo StorSimple
1. Hello utilizzare [riavviare o arrestare un controller](#restart-or-shut-down-a-single-controller) tooidentify procedura e arresta il controller passivo hello del dispositivo. È possibile eseguire questa operazione nel portale di Azure classico hello o in Windows PowerShell per StorSimple.
2. Ripetere hello sopra tooshut passaggio verso il basso controller attivo hello.
3. È ora necessario toolook in hello backplane del dispositivo hello. Dopo due controller di hello vengono arrestati completamente, hello LED di stato di entrambi i controller hello deve essere di colore rosso lampeggiante. Se è necessario tooturn off dispositivo hello completamente in questo momento, hello capovolto interruttori di alimentazione di entrambi Power and Cooling Module (PCM) posizione OFF toohello. Questo necessario disattivare la periferica hello.

<!--#### tooshut down a StorSimple device in Windows PowerShell for StorSimple

1. Connect toohello serial console of hello StorSimple device by following hello steps in [Use PuTTY tooconnect toohello device serial console](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-serial-console).

1. In hello serial console menu, verify from hello banner message that hello controller you are connected toois hello passive controller. If you are connected toohello active controller, disconnect from this controller and connect toohello other controller.

1. In hello serial console menu, choose option 1, **log in with full access**.

1. At hello prompt, type:

    `Stop-HCSController`

    This should shut down hello current controller. tooverify whether hello shutdown has finished, check hello back of hello device. hello controller status LED should be solid red.

1. Repeat steps 1 through 4 tooconnect toohello active controller and then shut it down.

1. After both hello controllers are completely shut down, hello status LEDs on both should be blinking red. If you need tooturn off hello device completely at this time, flip hello power switches on both Power and Cooling Modules (PCMs) toohello OFF position.-->

## <a name="reset-hello-device-toofactory-default-settings"></a>Ripristinare le impostazioni predefinite di hello dispositivo toofactory
> [!IMPORTANT]
> Se è necessario tooreset le impostazioni predefinite del dispositivo toofactory, contattare il supporto Microsoft. procedura Hello descritta di seguito deve essere utilizzato solo in combinazione con il supporto Microsoft.
> 
> 

Questa procedura viene descritto come tooreset le impostazioni predefinite di Microsoft Azure StorSimple dispositivo toofactory tramite Windows PowerShell per StorSimple.
Reimpostazione di un dispositivo rimuove tutti i dati e impostazioni dall'intero cluster di hello per impostazione predefinita.

Eseguire le impostazioni predefinite di Microsoft Azure StorSimple dispositivo toofactory di hello tooreset i passaggi seguenti:

### <a name="tooreset-hello-device-toodefault-settings-in-windows-powershell-for-storsimple"></a>tooreset hello toodefault impostazioni dei dispositivi in Windows PowerShell per StorSimple
1. Dispositivo di hello accesso tramite la console seriale. Controllare hello intestazione messaggio tooensure siano controller attivo toohello connesso.
2. Nel menu della console seriale hello, selezionare l'opzione 1, **Accedi con accesso completo**.
3. Al prompt dei comandi hello, digitare hello intero cluster hello tooreset comando seguente, la rimozione di tutte le impostazioni di dati, metadati e controller:
   
    `Reset-HcsFactoryDefault`
   
    tooinstead reimpostare un singolo controller, utilizzare hello [Reset-HcsFactoryDefault](http://technet.microsoft.com/library/dn688132.aspx) cmdlet con hello `-scope` parametro.)
   
    sistema di Hello verrà riavviato più volte. Verrà visualizzato un messaggio hello reimpostazione è stata completata. A seconda del modello di sistema di hello, può richiedere 45-60 minuti per un dispositivo 8100 e 60-90 minuti per un toofinish 8600 questo processo.
   
   > [!TIP]
   > * Se si utilizza aggiornamento 1.2 o versioni precedenti utilizzare hello `–SkipFirmwareVersionCheck` controllo della versione del firmware hello tooskip parametro (in caso contrario verrà visualizzato un errore di mancata corrispondenza del firmware: impostazioni di fabbrica non possono continuare a causa di mancata corrispondenza tooa nelle versioni del firmware hello. ).
   > * procedura di reimpostazione della factory Hello potrebbe non riuscire per i dispositivi StorSimple eseguono Update 1 o 1.1 nel portale amministrativo hello e avere eseguito una singola o doppia sostituzione (con controller di sostituzione che sono stati spediti con pre-aggiornamento 1 software). Ciò accade quando factory hello reimpostare immagine è stata convalidata per presenza hello di un file di SHA1 sul controller hello che non esiste per il software di pre-aggiornamento 1. Se viene visualizzato questo factory reimpostare l'errore, contattare il supporto Microsoft tooassist si con hello passaggi successivi. Questo problema non viene visualizzato con controller sostitutivi fornito dalla factory hello con Update 1 o versioni successive del software.
   > 
   > 

## <a name="questions-and-answers-about-managing-device-controllers"></a>Domande e risposte sulla gestione dei controller del dispositivo
In questa sezione, è stato riepilogate alcune delle domande frequenti hello per quanto riguarda la gestione dei controller del dispositivo StorSimple.

**D.** Cosa accade se entrambi hello controller del dispositivo sono integro e acceso in e riavviare o arrestare controller attivo hello?

**R.** Se entrambi i controller hello nel dispositivo sono integri e accesi, verrà richiesto di confermare. È possibile scegliere di:

* **Riavvia controller attivo hello** : si riceverà una notifica che il riavvio di un controller attivo causerà hello dispositivo toofail sul controller passivo toohello. Hello controller verrà riavviato.
* **Arrestare il controller attivo** - viene ricevuta una notifica indicante che l'arresto del controller attivo determina tempi di inattività. È necessario anche toopush hello pulsante di alimentazione hello tooturn di dispositivo sul controller hello.

**D.** Cosa accade se hello il controller passivo del dispositivo è disponibile o è spento off e si riavvia o si arresta controller attivo hello?

**R.** Se il controller passivo hello nel dispositivo è disponibile o è spento e si sceglie di:

* **Riavvia controller attivo hello** : si riceverà una notifica che funzionamento hello comporterà un'interruzione temporanea del servizio hello e verrà richiesto di confermare.
* **Arrestare un controller attivo** : si riceverà una notifica che continuando hello operazione comporta tempi di inattività e che sarà necessario pulsante di alimentazione toopush hello in uno o entrambi tooturn controller sul dispositivo hello. Verrà richiesto di confermare.

**D.** Se riavvio del controller hello o un arresto non è riuscita tooprogress?

**R.** Il riavvio o l'arresto di un controller può non riuscire se:

* Un aggiornamento del dispositivo è in corso.
* Un riavvio del controller è già in corso.
* Un arresto del controller è già in corso.

**D.** Come si capisce se un controller è stato riavviato o arrestato?

**R.** È possibile controllare lo stato del controller hello nella pagina Manutenzione hello. stato del controller Hello indica se un controller è stato riavviato o arrestato. Inoltre, pagina avvisi hello conterrà un avviso informativo se controller hello è stato riavviato o arrestato. le operazioni di riavvio e arresto controller Hello vengono anche registrate nei log di operazione hello. Per ulteriori informazioni sui log operazioni, andare troppo[visualizzare log operazioni hello](storsimple-service-dashboard.md#view-the-operations-logs).

**D.** È qualsiasi toohello impatto i/o in seguito al failover del controller?

**R.** le connessioni TCP Hello tra gli iniziatori e controller attivo verranno reimpostate in seguito al failover del controller, ma verranno ristabilite non appena il controller passivo hello presuppone che l'operazione. Potrebbe esserci una pausa temporanea (meno di 30 secondi) nell'attività dei / o tra gli iniziatori e dispositivo hello hello durante questa operazione.

**D.** Come visualizzare il tooservice controller dopo che è stato arrestato e rimosso?

**R.** tooreturn tooservice un controller, è necessario inserirlo nello chassis hello come descritto in [sostituire un modulo controller sul dispositivo StorSimple](storsimple-controller-replacement.md).

## <a name="next-steps"></a>Passaggi successivi
* Se si verificano problemi con i controller del dispositivo StorSimple che è possibile risolvere utilizzando procedure hello elencate in questa esercitazione, [contattare il supporto Microsoft](storsimple-contact-microsoft-support.md).
* toolearn ulteriori informazioni sull'utilizzo del servizio StorSimple Manager hello, andare troppo[utilizzare hello tooadminister servizio StorSimple Manager dispositivo StorSimple](storsimple-manager-service-administration.md).

