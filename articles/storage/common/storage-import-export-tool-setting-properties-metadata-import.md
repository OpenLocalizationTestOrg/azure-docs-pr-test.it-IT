---
title: "aaaSetting proprietà e i metadati utilizzando Importazione/esportazione di Azure | Documenti Microsoft"
description: "Informazioni su come imposta toospecify toobe di proprietà e metadati per il BLOB di destinazione hello durante l'esecuzione di hello strumento di importazione/esportazione di Azure tooprepare le unità."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: c763237160f0e4b72ce88fd31e2958994bfe8e50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="setting-properties-and-metadata-during-hello-import-process"></a>Impostazione delle proprietà e metadati hello durante il processo di importazione

Quando si eseguono hello dello strumento di importazione/esportazione di Microsoft Azure tooprepare le unità, è possibile specificare le proprietà e metadati toobe impostato per il BLOB di destinazione hello. A tale scopo, seguire questa procedura:

1.  proprietà blob tooset, creare un file di testo nel computer locale che specifica i nomi delle proprietà e valori.
2.  tooset i metadati del blob, creare un file di testo nel computer locale che specifica i nomi dei metadati e i valori.
3.  Passare tooone percorso completo di hello o entrambi questi toohello file dello strumento di importazione/esportazione di Azure come parte di hello `PrepImport` operazione.

> [!NOTE]
>  Quando si specifica un file di proprietà o di metadati durante una sessione di copia, tali proprietà o metadati vengono impostati per ogni BLOB importato durante tale sessione di copia. Se si desidera toospecify un diverso set di proprietà o metadati per alcuni BLOB hello importati, è necessario toocreate separato copiare sessione con proprietà diverse o file di metadati.

## <a name="specify-blob-properties-in-a-text-file"></a>Specificare le proprietà dei BLOB in un file di testo

proprietà blob toospecify, creare un file di testo locale e includere il XML che specifica i nomi delle proprietà come elementi e i valori delle proprietà come valori. Ecco un esempio che specifica alcuni valori delle proprietà:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Properties>
    <Content-Type>application/octet-stream</Content-Type>
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>
    <Cache-Control>no-cache</Cache-Control>
</Properties>
```

Salvare hello tooa locale percorso del file come `C:\WAImportExport\ImportProperties.txt`.

## <a name="specify-blob-metadata-in-a-text-file"></a>Specificare i metadati dei BLOB in un file di testo

Analogamente, toospecify i metadati del blob, creare un file di testo locale che specifica i nomi dei metadati come elementi e i valori dei metadati come valori. Ecco un esempio che specifica alcuni valori dei metadati:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Metadata>
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>
    <DataSetName>SampleData</DataSetName>
    <CreationDate>10/1/2013</CreationDate>
</Metadata>
```

Salvare hello tooa locale percorso del file come `C:\WAImportExport\ImportMetadata.txt`.

## <a name="add-hello-path-tooproperties-and-metadata-files-in-datasetcsv"></a>Aggiungere i file di metadati e tooproperties percorso hello in dataset.csv

```
BasePath,DstBlobPathOrPrefix,BlobType,Disposition,MetadataFile,PropertiesFile
H:\Video\,https://mystorageaccount.blob.core.windows.net/video/,BlockBlob,rename,None,H:\mydirectory\properties.xml
H:\Photo\,https://mystorageaccount.blob.core.windows.net/photo/,BlockBlob,rename,None,H:\mydirectory\properties.xml
K:\Temp\FavoriteVideo.ISO,https://mystorageaccount.blob.core.windows.net/favorite/FavoriteVideo.ISO,BlockBlob,rename,None,H:\mydirectory\properties.xml
\\myshare\john\music\,https://mystorageaccount.blob.core.windows.net/music/,BlockBlob,rename,None,H:\mydirectory\properties.xml
```

## <a name="next-steps"></a>Passaggi successivi

* [Import/Export service metadata and properties file format](../storage-import-export-file-format-metadata-and-properties.md) (Formato dei file di metadati e delle proprietà del servizio Importazione/Esportazione)
