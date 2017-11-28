---
redirect_url: /azure/sql-data-warehouse/sql-data-warehouse-load-with-data-factory
title: dati aaaLoad con Data Factory di Azure | Documenti Microsoft
description: Informazioni su dati tooload con Data Factory di Azure
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
ms.openlocfilehash: 4186bd88d14be33f90130a41e8df06ce1d7cbab2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-with-azure-data-factory"></a><span data-ttu-id="d635b-103">Caricare i dati con Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="d635b-103">Load Data with Azure Data Factory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d635b-104">Redgate</span><span class="sxs-lookup"><span data-stu-id="d635b-104">Redgate</span></span>](sql-data-warehouse-load-with-redgate.md)  
> * [<span data-ttu-id="d635b-105">Data Factory</span><span class="sxs-lookup"><span data-stu-id="d635b-105">Data Factory</span></span>](sql-data-warehouse-get-started-load-with-azure-data-factory.md)  
> * [<span data-ttu-id="d635b-106">PolyBase</span><span class="sxs-lookup"><span data-stu-id="d635b-106">PolyBase</span></span>](sql-data-warehouse-get-started-load-with-polybase.md)  
> * [<span data-ttu-id="d635b-107">BCP</span><span class="sxs-lookup"><span data-stu-id="d635b-107">BCP</span></span>](sql-data-warehouse-load-with-bcp.md)  
> 
> 

<span data-ttu-id="d635b-108">In questa esercitazione illustra come toocreate una pipeline di dati di Azure Data Factory toomove da tooAzure Blob di archiviazione di Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="d635b-108">This tutorial shows you how toocreate a pipeline in Azure Data Factory toomove data from Azure Storage Blob tooAzure SQL Data Warehouse.</span></span> <span data-ttu-id="d635b-109">Con hello viene visualizzata la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="d635b-109">With hello following steps you will:</span></span>

* <span data-ttu-id="d635b-110">Configurare dati di esempio in un BLOB del servizio di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="d635b-110">Set up sample data in an Azure Storage Blob.</span></span>
* <span data-ttu-id="d635b-111">Connettere le risorse tooAzure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="d635b-111">Connect resources tooAzure Data Factory.</span></span>
* <span data-ttu-id="d635b-112">Creare una pipeline di dati toomove da tooSQL BLOB di archiviazione del Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="d635b-112">Create a pipeline toomove data from Storage Blobs tooSQL Data Warehouse.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-Azure-SQL-Data-Warehouse-with-Azure-Data-Factory/player]
> 
> 

## <a name="before-you-begin"></a><span data-ttu-id="d635b-113">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="d635b-113">Before you begin</span></span>
<span data-ttu-id="d635b-114">toofamiliarize familiarità con Azure Data Factory, vedere [tooAzure introduzione Data Factory][Introduction tooAzure Data Factory].</span><span class="sxs-lookup"><span data-stu-id="d635b-114">toofamiliarize yourself with Azure Data Factory, see [Introduction tooAzure Data Factory][Introduction tooAzure Data Factory].</span></span>

### <a name="create-or-identify-resources"></a><span data-ttu-id="d635b-115">Creare o identificare le risorse</span><span class="sxs-lookup"><span data-stu-id="d635b-115">Create or identify resources</span></span>
<span data-ttu-id="d635b-116">Prima di iniziare questa esercitazione, è necessario hello toohave seguenti risorse:</span><span class="sxs-lookup"><span data-stu-id="d635b-116">Before starting this tutorial, you need toohave hello following resources:</span></span>

* <span data-ttu-id="d635b-117">**Blob di archiviazione Azure**: questa esercitazione viene utilizzato il Blob di archiviazione di Azure come origine dati hello per la pipeline di Data Factory di Azure hello e pertanto è necessario toohave un toostore disponibili hello campione di dati.</span><span class="sxs-lookup"><span data-stu-id="d635b-117">**Azure Storage Blob**: This tutorial uses Azure Storage Blob as hello data source for hello Azure Data Factory pipeline, and so you need toohave one available toostore hello sample data.</span></span> <span data-ttu-id="d635b-118">Se non hai uno già, informazioni su come troppo[creare un account di archiviazione][Create a storage account].</span><span class="sxs-lookup"><span data-stu-id="d635b-118">If you don't have one already, learn how too[Create a storage account][Create a storage account].</span></span>
* <span data-ttu-id="d635b-119">**SQL Data Warehouse**: questa esercitazione Sposta i dati di hello dal Blob di archiviazione di Azure troppo SQL Data Warehouse e pertanto necessario toohave un data warehouse online che viene caricato con i dati di esempio AdventureWorksDW hello.</span><span class="sxs-lookup"><span data-stu-id="d635b-119">**SQL Data Warehouse**: This tutorial moves hello data from Azure Storage Blob too SQL Data Warehouse and so need toohave a data warehouse online that is loaded with hello AdventureWorksDW sample data.</span></span> <span data-ttu-id="d635b-120">Se si dispone già di un data warehouse, informazioni su come troppo[eseguire il provisioning di uno][Create a SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="d635b-120">If you do not already have a data warehouse, learn how too[provision one][Create a SQL Data Warehouse].</span></span> <span data-ttu-id="d635b-121">Se si dispone di un data warehouse, ma non effettuare il provisioning con i dati di esempio hello, è possibile [caricarla manualmente][Load sample data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="d635b-121">If you have a data warehouse but didn't provision it with hello sample data, you can [load it manually][Load sample data into SQL Data Warehouse].</span></span>
* <span data-ttu-id="d635b-122">**Azure Data Factory**: Data Factory di Azure completa carico effettivo hello e pertanto è necessario toohave uno che è possibile utilizzare pipeline lo spostamento dei dati di toobuild hello.</span><span class="sxs-lookup"><span data-stu-id="d635b-122">**Azure Data Factory**: Azure Data Factory completes hello actual load and so you need toohave one that you can use toobuild hello data movement pipeline.</span></span> <span data-ttu-id="d635b-123">Se non hai uno già, informazioni su come toocreate uno nel passaggio 1 di [Introduzione a Data Factory di Azure (Editor delle Data Factory)][Get started with Azure Data Factory (Data Factory Editor)].</span><span class="sxs-lookup"><span data-stu-id="d635b-123">If you don't have one already, learn how toocreate one in Step 1 of [Get started with Azure Data Factory (Data Factory Editor)][Get started with Azure Data Factory (Data Factory Editor)].</span></span>
* <span data-ttu-id="d635b-124">**AZCopy**: È necessario dati di esempio hello toocopy AZCopy del Blob di archiviazione di Azure di tooyour client locale.</span><span class="sxs-lookup"><span data-stu-id="d635b-124">**AZCopy**: You need AZCopy toocopy hello sample data from your local client tooyour Azure Storage Blob.</span></span> <span data-ttu-id="d635b-125">Per le istruzioni di installazione, vedere hello [AZCopy documentazione][AZCopy documentation].</span><span class="sxs-lookup"><span data-stu-id="d635b-125">For install instructions, see hello [AZCopy documentation][AZCopy documentation].</span></span>

## <a name="step-1-copy-sample-data-tooazure-storage-blob"></a><span data-ttu-id="d635b-126">Passaggio 1: Copiare dati di esempio tooAzure Blob di archiviazione</span><span class="sxs-lookup"><span data-stu-id="d635b-126">Step 1: Copy sample data tooAzure Storage Blob</span></span>
<span data-ttu-id="d635b-127">Dopo aver creato tutti i componenti di hello pronti, si è pronti toocopy esempio dati tooyour Blob di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="d635b-127">Once you have all hello pieces ready, you are ready toocopy sample data tooyour Azure Storage Blob.</span></span>

1. <span data-ttu-id="d635b-128">[Scaricare i dati di esempio][Download sample data].</span><span class="sxs-lookup"><span data-stu-id="d635b-128">[Download sample data][Download sample data].</span></span> <span data-ttu-id="d635b-129">Questi dati aggiunge un altro tre anni di dati di vendita tooyour dati di esempio AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="d635b-129">This data adds another three years of sales data tooyour AdventureWorksDW sample data.</span></span>
2. <span data-ttu-id="d635b-130">Utilizzare questo comando di AZCopy toocopy hello tre anni di dati tooyour Blob di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="d635b-130">Use this AZCopy command toocopy hello three years of data tooyour Azure Storage Blob.</span></span>
   
    ````
    AzCopy /Source:<Sample Data Location>  /Dest:https://<storage account>.blob.core.windows.net/<container name> /DestKey:<storage key> /Pattern:FactInternetSales.csv
    ````

## <a name="step-2-connect-resources-tooazure-data-factory"></a><span data-ttu-id="d635b-131">Passaggio 2: Connettere le risorse tooAzure Data Factory</span><span class="sxs-lookup"><span data-stu-id="d635b-131">Step 2: Connect resources tooAzure Data Factory</span></span>
<span data-ttu-id="d635b-132">Ora che i dati di hello sono sul posto è possibile creare hello Azure Data Factory pipeline toomove hello dati dall'archiviazione blob di Azure in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="d635b-132">Now that hello data is in place we can create hello Azure Data Factory pipeline toomove hello data from Azure blob storage into SQL Data Warehouse.</span></span>

<span data-ttu-id="d635b-133">tooget avviato, aprire hello [portale di Azure] [ Azure portal] e selezionare la data factory dal menu a sinistra di hello.</span><span class="sxs-lookup"><span data-stu-id="d635b-133">tooget started, open hello [Azure portal][Azure portal] and select your data factory from hello left-hand menu.</span></span>

### <a name="step-21-create-linked-service"></a><span data-ttu-id="d635b-134">Passaggio 2.1: Creare servizi collegati</span><span class="sxs-lookup"><span data-stu-id="d635b-134">Step 2.1: Create Linked Service</span></span>
<span data-ttu-id="d635b-135">Collegare l'account di archiviazione di Azure e SQL Data Warehouse tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="d635b-135">Link your Azure storage account and SQL Data Warehouse tooyour data factory.</span></span>  

1. <span data-ttu-id="d635b-136">Innanzitutto, avviare il processo di registrazione di hello facendo clic nella sezione 'Servizi collegati' hello della data factory e quindi fare clic su 'Nuovo archivio dati.'</span><span class="sxs-lookup"><span data-stu-id="d635b-136">First, begin hello registration process by clicking hello 'Linked Services' section of your data factory and then click 'New data store.'</span></span> <span data-ttu-id="d635b-137">Scegliere un nome tooregister l'archiviazione di azure in archiviazione di Azure selezionare il tipo e quindi immettere il nome dell'Account e la chiave dell'Account.</span><span class="sxs-lookup"><span data-stu-id="d635b-137">Choose a name tooregister your azure storage under, select Azure Storage as your type, and then enter your Account Name and Account Key.</span></span>
2. <span data-ttu-id="d635b-138">SQL Data Warehouse tooregister passare toohello 'Autore e Distribuisci' sezione, selezionare 'Nuovo archivio dati' e 'Azure SQL Data Warehouse'.</span><span class="sxs-lookup"><span data-stu-id="d635b-138">tooregister SQL Data Warehouse navigate toohello 'Author and Deploy' section, select 'New Data Store', and then 'Azure SQL Data Warehouse'.</span></span> <span data-ttu-id="d635b-139">Copiare e incollare in questo modello e quindi immettere le informazioni specifiche.</span><span class="sxs-lookup"><span data-stu-id="d635b-139">Copy and paste in this template, and then fill in your specific information.</span></span>
   
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

### <a name="step-22-define-hello-dataset"></a><span data-ttu-id="d635b-140">Passaggio 2.2: Definire set di dati hello</span><span class="sxs-lookup"><span data-stu-id="d635b-140">Step 2.2: Define hello dataset</span></span>
<span data-ttu-id="d635b-141">Dopo la creazione di hello servizi collegati, abbiamo toodefine hello set di dati.</span><span class="sxs-lookup"><span data-stu-id="d635b-141">After creating hello linked services, we will have toodefine hello data sets.</span></span>  <span data-ttu-id="d635b-142">In questo caso, ciò significa definizione della struttura di dati viene spostati dal data warehouse tooyour archiviazione hello hello.</span><span class="sxs-lookup"><span data-stu-id="d635b-142">Here this means defining hello structure of hello data that is being moved from your storage tooyour data warehouse.</span></span>  <span data-ttu-id="d635b-143">Altre informazioni sulla creazione</span><span class="sxs-lookup"><span data-stu-id="d635b-143">You can read more about creating</span></span>

1. <span data-ttu-id="d635b-144">Avviare questo processo, passando toohello ' autore Distribuisci ' sezione e la data factory.</span><span class="sxs-lookup"><span data-stu-id="d635b-144">Start this process by navigating toohello 'Author and Deploy' section of your data factory.</span></span>
2. <span data-ttu-id="d635b-145">Fare clic su "Nuovo set di dati" e quindi toolink 'Archiviazione Blob di Azure' la data factory tooyour di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="d635b-145">Click 'New dataset' and then 'Azure Blob storage' toolink your storage tooyour data factory.</span></span>  <span data-ttu-id="d635b-146">È possibile utilizzare i dati hello sotto toodefine script nell'archiviazione Blob di Azure:</span><span class="sxs-lookup"><span data-stu-id="d635b-146">You can use hello below script toodefine your data in Azure Blob storage:</span></span>
   
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
3. <span data-ttu-id="d635b-147">Verrà ora definito il set di dati per SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="d635b-147">Now we define our dataset for SQL Data Warehouse.</span></span> <span data-ttu-id="d635b-148">Si inizierà in hello allo stesso modo, facendo clic su "Nuovo set di dati" e quindi 'Azure SQL Data Warehouse'.</span><span class="sxs-lookup"><span data-stu-id="d635b-148">We start in hello same way, by clicking 'New dataset' and then 'Azure SQL Data Warehouse'.</span></span>
   
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

## <a name="step-3-create-and-run-your-pipeline"></a><span data-ttu-id="d635b-149">Passaggio 3: Creare ed eseguire la pipeline</span><span class="sxs-lookup"><span data-stu-id="d635b-149">Step 3: Create and run your pipeline</span></span>
<span data-ttu-id="d635b-150">Infine, è impostato ed eseguire pipeline hello in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="d635b-150">Finally, we set up and run hello pipeline in Azure Data Factory.</span></span>  <span data-ttu-id="d635b-151">Si tratta di operazione hello che viene completato lo spostamento dei dati effettivi hello.</span><span class="sxs-lookup"><span data-stu-id="d635b-151">This is hello operation that completes hello actual data movement.</span></span>  <span data-ttu-id="d635b-152">È possibile trovare una visualizzazione completa di operazioni di hello che è possibile completare con SQL Data Warehouse e Data Factory di Azure [qui][Move data tooand from Azure SQL Data Warehouse using Azure Data Factory].</span><span class="sxs-lookup"><span data-stu-id="d635b-152">You can find a full view of hello operations that you can complete with SQL Data Warehouse and Azure Data Factory [here][Move data tooand from Azure SQL Data Warehouse using Azure Data Factory].</span></span>

<span data-ttu-id="d635b-153">Nella sezione 'Autore e Distribuisci' hello, fare clic su 'Più comandi' e quindi 'Nuova Pipeline'.</span><span class="sxs-lookup"><span data-stu-id="d635b-153">In hello 'Author and Deploy' section, click 'More Commands' and then 'New Pipeline'.</span></span>  <span data-ttu-id="d635b-154">Dopo aver creato la pipeline hello, è possibile utilizzare hello seguito codice tootransfer hello dati tooyour del data warehouse:</span><span class="sxs-lookup"><span data-stu-id="d635b-154">After you create hello pipeline, you can use hello below code tootransfer hello data tooyour data warehouse:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="d635b-155">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d635b-155">Next steps</span></span>
<span data-ttu-id="d635b-156">toolearn, iniziare la visualizzazione:</span><span class="sxs-lookup"><span data-stu-id="d635b-156">toolearn more, start by viewing:</span></span>

* <span data-ttu-id="d635b-157">[Percorso di apprendimento per Azure Data Factory][Azure Data Factory learning path].</span><span class="sxs-lookup"><span data-stu-id="d635b-157">[Azure Data Factory learning path][Azure Data Factory learning path].</span></span>
* <span data-ttu-id="d635b-158">[Connettore Azure SQL Data Warehouse][Azure SQL Data Warehouse Connector].</span><span class="sxs-lookup"><span data-stu-id="d635b-158">[Azure SQL Data Warehouse Connector][Azure SQL Data Warehouse Connector].</span></span> <span data-ttu-id="d635b-159">Questo è l'argomento di riferimento hello core per l'utilizzo di Data Factory di Azure con Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="d635b-159">This is hello core reference topic for using Azure Data Factory with Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="d635b-160">Questi argomenti forniscono informazioni dettagliate su Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="d635b-160">These topics provide detailed information about Azure Data Factory.</span></span> <span data-ttu-id="d635b-161">Vengono illustrate HDInsight o Database SQL di Azure, ma hello informazioni si applicano anche tooAzure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="d635b-161">They discuss Azure SQL Database or HDInsight, but hello information also applies tooAzure SQL Data Warehouse.</span></span>

* <span data-ttu-id="d635b-162">[Esercitazione: Introduzione a Data Factory di Azure] [ Tutorial: Get started with Azure Data Factory] si tratta di hello esercitazione di base per l'elaborazione dei dati con Data Factory di Azure.</span><span class="sxs-lookup"><span data-stu-id="d635b-162">[Tutorial: Get started with Azure Data Factory][Tutorial: Get started with Azure Data Factory] This is hello core tutorial for processing data with Azure Data Factory.</span></span> <span data-ttu-id="d635b-163">In questa esercitazione verrà compilare le pipeline prima che utilizza tootransform HDInsight e analizzare i log web su base mensile.</span><span class="sxs-lookup"><span data-stu-id="d635b-163">In this tutorial, you will build your first pipeline that uses HDInsight tootransform and analyze web logs on a monthly basis.</span></span> <span data-ttu-id="d635b-164">Si noti che questa esercitazione non prevede attività di copia.</span><span class="sxs-lookup"><span data-stu-id="d635b-164">Note, there is no copy activity in this tutorial.</span></span>
* <span data-ttu-id="d635b-165">[Esercitazione: Copiare i dati da tooAzure Blob di archiviazione di Azure SQL Database][Tutorial: Copy data from Azure Storage Blob tooAzure SQL Database].</span><span class="sxs-lookup"><span data-stu-id="d635b-165">[Tutorial: Copy data from Azure Storage Blob tooAzure SQL Database][Tutorial: Copy data from Azure Storage Blob tooAzure SQL Database].</span></span> <span data-ttu-id="d635b-166">In questa esercitazione è creare una pipeline di dati di Azure Data Factory toocopy da tooAzure Blob di archiviazione di Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="d635b-166">In this tutorial, you create a pipeline in Azure Data Factory toocopy data from Azure Storage Blob tooAzure SQL Database.</span></span>

<!--Image references-->

<!--Article references-->
[AZCopy documentation]: ../storage/storage-use-azcopy.md
[Azure SQL Data Warehouse Connector]: ../data-factory/data-factory-azure-sql-data-warehouse-connector.md
[BCP]: sql-data-warehouse-load-with-bcp.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Create a storage account]: ../storage/storage-create-storage-account.md#create-a-storage-account
[Data Factory]: sql-data-warehouse-get-started-load-with-azure-data-factory.md
[Get started with Azure Data Factory (Data Factory Editor)]: ../data-factory/data-factory-build-your-first-pipeline-using-editor.md
[Introduction tooAzure Data Factory]: ../data-factory/data-factory-introduction.md
[Load sample data into SQL Data Warehouse]: sql-data-warehouse-load-sample-databases.md
[Move data tooand from Azure SQL Data Warehouse using Azure Data Factory]: ../data-factory/data-factory-azure-sql-data-warehouse-connector.md
[PolyBase]: sql-data-warehouse-get-started-load-with-polybase.md
[Tutorial: Copy data from Azure Storage Blob tooAzure SQL Database]: ../data-factory/data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[Tutorial: Get started with Azure Data Factory]: ../data-factory/data-factory-build-your-first-pipeline.md

<!--MSDN references-->

<!--Other Web references-->
[Azure Data Factory learning path]: https://azure.microsoft.com/documentation/learning-paths/data-factory
[Azure portal]: https://portal.azure.com
[Download sample data]: https://migrhoststorage.blob.core.windows.net/adfsample/FactInternetSales.csv
