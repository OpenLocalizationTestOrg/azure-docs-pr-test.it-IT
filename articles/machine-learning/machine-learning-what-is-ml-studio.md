---
title: "aaaWhat è Azure Machine Learning Studio? | Microsoft Docs"
description: Panoramica di Azure ML Studio, uno strumento di trascinamento per la creazione rapida di modelli da una libreria di algoritmi e moduli pronta per l'uso.
keywords: azure machine learning,azure ml, ml studio
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: e65c8fe1-7991-4a2a-86ef-fd80a7a06269
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: a25f2d9e75d088a37930de98240c6e14c9567fa4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-machine-learning-studio"></a>Informazioni su Azure Machine Learning Studio
Microsoft Azure Machine Learning Studio è uno strumento di collaborazione, trascinamento e rilascio, è possibile utilizzare toobuild, testare e distribuire soluzioni analitica predittiva sui dati. Machine Learning Studio pubblica i modelli come servizi Web che possono essere facilmente usati da applicazioni personalizzate o strumenti di Business Intelligence, ad esempio Excel.

Machine Learning Studio è il punto di incontro di scienza dei dati, analisi predittive, risorse cloud e dati.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="hello-machine-learning-studio-interactive-workspace"></a>Hello dell'area di lavoro interattiva di Machine Learning Studio
un modello di analisi predittiva toodevelop, si utilizzano in genere dati da una o più origini, trasformare e analizzare i dati tramite varie funzioni statistiche e la manipolazione dei dati e generare un set di risultati. Lo sviluppo di un modello come questo è un processo iterativo. Durante la modifica di hello varie funzioni e i relativi parametri, i risultati della convergono finché non è certi di disporre di un modello con training ed efficace.

**Azure Machine Learning Studio** fornisce tooeasily un'area di lavoro interattivi, visual compili, test e di eseguire l'iterazione su un modello di analisi predittiva. Di trascinamento e rilascio ***set di dati*** e analisi ***moduli*** in un'area di lavoro interattivo, che li connettono tooform insieme un ***sperimentare***, che è possibile eseguire in Machine Learning Studio. tooiterate sulla struttura del modello, esperimento hello, salvare una copia se si desidera, modificare ed eseguirlo nuovamente. Quando si è pronti, è possibile convertire il ***esperimento di training*** tooa ***esperimento predittiva***e quindi pubblicarlo come un ***servizio web*** in modo che il modello è possibile accedere tramite altri utenti.

Non è è richiesta alcuna programmazione, la connessione appena visivamente tooconstruct set di dati e i moduli del modello di analisi predittiva.

> [!TIP]
> toodownload e stampare un diagramma che offra una panoramica delle funzionalità di hello di Machine Learning Studio, vedere [diagramma della panoramica delle funzionalità di Azure Machine Learning Studio](machine-learning-studio-overview-diagram.md).
> 
> 

![Diagramma di Azure ML Studio: Creare esperimenti, leggere dati per molte origini, scrivere dati con punteggio, scrivere modelli.][ml-studio-overview]

## <a name="get-started-with-machine-learning-studio"></a>Introduzione a Machine Learning Studio
Quando si immette innanzitutto [Machine Learning Studio](https://studio.azureml.net) vedrai hello **Home** pagina. Da qui è possibile visualizzare documentazione, video e webinar, nonché trovare altre risorse utili.

Fare clic sul menu superiore sinistro hello ![Menu](media/machine-learning-what-is-ml-studio/menu.png) in cui sono disponibili numerose opzioni.

### <a name="cortana-intelligence"></a>Cortana Intelligence
Fare clic su **Cortana Intelligence** e verrà visualizzato toohello home page di hello [Cortana Intelligence Suite](https://www.microsoft.com/cloud-platform/cortana-intelligence-suite). Hello Cortana Intelligence Suite è di tipo data grande completamente gestito e avanzate tootransform suite analitica dei dati in azione intelligente. Vedere hello Suite home page per la documentazione completa, inclusi storie cliente.

### <a name="azure-machine-learning"></a>Azure Machine Learning
Sono disponibili due opzioni, **Home**, pagina hello in cui è stato avviato, e **Studio**.

Fare clic su **Studio** e verrà visualizzato toohello **Azure Machine Learning Studio**. Innanzitutto verrà chiesto toosign utilizzando l'account Microsoft o l'account aziendale o dell'istituto di istruzione. Una volta effettuato l'accesso, verrà visualizzato hello seguenti schede a sinistra di hello:

* **PROJECTS** (PROGETTI): raccolte di esperimenti, set di dati, blocchi appunti e altre risorse che rappresentano un solo progetto.
* **EXPERIMENTS** (ESPERIMENTI): esperimenti creati, eseguiti e salvati come bozze.
* **WEB SERVICES** (SERVIZI WEB): servizi Web distribuiti tramite gli esperimenti.
* **NOTEBOOKS** - notebook Jupyter creati.
* **DATASETS** (SET DI DATI): set di dati caricati in Studio.
* **TRAINED MODELS** - modelli sottoposti a training durante gli esperimenti e salvati in Studio.
* **IMPOSTAZIONI** -una raccolta di impostazioni che è possibile usare tooconfigure l'account e risorse.

### <a name="gallery"></a>Gallery
Fare clic su **raccolta** e verrà visualizzato toohello  **[Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com/)**. Raccolta Hello è una posizione in cui una community di esperti di dati e gli sviluppatori condividono soluzioni create tramite i componenti di hello Cortana Intelligence Suite.

Per ulteriori informazioni sulla raccolta hello, vedere [condivisione e individuare soluzioni in Cortana Intelligence Gallery hello](machine-learning-gallery-how-to-use-contribute-publish.md).

## <a name="components-of-an-experiment"></a>Componenti di un esperimento
Un esperimento costituito dal set di dati che forniscono dati tooanalytical moduli, che connettono contemporaneamente tooconstruct un modello di analisi predittiva. In particolare, un esperimento valido ha le caratteristiche seguenti:

* sperimentazione Hello ha almeno un set di dati e un modulo
* Set di dati può essere connesso toomodules solo
* I moduli possono essere connesso tooeither i set di dati o altri moduli
* Tutte le porte di input per i moduli devono avere dati toohello connessione flusso
* Tutti i parametri necessari per ogni modulo devono essere impostati.

È possibile creare un esperimento da zero oppure è possibile usare un esperimento di esempio esistente come modello. Per ulteriori informazioni, vedere [esperimenti di esempio copia toocreate esperimenti di machine learning nuovo](machine-learning-sample-experiments.md).

Per un esempio di creazione di un esperimento semplice, vedere [Creare un semplice esperimento in Azure Machine Learning Studio](machine-learning-create-experiment.md).

Per una procedura dettagliata più completa della creazione di una soluzione di analisi predittiva, vedere [Sviluppare una soluzione predittiva con Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md).

### <a name="datasets"></a>DATASETS
Un set di dati è dati che sono stato caricato tooMachine Learning Studio in modo che può essere utilizzato nel processo di modellazione hello. È incluso in Machine Learning Studio per tooexperiment con un numero di set di dati di esempio e, è possibile caricare più set di dati a seconda delle necessità. Ecco alcuni esempi di set di dati inclusi:

* **MPG data for various automobiles** : valori di consumo del carburante per le automobili identificate in base a numero di cilindri, potenza e così via.
* **Breast cancer data** : dati relativi alla diagnosi del tumore al seno.
* **Forest fires data** : dimensioni degli incendi boschivi nel nord-est del Portogallo.

Durante la compilazione di un esperimento è possibile scegliere dall'elenco dei set di dati disponibili a hello toohello a sinistra dell'area di disegno hello.

Per un elenco di set di dati di esempio incluso in Machine Learning Studio, vedere [utilizzare set di dati di esempio hello in Azure Machine Learning Studio](machine-learning-use-sample-datasets.md).

### <a name="modules"></a>Moduli
Un modulo è un algoritmo che è possibile applicare ai dati. Machine Learning Studio include un numero di moduli che vanno da dati in entrata funzioni tootraining, valutazione e convalida i processi. Ecco alcuni esempi di moduli inclusi:

* [Convertire tooARFF] [ convert-to-arff] -converte un set di dati serializzati di .NET tooAttribute-Relation File formato ARFF ().
* [Compute Elementary Statistics][elementary-statistics] (Calcola statistiche elementari): calcola le statistiche elementari come media, deviazione standard e così via.
* [Linear Regression][linear-regression] (Regressione lineare): crea un modello di regressione lineare online basato su valori descent con sfumatura.
* [Score Model][score-model] (Assegna un punteggio al modello): assegna un punteggio a un modello di classificazione sottoposto a training o di regressione.

Durante la compilazione di un esperimento è possibile scegliere dall'elenco di hello dei moduli disponibili toohello a sinistra dell'area di disegno hello.  

Un modulo possono esistere un set di parametri che è possibile utilizzare algoritmi interni del modulo di tooconfigure hello. Quando si seleziona un modulo nell'area di disegno hello, i parametri del modulo hello vengono visualizzati in hello **proprietà** toohello riquadro a destra dell'area di disegno hello. È possibile modificare i parametri di hello in tale tootune riquadro del modello.

Per alcuni Guida spostarsi all'interno della libreria di grandi dimensioni hello algoritmi di machine learning disponibili, vedere [come algoritmi toochoose per Microsoft Azure Machine Learning](machine-learning-algorithm-choice.md).

## <a name="deploying-a-predictive-analytics-web-service"></a>Distribuzione di un servizio Web di analisi predittiva
Quando il modello di analisi predittiva è pronto, è possibile distribuirlo come servizio Web direttamente da Machine Learning Studio. Per altre informazioni su questo processo, vedere [Distribuire un servizio Web di Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).

[ml-studio-overview]:./media/machine-learning-what-is-ml-studio/azure-ml-studio-diagram.jpg

<!-- Module References -->
[convert-to-arff]: https://msdn.microsoft.com/library/azure/62d2cece-d832-4a7a-a0bd-f01f03af0960/
[elementary-statistics]: https://msdn.microsoft.com/library/azure/3086b8d4-c895-45ba-8aa9-34f0c944d4d3/
[linear-regression]: https://msdn.microsoft.com/library/azure/31960a6f-789b-4cf7-88d6-2e1152c0bd1a/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
