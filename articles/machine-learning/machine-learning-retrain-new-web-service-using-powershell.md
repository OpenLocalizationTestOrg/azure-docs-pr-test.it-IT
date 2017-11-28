---
title: Ripetere il training di un nuovo servizio Web di Machine Learning Azure con PowerShell | Documentazione Microsoft
description: Informazioni su come ripetere il training di un modello in modo programmatico e aggiornare il servizio Web per l'uso del modello appena sottoposto a training in Azure Machine Learning con i cmdlet di gestione di PowerShell.
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
ms.openlocfilehash: 804dd59e62f38ee1878045d93211ee18e0d5bfce
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="retrain-a-new-resource-manager-based-web-service-using-the-machine-learning-management-powershell-cmdlets"></a><span data-ttu-id="0b883-103">Ripetere il training di un nuovo servizio Web basato su Resource Manager usando i cmdlet di gestione di PowerShell per Machine Learning</span><span class="sxs-lookup"><span data-stu-id="0b883-103">Retrain a New Resource Manager based web service using the Machine Learning Management PowerShell cmdlets</span></span>
<span data-ttu-id="0b883-104">Quando si ripete il training di un nuovo servizio Web, si aggiorna la definizione del servizio Web predittivo perché faccia riferimento al nuovo modello sottoposto a training.</span><span class="sxs-lookup"><span data-stu-id="0b883-104">When you retrain a New web service, you update the predictive web service definition to reference the new trained model.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="0b883-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="0b883-105">Prerequisites</span></span>
<span data-ttu-id="0b883-106">È necessario impostare un esperimento di training e un esperimento predittivo come illustrato in [Ripetere il training dei modelli di Machine Learning in modo programmatico](machine-learning-retrain-models-programmatically.md).</span><span class="sxs-lookup"><span data-stu-id="0b883-106">You must set up a training experiment and a predictive experiment as shown in [Retrain Machine Learning models programmatically](machine-learning-retrain-models-programmatically.md).</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="0b883-107">L'esperimento predittivo deve essere distribuito come servizio Web nuovo di Machine Learning basato su Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="0b883-107">The predictive experiment must be deployed as an Azure Resource Manager (New) based machine learning web service.</span></span> <span data-ttu-id="0b883-108">Per distribuire un nuovo servizio Web è necessario disporre delle autorizzazioni sufficienti nella sottoscrizione a cui si sta distribuendo il servizio Web.</span><span class="sxs-lookup"><span data-stu-id="0b883-108">To deploy a New web service you must have sufficient permissions in the subscription to which you deploying the web service.</span></span> <span data-ttu-id="0b883-109">Per altre informazioni, vedere [Gestire un servizio Web usando il portale dei servizi Web di Azure Machine Learning](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="0b883-109">For more information, see [Manage a Web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="0b883-110">Per altre informazioni sulla distribuzione di servizi Web, vedere [Distribuire un servizio Web di Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="0b883-110">For additional information on Deploying web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

<span data-ttu-id="0b883-111">Questo processo richiede che siano stati installati i cmdlet di Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="0b883-111">This process requires that you have installed the Azure Machine Learning Cmdlets.</span></span> <span data-ttu-id="0b883-112">Per l'installazione dei cmdlet di Machine Learning, vedere le informazioni di riferimento sui [cmdlet di Azure Machine Learning](https://msdn.microsoft.com/library/azure/mt767952.aspx) in MSDN.</span><span class="sxs-lookup"><span data-stu-id="0b883-112">For information installing the Machine Learning cmdlets, see the [Azure Machine Learning Cmdlets](https://msdn.microsoft.com/library/azure/mt767952.aspx) reference on MSDN.</span></span>

<span data-ttu-id="0b883-113">È necessario aver copiato le informazioni seguenti dall'output di ripetizione del training:</span><span class="sxs-lookup"><span data-stu-id="0b883-113">Copied the following information from the retraining output:</span></span>

* <span data-ttu-id="0b883-114">BaseLocation</span><span class="sxs-lookup"><span data-stu-id="0b883-114">BaseLocation</span></span>
* <span data-ttu-id="0b883-115">RelativeLocation</span><span class="sxs-lookup"><span data-stu-id="0b883-115">RelativeLocation</span></span>

<span data-ttu-id="0b883-116">I passaggi da eseguire sono:</span><span class="sxs-lookup"><span data-stu-id="0b883-116">The steps you take are:</span></span>

1. <span data-ttu-id="0b883-117">Accedere con l'account di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="0b883-117">Sign in to your Azure Resource Manager account.</span></span>
2. <span data-ttu-id="0b883-118">Ottenere la definizione del servizio Web</span><span class="sxs-lookup"><span data-stu-id="0b883-118">Get the web service definition</span></span>
3. <span data-ttu-id="0b883-119">Esportare la definizione del servizio Web in un file in formato JSON</span><span class="sxs-lookup"><span data-stu-id="0b883-119">Export the Web Service Definition as JSON</span></span>
4. <span data-ttu-id="0b883-120">Aggiornare il riferimento al BLOB ilearner nel file JSON.</span><span class="sxs-lookup"><span data-stu-id="0b883-120">Update the reference to the ilearner blob in the JSON.</span></span>
5. <span data-ttu-id="0b883-121">Importare il file JSON in una definizione del servizio Web</span><span class="sxs-lookup"><span data-stu-id="0b883-121">Import the JSON into a Web Service Definition</span></span>
6. <span data-ttu-id="0b883-122">Aggiornare il servizio Web con la nuova definizione</span><span class="sxs-lookup"><span data-stu-id="0b883-122">Update the web service with new Web Service Definition</span></span>

## <a name="sign-in-to-your-azure-resource-manager-account"></a><span data-ttu-id="0b883-123">Accedere con l'account di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0b883-123">Sign in to your Azure Resource Manager account</span></span>
<span data-ttu-id="0b883-124">È prima necessario accedere al proprio account Azure dall'interno dell'ambiente di PowerShell tramite il cmdlet [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) .</span><span class="sxs-lookup"><span data-stu-id="0b883-124">You must first sign in to your Azure account from within the PowerShell environment using the [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span>

## <a name="get-the-web-service-definition"></a><span data-ttu-id="0b883-125">Ottenere la definizione del servizio Web</span><span class="sxs-lookup"><span data-stu-id="0b883-125">Get the Web Service Definition</span></span>
<span data-ttu-id="0b883-126">Ottenere quindi il servizio Web chiamando il cmdlet [Get-AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx) .</span><span class="sxs-lookup"><span data-stu-id="0b883-126">Next, get the Web Service by calling the [Get-AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span> <span data-ttu-id="0b883-127">La definizione del servizio Web è una rappresentazione interna del modello sottoposto a training del servizio Web e non è direttamente modificabile.</span><span class="sxs-lookup"><span data-stu-id="0b883-127">The Web Service Definition is an internal representation of the trained model of the web service and is not directly modifiable.</span></span> <span data-ttu-id="0b883-128">Assicurarsi di recuperare la definizione del servizio Web per l'esperimento predittivo e non per l'esperimento di training.</span><span class="sxs-lookup"><span data-stu-id="0b883-128">Make sure that you are retrieving the Web Service Definition for your Predictive experiment and not your training experiment.</span></span>

    $wsd = Get-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

<span data-ttu-id="0b883-129">Per determinare il nome del gruppo di risorse di un servizio Web esistente, eseguire il cmdlet Get-AzureRmMlWebService senza parametri per visualizzare i servizi Web nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="0b883-129">To determine the resource group name of an existing web service, run the Get-AzureRmMlWebService cmdlet without any parameters to display the web services in your subscription.</span></span> <span data-ttu-id="0b883-130">Individuare il servizio Web e quindi osservare l'ID del servizio Web.</span><span class="sxs-lookup"><span data-stu-id="0b883-130">Locate the web service, and then look at its web service ID.</span></span> <span data-ttu-id="0b883-131">Il nome del gruppo di risorse è il quarto elemento dell'ID, subito dopo l'elemento *resourceGroups* .</span><span class="sxs-lookup"><span data-stu-id="0b883-131">The name of the resource group is the fourth element in the ID, just after the *resourceGroups* element.</span></span> <span data-ttu-id="0b883-132">Nell'esempio seguente, il nome del gruppo di risorse è Default-MachineLearning-SouthCentralUS.</span><span class="sxs-lookup"><span data-stu-id="0b883-132">In the following example, the resource group name is Default-MachineLearning-SouthCentralUS.</span></span>

    Properties : Microsoft.Azure.Management.MachineLearning.WebServices.Models.WebServicePropertiesForGraph
    Id : /subscriptions/<subscription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237
    Name : RetrainSamplePre.2016.8.17.0.3.51.237
    Location : South Central US
    Type : Microsoft.MachineLearning/webServices
    Tags : {}

<span data-ttu-id="0b883-133">In alternativa, per determinare il nome del gruppo di risorse di un servizio Web esistente, accedere al portale di Microsoft Azure Machine Learning Web Services (Servizi Web di Microsoft Azure Machine Learning).</span><span class="sxs-lookup"><span data-stu-id="0b883-133">Alternatively, to determine the resource group name of an existing web service, log on to the Microsoft Azure Machine Learning Web Services portal.</span></span> <span data-ttu-id="0b883-134">Selezionare il servizio Web.</span><span class="sxs-lookup"><span data-stu-id="0b883-134">Select the web service.</span></span> <span data-ttu-id="0b883-135">Il nome del gruppo di risorse è il quinto elemento dell'URL del servizio Web, subito dopo l'elemento *resourceGroups* .</span><span class="sxs-lookup"><span data-stu-id="0b883-135">The resource group name is the fifth element of the URL of the web service, just after the *resourceGroups* element.</span></span> <span data-ttu-id="0b883-136">Nell'esempio seguente, il nome del gruppo di risorse è Default-MachineLearning-SouthCentralUS.</span><span class="sxs-lookup"><span data-stu-id="0b883-136">In the following example, the resource group name is Default-MachineLearning-SouthCentralUS.</span></span>

    https://services.azureml.net/subscriptions/<subcription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237


## <a name="export-the-web-service-definition-as-json"></a><span data-ttu-id="0b883-137">Esportare la definizione del servizio Web in un file in formato JSON</span><span class="sxs-lookup"><span data-stu-id="0b883-137">Export the Web Service Definition as JSON</span></span>
<span data-ttu-id="0b883-138">Per modificare la definizione per l'uso del modello appena sottoposto a training, è prima necessario usare il cmdlet [Export-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767935.aspx) per esportare la definizione in un file in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="0b883-138">To modify the definition to the trained model to use the newly Trained Model, you must first use the [Export-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767935.aspx) cmdlet to export it to a JSON format file.</span></span>

    Export-AzureRmMlWebService -WebService $wsd -OutputFile "C:\temp\mlservice_export.json"

## <a name="update-the-reference-to-the-ilearner-blob-in-the-json"></a><span data-ttu-id="0b883-139">Aggiornare il riferimento al BLOB ilearner nel file JSON.</span><span class="sxs-lookup"><span data-stu-id="0b883-139">Update the reference to the ilearner blob in the JSON.</span></span>
<span data-ttu-id="0b883-140">Negli asset individuare il [modello con training] e aggiornare il valore *uri* nel nodo *locationInfo* con l'URI del BLOB ilearner.</span><span class="sxs-lookup"><span data-stu-id="0b883-140">In the assets, locate the [trained model], update the *uri* value in the *locationInfo* node with the URI of the ilearner blob.</span></span> <span data-ttu-id="0b883-141">L'URI viene generato combinando i valori di *BaseLocation* e *RelativeLocation* dell'output della chiamata di ripetizione del training del servizio Esecuzione batch.</span><span class="sxs-lookup"><span data-stu-id="0b883-141">The URI is generated by combining the *BaseLocation* and the *RelativeLocation* from the output of the BES retraining call.</span></span> <span data-ttu-id="0b883-142">Il percorso viene così aggiornato in modo da fare riferimento al nuovo modello sottoposto a training.</span><span class="sxs-lookup"><span data-stu-id="0b883-142">This updates the path to reference the new trained model.</span></span>

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

## <a name="import-the-json-into-a-web-service-definition"></a><span data-ttu-id="0b883-143">Importare il file JSON in una definizione del servizio Web</span><span class="sxs-lookup"><span data-stu-id="0b883-143">Import the JSON into a Web Service Definition</span></span>
<span data-ttu-id="0b883-144">È necessario usare il cmdlet [Import-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767925.aspx) per convertire di nuovo il file JSON modificato in una definizione del servizio Web che possa essere usata per il relativo aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="0b883-144">You must use the [Import-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767925.aspx) cmdlet to convert the modified JSON file back into a Web Service Definition that you can use to update the Web Service Definition.</span></span>

    $wsd = Import-AzureRmMlWebService -InputFile "C:\temp\mlservice_export.json"


## <a name="update-the-web-service-with-new-web-service-definition"></a><span data-ttu-id="0b883-145">Aggiornare il servizio Web con la nuova definizione</span><span class="sxs-lookup"><span data-stu-id="0b883-145">Update the web service with new Web Service Definition</span></span>
<span data-ttu-id="0b883-146">Usare infine il cmdlet [Update-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767922.aspx) per aggiornare la definizione del servizio Web.</span><span class="sxs-lookup"><span data-stu-id="0b883-146">Finally, you use [Update-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767922.aspx) cmdlet to update the Web Service Definition.</span></span>

    Update-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'  -ServiceUpdates $wsd

## <a name="summary"></a><span data-ttu-id="0b883-147">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="0b883-147">Summary</span></span>
<span data-ttu-id="0b883-148">Usando i cmdlet di gestione PowerShell per Machine Learning, è possibile aggiornare il modello con training di un servizio Web predittivo abilitando scenari come:</span><span class="sxs-lookup"><span data-stu-id="0b883-148">Using the Machine Learning PowerShell management cmdlets, you can update the trained model of a predictive Web Service enabling scenarios such as:</span></span>

* <span data-ttu-id="0b883-149">Ripetizione periodica del training del modello con nuovi dati.</span><span class="sxs-lookup"><span data-stu-id="0b883-149">Periodic model retraining with new data.</span></span>
* <span data-ttu-id="0b883-150">Distribuzione di un modello ai clienti per fare in modo che possano ripetere il training del modello con i propri dati.</span><span class="sxs-lookup"><span data-stu-id="0b883-150">Distribution of a model to customers with the goal of letting them retrain the model using their own data.</span></span>

