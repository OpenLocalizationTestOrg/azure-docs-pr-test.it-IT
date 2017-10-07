---
title: pipeline di dati predittivi aaaCreate utilizzando Data Factory di Azure | Documenti Microsoft
description: Viene descritto come toocreate creare pipeline predittive con Data Factory di Azure e Azure Machine Learning
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 4fad8445-4e96-4ce0-aa23-9b88e5ec1965
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: 943210c28b1696e299ff9b7cc96369b95f182354
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-predictive-pipelines-using-azure-machine-learning-and-azure-data-factory"></a>Creare pipeline predittive tramite Azure Machine Learning e Azure Data Factory

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

## <a name="introduction"></a>Introduzione

### <a name="azure-machine-learning"></a>Azure Machine Learning
[Azure Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/) Abilita è toobuild, testare e distribuire soluzioni analitica predittiva. Da un punto di vista generale, questo avviene in tre passaggi:

1. **Creare un esperimento di training**. Eseguire questo passaggio utilizzando hello Azure ML Studio. Machine Learning studio di Hello è un ambiente di sviluppo visivo collaborativo utilizzare tootrain e testare un modello predittivo analitica utilizzando i dati di training.
2. **Convertirlo esperimento predittiva tooa**. Una volta il modello è stato eseguito con i dati esistenti e si è pronti toouse è tooscore nuovi dati, la preparazione e semplificare l'esperimento di assegnazione dei punteggi.
3. **Distribuirlo come servizio Web**. È possibile pubblicare l'esperimento di assegnazione dei punteggi come servizio Web di Azure. È possibile modello di dati tooyour tramite questo punto finale del servizio web di inviare e ricevere le stime di risultato da modello hello.  

### <a name="azure-data-factory"></a>Data factory di Azure
Data Factory è un servizio di integrazione di dati basato su cloud che Orchestra e automatizza hello **spostamento** e **trasformazione** dei dati. È possibile creare soluzioni di integrazione dati utilizzando Data Factory di Azure che possono inserire dati da diversi archivi dati, dati hello/processo di trasformazione e pubblicare archivi dati toohello di hello risultato dati.

Servizio Data Factory consente una pipeline di dati toocreate spostano e trasformare i dati e quindi eseguirla le pipeline hello in una pianificazione specifica (oraria, giornaliera, settimanale e così via). Offre inoltre le dipendenze tra le pipeline di dati e la derivazione di visualizzazioni dettagliate toodisplay hello e monitorare tutte le pipeline di dati da un problemi di individuare tooeasily singola vista unificata e gli avvisi di monitoraggio del programma di installazione.

Vedere [tooAzure introduzione Data Factory](data-factory-introduction.md) e [compilare le pipeline prima](data-factory-build-your-first-pipeline.md) tooquickly articoli introduzione hello servizio Azure Data Factory.

### <a name="data-factory-and-machine-learning-together"></a>Data Factory e Machine Learning
Azure consente di Data Factory è tooeasily creare pipeline che utilizzano un report pubblicato [Azure Machine Learning] [ azure-machine-learning] web service per analitica predittiva. Utilizzo di hello **attività di esecuzione Batch** in una pipeline di Data Factory di Azure, è possibile richiamare un toomake stime di Azure ML web service sui dati hello in batch. Vedere [richiamando un Azure ML servizio web utilizzando hello attività di esecuzione Batch](#invoking-an-azure-ml-web-service-using-the-batch-execution-activity) sezione per informazioni dettagliate.

Nel corso del tempo, i modelli di previsione hello negli esperimenti di assegnazione dei punteggi di hello Azure ML devono toobe ripetere il training con nuovi set di dati di input. È possibile ripetere il training un modello da una pipeline di Data Factory di Azure ML effettuando hello alla procedura seguente:

1. Pubblicare l'esperimento di training hello (non predittiva esperimento) come un servizio web. Eseguire questo passaggio in Azure Machine Learning Studio hello come esperimento predittiva tooexpose come un servizio web nello scenario precedente hello.
2. Usa servizio web per esperimento di training hello hello attività di esecuzione Batch di Azure ML tooinvoke hello. In pratica, è possibile utilizzare hello esecuzione Batch di Azure ML attività tooinvoke training servizio web e il servizio web di punteggio.

Dopo avere completato con ripetizione di training, aggiornare il punteggio di servizio web (esperimento predittiva esposta come servizio web) con il modello appena eseguito il training di hello utilizzando hello hello **attività risorse di Azure ML aggiornare**. Per informazioni dettagliate, vedere l'articolo [Updating models using Update Resource Activity](data-factory-azure-ml-update-resource-activity.md) (Aggiornamento dei modelli con Attività della risorsa di aggiornamento).

## <a name="invoking-a-web-service-using-batch-execution-activity"></a>Richiamo di un servizio Web tramite Attività di esecuzione batch
Utilizzare l'elaborazione e lo spostamento dei dati di Azure Data Factory tooorchestrate e quindi eseguire esecuzione batch utilizzando Azure Machine Learning. Ecco i passaggi di livello superiore di hello:

1. Creare un servizio collegato di Azure Machine Learning. È necessario hello seguenti valori:

   1. **URI della richiesta** per hello API esecuzione Batch. È possibile trovare l'URI della richiesta di hello facendo hello **esecuzione BATCH** collegamento nella pagina servizi web di hello.
   2. **Chiave API** per hello pubblicato il servizio web Azure Machine Learning. È possibile trovare la chiave API hello facendo clic sul servizio web hello che è stata pubblicata.
   3. Hello utilizzare **AzureMLBatchExecution** attività.

      ![Dashboard di Machine Learning](./media/data-factory-azure-ml-batch-execution-activity/AzureMLDashboard.png)

      ![Batch URI](./media/data-factory-azure-ml-batch-execution-activity/batch-uri.png)

### <a name="scenario-experiments-using-web-service-inputsoutputs-that-refer-toodata-in-azure-blob-storage"></a>Scenario: Esperimenti con Web servizio degli input/output che fanno riferimento toodata nell'archiviazione Blob di Azure
In questo scenario, hello servizio Web di Azure Machine Learning esegue le stime utilizzando i dati da un file in una risorsa di archiviazione blob di Azure e archivia i risultati della stima hello nell'archiviazione blob hello. Hello JSON seguente definisce una pipeline di Data Factory con un'attività AzureMLBatchExecution. attività Hello dispone di set di dati hello **DecisionTreeInputBlob** come input e **DecisionTreeResultBlob** come output di hello. Hello **DecisionTreeInputBlob** viene passato come un servizio web di input toohello da utilizzando hello **WebServiceInputActivity** proprietà JSON. Hello **DecisionTreeResultBlob** viene passato come un servizio Web toohello di output da utilizzando hello **webserviceoutputs della** proprietà JSON.  

> [!IMPORTANT]
> Se il servizio web hello accetta più input, utilizzare hello **webServiceInputs** proprietà anziché **webServiceInput**. Vedere hello [servizio Web richiede più input](#web-service-requires-multiple-inputs) sezione per un esempio di utilizzo di proprietà webServiceInputs hello.
>
> Set di dati che fanno riferimento hello **webServiceInput**/**webServiceInputs** e **webserviceoutputs della** proprietà (in  **typeProperties**) deve essere incluso anche in attività hello **input** e **restituisce**.
>
> Nell'esperimento di Machine Learning di Azure,le porte e i parametri globali di input e output del servizio Web hanno nomi predefiniti ("input1", "input2") che è possibile personalizzare. nomi di Hello che è usare per webServiceInputs e webserviceoutputs della globalparameters della impostazioni devono corrispondere esattamente nomi hello negli esperimenti hello. È possibile visualizzare i payload di richiesta di esempio hello nella hello Help esecuzione Batch per il mapping di Azure ML endpoint tooverify hello previsto.
>
>

```JSON
{
  "name": "PredictivePipeline",
  "properties": {
    "description": "use AzureML model",
    "activities": [
      {
        "name": "MLActivity",
        "type": "AzureMLBatchExecution",
        "description": "prediction analysis on batch input",
        "inputs": [
          {
            "name": "DecisionTreeInputBlob"
          }
        ],
        "outputs": [
          {
            "name": "DecisionTreeResultBlob"
          }
        ],
        "linkedServiceName": "MyAzureMLLinkedService",
        "typeProperties":
        {
            "webServiceInput": "DecisionTreeInputBlob",
            "webServiceOutputs": {
                "output1": "DecisionTreeResultBlob"
            }                
        },
        "policy": {
          "concurrency": 3,
          "executionPriorityOrder": "NewestFirst",
          "retry": 1,
          "timeout": "02:00:00"
        }
      }
    ],
    "start": "2016-02-13T00:00:00Z",
    "end": "2016-02-14T00:00:00Z"
  }
}
```
> [!NOTE]
> Solo input e output dell'attività AzureMLBatchExecution hello possono essere passati come parametri toohello servizio Web. Ad esempio, in hello sopra frammento di codice JSON, DecisionTreeInputBlob è un input toohello AzureMLBatchExecution attività, che viene passato come un input toohello servizio Web tramite un parametro webServiceInput.   
>
>

### <a name="example"></a>Esempio
Toohold di archiviazione di Azure viene utilizzato questo esempio sia hello dati di input e outpui.

È consigliabile eseguire hello [compilare le pipeline prima con Data Factory] [ adf-build-1st-pipeline] esercitazione prima di passare attraverso questo esempio. In questo esempio, utilizzare hello Editor delle Data Factory toocreate gli elementi Data Factory (servizi collegati, i set di dati, pipeline).   

1. Creare un **servizio collegato** per **Archiviazione di Azure**. Se hello i file di input e outpui sono in diversi account di archiviazione, è necessario due servizi collegati. Di seguito è fornito un esempio JSON:

    ```JSON
    {
      "name": "StorageLinkedService",
      "properties": {
        "type": "AzureStorage",
        "typeProperties": {
          "connectionString": "DefaultEndpointsProtocol=https;AccountName=[acctName];AccountKey=[acctKey]"
        }
      }
    }
    ```
2. Creare hello **input** Data Factory di Azure **dataset**. A differenza di altri set di dati di Data Factory, questi devono includere entrambi i valori **folderPath** e **fileName**. È possibile utilizzare toocause partizionamento ogni tooprocess (ogni sezione di dati) di esecuzione batch o produrre input univoco e i file di output. Potrebbe essere necessario tooinclude alcuni hello tootransform attività upstream di input in formato CSV hello e inserirlo nell'account di archiviazione hello per ogni sezione. In tal caso, è necessario includere non hello **esterno** e **externalData** impostazioni mostrate nell'hello seguente esempio, il DecisionTreeInputBlob sarebbe e il set di dati di hello output di un'attività diversa.

    ```JSON
    {
      "name": "DecisionTreeInputBlob",
      "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
          "folderPath": "azuremltesting/input",
          "fileName": "in.csv",
          "format": {
            "type": "TextFormat",
            "columnDelimiter": ","
          }
        },
        "external": true,
        "availability": {
          "frequency": "Day",
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

    Il file di input csv deve includere una riga dell'intestazione di colonna hello. Se si utilizza hello **attività di copia** toocreate o spostare hello csv nell'archiviazione blob di hello, è necessario impostare proprietà di sink hello **blobWriterAddHeader** troppo**true**. ad esempio:

    ```JSON
    sink:
    {
        "type": "BlobSink",     
        "blobWriterAddHeader": true
    }
    ```

    Se il file csv hello non dispone di intestazione hello, si può vedere hello il seguente errore: **errore nell'attività: errore durante la lettura di stringa. Token imprevisto: StartObject. Percorso '', riga 1, posizione 1**.
3. Creare hello **output** Data Factory di Azure **dataset**. L'esempio Usa partizionamento toocreate un percorso di output univoca per ogni esecuzione della sezione. Senza il partizionamento hello, attività hello sovrascriverebbe il file hello.

    ```JSON
    {
      "name": "DecisionTreeResultBlob",
      "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
          "folderPath": "azuremltesting/scored/{folderpart}/",
          "fileName": "{filepart}result.csv",
          "partitionedBy": [
            {
              "name": "folderpart",
              "value": {
                "type": "DateTime",
                "date": "SliceStart",
                "format": "yyyyMMdd"
              }
            },
            {
              "name": "filepart",
              "value": {
                "type": "DateTime",
                "date": "SliceStart",
                "format": "HHmmss"
              }
            }
          ],
          "format": {
            "type": "TextFormat",
            "columnDelimiter": ","
          }
        },
        "availability": {
          "frequency": "Day",
          "interval": 15
        }
      }
    }
    ```
4. Creare un **servizio collegato** di tipo: **nell'oggetto AzureMLLinkedService**, fornendo la chiave API hello e modello di URL di esecuzione batch.

    ```JSON
    {
      "name": "MyAzureMLLinkedService",
      "properties": {
        "type": "AzureML",
        "typeProperties": {
          "mlEndpoint": "https://[batch execution endpoint]/jobs",
          "apiKey": "[apikey]"
        }
      }
    }
    ```
5. Creare infine una pipeline contenente un'attività **AzureMLBatchExecution** . In fase di esecuzione della pipeline esegue hello alla procedura seguente:

   1. Ottiene il percorso di hello hello del file di input da input set di dati.
   2. Richiama l'esecuzione di batch di Azure Machine Learning hello API
   3. Copie hello blob toohello output esecuzione di batch specificato con il set di dati di output.

      > [!NOTE]
      > L'attività AzureMLBatchExecution può avere zero o più input e uno o più output.
      >
      >

    ```JSON
    {
        "name": "PredictivePipeline",
        "properties": {
            "description": "use AzureML model",
            "activities": [
            {
                "name": "MLActivity",
                "type": "AzureMLBatchExecution",
                "description": "prediction analysis on batch input",
                "inputs": [
                {
                    "name": "DecisionTreeInputBlob"
                }
                ],
                "outputs": [
                {
                    "name": "DecisionTreeResultBlob"
                }
                ],
                "linkedServiceName": "MyAzureMLLinkedService",
                "typeProperties":
                {
                    "webServiceInput": "DecisionTreeInputBlob",
                    "webServiceOutputs": {
                        "output1": "DecisionTreeResultBlob"
                    }                
                },
                "policy": {
                    "concurrency": 3,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1,
                    "timeout": "02:00:00"
                }
            }
            ],
            "start": "2016-02-13T00:00:00Z",
            "end": "2016-02-14T00:00:00Z"
        }
    }
    ```

      Per la data e l'ora di **inizio** e di **fine** è necessario usare il [formato ISO](http://en.wikipedia.org/wiki/ISO_8601). ad esempio 2014-10-14T16:32:41Z. Hello **fine** ora è facoltativo. Se non specifica alcun valore per hello **fine** proprietà, viene calcolato come "**start + 48 ore.**" specificare in modo indefinito, pipeline hello toorun **9999-09-09** come valore hello hello **fine** proprietà. Per informazioni dettagliate sulle proprietà JSON, vedere [Informazioni di riferimento sugli script JSON di Data Factory](https://msdn.microsoft.com/library/dn835050.aspx) .

      > [!NOTE]
      > Input per l'attività AzureMLBatchExecution hello è facoltativo.
      >
      >

### <a name="scenario-experiments-using-readerwriter-modules-toorefer-toodata-in-various-storages"></a>Scenario: Esperimenti con i moduli di lettura/scrittura toorefer toodata in vari archivi
Un altro scenario comune quando si creano gli esperimenti di Azure ML è toouse moduli di lettura e scrittura. modulo del lettore Hello è tooload utilizzati dati in un esperimento e modulo di scrittura hello è toosave dati dei propri esperimenti. Per informazioni dettagliate sui moduli Reader e Writer, vedere gli argomenti [Reader](https://msdn.microsoft.com/library/azure/dn905997.aspx) e [Writer](https://msdn.microsoft.com/library/azure/dn905984.aspx) in MSDN Library.     

Quando si utilizzano moduli di lettura e scrittura hello, è buona norma toouse un parametro del servizio Web per ogni proprietà di questi moduli di lettura/scrittura. Questi parametri web consentono i valori hello tooconfigure durante il runtime. Ad esempio, è possibile creare un esperimento con un modulo Reader che usa un database SQL di Azure: XXX.database.windows.net. Dopo la distribuzione di servizio web hello, si desidera consumer hello tooenable di hello web servizio toospecify YYY.database.windows.net chiamato un altro Server di SQL Azure. È possibile utilizzare un tooallow di parametro del servizio Web toobe questo valore configurato.

> [!NOTE]
> L'input e l'output del servizio Web sono diversi dai parametri del servizio Web. Nel primo scenario hello, è stato illustrato come un input e output può essere specificati per un servizio Web di Azure ML. In questo scenario, passare i parametri per un servizio Web corrispondenti tooproperties dei moduli di lettura/scrittura.
>
>

Viene preso in esame uno scenario relativo all'uso dei parametri del servizio Web. Si dispone di un servizio web Azure Machine Learning distribuito che usa un dati tooread modulo del lettore da una delle origini dati hello è supportate da Azure Machine Learning (ad esempio: Database SQL di Azure). Una volta eseguita, l'esecuzione batch hello risultati hello vengono scritti utilizzando un modulo di scrittura (Database SQL di Azure).  Nessun input del servizio web e output vengono definiti negli esperimenti hello. In questo caso, si consiglia di configurare i parametri del servizio web rilevanti per i moduli di lettura e scrittura hello. Questa configurazione consente ai moduli toobe configurato quando si utilizza l'attività AzureMLBatchExecution hello hello lettura/scrittura. Specificare i parametri di servizio Web in hello **globalparameters della** sezione in formato JSON dell'attività hello come indicato di seguito.

```JSON
"typeProperties": {
    "globalParameters": {
        "Param 1": "Value 1",
        "Param 2": "Value 2"
    }
}
```

È inoltre possibile utilizzare [funzioni di Data Factory](data-factory-functions-variables.md) per passare i valori per hello parametri del servizio Web come illustrato nell'esempio seguente hello:

```JSON
"typeProperties": {
    "globalParameters": {
       "Database query": "$$Text.Format('SELECT * FROM myTable WHERE timeColumn = \\'{0:yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(WindowStart, 0))"
    }
}
```

> [!NOTE]
> parametri del servizio Web Hello tra maiuscole e minuscole, verificare che i nomi di hello specificati nell'attività hello JSON corrispondano hello quelli esposti dal servizio Web hello.
>
>

### <a name="using-a-reader-module-tooread-data-from-multiple-files-in-azure-blob"></a>Utilizzo di un dati tooread modulo del lettore da più file in Blob di Azure
Le pipeline di Big Data, con attività come Pig e Hive, possono generare uno o più file di output senza estensioni. Ad esempio, quando si specifica una tabella Hive esterna, hello dati per una tabella Hive esterna hello possono essere archiviati nell'archiviazione blob di Azure con hello seguente nome 000000_0. È possibile utilizzare più file di modulo del lettore hello in un esperimento di tooread e utilizzarli per le stime.

Quando si Usa modulo del lettore hello in un esperimento di Azure Machine Learning, è possibile specificare i Blob di Azure come input. file Hello hello archiviazione blob di Azure possono essere file di output di hello (esempio: 000000_0) che vengono generati da uno script Pig e Hive in HDInsight. Hello modulo del lettore consente tooread file (con nessuna estensione) configurando hello **toocontainer percorso, directory/blob**. Hello **percorso toocontainer** punti toohello contenitore e **directory/blob** punta toofolder che contiene i file hello, come illustrato nella seguente immagine hello. Hello asterisco, ovvero \*) **specifica che tutti i file nella cartella/contenitore hello di hello (vale a dire dati/aggregateddata/anno = mese/2014-6 /\*)** vengono lette come parte dell'esperimento hello.

![Proprietà del Blob Azure](./media/data-factory-create-predictive-pipelines/azure-blob-properties.png)

### <a name="example"></a>Esempio
#### <a name="pipeline-with-azuremlbatchexecution-activity-with-web-service-parameters"></a>Pipeline con l'attività AzureMLBatchExecution con parametri del servizio Web

```JSON
{
  "name": "MLWithSqlReaderSqlWriter",
  "properties": {
    "description": "Azure ML model with sql azure reader/writer",
    "activities": [
      {
        "name": "MLSqlReaderSqlWriterActivity",
        "type": "AzureMLBatchExecution",
        "description": "test",
        "inputs": [
          {
            "name": "MLSqlInput"
          }
        ],
        "outputs": [
          {
            "name": "MLSqlOutput"
          }
        ],
        "linkedServiceName": "MLSqlReaderSqlWriterDecisionTreeModel",
        "typeProperties":
        {
            "webServiceInput": "MLSqlInput",
            "webServiceOutputs": {
                "output1": "MLSqlOutput"
            }
              "globalParameters": {
                "Database server name": "<myserver>.database.windows.net",
                "Database name": "<database>",
                "Server user account name": "<user name>",
                "Server user account password": "<password>"
              }              
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "NewestFirst",
          "retry": 1,
          "timeout": "02:00:00"
        },
      }
    ],
    "start": "2016-02-13T00:00:00Z",
    "end": "2016-02-14T00:00:00Z"
  }
}
```

In hello esempio JSON precedente:

* Hello distribuito Azure Machine Learning Web servizio utilizza un lettore e un writer modulo tooread/scrittura di dati da / tooan Database SQL di Azure. Questo servizio Web espone hello seguenti quattro parametri: nome del server, nome del Database, nome Server dell'account utente e password dell'account utente Server di Database.  
* Per la data e l'ora di **inizio** e di **fine** è necessario usare il [formato ISO](http://en.wikipedia.org/wiki/ISO_8601). ad esempio 2014-10-14T16:32:41Z. Hello **fine** ora è facoltativo. Se non specifica alcun valore per hello **fine** proprietà, viene calcolato come "**start + 48 ore.**" specificare in modo indefinito, pipeline hello toorun **9999-09-09** come valore hello hello **fine** proprietà. Per informazioni dettagliate sulle proprietà JSON, vedere [Informazioni di riferimento sugli script JSON di Data Factory](https://msdn.microsoft.com/library/dn835050.aspx) .

### <a name="other-scenarios"></a>Altri scenari
#### <a name="web-service-requires-multiple-inputs"></a>Il servizio Web richiede più input
Se il servizio web hello accetta più input, utilizzare hello **webServiceInputs** proprietà anziché **webServiceInput**. Set di dati che fanno riferimento hello **webServiceInputs** deve essere incluso anche in attività hello **input**.

Nell'esperimento di Machine Learning di Azure,le porte e i parametri globali di input e output del servizio Web hanno nomi predefiniti ("input1", "input2") che è possibile personalizzare. nomi di Hello che è usare per webServiceInputs e webserviceoutputs della globalparameters della impostazioni devono corrispondere esattamente nomi hello negli esperimenti hello. È possibile visualizzare i payload di richiesta di esempio hello nella hello Help esecuzione Batch per il mapping di Azure ML endpoint tooverify hello previsto.

```JSON
{
    "name": "PredictivePipeline",
    "properties": {
        "description": "use AzureML model",
        "activities": [{
            "name": "MLActivity",
            "type": "AzureMLBatchExecution",
            "description": "prediction analysis on batch input",
            "inputs": [{
                "name": "inputDataset1"
            }, {
                "name": "inputDataset2"
            }],
            "outputs": [{
                "name": "outputDataset"
            }],
            "linkedServiceName": "MyAzureMLLinkedService",
            "typeProperties": {
                "webServiceInputs": {
                    "input1": "inputDataset1",
                    "input2": "inputDataset2"
                },
                "webServiceOutputs": {
                    "output1": "outputDataset"
                }
            },
            "policy": {
                "concurrency": 3,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "02:00:00"
            }
        }],
        "start": "2016-02-13T00:00:00Z",
        "end": "2016-02-14T00:00:00Z"
    }
}
```

#### <a name="web-service-does-not-require-an-input"></a>Servizio Web non richiede un input
Servizi web di esecuzione batch di Azure ML può essere utilizzato toorun flussi di lavoro, ad esempio R o script Python, che non richieda alcun input. In alternativa, esperimento hello può essere configurato con un modulo del lettore che espongono qualsiasi globalparameters della. In tal caso, hello AzureMLBatchExecution attività sarà configurata come segue:

```JSON
{
    "name": "scoring service",
    "type": "AzureMLBatchExecution",
    "outputs": [
        {
            "name": "myBlob"
        }
    ],
    "typeProperties": {
        "webServiceOutputs": {
            "output1": "myBlob"
        }              
     },
    "linkedServiceName": "mlEndpoint",
    "policy": {
        "concurrency": 1,
        "executionPriorityOrder": "NewestFirst",
        "retry": 1,
        "timeout": "02:00:00"
    }
},
```

#### <a name="web-service-does-not-require-an-inputoutput"></a>Servizio Web non richiede un input/output
servizio web di esecuzione batch di Azure ML Hello potrebbe non avere alcun output di servizio Web configurato. In questo esempio non sono disponibili input o output del servizio Web, né alcuna proprietà GlobalParameters configurata. È ancora un output configurato nella attività hello stessa, ma non viene fornito come un webServiceOutput.

```JSON
{
    "name": "retraining",
    "type": "AzureMLBatchExecution",
    "outputs": [
        {
            "name": "placeholderOutputDataset"
        }
    ],
    "typeProperties": {
     },
    "linkedServiceName": "mlEndpoint",
    "policy": {
        "concurrency": 1,
        "executionPriorityOrder": "NewestFirst",
        "retry": 1,
        "timeout": "02:00:00"
    }
},
```

#### <a name="web-service-uses-readers-and-writers-and-hello-activity-runs-only-when-other-activities-have-succeeded"></a>Web Service utilizza lettori e writer e attività di hello viene eseguito solo dopo che altre attività hanno avuto esito positivo
Hello Azure ML web reader e writer moduli del servizio potrebbero essere configurato toorun con o senza alcun globalparameters della. Tuttavia, è consigliabile tooembed servizio viene chiamata in una pipeline che utilizza il servizio hello tooinvoke dipendenze di set di dati solo se alcune operazioni di elaborazione a monte è stata completata. È inoltre possibile attivare un'altra azione dopo il completamento dell'esecuzione di batch hello utilizzando questo approccio. In tal caso, è possibile esprimere le dipendenze di hello mediante attività input e output, senza il nome di uno di essi come servizio Web input o output.

```JSON
{
    "name": "retraining",
    "type": "AzureMLBatchExecution",
    "inputs": [
        {
            "name": "upstreamData1"
        },
        {
            "name": "upstreamData2"
        }
    ],
    "outputs": [
        {
            "name": "downstreamData"
        }
    ],
    "typeProperties": {
     },
    "linkedServiceName": "mlEndpoint",
    "policy": {
        "concurrency": 1,
        "executionPriorityOrder": "NewestFirst",
        "retry": 1,
        "timeout": "02:00:00"
    }
},
```

Hello **informazioni chiave** sono:

* Se l'endpoint esperimento utilizza un WebServiceInputActivity: è rappresentato da un set di dati blob ed è incluso in input dell'attività hello e proprietà WebServiceInputActivity hello. In caso contrario, proprietà WebServiceInputActivity hello viene omesso.
* Se l'endpoint esperimento utilizza webServiceOutput(s): essi sono rappresentate dal set di dati blob e sono inclusi negli output di hello attività e nella proprietà webserviceoutputs della hello. output attività Hello e webserviceoutputs della viene eseguito il mapping dal nome hello di ogni output nell'esperimento hello. In caso contrario, proprietà webserviceoutputs della hello viene omesso.
* Se l'endpoint esperimento espone globalParameter(s), essi vengono fornite nella proprietà globalparameters della attività di hello come coppie di chiavi, valore. In caso contrario, proprietà globalparameters della hello viene omesso. le chiavi di Hello maiuscole e minuscole. [Funzioni di Azure Data Factory](data-factory-functions-variables.md) può essere utilizzata nei valori hello.
* Set di dati aggiuntivi possono essere incluse nelle proprietà di input e output di attività hello, senza hello attività typeProperties cui fa riferimento. Questi set di dati determinano l'esecuzione di dipendenze di sezione ma in caso contrario vengono ignorate dal hello AzureMLBatchExecution attività.


## <a name="updating-models-using-update-resource-activity"></a>Aggiornamento dei modelli con Attività della risorsa di aggiornamento
Dopo avere completato con ripetizione di training, aggiornare il punteggio di servizio web (esperimento predittiva esposta come servizio web) con il modello appena eseguito il training di hello utilizzando hello hello **attività risorse di Azure ML aggiornare**. Per informazioni dettagliate, vedere l'articolo [Updating models using Update Resource Activity](data-factory-azure-ml-update-resource-activity.md) (Aggiornamento dei modelli con Attività della risorsa di aggiornamento).

### <a name="reader-and-writer-modules"></a>Moduli Reader e Writer 
Uno scenario comune per l'utilizzo di parametri del servizio Web è utilizzare hello di Azure SQL reader e writer. modulo del lettore Hello è tooload utilizzati dati in un esperimento dai servizi di gestione dati all'esterno di Azure Machine Learning Studio. modulo di scrittura Hello è toosave dati dei propri esperimenti in servizi di gestione dati all'esterno di Azure Machine Learning Studio.  

Per informazioni dettagliate sui BLOB di Azure o sui moduli Reader e Writer SQL di Azure, vedere gli argomenti [Reader](https://msdn.microsoft.com/library/azure/dn905997.aspx) e [Writer](https://msdn.microsoft.com/library/azure/dn905984.aspx) in MSDN Library. esempio Hello nella sezione precedente hello utilizzato lettura Blob di Azure hello e agente di scrittura Blob di Azure. Questa sezione illustra l'uso di un reader e un writer SQL di Azure.

## <a name="frequently-asked-questions"></a>Domande frequenti
**D:** Ho più file generati dalle pipeline di Big Data. È possibile utilizzare toowork AzureMLBatchExecution attività hello in tutti i file hello?

**R:** Sì. Vedere hello **utilizzando un dati tooread modulo del lettore da più file in Blob di Azure** sezione per informazioni dettagliate.

## <a name="azure-ml-batch-scoring-activity"></a>Attività di assegnazione dei punteggi di batch di Azure ML
Se si utilizza hello **AzureMLBatchScoring** toointegrate di attività con Azure Machine Learning, è consigliabile utilizzare più recente hello **AzureMLBatchExecution** attività.

Hello AzureMLBatchExecution attività è stata introdotta nella versione di agosto 2015 di Azure SDK e di Azure PowerShell hello.

Se si desidera toocontinue utilizzando attività AzureMLBatchScoring hello, continuare a leggere questa sezione.  

### <a name="azure-ml-batch-scoring-activity-using-azure-storage-for-inputoutput"></a>Attività di assegnazione dei punteggi di batch di Azure ML che usa Archiviazione di Azure per l'input/output

```JSON
{
  "name": "PredictivePipeline",
  "properties": {
    "description": "use AzureML model",
    "activities": [
      {
        "name": "MLActivity",
        "type": "AzureMLBatchScoring",
        "description": "prediction analysis on batch input",
        "inputs": [
          {
            "name": "ScoringInputBlob"
          }
        ],
        "outputs": [
          {
            "name": "ScoringResultBlob"
          }
        ],
        "linkedServiceName": "MyAzureMLLinkedService",
        "policy": {
          "concurrency": 3,
          "executionPriorityOrder": "NewestFirst",
          "retry": 1,
          "timeout": "02:00:00"
        }
      }
    ],
    "start": "2016-02-13T00:00:00Z",
    "end": "2016-02-14T00:00:00Z"
  }
}
```

### <a name="web-service-parameters"></a>Parametri del servizio Web
toospecify valori per parametri del servizio Web, aggiungere un **typeProperties** sezione toohello **AzureMLBatchScoringActivty** sezione nella pipeline hello JSON, come illustrato nell'esempio seguente hello:

```JSON
"typeProperties": {
    "webServiceParameters": {
        "Param 1": "Value 1",
        "Param 2": "Value 2"
    }
}
```
È inoltre possibile utilizzare [funzioni di Data Factory](data-factory-functions-variables.md) per passare i valori per hello parametri del servizio Web come illustrato nell'esempio seguente hello:

```JSON
"typeProperties": {
    "webServiceParameters": {
       "Database query": "$$Text.Format('SELECT * FROM myTable WHERE timeColumn = \\'{0:yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(WindowStart, 0))"
    }
}
```

> [!NOTE]
> parametri del servizio Web Hello tra maiuscole e minuscole, verificare che i nomi di hello specificati nell'attività hello JSON corrispondano hello quelli esposti dal servizio Web hello.
>
>

## <a name="see-also"></a>Vedere anche
* [Post di blog di Azure: Guida introduttiva a Data Factory di Azure e ad Azure Machine Learning](https://azure.microsoft.com/blog/getting-started-with-azure-data-factory-and-azure-machine-learning-4/)

[adf-build-1st-pipeline]: data-factory-build-your-first-pipeline.md

[azure-machine-learning]: http://azure.microsoft.com/services/machine-learning/
