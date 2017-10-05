---
title: Distribuire un'area di lavoro di Machine Learning con Azure Resource Manager | Documentazione Microsoft
description: Come distribuire un'area di lavoro per Azure Machine Learning usando il modello di Azure Resource Manager
services: machine-learning
documentationcenter: 
author: ahgyger
manager: haining
editor: garye
ms.assetid: 4955ac4d-ff99-4908-aa27-69b6bfcc8e85
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/15/2017
ms.author: ahgyger
ms.openlocfilehash: 9e37780428b0867da63987ec4f7f843a8abeb907
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-machine-learning-workspace-using-azure-resource-manager"></a><span data-ttu-id="0f170-103">Distribuire un'area di lavoro di Machine Learning con Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0f170-103">Deploy Machine Learning Workspace Using Azure Resource Manager</span></span>
## <a name="introduction"></a><span data-ttu-id="0f170-104">Introduzione</span><span class="sxs-lookup"><span data-stu-id="0f170-104">Introduction</span></span>
<span data-ttu-id="0f170-105">L'uso di un modello di distribuzione Azure Resource Manager consente di risparmiare tempo perché è possibile distribuire in modo scalabile i componenti interconnessi con un meccanismo di convalida e di ripetizione dei tentativi.</span><span class="sxs-lookup"><span data-stu-id="0f170-105">Using an Azure Resource Manager deployment template saves you time by giving you a scalable way to deploy interconnected components with a validation and retry mechanism.</span></span> <span data-ttu-id="0f170-106">Per configurare le aree di lavoro di Azure Machine Learning, ad esempio, è necessario configurare prima un account di archiviazione di Azure e quindi distribuire l'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="0f170-106">To set up Azure Machine Learning Workspaces, for example, you need to first configure an Azure storage account and then deploy your workspace.</span></span> <span data-ttu-id="0f170-107">Si immagini di doverlo fare manualmente per centinaia di aree di lavoro.</span><span class="sxs-lookup"><span data-stu-id="0f170-107">Imagine doing this manually for hundreds of workspaces.</span></span> <span data-ttu-id="0f170-108">Un'alternativa più semplice prevede l'uso di un modello di Azure Resource Manager per distribuire un'area di lavoro di Azure Machine Learning e tutte le dipendenze.</span><span class="sxs-lookup"><span data-stu-id="0f170-108">An easier alternative is to use an Azure Resource Manager template to deploy an Azure Machine Learning Workspace and all its dependencies.</span></span> <span data-ttu-id="0f170-109">Questo articolo illustra il processo in dettaglio.</span><span class="sxs-lookup"><span data-stu-id="0f170-109">This article takes you through this process step-by-step.</span></span> <span data-ttu-id="0f170-110">Per una panoramica generale di Azure Resource Manager, vedere [Panoramica di Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0f170-110">For a great overview of Azure Resource Manager, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

## <a name="step-by-step-create-a-machine-learning-workspace"></a><span data-ttu-id="0f170-111">Procedura dettagliata: Creare un'area di lavoro di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="0f170-111">Step-by-step: create a Machine Learning Workspace</span></span>
<span data-ttu-id="0f170-112">Verrà creato un gruppo di risorse di Azure, quindi verranno distribuiti un nuovo account di archiviazione di Azure e una nuova area di lavoro di Azure Machine Learning usando un modello di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="0f170-112">We will create an Azure resource group, then deploy a new Azure storage account and a new Azure Machine Learning Workspace using a Resource Manager template.</span></span> <span data-ttu-id="0f170-113">Una volta completata la distribuzione, verranno visualizzate importanti informazioni sulle aree di lavoro create (la chiave primaria, l'ID area di lavoro e l'URL dell'area di lavoro).</span><span class="sxs-lookup"><span data-stu-id="0f170-113">Once the deployment is complete, we will print out important information about the workspaces that were created (the primary key, the workspaceID, and the URL to the workspace).</span></span>

### <a name="create-an-azure-resource-manager-template"></a><span data-ttu-id="0f170-114">Creare un modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0f170-114">Create an Azure Resource Manager template</span></span>
<span data-ttu-id="0f170-115">Un'area di lavoro di Machine Learning richiede un account di archiviazione di Azure per archiviare il set di dati collegato.</span><span class="sxs-lookup"><span data-stu-id="0f170-115">A Machine Learning Workspace requires an Azure storage account to store the dataset linked to it.</span></span>
<span data-ttu-id="0f170-116">Il modello seguente usa il nome del gruppo di risorse per generare il nome dell'account di archiviazione e il nome dell'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="0f170-116">The following template uses the name of the resource group to generate the storage account name and the workspace name.</span></span>  <span data-ttu-id="0f170-117">Usa anche il nome dell'account di archiviazione come proprietà durante la creazione dell'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="0f170-117">It also uses the storage account name as a property when creating the workspace.</span></span>

```
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "variables": {
        "namePrefix": "[resourceGroup().name]",
        "location": "[resourceGroup().location]",
        "mlVersion": "2016-04-01",
        "stgVersion": "2015-06-15",
        "storageAccountName": "[concat(variables('namePrefix'),'stg')]",
        "mlWorkspaceName": "[concat(variables('namePrefix'),'mlwk')]",
        "mlResourceId": "[resourceId('Microsoft.MachineLearning/workspaces', variables('mlWorkspaceName'))]",
        "stgResourceId": "[resourceId('Microsoft.Storage/storageAccounts', variables('storageAccountName'))]",
        "storageAccountType": "Standard_LRS"
    },
    "resources": [
        {
            "apiVersion": "[variables('stgVersion')]",
            "name": "[variables('storageAccountName')]",
            "type": "Microsoft.Storage/storageAccounts",
            "location": "[variables('location')]",
            "properties": {
                "accountType": "[variables('storageAccountType')]"
            }
        },
        {
            "apiVersion": "[variables('mlVersion')]",
            "type": "Microsoft.MachineLearning/workspaces",
            "name": "[variables('mlWorkspaceName')]",
            "location": "[variables('location')]",
            "dependsOn": ["[variables('stgResourceId')]"],
            "properties": {
                "UserStorageAccountId": "[variables('stgResourceId')]"
            }
        }
    ],
    "outputs": {
        "mlWorkspaceObject": {"type": "object", "value": "[reference(variables('mlResourceId'), variables('mlVersion'))]"},
        "mlWorkspaceToken": {"type": "string", "value": "[listWorkspaceKeys(variables('mlResourceId'), variables('mlVersion')).primaryToken]"},
        "mlWorkspaceWorkspaceID": {"type": "string", "value": "[reference(variables('mlResourceId'), variables('mlVersion')).WorkspaceId]"},
        "mlWorkspaceWorkspaceLink": {"type": "string", "value": "[concat('https://studio.azureml.net/Home/ViewWorkspace/', reference(variables('mlResourceId'), variables('mlVersion')).WorkspaceId)]"}
    }
}

```
<span data-ttu-id="0f170-118">Salvare questo modello come file mlworkspace.json in c:\temp\.</span><span class="sxs-lookup"><span data-stu-id="0f170-118">Save this template as mlworkspace.json file under c:\temp\.</span></span>

### <a name="deploy-the-resource-group-based-on-the-template"></a><span data-ttu-id="0f170-119">Distribuire il gruppo di risorse in base al modello</span><span class="sxs-lookup"><span data-stu-id="0f170-119">Deploy the resource group, based on the template</span></span>
* <span data-ttu-id="0f170-120">Aprire PowerShell</span><span class="sxs-lookup"><span data-stu-id="0f170-120">Open PowerShell</span></span>
* <span data-ttu-id="0f170-121">Installare i moduli per Azure Resource Manager e Azure Service Management</span><span class="sxs-lookup"><span data-stu-id="0f170-121">Install modules for Azure Resource Manager and Azure Service Management</span></span>  

```
# Install the Azure Resource Manager modules from the PowerShell Gallery (press “A”)
Install-Module AzureRM -Scope CurrentUser

# Install the Azure Service Management modules from the PowerShell Gallery (press “A”)
Install-Module Azure -Scope CurrentUser
```

   <span data-ttu-id="0f170-122">Con questi passaggi vengono scaricati e installati i moduli necessari per completare i passaggi rimanenti.</span><span class="sxs-lookup"><span data-stu-id="0f170-122">These steps download and install the modules necessary to complete the remaining steps.</span></span> <span data-ttu-id="0f170-123">È necessario eseguirli una sola volta nell'ambiente in cui si eseguono i comandi di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0f170-123">This only needs to be done once in the environment where you are executing the PowerShell commands.</span></span>   

* <span data-ttu-id="0f170-124">Eseguire l'autenticazione ad Azure</span><span class="sxs-lookup"><span data-stu-id="0f170-124">Authenticate to Azure</span></span>  

```
# Authenticate (enter your credentials in the pop-up window)
Add-AzureRmAccount
```
<span data-ttu-id="0f170-125">Questo passaggio deve essere ripetuto per ogni sessione.</span><span class="sxs-lookup"><span data-stu-id="0f170-125">This step needs to be repeated for each session.</span></span> <span data-ttu-id="0f170-126">Una volta eseguita l'autenticazione, verranno visualizzate le informazioni sulla sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="0f170-126">Once authenticated, your subscription information should be displayed.</span></span>

![Account Azure][1]

<span data-ttu-id="0f170-128">Ora che si ha accesso ad Azure, è possibile creare il gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="0f170-128">Now that we have access to Azure, we can create the resource group.</span></span>

* <span data-ttu-id="0f170-129">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="0f170-129">Create a resource group</span></span>

```
$rg = New-AzureRmResourceGroup -Name "uniquenamerequired523" -Location "South Central US"
$rg
```

<span data-ttu-id="0f170-130">Verificare che il provisioning del gruppo di risorse venga effettuato correttamente.</span><span class="sxs-lookup"><span data-stu-id="0f170-130">Verify that the resource group is correctly provisioned.</span></span> <span data-ttu-id="0f170-131">**ProvisioningState** deve essere "Succeeded".</span><span class="sxs-lookup"><span data-stu-id="0f170-131">**ProvisioningState** should be “Succeeded.”</span></span>
<span data-ttu-id="0f170-132">Il nome del gruppo di risorse viene usato dal modello per generare il nome dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="0f170-132">The resource group name is used by the template to generate the storage account name.</span></span> <span data-ttu-id="0f170-133">Il nome dell'account di archiviazione deve essere di lunghezza compresa tra 3 e 24 caratteri e usare solo numeri e lettere minuscole.</span><span class="sxs-lookup"><span data-stu-id="0f170-133">The storage account name must be between 3 and 24 characters in length and use numbers and lower-case letters only.</span></span>

![Gruppo di risorse][2]

* <span data-ttu-id="0f170-135">Usando la distribuzione del gruppo di risorse, distribuire una nuova area di lavoro di Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="0f170-135">Using the resource group deployment, deploy a new Machine Learning Workspace.</span></span>

```
# Create a Resource Group, TemplateFile is the location of the JSON template.
$rgd = New-AzureRmResourceGroupDeployment -Name "demo" -TemplateFile "C:\temp\mlworkspace.json" -ResourceGroupName $rg.ResourceGroupName
```

<span data-ttu-id="0f170-136">Una volta completata la distribuzione, è semplice accedere alle proprietà dell'area di lavoro distribuita.</span><span class="sxs-lookup"><span data-stu-id="0f170-136">Once the deployment is completed, it is straightforward to access properties of the workspace you deployed.</span></span> <span data-ttu-id="0f170-137">Ad esempio, è possibile accedere al token di chiave primaria.</span><span class="sxs-lookup"><span data-stu-id="0f170-137">For example, you can access the Primary Key Token.</span></span>

```
# Access Azure ML Workspace Token after its deployment.
$rgd.Outputs.mlWorkspaceToken.Value
```

<span data-ttu-id="0f170-138">Un altro modo per recuperare i token dell'area di lavoro esistente consiste nell'utilizzare il comando Invoke-AzureRmResourceAction.</span><span class="sxs-lookup"><span data-stu-id="0f170-138">Another way to retrieve tokens of existing workspace is to use the Invoke-AzureRmResourceAction command.</span></span> <span data-ttu-id="0f170-139">Ad esempio, è possibile elencare i token primari e secondari di tutte le aree di lavoro.</span><span class="sxs-lookup"><span data-stu-id="0f170-139">For example, you can list the primary and secondary tokens of all workspaces.</span></span>

```  
# List the primary and secondary tokens of all workspaces
Get-AzureRmResource |? { $_.ResourceType -Like "*MachineLearning/workspaces*"} |% { Invoke-AzureRmResourceAction -ResourceId $_.ResourceId -Action listworkspacekeys -Force}  
```
<span data-ttu-id="0f170-140">Dopo il provisioning dell'area di lavoro, è anche possibile automatizzare diverse attività di Azure Machine Learning Studio usando il [modulo PowerShell per Azure Machine Learning](http://aka.ms/amlps).</span><span class="sxs-lookup"><span data-stu-id="0f170-140">After the workspace is provisioned, you can also automate many Azure Machine Learning Studio tasks using the [PowerShell Module for Azure Machine Learning](http://aka.ms/amlps).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0f170-141">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0f170-141">Next Steps</span></span>
* <span data-ttu-id="0f170-142">Altre informazioni sulla [Creazione di modelli di Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="0f170-142">Learn more about [authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span> 
* <span data-ttu-id="0f170-143">Vedere il [repository di modelli di avvio rapido di Azure](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="0f170-143">Have a look at the [Azure Quickstart Templates Repository](https://github.com/Azure/azure-quickstart-templates).</span></span> 
* <span data-ttu-id="0f170-144">Guardare questo video su [Azure Resource Manager](https://channel9.msdn.com/Events/Ignite/2015/C9-39).</span><span class="sxs-lookup"><span data-stu-id="0f170-144">Watch this video about [Azure Resource Manager](https://channel9.msdn.com/Events/Ignite/2015/C9-39).</span></span> 

<!--Image references-->
[1]: ../media/machine-learning-deploy-with-resource-manager-template/azuresubscription.png
[2]: ../media/machine-learning-deploy-with-resource-manager-template/resourcegroupprovisioning.png


<!--Link references-->
