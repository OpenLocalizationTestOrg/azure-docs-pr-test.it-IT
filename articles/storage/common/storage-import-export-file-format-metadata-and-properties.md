---
title: "formato file metadati e proprietà aaaAzure importazione/esportazione | Documenti Microsoft"
description: "Informazioni su come toospecify metadati e le proprietà per uno o più blob che fanno parte di un'importazione o esportazione di processo."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 840364c6-d9a8-4b43-a9f3-f7441c625069
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: bb13c1f1a27baea77298cb224970cd521d02d8c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-importexport-service-metadata-and-properties-file-format"></a>Formato di file dei metadati e delle proprietà di Importazione/Esportazione di Azure
È possibile specificare i metadati e le proprietà per uno o più BLOB nell'ambito di un processo di importazione o esportazione. tooset metadati o proprietà per il BLOB viene creato come parte di un processo di importazione, fornire un file di metadati o delle proprietà nel disco rigido hello contenente hello toobe di dati importati. Per un processo di esportazione, proprietà e i metadati vengono scritti tooa file di metadati o delle proprietà che è incluso nel disco rigido hello restituito tooyou.  
  
## <a name="metadata-file-format"></a>Formato del file di metadati  
formato Hello di un file di metadati è il seguente:  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Metadata>  
[<metadata-name-1>metadata-value-1</metadata-name-1>]  
[<metadata-name-2>metadata-value-2</metadata-name-2>]  
. . .  
</Metadata>  
```
  
|Elemento XML|Tipo|Descrizione|  
|-----------------|----------|-----------------|  
|`Metadata`|Elemento radice|elemento radice di Hello hello del file di metadati.|  
|`metadata-name`|String|Facoltativo. elemento XML Hello specifica il nome di hello di hello metadati per il blob hello e il relativo valore specifica il valore di hello dell'impostazione dei metadati hello.|  
  
## <a name="properties-file-format"></a>Formato del file delle proprietà  
formato Hello di un file di proprietà è il seguente:  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Properties>  
[<Last-Modified>date-time-value</Last-Modified>]  
[<Etag>etag</Etag>]  
[<Content-Length>size-in-bytes<Content-Length>]  
[<Content-Type>content-type</Content-Type>]  
[<Content-MD5>content-md5</Content-MD5>]  
[<Content-Encoding>content-encoding</Content-Encoding>]  
[<Content-Language>content-language</Content-Language>]  
[<Cache-Control>cache-control</Cache-Control>]  
</Properties>  
```
  
|Elemento XML|Tipo|Descrizione|  
|-----------------|----------|-----------------|  
|`Properties`|Elemento radice|elemento radice di Hello del file delle proprietà hello.|  
|`Last-Modified`|String|Facoltativo. ora ultima modifica Hello per blob hello. Solo per i processi di esportazione.|  
|`Etag`|String|Facoltativo. Hello valore ETag del blob. Solo per i processi di esportazione.|  
|`Content-Length`|String|Facoltativo. dimensioni di Hello di hello blob in byte. Solo per i processi di esportazione.|  
|`Content-Type`|String|Facoltativo. tipo di contenuto Hello del blob hello.|  
|`Content-MD5`|String|Facoltativo. Hello hash MD5 del blob.|  
|`Content-Encoding`|String|Facoltativo. contenuto del blob Hello codifica.|  
|`Content-Language`|String|Facoltativo. Hello linguaggio del contenuto del blob.|  
|`Cache-Control`|String|Facoltativo. stringa di controllo della cache Hello per blob hello.|  

## <a name="next-steps"></a>Passaggi successivi

Per le regole dettagliate sull'impostazione dei metadati e delle proprietà di un BLOB, vedere [Set blob properties](/rest/api/storageservices/set-blob-properties) (Impostare le proprietà di un BLOB), [Set Blob Metadata](/rest/api/storageservices/set-blob-metadata) (Impostare i metadati di un BLOB) e [Setting and retrieving properties and metadata for blob resources](/rest/api/storageservices/setting-and-retrieving-properties-and-metadata-for-blob-resources) (Impostazione e recupero di proprietà e metadati per le risorse BLOB).
