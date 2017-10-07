---
title: API rilevamento anomalie di Machine Learning aaaAzure | Documenti Microsoft
description: "API di rilevamento delle anomalie è un esempio compilato con Microsoft Azure Machine Learning che consente di rilevare anomalie nei dati della serie temporale con i valori numerici disposti in modo uniforme nel tempo."
services: machine-learning
documentationcenter: 
author: alokkirpal
manager: jhubbard
editor: cgronlun
ms.assetid: 52fafe1f-e93d-47df-a8ac-9a9a53b60824
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 06/05/2017
ms.author: alok;rotimpe
ms.openlocfilehash: ce153689b8ddb36b67a2ad3607d846ea83ebcf61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="machine-learning-anomaly-detection-api"></a>API di rilevamento delle anomalie di Machine Learning
## <a name="overview"></a>Panoramica
[API di rilevamento delle anomalie](https://gallery.cortanaintelligence.com/MachineLearningAPI/Anomaly-Detection-2) è un esempio compilato con Azure Machine Learning che consente di rilevare anomalie nei dati della serie temporale con i valori numerici disposti in modo uniforme nel tempo.

Questa API può rilevare i seguenti tipi di modelli anomali nei dati della serie temporale hello:

* **Tendenze positive e negative**: ad esempio, quando si monitora l'utilizzo della memoria di elaborazione, una tendenza verso l'alto può risultare interessante perché può indicare una perdita di memoria.
* **Modifiche dell'intervallo dinamico di valori hello**: ad esempio, durante il monitoraggio delle eccezioni hello generate da un servizio cloud, eventuali modifiche dell'intervallo dinamico di valori hello potrebbero indicare l'instabilità dello stato di hello del servizio di hello, e
* **Picchi e DIP**: ad esempio, durante il monitoraggio numero hello di errori di accesso in un servizio o il numero di estrazioni in un sito di e-commerce, picchi o DIP potrebbe indicare un comportamento anomalo.

Queste funzionalità di rilevamento di Machine Learning tengono traccia delle modifiche dei valori nel tempo e segnalano quelle in corso sotto forma di punteggi delle anomalie. Non richiedono ottimizzazione soglia ad hoc e i relativi punteggi possono essere tasso positivo false toocontrol utilizzato. rilevamento di anomalie Hello API risulta utile in diversi scenari, ad esempio il monitoraggio del servizio grazie al rilevamento di indicatori KPI nel tempo, l'utilizzo di monitoraggio tramite metriche, ad esempio numero di ricerche, un numero di clic, il monitoraggio delle prestazioni tramite contatori di memoria, CPU, file legge, e così via nel tempo.

offerta di rilevamento di anomalie Hello viene fornito con tooget strumenti utili per iniziare.

* Hello [applicazione web](http://anomalydetection-aml.azurewebsites.net/) consente di valutare e visualizzare i risultati di hello di rilevamento di anomalie API sui dati.

> [!NOTE]
> Provare la **soluzione IT Anomaly Insights** supportata da [questa API](https://gallery.cortanaintelligence.com/MachineLearningAPI/Anomaly-Detection-2)
> 
> tooget questa soluzione tooend end distribuito tooyour sottoscrizione di Azure <a href="https://gallery.cortanaintelligence.com/Solution/Anomaly-Detection-Pre-Configured-Solution-1" target="_blank"> **iniziare da qui >**</a>
> 
>

## <a name="api-deployment"></a>Distribuzione API
In hello toouse ordine API, è necessario distribuirlo tooyour sottoscrizione di Azure in cui verrà ospitato come servizio web di Azure Machine Learning.  È possibile farlo da hello [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/MachineLearningAPI/Anomaly-Detection-2).  Verrà distribuito due servizi Web di Azure ml (e le relative risorse) tooyour sottoscrizione di Azure - uno per il rilevamento di anomalie con rilevamento della stagionalità e uno senza rilevamento della stagionalità.  Una volta completata la distribuzione di hello, sarà in grado di toomanage le API da hello [servizi web di Azure ml](https://services.azureml.net/webservices/) pagina.  In questa pagina, si verrà essere in grado di toofind i percorsi di endpoint, le chiavi API, nonché esempi di codice per chiamare l'API di hello.  Le istruzioni più dettagliate sono disponibili [qui](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-manage-new-webservice).

## <a name="scaling-hello-api"></a>Scala hello API
Per impostazione predefinita, la distribuzione disporrà di un piano di fatturazione di sviluppo/test gratuito che include 1.000 operazioni e 2 ore di calcolo al mese.  È possibile aggiornare il piano tooanother in base alle esigenze.  Sono disponibili dettagli sui prezzi di hello di piani diversi [qui](https://azure.microsoft.com/en-us/pricing/details/machine-learning/) in "Prezzi di API Web di produzione".

## <a name="managing-aml-plans"></a>Gestione dei piani AML 
È possibile gestire il piano di fatturazione [qui](https://services.azureml.net/plans/).  nome del piano di Hello si baserà sul nome del gruppo di risorse hello che scelto durante la distribuzione di API hello e una stringa che rappresenta la sottoscrizione tooyour univoco.  Istruzioni su come tooupgrade il piano sono disponibili [qui](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-manage-new-webservice) nella sezione "Gestione dei piani di fatturazione" hello.

## <a name="api-definition"></a>Definizione dell'API
servizio web Hello fornisce un'API basata su REST su HTTPS che possono essere utilizzati in modi diversi, ad esempio un web o applicazione per dispositivi mobili, R, Python, Excel, e così via.  Si invia il servizio di toothis ora serie dati tramite una chiamata API REST e l'esecuzione di una combinazione di tipi anomalie tre hello descritto di seguito.

## <a name="calling-hello-api"></a>Chiamata API hello
In hello toocall ordine API, sarà necessario posizione dell'endpoint tooknow hello e la chiave API.  Entrambi questi elementi, insieme al codice di esempio per la chiamata API hello, sono disponibili da hello [servizi web di Azure ml](https://services.azureml.net/webservices/) pagina.  Passare API toohello desiderato e quindi fare clic su hello "Consumare" scheda toofind li.  Si noti che è possibile chiamare l'API di hello come un'API Swagger (ad esempio con il parametro URL hello `format=swagger`) o come un non - Swagger API (ad esempio senza hello `format` parametro URL).  codice di esempio Hello utilizza il formato di Swagger hello.  Di seguito viene riportato un esempio di richiesta e risposta in formato non Swagger.  Questi esempi sono endpoint stagionalità toohello.  endpoint non stagionalità Hello è simile.

### <a name="sample-request-body"></a>Corpo della richiesta di esempio
richiesta di Hello contiene due oggetti: `Inputs` e `GlobalParameters`.  Nella richiesta di esempio hello riportato di seguito, alcuni parametri vengono inviati in modo esplicito mentre altri no (scorrere verso il basso per un elenco completo dei parametri per ogni endpoint).  Parametri che non vengono inviati in modo esplicito nella richiesta di hello verranno utilizzati i valori predefiniti di hello specificati di seguito.

    {
                "Inputs": {
                        "input1": {
                                "ColumnNames": ["Time", "Data"],
                                "Values": [
                                        ["5/30/2010 18:07:00", "1"],
                                        ["5/30/2010 18:08:00", "1.4"],
                                        ["5/30/2010 18:09:00", "1.1"]
                                ]
                        }
                },
        "GlobalParameters": {
            "tspikedetector.sensitivity": "3",
            "zspikedetector.sensitivity": "3",
            "bileveldetector.sensitivity": "3.25",
            "detectors.spikesdips": "Both"
        }
    }

### <a name="sample-response"></a>Risposta di esempio
Si noti che, in hello toosee ordine `ColumnNames` campo, è necessario includere `details=true` come parametro URL nella richiesta.  Vedere le tabelle di hello sotto per hello significato ciascuno di questi campi.

    {
        "Results": {
            "output1": {
                "type": "table",
                "value": {
                    "Values": [
                        ["5/30/2010 6:07:00 PM", "1", "1", "0", "0", "-0.687952590518378", "0", "-0.687952590518378", "0", "-0.687952590518378", "0"],
                        ["5/30/2010 6:08:00 PM", "1.4", "1.4", "0", "0", "-1.07030497733224", "0", "-0.884548154298423", "0", "-1.07030497733224", "0"],
                        ["5/30/2010 6:09:00 PM", "1.1", "1.1", "0", "0", "-1.30229513613974", "0", "-1.173800281031", "0", "-1.30229513613974", "0"]
                    ],
                    "ColumnNames": ["Time", "OriginalData", "ProcessedData", "TSpike", "ZSpike", "BiLevelChangeScore", "BiLevelChangeAlert", "PosTrendScore", "PosTrendAlert", "NegTrendScore", "NegTrendAlert"],
                    "ColumnTypes": ["DateTime", "Double", "Double", "Double", "Double", "Double", "Int32", "Double", "Int32", "Double", "Int32"]
                }
            }
        }
    }


## <a name="score-api"></a>API Score
Hello API di punteggio viene utilizzato per l'esecuzione di rilevamento di anomalie in dati della serie temporale non stagionali. Hello API esegue un numero di rilevatori di anomalie sui dati hello e restituisce i punteggi di anomalie. Figura Hello seguente mostra un esempio di anomalie che hello che può rilevare l'API di punteggio. Questa serie temporale presenta due modifiche di livello distinte e 3 picchi. punti di Hello rosso mostrano il tempo di hello in cui hello modifica del livello viene rilevato, mentre punti hello nero mostrano picchi hello rilevato.
![API Score][1]

### <a name="detectors"></a>Funzionalità di rilevamento
rilevamento di anomalie Hello API supporta i rilevatori in ampie 3 categorie. Informazioni dettagliate sulla specifici parametri di input e output per ogni tipo di rilevamento sono reperibile in hello nella tabella seguente.

| Categoria di rilevamento | Funzionalità di rilevamento | Descrizione | Parametri di input | Output |
| --- | --- | --- | --- | --- |
| Rilevamento picchi |Rilevamento picchi TSpike |Rilevare picchi e DIP in base a hello distante valori sono compresi tra i primo e il terzi quartile |*tspikedetector.Sensitivity:* accetta il valore intero nell'intervallo di hello predefinito di 1 a 10: 3; I valori più alti intercetterà ulteriori valori estremi, rendendo in tal modo meno sensibili |TSpike: valori binari, '1' se viene rilevato un picco o una flessione. In caso contrario '0'. |
| Rilevamento picchi | Rilevamento picchi ZSpike |Rilevare tali picchi o DIP in base a datapoints hello fino a che punto sono rispetto alla relativa Media |*zspikedetector.Sensitivity:* accettare il valore intero nell'intervallo di hello predefinito di 1 a 10: 3; I valori più alti intercetterà ulteriori valori estremi, rendendo meno sensibili |ZSpike: valori binari, '1' se viene rilevato un picco o una flessione. In caso contrario '0'. | |
| Rilevamento di tendenza lenta |Rilevamento di tendenza lenta |Rilevare lenta tendenza positiva in base alle hello set sensibilità |*trenddetector.Sensitivity:* soglia sul punteggio di rilevamento (impostazione predefinita: 3.25, 3.25-5 è un intervallo ragionevole di tooselect da; hello superiore hello meno sensibile) |tscore: numero mobile che rappresenta il punteggio dell'anomalia nella tendenza. |
| Rilevamento della modifica di livello | Rilevamento bidirezionale della modifica di livello |Rilevare la modifica sia verso l'alto e verso il basso livello in base alle hello set sensibilità |*bileveldetector.Sensitivity:* soglia sul punteggio di rilevamento (impostazione predefinita: 3.25, 3.25-5 è un intervallo ragionevole di tooselect da; hello superiore hello meno sensibile) |rpscore: numero mobile che rappresenta il punteggio dell'anomalia nella modifica di livello verso l'alto e verso il basso. | |

### <a name="parameters"></a>parameters
Informazioni più dettagliate su questi parametri di input sono elencate nella tabella hello riportata di seguito:

| Parametri di input | Descrizione | Impostazione predefinita | Tipo | Intervallo valido | Intervallo consigliato |
| --- | --- | --- | --- | --- | --- |
| detectors.historyWindow |Cronologia, in numero di punti dati, usata per il calcolo del punteggio delle anomalie |500 |integer |10-2000 |In base alle serie temporali. |
| detectors.spikesdips | Se toodetect solo picchi, solo DIP, o entrambi |Entrambi |enumerato |Entrambi, picchi e flessioni |Entrambi |
| bileveldetector.sensitivity |Sensibilità per il rilevamento delle modifiche di livello bidirezionali. |3.25 |double |Nessuna |3.25-5 (Meno valori, maggiore sensibilità) |
| trenddetector.sensitivity |Sensibilità per il rilevamento di tendenza positiva. |3.25 |double |Nessuna |3.25-5 (Meno valori, maggiore sensibilità) |
| tspikedetector.sensitivity |Sensibilità per il rilevamento di picchi TSpike. |3 |integer |1-10 |3-5 (Minori sono i valori, maggiore è la sensibilità) |
| zspikedetector.sensitivity |Sensibilità per il rilevamento di picchi ZSpike |3 |integer |1-10 |3-5 (Minori sono i valori, maggiore è la sensibilità) |
| postprocess.tailRows |Numero di dati più recenti hello punta toobe mantenuti nei risultati di output di hello |0 |numero intero |0 (mantenere tutti i punti dati), o specificare un numero di punti tookeep nei risultati |N/D |

### <a name="output"></a>Output
Hello API alimentato rilevatori di tutti i dati della serie temporale e restituisce i punteggi di anomalie e gli indicatori di picco binario per ogni punto nel tempo. tabella Hello riportata di seguito sono elencati gli output di hello API. 

| outputs | Descrizione |
| --- | --- |
| Time |Timestamp di dati non elaborati o dati aggregati (e/o) attribuiti se viene applicata l'aggregazione (e/o) l'attribuzione di dati mancanti. |
| Dati |Valori di dati non elaborati o dati aggregati (e/o) attribuiti se viene applicata l'aggregazione (e/o) l'attribuzione di dati mancanti. |
| Tspike |Indicatore binarie tooindicate se rileva un picco Rilevatore TSpike |
| Zspike |Indicatore binarie tooindicate se rileva un picco Rilevatore ZSpike |
| rpscore |Numero mobile che rappresenta il punteggio dell'anomalia nella modifica di livello bidirezionale. |
| rpalert |il valore di 1/0 che indica il livello bidirezionale è modificare anomalie in base a sensibilità input hello |
| tscore |Numero mobile che rappresenta il punteggio dell'anomalia nella tendenza positiva. |
| talert |il valore di 1/0 indica vi è anomalie una tendenza positiva in base a sensibilità input hello |

## <a name="scorewithseasonality-api"></a>API ScoreWithSeasonality
Hello API ScoreWithSeasonality viene utilizzato per l'esecuzione di rilevamento di anomalie in serie temporale che dispongono di modelli stagionali. Questa API è deviazioni toodetect utili nei modelli stagionali.  
Hello figura riportata di seguito viene illustrato un esempio di anomalie, rilevato in una serie temporale stagionali. serie temporale Hello ha un picco (hello 1 punto nero), due DIP (punto nero 2nd hello e uno alla fine di hello) e una modifica del livello (punto rosso). Si noti che entrambi hello dip interno hello delle serie temporali hello e modifica del livello di hello solo presentano dopo la rimozione di componenti stagionali dalla serie hello.
![Stagionalità API][2]

### <a name="detectors"></a>Funzionalità di rilevamento
i rilevatori Hello nell'endpoint stagionalità hello sono simile toohello quelli nell'endpoint non stagionalità hello, ma con nomi di parametro leggermente diversi (elencati di seguito).

### <a name="parameters"></a>parameters

Informazioni più dettagliate su questi parametri di input sono elencate nella tabella hello riportata di seguito:

| Parametri di input | Descrizione | Impostazione predefinita | Tipo | Intervallo valido | Intervallo consigliato |
| --- | --- | --- | --- | --- | --- |
| preprocess.aggregationInterval |Intervallo in secondi per l'aggregazione di serie temporali di input. |0, non viene eseguita alcuna aggregazione. |integer |0: ignora l'aggregazione. In caso contrario > 0. |giorno too1 5 minuti, dipendente di serie temporali |
| preprocess.aggregationFunc |Funzione utilizzata per aggregare i dati in hello specificato AggregationInterval |mean |enumerato |mean, sum, length |N/D |
| preprocess.replaceMissing |Dati mancanti tooimpute utilizzati valori |lkv (ultimo valore noto) |enumerato |zero, lkv, mean |N/D |
| detectors.historyWindow |Cronologia, in numero di punti dati, usata per il calcolo del punteggio delle anomalie |500 |integer |10-2000 |In base alle serie temporali. |
| detectors.spikesdips | Se toodetect solo picchi, solo DIP, o entrambi |Entrambi |enumerato |Entrambi, picchi e flessioni |Entrambi |
| bileveldetector.sensitivity |Sensibilità per il rilevamento delle modifiche di livello bidirezionali. |3.25 |double |Nessuna |3.25-5 (Meno valori, maggiore sensibilità) |
| postrenddetector.sensitivity |Sensibilità per il rilevamento di tendenza positiva. |3.25 |double |Nessuna |3.25-5 (Meno valori, maggiore sensibilità) |
| negtrenddetector.sensitivity |Sensibilità per il rilevamento di tendenza negativa. |3.25 |double |Nessuna |3.25-5 (Meno valori, maggiore sensibilità) |
| tspikedetector.sensitivity |Sensibilità per il rilevamento di picchi TSpike. |3 |integer |1-10 |3-5 (Minori sono i valori, maggiore è la sensibilità) |
| zspikedetector.sensitivity |Sensibilità per il rilevamento di picchi ZSpike |3 |integer |1-10 |3-5 (Minori sono i valori, maggiore è la sensibilità) |
| seasonality.enable |Se analysis stagionalità toobe avviene |true |boolean |true, false |In base alle serie temporali. |
| seasonality.numSeasonality |Numero massimo di cicli periodica toobe rilevato |1 |integer |1, 2 |Da 1 a 2 |
| seasonality.transform |Se i componenti stagionali (e) di tendenza devono essere rimossi prima di applicare il rilevamento delle anomalie. |deseason |enumerato |none, deseason, deseasontrend |N/D |
| postprocess.tailRows |Numero di dati più recenti hello punta toobe mantenuti nei risultati di output di hello |0 |numero intero |0 (mantenere tutti i punti dati), o specificare un numero di punti tookeep nei risultati |N/D |

### <a name="output"></a>Output
Hello API alimentato rilevatori di tutti i dati della serie temporale e restituisce i punteggi di anomalie e gli indicatori di picco binario per ogni punto nel tempo. tabella Hello riportata di seguito sono elencati gli output di hello API. 

| outputs | Descrizione |
| --- | --- |
| Time |Timestamp di dati non elaborati o dati aggregati (e/o) attribuiti se viene applicata l'aggregazione (e/o) l'attribuzione di dati mancanti. |
| OriginalData |Valori di dati non elaborati o dati aggregati (e/o) attribuiti se viene applicata l'aggregazione (e/o) l'attribuzione di dati mancanti. |
| ProcessedData |Uno dei seguenti hello: <ul><li>Serie temporali regolate in base alla stagionalità in caso di rilevamento di una stagionalità significativa e di selezione dell'opzione deseason</li><li>Serie temporali regolate in base alla stagionalità e senza tendenza, se è stata rilevata una stagionalità significativa ed è selezionata l'opzione deseasontrend</li><li>in caso contrario, è hello come OriginalData</li> |
| Tspike |Indicatore binarie tooindicate se rileva un picco Rilevatore TSpike |
| Zspike |Indicatore binarie tooindicate se rileva un picco Rilevatore ZSpike |
| BiLevelChangeScore |Numero mobile che rappresenta il punteggio dell'anomalia nella modifica di livello |
| BiLevelChangeAlert |1/0 valore che indica che vi è un'anomalie di modifica del livello in base a sensibilità input hello |
| PosTrendScore |Numero mobile che rappresenta il punteggio dell'anomalia nella tendenza positiva. |
| PosTrendAlert |il valore di 1/0 indica vi è anomalie una tendenza positiva in base a sensibilità input hello |
| NegTrendScore |Numero mobile che rappresenta il punteggio dell'anomalia nella tendenza negativa |
| NegTrendAlert |il valore di 1/0 indica vi è anomalie una tendenza negativa in base a sensibilità input hello |

[1]: ./media/machine-learning-apps-anomaly-detection-api/anomaly-detection-score.png
[2]: ./media/machine-learning-apps-anomaly-detection-api/anomaly-detection-seasonal.png

