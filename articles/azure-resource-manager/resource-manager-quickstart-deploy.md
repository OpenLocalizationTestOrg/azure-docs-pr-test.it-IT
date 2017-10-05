---
title: Distribuire risorse in Azure | Microsoft Docs
description: Usare Azure PowerShell o l'interfaccia della riga di comando di Azure per distribuire le risorse in Azure. Le risorse sono definite in un modello di Resource Manager.
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
ms.openlocfilehash: 19d5ec337a18b1a159de05ed611b2ccd0c15c592
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-resources-to-azure"></a><span data-ttu-id="afd8d-104">Distribuire risorse in Azure</span><span class="sxs-lookup"><span data-stu-id="afd8d-104">Deploy resources to Azure</span></span>

<span data-ttu-id="afd8d-105">In questo articolo viene illustrato come distribuire le risorse nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="afd8d-105">This topic shows how to deploy resources to your Azure subscription.</span></span> <span data-ttu-id="afd8d-106">È possibile usare Azure PowerShell o l'interfaccia della riga di comando di Azure per distribuire un modello di Resource Manager che definisce l'infrastruttura per la soluzione.</span><span class="sxs-lookup"><span data-stu-id="afd8d-106">You can use either Azure PowerShell or Azure CLI to deploy a Resource Manager template that defines the infrastructure for your solution.</span></span>

<span data-ttu-id="afd8d-107">Per un'introduzione ai concetti di Gestione risorse, vedere [Panoramica di Azure Rseource Manager](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="afd8d-107">For an introduction to concepts of Resource Manager, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>

## <a name="steps-for-deployment"></a><span data-ttu-id="afd8d-108">Procedura per la distribuzione</span><span class="sxs-lookup"><span data-stu-id="afd8d-108">Steps for deployment</span></span>

<span data-ttu-id="afd8d-109">In questo argomento si presuppone che l'utente stia distribuendo il [modello di archiviazione di esempio](#example-storage-template) in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="afd8d-109">This topic assumes you are deploying the [example storage template](#example-storage-template) in this topic.</span></span> <span data-ttu-id="afd8d-110">È possibile usare un modello diverso, ma i parametri usati saranno diversi da quelli mostrati di seguito.</span><span class="sxs-lookup"><span data-stu-id="afd8d-110">You can use a different template, but the parameters you pass are different than what is shown in this topic.</span></span>

<span data-ttu-id="afd8d-111">Dopo aver creato un modello, la procedura generale per la distribuzione del modello consiste in:</span><span class="sxs-lookup"><span data-stu-id="afd8d-111">After creating a template, the general steps for deploying your template are:</span></span>

1. <span data-ttu-id="afd8d-112">Accedere all'account</span><span class="sxs-lookup"><span data-stu-id="afd8d-112">Log in to your account</span></span>
2. <span data-ttu-id="afd8d-113">Selezionare la sottoscrizione da usare (necessario solo se si dispone di più sottoscrizioni e se si desidera usarne una diversa dalla sottoscrizione predefinita)</span><span class="sxs-lookup"><span data-stu-id="afd8d-113">Select the subscription to use (only necessary if you have multiple subscriptions, and you want to use one that is not the default subscription)</span></span>
3. <span data-ttu-id="afd8d-114">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="afd8d-114">Create a resource group</span></span>
4. <span data-ttu-id="afd8d-115">Distribuire il modello</span><span class="sxs-lookup"><span data-stu-id="afd8d-115">Deploy the template</span></span>
5. <span data-ttu-id="afd8d-116">Controllare lo stato della distribuzione</span><span class="sxs-lookup"><span data-stu-id="afd8d-116">Check your deployment status</span></span>

<span data-ttu-id="afd8d-117">Nelle sezioni seguenti viene illustrato come eseguire questa procedura con [PowerShell](#powershell) o con l'[interfaccia della riga di comando di Azure](#azure-cli).</span><span class="sxs-lookup"><span data-stu-id="afd8d-117">The following sections show how to perform those steps with [PowerShell](#powershell) or [Azure CLI](#azure-cli).</span></span>

## <a name="powershell"></a><span data-ttu-id="afd8d-118">PowerShell</span><span class="sxs-lookup"><span data-stu-id="afd8d-118">PowerShell</span></span>

1. <span data-ttu-id="afd8d-119">Per installare Azure PowerShell vedere [Get started with Azure PowerShell cmdlets](/powershell/azure/overview) (Guida introduttiva ai cmdlet di Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="afd8d-119">To install Azure PowerShell, see [Get started with Azure PowerShell cmdlets](/powershell/azure/overview).</span></span>

2. <span data-ttu-id="afd8d-120">Per iniziare a usare rapidamente la distribuzione, usare i cmdlets seguenti:</span><span class="sxs-lookup"><span data-stu-id="afd8d-120">To quickly get started with deployment, use the following cmdlets:</span></span>

  ```powershell
  Login-AzureRmAccount
  Set-AzureRmContext -SubscriptionID {subscription-id}

  New-AzureRmResourceGroup -Name ExampleGroup -Location "Central US"
  New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleGroup -TemplateFile c:\MyTemplates\azuredeploy.json 
  ```

  <span data-ttu-id="afd8d-121">Il cmdlet `Set-AzureRmContext` è necessario solo se si desidera usare una sottoscrizione diversa dalla sottoscrizione predefinita.</span><span class="sxs-lookup"><span data-stu-id="afd8d-121">The `Set-AzureRmContext` cmdlet is only needed if you want to use a subscription other than your default subscription.</span></span> <span data-ttu-id="afd8d-122">Per vedere tutte le sottoscrizioni e i relativi ID, usare:</span><span class="sxs-lookup"><span data-stu-id="afd8d-122">To see all your subscriptions and their IDs, use:</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

3. <span data-ttu-id="afd8d-123">Per il completamento della distribuzione sarà necessario attendere alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="afd8d-123">The deployment can take a few minutes to complete.</span></span> <span data-ttu-id="afd8d-124">Al termine, viene visualizzato un messaggio simile a:</span><span class="sxs-lookup"><span data-stu-id="afd8d-124">When it finishes, you see a message similar to:</span></span>

  ```powershell
  DeploymentName          : ExampleDeployment
  CorrelationId           : 07b3b233-8367-4a0b-b9bc-7aa189065665
  ResourceGroupName       : ExampleGroup
  ProvisioningState       : Succeeded
  ...
  ```

4. <span data-ttu-id="afd8d-125">Per verificare che l'account di archiviazione e il gruppo di risorse siano stati distribuiti per la sottoscrizione, usare:</span><span class="sxs-lookup"><span data-stu-id="afd8d-125">To see that your resource group and storage account were deployed to your subscription, use:</span></span>

  ```powershell
  Get-AzureRmResourceGroup -Name ExampleGroup
  Find-AzureRmResource -ResourceGroupNameEquals ExampleGroup
  ```

5. <span data-ttu-id="afd8d-126">Quando si distribuisce un modello, è possibile specificare i parametri del modello come parametri di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="afd8d-126">You can specify template parameters as PowerShell parameters when deploying a template.</span></span> <span data-ttu-id="afd8d-127">L'esempio precedente non comprendeva i parametri del modello, pertanto nel modello sono stati usati i valori predefiniti.</span><span class="sxs-lookup"><span data-stu-id="afd8d-127">The earlier example did not include any template parameters, so the default values in the template were used.</span></span> <span data-ttu-id="afd8d-128">Per distribuire un altro account di archiviazione e fornire i valori dei parametri per il prefisso del nome di archiviazione e lo SKU dell'account di archiviazione, usare:</span><span class="sxs-lookup"><span data-stu-id="afd8d-128">To deploy another storage account, and provide parameter values for the storage name prefix and the storage account SKU, use:</span></span>

  ```powershell
  New-AzureRmResourceGroupDeployment -Name ExampleDeployment2 -ResourceGroupName ExampleGroup -TemplateFile c:\MyTemplates\azuredeploy.json -storageNamePrefix "contoso" -storageSKU "Standard_GRS"
  ```

  <span data-ttu-id="afd8d-129">Si dispone ora di due account di archiviazione nel gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="afd8d-129">You now have two storage accounts in your resource group.</span></span> 

## <a name="azure-cli"></a><span data-ttu-id="afd8d-130">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="afd8d-130">Azure CLI</span></span>

1. <span data-ttu-id="afd8d-131">Per installare l'interfaccia della riga di comando di Azure, vedere [Install Azure CLI 2.0](/cli/azure/install-az-cli2) (Installare l'interfaccia della riga di comando di Azure 2.0).</span><span class="sxs-lookup"><span data-stu-id="afd8d-131">To install Azure CLI, see [Install Azure CLI 2.0](/cli/azure/install-az-cli2).</span></span>

2. <span data-ttu-id="afd8d-132">Per iniziare a usare rapidamente la distribuzione, usare i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="afd8d-132">To quickly get started with deployment, use the following commands:</span></span>

  ```azurecli
  az login
  az account set --subscription {subscription-id}

  az group create --name ExampleGroup --location "Central US"
  az group deployment create --name ExampleDeployment --resource-group ExampleGroup --template-file c:\MyTemplates\azuredeploy.json
  ```

  <span data-ttu-id="afd8d-133">Il comando `az account set` è necessario solo se si desidera usare una sottoscrizione diversa dalla sottoscrizione predefinita.</span><span class="sxs-lookup"><span data-stu-id="afd8d-133">The `az account set` command is only needed if you want to use a subscription other than your default subscription.</span></span> <span data-ttu-id="afd8d-134">Per vedere tutte le sottoscrizioni e i relativi ID, usare:</span><span class="sxs-lookup"><span data-stu-id="afd8d-134">To see all your subscriptions and their IDs, use:</span></span>

  ```azurecli
  az account list
  ```

3. <span data-ttu-id="afd8d-135">Per il completamento della distribuzione sarà necessario attendere alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="afd8d-135">The deployment can take a few minutes to complete.</span></span> <span data-ttu-id="afd8d-136">Al termine, viene visualizzato un messaggio simile a:</span><span class="sxs-lookup"><span data-stu-id="afd8d-136">When it finishes, you see a message similar to:</span></span>

  ```azurecli
  "provisioningState": "Succeeded",
  ```

4. <span data-ttu-id="afd8d-137">Per verificare che l'account di archiviazione e il gruppo di risorse siano stati distribuiti per la sottoscrizione, usare:</span><span class="sxs-lookup"><span data-stu-id="afd8d-137">To see that your resource group and storage account were deployed to your subscription, use:</span></span>

  ```azurecli
  az group show --name ExampleGroup
  az resource list --resource-group ExampleGroup
  ```

5. <span data-ttu-id="afd8d-138">Quando si distribuisce un modello, è possibile specificare i parametri del modello come parametri di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="afd8d-138">You can specify template parameters as PowerShell parameters when deploying a template.</span></span> <span data-ttu-id="afd8d-139">L'esempio precedente non comprendeva i parametri del modello, pertanto nel modello sono stati usati i valori predefiniti.</span><span class="sxs-lookup"><span data-stu-id="afd8d-139">The earlier example did not include any template parameters, so the default values in the template were used.</span></span> <span data-ttu-id="afd8d-140">Per distribuire un altro account di archiviazione e fornire i valori dei parametri per il prefisso del nome di archiviazione e lo SKU dell'account di archiviazione, usare:</span><span class="sxs-lookup"><span data-stu-id="afd8d-140">To deploy another storage account, and provide parameter values for the storage name prefix and the storage account SKU, use:</span></span>

  ```azurecli
  az group deployment create --name ExampleDeployment2 --resource-group ExampleGroup --template-file c:\MyTemplates\azuredeploy.json --parameters '{"storageNamePrefix":{"value":"contoso"},"storageSKU":{"value":"Standard_GRS"}}'
  ```

  <span data-ttu-id="afd8d-141">Si dispone ora di due account di archiviazione nel gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="afd8d-141">You now have two storage accounts in your resource group.</span></span> 

## <a name="example-storage-template"></a><span data-ttu-id="afd8d-142">Modello di archiviazione di esempio</span><span class="sxs-lookup"><span data-stu-id="afd8d-142">Example storage template</span></span>

<span data-ttu-id="afd8d-143">Per distribuire un account di archiviazione nella sottoscrizione, usare il modello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="afd8d-143">Use the following example template to deploy a storage account to your subscription:</span></span>

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
        "description": "The value to use for starting the storage account name."
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
        "description": "The type of replication to use for the storage account."
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

## <a name="next-steps"></a><span data-ttu-id="afd8d-144">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="afd8d-144">Next steps</span></span>

* <span data-ttu-id="afd8d-145">Per informazioni dettagliate sull'uso di PowerShell per distribuire i modelli, vedere [Distribuire le risorse con i modelli di Azure Resource Manager e Azure PowerShell](/azure/azure-resource-manager/resource-group-template-deploy).</span><span class="sxs-lookup"><span data-stu-id="afd8d-145">For detailed information about using PowerShell to deploy templates, see [Deploy resources with Resource Manager templates and Azure PowerShell](/azure/azure-resource-manager/resource-group-template-deploy).</span></span>
* <span data-ttu-id="afd8d-146">Per informazioni dettagliate sull'uso dell'interfaccia della riga di comando di Azure per distribuire i modelli, vedere [Distribuire le risorse con i modelli di Azure Resource Manager e l'interfaccia della riga di comando di Azure](/azure/azure-resource-manager/resource-group-template-deploy-cli).</span><span class="sxs-lookup"><span data-stu-id="afd8d-146">For detailed information about using Azure CLI to deploy templates, see [Deploy resources with Resource Manager templates and Azure CLI](/azure/azure-resource-manager/resource-group-template-deploy-cli).</span></span>



