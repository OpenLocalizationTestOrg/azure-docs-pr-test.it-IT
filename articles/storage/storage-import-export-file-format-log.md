---
title: Formato dei file di log del servizio Importazione/Esportazione | Documentazione Microsoft
description: Altre informazioni sul formato dei file di log creati quando vengono eseguiti i passaggi per un processo del servizio Importazione/Esportazione.
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
ms.openlocfilehash: 16234ccaf13ce1d85cfd207ed4734e683070faa6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-importexport-service-log-file-format"></a><span data-ttu-id="a75dd-103">Formato dei file di log del servizio Importazione/Esportazione di Azure</span><span class="sxs-lookup"><span data-stu-id="a75dd-103">Azure Import/Export service log file format</span></span>
<span data-ttu-id="a75dd-104">Quando il servizio Importazione/Esportazione di Microsoft Azure esegue un'azione in un'unità come parte di un processo di importazione o di esportazione, i log vengono scritti in BLOB in blocchi nell'account di archiviazione associato a tale processo.</span><span class="sxs-lookup"><span data-stu-id="a75dd-104">When the Microsoft Azure Import/Export service performs an action on a drive as part of an import job or an export job, logs are written to block blobs in the storage account associated with that job.</span></span>  
  
<span data-ttu-id="a75dd-105">Esistono due log che possono essere scritti dal servizio Importazione/Esportazione:</span><span class="sxs-lookup"><span data-stu-id="a75dd-105">There are two logs that may be written by the Import/Export service:</span></span>  
  
-   <span data-ttu-id="a75dd-106">Il log degli errori viene sempre generato in caso di errore.</span><span class="sxs-lookup"><span data-stu-id="a75dd-106">The error log is always generated in the event of an error.</span></span>  
  
-   <span data-ttu-id="a75dd-107">Il log dettagliato non è abilitato per impostazione predefinita, ma può essere abilitato impostando la proprietà `EnableVerboseLog` in un'operazione di tipo [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) o [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update).</span><span class="sxs-lookup"><span data-stu-id="a75dd-107">The verbose log is not enabled by default, but may be enabled by setting the `EnableVerboseLog` property on a [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) or [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operation.</span></span>  
  
## <a name="log-file-location"></a><span data-ttu-id="a75dd-108">Posizione dei file di log</span><span class="sxs-lookup"><span data-stu-id="a75dd-108">Log file location</span></span>  
<span data-ttu-id="a75dd-109">I log vengono scritti in BLOB in blocchi nel contenitore o nella directory virtuale specificata tramite l'impostazione `ImportExportStatesPath`, che è possibile impostare in un'operazione di tipo `Put Job`.</span><span class="sxs-lookup"><span data-stu-id="a75dd-109">The logs are written to block blobs in the container or virtual directory specified by the `ImportExportStatesPath` setting, which you can set on a `Put Job` operation.</span></span> <span data-ttu-id="a75dd-110">La posizione in cui vengono scritti i log dipende da come viene specificata l'autenticazione per il processo e dal valore specificato per `ImportExportStatesPath`.</span><span class="sxs-lookup"><span data-stu-id="a75dd-110">The location to which the logs are written depends on how authentication is specified for the job, together with the value specified for `ImportExportStatesPath`.</span></span> <span data-ttu-id="a75dd-111">L'autenticazione per il processo può essere specificata tramite una chiave dell'account di archiviazione o la firma di accesso condiviso di un contenitore.</span><span class="sxs-lookup"><span data-stu-id="a75dd-111">Authentication for the job may be specified via a storage account key, or a container SAS (shared access signature).</span></span>  
  
<span data-ttu-id="a75dd-112">Il nome del contenitore o della directory virtuale può essere il nome predefinito di `waimportexport` oppure il nome di un altro contenitore o di un'altra directory virtuale specificato dall'utente.</span><span class="sxs-lookup"><span data-stu-id="a75dd-112">The name of the container or virtual directory may either be the default name of `waimportexport`, or another container or virtual directory name that you specify.</span></span>  
  
<span data-ttu-id="a75dd-113">Nella tabella seguente vengono illustrate le opzioni possibili:</span><span class="sxs-lookup"><span data-stu-id="a75dd-113">The table below shows the possible options:</span></span>  
  
|<span data-ttu-id="a75dd-114">Metodo di autenticazione</span><span class="sxs-lookup"><span data-stu-id="a75dd-114">Authentication Method</span></span>|<span data-ttu-id="a75dd-115">Valore dell'elemento `ImportExportStatesPath`</span><span class="sxs-lookup"><span data-stu-id="a75dd-115">Value of `ImportExportStatesPath`Element</span></span>|<span data-ttu-id="a75dd-116">Posizione dei BLOB di log</span><span class="sxs-lookup"><span data-stu-id="a75dd-116">Location of Log Blobs</span></span>|  
|---------------------------|----------------------------------------------|---------------------------|  
|<span data-ttu-id="a75dd-117">Chiave dell'account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="a75dd-117">Storage account key</span></span>|<span data-ttu-id="a75dd-118">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="a75dd-118">Default value</span></span>|<span data-ttu-id="a75dd-119">Un contenitore denominato `waimportexport`, ovvero il contenitore predefinito.</span><span class="sxs-lookup"><span data-stu-id="a75dd-119">A container named `waimportexport`, which is the default container.</span></span> <span data-ttu-id="a75dd-120">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="a75dd-120">For example:</span></span><br /><br /> `https://myaccount.blob.core.windows.net/waimportexport`|  
|<span data-ttu-id="a75dd-121">Chiave dell'account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="a75dd-121">Storage account key</span></span>|<span data-ttu-id="a75dd-122">Valore specificato dall'utente</span><span class="sxs-lookup"><span data-stu-id="a75dd-122">User-specified value</span></span>|<span data-ttu-id="a75dd-123">Un contenitore denominato dall'utente.</span><span class="sxs-lookup"><span data-stu-id="a75dd-123">A container named by the user.</span></span> <span data-ttu-id="a75dd-124">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="a75dd-124">For example:</span></span><br /><br /> `https://myaccount.blob.core.windows.net/mylogcontainer`|  
|<span data-ttu-id="a75dd-125">Firma di accesso condiviso del contenitore</span><span class="sxs-lookup"><span data-stu-id="a75dd-125">Container SAS</span></span>|<span data-ttu-id="a75dd-126">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="a75dd-126">Default value</span></span>|<span data-ttu-id="a75dd-127">Una directory virtuale denominata `waimportexport`, ovvero il nome predefinito, sotto il contenitore specificato nella firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="a75dd-127">A virtual directory named `waimportexport`, which is the default name, beneath the container specified in the SAS.</span></span><br /><br /> <span data-ttu-id="a75dd-128">Ad esempio, se la firma di accesso condiviso specificata per il processo è `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, la posizione del log sarà `https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport`</span><span class="sxs-lookup"><span data-stu-id="a75dd-128">For example, if the SAS specified for the job is  `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, then the log location would be `https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport`</span></span>|  
|<span data-ttu-id="a75dd-129">Firma di accesso condiviso del contenitore</span><span class="sxs-lookup"><span data-stu-id="a75dd-129">Container SAS</span></span>|<span data-ttu-id="a75dd-130">Valore specificato dall'utente</span><span class="sxs-lookup"><span data-stu-id="a75dd-130">User-specified value</span></span>|<span data-ttu-id="a75dd-131">Una directory virtuale denominata dall'utente, sotto il contenitore specificato nella firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="a75dd-131">A virtual directory named by the user, beneath the container specified in the SAS.</span></span><br /><br /> <span data-ttu-id="a75dd-132">Ad esempio, se la firma di accesso condiviso specificata per il processo è `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue` e la directory virtuale specificata è denominata `mylogblobs`, la posizione del log sarà `https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport/mylogblobs`.</span><span class="sxs-lookup"><span data-stu-id="a75dd-132">For example, if the SAS specified for the job is  `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, and the specified virtual directory is named `mylogblobs`, then the log location would be `https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport/mylogblobs`.</span></span>|  
  
<span data-ttu-id="a75dd-133">È possibile recuperare l'URL per l'errore e i log dettagliati chiamando l'operazione [Get Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate).</span><span class="sxs-lookup"><span data-stu-id="a75dd-133">You can retrieve the URL for the error and verbose logs by calling the [Get Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span></span> <span data-ttu-id="a75dd-134">I log sono disponibili al termine dell'elaborazione dell'unità.</span><span class="sxs-lookup"><span data-stu-id="a75dd-134">The logs are available after processing of the drive is complete.</span></span>  
  
## <a name="log-file-format"></a><span data-ttu-id="a75dd-135">Formato di file dei log</span><span class="sxs-lookup"><span data-stu-id="a75dd-135">Log file format</span></span>  
<span data-ttu-id="a75dd-136">Il formato è lo stesso per entrambi i log: un BLOB che contiene le descrizioni XML degli eventi che si sono verificati durante la copia dei BLOB tra il disco rigido e l'account del cliente.</span><span class="sxs-lookup"><span data-stu-id="a75dd-136">The format for both logs is the same: a blob containing XML descriptions of the events that occurred while copying blobs between the hard drive and the customer's account.</span></span>  
  
<span data-ttu-id="a75dd-137">Il log dettagliato contiene informazioni complete sullo stato dell'operazione di copia per ogni BLOB (per un processo di importazione) o file (per un processo di esportazione), mentre il log degli errori contiene solo le informazioni per i BLOB o i file che hanno rilevato errori durante il processo di importazione o esportazione.</span><span class="sxs-lookup"><span data-stu-id="a75dd-137">The verbose log contains complete information about the status of the copy operation for every blob (for an import job) or file (for an export job), whereas the error log contains only the information for blobs or files that encountered errors during the import or export job.</span></span>  
  
<span data-ttu-id="a75dd-138">Di seguito è mostrato il formato di log dettagliato.</span><span class="sxs-lookup"><span data-stu-id="a75dd-138">The verbose log format is shown below.</span></span> <span data-ttu-id="a75dd-139">Il log degli errori presenta la stessa struttura, ma esclude le operazioni riuscite.</span><span class="sxs-lookup"><span data-stu-id="a75dd-139">The error log has the same structure, but filters out successful operations.</span></span>  

```xml
<DriveLog Version="2014-11-01">  
  <DriveId>drive-id</DriveId>  
  [<Blob Status="blob-status">  
   <BlobPath>blob-path</BlobPath>  
   <FilePath>file-path</FilePath>  
   [<Snapshot>snapshot</Snapshot>]  
   <Length>length</Length>  
   [<LastModified>last-modified</LastModified>]  
   [<ImportDisposition Status="import-disposition-status">import-disposition</ImportDisposition>]  
   [page-range-list-or-block-list]  
   [metadata-status]  
   [properties-status]  
  </Blob>]  
  [<Blob>  
    . . .  
  </Blob>]  
  <Status>drive-status</Status>  
</DriveLog>  
  
page-range-list-or-block-list ::= 
  page-range-list | block-list  
  
page-range-list ::=   
<PageRangeList>  
      [<PageRange Offset="page-range-offset" Length="page-range-length"   
       [Hash="md5-hash"] Status="page-range-status"/>]  
      [<PageRange Offset="page-range-offset" Length="page-range-length"   
       [Hash="md5-hash"] Status="page-range-status"/>]  
</PageRangeList>  
  
block-list ::=  
<BlockList>  
      [<Block Offset="block-offset" Length="block-length" [Id="block-id"]  
       [Hash="md5-hash"] Status="block-status"/>]  
      [<Block Offset="block-offset" Length="block-length" [Id="block-id"]   
       [Hash="md5-hash"] Status="block-status"/>]  
</BlockList>  
  
metadata-status ::=  
<Metadata Status="metadata-status">  
   [<GlobalPath Hash="md5-hash">global-metadata-file-path</GlobalPath>]  
   [<Path Hash="md5-hash">metadata-file-path</Path>]  
</Metadata>  
  
properties-status ::=  
<Properties Status="properties-status">  
   [<GlobalPath Hash="md5-hash">global-properties-file-path</GlobalPath>]  
   [<Path Hash="md5-hash">properties-file-path</Path>]  
</Properties>  
```

<span data-ttu-id="a75dd-140">Nella tabella seguente vengono illustrati gli elementi del file di log.</span><span class="sxs-lookup"><span data-stu-id="a75dd-140">The following table describes the elements of the log file.</span></span>  
  
|<span data-ttu-id="a75dd-141">Elemento XML</span><span class="sxs-lookup"><span data-stu-id="a75dd-141">XML Element</span></span>|<span data-ttu-id="a75dd-142">Tipo</span><span class="sxs-lookup"><span data-stu-id="a75dd-142">Type</span></span>|<span data-ttu-id="a75dd-143">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a75dd-143">Description</span></span>|  
|-----------------|----------|-----------------|  
|`DriveLog`|<span data-ttu-id="a75dd-144">Elemento XML</span><span class="sxs-lookup"><span data-stu-id="a75dd-144">XML Element</span></span>|<span data-ttu-id="a75dd-145">Rappresenta un log di unità.</span><span class="sxs-lookup"><span data-stu-id="a75dd-145">Represents a drive log.</span></span>|  
|`Version`|<span data-ttu-id="a75dd-146">Attributo, stringa</span><span class="sxs-lookup"><span data-stu-id="a75dd-146">Attribute, String</span></span>|<span data-ttu-id="a75dd-147">Versione del formato del log.</span><span class="sxs-lookup"><span data-stu-id="a75dd-147">The version of the log format.</span></span>|  
|`DriveId`|<span data-ttu-id="a75dd-148">string</span><span class="sxs-lookup"><span data-stu-id="a75dd-148">String</span></span>|<span data-ttu-id="a75dd-149">Numero di serie dell'hardware dell'unità.</span><span class="sxs-lookup"><span data-stu-id="a75dd-149">The drive's hardware serial number.</span></span>|  
|`Status`|<span data-ttu-id="a75dd-150">String</span><span class="sxs-lookup"><span data-stu-id="a75dd-150">String</span></span>|<span data-ttu-id="a75dd-151">Stato di elaborazione dell'unità.</span><span class="sxs-lookup"><span data-stu-id="a75dd-151">Status of the drive processing.</span></span> <span data-ttu-id="a75dd-152">Per altre informazioni, vedere la tabella `Drive Status Codes` di seguito.</span><span class="sxs-lookup"><span data-stu-id="a75dd-152">See the `Drive Status Codes` table below for more information.</span></span>|  
|`Blob`|<span data-ttu-id="a75dd-153">Elemento XML nidificato</span><span class="sxs-lookup"><span data-stu-id="a75dd-153">Nested XML element</span></span>|<span data-ttu-id="a75dd-154">Rappresenta un BLOB.</span><span class="sxs-lookup"><span data-stu-id="a75dd-154">Represents a blob.</span></span>|  
|`Blob/BlobPath`|<span data-ttu-id="a75dd-155">string</span><span class="sxs-lookup"><span data-stu-id="a75dd-155">String</span></span>|<span data-ttu-id="a75dd-156">L'URI del BLOB.</span><span class="sxs-lookup"><span data-stu-id="a75dd-156">The URI of the blob.</span></span>|  
|`Blob/FilePath`|<span data-ttu-id="a75dd-157">String</span><span class="sxs-lookup"><span data-stu-id="a75dd-157">String</span></span>|<span data-ttu-id="a75dd-158">Il percorso relativo verso il file nell'unità.</span><span class="sxs-lookup"><span data-stu-id="a75dd-158">The relative path to the file on the drive.</span></span>|  
|`Blob/Snapshot`|<span data-ttu-id="a75dd-159">DateTime</span><span class="sxs-lookup"><span data-stu-id="a75dd-159">DateTime</span></span>|<span data-ttu-id="a75dd-160">La versione dello snapshot del BLOB, solo per un processo di esportazione.</span><span class="sxs-lookup"><span data-stu-id="a75dd-160">The snapshot version of the blob, for an export job only.</span></span>|  
|`Blob/Length`|<span data-ttu-id="a75dd-161">Integer</span><span class="sxs-lookup"><span data-stu-id="a75dd-161">Integer</span></span>|<span data-ttu-id="a75dd-162">La lunghezza totale dei BLOB in byte.</span><span class="sxs-lookup"><span data-stu-id="a75dd-162">The total length of the blob in bytes.</span></span>|  
|`Blob/LastModified`|<span data-ttu-id="a75dd-163">DateTime</span><span class="sxs-lookup"><span data-stu-id="a75dd-163">DateTime</span></span>|<span data-ttu-id="a75dd-164">Data e ora dell'ultima modifica al BLOB, solo per un processo di esportazione.</span><span class="sxs-lookup"><span data-stu-id="a75dd-164">The date/time that the blob was last modified, for an export job only.</span></span>|  
|`Blob/ImportDisposition`|<span data-ttu-id="a75dd-165">String</span><span class="sxs-lookup"><span data-stu-id="a75dd-165">String</span></span>|<span data-ttu-id="a75dd-166">La disposizione di importazione del BLOB, solo per un processo di importazione.</span><span class="sxs-lookup"><span data-stu-id="a75dd-166">The import disposition of the blob, for an import job only.</span></span>|  
|`Blob/ImportDisposition/@Status`|<span data-ttu-id="a75dd-167">Attributo, stringa</span><span class="sxs-lookup"><span data-stu-id="a75dd-167">Attribute, String</span></span>|<span data-ttu-id="a75dd-168">Lo stato della disposizione di importazione.</span><span class="sxs-lookup"><span data-stu-id="a75dd-168">The status of the import disposition.</span></span>|  
|`PageRangeList`|<span data-ttu-id="a75dd-169">Elemento XML nidificato</span><span class="sxs-lookup"><span data-stu-id="a75dd-169">Nested XML element</span></span>|<span data-ttu-id="a75dd-170">Rappresenta un elenco di intervalli di pagine per un BLOB di pagine.</span><span class="sxs-lookup"><span data-stu-id="a75dd-170">Represents a list of page ranges for a page blob.</span></span>|  
|`PageRange`|<span data-ttu-id="a75dd-171">Elemento XML</span><span class="sxs-lookup"><span data-stu-id="a75dd-171">XML element</span></span>|<span data-ttu-id="a75dd-172">Rappresenta un intervallo di pagine.</span><span class="sxs-lookup"><span data-stu-id="a75dd-172">Represents a page range.</span></span>|  
|`PageRange/@Offset`|<span data-ttu-id="a75dd-173">Attributo, valore integer</span><span class="sxs-lookup"><span data-stu-id="a75dd-173">Attribute, Integer</span></span>|<span data-ttu-id="a75dd-174">L'offset iniziale dell'intervallo di pagine nel BLOB.</span><span class="sxs-lookup"><span data-stu-id="a75dd-174">Starting offset of the page range in the blob.</span></span>|  
|`PageRange/@Length`|<span data-ttu-id="a75dd-175">Attributo, valore integer</span><span class="sxs-lookup"><span data-stu-id="a75dd-175">Attribute, Integer</span></span>|<span data-ttu-id="a75dd-176">La lunghezza in byte dell'intervallo di pagine.</span><span class="sxs-lookup"><span data-stu-id="a75dd-176">Length in bytes of the page range.</span></span>|  
|`PageRange/@Hash`|<span data-ttu-id="a75dd-177">Attributo, stringa</span><span class="sxs-lookup"><span data-stu-id="a75dd-177">Attribute, String</span></span>|<span data-ttu-id="a75dd-178">L'hash MD5 codificato in base 16 dell'intervallo di pagine.</span><span class="sxs-lookup"><span data-stu-id="a75dd-178">Base16-encoded MD5 hash of the page range.</span></span>|  
|`PageRange/@Status`|<span data-ttu-id="a75dd-179">Attributo, stringa</span><span class="sxs-lookup"><span data-stu-id="a75dd-179">Attribute, String</span></span>|<span data-ttu-id="a75dd-180">Lo stato di elaborazione dell'intervallo di pagine.</span><span class="sxs-lookup"><span data-stu-id="a75dd-180">Status of processing the page range.</span></span>|  
|`BlockList`|<span data-ttu-id="a75dd-181">Elemento XML nidificato</span><span class="sxs-lookup"><span data-stu-id="a75dd-181">Nested XML element</span></span>|<span data-ttu-id="a75dd-182">Rappresenta un elenco di blocchi per un BLOB in blocchi.</span><span class="sxs-lookup"><span data-stu-id="a75dd-182">Represents a list of blocks for a block blob.</span></span>|  
|`Block`|<span data-ttu-id="a75dd-183">Elemento XML</span><span class="sxs-lookup"><span data-stu-id="a75dd-183">XML element</span></span>|<span data-ttu-id="a75dd-184">Rappresenta un blocco.</span><span class="sxs-lookup"><span data-stu-id="a75dd-184">Represents a block.</span></span>|  
|`Block/@Offset`|<span data-ttu-id="a75dd-185">Attributo, valore integer</span><span class="sxs-lookup"><span data-stu-id="a75dd-185">Attribute, Integer</span></span>|<span data-ttu-id="a75dd-186">L'offset iniziale del blocco nel BLOB.</span><span class="sxs-lookup"><span data-stu-id="a75dd-186">Starting offset of the block in the blob.</span></span>|  
|`Block/@Length`|<span data-ttu-id="a75dd-187">Attributo, valore integer</span><span class="sxs-lookup"><span data-stu-id="a75dd-187">Attribute, Integer</span></span>|<span data-ttu-id="a75dd-188">La lunghezza in byte del blocco.</span><span class="sxs-lookup"><span data-stu-id="a75dd-188">Length in bytes of the block.</span></span>|  
|`Block/@Id`|<span data-ttu-id="a75dd-189">Attributo, stringa</span><span class="sxs-lookup"><span data-stu-id="a75dd-189">Attribute, String</span></span>|<span data-ttu-id="a75dd-190">L'ID del blocco.</span><span class="sxs-lookup"><span data-stu-id="a75dd-190">The block ID.</span></span>|  
|`Block/@Hash`|<span data-ttu-id="a75dd-191">Attributo, stringa</span><span class="sxs-lookup"><span data-stu-id="a75dd-191">Attribute, String</span></span>|<span data-ttu-id="a75dd-192">L'hash MD5 codificato in base 16 del blocco.</span><span class="sxs-lookup"><span data-stu-id="a75dd-192">Base16-encoded MD5 hash of the block.</span></span>|  
|`Block/@Status`|<span data-ttu-id="a75dd-193">Attributo, stringa</span><span class="sxs-lookup"><span data-stu-id="a75dd-193">Attribute, String</span></span>|<span data-ttu-id="a75dd-194">Lo stato di elaborazione del blocco.</span><span class="sxs-lookup"><span data-stu-id="a75dd-194">Status of processing the block.</span></span>|  
|`Metadata`|<span data-ttu-id="a75dd-195">Elemento XML nidificato</span><span class="sxs-lookup"><span data-stu-id="a75dd-195">Nested XML element</span></span>|<span data-ttu-id="a75dd-196">Rappresenta i metadati del BLOB.</span><span class="sxs-lookup"><span data-stu-id="a75dd-196">Represents the blob's metadata.</span></span>|  
|`Metadata/@Status`|<span data-ttu-id="a75dd-197">Attributo, stringa</span><span class="sxs-lookup"><span data-stu-id="a75dd-197">Attribute, String</span></span>|<span data-ttu-id="a75dd-198">Lo stato di elaborazione dei metadati del BLOB.</span><span class="sxs-lookup"><span data-stu-id="a75dd-198">Status of processing of the blob metadata.</span></span>|  
|`Metadata/GlobalPath`|<span data-ttu-id="a75dd-199">String</span><span class="sxs-lookup"><span data-stu-id="a75dd-199">String</span></span>|<span data-ttu-id="a75dd-200">Il percorso relativo verso il file di metadati globale.</span><span class="sxs-lookup"><span data-stu-id="a75dd-200">Relative path to the global metadata file.</span></span>|  
|`Metadata/GlobalPath/@Hash`|<span data-ttu-id="a75dd-201">Attributo, stringa</span><span class="sxs-lookup"><span data-stu-id="a75dd-201">Attribute, String</span></span>|<span data-ttu-id="a75dd-202">L'hash MD5 codificato in base 16 del file di metadati globale.</span><span class="sxs-lookup"><span data-stu-id="a75dd-202">Base16-encoded MD5 hash of the global metadata file.</span></span>|  
|`Metadata/Path`|<span data-ttu-id="a75dd-203">String</span><span class="sxs-lookup"><span data-stu-id="a75dd-203">String</span></span>|<span data-ttu-id="a75dd-204">Il percorso relativo verso il file di metadati.</span><span class="sxs-lookup"><span data-stu-id="a75dd-204">Relative path to the metadata file.</span></span>|  
|`Metadata/Path/@Hash`|<span data-ttu-id="a75dd-205">Attributo, stringa</span><span class="sxs-lookup"><span data-stu-id="a75dd-205">Attribute, String</span></span>|<span data-ttu-id="a75dd-206">L'hash MD5 codificato in base 16 del file di metadati.</span><span class="sxs-lookup"><span data-stu-id="a75dd-206">Base16-encoded MD5 hash of the metadata file.</span></span>|  
|`Properties`|<span data-ttu-id="a75dd-207">Elemento XML nidificato</span><span class="sxs-lookup"><span data-stu-id="a75dd-207">Nested XML element</span></span>|<span data-ttu-id="a75dd-208">Rappresenta le proprietà del BLOB.</span><span class="sxs-lookup"><span data-stu-id="a75dd-208">Represents the blob properties.</span></span>|  
|`Properties/@Status`|<span data-ttu-id="a75dd-209">Attributo, stringa</span><span class="sxs-lookup"><span data-stu-id="a75dd-209">Attribute, String</span></span>|<span data-ttu-id="a75dd-210">Lo stato di elaborazione delle proprietà del BLOB, ad esempio file non trovato, completato e così via.</span><span class="sxs-lookup"><span data-stu-id="a75dd-210">Status of processing the blob properties, e.g. file not found, completed.</span></span>|  
|`Properties/GlobalPath`|<span data-ttu-id="a75dd-211">String</span><span class="sxs-lookup"><span data-stu-id="a75dd-211">String</span></span>|<span data-ttu-id="a75dd-212">Il percorso relativo verso il file di proprietà globale.</span><span class="sxs-lookup"><span data-stu-id="a75dd-212">Relative path to the global properties file.</span></span>|  
|`Properties/GlobalPath/@Hash`|<span data-ttu-id="a75dd-213">Attributo, stringa</span><span class="sxs-lookup"><span data-stu-id="a75dd-213">Attribute, String</span></span>|<span data-ttu-id="a75dd-214">L'hash MD5 codificato in base 16 del file di proprietà globale.</span><span class="sxs-lookup"><span data-stu-id="a75dd-214">Base16-encoded MD5 hash of the global properties file.</span></span>|  
|`Properties/Path`|<span data-ttu-id="a75dd-215">String</span><span class="sxs-lookup"><span data-stu-id="a75dd-215">String</span></span>|<span data-ttu-id="a75dd-216">Il percorso relativo verso il file di proprietà.</span><span class="sxs-lookup"><span data-stu-id="a75dd-216">Relative path to the properties file.</span></span>|  
|`Properties/Path/@Hash`|<span data-ttu-id="a75dd-217">Attributo, stringa</span><span class="sxs-lookup"><span data-stu-id="a75dd-217">Attribute, String</span></span>|<span data-ttu-id="a75dd-218">L'hash MD5 codificato in base 16 del file di proprietà.</span><span class="sxs-lookup"><span data-stu-id="a75dd-218">Base16-encoded MD5 hash of the properties file.</span></span>|  
|`Blob/Status`|<span data-ttu-id="a75dd-219">String</span><span class="sxs-lookup"><span data-stu-id="a75dd-219">String</span></span>|<span data-ttu-id="a75dd-220">Lo stato di elaborazione del BLOB.</span><span class="sxs-lookup"><span data-stu-id="a75dd-220">Status of processing the blob.</span></span>|  
  
# <a name="drive-status-codes"></a><span data-ttu-id="a75dd-221">Codici di stato per un'unità</span><span class="sxs-lookup"><span data-stu-id="a75dd-221">Drive status codes</span></span>  
<span data-ttu-id="a75dd-222">Nella tabella seguente sono elencati i codici di stato per l'elaborazione di un'unità.</span><span class="sxs-lookup"><span data-stu-id="a75dd-222">The following table lists the status codes for processing a drive.</span></span>  
  
|<span data-ttu-id="a75dd-223">Codice di stato</span><span class="sxs-lookup"><span data-stu-id="a75dd-223">Status code</span></span>|<span data-ttu-id="a75dd-224">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a75dd-224">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="a75dd-225">L'unità ha completato l'elaborazione senza errori.</span><span class="sxs-lookup"><span data-stu-id="a75dd-225">The drive has finished processing without any errors.</span></span>|  
|`CompletedWithWarnings`|<span data-ttu-id="a75dd-226">L'unità ha completato l'elaborazione con avvisi di uno o più BLOB in base alle disposizioni di importazione specificate per i BLOB.</span><span class="sxs-lookup"><span data-stu-id="a75dd-226">The drive has finished processing with warnings in one or more blobs per the import dispositions specified for the blobs.</span></span>|  
|`CompletedWithErrors`|<span data-ttu-id="a75dd-227">L'unità ha completato l'elaborazione con errori in uno o più BLOB o blocchi.</span><span class="sxs-lookup"><span data-stu-id="a75dd-227">The drive has finished with errors in one or more blobs or chunks.</span></span>|  
|`DiskNotFound`|<span data-ttu-id="a75dd-228">Nessun disco trovato nell'unità.</span><span class="sxs-lookup"><span data-stu-id="a75dd-228">No disk is found on the drive.</span></span>|  
|`VolumeNotNtfs`|<span data-ttu-id="a75dd-229">Il primo volume di dati sul disco non è in formato NTFS.</span><span class="sxs-lookup"><span data-stu-id="a75dd-229">The first data volume on the disk is not in NTFS format.</span></span>|  
|`DiskOperationFailed`|<span data-ttu-id="a75dd-230">Si è verificato un errore sconosciuto durante l'esecuzione di operazioni sull'unità.</span><span class="sxs-lookup"><span data-stu-id="a75dd-230">An unknown failure occurred when performing operations on the drive.</span></span>|  
|`BitLockerVolumeNotFound`|<span data-ttu-id="a75dd-231">Non è stato trovato nessun volume BitLocker crittografabile.</span><span class="sxs-lookup"><span data-stu-id="a75dd-231">No BitLocker encryptable volume is found.</span></span>|  
|`BitLockerNotActivated`|<span data-ttu-id="a75dd-232">Nel volume non è abilitato BitLocker.</span><span class="sxs-lookup"><span data-stu-id="a75dd-232">BitLocker is not enabled on the volume.</span></span>|  
|`BitLockerProtectorNotFound`|<span data-ttu-id="a75dd-233">La protezione con chiave con password numerica non esiste nel volume.</span><span class="sxs-lookup"><span data-stu-id="a75dd-233">The numerical password key protector does not exist on the volume.</span></span>|  
|`BitLockerKeyInvalid`|<span data-ttu-id="a75dd-234">La password numerica specificata non può sbloccare il volume.</span><span class="sxs-lookup"><span data-stu-id="a75dd-234">The numerical password provided cannot unlock the volume.</span></span>|  
|`BitLockerUnlockVolumeFailed`|<span data-ttu-id="a75dd-235">Si è verificato un errore sconosciuto durante il tentativo di sbloccare il volume.</span><span class="sxs-lookup"><span data-stu-id="a75dd-235">Unknown failure has happened when trying to unlock the volume.</span></span>|  
|`BitLockerFailed`|<span data-ttu-id="a75dd-236">Si è verificato un errore sconosciuto durante l'esecuzione di operazioni BitLocker.</span><span class="sxs-lookup"><span data-stu-id="a75dd-236">An unknown failure occurred while performing BitLocker operations.</span></span>|  
|`ManifestNameInvalid`|<span data-ttu-id="a75dd-237">Il nome del file manifesto non è valido.</span><span class="sxs-lookup"><span data-stu-id="a75dd-237">The manifest file name is invalid.</span></span>|  
|`ManifestNameTooLong`|<span data-ttu-id="a75dd-238">Il nome del file manifesto è troppo lungo.</span><span class="sxs-lookup"><span data-stu-id="a75dd-238">The manifest file name is too long.</span></span>|  
|`ManifestNotFound`|<span data-ttu-id="a75dd-239">Il file manifesto non è stato trovato.</span><span class="sxs-lookup"><span data-stu-id="a75dd-239">The manifest file is not found.</span></span>|  
|`ManifestAccessDenied`|<span data-ttu-id="a75dd-240">L'accesso al file manifesto è stato negato.</span><span class="sxs-lookup"><span data-stu-id="a75dd-240">Access to the manifest file is denied.</span></span>|  
|`ManifestCorrupted`|<span data-ttu-id="a75dd-241">Il file manifesto è danneggiato (il contenuto non corrisponde all'hash).</span><span class="sxs-lookup"><span data-stu-id="a75dd-241">The manifest file is corrupted (the content does not match its hash).</span></span>|  
|`ManifestFormatInvalid`|<span data-ttu-id="a75dd-242">Il contenuto del manifesto non è conforme al formato richiesto.</span><span class="sxs-lookup"><span data-stu-id="a75dd-242">The manifest content does not conform to the required format.</span></span>|  
|`ManifestDriveIdMismatch`|<span data-ttu-id="a75dd-243">L'ID unità nel file manifesto non corrisponde a quello letto dall'unità.</span><span class="sxs-lookup"><span data-stu-id="a75dd-243">The drive ID in the manifest file does not match the one read from the drive.</span></span>|  
|`ReadManifestFailed`|<span data-ttu-id="a75dd-244">Si è verificato un errore di I/O durante la lettura dal manifesto.</span><span class="sxs-lookup"><span data-stu-id="a75dd-244">A disk I/O failure occurred while reading from the manifest.</span></span>|  
|`BlobListFormatInvalid`|<span data-ttu-id="a75dd-245">Il BLOB dell'elenco di BLOB di esportazione non è conforme al formato richiesto.</span><span class="sxs-lookup"><span data-stu-id="a75dd-245">The export blob list blob does not conform to the required format.</span></span>|  
|`BlobRequestForbidden`|<span data-ttu-id="a75dd-246">Non è consentito l'accesso ai BLOB nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="a75dd-246">Access to the blobs in the storage account is forbidden.</span></span> <span data-ttu-id="a75dd-247">Ciò potrebbe essere dovuto al fatto che la chiave dell'account di archiviazione o la firma di accesso condiviso del contenitore non sono validi.</span><span class="sxs-lookup"><span data-stu-id="a75dd-247">This might be due to invalid storage account key or container SAS.</span></span>|  
|`InternalError`|<span data-ttu-id="a75dd-248">Si è verificato un errore interno durante l'elaborazione dell'unità.</span><span class="sxs-lookup"><span data-stu-id="a75dd-248">And internal error occurred while processing the drive.</span></span>|  
  
## <a name="blob-status-codes"></a><span data-ttu-id="a75dd-249">Codici di stato per un BLOB</span><span class="sxs-lookup"><span data-stu-id="a75dd-249">Blob status codes</span></span>  
<span data-ttu-id="a75dd-250">Nella tabella seguente sono elencati i codici di stato per l'elaborazione di un BLOB.</span><span class="sxs-lookup"><span data-stu-id="a75dd-250">The following table lists the status codes for processing a blob.</span></span>  
  
|<span data-ttu-id="a75dd-251">Codice di stato</span><span class="sxs-lookup"><span data-stu-id="a75dd-251">Status code</span></span>|<span data-ttu-id="a75dd-252">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a75dd-252">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="a75dd-253">Il BLOB ha completato l'elaborazione senza errori.</span><span class="sxs-lookup"><span data-stu-id="a75dd-253">The blob has finished processing without errors.</span></span>|  
|`CompletedWithErrors`|<span data-ttu-id="a75dd-254">Il BLOB ha completato l'elaborazione con errori in uno o più intervalli di pagine o blocchi, metadati o proprietà.</span><span class="sxs-lookup"><span data-stu-id="a75dd-254">The blob has finished processing with errors in one or more page ranges or blocks, metadata, or properties.</span></span>|  
|`FileNameInvalid`|<span data-ttu-id="a75dd-255">Il nome del file non è valido.</span><span class="sxs-lookup"><span data-stu-id="a75dd-255">The file name is invalid.</span></span>|  
|`FileNameTooLong`|<span data-ttu-id="a75dd-256">Il nome del file è troppo lungo.</span><span class="sxs-lookup"><span data-stu-id="a75dd-256">The file name is too long.</span></span>|  
|`FileNotFound`|<span data-ttu-id="a75dd-257">Il file non è stato trovato.</span><span class="sxs-lookup"><span data-stu-id="a75dd-257">The file is not found.</span></span>|  
|`FileAccessDenied`|<span data-ttu-id="a75dd-258">L'accesso al file è stato negato.</span><span class="sxs-lookup"><span data-stu-id="a75dd-258">Access to the file is denied.</span></span>|  
|`BlobRequestFailed`|<span data-ttu-id="a75dd-259">La richiesta del servizio BLOB di accedere al BLOB ha avuto esito negativo.</span><span class="sxs-lookup"><span data-stu-id="a75dd-259">The Blob service request to access the blob has failed.</span></span>|  
|`BlobRequestForbidden`|<span data-ttu-id="a75dd-260">La richiesta del servizio BLOB di accedere al BLOB è vietata.</span><span class="sxs-lookup"><span data-stu-id="a75dd-260">The Blob service request to access the blob is forbidden.</span></span> <span data-ttu-id="a75dd-261">Ciò potrebbe essere dovuto al fatto che la chiave dell'account di archiviazione o la firma di accesso condiviso del contenitore non sono validi.</span><span class="sxs-lookup"><span data-stu-id="a75dd-261">This might be due to invalid storage account key or container SAS.</span></span>|  
|`RenameFailed`|<span data-ttu-id="a75dd-262">Impossibile rinominare il BLOB (per un processo di importazione) o il file (per un processo di esportazione).</span><span class="sxs-lookup"><span data-stu-id="a75dd-262">Failed to rename the blob (for an import job) or the file (for an export job).</span></span>|  
|`BlobUnexpectedChange`|<span data-ttu-id="a75dd-263">Si è verificato un cambiamento imprevisto nel BLOB (per un processo di esportazione).</span><span class="sxs-lookup"><span data-stu-id="a75dd-263">An unexpected change has occurred with the blob (for an export job).</span></span>|  
|`LeasePresent`|<span data-ttu-id="a75dd-264">È presente un lease nel BLOB.</span><span class="sxs-lookup"><span data-stu-id="a75dd-264">There is a lease present on the blob.</span></span>|  
|`IOFailed`|<span data-ttu-id="a75dd-265">Si è verificato un errore di I/O nel disco o nella rete durante l'elaborazione del BLOB.</span><span class="sxs-lookup"><span data-stu-id="a75dd-265">A disk or network I/O failure occurred while processing the blob.</span></span>|  
|`Failed`|<span data-ttu-id="a75dd-266">Si è verificato un errore sconosciuto durante l'elaborazione del BLOB.</span><span class="sxs-lookup"><span data-stu-id="a75dd-266">An unknown failure occurred while processing the blob.</span></span>|  
  
## <a name="import-disposition-status-codes"></a><span data-ttu-id="a75dd-267">Codici di stato per una disposizione di importazione</span><span class="sxs-lookup"><span data-stu-id="a75dd-267">Import disposition status codes</span></span>  
<span data-ttu-id="a75dd-268">Nella tabella seguente sono elencati i codici di stato per la risoluzione di una disposizione di importazione.</span><span class="sxs-lookup"><span data-stu-id="a75dd-268">The following table lists the status codes for resolving an import disposition.</span></span>  
  
|<span data-ttu-id="a75dd-269">Codice di stato</span><span class="sxs-lookup"><span data-stu-id="a75dd-269">Status code</span></span>|<span data-ttu-id="a75dd-270">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a75dd-270">Description</span></span>|  
|-----------------|-----------------|  
|`Created`|<span data-ttu-id="a75dd-271">Il BLOB è stato creato.</span><span class="sxs-lookup"><span data-stu-id="a75dd-271">The blob has been created.</span></span>|  
|`Renamed`|<span data-ttu-id="a75dd-272">Il BLOB è stato rinominato in base alla disposizione di importazione di ridenominazione.</span><span class="sxs-lookup"><span data-stu-id="a75dd-272">The blob has been renamed per rename import disposition.</span></span> <span data-ttu-id="a75dd-273">L'elemento `Blob/BlobPath` contiene l'URI per il BLOB rinominato.</span><span class="sxs-lookup"><span data-stu-id="a75dd-273">The `Blob/BlobPath` element contains the URI for the renamed blob.</span></span>|  
|`Skipped`|<span data-ttu-id="a75dd-274">Il BLOB è stato ignorato in base alla disposizione di importazione `no-overwrite`.</span><span class="sxs-lookup"><span data-stu-id="a75dd-274">The blob has been skipped per `no-overwrite` import disposition.</span></span>|  
|`Overwritten`|<span data-ttu-id="a75dd-275">Il BLOB ha sovrascritto un BLOB esistente in base alla disposizione di importazione `overwrite`.</span><span class="sxs-lookup"><span data-stu-id="a75dd-275">The blob has overwritten an existing blob per `overwrite` import disposition.</span></span>|  
|`Cancelled`|<span data-ttu-id="a75dd-276">Un errore precedente ha arrestato un'ulteriore elaborazione della disposizione di importazione.</span><span class="sxs-lookup"><span data-stu-id="a75dd-276">A prior failure has stopped further processing of the import disposition.</span></span>|  
  
## <a name="page-rangeblock-status-codes"></a><span data-ttu-id="a75dd-277">Codici di stato per un intervallo/blocco di pagine</span><span class="sxs-lookup"><span data-stu-id="a75dd-277">Page range/block status codes</span></span>  
<span data-ttu-id="a75dd-278">Nella tabella seguente sono elencati i codici di stato per l'elaborazione di un intervallo di pagine o un blocco.</span><span class="sxs-lookup"><span data-stu-id="a75dd-278">The following table lists the status codes for processing a page range or a block.</span></span>  
  
|<span data-ttu-id="a75dd-279">Codice di stato</span><span class="sxs-lookup"><span data-stu-id="a75dd-279">Status code</span></span>|<span data-ttu-id="a75dd-280">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a75dd-280">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="a75dd-281">L'intervallo di pagine o il blocco ha completato l'elaborazione senza errori.</span><span class="sxs-lookup"><span data-stu-id="a75dd-281">The page range or block has finished processing without any errors.</span></span>|  
|`Committed`|<span data-ttu-id="a75dd-282">È stato eseguito il commit del blocco, ma non per l'intero elenco di blocchi, dal momento che altri blocchi o l'intero elenco di blocchi hanno avuto esito negativo.</span><span class="sxs-lookup"><span data-stu-id="a75dd-282">The block has been committed,  but not in the full block list because other blocks have failed, or put full block list itself has failed.</span></span>|  
|`Uncommitted`|<span data-ttu-id="a75dd-283">Il blocco è stato caricato ma non è stato eseguito il commit.</span><span class="sxs-lookup"><span data-stu-id="a75dd-283">The block is uploaded but not committed.</span></span>|  
|`Corrupted`|<span data-ttu-id="a75dd-284">L'intervallo di pagine o il blocco è danneggiato (il contenuto non corrisponde all'hash).</span><span class="sxs-lookup"><span data-stu-id="a75dd-284">The page range or block is corrupted (the content does not match its hash).</span></span>|  
|`FileUnexpectedEnd`|<span data-ttu-id="a75dd-285">È stata rilevata una fine imprevista del file.</span><span class="sxs-lookup"><span data-stu-id="a75dd-285">An unexpected end of file has been encountered.</span></span>|  
|`BlobUnexpectedEnd`|<span data-ttu-id="a75dd-286">È stata rilevata una fine imprevista del BLOB.</span><span class="sxs-lookup"><span data-stu-id="a75dd-286">An unexpected end of blob has been encountered.</span></span>|  
|`BlobRequestFailed`|<span data-ttu-id="a75dd-287">La richiesta del servizio BLOB di accedere all'intervallo di pagine o al blocco ha avuto esito negativo.</span><span class="sxs-lookup"><span data-stu-id="a75dd-287">The Blob service request to access the page range or block has failed.</span></span>|  
|`IOFailed`|<span data-ttu-id="a75dd-288">Si è verificato un errore di I/O nel disco o nella rete durante l'elaborazione dell'intervallo di pagine o del blocco.</span><span class="sxs-lookup"><span data-stu-id="a75dd-288">A disk or network I/O failure occurred while processing the page range or block.</span></span>|  
|`Failed`|<span data-ttu-id="a75dd-289">Si è verificato un errore sconosciuto durante l'elaborazione dell'intervallo di pagine o del blocco.</span><span class="sxs-lookup"><span data-stu-id="a75dd-289">An unknown failure occurred while processing the page range or block.</span></span>|  
|`Cancelled`|<span data-ttu-id="a75dd-290">Un errore precedente ha arrestato un'ulteriore elaborazione dell'intervallo di pagine o del blocco.</span><span class="sxs-lookup"><span data-stu-id="a75dd-290">A prior failure has stopped further processing of the page range or block.</span></span>|  
  
## <a name="metadata-status-codes"></a><span data-ttu-id="a75dd-291">Codici di stato per i metadati</span><span class="sxs-lookup"><span data-stu-id="a75dd-291">Metadata status codes</span></span>  
<span data-ttu-id="a75dd-292">Nella tabella seguente sono elencati i codici di stato per l'elaborazione dei metadati del BLOB.</span><span class="sxs-lookup"><span data-stu-id="a75dd-292">The following table lists the status codes for processing blob metadata.</span></span>  
  
|<span data-ttu-id="a75dd-293">Codice di stato</span><span class="sxs-lookup"><span data-stu-id="a75dd-293">Status code</span></span>|<span data-ttu-id="a75dd-294">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a75dd-294">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="a75dd-295">I metadati hanno completato l'elaborazione senza errori.</span><span class="sxs-lookup"><span data-stu-id="a75dd-295">The metadata has finished processing without errors.</span></span>|  
|`FileNameInvalid`|<span data-ttu-id="a75dd-296">Il nome del file di metadati non è valido.</span><span class="sxs-lookup"><span data-stu-id="a75dd-296">The metadata file name is invalid.</span></span>|  
|`FileNameTooLong`|<span data-ttu-id="a75dd-297">Il nome del file di metadati è troppo lungo.</span><span class="sxs-lookup"><span data-stu-id="a75dd-297">The metadata file name is too long.</span></span>|  
|`FileNotFound`|<span data-ttu-id="a75dd-298">Il nome del file di metadati non è stato trovato.</span><span class="sxs-lookup"><span data-stu-id="a75dd-298">The metadata file is not found.</span></span>|  
|`FileAccessDenied`|<span data-ttu-id="a75dd-299">L'accesso al file di metadati è stato negato.</span><span class="sxs-lookup"><span data-stu-id="a75dd-299">Access to the metadata file is denied.</span></span>|  
|`Corrupted`|<span data-ttu-id="a75dd-300">Il file di metadati è danneggiato (il contenuto non corrisponde all'hash).</span><span class="sxs-lookup"><span data-stu-id="a75dd-300">The metadata file is corrupted (the content does not match its hash).</span></span>|  
|`XmlReadFailed`|<span data-ttu-id="a75dd-301">Il contenuto dei metadati non è conforme al formato richiesto.</span><span class="sxs-lookup"><span data-stu-id="a75dd-301">The metadata content does not conform to the required format.</span></span>|  
|`XmlWriteFailed`|<span data-ttu-id="a75dd-302">La scrittura dell'elemento XML dei metadati ha avuto esito negativo.</span><span class="sxs-lookup"><span data-stu-id="a75dd-302">Writing the metadata XML has failed.</span></span>|  
|`BlobRequestFailed`|<span data-ttu-id="a75dd-303">La richiesta del servizio BLOB di accedere ai metadati ha avuto esito negativo.</span><span class="sxs-lookup"><span data-stu-id="a75dd-303">The Blob service request to access the metadata has failed.</span></span>|  
|`IOFailed`|<span data-ttu-id="a75dd-304">Si è verificato un errore di I/O nel disco o nella rete durante l'elaborazione dei metadati.</span><span class="sxs-lookup"><span data-stu-id="a75dd-304">A disk or network I/O failure occurred while processing the metadata.</span></span>|  
|`Failed`|<span data-ttu-id="a75dd-305">Si è verificato un errore sconosciuto durante l'elaborazione dei metadati.</span><span class="sxs-lookup"><span data-stu-id="a75dd-305">An unknown failure occurred while processing the metadata.</span></span>|  
|`Cancelled`|<span data-ttu-id="a75dd-306">Un errore precedente ha arrestato un'ulteriore elaborazione dei metadati.</span><span class="sxs-lookup"><span data-stu-id="a75dd-306">A prior failure has stopped further processing of the metadata.</span></span>|  
  
## <a name="properties-status-codes"></a><span data-ttu-id="a75dd-307">Codici di stato delle proprietà</span><span class="sxs-lookup"><span data-stu-id="a75dd-307">Properties status codes</span></span>  
<span data-ttu-id="a75dd-308">Nella tabella seguente sono elencati i codici di stato per l'elaborazione delle proprietà del BLOB.</span><span class="sxs-lookup"><span data-stu-id="a75dd-308">The following table lists the status codes for processing blob properties.</span></span>  
  
|<span data-ttu-id="a75dd-309">Codice di stato</span><span class="sxs-lookup"><span data-stu-id="a75dd-309">Status code</span></span>|<span data-ttu-id="a75dd-310">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a75dd-310">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="a75dd-311">Le proprietà hanno completato l'elaborazione senza errori.</span><span class="sxs-lookup"><span data-stu-id="a75dd-311">The properties have finished processing without any errors.</span></span>|  
|`FileNameInvalid`|<span data-ttu-id="a75dd-312">Il nome del file di proprietà non è valido.</span><span class="sxs-lookup"><span data-stu-id="a75dd-312">The properties file name is invalid.</span></span>|  
|`FileNameTooLong`|<span data-ttu-id="a75dd-313">Il nome del file di proprietà è troppo lungo.</span><span class="sxs-lookup"><span data-stu-id="a75dd-313">The properties file name is too long.</span></span>|  
|`FileNotFound`|<span data-ttu-id="a75dd-314">Il file di proprietà non è stato trovato.</span><span class="sxs-lookup"><span data-stu-id="a75dd-314">The properties file is not found.</span></span>|  
|`FileAccessDenied`|<span data-ttu-id="a75dd-315">L'accesso al file di proprietà è stato negato.</span><span class="sxs-lookup"><span data-stu-id="a75dd-315">Access to the properties file is denied.</span></span>|  
|`Corrupted`|<span data-ttu-id="a75dd-316">Il file di proprietà è danneggiato (il contenuto non corrisponde all'hash).</span><span class="sxs-lookup"><span data-stu-id="a75dd-316">The properties file is corrupted (the content does not match its hash).</span></span>|  
|`XmlReadFailed`|<span data-ttu-id="a75dd-317">Il contenuto delle proprietà non è conforme al formato richiesto.</span><span class="sxs-lookup"><span data-stu-id="a75dd-317">The properties content does not conform to the required format.</span></span>|  
|`XmlWriteFailed`|<span data-ttu-id="a75dd-318">La scrittura dell'elemento XML delle proprietà ha avuto esito negativo.</span><span class="sxs-lookup"><span data-stu-id="a75dd-318">Writing the properties XML has failed.</span></span>|  
|`BlobRequestFailed`|<span data-ttu-id="a75dd-319">La richiesta del servizio BLOB di accedere alle proprietà ha avuto esito negativo.</span><span class="sxs-lookup"><span data-stu-id="a75dd-319">The Blob service request to access the properties has failed.</span></span>|  
|`IOFailed`|<span data-ttu-id="a75dd-320">Si è verificato un errore di I/O nel disco o nella rete durante l'elaborazione delle proprietà.</span><span class="sxs-lookup"><span data-stu-id="a75dd-320">A disk or network I/O failure occurred while processing the properties.</span></span>|  
|`Failed`|<span data-ttu-id="a75dd-321">Si è verificato un errore sconosciuto durante l'elaborazione delle proprietà.</span><span class="sxs-lookup"><span data-stu-id="a75dd-321">An unknown failure occurred while processing the properties.</span></span>|  
|`Cancelled`|<span data-ttu-id="a75dd-322">Un errore precedente ha arrestato un'ulteriore elaborazione delle proprietà.</span><span class="sxs-lookup"><span data-stu-id="a75dd-322">A prior failure has stopped further processing of the properties.</span></span>|  
  
## <a name="sample-logs"></a><span data-ttu-id="a75dd-323">Esempi di log</span><span class="sxs-lookup"><span data-stu-id="a75dd-323">Sample logs</span></span>  
<span data-ttu-id="a75dd-324">Di seguito è riportato un esempio di log dettagliato.</span><span class="sxs-lookup"><span data-stu-id="a75dd-324">The following is an example of verbose log.</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<DriveLog Version="2014-11-01">  
    <DriveId>WD-WMATV123456</DriveId>  
    <Blob Status="Completed">  
       <BlobPath>pictures/bob/wild/desert.jpg</BlobPath>  
       <FilePath>\Users\bob\Pictures\wild\desert.jpg</FilePath>  
       <Length>98304</Length>  
       <ImportDisposition Status="Created">overwrite</ImportDisposition>  
       <BlockList>  
          <Block Offset="0" Length="65536" Id="AAAAAA==" Hash=" 9C8AE14A55241F98533C4D80D85CDC68" Status="Completed"/>  
          <Block Offset="65536" Length="32768" Id="AQAAAA==" Hash=" DF54C531C9B3CA2570FDDDB3BCD0E27D" Status="Completed"/>  
       </BlockList>  
       <Metadata Status="Completed">  
          <GlobalPath Hash=" E34F54B7086BCF4EC1601D056F4C7E37">\Users\bob\Pictures\wild\metadata.xml</GlobalPath>  
       </Metadata>  
    </Blob>  
    <Blob Status="CompletedWithErrors">  
       <BlobPath>pictures/bob/animals/koala.jpg</BlobPath>  
       <FilePath>\Users\bob\Pictures\animals\koala.jpg</FilePath>  
       <Length>163840</Length>  
       <ImportDisposition Status="Overwritten">overwrite</ImportDisposition>  
       <PageRangeList>  
          <PageRange Offset="0" Length="65536" Hash="19701B8877418393CB3CB567F53EE225" Status="Completed"/>  
          <PageRange Offset="65536" Length="65536" Hash="AA2585F6F6FD01C4AD4256E018240CD4" Status="Corrupted"/>  
          <PageRange Offset="131072" Length="4096" Hash="9BA552E1C3EEAFFC91B42B979900A996" Status="Completed"/>  
       </PageRangeList>  
       <Properties Status="Completed">  
          <Path Hash="38D7AE80653F47F63C0222FEE90EC4E7">\Users\bob\Pictures\animals\koala.jpg.properties</Path>  
       </Properties>  
    </Blob>  
    <Status>CompletedWithErrors</Status>  
</DriveLog>  
```  
  
<span data-ttu-id="a75dd-325">Di seguito è riportato il log degli errori corrispondente.</span><span class="sxs-lookup"><span data-stu-id="a75dd-325">The corresponding error log is shown below.</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<DriveLog Version="2014-11-01">  
    <DriveId>WD-WMATV6965824</DriveId>  
    <Blob Status="CompletedWithErrors">  
       <BlobPath>pictures/bob/animals/koala.jpg</BlobPath>  
       <FilePath>\Users\bob\Pictures\animals\koala.jpg</FilePath>  
       <Length>163840</Length>  
       <ImportDisposition Status="Overwritten">overwrite</ImportDisposition>  
       <PageRangeList>  
          <PageRange Offset="65536" Length="65536" Hash="AA2585F6F6FD01C4AD4256E018240CD4" Status="Corrupted"/>  
       </PageRangeList>  
    </Blob>  
    <Status>CompletedWithErrors</Status>  
</DriveLog>  
```

 <span data-ttu-id="a75dd-326">Il log degli errori seguente per un processo di importazione contiene un errore relativo a un file non trovato nell'unità di importazione.</span><span class="sxs-lookup"><span data-stu-id="a75dd-326">The follow error log for an import job contains an error about a file not found on the import drive.</span></span> <span data-ttu-id="a75dd-327">Si noti che lo stato dei componenti successivi è `Cancelled`.</span><span class="sxs-lookup"><span data-stu-id="a75dd-327">Note that the status of subsequent components is `Cancelled`.</span></span>  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveLog Version="2014-11-01">  
  <DriveId>9WM35C2V</DriveId>  
  <Blob Status="FileNotFound">  
    <BlobPath>pictures/animals/koala.jpg</BlobPath>  
    <FilePath>\animals\koala.jpg</FilePath>  
    <Length>30310</Length>  
    <ImportDisposition Status="Cancelled">rename</ImportDisposition>  
    <BlockList>  
      <Block Offset="0" Length="6062" Id="MD5/cAzn4h7VVSWXf696qp5Uaw==" Hash="700CE7E21ED55525977FAF7AAA9E546B" Status="Cancelled" />  
      <Block Offset="6062" Length="6062" Id="MD5/PEnGwYOI8LPLNYdfKr7kAg==" Hash="3C49C6C18388F0B3CB35875F2ABEE402" Status="Cancelled" />  
      <Block Offset="12124" Length="6062" Id="MD5/FG4WxqfZKuUWZ2nGTU2qVA==" Hash="146E16C6A7D92AE5166769C64D4DAA54" Status="Cancelled" />  
      <Block Offset="18186" Length="6062" Id="MD5/ZzibNDzr3IRBQENRyegeXQ==" Hash="67389B343CEBDC8441404351C9E81E5D" Status="Cancelled" />  
      <Block Offset="24248" Length="6062" Id="MD5/ZzibNDzr3IRBQENRyegeXQ==" Hash="67389B343CEBDC8441404351C9E81E5D" Status="Cancelled" />  
    </BlockList>  
  </Blob>  
  <Status>CompletedWithErrors</Status>  
</DriveLog>  
```

<span data-ttu-id="a75dd-328">Il log degli errori seguente per un processo di esportazione indica che il contenuto del BLOB è stato scritto correttamente nell'unità, ma si è verificato un errore durante l'esportazione le proprietà del BLOB.</span><span class="sxs-lookup"><span data-stu-id="a75dd-328">The following error log for an export job indicates that the blob content has been successfully written to the drive, but that an error occurred while exporting the blob's properties.</span></span>  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveLog Version="2014-11-01">  
  <DriveId>9WM35C3U</DriveId>  
  <Blob Status="CompletedWithErrors">  
    <BlobPath>pictures/wild/canyon.jpg</BlobPath>  
    <FilePath>\pictures\wild\canyon.jpg</FilePath>  
    <LastModified>2012-09-18T23:47:08Z</LastModified>  
    <Length>163840</Length>  
    <BlockList />  
    <Properties Status="Failed" />  
  </Blob>  
  <Status>CompletedWithErrors</Status>  
</DriveLog>  
```
  
## <a name="next-steps"></a><span data-ttu-id="a75dd-329">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a75dd-329">Next steps</span></span>
 
* <span data-ttu-id="a75dd-330">[Storage Import/Export REST API](/rest/api/storageimportexport/) (API REST di importazione/esportazione dell'archiviazione)</span><span class="sxs-lookup"><span data-stu-id="a75dd-330">[Storage Import/Export REST API](/rest/api/storageimportexport/)</span></span>
