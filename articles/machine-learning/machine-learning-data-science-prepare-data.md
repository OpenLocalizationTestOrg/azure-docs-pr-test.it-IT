---
title: aaaClean e preparare i dati per Azure Machine Learning | Documenti Microsoft
description: "Pre-elaborazione e pulire dati tooprepare è per machine learning."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: bdf659ec-4881-4324-8b9c-747cbfa0c3cd
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: 3e3c3e4b0cfb9187f5820d7165e6ee1ea013ba02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tasks-tooprepare-data-for-enhanced-machine-learning"></a>Dati tooprepare di attività per l'apprendimento automatico avanzato
La pre-elaborazione e la pulizia dei dati rappresentano attività importanti che in genere devono essere eseguite prima di poter usare un set di dati in modo efficace per Machine Learning. I dati non elaborati sono fastidiosi, non affidabili e potrebbero non contenere alcuni valori. Utilizzare tali dati per la modellazione può produrre risultati fuorvianti. Queste attività fanno parte di hello Team Data Science processo (TDSP) e in genere seguono un'esplorazione iniziale di un set di dati utilizzato toodiscover e pre-elaborazione hello piano necessario. Per istruzioni sul processo TDSP hello più dettagliate, vedere hello procedure hello [processo di analisi scientifica dei dati di Team](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).

Pre-elaborazione e attività di pulizia, ad esempio attività di esplorazione dei dati di hello, possono essere eseguite in un'ampia gamma di ambienti, ad esempio SQL o Hive di Azure Machine Learning Studio e con vari strumenti e linguaggi, ad esempio R o Python, a seconda di dove i dati vengono modalità di formattazione memorizzato. Poiché TDSP è iterativa, queste attività possono essere eseguito in varie fasi del flusso di lavoro hello del processo di hello.

Questo articolo presenta alcuni concetti e attività di elaborazione dei dati che possono essere effettuati prima dell'inserimento dei dati in Azure Machine Learning.

Per un esempio di esplorazione dei dati e pre-elaborazione eseguita all'interno di Azure Machine Learning studio, vedere hello [pre-elaborazione dati in Azure Machine Learning Studio](https://azure.microsoft.com/documentation/videos/preprocessing-data-in-azure-ml-studio/) video.

## <a name="why-pre-process-and-clean-data"></a>Perché pre-elaborare e pulire i dati?
Raccolti da diverse origini dati reali e i processi e può contenere irregolarità o dati danneggiati compromettere la qualità di hello del set di dati hello. problemi di qualità dei dati in genere Hello che si verificano sono:

* **Dati incompleti**: nei dati mancano attributi o non sono presenti valori.
* **Dati fastidiosi**: i dati contengono record o outlier errati.
* **Dati incoerenti**: i dati contengono record in conflitto o discrepanze.

La qualità dei dati è un prerequisito per modelli predittivi di qualità. tooavoid "garbage in garbage out" e migliorare la qualità dei dati e pertanto le prestazioni del modello, è imperativo tooconduct un toospot schermata integrità dati dati problemi tempestivamente e decidere hello corrispondente l'elaborazione dati e operazioni di pulizia.

## <a name="what-are-some-typical-data-health-screens-that-are-employed"></a>Quali sono le tipiche analisi dell'integrità dei dati che vengono impiegate?
È possibile controllare la qualità generale hello delle controllando:

* numero di Hello **record**.
* numero di Hello **attributi** (o **funzionalità**).
* attributo Hello **tipi di dati** (nominale, ordinale o continuo).
* numero di Hello **valori mancanti**.
* **Correttezza del formato** dei dati di hello.
  * Se i dati di hello in TSV o CSV, verificare che i separatori di colonna hello e separatori di riga sempre correttamente separano di colonne e righe.
  * Se i dati di hello in formato HTML o XML, controllare se dati hello sono corretto in base a loro rispettivi standard.
  * L'analisi potrebbe inoltre essere necessaria in tooextract strutturate le informazioni sugli ordini dati strutturati o semistrutturati.
* **Record di dati incoerenti**. Controllo hello intervallo di valori consentiti. ad esempio, se i dati di hello contengano studente GPA, verificare se è hello GPA in hello designato intervallo, ad esempio 0 ~ 4.

Quando si verificano problemi con i dati, **passaggi di elaborazione** è necessario che spesso include la pulizia dei valori mancanti, normalizzazione dei dati, discretizzazione, tooremove l'elaborazione di testo e/o sostituire i caratteri incorporati che potrebbero influire sulla allineamento dei dati, misti tipi di dati in comune, campi e ad altri utenti.

**Azure Machine Learning utilizza dati tabulari in formato corretto**.  Se dati hello sono già in formato tabulare, pre-elaborazione di dati può essere eseguita direttamente con Azure Machine Learning in hello Machine Learning Studio.  Se i dati non sono in formato tabulare, ad esempio che si trova in XML, l'analisi potrebbe essere necessario nel modulo di tootabular dati hello tooconvert dell'ordine.  

## <a name="what-are-some-of-hello-major-tasks-in-data-pre-processing"></a>Quali sono alcune delle attività di rilievo hello pre-elaborazione di dati?
* **Pulizia dei dati**: compilare o inserire i valori mancanti, individuare e rimuovere dati e outlier che creano disturbo.
* **La trasformazione dei dati**: normalizzare le dimensioni tooreduce dati e rumore.
* **Riduzione dei dati**: esempi di record di dati o attributi per una gestione dei dati semplificata.
* **Discretizzazione dati**: Convert continua attributi attributi toocategorical per facilitare l'utilizzo con alcuni metodi di machine learning.
* **Pulizia del testo**: rimuovere i caratteri incorporati che potrebbero causare problemi di allineamento dei dati, ad esempio, schede incorporate in un file di dati separato da tabulazioni, nuove righe incorporate che potrebbero interrompere record ecc.

Hello sezioni seguenti descrivono in dettaglio alcuni di questi passaggi di elaborazione dei dati.

## <a name="how-toodeal-with-missing-values"></a>Come valori toodeal con mancante?
toodeal con valori mancanti, è consigliabile toofirst identificare il motivo di hello per i valori di problema di hello handle toobetter hello mancante. I metodi di gestione dei valori mancanti tipici sono:

* **Eliminazione**: rimuovere i record con valori mancanti
* **Sostituzione fittizia**: sostituire un valore mancante con un valore fittizio, ad esempio, *unknown* per valori categorici o 0 per valori numerici.
* **Significa sostituzione**: se i dati mancanti hello sono di tipo numerici, sostituire i valori mancanti hello con Media hello.
* **Sostituzione di frequente**: se i dati mancanti hello sono organizzato per categorie, sostituire i valori mancanti hello con elemento più frequente di hello
* **Sostituzione di regressione**: utilizzo di valori regressione metodo tooreplace mancanti con valori regrediti.  

## <a name="how-toonormalize-data"></a>Come toonormalize dati?
Dati normalizzazione Ridimensiona nuovamente i valori numerici tooa intervallo specificato. I metodi di normalizzazione dei dati più comuni includono:

* **Min-Max normalizzazione**: in modo lineare hello dati tooa intervallo trasformato, ad esempio compreso tra 0 e 1, dove hello il valore minimo è scalato too0 e too1 al valore massimo.
* **Normalizzazione del punteggio Z**: ridimensionare i dati in base ai media e deviazione standard: divisione hello differenza dati hello e hello Media per la deviazione standard di hello.
* **Scalabilità decimale**: scala dati hello per lo spostamento hello separatore decimale del valore di attributo hello.  

## <a name="how-toodiscretize-data"></a>Come toodiscretize dati?
Dati possono essere discretizzati convertendo attributi toonominal valori continui o intervalli. Ciò può essere fatto nei seguenti modi:

* **Creazione di contenitori di uguale larghezza**: dividere l'intervallo di hello di tutti i valori possibili di un attributo in gruppi di N di hello stessa dimensione e assegnare i valori hello che rientrano in una classe con il numero di bin hello.
* **Creazione di contenitori di uguale altezza**: dividere l'intervallo di hello di tutti i valori possibili di un attributo in gruppi di N, ognuno dei quali contiene hello stesso numero di istanze, quindi assegnare hello valori che rientrano in una classe con hello bin numero.  

## <a name="how-tooreduce-data"></a>Come tooreduce dati?
Esistono vari metodi tooreduce dimensioni dei dati di gestione dei dati più semplice. A seconda di dominio di dimensioni e hello dati, è possibile applicare hello dei seguenti metodi:

* **Registrare campionamento**: esempio hello i record di dati e scegliere solo sottoinsieme rappresentativo di hello dai dati hello.
* **Attributo campionamento**: selezionare solo un subset di attributi più importanti hello dai dati hello.  
* **Aggregazione**: suddividere i dati di hello in gruppi e archiviare i numeri di hello per ogni gruppo. Ad esempio, hello Ricavi giornalieri numeri di una catena di ristorante su hello 20 anni precedenti possono essere aggregati toomonthly tooreduce hello fatturato dei dati di hello.  

## <a name="how-tooclean-text-data"></a>Come dati di testo tooclean?
**I campi di testo nei dati tabulari** possono includere caratteri che influiscono sull'allineamento delle colonne e/o sui limiti dei record. Ad esempio, le schede incorporate in un file separato da tabulazioni possono causare il disallineamento delle colonne e i caratteri di nuove righe incorporate possono interrompere le righe del record. Gestione durante la scrittura o lettura di testo di codifica del testo non corretto comporta la perdita di tooinformation, accidentale introduzione di illeggibili caratteri, ad esempio, i valori null e può inoltre effetto testo l'analisi. Un'attenta analisi e la modifica potrebbe essere necessario nei campi di testo tooclean ordine corretto e/o dati strutturati tooextract dai dati di testo non strutturati o semistrutturati.

**L'esplorazione dei dati** offre una visualizzazione dati hello anticipata. Un numero di problemi di dati può essere rivelato durante questo passaggio e metodi corrispondenti possono essere applicati tooaddress tali problemi.  È importante tooask domande che cos'è l'origine di hello del problema hello e come problema hello potrebbe essere stati introdotti. Ciò consente inoltre di stabilire i passaggi di elaborazione dei dati hello toobe che è necessario prendere tooresolve li. tipo Hello di insights uno intende tooderive dai dati hello può essere anche usato tooprioritize hello l'elaborazione dati sforzo.

## <a name="references"></a>Riferimenti
> *Data Mining: Concepts and Techniques*, Third Edition, Morgan Kaufmann, 2011, Jiawei Han, Micheline Kamber, and Jian Pei
> 
> 

