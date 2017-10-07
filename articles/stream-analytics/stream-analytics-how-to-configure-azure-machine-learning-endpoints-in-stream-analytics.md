---
title: gli endpoint di Azure Machine Learning aaaUse nel flusso Analitica | Documenti Microsoft
description: Funzioni definite dall'utente di Machine Learning in Analisi di flusso
keywords: 
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 406b258f-b8c2-4e55-953c-b7f84e8e5354
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 013b841ee85b1e0b6d8139a9ba0dde88fc3f8ad0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="machine-learning-integration-in-stream-analytics"></a>Integrazione di Machine Learning in Analisi di flusso
Flusso Analitica supporta funzioni definite dall'utente che richiamano gli endpoint di Machine Learning tooAzure. Supporto delle API REST per questa funzionalità è descritta in dettaglio in hello [libreria dell'API REST di flusso Analitica](https://msdn.microsoft.com/library/azure/dn835031.aspx). Questo articolo fornisce le informazioni supplementari necessarie per la corretta implementazione di questa funzionalità in Analisi di flusso. È stata pubblicata anche un'esercitazione che è disponibile [qui](stream-analytics-machine-learning-integration-tutorial.md).

## <a name="overview-azure-machine-learning-terminology"></a>Panoramica: Terminologia di Azure Machine Learning
Microsoft Azure Machine Learning fornisce uno strumento di collaborazione, trascinamento e rilascio, è possibile utilizzare toobuild, testare e distribuire soluzioni analitica predittiva sui dati. Questo strumento viene chiamato hello *Azure Machine Learning Studio*. studio Hello è toointeract utilizzati con hello risorse Machine Learning e compilare con facilità, test e alla progettazione di eseguire l'iterazione. Di seguito sono riportate le risorse e le rispettive definizioni.

* **Area di lavoro**: hello *dell'area di lavoro* è un contenitore che include tutte le altre risorse Machine Learning in un contenitore per la gestione e controllo.
* **Sperimentazione**: *esperimenti* vengono create dal DataSet tooutilize gli esperti di dati e di eseguire il training di un modello di machine learning.
* **Endpoint**: *endpoint* sono hello Azure Machine Learning caratteristiche tootake dell'oggetto utilizzato come input, applicare un modello di apprendimento automatico specificato e restituire l'output con punteggio.
* **Servizio Web di assegnazione dei punteggi**: un *servizio Web di assegnazione dei punteggi* è una raccolta di endpoint, come indicato sopra.

Ogni endpoint ha API per l'esecuzione batch e per l'esecuzione sincrona. Analisi di flusso usa l'esecuzione sincrona. nome del servizio specifico Hello è un [servizio richiesta/risposta](../machine-learning/machine-learning-consume-web-services.md) in Azure ml studio.

## <a name="machine-learning-resources-needed-for-stream-analytics-jobs"></a>Risorse di Machine Learning necessarie per i processi di analisi di flusso
Ai fini di hello di Analitica di flusso del processo di elaborazione, un endpoint di tipo richiesta/risposta, un [apikey](../machine-learning/machine-learning-connect-to-azure-machine-learning-web-service.md), e una definizione swagger tutti necessari per la corretta esecuzione. Flusso Analitica dispone di un endpoint aggiuntivo che costruisce l'url dell'endpoint swagger hello, Cerca l'interfaccia hello e restituisce un utente di toohello definizione di funzione definita dall'utente predefinito.

## <a name="configure-a-stream-analytics-and-machine-learning-udf-via-rest-api"></a>Configurare una funzione definita dall'utente di Analisi di flusso e di Machine Learning con l'API REST
Mediante le API REST è possibile configurare le funzioni di linguaggio macchina Azure toocall di processo. come indicato di seguito sono riportati i passaggi di Hello:

1. Creare un processo di Analisi di flusso.
2. Definire un input
3. Definire un output
4. Creare una funzione definita dall'utente
5. Scrivere una trasformazione di flusso Analitica che chiama hello funzione definita dall'utente
6. Avviare il processo di hello

## <a name="creating-a-udf-with-basic-properties"></a>Creazione di una funzione definita dall'utente con proprietà di base
Ad esempio, hello codice di esempio seguente viene creata una funzione scalare definita dall'utente denominato *newudf* che associa l'endpoint di Azure Machine Learning tooan. Si noti che hello *endpoint* (URI del servizio) sono disponibili nella pagina della Guida hello API per hello scelto servizio e hello *apiKey* sono reperibili nella pagina principale di servizi di hello.

````
    PUT : /subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.StreamAnalytics/streamingjobs/<streamingjobName>/functions/<udfName>?api-version=<apiVersion>  
````

Corpo della richiesta di esempio:  

````
    {
        "name": "newudf",
        "properties": {
            "type": "Scalar",
            "properties": {
                "binding": {
                    "type": "Microsoft.MachineLearning/WebService",
                    "properties": {
                        "endpoint": "https://ussouthcentral.services.azureml.net/workspaces/f80d5d7a77fb4b46bf2a30c63c078dca/services/b7be5e40fd194258796fb402c1958eaf/execute ",
                        "apiKey": "replacekeyhere"
                    }
                }
            }
        }
    }
````

## <a name="call-retrievedefaultdefinition-endpoint-for-default-udf"></a>Chiamare l'endpoint RetrieveDefaultDefinition per la funzione definita dall'utente predefinita
Una volta hello scheletro che funzione definita dall'utente viene creata una definizione completa di hello di hello che funzione definita dall'utente è necessaria. endpoint RetreiveDefaultDefinition Hello consente di ottenere definizione default hello per una funzione scalare che è l'endpoint di Azure Machine Learning tooan associato. payload Hello seguente richiede definizione di funzione definita dall'utente tooget hello default per una funzione scalare che è l'endpoint di Azure Machine Learning tooan associato. Non consente di specificare endpoint effettivo hello perché è già stato specificato durante la richiesta PUT. Flusso Analitica chiama endpoint hello fornito nella richiesta di hello se viene fornito in modo esplicito. In caso contrario, viene utilizzato hello uno stato a cui fa riferimento. Di seguito hello accetta definita un'unica stringa parametro (una frase) e restituisce un singolo output di tipo stringa che indica l'etichetta "sentiment" hello per la frase.

````
POST : /subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.StreamAnalytics/streamingjobs/<streamingjobName>/functions/<udfName>/RetrieveDefaultDefinition?api-version=<apiVersion>
````

Corpo della richiesta di esempio:  

````
    {
        "bindingType": "Microsoft.MachineLearning/WebService",
        "bindingRetrievalProperties": {
            "executeEndpoint": null,
            "udfType": "Scalar"
        }
    }
````

Un output di esempio dovrebbe essere simile al seguente.  

````
    {
        "name": "newudf",
        "properties": {
            "type": "Scalar",
            "properties": {
                "inputs": [{
                    "dataType": "nvarchar(max)",
                    "isConfigurationParameter": null
                }],
                "output": {
                    "dataType": "nvarchar(max)"
                },
                "binding": {
                    "type": "Microsoft.MachineLearning/WebService",
                    "properties": {
                        "endpoint": "https://ussouthcentral.services.azureml.net/workspaces/f80d5d7a77ga4a4bbf2a30c63c078dca/services/b7be5e40fd194258896fb602c1858eaf/execute",
                        "apiKey": null,
                        "inputs": {
                            "name": "input1",
                            "columnNames": [{
                                "name": "tweet",
                                "dataType": "string",
                                "mapTo": 0
                            }]
                        },
                        "outputs": [{
                            "name": "Sentiment",
                            "dataType": "string"
                        }],
                        "batchSize": 10
                    }
                }
            }
        }
    }
````

## <a name="patch-udf-with-hello-response"></a>Patch di funzione definita dall'utente con risposta hello
Ora hello funzione definita dall'utente devono essere aggiornati con risposta precedente hello, come illustrato di seguito.

````
PATCH : /subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.StreamAnalytics/streamingjobs/<streamingjobName>/functions/<udfName>?api-version=<apiVersion>
````

Corpo della richiesta (output da RetrieveDefaultDefinition):

````
    {
        "name": "newudf",
        "properties": {
            "type": "Scalar",
            "properties": {
                "inputs": [{
                    "dataType": "nvarchar(max)",
                    "isConfigurationParameter": null
                }],
                "output": {
                    "dataType": "nvarchar(max)"
                },
                "binding": {
                    "type": "Microsoft.MachineLearning/WebService",
                    "properties": {
                        "endpoint": "https://ussouthcentral.services.azureml.net/workspaces/f80d5d7a77ga4a4bbf2a30c63c078dca/services/b7be5e40fd194258896fb602c1858eaf/execute",
                        "apiKey": null,
                        "inputs": {
                            "name": "input1",
                            "columnNames": [{
                                "name": "tweet",
                                "dataType": "string",
                                "mapTo": 0
                            }]
                        },
                        "outputs": [{
                            "name": "Sentiment",
                            "dataType": "string"
                        }],
                        "batchSize": 10
                    }
                }
            }
        }
    }
````

## <a name="implement-stream-analytics-transformation-toocall-hello-udf"></a>Implementare flusso Analitica trasformazione toocall hello funzione definita dall'utente
Ora eseguire una query hello (qui denominata scoreTweet) per ogni evento di input e scrivere una risposta per l'output di tooan tale evento.  

````
    {
        "name": "transformation",
        "properties": {
            "streamingUnits": null,
            "query": "select *,scoreTweet(Tweet) TweetSentiment into blobOutput from blobInput"
        }
    }
````


## <a name="get-help"></a>Ottenere aiuto
Per assistenza, provare il [Forum di Analisi di flusso di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Passaggi successivi
* [Introduzione tooAzure flusso Analitica](stream-analytics-introduction.md)
* [Introduzione all'uso di Analisi dei flussi di Azure](stream-analytics-real-time-fraud-detection.md)
* [Ridimensionare i processi di Analisi dei flussi di Azure](stream-analytics-scale-jobs.md)
* [Informazioni di riferimento sul linguaggio di query di Analisi dei flussi di Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure](https://msdn.microsoft.com/library/azure/dn835031.aspx)
