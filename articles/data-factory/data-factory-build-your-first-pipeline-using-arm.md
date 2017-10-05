---
title: Creare la prima data factory (modello di Resource Manager) | Documentazione Microsoft
description: In questa esercitazione si crea una pipeline di esempio di Azure Data Factory usando il modello di Azure Resource Manager.
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: eb9e70b9-a13a-4a27-8256-2759496be470
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: c67169f296f2f13b9ee87180f126fb1dcf10fbea
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-resource-manager-template"></a><span data-ttu-id="c26e8-103">Esercitazione: Creare la prima data factory di Azure usando il modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c26e8-103">Tutorial: Build your first Azure data factory using Azure Resource Manager template</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c26e8-104">Panoramica e prerequisiti</span><span class="sxs-lookup"><span data-stu-id="c26e8-104">Overview and prerequisites</span></span>](data-factory-build-your-first-pipeline.md)
> * [<span data-ttu-id="c26e8-105">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="c26e8-105">Azure portal</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
> * [<span data-ttu-id="c26e8-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c26e8-106">Visual Studio</span></span>](data-factory-build-your-first-pipeline-using-vs.md)
> * [<span data-ttu-id="c26e8-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c26e8-107">PowerShell</span></span>](data-factory-build-your-first-pipeline-using-powershell.md)
> * [<span data-ttu-id="c26e8-108">Modello di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c26e8-108">Resource Manager Template</span></span>](data-factory-build-your-first-pipeline-using-arm.md)
> * [<span data-ttu-id="c26e8-109">API REST</span><span class="sxs-lookup"><span data-stu-id="c26e8-109">REST API</span></span>](data-factory-build-your-first-pipeline-using-rest-api.md)
> 
> 

<span data-ttu-id="c26e8-110">In questo articolo viene usato un modello di Azure Resource Manager per creare la prima data factory di Azure.</span><span class="sxs-lookup"><span data-stu-id="c26e8-110">In this article, you use an Azure Resource Manager template to create your first Azure data factory.</span></span> <span data-ttu-id="c26e8-111">Per eseguire l'esercitazione usando altri strumenti/SDK, selezionare una delle opzioni dall'elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="c26e8-111">To do the tutorial using other tools/SDKs, select one of the options from the drop-down list.</span></span>

<span data-ttu-id="c26e8-112">La pipeline in questa esercitazione include un'attività, l'**attività Hive di HDInsight**,</span><span class="sxs-lookup"><span data-stu-id="c26e8-112">The pipeline in this tutorial has one activity: **HDInsight Hive activity**.</span></span> <span data-ttu-id="c26e8-113">che esegue uno script Hive in un cluster Azure HDInsight per trasformare i dati di input e generare i dati di output.</span><span class="sxs-lookup"><span data-stu-id="c26e8-113">This activity runs a hive script on an Azure HDInsight cluster that transforms input data to produce output data.</span></span> <span data-ttu-id="c26e8-114">L'esecuzione della pipeline è pianificata una volta al mese tra le ore di inizio e di fine specificate.</span><span class="sxs-lookup"><span data-stu-id="c26e8-114">The pipeline is scheduled to run once a month between the specified start and end times.</span></span> 

> [!NOTE]
> <span data-ttu-id="c26e8-115">La pipeline di dati in questa esercitazione trasforma i dati di input per produrre dati di output.</span><span class="sxs-lookup"><span data-stu-id="c26e8-115">The data pipeline in this tutorial transforms input data to produce output data.</span></span> <span data-ttu-id="c26e8-116">Per un'esercitazione su come copiare dati usando Azure Data Factory, vedere [Copiare dati da un archivio BLOB al database SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="c26e8-116">For a tutorial on how to copy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage to SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
> 
> <span data-ttu-id="c26e8-117">La pipeline in questa esercitazione include solo un'attività di tipo HDInsightHive.</span><span class="sxs-lookup"><span data-stu-id="c26e8-117">The pipeline in this tutorial has only one activity of type: HDInsightHive.</span></span> <span data-ttu-id="c26e8-118">Una pipeline può includere più attività</span><span class="sxs-lookup"><span data-stu-id="c26e8-118">A pipeline can have more than one activity.</span></span> <span data-ttu-id="c26e8-119">ed è possibile concatenarne due, ovvero eseguire un'attività dopo l'altra, impostando il set di dati di output di un'attività come set di dati di input dell'altra.</span><span class="sxs-lookup"><span data-stu-id="c26e8-119">And, you can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="c26e8-120">Per altre informazioni, vedere [Pianificazione ed esecuzione in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="c26e8-120">For more information, see [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="c26e8-121">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="c26e8-121">Prerequisites</span></span>
* <span data-ttu-id="c26e8-122">Vedere la [panoramica dell'esercitazione](data-factory-build-your-first-pipeline.md) ed eseguire i passaggi relativi ai **prerequisiti** .</span><span class="sxs-lookup"><span data-stu-id="c26e8-122">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete the **prerequisite** steps.</span></span>
* <span data-ttu-id="c26e8-123">Seguire le istruzioni disponibili nell'articolo [Come installare e configurare Azure PowerShell](/powershell/azure/overview) per installare la versione più recente di Azure PowerShell nel computer.</span><span class="sxs-lookup"><span data-stu-id="c26e8-123">Follow instructions in [How to install and configure Azure PowerShell](/powershell/azure/overview) article to install latest version of Azure PowerShell on your computer.</span></span>
* <span data-ttu-id="c26e8-124">Per informazioni sulla creazione di modelli di Azure Resource Manager, vedere [Creazione di modelli di Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) .</span><span class="sxs-lookup"><span data-stu-id="c26e8-124">See [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md) to learn about Azure Resource Manager templates.</span></span> 

## <a name="in-this-tutorial"></a><span data-ttu-id="c26e8-125">Contenuto dell'esercitazione:</span><span class="sxs-lookup"><span data-stu-id="c26e8-125">In this tutorial</span></span>
| <span data-ttu-id="c26e8-126">Entità</span><span class="sxs-lookup"><span data-stu-id="c26e8-126">Entity</span></span> | <span data-ttu-id="c26e8-127">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c26e8-127">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c26e8-128">Servizio collegato Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="c26e8-128">Azure Storage linked service</span></span> |<span data-ttu-id="c26e8-129">Collega l'account di archiviazione di Azure alla data factory.</span><span class="sxs-lookup"><span data-stu-id="c26e8-129">Links your Azure Storage account to the data factory.</span></span> <span data-ttu-id="c26e8-130">In questo esempio l'account di archiviazione di Azure contiene i dati di input e di output per la pipeline.</span><span class="sxs-lookup"><span data-stu-id="c26e8-130">The Azure Storage account holds the input and output data for the pipeline in this sample.</span></span> |
| <span data-ttu-id="c26e8-131">Servizio collegato su richiesta HDInsight</span><span class="sxs-lookup"><span data-stu-id="c26e8-131">HDInsight on-demand linked service</span></span> |<span data-ttu-id="c26e8-132">Collega un cluster HDInsight su richiesta alla data factory.</span><span class="sxs-lookup"><span data-stu-id="c26e8-132">Links an on-demand HDInsight cluster to the data factory.</span></span> <span data-ttu-id="c26e8-133">Il cluster viene creato automaticamente per elaborare i dati e viene eliminato al termine dell'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="c26e8-133">The cluster is automatically created for you to process data and is deleted after the processing is done.</span></span> |
| <span data-ttu-id="c26e8-134">Set di dati di input del BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="c26e8-134">Azure Blob input dataset</span></span> |<span data-ttu-id="c26e8-135">Fa riferimento al servizio collegato di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="c26e8-135">Refers to the Azure Storage linked service.</span></span> <span data-ttu-id="c26e8-136">Il servizio collegato fa riferimento a un account di archiviazione di Azure e il set di dati del BLOB di Azure specifica il contenitore, la cartella e il nome del file nella risorsa di archiviazione che contiene i dati di input.</span><span class="sxs-lookup"><span data-stu-id="c26e8-136">The linked service refers to an Azure Storage account and the Azure Blob dataset specifies the container, folder, and file name in the storage that holds the input data.</span></span> |
| <span data-ttu-id="c26e8-137">Set di dati di output del BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="c26e8-137">Azure Blob output dataset</span></span> |<span data-ttu-id="c26e8-138">Fa riferimento al servizio collegato di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="c26e8-138">Refers to the Azure Storage linked service.</span></span> <span data-ttu-id="c26e8-139">Il servizio collegato fa riferimento a un account di archiviazione di Azure e il set di dati del BLOB di Azure specifica il contenitore, la cartella e il nome del file nella risorsa di archiviazione che contiene i dati di output.</span><span class="sxs-lookup"><span data-stu-id="c26e8-139">The linked service refers to an Azure Storage account and the Azure Blob dataset specifies the container, folder, and file name in the storage that holds the output data.</span></span> |
| <span data-ttu-id="c26e8-140">Data Pipeline</span><span class="sxs-lookup"><span data-stu-id="c26e8-140">Data pipeline</span></span> |<span data-ttu-id="c26e8-141">La pipeline ha un'attività di tipo HDInsightHive che utilizza il set di dati di input e produce il set di dati di output.</span><span class="sxs-lookup"><span data-stu-id="c26e8-141">The pipeline has one activity of type HDInsightHive, which consumes the input dataset and produces the output dataset.</span></span> |

<span data-ttu-id="c26e8-142">Una data factory può comprendere una o più pipeline.</span><span class="sxs-lookup"><span data-stu-id="c26e8-142">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="c26e8-143">Una pipeline può comprendere una o più attività.</span><span class="sxs-lookup"><span data-stu-id="c26e8-143">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="c26e8-144">Esistono due tipi di attività: [attività di spostamento dei dati](data-factory-data-movement-activities.md) e [attività di trasformazione dei dati](data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="c26e8-144">There are two types of activities: [data movement activities](data-factory-data-movement-activities.md) and [data transformation activities](data-factory-data-transformation-activities.md).</span></span> <span data-ttu-id="c26e8-145">In questa esercitazione si crea una pipeline con un'attività (attività Hive).</span><span class="sxs-lookup"><span data-stu-id="c26e8-145">In this tutorial, you create a pipeline with one activity (Hive activity).</span></span>

<span data-ttu-id="c26e8-146">La sezione seguente contiene il modello di Resource Manager completo per la definizione di entità di Data Factory. In questo modo sarà possibile eseguire rapidamente l'esercitazione e testare il modello.</span><span class="sxs-lookup"><span data-stu-id="c26e8-146">The following section provides the complete Resource Manager template for defining Data Factory entities so that you can quickly run through the tutorial and test the template.</span></span> <span data-ttu-id="c26e8-147">Per conoscere come viene definita ogni entità di Data Factory, vedere la sezione [Entità di Data Factory nel modello](#data-factory-entities-in-the-template).</span><span class="sxs-lookup"><span data-stu-id="c26e8-147">To understand how each Data Factory entity is defined, see [Data Factory entities in the template](#data-factory-entities-in-the-template) section.</span></span>

## <a name="data-factory-json-template"></a><span data-ttu-id="c26e8-148">Modello JSON di Data Factory</span><span class="sxs-lookup"><span data-stu-id="c26e8-148">Data Factory JSON template</span></span>
<span data-ttu-id="c26e8-149">Il modello di Resource Manager principale per la definizione di una data factory è il seguente:</span><span class="sxs-lookup"><span data-stu-id="c26e8-149">The top-level Resource Manager template for defining a data factory is:</span></span> 

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
<span data-ttu-id="c26e8-150">Creare un file JSON denominato **ADFTutorialARM.json** nella cartella **C:\ADFGetStarted** con il contenuto seguente:</span><span class="sxs-lookup"><span data-stu-id="c26e8-150">Create a JSON file named **ADFTutorialARM.json** in **C:\ADFGetStarted** folder with the following content:</span></span>

```json
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "parameters": {
        "storageAccountName": { "type": "string", "metadata": { "description": "Name of the Azure storage account that contains the input/output data." } },
          "storageAccountKey": { "type": "securestring", "metadata": { "description": "Key for the Azure storage account." } },
          "blobContainer": { "type": "string", "metadata": { "description": "Name of the blob container in the Azure Storage account." } },
          "inputBlobFolder": { "type": "string", "metadata": { "description": "The folder in the blob container that has the input file." } },
          "inputBlobName": { "type": "string", "metadata": { "description": "Name of the input file/blob." } },
          "outputBlobFolder": { "type": "string", "metadata": { "description": "The folder in the blob container that will hold the transformed data." } },
          "hiveScriptFolder": { "type": "string", "metadata": { "description": "The folder in the blob container that contains the Hive query file." } },
          "hiveScriptFile": { "type": "string", "metadata": { "description": "Name of the hive query (HQL) file." } }
    },
    "variables": {
          "dataFactoryName": "[concat('HiveTransformDF', uniqueString(resourceGroup().id))]",
          "azureStorageLinkedServiceName": "AzureStorageLinkedService",
          "hdInsightOnDemandLinkedServiceName": "HDInsightOnDemandLinkedService",
          "blobInputDatasetName": "AzureBlobInput",
          "blobOutputDatasetName": "AzureBlobOutput",
          "pipelineName": "HiveTransformPipeline"
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
            "name": "[variables('hdInsightOnDemandLinkedServiceName')]",
            "dependsOn": [
                  "[variables('dataFactoryName')]",
                  "[variables('azureStorageLinkedServiceName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
                  "type": "HDInsightOnDemand",
                  "typeProperties": {
                    "version": "3.5",
                    "clusterSize": 1,
                    "timeToLive": "00:05:00",
                    "osType": "Linux",
                    "linkedServiceName": "[variables('azureStorageLinkedServiceName')]"
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
                  "typeProperties": {
                    "fileName": "[parameters('inputBlobName')]",
                    "folderPath": "[concat(parameters('blobContainer'), '/', parameters('inputBlobFolder'))]",
                    "format": {
                          "type": "TextFormat",
                          "columnDelimiter": ","
                    }
                  },
                  "availability": {
                    "frequency": "Month",
                    "interval": 1
                  },
                  "external": true
            }
          },
          {
            "type": "datasets",
            "name": "[variables('blobOutputDatasetName')]",
            "dependsOn": [
                  "[variables('dataFactoryName')]",
                  "[variables('azureStorageLinkedServiceName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
                  "type": "AzureBlob",
                  "linkedServiceName": "[variables('azureStorageLinkedServiceName')]",
                  "typeProperties": {
                    "folderPath": "[concat(parameters('blobContainer'), '/', parameters('outputBlobFolder'))]",
                    "format": {
                          "type": "TextFormat",
                          "columnDelimiter": ","
                    }
                  },
                  "availability": {
                    "frequency": "Month",
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
                  "[variables('hdInsightOnDemandLinkedServiceName')]",
                  "[variables('blobInputDatasetName')]",
                  "[variables('blobOutputDatasetName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
                  "description": "Pipeline that transforms data using Hive script.",
                  "activities": [
                {
                      "type": "HDInsightHive",
                      "typeProperties": {
                        "scriptPath": "[concat(parameters('blobContainer'), '/', parameters('hiveScriptFolder'), '/', parameters('hiveScriptFile'))]",
                        "scriptLinkedService": "[variables('azureStorageLinkedServiceName')]",
                        "defines": {
                              "inputtable": "[concat('wasb://', parameters('blobContainer'), '@', parameters('storageAccountName'), '.blob.core.windows.net/', parameters('inputBlobFolder'))]",
                              "partitionedtable": "[concat('wasb://', parameters('blobContainer'), '@', parameters('storageAccountName'), '.blob.core.windows.net/', parameters('outputBlobFolder'))]"
                        }
                      },
                      "inputs": [
                        {
                              "name": "[variables('blobInputDatasetName')]"
                        }
                      ],
                      "outputs": [
                        {
                              "name": "[variables('blobOutputDatasetName')]"
                        }
                      ],
                      "policy": {
                        "concurrency": 1,
                        "retry": 3
                      },
                      "scheduler": {
                        "frequency": "Month",
                        "interval": 1
                      },
                      "name": "RunSampleHiveActivity",
                      "linkedServiceName": "[variables('hdInsightOnDemandLinkedServiceName')]"
                }
                  ],
                  "start": "2017-07-01T00:00:00Z",
                  "end": "2017-07-02T00:00:00Z",
                  "isPaused": false
              }
          }
        ]
      }
    ]
}
```

> [!NOTE]
> <span data-ttu-id="c26e8-151">È possibile trovare un altro esempio del modello di Resource Manager per la creazione di una data factory di Azure in [Tutorial: Create a pipeline with Copy Activity using an Azure Resource Manager template](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md) (Esercitazione: Creare una pipeline con l'attività di copia usando un modello di Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="c26e8-151">You can find another example of Resource Manager template for creating an Azure data factory on [Tutorial: Create a pipeline with Copy Activity using an Azure Resource Manager template](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md).</span></span>  
> 
> 

## <a name="parameters-json"></a><span data-ttu-id="c26e8-152">Parametri JSON</span><span class="sxs-lookup"><span data-stu-id="c26e8-152">Parameters JSON</span></span>
<span data-ttu-id="c26e8-153">Creare un file JSON denominato **ADFTutorialARM-Parameters.json** contenente i parametri per il modello di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c26e8-153">Create a JSON file named **ADFTutorialARM-Parameters.json** that contains parameters for the Azure Resource Manager template.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="c26e8-154">Specificare il nome e la chiave dell'account di archiviazione di Azure per i parametri **storageAccountName** e **storageAccountKey** in questo file dei parametri.</span><span class="sxs-lookup"><span data-stu-id="c26e8-154">Specify the name and key of your Azure Storage account for the **storageAccountName** and **storageAccountKey** parameters in this parameter file.</span></span> 
> 
> 

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountName": {
            "value": "<Name of your Azure Storage account>"
        },
        "storageAccountKey": {
            "value": "<Key of your Azure Storage account>"
        },
        "blobContainer": {
            "value": "adfgetstarted"
        },
        "inputBlobFolder": {
            "value": "inputdata"
        },
        "inputBlobName": {
            "value": "input.log"
        },
        "outputBlobFolder": {
            "value": "partitioneddata"
        },
        "hiveScriptFolder": {
              "value": "script"
        },
        "hiveScriptFile": {
              "value": "partitionweblogs.hql"
        }
    }
}
```

> [!IMPORTANT]
> <span data-ttu-id="c26e8-155">Si possono avere file JSON di parametri separati per gli ambienti di sviluppo, test e produzione che è possibile usare con lo stesso modello JSON di Data Factory.</span><span class="sxs-lookup"><span data-stu-id="c26e8-155">You may have separate parameter JSON files for development, testing, and production environments that you can use with the same Data Factory JSON template.</span></span> <span data-ttu-id="c26e8-156">Usando uno script di Power Shell, è possibile automatizzare la distribuzione delle entità di Data Factory in questi ambienti.</span><span class="sxs-lookup"><span data-stu-id="c26e8-156">By using a Power Shell script, you can automate deploying Data Factory entities in these environments.</span></span> 
> 
> 

## <a name="create-data-factory"></a><span data-ttu-id="c26e8-157">Creare un'istanza di Data Factory</span><span class="sxs-lookup"><span data-stu-id="c26e8-157">Create data factory</span></span>
1. <span data-ttu-id="c26e8-158">Avviare **Azure PowerShell** ed eseguire questo comando:</span><span class="sxs-lookup"><span data-stu-id="c26e8-158">Start **Azure PowerShell** and run the following command:</span></span> 
   * <span data-ttu-id="c26e8-159">Eseguire il comando seguente e immettere il nome utente e la password usati per accedere al portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="c26e8-159">Run the following command and enter the user name and password that you use to sign in to the Azure portal.</span></span>
    ```PowerShell
    Login-AzureRmAccount
    ```  
   * <span data-ttu-id="c26e8-160">Eseguire il comando seguente per visualizzare tutte le sottoscrizioni per l'account.</span><span class="sxs-lookup"><span data-stu-id="c26e8-160">Run the following command to view all the subscriptions for this account.</span></span>
    ```PowerShell
    Get-AzureRmSubscription
    ``` 
   * <span data-ttu-id="c26e8-161">Eseguire il comando seguente per selezionare la sottoscrizione da usare.</span><span class="sxs-lookup"><span data-stu-id="c26e8-161">Run the following command to select the subscription that you want to work with.</span></span> <span data-ttu-id="c26e8-162">La sottoscrizione deve corrispondere a quella usata nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="c26e8-162">This subscription should be the same as the one you used in the Azure portal.</span></span>
    ```
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```   
2. <span data-ttu-id="c26e8-163">Eseguire il comando seguente per distribuire entità di Data Factory usando il modello di Resource Manager creato nel Passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="c26e8-163">Run the following command to deploy Data Factory entities using the Resource Manager template you created in Step 1.</span></span> 

    ```PowerShell
    New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile C:\ADFGetStarted\ADFTutorialARM.json -TemplateParameterFile C:\ADFGetStarted\ADFTutorialARM-Parameters.json
    ```

## <a name="monitor-pipeline"></a><span data-ttu-id="c26e8-164">Monitorare la pipeline</span><span class="sxs-lookup"><span data-stu-id="c26e8-164">Monitor pipeline</span></span>
1. <span data-ttu-id="c26e8-165">Dopo l'accesso al [portale di Azure](https://portal.azure.com/) fare clic su **Esplora** e selezionare **Data factory**.</span><span class="sxs-lookup"><span data-stu-id="c26e8-165">After logging in to the [Azure portal](https://portal.azure.com/), Click **Browse** and select **Data factories**.</span></span>
     <span data-ttu-id="c26e8-166">![Esplorare->Data factory](./media/data-factory-build-your-first-pipeline-using-arm/BrowseDataFactories.png)</span><span class="sxs-lookup"><span data-stu-id="c26e8-166">![Browse->Data factories](./media/data-factory-build-your-first-pipeline-using-arm/BrowseDataFactories.png)</span></span>
2. <span data-ttu-id="c26e8-167">Nel pannello **Data factory** fare clic sulla data factory **TutorialFactoryARM** creata.</span><span class="sxs-lookup"><span data-stu-id="c26e8-167">In the **Data Factories** blade, click the data factory (**TutorialFactoryARM**) you created.</span></span>    
3. <span data-ttu-id="c26e8-168">Nel pannello **Data factory** relativo alla data factory scelta fare clic su **Diagramma**.</span><span class="sxs-lookup"><span data-stu-id="c26e8-168">In the **Data Factory** blade for your data factory, click **Diagram**.</span></span>

     ![Riquadro Diagramma](./media/data-factory-build-your-first-pipeline-using-arm/DiagramTile.png)
4. <span data-ttu-id="c26e8-170">In **Vista diagramma**saranno visualizzati una panoramica delle pipeline e i set di dati usati in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="c26e8-170">In the **Diagram View**, you see an overview of the pipelines, and datasets used in this tutorial.</span></span>
   
   ![Vista diagramma](./media/data-factory-build-your-first-pipeline-using-arm/DiagramView.png) 
5. <span data-ttu-id="c26e8-172">In Vista diagramma fare doppio clic sul set di dati **AzureBlobOutput**.</span><span class="sxs-lookup"><span data-stu-id="c26e8-172">In the Diagram View, double-click the dataset **AzureBlobOutput**.</span></span> <span data-ttu-id="c26e8-173">Viene visualizzata la sezione in fase di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="c26e8-173">You see that the slice that is currently being processed.</span></span>
   
    ![Set di dati](./media/data-factory-build-your-first-pipeline-using-arm/AzureBlobOutput.png)
6. <span data-ttu-id="c26e8-175">Al termine dell'elaborazione lo stato della sezione è **Pronta** .</span><span class="sxs-lookup"><span data-stu-id="c26e8-175">When processing is done, you see the slice in **Ready** state.</span></span> <span data-ttu-id="c26e8-176">La creazione di un cluster HDInsight su richiesta di solito richiede tempo (circa 20 minuti).</span><span class="sxs-lookup"><span data-stu-id="c26e8-176">Creation of an on-demand HDInsight cluster usually takes sometime (approximately 20 minutes).</span></span> <span data-ttu-id="c26e8-177">Di conseguenza, prevedere **circa 30 minuti** per l'elaborazione della sezione nella pipeline.</span><span class="sxs-lookup"><span data-stu-id="c26e8-177">Therefore, expect the pipeline to take **approximately 30 minutes** to process the slice.</span></span>
   
    ![Set di dati](./media/data-factory-build-your-first-pipeline-using-arm/SliceReady.png)    
7. <span data-ttu-id="c26e8-179">Quando lo stato della sezione è **Pronto**, cercare i dati di output nella cartella **partitioneddata** del contenitore **adfgetstarted** nell'archivio BLOB.</span><span class="sxs-lookup"><span data-stu-id="c26e8-179">When the slice is in **Ready** state, check the **partitioneddata** folder in the **adfgetstarted** container in your blob storage for the output data.</span></span>  

<span data-ttu-id="c26e8-180">Per istruzioni su come usare i pannelli del portale di Azure per monitorare la pipeline e i set di dati creati in questa esercitazione, vedere [Monitorare e gestire le pipeline di Azure Data Factory](data-factory-monitor-manage-pipelines.md) .</span><span class="sxs-lookup"><span data-stu-id="c26e8-180">See [Monitor datasets and pipeline](data-factory-monitor-manage-pipelines.md) for instructions on how to use the Azure portal blades to monitor the pipeline and datasets you have created in this tutorial.</span></span>

<span data-ttu-id="c26e8-181">È anche possibile usare l'app di monitoraggio e gestione per monitorare le pipeline di dati.</span><span class="sxs-lookup"><span data-stu-id="c26e8-181">You can also use Monitor and Manage App to monitor your data pipelines.</span></span> <span data-ttu-id="c26e8-182">Per i dettagli sull'uso dell'applicazione, vedere [Monitorare e gestire le pipeline di Azure Data Factory con la nuova app di monitoraggio e gestione](data-factory-monitor-manage-app.md) .</span><span class="sxs-lookup"><span data-stu-id="c26e8-182">See [Monitor and manage Azure Data Factory pipelines using Monitoring App](data-factory-monitor-manage-app.md) for details about using the application.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="c26e8-183">Il file di input viene eliminato quando la sezione viene elaborata correttamente.</span><span class="sxs-lookup"><span data-stu-id="c26e8-183">The input file gets deleted when the slice is processed successfully.</span></span> <span data-ttu-id="c26e8-184">Per eseguire di nuovo la sezione o ripetere l'esercitazione, caricare quindi il file di input (input.log) nella cartella inputdata del contenitore adfgetstarted.</span><span class="sxs-lookup"><span data-stu-id="c26e8-184">Therefore, if you want to rerun the slice or do the tutorial again, upload the input file (input.log) to the inputdata folder of the adfgetstarted container.</span></span>
> 
> 

## <a name="data-factory-entities-in-the-template"></a><span data-ttu-id="c26e8-185">Entità di Data Factory nel modello</span><span class="sxs-lookup"><span data-stu-id="c26e8-185">Data Factory entities in the template</span></span>
### <a name="define-data-factory"></a><span data-ttu-id="c26e8-186">Definire una data factory</span><span class="sxs-lookup"><span data-stu-id="c26e8-186">Define data factory</span></span>
<span data-ttu-id="c26e8-187">È possibile definire una data factory nel modello di Resource Manager come illustrato nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="c26e8-187">You define a data factory in the Resource Manager template as shown in the following sample:</span></span>  

```json
"resources": [
{
    "name": "[variables('dataFactoryName')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "West US"
}
```
<span data-ttu-id="c26e8-188">Il valore dataFactoryName viene definito come segue:</span><span class="sxs-lookup"><span data-stu-id="c26e8-188">The dataFactoryName is defined as:</span></span> 

```json
"dataFactoryName": "[concat('HiveTransformDF', uniqueString(resourceGroup().id))]",
```
<span data-ttu-id="c26e8-189">È una stringa univoca basata sull'ID del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="c26e8-189">It is a unique string based on the resource group ID.</span></span>  

### <a name="defining-data-factory-entities"></a><span data-ttu-id="c26e8-190">Definizione di entità di Data factory</span><span class="sxs-lookup"><span data-stu-id="c26e8-190">Defining Data Factory entities</span></span>
<span data-ttu-id="c26e8-191">Le entità di Data Factory seguenti vengono definite nel modello JSON:</span><span class="sxs-lookup"><span data-stu-id="c26e8-191">The following Data Factory entities are defined in the JSON template:</span></span> 

* [<span data-ttu-id="c26e8-192">Servizio collegato Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="c26e8-192">Azure Storage linked service</span></span>](#azure-storage-linked-service)
* [<span data-ttu-id="c26e8-193">Servizio collegato su richiesta HDInsight</span><span class="sxs-lookup"><span data-stu-id="c26e8-193">HDInsight on-demand linked service</span></span>](#hdinsight-on-demand-linked-service)
* [<span data-ttu-id="c26e8-194">Set di dati di input del BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="c26e8-194">Azure blob input dataset</span></span>](#azure-blob-input-dataset)
* [<span data-ttu-id="c26e8-195">Set di dati di output del BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="c26e8-195">Azure blob output dataset</span></span>](#azure-blob-output-dataset)
* [<span data-ttu-id="c26e8-196">Pipeline di dati con un'attività di copia</span><span class="sxs-lookup"><span data-stu-id="c26e8-196">Data pipeline with a copy activity</span></span>](#data-pipeline)

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="c26e8-197">Servizio collegato Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="c26e8-197">Azure Storage linked service</span></span>
<span data-ttu-id="c26e8-198">In questa sezione si specificano il nome e la chiave dell'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="c26e8-198">You specify the name and key of your Azure storage account in this section.</span></span> <span data-ttu-id="c26e8-199">Per informazioni dettagliate sulle proprietà JSON usate per definire un servizio collegato di Archiviazione di Azure, vedere [Servizio collegato Archiviazione di Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service).</span><span class="sxs-lookup"><span data-stu-id="c26e8-199">See [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used to define an Azure Storage linked service.</span></span> 

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
<span data-ttu-id="c26e8-200">**connectionString** usa i parametri storageAccountName e storageAccountKey.</span><span class="sxs-lookup"><span data-stu-id="c26e8-200">The **connectionString** uses the storageAccountName and storageAccountKey parameters.</span></span> <span data-ttu-id="c26e8-201">I valori per questi parametri sono stati passati usando un file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="c26e8-201">The values for these parameters passed by using a configuration file.</span></span> <span data-ttu-id="c26e8-202">La definizione usa anche le variabili azureStroageLinkedService e dataFactoryName definite nel modello.</span><span class="sxs-lookup"><span data-stu-id="c26e8-202">The definition also uses variables: azureStroageLinkedService and dataFactoryName defined in the template.</span></span> 

#### <a name="hdinsight-on-demand-linked-service"></a><span data-ttu-id="c26e8-203">Servizio collegato su richiesta HDInsight</span><span class="sxs-lookup"><span data-stu-id="c26e8-203">HDInsight on-demand linked service</span></span>
<span data-ttu-id="c26e8-204">Per informazioni dettagliate sulle proprietà JSON usate per definire un servizio collegato su richiesta HDInsight, vedere [Servizi collegati di calcolo](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="c26e8-204">See [Compute linked services](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) article for details about JSON properties used to define an HDInsight on-demand linked service.</span></span>  

```json
{
    "type": "linkedservices",
    "name": "[variables('hdInsightOnDemandLinkedServiceName')]",
    "dependsOn": [
        "[variables('dataFactoryName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
        "type": "HDInsightOnDemand",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "linkedServiceName": "[variables('azureStorageLinkedServiceName')]"
        }
    }
}
```
<span data-ttu-id="c26e8-205">Tenere presente quanto segue:</span><span class="sxs-lookup"><span data-stu-id="c26e8-205">Note the following points:</span></span> 

* <span data-ttu-id="c26e8-206">Data Factory crea automaticamente un cluster HDInsight **basato su Linux** con il codice JSON precedente.</span><span class="sxs-lookup"><span data-stu-id="c26e8-206">The Data Factory creates a **Linux-based** HDInsight cluster for you with the above JSON.</span></span> <span data-ttu-id="c26e8-207">Per i dettagli, vedere [Servizio collegato Azure HDInsight su richiesta](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) .</span><span class="sxs-lookup"><span data-stu-id="c26e8-207">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span> 
* <span data-ttu-id="c26e8-208">È possibile usare il **proprio cluster HDInsight** anziché un cluster HDInsight su richiesta.</span><span class="sxs-lookup"><span data-stu-id="c26e8-208">You could use **your own HDInsight cluster** instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="c26e8-209">Per i dettagli, vedere [Servizio collegato Azure HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) .</span><span class="sxs-lookup"><span data-stu-id="c26e8-209">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details.</span></span>
* <span data-ttu-id="c26e8-210">Il cluster HDInsight crea un **contenitore predefinito** nell'archivio BLOB specificato nel file JSON (**linkedServiceName**).</span><span class="sxs-lookup"><span data-stu-id="c26e8-210">The HDInsight cluster creates a **default container** in the blob storage you specified in the JSON (**linkedServiceName**).</span></span> <span data-ttu-id="c26e8-211">HDInsight non elimina il contenitore quando viene eliminato il cluster.</span><span class="sxs-lookup"><span data-stu-id="c26e8-211">HDInsight does not delete this container when the cluster is deleted.</span></span> <span data-ttu-id="c26e8-212">Questo comportamento dipende dalla progettazione.</span><span class="sxs-lookup"><span data-stu-id="c26e8-212">This behavior is by design.</span></span> <span data-ttu-id="c26e8-213">Con il servizio collegato HDInsight su richiesta, viene creato un cluster HDInsight ogni volta che è necessario elaborare una sezione, a meno che non esista un cluster attivo (**timeToLive**) che viene eliminato al termine dell'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="c26e8-213">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice needs to be processed unless there is an existing live cluster (**timeToLive**) and is deleted when the processing is done.</span></span>
  
    <span data-ttu-id="c26e8-214">Man mano che vengono elaborate più sezioni, vengono visualizzati numerosi contenitori nell'archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="c26e8-214">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="c26e8-215">Se non sono necessari per risolvere i problemi relativi ai processi, è possibile eliminarli per ridurre i costi di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="c26e8-215">If you do not need them for troubleshooting of the jobs, you may want to delete them to reduce the storage cost.</span></span> <span data-ttu-id="c26e8-216">I nomi dei contenitori seguono questo schema: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span><span class="sxs-lookup"><span data-stu-id="c26e8-216">The names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="c26e8-217">Per eliminare i contenitori nell'archivio BLOB di Azure, usare strumenti come [Microsoft Azure Storage Explorer](http://storageexplorer.com/) .</span><span class="sxs-lookup"><span data-stu-id="c26e8-217">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) to delete containers in your Azure blob storage.</span></span>

<span data-ttu-id="c26e8-218">Per i dettagli, vedere [Servizio collegato Azure HDInsight su richiesta](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) .</span><span class="sxs-lookup"><span data-stu-id="c26e8-218">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>

#### <a name="azure-blob-input-dataset"></a><span data-ttu-id="c26e8-219">Set di dati di input del BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="c26e8-219">Azure blob input dataset</span></span>
<span data-ttu-id="c26e8-220">Vengono specificati i nomi del contenitore BLOB, della cartella e del file contenente i dati di input.</span><span class="sxs-lookup"><span data-stu-id="c26e8-220">You specify the names of blob container, folder, and file that contains the input data.</span></span> <span data-ttu-id="c26e8-221">Per informazioni dettagliate sulle proprietà JSON usate per definire un set di dati del BLOB di Azure, vedere [Proprietà del set di dati del BLOB di Azure](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="c26e8-221">See [Azure Blob dataset properties](data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used to define an Azure Blob dataset.</span></span> 

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
        "typeProperties": {
            "fileName": "[parameters('inputBlobName')]",
            "folderPath": "[concat(parameters('blobContainer'), '/', parameters('inputBlobFolder'))]",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1
        },
        "external": true
    }
}
```
<span data-ttu-id="c26e8-222">Questa definizione usa i parametri seguenti definiti nel modello di parametro: blobContainer, inputBlobFolder e inputBlobName.</span><span class="sxs-lookup"><span data-stu-id="c26e8-222">This definition uses the following parameters defined in parameter template: blobContainer, inputBlobFolder, and inputBlobName.</span></span> 

#### <a name="azure-blob-output-dataset"></a><span data-ttu-id="c26e8-223">Set di dati di output del BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="c26e8-223">Azure Blob output dataset</span></span>
<span data-ttu-id="c26e8-224">Vengono specificati i nomi del contenitore BLOB e della cartella che contiene i dati di output.</span><span class="sxs-lookup"><span data-stu-id="c26e8-224">You specify the names of blob container and folder that holds the output data.</span></span> <span data-ttu-id="c26e8-225">Per informazioni dettagliate sulle proprietà JSON usate per definire un set di dati del BLOB di Azure, vedere [Proprietà del set di dati del BLOB di Azure](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="c26e8-225">See [Azure Blob dataset properties](data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used to define an Azure Blob dataset.</span></span>  

```json
{
    "type": "datasets",
    "name": "[variables('blobOutputDatasetName')]",
    "dependsOn": [
        "[variables('dataFactoryName')]",
        "[variables('azureStorageLinkedServiceName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "[variables('azureStorageLinkedServiceName')]",
        "typeProperties": {
            "folderPath": "[concat(parameters('blobContainer'), '/', parameters('outputBlobFolder'))]",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="c26e8-226">Questa definizione usa i parametri seguenti definiti nel modello di parametro: blobContainer e outputBlobFolder.</span><span class="sxs-lookup"><span data-stu-id="c26e8-226">This definition uses the following parameters defined in the parameter template: blobContainer and outputBlobFolder.</span></span> 

#### <a name="data-pipeline"></a><span data-ttu-id="c26e8-227">Data Pipeline</span><span class="sxs-lookup"><span data-stu-id="c26e8-227">Data pipeline</span></span>
<span data-ttu-id="c26e8-228">Viene definita una pipeline che trasforma i dati eseguendo lo script Hive in un cluster HDInsight di Azure su richiesta.</span><span class="sxs-lookup"><span data-stu-id="c26e8-228">You define a pipeline that transform data by running Hive script on an on-demand Azure HDInsight cluster.</span></span> <span data-ttu-id="c26e8-229">Per le descrizioni degli elementi JSON usati per definire una pipeline in questo esempio, vedere [Pipeline JSON](data-factory-create-pipelines.md#pipeline-json).</span><span class="sxs-lookup"><span data-stu-id="c26e8-229">See [Pipeline JSON](data-factory-create-pipelines.md#pipeline-json) for descriptions of JSON elements used to define a pipeline in this example.</span></span> 

```json
{
    "type": "datapipelines",
    "name": "[variables('pipelineName')]",
    "dependsOn": [
        "[variables('dataFactoryName')]",
        "[variables('azureStorageLinkedServiceName')]",
        "[variables('hdInsightOnDemandLinkedServiceName')]",
        "[variables('blobInputDatasetName')]",
        "[variables('blobOutputDatasetName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
        "description": "Pipeline that transforms data using Hive script.",
        "activities": [
        {
            "type": "HDInsightHive",
            "typeProperties": {
                "scriptPath": "[concat(parameters('blobContainer'), '/', parameters('hiveScriptFolder'), '/', parameters('hiveScriptFile'))]",
                "scriptLinkedService": "[variables('azureStorageLinkedServiceName')]",
                "defines": {
                    "inputtable": "[concat('wasb://', parameters('blobContainer'), '@', parameters('storageAccountName'), '.blob.core.windows.net/', parameters('inputBlobFolder'))]",
                    "partitionedtable": "[concat('wasb://', parameters('blobContainer'), '@', parameters('storageAccountName'), '.blob.core.windows.net/', parameters('outputBlobFolder'))]"
                }
            },
            "inputs": [
            {
                "name": "[variables('blobInputDatasetName')]"
            }
            ],
            "outputs": [
            {
                "name": "[variables('blobOutputDatasetName')]"
            }
            ],
            "policy": {
                "concurrency": 1,
                "retry": 3
            },
            "scheduler": {
                "frequency": "Month",
                "interval": 1
            },
            "name": "RunSampleHiveActivity",
            "linkedServiceName": "[variables('hdInsightOnDemandLinkedServiceName')]"
        }
        ],
        "start": "2017-07-01T00:00:00Z",
        "end": "2017-07-02T00:00:00Z",
        "isPaused": false
    }
}
```

## <a name="reuse-the-template"></a><span data-ttu-id="c26e8-230">Riutilizzare il modello</span><span class="sxs-lookup"><span data-stu-id="c26e8-230">Reuse the template</span></span>
<span data-ttu-id="c26e8-231">Nell'esercitazione sono stati creati un modello per definire le entità di Data Factory e un modello per passare i valori dei parametri.</span><span class="sxs-lookup"><span data-stu-id="c26e8-231">In the tutorial, you created a template for defining Data Factory entities and a template for passing values for parameters.</span></span> <span data-ttu-id="c26e8-232">Per usare lo stesso modello per distribuire le entità di Data Factory in ambienti diversi, si crea un file dei parametri per ogni ambiente e lo si usa durante la distribuzione in tale ambiente.</span><span class="sxs-lookup"><span data-stu-id="c26e8-232">To use the same template to deploy Data Factory entities to different environments, you create a parameter file for each environment and use it when deploying to that environment.</span></span>     

<span data-ttu-id="c26e8-233">Esempio:</span><span class="sxs-lookup"><span data-stu-id="c26e8-233">Example:</span></span>  

```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Dev.json

New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Test.json

New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Production.json
```
<span data-ttu-id="c26e8-234">Si noti che il primo comando usa il file dei parametri per l'ambiente di sviluppo, il secondo per l'ambiente di test e il terzo per l'ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="c26e8-234">Notice that the first command uses parameter file for the development environment, second one for the test environment, and the third one for the production environment.</span></span>  

<span data-ttu-id="c26e8-235">È anche possibile riutilizzare il modello per eseguire attività ripetute.</span><span class="sxs-lookup"><span data-stu-id="c26e8-235">You can also reuse the template to perform repeated tasks.</span></span> <span data-ttu-id="c26e8-236">Ad esempio, è necessario creare più data factory con una o più pipeline che implementano la stessa logica, ma ogni data factory usa account di archiviazione di Azure e di database SQL di Azure diversi.</span><span class="sxs-lookup"><span data-stu-id="c26e8-236">For example, you need to create many data factories with one or more pipelines that implement the same logic but each data factory uses different Azure storage and Azure SQL Database accounts.</span></span> <span data-ttu-id="c26e8-237">In questo scenario si usa lo stesso modello nello stesso ambiente (sviluppo, test o produzione) con file dei parametri diversi per creare le data factory.</span><span class="sxs-lookup"><span data-stu-id="c26e8-237">In this scenario, you use the same template in the same environment (dev, test, or production) with different parameter files to create data factories.</span></span> 

## <a name="resource-manager-template-for-creating-a-gateway"></a><span data-ttu-id="c26e8-238">Modello di Resource Manager per la creazione di un gateway</span><span class="sxs-lookup"><span data-stu-id="c26e8-238">Resource Manager template for creating a gateway</span></span>
<span data-ttu-id="c26e8-239">Di seguito è disponibile un modello di Resource Manager per la creazione di un gateway logico nel back-end.</span><span class="sxs-lookup"><span data-stu-id="c26e8-239">Here is a sample Resource Manager template for creating a logical gateway in the back.</span></span> <span data-ttu-id="c26e8-240">Installare un gateway nel computer locale o nella VM IaaS di Azure e registrare il gateway con il servizio Data Factory usando una chiave.</span><span class="sxs-lookup"><span data-stu-id="c26e8-240">Install a gateway on your on-premises computer or Azure IaaS VM and register the gateway with Data Factory service using a key.</span></span> <span data-ttu-id="c26e8-241">Per altre informazioni vedere [Spostare dati tra origini locali e il cloud con Gateway di gestione dati](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="c26e8-241">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) for details.</span></span>

```json
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "parameters": {
    },
    "variables": {
        "dataFactoryName":  "GatewayUsingArmDF",
        "apiVersion": "2015-10-01",
        "singleQuote": "'"
    },
    "resources": [
        {
            "name": "[variables('dataFactoryName')]",
            "apiVersion": "[variables('apiVersion')]",
            "type": "Microsoft.DataFactory/datafactories",
            "location": "eastus",
            "resources": [
                {
                    "dependsOn": [ "[concat('Microsoft.DataFactory/dataFactories/', variables('dataFactoryName'))]" ],
                    "type": "gateways",
                    "apiVersion": "[variables('apiVersion')]",
                    "name": "GatewayUsingARM",
                    "properties": {
                        "description": "my gateway"
                    }
                }            
            ]
        }
    ]
}
```
<span data-ttu-id="c26e8-242">Questo modello crea una data factory denominata GatewayUsingArmDF con un gateway denominato GatewayUsingARM.</span><span class="sxs-lookup"><span data-stu-id="c26e8-242">This template creates a data factory named GatewayUsingArmDF with a gateway named: GatewayUsingARM.</span></span> 

## <a name="see-also"></a><span data-ttu-id="c26e8-243">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c26e8-243">See Also</span></span>
| <span data-ttu-id="c26e8-244">Argomento</span><span class="sxs-lookup"><span data-stu-id="c26e8-244">Topic</span></span> | <span data-ttu-id="c26e8-245">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c26e8-245">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="c26e8-246">Pipeline</span><span class="sxs-lookup"><span data-stu-id="c26e8-246">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="c26e8-247">Questo articolo fornisce informazioni sulle pipeline e sulle attività in Azure Data Factory e su come usarle per costruire flussi di lavoro end-to-end basati sui dati per lo scenario o l'azienda.</span><span class="sxs-lookup"><span data-stu-id="c26e8-247">This article helps you understand pipelines and activities in Azure Data Factory and how to use them to construct end-to-end data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="c26e8-248">Set di dati</span><span class="sxs-lookup"><span data-stu-id="c26e8-248">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="c26e8-249">Questo articolo fornisce informazioni sui set di dati in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="c26e8-249">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="c26e8-250">Pianificazione ed esecuzione</span><span class="sxs-lookup"><span data-stu-id="c26e8-250">Scheduling and execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="c26e8-251">Questo articolo descrive gli aspetti di pianificazione ed esecuzione del modello applicativo di Data factory di Azure.</span><span class="sxs-lookup"><span data-stu-id="c26e8-251">This article explains the scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="c26e8-252">Monitorare e gestire le pipeline con l'app di monitoraggio</span><span class="sxs-lookup"><span data-stu-id="c26e8-252">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="c26e8-253">Questo articolo descrive come monitorare, gestire ed eseguire il debug delle pipeline usando l'app di monitoraggio e gestione.</span><span class="sxs-lookup"><span data-stu-id="c26e8-253">This article describes how to monitor, manage, and debug pipelines using the Monitoring & Management App.</span></span> |

