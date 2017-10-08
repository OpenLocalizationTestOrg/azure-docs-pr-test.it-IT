---
title: un controller del dispositivo StorSimple aaaReplace | Documenti Microsoft
description: Viene illustrato come tooremove e sostituire uno o entrambi i moduli controller sul dispositivo StorSimple.
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: e25b52b7-60f5-47f3-bffc-6c157d57ab5d
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 03/03/2017
ms.author: alkohli
ms.openlocfilehash: ebf5c5830120857f69909113e3a111f4dda30e57
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="replace-a-controller-module-on-your-storsimple-device"></a>Sostituire un modulo controller nel dispositivo StorSimple
## <a name="overview"></a>Panoramica
In questa esercitazione viene illustrato come tooremove e sostituire uno o entrambi i moduli controller in un dispositivo StorSimple. Viene inoltre hello sottostante la logica per scenari di sostituzione dei controller singolo e doppio hello.

> [!NOTE]
> Sostituzione di un controller di tooperforming precedente, è consigliabile aggiornare sempre la versione più recente di firmware toohello controller.
> 
> tooprevent danneggiare il dispositivo di StorSimple tooyour, non rimuovere controller hello fino a quando i LED hello hello seguenti:
> 
> * Tutte le luci sono impostate su OFF.
> * LED 3, ![icona segno di spunta verde](./media/storsimple-controller-replacement/HCS_GreenCheckIcon.png) e ![icona segno di spunta rossa](./media/storsimple-controller-replacement/HCS_RedCrossIcon.png) lampeggiano e LED 0 e LED 7 sono **ON**.
> 
> 

Hello nella tabella seguente illustra gli scenari di sostituzione controller hello è supportato.

| Caso | Scenario di sostituzione | Procedura applicabile |
|:--- |:--- |:--- |
| 1 |Un controller è in uno stato di errore, hello altro controller è integro e operativo. |[Singola sostituzione dei controller](#replace-a-single-controller), che descrive hello [logica alla base di sostituzione di un singolo controller](#single-controller-replacement-logic), nonché hello [procedura per la sostituzione](#single-controller-replacement-steps). |
| 2 |Entrambi i controller hello non riuscite e devono essere sostituiti. chassis Hello, dischi ed enclosure per dischi sono integri. |[Sostituzione di entrambi i controller](#replace-both-controllers), che descrive hello [logica alla base di una sostituzione di entrambi i controller](#dual-controller-replacement-logic), nonché hello [procedura per la sostituzione](#dual-controller-replacement-steps). |
| 3 |Controller da hello stesso dispositivo o da diversi dispositivi vengono scambiati. chassis Hello, dischi ed enclosure per dischi sono integri. |Verrà visualizzato un messaggio di avviso di mancata corrispondenza dello slot. |
| 4 |Un controller è manca e hello ha esito negativo altri controller. |[Sostituzione di entrambi i controller](#replace-both-controllers), che descrive hello [logica alla base di una sostituzione di entrambi i controller](#dual-controller-replacement-logic), nonché hello [procedura per la sostituzione](#dual-controller-replacement-steps). |
| 5 |Uno o entrambi i controller hanno avuto esito negativo. Dispositivo hello è possibile accedere tramite la console seriale hello o la comunicazione remota di Windows PowerShell. |[Contattare il supporto tecnico Microsoft](storsimple-contact-microsoft-support.md) per una procedura di sostituzione manuale. |
| 6 |controller Hello dispone di una versione di build diverso, che potrebbe essere dovuto a:<ul><li>I controller hanno una versione diversa del software.</li><li>I controller hanno una versione diversa del firmware.</li></ul> |Se le versioni di software di hello controller sono diverse, la logica di sostituzione hello rileva che e aggiornamenti hello versione del software sul controller sostitutivo hello.<br><br>Se sono diverse versioni del firmware dei controller hello e versione vecchia hello è **non** aggiornabile automaticamente un messaggio di avviso verrà visualizzato nel portale di Azure classico hello. Si deve cercare gli aggiornamenti e installare gli aggiornamenti del firmware hello.</br></br>Se sono diverse versioni del firmware dei controller hello e hello versione vecchia è aggiornabile automaticamente, logica di sostituzione controller hello rileverà la situazione e dopo l'avvio del controller hello, firmware hello verrà aggiornato automaticamente. |

È necessario un modulo controller tooremove se non è riuscito. Uno o entrambi i moduli controller hello possono avere esito negativo, che possono portare a una sostituzione di un singolo controller o sostituzione di entrambi i controller. Per procedure sostitutive e logica hello su cui si basano, vedere l'esempio hello:

* [Sostituire un singolo controller](#replace-a-single-controller)
* [Sostituire entrambi i controller](#replace-both-controllers)
* [Rimuovere un controller](#remove-a-controller)
* [Aggiungere un controller.](#insert-a-controller)
* [Identificare hello controller attivo sul dispositivo](#identify-the-active-controller-on-your-device)

> [!IMPORTANT]
> Prima di rimozione e sostituzione di un controller, esaminare le informazioni di sicurezza hello in [sostituzione dei componenti hardware StorSimple](storsimple-hardware-component-replacement.md).
> 
> 

## <a name="replace-a-single-controller"></a>Sostituire un singolo controller
Quando uno dei controller hello due dispositivi di Microsoft Azure StorSimple hello non è riuscita, non funziona correttamente o è mancante, è necessario tooreplace un singolo controller. 

### <a name="single-controller-replacement-logic"></a>Logica di sostituzione del singolo controller
La sostituzione di un singolo controller, è necessario rimuovere il servizio controller non funzionante hello. (controller rimanente hello dispositivo hello è controller attivo hello). Quando si inserisce controller sostitutivo hello, hello seguenti azioni:

1. controller sostitutivo Hello inizia immediatamente a comunicare con il dispositivo di StorSimple hello.
2. Uno snapshot di hello disco virtuale (VHD) per il controller attivo hello viene copiato nel controller sostitutivo hello.
3. snapshot Hello viene modificato in modo che quando il controller sostitutivo hello viene avviato da questo disco rigido virtuale, venga riconosciuto come controller in standby.
4. Una volta completate le modifiche di hello, controller sostitutivo hello verrà avviato come controller in standby hello.
5. Quando si eseguono entrambi i controller hello, hello cluster passa alla modalità online.

### <a name="single-controller-replacement-steps"></a>Procedura per la sostituzione di un singolo controller
Completare hello procedura seguente se uno dei controller hello nel dispositivo StorSimple di Microsoft Azure ha esito negativo. (hello altro controller deve essere attivo e in esecuzione. Se entrambi i controller guasto o di malfunzionamento, andare troppo[procedura di sostituzione di entrambi i controller](#dual-controller-replacement-steps).)

> [!NOTE]
> Può richiedere 30 a 45 minuti per toorestart controller hello e recuperare completamente dalla procedura di sostituzione hello singolo controller. durata totale Hello hello intera procedura, incluso il collegamento hello cavi, è di circa 2 ore.
> 
> 

#### <a name="tooremove-a-single-failed-controller-module"></a>tooremove un modulo singolo controller non funzionante
1. Nel portale di Azure classico hello, servizio StorSimple Manager toohello, quindi scegliere hello **dispositivi** scheda e quindi fare clic su nome hello del dispositivo di hello che si desidera toomonitor.
2. Andare troppo**manutenzione > stato dell'Hardware**. stato Hello del Controller 0 o Controller 1 deve essere rosso, che indica un errore.
   
   > [!NOTE]
   > controller non funzionante Hello in sostituzione di un singolo controller è sempre un controller in standby.
   > 
   > 
3. Utilizzare la figura 1 e hello modulo controller non di hello toolocate nella tabella seguente.  
   
    ![Backplane dei moduli dello chassis principale del dispositivo](./media/storsimple-controller-replacement/IC740994.png)
   
    **Figura 1** retro del dispositivo StorSimple
   
   | Etichetta | Descrizione |
   |:--- |:--- |
   | 1 |PCM 0 |
   | 2 |PCM 1 |
   | 3 |Controller 0 |
   | 4 |Controller 1 |
4. In hello controller non funzionante, rimuovere tutti i cavi di rete connessa hello di hello porte dati. Se si utilizza un modello 8600, rimuovere anche i cavi SAS che si connettono i controller EBOD toohello controller hello hello.
5. Seguire i passaggi di hello in [rimuovere un controller](#remove-a-controller) tooremove hello Impossibile controller. 
6. Sostituzione di factory installazione hello in hello stesso slot da cui controller non funzionante hello è stato rimosso. In questo modo viene attivata la logica di sostituzione di hello singolo controller. Per altre informazioni, vedere [Logica di sostituzione di un singolo controller](#single-controller-replacement-logic).
7. Mentre la logica di sostituzione di hello singolo controller viene eseguita in background hello, ricollegare i cavi di hello. Richiedere l'attenzione tooconnect che tutti i cavi hello hello esattamente allo stesso modo con cui erano collegati prima della sostituzione hello.
8. Una volta riavviato il controller di hello, controllare hello **lo stato del Controller** hello e **lo stato del Cluster** in hello Azure classico tooverify portale che hello controller tooa indietro lo stato è integro e in modalità standby .

> [!NOTE]
> Se si sta monitorando dispositivo hello tramite la console seriale hello, si verifichino più riavvii durante il ripristino dalla procedura di sostituzione hello hello. Quando viene presentato menu della console seriale hello, si saprà che hello di sostituzione è completata. Se il menu di hello non viene visualizzato entro 2 ore dall'inizio hello sostituzione dei controller, [contattare il supporto Microsoft](storsimple-contact-microsoft-support.md).
>
> A partire da Update 4, è inoltre possibile utilizzare i cmdlet di hello `Get-HCSControllerReplacementStatus` nell'interfaccia di Windows PowerShell hello hello toomonitor hello dello stato dei dispositivi del processo di sostituzione del controller hello.
> 

## <a name="replace-both-controllers"></a>Sostituire entrambi i controller
Quando entrambi i controller sul dispositivo Microsoft Azure StorSimple hello non sono riuscita, malfunzionamento o sono mancanti, è necessario tooreplace entrambi i controller. 

### <a name="dual-controller-replacement-logic"></a>Logica di sostituzione doppia del controller
In una doppia sostituzione di controller, rimuovere prima entrambi i controller che hanno avuto esito negativo e quindi inserire le sostituzioni. Quando vengono inseriti due controller di sostituzione hello, hello seguenti azioni:

1. il controller sostitutivo Hello nell'alloggiamento 0 controlla seguente hello:
   
   1. Sta utilizzando le versioni correnti di software e firmware hello?
   2. Si tratta di una parte del cluster hello?
   3. Controller peer hello in esecuzione ed è in cluster?
      
      Se nessuna di queste condizioni sono vere, controller hello ricerca per il backup giornaliero più recente di hello (si trova in hello **nonDOMstorage** sull'unità S). Hello controller copie hello allo snapshot più recente di hello disco rigido virtuale da un backup hello.
2. controller Hello nello slot 0 usa hello snapshot tooimage stesso.
3. Nel frattempo, controller hello nello slot 1 rimane in attesa per la creazione dell'immagine di controller 0 toocomplete hello e avvio.
4. Dopo l'avvio del controller 0, il controller 1 rileva cluster hello creato dal controller 0, che attiva la logica di sostituzione di hello singolo controller. Per altre informazioni, vedere [Logica di sostituzione di un singolo controller](#single-controller-replacement-logic).
5. Successivamente, verranno eseguito entrambi i controller e hello cluster passerà online.

> [!IMPORTANT]
> In seguito alla sostituzione di due controller, dopo aver configurato il dispositivo di StorSimple hello, è essenziale eseguire manuale di un backup del dispositivo hello. I backup giornalieri di configurazione dispositivo non vengono attivati fino a che non sono trascorse 24 ore. Lavorare con [supporto Microsoft](storsimple-contact-microsoft-support.md) toomake un backup manuale del dispositivo.
> 
> 

### <a name="dual-controller-replacement-steps"></a>Procedura per la sostituzione doppia del controller
Questo flusso di lavoro è obbligatorio quando entrambi i controller di hello nel dispositivo StorSimple di Microsoft Azure non è riuscita. Questo problema può verificarsi in un Data Center nel quale sistema di raffreddamento hello smette di funzionare e di conseguenza, non di entrambi i controller hello entro un breve periodo di tempo. A seconda se il dispositivo di StorSimple hello è attivato o disattivato, se si utilizza un 8600 o un modello 8100, un set diverso di passaggi è obbligatorio.

> [!IMPORTANT]
> Può richiedere 45 minuti too1 ora toorestart controller hello e recuperare completamente da una routine di sostituzione di entrambi i controller. durata totale Hello hello intera procedura, incluso il collegamento hello cavi, è di circa 2,5 ore.
> 
> 

#### <a name="tooreplace-both-controller-modules"></a>tooreplace entrambi i moduli controller
1. Se il dispositivo hello è disattivato, ignorare questo passaggio e continuare toohello successivo. Se il dispositivo hello è attivato, disattivare dispositivo hello.
   
   1. Se si utilizza un modello 8600, disattivare enclosure principale hello e quindi disattivare hello enclosure EBOD.
   2. Attendere che il dispositivo hello arresto completo. Tutti i LED di hello in hello parte posteriore dispositivo hello è disattivata.
2. Rimuovere tutti i cavi di rete hello sono porte dati toohello connesso. Se si utilizza un modello 8600, rimuovere anche i cavi SAS che connettono l'enclosure EBOD di hello enclosure principale toohello hello.
3. Rimuovere entrambi i controller dal dispositivo StorSimple hello. Per altre informazioni, vedere [Rimuovere un controller](#remove-a-controller).
4. Inserire prima sostituzione factory hello per Controller 0 e quindi inserire Controller 1. Per altre informazioni, vedere [Inserire un controller](#insert-a-controller). In questo modo viene attivata la logica di sostituzione di hello entrambi i controller. Per altre informazioni, vedere [Logica di sostituzione doppia del controller](#dual-controller-replacement-logic).
5. Mentre la logica di sostituzione di hello controller viene eseguita in background hello, ricollegare i cavi di hello. Richiedere l'attenzione tooconnect che tutti i cavi hello hello esattamente allo stesso modo con cui erano collegati prima della sostituzione hello. Vedere hello indicazioni dettagliate per il modello in hello cavo sezione dispositivo di [installare il dispositivo StorSimple 8100](storsimple-8100-hardware-installation.md) o [installare del dispositivo 8600 StorSimple](storsimple-8600-hardware-installation.md).
6. Accendere il dispositivo di StorSimple hello. Se si usa un modello 8600:
   
   1. Verificare che tale hello enclosure EBOD è accesa per prima.
   2. Attendere fino a quando non è in esecuzione hello enclosure EBOD.
   3. Accendere l'enclosure principale hello.
   4. Dopo il primo controller di hello riavviato e in uno stato integro, verrà eseguito il sistema hello.
      
      > [!NOTE]
      > Se si sta monitorando dispositivo hello tramite la console seriale hello, si verifichino più riavvii durante il ripristino dalla procedura di sostituzione hello hello. Quando viene visualizzato il menu di console seriale hello, si saprà che hello di sostituzione è completata. Se il menu di hello non viene visualizzato entro 2 ore e mezzo dall'inizio hello sostituzione dei controller, [contattare il supporto Microsoft](storsimple-contact-microsoft-support.md).
      > 
      > 

## <a name="remove-a-controller"></a>Rimuovere un controller
Utilizzare hello seguendo procedure tooremove un modulo controller danneggiato dal dispositivo StorSimple.

> [!NOTE]
> Hello illustrazioni seguenti è per il controller 0. Per il controller 1, questi potrebbe essere annullati.
> 
> 

#### <a name="tooremove-a-controller-module"></a>tooremove un modulo controller
1. Afferrare hello linguetta del modulo tra il pollice e l'indice.
2. Stringere delicatamente il pollice e l'indice toorelease insieme hello latch del controller.
   
    ![Rilascio della linguetta](./media/storsimple-controller-replacement/IC741047.png)
   
    **Figura 2** Rilascio della linguetta
3. Utilizzare latch hello come controller di hello handle tooslide esterno dello chassis hello.
   
    ![Scorrimento del Controller all'esterno dello Chassis](./media/storsimple-controller-replacement/IC741048.png)
   
    **Figura 3** controller hello estendibile esterno dello chassis hello

## <a name="insert-a-controller"></a>Aggiungere un controller.
Utilizzare hello seguendo procedure tooinstall un modulo controller fornito dal produttore dopo la rimozione di un modulo non funzionante dal dispositivo StorSimple.

#### <a name="tooinstall-a-controller-module"></a>tooinstall un modulo controller
1. Controllare la toosee toohello eventuali danni connettori di interfaccia. Se uno qualsiasi dei pin dei connettori hello sono piegato o danneggiato, non installare il modulo di hello.
2. Diapositiva modulo controller hello nello chassis hello mentre hello fermo completamente aperto. 
   
    ![Scorrimento del Controller all'interno dello Chassis](./media/storsimple-controller-replacement/IC741053.png)
   
    **Figura 4** inserimento del controller nello chassis hello
3. Con modulo controller hello inserito, iniziare chiusura del latch hello mentre continua toopush hello nello chassis hello. Hello fermo scatterà, controller hello tooguide nella posizione desiderata.
   
    ![Chiusura della linguetta del Controller](./media/storsimple-controller-replacement/IC741054.png)
   
    **Figura 5** chiusura del latch del controller hello
4. Quando si posiziona il latch hello correttamente completato. Hello **OK** LED dovrebbe ora essere in.  
   
   > [!NOTE]
   > Potrebbe essere necessaria fino too5 minuti per il controller di hello e hello tooactivate LED.
   > 
   > 
5. tooverify che ha esito positivo, in sostituzione di hello hello Azure classico, andare troppo**dispositivi** > **manutenzione** > **stato Hardware**e assicurarsi che sia controller 0 e controller 1 siano integri (lo stato sia verde).

## <a name="identify-hello-active-controller-on-your-device"></a>Identificare hello controller attivo sul dispositivo
Esistono molte situazioni, ad esempio primo dispositivo registrazione o la sostituzione controller, che richiedono il controller attivo di hello toolocate in un dispositivo StorSimple. controller attivo Hello elabora tutti hello operazioni su disco del firmware e rete. È possibile utilizzare uno qualsiasi dei seguenti controller attivo di metodi tooidentify hello hello:

* [Usare controller attivo hello Azure tooidentify portale classico di hello](#use-the-azure-classic-portal-to-identify-the-active-controller)
* [Utilizzo di Windows PowerShell per il controller attivo hello tooidentify di StorSimple](#use-windows-powershell-for-storsimple-to-identify-the-active-controller)
* [Controllare i controller attivo hello tooidentify dispositivo fisico hello](#check-the-physical-device-to-identify-the-active-controller)

Ognuna di queste procedure è descritta di seguito.

### <a name="use-hello-azure-classic-portal-tooidentify-hello-active-controller"></a>Usare controller attivo hello Azure tooidentify portale classico di hello
Nel portale di Azure classico hello, passare troppo**dispositivi** > **manutenzione**, scorrere fino a toohello **controller** sezione. Qui è possibile verificare quale controller è attivo.

![Identificare il controller attivo nel portale di Azure classico](./media/storsimple-controller-replacement/IC752072.png)

**Figura 6** controller attivo di hello che Mostra portale di Azure classico

### <a name="use-windows-powershell-for-storsimple-tooidentify-hello-active-controller"></a>Utilizzo di Windows PowerShell per il controller attivo hello tooidentify di StorSimple
Quando si accede a un dispositivo tramite la console seriale hello, viene visualizzato un messaggio banner. messaggio banner contiene informazioni sul dispositivo, ad esempio modello hello, nome, versione del software installata e stato del controller hello che si accede. Hello seguente immagine mostra un esempio di un messaggio banner:

![Messaggio di intestazione seriale](./media/storsimple-controller-replacement/IC741098.png)

**Figura 7** Messaggio di intestazione che mostra il controller 0 come attivo

È possibile utilizzare hello intestazione messaggio toodetermine se hello controller si è connessi toois attivo o passivo.

### <a name="check-hello-physical-device-tooidentify-hello-active-controller"></a>Controllare i controller attivo hello tooidentify dispositivo fisico hello
controller attivo di hello tooidentify sul dispositivo, individuare il LED di hello blu sopra la porta dati 5 hello in hello parte posteriore dell'enclosure principale hello.

Se il LED è lampeggiante, hello controller è attivo e hello altro controller è in modalità standby. Tabella come ausilio utilizzare hello seguente diagramma.

![Piano posteriore dell'enclosure principale del dispositivo con porte dati](./media/storsimple-controller-replacement/IC741055.png)

**Figura 8** Parte posteriore dell’enclosure principale con porte dati e  LED di monitoraggio

| Etichetta | Descrizione |
|:--- |:--- |
| 1-6 |porte di rete DATI da 0 a 5 |
| 7 |LED blu |

## <a name="next-steps"></a>Passaggi successivi
Leggere ulteriori informazioni sulla [Sostituzione dei componenti hardware di StorSimple](storsimple-hardware-component-replacement.md).

