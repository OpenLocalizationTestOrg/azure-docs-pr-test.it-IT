---
title: aaaIs dati pronti per l'analisi scientifica dei dati? Valutazione dei dati con Azure Machine Learning | Microsoft Docs
description: Informazioni su criteri hello 4 per dati toobe pronto per l'analisi scientifica dei dati. Analisi scientifica dei dati per i principianti video 2 include esempi concreti toohelp con la valutazione dei dati di base.
keywords: "dati rilevanti, valutare i dati, preparare i dati, criteri dei dati, compatibilità con i dati"
services: machine-learning
documentationcenter: na
author: cjgronlund
manager: jhubbard
editor: cjgronlund
ms.assetid: d502062c-da70-4b21-9054-0bfd9902612e
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/13/2017
ms.author: cgronlun
ms.openlocfilehash: ef6bb680ace771537157dbdd50a4ccce0a3eb7ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="is-your-data-ready-for-data-science"></a>Sono pronti i dati per l'analisi scientifica?
## <a name="video-2-data-science-for-beginners-series"></a>Video 2: Analisi scientifica dei dati per principianti
Informazioni su come tooevaluate toomake i dati che vengano soddisfatti i criteri di base toobe pronto per l'analisi scientifica dei dati.

hello tooget meglio serie hello, guardare tutti. [Passare l'elenco toohello di video](#other-videos-in-this-series)
<br>

> [!VIDEO https://channel9.msdn.com/Shows/SupervisionNotRequired/9/player]
>
>

## <a name="other-videos-in-this-series"></a>Altri video della serie
*Analisi scientifica dei dati per i principianti* scienza di toodata una rapida introduzione in cinque brevi video.

* Video 1: [hello 5 domande risposte di analisi scientifica dei dati](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) *(5 min 14 sec)*
* Video 2: Verifica della preparazione dei dati per l'analisi scientifica dei dati
* Video 3: [Porre una domanda a cui è possibile rispondere con i dati](machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data.md) *(4 min e 17 sec)*
* Video 4: [Prevedere una risposta con un modello semplice](machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model.md) *(7 min e 42 sec)*
* Video 5: [copiare analisi scientifica dei dati di altre persone lavoro toodo](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) *(3 min 18 sec)*

## <a name="transcript-is-your-data-ready-for-data-science"></a>Trascrizione: Sono pronti i dati per l'analisi scientifica?
Benvenuto troppo "è dati pronto per l'analisi scientifica dei dati?" Hello secondo video in serie hello *analisi scientifica dei dati per i principianti*.  

Prima di analisi scientifica dei dati è possibile assegnare si hello risposte desiderate, è necessario toogive alcuni toowork materie di alta qualità con. Esecuzione di una pizza, hello migliori hello gli ingredienti si avvia, hello meglio prodotto finale hello. 

## <a name="criteria-for-data"></a>Criteri per i dati
In tal caso, nel caso di hello di analisi scientifica dei dati, esistono alcuni ingredienti che è necessario toopull.

Sono fondamentali dati:

* Rilevanti
* Connesso
* Accurati
* Sufficiente toowork con

## <a name="is-your-data-relevant"></a>Sono rilevanti i dati?
In modo principio prima hello - è necessario che i dati rilevanti.

![Dati rilevanti vs. dati irrilevanti, valutare i dati](./media/machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science/relevant-and-irrelevant-data.png)

Esaminare la tabella hello a sinistra hello. Viene soddisfatta sette persone all'esterno delle barre di Boston, misurato loro livello alcole sangue, hello Red Sox battuta Media di un gioco ultima e il prezzo di hello di latte in hello più vicino al punto vendita.

Si tratta di dati del tutto legittimi. L'unico inconveniente è che non sono rilevanti. Non esiste alcuna relazione ovvia tra questi numeri. Se è stato assegnato hello prezzo corrente di latte e hello media battuta Red Sox, non è possibile si può immaginare contenuto alcole sangue.

Esaminare ora tabella hello a destra hello. Questo tempo è misurato corpo hello di massa e conteggiato svariate ogni persona avute bibite.  numeri di Hello in ogni riga sono ora rilevanti tooeach altri. Se ha fornito il numero di massa e hello corpo di limetta fresca ho, è possibile apportare una probabilità my sangue alcole contenuto.

## <a name="do-you-have-connected-data"></a>I dati a disposizione sono connessi?
principio Avanti Hello è dati connessa.

![Dati connessi vs. dati disconnessi: criteri dei dati, preparazione dei dati](./media/machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science/connected-vs-disconnected-data.png)

Ecco alcuni dati pertinenti qualità hello di hamburger: griglia temperatura peso ad e classificazione di cibo locale hello rivista. Ma si noti il gap di hello nella tabella hello hello sinistra.

Alcuni valori non sono presenti nella maggior parte dei set di dati. È comune fori toohave simile al seguente e sono disponibili modi toowork attorno a esse. Ma se è presente una quantità eccessiva mancante, i dati iniziano toolook come cheese Svizzera.

Se si esamina la tabella hello a sinistra di hello, è pertanto quantità di dati mancanti, è toocome rigido backup con qualsiasi tipo di relazione tra griglia peso temperatura e ad. Questo è un esempio di dati disconnessi.

Hello tabella a destra hello, tuttavia, è completo e un esempio di dati connessi - completo.

## <a name="is-your-data-accurate"></a>Sono accurati i dati?
Hello principio avanti che dobbiamo è la precisione. Ecco quattro destinazioni che si desidera toohit con frecce.

![Dati accurati vs. dati non accurati - criteri di dati](./media/machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science/inaccurate-vs-accurate-data.png)

Esaminare la destinazione hello in alto a destra hello. Abbiamo un raggruppamento di una stretta attorno a bullseye hello. Quello è naturalmente accurato. In modo anomalo, nella lingua hello dell'analisi scientifica dei dati, le prestazioni a destra di destinazione hello sottostanti vengano inoltre considerate accurate.

Se toomap centro hello di queste frecce, si vedrà che è molto simile toohello bullseye. frecce Hello si diffondono tutte intorno destinazione hello, in modo che si sono considerate non precise, ma è incentrate sul bullseye hello, in modo che si sono considerati accurati.

Esaminare ora destinazione alto-sinistra hello. le frecce sono molto vicine l'una all'altra, si tratta di un raggruppamento stretto. Ma sono precisi, ma sono corrette perché center hello è fuori bullseye hello. E, naturalmente, frecce hello nella destinazione nella parte inferiore sinistra hello sono corrette e imprecisa. Questo arciere deve fare più pratica.

## <a name="do-you-have-enough-data-toowork-with"></a>È sufficiente toowork dati con
Infine, principio #4 - dobbiamo toohave dati sufficienti.

![La quantità dei dati a disposizione è sufficiente per l'analisi? Valutazione dei dati](./media/machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science/barely-enough-data.png)

Si immagini che ciascun punto di dati nella tabella sia una pennellata in un dipinto. Se è installato solo alcuni di essi, disegno hello può essere piuttosto fuzzy - tootell disco rigido è ciò che è.

Se si aggiungono alcuni altri tratti pennello, il disegno avvia tooget un più nitida minimo.

Quando si dispone di poco sufficiente tracce, è possibile visualizzare solo sufficiente toomake alcune decisioni ampie. Si tratta di una posizione di che cui si desidera conoscere toovisit? C'è molta luce, l'acqua sembra limpida: sì, è il posto in cui andrò in vacanza.

Quando si aggiungono più dati, immagine hello diventa più chiara e per prendere decisioni più dettagliate. Ora esaminare hello tre hotel banca sinistro hello. Si conosce, mi piace davvero caratteristiche correlate all'architettura di hello di hello in primo piano hello. Disponibile, rimangano piano terzo hello.

Con i dati rilevanti, connesso, precisione, e sufficienti, si dispone di tutti gli ingredienti hello dobbiamo toodo alcune analisi scientifica dei dati di alta qualità.

Essere certi toocheck out hello altri video di quattro *analisi scientifica dei dati per i principianti* da Microsoft Azure Machine Learning.

## <a name="next-steps"></a>Passaggi successivi
* [Effettuare il primo esperimento di analisi scientifica dei dati con Machine Learning Studio](machine-learning-create-experiment.md)
* [Ottenere un tooMachine introduzione di apprendimento in Microsoft Azure](machine-learning-what-is-machine-learning.md)
