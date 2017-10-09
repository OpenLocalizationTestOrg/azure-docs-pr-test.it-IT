---
title: indicatori di monitoraggio aaaStorSimple | Documenti Microsoft
description: Descrive hello diodi a emissione luminosa (LED) e lo stato di allarmi acustici utilizzati toomonitor hello del dispositivo StorSimple hello.
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 59dee7b9-ca6d-4fd9-96e6-a0071e8d248e
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: alkohli
ms.openlocfilehash: e690b8f4727272f5fbb8886a594a046f794a1380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-monitoring-indicators-toomanage-your-device"></a>Usare il dispositivo di StorSimple toomanage indicatori di monitoraggio
## <a name="overview"></a>Panoramica
Il dispositivo StorSimple include diodi a emissione luminosa (LED) e avvisi che è possibile utilizzare toomonitor hello moduli e stato generale del dispositivo StorSimple hello. indicatori di monitoraggio Hello è reperibile in componenti hardware hello enclosure principale del dispositivo hello e hello EBOD. Hello indicatori di monitoraggio può essere LED o allarmi acustici.

Esistono tre stati utilizzati tooindicate hello LED di un modulo: verde, intermittente giallo-verde toored, o rosso-ambra.  

* I LED verdi indicano uno stato operativo integro.  
* Toored-ambra verde lampeggiante LED rappresentano presenza hello di condizioni non critiche che potrebbero richiedere l'intervento dell'utente.  
* LED rosso-ambra indicano che è presente un errore critico presente nel modulo hello.  

Hello parte restante di questo articolo vengono descritti diversi indicatori LED di monitoraggio, le relative posizioni nel dispositivo StorSimple hello hello, lo stato del dispositivo hello basato su hello dei LED e qualsiasi allarmi acustici associati.

## <a name="front-panel-indicator-leds"></a>Indicatori LED sul pannello anteriore
pannello anteriore Hello, noto anche come hello *pannello operativo* o *al pannello ops*, Visualizza lo stato di aggregazione hello di tutti i moduli di hello nel sistema hello. pannello anteriore Hello è identico in hello StorSimple primario e hello enclosure EBOD e viene riportato di seguito.  

   ![Pannello anteriore del dispositivo][1]

pannello anteriore Hello contiene hello indicatori seguenti:  

1. Pulsante di disattivazione audio
2. Indicatore LED (verde/rosso-ambra) di alimentazione
3. Indicatore LED di errore nel modulo (ACCESO rosso-ambra/SPENTO)
4. Indicatore LED di errore logico (ACCESO rosso-ambra/SPENTO)
5. Display ID unità  

la differenza principale tra pannello anteriore hello LED per il dispositivo hello e quelle per l'enclosure EBOD hello Hello è hello **numero di identificazione di unità di sistema** mostrato sul display LED hello. unità di Hello predefinito visualizzato sul dispositivo hello è **00**, mentre l'ID di unità predefinito hello visualizzato in hello enclosure EBOD è **01**. In questo modo è tooquickly distinguere tra il dispositivo hello ed enclosure EBOD hello quando hello dispositivo viene acceso. Se il dispositivo è disattivato, utilizzare le informazioni di hello disponibili [accendere un nuovo dispositivo](storsimple-turn-device-on-or-off.md#turn-on-a-new-device) dispositivo hello toodifferentiate hello enclosure EBOD.  

## <a name="front-panel-led-status"></a>Stato dei LED sul pannello anteriore
Utilizzare hello seguente lo stato di hello tooidentify tabella indicato dalle hello LED sul pannello anteriore di hello per hello dispositivo o l'enclosure EBOD hello.  

| Alimentazione del sistema | Errore del modulo | Errore logico | Allarme | Stato |
| --- | --- | --- | --- | --- |
| Rosso-ambra |DISATTIVA |DISATTIVA |N/D |Alimentazione CA interrotta, funzionamento alimentazione di backup oppure alimentazione in e sono stati rimossi i moduli controller hello. |
| Verde |ATTIVA |ATTIVA |N/D |Stato del test di alimentazione del pannello delle operazioni acceso (5 sec) |
| Verde |DISATTIVA |DISATTIVA |N/D |Acceso, funzionamento corretto |
| Verde |ATTIVA |N/D |LED di errore PCM, LED di malfunzionamento ventola |Qualsiasi errore PCM, errore delle ventola oppure sotto o sovratemperatura |
| Verde |ATTIVA |N/D |LED modulo I/O |Qualsiasi errore del modulo controller |
| Verde |ATTIVA |N/D |N/D |Errore logico chassis |
| Verde |Lampeggiante |N/D |LED di stato del modulo sul modulo controller. LED di errore PCM, LED di malfunzionamento ventola |Tipo di modulo controller installato sconosciuto, errore del bus I2C, errore di configurazione del controller del modulo VPD (vital product data) |

## <a name="power-cooling-module-pcm-indicator-leds"></a>Indicatori LED del modulo di alimentazione e raffreddamento (PCM)
Alimentazione e raffreddamento (PCM) indicatori LED del modulo sono reperibile in hello parte posteriore dell'enclosure principale hello o enclosure EBOD ogni modulo PCM. Questo argomento viene illustrato come hello toouse seguente lo stato di hello toomonitor LED del dispositivo StorSimple.  

* LED PCM per enclosure principale hello
* LED PCM per hello enclosure EBOD

## <a name="pcm-leds-for-hello-primary-enclosure"></a>LED PCM per enclosure principale hello
dispositivo StorSimple Hello dispone di un modulo PCM da 764 w con una batteria aggiuntiva. Hello figura seguente Mostra pannello dei LED hello per dispositivo hello.  

   ![LED PCM nell'enclosure principale hello][2]

Legenda dei LED:

1. Guasto dell’alimentazione CA
2. Guasto alla ventola
3. Guasto alla batteria
4. PCM OK
5. Guasto CC
6. Batteria integra  

LED di stato di Hello di hello che PCM è indicato in hello pannello. Pannello LED del PCM di Hello dispositivo ha sei LED. Quattro di questi LED display hello stato alimentatore hello e ventola hello. Hello rimanenti due LED indica stato hello del modulo batteria di backup hello hello PCM. È possibile utilizzare hello seguenti tabelle toodetermine hello stato hello PCM.  

### <a name="pcm-indicator-leds-for-power-supply-and-fan"></a>Indicatori LED del PCM per l'alimentatore e la ventola
| Stato | PCM OK (verde) | Guasto CA (ambra) | Guasto ventola (ambra) | Guasto CC (ambra) |
| --- | --- | --- | --- | --- |
| Nessuna alimentazione CA (tooenclosure) |DISATTIVA |DISATTIVA |DISATTIVA |DISATTIVA |
| Alimentazione CA assente (solo questo PCM) |DISATTIVA |ATTIVA |DISATTIVA |ATTIVA |
| CA presente PCM ATTIVO - OK |ATTIVA |DISATTIVA |DISATTIVA |DISATTIVA |
| Guasto PCM (guasto ventola) |DISATTIVA |DISATTIVA |ATTIVA |N/D |
| Errore PCM (sovramperaggio, sovratensione, sovracorrente) |DISATTIVA |ATTIVA |ATTIVA |ATTIVA |
| PCM (ventola fuori tolleranza) |ATTIVA |DISATTIVA |DISATTIVA |ATTIVA |
| Modalità standby |Intermittente |DISATTIVA |DISATTIVA |DISATTIVA |
| Download firmware PCM |DISATTIVA |Intermittente |Intermittente |Intermittente |

### <a name="pcm-indicator-leds-for-hello-backup-battery"></a>Indicatori LED del PCM per batteria di backup hello
| Stato | Batteria integra (verde) | Errore batteria (ambra) |
| --- | --- | --- |
| Batteria assente |DISATTIVA |DISATTIVA |
| Batteria presente e carica |ATTIVA |DISATTIVA |
| Batteria in carica o scarica per manutenzione |Intermittente |DISATTIVA |
| Errore batteria "software" (recuperabile) |DISATTIVA |Intermittente |
| Errore batteria "hardware" (non recuperabile) |DISATTIVA |ATTIVA |
| Batteria disattivata |Intermittente |DISATTIVA |

## <a name="pcm-leds-for-hello-ebod-enclosure"></a>LED PCM per hello enclosure EBOD
Hello chassis EBOD ha un PCM a 580 w e nessuna batteria aggiuntiva. il pannello PCM Hello per hello chassis EBOD ha indicatori LED solo per hello alimentatori e ventole hello. Hello figura seguente mostra questi LED.

   ![LED PCM hello enclosure EBOD][3] 

È possibile utilizzare hello seguente tabella toodetermine hello stato hello PCM.  

| Stato | PCM OK (verde) | Guasto CA (ambra) | Guasto ventola (ambra) | Guasto CC (ambra) |
| --- | --- | --- | --- | --- |
| Nessuna alimentazione CA (tooenclosure) |DISATTIVA |DISATTIVA |DISATTIVA |DISATTIVA |
| Alimentazione CA assente (solo questo PCM) |DISATTIVA |ATTIVA |DISATTIVA |ATTIVA |
| CA presente PCM ATTIVO - OK |ATTIVA |DISATTIVA |DISATTIVA |DISATTIVA |
| Guasto PCM (guasto ventola) |DISATTIVA |DISATTIVA |ATTIVA |X |
| Errore PCM (sovramperaggio, sovratensione, sovracorrente) |DISATTIVA |ATTIVA |ATTIVA |ATTIVA |
| PCM (ventola fuori tolleranza) |ATTIVA |DISATTIVA |DISATTIVA |ATTIVA |
| Modello standby |Intermittente |DISATTIVA |DISATTIVA |DISATTIVA |
| Download firmware PCM |DISATTIVA |Intermittente |Intermittente |Intermittente |

## <a name="controller-module-indicator-leds"></a>Indicatori LED del modulo controller
dispositivo StorSimple Hello contiene LED per il controller primario di hello e i moduli controller EBOD di hello.   

### <a name="monitoring-leds-for-hello-primary-controller"></a>LED di monitoraggio per il controller primario di hello
Hello figura riportata di seguito consente di identificare hello LED sul controller primario di hello. (Tutti i componenti di hello sono elencati tooaid orientamento).  

   ![LED di monitoraggio - controller primario][4]

Utilizzare hello seguente tabella toodetermine se il modulo controller hello funziona correttamente.  

### <a name="controller-indicator-leds"></a>Indicatori LED del controller
| LED | Descrizione |
| --- | --- |
| LED ID (blu) |Indica che tale modulo hello è stato identificato. Se il LED blu hello è lampeggiante in un controller in esecuzione, quindi hello controller è hello controller attivo e hello altro è hello controller in standby. Per ulteriori informazioni, vedere [controller attivo hello di identificazione sul dispositivo](storsimple-8000-controller-replacement.md#identify-the-active-controller-on-your-device). |
| LED errore (ambra) |Indica un errore nel controller hello. |
| LED OK (verde) |Luce verde fissa indica che controller hello OK. Una luce verde intermittente indica un errore di configurazione del controller VPD. |
| LED attività SAS (verde) |Una luce verde continua indica una connessione senza attività corrente. Una luce verde lampeggiante indica hello connessione dispone di un'attività in corso. |
| LED stato Ethernet |Il lato destro indica un’attività di collegamento/rete: collegamento attivo (verde continuo), attività di rete (verde intermittente). Il lato sinistro indica la velocità di rete: 1000 Mb/s (giallo), 100 Mb/s (verde) e 10 Mb/s (SPENTA). A seconda del modello componente hello, la luce potrebbe lampeggi anche se l'interfaccia di rete hello non è abilitato. |
| LED POST |Indica lo stato di avanzamento di hello avvio quando hello controller viene acceso. Se il dispositivo di StorSimple hello non riesce tooboot, questo LED identificare il supporto Microsoft hello punto hello procedura di avvio in cui si è verificato un errore di hello. |

> [!IMPORTANT]
> Se il LED di errore hello è acceso, significa che è un problema con il modulo controller hello che può essere risolto riavviando controller hello. Se il controller hello il riavvio non risolve il problema, contattare il supporto Microsoft.  
> 
> 

### <a name="monitoring-leds-for-hello-ebod-ebod-enclosure"></a>LED di monitoraggio per hello EBOD (enclosure EBOD)
Ogni hello 6 Gb/controller EBOD SAS s dispone di LED che indicano lo stato, come illustrato nella seguente figura hello.  

  ![LED di monitoraggio - chassis EBOD][5]

La tabella seguente hello utilizzare toodetermine se hello modulo controller EBOD funziona normalmente.  

### <a name="ebod-controller-module-indicator-leds"></a>Indicatori LED del modulo controller EBOD
| Stato | Modulo I/O OK (verde) | Errore modulo I/O (ambra) | Attività porta host (verde) |
| --- | --- | --- | --- |
| Modulo controller OK |ATTIVA |DISATTIVA |- |
| Errore del modulo controller |DISATTIVA |ATTIVA |- |
| Nessuna connessione porta host esterna |- |- |DISATTIVA |
| Connessione porta host esterna – Nessuna attività |- |- |ATTIVA |
| Connessione porta host esterna – Attività |- |- |Intermittente |
| Errore metadati modulo controller |Intermittente |- |- |

## <a name="disk-drive-indicator-leds-for-hello-primary-enclosure-and-ebod-enclosure"></a>Indicatori LED delle unità di disco per hello enclosure principale ed EBOD
dispositivo StorSimple Hello è l'unità disco situate sia hello primario e hello EBOD. Come descritto in questa sezione, ogni unità disco contiene indicatori LED di monitoraggio. 

Per le unità disco, hello hello lo stato è indicato da una verde LED e un LED rosso-ambra montati nella parte anteriore hello di ogni modulo di gestione delle spedizioni di unità. Hello figura seguente mostra questi LED.

  ![LED delle unità disco][6]

Utilizzare hello seguente lo stato della tabella toodetermine hello di ogni unità disco, che a sua volta influisce sull'hello stato LED sul pannello anteriore.  

### <a name="disk-drive-indicator-leds-for-hello-ebod-enclosure"></a>Indicatori LED delle unità di disco per hello enclosure EBOD
| Stato | LED attività OK (verde) | LED errore (rosso-ambra) | LED pannello delle operazioni associato |
| --- | --- | --- | --- |
| Nessuna unità installata |DISATTIVA |DISATTIVA |None |
| Unità installata e operativa |Intermittente acceso/spento in base all’attività |X |None |
| Set di identità del dispositivo servizi chassis SCSI (SES) |ATTIVA |Intermittenza 1 secondo accesa/1 secondo spenta |None |
| Set bit errore dispositivo SES |ATTIVA |ATTIVA |Errore logico (rosso) |
| Errore circuito di controllo alimentazione |DISATTIVA |ATTIVA |Errore del modulo (rosso) |

## <a name="audible-alarms"></a>Allarmi acustici
Un dispositivo StorSimple contiene allarmi acustici sia enclosure principale hello e hello EBOD. Un allarme acustico si trova sul pannello anteriore hello (detto anche pannello operativo hello) di entrambe le enclosure. allarme acustico Hello indica quando una condizione di errore è presente. Hello seguenti condizioni attiverà allarme hello:  

* Guasto alla ventola o errore
* Voltaggio fuori misura
* Condizione di sovra o sottotemperatura
* Sovraccarico termico
* Errore di sistema
* Errore logico
* Errore di alimentazione
* Rimozione di un modulo di alimentazione e raffreddamento (PCM)  

Hello nella tabella seguente vengono descritti hello vari stati di allarme.  

### <a name="alarm-states"></a>Stati di allarme
| Stato di allarme | Azione | Azione con il pulsante di disattivazione audio premuto |
| --- | --- | --- |
| S0 |Modalità normale: invisibile all'utente |Doppio segnale acustico |
| S1 |Modalità errore: 1 secondo accesa/1 secondo spenta |La transizione tooS2 o S3 (vedere note) |
| S2 |Modalità promemoria: segnale acustico intermittente |None |
| S3 |Modalità disattivato: invisibile all'utente |None |
| S4 |Modalità errore critico: allarme continuo |Non disponibile: disattivazione non attiva |

> [!NOTE]
> * Nello stato S1, se non si preme Disattiva entro 2 minuti, hello automaticamente transizioni di stato tooS2 o S3.  
> * Stati di allarme S1 tooS4 restituire tooS0 dopo la condizione di errore hello.  
> * Lo stato di errore critico S4 può essere immesso da qualunque altro stato.  


È possibile disattivare l'allarme acustico hello premendo l'apposito pulsante hello al pannello ops hello. Verrà disattivato automaticamente dopo due minuti se l'opzione Disattiva hello non viene premuto manualmente. Quando viene disattivato l'allarme hello continueranno toosound con tooindicate brevi Beep intermittenti che esista ancora un problema. allarme Hello sarà invisibile all'utente quando vengono cancellati tutti i problemi di hello.

Hello nella tabella seguente vengono descritti hello varie condizioni di allarme.

### <a name="alarm-conditions"></a>Condizioni di allarme
| Stato | Gravità | Allarme | LED pannello delle operazioni |
| --- | --- | --- | --- |
| Avviso PCM - Interruzione dell'alimentazione CD da un singolo PCM |Errore – Perdita di ridondanza assente |S1 |Errore del modulo |
| Avviso PCM - Interruzione dell'alimentazione CD da un singolo PCM |Errore – Perdita di ridondanza |S1 |Errore del modulo |
| Guasto ventola del PCM |Errore – Perdita di ridondanza |S1 |Errore del modulo |
| Errore PCM rilevato dal modulo SBB |Errore |S1 |Errore del modulo |
| PCM rimosso |Errore di configurazione |None |Errore del modulo |
| Errore di configurazione dello chassis |Errore - Critico |S1 |Errore del modulo |
| Allerta temperatura di avviso bassa |Avviso |S1 |Errore del modulo |
| Allerta temperatura di avviso alta |Avviso |S1 |Errore del modulo |
| Allarme sovratemperatura |Errore - Critico |S1 |Errore del modulo |
| Errore del bus I2C |Errore – Perdita di ridondanza |S1 |Errore del modulo |
| Errore di comunicazione (I2C) del pannello delle operazioni |Errore - Critico |S1 |Errore del modulo |
| Errore del controller |Errore - Critico |S1 |Errore del modulo |
| Errore del modulo di interfaccia SBB |Errore - Critico |S1 |Errore del modulo |
| Errore del modulo di interfaccia SBB - Moduli funzionanti rimanenti non presenti |Errore - Critico |S4 |Errore del modulo |
| Modulo interfaccia SBB rimosso |Avviso |None |Errore del modulo |
| Errore di controllo dell’alimentazione dell’unità |Avviso - Interruzione dell'alimentazione dell’unità assente |S1 |Errore del modulo |
| Errore di controllo dell’alimentazione dell’unità |Errore - Critico; interruzione dell'alimentazione unità |S1 |Errore del modulo |
| Unità rimossa |Avviso |None |Errore del modulo |
| Disponibilità alimentazione insufficiente |Avviso |None |Errore del modulo |

## <a name="next-steps"></a>Passaggi successivi
Ulteriori informazioni sui [componenti hardware e sullo stato di StorSimple](storsimple-8000-monitor-hardware-status.md)

[1]: ./media/storsimple-monitoring-indicators/storsimple-monitoring-indicators-IMAGE01.png
[2]: ./media/storsimple-monitoring-indicators/storsimple-monitoring-indicators-IMAGE02.png
[3]: ./media/storsimple-monitoring-indicators/storsimple-monitoring-indicators-IMAGE03.png
[4]: ./media/storsimple-monitoring-indicators/storsimple-monitoring-indicators-IMAGE04.png
[5]: ./media/storsimple-monitoring-indicators/storsimple-monitoring-indicators-IMAGE05.png
[6]: ./media/storsimple-monitoring-indicators/storsimple-monitoring-indicators-IMAGE06.png


