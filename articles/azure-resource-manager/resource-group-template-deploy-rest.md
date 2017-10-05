---
title: Distribuire le risorse con i modelli e l'API REST | Microsoft Docs
description: Utilizzare Azure Resource Manager e l'API REST di Resource Manager per distribuire una risorsa in Azure. Le risorse sono definite in un modello di Resource Manager.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 1d8fbd4c-78b0-425b-ba76-f2b7fd260b45
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/10/2017
ms.author: tomfitz
ms.openlocfilehash: 46856a25fb57bb2c5a3c1aeae13c11655e1a58a5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-resource-manager-rest-api"></a><span data-ttu-id="0f9c4-104">Distribuire le risorse con i modelli e l'API REST di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0f9c4-104">Deploy resources with Resource Manager templates and Resource Manager REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0f9c4-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0f9c4-105">PowerShell</span></span>](resource-group-template-deploy.md)
> * [<span data-ttu-id="0f9c4-106">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="0f9c4-106">Azure CLI</span></span>](resource-group-template-deploy-cli.md)
> * [<span data-ttu-id="0f9c4-107">Portale</span><span class="sxs-lookup"><span data-stu-id="0f9c4-107">Portal</span></span>](resource-group-template-deploy-portal.md)
> * [<span data-ttu-id="0f9c4-108">API REST</span><span class="sxs-lookup"><span data-stu-id="0f9c4-108">REST API</span></span>](resource-group-template-deploy-rest.md)
> 
> 

<span data-ttu-id="0f9c4-109">In questo articolo viene illustrato come utilizzare l'API REST di Resource Manager con i modelli di Resource Manager per distribuire le risorse in Azure.</span><span class="sxs-lookup"><span data-stu-id="0f9c4-109">This article explains how to use the Resource Manager REST API with Resource Manager templates to deploy your resources to Azure.</span></span>  

> [!TIP]
> <span data-ttu-id="0f9c4-110">Per informazioni su come eseguire il debug di un errore durante la distribuzione, vedere:</span><span class="sxs-lookup"><span data-stu-id="0f9c4-110">For help with debugging an error during deployment, see:</span></span>
> 
> * <span data-ttu-id="0f9c4-111">[View deployment operations](resource-manager-deployment-operations.md) (Visualizzare le operazioni di distribuzione) per ottenere informazioni per la risoluzione degli errori</span><span class="sxs-lookup"><span data-stu-id="0f9c4-111">[View deployment operations](resource-manager-deployment-operations.md) to learn about getting information that helps you troubleshoot your error</span></span>
> * <span data-ttu-id="0f9c4-112">[Risolvere errori comuni durante la distribuzione di risorse in Azure con Azure Resource Manager](resource-manager-common-deployment-errors.md) per informazioni sulla risoluzione degli errori di distribuzione più comuni</span><span class="sxs-lookup"><span data-stu-id="0f9c4-112">[Troubleshoot common errors when deploying resources to Azure with Azure Resource Manager](resource-manager-common-deployment-errors.md) to learn how to resolve common deployment errors</span></span>
> 
> 

<span data-ttu-id="0f9c4-113">Il modello può essere un file locale oppure un file esterno disponibile tramite un URI.</span><span class="sxs-lookup"><span data-stu-id="0f9c4-113">Your template can be either a local file or an external file that is available through a URI.</span></span> <span data-ttu-id="0f9c4-114">Quando il modello si trova in un account di archiviazione, è possibile limitare l'accesso al modello e fornire un token di firma di accesso condiviso in fase di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="0f9c4-114">When your template resides in a storage account, you can restrict access to the template and provide a shared access signature (SAS) token during deployment.</span></span>

[!INCLUDE [resource-manager-deployments](../../includes/resource-manager-deployments.md)]

## <a name="deploy-with-the-rest-api"></a><span data-ttu-id="0f9c4-115">Distribuire con l'API REST</span><span class="sxs-lookup"><span data-stu-id="0f9c4-115">Deploy with the REST API</span></span>
1. <span data-ttu-id="0f9c4-116">Impostare [parametri e intestazioni comuni](https://docs.microsoft.com/rest/api/index), tra cui i token di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="0f9c4-116">Set [common parameters and headers](https://docs.microsoft.com/rest/api/index), including authentication tokens.</span></span>
2. <span data-ttu-id="0f9c4-117">Se non è già disponibile un gruppo di risorse, crearne uno.</span><span class="sxs-lookup"><span data-stu-id="0f9c4-117">If you do not have an existing resource group, create a resource group.</span></span> <span data-ttu-id="0f9c4-118">Specificare l'ID sottoscrizione, il nome del nuovo gruppo di risorse e il percorso per la soluzione.</span><span class="sxs-lookup"><span data-stu-id="0f9c4-118">Provide your subscription ID, the name of the new resource group, and location that you need for your solution.</span></span> <span data-ttu-id="0f9c4-119">Per ulteriori informazioni, vedere [Create a resource group](https://docs.microsoft.com/rest/api/resources/resourcegroups#ResourceGroups_CreateOrUpdate) (Creare un gruppo di risorse).</span><span class="sxs-lookup"><span data-stu-id="0f9c4-119">For more information, see [Create a resource group](https://docs.microsoft.com/rest/api/resources/resourcegroups#ResourceGroups_CreateOrUpdate).</span></span>
   
        PUT https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>?api-version=2015-01-01
          <common headers>
          {
            "location": "West US",
            "tags": {
               "tagname1": "tagvalue1"
            }
          }
3. <span data-ttu-id="0f9c4-120">Convalidare la distribuzione prima dell'esecuzione eseguendo l'operazione di [convalida della distribuzione di un modello](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Validate) .</span><span class="sxs-lookup"><span data-stu-id="0f9c4-120">Validate your deployment before executing it by running the [Validate a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Validate) operation.</span></span> <span data-ttu-id="0f9c4-121">Durante il test della distribuzione, specificare i parametri esattamente come quando si esegue la distribuzione (illustrata nel passaggio successivo).</span><span class="sxs-lookup"><span data-stu-id="0f9c4-121">When testing the deployment, provide parameters exactly as you would when executing the deployment (shown in the next step).</span></span>
4. <span data-ttu-id="0f9c4-122">Creare una distribuzione.</span><span class="sxs-lookup"><span data-stu-id="0f9c4-122">Create a deployment.</span></span> <span data-ttu-id="0f9c4-123">Fornire l'ID sottoscrizione, il nome del gruppo di risorse, il nome della distribuzione e un collegamento al modello.</span><span class="sxs-lookup"><span data-stu-id="0f9c4-123">Provide your subscription ID, the name of the resource group, the name of the deployment, and a link to your template.</span></span> <span data-ttu-id="0f9c4-124">Per informazioni sul file di modello, vedere [File di parametri](#parameter-file).</span><span class="sxs-lookup"><span data-stu-id="0f9c4-124">For information about the template file, see [Parameter file](#parameter-file).</span></span> <span data-ttu-id="0f9c4-125">Per altre informazioni sull'API REST per creare un gruppo di risorse, vedere [Create a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_CreateOrUpdate) (Creare la distribuzione di un modello).</span><span class="sxs-lookup"><span data-stu-id="0f9c4-125">For more information about the REST API to create a resource group, see [Create a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_CreateOrUpdate).</span></span> <span data-ttu-id="0f9c4-126">Si noti che la **modalità** è impostata su **Incrementale**.</span><span class="sxs-lookup"><span data-stu-id="0f9c4-126">Notice the **mode** is set to **Incremental**.</span></span> <span data-ttu-id="0f9c4-127">Per eseguire una distribuzione completa, impostare **mode** su **Complete** (Completo).</span><span class="sxs-lookup"><span data-stu-id="0f9c4-127">To run a complete deployment, set **mode** to **Complete**.</span></span> <span data-ttu-id="0f9c4-128">Quando si utilizza la modalità di completamento, fare attenzione a non eliminare inavvertitamente le risorse non presenti nel modello.</span><span class="sxs-lookup"><span data-stu-id="0f9c4-128">Be careful when using the complete mode as you can inadvertently delete resources that are not in your template.</span></span>
   
        PUT https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>/providers/Microsoft.Resources/deployments/<YourDeploymentName>?api-version=2015-01-01
          <common headers>
          {
            "properties": {
              "templateLink": {
                "uri": "http://mystorageaccount.blob.core.windows.net/templates/template.json",
                "contentVersion": "1.0.0.0"
              },
              "mode": "Incremental",
              "parametersLink": {
                "uri": "http://mystorageaccount.blob.core.windows.net/templates/parameters.json",
                "contentVersion": "1.0.0.0"
              }
            }
          }
   
      <span data-ttu-id="0f9c4-129">Per registrare il contenuto della risposta, il contenuto della richiesta o entrambi, includere **debugSetting** nella richiesta.</span><span class="sxs-lookup"><span data-stu-id="0f9c4-129">If you want to log response content, request content, or both, include **debugSetting** in the request.</span></span>
   
        "debugSetting": {
          "detailLevel": "requestContent, responseContent"
        }
   
      <span data-ttu-id="0f9c4-130">È possibile impostare l'account di archiviazione per l'utilizzzo di un token di firma di accesso condiviso (SAS).</span><span class="sxs-lookup"><span data-stu-id="0f9c4-130">You can set up your storage account to use a shared access signature (SAS) token.</span></span> <span data-ttu-id="0f9c4-131">Per altre informazioni, vedere [Delegating Access with a Shared Access Signature](https://docs.microsoft.com/rest/api/storageservices/delegating-access-with-a-shared-access-signature) (Delega dell'accesso con una firma di accesso condiviso).</span><span class="sxs-lookup"><span data-stu-id="0f9c4-131">For more information, see [Delegating Access with a Shared Access Signature](https://docs.microsoft.com/rest/api/storageservices/delegating-access-with-a-shared-access-signature).</span></span>
5. <span data-ttu-id="0f9c4-132">Ottenere lo stato della distribuzione del modello.</span><span class="sxs-lookup"><span data-stu-id="0f9c4-132">Get the status of the template deployment.</span></span> <span data-ttu-id="0f9c4-133">Per altre informazioni, vedere [Get information about a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get) (Ottenere informazioni sulla distribuzione di un modello).</span><span class="sxs-lookup"><span data-stu-id="0f9c4-133">For more information, see [Get information about a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get).</span></span>
   
          GET https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>/providers/Microsoft.Resources/deployments/<YourDeploymentName>?api-version=2015-01-01
           <common headers>

## <a name="parameter-file"></a><span data-ttu-id="0f9c4-134">File di parametri</span><span class="sxs-lookup"><span data-stu-id="0f9c4-134">Parameter file</span></span>

[!INCLUDE [resource-manager-parameter-file](../../includes/resource-manager-parameter-file.md)]

## <a name="next-steps"></a><span data-ttu-id="0f9c4-135">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0f9c4-135">Next steps</span></span>
* <span data-ttu-id="0f9c4-136">Per altre informazioni sulla gestione delle operazioni REST asincrone, vedere [Track asynchronous Azure operations](resource-manager-async-operations.md) (Tenere traccia delle operazioni asincrone di Azure).</span><span class="sxs-lookup"><span data-stu-id="0f9c4-136">To learn about handling asynchronous REST operations, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span></span>
* <span data-ttu-id="0f9c4-137">Per un esempio di distribuzione delle risorse con la libreria client .NET, vedere [Distribuire le risorse usando le librerie .NET e un modello](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0f9c4-137">For an example of deploying resources through the .NET client library, see [Deploy resources using .NET libraries and a template](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="0f9c4-138">Per definire i parametri nel modello, vedere [Creazione di modelli](resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="0f9c4-138">To define parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="0f9c4-139">Per indicazioni sulla distribuzione della soluzione in ambienti diversi, vedere [Ambienti di sviluppo e test in Microsoft Azure](solution-dev-test-environments.md).</span><span class="sxs-lookup"><span data-stu-id="0f9c4-139">For guidance on deploying your solution to different environments, see [Development and test environments in Microsoft Azure](solution-dev-test-environments.md).</span></span>
* <span data-ttu-id="0f9c4-140">Per indicazioni su come le aziende possono usare Resource Manager per gestire efficacemente le sottoscrizioni, vedere [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md) (Scaffolding aziendale Azure - Governance prescrittiva per le sottoscrizioni).</span><span class="sxs-lookup"><span data-stu-id="0f9c4-140">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

