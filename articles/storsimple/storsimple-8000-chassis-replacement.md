---
title: chassis aaaReplace nel dispositivo StorSimple serie 8000 | Documenti Microsoft
description: Viene descritto come tooremove e sostituire hello chassis per l'enclosure principale StorSimple o enclosure EBOD.
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
ms.date: 06/05/2017
ms.author: alkohli
ms.openlocfilehash: 94bbd3d354a9b8866ece036238927e67ec5ce2a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="replace-hello-chassis-on-your-storsimple-device"></a>Sostituzione dello chassis hello nel dispositivo StorSimple
## <a name="overview"></a>Panoramica
In questa esercitazione viene illustrato come tooremove e sostituire uno chassis in un dispositivo StorSimple serie 8000. modello Hello StorSimple 8100 è un dispositivo a enclosure singola (uno chassis), mentre hello 8600 è un dispositivo a doppia enclosure (due chassis). Per un modello 8600, esistono potenzialmente due chassis che potrebbe non riuscire in dispositivo hello: hello chassis per enclosure principale hello o chassis hello hello enclosure EBOD.

In entrambi i casi chassis sostitutivo hello è fornito da Microsoft è vuoto. Non verranno inclusi PCM, moduli controller, unità disco a stato solido (SSD), unità disco rigido (HDD) o moduli EBOD.

> [!IMPORTANT]
> Prima di rimozione e sostituzione dello chassis hello, esaminare le informazioni di sicurezza hello in [sostituzione dei componenti hardware StorSimple](storsimple-8000-hardware-component-replacement.md).


## <a name="remove-hello-chassis"></a>Rimuovere hello chassis
Eseguire hello seguente chassis hello tooremove di passaggi nel dispositivo StorSimple.

#### <a name="tooremove-a-chassis"></a>tooremove uno chassis
1. Verificare che il dispositivo StorSimple hello è spento e scollegato dalla fonte di alimentazione hello.
2. Rimuovere tutti i cavi SAS e rete hello, se applicabile.
3. Rimuovere l'unità di hello dal rack hello.
4. Rimuovere ciascun nome dell'unità hello e prendere nota di slot hello da cui vengono rimossi. Per ulteriori informazioni, vedere [rimuovere l'unità disco hello](storsimple-8000-disk-drive-replacement.md#remove-the-disk-drive).
5. In hello enclosure EBOD (se si tratta di chassis hello non riuscita), rimuovere i moduli controller EBOD di hello. Per ulteriori informazioni, vedere [Rimuovere un controller EBOD](storsimple-8000-ebod-controller-replacement.md#remove-an-ebod-controller).
   
    In hello enclosure principale (se si tratta dello chassis hello non riuscita), rimuovere i controller hello e prendere nota di slot hello da cui vengono rimossi. Per ulteriori informazioni, vedere [Rimuovere un controller](storsimple-8000-controller-replacement.md#remove-a-controller).

## <a name="install-hello-chassis"></a>Installare hello chassis
Eseguire hello seguente chassis hello tooinstall di passaggi nel dispositivo StorSimple.

#### <a name="tooinstall-a-chassis"></a>tooinstall uno chassis
1. Montare su rack hello chassis hello. Per altre informazioni, vedere [Montare su rack il dispositivo StorSimple 8100](storsimple-8100-hardware-installation.md#rack-mount-your-storsimple-8100-device) o [Montare su rack il dispositivo StorSimple 8600](storsimple-8600-hardware-installation.md#rack-mount-your-storsimple-8600-device).
2. Dopo aver hello montato nel rack hello, installare i moduli controller hello nelle hello che stesso posizioni che sono stati installati in precedenza.
3. Installazione hello unità in hello stesso posiziona e slot che sono stati installati in precedenza.
   
   > [!NOTE]
   > È consigliabile installare prima unità SSD hello negli slot hello e quindi installare hello HDD.
  
4. Dispositivo hello montato nel rack hello e installati componenti di hello, connettersi fonti di alimentazione appropriate toohello il dispositivo e accendere il dispositivo hello. Per i dettagli, vedere [Cablare il dispositivo StorSimple 8100](storsimple-8100-hardware-installation.md#cable-your-storsimple-8100-device) o [Cablare il dispositivo StorSimple 8600](storsimple-8600-hardware-installation.md#cable-your-storsimple-8600-device).

## <a name="next-steps"></a>Passaggi successivi
Leggere ulteriori informazioni sulla [Sostituzione dei componenti hardware di StorSimple](storsimple-8000-hardware-component-replacement.md).

