---
title: aaaDebug il modello in Azure Machine Learning | Documenti Microsoft
description: Gli errori di toodebug generati dal modello di training e il modello di punteggio come moduli in Azure Machine Learning.
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 629dc45e-ac1e-4b7d-b120-08813dc448be
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bradsev;garye
ms.openlocfilehash: ee38ca8ce38d4fc7add5ba70c80ab9bb2ceaf1d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="debug-your-model-in-azure-machine-learning"></a>Debug del modello in Azure Machine Learning

Questo articolo descrive le cause possibili di hello perché uno dei seguenti due errori hello potrebbero essere presenti durante l'esecuzione di un modello:

* Hello [Train Model] [ train-model] modulo genera un errore 
* Hello [Score Model] [ score-model] modulo genera risultati non corretti 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="train-model-module-produces-an-error"></a>Il modulo Train Model genera un errore

![Immagine1](./media/machine-learning-debug-models/train_model-1.png)

Hello [Train Model] [ train-model] modulo prevede due input:

1. tipo di Hello del modello di machine learning dalla raccolta hello di modelli forniti da Azure Machine Learning.
2. dati di training con una colonna di etichetta specificata, che specifica Hello hello toopredict variabile (hello altre colonne vengono considerate toobe funzionalità).

Questo modulo può produrre un errore in hello seguenti casi:

1. colonna di etichetta Hello è stato specificato correttamente. Questa situazione può verificarsi se è selezionata più di una colonna come etichetta hello o un indice di colonna non è selezionato. Ad esempio, secondo caso hello verrà applicata se viene utilizzato un indice di colonna pari a 30 con un set di dati di input che ha solo 25 colonne.

2. Hello dataset non contiene tutte le colonne di funzionalità. Ad esempio, se hello di un set di dati dell'input ha una sola colonna, che è contrassegnata come colonna di etichetta hello, non vi sarà alcuna funzionalità con il modello di hello toobuild. In questo caso, hello [Train Model] [ train-model] modulo genera un errore.

3. Hello input set di dati (funzionalità o etichetta) contiene un numero infinito come valore.

## <a name="score-model-module-produces-incorrect-results"></a>Il modulo Classificazione del modello genera risultati non corretti

![Immagine2](./media/machine-learning-debug-models/train_test-2.png)

In genere esperimento per l'apprendimento supervisionato training/test, hello [dati divisi] [ split] modulo suddivide hello set di dati originale in due parti: una parte è il modello di hello tootrain utilizzato e viene utilizzata una parte tooscore come modello con training hello prestazioni. modello con training Hello è usato tooscore hello dati di test, dopo il quale i risultati di hello sono valutate toodetermine hello accuratezza del modello di hello.

Hello [Score Model] [ score-model] modulo richiede due input:

1. Un output di un modello con Training da hello [Train Model] [ train-model] modulo.
2. Un punteggio set di dati che è diverso dal set di dati hello utilizzato il modello di hello tootrain.

È possibile che, anche se ha esito positivo esperimento hello, hello del [Score Model] [ score-model] modulo genera risultati non corretti. Diversi scenari possono generare questo toohappen:

1. Se hello specificato etichetta è categorica e un modello di regressione è sottoposto a training sui dati hello, verrà prodotto un output non corretto da hello [Score Model] [ score-model] modulo. Questo si verifica perché la regressione richiede una variabile di risposta continua. In questo caso, sarebbe più adatta toouse un modello di classificazione. 

2. Analogamente, se un modello di classificazione viene eseguito il training su un set di dati con numeri a virgola mobile nella colonna di etichetta hello, può produrre risultati indesiderati. Questo si verifica perché la classificazione richiede una variabile di risposta discreta che ammette solo valori all'interno di un set di classi finito e solitamente di dimensioni ridotte.

3. Se hello punteggio set di dati non contiene tutti i modelli di hello tootrain di funzionalità utilizzate hello, hello [Score Model] [ score-model] genera un errore.

4. Se una riga nel set di dati di punteggio hello contiene un valore mancante o un valore infinito per tutte le sue funzionalità, hello [Score Model] [ score-model] non produrrà qualsiasi riga di output corrispondente toothat.

5. Hello [Score Model] [ score-model] può produrre output identici per tutte le righe nel set di dati di punteggio hello. Ciò può verificarsi, ad esempio, quando si tenta di classificazione utilizzando foreste delle decisioni, numero minimo di hello degli esempi per ogni nodo foglia sia toobe più hello numero di esempi di training disponibili.

<!-- Module References -->
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/

