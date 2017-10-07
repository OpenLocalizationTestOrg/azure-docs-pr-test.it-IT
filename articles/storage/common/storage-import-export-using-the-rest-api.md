---
title: hello aaaUsing API REST del servizio importazione/esportazione di Azure | Documenti Microsoft
description: Informazioni su dove del servizio API REST, inclusi entrambi materiale di riferimento come tooand toofind risorse per l'utilizzo di hello importazione/esportazione di Azure.
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 233f80e9-2e7f-48e0-9639-5c7785e7d743
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: fc7e1007ad632cf6f771c2545644f8de43c8f181
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-importexport-service-rest-api"></a>Tramite l'API REST del servizio importazione/esportazione di Azure hello

Hello servizio importazione/esportazione di Microsoft Azure espone un controllo a livello di codice tooenable di API REST dei processi di importazione/esportazione. È possibile utilizzare l'API REST di hello tooperform tutti hello importazione/esportazione di operazioni che è possibile eseguire con hello [portale di Azure](https://portal.azure.com/). Inoltre, è possibile utilizzare hello API REST tooperform determinate operazioni granulari, ad esempio l'esecuzione di query hello percentuale di completamento di un processo, che non è attualmente disponibile nel portale di Azure classico hello.

Vedere [tramite servizio di importazione/esportazione di Microsoft Azure hello, dati tooTransfer tooBlob archiviazione](../storage-import-export-service.md) per una panoramica del servizio di importazione/esportazione hello e un'esercitazione che illustra come toouse hello toocreate portale classico e gestire l'importazione e i processi di esportazione.

## <a name="service-endpoints"></a>Endpoint di servizio

Hello servizio importazione/esportazione di Azure è un provider di risorse per Gestione risorse di Azure e fornisce un set di API REST a hello endpoint HTTPS per la gestione dei processi di importazione/esportazione seguenti:

```
https://management.azure.com/subscriptions/<subscription-id>/resourceGroups/<resource-group>/providers/Microsoft.ImportExport/jobs/<job-name>
```

## <a name="versioning"></a>Controllo delle versioni

Le richieste di servizio di importazione/esportazione toohello deve specificare hello `api-version` parametro e impostarne il valore troppo`2016-11-01`.

## <a name="importexport-service-operations"></a>Operazioni del servizio Importazione/Esportazione

[Creating an import job](../storage-import-export-creating-an-import-job.md) (Creazione di un processo di importazione)

[Creazione di un processo di esportazione](../storage-import-export-creating-an-export-job.md)

[Retrieving state information for a job](storage-import-export-retrieving-state-info-for-a-job.md) (Recupero delle informazioni sullo stato per un processo)

[Enumerazione dei processi](../storage-import-export-enumerating-jobs.md)

[Cancelling and deleting jobs](storage-import-export-cancelling-and-deleting-jobs.md) (Annullamento ed eliminazione dei processi)

[Backup dei manifesti delle unità](../storage-import-export-backing-up-drive-manifests.md)

[Diagnostica e ripristino dagli errori per i processi di Importazione/Esportazione](../storage-import-export-diagnostics-and-error-recovery.md)

## <a name="next-steps"></a>Passaggi successivi

* [REST di importazione/esportazione dell'archiviazione](/rest/api/storageimportexport)
