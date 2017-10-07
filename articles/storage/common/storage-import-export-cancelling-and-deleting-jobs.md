---
title: aaaCancel ed eliminare un processo di importazione/esportazione di Azure | Documenti Microsoft
description: Informazioni su come toocancel ed eliminare i processi per hello servizio importazione/esportazione di Microsoft Azure.
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: fd3d66f0-1dbb-4c75-9223-307d5abaeefc
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 13456a8e7652850baacb53730cc7bb1520b0a4c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="canceling-and-deleting-azure-importexport-jobs"></a>Annullamento ed eliminazione dei processi di Importazione/Esportazione di Azure

 toorequest che un processo annullato prima che si trova in hello `Packaging` stato, chiamata hello [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operazione e set hello `CancelRequested` elemento troppo`true`. Hello processi vengono annullati su base principio del best effort. Se le unità sono nel processo di hello di trasferimento dei dati, dati possono continuare toobe trasferiti anche dopo che è stato richiesto l'annullamento.

 Un processo annullato viene spostata toohello `Completed` stato e vengono mantenuti per 90 giorni, a quel punto viene eliminato.

 toodelete un processo, chiamata hello [Elimina processo](/rest/api/storageimportexport/jobs#Jobs_Delete) operazione prima di hello processo venga spedito (vale a dire, durante il processo di hello hello `Creating` stato). È anche possibile eliminare un processo in questo caso hello `Completed` stato. Dopo l'eliminazione di un processo, lo stato e le relative informazioni non saranno più accessibili tramite l'API REST hello o hello portale di Azure.

## <a name="next-steps"></a>Passaggi successivi

* [Tramite l'API REST del servizio importazione/esportazione hello](storage-import-export-using-the-rest-api.md)
