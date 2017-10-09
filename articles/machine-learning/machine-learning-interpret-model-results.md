---
title: risultati del modello aaaInterpret in Machine Learning | Documenti Microsoft
description: Come parametro ottimale di toochoose hello impostato per l'utilizzo di un algoritmo e la visualizzazione modello di punteggio restituisce.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 6230e5ab-a5c0-4c21-a061-47675ba3342c
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 52161b1aa5ff3e7a63fc4b1bfb7c5e354eabcc50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="interpret-model-results-in-azure-machine-learning"></a>Interpretare i risultati dei modelli in Azure Machine Learning
Questo argomento viene illustrato come toovisualize e interpretare i risultati di stima in Azure Machine Learning Studio. Dopo aver eseguito il training un modello ed eseguite stime su di esso ("con punteggio modello hello"), è necessario toounderstand e interpretare i risultati di stima hello.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

In Azure Machine Learning esistono quattro tipi principali di modelli di apprendimento automatico:

* classificazione
* clustering
* regressione
* sistemi di raccomandazione

i moduli di Hello utilizzati per la stima nella parte superiore di questi modelli sono:

* Modulo [Score Model][score-model] per la classificazione e la regressione
* [Assegnare tooClusters] [ assign-to-clusters] modulo per il clustering
* Modulo [Score Matchbox Recommender][score-matchbox-recommender] per i sistemi di raccomandazione

Questo documento illustra come stima toointerpret i risultati per ognuno di questi moduli. Per una panoramica di questi moduli, vedere [come toochoose parametri toooptimize algoritmi in Azure Machine Learning](machine-learning-algorithm-parameters-optimize.md).

Questo argomento illustra l'interpretazione delle stime, non la valutazione dei modelli. Per ulteriori informazioni su come tooevaluate il modello, vedere [tooevaluate come modello di prestazioni in Azure Machine Learning](machine-learning-evaluate-model-performance.md).

Se si sono tooAzure nuovo Machine Learning ed è necessario consentire la creazione di un semplice esperimento tooget avviato, vedere [creare un semplice esperimento in Azure Machine Learning Studio](machine-learning-create-experiment.md) in Azure Machine Learning Studio.

## <a name="classification"></a>Classificazione
I problemi di classificazione possono essere suddivisi in:

* Problemi con solo due classi (classificazione a due classi o binaria)
* Problemi con più di due classi (classificazione multiclasse)

Azure Machine Learning ha diversi moduli toodeal con ognuno di questi tipi di classificazione, ma hello metodi per l'interpretazione dei risultati di stima sono simili.

### <a name="two-class-classification"></a>Classificazione a due classi
**Esperimento di esempio**

Un esempio di un problema di classificazione a due classi è classificazione hello di fiori iris. attività Hello è fiori iris tooclassify in base alle rispettive funzionalità. set di dati Iris specificato in Azure Machine Learning Hello è un subset di hello diffuso [set di dati Iris](http://en.wikipedia.org/wiki/Iris_flower_data_set) contenente le istanze di solo due fiore specie (classi 0 e 1). Ciascun fiore presenta quattro caratteristiche: lunghezza del sepalo, larghezza del sepalo, lunghezza del petalo e larghezza del petalo.

![Schermata dell'esperimento relativo ai fiori Iris](./media/machine-learning-interpret-model-results/1.png)

Figura 1. Esperimento del problema di classificazione a due classi relativo ai fiori Iris

Un esperimento è stata eseguita toosolve questo problema, come illustrato nella figura 1. È stato eseguito il training e assegnato un punteggio a un modello degli alberi delle decisioni con boosting a due classi. Ora è possibile visualizzare i risultati della stima hello da hello [Score Model] [ score-model] modulo facendo clic su hello porta di output di hello [Score Model] [ score-model]modulo e quindi fare clic su **Visualizza**.

![Modulo Score Model](./media/machine-learning-interpret-model-results/1_1.png)

Verrà visualizzata hello punteggio risultati, come illustrato nella figura 2.

![Risultati dell'esperimento di classificazione a due classi relativo ai fiori Iris](./media/machine-learning-interpret-model-results/2.png)

Figura 2. Visualizzazione dei risultati del modulo Score Model nella classificazione a due classi

**Interpretazione dei risultati**

Sono presenti sei colonne nella tabella risultati hello. quattro colonne sinistra Hello sono funzionalità di quattro hello. Hello destra due colonne, Scored Labels e calcolato il punteggio di probabilità, sono i risultati della stima hello. Hello calcolato il punteggio della probabilità colonna Mostra hello probabilità che un fiore appartiene toohello positivo classe (classe 1). Ad esempio, hello primo numero hello colonna (0.028571) indica la probabilità di 0.028571 hello fiore prima appartiene tooClass 1. classe per ogni fiore stato stimato Hello Scored Labels colonna Mostra hello. Si basa sulla colonna con punteggi di probabilità hello. Se calcolato il punteggio della probabilità di un fiore hello è maggiore di 0,5, stimato come classe 1. in caso contrario, viene stimata la Classe 0.

**Pubblicazione come servizio Web**

Dopo i risultati di stima hello riconosciuti e ritenuti audio, hello esperimento può essere pubblicato come servizio web in modo che sia possibile distribuirla in varie applicazioni e chiamarlo stime classe tooobtain su qualsiasi nuova fiore iris. toolearn come toochange training provare in un esperimento di assegnazione dei punteggi e pubblicarlo come un servizio web, vedere [pubblica servizio web di Azure Machine Learning hello](machine-learning-walkthrough-5-publish-web-service.md). Questa procedura consente di ottenere un esperimento di assegnazione dei punteggi, come illustrato nella figura 3.

![Schermata dell'esperimento di assegnazione dei punteggi](./media/machine-learning-interpret-model-results/3.png)

Figura 3. Esperimento di assegnazione dei punteggi hello iris classificazione a due classi problema

È ora necessario tooset hello input e output per il servizio web hello. input Hello è porta di input destro hello di [Score Model][score-model], che è hello Iris fiore funzionalità input. Hello scelta dell'output di hello varia a seconda se si è interessati in hello stimato classe (con punteggio etichetta), hello calcolato il punteggio della probabilità o entrambi. In questo esempio si suppone di essere interessati a entrambe. hello tooselect desiderato di colonne di output, utilizzare un [selezionare le colonne nel set di dati] [ select-columns] modulo. Fare clic su [Select Columns in Data set][select-columns], su **Launch column selector** (Avvia selettore colonne) e selezionare **Scored Labels** (Etichette con punteggio) e **Scored Probabilities** (Probabilità con punteggio). Dopo aver impostato una porta di output di hello del [selezionare le colonne nel set di dati] [ select-columns] e ripetere l'esecuzione, dovrebbe essere pronto toopublish esperimento di assegnazione dei punteggi hello come servizio web, fare clic su **pubblica sul WEB SERVIZIO**. sperimentazione finale Hello è simile a figura 4.

![esperimento di classificazione a due classi iris Hello](./media/machine-learning-interpret-model-results/4.png)

Figura 4. Esperimento finale di assegnazione dei punteggi per un problema di classificazione a due classi relativo ai fiori Iris

Dopo l'esecuzione del servizio web hello e immettere i valori alcune funzionalità di un'istanza di test, il risultato di hello restituisce due numeri. primo numero Hello è hello con punteggio di etichetta e hello è secondo hello con punteggio di probabilità. Con una probabilità pari a 0,9655, si stima che il fiore appartenga alla Classe 1.

![Modello del test di interpretazione del punteggio](./media/machine-learning-interpret-model-results/4_1.png)

![Risultati del test di assegnazione dei punteggi](./media/machine-learning-interpret-model-results/5.png)

Figura 5. Risultato del servizio Web relativo alla classificazione a due classi dei fiori Iris

### <a name="multi-class-classification"></a>Classificazione multiclasse
**Esperimento di esempio**

In questo esercizio viene considerata un'attività di riconoscimento di lettere come esempio di classificazione multiclasse. Hello classificatore tenta toopredict una determinata lettera (classe) in base a alcuni valori di attributo scritta manualmente estratti da immagini di hello scritta manualmente.

![Esempio di riconoscimento delle lettere](./media/machine-learning-interpret-model-results/5_1.png)

Nei dati di training hello, sono disponibili 16 funzionalità estratte da immagini lettera scritta manualmente. Hello 26 lettere formano i 26 classi. Figura 6 viene mostrato un esperimento che eseguirà una classificazione multiclasse il training del modello per il riconoscimento di lettere e stimare in hello stesso set su un set di dati di test di funzionalità.

![Esperimento di classificazione multiclasse relativo al riconoscimento delle lettere](./media/machine-learning-interpret-model-results/6.png)

Figura 6. Esperimento per un problema di classificazione multiclasse relativo al riconoscimento delle lettere

Visualizzazione dei risultati hello hello [Score Model] [ score-model] modulo, fare clic sulla porta di output di hello del [Score Model] [ score-model] modulo e quindi Fare clic su **Visualizza**, verrà visualizzato il contenuto come illustrato nella figura 7.

![Risultati del modulo Score Model](./media/machine-learning-interpret-model-results/7.png)

Figura 7. Visualizzazione dei risultati del modulo Score Model nella classificazione multiclasse

**Interpretazione dei risultati**

16 colonne sinistra Hello rappresentano i valori delle funzionalità del set di test hello hello. colonne di Hello con nomi come calcolato il punteggio di probabilità per la classe "XX" come colonna con punteggi di probabilità hello in caso di due classi hello. Indicano probabilità hello hello voce corrispondente rientrano in una determinata classe. Ad esempio, per la prima voce hello, è 0.003571 probabile che sia un "A", 0.000451 probabilità è un "B" e così via. la colonna ultimo Hello (Scored etichette) è hello come Scored Labels in caso di due classi hello. Seleziona classe hello con punteggio di probabilità come classe stimate della voce corrispondente hello hello hello più grande. Ad esempio, per la prima voce hello, hello con punteggio etichetta è "F" perché ha hello più grande probabilità toobe una "F" (0.916995).

**Pubblicazione come servizio Web**

È inoltre possibile ottenere hello con punteggio di etichetta per ogni voce e hello probabilità di hello con punteggio con etichetta. logica di base Hello è probabilità più grande di hello toofind tra hello tutti con punteggi di probabilità. toodo, è necessario hello toouse [Execute R Script] [ execute-r-script] modulo. Hello codice R è illustrato nella figura 8 e il risultato di hello dell'esperimento hello è illustrato nella figura 9.

![Esempio di codice R](./media/machine-learning-interpret-model-results/8.png)

Figura 8. Il codice R per l'estrazione Scored Labels e hello associate delle probabilità delle etichette hello

![Risultato dell'esperimento](./media/machine-learning-interpret-model-results/9.png)

Figura 9. Esperimento di assegnazione dei punteggi finale del problema di classificazione multiclasse di riconoscimento della hello

Dopo che si pubblica e servizio web di hello e immettere i valori di alcune funzionalità di input, hello restituito risultato ha un aspetto simile nella figura 10. Con le funzionalità di 16 estratte, la lettera scritta manualmente è stimato toobe "T" con probabilità 0.9715.

![Modulo del test di interpretazione del punteggio](./media/machine-learning-interpret-model-results/9_1.png)

![Risultato del test](./media/machine-learning-interpret-model-results/10.png)

Figura 10. Risultato del servizio Web relativo alla classificazione multiclasse

## <a name="regression"></a>regressione
I problemi di regressione differiscono dai problemi di classificazione per alcuni aspetti. In un problema di classificazione, si sta tentando di classi discreti toopredict, ad esempio la classe a cui appartiene un fiore iris. Ma, come nel seguente esempio di un problema di regressione hello, si noterà che stai tentando toopredict una variabile continua, ad esempio il prezzo di hello di un'automobile.

**Esperimento di esempio**

Come esempio di regressione si considera la stima del prezzo di un'automobile. Si sta tentando di prezzo hello toopredict di un'automobile in base alle relative funzionalità, tra cui marca, tipo di carburante, tipo di corpo e ruota. sperimentazione Hello è illustrato nella figura 11.

![Esperimento di regressione relativo al prezzo di un'automobile](./media/machine-learning-interpret-model-results/11.png)

Figura 11. Esperimento di un problema di regressione relativo al prezzo di un'automobile

La visualizzazione hello [Score Model] [ score-model] modulo, il risultato di hello mostrata nella figura 12.

![Risultato di assegnazione dei punteggi per un problema relativo alla stima del prezzo di un'automobile](./media/machine-learning-interpret-model-results/12.png)

Figura 12. Assegnazione dei punteggi risultato per il problema di stima prezzo automobili hello

**Interpretazione dei risultati**

Etichette con punteggio è la colonna di risultati hello in questo risultato punteggio. numeri di Hello sono prezzo stimato hello ogni automobile.

**Pubblicazione come servizio Web**

È possibile pubblicare l'esperimento di regressione hello in un servizio web e chiamarlo per la stima di prezzo automobili in hello come classificazione a due classi hello caso d'uso.

![Esperimento di assegnazione dei punteggi per un problema di regressione relativo al prezzo di un'automobile](./media/machine-learning-interpret-model-results/13.png)

Figura 13. Esperimento di assegnazione dei punteggi di un problema di regressione relativo al prezzo di un'automobile

Esecuzione del servizio web di hello, hello ha restituito risultati aspetto figura 14. prezzo stimato Hello questa automobile è $15,085.52.

![Modulo del test di interpretazione del punteggio](./media/machine-learning-interpret-model-results/13_1.png)

![Risultati del modulo di assegnazione dei punteggi](./media/machine-learning-interpret-model-results/14.png)

Figura 14. Risultato del servizio Web del problema di regressione relativo al prezzo di un'automobile

## <a name="clustering"></a>clustering
**Esperimento di esempio**

Consente di usare il set di dati Iris hello nuovamente toobuild un esperimento di clustering. Qui puoi escludere le etichette di classe hello nel set di dati hello in modo che solo dispone di funzionalità e può essere utilizzato per il clustering. In questo iris caso d'uso, specificare il numero di hello di cluster toobe due durante il processo di training hello, ovvero che si sarebbero cluster fiori hello in due classi. sperimentazione Hello è illustrato nella figura 15.

![Esperimento del problema relativo al clustering dei fiori Iris](./media/machine-learning-interpret-model-results/15.png)

Figura 15. Esperimento del problema relativo al clustering dei fiori Iris

Clustering si differenzia dalla classificazione in hello set di dati di training non dispone di etichette dati verificati da solo. Gruppi di clustering hello le istanze di set di dati di training in cluster distinti. Durante il processo di training hello, etichette di hello hello voci da differenze hello tra le funzionalità di apprendimento. Successivamente, è possibile utilizzare modello con training hello toofurther classificare i movimenti futuri. Esistono due parti del risultato hello che siamo interessati all'interno di un problema di clustering. prima parte Hello l'assegnazione di etichette hello set di dati di training e hello in secondo luogo è la classificazione di un nuovo set di dati con modello con training hello.

Hello prima parte del risultato hello può essere visualizzati facendo clic a sinistra sulla porta di output di hello [Train Clustering Model] [ train-clustering-model] e quindi fare clic su **Visualizza**. visualizzazione di Hello è illustrata nella figura 16.

![Risultato di clustering](./media/machine-learning-interpret-model-results/16.png)

Figura 16. Visualizzare i risultati per set di dati di training hello clustering

risultato Hello della seconda parte hello, clustering di nuove voci con modello di clustering con training di hello, è illustrato nella figura 17.

![Visualizzazione del risultato di clustering](./media/machine-learning-interpret-model-results/17.png)

Figura 17. Visualizzazione del risultato di clustering su un nuovo set di dati

**Interpretazione dei risultati**

Anche se i risultati di hello parti hello due derivano dalle fasi di sperimentazione diversi, il loro aspetto hello stesso e sono interpretati in hello allo stesso modo. Hello prime quattro colonne sono funzionalità. Hello ultima colonna, le assegnazioni, è il risultato di stima hello. hello voci assegnate Hello stimati stesso numero toobe in hello stesso cluster, vale a dire condividono analogie in qualche modo (questo esperimento utilizza metrica di distanza euclidea hello predefinita). Poiché è stato specificato il numero di hello di toobe cluster 2, le voci di hello nelle assegnazioni sono etichettate come 0 o 1.

**Pubblicazione come servizio Web**

È possibile pubblicare hello clustering esperimento in un servizio web e chiamarlo per stime clustering hello stesso modo in caso di utilizzo nella classificazione a due classi hello.

![Esperimento di assegnazione dei punteggi per un problema di clustering relativo ai fiori Iris](./media/machine-learning-interpret-model-results/18.png)

Figura 18. Esperimento di assegnazione dei punteggi di un problema di clustering relativo ai fiori Iris

Dopo l'esecuzione del servizio web di hello, hello ha restituito risultati aspetto figura 19. Questo fiore è stimato toobe cluster 0.

![Modulo del test di interpretazione del punteggio](./media/machine-learning-interpret-model-results/18_1.png)

![Risultato del modulo di assegnazione dei punteggi](./media/machine-learning-interpret-model-results/19.png)

Figura 19. Risultato del servizio Web relativo alla classificazione a due classi dei fiori Iris

## <a name="recommender-system"></a>Sistema di raccomandazione
**Esperimento di esempio**

Per i sistemi di raccomandazione, è possibile utilizzare un problema di raccomandazione ristorante hello ad esempio: è possibile consigliare ai ristoranti per i clienti in base alla cronologia di valutazione. dati di input Hello è costituito da tre parti:

* Valutazioni sui ristoranti espresse dai clienti
* Dati sulle caratteristiche dei clienti
* Restaurant feature data

Esistono diverse cose che possiamo fare con hello [Train Matchbox Recommender] [ train-matchbox-recommender] modulo in Azure Machine Learning:

* Stimare le valutazioni per un determinato utente ed elemento
* È consigliabile tooa elementi dato utente
* Trovare utenti correlati i tooa dato utente
* Trovare tooa di elementi correlati in base elemento

È possibile scegliere quali toodo selezionando una delle opzioni di hello quattro in hello **tipo stima Recommender** menu. In questo caso vengono analizzati tutti i quattro scenari.

![Matchbox Recommender](./media/machine-learning-interpret-model-results/19_1.png)

Un tipico esperimento di Azure Machine Learning per un sistema di raccomandazione è illustrato nella figura 20. Per informazioni su come toouse i moduli di sistema di raccomandazione, vedere [di raccomandazione matchbox Train] [ train-matchbox-recommender] e [punteggio di raccomandazione matchbox] [ score-matchbox-recommender].

![Esperimento per il sistema di raccomandazione](./media/machine-learning-interpret-model-results/20.png)

Figura 20. Esperimento per il sistema di raccomandazione

**Interpretazione dei risultati**

**Stimare le valutazioni per un determinato utente ed elemento**

Selezionando **stima delle classificazioni** in **tipo stima Recommender**, viene chiesto raccomandazione hello hello toopredict di sistema per un determinato utente ed elemento. visualizzazione di hello Hello [Score Matchbox Recommender] [ score-matchbox-recommender] output sarà analogo figura 21.

![Assegnare un punteggio del sistema di raccomandazione hello - classificazione stima di risultati](./media/machine-learning-interpret-model-results/21.png)

Figura 21. Visualizzare i risultati di punteggio hello del sistema di raccomandazione hello: stima delle classificazioni

Hello prime due colonne sono coppie utente-elemento hello fornite da dati di input hello. terza colonna Hello è hello classificazione stimata di un utente per un determinato elemento. Nella prima riga hello, ad esempio cliente U1048 stimato ristorante toorate 135026 2.

**È consigliabile tooa elementi dato utente**

Selezionando **raccomandazione di un elemento** in **tipo stima Recommender**, chiesto raccomandazione hello sistema toorecommend elementi tooa dato utente. Hello ultimo parametro toochoose in questo scenario è *consigliata la selezione di elementi*. opzione Hello **da elementi classificati (per la valutazione del modello)** viene utilizzata principalmente per la valutazione del modello durante il processo di training hello. per questa fase di stima si usa l'opzione **From All Items** (Da tutti gli elementi). visualizzazione di hello Hello [Score Matchbox Recommender] [ score-matchbox-recommender] output sarà analogo figura 22.

![Risultato di assegnazione dei punteggi del sistema di raccomandazione - Raccomandazione dell'elemento](./media/machine-learning-interpret-model-results/22.png)

Figura 22. Visualizzare il risultato di punteggio del sistema di raccomandazione hello - raccomandazione di un elemento

Hello prima di hello rappresenta le colonne di hello sei dato utente ID toorecommend gli elementi, come specificato dai dati di input hello. Hello altre cinque colonne rappresentano gli elementi di hello consigliati utente toohello in ordine decrescente di rilevanza. Ad esempio, nella prima riga hello, hello più consigliabile ristorante per cliente U1048 134986, seguito da 135018, 134975, 135021 e 132862.

**Trovare utenti correlati i tooa dato utente**

Selezionando **utenti correlati** in **tipo stima Recommender**, chiesto raccomandazione hello tooa dato utente di sistema toofind utenti correlati. Gli utenti correlati sono gli utenti di hello con preferenze simili. Hello ultimo parametro toochoose in questo scenario è *correlati selezione utente*. opzione Hello **da utenti che classificato elementi (per la valutazione del modello)** viene utilizzata principalmente per la valutazione del modello durante il processo di training hello. per questa fase di stima si usa l'opzione **From All Users** (Da tutti gli utenti). visualizzazione di hello Hello [Score Matchbox Recommender] [ score-matchbox-recommender] output sarà analogo figura 23.

![Risultato di assegnazione dei punteggi del sistema di raccomandazione - Utenti correlati](./media/machine-learning-interpret-model-results/23.png)

Figura 23. Visualizzare i risultati di punteggio del sistema di raccomandazione hello - gli utenti correlati

Hello prima di hello Mostra colonne di hello sei dato toofind Necessito ID utente correlati agli utenti, fornito da dati di input. Hello altri archivi di cinque colonne hello utenti correlati stimati dell'utente hello in ordine decrescente di rilevanza. Ad esempio, nella prima riga hello, hello più rilevanti per il cliente U1048 è cliente U1051, seguito da U1066, U1044, U1017 e U1072.

**Trovare tooa di elementi correlati in base elemento**

Selezionando **elementi correlati** in **tipo stima Recommender**, viene chiesto raccomandazione hello elemento tooa specificato di elementi correlati toofind del sistema. Relativi elementi sono hello elementi probabilmente toobe ritengono da hello stesso utente. Hello ultimo parametro toochoose in questo scenario è *la selezione di elementi correlati*. opzione Hello **da elementi classificati (per la valutazione del modello)** viene utilizzata principalmente per la valutazione del modello durante il processo di training hello. per questa fase di stima si usa l'opzione **From All Items** (Da tutti gli elementi). visualizzazione di hello Hello [Score Matchbox Recommender] [ score-matchbox-recommender] output sarà analogo figura 24.

![Risultato di assegnazione dei punteggi del sistema di raccomandazione - Elementi correlati](./media/machine-learning-interpret-model-results/24.png)

Figura 24. Visualizzare i risultati di punteggio del sistema di raccomandazione hello - elementi correlati

prima di hello rappresenta le colonne di hello sei dato gli ID degli elementi necessita Hello toofind relativi elementi, come specificato dai dati di input hello. Hello altri archivi di cinque colonne hello elementi correlati stimati dell'elemento hello in ordine decrescente in termini di pertinenza. Ad esempio, nella prima riga hello, hello più rilevanti per l'elemento 135026 è 135074, seguito da 135035, 132875, 135055 e 134992.

**Pubblicazione come servizio Web**

il processo di Hello della pubblicazione di questi esperimenti come stime tooget di servizi web è simile per ognuno dei quattro scenari hello. Qui verranno secondo scenario di hello (è consigliabile elementi tooa dato utente) come esempio. È possibile seguire hello stessa procedura con hello altre tre.

Salvataggio hello training del sistema di raccomandazione come un modello con training e filtro hello dati di input tooa colonna ID singolo utente come richiesto, è possibile associare la sperimentazione hello come illustrato nella figura 25 e pubblicarlo come un servizio web.

![Assegnazione dei punteggi esperimento di problema di raccomandazione hello ristorante](./media/machine-learning-interpret-model-results/25.png)

Figura 25. Assegnazione dei punteggi esperimento di problema di raccomandazione hello ristorante

Esecuzione del servizio web di hello, hello ha restituito risultati aspetto figura 26. i ristoranti consigliato cinque Hello per utente U1048 sono 134986, 135018, 134975, 135021 e 132862.

![Esempio di servizio di sistema di raccomandazione](./media/machine-learning-interpret-model-results/25_1.png)

![Risultati dell'esperimento di esempio](./media/machine-learning-interpret-model-results/26.png)

Figura 26. Risultato del servizio Web relativo al problema di raccomandazione di ristoranti

<!-- Module References -->
[assign-to-clusters]: https://msdn.microsoft.com/library/azure/eed3ee76-e8aa-46e6-907c-9ca767f5c114/
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[score-matchbox-recommender]: https://msdn.microsoft.com/library/azure/55544522-9a10-44bd-884f-9a91a9cec2cd/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[train-clustering-model]: https://msdn.microsoft.com/library/azure/bb43c744-f7fa-41d0-ae67-74ae75da3ffd/
[train-matchbox-recommender]: https://msdn.microsoft.com/library/azure/fa4aa69d-2f1c-4ba4-ad5f-90ea3a515b4c/
