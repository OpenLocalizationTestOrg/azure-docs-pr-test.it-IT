---
title: sostituzione dei componenti hardware serie 8000 aaaStorSimple | Documenti Microsoft
description: "Viene descritto come toosafely sostituire hello PCM, batteria, i moduli controller, controller di EBOD, unità disco e chassis di un dispositivo StorSimple."
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
ms.custom: 
ms.openlocfilehash: 5baca8ff630a1c064cb8bf7e1024b6590f0d6b81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="replace-a-hardware-component-on-your-storsimple-8000-series-device"></a>Sostituire un componente hardware sul dispositivo StorSimple serie 8000

## <a name="overview"></a>Panoramica
esercitazioni di sostituzione componente hardware Hello vengono descritti i componenti hardware hello del Microsoft Azure StorSimple 8000 series dispositivo e hello passaggi necessari tooremove e sostituiscono. In questo articolo vengono descritte le icone di sicurezza hello, vengono forniti i puntatori toohello dettagliate esercitazioni e gli elenchi di hello componenti che possono essere sostituiti.

> [!IMPORTANT]
> Prima di tentare di tooremove o sostituire qualsiasi componente di StorSimple, verificare che hello [convenzioni delle icone di sicurezza](#safety-icon-conventions) e altri [precauzioni di sicurezza](storsimple-safety.md).


### <a name="safety-icon-conventions"></a>Convenzioni di sicurezza
Hello nella tabella seguente descrive le icone di sicurezza hello utilizzati in queste esercitazioni. Prestare particolare attenzione icone toothese quando si attraversano tooremove passaggi hello e sostituiscono i componenti del dispositivo.

| Icona | Text | Informazioni aggiuntive |
|:--- |:--- |:--- |
| ![Icona di avviso](./media/storsimple-hardware-component-replacement/Warning.png) |**PERICOLO!** |Indica una situazione di pericolo che, se non viene evitato, comporterà morte o gravi ferite. Questo segnale è limitato toohello situazioni più estreme. |
| ![Icona di avviso](./media/storsimple-hardware-component-replacement/Warning.png) |**AVVISO!** |Indica una situazione di pericolo che, se non viene evitata, può comportare morte o gravi ferite. |
| ![Icona di attenzione](./media/storsimple-hardware-component-replacement/Caution.png) |**ATTENZIONE!** |Indica una situazione di pericolo che, se non viene evitato, comporterà ferite lievi o limitate. |
| ![Icona di notifica](./media/storsimple-hardware-component-replacement/NoticeIcon.png) |**NOTIFICA:** |Indica le informazioni considerate importanti, ma non correlate al rischio. |
| ![Icona di scossa elettrica](./media/storsimple-hardware-component-replacement/Electric.png) |**Pericolo di scosse elettriche** |Indica alta tensione. |
| ![Icona peso elevato](./media/storsimple-hardware-component-replacement/Weight.png) |**Pesante** | |
| ![Nessuna icona di parti riparabili dall'utente](./media/storsimple-hardware-component-replacement/NoUserServiceableParts.png) |**Nessuna parte riparabile dall'utente** |Non accedere a meno che non si sia stati adeguatamente formati. |
| ![Icona di istruzioni di lettura](./media/storsimple-hardware-component-replacement/ReadInstructions.png) |**Leggere prima tutte le istruzioni** | |
| ![Icona suggerimento di pericolo](./media/storsimple-hardware-component-replacement/TipHazard.png) |**Suggerimento di pericolo** | |

### <a name="before-you-begin"></a>Prima di iniziare
Acquisire familiarità con le informazioni di sicurezza hello le icone di sicurezza e di dispositivi utilizzati in questa esercitazione. Andare troppo[installazione in modo sicuro e il funzionamento del dispositivo StorSimple](storsimple-safety.md) per informazioni complete. Essere certi hello tooreview [precauzioni di sicurezza](storsimple-safety.md#handling-precautions) prima di gestire il dispositivo StorSimple.

Prima di tentare tooreplace un componente, prendere in considerazione le seguenti informazioni hello.

![Icona di avviso](./media/storsimple-hardware-component-replacement/Warning.png)![Icona di scossa elettrica](./media/storsimple-hardware-component-replacement/Electric.png)**AVVISO!**

* Collegarsi a terra correttamente usando un elettrostatica o passepartout antistatiche durante la gestione di moduli e i componenti del dispositivo StorSimple.
* Non toccare nessun circuito. Utilizzare hello fornito maniglie e guide durante la gestione di componenti che possono essere esposto un circuito.

![Warning Icon](./media/storsimple-hardware-component-replacement/Warning.png)![Notice Icon](./media/storsimple-hardware-component-replacement/NoticeIcon.png)**NOTIFICA:**

Quando si sostituisce un modulo, **non lasciare mai vuoto un alloggiamento nella parte posteriore di hello dell'enclosure hello**. Ottenere una sostituzione o un modulo vuoto prima di rimuovere parte difettosa hello.

## <a name="hardware-component-replacement-procedures"></a>Procedure di sostituzione di componenti hardware
Il dispositivo StorSimple serie 8000 è costituito da diversi moduli plug-in hello primario e/o l'enclosure EBOD. Hello 8100 ha una sola enclosure principale, mentre hello 8600 è un dispositivo con enclosure doppia con una enclosure principale e una EBOD.

Hello principali componenti hardware del dispositivo sono riepilogati nella hello le tabelle seguenti. Fare clic sul collegamento hello in hello **la procedura di sostituzione** toohello toogo colonna associata esercitazione.

| Componenti | # Presente | Modulo plug-in? | Procedura di sostituzione |
|:--- |:--- |:--- |:--- |
| Chassis |1 |No |[Sostituzione dello chassis hello nel dispositivo StorSimple](storsimple-8000-chassis-replacement.md) |
| Controller primari |2 |Sì |[Sostituire un modulo controller nel dispositivo StorSimple](storsimple-8000-controller-replacement.md) |
| Power and Cooling Modules (PCM) da 764W |2 |Sì |[Sostituire un PCM sul dispositivo StorSimple](storsimple-8000-power-cooling-module-replacement.md) |
| Batteria di backup |2 |Sì |[Sostituire il modulo batteria di backup hello nel dispositivo StorSimple](storsimple-8000-battery-replacement.md) |
| Unità disco |12 |Sì |[Sostituire un'unità disco del dispositivo StorSimple](storsimple-8000-disk-drive-replacement.md) |

**Tabella 1** enclosure principale hello i componenti Hardware

enclosure principale Hello ed enclosure EBOD hello si differenziano per i propri moduli i/o. Inoltre, hello PCM hanno un wattaggio diverso. Hello PCM nell'enclosure principale hello sono a 764 W, mentre quelli hello enclosure EBOD sono a 580 w. PCM hello in hello primario enclosure includere anche un modulo batteria di backup.

| Componenti | # Presente | Modulo plug-in? | Procedura di sostituzione |
|:--- |:--- |:--- |:--- |
| Chassis |1 |No |[Sostituzione dello chassis hello nel dispositivo StorSimple](storsimple-8000-chassis-replacement.md) |
| Controller EBOD |2 |Sì |[Sostituire un controller EBOD sul dispositivo StorSimple](storsimple-8000-ebod-controller-replacement.md) |
| Power and Cooling Modules (PCM) da 580W |2 |Sì |[Sostituire un PCM sul dispositivo StorSimple](storsimple-8000-power-cooling-module-replacement.md) |
| Unità disco |12 |Sì |[Sostituire un'unità disco del dispositivo StorSimple](storsimple-8000-disk-drive-replacement.md) |

**Tabella 2** i componenti Hardware hello enclosure EBOD

i moduli plug-in Hello nel dispositivo hello vengono evidenziati in hello seguenti diagrammi anteriori e posteriori. È possibile utilizzare questi diagrammi toodetermine hello ha sede hello diversi moduli plug-in se è necessaria una sostituzione. Hello anteriore illustrata hello le unità disco e i diagrammi posteriore hello di hello EBOD hello enclosure principale ed Mostra hello moduli plug-in.

![Piano anteriore del dispositivo con unità disco](./media/storsimple-hardware-component-replacement/IC741028.png)

**Figura 1** parte anteriore del dispositivo hello

| Etichetta | Description |
|:--- |:--- |
| 0 - 11 |Unità di dischi (totale pari a 12) |

Le enclosure principale hello e hello EBOD estraibili delle unità. chassis di Hello alloggia 12 unità disco 3,5" disposte in un formato 3 x 4.

![Backplane dei moduli dello chassis principale del dispositivo](./media/storsimple-hardware-component-replacement/IC740994.png)

**Figura 2** parte posteriore dell'enclosure principale hello

| Etichetta | Descrizione |
|:--- |:--- |
| 1 |PCM 0 |
| 2 |PCM 1 |
| 3 |Controller 0 |
| 4 |Controller 1 |

![Piano posteriore dei moduli plug-in dell'enclosure EBOD del dispositivo](./media/storsimple-hardware-component-replacement/IC769599.png)

**Figura 3** parte posteriore dell'enclosure EBOD hello

| Etichetta | Descrizione |
|:--- |:--- |
| 1 |PCM 0 |
| 2 |PCM 1 |
| 3 |Controller 0 EBOD |
| 4 |Controller 1 EBOD |

## <a name="field-replaceable-units"></a>Unità sostituibile sul campo 
Hello seguenti unità sostituibili sul campo (FRU) sono disponibile per il dispositivo StorSimple:

* Chassis (incluso pannello operativo integrato hello)
* PCM con AC da 764 W
* PCM con AC da 580 W
* Unità disco rigido con modulo unità carrier
* Modulo controller
* Modulo controller EBOD
* Modulo batteria di backup
* Kit per il montaggio su rack

. [Contattare il supporto Microsoft](storsimple-8000-contact-microsoft-support.md) tooorder una di queste unità sostitutive.

## <a name="next-steps"></a>Passaggi successivi
Rivedere tutte [informazioni sulla sicurezza](storsimple-safety.md) prima di tentare di tooreplace un componente hardware di StorSimple.

