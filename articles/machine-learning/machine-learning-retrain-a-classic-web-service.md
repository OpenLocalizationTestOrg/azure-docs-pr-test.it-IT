---
title: Ripetere il training di un servizio Web classico | Documentazione Microsoft
description: Informazioni su come ripetere il training di un modello a livello di codice e aggiornare il servizio Web per l'uso del modello appena sottoposto a training in Azure Machine Learning.
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
ms.openlocfilehash: 3f9f4cd5ed36262845f7a3139073ccd4e49f472a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="retrain-a-classic-web-service"></a><span data-ttu-id="0f08e-103">Ripetere il training di un servizio Web classico</span><span class="sxs-lookup"><span data-stu-id="0f08e-103">Retrain a Classic web service</span></span>
<span data-ttu-id="0f08e-104">Il servizio Web predittivo distribuito è l'endpoint dei punteggi predefinito.</span><span class="sxs-lookup"><span data-stu-id="0f08e-104">The Predictive Web Service you deployed is the default scoring endpoint.</span></span> <span data-ttu-id="0f08e-105">Gli endpoint predefiniti vengono mantenuti sincronizzati con gli esperimenti di training e di assegnazione dei punteggi di origine, quindi il modello con training per l'endpoint predefinito non può essere sostituito.</span><span class="sxs-lookup"><span data-stu-id="0f08e-105">Default endpoints are kept in sync with the original training and scoring experiments, and therefore the trained model for the default endpoint cannot be replaced.</span></span> <span data-ttu-id="0f08e-106">Per ripetere il training del servizio Web è necessario aggiungere un nuovo endpoint al servizio Web.</span><span class="sxs-lookup"><span data-stu-id="0f08e-106">To retrain the web service, you must add a new endpoint to the web service.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="0f08e-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="0f08e-107">Prerequisites</span></span>
<span data-ttu-id="0f08e-108">È necessario impostare un esperimento di training e un esperimento predittivo come illustrato in [Ripetere il training dei modelli di Machine Learning in modo programmatico](machine-learning-retrain-models-programmatically.md).</span><span class="sxs-lookup"><span data-stu-id="0f08e-108">You must have set up a training experiment and a predictive experiment as shown in [Retrain Machine Learning models programmatically](machine-learning-retrain-models-programmatically.md).</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="0f08e-109">L'esperimento predittivo deve essere distribuito come servizio Web di Machine Learning classico.</span><span class="sxs-lookup"><span data-stu-id="0f08e-109">The predictive experiment must be deployed as a Classic machine learning web service.</span></span> 
> 
> 

<span data-ttu-id="0f08e-110">Per altre informazioni sulla distribuzione di servizi Web, vedere [Distribuire un servizio Web di Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="0f08e-110">For additional information on Deploying web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

## <a name="add-a-new-endpoint"></a><span data-ttu-id="0f08e-111">Aggiungere un nuovo endpoint</span><span class="sxs-lookup"><span data-stu-id="0f08e-111">Add a new Endpoint</span></span>
<span data-ttu-id="0f08e-112">Il servizio Web predittivo distribuito contiene un endpoint di assegnazione dei punteggi predefinito che viene mantenuto sincronizzato con il modello con training originale con esperimenti di training e di assegnazione dei punteggi.</span><span class="sxs-lookup"><span data-stu-id="0f08e-112">The Predictive Web Service that you deployed contains a default scoring endpoint that is kept in sync with the original training and scoring experiments trained model.</span></span> <span data-ttu-id="0f08e-113">Per aggiornare il servizio Web con un nuovo modello con training, è necessario creare un nuovo endpoint di assegnazione dei punteggi.</span><span class="sxs-lookup"><span data-stu-id="0f08e-113">To update your web service to with a new trained model, you must create a new scoring endpoint.</span></span> 

<span data-ttu-id="0f08e-114">Per creare un nuovo endpoint dei punteggi, nel servizio Web predittivo che può essere aggiornato con il modello con training:</span><span class="sxs-lookup"><span data-stu-id="0f08e-114">To create a new scoring endpoint, on the Predictive Web Service that can be updated with the trained model:</span></span>

> [!NOTE]
> <span data-ttu-id="0f08e-115">Assicurarsi di aggiungere l'endpoint al servizio Web predittivo, non al servizio Web di training.</span><span class="sxs-lookup"><span data-stu-id="0f08e-115">Be sure you are adding the endpoint to the Predictive Web Service, not the Training Web Service.</span></span> <span data-ttu-id="0f08e-116">Se sono stati distribuiti correttamente sia un servizio Web di training che uno predittivo, verranno visualizzati due servizi Web elencati separatamente.</span><span class="sxs-lookup"><span data-stu-id="0f08e-116">If you have correctly deployed both a Training and a Predictive Web Service, you should see two separate web services listed.</span></span> <span data-ttu-id="0f08e-117">Il servizio Web predittivo deve terminare con "[predictive exp.]".</span><span class="sxs-lookup"><span data-stu-id="0f08e-117">The Predictive Web Service should end with "[predictive exp.]".</span></span>
> 
> 

<span data-ttu-id="0f08e-118">Esistono tre modi per aggiungere un nuovo endpoint a un servizio Web:</span><span class="sxs-lookup"><span data-stu-id="0f08e-118">There are three ways in which you can add a new end point to a web service:</span></span>

1. <span data-ttu-id="0f08e-119">A livello di codice</span><span class="sxs-lookup"><span data-stu-id="0f08e-119">Programmatically</span></span>
2. <span data-ttu-id="0f08e-120">Usare il portale dei servizi Web di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="0f08e-120">Use the Microsoft Azure Web Services portal</span></span>
3. <span data-ttu-id="0f08e-121">Usare il portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="0f08e-121">Use the Azure classic portal</span></span>

### <a name="programmatically-add-an-endpoint"></a><span data-ttu-id="0f08e-122">Aggiungere un endpoint a livello di codice</span><span class="sxs-lookup"><span data-stu-id="0f08e-122">Programmatically add an endpoint</span></span>
<span data-ttu-id="0f08e-123">È possibile aggiungere endpoint di assegnazione dei punteggi usando il codice di esempio disponibile in questo [repository GitHub](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="0f08e-123">You can add scoring endpoints using the sample code provided in this [github repository](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs).</span></span>

### <a name="use-the-microsoft-azure-web-services-portal-to-add-an-endpoint"></a><span data-ttu-id="0f08e-124">Usare il portale dei servizi Web di Microsoft Azure per aggiungere un endpoint</span><span class="sxs-lookup"><span data-stu-id="0f08e-124">Use the Microsoft Azure Web Services portal to add an endpoint</span></span>
1. <span data-ttu-id="0f08e-125">In Machine Learning Studio fare clic su Web Services (Servizi Web) nella colonna di spostamento a sinistra.</span><span class="sxs-lookup"><span data-stu-id="0f08e-125">In Machine Learning Studio, on the left navigation column, click Web Services.</span></span>
2. <span data-ttu-id="0f08e-126">Nella parte inferiore del dashboard dei servizi Web, fare clic su **Manage endpoints preview** (Gestisci anteprima endpoint).</span><span class="sxs-lookup"><span data-stu-id="0f08e-126">At the bottom of the web service dashboard, click **Manage endpoints preview**.</span></span>
3. <span data-ttu-id="0f08e-127">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="0f08e-127">Click **Add**.</span></span>
4. <span data-ttu-id="0f08e-128">Immettere un nome e una descrizione per il nuovo endpoint.</span><span class="sxs-lookup"><span data-stu-id="0f08e-128">Type a name and description for the new endpoint.</span></span> <span data-ttu-id="0f08e-129">Selezionare il livello di registrazione e indicare se i dati di esempio sono abilitati.</span><span class="sxs-lookup"><span data-stu-id="0f08e-129">Select the logging level and whether sample data is enabled.</span></span> <span data-ttu-id="0f08e-130">Per altre informazioni sulla registrazione, vedere [Abilitare la registrazione per i servizi Web di Machine Learning](machine-learning-web-services-logging.md).</span><span class="sxs-lookup"><span data-stu-id="0f08e-130">For more information on logging, see [Enable logging for Machine Learning web services](machine-learning-web-services-logging.md).</span></span>

### <a name="use-the-azure-classic-portal-to-add-an-endpoint"></a><span data-ttu-id="0f08e-131">Usare il portale di Azure classico per aggiungere un endpoint</span><span class="sxs-lookup"><span data-stu-id="0f08e-131">Use the Azure classic portal to add an endpoint</span></span>
1. <span data-ttu-id="0f08e-132">Accedere al [portale di Azure classico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="0f08e-132">Sign in to the [classic Azure portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="0f08e-133">Nel menu a sinistra fare clic su **Machine Learning**.</span><span class="sxs-lookup"><span data-stu-id="0f08e-133">In the left menu, click **Machine Learning**.</span></span>
3. <span data-ttu-id="0f08e-134">In Nome fare clic sull'area di lavoro e quindi su **Servizi Web**.</span><span class="sxs-lookup"><span data-stu-id="0f08e-134">Under Name, click your workspace and then click **Web Services**.</span></span>
4. <span data-ttu-id="0f08e-135">In Nome fare clic su **Census Model [predictive exp.]**.</span><span class="sxs-lookup"><span data-stu-id="0f08e-135">Under Name, click **Census Model [predictive exp.]**.</span></span>
5. <span data-ttu-id="0f08e-136">Nella parte inferiore della pagina fare clic su **Aggiungi endpoint**.</span><span class="sxs-lookup"><span data-stu-id="0f08e-136">At the bottom of the page, click **Add Endpoint**.</span></span> <span data-ttu-id="0f08e-137">Per altre informazioni sull'aggiunta di endpoint, vedere [Creazione di endpoint](machine-learning-create-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="0f08e-137">For more information on adding endpoints, see [Creating Endpoints](machine-learning-create-endpoint.md).</span></span> 

## <a name="update-the-added-endpoints-trained-model"></a><span data-ttu-id="0f08e-138">Aggiornare il modello con training dell'endpoint aggiunto</span><span class="sxs-lookup"><span data-stu-id="0f08e-138">Update the added endpoint’s Trained Model</span></span>
<span data-ttu-id="0f08e-139">Per completare il processo di ripetizione del training, è necessario aggiornare il modello con training del nuovo endpoint aggiunto.</span><span class="sxs-lookup"><span data-stu-id="0f08e-139">To complete the retraining process, you must update the trained model of the new endpoint that you added.</span></span>

* <span data-ttu-id="0f08e-140">Se il nuovo endpoint è stato aggiunto usando il portale di Azure classico, è possibile fare clic sul nome del nuovo endpoint nel portale, quindi sul collegamento **UpdateResource** per ottenere l'URL necessario per aggiornare il modello dell'endpoint.</span><span class="sxs-lookup"><span data-stu-id="0f08e-140">If you added the new endpoint using the classic Azure portal, you can click the new endpoint's name in the portal, then the **UpdateResource** link to get the URL you would need to update the endpoint's model.</span></span>
* <span data-ttu-id="0f08e-141">Se l'endpoint è stato aggiunto usando il codice di esempio, è inclusa la posizione dell'URL della guida identificato dal valore *HelpLocationURL* nell'output.</span><span class="sxs-lookup"><span data-stu-id="0f08e-141">If you added the endpoint using the sample code, this includes location of the help URL identified by the *HelpLocationURL* value in the output.</span></span>

<span data-ttu-id="0f08e-142">Per recuperare l'URL del percorso:</span><span class="sxs-lookup"><span data-stu-id="0f08e-142">To retrieve the path URL:</span></span>

1. <span data-ttu-id="0f08e-143">Copiare e incollare l'URL nel browser.</span><span class="sxs-lookup"><span data-stu-id="0f08e-143">Copy and paste the URL into your browser.</span></span>
2. <span data-ttu-id="0f08e-144">Fare clic sul collegamento Aggiorna risorsa.</span><span class="sxs-lookup"><span data-stu-id="0f08e-144">Click the Update Resource link.</span></span>
3. <span data-ttu-id="0f08e-145">Copiare l'URL POST della richiesta PATCH.</span><span class="sxs-lookup"><span data-stu-id="0f08e-145">Copy the POST URL of the PATCH request.</span></span> <span data-ttu-id="0f08e-146">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="0f08e-146">For example:</span></span>
   
     <span data-ttu-id="0f08e-147">PATCH URL: https://management.azureml.net/workspaces/00bf70534500b34rebfa1843d6/webservices/af3er32ad393852f9b30ac9a35b/endpoints/newendpoint2</span><span class="sxs-lookup"><span data-stu-id="0f08e-147">PATCH URL: https://management.azureml.net/workspaces/00bf70534500b34rebfa1843d6/webservices/af3er32ad393852f9b30ac9a35b/endpoints/newendpoint2</span></span>

<span data-ttu-id="0f08e-148">Ora è possibile usare il modello con training per aggiornare l'endpoint dei punteggi creato prima.</span><span class="sxs-lookup"><span data-stu-id="0f08e-148">You can now use the trained model to update the scoring endpoint that you created previously.</span></span>

<span data-ttu-id="0f08e-149">Il codice di esempio seguente mostra come usare *BaseLocation*, *RelativeLocation*, *SasBlobToken* e l'URL PATCH per aggiornare l'endpoint.</span><span class="sxs-lookup"><span data-stu-id="0f08e-149">The following sample code shows you how to use the *BaseLocation*, *RelativeLocation*, *SasBlobToken*, and PATCH URL to update the endpoint.</span></span>

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
                        RelativeLocation = "your endpoint relative location", //from the output, for example: “experimentoutput/8946abfd-79d6-4438-89a9-3e5d109183/8946abfd-79d6-4438-89a9-3e5d109183.ilearner”
                        SasBlobToken = "your endpoint SAS blob token" //from the output, for example: “?sv=2013-08-15&sr=c&sig=37lTTfngRwxCcf94%3D&st=2015-01-30T22%3A53%3A06Z&se=2015-01-31T22%3A58%3A06Z&sp=rl”
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

<span data-ttu-id="0f08e-150">I valori di *apiKey* e *endpointUrl* per la chiamata possono essere ottenuti dal dashboard dell'endpoint.</span><span class="sxs-lookup"><span data-stu-id="0f08e-150">The *apiKey* and the *endpointUrl* for the call can be obtained from endpoint dashboard.</span></span>

<span data-ttu-id="0f08e-151">Il valore del parametro *Name* in *Resources* deve corrispondere al nome della risorsa del modello sottoposto a training nell'esperimento predittivo.</span><span class="sxs-lookup"><span data-stu-id="0f08e-151">The value of the *Name* parameter in *Resources* should match the Resource Name of the saved Trained Model in the predictive experiment.</span></span> <span data-ttu-id="0f08e-152">Per ottenere il nome della risorsa:</span><span class="sxs-lookup"><span data-stu-id="0f08e-152">To get the Resource Name:</span></span>

1. <span data-ttu-id="0f08e-153">Accedere al [portale di Azure classico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="0f08e-153">Sign in to the [classic Azure portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="0f08e-154">Nel menu a sinistra fare clic su **Machine Learning**.</span><span class="sxs-lookup"><span data-stu-id="0f08e-154">In the left menu, click **Machine Learning**.</span></span>
3. <span data-ttu-id="0f08e-155">In Nome fare clic sull'area di lavoro e quindi su **Servizi Web**.</span><span class="sxs-lookup"><span data-stu-id="0f08e-155">Under Name, click your workspace and then click **Web Services**.</span></span>
4. <span data-ttu-id="0f08e-156">In Nome fare clic su **Census Model [predictive exp.]**.</span><span class="sxs-lookup"><span data-stu-id="0f08e-156">Under Name, click **Census Model [predictive exp.]**.</span></span>
5. <span data-ttu-id="0f08e-157">Fare clic sul nuovo endpoint aggiunto.</span><span class="sxs-lookup"><span data-stu-id="0f08e-157">Click the new endpoint you added.</span></span>
6. <span data-ttu-id="0f08e-158">Nel dashboard dell'endpoint fare clic su **Aggiorna risorsa**.</span><span class="sxs-lookup"><span data-stu-id="0f08e-158">On the endpoint dashboard, click **Update Resource**.</span></span>
7. <span data-ttu-id="0f08e-159">Nella pagina della documentazione sull'aggiornamento dell'API di risorsa per il servizio Web è possibile trovare **Nome risorsa** in **Risorse aggiornabili**.</span><span class="sxs-lookup"><span data-stu-id="0f08e-159">On the Update Resource API Documentation page for the web service, you can find the **Resource Name** under **Updatable Resources**.</span></span>

<span data-ttu-id="0f08e-160">Se il token di firma di accesso condiviso scade prima di avere terminato l'aggiornamento dell'endpoint, è necessario eseguire un'operazione GET con l'ID processo per ottenere un nuovo token.</span><span class="sxs-lookup"><span data-stu-id="0f08e-160">If your SAS token expires before you finish updating the endpoint, you must perform a GET with the Job Id to obtain a fresh token.</span></span>

<span data-ttu-id="0f08e-161">Al termine dell'esecuzione del codice, il nuovo endpoint verrà avviato con il modello di cui è stato ripetuto il training in circa 30 secondi.</span><span class="sxs-lookup"><span data-stu-id="0f08e-161">When the code has successfully run, the new endpoint should start using the retrained model in approximately 30 seconds.</span></span>

## <a name="summary"></a><span data-ttu-id="0f08e-162">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="0f08e-162">Summary</span></span>
<span data-ttu-id="0f08e-163">Usando le API per la ripetizione del training, è possibile aggiornare il modello con training di un servizio Web predittivo abilitando scenari come:</span><span class="sxs-lookup"><span data-stu-id="0f08e-163">Using the Retraining APIs, you can update the trained model of a predictive Web Service enabling scenarios such as:</span></span>

* <span data-ttu-id="0f08e-164">Ripetizione periodica del training del modello con nuovi dati.</span><span class="sxs-lookup"><span data-stu-id="0f08e-164">Periodic model retraining with new data.</span></span>
* <span data-ttu-id="0f08e-165">Distribuzione di un modello ai clienti per fare in modo che possano ripetere il training del modello con i propri dati.</span><span class="sxs-lookup"><span data-stu-id="0f08e-165">Distribution of a model to customers with the goal of letting them retrain the model using their own data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0f08e-166">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0f08e-166">Next steps</span></span>
[<span data-ttu-id="0f08e-167">Risoluzione dei problemi relativi alla ripetizione del training di un servizio Web classico di Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="0f08e-167">Troubleshooting the retraining of an Azure Machine Learning classic web service</span></span>](machine-learning-troubleshooting-retraining-models.md)

