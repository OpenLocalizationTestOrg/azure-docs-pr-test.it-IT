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
ms.openlocfilehash: 5d2aba510dafd0ca9a10f5643f721e7059a6a8f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="canceling-and-deleting-azure-importexport-jobs"></a>Annullamento ed eliminazione dei processi di Importazione/Esportazione di Azure

È possibile richiedere che un processo annullato prima che sia in hello `Packaging` stato dal chiamante hello [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operazione e impostazione hello `CancelRequested` elemento troppo`true`. il processo di Hello verrà annullato con cadenza principio del best effort. Se le unità sono nel processo di hello di trasferimento dei dati, dati possono continuare toobe trasferiti anche dopo che è stato richiesto l'annullamento.

 Un processo annullato passerà toohello `Completed` stato e verrà conservato per 90 giorni, a quel punto verrà eliminato.

 toodelete un processo, chiamata hello [Elimina processo](/rest/api/storageimportexport/jobs#Jobs_Delete) operazione prima di hello processo venga spedito (*ad esempio*, durante il processo di hello hello `Creating` stato). È anche possibile eliminare un processo in questo caso hello `Completed` stato. Dopo aver eliminato un processo, lo stato e le relative informazioni non saranno più accessibili tramite l'API REST hello o hello portale di Azure.

## <a name="next-steps"></a>Passaggi successivi

* [Tramite l'API REST del servizio importazione/esportazione hello](storage-import-export-using-the-rest-api.md)
