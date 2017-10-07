---
title: processo di importazione aaaSample del flusso di lavoro tooprep dischi rigidi per un'importazione/esportazione di Azure | Documenti Microsoft
description: "Una procedura dettagliata per il processo completo di hello la preparazione dell'unità per un processo di importazione in hello servizio importazione/esportazione di Azure, vedere."
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
ms.date: 04/07/2017
ms.author: muralikk
ms.openlocfilehash: fa7f36300b35b81757523de4960fd583bd4bf305
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="sample-workflow-tooprepare-hard-drives-for-an-import-job"></a>Unità disco rigido tooprepare del flusso di lavoro di esempio per un processo di importazione

In questo articolo illustra hello processo completo di preparazione delle unità per un processo di importazione.

## <a name="sample-data"></a>Dati di esempio

Questo esempio vengono importati dati seguenti in un account di archiviazione di Azure denominato hello `mystorageaccount`:

|Percorso|Descrizione|Dimensioni dei dati|
|--------------|-----------------|-----|
|H:\Video\ |Una raccolta di video|12 TB|
|H:\Photo\ |Una raccolta di foto|30 GB|
|K:\Temp\FavoriteMovie.ISO|Un'immagine di disco Blu-ray™|25 GB|
|\\\bigshare\john\music\|Una raccolta di file musicali in una condivisione di rete|10 GB|

## <a name="storage-account-destinations"></a>Destinazioni degli account di archiviazione

il processo di importazione Hello verrà importati i dati di hello in seguito le destinazioni nell'account di archiviazione hello hello:

|Sorgente|BLOB o directory virtuale di destinazione|
|------------|-------------------------------------------|
|H:\Video\ |video/|
|H:\Photo\ |photo/|
|K:\Temp\FavoriteMovie.ISO|favorite/FavoriteMovies.ISO|
|\\\bigshare\john\music\ |music|

Con questo mapping, hello file `H:\Video\Drama\GreatMovie.mov` sarà blob importati toohello `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.

## <a name="determine-hard-drive-requirements"></a>Determinare i requisiti del disco rigido

Successivamente, toodetermine il numero di dischi rigido necessari, calcolo hello dimensioni dei dati hello:

`12TB + 30GB + 25GB + 10GB = 12TB + 65GB`

Per questo esempio, dovrebbero essere sufficienti due dischi rigidi da 8 TB. Tuttavia, poiché la directory di origine hello `H:\Video` include 12TB di dati e la capacità del disco rigido singolo è solo 8TB, si sarà in grado di toospecify in hello seguenti modalità di hello **driveset.csv** file:

```
DriveLetter,FormatOption,SilentOrPromptOnFormat,Encryption,ExistingBitLockerKey
X,Format,SilentMode,Encrypt,
Y,Format,SilentMode,Encrypt,
```
strumento Hello distribuirà dati tra due dischi rigidi in modo ottimizzato.

## <a name="attach-drives-and-configure-hello-job"></a>Collegare l'unità e configurare il processo di hello
Verrà collegare entrambi macchina toohello dischi e volumi creati. Creare quindi il file **dataset.csv**:
```
BasePath,DstBlobPathOrPrefix,BlobType,Disposition,MetadataFile,PropertiesFile
H:\Video\,video/,BlockBlob,rename,None,H:\mydirectory\properties.xml
H:\Photo\,photo/,BlockBlob,rename,None,H:\mydirectory\properties.xml
K:\Temp\FavoriteVideo.ISO,favorite/FavoriteVideo.ISO,BlockBlob,rename,None,H:\mydirectory\properties.xml
\\myshare\john\music\,music/,BlockBlob,rename,None,H:\mydirectory\properties.xml
```

Inoltre, è possibile impostare hello i metadati per tutti i file seguenti:

* **UploadMethod:** servizio Importazione/Esportazione di Windows Azure
* **DataSetName:** SampleData
* **CreationDate:** 10/1/2013

tooset metadati per i file hello importato, creare un file di testo, `c:\WAImportExport\SampleMetadata.txt`, con hello seguente contenuto:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Metadata>
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>
    <DataSetName>SampleData</DataSetName>
    <CreationDate>10/1/2013</CreationDate>
</Metadata>
```

È inoltre possibile impostare alcune proprietà per hello `FavoriteMovie.ISO` blob:

* **Content-Type:** application/octet-stream
* **Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ==
* **Cache-Control:** no-cache

tooset queste proprietà, creare un file di testo, `c:\WAImportExport\SampleProperties.txt`:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Properties>
    <Content-Type>application/octet-stream</Content-Type>
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>
    <Cache-Control>no-cache</Cache-Control>
</Properties>
```

## <a name="run-hello-azure-importexport-tool-waimportexportexe"></a>Hello esecuzione dello strumento di importazione/esportazione di Azure (WAImportExport.exe)

Si è ora pronto toorun hello strumento di importazione/esportazione di Azure tooprepare hello due unità disco rigido.

**Per la prima sessione hello:**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#1  /sk:************* /InitialDriveSet:driveset-1.csv /DataSet:dataset-1.csv /logdir:F:\logs
```

Se tutti i dati più devono toobe aggiunto, creare un altro file di set di dati (stesso formato Initialdataset).

**Per una seconda sessione hello:**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2  /DataSet:dataset-2.csv
```

Dopo aver completato le sessioni di copia hello, è possibile disconnettere hello due unità dal computer di hello copia e spedirle toohello data center Azure appropriato. Carica file journal hello due, `<FirstDriveSerialNumber>.xml` e `<SecondDriveSerialNumber>.xml`, quando si crea il processo di importazione hello in hello portale di Azure.

## <a name="next-steps"></a>Passaggi successivi

* [Preparing hard drives for an import job](../storage-import-export-tool-preparing-hard-drives-import.md) (Preparazione dei dischi rigidi per un processo di importazione)
* [Quick reference for frequently used commands](../storage-import-export-tool-quick-reference.md) (Riferimento rapido per i comandi usati più di frequente)
