---
title: 'Passaggio 5: Distribuzione di servizio web di Machine Learning hello | Documenti Microsoft'
description: 'Passaggio 5 di hello sviluppare una procedura dettagliata soluzione predittiva: distribuire un esperimento predittivo in Machine Learning Studio come un servizio web.'
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 3fca74a3-c44b-4583-a218-c14c46ee5338
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 76391010972ed1450bbda8bfb2352c7b22b51ccc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-5-deploy-hello-azure-machine-learning-web-service"></a>Procedura dettagliata passaggio 5: Distribuzione di servizio web di Azure Machine Learning hello
Si tratta di hello quinto passaggio del processo di questa procedura dettagliata hello, [sviluppare una soluzione analitica predittiva in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)

1. [Creare un'area di lavoro di Machine Learning](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [Caricare i dati esistenti](machine-learning-walkthrough-2-upload-data.md)
3. [Creare un nuovo esperimento](machine-learning-walkthrough-3-create-new-experiment.md)
4. [Eseguire il training e valutare i modelli di hello](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. **Distribuzione di servizio web hello**
6. [Servizio web di accesso hello](machine-learning-walkthrough-6-access-web-service.md)

- - -
toogive altri toouse una possibilità hello modello predittivo abbiamo sviluppato in questa procedura dettagliata, è possibile distribuirla come servizio web in Azure.

Un punto toothis è abbiamo provato a training modello in esame. Ma servizio hello distribuito non verrà toodo training - saranno toogenerate nuove stime per l'input dell'utente hello basato sul nostro modello di punteggio. Pertanto verrà toodo alcuni tooconvert preparazione questo esperimento da un ***training*** sperimentare tooa ***predittiva*** provare. 

Il processo si articola in tre passaggi:  

1. Rimuovere uno dei modelli di hello
2. Convertire hello *esperimento di training* abbiamo creato in un *esperimento predittiva*
3. Distribuire l'esperimento predittiva hello come un servizio web

## <a name="remove-one-of-hello-models"></a>Rimuovere uno dei modelli di hello

Innanzitutto, è necessario tootrim questo esperimento verso il basso un po'. Si dispongono di due modelli diversi in esperimento hello, ma si desidera solo toouse un modello quando si distribuisce questo come un servizio web.  

Si supponga che abbiamo deciso tale modello di struttura ad albero con Boosting hello eseguita meglio di modello SVM hello. Pertanto hello prima cosa toodo hello remove [Two-Class Support Vector Machine] [ two-class-support-vector-machine] modulo e i moduli hello utilizzati per il training. È una copia dell'esperimento hello toomake innanzitutto facendo **Salva con nome** nella parte inferiore di hello di hello provare l'area di disegno.

È necessario hello toodelete seguenti moduli:  

* [Two-Class Support Vector Machine][two-class-support-vector-machine]
* [Eseguire il training del modello] [ train-model] e [Score Model] [ score-model] moduli che sono stati connessi tooit
* [Normalize Data][normalize-data] (entrambi)
* [Valutazione del modello] [ evaluate-model] (perché è terminato la valutazione dei modelli di hello)

Selezionare ogni modulo e premere CANC hello o modulo hello pulsante destro del mouse e selezionare **eliminare**. 

![Modello SVM hello rimosso][3a]

Il modello avrà ora un aspetto analogo al seguente:

![Modello SVM hello rimosso][3]

Ora siamo toodeploy pronto questo modello utilizzando hello [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree].

## <a name="convert-hello-training-experiment-tooa-predictive-experiment"></a>Convertire l'esperimento predittiva tooa di hello esperimento di training

tooget questo modello pronto per la distribuzione, è necessario tooconvert questo esperimento tooa predittiva esperimento di training. Questa operazione comporta tre passaggi:

1. Salvare il modello di hello è stato eseguito il training e sostituire i moduli di training
2. Tagliare i moduli di tooremove esperimento hello necessari solo per il training
3. Definire quale hello web servizio accetta input e in cui viene generato l'output di hello

Impossibile eseguire questa operazione manualmente, ma fortunatamente tutti i tre passaggi possono essere eseguiti facendo clic su **di servizio Web** nella parte inferiore di hello dell'area di disegno esperimento hello (e selezionando hello **servizio Web predittivo** opzione).

> [!TIP]
> Se si desidera visualizzare ulteriori dettagli su cosa accade quando si converte un esperimento di training per tooa predittiva provare, vedere [come tooprepare il modello per la distribuzione in Azure Machine Learning Studio](machine-learning-convert-training-experiment-to-scoring-experiment.md).

Quando si fa clic su **Set Up Web Service**(Configura servizio Web), vengono eseguite diverse operazioni:

* modello con training Hello è convertito tooa singolo **modello con training** modulo e archiviati in hello modulo tavolozza toohello a sinistra di hello provare l'area di disegno (è possibile trovare in **modelli con training**)
* Vengono rimossi i moduli usati per il training, in particolare:
  * [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree]
  * [Train Model][train-model]
  * [Split Data][split]
  * in secondo luogo Hello [Execute R Script] [ execute-r-script] modulo utilizzato per i dati di test
* modello con training Hello salvato viene aggiunto nuovamente nella sperimentazione hello
* **Input del servizio Web** e **output del servizio Web** vengono aggiunti i moduli (questi identificano i dati dell'utente hello in cui verranno attivata la modello hello e i dati da restituire quando accede al servizio web hello)

> [!NOTE]
> È possibile vedere che esperimento hello viene salvato in due parti in schede che sono stati aggiunti nella parte superiore di hello dell'area di disegno di hello esperimento. Hello esperimento di training originale è sotto la scheda hello **esperimento di Training**, ed è appena creato esperimento predittiva hello in **esperimento predittiva**. sperimentazione predittiva Hello è hello uno che vengono distribuiti come un servizio web.

È necessario un passaggio aggiuntivo tootake con questo particolare esperimento.
È stato aggiunto due [Execute R Script] [ execute-r-script] tooprovide moduli un peso funzione toohello dati. Che è solo uno stratagemma che è necessaria per il training e test, pertanto è possibile estrarre i moduli nel modello finale hello.
Machine Learning Studio rimosso uno [Execute R Script] [ execute-r-script] modulo quando rimosso hello [Split] [ split] modulo. Ora è possibile rimuovere altri hello e connettersi [Metadata Editor] [ metadata-editor] direttamente troppo[Score Model][score-model].    

L'esperimento dovrebbe risultare simile al seguente:  

![Modello con training hello di punteggio][4]  

> [!NOTE]
> Si potrebbe chiedere perché è stato lasciato il set di dati di carta di credito tedesco UCI di hello nell'esperimento predittiva hello. servizio Hello verrà tooscore hello dati utente, non hello set di dati originale, pertanto perché lasciare hello set di dati originale nel modello hello?
> 
> È vero che servizio hello non necessario hello originale dei dati della carta di credito. Tuttavia, è necessario schema hello per tali dati, che include informazioni quali il numero di colonne sono disponibili e le colonne sono di tipo numeriche. Queste informazioni sullo schema sono necessario toointerpret hello dati utente. Si lascia questi componenti connessi in modo che hello punteggio modulo dispone dello schema di dataset hello quando è in esecuzione il servizio di hello. dati Hello non viene usati, solo schema di hello.  
> 
> 

Eseguire l'esperimento hello un'ultima volta (fare clic su **eseguire**.) Se si desidera tooverify che hello modello sta ancora lavorando, fare clic su output di hello di hello [Score Model] [ score-model] modulo e selezionare **Visualizza risultati**. È possibile che dati originali hello sono visualizzato, valore di rischio di credito hello ("Scored Labels") e hello punteggio il valore di probabilità ("calcolato il punteggio della probabilità".) 

## <a name="deploy-hello-web-service"></a>Distribuzione di servizio web hello
È possibile distribuire hello esperimento come un servizio web classica o come un nuovo servizio web che si basa su Gestione risorse di Azure.

### <a name="deploy-as-a-classic-web-service"></a>Distribuire l'esperimento come servizio Web classico
toodeploy un classico web servizio derivato da esperimento, fare clic su **distribuzione servizio Web** seguito hello area di disegno e selezionare **distribuzione di un servizio Web [classica]**. Machine Learning Studio distribuisce hello esperimento come servizio web e consente di passare toohello dashboard per il servizio web. In questa pagina è possibile restituire esperimento toohello (**Visualizza lo snapshot** o **visualizzare più recente**) ed eseguire un test semplice del servizio web hello (vedere **Test servizio web hello** sotto). È anche informazioni per la creazione di applicazioni che possono accedere a un servizio web hello (ulteriori informazioni nel passaggio successivo di hello di questa procedura dettagliata).

![Dashboard del servizio Web][6]

È possibile configurare il servizio di hello facendo hello **configurazione** scheda. Qui è possibile modificare il nome di servizio hello (è nome esperimento hello specificato per impostazione predefinita) e assegnare una descrizione. È inoltre possibile assegnare più descrittive etichette per hello dati di input e outpui.  

![Configurare il servizio web hello][5]  

### <a name="deploy-as-a-new-web-service"></a>Distribuire l'esperimento come nuovo servizio Web

> [!NOTE] 
> un nuovo servizio web deve disporre di autorizzazioni sufficienti in hello sottoscrizione toowhich si sta distribuendo toodeploy hello servizio web. Per ulteriori informazioni, vedere [gestire un servizio web tramite il portale di servizi Web di Azure Machine Learning hello](machine-learning-manage-new-webservice.md). 

toodeploy un nuovo servizio web derivata da esperimento:

1. Fare clic su **distribuzione servizio Web** seguito hello area di disegno e selezionare **distribuzione servizio Web [New]**. Machine Learning Studio trasferisce i servizi web Azure Machine Learning toohello **distribuire esperimento** pagina.

2. Immettere un nome per il servizio web hello. 

3. Per **prezzo piano**, è possibile selezionare un piano tariffario esistente o seleziona "nuovo" e concedere hello nuovo piano di un nome e l'opzione piano mensile hello selezionare. piano di Hello livelli predefinito toohello piani per l'area predefinita e il servizio web è distribuito toothat area.

4. Fare clic su **Distribuisci**.

Dopo alcuni minuti, hello **delle Guide rapide** verrà visualizzata la pagina relativa al servizio web.

È possibile configurare il servizio di hello facendo hello **configura** scheda. Qui è possibile modificare il servizio hello title e assegnargli una descrizione. 

hello tootest servizio web, fare clic su hello **Test** scheda (vedere **Test servizio web hello** sotto). Per informazioni sulla creazione di applicazioni che possono accedere hello web servizio, fare clic su hello **consumare** scheda (passaggio successivo di hello in questa procedura dettagliata entra in modo più dettagliato).

> [!TIP]
> Dopo aver distribuito, è possibile aggiornare il servizio di web hello. Ad esempio, se si desidera toochange il modello, quindi è possibile modificare esperimento di training hello, modificare i parametri di modello hello e scegliere **distribuzione servizio Web**, se si seleziona **distribuzione di un servizio Web [classica]** o  **Distribuzione di servizio Web [New]**. Quando si distribuisce nuovamente esperimento hello, sostituisce servizio web hello, ora utilizzando il modello aggiornato.  
> 
> 

## <a name="test-hello-web-service"></a>Servizio web hello di test

Quando si accede a servizio web hello, i dati dell'utente hello passano attraverso hello **input del servizio Web** modulo in cui è passata toohello [Score Model] [ score-model] modulo e con punteggi. modo Hello che è stato configurato l'esperimento predittiva hello, modello hello prevede che i dati in hello stesso formato delle hello credito rischio set di dati originale.
Hello vengono restituiti toohello utente dal servizio web hello tramite hello **output del servizio Web** modulo.

> [!TIP]
> modo Hello abbiamo hello predittiva esperimento configurato, hello intera risultante dalla hello [Score Model] [ score-model] modulo vengono restituiti. Sono inclusi tutti i dati di input hello più valore di rischio di credito hello e hello assegnazione dei punteggi di probabilità. Ma è possibile restituire un elemento diverso se si desidera, ad esempio, è possibile restituire solo valore di rischio per la carta di credito hello. toodo, questa operazione di inserimento un [Project Columns] [ project-columns] modulo tra [Score Model] [ score-model] hello e **outputdelservizioWeb** tooeliminate colonne non desiderate hello tooreturn servizio web. 
> 
> 

È possibile testare un sito web classica service in **Machine Learning Studio** o hello **servizi Web di Azure Machine Learning** portale.
È possibile testare solo un nuovo servizio web hello **servizi Web di Machine Learning** portale.

> [!TIP]
> Durante il test nel portale di servizi Web di Azure Machine Learning hello, è possibile impostare il portale di hello creare dati di esempio che è possibile utilizzare il servizio di richiesta-risposta hello tootest. In hello **configura** pagina, selezionare "Sì" per **dati di esempio abilitata?**. Quando si apre la scheda di richiesta-risposta hello hello **Test** pagina portale hello compila i dati di esempio tratti da hello credito rischio set di dati originale.

### <a name="test-a-classic-web-service"></a>Testare un servizio Web classico

È possibile testare un servizio web classica in Machine Learning Studio o nel portale di servizi Web di Machine Learning hello. 

#### <a name="test-in-machine-learning-studio"></a>Testare in Machine Learning Studio

1. In hello **DASHBOARD** pagina per il servizio web hello, fare clic su hello **Test** pulsante sotto **Endpoint predefinito**. Una finestra di dialogo viene visualizzata e viene chiesto di dati di input per il servizio hello hello. Questi è hello stesse colonne visualizzate in hello credito rischio set di dati originale.  

2. Immettere un set di dati e quindi fare clic su **OK**. 

#### <a name="test-in-hello-machine-learning-web-services-portal"></a>Test nel portale di servizi Web di Machine Learning hello

1. In hello **DASHBOARD** pagina per il servizio web hello, fare clic su hello **anteprima Test** collegamento in **Endpoint predefinito**. pagina di prova Hello nel portale di servizi Web di Azure Machine Learning hello hello endpoint del servizio web viene visualizzata e viene chiesto di dati di input per il servizio hello hello. Questi è hello stesse colonne visualizzate in hello credito rischio set di dati originale.

2. Fare clic su **Test Request-Response** (Test Richiesta-risposta). 

### <a name="test-a-new-web-service"></a>Testare un nuovo servizio Web

È possibile testare un nuovo servizio web solo nel portale di servizi Web di Machine Learning hello.

1. In hello [servizi Web di Azure Machine Learning](https://services.azureml.net/quickstart) portale, fare clic su **Test** nella parte superiore di hello della pagina hello. Hello **Test** verrà visualizzata la pagina e che è possibile inserire i dati per il servizio di hello. i campi di input Hello visualizzati corrispondono toohello colonne visualizzate in hello credito rischio set di dati originale. 

2. Immettere un set di dati e quindi fare clic su **Test Request-Response**(Test Richiesta-risposta).

risultati del test di hello Hello vengono visualizzati sul lato destro di hello della pagina hello nella colonna di output di hello. 


## <a name="manage-hello-web-service"></a>Gestire il servizio web hello

### <a name="manage-a-classic-web-service-in-hello-azure-classic-portal"></a>Gestire un servizio web classica nel portale di Azure classico hello

Dopo aver distribuito il servizio web classica, è possibile gestire dal hello [portale di Azure classico](https://manage.windowsazure.com).

1. Accedi toohello [portale di Azure classico](https://manage.windowsazure.com)
2. Nel Pannello di servizi di Microsoft Azure hello, fare clic su **MACHINE LEARNING**
3. Fare clic sull'area di lavoro.
4. Fare clic su hello **servizi Web** scheda
5. Fare clic su servizio web hello che è stato creato
6. Fare clic sull'endpoint "predefinita" hello

Da qui, è possibile eseguire operazioni quali il monitoraggio esegue il servizio web hello e apportare modifiche delle prestazioni modificando il numero di chiamate simultanee hello servizio può gestire.

Per informazioni dettagliate, vedere:

* [Creazione di endpoint](machine-learning-create-endpoint.md)
* [Ridimensionamento di un servizio Web](machine-learning-scaling-webservice.md)

### <a name="manage-a-classic-or-new-web-service-in-hello-azure-machine-learning-web-services-portal"></a>Gestire un classica o un nuovo servizio web nel portale di servizi Web di Azure Machine Learning hello

Dopo aver distribuito il servizio web, se classico o nuova, è possibile gestire dal hello [servizi Web di Microsoft Azure Machine Learning](https://services.azureml.net/quickstart) portale.

prestazioni di hello toomonitor del servizio web:

1. Accedi toohello [servizi Web di Microsoft Azure Machine Learning](https://services.azureml.net/quickstart) portale
2. Fare clic su **Servizi Web**
3. Fare clic sul servizio Web
4. Fare clic su hello **Dashboard**

- - -
**Passaggio successivo: [accedere al servizio web hello](machine-learning-walkthrough-6-access-web-service.md)**

[3]: ./media/machine-learning-walkthrough-5-publish-web-service/publish3.png
[3a]: ./media/machine-learning-walkthrough-5-publish-web-service/publish3a.png
[4]: ./media/machine-learning-walkthrough-5-publish-web-service/publish4.png
[5]: ./media/machine-learning-walkthrough-5-publish-web-service/publish5.png
[6]: ./media/machine-learning-walkthrough-5-publish-web-service/publish6.png


<!-- Module References -->
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[metadata-editor]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[normalize-data]: https://msdn.microsoft.com/library/azure/986df333-6748-4b85-923d-871df70d6aaf/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
[two-class-boosted-decision-tree]: https://msdn.microsoft.com/library/azure/e3c522f8-53d9-4829-8ea4-5c6a6b75330c/
[two-class-support-vector-machine]: https://msdn.microsoft.com/library/azure/12d8479b-74b4-4e67-b8de-d32867380e20/
[project-columns]: https://msdn.microsoft.com/en-us/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
