---
title: Utilizzare un servizio Web di Machine Learning con un modello di app Web | Documentazione Microsoft
description: Usare un modello di app Web in Azure Marketplace per utilizzare un servizio Web predittivo in Azure Machine Learning.
keywords: servizio Web,messa in funzione,API REST,Machine Learning
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: e0d71683-61b9-4675-8df5-09ddc2f0d92d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye;raymondl
ms.openlocfilehash: 95aa1fa23d83ec0dcd00870179167e803bafbd16
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="consume-an-azure-machine-learning-web-service-with-a-web-app-template"></a><span data-ttu-id="92bf4-104">Utilizzare un servizio Web di Azure Machine Learning con un modello di app Web</span><span class="sxs-lookup"><span data-stu-id="92bf4-104">Consume an Azure Machine Learning web service with a web app template</span></span>

<span data-ttu-id="92bf4-105">Dopo aver sviluppato il modello predittivo e averlo distribuito come un servizio web di Azure mediante Machine Learning Studio o mediante strumenti come R o Python, è possibile accedere al modello operazionalizzato utilizzando un'API REST.</span><span class="sxs-lookup"><span data-stu-id="92bf4-105">Once you've developed your predictive model and deployed it as an Azure web service using Machine Learning Studio, or using tools such as R or Python, you can access the operationalized model using a REST API.</span></span>

<span data-ttu-id="92bf4-106">Ci sono diversi modi per utilizzare l'API REST e accedere al servizio Web.</span><span class="sxs-lookup"><span data-stu-id="92bf4-106">There are a number of ways to consume the REST API and access the web service.</span></span> <span data-ttu-id="92bf4-107">Ad esempio, è possibile scrivere un'applicazione in C#, R o Python usando il codice di esempio generato quando è stato distribuito il servizio Web, disponibile nel [portale del servizio Web di Machine Learning](https://services.azureml.net/quickstart) o nel dashboard del servizio Web in Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="92bf4-107">For example, you can write an application in C#, R, or Python using the sample code generated for you when you deployed the web service (available in the [Machine Learning Web Services Portal](https://services.azureml.net/quickstart) or in the web service dashboard in Machine Learning Studio).</span></span> <span data-ttu-id="92bf4-108">In alternativa è possibile usare la cartella di lavoro Microsoft Excel di esempio creata nello stesso momento.</span><span class="sxs-lookup"><span data-stu-id="92bf4-108">Or you can use the sample Microsoft Excel workbook created for you at the same time.</span></span>

<span data-ttu-id="92bf4-109">Il modo più rapido e semplice per accedere al servizio Web consiste però nell'usare i modelli di app Web disponibili nel [Marketplace delle app Web di Azure](https://azure.microsoft.com/marketplace/web-applications/all/).</span><span class="sxs-lookup"><span data-stu-id="92bf4-109">But the quickest and easiest way to access your web service is through the Web App Templates available in the [Azure Web App Marketplace](https://azure.microsoft.com/marketplace/web-applications/all/).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="the-azure-machine-learning-web-app-templates"></a><span data-ttu-id="92bf4-110">Modelli di app Web di Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="92bf4-110">The Azure Machine Learning Web App Templates</span></span>
<span data-ttu-id="92bf4-111">I modelli di app Web disponibili in Azure Marketplace consentono di compilare un'app Web personalizzata che riconosce i dati di input del servizio Web e i risultati previsti.</span><span class="sxs-lookup"><span data-stu-id="92bf4-111">The web app templates available in the Azure Marketplace can build a custom web app that knows your web service's input data and expected results.</span></span> <span data-ttu-id="92bf4-112">È sufficiente concedere all'app Web l'accesso al proprio servizio Web e ai dati e il modello farà il resto.</span><span class="sxs-lookup"><span data-stu-id="92bf4-112">All you need to do is give the web app access to your web service and data, and the template does the rest.</span></span>

<span data-ttu-id="92bf4-113">Sono disponibili due modelli:</span><span class="sxs-lookup"><span data-stu-id="92bf4-113">Two templates are available:</span></span>

* [<span data-ttu-id="92bf4-114">Modello di app Web del servizio di richiesta/risposta di Azure ML</span><span class="sxs-lookup"><span data-stu-id="92bf4-114">Azure ML Request-Response Service Web App Template</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlaspnettemplateforrrs/)
* [<span data-ttu-id="92bf4-115">Modello di app Web del servizio di esecuzione batch di Azure ML</span><span class="sxs-lookup"><span data-stu-id="92bf4-115">Azure ML Batch Execution Service Web App Template</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/)

<span data-ttu-id="92bf4-116">Ogni modello crea un'applicazione ASP.NET di esempio, usando l'URI dell'APIe la chiave per il servizio Web, e lao distribuisce come sito Web in Azure.</span><span class="sxs-lookup"><span data-stu-id="92bf4-116">Each template creates a sample ASP.NET application, using the API URI and Key for your web service, and deploys it as a web site to Azure.</span></span> <span data-ttu-id="92bf4-117">Il modello di richiesta-risposta del servizio (RRS) crea un'app Web che consente di inviare una singola riga di dati al servizio Web per ottenere un singolo risultato.</span><span class="sxs-lookup"><span data-stu-id="92bf4-117">The Request-Response Service (RRS) template creates a web app that allows you to send a single row of data to the web service to get a single result.</span></span> <span data-ttu-id="92bf4-118">Il modello di servizio di esecuzione batch (BES) crea un'app Web che consente di inviare numerose righe di dati per ottenere più risultati.</span><span class="sxs-lookup"><span data-stu-id="92bf4-118">The Batch Execution Service (BES) template creates a web app that allows you to send many rows of data to get multiple results.</span></span>

<span data-ttu-id="92bf4-119">Per usare questi modelli non è necessario alcuna codifica.</span><span class="sxs-lookup"><span data-stu-id="92bf4-119">No coding is required to use these templates.</span></span> <span data-ttu-id="92bf4-120">È sufficiente implementare l'URI e la chiave API per ottenere la compilazione automatica dell'applicazione da parte del modello.</span><span class="sxs-lookup"><span data-stu-id="92bf4-120">You just supply the API Key and URI, and the template builds the application for you.</span></span>

<span data-ttu-id="92bf4-121">Per ottenere la chiave API e l'URI della richiesta per un servizio web:</span><span class="sxs-lookup"><span data-stu-id="92bf4-121">To get the API key and Request URI for a web service:</span></span>

1. <span data-ttu-id="92bf4-122">Nel [portale dei servizi Web](https://services.azureml.net/quickstart), per un nuovo servizio Web, fare clic su **Servizi Web** nella parte superiore.</span><span class="sxs-lookup"><span data-stu-id="92bf4-122">In the [Web Services Portal](https://services.azureml.net/quickstart), for a New web service, click **Web Services** at the top.</span></span> <span data-ttu-id="92bf4-123">Per un servizio Web classico, fare clic su **Servizi Web classici**.</span><span class="sxs-lookup"><span data-stu-id="92bf4-123">Or for a Classic web service click **Classic Web Services**.</span></span>
2. <span data-ttu-id="92bf4-124">Selezionare il servizio Web a cui si desidera accedere.</span><span class="sxs-lookup"><span data-stu-id="92bf4-124">Click the web service you want to access.</span></span>
3. <span data-ttu-id="92bf4-125">Per un servizio Web classico, fare clic sull'endpoint a cui si desidera accedere.</span><span class="sxs-lookup"><span data-stu-id="92bf4-125">For a Classic web service, click the endpoint you want to access.</span></span>
4. <span data-ttu-id="92bf4-126">Fare clic su **Consumo** nella parte superiore.</span><span class="sxs-lookup"><span data-stu-id="92bf4-126">Click **Consume** at the top.</span></span>
5. <span data-ttu-id="92bf4-127">Copiare la chiave **primaria** o **secondaria** e salvarla.</span><span class="sxs-lookup"><span data-stu-id="92bf4-127">Copy the **Primary** or **Secondary Key** and save it.</span></span>
6. <span data-ttu-id="92bf4-128">Se si sta creando un modello di Servizio di richiesta-risposta (RRS), copiare l'URI **richiesta-risposta** e salvarlo.</span><span class="sxs-lookup"><span data-stu-id="92bf4-128">If you're creating a Request-Response Service (RRS) template, copy the **Request-Response** URI and save it.</span></span> <span data-ttu-id="92bf4-129">Se si sta creando un modello di Servizio Esecuzione batch (BES), copiare l'URI delle **richieste Batch** e salvarlo.</span><span class="sxs-lookup"><span data-stu-id="92bf4-129">If you're creating a Batch Execution Service (BES) template, copy the **Batch Requests** URI and save it.</span></span>


## <a name="how-to-use-the-request-response-service-rrs-template"></a><span data-ttu-id="92bf4-130">Come usare il modello di servizio di richiesta-risposta (RRS)</span><span class="sxs-lookup"><span data-stu-id="92bf4-130">How to use the Request-Response Service (RRS) template</span></span>
<span data-ttu-id="92bf4-131">Seguire questa procedura per usare il modello di app Web di RRS, come illustrato nella figura seguente.</span><span class="sxs-lookup"><span data-stu-id="92bf4-131">Follow these steps to use the RRS web app template, as shown in the following diagram.</span></span>

![Processo per l'uso del modello Web RRS][image1]


<!--    ![API Key][image3] -->

<!-- This value will look like this:
   
        https://ussouthcentral.services.azureml.net/workspaces/<workspace-id>/services/<service-id>/execute?api-version=2.0&details=true
   
    ![Request URI][image4] -->

1. <span data-ttu-id="92bf4-133">Passare al [portale di Azure](https://portal.azure.com), fare clic su **Accedi** e quindi su **Nuovo**, cercare e selezionare **Azure ML Request-Response Service Web App** (App Web del Servizio di richiesta-risposta di Azure ML) e quindi fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="92bf4-133">Go to the [Azure portal](https://portal.azure.com), **Login**, click **New**, search for and select **Azure ML Request-Response Service Web App**, then click **Create**.</span></span> 
   
   * <span data-ttu-id="92bf4-134">Assegnare all'app Web un nome univoco.</span><span class="sxs-lookup"><span data-stu-id="92bf4-134">Give your web app a unique name.</span></span> <span data-ttu-id="92bf4-135">L'URL dell'app Web sarà il nome seguito da `.azurewebsites.net.` Ad esempio, `http://carprediction.azurewebsites.net.`</span><span class="sxs-lookup"><span data-stu-id="92bf4-135">The URL of the web app will be this name followed by `.azurewebsites.net.` For example, `http://carprediction.azurewebsites.net.`</span></span>
   * <span data-ttu-id="92bf4-136">Selezionare la sottoscrizione di Azure e servizi in cui è in esecuzione il servizio Web.</span><span class="sxs-lookup"><span data-stu-id="92bf4-136">Select the Azure subscription and services under which your web service is running.</span></span>
   * <span data-ttu-id="92bf4-137">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="92bf4-137">Click **Create**.</span></span>
     
     ![Crea app Web][image5]

4. <span data-ttu-id="92bf4-139">Quando Azure ha terminato la distribuzione dell'app Web, fare clic su **URL** nella pagina delle impostazioni dell'app Web in Azure o immettere l'URL in un browser web.</span><span class="sxs-lookup"><span data-stu-id="92bf4-139">When Azure has finished deploying the web app, click the **URL** on the web app settings page in Azure, or enter the URL in a web browser.</span></span> <span data-ttu-id="92bf4-140">Ad esempio, `http://carprediction.azurewebsites.net.`</span><span class="sxs-lookup"><span data-stu-id="92bf4-140">For example, `http://carprediction.azurewebsites.net.`</span></span>
5. <span data-ttu-id="92bf4-141">Quando l'app Web viene eseguita per la prima volta, verranno richiesti i valori di **API Post URL** (URL post API) e **API Key** (Chiave API).</span><span class="sxs-lookup"><span data-stu-id="92bf4-141">When the web app first runs it will ask you for the **API Post URL** and **API Key**.</span></span>
   <span data-ttu-id="92bf4-142">Immettere i valori salvati in precedenza (rispettivamente l'**URI della richiesta** e la **chiave API**).</span><span class="sxs-lookup"><span data-stu-id="92bf4-142">Enter the values you saved earlier (**Request URI** and **API Key**, respectively).</span></span>
     
     <span data-ttu-id="92bf4-143">Fare clic su **Submit**.</span><span class="sxs-lookup"><span data-stu-id="92bf4-143">Click **Submit**.</span></span>
     
     ![Immettere Post URI e API Key][image6]

6. <span data-ttu-id="92bf4-145">L'app Web visualizza la propria pagina **Configurazione app Web** con le impostazioni del servizio Web correnti.</span><span class="sxs-lookup"><span data-stu-id="92bf4-145">The web app displays its **Web App Configuration** page with the current web service settings.</span></span> <span data-ttu-id="92bf4-146">Qui è possibile apportare modifiche alle impostazioni usate dall'app Web.</span><span class="sxs-lookup"><span data-stu-id="92bf4-146">Here you can make changes to the settings used by the web app.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="92bf4-147">La modifica delle impostazioni in questa pagina si applicano solo a questa app Web.</span><span class="sxs-lookup"><span data-stu-id="92bf4-147">Changing the settings here only changes them for this web app.</span></span> <span data-ttu-id="92bf4-148">Non vengono modificate le impostazioni predefinite del servizio Web.</span><span class="sxs-lookup"><span data-stu-id="92bf4-148">It doesn't change the default settings of your web service.</span></span> <span data-ttu-id="92bf4-149">Ad esempio, se si modifica la voce **Description** qui, non viene modificata la descrizione indicata nel dashboard del servizio Web in Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="92bf4-149">For example, if you change the **Description** here it doesn't change the description shown on the web service dashboard in Machine Learning Studio.</span></span>
   > 
   > 
   
    <span data-ttu-id="92bf4-150">Al termine, fare clic su **Save changes** (Salva modifiche) e quindi fare clic su **Go to Home Page** (Vai a home page).</span><span class="sxs-lookup"><span data-stu-id="92bf4-150">When you're done, click **Save changes**, and then click **Go to Home Page**.</span></span>

7. <span data-ttu-id="92bf4-151">Dalla home page è possibile immettere i valori da inviare al servizio Web.</span><span class="sxs-lookup"><span data-stu-id="92bf4-151">From the home page you can enter values to send to your web service.</span></span> <span data-ttu-id="92bf4-152">Al termine fare clic su **Invia** e verrà restituito il risultato.</span><span class="sxs-lookup"><span data-stu-id="92bf4-152">Click **Submit** when you're done, and the result will be returned.</span></span>

<span data-ttu-id="92bf4-153">Se si vuole ritornare alla pagina **Configuration** (Configurazione), andare alla pagina `setting.aspx` dell'app Web.</span><span class="sxs-lookup"><span data-stu-id="92bf4-153">If you want to return to the **Configuration** page, go to the `setting.aspx` page of the web app.</span></span> <span data-ttu-id="92bf4-154">Ad esempio: `http://carprediction.azurewebsites.net/setting.aspx.` Verrà richiesto di immettere di nuovo la chiave dell'API richiesta per accedere alla pagina e aggiornare le impostazioni.</span><span class="sxs-lookup"><span data-stu-id="92bf4-154">For example: `http://carprediction.azurewebsites.net/setting.aspx.` You will be prompted to enter the API key again - you need that to access the page and update the settings.</span></span>

<span data-ttu-id="92bf4-155">È possibile arrestare, riavviare o eliminare l'app Web nel portale di Azure come qualsiasi altra app Web.</span><span class="sxs-lookup"><span data-stu-id="92bf4-155">You can stop, restart, or delete the web app in the Azure portal like any other web app.</span></span> <span data-ttu-id="92bf4-156">Mentre è in esecuzione, è possibile accedere all'indirizzo Web della home page e immettere nuovi valori.</span><span class="sxs-lookup"><span data-stu-id="92bf4-156">As long as it is running you can browse to the home web address and enter new values.</span></span>

## <a name="how-to-use-the-batch-execution-service-bes-template"></a><span data-ttu-id="92bf4-157">Come usare il modello di servizio di esecuzione batch (BES)</span><span class="sxs-lookup"><span data-stu-id="92bf4-157">How to use the Batch Execution Service (BES) template</span></span>
<span data-ttu-id="92bf4-158">È possibile usare il modello di app Web BES così come si usa il modello RRS, ad eccezione del fatto che l'app Web creata consentirà di inviare più righe di dati e ricevere più risultati.</span><span class="sxs-lookup"><span data-stu-id="92bf4-158">You can use the BES web app template in the same way as the RRS template, except that the web app that's created will allow you to submit multiple rows of data and receive multiple results.</span></span>

<span data-ttu-id="92bf4-159">I valori di input per un servizio Web di esecuzione batch possono provenire da Archiviazione di Azure o da un file locale. I risultati vengono archiviati in un contenitore di Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="92bf4-159">The input values for a batch execution web service can come from Azure storage or a local file; the results are stored in an Azure storage container.</span></span>
<span data-ttu-id="92bf4-160">È quindi necessario un contenitore di archiviazione di Azure per contenere i risultati restituiti dall'app Web e sarà necessario preparare i dati di input.</span><span class="sxs-lookup"><span data-stu-id="92bf4-160">So, you'll need an Azure storage container to hold the results returned by the web app, and you'll need to get your input data ready.</span></span>

![Processo per l'uso del modello Web BES][image2]

1. <span data-ttu-id="92bf4-162">Seguire la stessa procedura per creare l'app Web BES come modello RRS, oppure passare al [Azure ML Batch Execution Service Web App Template](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/) (Modello di app Web del servizio di esecuzione batch di Azure ML) per aprire il modello BES in Azure Marketplace e fare clic su **Crea app Web**.</span><span class="sxs-lookup"><span data-stu-id="92bf4-162">Follow the same procedure to create the BES web app as for the RRS template, except go to [Azure ML Batch Execution Service Web App Template](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/) to open the BES template on Azure Marketplace and click **Create Web App**.</span></span>

2. <span data-ttu-id="92bf4-163">Per specificare dove archiviare i risultati, immettere le informazioni relative al contenitore di destinazione nella home page dell'app Web.</span><span class="sxs-lookup"><span data-stu-id="92bf4-163">To specify where you want the results stored, enter the destination container information on the web app home page.</span></span> <span data-ttu-id="92bf4-164">Specificare anche dove l'app Web può ottenere i valori di input, ad esempio in un file locale o in un contenitore di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="92bf4-164">Also specify where the web app can get the input values, either in a local file or an Azure storage container.</span></span>
   <span data-ttu-id="92bf4-165">Fare clic su **Submit**.</span><span class="sxs-lookup"><span data-stu-id="92bf4-165">Click **Submit**.</span></span>
   
    ![Informazioni sull'archiviazione][image7]

<span data-ttu-id="92bf4-167">L'app Web visualizzerà una pagina con lo stato del processo.</span><span class="sxs-lookup"><span data-stu-id="92bf4-167">The web app will display a page with job status.</span></span>
<span data-ttu-id="92bf4-168">Una volta completato il processo, verrà indicato il percorso dei risultati nell'archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="92bf4-168">When the job has completed you'll be given the location of the results in Azure blob storage.</span></span> <span data-ttu-id="92bf4-169">È possibile scegliere di scaricare i risultati in un file locale.</span><span class="sxs-lookup"><span data-stu-id="92bf4-169">You also have the option of downloading the results to a local file.</span></span>

## <a name="for-more-information"></a><span data-ttu-id="92bf4-170">Per altre informazioni</span><span class="sxs-lookup"><span data-stu-id="92bf4-170">For more information</span></span>
<span data-ttu-id="92bf4-171">Per altre informazioni su...</span><span class="sxs-lookup"><span data-stu-id="92bf4-171">To learn more about...</span></span>

* <span data-ttu-id="92bf4-172">creazione di un esperimento di apprendimento automatico con Machine Learning Studio, vedere [Esercitazione di Machine Learning: Creare il primo esperimento in Azure Machine Learning Studio](machine-learning-create-experiment.md)</span><span class="sxs-lookup"><span data-stu-id="92bf4-172">creating a machine learning experiment with Machine Learning Studio, see [Create your first experiment in Azure Machine Learning Studio](machine-learning-create-experiment.md)</span></span>
* <span data-ttu-id="92bf4-173">come distribuire l'esperimento di Machine Learning come servizio Web, vedere [Distribuire un servizio Web di Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md)</span><span class="sxs-lookup"><span data-stu-id="92bf4-173">how to deploy your machine learning experiment as a web service, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md)</span></span>
* <span data-ttu-id="92bf4-174">altre modalità di accesso al servizio Web, vedere [Come usare un servizio Web di Azure Machine Learning](machine-learning-consume-web-services.md)</span><span class="sxs-lookup"><span data-stu-id="92bf4-174">other ways to access your web service, see [How to consume an Azure Machine Learning Web service](machine-learning-consume-web-services.md)</span></span>

[image1]: media/machine-learning-consume-web-service-with-web-app-template/rrs-web-template-flow.png
[image2]: media/machine-learning-consume-web-service-with-web-app-template/bes-web-template-flow.png
[image3]: media/machine-learning-consume-web-service-with-web-app-template/api-key.png
[image4]: media/machine-learning-consume-web-service-with-web-app-template/post-uri.png
[image5]: media/machine-learning-consume-web-service-with-web-app-template/create-web-app.png
[image6]: media/machine-learning-consume-web-service-with-web-app-template/web-service-info.png
[image7]: media/machine-learning-consume-web-service-with-web-app-template/storage.png
