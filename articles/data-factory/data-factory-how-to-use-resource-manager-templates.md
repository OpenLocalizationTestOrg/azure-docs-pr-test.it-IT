---
title: Usare i modelli di Resource Manager in Data Factory | Microsoft Docs
description: "Informazioni su come creare e usare modelli di Azure Resource Manager per la creazione di entità di Data Factory."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: 
ms.assetid: 37724021-f55f-4e85-9206-6d4a48bda3d8
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: c3ea2c047434b5b5495f0ce85be9376a502e4962
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-templates-to-create-azure-data-factory-entities"></a><span data-ttu-id="37471-103">Usare modelli per creare entità di Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="37471-103">Use templates to create Azure Data Factory entities</span></span>
## <a name="overview"></a><span data-ttu-id="37471-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="37471-104">Overview</span></span>
<span data-ttu-id="37471-105">Durante l'uso di Azure Data Factory per le esigenze di integrazione dei dati, può essere necessario riusare lo stesso modello in ambienti diversi o implementare ripetutamente la stessa attività all'interno di una soluzione.</span><span class="sxs-lookup"><span data-stu-id="37471-105">While using Azure Data Factory for your data integration needs, you may find yourself reusing the same pattern across different environments or implementing the same task repetitively within the same solution.</span></span> <span data-ttu-id="37471-106">I modelli consentono di implementare e gestire questi scenari in modo semplificato.</span><span class="sxs-lookup"><span data-stu-id="37471-106">Templates help you implement and manage these scenarios in an easy manner.</span></span> <span data-ttu-id="37471-107">I modelli di Azure Data Factory rappresentano la soluzione ideale per gli scenari che implicano riusabilità e ripetizione.</span><span class="sxs-lookup"><span data-stu-id="37471-107">Templates in Azure Data Factory are ideal for scenarios that involve reusability and repetition.</span></span>

<span data-ttu-id="37471-108">Si consideri la situazione in cui un'organizzazione ha 10 impianti di produzione a livello globale.</span><span class="sxs-lookup"><span data-stu-id="37471-108">Consider the situation where an organization has 10 manufacturing plants across the world.</span></span> <span data-ttu-id="37471-109">I log provenienti da ogni impianto vengono archiviati in un database SQL Server locale separato.</span><span class="sxs-lookup"><span data-stu-id="37471-109">The logs from each plant are stored in a separate on-premises SQL Server database.</span></span> <span data-ttu-id="37471-110">La società vuole compilare un unico data warehouse nel cloud per l'analisi ad hoc.</span><span class="sxs-lookup"><span data-stu-id="37471-110">The company wants to build a single data warehouse in the cloud for ad-hoc analytics.</span></span> <span data-ttu-id="37471-111">Vuole inoltre sfruttare la stessa logica, ma configurazioni diverse per gli ambienti di sviluppo, test e produzione.</span><span class="sxs-lookup"><span data-stu-id="37471-111">It also wants to have the same logic but different configurations for development, test, and production environments.</span></span>

<span data-ttu-id="37471-112">In questo caso, è necessario ripetere un'attività all'interno dello stesso ambiente, ma con valori diversi nelle 10 data factory per ogni impianto di produzione.</span><span class="sxs-lookup"><span data-stu-id="37471-112">In this case, a task needs to be repeated within the same environment, but with different values across the 10 data factories for each manufacturing plant.</span></span> <span data-ttu-id="37471-113">In effetti, l'elemento della **ripetizione** è presente.</span><span class="sxs-lookup"><span data-stu-id="37471-113">In effect, **repetition** is present.</span></span> <span data-ttu-id="37471-114">La creazione di modelli consente l'astrazione di questo flusso generico (ovvero di pipeline con le stesse attività in ogni data factory), ma usa un file dei parametri separato per ogni impianto di produzione.</span><span class="sxs-lookup"><span data-stu-id="37471-114">Templating allows the abstraction of this generic flow (that is, pipelines having the same activities in each data factory), but uses a separate parameter file for each manufacturing plant.</span></span>

<span data-ttu-id="37471-115">L'organizzazione vuole inoltre distribuire le 10 data factory più volte in ambienti diversi, pertanto i modelli possono sfruttare questa **riusabilità** utilizzando file dei parametri separati per gli ambienti di sviluppo, test e produzione.</span><span class="sxs-lookup"><span data-stu-id="37471-115">Furthermore, as the organization wants to deploy these 10 data factories multiple times across different environments, templates can use this **reusability** by utilizing separate parameter files for development, test, and production environments.</span></span>

## <a name="templating-with-azure-resource-manager"></a><span data-ttu-id="37471-116">Creazione di modelli con Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="37471-116">Templating with Azure Resource Manager</span></span>
<span data-ttu-id="37471-117">I [modelli di Azure Resource Manager](../azure-resource-manager/resource-group-overview.md#template-deployment) rappresentano un'ottima soluzione per la creazione di modelli in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="37471-117">[Azure Resource Manager templates](../azure-resource-manager/resource-group-overview.md#template-deployment) are a great way to achieve templating in Azure Data Factory.</span></span> <span data-ttu-id="37471-118">I modelli di Resource Manager consentono di definire l'infrastruttura e la configurazione della soluzione di Azure tramite un file JSON.</span><span class="sxs-lookup"><span data-stu-id="37471-118">Resource Manager templates define the infrastructure and configuration of your Azure solution through a JSON file.</span></span> <span data-ttu-id="37471-119">Poiché i modelli di Azure Resource Manager funzionano con tutti i servizi di Azure o con la maggior parte di essi, Resource Manager può essere ampiamente usato per gestire facilmente tutte le risorse degli asset di Azure.</span><span class="sxs-lookup"><span data-stu-id="37471-119">Because Azure Resource Manager templates work with all/most Azure services, it can be widely used to easily manage all resources of your Azure assets.</span></span> <span data-ttu-id="37471-120">Per informazioni generali sui modelli di Azure Resource Manager, vedere [Creazione di modelli di Gestione risorse di Azure](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="37471-120">See [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md) to learn more about the Resource Manager Templates in general.</span></span>

## <a name="tutorials"></a><span data-ttu-id="37471-121">Esercitazioni</span><span class="sxs-lookup"><span data-stu-id="37471-121">Tutorials</span></span>
<span data-ttu-id="37471-122">Per istruzioni dettagliate sulla creazione di entità di Data Factory tramite i modelli di Resource Manager, vedere le esercitazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="37471-122">See the following tutorials for step-by-step instructions to create Data Factory entities by using Resource Manager templates:</span></span>

* <span data-ttu-id="37471-123">[Tutorial: Create a pipeline to copy data by using Azure Resource Manager template](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md) (Esercitazione: Creare una pipeline per copiare dati usando il modello di Azure Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="37471-123">[Tutorial: Create a pipeline to copy data by using Azure Resource Manager template](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)</span></span>
* <span data-ttu-id="37471-124">[Tutorial: Create a pipeline to process data by using Azure Resource Manager template](data-factory-build-your-first-pipeline.md) (Esercitazione: Creare una pipeline per elaborare dati usando il modello di Azure Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="37471-124">[Tutorial: Create a pipeline to process data by using Azure Resource Manager template](data-factory-build-your-first-pipeline.md)</span></span>

## <a name="data-factory-templates-on-github"></a><span data-ttu-id="37471-125">Modelli di data factory in GitHub</span><span class="sxs-lookup"><span data-stu-id="37471-125">Data Factory templates on GitHub</span></span>
<span data-ttu-id="37471-126">Vedere i modelli di avvio rapido di Azure in GitHub elencati di seguito:</span><span class="sxs-lookup"><span data-stu-id="37471-126">Check out the following Azure quick start templates on GitHub:</span></span>

* <span data-ttu-id="37471-127">[Create a Data factory to copy data from Azure Blob Storage to Azure SQL Database](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-blob-to-sql-copy) (Creare una data factory per copiare dati dall'archivio BLOB di Azure al database SQL di Azure)</span><span class="sxs-lookup"><span data-stu-id="37471-127">[Create a Data factory to copy data from Azure Blob Storage to Azure SQL Database](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-blob-to-sql-copy)</span></span>
* <span data-ttu-id="37471-128">[Create a Data factory with Hive activity on Azure HDInsight cluster](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-hive-transformation) (Creare una data factory con un'attività Hive in un cluster Azure HDInsight)</span><span class="sxs-lookup"><span data-stu-id="37471-128">[Create a Data factory with Hive activity on Azure HDInsight cluster](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-hive-transformation)</span></span>
* <span data-ttu-id="37471-129">[Create a Data factory to copy data from Salesforce to Azure Blobs](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-salesforce-to-blob-copy) (Creare una data factory per copiare dati da Salesforce a BLOB di Azure)</span><span class="sxs-lookup"><span data-stu-id="37471-129">[Create a Data factory to copy data from Salesforce to Azure Blobs](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-salesforce-to-blob-copy)</span></span>
* [<span data-ttu-id="37471-130">Creare una Data factory che collega le attività: copia i dati da un server FTP ai BLOB di Azure, richiama uno script hive in un cluster HDInsight su richiesta per trasformare i dati e copia i risultati nel database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="37471-130">Create a Data factory that chains activities: copies data from an FTP server to Azure Blobs, invokes a hive script on an on-demand HDInsight cluster to transform the data, and copies result into Azure SQL Database</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-data-factory-ftp-hive-blob)

<span data-ttu-id="37471-131">È possibile condividere i modelli di Azure Data Factory in [Modelli di avvio rapido di Azure](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="37471-131">Feel free to share your Azure Data Factory templates at [Azure Quick start](https://azure.microsoft.com/documentation/templates/).</span></span> <span data-ttu-id="37471-132">Durante lo sviluppo di modelli che possono essere condivisi tramite questo repository, consultare la [guida alla collaborazione](https://github.com/Azure/azure-quickstart-templates/tree/master/1-CONTRIBUTION-GUIDE).</span><span class="sxs-lookup"><span data-stu-id="37471-132">Refer to the [contribution guide](https://github.com/Azure/azure-quickstart-templates/tree/master/1-CONTRIBUTION-GUIDE) while developing templates that can be shared via this repository.</span></span>

<span data-ttu-id="37471-133">Le sezioni seguenti includono informazioni dettagliate sulla definizione delle risorse di Data Factory in un modello di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="37471-133">The following sections provide details about defining Data Factory resources in a Resource Manager template.</span></span>

## <a name="defining-data-factory-resources-in-templates"></a><span data-ttu-id="37471-134">Definizione delle risorse di Data Factory nei modelli</span><span class="sxs-lookup"><span data-stu-id="37471-134">Defining Data Factory resources in templates</span></span>
<span data-ttu-id="37471-135">Il modello principale per la definizione di una data factory è il seguente:</span><span class="sxs-lookup"><span data-stu-id="37471-135">The top-level template for defining a data factory is:</span></span>

```JSON
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
    { "type": "linkedservices",
        ...
    },
    {"type": "datasets",
        ...
    },
    {"type": "dataPipelines",
        ...
    }
}
```

### <a name="define-data-factory"></a><span data-ttu-id="37471-136">Definire una data factory</span><span class="sxs-lookup"><span data-stu-id="37471-136">Define data factory</span></span>
<span data-ttu-id="37471-137">È possibile definire una data factory nel modello di Resource Manager come illustrato nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="37471-137">You define a data factory in the Resource Manager template as shown in the following sample:</span></span>

```JSON
"resources": [
{
    "name": "[variables('<mydataFactoryName>')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "East US"
}
```
<span data-ttu-id="37471-138">Il valore dataFactoryName viene definito in "variables" come segue:</span><span class="sxs-lookup"><span data-stu-id="37471-138">The dataFactoryName is defined in “variables” as:</span></span>

```JSON
"dataFactoryName": "[concat('<myDataFactoryName>', uniqueString(resourceGroup().id))]",
```

### <a name="define-linked-services"></a><span data-ttu-id="37471-139">Definire servizi collegati</span><span class="sxs-lookup"><span data-stu-id="37471-139">Define linked services</span></span>

```JSON
"type": "linkedservices",
"name": "[variables('<LinkedServiceName>')]",
"apiVersion": "2015-10-01",
"dependsOn": [ "[variables('<dataFactoryName>')]" ],
"properties": {
    ...
}
```

<span data-ttu-id="37471-140">Per informazioni dettagliate sulle proprietà JSON per il servizio collegato specifico da distribuire, vedere [Servizio collegato Archiviazione](data-factory-azure-blob-connector.md#azure-storage-linked-service) o [Servizi collegati di calcolo](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="37471-140">See [Storage Linked Service](data-factory-azure-blob-connector.md#azure-storage-linked-service) or [Compute Linked Services](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details about the JSON properties for the specific linked service you wish to deploy.</span></span> <span data-ttu-id="37471-141">Il parametro "dependsOn" specifica il nome della data factory corrispondente.</span><span class="sxs-lookup"><span data-stu-id="37471-141">The “dependsOn” parameter specifies name of the corresponding data factory.</span></span> <span data-ttu-id="37471-142">Un esempio di definizione di un servizio collegato per Archiviazione di Azure è illustrato nella definizione JSON seguente:</span><span class="sxs-lookup"><span data-stu-id="37471-142">An example of defining a linked service for Azure Storage is shown in the following JSON definition:</span></span>

### <a name="define-datasets"></a><span data-ttu-id="37471-143">Definire i set di dati</span><span class="sxs-lookup"><span data-stu-id="37471-143">Define datasets</span></span>

```JSON
"type": "datasets",
"name": "[variables('<myDatasetName>')]",
"dependsOn": [
    "[variables('<dataFactoryName>')]",
    "[variables('<myDatasetLinkedServiceName>')]"
],
"apiVersion": "2015-10-01",
"properties": {
    ...
}
```
<span data-ttu-id="37471-144">Per informazioni dettagliate sulle proprietà JSON per il tipo di set di dati specifico da distribuire, vedere [Archivi dati e formati supportati](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="37471-144">Refer to [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) for details about the JSON properties for the specific dataset type you wish to deploy.</span></span> <span data-ttu-id="37471-145">Il parametro "dependsOn" specifica il nome della data factory e del servizio collegato di archiviazione corrispondenti.</span><span class="sxs-lookup"><span data-stu-id="37471-145">Note the “dependsOn” parameter specifies name of the corresponding data factory and storage linked service.</span></span> <span data-ttu-id="37471-146">Un esempio di definizione di un tipo di set di dati per l'archivio BLOB di Azure è illustrato nella definizione JSON seguente:</span><span class="sxs-lookup"><span data-stu-id="37471-146">An example of defining dataset type of Azure blob storage is shown in the following JSON definition:</span></span>

```JSON
"type": "datasets",
"name": "[variables('storageDataset')]",
"dependsOn": [
    "[variables('dataFactoryName')]",
    "[variables('storageLinkedServiceName')]"
],
"apiVersion": "2015-10-01",
"properties": {
"type": "AzureBlob",
"linkedServiceName": "[variables('storageLinkedServiceName')]",
"typeProperties": {
    "folderPath": "[concat(parameters('sourceBlobContainer'), '/')]",
    "fileName": "[parameters('sourceBlobName')]",
    "format": {
        "type": "TextFormat"
    }
},
"availability": {
    "frequency": "Hour",
    "interval": 1
}
```

### <a name="define-pipelines"></a><span data-ttu-id="37471-147">Definire pipeline</span><span class="sxs-lookup"><span data-stu-id="37471-147">Define pipelines</span></span>

```JSON
"type": "dataPipelines",
"name": "[variables('<mypipelineName>')]",
"dependsOn": [
    "[variables('<dataFactoryName>')]",
    "[variables('<inputDatasetLinkedServiceName>')]",
    "[variables('<outputDatasetLinkedServiceName>')]",
    "[variables('<inputDataset>')]",
    "[variables('<outputDataset>')]"
],
"apiVersion": "2015-10-01",
"properties": {
    activities: {
        ...
    }
}
```

<span data-ttu-id="37471-148">Per informazioni dettagliate sulle proprietà JSON per la definizione di attività e pipeline specifiche da distribuire, vedere la sezione relativa alla [definizione di pipeline](data-factory-create-pipelines.md#pipeline-json).</span><span class="sxs-lookup"><span data-stu-id="37471-148">Refer to [defining pipelines](data-factory-create-pipelines.md#pipeline-json) for details about the JSON properties for defining the specific pipeline and activities you wish to deploy.</span></span> <span data-ttu-id="37471-149">Il parametro "dependsOn" specifica il nome della data factory e di tutti i servizi collegati o dei set di dati corrispondenti.</span><span class="sxs-lookup"><span data-stu-id="37471-149">Note the “dependsOn” parameter specifies name of the data factory, and any corresponding linked services or datasets.</span></span> <span data-ttu-id="37471-150">Un esempio di pipeline che copia i dati dall'archivio BLOB di Azure al database SQL di Azure è illustrato nel frammento di codice JSON seguente:</span><span class="sxs-lookup"><span data-stu-id="37471-150">An example of a pipeline that copies data from Azure Blob Storage to Azure SQL Database is shown in the following JSON snippet:</span></span>

```JSON
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
    "start": "2016-10-03T00:00:00Z",
    "end": "2016-10-04T00:00:00Z"
}
```
## <a name="parameterizing-data-factory-template"></a><span data-ttu-id="37471-151">Uso di parametri nel modello di Data Factory</span><span class="sxs-lookup"><span data-stu-id="37471-151">Parameterizing Data Factory template</span></span>
<span data-ttu-id="37471-152">Per le procedure consigliate sull'uso dei parametri, vedere l'articolo [Procedure consigliate per la creazione di modelli di Azure Resource Manager](../azure-resource-manager/resource-manager-template-best-practices.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="37471-152">For best practices on parameterizing, see [Best practices for creating Azure Resource Manager templates](../azure-resource-manager/resource-manager-template-best-practices.md#parameters) article.</span></span> <span data-ttu-id="37471-153">In generale l'utilizzo dei parametri deve essere ridotto al minimo, soprattutto se è possibile usare variabili anziché parametri.</span><span class="sxs-lookup"><span data-stu-id="37471-153">In general, parameter usage should be minimized, especially if variables can be used instead.</span></span> <span data-ttu-id="37471-154">Specificare i parametri solo negli scenari seguenti:</span><span class="sxs-lookup"><span data-stu-id="37471-154">Only provide parameters in the following scenarios:</span></span>

* <span data-ttu-id="37471-155">Le impostazioni variano a seconda dell'ambiente, ad esempio di sviluppo, test e produzione</span><span class="sxs-lookup"><span data-stu-id="37471-155">Settings vary by environment (example: development, test, and production)</span></span>
* <span data-ttu-id="37471-156">Segreti (password)</span><span class="sxs-lookup"><span data-stu-id="37471-156">Secrets (such as passwords)</span></span>

<span data-ttu-id="37471-157">Se è necessario eseguire il pull di segreti dall'[Insieme di credenziali delle chiavi di Azure](../key-vault/key-vault-get-started.md) quando si distribuiscono entità di Azure Data Factory tramite modelli, specificare l'**insieme di credenziali delle chiavi** e il **nome del segreto** come illustrato nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="37471-157">If you need to pull secrets from [Azure Key Vault](../key-vault/key-vault-get-started.md) when deploying Azure Data Factory entities using templates, specify the **key vault** and **secret name** as shown in the following example:</span></span>

```JSON
"parameters": {
    "storageAccountKey": {
        "reference": {
            "keyVault": {
                "id":"/subscriptions/<subscriptionID>/resourceGroups/<resourceGroupName>/providers/Microsoft.KeyVault/vaults/<keyVaultName>",
             },
            "secretName": "<secretName>"
           },
       },
       ...
}
```

> [!NOTE]
> <span data-ttu-id="37471-158">Attualmente l'esportazione di modelli per le data factory esistenti non è ancora supportata, ma è in via di realizzazione.</span><span class="sxs-lookup"><span data-stu-id="37471-158">While exporting templates for existing data factories is currently not yet supported, it is in the works.</span></span>
>
>
