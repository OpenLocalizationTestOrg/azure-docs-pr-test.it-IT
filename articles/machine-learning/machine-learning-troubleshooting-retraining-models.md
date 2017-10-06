---
title: servizio web di ripetizione di training un classico Azure Machine Learning aaaTroubleshoot | Documenti Microsoft
description: "Identificare e correggere riscontra problemi comuni quando si è ripetizione di training modello di hello per un servizio Web di Azure Machine Learning."
services: machine-learning
documentationcenter: 
author: VDonGlover
manager: raymondl
editor: 
ms.assetid: 75cac53c-185c-437d-863a-5d66d871921e
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 2b6a78eaba161877106dccdc23437b5e454fca7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hello-retraining-of-an-azure-machine-learning-classic-web-service"></a>Risoluzione dei problemi hello ripetizione di training di un servizio Web di Azure Machine Learning classico
## <a name="retraining-overview"></a>Panoramica sulla ripetizione del training
Un esperimento predittivo distribuito come servizio Web di assegnazione dei punteggi è un modello statico. Man mano che diventano disponibili nuovi dati o quando il consumer hello di hello API ha i propri dati, il modello di hello deve toobe ripetere il training. 

Per una descrizione completa del processo di un servizio Web classico di ripetizione di training hello, vedere [riqualificare Machine Learning i modelli a livello di codice](machine-learning-retrain-models-programmatically.md).

## <a name="retraining-process"></a>Processo di ripetizione del training
Quando è necessario tooretrain hello servizio Web, è necessario aggiungere alcune parti aggiuntive:

* Un servizio Web distribuito da hello esperimento di Training. sperimentazione Hello deve avere un **Output del servizio Web** modulo collegato toohello output di hello **Train Model** modulo.  
  
    ![Collegare il modello train toohello output di hello web servizio.][image1]
* Un nuovo endpoint aggiunto tooyour punteggio servizio Web.  È possibile aggiungere endpoint hello a livello di codice mediante il codice di esempio hello a cui fa riferimento in hello riqualificare Machine Learning i modelli a livello di programmazione argomento o tramite hello portale di Azure classico.

È quindi possibile utilizzare hello c# codice di esempio dal modello di tooretrain pagina della Guida dell'API del servizio Web formazione di hello. Dopo aver valutato i risultati di hello e si è soddisfatti dei loro, si aggiorna modello con training di hello punteggio servizio web mediante hello nuovo endpoint in cui è stato aggiunto.

Con tutte le parti di hello sul posto, è necessario eseguire il modello di hello tooretrain la passaggi principali hello sono i seguenti:

1. Chiamare hello servizio Web di formazione: hello è toohello servizio esecuzione Batch (BES), non hello richiesta risposta del servizio (RR). È possibile utilizzare codice di esempio c# hello nella chiamata di API hello Guida pagina toomake hello. 
2. Cercare valori hello hello *BaseLocation*, *RelativeLocation*, e *SasBlobToken*: questi valori vengono restituiti nell'output di hello dal toohello chiamata Web Training Servizio. 
   ![visualizzazione di output di hello di hello esempio hello BaseLocation RelativeLocation e SasBlobToken valori di ripetizione di training.][image6]
3. Aggiornamento hello aggiunta endpoint da hello punteggio nuovo servizio web con hello training del modello: mediante il codice di esempio hello fornito in hello Machine Learning ripetere il training dei modelli di aggiornare a livello di codice nuovo endpoint hello toohello valutazione modello con hello appena aggiunto modello con training dallo hello servizio Web di Training.

## <a name="common-obstacles"></a>Ostacoli comuni
### <a name="check-toosee-if-you-have-hello-correct-patch-url"></a>Controllare toosee se si dispone di hello correggere PATCH URL
Hello PATCH l'URL utilizzato deve essere hello associato hello nuovo endpoint di punteggio aggiunto toohello punteggio servizio Web. Esistono numerosi modi tooobtain hello PATCH URL:

**Opzione 1: a livello di codice**

hello tooget correggere PATCH URL:

1. Eseguire hello [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) codice di esempio.
2. Output di hello di AddEndpoint, trovare hello *HelpLocation* valore e copiare l'URL di hello.
   
   ![HelpLocation nell'output di hello dell'esempio addEndpoint hello.][image2]
3. Incollare l'URL di hello in una pagina di tooa toonavigate browser che fornisce i collegamenti della Guida per hello servizio Web.
4. Fare clic su hello **aggiornamento risorsa** pagina della Guida di collegamento tooopen hello patch.

**Opzione 2: Utilizzare hello portale di Azure classico**

1. Accedi toohello [portale di Azure classico](https://manage.windowsazure.com).
2. Scheda di Machine Learning hello aperto. ![Scheda Machine Learning.][image4]
3. Fare clic sul nome dell'area di lavoro, quindi su **Servizi Web**.
4. Fare clic su servizio Web che si lavora con punteggio hello. (Se non è stato modificato il nome predefinito hello del servizio web hello, terminerà in [punteggio Exp]..)
5. Fare clic su **Aggiungi endpoint**.
6. Dopo l'aggiunta di endpoint hello, fare clic su nome endpoint hello. Quindi fare clic su **aggiornamento risorsa** tooopen hello patch pagina della Guida.

> [!NOTE]
> Se sono stati aggiunti hello toohello di endpoint servizio Web di formazione anziché hello predittiva del servizio Web, viene visualizzato il seguente errore quando si fa clic hello hello **aggiornamento risorsa** collegamento: spiacenti, ma questa funzionalità non è supportata o disponibile in questo contesto. Questo servizio Web non dispone di alcuna risorsa aggiornabile. Ci scusiamo per eventuali inconvenienti hello e si sta lavorando a migliorare il flusso di lavoro.
> 
> 

![Dashboard del nuovo endpoint.][image3]

pagina della Guida di PATCH Hello contiene PATCH URL, è necessario utilizzare hello e fornisce il codice di esempio è possibile utilizzare toocall è.

![URL della patch.][image5]

### <a name="check-toosee-that-you-are-updating-hello-correct-scoring-endpoint"></a>Verificare che si sta aggiornando un endpoint di assegnazione dei punteggi corretto hello toosee
* Patch non hello servizio Web di formazione: hello patch operazione deve essere eseguita nel servizio Web di punteggio hello.
* Patch non endpoint predefinito hello su servizio Web: hello patch operazione deve essere eseguita su hello punteggio nuovo endpoint del servizio Web che è stato aggiunto.

È possibile verificare quale endpoint hello del servizio Web è abilitata per hello visita portale di Azure classico. 

> [!NOTE]
> Assicurarsi che si sta aggiungendo hello toohello di endpoint servizio Web predittivo, non hello servizio Web di Training. Se sono stati distribuiti correttamente sia un servizio Web di training che uno predittivo, verranno elencati due servizi Web separati. Servizio Web predittivo Hello deve terminare con "[predittiva exp]"..
> 
> 

1. Accedi toohello [portale di Azure classico](https://manage.windowsazure.com).
2. Scheda di Machine Learning hello aperto. ![Interfaccia utente dell'area di lavoro di Machine Learning.][image4]
3. Selezionare l'area di lavoro.
4. Fare clic su **Servizi Web**.
5. Selezionare il servizio Web predittivo.
6. Verificare che un servizio Web toohello è stato aggiunto il nuovo endpoint.

### <a name="check-hello-workspace-that-your-web-service-is-in-tooensure-it-is-in-hello-correct-region"></a>Controllare hello area di lavoro del servizio web in tooensure che è nell'area corretta hello
1. Accedi toohello [portale di Azure classico](https://manage.windowsazure.com).
2. Selezionare il menu di hello Machine Learning.
   ![Interfaccia utente dell'area di Machine Learning.][image4]
3. Verificare il percorso di hello dell'area di lavoro.

<!-- Image Links -->

[image1]: ./media/machine-learning-troubleshooting-retraining-a-model/ml-studio-tm-connnected-to-web-service-out.png
[image2]: ./media/machine-learning-troubleshooting-retraining-a-model/addEndpoint-output.png
[image3]: ./media/machine-learning-troubleshooting-retraining-a-model/azure-portal-update-resource.png
[image4]: ./media/machine-learning-troubleshooting-retraining-a-model/azure-portal-machine-learning-tab.png
[image5]: ./media/machine-learning-troubleshooting-retraining-a-model/ml-help-page-patch-url.png
[image6]: ./media/machine-learning-troubleshooting-retraining-a-model/retraining-output.png
[image7]: ./media/machine-learning-troubleshooting-retraining-a-model/web-services-tab.png
