---
title: un servizio web Machine Learning con un modello di app web aaaConsume | Documenti Microsoft
description: Utilizzare un modello di applicazione web in Azure Marketplace tooconsume un servizio web predittivo in Azure Machine Learning.
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
ms.openlocfilehash: 1199377bead470807d58ca7f7a667175cbb88450
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="consume-an-azure-machine-learning-web-service-with-a-web-app-template"></a><span data-ttu-id="7f925-104">Utilizzare un servizio Web di Azure Machine Learning con un modello di app Web</span><span class="sxs-lookup"><span data-stu-id="7f925-104">Consume an Azure Machine Learning web service with a web app template</span></span>

<span data-ttu-id="7f925-105">Dopo aver sviluppato il modello predittivo e viene distribuito come servizio web di Azure tramite Machine Learning Studio o mediante strumenti quali R o Python, è possibile accedere hello operativi i modello utilizzando un'API REST.</span><span class="sxs-lookup"><span data-stu-id="7f925-105">Once you've developed your predictive model and deployed it as an Azure web service using Machine Learning Studio, or using tools such as R or Python, you can access hello operationalized model using a REST API.</span></span>

<span data-ttu-id="7f925-106">Esistono diversi modi tooconsume hello API REST e accesso hello servizio web.</span><span class="sxs-lookup"><span data-stu-id="7f925-106">There are a number of ways tooconsume hello REST API and access hello web service.</span></span> <span data-ttu-id="7f925-107">Ad esempio, è possibile scrivere un'applicazione in c#, R, o Python mediante hello codice generato automaticamente al momento della distribuzione del servizio web hello di esempio (disponibile in hello [portale dei servizi Web Machine Learning](https://services.azureml.net/quickstart) o nel dashboard del servizio web hello in Machine Learning Studio).</span><span class="sxs-lookup"><span data-stu-id="7f925-107">For example, you can write an application in C#, R, or Python using hello sample code generated for you when you deployed hello web service (available in hello [Machine Learning Web Services Portal](https://services.azureml.net/quickstart) or in hello web service dashboard in Machine Learning Studio).</span></span> <span data-ttu-id="7f925-108">Oppure è possibile utilizzare una cartella di Microsoft Excel di esempio hello creata alla hello contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="7f925-108">Or you can use hello sample Microsoft Excel workbook created for you at hello same time.</span></span>

<span data-ttu-id="7f925-109">Ma hello tooaccess più semplice e rapido è il servizio web tramite i modelli di App Web hello disponibili in hello [App Web di Azure Marketplace](https://azure.microsoft.com/marketplace/web-applications/all/).</span><span class="sxs-lookup"><span data-stu-id="7f925-109">But hello quickest and easiest way tooaccess your web service is through hello Web App Templates available in hello [Azure Web App Marketplace](https://azure.microsoft.com/marketplace/web-applications/all/).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="hello-azure-machine-learning-web-app-templates"></a><span data-ttu-id="7f925-110">Modelli di App Web di Azure Machine Learning Hello</span><span class="sxs-lookup"><span data-stu-id="7f925-110">hello Azure Machine Learning Web App Templates</span></span>
<span data-ttu-id="7f925-111">modelli di app web Hello disponibili in Azure Marketplace hello è possono compilare un'app web personalizzato in grado di dati di input del servizio web e i risultati previsti.</span><span class="sxs-lookup"><span data-stu-id="7f925-111">hello web app templates available in hello Azure Marketplace can build a custom web app that knows your web service's input data and expected results.</span></span> <span data-ttu-id="7f925-112">È sufficiente toodo è di fornire dati e il servizio web di hello web app accesso tooyour e modello hello hello rest.</span><span class="sxs-lookup"><span data-stu-id="7f925-112">All you need toodo is give hello web app access tooyour web service and data, and hello template does hello rest.</span></span>

<span data-ttu-id="7f925-113">Sono disponibili due modelli:</span><span class="sxs-lookup"><span data-stu-id="7f925-113">Two templates are available:</span></span>

* [<span data-ttu-id="7f925-114">Modello di app Web del servizio di richiesta/risposta di Azure ML</span><span class="sxs-lookup"><span data-stu-id="7f925-114">Azure ML Request-Response Service Web App Template</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlaspnettemplateforrrs/)
* [<span data-ttu-id="7f925-115">Modello di app Web del servizio di esecuzione batch di Azure ML</span><span class="sxs-lookup"><span data-stu-id="7f925-115">Azure ML Batch Execution Service Web App Template</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/)

<span data-ttu-id="7f925-116">Ogni modello crea un'applicazione ASP.NET di esempio, con hello URI API e la chiave per il servizio web e lo distribuisce come tooAzure un sito web.</span><span class="sxs-lookup"><span data-stu-id="7f925-116">Each template creates a sample ASP.NET application, using hello API URI and Key for your web service, and deploys it as a web site tooAzure.</span></span> <span data-ttu-id="7f925-117">modello di servizio richiesta-risposta (RR) Hello crea un'app web che consente di toosend una singola riga di dati toohello web servizio tooget un singolo risultato.</span><span class="sxs-lookup"><span data-stu-id="7f925-117">hello Request-Response Service (RRS) template creates a web app that allows you toosend a single row of data toohello web service tooget a single result.</span></span> <span data-ttu-id="7f925-118">modello di servizio esecuzione Batch (BES) Hello crea un'app web che consente di toosend numerose righe di dati tooget più risultati.</span><span class="sxs-lookup"><span data-stu-id="7f925-118">hello Batch Execution Service (BES) template creates a web app that allows you toosend many rows of data tooget multiple results.</span></span>

<span data-ttu-id="7f925-119">Nessun tipo di codifica è obbligatorio toouse questi modelli.</span><span class="sxs-lookup"><span data-stu-id="7f925-119">No coding is required toouse these templates.</span></span> <span data-ttu-id="7f925-120">È sufficiente specificare hello chiave API e l'URI e il modello di hello compila l'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="7f925-120">You just supply hello API Key and URI, and hello template builds hello application for you.</span></span>

<span data-ttu-id="7f925-121">chiave API hello tooget e l'URI della richiesta per un servizio web:</span><span class="sxs-lookup"><span data-stu-id="7f925-121">tooget hello API key and Request URI for a web service:</span></span>

1. <span data-ttu-id="7f925-122">In hello [portale dei servizi Web](https://services.azureml.net/quickstart), per un nuovo servizio web, fare clic su **servizi Web** nella parte superiore di hello.</span><span class="sxs-lookup"><span data-stu-id="7f925-122">In hello [Web Services Portal](https://services.azureml.net/quickstart), for a New web service, click **Web Services** at hello top.</span></span> <span data-ttu-id="7f925-123">Per un servizio Web classico, fare clic su **Servizi Web classici**.</span><span class="sxs-lookup"><span data-stu-id="7f925-123">Or for a Classic web service click **Classic Web Services**.</span></span>
2. <span data-ttu-id="7f925-124">Fare clic su servizio web di hello da tooaccess.</span><span class="sxs-lookup"><span data-stu-id="7f925-124">Click hello web service you want tooaccess.</span></span>
3. <span data-ttu-id="7f925-125">Per un servizio web classica, fare clic sull'endpoint hello desiderato tooaccess.</span><span class="sxs-lookup"><span data-stu-id="7f925-125">For a Classic web service, click hello endpoint you want tooaccess.</span></span>
4. <span data-ttu-id="7f925-126">Fare clic su **consumare** nella parte superiore di hello.</span><span class="sxs-lookup"><span data-stu-id="7f925-126">Click **Consume** at hello top.</span></span>
5. <span data-ttu-id="7f925-127">Hello copia **primario** o **chiave secondaria** e salvarlo.</span><span class="sxs-lookup"><span data-stu-id="7f925-127">Copy hello **Primary** or **Secondary Key** and save it.</span></span>
6. <span data-ttu-id="7f925-128">Se si sta creando un modello di servizio richiesta-risposta (RR), copiare hello **richiesta-risposta** URI e salvarlo.</span><span class="sxs-lookup"><span data-stu-id="7f925-128">If you're creating a Request-Response Service (RRS) template, copy hello **Request-Response** URI and save it.</span></span> <span data-ttu-id="7f925-129">Se si sta creando un modello di servizio esecuzione Batch (BES), copiare hello **richieste Batch** URI e salvarlo.</span><span class="sxs-lookup"><span data-stu-id="7f925-129">If you're creating a Batch Execution Service (BES) template, copy hello **Batch Requests** URI and save it.</span></span>


## <a name="how-toouse-hello-request-response-service-rrs-template"></a><span data-ttu-id="7f925-130">Come toouse hello modello richiesta-risposta del servizio (RR)</span><span class="sxs-lookup"><span data-stu-id="7f925-130">How toouse hello Request-Response Service (RRS) template</span></span>
<span data-ttu-id="7f925-131">Seguire questi passaggi toouse hello RR app modello web, come illustrato nel seguente diagramma hello.</span><span class="sxs-lookup"><span data-stu-id="7f925-131">Follow these steps toouse hello RRS web app template, as shown in hello following diagram.</span></span>

![Modello di processo toouse RR web][image1]


<!--    ![API Key][image3] -->

<!-- This value will look like this:
   
        https://ussouthcentral.services.azureml.net/workspaces/<workspace-id>/services/<service-id>/execute?api-version=2.0&details=true
   
    ![Request URI][image4] -->

1. <span data-ttu-id="7f925-133">Passare toohello [portale di Azure](https://portal.azure.com), **accesso**, fare clic su **New**, cercare e selezionare **Azure ML richiesta-risposta del servizio Web App**, quindi fare clic su **Creare**.</span><span class="sxs-lookup"><span data-stu-id="7f925-133">Go toohello [Azure portal](https://portal.azure.com), **Login**, click **New**, search for and select **Azure ML Request-Response Service Web App**, then click **Create**.</span></span> 
   
   * <span data-ttu-id="7f925-134">Assegnare all'app Web un nome univoco.</span><span class="sxs-lookup"><span data-stu-id="7f925-134">Give your web app a unique name.</span></span> <span data-ttu-id="7f925-135">URL di Hello dell'app web hello sarà il nome seguito da `.azurewebsites.net.` , ad esempio,`http://carprediction.azurewebsites.net.`</span><span class="sxs-lookup"><span data-stu-id="7f925-135">hello URL of hello web app will be this name followed by `.azurewebsites.net.` For example, `http://carprediction.azurewebsites.net.`</span></span>
   * <span data-ttu-id="7f925-136">Selezionare servizi e hello sottoscrizione di Azure in cui è in esecuzione il servizio web.</span><span class="sxs-lookup"><span data-stu-id="7f925-136">Select hello Azure subscription and services under which your web service is running.</span></span>
   * <span data-ttu-id="7f925-137">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="7f925-137">Click **Create**.</span></span>
     
     ![Crea app Web][image5]

4. <span data-ttu-id="7f925-139">Quando Azure ha completato la distribuzione di app web hello, fare clic su hello **URL** hello pagina Impostazioni di app web in Azure, o immettere l'URL di hello in un web browser.</span><span class="sxs-lookup"><span data-stu-id="7f925-139">When Azure has finished deploying hello web app, click hello **URL** on hello web app settings page in Azure, or enter hello URL in a web browser.</span></span> <span data-ttu-id="7f925-140">Ad esempio, `http://carprediction.azurewebsites.net.`</span><span class="sxs-lookup"><span data-stu-id="7f925-140">For example, `http://carprediction.azurewebsites.net.`</span></span>
5. <span data-ttu-id="7f925-141">Quando hello prima esecuzione applicazione web, verrà chiesto di hello **API Post URL** e **chiave API**.</span><span class="sxs-lookup"><span data-stu-id="7f925-141">When hello web app first runs it will ask you for hello **API Post URL** and **API Key**.</span></span>
   <span data-ttu-id="7f925-142">Immettere i valori hello salvato in precedenza (**URI della richiesta** e **chiave API**, rispettivamente).</span><span class="sxs-lookup"><span data-stu-id="7f925-142">Enter hello values you saved earlier (**Request URI** and **API Key**, respectively).</span></span>
     
     <span data-ttu-id="7f925-143">Fare clic su **Submit**.</span><span class="sxs-lookup"><span data-stu-id="7f925-143">Click **Submit**.</span></span>
     
     ![Immettere Post URI e API Key][image6]

6. <span data-ttu-id="7f925-145">Hello web app viene visualizzata la **configurazione delle App Web** pagina con le impostazioni del servizio web corrente hello.</span><span class="sxs-lookup"><span data-stu-id="7f925-145">hello web app displays its **Web App Configuration** page with hello current web service settings.</span></span> <span data-ttu-id="7f925-146">Qui è possibile modificare le impostazioni di toohello usate dall'app web hello.</span><span class="sxs-lookup"><span data-stu-id="7f925-146">Here you can make changes toohello settings used by hello web app.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="7f925-147">Modifica delle impostazioni di hello qui solo li modifica per questa app web.</span><span class="sxs-lookup"><span data-stu-id="7f925-147">Changing hello settings here only changes them for this web app.</span></span> <span data-ttu-id="7f925-148">Non modifica le impostazioni predefinite di hello del servizio web.</span><span class="sxs-lookup"><span data-stu-id="7f925-148">It doesn't change hello default settings of your web service.</span></span> <span data-ttu-id="7f925-149">Ad esempio, se si modifica hello **descrizione** qui non modifica descrizione hello visualizzate nel dashboard del servizio web hello in Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="7f925-149">For example, if you change hello **Description** here it doesn't change hello description shown on hello web service dashboard in Machine Learning Studio.</span></span>
   > 
   > 
   
    <span data-ttu-id="7f925-150">Al termine, fare clic su **salvare modifiche**, quindi fare clic su **passare tooHome pagina**.</span><span class="sxs-lookup"><span data-stu-id="7f925-150">When you're done, click **Save changes**, and then click **Go tooHome Page**.</span></span>

7. <span data-ttu-id="7f925-151">Da hello pagina home che è possibile immettere i valori del servizio web di toosend tooyour.</span><span class="sxs-lookup"><span data-stu-id="7f925-151">From hello home page you can enter values toosend tooyour web service.</span></span> <span data-ttu-id="7f925-152">Fare clic su **Invia** quando è terminato e verrà restituito il risultato di hello.</span><span class="sxs-lookup"><span data-stu-id="7f925-152">Click **Submit** when you're done, and hello result will be returned.</span></span>

<span data-ttu-id="7f925-153">Se si desidera tooreturn toohello **configurazione** pagina, visitare toohello `setting.aspx` pagina dell'app web hello.</span><span class="sxs-lookup"><span data-stu-id="7f925-153">If you want tooreturn toohello **Configuration** page, go toohello `setting.aspx` page of hello web app.</span></span> <span data-ttu-id="7f925-154">Ad esempio: `http://carprediction.azurewebsites.net/setting.aspx.` sarà chiave hello API tooenter richiesta nuovamente, è necessario che tooaccess hello pagina e aggiornare le impostazioni di hello.</span><span class="sxs-lookup"><span data-stu-id="7f925-154">For example: `http://carprediction.azurewebsites.net/setting.aspx.` You will be prompted tooenter hello API key again - you need that tooaccess hello page and update hello settings.</span></span>

<span data-ttu-id="7f925-155">È possibile riavviare, arrestare o eliminare l'app web hello in hello portale di Azure come qualsiasi altra app web.</span><span class="sxs-lookup"><span data-stu-id="7f925-155">You can stop, restart, or delete hello web app in hello Azure portal like any other web app.</span></span> <span data-ttu-id="7f925-156">Fino a quando è in esecuzione è possibile individuare l'indirizzo web home toohello e immettere nuovi valori.</span><span class="sxs-lookup"><span data-stu-id="7f925-156">As long as it is running you can browse toohello home web address and enter new values.</span></span>

## <a name="how-toouse-hello-batch-execution-service-bes-template"></a><span data-ttu-id="7f925-157">Come toouse hello modello Servizio esecuzione Batch (BES)</span><span class="sxs-lookup"><span data-stu-id="7f925-157">How toouse hello Batch Execution Service (BES) template</span></span>
<span data-ttu-id="7f925-158">È possibile utilizzare BES hello modello applicazione web in hello stesso modo come modello di record di risorse hello, ad eccezione di app web hello creato sarà toosubmit più righe di dati e la ricezione di più risultati.</span><span class="sxs-lookup"><span data-stu-id="7f925-158">You can use hello BES web app template in hello same way as hello RRS template, except that hello web app that's created will allow you toosubmit multiple rows of data and receive multiple results.</span></span>

<span data-ttu-id="7f925-159">valori di input per un servizio web di esecuzione batch Hello possono provenire da archiviazione di Azure o un file locale. Hello risultati vengono archiviati in un contenitore di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="7f925-159">hello input values for a batch execution web service can come from Azure storage or a local file; hello results are stored in an Azure storage container.</span></span>
<span data-ttu-id="7f925-160">In tal caso, sarà necessario un toohold contenitore di archiviazione di Azure hello risultati restituiti dall'app web hello e sarà necessario tooget i dati di input pronto.</span><span class="sxs-lookup"><span data-stu-id="7f925-160">So, you'll need an Azure storage container toohold hello results returned by hello web app, and you'll need tooget your input data ready.</span></span>

![Elaborare toouse BES modello web][image2]

1. <span data-ttu-id="7f925-162">Seguire hello stesso hello toocreate procedure BES web app per modello di record di risorse hello, ad eccezione di go troppo[modello di App di Azure ML Batch esecuzione del servizio Web](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/) tooopen hello modello BES in Azure Marketplace e fare clic su **creare App Web** .</span><span class="sxs-lookup"><span data-stu-id="7f925-162">Follow hello same procedure toocreate hello BES web app as for hello RRS template, except go too[Azure ML Batch Execution Service Web App Template](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/) tooopen hello BES template on Azure Marketplace and click **Create Web App**.</span></span>

2. <span data-ttu-id="7f925-163">toospecify in cui si desidera risultati hello archiviati, immettere le informazioni sul contenitore di destinazione hello nella home page di hello web app.</span><span class="sxs-lookup"><span data-stu-id="7f925-163">toospecify where you want hello results stored, enter hello destination container information on hello web app home page.</span></span> <span data-ttu-id="7f925-164">Specificare anche dove hello web app può ottenere valori di input di hello, in un file locale o un contenitore di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="7f925-164">Also specify where hello web app can get hello input values, either in a local file or an Azure storage container.</span></span>
   <span data-ttu-id="7f925-165">Fare clic su **Submit**.</span><span class="sxs-lookup"><span data-stu-id="7f925-165">Click **Submit**.</span></span>
   
    ![Informazioni sull'archiviazione][image7]

<span data-ttu-id="7f925-167">app web Hello verrà visualizzata una pagina con lo stato del processo.</span><span class="sxs-lookup"><span data-stu-id="7f925-167">hello web app will display a page with job status.</span></span>
<span data-ttu-id="7f925-168">Completato il processo di hello verranno presentate hello percorso di hello risultati nell'archiviazione blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="7f925-168">When hello job has completed you'll be given hello location of hello results in Azure blob storage.</span></span> <span data-ttu-id="7f925-169">È anche possibile hello download hello risultati tooa del file locale.</span><span class="sxs-lookup"><span data-stu-id="7f925-169">You also have hello option of downloading hello results tooa local file.</span></span>

## <a name="for-more-information"></a><span data-ttu-id="7f925-170">Per altre informazioni</span><span class="sxs-lookup"><span data-stu-id="7f925-170">For more information</span></span>
<span data-ttu-id="7f925-171">toolearn ulteriori informazioni...</span><span class="sxs-lookup"><span data-stu-id="7f925-171">toolearn more about...</span></span>

* <span data-ttu-id="7f925-172">creazione di un esperimento di apprendimento automatico con Machine Learning Studio, vedere [Esercitazione di Machine Learning: Creare il primo esperimento in Azure Machine Learning Studio](machine-learning-create-experiment.md)</span><span class="sxs-lookup"><span data-stu-id="7f925-172">creating a machine learning experiment with Machine Learning Studio, see [Create your first experiment in Azure Machine Learning Studio](machine-learning-create-experiment.md)</span></span>
* <span data-ttu-id="7f925-173">toodeploy l'apprendimento esperimento come servizio web, vedere [distribuire un servizio web Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md)</span><span class="sxs-lookup"><span data-stu-id="7f925-173">how toodeploy your machine learning experiment as a web service, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md)</span></span>
* <span data-ttu-id="7f925-174">altri modi tooaccess il servizio web, vedere [come tooconsume un servizio Web di Azure Machine Learning](machine-learning-consume-web-services.md)</span><span class="sxs-lookup"><span data-stu-id="7f925-174">other ways tooaccess your web service, see [How tooconsume an Azure Machine Learning Web service](machine-learning-consume-web-services.md)</span></span>

[image1]: media/machine-learning-consume-web-service-with-web-app-template/rrs-web-template-flow.png
[image2]: media/machine-learning-consume-web-service-with-web-app-template/bes-web-template-flow.png
[image3]: media/machine-learning-consume-web-service-with-web-app-template/api-key.png
[image4]: media/machine-learning-consume-web-service-with-web-app-template/post-uri.png
[image5]: media/machine-learning-consume-web-service-with-web-app-template/create-web-app.png
[image6]: media/machine-learning-consume-web-service-with-web-app-template/web-service-info.png
[image7]: media/machine-learning-consume-web-service-with-web-app-template/storage.png
