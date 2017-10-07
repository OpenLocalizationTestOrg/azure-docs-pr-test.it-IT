---
title: configurazione dell'account di automazione di Azure aaaValidate | Documenti Microsoft
description: "In questo articolo viene descritto come configurazione hello tooconfirm dell'account di automazione è configurato correttamente."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/07/2017
ms.author: magoedte
ms.openlocfilehash: 3a990dcc6661cf67c4b62592ce03d55a3791053a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="test-azure-automation-run-as-account-authentication"></a>Testare l'autenticazione con un account RunAs di Automazione di Azure
Dopo aver creato un account di automazione correttamente, è possibile eseguire tooconfirm un semplice test si è in grado di autenticare toosuccessfully in Gestione risorse di Azure o distribuzione di Azure classica con l'account RunAs automazione appena creato o aggiornato.    

## <a name="automation-run-as-authentication"></a>Autenticazione con l'account RunAs di Automazione
Utilizzare anche codice di esempio hello seguente[creare un runbook PowerShell](automation-creating-importing-runbook.md) autenticazione tooverify utilizzando hello eseguite come account e anche in tooauthenticate il runbook personalizzati e gestire le risorse di gestione delle risorse con l'account di automazione.   

    $connectionName = "AzureRunAsConnection"
    try
    {
        # Get hello connection "AzureRunAsConnection "
        $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         

        "Logging in tooAzure..."
        Add-AzureRmAccount `
           -ServicePrincipal `
           -TenantId $servicePrincipalConnection.TenantId `
           -ApplicationId $servicePrincipalConnection.ApplicationId `
           -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint 
    }
    catch {
       if (!$servicePrincipalConnection)
       {
          $ErrorMessage = "Connection $connectionName not found."
          throw $ErrorMessage
      } else{
          Write-Error -Message $_.Exception
          throw $_.Exception
      }
    }

    #Get all ARM resources from all resource groups
    $ResourceGroups = Get-AzureRmResourceGroup 

    foreach ($ResourceGroup in $ResourceGroups)
    {    
       Write-Output ("Showing resources in resource group " + $ResourceGroup.ResourceGroupName)
       $Resources = Find-AzureRmResource -ResourceGroupNameContains $ResourceGroup.ResourceGroupName | Select ResourceName, ResourceType
       ForEach ($Resource in $Resources)
       {
          Write-Output ($Resource.ResourceName + " of type " +  $Resource.ResourceType)
       }
       Write-Output ("")
    } 

Si noti hello cmdlet usato per l'autenticazione runbook hello - **Aggiungi AzureRmAccount**, hello utilizza *ServicePrincipalCertificate* set di parametri.  ed esegue l'autenticazione usando il certificato dell'entità servizio, non le credenziali.  

Quando si [eseguire runbook hello](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) toovalidate l'account RunAs, un [processo del runbook](automation-runbook-execution.md) viene creato, viene visualizzato il pannello di processo hello e visualizzato lo stato del processo hello in hello **riepilogo**riquadro. lo stato del processo Hello verrà avviato come *in coda* che indica che è in attesa per un runbook worker in hello cloud toobecome disponibili. Verranno quindi spostati troppo*iniziale* quando un thread di lavoro attestazioni processo hello e quindi *esecuzione* quando runbook hello effettivamente avviata l'esecuzione.  Al termine del processo del runbook hello, dovremmo vedere lo stato **completato**.

toosee hello risultati dettagliati di hello runbook, fare clic su hello **Output** riquadro.  In hello **Output** pannello, si noterà ha autenticato e restituisce un elenco di tutte le risorse in tutti i gruppi di risorse nella sottoscrizione.  

Ricorda però blocco hello tooremove codice che inizia con il commento hello `#Get all ARM resources from all resource groups` quando è riutilizzare codice hello dai runbook.

## <a name="classic-run-as-authentication"></a>Autenticazione con l'account RunAs classico
Utilizzare anche codice di esempio hello seguente[creare un runbook PowerShell](automation-creating-importing-runbook.md) tooverify l'autenticazione tramite hello Classic eseguite come account e anche in tooauthenticate il runbook personalizzati e gestire le risorse nel modello di distribuzione classica hello.  

    $ConnectionAssetName = "AzureClassicRunAsConnection"
    # Get hello connection
    $connection = Get-AutomationConnection -Name $connectionAssetName        

    # Authenticate tooAzure with certificate
    Write-Verbose "Get connection asset: $ConnectionAssetName" -Verbose
    $Conn = Get-AutomationConnection -Name $ConnectionAssetName
    if ($Conn -eq $null)
    {
       throw "Could not retrieve connection asset: $ConnectionAssetName. Assure that this asset exists in hello Automation account."
    }

    $CertificateAssetName = $Conn.CertificateAssetName
    Write-Verbose "Getting hello certificate: $CertificateAssetName" -Verbose
    $AzureCert = Get-AutomationCertificate -Name $CertificateAssetName
    if ($AzureCert -eq $null)
    {
       throw "Could not retrieve certificate asset: $CertificateAssetName. Assure that this asset exists in hello Automation account."
    }

    Write-Verbose "Authenticating tooAzure with certificate." -Verbose
    Set-AzureSubscription -SubscriptionName $Conn.SubscriptionName -SubscriptionId $Conn.SubscriptionID -Certificate $AzureCert
    Select-AzureSubscription -SubscriptionId $Conn.SubscriptionID
    
    #Get all VMs in hello subscription and return list with name of each
    Get-AzureVM | ft Name

Quando si [eseguire runbook hello](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) toovalidate l'account RunAs, un [processo del runbook](automation-runbook-execution.md) viene creato, viene visualizzato il pannello di processo hello e visualizzato lo stato del processo hello in hello **riepilogo**riquadro. lo stato del processo Hello verrà avviato come *in coda* che indica che è in attesa per un runbook worker in hello cloud toobecome disponibili. Verranno quindi spostati troppo*iniziale* quando un thread di lavoro attestazioni processo hello e quindi *esecuzione* quando runbook hello effettivamente avviata l'esecuzione.  Al termine del processo del runbook hello, dovremmo vedere lo stato **completato**.

toosee hello risultati dettagliati di hello runbook, fare clic su hello **Output** riquadro.  In hello **Output** pannello, si noterà ha autenticato e restituisce un elenco di tutte le macchine virtuali di Azure da VMName che vengono distribuiti nella sottoscrizione.  

Ricorda però tooremove hello cmdlet **Get-AzureVM** quando è riutilizzare codice hello dai runbook.

## <a name="next-steps"></a>Passaggi successivi
* tooget avviato con runbook PowerShell, vedere [il primo runbook PowerShell](automation-first-runbook-textual-powershell.md).
* toolearn ulteriori informazioni sui grafici per la modifica, vedere [grafici per la modifica in automazione di Azure](automation-graphical-authoring-intro.md).
