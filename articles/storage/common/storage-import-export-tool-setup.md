---
title: Configurazione dello strumento Importazione/Esportazione di Azure | Documentazione Microsoft
description: "Informazioni su come configurare lo strumento di preparazione e ripristino delle unità per il servizio Importazione/Esportazione di Azure."
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
ms.openlocfilehash: 5b73fec119a88cd86e68537199e7567afa3fdba8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="setting-up-the-azure-importexport-tool"></a><span data-ttu-id="4156e-103">Configurazione dello strumento Importazione/Esportazione di Azure</span><span class="sxs-lookup"><span data-stu-id="4156e-103">Setting up the Azure Import/Export Tool</span></span>

<span data-ttu-id="4156e-104">Lo strumento Importazione/Esportazione di Microsoft Azure è lo strumento di preparazione e ripristino delle unità che è possibile usare con il servizio Importazione/Esportazione di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="4156e-104">The Microsoft Azure Import/Export Tool is the drive preparation and repair tool that you can use with the Microsoft Azure Import/Export service.</span></span> <span data-ttu-id="4156e-105">È possibile usare lo strumento per svolgere le funzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="4156e-105">You can use the tool for the following functions:</span></span>

* <span data-ttu-id="4156e-106">Prima di creare un processo di importazione, è possibile usare questo strumento per copiare i dati nei dischi rigidi che si intende spedire a un data center di Azure.</span><span class="sxs-lookup"><span data-stu-id="4156e-106">Before creating an import job, you can use this tool to copy data to the hard drives you are going to ship to an Azure data center.</span></span>
* <span data-ttu-id="4156e-107">Al termine di un processo di importazione, è possibile usare questo strumento per ripristinare eventuali BLOB danneggiati, mancanti o in conflitto con altri BLOB.</span><span class="sxs-lookup"><span data-stu-id="4156e-107">After an import job has completed, you can use this tool to repair any blobs that were corrupted, were missing, or conflicted with other blobs.</span></span>
* <span data-ttu-id="4156e-108">Dopo aver ricevuto le unità da un processo di esportazione completato, è possibile usare questo strumento per recuperare eventuali file danneggiati o mancanti nelle unità.</span><span class="sxs-lookup"><span data-stu-id="4156e-108">After you receive the drives from a completed export job, you can use this tool to repair any files that were corrupted or missing on the drives.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4156e-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="4156e-109">Prerequisites</span></span>

<span data-ttu-id="4156e-110">Se si intende **preparare le unità** per un processo di importazione, è necessario soddisfare i prerequisiti seguenti:</span><span class="sxs-lookup"><span data-stu-id="4156e-110">If you are **preparing drives** for an import job, the following prerequisites must be met:</span></span>

* <span data-ttu-id="4156e-111">È necessario disporre di una sottoscrizione di Azure attiva.</span><span class="sxs-lookup"><span data-stu-id="4156e-111">You must have an active Azure subscription.</span></span>
* <span data-ttu-id="4156e-112">La sottoscrizione deve includere un account di archiviazione con spazio disponibile sufficiente per archiviare i file che si intende importare.</span><span class="sxs-lookup"><span data-stu-id="4156e-112">Your subscription must include a storage account with enough available space to store the files you are going to import.</span></span>
* <span data-ttu-id="4156e-113">È necessaria almeno una delle chiavi di accesso dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="4156e-113">You need at least one of the storage account access keys.</span></span>
* <span data-ttu-id="4156e-114">È necessario un computer ("computer di copia") in cui sia installato Windows 7, Windows Server 2008 R2 o un sistema operativo Windows più recente.</span><span class="sxs-lookup"><span data-stu-id="4156e-114">You need a computer (the "copy machine") with Windows 7, Windows Server 2008 R2, or a newer Windows operating system installed.</span></span>
* <span data-ttu-id="4156e-115">Nel computer di copia deve essere installato .NET Framework 4.</span><span class="sxs-lookup"><span data-stu-id="4156e-115">The .NET Framework 4 must be installed on the copy machine.</span></span>
* <span data-ttu-id="4156e-116">Nel computer di copia deve essere abilitato BitLocker.</span><span class="sxs-lookup"><span data-stu-id="4156e-116">BitLocker must be enabled on the copy machine.</span></span>
* <span data-ttu-id="4156e-117">Sono necessari uno o più dischi rigidi SATA da 3,5 pollici vuoti connessi al computer di copia.</span><span class="sxs-lookup"><span data-stu-id="4156e-117">You need one or more empty 3.5-inch SATA hard drives connected to the copy machine.</span></span>
* <span data-ttu-id="4156e-118">I file che si intende importare devono essere accessibili dal computer di copia, che si trovino in una condivisione di rete o in un disco rigido locale.</span><span class="sxs-lookup"><span data-stu-id="4156e-118">The files you plan to import must be accessible from the copy machine, whether they are on a network share or a local hard drive.</span></span>

<span data-ttu-id="4156e-119">Se si tenta di **recuperare un'importazione** parzialmente non riuscita, è necessario disporre dei seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="4156e-119">If you are attempting to **repair an import** that has partially failed, you need:</span></span>

* <span data-ttu-id="4156e-120">I file di log di copia</span><span class="sxs-lookup"><span data-stu-id="4156e-120">The copy log files</span></span>
* <span data-ttu-id="4156e-121">La chiave dell'account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="4156e-121">The storage account key</span></span>

<span data-ttu-id="4156e-122">Se si tenta di **recuperare un'esportazione** parzialmente non riuscita, è necessario disporre dei seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="4156e-122">If you are attempting to **repair an export**  that has partially failed, you need:</span></span>

* <span data-ttu-id="4156e-123">I file di log di copia</span><span class="sxs-lookup"><span data-stu-id="4156e-123">The copy log files</span></span>
* <span data-ttu-id="4156e-124">I file manifesto (facoltativi)</span><span class="sxs-lookup"><span data-stu-id="4156e-124">The manifest files (optional)</span></span>
* <span data-ttu-id="4156e-125">La chiave dell'account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="4156e-125">The storage account key</span></span>

## <a name="installing-the-azure-importexport-tool"></a><span data-ttu-id="4156e-126">Installazione dello strumento di importazione/esportazione di Azure</span><span class="sxs-lookup"><span data-stu-id="4156e-126">Installing the Azure Import/Export Tool</span></span>

<span data-ttu-id="4156e-127">Prima di tutto [scaricare lo strumento Importazione/Esportazione di Azure](https://www.microsoft.com/download/details.aspx?id=55280) ed estrarlo in una directory nel computer in uso, ad esempio `c:\WAImportExport`.</span><span class="sxs-lookup"><span data-stu-id="4156e-127">First, [download the Azure Import/Export Tool](https://www.microsoft.com/download/details.aspx?id=55280) and extract it to a directory on your computer, for example `c:\WAImportExport`.</span></span>

<span data-ttu-id="4156e-128">Lo strumento Importazione/Esportazione di Azure è costituito dai file indicati di seguito:</span><span class="sxs-lookup"><span data-stu-id="4156e-128">The Azure Import/Export Tool consists of the following files:</span></span>

* <span data-ttu-id="4156e-129">dataset.csv</span><span class="sxs-lookup"><span data-stu-id="4156e-129">dataset.csv</span></span>
* <span data-ttu-id="4156e-130">driveset.csv</span><span class="sxs-lookup"><span data-stu-id="4156e-130">driveset.csv</span></span>
* <span data-ttu-id="4156e-131">hddid.dll</span><span class="sxs-lookup"><span data-stu-id="4156e-131">hddid.dll</span></span>
* <span data-ttu-id="4156e-132">Microsoft.Data.Services.Client.dll</span><span class="sxs-lookup"><span data-stu-id="4156e-132">Microsoft.Data.Services.Client.dll</span></span>
* <span data-ttu-id="4156e-133">Microsoft.WindowsAzure.Storage.dll</span><span class="sxs-lookup"><span data-stu-id="4156e-133">Microsoft.WindowsAzure.Storage.dll</span></span>
* <span data-ttu-id="4156e-134">Microsoft.WindowsAzure.Storage.pdb</span><span class="sxs-lookup"><span data-stu-id="4156e-134">Microsoft.WindowsAzure.Storage.pdb</span></span>
* <span data-ttu-id="4156e-135">Microsoft.WindowsAzure.Storage.xml</span><span class="sxs-lookup"><span data-stu-id="4156e-135">Microsoft.WindowsAzure.Storage.xml</span></span>
* <span data-ttu-id="4156e-136">WAImportExport.exe</span><span class="sxs-lookup"><span data-stu-id="4156e-136">WAImportExport.exe</span></span>
* <span data-ttu-id="4156e-137">WAImportExport.exe.config</span><span class="sxs-lookup"><span data-stu-id="4156e-137">WAImportExport.exe.config</span></span>
* <span data-ttu-id="4156e-138">WAImportExport.pdb</span><span class="sxs-lookup"><span data-stu-id="4156e-138">WAImportExport.pdb</span></span>
* <span data-ttu-id="4156e-139">WAImportExportCore.dll</span><span class="sxs-lookup"><span data-stu-id="4156e-139">WAImportExportCore.dll</span></span>
* <span data-ttu-id="4156e-140">WAImportExportCore.pdb</span><span class="sxs-lookup"><span data-stu-id="4156e-140">WAImportExportCore.pdb</span></span>
* <span data-ttu-id="4156e-141">WAImportExportRepair.dll</span><span class="sxs-lookup"><span data-stu-id="4156e-141">WAImportExportRepair.dll</span></span>
* <span data-ttu-id="4156e-142">WAImportExportRepair.pdb</span><span class="sxs-lookup"><span data-stu-id="4156e-142">WAImportExportRepair.pdb</span></span>

<span data-ttu-id="4156e-143">Aprire quindi una finestra del prompt dei comandi in **modalità amministratore** e passare alla directory contenente i file estratti.</span><span class="sxs-lookup"><span data-stu-id="4156e-143">Next, open a Command Prompt window in **Administrator mode**, and change into the directory containing the extracted files.</span></span>

<span data-ttu-id="4156e-144">Per visualizzare la Guida per il comando, eseguire lo strumento (`WAImportExport.exe`) senza parametri:</span><span class="sxs-lookup"><span data-stu-id="4156e-144">To output help for the command, run the tool (`WAImportExport.exe`) without parameters:</span></span>

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
        - Required. Path to the journal file. A journal file tracks a set of drives and
          records the progress in preparing these drives. The journal file must always
          be specified.
    /logdir:<LogDirectory>
        - Optional. The log directory. Verbose log files as well as some temporary
          files will be written to this directory. If not specified, current directory
          will be used as the log directory. The log directory can be specified only
          once for the same journal file.
    /id:<SessionId>
        - Optional. The session Id is used to identify a copy session. It is used to
          ensure accurate recovery of an interrupted copy session.
    /ResumeSession
        - Optional. If the last copy session was terminated abnormally, this parameter
          can be specified to resume the session.
    /AbortSession
        - Optional. If the last copy session was terminated abnormally, this parameter
          can be specified to abort the session.
    /sn:<StorageAccountName>
        - Required. Only applicable for RepairImport and RepairExport. The name of
          the storage account.
    /sk:<StorageAccountKey>
        - Required. The key of the storage account.
    /InitialDriveSet:<driveset.csv>
        - Required. A .csv file that contains a list of drives to prepare.
    /AdditionalDriveSet:<driveset.csv>
        - Required. A .csv file that contains a list of additional drives to be added.
    /r:<RepairFile>
        - Required. Only applicable for RepairImport and RepairExport.
          Path to the file for tracking repair progress. Each drive must have one
          and only one repair file.
    /d:<TargetDirectories>
        - Required. Only applicable for RepairImport and RepairExport.
          For RepairImport, one or more semicolon-separated directories to repair;
          For RepairExport, one directory to repair, e.g. root directory of the drive.
    /CopyLogFile:<DriveCopyLogFile>
        - Required. Only applicable for RepairImport and RepairExport. Path to the
          drive copy log file (verbose or error).
    /ManifestFile:<DriveManifestFile>
        - Required. Only applicable for RepairExport. Path to the drive manifest file.
    /PathMapFile:<DrivePathMapFile>
        - Optional. Only applicable for RepairImport. Path to the file containing
          mappings of file paths relative to the drive root to locations of actual files
          (tab-delimited). When first specified, it will be populated with file paths
          with empty targets, which means either they are not found in TargetDirectories,
          access denied, with invalid name, or they exist in multiple directories. The
          path map file can be manually edited to include the correct target paths and
          specified again for the tool to resolve the file paths correctly.
    /ExportBlobListFile:<ExportBlobListFile>
        - Required. Path to the XML file containing list of blob paths or blob path
          prefixes for the blobs to be exported. The file format is the same as the
          blob list blob format in the Put Job operation of the Import/Export Service
          REST API.
    /DriveSize:<DriveSize>
        - Required. Size of drives to be used for export. For example, 500GB, 1.5TB.
          Note: 1 GB = 1,000,000,000 bytes
                1 TB = 1,000,000,000,000 bytes
    /DataSet:<dataset.csv>
        - Required. A .csv file that contains a list of directories and/or a list files
          to be copied to target drives.

    /silentmode
        - Optional. If not specified, it will remind you the requirement of drives and
          need your confirmation to continue.

Examples:

    Copy a data set to a drive:
    WAImportExport.exe PrepImport
        /j:9WM35C2V.jrn /id:session#1 /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GEL
        xmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /InitialDriveSet:driveset1.csv
        /DataSet:data.csv

    Copy another dataset to the same drive following the above command:
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

## <a name="next-steps"></a><span data-ttu-id="4156e-145">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4156e-145">Next steps</span></span>

* <span data-ttu-id="4156e-146">[Preparing hard drives for an import job](../storage-import-export-tool-preparing-hard-drives-import.md) (Preparazione dei dischi rigidi per un processo di importazione)</span><span class="sxs-lookup"><span data-stu-id="4156e-146">[Preparing hard drives for an import job](../storage-import-export-tool-preparing-hard-drives-import.md)</span></span>
* <span data-ttu-id="4156e-147">[Previewing drive usage for an export job](../storage-import-export-tool-previewing-drive-usage-export-v1.md) (Anteprima dell'uso del disco per un processo di esportazione)</span><span class="sxs-lookup"><span data-stu-id="4156e-147">[Previewing drive usage for an export job](../storage-import-export-tool-previewing-drive-usage-export-v1.md)</span></span>
* [<span data-ttu-id="4156e-148">Revisione dello stato dei processi con i file di log di copia</span><span class="sxs-lookup"><span data-stu-id="4156e-148">Reviewing job status with copy log files</span></span>](../storage-import-export-tool-reviewing-job-status-v1.md)
* [<span data-ttu-id="4156e-149">Riparazione di un processo di importazione</span><span class="sxs-lookup"><span data-stu-id="4156e-149">Repairing an import job</span></span>](../storage-import-export-tool-repairing-an-import-job-v1.md)
* <span data-ttu-id="4156e-150">[Repairing an export job](../storage-import-export-tool-repairing-an-export-job-v1.md) (Riparazione di un processo di esportazione)</span><span class="sxs-lookup"><span data-stu-id="4156e-150">[Repairing an export job](../storage-import-export-tool-repairing-an-export-job-v1.md)</span></span>
* [<span data-ttu-id="4156e-151">Risoluzione dei problemi relativi allo strumento Importazione/Esportazione di Azure</span><span class="sxs-lookup"><span data-stu-id="4156e-151">Troubleshooting the Azure Import/Export Tool</span></span>](storage-import-export-tool-troubleshooting-v1.md)
