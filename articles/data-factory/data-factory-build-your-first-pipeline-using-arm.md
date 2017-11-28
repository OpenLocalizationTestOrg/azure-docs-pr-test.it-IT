---
title: aaaBuild la prima data factory (modello di gestione delle risorse) | Documenti Microsoft
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
ms.openlocfilehash: fa08cd1ac3a0e5c5bf4bd4c6bd9dfa6dba9f4319
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-resource-manager-template"></a><span data-ttu-id="ae9d6-103">Esercitazione: Creare la prima data factory di Azure usando il modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ae9d6-103">Tutorial: Build your first Azure data factory using Azure Resource Manager template</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ae9d6-104">Panoramica e prerequisiti</span><span class="sxs-lookup"><span data-stu-id="ae9d6-104">Overview and prerequisites</span></span>](data-factory-build-your-first-pipeline.md)
> * [<span data-ttu-id="ae9d6-105">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="ae9d6-105">Azure portal</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
> * [<span data-ttu-id="ae9d6-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ae9d6-106">Visual Studio</span></span>](data-factory-build-your-first-pipeline-using-vs.md)
> * [<span data-ttu-id="ae9d6-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ae9d6-107">PowerShell</span></span>](data-factory-build-your-first-pipeline-using-powershell.md)
> * [<span data-ttu-id="ae9d6-108">Modello di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ae9d6-108">Resource Manager Template</span></span>](data-factory-build-your-first-pipeline-using-arm.md)
> * [<span data-ttu-id="ae9d6-109">API REST</span><span class="sxs-lookup"><span data-stu-id="ae9d6-109">REST API</span></span>](data-factory-build-your-first-pipeline-using-rest-api.md)
> 
> 

<span data-ttu-id="ae9d6-110">In questo articolo, si utilizza un toocreate modello di gestione risorse di Azure prima data factory di Azure.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-110">In this article, you use an Azure Resource Manager template toocreate your first Azure data factory.</span></span> <span data-ttu-id="ae9d6-111">esercitazione di hello toodo tramite altri strumenti/SDK, selezionare una delle opzioni di hello dall'elenco a discesa hello.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-111">toodo hello tutorial using other tools/SDKs, select one of hello options from hello drop-down list.</span></span>

<span data-ttu-id="ae9d6-112">pipeline Hello in questa esercitazione è un'attività: **attività Hive di HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-112">hello pipeline in this tutorial has one activity: **HDInsight Hive activity**.</span></span> <span data-ttu-id="ae9d6-113">Questa attività esegue uno script hive in un cluster HDInsight di Azure che trasformazioni i dati di output tooproduce di dati di input.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-113">This activity runs a hive script on an Azure HDInsight cluster that transforms input data tooproduce output data.</span></span> <span data-ttu-id="ae9d6-114">pipeline di Hello è toorun pianificato dopo un mese tra hello specificato di ore di inizio e fine.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-114">hello pipeline is scheduled toorun once a month between hello specified start and end times.</span></span> 

> [!NOTE]
> <span data-ttu-id="ae9d6-115">pipeline di dati Hello in questa esercitazione Trasforma i dati di output tooproduce di dati di input.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-115">hello data pipeline in this tutorial transforms input data tooproduce output data.</span></span> <span data-ttu-id="ae9d6-116">Per un'esercitazione su come dati di toocopy tramite Data Factory di Azure, vedere [esercitazione: copiare i dati da archiviazione Blob tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="ae9d6-116">For a tutorial on how toocopy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
> 
> <span data-ttu-id="ae9d6-117">pipeline di Hello in questa esercitazione contiene una sola attività di tipo: HDInsightHive.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-117">hello pipeline in this tutorial has only one activity of type: HDInsightHive.</span></span> <span data-ttu-id="ae9d6-118">Una pipeline può includere più attività</span><span class="sxs-lookup"><span data-stu-id="ae9d6-118">A pipeline can have more than one activity.</span></span> <span data-ttu-id="ae9d6-119">Inoltre, è possibile concatenare le due attività (eseguire un'attività dopo l'altro) mediante l'impostazione di set di dati di hello output di un'attività come hello input set di dati di hello altre attività.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-119">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="ae9d6-120">Per altre informazioni, vedere [Pianificazione ed esecuzione in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="ae9d6-120">For more information, see [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="ae9d6-121">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="ae9d6-121">Prerequisites</span></span>
* <span data-ttu-id="ae9d6-122">Leggere [esercitazione Panoramica](data-factory-build-your-first-pipeline.md) articolo e hello completo **prerequisito** passaggi.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-122">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete hello **prerequisite** steps.</span></span>
* <span data-ttu-id="ae9d6-123">Seguire le istruzioni [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview) articolo tooinstall versione più recente di Azure PowerShell nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-123">Follow instructions in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) article tooinstall latest version of Azure PowerShell on your computer.</span></span>
* <span data-ttu-id="ae9d6-124">Vedere [la creazione di modelli di gestione risorse di Azure](../azure-resource-manager/resource-group-authoring-templates.md) toolearn sui modelli di gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-124">See [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md) toolearn about Azure Resource Manager templates.</span></span> 

## <a name="in-this-tutorial"></a><span data-ttu-id="ae9d6-125">Contenuto dell'esercitazione:</span><span class="sxs-lookup"><span data-stu-id="ae9d6-125">In this tutorial</span></span>
| <span data-ttu-id="ae9d6-126">Entità</span><span class="sxs-lookup"><span data-stu-id="ae9d6-126">Entity</span></span> | <span data-ttu-id="ae9d6-127">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ae9d6-127">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ae9d6-128">Servizio collegato Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="ae9d6-128">Azure Storage linked service</span></span> |<span data-ttu-id="ae9d6-129">Collega la data factory toohello account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-129">Links your Azure Storage account toohello data factory.</span></span> <span data-ttu-id="ae9d6-130">contiene account di archiviazione di Azure Hello hello dati di input e outpui per la pipeline di hello in questo esempio.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-130">hello Azure Storage account holds hello input and output data for hello pipeline in this sample.</span></span> |
| <span data-ttu-id="ae9d6-131">Servizio collegato su richiesta HDInsight</span><span class="sxs-lookup"><span data-stu-id="ae9d6-131">HDInsight on-demand linked service</span></span> |<span data-ttu-id="ae9d6-132">Collega una factory del dati toohello cluster HDInsight su richiesta.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-132">Links an on-demand HDInsight cluster toohello data factory.</span></span> <span data-ttu-id="ae9d6-133">cluster Hello viene creato automaticamente tooprocess dati e viene eliminato al termine dell'elaborazione hello.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-133">hello cluster is automatically created for you tooprocess data and is deleted after hello processing is done.</span></span> |
| <span data-ttu-id="ae9d6-134">Set di dati di input del BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="ae9d6-134">Azure Blob input dataset</span></span> |<span data-ttu-id="ae9d6-135">Fa riferimento il servizio di archiviazione di Azure collegati toohello.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-135">Refers toohello Azure Storage linked service.</span></span> <span data-ttu-id="ae9d6-136">Hello servizio collegato fa riferimento tooan account di archiviazione Azure e set di dati Blob di Azure hello specifica hello contenitore, cartella e nome file nel servizio di archiviazione che contiene i dati di input hello hello.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-136">hello linked service refers tooan Azure Storage account and hello Azure Blob dataset specifies hello container, folder, and file name in hello storage that holds hello input data.</span></span> |
| <span data-ttu-id="ae9d6-137">Set di dati di output del BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="ae9d6-137">Azure Blob output dataset</span></span> |<span data-ttu-id="ae9d6-138">Fa riferimento il servizio di archiviazione di Azure collegati toohello.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-138">Refers toohello Azure Storage linked service.</span></span> <span data-ttu-id="ae9d6-139">Hello servizio collegato fa riferimento tooan account di archiviazione Azure e set di dati Blob di Azure hello specifica hello contenitore, cartella e nome file nel servizio di archiviazione che contiene i dati di output di hello hello.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-139">hello linked service refers tooan Azure Storage account and hello Azure Blob dataset specifies hello container, folder, and file name in hello storage that holds hello output data.</span></span> |
| <span data-ttu-id="ae9d6-140">Data Pipeline</span><span class="sxs-lookup"><span data-stu-id="ae9d6-140">Data pipeline</span></span> |<span data-ttu-id="ae9d6-141">Hello pipeline dispone di un'attività di tipo HDInsightHive, che elabora hello di un set di dati dell'input e restituisce il set di dati di hello output.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-141">hello pipeline has one activity of type HDInsightHive, which consumes hello input dataset and produces hello output dataset.</span></span> |

<span data-ttu-id="ae9d6-142">Una data factory può comprendere una o più pipeline.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-142">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="ae9d6-143">Una pipeline può comprendere una o più attività.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-143">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="ae9d6-144">Esistono due tipi di attività: [attività di spostamento dei dati](data-factory-data-movement-activities.md) e [attività di trasformazione dei dati](data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="ae9d6-144">There are two types of activities: [data movement activities](data-factory-data-movement-activities.md) and [data transformation activities](data-factory-data-transformation-activities.md).</span></span> <span data-ttu-id="ae9d6-145">In questa esercitazione si crea una pipeline con un'attività (attività Hive).</span><span class="sxs-lookup"><span data-stu-id="ae9d6-145">In this tutorial, you create a pipeline with one activity (Hive activity).</span></span>

<span data-ttu-id="ae9d6-146">Hello nella sezione seguente fornisce hello completo Gestione risorse modello per la definizione di entità Data Factory, che è possibile eseguire rapidamente tramite modelli di hello hello esercitazione e test.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-146">hello following section provides hello complete Resource Manager template for defining Data Factory entities so that you can quickly run through hello tutorial and test hello template.</span></span> <span data-ttu-id="ae9d6-147">toounderstand della definizione di ogni entità Data Factory, vedere [entità Data Factory nel modello hello](#data-factory-entities-in-the-template) sezione.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-147">toounderstand how each Data Factory entity is defined, see [Data Factory entities in hello template](#data-factory-entities-in-the-template) section.</span></span>

## <a name="data-factory-json-template"></a><span data-ttu-id="ae9d6-148">Modello JSON di Data Factory</span><span class="sxs-lookup"><span data-stu-id="ae9d6-148">Data Factory JSON template</span></span>
<span data-ttu-id="ae9d6-149">Hello modello Gestione risorse di livello superiore per la definizione di una data factory è:</span><span class="sxs-lookup"><span data-stu-id="ae9d6-149">hello top-level Resource Manager template for defining a data factory is:</span></span> 

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
<span data-ttu-id="ae9d6-150">Creare un file JSON denominato **ADFTutorialARM.json** in **C:\ADFGetStarted** cartella con hello seguente contenuto:</span><span class="sxs-lookup"><span data-stu-id="ae9d6-150">Create a JSON file named **ADFTutorialARM.json** in **C:\ADFGetStarted** folder with hello following content:</span></span>

```json
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "parameters": {
        "storageAccountName": { "type": "string", "metadata": { "description": "Name of hello Azure storage account that contains hello input/output data." } },
          "storageAccountKey": { "type": "securestring", "metadata": { "description": "Key for hello Azure storage account." } },
          "blobContainer": { "type": "string", "metadata": { "description": "Name of hello blob container in hello Azure Storage account." } },
          "inputBlobFolder": { "type": "string", "metadata": { "description": "hello folder in hello blob container that has hello input file." } },
          "inputBlobName": { "type": "string", "metadata": { "description": "Name of hello input file/blob." } },
          "outputBlobFolder": { "type": "string", "metadata": { "description": "hello folder in hello blob container that will hold hello transformed data." } },
          "hiveScriptFolder": { "type": "string", "metadata": { "description": "hello folder in hello blob container that contains hello Hive query file." } },
          "hiveScriptFile": { "type": "string", "metadata": { "description": "Name of hello hive query (HQL) file." } }
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
> <span data-ttu-id="ae9d6-151">È possibile trovare un altro esempio del modello di Resource Manager per la creazione di una data factory di Azure in [Tutorial: Create a pipeline with Copy Activity using an Azure Resource Manager template](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md) (Esercitazione: Creare una pipeline con l'attività di copia usando un modello di Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="ae9d6-151">You can find another example of Resource Manager template for creating an Azure data factory on [Tutorial: Create a pipeline with Copy Activity using an Azure Resource Manager template](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md).</span></span>  
> 
> 

## <a name="parameters-json"></a><span data-ttu-id="ae9d6-152">Parametri JSON</span><span class="sxs-lookup"><span data-stu-id="ae9d6-152">Parameters JSON</span></span>
<span data-ttu-id="ae9d6-153">Creare un file JSON denominato **ADFTutorialARM Parameters.json** che contiene i parametri per il modello di gestione risorse di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-153">Create a JSON file named **ADFTutorialARM-Parameters.json** that contains parameters for hello Azure Resource Manager template.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="ae9d6-154">Specificare il nome di hello e una chiave dell'account di archiviazione di Azure per hello **storageAccountName** e **storageAccountKey** parametri in questo file di parametro.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-154">Specify hello name and key of your Azure Storage account for hello **storageAccountName** and **storageAccountKey** parameters in this parameter file.</span></span> 
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
> <span data-ttu-id="ae9d6-155">È possibile file JSON di parametro separato per lo sviluppo, test e ambienti di produzione che è possibile utilizzare con hello stesso modello di Data Factory JSON.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-155">You may have separate parameter JSON files for development, testing, and production environments that you can use with hello same Data Factory JSON template.</span></span> <span data-ttu-id="ae9d6-156">Usando uno script di Power Shell, è possibile automatizzare la distribuzione delle entità di Data Factory in questi ambienti.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-156">By using a Power Shell script, you can automate deploying Data Factory entities in these environments.</span></span> 
> 
> 

## <a name="create-data-factory"></a><span data-ttu-id="ae9d6-157">Creare un'istanza di Data Factory</span><span class="sxs-lookup"><span data-stu-id="ae9d6-157">Create data factory</span></span>
1. <span data-ttu-id="ae9d6-158">Avviare **Azure PowerShell** e hello esecuzione comando seguente:</span><span class="sxs-lookup"><span data-stu-id="ae9d6-158">Start **Azure PowerShell** and run hello following command:</span></span> 
   * <span data-ttu-id="ae9d6-159">Eseguire hello comando seguente e immettere nome utente hello e la password usati toosign in toohello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-159">Run hello following command and enter hello user name and password that you use toosign in toohello Azure portal.</span></span>
    ```PowerShell
    Login-AzureRmAccount
    ```  
   * <span data-ttu-id="ae9d6-160">Eseguire hello successivo comando tooview tutte le sottoscrizioni di hello per questo account.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-160">Run hello following command tooview all hello subscriptions for this account.</span></span>
    ```PowerShell
    Get-AzureRmSubscription
    ``` 
   * <span data-ttu-id="ae9d6-161">Sottoscrizione hello tooselect da toowork con il comando seguente hello esecuzione.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-161">Run hello following command tooselect hello subscription that you want toowork with.</span></span> <span data-ttu-id="ae9d6-162">La sottoscrizione deve essere hello uguali a quelli hello usato nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-162">This subscription should be hello same as hello one you used in hello Azure portal.</span></span>
    ```
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```   
2. <span data-ttu-id="ae9d6-163">Eseguire hello successivo comando toodeploy Data Factory le entità utilizzando il modello di gestione risorse hello creato nel passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-163">Run hello following command toodeploy Data Factory entities using hello Resource Manager template you created in Step 1.</span></span> 

    ```PowerShell
    New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile C:\ADFGetStarted\ADFTutorialARM.json -TemplateParameterFile C:\ADFGetStarted\ADFTutorialARM-Parameters.json
    ```

## <a name="monitor-pipeline"></a><span data-ttu-id="ae9d6-164">Monitorare la pipeline</span><span class="sxs-lookup"><span data-stu-id="ae9d6-164">Monitor pipeline</span></span>
1. <span data-ttu-id="ae9d6-165">Dopo l'accesso toohello [portale di Azure](https://portal.azure.com/), fare clic su **Sfoglia** e selezionare **Data factory**.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-165">After logging in toohello [Azure portal](https://portal.azure.com/), Click **Browse** and select **Data factories**.</span></span>
     <span data-ttu-id="ae9d6-166">![Esplorare-&gt;Data factory](./media/data-factory-build-your-first-pipeline-using-arm/BrowseDataFactories.png)</span><span class="sxs-lookup"><span data-stu-id="ae9d6-166">![Browse->Data factories](./media/data-factory-build-your-first-pipeline-using-arm/BrowseDataFactories.png)</span></span>
2. <span data-ttu-id="ae9d6-167">In hello **Data factory** pannello, fare clic su data factory di hello (**TutorialFactoryARM**) creato.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-167">In hello **Data Factories** blade, click hello data factory (**TutorialFactoryARM**) you created.</span></span>    
3. <span data-ttu-id="ae9d6-168">In hello **Data Factory** pannello per il data factory, fare clic su **diagramma**.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-168">In hello **Data Factory** blade for your data factory, click **Diagram**.</span></span>

     ![Riquadro Diagramma](./media/data-factory-build-your-first-pipeline-using-arm/DiagramTile.png)
4. <span data-ttu-id="ae9d6-170">In hello **vista diagramma**, si visualizza una panoramica delle pipeline hello e set di dati utilizzati in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-170">In hello **Diagram View**, you see an overview of hello pipelines, and datasets used in this tutorial.</span></span>
   
   ![Vista Diagramma](./media/data-factory-build-your-first-pipeline-using-arm/DiagramView.png) 
5. <span data-ttu-id="ae9d6-172">In vista diagramma hello, fare doppio clic sul set di dati hello **AzureBlobOutput**.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-172">In hello Diagram View, double-click hello dataset **AzureBlobOutput**.</span></span> <span data-ttu-id="ae9d6-173">Vedrai tale sezione hello che è in corso di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-173">You see that hello slice that is currently being processed.</span></span>
   
    ![Set di dati](./media/data-factory-build-your-first-pipeline-using-arm/AzureBlobOutput.png)
6. <span data-ttu-id="ae9d6-175">Quando viene eseguita l'elaborazione, vedrai sezione hello **pronto** stato.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-175">When processing is done, you see hello slice in **Ready** state.</span></span> <span data-ttu-id="ae9d6-176">La creazione di un cluster HDInsight su richiesta di solito richiede tempo (circa 20 minuti).</span><span class="sxs-lookup"><span data-stu-id="ae9d6-176">Creation of an on-demand HDInsight cluster usually takes sometime (approximately 20 minutes).</span></span> <span data-ttu-id="ae9d6-177">Pertanto, prevedere hello pipeline tootake **circa 30 minuti** tooprocess hello sezione.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-177">Therefore, expect hello pipeline tootake **approximately 30 minutes** tooprocess hello slice.</span></span>
   
    ![Set di dati](./media/data-factory-build-your-first-pipeline-using-arm/SliceReady.png)    
7. <span data-ttu-id="ae9d6-179">Quando si trova in sezione hello **pronto** stato, controllare hello **partitioneddata** cartella hello **adfgetstarted** contenitore nell'archiviazione blob per hello i dati di output.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-179">When hello slice is in **Ready** state, check hello **partitioneddata** folder in hello **adfgetstarted** container in your blob storage for hello output data.</span></span>  

<span data-ttu-id="ae9d6-180">Vedere [monitorare set di dati e della pipeline](data-factory-monitor-manage-pipelines.md) per istruzioni su come pipeline di toouse hello pannelli portale Azure toomonitor hello e set di dati è stato creato in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-180">See [Monitor datasets and pipeline](data-factory-monitor-manage-pipelines.md) for instructions on how toouse hello Azure portal blades toomonitor hello pipeline and datasets you have created in this tutorial.</span></span>

<span data-ttu-id="ae9d6-181">È inoltre possibile utilizzare toomonitor monitorare e gestire App le pipeline di dati.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-181">You can also use Monitor and Manage App toomonitor your data pipelines.</span></span> <span data-ttu-id="ae9d6-182">Vedere [monitoraggio e la gestione delle pipeline di Data Factory di Azure utilizzando App monitoraggio](data-factory-monitor-manage-app.md) per informazioni dettagliate sull'utilizzo di un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-182">See [Monitor and manage Azure Data Factory pipelines using Monitoring App](data-factory-monitor-manage-app.md) for details about using hello application.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="ae9d6-183">file di input Hello eliminato quando la sezione hello viene elaborata correttamente.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-183">hello input file gets deleted when hello slice is processed successfully.</span></span> <span data-ttu-id="ae9d6-184">Pertanto, se si desidera toorerun hello sezione o hello esercitazione nuovamente, hello del file di input (input.log) toohello inputdata cartella del contenitore adfgetstarted hello di caricamento.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-184">Therefore, if you want toorerun hello slice or do hello tutorial again, upload hello input file (input.log) toohello inputdata folder of hello adfgetstarted container.</span></span>
> 
> 

## <a name="data-factory-entities-in-hello-template"></a><span data-ttu-id="ae9d6-185">Entità di modello hello Factory di dati</span><span class="sxs-lookup"><span data-stu-id="ae9d6-185">Data Factory entities in hello template</span></span>
### <a name="define-data-factory"></a><span data-ttu-id="ae9d6-186">Definire una data factory</span><span class="sxs-lookup"><span data-stu-id="ae9d6-186">Define data factory</span></span>
<span data-ttu-id="ae9d6-187">È consigliabile definire una data factory nel modello di gestione risorse di hello come illustrato nel seguente esempio hello:</span><span class="sxs-lookup"><span data-stu-id="ae9d6-187">You define a data factory in hello Resource Manager template as shown in hello following sample:</span></span>  

```json
"resources": [
{
    "name": "[variables('dataFactoryName')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "West US"
}
```
<span data-ttu-id="ae9d6-188">dataFactoryName Hello è definito come:</span><span class="sxs-lookup"><span data-stu-id="ae9d6-188">hello dataFactoryName is defined as:</span></span> 

```json
"dataFactoryName": "[concat('HiveTransformDF', uniqueString(resourceGroup().id))]",
```
<span data-ttu-id="ae9d6-189">È una stringa univoca in base a hello ID gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-189">It is a unique string based on hello resource group ID.</span></span>  

### <a name="defining-data-factory-entities"></a><span data-ttu-id="ae9d6-190">Definizione di entità di Data factory</span><span class="sxs-lookup"><span data-stu-id="ae9d6-190">Defining Data Factory entities</span></span>
<span data-ttu-id="ae9d6-191">Hello entità Data Factory seguenti vengono definite nel modello JSON hello:</span><span class="sxs-lookup"><span data-stu-id="ae9d6-191">hello following Data Factory entities are defined in hello JSON template:</span></span> 

* [<span data-ttu-id="ae9d6-192">Servizio collegato Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="ae9d6-192">Azure Storage linked service</span></span>](#azure-storage-linked-service)
* [<span data-ttu-id="ae9d6-193">Servizio collegato su richiesta HDInsight</span><span class="sxs-lookup"><span data-stu-id="ae9d6-193">HDInsight on-demand linked service</span></span>](#hdinsight-on-demand-linked-service)
* [<span data-ttu-id="ae9d6-194">Set di dati di input del BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="ae9d6-194">Azure blob input dataset</span></span>](#azure-blob-input-dataset)
* [<span data-ttu-id="ae9d6-195">Set di dati di output del BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="ae9d6-195">Azure blob output dataset</span></span>](#azure-blob-output-dataset)
* [<span data-ttu-id="ae9d6-196">Pipeline di dati con un'attività di copia</span><span class="sxs-lookup"><span data-stu-id="ae9d6-196">Data pipeline with a copy activity</span></span>](#data-pipeline)

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="ae9d6-197">Servizio collegato Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="ae9d6-197">Azure Storage linked service</span></span>
<span data-ttu-id="ae9d6-198">Specificare il nome di hello e chiave dell'account di archiviazione di Azure in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-198">You specify hello name and key of your Azure storage account in this section.</span></span> <span data-ttu-id="ae9d6-199">Vedere [servizio collegato di archiviazione di Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service) per informazioni dettagliate su JSON proprietà utilizzate toodefine servizio collegato di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-199">See [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used toodefine an Azure Storage linked service.</span></span> 

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
<span data-ttu-id="ae9d6-200">Hello **connectionString** utilizza hello parametri storageAccountName e storageAccountKey.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-200">hello **connectionString** uses hello storageAccountName and storageAccountKey parameters.</span></span> <span data-ttu-id="ae9d6-201">valori Hello per questi parametri passati mediante un file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-201">hello values for these parameters passed by using a configuration file.</span></span> <span data-ttu-id="ae9d6-202">definizione di Hello utilizza anche variabili: azureStroageLinkedService e dataFactoryName definiti nel modello di hello.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-202">hello definition also uses variables: azureStroageLinkedService and dataFactoryName defined in hello template.</span></span> 

#### <a name="hdinsight-on-demand-linked-service"></a><span data-ttu-id="ae9d6-203">Servizio collegato su richiesta HDInsight</span><span class="sxs-lookup"><span data-stu-id="ae9d6-203">HDInsight on-demand linked service</span></span>
<span data-ttu-id="ae9d6-204">Vedere [servizi collegati di calcolo](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) articolo per informazioni dettagliate su JSON proprietà utilizzate toodefine un servizio collegato di HDInsight su richiesta.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-204">See [Compute linked services](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) article for details about JSON properties used toodefine an HDInsight on-demand linked service.</span></span>  

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
<span data-ttu-id="ae9d6-205">Si noti hello seguenti punti:</span><span class="sxs-lookup"><span data-stu-id="ae9d6-205">Note hello following points:</span></span> 

* <span data-ttu-id="ae9d6-206">Hello Data Factory viene creata una **basati su Linux** cluster HDInsight per l'utente con hello sopra JSON.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-206">hello Data Factory creates a **Linux-based** HDInsight cluster for you with hello above JSON.</span></span> <span data-ttu-id="ae9d6-207">Per i dettagli, vedere [Servizio collegato Azure HDInsight su richiesta](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) .</span><span class="sxs-lookup"><span data-stu-id="ae9d6-207">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span> 
* <span data-ttu-id="ae9d6-208">È possibile usare il **proprio cluster HDInsight** anziché un cluster HDInsight su richiesta.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-208">You could use **your own HDInsight cluster** instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="ae9d6-209">Per i dettagli, vedere [Servizio collegato Azure HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) .</span><span class="sxs-lookup"><span data-stu-id="ae9d6-209">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details.</span></span>
* <span data-ttu-id="ae9d6-210">Crea cluster HDInsight Hello un **contenitore predefinito** nell'archiviazione blob hello specificato in JSON hello (**linkedServiceName**).</span><span class="sxs-lookup"><span data-stu-id="ae9d6-210">hello HDInsight cluster creates a **default container** in hello blob storage you specified in hello JSON (**linkedServiceName**).</span></span> <span data-ttu-id="ae9d6-211">HDInsight non eliminare questo contenitore quando viene eliminato il cluster hello.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-211">HDInsight does not delete this container when hello cluster is deleted.</span></span> <span data-ttu-id="ae9d6-212">Questo comportamento dipende dalla progettazione.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-212">This behavior is by design.</span></span> <span data-ttu-id="ae9d6-213">Con il servizio collegato di HDInsight su richiesta, un cluster HDInsight viene creato ogni volta che una sezione deve toobe elaborati a meno che non vi è un cluster esistente in tempo reale (**timeToLive**) e viene eliminata quando viene eseguita un'elaborazione hello.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-213">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice needs toobe processed unless there is an existing live cluster (**timeToLive**) and is deleted when hello processing is done.</span></span>
  
    <span data-ttu-id="ae9d6-214">Man mano che vengono elaborate più sezioni, vengono visualizzati numerosi contenitori nell'archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-214">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="ae9d6-215">Se non li necessario per la risoluzione dei problemi dei processi di hello, è opportuno toodelete li tooreduce hello il costo di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-215">If you do not need them for troubleshooting of hello jobs, you may want toodelete them tooreduce hello storage cost.</span></span> <span data-ttu-id="ae9d6-216">i nomi di Hello di questi contenitori seguono un modello: "adf**yourdatafactoryname**-**linkedservicename**- datetimestamp".</span><span class="sxs-lookup"><span data-stu-id="ae9d6-216">hello names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="ae9d6-217">Utilizzare strumenti come [Esplora archivi Microsoft](http://storageexplorer.com/) toodelete contenitori di Azure nell'archiviazione blob.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-217">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) toodelete containers in your Azure blob storage.</span></span>

<span data-ttu-id="ae9d6-218">Per i dettagli, vedere [Servizio collegato Azure HDInsight su richiesta](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) .</span><span class="sxs-lookup"><span data-stu-id="ae9d6-218">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>

#### <a name="azure-blob-input-dataset"></a><span data-ttu-id="ae9d6-219">Set di dati di input del BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="ae9d6-219">Azure blob input dataset</span></span>
<span data-ttu-id="ae9d6-220">Specificare nomi di hello del contenitore blob, cartelle e file che contiene i dati di input hello.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-220">You specify hello names of blob container, folder, and file that contains hello input data.</span></span> <span data-ttu-id="ae9d6-221">Vedere [proprietà set di dati Blob di Azure](data-factory-azure-blob-connector.md#dataset-properties) per informazioni dettagliate su JSON proprietà utilizzate toodefine un set di dati Blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-221">See [Azure Blob dataset properties](data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used toodefine an Azure Blob dataset.</span></span> 

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
<span data-ttu-id="ae9d6-222">Questa definizione utilizza i seguenti parametri definiti nel modello di parametro hello: blobContainer, inputBlobFolder e inputBlobName.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-222">This definition uses hello following parameters defined in parameter template: blobContainer, inputBlobFolder, and inputBlobName.</span></span> 

#### <a name="azure-blob-output-dataset"></a><span data-ttu-id="ae9d6-223">Set di dati di output del BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="ae9d6-223">Azure Blob output dataset</span></span>
<span data-ttu-id="ae9d6-224">Specificare i nomi di hello del contenitore blob e di cartella che contiene i dati di output di hello.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-224">You specify hello names of blob container and folder that holds hello output data.</span></span> <span data-ttu-id="ae9d6-225">Vedere [proprietà set di dati Blob di Azure](data-factory-azure-blob-connector.md#dataset-properties) per informazioni dettagliate su JSON proprietà utilizzate toodefine un set di dati Blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-225">See [Azure Blob dataset properties](data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used toodefine an Azure Blob dataset.</span></span>  

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

<span data-ttu-id="ae9d6-226">Questa definizione utilizza i seguenti parametri definiti nel modello di parametro hello hello: blobContainer e outputBlobFolder.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-226">This definition uses hello following parameters defined in hello parameter template: blobContainer and outputBlobFolder.</span></span> 

#### <a name="data-pipeline"></a><span data-ttu-id="ae9d6-227">Data Pipeline</span><span class="sxs-lookup"><span data-stu-id="ae9d6-227">Data pipeline</span></span>
<span data-ttu-id="ae9d6-228">Viene definita una pipeline che trasforma i dati eseguendo lo script Hive in un cluster HDInsight di Azure su richiesta.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-228">You define a pipeline that transform data by running Hive script on an on-demand Azure HDInsight cluster.</span></span> <span data-ttu-id="ae9d6-229">Vedere [JSON di Pipeline](data-factory-create-pipelines.md#pipeline-json) per le descrizioni degli elementi usati di JSON toodefine una pipeline in questo esempio.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-229">See [Pipeline JSON](data-factory-create-pipelines.md#pipeline-json) for descriptions of JSON elements used toodefine a pipeline in this example.</span></span> 

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

## <a name="reuse-hello-template"></a><span data-ttu-id="ae9d6-230">Riutilizzare hello modello</span><span class="sxs-lookup"><span data-stu-id="ae9d6-230">Reuse hello template</span></span>
<span data-ttu-id="ae9d6-231">Nell'esercitazione hello è creato un modello per la definizione di entità Data Factory e un modello per il passaggio di valori per i parametri.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-231">In hello tutorial, you created a template for defining Data Factory entities and a template for passing values for parameters.</span></span> <span data-ttu-id="ae9d6-232">toouse hello stessi ambienti con toodifferent entità modello toodeploy Data Factory, creare un file di parametro per ogni ambiente e usarlo quando si distribuisce toothat ambiente.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-232">toouse hello same template toodeploy Data Factory entities toodifferent environments, you create a parameter file for each environment and use it when deploying toothat environment.</span></span>     

<span data-ttu-id="ae9d6-233">Esempio:</span><span class="sxs-lookup"><span data-stu-id="ae9d6-233">Example:</span></span>  

```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Dev.json

New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Test.json

New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Production.json
```
<span data-ttu-id="ae9d6-234">Si noti che hello primo comando Usa il file di parametro per l'ambiente di sviluppo hello, secondo una per hello ambiente di test e una terza per ambiente di produzione hello hello.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-234">Notice that hello first command uses parameter file for hello development environment, second one for hello test environment, and hello third one for hello production environment.</span></span>  

<span data-ttu-id="ae9d6-235">È inoltre possibile riutilizzare hello modello tooperform ripetuto di attività.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-235">You can also reuse hello template tooperform repeated tasks.</span></span> <span data-ttu-id="ae9d6-236">Ad esempio, è necessario toocreate molti data factory con uno o più pipeline che implementano hello stessa logica, ma ogni data factory Usa archiviazione di Azure differente e gli account di Database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-236">For example, you need toocreate many data factories with one or more pipelines that implement hello same logic but each data factory uses different Azure storage and Azure SQL Database accounts.</span></span> <span data-ttu-id="ae9d6-237">In questo scenario, si usa hello stesso modello in hello stesso ambiente (sviluppo, test o produzione) con parametri diversi file toocreate data factory.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-237">In this scenario, you use hello same template in hello same environment (dev, test, or production) with different parameter files toocreate data factories.</span></span> 

## <a name="resource-manager-template-for-creating-a-gateway"></a><span data-ttu-id="ae9d6-238">Modello di Resource Manager per la creazione di un gateway</span><span class="sxs-lookup"><span data-stu-id="ae9d6-238">Resource Manager template for creating a gateway</span></span>
<span data-ttu-id="ae9d6-239">Di seguito è riportato un modello di gestione risorse di esempio per la creazione di un gateway logico in hello nuovamente.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-239">Here is a sample Resource Manager template for creating a logical gateway in hello back.</span></span> <span data-ttu-id="ae9d6-240">Installare un gateway nel computer locale o macchina virtuale IaaS di Azure e registrare il gateway di hello con il servizio Data Factory tramite una chiave.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-240">Install a gateway on your on-premises computer or Azure IaaS VM and register hello gateway with Data Factory service using a key.</span></span> <span data-ttu-id="ae9d6-241">Per altre informazioni vedere [Spostare dati tra origini locali e il cloud con Gateway di gestione dati](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="ae9d6-241">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) for details.</span></span>

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
<span data-ttu-id="ae9d6-242">Questo modello crea una data factory denominata GatewayUsingArmDF con un gateway denominato GatewayUsingARM.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-242">This template creates a data factory named GatewayUsingArmDF with a gateway named: GatewayUsingARM.</span></span> 

## <a name="see-also"></a><span data-ttu-id="ae9d6-243">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="ae9d6-243">See Also</span></span>
| <span data-ttu-id="ae9d6-244">Argomento</span><span class="sxs-lookup"><span data-stu-id="ae9d6-244">Topic</span></span> | <span data-ttu-id="ae9d6-245">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ae9d6-245">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="ae9d6-246">Pipeline</span><span class="sxs-lookup"><span data-stu-id="ae9d6-246">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="ae9d6-247">In questo articolo consente di comprendere le pipeline e attività nella Data Factory di Azure e come toouse li tooconstruct end-to-end basato sui dati dei flussi di lavoro degli scenario o dell'azienda.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-247">This article helps you understand pipelines and activities in Azure Data Factory and how toouse them tooconstruct end-to-end data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="ae9d6-248">Set di dati</span><span class="sxs-lookup"><span data-stu-id="ae9d6-248">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="ae9d6-249">Questo articolo fornisce informazioni sui set di dati in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-249">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="ae9d6-250">Pianificazione ed esecuzione</span><span class="sxs-lookup"><span data-stu-id="ae9d6-250">Scheduling and execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="ae9d6-251">Questo articolo illustra gli aspetti hello di pianificazione e l'esecuzione del modello di applicazione di Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-251">This article explains hello scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="ae9d6-252">Monitorare e gestire le pipeline con l'app di monitoraggio</span><span class="sxs-lookup"><span data-stu-id="ae9d6-252">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="ae9d6-253">In questo articolo viene descritto come toomonitor, gestire ed eseguire il debug pipeline utilizzando hello monitoraggio e gestione delle App.</span><span class="sxs-lookup"><span data-stu-id="ae9d6-253">This article describes how toomonitor, manage, and debug pipelines using hello Monitoring & Management App.</span></span> |

