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
ms.date: 01/22/2018
ms.author: spelluru
robots: noindex
ms.openlocfilehash: 7ac85285b036aec7d0e3e1b23b8cec26886f1e3c
ms.sourcegitcommit: 9cc3d9b9c36e4c973dd9c9028361af1ec5d29910
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/23/2018
---
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-resource-manager-template"></a>Esercitazione: Creare la prima data factory di Azure usando il modello di Azure Resource Manager
> [!div class="op_single_selector"]
> * [Panoramica e prerequisiti](data-factory-build-your-first-pipeline.md)
> * [Azure portal](data-factory-build-your-first-pipeline-using-editor.md)
> * [Visual Studio](data-factory-build-your-first-pipeline-using-vs.md)
> * [PowerShell](data-factory-build-your-first-pipeline-using-powershell.md)
> * [Modello di Resource Manager](data-factory-build-your-first-pipeline-using-arm.md)
> * [API REST](data-factory-build-your-first-pipeline-using-rest-api.md)
> 
 
> [!NOTE]
> Questo articolo si applica alla versione 1 del servizio Data Factory, disponibile a livello generale (GA). Se si usa la versione 2 del servizio Data Factory, disponibile in anteprima, vedere la [guida introduttiva per la creazione di una data factory con Azure Data Factory versione 2](../quickstart-create-data-factory-dot-net.md).

In questo articolo viene usato un modello di Azure Resource Manager per creare la prima data factory di Azure. Per eseguire l'esercitazione usando altri strumenti/SDK, selezionare una delle opzioni dall'elenco a discesa.

La pipeline in questa esercitazione include un'attività, l'**attività Hive di HDInsight**, che esegue uno script Hive in un cluster Azure HDInsight per trasformare i dati di input e generare i dati di output. L'esecuzione della pipeline è pianificata una volta al mese tra le ore di inizio e di fine specificate. 

> [!NOTE]
> La pipeline di dati in questa esercitazione trasforma i dati di input per produrre dati di output. Per un'esercitazione su come copiare dati usando Azure Data Factory, vedere [Copiare dati da un archivio BLOB al database SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
> 
> La pipeline in questa esercitazione include solo un'attività di tipo HDInsightHive. Una pipeline può includere più attività ed è possibile concatenarne due, ovvero eseguire un'attività dopo l'altra, impostando il set di dati di output di un'attività come set di dati di input dell'altra. Per altre informazioni, vedere [Pianificazione ed esecuzione in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline). 

## <a name="prerequisites"></a>prerequisiti
* Vedere la [panoramica dell'esercitazione](data-factory-build-your-first-pipeline.md) ed eseguire i passaggi relativi ai **prerequisiti** .
* Seguire le istruzioni disponibili nell'articolo [Come installare e configurare Azure PowerShell](/powershell/azure/overview) per installare la versione più recente di Azure PowerShell nel computer.
* Per informazioni sulla creazione di modelli di Azure Resource Manager, vedere [Creazione di modelli di Azure Resource Manager](../../azure-resource-manager/resource-group-authoring-templates.md) . 

## <a name="in-this-tutorial"></a>Contenuto dell'esercitazione:
| Entità | DESCRIZIONE |
| --- | --- |
| Servizio collegato Archiviazione di Azure |Collega l'account di archiviazione di Azure alla data factory. In questo esempio l'account di archiviazione di Azure contiene i dati di input e di output per la pipeline. |
| Servizio collegato su richiesta HDInsight |Collega un cluster HDInsight su richiesta alla data factory. Il cluster viene creato automaticamente per elaborare i dati e viene eliminato al termine dell'elaborazione. |
| Set di dati di input del BLOB di Azure |Fa riferimento al servizio collegato di archiviazione di Azure. Il servizio collegato fa riferimento a un account di archiviazione di Azure e il set di dati del BLOB di Azure specifica il contenitore, la cartella e il nome del file nella risorsa di archiviazione che contiene i dati di input. |
| Set di dati di output del BLOB di Azure |Fa riferimento al servizio collegato di archiviazione di Azure. Il servizio collegato fa riferimento a un account di archiviazione di Azure e il set di dati del BLOB di Azure specifica il contenitore, la cartella e il nome del file nella risorsa di archiviazione che contiene i dati di output. |
| Data Pipeline |La pipeline ha un'attività di tipo HDInsightHive che utilizza il set di dati di input e produce il set di dati di output. |

Una data factory può comprendere una o più pipeline. Una pipeline può comprendere una o più attività. Esistono due tipi di attività: [attività di spostamento dei dati](data-factory-data-movement-activities.md) e [attività di trasformazione dei dati](data-factory-data-transformation-activities.md). In questa esercitazione si crea una pipeline con un'attività (attività Hive).

La sezione seguente contiene il modello di Resource Manager completo per la definizione di entità di Data Factory. In questo modo sarà possibile eseguire rapidamente l'esercitazione e testare il modello. Per conoscere come viene definita ogni entità di Data Factory, vedere la sezione [Entità di Data Factory nel modello](#data-factory-entities-in-the-template).

## <a name="data-factory-json-template"></a>Modello JSON di Data Factory
Il modello di Resource Manager principale per la definizione di una data factory è il seguente: 

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
Creare un file JSON denominato **ADFTutorialARM.json** nella cartella **C:\ADFGetStarted** con il contenuto seguente:

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
> È possibile trovare un altro esempio del modello di Resource Manager per la creazione di una data factory di Azure in [Tutorial: Create a pipeline with Copy Activity using an Azure Resource Manager template](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md) (Esercitazione: Creare una pipeline con l'attività di copia usando un modello di Resource Manager).  
> 
> 

## <a name="parameters-json"></a>Parametri JSON
Creare un file JSON denominato **ADFTutorialARM-Parameters.json** contenente i parametri per il modello di Azure Resource Manager.  

> [!IMPORTANT]
> Specificare il nome e la chiave dell'account di archiviazione di Azure per i parametri **storageAccountName** e **storageAccountKey** in questo file dei parametri. 
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
> Si possono avere file JSON di parametri separati per gli ambienti di sviluppo, test e produzione che è possibile usare con lo stesso modello JSON di Data Factory. Usando uno script di Power Shell, è possibile automatizzare la distribuzione delle entità di Data Factory in questi ambienti. 
> 
> 

## <a name="create-data-factory"></a>Creare un'istanza di Data Factory
1. Avviare **Azure PowerShell** ed eseguire questo comando: 
   * Eseguire il comando seguente e immettere il nome utente e la password usati per accedere al portale di Azure.
    ```PowerShell
    Login-AzureRmAccount
    ```  
   * Eseguire il comando seguente per visualizzare tutte le sottoscrizioni per l'account.
    ```PowerShell
    Get-AzureRmSubscription
    ``` 
   * Eseguire il comando seguente per selezionare la sottoscrizione da usare. La sottoscrizione deve corrispondere a quella usata nel portale di Azure.
    ```
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```   
2. Eseguire il comando seguente per distribuire entità di Data Factory usando il modello di Resource Manager creato nel Passaggio 1. 

    ```PowerShell
    New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile C:\ADFGetStarted\ADFTutorialARM.json -TemplateParameterFile C:\ADFGetStarted\ADFTutorialARM-Parameters.json
    ```

## <a name="monitor-pipeline"></a>Monitorare la pipeline
1. Dopo l'accesso al [portale di Azure](https://portal.azure.com/) fare clic su **Esplora** e selezionare **Data factory**.
     ![Esplorare-&gt;Data factory](./media/data-factory-build-your-first-pipeline-using-arm/BrowseDataFactories.png)
2. Nel pannello **Data factory** fare clic sulla data factory **TutorialFactoryARM** creata.    
3. Nel pannello **Data factory** relativo alla data factory scelta fare clic su **Diagramma**.

     ![Riquadro Diagramma](./media/data-factory-build-your-first-pipeline-using-arm/DiagramTile.png)
4. In **Vista diagramma**saranno visualizzati una panoramica delle pipeline e i set di dati usati in questa esercitazione.
   
   ![Vista diagramma](./media/data-factory-build-your-first-pipeline-using-arm/DiagramView.png) 
5. In Vista diagramma fare doppio clic sul set di dati **AzureBlobOutput**. Viene visualizzata la sezione in fase di elaborazione.
   
    ![Set di dati](./media/data-factory-build-your-first-pipeline-using-arm/AzureBlobOutput.png)
6. Al termine dell'elaborazione lo stato della sezione è **Pronta** . La creazione di un cluster HDInsight su richiesta di solito richiede tempo (circa 20 minuti). Di conseguenza, prevedere **circa 30 minuti** per l'elaborazione della sezione nella pipeline.
   
    ![Set di dati](./media/data-factory-build-your-first-pipeline-using-arm/SliceReady.png)    
7. Quando lo stato della sezione è **Pronto**, cercare i dati di output nella cartella **partitioneddata** del contenitore **adfgetstarted** nell'archivio BLOB.  

Per istruzioni su come usare i pannelli del portale di Azure per monitorare la pipeline e i set di dati creati in questa esercitazione, vedere [Monitorare e gestire le pipeline di Azure Data Factory](data-factory-monitor-manage-pipelines.md) .

È anche possibile usare l'app di monitoraggio e gestione per monitorare le pipeline di dati. Per i dettagli sull'uso dell'applicazione, vedere [Monitorare e gestire le pipeline di Azure Data Factory con la nuova app di monitoraggio e gestione](data-factory-monitor-manage-app.md) . 

> [!IMPORTANT]
> Il file di input viene eliminato quando la sezione viene elaborata correttamente. Per eseguire di nuovo la sezione o ripetere l'esercitazione, caricare quindi il file di input (input.log) nella cartella inputdata del contenitore adfgetstarted.
> 
> 

## <a name="data-factory-entities-in-the-template"></a>Entità di Data Factory nel modello
### <a name="define-data-factory"></a>Definire una data factory
È possibile definire una data factory nel modello di Resource Manager come illustrato nell'esempio seguente:  

```json
"resources": [
{
    "name": "[variables('dataFactoryName')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "West US"
}
```
Il valore dataFactoryName viene definito come segue: 

```json
"dataFactoryName": "[concat('HiveTransformDF', uniqueString(resourceGroup().id))]",
```
È una stringa univoca basata sull'ID del gruppo di risorse.  

### <a name="defining-data-factory-entities"></a>Definizione di entità di Data factory
Le entità di Data Factory seguenti vengono definite nel modello JSON: 

* [Servizio collegato Archiviazione di Azure](#azure-storage-linked-service)
* [Servizio collegato su richiesta HDInsight](#hdinsight-on-demand-linked-service)
* [Set di dati di input del BLOB di Azure](#azure-blob-input-dataset)
* [Set di dati di output del BLOB di Azure](#azure-blob-output-dataset)
* [Pipeline di dati con un'attività di copia](#data-pipeline)

#### <a name="azure-storage-linked-service"></a>Servizio collegato Archiviazione di Azure
In questa sezione si specificano il nome e la chiave dell'account di archiviazione di Azure. Per informazioni dettagliate sulle proprietà JSON usate per definire un servizio collegato di Archiviazione di Azure, vedere [Servizio collegato Archiviazione di Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service). 

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
**connectionString** usa i parametri storageAccountName e storageAccountKey. I valori per questi parametri sono stati passati usando un file di configurazione. La definizione usa anche le variabili azureStroageLinkedService e dataFactoryName definite nel modello. 

#### <a name="hdinsight-on-demand-linked-service"></a>Servizio collegato su richiesta HDInsight
Per informazioni dettagliate sulle proprietà JSON usate per definire un servizio collegato su richiesta HDInsight, vedere [Servizi collegati di calcolo](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).  

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
Tenere presente quanto segue: 

* Data Factory crea automaticamente un cluster HDInsight **basato su Linux** con il codice JSON precedente. Per i dettagli, vedere [Servizio collegato Azure HDInsight su richiesta](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) . 
* È possibile usare il **proprio cluster HDInsight** anziché un cluster HDInsight su richiesta. Per i dettagli, vedere [Servizio collegato Azure HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) .
* Il cluster HDInsight crea un **contenitore predefinito** nell'archivio BLOB specificato nel file JSON (**linkedServiceName**). HDInsight non elimina il contenitore quando viene eliminato il cluster. Questo comportamento dipende dalla progettazione. Con il servizio collegato HDInsight su richiesta, viene creato un cluster HDInsight ogni volta che è necessario elaborare una sezione, a meno che non esista un cluster attivo (**timeToLive**) che viene eliminato al termine dell'elaborazione.
  
    Man mano che vengono elaborate più sezioni, vengono visualizzati numerosi contenitori nell'archivio BLOB di Azure. Se non sono necessari per risolvere i problemi relativi ai processi, è possibile eliminarli per ridurre i costi di archiviazione. I nomi dei contenitori seguono questo schema: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp". Per eliminare i contenitori nell'archivio BLOB di Azure, usare strumenti come [Microsoft Azure Storage Explorer](http://storageexplorer.com/) .

Per i dettagli, vedere [Servizio collegato Azure HDInsight su richiesta](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) .

#### <a name="azure-blob-input-dataset"></a>Set di dati di input del BLOB di Azure
Vengono specificati i nomi del contenitore BLOB, della cartella e del file contenente i dati di input. Per informazioni dettagliate sulle proprietà JSON usate per definire un set di dati del BLOB di Azure, vedere [Proprietà del set di dati del BLOB di Azure](data-factory-azure-blob-connector.md#dataset-properties). 

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
Questa definizione usa i parametri seguenti definiti nel modello di parametro: blobContainer, inputBlobFolder e inputBlobName. 

#### <a name="azure-blob-output-dataset"></a>Set di dati di output del BLOB di Azure
Vengono specificati i nomi del contenitore BLOB e della cartella che contiene i dati di output. Per informazioni dettagliate sulle proprietà JSON usate per definire un set di dati del BLOB di Azure, vedere [Proprietà del set di dati del BLOB di Azure](data-factory-azure-blob-connector.md#dataset-properties).  

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

Questa definizione usa i parametri seguenti definiti nel modello di parametro: blobContainer e outputBlobFolder. 

#### <a name="data-pipeline"></a>Data Pipeline
Viene definita una pipeline che trasforma i dati eseguendo lo script Hive in un cluster HDInsight di Azure su richiesta. Per le descrizioni degli elementi JSON usati per definire una pipeline in questo esempio, vedere [Pipeline JSON](data-factory-create-pipelines.md#pipeline-json). 

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

## <a name="reuse-the-template"></a>Riutilizzare il modello
Nell'esercitazione sono stati creati un modello per definire le entità di Data Factory e un modello per passare i valori dei parametri. Per usare lo stesso modello per distribuire le entità di Data Factory in ambienti diversi, si crea un file dei parametri per ogni ambiente e lo si usa durante la distribuzione in tale ambiente.     

Esempio:  

```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Dev.json

New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Test.json

New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Production.json
```
Si noti che il primo comando usa il file dei parametri per l'ambiente di sviluppo, il secondo per l'ambiente di test e il terzo per l'ambiente di produzione.  

È anche possibile riutilizzare il modello per eseguire attività ripetute. Ad esempio, è necessario creare più data factory con una o più pipeline che implementano la stessa logica, ma ogni data factory usa account di archiviazione di Azure e di database SQL di Azure diversi. In questo scenario si usa lo stesso modello nello stesso ambiente (sviluppo, test o produzione) con file dei parametri diversi per creare le data factory. 

## <a name="resource-manager-template-for-creating-a-gateway"></a>Modello di Resource Manager per la creazione di un gateway
Di seguito è disponibile un modello di Resource Manager per la creazione di un gateway logico nel back-end. Installare un gateway nel computer locale o nella VM IaaS di Azure e registrare il gateway con il servizio Data Factory usando una chiave. Per altre informazioni vedere [Spostare dati tra origini locali e il cloud con Gateway di gestione dati](data-factory-move-data-between-onprem-and-cloud.md) .

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
| Argomento | DESCRIZIONE |
|:--- |:--- |
| [Pipeline](data-factory-create-pipelines.md) |Questo articolo fornisce informazioni sulle pipeline e sulle attività in Azure Data Factory e su come usarle per costruire flussi di lavoro end-to-end basati sui dati per lo scenario o l'azienda. |
| [Set di dati](data-factory-create-datasets.md) |Questo articolo fornisce informazioni sui set di dati in Azure Data Factory. |
| [Pianificazione ed esecuzione](data-factory-scheduling-and-execution.md) |Questo articolo descrive gli aspetti di pianificazione ed esecuzione del modello applicativo di Data factory di Azure. |
| [Monitorare e gestire le pipeline con l'app di monitoraggio](data-factory-monitor-manage-app.md) |Questo articolo descrive come monitorare, gestire ed eseguire il debug delle pipeline usando l'app di monitoraggio e gestione. |

