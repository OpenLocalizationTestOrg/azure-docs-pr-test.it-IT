---
title: stato del processo di importazione/esportazione di Azure - v1 aaaReviewing | Documenti Microsoft
description: "Informazioni su come file di log di hello toouse creati quando hello importazione o Esporta processo è stato eseguito il processo di importazione/esportazione di hello stato hello toosee."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: c69d1d69-6403-4eee-9949-0185faeecfa1
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/26/2017
ms.author: muralikk
ms.openlocfilehash: 363731ede4751124a714b4ce96852e0b8c4dbca4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="reviewing-azure-importexport-job-status-with-copy-log-files"></a>Esame dello stato del processo di Importazione/Esportazione di Azure con i file di log di copia
Quando hello servizio importazione/esportazione di Microsoft Azure elabora unità associate a un processo di importazione o esportazione, viene scritta copia log file toohello storage account tooor da cui si importano o esportano i BLOB. file di log Hello contiene lo stato dettagliato di ogni file importato o esportato. file di log di copia di Hello URL tooeach viene restituito quando si esegue una query sullo stato di hello di un processo completato. vedere [recupero del processo](/rest/api/storageservices/Get-Job3) per ulteriori informazioni.  

## <a name="example-urls"></a>URL di esempio

di seguito Hello sono gli URL di esempio per i file di log di copia per un processo di importazione con due unità:  
  
 `http://myaccount.blob.core.windows.net/ImportExportStatesPath/waies/myjob_9WM35C2V_20130921-034307-902_error.xml`  
  
 `http://myaccount.blob.core.windows.net/ImportExportStatesPath/waies/myjob_9WM45A6Q_20130921-042122-021_error.xml`  
  
 Vedere [il servizio di importazione/esportazione il formato di File di Log](../storage-import-export-file-format-log.md) formato hello dei log di copia e l'elenco completo di hello dei codici di stato.  
  
## <a name="next-steps"></a>Passaggi successivi
 
 * [Impostazione hello strumento di importazione/esportazione di Azure](storage-import-export-tool-setup-v1.md)   
 * [Preparing hard drives for an import job](../storage-import-export-tool-preparing-hard-drives-import-v1.md) (Preparazione dei dischi rigidi per un processo di importazione)   
 * [Repairing an import job](../storage-import-export-tool-repairing-an-import-job-v1.md) (Riparazione di un processo di importazione)   
 * [Repairing an export job](../storage-import-export-tool-repairing-an-export-job-v1.md) (Riparazione di un processo di esportazione)   
 * [Risoluzione dei problemi hello strumento di importazione/esportazione di Azure](storage-import-export-tool-troubleshooting-v1.md)
