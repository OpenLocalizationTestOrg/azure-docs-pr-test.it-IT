---
title: un processo di esportazione di importazione/esportazione di Azure - v1 aaaRepairing | Documenti Microsoft
description: "Informazioni su come un processo di esportazione che è stato creato ed eseguito con toorepair hello importazione/esportazione di Azure service."
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
ms.openlocfilehash: e54bc66495c8a3473b8ec51bb254bce8bdc9eab9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="repairing-an-export-job"></a><span data-ttu-id="0c0d5-103">Riparazione di un processo di esportazione</span><span class="sxs-lookup"><span data-stu-id="0c0d5-103">Repairing an export job</span></span>
<span data-ttu-id="0c0d5-104">Al termine di un processo di esportazione, è possibile eseguire hello dello strumento di importazione/esportazione di Microsoft Azure da sito locale:</span><span class="sxs-lookup"><span data-stu-id="0c0d5-104">After an export job has completed, you can run hello Microsoft Azure Import/Export Tool on-premises to:</span></span>  
  
1.  <span data-ttu-id="0c0d5-105">Scaricare i file che il servizio di importazione/esportazione di Azure hello è stato Impossibile tooexport.</span><span class="sxs-lookup"><span data-stu-id="0c0d5-105">Download any files that hello Azure Import/Export service was unable tooexport.</span></span>  
  
2.  <span data-ttu-id="0c0d5-106">Verificare che i file hello hello unità siano stati esportati correttamente.</span><span class="sxs-lookup"><span data-stu-id="0c0d5-106">Validate that hello files on hello drive were correctly exported.</span></span>  
  
<span data-ttu-id="0c0d5-107">È necessario disporre della connettività tooAzure archiviazione toouse questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="0c0d5-107">You must have connectivity tooAzure Storage toouse this functionality.</span></span>  
  
<span data-ttu-id="0c0d5-108">comando Hello per il ripristino di un processo di importazione è **RepairExport**.</span><span class="sxs-lookup"><span data-stu-id="0c0d5-108">hello command for repairing an import job is **RepairExport**.</span></span>

## <a name="repairexport-parameters"></a><span data-ttu-id="0c0d5-109">Parametri di RepairExport</span><span class="sxs-lookup"><span data-stu-id="0c0d5-109">RepairExport parameters</span></span>

<span data-ttu-id="0c0d5-110">Hello seguenti parametri possono essere specificati con **RepairExport**:</span><span class="sxs-lookup"><span data-stu-id="0c0d5-110">hello following parameters can be specified with **RepairExport**:</span></span>  
  
|<span data-ttu-id="0c0d5-111">.</span><span class="sxs-lookup"><span data-stu-id="0c0d5-111">Parameter</span></span>|<span data-ttu-id="0c0d5-112">Descrizione</span><span class="sxs-lookup"><span data-stu-id="0c0d5-112">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="0c0d5-113">**/r:<RepairFile\>**</span><span class="sxs-lookup"><span data-stu-id="0c0d5-113">**/r:<RepairFile\>**</span></span>|<span data-ttu-id="0c0d5-114">Obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="0c0d5-114">Required.</span></span> <span data-ttu-id="0c0d5-115">File di correzione toohello percorso, che tiene traccia dell'avanzamento hello di correzione hello e consente un ripristino interrotto tooresume.</span><span class="sxs-lookup"><span data-stu-id="0c0d5-115">Path toohello repair file, which tracks hello progress of hello repair, and allows you tooresume an interrupted repair.</span></span> <span data-ttu-id="0c0d5-116">Ogni unità deve contenere un solo file di ripristino.</span><span class="sxs-lookup"><span data-stu-id="0c0d5-116">Each drive must have one and only one repair file.</span></span> <span data-ttu-id="0c0d5-117">Quando si avvia un ripristino per una determinata unità, verrà passato in hello percorso tooa file di ripristino non esiste ancora.</span><span class="sxs-lookup"><span data-stu-id="0c0d5-117">When you start a repair for a given drive, you will pass in hello path tooa repair file which does not yet exist.</span></span> <span data-ttu-id="0c0d5-118">tooresume un ripristino interrotto, è necessario passare nel nome hello di un file di ripristino esistente.</span><span class="sxs-lookup"><span data-stu-id="0c0d5-118">tooresume an interrupted repair, you should pass in hello name of an existing repair file.</span></span> <span data-ttu-id="0c0d5-119">è necessario specificare sempre Hello Ripristina file corrispondente toohello unità di destinazione.</span><span class="sxs-lookup"><span data-stu-id="0c0d5-119">hello repair file corresponding toohello target drive must always be specified.</span></span>|  
|<span data-ttu-id="0c0d5-120">**/logdir:&lt;LogDirectory\>**</span><span class="sxs-lookup"><span data-stu-id="0c0d5-120">**/logdir:<LogDirectory\>**</span></span>|<span data-ttu-id="0c0d5-121">Facoltativo.</span><span class="sxs-lookup"><span data-stu-id="0c0d5-121">Optional.</span></span> <span data-ttu-id="0c0d5-122">directory dei log Hello.</span><span class="sxs-lookup"><span data-stu-id="0c0d5-122">hello log directory.</span></span> <span data-ttu-id="0c0d5-123">File di log dettagliati verranno scritti toothis directory.</span><span class="sxs-lookup"><span data-stu-id="0c0d5-123">Verbose log files will be written toothis directory.</span></span> <span data-ttu-id="0c0d5-124">Se non viene specificata alcuna directory di log, la directory corrente hello da utilizzare come directory dei log hello.</span><span class="sxs-lookup"><span data-stu-id="0c0d5-124">If no log directory is specified, hello current directory will be used as hello log directory.</span></span>|  
|<span data-ttu-id="0c0d5-125">**/d:&lt;TargetDirectory\>**</span><span class="sxs-lookup"><span data-stu-id="0c0d5-125">**/d:<TargetDirectory\>**</span></span>|<span data-ttu-id="0c0d5-126">Obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="0c0d5-126">Required.</span></span> <span data-ttu-id="0c0d5-127">Hello directory toovalidate e il ripristino.</span><span class="sxs-lookup"><span data-stu-id="0c0d5-127">hello directory toovalidate and repair.</span></span> <span data-ttu-id="0c0d5-128">Si tratta in genere directory radice di hello dell'unità di esportazione di hello, ma potrebbe anche essere una condivisione di file di rete contenente una copia dei file hello esportata.</span><span class="sxs-lookup"><span data-stu-id="0c0d5-128">This is usually hello root directory of hello export drive, but could also be a network file share containing a copy of hello exported files.</span></span>|  
|<span data-ttu-id="0c0d5-129">**/bk:<BitLockerKey\>**</span><span class="sxs-lookup"><span data-stu-id="0c0d5-129">**/bk:<BitLockerKey\>**</span></span>|<span data-ttu-id="0c0d5-130">Facoltativo.</span><span class="sxs-lookup"><span data-stu-id="0c0d5-130">Optional.</span></span> <span data-ttu-id="0c0d5-131">Specificare la chiave di BitLocker hello se si desidera toounlock strumento hello vengono archiviati in cui i file esportati hello crittografato.</span><span class="sxs-lookup"><span data-stu-id="0c0d5-131">You should specify hello BitLocker key if you want hello tool toounlock an encrypted where hello exported files are stored.</span></span>|  
|<span data-ttu-id="0c0d5-132">**/sn:&lt;StorageAccountName\>**</span><span class="sxs-lookup"><span data-stu-id="0c0d5-132">**/sn:<StorageAccountName\>**</span></span>|<span data-ttu-id="0c0d5-133">Obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="0c0d5-133">Required.</span></span> <span data-ttu-id="0c0d5-134">processo di esportazione nome Hello hello dell'account di archiviazione per hello.</span><span class="sxs-lookup"><span data-stu-id="0c0d5-134">hello name of hello storage account for hello export job.</span></span>|  
|<span data-ttu-id="0c0d5-135">**/sk:<StorageAccountKey\>**</span><span class="sxs-lookup"><span data-stu-id="0c0d5-135">**/sk:<StorageAccountKey\>**</span></span>|<span data-ttu-id="0c0d5-136">**Obbligatorio** solo se non è specificata una firma di accesso condiviso del contenitore.</span><span class="sxs-lookup"><span data-stu-id="0c0d5-136">**Required** if and only if a container SAS is not specified.</span></span> <span data-ttu-id="0c0d5-137">processo di esportazione chiave Hello per l'account di archiviazione hello per hello.</span><span class="sxs-lookup"><span data-stu-id="0c0d5-137">hello account key for hello storage account for hello export job.</span></span>|  
|<span data-ttu-id="0c0d5-138">**/csas:<ContainerSas\>**</span><span class="sxs-lookup"><span data-stu-id="0c0d5-138">**/csas:<ContainerSas\>**</span></span>|<span data-ttu-id="0c0d5-139">**Richiesto** se e solo se chiave dell'account di archiviazione hello non è specificato.</span><span class="sxs-lookup"><span data-stu-id="0c0d5-139">**Required** if and only if hello storage account key is not specified.</span></span> <span data-ttu-id="0c0d5-140">contenitore di Hello SAS per accedere agli oggetti BLOB hello associato al processo di esportazione hello.</span><span class="sxs-lookup"><span data-stu-id="0c0d5-140">hello container SAS for accessing hello blobs associated with hello export job.</span></span>|  
|<span data-ttu-id="0c0d5-141">**/CopyLogFile:\><DriveCopyLogFile**</span><span class="sxs-lookup"><span data-stu-id="0c0d5-141">**/CopyLogFile:<DriveCopyLogFile\>**</span></span>|<span data-ttu-id="0c0d5-142">Obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="0c0d5-142">Required.</span></span> <span data-ttu-id="0c0d5-143">Hello percorso toohello unità Copia file di log.</span><span class="sxs-lookup"><span data-stu-id="0c0d5-143">hello path toohello drive copy log file.</span></span> <span data-ttu-id="0c0d5-144">file Hello viene generato dal servizio di importazione/esportazione di Azure hello e può essere scaricato dall'archiviazione blob hello associata al processo hello.</span><span class="sxs-lookup"><span data-stu-id="0c0d5-144">hello file is generated by hello Windows Azure Import/Export service and can be downloaded from hello blob storage associated with hello job.</span></span> <span data-ttu-id="0c0d5-145">file di log di copia Hello contiene informazioni sui blob non riuscito o i file che sono toobe riparato.</span><span class="sxs-lookup"><span data-stu-id="0c0d5-145">hello copy log file contains information about failed blobs or files which are toobe repaired.</span></span>|  
|<span data-ttu-id="0c0d5-146">**/ManifestFile:<DriveManifestFile\>**</span><span class="sxs-lookup"><span data-stu-id="0c0d5-146">**/ManifestFile:<DriveManifestFile\>**</span></span>|<span data-ttu-id="0c0d5-147">Facoltativo.</span><span class="sxs-lookup"><span data-stu-id="0c0d5-147">Optional.</span></span> <span data-ttu-id="0c0d5-148">file manifesto dell'unità di Hello percorso toohello esportazione.</span><span class="sxs-lookup"><span data-stu-id="0c0d5-148">hello path toohello export drive's manifest file.</span></span> <span data-ttu-id="0c0d5-149">Questo file è generato dal servizio di importazione/esportazione di Azure hello e archiviato nell'unità di esportazione hello e, facoltativamente in un blob nell'account di archiviazione hello associata al processo hello.</span><span class="sxs-lookup"><span data-stu-id="0c0d5-149">This file is generated by hello Windows Azure Import/Export service and stored on hello export drive, and optionally in a blob in hello storage account associated with hello job.</span></span><br /><br /> <span data-ttu-id="0c0d5-150">Hello contenuto del file nell'unità di esportazione hello verranno verificati con hash MD5 hello contenute nel file hello.</span><span class="sxs-lookup"><span data-stu-id="0c0d5-150">hello content of hello files on hello export drive will be verified with hello MD5 hashes contained in this file.</span></span> <span data-ttu-id="0c0d5-151">Tutti i file toobe determinato danneggiato verrà scaricato e riscritto toohello directory di destinazione.</span><span class="sxs-lookup"><span data-stu-id="0c0d5-151">Any files that are determined toobe corrupted will be downloaded and rewritten toohello target directories.</span></span>|  
  
## <a name="using-repairexport-mode-toocorrect-failed-exports"></a><span data-ttu-id="0c0d5-152">Utilizzo di RepairExport toocorrect modalità esportazioni non riuscita</span><span class="sxs-lookup"><span data-stu-id="0c0d5-152">Using RepairExport mode toocorrect failed exports</span></span>  
<span data-ttu-id="0c0d5-153">È possibile utilizzare i file toodownload hello strumento di importazione/esportazione di Azure che non è stato possibile tooexport.</span><span class="sxs-lookup"><span data-stu-id="0c0d5-153">You can use hello Azure Import/Export Tool toodownload files that failed tooexport.</span></span> <span data-ttu-id="0c0d5-154">file di log di copia Hello conterrà un elenco di file che non è stato possibile tooexport.</span><span class="sxs-lookup"><span data-stu-id="0c0d5-154">hello copy log file will contain a list of files that failed tooexport.</span></span>  
  
<span data-ttu-id="0c0d5-155">le cause degli errori nelle esportazioni Hello includono hello le possibilità seguenti:</span><span class="sxs-lookup"><span data-stu-id="0c0d5-155">hello causes of export failures include hello following possibilities:</span></span>  
  
-   <span data-ttu-id="0c0d5-156">Unità danneggiate</span><span class="sxs-lookup"><span data-stu-id="0c0d5-156">Damaged drives</span></span>  
  
-   <span data-ttu-id="0c0d5-157">chiave dell'account di archiviazione Hello modificato durante il processo di trasferimento hello</span><span class="sxs-lookup"><span data-stu-id="0c0d5-157">hello storage account key changed during hello transfer process</span></span>  
  
<span data-ttu-id="0c0d5-158">strumento hello toorun **RepairExport** modalità, è innanzitutto necessario tooconnect hello unità contenente hello file esportati tooyour computer.</span><span class="sxs-lookup"><span data-stu-id="0c0d5-158">toorun hello tool in **RepairExport** mode, you first need tooconnect hello drive containing hello exported files tooyour computer.</span></span> <span data-ttu-id="0c0d5-159">Successivamente, eseguire lo strumento di importazione/esportazione di Azure, specifica di hello percorso toothat unità con hello hello `/d` parametro.</span><span class="sxs-lookup"><span data-stu-id="0c0d5-159">Next, run hello Azure Import/Export Tool, specifying hello path toothat drive with hello `/d` parameter.</span></span> <span data-ttu-id="0c0d5-160">È necessario anche file di log di copia dell'unità di toospecify hello percorso toohello che è stato scaricato.</span><span class="sxs-lookup"><span data-stu-id="0c0d5-160">You also need toospecify hello path toohello drive's copy log file that you downloaded.</span></span> <span data-ttu-id="0c0d5-161">Hello seguente esempio di riga di comando seguente esegue hello strumento toorepair eventuali file non tooexport:</span><span class="sxs-lookup"><span data-stu-id="0c0d5-161">hello following command line example below runs hello tool toorepair any files that failed tooexport:</span></span>  
  
```  
WAImportExport.exe RepairExport /r:C:\WAImportExport\9WM35C3U.rep /d:G:\ /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C3U.log  
```  
  
<span data-ttu-id="0c0d5-162">Hello Ecco un esempio di un file di log di copia che mostra un blocco in hello tooexport di blob non riuscita:</span><span class="sxs-lookup"><span data-stu-id="0c0d5-162">hello following is an example of a copy log file that shows that one block in hello blob failed tooexport:</span></span>  
  
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
  
<span data-ttu-id="0c0d5-163">file di log di copia Hello indica che si è verificato un errore durante uno dei file toohello di blocchi del blob hello nell'unità di esportazione hello download hello servizio importazione/esportazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="0c0d5-163">hello copy log file indicates that a failure occurred while hello Windows Azure Import/Export service was downloading one of hello blob's blocks toohello file on hello export drive.</span></span> <span data-ttu-id="0c0d5-164">altri componenti del file hello scaricato correttamente Hello e lunghezza del file hello è stata impostata correttamente.</span><span class="sxs-lookup"><span data-stu-id="0c0d5-164">hello other components of hello file downloaded successfully, and hello file length was correctly set.</span></span> <span data-ttu-id="0c0d5-165">In questo caso, alla quale strumento hello aprire file hello in unità hello, scaricare blocco hello dall'account di archiviazione hello e scriverlo toohello intervallo del file a partire dall'offset 65536 con lunghezza 65536.</span><span class="sxs-lookup"><span data-stu-id="0c0d5-165">In this case, hello tool will open hello file on hello drive, download hello block from hello storage account, and write it toohello file range starting from offset 65536 with length 65536.</span></span>  
  
## <a name="using-repairexport-toovalidate-drive-contents"></a><span data-ttu-id="0c0d5-166">Utilizzo di RepairExport toovalidate contenuti dell'unità</span><span class="sxs-lookup"><span data-stu-id="0c0d5-166">Using RepairExport toovalidate drive contents</span></span>  
<span data-ttu-id="0c0d5-167">È inoltre possibile utilizzare importazione/esportazione di Azure con hello **RepairExport** opzione toovalidate hello contenuto unità hello siano corretto.</span><span class="sxs-lookup"><span data-stu-id="0c0d5-167">You can also use Azure Import/Export with hello **RepairExport** option toovalidate hello contents on hello drive are correct.</span></span> <span data-ttu-id="0c0d5-168">file manifesto di Hello in ogni unità di esportazione contiene MD5s per il contenuto dell'unità hello hello.</span><span class="sxs-lookup"><span data-stu-id="0c0d5-168">hello manifest file on each export drive contains MD5s for hello contents of hello drive.</span></span>  
  
<span data-ttu-id="0c0d5-169">Hello servizio importazione/esportazione di Azure inoltre possibile salvare i file manifesto hello tooa account di archiviazione durante il processo di esportazione hello.</span><span class="sxs-lookup"><span data-stu-id="0c0d5-169">hello Azure Import/Export service can also save hello manifest files tooa storage account during hello export process.</span></span> <span data-ttu-id="0c0d5-170">Hello percorso dei file manifesto hello è disponibile tramite hello [recupero del processo](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operazione quando il processo di hello è stata completata.</span><span class="sxs-lookup"><span data-stu-id="0c0d5-170">hello location of hello manifest files is available via hello [Get Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation when hello job has completed.</span></span> <span data-ttu-id="0c0d5-171">Vedere [formato del File manifesto del servizio di importazione/esportazione](storage-import-export-file-format-metadata-and-properties.md) per ulteriori informazioni sul formato hello di un file manifesto dell'unità.</span><span class="sxs-lookup"><span data-stu-id="0c0d5-171">See [Import/Export service Manifest File Format](storage-import-export-file-format-metadata-and-properties.md) for more information about hello format of a drive manifest file.</span></span>  
  
<span data-ttu-id="0c0d5-172">Hello esempio seguente viene illustrato come toorun hello strumento di importazione/esportazione di Azure con hello **/ManifestFile** e **/CopyLogFile** parametri:</span><span class="sxs-lookup"><span data-stu-id="0c0d5-172">hello following example shows how toorun hello Azure Import/Export Tool with hello **/ManifestFile** and **/CopyLogFile** parameters:</span></span>  
  
```  
WAImportExport.exe RepairExport /r:C:\WAImportExport\9WM35C3U.rep /d:G:\ /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C3U.log /ManifestFile:G:\9WM35C3U.manifest  
```  
  
<span data-ttu-id="0c0d5-173">Hello Ecco un esempio di un file manifesto:</span><span class="sxs-lookup"><span data-stu-id="0c0d5-173">hello following is an example of a manifest file:</span></span>  
  
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
  
<span data-ttu-id="0c0d5-174">Dopo il processo di ripristino di completamento hello, hello strumento leggerà ciascun file a cui fa riferimento nel file manifesto hello e verificare l'integrità del file hello con hash MD5 hello.</span><span class="sxs-lookup"><span data-stu-id="0c0d5-174">After finishing hello repair process, hello tool will read through each file referenced in hello manifest file and verify hello file's integrity with hello MD5 hashes.</span></span> <span data-ttu-id="0c0d5-175">Per il manifesto hello sopra, analizzerà hello seguenti componenti.</span><span class="sxs-lookup"><span data-stu-id="0c0d5-175">For hello manifest above, it will go through hello following components.</span></span>  

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

<span data-ttu-id="0c0d5-176">Qualsiasi componente mancata verifica hello verrà scaricati dallo strumento hello e riscritti toohello lo stesso file nell'unità di hello.</span><span class="sxs-lookup"><span data-stu-id="0c0d5-176">Any component failing hello verification will be downloaded by hello tool and rewritten toohello same file on hello drive.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="0c0d5-177">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0c0d5-177">Next steps</span></span>
 
* [<span data-ttu-id="0c0d5-178">Impostazione hello strumento di importazione/esportazione di Azure</span><span class="sxs-lookup"><span data-stu-id="0c0d5-178">Setting Up hello Azure Import/Export Tool</span></span>](storage-import-export-tool-setup-v1.md)   
* <span data-ttu-id="0c0d5-179">[Preparing hard drives for an import job](../storage-import-export-tool-preparing-hard-drives-import-v1.md) (Preparazione dei dischi rigidi per un processo di importazione)</span><span class="sxs-lookup"><span data-stu-id="0c0d5-179">[Preparing hard drives for an import job](../storage-import-export-tool-preparing-hard-drives-import-v1.md)</span></span>   
* <span data-ttu-id="0c0d5-180">[Reviewing job status with copy log files](storage-import-export-tool-reviewing-job-status-v1.md) (Revisione dello stato dei processi con i file di log di copia)</span><span class="sxs-lookup"><span data-stu-id="0c0d5-180">[Reviewing job status with copy log files](storage-import-export-tool-reviewing-job-status-v1.md)</span></span>   
* [<span data-ttu-id="0c0d5-181">Riparazione di un processo di importazione</span><span class="sxs-lookup"><span data-stu-id="0c0d5-181">Repairing an import job</span></span>](storage-import-export-tool-repairing-an-import-job-v1.md)   
* [<span data-ttu-id="0c0d5-182">Risoluzione dei problemi hello strumento di importazione/esportazione di Azure</span><span class="sxs-lookup"><span data-stu-id="0c0d5-182">Troubleshooting hello Azure Import/Export Tool</span></span>](storage-import-export-tool-troubleshooting-v1.md)
