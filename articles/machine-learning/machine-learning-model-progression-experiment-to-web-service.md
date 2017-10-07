---
title: un modello di Azure Machine Learning aaaHow diventa un servizio web | Documenti Microsoft
description: Una panoramica dei meccanismi di hello di come il avanzamento del modello di Azure Machine Learning da uno sviluppo sperimentare tooan operativi del servizio Web.
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 25e0c025-f8b0-44ab-beaf-d0f2d485eb91
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: 2bbe09fa8fa22662cf8ec4a8b6249d23c87c8ddf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-a-machine-learning-model-progresses-from-an-experiment-tooan-operationalized-web-service"></a>Come l'avanzamento un modello di Machine Learning da un esperimento di tooan operativi del servizio Web
Azure Machine Learning Studio fornisce un'area di disegno interattivo che consente di toodevelop, eseguire, testare ed eseguire l'iterazione un ***sperimentare*** che rappresenta un modello di analisi predittiva. Sono disponibili diversi moduli che consentono di:

* Immettere i dati nell'esperimento
* Modificare i dati di hello
* Eseguire il training di un modello usando algoritmi di Machine Learning
* Modello di punteggio hello
* Valutare i risultati di hello
* Restituire i valori finali

Quando l'esperimento soddisfa le esigenze, è possibile distribuirlo come ***servizio Web classico di Azure Machine Learning*** o come ***nuovo servizio Web di Azure Machine Learning***, per consentire agli utenti di inviare nuovi dati e ricevere i risultati.

In questo articolo viene fornita una panoramica dei meccanismi di hello di come l'avanzamento il modello di Machine Learning da un tooan esperimento di sviluppo operativi del servizio Web.

> [!NOTE]
> Esistono altri modi toodevelop e distribuire modelli di machine learning, ma in questo articolo è incentrato sulle modalità di utilizzo di Machine Learning Studio. Ad esempio, una descrizione di come toocreate un servizio Web predittivo classico con R, vedere hello post di blog di tooread [compilazione & distribuire predittiva Web App utilizzando RStudio e Azure ML](http://blogs.technet.com/b/machinelearning/archive/2015/09/25/build-and-deploy-a-predictive-web-app-using-rstudio-and-azure-ml.aspx).
> 
> 

Mentre Azure Machine Learning Studio è toohelp progettato sviluppare e distribuire un *modello di analisi predittiva*, è possibile toouse Studio toodevelop un esperimento che non include un modello di analisi predittiva. Ad esempio, un esperimento potrebbe dati di solo input, modificare e quindi riportare i risultati di hello. Analogamente a un esperimento di analisi predittiva, è possibile distribuire questo non predittiva esperimento come servizio Web, ma è un processo più semplice perché non è di training o la valutazione di un modello di machine learning esperimento hello. Sebbene non sia hello tipico toouse Studio in questo modo, verrà incluso in discussione hello in modo che in questo modo una spiegazione completa del funzionamento di Studio.

## <a name="developing-and-deploying-a-predictive-web-service"></a>Sviluppo e distribuzione di un servizio Web predittivo
Ecco le fasi hello una tipica soluzione segue quando si sviluppano e distribuirlo Machine Learning Studio:

![Flusso di distribuzione](media/machine-learning-model-progression-experiment-to-web-service/model-stages-from-experiment-to-web-service.png)

*Figura 1 - Fasi di un modello di analisi predittiva tipico*

### <a name="hello-training-experiment"></a>esperimento di training Hello
Hello ***esperimento di training*** hello fase iniziale di sviluppo il servizio Web Machine Learning Studio. Hello esperimento di training hello mira toogive un toodevelop sul posto, testare, eseguire l'iterazione e infine eseguire il training di un modello di machine learning. È possibile anche eseguire il training più modelli contemporaneamente quando si cerca la soluzione migliore di hello, ma dopo aver sperimentato si selezionerà un singolo stato sottoposto a training del modello ed eliminare hello rest da esperimento hello. Per un esempio di sviluppo di un esperimento di analisi predittiva, vedere [Sviluppare una soluzione di analisi predittiva per la valutazione del rischio di credito in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md).

### <a name="hello-predictive-experiment"></a>sperimentazione predittiva Hello
Dopo aver creato un modello con training nell'esperimento di training, fare clic su **di servizio Web** e selezionare **servizio Web predittivo** nel processo di hello tooinitiate Machine Learning Studio di conversione del training Provare tooa ***esperimento predittiva***. scopo dell'esperimento predittiva hello Hello è toouse i modello con training tooscore nuovi dati, con l'obiettivo hello di infine diventare operativi come servizio Web di Azure.

Questa conversione viene eseguita automaticamente tramite hello alla procedura seguente:

* Convertire il set di hello dei moduli utilizzati per il training in un unico modulo e salvarlo come un modello con training
* Eliminare tutti i moduli estranei non correlati tooscoring
* Aggiungere l'input e output porte hello eventuale Web verrà utilizzato dal servizio

Potrebbero essere presenti ulteriori modifiche toomake tooget il toodeploy pronto predittiva esperimento come servizio Web. Ad esempio, se si desidera hello Web servizio toooutput solo un subset dei risultati, è possibile aggiungere un modulo di filtro porta di output di hello.

In questo processo di conversione, non viene scartata esperimento di training hello. Una volta completato il processo di hello, si dispongono di due schede in Studio: uno per esperimento di training hello e uno per la prova predittiva hello. In questo modo è possibile apportare modifiche esperimento di training toohello prima di distribuire il servizio Web e ricompilare l'esperimento predittiva hello. Oppure è possibile salvare una copia di toostart esperimento di training hello un'altra riga di sperimentazione.

> [!NOTE]
> Quando fa clic su **servizio Web predittivo** si avvia un processo automatico di tooconvert l'esperimento di training esperimento tooa predittiva, che funziona bene nella maggior parte dei casi. Se l'esperimento di training è complessa (ad esempio, si dispone di più percorsi per il training che si uniscono), è preferibile toodo questa conversione manualmente. Per ulteriori informazioni, vedere [come tooprepare il modello per la distribuzione in Azure Machine Learning Studio](machine-learning-convert-training-experiment-to-scoring-experiment.md).
> 
> 

### <a name="hello-web-service"></a>Hello servizio Web
Quando l'esperimento predittivo soddisfa le esigenze, è possibile distribuire il servizio come servizio Web classico o nuovo servizio Web basato su Azure Resource Manager. toooperationalize il modello di distribuzione come un *servizio Web di Learning classico macchina*, fare clic su **distribuzione servizio Web** e selezionare **distribuzione di un servizio Web [classica]**. toodeploy come *servizio nuovo Web di Machine Learning*, fare clic su **distribuzione servizio Web** e selezionare **distribuzione servizio Web [New]**. Gli utenti possono ora modello tooyour dati utilizzando l'API REST del servizio Web hello di inviare e ricevere i risultati di hello indietro. Per ulteriori informazioni, vedere [come un servizio Web di Azure Machine Learning tooconsume](machine-learning-consume-web-services.md).

## <a name="hello-non-typical-case-creating-a-non-predictive-web-service"></a>non avviene Hello: creazione di un servizio Web non predittiva
Se l'esperimento non eseguire il training un modello di analisi predittiva, sarà necessario toocreate sia un esperimento di training e un esperimento di assegnazione dei punteggi: è presente solo un esperimento e distribuirla come servizio Web. Machine Learning Studio rileva se l'esperimento contiene un modello predittivo analizzando i moduli di hello che è stato utilizzato.

Dopo avere eseguito l'iterazione dell'esperimento e averlo verificato:

1. Fare clic su **Set Up Web Service** (Configura servizio Web) e selezionare **Retraining Web Service** (Servizio Web di ripetizione del training). I nodi di input e di output verranno aggiunti automaticamente.
2. Fare clic su **Run**
3. Fare clic su **distribuzione servizio Web** e selezionare **distribuzione di un servizio Web [classica]** o **distribuzione servizio Web [New]** a seconda di hello ambiente toowhich si desideri toodeploy.

Il servizio Web ora è distribuito ed è possibile accedervi e gestirlo proprio come si fa con un servizio Web predittivo.

## <a name="updating-your-web-service"></a>Aggiornamento del servizio Web
Dopo aver distribuito l'esperimento come servizio Web, cosa accade se è necessario tooupdate è?

È necessario che dipende da tooupdate:

**Si desidera toochange hello input o output o si desidera toomodify come servizio Web hello modifica i dati**

Se non si modificano il modello di hello, ma modificare solo la modalità di hello servizio Web gestione dati, è possibile modificare l'esperimento predittiva hello e quindi fare clic su **distribuzione servizio Web** e selezionare **distribuzione di un servizio Web [classica]** o **distribuzione servizio Web [New]** nuovamente. Hello servizio Web viene arrestato, hello esperimento predittiva aggiornato viene distribuito e hello servizio Web viene riavviato.

Di seguito è riportato un esempio: si supponga che l'esperimento predittiva restituisce l'intera riga di hello di dati di input con hello risultato stimato. Si potrebbe decidere che il risultato restituito hello toojust di hello Web service. È possibile aggiungere un **Project Columns** modulo nell'esperimento predittiva hello, prima della porta, di output di hello tooexclude colonne diverso da hello risultato. Quando fa clic su **distribuzione servizio Web** e selezionare **distribuzione di un servizio Web [classica]** o **distribuzione servizio Web [New]** nuovamente, hello servizio Web viene aggiornato.

**Si desidera tooretrain hello modello con nuovi dati**

Se si desidera tookeep il modello di machine learning, ma si desidera tooretrain, con i nuovi dati, sono disponibili due opzioni:

1. **Ripetere il training del modello di hello mentre è in esecuzione il servizio Web hello** -se si desidera tooretrain modello mentre è in esecuzione il servizio Web predittivo di hello, è possibile farlo apportando poche modifiche toohello training esperimento toomake è un *** ripetizione di training esperimento***, quindi è possibile distribuirlo come una  ***i web* servizio**. Per istruzioni su come toodo questa operazione, vedere [Machine Learning ripetere il training dei modelli a livello di codice](machine-learning-retrain-models-programmatically.md).
2. **Tornare indietro toohello esperimento di training originale e utilizza il modello di training diversi dati toodevelop** : l'esperimento predittiva è collegato toohello servizio Web, ma l'esperimento di training hello non è collegato direttamente in questo modo. Se si modifica esperimento di training originale hello e fare clic su **di servizio Web**, verrà creato un *nuova* predittiva provare che, quando viene distribuito, verrà creato un *nuova* Web servizio. Non solo aggiorna il servizio Web originale di hello.
   
   Se è necessario esperimento di training hello toomodify, aprirla e fare clic su **Salva con nome** toomake una copia. Lascerà esperimento di training originale intatto hello esperimento predittiva e servizio Web. È quindi possibile creare un nuovo servizio Web con le modifiche. Dopo aver distribuito hello nuovo servizio Web è possibile quindi decidere se toostop hello precedente del servizio Web o continuare a eseguire insieme hello uno nuovo.

**Si desidera un modello diverso tootrain**

Se si desidera toomake cambia tooyour originale predittiva esperimento, quali la selezione di un computer diverso, algoritmo di apprendimento sta tentando di un metodo diverso di training e così via, è necessario seconda procedura hello toofollow descritto in precedenza per la ripetizione di training del modello: Aprire l'esperimento di training hello, fare clic su **Salva con nome** toomake una copia e quindi avviare di nuovo percorso di sviluppo del modello, creazione esperimento predittiva hello e distribuzione di hello verso il basso hello servizio web. Verrà creato un nuovo servizio Web non correlati toohello originale, è possibile decidere quali tookeep uno o entrambi, in esecuzione.

## <a name="next-steps"></a>Passaggi successivi
Per ulteriori informazioni sul processo di hello di sviluppo e test, vedere hello seguenti articoli:

* conversione di sperimentazione hello - [come tooprepare il modello per la distribuzione in Azure Machine Learning Studio](machine-learning-convert-training-experiment-to-scoring-experiment.md)
* distribuzione del servizio Web hello - [distribuire un servizio web Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md)
* i modelli di hello - [Machine Learning ripetere il training dei modelli a livello di codice](machine-learning-retrain-models-programmatically.md)

Per esempi dell'intero processo hello, vedere:

* [Esercitazione di Machine Learning: Creare il primo esperimento in Azure Machine Learning Studio](machine-learning-create-experiment.md)
* [Procedura dettagliata: Sviluppare una soluzione di analisi predittiva per la valutazione del rischio di credito in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)

