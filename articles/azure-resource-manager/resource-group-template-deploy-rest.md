---
title: risorse aaaDeploy con API REST e modello | Documenti Microsoft
description: Utilizzare Gestione risorse di Azure e il REST API di gestione risorse toodeploy un tooAzure di risorse. risorse di Hello vengono definite in un modello di gestione risorse.
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
ms.openlocfilehash: 347ad3bdb604429e7291297d448688204af69b46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-resource-manager-rest-api"></a><span data-ttu-id="619f1-104">Distribuire le risorse con i modelli e l'API REST di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="619f1-104">Deploy resources with Resource Manager templates and Resource Manager REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="619f1-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="619f1-105">PowerShell</span></span>](resource-group-template-deploy.md)
> * [<span data-ttu-id="619f1-106">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="619f1-106">Azure CLI</span></span>](resource-group-template-deploy-cli.md)
> * [<span data-ttu-id="619f1-107">Portale</span><span class="sxs-lookup"><span data-stu-id="619f1-107">Portal</span></span>](resource-group-template-deploy-portal.md)
> * [<span data-ttu-id="619f1-108">API REST</span><span class="sxs-lookup"><span data-stu-id="619f1-108">REST API</span></span>](resource-group-template-deploy-rest.md)
> 
> 

<span data-ttu-id="619f1-109">Questo articolo spiega come toouse hello REST API di gestione risorse con Gestione risorse modelli toodeploy tooAzure le risorse.</span><span class="sxs-lookup"><span data-stu-id="619f1-109">This article explains how toouse hello Resource Manager REST API with Resource Manager templates toodeploy your resources tooAzure.</span></span>  

> [!TIP]
> <span data-ttu-id="619f1-110">Per informazioni su come eseguire il debug di un errore durante la distribuzione, vedere:</span><span class="sxs-lookup"><span data-stu-id="619f1-110">For help with debugging an error during deployment, see:</span></span>
> 
> * <span data-ttu-id="619f1-111">[Per visualizzare le operazioni di distribuzione](resource-manager-deployment-operations.md) toolearn sul recupero di informazioni che consentono di risolvere l'errore</span><span class="sxs-lookup"><span data-stu-id="619f1-111">[View deployment operations](resource-manager-deployment-operations.md) toolearn about getting information that helps you troubleshoot your error</span></span>
> * <span data-ttu-id="619f1-112">[Risolvere gli errori comuni durante la distribuzione di risorse tooAzure con Azure Resource Manager](resource-manager-common-deployment-errors.md) toolearn come tooresolve comuni errori di distribuzione</span><span class="sxs-lookup"><span data-stu-id="619f1-112">[Troubleshoot common errors when deploying resources tooAzure with Azure Resource Manager](resource-manager-common-deployment-errors.md) toolearn how tooresolve common deployment errors</span></span>
> 
> 

<span data-ttu-id="619f1-113">Il modello può essere un file locale oppure un file esterno disponibile tramite un URI.</span><span class="sxs-lookup"><span data-stu-id="619f1-113">Your template can be either a local file or an external file that is available through a URI.</span></span> <span data-ttu-id="619f1-114">Quando il modello si trova in un account di archiviazione, è possibile limitare il modello di toohello access e fornire un token di firma di accesso condiviso durante la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="619f1-114">When your template resides in a storage account, you can restrict access toohello template and provide a shared access signature (SAS) token during deployment.</span></span>

[!INCLUDE [resource-manager-deployments](../../includes/resource-manager-deployments.md)]

## <a name="deploy-with-hello-rest-api"></a><span data-ttu-id="619f1-115">Distribuire con hello API REST</span><span class="sxs-lookup"><span data-stu-id="619f1-115">Deploy with hello REST API</span></span>
1. <span data-ttu-id="619f1-116">Impostare [parametri e intestazioni comuni](https://docs.microsoft.com/rest/api/index), tra cui i token di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="619f1-116">Set [common parameters and headers](https://docs.microsoft.com/rest/api/index), including authentication tokens.</span></span>
2. <span data-ttu-id="619f1-117">Se non è già disponibile un gruppo di risorse, crearne uno.</span><span class="sxs-lookup"><span data-stu-id="619f1-117">If you do not have an existing resource group, create a resource group.</span></span> <span data-ttu-id="619f1-118">Specificare l'ID sottoscrizione, nome hello del nuovo gruppo di risorse hello e il percorso che è necessario per la soluzione.</span><span class="sxs-lookup"><span data-stu-id="619f1-118">Provide your subscription ID, hello name of hello new resource group, and location that you need for your solution.</span></span> <span data-ttu-id="619f1-119">Per ulteriori informazioni, vedere [Create a resource group](https://docs.microsoft.com/rest/api/resources/resourcegroups#ResourceGroups_CreateOrUpdate) (Creare un gruppo di risorse).</span><span class="sxs-lookup"><span data-stu-id="619f1-119">For more information, see [Create a resource group](https://docs.microsoft.com/rest/api/resources/resourcegroups#ResourceGroups_CreateOrUpdate).</span></span>
   
        PUT https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>?api-version=2015-01-01
          <common headers>
          {
            "location": "West US",
            "tags": {
               "tagname1": "tagvalue1"
            }
          }
3. <span data-ttu-id="619f1-120">Convalidare la distribuzione prima dell'esecuzione eseguendo hello [convalidare una distribuzione modello](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Validate) operazione.</span><span class="sxs-lookup"><span data-stu-id="619f1-120">Validate your deployment before executing it by running hello [Validate a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Validate) operation.</span></span> <span data-ttu-id="619f1-121">Durante il test di distribuzione di hello, specificare i parametri, esattamente come quando si esegue la distribuzione di hello (illustrata nel passaggio successivo hello).</span><span class="sxs-lookup"><span data-stu-id="619f1-121">When testing hello deployment, provide parameters exactly as you would when executing hello deployment (shown in hello next step).</span></span>
4. <span data-ttu-id="619f1-122">Creare una distribuzione.</span><span class="sxs-lookup"><span data-stu-id="619f1-122">Create a deployment.</span></span> <span data-ttu-id="619f1-123">Specificare l'ID sottoscrizione, il nome di hello hello del gruppo di risorse, nome hello della distribuzione di hello e un modello di tooyour di collegamento.</span><span class="sxs-lookup"><span data-stu-id="619f1-123">Provide your subscription ID, hello name of hello resource group, hello name of hello deployment, and a link tooyour template.</span></span> <span data-ttu-id="619f1-124">Per informazioni sul file di modello hello, vedere [file parametro](#parameter-file).</span><span class="sxs-lookup"><span data-stu-id="619f1-124">For information about hello template file, see [Parameter file](#parameter-file).</span></span> <span data-ttu-id="619f1-125">Per ulteriori informazioni sulle API REST di hello toocreate un gruppo di risorse, vedere [creare una distribuzione modello](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_CreateOrUpdate).</span><span class="sxs-lookup"><span data-stu-id="619f1-125">For more information about hello REST API toocreate a resource group, see [Create a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_CreateOrUpdate).</span></span> <span data-ttu-id="619f1-126">Hello preavviso **modalità** è troppo**incrementale**.</span><span class="sxs-lookup"><span data-stu-id="619f1-126">Notice hello **mode** is set too**Incremental**.</span></span> <span data-ttu-id="619f1-127">impostare una distribuzione completa, toorun **modalità** troppo**completa**.</span><span class="sxs-lookup"><span data-stu-id="619f1-127">toorun a complete deployment, set **mode** too**Complete**.</span></span> <span data-ttu-id="619f1-128">Prestare attenzione quando si utilizza modalità di completamento hello come è possibile eliminare inavvertitamente le risorse che non sono presenti nel modello.</span><span class="sxs-lookup"><span data-stu-id="619f1-128">Be careful when using hello complete mode as you can inadvertently delete resources that are not in your template.</span></span>
   
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
   
      <span data-ttu-id="619f1-129">Se si desidera toolog del contenuto della risposta, il contenuto della richiesta o entrambi, includere **debugSetting** nella richiesta di hello.</span><span class="sxs-lookup"><span data-stu-id="619f1-129">If you want toolog response content, request content, or both, include **debugSetting** in hello request.</span></span>
   
        "debugSetting": {
          "detailLevel": "requestContent, responseContent"
        }
   
      <span data-ttu-id="619f1-130">È possibile impostare il toouse di account di archiviazione un token di firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="619f1-130">You can set up your storage account toouse a shared access signature (SAS) token.</span></span> <span data-ttu-id="619f1-131">Per altre informazioni, vedere [Delegating Access with a Shared Access Signature](https://docs.microsoft.com/rest/api/storageservices/delegating-access-with-a-shared-access-signature) (Delega dell'accesso con una firma di accesso condiviso).</span><span class="sxs-lookup"><span data-stu-id="619f1-131">For more information, see [Delegating Access with a Shared Access Signature](https://docs.microsoft.com/rest/api/storageservices/delegating-access-with-a-shared-access-signature).</span></span>
5. <span data-ttu-id="619f1-132">Ottenere lo stato di hello di distribuzione del modello hello.</span><span class="sxs-lookup"><span data-stu-id="619f1-132">Get hello status of hello template deployment.</span></span> <span data-ttu-id="619f1-133">Per altre informazioni, vedere [Get information about a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get) (Ottenere informazioni sulla distribuzione di un modello).</span><span class="sxs-lookup"><span data-stu-id="619f1-133">For more information, see [Get information about a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get).</span></span>
   
          GET https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>/providers/Microsoft.Resources/deployments/<YourDeploymentName>?api-version=2015-01-01
           <common headers>

## <a name="parameter-file"></a><span data-ttu-id="619f1-134">File di parametri</span><span class="sxs-lookup"><span data-stu-id="619f1-134">Parameter file</span></span>

[!INCLUDE [resource-manager-parameter-file](../../includes/resource-manager-parameter-file.md)]

## <a name="next-steps"></a><span data-ttu-id="619f1-135">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="619f1-135">Next steps</span></span>
* <span data-ttu-id="619f1-136">toolearn sulla gestione di operazioni asincrone di REST, vedere [tenere traccia delle operazioni asincrone di Azure](resource-manager-async-operations.md).</span><span class="sxs-lookup"><span data-stu-id="619f1-136">toolearn about handling asynchronous REST operations, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span></span>
* <span data-ttu-id="619f1-137">Per un esempio di distribuzione delle risorse tramite una libreria client .NET di hello, vedere [distribuire le risorse con le librerie .NET e un modello](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="619f1-137">For an example of deploying resources through hello .NET client library, see [Deploy resources using .NET libraries and a template](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="619f1-138">toodefine i parametri di modello, vedere [creazione di modelli](resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="619f1-138">toodefine parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="619f1-139">Per istruzioni sulla distribuzione negli ambienti toodifferent soluzione, vedere [gli ambienti di sviluppo e test in Microsoft Azure](solution-dev-test-environments.md).</span><span class="sxs-lookup"><span data-stu-id="619f1-139">For guidance on deploying your solution toodifferent environments, see [Development and test environments in Microsoft Azure](solution-dev-test-environments.md).</span></span>
* <span data-ttu-id="619f1-140">Per istruzioni su come le aziende possono usare tooeffectively Gestione risorse di gestione di sottoscrizioni, vedere [lo scaffolding di Azure enterprise - governance sottoscrizione rigorosa](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="619f1-140">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

