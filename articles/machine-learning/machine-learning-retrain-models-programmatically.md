---
title: aaaRetrain Machine Learning i modelli a livello di codice | Documenti Microsoft
description: Informazioni su come tooprogrammatically ripetere il training di un modello e aggiornamento hello web servizio toouse hello appena modello con Training in Azure Machine Learning.
services: machine-learning
documentationcenter: 
author: raymondlaghaeian
manager: jhubbard
editor: cgronlun
ms.assetid: 7ae4f977-e6bf-4d04-9dde-28a66ce7b664
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: raymondl;garye;v-donglo
ms.openlocfilehash: edbb64c08f7d9edf3c76e23e0cc7e14c0125d697
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-machine-learning-models-programmatically"></a><span data-ttu-id="4a2ec-103">Ripetere il training dei modelli di Machine Learning a livello di codice</span><span class="sxs-lookup"><span data-stu-id="4a2ec-103">Retrain Machine Learning models programmatically</span></span>
<span data-ttu-id="4a2ec-104">In questa procedura dettagliata si apprenderà come tooprogrammatically ripetere il training di un servizio Web di Azure Machine Learning con c# e hello servizio esecuzione Batch di Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="4a2ec-104">In this walkthrough, you will learn how tooprogrammatically retrain an Azure Machine Learning Web Service using C# and hello Machine Learning Batch Execution service.</span></span>

<span data-ttu-id="4a2ec-105">Dopo avere ripetere il training del modello di hello, hello procedure dettagliate seguenti Mostra come tooupdate hello modello del servizio web predittivo:</span><span class="sxs-lookup"><span data-stu-id="4a2ec-105">Once you have retrained hello model, hello following walkthroughs show how tooupdate hello model in your predictive web service:</span></span>

* <span data-ttu-id="4a2ec-106">Se è stato distribuito un servizio web classica nel portale di servizi Web di Machine Learning hello, vedere [ripetere il training di un servizio web classica](machine-learning-retrain-a-classic-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="4a2ec-106">If you deployed a Classic web service in hello Machine Learning Web Services portal, see [Retrain a Classic web service](machine-learning-retrain-a-classic-web-service.md).</span></span> 
* <span data-ttu-id="4a2ec-107">Se è stato distribuito un nuovo servizio web, vedere [ripetere il training di un nuovo servizio web usando i cmdlet di Machine Learning Management hello](machine-learning-retrain-new-web-service-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="4a2ec-107">If you deployed a New web service, see [Retrain a New web service using hello Machine Learning Management cmdlets](machine-learning-retrain-new-web-service-using-powershell.md).</span></span>

<span data-ttu-id="4a2ec-108">Per una panoramica del processo di ripetizione di training hello, vedere [ripetere il training di un modello di Machine Learning](machine-learning-retrain-machine-learning-model.md).</span><span class="sxs-lookup"><span data-stu-id="4a2ec-108">For an overview of hello retraining process, see [Retrain a Machine Learning Model](machine-learning-retrain-machine-learning-model.md).</span></span>

<span data-ttu-id="4a2ec-109">Se si desidera toostart esistenti nuovo gestore di risorse di Azure basato su servizio web, vedere [ripetere il training di un servizio web predittivo esistente](machine-learning-retrain-existing-resource-manager-based-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="4a2ec-109">If you want toostart with your existing New Azure Resource Manager based web service, see [Retrain an existing Predictive web service](machine-learning-retrain-existing-resource-manager-based-web-service.md).</span></span>

## <a name="create-a-training-experiment"></a><span data-ttu-id="4a2ec-110">Creare un esperimento di training</span><span class="sxs-lookup"><span data-stu-id="4a2ec-110">Create a training experiment</span></span>
<span data-ttu-id="4a2ec-111">Per questo esempio, si utilizzerà "esempio 5: Train, Test, Evaluate for Binary Classification: Adult Dataset" dagli esempi di Microsoft Azure Machine Learning hello.</span><span class="sxs-lookup"><span data-stu-id="4a2ec-111">For this example, you will use "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset" from hello Microsoft Azure Machine Learning samples.</span></span> 

<span data-ttu-id="4a2ec-112">sperimentazione hello toocreate:</span><span class="sxs-lookup"><span data-stu-id="4a2ec-112">toocreate hello experiment:</span></span>

1. <span data-ttu-id="4a2ec-113">Accedere a tooMicrosoft Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="4a2ec-113">Sign into tooMicrosoft Azure Machine Learning Studio.</span></span> 
2. <span data-ttu-id="4a2ec-114">Scegliere hello nell'angolo inferiore destro del dashboard hello, **New**.</span><span class="sxs-lookup"><span data-stu-id="4a2ec-114">On hello bottom right corner of hello dashboard, click **New**.</span></span>
3. <span data-ttu-id="4a2ec-115">Hello Microsoft Samples, selezionare 5 di esempio.</span><span class="sxs-lookup"><span data-stu-id="4a2ec-115">From hello Microsoft Samples, select Sample 5.</span></span>
4. <span data-ttu-id="4a2ec-116">esperimento hello toorename, nella parte superiore di hello dell'area di disegno di hello esperimento, selezionare il nome di sperimentazione hello "esempio 5: Train, Test, Evaluate for Binary Classification: Adult Dataset".</span><span class="sxs-lookup"><span data-stu-id="4a2ec-116">toorename hello experiment, at hello top of hello experiment canvas, select hello experiment name "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset".</span></span>
5. <span data-ttu-id="4a2ec-117">Digitare Census Model.</span><span class="sxs-lookup"><span data-stu-id="4a2ec-117">Type Census Model.</span></span>
6. <span data-ttu-id="4a2ec-118">Nella parte inferiore di hello dell'area di disegno esperimento hello, fare clic su **eseguire**.</span><span class="sxs-lookup"><span data-stu-id="4a2ec-118">At hello bottom of hello experiment canvas, click **Run**.</span></span>
7. <span data-ttu-id="4a2ec-119">Fare clic su **Set Up Web service** (Configura servizio Web) e selezionare **Retraining Web service** (Servizio Web di ripetizione del training).</span><span class="sxs-lookup"><span data-stu-id="4a2ec-119">Click **Set Up web service** and select **Retraining web service**.</span></span> 

<span data-ttu-id="4a2ec-120">Hello il seguente esperimento iniziale hello.</span><span class="sxs-lookup"><span data-stu-id="4a2ec-120">hello following shows hello initial experiment.</span></span>
   
   ![Esperimento iniziale.][2]


## <a name="create-a-predictive-experiment-and-publish-as-a-web-service"></a><span data-ttu-id="4a2ec-122">Creare un esperimento predittivo e pubblicarlo come servizio Web</span><span class="sxs-lookup"><span data-stu-id="4a2ec-122">Create a predictive experiment and publish as a web service</span></span>
<span data-ttu-id="4a2ec-123">Ora viene creato un esperimento predicativo.</span><span class="sxs-lookup"><span data-stu-id="4a2ec-123">Next you create a Predicative Experiment.</span></span>

1. <span data-ttu-id="4a2ec-124">Nella parte inferiore di hello dell'area di disegno esperimento hello, fare clic su **di servizio Web** e selezionare **servizio Web predittivo**.</span><span class="sxs-lookup"><span data-stu-id="4a2ec-124">At hello bottom of hello experiment canvas, click **Set Up Web Service** and select **Predictive Web Service**.</span></span> <span data-ttu-id="4a2ec-125">Questo modello hello viene salvata come un modello con training e aggiunge i moduli di Input e Output del servizio web.</span><span class="sxs-lookup"><span data-stu-id="4a2ec-125">This saves hello model as a Trained Model and adds web service Input and Output modules.</span></span> 
2. <span data-ttu-id="4a2ec-126">Fare clic su **Run**.</span><span class="sxs-lookup"><span data-stu-id="4a2ec-126">Click **Run**.</span></span> 
3. <span data-ttu-id="4a2ec-127">Al termine dell'esecuzione esperimento hello, fare clic su **distribuzione di un servizio Web [classica]** o **distribuzione servizio Web [New]**.</span><span class="sxs-lookup"><span data-stu-id="4a2ec-127">After hello experiment has finished running, click **Deploy Web Service [Classic]** or **Deploy Web Service [New]**.</span></span>

> [!NOTE] 
> <span data-ttu-id="4a2ec-128">un nuovo servizio web deve disporre di autorizzazioni sufficienti in hello toowhich di sottoscrizione per la distribuzione del servizio web hello toodeploy.</span><span class="sxs-lookup"><span data-stu-id="4a2ec-128">toodeploy a New web service you must have sufficient permissions in hello subscription toowhich you deploying hello web service.</span></span> <span data-ttu-id="4a2ec-129">Per ulteriori informazioni, vedere [gestire un servizio Web tramite il portale di servizi Web di Azure Machine Learning hello](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="4a2ec-129">For more information see, [Manage a Web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

## <a name="deploy-hello-training-experiment-as-a-training-web-service"></a><span data-ttu-id="4a2ec-130">Distribuire hello esperimento di training come un servizio web di Training</span><span class="sxs-lookup"><span data-stu-id="4a2ec-130">Deploy hello training experiment as a Training web service</span></span>
<span data-ttu-id="4a2ec-131">modello con training hello tooretrain, è necessario distribuire l'esperimento di training hello che è stato creato come un servizio web Retraining.</span><span class="sxs-lookup"><span data-stu-id="4a2ec-131">tooretrain hello trained model, you must deploy hello training experiment that you created as a Retraining web service.</span></span> <span data-ttu-id="4a2ec-132">Questo servizio web è necessario un *Output del servizio Web* modulo connesso toohello  *[Train Model] [ train-model]*  module, toobe tooproduce in grado di nuovo modelli di training.</span><span class="sxs-lookup"><span data-stu-id="4a2ec-132">This web service needs a *Web Service Output* module connected toohello *[Train Model][train-model]* module, toobe able tooproduce new trained models.</span></span>

1. <span data-ttu-id="4a2ec-133">esperimento di training toohello tooreturn, fare clic sull'icona esperimenti hello nel riquadro di sinistra hello, quindi fare clic su esperimento hello denominato modello di censimento.</span><span class="sxs-lookup"><span data-stu-id="4a2ec-133">tooreturn toohello training experiment, click hello Experiments icon in hello left pane, then click hello experiment named Census Model.</span></span>  
2. <span data-ttu-id="4a2ec-134">Nella casella di ricerca di hello elementi esperimento di ricerca, digitare il servizio web.</span><span class="sxs-lookup"><span data-stu-id="4a2ec-134">In hello Search Experiment Items search box, type web service.</span></span> 
3. <span data-ttu-id="4a2ec-135">Trascinare un *Input del servizio Web* modulo sul hello provare l'area di disegno e connettersi toohello il relativo output *Clean Missing Data* modulo.</span><span class="sxs-lookup"><span data-stu-id="4a2ec-135">Drag a *Web Service Input* module onto hello experiment canvas and connect its output toohello *Clean Missing Data* module.</span></span>  <span data-ttu-id="4a2ec-136">In questo modo si garantisce che i dati viene elaborati hello stesso come dati di training originale.</span><span class="sxs-lookup"><span data-stu-id="4a2ec-136">This ensures that your retraining data is processed hello same way as your original training data.</span></span>
4. <span data-ttu-id="4a2ec-137">Trascinare due *servizio Output web* moduli su hello provare l'area di disegno.</span><span class="sxs-lookup"><span data-stu-id="4a2ec-137">Drag two *web service Output* modules onto hello experiment canvas.</span></span> <span data-ttu-id="4a2ec-138">Connettere l'output di hello di hello *Train Model* output tooone e hello del modulo di hello *Evaluate Model* toohello altro modulo.</span><span class="sxs-lookup"><span data-stu-id="4a2ec-138">Connect hello output of hello *Train Model* module tooone and hello output of hello *Evaluate Model* module toohello other.</span></span> <span data-ttu-id="4a2ec-139">output del servizio web per Hello **Train Model** offre un nuovo modello con training di hello.</span><span class="sxs-lookup"><span data-stu-id="4a2ec-139">hello web service output for **Train Model** gives us hello new trained model.</span></span> <span data-ttu-id="4a2ec-140">Hello output collegato troppo**Evaluate Model** restituisce tale modulo dell'output, ovvero i risultati delle prestazioni hello.</span><span class="sxs-lookup"><span data-stu-id="4a2ec-140">hello output attached too**Evaluate Model** returns that module’s output, which is hello performance results.</span></span>
5. <span data-ttu-id="4a2ec-141">Fare clic su **Run**.</span><span class="sxs-lookup"><span data-stu-id="4a2ec-141">Click **Run**.</span></span> 

<span data-ttu-id="4a2ec-142">Successivamente è necessario distribuire hello esperimento di training come servizio web che produce un modello con training e risultati della valutazione del modello.</span><span class="sxs-lookup"><span data-stu-id="4a2ec-142">Next you must deploy hello training experiment as a web service that produces a trained model and model evaluation results.</span></span> <span data-ttu-id="4a2ec-143">tooaccomplish questa operazione, il set successivo di azioni dipendono se si lavora con un servizio web classica o di un nuovo servizio web.</span><span class="sxs-lookup"><span data-stu-id="4a2ec-143">tooaccomplish this, your next set of actions are dependent on whether you are working with a Classic web service or a New web service.</span></span>  

<span data-ttu-id="4a2ec-144">**Servizio Web classico**</span><span class="sxs-lookup"><span data-stu-id="4a2ec-144">**Classic web service**</span></span>

<span data-ttu-id="4a2ec-145">Nella parte inferiore di hello dell'area di disegno esperimento hello, fare clic su **di servizio Web** e selezionare **distribuzione di un servizio Web [classica]**.</span><span class="sxs-lookup"><span data-stu-id="4a2ec-145">At hello bottom of hello experiment canvas, click **Set Up Web Service** and select **Deploy Web Service [Classic]**.</span></span> <span data-ttu-id="4a2ec-146">Servizio Web Hello **Dashboard** viene visualizzato con una pagina della Guida hello chiave API e hello API per l'esecuzione Batch.</span><span class="sxs-lookup"><span data-stu-id="4a2ec-146">hello Web Service **Dashboard** is displayed with hello API Key and hello API help page for Batch Execution.</span></span> <span data-ttu-id="4a2ec-147">È utilizzabile solo hello metodo di esecuzione Batch per la creazione di modelli di training.</span><span class="sxs-lookup"><span data-stu-id="4a2ec-147">Only hello Batch Execution method can be used for creating Trained Models.</span></span>

<span data-ttu-id="4a2ec-148">**Nuovo servizio Web**</span><span class="sxs-lookup"><span data-stu-id="4a2ec-148">**New web service**</span></span>

<span data-ttu-id="4a2ec-149">Nella parte inferiore di hello dell'area di disegno esperimento hello, fare clic su **di servizio Web** e selezionare **distribuzione servizio Web [New]**.</span><span class="sxs-lookup"><span data-stu-id="4a2ec-149">At hello bottom of hello experiment canvas, click **Set Up Web Service** and select **Deploy Web Service [New]**.</span></span> <span data-ttu-id="4a2ec-150">portale Web del servizio servizi Web di Azure Machine Learning Hello verrà visualizzata la pagina del servizio web di distribuire toohello.</span><span class="sxs-lookup"><span data-stu-id="4a2ec-150">hello Web Service Azure Machine Learning Web Services portal opens toohello Deploy web service page.</span></span> <span data-ttu-id="4a2ec-151">Digitare un nome per il servizio Web e scegliere un piano di pagamento, quindi fare clic su **Distribuisci**.</span><span class="sxs-lookup"><span data-stu-id="4a2ec-151">Type a name for your web service and choose a payment plan, then click **Deploy**.</span></span> <span data-ttu-id="4a2ec-152">Solo hello metodo di esecuzione di Batch può essere utilizzato per la creazione di modelli con training</span><span class="sxs-lookup"><span data-stu-id="4a2ec-152">Only hello Batch Execution method can be used for creating Trained Models</span></span>

<span data-ttu-id="4a2ec-153">In entrambi i casi, dopo l'esperimento ha completata esecuzione, flusso di lavoro hello risultante dovrebbe apparire come segue:</span><span class="sxs-lookup"><span data-stu-id="4a2ec-153">In either case, after experiment has completed running, hello resulting workflow should look as follows:</span></span>

![Flusso di lavoro risultante dopo l'esecuzione.][4]



## <a name="retrain-hello-model-with-new-data-using-bes"></a><span data-ttu-id="4a2ec-155">Ripetere il training del modello di hello con nuovi dati usando BES</span><span class="sxs-lookup"><span data-stu-id="4a2ec-155">Retrain hello model with new data using BES</span></span>
<span data-ttu-id="4a2ec-156">Per questo esempio, si utilizza c# toocreate hello formazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="4a2ec-156">For this example, you are using C# toocreate hello retraining application.</span></span> <span data-ttu-id="4a2ec-157">È possibile inoltre utilizzare hello Python o R esempio codice tooaccomplish questa attività.</span><span class="sxs-lookup"><span data-stu-id="4a2ec-157">You can also use hello Python or R sample code tooaccomplish this task.</span></span>

<span data-ttu-id="4a2ec-158">toocall hello API ripetizione di training:</span><span class="sxs-lookup"><span data-stu-id="4a2ec-158">toocall hello Retraining APIs:</span></span>

1. <span data-ttu-id="4a2ec-159">Creare un'applicazione console C# in Visual Studio. A tale scopo, selezionare **Nuovo** > **Progetto** > **Visual C#** > **Desktop classico di Windows** > **Applicazione console (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="4a2ec-159">Create a C# console application in Visual Studio: **New** > **Project** > **Visual C#** > **Windows Classic Desktop** > **Console App (.NET Framework)**.</span></span>
2. <span data-ttu-id="4a2ec-160">Accedi toohello portale servizio Web di Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="4a2ec-160">Sign in toohello Machine Learning Web Service portal.</span></span>
3. <span data-ttu-id="4a2ec-161">Se si usa un servizio Web classico, fare clic su **Classic Web Services**(Servizi Web classici).</span><span class="sxs-lookup"><span data-stu-id="4a2ec-161">If you are working with a Classic web service, click **Classic Web Services**.</span></span>
   1. <span data-ttu-id="4a2ec-162">Fare clic su servizio web hello in uso.</span><span class="sxs-lookup"><span data-stu-id="4a2ec-162">Click hello web service you are working with.</span></span>
   2. <span data-ttu-id="4a2ec-163">Fare clic su endpoint predefinito hello.</span><span class="sxs-lookup"><span data-stu-id="4a2ec-163">Click hello default endpoint.</span></span>
   3. <span data-ttu-id="4a2ec-164">Fare clic su **Consume**(Uso).</span><span class="sxs-lookup"><span data-stu-id="4a2ec-164">Click **Consume**.</span></span>
   4. <span data-ttu-id="4a2ec-165">Nella parte inferiore di hello di hello **consumare** pagina hello **codice di esempio** fare clic su **Batch**.</span><span class="sxs-lookup"><span data-stu-id="4a2ec-165">At hello bottom of hello **Consume** page, in hello **Sample Code** section, click **Batch**.</span></span>
   5. <span data-ttu-id="4a2ec-166">Continuare toostep 5 di questa procedura.</span><span class="sxs-lookup"><span data-stu-id="4a2ec-166">Continue toostep 5 of this procedure.</span></span>
4. <span data-ttu-id="4a2ec-167">Se si usa un nuovo servizio Web, fare clic su **Servizi Web**.</span><span class="sxs-lookup"><span data-stu-id="4a2ec-167">If you are working with a New web service, click **Web Services**.</span></span>
   1. <span data-ttu-id="4a2ec-168">Fare clic su servizio web hello in uso.</span><span class="sxs-lookup"><span data-stu-id="4a2ec-168">Click hello web service you are working with.</span></span>
   2. <span data-ttu-id="4a2ec-169">Fare clic su **Consume**(Uso).</span><span class="sxs-lookup"><span data-stu-id="4a2ec-169">Click **Consume**.</span></span>
   3. <span data-ttu-id="4a2ec-170">Nella parte inferiore di hello di hello consumare nella pagina hello **codice di esempio** fare clic su **Batch**.</span><span class="sxs-lookup"><span data-stu-id="4a2ec-170">At hello bottom of hello Consume page, in hello **Sample Code** section, click **Batch**.</span></span>
5. <span data-ttu-id="4a2ec-171">Copiare hello c# codice di esempio per l'esecuzione batch e incollarlo nel file Program.cs hello, assicurandosi che lo spazio dei nomi hello rimane invariata.</span><span class="sxs-lookup"><span data-stu-id="4a2ec-171">Copy hello sample C# code for batch execution and paste it into hello Program.cs file, making sure hello namespace remains intact.</span></span>

<span data-ttu-id="4a2ec-172">Aggiungere il pacchetto Nuget hello webapi come specificato nei commenti hello.</span><span class="sxs-lookup"><span data-stu-id="4a2ec-172">Add hello Nuget package Microsoft.AspNet.WebApi.Client as specified in hello comments.</span></span> <span data-ttu-id="4a2ec-173">tooadd hello riferimento tooMicrosoft.WindowsAzure.Storage.dll, si potrebbe essere necessario innanzitutto libreria client di hello tooinstall per servizi di archiviazione di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="4a2ec-173">tooadd hello reference tooMicrosoft.WindowsAzure.Storage.dll, you might first need tooinstall hello client library for Microsoft Azure storage services.</span></span> <span data-ttu-id="4a2ec-174">Per altre informazioni, vedere i [servizi di archiviazione Windows](https://www.nuget.org/packages/WindowsAzure.Storage).</span><span class="sxs-lookup"><span data-stu-id="4a2ec-174">For more information, see [Windows Storage Services](https://www.nuget.org/packages/WindowsAzure.Storage).</span></span>

### <a name="update-hello-apikey-declaration"></a><span data-ttu-id="4a2ec-175">Aggiornare hello apikey dichiarazione</span><span class="sxs-lookup"><span data-stu-id="4a2ec-175">Update hello apikey declaration</span></span>
<span data-ttu-id="4a2ec-176">Individuare hello **apikey** dichiarazione.</span><span class="sxs-lookup"><span data-stu-id="4a2ec-176">Locate hello **apikey** declaration.</span></span>

    const string apiKey = "abc123"; // Replace this with hello API key for hello web service

<span data-ttu-id="4a2ec-177">In hello **informazioni di base al consumo** sezione di hello **consumare** individuare la chiave primaria di hello e copiarlo toohello **apikey** dichiarazione.</span><span class="sxs-lookup"><span data-stu-id="4a2ec-177">In hello **Basic consumption info** section of hello **Consume** page, locate hello primary key and copy it toohello **apikey** declaration.</span></span>

### <a name="update-hello-azure-storage-information"></a><span data-ttu-id="4a2ec-178">Aggiornare le informazioni di archiviazione di Azure hello</span><span class="sxs-lookup"><span data-stu-id="4a2ec-178">Update hello Azure Storage information</span></span>
<span data-ttu-id="4a2ec-179">codice di esempio BES Hello carica un file da un tooAzure unità locale (ad esempio "C:\temp\CensusIpnput.csv"), archiviazione, elabora e scrive hello risultati indietro tooAzure archiviazione.</span><span class="sxs-lookup"><span data-stu-id="4a2ec-179">hello BES sample code uploads a file from a local drive (For example "C:\temp\CensusIpnput.csv") tooAzure Storage, processes it, and writes hello results back tooAzure Storage.</span></span>  

<span data-ttu-id="4a2ec-180">tooaccomplish questa attività, è necessario recuperare hello archiviazione nome, chiave e contenitore informazioni sull'account per l'account di archiviazione dal portale di Azure classico hello e aggiornamento hello corrispondenti valori nel codice hello.</span><span class="sxs-lookup"><span data-stu-id="4a2ec-180">tooaccomplish this task, you must retrieve hello Storage account name, key, and container information for your Storage account from hello classic Azure portal and hello update corresponding values in hello code.</span></span> 

1. <span data-ttu-id="4a2ec-181">Accedi a portale di Azure classico toohello.</span><span class="sxs-lookup"><span data-stu-id="4a2ec-181">Sign in toohello classic Azure portal.</span></span>
2. <span data-ttu-id="4a2ec-182">Nella colonna sinistra hello, fare clic su **archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="4a2ec-182">In hello left navigation column, click **Storage**.</span></span>
3. <span data-ttu-id="4a2ec-183">Dall'elenco di hello di account di archiviazione, selezionare uno toostore hello ripetere il training del modello.</span><span class="sxs-lookup"><span data-stu-id="4a2ec-183">From hello list of storage accounts, select one toostore hello retrained model.</span></span>
4. <span data-ttu-id="4a2ec-184">Nella parte inferiore di hello della pagina hello, fare clic su **Gestisci chiavi di accesso**.</span><span class="sxs-lookup"><span data-stu-id="4a2ec-184">At hello bottom of hello page, click **Manage Access Keys**.</span></span>
5. <span data-ttu-id="4a2ec-185">Copiare e salvare hello **chiave di accesso primaria** e hello Chiudi finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="4a2ec-185">Copy and save hello **Primary Access Key** and close hello dialog.</span></span> 
6. <span data-ttu-id="4a2ec-186">Nella parte superiore di hello della pagina hello, fare clic su **contenitori**.</span><span class="sxs-lookup"><span data-stu-id="4a2ec-186">At hello top of hello page, click **Containers**.</span></span>
7. <span data-ttu-id="4a2ec-187">Selezionare un contenitore esistente o crearne uno nuovo e salvare il nome di hello.</span><span class="sxs-lookup"><span data-stu-id="4a2ec-187">Select an existing container or create a new one and save hello name.</span></span>

<span data-ttu-id="4a2ec-188">Individuare hello *StorageAccountName*, *StorageAccountKey*, e *StorageContainerName* dichiarazioni e aggiornare i valori di hello è stato salvato da hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="4a2ec-188">Locate hello *StorageAccountName*, *StorageAccountKey*, and *StorageContainerName* declarations and update hello values you saved from hello Azure portal.</span></span>

    const string StorageAccountName = "mystorageacct"; // Replace this with your Azure Storage Account name
    const string StorageAccountKey = "a_storage_account_key"; // Replace this with your Azure Storage Key
    const string StorageContainerName = "mycontainer"; // Replace this with your Azure Storage Container name

<span data-ttu-id="4a2ec-189">È anche necessario verificare il file di input hello è disponibile nel percorso di hello specificate nel codice hello.</span><span class="sxs-lookup"><span data-stu-id="4a2ec-189">You also must ensure hello input file is available at hello location you specify in hello code.</span></span> 

### <a name="specify-hello-output-location"></a><span data-ttu-id="4a2ec-190">Specificare il percorso di output di hello</span><span class="sxs-lookup"><span data-stu-id="4a2ec-190">Specify hello output location</span></span>
<span data-ttu-id="4a2ec-191">Quando si specifica il percorso di output di hello in hello del payload della richiesta, hello estensione del file hello specificato *RelativeLocation* deve essere specificato come ilearner.</span><span class="sxs-lookup"><span data-stu-id="4a2ec-191">When specifying hello output location in hello Request Payload, hello extension of hello file specified in *RelativeLocation* must be specified as ilearner.</span></span> 

<span data-ttu-id="4a2ec-192">Vedere hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="4a2ec-192">See hello following example:</span></span>

    Outputs = new Dictionary<string, AzureBlobDataReference>() {
        {
            "output1",
            new AzureBlobDataReference()
            {
                ConnectionString = storageConnectionString,
                RelativeLocation = string.Format("{0}/output1results.ilearner", StorageContainerName) /*Replace this with hello location you would like toouse for your output file, and valid file extension (usually .csv for scoring results, or .ilearner for trained models)*/
            }
        },

> [!NOTE]
> <span data-ttu-id="4a2ec-193">nomi di Hello di percorsi di output possono essere diversi da quelle in questa procedura dettagliata sulla base di hello ordine in cui è stato aggiunto moduli di output di hello web servizio hello.</span><span class="sxs-lookup"><span data-stu-id="4a2ec-193">hello names of your output locations may be different from hello ones in this walkthrough based on hello order in which you added hello web service output modules.</span></span> <span data-ttu-id="4a2ec-194">Dopo aver impostato questo esperimento di training con due output, risultati di hello includono informazioni sul percorso di archiviazione per entrambi gli elementi.</span><span class="sxs-lookup"><span data-stu-id="4a2ec-194">Since you set up this training experiment with two outputs, hello results include storage location information for both of them.</span></span>  
> 
> 

![Output della ripetizione del training.][6]

<span data-ttu-id="4a2ec-196">Diagramma 4: output della ripetizione del training.</span><span class="sxs-lookup"><span data-stu-id="4a2ec-196">Diagram 4: Retraining output.</span></span>

## <a name="evaluate-hello-retraining-results"></a><span data-ttu-id="4a2ec-197">Valutare i risultati di ripetizione di training hello</span><span class="sxs-lookup"><span data-stu-id="4a2ec-197">Evaluate hello Retraining Results</span></span>
<span data-ttu-id="4a2ec-198">Quando si esegue un'applicazione hello, output di hello include l'URL di hello e tooaccess necessari token SAS hello risultati della valutazione.</span><span class="sxs-lookup"><span data-stu-id="4a2ec-198">When you run hello application, hello output includes hello URL and SAS token necessary tooaccess hello evaluation results.</span></span>

<span data-ttu-id="4a2ec-199">È possibile visualizzare i risultati delle prestazioni hello di hello Training modello combinando hello *BaseLocation*, *RelativeLocation*, e *SasBlobToken* dai risultati di output di hello per *USCITA2* (come mostrato nella precedente ripetizione di training immagine di output di hello) e incollare l'URL completo di hello nella barra degli indirizzi del browser hello.</span><span class="sxs-lookup"><span data-stu-id="4a2ec-199">You can see hello performance results of hello retrained model by combining hello *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from hello output results for *output2* (as shown in hello preceding retraining output image) and pasting hello complete URL in hello browser address bar.</span></span>  

<span data-ttu-id="4a2ec-200">Esamina hello risultati toodetermine modello sottoposto a training appena hello esegue anche sufficiente hello tooreplace uno esistente.</span><span class="sxs-lookup"><span data-stu-id="4a2ec-200">Examine hello results toodetermine whether hello newly trained model performs well enough tooreplace hello existing one.</span></span>

<span data-ttu-id="4a2ec-201">Hello copia *BaseLocation*, *RelativeLocation*, e *SasBlobToken* dai risultati di output di hello, che verranno utilizzati durante il processo di ripetizione di training hello.</span><span class="sxs-lookup"><span data-stu-id="4a2ec-201">Copy hello *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from hello output results, you will use them during hello retraining process.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4a2ec-202">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4a2ec-202">Next steps</span></span>
<span data-ttu-id="4a2ec-203">Se è stata distribuita, fare clic su servizio web predittivo hello **distribuzione di un servizio Web [classica]**, vedere [ripetere il training di un servizio web classica](machine-learning-retrain-a-classic-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="4a2ec-203">If you deployed hello predictive web service by clicking **Deploy Web Service [Classic]**, see [Retrain a Classic web service](machine-learning-retrain-a-classic-web-service.md).</span></span>

<span data-ttu-id="4a2ec-204">Se è stata distribuita, fare clic su servizio web predittivo hello **distribuzione servizio Web [New]**, vedere [ripetere il training di un nuovo servizio web usando i cmdlet di Machine Learning Management hello](machine-learning-retrain-new-web-service-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="4a2ec-204">If you deployed hello predictive web service by clicking **Deploy Web Service [New]**, see [Retrain a New web service using hello Machine Learning Management cmdlets](machine-learning-retrain-new-web-service-using-powershell.md).</span></span>

<!-- Retrain a New web service using hello Machine Learning Management REST API -->


[1]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE01.png
[2]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE02.png
[3]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE03.png
[4]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE04.png
[5]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE05.png
[6]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE06.png
[7]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE07.png


<!-- Module References -->
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
