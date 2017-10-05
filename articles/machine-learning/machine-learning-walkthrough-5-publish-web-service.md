---
title: 'Passaggio 5: Distribuire il servizio Web di Machine Learning | Microsoft Docs'
description: 'Passaggio 5 della procedura dettagliata Sviluppare una soluzione predittiva: Distribuire un esperimento predittivo in Machine Learning Studio come servizio Web.'
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
ms.openlocfilehash: cec1bcceea158a20742c7019a266dcefaac4c9cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="walkthrough-step-5-deploy-the-azure-machine-learning-web-service"></a><span data-ttu-id="32305-103">Passaggio 5 della procedura dettagliata: Distribuzione del servizio Web di Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="32305-103">Walkthrough Step 5: Deploy the Azure Machine Learning web service</span></span>
<span data-ttu-id="32305-104">Questo è il quinto passaggio della procedura dettagliata [Sviluppare una soluzione predittiva in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="32305-104">This is the fifth step of the walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="32305-105">Creare un'area di lavoro di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="32305-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="32305-106">Caricare i dati esistenti</span><span class="sxs-lookup"><span data-stu-id="32305-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="32305-107">Creare un nuovo esperimento</span><span class="sxs-lookup"><span data-stu-id="32305-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="32305-108">Eseguire il training e valutare i modelli</span><span class="sxs-lookup"><span data-stu-id="32305-108">Train and evaluate the models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. <span data-ttu-id="32305-109">**Distribuire il servizio web**</span><span class="sxs-lookup"><span data-stu-id="32305-109">**Deploy the web service**</span></span>
6. [<span data-ttu-id="32305-110">Accedere al servizio Web</span><span class="sxs-lookup"><span data-stu-id="32305-110">Access the web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<span data-ttu-id="32305-111">Per permettere ad altri utenti di usare il modello predittivo sviluppato in questa procedura dettagliata, il modello può ora essere distribuito come servizio Web in Azure.</span><span class="sxs-lookup"><span data-stu-id="32305-111">To give others a chance to use the predictive model we've developed in this walkthrough, we can deploy it as a web service on Azure.</span></span>

<span data-ttu-id="32305-112">Fino a questo punto è stato sperimentato il training da parte del modello,</span><span class="sxs-lookup"><span data-stu-id="32305-112">Up to this point we've been experimenting with training our model.</span></span> <span data-ttu-id="32305-113">ma il servizio distribuito non dovrà più eseguire il training, perché genererà le stime assegnando un punteggio all'input dell'utente in base al modello.</span><span class="sxs-lookup"><span data-stu-id="32305-113">But the deployed service is no longer going to do training - it's going to generate new predictions by scoring the user's input based on our model.</span></span> <span data-ttu-id="32305-114">Di conseguenza, è necessario eseguire alcuni preparativi per convertire questo esperimento da esperimento di ***training*** a esperimento ***predittivo***.</span><span class="sxs-lookup"><span data-stu-id="32305-114">So we're going to do some preparation to convert this experiment from a ***training*** experiment to a ***predictive*** experiment.</span></span> 

<span data-ttu-id="32305-115">Il processo si articola in tre passaggi:</span><span class="sxs-lookup"><span data-stu-id="32305-115">This is a three-step process:</span></span>  

1. <span data-ttu-id="32305-116">Rimuovere uno dei modelli</span><span class="sxs-lookup"><span data-stu-id="32305-116">Remove one of the models</span></span>
2. <span data-ttu-id="32305-117">Convertire l'*esperimento di training* creato in *esperimento predittivo*</span><span class="sxs-lookup"><span data-stu-id="32305-117">Convert the *training experiment* we've created into a *predictive experiment*</span></span>
3. <span data-ttu-id="32305-118">Distribuire l'esperimento predittivo come servizio Web</span><span class="sxs-lookup"><span data-stu-id="32305-118">Deploy the predictive experiment as a web service</span></span>

## <a name="remove-one-of-the-models"></a><span data-ttu-id="32305-119">Rimuovere uno dei modelli</span><span class="sxs-lookup"><span data-stu-id="32305-119">Remove one of the models</span></span>

<span data-ttu-id="32305-120">Prima è necessario ridurre un po' questo esperimento.</span><span class="sxs-lookup"><span data-stu-id="32305-120">First, we need to trim this experiment down a little.</span></span> <span data-ttu-id="32305-121">Nell'esperimento sono attualmente presenti due modelli diversi, ma si desidera usare un solo modello da distribuire come servizio Web.</span><span class="sxs-lookup"><span data-stu-id="32305-121">We currently have two different models in the experiment, but we only want to use one model when we deploy this as a web service.</span></span>  

<span data-ttu-id="32305-122">Si supponga che il modello di albero con boosting sia il modello eseguito meglio con il modello SVM.</span><span class="sxs-lookup"><span data-stu-id="32305-122">Let's say we've decided that the boosted tree model performed better than the SVM model.</span></span> <span data-ttu-id="32305-123">La prima cosa da fare, quindi, è rimuovere il modulo [Two-Class Support Vector Machine][two-class-support-vector-machine] e i moduli usati per eseguirne il training.</span><span class="sxs-lookup"><span data-stu-id="32305-123">So the first thing to do is remove the [Two-Class Support Vector Machine][two-class-support-vector-machine] module and the modules that were used for training it.</span></span> <span data-ttu-id="32305-124">È possibile creare prima una copia dell'esperimento facendo clic su **Save As** nella parte inferiore dell'area di disegno dell'esperimento.</span><span class="sxs-lookup"><span data-stu-id="32305-124">You may want to make a copy of the experiment first by clicking **Save As** at the bottom of the experiment canvas.</span></span>

<span data-ttu-id="32305-125">È necessario eliminare i seguenti moduli:</span><span class="sxs-lookup"><span data-stu-id="32305-125">We need to delete the following modules:</span></span>  

* <span data-ttu-id="32305-126">[Two-Class Support Vector Machine][two-class-support-vector-machine]</span><span class="sxs-lookup"><span data-stu-id="32305-126">[Two-Class Support Vector Machine][two-class-support-vector-machine]</span></span>
* <span data-ttu-id="32305-127">I moduli [Train Model][train-model] e [Score Model][score-model] che sono stati connessi</span><span class="sxs-lookup"><span data-stu-id="32305-127">[Train Model][train-model] and [Score Model][score-model] modules that were connected to it</span></span>
* <span data-ttu-id="32305-128">[Normalize Data][normalize-data] (entrambi)</span><span class="sxs-lookup"><span data-stu-id="32305-128">[Normalize Data][normalize-data] (both of them)</span></span>
* <span data-ttu-id="32305-129">[Evaluate Model][evaluate-model] (poiché è terminata la valutazione dei modelli)</span><span class="sxs-lookup"><span data-stu-id="32305-129">[Evaluate Model][evaluate-model] (because we're finished evaluating the models)</span></span>

<span data-ttu-id="32305-130">Selezionare ogni modulo e premere CANC oppure fare clic con il pulsante destro del mouse sul modulo e scegliere **Delete** (Elimina).</span><span class="sxs-lookup"><span data-stu-id="32305-130">Select each module and press the Delete key, or right-click the module and select **Delete**.</span></span> 

![Rimuovere il modello SVM][3a]

<span data-ttu-id="32305-132">Il modello avrà ora un aspetto analogo al seguente:</span><span class="sxs-lookup"><span data-stu-id="32305-132">Our model should now look something like this:</span></span>

![Rimuovere il modello SVM][3]

<span data-ttu-id="32305-134">Ora il modello è pronto per essere distribuito tramite il modulo [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree].</span><span class="sxs-lookup"><span data-stu-id="32305-134">Now we're ready to deploy this model using the [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree].</span></span>

## <a name="convert-the-training-experiment-to-a-predictive-experiment"></a><span data-ttu-id="32305-135">Convertire l'esperimento di training in un esperimento predittivo</span><span class="sxs-lookup"><span data-stu-id="32305-135">Convert the training experiment to a predictive experiment</span></span>

<span data-ttu-id="32305-136">Per preparare questo modello per la distribuzione, è necessario convertire l'esperimento di training in un esperimento predittivo.</span><span class="sxs-lookup"><span data-stu-id="32305-136">To get this model ready for deployment, we need to convert this training experiment to a predictive experiment.</span></span> <span data-ttu-id="32305-137">Questa operazione comporta tre passaggi:</span><span class="sxs-lookup"><span data-stu-id="32305-137">This involves three steps:</span></span>

1. <span data-ttu-id="32305-138">Salvare il modello di cui è stato eseguito il training e usarlo per sostituire i moduli di training</span><span class="sxs-lookup"><span data-stu-id="32305-138">Save the model we've trained and then replace our training modules</span></span>
2. <span data-ttu-id="32305-139">Ridurre l'esperimento per rimuovere i moduli che sono serviti solo per il training</span><span class="sxs-lookup"><span data-stu-id="32305-139">Trim the experiment to remove modules that were only needed for training</span></span>
3. <span data-ttu-id="32305-140">Definire il punto in cui il servizio Web accetterà l'input e in cui genererà l'output</span><span class="sxs-lookup"><span data-stu-id="32305-140">Define where the web service will accept input and where it generates the output</span></span>

<span data-ttu-id="32305-141">È possibile eseguire questa procedura manualmente, ma i tre passaggi possono essere effettuati facendo clic su **Configura servizio Web** nella parte inferiore dell'area di disegno dell'esperimento e selezionare l'opzione **Predictive Web Service** (Servizio Web predittivo) per eseguire tutti e tre i passaggi.</span><span class="sxs-lookup"><span data-stu-id="32305-141">We could do this manually, but fortunately all three steps can be accomplished by clicking **Set Up Web Service** at the bottom of the experiment canvas (and selecting the **Predictive Web Service** option).</span></span>

> [!TIP]
> <span data-ttu-id="32305-142">Per informazioni dettagliate cosa accade quando si converte un esperimento di training in un esperimento predittivo, vedere l'articolo relativo alla [preparazione del modello per la distribuzione in Azure Machine Learning Studio](machine-learning-convert-training-experiment-to-scoring-experiment.md).</span><span class="sxs-lookup"><span data-stu-id="32305-142">If you want more details on what happens when you convert a training experiment to a predictive experiment, see [How to prepare your model for deployment in Azure Machine Learning Studio](machine-learning-convert-training-experiment-to-scoring-experiment.md).</span></span>

<span data-ttu-id="32305-143">Quando si fa clic su **Set Up Web Service**(Configura servizio Web), vengono eseguite diverse operazioni:</span><span class="sxs-lookup"><span data-stu-id="32305-143">When you click **Set Up Web Service**, several things happen:</span></span>

* <span data-ttu-id="32305-144">Il modello di cui è stato eseguito il training viene convertito in un singolo modulo **Trained Model** e archiviato nella tavolozza dei moduli a sinistra dell'area di disegno dell'esperimento e sarà disponibile in **Trained Models**.</span><span class="sxs-lookup"><span data-stu-id="32305-144">The trained model is converted to a single **Trained Model** module and stored in the module palette to the left of the experiment canvas (you can find it under **Trained Models**)</span></span>
* <span data-ttu-id="32305-145">Vengono rimossi i moduli usati per il training, in particolare:</span><span class="sxs-lookup"><span data-stu-id="32305-145">Modules that were used for training are removed; specifically:</span></span>
  * <span data-ttu-id="32305-146">[Two-Class Boosted Decision Tree][two-class-boosted-decision-tree]</span><span class="sxs-lookup"><span data-stu-id="32305-146">[Two-Class Boosted Decision Tree][two-class-boosted-decision-tree]</span></span>
  * <span data-ttu-id="32305-147">[Train Model][train-model]</span><span class="sxs-lookup"><span data-stu-id="32305-147">[Train Model][train-model]</span></span>
  * <span data-ttu-id="32305-148">[Split Data][split]</span><span class="sxs-lookup"><span data-stu-id="32305-148">[Split Data][split]</span></span>
  * <span data-ttu-id="32305-149">Il secondo modulo [Execute R Script][execute-r-script] usato per i dati di test</span><span class="sxs-lookup"><span data-stu-id="32305-149">the second [Execute R Script][execute-r-script] module that was used for test data</span></span>
* <span data-ttu-id="32305-150">Il modello con training salvato viene aggiunto nuovamente all'esperimento</span><span class="sxs-lookup"><span data-stu-id="32305-150">The saved trained model is added back into the experiment</span></span>
* <span data-ttu-id="32305-151">Vengono aggiunti i moduli **Web service input** (Input servizio Web) e **Output servizio Web**; queste informazioni identificano dove verranno immessi i dati dell'utente nel modello e i dati che verranno restituiti quando si accede al servizio Web</span><span class="sxs-lookup"><span data-stu-id="32305-151">**Web service input** and **Web service output** modules are added (these identify where the user's data will enter the model, and what data is returned, when the web service is accessed)</span></span>

> [!NOTE]
> <span data-ttu-id="32305-152">Si può notare che l'esperimento viene salvato in due parti sotto le schede che sono state aggiunte all'inizio dell'area di disegno dell'esperimento.</span><span class="sxs-lookup"><span data-stu-id="32305-152">You can see that the experiment is saved in two parts under tabs that have been added at the top of the experiment canvas.</span></span> <span data-ttu-id="32305-153">L'esperimento di training originale si trova sotto la scheda **Esperimento di training** e l'esperimento predittivo appena creato si trova sotto **Esperimento predittivo**.</span><span class="sxs-lookup"><span data-stu-id="32305-153">The original training experiment is under the tab **Training experiment**, and the newly created predictive experiment is under **Predictive experiment**.</span></span> <span data-ttu-id="32305-154">L'esperimento predittivo è quello che verrà distribuito come servizio Web.</span><span class="sxs-lookup"><span data-stu-id="32305-154">The predictive experiment is the one we'll deploy as a web service.</span></span>

<span data-ttu-id="32305-155">Con questo particolare esperimento è necessario effettuare un'operazione aggiuntiva.</span><span class="sxs-lookup"><span data-stu-id="32305-155">We need to take one additional step with this particular experiment.</span></span>
<span data-ttu-id="32305-156">Sono stati aggiungi due moduli [Execute R Script][execute-r-script] per fornire una funzione di ponderazione per i dati.</span><span class="sxs-lookup"><span data-stu-id="32305-156">We added two [Execute R Script][execute-r-script] modules to provide a weighting function to the data.</span></span> <span data-ttu-id="32305-157">Si tratta semplicemente di un espediente necessario per il training e il test ed è quindi possibile estrarre i moduli nel modello finale.</span><span class="sxs-lookup"><span data-stu-id="32305-157">That was just a trick we needed for training and testing, so we can take out those modules in the final model.</span></span>
<span data-ttu-id="32305-158">Machine Learning Studio ha rimosso un modulo [Execute R Script][execute-r-script] durante la rimozione del modulo [Split Data][split].</span><span class="sxs-lookup"><span data-stu-id="32305-158">Machine Learning Studio removed one [Execute R Script][execute-r-script] module when it removed the [Split][split] module.</span></span> <span data-ttu-id="32305-159">È possibile rimuovere l'altro modulo e connettere [Metadata Editor][metadata-editor] direttamente a [Score Model][score-model].</span><span class="sxs-lookup"><span data-stu-id="32305-159">Now we can remove the other and connect [Metadata Editor][metadata-editor] directly to [Score Model][score-model].</span></span>    

<span data-ttu-id="32305-160">L'esperimento dovrebbe risultare simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="32305-160">Our experiment should now look like this:</span></span>  

![Valutazione del modello sottoposto a training][4]  

> [!NOTE]
> <span data-ttu-id="32305-162">Ci si chiederà perché il set di dati relativo alle carte di credito tedesche UCI sia stato lasciato nell'esperimento predittivo.</span><span class="sxs-lookup"><span data-stu-id="32305-162">You may be wondering why we left the UCI German Credit Card Data dataset in the predictive experiment.</span></span> <span data-ttu-id="32305-163">Il servizio assegnerà un punteggio ai dati dell'utente, non al set di dati originale, quindi perché lasciare il set di dati originale nel modello?</span><span class="sxs-lookup"><span data-stu-id="32305-163">The service is going to score the user's data, not the original dataset, so why leave the original dataset in the model?</span></span>
> 
> <span data-ttu-id="32305-164">Il servizio non necessita dei dati della carta di credito originali.</span><span class="sxs-lookup"><span data-stu-id="32305-164">It's true that the service doesn't need the original credit card data.</span></span> <span data-ttu-id="32305-165">Necessita però dello schema per tali dati, incluse informazioni come il numero di colonne presenti e quali colone sono numeriche.</span><span class="sxs-lookup"><span data-stu-id="32305-165">But it does need the schema for that data, which includes information such as how many columns there are and which columns are numeric.</span></span> <span data-ttu-id="32305-166">Queste informazioni sullo schema sono necessarie per interpretare i dati dell'utente.</span><span class="sxs-lookup"><span data-stu-id="32305-166">This schema information is necessary to interpret the user's data.</span></span> <span data-ttu-id="32305-167">È necessario lasciare questi componenti connessi in modo che il modulo di punteggio abbia lo schema del set di dati quando il servizio è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="32305-167">We leave these components connected so that the scoring module has the dataset schema when the service is running.</span></span> <span data-ttu-id="32305-168">I dati non vengono usati, solo lo schema.</span><span class="sxs-lookup"><span data-stu-id="32305-168">The data isn't used, just the schema.</span></span>  
> 
> 

<span data-ttu-id="32305-169">Eseguire l'esperimento un'ultima volta, facendo clic su **Run** (Esegui). Se si vuole verificare che il modello funzioni ancora, fare clic sull'output del modulo [Score Model][score-model] e selezionare **Visualizza risultati**.</span><span class="sxs-lookup"><span data-stu-id="32305-169">Run the experiment one last time (click **Run**.) If you want to verify that the model is still working, click the output of the [Score Model][score-model] module and select **View Results**.</span></span> <span data-ttu-id="32305-170">Verranno visualizzati i dati originali, insieme al valore di rischio di credito "Scored Labels" (Etichette punteggio) e al valore di probabilità del punteggio "Scored Probabilities" (Probabilità punteggio).</span><span class="sxs-lookup"><span data-stu-id="32305-170">You can see that the original data is displayed, along with the credit risk value ("Scored Labels") and the scoring probability value ("Scored Probabilities".)</span></span> 

## <a name="deploy-the-web-service"></a><span data-ttu-id="32305-171">Distribuire il servizio web</span><span class="sxs-lookup"><span data-stu-id="32305-171">Deploy the web service</span></span>
<span data-ttu-id="32305-172">È possibile distribuire l'esperimento come servizio Web classico o come nuovo servizio Web basato su Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="32305-172">You can deploy the experiment as either a Classic web service, or as a New web service that's based on Azure Resource Manager.</span></span>

### <a name="deploy-as-a-classic-web-service"></a><span data-ttu-id="32305-173">Distribuire l'esperimento come servizio Web classico</span><span class="sxs-lookup"><span data-stu-id="32305-173">Deploy as a Classic web service</span></span>
<span data-ttu-id="32305-174">Per distribuire un servizio Web classico derivato dall'esperimento, fare clic su **Distribuisci servizio Web** sotto l'area di disegno e selezionare **Distribuisci servizio Web - Nuovo**.</span><span class="sxs-lookup"><span data-stu-id="32305-174">To deploy a Classic web service derived from our experiment, click **Deploy Web Service** below the canvas and select **Deploy Web Service [Classic]**.</span></span> <span data-ttu-id="32305-175">Machine Learning Studio distribuisce l'esperimento come servizio Web e apre il dashboard del servizio.</span><span class="sxs-lookup"><span data-stu-id="32305-175">Machine Learning Studio deploys the experiment as a web service and takes you to the dashboard for that web service.</span></span> <span data-ttu-id="32305-176">Da qui è possibile tornare all'esperimento (**View snapshot** (Visualizza snapshot) o **View latest** (Visualizza più recente)) ed eseguire un semplice test del servizio Web. Vedere **Testare il servizio Web** di seguito.</span><span class="sxs-lookup"><span data-stu-id="32305-176">From this page you can return to the experiment (**View snapshot** or **View latest**) and run a simple test of the web service (see **Test the web service** below).</span></span> <span data-ttu-id="32305-177">Qui sono inoltre disponibili informazioni per la creazione di applicazioni in grado di accedere al servizio Web (altre informazioni nella sezione successiva di questa procedura dettagliata).</span><span class="sxs-lookup"><span data-stu-id="32305-177">There is also information here for creating applications that can access the web service (more on that in the next step of this walkthrough).</span></span>

![Dashboard del servizio Web][6]

<span data-ttu-id="32305-179">È possibile configurare il servizio facendo clic sulla scheda **CONFIGURATION** (CONFIGURAZIONE),</span><span class="sxs-lookup"><span data-stu-id="32305-179">You can configure the service by clicking the **CONFIGURATION** tab.</span></span> <span data-ttu-id="32305-180">dove è possibile modificare il nome del servizio (per impostazione predefinita ha il nome dell'esperimento) e aggiungere una descrizione.</span><span class="sxs-lookup"><span data-stu-id="32305-180">Here you can modify the service name (it's given the experiment name by default) and give it a description.</span></span> <span data-ttu-id="32305-181">È anche possibile inserire etichette più descrittive per i dati di input e output.</span><span class="sxs-lookup"><span data-stu-id="32305-181">You can also give more friendly labels for the input and output data.</span></span>  

![Configurare il servizio Web][5]  

### <a name="deploy-as-a-new-web-service"></a><span data-ttu-id="32305-183">Distribuire l'esperimento come nuovo servizio Web</span><span class="sxs-lookup"><span data-stu-id="32305-183">Deploy as a New web service</span></span>

> [!NOTE] 
> <span data-ttu-id="32305-184">Per distribuire un nuovo servizio Web è necessario disporre delle autorizzazioni sufficienti nella sottoscrizione a cui si sta distribuendo il servizio Web.</span><span class="sxs-lookup"><span data-stu-id="32305-184">To deploy a New web service you must have sufficient permissions in the subscription to which you are deploying the web service.</span></span> <span data-ttu-id="32305-185">Per altre informazioni, vedere [Gestire un servizio Web usando il portale dei servizi Web di Azure Machine Learning](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="32305-185">For more information, see [Manage a web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="32305-186">Per distribuire un nuovo servizio Web derivato dall'esperimento:</span><span class="sxs-lookup"><span data-stu-id="32305-186">To deploy a New web service derived from our experiment:</span></span>

1. <span data-ttu-id="32305-187">Fare clic su **Deploy Web Service** (Distribuisci servizio Web) sotto l'area di disegno e selezionare **Deploy Web Service [New]** (Distribuisci servizio Web [Nuovo]).</span><span class="sxs-lookup"><span data-stu-id="32305-187">Click **Deploy Web Service** below the canvas and select **Deploy Web Service [New]**.</span></span> <span data-ttu-id="32305-188">Machine Learning Studio visualizza la pagina **Deploy Experiment** (Distribuisci esperimento) dei servizi Web di Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="32305-188">Machine Learning Studio transfers you to the Azure Machine Learning web services **Deploy Experiment** page.</span></span>

2. <span data-ttu-id="32305-189">Immettere un nome per il servizio Web.</span><span class="sxs-lookup"><span data-stu-id="32305-189">Enter a name for the web service.</span></span> 

3. <span data-ttu-id="32305-190">Per **Piano tariffario** è possibile selezionare un piano tariffario esistente o selezionare "Nuovo" e denominare il nuovo piano, quindi selezionare l'opzione del piano mensile.</span><span class="sxs-lookup"><span data-stu-id="32305-190">For **Price Plan**, you can select an existing pricing plan, or select "Create new" and give the new plan a name and select the monthly plan option.</span></span> <span data-ttu-id="32305-191">Per impostazione predefinita vengono usati i livelli di piano per l'area predefinita e il servizio Web viene distribuito in questa area.</span><span class="sxs-lookup"><span data-stu-id="32305-191">The plan tiers default to the plans for your default region and your web service is deployed to that region.</span></span>

4. <span data-ttu-id="32305-192">Fare clic su **Distribuisci**.</span><span class="sxs-lookup"><span data-stu-id="32305-192">Click **Deploy**.</span></span>

<span data-ttu-id="32305-193">Dopo alcuni minuti verrà visualizzata la pagina **Avvio rapido** per il servizio Web.</span><span class="sxs-lookup"><span data-stu-id="32305-193">After a few minutes, the **Quickstart** page for your web service opens.</span></span>

<span data-ttu-id="32305-194">È possibile configurare il servizio facendo clic sulla scheda **Configura**.</span><span class="sxs-lookup"><span data-stu-id="32305-194">You can configure the service by clicking the **Configure** tab.</span></span> <span data-ttu-id="32305-195">Qui è possibile modificare il titolo del servizio e assegnare una descrizione.</span><span class="sxs-lookup"><span data-stu-id="32305-195">Here you can modify the service title and give it a description.</span></span> 

<span data-ttu-id="32305-196">Per testare il servizio Web, selezionare la scheda **Test**. Vedere **Testare il servizio Web** di seguito.</span><span class="sxs-lookup"><span data-stu-id="32305-196">To test the web service, click the **Test** tab (see **Test the web service** below).</span></span> <span data-ttu-id="32305-197">Per informazioni sulla creazione di applicazioni in grado di accedere al servizio Web, fare clic sull'opzione di menu **Consumo**. Altre informazioni sono disponibili nella sezione successiva di questa procedura dettagliata.</span><span class="sxs-lookup"><span data-stu-id="32305-197">For information on creating applications that can access the web service, click the **Consume** tab (the next step in this walkthrough will go into more detail).</span></span>

> [!TIP]
> <span data-ttu-id="32305-198">È possibile aggiornare il servizio Web dopo averlo distribuito.</span><span class="sxs-lookup"><span data-stu-id="32305-198">You can update the web service after you've deployed it.</span></span> <span data-ttu-id="32305-199">Se, ad esempio, si vuole cambiare il modello, è possibile modificare l'esperimento di training, modificare i parametri del modello e fare clic su **Deploy Web Service** (Distribuisci servizio Web), selezionando **Deploy Web Service [Classic]** (Distribuisci servizio Web [Classico]) o **Deploy Web Service [New]** (Distribuisci servizio Web [Nuovo]).</span><span class="sxs-lookup"><span data-stu-id="32305-199">For example, if you want to change your model, then you can edit the training experiment, tweak the model parameters, and click **Deploy Web Service**, selecting **Deploy Web Service [Classic]** or **Deploy Web Service [New]**.</span></span> <span data-ttu-id="32305-200">Quando si distribuisce di nuovo l'esperimento, il servizio Web viene sostituito con il modello aggiornato.</span><span class="sxs-lookup"><span data-stu-id="32305-200">When you deploy the experiment again, it replaces the web service, now using your updated model.</span></span>  
> 
> 

## <a name="test-the-web-service"></a><span data-ttu-id="32305-201">Testare il servizio Web</span><span class="sxs-lookup"><span data-stu-id="32305-201">Test the web service</span></span>

<span data-ttu-id="32305-202">Quando viene eseguito l'accesso al servizio Web, i dati dell'utente vengono inseriti mediante il modulo **Web service input** (Input servizio Web)e trasferiti nel modulo [Score Model][score-model] (Modello punteggio), in cui viene assegnato un punteggio.</span><span class="sxs-lookup"><span data-stu-id="32305-202">When the web service is accessed, the user's data enters through the **Web service input** module where it's passed to the [Score Model][score-model] module and scored.</span></span> <span data-ttu-id="32305-203">In considerazione del modo in cui l'esperimento predittivo è configurato, il modello presuppone che i dati abbiano lo stesso formato del set di dati del rischio di credito originale.</span><span class="sxs-lookup"><span data-stu-id="32305-203">The way we've set up the predictive experiment, the model expects data in the same format as the original credit risk dataset.</span></span>
<span data-ttu-id="32305-204">I risultati vengono quindi restituiti all'utente dal servizio Web tramite il modulo **Output servizio Web**.</span><span class="sxs-lookup"><span data-stu-id="32305-204">The results are returned to the user from the web service through the **Web service output** module.</span></span>

> [!TIP]
> <span data-ttu-id="32305-205">In considerazione del modo in cui l'esperimento predittivo è configurato, vengono restituiti tutti i risultati del modulo [Score Model][score-model].</span><span class="sxs-lookup"><span data-stu-id="32305-205">The way we have the predictive experiment configured, the entire results from the [Score Model][score-model] module are returned.</span></span> <span data-ttu-id="32305-206">Ciò include tutti i dati di input, il valore del rischio di credito e il valore di probabilità del punteggio.</span><span class="sxs-lookup"><span data-stu-id="32305-206">This includes all the input data plus the credit risk value and the scoring probability.</span></span> <span data-ttu-id="32305-207">Ma è possibile restituire un elemento diverso se si desidera, ad esempio, si potrebbe restituire solo il valore di rischio di credito.</span><span class="sxs-lookup"><span data-stu-id="32305-207">But you can return something different if you want - for example, you could return just the credit risk value.</span></span> <span data-ttu-id="32305-208">A tale scopo, inserire un modulo [Project Columns][project-columns] (Colonne progetto) tra [Score Model][score-model] (Modello punteggio) e **Output servizio Web** per eliminare le colonne che il servizio Web non deve restituire.</span><span class="sxs-lookup"><span data-stu-id="32305-208">To do this, insert a [Project Columns][project-columns] module between [Score Model][score-model] and the **Web service output** to eliminate columns you don't want the web service to return.</span></span> 
> 
> 

<span data-ttu-id="32305-209">È possibile testare il servizio Web in **Machine Learning Studio** o nel portale dei **servizi Web di Azure Machine Learning**.</span><span class="sxs-lookup"><span data-stu-id="32305-209">You can test a Classic web service either in **Machine Learning Studio** or in the **Azure Machine Learning Web Services** portal.</span></span>
<span data-ttu-id="32305-210">È possibile testare un nuovo servizio Web solo dal portale dei **servizi Web di Azure Machine Learning**.</span><span class="sxs-lookup"><span data-stu-id="32305-210">You can test a New web service only in the **Machine Learning Web Services** portal.</span></span>

> [!TIP]
> <span data-ttu-id="32305-211">Quando il test viene eseguito nel portale dei servizi Web di Azure Machine Learning, è possibile fare in modo che il portali crei dati di esempio da usare per testare il servizio di richiesta-risposta.</span><span class="sxs-lookup"><span data-stu-id="32305-211">When testing in the Azure Machine Learning Web Services portal, you can have the portal create sample data that you can use to test the Request-Response service.</span></span> <span data-ttu-id="32305-212">Nella pagina **Configura** selezionare "Sì" per la richiesta di **dati di esempio abilitati?**.</span><span class="sxs-lookup"><span data-stu-id="32305-212">On the **Configure** page, select "Yes" for **Sample Data Enabled?**.</span></span> <span data-ttu-id="32305-213">Quando si apre la scheda Richiesta-risposta della pagina **Test**, il portale compila i dati di esempio prelevati dal set di dati del rischio di credito originale.</span><span class="sxs-lookup"><span data-stu-id="32305-213">When you open the Request-Response tab on the **Test** page, the portal fills in sample data taken from the original credit risk dataset.</span></span>

### <a name="test-a-classic-web-service"></a><span data-ttu-id="32305-214">Testare un servizio Web classico</span><span class="sxs-lookup"><span data-stu-id="32305-214">Test a Classic web service</span></span>

<span data-ttu-id="32305-215">È possibile testare un servizio Web classico in Machine Learning Studio o nel portale dei servizi Web di Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="32305-215">You can test a Classic web service in Machine Learning Studio or in the Machine Learning Web Services portal.</span></span> 

#### <a name="test-in-machine-learning-studio"></a><span data-ttu-id="32305-216">Testare in Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="32305-216">Test in Machine Learning Studio</span></span>

1. <span data-ttu-id="32305-217">Nella pagina **DASHBOARD** del servizio Web fare clic sul pulsante **Test** in **Default Endpoint** (Endpoint predefinito).</span><span class="sxs-lookup"><span data-stu-id="32305-217">On the **DASHBOARD** page for the web service, click the **Test** button under **Default Endpoint**.</span></span> <span data-ttu-id="32305-218">Viene visualizzata una finestra di dialogo che richiede i dati di input per il servizio.</span><span class="sxs-lookup"><span data-stu-id="32305-218">A dialog pops up and asks you for the input data for the service.</span></span> <span data-ttu-id="32305-219">Sono le stesse colonne visualizzate nel set di dati del rischio di credito originale.</span><span class="sxs-lookup"><span data-stu-id="32305-219">These are the same columns that appeared in the original credit risk dataset.</span></span>  

2. <span data-ttu-id="32305-220">Immettere un set di dati e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="32305-220">Enter a set of data and then click **OK**.</span></span> 

#### <a name="test-in-the-machine-learning-web-services-portal"></a><span data-ttu-id="32305-221">Testare nel portale dei servizi Web di Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="32305-221">Test in the Machine Learning Web Services portal</span></span>

1. <span data-ttu-id="32305-222">Nella pagina **DASHBOARD** del servizio Web fare clic sul pulsante **Test preview** (Anteprima test) in **Default Endpoint** (Endpoint predefinito).</span><span class="sxs-lookup"><span data-stu-id="32305-222">On the **DASHBOARD** page for the web service, click the **Test preview** link under **Default Endpoint**.</span></span> <span data-ttu-id="32305-223">Viene visualizzata la pagina di test nel portale del servizio Web di Azure Machine Learning per l'endpoint di servizio Web e vengono chiesti i dati di input per il servizio.</span><span class="sxs-lookup"><span data-stu-id="32305-223">The test page in the Azure Machine Learning Web Services portal for the web service endpoint opens and asks you for the input data for the service.</span></span> <span data-ttu-id="32305-224">Sono le stesse colonne visualizzate nel set di dati del rischio di credito originale.</span><span class="sxs-lookup"><span data-stu-id="32305-224">These are the same columns that appeared in the original credit risk dataset.</span></span>

2. <span data-ttu-id="32305-225">Fare clic su **Test Request-Response** (Test Richiesta-risposta).</span><span class="sxs-lookup"><span data-stu-id="32305-225">Click **Test Request-Response**.</span></span> 

### <a name="test-a-new-web-service"></a><span data-ttu-id="32305-226">Testare un nuovo servizio Web</span><span class="sxs-lookup"><span data-stu-id="32305-226">Test a New web service</span></span>

<span data-ttu-id="32305-227">È possibile testare un nuovo servizio Web solo dal portale dei servizi Web di Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="32305-227">You can test a New web service only in the Machine Learning Web Services portal.</span></span>

1. <span data-ttu-id="32305-228">Nel portale dei [servizi Web di Azure Machine Learning](https://services.azureml.net/quickstart) fare clic su **Test** nella parte superiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="32305-228">In the [Azure Machine Learning Web Services](https://services.azureml.net/quickstart) portal, click **Test** at the top of the page.</span></span> <span data-ttu-id="32305-229">Viene visualizzata la pagina **Test**, in cui è possibile immettere i dati per il servizio.</span><span class="sxs-lookup"><span data-stu-id="32305-229">The **Test** page opens and you can input data for the service.</span></span> <span data-ttu-id="32305-230">I campi di input visualizzati corrispondono alle colonne visualizzate nel set di dati del rischio di credito originale.</span><span class="sxs-lookup"><span data-stu-id="32305-230">The input fields displayed correspond to the columns that appeared in the original credit risk dataset.</span></span> 

2. <span data-ttu-id="32305-231">Immettere un set di dati e quindi fare clic su **Test Request-Response**(Test Richiesta-risposta).</span><span class="sxs-lookup"><span data-stu-id="32305-231">Enter a set of data and then click **Test Request-Response**.</span></span>

<span data-ttu-id="32305-232">I risultati del test vengono visualizzati sul lato destro della pagina nella colonna di output.</span><span class="sxs-lookup"><span data-stu-id="32305-232">The results of the test are displayed on the right-hand side of the page in the output column.</span></span> 


## <a name="manage-the-web-service"></a><span data-ttu-id="32305-233">Gestire il servizio Web</span><span class="sxs-lookup"><span data-stu-id="32305-233">Manage the web service</span></span>

### <a name="manage-a-classic-web-service-in-the-azure-classic-portal"></a><span data-ttu-id="32305-234">Gestire un servizio Web classico nel portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="32305-234">Manage a Classic web service in the Azure classic portal</span></span>

<span data-ttu-id="32305-235">Dopo aver distribuito il servizio Web classico, è possibile gestirlo dal [portale di Azure classico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="32305-235">Once you've deployed your Classic web service, you can manage it from the [Azure classic portal](https://manage.windowsazure.com).</span></span>

1. <span data-ttu-id="32305-236">Accedere al [portale di Azure classico](https://manage.windowsazure.com)</span><span class="sxs-lookup"><span data-stu-id="32305-236">Sign in to the [Azure classic portal](https://manage.windowsazure.com)</span></span>
2. <span data-ttu-id="32305-237">Nel riquadro dei servizi di Microsoft Azure fare clic su **MACHINE LEARNING**</span><span class="sxs-lookup"><span data-stu-id="32305-237">In the Microsoft Azure services panel, click **MACHINE LEARNING**</span></span>
3. <span data-ttu-id="32305-238">Fare clic sull'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="32305-238">Click your workspace</span></span>
4. <span data-ttu-id="32305-239">Fare clic sulla scheda **Servizi Web**.</span><span class="sxs-lookup"><span data-stu-id="32305-239">Click the **Web services** tab</span></span>
5. <span data-ttu-id="32305-240">Fare clic sul servizio Web creato</span><span class="sxs-lookup"><span data-stu-id="32305-240">Click the web service we created</span></span>
6. <span data-ttu-id="32305-241">Fare clic sull'endpoint "predefinito".</span><span class="sxs-lookup"><span data-stu-id="32305-241">Click the "default" endpoint</span></span>

<span data-ttu-id="32305-242">Da qui è possibile eseguire varie operazioni, ad esempio monitorare come opera il servizio Web e apportare piccole modifiche alle prestazioni cambiando il numero di chiamate simultanee gestite dal servizio.</span><span class="sxs-lookup"><span data-stu-id="32305-242">From here, you can do things like monitor how the web service is doing and make performance tweaks by changing how many concurrent calls the service can handle.</span></span>

<span data-ttu-id="32305-243">Per informazioni dettagliate, vedere:</span><span class="sxs-lookup"><span data-stu-id="32305-243">For more details, see:</span></span>

* [<span data-ttu-id="32305-244">Creazione di endpoint</span><span class="sxs-lookup"><span data-stu-id="32305-244">Creating Endpoints</span></span>](machine-learning-create-endpoint.md)
* [<span data-ttu-id="32305-245">Ridimensionamento di un servizio Web</span><span class="sxs-lookup"><span data-stu-id="32305-245">Scaling web service</span></span>](machine-learning-scaling-webservice.md)

### <a name="manage-a-classic-or-new-web-service-in-the-azure-machine-learning-web-services-portal"></a><span data-ttu-id="32305-246">Gestire un servizio Web nuovo o classico usando il portale dei servizi Web di Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="32305-246">Manage a Classic or New web service in the Azure Machine Learning Web Services portal</span></span>

<span data-ttu-id="32305-247">Dopo avere distribuito il servizio Web, classico o nuovo, è possibile gestirlo dal [portale dei servizi Web di Microsoft Azure Machine Learning](https://services.azureml.net/quickstart).</span><span class="sxs-lookup"><span data-stu-id="32305-247">Once you've deployed your web service, whether Classic or New, you can manage it from the [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/quickstart) portal.</span></span>

<span data-ttu-id="32305-248">Per monitorare le prestazioni del servizio Web:</span><span class="sxs-lookup"><span data-stu-id="32305-248">To monitor the performance of your web service:</span></span>

1. <span data-ttu-id="32305-249">Accedere al portale dei [servizi Web di Microsoft Azure Machine Learning](https://services.azureml.net/quickstart)</span><span class="sxs-lookup"><span data-stu-id="32305-249">Sign in to the [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/quickstart) portal</span></span>
2. <span data-ttu-id="32305-250">Fare clic su **Servizi Web**</span><span class="sxs-lookup"><span data-stu-id="32305-250">Click **Web services**</span></span>
3. <span data-ttu-id="32305-251">Fare clic sul servizio Web</span><span class="sxs-lookup"><span data-stu-id="32305-251">Click your web service</span></span>
4. <span data-ttu-id="32305-252">Fare clic su **Dashboard**</span><span class="sxs-lookup"><span data-stu-id="32305-252">Click the **Dashboard**</span></span>

- - -
<span data-ttu-id="32305-253">**Passaggio successivo:[Accedere al servizio Web](machine-learning-walkthrough-6-access-web-service.md)**</span><span class="sxs-lookup"><span data-stu-id="32305-253">**Next: [Access the web service](machine-learning-walkthrough-6-access-web-service.md)**</span></span>

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
