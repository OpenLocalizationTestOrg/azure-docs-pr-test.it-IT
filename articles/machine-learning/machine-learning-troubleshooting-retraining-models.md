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
# <a name="troubleshooting-hello-retraining-of-an-azure-machine-learning-classic-web-service"></a><span data-ttu-id="84e8b-103">Risoluzione dei problemi hello ripetizione di training di un servizio Web di Azure Machine Learning classico</span><span class="sxs-lookup"><span data-stu-id="84e8b-103">Troubleshooting hello retraining of an Azure Machine Learning Classic Web service</span></span>
## <a name="retraining-overview"></a><span data-ttu-id="84e8b-104">Panoramica sulla ripetizione del training</span><span class="sxs-lookup"><span data-stu-id="84e8b-104">Retraining overview</span></span>
<span data-ttu-id="84e8b-105">Un esperimento predittivo distribuito come servizio Web di assegnazione dei punteggi è un modello statico.</span><span class="sxs-lookup"><span data-stu-id="84e8b-105">When you deploy a predictive experiment as a scoring web service it is a static model.</span></span> <span data-ttu-id="84e8b-106">Man mano che diventano disponibili nuovi dati o quando il consumer hello di hello API ha i propri dati, il modello di hello deve toobe ripetere il training.</span><span class="sxs-lookup"><span data-stu-id="84e8b-106">As new data becomes available or when hello consumer of hello API has their own data, hello model needs toobe retrained.</span></span> 

<span data-ttu-id="84e8b-107">Per una descrizione completa del processo di un servizio Web classico di ripetizione di training hello, vedere [riqualificare Machine Learning i modelli a livello di codice](machine-learning-retrain-models-programmatically.md).</span><span class="sxs-lookup"><span data-stu-id="84e8b-107">For a complete walkthrough of hello retraining process of a Classic Web service, see [Retrain Machine Learning Models Programmatically](machine-learning-retrain-models-programmatically.md).</span></span>

## <a name="retraining-process"></a><span data-ttu-id="84e8b-108">Processo di ripetizione del training</span><span class="sxs-lookup"><span data-stu-id="84e8b-108">Retraining process</span></span>
<span data-ttu-id="84e8b-109">Quando è necessario tooretrain hello servizio Web, è necessario aggiungere alcune parti aggiuntive:</span><span class="sxs-lookup"><span data-stu-id="84e8b-109">When you need tooretrain hello Web service, you must add some additional pieces:</span></span>

* <span data-ttu-id="84e8b-110">Un servizio Web distribuito da hello esperimento di Training.</span><span class="sxs-lookup"><span data-stu-id="84e8b-110">A Web service deployed from hello Training Experiment.</span></span> <span data-ttu-id="84e8b-111">sperimentazione Hello deve avere un **Output del servizio Web** modulo collegato toohello output di hello **Train Model** modulo.</span><span class="sxs-lookup"><span data-stu-id="84e8b-111">hello experiment must have a **Web Service Output** module attached toohello output of hello **Train Model** module.</span></span>  
  
    ![Collegare il modello train toohello output di hello web servizio.][image1]
* <span data-ttu-id="84e8b-113">Un nuovo endpoint aggiunto tooyour punteggio servizio Web.</span><span class="sxs-lookup"><span data-stu-id="84e8b-113">A new endpoint added tooyour scoring Web service.</span></span>  <span data-ttu-id="84e8b-114">È possibile aggiungere endpoint hello a livello di codice mediante il codice di esempio hello a cui fa riferimento in hello riqualificare Machine Learning i modelli a livello di programmazione argomento o tramite hello portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="84e8b-114">You can add hello endpoint programmatically using hello sample code referenced in hello Retrain Machine Learning models programmatically topic or through hello Azure classic portal.</span></span>

<span data-ttu-id="84e8b-115">È quindi possibile utilizzare hello c# codice di esempio dal modello di tooretrain pagina della Guida dell'API del servizio Web formazione di hello.</span><span class="sxs-lookup"><span data-stu-id="84e8b-115">You can then use hello sample C# code from hello Training Web Service's API help page tooretrain model.</span></span> <span data-ttu-id="84e8b-116">Dopo aver valutato i risultati di hello e si è soddisfatti dei loro, si aggiorna modello con training di hello punteggio servizio web mediante hello nuovo endpoint in cui è stato aggiunto.</span><span class="sxs-lookup"><span data-stu-id="84e8b-116">Once you have evaluated hello results and are satisfied with them, you update hello trained model scoring web service using hello new endpoint that you added.</span></span>

<span data-ttu-id="84e8b-117">Con tutte le parti di hello sul posto, è necessario eseguire il modello di hello tooretrain la passaggi principali hello sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="84e8b-117">With all hello pieces in place, hello major steps you must take tooretrain hello model are as follows:</span></span>

1. <span data-ttu-id="84e8b-118">Chiamare hello servizio Web di formazione: hello è toohello servizio esecuzione Batch (BES), non hello richiesta risposta del servizio (RR).</span><span class="sxs-lookup"><span data-stu-id="84e8b-118">Call hello Training Web Service:  hello call is toohello Batch Execution Service (BES), not hello Request Response Service (RRS).</span></span> <span data-ttu-id="84e8b-119">È possibile utilizzare codice di esempio c# hello nella chiamata di API hello Guida pagina toomake hello.</span><span class="sxs-lookup"><span data-stu-id="84e8b-119">You can use hello sample C# code on hello API help page toomake hello call.</span></span> 
2. <span data-ttu-id="84e8b-120">Cercare valori hello hello *BaseLocation*, *RelativeLocation*, e *SasBlobToken*: questi valori vengono restituiti nell'output di hello dal toohello chiamata Web Training Servizio.</span><span class="sxs-lookup"><span data-stu-id="84e8b-120">Find hello values for hello *BaseLocation*, *RelativeLocation*, and *SasBlobToken*: These values are returned in hello output from your call toohello Training Web Service.</span></span> 
   <span data-ttu-id="84e8b-121">![visualizzazione di output di hello di hello esempio hello BaseLocation RelativeLocation e SasBlobToken valori di ripetizione di training.][image6]</span><span class="sxs-lookup"><span data-stu-id="84e8b-121">![showing hello output of hello retraining sample and hello BaseLocation, RelativeLocation, and  SasBlobToken values.][image6]</span></span>
3. <span data-ttu-id="84e8b-122">Aggiornamento hello aggiunta endpoint da hello punteggio nuovo servizio web con hello training del modello: mediante il codice di esempio hello fornito in hello Machine Learning ripetere il training dei modelli di aggiornare a livello di codice nuovo endpoint hello toohello valutazione modello con hello appena aggiunto modello con training dallo hello servizio Web di Training.</span><span class="sxs-lookup"><span data-stu-id="84e8b-122">Update hello added endpoint from hello scoring web service with hello new trained model: Using hello sample code provided in hello Retrain Machine Learning models programmatically, update hello new endpoint you added toohello scoring model with hello newly trained model from hello Training Web Service.</span></span>

## <a name="common-obstacles"></a><span data-ttu-id="84e8b-123">Ostacoli comuni</span><span class="sxs-lookup"><span data-stu-id="84e8b-123">Common obstacles</span></span>
### <a name="check-toosee-if-you-have-hello-correct-patch-url"></a><span data-ttu-id="84e8b-124">Controllare toosee se si dispone di hello correggere PATCH URL</span><span class="sxs-lookup"><span data-stu-id="84e8b-124">Check toosee if you have hello correct PATCH URL</span></span>
<span data-ttu-id="84e8b-125">Hello PATCH l'URL utilizzato deve essere hello associato hello nuovo endpoint di punteggio aggiunto toohello punteggio servizio Web.</span><span class="sxs-lookup"><span data-stu-id="84e8b-125">hello PATCH URL you are using must be hello one associated with hello new scoring endpoint you added toohello scoring Web service.</span></span> <span data-ttu-id="84e8b-126">Esistono numerosi modi tooobtain hello PATCH URL:</span><span class="sxs-lookup"><span data-stu-id="84e8b-126">There are a number of ways tooobtain hello PATCH URL:</span></span>

<span data-ttu-id="84e8b-127">**Opzione 1: a livello di codice**</span><span class="sxs-lookup"><span data-stu-id="84e8b-127">**Option 1: Programatically**</span></span>

<span data-ttu-id="84e8b-128">hello tooget correggere PATCH URL:</span><span class="sxs-lookup"><span data-stu-id="84e8b-128">tooget hello correct PATCH URL:</span></span>

1. <span data-ttu-id="84e8b-129">Eseguire hello [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) codice di esempio.</span><span class="sxs-lookup"><span data-stu-id="84e8b-129">Run hello [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) sample code.</span></span>
2. <span data-ttu-id="84e8b-130">Output di hello di AddEndpoint, trovare hello *HelpLocation* valore e copiare l'URL di hello.</span><span class="sxs-lookup"><span data-stu-id="84e8b-130">From hello output of AddEndpoint, find hello *HelpLocation* value and copy hello URL.</span></span>
   
   ![HelpLocation nell'output di hello dell'esempio addEndpoint hello.][image2]
3. <span data-ttu-id="84e8b-132">Incollare l'URL di hello in una pagina di tooa toonavigate browser che fornisce i collegamenti della Guida per hello servizio Web.</span><span class="sxs-lookup"><span data-stu-id="84e8b-132">Paste hello URL into a browser toonavigate tooa page that provides help links for hello Web service.</span></span>
4. <span data-ttu-id="84e8b-133">Fare clic su hello **aggiornamento risorsa** pagina della Guida di collegamento tooopen hello patch.</span><span class="sxs-lookup"><span data-stu-id="84e8b-133">Click hello **Update Resource** link tooopen hello patch help page.</span></span>

<span data-ttu-id="84e8b-134">**Opzione 2: Utilizzare hello portale di Azure classico**</span><span class="sxs-lookup"><span data-stu-id="84e8b-134">**Option 2: Use hello Azure classic portal**</span></span>

1. <span data-ttu-id="84e8b-135">Accedi toohello [portale di Azure classico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="84e8b-135">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="84e8b-136">Scheda di Machine Learning hello aperto. ![Scheda Machine Learning.][image4]</span><span class="sxs-lookup"><span data-stu-id="84e8b-136">Open hello Machine Learning tab. ![Machine leaning tab.][image4]</span></span>
3. <span data-ttu-id="84e8b-137">Fare clic sul nome dell'area di lavoro, quindi su **Servizi Web**.</span><span class="sxs-lookup"><span data-stu-id="84e8b-137">Click your workspace name, then **Web Services**.</span></span>
4. <span data-ttu-id="84e8b-138">Fare clic su servizio Web che si lavora con punteggio hello.</span><span class="sxs-lookup"><span data-stu-id="84e8b-138">Click hello scoring Web service you are working with.</span></span> <span data-ttu-id="84e8b-139">(Se non è stato modificato il nome predefinito hello del servizio web hello, terminerà in [punteggio Exp]..)</span><span class="sxs-lookup"><span data-stu-id="84e8b-139">(If you did not modify hello default name of hello web service, it will end in [Scoring Exp.].)</span></span>
5. <span data-ttu-id="84e8b-140">Fare clic su **Aggiungi endpoint**.</span><span class="sxs-lookup"><span data-stu-id="84e8b-140">Click **Add Endpoint**.</span></span>
6. <span data-ttu-id="84e8b-141">Dopo l'aggiunta di endpoint hello, fare clic su nome endpoint hello.</span><span class="sxs-lookup"><span data-stu-id="84e8b-141">After hello endpoint is added, click hello endpoint name.</span></span> <span data-ttu-id="84e8b-142">Quindi fare clic su **aggiornamento risorsa** tooopen hello patch pagina della Guida.</span><span class="sxs-lookup"><span data-stu-id="84e8b-142">Then click **Update Resource** tooopen hello patching help page.</span></span>

> [!NOTE]
> <span data-ttu-id="84e8b-143">Se sono stati aggiunti hello toohello di endpoint servizio Web di formazione anziché hello predittiva del servizio Web, viene visualizzato il seguente errore quando si fa clic hello hello **aggiornamento risorsa** collegamento: spiacenti, ma questa funzionalità non è supportata o disponibile in questo contesto.</span><span class="sxs-lookup"><span data-stu-id="84e8b-143">If you have added hello endpoint toohello Training Web Service instead of hello Predictive Web Service, you will receive hello following error when you click hello **Update Resource** link: Sorry, but this feature is not supported or available in this context.</span></span> <span data-ttu-id="84e8b-144">Questo servizio Web non dispone di alcuna risorsa aggiornabile.</span><span class="sxs-lookup"><span data-stu-id="84e8b-144">This Web Service has no updatable resources.</span></span> <span data-ttu-id="84e8b-145">Ci scusiamo per eventuali inconvenienti hello e si sta lavorando a migliorare il flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="84e8b-145">We apologize for hello inconvenience and are working on improving this workflow.</span></span>
> 
> 

![Dashboard del nuovo endpoint.][image3]

<span data-ttu-id="84e8b-147">pagina della Guida di PATCH Hello contiene PATCH URL, è necessario utilizzare hello e fornisce il codice di esempio è possibile utilizzare toocall è.</span><span class="sxs-lookup"><span data-stu-id="84e8b-147">hello PATCH help page contains hello PATCH URL you must use and provides sample code you can use toocall it.</span></span>

![URL della patch.][image5]

### <a name="check-toosee-that-you-are-updating-hello-correct-scoring-endpoint"></a><span data-ttu-id="84e8b-149">Verificare che si sta aggiornando un endpoint di assegnazione dei punteggi corretto hello toosee</span><span class="sxs-lookup"><span data-stu-id="84e8b-149">Check toosee that you are updating hello correct scoring endpoint</span></span>
* <span data-ttu-id="84e8b-150">Patch non hello servizio Web di formazione: hello patch operazione deve essere eseguita nel servizio Web di punteggio hello.</span><span class="sxs-lookup"><span data-stu-id="84e8b-150">Do not patch hello Training Web Service: hello patch operation must be performed on hello scoring Web service.</span></span>
* <span data-ttu-id="84e8b-151">Patch non endpoint predefinito hello su servizio Web: hello patch operazione deve essere eseguita su hello punteggio nuovo endpoint del servizio Web che è stato aggiunto.</span><span class="sxs-lookup"><span data-stu-id="84e8b-151">Do not patch hello default endpoint on Web service: hello patch operation must be performed on hello new scoring Web service endpoint that you added.</span></span>

<span data-ttu-id="84e8b-152">È possibile verificare quale endpoint hello del servizio Web è abilitata per hello visita portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="84e8b-152">You can verify which Web service hello endpoint is on by visiting hello Azure classic portal.</span></span> 

> [!NOTE]
> <span data-ttu-id="84e8b-153">Assicurarsi che si sta aggiungendo hello toohello di endpoint servizio Web predittivo, non hello servizio Web di Training.</span><span class="sxs-lookup"><span data-stu-id="84e8b-153">Be sure you are adding hello endpoint toohello Predictive Web Service, not hello Training Web Service.</span></span> <span data-ttu-id="84e8b-154">Se sono stati distribuiti correttamente sia un servizio Web di training che uno predittivo, verranno elencati due servizi Web separati.</span><span class="sxs-lookup"><span data-stu-id="84e8b-154">If you have correctly deployed both a Training and a Predictive Web Service, you should see two separate Web services listed.</span></span> <span data-ttu-id="84e8b-155">Servizio Web predittivo Hello deve terminare con "[predittiva exp]"..</span><span class="sxs-lookup"><span data-stu-id="84e8b-155">hello Predictive Web Service should end with "[predictive exp.]".</span></span>
> 
> 

1. <span data-ttu-id="84e8b-156">Accedi toohello [portale di Azure classico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="84e8b-156">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="84e8b-157">Scheda di Machine Learning hello aperto. ![Interfaccia utente dell'area di lavoro di Machine Learning.][image4]</span><span class="sxs-lookup"><span data-stu-id="84e8b-157">Open hello Machine Learning tab. ![Machine learning workspace UI.][image4]</span></span>
3. <span data-ttu-id="84e8b-158">Selezionare l'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="84e8b-158">Select your workspace.</span></span>
4. <span data-ttu-id="84e8b-159">Fare clic su **Servizi Web**.</span><span class="sxs-lookup"><span data-stu-id="84e8b-159">Click **Web Services**.</span></span>
5. <span data-ttu-id="84e8b-160">Selezionare il servizio Web predittivo.</span><span class="sxs-lookup"><span data-stu-id="84e8b-160">Select your Predictive Web Service.</span></span>
6. <span data-ttu-id="84e8b-161">Verificare che un servizio Web toohello è stato aggiunto il nuovo endpoint.</span><span class="sxs-lookup"><span data-stu-id="84e8b-161">Verify that your new endpoint was added toohello Web service.</span></span>

### <a name="check-hello-workspace-that-your-web-service-is-in-tooensure-it-is-in-hello-correct-region"></a><span data-ttu-id="84e8b-162">Controllare hello area di lavoro del servizio web in tooensure che è nell'area corretta hello</span><span class="sxs-lookup"><span data-stu-id="84e8b-162">Check hello workspace that your web service is in tooensure it is in hello correct region</span></span>
1. <span data-ttu-id="84e8b-163">Accedi toohello [portale di Azure classico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="84e8b-163">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="84e8b-164">Selezionare il menu di hello Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="84e8b-164">Select Machine Learning from hello menu.</span></span>
   <span data-ttu-id="84e8b-165">![Interfaccia utente dell'area di Machine Learning.][image4]</span><span class="sxs-lookup"><span data-stu-id="84e8b-165">![Machine learning region UI.][image4]</span></span>
3. <span data-ttu-id="84e8b-166">Verificare il percorso di hello dell'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="84e8b-166">Verify hello location of your workspace.</span></span>

<!-- Image Links -->

[image1]: ./media/machine-learning-troubleshooting-retraining-a-model/ml-studio-tm-connnected-to-web-service-out.png
[image2]: ./media/machine-learning-troubleshooting-retraining-a-model/addEndpoint-output.png
[image3]: ./media/machine-learning-troubleshooting-retraining-a-model/azure-portal-update-resource.png
[image4]: ./media/machine-learning-troubleshooting-retraining-a-model/azure-portal-machine-learning-tab.png
[image5]: ./media/machine-learning-troubleshooting-retraining-a-model/ml-help-page-patch-url.png
[image6]: ./media/machine-learning-troubleshooting-retraining-a-model/retraining-output.png
[image7]: ./media/machine-learning-troubleshooting-retraining-a-model/web-services-tab.png
