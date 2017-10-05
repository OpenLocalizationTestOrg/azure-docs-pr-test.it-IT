---
title: Ripetere il training dei modelli di Machine Learning a livello di codice | Documentazione Microsoft
description: Informazioni su come ripetere il training di un modello a livello di codice e aggiornare il servizio Web per l'uso del modello appena sottoposto a training in Azure Machine Learning.
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
ms.openlocfilehash: cf7a39e14a935d0d0e0df07e66a8f37480ec9687
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="retrain-machine-learning-models-programmatically"></a><span data-ttu-id="86a0e-103">Ripetere il training dei modelli di Machine Learning a livello di codice</span><span class="sxs-lookup"><span data-stu-id="86a0e-103">Retrain Machine Learning models programmatically</span></span>
<span data-ttu-id="86a0e-104">Questa procedura dettagliata descrive come ripetere il training di un servizio Web di Azure Machine Learning a livello di codice usando C# e il servizio Esecuzione batch di Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="86a0e-104">In this walkthrough, you will learn how to programmatically retrain an Azure Machine Learning Web Service using C# and the Machine Learning Batch Execution service.</span></span>

<span data-ttu-id="86a0e-105">Dopo aver ripetuto il training del modello, attenersi alle procedure dettagliate seguenti che descrivono come aggiornare il modello nel servizio Web predittivo:</span><span class="sxs-lookup"><span data-stu-id="86a0e-105">Once you have retrained the model, the following walkthroughs show how to update the model in your predictive web service:</span></span>

* <span data-ttu-id="86a0e-106">Se è stato distribuito un servizio Web classico nel portale dei servizi Web di Machine Learning, vedere [Ripetere il training di un servizio Web classico](machine-learning-retrain-a-classic-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="86a0e-106">If you deployed a Classic web service in the Machine Learning Web Services portal, see [Retrain a Classic web service](machine-learning-retrain-a-classic-web-service.md).</span></span> 
* <span data-ttu-id="86a0e-107">Se è stato distribuito un nuovo servizio Web, vedere [Ripetere il training di un nuovo servizio Web usando i cmdlet di gestione di Machine Learning](machine-learning-retrain-new-web-service-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="86a0e-107">If you deployed a New web service, see [Retrain a New web service using the Machine Learning Management cmdlets](machine-learning-retrain-new-web-service-using-powershell.md).</span></span>

<span data-ttu-id="86a0e-108">Per una panoramica del processo di ripetizione del training, vedere [Ripetere il training di un modello di Machine Learning](machine-learning-retrain-machine-learning-model.md).</span><span class="sxs-lookup"><span data-stu-id="86a0e-108">For an overview of the retraining process, see [Retrain a Machine Learning Model](machine-learning-retrain-machine-learning-model.md).</span></span>

<span data-ttu-id="86a0e-109">Se si vuole iniziare con il servizio Web esistente basato sul nuovo Azure Resource Manager, vedere [Retrain an existing Predictive web service](machine-learning-retrain-existing-resource-manager-based-web-service.md) (Ripetere il training di un servizio Web predittivo esistente).</span><span class="sxs-lookup"><span data-stu-id="86a0e-109">If you want to start with your existing New Azure Resource Manager based web service, see [Retrain an existing Predictive web service](machine-learning-retrain-existing-resource-manager-based-web-service.md).</span></span>

## <a name="create-a-training-experiment"></a><span data-ttu-id="86a0e-110">Creare un esperimento di training</span><span class="sxs-lookup"><span data-stu-id="86a0e-110">Create a training experiment</span></span>
<span data-ttu-id="86a0e-111">Per questo esempio, si userà "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset" che fa parte degli esempi di Microsoft Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="86a0e-111">For this example, you will use "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset" from the Microsoft Azure Machine Learning samples.</span></span> 

<span data-ttu-id="86a0e-112">Per creare l'esperimento:</span><span class="sxs-lookup"><span data-stu-id="86a0e-112">To create the experiment:</span></span>

1. <span data-ttu-id="86a0e-113">Accedere a Microsoft Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="86a0e-113">Sign into to Microsoft Azure Machine Learning Studio.</span></span> 
2. <span data-ttu-id="86a0e-114">Nell'angolo in basso a destra del dashboard fare clic su **New**(Nuovo).</span><span class="sxs-lookup"><span data-stu-id="86a0e-114">On the bottom right corner of the dashboard, click **New**.</span></span>
3. <span data-ttu-id="86a0e-115">Tra gli esempi di Microsoft selezionare l'esempio 5.</span><span class="sxs-lookup"><span data-stu-id="86a0e-115">From the Microsoft Samples, select Sample 5.</span></span>
4. <span data-ttu-id="86a0e-116">Per rinominare l'esperimento, nella parte superiore dell'area di disegno dell'esperimento selezionare il nome dell'esperimento "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset".</span><span class="sxs-lookup"><span data-stu-id="86a0e-116">To rename the experiment, at the top of the experiment canvas, select the experiment name "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset".</span></span>
5. <span data-ttu-id="86a0e-117">Digitare Census Model.</span><span class="sxs-lookup"><span data-stu-id="86a0e-117">Type Census Model.</span></span>
6. <span data-ttu-id="86a0e-118">Fare clic su **Run**(Esegui) nella parte inferiore dell'area di disegno dell'esperimento.</span><span class="sxs-lookup"><span data-stu-id="86a0e-118">At the bottom of the experiment canvas, click **Run**.</span></span>
7. <span data-ttu-id="86a0e-119">Fare clic su **Set Up Web service** (Configura servizio Web) e selezionare **Retraining Web service** (Servizio Web di ripetizione del training).</span><span class="sxs-lookup"><span data-stu-id="86a0e-119">Click **Set Up web service** and select **Retraining web service**.</span></span> 

<span data-ttu-id="86a0e-120">Di seguito viene illustrato l'esperimento iniziale.</span><span class="sxs-lookup"><span data-stu-id="86a0e-120">The following shows the initial experiment.</span></span>
   
   ![Esperimento iniziale.][2]


## <a name="create-a-predictive-experiment-and-publish-as-a-web-service"></a><span data-ttu-id="86a0e-122">Creare un esperimento predittivo e pubblicarlo come servizio Web</span><span class="sxs-lookup"><span data-stu-id="86a0e-122">Create a predictive experiment and publish as a web service</span></span>
<span data-ttu-id="86a0e-123">Ora viene creato un esperimento predicativo.</span><span class="sxs-lookup"><span data-stu-id="86a0e-123">Next you create a Predicative Experiment.</span></span>

1. <span data-ttu-id="86a0e-124">Nella parte inferiore dell'area di disegno dell'esperimento fare clic su **Set Up Web Service** (Configura servizio Web) e selezionare **Predictive Web Service** (Servizio Web predittivo).</span><span class="sxs-lookup"><span data-stu-id="86a0e-124">At the bottom of the experiment canvas, click **Set Up Web Service** and select **Predictive Web Service**.</span></span> <span data-ttu-id="86a0e-125">In questo modo, il modello verrà salvato come modello con training e verranno aggiunti i moduli di input e output del servizio Web.</span><span class="sxs-lookup"><span data-stu-id="86a0e-125">This saves the model as a Trained Model and adds web service Input and Output modules.</span></span> 
2. <span data-ttu-id="86a0e-126">Fare clic su **Run**.</span><span class="sxs-lookup"><span data-stu-id="86a0e-126">Click **Run**.</span></span> 
3. <span data-ttu-id="86a0e-127">Al termine dell'esecuzione dell'esperimento, fare clic su **Deploy Web Service [Classic]** (Distribuisci servizio Web [Classico]) o **Deploy Web Service [New]** (Distribuisci servizio Web [Nuovo]).</span><span class="sxs-lookup"><span data-stu-id="86a0e-127">After the experiment has finished running, click **Deploy Web Service [Classic]** or **Deploy Web Service [New]**.</span></span>

> [!NOTE] 
> <span data-ttu-id="86a0e-128">Per distribuire un nuovo servizio Web è necessario disporre delle autorizzazioni sufficienti nella sottoscrizione a cui si sta distribuendo il servizio Web.</span><span class="sxs-lookup"><span data-stu-id="86a0e-128">To deploy a New web service you must have sufficient permissions in the subscription to which you deploying the web service.</span></span> <span data-ttu-id="86a0e-129">Per altre informazioni, vedere [Gestire un servizio Web usando il portale dei servizi Web di Azure Machine Learning](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="86a0e-129">For more information see, [Manage a Web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

## <a name="deploy-the-training-experiment-as-a-training-web-service"></a><span data-ttu-id="86a0e-130">Distribuire l'esperimento di training come servizio Web di training</span><span class="sxs-lookup"><span data-stu-id="86a0e-130">Deploy the training experiment as a Training web service</span></span>
<span data-ttu-id="86a0e-131">Per ripetere il training del modello con training, è necessario distribuire l'esperimento di training creato come servizio Web di ripetizione del training.</span><span class="sxs-lookup"><span data-stu-id="86a0e-131">To retrain the trained model, you must deploy the training experiment that you created as a Retraining web service.</span></span> <span data-ttu-id="86a0e-132">Per produrre nuovi modelli con training, questo servizio Web necessita di un modulo *Web Service Output* connesso al modulo *[Train Model][train-model]*.</span><span class="sxs-lookup"><span data-stu-id="86a0e-132">This web service needs a *Web Service Output* module connected to the *[Train Model][train-model]* module, to be able to produce new trained models.</span></span>

1. <span data-ttu-id="86a0e-133">Per tornare all'esperimento di training, fare clic sull'icona Experiments (Esperimenti) nel riquadro sinistro e quindi sull'esperimento denominato Census Model.</span><span class="sxs-lookup"><span data-stu-id="86a0e-133">To return to the training experiment, click the Experiments icon in the left pane, then click the experiment named Census Model.</span></span>  
2. <span data-ttu-id="86a0e-134">Nella casella di ricerca Search Experiment Items (Cerca elementi esperimento) digitare Web service.</span><span class="sxs-lookup"><span data-stu-id="86a0e-134">In the Search Experiment Items search box, type web service.</span></span> 
3. <span data-ttu-id="86a0e-135">Trascinare un modulo *Web Service Input* (Input servizio Web) nell'area di disegno dell'esperimento e connetterne l'output al modulo *Clean Missing Data* (Pulisci dati mancanti).</span><span class="sxs-lookup"><span data-stu-id="86a0e-135">Drag a *Web Service Input* module onto the experiment canvas and connect its output to the *Clean Missing Data* module.</span></span>  <span data-ttu-id="86a0e-136">In questo modo, i dati di ripetizione del training vengono elaborati allo stesso modo dei dati di training originali.</span><span class="sxs-lookup"><span data-stu-id="86a0e-136">This ensures that your retraining data is processed the same way as your original training data.</span></span>
4. <span data-ttu-id="86a0e-137">Trascinare due moduli *Web service Output* (Output servizio Web) nell'area di disegno dell'esperimento.</span><span class="sxs-lookup"><span data-stu-id="86a0e-137">Drag two *web service Output* modules onto the experiment canvas.</span></span> <span data-ttu-id="86a0e-138">Connettere l'output del modulo *Train Model* (Modello di training) a un modulo e l'output del modulo *Evaluate Model* (Modello di valutazione) all'altro.</span><span class="sxs-lookup"><span data-stu-id="86a0e-138">Connect the output of the *Train Model* module to one and the output of the *Evaluate Model* module to the other.</span></span> <span data-ttu-id="86a0e-139">Con l'output del servizio Web per **Train Model** (Modello di training) è possibile ottenere il nuovo modello con training.</span><span class="sxs-lookup"><span data-stu-id="86a0e-139">The web service output for **Train Model** gives us the new trained model.</span></span> <span data-ttu-id="86a0e-140">L'output collegato al modulo **Evaluate Model** (Modello di valutazione) restituisce l'output del modulo, che corrisponde ai risultati sulle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="86a0e-140">The output attached to **Evaluate Model** returns that module’s output, which is the performance results.</span></span>
5. <span data-ttu-id="86a0e-141">Fare clic su **Run**.</span><span class="sxs-lookup"><span data-stu-id="86a0e-141">Click **Run**.</span></span> 

<span data-ttu-id="86a0e-142">Sarà quindi necessario distribuire l'esperimento di training come un servizio Web che produce un modello sottoposto a training e risultati di valutazione del modello.</span><span class="sxs-lookup"><span data-stu-id="86a0e-142">Next you must deploy the training experiment as a web service that produces a trained model and model evaluation results.</span></span> <span data-ttu-id="86a0e-143">A tale scopo, il set di azioni successivo dipende dall'uso di un servizio Web classico o di un nuovo servizio Web.</span><span class="sxs-lookup"><span data-stu-id="86a0e-143">To accomplish this, your next set of actions are dependent on whether you are working with a Classic web service or a New web service.</span></span>  

<span data-ttu-id="86a0e-144">**Servizio Web classico**</span><span class="sxs-lookup"><span data-stu-id="86a0e-144">**Classic web service**</span></span>

<span data-ttu-id="86a0e-145">Nella parte inferiore dell'area di disegno dell'esperimento fare clic su **Set Up Web Service** (Configura servizio Web) e selezionare **Deploy Web Service [Classic]** (Distribuisci servizio Web [Classico]).</span><span class="sxs-lookup"><span data-stu-id="86a0e-145">At the bottom of the experiment canvas, click **Set Up Web Service** and select **Deploy Web Service [Classic]**.</span></span> <span data-ttu-id="86a0e-146">Viene visualizzato il **Dashboard** del servizio Web con la chiave API e la pagina della guida dell'API per l'esecuzione batch.</span><span class="sxs-lookup"><span data-stu-id="86a0e-146">The Web Service **Dashboard** is displayed with the API Key and the API help page for Batch Execution.</span></span> <span data-ttu-id="86a0e-147">È possibile usare solo il metodo di esecuzione batch per la creazione di modelli di training.</span><span class="sxs-lookup"><span data-stu-id="86a0e-147">Only the Batch Execution method can be used for creating Trained Models.</span></span>

<span data-ttu-id="86a0e-148">**Nuovo servizio Web**</span><span class="sxs-lookup"><span data-stu-id="86a0e-148">**New web service**</span></span>

<span data-ttu-id="86a0e-149">Nella parte inferiore dell'area di disegno dell'esperimento fare clic su **Set Up Web Service** (Configura servizio Web) e selezionare **Deploy Web Service [New]** (Distribuisci servizio Web [Nuovo]).</span><span class="sxs-lookup"><span data-stu-id="86a0e-149">At the bottom of the experiment canvas, click **Set Up Web Service** and select **Deploy Web Service [New]**.</span></span> <span data-ttu-id="86a0e-150">Il portale dei servizi Web di Azure Machine Learning visualizzerà la pagina Deploy Web service (Distribuisci servizio Web).</span><span class="sxs-lookup"><span data-stu-id="86a0e-150">The Web Service Azure Machine Learning Web Services portal opens to the Deploy web service page.</span></span> <span data-ttu-id="86a0e-151">Digitare un nome per il servizio Web e scegliere un piano di pagamento, quindi fare clic su **Distribuisci**.</span><span class="sxs-lookup"><span data-stu-id="86a0e-151">Type a name for your web service and choose a payment plan, then click **Deploy**.</span></span> <span data-ttu-id="86a0e-152">È possibile usare solo il metodo di esecuzione batch per la creazione di modelli di training</span><span class="sxs-lookup"><span data-stu-id="86a0e-152">Only the Batch Execution method can be used for creating Trained Models</span></span>

<span data-ttu-id="86a0e-153">Al termine dell'esecuzione dell'esperimento, il flusso di lavoro sarà in ogni caso simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="86a0e-153">In either case, after experiment has completed running, the resulting workflow should look as follows:</span></span>

![Flusso di lavoro risultante dopo l'esecuzione.][4]



## <a name="retrain-the-model-with-new-data-using-bes"></a><span data-ttu-id="86a0e-155">Ripetere il training del modello con i nuovi dati usando BES</span><span class="sxs-lookup"><span data-stu-id="86a0e-155">Retrain the model with new data using BES</span></span>
<span data-ttu-id="86a0e-156">In questo esempio viene usato C# per creare l'applicazione di ripetizione del training.</span><span class="sxs-lookup"><span data-stu-id="86a0e-156">For this example, you are using C# to create the retraining application.</span></span> <span data-ttu-id="86a0e-157">Per eseguire questa attività, è anche possibile usare il codice di esempio Python o R.</span><span class="sxs-lookup"><span data-stu-id="86a0e-157">You can also use the Python or R sample code to accomplish this task.</span></span>

<span data-ttu-id="86a0e-158">Per chiamare le API per la ripetizione del training:</span><span class="sxs-lookup"><span data-stu-id="86a0e-158">To call the Retraining APIs:</span></span>

1. <span data-ttu-id="86a0e-159">Creare un'applicazione console C# in Visual Studio. A tale scopo, selezionare **Nuovo** > **Progetto** > **Visual C#** > **Desktop classico di Windows** > **Applicazione console (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="86a0e-159">Create a C# console application in Visual Studio: **New** > **Project** > **Visual C#** > **Windows Classic Desktop** > **Console App (.NET Framework)**.</span></span>
2. <span data-ttu-id="86a0e-160">Accedere al portale dei servizi Web di Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="86a0e-160">Sign in to the Machine Learning Web Service portal.</span></span>
3. <span data-ttu-id="86a0e-161">Se si usa un servizio Web classico, fare clic su **Classic Web Services**(Servizi Web classici).</span><span class="sxs-lookup"><span data-stu-id="86a0e-161">If you are working with a Classic web service, click **Classic Web Services**.</span></span>
   1. <span data-ttu-id="86a0e-162">Fare clic sul servizio Web in uso.</span><span class="sxs-lookup"><span data-stu-id="86a0e-162">Click the web service you are working with.</span></span>
   2. <span data-ttu-id="86a0e-163">Fare clic sull'endpoint predefinito.</span><span class="sxs-lookup"><span data-stu-id="86a0e-163">Click the default endpoint.</span></span>
   3. <span data-ttu-id="86a0e-164">Fare clic su **Consume**(Uso).</span><span class="sxs-lookup"><span data-stu-id="86a0e-164">Click **Consume**.</span></span>
   4. <span data-ttu-id="86a0e-165">Nella sezione **Sample Code** (Codice di esempio) nella parte inferiore della pagina **Consume** (Uso) fare clic su **Batch**.</span><span class="sxs-lookup"><span data-stu-id="86a0e-165">At the bottom of the **Consume** page, in the **Sample Code** section, click **Batch**.</span></span>
   5. <span data-ttu-id="86a0e-166">Procedere al passaggio 5 di questa procedura.</span><span class="sxs-lookup"><span data-stu-id="86a0e-166">Continue to step 5 of this procedure.</span></span>
4. <span data-ttu-id="86a0e-167">Se si usa un nuovo servizio Web, fare clic su **Servizi Web**.</span><span class="sxs-lookup"><span data-stu-id="86a0e-167">If you are working with a New web service, click **Web Services**.</span></span>
   1. <span data-ttu-id="86a0e-168">Fare clic sul servizio Web in uso.</span><span class="sxs-lookup"><span data-stu-id="86a0e-168">Click the web service you are working with.</span></span>
   2. <span data-ttu-id="86a0e-169">Fare clic su **Consume**(Uso).</span><span class="sxs-lookup"><span data-stu-id="86a0e-169">Click **Consume**.</span></span>
   3. <span data-ttu-id="86a0e-170">Nella sezione **Sample Code** (Codice di esempio) nella parte inferiore della pagina Consume (Uso) fare clic su **Batch**.</span><span class="sxs-lookup"><span data-stu-id="86a0e-170">At the bottom of the Consume page, in the **Sample Code** section, click **Batch**.</span></span>
5. <span data-ttu-id="86a0e-171">Copiare il codice C# di esempio per l'esecuzione batch e incollarlo nel file Program.cs, verificando che lo spazio dei nomi rimanga invariato.</span><span class="sxs-lookup"><span data-stu-id="86a0e-171">Copy the sample C# code for batch execution and paste it into the Program.cs file, making sure the namespace remains intact.</span></span>

<span data-ttu-id="86a0e-172">Aggiungere il pacchetto NuGet Microsoft.AspNet.WebApi.Client come specificato nei commenti.</span><span class="sxs-lookup"><span data-stu-id="86a0e-172">Add the Nuget package Microsoft.AspNet.WebApi.Client as specified in the comments.</span></span> <span data-ttu-id="86a0e-173">Per aggiungere il riferimento a Microsoft.WindowsAzure.Storage.dll, potrebbe essere prima necessario installare la libreria client per i servizi di archiviazione di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="86a0e-173">To add the reference to Microsoft.WindowsAzure.Storage.dll, you might first need to install the client library for Microsoft Azure storage services.</span></span> <span data-ttu-id="86a0e-174">Per altre informazioni, vedere i [servizi di archiviazione Windows](https://www.nuget.org/packages/WindowsAzure.Storage).</span><span class="sxs-lookup"><span data-stu-id="86a0e-174">For more information, see [Windows Storage Services](https://www.nuget.org/packages/WindowsAzure.Storage).</span></span>

### <a name="update-the-apikey-declaration"></a><span data-ttu-id="86a0e-175">Aggiornare la dichiarazione apikey</span><span class="sxs-lookup"><span data-stu-id="86a0e-175">Update the apikey declaration</span></span>
<span data-ttu-id="86a0e-176">Individuare la dichiarazione **apikey** .</span><span class="sxs-lookup"><span data-stu-id="86a0e-176">Locate the **apikey** declaration.</span></span>

    const string apiKey = "abc123"; // Replace this with the API key for the web service

<span data-ttu-id="86a0e-177">Nella sezione **Basic consumption info** (Informazioni di base sul consumo) della pagina **Consume** (Uso) individuare la chiave primaria e copiarla nella dichiarazione **apikey**.</span><span class="sxs-lookup"><span data-stu-id="86a0e-177">In the **Basic consumption info** section of the **Consume** page, locate the primary key and copy it to the **apikey** declaration.</span></span>

### <a name="update-the-azure-storage-information"></a><span data-ttu-id="86a0e-178">Aggiornare le informazioni di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="86a0e-178">Update the Azure Storage information</span></span>
<span data-ttu-id="86a0e-179">Il codice di esempio BES carica un file da un'unità locale (ad esempio, "C:\temp\CensusIpnput.csv") in Archiviazione di Azure, lo elabora e scrive i risultati in Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="86a0e-179">The BES sample code uploads a file from a local drive (For example "C:\temp\CensusIpnput.csv") to Azure Storage, processes it, and writes the results back to Azure Storage.</span></span>  

<span data-ttu-id="86a0e-180">Per eseguire questa attività è necessario recuperare il nome dell'account di archiviazione, la chiave e le informazioni sul per l'account di archiviazione dal portale di Azure classico e quindi aggiornare i valori corrispondenti nel codice.</span><span class="sxs-lookup"><span data-stu-id="86a0e-180">To accomplish this task, you must retrieve the Storage account name, key, and container information for your Storage account from the classic Azure portal and the update corresponding values in the code.</span></span> 

1. <span data-ttu-id="86a0e-181">Accedere al portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="86a0e-181">Sign in to the classic Azure portal.</span></span>
2. <span data-ttu-id="86a0e-182">Nella colonna di spostamento a sinistra fare clic su **Archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="86a0e-182">In the left navigation column, click **Storage**.</span></span>
3. <span data-ttu-id="86a0e-183">Nell'elenco degli account di archiviazione selezionarne uno per l'archiviazione del modello per il quale è stato ripetuto il training.</span><span class="sxs-lookup"><span data-stu-id="86a0e-183">From the list of storage accounts, select one to store the retrained model.</span></span>
4. <span data-ttu-id="86a0e-184">Nella parte inferiore della pagina fare clic su **Gestisci chiavi di accesso**.</span><span class="sxs-lookup"><span data-stu-id="86a0e-184">At the bottom of the page, click **Manage Access Keys**.</span></span>
5. <span data-ttu-id="86a0e-185">Copiare e salvare la **chiave di accesso primaria** , quindi chiudere la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="86a0e-185">Copy and save the **Primary Access Key** and close the dialog.</span></span> 
6. <span data-ttu-id="86a0e-186">Nella parte superiore della pagina fare clic su **Contenitori**.</span><span class="sxs-lookup"><span data-stu-id="86a0e-186">At the top of the page, click **Containers**.</span></span>
7. <span data-ttu-id="86a0e-187">Selezionare un contenitore esistente oppure crearne uno nuovo e salvare il nome.</span><span class="sxs-lookup"><span data-stu-id="86a0e-187">Select an existing container or create a new one and save the name.</span></span>

<span data-ttu-id="86a0e-188">Individuare le dichiarazioni *StorageAccountName*, *StorageAccountKey* e *StorageContainerName* e aggiornare i valori salvati dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="86a0e-188">Locate the *StorageAccountName*, *StorageAccountKey*, and *StorageContainerName* declarations and update the values you saved from the Azure portal.</span></span>

    const string StorageAccountName = "mystorageacct"; // Replace this with your Azure Storage Account name
    const string StorageAccountKey = "a_storage_account_key"; // Replace this with your Azure Storage Key
    const string StorageContainerName = "mycontainer"; // Replace this with your Azure Storage Container name

<span data-ttu-id="86a0e-189">È necessario anche assicurarsi che il file di input sia disponibile nella posizione specificata nel codice.</span><span class="sxs-lookup"><span data-stu-id="86a0e-189">You also must ensure the input file is available at the location you specify in the code.</span></span> 

### <a name="specify-the-output-location"></a><span data-ttu-id="86a0e-190">Specificare il percorso di output</span><span class="sxs-lookup"><span data-stu-id="86a0e-190">Specify the output location</span></span>
<span data-ttu-id="86a0e-191">Quando si specifica il percorso di output nel payload della richiesta, l'estensione del file specificata in *RelativeLocation* deve essere indicata come ilearner.</span><span class="sxs-lookup"><span data-stu-id="86a0e-191">When specifying the output location in the Request Payload, the extension of the file specified in *RelativeLocation* must be specified as ilearner.</span></span> 

<span data-ttu-id="86a0e-192">Vedere l'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="86a0e-192">See the following example:</span></span>

    Outputs = new Dictionary<string, AzureBlobDataReference>() {
        {
            "output1",
            new AzureBlobDataReference()
            {
                ConnectionString = storageConnectionString,
                RelativeLocation = string.Format("{0}/output1results.ilearner", StorageContainerName) /*Replace this with the location you would like to use for your output file, and valid file extension (usually .csv for scoring results, or .ilearner for trained models)*/
            }
        },

> [!NOTE]
> <span data-ttu-id="86a0e-193">I nomi dei percorsi di output possono essere diversi da quelli di questa procedura dettagliata a seconda dell'ordine in cui sono stati aggiunti i moduli di output del servizio Web.</span><span class="sxs-lookup"><span data-stu-id="86a0e-193">The names of your output locations may be different from the ones in this walkthrough based on the order in which you added the web service output modules.</span></span> <span data-ttu-id="86a0e-194">Dato che questo esperimento di training è stato configurato con due output, i risultati includono le informazioni sul percorso di archiviazione per entrambi.</span><span class="sxs-lookup"><span data-stu-id="86a0e-194">Since you set up this training experiment with two outputs, the results include storage location information for both of them.</span></span>  
> 
> 

![Output della ripetizione del training.][6]

<span data-ttu-id="86a0e-196">Diagramma 4: output della ripetizione del training.</span><span class="sxs-lookup"><span data-stu-id="86a0e-196">Diagram 4: Retraining output.</span></span>

## <a name="evaluate-the-retraining-results"></a><span data-ttu-id="86a0e-197">Valutare i risultati della ripetizione del training</span><span class="sxs-lookup"><span data-stu-id="86a0e-197">Evaluate the Retraining Results</span></span>
<span data-ttu-id="86a0e-198">Quando si esegue l'applicazione, l'output include l'URL e il token di firma di accesso condiviso necessari per accedere ai risultati della valutazione.</span><span class="sxs-lookup"><span data-stu-id="86a0e-198">When you run the application, the output includes the URL and SAS token necessary to access the evaluation results.</span></span>

<span data-ttu-id="86a0e-199">È possibile visualizzare i risultati sulle prestazioni del modello sottoposto nuovamente a training combinando *BaseLocation*, *RelativeLocation* e *SasBlobToken* dai risultati di output per *output2* (come mostrato nell'immagine precedente dell'output della ripetizione del training) e incollando l'URL completo nella barra degli indirizzi del browser.</span><span class="sxs-lookup"><span data-stu-id="86a0e-199">You can see the performance results of the retrained model by combining the *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from the output results for *output2* (as shown in the preceding retraining output image) and pasting the complete URL in the browser address bar.</span></span>  

<span data-ttu-id="86a0e-200">Esaminare i risultati per determinare se le prestazioni del modello appena sottoposto a training sono abbastanza elevate da sostituire quello esistente.</span><span class="sxs-lookup"><span data-stu-id="86a0e-200">Examine the results to determine whether the newly trained model performs well enough to replace the existing one.</span></span>

<span data-ttu-id="86a0e-201">Copiare *BaseLocation*, *RelativeLocation* e *SasBlobToken* dai risultati di output. Verranno usati durante il processo di ripetizione del training.</span><span class="sxs-lookup"><span data-stu-id="86a0e-201">Copy the *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from the output results, you will use them during the retraining process.</span></span>

## <a name="next-steps"></a><span data-ttu-id="86a0e-202">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="86a0e-202">Next steps</span></span>
<span data-ttu-id="86a0e-203">Se è stato distribuito il servizio Web predittivo facendo clic su **Deploy Web Service [Classic]** (Distribuisci servizio Web [Classico]), vedere [Ripetere il training di un servizio Web classico](machine-learning-retrain-a-classic-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="86a0e-203">If you deployed the predictive web service by clicking **Deploy Web Service [Classic]**, see [Retrain a Classic web service](machine-learning-retrain-a-classic-web-service.md).</span></span>

<span data-ttu-id="86a0e-204">Se è stato distribuito un nuovo servizio Web facendo clic su **Deploy Web Service [New]** (Distribuisci servizio Web [Nuovo]), vedere [Ripetere il training di un nuovo servizio Web usando i cmdlet di gestione di Machine Learning](machine-learning-retrain-new-web-service-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="86a0e-204">If you deployed the predictive web service by clicking **Deploy Web Service [New]**, see [Retrain a New web service using the Machine Learning Management cmdlets](machine-learning-retrain-new-web-service-using-powershell.md).</span></span>

<!-- Retrain a New web service using the Machine Learning Management REST API -->


[1]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE01.png
[2]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE02.png
[3]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE03.png
[4]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE04.png
[5]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE05.png
[6]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE06.png
[7]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE07.png


<!-- Module References -->
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
