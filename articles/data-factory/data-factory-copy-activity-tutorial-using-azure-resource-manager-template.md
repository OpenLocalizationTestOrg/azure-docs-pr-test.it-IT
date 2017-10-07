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
# <a name="tutorial-use-azure-resource-manager-template-toocreate-a-data-factory-pipeline-toocopy-data"></a>Esercitazione: Usare Gestione risorse di Azure modello toocreate una Data Factory pipeline toocopy di dati 
> [!div class="op_single_selector"]
> * [Panoramica e prerequisiti](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [Copia guidata](data-factory-copy-data-wizard-tutorial.md)
> * [Portale di Azure](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)
> * [Modello di Azure Resource Manager](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [API REST](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [API .NET](data-factory-copy-activity-tutorial-using-dotnet-api.md)
> 
> 

In questa esercitazione illustra come toouse un toocreate modello di gestione risorse di Azure una data factory di Azure. pipeline di dati Hello in questa esercitazione consente di copiare dati da un archivio dati di origine dati archivio tooa destinazione. Non Trasforma dati di output tooproduce dati di input. Per un'esercitazione su come dati di tootransform tramite Data Factory di Azure, vedere [esercitazione: creare una pipeline di dati tootransform utilizzando cluster Hadoop](data-factory-build-your-first-pipeline.md).

In questa esercitazione si crea una pipeline contenente una sola attività: un'attività di copia attività di copia Hello copia dati da un archivio dati di sink supportati tooa di archivio di dati supportati. Per un elenco degli archivi dati supportati come origini e sink, vedere gli [archivi dati supportati](data-factory-data-movement-activities.md#supported-data-stores-and-formats). attività Hello è alimentato da un servizio disponibile a livello globale che è possibile copiare dati tra diversi archivi dati in modo sicuro, affidabile e scalabile. Per ulteriori informazioni sulle attività di copia hello, vedere [attività lo spostamento dei dati](data-factory-data-movement-activities.md).

Una pipeline può includere più attività Inoltre, è possibile concatenare le due attività (eseguire un'attività dopo l'altro) mediante l'impostazione di set di dati di hello output di un'attività come hello input set di dati di hello altre attività. Per altre informazioni, vedere [Attività multiple in una pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline). 

> [!NOTE] 
> pipeline di dati Hello in questa esercitazione consente di copiare dati da un archivio dati di origine dati archivio tooa destinazione. Per un'esercitazione su come dati di tootransform tramite Data Factory di Azure, vedere [esercitazione: creare una pipeline di dati tootransform utilizzando cluster Hadoop](data-factory-build-your-first-pipeline.md). 

## <a name="prerequisites"></a>Prerequisiti
* Seguire i passaggi [esercitazione panoramica e prerequisiti](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) e hello completo **prerequisito** passaggi.
* Seguire le istruzioni [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview) articolo tooinstall versione più recente di Azure PowerShell nel computer in uso. In questa esercitazione, utilizzare le entità di PowerShell toodeploy Data Factory. 
* (facoltativo) Vedere [la creazione di modelli di gestione risorse di Azure](../azure-resource-manager/resource-group-authoring-templates.md) toolearn sui modelli di gestione risorse di Azure.

## <a name="in-this-tutorial"></a>Contenuto dell'esercitazione:
In questa esercitazione, si crea una factory di dati con hello entità Data Factory di seguito:

| Entità | Descrizione |
| --- | --- |
| Servizio collegato Archiviazione di Azure |Collega la data factory toohello account di archiviazione di Azure. Archiviazione di Azure è l'archivio dati di origine hello e database SQL di Azure è hello sink dati store per le attività di copia hello in esercitazione hello. Specifica account di archiviazione hello che contiene i dati di input per l'attività di copia hello hello. |
| Servizio collegato per il database SQL Azure |Collega il toohello data factory di Azure SQL database. Specifica i database SQL di Azure hello che contiene i dati di output di hello per attività di copia hello. |
| Set di dati di input del BLOB di Azure |Fa riferimento il servizio di archiviazione di Azure collegati toohello. Hello servizio collegato fa riferimento tooan account di archiviazione Azure e set di dati Blob di Azure hello specifica hello contenitore, cartella e nome file nel servizio di archiviazione che contiene i dati di input hello hello. |
| Set di dati di output di SQL Azure |Fa riferimento a servizio collegato SQL Azure toohello. servizio collegato SQL Azure Hello fa riferimento a server SQL Azure tooan e set di dati SQL di Azure hello Specifica nome hello della tabella di hello che contiene i dati di output di hello. |
| Data Pipeline |pipeline di Hello dispone di un'attività di copia che accetta i set di dati blob di Azure hello come input di tipo e set di dati di SQL Azure come output di hello. attività di copia Hello copia dati da una tabella di tooa blob di Azure in database SQL di Azure hello. |

Una data factory può comprendere una o più pipeline. Una pipeline può comprendere una o più attività. Esistono due tipi di attività: [attività di spostamento dei dati](data-factory-data-movement-activities.md) e [attività di trasformazione dei dati](data-factory-data-transformation-activities.md). In questa esercitazione si crea una pipeline con una sola attività (attività di copia).

![Copiare il Blob di Azure tooAzure Database SQL](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/CopyBlob2SqlDiagram.png) 

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
Creare un file JSON denominato **ADFCopyTutorialARM.json** in **C:\ADFGetStarted** cartella con hello seguente contenuto:

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

## <a name="parameters-json"></a>Parametri JSON
Creare un file JSON denominato **ADFCopyTutorialARM Parameters.json** che contiene i parametri per il modello di gestione risorse di Azure hello. 

> [!IMPORTANT]
> Specificare il nome e la chiave dell'account di archiviazione di Azure per i parametri storageAccountName e storageAccountKey.  
> 
> Specificare il server SQL Azure, il database, l'utente e la password per i parametri sqlServerName, databaseName, sqlServerUserName e sqlServerPassword.  

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
   * Sottoscrizione hello tooselect da toowork con il comando seguente hello esecuzione.
    
    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```    
2. Eseguire hello successivo comando toodeploy Data Factory le entità utilizzando il modello di gestione risorse hello creato nel passaggio 1.

    ```PowerShell   
    New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile C:\ADFGetStarted\ADFCopyTutorialARM.json -TemplateParameterFile C:\ADFGetStarted\ADFCopyTutorialARM-Parameters.json
    ```

## <a name="monitor-pipeline"></a>Monitorare la pipeline

1. Accedi toohello [portale di Azure](https://portal.azure.com) utilizzando l'account di Azure.
2. Fare clic su **Data factory** hello sinistro menu (o) fare clic su **più servizi** e fare clic su **Data factory** in **INTELLIGENCE + analisi** categoria.
   
    ![Menu Data factory](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/data-factories-menu.png)
3. In hello **Data factory** pagina, cercare e individuare la data factory (AzureBlobToAzureSQLDatabaseDF). 
   
    ![Cercare la data factory](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/search-for-data-factory.png)  
4. Fare clic sulla data factory di Azure. Vedrai hello home page per data factory di hello.
   
    ![Home page della data factory](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/data-factory-home-page.png)  
6. Seguire le istruzioni da [monitorare set di dati e della pipeline](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline) pipeline hello toomonitor e set di dati è stato creato in questa esercitazione. Attualmente, Visual Studio non supporta il monitoraggio delle pipeline di Data Factory.
7. Quando una sezione è hello **pronto** stato, verificare che i dati di hello toohello copiato **emp** tabella nel database di SQL Azure hello.


Per ulteriori informazioni su come pipeline di toomonitor toouse pannelli portale Azure e set di dati è stato creato in questa esercitazione, vedere [monitorare set di dati e della pipeline](data-factory-monitor-manage-pipelines.md) .

Per ulteriori informazioni su come toouse hello monitoraggio e Gestione applicazione toomonitor i dati delle pipeline, vedere [monitoraggio e la gestione delle pipeline di Data Factory di Azure utilizzando App monitoraggio](data-factory-monitor-manage-app.md).

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
"dataFactoryName": "[concat('AzureBlobToAzureSQLDatabaseDF', uniqueString(resourceGroup().id))]"
```

È una stringa univoca in base a hello ID gruppo di risorse.  

### <a name="defining-data-factory-entities"></a>Definizione di entità di Data factory
Hello entità Data Factory seguenti vengono definite nel modello JSON hello: 

1. [Servizio collegato Archiviazione di Azure](#azure-storage-linked-service)
2. [Servizio collegato SQL di Azure](#azure-sql-database-linked-service)
3. [Set di dati del BLOB di Azure](#azure-blob-dataset)
4. [Set di dati di Azure SQL](#azure-sql-dataset)
5. [Pipeline di dati con un'attività di copia](#data-pipeline)

#### <a name="azure-storage-linked-service"></a>Servizio collegato Archiviazione di Azure
Hello AzureStorageLinkedService collega la data factory toohello account di archiviazione di Azure. È stato creato un contenitore e caricare l'account di archiviazione di dati toothis come parte di [prerequisiti](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md). Specificare il nome di hello e chiave dell'account di archiviazione di Azure in questa sezione. Vedere [servizio collegato di archiviazione di Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service) per informazioni dettagliate su JSON proprietà utilizzate toodefine servizio collegato di archiviazione di Azure. 

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

connectionString Hello utilizza i parametri di storageAccountName e storageAccountKey hello. valori Hello per questi parametri passati mediante un file di configurazione. definizione di Hello utilizza anche variabili: azureStroageLinkedService e dataFactoryName definiti nel modello di hello. 

#### <a name="azure-sql-database-linked-service"></a>Servizio collegato per il database SQL Azure
AzureSqlLinkedService collega il toohello data factory di Azure SQL database. dati Hello che viene copiati dall'archiviazione blob hello vengono archiviati nel database. Tabella emp hello è stato creato in questo database come parte di [prerequisiti](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md). Specificare nome del server SQL Azure hello, nome del database, nome utente e password dell'utente in questa sezione. Vedere [servizio collegato SQL Azure](data-factory-azure-sql-connector.md#linked-service-properties) per informazioni dettagliate su JSON proprietà utilizzate toodefine servizio collegato SQL Azure.  

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

connectionString Hello utilizza sqlServerName, databaseName, sqlServerUserName e sqlServerPassword parametri i cui valori vengono passati mediante un file di configurazione. Hello definizione utilizza inoltre hello seguenti variabili dal modello hello: azureSqlLinkedServiceName, dataFactoryName.

#### <a name="azure-blob-dataset"></a>Set di dati del BLOB di Azure
il servizio di archiviazione di Azure collegati Hello specifica hello stringa di connessione del servizio Data Factory utilizzata in fase di esecuzione tooconnect tooyour account di archiviazione di Azure. Nella definizione di set di dati blob di Azure, specificare i nomi di contenitore blob, cartelle e file che contiene i dati di input hello. Vedere [proprietà set di dati Blob di Azure](data-factory-azure-blob-connector.md#dataset-properties) per informazioni dettagliate su JSON proprietà utilizzate toodefine un set di dati Blob di Azure. 

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

#### <a name="azure-sql-dataset"></a>Set di dati di Azure SQL
Specificare il nome di hello della tabella hello in database SQL di Azure hello che contiene i dati copiato hello da hello archiviazione Blob di Azure. Vedere [proprietà set di dati di SQL Azure](data-factory-azure-sql-connector.md#dataset-properties) per informazioni dettagliate su JSON proprietà utilizzate toodefine un set di dati di SQL Azure. 

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

#### <a name="data-pipeline"></a>Data Pipeline
È possibile definire una pipeline che copia i dati dal set di dati SQL di Azure toohello di hello blob di Azure set di dati. Vedere [JSON di Pipeline](data-factory-create-pipelines.md#pipeline-json) per le descrizioni degli elementi usati di JSON toodefine una pipeline in questo esempio. 

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

## <a name="reuse-hello-template"></a>Riutilizzare hello modello
Nell'esercitazione hello è creato un modello per la definizione di entità Data Factory e un modello per il passaggio di valori per i parametri. pipeline Hello copia dati da un database di SQL Azure tooan di account di archiviazione di Azure specificato tramite i parametri. toouse hello stessi ambienti con toodifferent entità modello toodeploy Data Factory, creare un file di parametro per ogni ambiente e usarlo quando si distribuisce toothat ambiente.     

Esempio:  

```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Dev.json
```
```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Test.json
```
```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Production.json
```

Si noti che hello primo comando Usa il file di parametro per l'ambiente di sviluppo hello, secondo una per hello ambiente di test e una terza per ambiente di produzione hello hello.  

È inoltre possibile riutilizzare hello modello tooperform ripetuto di attività. Ad esempio, è necessario toocreate molti data factory con uno o più pipeline che implementano hello stesso logica ma ogni data factory utilizza diversi account di archiviazione e il Database SQL. In questo scenario, si usa hello stesso modello in hello stesso ambiente (sviluppo, test o produzione) con parametri diversi file toocreate data factory.   

## <a name="next-steps"></a>Passaggi successivi
In questa esercitazione sono stati usati l'archivio BLOB di Azure come archivio dati di origine e un database SQL di Azure come archivio dati di destinazione in un'operazione di copia. Hello nella tabella seguente fornisce un elenco di archivi di dati supportato come origini e destinazioni da attività di copia hello: 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

toolearn su come archiviano dati toocopy da e verso un tipo di dati, fare clic su collegamento hello per hello archivio di dati nella tabella hello.
