---
title: 'Esercitazione: Creare una pipeline usando il modello di Resource Manager | Documentazione Microsoft'
description: In questa esercitazione si crea una pipeline di Azure Data Factory usando un modello di Azure Resource Manager. La pipeline copia i dati da un archivio BLOB di Azure a un database SQL di Azure.
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 1274e11a-e004-4df5-af07-850b2de7c15e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 8a155213ed17e516a5c46abbe3d8a2bcc52268ed
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-use-azure-resource-manager-template-to-create-a-data-factory-pipeline-to-copy-data"></a><span data-ttu-id="bfed6-104">Esercitazione: Usare un modello di Azure Resource Manager per creare una pipeline di Data Factory per copiare dati</span><span class="sxs-lookup"><span data-stu-id="bfed6-104">Tutorial: Use Azure Resource Manager template to create a Data Factory pipeline to copy data</span></span> 
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bfed6-105">Panoramica e prerequisiti</span><span class="sxs-lookup"><span data-stu-id="bfed6-105">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="bfed6-106">Copia guidata</span><span class="sxs-lookup"><span data-stu-id="bfed6-106">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="bfed6-107">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="bfed6-107">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="bfed6-108">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bfed6-108">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="bfed6-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bfed6-109">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="bfed6-110">Modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="bfed6-110">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="bfed6-111">API REST</span><span class="sxs-lookup"><span data-stu-id="bfed6-111">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="bfed6-112">API .NET</span><span class="sxs-lookup"><span data-stu-id="bfed6-112">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
> 
> 

<span data-ttu-id="bfed6-113">Questa esercitazione illustra come usare un modello di Azure Resource Manager per creare una data factory di Azure.</span><span class="sxs-lookup"><span data-stu-id="bfed6-113">This tutorial shows you how to use an Azure Resource Manager template to create an Azure data factory.</span></span> <span data-ttu-id="bfed6-114">La pipeline di dati in questa esercitazione copia i dati da un archivio dati di origine a un archivio dati di destinazione.</span><span class="sxs-lookup"><span data-stu-id="bfed6-114">The data pipeline in this tutorial copies data from a source data store to a destination data store.</span></span> <span data-ttu-id="bfed6-115">Non trasforma i dati di input per produrre dati di output.</span><span class="sxs-lookup"><span data-stu-id="bfed6-115">It does not transform input data to produce output data.</span></span> <span data-ttu-id="bfed6-116">Per un'esercitazione su come trasformare i dati usando Azure Data Factory, vedere [Esercitazione: Creare una pipeline per trasformare i dati usando un cluster Hadoop](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="bfed6-116">For a tutorial on how to transform data using Azure Data Factory, see [Tutorial: Build a pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

<span data-ttu-id="bfed6-117">In questa esercitazione si crea una pipeline contenente una sola attività: un'attività di copia</span><span class="sxs-lookup"><span data-stu-id="bfed6-117">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="bfed6-118">che copia i dati da un archivio dati supportato a un archivio dati sink supportato.</span><span class="sxs-lookup"><span data-stu-id="bfed6-118">The copy activity copies data from a supported data store to a supported sink data store.</span></span> <span data-ttu-id="bfed6-119">Per un elenco degli archivi dati supportati come origini e sink, vedere gli [archivi dati supportati](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="bfed6-119">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="bfed6-120">e si basa su un servizio disponibile a livello globale che può copiare dati tra diversi archivi dati in modo sicuro, affidabile e scalabile.</span><span class="sxs-lookup"><span data-stu-id="bfed6-120">The activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="bfed6-121">Per altre informazioni sull'attività di copia, vedere le [attività di spostamento dei dati](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="bfed6-121">For more information about the Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="bfed6-122">Una pipeline può includere più attività</span><span class="sxs-lookup"><span data-stu-id="bfed6-122">A pipeline can have more than one activity.</span></span> <span data-ttu-id="bfed6-123">ed è possibile concatenarne due, ovvero eseguire un'attività dopo l'altra, impostando il set di dati di output di un'attività come set di dati di input dell'altra.</span><span class="sxs-lookup"><span data-stu-id="bfed6-123">And, you can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="bfed6-124">Per altre informazioni, vedere [Attività multiple in una pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="bfed6-124">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span> 

> [!NOTE] 
> <span data-ttu-id="bfed6-125">La pipeline di dati in questa esercitazione copia i dati da un archivio dati di origine a un archivio dati di destinazione.</span><span class="sxs-lookup"><span data-stu-id="bfed6-125">The data pipeline in this tutorial copies data from a source data store to a destination data store.</span></span> <span data-ttu-id="bfed6-126">Per un'esercitazione su come trasformare i dati usando Azure Data Factory, vedere [Esercitazione: Creare una pipeline per trasformare i dati usando un cluster Hadoop](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="bfed6-126">For a tutorial on how to transform data using Azure Data Factory, see [Tutorial: Build a pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="bfed6-127">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="bfed6-127">Prerequisites</span></span>
* <span data-ttu-id="bfed6-128">Vedere [Panoramica e prerequisiti dell'esercitazione](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) ed eseguire i passaggi relativi ai **prerequisiti**.</span><span class="sxs-lookup"><span data-stu-id="bfed6-128">Go through [Tutorial Overview and Prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) and complete the **prerequisite** steps.</span></span>
* <span data-ttu-id="bfed6-129">Seguire le istruzioni disponibili nell'articolo [Come installare e configurare Azure PowerShell](/powershell/azure/overview) per installare la versione più recente di Azure PowerShell nel computer.</span><span class="sxs-lookup"><span data-stu-id="bfed6-129">Follow instructions in [How to install and configure Azure PowerShell](/powershell/azure/overview) article to install latest version of Azure PowerShell on your computer.</span></span> <span data-ttu-id="bfed6-130">In questa esercitazione si usa PowerShell per distribuire le entità di Data Factory.</span><span class="sxs-lookup"><span data-stu-id="bfed6-130">In this tutorial, you use PowerShell to deploy Data Factory entities.</span></span> 
* <span data-ttu-id="bfed6-131">(facoltativo) Per informazioni sulla creazione di modelli di Azure Resource Manager, vedere [Creazione di modelli di Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="bfed6-131">(optional) See [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md) to learn about Azure Resource Manager templates.</span></span>

## <a name="in-this-tutorial"></a><span data-ttu-id="bfed6-132">Contenuto dell'esercitazione:</span><span class="sxs-lookup"><span data-stu-id="bfed6-132">In this tutorial</span></span>
<span data-ttu-id="bfed6-133">In questa esercitazione si crea una data factory con le entità di Data Factory seguenti:</span><span class="sxs-lookup"><span data-stu-id="bfed6-133">In this tutorial, you create a data factory with the following Data Factory entities:</span></span>

| <span data-ttu-id="bfed6-134">Entità</span><span class="sxs-lookup"><span data-stu-id="bfed6-134">Entity</span></span> | <span data-ttu-id="bfed6-135">Descrizione</span><span class="sxs-lookup"><span data-stu-id="bfed6-135">Description</span></span> |
| --- | --- |
| <span data-ttu-id="bfed6-136">Servizio collegato Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="bfed6-136">Azure Storage linked service</span></span> |<span data-ttu-id="bfed6-137">Collega l'account di archiviazione di Azure alla data factory.</span><span class="sxs-lookup"><span data-stu-id="bfed6-137">Links your Azure Storage account to the data factory.</span></span> <span data-ttu-id="bfed6-138">Archiviazione di Azure è l'archivio dati di origine e il database SQL di Azure è l'archivio dati del sink per l'attività di copia nell'esercitazione.</span><span class="sxs-lookup"><span data-stu-id="bfed6-138">Azure Storage is the source data store and Azure SQL database is the sink data store for the copy activity in the tutorial.</span></span> <span data-ttu-id="bfed6-139">Specifica l'account di archiviazione che contiene i dati di input per l'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="bfed6-139">It specifies the storage account that contains the input data for the copy activity.</span></span> |
| <span data-ttu-id="bfed6-140">Servizio collegato per il database SQL Azure</span><span class="sxs-lookup"><span data-stu-id="bfed6-140">Azure SQL Database linked service</span></span> |<span data-ttu-id="bfed6-141">Collega il database SQL di Azure alla data factory.</span><span class="sxs-lookup"><span data-stu-id="bfed6-141">Links your Azure SQL database to the data factory.</span></span> <span data-ttu-id="bfed6-142">Specifica il database SQL di Azure che contiene i dati di output per l'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="bfed6-142">It specifies the Azure SQL database that holds the output data for the copy activity.</span></span> |
| <span data-ttu-id="bfed6-143">Set di dati di input del BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="bfed6-143">Azure Blob input dataset</span></span> |<span data-ttu-id="bfed6-144">Fa riferimento al servizio collegato di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="bfed6-144">Refers to the Azure Storage linked service.</span></span> <span data-ttu-id="bfed6-145">Il servizio collegato fa riferimento a un account di archiviazione di Azure e il set di dati del BLOB di Azure specifica il contenitore, la cartella e il nome del file nella risorsa di archiviazione che contiene i dati di input.</span><span class="sxs-lookup"><span data-stu-id="bfed6-145">The linked service refers to an Azure Storage account and the Azure Blob dataset specifies the container, folder, and file name in the storage that holds the input data.</span></span> |
| <span data-ttu-id="bfed6-146">Set di dati di output di SQL Azure</span><span class="sxs-lookup"><span data-stu-id="bfed6-146">Azure SQL output dataset</span></span> |<span data-ttu-id="bfed6-147">Fa riferimento al servizio collegato SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="bfed6-147">Refers to the Azure SQL linked service.</span></span> <span data-ttu-id="bfed6-148">Il servizio collegato SQL di Azure fa riferimento a un server di Azure SQL e il set di dati SQL di Azure specifica il nome della tabella che contiene i dati di output.</span><span class="sxs-lookup"><span data-stu-id="bfed6-148">The Azure SQL linked service refers to an Azure SQL server and the Azure SQL dataset specifies the name of the table that holds the output data.</span></span> |
| <span data-ttu-id="bfed6-149">Data Pipeline</span><span class="sxs-lookup"><span data-stu-id="bfed6-149">Data pipeline</span></span> |<span data-ttu-id="bfed6-150">La pipeline ha un'attività di tipo copia che accetta il set di dati del BLOB di Azure come input e il set di dati SQL di Azure come output.</span><span class="sxs-lookup"><span data-stu-id="bfed6-150">The pipeline has one activity of type Copy that takes the Azure blob dataset as an input and the Azure SQL dataset as an output.</span></span> <span data-ttu-id="bfed6-151">L'attività di copia esegue la copia dei dati da un BLOB di Azure a una tabella nel database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="bfed6-151">The copy activity copies data from an Azure blob to a table in the Azure SQL database.</span></span> |

<span data-ttu-id="bfed6-152">Una data factory può comprendere una o più pipeline.</span><span class="sxs-lookup"><span data-stu-id="bfed6-152">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="bfed6-153">Una pipeline può comprendere una o più attività.</span><span class="sxs-lookup"><span data-stu-id="bfed6-153">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="bfed6-154">Esistono due tipi di attività: [attività di spostamento dei dati](data-factory-data-movement-activities.md) e [attività di trasformazione dei dati](data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="bfed6-154">There are two types of activities: [data movement activities](data-factory-data-movement-activities.md) and [data transformation activities](data-factory-data-transformation-activities.md).</span></span> <span data-ttu-id="bfed6-155">In questa esercitazione si crea una pipeline con una sola attività (attività di copia).</span><span class="sxs-lookup"><span data-stu-id="bfed6-155">In this tutorial, you create a pipeline with one activity (copy activity).</span></span>

![Copiare il BLOB di Azure nel database SQL di Azure](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/CopyBlob2SqlDiagram.png) 

<span data-ttu-id="bfed6-157">La sezione seguente contiene il modello di Resource Manager completo per la definizione di entità di Data Factory. In questo modo sarà possibile eseguire rapidamente l'esercitazione e testare il modello.</span><span class="sxs-lookup"><span data-stu-id="bfed6-157">The following section provides the complete Resource Manager template for defining Data Factory entities so that you can quickly run through the tutorial and test the template.</span></span> <span data-ttu-id="bfed6-158">Per conoscere come viene definita ogni entità di Data Factory, vedere la sezione [Entità di Data Factory nel modello](#data-factory-entities-in-the-template).</span><span class="sxs-lookup"><span data-stu-id="bfed6-158">To understand how each Data Factory entity is defined, see [Data Factory entities in the template](#data-factory-entities-in-the-template) section.</span></span>

## <a name="data-factory-json-template"></a><span data-ttu-id="bfed6-159">Modello JSON di Data Factory</span><span class="sxs-lookup"><span data-stu-id="bfed6-159">Data Factory JSON template</span></span>
<span data-ttu-id="bfed6-160">Il modello di Resource Manager principale per la definizione di una data factory è il seguente:</span><span class="sxs-lookup"><span data-stu-id="bfed6-160">The top-level Resource Manager template for defining a data factory is:</span></span> 

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": { ...
    },
    "variables": { ...
    },
    "resources": [
        {
            "name": "[parameters('dataFactoryName')]",
            "apiVersion": "[variables('apiVersion')]",
            "type": "Microsoft.DataFactory/datafactories",
            "location": "westus",
            "resources": [
                { ... },
                { ... },
                { ... },
                { ... }
            ]
        }
    ]
}
```
<span data-ttu-id="bfed6-161">Creare un file JSON denominato **ADFCopyTutorialARM.json** nella cartella **C:\ADFGetStarted** con il contenuto seguente:</span><span class="sxs-lookup"><span data-stu-id="bfed6-161">Create a JSON file named **ADFCopyTutorialARM.json** in **C:\ADFGetStarted** folder with the following content:</span></span>

```json
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "parameters": {
      "storageAccountName": { "type": "string", "metadata": { "description": "Name of the Azure storage account that contains the data to be copied." } },
      "storageAccountKey": { "type": "securestring", "metadata": { "description": "Key for the Azure storage account." } },
      "sourceBlobContainer": { "type": "string", "metadata": { "description": "Name of the blob container in the Azure Storage account." } },
      "sourceBlobName": { "type": "string", "metadata": { "description": "Name of the blob in the container that has the data to be copied to Azure SQL Database table" } },
      "sqlServerName": { "type": "string", "metadata": { "description": "Name of the Azure SQL Server that will hold the output/copied data." } },
      "databaseName": { "type": "string", "metadata": { "description": "Name of the Azure SQL Database in the Azure SQL server." } },
      "sqlServerUserName": { "type": "string", "metadata": { "description": "Name of the user that has access to the Azure SQL server." } },
      "sqlServerPassword": { "type": "securestring", "metadata": { "description": "Password for the user." } },
      "targetSQLTable": { "type": "string", "metadata": { "description": "Table in the Azure SQL Database that will hold the copied data." } 
      } 
    },
    "variables": {
      "dataFactoryName": "[concat('AzureBlobToAzureSQLDatabaseDF', uniqueString(resourceGroup().id))]",
      "azureSqlLinkedServiceName": "AzureSqlLinkedService",
      "azureStorageLinkedServiceName": "AzureStorageLinkedService",
      "blobInputDatasetName": "BlobInputDataset",
      "sqlOutputDatasetName": "SQLOutputDataset",
      "pipelineName": "Blob2SQLPipeline"
    },
    "resources": [
      {
        "name": "[variables('dataFactoryName')]",
        "apiVersion": "2015-10-01",
        "type": "Microsoft.DataFactory/datafactories",
        "location": "West US",
        "resources": [
          {
            "type": "linkedservices",
            "name": "[variables('azureStorageLinkedServiceName')]",
            "dependsOn": [
              "[variables('dataFactoryName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
              "type": "AzureStorage",
              "description": "Azure Storage linked service",
              "typeProperties": {
                "connectionString": "[concat('DefaultEndpointsProtocol=https;AccountName=',parameters('storageAccountName'),';AccountKey=',parameters('storageAccountKey'))]"
              }
            }
          },
          {
            "type": "linkedservices",
            "name": "[variables('azureSqlLinkedServiceName')]",
            "dependsOn": [
              "[variables('dataFactoryName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
              "type": "AzureSqlDatabase",
              "description": "Azure SQL linked service",
              "typeProperties": {
                "connectionString": "[concat('Server=tcp:',parameters('sqlServerName'),'.database.windows.net,1433;Database=', parameters('databaseName'), ';User ID=',parameters('sqlServerUserName'),';Password=',parameters('sqlServerPassword'),';Trusted_Connection=False;Encrypt=True;Connection Timeout=30')]"
              }
            }
          },
          {
            "type": "datasets",
            "name": "[variables('blobInputDatasetName')]",
            "dependsOn": [
              "[variables('dataFactoryName')]",
              "[variables('azureStorageLinkedServiceName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
              "type": "AzureBlob",
              "linkedServiceName": "[variables('azureStorageLinkedServiceName')]",
              "structure": [
                {
                  "name": "Column0",
                  "type": "String"
                },
                {
                  "name": "Column1",
                  "type": "String"
                }
              ],
              "typeProperties": {
                "folderPath": "[concat(parameters('sourceBlobContainer'), '/')]",
                "fileName": "[parameters('sourceBlobName')]",
                "format": {
                  "type": "TextFormat",
                  "columnDelimiter": ","
                }
              },
              "availability": {
                "frequency": "Hour",
                "interval": 1
              },
              "external": true
            }
          },
          {
            "type": "datasets",
            "name": "[variables('sqlOutputDatasetName')]",
            "dependsOn": [
              "[variables('dataFactoryName')]",
              "[variables('azureSqlLinkedServiceName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
              "type": "AzureSqlTable",
              "linkedServiceName": "[variables('azureSqlLinkedServiceName')]",
              "structure": [
                {
                  "name": "FirstName",
                  "type": "String"
                },
                {
                  "name": "LastName",
                  "type": "String"
                }
              ],
              "typeProperties": {
                "tableName": "[parameters('targetSQLTable')]"
              },
              "availability": {
                "frequency": "Hour",
                "interval": 1
              }
            }
          },
          {
            "type": "datapipelines",
            "name": "[variables('pipelineName')]",
            "dependsOn": [
              "[variables('dataFactoryName')]",
              "[variables('azureStorageLinkedServiceName')]",
              "[variables('azureSqlLinkedServiceName')]",
              "[variables('blobInputDatasetName')]",
              "[variables('sqlOutputDatasetName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
              "activities": [
                {
                  "name": "CopyFromAzureBlobToAzureSQL",
                  "description": "Copy data frm Azure blob to Azure SQL",
                  "type": "Copy",
                  "inputs": [
                    {
                      "name": "[variables('blobInputDatasetName')]"
                    }
                  ],
                  "outputs": [
                    {
                      "name": "[variables('sqlOutputDatasetName')]"
                    }
                  ],
                  "typeProperties": {
                    "source": {
                      "type": "BlobSource"
                    },
                    "sink": {
                      "type": "SqlSink",
                      "sqlWriterCleanupScript": "$$Text.Format('DELETE FROM {0}', 'emp')"
                    },
                    "translator": {
                      "type": "TabularTranslator",
                      "columnMappings": "Column0:FirstName,Column1:LastName"
                    }
                  },
                  "Policy": {
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 3,
                    "timeout": "01:00:00"
                  }
                }
              ],
              "start": "2017-05-11T00:00:00Z",
              "end": "2017-05-12T00:00:00Z"
            }
          }
        ]
      }
    ]
  }
```

## <a name="parameters-json"></a><span data-ttu-id="bfed6-162">Parametri JSON</span><span class="sxs-lookup"><span data-stu-id="bfed6-162">Parameters JSON</span></span>
<span data-ttu-id="bfed6-163">Creare un file JSON denominato **ADFCopyTutorialARM-Parameters.json** contenente i parametri per il modello di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="bfed6-163">Create a JSON file named **ADFCopyTutorialARM-Parameters.json** that contains parameters for the Azure Resource Manager template.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="bfed6-164">Specificare il nome e la chiave dell'account di archiviazione di Azure per i parametri storageAccountName e storageAccountKey.</span><span class="sxs-lookup"><span data-stu-id="bfed6-164">Specify name and key of your Azure Storage account for storageAccountName and storageAccountKey parameters.</span></span>  
> 
> <span data-ttu-id="bfed6-165">Specificare il server SQL Azure, il database, l'utente e la password per i parametri sqlServerName, databaseName, sqlServerUserName e sqlServerPassword.</span><span class="sxs-lookup"><span data-stu-id="bfed6-165">Specify Azure SQL server, database, user, and password for sqlServerName, databaseName, sqlServerUserName, and sqlServerPassword parameters.</span></span>  

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": { 
        "storageAccountName": { "value": "<Name of the Azure storage account>"    },
        "storageAccountKey": {
            "value": "<Key for the Azure storage account>"
        },
        "sourceBlobContainer": { "value": "adftutorial" },
        "sourceBlobName": { "value": "emp.txt" },
        "sqlServerName": { "value": "<Name of the Azure SQL server>" },
        "databaseName": { "value": "<Name of the Azure SQL database>" },
        "sqlServerUserName": { "value": "<Name of the user who has access to the Azure SQL database>" },
        "sqlServerPassword": { "value": "<password for the user>" },
        "targetSQLTable": { "value": "emp" }
    }
}
```

> [!IMPORTANT]
> <span data-ttu-id="bfed6-166">Si possono avere file JSON di parametri separati per gli ambienti di sviluppo, test e produzione che è possibile usare con lo stesso modello JSON di Data Factory.</span><span class="sxs-lookup"><span data-stu-id="bfed6-166">You may have separate parameter JSON files for development, testing, and production environments that you can use with the same Data Factory JSON template.</span></span> <span data-ttu-id="bfed6-167">Usando uno script di Power Shell, è possibile automatizzare la distribuzione delle entità di Data Factory in questi ambienti.</span><span class="sxs-lookup"><span data-stu-id="bfed6-167">By using a Power Shell script, you can automate deploying Data Factory entities in these environments.</span></span>  
> 
> 

## <a name="create-data-factory"></a><span data-ttu-id="bfed6-168">Creare un'istanza di Data Factory</span><span class="sxs-lookup"><span data-stu-id="bfed6-168">Create data factory</span></span>
1. <span data-ttu-id="bfed6-169">Avviare **Azure PowerShell** ed eseguire questo comando:</span><span class="sxs-lookup"><span data-stu-id="bfed6-169">Start **Azure PowerShell** and run the following command:</span></span>
   * <span data-ttu-id="bfed6-170">Eseguire il comando seguente e immettere il nome utente e la password usati per accedere al portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="bfed6-170">Run the following command and enter the user name and password that you use to sign in to the Azure portal.</span></span>
   
    ```PowerShell
    Login-AzureRmAccount    
    ```  
   * <span data-ttu-id="bfed6-171">Eseguire il comando seguente per visualizzare tutte le sottoscrizioni per l'account.</span><span class="sxs-lookup"><span data-stu-id="bfed6-171">Run the following command to view all the subscriptions for this account.</span></span>
   
    ```PowerShell
    Get-AzureRmSubscription
    ```   
   * <span data-ttu-id="bfed6-172">Eseguire il comando seguente per selezionare la sottoscrizione da usare.</span><span class="sxs-lookup"><span data-stu-id="bfed6-172">Run the following command to select the subscription that you want to work with.</span></span>
    
    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```    
2. <span data-ttu-id="bfed6-173">Eseguire il comando seguente per distribuire entità di Data Factory usando il modello di Resource Manager creato nel Passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="bfed6-173">Run the following command to deploy Data Factory entities using the Resource Manager template you created in Step 1.</span></span>

    ```PowerShell   
    New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile C:\ADFGetStarted\ADFCopyTutorialARM.json -TemplateParameterFile C:\ADFGetStarted\ADFCopyTutorialARM-Parameters.json
    ```

## <a name="monitor-pipeline"></a><span data-ttu-id="bfed6-174">Monitorare la pipeline</span><span class="sxs-lookup"><span data-stu-id="bfed6-174">Monitor pipeline</span></span>

1. <span data-ttu-id="bfed6-175">Accedere al [portale di Azure](https://portal.azure.com) con il proprio account Azure.</span><span class="sxs-lookup"><span data-stu-id="bfed6-175">Log in to the [Azure portal](https://portal.azure.com) using your Azure account.</span></span>
2. <span data-ttu-id="bfed6-176">Scegliere **Data factory** dal menu a sinistra o fare clic su **Altri servizi** e quindi su **Data factory** nella categoria **INTELLIGENCE E ANALISI**.</span><span class="sxs-lookup"><span data-stu-id="bfed6-176">Click **Data factories** on the left menu (or) click **More services** and click **Data factories** under **INTELLIGENCE + ANALYTICS** category.</span></span>
   
    ![Menu Data factory](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/data-factories-menu.png)
3. <span data-ttu-id="bfed6-178">Nella pagina **Data factory** cercare e trovare la data factory (AzureBlobToAzureSQLDatabaseDF).</span><span class="sxs-lookup"><span data-stu-id="bfed6-178">In the **Data factories** page, search for and find your data factory (AzureBlobToAzureSQLDatabaseDF).</span></span> 
   
    ![Cercare la data factory](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/search-for-data-factory.png)  
4. <span data-ttu-id="bfed6-180">Fare clic sulla data factory di Azure.</span><span class="sxs-lookup"><span data-stu-id="bfed6-180">Click your Azure data factory.</span></span> <span data-ttu-id="bfed6-181">Viene visualizzata la home page della data factory.</span><span class="sxs-lookup"><span data-stu-id="bfed6-181">You see the home page for the data factory.</span></span>
   
    ![Home page della data factory](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/data-factory-home-page.png)  
6. <span data-ttu-id="bfed6-183">Per monitorare la pipeline e i set di dati creati in questa esercitazione, seguire le istruzioni riportate nella sezione su come [monitorare set di dati e pipeline](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline).</span><span class="sxs-lookup"><span data-stu-id="bfed6-183">Follow instructions from [Monitor datasets and pipeline](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline) to monitor the pipeline and datasets you have created in this tutorial.</span></span> <span data-ttu-id="bfed6-184">Attualmente, Visual Studio non supporta il monitoraggio delle pipeline di Data Factory.</span><span class="sxs-lookup"><span data-stu-id="bfed6-184">Currently, Visual Studio does not support monitoring Data Factory pipelines.</span></span>
7. <span data-ttu-id="bfed6-185">Quando lo stato della sezione è **Pronto**, verificare che i dati siano copiati nella tabella **emp** nel database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="bfed6-185">When a slice is in the **Ready** state, verify that the data is copied to the **emp** table in the Azure SQL database.</span></span>


<span data-ttu-id="bfed6-186">Per altre informazioni su come usare i pannelli del portale di Azure per monitorare la pipeline e i set di dati creati in questa esercitazione, vedere l'articolo su come [monitorare set di dati e pipeline](data-factory-monitor-manage-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="bfed6-186">For more information on how to use Azure portal blades to monitor pipeline and datasets you have created in this tutorial, see [Monitor datasets and pipeline](data-factory-monitor-manage-pipelines.md) .</span></span>

<span data-ttu-id="bfed6-187">Per altre informazioni su come usare l'applicazione Monitoraggio e gestione per monitorare le pipeline di dati, vedere [Monitorare e gestire le pipeline di Azure Data Factory con l'app di monitoraggio](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="bfed6-187">For more information on how to use the Monitor & Manage application to monitor your data pipelines, see [Monitor and manage Azure Data Factory pipelines using Monitoring App](data-factory-monitor-manage-app.md).</span></span>

## <a name="data-factory-entities-in-the-template"></a><span data-ttu-id="bfed6-188">Entità di Data Factory nel modello</span><span class="sxs-lookup"><span data-stu-id="bfed6-188">Data Factory entities in the template</span></span>
### <a name="define-data-factory"></a><span data-ttu-id="bfed6-189">Definire una data factory</span><span class="sxs-lookup"><span data-stu-id="bfed6-189">Define data factory</span></span>
<span data-ttu-id="bfed6-190">È possibile definire una data factory nel modello di Resource Manager come illustrato nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="bfed6-190">You define a data factory in the Resource Manager template as shown in the following sample:</span></span>  

```json
"resources": [
{
    "name": "[variables('dataFactoryName')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "West US"
}
```

<span data-ttu-id="bfed6-191">Il valore dataFactoryName viene definito come segue:</span><span class="sxs-lookup"><span data-stu-id="bfed6-191">The dataFactoryName is defined as:</span></span> 

```json
"dataFactoryName": "[concat('AzureBlobToAzureSQLDatabaseDF', uniqueString(resourceGroup().id))]"
```

<span data-ttu-id="bfed6-192">È una stringa univoca basata sull'ID del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="bfed6-192">It is a unique string based on the resource group ID.</span></span>  

### <a name="defining-data-factory-entities"></a><span data-ttu-id="bfed6-193">Definizione di entità di Data factory</span><span class="sxs-lookup"><span data-stu-id="bfed6-193">Defining Data Factory entities</span></span>
<span data-ttu-id="bfed6-194">Le entità di Data Factory seguenti vengono definite nel modello JSON:</span><span class="sxs-lookup"><span data-stu-id="bfed6-194">The following Data Factory entities are defined in the JSON template:</span></span> 

1. [<span data-ttu-id="bfed6-195">Servizio collegato Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="bfed6-195">Azure Storage linked service</span></span>](#azure-storage-linked-service)
2. [<span data-ttu-id="bfed6-196">Servizio collegato SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="bfed6-196">Azure SQL linked service</span></span>](#azure-sql-database-linked-service)
3. [<span data-ttu-id="bfed6-197">Set di dati del BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="bfed6-197">Azure blob dataset</span></span>](#azure-blob-dataset)
4. [<span data-ttu-id="bfed6-198">Set di dati di Azure SQL</span><span class="sxs-lookup"><span data-stu-id="bfed6-198">Azure SQL dataset</span></span>](#azure-sql-dataset)
5. [<span data-ttu-id="bfed6-199">Pipeline di dati con un'attività di copia</span><span class="sxs-lookup"><span data-stu-id="bfed6-199">Data pipeline with a copy activity</span></span>](#data-pipeline)

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="bfed6-200">Servizio collegato Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="bfed6-200">Azure Storage linked service</span></span>
<span data-ttu-id="bfed6-201">AzureStorageLinkedService collega l'account di archiviazione di Azure alla data factory.</span><span class="sxs-lookup"><span data-stu-id="bfed6-201">The AzureStorageLinkedService links your Azure storage account to the data factory.</span></span> <span data-ttu-id="bfed6-202">Come parte dei [prerequisiti](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) è stato creato un contenitore e sono stati caricati i dati in questo account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="bfed6-202">You created a container and uploaded data to this storage account as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> <span data-ttu-id="bfed6-203">In questa sezione si specificano il nome e la chiave dell'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="bfed6-203">You specify the name and key of your Azure storage account in this section.</span></span> <span data-ttu-id="bfed6-204">Per informazioni dettagliate sulle proprietà JSON usate per definire un servizio collegato di Archiviazione di Azure, vedere [Servizio collegato Archiviazione di Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service).</span><span class="sxs-lookup"><span data-stu-id="bfed6-204">See [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used to define an Azure Storage linked service.</span></span> 

```json
{
    "type": "linkedservices",
    "name": "[variables('azureStorageLinkedServiceName')]",
    "dependsOn": [
        "[variables('dataFactoryName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
        "type": "AzureStorage",
        "description": "Azure Storage linked service",
        "typeProperties": {
            "connectionString": "[concat('DefaultEndpointsProtocol=https;AccountName=',parameters('storageAccountName'),';AccountKey=',parameters('storageAccountKey'))]"
        }
    }
}
```

<span data-ttu-id="bfed6-205">connectionString usa i parametri storageAccountName e storageAccountKey.</span><span class="sxs-lookup"><span data-stu-id="bfed6-205">The connectionString uses the storageAccountName and storageAccountKey parameters.</span></span> <span data-ttu-id="bfed6-206">I valori per questi parametri sono stati passati usando un file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="bfed6-206">The values for these parameters passed by using a configuration file.</span></span> <span data-ttu-id="bfed6-207">La definizione usa anche le variabili azureStroageLinkedService e dataFactoryName definite nel modello.</span><span class="sxs-lookup"><span data-stu-id="bfed6-207">The definition also uses variables: azureStroageLinkedService and dataFactoryName defined in the template.</span></span> 

#### <a name="azure-sql-database-linked-service"></a><span data-ttu-id="bfed6-208">Servizio collegato per il database SQL Azure</span><span class="sxs-lookup"><span data-stu-id="bfed6-208">Azure SQL Database linked service</span></span>
<span data-ttu-id="bfed6-209">AzureSqlLinkedService collega il database SQL di Azure alla data factory.</span><span class="sxs-lookup"><span data-stu-id="bfed6-209">AzureSqlLinkedService links your Azure SQL database to the data factory.</span></span> <span data-ttu-id="bfed6-210">I dati copiati dall'archivio BLOB vengono archiviati in questo database.</span><span class="sxs-lookup"><span data-stu-id="bfed6-210">The data that is copied from the blob storage is stored in this database.</span></span> <span data-ttu-id="bfed6-211">Come parte dei [prerequisiti](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) è stata creata la tabella emp in questo database.</span><span class="sxs-lookup"><span data-stu-id="bfed6-211">You created the emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> <span data-ttu-id="bfed6-212">In questa sezione si specificano il nome del server di Azure SQL, il nome del database, il nome utente e la password utente.</span><span class="sxs-lookup"><span data-stu-id="bfed6-212">You specify the Azure SQL server name, database name, user name, and user password in this section.</span></span> <span data-ttu-id="bfed6-213">Per informazioni dettagliate sulle proprietà JSON usate per definire un servizio collegato di Azure SQL, vedere [Servizio collegato Azure SQL](data-factory-azure-sql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="bfed6-213">See [Azure SQL linked service](data-factory-azure-sql-connector.md#linked-service-properties) for details about JSON properties used to define an Azure SQL linked service.</span></span>  

```json
{
    "type": "linkedservices",
    "name": "[variables('azureSqlLinkedServiceName')]",
    "dependsOn": [
      "[variables('dataFactoryName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
          "type": "AzureSqlDatabase",
          "description": "Azure SQL linked service",
          "typeProperties": {
            "connectionString": "[concat('Server=tcp:',parameters('sqlServerName'),'.database.windows.net,1433;Database=', parameters('databaseName'), ';User ID=',parameters('sqlServerUserName'),';Password=',parameters('sqlServerPassword'),';Trusted_Connection=False;Encrypt=True;Connection Timeout=30')]"
          }
    }
}
```

<span data-ttu-id="bfed6-214">connectionString usa i parametri sqlServerName, databaseName, sqlServerUserName e sqlServerPassword i cui valori vengono passati usando un file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="bfed6-214">The connectionString uses sqlServerName, databaseName, sqlServerUserName, and sqlServerPassword parameters whose values are passed by using a configuration file.</span></span> <span data-ttu-id="bfed6-215">La definizione usa anche le variabili seguenti del modello: azureSqlLinkedServiceName, dataFactoryName.</span><span class="sxs-lookup"><span data-stu-id="bfed6-215">The definition also uses the following variables from the template: azureSqlLinkedServiceName, dataFactoryName.</span></span>

#### <a name="azure-blob-dataset"></a><span data-ttu-id="bfed6-216">Set di dati del BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="bfed6-216">Azure blob dataset</span></span>
<span data-ttu-id="bfed6-217">Il servizio collegato Archiviazione di Azure specifica la stringa di connessione usata dal servizio Data Factory in fase di esecuzione per connettersi all'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="bfed6-217">The Azure storage linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure storage account.</span></span> <span data-ttu-id="bfed6-218">Nella definizione del set di dati del BLOB si specificano i nomi del contenitore BLOB, della cartella e del file contenente i dati di input.</span><span class="sxs-lookup"><span data-stu-id="bfed6-218">In Azure blob dataset definition, you specify names of blob container, folder, and file that contains the input data.</span></span> <span data-ttu-id="bfed6-219">Per informazioni dettagliate sulle proprietà JSON usate per definire un set di dati del BLOB di Azure, vedere [Proprietà del set di dati del BLOB di Azure](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="bfed6-219">See [Azure Blob dataset properties](data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used to define an Azure Blob dataset.</span></span> 

```json
{
    "type": "datasets",
    "name": "[variables('blobInputDatasetName')]",
    "dependsOn": [
      "[variables('dataFactoryName')]",
      "[variables('azureStorageLinkedServiceName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
        "type": "AzureBlob",
          "linkedServiceName": "[variables('azureStorageLinkedServiceName')]",
        "structure": [
        {
              "name": "Column0",
              "type": "String"
        },
        {
              "name": "Column1",
              "type": "String"
        }
          ],
          "typeProperties": {
            "folderPath": "[concat(parameters('sourceBlobContainer'), '/')]",
            "fileName": "[parameters('sourceBlobName')]",
            "format": {
                  "type": "TextFormat",
                  "columnDelimiter": ","
            }
          },
          "availability": {
            "frequency": "Hour",
            "interval": 1
          },
          "external": true
    }
}
```

#### <a name="azure-sql-dataset"></a><span data-ttu-id="bfed6-220">Set di dati di Azure SQL</span><span class="sxs-lookup"><span data-stu-id="bfed6-220">Azure SQL dataset</span></span>
<span data-ttu-id="bfed6-221">Viene specificato il nome della tabella nel database SQL di Azure che contiene i dati copiati dall'archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="bfed6-221">You specify the name of the table in the Azure SQL database that holds the copied data from the Azure Blob storage.</span></span> <span data-ttu-id="bfed6-222">Per informazioni dettagliate sulle proprietà JSON usate per definire un set di dati di Azure SQL, vedere [Proprietà del set di dati di Azure SQL](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="bfed6-222">See [Azure SQL dataset properties](data-factory-azure-sql-connector.md#dataset-properties) for details about JSON properties used to define an Azure SQL dataset.</span></span> 

```json
{
    "type": "datasets",
    "name": "[variables('sqlOutputDatasetName')]",
    "dependsOn": [
        "[variables('dataFactoryName')]",
          "[variables('azureSqlLinkedServiceName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
          "type": "AzureSqlTable",
          "linkedServiceName": "[variables('azureSqlLinkedServiceName')]",
          "structure": [
        {
              "name": "FirstName",
              "type": "String"
        },
        {
              "name": "LastName",
              "type": "String"
        }
          ],
          "typeProperties": {
            "tableName": "[parameters('targetSQLTable')]"
          },
          "availability": {
            "frequency": "Hour",
            "interval": 1
          }
    }
}
```

#### <a name="data-pipeline"></a><span data-ttu-id="bfed6-223">Data Pipeline</span><span class="sxs-lookup"><span data-stu-id="bfed6-223">Data pipeline</span></span>
<span data-ttu-id="bfed6-224">Viene definita una pipeline che copia i dati dal set di dati del BLOB di Azure al set di dati di Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="bfed6-224">You define a pipeline that copies data from the Azure blob dataset to the Azure SQL dataset.</span></span> <span data-ttu-id="bfed6-225">Per le descrizioni degli elementi JSON usati per definire una pipeline in questo esempio, vedere [Pipeline JSON](data-factory-create-pipelines.md#pipeline-json).</span><span class="sxs-lookup"><span data-stu-id="bfed6-225">See [Pipeline JSON](data-factory-create-pipelines.md#pipeline-json) for descriptions of JSON elements used to define a pipeline in this example.</span></span> 

```json
{
    "type": "datapipelines",
    "name": "[variables('pipelineName')]",
    "dependsOn": [
        "[variables('dataFactoryName')]",
          "[variables('azureStorageLinkedServiceName')]",
          "[variables('azureSqlLinkedServiceName')]",
          "[variables('blobInputDatasetName')]",
          "[variables('sqlOutputDatasetName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
          "activities": [
        {
              "name": "CopyFromAzureBlobToAzureSQL",
              "description": "Copy data frm Azure blob to Azure SQL",
              "type": "Copy",
              "inputs": [
            {
                  "name": "[variables('blobInputDatasetName')]"
            }
              ],
              "outputs": [
            {
                  "name": "[variables('sqlOutputDatasetName')]"
            }
              ],
              "typeProperties": {
                "source": {
                      "type": "BlobSource"
                },
                "sink": {
                      "type": "SqlSink",
                      "sqlWriterCleanupScript": "$$Text.Format('DELETE FROM {0}', 'emp')"
                },
                "translator": {
                      "type": "TabularTranslator",
                      "columnMappings": "Column0:FirstName,Column1:LastName"
                }
              },
              "Policy": {
                "concurrency": 1,
                "executionPriorityOrder": "NewestFirst",
                "retry": 3,
                "timeout": "01:00:00"
              }
        }
          ],
          "start": "2017-05-11T00:00:00Z",
          "end": "2017-05-12T00:00:00Z"
    }
}
```

## <a name="reuse-the-template"></a><span data-ttu-id="bfed6-226">Riutilizzare il modello</span><span class="sxs-lookup"><span data-stu-id="bfed6-226">Reuse the template</span></span>
<span data-ttu-id="bfed6-227">Nell'esercitazione sono stati creati un modello per definire le entità di Data Factory e un modello per passare i valori dei parametri.</span><span class="sxs-lookup"><span data-stu-id="bfed6-227">In the tutorial, you created a template for defining Data Factory entities and a template for passing values for parameters.</span></span> <span data-ttu-id="bfed6-228">La pipeline copia i dati da un account di archiviazione di Azure a un database SQL di Azure specificato tramite i parametri.</span><span class="sxs-lookup"><span data-stu-id="bfed6-228">The pipeline copies data from an Azure Storage account to an Azure SQL database specified via parameters.</span></span> <span data-ttu-id="bfed6-229">Per usare lo stesso modello per distribuire le entità di Data Factory in ambienti diversi, si crea un file dei parametri per ogni ambiente e lo si usa durante la distribuzione in tale ambiente.</span><span class="sxs-lookup"><span data-stu-id="bfed6-229">To use the same template to deploy Data Factory entities to different environments, you create a parameter file for each environment and use it when deploying to that environment.</span></span>     

<span data-ttu-id="bfed6-230">Esempio:</span><span class="sxs-lookup"><span data-stu-id="bfed6-230">Example:</span></span>  

```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Dev.json
```
```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Test.json
```
```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Production.json
```

<span data-ttu-id="bfed6-231">Si noti che il primo comando usa il file dei parametri per l'ambiente di sviluppo, il secondo per l'ambiente di test e il terzo per l'ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="bfed6-231">Notice that the first command uses parameter file for the development environment, second one for the test environment, and the third one for the production environment.</span></span>  

<span data-ttu-id="bfed6-232">È anche possibile riutilizzare il modello per eseguire attività ripetute.</span><span class="sxs-lookup"><span data-stu-id="bfed6-232">You can also reuse the template to perform repeated tasks.</span></span> <span data-ttu-id="bfed6-233">Ad esempio, è necessario creare più data factory con una o più pipeline che implementano la stessa logica, ma ogni data factory usa account di archiviazione e di database SQL diversi.</span><span class="sxs-lookup"><span data-stu-id="bfed6-233">For example, you need to create many data factories with one or more pipelines that implement the same logic but each data factory uses different Storage and SQL Database accounts.</span></span> <span data-ttu-id="bfed6-234">In questo scenario si usa lo stesso modello nello stesso ambiente (sviluppo, test o produzione) con file dei parametri diversi per creare le data factory.</span><span class="sxs-lookup"><span data-stu-id="bfed6-234">In this scenario, you use the same template in the same environment (dev, test, or production) with different parameter files to create data factories.</span></span>   

## <a name="next-steps"></a><span data-ttu-id="bfed6-235">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="bfed6-235">Next steps</span></span>
<span data-ttu-id="bfed6-236">In questa esercitazione sono stati usati l'archivio BLOB di Azure come archivio dati di origine e un database SQL di Azure come archivio dati di destinazione in un'operazione di copia.</span><span class="sxs-lookup"><span data-stu-id="bfed6-236">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="bfed6-237">La tabella seguente contiene un elenco degli archivi dati supportati come origini e come destinazioni dall'attività di copia:</span><span class="sxs-lookup"><span data-stu-id="bfed6-237">The following table provides a list of data stores supported as sources and destinations by the copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="bfed6-238">Per informazioni su come copiare dati da/in un archivio dati, fare clic sul collegamento relativo all'archivio dati nella tabella.</span><span class="sxs-lookup"><span data-stu-id="bfed6-238">To learn about how to copy data to/from a data store, click the link for the data store in the table.</span></span>
