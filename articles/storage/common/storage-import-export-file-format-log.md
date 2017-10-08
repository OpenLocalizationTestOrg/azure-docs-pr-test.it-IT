---
title: formato di file log di importazione/esportazione aaaAzure | Documenti Microsoft
description: Informazioni sul formato hello hello di file di log creato quando vengono eseguiti i passaggi per un processo del servizio di importazione/esportazione.
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
ms.openlocfilehash: 15a652455aa947922af0aa39ccefe68811a3db19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-importexport-service-log-file-format"></a><span data-ttu-id="1d7f4-103">Formato dei file di log del servizio Importazione/Esportazione di Azure</span><span class="sxs-lookup"><span data-stu-id="1d7f4-103">Azure Import/Export service log file format</span></span>
<span data-ttu-id="1d7f4-104">Quando hello servizio importazione/esportazione di Microsoft Azure esegue un'azione in un'unità come parte di un processo di importazione o esportazione, i log vengono scritti tooblock BLOB nell'account di archiviazione hello associata a tale processo.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-104">When hello Microsoft Azure Import/Export service performs an action on a drive as part of an import job or an export job, logs are written tooblock blobs in hello storage account associated with that job.</span></span>  
  
<span data-ttu-id="1d7f4-105">Esistono due log che possono essere scritti dal servizio di importazione/esportazione hello:</span><span class="sxs-lookup"><span data-stu-id="1d7f4-105">There are two logs that may be written by hello Import/Export service:</span></span>  
  
-   <span data-ttu-id="1d7f4-106">log degli errori di Hello viene sempre generata in caso di hello di un errore.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-106">hello error log is always generated in hello event of an error.</span></span>  
  
-   <span data-ttu-id="1d7f4-107">Hello log dettagliato non è abilitato per impostazione predefinita, ma può essere abilitato per impostazione hello `EnableVerboseLog` proprietà in un [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) o [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operazione.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-107">hello verbose log is not enabled by default, but may be enabled by setting hello `EnableVerboseLog` property on a [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) or [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operation.</span></span>  
  
## <a name="log-file-location"></a><span data-ttu-id="1d7f4-108">Posizione dei file di log</span><span class="sxs-lookup"><span data-stu-id="1d7f4-108">Log file location</span></span>  
<span data-ttu-id="1d7f4-109">Hello vengono scritti i log tooblock BLOB nel contenitore hello o la directory virtuale specificata da hello `ImportExportStatesPath` impostazione, è possibile impostare un `Put Job` operazione.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-109">hello logs are written tooblock blobs in hello container or virtual directory specified by hello `ImportExportStatesPath` setting, which you can set on a `Put Job` operation.</span></span> <span data-ttu-id="1d7f4-110">Hello percorso toowhich hello registri dipende da come viene specificata l'autenticazione per il processo di hello, nonché hello valore specificato per `ImportExportStatesPath`.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-110">hello location toowhich hello logs are written depends on how authentication is specified for hello job, together with hello value specified for `ImportExportStatesPath`.</span></span> <span data-ttu-id="1d7f4-111">È possibile specificare l'autenticazione per il processo di hello tramite una chiave di account di archiviazione o un contenitore di firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-111">Authentication for hello job may be specified via a storage account key, or a container SAS (shared access signature).</span></span>  
  
<span data-ttu-id="1d7f4-112">nome Hello del contenitore hello o la directory virtuale può essere sia un nome predefinito hello `waimportexport`, o un altro contenitore o nome della directory virtuale specificati.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-112">hello name of hello container or virtual directory may either be hello default name of `waimportexport`, or another container or virtual directory name that you specify.</span></span>  
  
<span data-ttu-id="1d7f4-113">tabella Hello seguente mostra le opzioni possibili hello:</span><span class="sxs-lookup"><span data-stu-id="1d7f4-113">hello table below shows hello possible options:</span></span>  
  
|<span data-ttu-id="1d7f4-114">Metodo di autenticazione</span><span class="sxs-lookup"><span data-stu-id="1d7f4-114">Authentication Method</span></span>|<span data-ttu-id="1d7f4-115">Valore dell'elemento `ImportExportStatesPath`</span><span class="sxs-lookup"><span data-stu-id="1d7f4-115">Value of `ImportExportStatesPath`Element</span></span>|<span data-ttu-id="1d7f4-116">Posizione dei BLOB di log</span><span class="sxs-lookup"><span data-stu-id="1d7f4-116">Location of Log Blobs</span></span>|  
|---------------------------|----------------------------------------------|---------------------------|  
|<span data-ttu-id="1d7f4-117">Chiave dell'account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="1d7f4-117">Storage account key</span></span>|<span data-ttu-id="1d7f4-118">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="1d7f4-118">Default value</span></span>|<span data-ttu-id="1d7f4-119">Un contenitore denominato `waimportexport`, ovvero contenitore predefinito hello.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-119">A container named `waimportexport`, which is hello default container.</span></span> <span data-ttu-id="1d7f4-120">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="1d7f4-120">For example:</span></span><br /><br /> `https://myaccount.blob.core.windows.net/waimportexport`|  
|<span data-ttu-id="1d7f4-121">Chiave dell'account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="1d7f4-121">Storage account key</span></span>|<span data-ttu-id="1d7f4-122">Valore specificato dall'utente</span><span class="sxs-lookup"><span data-stu-id="1d7f4-122">User-specified value</span></span>|<span data-ttu-id="1d7f4-123">Un contenitore denominato dall'utente hello.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-123">A container named by hello user.</span></span> <span data-ttu-id="1d7f4-124">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="1d7f4-124">For example:</span></span><br /><br /> `https://myaccount.blob.core.windows.net/mylogcontainer`|  
|<span data-ttu-id="1d7f4-125">Firma di accesso condiviso del contenitore</span><span class="sxs-lookup"><span data-stu-id="1d7f4-125">Container SAS</span></span>|<span data-ttu-id="1d7f4-126">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="1d7f4-126">Default value</span></span>|<span data-ttu-id="1d7f4-127">Una directory virtuale denominata `waimportexport`, ovvero nome predefinito di hello, sotto il contenitore di hello specificato nella firma di accesso condiviso hello.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-127">A virtual directory named `waimportexport`, which is hello default name, beneath hello container specified in hello SAS.</span></span><br /><br /> <span data-ttu-id="1d7f4-128">Ad esempio, se hello firma di accesso condiviso per il processo di hello è `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, percorso log hello sarà`https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport`</span><span class="sxs-lookup"><span data-stu-id="1d7f4-128">For example, if hello SAS specified for hello job is  `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, then hello log location would be `https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport`</span></span>|  
|<span data-ttu-id="1d7f4-129">Firma di accesso condiviso del contenitore</span><span class="sxs-lookup"><span data-stu-id="1d7f4-129">Container SAS</span></span>|<span data-ttu-id="1d7f4-130">Valore specificato dall'utente</span><span class="sxs-lookup"><span data-stu-id="1d7f4-130">User-specified value</span></span>|<span data-ttu-id="1d7f4-131">Una directory virtuale denominata dall'utente hello, sotto il contenitore di hello specificato nella firma di accesso condiviso hello.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-131">A virtual directory named by hello user, beneath hello container specified in hello SAS.</span></span><br /><br /> <span data-ttu-id="1d7f4-132">Ad esempio, se hello firma di accesso condiviso per il processo di hello è `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, e hello specificato una directory virtuale è denominata `mylogblobs`, percorso log hello sarà `https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport/mylogblobs`.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-132">For example, if hello SAS specified for hello job is  `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, and hello specified virtual directory is named `mylogblobs`, then hello log location would be `https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport/mylogblobs`.</span></span>|  
  
<span data-ttu-id="1d7f4-133">È possibile recuperare l'URL hello errore hello e di log dettagliati dal chiamante hello [recupero del processo](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operazione.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-133">You can retrieve hello URL for hello error and verbose logs by calling hello [Get Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span></span> <span data-ttu-id="1d7f4-134">al termine dell'elaborazione dell'unità di hello, sono disponibili log di Hello.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-134">hello logs are available after processing of hello drive is complete.</span></span>  
  
## <a name="log-file-format"></a><span data-ttu-id="1d7f4-135">Formato di file dei log</span><span class="sxs-lookup"><span data-stu-id="1d7f4-135">Log file format</span></span>  
<span data-ttu-id="1d7f4-136">Hello formato per entrambi i log è hello stesso: un blob che contiene le descrizioni XML degli eventi di hello che si è verificato durante la copia di BLOB tra hello disco rigido e account del cliente hello.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-136">hello format for both logs is hello same: a blob containing XML descriptions of hello events that occurred while copying blobs between hello hard drive and hello customer's account.</span></span>  
  
<span data-ttu-id="1d7f4-137">log dettagliato Hello contiene informazioni complete sullo stato di hello dell'operazione di copia hello per ogni blob (per un processo di importazione) o un file (per un processo di esportazione), mentre il log degli errori di hello contiene solo le informazioni di hello per BLOB o i file che ha rilevato errori durante hello importare o esportare i processi.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-137">hello verbose log contains complete information about hello status of hello copy operation for every blob (for an import job) or file (for an export job), whereas hello error log contains only hello information for blobs or files that encountered errors during hello import or export job.</span></span>  
  
<span data-ttu-id="1d7f4-138">formato del log dettagliato Hello è illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-138">hello verbose log format is shown below.</span></span> <span data-ttu-id="1d7f4-139">log degli errori di Hello è hello struttura, ma esclude le operazioni riuscite.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-139">hello error log has hello same structure, but filters out successful operations.</span></span>  

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

<span data-ttu-id="1d7f4-140">Hello nella tabella seguente descrive gli elementi di hello hello del file di log.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-140">hello following table describes hello elements of hello log file.</span></span>  
  
|<span data-ttu-id="1d7f4-141">Elemento XML</span><span class="sxs-lookup"><span data-stu-id="1d7f4-141">XML Element</span></span>|<span data-ttu-id="1d7f4-142">Tipo</span><span class="sxs-lookup"><span data-stu-id="1d7f4-142">Type</span></span>|<span data-ttu-id="1d7f4-143">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1d7f4-143">Description</span></span>|  
|-----------------|----------|-----------------|  
|`DriveLog`|<span data-ttu-id="1d7f4-144">Elemento XML</span><span class="sxs-lookup"><span data-stu-id="1d7f4-144">XML Element</span></span>|<span data-ttu-id="1d7f4-145">Rappresenta un log di unità.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-145">Represents a drive log.</span></span>|  
|`Version`|<span data-ttu-id="1d7f4-146">Attributo, stringa</span><span class="sxs-lookup"><span data-stu-id="1d7f4-146">Attribute, String</span></span>|<span data-ttu-id="1d7f4-147">versione di Hello del formato di log hello.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-147">hello version of hello log format.</span></span>|  
|`DriveId`|<span data-ttu-id="1d7f4-148">String</span><span class="sxs-lookup"><span data-stu-id="1d7f4-148">String</span></span>|<span data-ttu-id="1d7f4-149">numero di serie dell'hardware dell'unità di Hello.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-149">hello drive's hardware serial number.</span></span>|  
|`Status`|<span data-ttu-id="1d7f4-150">String</span><span class="sxs-lookup"><span data-stu-id="1d7f4-150">String</span></span>|<span data-ttu-id="1d7f4-151">Stato di elaborazione di unità hello.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-151">Status of hello drive processing.</span></span> <span data-ttu-id="1d7f4-152">Vedere hello `Drive Status Codes` tabella riportata di seguito per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-152">See hello `Drive Status Codes` table below for more information.</span></span>|  
|`Blob`|<span data-ttu-id="1d7f4-153">Elemento XML nidificato</span><span class="sxs-lookup"><span data-stu-id="1d7f4-153">Nested XML element</span></span>|<span data-ttu-id="1d7f4-154">Rappresenta un BLOB.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-154">Represents a blob.</span></span>|  
|`Blob/BlobPath`|<span data-ttu-id="1d7f4-155">String</span><span class="sxs-lookup"><span data-stu-id="1d7f4-155">String</span></span>|<span data-ttu-id="1d7f4-156">URI del blob hello Hello.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-156">hello URI of hello blob.</span></span>|  
|`Blob/FilePath`|<span data-ttu-id="1d7f4-157">String</span><span class="sxs-lookup"><span data-stu-id="1d7f4-157">String</span></span>|<span data-ttu-id="1d7f4-158">Hello percorso relativo toohello file hello unità.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-158">hello relative path toohello file on hello drive.</span></span>|  
|`Blob/Snapshot`|<span data-ttu-id="1d7f4-159">DateTime</span><span class="sxs-lookup"><span data-stu-id="1d7f4-159">DateTime</span></span>|<span data-ttu-id="1d7f4-160">versione di Hello snapshot del blob hello, per un solo processo di esportazione.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-160">hello snapshot version of hello blob, for an export job only.</span></span>|  
|`Blob/Length`|<span data-ttu-id="1d7f4-161">Integer</span><span class="sxs-lookup"><span data-stu-id="1d7f4-161">Integer</span></span>|<span data-ttu-id="1d7f4-162">lunghezza totale di Hello di blob hello in byte.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-162">hello total length of hello blob in bytes.</span></span>|  
|`Blob/LastModified`|<span data-ttu-id="1d7f4-163">DateTime</span><span class="sxs-lookup"><span data-stu-id="1d7f4-163">DateTime</span></span>|<span data-ttu-id="1d7f4-164">Hello data/ora ultima modifica del blob che hello, per un solo processo di esportazione.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-164">hello date/time that hello blob was last modified, for an export job only.</span></span>|  
|`Blob/ImportDisposition`|<span data-ttu-id="1d7f4-165">String</span><span class="sxs-lookup"><span data-stu-id="1d7f4-165">String</span></span>|<span data-ttu-id="1d7f4-166">Hello importare disposition del blob hello, per un solo processo di importazione.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-166">hello import disposition of hello blob, for an import job only.</span></span>|  
|`Blob/ImportDisposition/@Status`|<span data-ttu-id="1d7f4-167">Attributo, stringa</span><span class="sxs-lookup"><span data-stu-id="1d7f4-167">Attribute, String</span></span>|<span data-ttu-id="1d7f4-168">stato Hello di hello disposizione di importazione.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-168">hello status of hello import disposition.</span></span>|  
|`PageRangeList`|<span data-ttu-id="1d7f4-169">Elemento XML nidificato</span><span class="sxs-lookup"><span data-stu-id="1d7f4-169">Nested XML element</span></span>|<span data-ttu-id="1d7f4-170">Rappresenta un elenco di intervalli di pagine per un BLOB di pagine.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-170">Represents a list of page ranges for a page blob.</span></span>|  
|`PageRange`|<span data-ttu-id="1d7f4-171">Elemento XML</span><span class="sxs-lookup"><span data-stu-id="1d7f4-171">XML element</span></span>|<span data-ttu-id="1d7f4-172">Rappresenta un intervallo di pagine.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-172">Represents a page range.</span></span>|  
|`PageRange/@Offset`|<span data-ttu-id="1d7f4-173">Attributo, valore integer</span><span class="sxs-lookup"><span data-stu-id="1d7f4-173">Attribute, Integer</span></span>|<span data-ttu-id="1d7f4-174">Offset iniziale dell'intervallo di pagine hello in blob hello.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-174">Starting offset of hello page range in hello blob.</span></span>|  
|`PageRange/@Length`|<span data-ttu-id="1d7f4-175">Attributo, valore integer</span><span class="sxs-lookup"><span data-stu-id="1d7f4-175">Attribute, Integer</span></span>|<span data-ttu-id="1d7f4-176">Lunghezza in byte dell'intervallo di pagine hello.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-176">Length in bytes of hello page range.</span></span>|  
|`PageRange/@Hash`|<span data-ttu-id="1d7f4-177">Attributo, stringa</span><span class="sxs-lookup"><span data-stu-id="1d7f4-177">Attribute, String</span></span>|<span data-ttu-id="1d7f4-178">Hash MD5 codificato in base 16 dell'intervallo di pagine hello.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-178">Base16-encoded MD5 hash of hello page range.</span></span>|  
|`PageRange/@Status`|<span data-ttu-id="1d7f4-179">Attributo, stringa</span><span class="sxs-lookup"><span data-stu-id="1d7f4-179">Attribute, String</span></span>|<span data-ttu-id="1d7f4-180">Stato di elaborazione l'intervallo di pagine hello.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-180">Status of processing hello page range.</span></span>|  
|`BlockList`|<span data-ttu-id="1d7f4-181">Elemento XML nidificato</span><span class="sxs-lookup"><span data-stu-id="1d7f4-181">Nested XML element</span></span>|<span data-ttu-id="1d7f4-182">Rappresenta un elenco di blocchi per un BLOB in blocchi.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-182">Represents a list of blocks for a block blob.</span></span>|  
|`Block`|<span data-ttu-id="1d7f4-183">Elemento XML</span><span class="sxs-lookup"><span data-stu-id="1d7f4-183">XML element</span></span>|<span data-ttu-id="1d7f4-184">Rappresenta un blocco.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-184">Represents a block.</span></span>|  
|`Block/@Offset`|<span data-ttu-id="1d7f4-185">Attributo, valore integer</span><span class="sxs-lookup"><span data-stu-id="1d7f4-185">Attribute, Integer</span></span>|<span data-ttu-id="1d7f4-186">Offset iniziale del blocco di hello nel blob hello.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-186">Starting offset of hello block in hello blob.</span></span>|  
|`Block/@Length`|<span data-ttu-id="1d7f4-187">Attributo, valore integer</span><span class="sxs-lookup"><span data-stu-id="1d7f4-187">Attribute, Integer</span></span>|<span data-ttu-id="1d7f4-188">Lunghezza in byte del blocco di hello.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-188">Length in bytes of hello block.</span></span>|  
|`Block/@Id`|<span data-ttu-id="1d7f4-189">Attributo, stringa</span><span class="sxs-lookup"><span data-stu-id="1d7f4-189">Attribute, String</span></span>|<span data-ttu-id="1d7f4-190">ID del blocco di Hello.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-190">hello block ID.</span></span>|  
|`Block/@Hash`|<span data-ttu-id="1d7f4-191">Attributo, stringa</span><span class="sxs-lookup"><span data-stu-id="1d7f4-191">Attribute, String</span></span>|<span data-ttu-id="1d7f4-192">Hash MD5 codificato in base 16 del blocco di hello.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-192">Base16-encoded MD5 hash of hello block.</span></span>|  
|`Block/@Status`|<span data-ttu-id="1d7f4-193">Attributo, stringa</span><span class="sxs-lookup"><span data-stu-id="1d7f4-193">Attribute, String</span></span>|<span data-ttu-id="1d7f4-194">Stato di elaborazione blocco hello.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-194">Status of processing hello block.</span></span>|  
|`Metadata`|<span data-ttu-id="1d7f4-195">Elemento XML nidificato</span><span class="sxs-lookup"><span data-stu-id="1d7f4-195">Nested XML element</span></span>|<span data-ttu-id="1d7f4-196">Rappresenta i metadati del blob hello.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-196">Represents hello blob's metadata.</span></span>|  
|`Metadata/@Status`|<span data-ttu-id="1d7f4-197">Attributo, stringa</span><span class="sxs-lookup"><span data-stu-id="1d7f4-197">Attribute, String</span></span>|<span data-ttu-id="1d7f4-198">Stato di elaborazione dei metadati del blob hello.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-198">Status of processing of hello blob metadata.</span></span>|  
|`Metadata/GlobalPath`|<span data-ttu-id="1d7f4-199">String</span><span class="sxs-lookup"><span data-stu-id="1d7f4-199">String</span></span>|<span data-ttu-id="1d7f4-200">File dei metadati globali toohello di percorso relativo.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-200">Relative path toohello global metadata file.</span></span>|  
|`Metadata/GlobalPath/@Hash`|<span data-ttu-id="1d7f4-201">Attributo, stringa</span><span class="sxs-lookup"><span data-stu-id="1d7f4-201">Attribute, String</span></span>|<span data-ttu-id="1d7f4-202">Hash MD5 codificato in base 16 del file di metadati globali hello.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-202">Base16-encoded MD5 hash of hello global metadata file.</span></span>|  
|`Metadata/Path`|<span data-ttu-id="1d7f4-203">String</span><span class="sxs-lookup"><span data-stu-id="1d7f4-203">String</span></span>|<span data-ttu-id="1d7f4-204">File di metadati toohello percorso relativo.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-204">Relative path toohello metadata file.</span></span>|  
|`Metadata/Path/@Hash`|<span data-ttu-id="1d7f4-205">Attributo, stringa</span><span class="sxs-lookup"><span data-stu-id="1d7f4-205">Attribute, String</span></span>|<span data-ttu-id="1d7f4-206">Hash MD5 codificato in base 16 del file di metadati hello.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-206">Base16-encoded MD5 hash of hello metadata file.</span></span>|  
|`Properties`|<span data-ttu-id="1d7f4-207">Elemento XML nidificato</span><span class="sxs-lookup"><span data-stu-id="1d7f4-207">Nested XML element</span></span>|<span data-ttu-id="1d7f4-208">Rappresenta le proprietà del blob hello.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-208">Represents hello blob properties.</span></span>|  
|`Properties/@Status`|<span data-ttu-id="1d7f4-209">Attributo, stringa</span><span class="sxs-lookup"><span data-stu-id="1d7f4-209">Attribute, String</span></span>|<span data-ttu-id="1d7f4-210">Stato di elaborazione delle proprietà del blob hello, ad esempio file non viene trovato, completato.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-210">Status of processing hello blob properties, e.g. file not found, completed.</span></span>|  
|`Properties/GlobalPath`|<span data-ttu-id="1d7f4-211">String</span><span class="sxs-lookup"><span data-stu-id="1d7f4-211">String</span></span>|<span data-ttu-id="1d7f4-212">File delle proprietà globali toohello di percorso relativo.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-212">Relative path toohello global properties file.</span></span>|  
|`Properties/GlobalPath/@Hash`|<span data-ttu-id="1d7f4-213">Attributo, stringa</span><span class="sxs-lookup"><span data-stu-id="1d7f4-213">Attribute, String</span></span>|<span data-ttu-id="1d7f4-214">Hash MD5 codificato in base 16 del file delle proprietà globali hello.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-214">Base16-encoded MD5 hash of hello global properties file.</span></span>|  
|`Properties/Path`|<span data-ttu-id="1d7f4-215">String</span><span class="sxs-lookup"><span data-stu-id="1d7f4-215">String</span></span>|<span data-ttu-id="1d7f4-216">File delle proprietà toohello del percorso relativo.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-216">Relative path toohello properties file.</span></span>|  
|`Properties/Path/@Hash`|<span data-ttu-id="1d7f4-217">Attributo, stringa</span><span class="sxs-lookup"><span data-stu-id="1d7f4-217">Attribute, String</span></span>|<span data-ttu-id="1d7f4-218">Hash MD5 codificato in base 16 del file di proprietà hello.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-218">Base16-encoded MD5 hash of hello properties file.</span></span>|  
|`Blob/Status`|<span data-ttu-id="1d7f4-219">String</span><span class="sxs-lookup"><span data-stu-id="1d7f4-219">String</span></span>|<span data-ttu-id="1d7f4-220">Stato di elaborazione blob hello.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-220">Status of processing hello blob.</span></span>|  
  
# <a name="drive-status-codes"></a><span data-ttu-id="1d7f4-221">Codici di stato per un'unità</span><span class="sxs-lookup"><span data-stu-id="1d7f4-221">Drive status codes</span></span>  
<span data-ttu-id="1d7f4-222">Hello nella tabella seguente sono elencati i codici di stato hello per l'elaborazione di un'unità.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-222">hello following table lists hello status codes for processing a drive.</span></span>  
  
|<span data-ttu-id="1d7f4-223">Codice di stato</span><span class="sxs-lookup"><span data-stu-id="1d7f4-223">Status code</span></span>|<span data-ttu-id="1d7f4-224">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1d7f4-224">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="1d7f4-225">unità di Hello ha terminato l'elaborazione senza errori.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-225">hello drive has finished processing without any errors.</span></span>|  
|`CompletedWithWarnings`|<span data-ttu-id="1d7f4-226">unità di Hello ha terminato l'elaborazione con avvisi in uno o più BLOB per disposizioni di importazione hello specificate per i BLOB hello.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-226">hello drive has finished processing with warnings in one or more blobs per hello import dispositions specified for hello blobs.</span></span>|  
|`CompletedWithErrors`|<span data-ttu-id="1d7f4-227">Hello unità ha terminato con errori in uno o più BLOB o blocchi.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-227">hello drive has finished with errors in one or more blobs or chunks.</span></span>|  
|`DiskNotFound`|<span data-ttu-id="1d7f4-228">Nessun disco disponibile nell'unità di hello.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-228">No disk is found on hello drive.</span></span>|  
|`VolumeNotNtfs`|<span data-ttu-id="1d7f4-229">volume di dati su disco hello prima Hello non è in formato NTFS.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-229">hello first data volume on hello disk is not in NTFS format.</span></span>|  
|`DiskOperationFailed`|<span data-ttu-id="1d7f4-230">Si è verificato un errore sconosciuto durante l'esecuzione di operazioni sulle unità hello.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-230">An unknown failure occurred when performing operations on hello drive.</span></span>|  
|`BitLockerVolumeNotFound`|<span data-ttu-id="1d7f4-231">Non è stato trovato nessun volume BitLocker crittografabile.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-231">No BitLocker encryptable volume is found.</span></span>|  
|`BitLockerNotActivated`|<span data-ttu-id="1d7f4-232">BitLocker non è abilitato nel volume hello.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-232">BitLocker is not enabled on hello volume.</span></span>|  
|`BitLockerProtectorNotFound`|<span data-ttu-id="1d7f4-233">protezione con chiave di Hello password numerica non esiste nel volume hello.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-233">hello numerical password key protector does not exist on hello volume.</span></span>|  
|`BitLockerKeyInvalid`|<span data-ttu-id="1d7f4-234">password numerica di Hello specificata non è possibile sbloccare il volume di hello.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-234">hello numerical password provided cannot unlock hello volume.</span></span>|  
|`BitLockerUnlockVolumeFailed`|<span data-ttu-id="1d7f4-235">Quando si tenta di volume hello toounlock, si è verificato un errore sconosciuto.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-235">Unknown failure has happened when trying toounlock hello volume.</span></span>|  
|`BitLockerFailed`|<span data-ttu-id="1d7f4-236">Si è verificato un errore sconosciuto durante l'esecuzione di operazioni BitLocker.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-236">An unknown failure occurred while performing BitLocker operations.</span></span>|  
|`ManifestNameInvalid`|<span data-ttu-id="1d7f4-237">nome del file manifesto Hello non è valido.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-237">hello manifest file name is invalid.</span></span>|  
|`ManifestNameTooLong`|<span data-ttu-id="1d7f4-238">nome del file manifesto Hello è troppo lungo.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-238">hello manifest file name is too long.</span></span>|  
|`ManifestNotFound`|<span data-ttu-id="1d7f4-239">file manifesto di Hello non viene trovato.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-239">hello manifest file is not found.</span></span>|  
|`ManifestAccessDenied`|<span data-ttu-id="1d7f4-240">File manifesto toohello di accesso è negato.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-240">Access toohello manifest file is denied.</span></span>|  
|`ManifestCorrupted`|<span data-ttu-id="1d7f4-241">Hello file manifesto è danneggiato (hello contenuto non corrisponde al valore hash).</span><span class="sxs-lookup"><span data-stu-id="1d7f4-241">hello manifest file is corrupted (hello content does not match its hash).</span></span>|  
|`ManifestFormatInvalid`|<span data-ttu-id="1d7f4-242">contenuto del manifesto Hello formato richiesto toohello non è conforme.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-242">hello manifest content does not conform toohello required format.</span></span>|  
|`ManifestDriveIdMismatch`|<span data-ttu-id="1d7f4-243">Hello unità che ID nel file manifesto hello non corrisponde a una lettura dal disco hello hello.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-243">hello drive ID in hello manifest file does not match hello one read from hello drive.</span></span>|  
|`ReadManifestFailed`|<span data-ttu-id="1d7f4-244">Si è verificato un errore dei / o del disco durante la lettura dal manifesto hello.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-244">A disk I/O failure occurred while reading from hello manifest.</span></span>|  
|`BlobListFormatInvalid`|<span data-ttu-id="1d7f4-245">elenco di blob di Hello esportazione formato richiesto toohello non è conforme.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-245">hello export blob list blob does not conform toohello required format.</span></span>|  
|`BlobRequestForbidden`|<span data-ttu-id="1d7f4-246">Accedi ai BLOB toohello nell'account di archiviazione hello non è consentito.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-246">Access toohello blobs in hello storage account is forbidden.</span></span> <span data-ttu-id="1d7f4-247">Potrebbe trattarsi di scadenza tooinvalid chiave dell'account di archiviazione o firma di accesso.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-247">This might be due tooinvalid storage account key or container SAS.</span></span>|  
|`InternalError`|<span data-ttu-id="1d7f4-248">E si è verificato un errore interno durante l'elaborazione di unità hello.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-248">And internal error occurred while processing hello drive.</span></span>|  
  
## <a name="blob-status-codes"></a><span data-ttu-id="1d7f4-249">Codici di stato per un BLOB</span><span class="sxs-lookup"><span data-stu-id="1d7f4-249">Blob status codes</span></span>  
<span data-ttu-id="1d7f4-250">Hello nella tabella seguente sono elencati i codici di stato hello per l'elaborazione di un blob.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-250">hello following table lists hello status codes for processing a blob.</span></span>  
  
|<span data-ttu-id="1d7f4-251">Codice di stato</span><span class="sxs-lookup"><span data-stu-id="1d7f4-251">Status code</span></span>|<span data-ttu-id="1d7f4-252">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1d7f4-252">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="1d7f4-253">blob di Hello ha terminato l'elaborazione senza errori.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-253">hello blob has finished processing without errors.</span></span>|  
|`CompletedWithErrors`|<span data-ttu-id="1d7f4-254">blob Hello ha terminato l'elaborazione con errori in uno o più intervalli di pagine o blocchi, metadati o proprietà.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-254">hello blob has finished processing with errors in one or more page ranges or blocks, metadata, or properties.</span></span>|  
|`FileNameInvalid`|<span data-ttu-id="1d7f4-255">nome del file Hello non è valido.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-255">hello file name is invalid.</span></span>|  
|`FileNameTooLong`|<span data-ttu-id="1d7f4-256">nome del file Hello è troppo lungo.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-256">hello file name is too long.</span></span>|  
|`FileNotFound`|<span data-ttu-id="1d7f4-257">non è stato trovato il file Hello.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-257">hello file is not found.</span></span>|  
|`FileAccessDenied`|<span data-ttu-id="1d7f4-258">File toohello accesso negato.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-258">Access toohello file is denied.</span></span>|  
|`BlobRequestFailed`|<span data-ttu-id="1d7f4-259">richiesta di servizio Blob Hello tooaccess hello blob non riuscita.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-259">hello Blob service request tooaccess hello blob has failed.</span></span>|  
|`BlobRequestForbidden`|<span data-ttu-id="1d7f4-260">richiesta del servizio Blob Hello tooaccess hello blob non è consentito.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-260">hello Blob service request tooaccess hello blob is forbidden.</span></span> <span data-ttu-id="1d7f4-261">Potrebbe trattarsi di scadenza tooinvalid chiave dell'account di archiviazione o firma di accesso.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-261">This might be due tooinvalid storage account key or container SAS.</span></span>|  
|`RenameFailed`|<span data-ttu-id="1d7f4-262">Impossibile blob hello toorename (per un processo di importazione) o file hello (per un processo di esportazione).</span><span class="sxs-lookup"><span data-stu-id="1d7f4-262">Failed toorename hello blob (for an import job) or hello file (for an export job).</span></span>|  
|`BlobUnexpectedChange`|<span data-ttu-id="1d7f4-263">Si è verificato una modifica imprevista con blob hello (per un processo di esportazione).</span><span class="sxs-lookup"><span data-stu-id="1d7f4-263">An unexpected change has occurred with hello blob (for an export job).</span></span>|  
|`LeasePresent`|<span data-ttu-id="1d7f4-264">È presente su blob hello un lease.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-264">There is a lease present on hello blob.</span></span>|  
|`IOFailed`|<span data-ttu-id="1d7f4-265">Un disco o un errore dei / o di rete si è verificato durante l'elaborazione hello blob.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-265">A disk or network I/O failure occurred while processing hello blob.</span></span>|  
|`Failed`|<span data-ttu-id="1d7f4-266">Si è verificato un errore sconosciuto durante l'elaborazione hello blob.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-266">An unknown failure occurred while processing hello blob.</span></span>|  
  
## <a name="import-disposition-status-codes"></a><span data-ttu-id="1d7f4-267">Codici di stato per una disposizione di importazione</span><span class="sxs-lookup"><span data-stu-id="1d7f4-267">Import disposition status codes</span></span>  
<span data-ttu-id="1d7f4-268">Hello nella tabella seguente sono elencati i codici di stato hello per la risoluzione di una disposizione di importazione.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-268">hello following table lists hello status codes for resolving an import disposition.</span></span>  
  
|<span data-ttu-id="1d7f4-269">Codice di stato</span><span class="sxs-lookup"><span data-stu-id="1d7f4-269">Status code</span></span>|<span data-ttu-id="1d7f4-270">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1d7f4-270">Description</span></span>|  
|-----------------|-----------------|  
|`Created`|<span data-ttu-id="1d7f4-271">Hello blob è stato creato.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-271">hello blob has been created.</span></span>|  
|`Renamed`|<span data-ttu-id="1d7f4-272">blob Hello è stato rinominato in base a disposizione di importazione rename.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-272">hello blob has been renamed per rename import disposition.</span></span> <span data-ttu-id="1d7f4-273">Hello `Blob/BlobPath` elemento contiene hello URI per il blob rinominato hello.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-273">hello `Blob/BlobPath` element contains hello URI for hello renamed blob.</span></span>|  
|`Skipped`|<span data-ttu-id="1d7f4-274">Hello blob è stato ignorato `no-overwrite` disposizione di importazione.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-274">hello blob has been skipped per `no-overwrite` import disposition.</span></span>|  
|`Overwritten`|<span data-ttu-id="1d7f4-275">è stato sovrascritto da un blob esistente per ogni blob Hello `overwrite` disposizione di importazione.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-275">hello blob has overwritten an existing blob per `overwrite` import disposition.</span></span>|  
|`Cancelled`|<span data-ttu-id="1d7f4-276">Un errore precedente ha arrestato un'ulteriore elaborazione della disposizione di importazione hello.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-276">A prior failure has stopped further processing of hello import disposition.</span></span>|  
  
## <a name="page-rangeblock-status-codes"></a><span data-ttu-id="1d7f4-277">Codici di stato per un intervallo/blocco di pagine</span><span class="sxs-lookup"><span data-stu-id="1d7f4-277">Page range/block status codes</span></span>  
<span data-ttu-id="1d7f4-278">Hello nella tabella seguente sono elencati i codici di stato hello per l'elaborazione di un intervallo di pagine o un blocco.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-278">hello following table lists hello status codes for processing a page range or a block.</span></span>  
  
|<span data-ttu-id="1d7f4-279">Codice di stato</span><span class="sxs-lookup"><span data-stu-id="1d7f4-279">Status code</span></span>|<span data-ttu-id="1d7f4-280">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1d7f4-280">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="1d7f4-281">intervallo di pagine Hello o un blocco ha terminato l'elaborazione senza errori.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-281">hello page range or block has finished processing without any errors.</span></span>|  
|`Committed`|<span data-ttu-id="1d7f4-282">blocco di Hello è stato eseguito il commit, ma non in hello completo perché altri blocchi necessario non è riuscita o inserire l'elenco completo di blocco non è riuscita.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-282">hello block has been committed,  but not in hello full block list because other blocks have failed, or put full block list itself has failed.</span></span>|  
|`Uncommitted`|<span data-ttu-id="1d7f4-283">blocco Hello è stato caricato ma non è stato eseguito il commit.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-283">hello block is uploaded but not committed.</span></span>|  
|`Corrupted`|<span data-ttu-id="1d7f4-284">intervallo di pagine Hello o un blocco è danneggiato (hello contenuto non corrisponde al valore hash).</span><span class="sxs-lookup"><span data-stu-id="1d7f4-284">hello page range or block is corrupted (hello content does not match its hash).</span></span>|  
|`FileUnexpectedEnd`|<span data-ttu-id="1d7f4-285">È stata rilevata una fine imprevista del file.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-285">An unexpected end of file has been encountered.</span></span>|  
|`BlobUnexpectedEnd`|<span data-ttu-id="1d7f4-286">È stata rilevata una fine imprevista del BLOB.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-286">An unexpected end of blob has been encountered.</span></span>|  
|`BlobRequestFailed`|<span data-ttu-id="1d7f4-287">Hello richiesta del servizio Blob tooaccess hello intervallo di pagine o blocchi non sono riuscita.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-287">hello Blob service request tooaccess hello page range or block has failed.</span></span>|  
|`IOFailed`|<span data-ttu-id="1d7f4-288">Un disco o un errore dei / o di rete durante l'elaborazione di intervallo di pagine hello o un blocco.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-288">A disk or network I/O failure occurred while processing hello page range or block.</span></span>|  
|`Failed`|<span data-ttu-id="1d7f4-289">Si è verificato un errore sconosciuto durante l'elaborazione di intervallo di pagine hello o un blocco.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-289">An unknown failure occurred while processing hello page range or block.</span></span>|  
|`Cancelled`|<span data-ttu-id="1d7f4-290">Un errore precedente ha arrestato l'ulteriore elaborazione dell'intervallo di pagine hello o un blocco.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-290">A prior failure has stopped further processing of hello page range or block.</span></span>|  
  
## <a name="metadata-status-codes"></a><span data-ttu-id="1d7f4-291">Codici di stato per i metadati</span><span class="sxs-lookup"><span data-stu-id="1d7f4-291">Metadata status codes</span></span>  
<span data-ttu-id="1d7f4-292">Hello nella tabella seguente sono elencati i codici di stato hello per l'elaborazione di metadati blob.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-292">hello following table lists hello status codes for processing blob metadata.</span></span>  
  
|<span data-ttu-id="1d7f4-293">Codice di stato</span><span class="sxs-lookup"><span data-stu-id="1d7f4-293">Status code</span></span>|<span data-ttu-id="1d7f4-294">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1d7f4-294">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="1d7f4-295">metadati Hello ha terminato l'elaborazione senza errori.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-295">hello metadata has finished processing without errors.</span></span>|  
|`FileNameInvalid`|<span data-ttu-id="1d7f4-296">nome di file di metadati Hello non è valido.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-296">hello metadata file name is invalid.</span></span>|  
|`FileNameTooLong`|<span data-ttu-id="1d7f4-297">nome di file di metadati Hello è troppo lungo.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-297">hello metadata file name is too long.</span></span>|  
|`FileNotFound`|<span data-ttu-id="1d7f4-298">file di metadati Hello non viene trovato.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-298">hello metadata file is not found.</span></span>|  
|`FileAccessDenied`|<span data-ttu-id="1d7f4-299">File di metadati toohello accesso negato.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-299">Access toohello metadata file is denied.</span></span>|  
|`Corrupted`|<span data-ttu-id="1d7f4-300">file di metadati Hello è danneggiato (hello contenuto non corrisponde al valore hash).</span><span class="sxs-lookup"><span data-stu-id="1d7f4-300">hello metadata file is corrupted (hello content does not match its hash).</span></span>|  
|`XmlReadFailed`|<span data-ttu-id="1d7f4-301">contenuto dei metadati Hello formato richiesto toohello non è conforme.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-301">hello metadata content does not conform toohello required format.</span></span>|  
|`XmlWriteFailed`|<span data-ttu-id="1d7f4-302">La scrittura dei metadati di hello che XML non è riuscita.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-302">Writing hello metadata XML has failed.</span></span>|  
|`BlobRequestFailed`|<span data-ttu-id="1d7f4-303">richiesta di servizio Blob Hello tooaccess hello metadati non riuscita.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-303">hello Blob service request tooaccess hello metadata has failed.</span></span>|  
|`IOFailed`|<span data-ttu-id="1d7f4-304">Si è verificato un errore dei / o disco o di rete durante l'elaborazione dei metadati hello.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-304">A disk or network I/O failure occurred while processing hello metadata.</span></span>|  
|`Failed`|<span data-ttu-id="1d7f4-305">Si è verificato un errore sconosciuto durante l'elaborazione dei metadati hello.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-305">An unknown failure occurred while processing hello metadata.</span></span>|  
|`Cancelled`|<span data-ttu-id="1d7f4-306">Un errore precedente ha arrestato un'ulteriore elaborazione dei metadati hello.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-306">A prior failure has stopped further processing of hello metadata.</span></span>|  
  
## <a name="properties-status-codes"></a><span data-ttu-id="1d7f4-307">Codici di stato delle proprietà</span><span class="sxs-lookup"><span data-stu-id="1d7f4-307">Properties status codes</span></span>  
<span data-ttu-id="1d7f4-308">Hello nella tabella seguente sono elencati i codici di stato hello per l'elaborazione delle proprietà del blob.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-308">hello following table lists hello status codes for processing blob properties.</span></span>  
  
|<span data-ttu-id="1d7f4-309">Codice di stato</span><span class="sxs-lookup"><span data-stu-id="1d7f4-309">Status code</span></span>|<span data-ttu-id="1d7f4-310">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1d7f4-310">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="1d7f4-311">proprietà Hello hanno terminato l'elaborazione senza errori.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-311">hello properties have finished processing without any errors.</span></span>|  
|`FileNameInvalid`|<span data-ttu-id="1d7f4-312">nome del file Hello proprietà non è valido.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-312">hello properties file name is invalid.</span></span>|  
|`FileNameTooLong`|<span data-ttu-id="1d7f4-313">nome del file delle proprietà Hello è troppo lungo.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-313">hello properties file name is too long.</span></span>|  
|`FileNotFound`|<span data-ttu-id="1d7f4-314">file di proprietà Hello non viene trovato.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-314">hello properties file is not found.</span></span>|  
|`FileAccessDenied`|<span data-ttu-id="1d7f4-315">File delle proprietà toohello di accesso è negato.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-315">Access toohello properties file is denied.</span></span>|  
|`Corrupted`|<span data-ttu-id="1d7f4-316">file delle proprietà Hello è danneggiato (hello contenuto non corrisponde al valore hash).</span><span class="sxs-lookup"><span data-stu-id="1d7f4-316">hello properties file is corrupted (hello content does not match its hash).</span></span>|  
|`XmlReadFailed`|<span data-ttu-id="1d7f4-317">contenuto di proprietà Hello formato richiesto toohello non è conforme.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-317">hello properties content does not conform toohello required format.</span></span>|  
|`XmlWriteFailed`|<span data-ttu-id="1d7f4-318">Scrittura delle proprietà hello che XML non è riuscita.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-318">Writing hello properties XML has failed.</span></span>|  
|`BlobRequestFailed`|<span data-ttu-id="1d7f4-319">richiesta del servizio Blob Hello tooaccess hello proprietà non è riuscita.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-319">hello Blob service request tooaccess hello properties has failed.</span></span>|  
|`IOFailed`|<span data-ttu-id="1d7f4-320">Si è verificato un errore dei / o disco o di rete durante l'elaborazione hello proprietà.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-320">A disk or network I/O failure occurred while processing hello properties.</span></span>|  
|`Failed`|<span data-ttu-id="1d7f4-321">Si è verificato un errore sconosciuto durante l'elaborazione hello proprietà.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-321">An unknown failure occurred while processing hello properties.</span></span>|  
|`Cancelled`|<span data-ttu-id="1d7f4-322">Un errore precedente ha arrestato un'ulteriore elaborazione delle proprietà hello.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-322">A prior failure has stopped further processing of hello properties.</span></span>|  
  
## <a name="sample-logs"></a><span data-ttu-id="1d7f4-323">Esempi di log</span><span class="sxs-lookup"><span data-stu-id="1d7f4-323">Sample logs</span></span>  
<span data-ttu-id="1d7f4-324">Hello Ecco un esempio di log dettagliato.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-324">hello following is an example of verbose log.</span></span>  
  
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
  
<span data-ttu-id="1d7f4-325">log degli errori corrispondente Hello è illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-325">hello corresponding error log is shown below.</span></span>  
  
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

 <span data-ttu-id="1d7f4-326">log degli errori di seguire Hello per un processo di importazione contiene un errore relativo a un file non trovato nell'unità di importazione hello.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-326">hello follow error log for an import job contains an error about a file not found on hello import drive.</span></span> <span data-ttu-id="1d7f4-327">Si noti che è stato hello dei componenti successivi `Cancelled`.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-327">Note that hello status of subsequent components is `Cancelled`.</span></span>  
  
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

<span data-ttu-id="1d7f4-328">Hello seguenti log degli errori per un processo di esportazione indica che il contenuto di blob hello è stata scritta correttamente toohello unità, ma che si è verificato un errore durante l'esportazione delle proprietà del blob hello.</span><span class="sxs-lookup"><span data-stu-id="1d7f4-328">hello following error log for an export job indicates that hello blob content has been successfully written toohello drive, but that an error occurred while exporting hello blob's properties.</span></span>  
  
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
  
## <a name="next-steps"></a><span data-ttu-id="1d7f4-329">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1d7f4-329">Next steps</span></span>
 
* <span data-ttu-id="1d7f4-330">[Storage Import/Export REST API](/rest/api/storageimportexport/) (API REST di importazione/esportazione dell'archiviazione)</span><span class="sxs-lookup"><span data-stu-id="1d7f4-330">[Storage Import/Export REST API](/rest/api/storageimportexport/)</span></span>
