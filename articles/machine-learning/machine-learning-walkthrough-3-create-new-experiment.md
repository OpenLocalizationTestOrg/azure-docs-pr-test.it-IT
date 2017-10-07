---
title: 'Passaggio 3: Creare un nuovo esperimento di Machine Learning | Documentazione Microsoft'
description: 'Passaggio 3 di hello sviluppare una procedura dettagliata soluzione predittiva: creare un nuovo esperimento di training in Azure Machine Learning Studio.'
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 660e3c27-55ef-4c33-a4e9-dff4d1224630
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 4697d461a205c50c8d2aa6a3bd56697840cb30f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-3-create-a-new-azure-machine-learning-experiment"></a>Passaggio 3 della procedura dettagliata: Creare un nuovo esperimento di Machine Learning di Azure
Si tratta di hello passaggio terza procedura dettagliata, hello [sviluppare una soluzione analitica predittiva in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)

1. [Creare un'area di lavoro di Machine Learning](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [Caricare i dati esistenti](machine-learning-walkthrough-2-upload-data.md)
3. **Creare un nuovo esperimento**
4. [Eseguire il training e valutare i modelli di hello](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [Distribuzione di servizio Web hello](machine-learning-walkthrough-5-publish-web-service.md)
6. [Accedere al servizio Web hello](machine-learning-walkthrough-6-access-web-service.md)

- - -
passaggio successivo di Hello in questa procedura dettagliata è toocreate un esperimento di Machine Learning Studio che utilizza set di dati hello che è caricati.  

1. In Studio, fare clic su **+ nuovo** nella parte inferiore di hello della finestra hello.
2. Selezionare **EXPERIMENT**e quindi selezionare "Blank Experiment". 

    ![Creare un nuovo esperimento][0]

2. Predefinito selezionare hello sperimentare nome nella parte superiore di hello dell'area di disegno hello e rinominarlo toosomething significativo.

    ![Rinominare l'esperimento][5]
   
   > [!TIP]
   > È una buona norma toofill **riepilogo** e **descrizione** per esperimento hello in hello **proprietà** riquadro. Fornire queste proprietà si hello esperimento di probabilità toodocument hello in modo che chiunque utilizzi in un secondo momento è possibile comprendere gli obiettivi e la metodologia.
   > 
   > ![Proprietà dell'esperimento][6]
   > 
3. In hello modulo tavolozza toohello a sinistra dell'area di disegno esperimento hello, espandere **Saved Datasets**.
4. Trova hello set di dati creati in **set di dati personali** e trascinarlo nell'area di disegno hello. È anche possibile trovare hello set di dati immettendo il nome di hello in hello **ricerca** casella sopra tavolozza hello.  

    ![Aggiungere l'esperimento di toohello hello set di dati][7]

## <a name="prepare-hello-data"></a>Preparare i dati di hello
È possibile visualizzare hello prime 100 righe di dati hello e alcune informazioni statistiche per l'intero set di dati hello: fare clic sulla porta di output di hello del set di dati hello (hello piccolo cerchio nella parte inferiore di hello) e selezionare **Visualizza**.  

Poiché le intestazioni di colonna non è disponibile il file di dati di hello, Studio ha fornito le intestazioni generiche (Col1, Col2, *e così via*). Buona intestazioni non sono essenziali toocreating un modello, ma rendono più semplice toowork con dati hello nell'esperimento hello. Inoltre, quando verrà pubblicato alla fine di questo modello in un servizio web, intestazioni hello consentono di identificare hello colonne toohello utente del servizio hello.  

È possibile aggiungere intestazioni di colonna utilizzando hello [Modifica metadati] [ edit-metadata] modulo.
Utilizzare hello [Modifica metadati] [ edit-metadata] toochange metadati del modulo associato a un set di dati. In questo caso, è utilizzarlo tooprovide nomi più descrittivi per le intestazioni di colonna. 

toouse [Modifica metadati][edit-metadata], è innanzitutto necessario specificare quale toomodify colonne (in questo caso, tutti gli elementi.) Specificare quindi hello azione toobe eseguite su tali colonne (in questo caso, la modifica delle intestazioni di colonna.)

1. Nella tavolozza modulo hello, digitare "metadati" hello **ricerca** casella. Hello [Modifica metadati] [ edit-metadata] viene visualizzato nell'elenco dei moduli di hello.

2. Fare clic e trascinare hello [Modifica metadati] [ edit-metadata] modulo sul hello area di disegno e rilasciarla sotto hello dataset viene aggiunto in precedenza.

3. Connettersi hello dataset toohello [Modifica metadati][edit-metadata]: fare clic sulla porta di output di hello del set di dati hello (hello piccolo cerchio nella parte inferiore di hello del set di dati hello), trascinare una porta di input di toohello [Modifica metadati ] [ edit-metadata] (hello piccolo cerchio nella parte superiore di hello del modulo hello), quindi rilasciare il pulsante di mouse hello. nel modulo e set di dati hello rimangano connesse, anche se uno spostarsi nell'area di disegno hello.
   
   sperimentazione Hello dovrebbe risultare simile al seguente:  
   
   ![Aggiunta di Edit Metadata][1]
   
   punto esclamativo rosso Hello indica che è ancora non impostato le proprietà di hello per questo modulo. Ce ne occuperemo subito.
   
   > [!TIP]
   > È possibile aggiungere un modulo tooa commento facendo doppio clic su modulo hello e immissione di testo. Ciò consente di visualizzare a colpo d'occhio esegue il modulo hello nell'esperimento. In questo caso, fare doppio clic su hello [Modifica metadati] [ edit-metadata] modulo e il tipo hello commento "Add intestazioni di colonna". Fare clic su qualsiasi altra posizione nella casella di testo hello tooclose hello area di disegno. toodisplay hello commento, fare clic sulla freccia hello sul modulo hello.
   > 
   > ![Modulo (Modifica metadati) con il commento aggiunto][8]
   > 
4. Selezionare [Modifica metadati][edit-metadata]e in hello **proprietà** toohello riquadro a destra dell'area di disegno hello, fare clic su **selettore di colonna avvio**.

5. In hello **selezionare colonne** finestra di dialogo, selezionare tutte le righe di hello **colonne disponibili** e fare clic su > toomove li troppo**colonne selezionate**.
   finestra di dialogo Hello dovrebbe essere simile al seguente:

   ![Selettore di colonna con tutte le colonne selezionate][2]

6. Fare clic su hello **OK** segno di spunta.

7. In hello **proprietà** riquadro, cercare hello **nuovi nomi di colonna** parametro. In questo campo, immettere un elenco di nomi per le colonne di 21 hello nel set di dati hello, separati da virgole e nell'ordine delle colonne. È possibile ottenere i nomi delle colonne hello nella documentazione di set di dati hello sul sito UCI hello, oppure per motivi di praticità, è possibile copiare e incollare hello seguente elenco:  
   
       Status of checking account, Duration in months, Credit history, Purpose, Credit amount, Savings account/bond, Present employment since, Installment rate in percentage of disposable income, Personal status and sex, Other debtors, Present residence since, Property, Age in years, Other installment plans, Housing, Number of existing credits, Job, Number of people providing maintenance for, Telephone, Foreign worker, Credit risk  
   
   riquadro Proprietà Hello è simile al seguente:
   
   ![Proprietà per Edit Metadata][3]

> [!TIP]
> Se si desidera intestazioni di colonna hello tooverify, eseguire l'esperimento hello (fare clic su **eseguire** sotto l'area di disegno esperimento hello). Quando al termine dell'esecuzione (viene visualizzato un segno di spunta verde nella [Modifica metadati][edit-metadata]), fare clic sulla porta di output di hello di hello [Modifica metadati] [ edit-metadata] modulo, quindi selezionare **Visualizza**. È possibile visualizzare l'output di hello di qualsiasi modulo in hello stesso modo tooview hello lo stato di avanzamento dei dati di hello tramite esperimento hello.
> 
> 

## <a name="create-training-and-test-datasets"></a>Creazione di set di dati di training e di test
Abbiamo bisogno di un modello di dati tootrain hello e alcuni tootest è.
Pertanto in hello passaggio successivo dell'esperimento hello hello set di dati verranno suddivise in due set di dati separati: uno per il training, il modello e uno per il testing.

toodo, utilizziamo hello [dati divisi] [ split] modulo.  

1. Trovare hello [dati divisi] [ split] modulo, trascinarla nell'area di disegno hello e connetterla toohello [Modifica metadati] [ edit-metadata] modulo.

2. Per impostazione predefinita, il rapporto di divisione hello è 0,5 e hello **divisione casuale** parametro è impostato. Ciò significa che una metà casuale dei dati hello è output tramite una porta di hello [dati divisi] [ split] modulo e metà tramita hello altri. È possibile modificare questi parametri, nonché hello **Random seed** parametro hello toochange suddiviso tra i set di training e dati di testing. Per questo esempio i parametri vengono lasciati inalterati.
   
   > [!TIP]
   > proprietà Hello **frazione di righe in hello set di dati di output prima** determina la quantità di dati hello è output tramite hello *sinistro* porta di output. Ad esempio, se si imposta hello rapporto too0.7, 70% dei dati hello è output tramite hello lasciato porta e il 30% tramite la porta di destra hello.  
   > 
   > 

3. Fare doppio clic su hello [dati divisi] [ split] modulo e immettere il commento hello, "dati di testing/Training divisione 50%". 

È possibile utilizzare l'output di hello di hello [dati divisi] [ split] test come dati di output di modulo, tuttavia è ad esempio, ma è opportuno scegliere toouse hello output a sinistra sotto forma di dati di training e hello destra.  

Come accennato in hello [passaggio precedente](machine-learning-walkthrough-2-upload-data.md), interpretato come un rischio elevato come basso costo hello è cinque volte superiore costo hello interpretato come un rischio di credito bassa come high. tooaccount per questo, si genera un nuovo set di dati che riflette la funzione di costo. In hello nuovo set di dati, ogni esempio ad alto rischio viene replicato cinque volte, ogni esempio basso rischio non viene replicata.   

Ciò è ottenibile usando il codice R:  

1. Individuare e trascinare hello [Execute R Script] [ execute-r-script] modulo nell'area di disegno di hello esperimento. 

2. Connettersi a sinistra sulla porta di output di hello hello [dati divisi] [ split] toohello modulo ("Dataset1") di porta di input prima di hello [Execute R Script] [ execute-r-script] modulo.

3. Fare doppio clic su hello [Execute R Script] [ execute-r-script] modulo e immettere il commento hello, "Set rettifica costo".

4. In hello **proprietà** riquadro testo predefinito hello di eliminazione in hello **Script R** parametro e immettere lo script:
   
       dataset1 <- maml.mapInputPort(1)
       data.set<-dataset1[dataset1[,21]==1,]
       pos<-dataset1[dataset1[,21]==2,]
       for (i in 1:5) data.set<-rbind(data.set,pos)
       maml.mapOutputPort("data.set")

    ![Script R nel modulo Execute R Script hello][9]

È necessario toodo la stessa operazione di replica per ogni output di hello [dati divisi] [ split] rettifica costo di modulo in modo da avere hello che hello set di training e dati di test stesso. Hello più semplice toodo modo tratta duplicando hello [Execute R Script] [ execute-r-script] modulo è appena creata e connetterlo toohello altri output porta di hello [dati divisi] [ split] modulo.

1. Pulsante destro del mouse hello [Execute R Script] [ execute-r-script] modulo e selezionare **copia**.

2. Area di disegno esperimento hello e scegliere **Incolla**.

3. Trascinare il nuovo modulo hello nella posizione e quindi connettere la porta di output di destra hello di hello [dati divisi] [ split] modulo toohello prima porta di input di questo nuovo [Execute R Script] [ execute-r-script] modulo. 

4. Nella parte inferiore di hello dell'area di disegno hello, fare clic su **eseguire**. 

> [!TIP]
> copia di Hello del modulo Execute R Script hello contiene hello stesso script come modulo originale hello. Quando si copia e Incolla di un modulo nell'area di disegno hello, copia hello mantiene tutte le proprietà di hello di hello originale.  
> 
> 

L'esperimento avrà ora un aspetto analogo al seguente:

![Adding Split module and R scripts][4]

Per altre informazioni sull'uso di script R negli esperimenti, vedere [Estendere l'esperimento con R](machine-learning-extend-your-experiment-with-r.md).

**Passaggio successivo: [Train e valutare i modelli di hello](machine-learning-walkthrough-4-train-and-evaluate-models.md)**

[0]: ./media/machine-learning-walkthrough-3-create-new-experiment/create-new-experiment.png
[5]: ./media/machine-learning-walkthrough-3-create-new-experiment/rename-experiment.png
[6]: ./media/machine-learning-walkthrough-3-create-new-experiment/experiment-properties.png
[7]: ./media/machine-learning-walkthrough-3-create-new-experiment/add-dataset-to-experiment.png
[8]: ./media/machine-learning-walkthrough-3-create-new-experiment/edit-metadata-with-comment.png
[9]: ./media/machine-learning-walkthrough-3-create-new-experiment/execute-r-script.png
[1]: ./media/machine-learning-walkthrough-3-create-new-experiment/experiment-with-edit-metadata-module.png
[2]: ./media/machine-learning-walkthrough-3-create-new-experiment/select-columns.png
[3]: ./media/machine-learning-walkthrough-3-create-new-experiment/edit-metadata-properties.png
[4]: ./media/machine-learning-walkthrough-3-create-new-experiment/experiment.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
