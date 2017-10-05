---
title: Esportare un modello di Resource Manager con Azure PowerShell | Documentazione Microsoft
description: Usare Azure Resource Manager e Azure PowerShell per esportare un modello da un gruppo di risorse.
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
ms.openlocfilehash: 7543811eb9448222b6e7c266756e68debc7d54be
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="export-azure-resource-manager-templates-with-powershell"></a><span data-ttu-id="0a352-103">Esportare modelli di Azure Resource Manager con PowerShell</span><span class="sxs-lookup"><span data-stu-id="0a352-103">Export Azure Resource Manager templates with PowerShell</span></span>

<span data-ttu-id="0a352-104">Resource Manager consente di esportare un modello di Resource Manager dalle risorse esistenti nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="0a352-104">Resource Manager enables you to export a Resource Manager template from existing resources in your subscription.</span></span> <span data-ttu-id="0a352-105">Il modello generato può essere usato per ottenere informazioni sulla sintassi del modello o per automatizzare la ridistribuzione della soluzione in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="0a352-105">You can use that generated template to learn about the template syntax or to automate the redeployment of your solution as needed.</span></span>

<span data-ttu-id="0a352-106">È importante notare che è possibile esportare un modello in due modi diversi:</span><span class="sxs-lookup"><span data-stu-id="0a352-106">It is important to note that there are two different ways to export a template:</span></span>

* <span data-ttu-id="0a352-107">È possibile esportare il modello vero e proprio usato per una distribuzione.</span><span class="sxs-lookup"><span data-stu-id="0a352-107">You can export the actual template that you used for a deployment.</span></span> <span data-ttu-id="0a352-108">Il modello esportato include tutti i parametri e le variabili uguali a quelli visualizzati nel modello originale.</span><span class="sxs-lookup"><span data-stu-id="0a352-108">The exported template includes all the parameters and variables exactly as they appeared in the original template.</span></span> <span data-ttu-id="0a352-109">Questo approccio è utile quando si vuole recuperare un modello.</span><span class="sxs-lookup"><span data-stu-id="0a352-109">This approach is helpful when you need to retrieve a template.</span></span>
* <span data-ttu-id="0a352-110">È possibile esportare un modello che rappresenta lo stato attuale del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="0a352-110">You can export a template that represents the current state of the resource group.</span></span> <span data-ttu-id="0a352-111">Il modello esportato non si basa su un modello qualsiasi usato per la distribuzione,</span><span class="sxs-lookup"><span data-stu-id="0a352-111">The exported template is not based on any template that you used for deployment.</span></span> <span data-ttu-id="0a352-112">ma crea un modello che è uno snapshot del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="0a352-112">Instead, it creates a template that is a snapshot of the resource group.</span></span> <span data-ttu-id="0a352-113">Il modello esportato ha diversi valori hardcoded e probabilmente meno parametri di quelli che si definiscono in genere.</span><span class="sxs-lookup"><span data-stu-id="0a352-113">The exported template has many hard-coded values and probably not as many parameters as you would typically define.</span></span> <span data-ttu-id="0a352-114">Questo approccio è utile quando si modifica il gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="0a352-114">This approach is useful when you have modified the resource group.</span></span> <span data-ttu-id="0a352-115">e in seguito è necessario acquisire il gruppo di risorse come modello.</span><span class="sxs-lookup"><span data-stu-id="0a352-115">Now, you need to capture the resource group as a template.</span></span>

<span data-ttu-id="0a352-116">Questo argomento illustra entrambi gli approcci.</span><span class="sxs-lookup"><span data-stu-id="0a352-116">This topic shows both approaches.</span></span>

## <a name="deploy-a-solution"></a><span data-ttu-id="0a352-117">Distribuire una soluzione</span><span class="sxs-lookup"><span data-stu-id="0a352-117">Deploy a solution</span></span>

<span data-ttu-id="0a352-118">Per illustrare entrambi gli approcci per l'esportazione di un modello, si inizia con la distribuzione di una soluzione nella sottoscrizione in uso.</span><span class="sxs-lookup"><span data-stu-id="0a352-118">To illustrate both approaches for exporting a template, let's start by deploying a solution to your subscription.</span></span> <span data-ttu-id="0a352-119">Se si dispone già di un gruppo di risorse nella sottoscrizione che si vuole esportare, non è necessario distribuire la soluzione.</span><span class="sxs-lookup"><span data-stu-id="0a352-119">If you already have a resource group in your subscription that you want to export, you do not have to deploy this solution.</span></span> <span data-ttu-id="0a352-120">Il resto dell'articolo si riferisce tuttavia al modello per questa soluzione.</span><span class="sxs-lookup"><span data-stu-id="0a352-120">However, the remainder of this article refers to the template for this solution.</span></span> <span data-ttu-id="0a352-121">Lo script di esempio distribuisce un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="0a352-121">The example script deploys a storage account.</span></span>

```powershell
New-AzureRmResourceGroup -Name ExampleGroup -Location "South Central US"
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup `
  -DeploymentName NewStorage
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json
```  

## <a name="save-template-from-deployment-history"></a><span data-ttu-id="0a352-122">Salvare il modello dalla cronologia di distribuzione</span><span class="sxs-lookup"><span data-stu-id="0a352-122">Save template from deployment history</span></span>

<span data-ttu-id="0a352-123">È possibile recuperare un modello dalla cronologia della distribuzione usando il comando [Save-AzureRmResourceGroupDeploymentTemplate](/powershell/module/azurerm.resources/save-azurermresourcegroupdeploymenttemplate).</span><span class="sxs-lookup"><span data-stu-id="0a352-123">You can retrieve a template from your deployment history by using the [Save-AzureRmResourceGroupDeploymentTemplate](/powershell/module/azurerm.resources/save-azurermresourcegroupdeploymenttemplate) command.</span></span> <span data-ttu-id="0a352-124">L'esempio seguente illustra come salvare il modello distribuito in precedenza:</span><span class="sxs-lookup"><span data-stu-id="0a352-124">The following example saves the template that you previously deploy:</span></span>

```powershell
Save-AzureRmResourceGroupDeploymentTemplate -ResourceGroupName ExampleGroup -DeploymentName NewStorage
```

<span data-ttu-id="0a352-125">Restituisce il percorso del modello.</span><span class="sxs-lookup"><span data-stu-id="0a352-125">It returns the location of the template.</span></span>

```powershell
Path
----
C:\Users\exampleuser\NewStorage.json
```

<span data-ttu-id="0a352-126">Aprendo il file si nota che si tratta dello stesso modello usato per la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="0a352-126">Open the file, and notice that it is the exact template you used for deployment.</span></span> <span data-ttu-id="0a352-127">I parametri e le variabili corrispondono al modello di GitHub.</span><span class="sxs-lookup"><span data-stu-id="0a352-127">The parameters and variables match the template from GitHub.</span></span> <span data-ttu-id="0a352-128">È possibile ridistribuire il modello.</span><span class="sxs-lookup"><span data-stu-id="0a352-128">You can redeploy this template.</span></span>

## <a name="export-resource-group-as-template"></a><span data-ttu-id="0a352-129">Esportare il gruppo di risorse come modello</span><span class="sxs-lookup"><span data-stu-id="0a352-129">Export resource group as template</span></span>

<span data-ttu-id="0a352-130">Invece di recuperare un modello dalla cronologia di distribuzione, è possibile recuperarne uno che rappresenta lo stato attuale di un gruppo di risorse usando il comando [Export-AzureRmResourceGroup](/powershell/module/azurerm.resources/export-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="0a352-130">Instead of retrieving a template from the deployment history, you can retrieve a template that represents the current state of a resource group by using the [Export-AzureRmResourceGroup](/powershell/module/azurerm.resources/export-azurermresourcegroup) command.</span></span> <span data-ttu-id="0a352-131">Il comando è utile quando sono state apportate numerose modifiche al gruppo di risorse e nessun modello esistente è in grado di rappresentarle tutte.</span><span class="sxs-lookup"><span data-stu-id="0a352-131">You use this command when you have made many changes to your resource group and no existing template represents all the changes.</span></span>

```powershell
Export-AzureRmResourceGroup -ResourceGroupName ExampleGroup
```

<span data-ttu-id="0a352-132">Restituisce il percorso del modello.</span><span class="sxs-lookup"><span data-stu-id="0a352-132">It returns the location of the template.</span></span>

```powershell
Path
----
C:\Users\exampleuser\ExampleGroup.json
```

<span data-ttu-id="0a352-133">Aprendo il file si nota che è diverso rispetto al modello di GitHub.</span><span class="sxs-lookup"><span data-stu-id="0a352-133">Open the file, and notice that it is different than the template in GitHub.</span></span> <span data-ttu-id="0a352-134">Contiene parametri diversi e non include variabili.</span><span class="sxs-lookup"><span data-stu-id="0a352-134">It has different parameters and no variables.</span></span> <span data-ttu-id="0a352-135">I valori dello SKU e della posizione della risorsa di archiviazione sono impostati come hardcoded.</span><span class="sxs-lookup"><span data-stu-id="0a352-135">The storage SKU and location are hard-coded to values.</span></span> <span data-ttu-id="0a352-136">L'esempio seguente mostra il modello esportato, ma il modello in uso presenta un nome di parametro leggermente diverso:</span><span class="sxs-lookup"><span data-stu-id="0a352-136">The following example shows the exported template, but your template has a slightly different parameter name:</span></span>

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

<span data-ttu-id="0a352-137">È possibile ridistribuire questo modello, ma è necessario individuare un nome univoco per l'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="0a352-137">You can redeploy this template, but it requires guessing a unique name for the storage account.</span></span> <span data-ttu-id="0a352-138">Il nome del parametro è leggermente diverso.</span><span class="sxs-lookup"><span data-stu-id="0a352-138">The name of your parameter is slightly different.</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup `
  -TemplateFile C:\Users\exampleuser\ExampleGroup.json `
  -storageAccounts_nf3mvst4nqb36standardsa_name tfnewstorage0501
```

## <a name="customize-exported-template"></a><span data-ttu-id="0a352-139">Personalizzare il modello esportato</span><span class="sxs-lookup"><span data-stu-id="0a352-139">Customize exported template</span></span>

<span data-ttu-id="0a352-140">È possibile modificare questo modello per renderlo più flessibile e facile da usare.</span><span class="sxs-lookup"><span data-stu-id="0a352-140">You can modify this template to make it easier to use and more flexible.</span></span> <span data-ttu-id="0a352-141">Per consentire più posizioni, modificare la proprietà location affinché usi la stessa posizione del gruppo di risorse:</span><span class="sxs-lookup"><span data-stu-id="0a352-141">To allow for more locations, change the location property to use the same location as the resource group:</span></span>

```json
"location": "[resourceGroup().location]",
```

<span data-ttu-id="0a352-142">Per evitare di dover individuare un nome univoco per l'account di archiviazione, rimuovere il parametro per il nome dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="0a352-142">To avoid having to guess a uniques name for storage account, remove the parameter for the storage account name.</span></span> <span data-ttu-id="0a352-143">Aggiungere un parametro per il suffisso del nome di archiviazione e uno SKU di archiviazione:</span><span class="sxs-lookup"><span data-stu-id="0a352-143">Add a parameter for a storage name suffix, and a storage SKU:</span></span>

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

<span data-ttu-id="0a352-144">Aggiungere una variabile che costruisce il nome dell'account di archiviazione con la funzione uniqueString:</span><span class="sxs-lookup"><span data-stu-id="0a352-144">Add a variable that constructs the storage account name with the uniqueString function:</span></span>

```json
"variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]"
  },
```

<span data-ttu-id="0a352-145">Impostare il nome dell'account di archiviazione sulla variabile:</span><span class="sxs-lookup"><span data-stu-id="0a352-145">Set the name of the storage account to the variable:</span></span>

```json
"name": "[variables('storageAccountName')]",
```

<span data-ttu-id="0a352-146">Impostare lo SKU sul parametro:</span><span class="sxs-lookup"><span data-stu-id="0a352-146">Set the SKU to the parameter:</span></span>

```json
"sku": {
    "name": "[parameters('storageAccountType')]",
    "tier": "Standard"
},
```

<span data-ttu-id="0a352-147">Il modello si presenta ora come segue:</span><span class="sxs-lookup"><span data-stu-id="0a352-147">Your template now looks like:</span></span>

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

<span data-ttu-id="0a352-148">Ridistribuire il modello modificato.</span><span class="sxs-lookup"><span data-stu-id="0a352-148">Redeploy the modified template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0a352-149">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0a352-149">Next steps</span></span>
* <span data-ttu-id="0a352-150">Per altre informazioni sull'uso del portale per esportare un modello, vedere [Esportare un modello di Azure Resource Manager da risorse esistenti](resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="0a352-150">For information about using the portal to export a template, see [Export an Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>
* <span data-ttu-id="0a352-151">Per definire i parametri nel modello, vedere [Creazione di modelli](resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="0a352-151">To define parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="0a352-152">Per suggerimenti su come risolvere i comuni errori di distribuzione, vedere [Risolvere errori comuni durante la distribuzione di risorse in Azure con Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="0a352-152">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
