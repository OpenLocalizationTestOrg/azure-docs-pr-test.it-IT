---
title: "Aggiungere la tolleranza di errore all'attività di copia di Azure Data Factory ignorando le righe incompatibili | Microsoft Docs"
description: "Informazioni su come aggiungere la tolleranza di errore all'attività di copia di Azure Data Factory ignorando le righe incompatibili"
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
ms.openlocfilehash: e2a108752259d5da3b401666c6bdbaad13b7ea90
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="add-fault-tolerance-in-copy-activity-by-skipping-incompatible-rows"></a><span data-ttu-id="e8782-103">Aggiungere la tolleranza di errore all'attività di copia ignorando le righe incompatibili</span><span class="sxs-lookup"><span data-stu-id="e8782-103">Add fault tolerance in Copy Activity by skipping incompatible rows</span></span>

<span data-ttu-id="e8782-104">L'[attività di copia](data-factory-data-movement-activities.md) di Azure Data Factory offre due modi per gestire le righe incompatibili durante la copia di dati tra gli archivi dati di origine e sink:</span><span class="sxs-lookup"><span data-stu-id="e8782-104">Azure Data Factory [Copy Activity](data-factory-data-movement-activities.md) offers you two ways to handle incompatible rows when copying data between source and sink data stores:</span></span>

- <span data-ttu-id="e8782-105">È possibile interrompere l'attività di copia quando vengono rilevati dati incompatibili (comportamento predefinito).</span><span class="sxs-lookup"><span data-stu-id="e8782-105">You can abort and fail the copy activity when incompatible data is encountered (default behavior).</span></span>
- <span data-ttu-id="e8782-106">È possibile continuare a copiare tutti i dati aggiungendo la tolleranza di errore e ignorando le righe di dati incompatibili.</span><span class="sxs-lookup"><span data-stu-id="e8782-106">You can continue to copy all of the data by adding fault tolerance and skipping incompatible data rows.</span></span> <span data-ttu-id="e8782-107">È anche possibile registrare le righe incompatibili nell'archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="e8782-107">In addition, you can log the incompatible rows in Azure Blob storage.</span></span> <span data-ttu-id="e8782-108">È quindi possibile esaminare il log per conoscere la causa dell'errore, correggere i dati nell'origine dati e ripetere l'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="e8782-108">You can then examine the log to learn the cause for the failure, fix the data on the data source, and retry the copy activity.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="e8782-109">Scenari supportati</span><span class="sxs-lookup"><span data-stu-id="e8782-109">Supported scenarios</span></span>
<span data-ttu-id="e8782-110">L'attività di copia supporta tre scenari per rilevare, ignorare e registrare i dati incompatibili:</span><span class="sxs-lookup"><span data-stu-id="e8782-110">Copy Activity supports three scenarios for detecting, skipping, and logging incompatible data:</span></span>

- <span data-ttu-id="e8782-111">**Incompatibilità tra il tipo di dati di origine e il tipo nativo sink**</span><span class="sxs-lookup"><span data-stu-id="e8782-111">**Incompatibility between the source data type and the sink native type**</span></span>

    <span data-ttu-id="e8782-112">Esempio: si vogliono copiare dati da un file CSV nell'archivio BLOB a un database SQL con una definizione di schema che contiene tre colonne di tipo **INT**.</span><span class="sxs-lookup"><span data-stu-id="e8782-112">For example: Copy data from a CSV file in Blob storage to a SQL database with a schema definition that contains three **INT** type columns.</span></span> <span data-ttu-id="e8782-113">Le righe del file CSV contenenti dati numerici, ad esempio `123,456,789`, vengono copiate nell'archivio sink.</span><span class="sxs-lookup"><span data-stu-id="e8782-113">The CSV file rows that contain numeric data, such as `123,456,789` are copied successfully to the sink store.</span></span> <span data-ttu-id="e8782-114">Tuttavia, le righe che contengono valori non numerici, ad esempio `123,456,abc`, vengono rilevate come incompatibili e vengono ignorate.</span><span class="sxs-lookup"><span data-stu-id="e8782-114">However, the rows that contain non-numeric values, such as `123,456,abc` are detected as incompatible and are skipped.</span></span>

- <span data-ttu-id="e8782-115">**Mancata corrispondenza nel numero di colonne tra l'origine e il sink**</span><span class="sxs-lookup"><span data-stu-id="e8782-115">**Mismatch in the number of columns between the source and the sink**</span></span>

    <span data-ttu-id="e8782-116">Esempio: si vogliono copiare dati da un file CSV nell'archivio BLOB a un database SQL con una definizione di schema che contiene sei colonne.</span><span class="sxs-lookup"><span data-stu-id="e8782-116">For example: Copy data from a CSV file in Blob storage to a SQL database with a schema definition that contains six columns.</span></span> <span data-ttu-id="e8782-117">Le righe del file CSV che contengono sei colonne vengono copiate nell'archivio sink.</span><span class="sxs-lookup"><span data-stu-id="e8782-117">The CSV file rows that contain six columns are copied successfully to the sink store.</span></span> <span data-ttu-id="e8782-118">Le righe del file CSV che contengono più o meno di sei colonne vengono rilevate come incompatibili e vengono ignorate.</span><span class="sxs-lookup"><span data-stu-id="e8782-118">The CSV file rows that contain more or fewer than six columns are detected as incompatible and are skipped.</span></span>

- <span data-ttu-id="e8782-119">**Violazione della chiave primaria durante la scrittura in un database relazionale**</span><span class="sxs-lookup"><span data-stu-id="e8782-119">**Primary key violation when writing to a relational database**</span></span>

    <span data-ttu-id="e8782-120">Esempio: si vogliono copiare dati da un'istanza di SQL Server a un database SQL.</span><span class="sxs-lookup"><span data-stu-id="e8782-120">For example: Copy data from a SQL server to a SQL database.</span></span> <span data-ttu-id="e8782-121">Il database SQL del sink contiene la definizione di una chiave primaria, che invece manca nell'istanza di SQL Server di origine.</span><span class="sxs-lookup"><span data-stu-id="e8782-121">A primary key is defined in the sink SQL database, but no such primary key is defined in the source SQL server.</span></span> <span data-ttu-id="e8782-122">Non è possibile copiare nel sink le righe duplicate presenti nell'origine.</span><span class="sxs-lookup"><span data-stu-id="e8782-122">The duplicated rows that exist in the source cannot be copied to the sink.</span></span> <span data-ttu-id="e8782-123">L'attività di copia copierà nel sink solo la prima riga dei dati di origine.</span><span class="sxs-lookup"><span data-stu-id="e8782-123">Copy Activity copies only the first row of the source data into the sink.</span></span> <span data-ttu-id="e8782-124">Le righe di origine successive che contengono il valore della chiave primaria duplicato vengono rilevate come incompatibili e vengono ignorate.</span><span class="sxs-lookup"><span data-stu-id="e8782-124">The subsequent source rows that contain the duplicated primary key value are detected as incompatible and are skipped.</span></span>

## <a name="configuration"></a><span data-ttu-id="e8782-125">Configurazione</span><span class="sxs-lookup"><span data-stu-id="e8782-125">Configuration</span></span>
<span data-ttu-id="e8782-126">L'esempio seguente offre la definizione JSON per specificare di ignorare le righe incompatibili nell'attività di copia:</span><span class="sxs-lookup"><span data-stu-id="e8782-126">The following example provides a JSON definition to configure skipping the incompatible rows in Copy Activity:</span></span>

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

| <span data-ttu-id="e8782-127">Proprietà</span><span class="sxs-lookup"><span data-stu-id="e8782-127">Property</span></span> | <span data-ttu-id="e8782-128">Descrizione</span><span class="sxs-lookup"><span data-stu-id="e8782-128">Description</span></span> | <span data-ttu-id="e8782-129">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="e8782-129">Allowed values</span></span> | <span data-ttu-id="e8782-130">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="e8782-130">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e8782-131">**enableSkipIncompatibleRow**</span><span class="sxs-lookup"><span data-stu-id="e8782-131">**enableSkipIncompatibleRow**</span></span> | <span data-ttu-id="e8782-132">Specificare se ignorare o meno le righe incompatibili durante la copia.</span><span class="sxs-lookup"><span data-stu-id="e8782-132">Enable skipping incompatible rows during copy or not.</span></span> | <span data-ttu-id="e8782-133">True</span><span class="sxs-lookup"><span data-stu-id="e8782-133">True</span></span><br/><span data-ttu-id="e8782-134">False (impostazione predefinita)</span><span class="sxs-lookup"><span data-stu-id="e8782-134">False (default)</span></span> | <span data-ttu-id="e8782-135">No</span><span class="sxs-lookup"><span data-stu-id="e8782-135">No</span></span> |
| <span data-ttu-id="e8782-136">**redirectIncompatibleRowSettings**</span><span class="sxs-lookup"><span data-stu-id="e8782-136">**redirectIncompatibleRowSettings**</span></span> | <span data-ttu-id="e8782-137">Un gruppo di proprietà che può essere specificato quando si vuole registrare le righe incompatibili.</span><span class="sxs-lookup"><span data-stu-id="e8782-137">A group of properties that can be specified when you want to log the incompatible rows.</span></span> | &nbsp; | <span data-ttu-id="e8782-138">No</span><span class="sxs-lookup"><span data-stu-id="e8782-138">No</span></span> |
| <span data-ttu-id="e8782-139">**linkedServiceName**</span><span class="sxs-lookup"><span data-stu-id="e8782-139">**linkedServiceName**</span></span> | <span data-ttu-id="e8782-140">Servizio collegato di Archiviazione di Azure con cui archiviare il log che contiene le righe ignorate.</span><span class="sxs-lookup"><span data-stu-id="e8782-140">The linked service of Azure Storage to store the log that contains the skipped rows.</span></span> | <span data-ttu-id="e8782-141">Nome di un servizio collegato [AzureStorage](data-factory-azure-blob-connector.md#azure-storage-linked-service) o [AzureStorageSas](data-factory-azure-blob-connector.md#azure-storage-sas-linked-service) che fa riferimento all'istanza di archiviazione da usare per archiviare il file di log.</span><span class="sxs-lookup"><span data-stu-id="e8782-141">The name of an [AzureStorage](data-factory-azure-blob-connector.md#azure-storage-linked-service) or [AzureStorageSas](data-factory-azure-blob-connector.md#azure-storage-sas-linked-service) linked service, which refers to the storage instance that you want to use to store the log file.</span></span> | <span data-ttu-id="e8782-142">No</span><span class="sxs-lookup"><span data-stu-id="e8782-142">No</span></span> |
| <span data-ttu-id="e8782-143">**path**</span><span class="sxs-lookup"><span data-stu-id="e8782-143">**path**</span></span> | <span data-ttu-id="e8782-144">Percorso del file di log che contiene le righe ignorate.</span><span class="sxs-lookup"><span data-stu-id="e8782-144">The path of the log file that contains the skipped rows.</span></span> | <span data-ttu-id="e8782-145">Specificare il percorso dell'archivio BLOB da usare per registrare i dati incompatibili.</span><span class="sxs-lookup"><span data-stu-id="e8782-145">Specify the Blob storage path that you want to use to log the incompatible data.</span></span> <span data-ttu-id="e8782-146">Se non si specifica un percorso, il servizio crea automaticamente un contenitore.</span><span class="sxs-lookup"><span data-stu-id="e8782-146">If you do not provide a path, the service creates a container for you.</span></span> | <span data-ttu-id="e8782-147">No</span><span class="sxs-lookup"><span data-stu-id="e8782-147">No</span></span> |

## <a name="monitoring"></a><span data-ttu-id="e8782-148">Monitoraggio</span><span class="sxs-lookup"><span data-stu-id="e8782-148">Monitoring</span></span>
<span data-ttu-id="e8782-149">Al termine dell'esecuzione dell'attività di copia, è possibile visualizzare il numero di righe ignorate nella sezione di monitoraggio:</span><span class="sxs-lookup"><span data-stu-id="e8782-149">After the copy activity run completes, you can see the number of skipped rows in the monitoring section:</span></span>

![Monitorare le righe incompatibili ignorate](./media/data-factory-copy-activity-fault-tolerance/skip-incompatible-rows-monitoring.png)

<span data-ttu-id="e8782-151">Se si configura la registrazione delle righe incompatibili, il file di log sarà disponibile nel percorso: `https://[your-blob-account].blob.core.windows.net/[path-if-configured]/[copy-activity-run-id]/[auto-generated-GUID].csv`. Il file di log contiene le righe ignorate e la causa radice dell'incompatibilità.</span><span class="sxs-lookup"><span data-stu-id="e8782-151">If you configure to log the incompatible rows, you can find the log file at this path: `https://[your-blob-account].blob.core.windows.net/[path-if-configured]/[copy-activity-run-id]/[auto-generated-GUID].csv` In the log file, you can see the rows that were skipped and the root cause of the incompatibility.</span></span>

<span data-ttu-id="e8782-152">Nel file vengono registrati sia i dati originali che l'errore corrispondente.</span><span class="sxs-lookup"><span data-stu-id="e8782-152">Both the original data and the corresponding error are logged in the file.</span></span> <span data-ttu-id="e8782-153">Di seguito è riportato un esempio del contenuto del file di log:</span><span class="sxs-lookup"><span data-stu-id="e8782-153">An example of the log file content is as follows:</span></span>
```
data1, data2, data3, UserErrorInvalidDataValue,Column 'Prop_2' contains an invalid value 'data3'. Cannot convert 'data3' to type 'DateTime'.,
data4, data5, data6, Violation of PRIMARY KEY constraint 'PK_tblintstrdatetimewithpk'. Cannot insert duplicate key in object 'dbo.tblintstrdatetimewithpk'. The duplicate key value is (data4).
```

## <a name="next-steps"></a><span data-ttu-id="e8782-154">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e8782-154">Next steps</span></span>
<span data-ttu-id="e8782-155">Per altre informazioni sull'attività di copia di Azure Data Factory, vedere [Spostare dati con l'attività di copia](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="e8782-155">To learn more about Azure Data Factory Copy Activity, see [Move data by using Copy Activity](data-factory-data-movement-activities.md).</span></span>