---
title: i modelli di analitica testo aaaCreate in Azure Machine Learning Studio | Documenti Microsoft
description: Come analitica testo toocreate modelli in Azure Machine Learning Studio usando i moduli per la pre-elaborazione di testo, N-grammi o feature hashing
services: machine-learning
documentationcenter: 
author: rastala
manager: jhubbard
editor: 
ms.assetid: 08cd6723-3ae6-4e99-a924-e650942e461b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: roastala
ms.openlocfilehash: e3799f37ba54bb2ec8815ecf5ed34e145ffb20e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-text-analytics-models-in-azure-machine-learning-studio"></a>Creare modelli di analisi del testo in Azure Machine Learning Studio
È possibile utilizzare Azure Machine Learning toobuild e utilizzare i modelli di testo analitica. Questi modelli consentono di risolvere, ad esempio, problemi di classificazione dei documenti o analisi di valutazione.

In un esperimento di analisi del testo è necessario in genere:

1. Pulire e pre-elaborare i set di dati di testo
2. Estrarre i vettori di caratteristiche numeriche dal testo pre-elaborato
3. Addestrare il modello di classificazione o regressione
4. Assegnare un punteggio e convalidare il modello di hello
5. Distribuire hello modello tooproduction

In questa esercitazione si apprenderanno questi passaggi eseguendo un modello di analisi di valutazione mediante il set di dati di Amazon Book Reviews (vedere il documento di ricerca “Biographies, Bollywood, Boom-boxes and Blenders: Domain Adaptation for Sentiment Classification” di John Blitzer, Mark Dredze e Fernando Pereira; Association of Computational Linguistics (ACL), 2007). Questo set di dati è costituito da punteggi di recensione (1-2 o 4-5) e testo in formato libero. obiettivo Hello è punteggio di revisione hello toopredict: basso (1 - 2) o high (4-5).

È possibile trovare gli esperimenti trattati in questa esercitazione nella raccolta Cortana Intelligence:

[Stimare le recensioni dei libri](https://gallery.cortanaintelligence.com/Experiment/Predict-Book-Reviews-1)

[Stimare le recensioni dei libri - Esperimento predittivo](https://gallery.cortanaintelligence.com/Experiment/Predict-Book-Reviews-Predictive-Experiment-1)

## <a name="step-1-clean-and-preprocess-text-dataset"></a>Passaggio 1: Pulire e pre-elaborare i set di dati di testo
Iniziamo hello esperimento dividendo i punteggi di revisione hello in bucket minimo e massimo categorico tooformulate hello problema classificazione a due classi. Vengono usati i moduli [Edit Metadata](https://msdn.microsoft.com/library/azure/dn905986.aspx) e [Group Categorical Values](https://msdn.microsoft.com/library/azure/dn906014.aspx) (Valori di categoria del gruppo).

![Creazione dell'etichetta](./media/machine-learning-text-analytics-module-tutorial/create-label.png)

Quindi, si rimuovono hello testo tramite [pre-elaborazione di testo](https://msdn.microsoft.com/library/azure/mt762915.aspx) modulo. pulizia Hello riduce rumore hello nei set di dati hello, consentono di trovare hello funzionalità più importanti e migliorare hello sull'accuratezza del modello finale hello. Vengono rimosse le parole non significative: parole comuni, come articoli e preposizioni, nonché numeri, caratteri speciali, caratteri duplicati, indirizzi di posta elettronica e URL. È inoltre convertire toolowercase testo hello lemmatize parole hello e rilevare i delimitatori di frase quindi indicate da "|" simbolo di testo pre-elaborato.

![Preprocess Text](./media/machine-learning-text-analytics-module-tutorial/preprocess-text.png)

Cosa accade se si desidera un elenco di parole non significative personalizzato toouse? È possibile passarlo come input facoltativo. È inoltre possibile utilizzare sottostringhe di tooreplace espressione regolare sintassi personalizzate in c# e rimuovere parole da parte del discorso: sostantivi, verbi o aggettivi.

Dopo aver hello pre-elaborazione, è suddividere i dati di hello in training e set di test.

## <a name="step-2-extract-numeric-feature-vectors-from-pre-processed-text"></a>Passaggio 2: Estrarre vettori di caratteristiche numeriche dal testo pre-elaborato
toobuild un modello di dati di testo, in genere necessario tooconvert testo in formato libero in vettori di funzioni numeriche. In questo esempio, si usa [estrarre N-gramma funzionalità dal testo](https://msdn.microsoft.com/library/azure/mt762916.aspx) modulo tootransform hello toosuch formato dati. Il modulo accetta una colonna di parole separate da spazi e calcola un dizionario di parole, o n-grammi di parole, che vengono visualizzate nel set di dati. Quindi conta il numero di volte in cui ogni parola, o n-gramma, compare in ogni record e crea vettori di caratteristiche da questi conteggi. In questa esercitazione, N-gramma dimensioni too2, sono stati impostati i vettori di funzioni di includere singole parole e combinazioni di due parole successive.

![Estrazione degli n-grammi](./media/machine-learning-text-analytics-module-tutorial/extract-ngrams.png)

Si applica TF * conta IDF (termine frequenza Inverse Document Frequency) ponderazione tooN-gramma. Questo approccio aggiunge peso delle parole che vengono usati frequentemente in un singolo record, ma sono rari tra hello intero set di dati. Altre opzioni sono la ponderazione binaria, TF e grafica.

Funzioni di testo come queste sono spesso caratterizzate da alta dimensionalità. Ad esempio, se il corpo ha 100.000 parole univoche, lo spazio di funzioni avrà 100.000 dimensioni o più se vengono usati gli n-grammi. modulo di estrarre le funzionalità di N-gramma Hello offre un set di dimensionalità hello tooreduce di opzioni. È possibile scegliere le parole tooexclude valore predittivo significativo toohave breve o lungo o troppo comune o troppo frequenti. In questa esercitazione si escludono gli n-grammi che vengono visualizzati in meno di 5 record o in più dell'80% dei record.

Inoltre, è possibile utilizzare funzionalità selezione tooselect solo le funzionalità che sono più hello correlate con la destinazione di stima. Utilizziamo chi quadrato selezione tooselect 1000 funzionalità. È possibile visualizzare il vocabolario hello N-grammi delle parole selezionate facendo clic destro output di hello del modulo di estrazione N-grammi.

Come un approccio alternativo toousing estrarre N-gramma funzionalità, è possibile usare modulo Feature Hashing. Si noti tuttavia che [Feature Hashing](https://msdn.microsoft.com/library/azure/dn906018.aspx) non dispone di capacità integrate di selezione delle funzioni o di ponderazione TF*IDF.

## <a name="step-3-train-classification-or-regression-model"></a>Passaggio 3: Addestrare il modello di classificazione o regressione
Ora il testo hello è stato trasformato toonumeric funzionalità colonne. set di dati Hello contiene ancora le colonne stringa dalle fasi precedenti, permette di usare le colonne selezionate nel set di dati tooexclude li.

È quindi possibile utilizzare [Two-Class Logistic Regression](https://msdn.microsoft.com/library/azure/dn905994.aspx) toopredict alla destinazione: punteggio revisione alta o bassa. A questo punto, problema di analitica testo hello è stata trasformata in un problema di classificazione regolare. È possibile utilizzare gli strumenti di hello disponibili nel modello di Azure Machine Learning tooimprove hello. Ad esempio, è possibile sperimentare diversi classificatori toofind risultati il livello di accuratezza, assegnare o utilizzare hyperparameter ottimizzazione accuratezza hello tooimprove.

![Addestramento e assegnazione dei punteggi](./media/machine-learning-text-analytics-module-tutorial/scoring-text.png)

## <a name="step-4-score-and-validate-hello-model"></a>Passaggio 4: Assegnare un punteggio e convalidare il modello di hello
Come si potrebbe verificare modello con training hello? È il punteggio nel set di dati di hello test e valutare l'accuratezza di hello. Tuttavia, il modello di hello appreso vocabolario hello di N-grammi e i relativi pesi da hello training set. Pertanto, da utilizzare il vocabolario e i pesi durante l'estrazione di funzioni dai dati di test, come anziché vocabolario hello toocreating da zero. Pertanto, è aggiungere funzionalità di N-gramma estrarre modulo toohello punteggio ramo dell'esperimento hello, collegare hello output vocabolario dal ramo di training e impostare modalità vocabolario hello tooread sola. È inoltre disabilitare hello applicando un filtro di N-grammi per frequenza dall'impostazione istanza di hello too1 minimo e massimo too100% e disattivare la selezione di funzionalità hello.

Dopo aver hello colonna di testo in test di dati sono stati trasformati toonumeric colonne di funzioni, Microsoft esclude stringa hello come colonne nelle fasi precedenti nel ramo di training. È quindi utilizzare le stime di toomake modulo Score Model e accuratezza di hello tooevaluate modulo Evaluate Model.

## <a name="step-5-deploy-hello-model-tooproduction"></a>Passaggio 5: Distribuire hello modello tooproduction
modello di Hello è quasi pronti toobe distribuito tooproduction. Se viene distribuito come servizio Web, accetta una stringa di testo in formato libero come input e restituisce una stima "alta" o "bassa". Usa hello appreso N-gramma vocabolario tootransform hello testo toofeatures e training del modello di regressione logistica toomake una stima da tali funzionalità. 

tooset backup esperimento predittiva hello, è innanzitutto salvare vocabolario N-gramma hello come set di dati e hello training del modello di regressione logistica dal ramo di training hello dell'esperimento hello. Quindi, è salvare esperimento hello "Salva con nome" toocreate utilizzando un grafico dell'esperimento per esperimento predittiva. Si rimuove il modulo di suddivisione dei dati hello e ramo training hello da esperimento hello. È quindi connettere il vocabolario di N-gramma hello salvato in precedenza e modello tooExtract N-gramma funzionalità e moduli Score Model, rispettivamente. Rimuovere inoltre modulo Evaluate Model hello.

Si seleziona colonne nel set di dati modulo prima colonna di etichetta di testo pre-elaborazione modulo tooremove hello, inserire e deseleziona l'opzione "Aggiungi punteggio colonna toodataset" nel modulo di punteggio. In questo modo, servizio web hello non richiedere l'etichetta di hello tenta toopredict e echo non le funzionalità di input hello in risposta.

![Esperimento predittivo](./media/machine-learning-text-analytics-module-tutorial/predictive-text.png)

Ora abbiamo un esperimento che può essere pubblicato come servizio Web e chiamato mediante le API di richiesta-risposta o di esecuzione in batch.

## <a name="next-steps"></a>Passaggi successivi
Per informazioni sui moduli di analisi del testo, vedere la [documentazione su MSDN](https://msdn.microsoft.com/library/azure/dn905886.aspx).

