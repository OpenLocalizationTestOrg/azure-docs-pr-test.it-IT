---
title: Creare un processo di importazione per Importazione/Esportazione di Azure | Documentazione Microsoft
description: Informazioni su come creare un'importazione per il servizio Importazione/Esportazione di Microsoft Azure.
author: muralikk
manager: syadav
editor: syadav
services: storage
documentationcenter: 
ms.assetid: 8b886e83-6148-4149-9d0f-5d48ec822475
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: d373d2a0e601f2796719fc5efb8761f276ab24d9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="creating-an-import-job-for-the-azure-importexport-service"></a><span data-ttu-id="c9086-103">Creazione di un processo di importazione per Importazione/Esportazione di Azure</span><span class="sxs-lookup"><span data-stu-id="c9086-103">Creating an import job for the Azure Import/Export service</span></span>

<span data-ttu-id="c9086-104">La creazione di un processo di importazione per il servizio di Importazione/Esportazione di Microsoft Azure utilizzando l'API REST prevede i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="c9086-104">Creating an import job for the Microsoft Azure Import/Export service using the REST API involves the following steps:</span></span>

-   <span data-ttu-id="c9086-105">Preparazione delle unità con lo strumento Importazione/Esportazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="c9086-105">Preparing drives with the Azure Import/Export Tool.</span></span>

-   <span data-ttu-id="c9086-106">Ottenimento della posizione a cui si desidera spedire l'unità.</span><span class="sxs-lookup"><span data-stu-id="c9086-106">Obtaining the location to which to ship the drive.</span></span>

-   <span data-ttu-id="c9086-107">Creazione del processo di importazione.</span><span class="sxs-lookup"><span data-stu-id="c9086-107">Creating the import job.</span></span>

-   <span data-ttu-id="c9086-108">Spedizione delle unità vuote a Microsoft tramite un vettore supportato.</span><span class="sxs-lookup"><span data-stu-id="c9086-108">Shipping the drives to Microsoft via a supported carrier service.</span></span>

-   <span data-ttu-id="c9086-109">Aggiornamento del processo di importazione con i dettagli di spedizione.</span><span class="sxs-lookup"><span data-stu-id="c9086-109">Updating the import job with the shipping details.</span></span>

 <span data-ttu-id="c9086-110">Vedere [Uso del servizio Importazione/Esportazione di Microsoft Azure per trasferire i dati nell'archiviazione BLOB](storage-import-export-service.md) per una panoramica del servizio Importazione/Esportazione e un'esercitazione che illustra come usare il [portale di Azure](https://portal.azure.com/) per creare e gestire i processi di importazione ed esportazione.</span><span class="sxs-lookup"><span data-stu-id="c9086-110">See [Using the Microsoft Azure Import/Export service to Transfer Data to Blob Storage](storage-import-export-service.md) for an overview of the Import/Export service and a tutorial that demonstrates how to use the [Azure  portal](https://portal.azure.com/) to create and manage import and export jobs.</span></span>

## <a name="preparing-drives-with-the-azure-importexport-tool"></a><span data-ttu-id="c9086-111">Preparazione delle unità con lo strumento di Importazione/Esportazione di Azure</span><span class="sxs-lookup"><span data-stu-id="c9086-111">Preparing drives with the Azure Import/Export Tool</span></span>

<span data-ttu-id="c9086-112">I passaggi per preparare le unità per un processo di importazione sono uguali se si crea il processo tramite il portale o l'API REST.</span><span class="sxs-lookup"><span data-stu-id="c9086-112">The steps to prepare drives for an import job are the same whether you create the jobvia the portal or via the REST API.</span></span>

<span data-ttu-id="c9086-113">Di seguito è riportata una breve panoramica della preparazione dell'unità.</span><span class="sxs-lookup"><span data-stu-id="c9086-113">Below is a brief overview of drive preparation.</span></span> <span data-ttu-id="c9086-114">Per istruzioni complete, vedere il [Riferimento dello strumento di importazione/esportazione di Azure](storage-import-export-tool-how-to-v1.md).</span><span class="sxs-lookup"><span data-stu-id="c9086-114">Refer to the [Azure Import-ExportTool Reference](storage-import-export-tool-how-to-v1.md) for complete instructions.</span></span> <span data-ttu-id="c9086-115">È possibile scaricare lo strumento Importazione/Esportazione di Azure [qui](http://go.microsoft.com/fwlink/?LinkID=301900).</span><span class="sxs-lookup"><span data-stu-id="c9086-115">You can download the Azure Import/Export Tool [here](http://go.microsoft.com/fwlink/?LinkID=301900).</span></span>

<span data-ttu-id="c9086-116">La preparazione dell'unità comporta:</span><span class="sxs-lookup"><span data-stu-id="c9086-116">Preparing your drive involves:</span></span>

-   <span data-ttu-id="c9086-117">Identificazione dei dati da importare.</span><span class="sxs-lookup"><span data-stu-id="c9086-117">Identifying the data to be imported.</span></span>

-   <span data-ttu-id="c9086-118">Identificazione dei BLOB di destinazione in Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="c9086-118">Identifying the destination blobs in Windows Azure Storage.</span></span>

-   <span data-ttu-id="c9086-119">Uso dello strumento Importazione/Esportazione di Azure per copiare i dati in uno o più dischi rigidi.</span><span class="sxs-lookup"><span data-stu-id="c9086-119">Using the Azure Import/Export Tool to copy your data to one or more hard drives.</span></span>

 <span data-ttu-id="c9086-120">Lo strumento Importazione/Esportazione di Azure genererà anche un file manifesto per ciascuna unità preparata.</span><span class="sxs-lookup"><span data-stu-id="c9086-120">The Azure Import/Export Tool will also generate a manifest file for each of the drives as it is prepared.</span></span> <span data-ttu-id="c9086-121">Contiene un file manifesto:</span><span class="sxs-lookup"><span data-stu-id="c9086-121">A manifest file contains:</span></span>

-   <span data-ttu-id="c9086-122">Enumerazione di tutti i file destinati al caricamento e il mapping tra questi file sui BLOB.</span><span class="sxs-lookup"><span data-stu-id="c9086-122">An enumeration of all the files intended for upload and the mappings from these files to blobs.</span></span>

-   <span data-ttu-id="c9086-123">Checksum dei segmenti di ciascun file.</span><span class="sxs-lookup"><span data-stu-id="c9086-123">Checksums of the segments of each file.</span></span>

-   <span data-ttu-id="c9086-124">Informazioni sui metadati e proprietà da associare a ogni BLOB.</span><span class="sxs-lookup"><span data-stu-id="c9086-124">Information about the metadata and properties to associate with each blob.</span></span>

-   <span data-ttu-id="c9086-125">Elenco delle azioni da intraprendere se un BLOB che viene caricato ha lo stesso nome di un BLOB esistente nel contenitore.</span><span class="sxs-lookup"><span data-stu-id="c9086-125">A listing of the action to take if a blob that is being uploaded has the same name as an existing blob in the container.</span></span> <span data-ttu-id="c9086-126">Le opzioni possibili sono: a) sovrascrivere il BLOB con il file, b) mantenere il BLOB esistente e ignorare il caricamento del file, c) aggiungere un suffisso al nome in modo che non sia in conflitto con altri file.</span><span class="sxs-lookup"><span data-stu-id="c9086-126">Possible options are: a) overwrite the blob with the file, b) keep the existing blob and skip uploading the file, c) append a suffix to the name so that it does not conflict with other files.</span></span>

## <a name="obtaining-your-shipping-location"></a><span data-ttu-id="c9086-127">Acquisizione della località di spedizione</span><span class="sxs-lookup"><span data-stu-id="c9086-127">Obtaining your shipping location</span></span>

<span data-ttu-id="c9086-128">Prima di creare un processo di importazione, è necessario ottenere il nome e l'indirizzo di una posizione di spedizione chiamando l'operazione [List Locations](/rest/api/storageimportexport/listlocations) (Elenca posizioni).</span><span class="sxs-lookup"><span data-stu-id="c9086-128">Before creating an import job, you need to obtain a shipping location name and address by calling the [List Locations](/rest/api/storageimportexport/listlocations) operation.</span></span> <span data-ttu-id="c9086-129">`List Locations` restituirà un elenco di posizione con gli indirizzi postali.</span><span class="sxs-lookup"><span data-stu-id="c9086-129">`List Locations` will return a list of locations and their mailing addresses.</span></span> <span data-ttu-id="c9086-130">È possibile selezionare una posizione dall'elenco restituito e spedire i dischi rigidi a tale indirizzo.</span><span class="sxs-lookup"><span data-stu-id="c9086-130">You can select a location from the returned list and ship your hard drives to that address.</span></span> <span data-ttu-id="c9086-131">È anche possibile usare l'operazione `Get Location` per ottenere direttamente l'indirizzo di spedizione di una posizione specifica.</span><span class="sxs-lookup"><span data-stu-id="c9086-131">You can also use the `Get Location` operation to obtain the shipping address for a specific location directly.</span></span>

 <span data-ttu-id="c9086-132">Seguire i passaggi sotto per ottenere la posizione di spedizione:</span><span class="sxs-lookup"><span data-stu-id="c9086-132">Follow the steps below to obtain the shipping location:</span></span>

-   <span data-ttu-id="c9086-133">Identificare il nome della località dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="c9086-133">Identify the name of the location of your storage account.</span></span> <span data-ttu-id="c9086-134">Si può trovare questo valore nel campo **Posizione** nel **dashboard** dell'account di archiviazione del portale di Azure oppure lo si può cercare usando l'operazione dell'API Gestione dei servizi [Get Storage Account Properties](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).</span><span class="sxs-lookup"><span data-stu-id="c9086-134">This value can be found under the **Location** field on the storage account's **Dashboard** in the Azure portal or queried for by using the service management API operation [Get Storage Account Properties](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).</span></span>

-   <span data-ttu-id="c9086-135">Recuperare la posizione disponibile per elaborare questo account di archiviazione chiamando l'operazione `Get Location`.</span><span class="sxs-lookup"><span data-stu-id="c9086-135">Retrieve the location that is available to process this storage account by calling the `Get Location` operation.</span></span>

-   <span data-ttu-id="c9086-136">Se la proprietà `AlternateLocations` della posizione contiene la posizione stessa, è possibile usare questa posizione.</span><span class="sxs-lookup"><span data-stu-id="c9086-136">If the `AlternateLocations` property of the location contains the location itself, then it is okay to use this location.</span></span> <span data-ttu-id="c9086-137">In caso contrario, chiamare di nuovo l'operazione `Get Location` con una delle posizione alternative.</span><span class="sxs-lookup"><span data-stu-id="c9086-137">Otherwise, call the `Get Location` operation again with one of the alternate locations.</span></span> <span data-ttu-id="c9086-138">La località originale potrebbe essere chiusa temporaneamente per manutenzione.</span><span class="sxs-lookup"><span data-stu-id="c9086-138">The original location might be temporarily closed for maintenance.</span></span>

## <a name="creating-the-import-job"></a><span data-ttu-id="c9086-139">Creazione del processo di importazione</span><span class="sxs-lookup"><span data-stu-id="c9086-139">Creating the import job</span></span>
<span data-ttu-id="c9086-140">Per creare il processo di importazione, chiamare l'operazione [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) (Inserisci processo).</span><span class="sxs-lookup"><span data-stu-id="c9086-140">To create the import job, call the [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span></span> <span data-ttu-id="c9086-141">Sarà necessario specificare le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="c9086-141">You will need to provide the following information:</span></span>

-   <span data-ttu-id="c9086-142">Un nome per il processo.</span><span class="sxs-lookup"><span data-stu-id="c9086-142">A name for the job.</span></span>

-   <span data-ttu-id="c9086-143">nome dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="c9086-143">The storage account name.</span></span>

-   <span data-ttu-id="c9086-144">Il nome della posizione di spedizione, ottenuto nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="c9086-144">The shipping location name, obtained from the previous step.</span></span>

-   <span data-ttu-id="c9086-145">Un tipo di processo (importazione).</span><span class="sxs-lookup"><span data-stu-id="c9086-145">A job type (Import).</span></span>

-   <span data-ttu-id="c9086-146">L'indirizzo mittente dove inviare le unità al termine del processo di importazione.</span><span class="sxs-lookup"><span data-stu-id="c9086-146">The return address where the drives should be sent after the import job has completed.</span></span>

-   <span data-ttu-id="c9086-147">Elenco delle unità nel processo.</span><span class="sxs-lookup"><span data-stu-id="c9086-147">The list of drives in the job.</span></span> <span data-ttu-id="c9086-148">Per ogni unità, è necessario includere le seguenti informazioni ottenute durante la fase di preparazione dell'unità:</span><span class="sxs-lookup"><span data-stu-id="c9086-148">For each drive, you must include the following information that was obtained during the drive preparation step:</span></span>

    -   <span data-ttu-id="c9086-149">ID dell'unità</span><span class="sxs-lookup"><span data-stu-id="c9086-149">The drive Id</span></span>

    -   <span data-ttu-id="c9086-150">La chiave di BitLocker</span><span class="sxs-lookup"><span data-stu-id="c9086-150">The BitLocker key</span></span>

    -   <span data-ttu-id="c9086-151">Il percorso relativo del file manifesto nel disco rigido</span><span class="sxs-lookup"><span data-stu-id="c9086-151">The manifest file relative path on the hard drive</span></span>

    -   <span data-ttu-id="c9086-152">Hash MD5 del file manifesto codificato in base 16</span><span class="sxs-lookup"><span data-stu-id="c9086-152">The Base16 encoded manifest file MD5 hash</span></span>

## <a name="shipping-your-drives"></a><span data-ttu-id="c9086-153">Spedizione delle unità</span><span class="sxs-lookup"><span data-stu-id="c9086-153">Shipping your drives</span></span>
<span data-ttu-id="c9086-154">È necessario spedire le unità all'indirizzo ottenuto nel passaggio precedente e fornire il numero di tracciabilità del pacchetto nel servizio di Importazione/Esportazione.</span><span class="sxs-lookup"><span data-stu-id="c9086-154">You must ship your drives to the address that you obtained from the previous step, and you must provide the Import/Export service with the tracking number of the package.</span></span>

> [!NOTE]
>  <span data-ttu-id="c9086-155">È necessario spedire le unità con un vettore supportato, che fornirà un numero di tracciabilità per il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="c9086-155">You must ship your drives via a supported carrier service, which will provide a tracking number for your package.</span></span>

## <a name="updating-the-import-job-with-your-shipping-information"></a><span data-ttu-id="c9086-156">Aggiornamento del processo di importazione con le informazioni sulla spedizione</span><span class="sxs-lookup"><span data-stu-id="c9086-156">Updating the import job with your shipping information</span></span>
<span data-ttu-id="c9086-157">Dopo avere ottenuto il numero di tracciabilità, chiamare l'operazione [Update Job Properties](/api/storageimportexport/jobs#Jobs_Update) (Aggiorna proprietà processo) per aggiornare il nome del vettore, il numero di tracciabilità per il processo e il numero di account del vettore per la spedizione per reso.</span><span class="sxs-lookup"><span data-stu-id="c9086-157">After you have your tracking number, call the [Update Job Properties](/api/storageimportexport/jobs#Jobs_Update) operation to update the shipping carrier name, the tracking number for the job, and the carrier account number for return shipping.</span></span> <span data-ttu-id="c9086-158">Facoltativamente è possibile specificare il numero di unità e la data di spedizione.</span><span class="sxs-lookup"><span data-stu-id="c9086-158">You can optionally specify the number of drives and the shipping date as well.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c9086-159">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c9086-159">Next steps</span></span>

* [<span data-ttu-id="c9086-160">Uso dell'API REST del servizio Importazione/Esportazione</span><span class="sxs-lookup"><span data-stu-id="c9086-160">Using the Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
