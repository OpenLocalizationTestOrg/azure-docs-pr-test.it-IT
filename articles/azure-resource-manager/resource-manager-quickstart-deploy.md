---
title: aaaDeploy risorse tooAzure | Documenti Microsoft
description: Usare Azure PowerShell o l'interfaccia CLI di Azure tooAzure risorse toodeploy. risorse di Hello vengono definite in un modello di gestione risorse.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/16/2017
ms.author: tomfitz
ms.openlocfilehash: 0cd3f8ad45af1fb85c78899b56f6807d00b859f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-tooazure"></a><span data-ttu-id="b8241-104">Distribuire le risorse tooAzure</span><span class="sxs-lookup"><span data-stu-id="b8241-104">Deploy resources tooAzure</span></span>

<span data-ttu-id="b8241-105">Questo argomento viene illustrato come toodeploy risorse tooyour sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="b8241-105">This topic shows how toodeploy resources tooyour Azure subscription.</span></span> <span data-ttu-id="b8241-106">È possibile usare Azure PowerShell o Azure CLI toodeploy un modello di gestione risorse che definisce l'infrastruttura di hello per la soluzione.</span><span class="sxs-lookup"><span data-stu-id="b8241-106">You can use either Azure PowerShell or Azure CLI toodeploy a Resource Manager template that defines hello infrastructure for your solution.</span></span>

<span data-ttu-id="b8241-107">Per un'introduzione tooconcepts di gestione risorse, vedere [Panoramica di gestione risorse di Azure](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b8241-107">For an introduction tooconcepts of Resource Manager, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>

## <a name="steps-for-deployment"></a><span data-ttu-id="b8241-108">Procedura per la distribuzione</span><span class="sxs-lookup"><span data-stu-id="b8241-108">Steps for deployment</span></span>

<span data-ttu-id="b8241-109">In questo argomento si presuppone che si sta distribuendo hello [modello di archiviazione di esempio](#example-storage-template) in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="b8241-109">This topic assumes you are deploying hello [example storage template](#example-storage-template) in this topic.</span></span> <span data-ttu-id="b8241-110">È possibile utilizzare un modello diverso, ma i parametri di hello che passare sono diversi rispetto a quanto mostrato in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="b8241-110">You can use a different template, but hello parameters you pass are different than what is shown in this topic.</span></span>

<span data-ttu-id="b8241-111">Dopo aver creato un modello, hello generale per la distribuzione del modello di passaggi:</span><span class="sxs-lookup"><span data-stu-id="b8241-111">After creating a template, hello general steps for deploying your template are:</span></span>

1. <span data-ttu-id="b8241-112">Accedi tooyour account</span><span class="sxs-lookup"><span data-stu-id="b8241-112">Log in tooyour account</span></span>
2. <span data-ttu-id="b8241-113">Selezionare toouse sottoscrizione hello (necessario solo se si dispone di più sottoscrizioni e si desidera toouse uno che non sia sottoscrizione predefinita hello)</span><span class="sxs-lookup"><span data-stu-id="b8241-113">Select hello subscription toouse (only necessary if you have multiple subscriptions, and you want toouse one that is not hello default subscription)</span></span>
3. <span data-ttu-id="b8241-114">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="b8241-114">Create a resource group</span></span>
4. <span data-ttu-id="b8241-115">Distribuire il modello di hello</span><span class="sxs-lookup"><span data-stu-id="b8241-115">Deploy hello template</span></span>
5. <span data-ttu-id="b8241-116">Controllare lo stato della distribuzione</span><span class="sxs-lookup"><span data-stu-id="b8241-116">Check your deployment status</span></span>

<span data-ttu-id="b8241-117">Hello nelle sezioni seguenti mostrano come tooperform tali passaggi con [PowerShell](#powershell) o [CLI di Azure](#azure-cli).</span><span class="sxs-lookup"><span data-stu-id="b8241-117">hello following sections show how tooperform those steps with [PowerShell](#powershell) or [Azure CLI](#azure-cli).</span></span>

## <a name="powershell"></a><span data-ttu-id="b8241-118">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b8241-118">PowerShell</span></span>

1. <span data-ttu-id="b8241-119">tooinstall Azure PowerShell, vedere [Introduzione ai cmdlet di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b8241-119">tooinstall Azure PowerShell, see [Get started with Azure PowerShell cmdlets](/powershell/azure/overview).</span></span>

2. <span data-ttu-id="b8241-120">tooquickly Introduzione alla distribuzione, utilizzare hello seguente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="b8241-120">tooquickly get started with deployment, use hello following cmdlets:</span></span>

  ```powershell
  Login-AzureRmAccount
  Set-AzureRmContext -SubscriptionID {subscription-id}

  New-AzureRmResourceGroup -Name ExampleGroup -Location "Central US"
  New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleGroup -TemplateFile c:\MyTemplates\azuredeploy.json 
  ```

  <span data-ttu-id="b8241-121">Hello `Set-AzureRmContext` cmdlet è necessario solo se si desidera toouse una sottoscrizione diversa da abbonamento predefinito.</span><span class="sxs-lookup"><span data-stu-id="b8241-121">hello `Set-AzureRmContext` cmdlet is only needed if you want toouse a subscription other than your default subscription.</span></span> <span data-ttu-id="b8241-122">toosee tutte le sottoscrizioni e i relativi ID, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="b8241-122">toosee all your subscriptions and their IDs, use:</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

3. <span data-ttu-id="b8241-123">distribuzione di Hello può richiedere alcuni minuti toocomplete.</span><span class="sxs-lookup"><span data-stu-id="b8241-123">hello deployment can take a few minutes toocomplete.</span></span> <span data-ttu-id="b8241-124">Al termine, viene visualizzato un messaggio simile a:</span><span class="sxs-lookup"><span data-stu-id="b8241-124">When it finishes, you see a message similar to:</span></span>

  ```powershell
  DeploymentName          : ExampleDeployment
  CorrelationId           : 07b3b233-8367-4a0b-b9bc-7aa189065665
  ResourceGroupName       : ExampleGroup
  ProvisioningState       : Succeeded
  ...
  ```

4. <span data-ttu-id="b8241-125">toosee che l'account di archiviazione e di gruppo di risorse sono stati distribuiti tooyour sottoscrizione, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="b8241-125">toosee that your resource group and storage account were deployed tooyour subscription, use:</span></span>

  ```powershell
  Get-AzureRmResourceGroup -Name ExampleGroup
  Find-AzureRmResource -ResourceGroupNameEquals ExampleGroup
  ```

5. <span data-ttu-id="b8241-126">Quando si distribuisce un modello, è possibile specificare i parametri del modello come parametri di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b8241-126">You can specify template parameters as PowerShell parameters when deploying a template.</span></span> <span data-ttu-id="b8241-127">Hello l'esempio precedente non include alcun parametro di modello, pertanto sono stati utilizzati i valori predefiniti di hello nel modello di hello.</span><span class="sxs-lookup"><span data-stu-id="b8241-127">hello earlier example did not include any template parameters, so hello default values in hello template were used.</span></span> <span data-ttu-id="b8241-128">toodeploy archiviazione un altro account e specificare i valori dei parametri per prefisso del nome di archiviazione hello e account di archiviazione hello SKU, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="b8241-128">toodeploy another storage account, and provide parameter values for hello storage name prefix and hello storage account SKU, use:</span></span>

  ```powershell
  New-AzureRmResourceGroupDeployment -Name ExampleDeployment2 -ResourceGroupName ExampleGroup -TemplateFile c:\MyTemplates\azuredeploy.json -storageNamePrefix "contoso" -storageSKU "Standard_GRS"
  ```

  <span data-ttu-id="b8241-129">Si dispone ora di due account di archiviazione nel gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="b8241-129">You now have two storage accounts in your resource group.</span></span> 

## <a name="azure-cli"></a><span data-ttu-id="b8241-130">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="b8241-130">Azure CLI</span></span>

1. <span data-ttu-id="b8241-131">tooinstall CLI di Azure, vedere [installare Azure CLI 2.0](/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="b8241-131">tooinstall Azure CLI, see [Install Azure CLI 2.0](/cli/azure/install-az-cli2).</span></span>

2. <span data-ttu-id="b8241-132">tooquickly Introduzione alla distribuzione, utilizzare hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="b8241-132">tooquickly get started with deployment, use hello following commands:</span></span>

  ```azurecli
  az login
  az account set --subscription {subscription-id}

  az group create --name ExampleGroup --location "Central US"
  az group deployment create --name ExampleDeployment --resource-group ExampleGroup --template-file c:\MyTemplates\azuredeploy.json
  ```

  <span data-ttu-id="b8241-133">Hello `az account set` comando è necessario solo se si desidera toouse una sottoscrizione diversa da abbonamento predefinito.</span><span class="sxs-lookup"><span data-stu-id="b8241-133">hello `az account set` command is only needed if you want toouse a subscription other than your default subscription.</span></span> <span data-ttu-id="b8241-134">toosee tutte le sottoscrizioni e i relativi ID, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="b8241-134">toosee all your subscriptions and their IDs, use:</span></span>

  ```azurecli
  az account list
  ```

3. <span data-ttu-id="b8241-135">distribuzione di Hello può richiedere alcuni minuti toocomplete.</span><span class="sxs-lookup"><span data-stu-id="b8241-135">hello deployment can take a few minutes toocomplete.</span></span> <span data-ttu-id="b8241-136">Al termine, viene visualizzato un messaggio simile a:</span><span class="sxs-lookup"><span data-stu-id="b8241-136">When it finishes, you see a message similar to:</span></span>

  ```azurecli
  "provisioningState": "Succeeded",
  ```

4. <span data-ttu-id="b8241-137">toosee che l'account di archiviazione e di gruppo di risorse sono stati distribuiti tooyour sottoscrizione, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="b8241-137">toosee that your resource group and storage account were deployed tooyour subscription, use:</span></span>

  ```azurecli
  az group show --name ExampleGroup
  az resource list --resource-group ExampleGroup
  ```

5. <span data-ttu-id="b8241-138">Quando si distribuisce un modello, è possibile specificare i parametri del modello come parametri di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b8241-138">You can specify template parameters as PowerShell parameters when deploying a template.</span></span> <span data-ttu-id="b8241-139">Hello l'esempio precedente non include alcun parametro di modello, pertanto sono stati utilizzati i valori predefiniti di hello nel modello di hello.</span><span class="sxs-lookup"><span data-stu-id="b8241-139">hello earlier example did not include any template parameters, so hello default values in hello template were used.</span></span> <span data-ttu-id="b8241-140">toodeploy archiviazione un altro account e specificare i valori dei parametri per prefisso del nome di archiviazione hello e account di archiviazione hello SKU, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="b8241-140">toodeploy another storage account, and provide parameter values for hello storage name prefix and hello storage account SKU, use:</span></span>

  ```azurecli
  az group deployment create --name ExampleDeployment2 --resource-group ExampleGroup --template-file c:\MyTemplates\azuredeploy.json --parameters '{"storageNamePrefix":{"value":"contoso"},"storageSKU":{"value":"Standard_GRS"}}'
  ```

  <span data-ttu-id="b8241-141">Si dispone ora di due account di archiviazione nel gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="b8241-141">You now have two storage accounts in your resource group.</span></span> 

## <a name="example-storage-template"></a><span data-ttu-id="b8241-142">Modello di archiviazione di esempio</span><span class="sxs-lookup"><span data-stu-id="b8241-142">Example storage template</span></span>

<span data-ttu-id="b8241-143">Utilizzare hello seguente modello di esempio toodeploy sottoscrizione tooyour un account di archiviazione:</span><span class="sxs-lookup"><span data-stu-id="b8241-143">Use hello following example template toodeploy a storage account tooyour subscription:</span></span>

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageNamePrefix": {
      "type": "string",
      "maxLength": 11,
      "defaultValue": "storage",
      "metadata": {
        "description": "hello value toouse for starting hello storage account name."
      }
    },
    "storageSKU": {
      "type": "string",
      "allowedValues": [
        "Standard_LRS",
        "Standard_ZRS",
        "Standard_GRS",
        "Standard_RAGRS",
        "Premium_LRS"
      ],
      "defaultValue": "Standard_LRS",
      "metadata": {
        "description": "hello type of replication toouse for hello storage account."
      }
    }
  },
  "variables": {
    "storageName": "[concat(parameters('storageNamePrefix'), uniqueString(resourceGroup().id))]"
  },
  "resources": [
    {
      "name": "[variables('storageName')]",
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "2016-05-01",
      "sku": {
        "name": "[parameters('storageSKU')]"
      },
      "kind": "Storage",
      "location": "[resourceGroup().location]",
      "tags": {},
      "properties": {
      }
    }
  ],
  "outputs": {  }
}
```

## <a name="next-steps"></a><span data-ttu-id="b8241-144">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b8241-144">Next steps</span></span>

* <span data-ttu-id="b8241-145">Per informazioni dettagliate sull'utilizzo di PowerShell toodeploy modelli, vedere [distribuire le risorse e modelli di gestione risorse di Azure PowerShell](/azure/azure-resource-manager/resource-group-template-deploy).</span><span class="sxs-lookup"><span data-stu-id="b8241-145">For detailed information about using PowerShell toodeploy templates, see [Deploy resources with Resource Manager templates and Azure PowerShell](/azure/azure-resource-manager/resource-group-template-deploy).</span></span>
* <span data-ttu-id="b8241-146">Per informazioni dettagliate sull'utilizzo dei modelli toodeploy CLI di Azure, vedere [distribuire le risorse con i modelli di gestione risorse e CLI di Azure](/azure/azure-resource-manager/resource-group-template-deploy-cli).</span><span class="sxs-lookup"><span data-stu-id="b8241-146">For detailed information about using Azure CLI toodeploy templates, see [Deploy resources with Resource Manager templates and Azure CLI](/azure/azure-resource-manager/resource-group-template-deploy-cli).</span></span>



