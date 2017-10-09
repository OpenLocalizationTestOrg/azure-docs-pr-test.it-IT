---
title: un servizio web classica aaaRetrain | Documenti Microsoft
description: Informazioni su come tooprogrammatically ripetere il training di un modello e aggiornamento hello web servizio toouse hello appena modello con Training in Azure Machine Learning.
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondlaghaeian
editor: 
ms.assetid: e36e1961-9e8b-4801-80ef-46d80b140452
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: d3ba21ed75f02868535cb2fcac607643303a9554
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-a-classic-web-service"></a><span data-ttu-id="fd4a6-103">Ripetere il training di un servizio Web classico</span><span class="sxs-lookup"><span data-stu-id="fd4a6-103">Retrain a Classic web service</span></span>
<span data-ttu-id="fd4a6-104">Hello predittiva del servizio Web è stato distribuito è predefinito hello punteggio endpoint.</span><span class="sxs-lookup"><span data-stu-id="fd4a6-104">hello Predictive Web Service you deployed is hello default scoring endpoint.</span></span> <span data-ttu-id="fd4a6-105">Gli endpoint predefiniti vengono mantenuti sincronizzati con hello originali di training e assegnazione dei punteggi esperimenti, e pertanto hello modello con training per l'endpoint predefinito hello non può essere sostituito.</span><span class="sxs-lookup"><span data-stu-id="fd4a6-105">Default endpoints are kept in sync with hello original training and scoring experiments, and therefore hello trained model for hello default endpoint cannot be replaced.</span></span> <span data-ttu-id="fd4a6-106">servizio web di hello tooretrain, è necessario aggiungere un nuovo servizio web toohello di endpoint.</span><span class="sxs-lookup"><span data-stu-id="fd4a6-106">tooretrain hello web service, you must add a new endpoint toohello web service.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="fd4a6-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="fd4a6-107">Prerequisites</span></span>
<span data-ttu-id="fd4a6-108">È necessario impostare un esperimento di training e un esperimento predittivo come illustrato in [Ripetere il training dei modelli di Machine Learning in modo programmatico](machine-learning-retrain-models-programmatically.md).</span><span class="sxs-lookup"><span data-stu-id="fd4a6-108">You must have set up a training experiment and a predictive experiment as shown in [Retrain Machine Learning models programmatically](machine-learning-retrain-models-programmatically.md).</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="fd4a6-109">sperimentazione predittiva Hello deve essere distribuito come un classica servizio web machine learning.</span><span class="sxs-lookup"><span data-stu-id="fd4a6-109">hello predictive experiment must be deployed as a Classic machine learning web service.</span></span> 
> 
> 

<span data-ttu-id="fd4a6-110">Per altre informazioni sulla distribuzione di servizi Web, vedere [Distribuire un servizio Web di Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="fd4a6-110">For additional information on Deploying web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

## <a name="add-a-new-endpoint"></a><span data-ttu-id="fd4a6-111">Aggiungere un nuovo endpoint</span><span class="sxs-lookup"><span data-stu-id="fd4a6-111">Add a new Endpoint</span></span>
<span data-ttu-id="fd4a6-112">Hello predittiva del servizio Web che è stato distribuito contiene un endpoint che viene mantenuta la sincronizzazione con training originale hello e il modello con training di punteggio esperimenti di punteggio predefinito.</span><span class="sxs-lookup"><span data-stu-id="fd4a6-112">hello Predictive Web Service that you deployed contains a default scoring endpoint that is kept in sync with hello original training and scoring experiments trained model.</span></span> <span data-ttu-id="fd4a6-113">tooupdate toowith per il servizio web un nuovo modello con training, è necessario creare un nuovo endpoint di assegnazione dei punteggi.</span><span class="sxs-lookup"><span data-stu-id="fd4a6-113">tooupdate your web service toowith a new trained model, you must create a new scoring endpoint.</span></span> 

<span data-ttu-id="fd4a6-114">un nuovo endpoint di punteggio, nel servizio Web predittivo che possono essere aggiornate con modello con training hello hello toocreate:</span><span class="sxs-lookup"><span data-stu-id="fd4a6-114">toocreate a new scoring endpoint, on hello Predictive Web Service that can be updated with hello trained model:</span></span>

> [!NOTE]
> <span data-ttu-id="fd4a6-115">Assicurarsi che si sta aggiungendo hello toohello di endpoint servizio Web predittivo, non hello servizio Web di Training.</span><span class="sxs-lookup"><span data-stu-id="fd4a6-115">Be sure you are adding hello endpoint toohello Predictive Web Service, not hello Training Web Service.</span></span> <span data-ttu-id="fd4a6-116">Se sono stati distribuiti correttamente sia un servizio Web di training che uno predittivo, verranno visualizzati due servizi Web elencati separatamente.</span><span class="sxs-lookup"><span data-stu-id="fd4a6-116">If you have correctly deployed both a Training and a Predictive Web Service, you should see two separate web services listed.</span></span> <span data-ttu-id="fd4a6-117">Servizio Web predittivo Hello deve terminare con "[predittiva exp]"..</span><span class="sxs-lookup"><span data-stu-id="fd4a6-117">hello Predictive Web Service should end with "[predictive exp.]".</span></span>
> 
> 

<span data-ttu-id="fd4a6-118">Esistono tre modi in cui è possibile aggiungere un nuovo servizio web di tooa punto finale:</span><span class="sxs-lookup"><span data-stu-id="fd4a6-118">There are three ways in which you can add a new end point tooa web service:</span></span>

1. <span data-ttu-id="fd4a6-119">A livello di codice</span><span class="sxs-lookup"><span data-stu-id="fd4a6-119">Programmatically</span></span>
2. <span data-ttu-id="fd4a6-120">Utilizzare il portale di servizi Web di Microsoft Azure hello</span><span class="sxs-lookup"><span data-stu-id="fd4a6-120">Use hello Microsoft Azure Web Services portal</span></span>
3. <span data-ttu-id="fd4a6-121">Utilizzare hello portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="fd4a6-121">Use hello Azure classic portal</span></span>

### <a name="programmatically-add-an-endpoint"></a><span data-ttu-id="fd4a6-122">Aggiungere un endpoint a livello di codice</span><span class="sxs-lookup"><span data-stu-id="fd4a6-122">Programmatically add an endpoint</span></span>
<span data-ttu-id="fd4a6-123">È possibile aggiungere endpoint di assegnazione dei punteggi usando il codice di esempio hello fornito in questo [repository github](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="fd4a6-123">You can add scoring endpoints using hello sample code provided in this [github repository](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs).</span></span>

### <a name="use-hello-microsoft-azure-web-services-portal-tooadd-an-endpoint"></a><span data-ttu-id="fd4a6-124">Utilizzare hello tooadd portale di servizi Web di Microsoft Azure un endpoint</span><span class="sxs-lookup"><span data-stu-id="fd4a6-124">Use hello Microsoft Azure Web Services portal tooadd an endpoint</span></span>
1. <span data-ttu-id="fd4a6-125">In Machine Learning Studio, nella colonna sinistra hello, fare clic su servizi Web.</span><span class="sxs-lookup"><span data-stu-id="fd4a6-125">In Machine Learning Studio, on hello left navigation column, click Web Services.</span></span>
2. <span data-ttu-id="fd4a6-126">Nella parte inferiore di hello del dashboard del servizio web hello, fare clic su **anteprima endpoint Gestisci**.</span><span class="sxs-lookup"><span data-stu-id="fd4a6-126">At hello bottom of hello web service dashboard, click **Manage endpoints preview**.</span></span>
3. <span data-ttu-id="fd4a6-127">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="fd4a6-127">Click **Add**.</span></span>
4. <span data-ttu-id="fd4a6-128">Digitare un nome e una descrizione per il nuovo endpoint di hello.</span><span class="sxs-lookup"><span data-stu-id="fd4a6-128">Type a name and description for hello new endpoint.</span></span> <span data-ttu-id="fd4a6-129">Selezionare il livello di registrazione hello e indica se sono abilitati i dati di esempio.</span><span class="sxs-lookup"><span data-stu-id="fd4a6-129">Select hello logging level and whether sample data is enabled.</span></span> <span data-ttu-id="fd4a6-130">Per altre informazioni sulla registrazione, vedere [Abilitare la registrazione per i servizi Web di Machine Learning](machine-learning-web-services-logging.md).</span><span class="sxs-lookup"><span data-stu-id="fd4a6-130">For more information on logging, see [Enable logging for Machine Learning web services](machine-learning-web-services-logging.md).</span></span>

### <a name="use-hello-azure-classic-portal-tooadd-an-endpoint"></a><span data-ttu-id="fd4a6-131">Utilizzare hello Azure tooadd portale classico un endpoint</span><span class="sxs-lookup"><span data-stu-id="fd4a6-131">Use hello Azure classic portal tooadd an endpoint</span></span>
1. <span data-ttu-id="fd4a6-132">Accedi toohello [portale di Azure classico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="fd4a6-132">Sign in toohello [classic Azure portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="fd4a6-133">Nel menu a sinistra di hello, fare clic su **Machine Learning**.</span><span class="sxs-lookup"><span data-stu-id="fd4a6-133">In hello left menu, click **Machine Learning**.</span></span>
3. <span data-ttu-id="fd4a6-134">In Nome fare clic sull'area di lavoro e quindi su **Servizi Web**.</span><span class="sxs-lookup"><span data-stu-id="fd4a6-134">Under Name, click your workspace and then click **Web Services**.</span></span>
4. <span data-ttu-id="fd4a6-135">In Nome fare clic su **Census Model [predictive exp.]**.</span><span class="sxs-lookup"><span data-stu-id="fd4a6-135">Under Name, click **Census Model [predictive exp.]**.</span></span>
5. <span data-ttu-id="fd4a6-136">Nella parte inferiore di hello della pagina hello, fare clic su **Aggiungi Endpoint**.</span><span class="sxs-lookup"><span data-stu-id="fd4a6-136">At hello bottom of hello page, click **Add Endpoint**.</span></span> <span data-ttu-id="fd4a6-137">Per altre informazioni sull'aggiunta di endpoint, vedere [Creazione di endpoint](machine-learning-create-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="fd4a6-137">For more information on adding endpoints, see [Creating Endpoints](machine-learning-create-endpoint.md).</span></span> 

## <a name="update-hello-added-endpoints-trained-model"></a><span data-ttu-id="fd4a6-138">Aggiunta di hello aggiornamento modello con training dell'endpoint</span><span class="sxs-lookup"><span data-stu-id="fd4a6-138">Update hello added endpoint’s Trained Model</span></span>
<span data-ttu-id="fd4a6-139">processo di toocomplete i hello, è necessario aggiornare il modello con training di hello di hello nuovo endpoint in cui è stato aggiunto.</span><span class="sxs-lookup"><span data-stu-id="fd4a6-139">toocomplete hello retraining process, you must update hello trained model of hello new endpoint that you added.</span></span>

* <span data-ttu-id="fd4a6-140">Se è stato aggiunto nuovo endpoint hello usando il portale di Azure classico di hello, è possibile fare clic sul nome dell'endpoint di hello nuovo nel portale di hello quindi hello **UpdateResource** collegamento URL hello tooget è necessario il modello dell'endpoint di tooupdate hello.</span><span class="sxs-lookup"><span data-stu-id="fd4a6-140">If you added hello new endpoint using hello classic Azure portal, you can click hello new endpoint's name in hello portal, then hello **UpdateResource** link tooget hello URL you would need tooupdate hello endpoint's model.</span></span>
* <span data-ttu-id="fd4a6-141">Se si aggiungono endpoint hello mediante il codice di esempio hello, sono inclusi percorso dell'URL della Guida hello identificato da hello *HelpLocationURL* valore nell'output di hello.</span><span class="sxs-lookup"><span data-stu-id="fd4a6-141">If you added hello endpoint using hello sample code, this includes location of hello help URL identified by hello *HelpLocationURL* value in hello output.</span></span>

<span data-ttu-id="fd4a6-142">tooretrieve hello percorso URL:</span><span class="sxs-lookup"><span data-stu-id="fd4a6-142">tooretrieve hello path URL:</span></span>

1. <span data-ttu-id="fd4a6-143">Copiare e incollare l'URL di hello nel browser.</span><span class="sxs-lookup"><span data-stu-id="fd4a6-143">Copy and paste hello URL into your browser.</span></span>
2. <span data-ttu-id="fd4a6-144">Fare clic sul collegamento di aggiornamento risorsa hello.</span><span class="sxs-lookup"><span data-stu-id="fd4a6-144">Click hello Update Resource link.</span></span>
3. <span data-ttu-id="fd4a6-145">Copiare hello POST URL della richiesta PATCH hello.</span><span class="sxs-lookup"><span data-stu-id="fd4a6-145">Copy hello POST URL of hello PATCH request.</span></span> <span data-ttu-id="fd4a6-146">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="fd4a6-146">For example:</span></span>
   
     <span data-ttu-id="fd4a6-147">PATCH URL: https://management.azureml.net/workspaces/00bf70534500b34rebfa1843d6/webservices/af3er32ad393852f9b30ac9a35b/endpoints/newendpoint2</span><span class="sxs-lookup"><span data-stu-id="fd4a6-147">PATCH URL: https://management.azureml.net/workspaces/00bf70534500b34rebfa1843d6/webservices/af3er32ad393852f9b30ac9a35b/endpoints/newendpoint2</span></span>

<span data-ttu-id="fd4a6-148">È ora possibile utilizzare hello tooupdate di modello con training hello punteggio endpoint creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="fd4a6-148">You can now use hello trained model tooupdate hello scoring endpoint that you created previously.</span></span>

<span data-ttu-id="fd4a6-149">Hello codice di esempio seguente illustra come hello toouse *BaseLocation*, *RelativeLocation*, *SasBlobToken*e l'URL di PATCH tooupdate hello endpoint.</span><span class="sxs-lookup"><span data-stu-id="fd4a6-149">hello following sample code shows you how toouse hello *BaseLocation*, *RelativeLocation*, *SasBlobToken*, and PATCH URL tooupdate hello endpoint.</span></span>

    private async Task OverwriteModel()
    {
        var resourceLocations = new
        {
            Resources = new[]
            {
                new
                {
                    Name = "Census Model [trained model]",
                    Location = new AzureBlobDataReference()
                    {
                        BaseLocation = "https://esintussouthsus.blob.core.windows.net/",
                        RelativeLocation = "your endpoint relative location", //from hello output, for example: “experimentoutput/8946abfd-79d6-4438-89a9-3e5d109183/8946abfd-79d6-4438-89a9-3e5d109183.ilearner”
                        SasBlobToken = "your endpoint SAS blob token" //from hello output, for example: “?sv=2013-08-15&sr=c&sig=37lTTfngRwxCcf94%3D&st=2015-01-30T22%3A53%3A06Z&se=2015-01-31T22%3A58%3A06Z&sp=rl”
                    }
                }
            }
        };

        using (var client = new HttpClient())
        {
            client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", apiKey);

            using (var request = new HttpRequestMessage(new HttpMethod("PATCH"), endpointUrl))
            {
                request.Content = new StringContent(JsonConvert.SerializeObject(resourceLocations), System.Text.Encoding.UTF8, "application/json");
                HttpResponseMessage response = await client.SendAsync(request);

                if (!response.IsSuccessStatusCode)
                {
                    await WriteFailedResponse(response);
                }

                // Do what you want with a successful response here.
            }
        }
    }

<span data-ttu-id="fd4a6-150">Hello *apiKey* hello e *endpointUrl* per chiamata hello può essere ottenuto dal dashboard di endpoint.</span><span class="sxs-lookup"><span data-stu-id="fd4a6-150">hello *apiKey* and hello *endpointUrl* for hello call can be obtained from endpoint dashboard.</span></span>

<span data-ttu-id="fd4a6-151">valore di hello Hello *nome* parametro *risorse* deve hello corrispondenza nome risorsa di hello salvato il modello con training nella sperimentazione predittiva hello.</span><span class="sxs-lookup"><span data-stu-id="fd4a6-151">hello value of hello *Name* parameter in *Resources* should match hello Resource Name of hello saved Trained Model in hello predictive experiment.</span></span> <span data-ttu-id="fd4a6-152">hello tooget nome risorsa:</span><span class="sxs-lookup"><span data-stu-id="fd4a6-152">tooget hello Resource Name:</span></span>

1. <span data-ttu-id="fd4a6-153">Accedi toohello [portale di Azure classico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="fd4a6-153">Sign in toohello [classic Azure portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="fd4a6-154">Nel menu a sinistra di hello, fare clic su **Machine Learning**.</span><span class="sxs-lookup"><span data-stu-id="fd4a6-154">In hello left menu, click **Machine Learning**.</span></span>
3. <span data-ttu-id="fd4a6-155">In Nome fare clic sull'area di lavoro e quindi su **Servizi Web**.</span><span class="sxs-lookup"><span data-stu-id="fd4a6-155">Under Name, click your workspace and then click **Web Services**.</span></span>
4. <span data-ttu-id="fd4a6-156">In Nome fare clic su **Census Model [predictive exp.]**.</span><span class="sxs-lookup"><span data-stu-id="fd4a6-156">Under Name, click **Census Model [predictive exp.]**.</span></span>
5. <span data-ttu-id="fd4a6-157">Fare clic su nuovo endpoint hello che è stato aggiunto.</span><span class="sxs-lookup"><span data-stu-id="fd4a6-157">Click hello new endpoint you added.</span></span>
6. <span data-ttu-id="fd4a6-158">Nel dashboard di endpoint hello, fare clic su **aggiornamento risorsa**.</span><span class="sxs-lookup"><span data-stu-id="fd4a6-158">On hello endpoint dashboard, click **Update Resource**.</span></span>
7. <span data-ttu-id="fd4a6-159">Nella pagina di hello la documentazione dell'API di risorsa di aggiornamento per il servizio web hello, è possibile trovare hello **nome risorsa** in **risorse aggiornabili**.</span><span class="sxs-lookup"><span data-stu-id="fd4a6-159">On hello Update Resource API Documentation page for hello web service, you can find hello **Resource Name** under **Updatable Resources**.</span></span>

<span data-ttu-id="fd4a6-160">Se il token di firma di accesso condiviso scade prima di completare l'aggiornamento dell'endpoint di hello, è necessario eseguire un'operazione GET con hello Id processo tooobtain un nuovo token.</span><span class="sxs-lookup"><span data-stu-id="fd4a6-160">If your SAS token expires before you finish updating hello endpoint, you must perform a GET with hello Job Id tooobtain a fresh token.</span></span>

<span data-ttu-id="fd4a6-161">Quando il codice hello è stato eseguito correttamente, deve iniziare nuovo endpoint hello tramite il modello di training hello in circa 30 secondi.</span><span class="sxs-lookup"><span data-stu-id="fd4a6-161">When hello code has successfully run, hello new endpoint should start using hello retrained model in approximately 30 seconds.</span></span>

## <a name="summary"></a><span data-ttu-id="fd4a6-162">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="fd4a6-162">Summary</span></span>
<span data-ttu-id="fd4a6-163">Utilizzando hello API ripetizione di training, è possibile aggiornare hello modello con training di un servizio Web predittivo abilitazione degli scenari, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="fd4a6-163">Using hello Retraining APIs, you can update hello trained model of a predictive Web Service enabling scenarios such as:</span></span>

* <span data-ttu-id="fd4a6-164">Ripetizione periodica del training del modello con nuovi dati.</span><span class="sxs-lookup"><span data-stu-id="fd4a6-164">Periodic model retraining with new data.</span></span>
* <span data-ttu-id="fd4a6-165">Distribuzione di un modello di toocustomers con obiettivo hello di informarli del training modello di hello usando i propri dati.</span><span class="sxs-lookup"><span data-stu-id="fd4a6-165">Distribution of a model toocustomers with hello goal of letting them retrain hello model using their own data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fd4a6-166">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fd4a6-166">Next steps</span></span>
[<span data-ttu-id="fd4a6-167">Risoluzione dei problemi hello ripetizione di training di un servizio web classico di Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="fd4a6-167">Troubleshooting hello retraining of an Azure Machine Learning classic web service</span></span>](machine-learning-troubleshooting-retraining-models.md)

