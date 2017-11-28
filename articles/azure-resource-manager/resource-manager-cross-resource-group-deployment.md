---
title: gruppi di risorse toomultiple aaaDeploy risorse di Azure | Documenti Microsoft
description: "Viene illustrato come raggruppare i tootarget più di una risorsa di Azure durante la distribuzione."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/15/2017
ms.author: tomfitz
ms.openlocfilehash: 93a39a26e0ca18dfcb5c6e8de95c38a64186d6de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-azure-resources-toomore-than-one-resource-group"></a><span data-ttu-id="0c07a-103">Distribuire le risorse di Azure toomore rispetto a un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="0c07a-103">Deploy Azure resources toomore than one resource group</span></span>

<span data-ttu-id="0c07a-104">In genere, si distribuisce tutte le risorse di hello del modello tooa singolo gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="0c07a-104">Typically, you deploy all hello resources in your template tooa single resource group.</span></span> <span data-ttu-id="0c07a-105">Tuttavia, esistono scenari in cui si desidera un set di risorse toodeploy insieme ma posizionarli in diversi gruppi di risorse.</span><span class="sxs-lookup"><span data-stu-id="0c07a-105">However, there are scenarios where you want toodeploy a set of resources together but place them in different resource groups.</span></span> <span data-ttu-id="0c07a-106">Ad esempio, è consigliabile toodeploy hello backup virtual machine per percorso e il gruppo di risorse distinto tooa Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="0c07a-106">For example, you may want toodeploy hello backup virtual machine for Azure Site Recovery tooa separate resource group and location.</span></span> <span data-ttu-id="0c07a-107">Gestione risorse consente toouse annidati modelli tootarget diversi gruppi di risorse di gruppo di risorse hello usato per il modello padre hello.</span><span class="sxs-lookup"><span data-stu-id="0c07a-107">Resource Manager enables you toouse nested templates tootarget different resource groups than hello resource group used for hello parent template.</span></span>

<span data-ttu-id="0c07a-108">gruppo di risorse Hello è il contenitore del ciclo di vita hello per un'applicazione hello e la relativa raccolta di risorse.</span><span class="sxs-lookup"><span data-stu-id="0c07a-108">hello resource group is hello lifecycle container for hello application and its collection of resources.</span></span> <span data-ttu-id="0c07a-109">Si crea il gruppo di risorse hello di fuori di modello hello e specificare hello risorsa gruppo tootarget durante la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="0c07a-109">You create hello resource group outside of hello template, and specify hello resource group tootarget during deployment.</span></span> <span data-ttu-id="0c07a-110">Per i gruppi di tooresource un'introduzione, vedere [Panoramica di gestione risorse di Azure](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0c07a-110">For an introduction tooresource groups, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>

## <a name="example-template"></a><span data-ttu-id="0c07a-111">Modello di esempio</span><span class="sxs-lookup"><span data-stu-id="0c07a-111">Example template</span></span>

<span data-ttu-id="0c07a-112">tootarget una risorsa diversa, è necessario utilizzare un modello annidato o collegato durante la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="0c07a-112">tootarget a different resource, you must use a nested or linked template during deployment.</span></span> <span data-ttu-id="0c07a-113">Hello `Microsoft.Resources/deployments` fornisce un `resourceGroup` parametro che consente di toospecify un gruppo di risorse diversi per hello annidati di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="0c07a-113">hello `Microsoft.Resources/deployments` resource type provides a `resourceGroup` parameter that enables you toospecify a different resource group for hello nested deployment.</span></span> <span data-ttu-id="0c07a-114">Tutti i gruppi di risorse hello devono esistere prima di eseguire la distribuzione di hello.</span><span class="sxs-lookup"><span data-stu-id="0c07a-114">All hello resource groups must exist before running hello deployment.</span></span> <span data-ttu-id="0c07a-115">esempio Hello distribuisce due account di archiviazione - in gruppo di risorse hello specificato durante la distribuzione e uno in un gruppo di risorse denominato `crossResourceGroupDeployment`:</span><span class="sxs-lookup"><span data-stu-id="0c07a-115">hello following example deploys two storage accounts - one in hello resource group specified during deployment, and one in a resource group named `crossResourceGroupDeployment`:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "StorageAccountName1": {
            "type": "string"
        },
        "StorageAccountName2": {
            "type": "string"
        }
    },
    "variables": {},
    "resources": [
        {
            "apiVersion": "2017-05-10",
            "name": "nestedTemplate",
            "type": "Microsoft.Resources/deployments",
            "resourceGroup": "crossResourceGroupDeployment",
            "properties": {
                "mode": "Incremental",
                "template": {
                    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
                    "contentVersion": "1.0.0.0",
                    "parameters": {},
                    "variables": {},
                    "resources": [
                        {
                            "type": "Microsoft.Storage/storageAccounts",
                            "name": "[parameters('StorageAccountName2')]",
                            "apiVersion": "2015-06-15",
                            "location": "West US",
                            "properties": {
                                "accountType": "Standard_LRS"
                            }
                        }
                    ]
                },
                "parameters": {}
            }
        },
        {
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[parameters('StorageAccountName1')]",
            "apiVersion": "2015-06-15",
            "location": "West US",
            "properties": {
                "accountType": "Standard_LRS"
            }
        }
    ]
}
```

<span data-ttu-id="0c07a-116">Se si imposta `resourceGroup` toohello nome di un gruppo di risorse che non esiste, hello distribuzione non riesce.</span><span class="sxs-lookup"><span data-stu-id="0c07a-116">If you set `resourceGroup` toohello name of a resource group that does not exist, hello deployment fails.</span></span> <span data-ttu-id="0c07a-117">Se non si specifica un valore per `resourceGroup`, Gestione risorse Usa gruppo di risorse padre hello.</span><span class="sxs-lookup"><span data-stu-id="0c07a-117">If you do not provide a value for `resourceGroup`, Resource Manager uses hello parent resource group.</span></span>  

## <a name="deploy-hello-template"></a><span data-ttu-id="0c07a-118">Distribuire il modello di hello</span><span class="sxs-lookup"><span data-stu-id="0c07a-118">Deploy hello template</span></span>

<span data-ttu-id="0c07a-119">modello di esempio hello toodeploy, è possibile utilizzare il portale di hello, Azure PowerShell o CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="0c07a-119">toodeploy hello example template, you can use hello portal, Azure PowerShell, or Azure CLI.</span></span> <span data-ttu-id="0c07a-120">Per Azure PowerShell o l'interfaccia della riga di comando di Azure è necessario usare una versione di maggio 2017 o successiva.</span><span class="sxs-lookup"><span data-stu-id="0c07a-120">For Azure PowerShell or Azure CLI, you must use a release from May 2017 or later.</span></span> <span data-ttu-id="0c07a-121">Negli esempi di Hello si presuppone di aver salvato il modello di hello in locale come un file denominato **crossrgdeployment.json**.</span><span class="sxs-lookup"><span data-stu-id="0c07a-121">hello examples assume you have saved hello template locally as a file named **crossrgdeployment.json**.</span></span>

<span data-ttu-id="0c07a-122">Per PowerShell:</span><span class="sxs-lookup"><span data-stu-id="0c07a-122">For PowerShell:</span></span>

```powershell
Login-AzureRmAccount

New-AzureRmResourceGroup -Name mainResourceGroup -Location "South Central US"
New-AzureRmResourceGroup -Name crossResourceGroupDeployment -Location "Central US"
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName mainResourceGroup `
  -TemplateFile c:\MyTemplates\crossrgdeployment.json
```

<span data-ttu-id="0c07a-123">Per l'interfaccia della riga di comando di Azure:</span><span class="sxs-lookup"><span data-stu-id="0c07a-123">For Azure CLI:</span></span>

```azurecli
az login

az group create --name mainResourceGroup --location "South Central US"
az group create --name crossResourceGroupDeployment --location "Central US"
az group deployment create \
    --name ExampleDeployment \
    --resource-group mainResourceGroup \
    --template-file crossrgdeployment.json
```

<span data-ttu-id="0c07a-124">Al termine della distribuzione, vengono visualizzati due gruppi di risorse.</span><span class="sxs-lookup"><span data-stu-id="0c07a-124">After deployment completes, you see two resource groups.</span></span> <span data-ttu-id="0c07a-125">Ogni gruppo di risorse contiene un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="0c07a-125">Each resource group contains a storage account.</span></span>

## <a name="use-resourcegroup-function"></a><span data-ttu-id="0c07a-126">Usare la funzione resourceGroup()</span><span class="sxs-lookup"><span data-stu-id="0c07a-126">Use resourceGroup() function</span></span>

<span data-ttu-id="0c07a-127">Per attraversare distribuzioni del gruppo di risorse hello [resouceGroup() funzione](resource-group-template-functions-resource.md#resourcegroup) viene risolta in base alle modalità modello nidificato hello utilizzata per specificare.</span><span class="sxs-lookup"><span data-stu-id="0c07a-127">For cross resource group deployments, hello [resouceGroup() function](resource-group-template-functions-resource.md#resourcegroup) resolves differently based on how you specify hello nested template.</span></span> 

<span data-ttu-id="0c07a-128">Se si incorpora un modello all'interno di un altro modello, resouceGroup() nel modello annidato hello risolve toohello gruppo di risorse padre.</span><span class="sxs-lookup"><span data-stu-id="0c07a-128">If you embed one template within another template, resouceGroup() in hello nested template resolves toohello parent resource group.</span></span> <span data-ttu-id="0c07a-129">Un modello incorporato utilizza hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="0c07a-129">An embedded template uses hello following format:</span></span>

```json
"apiVersion": "2017-05-10",
"name": "embeddedTemplate",
"type": "Microsoft.Resources/deployments",
"resourceGroup": "crossResourceGroupDeployment",
"properties": {
    "mode": "Incremental",
    "template": {
        ...
        resourceGroup() refers tooparent resource group
    }
}
```

<span data-ttu-id="0c07a-130">Se si collega modello separato tooa, resouceGroup() nel modello collegato hello risolve il gruppo di risorse annidati di toohello.</span><span class="sxs-lookup"><span data-stu-id="0c07a-130">If you link tooa separate template, resouceGroup() in hello linked template resolves toohello nested resource group.</span></span> <span data-ttu-id="0c07a-131">Un modello collegato utilizza hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="0c07a-131">A linked template uses hello following format:</span></span>

```json
"apiVersion": "2017-05-10",
"name": "linkedTemplate",
"type": "Microsoft.Resources/deployments",
"resourceGroup": "crossResourceGroupDeployment",
"properties": {
    "mode": "Incremental",
    "templateLink": {
        ...
        resourceGroup() in linked template refers toolinked resource group
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="0c07a-132">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0c07a-132">Next steps</span></span>

* <span data-ttu-id="0c07a-133">toounderstand toodefine parametri nel modello, vedere [comprendere hello struttura e la sintassi dei modelli di Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="0c07a-133">toounderstand how toodefine parameters in your template, see [Understand hello structure and syntax of Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="0c07a-134">Per suggerimenti su come risolvere i comuni errori di distribuzione, vedere [Risolvere errori comuni durante la distribuzione di risorse in Azure con Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="0c07a-134">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="0c07a-135">Per informazioni sulla distribuzione di un modello che richiede un token di firma di accesso condiviso, vedere [Distribuire un modello privato con un token di firma di accesso condiviso](resource-manager-powershell-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="0c07a-135">For information about deploying a template that requires a SAS token, see [Deploy private template with SAS token](resource-manager-powershell-sas-token.md).</span></span>
