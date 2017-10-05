---
title: "Creare più modelli da un esperimento | Documentazione Microsoft"
description: "Usare PowerShell per creare più modelli di Machine Learning ed endpoint di servizio Web con lo stesso algoritmo ma con set di dati di training diversi."
services: machine-learning
documentationcenter: 
author: hning86
manager: jhubbard
editor: cgronlun
ms.assetid: 1076b8eb-5a0d-4ac5-8601-8654d9be229f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: garye;haining
ms.openlocfilehash: 21d8c1ee0877df8d317d5a14131dc574fa5303c4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="create-many-machine-learning-models-and-web-service-endpoints-from-one-experiment-using-powershell"></a><span data-ttu-id="7f70a-103">Creare più modelli di Machine Learning ed endpoint di servizio Web da un esperimento usando PowerShell</span><span class="sxs-lookup"><span data-stu-id="7f70a-103">Create many Machine Learning models and web service endpoints from one experiment using PowerShell</span></span>
<span data-ttu-id="7f70a-104">In uno scenario di apprendimento automatico comune, si potrebbe voler creare più modelli che usano lo stesso flusso di lavoro di training e lo stesso algoritmo, ma con set di dati di training diversi come input.</span><span class="sxs-lookup"><span data-stu-id="7f70a-104">Here's a common machine learning problem: You want to create many models that have the same training workflow and use the same algorithm, but have different training datasets as input.</span></span> <span data-ttu-id="7f70a-105">Questo articolo illustra come eseguire questa operazione su larga scala in Azure Machine Learning Studio usando un singolo esperimento.</span><span class="sxs-lookup"><span data-stu-id="7f70a-105">This article shows you how to do this at scale in Azure Machine Learning Studio using just a single experiment.</span></span>

<span data-ttu-id="7f70a-106">Si supponga, ad esempio, di essere proprietari di un franchising globale di noleggio di biciclette.</span><span class="sxs-lookup"><span data-stu-id="7f70a-106">For example, let's say you own a global bike rental franchise business.</span></span> <span data-ttu-id="7f70a-107">Si vuole compilare un modello di regressione per prevedere la domanda di noleggio in base ai dati storici.</span><span class="sxs-lookup"><span data-stu-id="7f70a-107">You want to build a regression model to predict the rental demand based on historic data.</span></span> <span data-ttu-id="7f70a-108">Sono disponibili 1.000 punti di noleggio in tutto il mondo, per ognuno dei quali è stato raccolto un set di dati che include funzionalità importanti, come data, ora, meteo e traffico, specifiche per ogni località.</span><span class="sxs-lookup"><span data-stu-id="7f70a-108">You have 1,000 rental locations across the world and you've collected a dataset for each location that includes important features such as date, time, weather, and traffic that are specific to each location.</span></span>

<span data-ttu-id="7f70a-109">Si potrebbe eseguire il training del modello una sola volta usando una versione unita di tutti i set di dati di tutte le località.</span><span class="sxs-lookup"><span data-stu-id="7f70a-109">You could train your model once using a merged version of all the datasets across all locations.</span></span> <span data-ttu-id="7f70a-110">Ma dal momento che ogni località ha un ambiente unico, è preferibile eseguire il training del modello di regressione separatamente usando i set di dati delle singole località.</span><span class="sxs-lookup"><span data-stu-id="7f70a-110">But because each of your locations has a unique environment, a better approach would be to train your regression model separately using the dataset for each location.</span></span> <span data-ttu-id="7f70a-111">In questo modo, ogni modello di cui è stato eseguito il training terrà conto delle diverse caratteristiche, quali dimensioni del negozio, volume, posizione geografica, popolazione, traffico compatibile con le biciclette *e così via*.</span><span class="sxs-lookup"><span data-stu-id="7f70a-111">That way, each trained model could take into account the different store sizes, volume, geography, population, bike-friendly traffic environment, *etc.*.</span></span>

<span data-ttu-id="7f70a-112">Questo potrebbe essere l'approccio migliore, ma creare 1.000 esperimenti di training in Azure Machine Learning che rappresentano le singole località non è molto pratico.</span><span class="sxs-lookup"><span data-stu-id="7f70a-112">That may be the best approach, but you don't want to create 1,000 training experiments in Azure Machine Learning with each one representing a unique location.</span></span> <span data-ttu-id="7f70a-113">Oltre a essere un'attività piuttosto complessa, è anche inefficiente perché ogni esperimento avrà gli stessi componenti ad eccezione del set di dati di training.</span><span class="sxs-lookup"><span data-stu-id="7f70a-113">Besides being an overwhelming task, it's also seems pretty inefficient since each experiment would have all the same components except for the training dataset.</span></span>

<span data-ttu-id="7f70a-114">Per fortuna, l'[API di ripetizione del training di Azure Machine Learning](machine-learning-retrain-models-programmatically.md) permette di eseguire questa operazione, automatizzando l'attività con [Azure Machine Learning PowerShell](machine-learning-powershell-module.md).</span><span class="sxs-lookup"><span data-stu-id="7f70a-114">Fortunately, we can accomplish this by using the [Azure Machine Learning retraining API](machine-learning-retrain-models-programmatically.md) and automating the task with [Azure Machine Learning PowerShell](machine-learning-powershell-module.md).</span></span>

> [!NOTE]
> <span data-ttu-id="7f70a-115">Per eseguire l'esempio più velocemente, il numero di località verrà ridotto da 1.000 a 10,</span><span class="sxs-lookup"><span data-stu-id="7f70a-115">To make our sample run faster, we'll reduce the number of locations from 1,000 to 10.</span></span> <span data-ttu-id="7f70a-116">ma gli stessi principi e procedure si applicano anche a 1.000 località.</span><span class="sxs-lookup"><span data-stu-id="7f70a-116">But the same principles and procedures apply to 1,000 locations.</span></span> <span data-ttu-id="7f70a-117">L'unica differenza è che per eseguire il training di 1.000 set di dati è consigliabile eseguire in parallelo lo script di PowerShell riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="7f70a-117">The only difference is that if you want to train from 1,000 datasets you probably want to think of running the following PowerShell scripts in parallel.</span></span> <span data-ttu-id="7f70a-118">Come eseguire questa operazione non rientra nell'ambito di questo articolo, ma in Internet è possibile trovare esempi di multithreading con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7f70a-118">How to do that is beyond the scope of this article, but you can find examples of PowerShell multi-threading on the Internet.</span></span>  
> 
> 

## <a name="set-up-the-training-experiment"></a><span data-ttu-id="7f70a-119">Configurare l'esperimento di training</span><span class="sxs-lookup"><span data-stu-id="7f70a-119">Set up the training experiment</span></span>
<span data-ttu-id="7f70a-120">In questo articolo viene usato un [esperimento di training](https://gallery.cortanaintelligence.com/Experiment/Bike-Rental-Training-Experiment-1) di esempio creato in [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="7f70a-120">We're going to use an example [training experiment](https://gallery.cortanaintelligence.com/Experiment/Bike-Rental-Training-Experiment-1) that we've already created in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="7f70a-121">Aprire l'esperimento nell'area di lavoro di [Azure Machine Learning Studio](https://studio.azureml.net) .</span><span class="sxs-lookup"><span data-stu-id="7f70a-121">Open this experiment in your [Azure Machine Learning Studio](https://studio.azureml.net) workspace.</span></span>

> [!NOTE]
> <span data-ttu-id="7f70a-122">Per poter proseguire con l'esempio è consigliabile usare un'area di lavoro standard anziché una gratuita.</span><span class="sxs-lookup"><span data-stu-id="7f70a-122">In order to follow along with this example, you may want to use a standard workspace rather than a free workspace.</span></span> <span data-ttu-id="7f70a-123">Verrà creato un endpoint per ogni cliente, per un totale di 10 endpoint, e questo richiede l'uso di un'area di lavoro standard. Le aree di lavoro gratuite hanno un limite di tre endpoint.</span><span class="sxs-lookup"><span data-stu-id="7f70a-123">We'll be creating one endpoint for each customer - for a total of 10 endpoints - and that will require a standard workspace since a free workspace is limited to 3 endpoints.</span></span> <span data-ttu-id="7f70a-124">Se è disponibile soltanto un'area di lavoro gratuita, è sufficiente modificare gli script riportati di seguito in base a tre località.</span><span class="sxs-lookup"><span data-stu-id="7f70a-124">If you only have a free workspace, just modify the scripts below to allow for only 3 locations.</span></span>
> 
> 

<span data-ttu-id="7f70a-125">L’esperimento utilizza un modulo **Import Data** per importare il set di dati di training *customer001.csv* da un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="7f70a-125">The experiment uses an **Import Data** module to import the training dataset *customer001.csv* from an Azure storage account.</span></span> <span data-ttu-id="7f70a-126">Si supponga di aver raccolto i set di dati di training da tutti i punti di noleggio di biciclette e di averli archiviati nello stesso archivio BLOB con nomi di file da *rentalloc001.csv* a *rentalloc10.csv*.</span><span class="sxs-lookup"><span data-stu-id="7f70a-126">Let's assume we have collected training datasets from all bike rental locations and stored them in the same blob storage location with file names ranging from *rentalloc001.csv* to *rentalloc10.csv*.</span></span>

![immagine](./media/machine-learning-create-models-and-endpoints-with-powershell/reader-module.png)

<span data-ttu-id="7f70a-128">Si noti che al modulo **Train Model** (Modello di training) è stato aggiunto un modulo **Web service output** (Output servizio Web).</span><span class="sxs-lookup"><span data-stu-id="7f70a-128">Note that a **Web Service Output** module has been added to the **Train Model** module.</span></span>
<span data-ttu-id="7f70a-129">Quando l'esperimento viene distribuito come servizio Web, l'endpoint associato a tale output restituisce il modello di cui è stato eseguito il training come file con estensione ilearner.</span><span class="sxs-lookup"><span data-stu-id="7f70a-129">When this experiment is deployed as a web service, the endpoint associated with that output will return the trained model in the format of a .ilearner file.</span></span>

<span data-ttu-id="7f70a-130">Si noti anche che viene impostato un parametro del servizio Web per l'URL utilizzato dal modulo **Import Data** .</span><span class="sxs-lookup"><span data-stu-id="7f70a-130">Also note that we set up a web service parameter for the URL that the **Import Data** module uses.</span></span> <span data-ttu-id="7f70a-131">Questo permette di usare il parametro per specificare singoli set di dati di training per eseguire il training del modello per ogni località.</span><span class="sxs-lookup"><span data-stu-id="7f70a-131">This allows us to use the parameter to specify individual training datasets to train the model for each location.</span></span>
<span data-ttu-id="7f70a-132">Questa stessa operazione può essere eseguita in altri modi, ad esempio usando una query SQL con un parametro del servizio Web per ottenere dati da un database SQL di Azure o semplicemente un modulo **Web service input** (Input servizio Web) per passare un set di dati al servizio Web.</span><span class="sxs-lookup"><span data-stu-id="7f70a-132">There are other ways we could have done this, such as using a SQL query with a web service parameter to get data from a SQL Azure database, or simply using a  **Web Service Input** module to pass in a dataset to the web service.</span></span>

![immagine](./media/machine-learning-create-models-and-endpoints-with-powershell/web-service-output.png)

<span data-ttu-id="7f70a-134">Provare a eseguire l'esperimento di training usando il valore predefinito *rental001.csv* come set di dati di training.</span><span class="sxs-lookup"><span data-stu-id="7f70a-134">Now, let's run this training experiment using the default value *rental001.csv* as the training dataset.</span></span> <span data-ttu-id="7f70a-135">Fare clic sull'output del modulo **Evaluate** (Valuta) e selezionare **Visualizza** (Visualizza) per vedere che è stata ottenuta una prestazione soddisfacente di *AUC* = 0,91.</span><span class="sxs-lookup"><span data-stu-id="7f70a-135">If you view the output of the **Evaluate** module (click the output and select **Visualize**), you can see we get a decent performance of *AUC* = 0.91.</span></span> <span data-ttu-id="7f70a-136">A questo punto è possibile distribuire un servizio Web basato su questo esperimento di training.</span><span class="sxs-lookup"><span data-stu-id="7f70a-136">At this point, we're ready to deploy a web service out of this training experiment.</span></span>

## <a name="deploy-the-training-and-scoring-web-services"></a><span data-ttu-id="7f70a-137">Distribuire il training e assegnare punteggi ai servizi Web</span><span class="sxs-lookup"><span data-stu-id="7f70a-137">Deploy the training and scoring web services</span></span>
<span data-ttu-id="7f70a-138">Per distribuire il servizio Web di training, fare clic sul pulsante **Set Up Web Service** (Configura servizio Web) sotto l'area di disegno dell'esperimento e selezionare **Deploy Web Service** (Distribuisci servizio Web).</span><span class="sxs-lookup"><span data-stu-id="7f70a-138">To deploy the training web service, click the **Set Up Web Service** button below the experiment canvas and select **Deploy Web Service**.</span></span> <span data-ttu-id="7f70a-139">Denominare il servizio Web "Bike Rental Training".</span><span class="sxs-lookup"><span data-stu-id="7f70a-139">Call this web service ""Bike Rental Training".</span></span>

<span data-ttu-id="7f70a-140">Ora è necessario distribuire il servizio Web di attribuzione dei punteggi.</span><span class="sxs-lookup"><span data-stu-id="7f70a-140">Now we need to deploy the scoring web service.</span></span>
<span data-ttu-id="7f70a-141">A tale scopo, è possibile fare clic su **Set Up Web Service** (Configura servizio Web) sotto l'area di disegno e selezionare **Predictive Web Service** (Servizio Web predittivo).</span><span class="sxs-lookup"><span data-stu-id="7f70a-141">To do this, we can click **Set Up Web Service** below the canvas and select **Predictive Web Service**.</span></span> <span data-ttu-id="7f70a-142">Verrà creato un esperimento di assegnazione dei punteggi.</span><span class="sxs-lookup"><span data-stu-id="7f70a-142">This creates a scoring experiment.</span></span>
<span data-ttu-id="7f70a-143">È necessario apportare alcune piccole modifiche per consentire il funzionamento come servizio Web, ad esempio rimuovere la colonna etichetta "cnt" dai dati di input e limitare l'output all'ID istanza e al valore stimato corrispondente.</span><span class="sxs-lookup"><span data-stu-id="7f70a-143">We'll need to make a few minor adjustments to make it work as a web service, such as removing the label column "cnt" from the input data and limiting the output to only the instance id and the corresponding predicted value.</span></span>

<span data-ttu-id="7f70a-144">Per comodità è possibile aprire l' [esperimento predittivo](https://gallery.cortanaintelligence.com/Experiment/Bike-Rental-Predicative-Experiment-1) che è stato preparato nella raccolta.</span><span class="sxs-lookup"><span data-stu-id="7f70a-144">To save yourself that work, you can simply open the [predictive experiment](https://gallery.cortanaintelligence.com/Experiment/Bike-Rental-Predicative-Experiment-1) in the Gallery that's already been prepared.</span></span>

<span data-ttu-id="7f70a-145">Per distribuire il servizio Web eseguire l'esperimento predittivo, quindi fare clic sul pulsante **Deploy Web Service** sotto l'area di disegno.</span><span class="sxs-lookup"><span data-stu-id="7f70a-145">To deploy the web service, run the predictive experiment, then click the **Deploy Web Service** button below the canvas.</span></span> <span data-ttu-id="7f70a-146">Denominare il servizio Web di attribuzione dei punteggi "Bike Rental Scoring".</span><span class="sxs-lookup"><span data-stu-id="7f70a-146">Name the scoring web service "Bike Rental Scoring"".</span></span>

## <a name="create-10-identical-web-service-endpoints-with-powershell"></a><span data-ttu-id="7f70a-147">Creare 10 endpoint di servizio Web identici con PowerShell</span><span class="sxs-lookup"><span data-stu-id="7f70a-147">Create 10 identical web service endpoints with PowerShell</span></span>
<span data-ttu-id="7f70a-148">Questo servizio Web include un endpoint predefinito,</span><span class="sxs-lookup"><span data-stu-id="7f70a-148">This web service comes with a default endpoint.</span></span> <span data-ttu-id="7f70a-149">che però non viene usato in questo esempio perché non può essere aggiornato.</span><span class="sxs-lookup"><span data-stu-id="7f70a-149">But we're not as interested in the default endpoint since it can't be updated.</span></span> <span data-ttu-id="7f70a-150">È quindi necessario creare altri 10 endpoint, uno per ogni località.</span><span class="sxs-lookup"><span data-stu-id="7f70a-150">What we need to do is to create 10 additional endpoints, one for each location.</span></span> <span data-ttu-id="7f70a-151">A tale scopo, usare PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7f70a-151">We'll do this with PowerShell.</span></span>

<span data-ttu-id="7f70a-152">Configurare l'ambiente PowerShell:</span><span class="sxs-lookup"><span data-stu-id="7f70a-152">First, we set up our PowerShell environment:</span></span>

    Import-Module .\AzureMLPS.dll
    # Assume the default configuration file exists and is properly set to point to the valid Workspace.
    $scoringSvc = Get-AmlWebService | where Name -eq 'Bike Rental Scoring'
    $trainingSvc = Get-AmlWebService | where Name -eq 'Bike Rental Training'

<span data-ttu-id="7f70a-153">Quindi, eseguire il comando di PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="7f70a-153">Then, run the following PowerShell command:</span></span>

    # Create 10 endpoints on the scoring web service.
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        Write-Host ('adding endpoint ' + $endpointName + '...')
        Add-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -Description $endpointName     
    }

<span data-ttu-id="7f70a-154">I 10 endpoint appena creati contengono tutti lo stesso modello di cui è stato eseguito il training sul set di dati *customer001.csv*.</span><span class="sxs-lookup"><span data-stu-id="7f70a-154">Now we've created 10 endpoints and they all contain the same trained model trained on *customer001.csv*.</span></span> <span data-ttu-id="7f70a-155">Per visualizzarli è possibile usare il portale di gestione di Azure.</span><span class="sxs-lookup"><span data-stu-id="7f70a-155">You can view them in the Azure Management Portal.</span></span>

![immagine](./media/machine-learning-create-models-and-endpoints-with-powershell/created-endpoints.png)

## <a name="update-the-endpoints-to-use-separate-training-datasets-using-powershell"></a><span data-ttu-id="7f70a-157">Aggiornare gli endpoint per l'uso di set di dati di training separati tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="7f70a-157">Update the endpoints to use separate training datasets using PowerShell</span></span>
<span data-ttu-id="7f70a-158">Il passaggio successivo consiste nell'aggiornare gli endpoint con i modelli di cui è stato eseguito il training univoco sui dati dei singoli clienti.</span><span class="sxs-lookup"><span data-stu-id="7f70a-158">The next step is to update the endpoints with models uniquely trained on each customer's individual data.</span></span> <span data-ttu-id="7f70a-159">Prima, però, è necessario produrre tali modelli dal servizio Web **Bike Rental Training** .</span><span class="sxs-lookup"><span data-stu-id="7f70a-159">But first we need to produce these models from the **Bike Rental Training** web service.</span></span> <span data-ttu-id="7f70a-160">Tornare al servizio Web **Bike Rental Training** .</span><span class="sxs-lookup"><span data-stu-id="7f70a-160">Let's go back to the **Bike Rental Training** web service.</span></span> <span data-ttu-id="7f70a-161">È necessario chiamare 10 volte il relativo endpoint BES con 10 set di dati di training diversi per produrre 10 modelli differenti.</span><span class="sxs-lookup"><span data-stu-id="7f70a-161">We need to call its BES endpoint 10 times with 10 different training datasets in order to produce 10 different models.</span></span> <span data-ttu-id="7f70a-162">A tale scopo, usare il cmdlet **InovkeAmlWebServiceBESEndpoint** di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7f70a-162">We'll use the **InovkeAmlWebServiceBESEndpoint** PowerShell cmdlet to do this.</span></span>

<span data-ttu-id="7f70a-163">È inoltre necessario fornire le credenziali per l'account di archiviazione BLOB in `$configContent`, ovvero i campi `AccountName`, `AccountKey` e `RelativeLocation`.</span><span class="sxs-lookup"><span data-stu-id="7f70a-163">You will also need to provide credentials for your blob storage account into `$configContent`, namely, at the fields `AccountName`, `AccountKey` and `RelativeLocation`.</span></span> <span data-ttu-id="7f70a-164">`AccountName` può essere uno dei nomi di account, come illustrato nel **portale di gestione di Azure classico** (scheda*Archiviazione* ).</span><span class="sxs-lookup"><span data-stu-id="7f70a-164">The `AccountName` can be one of your account names, as seen in the **Classic Azure Management Portal** (*Storage* tab).</span></span> <span data-ttu-id="7f70a-165">Dopo avere fatto clic su un account di archiviazione,è possibile trovare il relativo `AccountKey` scegliendo il pulsante **Gestisci chiavi di accesso** nella parte inferiore e copiando il valore di *Chiave di accesso primaria*.</span><span class="sxs-lookup"><span data-stu-id="7f70a-165">Once you click on a storage account, its `AccountKey` can be found by pressing the **Manage Access Keys** button at the bottom and copying the *Primary Access Key*.</span></span> <span data-ttu-id="7f70a-166">`RelativeLocation` è il percorso relativo della risorsa di archiviazione in cui verrà archiviato un nuovo modello.</span><span class="sxs-lookup"><span data-stu-id="7f70a-166">The `RelativeLocation` is the path relative to your storage where a new model will be stored.</span></span> <span data-ttu-id="7f70a-167">Ad esempio, il percorso `hai/retrain/bike_rental/` nello script seguente punta a un contenitore denominato `hai` e `/retrain/bike_rental/` sono le sottocartelle.</span><span class="sxs-lookup"><span data-stu-id="7f70a-167">For instance, the path `hai/retrain/bike_rental/` in the script below points to a container named `hai`, and `/retrain/bike_rental/` are subfolders.</span></span> <span data-ttu-id="7f70a-168">Attualmente, non è possibile creare sottocartelle tramite l'interfaccia utente del portale, ma esistono diversi [Strumenti di esplorazione degli archivi di Azure](../storage/common/storage-explorers.md) che consentono di eseguire questa operazione.</span><span class="sxs-lookup"><span data-stu-id="7f70a-168">Currently, you cannot create subfolders through the portal UI, but there are [several Azure Storage Explorers](../storage/common/storage-explorers.md) that allow you to do so.</span></span> <span data-ttu-id="7f70a-169">È consigliabile creare un nuovo contenitore nella risorsa di archiviazione per archiviare i nuovi modelli sottoposti a training (file con estensione ilearner) come segue: dalla pagina Archiviazione fare clic sul pulsante **Aggiungi** nella parte inferiore e denominarlo `retrain`.</span><span class="sxs-lookup"><span data-stu-id="7f70a-169">It is recommended that you create a new container in your storage to store the new trained models (.ilearner files) as follows: from your storage page, click on the **Add** button at the bottom and name it `retrain`.</span></span> <span data-ttu-id="7f70a-170">In breve, le modifiche necessarie allo script seguente si riferiscono a `AccountName`, `AccountKey` e `RelativeLocation` (:`"retrain/model' + $seq + '.ilearner"`).</span><span class="sxs-lookup"><span data-stu-id="7f70a-170">In summary, the necassary changes to the script below pertain to `AccountName`, `AccountKey` and `RelativeLocation` (:`"retrain/model' + $seq + '.ilearner"`).</span></span>

    # Invoke the retraining API 10 times
    # This is the default (and the only) endpoint on the training web service
    $trainingSvcEp = (Get-AmlWebServiceEndpoint -WebServiceId $trainingSvc.Id)[0];
    $submitJobRequestUrl = $trainingSvcEp.ApiLocation + '/jobs?api-version=2.0';
    $apiKey = $trainingSvcEp.PrimaryKey;
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $inputFileName = 'https://bostonmtc.blob.core.windows.net/hai/retrain/bike_rental/BikeRental' + $seq + '.csv';
        $configContent = '{ "GlobalParameters": { "URI": "' + $inputFileName + '" }, "Outputs": { "output1": { "ConnectionString": "DefaultEndpointsProtocol=https;AccountName=<myaccount>;AccountKey=<mykey>", "RelativeLocation": "hai/retrain/bike_rental/model' + $seq + '.ilearner" } } }';
        Write-Host ('training regression model on ' + $inputFileName + ' for rental location ' + $seq + '...');
        Invoke-AmlWebServiceBESEndpoint -JobConfigString $configContent -SubmitJobRequestUrl $submitJobRequestUrl -ApiKey $apiKey
    }

> [!NOTE]
> <span data-ttu-id="7f70a-171">L'endpoint BES è l'unica modalità supportata per questa operazione.</span><span class="sxs-lookup"><span data-stu-id="7f70a-171">The BES endpoint is the only supported mode for this operation.</span></span> <span data-ttu-id="7f70a-172">Non è possibile usare la modalità RRS per la creazione di modelli di training.</span><span class="sxs-lookup"><span data-stu-id="7f70a-172">RRS cannot be used for producing trained models.</span></span>
> 
> 

<span data-ttu-id="7f70a-173">Come si può vedere nel codice riportato sopra, anziché costruire 10 file JSON di configurazione del processo BES diversi, la stringa di configurazione viene creata in modo dinamico e inviata al parametro *jobConfigString* del cmdlet **InvokeAmlWebServceBESEndpoint** , dato che non è necessario mantenere una copia su disco.</span><span class="sxs-lookup"><span data-stu-id="7f70a-173">As you can see above, instead of constructing 10 different BES job configuration json files, we dynamically create the config string instead and feed it to the *jobConfigString* parameter of the **InvokeAmlWebServceBESEndpoint** cmdlet, since there is really no need to keep a copy on disk.</span></span>

<span data-ttu-id="7f70a-174">Se tutto va bene, dopo poco tempo nell'account di archiviazione di Azure dovrebbero essere disponibili 10 file con estensione ilearner, da *model001.ilearner* a *model010.ilearner*.</span><span class="sxs-lookup"><span data-stu-id="7f70a-174">If everything goes well, after a while you should see 10 .ilearner files, from *model001.ilearner* to *model010.ilearner*, in your Azure storage account.</span></span> <span data-ttu-id="7f70a-175">A questo punto è possibile aggiornare i 10 endpoint di servizio Web di attribuzione dei punteggi con tali modelli, usando il cmdlet **Patch-AmlWebServiceEndpoint** di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7f70a-175">Now we're ready to update our 10 scoring web service endpoints with these models using the **Patch-AmlWebServiceEndpoint** PowerShell cmdlet.</span></span> <span data-ttu-id="7f70a-176">Tenere presente anche in questo caso che è possibile applicare patch soltanto agli endpoint non predefiniti creati in precedenza a livello di codice.</span><span class="sxs-lookup"><span data-stu-id="7f70a-176">Remember again that we can only patch the non-default endpoints we programmatically created earlier.</span></span>

    # Patch the 10 endpoints with respective .ilearner models
    $baseLoc = 'http://bostonmtc.blob.core.windows.net/'
    $sasToken = '<my_blob_sas_token>'
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        $relativeLoc = 'hai/retrain/bike_rental/model' + $seq + '.ilearner';
        Write-Host ('Patching endpoint ' + $endpointName + '...');
        Patch-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -ResourceName 'Bike Rental [trained model]' -BaseLocation $baseLoc -RelativeLocation $relativeLoc -SasBlobToken $sasToken
    }

<span data-ttu-id="7f70a-177">L'esecuzione dovrebbe essere abbastanza rapida.</span><span class="sxs-lookup"><span data-stu-id="7f70a-177">This should run fairly quickly.</span></span> <span data-ttu-id="7f70a-178">Al termine saranno disponibili 10 endpoint di servizio Web predittivi, ognuno dei quali contiene un modello di cui è stato eseguito il training in modo univoco sul set di dati specifico di un punto di noleggio. Tutto questo a partire da un unico esperimento di training.</span><span class="sxs-lookup"><span data-stu-id="7f70a-178">When the execution finishes, we'll have successfully created 10 predictive web service endpoints, each containing a trained model uniquely trained on the dataset specific to a rental location, all from a single training experiment.</span></span> <span data-ttu-id="7f70a-179">Per eseguire una verifica, è possibile chiamare gli endpoint con il cmdlet **InvokeAmlWebServiceRRSEndpoint**, fornendo gli stessi dati di input. Il risultato dovrebbe essere costituito da stime diverse, dato che per il training di ogni modello è stato usato un set di dati di training diverso.</span><span class="sxs-lookup"><span data-stu-id="7f70a-179">To verify this, you can try calling these endpoints using the **InvokeAmlWebServiceRRSEndpoint** cmdlet, providing them with the same input data, and you should expect to see different prediction results since the models are trained with different training sets.</span></span>

## <a name="full-powershell-script"></a><span data-ttu-id="7f70a-180">Script di PowerShell completo</span><span class="sxs-lookup"><span data-stu-id="7f70a-180">Full PowerShell script</span></span>
<span data-ttu-id="7f70a-181">Di seguito è riportato il listato del codice sorgente completo:</span><span class="sxs-lookup"><span data-stu-id="7f70a-181">Here's the listing of the full source code:</span></span>

    Import-Module .\AzureMLPS.dll
    # Assume the default configuration file exists and properly set to point to the valid workspace.
    $scoringSvc = Get-AmlWebService | where Name -eq 'Bike Rental Scoring'
    $trainingSvc = Get-AmlWebService | where Name -eq 'Bike Rental Training'

    # Create 10 endpoints on the scoring web service
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        Write-Host ('adding endpoint ' + $endpontName + '...')
        Add-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -Description $endpointName     
    }

    # Invoke the retraining API 10 times to produce 10 regression models in .ilearner format
    $trainingSvcEp = (Get-AmlWebServiceEndpoint -WebServiceId $trainingSvc.Id)[0];
    $submitJobRequestUrl = $trainingSvcEp.ApiLocation + '/jobs?api-version=2.0';
    $apiKey = $trainingSvcEp.PrimaryKey;
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $inputFileName = 'https://bostonmtc.blob.core.windows.net/hai/retrain/bike_rental/BikeRental' + $seq + '.csv';
        $configContent = '{ "GlobalParameters": { "URI": "' + $inputFileName + '" }, "Outputs": { "output1": { "ConnectionString": "DefaultEndpointsProtocol=https;AccountName=<myaccount>;AccountKey=<mykey>", "RelativeLocation": "hai/retrain/bike_rental/model' + $seq + '.ilearner" } } }';
        Write-Host ('training regression model on ' + $inputFileName + ' for rental location ' + $seq + '...');
        Invoke-AmlWebServiceBESEndpoint -JobConfigString $configContent -SubmitJobRequestUrl $submitJobRequestUrl -ApiKey $apiKey
    }

    # Patch the 10 endpoints with respective .ilearner models
    $baseLoc = 'http://bostonmtc.blob.core.windows.net/'
    $sasToken = '?test'
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        $relativeLoc = 'hai/retrain/bike_rental/model' + $seq + '.ilearner';
        Write-Host ('Patching endpoint ' + $endpointName + '...');
        Patch-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -ResourceName 'Bike Rental [trained model]' -BaseLocation $baseLoc -RelativeLocation $relativeLoc -SasBlobToken $sasToken
    }
