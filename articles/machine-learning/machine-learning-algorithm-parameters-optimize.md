---
title: aaaOptimize algoritmi in Azure Machine Learning | Documenti Microsoft
description: Viene illustrato come impostare parametri di toochoose hello ottimale per un algoritmo in Azure Machine Learning.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 6717e30e-b8d8-4cc1-ad0b-1d4727928d32
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: fbf2f71abdbce19483fb048d67a39cbb368a928e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="choose-parameters-toooptimize-your-algorithms-in-azure-machine-learning"></a>Scegliere i parametri toooptimize algoritmi in Azure Machine Learning
In questo argomento viene descritto come toochoose hello destra hyperparameter impostare per un algoritmo in Azure Machine Learning. La maggior parte degli algoritmi di machine learning sono tooset parametri. Durante il training di un modello, è necessario tooprovide valori per tali parametri. efficacia Hello del modello con training hello dipende dai parametri di modello di hello prescelto. Hello processo di individuazione set ottimale di hello dei parametri è noto come *selezione del modello*.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Esistono vari selezione modello toodo di modi. La convalida incrociata è uno dei metodi hello più ampiamente utilizzato per la selezione di modello in machine learning ed è un meccanismo di selezione del modello predefinito hello in Azure Machine Learning. Poiché Azure Machine Learning supporta R e Python, è sempre possibile implementare i relativi meccanismi di selezione del modello tramite R o Python.

Esistono quattro passaggi nel processo di hello di hello migliore set di parametri di ricerca:

1. **Definire spazio parametro hello**: per l'algoritmo di hello, innanzitutto stabilire i valori di parametro corretti hello da tooconsider.
2. **Definire le impostazioni di convalida incrociata hello**: decidere come la convalida incrociata toochoose Raggruppa per set di dati hello.
3. **Definire la metrica hello**: decidere quali toouse metrica per la determinazione hello miglior set di parametri, ad esempio accuratezza, quadratico medio, errore, precisione, richiamo o punteggio f.
4. **Eseguire il training, valutare e confrontare**: svolte dai, basata sulla metrica errore hello definita per ogni combinazione univoca di valori di parametro hello, la convalida incrociata. Dopo la valutazione e confronto, è possibile scegliere modello di prestazioni migliori hello.

Hello seguente immagine illustra Mostra come questo può essere realizzato in Azure Machine Learning.

![Trovare il set di parametri migliore hello](./media/machine-learning-algorithm-parameters-optimize/fig1.png)

## <a name="define-hello-parameter-space"></a>Definire spazio parametro hello
È possibile definire il parametro hello impostato in fase di inizializzazione modello hello. riquadro dei parametri di tutti gli algoritmi di machine learning Hello è disponibili due modalità trainer: *singolo parametro* e *Parameterrange*. Scegliere la modalità intervallo di parametri. Nella modalità intervallo di parametri è possibile immettere più valori per ogni parametro. Nella casella di testo hello, è possibile immettere valori separati da virgola.

![Albero delle decisioni a due classi con innalzamento, parametro singolo](./media/machine-learning-algorithm-parameters-optimize/fig2.png)

 In alternativa, è possibile definire i punti massimo e minimo di hello di griglia hello e hello del numero totale di punti toobe generato con **Usa il generatore di intervallo**. Per impostazione predefinita, i valori dei parametri hello vengono generati su una scala lineare. Tuttavia, se **scala logaritmica** è selezionata, vengono generati valori hello in scala logaritmica hello (rapporto hello tra punti adiacenti hello è costante anziché la relativa differenza). Per i parametri Integer, è possibile definire un intervallo tramite un segno meno. Ad esempio, "1-10" significa che tutti i numeri interi compresi tra 1 e 10 (inclusi) formano il set di parametri di hello. È supportata anche una modalità mista. Ad esempio, hello set di parametri "1-10, 20, 50" includono numeri interi da 1 a 10, 20 e 50.

![Albero delle decisioni a due classi con innalzamento, intervallo di parametri](./media/machine-learning-algorithm-parameters-optimize/fig3.png)

## <a name="define-cross-validation-folds"></a>Definire le riduzioni di convalida incrociata
Hello [Partition and Sample] [ partition-and-sample] modulo può essere utilizzato toorandomly assegnare riduzioni toohello dati. Nel seguente esempio di configurazione per il modulo hello di hello, si definiscono cinque sezioni e assegna in modo casuale una sezione numero di istanze esempio toohello.

![Partition and sample (Partizione ed esempio)](./media/machine-learning-algorithm-parameters-optimize/fig4.png)

## <a name="define-hello-metric"></a>Definire la metrica hello
Hello [ottimizzare modello Iperparametri] [ tune-model-hyperparameters] modulo fornisce il supporto per la scelta in modo empirico hello miglior set di parametri per un set di dati e l'algoritmo specificato. Inoltre tooother informazioni hello training del modello, hello **proprietà** riquadro di questo modulo include la metrica hello per determinare il set di parametri migliore hello. E ha due elenchi a discesa rispettivamente per gli algoritmi di classificazione e di regressione. Se l'algoritmo hello presi in considerazione è un algoritmo di classificazione, la metrica di regressione hello viene ignorata e viceversa. In questo esempio specifico, è la metrica hello **accuratezza**.   

![Organizzare i parametri](./media/machine-learning-algorithm-parameters-optimize/fig5.png)

## <a name="train-evaluate-and-compare"></a>Eseguire il training, valutare e confrontare
Hello stesso [ottimizzare modello Iperparametri] [ tune-model-hyperparameters] modulo esegue il training di tutti i modelli di hello che corrispondono a set di parametri toohello, valuta diverse metriche e quindi Crea modello sottoposto a training con mapping più appropriato di hello basato su hello metrica che scelta. Tale modulo dispone di due input obbligatori:

* strumento di apprendimento senza training Hello
* set di dati Hello

modulo di Hello dispone anche di un set di dati di input facoltativo. Connettersi hello dataset con un set di dati obbligatorio riduzione informazioni toohello input. Se non è assegnata qualsiasi informazione di riduzione hello set di dati, una 10-fold la convalida incrociata viene eseguita automaticamente per impostazione predefinita. Se non è stata effettuata l'assegnazione riduzione hello e viene fornito un set di dati di convalida alla porta di set di dati facoltativo hello, viene scelta una modalità train, test e hello primo set di dati è il modello di hello tootrain utilizzati per ogni combinazione di parametri.

![Classificatore dell'albero delle decisioni con innalzamento](./media/machine-learning-algorithm-parameters-optimize/fig6a.png)

modello Hello viene quindi valutata sul set di dati di hello convalida. Hello lasciato la porta di output di hello modulo Mostra metriche come funzioni di valori di parametro. Hello destra porta di output fornisce modello con training hello corrispondente al modello di prestazioni migliori toohello in base toohello scelto metrica (**accuratezza** in questo caso).  

![Set di dati di convalida](./media/machine-learning-algorithm-parameters-optimize/fig6b.png)

È possibile visualizzare i parametri esatti di hello scelti visualizzando hello porta di output di destra. Questo modello può essere utilizzato per la valutazione in un set di test o in un servizio web operativo dopo il salvataggio come modello per il training.

<!-- Module References -->
[partition-and-sample]: https://msdn.microsoft.com/library/azure/a8726e34-1b3e-4515-b59a-3e4a475654b8/
[tune-model-hyperparameters]: https://msdn.microsoft.com/library/azure/038d91b6-c2f2-42a1-9215-1f2c20ed1b40/
