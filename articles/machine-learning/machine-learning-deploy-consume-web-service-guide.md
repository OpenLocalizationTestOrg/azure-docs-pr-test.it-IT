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
ms.openlocfilehash: 18edabe267ec06c08074d7a7a6d71435cedc8489
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-machine-learning-web-services-deployment-and-consumption"></a><span data-ttu-id="8c6e0-103">Servizi Web di Azure Machine Learning: distribuzione e uso</span><span class="sxs-lookup"><span data-stu-id="8c6e0-103">Azure Machine Learning Web Services: Deployment and consumption</span></span>
<span data-ttu-id="8c6e0-104">È possibile usare Azure Machine Learning (Azure ML) per distribuire i flussi di lavoro e i modelli di Machine Learning come servizi Web.</span><span class="sxs-lookup"><span data-stu-id="8c6e0-104">You can use Azure Machine Learning to deploy machine-learning workflows and models as web services.</span></span> <span data-ttu-id="8c6e0-105">Questi servizi Web possono quindi essere usati per chiamare i modelli di Machine Learning dalle applicazioni tramite Internet per eseguire stime in tempo reale o in modalità batch.</span><span class="sxs-lookup"><span data-stu-id="8c6e0-105">These web services can then be used to call the machine-learning models from applications over the Internet to do predictions in real time or in batch mode.</span></span> <span data-ttu-id="8c6e0-106">Essendo RESTFul, i servizi Web possono essere chiamati da diversi linguaggi di programmazione e piattaforme, come .NET e Java, nonché applicazioni, come Excel.</span><span class="sxs-lookup"><span data-stu-id="8c6e0-106">Because the web services are RESTful, you can call them from various programming languages and platforms, such as .NET and Java, and from applications, such as Excel.</span></span>

<span data-ttu-id="8c6e0-107">Le sezioni successive forniscono collegamenti a procedure dettagliate, codice e documentazione per aiutarvi a iniziare.</span><span class="sxs-lookup"><span data-stu-id="8c6e0-107">The next sections provide links to walkthroughs, code, and documentation to help get you started.</span></span>

## <a name="deploy-a-web-service"></a><span data-ttu-id="8c6e0-108">Distribuire un servizio Web</span><span class="sxs-lookup"><span data-stu-id="8c6e0-108">Deploy a web service</span></span>
### <a name="with-azure-machine-learning-studio"></a><span data-ttu-id="8c6e0-109">Con Azure Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="8c6e0-109">With Azure Machine Learning Studio</span></span>
<span data-ttu-id="8c6e0-110">Machine Learning Studio e il portale dei servizi Web di Microsoft Azure Machine Learning aiutano a distribuire e gestire un servizio Web senza dover scrivere codice.</span><span class="sxs-lookup"><span data-stu-id="8c6e0-110">Machine Learning Studio and the Microsoft Azure Machine Learning Web Services portal help you deploy and manage a web service without writing code.</span></span>

<span data-ttu-id="8c6e0-111">I collegamenti seguenti offrono informazioni generali su come distribuire un nuovo servizio Web:</span><span class="sxs-lookup"><span data-stu-id="8c6e0-111">The following links provide general Information about how to deploy a new web service:</span></span>

* <span data-ttu-id="8c6e0-112">Per una panoramica di come distribuire un nuovo servizio Web basato su Azure Resource Manager, vedere [Distribuire un nuovo servizio Web](machine-learning-webservice-deploy-a-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="8c6e0-112">For an overview about how to deploy a new web service that's based on Azure Resource Manager, see [Deploy a new web service](machine-learning-webservice-deploy-a-web-service.md).</span></span>
* <span data-ttu-id="8c6e0-113">Per una procedura dettagliata su come distribuire un servizio Web, vedere [Distribuire un servizio Web di Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="8c6e0-113">For a walkthrough about how to deploy a web service, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>
* <span data-ttu-id="8c6e0-114">Per una procedura dettagliata su come creare e distribuire un servizio Web, vedere [Passaggio 1 della procedura dettagliata: Creare un'area di lavoro di Machine Learning](machine-learning-walkthrough-1-create-ml-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="8c6e0-114">For a full walkthrough about how to create and deploy a web service, see [Walkthrough Step 1: Create a Machine Learning workspace](machine-learning-walkthrough-1-create-ml-workspace.md).</span></span>
* <span data-ttu-id="8c6e0-115">Per esempi specifici di distribuzione di un servizio Web, vedere:</span><span class="sxs-lookup"><span data-stu-id="8c6e0-115">For specific examples that deploy a web service, see:</span></span>

  * [<span data-ttu-id="8c6e0-116">Passaggio 5 della procedura dettagliata: Distribuzione del servizio Web di Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="8c6e0-116">Walkthrough Step 5: Deploy the Azure Machine Learning web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
  * [<span data-ttu-id="8c6e0-117">Come distribuire un servizio Web in più aree</span><span class="sxs-lookup"><span data-stu-id="8c6e0-117">How to deploy a web service to multiple regions</span></span>](machine-learning-how-to-deploy-to-multiple-regions.md)

### <a name="with-web-services-resource-provider-apis-azure-resource-manager-apis"></a><span data-ttu-id="8c6e0-118">Con le API del provider di risorse di servizi Web (API di Azure Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="8c6e0-118">With web services resource provider APIs (Azure Resource Manager APIs)</span></span>
<span data-ttu-id="8c6e0-119">Il provider di risorse di Azure Machine Learning per i servizi Web consente di distribuire e gestire servizi Web tramite chiamate all'API REST.</span><span class="sxs-lookup"><span data-stu-id="8c6e0-119">The Azure Machine Learning resource provider for web services enables deployment and management of web services by using REST API calls.</span></span> <span data-ttu-id="8c6e0-120">Per altre informazioni, vedere i riferimenti al [servizio Web di Machine Learning (REST)](/rest/api/machinelearning/index).</span><span class="sxs-lookup"><span data-stu-id="8c6e0-120">For additional details, see the [Machine Learning Web Service (REST)](/rest/api/machinelearning/index) reference.</span></span>

<!-- [Machine Learning Web Service (REST)](https://msdn.microsoft.com/library/azure/mt767538.aspx) reference. -->


### <a name="with-powershell-cmdlets"></a><span data-ttu-id="8c6e0-121">Con i cmdlet di PowerShell</span><span class="sxs-lookup"><span data-stu-id="8c6e0-121">With PowerShell cmdlets</span></span>
<span data-ttu-id="8c6e0-122">Il provider di risorse di Azure Machine Learning per i servizi Web consente di distribuire e gestire i servizi Web tramite cmdlet di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8c6e0-122">Azure Machine Learning resource provider for web services enables deployment and management of web services by using PowerShell cmdlets.</span></span>

<span data-ttu-id="8c6e0-123">Per usare i cmdlet è prima necessario accedere al proprio account Azure dall'interno dell'ambiente di PowerShell tramite il cmdlet [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) .</span><span class="sxs-lookup"><span data-stu-id="8c6e0-123">To use the cmdlets, you must first sign in to your Azure account from within the PowerShell environment by using the [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span> <span data-ttu-id="8c6e0-124">Se non si ha familiarità con la chiamata di comandi di PowerShell basati su Resource Manger, vedere [Uso di Azure PowerShell con Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md#log-in-to-your-azure-account).</span><span class="sxs-lookup"><span data-stu-id="8c6e0-124">If you are unfamiliar with how to call PowerShell commands that are based on Resource Manager, see [Using Azure PowerShell with Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md#log-in-to-your-azure-account).</span></span>

<span data-ttu-id="8c6e0-125">Usare questo [codice di esempio](https://github.com/ritwik20/AzureML-WebServices)per esportare l'esperimento predittivo.</span><span class="sxs-lookup"><span data-stu-id="8c6e0-125">To export your predictive experiment, use [this sample code](https://github.com/ritwik20/AzureML-WebServices).</span></span> <span data-ttu-id="8c6e0-126">Dopo aver creato il file .exe dal codice è possibile digitare:</span><span class="sxs-lookup"><span data-stu-id="8c6e0-126">After you create the .exe file from the code, you can type:</span></span>

    C:\<folder>\GetWSD <experiment-url> <workspace-auth-token>

<span data-ttu-id="8c6e0-127">Con l'esecuzione dell'applicazione viene creato un modello JSON di servizio Web.</span><span class="sxs-lookup"><span data-stu-id="8c6e0-127">Running the application creates a web service JSON template.</span></span> <span data-ttu-id="8c6e0-128">Per usare il modello per distribuire un servizio Web è necessario aggiungere le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="8c6e0-128">To use the template to deploy a web service, you must add the following information:</span></span>

* <span data-ttu-id="8c6e0-129">Nome e chiave dell'account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="8c6e0-129">Storage account name and key</span></span>

    <span data-ttu-id="8c6e0-130">È possibile ottenere il nome e la chiave dell'account di archiviazione dal [portale di Azure](https://portal.azure.com/) o dal [portale di Azure classico](http://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="8c6e0-130">You can get the storage account name and key from either the [Azure portal](https://portal.azure.com/) or the [Azure classic portal](http://manage.windowsazure.com/).</span></span>
* <span data-ttu-id="8c6e0-131">ID del piano di impegno</span><span class="sxs-lookup"><span data-stu-id="8c6e0-131">Commitment plan ID</span></span>

    <span data-ttu-id="8c6e0-132">È possibile ottenere l'ID del piano dal portale dei [servizi Web di Azure Machine Learning](https://services.azureml.net) eseguendo l'accesso e facendo clic sul nome di un piano.</span><span class="sxs-lookup"><span data-stu-id="8c6e0-132">You can get the plan ID from the [Azure Machine Learning Web Services](https://services.azureml.net) portal by signing in and clicking a plan name.</span></span>

<span data-ttu-id="8c6e0-133">Aggiungere le informazioni al modello JSON come figli del nodo *Properties* allo stesso livello del nodo *MachineLearningWorkspace*.</span><span class="sxs-lookup"><span data-stu-id="8c6e0-133">Add them to the JSON template as children of the *Properties* node at the same level as the *MachineLearningWorkspace* node.</span></span>

<span data-ttu-id="8c6e0-134">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="8c6e0-134">Here's an example:</span></span>

    "StorageAccount": {
            "name": "YourStorageAccountName",
            "key": "YourStorageAccountKey"
    },
    "CommitmentPlan": {
        "id": "subscriptions/YouSubscriptionID/resourceGroups/YourResourceGroupID/providers/Microsoft.MachineLearning/commitmentPlans/YourPlanName"
    }

<span data-ttu-id="8c6e0-135">Per altre informazioni, vedere gli articoli e il codice di esempio seguenti:</span><span class="sxs-lookup"><span data-stu-id="8c6e0-135">See the following articles and sample code for additional details:</span></span>

* <span data-ttu-id="8c6e0-136">[cmdlet di Azure Machine Learning](https://msdn.microsoft.com/library/azure/mt767952.aspx) in MSDN</span><span class="sxs-lookup"><span data-stu-id="8c6e0-136">[Azure Machine Learning Cmdlets](https://msdn.microsoft.com/library/azure/mt767952.aspx) reference on MSDN</span></span>
* <span data-ttu-id="8c6e0-137">[Procedura dettagliata](https://github.com/raymondlaghaeian/azureml-webservices-arm-powershell/blob/master/sample-commands.txt) di esempio su GitHub</span><span class="sxs-lookup"><span data-stu-id="8c6e0-137">Sample [walkthrough](https://github.com/raymondlaghaeian/azureml-webservices-arm-powershell/blob/master/sample-commands.txt) on GitHub</span></span>

## <a name="consume-the-web-services"></a><span data-ttu-id="8c6e0-138">Utilizzare i servizi Web</span><span class="sxs-lookup"><span data-stu-id="8c6e0-138">Consume the web services</span></span>
### <a name="from-the-azure-machine-learning-web-services-ui-testing"></a><span data-ttu-id="8c6e0-139">Dall'interfaccia utente dei servizi Web di Azure Machine Learning (test)</span><span class="sxs-lookup"><span data-stu-id="8c6e0-139">From the Azure Machine Learning Web Services UI (Testing)</span></span>
<span data-ttu-id="8c6e0-140">È possibile testare il servizio Web dal portale dei servizi Web di Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="8c6e0-140">You can test your web service from the Azure Machine Learning Web Services portal.</span></span> <span data-ttu-id="8c6e0-141">Sono inclusi i test delle interfacce del Servizio di richiesta-risposta (RRS) e del Servizio Esecuzione batch (BES).</span><span class="sxs-lookup"><span data-stu-id="8c6e0-141">This includes testing the Request-Response service (RRS) and Batch Execution service (BES) interfaces.</span></span>

* [<span data-ttu-id="8c6e0-142">Distribuire un nuovo servizio Web</span><span class="sxs-lookup"><span data-stu-id="8c6e0-142">Deploy a new web service</span></span>](machine-learning-webservice-deploy-a-web-service.md)
* [<span data-ttu-id="8c6e0-143">Distribuire un servizio Web di Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="8c6e0-143">Deploy an Azure Machine Learning web service</span></span>](machine-learning-publish-a-machine-learning-web-service.md)
* [<span data-ttu-id="8c6e0-144">Passaggio 5 della procedura dettagliata: Distribuzione del servizio Web di Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="8c6e0-144">Walkthrough Step 5: Deploy the Azure Machine Learning web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)

### <a name="from-excel"></a><span data-ttu-id="8c6e0-145">Da Excel</span><span class="sxs-lookup"><span data-stu-id="8c6e0-145">From Excel</span></span>
<span data-ttu-id="8c6e0-146">È possibile scaricare un modello di Excel che usa il servizio Web:</span><span class="sxs-lookup"><span data-stu-id="8c6e0-146">You can download an Excel template that consumes the web service:</span></span>

* [<span data-ttu-id="8c6e0-147">Utilizzo di un servizio Web di Azure Machine Learning da Excel</span><span class="sxs-lookup"><span data-stu-id="8c6e0-147">Consuming an Azure Machine Learning web service from Excel</span></span>](machine-learning-consuming-from-excel.md)
* [<span data-ttu-id="8c6e0-148">Componente aggiuntivo Excel per i servizi Web di Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="8c6e0-148">Excel add-in for Azure Machine Learning Web Services</span></span>](machine-learning-excel-add-in-for-web-services.md)

### <a name="from-a-rest-based-client"></a><span data-ttu-id="8c6e0-149">Da un client basato su REST</span><span class="sxs-lookup"><span data-stu-id="8c6e0-149">From a REST-based client</span></span>
<span data-ttu-id="8c6e0-150">I servizi Web di Azure Machine Learning sono API RESTful.</span><span class="sxs-lookup"><span data-stu-id="8c6e0-150">Azure Machine Learning Web Services are RESTful APIs.</span></span> <span data-ttu-id="8c6e0-151">È possibile usare queste API da diverse piattaforme quali .NET, Python, R, Java e così via. La pagina **di utilizzo** del servizio Web nel [portale dei servizi Web di Microsoft Azure Machine Learning](https://services.azureml.net) offre codice di esempio che può essere utile per iniziare.</span><span class="sxs-lookup"><span data-stu-id="8c6e0-151">You can consume these APIs from various platforms, such as .NET, Python, R, Java, etc. The **Consume** page for your web service on the [Microsoft Azure Machine Learning Web Services portal](https://services.azureml.net) has sample code that can help you get started.</span></span> <span data-ttu-id="8c6e0-152">Per altre informazioni, vedere [Come usare un servizio Web di Azure Machine Learning pubblicato da un esperimento di Machine Learning](machine-learning-consume-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="8c6e0-152">For more information, see [How to consume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>
