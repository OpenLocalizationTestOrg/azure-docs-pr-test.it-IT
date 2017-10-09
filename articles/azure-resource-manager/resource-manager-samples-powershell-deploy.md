---
title: aaaAzure Script di PowerShell di esempio - distribuire il modello | Documenti Microsoft
description: Esempio di script per la distribuzione di un modello di Azure Resource Manager.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: tomfitz
ms.openlocfilehash: 536b8ccecad4ed8a4c4a4139c6bf4600e2eb9405
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-manager-template-deployment---powershell-script"></a><span data-ttu-id="58e05-103">Distribuzione di modelli di Azure Resource Manager - Script di PowerShell</span><span class="sxs-lookup"><span data-stu-id="58e05-103">Azure Resource Manager template deployment - PowerShell script</span></span>

<span data-ttu-id="58e05-104">Questo script consente di distribuire un gruppo di risorse tooa modello di gestione delle risorse nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="58e05-104">This script deploys a Resource Manager template tooa resource group in your subscription.</span></span>

[!INCLUDE [sample-powershell-install](../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="58e05-105">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="58e05-105">Sample script</span></span>

```powershell
<#
 .SYNOPSIS
    Deploys a template tooAzure

 .DESCRIPTION
    Deploys an Azure Resource Manager template
#>

param (
    [Parameter(Mandatory)]
    #hello subscription id where hello template will be deployed.
    [string]$SubscriptionId,  

    [Parameter(Mandatory)]
    #hello resource group where hello template will be deployed. Can be hello name of an existing or a new resource group.
    [string]$ResourceGroupName, 

    #Optional, a resource group location. If specified, will try toocreate a new resource group in this location. If not specified, assumes resource group is existing.
    [string]$ResourceGroupLocation, 

    #hello deployment name.
    [Parameter(Mandatory)]
    [string]$DeploymentName,    

    #Path toohello template file. Defaults tootemplate.json.
    [string]$TemplateFilePath = "template.json",  

    #Path toohello parameters file. Defaults tooparameters.json. If file is not found, will prompt for parameter values based on template.
    [string]$ParametersFilePath = "parameters.json"
)

$ErrorActionPreference = "Stop"

# Login tooAzure and select subscription
Write-Output "Logging in"
Login-AzureRmAccount
Write-Output "Selecting subscription '$SubscriptionId'"
Select-AzureRmSubscription -SubscriptionID $SubscriptionId

# Create or check for existing resource group
$resourceGroup = Get-AzureRmResourceGroup -Name $ResourceGroupName -ErrorAction SilentlyContinue
if ( -not $ResourceGroup ) {
    Write-Output "Could not find resource group '$ResourceGroupName' - will create it"
    if ( -not $ResourceGroupLocation ) {
        $ResourceGroupLocation = Read-Host -Prompt 'Enter location for resource group'
    }
    Write-Output "Creating resource group '$ResourceGroupName' in location '$ResourceGroupLocation'"
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $resourceGroupLocation
}
else {
    Write-Output "Using existing resource group '$ResourceGroupName'"
}

# Start hello deployment
Write-Output "Starting deployment"
if ( Test-Path $ParametersFilePath ) {
    New-AzureRmResourceGroupDeployment -ResourceGroupName $ResourceGroupName -TemplateFile $TemplateFilePath -TemplateParameterFile $ParametersFilePath
}
else {
    New-AzureRmResourceGroupDeployment -ResourceGroupName $ResourceGroupName -TemplateFile $TemplateFilePath
}
``` 

## <a name="clean-up-deployment"></a><span data-ttu-id="58e05-106">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="58e05-106">Clean up deployment</span></span> 

<span data-ttu-id="58e05-107">Comando che segue hello esecuzione gruppo di risorse tooremove hello e tutte le relative risorse.</span><span class="sxs-lookup"><span data-stu-id="58e05-107">Run hello following command tooremove hello resource group and all its resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="58e05-108">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="58e05-108">Script explanation</span></span>

<span data-ttu-id="58e05-109">Questo script utilizza hello dopo la distribuzione di comandi toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="58e05-109">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="58e05-110">Ogni elemento nella documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="58e05-110">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="58e05-111">Comando</span><span class="sxs-lookup"><span data-stu-id="58e05-111">Command</span></span> | <span data-ttu-id="58e05-112">Note</span><span class="sxs-lookup"><span data-stu-id="58e05-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="58e05-113">Register-AzureRmResourceProvider</span><span class="sxs-lookup"><span data-stu-id="58e05-113">Register-AzureRmResourceProvider</span></span>](/powershell/module/azurerm.resources/register-azurermresourceprovider) | <span data-ttu-id="58e05-114">Registra un provider di risorse in modo relativi tipi di risorse possono essere distribuito tooyour sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="58e05-114">Registers a resource provider so its resource types can be deployed tooyour subscription.</span></span>  |
| [<span data-ttu-id="58e05-115">Get-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="58e05-115">Get-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/get-azurermresourcegroup) | <span data-ttu-id="58e05-116">Ottiene i gruppi di risorse.</span><span class="sxs-lookup"><span data-stu-id="58e05-116">Gets resource groups.</span></span>  |
| [<span data-ttu-id="58e05-117">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="58e05-117">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="58e05-118">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="58e05-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="58e05-119">New-AzureRmResourceGroupDeployment</span><span class="sxs-lookup"><span data-stu-id="58e05-119">New-AzureRmResourceGroupDeployment</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) | <span data-ttu-id="58e05-120">Aggiunge un gruppo di risorse tooa di distribuzione di Azure.</span><span class="sxs-lookup"><span data-stu-id="58e05-120">Adds an Azure deployment tooa resource group.</span></span>  |
| [<span data-ttu-id="58e05-121">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="58e05-121">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="58e05-122">Rimuove un gruppo di risorse e tutte le risorse contenute al suo interno.</span><span class="sxs-lookup"><span data-stu-id="58e05-122">Removes a resource group and all resources contained within.</span></span> |



## <a name="next-steps"></a><span data-ttu-id="58e05-123">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="58e05-123">Next steps</span></span>
* <span data-ttu-id="58e05-124">Per i modelli di toodeploying un'introduzione, vedere [distribuire le risorse e modelli di gestione risorse di Azure PowerShell](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="58e05-124">For an introduction toodeploying templates, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy.md).</span></span>
* <span data-ttu-id="58e05-125">Per informazioni sulla distribuzione di un modello che richiede un token di firma di accesso condiviso, vedere [Distribuire un modello privato con un token di firma di accesso condiviso](resource-manager-powershell-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="58e05-125">For information about deploying a template that requires a SAS token, see [Deploy private template with SAS token](resource-manager-powershell-sas-token.md).</span></span>
* <span data-ttu-id="58e05-126">toodefine i parametri di modello, vedere [creazione di modelli](resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="58e05-126">toodefine parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="58e05-127">Per istruzioni su come le aziende possono usare tooeffectively Gestione risorse di gestione di sottoscrizioni, vedere [lo scaffolding di Azure enterprise - governance sottoscrizione rigorosa](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="58e05-127">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

