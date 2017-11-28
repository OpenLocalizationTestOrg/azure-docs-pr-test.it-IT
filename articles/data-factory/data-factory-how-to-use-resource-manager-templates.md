---
title: modelli di gestione risorse aaaUse in Data Factory | Documenti Microsoft
description: "Informazioni su come toocreate entità e di utilizzare Gestione risorse di Azure modelli toocreate Data Factory."
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
ms.openlocfilehash: 60d5dbd29494420006aed6d5bd9a10a63c36bec3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-templates-toocreate-azure-data-factory-entities"></a><span data-ttu-id="c80c1-103">Utilizzare le entità di Azure Data Factory toocreate modelli</span><span class="sxs-lookup"><span data-stu-id="c80c1-103">Use templates toocreate Azure Data Factory entities</span></span>
## <a name="overview"></a><span data-ttu-id="c80c1-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="c80c1-104">Overview</span></span>
<span data-ttu-id="c80c1-105">Durante l'utilizzo di Azure Data Factory per le esigenze di integrazione di dati, potrebbe essere necessario riutilizzare hello stesso modello tra ambienti diversi o implementazione hello stessa attività ripetutamente all'interno di hello stessa soluzione.</span><span class="sxs-lookup"><span data-stu-id="c80c1-105">While using Azure Data Factory for your data integration needs, you may find yourself reusing hello same pattern across different environments or implementing hello same task repetitively within hello same solution.</span></span> <span data-ttu-id="c80c1-106">I modelli consentono di implementare e gestire questi scenari in modo semplificato.</span><span class="sxs-lookup"><span data-stu-id="c80c1-106">Templates help you implement and manage these scenarios in an easy manner.</span></span> <span data-ttu-id="c80c1-107">I modelli di Azure Data Factory rappresentano la soluzione ideale per gli scenari che implicano riusabilità e ripetizione.</span><span class="sxs-lookup"><span data-stu-id="c80c1-107">Templates in Azure Data Factory are ideal for scenarios that involve reusability and repetition.</span></span>

<span data-ttu-id="c80c1-108">Si consideri la situazione hello in un'organizzazione ha 10 impianti di produzione in HelloWorld.</span><span class="sxs-lookup"><span data-stu-id="c80c1-108">Consider hello situation where an organization has 10 manufacturing plants across hello world.</span></span> <span data-ttu-id="c80c1-109">i log di Hello da ogni pianta vengono archiviati in un database di SQL Server locale separato.</span><span class="sxs-lookup"><span data-stu-id="c80c1-109">hello logs from each plant are stored in a separate on-premises SQL Server database.</span></span> <span data-ttu-id="c80c1-110">società Hello richiede un unico data warehouse nel cloud hello toobuild per analitica ad hoc.</span><span class="sxs-lookup"><span data-stu-id="c80c1-110">hello company wants toobuild a single data warehouse in hello cloud for ad-hoc analytics.</span></span> <span data-ttu-id="c80c1-111">Inoltre importante toohave hello stessa logica ma configurazioni diverse per gli ambienti di sviluppo, test e produzione.</span><span class="sxs-lookup"><span data-stu-id="c80c1-111">It also wants toohave hello same logic but different configurations for development, test, and production environments.</span></span>

<span data-ttu-id="c80c1-112">In questo caso, un'attività deve toobe ripetuto all'interno dello stesso ambiente hello, ma con valori diversi in hello 10 data factory per ogni impianto di produzione.</span><span class="sxs-lookup"><span data-stu-id="c80c1-112">In this case, a task needs toobe repeated within hello same environment, but with different values across hello 10 data factories for each manufacturing plant.</span></span> <span data-ttu-id="c80c1-113">In effetti, l'elemento della **ripetizione** è presente.</span><span class="sxs-lookup"><span data-stu-id="c80c1-113">In effect, **repetition** is present.</span></span> <span data-ttu-id="c80c1-114">Applicazione di modelli consente di astrazione hello questo flusso generico (vale a dire pipeline con hello stessa attività in ogni data factory), ma utilizza un file di parametro separato per ogni impianto di produzione.</span><span class="sxs-lookup"><span data-stu-id="c80c1-114">Templating allows hello abstraction of this generic flow (that is, pipelines having hello same activities in each data factory), but uses a separate parameter file for each manufacturing plant.</span></span>

<span data-ttu-id="c80c1-115">Inoltre, come hello organizzazione desidera toodeploy queste factory 10 dati volte più tra ambienti diversi, i modelli possono utilizzare questo **riusabilità** utilizzando i file di parametro separato per lo sviluppo, test, e ambienti di produzione.</span><span class="sxs-lookup"><span data-stu-id="c80c1-115">Furthermore, as hello organization wants toodeploy these 10 data factories multiple times across different environments, templates can use this **reusability** by utilizing separate parameter files for development, test, and production environments.</span></span>

## <a name="templating-with-azure-resource-manager"></a><span data-ttu-id="c80c1-116">Creazione di modelli con Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c80c1-116">Templating with Azure Resource Manager</span></span>
<span data-ttu-id="c80c1-117">[Modelli di Azure Resource Manager](../azure-resource-manager/resource-group-overview.md#template-deployment) sono un modello di tooachieve ideale in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="c80c1-117">[Azure Resource Manager templates](../azure-resource-manager/resource-group-overview.md#template-deployment) are a great way tooachieve templating in Azure Data Factory.</span></span> <span data-ttu-id="c80c1-118">Modelli di gestione risorse definiscono infrastruttura hello e la configurazione della soluzione Azure tramite un file JSON.</span><span class="sxs-lookup"><span data-stu-id="c80c1-118">Resource Manager templates define hello infrastructure and configuration of your Azure solution through a JSON file.</span></span> <span data-ttu-id="c80c1-119">Poiché i modelli di gestione risorse di Azure funzionano con tutti/la maggior parte dei servizi di Azure, può essere utilizzato ampiamente tooeasily gestire tutte le risorse delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="c80c1-119">Because Azure Resource Manager templates work with all/most Azure services, it can be widely used tooeasily manage all resources of your Azure assets.</span></span> <span data-ttu-id="c80c1-120">Vedere [modelli Authoring Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) toolearn ulteriori informazioni sugli hello in genere i modelli di gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="c80c1-120">See [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md) toolearn more about hello Resource Manager Templates in general.</span></span>

## <a name="tutorials"></a><span data-ttu-id="c80c1-121">Esercitazioni</span><span class="sxs-lookup"><span data-stu-id="c80c1-121">Tutorials</span></span>
<span data-ttu-id="c80c1-122">Vedere hello seguenti esercitazioni per le entità di Data Factory toocreate dettagliate tramite i modelli di gestione risorse:</span><span class="sxs-lookup"><span data-stu-id="c80c1-122">See hello following tutorials for step-by-step instructions toocreate Data Factory entities by using Resource Manager templates:</span></span>

* [<span data-ttu-id="c80c1-123">Esercitazione: Creare una pipeline di dati toocopy utilizzando il modello di gestione risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="c80c1-123">Tutorial: Create a pipeline toocopy data by using Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
* [<span data-ttu-id="c80c1-124">Esercitazione: Creare una pipeline di dati tooprocess utilizzando il modello di gestione risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="c80c1-124">Tutorial: Create a pipeline tooprocess data by using Azure Resource Manager template</span></span>](data-factory-build-your-first-pipeline.md)

## <a name="data-factory-templates-on-github"></a><span data-ttu-id="c80c1-125">Modelli di data factory in GitHub</span><span class="sxs-lookup"><span data-stu-id="c80c1-125">Data Factory templates on GitHub</span></span>
<span data-ttu-id="c80c1-126">Estrarre hello seguenti modelli di avvio rapido di Azure su GitHub:</span><span class="sxs-lookup"><span data-stu-id="c80c1-126">Check out hello following Azure quick start templates on GitHub:</span></span>

* [<span data-ttu-id="c80c1-127">Creare un Data factory toocopy dati dall'archiviazione Blob di Azure tooAzure Database SQL</span><span class="sxs-lookup"><span data-stu-id="c80c1-127">Create a Data factory toocopy data from Azure Blob Storage tooAzure SQL Database</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-blob-to-sql-copy)
* <span data-ttu-id="c80c1-128">[Create a Data factory with Hive activity on Azure HDInsight cluster](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-hive-transformation) (Creare una data factory con un'attività Hive in un cluster Azure HDInsight)</span><span class="sxs-lookup"><span data-stu-id="c80c1-128">[Create a Data factory with Hive activity on Azure HDInsight cluster](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-hive-transformation)</span></span>
* [<span data-ttu-id="c80c1-129">Creare un Data factory toocopy dati da BLOB tooAzure Salesforce</span><span class="sxs-lookup"><span data-stu-id="c80c1-129">Create a Data factory toocopy data from Salesforce tooAzure Blobs</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-salesforce-to-blob-copy)
* [<span data-ttu-id="c80c1-130">Creare una Data factory che raccoglie le attività: copia i dati da un server FTP tooAzure BLOB, richiama uno script hive in un su richiesta HDInsight cluster tootransform hello di dati e copia i risultati nel Database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="c80c1-130">Create a Data factory that chains activities: copies data from an FTP server tooAzure Blobs, invokes a hive script on an on-demand HDInsight cluster tootransform hello data, and copies result into Azure SQL Database</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-data-factory-ftp-hive-blob)

<span data-ttu-id="c80c1-131">È gratuito tooshare i modelli di Data Factory di Azure in [avvio rapido di Azure](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="c80c1-131">Feel free tooshare your Azure Data Factory templates at [Azure Quick start](https://azure.microsoft.com/documentation/templates/).</span></span> <span data-ttu-id="c80c1-132">Fare riferimento toohello [Guida alla collaborazione](https://github.com/Azure/azure-quickstart-templates/tree/master/1-CONTRIBUTION-GUIDE) durante lo sviluppo di modelli che possono essere condivise tramite questo repository.</span><span class="sxs-lookup"><span data-stu-id="c80c1-132">Refer toohello [contribution guide](https://github.com/Azure/azure-quickstart-templates/tree/master/1-CONTRIBUTION-GUIDE) while developing templates that can be shared via this repository.</span></span>

<span data-ttu-id="c80c1-133">Hello le sezioni seguenti fornisce informazioni dettagliate sulla definizione delle risorse di Data Factory in un modello di gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="c80c1-133">hello following sections provide details about defining Data Factory resources in a Resource Manager template.</span></span>

## <a name="defining-data-factory-resources-in-templates"></a><span data-ttu-id="c80c1-134">Definizione delle risorse di Data Factory nei modelli</span><span class="sxs-lookup"><span data-stu-id="c80c1-134">Defining Data Factory resources in templates</span></span>
<span data-ttu-id="c80c1-135">modello di livello superiore per la definizione di una data factory Hello è:</span><span class="sxs-lookup"><span data-stu-id="c80c1-135">hello top-level template for defining a data factory is:</span></span>

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

### <a name="define-data-factory"></a><span data-ttu-id="c80c1-136">Definire una data factory</span><span class="sxs-lookup"><span data-stu-id="c80c1-136">Define data factory</span></span>
<span data-ttu-id="c80c1-137">È consigliabile definire una data factory nel modello di gestione risorse di hello come illustrato nel seguente esempio hello:</span><span class="sxs-lookup"><span data-stu-id="c80c1-137">You define a data factory in hello Resource Manager template as shown in hello following sample:</span></span>

```JSON
"resources": [
{
    "name": "[variables('<mydataFactoryName>')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "East US"
}
```
<span data-ttu-id="c80c1-138">dataFactoryName Hello è definito in "variabili" come:</span><span class="sxs-lookup"><span data-stu-id="c80c1-138">hello dataFactoryName is defined in “variables” as:</span></span>

```JSON
"dataFactoryName": "[concat('<myDataFactoryName>', uniqueString(resourceGroup().id))]",
```

### <a name="define-linked-services"></a><span data-ttu-id="c80c1-139">Definire servizi collegati</span><span class="sxs-lookup"><span data-stu-id="c80c1-139">Define linked services</span></span>

```JSON
"type": "linkedservices",
"name": "[variables('<LinkedServiceName>')]",
"apiVersion": "2015-10-01",
"dependsOn": [ "[variables('<dataFactoryName>')]" ],
"properties": {
    ...
}
```

<span data-ttu-id="c80c1-140">Vedere [servizio collegato di archiviazione](data-factory-azure-blob-connector.md#azure-storage-linked-service) o [servizi collegati di calcolo](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) per dettagli sulle proprietà JSON hello per il servizio collegato specifico hello desiderato toodeploy.</span><span class="sxs-lookup"><span data-stu-id="c80c1-140">See [Storage Linked Service](data-factory-azure-blob-connector.md#azure-storage-linked-service) or [Compute Linked Services](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details about hello JSON properties for hello specific linked service you wish toodeploy.</span></span> <span data-ttu-id="c80c1-141">il parametro "dependsOn" Hello Specifica nome della hello corrispondente data factory.</span><span class="sxs-lookup"><span data-stu-id="c80c1-141">hello “dependsOn” parameter specifies name of hello corresponding data factory.</span></span> <span data-ttu-id="c80c1-142">Nel seguente definizione JSON hello è illustrato un esempio di definizione di un servizio collegato di archiviazione di Azure:</span><span class="sxs-lookup"><span data-stu-id="c80c1-142">An example of defining a linked service for Azure Storage is shown in hello following JSON definition:</span></span>

### <a name="define-datasets"></a><span data-ttu-id="c80c1-143">Definire i set di dati</span><span class="sxs-lookup"><span data-stu-id="c80c1-143">Define datasets</span></span>

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
<span data-ttu-id="c80c1-144">Fare riferimento troppo[supportati archivi dati](data-factory-data-movement-activities.md#supported-data-stores-and-formats) per dettagli sulle proprietà JSON hello per il tipo di set di dati specifico hello desiderato toodeploy.</span><span class="sxs-lookup"><span data-stu-id="c80c1-144">Refer too[Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) for details about hello JSON properties for hello specific dataset type you wish toodeploy.</span></span> <span data-ttu-id="c80c1-145">Nota hello "dependsOn" parametro specifica nome di dati corrispondenti hello factory e l'archiviazione di servizio collegato.</span><span class="sxs-lookup"><span data-stu-id="c80c1-145">Note hello “dependsOn” parameter specifies name of hello corresponding data factory and storage linked service.</span></span> <span data-ttu-id="c80c1-146">Nel seguente definizione JSON hello è illustrato un esempio di definizione di tipo di set di dati di archiviazione blob di Azure:</span><span class="sxs-lookup"><span data-stu-id="c80c1-146">An example of defining dataset type of Azure blob storage is shown in hello following JSON definition:</span></span>

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

### <a name="define-pipelines"></a><span data-ttu-id="c80c1-147">Definire pipeline</span><span class="sxs-lookup"><span data-stu-id="c80c1-147">Define pipelines</span></span>

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

<span data-ttu-id="c80c1-148">Fare riferimento troppo[definizione di pipeline](data-factory-create-pipelines.md#pipeline-json) per ulteriori informazioni sulle proprietà JSON hello per la definizione di hello specifico della pipeline e le attività desiderate toodeploy.</span><span class="sxs-lookup"><span data-stu-id="c80c1-148">Refer too[defining pipelines](data-factory-create-pipelines.md#pipeline-json) for details about hello JSON properties for defining hello specific pipeline and activities you wish toodeploy.</span></span> <span data-ttu-id="c80c1-149">Nota hello "dependsOn" parametro specifica nome della data factory di hello e tutti i servizi collegati corrispondenti o i set di dati.</span><span class="sxs-lookup"><span data-stu-id="c80c1-149">Note hello “dependsOn” parameter specifies name of hello data factory, and any corresponding linked services or datasets.</span></span> <span data-ttu-id="c80c1-150">Nel seguente frammento di codice JSON hello è illustrato un esempio di una pipeline che copia i dati da archiviazione Blob di Azure tooAzure Database SQL:</span><span class="sxs-lookup"><span data-stu-id="c80c1-150">An example of a pipeline that copies data from Azure Blob Storage tooAzure SQL Database is shown in hello following JSON snippet:</span></span>

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
    "start": "2016-10-03T00:00:00Z",
    "end": "2016-10-04T00:00:00Z"
}
```
## <a name="parameterizing-data-factory-template"></a><span data-ttu-id="c80c1-151">Uso di parametri nel modello di Data Factory</span><span class="sxs-lookup"><span data-stu-id="c80c1-151">Parameterizing Data Factory template</span></span>
<span data-ttu-id="c80c1-152">Per le procedure consigliate sull'uso dei parametri, vedere l'articolo [Procedure consigliate per la creazione di modelli di Azure Resource Manager](../azure-resource-manager/resource-manager-template-best-practices.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="c80c1-152">For best practices on parameterizing, see [Best practices for creating Azure Resource Manager templates](../azure-resource-manager/resource-manager-template-best-practices.md#parameters) article.</span></span> <span data-ttu-id="c80c1-153">In generale l'utilizzo dei parametri deve essere ridotto al minimo, soprattutto se è possibile usare variabili anziché parametri.</span><span class="sxs-lookup"><span data-stu-id="c80c1-153">In general, parameter usage should be minimized, especially if variables can be used instead.</span></span> <span data-ttu-id="c80c1-154">Fornire solo parametri in hello seguenti scenari:</span><span class="sxs-lookup"><span data-stu-id="c80c1-154">Only provide parameters in hello following scenarios:</span></span>

* <span data-ttu-id="c80c1-155">Le impostazioni variano a seconda dell'ambiente, ad esempio di sviluppo, test e produzione</span><span class="sxs-lookup"><span data-stu-id="c80c1-155">Settings vary by environment (example: development, test, and production)</span></span>
* <span data-ttu-id="c80c1-156">Segreti (password)</span><span class="sxs-lookup"><span data-stu-id="c80c1-156">Secrets (such as passwords)</span></span>

<span data-ttu-id="c80c1-157">Se è necessario segreti toopull da [insieme credenziali chiavi Azure](../key-vault/key-vault-get-started.md) durante la distribuzione utilizzando i modelli di entità di Azure Data Factory, specificare hello **insieme di credenziali chiave** e **nome segreto** come illustrato Hello l'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="c80c1-157">If you need toopull secrets from [Azure Key Vault](../key-vault/key-vault-get-started.md) when deploying Azure Data Factory entities using templates, specify hello **key vault** and **secret name** as shown in hello following example:</span></span>

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
> <span data-ttu-id="c80c1-158">Esportazione di modelli per i produttori di dati esistente non è ancora supportato, ma è in hello funziona.</span><span class="sxs-lookup"><span data-stu-id="c80c1-158">While exporting templates for existing data factories is currently not yet supported, it is in hello works.</span></span>
>
>
