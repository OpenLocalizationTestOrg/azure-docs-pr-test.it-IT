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
# <a name="use-templates-toocreate-azure-data-factory-entities"></a>Utilizzare le entità di Azure Data Factory toocreate modelli
## <a name="overview"></a>Panoramica
Durante l'utilizzo di Azure Data Factory per le esigenze di integrazione di dati, potrebbe essere necessario riutilizzare hello stesso modello tra ambienti diversi o implementazione hello stessa attività ripetutamente all'interno di hello stessa soluzione. I modelli consentono di implementare e gestire questi scenari in modo semplificato. I modelli di Azure Data Factory rappresentano la soluzione ideale per gli scenari che implicano riusabilità e ripetizione.

Si consideri la situazione hello in un'organizzazione ha 10 impianti di produzione in HelloWorld. i log di Hello da ogni pianta vengono archiviati in un database di SQL Server locale separato. società Hello richiede un unico data warehouse nel cloud hello toobuild per analitica ad hoc. Inoltre importante toohave hello stessa logica ma configurazioni diverse per gli ambienti di sviluppo, test e produzione.

In questo caso, un'attività deve toobe ripetuto all'interno dello stesso ambiente hello, ma con valori diversi in hello 10 data factory per ogni impianto di produzione. In effetti, l'elemento della **ripetizione** è presente. Applicazione di modelli consente di astrazione hello questo flusso generico (vale a dire pipeline con hello stessa attività in ogni data factory), ma utilizza un file di parametro separato per ogni impianto di produzione.

Inoltre, come hello organizzazione desidera toodeploy queste factory 10 dati volte più tra ambienti diversi, i modelli possono utilizzare questo **riusabilità** utilizzando i file di parametro separato per lo sviluppo, test, e ambienti di produzione.

## <a name="templating-with-azure-resource-manager"></a>Creazione di modelli con Azure Resource Manager
[Modelli di Azure Resource Manager](../azure-resource-manager/resource-group-overview.md#template-deployment) sono un modello di tooachieve ideale in Azure Data Factory. Modelli di gestione risorse definiscono infrastruttura hello e la configurazione della soluzione Azure tramite un file JSON. Poiché i modelli di gestione risorse di Azure funzionano con tutti/la maggior parte dei servizi di Azure, può essere utilizzato ampiamente tooeasily gestire tutte le risorse delle risorse di Azure. Vedere [modelli Authoring Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) toolearn ulteriori informazioni sugli hello in genere i modelli di gestione risorse.

## <a name="tutorials"></a>Esercitazioni
Vedere hello seguenti esercitazioni per le entità di Data Factory toocreate dettagliate tramite i modelli di gestione risorse:

* [Esercitazione: Creare una pipeline di dati toocopy utilizzando il modello di gestione risorse di Azure](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
* [Esercitazione: Creare una pipeline di dati tooprocess utilizzando il modello di gestione risorse di Azure](data-factory-build-your-first-pipeline.md)

## <a name="data-factory-templates-on-github"></a>Modelli di data factory in GitHub
Estrarre hello seguenti modelli di avvio rapido di Azure su GitHub:

* [Creare un Data factory toocopy dati dall'archiviazione Blob di Azure tooAzure Database SQL](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-blob-to-sql-copy)
* [Create a Data factory with Hive activity on Azure HDInsight cluster](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-hive-transformation) (Creare una data factory con un'attività Hive in un cluster Azure HDInsight)
* [Creare un Data factory toocopy dati da BLOB tooAzure Salesforce](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-salesforce-to-blob-copy)
* [Creare una Data factory che raccoglie le attività: copia i dati da un server FTP tooAzure BLOB, richiama uno script hive in un su richiesta HDInsight cluster tootransform hello di dati e copia i risultati nel Database SQL di Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-data-factory-ftp-hive-blob)

È gratuito tooshare i modelli di Data Factory di Azure in [avvio rapido di Azure](https://azure.microsoft.com/documentation/templates/). Fare riferimento toohello [Guida alla collaborazione](https://github.com/Azure/azure-quickstart-templates/tree/master/1-CONTRIBUTION-GUIDE) durante lo sviluppo di modelli che possono essere condivise tramite questo repository.

Hello le sezioni seguenti fornisce informazioni dettagliate sulla definizione delle risorse di Data Factory in un modello di gestione risorse.

## <a name="defining-data-factory-resources-in-templates"></a>Definizione delle risorse di Data Factory nei modelli
modello di livello superiore per la definizione di una data factory Hello è:

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

### <a name="define-data-factory"></a>Definire una data factory
È consigliabile definire una data factory nel modello di gestione risorse di hello come illustrato nel seguente esempio hello:

```JSON
"resources": [
{
    "name": "[variables('<mydataFactoryName>')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "East US"
}
```
dataFactoryName Hello è definito in "variabili" come:

```JSON
"dataFactoryName": "[concat('<myDataFactoryName>', uniqueString(resourceGroup().id))]",
```

### <a name="define-linked-services"></a>Definire servizi collegati

```JSON
"type": "linkedservices",
"name": "[variables('<LinkedServiceName>')]",
"apiVersion": "2015-10-01",
"dependsOn": [ "[variables('<dataFactoryName>')]" ],
"properties": {
    ...
}
```

Vedere [servizio collegato di archiviazione](data-factory-azure-blob-connector.md#azure-storage-linked-service) o [servizi collegati di calcolo](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) per dettagli sulle proprietà JSON hello per il servizio collegato specifico hello desiderato toodeploy. il parametro "dependsOn" Hello Specifica nome della hello corrispondente data factory. Nel seguente definizione JSON hello è illustrato un esempio di definizione di un servizio collegato di archiviazione di Azure:

### <a name="define-datasets"></a>Definire i set di dati

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
Fare riferimento troppo[supportati archivi dati](data-factory-data-movement-activities.md#supported-data-stores-and-formats) per dettagli sulle proprietà JSON hello per il tipo di set di dati specifico hello desiderato toodeploy. Nota hello "dependsOn" parametro specifica nome di dati corrispondenti hello factory e l'archiviazione di servizio collegato. Nel seguente definizione JSON hello è illustrato un esempio di definizione di tipo di set di dati di archiviazione blob di Azure:

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

### <a name="define-pipelines"></a>Definire pipeline

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

Fare riferimento troppo[definizione di pipeline](data-factory-create-pipelines.md#pipeline-json) per ulteriori informazioni sulle proprietà JSON hello per la definizione di hello specifico della pipeline e le attività desiderate toodeploy. Nota hello "dependsOn" parametro specifica nome della data factory di hello e tutti i servizi collegati corrispondenti o i set di dati. Nel seguente frammento di codice JSON hello è illustrato un esempio di una pipeline che copia i dati da archiviazione Blob di Azure tooAzure Database SQL:

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
## <a name="parameterizing-data-factory-template"></a>Uso di parametri nel modello di Data Factory
Per le procedure consigliate sull'uso dei parametri, vedere l'articolo [Procedure consigliate per la creazione di modelli di Azure Resource Manager](../azure-resource-manager/resource-manager-template-best-practices.md#parameters). In generale l'utilizzo dei parametri deve essere ridotto al minimo, soprattutto se è possibile usare variabili anziché parametri. Fornire solo parametri in hello seguenti scenari:

* Le impostazioni variano a seconda dell'ambiente, ad esempio di sviluppo, test e produzione
* Segreti (password)

Se è necessario segreti toopull da [insieme credenziali chiavi Azure](../key-vault/key-vault-get-started.md) durante la distribuzione utilizzando i modelli di entità di Azure Data Factory, specificare hello **insieme di credenziali chiave** e **nome segreto** come illustrato Hello l'esempio seguente:

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
> Esportazione di modelli per i produttori di dati esistente non è ancora supportato, ma è in hello funziona.
>
>
