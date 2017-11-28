---
title: un'area di lavoro di Machine Learning con Azure Resource Manager aaaDeploy | Documenti Microsoft
description: Come toodeploy un'area di lavoro per Azure Machine Learning che usano il modello di gestione risorse di Azure
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
ms.openlocfilehash: 308959825bcbd670f6ce9b6dc381be767f172357
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-machine-learning-workspace-using-azure-resource-manager"></a><span data-ttu-id="7ddbf-103">Distribuire un'area di lavoro di Machine Learning con Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7ddbf-103">Deploy Machine Learning Workspace Using Azure Resource Manager</span></span>
## <a name="introduction"></a><span data-ttu-id="7ddbf-104">Introduzione</span><span class="sxs-lookup"><span data-stu-id="7ddbf-104">Introduction</span></span>
<span data-ttu-id="7ddbf-105">Utilizzando un gestore delle risorse Azure modello di distribuzione consente di risparmiare tempo fornendo un modo scalabile di toodeploy interconnessi componenti con un meccanismo di convalida e riprovare.</span><span class="sxs-lookup"><span data-stu-id="7ddbf-105">Using an Azure Resource Manager deployment template saves you time by giving you a scalable way toodeploy interconnected components with a validation and retry mechanism.</span></span> <span data-ttu-id="7ddbf-106">tooset le aree di lavoro di Azure Machine Learning, ad esempio, è necessario configurare un account di archiviazione di Azure e quindi distribuire l'area di lavoro di toofirst.</span><span class="sxs-lookup"><span data-stu-id="7ddbf-106">tooset up Azure Machine Learning Workspaces, for example, you need toofirst configure an Azure storage account and then deploy your workspace.</span></span> <span data-ttu-id="7ddbf-107">Si immagini di doverlo fare manualmente per centinaia di aree di lavoro.</span><span class="sxs-lookup"><span data-stu-id="7ddbf-107">Imagine doing this manually for hundreds of workspaces.</span></span> <span data-ttu-id="7ddbf-108">Un'alternativa più semplice è toouse un toodeploy modello di gestione risorse di Azure un'area di lavoro di Azure Machine Learning e tutte le relative dipendenze.</span><span class="sxs-lookup"><span data-stu-id="7ddbf-108">An easier alternative is toouse an Azure Resource Manager template toodeploy an Azure Machine Learning Workspace and all its dependencies.</span></span> <span data-ttu-id="7ddbf-109">Questo articolo illustra il processo in dettaglio.</span><span class="sxs-lookup"><span data-stu-id="7ddbf-109">This article takes you through this process step-by-step.</span></span> <span data-ttu-id="7ddbf-110">Per una panoramica generale di Azure Resource Manager, vedere [Panoramica di Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7ddbf-110">For a great overview of Azure Resource Manager, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

## <a name="step-by-step-create-a-machine-learning-workspace"></a><span data-ttu-id="7ddbf-111">Procedura dettagliata: Creare un'area di lavoro di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="7ddbf-111">Step-by-step: create a Machine Learning Workspace</span></span>
<span data-ttu-id="7ddbf-112">Verrà creato un gruppo di risorse di Azure, quindi verranno distribuiti un nuovo account di archiviazione di Azure e una nuova area di lavoro di Azure Machine Learning usando un modello di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7ddbf-112">We will create an Azure resource group, then deploy a new Azure storage account and a new Azure Machine Learning Workspace using a Resource Manager template.</span></span> <span data-ttu-id="7ddbf-113">Una volta completata la distribuzione di hello, si verrà stampato informazioni importanti sulle aree di lavoro hello creati (chiave primaria hello Idareadilavoro hello e dell'area di lavoro di hello URL toohello).</span><span class="sxs-lookup"><span data-stu-id="7ddbf-113">Once hello deployment is complete, we will print out important information about hello workspaces that were created (hello primary key, hello workspaceID, and hello URL toohello workspace).</span></span>

### <a name="create-an-azure-resource-manager-template"></a><span data-ttu-id="7ddbf-114">Creare un modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7ddbf-114">Create an Azure Resource Manager template</span></span>
<span data-ttu-id="7ddbf-115">Un'area di lavoro di Machine Learning richiede un set di dati collegato tooit di archiviazione di Azure account toostore hello.</span><span class="sxs-lookup"><span data-stu-id="7ddbf-115">A Machine Learning Workspace requires an Azure storage account toostore hello dataset linked tooit.</span></span>
<span data-ttu-id="7ddbf-116">Hello modello seguente utilizza il nome di hello del hello Nome gruppo di risorse toogenerate hello storage account e il nome dell'area di lavoro hello.</span><span class="sxs-lookup"><span data-stu-id="7ddbf-116">hello following template uses hello name of hello resource group toogenerate hello storage account name and hello workspace name.</span></span>  <span data-ttu-id="7ddbf-117">Utilizza inoltre nome account di archiviazione hello come una proprietà durante la creazione dell'area di lavoro di hello.</span><span class="sxs-lookup"><span data-stu-id="7ddbf-117">It also uses hello storage account name as a property when creating hello workspace.</span></span>

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
<span data-ttu-id="7ddbf-118">Salvare questo modello come file mlworkspace.json in c:\temp\.</span><span class="sxs-lookup"><span data-stu-id="7ddbf-118">Save this template as mlworkspace.json file under c:\temp\.</span></span>

### <a name="deploy-hello-resource-group-based-on-hello-template"></a><span data-ttu-id="7ddbf-119">Distribuire il gruppo di risorse hello, basato sul modello hello</span><span class="sxs-lookup"><span data-stu-id="7ddbf-119">Deploy hello resource group, based on hello template</span></span>
* <span data-ttu-id="7ddbf-120">Aprire PowerShell</span><span class="sxs-lookup"><span data-stu-id="7ddbf-120">Open PowerShell</span></span>
* <span data-ttu-id="7ddbf-121">Installare i moduli per Azure Resource Manager e Azure Service Management</span><span class="sxs-lookup"><span data-stu-id="7ddbf-121">Install modules for Azure Resource Manager and Azure Service Management</span></span>  

```
# Install hello Azure Resource Manager modules from hello PowerShell Gallery (press “A”)
Install-Module AzureRM -Scope CurrentUser

# Install hello Azure Service Management modules from hello PowerShell Gallery (press “A”)
Install-Module Azure -Scope CurrentUser
```

   <span data-ttu-id="7ddbf-122">Questi passaggi scaricare e installare i passaggi rimanenti hello hello moduli toocomplete necessarie.</span><span class="sxs-lookup"><span data-stu-id="7ddbf-122">These steps download and install hello modules necessary toocomplete hello remaining steps.</span></span> <span data-ttu-id="7ddbf-123">Questa operazione deve solo toobe eseguito una volta nell'ambiente di hello in cui si siano eseguendo i comandi di PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="7ddbf-123">This only needs toobe done once in hello environment where you are executing hello PowerShell commands.</span></span>   

* <span data-ttu-id="7ddbf-124">L'autenticazione tooAzure</span><span class="sxs-lookup"><span data-stu-id="7ddbf-124">Authenticate tooAzure</span></span>  

```
# Authenticate (enter your credentials in hello pop-up window)
Add-AzureRmAccount
```
<span data-ttu-id="7ddbf-125">Questo passaggio è necessario toobe ripetuto per ogni sessione.</span><span class="sxs-lookup"><span data-stu-id="7ddbf-125">This step needs toobe repeated for each session.</span></span> <span data-ttu-id="7ddbf-126">Una volta eseguita l'autenticazione, verranno visualizzate le informazioni sulla sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="7ddbf-126">Once authenticated, your subscription information should be displayed.</span></span>

![Account Azure][1]

<span data-ttu-id="7ddbf-128">Ora che si dispone di accesso tooAzure, possiamo creare il gruppo di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="7ddbf-128">Now that we have access tooAzure, we can create hello resource group.</span></span>

* <span data-ttu-id="7ddbf-129">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="7ddbf-129">Create a resource group</span></span>

```
$rg = New-AzureRmResourceGroup -Name "uniquenamerequired523" -Location "South Central US"
$rg
```

<span data-ttu-id="7ddbf-130">Verificare che il gruppo di risorse hello viene correttamente eseguito il provisioning.</span><span class="sxs-lookup"><span data-stu-id="7ddbf-130">Verify that hello resource group is correctly provisioned.</span></span> <span data-ttu-id="7ddbf-131">**ProvisioningState** deve essere "Succeeded".</span><span class="sxs-lookup"><span data-stu-id="7ddbf-131">**ProvisioningState** should be “Succeeded.”</span></span>
<span data-ttu-id="7ddbf-132">nome del gruppo di risorse Hello viene utilizzato dal nome account di archiviazione di hello modello toogenerate hello.</span><span class="sxs-lookup"><span data-stu-id="7ddbf-132">hello resource group name is used by hello template toogenerate hello storage account name.</span></span> <span data-ttu-id="7ddbf-133">nome account di archiviazione Hello deve essere di lunghezza compresa tra 3 e 24 caratteri e utilizzare numeri e lettere minuscole solo.</span><span class="sxs-lookup"><span data-stu-id="7ddbf-133">hello storage account name must be between 3 and 24 characters in length and use numbers and lower-case letters only.</span></span>

![Gruppo di risorse][2]

* <span data-ttu-id="7ddbf-135">Mediante la distribuzione di gruppo di risorse hello, distribuire una nuova area di Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="7ddbf-135">Using hello resource group deployment, deploy a new Machine Learning Workspace.</span></span>

```
# Create a Resource Group, TemplateFile is hello location of hello JSON template.
$rgd = New-AzureRmResourceGroupDeployment -Name "demo" -TemplateFile "C:\temp\mlworkspace.json" -ResourceGroupName $rg.ResourceGroupName
```

<span data-ttu-id="7ddbf-136">Al termine della distribuzione di hello, risulta semplice tooaccess proprietà dell'area di lavoro hello che è stato distribuito.</span><span class="sxs-lookup"><span data-stu-id="7ddbf-136">Once hello deployment is completed, it is straightforward tooaccess properties of hello workspace you deployed.</span></span> <span data-ttu-id="7ddbf-137">Ad esempio, è possibile accedere hello Token di chiave primaria.</span><span class="sxs-lookup"><span data-stu-id="7ddbf-137">For example, you can access hello Primary Key Token.</span></span>

```
# Access Azure ML Workspace Token after its deployment.
$rgd.Outputs.mlWorkspaceToken.Value
```

<span data-ttu-id="7ddbf-138">Un altro token di tooretrieve modo dell'area di lavoro esistente è hello toouse comando Invoke-AzureRmResourceAction.</span><span class="sxs-lookup"><span data-stu-id="7ddbf-138">Another way tooretrieve tokens of existing workspace is toouse hello Invoke-AzureRmResourceAction command.</span></span> <span data-ttu-id="7ddbf-139">Ad esempio, è possibile elencare i token primario e secondario hello di tutte le aree di lavoro.</span><span class="sxs-lookup"><span data-stu-id="7ddbf-139">For example, you can list hello primary and secondary tokens of all workspaces.</span></span>

```  
# List hello primary and secondary tokens of all workspaces
Get-AzureRmResource |? { $_.ResourceType -Like "*MachineLearning/workspaces*"} |% { Invoke-AzureRmResourceAction -ResourceId $_.ResourceId -Action listworkspacekeys -Force}  
```
<span data-ttu-id="7ddbf-140">Dopo il provisioning dell'area di lavoro di hello, è inoltre possibile automatizzare molte attività di Azure Machine Learning Studio usando hello [modulo PowerShell per Azure Machine Learning](http://aka.ms/amlps).</span><span class="sxs-lookup"><span data-stu-id="7ddbf-140">After hello workspace is provisioned, you can also automate many Azure Machine Learning Studio tasks using hello [PowerShell Module for Azure Machine Learning](http://aka.ms/amlps).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7ddbf-141">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7ddbf-141">Next Steps</span></span>
* <span data-ttu-id="7ddbf-142">Altre informazioni sulla [Creazione di modelli di Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="7ddbf-142">Learn more about [authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span> 
* <span data-ttu-id="7ddbf-143">Osservare hello [archivio modelli di avvio rapido di Azure](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="7ddbf-143">Have a look at hello [Azure Quickstart Templates Repository](https://github.com/Azure/azure-quickstart-templates).</span></span> 
* <span data-ttu-id="7ddbf-144">Guardare questo video su [Azure Resource Manager](https://channel9.msdn.com/Events/Ignite/2015/C9-39).</span><span class="sxs-lookup"><span data-stu-id="7ddbf-144">Watch this video about [Azure Resource Manager](https://channel9.msdn.com/Events/Ignite/2015/C9-39).</span></span> 

<!--Image references-->
[1]: ../media/machine-learning-deploy-with-resource-manager-template/azuresubscription.png
[2]: ../media/machine-learning-deploy-with-resource-manager-template/resourcegroupprovisioning.png


<!--Link references-->
