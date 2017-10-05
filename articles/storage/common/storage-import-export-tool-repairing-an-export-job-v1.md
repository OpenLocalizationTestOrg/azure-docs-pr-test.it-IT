---
title: Riparazione di un processo di esportazione in Importazione/Esportazione di Azure - versione 1 | Documentazione Microsoft
description: "Informazioni su come ripristinare un processo di esportazione che è stato creato ed eseguito tramite il servizio Importazione/Esportazione di Azure."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 728e2a42-04ce-4be8-9375-e9e2bc6827a5
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 57ab58fa1fd8371d0b6f019f94bb162bcc1e0e43
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="repairing-an-export-job"></a><span data-ttu-id="b359f-103">Riparazione di un processo di esportazione</span><span class="sxs-lookup"><span data-stu-id="b359f-103">Repairing an export job</span></span>
<span data-ttu-id="b359f-104">Al termine di un processo di esportazione, è possibile eseguire lo strumento Importazione/Esportazione di Microsoft Azure in locale per:</span><span class="sxs-lookup"><span data-stu-id="b359f-104">After an export job has completed, you can run the Microsoft Azure Import/Export Tool on-premises to:</span></span>  
  
1.  <span data-ttu-id="b359f-105">Scaricare i file che il servizio di Importazione/Esportazione di Azure non è riuscito a esportare.</span><span class="sxs-lookup"><span data-stu-id="b359f-105">Download any files that the Azure Import/Export service was unable to export.</span></span>  
  
2.  <span data-ttu-id="b359f-106">Verificare che i file sull'unità siano stati esportati correttamente.</span><span class="sxs-lookup"><span data-stu-id="b359f-106">Validate that the files on the drive were correctly exported.</span></span>  
  
<span data-ttu-id="b359f-107">È necessario disporre della connettività all'archiviazione di Azure per usare questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="b359f-107">You must have connectivity to Azure Storage to use this functionality.</span></span>  
  
<span data-ttu-id="b359f-108">Il comando per la riparazione di un processo di importazione è **RepairExport**.</span><span class="sxs-lookup"><span data-stu-id="b359f-108">The command for repairing an import job is **RepairExport**.</span></span>

## <a name="repairexport-parameters"></a><span data-ttu-id="b359f-109">Parametri di RepairExport</span><span class="sxs-lookup"><span data-stu-id="b359f-109">RepairExport parameters</span></span>

<span data-ttu-id="b359f-110">È possibile specificare i parametri seguenti con **RepairExport**:</span><span class="sxs-lookup"><span data-stu-id="b359f-110">The following parameters can be specified with **RepairExport**:</span></span>  
  
|<span data-ttu-id="b359f-111">Parametro</span><span class="sxs-lookup"><span data-stu-id="b359f-111">Parameter</span></span>|<span data-ttu-id="b359f-112">Descrizione</span><span class="sxs-lookup"><span data-stu-id="b359f-112">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="b359f-113">**/r:<RepairFile\>**</span><span class="sxs-lookup"><span data-stu-id="b359f-113">**/r:<RepairFile\>**</span></span>|<span data-ttu-id="b359f-114">Obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="b359f-114">Required.</span></span> <span data-ttu-id="b359f-115">Percorso del file di ripristino che tiene traccia dell'avanzamento del ripristino e consente di riprendere un ripristino interrotto.</span><span class="sxs-lookup"><span data-stu-id="b359f-115">Path to the repair file, which tracks the progress of the repair, and allows you to resume an interrupted repair.</span></span> <span data-ttu-id="b359f-116">Ogni unità deve contenere un solo file di ripristino.</span><span class="sxs-lookup"><span data-stu-id="b359f-116">Each drive must have one and only one repair file.</span></span> <span data-ttu-id="b359f-117">Quando si avvia un ripristino per una determinata unità, si viene spostati nel percorso di un file di ripristino che non esiste ancora.</span><span class="sxs-lookup"><span data-stu-id="b359f-117">When you start a repair for a given drive, you will pass in the path to a repair file which does not yet exist.</span></span> <span data-ttu-id="b359f-118">Per riprendere un ripristino interrotto, è consigliabile inserire il nome di un file di ripristino esistente.</span><span class="sxs-lookup"><span data-stu-id="b359f-118">To resume an interrupted repair, you should pass in the name of an existing repair file.</span></span> <span data-ttu-id="b359f-119">Il file di ripristino corrispondente all'unità di destinazione deve essere sempre specificato.</span><span class="sxs-lookup"><span data-stu-id="b359f-119">The repair file corresponding to the target drive must always be specified.</span></span>|  
|<span data-ttu-id="b359f-120">**/logdir:<LogDirectory\>**</span><span class="sxs-lookup"><span data-stu-id="b359f-120">**/logdir:<LogDirectory\>**</span></span>|<span data-ttu-id="b359f-121">Facoltativa.</span><span class="sxs-lookup"><span data-stu-id="b359f-121">Optional.</span></span> <span data-ttu-id="b359f-122">Directory dei log.</span><span class="sxs-lookup"><span data-stu-id="b359f-122">The log directory.</span></span> <span data-ttu-id="b359f-123">in cui verranno scritti file di log dettagliati.</span><span class="sxs-lookup"><span data-stu-id="b359f-123">Verbose log files will be written to this directory.</span></span> <span data-ttu-id="b359f-124">Se non è specificata alcuna directory dei log, verrà usata la directory corrente.</span><span class="sxs-lookup"><span data-stu-id="b359f-124">If no log directory is specified, the current directory will be used as the log directory.</span></span>|  
|<span data-ttu-id="b359f-125">**/d:<TargetDirectory\>**</span><span class="sxs-lookup"><span data-stu-id="b359f-125">**/d:<TargetDirectory\>**</span></span>|<span data-ttu-id="b359f-126">Obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="b359f-126">Required.</span></span> <span data-ttu-id="b359f-127">La directory per la convalida e il ripristino.</span><span class="sxs-lookup"><span data-stu-id="b359f-127">The directory to validate and repair.</span></span> <span data-ttu-id="b359f-128">Si tratta in genere della directory radice dell'unità di esportazione, ma potrebbe anche essere una condivisione di file di rete che contiene una copia dei file esportati.</span><span class="sxs-lookup"><span data-stu-id="b359f-128">This is usually the root directory of the export drive, but could also be a network file share containing a copy of the exported files.</span></span>|  
|<span data-ttu-id="b359f-129">**/bk:<BitLockerKey\>**</span><span class="sxs-lookup"><span data-stu-id="b359f-129">**/bk:<BitLockerKey\>**</span></span>|<span data-ttu-id="b359f-130">Facoltativa.</span><span class="sxs-lookup"><span data-stu-id="b359f-130">Optional.</span></span> <span data-ttu-id="b359f-131">È necessario specificare la chiave BitLocker se si desidera che lo strumento sblocchi un'unità crittografata in cui sono archiviati i file esportati.</span><span class="sxs-lookup"><span data-stu-id="b359f-131">You should specify the BitLocker key if you want the tool to unlock an encrypted where the exported files are stored.</span></span>|  
|<span data-ttu-id="b359f-132">**/sn:<StorageAccountName\>**</span><span class="sxs-lookup"><span data-stu-id="b359f-132">**/sn:<StorageAccountName\>**</span></span>|<span data-ttu-id="b359f-133">Obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="b359f-133">Required.</span></span> <span data-ttu-id="b359f-134">Il nome dell'account di archiviazione per il processo di esportazione.</span><span class="sxs-lookup"><span data-stu-id="b359f-134">The name of the storage account for the export job.</span></span>|  
|<span data-ttu-id="b359f-135">**/sk:<StorageAccountKey\>**</span><span class="sxs-lookup"><span data-stu-id="b359f-135">**/sk:<StorageAccountKey\>**</span></span>|<span data-ttu-id="b359f-136">**Obbligatorio** solo se non è specificata una firma di accesso condiviso del contenitore.</span><span class="sxs-lookup"><span data-stu-id="b359f-136">**Required** if and only if a container SAS is not specified.</span></span> <span data-ttu-id="b359f-137">Chiave dell'account per l'account di archiviazione per il processo di esportazione.</span><span class="sxs-lookup"><span data-stu-id="b359f-137">The account key for the storage account for the export job.</span></span>|  
|<span data-ttu-id="b359f-138">**/csas:<ContainerSas\>**</span><span class="sxs-lookup"><span data-stu-id="b359f-138">**/csas:<ContainerSas\>**</span></span>|<span data-ttu-id="b359f-139">**Obbligatorio** solo se non è specificata la chiave dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="b359f-139">**Required** if and only if the storage account key is not specified.</span></span> <span data-ttu-id="b359f-140">Firma di accesso condiviso del contenitore per l'accesso ai BLOB associati al processo di esportazione.</span><span class="sxs-lookup"><span data-stu-id="b359f-140">The container SAS for accessing the blobs associated with the export job.</span></span>|  
|<span data-ttu-id="b359f-141">**/CopyLogFile:\><DriveCopyLogFile**</span><span class="sxs-lookup"><span data-stu-id="b359f-141">**/CopyLogFile:<DriveCopyLogFile\>**</span></span>|<span data-ttu-id="b359f-142">Obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="b359f-142">Required.</span></span> <span data-ttu-id="b359f-143">Il percorso del file dei log di copia dell'unità.</span><span class="sxs-lookup"><span data-stu-id="b359f-143">The path to the drive copy log file.</span></span> <span data-ttu-id="b359f-144">Il file viene generato dal servizio di Importazione/Esportazione di Azure e può essere scaricato dall'archiviazione BLOB associata al processo.</span><span class="sxs-lookup"><span data-stu-id="b359f-144">The file is generated by the Windows Azure Import/Export service and can be downloaded from the blob storage associated with the job.</span></span> <span data-ttu-id="b359f-145">Il file dei log di copia contiene informazioni sui BLOB non riusciti o sui file da ripristinare.</span><span class="sxs-lookup"><span data-stu-id="b359f-145">The copy log file contains information about failed blobs or files which are to be repaired.</span></span>|  
|<span data-ttu-id="b359f-146">**/ManifestFile:<DriveManifestFile\>**</span><span class="sxs-lookup"><span data-stu-id="b359f-146">**/ManifestFile:<DriveManifestFile\>**</span></span>|<span data-ttu-id="b359f-147">Facoltativa.</span><span class="sxs-lookup"><span data-stu-id="b359f-147">Optional.</span></span> <span data-ttu-id="b359f-148">Il percorso al file manifesto dell'unità di esportazione.</span><span class="sxs-lookup"><span data-stu-id="b359f-148">The path to the export drive's manifest file.</span></span> <span data-ttu-id="b359f-149">Questo file è generato dal servizio Importazione/Esportazione di Azure e archiviato nell'unità di esportazione e facoltativamente in un BLOB nell'account di archiviazione associato al processo.</span><span class="sxs-lookup"><span data-stu-id="b359f-149">This file is generated by the Windows Azure Import/Export service and stored on the export drive, and optionally in a blob in the storage account associated with the job.</span></span><br /><br /> <span data-ttu-id="b359f-150">Il contenuto dei file nell'unità di esportazione verrà verificato con gli hash MD5 contenuti in questo file.</span><span class="sxs-lookup"><span data-stu-id="b359f-150">The content of the files on the export drive will be verified with the MD5 hashes contained in this file.</span></span> <span data-ttu-id="b359f-151">Tutti i file considerati danneggiati che saranno scaricati e riscritti nelle directory di destinazione.</span><span class="sxs-lookup"><span data-stu-id="b359f-151">Any files that are determined to be corrupted will be downloaded and rewritten to the target directories.</span></span>|  
  
## <a name="using-repairexport-mode-to-correct-failed-exports"></a><span data-ttu-id="b359f-152">Uso della modalità RepairExport per correggere esportazioni non riuscite</span><span class="sxs-lookup"><span data-stu-id="b359f-152">Using RepairExport mode to correct failed exports</span></span>  
<span data-ttu-id="b359f-153">È possibile usare lo strumento Importazione/Esportazione di Azure per scaricare i file non esportati.</span><span class="sxs-lookup"><span data-stu-id="b359f-153">You can use the Azure Import/Export Tool to download files that failed to export.</span></span> <span data-ttu-id="b359f-154">Il file di log di copia conterrà un elenco di file con errori di esportazione.</span><span class="sxs-lookup"><span data-stu-id="b359f-154">The copy log file will contain a list of files that failed to export.</span></span>  
  
<span data-ttu-id="b359f-155">Le cause di errori di esportazione includono le possibilità seguenti:</span><span class="sxs-lookup"><span data-stu-id="b359f-155">The causes of export failures include the following possibilities:</span></span>  
  
-   <span data-ttu-id="b359f-156">Unità danneggiate</span><span class="sxs-lookup"><span data-stu-id="b359f-156">Damaged drives</span></span>  
  
-   <span data-ttu-id="b359f-157">La chiave di account di archiviazione modificata durante il processo di trasferimento</span><span class="sxs-lookup"><span data-stu-id="b359f-157">The storage account key changed during the transfer process</span></span>  
  
<span data-ttu-id="b359f-158">Per eseguire lo strumento in modalità **RepairExport**, è necessario innanzitutto connettere l'unità contenente i file esportati nel computer.</span><span class="sxs-lookup"><span data-stu-id="b359f-158">To run the tool in **RepairExport** mode, you first need to connect the drive containing the exported files to your computer.</span></span> <span data-ttu-id="b359f-159">Eseguire poi lo strumento Importazione/Esportazione di Azure, specificando il percorso dell'unità con il parametro `/d`.</span><span class="sxs-lookup"><span data-stu-id="b359f-159">Next, run the Azure Import/Export Tool, specifying the path to that drive with the `/d` parameter.</span></span> <span data-ttu-id="b359f-160">È inoltre necessario specificare il percorso di file di log di copia dell'unità che è stato scaricato.</span><span class="sxs-lookup"><span data-stu-id="b359f-160">You also need to specify the path to the drive's copy log file that you downloaded.</span></span> <span data-ttu-id="b359f-161">Nell'esempio seguente, la riga di comando esegue lo strumento per recuperare eventuali file con errori di esportazione:</span><span class="sxs-lookup"><span data-stu-id="b359f-161">The following command line example below runs the tool to repair any files that failed to export:</span></span>  
  
```  
WAImportExport.exe RepairExport /r:C:\WAImportExport\9WM35C3U.rep /d:G:\ /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C3U.log  
```  
  
<span data-ttu-id="b359f-162">Di seguito è riportato un esempio di un file di log di copia che mostra un blocco nel BLOB con errori di esportazione:</span><span class="sxs-lookup"><span data-stu-id="b359f-162">The following is an example of a copy log file that shows that one block in the blob failed to export:</span></span>  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveLog>  
  <DriveId>9WM35C2V</DriveId>  
  <Blob Status="CompletedWithErrors">  
    <BlobPath>pictures/wild/desert.jpg</BlobPath>  
    <FilePath>\pictures\wild\desert.jpg</FilePath>  
    <LastModified>2012-09-18T23:47:08Z</LastModified>  
    <Length>163840</Length>  
    <BlockList>  
      <Block Offset="65536" Length="65536" Id="AQAAAA==" Status="Failed" />  
    </BlockList>  
  </Blob>  
  <Status>CompletedWithErrors</Status>  
</DriveLog>  
```  
  
<span data-ttu-id="b359f-163">Il file di log di copia indica che si è verificato un errore durante il download di uno dei blocchi del BLOB sul file nell'unità di esportazione da parte del servizio di Importazione/Esportazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="b359f-163">The copy log file indicates that a failure occurred while the Windows Azure Import/Export service was downloading one of the blob's blocks to the file on the export drive.</span></span> <span data-ttu-id="b359f-164">Gli altri componenti del file scaricato correttamente e la lunghezza del file sono stati impostati correttamente.</span><span class="sxs-lookup"><span data-stu-id="b359f-164">The other components of the file downloaded successfully, and the file length was correctly set.</span></span> <span data-ttu-id="b359f-165">In questo caso, lo strumento apre il file nell'unità, scarica il blocco dall'account di archiviazione e scrive sull'intervallo dei file a partire dall'offset 65536 con lunghezza 65536.</span><span class="sxs-lookup"><span data-stu-id="b359f-165">In this case, the tool will open the file on the drive, download the block from the storage account, and write it to the file range starting from offset 65536 with length 65536.</span></span>  
  
## <a name="using-repairexport-to-validate-drive-contents"></a><span data-ttu-id="b359f-166">Uso di RepairExport per convalidare i contenuti dell'unità</span><span class="sxs-lookup"><span data-stu-id="b359f-166">Using RepairExport to validate drive contents</span></span>  
<span data-ttu-id="b359f-167">È inoltre possibile utilizzare Importazione/Esportazione di Azure con l'opzione **RepairExport** per convalidare la correttezza del contenuto sull'unità.</span><span class="sxs-lookup"><span data-stu-id="b359f-167">You can also use Azure Import/Export with the **RepairExport** option to validate the contents on the drive are correct.</span></span> <span data-ttu-id="b359f-168">Il file manifesto in ogni unità di esportazione contiene MD5 per il contenuto dell'unità.</span><span class="sxs-lookup"><span data-stu-id="b359f-168">The manifest file on each export drive contains MD5s for the contents of the drive.</span></span>  
  
<span data-ttu-id="b359f-169">Il servizio di Importazione/Esportazione di Azure può inoltre salvare i file manifesto su un account di archiviazione durante il processo di esportazione.</span><span class="sxs-lookup"><span data-stu-id="b359f-169">The Azure Import/Export service can also save the manifest files to a storage account during the export process.</span></span> <span data-ttu-id="b359f-170">Il percorso del file manifesto è disponibile tramite l'operazione [Get Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) (Ottieni processo) al completamento del processo.</span><span class="sxs-lookup"><span data-stu-id="b359f-170">The location of the manifest files is available via the [Get Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation when the job has completed.</span></span> <span data-ttu-id="b359f-171">Per altre informazioni sul formato di un file manifesto dell'unità, vedere [Formato del file manifesto del servizio Importazione/Esportazione di Azure](storage-import-export-file-format-metadata-and-properties.md).</span><span class="sxs-lookup"><span data-stu-id="b359f-171">See [Import/Export service Manifest File Format](storage-import-export-file-format-metadata-and-properties.md) for more information about the format of a drive manifest file.</span></span>  
  
<span data-ttu-id="b359f-172">Nell'esempio seguente viene illustrato come eseguire lo strumento Importazione/Esportazione di Azure con i parametri **/ManifestFile** e **/CopyLogFile**:</span><span class="sxs-lookup"><span data-stu-id="b359f-172">The following example shows how to run the Azure Import/Export Tool with the **/ManifestFile** and **/CopyLogFile** parameters:</span></span>  
  
```  
WAImportExport.exe RepairExport /r:C:\WAImportExport\9WM35C3U.rep /d:G:\ /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C3U.log /ManifestFile:G:\9WM35C3U.manifest  
```  
  
<span data-ttu-id="b359f-173">Di seguito è riportato un esempio di file manifesto:</span><span class="sxs-lookup"><span data-stu-id="b359f-173">The following is an example of a manifest file:</span></span>  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveManifest Version="2011-10-01">  
  <Drive>  
    <DriveId>9WM35C3U</DriveId>  
    <ClientCreator>Windows Azure Import/Export service</ClientCreator>  
    <BlobList>
      <Blob>  
        <BlobPath>pictures/city/redmond.jpg</BlobPath>  
        <FilePath>\pictures\city\redmond.jpg</FilePath>  
        <Length>15360</Length>  
        <PageRangeList>  
          <PageRange Offset="0" Length="3584" Hash="72FC55ED9AFDD40A0C8D5C4193208416" />  
          <PageRange Offset="3584" Length="3584" Hash="68B28A561B73D1DA769D4C24AA427DB8" />  
          <PageRange Offset="7168" Length="512" Hash="F521DF2F50C46BC5F9EA9FB787A23EED" />  
        </PageRangeList>  
        <PropertiesPath Hash="E72A22EA959566066AD89E3B49020C0A">\pictures\city\redmond.jpg.properties</PropertiesPath>  
      </Blob>  
      <Blob>  
        <BlobPath>pictures/wild/canyon.jpg</BlobPath>  
        <FilePath>\pictures\wild\canyon.jpg</FilePath>  
        <Length>10884</Length>  
        <BlockList>  
          <Block Offset="0" Length="2721" Id="AAAAAA==" Hash="263DC9C4B99C2177769C5EBE04787037" />  
          <Block Offset="2721" Length="2721" Id="AQAAAA==" Hash="0C52BAE2CC20EFEC15CC1E3045517AA6" />  
          <Block Offset="5442" Length="2721" Id="AgAAAA==" Hash="73D1CB62CB426230C34C9F57B7148F10" />  
          <Block Offset="8163" Length="2721" Id="AwAAAA==" Hash="11210E665C5F8E7E4F136D053B243E6A" />  
        </BlockList>  
        <PropertiesPath Hash="81D7F81B2C29F10D6E123D386C3A4D5A">\pictures\wild\canyon.jpg.properties</PropertiesPath>  
      </Blob> 
    </BlobList>  
 </Drive>  
</DriveManifest>  
``` 
  
<span data-ttu-id="b359f-174">Dopo aver completato il processo di ripristino, lo strumento leggerà ciascun file a cui fa riferimento nel file manifesto e verificare l'integrità del file con gli hash MD5.</span><span class="sxs-lookup"><span data-stu-id="b359f-174">After finishing the repair process, the tool will read through each file referenced in the manifest file and verify the file's integrity with the MD5 hashes.</span></span> <span data-ttu-id="b359f-175">Per il file manifesto di cui sopra, analizzerà i componenti seguenti.</span><span class="sxs-lookup"><span data-stu-id="b359f-175">For the manifest above, it will go through the following components.</span></span>  

```  
G:\pictures\city\redmond.jpg, offset 0, length 3584  
  
G:\pictures\city\redmond.jpg, offset 3584, length 3584  
  
G:\pictures\city\redmond.jpg, offset 7168, length 3584  
  
G:\pictures\city\redmond.jpg.properties  
  
G:\pictures\wild\canyon.jpg, offset 0, length 2721  
  
G:\pictures\wild\canyon.jpg, offset 2721, length 2721  
  
G:\pictures\wild\canyon.jpg, offset 5442, length 2721  
  
G:\pictures\wild\canyon.jpg, offset 8163, length 2721  
  
G:\pictures\wild\canyon.jpg.properties  
```

<span data-ttu-id="b359f-176">Qualsiasi componente con esito negativo della verifica verrà scaricato dallo strumento e riscritto nello stesso file sull'unità.</span><span class="sxs-lookup"><span data-stu-id="b359f-176">Any component failing the verification will be downloaded by the tool and rewritten to the same file on the drive.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="b359f-177">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b359f-177">Next steps</span></span>
 
* [<span data-ttu-id="b359f-178">Configurazione dello strumento Importazione/Esportazione di Azure</span><span class="sxs-lookup"><span data-stu-id="b359f-178">Setting Up the Azure Import/Export Tool</span></span>](storage-import-export-tool-setup-v1.md)   
* <span data-ttu-id="b359f-179">[Preparing hard drives for an import job](../storage-import-export-tool-preparing-hard-drives-import-v1.md) (Preparazione dei dischi rigidi per un processo di importazione)</span><span class="sxs-lookup"><span data-stu-id="b359f-179">[Preparing hard drives for an import job](../storage-import-export-tool-preparing-hard-drives-import-v1.md)</span></span>   
* <span data-ttu-id="b359f-180">[Reviewing job status with copy log files](storage-import-export-tool-reviewing-job-status-v1.md) (Revisione dello stato dei processi con i file di log di copia)</span><span class="sxs-lookup"><span data-stu-id="b359f-180">[Reviewing job status with copy log files](storage-import-export-tool-reviewing-job-status-v1.md)</span></span>   
* <span data-ttu-id="b359f-181">[Repairing an import job](storage-import-export-tool-repairing-an-import-job-v1.md) (Riparazione di un processo di importazione)</span><span class="sxs-lookup"><span data-stu-id="b359f-181">[Repairing an import job](storage-import-export-tool-repairing-an-import-job-v1.md)</span></span>   
* [<span data-ttu-id="b359f-182">Risoluzione dei problemi relativi allo strumento Importazione/Esportazione di Azure</span><span class="sxs-lookup"><span data-stu-id="b359f-182">Troubleshooting the Azure Import/Export Tool</span></span>](storage-import-export-tool-troubleshooting-v1.md)
