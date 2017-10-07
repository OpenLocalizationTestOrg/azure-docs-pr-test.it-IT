---
title: aaaPass un formato JSON dell'oggetto tooan runbook di automazione di Azure | Documenti Microsoft
description: Come toopass parametri tooa runbook come un oggetto JSON
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
ms.date: 06/15/2017
ms.author: eslesar
ms.openlocfilehash: 8229a16015d549927ead5496c70e9fb391d35498
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="pass-a-json-object-tooan-azure-automation-runbook"></a>Passare a un runbook di automazione di Azure tooan oggetto JSON

Può essere utile toostore dati che si desidera toopass tooa runbook in un file JSON.
Ad esempio, è possibile creare un file JSON che contiene tutti i parametri di hello desiderato toopass tooa runbook.
toodo, si tooconvert hello JSON tooa stringa e quindi convertire l'oggetto di PowerShell tooa stringa hello prima di passare il runbook toohello contenuto.

In questo esempio, si creerà uno script di PowerShell che chiama [inizio AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) toostart un runbook di PowerShell, il passaggio di contenuto di hello di hello JSON toohello runbook.
runbook PowerShell Hello avvia una macchina virtuale di Azure, recupero dei parametri di hello per hello VM da hello JSON che è stato passato.

## <a name="prerequisites"></a>Prerequisiti
toocomplete questa esercitazione, è necessario hello seguenti:

* Sottoscrizione di Azure. Se non si ha ancora una sottoscrizione, è possibile [attivare i vantaggi della sottoscrizione MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) oppure <a href="/pricing/free-account/" target="_blank">[iscriversi per ottenere un account gratuito](https://azure.microsoft.com/free/).
* [Account di automazione](automation-sec-configure-azure-runas-account.md) toohold hello runbook ed eseguire l'autenticazione tooAzure risorse.  Questo account deve disporre dell'autorizzazione toostart e arrestare la macchina virtuale hello.
* Macchina virtuale di Azure. La macchina virtuale viene arrestata e avviata, quindi non deve essere una macchina virtuale di produzione.
* Azure Powershell installato in un computer locale. Vedere [installare e configurare Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) per informazioni su come tooget Azure PowerShell.

## <a name="create-hello-json-file"></a>Creare file JSON hello

Digitare quanto segue di hello test in un file di testo e salvarlo come `test.json` in un punto qualsiasi nel computer locale.

```json
{
   "VmName" : "TestVM",
   "ResourceGroup" : "AzureAutomationTest"
}
```

## <a name="create-hello-runbook"></a>Creare runbook hello

Creare un nuovo runbook di PowerShell denominato "Test-Json" in Automazione di Azure.
toolearn toocreate un nuovo runbook di PowerShell, vedere [il primo runbook PowerShell](automation-first-runbook-textual-powershell.md).

dati JSON hello tooaccept hello runbook deve accettare un oggetto come un parametro di input.

runbook Hello è quindi possibile utilizzare le proprietà di hello definite in hello JSON.

```powershell
Param(
     [parameter(Mandatory=$true)]
     [object]$json
)

# Connect tooAzure account   
$Conn = Get-AutomationConnection -Name AzureRunAsConnection
Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationID $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint

# Convert object tooactual JSON
$json = $json | ConvertFrom-Json

# Use hello values from hello JSON object as hello parameters for your command
Start-AzureRmVM -Name $json.VMName -ResourceGroupName $json.ResourceGroup
 ```

 Salvare e pubblicare il runbook nell'account di automazione.

## <a name="call-hello-runbook-from-powershell"></a>Chiamata runbook hello da PowerShell

È ora possibile chiamare hello runbook dal computer locale tramite Azure PowerShell.
Eseguire i seguenti comandi PowerShell hello:

1. Accedi tooAzure:
   ```powershell
   Login-AzureRmAccount
   ```
    Si sono tooenter richieste le credenziali di Azure.
1. Ottenere il contenuto di hello del file JSON hello e convertirlo tooa stringa:
    ```powershell
    $json =  (Get-content -path 'JsonPath\test.json' -Raw) | Out-string
    ```
    `JsonPath`è il percorso di hello in cui è stato salvato il file JSON di hello.
1. Convertire il contenuto della stringa hello `$json` tooa PowerShell oggetto:
   ```powershell
   $JsonParams = @{"json"=$json}
   ```
1. Creare una tabella hash per i parametri di hello per `Start-AzureRmAutomstionRunbook`:
   ```powershell
   $RBParams = @{
        AutomationAccountName = 'AATest'
        ResourceGroupName = 'RGTest'
        Name = 'Test-Json'
        Parameters = $JsonParams
   }
   ```
   Si noti che è impostato come valore hello `Parameters` toohello PowerShell oggetto che contiene i valori hello dal file JSON hello. 
1. Avviare il runbook hello
   ```powershell
   $job = Start-AzureRmAutomationRunbook @RBParams
   ```

Hello runbook vengono utilizzati valori hello hello JSON file toostart una macchina virtuale.

## <a name="next-steps"></a>Passaggi successivi

* toolearn più sulla modifica di runbook PowerShell e flusso di lavoro di PowerShell con un editor di testo, vedere [modifica testuale runbook in automazione di Azure](automation-edit-textual-runbook.md) 
* toolearn ulteriori informazioni su creazione e importazione di runbook, vedere [creazione o importazione di un runbook in automazione di Azure](automation-creating-importing-runbook.md)


