---
title: aaaHow tooprepare il modello per la distribuzione in Azure Machine Learning Studio | Documenti Microsoft
description: Come tooprepare il modello con training per la distribuzione come web service convertendo il training di Machine Learning Studio provare tooa predittiva esperimento.
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: eb943c45-541a-401d-844a-c3337de82da6
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/28/2017
ms.author: garye
ms.openlocfilehash: d25bc68be63679a803bfc24a9e29e009a9263f5f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooprepare-your-model-for-deployment-in-azure-machine-learning-studio"></a>Come tooprepare il modello per la distribuzione in Azure Machine Learning Studio

Consente di Azure Machine Learning Studio che Hello strumenti necessari toodevelop un modello analitica predittiva e quindi rendere operativo il mediante la distribuzione come un servizio web di Azure.

toodo, si utilizza toocreate Studio un esperimento - chiamato un *esperimento di training* - in cui eseguire il training, assegnare un punteggio e modificare il modello. Dopo aver verificato, si ottiene il toodeploy pronto modello convertendo il tooa esperimento di training *esperimento predittiva* che è configurato tooscore dati dell'utente.

Un esempio di questo processo è disponibile in [Procedura dettagliata: Sviluppare una soluzione di analisi predittiva per la valutazione del rischio di credito in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md).

In questo articolo prende un approfondimento dettagli hello di come un esperimento di training viene convertito in un esperimento predittivo e la modalità di distribuzione che esperimento predittiva. In base a questi dettagli, è possibile ottenere informazioni come tooconfigure toomake il modello distribuito è più efficace.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="overview"></a>Panoramica 

Hello di conversione di un esperimento di training esperimento tooa predittiva prevede tre passaggi:

1. Sostituire con il modello con training moduli di algoritmo di apprendimento automatico hello.
2. Trim hello esperimento tooonly i moduli che sono necessari per il punteggio. Un esperimento di training include un numero di moduli che sono necessari per il training, ma non sono necessarie dopo il training del modello hello.
3. Definire il modello accetta i dati utente del servizio web hello e quali dati verranno restituiti.

> [!TIP]
> Durante l'esperimento di training, è stato eseguito il training ed è stato assegnato un punteggio al modello utilizzando i propri dati. Ma una volta distribuito, gli utenti inviano di nuovo modello di dati tooyour e verranno restituiti i risultati di stima. In tal caso, quando si converte il tooget predittiva esperimento di training esperimento tooa pronto per la distribuzione, tenere in considerazione come modello hello verrà usato da altri utenti.
> 
> 

## <a name="set-up-web-service-button"></a>Pulsante Set Up Web Service
Dopo aver eseguito l'esperimento (fare clic su **eseguire** nella parte inferiore di hello dell'area di disegno esperimento hello), fare clic su hello **di servizio Web** pulsante (Seleziona hello **servizio Web predittivo** opzione). **Configura Service Web** esegue per si hello tre passaggi di conversione esperimento predittiva tooa esperimento di training:

1. Salva il modello con training nella hello **modelli con training** sezione della tavolozza modulo hello (toohello a sinistra dell'area di disegno esperimento hello). Sostituisce quindi l'algoritmo di apprendimento automatico hello e [Train Model] [ train-model] moduli con hello salvato training del modello.
2. Analizza l'esperimento e rimuove i moduli chiaramente usati solo per il training e non più necessari.
3. Inserisce moduli di _input_ e di _output del servizio Web_ in posizioni predefinite nell'esperimento (questi moduli accettano e restituiscono i dati utente).

Ad esempio, un modello di albero delle decisioni con Boosting due classi utilizzando i dati di esempio census seguente hello provare treni:

![esperimento di training][figure1]

i moduli di Hello in questo esperimento eseguono fondamentalmente quattro diverse funzioni:

![Funzioni del modulo][figure2]

Quando si converte questo esperimento di training esperimento tooa predittiva, alcuni di questi moduli non sono più necessari o ora uno scopo diverso:

* **Dati** -dati hello in questo set di dati di esempio non viene utilizzati durante l'assegnazione dei punteggi - utente hello del servizio web hello fornirà hello toobe di dati con punteggio. Tuttavia, i metadati di hello da questo set di dati, ad esempio tipi di dati, viene utilizzato dal modello con training hello. Pertanto è necessario il set di dati di tookeep hello nell'esperimento predittiva hello in modo da poter fornire i metadati.

* **Prepara** : a seconda dei dati utente hello che verranno inviate per il punteggio, questi moduli possono o non sia necessario tooprocess dati in entrata hello. Hello **di servizio Web** pulsante non tocchi questi, è necessario toodecide come si desidera toohandle li.
  
    Ad esempio, in questo esempio hello esempio set di dati potrebbe essere i valori mancanti, pertanto un [Clean Missing Data] [ clean-missing-data] modulo è stato incluso toodeal con essi. Set di dati campione hello include inoltre le colonne non modello hello tootrain necessari. Pertanto un [selezionare le colonne nel set di dati] [ select-columns] modulo è stato incluso tooexclude queste colonne aggiuntive da hello del flusso di dati. Se i dati di hello che verranno inviati per l'assegnazione dei punteggi tramite hello servizio web non sarà disponibili i valori mancanti, quindi è possibile rimuovere hello [Clean Missing Data] [ clean-missing-data] modulo. Tuttavia, poiché hello [selezionare le colonne nel set di dati] [ select-columns] modulo consente di definire le colonne di hello dei dati prevede che tale modello con training hello, che il modulo richiede tooremain.

* **Train** -questi moduli sono modello hello tootrain utilizzato. Quando fa clic su **di servizio Web**, questi moduli vengono sostituiti con un singolo modulo che contiene il modello di hello training. Questo nuovo modulo viene salvato in hello **modelli con training** sezione della tavolozza modulo hello.

* **Punteggio** : In questo esempio hello [dati divisi] [ split] modulo è utilizzato toodivide flusso di dati hello in dati di test e dati di training. Nell'esperimento predittiva hello, ci stiamo non training più, questa operazione [dati divisi] [ split] può essere rimosso. Analogamente, hello secondo [Score Model] [ score-model] modulo e hello [Evaluate Model] [ evaluate-model] modulo vengono utilizzati toocompare risultati test hello i dati, pertanto questi moduli non sono necessarie in hello predittiva provare. Hello rimanenti [Score Model] [ score-model] modulo, tuttavia, è necessario tooreturn un punteggio di risultati tramite servizio web hello.

Ecco come appare l'esempio dopo aver fatto clic su **Set Up Web Service**:

![Esperimento predittivo convertito][figure3]

Hello lavoro svolto dal **di servizio Web** potrebbe essere sufficiente tooprepare toobe l'esperimento distribuita come servizio web. Tuttavia, è consigliabile toodo alcuni esperimento tooyour specifico di operazioni aggiuntive.

### <a name="adjust-input-and-output-modules"></a>Regolazione dei moduli di input e output
Nell'esperimento di training, è utilizzato un set di dati di training e quindi ha alcuni tooget elaborazione hello dati in un form che hello necessario l'algoritmo di apprendimento automatico. Se non è necessario l'elaborazione dati hello previsti tooreceive tramite servizio web hello, è possibile ignorare: connettere hello output di hello **il modulo di input del servizio Web** tooa modulo diverso nell'esperimento. dati dell'utente Hello arriverà ora nel modello di hello in questa posizione.

Ad esempio, per impostazione predefinita **di servizio Web** inserisce hello **input del servizio Web** modulo nella parte superiore di hello del flusso di dati, come illustrato nella figura hello precedente. Ma è possibile posizionare manualmente hello **input del servizio Web** oltre i moduli di elaborazione dati hello:

![Input del servizio web hello mobile][figure4]

dati di input Hello fornito tramite hello servizio web passerà direttamente nel modulo di modello di punteggio hello senza alcuna pre-elaborazione.

Analogamente, per impostazione predefinita **di servizio Web** inserisce hello modulo output del servizio Web nella parte inferiore di hello del flusso di dati. In questo esempio, servizio web hello restituirà l'output di hello hello utente toohello [Score Model] [ score-model] modulo, che include il vettore di dati di input completo hello e hello punteggio risultati.
Tuttavia, se si desidera tooreturn qualcosa diverso, è possibile aggiungere moduli aggiuntivi prima di hello **output del servizio Web** modulo. 

Ad esempio, tooreturn solo hello punteggio i risultati e non hello intera vettore di dati di input, aggiungere un [selezionare le colonne nel set di dati] [ select-columns] tooexclude modulo tutte le colonne tranne hello punteggio risultati. Spostare quindi hello **output del servizio Web** toohello output del modulo di hello [selezionare le colonne nel set di dati] [ select-columns] modulo. sperimentazione Hello è simile al seguente:

![Lo spostamento di output del servizio web hello][figure5]

### <a name="add-or-remove-additional-data-processing-modules"></a>Aggiungere o rimuovere i moduli di elaborazione dati aggiuntivi
Se presenti nell'esperimento, è possibile rimuove i moduli di cui si è certi che non saranno utili per la classificazione. Ad esempio, quando è stata spostata hello **input del servizio Web** tooa modulo punto dopo hello moduli per l'elaborazione dati, è possibile rimuovere hello [Clean Missing Data] [ clean-missing-data] modulo da sperimentazione predittiva Hello.

L'esperimento predittivo ora appare come illustrato di seguito:

![Rimozione del modulo aggiuntivo][figure6]


### <a name="add-optional-web-service-parameters"></a>Aggiungere parametri facoltativi al servizio Web
In alcuni casi, è consigliabile utente hello tooallow il comportamento hello toochange del servizio web di moduli quando accede al servizio hello. *I parametri di servizio Web* consentono toodo questo.

Un esempio comune sta configurando un [l'importazione dei dati] [ import-data] modulo pertanto utente hello di hello distribuita il servizio web è possibile specificare un'origine dati diversa quando accede al servizio web hello. oppure la configurazione di un modulo [Export Data][export-data] (Esporta dati) in modo che sia possibile specificare una destinazione differente.

È possibile definire i parametri del servizio Web e associarli a uno o più parametri di modulo e specificare se sono obbligatori o facoltativi. utente Hello del servizio web hello fornisce valori per questi parametri quando si accede servizio hello e azioni modulo hello verranno modificate di conseguenza.

Per ulteriori informazioni sui parametri del servizio Web e come toouse, vedere [utilizzando Azure Machine Learning parametri del servizio Web][webserviceparameters].

[webserviceparameters]: machine-learning-web-service-parameters.md


## <a name="deploy-hello-predictive-experiment-as-a-web-service"></a>Distribuire l'esperimento predittiva hello come un servizio web
Ora che esperimento predittiva hello sufficientemente preparato, è possibile distribuirlo come servizio web di Azure. Usa servizio web hello, gli utenti possono inviare modello tooyour dati modello hello restituirà le previsioni.

Per ulteriori informazioni sul processo di distribuzione completa di hello, vedere [distribuire un servizio web Azure Machine Learning][deploy]

[deploy]: machine-learning-publish-a-machine-learning-web-service.md


<!-- Images -->
[figure1]:./media/machine-learning-convert-training-experiment-to-scoring-experiment/figure1.png
[figure2]:./media/machine-learning-convert-training-experiment-to-scoring-experiment/figure2.png
[figure3]:./media/machine-learning-convert-training-experiment-to-scoring-experiment/figure3.png
[figure4]:./media/machine-learning-convert-training-experiment-to-scoring-experiment/figure4.png
[figure5]:./media/machine-learning-convert-training-experiment-to-scoring-experiment/figure5.png
[figure6]:./media/machine-learning-convert-training-experiment-to-scoring-experiment/figure6.png


<!-- Module References -->
[clean-missing-data]: https://msdn.microsoft.com/library/azure/d2c5ca2f-7323-41a3-9b7e-da917c99f0c4/
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
[export-data]: https://msdn.microsoft.com/library/azure/7a391181-b6a7-4ad4-b82d-e419c0d6522c/
