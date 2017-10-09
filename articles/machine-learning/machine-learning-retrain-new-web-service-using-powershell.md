---
title: un servizio web Azure Machine Learning nuovo con PowerShell aaaRetrain | Documenti Microsoft
description: Informazioni su come tooprogrammatically ripetere il training di un modello e l'aggiornamento hello toouse hello appena sottoposto a training modello di servizio web in Azure Machine Learning tramite i cmdlet di PowerShell di gestione di Machine Learning hello.
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondlaghaeian
editor: 
ms.assetid: 3953a398-6174-4d2d-8bbd-e55cf1639415
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/28/2017
ms.author: v-donglo
ms.openlocfilehash: 5b77fa82cfe17f0b4e90007ef81c506ab712475b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-a-new-resource-manager-based-web-service-using-hello-machine-learning-management-powershell-cmdlets"></a><span data-ttu-id="18dbf-103">Ripetere il training di un servizio web basato su nuovo gestore di risorse utilizzando i cmdlet di PowerShell di gestione di Machine Learning hello</span><span class="sxs-lookup"><span data-stu-id="18dbf-103">Retrain a New Resource Manager based web service using hello Machine Learning Management PowerShell cmdlets</span></span>
<span data-ttu-id="18dbf-104">Quando si ripetere il training di un nuovo servizio web, si aggiorna hello predittiva definizione tooreference hello nuovo sottoposto a training modello di servizio web.</span><span class="sxs-lookup"><span data-stu-id="18dbf-104">When you retrain a New web service, you update hello predictive web service definition tooreference hello new trained model.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="18dbf-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="18dbf-105">Prerequisites</span></span>
<span data-ttu-id="18dbf-106">È necessario impostare un esperimento di training e un esperimento predittivo come illustrato in [Ripetere il training dei modelli di Machine Learning in modo programmatico](machine-learning-retrain-models-programmatically.md).</span><span class="sxs-lookup"><span data-stu-id="18dbf-106">You must set up a training experiment and a predictive experiment as shown in [Retrain Machine Learning models programmatically](machine-learning-retrain-models-programmatically.md).</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="18dbf-107">sperimentazione predittiva Hello deve essere distribuito come una gestione risorse di Azure (nuovo) basato su servizio web machine learning.</span><span class="sxs-lookup"><span data-stu-id="18dbf-107">hello predictive experiment must be deployed as an Azure Resource Manager (New) based machine learning web service.</span></span> <span data-ttu-id="18dbf-108">un nuovo servizio web deve disporre di autorizzazioni sufficienti in hello toowhich di sottoscrizione per la distribuzione del servizio web hello toodeploy.</span><span class="sxs-lookup"><span data-stu-id="18dbf-108">toodeploy a New web service you must have sufficient permissions in hello subscription toowhich you deploying hello web service.</span></span> <span data-ttu-id="18dbf-109">Per ulteriori informazioni, vedere [gestire un servizio Web tramite il portale di servizi Web di Azure Machine Learning hello](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="18dbf-109">For more information, see [Manage a Web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="18dbf-110">Per altre informazioni sulla distribuzione di servizi Web, vedere [Distribuire un servizio Web di Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="18dbf-110">For additional information on Deploying web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

<span data-ttu-id="18dbf-111">Questo processo richiede che sia stato installato hello cmdlet di Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="18dbf-111">This process requires that you have installed hello Azure Machine Learning Cmdlets.</span></span> <span data-ttu-id="18dbf-112">Per installare i cmdlet di Machine Learning hello di informazioni, vedere hello [i cmdlet di Azure Machine Learning](https://msdn.microsoft.com/library/azure/mt767952.aspx) riferimento su MSDN.</span><span class="sxs-lookup"><span data-stu-id="18dbf-112">For information installing hello Machine Learning cmdlets, see hello [Azure Machine Learning Cmdlets](https://msdn.microsoft.com/library/azure/mt767952.aspx) reference on MSDN.</span></span>

<span data-ttu-id="18dbf-113">Hello copiato dalla ripetizione di training output hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="18dbf-113">Copied hello following information from hello retraining output:</span></span>

* <span data-ttu-id="18dbf-114">BaseLocation</span><span class="sxs-lookup"><span data-stu-id="18dbf-114">BaseLocation</span></span>
* <span data-ttu-id="18dbf-115">RelativeLocation</span><span class="sxs-lookup"><span data-stu-id="18dbf-115">RelativeLocation</span></span>

<span data-ttu-id="18dbf-116">Hello i passaggi sono:</span><span class="sxs-lookup"><span data-stu-id="18dbf-116">hello steps you take are:</span></span>

1. <span data-ttu-id="18dbf-117">Accedi tooyour account di gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="18dbf-117">Sign in tooyour Azure Resource Manager account.</span></span>
2. <span data-ttu-id="18dbf-118">Ottenere una definizione del servizio web hello</span><span class="sxs-lookup"><span data-stu-id="18dbf-118">Get hello web service definition</span></span>
3. <span data-ttu-id="18dbf-119">Esportazione hello definizione del servizio Web nel formato JSON</span><span class="sxs-lookup"><span data-stu-id="18dbf-119">Export hello Web Service Definition as JSON</span></span>
4. <span data-ttu-id="18dbf-120">Aggiornare i blob di ilearner toohello riferimento hello in hello JSON.</span><span class="sxs-lookup"><span data-stu-id="18dbf-120">Update hello reference toohello ilearner blob in hello JSON.</span></span>
5. <span data-ttu-id="18dbf-121">Importare hello JSON in una definizione del servizio Web</span><span class="sxs-lookup"><span data-stu-id="18dbf-121">Import hello JSON into a Web Service Definition</span></span>
6. <span data-ttu-id="18dbf-122">Aggiornare il servizio web hello con nuova definizione del servizio Web</span><span class="sxs-lookup"><span data-stu-id="18dbf-122">Update hello web service with new Web Service Definition</span></span>

## <a name="sign-in-tooyour-azure-resource-manager-account"></a><span data-ttu-id="18dbf-123">Accedi tooyour account di gestione risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="18dbf-123">Sign in tooyour Azure Resource Manager account</span></span>
<span data-ttu-id="18dbf-124">È necessario innanzitutto accedere nell'account di Azure dall'ambiente di PowerShell hello utilizzando hello tooyour [Aggiungi AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="18dbf-124">You must first sign in tooyour Azure account from within hello PowerShell environment using hello [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span>

## <a name="get-hello-web-service-definition"></a><span data-ttu-id="18dbf-125">Ottenere hello definizione del servizio Web</span><span class="sxs-lookup"><span data-stu-id="18dbf-125">Get hello Web Service Definition</span></span>
<span data-ttu-id="18dbf-126">Quindi, ottenere hello servizio Web dal chiamante hello [Get AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="18dbf-126">Next, get hello Web Service by calling hello [Get-AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span> <span data-ttu-id="18dbf-127">Hello definizione del servizio Web è una rappresentazione interna del modello con training di hello del servizio web hello e non è direttamente modificabile.</span><span class="sxs-lookup"><span data-stu-id="18dbf-127">hello Web Service Definition is an internal representation of hello trained model of hello web service and is not directly modifiable.</span></span> <span data-ttu-id="18dbf-128">Assicurarsi che si desidera recuperare hello definizione del servizio Web per l'esperimento predittiva e non l'esperimento di training.</span><span class="sxs-lookup"><span data-stu-id="18dbf-128">Make sure that you are retrieving hello Web Service Definition for your Predictive experiment and not your training experiment.</span></span>

    $wsd = Get-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

<span data-ttu-id="18dbf-129">toodetermine hello Nome gruppo di risorse di un servizio web esistente, eseguire il cmdlet Get-AzureRmMlWebService hello senza servizi parametri toodisplay hello web nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="18dbf-129">toodetermine hello resource group name of an existing web service, run hello Get-AzureRmMlWebService cmdlet without any parameters toodisplay hello web services in your subscription.</span></span> <span data-ttu-id="18dbf-130">Servizio web hello di individuare e quindi esaminare il relativo ID di servizio web.</span><span class="sxs-lookup"><span data-stu-id="18dbf-130">Locate hello web service, and then look at its web service ID.</span></span> <span data-ttu-id="18dbf-131">nome di Hello hello del gruppo di risorse è elemento quarto hello ID hello, subito dopo hello *resourceGroups* elemento.</span><span class="sxs-lookup"><span data-stu-id="18dbf-131">hello name of hello resource group is hello fourth element in hello ID, just after hello *resourceGroups* element.</span></span> <span data-ttu-id="18dbf-132">Nell'esempio seguente di hello, nome del gruppo di risorse hello è MachineLearning-predefinito-SouthCentralUS.</span><span class="sxs-lookup"><span data-stu-id="18dbf-132">In hello following example, hello resource group name is Default-MachineLearning-SouthCentralUS.</span></span>

    Properties : Microsoft.Azure.Management.MachineLearning.WebServices.Models.WebServicePropertiesForGraph
    Id : /subscriptions/<subscription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237
    Name : RetrainSamplePre.2016.8.17.0.3.51.237
    Location : South Central US
    Type : Microsoft.MachineLearning/webServices
    Tags : {}

<span data-ttu-id="18dbf-133">In alternativa, toodetermine hello Nome gruppo di risorse di un servizio web esistente, i log nel portale di servizi Web di Microsoft Azure Machine Learning toohello.</span><span class="sxs-lookup"><span data-stu-id="18dbf-133">Alternatively, toodetermine hello resource group name of an existing web service, log on toohello Microsoft Azure Machine Learning Web Services portal.</span></span> <span data-ttu-id="18dbf-134">Selezionare servizio web hello.</span><span class="sxs-lookup"><span data-stu-id="18dbf-134">Select hello web service.</span></span> <span data-ttu-id="18dbf-135">nome del gruppo di risorse Hello è hello quinto elemento hello URL del servizio web hello, subito dopo hello *resourceGroups* elemento.</span><span class="sxs-lookup"><span data-stu-id="18dbf-135">hello resource group name is hello fifth element of hello URL of hello web service, just after hello *resourceGroups* element.</span></span> <span data-ttu-id="18dbf-136">Nell'esempio seguente di hello, nome del gruppo di risorse hello è MachineLearning-predefinito-SouthCentralUS.</span><span class="sxs-lookup"><span data-stu-id="18dbf-136">In hello following example, hello resource group name is Default-MachineLearning-SouthCentralUS.</span></span>

    https://services.azureml.net/subscriptions/<subcription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237


## <a name="export-hello-web-service-definition-as-json"></a><span data-ttu-id="18dbf-137">Esportazione hello definizione del servizio Web nel formato JSON</span><span class="sxs-lookup"><span data-stu-id="18dbf-137">Export hello Web Service Definition as JSON</span></span>
<span data-ttu-id="18dbf-138">toomodify hello definizione toohello training del modello toouse hello appena modello con training, è innanzitutto necessario utilizzare hello [esportazione AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767935.aspx) tooexport cmdlet è tooa file di formato JSON.</span><span class="sxs-lookup"><span data-stu-id="18dbf-138">toomodify hello definition toohello trained model toouse hello newly Trained Model, you must first use hello [Export-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767935.aspx) cmdlet tooexport it tooa JSON format file.</span></span>

    Export-AzureRmMlWebService -WebService $wsd -OutputFile "C:\temp\mlservice_export.json"

## <a name="update-hello-reference-toohello-ilearner-blob-in-hello-json"></a><span data-ttu-id="18dbf-139">Aggiornare i blob di ilearner toohello riferimento hello in hello JSON.</span><span class="sxs-lookup"><span data-stu-id="18dbf-139">Update hello reference toohello ilearner blob in hello JSON.</span></span>
<span data-ttu-id="18dbf-140">Attività hello, individuare hello [modello con training], aggiornamento hello *uri* valore hello *locationInfo* nodo con l'URI del blob ilearner hello hello.</span><span class="sxs-lookup"><span data-stu-id="18dbf-140">In hello assets, locate hello [trained model], update hello *uri* value in hello *locationInfo* node with hello URI of hello ilearner blob.</span></span> <span data-ttu-id="18dbf-141">Hello URI viene generato dalla combinazione hello *BaseLocation* hello e *RelativeLocation* dall'output di hello di chiamata i BES hello.</span><span class="sxs-lookup"><span data-stu-id="18dbf-141">hello URI is generated by combining hello *BaseLocation* and hello *RelativeLocation* from hello output of hello BES retraining call.</span></span> <span data-ttu-id="18dbf-142">Aggiorna hello percorso tooreference hello nuovo modello con training.</span><span class="sxs-lookup"><span data-stu-id="18dbf-142">This updates hello path tooreference hello new trained model.</span></span>

     "asset3": {
        "name": "Retrain Samp.le [trained model]",
        "type": "Resource",
        "locationInfo": {
          "uri": "https://mltestaccount.blob.core.windows.net/azuremlassetscontainer/baca7bca650f46218633552c0bcbba0e.ilearner"
        },
        "outputPorts": {
          "Results dataset": {
            "type": "Dataset"
          }
        }
      },

## <a name="import-hello-json-into-a-web-service-definition"></a><span data-ttu-id="18dbf-143">Importare hello JSON in una definizione del servizio Web</span><span class="sxs-lookup"><span data-stu-id="18dbf-143">Import hello JSON into a Web Service Definition</span></span>
<span data-ttu-id="18dbf-144">È necessario utilizzare hello [importazione AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767925.aspx) cmdlet tooconvert hello modificati file JSON in una definizione del servizio Web che è possibile utilizzare tooupdate hello definizione del servizio Web.</span><span class="sxs-lookup"><span data-stu-id="18dbf-144">You must use hello [Import-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767925.aspx) cmdlet tooconvert hello modified JSON file back into a Web Service Definition that you can use tooupdate hello Web Service Definition.</span></span>

    $wsd = Import-AzureRmMlWebService -InputFile "C:\temp\mlservice_export.json"


## <a name="update-hello-web-service-with-new-web-service-definition"></a><span data-ttu-id="18dbf-145">Aggiornare il servizio web hello con nuova definizione del servizio Web</span><span class="sxs-lookup"><span data-stu-id="18dbf-145">Update hello web service with new Web Service Definition</span></span>
<span data-ttu-id="18dbf-146">Utilizzare infine [aggiornamento AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767922.aspx) cmdlet tooupdate hello definizione del servizio Web.</span><span class="sxs-lookup"><span data-stu-id="18dbf-146">Finally, you use [Update-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767922.aspx) cmdlet tooupdate hello Web Service Definition.</span></span>

    Update-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'  -ServiceUpdates $wsd

## <a name="summary"></a><span data-ttu-id="18dbf-147">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="18dbf-147">Summary</span></span>
<span data-ttu-id="18dbf-148">Utilizzando i cmdlet di gestione di PowerShell di Machine Learning hello, è possibile aggiornare il modello con training di hello di un servizio Web predittivo l'abilitazione di scenari, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="18dbf-148">Using hello Machine Learning PowerShell management cmdlets, you can update hello trained model of a predictive Web Service enabling scenarios such as:</span></span>

* <span data-ttu-id="18dbf-149">Ripetizione periodica del training del modello con nuovi dati.</span><span class="sxs-lookup"><span data-stu-id="18dbf-149">Periodic model retraining with new data.</span></span>
* <span data-ttu-id="18dbf-150">Distribuzione di un modello di toocustomers con obiettivo hello di informarli del training modello di hello usando i propri dati.</span><span class="sxs-lookup"><span data-stu-id="18dbf-150">Distribution of a model toocustomers with hello goal of letting them retrain hello model using their own data.</span></span>

