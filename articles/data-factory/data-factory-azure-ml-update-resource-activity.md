---
title: i modelli di Machine Learning aaaUpdate utilizzando Data Factory di Azure | Documenti Microsoft
description: Viene descritto come toocreate creare pipeline predittive con Data Factory di Azure e Azure Machine Learning
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: 6e5e4d2cfd245c7a9ed3bb9cdacca1f7f82b9620
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="updating-azure-machine-learning-models-using-update-resource-activity"></a>Aggiornamento dei modelli di Azure Machine Learning con Attività della risorsa di aggiornamento

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [Attività Hive](data-factory-hive-activity.md) 
> * [Attività di Pig](data-factory-pig-activity.md)
> * [Attività MapReduce](data-factory-map-reduce.md)
> * [Attività di Hadoop Streaming](data-factory-hadoop-streaming-activity.md)
> * [Attività Spark](data-factory-spark.md)
> * [Attività di esecuzione batch di Machine Learning](data-factory-azure-ml-batch-execution-activity.md)
> * [Attività della risorsa di aggiornamento di Machine Learning](data-factory-azure-ml-update-resource-activity.md)
> * [Attività stored procedure](data-factory-stored-proc-activity.md)
> * [Attività U-SQL di Data Lake Analytics](data-factory-usql-activity.md)
> * [Attività personalizzata di .NET](data-factory-use-custom-activities.md)

In questo articolo fa da complemento hello principale Data Factory di Azure - articolo di integrazione di Azure Machine Learning: [creare pipeline predittive con Data Factory di Azure e di Azure Machine Learning](data-factory-azure-ml-batch-execution-activity.md). Se non già stato fatto, esaminare l'articolo principale hello prima di leggere questo articolo. 

## <a name="overview"></a>Panoramica
Nel corso del tempo, i modelli di previsione hello negli esperimenti di assegnazione dei punteggi di hello Azure ML devono toobe ripetere il training con nuovi set di dati di input. Dopo avere completato con ripetizione di training, si desidera hello tooupdate punteggio servizio web con hello ripetere il training del modello ML. Hello passaggi tipici tooenable ripetizione di training e l'aggiornamento di modelli di Azure ML tramite i servizi web sono:

1. Creare un esperimento in [Azure ML Studio](https://studio.azureml.net).
2. Quando si è soddisfatti dei modello hello, utilizzare servizi di Azure ML Studio toopublish web per entrambi hello **esperimento di training** e assegnazione dei punteggi /**esperimento predittiva**.

Hello nella tabella seguente descrive i servizi web hello utilizzati in questo esempio.  Per altre informazioni, vedere [Ripetere il training dei modelli di Machine Learning a livello di codice](../machine-learning/machine-learning-retrain-models-programmatically.md) .

- **Servizio Web di training**: riceve dati di training e produce modelli sottoposti a training. output di Hello di ripetizione di training hello è un file .ilearner in una risorsa di archiviazione Blob di Azure. Hello **predefinito endpoint** viene creato automaticamente per quando si pubblica la formazione di hello riuscire come servizio web. È possibile creare più endpoint, ma esempio hello utilizza solo endpoint di hello predefinito.
- **Servizio Web di assegnazione dei punteggi**: riceve esempi di dati non etichettati ed esegue previsioni. output di Hello di stima può avere forme diverse, ad esempio un file CSV o le righe in un database di SQL Azure, a seconda della configurazione di hello dell'esperimento hello. endpoint predefinito Hello viene creato automaticamente quando si pubblica l'esperimento predittiva di hello come servizio web. 

Hello nella figura seguente viene illustrata hello relazione tra set di training e assegnazione dei punteggi di endpoint in Azure Machine Learning.

![SERVIZI WEB](./media/data-factory-azure-ml-batch-execution-activity/web-services.png)

È possibile richiamare hello **training servizio web** utilizzando hello **attività di esecuzione Batch di Azure ML**. Richiamare il servizio Web di training è la stessa operazione che si esegue per richiamare un servizio Web di Azure ML, il servizio Web di assegnazione dei punteggi, per la valutazione dei dati. Hello precedente copertura di sezioni, come un servizio web Machine Learning di Azure da una Data Factory di Azure tooinvoke della pipeline in dettaglio. 

È possibile richiamare hello **servizio web di punteggio** utilizzando hello **attività della risorsa di Azure ML aggiornamento** servizio web di hello tooupdate con modello sottoposto a training appena hello. seguono esempi Hello fornisce le definizioni di servizio collegato: 

## <a name="scoring-web-service-is-a-classic-web-service"></a>Il servizio Web di assegnazione dei punteggi è un servizio Web classico
Se hello servizio web di punteggio è un **servizio web classico**, creare hello secondo **endpoint non predefinito e aggiornabile** utilizzando hello [portale di Azure](https://manage.windowsazure.com). Per la procedura, vedere l'articolo [Creare endpoint](../machine-learning/machine-learning-create-endpoint.md) . Dopo aver creato endpoint aggiornabile di hello non predefinito, hello alla procedura seguente:

* Fare clic su **esecuzione BATCH** tooget hello URI valore hello **mlEndpoint** proprietà JSON.
* Fare clic su **aggiornamento risorsa** tooget hello URI valore per hello del collegamento **updateresourceendpoint ' dal** proprietà JSON. Nella pagina endpoint hello stesso è una chiave API Hello (nell'angolo in basso a destra di hello).

![Endpoint aggiornabile](./media/data-factory-azure-ml-batch-execution-activity/updatable-endpoint.png)

Hello di esempio seguente fornisce una definizione JSON di esempio per il servizio di Azure ml collegato hello. Hello apiKey di hello servizio collegato viene utilizzato per l'autenticazione.  

```json
{
    "name": "updatableScoringEndpoint2",
    "properties": {
        "type": "AzureML",
        "typeProperties": {
            "mlEndpoint": "https://ussouthcentral.services.azureml.net/workspaces/xxx/services/--scoring experiment--/jobs",
            "apiKey": "endpoint2Key",
            "updateResourceEndpoint": "https://management.azureml.net/workspaces/xxx/webservices/--scoring experiment--/endpoints/endpoint2"
        }
    }
}
```

## <a name="scoring-web-service-is-azure-resource-manager-web-service"></a>Il servizio di assegnazione dei punteggi è un servizio Web di Azure Resource Manager 
Se il servizio web hello è hello nuovo tipo di servizio web che espone un endpoint di gestione risorse di Azure, non è necessario tooadd hello secondo **non predefinito** endpoint. Hello **updateresourceendpoint ' dal** in hello servizio collegato è del formato hello: 

```
https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resource-group-name}/providers/Microsoft.MachineLearning/webServices/{web-service-name}?api-version=2016-05-01-preview. 
```

È possibile ottenere valori per i segnaposto hello URL quando si eseguono query del servizio web hello in hello [portale dei servizi Web Azure Machine Learning](https://services.azureml.net/). Hello nuovo tipo di endpoint di risorsa di aggiornamento richiede un token di Azure ad (Azure Active Directory). Specificare **servicePrincipalId** e **servicePrincipalKey** nel servizio collegato AzureML. Vedere [come toocreate entità del servizio e assegnare le autorizzazioni toomanage risorse di Azure](../azure-resource-manager/resource-group-create-service-principal-portal.md). Ecco una definizione di esempio del servizio collegato AzureML: 

```json
{
    "name": "AzureMLLinkedService",
    "properties": {
        "type": "AzureML",
        "description": "hello linked service for AML web service.",
        "typeProperties": {
            "mlEndpoint": "https://ussouthcentral.services.azureml.net/workspaces/0000000000000000000000000000000000000/services/0000000000000000000000000000000000000/jobs?api-version=2.0",
            "apiKey": "xxxxxxxxxxxx",
            "updateResourceEndpoint": "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myRG/providers/Microsoft.MachineLearning/webServices/myWebService?api-version=2016-05-01-preview",
            "servicePrincipalId": "000000000-0000-0000-0000-0000000000000",
            "servicePrincipalKey": "xxxxx",
            "tenant": "mycompany.com"
        }
    }
}
```

Hello nello scenario seguente vengono fornite informazioni dettagliate. Include un esempio per la ripetizione del training e l'aggiornamento dei modelli di Azure ML da una pipeline di Azure Data Factory.

## <a name="scenario-retraining-and-updating-an-azure-ml-model"></a>Scenario: ripetizione del training e aggiornamento di un modello di Azure ML
In questa sezione fornisce una pipeline di esempio che utilizza hello **attività esecuzione Batch di Azure ML** tooretrain un modello. pipeline di Hello utilizza inoltre hello **attività di Azure ML aggiornamento risorsa** modello hello tooupdate hello punteggio servizio web. sezione Hello nonché hello di frammenti di codice JSON per tutti i servizi collegati, i set di dati e della pipeline nell'esempio hello.

Di seguito è una vista diagramma hello della pipeline di esempio hello. Come si può notare, hello attività di esecuzione Batch di Azure ML accetta input di training hello e produce un output di training (file iLearner). Attività della risorsa di Azure ML aggiornamento Hello accetta l'output di training e aggiornamenti hello modello hello punteggio endpoint del servizio web. Hello attività della risorsa di aggiornamento non genera alcun output. placeholderBlob Hello è solo un set di dati del fittizio output richiesto dalla pipeline di hello toorun di hello Data Factory di Azure del servizio.

![Diagramma della pipeline](./media/data-factory-azure-ml-batch-execution-activity/update-activity-pipeline-diagram.png)

### <a name="azure-blob-storage-linked-service"></a>Servizio collegato di archiviazione BLOB di Azure:
Archiviazione di Azure Hello contiene hello dati seguenti:

* Dati di training. dati di input Hello per servizio web di hello Azure ML training.  
* File iLearner. Hello output dal servizio web di hello Azure ML training. Questo file è inoltre hello input toohello attività di aggiornamento risorsa.  

Ecco definizione JSON di esempio hello del servizio collegato hello:

```JSON
{
    "name": "StorageLinkedService",
      "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=name;AccountKey=key"
        }
    }
}
```

### <a name="training-input-dataset"></a>Set di dati di input di training:
Hello seguente set di dati rappresenta i dati di training input hello per servizio web di hello Azure ML training. l'attività di esecuzione Batch di Azure ML Hello accetta questo set di dati come input.

```JSON
{
    "name": "trainingData",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "labeledexamples",
            "fileName": "labeledexamples.arff",
            "format": {
                "type": "TextFormat"
            }
        },
        "availability": {
            "frequency": "Week",
            "interval": 1
        },
        "policy": {          
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

### <a name="training-output-dataset"></a>Set di dati di output di training:
Hello seguente set di dati rappresenta hello iLearner file di output dal servizio web di hello Azure ML training. Attività di esecuzione Batch di Azure ML Hello produce questo set di dati. Questo set di dati è inoltre hello input toohello attività di Azure ML aggiornamento risorsa.

```JSON
{
    "name": "trainedModelBlob",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "trainingoutput",
            "fileName": "model.ilearner",
            "format": {
                "type": "TextFormat"
            }
        },
        "availability": {
            "frequency": "Week",
            "interval": 1
        }
    }
}
```

### <a name="linked-service-for-azure-ml-training-endpoint"></a>Servizio collegato per l'endpoint di training di Azure ML
Hello frammento di codice JSON seguente definisce un servizio collegato di Azure Machine Learning che fa riferimento a endpoint predefinito toohello del servizio web di training hello.

```JSON
{    
    "name": "trainingEndpoint",
      "properties": {
        "type": "AzureML",
        "typeProperties": {
            "mlEndpoint": "https://ussouthcentral.services.azureml.net/workspaces/xxx/services/--training experiment--/jobs",
              "apiKey": "myKey"
        }
      }
}
```

In **Azure ML Studio**, hello tooget i valori per seguenti **mlEndpoint** e **apiKey**:

1. Fare clic su **servizi WEB** nel menu di sinistra hello.
2. Fare clic su hello **training servizio web** nell'elenco di hello dei servizi web.
3. Fare clic su Copia Avanti troppo**chiave API** casella di testo. Incollare la chiave hello negli Appunti hello nell'editor di JSON Factory dati hello.
4. In hello **Azure ML studio**, fare clic su **esecuzione BATCH** collegamento.
5. Hello copia **URI della richiesta** da hello **richiesta** sezione e incollarlo nell'editor delle Data Factory JSON hello.   

### <a name="linked-service-for-azure-ml-updatable-scoring-endpoint"></a>Servizio collegato per l'endpoint di assegnazione dei punteggi aggiornabile di Azure ML:
Hello frammento di codice JSON seguente definisce un servizio collegato di Azure Machine Learning che fa riferimento a endpoint aggiornabile di toohello non predefinito di hello punteggio servizio web.  

```JSON
{
    "name": "updatableScoringEndpoint2",
    "properties": {
        "type": "AzureML",
        "typeProperties": {
            "mlEndpoint": "https://ussouthcentral.services.azureml.net/workspaces/00000000eb0abe4d6bbb1d7886062747d7/services/00000000026734a5889e02fbb1f65cefd/jobs?api-version=2.0",
            "apiKey": "sooooooooooh3WvG1hBfKS2BNNcfwSO7hhY6dY98noLfOdqQydYDIXyf2KoIaN3JpALu/AKtflHWMOCuicm/Q==",
            "updateResourceEndpoint": "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/myWebService?api-version=2016-05-01-preview",
            "servicePrincipalId": "fe200044-c008-4008-a005-94000000731",
            "servicePrincipalKey": "zWa0000000000Tp6FjtZOspK/WMA2tQ08c8U+gZRBlw=",
            "tenant": "mycompany.com"
        }
    }
}
```

### <a name="placeholder-output-dataset"></a>Set di dati di output del segnaposto:
attività di Azure ML aggiornamento risorsa Hello non genera alcun output. Tuttavia, Data Factory di Azure richiede una pianificazione di hello output toodrive set di dati di una pipeline. quindi in questo esempio viene usato un set di dati segnaposto fittizio.  

```JSON
{
    "name": "placeholderBlob",
    "properties": {
        "availability": {
            "frequency": "Week",
            "interval": 1
        },
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "any",
            "format": {
                "type": "TextFormat"
            }
        }
    }
}
```

### <a name="pipeline"></a>Pipeline
Hello pipeline dispone di due attività: **AzureMLBatchExecution** e **AzureMLUpdateResource**. l'attività di esecuzione Batch di Azure ML Hello accetta i dati di training hello come input e genera un file iLearner come output. attività Hello richiama il servizio web di formazione hello (esperimento di training esposta come servizio web) con input hello i dati di training e riceve file ilearner hello dal servizio Web hello. placeholderBlob Hello è solo un set di dati del fittizio output richiesto dalla pipeline di hello toorun di hello Data Factory di Azure del servizio.

![Diagramma della pipeline](./media/data-factory-azure-ml-batch-execution-activity/update-activity-pipeline-diagram.png)

```JSON
{
    "name": "pipeline",
    "properties": {
        "activities": [
            {
                "name": "retraining",
                "type": "AzureMLBatchExecution",
                "inputs": [
                    {
                        "name": "trainingData"
                    }
                ],
                "outputs": [
                    {
                        "name": "trainedModelBlob"
                    }
                ],
                "typeProperties": {
                    "webServiceInput": "trainingData",
                    "webServiceOutputs": {
                        "output1": "trainedModelBlob"
                    }              
                 },
                "linkedServiceName": "trainingEndpoint",
                "policy": {
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1,
                    "timeout": "02:00:00"
                }
            },
            {
                "type": "AzureMLUpdateResource",
                "typeProperties": {
                    "trainedModelName": "Training Exp for ADF ML [trained model]",
                    "trainedModelDatasetName" :  "trainedModelBlob"
                },
                "inputs": [
                    {
                        "name": "trainedModelBlob"
                    }
                ],
                "outputs": [
                    {
                        "name": "placeholderBlob"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "name": "AzureML Update Resource",
                "linkedServiceName": "updatableScoringEndpoint2"
            }
        ],
        "start": "2016-02-13T00:00:00Z",
           "end": "2016-02-14T00:00:00Z"
    }
}
```
