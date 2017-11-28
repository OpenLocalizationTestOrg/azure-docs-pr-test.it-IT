---
title: Distribuire un nuovo servizio Web in Azure Machine Learning | Documentazione Microsoft
description: Il flusso di lavoro di implementazione di un servizio Web basato su ARM
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
redirect_document_id: TRUE
ms.openlocfilehash: 1415709f9da2bb2cce859af9feb0ec15c1fa5801
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-a-new-web-service"></a><span data-ttu-id="950a8-103">Distribuire un nuovo servizio Web</span><span class="sxs-lookup"><span data-stu-id="950a8-103">Deploy a new web service</span></span>
<span data-ttu-id="950a8-104">Microsoft Azure Machine Learning offre ora servizi Web basati su [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) consentendo nuove opzioni del piano di fatturazione e la distribuzione del servizio Web in più aree.</span><span class="sxs-lookup"><span data-stu-id="950a8-104">Microsoft Azure Machine learning now provides web services that are based on [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) allowing for new billing plan options and deploying your web service to multiple regions.</span></span>

<span data-ttu-id="950a8-105">Il flusso di lavoro generale per distribuire un servizio Web usando i servizi Web di Microsoft Azure Machine Learning è:</span><span class="sxs-lookup"><span data-stu-id="950a8-105">The general workflow to deploy a web service using Microsoft Azure Machine Learning Web Services is:</span></span>

* <span data-ttu-id="950a8-106">Creare un esperimento predittivo</span><span class="sxs-lookup"><span data-stu-id="950a8-106">Create a predictive experiment</span></span>
* <span data-ttu-id="950a8-107">distribuirlo</span><span class="sxs-lookup"><span data-stu-id="950a8-107">deploy it</span></span>
* <span data-ttu-id="950a8-108">configurare il relativo nome</span><span class="sxs-lookup"><span data-stu-id="950a8-108">configure its name</span></span>
* <span data-ttu-id="950a8-109">piano di fatturazione</span><span class="sxs-lookup"><span data-stu-id="950a8-109">billing plan</span></span>
* <span data-ttu-id="950a8-110">eseguirne il test</span><span class="sxs-lookup"><span data-stu-id="950a8-110">test it</span></span>
* <span data-ttu-id="950a8-111">usarlo.</span><span class="sxs-lookup"><span data-stu-id="950a8-111">consume it.</span></span>

<span data-ttu-id="950a8-112">L'immagine seguente illustra il flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="950a8-112">The following graphic illustrates the workflow.</span></span>

![Flusso di lavoro per la distribuzione di un servizio Web][1]

## <a name="deploy-web-service-from-studio"></a><span data-ttu-id="950a8-114">Distribuire il servizio Web da Studio</span><span class="sxs-lookup"><span data-stu-id="950a8-114">Deploy web service from Studio</span></span>
<span data-ttu-id="950a8-115">Per distribuire un esperimento come nuovo servizio Web.</span><span class="sxs-lookup"><span data-stu-id="950a8-115">To deploy an experiment as a new web service.</span></span> <span data-ttu-id="950a8-116">Accedere a Machine Learning Studio e creare un nuovo servizio Web predittivo.</span><span class="sxs-lookup"><span data-stu-id="950a8-116">Sign into the Machine Learning Studio and create a new predictive web service.</span></span> 

<span data-ttu-id="950a8-117">**Nota**: se un esperimento è già stato distribuito come servizio Web classico non è possibile distribuirlo come un nuovo servizio Web.</span><span class="sxs-lookup"><span data-stu-id="950a8-117">**Note**: If you have already deployed an experiment as a classic web service you cannot deploy it as a new web service.</span></span>

<span data-ttu-id="950a8-118">Fare clic su **Run** (Esegui) nella parte inferiore dell'area di disegno dell'esperimento e quindi fare clic su **Deploy Web Service** (Distribuisci servizio Web) e su **Deploy Web Service [New]** (Distribuisci servizio Web [Nuovo]).</span><span class="sxs-lookup"><span data-stu-id="950a8-118">Click **Run** at the bottom of the experiment canvas and then click **Deploy Web Service** and **Deploy Web Service [New]**.</span></span> <span data-ttu-id="950a8-119">Verrà aperta la pagina di distribuzione del portale di gestione dei servizi Web di Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="950a8-119">The deployment page of the Machine Learning Web Service manager will open.</span></span>

## <a name="machine-learning-web-service-manager-deploy-experiment-page"></a><span data-ttu-id="950a8-120">Pagina Deploy Experiment (Sperimentazione distribuzione) di Machine Learning Web Service Manager</span><span class="sxs-lookup"><span data-stu-id="950a8-120">Machine Learning Web Service Manager Deploy Experiment Page</span></span>
<span data-ttu-id="950a8-121">Nella pagina Deploy Experiment (Sperimentazione distribuzione) immettere un nome per il servizio Web.</span><span class="sxs-lookup"><span data-stu-id="950a8-121">On the Deploy Experiment page, enter a name for the web service.</span></span>
<span data-ttu-id="950a8-122">Selezionare un piano tariffario.</span><span class="sxs-lookup"><span data-stu-id="950a8-122">Select a pricing plan.</span></span> <span data-ttu-id="950a8-123">Se è disponibile un piano tariffario, è possibile selezionarlo; in caso contrario è necessario creare un nuovo piano tariffario per il servizio.</span><span class="sxs-lookup"><span data-stu-id="950a8-123">If you have an existing pricing plan you can select it, otherwise you must create a new price plan for the service.</span></span> 

1. <span data-ttu-id="950a8-124">Nell'elenco a discesa **Price Plan** (Piano tariffario) selezionare un piano esistente o l'opzione **Select new plan** (Seleziona nuovo piano).</span><span class="sxs-lookup"><span data-stu-id="950a8-124">In the **Price Plan** drop down, select an existing plan or select the **Select new plan** option.</span></span>
2. <span data-ttu-id="950a8-125">In **Plan Name**(Nome piano) digitare un nome che identifica il piano di fatturazione.</span><span class="sxs-lookup"><span data-stu-id="950a8-125">In **Plan Name**, type a name that will identify the plan on your bill.</span></span>
3. <span data-ttu-id="950a8-126">Selezionare uno dei **livelli del piano mensile**.</span><span class="sxs-lookup"><span data-stu-id="950a8-126">Select one of the **Monthly Plan Tiers**.</span></span> <span data-ttu-id="950a8-127">Si noti che per impostazione predefinita i livelli di piano vengono impostati sui piani per l'area predefinita e il servizio Web viene distribuito in tale area.</span><span class="sxs-lookup"><span data-stu-id="950a8-127">Note that the plan tiers default to the plans for your default region and your web service is deployed to that region.</span></span>

<span data-ttu-id="950a8-128">Fare clic su **Distribuisci** e verrà visualizzata la pagina Avvio rapido per il servizio Web.</span><span class="sxs-lookup"><span data-stu-id="950a8-128">Click **Deploy** and the Quickstart page for your web service opens.</span></span>

## <a name="quickstart-page"></a><span data-ttu-id="950a8-129">Pagina Avvio rapido</span><span class="sxs-lookup"><span data-stu-id="950a8-129">Quickstart page</span></span>
<span data-ttu-id="950a8-130">La pagina Avvio rapido del servizio Web offre indicazioni e accesso alle attività più comuni eseguite dopo la creazione di un nuovo servizio Web.</span><span class="sxs-lookup"><span data-stu-id="950a8-130">The web service Quickstart page gives you access and guidance on the most common tasks you will perform after creating a new web service.</span></span> <span data-ttu-id="950a8-131">Da qui è possibile accedere facilmente alle pagine di **test** e di **consumo**.</span><span class="sxs-lookup"><span data-stu-id="950a8-131">From here you can easily access both the **Test** page and **Consume** page.</span></span>

## <a name="testing-your-web-service"></a><span data-ttu-id="950a8-132">Test del servizio Web</span><span class="sxs-lookup"><span data-stu-id="950a8-132">Testing your web service</span></span>
<span data-ttu-id="950a8-133">Dalla pagina Avvio rapido fare clic su Test web service (Test servizio Web) nelle attività comuni.</span><span class="sxs-lookup"><span data-stu-id="950a8-133">From the Quickstart page, click Test web service under common tasks.</span></span>   

<span data-ttu-id="950a8-134">Per eseguire il test del servizio Web come servizio di richiesta-risposta (RRS):</span><span class="sxs-lookup"><span data-stu-id="950a8-134">To test the web service as a Request-Response Service (RRS):</span></span>

* <span data-ttu-id="950a8-135">Fare clic su **Test** nella barra dei menu.</span><span class="sxs-lookup"><span data-stu-id="950a8-135">Click **Test** on the menu bar.</span></span>
* <span data-ttu-id="950a8-136">Fare clic su **Request-Response**(Richiesta-risposta).</span><span class="sxs-lookup"><span data-stu-id="950a8-136">Click **Request-Response**.</span></span>
* <span data-ttu-id="950a8-137">Immettere i valori appropriati per le colonne di input dell'esperimento.</span><span class="sxs-lookup"><span data-stu-id="950a8-137">Enter appropriate values for the input columns of your experiment.</span></span>
* <span data-ttu-id="950a8-138">Fare clic su Test **Request-Response**(Test Richiesta-risposta).</span><span class="sxs-lookup"><span data-stu-id="950a8-138">Click Test **Request-Response**.</span></span>

<span data-ttu-id="950a8-139">I risultati verranno visualizzati sul lato destro della pagina.</span><span class="sxs-lookup"><span data-stu-id="950a8-139">You results will display on the right hand side of the page.</span></span>

<span data-ttu-id="950a8-140">Per testare un servizio di esecuzione batch (BES), si userà un file CSV:</span><span class="sxs-lookup"><span data-stu-id="950a8-140">To test a Batch Execution Service (BES) web service, you will use a CSV file:</span></span>

* <span data-ttu-id="950a8-141">Fare clic su **Test** nella barra dei menu.</span><span class="sxs-lookup"><span data-stu-id="950a8-141">Click **Test** on the menu bar.</span></span>
* <span data-ttu-id="950a8-142">Fare clic su **Batch**.</span><span class="sxs-lookup"><span data-stu-id="950a8-142">Click **Batch**.</span></span>
* <span data-ttu-id="950a8-143">Sotto l'input fare clic su Sfoglia e passare al file di dati di esempio.</span><span class="sxs-lookup"><span data-stu-id="950a8-143">Under your input, click Browse and navigate to your sample data file.</span></span>
* <span data-ttu-id="950a8-144">Fare clic su **Test**.</span><span class="sxs-lookup"><span data-stu-id="950a8-144">Click **Test**.</span></span>

<span data-ttu-id="950a8-145">Lo stato del test viene visualizzato in **Test Batch Jobs**(Test Processi batch).</span><span class="sxs-lookup"><span data-stu-id="950a8-145">The status of your test is displayed under **Test Batch Jobs**.</span></span>

## <a name="consuming-your-web-service"></a><span data-ttu-id="950a8-146">Uso del servizio Web</span><span class="sxs-lookup"><span data-stu-id="950a8-146">Consuming your Web Service</span></span>
<span data-ttu-id="950a8-147">Quando viene pubblicato come servizio Web, gli esperimenti Azure Machine Learning forniscono un'API REST che può essere utilizzata da un'ampia gamma di dispositivi e piattaforme.</span><span class="sxs-lookup"><span data-stu-id="950a8-147">When deployed as a web service, Azure Machine Learning experiments provide a REST API that can be consumed by a wide range of devices and platforms.</span></span> <span data-ttu-id="950a8-148">Infatti, la semplice API REST accetta e risponde con messaggi in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="950a8-148">This is because the simple REST API accepts and responds with JSON formatted messages.</span></span> <span data-ttu-id="950a8-149">Il portale di Azure Machine Learning fornisce il codice che può essere utilizzato per chiamare il servizio Web in R, c# e Python.</span><span class="sxs-lookup"><span data-stu-id="950a8-149">The Azure Machine Learning portal provides code that can be used to call the web service in R, C#, and Python.</span></span>

<span data-ttu-id="950a8-150">Nella pagina relativa all'uso è possibile trovare:</span><span class="sxs-lookup"><span data-stu-id="950a8-150">On the Consuming page you can find:</span></span>

* <span data-ttu-id="950a8-151">La chiave API e l'URI per l'uso del servizio Web nelle app.</span><span class="sxs-lookup"><span data-stu-id="950a8-151">The API key and URI's for consuming web service in apps.</span></span>
* <span data-ttu-id="950a8-152">I modelli di app Web e di Excel per avviare il processo di uso.</span><span class="sxs-lookup"><span data-stu-id="950a8-152">Excel and web app templates to kick start your consumption process.</span></span>
* <span data-ttu-id="950a8-153">Codice di esempio in C#, Python e R per iniziare.</span><span class="sxs-lookup"><span data-stu-id="950a8-153">Sample code in C#, python, and R to get you started.</span></span>

<span data-ttu-id="950a8-154">Per altre informazioni sulla creazione di servizi Web, vedere [Come usare un servizio Web di Azure Machine Learning](machine-learning-consume-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="950a8-154">For more information on consuming web services, see [How to consume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="950a8-155">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="950a8-155">Next Steps</span></span>
<span data-ttu-id="950a8-156">Per altre informazioni sull'utilizzo dei servizi Web, vedere:</span><span class="sxs-lookup"><span data-stu-id="950a8-156">For more information on consuming web services, see:</span></span>

[<span data-ttu-id="950a8-157">Come usare un servizio Web di Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="950a8-157">How to consume an Azure Machine Learning Web service</span></span>](machine-learning-consume-web-services.md)

[<span data-ttu-id="950a8-158">Servizi Web di Azure Machine Learning: distribuzione e uso</span><span class="sxs-lookup"><span data-stu-id="950a8-158">Azure Machine Learning Web Services: Deployment and consumption</span></span>](machine-learning-deploy-consume-web-service-guide.md)

<!--Image references-->
[1]: ./media/machine-learning-webservice-deploy-a-web-service/armdeploymentworkflow.png


<!--links-->
