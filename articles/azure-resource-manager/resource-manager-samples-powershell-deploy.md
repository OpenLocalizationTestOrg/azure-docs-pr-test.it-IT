---
title: Esempio di script di Azure PowerShell - Distribuire un modello | Microsoft Docs
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
ms.openlocfilehash: b7a7dda1da653d084e02e6724d2f0cb5aa76807a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-resource-manager-template-deployment---powershell-script"></a><span data-ttu-id="6cd61-103">Distribuzione di modelli di Azure Resource Manager - Script di PowerShell</span><span class="sxs-lookup"><span data-stu-id="6cd61-103">Azure Resource Manager template deployment - PowerShell script</span></span>

<span data-ttu-id="6cd61-104">Questo script consente di distribuire un modello di Resource Manager in un gruppo di risorse nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="6cd61-104">This script deploys a Resource Manager template to a resource group in your subscription.</span></span>

[!INCLUDE [sample-powershell-install](../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="6cd61-105">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="6cd61-105">Sample script</span></span>

```powershell
<#
 .SYNOPSIS
    Deploys a template to Azure

 .DESCRIPTION
    Deploys an Azure Resource Manager template
#>

param (
    [Parameter(Mandatory)]
    #The subscription id where the template will be deployed.
    [string]$SubscriptionId,  

    [Parameter(Mandatory)]
    #The resource group where the template will be deployed. Can be the name of an existing or a new resource group.
    [string]$ResourceGroupName, 

    #Optional, a resource group location. If specified, will try to create a new resource group in this location. If not specified, assumes resource group is existing.
    [string]$ResourceGroupLocation, 

    #The deployment name.
    [Parameter(Mandatory)]
    [string]$DeploymentName,    

    #Path to the template file. Defaults to template.json.
    [string]$TemplateFilePath = "template.json",  

    #Path to the parameters file. Defaults to parameters.json. If file is not found, will prompt for parameter values based on template.
    [string]$ParametersFilePath = "parameters.json"
)

$ErrorActionPreference = "Stop"

# Login to Azure and select subscription
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

# Start the deployment
Write-Output "Starting deployment"
if ( Test-Path $ParametersFilePath ) {
    New-AzureRmResourceGroupDeployment -ResourceGroupName $ResourceGroupName -TemplateFile $TemplateFilePath -TemplateParameterFile $ParametersFilePath
}
else {
    New-AzureRmResourceGroupDeployment -ResourceGroupName $ResourceGroupName -TemplateFile $TemplateFilePath
}
``` 

## <a name="clean-up-deployment"></a><span data-ttu-id="6cd61-106">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="6cd61-106">Clean up deployment</span></span> 

<span data-ttu-id="6cd61-107">Eseguire il comando seguente per rimuovere il gruppo di risorse e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="6cd61-107">Run the following command to remove the resource group and all its resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="6cd61-108">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="6cd61-108">Script explanation</span></span>

<span data-ttu-id="6cd61-109">Questo script usa i comandi seguenti per creare la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="6cd61-109">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="6cd61-110">Ogni elemento della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="6cd61-110">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="6cd61-111">Comando</span><span class="sxs-lookup"><span data-stu-id="6cd61-111">Command</span></span> | <span data-ttu-id="6cd61-112">Note</span><span class="sxs-lookup"><span data-stu-id="6cd61-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="6cd61-113">Register-AzureRmResourceProvider</span><span class="sxs-lookup"><span data-stu-id="6cd61-113">Register-AzureRmResourceProvider</span></span>](/powershell/module/azurerm.resources/register-azurermresourceprovider) | <span data-ttu-id="6cd61-114">Registra un provider di risorse in modo che i relativi tipi di risorse possano essere distribuiti nella sottoscrizione in uso.</span><span class="sxs-lookup"><span data-stu-id="6cd61-114">Registers a resource provider so its resource types can be deployed to your subscription.</span></span>  |
| [<span data-ttu-id="6cd61-115">Get-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="6cd61-115">Get-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/get-azurermresourcegroup) | <span data-ttu-id="6cd61-116">Ottiene i gruppi di risorse.</span><span class="sxs-lookup"><span data-stu-id="6cd61-116">Gets resource groups.</span></span>  |
| [<span data-ttu-id="6cd61-117">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="6cd61-117">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="6cd61-118">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="6cd61-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="6cd61-119">New-AzureRmResourceGroupDeployment</span><span class="sxs-lookup"><span data-stu-id="6cd61-119">New-AzureRmResourceGroupDeployment</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) | <span data-ttu-id="6cd61-120">Aggiunge una distribuzione di Azure a un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="6cd61-120">Adds an Azure deployment to a resource group.</span></span>  |
| [<span data-ttu-id="6cd61-121">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="6cd61-121">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="6cd61-122">Rimuove un gruppo di risorse e tutte le risorse contenute al suo interno.</span><span class="sxs-lookup"><span data-stu-id="6cd61-122">Removes a resource group and all resources contained within.</span></span> |



## <a name="next-steps"></a><span data-ttu-id="6cd61-123">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6cd61-123">Next steps</span></span>
* <span data-ttu-id="6cd61-124">Per un'introduzione alla distribuzione dei modelli, vedere [Distribuire le risorse con i modelli di Resource Manager e Azure PowerShell](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="6cd61-124">For an introduction to deploying templates, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy.md).</span></span>
* <span data-ttu-id="6cd61-125">Per informazioni sulla distribuzione di un modello che richiede un token di firma di accesso condiviso, vedere [Distribuire un modello privato con un token di firma di accesso condiviso](resource-manager-powershell-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="6cd61-125">For information about deploying a template that requires a SAS token, see [Deploy private template with SAS token](resource-manager-powershell-sas-token.md).</span></span>
* <span data-ttu-id="6cd61-126">Per definire i parametri nel modello, vedere [Creazione di modelli](resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="6cd61-126">To define parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="6cd61-127">Per indicazioni su come le aziende possono usare Resource Manager per gestire efficacemente le sottoscrizioni, vedere [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md) (Scaffolding aziendale Azure - Governance prescrittiva per le sottoscrizioni).</span><span class="sxs-lookup"><span data-stu-id="6cd61-127">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

