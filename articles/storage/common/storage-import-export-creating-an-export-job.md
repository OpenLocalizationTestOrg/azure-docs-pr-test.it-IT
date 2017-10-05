---
title: Creare un processo di esportazione per Importazione/Esportazione di Azure | Documentazione Microsoft
description: Informazioni su come creare un processo di esportazione per il servizio Importazione/Esportazione di Microsoft Azure.
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
ms.openlocfilehash: bdeac373aa8270bd9de8f135ec7166d744fd83ae
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="creating-an-export-job-for-the-azure-importexport-service"></a><span data-ttu-id="53d56-103">Creazione di un processo di esportazione per Importazione/Esportazione di Azure</span><span class="sxs-lookup"><span data-stu-id="53d56-103">Creating an export job for the Azure Import/Export service</span></span>
<span data-ttu-id="53d56-104">La creazione di un processo di esportazione per il servizio Importazione/Esportazione di Microsoft Azure con l'API REST prevede i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="53d56-104">Creating an export job for the Microsoft Azure Import/Export service using the REST API involves the following steps:</span></span>

-   <span data-ttu-id="53d56-105">Selezione dei BLOB da esportare.</span><span class="sxs-lookup"><span data-stu-id="53d56-105">Selecting the blobs to export.</span></span>

-   <span data-ttu-id="53d56-106">Acquisizione di una località di spedizione.</span><span class="sxs-lookup"><span data-stu-id="53d56-106">Obtaining a shipping location.</span></span>

-   <span data-ttu-id="53d56-107">Creazione del processo di esportazione.</span><span class="sxs-lookup"><span data-stu-id="53d56-107">Creating the export job.</span></span>

-   <span data-ttu-id="53d56-108">Spedizione delle unità vuote a Microsoft tramite un vettore supportato.</span><span class="sxs-lookup"><span data-stu-id="53d56-108">Shipping your empty drives to Microsoft via a supported carrier service.</span></span>

-   <span data-ttu-id="53d56-109">Aggiornamento del processo di esportazione con le informazioni del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="53d56-109">Updating the export job with the package information.</span></span>

-   <span data-ttu-id="53d56-110">Ricezione delle unità da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="53d56-110">Receiving the drives back from Microsoft.</span></span>

 <span data-ttu-id="53d56-111">Vedere [Uso del servizio Importazione/Esportazione di Microsoft Azure per trasferire i dati all'archivio BLOB](storage-import-export-service.md) per una panoramica del servizio Importazione/Esportazione e un'esercitazione che illustra come usare il [portale di Azure](https://portal.azure.com/) per creare e gestire i processi di importazione ed esportazione.</span><span class="sxs-lookup"><span data-stu-id="53d56-111">See [Using the Windows Azure Import/Export service to Transfer Data to Blob Storage](storage-import-export-service.md) for an overview of the Import/Export service and a tutorial that demonstrates how to use the [Azure portal](https://portal.azure.com/) to create and manage import and export jobs.</span></span>

## <a name="selecting-blobs-to-export"></a><span data-ttu-id="53d56-112">Selezione dei BLOB da esportare</span><span class="sxs-lookup"><span data-stu-id="53d56-112">Selecting blobs to export</span></span>
 <span data-ttu-id="53d56-113">Per creare un processo di esportazione, sarà necessario specificare un elenco di BLOB che si vuole esportare dall'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="53d56-113">To create an export job, you will need to provide a list of blobs that you want to export from your storage account.</span></span> <span data-ttu-id="53d56-114">È possibile selezionare i BLOB da esportare in modi diversi:</span><span class="sxs-lookup"><span data-stu-id="53d56-114">There are a few ways to select blobs to be exported:</span></span>

-   <span data-ttu-id="53d56-115">È possibile usare un percorso BLOB relativo per selezionare un singolo BLOB e tutti gli snapshot.</span><span class="sxs-lookup"><span data-stu-id="53d56-115">You can use a relative blob path to select a single blob and all of its snapshots.</span></span>

-   <span data-ttu-id="53d56-116">È possibile usare un percorso BLOB relativo per selezionare un singolo BLOB escludendo gli snapshot.</span><span class="sxs-lookup"><span data-stu-id="53d56-116">You can use a relative blob path to select a single blob excluding its snapshots.</span></span>

-   <span data-ttu-id="53d56-117">È possibile usare un percorso BLOB relativo e un tempo di snapshot per selezionare un singolo snapshot.</span><span class="sxs-lookup"><span data-stu-id="53d56-117">You can use a relative blob path and a snapshot time to select a single snapshot.</span></span>

-   <span data-ttu-id="53d56-118">È possibile usare un prefisso BLOB per selezionare tutti i BLOB e gli snapshot con il prefisso specificato.</span><span class="sxs-lookup"><span data-stu-id="53d56-118">You can use a blob prefix to select all blobs and snapshots with the given prefix.</span></span>

-   <span data-ttu-id="53d56-119">È possibile esportare tutti i BLOB e gli snapshot nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="53d56-119">You can export all blobs and snapshots in the storage account.</span></span>

 <span data-ttu-id="53d56-120">Per altre informazioni sulla specifica dei BLOB da esportare, vedere l'operazione [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate).</span><span class="sxs-lookup"><span data-stu-id="53d56-120">For more information about specifying blobs to export, see the [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span></span>

## <a name="obtaining-your-shipping-location"></a><span data-ttu-id="53d56-121">Acquisizione della località di spedizione</span><span class="sxs-lookup"><span data-stu-id="53d56-121">Obtaining your shipping location</span></span>
<span data-ttu-id="53d56-122">Prima di creare un processo di esportazione, è necessario ottenere il nome e l'indirizzo di una località di spedizione chiamando l'operazione [Get Location](https://portal.azure.com) o [List Locations](/rest/api/storageimportexport/listlocations).</span><span class="sxs-lookup"><span data-stu-id="53d56-122">Before creating an export job, you need to obtain a shipping location name and address by calling the [Get Location](https://portal.azure.com) or [List Locations](/rest/api/storageimportexport/listlocations) operation.</span></span> <span data-ttu-id="53d56-123">`List Locations` restituirà un elenco di località con gli indirizzi postali.</span><span class="sxs-lookup"><span data-stu-id="53d56-123">`List Locations` will return a list of locations and their mailing addresses.</span></span> <span data-ttu-id="53d56-124">È possibile selezionare una posizione dall'elenco restituito e spedire i dischi rigidi a tale indirizzo.</span><span class="sxs-lookup"><span data-stu-id="53d56-124">You can select a location from the returned list and ship your hard drives to that address.</span></span> <span data-ttu-id="53d56-125">È anche possibile usare l'operazione `Get Location` per ottenere direttamente l'indirizzo di spedizione di una posizione specifica.</span><span class="sxs-lookup"><span data-stu-id="53d56-125">You can also use the `Get Location` operation to obtain the shipping address for a specific location directly.</span></span>

<span data-ttu-id="53d56-126">Seguire i passaggi sotto per ottenere la posizione di spedizione:</span><span class="sxs-lookup"><span data-stu-id="53d56-126">Follow the steps below to obtain the shipping location:</span></span>

-   <span data-ttu-id="53d56-127">Identificare il nome della località dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="53d56-127">Identify the name of the location of your storage account.</span></span> <span data-ttu-id="53d56-128">Si può trovare questo valore nel campo **Località** nel **dashboard** dell'account di archiviazione del portale classico oppure lo si può cercare usando l'operazione dell'API Gestione dei servizi [Get Storage Account Properties](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).</span><span class="sxs-lookup"><span data-stu-id="53d56-128">This value can be found under the **Location** field on the storage account's **Dashboard** in the classic portal or queried for by using the service management API operation [Get Storage Account Properties](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).</span></span>

-   <span data-ttu-id="53d56-129">Recuperare la località disponibile per elaborare questo account di archiviazione chiamando l'operazione `Get Location`.</span><span class="sxs-lookup"><span data-stu-id="53d56-129">Retrieve the location that are available to process this storage account by calling the `Get Location` operation.</span></span>

-   <span data-ttu-id="53d56-130">Se la proprietà `AlternateLocations` della località contiene la località stessa, è possibile usare questa località.</span><span class="sxs-lookup"><span data-stu-id="53d56-130">If the `AlternateLocations` property of the location contains the location itself, then it is okay to use this location.</span></span> <span data-ttu-id="53d56-131">In caso contrario, chiamare di nuovo l'operazione `Get Location` con una delle posizione alternative.</span><span class="sxs-lookup"><span data-stu-id="53d56-131">Otherwise, call the `Get Location` operation again with one of the alternate locations.</span></span> <span data-ttu-id="53d56-132">La località originale potrebbe essere chiusa temporaneamente per manutenzione.</span><span class="sxs-lookup"><span data-stu-id="53d56-132">The original location might be temporarily closed for maintenance.</span></span>

## <a name="creating-the-export-job"></a><span data-ttu-id="53d56-133">Creazione del processo di esportazione</span><span class="sxs-lookup"><span data-stu-id="53d56-133">Creating the export job</span></span>
 <span data-ttu-id="53d56-134">Per creare il processo di esportazione, chiamare l'operazione [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate).</span><span class="sxs-lookup"><span data-stu-id="53d56-134">To create the export job, call the [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span></span> <span data-ttu-id="53d56-135">Sarà necessario specificare le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="53d56-135">You will need to provide the following information:</span></span>

-   <span data-ttu-id="53d56-136">Un nome per il processo.</span><span class="sxs-lookup"><span data-stu-id="53d56-136">A name for the job.</span></span>

-   <span data-ttu-id="53d56-137">nome dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="53d56-137">The storage account name.</span></span>

-   <span data-ttu-id="53d56-138">Il nome della località di spedizione, ottenuto nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="53d56-138">The shipping location name, obtained in the previous step.</span></span>

-   <span data-ttu-id="53d56-139">Un tipo di processo (esportazione).</span><span class="sxs-lookup"><span data-stu-id="53d56-139">A job type (Export).</span></span>

-   <span data-ttu-id="53d56-140">L'indirizzo mittente dove inviare le unità al termine del processo di esportazione.</span><span class="sxs-lookup"><span data-stu-id="53d56-140">The return address where the drives should be sent after the export job has completed.</span></span>

-   <span data-ttu-id="53d56-141">L'elenco di BLOB (o i prefissi BLOB) da esportare.</span><span class="sxs-lookup"><span data-stu-id="53d56-141">The list of blobs (or blob prefixes) to be exported.</span></span>

## <a name="shipping-your-drives"></a><span data-ttu-id="53d56-142">Spedizione delle unità</span><span class="sxs-lookup"><span data-stu-id="53d56-142">Shipping your drives</span></span>
 <span data-ttu-id="53d56-143">Usare ora lo strumento Importazione/Esportazione di Azure per determinare il numero di unità necessarie da inviare, in base ai BLOB selezionati per l'esportazione e alle dimensioni delle unità.</span><span class="sxs-lookup"><span data-stu-id="53d56-143">Next, use the Azure Import/Export Tool to determine the number of drives you need to send, based on the blobs you have selected to be exported and the drive size.</span></span> <span data-ttu-id="53d56-144">Per i dettagli vedere [Azure Import/Export Tool Reference](storage-import-export-tool-how-to-v1.md) (Informazioni di riferimento sullo strumento Importazione/Esportazione di Azure).</span><span class="sxs-lookup"><span data-stu-id="53d56-144">See the [Azure Import/Export Tool Reference](storage-import-export-tool-how-to-v1.md) for details.</span></span>

 <span data-ttu-id="53d56-145">Inserire le unità in un singolo pacchetto e spedirle all'indirizzo ottenuto nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="53d56-145">Package the drives in a single package and ship them to the address obtained in the earlier step.</span></span> <span data-ttu-id="53d56-146">Prendere nota del numero di tracciabilità del pacchetto per il passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="53d56-146">Note the tracking number of your package for the next step.</span></span>

> [!NOTE]
>  <span data-ttu-id="53d56-147">È necessario spedire le unità con un vettore supportato, che fornirà un numero di tracciabilità per il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="53d56-147">You must ship your drives via a supported carrier service, which will provide a tracking number for your package.</span></span>

## <a name="updating-the-export-job-with-your-package-information"></a><span data-ttu-id="53d56-148">Aggiornamento del processo di esportazione con le informazioni del pacchetto</span><span class="sxs-lookup"><span data-stu-id="53d56-148">Updating the export job with your package information</span></span>
 <span data-ttu-id="53d56-149">Dopo avere ottenuto il numero di tracciabilità, chiamare l'operazione [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) per aggiornare il nome del vettore e il numero di tracciabilità per il processo.</span><span class="sxs-lookup"><span data-stu-id="53d56-149">After you have your tracking number, call the [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operation to updated the carrier name and tracking number for the job.</span></span> <span data-ttu-id="53d56-150">È facoltativamente possibile specificare anche il numero di unità, l'indirizzo mittente e la data di spedizione.</span><span class="sxs-lookup"><span data-stu-id="53d56-150">You can optionally specify the number of drives, the return address, and the shipping date as well.</span></span>

## <a name="receiving-the-package"></a><span data-ttu-id="53d56-151">Ricezione del pacchetto</span><span class="sxs-lookup"><span data-stu-id="53d56-151">Receiving the package</span></span>
 <span data-ttu-id="53d56-152">Dopo che il processo di esportazione è stato elaborato, le unità verranno restituite all'utente con i dati crittografati.</span><span class="sxs-lookup"><span data-stu-id="53d56-152">After your export job has been processed, your drives will be returned to you with your encrypted data.</span></span> <span data-ttu-id="53d56-153">È possibile recuperare la chiave BitLocker per ogni unità chiamando l'operazione [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get).</span><span class="sxs-lookup"><span data-stu-id="53d56-153">You can retrieve the BitLocker key for each of the drives by calling the [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) operation.</span></span> <span data-ttu-id="53d56-154">È quindi possibile sbloccare l'unità usando la chiave.</span><span class="sxs-lookup"><span data-stu-id="53d56-154">You can then unlock the drive using the key.</span></span> <span data-ttu-id="53d56-155">Il file manifesto di ogni unità contiene l'elenco di file dell'unità, oltre all'indirizzo BLOB originale per ogni file.</span><span class="sxs-lookup"><span data-stu-id="53d56-155">The drive manifest file on each drive contains the list of files on the drive, as well as the original blob address for each file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="53d56-156">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="53d56-156">Next steps</span></span>

* [<span data-ttu-id="53d56-157">Uso dell'API REST del servizio Importazione/Esportazione</span><span class="sxs-lookup"><span data-stu-id="53d56-157">Using the Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
