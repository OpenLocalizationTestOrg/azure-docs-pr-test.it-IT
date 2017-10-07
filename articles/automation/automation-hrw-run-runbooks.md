---
title: aaaRun runbook in Runbook Worker ibrido automazione di Azure | Documenti Microsoft
description: Questo articolo fornisce informazioni sull'esecuzione dei runbook sul computer nel proprio data center locale o un provider di cloud con il ruolo di lavoro ibridi per Runbook hello.
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 06227cda-f3d1-47fe-b3f8-436d2b9d81ee
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/22/2017
ms.author: magoedte
ms.openlocfilehash: 51961e02603e5690edd11e577594ad2ddea489a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="running-runbooks-on-a-hybrid-runbook-worker"></a>Esecuzione di runbook in un ruolo di lavoro ibrido per runbook 
Non c'è alcuna differenza nella struttura di hello di runbook in esecuzione in automazione di Azure e quelle eseguite in un Runbook Worker ibrido. I runbook che utilizzare con ogni probabilmente differisce notevolmente tuttavia poiché i runbook di destinazione di un Runbook Worker ibrido in genere la gestione delle risorse sul computer locale di hello stesso o sulle risorse nell'ambiente di hello locale in cui è distribuito, mentre i runbook in automazione di Azure è in genere gestire le risorse in hello cloud di Azure.

È possibile modificare un runbook per lavoro ibridi per Runbook in automazione di Azure, ma è possibile che problemi se si tenta di tootest hello runbook nell'editor di hello.  i moduli di PowerShell Hello che accedono alle risorse locali hello potrebbero non essere installate nell'ambiente di automazione di Azure in questo caso, avrà esito negativo test hello.  Se si installa hello necessari moduli, quindi hello runbook verrà eseguito, ma non sarà in grado di tooaccess risorse locali per un test completo.

## <a name="starting-a-runbook-on-hybrid-runbook-worker"></a>Avvio di un runbook in un ruolo di lavoro ibrido per runbook
[avvio di un runbook in Automazione di Azure](automation-starting-a-runbook.md) illustra diversi modi in cui è possibile eseguire l'avvio dei runbook.  Runbook Worker ibrido aggiunge un **RunOn** opzione in cui è possibile specificare il nome di hello di un gruppo di Runbook Worker ibrido.  Se viene specificato un gruppo, quindi runbook hello viene recuperato ed eseguito dei lavoratori hello in tale gruppo.  Se non si specifica l'opzione, verrà eseguito come di consueto in Automazione di Azure.

Quando si avvia un runbook nel portale di Azure hello, viene visualizzata una **eseguiti** opzione che consente di selezionare **Azure** o **Worker ibrido**.  Se si seleziona **Worker ibrido**, è quindi possibile selezionare il gruppo di hello da un elenco a discesa.

Hello utilizzare **RunOn** parametro.  È possibile utilizzare hello successivo comando toostart un runbook denominato Test-Runbook su un gruppo di Runbook Worker ibrido denominato MyHybridGroup utilizzando Windows PowerShell.

    Start-AzureRmAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Test-Runbook" -RunOn "MyHybridGroup"

> [!NOTE]
> Hello **RunOn** toohello è stato aggiunto il parametro **Start-AzureAutomationRunbook** cmdlet nella versione 0.9.1 di Microsoft Azure PowerShell.  È necessario [scaricare la versione più recente di hello](https://azure.microsoft.com/downloads/) se si dispone di una precedente installazione.  È necessario solo tooinstall questa versione in una workstation in cui si avvia runbook hello da Windows PowerShell.  Non è necessario tooinstall sul computer di lavoro hello a meno che non si prevede di runbook toostart da tale computer.  È attualmente non può avviare un runbook in un Runbook Worker ibrido da un altro runbook, poiché ciò richiede più recente di Azure Powershell toobe installato nell'account di automazione hello.  la versione più recente di Hello viene aggiornata automaticamente in automazione di Azure e automaticamente propagata non appena toohello worker.
>
>

## <a name="runbook-permissions"></a>Autorizzazioni per i runbook
I runbook in esecuzione in un Runbook Worker ibrido non è possibile utilizzare hello stesso metodo che viene in genere utilizzata per i runbook autenticazione tooAzure risorse, poiché accedono alle risorse all'esterno di Azure.  runbook Hello possibile fornire la propria autenticazione toolocal risorse oppure è possibile specificare un tooprovide account RunAs un contesto utente per tutti i runbook.

### <a name="runbook-authentication"></a>Autenticazione dei runbook
Per impostazione predefinita, i runbook verranno eseguiti nel contesto di hello hello locale dell'account di sistema nel computer locale hello, pertanto è necessario che specifichi le proprie tooresources di autenticazione che avranno accesso.  

È possibile utilizzare [credenziali](http://msdn.microsoft.com/library/dn940015.aspx) e [certificato](http://msdn.microsoft.com/library/dn940013.aspx) asset nel runbook con i cmdlet che consentono di toospecify credenziali in modo da poter autenticare toodifferent risorse.  Hello esempio seguente viene mostrata una parte di un runbook che riavvia un computer.  Recupera le credenziali da un nome di risorsa e hello credenziale di computer hello da un asset della variabile e quindi utilizza questi valori con il cmdlet Restart-Computer hello.

    $Cred = Get-AzureRmAutomationCredential -ResourceGroupName "ResourceGroup01" -Name "MyCredential"
    $Computer = Get-AzureRmAutomationVariable -ResourceGroupName "ResourceGroup01" -Name  "ComputerName"

    Restart-Computer -ComputerName $Computer -Credential $Cred

È anche possibile sfruttare [InlineScript](automation-powershell-workflow.md#inlinescript), che consente toorun blocchi di codice in un altro computer con le credenziali specificate da hello [parametro comune PSCredential](http://technet.microsoft.com/library/jj129719.aspx).

### <a name="runas-account"></a>Account RunAs
Anziché runbook fornire la propria autenticazione toolocal risorse, è possibile specificare un **RunAs** account per un gruppo di lavoro ibrido.  Specificare un [asset delle credenziali](automation-credentials.md) che ha accesso alle risorse di toolocal e tutti i runbook eseguito con tali credenziali durante l'esecuzione in un Runbook Worker ibrido nel gruppo di hello.  

nome utente di Hello per le credenziali di hello deve essere in uno dei seguenti formati hello:

* dominio\nome utente
* username@domain
* nome utente (per computer locale di account locale toohello)

Utilizzare hello seguendo procedure toospecify un account RunAs per un gruppo di lavoro ibrido:

1. Creare un [asset delle credenziali](automation-credentials.md) con toolocal di accedere alle risorse.
2. Aprire l'account di automazione hello in hello portale di Azure.
3. Seleziona hello **gruppi di lavoro ibrido** riquadro e quindi selezionare il gruppo di hello.
4. Selezionare **Tutte le impostazioni** e quindi **Impostazioni del gruppo di lavoro ibrido**.
5. Modifica **runas** da **predefinito** troppo**personalizzato**.
6. Selezionare credenziali hello e fare clic su **salvare**.

### <a name="automation-run-as-account"></a>Account RunAs di Automazione
Come parte del processo di compilazione automatizzato per la distribuzione delle risorse in Azure, potrebbe essere necessario l'accesso locale tooon sistemi toosupport un'attività o un set di passaggi nella sequenza di distribuzione.  l'autenticazione toosupport utilizzando account RunAs hello Azure, è necessario tooinstall hello runas certificato dell'account.  

Hello seguente runbook di PowerShell, *esportazione RunAsCertificateToHybridWorker*, hello runas certificato viene esportato dall'account di automazione di Azure e scarica e importarli nell'archivio certificati del computer locale hello in un Ruoli di lavoro ibridi connessi toohello stesso account.  Una volta completato questo passaggio, verifica lavoro hello può eseguire l'autenticazione utilizzando l'account RunAs hello tooAzure.

    <#PSScriptInfo
    .VERSION 1.0
    .GUID 3a796b9a-623d-499d-86c8-c249f10a6986
    .AUTHOR Azure Automation Team
    .COMPANYNAME Microsoft
    .COPYRIGHT 
    .TAGS Azure Automation 
    .LICENSEURI 
    .PROJECTURI 
    .ICONURI 
    .EXTERNALMODULEDEPENDENCIES 
    .REQUIREDSCRIPTS 
    .EXTERNALSCRIPTDEPENDENCIES 
    .RELEASENOTES
    #>

    <#  
    .SYNOPSIS  
    Exports hello Run As certificate from an Azure Automation account tooa hybrid worker in that account. 
  
    .DESCRIPTION  
    This runbook exports hello Run As certificate from an Azure Automation account tooa hybrid worker in that account.
    Run this runbook in hello hybrid worker where you want hello certificate installed.
    This allows hello use of hello AzureRunAsConnection tooauthenticate tooAzure and manage Azure resources from runbooks running in hello hybrid worker.

    .EXAMPLE
    .\Export-RunAsCertificateToHybridWorker

    .NOTES
    AUTHOR: Azure Automation Team 
    LASTEDIT: 2016.10.13
    #>

    [OutputType([string])] 

    # Set hello password used for this certificate
    $Password = "YourStrongPasswordForTheCert"

    # Stop on errors
    $ErrorActionPreference = 'stop'

    # Get hello management certificate that will be used toomake calls into Azure Service Management resources
    $RunAsCert = Get-AutomationCertificate -Name "AzureRunAsCertificate"
       
    # location toostore temporary certificate in hello Automation service host
    $CertPath = Join-Path $env:temp  "AzureRunAsCertificate.pfx"
   
    # Save hello certificate
    $Cert = $RunAsCert.Export("pfx",$Password)
    Set-Content -Value $Cert -Path $CertPath -Force -Encoding Byte | Write-Verbose 

    Write-Output ("Importing certificate into $env:computername local machine root store from " + $CertPath)
    $SecurePassword = ConvertTo-SecureString $Password -AsPlainText -Force
    Import-PfxCertificate -FilePath $CertPath -CertStoreLocation Cert:\LocalMachine\My -Password $SecurePassword -Exportable | Write-Verbose

    # Test that authentication tooAzure Resource Manager is working
    $RunAsConnection = Get-AutomationConnection -Name "AzureRunAsConnection" 
    
    Add-AzureRmAccount `
      -ServicePrincipal `
      -TenantId $RunAsConnection.TenantId `
      -ApplicationId $RunAsConnection.ApplicationId `
      -CertificateThumbprint $RunAsConnection.CertificateThumbprint | Write-Verbose

    Set-AzureRmContext -SubscriptionId $RunAsConnection.SubscriptionID | Write-Verbose

    # List automation accounts tooconfirm Azure Resource Manager calls are working
    Get-AzureRmAutomationAccount | Select AutomationAccountName

Salvare hello *esportazione RunAsCertificateToHybridWorker* runbook tooyour computer con un `.ps1` estensione.  Importarlo nell'account di automazione e modificare runbook hello, modifica il valore di hello di hello variabile `$Password` con la propria password.  Pubblicare ed eseguire runbook hello gruppo di lavoro ibridi hello che eseguono e l'autenticazione utilizzando l'account RunAs hello runbook di destinazione.  Hello processo flusso report hello tentativo tooimport hello certificato nell'archivio del computer locale hello e segue con più righe, a seconda del numero di account di automazione è definito nella sottoscrizione e se l'autenticazione ha esito positivo.  

## <a name="troubleshooting-runbooks-on-hybrid-runbook-worker"></a>Risoluzione dei problemi relativi ai runbook nel ruolo di lavoro ibrido per runbook
I log vengono archiviati localmente in ogni ruolo di lavoro ibrido in C:\ProgramData\Microsoft\System Center\Orchestrator\7.2\SMA\Sandboxes.  Ruolo di lavoro ibrido registra anche errori ed eventi nel registro eventi di Windows hello in **applicazioni e servizi Logs\Microsoft-SMA\Operational**.  Gli eventi correlati toorunbooks eseguita nel ruolo di lavoro hello vengono scritti troppo**applicazioni e servizi Logs\Microsoft-Automation\Operational**.  Hello **Microsoft SMA** log include molti più eventi toohello correlati runbook processo toohello inserito hello e lavoro elaborazione del runbook hello.  Durante la hello **automazione di Microsoft** registro eventi non dispone di molti eventi con dettagli assistito hello risoluzione dei problemi di esecuzione del runbook, si noterà almeno risultati hello di processo del runbook hello.  

[I messaggi e output di runbook](automation-runbook-output-and-messages.md) inviati tooAzure automazione da processi di lavoro ibridi soli come i processi di runbook eseguiti nel cloud hello.  È inoltre possibile abilitare hello dettagliato e flussi di stato di avanzamento hello stesso si farebbe per altri runbook.  

Se i runbook non vengono completate correttamente e viene visualizzato lo stato processo hello riepilogo **Suspended**, consultare Risoluzione dei problemi di articolo hello [Runbook Worker ibrido: consente di terminare un processo del runbook con lo stato Sospeso](automation-troubleshooting-hybrid-runbook-worker.md#a-runbook-job-terminates-with-a-status-of-suspended).   

## <a name="next-steps"></a>Passaggi successivi
* toolearn informazioni su hello diversi metodi che possono essere utilizzati toostart un runbook, vedere [avvio di un Runbook in automazione di Azure](automation-starting-a-runbook.md).  
* toounderstand hello procedure diverse per l'utilizzo di PowerShell e flusso di lavoro PowerShell runbook in automazione di Azure utilizzando l'editor di testo hello, vedere [modifica di un Runbook in automazione di Azure](automation-edit-textual-runbook.md)
