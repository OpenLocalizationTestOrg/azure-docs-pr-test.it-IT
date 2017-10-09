---
title: un nuovo servizio web in Azure Machine Learning aaaDeploying | Documenti Microsoft
description: servizio web basato su flusso di lavoro Hello della distribuzione di un ramo
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: a358b04f-0d08-4d50-820e-eeac971854cf
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/13/2017
ms.author: v-donglo
ROBOTS: NOINDEX
redirect_url: machine-learning-publish-a-machine-learning-web-service
redirect_document_id: True
ms.openlocfilehash: 2cbfda44b97a6b992fbdfdfb0c761e6c9e169035
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-new-web-service"></a><span data-ttu-id="a2edf-103">Distribuire un nuovo servizio Web</span><span class="sxs-lookup"><span data-stu-id="a2edf-103">Deploy a new web service</span></span>
<span data-ttu-id="a2edf-104">Microsoft Azure Machine learning ora fornisce i servizi web basati su [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) consentendo nuove opzioni del piano di fatturazione e le aree toomultiple del servizio web di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="a2edf-104">Microsoft Azure Machine learning now provides web services that are based on [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) allowing for new billing plan options and deploying your web service toomultiple regions.</span></span>

<span data-ttu-id="a2edf-105">flusso di lavoro generale di Hello toodeploy un servizio web tramite i servizi Web di Microsoft Azure Machine Learning è:</span><span class="sxs-lookup"><span data-stu-id="a2edf-105">hello general workflow toodeploy a web service using Microsoft Azure Machine Learning Web Services is:</span></span>

* <span data-ttu-id="a2edf-106">Creare un esperimento predittivo</span><span class="sxs-lookup"><span data-stu-id="a2edf-106">Create a predictive experiment</span></span>
* <span data-ttu-id="a2edf-107">distribuirlo</span><span class="sxs-lookup"><span data-stu-id="a2edf-107">deploy it</span></span>
* <span data-ttu-id="a2edf-108">configurare il relativo nome</span><span class="sxs-lookup"><span data-stu-id="a2edf-108">configure its name</span></span>
* <span data-ttu-id="a2edf-109">piano di fatturazione</span><span class="sxs-lookup"><span data-stu-id="a2edf-109">billing plan</span></span>
* <span data-ttu-id="a2edf-110">eseguirne il test</span><span class="sxs-lookup"><span data-stu-id="a2edf-110">test it</span></span>
* <span data-ttu-id="a2edf-111">usarlo.</span><span class="sxs-lookup"><span data-stu-id="a2edf-111">consume it.</span></span>

<span data-ttu-id="a2edf-112">Hello seguente immagine illustra del flusso di lavoro di hello.</span><span class="sxs-lookup"><span data-stu-id="a2edf-112">hello following graphic illustrates hello workflow.</span></span>

![Flusso di lavoro per la distribuzione di un servizio Web][1]

## <a name="deploy-web-service-from-studio"></a><span data-ttu-id="a2edf-114">Distribuire il servizio Web da Studio</span><span class="sxs-lookup"><span data-stu-id="a2edf-114">Deploy web service from Studio</span></span>
<span data-ttu-id="a2edf-115">toodeploy un esperimento come un nuovo servizio web.</span><span class="sxs-lookup"><span data-stu-id="a2edf-115">toodeploy an experiment as a new web service.</span></span> <span data-ttu-id="a2edf-116">Accedere al hello Machine Learning Studio e creare un nuovo servizio web predittivo.</span><span class="sxs-lookup"><span data-stu-id="a2edf-116">Sign into hello Machine Learning Studio and create a new predictive web service.</span></span> 

<span data-ttu-id="a2edf-117">**Nota**: se un esperimento è già stato distribuito come servizio Web classico non è possibile distribuirlo come un nuovo servizio Web.</span><span class="sxs-lookup"><span data-stu-id="a2edf-117">**Note**: If you have already deployed an experiment as a classic web service you cannot deploy it as a new web service.</span></span>

<span data-ttu-id="a2edf-118">Fare clic su **eseguire** nella parte inferiore di hello di hello provare l'area di disegno e quindi fare clic su **distribuzione servizio Web** e **distribuzione servizio Web [New]**.</span><span class="sxs-lookup"><span data-stu-id="a2edf-118">Click **Run** at hello bottom of hello experiment canvas and then click **Deploy Web Service** and **Deploy Web Service [New]**.</span></span> <span data-ttu-id="a2edf-119">verrà visualizzata la pagina distribuzione Hello di Gestione servizio Web di Machine Learning hello.</span><span class="sxs-lookup"><span data-stu-id="a2edf-119">hello deployment page of hello Machine Learning Web Service manager will open.</span></span>

## <a name="machine-learning-web-service-manager-deploy-experiment-page"></a><span data-ttu-id="a2edf-120">Pagina Deploy Experiment (Sperimentazione distribuzione) di Machine Learning Web Service Manager</span><span class="sxs-lookup"><span data-stu-id="a2edf-120">Machine Learning Web Service Manager Deploy Experiment Page</span></span>
<span data-ttu-id="a2edf-121">Nella pagina distribuzione esperimento hello, immettere un nome per il servizio web hello.</span><span class="sxs-lookup"><span data-stu-id="a2edf-121">On hello Deploy Experiment page, enter a name for hello web service.</span></span>
<span data-ttu-id="a2edf-122">Selezionare un piano tariffario.</span><span class="sxs-lookup"><span data-stu-id="a2edf-122">Select a pricing plan.</span></span> <span data-ttu-id="a2edf-123">Se si dispone di un piano tariffario esistente che è possibile selezionarlo, in caso contrario è necessario creare un nuovo piano di prezzo per servizio hello.</span><span class="sxs-lookup"><span data-stu-id="a2edf-123">If you have an existing pricing plan you can select it, otherwise you must create a new price plan for hello service.</span></span> 

1. <span data-ttu-id="a2edf-124">In hello **prezzo piano** elenco a discesa, selezionare un piano esistente o hello **Seleziona nuovo piano** opzione.</span><span class="sxs-lookup"><span data-stu-id="a2edf-124">In hello **Price Plan** drop down, select an existing plan or select hello **Select new plan** option.</span></span>
2. <span data-ttu-id="a2edf-125">In **nome piano**, digitare un nome che identifichi il piano di hello nella fattura.</span><span class="sxs-lookup"><span data-stu-id="a2edf-125">In **Plan Name**, type a name that will identify hello plan on your bill.</span></span>
3. <span data-ttu-id="a2edf-126">Selezionare una delle hello **livelli di pianificazione mensile**.</span><span class="sxs-lookup"><span data-stu-id="a2edf-126">Select one of hello **Monthly Plan Tiers**.</span></span> <span data-ttu-id="a2edf-127">Si noti che i livelli di hello piano predefinito toohello piani per l'area predefinita e il servizio web sono distribuito toothat area.</span><span class="sxs-lookup"><span data-stu-id="a2edf-127">Note that hello plan tiers default toohello plans for your default region and your web service is deployed toothat region.</span></span>

<span data-ttu-id="a2edf-128">Fare clic su **Distribuisci** e verrà visualizzata la pagina avvio rapido di hello per il servizio web.</span><span class="sxs-lookup"><span data-stu-id="a2edf-128">Click **Deploy** and hello Quickstart page for your web service opens.</span></span>

## <a name="quickstart-page"></a><span data-ttu-id="a2edf-129">Pagina Avvio rapido</span><span class="sxs-lookup"><span data-stu-id="a2edf-129">Quickstart page</span></span>
<span data-ttu-id="a2edf-130">pagina avvio rapido del servizio web di Hello consente di ottenere accesso e informazioni aggiuntive sulle attività più comuni di hello che verranno eseguite dopo la creazione di un nuovo servizio web.</span><span class="sxs-lookup"><span data-stu-id="a2edf-130">hello web service Quickstart page gives you access and guidance on hello most common tasks you will perform after creating a new web service.</span></span> <span data-ttu-id="a2edf-131">Da qui è possibile accedere facilmente entrambi hello **Test** pagina e **consumare** pagina.</span><span class="sxs-lookup"><span data-stu-id="a2edf-131">From here you can easily access both hello **Test** page and **Consume** page.</span></span>

## <a name="testing-your-web-service"></a><span data-ttu-id="a2edf-132">Test del servizio Web</span><span class="sxs-lookup"><span data-stu-id="a2edf-132">Testing your web service</span></span>
<span data-ttu-id="a2edf-133">Dalla pagina avvio rapido di hello, fare clic su servizio web di Test nell'area attività comuni.</span><span class="sxs-lookup"><span data-stu-id="a2edf-133">From hello Quickstart page, click Test web service under common tasks.</span></span>   

<span data-ttu-id="a2edf-134">servizio web tootest hello come un servizio di richiesta-risposta (RR):</span><span class="sxs-lookup"><span data-stu-id="a2edf-134">tootest hello web service as a Request-Response Service (RRS):</span></span>

* <span data-ttu-id="a2edf-135">Fare clic su **Test** sulla barra dei menu hello.</span><span class="sxs-lookup"><span data-stu-id="a2edf-135">Click **Test** on hello menu bar.</span></span>
* <span data-ttu-id="a2edf-136">Fare clic su **Request-Response**(Richiesta-risposta).</span><span class="sxs-lookup"><span data-stu-id="a2edf-136">Click **Request-Response**.</span></span>
* <span data-ttu-id="a2edf-137">Immettere i valori appropriati per le colonne di input hello dell'esperimento.</span><span class="sxs-lookup"><span data-stu-id="a2edf-137">Enter appropriate values for hello input columns of your experiment.</span></span>
* <span data-ttu-id="a2edf-138">Fare clic su Test **Request-Response**(Test Richiesta-risposta).</span><span class="sxs-lookup"><span data-stu-id="a2edf-138">Click Test **Request-Response**.</span></span>

<span data-ttu-id="a2edf-139">Risultati verranno visualizzati in hello lato destro della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="a2edf-139">You results will display on hello right hand side of hello page.</span></span>

<span data-ttu-id="a2edf-140">tootest un servizio web servizio esecuzione Batch (BES), si utilizzerà un file CSV:</span><span class="sxs-lookup"><span data-stu-id="a2edf-140">tootest a Batch Execution Service (BES) web service, you will use a CSV file:</span></span>

* <span data-ttu-id="a2edf-141">Fare clic su **Test** sulla barra dei menu hello.</span><span class="sxs-lookup"><span data-stu-id="a2edf-141">Click **Test** on hello menu bar.</span></span>
* <span data-ttu-id="a2edf-142">Fare clic su **Batch**.</span><span class="sxs-lookup"><span data-stu-id="a2edf-142">Click **Batch**.</span></span>
* <span data-ttu-id="a2edf-143">Nell'input dell'utente, fare clic su Sfoglia e passare i file di dati di esempio tooyour.</span><span class="sxs-lookup"><span data-stu-id="a2edf-143">Under your input, click Browse and navigate tooyour sample data file.</span></span>
* <span data-ttu-id="a2edf-144">Fare clic su **Test**.</span><span class="sxs-lookup"><span data-stu-id="a2edf-144">Click **Test**.</span></span>

<span data-ttu-id="a2edf-145">stato Hello del test viene visualizzato in **testare i processi Batch**.</span><span class="sxs-lookup"><span data-stu-id="a2edf-145">hello status of your test is displayed under **Test Batch Jobs**.</span></span>

## <a name="consuming-your-web-service"></a><span data-ttu-id="a2edf-146">Uso del servizio Web</span><span class="sxs-lookup"><span data-stu-id="a2edf-146">Consuming your Web Service</span></span>
<span data-ttu-id="a2edf-147">Quando viene pubblicato come servizio Web, gli esperimenti Azure Machine Learning forniscono un'API REST che può essere utilizzata da un'ampia gamma di dispositivi e piattaforme.</span><span class="sxs-lookup"><span data-stu-id="a2edf-147">When deployed as a web service, Azure Machine Learning experiments provide a REST API that can be consumed by a wide range of devices and platforms.</span></span> <span data-ttu-id="a2edf-148">Questo avviene perché i messaggi in formato hello simple API REST accetti e risponda con JSON.</span><span class="sxs-lookup"><span data-stu-id="a2edf-148">This is because hello simple REST API accepts and responds with JSON formatted messages.</span></span> <span data-ttu-id="a2edf-149">portale di Azure Machine Learning Hello fornisce codice che può essere utilizzato servizio web di hello toocall in R, c# e Python.</span><span class="sxs-lookup"><span data-stu-id="a2edf-149">hello Azure Machine Learning portal provides code that can be used toocall hello web service in R, C#, and Python.</span></span>

<span data-ttu-id="a2edf-150">Nella pagina di consumo hello è possibile trovare:</span><span class="sxs-lookup"><span data-stu-id="a2edf-150">On hello Consuming page you can find:</span></span>

* <span data-ttu-id="a2edf-151">chiave API Hello e l'URI per l'utilizzo del servizio web nelle app.</span><span class="sxs-lookup"><span data-stu-id="a2edf-151">hello API key and URI's for consuming web service in apps.</span></span>
* <span data-ttu-id="a2edf-152">Excel e web tookick di modelli di app di avviare il processo di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="a2edf-152">Excel and web app templates tookick start your consumption process.</span></span>
* <span data-ttu-id="a2edf-153">Codice di esempio in c#, python e R tooget è stato avviato.</span><span class="sxs-lookup"><span data-stu-id="a2edf-153">Sample code in C#, python, and R tooget you started.</span></span>

<span data-ttu-id="a2edf-154">Per ulteriori informazioni sull'utilizzo di servizi web, vedere [come un servizio Web di Azure Machine Learning tooconsume](machine-learning-consume-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="a2edf-154">For more information on consuming web services, see [How tooconsume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a2edf-155">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a2edf-155">Next Steps</span></span>
<span data-ttu-id="a2edf-156">Per altre informazioni sull'utilizzo dei servizi Web, vedere:</span><span class="sxs-lookup"><span data-stu-id="a2edf-156">For more information on consuming web services, see:</span></span>

[<span data-ttu-id="a2edf-157">Come un servizio Web di Azure Machine Learning tooconsume</span><span class="sxs-lookup"><span data-stu-id="a2edf-157">How tooconsume an Azure Machine Learning Web service</span></span>](machine-learning-consume-web-services.md)

[<span data-ttu-id="a2edf-158">Servizi Web di Azure Machine Learning: distribuzione e uso</span><span class="sxs-lookup"><span data-stu-id="a2edf-158">Azure Machine Learning Web Services: Deployment and consumption</span></span>](machine-learning-deploy-consume-web-service-guide.md)

<!--Image references-->
[1]: ./media/machine-learning-webservice-deploy-a-web-service/armdeploymentworkflow.png


<!--links-->
