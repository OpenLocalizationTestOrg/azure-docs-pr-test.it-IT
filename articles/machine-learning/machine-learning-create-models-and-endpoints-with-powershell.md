---
title: "aaaCreate più modelli da un esperimento | Documenti Microsoft"
description: "Utilizzare PowerShell toocreate più modelli di Machine Learning e gli endpoint di servizio con hello web stesso algoritmo, ma i set di dati di training diversi."
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
ms.openlocfilehash: 4a258a8ab26395d4169a058520151c860e16e169
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-many-machine-learning-models-and-web-service-endpoints-from-one-experiment-using-powershell"></a><span data-ttu-id="5fa51-103">Creare più modelli di Machine Learning ed endpoint di servizio Web da un esperimento usando PowerShell</span><span class="sxs-lookup"><span data-stu-id="5fa51-103">Create many Machine Learning models and web service endpoints from one experiment using PowerShell</span></span>
<span data-ttu-id="5fa51-104">Di seguito è un problema comune di apprendimento macchina: si desidera toocreate molti modelli contenenti hello stesso flusso di lavoro di training e utilizzare hello stesso algoritmo, ma dispone di set di dati di training diversi come input.</span><span class="sxs-lookup"><span data-stu-id="5fa51-104">Here's a common machine learning problem: You want toocreate many models that have hello same training workflow and use hello same algorithm, but have different training datasets as input.</span></span> <span data-ttu-id="5fa51-105">In questo articolo illustra come toodo questo su larga scala in Azure Machine Learning Studio usando un esperimento di singolo.</span><span class="sxs-lookup"><span data-stu-id="5fa51-105">This article shows you how toodo this at scale in Azure Machine Learning Studio using just a single experiment.</span></span>

<span data-ttu-id="5fa51-106">Si supponga, ad esempio, di essere proprietari di un franchising globale di noleggio di biciclette.</span><span class="sxs-lookup"><span data-stu-id="5fa51-106">For example, let's say you own a global bike rental franchise business.</span></span> <span data-ttu-id="5fa51-107">Si desidera toobuild una richiesta di noleggio di regressione modello toopredict hello in base ai dati cronologici.</span><span class="sxs-lookup"><span data-stu-id="5fa51-107">You want toobuild a regression model toopredict hello rental demand based on historic data.</span></span> <span data-ttu-id="5fa51-108">Posizioni di noleggio 1.000 sono mondo hello e aver raccolto un set di dati per ogni percorso che include funzionalità importanti, ad esempio data, ora, meteo e il traffico che sono specifici tooeach percorso.</span><span class="sxs-lookup"><span data-stu-id="5fa51-108">You have 1,000 rental locations across hello world and you've collected a dataset for each location that includes important features such as date, time, weather, and traffic that are specific tooeach location.</span></span>

<span data-ttu-id="5fa51-109">Impossibile eseguire il training del modello una volta con una versione unita di tutti i set di hello in tutte le posizioni.</span><span class="sxs-lookup"><span data-stu-id="5fa51-109">You could train your model once using a merged version of all hello datasets across all locations.</span></span> <span data-ttu-id="5fa51-110">Ma poiché ognuno dei percorsi di un ambiente univoco, un approccio migliore potrebbe essere tootrain il modello di regressione separatamente utilizzando hello set di dati per ogni posizione.</span><span class="sxs-lookup"><span data-stu-id="5fa51-110">But because each of your locations has a unique environment, a better approach would be tootrain your regression model separately using hello dataset for each location.</span></span> <span data-ttu-id="5fa51-111">In questo modo, ogni modello con training può richiedere in dimensioni di archivio diversi account hello, volume, geography, popolamento, ambiente, finestra bike orientato al traffico *e così via*.</span><span class="sxs-lookup"><span data-stu-id="5fa51-111">That way, each trained model could take into account hello different store sizes, volume, geography, population, bike-friendly traffic environment, *etc.*.</span></span>

<span data-ttu-id="5fa51-112">Che può essere l'approccio migliore hello, ma non si vuole toocreate 1.000 esperimenti di training in Azure Machine Learning con ciascuno dei quali rappresenta un percorso univoco.</span><span class="sxs-lookup"><span data-stu-id="5fa51-112">That may be hello best approach, but you don't want toocreate 1,000 training experiments in Azure Machine Learning with each one representing a unique location.</span></span> <span data-ttu-id="5fa51-113">Oltre a essere un'attività piuttosto complessa, è inoltre sembra molto inefficiente poiché ogni esperimento avrebbe tutti hello stessi componenti ad eccezione di hello training set.</span><span class="sxs-lookup"><span data-stu-id="5fa51-113">Besides being an overwhelming task, it's also seems pretty inefficient since each experiment would have all hello same components except for hello training dataset.</span></span>

<span data-ttu-id="5fa51-114">Fortunatamente, è possibile effettuare questa operazione utilizzando hello [ripetizione di training API di Azure Machine Learning](machine-learning-retrain-models-programmatically.md) e automazione di attività hello con [Azure Machine Learning PowerShell](machine-learning-powershell-module.md).</span><span class="sxs-lookup"><span data-stu-id="5fa51-114">Fortunately, we can accomplish this by using hello [Azure Machine Learning retraining API](machine-learning-retrain-models-programmatically.md) and automating hello task with [Azure Machine Learning PowerShell](machine-learning-powershell-module.md).</span></span>

> [!NOTE]
> <span data-ttu-id="5fa51-115">toomake eseguito più velocemente di questo esempio, si sarà ridurre il numero di hello di percorsi da 1.000 too10.</span><span class="sxs-lookup"><span data-stu-id="5fa51-115">toomake our sample run faster, we'll reduce hello number of locations from 1,000 too10.</span></span> <span data-ttu-id="5fa51-116">Ma hello gli stessi principi e procedure too1, posizioni 000.</span><span class="sxs-lookup"><span data-stu-id="5fa51-116">But hello same principles and procedures apply too1,000 locations.</span></span> <span data-ttu-id="5fa51-117">Hello unica differenza è che se si desidera tootrain da 1.000 set di dati si vorrà toothink dell'esecuzione di hello seguente script di PowerShell in parallelo.</span><span class="sxs-lookup"><span data-stu-id="5fa51-117">hello only difference is that if you want tootrain from 1,000 datasets you probably want toothink of running hello following PowerShell scripts in parallel.</span></span> <span data-ttu-id="5fa51-118">Come toodo che esula hello in questo articolo, ma è possibile trovare esempi di PowerShell multithreading in hello Internet.</span><span class="sxs-lookup"><span data-stu-id="5fa51-118">How toodo that is beyond hello scope of this article, but you can find examples of PowerShell multi-threading on hello Internet.</span></span>  
> 
> 

## <a name="set-up-hello-training-experiment"></a><span data-ttu-id="5fa51-119">Impostare l'esperimento di training hello</span><span class="sxs-lookup"><span data-stu-id="5fa51-119">Set up hello training experiment</span></span>
<span data-ttu-id="5fa51-120">Verrà riportato un esempio di toouse [esperimento di training](https://gallery.cortanaintelligence.com/Experiment/Bike-Rental-Training-Experiment-1) che abbiamo creato in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="5fa51-120">We're going toouse an example [training experiment](https://gallery.cortanaintelligence.com/Experiment/Bike-Rental-Training-Experiment-1) that we've already created in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="5fa51-121">Aprire l'esperimento nell'area di lavoro di [Azure Machine Learning Studio](https://studio.azureml.net) .</span><span class="sxs-lookup"><span data-stu-id="5fa51-121">Open this experiment in your [Azure Machine Learning Studio](https://studio.azureml.net) workspace.</span></span>

> [!NOTE]
> <span data-ttu-id="5fa51-122">In ordine toofollow con questo esempio, è opportuno toouse un'area di lavoro standard, anziché un'area di lavoro disponibile.</span><span class="sxs-lookup"><span data-stu-id="5fa51-122">In order toofollow along with this example, you may want toouse a standard workspace rather than a free workspace.</span></span> <span data-ttu-id="5fa51-123">Si verrà creato un endpoint per ogni cliente - per un totale di 10 endpoint - e che richiedono un'area di lavoro standard, poiché un'area di lavoro disponibile è limitata too3 endpoint.</span><span class="sxs-lookup"><span data-stu-id="5fa51-123">We'll be creating one endpoint for each customer - for a total of 10 endpoints - and that will require a standard workspace since a free workspace is limited too3 endpoints.</span></span> <span data-ttu-id="5fa51-124">Se si dispone solo di un'area di lavoro disponibile, è sufficiente modificare script hello sotto tooallow per solo 3 posizioni.</span><span class="sxs-lookup"><span data-stu-id="5fa51-124">If you only have a free workspace, just modify hello scripts below tooallow for only 3 locations.</span></span>
> 
> 

<span data-ttu-id="5fa51-125">sperimentazione Hello utilizza un **l'importazione dei dati** modulo tooimport hello training set *customer001.csv* da un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="5fa51-125">hello experiment uses an **Import Data** module tooimport hello training dataset *customer001.csv* from an Azure storage account.</span></span> <span data-ttu-id="5fa51-126">Si supponga che abbiamo raccolti i set di dati di training da tutti i percorsi di noleggio di biciclette e salvate in hello stesso percorso di archiviazione del blob con nomi di file compreso tra *rentalloc001.csv* troppo*rentalloc10.csv* .</span><span class="sxs-lookup"><span data-stu-id="5fa51-126">Let's assume we have collected training datasets from all bike rental locations and stored them in hello same blob storage location with file names ranging from *rentalloc001.csv* too*rentalloc10.csv*.</span></span>

![immagine](./media/machine-learning-create-models-and-endpoints-with-powershell/reader-module.png)

<span data-ttu-id="5fa51-128">Si noti che un **Output del servizio Web** modulo è stato aggiunto toohello **Train Model** modulo.</span><span class="sxs-lookup"><span data-stu-id="5fa51-128">Note that a **Web Service Output** module has been added toohello **Train Model** module.</span></span>
<span data-ttu-id="5fa51-129">Quando questo esperimento viene distribuito come servizio web, in formato hello di un file .ilearner endpoint hello associata a tale output restituirà modello con training hello.</span><span class="sxs-lookup"><span data-stu-id="5fa51-129">When this experiment is deployed as a web service, hello endpoint associated with that output will return hello trained model in hello format of a .ilearner file.</span></span>

<span data-ttu-id="5fa51-130">Si noti inoltre che è necessario impostare un parametro del servizio web per URL hello che hello **l'importazione dei dati** modulo Usa.</span><span class="sxs-lookup"><span data-stu-id="5fa51-130">Also note that we set up a web service parameter for hello URL that hello **Import Data** module uses.</span></span> <span data-ttu-id="5fa51-131">In questo modo toouse hello parametro toospecify singoli set di dati tootrain hello modello di training per ogni posizione.</span><span class="sxs-lookup"><span data-stu-id="5fa51-131">This allows us toouse hello parameter toospecify individual training datasets tootrain hello model for each location.</span></span>
<span data-ttu-id="5fa51-132">Esistono altri modi in cui è stato possibile eseguita questa operazione, ad esempio mediante una query SQL con un dati tooget parametro del servizio web da un database di SQL Azure o semplicemente un **Input del servizio Web** toopass modulo in un set di dati di toohello servizio web.</span><span class="sxs-lookup"><span data-stu-id="5fa51-132">There are other ways we could have done this, such as using a SQL query with a web service parameter tooget data from a SQL Azure database, or simply using a  **Web Service Input** module toopass in a dataset toohello web service.</span></span>

![immagine](./media/machine-learning-create-models-and-endpoints-with-powershell/web-service-output.png)

<span data-ttu-id="5fa51-134">A questo punto, eseguire questo esperimento di training, specificando il valore predefinito di hello *rental001.csv* come hello set di dati di training.</span><span class="sxs-lookup"><span data-stu-id="5fa51-134">Now, let's run this training experiment using hello default value *rental001.csv* as hello training dataset.</span></span> <span data-ttu-id="5fa51-135">Se si visualizza l'output di hello di hello **Evaluate** modulo (output di hello scegliere **Visualizza**), è possibile vedere si ottiene un ragionevole delle prestazioni di *AUC* = 0.91.</span><span class="sxs-lookup"><span data-stu-id="5fa51-135">If you view hello output of hello **Evaluate** module (click hello output and select **Visualize**), you can see we get a decent performance of *AUC* = 0.91.</span></span> <span data-ttu-id="5fa51-136">A questo punto, si è pronti toodeploy un servizio web da questo esperimento di training.</span><span class="sxs-lookup"><span data-stu-id="5fa51-136">At this point, we're ready toodeploy a web service out of this training experiment.</span></span>

## <a name="deploy-hello-training-and-scoring-web-services"></a><span data-ttu-id="5fa51-137">Distribuire training hello e assegnazione dei punteggi di servizi web</span><span class="sxs-lookup"><span data-stu-id="5fa51-137">Deploy hello training and scoring web services</span></span>
<span data-ttu-id="5fa51-138">hello toodeploy training servizio web, fare clic su hello **di servizio Web** sotto l'area di disegno esperimento hello e selezionare **distribuzione servizio Web**.</span><span class="sxs-lookup"><span data-stu-id="5fa51-138">toodeploy hello training web service, click hello **Set Up Web Service** button below hello experiment canvas and select **Deploy Web Service**.</span></span> <span data-ttu-id="5fa51-139">Denominare il servizio Web "Bike Rental Training".</span><span class="sxs-lookup"><span data-stu-id="5fa51-139">Call this web service ""Bike Rental Training".</span></span>

<span data-ttu-id="5fa51-140">A questo punto è necessario il servizio web assegnazione dei punteggi di toodeploy hello.</span><span class="sxs-lookup"><span data-stu-id="5fa51-140">Now we need toodeploy hello scoring web service.</span></span>
<span data-ttu-id="5fa51-141">toodo, è possibile fare clic su **di servizio Web** seguito hello area di disegno e selezionare **servizio Web predittivo**.</span><span class="sxs-lookup"><span data-stu-id="5fa51-141">toodo this, we can click **Set Up Web Service** below hello canvas and select **Predictive Web Service**.</span></span> <span data-ttu-id="5fa51-142">Verrà creato un esperimento di assegnazione dei punteggi.</span><span class="sxs-lookup"><span data-stu-id="5fa51-142">This creates a scoring experiment.</span></span>
<span data-ttu-id="5fa51-143">È necessario toomake alcune piccole modifiche toomake, che funziona come un servizio web, ad esempio dati di input di rimuovere la colonna di etichetta hello "cnt" dalla hello e limitando l'id dell'istanza hello tooonly output hello e hello corrispondente valore stimato.</span><span class="sxs-lookup"><span data-stu-id="5fa51-143">We'll need toomake a few minor adjustments toomake it work as a web service, such as removing hello label column "cnt" from hello input data and limiting hello output tooonly hello instance id and hello corresponding predicted value.</span></span>

<span data-ttu-id="5fa51-144">toosave manualmente che funzionano, è possibile aprire semplicemente hello [esperimento predittiva](https://gallery.cortanaintelligence.com/Experiment/Bike-Rental-Predicative-Experiment-1) in hello raccolta che è già stata preparata.</span><span class="sxs-lookup"><span data-stu-id="5fa51-144">toosave yourself that work, you can simply open hello [predictive experiment](https://gallery.cortanaintelligence.com/Experiment/Bike-Rental-Predicative-Experiment-1) in hello Gallery that's already been prepared.</span></span>

<span data-ttu-id="5fa51-145">servizio web di toodeploy hello, eseguire l'esperimento predittiva hello, quindi fare clic su hello **distribuzione servizio Web** pulsante sotto l'area di disegno hello.</span><span class="sxs-lookup"><span data-stu-id="5fa51-145">toodeploy hello web service, run hello predictive experiment, then click hello **Deploy Web Service** button below hello canvas.</span></span> <span data-ttu-id="5fa51-146">Hello Nome servizio web "Punteggio noleggio Bike" di punteggio ".</span><span class="sxs-lookup"><span data-stu-id="5fa51-146">Name hello scoring web service "Bike Rental Scoring"".</span></span>

## <a name="create-10-identical-web-service-endpoints-with-powershell"></a><span data-ttu-id="5fa51-147">Creare 10 endpoint di servizio Web identici con PowerShell</span><span class="sxs-lookup"><span data-stu-id="5fa51-147">Create 10 identical web service endpoints with PowerShell</span></span>
<span data-ttu-id="5fa51-148">Questo servizio Web include un endpoint predefinito,</span><span class="sxs-lookup"><span data-stu-id="5fa51-148">This web service comes with a default endpoint.</span></span> <span data-ttu-id="5fa51-149">Ma non siamo interessati come endpoint predefinito hello poiché non può essere aggiornata.</span><span class="sxs-lookup"><span data-stu-id="5fa51-149">But we're not as interested in hello default endpoint since it can't be updated.</span></span> <span data-ttu-id="5fa51-150">È necessario toodo è toocreate 10 altri endpoint, uno per ogni posizione.</span><span class="sxs-lookup"><span data-stu-id="5fa51-150">What we need toodo is toocreate 10 additional endpoints, one for each location.</span></span> <span data-ttu-id="5fa51-151">A tale scopo, usare PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5fa51-151">We'll do this with PowerShell.</span></span>

<span data-ttu-id="5fa51-152">Configurare l'ambiente PowerShell:</span><span class="sxs-lookup"><span data-stu-id="5fa51-152">First, we set up our PowerShell environment:</span></span>

    Import-Module .\AzureMLPS.dll
    # Assume hello default configuration file exists and is properly set toopoint toohello valid Workspace.
    $scoringSvc = Get-AmlWebService | where Name -eq 'Bike Rental Scoring'
    $trainingSvc = Get-AmlWebService | where Name -eq 'Bike Rental Training'

<span data-ttu-id="5fa51-153">Eseguire quindi hello comando PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="5fa51-153">Then, run hello following PowerShell command:</span></span>

    # Create 10 endpoints on hello scoring web service.
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        Write-Host ('adding endpoint ' + $endpointName + '...')
        Add-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -Description $endpointName     
    }

<span data-ttu-id="5fa51-154">Ora abbiamo creato 10 endpoint e contengono hello stesso modello con training sottoposto a training sui *customer001.csv*.</span><span class="sxs-lookup"><span data-stu-id="5fa51-154">Now we've created 10 endpoints and they all contain hello same trained model trained on *customer001.csv*.</span></span> <span data-ttu-id="5fa51-155">È possibile visualizzarli in hello portale di gestione di Azure.</span><span class="sxs-lookup"><span data-stu-id="5fa51-155">You can view them in hello Azure Management Portal.</span></span>

![immagine](./media/machine-learning-create-models-and-endpoints-with-powershell/created-endpoints.png)

## <a name="update-hello-endpoints-toouse-separate-training-datasets-using-powershell"></a><span data-ttu-id="5fa51-157">Aggiornare hello endpoint toouse separato training set di dati tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="5fa51-157">Update hello endpoints toouse separate training datasets using PowerShell</span></span>
<span data-ttu-id="5fa51-158">passaggio successivo Hello è endpoint hello tooupdate con i modelli in modo univoco sottoposto a training sui singoli dati di ogni cliente.</span><span class="sxs-lookup"><span data-stu-id="5fa51-158">hello next step is tooupdate hello endpoints with models uniquely trained on each customer's individual data.</span></span> <span data-ttu-id="5fa51-159">Ma è prima necessario tooproduce questi modelli da hello **Bike noleggio Training** servizio web.</span><span class="sxs-lookup"><span data-stu-id="5fa51-159">But first we need tooproduce these models from hello **Bike Rental Training** web service.</span></span> <span data-ttu-id="5fa51-160">Necessario tornare indietro toohello **Bike noleggio Training** servizio web.</span><span class="sxs-lookup"><span data-stu-id="5fa51-160">Let's go back toohello **Bike Rental Training** web service.</span></span> <span data-ttu-id="5fa51-161">È necessario toocall endpoint BES 10 volte con 10 set di dati di training diversi in modelli diversi di ordine tooproduce 10.</span><span class="sxs-lookup"><span data-stu-id="5fa51-161">We need toocall its BES endpoint 10 times with 10 different training datasets in order tooproduce 10 different models.</span></span> <span data-ttu-id="5fa51-162">Si userà hello **InovkeAmlWebServiceBESEndpoint** toodo cmdlet PowerShell questo.</span><span class="sxs-lookup"><span data-stu-id="5fa51-162">We'll use hello **InovkeAmlWebServiceBESEndpoint** PowerShell cmdlet toodo this.</span></span>

<span data-ttu-id="5fa51-163">È necessario anche tooprovide credenziali per l'account di archiviazione blob in `$configContent`, vale a dire, campi hello `AccountName`, `AccountKey` e `RelativeLocation`.</span><span class="sxs-lookup"><span data-stu-id="5fa51-163">You will also need tooprovide credentials for your blob storage account into `$configContent`, namely, at hello fields `AccountName`, `AccountKey` and `RelativeLocation`.</span></span> <span data-ttu-id="5fa51-164">Hello `AccountName` può essere uno dei nomi di account, come illustrato nel hello **portale di gestione di Azure classico** (*archiviazione* scheda).</span><span class="sxs-lookup"><span data-stu-id="5fa51-164">hello `AccountName` can be one of your account names, as seen in hello **Classic Azure Management Portal** (*Storage* tab).</span></span> <span data-ttu-id="5fa51-165">Quando si fa clic su un account di archiviazione, il relativo `AccountKey` sono reperibili effettuando premendo hello **Gestisci chiavi di accesso** pulsante nella parte inferiore di hello e copia hello *chiave di accesso primaria*.</span><span class="sxs-lookup"><span data-stu-id="5fa51-165">Once you click on a storage account, its `AccountKey` can be found by pressing hello **Manage Access Keys** button at hello bottom and copying hello *Primary Access Key*.</span></span> <span data-ttu-id="5fa51-166">Hello `RelativeLocation` è archiviazione tooyour relativo percorso di hello in cui verrà archiviato un nuovo modello.</span><span class="sxs-lookup"><span data-stu-id="5fa51-166">hello `RelativeLocation` is hello path relative tooyour storage where a new model will be stored.</span></span> <span data-ttu-id="5fa51-167">Ad esempio, percorso di hello `hai/retrain/bike_rental/` nello script hello sotto punti tooa contenitore denominato `hai`, e `/retrain/bike_rental/` sono le sottocartelle.</span><span class="sxs-lookup"><span data-stu-id="5fa51-167">For instance, hello path `hai/retrain/bike_rental/` in hello script below points tooa container named `hai`, and `/retrain/bike_rental/` are subfolders.</span></span> <span data-ttu-id="5fa51-168">Attualmente, non è possibile creare sottocartelle tramite l'interfaccia utente del portale hello, ma esistono [Esplora archivi di Azure diversi](../storage/common/storage-explorers.md) che consentono di toodo così.</span><span class="sxs-lookup"><span data-stu-id="5fa51-168">Currently, you cannot create subfolders through hello portal UI, but there are [several Azure Storage Explorers](../storage/common/storage-explorers.md) that allow you toodo so.</span></span> <span data-ttu-id="5fa51-169">Si consiglia di creare un nuovo contenitore nel hello toostore archiviazione nuovi modelli con training (file .ilearner) come segue: dalla pagina di archiviazione, fare clic su hello **Aggiungi** pulsante nella parte inferiore di hello e denominarlo `retrain`.</span><span class="sxs-lookup"><span data-stu-id="5fa51-169">It is recommended that you create a new container in your storage toostore hello new trained models (.ilearner files) as follows: from your storage page, click on hello **Add** button at hello bottom and name it `retrain`.</span></span> <span data-ttu-id="5fa51-170">In sintesi, script toohello le modifiche necessarie hello riportato di seguito riguardano troppo`AccountName`, `AccountKey` e `RelativeLocation` (:`"retrain/model' + $seq + '.ilearner"`).</span><span class="sxs-lookup"><span data-stu-id="5fa51-170">In summary, hello necassary changes toohello script below pertain too`AccountName`, `AccountKey` and `RelativeLocation` (:`"retrain/model' + $seq + '.ilearner"`).</span></span>

    # Invoke hello retraining API 10 times
    # This is hello default (and hello only) endpoint on hello training web service
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
> <span data-ttu-id="5fa51-171">endpoint BES Hello è hello è supportato solo in modalità per questa operazione.</span><span class="sxs-lookup"><span data-stu-id="5fa51-171">hello BES endpoint is hello only supported mode for this operation.</span></span> <span data-ttu-id="5fa51-172">Non è possibile usare la modalità RRS per la creazione di modelli di training.</span><span class="sxs-lookup"><span data-stu-id="5fa51-172">RRS cannot be used for producing trained models.</span></span>
> 
> 

<span data-ttu-id="5fa51-173">Come si può notare, anziché costruire 10 diversi BES processo json i file di configurazione in modo dinamico invece di creare la stringa di configurazione hello i feed di toohello *jobConfigString* parametro di hello  **InvokeAmlWebServceBESEndpoint** cmdlet, perché non è realmente non tookeep necessità per una copia su disco.</span><span class="sxs-lookup"><span data-stu-id="5fa51-173">As you can see above, instead of constructing 10 different BES job configuration json files, we dynamically create hello config string instead and feed it toohello *jobConfigString* parameter of hello **InvokeAmlWebServceBESEndpoint** cmdlet, since there is really no need tookeep a copy on disk.</span></span>

<span data-ttu-id="5fa51-174">Se tutto va bene, dopo un periodo di tempo dovrebbe 10 file .ilearner, da *model001.ilearner* troppo*model010.ilearner*, nell'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="5fa51-174">If everything goes well, after a while you should see 10 .ilearner files, from *model001.ilearner* too*model010.ilearner*, in your Azure storage account.</span></span> <span data-ttu-id="5fa51-175">Ora siamo tooupdate pronto i 10 punteggio web gli endpoint del servizio con questi modelli utilizzando hello **Patch AmlWebServiceEndpoint** cmdlet di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5fa51-175">Now we're ready tooupdate our 10 scoring web service endpoints with these models using hello **Patch-AmlWebServiceEndpoint** PowerShell cmdlet.</span></span> <span data-ttu-id="5fa51-176">Ricorda nuovamente è solo possibile applicare una patch endpoint non predefinito hello a livello di codice creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="5fa51-176">Remember again that we can only patch hello non-default endpoints we programmatically created earlier.</span></span>

    # Patch hello 10 endpoints with respective .ilearner models
    $baseLoc = 'http://bostonmtc.blob.core.windows.net/'
    $sasToken = '<my_blob_sas_token>'
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        $relativeLoc = 'hai/retrain/bike_rental/model' + $seq + '.ilearner';
        Write-Host ('Patching endpoint ' + $endpointName + '...');
        Patch-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -ResourceName 'Bike Rental [trained model]' -BaseLocation $baseLoc -RelativeLocation $relativeLoc -SasBlobToken $sasToken
    }

<span data-ttu-id="5fa51-177">L'esecuzione dovrebbe essere abbastanza rapida.</span><span class="sxs-lookup"><span data-stu-id="5fa51-177">This should run fairly quickly.</span></span> <span data-ttu-id="5fa51-178">Al termine dell'esecuzione di hello, si sarà stato creato endpoint servizio web predittivo 10, ognuna delle quali contiene un modello con training, in modo univoco sottoposto a training sui hello set di dati specifico tooa località noleggio, da un esperimento di training singolo.</span><span class="sxs-lookup"><span data-stu-id="5fa51-178">When hello execution finishes, we'll have successfully created 10 predictive web service endpoints, each containing a trained model uniquely trained on hello dataset specific tooa rental location, all from a single training experiment.</span></span> <span data-ttu-id="5fa51-179">tooverify, è possibile provare a chiamare questi endpoint utilizzando hello **InvokeAmlWebServiceRRSEndpoint** cmdlet, fornire con hello stessi dati di input e, è necessario prevedere che i risultati di stima diverse toosee poiché sono modelli hello eseguito il training con set di training diversi.</span><span class="sxs-lookup"><span data-stu-id="5fa51-179">tooverify this, you can try calling these endpoints using hello **InvokeAmlWebServiceRRSEndpoint** cmdlet, providing them with hello same input data, and you should expect toosee different prediction results since hello models are trained with different training sets.</span></span>

## <a name="full-powershell-script"></a><span data-ttu-id="5fa51-180">Script di PowerShell completo</span><span class="sxs-lookup"><span data-stu-id="5fa51-180">Full PowerShell script</span></span>
<span data-ttu-id="5fa51-181">Ecco l'elenco hello del codice sorgente completo hello:</span><span class="sxs-lookup"><span data-stu-id="5fa51-181">Here's hello listing of hello full source code:</span></span>

    Import-Module .\AzureMLPS.dll
    # Assume hello default configuration file exists and properly set toopoint toohello valid workspace.
    $scoringSvc = Get-AmlWebService | where Name -eq 'Bike Rental Scoring'
    $trainingSvc = Get-AmlWebService | where Name -eq 'Bike Rental Training'

    # Create 10 endpoints on hello scoring web service
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        Write-Host ('adding endpoint ' + $endpontName + '...')
        Add-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -Description $endpointName     
    }

    # Invoke hello retraining API 10 times tooproduce 10 regression models in .ilearner format
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

    # Patch hello 10 endpoints with respective .ilearner models
    $baseLoc = 'http://bostonmtc.blob.core.windows.net/'
    $sasToken = '?test'
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        $relativeLoc = 'hai/retrain/bike_rental/model' + $seq + '.ilearner';
        Write-Host ('Patching endpoint ' + $endpointName + '...');
        Patch-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -ResourceName 'Bike Rental [trained model]' -BaseLocation $baseLoc -RelativeLocation $relativeLoc -SasBlobToken $sasToken
    }
