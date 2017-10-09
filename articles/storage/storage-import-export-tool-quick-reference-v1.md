---
title: riferimento aaaQuick per i comandi di processo di importazione dello strumento di importazione/esportazione di Azure - v1 | Documenti Microsoft
description: Guida di riferimento per i comandi dello strumento Importazione/Esportazione di Azure usati di frequente per i processi di importazione. Si riferisce toov1 di hello strumento di importazione/esportazione.
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
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: e36f065e5d23268758cf6b6db9428fe8a8e1056d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="quick-reference-for-frequently-used-commands-for-import-jobs"></a>Informazioni di riferimento rapido sui comandi di uso frequente per i processi di importazione
In questa sezione vengono forniti riferimenti rapidi per alcuni comandi usati di frequente. Per informazioni dettagliate sull'uso, vedere [Preparazione dei dischi rigidi per un processo di importazione](storage-import-export-tool-preparing-hard-drives-import-v1.md).  

## <a name="prepare-hello-disks-when-data-already-copied-toohello-disks"></a>Preparare i dischi di hello quando i dati copiati già toohello dischi
 Ecco un tooprepare di comando di esempio un dischi quando i dati copiati già toohello disco rigido che non ancora crittografato con BitLocker:  
  
```  
  WAImportExport.exe PrepImport /j:9WM35C2V.jrn /id:session#1 /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /t:d /encrypt /srcdir:d:\movies\drama /dstdir:movies/drama/ /skipwrite
```    

## <a name="copy-a-single-directory-tooa-hard-drive"></a>Copiare un singola directory tooa disco rigido  
 Ecco un toocopy di comando di esempio una singola origine directory tooa unità disco rigido non ancora crittografato con BitLocker:  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:movies /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:d:\Movies /dstdir:entertainment/movies/  
```  
  
## <a name="copy-wwo-directories-tooa-hard-drive"></a>Copiare wwo directory tooa disco rigido  
 toocopy due directory tooa unità di origine, sono necessari due comandi.  
  
 Hello primo comando specifica directory log hello, chiave dell'account di archiviazione, lettera di unità di destinazione e `format/encrypt` requisiti, in parametri comuni di addizione toohello:  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:movies /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:d:\Movies /dstdir:entertainment/movies/  
```  
  
 comando secondo Hello specifica file journal hello, un nuovo ID sessione e i percorsi di origine e destinazione di hello:  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:music /srcdir:d:\Music /dstdir:entertainment/music/  
```  
  
## <a name="copy-a-large-file-tooa-hard-drive-in-a-second-copy-session"></a>Copiare un file di grandi dimensioni tooa disco rigido in una seconda sessione di copia  
 Di seguito è riportato un esempio del comando che consente di copiare un'unità tooa singolo file di grandi dimensioni che è stata preparata in una sessione di copia precedente:  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:dvd /srcfile:d:\dvd\favoritemovie.vhd /dstblob:dvd/favoritemovie.vhd  
```  
  
## <a name="next-steps"></a>Passaggi successivi

* [Unità disco rigido tooprepare del flusso di lavoro di esempio per un processo di importazione](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow-v1.md)
