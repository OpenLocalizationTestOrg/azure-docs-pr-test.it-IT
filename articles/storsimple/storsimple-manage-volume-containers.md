---
title: aaaManage ai contenitori dei volumi StorSimple | Documenti Microsoft
description: Viene illustrato come utilizzare hello StorSimple Manager contenitori dei volumi servizio pagina tooadd, modificare o eliminare un contenitore del volume.
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 1c64ce75-1fd3-4d3b-9304-d4dc0fc2b069
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/24/2016
ms.author: v-sharos
ms.openlocfilehash: 9b29536e0072306e53ac92bacca78a13d932c2b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-storsimple-volume-containers"></a>Usare i contenitori di volumi StorSimple toomanage servizio StorSimple Manager hello
## <a name="overview"></a>Panoramica
In questa esercitazione viene illustrato come toouse hello toocreate servizio StorSimple Manager e gestire i contenitori di volumi StorSimple.

Un contenitore del volume in un dispositivo StorSimple di Microsoft Azure contiene uno o più volumi che condividono l'account di archiviazione, la crittografia e le impostazioni del consumo di larghezza di banda. Un dispositivo può avere più contenitori del volume per tutti i volumi. 

Un contenitore di volumi sono hello gli attributi seguenti:

* **Volumi** : hello a livelli o aggiunto in locale i volumi StorSimple di cui sono contenuti all'interno del contenitore di volume hello. Un contenitore del volume può contenere i volumi StorSimple too256.
* **Crittografia** : una chiave di crittografia che può essere definita per ogni contenitore del volume. Questa chiave viene usata per crittografare i dati di hello inviata da cloud toohello dispositivo StorSimple. Una chiave di livello militare AES a 256 bit viene utilizzata con la chiave immessa dall'utente hello. toosecure dei dati, è consigliabile abilitare sempre la crittografia dell'archiviazione cloud.
* **Account di archiviazione** : hello account di archiviazione di provider di servizi di archiviazione cloud tooyour collegato. Tutti i volumi di hello che risiedono in un contenitore di volumi condividono questo account di archiviazione. È possibile scegliere un account di archiviazione da un elenco esistente o creare un nuovo account quando si crea il contenitore di volumi hello e quindi specificare le credenziali di accesso hello per tale account.
* **Larghezza di banda cloud** : hello della larghezza di banda usata dal dispositivo hello per hello dati dal dispositivo hello inviati toohello cloud. È possibile applicare un controllo della larghezza di banda specificando un valore compreso tra 1 e 1000 Mbps quando si definisce questo contenitore. Se si desidera hello dispositivo tooconsume tutti disponibile della larghezza di banda, impostare tooUnlimited questo campo. È anche possibile creare e applicare una larghezza di banda modello tooallocate della larghezza di banda basato su pianificazione.

![Andare alla pagina Contenitori di volumi.](./media/storsimple-manage-volume-containers/HCS_VolumeContainersPage.png)

Procedure riportate di seguito viene illustrato come toouse hello StorSimple **contenitori di volumi** hello toocomplete pagina operazioni comuni seguenti:

* Aggiungere un contenitore di volumi 
* Modificare un contenitore di volumi 
* Eliminare un contenitore di volumi 

## <a name="add-a-volume-container"></a>Aggiungere un contenitore di volumi
Eseguire hello seguendo i passaggi tooadd un contenitore del volume.

[!INCLUDE [storsimple-add-volume-container](../../includes/storsimple-add-volume-container.md)]

## <a name="modify-a-volume-container"></a>Modificare un contenitore di volumi
Eseguire hello seguendo i passaggi toomodify un contenitore del volume.

[!INCLUDE [storsimple-modify-volume-container](../../includes/storsimple-modify-volume-container.md)]

## <a name="delete-a-volume-container"></a>Eliminare un contenitore di volumi
Un contenitore del volume ha volumi all'interno di esso. Può essere eliminato solo se tutti i volumi di hello in esso contenuti sono stati eliminati. Eseguire hello seguendo i passaggi toodelete un contenitore del volume.

[!INCLUDE [storsimple-delete-volume-container](../../includes/storsimple-delete-volume-container.md)]

## <a name="next-steps"></a>Passaggi successivi
* Ulteriori informazioni sulla [gestione di volumi StorSimple](storsimple-manage-volumes.md). 
* Altre informazioni, vedere [utilizzando hello tooadminister servizio StorSimple Manager dispositivo StorSimple](storsimple-manager-service-administration.md).

