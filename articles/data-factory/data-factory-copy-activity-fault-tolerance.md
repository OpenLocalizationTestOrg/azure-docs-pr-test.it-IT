---
title: "tolleranza di errore aaaAdd nell'attività di copia di Azure Data Factory ignorando righe incompatibile | Documenti Microsoft"
description: "Informazioni su come tooadd la tolleranza di errore nell'attività di copia di Azure Data Factory ignorando righe incompatibile durante la copia"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jingwang
ms.openlocfilehash: e7cf6117655910844b292d340674d8d631450a81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-fault-tolerance-in-copy-activity-by-skipping-incompatible-rows"></a><span data-ttu-id="0e65a-103">Aggiungere la tolleranza di errore all'attività di copia ignorando le righe incompatibili</span><span class="sxs-lookup"><span data-stu-id="0e65a-103">Add fault tolerance in Copy Activity by skipping incompatible rows</span></span>

<span data-ttu-id="0e65a-104">Azure Data Factory [attività di copia](data-factory-data-movement-activities.md) sono disponibili righe di due modi toohandle incompatibili quando si copiano dati tra archivi dati di origine e sink:</span><span class="sxs-lookup"><span data-stu-id="0e65a-104">Azure Data Factory [Copy Activity](data-factory-data-movement-activities.md) offers you two ways toohandle incompatible rows when copying data between source and sink data stores:</span></span>

- <span data-ttu-id="0e65a-105">È possibile interrompere e avere esito negativo copia hello verificato durante l'attività quando sono dati non compatibili (comportamento predefinito).</span><span class="sxs-lookup"><span data-stu-id="0e65a-105">You can abort and fail hello copy activity when incompatible data is encountered (default behavior).</span></span>
- <span data-ttu-id="0e65a-106">È possibile continuare toocopy tutti i dati di hello aggiungendo la tolleranza di errore e ignorare le righe di dati incompatibili.</span><span class="sxs-lookup"><span data-stu-id="0e65a-106">You can continue toocopy all of hello data by adding fault tolerance and skipping incompatible data rows.</span></span> <span data-ttu-id="0e65a-107">Inoltre, è possibile registrare righe incompatibile hello nell'archiviazione Blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="0e65a-107">In addition, you can log hello incompatible rows in Azure Blob storage.</span></span> <span data-ttu-id="0e65a-108">È quindi possibile esaminare hello log toolearn hello causa dell'errore hello, correggere i dati di hello sull'origine dati hello e ripetere l'attività di copia hello.</span><span class="sxs-lookup"><span data-stu-id="0e65a-108">You can then examine hello log toolearn hello cause for hello failure, fix hello data on hello data source, and retry hello copy activity.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="0e65a-109">Scenari supportati</span><span class="sxs-lookup"><span data-stu-id="0e65a-109">Supported scenarios</span></span>
<span data-ttu-id="0e65a-110">L'attività di copia supporta tre scenari per rilevare, ignorare e registrare i dati incompatibili:</span><span class="sxs-lookup"><span data-stu-id="0e65a-110">Copy Activity supports three scenarios for detecting, skipping, and logging incompatible data:</span></span>

- <span data-ttu-id="0e65a-111">**Incompatibilità tra hello tipo di dati di origine e il tipo nativo sink hello**</span><span class="sxs-lookup"><span data-stu-id="0e65a-111">**Incompatibility between hello source data type and hello sink native type**</span></span>

    <span data-ttu-id="0e65a-112">Ad esempio: copia dati da un file CSV in archiviazione di Blob tooa SQL del database con una definizione di schema che contiene tre **INT** colonne di tipo.</span><span class="sxs-lookup"><span data-stu-id="0e65a-112">For example: Copy data from a CSV file in Blob storage tooa SQL database with a schema definition that contains three **INT** type columns.</span></span> <span data-ttu-id="0e65a-113">righe di file CSV contenenti dati numerici, ad esempio Hello `123,456,789` vengono copiati correttamente archivio sink toohello.</span><span class="sxs-lookup"><span data-stu-id="0e65a-113">hello CSV file rows that contain numeric data, such as `123,456,789` are copied successfully toohello sink store.</span></span> <span data-ttu-id="0e65a-114">Tuttavia, hello righe che contengono valori non numerici, ad esempio `123,456,abc` vengono rilevati come incompatibili e vengono ignorati.</span><span class="sxs-lookup"><span data-stu-id="0e65a-114">However, hello rows that contain non-numeric values, such as `123,456,abc` are detected as incompatible and are skipped.</span></span>

- <span data-ttu-id="0e65a-115">**Mancata corrispondenza nel numero hello di colonne tra hello origine e sink di hello**</span><span class="sxs-lookup"><span data-stu-id="0e65a-115">**Mismatch in hello number of columns between hello source and hello sink**</span></span>

    <span data-ttu-id="0e65a-116">Ad esempio: copia dati da un file CSV in archiviazione di Blob tooa SQL del database con una definizione di schema che contiene sei colonne.</span><span class="sxs-lookup"><span data-stu-id="0e65a-116">For example: Copy data from a CSV file in Blob storage tooa SQL database with a schema definition that contains six columns.</span></span> <span data-ttu-id="0e65a-117">Hello file CSV le righe che contengono sei colonne vengono copiati correttamente archivio sink toohello.</span><span class="sxs-lookup"><span data-stu-id="0e65a-117">hello CSV file rows that contain six columns are copied successfully toohello sink store.</span></span> <span data-ttu-id="0e65a-118">righe di file CSV Hello che contengono meno di sei o più colonne vengono rilevate come incompatibile e vengono ignorate.</span><span class="sxs-lookup"><span data-stu-id="0e65a-118">hello CSV file rows that contain more or fewer than six columns are detected as incompatible and are skipped.</span></span>

- <span data-ttu-id="0e65a-119">**Violazione della chiave primaria per la scrittura di database relazionale tooa**</span><span class="sxs-lookup"><span data-stu-id="0e65a-119">**Primary key violation when writing tooa relational database**</span></span>

    <span data-ttu-id="0e65a-120">Ad esempio: copiare i dati da un database SQL di SQL server tooa.</span><span class="sxs-lookup"><span data-stu-id="0e65a-120">For example: Copy data from a SQL server tooa SQL database.</span></span> <span data-ttu-id="0e65a-121">Nel database SQL di sink hello è definita una chiave primaria, ma tale chiave non primaria è definito in hello origine di SQL server.</span><span class="sxs-lookup"><span data-stu-id="0e65a-121">A primary key is defined in hello sink SQL database, but no such primary key is defined in hello source SQL server.</span></span> <span data-ttu-id="0e65a-122">righe Hello duplicato presenti nell'origine hello non possono essere copiato toohello sink.</span><span class="sxs-lookup"><span data-stu-id="0e65a-122">hello duplicated rows that exist in hello source cannot be copied toohello sink.</span></span> <span data-ttu-id="0e65a-123">Attività di copia copia solo hello prima riga dei dati di origine hello in sink hello.</span><span class="sxs-lookup"><span data-stu-id="0e65a-123">Copy Activity copies only hello first row of hello source data into hello sink.</span></span> <span data-ttu-id="0e65a-124">Hello sorgente successiva le righe che contengono il valore di chiave primaria di hello duplicato vengono rilevate come incompatibile e vengono ignorate.</span><span class="sxs-lookup"><span data-stu-id="0e65a-124">hello subsequent source rows that contain hello duplicated primary key value are detected as incompatible and are skipped.</span></span>

## <a name="configuration"></a><span data-ttu-id="0e65a-125">Configurazione</span><span class="sxs-lookup"><span data-stu-id="0e65a-125">Configuration</span></span>
<span data-ttu-id="0e65a-126">Hello esempio seguente viene fornito un tooconfigure definizione JSON ignorare hello incompatibili nell'attività di copia:</span><span class="sxs-lookup"><span data-stu-id="0e65a-126">hello following example provides a JSON definition tooconfigure skipping hello incompatible rows in Copy Activity:</span></span>

```json
"typeProperties": {
    "source": {
        "type": "BlobSource"
    },
    "sink": {
        "type": "SqlSink",
    },         
    "enableSkipIncompatibleRow": true,           
    "redirectIncompatibleRowSettings": {
        "linkedServiceName": "BlobStorage",
        "path": "redirectcontainer/erroroutput"
    }
}
```

| <span data-ttu-id="0e65a-127">Proprietà</span><span class="sxs-lookup"><span data-stu-id="0e65a-127">Property</span></span> | <span data-ttu-id="0e65a-128">Descrizione</span><span class="sxs-lookup"><span data-stu-id="0e65a-128">Description</span></span> | <span data-ttu-id="0e65a-129">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="0e65a-129">Allowed values</span></span> | <span data-ttu-id="0e65a-130">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="0e65a-130">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0e65a-131">**enableSkipIncompatibleRow**</span><span class="sxs-lookup"><span data-stu-id="0e65a-131">**enableSkipIncompatibleRow**</span></span> | <span data-ttu-id="0e65a-132">Specificare se ignorare o meno le righe incompatibili durante la copia.</span><span class="sxs-lookup"><span data-stu-id="0e65a-132">Enable skipping incompatible rows during copy or not.</span></span> | <span data-ttu-id="0e65a-133">True</span><span class="sxs-lookup"><span data-stu-id="0e65a-133">True</span></span><br/><span data-ttu-id="0e65a-134">False (impostazione predefinita)</span><span class="sxs-lookup"><span data-stu-id="0e65a-134">False (default)</span></span> | <span data-ttu-id="0e65a-135">No</span><span class="sxs-lookup"><span data-stu-id="0e65a-135">No</span></span> |
| <span data-ttu-id="0e65a-136">**redirectIncompatibleRowSettings**</span><span class="sxs-lookup"><span data-stu-id="0e65a-136">**redirectIncompatibleRowSettings**</span></span> | <span data-ttu-id="0e65a-137">Un gruppo di proprietà che può essere specificato quando si desidera che le righe non compatibile di toolog hello.</span><span class="sxs-lookup"><span data-stu-id="0e65a-137">A group of properties that can be specified when you want toolog hello incompatible rows.</span></span> | &nbsp; | <span data-ttu-id="0e65a-138">No</span><span class="sxs-lookup"><span data-stu-id="0e65a-138">No</span></span> |
| <span data-ttu-id="0e65a-139">**linkedServiceName**</span><span class="sxs-lookup"><span data-stu-id="0e65a-139">**linkedServiceName**</span></span> | <span data-ttu-id="0e65a-140">servizio collegato Hello del log di hello toostore di archiviazione di Azure che contiene righe hello ignorata.</span><span class="sxs-lookup"><span data-stu-id="0e65a-140">hello linked service of Azure Storage toostore hello log that contains hello skipped rows.</span></span> | <span data-ttu-id="0e65a-141">nome Hello un [AzureStorage](data-factory-azure-blob-connector.md#azure-storage-linked-service) o [AzureStorageSas](data-factory-azure-blob-connector.md#azure-storage-sas-linked-service) servizio, che fa riferimento toohello istanza di archiviazione che si desidera file di log toouse toostore hello collegato.</span><span class="sxs-lookup"><span data-stu-id="0e65a-141">hello name of an [AzureStorage](data-factory-azure-blob-connector.md#azure-storage-linked-service) or [AzureStorageSas](data-factory-azure-blob-connector.md#azure-storage-sas-linked-service) linked service, which refers toohello storage instance that you want toouse toostore hello log file.</span></span> | <span data-ttu-id="0e65a-142">No</span><span class="sxs-lookup"><span data-stu-id="0e65a-142">No</span></span> |
| <span data-ttu-id="0e65a-143">**path**</span><span class="sxs-lookup"><span data-stu-id="0e65a-143">**path**</span></span> | <span data-ttu-id="0e65a-144">percorso di Hello hello del file di log che contiene hello ignorato righe.</span><span class="sxs-lookup"><span data-stu-id="0e65a-144">hello path of hello log file that contains hello skipped rows.</span></span> | <span data-ttu-id="0e65a-145">Specificare percorso di archiviazione Blob hello che dati non compatibili di toouse toolog hello.</span><span class="sxs-lookup"><span data-stu-id="0e65a-145">Specify hello Blob storage path that you want toouse toolog hello incompatible data.</span></span> <span data-ttu-id="0e65a-146">Se non si specifica un percorso, il servizio hello crea un contenitore.</span><span class="sxs-lookup"><span data-stu-id="0e65a-146">If you do not provide a path, hello service creates a container for you.</span></span> | <span data-ttu-id="0e65a-147">No</span><span class="sxs-lookup"><span data-stu-id="0e65a-147">No</span></span> |

## <a name="monitoring"></a><span data-ttu-id="0e65a-148">Monitoraggio</span><span class="sxs-lookup"><span data-stu-id="0e65a-148">Monitoring</span></span>
<span data-ttu-id="0e65a-149">Al termine dell'esecuzione dell'attività hello copia, è possibile visualizzare il numero di hello delle righe ignorate nella sezione monitoraggio hello:</span><span class="sxs-lookup"><span data-stu-id="0e65a-149">After hello copy activity run completes, you can see hello number of skipped rows in hello monitoring section:</span></span>

![Monitorare le righe incompatibili ignorate](./media/data-factory-copy-activity-fault-tolerance/skip-incompatible-rows-monitoring.png)

<span data-ttu-id="0e65a-151">Se si configurano le righe non compatibile di hello toolog, è possibile trovare il file di log hello in questo percorso: `https://[your-blob-account].blob.core.windows.net/[path-if-configured]/[copy-activity-run-id]/[auto-generated-GUID].csv` nel file di log hello, è possibile visualizzare le righe che sono state ignorate hello e hello a causa di incompatibilità hello.</span><span class="sxs-lookup"><span data-stu-id="0e65a-151">If you configure toolog hello incompatible rows, you can find hello log file at this path: `https://[your-blob-account].blob.core.windows.net/[path-if-configured]/[copy-activity-run-id]/[auto-generated-GUID].csv` In hello log file, you can see hello rows that were skipped and hello root cause of hello incompatibility.</span></span>

<span data-ttu-id="0e65a-152">Dati originali hello sia errore corrispondente hello vengono registrate nel file hello.</span><span class="sxs-lookup"><span data-stu-id="0e65a-152">Both hello original data and hello corresponding error are logged in hello file.</span></span> <span data-ttu-id="0e65a-153">Un esempio di contenuto del file di log hello è come segue:</span><span class="sxs-lookup"><span data-stu-id="0e65a-153">An example of hello log file content is as follows:</span></span>
```
data1, data2, data3, UserErrorInvalidDataValue,Column 'Prop_2' contains an invalid value 'data3'. Cannot convert 'data3' tootype 'DateTime'.,
data4, data5, data6, Violation of PRIMARY KEY constraint 'PK_tblintstrdatetimewithpk'. Cannot insert duplicate key in object 'dbo.tblintstrdatetimewithpk'. hello duplicate key value is (data4).
```

## <a name="next-steps"></a><span data-ttu-id="0e65a-154">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0e65a-154">Next steps</span></span>
<span data-ttu-id="0e65a-155">toolearn ulteriori informazioni sull'attività di copia di Azure Data Factory, vedere [spostare i dati utilizzando l'attività di copia](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="0e65a-155">toolearn more about Azure Data Factory Copy Activity, see [Move data by using Copy Activity](data-factory-data-movement-activities.md).</span></span>
