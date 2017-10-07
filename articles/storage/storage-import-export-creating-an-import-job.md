---
title: aaaCreate un processo di importazione per importazione/esportazione di Azure | Documenti Microsoft
description: Informazioni su come toocreate un'importazione per hello servizio importazione/esportazione di Microsoft Azure.
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
ms.openlocfilehash: da974c33a3688bb5e2412c8bfcbeca704096c2fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-import-job-for-hello-azure-importexport-service"></a><span data-ttu-id="81888-103">Creazione di un processo di importazione per hello servizio importazione/esportazione di Azure</span><span class="sxs-lookup"><span data-stu-id="81888-103">Creating an import job for hello Azure Import/Export service</span></span>

<span data-ttu-id="81888-104">La creazione di un processo di importazione per il servizio di importazione/esportazione di Microsoft Azure hello utilizzando hello API REST prevede hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="81888-104">Creating an import job for hello Microsoft Azure Import/Export service using hello REST API involves hello following steps:</span></span>

-   <span data-ttu-id="81888-105">Preparazione delle unità con hello strumento di importazione/esportazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="81888-105">Preparing drives with hello Azure Import/Export Tool.</span></span>

-   <span data-ttu-id="81888-106">Ottenere hello percorso toowhich tooship hello unità.</span><span class="sxs-lookup"><span data-stu-id="81888-106">Obtaining hello location toowhich tooship hello drive.</span></span>

-   <span data-ttu-id="81888-107">Creazione del processo di importazione hello.</span><span class="sxs-lookup"><span data-stu-id="81888-107">Creating hello import job.</span></span>

-   <span data-ttu-id="81888-108">Shipping hello unità tooMicrosoft tramite un servizio vettore supportato.</span><span class="sxs-lookup"><span data-stu-id="81888-108">Shipping hello drives tooMicrosoft via a supported carrier service.</span></span>

-   <span data-ttu-id="81888-109">Aggiornamento del processo di importazione hello con hello Dettagli spedizione.</span><span class="sxs-lookup"><span data-stu-id="81888-109">Updating hello import job with hello shipping details.</span></span>

 <span data-ttu-id="81888-110">Vedere [tramite servizio di importazione/esportazione di Microsoft Azure hello, dati tooTransfer tooBlob archiviazione](storage-import-export-service.md) per una panoramica del servizio di importazione/esportazione hello e un'esercitazione che illustra come hello toouse [portale di Azure](https://portal.azure.com/) toocreate e gestire l'importazione e i processi di esportazione.</span><span class="sxs-lookup"><span data-stu-id="81888-110">See [Using hello Microsoft Azure Import/Export service tooTransfer Data tooBlob Storage](storage-import-export-service.md) for an overview of hello Import/Export service and a tutorial that demonstrates how toouse hello [Azure  portal](https://portal.azure.com/) toocreate and manage import and export jobs.</span></span>

## <a name="preparing-drives-with-hello-azure-importexport-tool"></a><span data-ttu-id="81888-111">Preparazione delle unità con hello strumento di importazione/esportazione di Azure</span><span class="sxs-lookup"><span data-stu-id="81888-111">Preparing drives with hello Azure Import/Export Tool</span></span>

<span data-ttu-id="81888-112">Hello passaggi tooprepare unità per un processo di importazione sono hello stesso se si crea hello portale hello jobvia o tramite hello API REST.</span><span class="sxs-lookup"><span data-stu-id="81888-112">hello steps tooprepare drives for an import job are hello same whether you create hello jobvia hello portal or via hello REST API.</span></span>

<span data-ttu-id="81888-113">Di seguito è riportata una breve panoramica della preparazione dell'unità.</span><span class="sxs-lookup"><span data-stu-id="81888-113">Below is a brief overview of drive preparation.</span></span> <span data-ttu-id="81888-114">Fare riferimento toohello [Azure importazione ExportTool riferimento](storage-import-export-tool-how-to-v1.md) per istruzioni complete.</span><span class="sxs-lookup"><span data-stu-id="81888-114">Refer toohello [Azure Import-ExportTool Reference](storage-import-export-tool-how-to-v1.md) for complete instructions.</span></span> <span data-ttu-id="81888-115">È possibile scaricare lo strumento di importazione/esportazione di Azure hello [qui](http://go.microsoft.com/fwlink/?LinkID=301900).</span><span class="sxs-lookup"><span data-stu-id="81888-115">You can download hello Azure Import/Export Tool [here](http://go.microsoft.com/fwlink/?LinkID=301900).</span></span>

<span data-ttu-id="81888-116">La preparazione dell'unità comporta:</span><span class="sxs-lookup"><span data-stu-id="81888-116">Preparing your drive involves:</span></span>

-   <span data-ttu-id="81888-117">Identificazione hello toobe di dati importati.</span><span class="sxs-lookup"><span data-stu-id="81888-117">Identifying hello data toobe imported.</span></span>

-   <span data-ttu-id="81888-118">Identificazione dei blob di destinazione hello in archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="81888-118">Identifying hello destination blobs in Windows Azure Storage.</span></span>

-   <span data-ttu-id="81888-119">Utilizzo di hello strumento di importazione/esportazione di Azure toocopy tooone i dati o più dischi rigidi.</span><span class="sxs-lookup"><span data-stu-id="81888-119">Using hello Azure Import/Export Tool toocopy your data tooone or more hard drives.</span></span>

 <span data-ttu-id="81888-120">Hello strumento di importazione/esportazione di Azure genererà inoltre un file manifesto per ognuna delle unità hello preparata.</span><span class="sxs-lookup"><span data-stu-id="81888-120">hello Azure Import/Export Tool will also generate a manifest file for each of hello drives as it is prepared.</span></span> <span data-ttu-id="81888-121">Contiene un file manifesto:</span><span class="sxs-lookup"><span data-stu-id="81888-121">A manifest file contains:</span></span>

-   <span data-ttu-id="81888-122">Enumerazione di tutti i file hello destinato al caricamento e il mapping di hello da tooblobs questi file.</span><span class="sxs-lookup"><span data-stu-id="81888-122">An enumeration of all hello files intended for upload and hello mappings from these files tooblobs.</span></span>

-   <span data-ttu-id="81888-123">Checksum dei segmenti di hello di ogni file.</span><span class="sxs-lookup"><span data-stu-id="81888-123">Checksums of hello segments of each file.</span></span>

-   <span data-ttu-id="81888-124">Informazioni su tooassociate hello di proprietà e i metadati con ogni blob.</span><span class="sxs-lookup"><span data-stu-id="81888-124">Information about hello metadata and properties tooassociate with each blob.</span></span>

-   <span data-ttu-id="81888-125">Un elenco di hello azione tootake se dispone di un blob che è in fase di caricamento hello stesso nome di un blob esistente nel contenitore hello.</span><span class="sxs-lookup"><span data-stu-id="81888-125">A listing of hello action tootake if a blob that is being uploaded has hello same name as an existing blob in hello container.</span></span> <span data-ttu-id="81888-126">Le opzioni possibili sono: a) sovrascrivere il blob hello con file hello, b) mantenere il blob esistente hello e ignorare il caricamento di file hello, c) aggiungere un nome di toohello suffisso in modo che non è in conflitto con altri file.</span><span class="sxs-lookup"><span data-stu-id="81888-126">Possible options are: a) overwrite hello blob with hello file, b) keep hello existing blob and skip uploading hello file, c) append a suffix toohello name so that it does not conflict with other files.</span></span>

## <a name="obtaining-your-shipping-location"></a><span data-ttu-id="81888-127">Acquisizione della località di spedizione</span><span class="sxs-lookup"><span data-stu-id="81888-127">Obtaining your shipping location</span></span>

<span data-ttu-id="81888-128">Prima di creare un processo di importazione, è necessario tooobtain il nome di un'ubicazione di spedizione e l'indirizzo dal chiamante hello [List Locations](/rest/api/storageimportexport/listlocations) operazione.</span><span class="sxs-lookup"><span data-stu-id="81888-128">Before creating an import job, you need tooobtain a shipping location name and address by calling hello [List Locations](/rest/api/storageimportexport/listlocations) operation.</span></span> <span data-ttu-id="81888-129">`List Locations` restituirà un elenco di località con gli indirizzi postali.</span><span class="sxs-lookup"><span data-stu-id="81888-129">`List Locations` will return a list of locations and their mailing addresses.</span></span> <span data-ttu-id="81888-130">È possibile selezionare un'ubicazione hello elenco restituito e spedire il tuo indirizzo toothat unità disco rigido.</span><span class="sxs-lookup"><span data-stu-id="81888-130">You can select a location from hello returned list and ship your hard drives toothat address.</span></span> <span data-ttu-id="81888-131">È inoltre possibile utilizzare hello `Get Location` hello tooobtain operazione indirizzo per una determinata ubicazione di spedizione direttamente.</span><span class="sxs-lookup"><span data-stu-id="81888-131">You can also use hello `Get Location` operation tooobtain hello shipping address for a specific location directly.</span></span>

 <span data-ttu-id="81888-132">Seguire i passaggi di hello sotto tooobtain ubicazione di spedizione hello:</span><span class="sxs-lookup"><span data-stu-id="81888-132">Follow hello steps below tooobtain hello shipping location:</span></span>

-   <span data-ttu-id="81888-133">Identificare il nome di hello del percorso hello dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="81888-133">Identify hello name of hello location of your storage account.</span></span> <span data-ttu-id="81888-134">Questo valore è reperibile nella hello **percorso** campo dell'account di archiviazione hello **Dashboard** nel portale di Azure o eseguendo una query utilizzando Gestione servizio hello operazione API hello [ottenere archiviazione Proprietà dell'account](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).</span><span class="sxs-lookup"><span data-stu-id="81888-134">This value can be found under hello **Location** field on hello storage account's **Dashboard** in hello Azure portal or queried for by using hello service management API operation [Get Storage Account Properties](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).</span></span>

-   <span data-ttu-id="81888-135">Recuperare questo account di archiviazione di percorso hello tooprocess disponibile dal chiamante hello `Get Location` operazione.</span><span class="sxs-lookup"><span data-stu-id="81888-135">Retrieve hello location that is available tooprocess this storage account by calling hello `Get Location` operation.</span></span>

-   <span data-ttu-id="81888-136">Se hello `AlternateLocations` proprietà della posizione di hello contiene percorso hello stesso, quindi è corretto toouse questo percorso.</span><span class="sxs-lookup"><span data-stu-id="81888-136">If hello `AlternateLocations` property of hello location contains hello location itself, then it is okay toouse this location.</span></span> <span data-ttu-id="81888-137">In caso contrario, chiamare hello `Get Location` operazione con una delle posizioni alternative hello.</span><span class="sxs-lookup"><span data-stu-id="81888-137">Otherwise, call hello `Get Location` operation again with one of hello alternate locations.</span></span> <span data-ttu-id="81888-138">percorso originale Hello potrebbe essere chiusa temporaneamente per la manutenzione.</span><span class="sxs-lookup"><span data-stu-id="81888-138">hello original location might be temporarily closed for maintenance.</span></span>

## <a name="creating-hello-import-job"></a><span data-ttu-id="81888-139">Creazione del processo di importazione hello</span><span class="sxs-lookup"><span data-stu-id="81888-139">Creating hello import job</span></span>
<span data-ttu-id="81888-140">processo di importazione hello toocreate, chiamata hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operazione.</span><span class="sxs-lookup"><span data-stu-id="81888-140">toocreate hello import job, call hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span></span> <span data-ttu-id="81888-141">È necessario hello tooprovide le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="81888-141">You will need tooprovide hello following information:</span></span>

-   <span data-ttu-id="81888-142">Un nome per il processo di hello.</span><span class="sxs-lookup"><span data-stu-id="81888-142">A name for hello job.</span></span>

-   <span data-ttu-id="81888-143">nome di account di archiviazione Hello.</span><span class="sxs-lookup"><span data-stu-id="81888-143">hello storage account name.</span></span>

-   <span data-ttu-id="81888-144">Hello shipping nome dell'ubicazione, ottenuta nel passaggio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="81888-144">hello shipping location name, obtained from hello previous step.</span></span>

-   <span data-ttu-id="81888-145">Un tipo di processo (importazione).</span><span class="sxs-lookup"><span data-stu-id="81888-145">A job type (Import).</span></span>

-   <span data-ttu-id="81888-146">indirizzo del mittente Hello dove hello unità devono essere inviate una volta completato il processo di importazione hello.</span><span class="sxs-lookup"><span data-stu-id="81888-146">hello return address where hello drives should be sent after hello import job has completed.</span></span>

-   <span data-ttu-id="81888-147">elenco di Hello di unità nel processo di hello.</span><span class="sxs-lookup"><span data-stu-id="81888-147">hello list of drives in hello job.</span></span> <span data-ttu-id="81888-148">Per ogni unità, è necessario includere le seguenti informazioni che è state ottenute durante il passaggio di Preparazione unità hello hello:</span><span class="sxs-lookup"><span data-stu-id="81888-148">For each drive, you must include hello following information that was obtained during hello drive preparation step:</span></span>

    -   <span data-ttu-id="81888-149">Id dell'unità Hello</span><span class="sxs-lookup"><span data-stu-id="81888-149">hello drive Id</span></span>

    -   <span data-ttu-id="81888-150">chiave di BitLocker Hello</span><span class="sxs-lookup"><span data-stu-id="81888-150">hello BitLocker key</span></span>

    -   <span data-ttu-id="81888-151">percorso relativo del file manifesto Hello sul disco rigido hello</span><span class="sxs-lookup"><span data-stu-id="81888-151">hello manifest file relative path on hello hard drive</span></span>

    -   <span data-ttu-id="81888-152">file manifesto MD5 hash con codifica in base 16 Hello</span><span class="sxs-lookup"><span data-stu-id="81888-152">hello Base16 encoded manifest file MD5 hash</span></span>

## <a name="shipping-your-drives"></a><span data-ttu-id="81888-153">Spedizione delle unità</span><span class="sxs-lookup"><span data-stu-id="81888-153">Shipping your drives</span></span>
<span data-ttu-id="81888-154">È necessario fornire l'indirizzo toohello unità che ottenuta nel passaggio precedente hello ed è necessario fornire hello servizio importazione/esportazione con numero di pacchetti hello rilevamento hello.</span><span class="sxs-lookup"><span data-stu-id="81888-154">You must ship your drives toohello address that you obtained from hello previous step, and you must provide hello Import/Export service with hello tracking number of hello package.</span></span>

> [!NOTE]
>  <span data-ttu-id="81888-155">È necessario spedire le unità con un vettore supportato, che fornirà un numero di tracciabilità per il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="81888-155">You must ship your drives via a supported carrier service, which will provide a tracking number for your package.</span></span>

## <a name="updating-hello-import-job-with-your-shipping-information"></a><span data-ttu-id="81888-156">Aggiornamento del processo di importazione di hello con le informazioni di spedizione</span><span class="sxs-lookup"><span data-stu-id="81888-156">Updating hello import job with your shipping information</span></span>
<span data-ttu-id="81888-157">Dopo aver ottenuto il numero di tracciabilità, chiamare hello [Update Job Properties](/api/storageimportexport/jobs#Jobs_Update) hello tooupdate operazione shipping nome del gestore telefonico, il numero di tracciabilità hello per processo hello e numero di conto hello vettore per la spedizione di ritorno.</span><span class="sxs-lookup"><span data-stu-id="81888-157">After you have your tracking number, call hello [Update Job Properties](/api/storageimportexport/jobs#Jobs_Update) operation tooupdate hello shipping carrier name, hello tracking number for hello job, and hello carrier account number for return shipping.</span></span> <span data-ttu-id="81888-158">È facoltativamente possibile specificare il numero di hello di unità e hello nonché data di spedizione.</span><span class="sxs-lookup"><span data-stu-id="81888-158">You can optionally specify hello number of drives and hello shipping date as well.</span></span>

## <a name="next-steps"></a><span data-ttu-id="81888-159">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="81888-159">Next steps</span></span>

* [<span data-ttu-id="81888-160">Tramite l'API REST del servizio importazione/esportazione hello</span><span class="sxs-lookup"><span data-stu-id="81888-160">Using hello Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
