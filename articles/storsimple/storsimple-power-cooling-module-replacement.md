---
title: un PCM nel dispositivo StorSimple aaaReplace | Documenti Microsoft
description: Viene illustrato come tooremove e sostituire hello Power e modulo di raffreddamento (PCM) nel dispositivo StorSimple
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 24a158cb-0b79-4908-bb5a-431e48760f6a
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/18/2016
ms.author: alkohli
ms.openlocfilehash: cc19ccb29884557720f7538b90dfb05268330b72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="replace-a-power-and-cooling-module-on-your-storsimple-device"></a>Sostituzione di un modulo di alimentazione e raffreddamento nel dispositivo StorSimple
## <a name="overview"></a>Panoramica
Hello alimentazione e raffreddamento modulo PCM () nel dispositivo Microsoft Azure StorSimple costituito da un alimentatore e raffreddamento controllati tramite hello primario e l'enclosure EBOD. Esiste un solo modello di PCM certificato per ciascuno chassis. enclosure principale Hello è certificata per un PCM a 764 W ed enclosure EBOD hello è certificata per un PCM a 580 W. Anche se hello PCM enclosure principale hello e hello dell'enclosure EBOD sono diversi, la procedura di sostituzione hello è identica.

In questa esercitazione viene illustrato come:

* Rimuovere un PCM
* Installare un PCM sostitutivo

> [!IMPORTANT]
> Prima di rimozione e sostituzione di un PCM, esaminare le informazioni di sicurezza hello in [sostituzione dei componenti hardware StorSimple](storsimple-hardware-component-replacement.md).
> 
> 

## <a name="before-you-replace-a-pcm"></a>Prima di sostituire un PCM:
Tenere hello seguenti problemi importanti prima di sostituire il PCM:

* Alimentatore hello di hello guasto PCM, lasciare hello modulo non funzionante installato, ma rimuovere il cavo di alimentazione hello. ventola Hello continuerà alimentazione tooreceive enclosure hello e continuare tooprovide corretto raffreddamento. Se ha esito negativo della ventola hello, hello PCM deve toobe sostituito immediatamente.
* Prima di rimuovere hello PCM, scollegare hello alimentazione hello PCM disattivando interruttore hello (se presente) o rimuovendo il cavo di alimentazione hello. Ciò fornisce un sistema di tooyour di avviso che è imminente interruzione dell'alimentazione.
* Verificare che tale hello che è funzionale per l'altro PCM costantemente il funzionamento del sistema prima di sostituire hello PCM non funzionante. Un PCM guasto deve essere sostituito con un PCM completamente funzionante appena possibile.
* Sostituzione di un modulo PCM richiede solo pochi minuti toocomplete, ma deve essere completata entro 10 minuti dalla rimozione non riuscita hello PCM tooprevent surriscaldamento.
* Si noti che hello sostituzione 764 W i moduli PCM forniti dalla factory hello non contengano hello modulo batteria di backup. Sarà anche necessario batteria hello tooremove dal PCM non funzionante e quindi inserirla sostituzione hello di hello sostituzione modulo tooperforming precedente. Per ulteriori informazioni, vedere come troppo[rimuovere e inserire un modulo batteria di backup](storsimple-battery-replacement.md).

## <a name="remove-a-pcm"></a>Rimuovere un PCM
Quando si è pronti tooremove una potenza e modulo di raffreddamento (PCM) dal dispositivo di Microsoft Azure StorSimple, seguire queste istruzioni.

> [!NOTE]
> Prima di rimuovere il PCM, verificare di disporre di un componente sostitutivo corretto (764 W per l'enclosure principale hello) o 580 W per hello enclosure EBOD.
> 
> 

#### <a name="tooremove-a-pcm"></a>tooremove un PCM
1. Nel portale di Azure classico hello, fare clic su **dispositivi** > **manutenzione** > **stato Hardware**. Controllare lo stato di hello dei componenti PCM hello sotto **componenti condivisi** tooidentify quello non funzionante:
   
   * Se un alimentatore in PCM 0 non è riuscita, hello stato **alimentatore in PCM 0** sarà di colore rosso.
   * Se un alimentatore in PCM 1 non è riuscita, hello stato **alimentatore in PCM 1** sarà di colore rosso.
   * Se la ventola hello in PCM 1 non è riuscita, hello indicatore di stato del **raffreddamento 0 PCM 0** o **raffreddamento 1 PCM 0** sarà di colore rosso.
2. Individuare hello PCM non funzionante in hello eseguire il backup dell'enclosure principale hello. Se si esegue un modello 8600, identificare l'enclosure principale hello esaminando hello mostrato sul display LED sul pannello anteriore hello numero identificativo dell'unità del sistema. Hello predefinito visualizzato sull'enclosure principale hello è **00**, mentre il valore predefinito di hello ID di unità visualizzate nella hello enclosure EBOD è **01**. Hello diagramma e la tabella seguenti illustrano pannello anteriore di hello del display LED hello.
   
    ![ID del sistema sul pannello anteriore delle operazioni](./media/storsimple-power-cooling-module-replacement/IC740991.png)
   
     **Figura 1** pannello anteriore del dispositivo hello  
   
   | Etichetta | Descrizione |
   |:--- |:--- |
   | 1 |Pulsante di disattivazione audio |
   | 2 |Alimentazione del sistema |
   | 3 |Errore del modulo |
   | 4 |Errore logico |
   | 5 |Display ID unità |
3. può essere utilizzato anche il monitoraggio di indicatori LED di hello parte posteriore dell'enclosure principale hello Hello tooidentify hello PCM non funzionante. Vedere hello seguente diagramma e tabella come toounderstand toouse hello LED toolocate hello PCM non funzionante. Ad esempio, se hello LED corrispondente toohello **guasto ventola** è acceso, significa che la ventola hello non è riuscita. Analogamente, se hello LED corrispondente troppo**guasto AC** è acceso, significa che alimentatore hello non è riuscita. 
   
    ![Backplane degli indicatori LED di monitoraggio del PCM del dispositivo](./media/storsimple-power-cooling-module-replacement/IC740992.png)
   
     **Figura 2** Parte posteriore del PCM con i LED degli indicatori
   
   | Etichetta | Descrizione |
   |:--- |:--- |
   | 1 |Guasto dell’alimentazione CA |
   | 2 |Guasto alla ventola |
   | 3 |Guasto alla batteria |
   | 4 |PCM OK |
   | 5 |Guasto dell'alimentazione CC |
   | 6 |Integrità della batteria |
4. Fare riferimento toohello seguente diagramma di hello parte posteriore modulo PCM di hello StorSimple dispositivo toolocate hello non riuscita. PCM 0 si trova a sinistra di hello e PCM 1 è hello destra. tabella Hello che segue vengono illustrati i moduli di hello.
   
     ![Backplane dei moduli dello chassis principale del dispositivo](./media/storsimple-power-cooling-module-replacement/IC740994.png)
   
     **Figura 3** Parte posteriore del dispositivo con moduli plug-in 
   
   | Etichetta | Descrizione |
   |:--- |:--- |
   | 1 |PCM 0 |
   | 2 |PCM 1 |
   | 3 |Controller 0 |
   | 4 |Controller 1 |
5. Attivare off hello PCM non funzionante e scollegare cavo di alimentazione hello. È possibile rimuovere hello PCM.
6. Afferrare latch hello e lato hello di hello gestire PCM tra il pollice e l'indice, quindi premerli handle hello tooopen insieme.
   
    ![Apertura del punto di manipolazione del PCM](./media/storsimple-power-cooling-module-replacement/IC740995.png)
   
    **Figura 4** gestire hello apertura PCM
7. Tirare la maniglia hello e rimuovere hello PCM.
   
    ![Rimozione del PCM del dispositivo](./media/storsimple-power-cooling-module-replacement/IC740996.png)
   
    **Figura 5** rimozione hello PCM

## <a name="install-a-replacement-pcm"></a>Installare un PCM sostitutivo
Seguire questi tooinstall istruzioni un PCM del dispositivo StorSimple. Assicurarsi di avere inserito hello batteria di backup precedenti tooinstalling hello sostituzione di un modulo PCM (si applica solo PCM W too764). Per ulteriori informazioni, vedere come troppo[rimuovere e inserire un modulo batteria di backup](storsimple-battery-replacement.md).

#### <a name="tooinstall-a-pcm"></a>tooinstall un PCM
1. Verificare di aver hello PCM sostitutivo appropriato per questa enclosure. enclosure principale di Hello richiede un PCM a 764 W e hello enclosure EBOD deve un PCM a 580 W. Non è consigliabile tentare toouse hello PCM a 580 W enclosure principale hello o hello PCM 764 W in hello enclosure EBOD. Hello seguente immagine mostra se queste informazioni in hello etichetta ovvero tooidentify apposta toohello PCM.
   
    ![Etichetta del PCM del dispositivo](./media/storsimple-power-cooling-module-replacement/IC740973.png)
   
    **Figura 6** Etichetta del PCM
2. Controllare per enclosure toohello danni, prestando particolare attenzione toohello connettori. 
   
   > [!NOTE]
   > **Se qualsiasi connettore presenta pin piegati, non installare il modulo di hello.**
   > 
   > 
3. Con hello PCM gestire nel hello aprire posizione, il modulo hello diapositiva in enclosure hello.
   
    ![Installazione del PCM del dispositivo](./media/storsimple-power-cooling-module-replacement/IC740975.png)
   
    **Figura 7** installazione hello PCM
4. Chiudere manualmente maniglia del PCM hello. Quando hello handle fermo scatta, si sente un clic. 
   
   > [!NOTE]
   > si sono impegnati tooensure che hello pin dei connettori, è possibile tirare leggermente hello handle senza rilascio del latch hello. Se hello PCM scorre verso l'esterno, significa che il latch hello è stata chiusa prima hello connettori venissero inseriti.
   > 
   > 
5. Connettere hello cavi toohello power alimentazione e toohello PCM.
6. Proteggere ceppo hello Balle rilievo. 
7. Attivare hello PCM.
8. Verifica della corretta sostituzione hello: nel portale di Azure classico del servizio StorSimple Manager hello, passare troppo**dispositivi** > **manutenzione**  >  **Stato hardware**. In **componenti condivisi**, stato hello di hello PCM deve essere di colore verde. 
   
   > [!NOTE]
   > Potrebbe richiedere alcuni minuti per l'inizializzazione di toocompletely PCM sostitutivo hello.
   > 
   > 

## <a name="next-steps"></a>Passaggi successivi
Leggere ulteriori informazioni sulla [Sostituzione dei componenti hardware di StorSimple](storsimple-hardware-component-replacement.md).

