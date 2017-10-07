---
title: domande di analisi scientifica dei dati aaaThe 5 - analisi scientifica dei dati per i principianti - Azure Machine Learning | Documenti Microsoft
description: Analisi scientifica dei dati per utenti meno esperti illustra i concetti di base 5 brevi video, a partire da analisi scientifica dei dati di hello 5 domande e risposte. Da Azure Machine Learning.
keywords: eseguire l'analisi scientifica dei dati, analisi scientifica dei dati per principianti, fondamenti dell'analisi scientifica dei dati, domande sull'analisi scientifica dei dati, video sull'analisi scientifica dei dati, introduzione all'analisi scientifica dei dati
services: machine-learning
documentationcenter: na
author: cjgronlund
manager: jhubbard
editor: cjgronlund
ms.assetid: a01f93ee-01eb-4afe-abbd-cfa035c119b0
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/13/2017
ms.author: cgronlun
ms.openlocfilehash: 6de0ca22556771a3044520d9ccc6771c3de78771
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="data-science-for-beginners-video-1-hello-5-questions-data-science-answers"></a>Analisi scientifica dei dati per i principianti 1 video: hello 5 domande risposte di analisi scientifica dei dati
Ottenere una scienza toodata introduzione da *analisi scientifica dei dati per i principianti* in cinque brevi video da un esperto di dati superiore. Questi video sono basilari, ma utili per chi è interessati a eseguire l'analisi scientifica dei dati oppure lavora con addetti a questa operazione.

In questo video prima è sui tipi di hello di domande che possono rispondere analisi scientifica dei dati. hello tooget meglio serie hello, guardare tutti. [Passare l'elenco toohello di video](#other-videos-in-this-series)
<br>

> [!VIDEO https://channel9.msdn.com/Shows/SupervisionNotRequired/8/player]
>
>

## <a name="other-videos-in-this-series"></a>Altri video della serie
*Analisi scientifica dei dati per i principianti* scienza di toodata una rapida introduzione richiede circa 25 minuti totali. Estrarre tutti i cinque video:

* Video 1: hello 5 domande risposte di analisi scientifica dei dati
* Video 2: [Verifica della preparazione dei dati per l'analisi scientifica dei dati](machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science.md) *(4 min e 56 sec)*
* Video 3: [Porre una domanda a cui è possibile rispondere con i dati](machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data.md) *(4 min e 17 sec)*
* Video 4: [Prevedere una risposta con un modello semplice](machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model.md) *(7 min e 42 sec)*
* Video 5: [copiare analisi scientifica dei dati di altre persone lavoro toodo](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) *(3 min 18 sec)*

## <a name="transcript-hello-5-questions-data-science-answers"></a>Trascrizione: hello 5 domande risposte di analisi scientifica dei dati
Salve! Pagina iniziale di serie di video toohello *analisi scientifica dei dati per i principianti*.

Analisi scientifica dei dati può essere difficoltosa, pertanto verrà presentata nozioni di base hello qui senza equazioni o gergo di programmazione.

In questo video prima parleremo "hello 5 domande data science le risposte."

Analisi scientifica dei dati vengono utilizzati i numeri e i nomi (noto anche come categorie o le etichette) toopredict le risposte tooquestions.

Potrebbe essere sorprendente, ma *esistono solo cinque domande a cui l'analisi scientifica dei dati risponde*:

* È A o B?
* È strano?
* In che quantità o in che numero?
* In che modo sono organizzati i dati?
* Qual è il prossimo passo da fare?

La risposta a ciascuna di queste domande viene fornita da una famiglia a parte di metodi di apprendimento automatico, detti algoritmi.

È utile toothink su un algoritmo come una recipe e i dati come ingredienti hello. Un algoritmo indica come toocombine e la combinazione di hello dati in ordine tooget una risposta. I computer sono simili ai frullatori. È di eseguire la maggior parte del lavoro hello dell'algoritmo hello e ciò accade è abbastanza veloce.

## <a name="question-1-is-this-a-or-b-uses-classification-algorithms"></a>Domanda 1: È A o B? usa gli algoritmi di classificazione
Iniziamo con domanda hello: È presente o B?

![Algoritmi di classificazione: È A o B?](./media/machine-learning-data-science-for-beginners-the-5-questions-data-science-answers/classification-algorithms.png)

Questa famiglia di algoritmi viene detta classificazione a due classi.

È utile per qualsiasi domanda che può avere solo due risposte possibili.

ad esempio:

* Questo tire non riuscirà in hello miglia 1.000 Avanti: Sì o no?
* Cosa porta più clienti: un coupon da $ 5 o uno sconto del 25%?

Questa domanda può anche essere tooinclude rephrased più di due opzioni: È presente A o B o C o D, e così via.?  Si tratta in questo caso della classificazione multiclasse ed è utile quando sono possibili più risposte o diverse migliaia di risposte. Classificazione multiclasse sceglie hello quello più probabile.

## <a name="question-2-is-this-weird-uses-anomaly-detection-algorithms"></a>Domanda 2: È strano? usa gli algoritmi di rilevamento delle anomalie
Hello domanda successiva analisi scientifica dei dati può rispondere è: È questa separazione? A questa domanda risponde una famiglia di algoritmi detta rilevamento delle anomalie.

![Algoritmi di rilevamento delle anomalie: È strano?](./media/machine-learning-data-science-for-beginners-the-5-questions-data-science-answers/anomaly-detection-algorithms.png)

Chi usa una carta di credito, conosce già i vantaggi del rilevamento delle anomalie. Della carta di credito analizza ai modelli di acquisto, in modo che si può inviare un avviso illecito toopossible. Addebiti "strani" potrebbero essere acquisti presso un negozio in cui non si effettuano compere abitualmente o acquisti di articoli eccezionalmente costosi.

Questa domanda può essere utile in molti modi. Ad esempio:

* Se si dispone di un'automobile con indicatori di pressione, potrebbe essere tooknow: È il misuratore di richieste di lettura normale?
* Se si sta monitorando hello internet, è opportuno tooknow: il messaggio da hello tipico internet?

Il rilevamento delle anomalie segnala eventi o comportamenti imprevisti o insoliti. Fornisce indicazioni in toolook per eventuali problemi.

## <a name="question-3-how-much-or-how-many-uses-regression-algorithms"></a>Domanda 3: In che quantità? o In che numero? usa algoritmi di regressione
Apprendimento inoltre possibile stimare molto tooHow risposte hello? o come numero? famiglia di algoritmi Hello che risponda a questa domanda viene chiamata una regressione.

![Algoritmi di regressione: In che quantità? o In che numero?](./media/machine-learning-data-science-for-beginners-the-5-questions-data-science-answers/regression-algorithms.png)

Gli algoritmi di regressione effettuano previsioni numeriche, ad esempio:

* Cosa verrà hello temperatura essere martedì successivo?  
* Come andrà il quarto trimestre di vendite?

Aiutano a rispondere a qualsiasi domanda che richiede informazioni numeriche.

## <a name="question-4-how-is-this-organized-uses-clustering-algorithms"></a>Domanda 4: In che modo sono organizzati i dati? usa gli algoritmi di clustering
Ultimi due domande di hello sono ora un po' più avanzato.

Talvolta si desidera toounderstand hello struttura di un set di dati, questa organizzazione? Per questa domanda, non ci sono esempi per cui si conoscono già i risultati.

Esistono molti modi tootease out struttura hello dei dati. Un approccio è il clustering. Separa i dati in "gruppi" naturali per un'interpretazione più semplice. Con il clustering non vi è un'unica risposta corretta.

![Algoritmi di clustering: In che modo sono organizzati i dati?](./media/machine-learning-data-science-for-beginners-the-5-questions-data-science-answers/clustering-algorithms.png)

Esempi comuni di domande di clustering sono:

* Quali visualizzatori come hello stessi tipi di filmati?
* I modelli di stampante non riuscire hello allo stesso modo?

Riuscendo a capire come sono organizzati i dati, è possibile comprendere meglio, e prevedere, comportamenti ed eventi.  

## <a name="question-5-what-should-i-do-now-uses-reinforcement-learning-algorithms"></a>Domanda 5: Qual è il prossimo passo da fare? usa gli algoritmi di apprendimento per rinforzo
Hello ultimo domanda: cosa devo fare ora? usa una famiglia di algoritmi detta apprendimento per rinforzo.

Apprendimento amplificazione è stato ispirato dalla modalità di risposta toopunishment e premi cervello hello del RAT e comprensibile. Questi algoritmi imparare da risultati e scegliere l'azione successiva hello.

In genere, learning amplificazione è ideale per i sistemi automatizzati che dispongono di molte toomake piccole decisioni senza intervento umano.

![Algoritmi di apprendimento per rinforzo: Qual è il prossimo passo da fare?](./media/machine-learning-data-science-for-beginners-the-5-questions-data-science-answers/reinforcement-learning-algorithms.png)

Le domande a cui risponde riguardano sempre l'azione da intraprendere, di solito da una macchina o un robot. Alcuni esempi:

* Se sono un sistema di controllo di temperatura un edificio: regolare temperatura hello o lasciare il campo in cui è?  
* Per un'automobile senza pilota: In caso di semaforo giallo, frenare o accelerare?  
* Per un vuoto robot: mantenere tale o tornare indietro ad addebitare i costi stazione toohello?

Gli algoritmi di apprendimento per rinforzo raccolgono i dati durante i processi, imparando dai tentativi e dagli errori.

In modo che, in grado di analisi scientifica dei dati di hello 5 domande.

## <a name="next-steps"></a>Passaggi successivi
* [Effettuare il primo esperimento di analisi scientifica dei dati con Machine Learning Studio](machine-learning-create-experiment.md)
* [Ottenere un tooMachine introduzione di apprendimento in Microsoft Azure](machine-learning-what-is-machine-learning.md)
