---
title: aaaCreate un'esportazione processo di importazione/esportazione di Azure | Documenti Microsoft
description: Informazioni su come toocreate un'esportazione del processo per il servizio di importazione/esportazione di Microsoft Azure hello.
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 613d480b-a8ef-4b28-8f54-54174d59b3f4
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 4a10b42cc86dbf3bcea3a515bc065e2259228ef9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-export-job-for-hello-azure-importexport-service"></a><span data-ttu-id="397b2-103">Creazione di un processo di esportazione per hello servizio importazione/esportazione di Azure</span><span class="sxs-lookup"><span data-stu-id="397b2-103">Creating an export job for hello Azure Import/Export service</span></span>
<span data-ttu-id="397b2-104">La creazione di un processo di esportazione per il servizio di importazione/esportazione di Microsoft Azure hello utilizzando hello API REST prevede hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="397b2-104">Creating an export job for hello Microsoft Azure Import/Export service using hello REST API involves hello following steps:</span></span>

-   <span data-ttu-id="397b2-105">Selezione di hello BLOB tooexport.</span><span class="sxs-lookup"><span data-stu-id="397b2-105">Selecting hello blobs tooexport.</span></span>

-   <span data-ttu-id="397b2-106">Acquisizione di una località di spedizione.</span><span class="sxs-lookup"><span data-stu-id="397b2-106">Obtaining a shipping location.</span></span>

-   <span data-ttu-id="397b2-107">Creazione del processo di esportazione hello.</span><span class="sxs-lookup"><span data-stu-id="397b2-107">Creating hello export job.</span></span>

-   <span data-ttu-id="397b2-108">Spedizione tooMicrosoft le unità vuote tramite un servizio vettore supportato.</span><span class="sxs-lookup"><span data-stu-id="397b2-108">Shipping your empty drives tooMicrosoft via a supported carrier service.</span></span>

-   <span data-ttu-id="397b2-109">Aggiornamento del processo di esportazione hello con informazioni sul pacchetto hello.</span><span class="sxs-lookup"><span data-stu-id="397b2-109">Updating hello export job with hello package information.</span></span>

-   <span data-ttu-id="397b2-110">Ricezione di hello unità da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="397b2-110">Receiving hello drives back from Microsoft.</span></span>

 <span data-ttu-id="397b2-111">Vedere [tramite servizio di importazione/esportazione di Azure hello, dati tooTransfer tooBlob archiviazione](storage-import-export-service.md) per una panoramica del servizio di importazione/esportazione hello e un'esercitazione che illustra come hello toouse [portale di Azure](https://portal.azure.com/) toocreate e gestire l'importazione e i processi di esportazione.</span><span class="sxs-lookup"><span data-stu-id="397b2-111">See [Using hello Windows Azure Import/Export service tooTransfer Data tooBlob Storage](storage-import-export-service.md) for an overview of hello Import/Export service and a tutorial that demonstrates how toouse hello [Azure portal](https://portal.azure.com/) toocreate and manage import and export jobs.</span></span>

## <a name="selecting-blobs-tooexport"></a><span data-ttu-id="397b2-112">Selezione di BLOB tooexport</span><span class="sxs-lookup"><span data-stu-id="397b2-112">Selecting blobs tooexport</span></span>
 <span data-ttu-id="397b2-113">toocreate un processo di esportazione, sarà necessario tooprovide un elenco di blob che si desidera tooexport dall'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="397b2-113">toocreate an export job, you will need tooprovide a list of blobs that you want tooexport from your storage account.</span></span> <span data-ttu-id="397b2-114">Esistono alcuni modi tooselect BLOB toobe esportate:</span><span class="sxs-lookup"><span data-stu-id="397b2-114">There are a few ways tooselect blobs toobe exported:</span></span>

-   <span data-ttu-id="397b2-115">È possibile utilizzare un tooselect percorso blob relativo a un singolo blob e tutti i relativi snapshot.</span><span class="sxs-lookup"><span data-stu-id="397b2-115">You can use a relative blob path tooselect a single blob and all of its snapshots.</span></span>

-   <span data-ttu-id="397b2-116">È possibile utilizzare un tooselect percorso blob relativo di un singolo blob esclusi i relativi snapshot.</span><span class="sxs-lookup"><span data-stu-id="397b2-116">You can use a relative blob path tooselect a single blob excluding its snapshots.</span></span>

-   <span data-ttu-id="397b2-117">È possibile utilizzare un percorso blob relativo e un tooselect tempo snapshot un singolo snapshot.</span><span class="sxs-lookup"><span data-stu-id="397b2-117">You can use a relative blob path and a snapshot time tooselect a single snapshot.</span></span>

-   <span data-ttu-id="397b2-118">È possibile utilizzare un tooselect prefisso blob tutti i BLOB e snapshot con hello prefisso specificato.</span><span class="sxs-lookup"><span data-stu-id="397b2-118">You can use a blob prefix tooselect all blobs and snapshots with hello given prefix.</span></span>

-   <span data-ttu-id="397b2-119">È possibile esportare tutti i BLOB e snapshot nell'account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="397b2-119">You can export all blobs and snapshots in hello storage account.</span></span>

 <span data-ttu-id="397b2-120">Per ulteriori informazioni sulla specifica BLOB tooexport, vedere hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operazione.</span><span class="sxs-lookup"><span data-stu-id="397b2-120">For more information about specifying blobs tooexport, see hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span></span>

## <a name="obtaining-your-shipping-location"></a><span data-ttu-id="397b2-121">Acquisizione della località di spedizione</span><span class="sxs-lookup"><span data-stu-id="397b2-121">Obtaining your shipping location</span></span>
<span data-ttu-id="397b2-122">Prima di creare un processo di esportazione, è necessario tooobtain il nome di un'ubicazione di spedizione e l'indirizzo dal chiamante hello [ottenere percorso](https://portal.azure.com) o [List Locations](/rest/api/storageimportexport/listlocations) operazione.</span><span class="sxs-lookup"><span data-stu-id="397b2-122">Before creating an export job, you need tooobtain a shipping location name and address by calling hello [Get Location](https://portal.azure.com) or [List Locations](/rest/api/storageimportexport/listlocations) operation.</span></span> <span data-ttu-id="397b2-123">`List Locations` restituirà un elenco di località con gli indirizzi postali.</span><span class="sxs-lookup"><span data-stu-id="397b2-123">`List Locations` will return a list of locations and their mailing addresses.</span></span> <span data-ttu-id="397b2-124">È possibile selezionare un'ubicazione hello elenco restituito e spedire il tuo indirizzo toothat unità disco rigido.</span><span class="sxs-lookup"><span data-stu-id="397b2-124">You can select a location from hello returned list and ship your hard drives toothat address.</span></span> <span data-ttu-id="397b2-125">È inoltre possibile utilizzare hello `Get Location` hello tooobtain operazione indirizzo per una determinata ubicazione di spedizione direttamente.</span><span class="sxs-lookup"><span data-stu-id="397b2-125">You can also use hello `Get Location` operation tooobtain hello shipping address for a specific location directly.</span></span>

<span data-ttu-id="397b2-126">Seguire i passaggi di hello sotto tooobtain ubicazione di spedizione hello:</span><span class="sxs-lookup"><span data-stu-id="397b2-126">Follow hello steps below tooobtain hello shipping location:</span></span>

-   <span data-ttu-id="397b2-127">Identificare il nome di hello del percorso hello dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="397b2-127">Identify hello name of hello location of your storage account.</span></span> <span data-ttu-id="397b2-128">Questo valore è reperibile nella hello **percorso** campo dell'account di archiviazione hello **Dashboard** classica hello portale o eseguendo una query utilizzando Gestione servizio hello operazione API [ottenere Proprietà Account di archiviazione](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).</span><span class="sxs-lookup"><span data-stu-id="397b2-128">This value can be found under hello **Location** field on hello storage account's **Dashboard** in hello classic portal or queried for by using hello service management API operation [Get Storage Account Properties](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).</span></span>

-   <span data-ttu-id="397b2-129">Recuperare questo account di archiviazione percorso hello che sono disponibili tooprocess hello chiamante `Get Location` operazione.</span><span class="sxs-lookup"><span data-stu-id="397b2-129">Retrieve hello location that are available tooprocess this storage account by calling hello `Get Location` operation.</span></span>

-   <span data-ttu-id="397b2-130">Se hello `AlternateLocations` proprietà della posizione di hello contiene percorso hello stesso, quindi è corretto toouse questo percorso.</span><span class="sxs-lookup"><span data-stu-id="397b2-130">If hello `AlternateLocations` property of hello location contains hello location itself, then it is okay toouse this location.</span></span> <span data-ttu-id="397b2-131">In caso contrario, chiamare hello `Get Location` operazione con una delle posizioni alternative hello.</span><span class="sxs-lookup"><span data-stu-id="397b2-131">Otherwise, call hello `Get Location` operation again with one of hello alternate locations.</span></span> <span data-ttu-id="397b2-132">percorso originale Hello potrebbe essere chiusa temporaneamente per la manutenzione.</span><span class="sxs-lookup"><span data-stu-id="397b2-132">hello original location might be temporarily closed for maintenance.</span></span>

## <a name="creating-hello-export-job"></a><span data-ttu-id="397b2-133">Creazione del processo di esportazione hello</span><span class="sxs-lookup"><span data-stu-id="397b2-133">Creating hello export job</span></span>
 <span data-ttu-id="397b2-134">processo di esportazione hello toocreate, chiamata hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operazione.</span><span class="sxs-lookup"><span data-stu-id="397b2-134">toocreate hello export job, call hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span></span> <span data-ttu-id="397b2-135">È necessario hello tooprovide le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="397b2-135">You will need tooprovide hello following information:</span></span>

-   <span data-ttu-id="397b2-136">Un nome per il processo di hello.</span><span class="sxs-lookup"><span data-stu-id="397b2-136">A name for hello job.</span></span>

-   <span data-ttu-id="397b2-137">nome di account di archiviazione Hello.</span><span class="sxs-lookup"><span data-stu-id="397b2-137">hello storage account name.</span></span>

-   <span data-ttu-id="397b2-138">Hello shipping nome dell'ubicazione, ottenuto nel passaggio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="397b2-138">hello shipping location name, obtained in hello previous step.</span></span>

-   <span data-ttu-id="397b2-139">Un tipo di processo (esportazione).</span><span class="sxs-lookup"><span data-stu-id="397b2-139">A job type (Export).</span></span>

-   <span data-ttu-id="397b2-140">indirizzo del mittente Hello dove hello unità devono essere inviate al termine il processo di esportazione hello.</span><span class="sxs-lookup"><span data-stu-id="397b2-140">hello return address where hello drives should be sent after hello export job has completed.</span></span>

-   <span data-ttu-id="397b2-141">Hello toobe elenco di BLOB (o prefissi di blob) esportato.</span><span class="sxs-lookup"><span data-stu-id="397b2-141">hello list of blobs (or blob prefixes) toobe exported.</span></span>

## <a name="shipping-your-drives"></a><span data-ttu-id="397b2-142">Spedizione delle unità</span><span class="sxs-lookup"><span data-stu-id="397b2-142">Shipping your drives</span></span>
 <span data-ttu-id="397b2-143">Successivamente, utilizzare hello strumento di importazione/esportazione di Azure toodetermine hello numero di unità che è necessario toosend, in base a BLOB hello selezionati toobe esportato e hello dimensioni dell'unità.</span><span class="sxs-lookup"><span data-stu-id="397b2-143">Next, use hello Azure Import/Export Tool toodetermine hello number of drives you need toosend, based on hello blobs you have selected toobe exported and hello drive size.</span></span> <span data-ttu-id="397b2-144">Vedere hello [riferimento allo strumento di importazione/esportazione di Azure](storage-import-export-tool-how-to-v1.md) per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="397b2-144">See hello [Azure Import/Export Tool Reference](storage-import-export-tool-how-to-v1.md) for details.</span></span>

 <span data-ttu-id="397b2-145">Unità di hello pacchetto in un singolo pacchetto e spedirle toohello indirizzo ottenuto nel hello passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="397b2-145">Package hello drives in a single package and ship them toohello address obtained in hello earlier step.</span></span> <span data-ttu-id="397b2-146">Si noti hello tenere traccia del numero del pacchetto per il passaggio successivo hello.</span><span class="sxs-lookup"><span data-stu-id="397b2-146">Note hello tracking number of your package for hello next step.</span></span>

> [!NOTE]
>  <span data-ttu-id="397b2-147">È necessario spedire le unità con un vettore supportato, che fornirà un numero di tracciabilità per il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="397b2-147">You must ship your drives via a supported carrier service, which will provide a tracking number for your package.</span></span>

## <a name="updating-hello-export-job-with-your-package-information"></a><span data-ttu-id="397b2-148">Aggiornamento del processo di esportazione di hello con le informazioni sul pacchetto</span><span class="sxs-lookup"><span data-stu-id="397b2-148">Updating hello export job with your package information</span></span>
 <span data-ttu-id="397b2-149">Dopo aver ottenuto il numero di tracciabilità, chiamare hello [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operazione tooupdated hello vettore nome e il numero di hello processo di rilevamento.</span><span class="sxs-lookup"><span data-stu-id="397b2-149">After you have your tracking number, call hello [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operation tooupdated hello carrier name and tracking number for hello job.</span></span> <span data-ttu-id="397b2-150">È possibile specificare facoltativamente il numero di hello di unità, l'indirizzo restituito hello e data di spedizione hello.</span><span class="sxs-lookup"><span data-stu-id="397b2-150">You can optionally specify hello number of drives, hello return address, and hello shipping date as well.</span></span>

## <a name="receiving-hello-package"></a><span data-ttu-id="397b2-151">Ricezione di pacchetti hello</span><span class="sxs-lookup"><span data-stu-id="397b2-151">Receiving hello package</span></span>
 <span data-ttu-id="397b2-152">Dopo il processo di esportazione è stato elaborato, le unità verranno restituite tooyou con i dati crittografati.</span><span class="sxs-lookup"><span data-stu-id="397b2-152">After your export job has been processed, your drives will be returned tooyou with your encrypted data.</span></span> <span data-ttu-id="397b2-153">È possibile recuperare la chiave di BitLocker hello per ognuna delle unità hello dal chiamante hello [recupero del processo](/rest/api/storageimportexport/jobs#Jobs_Get) operazione.</span><span class="sxs-lookup"><span data-stu-id="397b2-153">You can retrieve hello BitLocker key for each of hello drives by calling hello [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) operation.</span></span> <span data-ttu-id="397b2-154">È quindi possibile sbloccare l'unità hello hello chiave.</span><span class="sxs-lookup"><span data-stu-id="397b2-154">You can then unlock hello drive using hello key.</span></span> <span data-ttu-id="397b2-155">file manifesto dell'unità di Hello su ciascuna unità contiene hello elenco di file in unità hello, come indirizzo blob originale hello per ogni file.</span><span class="sxs-lookup"><span data-stu-id="397b2-155">hello drive manifest file on each drive contains hello list of files on hello drive, as well as hello original blob address for each file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="397b2-156">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="397b2-156">Next steps</span></span>

* [<span data-ttu-id="397b2-157">Tramite l'API REST del servizio importazione/esportazione hello</span><span class="sxs-lookup"><span data-stu-id="397b2-157">Using hello Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
