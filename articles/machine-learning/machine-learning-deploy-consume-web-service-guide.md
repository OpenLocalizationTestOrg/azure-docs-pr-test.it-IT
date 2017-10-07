---
title: 'Servizi Web di Azure Machine Learning: distribuzione e utilizzo | Documentazione Microsoft'
description: Risorse per la distribuzione e l'uso dei servizi Web.
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: 47635376-d1f4-4ea4-a6af-bd1f99f69a69
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 539c2abb053a0f981be0374defe45cf4d96b740b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-machine-learning-web-services-deployment-and-consumption"></a><span data-ttu-id="7b004-103">Servizi Web di Azure Machine Learning: distribuzione e uso</span><span class="sxs-lookup"><span data-stu-id="7b004-103">Azure Machine Learning Web Services: Deployment and consumption</span></span>
<span data-ttu-id="7b004-104">È possibile utilizzare Azure Machine Learning toodeploy machine learning flussi di lavoro e i modelli come servizi web.</span><span class="sxs-lookup"><span data-stu-id="7b004-104">You can use Azure Machine Learning toodeploy machine-learning workflows and models as web services.</span></span> <span data-ttu-id="7b004-105">Questi servizi web possono quindi essere modelli di machine learning hello toocall utilizzati dalle applicazioni tramite le stime toodo Internet hello in tempo reale o in modalità batch.</span><span class="sxs-lookup"><span data-stu-id="7b004-105">These web services can then be used toocall hello machine-learning models from applications over hello Internet toodo predictions in real time or in batch mode.</span></span> <span data-ttu-id="7b004-106">Poiché i servizi web hello RESTful, è possibile chiamarli da diversi linguaggi di programmazione e piattaforme, ad esempio .NET e Java e da applicazioni, ad esempio Excel.</span><span class="sxs-lookup"><span data-stu-id="7b004-106">Because hello web services are RESTful, you can call them from various programming languages and platforms, such as .NET and Java, and from applications, such as Excel.</span></span>

<span data-ttu-id="7b004-107">Nelle sezioni successive di Hello forniscono collegamenti toowalkthroughs, codice e documentazione toohelp iniziare.</span><span class="sxs-lookup"><span data-stu-id="7b004-107">hello next sections provide links toowalkthroughs, code, and documentation toohelp get you started.</span></span>

## <a name="deploy-a-web-service"></a><span data-ttu-id="7b004-108">Distribuire un servizio Web</span><span class="sxs-lookup"><span data-stu-id="7b004-108">Deploy a web service</span></span>
### <a name="with-azure-machine-learning-studio"></a><span data-ttu-id="7b004-109">Con Azure Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="7b004-109">With Azure Machine Learning Studio</span></span>
<span data-ttu-id="7b004-110">Machine Learning Studio e il portale di servizi Web di Microsoft Azure Machine Learning hello consentono di distribuire e gestire un servizio web senza scrivere codice.</span><span class="sxs-lookup"><span data-stu-id="7b004-110">Machine Learning Studio and hello Microsoft Azure Machine Learning Web Services portal help you deploy and manage a web service without writing code.</span></span>

<span data-ttu-id="7b004-111">i collegamenti seguenti Hello forniscono informazioni generali su come toodeploy un nuovo servizio web:</span><span class="sxs-lookup"><span data-stu-id="7b004-111">hello following links provide general Information about how toodeploy a new web service:</span></span>

* <span data-ttu-id="7b004-112">Per una panoramica sul funzionamento toodeploy un nuovo servizio web che si basa su Gestione risorse di Azure, vedere [distribuire un nuovo servizio web](machine-learning-webservice-deploy-a-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="7b004-112">For an overview about how toodeploy a new web service that's based on Azure Resource Manager, see [Deploy a new web service](machine-learning-webservice-deploy-a-web-service.md).</span></span>
* <span data-ttu-id="7b004-113">Per una procedura dettagliata su come toodeploy un servizio web, vedere [distribuire un servizio web Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="7b004-113">For a walkthrough about how toodeploy a web service, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>
* <span data-ttu-id="7b004-114">Per una procedura dettagliata completa sul toocreate e distribuire un servizio web, vedere [procedura dettagliata passaggio 1: creare un'area di lavoro di Machine Learning](machine-learning-walkthrough-1-create-ml-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="7b004-114">For a full walkthrough about how toocreate and deploy a web service, see [Walkthrough Step 1: Create a Machine Learning workspace](machine-learning-walkthrough-1-create-ml-workspace.md).</span></span>
* <span data-ttu-id="7b004-115">Per esempi specifici di distribuzione di un servizio Web, vedere:</span><span class="sxs-lookup"><span data-stu-id="7b004-115">For specific examples that deploy a web service, see:</span></span>

  * [<span data-ttu-id="7b004-116">Procedura dettagliata passaggio 5: Distribuzione di servizio web di Azure Machine Learning hello</span><span class="sxs-lookup"><span data-stu-id="7b004-116">Walkthrough Step 5: Deploy hello Azure Machine Learning web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
  * [<span data-ttu-id="7b004-117">Come toodeploy web service toomultiple aree</span><span class="sxs-lookup"><span data-stu-id="7b004-117">How toodeploy a web service toomultiple regions</span></span>](machine-learning-how-to-deploy-to-multiple-regions.md)

### <a name="with-web-services-resource-provider-apis-azure-resource-manager-apis"></a><span data-ttu-id="7b004-118">Con le API del provider di risorse di servizi Web (API di Azure Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="7b004-118">With web services resource provider APIs (Azure Resource Manager APIs)</span></span>
<span data-ttu-id="7b004-119">provider di risorse di Azure Machine Learning Hello per servizi web consente la distribuzione e gestione dei servizi web tramite chiamate all'API REST.</span><span class="sxs-lookup"><span data-stu-id="7b004-119">hello Azure Machine Learning resource provider for web services enables deployment and management of web services by using REST API calls.</span></span> <span data-ttu-id="7b004-120">Per altre informazioni, vedere i riferimenti al [servizio Web di Machine Learning (REST)](/rest/api/machinelearning/index).</span><span class="sxs-lookup"><span data-stu-id="7b004-120">For additional details, see the [Machine Learning Web Service (REST)](/rest/api/machinelearning/index) reference.</span></span>

<!-- [Machine Learning Web Service (REST)](https://msdn.microsoft.com/library/azure/mt767538.aspx) reference. -->


### <a name="with-powershell-cmdlets"></a><span data-ttu-id="7b004-121">Con i cmdlet di PowerShell</span><span class="sxs-lookup"><span data-stu-id="7b004-121">With PowerShell cmdlets</span></span>
<span data-ttu-id="7b004-122">Il provider di risorse di Azure Machine Learning per i servizi Web consente di distribuire e gestire i servizi Web tramite cmdlet di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7b004-122">Azure Machine Learning resource provider for web services enables deployment and management of web services by using PowerShell cmdlets.</span></span>

<span data-ttu-id="7b004-123">toouse hello cmdlet, è necessario innanzitutto accedere tooyour account di Azure dall'ambiente di PowerShell hello utilizzando hello [Aggiungi AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="7b004-123">toouse hello cmdlets, you must first sign in tooyour Azure account from within hello PowerShell environment by using hello [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span> <span data-ttu-id="7b004-124">Se non si ha familiarità con modalità toocall PowerShell comandi che si basano su Gestione risorse, vedere [tramite Azure PowerShell con Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md#log-in-to-your-azure-account).</span><span class="sxs-lookup"><span data-stu-id="7b004-124">If you are unfamiliar with how toocall PowerShell commands that are based on Resource Manager, see [Using Azure PowerShell with Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md#log-in-to-your-azure-account).</span></span>

<span data-ttu-id="7b004-125">tooexport sperimentare la stima, utilizzare [questo codice di esempio](https://github.com/ritwik20/AzureML-WebServices).</span><span class="sxs-lookup"><span data-stu-id="7b004-125">tooexport your predictive experiment, use [this sample code](https://github.com/ritwik20/AzureML-WebServices).</span></span> <span data-ttu-id="7b004-126">Dopo aver creato il file di .exe hello dal codice hello, è possibile digitare:</span><span class="sxs-lookup"><span data-stu-id="7b004-126">After you create hello .exe file from hello code, you can type:</span></span>

    C:\<folder>\GetWSD <experiment-url> <workspace-auth-token>

<span data-ttu-id="7b004-127">Esecuzione di un'applicazione hello crea un modello di JSON del servizio web.</span><span class="sxs-lookup"><span data-stu-id="7b004-127">Running hello application creates a web service JSON template.</span></span> <span data-ttu-id="7b004-128">modello hello toouse toodeploy un servizio web, è necessario aggiungere hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="7b004-128">toouse hello template toodeploy a web service, you must add hello following information:</span></span>

* <span data-ttu-id="7b004-129">Nome e chiave dell'account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="7b004-129">Storage account name and key</span></span>

    <span data-ttu-id="7b004-130">È possibile ottenere nome account di archiviazione hello e la chiave da entrambi hello [portale di Azure](https://portal.azure.com/) o hello [portale di Azure classico](http://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="7b004-130">You can get hello storage account name and key from either hello [Azure portal](https://portal.azure.com/) or hello [Azure classic portal](http://manage.windowsazure.com/).</span></span>
* <span data-ttu-id="7b004-131">ID del piano di impegno</span><span class="sxs-lookup"><span data-stu-id="7b004-131">Commitment plan ID</span></span>

    <span data-ttu-id="7b004-132">È possibile ottenere l'ID del piano hello da hello [servizi Web di Azure Machine Learning](https://services.azureml.net) portale Accedi e facendo clic sul nome di un piano.</span><span class="sxs-lookup"><span data-stu-id="7b004-132">You can get hello plan ID from hello [Azure Machine Learning Web Services](https://services.azureml.net) portal by signing in and clicking a plan name.</span></span>

<span data-ttu-id="7b004-133">Aggiungerli modello JSON toohello come elementi figlio di hello *proprietà* nodo hello stesso livello come hello *MachineLearningWorkspace* nodo.</span><span class="sxs-lookup"><span data-stu-id="7b004-133">Add them toohello JSON template as children of hello *Properties* node at hello same level as hello *MachineLearningWorkspace* node.</span></span>

<span data-ttu-id="7b004-134">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="7b004-134">Here's an example:</span></span>

    "StorageAccount": {
            "name": "YourStorageAccountName",
            "key": "YourStorageAccountKey"
    },
    "CommitmentPlan": {
        "id": "subscriptions/YouSubscriptionID/resourceGroups/YourResourceGroupID/providers/Microsoft.MachineLearning/commitmentPlans/YourPlanName"
    }

<span data-ttu-id="7b004-135">Vedere i seguenti articoli hello e codice per altri dettagli di esempio:</span><span class="sxs-lookup"><span data-stu-id="7b004-135">See hello following articles and sample code for additional details:</span></span>

* <span data-ttu-id="7b004-136">[cmdlet di Azure Machine Learning](https://msdn.microsoft.com/library/azure/mt767952.aspx) in MSDN</span><span class="sxs-lookup"><span data-stu-id="7b004-136">[Azure Machine Learning Cmdlets](https://msdn.microsoft.com/library/azure/mt767952.aspx) reference on MSDN</span></span>
* <span data-ttu-id="7b004-137">[Procedura dettagliata](https://github.com/raymondlaghaeian/azureml-webservices-arm-powershell/blob/master/sample-commands.txt) di esempio su GitHub</span><span class="sxs-lookup"><span data-stu-id="7b004-137">Sample [walkthrough](https://github.com/raymondlaghaeian/azureml-webservices-arm-powershell/blob/master/sample-commands.txt) on GitHub</span></span>

## <a name="consume-hello-web-services"></a><span data-ttu-id="7b004-138">Utilizzare i servizi web hello</span><span class="sxs-lookup"><span data-stu-id="7b004-138">Consume hello web services</span></span>
### <a name="from-hello-azure-machine-learning-web-services-ui-testing"></a><span data-ttu-id="7b004-139">Da hello Azure Machine Learning servizi dell'interfaccia utente Web (test)</span><span class="sxs-lookup"><span data-stu-id="7b004-139">From hello Azure Machine Learning Web Services UI (Testing)</span></span>
<span data-ttu-id="7b004-140">È possibile testare il servizio web dal portale di servizi Web di Azure Machine Learning hello.</span><span class="sxs-lookup"><span data-stu-id="7b004-140">You can test your web service from hello Azure Machine Learning Web Services portal.</span></span> <span data-ttu-id="7b004-141">Ciò include la verifica del servizio di richiesta-risposta hello (RR) e delle interfacce del servizio esecuzione Batch (BES).</span><span class="sxs-lookup"><span data-stu-id="7b004-141">This includes testing hello Request-Response service (RRS) and Batch Execution service (BES) interfaces.</span></span>

* [<span data-ttu-id="7b004-142">Distribuire un nuovo servizio Web</span><span class="sxs-lookup"><span data-stu-id="7b004-142">Deploy a new web service</span></span>](machine-learning-webservice-deploy-a-web-service.md)
* [<span data-ttu-id="7b004-143">Distribuire un servizio Web di Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="7b004-143">Deploy an Azure Machine Learning web service</span></span>](machine-learning-publish-a-machine-learning-web-service.md)
* [<span data-ttu-id="7b004-144">Procedura dettagliata passaggio 5: Distribuzione di servizio web di Azure Machine Learning hello</span><span class="sxs-lookup"><span data-stu-id="7b004-144">Walkthrough Step 5: Deploy hello Azure Machine Learning web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)

### <a name="from-excel"></a><span data-ttu-id="7b004-145">Da Excel</span><span class="sxs-lookup"><span data-stu-id="7b004-145">From Excel</span></span>
<span data-ttu-id="7b004-146">È possibile scaricare un modello di Excel che utilizza servizio web hello:</span><span class="sxs-lookup"><span data-stu-id="7b004-146">You can download an Excel template that consumes hello web service:</span></span>

* [<span data-ttu-id="7b004-147">Utilizzo di un servizio Web di Azure Machine Learning da Excel</span><span class="sxs-lookup"><span data-stu-id="7b004-147">Consuming an Azure Machine Learning web service from Excel</span></span>](machine-learning-consuming-from-excel.md)
* [<span data-ttu-id="7b004-148">Componente aggiuntivo Excel per i servizi Web di Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="7b004-148">Excel add-in for Azure Machine Learning Web Services</span></span>](machine-learning-excel-add-in-for-web-services.md)

### <a name="from-a-rest-based-client"></a><span data-ttu-id="7b004-149">Da un client basato su REST</span><span class="sxs-lookup"><span data-stu-id="7b004-149">From a REST-based client</span></span>
<span data-ttu-id="7b004-150">I servizi Web di Azure Machine Learning sono API RESTful.</span><span class="sxs-lookup"><span data-stu-id="7b004-150">Azure Machine Learning Web Services are RESTful APIs.</span></span> <span data-ttu-id="7b004-151">È possibile utilizzare queste API da diverse piattaforme, ad esempio .NET, Python, R, Java, hello e così via **consumare** pagina per il servizio web in hello [portale di servizi Web di Microsoft Azure Machine Learning](https://services.azureml.net) dispone di esempio codice che consentono di iniziare.</span><span class="sxs-lookup"><span data-stu-id="7b004-151">You can consume these APIs from various platforms, such as .NET, Python, R, Java, etc. hello **Consume** page for your web service on hello [Microsoft Azure Machine Learning Web Services portal](https://services.azureml.net) has sample code that can help you get started.</span></span> <span data-ttu-id="7b004-152">Per ulteriori informazioni, vedere [come un servizio Web di Azure Machine Learning tooconsume](machine-learning-consume-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="7b004-152">For more information, see [How tooconsume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>
