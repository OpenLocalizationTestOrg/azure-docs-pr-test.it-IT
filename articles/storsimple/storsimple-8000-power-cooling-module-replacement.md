---
title: Sostituzione di un PCM nel dispositivo StorSimple serie 8000 | Microsoft Docs
description: Viene illustrato come rimuovere e sostituire il modulo di alimentazione e raffreddamento (PCM, Power and Cooling Module) nel dispositivo StorSimple
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/02/2017
ms.author: alkohli
ms.openlocfilehash: 7d181e6e434c998573dbea4b541cfacf7a28ee66
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="replace-a-power-and-cooling-module-on-your-storsimple-device"></a>Sostituzione di un modulo di alimentazione e raffreddamento nel dispositivo StorSimple
## <a name="overview"></a>Panoramica
Il modulo di alimentazione e raffreddamento (PCM, Power and Cooling Module) nel dispositivo Microsoft Azure StorSimple è costituito da un alimentatore e ventole di raffreddamento controllati attraverso gli chassis principale e EBOD. Esiste un solo modello di PCM certificato per ciascuno chassis. Lo chassis principale è certificato per un PCM 764 W e lo chassis EBOD è certificato per un PCM 580 W. Sebbene i PCM per lo chassis principale e lo chassis EBOD siano diversi, la procedura di sostituzione è identica.

In questa esercitazione viene illustrato come:

* Rimuovere un PCM
* Installare un PCM sostitutivo

> [!IMPORTANT]
> Prima di rimuovere e sostituire un PCM, esaminare le informazioni di sicurezza descritte in [Sostituzione dei componenti hardware di StorSimple](storsimple-8000-hardware-component-replacement.md).


## <a name="before-you-replace-a-pcm"></a>Prima di sostituire un PCM:
Prima di sostituire il PCM, tenere presente i seguenti aspetti importanti:

* Se l'alimentatore del PCM è guasto, lasciare il modulo guasto installato, ma rimuovere il cavo di alimentazione. La ventola continuerà a ricevere alimentazione dallo chassis e a fornire il raffreddamento appropriato. Se la ventola è guasta, il PCM deve essere sostituito immediatamente.
* Prima di rimuovere il PCM, disconnettere l'alimentazione da PCM disattivando l'interruttore principale (se presente) oppure rimuovendo fisicamente il cavo di alimentazione. Ciò determina la visualizzazione di un avviso sul sistema indicante che è imminente un'interruzione dell'alimentazione.
* Assicurarsi che l'altro PCM sia funzionale per un funzionamento continuato del sistema prima di sostituire il PCM guasto. Un PCM guasto deve essere sostituito con un PCM completamente funzionante appena possibile.
* La sostituzione del modulo PCM richiede solo alcuni minuti, ma deve essere completata entro 10 minuti dalla rimozione del PCM guasto per impedire il surriscaldamento.
* Notare che i moduli 764 W PCM di sostituzione forniti dal produttore non contengono il modulo batteria di backup. È necessario rimuovere la batteria dal PCM non funzionante, quindi inserirla nel modulo di sostituzione prima di eseguire la sostituzione. Per altre informazioni, vedere come [rimuovere e inserire un modulo batteria di backup](storsimple-8000-battery-replacement.md).

## <a name="remove-a-pcm"></a>Rimuovere un PCM
Per rimuovere un modulo di alimentazione e raffreddamento (PCM, Power and Cooling Module) dal dispositivo Microsoft Azure StorSimple, seguire queste istruzioni.

> [!NOTE]
> Prima di rimuovere il PCM, verificare di disporre di una sostituzione appropriata (764 W per lo chassis principale o 580 W per lo chassis EBOD).

#### <a name="to-remove-a-pcm"></a>Per rimuovere un PCM:
1. Nel portale di Azure classico, fare clic su **Impostazioni > Monitoraggio > Integrità hardware**. Controllare lo stato dei componenti del PCM sotto **Componenti condivisi** per identificare quale PCM è guasto:
   
   * Se un alimentatore in PCM 0 è guasto, lo stato di **Alimentatore in PCM 0** sarà rosso.
   * Se un alimentatore in PCM 1 è guasto, lo stato di **Alimentatore in PCM 1** sarà rosso.
   * Se la ventola in PCM 1 è guasta, lo stato di **Raffreddamento 0 per PCM 0** o **Raffreddamento 1 per PCM 0** sarà rosso.
2. Individuare il PCM guasto nella parte posteriore dello chassis principale. Se si esegue un modello 8600, identificare lo chassis principale controllando il numero di identificazione unità di sistema mostrato sul display LED del pannello anteriore. L'ID unità predefinito visualizzato sullo chassis principale è **00**, mentre l'ID unità predefinito visualizzato sullo chassis EBOD è **01**. Nel diagramma e nella tabella seguenti viene illustrato il pannello anteriore del display LED.
   
    ![ID del sistema sul pannello anteriore delle operazioni](./media/storsimple-power-cooling-module-replacement/IC740991.png)
   
     **Figura 1** Pannello anteriore del dispositivo  
   
   | Etichetta | Descrizione |
   |:--- |:--- |
   | 1 |Pulsante di disattivazione audio |
   | 2 |Alimentazione del sistema |
   | 3 |Errore del modulo |
   | 4 |Errore logico |
   | 5 |Display ID unità |
3. I LED degli indicatori di monitoraggio nella parte posteriore dello chassis principale possono inoltre essere utilizzati per identificare il PCM guasto. Vedere il diagramma e la tabella seguenti per comprendere come utilizzare i LED per individuare il PCM guasto. Ad esempio, se il LED corrispondente a **Guasto ventola** è attivo, la ventola è guasta. Allo stesso modo, se il LED corrispondente a **Guasto CA** è attivo, l'alimentatore è guasto. 
   
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
4. Fare riferimento al diagramma seguente relativo alla parte posteriore del dispositivo StorSimple per individuare il modulo PCM guasto. PCM 0 è a sinistra e PCM 1 è a destra. Nella tabella seguente vengono illustrati i moduli.
   
     ![Backplane dei moduli dello chassis principale del dispositivo](./media/storsimple-power-cooling-module-replacement/IC740994.png)
   
     **Figura 3** Parte posteriore del dispositivo con moduli plug-in 
   
   | Etichetta | Descrizione |
   |:--- |:--- |
   | 1 |PCM 0 |
   | 2 |PCM 1 |
   | 3 |Controller 0 |
   | 4 |Controller 1 |
5. Disattivare il PCM guasto e disconnettere il cavo di alimentazione. È ora possibile rimuovere il PCM.
6. Afferrare il chiavistello e il lato del punto di manipolazione del PCM tra il pollice e l'indice, quindi stringerli insieme per aprire il punto di manipolazione.
   
    ![Apertura del punto di manipolazione del PCM](./media/storsimple-power-cooling-module-replacement/IC740995.png)
   
    **Figura 4** Apertura del punto di manipolazione del PCM
7. Afferrare il punto di manipolazione e rimuovere il PCM.
   
    ![Rimozione del PCM del dispositivo](./media/storsimple-power-cooling-module-replacement/IC740996.png)
   
    **Figura 5** Rimozione del PCM

## <a name="install-a-replacement-pcm"></a>Installare un PCM sostitutivo
Seguire queste istruzioni per installare un PCM nel dispositivo StorSimple. Verificare di avere inserito il modulo batteria di backup prima di installare il PCM di sostituzione (si applica solo a 764 W PCM). Per altre informazioni, vedere come [rimuovere e inserire un modulo batteria di backup](storsimple-8000-battery-replacement.md).

#### <a name="to-install-a-pcm"></a>Per installare un PCM:
1. Verificare di disporre del PCM sostitutivo corretto per questo chassis. Per lo chassis principale è necessario un PCM 764 W e per lo chassis EBOD un PCM 580 W. Non tentare di utilizzare il PCM 580 W nello chassis principale o il PCM 764 W nello chassis EBOD. Nell'immagine seguente viene illustrato come identificare queste informazioni sull'etichetta apposta sul PCM.
   
    ![Etichetta del PCM del dispositivo](./media/storsimple-power-cooling-module-replacement/IC740973.png)
   
    **Figura 6** Etichetta del PCM
2. Verifica la presenza di danni sullo chassis, prestando particolare attenzione ai connettori. 
   
   > [!NOTE]
   > **Non installare il modulo se i perni dei connettori sono piegati.**
   > 
   > 
3. Con il punto di manipolazione del PCM in posizione aperta, far scorrere il modulo nello chassis.
   
    ![Installazione del PCM del dispositivo](./media/storsimple-power-cooling-module-replacement/IC740975.png)
   
    **Figura 7** Installazione del PCM
4. Chiudere manualmente il punto di manipolazione del PCM. Quando il punto di manipolazione viene attivato si dovrebbe ascoltare un clic.
   
   > [!NOTE]
   > Per assicurasi che i perni dei connettori siano attivati, è possibile tirare delicatamente il punto di manipolazione senza rilasciare il chiavistello. Se il PCM scorre fuori, il chiavistello è stato chiuso prima dell'attivazione dei connettori.
   
5. Connettere i cavi di alimentazione alla fonte di alimentazione e al PCM.
6. Fissare in posizione le fascette di serraggio.
7. Accendere il PCM.
8. Verificare che la sostituzione sia stata completata correttamente: nel portale di Azure del servizio Gestione dispositivi StorSimple, passare a **Impostazioni > Monitoraggio > Integrità hardware**. In **Componenti condivisi**, lo stato del PCM dovrebbe essere verde.
   
   > [!NOTE]
   > L'inizializzazione completa del PCM sostitutivo potrebbe richiedere alcuni minuti.

## <a name="next-steps"></a>Passaggi successivi
Leggere ulteriori informazioni sulla [Sostituzione dei componenti hardware di StorSimple](storsimple-8000-hardware-component-replacement.md).

