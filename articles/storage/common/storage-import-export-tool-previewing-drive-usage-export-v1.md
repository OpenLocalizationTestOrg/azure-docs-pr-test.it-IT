---
title: "utilizzo dell'unità di aaaPreviewing per un processo di esportazione di importazione/esportazione di Azure - v1 | Documenti Microsoft"
description: "Informazioni su come elenco hello toopreview di BLOB è stato selezionato per un processo di esportazione nel servizio di importazione/esportazione di Azure hello."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 7707d744-7ec7-4de8-ac9b-93a18608dc9a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: 7378c159f6d11702cda9ae7654e84d85f9b671b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="previewing-drive-usage-for-an-export-job"></a>Anteprima dell'uso del disco per un processo di esportazione
Prima di creare un processo di esportazione, è necessario esportata un set di BLOB toobe toochoose. servizio di importazione/esportazione di Microsoft Azure Hello consente toouse un elenco di percorsi blob o blob prefissi BLOB hello toorepresent selezionata.  
  
Successivamente, è necessario toodetermine il numero di unità è necessario toosend. Strumento di importazione/esportazione Hello fornisce hello `PreviewExport` sintassi del comando toopreview unità per i BLOB hello è selezionata, in base alle dimensioni di hello di hello unità verrà toouse.

## <a name="command-line-parameters"></a>Parametri della riga di comando

È possibile utilizzare i seguenti parametri quando si utilizza hello hello `PreviewExport` comando di hello strumento di importazione/esportazione.

|Parametro della riga di comando|Descrizione|  
|--------------------------|-----------------|  
|**/logdir:**&lt;DirectoryLog\>|Facoltativo. directory dei log Hello. File di log dettagliati verranno scritti toothis directory. Se non viene specificata alcuna directory di log, la directory corrente hello da utilizzare come directory dei log hello.|  
|**/sn:**<NomeAccountArchiviazione\>|Obbligatorio. processo di esportazione nome Hello hello dell'account di archiviazione per hello.|  
|**/sk:**&lt;ChiaveAccountArchiviazione\>|Obbligatorio solo se non è specificata una firma di accesso condiviso del contenitore. processo di esportazione chiave Hello per l'account di archiviazione hello per hello.|  
|**/csas:**&lt;ContainerSas\>|Obbligatorio solo se non è specificata una chiave dell'account di archiviazione. il contenitore di Hello SAS per elenco hello BLOB toobe esportati nel processo di esportazione hello.|  
|**/ExportBlobListFile:**&lt;FileElencoBlobEsportazione\>|Obbligatorio. Toohello percorso XML del file contenente l'elenco dei percorsi blob o prefissi di percorso per toobe BLOB hello esportata blob. formato di file Hello usato in hello `BlobListBlobPath` elemento hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operazione di hello API REST del servizio importazione/esportazione.|  
|**/DriveSize:**&lt;DimensioneUnità\>|Obbligatorio. dimensioni dell'unità toouse per un processo di esportazione, Hello *ad esempio*, 500 GB o 1,5 TB.|  

## <a name="command-line-example"></a>Esempio di riga di comando

esempio Hello illustra hello `PreviewExport` comando:  
  
```  
WAImportExport.exe PreviewExport /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /ExportBlobListFile:C:\WAImportExport\mybloblist.xml /DriveSize:500GB    
```  
  
Hello blob elenco file di esportazione può contenere nomi blob e prefissi blob, come illustrato di seguito:  
  
```xml 
<?xml version="1.0" encoding="utf-8"?>  
<BlobList>  
<BlobPath>pictures/animals/koala.jpg</BlobPath>  
<BlobPathPrefix>/vhds/</BlobPathPrefix>  
<BlobPathPrefix>/movies/</BlobPathPrefix>  
</BlobList>  
```

Hello strumento di importazione/esportazione di Azure Elenca tutti i BLOB toobe esportato e calcola come toopack in unità di hello specificato di dimensioni, prendendo in considerazione l'eventuale overhead necessario, quindi stima il numero di hello di unità necessarie BLOB hello toohold e utilizzo dell'unità informazioni.  
  
Di seguito è riportato un esempio di output di hello, senza log informativi:  
  
```  
Number of unique blob paths/prefixes:   3  
Number of duplicate blob paths/prefixes:        0  
Number of nonexistent blob paths/prefixes:      1  
  
Drive size:     500.00 GB  
Number of blobs that can be exported:   6  
Number of blobs that cannot be exported:        2  
Number of drives needed:        3  
        Drive #1:       blobs = 1, occupied space = 454.74 GB  
        Drive #2:       blobs = 3, occupied space = 441.37 GB  
        Drive #3:       blobs = 2, occupied space = 131.28 GB    
```  
  
## <a name="next-steps"></a>Passaggi successivi

* [Azure Import/Export Tool Reference](../storage-import-export-tool-how-to-v1.md) (Informazioni di riferimento sullo strumento Importazione/Esportazione di Azure)
