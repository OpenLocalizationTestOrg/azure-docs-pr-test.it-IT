---
title: una risposta con un semplice modello di regressione - Azure Machine Learning aaaPredict | Documenti Microsoft
description: Toocreate una regressione semplice come modello toopredict un prezzo di analisi scientifica dei dati per i principianti 4 video. Include una regressione lineare con i dati di destinazione.
keywords: creare un modello, modello semplice, previsione prezzi, modello di regressione semplice
services: machine-learning
documentationcenter: na
author: cjgronlund
manager: jhubbard
editor: cjgronlund
ms.assetid: a28f1fab-e2d8-4663-aa7d-ca3530c8b525
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/13/2017
ms.author: cgronlun
ms.openlocfilehash: d4270c2237c33b7e898b78a08b292bc9d62e49ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="predict-an-answer-with-a-simple-model"></a>Prevedere una risposta con un modello semplice
## <a name="video-4-data-science-for-beginners-series"></a>Video 4: Analisi scientifica dei dati per principianti
Informazioni su come toocreate un toopredict modello di regressione semplice hello prezzo di una forma di rombo scienza dei dati per i principianti 4 video. Verrà rappresentato un modello di regressione con i dati di destinazione.

hello tooget meglio serie hello, guardare tutti. [Passare l'elenco toohello di video](#other-videos-in-this-series)
<br>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/data-science-for-beginners-series-predict-an-answer-with-a-simple-model/player]
>
>

## <a name="other-videos-in-this-series"></a>Altri video della serie
*Analisi scientifica dei dati per i principianti* scienza di toodata una rapida introduzione in cinque brevi video.

* Video 1: [hello 5 domande risposte di analisi scientifica dei dati](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) *(5 min 14 sec)*
* Video 2: [Verifica della preparazione dei dati per l'analisi scientifica dei dati](machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science.md) *(4 min e 56 sec)*
* Video 3: [Porre una domanda a cui è possibile rispondere con i dati](machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data.md) *(4 min e 17 sec)*
* Video 4: Prevedere una risposta con un modello semplice
* Video 5: [copiare analisi scientifica dei dati di altre persone lavoro toodo](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) *(3 min 18 sec)*

## <a name="transcript-predict-an-answer-with-a-simple-model"></a>Trascrizione: Prevedere una risposta con un modello semplice
Benvenuti toohello quarto video in hello serie "Analisi scientifica dei dati per principianti". In questa occasione verrà creato un modello semplice e realizzata una previsione.

Un *modello* non è altro che una storia semplificata dei dati. Adesso spiegherò cosa intendo.

## <a name="collect-relevant-accurate-connected-enough-data"></a>Raccolta di dati rilevanti, accurati, connessi, in quantità sufficiente
Si immagini tooshop per una forma di rombo. Ho un anello che faceva parte nonna toomy con un'impostazione per un rombo 1,35 accento circonflesso e si desidera tooget un'idea di come relativo costo. Si acquisiscono un blocco note e penna in gioielleria hello e scrivere verso il basso prezzo hello di rombi hello in caso di hello e quanto essi valutare carato tutti. A partire da hello prima forma di rombo - relativo 1.01 carato e $7,366.

Ora scorrere e farlo per hello tutte le altri rombi nell'archivio di hello.

![Colonne di dati relativi ai diamanti](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/diamond-data.png)

L'elenco presenta quindi due colonne. Ciascuna colonna contiene un attributo diverso - peso in carati e prezzo - e ciascuna riga è un unico punto di dati che rappresenta un unico diamante.

In questo modo è stata creato un piccolo set di dati, ovvero una tabella. Si noti che questa tabella soddisfa i criteri di qualità:

* dati Hello **rilevanti** -peso è sicuramente correlati tooprice
* Ha **accurato** -è ricontrollato prezzi hello scritto verso il basso
* Sono **connessi** : nessuna delle colonne contiene spazi vuoti
* E, come vedremo, ha **sufficiente** tooanswer dati alla domanda

## <a name="ask-a-sharp-question"></a>Porre una domanda ben strutturata
Ora si sarà porre la domanda in modo acuto: "quante il costo toobuy un rombo accento circonflesso 1,35?"

In tale elenco avremo rest hello toouse del nostro tooget dati una domanda toohello risposta Web non dispone un rombo 1,35 accento circonflesso.

## <a name="plot-hello-existing-data"></a>Tracciare i dati esistenti hello
innanzitutto Hello che faremo è disegnare una linea orizzontale numero, un asse, pesi hello toochart chiamata. intervallo di Hello di pesi hello è too2 0, in modo ci sarà disegnare una linea che copre intervallo e inserire i segni di graduazione per ogni marcatore metà.

Successivamente viene disegnare un prezzo di hello toorecord asse verticale e connetterla asse orizzontale peso toohello. L'asse verticale sarà suddiviso in unità di dollari. A questo punto viene fuori un set di assi coordinati.

![Assi del peso e del prezzo](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/weight-and-price-axes.png)

Abbiamo tootake passare dati a questo punto è e trasformarlo in un *dispersione*. Si tratta di un set di dati numerici toovisualize consigliato.

Per punto dati prima di hello, abbiamo individuare una riga verticale alla carato 1.01. Poi, una linea orizzontale fino a $ 7.366. Laddove si intersecano, verrà disegnato un punto. Questo rappresenta il primo diamante.

Ora si scorrono ogni rombo nell'elenco e hello stessa operazione. Una volta terminato, questo è quello che si ottiene: un mucchio di punti, uno per ogni diamante.

![Grafico a dispersione](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/scatter-plot.png)

## <a name="draw-hello-model-through-hello-data-points"></a>Modello di hello disegno tramite i punti dati hello
Se si osserva squint e punti di hello, raccolta hello è una linea fat, fuzzy. Usando il pennarello è possibile tracciare una linea retta che la attraversi.

In questo modo si crea un *modello*. Considerare come tenendo reale hello e apportando una versione di cartoni animati semplicistico. Ora cartoni animati hello sono errato: riga hello non giunge a tutti i punti dati hello. ma è una semplificazione utile.

![Linea di regressione lineare](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/linear-regression-line.png)

fatto Hello che tutti i punti di hello non vengono sottoposti esattamente riga hello è accettabile. Gli esperti di dati viene illustrato questo pronunciando è hello modello - riga hello - e quindi ogni punto presenta alcuni *rumore* o *varianza* associato. È hello perfetto relazione sottostante ed è quindi avanzata, reale HelloWorld che aggiunge il rumore e ridurre le incertezze.

Poiché si sta tentando di domanda hello tooanswer *quanto?* si tratta di un *regressione*. E visto che viene usata una linea dritta, si tratta di una *regressione lineare*.

## <a name="use-hello-model-toofind-hello-answer"></a>Utilizzare risposte hello di hello modello toofind
Una volta pronto il modello, è possibile porgli la domanda: Quando costerà un diamante da 1,35 carati?

tooanswer alla domanda, si individuare carato 1,35 e tracciare una linea verticale. In linea del modello hello attraversa, abbiamo individuare un asse di dollaro toohello linea orizzontale. Va a colpire proprio i 10.000 dollari. Boom! Risposta hello: un rombo accento circonflesso 1,35 costa circa $10.000.

![Risposte hello sul modello hello](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/find-the-answer.png)

## <a name="create-a-confidence-interval"></a>Creare un intervallo di confidenza
È naturale toowonder come precisa è la stima. È utile tooknow se rombo accento circonflesso 1,35 hello sarà molto simile troppo$ 10.000 o molto superiore o inferiore. toofigure questo out, è possibile disegnare un elemento envelope retta di regressione hello che include la maggior parte dei punti di hello. La busta viene chiamata il nostro *intervallo di confidenza*: siamo certi piuttosto che i prezzi rientrano in questa busta, perché in hello precedente la maggior parte di essi. È possibile creare due linee orizzontali più da intersezione di riga accento circonflesso 1,35 hello hello superiore e inferiore di hello di tale envelope.

![intervallo di confidenza](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/confidence-interval.png)

Ora è possibile affermare qualcosa sull'intervallo di confidenza: suggerisce con fiducia che il prezzo di hello di accento circonflesso 1,35 rombo è circa $10.000 - ma potrebbe essere minimo di $8.000 e potrebbe essere a un massimo di $12.000.

## <a name="were-done-with-no-math-or-computers"></a>Ecco fatto, senza matematica, né computer
È stato fatto, quali gli esperti di dati di ricevimento dei pagamenti toodo e abbiamo appena disegnando:

* Abbiamo posto una domanda a cui è stato possibile rispondere con i dati
* È stato creato un *modello* usando una *regressione lineare*.
* È stata realizzata una *previsione*, completa di *intervallo di confidenza*

E non è stato utilizzato toodo matematiche o computer è.

Se fossero state necessarie ulteriori informazioni, ad esempio...

* Hello Taglia della forma di rombo hello
* variazioni di colore (come chiudere rombo hello è toobeing bianco)
* numero di Hello di inclusioni nella forma di rombo hello

...avremmo avuto più colonne. In quel caso, la matematica diventa utile. Se si dispone di più di due colonne, è toodraw rigido punti su carta. matematiche Hello consente si adattano perfettamente dati tooyour piano o riga.

E se al posto di una semplice manciata diamanti, si trattasse di duemila o due milioni, allora un lavoro al computer sarebbe molto più veloce.

Oggi, abbiamo parlato come regressione lineare toodo ed è resa una stima utilizzando i dati.

Impossibile verificare toocheck out hello altri video in "Data Science per principianti" da Microsoft Azure Machine Learning.

## <a name="next-steps"></a>Passaggi successivi
* [Effettuare il primo esperimento di analisi scientifica dei dati con Machine Learning Studio](machine-learning-create-experiment.md)
* [Ottenere un tooMachine introduzione di apprendimento in Microsoft Azure](machine-learning-what-is-machine-learning.md)
