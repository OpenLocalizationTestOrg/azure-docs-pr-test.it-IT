---
title: "Distribuire le risorse di Azure in più gruppi di risorse | Microsoft Docs"
description: "Illustra come specificare come destinazione più gruppi di risorse di Azure durante la distribuzione."
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
ms.openlocfilehash: d8b041213b269775175a810e585103d3c538557f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-azure-resources-to-more-than-one-resource-group"></a><span data-ttu-id="5dfc7-103">Distribuire le risorse di Azure in più gruppi di risorse</span><span class="sxs-lookup"><span data-stu-id="5dfc7-103">Deploy Azure resources to more than one resource group</span></span>

<span data-ttu-id="5dfc7-104">In genere si distribuiscono tutte le risorse del modello in un unico gruppo di risorse,</span><span class="sxs-lookup"><span data-stu-id="5dfc7-104">Typically, you deploy all the resources in your template to a single resource group.</span></span> <span data-ttu-id="5dfc7-105">ma in alcuni scenari può essere preferibile distribuire insieme un set di risorse, inserendole tuttavia in gruppi di risorse diversi.</span><span class="sxs-lookup"><span data-stu-id="5dfc7-105">However, there are scenarios where you want to deploy a set of resources together but place them in different resource groups.</span></span> <span data-ttu-id="5dfc7-106">Potrebbe essere necessario, ad esempio, distribuire la macchina virtuale di backup per Azure Site Recovery in un gruppo di risorse e in una posizione separati.</span><span class="sxs-lookup"><span data-stu-id="5dfc7-106">For example, you may want to deploy the backup virtual machine for Azure Site Recovery to a separate resource group and location.</span></span> <span data-ttu-id="5dfc7-107">Resource Manager consente di usare modelli annidati per specificare come destinazione gruppi di risorse diversi da quello usato per il modello padre.</span><span class="sxs-lookup"><span data-stu-id="5dfc7-107">Resource Manager enables you to use nested templates to target different resource groups than the resource group used for the parent template.</span></span>

<span data-ttu-id="5dfc7-108">Il gruppo di risorse è il contenitore del ciclo di vita per l'applicazione e la raccolta di risorse.</span><span class="sxs-lookup"><span data-stu-id="5dfc7-108">The resource group is the lifecycle container for the application and its collection of resources.</span></span> <span data-ttu-id="5dfc7-109">Si crea il gruppo di risorse al di fuori del modello e si specifica il gruppo di risorse da usare come destinazione durante la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="5dfc7-109">You create the resource group outside of the template, and specify the resource group to target during deployment.</span></span> <span data-ttu-id="5dfc7-110">Per un'introduzione ai gruppi di risorse, vedere [Panoramica di Azure Resource Manager](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5dfc7-110">For an introduction to resource groups, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>

## <a name="example-template"></a><span data-ttu-id="5dfc7-111">Modello di esempio</span><span class="sxs-lookup"><span data-stu-id="5dfc7-111">Example template</span></span>

<span data-ttu-id="5dfc7-112">Per specificare come destinazione una risorsa diversa, è necessario usare un modello annidato o collegato durante la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="5dfc7-112">To target a different resource, you must use a nested or linked template during deployment.</span></span> <span data-ttu-id="5dfc7-113">Il tipo di risorsa `Microsoft.Resources/deployments` fornisce un parametro `resourceGroup` che consente di specificare un gruppo di risorse diverso per la distribuzione annidata.</span><span class="sxs-lookup"><span data-stu-id="5dfc7-113">The `Microsoft.Resources/deployments` resource type provides a `resourceGroup` parameter that enables you to specify a different resource group for the nested deployment.</span></span> <span data-ttu-id="5dfc7-114">Tutti i gruppi di risorse devono esistere prima di eseguire la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="5dfc7-114">All the resource groups must exist before running the deployment.</span></span> <span data-ttu-id="5dfc7-115">L'esempio seguente distribuisce due account di archiviazione, uno nel gruppo di risorse specificato durante la distribuzione e uno in un gruppo di risorse denominato `crossResourceGroupDeployment`:</span><span class="sxs-lookup"><span data-stu-id="5dfc7-115">The following example deploys two storage accounts - one in the resource group specified during deployment, and one in a resource group named `crossResourceGroupDeployment`:</span></span>

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

<span data-ttu-id="5dfc7-116">Se si imposta `resourceGroup` sul nome di un gruppo di risorse che non esiste, la distribuzione ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="5dfc7-116">If you set `resourceGroup` to the name of a resource group that does not exist, the deployment fails.</span></span> <span data-ttu-id="5dfc7-117">Se non si specifica un valore per `resourceGroup`, Resource Manager usa il gruppo di risorse padre.</span><span class="sxs-lookup"><span data-stu-id="5dfc7-117">If you do not provide a value for `resourceGroup`, Resource Manager uses the parent resource group.</span></span>  

## <a name="deploy-the-template"></a><span data-ttu-id="5dfc7-118">Distribuire il modello</span><span class="sxs-lookup"><span data-stu-id="5dfc7-118">Deploy the template</span></span>

<span data-ttu-id="5dfc7-119">Per distribuire il modello di esempio, è possibile usare il portale, Azure PowerShell o l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="5dfc7-119">To deploy the example template, you can use the portal, Azure PowerShell, or Azure CLI.</span></span> <span data-ttu-id="5dfc7-120">Per Azure PowerShell o l'interfaccia della riga di comando di Azure è necessario usare una versione di maggio 2017 o successiva.</span><span class="sxs-lookup"><span data-stu-id="5dfc7-120">For Azure PowerShell or Azure CLI, you must use a release from May 2017 or later.</span></span> <span data-ttu-id="5dfc7-121">Gli esempi presuppongono che l'utente abbia salvato il modello in locale come file denominato **crossrgdeployment.json**.</span><span class="sxs-lookup"><span data-stu-id="5dfc7-121">The examples assume you have saved the template locally as a file named **crossrgdeployment.json**.</span></span>

<span data-ttu-id="5dfc7-122">Per PowerShell:</span><span class="sxs-lookup"><span data-stu-id="5dfc7-122">For PowerShell:</span></span>

```powershell
Login-AzureRmAccount

New-AzureRmResourceGroup -Name mainResourceGroup -Location "South Central US"
New-AzureRmResourceGroup -Name crossResourceGroupDeployment -Location "Central US"
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName mainResourceGroup `
  -TemplateFile c:\MyTemplates\crossrgdeployment.json
```

<span data-ttu-id="5dfc7-123">Per l'interfaccia della riga di comando di Azure:</span><span class="sxs-lookup"><span data-stu-id="5dfc7-123">For Azure CLI:</span></span>

```azurecli
az login

az group create --name mainResourceGroup --location "South Central US"
az group create --name crossResourceGroupDeployment --location "Central US"
az group deployment create \
    --name ExampleDeployment \
    --resource-group mainResourceGroup \
    --template-file crossrgdeployment.json
```

<span data-ttu-id="5dfc7-124">Al termine della distribuzione, vengono visualizzati due gruppi di risorse.</span><span class="sxs-lookup"><span data-stu-id="5dfc7-124">After deployment completes, you see two resource groups.</span></span> <span data-ttu-id="5dfc7-125">Ogni gruppo di risorse contiene un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="5dfc7-125">Each resource group contains a storage account.</span></span>

## <a name="use-resourcegroup-function"></a><span data-ttu-id="5dfc7-126">Usare la funzione resourceGroup()</span><span class="sxs-lookup"><span data-stu-id="5dfc7-126">Use resourceGroup() function</span></span>

<span data-ttu-id="5dfc7-127">Per le distribuzioni tra gruppi di risorse, la [funzione resouceGroup()](resource-group-template-functions-resource.md#resourcegroup) viene risolta in modo diverso in base al modo in cui si specifica il modello annidato.</span><span class="sxs-lookup"><span data-stu-id="5dfc7-127">For cross resource group deployments, the [resouceGroup() function](resource-group-template-functions-resource.md#resourcegroup) resolves differently based on how you specify the nested template.</span></span> 

<span data-ttu-id="5dfc7-128">Se si incorpora un modello in un altro modello, la funzione resouceGroup() nel modello annidato si risolve nel gruppo di risorse padre.</span><span class="sxs-lookup"><span data-stu-id="5dfc7-128">If you embed one template within another template, resouceGroup() in the nested template resolves to the parent resource group.</span></span> <span data-ttu-id="5dfc7-129">Un modello incorporato usa il formato seguente:</span><span class="sxs-lookup"><span data-stu-id="5dfc7-129">An embedded template uses the following format:</span></span>

```json
"apiVersion": "2017-05-10",
"name": "embeddedTemplate",
"type": "Microsoft.Resources/deployments",
"resourceGroup": "crossResourceGroupDeployment",
"properties": {
    "mode": "Incremental",
    "template": {
        ...
        resourceGroup() refers to parent resource group
    }
}
```

<span data-ttu-id="5dfc7-130">Se si crea un collegamento a un modello separato, la funzione resouceGroup() nel modello collegato si risolve nel gruppo di risorse annidato.</span><span class="sxs-lookup"><span data-stu-id="5dfc7-130">If you link to a separate template, resouceGroup() in the linked template resolves to the nested resource group.</span></span> <span data-ttu-id="5dfc7-131">Un modello collegato usa il formato seguente:</span><span class="sxs-lookup"><span data-stu-id="5dfc7-131">A linked template uses the following format:</span></span>

```json
"apiVersion": "2017-05-10",
"name": "linkedTemplate",
"type": "Microsoft.Resources/deployments",
"resourceGroup": "crossResourceGroupDeployment",
"properties": {
    "mode": "Incremental",
    "templateLink": {
        ...
        resourceGroup() in linked template refers to linked resource group
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="5dfc7-132">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5dfc7-132">Next steps</span></span>

* <span data-ttu-id="5dfc7-133">Per informazioni su come definire i parametri nel modello, vedere [Comprendere la struttura e la sintassi dei modelli di Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="5dfc7-133">To understand how to define parameters in your template, see [Understand the structure and syntax of Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="5dfc7-134">Per suggerimenti su come risolvere i comuni errori di distribuzione, vedere [Risolvere errori comuni durante la distribuzione di risorse in Azure con Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="5dfc7-134">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="5dfc7-135">Per informazioni sulla distribuzione di un modello che richiede un token di firma di accesso condiviso, vedere [Distribuire un modello privato con un token di firma di accesso condiviso](resource-manager-powershell-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="5dfc7-135">For information about deploying a template that requires a SAS token, see [Deploy private template with SAS token](resource-manager-powershell-sas-token.md).</span></span>
