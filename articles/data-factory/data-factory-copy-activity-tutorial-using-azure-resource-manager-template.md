---
title: 'Esercitazione: Creare una pipeline usando il modello di Resource Manager | Documentazione Microsoft'
description: In questa esercitazione si crea una pipeline di Azure Data Factory usando un modello di Azure Resource Manager. Questa pipeline copia dati da un database di SQL Azure tooan di archiviazione blob di Azure.
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
ms.openlocfilehash: 1c7567cb0423f7ce3e0cab2d77a4d861b70eb56b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-use-azure-resource-manager-template-toocreate-a-data-factory-pipeline-toocopy-data"></a><span data-ttu-id="93d6d-104">Esercitazione: Usare Gestione risorse di Azure modello toocreate una Data Factory pipeline toocopy di dati</span><span class="sxs-lookup"><span data-stu-id="93d6d-104">Tutorial: Use Azure Resource Manager template toocreate a Data Factory pipeline toocopy data</span></span> 
> [!div class="op_single_selector"]
> * [<span data-ttu-id="93d6d-105">Panoramica e prerequisiti</span><span class="sxs-lookup"><span data-stu-id="93d6d-105">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="93d6d-106">Copia guidata</span><span class="sxs-lookup"><span data-stu-id="93d6d-106">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="93d6d-107">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="93d6d-107">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="93d6d-108">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="93d6d-108">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="93d6d-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="93d6d-109">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="93d6d-110">Modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="93d6d-110">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="93d6d-111">API REST</span><span class="sxs-lookup"><span data-stu-id="93d6d-111">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="93d6d-112">API .NET</span><span class="sxs-lookup"><span data-stu-id="93d6d-112">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
> 
> 

<span data-ttu-id="93d6d-113">In questa esercitazione illustra come toouse un toocreate modello di gestione risorse di Azure una data factory di Azure.</span><span class="sxs-lookup"><span data-stu-id="93d6d-113">This tutorial shows you how toouse an Azure Resource Manager template toocreate an Azure data factory.</span></span> <span data-ttu-id="93d6d-114">pipeline di dati Hello in questa esercitazione consente di copiare dati da un archivio dati di origine dati archivio tooa destinazione.</span><span class="sxs-lookup"><span data-stu-id="93d6d-114">hello data pipeline in this tutorial copies data from a source data store tooa destination data store.</span></span> <span data-ttu-id="93d6d-115">Non Trasforma dati di output tooproduce dati di input.</span><span class="sxs-lookup"><span data-stu-id="93d6d-115">It does not transform input data tooproduce output data.</span></span> <span data-ttu-id="93d6d-116">Per un'esercitazione su come dati di tootransform tramite Data Factory di Azure, vedere [esercitazione: creare una pipeline di dati tootransform utilizzando cluster Hadoop](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="93d6d-116">For a tutorial on how tootransform data using Azure Data Factory, see [Tutorial: Build a pipeline tootransform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

<span data-ttu-id="93d6d-117">In questa esercitazione si crea una pipeline contenente una sola attività: un'attività di copia</span><span class="sxs-lookup"><span data-stu-id="93d6d-117">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="93d6d-118">attività di copia Hello copia dati da un archivio dati di sink supportati tooa di archivio di dati supportati.</span><span class="sxs-lookup"><span data-stu-id="93d6d-118">hello copy activity copies data from a supported data store tooa supported sink data store.</span></span> <span data-ttu-id="93d6d-119">Per un elenco degli archivi dati supportati come origini e sink, vedere gli [archivi dati supportati](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="93d6d-119">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="93d6d-120">attività Hello è alimentato da un servizio disponibile a livello globale che è possibile copiare dati tra diversi archivi dati in modo sicuro, affidabile e scalabile.</span><span class="sxs-lookup"><span data-stu-id="93d6d-120">hello activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="93d6d-121">Per ulteriori informazioni sulle attività di copia hello, vedere [attività lo spostamento dei dati](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="93d6d-121">For more information about hello Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="93d6d-122">Una pipeline può includere più attività</span><span class="sxs-lookup"><span data-stu-id="93d6d-122">A pipeline can have more than one activity.</span></span> <span data-ttu-id="93d6d-123">Inoltre, è possibile concatenare le due attività (eseguire un'attività dopo l'altro) mediante l'impostazione di set di dati di hello output di un'attività come hello input set di dati di hello altre attività.</span><span class="sxs-lookup"><span data-stu-id="93d6d-123">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="93d6d-124">Per altre informazioni, vedere [Attività multiple in una pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="93d6d-124">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span> 

> [!NOTE] 
> <span data-ttu-id="93d6d-125">pipeline di dati Hello in questa esercitazione consente di copiare dati da un archivio dati di origine dati archivio tooa destinazione.</span><span class="sxs-lookup"><span data-stu-id="93d6d-125">hello data pipeline in this tutorial copies data from a source data store tooa destination data store.</span></span> <span data-ttu-id="93d6d-126">Per un'esercitazione su come dati di tootransform tramite Data Factory di Azure, vedere [esercitazione: creare una pipeline di dati tootransform utilizzando cluster Hadoop](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="93d6d-126">For a tutorial on how tootransform data using Azure Data Factory, see [Tutorial: Build a pipeline tootransform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="93d6d-127">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="93d6d-127">Prerequisites</span></span>
* <span data-ttu-id="93d6d-128">Seguire i passaggi [esercitazione panoramica e prerequisiti](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) e hello completo **prerequisito** passaggi.</span><span class="sxs-lookup"><span data-stu-id="93d6d-128">Go through [Tutorial Overview and Prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) and complete hello **prerequisite** steps.</span></span>
* <span data-ttu-id="93d6d-129">Seguire le istruzioni [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview) articolo tooinstall versione più recente di Azure PowerShell nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="93d6d-129">Follow instructions in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) article tooinstall latest version of Azure PowerShell on your computer.</span></span> <span data-ttu-id="93d6d-130">In questa esercitazione, utilizzare le entità di PowerShell toodeploy Data Factory.</span><span class="sxs-lookup"><span data-stu-id="93d6d-130">In this tutorial, you use PowerShell toodeploy Data Factory entities.</span></span> 
* <span data-ttu-id="93d6d-131">(facoltativo) Vedere [la creazione di modelli di gestione risorse di Azure](../azure-resource-manager/resource-group-authoring-templates.md) toolearn sui modelli di gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="93d6d-131">(optional) See [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md) toolearn about Azure Resource Manager templates.</span></span>

## <a name="in-this-tutorial"></a><span data-ttu-id="93d6d-132">Contenuto dell'esercitazione:</span><span class="sxs-lookup"><span data-stu-id="93d6d-132">In this tutorial</span></span>
<span data-ttu-id="93d6d-133">In questa esercitazione, si crea una factory di dati con hello entità Data Factory di seguito:</span><span class="sxs-lookup"><span data-stu-id="93d6d-133">In this tutorial, you create a data factory with hello following Data Factory entities:</span></span>

| <span data-ttu-id="93d6d-134">Entità</span><span class="sxs-lookup"><span data-stu-id="93d6d-134">Entity</span></span> | <span data-ttu-id="93d6d-135">Descrizione</span><span class="sxs-lookup"><span data-stu-id="93d6d-135">Description</span></span> |
| --- | --- |
| <span data-ttu-id="93d6d-136">Servizio collegato Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="93d6d-136">Azure Storage linked service</span></span> |<span data-ttu-id="93d6d-137">Collega la data factory toohello account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="93d6d-137">Links your Azure Storage account toohello data factory.</span></span> <span data-ttu-id="93d6d-138">Archiviazione di Azure è l'archivio dati di origine hello e database SQL di Azure è hello sink dati store per le attività di copia hello in esercitazione hello.</span><span class="sxs-lookup"><span data-stu-id="93d6d-138">Azure Storage is hello source data store and Azure SQL database is hello sink data store for hello copy activity in hello tutorial.</span></span> <span data-ttu-id="93d6d-139">Specifica account di archiviazione hello che contiene i dati di input per l'attività di copia hello hello.</span><span class="sxs-lookup"><span data-stu-id="93d6d-139">It specifies hello storage account that contains hello input data for hello copy activity.</span></span> |
| <span data-ttu-id="93d6d-140">Servizio collegato per il database SQL Azure</span><span class="sxs-lookup"><span data-stu-id="93d6d-140">Azure SQL Database linked service</span></span> |<span data-ttu-id="93d6d-141">Collega il toohello data factory di Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="93d6d-141">Links your Azure SQL database toohello data factory.</span></span> <span data-ttu-id="93d6d-142">Specifica i database SQL di Azure hello che contiene i dati di output di hello per attività di copia hello.</span><span class="sxs-lookup"><span data-stu-id="93d6d-142">It specifies hello Azure SQL database that holds hello output data for hello copy activity.</span></span> |
| <span data-ttu-id="93d6d-143">Set di dati di input del BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="93d6d-143">Azure Blob input dataset</span></span> |<span data-ttu-id="93d6d-144">Fa riferimento il servizio di archiviazione di Azure collegati toohello.</span><span class="sxs-lookup"><span data-stu-id="93d6d-144">Refers toohello Azure Storage linked service.</span></span> <span data-ttu-id="93d6d-145">Hello servizio collegato fa riferimento tooan account di archiviazione Azure e set di dati Blob di Azure hello specifica hello contenitore, cartella e nome file nel servizio di archiviazione che contiene i dati di input hello hello.</span><span class="sxs-lookup"><span data-stu-id="93d6d-145">hello linked service refers tooan Azure Storage account and hello Azure Blob dataset specifies hello container, folder, and file name in hello storage that holds hello input data.</span></span> |
| <span data-ttu-id="93d6d-146">Set di dati di output di SQL Azure</span><span class="sxs-lookup"><span data-stu-id="93d6d-146">Azure SQL output dataset</span></span> |<span data-ttu-id="93d6d-147">Fa riferimento a servizio collegato SQL Azure toohello.</span><span class="sxs-lookup"><span data-stu-id="93d6d-147">Refers toohello Azure SQL linked service.</span></span> <span data-ttu-id="93d6d-148">servizio collegato SQL Azure Hello fa riferimento a server SQL Azure tooan e set di dati SQL di Azure hello Specifica nome hello della tabella di hello che contiene i dati di output di hello.</span><span class="sxs-lookup"><span data-stu-id="93d6d-148">hello Azure SQL linked service refers tooan Azure SQL server and hello Azure SQL dataset specifies hello name of hello table that holds hello output data.</span></span> |
| <span data-ttu-id="93d6d-149">Data Pipeline</span><span class="sxs-lookup"><span data-stu-id="93d6d-149">Data pipeline</span></span> |<span data-ttu-id="93d6d-150">pipeline di Hello dispone di un'attività di copia che accetta i set di dati blob di Azure hello come input di tipo e set di dati di SQL Azure come output di hello.</span><span class="sxs-lookup"><span data-stu-id="93d6d-150">hello pipeline has one activity of type Copy that takes hello Azure blob dataset as an input and hello Azure SQL dataset as an output.</span></span> <span data-ttu-id="93d6d-151">attività di copia Hello copia dati da una tabella di tooa blob di Azure in database SQL di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="93d6d-151">hello copy activity copies data from an Azure blob tooa table in hello Azure SQL database.</span></span> |

<span data-ttu-id="93d6d-152">Una data factory può comprendere una o più pipeline.</span><span class="sxs-lookup"><span data-stu-id="93d6d-152">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="93d6d-153">Una pipeline può comprendere una o più attività.</span><span class="sxs-lookup"><span data-stu-id="93d6d-153">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="93d6d-154">Esistono due tipi di attività: [attività di spostamento dei dati](data-factory-data-movement-activities.md) e [attività di trasformazione dei dati](data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="93d6d-154">There are two types of activities: [data movement activities](data-factory-data-movement-activities.md) and [data transformation activities](data-factory-data-transformation-activities.md).</span></span> <span data-ttu-id="93d6d-155">In questa esercitazione si crea una pipeline con una sola attività (attività di copia).</span><span class="sxs-lookup"><span data-stu-id="93d6d-155">In this tutorial, you create a pipeline with one activity (copy activity).</span></span>

![Copiare il Blob di Azure tooAzure Database SQL](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/CopyBlob2SqlDiagram.png) 

<span data-ttu-id="93d6d-157">Hello nella sezione seguente fornisce hello completo Gestione risorse modello per la definizione di entità Data Factory, che è possibile eseguire rapidamente tramite modelli di hello hello esercitazione e test.</span><span class="sxs-lookup"><span data-stu-id="93d6d-157">hello following section provides hello complete Resource Manager template for defining Data Factory entities so that you can quickly run through hello tutorial and test hello template.</span></span> <span data-ttu-id="93d6d-158">toounderstand della definizione di ogni entità Data Factory, vedere [entità Data Factory nel modello hello](#data-factory-entities-in-the-template) sezione.</span><span class="sxs-lookup"><span data-stu-id="93d6d-158">toounderstand how each Data Factory entity is defined, see [Data Factory entities in hello template](#data-factory-entities-in-the-template) section.</span></span>

## <a name="data-factory-json-template"></a><span data-ttu-id="93d6d-159">Modello JSON di Data Factory</span><span class="sxs-lookup"><span data-stu-id="93d6d-159">Data Factory JSON template</span></span>
<span data-ttu-id="93d6d-160">Hello modello Gestione risorse di livello superiore per la definizione di una data factory è:</span><span class="sxs-lookup"><span data-stu-id="93d6d-160">hello top-level Resource Manager template for defining a data factory is:</span></span> 

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
<span data-ttu-id="93d6d-161">Creare un file JSON denominato **ADFCopyTutorialARM.json** in **C:\ADFGetStarted** cartella con hello seguente contenuto:</span><span class="sxs-lookup"><span data-stu-id="93d6d-161">Create a JSON file named **ADFCopyTutorialARM.json** in **C:\ADFGetStarted** folder with hello following content:</span></span>

```json
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "parameters": {
      "storageAccountName": { "type": "string", "metadata": { "description": "Name of hello Azure storage account that contains hello data toobe copied." } },
      "storageAccountKey": { "type": "securestring", "metadata": { "description": "Key for hello Azure storage account." } },
      "sourceBlobContainer": { "type": "string", "metadata": { "description": "Name of hello blob container in hello Azure Storage account." } },
      "sourceBlobName": { "type": "string", "metadata": { "description": "Name of hello blob in hello container that has hello data toobe copied tooAzure SQL Database table" } },
      "sqlServerName": { "type": "string", "metadata": { "description": "Name of hello Azure SQL Server that will hold hello output/copied data." } },
      "databaseName": { "type": "string", "metadata": { "description": "Name of hello Azure SQL Database in hello Azure SQL server." } },
      "sqlServerUserName": { "type": "string", "metadata": { "description": "Name of hello user that has access toohello Azure SQL server." } },
      "sqlServerPassword": { "type": "securestring", "metadata": { "description": "Password for hello user." } },
      "targetSQLTable": { "type": "string", "metadata": { "description": "Table in hello Azure SQL Database that will hold hello copied data." } 
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
                  "description": "Copy data frm Azure blob tooAzure SQL",
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

## <a name="parameters-json"></a><span data-ttu-id="93d6d-162">Parametri JSON</span><span class="sxs-lookup"><span data-stu-id="93d6d-162">Parameters JSON</span></span>
<span data-ttu-id="93d6d-163">Creare un file JSON denominato **ADFCopyTutorialARM Parameters.json** che contiene i parametri per il modello di gestione risorse di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="93d6d-163">Create a JSON file named **ADFCopyTutorialARM-Parameters.json** that contains parameters for hello Azure Resource Manager template.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="93d6d-164">Specificare il nome e la chiave dell'account di archiviazione di Azure per i parametri storageAccountName e storageAccountKey.</span><span class="sxs-lookup"><span data-stu-id="93d6d-164">Specify name and key of your Azure Storage account for storageAccountName and storageAccountKey parameters.</span></span>  
> 
> <span data-ttu-id="93d6d-165">Specificare il server SQL Azure, il database, l'utente e la password per i parametri sqlServerName, databaseName, sqlServerUserName e sqlServerPassword.</span><span class="sxs-lookup"><span data-stu-id="93d6d-165">Specify Azure SQL server, database, user, and password for sqlServerName, databaseName, sqlServerUserName, and sqlServerPassword parameters.</span></span>  

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": { 
        "storageAccountName": { "value": "<Name of hello Azure storage account>"    },
        "storageAccountKey": {
            "value": "<Key for hello Azure storage account>"
        },
        "sourceBlobContainer": { "value": "adftutorial" },
        "sourceBlobName": { "value": "emp.txt" },
        "sqlServerName": { "value": "<Name of hello Azure SQL server>" },
        "databaseName": { "value": "<Name of hello Azure SQL database>" },
        "sqlServerUserName": { "value": "<Name of hello user who has access toohello Azure SQL database>" },
        "sqlServerPassword": { "value": "<password for hello user>" },
        "targetSQLTable": { "value": "emp" }
    }
}
```

> [!IMPORTANT]
> <span data-ttu-id="93d6d-166">È possibile file JSON di parametro separato per lo sviluppo, test e ambienti di produzione che è possibile utilizzare con hello stesso modello di Data Factory JSON.</span><span class="sxs-lookup"><span data-stu-id="93d6d-166">You may have separate parameter JSON files for development, testing, and production environments that you can use with hello same Data Factory JSON template.</span></span> <span data-ttu-id="93d6d-167">Usando uno script di Power Shell, è possibile automatizzare la distribuzione delle entità di Data Factory in questi ambienti.</span><span class="sxs-lookup"><span data-stu-id="93d6d-167">By using a Power Shell script, you can automate deploying Data Factory entities in these environments.</span></span>  
> 
> 

## <a name="create-data-factory"></a><span data-ttu-id="93d6d-168">Creare un'istanza di Data Factory</span><span class="sxs-lookup"><span data-stu-id="93d6d-168">Create data factory</span></span>
1. <span data-ttu-id="93d6d-169">Avviare **Azure PowerShell** e hello esecuzione comando seguente:</span><span class="sxs-lookup"><span data-stu-id="93d6d-169">Start **Azure PowerShell** and run hello following command:</span></span>
   * <span data-ttu-id="93d6d-170">Eseguire hello comando seguente e immettere nome utente hello e la password usati toosign in toohello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="93d6d-170">Run hello following command and enter hello user name and password that you use toosign in toohello Azure portal.</span></span>
   
    ```PowerShell
    Login-AzureRmAccount    
    ```  
   * <span data-ttu-id="93d6d-171">Eseguire hello successivo comando tooview tutte le sottoscrizioni di hello per questo account.</span><span class="sxs-lookup"><span data-stu-id="93d6d-171">Run hello following command tooview all hello subscriptions for this account.</span></span>
   
    ```PowerShell
    Get-AzureRmSubscription
    ```   
   * <span data-ttu-id="93d6d-172">Sottoscrizione hello tooselect da toowork con il comando seguente hello esecuzione.</span><span class="sxs-lookup"><span data-stu-id="93d6d-172">Run hello following command tooselect hello subscription that you want toowork with.</span></span>
    
    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```    
2. <span data-ttu-id="93d6d-173">Eseguire hello successivo comando toodeploy Data Factory le entità utilizzando il modello di gestione risorse hello creato nel passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="93d6d-173">Run hello following command toodeploy Data Factory entities using hello Resource Manager template you created in Step 1.</span></span>

    ```PowerShell   
    New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile C:\ADFGetStarted\ADFCopyTutorialARM.json -TemplateParameterFile C:\ADFGetStarted\ADFCopyTutorialARM-Parameters.json
    ```

## <a name="monitor-pipeline"></a><span data-ttu-id="93d6d-174">Monitorare la pipeline</span><span class="sxs-lookup"><span data-stu-id="93d6d-174">Monitor pipeline</span></span>

1. <span data-ttu-id="93d6d-175">Accedi toohello [portale di Azure](https://portal.azure.com) utilizzando l'account di Azure.</span><span class="sxs-lookup"><span data-stu-id="93d6d-175">Log in toohello [Azure portal](https://portal.azure.com) using your Azure account.</span></span>
2. <span data-ttu-id="93d6d-176">Fare clic su **Data factory** hello sinistro menu (o) fare clic su **più servizi** e fare clic su **Data factory** in **INTELLIGENCE + analisi** categoria.</span><span class="sxs-lookup"><span data-stu-id="93d6d-176">Click **Data factories** on hello left menu (or) click **More services** and click **Data factories** under **INTELLIGENCE + ANALYTICS** category.</span></span>
   
    ![Menu Data factory](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/data-factories-menu.png)
3. <span data-ttu-id="93d6d-178">In hello **Data factory** pagina, cercare e individuare la data factory (AzureBlobToAzureSQLDatabaseDF).</span><span class="sxs-lookup"><span data-stu-id="93d6d-178">In hello **Data factories** page, search for and find your data factory (AzureBlobToAzureSQLDatabaseDF).</span></span> 
   
    ![Cercare la data factory](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/search-for-data-factory.png)  
4. <span data-ttu-id="93d6d-180">Fare clic sulla data factory di Azure.</span><span class="sxs-lookup"><span data-stu-id="93d6d-180">Click your Azure data factory.</span></span> <span data-ttu-id="93d6d-181">Vedrai hello home page per data factory di hello.</span><span class="sxs-lookup"><span data-stu-id="93d6d-181">You see hello home page for hello data factory.</span></span>
   
    ![Home page della data factory](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/data-factory-home-page.png)  
6. <span data-ttu-id="93d6d-183">Seguire le istruzioni da [monitorare set di dati e della pipeline](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline) pipeline hello toomonitor e set di dati è stato creato in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="93d6d-183">Follow instructions from [Monitor datasets and pipeline](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline) toomonitor hello pipeline and datasets you have created in this tutorial.</span></span> <span data-ttu-id="93d6d-184">Attualmente, Visual Studio non supporta il monitoraggio delle pipeline di Data Factory.</span><span class="sxs-lookup"><span data-stu-id="93d6d-184">Currently, Visual Studio does not support monitoring Data Factory pipelines.</span></span>
7. <span data-ttu-id="93d6d-185">Quando una sezione è hello **pronto** stato, verificare che i dati di hello toohello copiato **emp** tabella nel database di SQL Azure hello.</span><span class="sxs-lookup"><span data-stu-id="93d6d-185">When a slice is in hello **Ready** state, verify that hello data is copied toohello **emp** table in hello Azure SQL database.</span></span>


<span data-ttu-id="93d6d-186">Per ulteriori informazioni su come pipeline di toomonitor toouse pannelli portale Azure e set di dati è stato creato in questa esercitazione, vedere [monitorare set di dati e della pipeline](data-factory-monitor-manage-pipelines.md) .</span><span class="sxs-lookup"><span data-stu-id="93d6d-186">For more information on how toouse Azure portal blades toomonitor pipeline and datasets you have created in this tutorial, see [Monitor datasets and pipeline](data-factory-monitor-manage-pipelines.md) .</span></span>

<span data-ttu-id="93d6d-187">Per ulteriori informazioni su come toouse hello monitoraggio e Gestione applicazione toomonitor i dati delle pipeline, vedere [monitoraggio e la gestione delle pipeline di Data Factory di Azure utilizzando App monitoraggio](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="93d6d-187">For more information on how toouse hello Monitor & Manage application toomonitor your data pipelines, see [Monitor and manage Azure Data Factory pipelines using Monitoring App](data-factory-monitor-manage-app.md).</span></span>

## <a name="data-factory-entities-in-hello-template"></a><span data-ttu-id="93d6d-188">Entità di modello hello Factory di dati</span><span class="sxs-lookup"><span data-stu-id="93d6d-188">Data Factory entities in hello template</span></span>
### <a name="define-data-factory"></a><span data-ttu-id="93d6d-189">Definire una data factory</span><span class="sxs-lookup"><span data-stu-id="93d6d-189">Define data factory</span></span>
<span data-ttu-id="93d6d-190">È consigliabile definire una data factory nel modello di gestione risorse di hello come illustrato nel seguente esempio hello:</span><span class="sxs-lookup"><span data-stu-id="93d6d-190">You define a data factory in hello Resource Manager template as shown in hello following sample:</span></span>  

```json
"resources": [
{
    "name": "[variables('dataFactoryName')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "West US"
}
```

<span data-ttu-id="93d6d-191">dataFactoryName Hello è definito come:</span><span class="sxs-lookup"><span data-stu-id="93d6d-191">hello dataFactoryName is defined as:</span></span> 

```json
"dataFactoryName": "[concat('AzureBlobToAzureSQLDatabaseDF', uniqueString(resourceGroup().id))]"
```

<span data-ttu-id="93d6d-192">È una stringa univoca in base a hello ID gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="93d6d-192">It is a unique string based on hello resource group ID.</span></span>  

### <a name="defining-data-factory-entities"></a><span data-ttu-id="93d6d-193">Definizione di entità di Data factory</span><span class="sxs-lookup"><span data-stu-id="93d6d-193">Defining Data Factory entities</span></span>
<span data-ttu-id="93d6d-194">Hello entità Data Factory seguenti vengono definite nel modello JSON hello:</span><span class="sxs-lookup"><span data-stu-id="93d6d-194">hello following Data Factory entities are defined in hello JSON template:</span></span> 

1. [<span data-ttu-id="93d6d-195">Servizio collegato Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="93d6d-195">Azure Storage linked service</span></span>](#azure-storage-linked-service)
2. [<span data-ttu-id="93d6d-196">Servizio collegato SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="93d6d-196">Azure SQL linked service</span></span>](#azure-sql-database-linked-service)
3. [<span data-ttu-id="93d6d-197">Set di dati del BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="93d6d-197">Azure blob dataset</span></span>](#azure-blob-dataset)
4. [<span data-ttu-id="93d6d-198">Set di dati di Azure SQL</span><span class="sxs-lookup"><span data-stu-id="93d6d-198">Azure SQL dataset</span></span>](#azure-sql-dataset)
5. [<span data-ttu-id="93d6d-199">Pipeline di dati con un'attività di copia</span><span class="sxs-lookup"><span data-stu-id="93d6d-199">Data pipeline with a copy activity</span></span>](#data-pipeline)

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="93d6d-200">Servizio collegato Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="93d6d-200">Azure Storage linked service</span></span>
<span data-ttu-id="93d6d-201">Hello AzureStorageLinkedService collega la data factory toohello account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="93d6d-201">hello AzureStorageLinkedService links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="93d6d-202">È stato creato un contenitore e caricare l'account di archiviazione di dati toothis come parte di [prerequisiti](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="93d6d-202">You created a container and uploaded data toothis storage account as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> <span data-ttu-id="93d6d-203">Specificare il nome di hello e chiave dell'account di archiviazione di Azure in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="93d6d-203">You specify hello name and key of your Azure storage account in this section.</span></span> <span data-ttu-id="93d6d-204">Vedere [servizio collegato di archiviazione di Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service) per informazioni dettagliate su JSON proprietà utilizzate toodefine servizio collegato di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="93d6d-204">See [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used toodefine an Azure Storage linked service.</span></span> 

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

<span data-ttu-id="93d6d-205">connectionString Hello utilizza i parametri di storageAccountName e storageAccountKey hello.</span><span class="sxs-lookup"><span data-stu-id="93d6d-205">hello connectionString uses hello storageAccountName and storageAccountKey parameters.</span></span> <span data-ttu-id="93d6d-206">valori Hello per questi parametri passati mediante un file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="93d6d-206">hello values for these parameters passed by using a configuration file.</span></span> <span data-ttu-id="93d6d-207">definizione di Hello utilizza anche variabili: azureStroageLinkedService e dataFactoryName definiti nel modello di hello.</span><span class="sxs-lookup"><span data-stu-id="93d6d-207">hello definition also uses variables: azureStroageLinkedService and dataFactoryName defined in hello template.</span></span> 

#### <a name="azure-sql-database-linked-service"></a><span data-ttu-id="93d6d-208">Servizio collegato per il database SQL Azure</span><span class="sxs-lookup"><span data-stu-id="93d6d-208">Azure SQL Database linked service</span></span>
<span data-ttu-id="93d6d-209">AzureSqlLinkedService collega il toohello data factory di Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="93d6d-209">AzureSqlLinkedService links your Azure SQL database toohello data factory.</span></span> <span data-ttu-id="93d6d-210">dati Hello che viene copiati dall'archiviazione blob hello vengono archiviati nel database.</span><span class="sxs-lookup"><span data-stu-id="93d6d-210">hello data that is copied from hello blob storage is stored in this database.</span></span> <span data-ttu-id="93d6d-211">Tabella emp hello è stato creato in questo database come parte di [prerequisiti](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="93d6d-211">You created hello emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> <span data-ttu-id="93d6d-212">Specificare nome del server SQL Azure hello, nome del database, nome utente e password dell'utente in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="93d6d-212">You specify hello Azure SQL server name, database name, user name, and user password in this section.</span></span> <span data-ttu-id="93d6d-213">Vedere [servizio collegato SQL Azure](data-factory-azure-sql-connector.md#linked-service-properties) per informazioni dettagliate su JSON proprietà utilizzate toodefine servizio collegato SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="93d6d-213">See [Azure SQL linked service](data-factory-azure-sql-connector.md#linked-service-properties) for details about JSON properties used toodefine an Azure SQL linked service.</span></span>  

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

<span data-ttu-id="93d6d-214">connectionString Hello utilizza sqlServerName, databaseName, sqlServerUserName e sqlServerPassword parametri i cui valori vengono passati mediante un file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="93d6d-214">hello connectionString uses sqlServerName, databaseName, sqlServerUserName, and sqlServerPassword parameters whose values are passed by using a configuration file.</span></span> <span data-ttu-id="93d6d-215">Hello definizione utilizza inoltre hello seguenti variabili dal modello hello: azureSqlLinkedServiceName, dataFactoryName.</span><span class="sxs-lookup"><span data-stu-id="93d6d-215">hello definition also uses hello following variables from hello template: azureSqlLinkedServiceName, dataFactoryName.</span></span>

#### <a name="azure-blob-dataset"></a><span data-ttu-id="93d6d-216">Set di dati del BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="93d6d-216">Azure blob dataset</span></span>
<span data-ttu-id="93d6d-217">il servizio di archiviazione di Azure collegati Hello specifica hello stringa di connessione del servizio Data Factory utilizzata in fase di esecuzione tooconnect tooyour account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="93d6d-217">hello Azure storage linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="93d6d-218">Nella definizione di set di dati blob di Azure, specificare i nomi di contenitore blob, cartelle e file che contiene i dati di input hello.</span><span class="sxs-lookup"><span data-stu-id="93d6d-218">In Azure blob dataset definition, you specify names of blob container, folder, and file that contains hello input data.</span></span> <span data-ttu-id="93d6d-219">Vedere [proprietà set di dati Blob di Azure](data-factory-azure-blob-connector.md#dataset-properties) per informazioni dettagliate su JSON proprietà utilizzate toodefine un set di dati Blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="93d6d-219">See [Azure Blob dataset properties](data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used toodefine an Azure Blob dataset.</span></span> 

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

#### <a name="azure-sql-dataset"></a><span data-ttu-id="93d6d-220">Set di dati di Azure SQL</span><span class="sxs-lookup"><span data-stu-id="93d6d-220">Azure SQL dataset</span></span>
<span data-ttu-id="93d6d-221">Specificare il nome di hello della tabella hello in database SQL di Azure hello che contiene i dati copiato hello da hello archiviazione Blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="93d6d-221">You specify hello name of hello table in hello Azure SQL database that holds hello copied data from hello Azure Blob storage.</span></span> <span data-ttu-id="93d6d-222">Vedere [proprietà set di dati di SQL Azure](data-factory-azure-sql-connector.md#dataset-properties) per informazioni dettagliate su JSON proprietà utilizzate toodefine un set di dati di SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="93d6d-222">See [Azure SQL dataset properties](data-factory-azure-sql-connector.md#dataset-properties) for details about JSON properties used toodefine an Azure SQL dataset.</span></span> 

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

#### <a name="data-pipeline"></a><span data-ttu-id="93d6d-223">Data Pipeline</span><span class="sxs-lookup"><span data-stu-id="93d6d-223">Data pipeline</span></span>
<span data-ttu-id="93d6d-224">È possibile definire una pipeline che copia i dati dal set di dati SQL di Azure toohello di hello blob di Azure set di dati.</span><span class="sxs-lookup"><span data-stu-id="93d6d-224">You define a pipeline that copies data from hello Azure blob dataset toohello Azure SQL dataset.</span></span> <span data-ttu-id="93d6d-225">Vedere [JSON di Pipeline](data-factory-create-pipelines.md#pipeline-json) per le descrizioni degli elementi usati di JSON toodefine una pipeline in questo esempio.</span><span class="sxs-lookup"><span data-stu-id="93d6d-225">See [Pipeline JSON](data-factory-create-pipelines.md#pipeline-json) for descriptions of JSON elements used toodefine a pipeline in this example.</span></span> 

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
              "description": "Copy data frm Azure blob tooAzure SQL",
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

## <a name="reuse-hello-template"></a><span data-ttu-id="93d6d-226">Riutilizzare hello modello</span><span class="sxs-lookup"><span data-stu-id="93d6d-226">Reuse hello template</span></span>
<span data-ttu-id="93d6d-227">Nell'esercitazione hello è creato un modello per la definizione di entità Data Factory e un modello per il passaggio di valori per i parametri.</span><span class="sxs-lookup"><span data-stu-id="93d6d-227">In hello tutorial, you created a template for defining Data Factory entities and a template for passing values for parameters.</span></span> <span data-ttu-id="93d6d-228">pipeline Hello copia dati da un database di SQL Azure tooan di account di archiviazione di Azure specificato tramite i parametri.</span><span class="sxs-lookup"><span data-stu-id="93d6d-228">hello pipeline copies data from an Azure Storage account tooan Azure SQL database specified via parameters.</span></span> <span data-ttu-id="93d6d-229">toouse hello stessi ambienti con toodifferent entità modello toodeploy Data Factory, creare un file di parametro per ogni ambiente e usarlo quando si distribuisce toothat ambiente.</span><span class="sxs-lookup"><span data-stu-id="93d6d-229">toouse hello same template toodeploy Data Factory entities toodifferent environments, you create a parameter file for each environment and use it when deploying toothat environment.</span></span>     

<span data-ttu-id="93d6d-230">Esempio:</span><span class="sxs-lookup"><span data-stu-id="93d6d-230">Example:</span></span>  

```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Dev.json
```
```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Test.json
```
```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Production.json
```

<span data-ttu-id="93d6d-231">Si noti che hello primo comando Usa il file di parametro per l'ambiente di sviluppo hello, secondo una per hello ambiente di test e una terza per ambiente di produzione hello hello.</span><span class="sxs-lookup"><span data-stu-id="93d6d-231">Notice that hello first command uses parameter file for hello development environment, second one for hello test environment, and hello third one for hello production environment.</span></span>  

<span data-ttu-id="93d6d-232">È inoltre possibile riutilizzare hello modello tooperform ripetuto di attività.</span><span class="sxs-lookup"><span data-stu-id="93d6d-232">You can also reuse hello template tooperform repeated tasks.</span></span> <span data-ttu-id="93d6d-233">Ad esempio, è necessario toocreate molti data factory con uno o più pipeline che implementano hello stesso logica ma ogni data factory utilizza diversi account di archiviazione e il Database SQL.</span><span class="sxs-lookup"><span data-stu-id="93d6d-233">For example, you need toocreate many data factories with one or more pipelines that implement hello same logic but each data factory uses different Storage and SQL Database accounts.</span></span> <span data-ttu-id="93d6d-234">In questo scenario, si usa hello stesso modello in hello stesso ambiente (sviluppo, test o produzione) con parametri diversi file toocreate data factory.</span><span class="sxs-lookup"><span data-stu-id="93d6d-234">In this scenario, you use hello same template in hello same environment (dev, test, or production) with different parameter files toocreate data factories.</span></span>   

## <a name="next-steps"></a><span data-ttu-id="93d6d-235">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="93d6d-235">Next steps</span></span>
<span data-ttu-id="93d6d-236">In questa esercitazione sono stati usati l'archivio BLOB di Azure come archivio dati di origine e un database SQL di Azure come archivio dati di destinazione in un'operazione di copia.</span><span class="sxs-lookup"><span data-stu-id="93d6d-236">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="93d6d-237">Hello nella tabella seguente fornisce un elenco di archivi di dati supportato come origini e destinazioni da attività di copia hello:</span><span class="sxs-lookup"><span data-stu-id="93d6d-237">hello following table provides a list of data stores supported as sources and destinations by hello copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="93d6d-238">toolearn su come archiviano dati toocopy da e verso un tipo di dati, fare clic su collegamento hello per hello archivio di dati nella tabella hello.</span><span class="sxs-lookup"><span data-stu-id="93d6d-238">toolearn about how toocopy data to/from a data store, click hello link for hello data store in hello table.</span></span>
