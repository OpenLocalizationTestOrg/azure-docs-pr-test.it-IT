---
title: Gestire i controller del dispositivo StorSimple serie 8000 | Microsoft Docs
description: Informazioni su come interrompere, riavviare, arrestare o reimpostare i controller del dispositivo StorSimple.
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
ms.openlocfilehash: 75c1bdb570967b6d1902697597f0b5bf3f4ffb7c
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/11/2017
---
# <a name="manage-your-storsimple-device-controllers"></a>Gestire i controller del dispositivo StorSimple

## <a name="overview"></a>Panoramica

In questa esercitazione vengono descritte le diverse operazioni che è possibile eseguire nei controller del dispositivo StorSimple. I controller del dispositivo StorSimple sono controller ridondanti (peer) in una configurazione attiva-passiva. In un determinato momento, un solo controller è attivo e sta elaborando tutte le operazioni su disco e di rete. L'altro controller è in modalità passiva. Se il controller attivo non restituisce l'esito positivo, il controller passivo diventa automaticamente attivo.

In questa esercitazione sono incluse le istruzioni dettagliate per gestire i controller del dispositivo tramite:

* Pannello **Controller** del dispositivo nel servizio di gestione dispositivi StorSimple.
* Windows PowerShell per StorSimple.

Si consiglia di gestire i controller dei dispositivi tramite il servizio Gestione dispositivi di StorSimple. Se un'azione può essere eseguita solo utilizzando Windows PowerShell per StorSimple, nell'esercitazione si esegue una nota.

Dopo aver letto questa esercitazione, si sarà in grado di:

* Riavviare o arrestare il controller di un dispositivo StorSimple
* Arrestare un dispositivo StorSimple
* Ripristinare le impostazioni predefinite del dispositivo StorSimple

## <a name="restart-or-shut-down-a-single-controller"></a>Riavviare o arrestare un singolo controller
Il riavvio o l'arresto del controller non è richiesto come parte del funzionamento normale del sistema. Le operazioni di arresto per un singolo controller del dispositivo sono comuni solo nei casi in cui si richiede la sostituzione di un componente hardware mal funzionante del dispositivo. Il riavvio del controller potrebbe essere necessario anche quando le prestazioni sono influenzate dall'utilizzo eccessivo della memoria o da un controller che non funziona correttamente. Potrebbe inoltre essere necessario eseguire il riavvio dopo la sostituzione di un controller, se si desidera attivare e testare il controller sostituito.

Il riavvio di un dispositivo non è un'operazione problematica per gli iniziatori connessi, supponendo che il controller passivo sia disponibile. Se un controller passivo non è disponibile o è spento, il riavvio del controller attivo potrebbe comportare l'interruzione del servizio e tempi di inattività.

> [!IMPORTANT]
> * **Un controller in esecuzione non deve mai essere fisicamente rimosso poiché potrebbe causare una perdita di ridondanza e un maggior rischio di tempi di inattività.**
> * La procedura seguente si applica solo al dispositivo StorSimple fisico. Per informazioni su come avviare, arrestare e riavviare l'appliance cloud StorSimple, vedere [Work with the cloud appliance](storsimple-8000-cloud-appliance-u2.md##work-with-the-storsimple-cloud-appliance) (usare l'appliance virtuale).

È possibile riavviare o arrestare un singolo controller del dispositivo mediante il portale di Azure del servizio Gestione dispositivi di StorSimple o Windows PowerShell per StorSimple.

Per gestire i controller del dispositivo dal portale di Azure, effettuare le seguenti operazioni.

#### <a name="to-restart-or-shut-down-a-controller-in-azure-portal"></a>Per riavviare o arrestare un controller nel portale di Azure
1. Nel servizio Gestione dispositivi StorSimple passare a **Dispositivi**. Il dispositivo verrà eliminato dall'elenco di dispositivi. 

    ![Scegliere un dispositivo](./media/storsimple-8000-manage-device-controller/manage-controller1.png)

2. Passare a **Impostazioni > Controller**.
   
    ![Verificare l'integrità dei controller del dispositivo StorSimple](./media/storsimple-8000-manage-device-controller/manage-controller2.png)
3. Aprire il pannello **Controller** e verificare che lo stato di entrambi i controller sul dispositivo sia **integro**. Selezionare un controller, fare clic con il pulsante destro del mouse, quindi selezionare **Riavvia** o **Arresto**.

    ![Riavviare o arrestare il controller di un dispositivo StorSimple](./media/storsimple-8000-manage-device-controller/manage-controller3.png)

4. Viene creato un processo per riavviare o arrestare il controller e vengono visualizzati degli avvisi, se presenti. Per monitorare il riavvio o l'arresto, passare a **Servizio > Log attività**, quindi filtrarli in base ai parametri specifici del servizio. Se un controller è stato arrestato, sarà necessario premere il pulsante di alimentazione presente su di esso per riaccenderlo.

#### <a name="to-restart-or-shut-down-a-controller-in-windows-powershell-for-storsimple"></a>Per riavviare o arrestare un controller in Windows PowerShell per StorSimple
Eseguire la procedura seguente per arrestare o riavviare un unico controller sul dispositivo StorSimple da Windows PowerShell per StorSimple.

1. Accedere al dispositivo tramite la console seriale o una sessione telnet da un computer remoto. Connettersi al controller 0 o al controller 1 seguendo i passaggi riportati in [Usare PuTTY per connettersi alla console seriale del dispositivo](storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).
2. Nel menu della console seriale, scegliere l'opzione 1, **Accedi con accesso completo**.
3. Nel messaggio dell'intestazione, prendere nota del controller a cui si è connessi (controller 0 o 1) e se è il controller attivo o passivo (standby).
   
   * Per arrestare un singolo controller, al prompt dei comandi, digitare:
     
       `Stop-HcsController`
     
       Il controller a cui si è connessi viene così arrestato. Se si arresta il controller attivo, verrà eseguito il failover del dispositivo sul controller passivo.

   * Per riavviare un controller, al prompt dei comandi, digitare:
     
       `Restart-HcsController`
     
       Il controller a cui si è connessi viene così riavviato. Se si riavvia il controller attivo, verrà eseguito il failover sul controller passivo prima del riavvio.

## <a name="shut-down-a-storsimple-device"></a>Arrestare un dispositivo StorSimple

In questa sezione viene illustrato come arrestare un dispositivo StorSimple in esecuzione o in errore da un computer remoto. Un dispositivo viene disattivato dopo l'arresto di entrambi i controller del dispositivo. L'arresto di un dispositivo viene eseguito quando il dispositivo viene spostato fisicamente o messo fuori servizio.

> [!IMPORTANT]
> Prima di arrestare il dispositivo, verificare l'integrità dei componenti del dispositivo. Passare al dispositivo e quindi fare clic su **Impostazioni > lntegrità hardware**. Nel pannello **Stato e integrità hardware**, verificare che lo stato del LED di tutti i componenti sia verde. Solo un dispositivo integro avrà lo stato verde. Se il dispositivo viene arrestato per la sostituzione di un componente che non funziona correttamente, verrà visualizzato lo stato di errore (rosso) o danneggiato (giallo) per i rispettivi componenti.


#### <a name="to-shut-down-a-storsimple-device"></a>Per arrestare un dispositivo StorSimple

1. Usare la procedura per [riavviare o arrestare un controller](#restart-or-shut-down-a-single-controller) per identificare e arrestare il controller passivo sul dispositivo. È possibile eseguire questa operazione nel portale di Azure o in Windows PowerShell per StorSimple.
2. Ripetere il passaggio precedente per arrestare il controller attivo.
3. È ora necessario osservare la superficie posteriore del dispositivo. Una volta che i due controller sono completamente arrestati, il LED di stato di entrambi i controller deve lampeggiare rosso. Se è necessario disattivare completamente il dispositivo in questa fase, posizionare gli interruttori di alimentazione dei moduli PCM (Power and Cooling Modules) su OFF. In tal modo il dispositivo viene spento.

## <a name="reset-the-device-to-factory-default-settings"></a>Ripristinare le impostazioni predefinite di fabbrica del dispositivo

> [!IMPORTANT]
> Se si desidera ripristinare le impostazioni predefinite di fabbrica del dispositivo, contattare il supporto Microsoft. La procedura descritta di seguito deve essere usata solo in combinazione con il supporto Microsoft.

Questa procedura descrive come ripristinare le impostazioni predefinite del dispositivo Microsoft Azure StorSimple usando Windows PowerShell per StorSimple.
La reimpostazione di un dispositivo comporta la rimozione di tutti i dati e le impostazioni dall'intero cluster per impostazione predefinita.

Per ripristinare le impostazioni predefinite di fabbrica del dispositivo StorSimple di Microsoft Azure, procedere come segue:

### <a name="to-reset-the-device-to-default-settings-in-windows-powershell-for-storsimple"></a>Per reimpostare il dispositivo per le impostazioni predefinite in Windows PowerShell per StorSimple
1. Accedere al dispositivo tramite la console seriale. Controllare il messaggio dell'intestazione per assicurarsi di essere connessi a controller **attivo**.
2. Nel menu della console seriale, scegliere l'opzione 1, **Accedi con accesso completo**.
3. Al prompt dei comandi digitare il comando seguente per ripristinare l'intero cluster, rimuovendo tutti i dati, i metadati e le impostazioni del controller:
   
    `Reset-HcsFactoryDefault`
   
    Per ripristinare invece un singolo controller, usare il cmdlet [Reset-HcsFactoryDefault](http://technet.microsoft.com/library/dn688132.aspx) con il parametro `-scope`.
   
    Il sistema verrà riavviato più volte. Verrà ricevuta una notifica al termine del processo di ripristino. A seconda del modello di sistema, per completare questo processo possono essere necessari 45-60 minuti per un dispositivo 8100 e 60-90 minuti per un dispositivo 8600.
   
## <a name="questions-and-answers-about-managing-device-controllers"></a>Domande e risposte sulla gestione dei controller del dispositivo
In questa sezione vengono riportate alcune delle domande frequenti relative alla gestione dei controller del dispositivo StorSimple.

**D.** Cosa accade se entrambi i controller del dispositivo sono integri e accesi e si riavvia o si arresta il controller attivo?

**R.** Se entrambi i controller del dispositivo sono integri e accesi, verrà richiesto di confermare. È possibile scegliere di:

* **Riavviare il controller attivo**: viene ricevuta una notifica indicante che il riavvio di un controller attivo comporta il failover del dispositivo sul controller passivo. Il controller viene riavviato.
* **Arrestare il controller attivo** - viene ricevuta una notifica indicante che l'arresto del controller attivo determina tempi di inattività. Inoltre, è necessario premere il pulsante di alimentazione sul dispositivo per accendere il controller.

**D.** Cosa accade se il controller passivo nel dispositivo non è disponibile o è spento e si riavvia o arresta il controller attivo?

**R.** Se il controller passivo sul dispositivo non è disponibile o è spento e si sceglie di:

* **Riavviare il controller attivo** : viene ricevuta una notifica indicante che se si continua l'operazione si verificherà un'interruzione temporanea del servizio e verrà richiesto di confermare.
* **Arrestare il controller attivo** - viene ricevuta una notifica indicante che la prosecuzione dell'operazione determina tempi di inattività. Inoltre, è necessario premere il pulsante di alimentazione su uno o entrambi i controller per accendere il dispositivo. Viene chiesto di confermare l'operazione.

**D.** Quand'è che il riavvio o l'arresto del controller non vengono eseguiti?

**R.** Il riavvio o l'arresto di un controller può non riuscire se:

* Un aggiornamento del dispositivo è in corso.
* Un riavvio del controller è già in corso.
* Un arresto del controller è già in corso.

**D.** Come si capisce se un controller è stato riavviato o arrestato?

**R.** È possibile controllare lo stato del controller nel pannello Controller. Lo stato del controller indica se un controller è in corso di riavvio o di arresto. Inoltre, nel pannello degli **avvisi** è incluso un avviso informativo indicante se il controller è stato riavviato o arrestato. Le operazioni di riavvio e arresto del controller vengono inoltre registrate nei log attività. Per altre informazioni sui log attività, passare a [Visualizzare i log attività](storsimple-8000-service-dashboard.md#view-the-activity-logs).

**D.** Il failover del controller ha impatto sulle operazioni di I/O?

**R.** Le connessioni TCP tra iniziatori e controller attivo verranno reimpostate a causa del failover del controller, ma verranno ristabilite quando il controller passivo assume il controllo. Nel corso di questa operazione potrebbe esserci una pausa temporanea (inferiore a 30 secondi) nell'attività di I/O tra gli iniziatori e il dispositivo.

**D.** Come ripristinare il controller di servizio dopo che è stato arrestato e rimosso?

**R.** Per ripristinare un controller di servizio, è necessario inserirlo nello chassis come descritto in [Sostituire un modulo controller nel dispositivo StorSimple](storsimple-8000-controller-replacement.md).

## <a name="next-steps"></a>Passaggi successivi
* Se si verificano problemi con i controller del dispositivo StorSimple che non si risolvono usando le procedure elencate in questa esercitazione, [contattare il supporto tecnico Microsoft](storsimple-8000-contact-microsoft-support.md).
* Per altre informazioni sull'uso del servizio Gestione dispositivi StorSimple, passare a [Uso del servizio Gestione dispositivi StorSimple per gestire il dispositivo StorSimple](storsimple-8000-manager-service-administration.md).

