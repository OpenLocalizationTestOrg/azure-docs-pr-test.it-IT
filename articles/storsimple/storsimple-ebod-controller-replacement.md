---
title: un controller di EBOD StorSimple aaaReplace | Documenti Microsoft
description: Viene illustrato come tooremove e sostituire uno o entrambi i controller EBOD in un dispositivo 8600 StorSimple.
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 8cbfa507-1a56-4e24-99dd-7db9abd3b850
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 5d29de2ee30bfdd70910050eee5cfa1d293d444f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="replace-an-ebod-controller-on-your-storsimple-device"></a>Sostituzione di un controller EBOD nel dispositivo StorSimple
## <a name="overview"></a>Panoramica
In questa esercitazione viene illustrato come tooreplace un modulo controller EBOD guasto nel dispositivo StorSimple di Microsoft Azure. un modulo controller EBOD tooreplace, è necessario:

* Rimuovere i controller EBOD guasto hello
* Installare un nuovo controller EBOD

Prendere in considerazione hello prima di iniziare le seguenti informazioni:

* In tutti gli slot inutilizzati, è necessario inserire moduli EBOD vuoti. Hello enclosure non viene raffreddata correttamente se un alloggiamento viene lasciato aperto.
* controller EBOD Hello è collegabile a caldo e può essere rimosso o sostituito. Non rimuovere un modulo guasto finché non si dispone di una sostituzione. Quando si avvia il processo di sostituzione hello, deve essere completato entro 10 minuti.

> [!IMPORTANT]
> Prima di tentare di tooremove o sostituire qualsiasi componente di StorSimple, verificare che hello [convenzioni delle icone di sicurezza](storsimple-safety.md#safety-icon-conventions) e altri [precauzioni di sicurezza](storsimple-safety.md).
> 
> 

## <a name="remove-an-ebod-controller"></a>Rimozione di un controller EBOD
Prima di sostituire hello Impossibile modulo controller EBOD nel dispositivo StorSimple, assicurarsi che hello altro modulo controller EBOD sia attivo e in esecuzione. Hello procedura e la tabella seguente viene illustrato come tooremove hello modulo controller EBOD.

#### <a name="tooremove-an-ebod-module"></a>tooremove un modulo EBOD
1. Hello aprirlo portale di Azure classico.
2. Passare troppo**dispositivi** > **manutenzione** > **stato Hardware**e verificare che i LED di stato hello di hello per hello EBOD attivo modulo controller sia di colore verde e hello LED per il modulo controller EBOD di hello non riuscito di colore rosso.
3. Posizionate hello parte posteriore dispositivo hello modulo controller EBOD di hello non riuscita.
4. Rimuovere i cavi di hello che collegano i controller di toohello modulo controller EBOD hello prima di rimuovere il modulo EBOD hello dal sistema hello.
5. Prendere nota di hello porta SAS del modulo controller EBOD hello che era connesso toohello controller. Dopo aver sostituito modulo EBOD hello sarà configurazione toothis del sistema hello toorestore obbligatorio. 
   
   > [!NOTE]
   > In genere, questa sarà la porta A, contrassegnato come **ospitare in** nel seguente diagramma hello.
   > 
   > 
   
    ![Backplane del controller EBOD](./media/storsimple-ebod-controller-replacement/IC741049.png)
   
     **Figura 1** Parte posteriore del modulo EBOD
   
   | Etichetta | Descrizione |
   |:--- |:--- |
   | 1 |LED di errore |
   | 2 |LED di alimentazione |
   | 3 |Connettori SAS |
   | 4 |LED SAS |
   | 5 |Porte seriali solo per l'utilizzo predefinito |
   | 6 |Porta (Host in entrata) |
   | 7 |Porta B (Host in uscita) |
   | 8 |Porta C (solo per utilizzo predefinito) |

## <a name="install-a-new-ebod-controller"></a>Installare un nuovo controller EBOD
Hello procedura e la tabella seguente viene illustrato come tooinstall un modulo controller EBOD del dispositivo StorSimple.

#### <a name="tooinstall-an-ebod-controller"></a>tooinstall un controller EBOD
1. Controllare hello EBOD dispositivo siano presenti danneggiamenti, in particolare toohello connettore di interfaccia. Se qualsiasi pin piegati, non installare il nuovo controller di EBOD hello.
2. Aprire posizione, il modulo hello diapositiva in enclosure hello fino a quando non hello scattare latch hello in hello.
   
    ![Installazione del controller EBOD](./media/storsimple-ebod-controller-replacement/IC741050.png)
   
    **Figura 2** modulo controller EBOD hello di installazione
3. Latch hello Chiudi. Quando si attiva il latch hello, si sente un clic.
   
    ![Rilascio del latch EBOD](./media/storsimple-ebod-controller-replacement/IC741047.png)
   
    **Figura 3** chiusura del latch del modulo EBOD hello
4. Ricollegare i cavi di hello. Utilizzare configurazione esatta hello che era presente prima della sostituzione hello. Vedere hello seguente diagramma e tabella per informazioni dettagliate su come cavi hello tooconnect.
   
    ![Cablare il dispositivo 4U per l'alimentazione](./media/storsimple-ebod-controller-replacement/IC770723.png)
   
    **Figura 4**. Ricollegamento dei cavi
   
   | Etichetta | Descrizione |
   |:--- |:--- |
   | 1 |Enclosure principale |
   | 2 |PCM 0 |
   | 3 |PCM 1 |
   | 4 |Controller 0 |
   | 5 |Controller 1 |
   | 6 |Controller 0 EBOD |
   | 7 |Controller 1 EBOD |
   | 8 |Chassis EBOD |
   | 9 |Unità PDU (Power Distribution Unit) |

## <a name="next-steps"></a>Passaggi successivi
Leggere ulteriori informazioni sulla [Sostituzione dei componenti hardware di StorSimple](storsimple-hardware-component-replacement.md).

