---
title: ripristino aaaDiagnostics e di errore per i processi di importazione/esportazione di Azure | Documenti Microsoft
description: Informazioni su come i processi del servizio tooenable la registrazione dettagliata per importazione/esportazione di Microsoft Azure.
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
ms.openlocfilehash: 48164279e7904c78fed802aa3cff66e589c3f12c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="diagnostics-and-error-recovery-for-azure-importexport-jobs"></a><span data-ttu-id="a7908-103">Diagnostica e ripristino dagli errori per i processi di Importazione/Esportazione di Azure</span><span class="sxs-lookup"><span data-stu-id="a7908-103">Diagnostics and error recovery for Azure Import/Export jobs</span></span>
<span data-ttu-id="a7908-104">Per ogni unità elaborata, hello servizio importazione/esportazione di Azure crea un log degli errori nell'account di archiviazione hello associata.</span><span class="sxs-lookup"><span data-stu-id="a7908-104">For each drive processed, hello Azure Import/Export service creates an error log in hello associated storage account.</span></span> <span data-ttu-id="a7908-105">È inoltre possibile abilitare la registrazione dettagliata per l'impostazione hello `LogLevel` proprietà troppo`Verbose` quando si chiama hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) o [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operazioni.</span><span class="sxs-lookup"><span data-stu-id="a7908-105">You can also enable verbose logging by setting hello `LogLevel` property too`Verbose` when calling hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) or [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operations.</span></span>

 <span data-ttu-id="a7908-106">Per impostazione predefinita, i log vengono scritti tooa contenitore denominato `waimportexport`.</span><span class="sxs-lookup"><span data-stu-id="a7908-106">By default, logs are written tooa container named `waimportexport`.</span></span> <span data-ttu-id="a7908-107">È possibile specificare un nome diverso dall'impostazione hello `DiagnosticsPath` proprietà quando si chiama hello `Put Job` o `Update Job Properties` operazioni.</span><span class="sxs-lookup"><span data-stu-id="a7908-107">You can specify a different name by setting hello `DiagnosticsPath` property when calling hello `Put Job` or `Update Job Properties` operations.</span></span> <span data-ttu-id="a7908-108">Hello i log vengono archiviati come BLOB in blocchi con hello convenzione di denominazione seguente: `waies/jobname_driveid_timestamp_logtype.xml`.</span><span class="sxs-lookup"><span data-stu-id="a7908-108">hello logs are stored as block blobs with hello following naming convention: `waies/jobname_driveid_timestamp_logtype.xml`.</span></span>

 <span data-ttu-id="a7908-109">È possibile recuperare hello URI dei log di hello per un processo dal chiamante hello [recupero del processo](/rest/api/storageimportexport/jobs#Jobs_Get) operazione.</span><span class="sxs-lookup"><span data-stu-id="a7908-109">You can retrieve hello URI of hello logs for a job by calling hello [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) operation.</span></span> <span data-ttu-id="a7908-110">Hello URI per il log dettagliato hello viene restituito in hello `VerboseLogUri` proprietà per ogni unità, mentre hello URI hello log degli errori viene restituito in hello `ErrorLogUri` proprietà.</span><span class="sxs-lookup"><span data-stu-id="a7908-110">hello URI for hello verbose log is returned in hello `VerboseLogUri` property for each drive, while hello URI for hello error log is returned in hello `ErrorLogUri` property.</span></span>

<span data-ttu-id="a7908-111">È possibile utilizzare hello hello tooidentify dati seguenti problemi di registrazione.</span><span class="sxs-lookup"><span data-stu-id="a7908-111">You can use hello logging data tooidentify hello following issues.</span></span>

## <a name="drive-errors"></a><span data-ttu-id="a7908-112">Errori delle unità</span><span class="sxs-lookup"><span data-stu-id="a7908-112">Drive errors</span></span>

<span data-ttu-id="a7908-113">Hello seguenti elementi viene classificato come errori del disco:</span><span class="sxs-lookup"><span data-stu-id="a7908-113">hello following items are classified as drive errors:</span></span>

-   <span data-ttu-id="a7908-114">Errori di accesso o lettura hello file manifesto</span><span class="sxs-lookup"><span data-stu-id="a7908-114">Errors in accessing or reading hello manifest file</span></span>

-   <span data-ttu-id="a7908-115">Chiavi BitLocker non corrette</span><span class="sxs-lookup"><span data-stu-id="a7908-115">Incorrect BitLocker keys</span></span>

-   <span data-ttu-id="a7908-116">Errori di lettura/scrittura delle unità</span><span class="sxs-lookup"><span data-stu-id="a7908-116">Drive read/write errors</span></span>

## <a name="blob-errors"></a><span data-ttu-id="a7908-117">Errori del BLOB</span><span class="sxs-lookup"><span data-stu-id="a7908-117">Blob errors</span></span>

<span data-ttu-id="a7908-118">Hello seguenti elementi viene classificato come errori di blob:</span><span class="sxs-lookup"><span data-stu-id="a7908-118">hello following items are classified as blob errors:</span></span>

-   <span data-ttu-id="a7908-119">BLOB o nomi non corretti o in conflitto</span><span class="sxs-lookup"><span data-stu-id="a7908-119">Incorrect or conflicting blob or names</span></span>

-   <span data-ttu-id="a7908-120">File mancanti</span><span class="sxs-lookup"><span data-stu-id="a7908-120">Missing files</span></span>

-   <span data-ttu-id="a7908-121">BLOB non trovato</span><span class="sxs-lookup"><span data-stu-id="a7908-121">Blob not found</span></span>

-   <span data-ttu-id="a7908-122">File troncati (file hello hello disco sono inferiori rispetto a quanto specificato nel manifesto hello)</span><span class="sxs-lookup"><span data-stu-id="a7908-122">Truncated files (hello files on hello disk are smaller than specified in hello manifest)</span></span>

-   <span data-ttu-id="a7908-123">Contenuto dei file danneggiato (per i processi di importazione, rilevato con un checksum MD5 non corrispondente)</span><span class="sxs-lookup"><span data-stu-id="a7908-123">Corrupted file content (for import jobs, detected with an MD5 checksum mismatch)</span></span>

-   <span data-ttu-id="a7908-124">File di metadati e proprietà BLOB danneggiati (rilevati con un checksum MD5 non corrispondente)</span><span class="sxs-lookup"><span data-stu-id="a7908-124">Corrupted blob metadata and property files (detected with an MD5 checksum mismatch)</span></span>

-   <span data-ttu-id="a7908-125">Schema errato per le proprietà del blob hello e/o file di metadati</span><span class="sxs-lookup"><span data-stu-id="a7908-125">Incorrect schema for hello blob properties and/or metadata files</span></span>

<span data-ttu-id="a7908-126">Potrebbero essere presenti i casi in cui alcune parti di un processo di importazione o esportazione non completata correttamente, mentre hello complessiva positivo del processo.</span><span class="sxs-lookup"><span data-stu-id="a7908-126">There may be cases where some parts of an import or export job do not complete successfully, while hello overall job still completes.</span></span> <span data-ttu-id="a7908-127">In questo caso, è possibile caricare o scaricare hello mancante porzioni di dati hello in rete oppure è possibile creare un nuovo dati hello tootransfer di processo.</span><span class="sxs-lookup"><span data-stu-id="a7908-127">In this case, you can either upload or download hello missing pieces of hello data over network, or you can create a new job tootransfer hello data.</span></span> <span data-ttu-id="a7908-128">Vedere hello [riferimento allo strumento di importazione/esportazione di Azure](storage-import-export-tool-how-to-v1.md) toolearn come toorepair hello dati in rete.</span><span class="sxs-lookup"><span data-stu-id="a7908-128">See hello [Azure Import/Export Tool Reference](storage-import-export-tool-how-to-v1.md) toolearn how toorepair hello data over network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a7908-129">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a7908-129">Next steps</span></span>

* [<span data-ttu-id="a7908-130">Tramite l'API REST del servizio importazione/esportazione hello</span><span class="sxs-lookup"><span data-stu-id="a7908-130">Using hello Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
