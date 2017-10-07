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
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-resource-manager-template"></a>Esercitazione: Creare la prima data factory di Azure usando il modello di Azure Resource Manager
> [!div class="op_single_selector"]
> * [Panoramica e prerequisiti](data-factory-build-your-first-pipeline.md)
> * [Portale di Azure](data-factory-build-your-first-pipeline-using-editor.md)
> * [Visual Studio](data-factory-build-your-first-pipeline-using-vs.md)
> * [PowerShell](data-factory-build-your-first-pipeline-using-powershell.md)
> * [Modello di Resource Manager](data-factory-build-your-first-pipeline-using-arm.md)
> * [API REST](data-factory-build-your-first-pipeline-using-rest-api.md)
> 
> 

In questo articolo, si utilizza un toocreate modello di gestione risorse di Azure prima data factory di Azure. esercitazione di hello toodo tramite altri strumenti/SDK, selezionare una delle opzioni di hello dall'elenco a discesa hello.

pipeline Hello in questa esercitazione è un'attività: **attività Hive di HDInsight**. Questa attività esegue uno script hive in un cluster HDInsight di Azure che trasformazioni i dati di output tooproduce di dati di input. pipeline di Hello è toorun pianificato dopo un mese tra hello specificato di ore di inizio e fine. 

> [!NOTE]
> pipeline di dati Hello in questa esercitazione Trasforma i dati di output tooproduce di dati di input. Per un'esercitazione su come dati di toocopy tramite Data Factory di Azure, vedere [esercitazione: copiare i dati da archiviazione Blob tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
> 
> pipeline di Hello in questa esercitazione contiene una sola attività di tipo: HDInsightHive. Una pipeline può includere più attività Inoltre, è possibile concatenare le due attività (eseguire un'attività dopo l'altro) mediante l'impostazione di set di dati di hello output di un'attività come hello input set di dati di hello altre attività. Per altre informazioni, vedere [Pianificazione ed esecuzione in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline). 

## <a name="prerequisites"></a>Prerequisiti
* Leggere [esercitazione Panoramica](data-factory-build-your-first-pipeline.md) articolo e hello completo **prerequisito** passaggi.
* Seguire le istruzioni [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview) articolo tooinstall versione più recente di Azure PowerShell nel computer in uso.
* Vedere [la creazione di modelli di gestione risorse di Azure](../azure-resource-manager/resource-group-authoring-templates.md) toolearn sui modelli di gestione risorse di Azure. 

## <a name="in-this-tutorial"></a>Contenuto dell'esercitazione:
| Entità | Descrizione |
| --- | --- |
| Servizio collegato Archiviazione di Azure |Collega la data factory toohello account di archiviazione di Azure. contiene account di archiviazione di Azure Hello hello dati di input e outpui per la pipeline di hello in questo esempio. |
| Servizio collegato su richiesta HDInsight |Collega una factory del dati toohello cluster HDInsight su richiesta. cluster Hello viene creato automaticamente tooprocess dati e viene eliminato al termine dell'elaborazione hello. |
| Set di dati di input del BLOB di Azure |Fa riferimento il servizio di archiviazione di Azure collegati toohello. Hello servizio collegato fa riferimento tooan account di archiviazione Azure e set di dati Blob di Azure hello specifica hello contenitore, cartella e nome file nel servizio di archiviazione che contiene i dati di input hello hello. |
| Set di dati di output del BLOB di Azure |Fa riferimento il servizio di archiviazione di Azure collegati toohello. Hello servizio collegato fa riferimento tooan account di archiviazione Azure e set di dati Blob di Azure hello specifica hello contenitore, cartella e nome file nel servizio di archiviazione che contiene i dati di output di hello hello. |
| Data Pipeline |Hello pipeline dispone di un'attività di tipo HDInsightHive, che elabora hello di un set di dati dell'input e restituisce il set di dati di hello output. |

Una data factory può comprendere una o più pipeline. Una pipeline può comprendere una o più attività. Esistono due tipi di attività: [attività di spostamento dei dati](data-factory-data-movement-activities.md) e [attività di trasformazione dei dati](data-factory-data-transformation-activities.md). In questa esercitazione si crea una pipeline con un'attività (attività Hive).

Hello nella sezione seguente fornisce hello completo Gestione risorse modello per la definizione di entità Data Factory, che è possibile eseguire rapidamente tramite modelli di hello hello esercitazione e test. toounderstand della definizione di ogni entità Data Factory, vedere [entità Data Factory nel modello hello](#data-factory-entities-in-the-template) sezione.

## <a name="data-factory-json-template"></a>Modello JSON di Data Factory
Hello modello Gestione risorse di livello superiore per la definizione di una data factory è: 

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
Creare un file JSON denominato **ADFTutorialARM.json** in **C:\ADFGetStarted** cartella con hello seguente contenuto:

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
> È possibile trovare un altro esempio del modello di Resource Manager per la creazione di una data factory di Azure in [Tutorial: Create a pipeline with Copy Activity using an Azure Resource Manager template](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md) (Esercitazione: Creare una pipeline con l'attività di copia usando un modello di Resource Manager).  
> 
> 

## <a name="parameters-json"></a>Parametri JSON
Creare un file JSON denominato **ADFTutorialARM Parameters.json** che contiene i parametri per il modello di gestione risorse di Azure hello.  

> [!IMPORTANT]
> Specificare il nome di hello e una chiave dell'account di archiviazione di Azure per hello **storageAccountName** e **storageAccountKey** parametri in questo file di parametro. 
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
> È possibile file JSON di parametro separato per lo sviluppo, test e ambienti di produzione che è possibile utilizzare con hello stesso modello di Data Factory JSON. Usando uno script di Power Shell, è possibile automatizzare la distribuzione delle entità di Data Factory in questi ambienti. 
> 
> 

## <a name="create-data-factory"></a>Creare un'istanza di Data Factory
1. Avviare **Azure PowerShell** e hello esecuzione comando seguente: 
   * Eseguire hello comando seguente e immettere nome utente hello e la password usati toosign in toohello portale di Azure.
    ```PowerShell
    Login-AzureRmAccount
    ```  
   * Eseguire hello successivo comando tooview tutte le sottoscrizioni di hello per questo account.
    ```PowerShell
    Get-AzureRmSubscription
    ``` 
   * Sottoscrizione hello tooselect da toowork con il comando seguente hello esecuzione. La sottoscrizione deve essere hello uguali a quelli hello usato nel portale di Azure hello.
    ```
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```   
2. Eseguire hello successivo comando toodeploy Data Factory le entità utilizzando il modello di gestione risorse hello creato nel passaggio 1. 

    ```PowerShell
    New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile C:\ADFGetStarted\ADFTutorialARM.json -TemplateParameterFile C:\ADFGetStarted\ADFTutorialARM-Parameters.json
    ```

## <a name="monitor-pipeline"></a>Monitorare la pipeline
1. Dopo l'accesso toohello [portale di Azure](https://portal.azure.com/), fare clic su **Sfoglia** e selezionare **Data factory**.
     ![Esplorare-&gt;Data factory](./media/data-factory-build-your-first-pipeline-using-arm/BrowseDataFactories.png)
2. In hello **Data factory** pannello, fare clic su data factory di hello (**TutorialFactoryARM**) creato.    
3. In hello **Data Factory** pannello per il data factory, fare clic su **diagramma**.

     ![Riquadro Diagramma](./media/data-factory-build-your-first-pipeline-using-arm/DiagramTile.png)
4. In hello **vista diagramma**, si visualizza una panoramica delle pipeline hello e set di dati utilizzati in questa esercitazione.
   
   ![Vista Diagramma](./media/data-factory-build-your-first-pipeline-using-arm/DiagramView.png) 
5. In vista diagramma hello, fare doppio clic sul set di dati hello **AzureBlobOutput**. Vedrai tale sezione hello che è in corso di elaborazione.
   
    ![Set di dati](./media/data-factory-build-your-first-pipeline-using-arm/AzureBlobOutput.png)
6. Quando viene eseguita l'elaborazione, vedrai sezione hello **pronto** stato. La creazione di un cluster HDInsight su richiesta di solito richiede tempo (circa 20 minuti). Pertanto, prevedere hello pipeline tootake **circa 30 minuti** tooprocess hello sezione.
   
    ![Set di dati](./media/data-factory-build-your-first-pipeline-using-arm/SliceReady.png)    
7. Quando si trova in sezione hello **pronto** stato, controllare hello **partitioneddata** cartella hello **adfgetstarted** contenitore nell'archiviazione blob per hello i dati di output.  

Vedere [monitorare set di dati e della pipeline](data-factory-monitor-manage-pipelines.md) per istruzioni su come pipeline di toouse hello pannelli portale Azure toomonitor hello e set di dati è stato creato in questa esercitazione.

È inoltre possibile utilizzare toomonitor monitorare e gestire App le pipeline di dati. Vedere [monitoraggio e la gestione delle pipeline di Data Factory di Azure utilizzando App monitoraggio](data-factory-monitor-manage-app.md) per informazioni dettagliate sull'utilizzo di un'applicazione hello. 

> [!IMPORTANT]
> file di input Hello eliminato quando la sezione hello viene elaborata correttamente. Pertanto, se si desidera toorerun hello sezione o hello esercitazione nuovamente, hello del file di input (input.log) toohello inputdata cartella del contenitore adfgetstarted hello di caricamento.
> 
> 

## <a name="data-factory-entities-in-hello-template"></a>Entità di modello hello Factory di dati
### <a name="define-data-factory"></a>Definire una data factory
È consigliabile definire una data factory nel modello di gestione risorse di hello come illustrato nel seguente esempio hello:  

```json
"resources": [
{
    "name": "[variables('dataFactoryName')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "West US"
}
```
dataFactoryName Hello è definito come: 

```json
"dataFactoryName": "[concat('HiveTransformDF', uniqueString(resourceGroup().id))]",
```
È una stringa univoca in base a hello ID gruppo di risorse.  

### <a name="defining-data-factory-entities"></a>Definizione di entità di Data factory
Hello entità Data Factory seguenti vengono definite nel modello JSON hello: 

* [Servizio collegato Archiviazione di Azure](#azure-storage-linked-service)
* [Servizio collegato su richiesta HDInsight](#hdinsight-on-demand-linked-service)
* [Set di dati di input del BLOB di Azure](#azure-blob-input-dataset)
* [Set di dati di output del BLOB di Azure](#azure-blob-output-dataset)
* [Pipeline di dati con un'attività di copia](#data-pipeline)

#### <a name="azure-storage-linked-service"></a>Servizio collegato Archiviazione di Azure
Specificare il nome di hello e chiave dell'account di archiviazione di Azure in questa sezione. Vedere [servizio collegato di archiviazione di Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service) per informazioni dettagliate su JSON proprietà utilizzate toodefine servizio collegato di archiviazione di Azure. 

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
Hello **connectionString** utilizza hello parametri storageAccountName e storageAccountKey. valori Hello per questi parametri passati mediante un file di configurazione. definizione di Hello utilizza anche variabili: azureStroageLinkedService e dataFactoryName definiti nel modello di hello. 

#### <a name="hdinsight-on-demand-linked-service"></a>Servizio collegato su richiesta HDInsight
Vedere [servizi collegati di calcolo](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) articolo per informazioni dettagliate su JSON proprietà utilizzate toodefine un servizio collegato di HDInsight su richiesta.  

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
Si noti hello seguenti punti: 

* Hello Data Factory viene creata una **basati su Linux** cluster HDInsight per l'utente con hello sopra JSON. Per i dettagli, vedere [Servizio collegato Azure HDInsight su richiesta](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) . 
* È possibile usare il **proprio cluster HDInsight** anziché un cluster HDInsight su richiesta. Per i dettagli, vedere [Servizio collegato Azure HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) .
* Crea cluster HDInsight Hello un **contenitore predefinito** nell'archiviazione blob hello specificato in JSON hello (**linkedServiceName**). HDInsight non eliminare questo contenitore quando viene eliminato il cluster hello. Questo comportamento dipende dalla progettazione. Con il servizio collegato di HDInsight su richiesta, un cluster HDInsight viene creato ogni volta che una sezione deve toobe elaborati a meno che non vi è un cluster esistente in tempo reale (**timeToLive**) e viene eliminata quando viene eseguita un'elaborazione hello.
  
    Man mano che vengono elaborate più sezioni, vengono visualizzati numerosi contenitori nell'archivio BLOB di Azure. Se non li necessario per la risoluzione dei problemi dei processi di hello, è opportuno toodelete li tooreduce hello il costo di archiviazione. i nomi di Hello di questi contenitori seguono un modello: "adf**yourdatafactoryname**-**linkedservicename**- datetimestamp". Utilizzare strumenti come [Esplora archivi Microsoft](http://storageexplorer.com/) toodelete contenitori di Azure nell'archiviazione blob.

Per i dettagli, vedere [Servizio collegato Azure HDInsight su richiesta](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) .

#### <a name="azure-blob-input-dataset"></a>Set di dati di input del BLOB di Azure
Specificare nomi di hello del contenitore blob, cartelle e file che contiene i dati di input hello. Vedere [proprietà set di dati Blob di Azure](data-factory-azure-blob-connector.md#dataset-properties) per informazioni dettagliate su JSON proprietà utilizzate toodefine un set di dati Blob di Azure. 

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
Questa definizione utilizza i seguenti parametri definiti nel modello di parametro hello: blobContainer, inputBlobFolder e inputBlobName. 

#### <a name="azure-blob-output-dataset"></a>Set di dati di output del BLOB di Azure
Specificare i nomi di hello del contenitore blob e di cartella che contiene i dati di output di hello. Vedere [proprietà set di dati Blob di Azure](data-factory-azure-blob-connector.md#dataset-properties) per informazioni dettagliate su JSON proprietà utilizzate toodefine un set di dati Blob di Azure.  

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

Questa definizione utilizza i seguenti parametri definiti nel modello di parametro hello hello: blobContainer e outputBlobFolder. 

#### <a name="data-pipeline"></a>Data Pipeline
Viene definita una pipeline che trasforma i dati eseguendo lo script Hive in un cluster HDInsight di Azure su richiesta. Vedere [JSON di Pipeline](data-factory-create-pipelines.md#pipeline-json) per le descrizioni degli elementi usati di JSON toodefine una pipeline in questo esempio. 

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

## <a name="reuse-hello-template"></a>Riutilizzare hello modello
Nell'esercitazione hello è creato un modello per la definizione di entità Data Factory e un modello per il passaggio di valori per i parametri. toouse hello stessi ambienti con toodifferent entità modello toodeploy Data Factory, creare un file di parametro per ogni ambiente e usarlo quando si distribuisce toothat ambiente.     

Esempio:  

```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Dev.json

New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Test.json

New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Production.json
```
Si noti che hello primo comando Usa il file di parametro per l'ambiente di sviluppo hello, secondo una per hello ambiente di test e una terza per ambiente di produzione hello hello.  

È inoltre possibile riutilizzare hello modello tooperform ripetuto di attività. Ad esempio, è necessario toocreate molti data factory con uno o più pipeline che implementano hello stessa logica, ma ogni data factory Usa archiviazione di Azure differente e gli account di Database SQL di Azure. In questo scenario, si usa hello stesso modello in hello stesso ambiente (sviluppo, test o produzione) con parametri diversi file toocreate data factory. 

## <a name="resource-manager-template-for-creating-a-gateway"></a>Modello di Resource Manager per la creazione di un gateway
Di seguito è riportato un modello di gestione risorse di esempio per la creazione di un gateway logico in hello nuovamente. Installare un gateway nel computer locale o macchina virtuale IaaS di Azure e registrare il gateway di hello con il servizio Data Factory tramite una chiave. Per altre informazioni vedere [Spostare dati tra origini locali e il cloud con Gateway di gestione dati](data-factory-move-data-between-onprem-and-cloud.md) .

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
Questo modello crea una data factory denominata GatewayUsingArmDF con un gateway denominato GatewayUsingARM. 

## <a name="see-also"></a>Vedere anche
| Argomento | Descrizione |
|:--- |:--- |
| [Pipeline](data-factory-create-pipelines.md) |In questo articolo consente di comprendere le pipeline e attività nella Data Factory di Azure e come toouse li tooconstruct end-to-end basato sui dati dei flussi di lavoro degli scenario o dell'azienda. |
| [Set di dati](data-factory-create-datasets.md) |Questo articolo fornisce informazioni sui set di dati in Azure Data Factory. |
| [Pianificazione ed esecuzione](data-factory-scheduling-and-execution.md) |Questo articolo illustra gli aspetti hello di pianificazione e l'esecuzione del modello di applicazione di Azure Data Factory. |
| [Monitorare e gestire le pipeline con l'app di monitoraggio](data-factory-monitor-manage-app.md) |In questo articolo viene descritto come toomonitor, gestire ed eseguire il debug pipeline utilizzando hello monitoraggio e gestione delle App. |

