---
title: modello di gestione risorse aaaExport con Azure PowerShell | Documenti Microsoft
description: Utilizzare Gestione risorse di Azure e Azure PowerShell tooexport un modello da un gruppo di risorse.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/01/2017
ms.author: tomfitz
ms.openlocfilehash: 9a239b7bce8209326c0e267a4d3d69f7014bdaed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="export-azure-resource-manager-templates-with-powershell"></a><span data-ttu-id="1fecd-103">Esportare modelli di Azure Resource Manager con PowerShell</span><span class="sxs-lookup"><span data-stu-id="1fecd-103">Export Azure Resource Manager templates with PowerShell</span></span>

<span data-ttu-id="1fecd-104">Gestione risorse consente tooexport un modello di gestione risorse da risorse esistenti nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="1fecd-104">Resource Manager enables you tooexport a Resource Manager template from existing resources in your subscription.</span></span> <span data-ttu-id="1fecd-105">È possibile utilizzare tale toolearn modello generato su hello modello tooautomate o la sintassi di hello ridistribuzione della soluzione in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="1fecd-105">You can use that generated template toolearn about hello template syntax or tooautomate hello redeployment of your solution as needed.</span></span>

<span data-ttu-id="1fecd-106">È importante toonote che non esistono due modi diversi tooexport un modello:</span><span class="sxs-lookup"><span data-stu-id="1fecd-106">It is important toonote that there are two different ways tooexport a template:</span></span>

* <span data-ttu-id="1fecd-107">È possibile esportare modello hello effettivo utilizzato per una distribuzione.</span><span class="sxs-lookup"><span data-stu-id="1fecd-107">You can export hello actual template that you used for a deployment.</span></span> <span data-ttu-id="1fecd-108">modello esportato Hello include tutti i parametri di hello e variabili, esattamente come appaiono nel modello originale hello.</span><span class="sxs-lookup"><span data-stu-id="1fecd-108">hello exported template includes all hello parameters and variables exactly as they appeared in hello original template.</span></span> <span data-ttu-id="1fecd-109">Questo approccio è utile quando è necessario tooretrieve un modello.</span><span class="sxs-lookup"><span data-stu-id="1fecd-109">This approach is helpful when you need tooretrieve a template.</span></span>
* <span data-ttu-id="1fecd-110">È possibile esportare un modello che rappresenta lo stato corrente di hello hello del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="1fecd-110">You can export a template that represents hello current state of hello resource group.</span></span> <span data-ttu-id="1fecd-111">modello esportato Hello non è basato su qualsiasi modello utilizzato per la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="1fecd-111">hello exported template is not based on any template that you used for deployment.</span></span> <span data-ttu-id="1fecd-112">Al contrario, viene creato un modello che è uno snapshot hello del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="1fecd-112">Instead, it creates a template that is a snapshot of hello resource group.</span></span> <span data-ttu-id="1fecd-113">modello esportato Hello molti valori hardcoded e probabilmente non tutti i parametri in genere è possibile definire.</span><span class="sxs-lookup"><span data-stu-id="1fecd-113">hello exported template has many hard-coded values and probably not as many parameters as you would typically define.</span></span> <span data-ttu-id="1fecd-114">Questo approccio è utile quando è stato modificato il gruppo di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="1fecd-114">This approach is useful when you have modified hello resource group.</span></span> <span data-ttu-id="1fecd-115">A questo punto, è necessario gruppo di risorse hello toocapture come modello.</span><span class="sxs-lookup"><span data-stu-id="1fecd-115">Now, you need toocapture hello resource group as a template.</span></span>

<span data-ttu-id="1fecd-116">Questo argomento illustra entrambi gli approcci.</span><span class="sxs-lookup"><span data-stu-id="1fecd-116">This topic shows both approaches.</span></span>

## <a name="deploy-a-solution"></a><span data-ttu-id="1fecd-117">Distribuire una soluzione</span><span class="sxs-lookup"><span data-stu-id="1fecd-117">Deploy a solution</span></span>

<span data-ttu-id="1fecd-118">Per iniziare la distribuzione di una sottoscrizione di tooyour soluzione tooillustrate entrambi approcci per l'esportazione di un modello.</span><span class="sxs-lookup"><span data-stu-id="1fecd-118">tooillustrate both approaches for exporting a template, let's start by deploying a solution tooyour subscription.</span></span> <span data-ttu-id="1fecd-119">Se si dispone già di un gruppo di risorse nella sottoscrizione che si desidera tooexport, non si dispone toodeploy questa soluzione.</span><span class="sxs-lookup"><span data-stu-id="1fecd-119">If you already have a resource group in your subscription that you want tooexport, you do not have toodeploy this solution.</span></span> <span data-ttu-id="1fecd-120">Tuttavia, il resto di hello di questo articolo si riferisce toohello modello per questa soluzione.</span><span class="sxs-lookup"><span data-stu-id="1fecd-120">However, hello remainder of this article refers toohello template for this solution.</span></span> <span data-ttu-id="1fecd-121">lo script di esempio Hello distribuisce un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="1fecd-121">hello example script deploys a storage account.</span></span>

```powershell
New-AzureRmResourceGroup -Name ExampleGroup -Location "South Central US"
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup `
  -DeploymentName NewStorage
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json
```  

## <a name="save-template-from-deployment-history"></a><span data-ttu-id="1fecd-122">Salvare un modello dalla cronologia di distribuzione</span><span class="sxs-lookup"><span data-stu-id="1fecd-122">Save template from deployment history</span></span>

<span data-ttu-id="1fecd-123">È possibile recuperare un modello dalla cronologia distribuzione tramite hello [Salva AzureRmResourceGroupDeploymentTemplate](/powershell/module/azurerm.resources/save-azurermresourcegroupdeploymenttemplate) comando.</span><span class="sxs-lookup"><span data-stu-id="1fecd-123">You can retrieve a template from your deployment history by using hello [Save-AzureRmResourceGroupDeploymentTemplate](/powershell/module/azurerm.resources/save-azurermresourcegroupdeploymenttemplate) command.</span></span> <span data-ttu-id="1fecd-124">Hello dopo esempio Salva hello template che si distribuisce in precedenza:</span><span class="sxs-lookup"><span data-stu-id="1fecd-124">hello following example saves hello template that you previously deploy:</span></span>

```powershell
Save-AzureRmResourceGroupDeploymentTemplate -ResourceGroupName ExampleGroup -DeploymentName NewStorage
```

<span data-ttu-id="1fecd-125">Restituisce il percorso di hello del modello di hello.</span><span class="sxs-lookup"><span data-stu-id="1fecd-125">It returns hello location of hello template.</span></span>

```powershell
Path
----
C:\Users\exampleuser\NewStorage.json
```

<span data-ttu-id="1fecd-126">Aprire il file hello e si noti che modello di esatta hello che è utilizzato per la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="1fecd-126">Open hello file, and notice that it is hello exact template you used for deployment.</span></span> <span data-ttu-id="1fecd-127">variabili e parametri hello corrispondano il modello di hello da GitHub.</span><span class="sxs-lookup"><span data-stu-id="1fecd-127">hello parameters and variables match hello template from GitHub.</span></span> <span data-ttu-id="1fecd-128">È possibile ridistribuire il modello.</span><span class="sxs-lookup"><span data-stu-id="1fecd-128">You can redeploy this template.</span></span>

## <a name="export-resource-group-as-template"></a><span data-ttu-id="1fecd-129">Esportare un gruppo di risorse come modello</span><span class="sxs-lookup"><span data-stu-id="1fecd-129">Export resource group as template</span></span>

<span data-ttu-id="1fecd-130">Invece di recuperare un modello dalla cronologia della distribuzione di hello, è possibile recuperare un modello che rappresenta lo stato corrente di hello di un gruppo di risorse utilizzando hello [esportazione AzureRmResourceGroup](/powershell/module/azurerm.resources/export-azurermresourcegroup) comando.</span><span class="sxs-lookup"><span data-stu-id="1fecd-130">Instead of retrieving a template from hello deployment history, you can retrieve a template that represents hello current state of a resource group by using hello [Export-AzureRmResourceGroup](/powershell/module/azurerm.resources/export-azurermresourcegroup) command.</span></span> <span data-ttu-id="1fecd-131">Utilizzare questo comando quando sono state apportate molte gruppo di risorse tooyour modifiche e nessun modello esistente rappresenta tutte le modifiche di hello.</span><span class="sxs-lookup"><span data-stu-id="1fecd-131">You use this command when you have made many changes tooyour resource group and no existing template represents all hello changes.</span></span>

```powershell
Export-AzureRmResourceGroup -ResourceGroupName ExampleGroup
```

<span data-ttu-id="1fecd-132">Restituisce il percorso di hello del modello di hello.</span><span class="sxs-lookup"><span data-stu-id="1fecd-132">It returns hello location of hello template.</span></span>

```powershell
Path
----
C:\Users\exampleuser\ExampleGroup.json
```

<span data-ttu-id="1fecd-133">Aprire il file hello e si noti che è diverso dal modello hello in GitHub.</span><span class="sxs-lookup"><span data-stu-id="1fecd-133">Open hello file, and notice that it is different than hello template in GitHub.</span></span> <span data-ttu-id="1fecd-134">Contiene parametri diversi e non include variabili.</span><span class="sxs-lookup"><span data-stu-id="1fecd-134">It has different parameters and no variables.</span></span> <span data-ttu-id="1fecd-135">archiviazione Hello SKU e la posizione sono hardcoded toovalues.</span><span class="sxs-lookup"><span data-stu-id="1fecd-135">hello storage SKU and location are hard-coded toovalues.</span></span> <span data-ttu-id="1fecd-136">Hello esempio seguente viene illustrato il modello esportato di hello, ma per il modello è un nome di parametro leggermente diverso:</span><span class="sxs-lookup"><span data-stu-id="1fecd-136">hello following example shows hello exported template, but your template has a slightly different parameter name:</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageAccounts_nf3mvst4nqb36standardsa_name": {
      "defaultValue": null,
      "type": "String"
    }
  },
  "variables": {},
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "sku": {
        "name": "Standard_LRS",
        "tier": "Standard"
      },
      "kind": "Storage",
      "name": "[parameters('storageAccounts_nf3mvst4nqb36standardsa_name')]",
      "apiVersion": "2016-01-01",
      "location": "southcentralus",
      "tags": {},
      "properties": {},
      "dependsOn": []
    }
  ]
}
```

<span data-ttu-id="1fecd-137">È possibile ridistribuire il modello, ma richiede l'individuazione di un nome univoco per l'account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="1fecd-137">You can redeploy this template, but it requires guessing a unique name for hello storage account.</span></span> <span data-ttu-id="1fecd-138">nome Hello del parametro è leggermente diversa.</span><span class="sxs-lookup"><span data-stu-id="1fecd-138">hello name of your parameter is slightly different.</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup `
  -TemplateFile C:\Users\exampleuser\ExampleGroup.json `
  -storageAccounts_nf3mvst4nqb36standardsa_name tfnewstorage0501
```

## <a name="customize-exported-template"></a><span data-ttu-id="1fecd-139">Personalizzare il modello esportato</span><span class="sxs-lookup"><span data-stu-id="1fecd-139">Customize exported template</span></span>

<span data-ttu-id="1fecd-140">È possibile modificare questo modello toomake è toouse più semplice e più flessibile.</span><span class="sxs-lookup"><span data-stu-id="1fecd-140">You can modify this template toomake it easier toouse and more flexible.</span></span> <span data-ttu-id="1fecd-141">tooallow per più percorsi, modifica hello percorso proprietà toouse hello stesso percorso del gruppo di risorse hello:</span><span class="sxs-lookup"><span data-stu-id="1fecd-141">tooallow for more locations, change hello location property toouse hello same location as hello resource group:</span></span>

```json
"location": "[resourceGroup().location]",
```

<span data-ttu-id="1fecd-142">tooavoid con tooguess nome univoche per l'account di archiviazione, il parametro hello remove per il nome di account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="1fecd-142">tooavoid having tooguess a uniques name for storage account, remove hello parameter for hello storage account name.</span></span> <span data-ttu-id="1fecd-143">Aggiungere un parametro per il suffisso del nome di archiviazione e uno SKU di archiviazione:</span><span class="sxs-lookup"><span data-stu-id="1fecd-143">Add a parameter for a storage name suffix, and a storage SKU:</span></span>

```json
"parameters": {
    "storageSuffix": {
      "type": "string",
      "defaultValue": "standardsa"
    },
    "storageAccountType": {
      "defaultValue": "Standard_LRS",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS",
        "Standard_ZRS"
      ],
      "type": "string",
      "metadata": {
        "description": "Storage Account type"
      }
    }
},
```

<span data-ttu-id="1fecd-144">Aggiungere una variabile che costruisce nome account di archiviazione hello con funzione uniqueString hello:</span><span class="sxs-lookup"><span data-stu-id="1fecd-144">Add a variable that constructs hello storage account name with hello uniqueString function:</span></span>

```json
"variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]"
  },
```

<span data-ttu-id="1fecd-145">Impostare il nome di hello della variabile toohello account di archiviazione hello:</span><span class="sxs-lookup"><span data-stu-id="1fecd-145">Set hello name of hello storage account toohello variable:</span></span>

```json
"name": "[variables('storageAccountName')]",
```

<span data-ttu-id="1fecd-146">Impostare hello SKU toohello parametro:</span><span class="sxs-lookup"><span data-stu-id="1fecd-146">Set hello SKU toohello parameter:</span></span>

```json
"sku": {
    "name": "[parameters('storageAccountType')]",
    "tier": "Standard"
},
```

<span data-ttu-id="1fecd-147">Il modello si presenta ora come segue:</span><span class="sxs-lookup"><span data-stu-id="1fecd-147">Your template now looks like:</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageSuffix": {
      "type": "string",
      "defaultValue": "standardsa"
    },
    "storageAccountType": {
      "defaultValue": "Standard_LRS",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS",
        "Standard_ZRS"
      ],
      "type": "string",
      "metadata": {
        "description": "Storage Account type"
      }
    }
  },
  "variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), parameters('storageSuffix'))]"
  },
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "sku": {
        "name": "[parameters('storageAccountType')]",
        "tier": "Standard"
      },
      "kind": "Storage",
      "name": "[variables('storageAccountName')]",
      "apiVersion": "2016-01-01",
      "location": "[resourceGroup().location]",
      "tags": {},
      "properties": {},
      "dependsOn": []
    }
  ]
}
```

<span data-ttu-id="1fecd-148">Ridistribuire modello modificato hello.</span><span class="sxs-lookup"><span data-stu-id="1fecd-148">Redeploy hello modified template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1fecd-149">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1fecd-149">Next steps</span></span>
* <span data-ttu-id="1fecd-150">Per informazioni sull'utilizzo di hello portale tooexport un modello, vedere [esportare un modello di gestione risorse di Azure da risorse esistenti](resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="1fecd-150">For information about using hello portal tooexport a template, see [Export an Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>
* <span data-ttu-id="1fecd-151">toodefine i parametri di modello, vedere [creazione di modelli](resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="1fecd-151">toodefine parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="1fecd-152">Per suggerimenti su come risolvere i comuni errori di distribuzione, vedere [Risolvere errori comuni durante la distribuzione di risorse in Azure con Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="1fecd-152">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
