---
title: le prestazioni del modello aaaEvaluate in Machine Learning | Documenti Microsoft
description: Viene illustrato come tooevaluate modello delle prestazioni in Azure Machine Learning.
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 5dc5348a-4488-4536-99eb-ff105be9b160
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: bradsev;garye
ms.openlocfilehash: 03477368758dbb13aa6f54c5d27fb215615d1f9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooevaluate-model-performance-in-azure-machine-learning"></a>Come tooevaluate modello delle prestazioni in Azure Machine Learning
In questo articolo viene illustrato come tooevaluate hello prestazioni di un modello in Azure Machine Learning Studio e fornisce una breve spiegazione di metriche di hello disponibile per questa attività. L'argomento presenta inoltre tre scenari di apprendimento sorvegliato comuni: 

* Regressione
* Classificazione binaria 
* Classificazione multiclasse

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Valutazione delle prestazioni di hello di un modello è una delle fasi di base hello nel processo di analisi scientifica dei dati hello. Indica l'efficacia hello punteggio (stime) di un set di dati è stato da un modello con training. 

Azure Machine Learning supporta la valutazione del modello tramite due moduli di apprendimento automatico principali, ovvero [Evaluate Model][evaluate-model] e [Cross-Validate Model][cross-validate-model]. Questi moduli consentono di toosee come il modello esegue in termini di un numero di metriche di uso comune in statistiche e machine learning.

## <a name="evaluation-vs-cross-validation"></a>Confronto tra la valutazione e la convalida incrociata
Valutazione e convalida incrociata sono le prestazioni di hello toomeasure modalità standard del modello. Entrambi generano metriche di valutazione che l'utente può usare per controllare o mettere a confronto quelle di altri modelli.

[Valutazione del modello] [ evaluate-model] prevede un set di dati con punteggio come input (o 2 in caso desideri prestazioni hello toocompare di 2 modelli diversi). Ciò significa che è necessario tootrain il modello utilizzando hello [Train Model] [ train-model] modulo e apportare le stime in alcuni set di dati utilizzando hello [Score Model] [ score-model] modulo, prima di poter valutare i risultati di hello. Hello valutazione si basa su con punteggio etichette/probabilità insieme alle etichette true hello, che sono tutti output hello hello [Score Model] [ score-model] modulo.

In alternativa, è possibile utilizzare la convalida incrociata tooperform diverse operazioni valutare train-punteggio (10 sezioni) automaticamente in diversi subset hello di dati di input. dati di input Hello sono suddiviso in 10 parti, in cui uno è riservato per il testing e hello altri 9 per il training. Questo processo viene ripetuto 10 volte e vengono calcolata la media di metriche di valutazione di hello. Ciò consente di determinare come anche un modello verrebbe generalizzare toonew i set di dati. Hello [Cross-Validate Model] [ cross-validate-model] modulo accetta in un modello senza training e alcuni etichetta risultati della valutazione hello set di dati e di output di hello ogni 10 sezioni, toohello inoltre calcolata la media dei risultati.

Nelle seguenti sezioni di hello, verrà compilare i modelli di classificazione e regressione semplici e valutare le prestazioni, utilizzando entrambi hello [Evaluate Model] [ evaluate-model] e hello [Cross-Validate Modello] [ cross-validate-model] moduli.

## <a name="evaluating-a-regression-model"></a>Valutazione di un modello di regressione
Si supponga di che voler toopredict prezzo dell'automobile, un utilizzo di alcune funzionalità, ad esempio dimensioni, potenza, le specifiche del motore e così via. Si tratta di un problema di regressione tipico, in cui hello variabile di destinazione (*prezzo*) è un valore numerico continuo. È possibile adattare un modello di regressione lineare semplice che, dato hello funzionalità valori di determinate un'automobile, stimare prezzo hello di tale macchina. È possibile utilizzare questo modello di regressione tooscore hello è sottoposto a training sui set di dati stesso. Una volta che è stata hello prezzi stimati per le automobili hello, è possibile valutare le prestazioni di hello del modello di hello esaminando quanto stime hello deviano dalla prezzi effettivi hello medio. tooillustrate, utilizziamo hello *set di dati (Raw) di prezzo Automobile* disponibile in hello **Saved Datasets** sezione in Azure Machine Learning Studio.

### <a name="creating-hello-experiment"></a>Creazione di hello esperimento
Aggiungere hello seguendo l'area di lavoro tooyour moduli in Azure Machine Learning Studio:

* Automobile price data (Raw)
* [Linear Regression][linear-regression]
* [Train Model][train-model]
* [Score Model][score-model]
* [Evaluate Model][evaluate-model]

Connettere le porte hello come mostrato nella figura 1 e colonna del set di etichetta hello di hello [Train Model] [ train-model] modulo troppo*prezzo*.

![Valutazione di un modello di regressione](media/machine-learning-evaluate-model-performance/1.png)

Figura 1. Valutazione di un modello di regressione.

### <a name="inspecting-hello-evaluation-results"></a>Esaminare i risultati della valutazione hello
Dopo l'esperimento hello in esecuzione, è possibile fare clic sulla porta di output di hello di hello [Evaluate Model] [ evaluate-model] modulo e selezionare *Visualizza* toosee risultati della valutazione hello. Hello metriche di valutazione disponibili per i modelli di regressione sono: *errore assoluto medio*, *errore assoluto medio radice*, *errore assoluto relativo*,  *Errore quadratico relativo*, hello e *coefficiente di determinazione*.

il termine Hello "error" di seguito rappresenta la differenza hello tra hello valore stimato e il valore true hello. valore assoluto di Hello o hello quadrato di questa differenza sono in genere calcolata toocapture hello totale grandezza di errore in tutte le istanze, come differenza hello tra hello stimata e il valore true può essere negativo in alcuni casi. metriche errore Hello prestazioni hello predittiva di un modello di regressione in termini di deviazione media hello di esecuzione delle stime dai valori true hello. I valori di errore più bassi indicano che il modello di hello più accurato nell'esecuzione di stime. Una metrica di errore generale di 0 indica che hello modello si adatta perfettamente dati hello.

coefficiente di determinazione, che è noto anche come R di Hello al quadrato, è anche un modo standard di misurare l'accuratezza modello di hello adatto dati hello. Questo può essere interpretato come proporzione hello della variazione spiegati da modello hello. Una percentuale più elevata è migliore nel caso in cui 1 indica un'idoneità perfetta.

![Metriche di valutazione della regressione lineare](media/machine-learning-evaluate-model-performance/2.png)

Figura 2. Metriche di valutazione della regressione lineare.

### <a name="using-cross-validation"></a>Uso della convalida incrociata
Come accennato in precedenza, è possibile eseguire training ripetuti, assegnazione di punteggi e valutazioni automaticamente utilizzando hello [Cross-Validate Model] [ cross-validate-model] modulo. In questo caso occorrono semplicemente un set di dati, un modello non sottoposto a training e un modulo [Cross-Validate Model][cross-validate-model] (vedere la figura seguente). Si noti che è necessario troppo colonna di etichetta hello tooset*prezzo* in hello [Cross-Validate Model] [ cross-validate-model] le proprietà del modulo.

![Convalida incrociata di un modello di regressione](media/machine-learning-evaluate-model-performance/3.png)

Figura 3. Esecuzione della convalida incrociata di un modello di regressione.

Dopo l'esperimento hello in esecuzione, è possibile esaminare i risultati della valutazione hello facendo clic sulla porta di output di destra hello di hello [Cross-Validate Model] [ cross-validate-model] modulo. Questo fornirà una visualizzazione dettagliata delle metriche hello per ogni iterazione (sezione) e hello calcolata la media dei risultati di ogni metrica hello (figura 4).

![Risultati della convalida incrociata di un modello di regressione](media/machine-learning-evaluate-model-performance/4.png)

Figura 4. Risultati della convalida incrociata di un modello di regressione.

## <a name="evaluating-a-binary-classification-model"></a>Valutazione di un modello di classificazione binaria
In uno scenario di classificazione binaria, la variabile di destinazione hello ha solo due possibili risultati, ad esempio: {0, 1} o {false, true}, {negativo, positivo}. Si supponga che è un set di dati dei dipendenti per adulti con alcuni dati demografici e variabili occupazione, e che viene richiesto di livello di reddito hello toopredict, una variabile con valori hello binaria {"< = 50k", "> 50K"}. In altre parole, la classe negativo hello rappresenta dipendenti hello verificare che sia minore o uguale too50K all'anno e hello positivo classe rappresenta tutti gli altri dipendenti. Come nello scenario di regressione hello, si sarebbe training di un modello, assegnare un punteggio alcuni dati e valutare i risultati di hello. Hello differenza principale è scelta hello di metriche di che Azure Machine Learning calcola e output. scenario di livello stima il reddito hello tooillustrate, si utilizzerà hello [per adulti](http://archive.ics.uci.edu/ml/datasets/Adult) toocreate set di dati un Azure Machine Learning sperimentazione e valutare le prestazioni di hello di un modello di regressione logistica a due classi, un file binario di uso comune funzione di classificazione.

### <a name="creating-hello-experiment"></a>Creazione di hello esperimento
Aggiungere hello seguendo l'area di lavoro tooyour moduli in Azure Machine Learning Studio:

* Adult Census Income Binary Classification dataset
* [Two-Class Logistic Regression][two-class-logistic-regression]
* [Train Model][train-model]
* [Score Model][score-model]
* [Evaluate Model][evaluate-model]

Connettere le porte hello come mostrato nella figura 5 e hello etichetta colonna del set di hello [Train Model] [ train-model] modulo troppo*reddito*.

![Valutazione di un modello di classificazione binaria](media/machine-learning-evaluate-model-performance/5.png)

Figura 5. Valutazione di un modello di classificazione binaria.

### <a name="inspecting-hello-evaluation-results"></a>Esaminare i risultati della valutazione hello
Dopo l'esperimento hello in esecuzione, è possibile fare clic sulla porta di output di hello di hello [Evaluate Model] [ evaluate-model] modulo e selezionare *Visualizza* risultati della valutazione hello toosee (figura 7). Hello metriche di valutazione disponibili per i modelli di classificazione binaria sono: *accuratezza*, *precisione*, *richiamare*, *punteggio F1*, e *AUC*. Inoltre, il modulo hello restituisce una matrice di confusione che mostra il numero di veri positivi, falsi negativi, falsi positivi e negativi true, hello nonché *ROC*, *precisione/richiamo*e *Accuratezza* curve.

L'accuratezza è semplicemente proporzione di hello istanze classificato correttamente. È in genere metrica prima di hello che si osserva durante la valutazione di una funzione di classificazione. Tuttavia, quando i dati di test hello sono sbilanciata (in cui la maggior parte delle istanze di hello appartengono tooone delle classi di hello) o si è più interessati prestazioni hello su una delle classi di hello, accuratezza effettivamente non acquisisce l'efficacia di un classificatore hello. Nello scenario di classificazione di livello di reddito hello, si supponga che si sta testando con determinati dati, dove 99% delle istanze di hello rappresentano utenti guadagnare minore o uguale too50K all'anno. È possibile tooachieve una precisione 0.99 dalla stima classe hello "< = 50k" per tutte le istanze. classificazione Hello viene visualizzato in questo caso toobe facendo un buon lavoro globale, ma in realtà, non tooclassify uno qualsiasi dei singoli utenti ad alto reddito di hello (% 1 hello) correttamente.

Per questo motivo, è utile toocompute altre metriche che consentono di acquisire gli aspetti più specifici di valutazione di hello. Prima di entrare nei dettagli hello di tali metriche, è una matrice di confusione hello toounderstand importante di una valutazione di classificazione binaria. classe di Hello etichette nel set di training hello possono assumere i valori possibili solo 2, che è in genere riferimento tooas positivo o negativo. le istanze positivi e negativi Hello che una funzione di classificazione consente di stimare correttamente vengono definite (TP) di veri positivi e negativi true (TN), rispettivamente. Analogamente, le istanze di classificazione non corretta di hello sono definite falsi positivi (/FP) e falsi negativi (FN). Matrice di confusione Hello è semplicemente una tabella che mostra il numero di istanze che rientrano in ognuna di queste 4 categorie hello. Azure Machine Learning decide automaticamente di hello due classi dataset hello ovvero hello positivo classe. Se le etichette di classe hello sono Boolean o numeri interi, hello istanze con etichette 'true' o '1' assegnate classe positivo hello. Se le etichette di hello sono stringhe, come nel caso di hello del set di dati di hello reddito, etichette hello vengono ordinate in ordine alfabetico e primo livello hello viene scelta classe negativo di hello toobe mentre secondo livello hello è la classe positivo hello.

![Matrice di confusione di classificazione binaria](media/machine-learning-evaluate-model-performance/6a.png)

Figura 6. Matrice di confusione di classificazione binaria.

Se si torna indietro toohello problema di classificazione di reddito, sarebbe necessario tooask diverse domande valutazione utili informazioni sulle prestazioni di hello del classificatore hello utilizzato. Una domanda molto naturale è: ' fuori individui hello cui hello modello toobe stimato ricevere > 50 K TP + FP (), quanti sono stati classificati in modo corretto (TP)?' Può rispondere a questa domanda esaminando hello **precisione** del modello di hello, che è la proporzione hello di positivi che siano classificati correttamente: TP/(TP+FP). Un'altra domanda comune è "tutti i dipendenti di reddito elevato hello con reddito > 50 k TP + FN (), quanti hello classificazione classificare correttamente (TP)". Si tratta in realtà hello **richiamare**, o tasso positivo true hello: TP/(TP+FN) del classificatore hello. Come si può notare, vi è un chiaro compromesso tra precisione e richiamo. Ad esempio, dato un set di dati relativamente bilanciato, una funzione di classificazione che stima principalmente positivo istanze, avrebbe un richiamo elevato, ma una precisione piuttosto bassa il numero di istanze negativo hello potrebbe essere classificato erroneamente risultante in un numero elevato di falsi positivi. toosee un tracciato di come questi due metriche variano, è possibile fare clic su curva ' Precisione/RICHIAMO' hello nella pagina di output di hello valutazione dei risultati (in alto a sinistra parte della figura 7).

![Risultati della valutazione della classificazione binaria](media/machine-learning-evaluate-model-performance/7.png)

Figura 7. Risultati della valutazione della classificazione binaria.

Un'altra metrica che viene spesso utilizzato con le hello **punteggio F1**, che accetta sia la precisione e richiamo in considerazione. È la media armonica per hello queste 2 metriche e viene calcolata come tale: F1 = 2 (richiamo precisione x) / (precisione + richiamo). punteggio F1 Hello è una valutazione di hello toosummarize efficace in un singolo numero, ma è sempre un toolook buona norma sia precisione e richiamo toobetter insieme comprendere il comportamento di una funzione di classificazione.

Inoltre, uno può controllare tasso positivo true da hello e frequenza di positivo false hello in hello **ricevitore operativo caratteristica (ROC)** curva e hello corrispondente **hello Area nella curva (AUC)** valore. Hello più vicino la curva è toohello superiore sinistro, le prestazioni del classificatore di hello migliori hello (vale a dire ottimizzazione hello true positivo velocità riducendo al minimo la frequenza di positivo false di hello). Curve di toohello Chiudi diagonale di hello tracciato, risultato classificatori che tendono a toomake stime che sono la chiusura toorandom un'ipotesi.

### <a name="using-cross-validation"></a>Uso della convalida incrociata
Come esempio di regressione hello, è possibile eseguire la convalida incrociata toorepeatedly treno, assegnare un punteggio e valutare diversi subset di dati hello automaticamente. Analogamente, possiamo utilizzare hello [Cross-Validate Model] [ cross-validate-model] modulo, un modello di regressione logistica senza training e un set di dati. colonna di etichetta Hello deve essere impostato troppo*reddito* in hello [Cross-Validate Model] [ cross-validate-model] le proprietà del modulo. Dopo la porta di hello di output eseguendo esperimento hello e fare clic sulla destra hello [Cross-Validate Model] [ cross-validate-model] modulo, è possibile osservare la metrica di classificazione binaria hello i valori per ogni riduzione, inoltre toohello deviazione media e standard di ognuno. 

![Convalida incrociata di un modello di classificazione binaria](media/machine-learning-evaluate-model-performance/8.png)

Figura 8. Convalida incrociata di un modello di classificazione binaria.

![Risultati della convalida incrociata di un classificatore binario.](media/machine-learning-evaluate-model-performance/9.png)

Figura 9. Risultati della convalida incrociata di un classificatore binario.

## <a name="evaluating-a-multiclass-classification-model"></a>Valutazione di un modello di classificazione multiclasse
In questo esercizio si utilizzerà hello diffuso [Iris](http://archive.ics.uci.edu/ml/datasets/Iris "Iris") set di dati che contiene le istanze di 3 diversi tipi (classi) di impianto iris hello. Esistono 4 valori caratteristici (lunghezza/larghezza sepalo e lunghezza/larghezza petalo) per ogni istanza. Negli esperimenti precedenti hello è eseguito il training e i modelli testati hello utilizzando hello stessi set di dati. In questo caso, si utilizzerà hello [dati divisi] [ split] subset toocreate 2 modulo dei dati di hello, formazione hello in primo luogo, assegnare un punteggio e valutare in hello secondo. Hello set di dati Iris è disponibile pubblicamente su hello [UCI Machine Learning Repository](http://archive.ics.uci.edu/ml/index.html)e può essere scaricata mediante un [l'importazione dei dati] [ import-data] modulo.

### <a name="creating-hello-experiment"></a>Creazione di hello esperimento
Aggiungere hello seguendo l'area di lavoro tooyour moduli in Azure Machine Learning Studio:

* [Import Data][import-data]
* [Multiclass Decision Forest][multiclass-decision-forest]
* [Split Data][split]
* [Train Model][train-model]
* [Score Model][score-model]
* [Evaluate Model][evaluate-model]

Connettere le porte hello come mostrato nella figura 10.

Impostare l'indice di colonna di etichetta hello di hello [Train Model] [ train-model] too5 modulo. set di dati Hello non esiste alcuna riga di intestazione ma verrà tale classe hello le etichette sono hello quinta colonna.

Fare clic su hello [l'importazione dei dati] [ import-data] modulo set hello e *origine dati* proprietà troppo*URL Web tramite HTTP*, hello e *URL*  toohttp://archive.ics.uci.edu/ml/machine-learning-databases/iris/iris.data.

Frazione di hello set di istanze toobe utilizzati per il training in hello [dati divisi] [ split] modulo (0,7 ad esempio).

![Valutazione di un classificatore multiclasse](media/machine-learning-evaluate-model-performance/10.png)

Figura 10. Valutazione di un classificatore multiclasse

### <a name="inspecting-hello-evaluation-results"></a>Esaminare i risultati della valutazione hello
Eseguire l'esperimento hello e fare clic sulla porta di output di hello di [Evaluate Model][evaluate-model]. risultati della valutazione Hello vengono presentati in forma di hello di una matrice di confusione, in questo caso. Matrice di Hello Mostra hello effettivi e stimate istanze per tutte le classi di 3.

![Risultati della valutazione della classificazione multiclasse](media/machine-learning-evaluate-model-performance/11.png)

Figura 11. Risultati di valutazione della classificazione a più classi.

### <a name="using-cross-validation"></a>Uso della convalida incrociata
Come accennato in precedenza, è possibile eseguire training ripetuti, assegnazione di punteggi e valutazioni automaticamente utilizzando hello [Cross-Validate Model] [ cross-validate-model] modulo. Saranno necessari un set di dati, un modello non sottoposto a training e un modulo [Cross-Validate Model][cross-validate-model] (vedere la figura seguente). Nuovo è necessario tooset colonna di etichetta hello di hello [Cross-Validate Model] [ cross-validate-model] modulo (indice di colonna 5 in questo caso). Dopo l'esecuzione esperimento hello e facendo clic sulla destra hello output porta hello [Cross-Validate Model][cross-validate-model], è possibile controllare i valori della metrica hello per ogni riduzione, nonché hello deviazione media e standard. metriche di Hello visualizzate di seguito sono toohello simile hello quelle illustrate in caso di classificazione binaria hello. Tuttavia, si noti che nella classificazione multiclasse, il calcolo hello veri positivi o negativi e falsi positivi o negativi viene eseguita dal conteggio dei singoli per ogni classe, perché non esiste alcuna classe generale positiva o negativa. Ad esempio, quando precisione hello elaborazione o il richiamo di classe "Iris setosa" hello, si presuppone che si tratta classe positivo hello e tutti gli altri come negativo.

![Convalida incrociata di un modello di classificazione multiclasse](media/machine-learning-evaluate-model-performance/12.png)

Figura 12. Convalida incrociata di un modello di classificazione a più classi.

![Risultati della convalida incrociata di un modello di classificazione multiclasse](media/machine-learning-evaluate-model-performance/13.png)

Figura 13. Risultati della convalida incrociata di un modello di classificazione multiclasse.

<!-- Module References -->
[cross-validate-model]: https://msdn.microsoft.com/library/azure/75fb875d-6b86-4d46-8bcc-74261ade5826/
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[linear-regression]: https://msdn.microsoft.com/library/azure/31960a6f-789b-4cf7-88d6-2e1152c0bd1a/
[multiclass-decision-forest]: https://msdn.microsoft.com/library/azure/5e70108d-2e44-45d9-86e8-94f37c68fe86/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
[two-class-logistic-regression]: https://msdn.microsoft.com/library/azure/b0fd7660-eeed-43c5-9487-20d9cc79ed5d/

