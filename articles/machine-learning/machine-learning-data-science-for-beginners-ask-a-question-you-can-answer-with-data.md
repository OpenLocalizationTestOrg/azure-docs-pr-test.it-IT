---
title: "aaaAsk può rispondere a una data di domanda - problemi di analisi scientifica dei dati - Azure Machine Learning | Documenti Microsoft"
description: Informazioni su come un'analisi scientifica dei dati acuto tooformulate domanda scienza dei dati per i principianti 3 video. Include un confronto delle domande di classificazione e regressione.
keywords: problemi di analisi scientifica dei dati, domande di analisi scientifica dei dati, formulare domande, domande di regressione, domande di classificazione, domanda ben strutturata
services: machine-learning
documentationcenter: na
author: cjgronlund
manager: jhubbard
editor: cjgronlund
ms.assetid: 5b9501e3-9964-417a-8ffc-8913103da77b
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/13/2017
ms.author: cgronlun
ms.openlocfilehash: 00c328f51e6d9ff6654b5966eb97d6762582f7e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="ask-a-question-you-can-answer-with-data"></a>Porre una domanda a cui è possibile rispondere con i dati
## <a name="video-3-data-science-for-beginners-series"></a>Video 3: Analisi scientifica dei dati per principianti
Informazioni su come tooformulate un problema di analisi scientifica dei dati in una domanda scienza dei dati per i principianti video 3. Questo video include un confronto di domande per gli algoritmi di classificazione e regressione.

hello tooget meglio serie hello, guardare tutti. [Passare l'elenco toohello di video](#other-videos-in-this-series)
<br>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Data-science-for-beginners-Ask-a-question-you-can-answer-with-data/player]
>
>

## <a name="other-videos-in-this-series"></a>Altri video della serie
*Analisi scientifica dei dati per i principianti* scienza di toodata una rapida introduzione in cinque brevi video.

* Video 1: [hello 5 domande risposte di analisi scientifica dei dati](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) *(5 min 14 sec)*
* Video 2: [Verifica della preparazione dei dati per l'analisi scientifica dei dati](machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science.md) *(4 min e 56 sec)*
* Video 3: Porre una domanda a cui è possibile rispondere con i dati
* Video 4: [Prevedere una risposta con un modello semplice](machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model.md) *(7 min e 42 sec)*
* Video 5: [copiare analisi scientifica dei dati di altre persone lavoro toodo](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) *(3 min 18 sec)*

## <a name="transcript-ask-a-question-you-can-answer-with-data"></a>Trascrizione: Porre una domanda a cui è possibile rispondere con i dati
Benvenuti toohello video terza serie hello "Analisi scientifica dei dati per utenti meno esperti."  

In questo video vengono forniti suggerimenti per formulare una domanda a cui è possibile rispondere con i dati.

È possibile ottenere informazioni da questo video, se si innanzitutto video hello due versioni precedenti di questa serie: "analisi scientifica dei dati di hello 5 domande possono rispondere" e "Is i dati sono pronti per l'analisi scientifica dei dati?"

## <a name="ask-a-sharp-question"></a>Porre una domanda ben strutturata
Abbiamo parlato sull'analisi scientifica dei dati è il processo di hello di utilizzo dei nomi (detti anche etichette o categorie) e numeri toopredict una domanda tooa di risposta. Ma non può essere qualsiasi domanda; ha toobe un *acuto domanda.*

Non dispone di una domanda vagamente toobe ha risposto con un nome o un numero. mentre lo è per una domanda ben strutturata.

Si immagini di trovare una lampada magica con un genio che risponde puntualmente a qualsiasi domanda. Ma è un qualunque informazione operazioni dannose, e si proverà a eseguire toomake la risposta come vagamente e confusi come è possibile farne. Si desidera toopin quest'ultimo verso il basso una domanda così solida che ha non è possibile contribuire ma indicano quali operazioni si desidera tooknow.

Se si tooask vagamente domande, ad esempio "Cosa accade toohappen con un titolo azionario?", può rispondere a qualunque informazione hello, "cambierà prezzo hello". È una risposta vera, ma non è molto utile.

Se tuttavia fosse tooask acuta domande come "Cosa my vendita prezzo azionario sarà settimana successiva?", hello qualunque informazione non è possibile aiutare ma consentono di uno specifico, rispondere e stimare un prezzo di vendita.

## <a name="examples-of-your-answer-target-data"></a>Esempi di risposta: dati di destinazione
Quando si formula una domanda, controllare toosee se sono presenti esempi di risposte hello nei dati.

Se la domanda è "Quale sarà il prezzo di vendita del mio titolo la prossima settimana?", è quindi presente che i dati includono la cronologia dei prezzi azionari hello toomake.

Se la domanda è "quali auto in my fleet toofail corso innanzitutto?" quindi abbiamo toomake che i dati sono incluse informazioni sugli errori precedenti.

![Dati di destinazione: esempi di risposta. Formulare una domanda di analisi scientifica dei dati.](./media/machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data/target-data.png)

Questi esempi di risposte sono detti destinazione. Una destinazione è ciò che stiamo tentando toopredict sui punti dati futuri, se si tratta di una categoria o un numero.

Se non si dispone di dati di destinazione, è necessario alcune tooget. Si sarà in grado di tooanswer la domanda senza di esso.

## <a name="reformulate-your-question"></a>Riformulare la domanda
In alcuni casi è possibile riformulare la tooget domanda una risposta più utile.

domanda Hello "è il punto dati A o B?" Consente di stimare categoria hello (o nome o l'etichetta) di un elemento. tooanswer, utilizzare un *algoritmo di classificazione*.

Hello domanda "Quanti?" o "Quanti?" prevede una quantità. tooanswer si utilizzi un *algoritmo di regressione*.

toosee come è possibile trasformare questi, diamo un'occhiata domanda hello, "quali notizia è lettore toothis più interessanti hello?" Richiede una stima di una singola opzione tra molte possibilità, in altre parole "È A o B o C o D?" e si userà un algoritmo di classificazione.

Ma, a questa domanda può essere tooanswer più semplice se si modifica la classe come "il livello di interesse è ogni storia in questo visualizzatore toothis elenco?" Ora è possibile assegnare a ogni articolo un punteggio numerico ed è articolo punteggi più alti di facile tooidentify hello. Si tratta di un riformulare della domanda di classificazione hello in una domanda di regressione o quanto?

![Riformulare la domanda. Domanda di classificazione e domanda di regressione.](./media/machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data/classification-question-vs-regression-question.png)

Come si porre che una domanda è un algoritmo di toowhich indicazione consente di ottenere una risposta.

Sono disponibili alcune famiglie di algoritmi: ad esempio hello quelli nel nostro esempio storia notizie - strettamente correlate. È possibile riformulare l'algoritmo di hello toouse domanda che fornisce risposte più utili di hello.

Ma più importanti, porre la domanda acuto - domanda hello che è possibile rispondere con i dati. E assicurarsi di avere tooanswer dati destra hello è.

Sono stati trattati alcuni principi di base per porre una domanda a cui è possibile rispondere con i dati.

Impossibile verificare toocheck out hello altri video in "Data Science per principianti" da Microsoft Azure Machine Learning.

## <a name="next-steps"></a>Passaggi successivi
* [Effettuare il primo esperimento di analisi scientifica dei dati con Machine Learning Studio](machine-learning-create-experiment.md)
* [Ottenere un tooMachine introduzione di apprendimento in Microsoft Azure](machine-learning-what-is-machine-learning.md)
