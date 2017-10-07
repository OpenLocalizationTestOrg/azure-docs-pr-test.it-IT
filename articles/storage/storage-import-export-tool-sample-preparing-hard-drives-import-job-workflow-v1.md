---
title: processo - v1 di importazione aaaSample del flusso di lavoro tooprep dischi rigidi per un'importazione/esportazione di Azure | Documenti Microsoft
description: "Una procedura dettagliata per il processo completo di hello la preparazione dell'unità per un processo di importazione in hello servizio importazione/esportazione di Azure, vedere."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 6eb1b1b7-c69f-4365-b5ef-3cd5e05eb72a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: f836fc6104d8b4ad5660cb110a62f61b40b0b7ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="sample-workflow-tooprepare-hard-drives-for-an-import-job"></a>Unità disco rigido tooprepare del flusso di lavoro di esempio per un processo di importazione
In questo argomento illustra hello processo completo di preparazione delle unità per un processo di importazione.  
  
Questo esempio vengono importati dati seguenti in un account di archiviazione Windows Azure denominato hello `mystorageaccount`:  
  
|Percorso|Descrizione|  
|--------------|-----------------|  
|H:\Video|Una raccolta di video, 5 TB in totale.|  
|H:\Photo|Una raccolta di foto, 30 GB in totale.|  
|K:\Temp\FavoriteMovie.ISO|Un'immagine di disco Blu-ray™, 25 GB.|  
|\\\bigshare\john\music|Una raccolta di file musicali in una condivisione di rete, 10 GB in totale.|  
  
Questi dati verrà importati il processo di importazione Hello in seguito le destinazioni nell'account di archiviazione hello hello:  
  
|Sorgente|BLOB o directory virtuale di destinazione|  
|------------|-------------------------------------------|  
|H:\Video|https://mystorageaccount.blob.core.windows.net/video|  
|H:\Photo|https://mystorageaccount.blob.core.windows.net/photo|  
|K:\Temp\FavoriteMovie.ISO|https://mystorageaccount.blob.core.windows.net/favorite/FavoriteMovies.ISO|  
|\\\bigshare\john\music|https://mystorageaccount.blob.core.windows.net/music|  
  
Con questo mapping, hello file `H:\Video\Drama\GreatMovie.mov` sarà blob importati toohello `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.  
  
Successivamente, toodetermine il numero di dischi rigido necessari, calcolo hello dimensioni dei dati hello:  
  
`5TB + 30GB + 25GB + 10GB = 5TB + 65GB`  
  
Per questo esempio, dovrebbero essere sufficienti due dischi rigidi da 3 TB. Tuttavia, poiché la directory di origine hello `H:\Video` include 5TB di dati e la capacità del disco rigido è di soli 3TB, è necessario toobreak `H:\Video` in due directory di dimensioni minori prima di eseguire lo strumento di importazione/esportazione di Microsoft Azure di hello: `H:\Video1` e `H:\Video2`. Questo passaggio vengono generate hello seguenti directory di origine:  
  
|Percorso|Dimensione|BLOB o directory virtuale di destinazione|  
|--------------|----------|-------------------------------------------|  
|H:\Video1|2,5 TB|https://mystorageaccount.blob.core.windows.net/video|  
|H:\Video2|2,5 TB|https://mystorageaccount.blob.core.windows.net/video|  
|H:\Photo|30 GB|https://mystorageaccount.blob.core.windows.net/photo|  
|K:\Temp\FavoriteMovies.ISO|25 GB|https://mystorageaccount.blob.core.windows.net/favorite/FavoriteMovies.ISO|  
|\\\bigshare\john\music|10 GB|https://mystorageaccount.blob.core.windows.net/music|  
  
 Si noti che anche se hello `H:\Video`directory è stata divisa directory tootwo, puntano toohello stessa directory virtuale di destinazione nell'account di archiviazione hello. In questo modo, tutti i file video sono conservati in un unico `video` contenitore nell'account di archiviazione hello.  
  
 Successivamente, hello sopra origine directory sono uniformemente distribuite toohello due dischi rigidi:  
  
||||  
|-|-|-|  
|Disco rigido|Directory di origine|Dimensioni totali|  
|Prima unità|H:\Video1|2,5 TB + 30 GB|  
||H:\Photo||  
|Seconda unità|H:\Video2|2,5 TB + 35 GB|  
||K:\Temp\BlueRay.ISO||  
||\\\bigshare\john\music||  
  
Inoltre, è possibile impostare hello i metadati per tutti i file seguenti:  
  
-   **UploadMethod:** servizio Importazione/Esportazione di Windows Azure  
  
-   **DataSetName:** SampleData  
  
-   **CreationDate:** 10/1/2013  
  
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
  
-   **Content-Type:** application/octet-stream  
  
-   **Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ==  
  
-   **Cache-Control:** no-cache  
  
tooset queste proprietà, creare un file di testo, `c:\WAImportExport\SampleProperties.txt`:  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Properties>  
    <Content-Type>application/octet-stream</Content-Type>  
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>  
    <Cache-Control>no-cache</Cache-Control>  
</Properties>  
```
  
Si è ora pronto toorun hello strumento di importazione/esportazione di Azure tooprepare hello due unità disco rigido. Si noti che:  
  
-   Hello prima unità viene montata come unità X.  
  
-   Hello seconda unità viene montata come unità Y.  
  
-   chiave di Hello per l'account di archiviazione hello `mystorageaccount` è `8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg==`.  

## <a name="preparing-disk-for-import-when-data-is-pre-loaded"></a>Preparazione del disco per l'importazione con dati precaricati
 
 Se toobe dati hello importato è già presente nel disco hello, utilizzare /skipwrite flag hello. Valore di /t e /srcdir deve puntare toohello disco viene preparato per l'importazione. Se non tutti hello dati su disco hello deve toogo toohello stessa directory virtuale di destinazione o alla radice dell'account di archiviazione hello, esecuzione hello stesso comando per ogni directory separatamente mantenere il valore di hello del /id lo stesso in tutte le esecuzioni.

>[!NOTE] 
>Non specificare /format come che verrà cancellare i dati di hello sul disco hello. È possibile specificare / crittografare o /bk a seconda se il disco di hello è già crittografato o meno. 
>

```
    When data is already present on hello disk for each drive run hello following command.
    WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Video1 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:x:\Video1 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt /skipwrite
```

## <a name="copy-sessions---first-drive"></a>Copiare le sessioni - prima unità

Per la prima unità hello, eseguire lo strumento di importazione/esportazione di Azure due volte i hello toocopy due origine hello directory:  

**Prima sessione di copia**
  
```
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Video1 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:H:\Video1 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```

**Seconda sessione di copia**

```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Photo /srcdir:H:\Photo /dstdir:photo/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt
```

## <a name="copy-sessions---second-drive"></a>Copiare le sessioni - seconda unità
 
Per hello seconda unità, eseguire hello strumento di importazione/esportazione di Azure tre volte, una volta per hello ogni directory di origine e una volta per hello autonoma Blu-Ray™ file di immagine):  
  
**Prima sessione di copia** 

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:Video2 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:y /format /encrypt /srcdir:H:\Video2 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```
  
**Seconda sessione di copia**

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:Music /srcdir:\\bigshare\john\music /dstdir:music/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```  
  
**Terza sessione di copia**  

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:BlueRayIso /srcfile:K:\Temp\BlueRay.ISO /dstblob:favorite/BlueRay.ISO /MetadataFile:c:\WAImportExport\SampleMetadata.txt /PropertyFile:c:\WAImportExport\SampleProperties.txt  
```

## <a name="copy-session-completion"></a>Completamento della sessione di copia

Dopo aver completato le sessioni di copia hello, è possibile disconnettere hello due unità dal computer di hello copia e spedirle toohello appropriato centro dati di Windows Azure. Carica file journal hello due, `FirstDrive.jrn` e `SecondDrive.jrn`, quando si crea il processo di importazione hello in hello [il portale di gestione di Windows Azure](https://manage.windowsazure.com/).  
  
## <a name="next-steps"></a>Passaggi successivi

* [Preparing hard drives for an import job](storage-import-export-tool-preparing-hard-drives-import-v1.md) (Preparazione dei dischi rigidi per un processo di importazione)   
* [Quick reference for frequently used commands](storage-import-export-tool-quick-reference-v1.md) (Riferimento rapido per i comandi usati più di frequente) 
