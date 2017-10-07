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
# <a name="deploy-an-azure-resource-manager-template-in-an-azure-automation-powershell-runbook"></a>Distribuire un modello di Azure Resource Manager in un runbook PowerShell di Automazione di Azure

È possibile scrivere un [runbook PowerShell di Automazione di Azure](automation-first-runbook-textual-powershell.md) che distribuisce una risorsa di Azure usando un [modello di Azure Resource Management](../azure-resource-manager/resource-manager-create-first-template.md).

Con questa operazione è possibile automatizzare la distribuzione delle risorse di Azure. È possibile anche gestire i modelli di Resource Manager in una posizione centrale protetta come Archiviazione di Azure.

In questo argomento, si crea un runbook di PowerShell che utilizza un modello di gestione risorse archiviato in [di archiviazione di Azure](../storage/common/storage-introduction.md) toodeploy un nuovo account di archiviazione di Azure.

## <a name="prerequisites"></a>Prerequisiti

toocomplete questa esercitazione, è necessario hello seguenti:

* Sottoscrizione di Azure. Se non si ha ancora una sottoscrizione, è possibile [attivare i vantaggi della sottoscrizione MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) oppure <a href="/pricing/free-account/" target="_blank">[iscriversi per ottenere un account gratuito](https://azure.microsoft.com/free/).
* [Account di automazione](automation-sec-configure-azure-runas-account.md) toohold hello runbook ed eseguire l'autenticazione tooAzure risorse.  Questo account deve disporre dell'autorizzazione toostart e arrestare la macchina virtuale hello.
* [Account di archiviazione Azure](../storage/common/storage-create-storage-account.md) in quale modello di gestione risorse di hello toostore
* Azure Powershell installato in un computer locale. Vedere [installare e configurare Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) per informazioni su come tooget Azure PowerShell.

## <a name="create-hello-resource-manager-template"></a>Creare il modello di gestione risorse di hello

In questo esempio si userà un modello di Resource Manager che distribuisce un nuovo account di Archiviazione di Azure.

In un editor di testo copiare hello seguente testo:

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

Salvare file hello localmente come `TemplateTest.json`.

## <a name="save-hello-resource-manager-template-in-azure-storage"></a>Salvare il modello di gestione risorse di hello in archiviazione di Azure

Ora è utilizzare PowerShell toocreate una condivisione di file di archiviazione di Azure e caricare hello `TemplateTest.json` file.
Per istruzioni sulla modalità di condivisione e di caricare un file nel portale di Azure hello toocreate un file, vedere [Introduzione all'archiviazione di File di Azure in Windows](../storage/files/storage-dotnet-how-to-use-files.md).

Avviare PowerShell nel computer locale, eseguire i seguenti comandi toocreate una condivisione file hello e caricare la condivisione file hello Gestione risorse modello toothat.

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

## <a name="create-hello-powershell-runbook-script"></a>Creare lo script del runbook PowerShell hello

Ora è creare uno script di PowerShell che ottiene hello `TemplateTest.json` file dall'archiviazione di Azure e distribuisce hello modello toocreate un nuovo account di archiviazione di Azure.

In un editor di testo, incollare hello seguente testo:

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

Salvare file hello localmente come `DeployTemplate.ps1`.

## <a name="import-and-publish-hello-runbook-into-your-azure-automation-account"></a>Importare e pubblicare hello runbook nell'account di automazione di Azure

Ora è utilizzare PowerShell tooimport hello runbook nell'account di automazione di Azure e quindi pubblicare il runbook hello.
Per informazioni su come tooimport e pubblicare un runbook in hello portale di Azure, vedere [creazione o importazione di un runbook in automazione di Azure](automation-creating-importing-runbook.md).

tooimport `DeployTemplate.ps1` nell'account di automazione come un runbook di PowerShell, eseguire i comandi di PowerShell seguente hello:

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

## <a name="start-hello-runbook"></a>Avviare il runbook hello

Ora runbook hello viene innanzitutto chiamata hello [inizio AzureRmAutomationRunbook](https://docs.microsoft.com/powershell/module/azurerm.automation/start-azurermautomationrunbook?view=azurermps-4.1.0) cmdlet.

Per informazioni su come toostart un runbook nel portale di Azure hello vedere [avvio di un runbook in automazione di Azure](automation-starting-a-runbook.md).

Eseguire i seguenti comandi nella console di PowerShell hello hello:

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

viene eseguito runbook Hello, ed è possibile verificare lo stato eseguendo `$job.Status`.

Ottiene il modello di gestione risorse di hello runbook Hello e lo usa toodeploy un nuovo account di archiviazione di Azure.
È possibile vedere che è stato creato il nuovo account di archiviazione hello eseguendo hello comando seguente:
```powershell
Get-AzureRmStorageAccount
```

## <a name="summary"></a>Riepilogo

L'operazione è terminata. Ora è possibile utilizzare automazione di Azure e archiviazione di Azure e Gestione risorse modelli toodeploy tutte le risorse di Azure.

## <a name="next-steps"></a>Passaggi successivi

* toolearn più sui modelli di gestione risorse, vedere [Panoramica di gestione risorse di Azure](../azure-resource-manager/resource-group-overview.md)
* tooget avviato con l'archiviazione di Azure, vedere [tooAzure introduzione archiviazione](../storage/common/storage-introduction.md).
* toofind altri runbook di automazione di Azure utili, vedere [raccolte Runbook e moduli di automazione di Azure](automation-runbook-gallery.md).
* toofind altri modelli di gestione risorse utili, vedere [modelli di avvio rapido di Azure](https://azure.microsoft.com/resources/templates/)

