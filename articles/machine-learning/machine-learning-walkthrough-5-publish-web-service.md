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
# <a name="walkthrough-step-5-deploy-hello-azure-machine-learning-web-service"></a><span data-ttu-id="4ee59-103">Procedura dettagliata passaggio 5: Distribuzione di servizio web di Azure Machine Learning hello</span><span class="sxs-lookup"><span data-stu-id="4ee59-103">Walkthrough Step 5: Deploy hello Azure Machine Learning web service</span></span>
<span data-ttu-id="4ee59-104">Si tratta di hello quinto passaggio del processo di questa procedura dettagliata hello, [sviluppare una soluzione analitica predittiva in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="4ee59-104">This is hello fifth step of hello walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="4ee59-105">Creare un'area di lavoro di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="4ee59-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="4ee59-106">Caricare i dati esistenti</span><span class="sxs-lookup"><span data-stu-id="4ee59-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="4ee59-107">Creare un nuovo esperimento</span><span class="sxs-lookup"><span data-stu-id="4ee59-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="4ee59-108">Eseguire il training e valutare i modelli di hello</span><span class="sxs-lookup"><span data-stu-id="4ee59-108">Train and evaluate hello models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. <span data-ttu-id="4ee59-109">**Distribuzione di servizio web hello**</span><span class="sxs-lookup"><span data-stu-id="4ee59-109">**Deploy hello web service**</span></span>
6. [<span data-ttu-id="4ee59-110">Servizio web di accesso hello</span><span class="sxs-lookup"><span data-stu-id="4ee59-110">Access hello web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<span data-ttu-id="4ee59-111">toogive altri toouse una possibilità hello modello predittivo abbiamo sviluppato in questa procedura dettagliata, è possibile distribuirla come servizio web in Azure.</span><span class="sxs-lookup"><span data-stu-id="4ee59-111">toogive others a chance toouse hello predictive model we've developed in this walkthrough, we can deploy it as a web service on Azure.</span></span>

<span data-ttu-id="4ee59-112">Un punto toothis è abbiamo provato a training modello in esame.</span><span class="sxs-lookup"><span data-stu-id="4ee59-112">Up toothis point we've been experimenting with training our model.</span></span> <span data-ttu-id="4ee59-113">Ma servizio hello distribuito non verrà toodo training - saranno toogenerate nuove stime per l'input dell'utente hello basato sul nostro modello di punteggio.</span><span class="sxs-lookup"><span data-stu-id="4ee59-113">But hello deployed service is no longer going toodo training - it's going toogenerate new predictions by scoring hello user's input based on our model.</span></span> <span data-ttu-id="4ee59-114">Pertanto verrà toodo alcuni tooconvert preparazione questo esperimento da un ***training*** sperimentare tooa ***predittiva*** provare.</span><span class="sxs-lookup"><span data-stu-id="4ee59-114">So we're going toodo some preparation tooconvert this experiment from a ***training*** experiment tooa ***predictive*** experiment.</span></span> 

<span data-ttu-id="4ee59-115">Il processo si articola in tre passaggi:</span><span class="sxs-lookup"><span data-stu-id="4ee59-115">This is a three-step process:</span></span>  

1. <span data-ttu-id="4ee59-116">Rimuovere uno dei modelli di hello</span><span class="sxs-lookup"><span data-stu-id="4ee59-116">Remove one of hello models</span></span>
2. <span data-ttu-id="4ee59-117">Convertire hello *esperimento di training* abbiamo creato in un *esperimento predittiva*</span><span class="sxs-lookup"><span data-stu-id="4ee59-117">Convert hello *training experiment* we've created into a *predictive experiment*</span></span>
3. <span data-ttu-id="4ee59-118">Distribuire l'esperimento predittiva hello come un servizio web</span><span class="sxs-lookup"><span data-stu-id="4ee59-118">Deploy hello predictive experiment as a web service</span></span>

## <a name="remove-one-of-hello-models"></a><span data-ttu-id="4ee59-119">Rimuovere uno dei modelli di hello</span><span class="sxs-lookup"><span data-stu-id="4ee59-119">Remove one of hello models</span></span>

<span data-ttu-id="4ee59-120">Innanzitutto, è necessario tootrim questo esperimento verso il basso un po'.</span><span class="sxs-lookup"><span data-stu-id="4ee59-120">First, we need tootrim this experiment down a little.</span></span> <span data-ttu-id="4ee59-121">Si dispongono di due modelli diversi in esperimento hello, ma si desidera solo toouse un modello quando si distribuisce questo come un servizio web.</span><span class="sxs-lookup"><span data-stu-id="4ee59-121">We currently have two different models in hello experiment, but we only want toouse one model when we deploy this as a web service.</span></span>  

<span data-ttu-id="4ee59-122">Si supponga che abbiamo deciso tale modello di struttura ad albero con Boosting hello eseguita meglio di modello SVM hello.</span><span class="sxs-lookup"><span data-stu-id="4ee59-122">Let's say we've decided that hello boosted tree model performed better than hello SVM model.</span></span> <span data-ttu-id="4ee59-123">Pertanto hello prima cosa toodo hello remove [Two-Class Support Vector Machine] [ two-class-support-vector-machine] modulo e i moduli hello utilizzati per il training.</span><span class="sxs-lookup"><span data-stu-id="4ee59-123">So hello first thing toodo is remove hello [Two-Class Support Vector Machine][two-class-support-vector-machine] module and hello modules that were used for training it.</span></span> <span data-ttu-id="4ee59-124">È una copia dell'esperimento hello toomake innanzitutto facendo **Salva con nome** nella parte inferiore di hello di hello provare l'area di disegno.</span><span class="sxs-lookup"><span data-stu-id="4ee59-124">You may want toomake a copy of hello experiment first by clicking **Save As** at hello bottom of hello experiment canvas.</span></span>

<span data-ttu-id="4ee59-125">È necessario hello toodelete seguenti moduli:</span><span class="sxs-lookup"><span data-stu-id="4ee59-125">We need toodelete hello following modules:</span></span>  

* <span data-ttu-id="4ee59-126">[Two-Class Support Vector Machine][two-class-support-vector-machine]</span><span class="sxs-lookup"><span data-stu-id="4ee59-126">[Two-Class Support Vector Machine][two-class-support-vector-machine]</span></span>
* <span data-ttu-id="4ee59-127">[Eseguire il training del modello] [ train-model] e [Score Model] [ score-model] moduli che sono stati connessi tooit</span><span class="sxs-lookup"><span data-stu-id="4ee59-127">[Train Model][train-model] and [Score Model][score-model] modules that were connected tooit</span></span>
* <span data-ttu-id="4ee59-128">[Normalize Data][normalize-data] (entrambi)</span><span class="sxs-lookup"><span data-stu-id="4ee59-128">[Normalize Data][normalize-data] (both of them)</span></span>
* <span data-ttu-id="4ee59-129">[Valutazione del modello] [ evaluate-model] (perché è terminato la valutazione dei modelli di hello)</span><span class="sxs-lookup"><span data-stu-id="4ee59-129">[Evaluate Model][evaluate-model] (because we're finished evaluating hello models)</span></span>

<span data-ttu-id="4ee59-130">Selezionare ogni modulo e premere CANC hello o modulo hello pulsante destro del mouse e selezionare **eliminare**.</span><span class="sxs-lookup"><span data-stu-id="4ee59-130">Select each module and press hello Delete key, or right-click hello module and select **Delete**.</span></span> 

![Modello SVM hello rimosso][3a]

<span data-ttu-id="4ee59-132">Il modello avrà ora un aspetto analogo al seguente:</span><span class="sxs-lookup"><span data-stu-id="4ee59-132">Our model should now look something like this:</span></span>

![Modello SVM hello rimosso][3]

<span data-ttu-id="4ee59-134">Ora siamo toodeploy pronto questo modello utilizzando hello [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree].</span><span class="sxs-lookup"><span data-stu-id="4ee59-134">Now we're ready toodeploy this model using hello [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree].</span></span>

## <a name="convert-hello-training-experiment-tooa-predictive-experiment"></a><span data-ttu-id="4ee59-135">Convertire l'esperimento predittiva tooa di hello esperimento di training</span><span class="sxs-lookup"><span data-stu-id="4ee59-135">Convert hello training experiment tooa predictive experiment</span></span>

<span data-ttu-id="4ee59-136">tooget questo modello pronto per la distribuzione, è necessario tooconvert questo esperimento tooa predittiva esperimento di training.</span><span class="sxs-lookup"><span data-stu-id="4ee59-136">tooget this model ready for deployment, we need tooconvert this training experiment tooa predictive experiment.</span></span> <span data-ttu-id="4ee59-137">Questa operazione comporta tre passaggi:</span><span class="sxs-lookup"><span data-stu-id="4ee59-137">This involves three steps:</span></span>

1. <span data-ttu-id="4ee59-138">Salvare il modello di hello è stato eseguito il training e sostituire i moduli di training</span><span class="sxs-lookup"><span data-stu-id="4ee59-138">Save hello model we've trained and then replace our training modules</span></span>
2. <span data-ttu-id="4ee59-139">Tagliare i moduli di tooremove esperimento hello necessari solo per il training</span><span class="sxs-lookup"><span data-stu-id="4ee59-139">Trim hello experiment tooremove modules that were only needed for training</span></span>
3. <span data-ttu-id="4ee59-140">Definire quale hello web servizio accetta input e in cui viene generato l'output di hello</span><span class="sxs-lookup"><span data-stu-id="4ee59-140">Define where hello web service will accept input and where it generates hello output</span></span>

<span data-ttu-id="4ee59-141">Impossibile eseguire questa operazione manualmente, ma fortunatamente tutti i tre passaggi possono essere eseguiti facendo clic su **di servizio Web** nella parte inferiore di hello dell'area di disegno esperimento hello (e selezionando hello **servizio Web predittivo** opzione).</span><span class="sxs-lookup"><span data-stu-id="4ee59-141">We could do this manually, but fortunately all three steps can be accomplished by clicking **Set Up Web Service** at hello bottom of hello experiment canvas (and selecting hello **Predictive Web Service** option).</span></span>

> [!TIP]
> <span data-ttu-id="4ee59-142">Se si desidera visualizzare ulteriori dettagli su cosa accade quando si converte un esperimento di training per tooa predittiva provare, vedere [come tooprepare il modello per la distribuzione in Azure Machine Learning Studio](machine-learning-convert-training-experiment-to-scoring-experiment.md).</span><span class="sxs-lookup"><span data-stu-id="4ee59-142">If you want more details on what happens when you convert a training experiment tooa predictive experiment, see [How tooprepare your model for deployment in Azure Machine Learning Studio](machine-learning-convert-training-experiment-to-scoring-experiment.md).</span></span>

<span data-ttu-id="4ee59-143">Quando si fa clic su **Set Up Web Service**(Configura servizio Web), vengono eseguite diverse operazioni:</span><span class="sxs-lookup"><span data-stu-id="4ee59-143">When you click **Set Up Web Service**, several things happen:</span></span>

* <span data-ttu-id="4ee59-144">modello con training Hello è convertito tooa singolo **modello con training** modulo e archiviati in hello modulo tavolozza toohello a sinistra di hello provare l'area di disegno (è possibile trovare in **modelli con training**)</span><span class="sxs-lookup"><span data-stu-id="4ee59-144">hello trained model is converted tooa single **Trained Model** module and stored in hello module palette toohello left of hello experiment canvas (you can find it under **Trained Models**)</span></span>
* <span data-ttu-id="4ee59-145">Vengono rimossi i moduli usati per il training, in particolare:</span><span class="sxs-lookup"><span data-stu-id="4ee59-145">Modules that were used for training are removed; specifically:</span></span>
  * <span data-ttu-id="4ee59-146">[Two-Class Boosted Decision Tree][two-class-boosted-decision-tree]</span><span class="sxs-lookup"><span data-stu-id="4ee59-146">[Two-Class Boosted Decision Tree][two-class-boosted-decision-tree]</span></span>
  * <span data-ttu-id="4ee59-147">[Train Model][train-model]</span><span class="sxs-lookup"><span data-stu-id="4ee59-147">[Train Model][train-model]</span></span>
  * <span data-ttu-id="4ee59-148">[Split Data][split]</span><span class="sxs-lookup"><span data-stu-id="4ee59-148">[Split Data][split]</span></span>
  * <span data-ttu-id="4ee59-149">in secondo luogo Hello [Execute R Script] [ execute-r-script] modulo utilizzato per i dati di test</span><span class="sxs-lookup"><span data-stu-id="4ee59-149">hello second [Execute R Script][execute-r-script] module that was used for test data</span></span>
* <span data-ttu-id="4ee59-150">modello con training Hello salvato viene aggiunto nuovamente nella sperimentazione hello</span><span class="sxs-lookup"><span data-stu-id="4ee59-150">hello saved trained model is added back into hello experiment</span></span>
* <span data-ttu-id="4ee59-151">**Input del servizio Web** e **output del servizio Web** vengono aggiunti i moduli (questi identificano i dati dell'utente hello in cui verranno attivata la modello hello e i dati da restituire quando accede al servizio web hello)</span><span class="sxs-lookup"><span data-stu-id="4ee59-151">**Web service input** and **Web service output** modules are added (these identify where hello user's data will enter hello model, and what data is returned, when hello web service is accessed)</span></span>

> [!NOTE]
> <span data-ttu-id="4ee59-152">È possibile vedere che esperimento hello viene salvato in due parti in schede che sono stati aggiunti nella parte superiore di hello dell'area di disegno di hello esperimento.</span><span class="sxs-lookup"><span data-stu-id="4ee59-152">You can see that hello experiment is saved in two parts under tabs that have been added at hello top of hello experiment canvas.</span></span> <span data-ttu-id="4ee59-153">Hello esperimento di training originale è sotto la scheda hello **esperimento di Training**, ed è appena creato esperimento predittiva hello in **esperimento predittiva**.</span><span class="sxs-lookup"><span data-stu-id="4ee59-153">hello original training experiment is under hello tab **Training experiment**, and hello newly created predictive experiment is under **Predictive experiment**.</span></span> <span data-ttu-id="4ee59-154">sperimentazione predittiva Hello è hello uno che vengono distribuiti come un servizio web.</span><span class="sxs-lookup"><span data-stu-id="4ee59-154">hello predictive experiment is hello one we'll deploy as a web service.</span></span>

<span data-ttu-id="4ee59-155">È necessario un passaggio aggiuntivo tootake con questo particolare esperimento.</span><span class="sxs-lookup"><span data-stu-id="4ee59-155">We need tootake one additional step with this particular experiment.</span></span>
<span data-ttu-id="4ee59-156">È stato aggiunto due [Execute R Script] [ execute-r-script] tooprovide moduli un peso funzione toohello dati.</span><span class="sxs-lookup"><span data-stu-id="4ee59-156">We added two [Execute R Script][execute-r-script] modules tooprovide a weighting function toohello data.</span></span> <span data-ttu-id="4ee59-157">Che è solo uno stratagemma che è necessaria per il training e test, pertanto è possibile estrarre i moduli nel modello finale hello.</span><span class="sxs-lookup"><span data-stu-id="4ee59-157">That was just a trick we needed for training and testing, so we can take out those modules in hello final model.</span></span>
<span data-ttu-id="4ee59-158">Machine Learning Studio rimosso uno [Execute R Script] [ execute-r-script] modulo quando rimosso hello [Split] [ split] modulo.</span><span class="sxs-lookup"><span data-stu-id="4ee59-158">Machine Learning Studio removed one [Execute R Script][execute-r-script] module when it removed hello [Split][split] module.</span></span> <span data-ttu-id="4ee59-159">Ora è possibile rimuovere altri hello e connettersi [Metadata Editor] [ metadata-editor] direttamente troppo[Score Model][score-model].</span><span class="sxs-lookup"><span data-stu-id="4ee59-159">Now we can remove hello other and connect [Metadata Editor][metadata-editor] directly too[Score Model][score-model].</span></span>    

<span data-ttu-id="4ee59-160">L'esperimento dovrebbe risultare simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="4ee59-160">Our experiment should now look like this:</span></span>  

![Modello con training hello di punteggio][4]  

> [!NOTE]
> <span data-ttu-id="4ee59-162">Si potrebbe chiedere perché è stato lasciato il set di dati di carta di credito tedesco UCI di hello nell'esperimento predittiva hello.</span><span class="sxs-lookup"><span data-stu-id="4ee59-162">You may be wondering why we left hello UCI German Credit Card Data dataset in hello predictive experiment.</span></span> <span data-ttu-id="4ee59-163">servizio Hello verrà tooscore hello dati utente, non hello set di dati originale, pertanto perché lasciare hello set di dati originale nel modello hello?</span><span class="sxs-lookup"><span data-stu-id="4ee59-163">hello service is going tooscore hello user's data, not hello original dataset, so why leave hello original dataset in hello model?</span></span>
> 
> <span data-ttu-id="4ee59-164">È vero che servizio hello non necessario hello originale dei dati della carta di credito.</span><span class="sxs-lookup"><span data-stu-id="4ee59-164">It's true that hello service doesn't need hello original credit card data.</span></span> <span data-ttu-id="4ee59-165">Tuttavia, è necessario schema hello per tali dati, che include informazioni quali il numero di colonne sono disponibili e le colonne sono di tipo numeriche.</span><span class="sxs-lookup"><span data-stu-id="4ee59-165">But it does need hello schema for that data, which includes information such as how many columns there are and which columns are numeric.</span></span> <span data-ttu-id="4ee59-166">Queste informazioni sullo schema sono necessario toointerpret hello dati utente.</span><span class="sxs-lookup"><span data-stu-id="4ee59-166">This schema information is necessary toointerpret hello user's data.</span></span> <span data-ttu-id="4ee59-167">Si lascia questi componenti connessi in modo che hello punteggio modulo dispone dello schema di dataset hello quando è in esecuzione il servizio di hello.</span><span class="sxs-lookup"><span data-stu-id="4ee59-167">We leave these components connected so that hello scoring module has hello dataset schema when hello service is running.</span></span> <span data-ttu-id="4ee59-168">dati Hello non viene usati, solo schema di hello.</span><span class="sxs-lookup"><span data-stu-id="4ee59-168">hello data isn't used, just hello schema.</span></span>  
> 
> 

<span data-ttu-id="4ee59-169">Eseguire l'esperimento hello un'ultima volta (fare clic su **eseguire**.) Se si desidera tooverify che hello modello sta ancora lavorando, fare clic su output di hello di hello [Score Model] [ score-model] modulo e selezionare **Visualizza risultati**.</span><span class="sxs-lookup"><span data-stu-id="4ee59-169">Run hello experiment one last time (click **Run**.) If you want tooverify that hello model is still working, click hello output of hello [Score Model][score-model] module and select **View Results**.</span></span> <span data-ttu-id="4ee59-170">È possibile che dati originali hello sono visualizzato, valore di rischio di credito hello ("Scored Labels") e hello punteggio il valore di probabilità ("calcolato il punteggio della probabilità".)</span><span class="sxs-lookup"><span data-stu-id="4ee59-170">You can see that hello original data is displayed, along with hello credit risk value ("Scored Labels") and hello scoring probability value ("Scored Probabilities".)</span></span> 

## <a name="deploy-hello-web-service"></a><span data-ttu-id="4ee59-171">Distribuzione di servizio web hello</span><span class="sxs-lookup"><span data-stu-id="4ee59-171">Deploy hello web service</span></span>
<span data-ttu-id="4ee59-172">È possibile distribuire hello esperimento come un servizio web classica o come un nuovo servizio web che si basa su Gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="4ee59-172">You can deploy hello experiment as either a Classic web service, or as a New web service that's based on Azure Resource Manager.</span></span>

### <a name="deploy-as-a-classic-web-service"></a><span data-ttu-id="4ee59-173">Distribuire l'esperimento come servizio Web classico</span><span class="sxs-lookup"><span data-stu-id="4ee59-173">Deploy as a Classic web service</span></span>
<span data-ttu-id="4ee59-174">toodeploy un classico web servizio derivato da esperimento, fare clic su **distribuzione servizio Web** seguito hello area di disegno e selezionare **distribuzione di un servizio Web [classica]**.</span><span class="sxs-lookup"><span data-stu-id="4ee59-174">toodeploy a Classic web service derived from our experiment, click **Deploy Web Service** below hello canvas and select **Deploy Web Service [Classic]**.</span></span> <span data-ttu-id="4ee59-175">Machine Learning Studio distribuisce hello esperimento come servizio web e consente di passare toohello dashboard per il servizio web.</span><span class="sxs-lookup"><span data-stu-id="4ee59-175">Machine Learning Studio deploys hello experiment as a web service and takes you toohello dashboard for that web service.</span></span> <span data-ttu-id="4ee59-176">In questa pagina è possibile restituire esperimento toohello (**Visualizza lo snapshot** o **visualizzare più recente**) ed eseguire un test semplice del servizio web hello (vedere **Test servizio web hello** sotto).</span><span class="sxs-lookup"><span data-stu-id="4ee59-176">From this page you can return toohello experiment (**View snapshot** or **View latest**) and run a simple test of hello web service (see **Test hello web service** below).</span></span> <span data-ttu-id="4ee59-177">È anche informazioni per la creazione di applicazioni che possono accedere a un servizio web hello (ulteriori informazioni nel passaggio successivo di hello di questa procedura dettagliata).</span><span class="sxs-lookup"><span data-stu-id="4ee59-177">There is also information here for creating applications that can access hello web service (more on that in hello next step of this walkthrough).</span></span>

![Dashboard del servizio Web][6]

<span data-ttu-id="4ee59-179">È possibile configurare il servizio di hello facendo hello **configurazione** scheda. Qui è possibile modificare il nome di servizio hello (è nome esperimento hello specificato per impostazione predefinita) e assegnare una descrizione.</span><span class="sxs-lookup"><span data-stu-id="4ee59-179">You can configure hello service by clicking hello **CONFIGURATION** tab. Here you can modify hello service name (it's given hello experiment name by default) and give it a description.</span></span> <span data-ttu-id="4ee59-180">È inoltre possibile assegnare più descrittive etichette per hello dati di input e outpui.</span><span class="sxs-lookup"><span data-stu-id="4ee59-180">You can also give more friendly labels for hello input and output data.</span></span>  

![Configurare il servizio web hello][5]  

### <a name="deploy-as-a-new-web-service"></a><span data-ttu-id="4ee59-182">Distribuire l'esperimento come nuovo servizio Web</span><span class="sxs-lookup"><span data-stu-id="4ee59-182">Deploy as a New web service</span></span>

> [!NOTE] 
> <span data-ttu-id="4ee59-183">un nuovo servizio web deve disporre di autorizzazioni sufficienti in hello sottoscrizione toowhich si sta distribuendo toodeploy hello servizio web.</span><span class="sxs-lookup"><span data-stu-id="4ee59-183">toodeploy a New web service you must have sufficient permissions in hello subscription toowhich you are deploying hello web service.</span></span> <span data-ttu-id="4ee59-184">Per ulteriori informazioni, vedere [gestire un servizio web tramite il portale di servizi Web di Azure Machine Learning hello](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="4ee59-184">For more information, see [Manage a web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="4ee59-185">toodeploy un nuovo servizio web derivata da esperimento:</span><span class="sxs-lookup"><span data-stu-id="4ee59-185">toodeploy a New web service derived from our experiment:</span></span>

1. <span data-ttu-id="4ee59-186">Fare clic su **distribuzione servizio Web** seguito hello area di disegno e selezionare **distribuzione servizio Web [New]**.</span><span class="sxs-lookup"><span data-stu-id="4ee59-186">Click **Deploy Web Service** below hello canvas and select **Deploy Web Service [New]**.</span></span> <span data-ttu-id="4ee59-187">Machine Learning Studio trasferisce i servizi web Azure Machine Learning toohello **distribuire esperimento** pagina.</span><span class="sxs-lookup"><span data-stu-id="4ee59-187">Machine Learning Studio transfers you toohello Azure Machine Learning web services **Deploy Experiment** page.</span></span>

2. <span data-ttu-id="4ee59-188">Immettere un nome per il servizio web hello.</span><span class="sxs-lookup"><span data-stu-id="4ee59-188">Enter a name for hello web service.</span></span> 

3. <span data-ttu-id="4ee59-189">Per **prezzo piano**, è possibile selezionare un piano tariffario esistente o seleziona "nuovo" e concedere hello nuovo piano di un nome e l'opzione piano mensile hello selezionare.</span><span class="sxs-lookup"><span data-stu-id="4ee59-189">For **Price Plan**, you can select an existing pricing plan, or select "Create new" and give hello new plan a name and select hello monthly plan option.</span></span> <span data-ttu-id="4ee59-190">piano di Hello livelli predefinito toohello piani per l'area predefinita e il servizio web è distribuito toothat area.</span><span class="sxs-lookup"><span data-stu-id="4ee59-190">hello plan tiers default toohello plans for your default region and your web service is deployed toothat region.</span></span>

4. <span data-ttu-id="4ee59-191">Fare clic su **Distribuisci**.</span><span class="sxs-lookup"><span data-stu-id="4ee59-191">Click **Deploy**.</span></span>

<span data-ttu-id="4ee59-192">Dopo alcuni minuti, hello **delle Guide rapide** verrà visualizzata la pagina relativa al servizio web.</span><span class="sxs-lookup"><span data-stu-id="4ee59-192">After a few minutes, hello **Quickstart** page for your web service opens.</span></span>

<span data-ttu-id="4ee59-193">È possibile configurare il servizio di hello facendo hello **configura** scheda. Qui è possibile modificare il servizio hello title e assegnargli una descrizione.</span><span class="sxs-lookup"><span data-stu-id="4ee59-193">You can configure hello service by clicking hello **Configure** tab. Here you can modify hello service title and give it a description.</span></span> 

<span data-ttu-id="4ee59-194">hello tootest servizio web, fare clic su hello **Test** scheda (vedere **Test servizio web hello** sotto).</span><span class="sxs-lookup"><span data-stu-id="4ee59-194">tootest hello web service, click hello **Test** tab (see **Test hello web service** below).</span></span> <span data-ttu-id="4ee59-195">Per informazioni sulla creazione di applicazioni che possono accedere hello web servizio, fare clic su hello **consumare** scheda (passaggio successivo di hello in questa procedura dettagliata entra in modo più dettagliato).</span><span class="sxs-lookup"><span data-stu-id="4ee59-195">For information on creating applications that can access hello web service, click hello **Consume** tab (hello next step in this walkthrough will go into more detail).</span></span>

> [!TIP]
> <span data-ttu-id="4ee59-196">Dopo aver distribuito, è possibile aggiornare il servizio di web hello.</span><span class="sxs-lookup"><span data-stu-id="4ee59-196">You can update hello web service after you've deployed it.</span></span> <span data-ttu-id="4ee59-197">Ad esempio, se si desidera toochange il modello, quindi è possibile modificare esperimento di training hello, modificare i parametri di modello hello e scegliere **distribuzione servizio Web**, se si seleziona **distribuzione di un servizio Web [classica]** o  **Distribuzione di servizio Web [New]**.</span><span class="sxs-lookup"><span data-stu-id="4ee59-197">For example, if you want toochange your model, then you can edit hello training experiment, tweak hello model parameters, and click **Deploy Web Service**, selecting **Deploy Web Service [Classic]** or **Deploy Web Service [New]**.</span></span> <span data-ttu-id="4ee59-198">Quando si distribuisce nuovamente esperimento hello, sostituisce servizio web hello, ora utilizzando il modello aggiornato.</span><span class="sxs-lookup"><span data-stu-id="4ee59-198">When you deploy hello experiment again, it replaces hello web service, now using your updated model.</span></span>  
> 
> 

## <a name="test-hello-web-service"></a><span data-ttu-id="4ee59-199">Servizio web hello di test</span><span class="sxs-lookup"><span data-stu-id="4ee59-199">Test hello web service</span></span>

<span data-ttu-id="4ee59-200">Quando si accede a servizio web hello, i dati dell'utente hello passano attraverso hello **input del servizio Web** modulo in cui è passata toohello [Score Model] [ score-model] modulo e con punteggi.</span><span class="sxs-lookup"><span data-stu-id="4ee59-200">When hello web service is accessed, hello user's data enters through hello **Web service input** module where it's passed toohello [Score Model][score-model] module and scored.</span></span> <span data-ttu-id="4ee59-201">modo Hello che è stato configurato l'esperimento predittiva hello, modello hello prevede che i dati in hello stesso formato delle hello credito rischio set di dati originale.</span><span class="sxs-lookup"><span data-stu-id="4ee59-201">hello way we've set up hello predictive experiment, hello model expects data in hello same format as hello original credit risk dataset.</span></span>
<span data-ttu-id="4ee59-202">Hello vengono restituiti toohello utente dal servizio web hello tramite hello **output del servizio Web** modulo.</span><span class="sxs-lookup"><span data-stu-id="4ee59-202">hello results are returned toohello user from hello web service through hello **Web service output** module.</span></span>

> [!TIP]
> <span data-ttu-id="4ee59-203">modo Hello abbiamo hello predittiva esperimento configurato, hello intera risultante dalla hello [Score Model] [ score-model] modulo vengono restituiti.</span><span class="sxs-lookup"><span data-stu-id="4ee59-203">hello way we have hello predictive experiment configured, hello entire results from hello [Score Model][score-model] module are returned.</span></span> <span data-ttu-id="4ee59-204">Sono inclusi tutti i dati di input hello più valore di rischio di credito hello e hello assegnazione dei punteggi di probabilità.</span><span class="sxs-lookup"><span data-stu-id="4ee59-204">This includes all hello input data plus hello credit risk value and hello scoring probability.</span></span> <span data-ttu-id="4ee59-205">Ma è possibile restituire un elemento diverso se si desidera, ad esempio, è possibile restituire solo valore di rischio per la carta di credito hello.</span><span class="sxs-lookup"><span data-stu-id="4ee59-205">But you can return something different if you want - for example, you could return just hello credit risk value.</span></span> <span data-ttu-id="4ee59-206">toodo, questa operazione di inserimento un [Project Columns] [ project-columns] modulo tra [Score Model] [ score-model] hello e **outputdelservizioWeb** tooeliminate colonne non desiderate hello tooreturn servizio web.</span><span class="sxs-lookup"><span data-stu-id="4ee59-206">toodo this, insert a [Project Columns][project-columns] module between [Score Model][score-model] and hello **Web service output** tooeliminate columns you don't want hello web service tooreturn.</span></span> 
> 
> 

<span data-ttu-id="4ee59-207">È possibile testare un sito web classica service in **Machine Learning Studio** o hello **servizi Web di Azure Machine Learning** portale.</span><span class="sxs-lookup"><span data-stu-id="4ee59-207">You can test a Classic web service either in **Machine Learning Studio** or in hello **Azure Machine Learning Web Services** portal.</span></span>
<span data-ttu-id="4ee59-208">È possibile testare solo un nuovo servizio web hello **servizi Web di Machine Learning** portale.</span><span class="sxs-lookup"><span data-stu-id="4ee59-208">You can test a New web service only in hello **Machine Learning Web Services** portal.</span></span>

> [!TIP]
> <span data-ttu-id="4ee59-209">Durante il test nel portale di servizi Web di Azure Machine Learning hello, è possibile impostare il portale di hello creare dati di esempio che è possibile utilizzare il servizio di richiesta-risposta hello tootest.</span><span class="sxs-lookup"><span data-stu-id="4ee59-209">When testing in hello Azure Machine Learning Web Services portal, you can have hello portal create sample data that you can use tootest hello Request-Response service.</span></span> <span data-ttu-id="4ee59-210">In hello **configura** pagina, selezionare "Sì" per **dati di esempio abilitata?**.</span><span class="sxs-lookup"><span data-stu-id="4ee59-210">On hello **Configure** page, select "Yes" for **Sample Data Enabled?**.</span></span> <span data-ttu-id="4ee59-211">Quando si apre la scheda di richiesta-risposta hello hello **Test** pagina portale hello compila i dati di esempio tratti da hello credito rischio set di dati originale.</span><span class="sxs-lookup"><span data-stu-id="4ee59-211">When you open hello Request-Response tab on hello **Test** page, hello portal fills in sample data taken from hello original credit risk dataset.</span></span>

### <a name="test-a-classic-web-service"></a><span data-ttu-id="4ee59-212">Testare un servizio Web classico</span><span class="sxs-lookup"><span data-stu-id="4ee59-212">Test a Classic web service</span></span>

<span data-ttu-id="4ee59-213">È possibile testare un servizio web classica in Machine Learning Studio o nel portale di servizi Web di Machine Learning hello.</span><span class="sxs-lookup"><span data-stu-id="4ee59-213">You can test a Classic web service in Machine Learning Studio or in hello Machine Learning Web Services portal.</span></span> 

#### <a name="test-in-machine-learning-studio"></a><span data-ttu-id="4ee59-214">Testare in Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="4ee59-214">Test in Machine Learning Studio</span></span>

1. <span data-ttu-id="4ee59-215">In hello **DASHBOARD** pagina per il servizio web hello, fare clic su hello **Test** pulsante sotto **Endpoint predefinito**.</span><span class="sxs-lookup"><span data-stu-id="4ee59-215">On hello **DASHBOARD** page for hello web service, click hello **Test** button under **Default Endpoint**.</span></span> <span data-ttu-id="4ee59-216">Una finestra di dialogo viene visualizzata e viene chiesto di dati di input per il servizio hello hello.</span><span class="sxs-lookup"><span data-stu-id="4ee59-216">A dialog pops up and asks you for hello input data for hello service.</span></span> <span data-ttu-id="4ee59-217">Questi è hello stesse colonne visualizzate in hello credito rischio set di dati originale.</span><span class="sxs-lookup"><span data-stu-id="4ee59-217">These are hello same columns that appeared in hello original credit risk dataset.</span></span>  

2. <span data-ttu-id="4ee59-218">Immettere un set di dati e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="4ee59-218">Enter a set of data and then click **OK**.</span></span> 

#### <a name="test-in-hello-machine-learning-web-services-portal"></a><span data-ttu-id="4ee59-219">Test nel portale di servizi Web di Machine Learning hello</span><span class="sxs-lookup"><span data-stu-id="4ee59-219">Test in hello Machine Learning Web Services portal</span></span>

1. <span data-ttu-id="4ee59-220">In hello **DASHBOARD** pagina per il servizio web hello, fare clic su hello **anteprima Test** collegamento in **Endpoint predefinito**.</span><span class="sxs-lookup"><span data-stu-id="4ee59-220">On hello **DASHBOARD** page for hello web service, click hello **Test preview** link under **Default Endpoint**.</span></span> <span data-ttu-id="4ee59-221">pagina di prova Hello nel portale di servizi Web di Azure Machine Learning hello hello endpoint del servizio web viene visualizzata e viene chiesto di dati di input per il servizio hello hello.</span><span class="sxs-lookup"><span data-stu-id="4ee59-221">hello test page in hello Azure Machine Learning Web Services portal for hello web service endpoint opens and asks you for hello input data for hello service.</span></span> <span data-ttu-id="4ee59-222">Questi è hello stesse colonne visualizzate in hello credito rischio set di dati originale.</span><span class="sxs-lookup"><span data-stu-id="4ee59-222">These are hello same columns that appeared in hello original credit risk dataset.</span></span>

2. <span data-ttu-id="4ee59-223">Fare clic su **Test Request-Response** (Test Richiesta-risposta).</span><span class="sxs-lookup"><span data-stu-id="4ee59-223">Click **Test Request-Response**.</span></span> 

### <a name="test-a-new-web-service"></a><span data-ttu-id="4ee59-224">Testare un nuovo servizio Web</span><span class="sxs-lookup"><span data-stu-id="4ee59-224">Test a New web service</span></span>

<span data-ttu-id="4ee59-225">È possibile testare un nuovo servizio web solo nel portale di servizi Web di Machine Learning hello.</span><span class="sxs-lookup"><span data-stu-id="4ee59-225">You can test a New web service only in hello Machine Learning Web Services portal.</span></span>

1. <span data-ttu-id="4ee59-226">In hello [servizi Web di Azure Machine Learning](https://services.azureml.net/quickstart) portale, fare clic su **Test** nella parte superiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="4ee59-226">In hello [Azure Machine Learning Web Services](https://services.azureml.net/quickstart) portal, click **Test** at hello top of hello page.</span></span> <span data-ttu-id="4ee59-227">Hello **Test** verrà visualizzata la pagina e che è possibile inserire i dati per il servizio di hello.</span><span class="sxs-lookup"><span data-stu-id="4ee59-227">hello **Test** page opens and you can input data for hello service.</span></span> <span data-ttu-id="4ee59-228">i campi di input Hello visualizzati corrispondono toohello colonne visualizzate in hello credito rischio set di dati originale.</span><span class="sxs-lookup"><span data-stu-id="4ee59-228">hello input fields displayed correspond toohello columns that appeared in hello original credit risk dataset.</span></span> 

2. <span data-ttu-id="4ee59-229">Immettere un set di dati e quindi fare clic su **Test Request-Response**(Test Richiesta-risposta).</span><span class="sxs-lookup"><span data-stu-id="4ee59-229">Enter a set of data and then click **Test Request-Response**.</span></span>

<span data-ttu-id="4ee59-230">risultati del test di hello Hello vengono visualizzati sul lato destro di hello della pagina hello nella colonna di output di hello.</span><span class="sxs-lookup"><span data-stu-id="4ee59-230">hello results of hello test are displayed on hello right-hand side of hello page in hello output column.</span></span> 


## <a name="manage-hello-web-service"></a><span data-ttu-id="4ee59-231">Gestire il servizio web hello</span><span class="sxs-lookup"><span data-stu-id="4ee59-231">Manage hello web service</span></span>

### <a name="manage-a-classic-web-service-in-hello-azure-classic-portal"></a><span data-ttu-id="4ee59-232">Gestire un servizio web classica nel portale di Azure classico hello</span><span class="sxs-lookup"><span data-stu-id="4ee59-232">Manage a Classic web service in hello Azure classic portal</span></span>

<span data-ttu-id="4ee59-233">Dopo aver distribuito il servizio web classica, è possibile gestire dal hello [portale di Azure classico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="4ee59-233">Once you've deployed your Classic web service, you can manage it from hello [Azure classic portal](https://manage.windowsazure.com).</span></span>

1. <span data-ttu-id="4ee59-234">Accedi toohello [portale di Azure classico](https://manage.windowsazure.com)</span><span class="sxs-lookup"><span data-stu-id="4ee59-234">Sign in toohello [Azure classic portal](https://manage.windowsazure.com)</span></span>
2. <span data-ttu-id="4ee59-235">Nel Pannello di servizi di Microsoft Azure hello, fare clic su **MACHINE LEARNING**</span><span class="sxs-lookup"><span data-stu-id="4ee59-235">In hello Microsoft Azure services panel, click **MACHINE LEARNING**</span></span>
3. <span data-ttu-id="4ee59-236">Fare clic sull'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="4ee59-236">Click your workspace</span></span>
4. <span data-ttu-id="4ee59-237">Fare clic su hello **servizi Web** scheda</span><span class="sxs-lookup"><span data-stu-id="4ee59-237">Click hello **Web services** tab</span></span>
5. <span data-ttu-id="4ee59-238">Fare clic su servizio web hello che è stato creato</span><span class="sxs-lookup"><span data-stu-id="4ee59-238">Click hello web service we created</span></span>
6. <span data-ttu-id="4ee59-239">Fare clic sull'endpoint "predefinita" hello</span><span class="sxs-lookup"><span data-stu-id="4ee59-239">Click hello "default" endpoint</span></span>

<span data-ttu-id="4ee59-240">Da qui, è possibile eseguire operazioni quali il monitoraggio esegue il servizio web hello e apportare modifiche delle prestazioni modificando il numero di chiamate simultanee hello servizio può gestire.</span><span class="sxs-lookup"><span data-stu-id="4ee59-240">From here, you can do things like monitor how hello web service is doing and make performance tweaks by changing how many concurrent calls hello service can handle.</span></span>

<span data-ttu-id="4ee59-241">Per informazioni dettagliate, vedere:</span><span class="sxs-lookup"><span data-stu-id="4ee59-241">For more details, see:</span></span>

* [<span data-ttu-id="4ee59-242">Creazione di endpoint</span><span class="sxs-lookup"><span data-stu-id="4ee59-242">Creating Endpoints</span></span>](machine-learning-create-endpoint.md)
* [<span data-ttu-id="4ee59-243">Ridimensionamento di un servizio Web</span><span class="sxs-lookup"><span data-stu-id="4ee59-243">Scaling web service</span></span>](machine-learning-scaling-webservice.md)

### <a name="manage-a-classic-or-new-web-service-in-hello-azure-machine-learning-web-services-portal"></a><span data-ttu-id="4ee59-244">Gestire un classica o un nuovo servizio web nel portale di servizi Web di Azure Machine Learning hello</span><span class="sxs-lookup"><span data-stu-id="4ee59-244">Manage a Classic or New web service in hello Azure Machine Learning Web Services portal</span></span>

<span data-ttu-id="4ee59-245">Dopo aver distribuito il servizio web, se classico o nuova, è possibile gestire dal hello [servizi Web di Microsoft Azure Machine Learning](https://services.azureml.net/quickstart) portale.</span><span class="sxs-lookup"><span data-stu-id="4ee59-245">Once you've deployed your web service, whether Classic or New, you can manage it from hello [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/quickstart) portal.</span></span>

<span data-ttu-id="4ee59-246">prestazioni di hello toomonitor del servizio web:</span><span class="sxs-lookup"><span data-stu-id="4ee59-246">toomonitor hello performance of your web service:</span></span>

1. <span data-ttu-id="4ee59-247">Accedi toohello [servizi Web di Microsoft Azure Machine Learning](https://services.azureml.net/quickstart) portale</span><span class="sxs-lookup"><span data-stu-id="4ee59-247">Sign in toohello [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/quickstart) portal</span></span>
2. <span data-ttu-id="4ee59-248">Fare clic su **Servizi Web**</span><span class="sxs-lookup"><span data-stu-id="4ee59-248">Click **Web services**</span></span>
3. <span data-ttu-id="4ee59-249">Fare clic sul servizio Web</span><span class="sxs-lookup"><span data-stu-id="4ee59-249">Click your web service</span></span>
4. <span data-ttu-id="4ee59-250">Fare clic su hello **Dashboard**</span><span class="sxs-lookup"><span data-stu-id="4ee59-250">Click hello **Dashboard**</span></span>

- - -
<span data-ttu-id="4ee59-251">**Passaggio successivo: [accedere al servizio web hello](machine-learning-walkthrough-6-access-web-service.md)**</span><span class="sxs-lookup"><span data-stu-id="4ee59-251">**Next: [Access hello web service](machine-learning-walkthrough-6-access-web-service.md)**</span></span>

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
