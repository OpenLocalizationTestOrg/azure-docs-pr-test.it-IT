---
title: un processo di importazione di importazione/esportazione di Azure - v1 aaaRepairing | Documenti Microsoft
description: "Informazioni su come un processo di importazione che è stato creato ed eseguito con toorepair hello importazione/esportazione di Azure service."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 38cc16bd-ad55-4625-9a85-e1726c35fd1b
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: a9ed81f50cffd8ae6e0cb21b25a04815c2b51ee5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="repairing-an-import-job"></a>Riparazione di un processo di importazione
servizio di importazione/esportazione di Microsoft Azure Hello potrebbe non riuscire toocopy alcuni dei file o parti di toohello un file del servizio Blob di Windows Azure. I motivi includono:  
  
-   File corrotti  
  
-   Unità danneggiate  
  
-   chiave dell'account archiviazione Hello modificata durante il trasferimento file hello.  
  
È possibile eseguire lo strumento di importazione/esportazione di Microsoft Azure hello con importazione hello file di log di copia del processo e strumento di hello caricherà i file mancanti hello (o parti di un file) del processo di importazione toocomplete tooyour Windows Azure storage account.  
  
## <a name="repairimport-parameters"></a>Parametri di RepairImport

Hello seguenti parametri possono essere specificati con **RepairImport**: 
  
|||  
|-|-|  
|**/r:**&lt;RepairFile\>|**Obbligatorio.** File di correzione toohello percorso, che tiene traccia dell'avanzamento hello di correzione hello e consente un ripristino interrotto tooresume. Ogni unità deve contenere un solo file di ripristino. Quando si avvia un ripristino per una determinata unità, verrà passato in hello percorso tooa file di ripristino non esiste ancora. tooresume un ripristino interrotto, è necessario passare nel nome hello di un file di ripristino esistente. è necessario specificare sempre Hello Ripristina file corrispondente toohello unità di destinazione.|  
|**/logdir:**&lt;LogDirectory\>|**Facoltativo.** directory dei log Hello. File di log dettagliati verranno scritti toothis directory. Se non viene specificata alcuna directory di log, la directory corrente hello da utilizzare come directory dei log hello.|  
|**/d:**<TargetDirectories\>|**Obbligatorio.** Uno o più directory di separati da punto e virgola contenenti hello file originali importati. unità di importazione Hello può anche essere usata, ma non è obbligatorio se sono disponibili posizioni alternative per i file originali.|  
|**/bk:**&lt;BitLockerKey\>|**Facoltativo.** Specificare la chiave di BitLocker hello se si desidera hello strumento toounlock un'unità crittografata in cui sono disponibili i file originali hello.|  
|**/sn:**<NomeAccountArchiviazione\>|**Obbligatorio.** nome Hello hello dell'account di archiviazione per hello processo di importazione.|  
|**/sk:**&lt;ChiaveAccountArchiviazione\>|**Obbligatorio** solo se non è specificata una firma di accesso condiviso del contenitore. processo di importazione chiave Hello per l'account di archiviazione hello per hello.|  
|**/csas:**&lt;ContainerSas\>|**Richiesto** se e solo se chiave dell'account di archiviazione hello non è specificato. contenitore di Hello SAS per accedere agli oggetti BLOB hello associato al processo di importazione hello.|  
|**/CopyLogFile:**&lt;DriveCopyLogFile\>|**Obbligatorio.** Percorso toohello copia file di log unità (log dettagliato o log degli errori). file Hello viene generato dal servizio di importazione/esportazione di Azure hello e può essere scaricato dall'archiviazione blob hello associata al processo hello. file di log di copia Hello contiene informazioni sui blob non riuscito o i file che sono toobe riparato.|  
|**/PathMapFile:**<DrivePathMapFile\>|**Facoltativo.** File di testo percorso tooa che può essere usato hello di ambiguità tooresolve se si dispone di più file con hello stesso nome che importati nello stesso processo. strumento di hello Hello prima ora viene eseguito, è possibile popolare questo file con tutti i nomi ambigui hello. Le esecuzioni successive dello strumento hello utilizzerà questa ambiguità hello tooresolve di file.|  
  
## <a name="using-hello-repairimport-command"></a>Comando RepairImport hello  
toorepair importazione di dati per flusso di dati di hello rete hello, è necessario specificare le directory hello contenenti hello file originali importati utilizzando hello `/d` parametro. È anche necessario specificare i file di log di copia hello scaricato dall'account di archiviazione. Toorepair una riga di comando tipica di un processo di importazione con errori parziali è simile:  
  
```  
WAImportExport.exe RepairImport /r:C:\WAImportExport\9WM35C2V.rep /d:C:\Users\bob\Pictures;X:\BobBackup\photos /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C2V.log  
```  
  
Hello Ecco un esempio di un file di log di copia. In questo caso, una 64 K parte di un file era danneggiata nell'unità spedita per il processo di importazione hello hello. Poiché questa è l'unico errore indicato hello, rest hello di BLOB hello nel processo di hello siano stati importati correttamente.  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveLog>  
 <DriveId>9WM35C2V</DriveId>  
 <Blob Status="CompletedWithErrors">  
 <BlobPath>pictures/animals/koala.jpg</BlobPath>  
 <FilePath>\animals\koala.jpg</FilePath>  
 <Length>163840</Length>  
 <ImportDisposition Status="Overwritten">overwrite</ImportDisposition>  
 <PageRangeList>  
  <PageRange Offset="65536" Length="65536" Hash="AA2585F6F6FD01C4AD4256E018240CD4" Status="Corrupted" />  
 </PageRangeList>  
 </Blob>  
 <Status>CompletedWithErrors</Status>  
</DriveLog>  
```
  
Quando questo log di copia viene passato toohello strumento di importazione/esportazione di Azure, lo strumento hello tenterà importazione hello toofinish del file copiando i contenuti mancanti hello in rete hello. Esempio hello precedente strumento hello cercherà il file originale di hello `\animals\koala.jpg` all'interno delle directory hello due `C:\Users\bob\Pictures` e `X:\BobBackup\photos`. Se hello file `C:\Users\bob\Pictures\animals\koala.jpg` esiste, hello strumento di importazione/esportazione di Azure copierà l'intervallo di blob di dati toohello corrispondente mancante hello `http://bobmediaaccount.blob.core.windows.net/pictures/animals/koala.jpg`.  
  
## <a name="resolving-conflicts-when-using-repairimport"></a>Risoluzione dei conflitti quando si usa RepairImport  
In alcuni casi, lo strumento hello potrebbe non essere toofind in grado di aprire hello necessari file o per uno dei seguenti motivi hello: Impossibile trovare il file hello, hello file non è accessibile, il nome di file hello è ambiguo o hello contenuto del file hello non è più corretto.  
  
Potrebbe verificarsi un errore ambiguo se strumento hello tenta toolocate `\animals\koala.jpg` ed è presente un file con lo stesso nome in entrambi `C:\Users\bob\pictures` e `X:\BobBackup\photos`. Ovvero, entrambi `C:\Users\bob\pictures\animals\koala.jpg` e `X:\BobBackup\photos\animals\koala.jpg` esiste in unità di processo di importazione hello.  
  
Hello `/PathMapFile` opzione consentirà tooresolve questi errori. È possibile specificare il nome di hello del file hello contenente elenco hello dei file hello strumento non è in grado di identificare toocorrectly. di seguito Hello è una riga di comando di esempio che popolerebbe il file `9WM35C2V_pathmap.txt`:  
  
```
WAImportExport.exe RepairImport /r:C:\WAImportExport\9WM35C2V.rep /d:C:\Users\bob\Pictures;X:\BobBackup\photos /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C2V.log /PathMapFile:C:\WAImportExport\9WM35C2V_pathmap.txt  
```
  
Hello strumento scriverà quindi i percorsi di file problematico hello troppo`9WM35C2V_pathmap.txt`, uno per ogni riga. Ad esempio, file hello può contenere hello seguenti voci dopo l'esecuzione comando hello:  
 
```
\animals\koala.jpg  
\animals\kangaroo.jpg  
```
  
 Per ogni file nell'elenco di hello, si deve tentare toolocate e aprire tooensure file hello è lo strumento toohello disponibile. Se si desidera strumento hello tootell in modo esplicito in un file toofind, è possibile modificare il percorso di hello file di mappa e aggiungere hello percorso tooeach file su hello stessa riga, separati da un carattere di tabulazione:  
  
```
\animals\koala.jpg           C:\Users\bob\Pictures\animals\koala.jpg  
\animals\kangaroo.jpg        X:\BobBackup\photos\animals\kangaroo.jpg  
```
  
Dopo che lo strumento di toohello disponibili i file necessari hello o l'aggiornamento del file hello percorso mappa, è possibile eseguire nuovamente processo di importazione hello toocomplete strumento hello.  
  
## <a name="next-steps"></a>Passaggi successivi
 
* [Impostazione hello strumento di importazione/esportazione di Azure](storage-import-export-tool-setup-v1.md)   
* [Preparing hard drives for an import job](storage-import-export-tool-preparing-hard-drives-import-v1.md) (Preparazione dei dischi rigidi per un processo di importazione)   
* [Reviewing job status with copy log files](storage-import-export-tool-reviewing-job-status-v1.md) (Revisione dello stato dei processi con i file di log di copia)   
* [Repairing an export job](storage-import-export-tool-repairing-an-export-job-v1.md) (Riparazione di un processo di esportazione)   
* [Risoluzione dei problemi hello strumento di importazione/esportazione di Azure](storage-import-export-tool-troubleshooting-v1.md)
