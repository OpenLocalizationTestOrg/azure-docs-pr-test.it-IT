---
title: aaaManage ai contenitori dei volumi StorSimple nel dispositivo serie StorSimple 8000 hello | Documenti Microsoft
description: Viene illustrato come usare hello gestione di dispositivi StorSimple contenitori dei volumi servizio pagina tooadd, modificare o eliminare un contenitore del volume.
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/19/2017
ms.author: alkohli
ms.openlocfilehash: 7374d4ab9aecd6280ae1d93a29f17d12d28c9362
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-storsimple-volume-containers"></a>Utilizzare i contenitori dei volumi StorSimple servizio toomanage hello dispositivo StorSimple Manager

## <a name="overview"></a>Panoramica
In questa esercitazione viene illustrato come toouse hello toocreate servizio di gestione di dispositivi StorSimple e gestire i contenitori di volumi StorSimple.

Un contenitore del volume in un dispositivo StorSimple di Microsoft Azure contiene uno o più volumi che condividono l'account di archiviazione, la crittografia e le impostazioni del consumo di larghezza di banda. Un dispositivo può avere più contenitori del volume per tutti i volumi. 

Un contenitore di volumi sono hello gli attributi seguenti:

* **Volumi** : hello a livelli o aggiunto in locale i volumi StorSimple di cui sono contenuti all'interno del contenitore di volume hello. 
* **Crittografia** : una chiave di crittografia che può essere definita per ogni contenitore del volume. Questa chiave viene usata per crittografare i dati di hello inviata da cloud toohello dispositivo StorSimple. Una chiave di livello militare AES a 256 bit viene utilizzata con la chiave immessa dall'utente hello. toosecure dei dati, è consigliabile abilitare sempre la crittografia dell'archiviazione cloud.
* **Account di archiviazione** : hello account di archiviazione Azure che sono utilizzati toostore hello dati. Tutti i volumi di hello che risiedono in un contenitore di volumi condividono questo account di archiviazione. È possibile scegliere un account di archiviazione da un elenco esistente o creare un nuovo account quando si crea il contenitore di volumi hello e quindi specificare le credenziali di accesso hello per tale account.
* **Larghezza di banda cloud** : hello della larghezza di banda usata dal dispositivo hello per hello dati dal dispositivo hello inviati toohello cloud. È possibile applicare un controllo della larghezza di banda specificando un valore compreso tra 1 e 1.000 Mbps quando si crea questo contenitore. Se si desidera hello dispositivo tooconsume tutti disponibile della larghezza di banda, impostare questo campo troppo**Unlimited**. È anche possibile creare e applicare una larghezza di banda modello tooallocate della larghezza di banda basato su pianificazione.

Hello procedure seguenti illustrano come toouse hello StorSimple **contenitori di volumi** hello toocomplete pannello operazioni comuni seguenti:

* Aggiungere un contenitore di volumi
* Modificare un contenitore di volumi
* Eliminare un contenitore di volumi

## <a name="add-a-volume-container"></a>Aggiungere un contenitore di volumi
Eseguire hello seguendo i passaggi tooadd un contenitore del volume.

[!INCLUDE [storsimple-8000-add-volume-container](../../includes/storsimple-8000-create-volume-container.md)]

## <a name="modify-a-volume-container"></a>Modificare un contenitore di volumi
Eseguire hello seguendo i passaggi toomodify un contenitore del volume.

[!INCLUDE [storsimple-8000-modify-volume-container](../../includes/storsimple-8000-modify-volume-container.md)]

## <a name="delete-a-volume-container"></a>Eliminare un contenitore di volumi
Un contenitore del volume ha volumi all'interno di esso. Può essere eliminato solo se tutti i volumi di hello in esso contenuti sono stati eliminati. Eseguire hello seguendo i passaggi toodelete un contenitore del volume.

[!INCLUDE [storsimple-8000-delete-volume-container](../../includes/storsimple-8000-delete-volume-container.md)]

## <a name="next-steps"></a>Passaggi successivi
* Ulteriori informazioni sulla [gestione di volumi StorSimple](storsimple-8000-manage-volumes-u2.md). 
* Altre informazioni, vedere [utilizzando hello tooadminister servizio di gestione di dispositivi StorSimple dispositivo StorSimple](storsimple-8000-manager-service-administration.md).

