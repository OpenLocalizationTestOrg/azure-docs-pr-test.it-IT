---
title: 'Passaggio 4: Eseguire il training e valutare i modelli di analisi predittiva hello | Documenti Microsoft'
description: "Passaggio 4 di hello sviluppare una procedura dettagliata soluzione predittiva: treno, assegnare un punteggio e valutare più modelli in Azure Machine Learning Studio."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: d905f6b3-9201-4117-b769-5f9ed5ee1cac
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: d86d7c5ae7524f71fe44d985db67c4618b7965a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-4-train-and-evaluate-hello-predictive-analytic-models"></a>Procedura dettagliata passaggio 4: Eseguire il training e valutare i modelli di analisi predittiva hello
In questo argomento contiene quarto passaggio di hello della procedura dettagliata hello [sviluppare una soluzione analitica predittiva in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)

1. [Creare un'area di lavoro di Machine Learning](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [Caricare i dati esistenti](machine-learning-walkthrough-2-upload-data.md)
3. [Creare un nuovo esperimento](machine-learning-walkthrough-3-create-new-experiment.md)
4. **Eseguire il training e valutare i modelli di hello**
5. [Distribuzione di servizio Web hello](machine-learning-walkthrough-5-publish-web-service.md)
6. [Accedere al servizio Web hello](machine-learning-walkthrough-6-access-web-service.md)

- - -
Uno dei vantaggi di hello dell'utilizzo di Azure Machine Learning Studio per la creazione di modelli di machine learning è hello possibilità tootry più di un tipo di modello alla volta in un esperimento singolo e confrontare i risultati di hello. Questo tipo di sperimentazione consente di trovare la soluzione migliore hello per il problema.

Nell'esperimento di hello è in corso di sviluppo in questa procedura dettagliata viene creare due tipi diversi di modelli e quindi confrontare i relativi toodecide risultati punteggio quale algoritmo desideriamo toouse nell'esperimento finale.  

Sono disponibili diversi modelli tra cui scegliere. modelli hello toosee disponibili, espandere hello **Machine Learning** nodo tavolozza modulo hello, quindi espandere **inizializzare modello** e hello nodi sottostanti. Ai fini di hello di questo esperimento, si selezionerà hello [Two-Class Support Vector Machine] [ two-class-support-vector-machine] (SVM) e hello [Two-Class Boosted Decision Tree] [ two-class-boosted-decision-tree] moduli.    

> [!TIP]
> Guida tooget decidere quale algoritmo di Machine Learning meglio si adatta alle particolare problema hello che stai tentando toosolve, vedere [come algoritmi toochoose per Microsoft Azure Machine Learning](machine-learning-algorithm-choice.md).
> 
> 

## <a name="train-hello-models"></a>Eseguire il training di modelli di hello

Verranno aggiunti entrambi hello [Two-Class Boosted Decision Tree] [ two-class-boosted-decision-tree] modulo e [Two-Class Support Vector Machine] [ two-class-support-vector-machine] questo modulo esperimento.

### <a name="two-class-boosted-decision-tree"></a>Two-Class Boosted Decision Tree

In primo luogo, impostazione modello di albero delle decisioni con Boosting hello.

1. Trovare hello [Two-Class Boosted Decision Tree] [ two-class-boosted-decision-tree] modulo tavolozza modulo hello e trascinarlo nell'area di disegno hello.

2. Trovare hello [Train Model] [ train-model] modulo, trascinarlo nell'area di disegno hello e quindi connettere l'output di hello di hello [Two-Class Boosted Decision Tree] [ two-class-boosted-decision-tree]toohello modulo lasciato porta di input di hello [Train Model] [ train-model] modulo.
   
   Hello [Two-Class Boosted Decision Tree] [ two-class-boosted-decision-tree] modulo Inizializza modello generico di hello e [Train Model] [ train-model] utilizza i dati di training modello di hello tootrain. 

3. Connettere hello output a sinistra di sinistra hello [Execute R Script] [ execute-r-script] porta di hello di input di destra toohello modulo [Train Model] [ train-model] modulo (è ha deciso [passaggio 3](machine-learning-walkthrough-3-create-new-experiment.md) di questa procedura dettagliata toouse hello i dati provenienti dal lato sinistro di modulo di hello suddivisione dei dati per il training hello).
   
   > [!TIP]
   > Non sono necessarie due input hello e uno di output di hello di hello [Execute R Script] [ execute-r-script] modulo per questo esercizio, pertanto è possibile lasciarli scollegato. 
   > 
   > 

Questa parte dell'esperimento hello sarà ora simile al seguente:  

![Training a model][1]

Ora è necessario tootell hello [Train Model] [ train-model] modulo che si desidera valore del rischio di credito hello toopredict modello hello.

1. Seleziona hello [Train Model] [ train-model] modulo. In hello **proprietà** riquadro, fare clic su **selettore di colonna avvio**.

2. In hello **selezionare una singola colonna** finestra di dialogo, digitare "rischio di credito" nel campo di ricerca hello in **colonne disponibili**, selezionare "Rischio di credito" di seguito e fare clic sul pulsante freccia destra hello ( **>** ) toomove "Credito rischio" troppo**colonne selezionate**. 

    ![Selezionare la colonna di rischio di credito hello per modulo Train Model hello][0]

3. Fare clic su hello **OK** segno di spunta.

### <a name="two-class-support-vector-machine"></a>Two-Class Support Vector Machine

Successivamente, è necessario impostare modello SVM hello.  

Innanzitutto, una breve spiegazione di SVM. Gli alberi delle decisioni con boosting funzionano bene con qualsiasi tipo di funzionalità. Tuttavia, poiché il modulo SVM hello genera un classificatore lineare, modello hello che genera errore hello migliore test quando dispongono di tutte le funzionalità numeriche hello stessa scala. tooconvert numerico tutte le funzionalità toohello stessa scala, si utilizza una trasformazione "Tanh" (con hello [Normalize Data] [ normalize-data] modulo). Ciò consente di trasformare i numeri nell'intervallo [0,1] hello. modulo SVM Hello converte in stringa funzionalità toocategorical funzionalità e quindi toobinary 0/1, in modo non è necessario toomanually trasformare le funzionalità di stringa. Inoltre, non vogliamo tootransform hello rischio di credito colonna (colonna 21): è numerico, ma è il valore di hello ci stiamo training hello toopredict modello, pertanto è necessario tooleave è da solo.  

hello tooset modello SVM hello, di seguito:

1. Trovare hello [Two-Class Support Vector Machine] [ two-class-support-vector-machine] modulo tavolozza modulo hello e trascinarlo nell'area di disegno hello.

2. Pulsante destro del mouse hello [Train Model] [ train-model] modulo, seleziona **copia**, quindi fare doppio clic su area di disegno hello e selezionare **Incolla**. copia di hello Hello [Train Model] [ train-model] del modulo è hello stesso selezione della colonna come hello originale.

3. Connettere l'output di hello di hello [Two-Class Support Vector Machine] [ two-class-support-vector-machine] toohello modulo lasciato porta di input di hello secondo [Train Model] [ train-model] modulo.

4. Trovare hello [Normalize Data] [ normalize-data] modulo e trascinarlo nell'area di disegno hello.

5. Connettere hello output a sinistra di sinistra hello [Execute R Script] [ execute-r-script] input toohello modulo di questo modulo (si noti che la porta di output di hello di un modulo può essere connesso toomore rispetto a un altro modulo).

6. Connettersi a sinistra sulla porta di output di hello hello [Normalize Data] [ normalize-data] toohello modulo destra input porta hello secondo [Train Model] [ train-model] modulo.

Questa parte dell'esperimento avrà ora un aspetto analogo al seguente:  

![Training del modello di secondo hello][2]  

Configurare ora hello [Normalize Data] [ normalize-data] modulo:

1. Fare clic su hello tooselect [Normalize Data] [ normalize-data] modulo. In hello **proprietà** riquadro, selezionare **Tanh** per hello **Transformation method** parametro.

2. Fare clic su **selettore di colonna avvio**, non selezionare "Nessuna columns" per **iniziano con**selezionare **Include** hello prima dall'elenco a discesa, selezionare **il tipo di colonna**in hello secondo elenco a discesa e selezionare **numerico** nell'elenco a discesa terzo hello. Specifica che vengono trasformati tutti hello colonne numeriche (e solo numerico).

3. Fare clic sul segno più (+) toohello a destra di questa riga hello: verrà creata una riga di menu a discesa. Selezionare **escludere** hello prima dall'elenco a discesa, selezionare **i nomi di colonna** in hello secondo elenco a discesa, quindi immettere "Credito di rischio" nel campo di testo hello. Specifica la colonna di rischio di credito hello deve essere ignorata (dobbiamo toodo questo perché la colonna è numerica e pertanto viene trasformato se è non è stata esclusa).

4. Fare clic su hello **OK** segno di spunta.  

    ![Selezionare le colonne per il modulo di hello Normalize Data][5]

Hello [Normalize Data] [ normalize-data] modulo viene ora set tooperform una trasformazione Tanh in tutte le colonne numeriche, ad eccezione di colonna di hello rischio di credito.  

## <a name="score-and-evaluate-hello-models"></a>Assegnare un punteggio e valutare i modelli di hello

Utilizziamo hello verifica dei dati che è stati separati da hello [dati divisi] [ split] tooscore modulo nostri modelli con training. È quindi possibile confrontare i risultati di hello di hello due modelli toosee che ha generato i risultati migliori.  

### <a name="add-hello-score-model-modules"></a>Aggiungere moduli Score Model hello

1. Trovare hello [Score Model] [ score-model] modulo e trascinarlo nell'area di disegno hello.

2. Connettersi hello [Train Model] [ train-model] modulo che è connesso toohello [Two-Class Boosted Decision Tree] [ two-class-boosted-decision-tree] input di sinistra toohello modulo porta di hello [Score Model] [ score-model] modulo.

3. Connettersi a destra di hello [Execute R Script] [ execute-r-script] toohello modulo (i dati di test) a destra di input porta hello [Score Model] [ score-model] modulo.

    ![Modulo Score Model (Punteggio modello) connesso][6]
   
   Hello [Score Model] [ score-model] modulo può richiedere ora le informazioni sul credito hello dalla verifica dei dati, eseguirlo tramite il modello di hello, hello e confrontare le stime di hello hello modello genera con hello effettivo rischio di credito colonna in dati di testing hello.

4. Copiare e incollare hello [Score Model] [ score-model] toocreate modulo una seconda copia.

5. Connettere l'output di hello del modello SVM hello (vale a dire, porta di hello di output hello [Train Model] [ train-model] modulo che è connesso toohello [Two-Class Support Vector Machine] [ two-class-support-vector-machine] modulo) toohello input hello porta in secondo luogo [Score Model] [ score-model] modulo.

6. Per il modello SVM hello abbiamo toodo hello stessi dati di test toohello trasformazione come è stato fatto toohello dati di training. Pertanto, copiare e incollare hello [Normalize Data] [ normalize-data] toocreate modulo una seconda copia e connetterla destra toohello [Execute R Script] [ execute-r-script] modulo.

7. La connessione di output a sinistra di hello di hello secondo [Normalize Data] [ normalize-data] toohello modulo destra input porta hello secondo [Score Model] [ score-model] modulo.

    ![Entrambi i moduli Score Model (Punteggio modello) connessi][7]

### <a name="add-hello-evaluate-model-module"></a>Aggiungi modulo Evaluate Model hello

tooevaluate hello due risultati del punteggio e confrontarli, utilizziamo un [Evaluate Model] [ evaluate-model] modulo.  

1. Trovare hello [Evaluate Model] [ evaluate-model] modulo e trascinarlo nell'area di disegno hello.

2. Connettere hello porta di output di hello [Score Model] [ score-model] associato hello modulo boosted decision toohello modello di struttura ad albero a sinistra di input porta hello [Evaluate Model] [ evaluate-model] modulo.

3. Connettersi hello altri [Score Model] [ score-model] porta di input di destra toohello modulo.  

    ![Modulo Evaluate Model (Modello di valutazione) connesso][8]

### <a name="run-hello-experiment-and-check-hello-results"></a>Eseguire l'esperimento hello e controllare i risultati di hello

toorun hello esperimento, fare clic su hello **eseguire** pulsante sotto l'area di disegno hello. L'operazione potrebbe richiedere alcuni minuti. Un indicatore rotante in ogni modulo viene illustrato che è in esecuzione e quindi un segno di spunta verde viene visualizzata al termine modulo hello. Quando tutti i moduli di hello dispongono di un segno di spunta, esperimento hello è terminata.

sperimentazione Hello dovrebbe risultare simile al seguente:  

![Valutazione di entrambi i modelli][3]

risultati di hello toocheck, fare clic su hello porta di output di hello [Evaluate Model] [ evaluate-model] modulo e selezionare **Visualizza**.  

Hello [Evaluate Model] [ evaluate-model] modulo produce una coppia di curve e le metriche che consentono di risultati di hello toocompare di due modelli con punteggio di hello. È possibile visualizzare i risultati di hello come curve di accuratezza, precisione/richiamo curve o curve ricevitore operatore caratteristica (ROC). Dati aggiuntivi visualizzati includono una matrice di confusione, valori cumulativi per area hello sotto la curva hello (AUC) e altre metriche. È possibile modificare il valore di soglia hello mobile hello il dispositivo di scorrimento sinistro o destro e osservare gli effetti set hello di metriche.  

toohello destra del grafico hello, fare clic su **Scored dataset** o **Scored dataset toocompare** toohighlight hello associato curva e toodisplay hello associata metriche riportato di seguito. Nella legenda hello per le curve hello, "Set di dati di punteggio" corrisponde a sinistra sulla porta di input di hello toohello [Evaluate Model] [ evaluate-model] modulo - in questo caso, si tratta di modello di albero delle decisioni con Boosting hello. "Scored dataset toocompare" corrisponde toohello destra porta di input - modello SVM hello in questo caso. Quando si fa clic su una delle etichette, curva hello per tale modello è evidenziata e vengono visualizzate le metriche corrispondente hello, come illustrato nella seguente immagine hello.  

![ROC curves for models][4]

Esaminando questi valori, è possibile decidere quale sia il modello toogiving più vicino che Hello risultati che si sta cercando. È possibile tornare indietro e scorrere l'esperimento modificando i valori dei parametri in modelli diversi di hello. 

Scienza Hello ed elementi grafici di interpretare i risultati e ottimizzazione delle prestazioni del modello hello è di fuori ambito hello di questa procedura dettagliata. Per ulteriori informazioni, si potrebbe leggere hello seguenti articoli:
- [Come tooevaluate modello delle prestazioni in Azure Machine Learning](machine-learning-evaluate-model-performance.md)
- [Scegliere i parametri toooptimize algoritmi in Azure Machine Learning](machine-learning-algorithm-parameters-optimize.md)
- [Interpretare i risultati dei modelli in Azure Machine Learning](machine-learning-interpret-model-results.md)

> [!TIP]
> Ogni volta che si esegue l'esperimento hello un record di tale iterazione viene mantenuta nella cronologia di esecuzione hello. È possibile visualizzare queste iterazioni e restituire tooany di essi, facendo clic su **Visualizza cronologia di esecuzione** sotto l'area di disegno hello. È anche possibile fare clic su **eseguire precedente** in hello **proprietà** iterazione di toohello tooreturn riquadro immediatamente precedente hello uno è aperta.
> 
> È possibile creare una copia di qualsiasi iterazione dell'esperimento facendo **SAVE AS** sotto l'area di disegno hello. 
> Utilizzo dell'esperimento hello **riepilogo** e **descrizione** proprietà tookeep un record di ciò che si è tentato nelle iterazioni esperimento.
> 
> Per altre informazioni, vedere [Gestire iterazioni dell'esperimento in Azure Machine Learning Studio](machine-learning-manage-experiment-iterations.md).  
> 
> 

- - -
**Passaggio successivo: [distribuire hello web servizio](machine-learning-walkthrough-5-publish-web-service.md)**

[0]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/train-model-select-column.png
[1]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/experiment-with-train-model.png
[2]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/svm-model-added.png
[3]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/final-experiment.png
[4]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/roc-curves.png
[5]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/normalize-data-select-column.png
[6]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/score-model-connected.png
[7]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/both-score-models-added.png
[8]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/evaluate-model-added.png


<!-- Module References -->
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[normalize-data]: https://msdn.microsoft.com/library/azure/986df333-6748-4b85-923d-871df70d6aaf/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
[two-class-boosted-decision-tree]: https://msdn.microsoft.com/library/azure/e3c522f8-53d9-4829-8ea4-5c6a6b75330c/
[two-class-support-vector-machine]: https://msdn.microsoft.com/library/azure/12d8479b-74b4-4e67-b8de-d32867380e20/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
