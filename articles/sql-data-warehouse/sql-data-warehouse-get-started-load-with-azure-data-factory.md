---
redirect_url: /azure/sql-data-warehouse/sql-data-warehouse-load-with-data-factory
title: Caricare i dati con Data factory di Azure | Documentazione Microsoft
description: Informazioni su come caricare i dati con Data factory di Azure
services: sql-data-warehouse
documentationcenter: NA
author: twounder
manager: jhubbard
editor: 
tags: azure-sql-data-warehouse
ms.assetid: ac7ddaa7-a3a5-4e15-b3cf-c696d2d105df
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 10/31/2016
ms.author: mausher;barbkess
ms.custom: loading
ms.openlocfilehash: 0b01c77c916b616974545fc3da442e72e5336399
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="load-data-with-azure-data-factory"></a><span data-ttu-id="437e7-103">Caricare i dati con Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="437e7-103">Load Data with Azure Data Factory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="437e7-104">Redgate</span><span class="sxs-lookup"><span data-stu-id="437e7-104">Redgate</span></span>](sql-data-warehouse-load-with-redgate.md)  
> * [<span data-ttu-id="437e7-105">Data Factory</span><span class="sxs-lookup"><span data-stu-id="437e7-105">Data Factory</span></span>](sql-data-warehouse-get-started-load-with-azure-data-factory.md)  
> * [<span data-ttu-id="437e7-106">PolyBase</span><span class="sxs-lookup"><span data-stu-id="437e7-106">PolyBase</span></span>](sql-data-warehouse-get-started-load-with-polybase.md)  
> * [<span data-ttu-id="437e7-107">BCP</span><span class="sxs-lookup"><span data-stu-id="437e7-107">BCP</span></span>](sql-data-warehouse-load-with-bcp.md)  
> 
> 

<span data-ttu-id="437e7-108">Questa esercitazione illustra come creare una pipeline in Azure Data Factory per lo spostamento di dati da un BLOB del servizio di archiviazione di Azure ad Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="437e7-108">This tutorial shows you how to create a pipeline in Azure Data Factory to move data from Azure Storage Blob to Azure SQL Data Warehouse.</span></span> <span data-ttu-id="437e7-109">I passaggi seguenti consentono di eseguire queste operazioni:</span><span class="sxs-lookup"><span data-stu-id="437e7-109">With the following steps you will:</span></span>

* <span data-ttu-id="437e7-110">Configurare dati di esempio in un BLOB del servizio di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="437e7-110">Set up sample data in an Azure Storage Blob.</span></span>
* <span data-ttu-id="437e7-111">Connettere le risorse a Data factory di Azure.</span><span class="sxs-lookup"><span data-stu-id="437e7-111">Connect resources to Azure Data Factory.</span></span>
* <span data-ttu-id="437e7-112">Creare una pipeline per spostare i dati dai BLOB di archiviazione a SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="437e7-112">Create a pipeline to move data from Storage Blobs to SQL Data Warehouse.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-Azure-SQL-Data-Warehouse-with-Azure-Data-Factory/player]
> 
> 

## <a name="before-you-begin"></a><span data-ttu-id="437e7-113">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="437e7-113">Before you begin</span></span>
<span data-ttu-id="437e7-114">Per una panoramica di Azure Data Factory, vedere [Introduzione al servizio Azure Data Factory][Introduction to Azure Data Factory].</span><span class="sxs-lookup"><span data-stu-id="437e7-114">To familiarize yourself with Azure Data Factory, see [Introduction to Azure Data Factory][Introduction to Azure Data Factory].</span></span>

### <a name="create-or-identify-resources"></a><span data-ttu-id="437e7-115">Creare o identificare le risorse</span><span class="sxs-lookup"><span data-stu-id="437e7-115">Create or identify resources</span></span>
<span data-ttu-id="437e7-116">Prima di iniziare questa esercitazione, è necessario avere le risorse seguenti.</span><span class="sxs-lookup"><span data-stu-id="437e7-116">Before starting this tutorial, you need to have the following resources:</span></span>

* <span data-ttu-id="437e7-117">**BLOB del servizio di archiviazione di Azure**: questa esercitazione usa il BLOB del servizio di archiviazione di Azure come origine dati per la pipeline di Azure Data Factory e quindi è necessario che ne sia disponibile uno per archiviare i dati di esempio.</span><span class="sxs-lookup"><span data-stu-id="437e7-117">**Azure Storage Blob**: This tutorial uses Azure Storage Blob as the data source for the Azure Data Factory pipeline, and so you need to have one available to store the sample data.</span></span> <span data-ttu-id="437e7-118">Se non ne è già disponibile uno, vedere [Creare un account di archiviazione][Create a storage account].</span><span class="sxs-lookup"><span data-stu-id="437e7-118">If you don't have one already, learn how to [Create a storage account][Create a storage account].</span></span>
* <span data-ttu-id="437e7-119">**SQL Data Warehouse**: questa esercitazione sposta i dati da un BLOB del servizio di archiviazione di Azure a SQL Data Warehouse ed è quindi necessario avere un data warehouse online caricato con i dati di esempio AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="437e7-119">**SQL Data Warehouse**: This tutorial moves the data from Azure Storage Blob to  SQL Data Warehouse and so need to have a data warehouse online that is loaded with the AdventureWorksDW sample data.</span></span> <span data-ttu-id="437e7-120">Se non si ha già un data warehouse, vedere le informazioni su come [effettuare il provisioning][Create a SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="437e7-120">If you do not already have a data warehouse, learn how to [provision one][Create a SQL Data Warehouse].</span></span> <span data-ttu-id="437e7-121">Se è disponibile un data warehouse, ma non ne è stato effettuato il provisioning con i dati di esempio, è possibile [caricarli manualmente][Load sample data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="437e7-121">If you have a data warehouse but didn't provision it with the sample data, you can [load it manually][Load sample data into SQL Data Warehouse].</span></span>
* <span data-ttu-id="437e7-122">**Azure Data Factory**: Azure Data Factory completa il caricamento effettivo ed è quindi necessario avere una data factory da poter usare per creare la pipeline per lo spostamento dei dati.</span><span class="sxs-lookup"><span data-stu-id="437e7-122">**Azure Data Factory**: Azure Data Factory completes the actual load and so you need to have one that you can use to build the data movement pipeline.</span></span> <span data-ttu-id="437e7-123">Se non si ha una data factory, per informazioni su come crearne una vedere il passaggio 1 dell'[introduzione ad Azure Data Factory (editor di Data Factory)][Get started with Azure Data Factory (Data Factory Editor)].</span><span class="sxs-lookup"><span data-stu-id="437e7-123">If you don't have one already, learn how to create one in Step 1 of [Get started with Azure Data Factory (Data Factory Editor)][Get started with Azure Data Factory (Data Factory Editor)].</span></span>
* <span data-ttu-id="437e7-124">**AZCopy**: per copiare i dati di esempio dal client locale al BLOB di archiviazione di Azure, è necessario AZCopy.</span><span class="sxs-lookup"><span data-stu-id="437e7-124">**AZCopy**: You need AZCopy to copy the sample data from your local client to your Azure Storage Blob.</span></span> <span data-ttu-id="437e7-125">Per istruzioni di installazione, vedere la [documentazione di AZCopy][AZCopy documentation].</span><span class="sxs-lookup"><span data-stu-id="437e7-125">For install instructions, see the [AZCopy documentation][AZCopy documentation].</span></span>

## <a name="step-1-copy-sample-data-to-azure-storage-blob"></a><span data-ttu-id="437e7-126">Passaggio 1: Copiare i dati di esempio nel BLOB di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="437e7-126">Step 1: Copy sample data to Azure Storage Blob</span></span>
<span data-ttu-id="437e7-127">Quando tutti i componenti sono pronti, è possibile copiare i dati di esempio nel BLOB del servizio di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="437e7-127">Once you have all the pieces ready, you are ready to copy sample data to your Azure Storage Blob.</span></span>

1. <span data-ttu-id="437e7-128">[Scaricare i dati di esempio][Download sample data].</span><span class="sxs-lookup"><span data-stu-id="437e7-128">[Download sample data][Download sample data].</span></span> <span data-ttu-id="437e7-129">Questi dati aggiungono altri tre anni di dati di vendita ai dati di esempio AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="437e7-129">This data adds another three years of sales data to your AdventureWorksDW sample data.</span></span>
2. <span data-ttu-id="437e7-130">Usare questo comando di AZCopy per copiare i tre anni di dati nel BLOB di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="437e7-130">Use this AZCopy command to copy the three years of data to your Azure Storage Blob.</span></span>
   
    ````
    AzCopy /Source:<Sample Data Location>  /Dest:https://<storage account>.blob.core.windows.net/<container name> /DestKey:<storage key> /Pattern:FactInternetSales.csv
    ````

## <a name="step-2-connect-resources-to-azure-data-factory"></a><span data-ttu-id="437e7-131">Passaggio 2: Connettere le risorse a Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="437e7-131">Step 2: Connect resources to Azure Data Factory</span></span>
<span data-ttu-id="437e7-132">Dopo avere inserito i dati, è possibile creare la pipeline di Azure Data Factory per spostare i dati dall'archivio BLOB di Azure in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="437e7-132">Now that the data is in place we can create the Azure Data Factory pipeline to move the data from Azure blob storage into SQL Data Warehouse.</span></span>

<span data-ttu-id="437e7-133">Per iniziare, aprire il [portale di Azure][Azure portal] e selezionare il servizio data factory dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="437e7-133">To get started, open the [Azure portal][Azure portal] and select your data factory from the left-hand menu.</span></span>

### <a name="step-21-create-linked-service"></a><span data-ttu-id="437e7-134">Passaggio 2.1: Creare servizi collegati</span><span class="sxs-lookup"><span data-stu-id="437e7-134">Step 2.1: Create Linked Service</span></span>
<span data-ttu-id="437e7-135">Collegare l'account di archiviazione di Azure e SQL Data Warehouse alla data factory.</span><span class="sxs-lookup"><span data-stu-id="437e7-135">Link your Azure storage account and SQL Data Warehouse to your data factory.</span></span>  

1. <span data-ttu-id="437e7-136">Iniziare prima di tutto il processo di registrazione facendo clic sulla sezione "Servizi collegati" della data factory e quindi su "Nuovo archivio dati".</span><span class="sxs-lookup"><span data-stu-id="437e7-136">First, begin the registration process by clicking the 'Linked Services' section of your data factory and then click 'New data store.'</span></span> <span data-ttu-id="437e7-137">Scegliere quindi un nome per registrare la risorsa di archiviazione di Azure, selezionare Archiviazione di Azure come tipo e immettere il nome dell'account e la chiave dell'account.</span><span class="sxs-lookup"><span data-stu-id="437e7-137">Choose a name to register your azure storage under, select Azure Storage as your type, and then enter your Account Name and Account Key.</span></span>
2. <span data-ttu-id="437e7-138">Per registrare SQL Data Warehouse passare alla sezione "Creare e distribuire", quindi selezionare "Nuovo archivio dati" e infine "Azure SQL Data Warehouse".</span><span class="sxs-lookup"><span data-stu-id="437e7-138">To register SQL Data Warehouse navigate to the 'Author and Deploy' section, select 'New Data Store', and then 'Azure SQL Data Warehouse'.</span></span> <span data-ttu-id="437e7-139">Copiare e incollare in questo modello e quindi immettere le informazioni specifiche.</span><span class="sxs-lookup"><span data-stu-id="437e7-139">Copy and paste in this template, and then fill in your specific information.</span></span>
   
    ```JSON
    {
        "name": "<Linked Service Name>",
        "properties": {
            "description": "",
            "type": "AzureSqlDW",
            "typeProperties": {
                 "connectionString": "Data Source=tcp:<server name>.database.windows.net,1433;Initial Catalog=<server name>;Integrated Security=False;User ID=<user>@<servername>;Password=<password>;Connect Timeout=30;Encrypt=True"
             }
        }
    }
    ```

### <a name="step-22-define-the-dataset"></a><span data-ttu-id="437e7-140">Passaggio 2.2: Definire il set di dati</span><span class="sxs-lookup"><span data-stu-id="437e7-140">Step 2.2: Define the dataset</span></span>
<span data-ttu-id="437e7-141">Dopo avere creato i servizi collegati, sarà necessario definire i set di dati,</span><span class="sxs-lookup"><span data-stu-id="437e7-141">After creating the linked services, we will have to define the data sets.</span></span>  <span data-ttu-id="437e7-142">ovvero definire la struttura dei dati da spostare dall'archiviazione al data warehouse.</span><span class="sxs-lookup"><span data-stu-id="437e7-142">Here this means defining the structure of the data that is being moved from your storage to your data warehouse.</span></span>  <span data-ttu-id="437e7-143">Altre informazioni sulla creazione</span><span class="sxs-lookup"><span data-stu-id="437e7-143">You can read more about creating</span></span>

1. <span data-ttu-id="437e7-144">Avviare il processo passando alla sezione 'Creare e distribuire' della data factory.</span><span class="sxs-lookup"><span data-stu-id="437e7-144">Start this process by navigating to the 'Author and Deploy' section of your data factory.</span></span>
2. <span data-ttu-id="437e7-145">Fare clic su 'Nuovo set di dati' e quindi su 'Archivio BLOB di Azure' per collegare la risorsa di archiviazione alla data factory.</span><span class="sxs-lookup"><span data-stu-id="437e7-145">Click 'New dataset' and then 'Azure Blob storage' to link your storage to your data factory.</span></span>  <span data-ttu-id="437e7-146">È possibile usare lo script seguente per definire i dati nell'archivio BLOB di Azure:</span><span class="sxs-lookup"><span data-stu-id="437e7-146">You can use the below script to define your data in Azure Blob storage:</span></span>
   
    ```JSON
    {
        "name": "<Dataset Name>",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "<linked storage name>",
            "typeProperties": {
                "folderPath": "<containter name>",
                "fileName": "FactInternetSales.csv",
                "format": {
                "type": "TextFormat",
                "columnDelimiter": ",",
                "rowDelimiter": "\n"
                }
            },
            "external": true,
            "availability": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "externalData": {
                    "retryInterval": "00:01:00",
                    "retryTimeout": "00:10:00",
                    "maximumRetry": 3
                }
            }
        }
    }
    ```
3. <span data-ttu-id="437e7-147">Verrà ora definito il set di dati per SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="437e7-147">Now we define our dataset for SQL Data Warehouse.</span></span> <span data-ttu-id="437e7-148">Si inizia sempre facendo clic su 'Nuovo set di dati' e quindi su 'Azure SQL Data Warehouse'.</span><span class="sxs-lookup"><span data-stu-id="437e7-148">We start in the same way, by clicking 'New dataset' and then 'Azure SQL Data Warehouse'.</span></span>
   
    ```JSON
    {
        "name": "DWDataset",
        "properties": {
            "type": "AzureSqlDWTable",
            "linkedServiceName": "AzureSqlDWLinkedService",
            "typeProperties": {
                "tableName": "FactInternetSales"
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            }
        }
    }
    ```

## <a name="step-3-create-and-run-your-pipeline"></a><span data-ttu-id="437e7-149">Passaggio 3: Creare ed eseguire la pipeline</span><span class="sxs-lookup"><span data-stu-id="437e7-149">Step 3: Create and run your pipeline</span></span>
<span data-ttu-id="437e7-150">Viene infine configurata ed eseguita la pipeline in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="437e7-150">Finally, we set up and run the pipeline in Azure Data Factory.</span></span>  <span data-ttu-id="437e7-151">Questa operazione completa lo spostamento effettivo dei dati.</span><span class="sxs-lookup"><span data-stu-id="437e7-151">This is the operation that completes the actual data movement.</span></span>  <span data-ttu-id="437e7-152">Per una visualizzazione completa delle operazioni che è possibile completare con SQL Data Warehouse e Azure Data Factory, vedere [qui][Move data to and from Azure SQL Data Warehouse using Azure Data Factory].</span><span class="sxs-lookup"><span data-stu-id="437e7-152">You can find a full view of the operations that you can complete with SQL Data Warehouse and Azure Data Factory [here][Move data to and from Azure SQL Data Warehouse using Azure Data Factory].</span></span>

<span data-ttu-id="437e7-153">Nella sezione "Creare e distribuire" fare clic su "Più comandi" e quindi su "Nuova pipeline".</span><span class="sxs-lookup"><span data-stu-id="437e7-153">In the 'Author and Deploy' section, click 'More Commands' and then 'New Pipeline'.</span></span>  <span data-ttu-id="437e7-154">Dopo la creazione della pipeline, è possibile usare il codice seguente per trasferire i dati al data warehouse:</span><span class="sxs-lookup"><span data-stu-id="437e7-154">After you create the pipeline, you can use the below code to transfer the data to your data warehouse:</span></span>

```JSON
{
    "name": "<Pipeline Name>",
    "properties": {
        "description": "<Description>",
        "activities": [
          {
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "BlobSource",
                    "skipHeaderLineCount": 1
                },
                "sink": {
                    "type": "SqlDWSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:10"
                }
            },
            "inputs": [
              {
                "name": "<Storage Dataset>"
              }
            ],
            "outputs": [
              {
                "name": "<Data Warehouse Dataset>"
              }
            ],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "Sample Copy",
            "description": "Copy Activity"
          }
        ],
        "start": "<Date YYYY-MM-DD>",
        "end": "<Date YYYY-MM-DD>",
        "isPaused": false
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="437e7-155">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="437e7-155">Next steps</span></span>
<span data-ttu-id="437e7-156">Per altre informazioni, vedere:</span><span class="sxs-lookup"><span data-stu-id="437e7-156">To learn more, start by viewing:</span></span>

* <span data-ttu-id="437e7-157">[Percorso di apprendimento per Azure Data Factory][Azure Data Factory learning path].</span><span class="sxs-lookup"><span data-stu-id="437e7-157">[Azure Data Factory learning path][Azure Data Factory learning path].</span></span>
* <span data-ttu-id="437e7-158">[Connettore Azure SQL Data Warehouse][Azure SQL Data Warehouse Connector].</span><span class="sxs-lookup"><span data-stu-id="437e7-158">[Azure SQL Data Warehouse Connector][Azure SQL Data Warehouse Connector].</span></span> <span data-ttu-id="437e7-159">Questo è l'argomento di riferimento di base per l'uso di Azure Data Factory con Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="437e7-159">This is the core reference topic for using Azure Data Factory with Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="437e7-160">Questi argomenti forniscono informazioni dettagliate su Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="437e7-160">These topics provide detailed information about Azure Data Factory.</span></span> <span data-ttu-id="437e7-161">Illustrano il database SQL di Azure o HDInsight, ma le informazioni si applicano anche ad Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="437e7-161">They discuss Azure SQL Database or HDInsight, but the information also applies to Azure SQL Data Warehouse.</span></span>

* <span data-ttu-id="437e7-162">[Esercitazione: Creare la prima data factory][Tutorial: Get started with Azure Data Factory]: questa è l'esercitazione di base per l'elaborazione dei dati con Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="437e7-162">[Tutorial: Get started with Azure Data Factory][Tutorial: Get started with Azure Data Factory] This is the core tutorial for processing data with Azure Data Factory.</span></span> <span data-ttu-id="437e7-163">In questa esercitazione verrà creata una prima pipeline che usa HDInsight per trasformare e analizzare i blog ogni mese.</span><span class="sxs-lookup"><span data-stu-id="437e7-163">In this tutorial, you will build your first pipeline that uses HDInsight to transform and analyze web logs on a monthly basis.</span></span> <span data-ttu-id="437e7-164">Si noti che questa esercitazione non prevede attività di copia.</span><span class="sxs-lookup"><span data-stu-id="437e7-164">Note, there is no copy activity in this tutorial.</span></span>
* <span data-ttu-id="437e7-165">[Esercitazione: Copiare i dati dal BLOB di archiviazione di Azure al database SQL di Azure][Tutorial: Copy data from Azure Storage Blob to Azure SQL Database].</span><span class="sxs-lookup"><span data-stu-id="437e7-165">[Tutorial: Copy data from Azure Storage Blob to Azure SQL Database][Tutorial: Copy data from Azure Storage Blob to Azure SQL Database].</span></span> <span data-ttu-id="437e7-166">In questa esercitazione verrà creata una pipeline in Azure Data Factory per copiare i dati da un BLOB del servizio di archiviazione di Azure a un database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="437e7-166">In this tutorial, you create a pipeline in Azure Data Factory to copy data from Azure Storage Blob to Azure SQL Database.</span></span>

<!--Image references-->

<!--Article references-->
[AZCopy documentation]: ../storage/storage-use-azcopy.md
[Azure SQL Data Warehouse Connector]: ../data-factory/data-factory-azure-sql-data-warehouse-connector.md
[BCP]: sql-data-warehouse-load-with-bcp.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Create a storage account]: ../storage/storage-create-storage-account.md#create-a-storage-account
[Data Factory]: sql-data-warehouse-get-started-load-with-azure-data-factory.md
[Get started with Azure Data Factory (Data Factory Editor)]: ../data-factory/data-factory-build-your-first-pipeline-using-editor.md
[Introduction to Azure Data Factory]: ../data-factory/data-factory-introduction.md
[Load sample data into SQL Data Warehouse]: sql-data-warehouse-load-sample-databases.md
[Move data to and from Azure SQL Data Warehouse using Azure Data Factory]: ../data-factory/data-factory-azure-sql-data-warehouse-connector.md
[PolyBase]: sql-data-warehouse-get-started-load-with-polybase.md
[Tutorial: Copy data from Azure Storage Blob to Azure SQL Database]: ../data-factory/data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[Tutorial: Get started with Azure Data Factory]: ../data-factory/data-factory-build-your-first-pipeline.md

<!--MSDN references-->

<!--Other Web references-->
[Azure Data Factory learning path]: https://azure.microsoft.com/documentation/learning-paths/data-factory
[Azure portal]: https://portal.azure.com
[Download sample data]: https://migrhoststorage.blob.core.windows.net/adfsample/FactInternetSales.csv
