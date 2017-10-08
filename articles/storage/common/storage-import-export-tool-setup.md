---
title: aaaSetting backup hello strumento di importazione/esportazione di Azure | Documenti Microsoft
description: "Informazioni su come tooset backup hello unità strumento di preparazione e per il servizio di importazione/esportazione di Azure hello."
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
ms.date: 06/29/2017
ms.author: muralikk
ms.openlocfilehash: 3d8897f2783112e07123669f1ba5b22576770e60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-hello-azure-importexport-tool"></a>Impostazione di hello strumento di importazione/esportazione di Azure

Strumento di importazione/esportazione di Microsoft Azure Hello è hello unità strumento di preparazione e che è possibile utilizzare con il servizio di importazione/esportazione di Microsoft Azure hello. È possibile utilizzare lo strumento hello per hello seguenti funzioni:

* Prima di creare un processo di importazione, è possibile utilizzare questo strumento toocopy dati toohello unità disco rigido verrà tooship tooan data center di Azure.
* Al termine di un processo di importazione, è possibile utilizzare questo toorepair strumento tutti i blob che sono stati danneggiati, mancano o in conflitto con altri BLOB.
* Dopo aver ricevuto hello unità da un processo di esportazione completato, è possibile utilizzare questo strumento toorepair tutti i file danneggiati o mancanti nelle unità hello.

## <a name="prerequisites"></a>Prerequisiti

Se si è **preparazione delle unità** per un processo di importazione, deve essere soddisfatti i seguenti prerequisiti hello:

* È necessario disporre di una sottoscrizione di Azure attiva.
* La sottoscrizione deve includere un account di archiviazione con numero di file hello toostore sufficiente spazio disponibile sarà tooimport.
* È necessario almeno una delle chiavi di accesso di account di archiviazione hello.
* È necessario un computer ("computer di copia" hello) con Windows 7, Windows Server 2008 R2 o installato un sistema operativo Windows più recente.
* Hello .NET Framework 4 deve essere installato nel computer di copia hello.
* BitLocker deve essere abilitato nel computer di copia hello.
* È necessario uno o più vuoto da 3,5 pollici dischi rigidi SATA connesso il computer di copia toohello.
* file Hello Prevedi tooimport devono essere accessibili dal computer di copia hello, che si trovino in una condivisione di rete o un disco rigido locale.

Se si sta tentando di troppo**recuperare un'importazione** che parzialmente non riuscita, è necessario:

* file di log di copia Hello
* chiave dell'account di archiviazione Hello

Se si sta tentando di troppo**recuperare un'esportazione** che parzialmente non riuscita, è necessario:

* file di log di copia Hello
* file manifesto Hello (facoltativi)
* chiave dell'account di archiviazione Hello

## <a name="installing-hello-azure-importexport-tool"></a>Hello installazione dello strumento di importazione/esportazione di Azure

Prima di tutto, [scaricare lo strumento di importazione/esportazione di Azure hello](https://www.microsoft.com/download/details.aspx?id=55280) ed estrarre i file tooa directory sul computer, ad esempio `c:\WAImportExport`.

Hello strumento di importazione/esportazione di Azure è costituita da hello i seguenti file:

* dataset.csv
* driveset.csv
* hddid.dll
* Microsoft.Data.Services.Client.dll
* Microsoft.WindowsAzure.Storage.dll
* Microsoft.WindowsAzure.Storage.pdb
* Microsoft.WindowsAzure.Storage.xml
* WAImportExport.exe
* WAImportExport.exe.config
* WAImportExport.pdb
* WAImportExportCore.dll
* WAImportExportCore.pdb
* WAImportExportRepair.dll
* WAImportExportRepair.pdb

Successivamente, aprire una finestra del prompt dei comandi in **modalità amministratore**, e modifiche nella directory hello hello contenente i file estratti.

Guida di toooutput per comando hello, eseguire lo strumento di hello (`WAImportExport.exe`) senza parametri:

```
WAImportExport, a client tool for Windows Azure Import/Export Service. Microsoft (c) 2013


Copy directories and/or files with a new copy session:
    WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> [/logdir:<LogDirectory>]
        [/sk:<StorageAccountKey>] [/silentmode] [/InitialDriveSet:<driveset.csv>]
        DataSet:<dataset.csv>

Add more drives:
    WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> /AdditionalDriveSet:<driveset.csv>

Abort an interrupted copy session:
    WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> /AbortSession

Resume an interrupted copy session:
    WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> /ResumeSession

List drives:
    WAImportExport.exe PrepImport /j:<JournalFile> /ListDrives

List copy sessions:
    WAImportExport.exe PrepImport /j:<JournalFile> /ListCopySessions

Repair a Drive:
    WAImportExport.exe RepairImport | RepairExport
        /r:<RepairFile> [/logdir:<LogDirectory>]
        [/d:<TargetDirectories>] [/bk:<BitLockerKey>]
        /sn:<StorageAccountName> /sk:<StorageAccountKey>
        [/CopyLogFile:<DriveCopyLogFile>] [/ManifestFile:<DriveManifestFile>]
        [/PathMapFile:<DrivePathMapFile>]

Preview an Export Job:
    WAImportExport.exe PreviewExport
        [/logdir:<LogDirectory>]
        /sn:<StorageAccountName> /sk:<StorageAccountKey>
        /ExportBlobListFile:<ExportBlobListFile> /DriveSize:<DriveSize>

Parameters:

    /j:<JournalFile>
        - Required. Path toohello journal file. A journal file tracks a set of drives and
          records hello progress in preparing these drives. hello journal file must always
          be specified.
    /logdir:<LogDirectory>
        - Optional. hello log directory. Verbose log files as well as some temporary
          files will be written toothis directory. If not specified, current directory
          will be used as hello log directory. hello log directory can be specified only
          once for hello same journal file.
    /id:<SessionId>
        - Optional. hello session Id is used tooidentify a copy session. It is used to
          ensure accurate recovery of an interrupted copy session.
    /ResumeSession
        - Optional. If hello last copy session was terminated abnormally, this parameter
          can be specified tooresume hello session.
    /AbortSession
        - Optional. If hello last copy session was terminated abnormally, this parameter
          can be specified tooabort hello session.
    /sn:<StorageAccountName>
        - Required. Only applicable for RepairImport and RepairExport. hello name of
          hello storage account.
    /sk:<StorageAccountKey>
        - Required. hello key of hello storage account.
    /InitialDriveSet:<driveset.csv>
        - Required. A .csv file that contains a list of drives tooprepare.
    /AdditionalDriveSet:<driveset.csv>
        - Required. A .csv file that contains a list of additional drives toobe added.
    /r:<RepairFile>
        - Required. Only applicable for RepairImport and RepairExport.
          Path toohello file for tracking repair progress. Each drive must have one
          and only one repair file.
    /d:<TargetDirectories>
        - Required. Only applicable for RepairImport and RepairExport.
          For RepairImport, one or more semicolon-separated directories toorepair;
          For RepairExport, one directory toorepair, e.g. root directory of hello drive.
    /CopyLogFile:<DriveCopyLogFile>
        - Required. Only applicable for RepairImport and RepairExport. Path toothe
          drive copy log file (verbose or error).
    /ManifestFile:<DriveManifestFile>
        - Required. Only applicable for RepairExport. Path toohello drive manifest file.
    /PathMapFile:<DrivePathMapFile>
        - Optional. Only applicable for RepairImport. Path toohello file containing
          mappings of file paths relative toohello drive root toolocations of actual files
          (tab-delimited). When first specified, it will be populated with file paths
          with empty targets, which means either they are not found in TargetDirectories,
          access denied, with invalid name, or they exist in multiple directories. The
          path map file can be manually edited tooinclude hello correct target paths and
          specified again for hello tool tooresolve hello file paths correctly.
    /ExportBlobListFile:<ExportBlobListFile>
        - Required. Path toohello XML file containing list of blob paths or blob path
          prefixes for hello blobs toobe exported. hello file format is hello same as the
          blob list blob format in hello Put Job operation of hello Import/Export Service
          REST API.
    /DriveSize:<DriveSize>
        - Required. Size of drives toobe used for export. For example, 500GB, 1.5TB.
          Note: 1 GB = 1,000,000,000 bytes
                1 TB = 1,000,000,000,000 bytes
    /DataSet:<dataset.csv>
        - Required. A .csv file that contains a list of directories and/or a list files
          toobe copied tootarget drives.

    /silentmode
        - Optional. If not specified, it will remind you hello requirement of drives and
          need your confirmation toocontinue.

Examples:

    Copy a data set tooa drive:
    WAImportExport.exe PrepImport
        /j:9WM35C2V.jrn /id:session#1 /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GEL
        xmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /InitialDriveSet:driveset1.csv
        /DataSet:data.csv

    Copy another dataset toohello same drive following hello above command:
    WAImportExport.exe PrepImport /j:9WM35C2V.jrn /id:session#2 /DataSet:dataset2.csv

    Preview how many 1.5 TB drives are needed for an export job:
    WAImportExport.exe PreviewExport
        /sn:mytestaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7K
        ysbbeKLDksg7VoN1W/a5UuM2zNgQ== /ExportBlobListFile:C:\temp\myexportbloblist.xml
        /DriveSize:1.5TB

    Repair an finished import job:
    WAImportExport.exe RepairImport
        /r:9WM35C2V.rep /d:X:\ /bk:442926-020713-108086-436744-137335-435358-242242-2795
        98 /sn:mytestaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94
        f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\temp\9WM35C2V_error.log
```

## <a name="next-steps"></a>Passaggi successivi

* [Preparing hard drives for an import job](../storage-import-export-tool-preparing-hard-drives-import.md) (Preparazione dei dischi rigidi per un processo di importazione)
* [Previewing drive usage for an export job](../storage-import-export-tool-previewing-drive-usage-export-v1.md) (Anteprima dell'uso del disco per un processo di esportazione)
* [Revisione dello stato dei processi con i file di log di copia](../storage-import-export-tool-reviewing-job-status-v1.md)
* [Riparazione di un processo di importazione](../storage-import-export-tool-repairing-an-import-job-v1.md)
* [Repairing an export job](../storage-import-export-tool-repairing-an-export-job-v1.md) (Riparazione di un processo di esportazione)
* [Risoluzione dei problemi hello strumento di importazione/esportazione di Azure](storage-import-export-tool-troubleshooting-v1.md)
