---
title: aaaDeploy un modello di gestione risorse di Azure in un runbook di automazione di Azure | Documenti Microsoft
description: Come toodeploy un modello di Azure Resource Manager archiviati in archiviazione di Azure da un runbook
services: automation
documentationcenter: dev-center-name
author: eslesar
manager: carmonm
keywords: powershell, runbook, json, automazione di azure
ms.service: automation
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: TBD
ms.date: 07/09/2017
ms.author: eslesar
ms.openlocfilehash: f489a8e8635a48f5a6a2f1a88e1c803f56f01832
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-azure-resource-manager-template-in-an-azure-automation-powershell-runbook"></a><span data-ttu-id="2d728-104">Distribuire un modello di Azure Resource Manager in un runbook PowerShell di Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="2d728-104">Deploy an Azure Resource Manager template in an Azure Automation PowerShell runbook</span></span>

<span data-ttu-id="2d728-105">È possibile scrivere un [runbook PowerShell di Automazione di Azure](automation-first-runbook-textual-powershell.md) che distribuisce una risorsa di Azure usando un [modello di Azure Resource Management](../azure-resource-manager/resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="2d728-105">You can write an [Azure Automation PowerShell runbook](automation-first-runbook-textual-powershell.md) that deploys an Azure resource by using an [Azure Resource Management template](../azure-resource-manager/resource-manager-create-first-template.md).</span></span>

<span data-ttu-id="2d728-106">Con questa operazione è possibile automatizzare la distribuzione delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="2d728-106">By doing this, you can automate deployment of Azure resources.</span></span> <span data-ttu-id="2d728-107">È possibile anche gestire i modelli di Resource Manager in una posizione centrale protetta come Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="2d728-107">You can maintain your Resource Manager templates in a central,secure location such as Azure Storage.</span></span>

<span data-ttu-id="2d728-108">In questo argomento, si crea un runbook di PowerShell che utilizza un modello di gestione risorse archiviato in [di archiviazione di Azure](../storage/common/storage-introduction.md) toodeploy un nuovo account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="2d728-108">In this topic, we create a PowerShell runbook that uses an Resource Manager template stored in [Azure Storage](../storage/common/storage-introduction.md) toodeploy a new Azure Storage account.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2d728-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="2d728-109">Prerequisites</span></span>

<span data-ttu-id="2d728-110">toocomplete questa esercitazione, è necessario hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="2d728-110">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="2d728-111">Sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="2d728-111">Azure subscription.</span></span> <span data-ttu-id="2d728-112">Se non si ha ancora una sottoscrizione, è possibile [attivare i vantaggi della sottoscrizione MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) oppure <a href="/pricing/free-account/" target="_blank">[iscriversi per ottenere un account gratuito](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="2d728-112">If you don't have one yet, you can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or <a href="/pricing/free-account/" target="_blank">[sign up for a free account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="2d728-113">[Account di automazione](automation-sec-configure-azure-runas-account.md) toohold hello runbook ed eseguire l'autenticazione tooAzure risorse.</span><span class="sxs-lookup"><span data-stu-id="2d728-113">[Automation account](automation-sec-configure-azure-runas-account.md) toohold hello runbook and authenticate tooAzure resources.</span></span>  <span data-ttu-id="2d728-114">Questo account deve disporre dell'autorizzazione toostart e arrestare la macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="2d728-114">This account must have permission toostart and stop hello virtual machine.</span></span>
* <span data-ttu-id="2d728-115">[Account di archiviazione Azure](../storage/common/storage-create-storage-account.md) in quale modello di gestione risorse di hello toostore</span><span class="sxs-lookup"><span data-stu-id="2d728-115">[Azure Storage account](../storage/common/storage-create-storage-account.md) in which toostore hello Resource Manager template</span></span>
* <span data-ttu-id="2d728-116">Azure Powershell installato in un computer locale.</span><span class="sxs-lookup"><span data-stu-id="2d728-116">Azure Powershell installed on a local machine.</span></span> <span data-ttu-id="2d728-117">Vedere [installare e configurare Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) per informazioni su come tooget Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2d728-117">See [Install and configure Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) for information about how tooget Azure PowerShell.</span></span>

## <a name="create-hello-resource-manager-template"></a><span data-ttu-id="2d728-118">Creare il modello di gestione risorse di hello</span><span class="sxs-lookup"><span data-stu-id="2d728-118">Create hello Resource Manager template</span></span>

<span data-ttu-id="2d728-119">In questo esempio si userà un modello di Resource Manager che distribuisce un nuovo account di Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="2d728-119">For this example, we use an Resource Manager template that deploys a new Azure Storage account.</span></span>

<span data-ttu-id="2d728-120">In un editor di testo copiare hello seguente testo:</span><span class="sxs-lookup"><span data-stu-id="2d728-120">In a text editor, copy hello following text:</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageAccountType": {
      "type": "string",
      "defaultValue": "Standard_LRS",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS",
        "Standard_ZRS",
        "Premium_LRS"
      ],
      "metadata": {
        "description": "Storage Account type"
      }
    }
  },
  "variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]"
  },
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[variables('storageAccountName')]",
      "apiVersion": "2016-01-01",
      "location": "[resourceGroup().location]",
      "sku": {
          "name": "[parameters('storageAccountType')]"
      },
      "kind": "Storage", 
      "properties": {
      }
    }
  ],
  "outputs": {
      "storageAccountName": {
          "type": "string",
          "value": "[variables('storageAccountName')]"
      }
  }
}
```

<span data-ttu-id="2d728-121">Salvare file hello localmente come `TemplateTest.json`.</span><span class="sxs-lookup"><span data-stu-id="2d728-121">Save hello file locally as `TemplateTest.json`.</span></span>

## <a name="save-hello-resource-manager-template-in-azure-storage"></a><span data-ttu-id="2d728-122">Salvare il modello di gestione risorse di hello in archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="2d728-122">Save hello Resource Manager template in Azure Storage</span></span>

<span data-ttu-id="2d728-123">Ora è utilizzare PowerShell toocreate una condivisione di file di archiviazione di Azure e caricare hello `TemplateTest.json` file.</span><span class="sxs-lookup"><span data-stu-id="2d728-123">Now we use PowerShell toocreate an Azure Storage file share and upload hello `TemplateTest.json` file.</span></span>
<span data-ttu-id="2d728-124">Per istruzioni sulla modalità di condivisione e di caricare un file nel portale di Azure hello toocreate un file, vedere [Introduzione all'archiviazione di File di Azure in Windows](../storage/files/storage-dotnet-how-to-use-files.md).</span><span class="sxs-lookup"><span data-stu-id="2d728-124">For instructions on how toocreate a file share and upload a file in hello Azure portal, see [Get started with Azure File storage on Windows](../storage/files/storage-dotnet-how-to-use-files.md).</span></span>

<span data-ttu-id="2d728-125">Avviare PowerShell nel computer locale, eseguire i seguenti comandi toocreate una condivisione file hello e caricare la condivisione file hello Gestione risorse modello toothat.</span><span class="sxs-lookup"><span data-stu-id="2d728-125">Launch PowerShell on your local machine, and run hello following commands toocreate a file share and upload hello Resource Manager template toothat file share.</span></span>

```powershell
# Login tooAzure
Login-AzureRmAccount

# Get hello access key for your storage account
$key = Get-AzureRmStorageAccountKey -ResourceGroupName 'MyAzureAccount' -Name 'MyStorageAccount'

# Create an Azure Storage context using hello first access key
$context = New-AzureStorageContext -StorageAccountName 'MyStorageAccount' -StorageAccountKey $key[0].value

# Create a file share named 'resource-templates' in your Azure Storage account
$fileShare = New-AzureStorageShare -Name 'resource-templates' -Context $context

# Add hello TemplateTest.json file toohello new file share
# "TemplatePath" is hello path where you saved hello TemplateTest.json file
$templateFile = 'C:\TemplatePath'
Set-AzureStorageFileContent -ShareName $fileShare.Name -Context $context -Source $templateFile
```

## <a name="create-hello-powershell-runbook-script"></a><span data-ttu-id="2d728-126">Creare lo script del runbook PowerShell hello</span><span class="sxs-lookup"><span data-stu-id="2d728-126">Create hello PowerShell runbook script</span></span>

<span data-ttu-id="2d728-127">Ora è creare uno script di PowerShell che ottiene hello `TemplateTest.json` file dall'archiviazione di Azure e distribuisce hello modello toocreate un nuovo account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="2d728-127">Now we create a PowerShell script that gets hello `TemplateTest.json` file from Azure Storage and deploys hello template toocreate a new Azure Storage account.</span></span>

<span data-ttu-id="2d728-128">In un editor di testo, incollare hello seguente testo:</span><span class="sxs-lookup"><span data-stu-id="2d728-128">In a text editor, paste hello following text:</span></span>

```powershell
param (
    [Parameter(Mandatory=$true)]
    [string]
    $ResourceGroupName,

    [Parameter(Mandatory=$true)]
    [string]
    $StorageAccountName,

    [Parameter(Mandatory=$true)]
    [string]
    $StorageAccountKey,

    [Parameter(Mandatory=$true)]
    [string]
    $StorageFileName
)



# Authenticate tooAzure if running from Azure Automation
$ServicePrincipalConnection = Get-AutomationConnection -Name "AzureRunAsConnection"
Add-AzureRmAccount `
    -ServicePrincipal `
    -TenantId $ServicePrincipalConnection.TenantId `
    -ApplicationId $ServicePrincipalConnection.ApplicationId `
    -CertificateThumbprint $ServicePrincipalConnection.CertificateThumbprint | Write-Verbose

#Set hello parameter values for hello Resource Manager template
$Parameters = @{
    "storageAccountType"="Standard_LRS"
    }

# Create a new context
$Context = New-AzureStorageContext -StorageAccountKey $StorageAccountKey

Get-AzureStorageFileContent -ShareName 'resource-templates' -Context $Context -path 'TemplateTest.json' -Destination 'C:\Temp'

$TemplateFile = Join-Path -Path 'C:\Temp' -ChildPath $StorageFileName

# Deploy hello storage account
New-AzureRmResourceGroupDeployment -ResourceGroupName $ResourceGroupName -TemplateFile $TemplateFile -TemplateParameterObject $Parameters 
``` 

<span data-ttu-id="2d728-129">Salvare file hello localmente come `DeployTemplate.ps1`.</span><span class="sxs-lookup"><span data-stu-id="2d728-129">Save hello file locally as `DeployTemplate.ps1`.</span></span>

## <a name="import-and-publish-hello-runbook-into-your-azure-automation-account"></a><span data-ttu-id="2d728-130">Importare e pubblicare hello runbook nell'account di automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="2d728-130">Import and publish hello runbook into your Azure Automation account</span></span>

<span data-ttu-id="2d728-131">Ora è utilizzare PowerShell tooimport hello runbook nell'account di automazione di Azure e quindi pubblicare il runbook hello.</span><span class="sxs-lookup"><span data-stu-id="2d728-131">Now we use PowerShell tooimport hello runbook into your Azure Automation account, and then publish hello runbook.</span></span>
<span data-ttu-id="2d728-132">Per informazioni su come tooimport e pubblicare un runbook in hello portale di Azure, vedere [creazione o importazione di un runbook in automazione di Azure](automation-creating-importing-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="2d728-132">For information about how tooimport and publish a runbook in hello Azure portal, see [Creating or importing a runbook in Azure Automation](automation-creating-importing-runbook.md).</span></span>

<span data-ttu-id="2d728-133">tooimport `DeployTemplate.ps1` nell'account di automazione come un runbook di PowerShell, eseguire i comandi di PowerShell seguente hello:</span><span class="sxs-lookup"><span data-stu-id="2d728-133">tooimport `DeployTemplate.ps1` into your Automation account as a PowerShell runbook, run hello following PowerShell commands:</span></span>

```powershell
# MyPath is hello path where you saved DeployTemplate.ps1
# MyResourceGroup is hello name of hello Azure ResourceGroup that contains your Azure Automation account
# MyAutomationAccount is hello name of your Automation account
$importParams = @{
    Path = 'C:\MyPath\DeployTemplate.ps1'
    ResourceGroupName = 'MyResourceGroup'
    AutomationAccountName = 'MyAutomationAccount'
    Type = 'PowerShell'
}
Import-AzureRmAutomationRunbook @

# Publish hello runbook
$publishParams = @{
    ResourceGroupName = 'MyResourceGroup'
    AutomationAccountName = 'MyAutomationAccount'
    Name = 'DeployTemplate'
}
Publish-AzureRmAutomationRunbook @publishParams
```

## <a name="start-hello-runbook"></a><span data-ttu-id="2d728-134">Avviare il runbook hello</span><span class="sxs-lookup"><span data-stu-id="2d728-134">Start hello runbook</span></span>

<span data-ttu-id="2d728-135">Ora runbook hello viene innanzitutto chiamata hello [inizio AzureRmAutomationRunbook](https://docs.microsoft.com/powershell/module/azurerm.automation/start-azurermautomationrunbook?view=azurermps-4.1.0) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2d728-135">Now we start hello runbook by calling hello [Start-AzureRmAutomationRunbook](https://docs.microsoft.com/powershell/module/azurerm.automation/start-azurermautomationrunbook?view=azurermps-4.1.0) cmdlet.</span></span>

<span data-ttu-id="2d728-136">Per informazioni su come toostart un runbook nel portale di Azure hello vedere [avvio di un runbook in automazione di Azure](automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="2d728-136">For information about how toostart a runbook in hello Azure portal, see [Starting a runbook in Azure Automation](automation-starting-a-runbook.md).</span></span>

<span data-ttu-id="2d728-137">Eseguire i seguenti comandi nella console di PowerShell hello hello:</span><span class="sxs-lookup"><span data-stu-id="2d728-137">Run hello following commands in hello PowerShell console:</span></span>

```powershell
# Set up hello parameters for hello runbook
$runbookParams = @{
    ResourceGroupName = 'MyResourceGroup'
    StorageAccountName = 'MyStorageAccount'
    StorageAccountKey = $key[0].Value # We got this key earlier
    StorageFileName = 'TemplateTest.json' 
}

# Set up parameters for hello Start-AzureRmAutomationRunbook cmdlet
$startParams = @{
    ResourceGroupName = 'MyResourceGroup'
    AutomationAccountName = 'MyAutomationAccount'
    Name = 'DeployTemplate'
    Parameters = $runbookParams
}

# Start hello runbook
$job = Start-AzureRmAutomationRunbook @startParams
```

<span data-ttu-id="2d728-138">viene eseguito runbook Hello, ed è possibile verificare lo stato eseguendo `$job.Status`.</span><span class="sxs-lookup"><span data-stu-id="2d728-138">hello runbook runs, and you can check its status by running `$job.Status`.</span></span>

<span data-ttu-id="2d728-139">Ottiene il modello di gestione risorse di hello runbook Hello e lo usa toodeploy un nuovo account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="2d728-139">hello runbook gets hello Resource Manager template and uses it toodeploy a new Azure Storage account.</span></span>
<span data-ttu-id="2d728-140">È possibile vedere che è stato creato il nuovo account di archiviazione hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="2d728-140">You can see that hello new storage account was created by running hello following command:</span></span>
```powershell
Get-AzureRmStorageAccount
```

## <a name="summary"></a><span data-ttu-id="2d728-141">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="2d728-141">Summary</span></span>

<span data-ttu-id="2d728-142">L'operazione è terminata.</span><span class="sxs-lookup"><span data-stu-id="2d728-142">That's it!</span></span> <span data-ttu-id="2d728-143">Ora è possibile utilizzare automazione di Azure e archiviazione di Azure e Gestione risorse modelli toodeploy tutte le risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="2d728-143">Now you can use Azure Automation and Azure Storage, and Resource Manager templates toodeploy all your Azure resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2d728-144">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2d728-144">Next steps</span></span>

* <span data-ttu-id="2d728-145">toolearn più sui modelli di gestione risorse, vedere [Panoramica di gestione risorse di Azure](../azure-resource-manager/resource-group-overview.md)</span><span class="sxs-lookup"><span data-stu-id="2d728-145">toolearn more about Resource Manager templates, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md)</span></span>
* <span data-ttu-id="2d728-146">tooget avviato con l'archiviazione di Azure, vedere [tooAzure introduzione archiviazione](../storage/common/storage-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2d728-146">tooget started with Azure Storage, see [Introduction tooAzure Storage](../storage/common/storage-introduction.md).</span></span>
* <span data-ttu-id="2d728-147">toofind altri runbook di automazione di Azure utili, vedere [raccolte Runbook e moduli di automazione di Azure](automation-runbook-gallery.md).</span><span class="sxs-lookup"><span data-stu-id="2d728-147">toofind other useful Azure Automation runbooks, see [Runbook and module galleries for Azure Automation](automation-runbook-gallery.md).</span></span>
* <span data-ttu-id="2d728-148">toofind altri modelli di gestione risorse utili, vedere [modelli di avvio rapido di Azure](https://azure.microsoft.com/resources/templates/)</span><span class="sxs-lookup"><span data-stu-id="2d728-148">toofind other useful Resource Manager templates, see [Azure Quickstart Templates](https://azure.microsoft.com/resources/templates/)</span></span>

