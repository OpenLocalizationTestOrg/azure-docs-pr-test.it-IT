---
title: Diagnostica e ripristino dagli errori per i processi di Importazione/Esportazione di Azure | Documentazione Microsoft
description: Informazioni su come abilitare la registrazione dettagliata per i processi del servizio Importazione/Esportazione di Microsoft Azure.
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 096cc795-9af6-4335-9fe8-fffa9f239a17
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 0068aae9d6780aa41a070db0eb191d0d5a165d21
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="diagnostics-and-error-recovery-for-azure-importexport-jobs"></a><span data-ttu-id="39c40-103">Diagnostica e ripristino dagli errori per i processi di Importazione/Esportazione di Azure</span><span class="sxs-lookup"><span data-stu-id="39c40-103">Diagnostics and error recovery for Azure Import/Export jobs</span></span>
<span data-ttu-id="39c40-104">Per ogni unità elaborata, il servizio Importazione/Esportazione di Azure crea un log degli errori nell'account di archiviazione associato.</span><span class="sxs-lookup"><span data-stu-id="39c40-104">For each drive processed, the Azure Import/Export service creates an error log in the associated storage account.</span></span> <span data-ttu-id="39c40-105">È anche possibile abilitare la registrazione dettagliata impostando la proprietà `LogLevel` su `Verbose` quando si chiamano le operazioni [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) o [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update).</span><span class="sxs-lookup"><span data-stu-id="39c40-105">You can also enable verbose logging by setting the `LogLevel` property to `Verbose` when calling the [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) or [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operations.</span></span>

 <span data-ttu-id="39c40-106">Per impostazione predefinita, i log vengono scritti in un contenitore denominato `waimportexport`.</span><span class="sxs-lookup"><span data-stu-id="39c40-106">By default, logs are written to a container named `waimportexport`.</span></span> <span data-ttu-id="39c40-107">È possibile specificare un nome diverso impostando la proprietà `DiagnosticsPath` quando si chiamano le operazioni `Put Job` or `Update Job Properties`.</span><span class="sxs-lookup"><span data-stu-id="39c40-107">You can specify a different name by setting the `DiagnosticsPath` property when calling the `Put Job` or `Update Job Properties` operations.</span></span> <span data-ttu-id="39c40-108">I log vengono archiviati come BLOB in blocchi con la convenzione di denominazione seguente: `waies/jobname_driveid_timestamp_logtype.xml`.</span><span class="sxs-lookup"><span data-stu-id="39c40-108">The logs are stored as block blobs with the following naming convention: `waies/jobname_driveid_timestamp_logtype.xml`.</span></span>

 <span data-ttu-id="39c40-109">È possibile recuperare l'URI dei log per un processo chiamando l'operazione [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get).</span><span class="sxs-lookup"><span data-stu-id="39c40-109">You can retrieve the URI of the logs for a job by calling the [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) operation.</span></span> <span data-ttu-id="39c40-110">L'URI per il log dettagliato viene restituito nella proprietà `VerboseLogUri` per ogni unità, mentre l'URI per il log degli errori viene restituito nella proprietà `ErrorLogUri`.</span><span class="sxs-lookup"><span data-stu-id="39c40-110">The URI for the verbose log is returned in the `VerboseLogUri` property for each drive, while the URI for the error log is returned in the `ErrorLogUri` property.</span></span>

<span data-ttu-id="39c40-111">È possibile usare i dati di registrazione per identificare i problemi seguenti.</span><span class="sxs-lookup"><span data-stu-id="39c40-111">You can use the logging data to identify the following issues.</span></span>

## <a name="drive-errors"></a><span data-ttu-id="39c40-112">Errori delle unità</span><span class="sxs-lookup"><span data-stu-id="39c40-112">Drive errors</span></span>

<span data-ttu-id="39c40-113">Gli elementi seguenti sono classificati come errori delle unità:</span><span class="sxs-lookup"><span data-stu-id="39c40-113">The following items are classified as drive errors:</span></span>

-   <span data-ttu-id="39c40-114">Errori di accesso o di lettura del file manifesto</span><span class="sxs-lookup"><span data-stu-id="39c40-114">Errors in accessing or reading the manifest file</span></span>

-   <span data-ttu-id="39c40-115">Chiavi BitLocker non corrette</span><span class="sxs-lookup"><span data-stu-id="39c40-115">Incorrect BitLocker keys</span></span>

-   <span data-ttu-id="39c40-116">Errori di lettura/scrittura delle unità</span><span class="sxs-lookup"><span data-stu-id="39c40-116">Drive read/write errors</span></span>

## <a name="blob-errors"></a><span data-ttu-id="39c40-117">Errori del BLOB</span><span class="sxs-lookup"><span data-stu-id="39c40-117">Blob errors</span></span>

<span data-ttu-id="39c40-118">Gli elementi seguenti sono classificati come errori del BLOB:</span><span class="sxs-lookup"><span data-stu-id="39c40-118">The following items are classified as blob errors:</span></span>

-   <span data-ttu-id="39c40-119">BLOB o nomi non corretti o in conflitto</span><span class="sxs-lookup"><span data-stu-id="39c40-119">Incorrect or conflicting blob or names</span></span>

-   <span data-ttu-id="39c40-120">File mancanti</span><span class="sxs-lookup"><span data-stu-id="39c40-120">Missing files</span></span>

-   <span data-ttu-id="39c40-121">BLOB non trovato</span><span class="sxs-lookup"><span data-stu-id="39c40-121">Blob not found</span></span>

-   <span data-ttu-id="39c40-122">File troncati (i file sul disco sono più piccoli di quanto specificato nel manifesto)</span><span class="sxs-lookup"><span data-stu-id="39c40-122">Truncated files (the files on the disk are smaller than specified in the manifest)</span></span>

-   <span data-ttu-id="39c40-123">Contenuto dei file danneggiato (per i processi di importazione, rilevato con un checksum MD5 non corrispondente)</span><span class="sxs-lookup"><span data-stu-id="39c40-123">Corrupted file content (for import jobs, detected with an MD5 checksum mismatch)</span></span>

-   <span data-ttu-id="39c40-124">File di metadati e proprietà BLOB danneggiati (rilevati con un checksum MD5 non corrispondente)</span><span class="sxs-lookup"><span data-stu-id="39c40-124">Corrupted blob metadata and property files (detected with an MD5 checksum mismatch)</span></span>

-   <span data-ttu-id="39c40-125">Schema non corretto per i file di metadati e/o proprietà BLOB</span><span class="sxs-lookup"><span data-stu-id="39c40-125">Incorrect schema for the blob properties and/or metadata files</span></span>

<span data-ttu-id="39c40-126">Può capitare che alcune parti di un processo di importazione o esportazione non vengano completate correttamente, anche se l'intero processo viene completato.</span><span class="sxs-lookup"><span data-stu-id="39c40-126">There may be cases where some parts of an import or export job do not complete successfully, while the overall job still completes.</span></span> <span data-ttu-id="39c40-127">In questo caso, è possibile caricare o scaricare in rete le parti mancanti dei dati oppure è possibile creare un nuovo processo per trasferire i dati.</span><span class="sxs-lookup"><span data-stu-id="39c40-127">In this case, you can either upload or download the missing pieces of the data over network, or you can create a new job to transfer the data.</span></span> <span data-ttu-id="39c40-128">Per informazioni su come ripristinare i dati in rete, vedere [Azure Import/Export Tool Reference](storage-import-export-tool-how-to-v1.md) (Informazioni di riferimento sullo strumento Importazione/Esportazione di Azure).</span><span class="sxs-lookup"><span data-stu-id="39c40-128">See the [Azure Import/Export Tool Reference](storage-import-export-tool-how-to-v1.md) to learn how to repair the data over network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="39c40-129">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="39c40-129">Next steps</span></span>

* [<span data-ttu-id="39c40-130">Uso dell'API REST del servizio Importazione/Esportazione</span><span class="sxs-lookup"><span data-stu-id="39c40-130">Using the Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
