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
# <a name="running-runbooks-on-a-hybrid-runbook-worker"></a><span data-ttu-id="f64bb-103">Esecuzione di runbook in un ruolo di lavoro ibrido per runbook</span><span class="sxs-lookup"><span data-stu-id="f64bb-103">Running runbooks on a Hybrid Runbook Worker</span></span> 
<span data-ttu-id="f64bb-104">Non c'è alcuna differenza nella struttura di hello di runbook in esecuzione in automazione di Azure e quelle eseguite in un Runbook Worker ibrido.</span><span class="sxs-lookup"><span data-stu-id="f64bb-104">There is no difference in hello structure of runbooks that run in Azure Automation and those that run on a Hybrid Runbook Worker.</span></span> <span data-ttu-id="f64bb-105">I runbook che utilizzare con ogni probabilmente differisce notevolmente tuttavia poiché i runbook di destinazione di un Runbook Worker ibrido in genere la gestione delle risorse sul computer locale di hello stesso o sulle risorse nell'ambiente di hello locale in cui è distribuito, mentre i runbook in automazione di Azure è in genere gestire le risorse in hello cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="f64bb-105">Runbooks that you use with each most likely differ significantly though since runbooks targeting a Hybrid Runbook Worker typically manage resources on hello local computer itself or against resources in hello local environment where it is deployed, while runbooks in Azure Automation typically manage resources in hello Azure cloud.</span></span>

<span data-ttu-id="f64bb-106">È possibile modificare un runbook per lavoro ibridi per Runbook in automazione di Azure, ma è possibile che problemi se si tenta di tootest hello runbook nell'editor di hello.</span><span class="sxs-lookup"><span data-stu-id="f64bb-106">You can edit a runbook for Hybrid Runbook Worker in Azure Automation, but you may have difficulties if you try tootest hello runbook in hello editor.</span></span>  <span data-ttu-id="f64bb-107">i moduli di PowerShell Hello che accedono alle risorse locali hello potrebbero non essere installate nell'ambiente di automazione di Azure in questo caso, avrà esito negativo test hello.</span><span class="sxs-lookup"><span data-stu-id="f64bb-107">hello PowerShell modules that access hello local resources may not be installed in your Azure Automation environment in which case, hello test would fail.</span></span>  <span data-ttu-id="f64bb-108">Se si installa hello necessari moduli, quindi hello runbook verrà eseguito, ma non sarà in grado di tooaccess risorse locali per un test completo.</span><span class="sxs-lookup"><span data-stu-id="f64bb-108">If you do install hello required modules, then hello runbook will run, but it will not be able tooaccess local resources for a complete test.</span></span>

## <a name="starting-a-runbook-on-hybrid-runbook-worker"></a><span data-ttu-id="f64bb-109">Avvio di un runbook in un ruolo di lavoro ibrido per runbook</span><span class="sxs-lookup"><span data-stu-id="f64bb-109">Starting a runbook on Hybrid Runbook Worker</span></span>
<span data-ttu-id="f64bb-110">[avvio di un runbook in Automazione di Azure](automation-starting-a-runbook.md) illustra diversi modi in cui è possibile eseguire l'avvio dei runbook.</span><span class="sxs-lookup"><span data-stu-id="f64bb-110">[Starting a Runbook in Azure Automation](automation-starting-a-runbook.md) describes different methods for starting a runbook.</span></span>  <span data-ttu-id="f64bb-111">Runbook Worker ibrido aggiunge un **RunOn** opzione in cui è possibile specificare il nome di hello di un gruppo di Runbook Worker ibrido.</span><span class="sxs-lookup"><span data-stu-id="f64bb-111">Hybrid Runbook Worker adds a **RunOn** option where you can specify hello name of a Hybrid Runbook Worker Group.</span></span>  <span data-ttu-id="f64bb-112">Se viene specificato un gruppo, quindi runbook hello viene recuperato ed eseguito dei lavoratori hello in tale gruppo.</span><span class="sxs-lookup"><span data-stu-id="f64bb-112">If a group is specified, then hello runbook is retrieved and run by of hello workers in that group.</span></span>  <span data-ttu-id="f64bb-113">Se non si specifica l'opzione, verrà eseguito come di consueto in Automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="f64bb-113">If this option is not specified, then it is run in Azure Automation as normal.</span></span>

<span data-ttu-id="f64bb-114">Quando si avvia un runbook nel portale di Azure hello, viene visualizzata una **eseguiti** opzione che consente di selezionare **Azure** o **Worker ibrido**.</span><span class="sxs-lookup"><span data-stu-id="f64bb-114">When you start a runbook in hello Azure portal, you are presented with a **Run on** option where you can select **Azure** or **Hybrid Worker**.</span></span>  <span data-ttu-id="f64bb-115">Se si seleziona **Worker ibrido**, è quindi possibile selezionare il gruppo di hello da un elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="f64bb-115">If you select **Hybrid Worker**, then you can select hello group from a dropdown.</span></span>

<span data-ttu-id="f64bb-116">Hello utilizzare **RunOn** parametro.</span><span class="sxs-lookup"><span data-stu-id="f64bb-116">Use hello **RunOn** parameter.</span></span>  <span data-ttu-id="f64bb-117">È possibile utilizzare hello successivo comando toostart un runbook denominato Test-Runbook su un gruppo di Runbook Worker ibrido denominato MyHybridGroup utilizzando Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f64bb-117">You can use hello following command toostart a runbook named Test-Runbook on a Hybrid Runbook Worker Group named MyHybridGroup using Windows PowerShell.</span></span>

    Start-AzureRmAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Test-Runbook" -RunOn "MyHybridGroup"

> [!NOTE]
> <span data-ttu-id="f64bb-118">Hello **RunOn** toohello è stato aggiunto il parametro **Start-AzureAutomationRunbook** cmdlet nella versione 0.9.1 di Microsoft Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f64bb-118">hello **RunOn** parameter was added toohello **Start-AzureAutomationRunbook** cmdlet in version 0.9.1 of Microsoft Azure PowerShell.</span></span>  <span data-ttu-id="f64bb-119">È necessario [scaricare la versione più recente di hello](https://azure.microsoft.com/downloads/) se si dispone di una precedente installazione.</span><span class="sxs-lookup"><span data-stu-id="f64bb-119">You should [download hello latest version](https://azure.microsoft.com/downloads/) if you have an earlier one installed.</span></span>  <span data-ttu-id="f64bb-120">È necessario solo tooinstall questa versione in una workstation in cui si avvia runbook hello da Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f64bb-120">You only need tooinstall this version on a workstation where you are starting hello runbook from Windows PowerShell.</span></span>  <span data-ttu-id="f64bb-121">Non è necessario tooinstall sul computer di lavoro hello a meno che non si prevede di runbook toostart da tale computer.</span><span class="sxs-lookup"><span data-stu-id="f64bb-121">You do not need tooinstall it on hello worker computer unless you intend toostart runbooks from that computer.</span></span>  <span data-ttu-id="f64bb-122">È attualmente non può avviare un runbook in un Runbook Worker ibrido da un altro runbook, poiché ciò richiede più recente di Azure Powershell toobe installato nell'account di automazione hello.</span><span class="sxs-lookup"><span data-stu-id="f64bb-122">You cannot currently start a runbook on a Hybrid Runbook Worker from another runbook since this would require hello latest version of Azure Powershell toobe installed in your Automation account.</span></span>  <span data-ttu-id="f64bb-123">la versione più recente di Hello viene aggiornata automaticamente in automazione di Azure e automaticamente propagata non appena toohello worker.</span><span class="sxs-lookup"><span data-stu-id="f64bb-123">hello latest version is automatically updated in Azure Automation and automatically pushed down toohello workers soon.</span></span>
>
>

## <a name="runbook-permissions"></a><span data-ttu-id="f64bb-124">Autorizzazioni per i runbook</span><span class="sxs-lookup"><span data-stu-id="f64bb-124">Runbook permissions</span></span>
<span data-ttu-id="f64bb-125">I runbook in esecuzione in un Runbook Worker ibrido non è possibile utilizzare hello stesso metodo che viene in genere utilizzata per i runbook autenticazione tooAzure risorse, poiché accedono alle risorse all'esterno di Azure.</span><span class="sxs-lookup"><span data-stu-id="f64bb-125">Runbooks running on a Hybrid Runbook Worker cannot use hello same method that is typically used for runbooks authenticating tooAzure resources, since they are accessing resources outside of Azure.</span></span>  <span data-ttu-id="f64bb-126">runbook Hello possibile fornire la propria autenticazione toolocal risorse oppure è possibile specificare un tooprovide account RunAs un contesto utente per tutti i runbook.</span><span class="sxs-lookup"><span data-stu-id="f64bb-126">hello runbook can either provide its own authentication toolocal resources, or you can specify a RunAs account tooprovide a user context for all runbooks.</span></span>

### <a name="runbook-authentication"></a><span data-ttu-id="f64bb-127">Autenticazione dei runbook</span><span class="sxs-lookup"><span data-stu-id="f64bb-127">Runbook authentication</span></span>
<span data-ttu-id="f64bb-128">Per impostazione predefinita, i runbook verranno eseguiti nel contesto di hello hello locale dell'account di sistema nel computer locale hello, pertanto è necessario che specifichi le proprie tooresources di autenticazione che avranno accesso.</span><span class="sxs-lookup"><span data-stu-id="f64bb-128">By default, runbooks will run in hello context of hello local System account on hello on-premises computer, so they must provide their own authentication tooresources that they will access.</span></span>  

<span data-ttu-id="f64bb-129">È possibile utilizzare [credenziali](http://msdn.microsoft.com/library/dn940015.aspx) e [certificato](http://msdn.microsoft.com/library/dn940013.aspx) asset nel runbook con i cmdlet che consentono di toospecify credenziali in modo da poter autenticare toodifferent risorse.</span><span class="sxs-lookup"><span data-stu-id="f64bb-129">You can use [Credential](http://msdn.microsoft.com/library/dn940015.aspx) and [Certificate](http://msdn.microsoft.com/library/dn940013.aspx) assets in your runbook with cmdlets that allow you toospecify credentials so you can authenticate toodifferent resources.</span></span>  <span data-ttu-id="f64bb-130">Hello esempio seguente viene mostrata una parte di un runbook che riavvia un computer.</span><span class="sxs-lookup"><span data-stu-id="f64bb-130">hello following example shows a portion of a runbook that restarts a computer.</span></span>  <span data-ttu-id="f64bb-131">Recupera le credenziali da un nome di risorsa e hello credenziale di computer hello da un asset della variabile e quindi utilizza questi valori con il cmdlet Restart-Computer hello.</span><span class="sxs-lookup"><span data-stu-id="f64bb-131">It retrieves credentials from a credential asset and hello name of hello computer from a variable asset and then uses these values with hello Restart-Computer cmdlet.</span></span>

    $Cred = Get-AzureRmAutomationCredential -ResourceGroupName "ResourceGroup01" -Name "MyCredential"
    $Computer = Get-AzureRmAutomationVariable -ResourceGroupName "ResourceGroup01" -Name  "ComputerName"

    Restart-Computer -ComputerName $Computer -Credential $Cred

<span data-ttu-id="f64bb-132">È anche possibile sfruttare [InlineScript](automation-powershell-workflow.md#inlinescript), che consente toorun blocchi di codice in un altro computer con le credenziali specificate da hello [parametro comune PSCredential](http://technet.microsoft.com/library/jj129719.aspx).</span><span class="sxs-lookup"><span data-stu-id="f64bb-132">You can also leverage [InlineScript](automation-powershell-workflow.md#inlinescript), which  allows you toorun blocks of code on another computer with credentials specified by hello [PSCredential common parameter](http://technet.microsoft.com/library/jj129719.aspx).</span></span>

### <a name="runas-account"></a><span data-ttu-id="f64bb-133">Account RunAs</span><span class="sxs-lookup"><span data-stu-id="f64bb-133">RunAs account</span></span>
<span data-ttu-id="f64bb-134">Anziché runbook fornire la propria autenticazione toolocal risorse, è possibile specificare un **RunAs** account per un gruppo di lavoro ibrido.</span><span class="sxs-lookup"><span data-stu-id="f64bb-134">Instead of having runbooks provide their own authentication toolocal resources, you can specify a **RunAs** account for a Hybrid worker group.</span></span>  <span data-ttu-id="f64bb-135">Specificare un [asset delle credenziali](automation-credentials.md) che ha accesso alle risorse di toolocal e tutti i runbook eseguito con tali credenziali durante l'esecuzione in un Runbook Worker ibrido nel gruppo di hello.</span><span class="sxs-lookup"><span data-stu-id="f64bb-135">You specify a [credential asset](automation-credentials.md) that has access toolocal resources, and all runbooks run under these credentials when running on a Hybrid Runbook Worker in hello group.</span></span>  

<span data-ttu-id="f64bb-136">nome utente di Hello per le credenziali di hello deve essere in uno dei seguenti formati hello:</span><span class="sxs-lookup"><span data-stu-id="f64bb-136">hello user name for hello credential must be in one of hello following formats:</span></span>

* <span data-ttu-id="f64bb-137">dominio\nome utente</span><span class="sxs-lookup"><span data-stu-id="f64bb-137">domain\username</span></span>
* username@domain
* <span data-ttu-id="f64bb-138">nome utente (per computer locale di account locale toohello)</span><span class="sxs-lookup"><span data-stu-id="f64bb-138">username (for accounts local toohello on-premises computer)</span></span>

<span data-ttu-id="f64bb-139">Utilizzare hello seguendo procedure toospecify un account RunAs per un gruppo di lavoro ibrido:</span><span class="sxs-lookup"><span data-stu-id="f64bb-139">Use hello following procedure toospecify a RunAs account for a Hybrid worker group:</span></span>

1. <span data-ttu-id="f64bb-140">Creare un [asset delle credenziali](automation-credentials.md) con toolocal di accedere alle risorse.</span><span class="sxs-lookup"><span data-stu-id="f64bb-140">Create a [credential asset](automation-credentials.md) with access toolocal resources.</span></span>
2. <span data-ttu-id="f64bb-141">Aprire l'account di automazione hello in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="f64bb-141">Open hello Automation account in hello Azure portal.</span></span>
3. <span data-ttu-id="f64bb-142">Seleziona hello **gruppi di lavoro ibrido** riquadro e quindi selezionare il gruppo di hello.</span><span class="sxs-lookup"><span data-stu-id="f64bb-142">Select hello **Hybrid Worker Groups** tile, and then select hello group.</span></span>
4. <span data-ttu-id="f64bb-143">Selezionare **Tutte le impostazioni** e quindi **Impostazioni del gruppo di lavoro ibrido**.</span><span class="sxs-lookup"><span data-stu-id="f64bb-143">Select **All settings** and then **Hybrid worker group settings**.</span></span>
5. <span data-ttu-id="f64bb-144">Modifica **runas** da **predefinito** troppo**personalizzato**.</span><span class="sxs-lookup"><span data-stu-id="f64bb-144">Change **Run As** from **Default** too**Custom**.</span></span>
6. <span data-ttu-id="f64bb-145">Selezionare credenziali hello e fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="f64bb-145">Select hello credential and click **Save**.</span></span>

### <a name="automation-run-as-account"></a><span data-ttu-id="f64bb-146">Account RunAs di Automazione</span><span class="sxs-lookup"><span data-stu-id="f64bb-146">Automation Run As account</span></span>
<span data-ttu-id="f64bb-147">Come parte del processo di compilazione automatizzato per la distribuzione delle risorse in Azure, potrebbe essere necessario l'accesso locale tooon sistemi toosupport un'attività o un set di passaggi nella sequenza di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="f64bb-147">As part of your automated build process for deploying resources in Azure, you may require access tooon-premise systems toosupport a task or set of steps in your deployment sequence.</span></span>  <span data-ttu-id="f64bb-148">l'autenticazione toosupport utilizzando account RunAs hello Azure, è necessario tooinstall hello runas certificato dell'account.</span><span class="sxs-lookup"><span data-stu-id="f64bb-148">toosupport authentication against Azure using hello Run As account, you need tooinstall hello Run As account certificate.</span></span>  

<span data-ttu-id="f64bb-149">Hello seguente runbook di PowerShell, *esportazione RunAsCertificateToHybridWorker*, hello runas certificato viene esportato dall'account di automazione di Azure e scarica e importarli nell'archivio certificati del computer locale hello in un Ruoli di lavoro ibridi connessi toohello stesso account.</span><span class="sxs-lookup"><span data-stu-id="f64bb-149">hello following PowerShell runbook, *Export-RunAsCertificateToHybridWorker*, exports hello Run As certificate from your Azure Automation account and downloads and imports it into hello local machine certificate store on a Hybrid worker connected toohello same account.</span></span>  <span data-ttu-id="f64bb-150">Una volta completato questo passaggio, verifica lavoro hello può eseguire l'autenticazione utilizzando l'account RunAs hello tooAzure.</span><span class="sxs-lookup"><span data-stu-id="f64bb-150">Once that step is completed, it verifies hello worker can successfully authenticate tooAzure using hello Run As account.</span></span>

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

<span data-ttu-id="f64bb-151">Salvare hello *esportazione RunAsCertificateToHybridWorker* runbook tooyour computer con un `.ps1` estensione.</span><span class="sxs-lookup"><span data-stu-id="f64bb-151">Save hello *Export-RunAsCertificateToHybridWorker* runbook tooyour computer with a `.ps1` extension.</span></span>  <span data-ttu-id="f64bb-152">Importarlo nell'account di automazione e modificare runbook hello, modifica il valore di hello di hello variabile `$Password` con la propria password.</span><span class="sxs-lookup"><span data-stu-id="f64bb-152">Import it into your Automation account and edit hello runbook, changing hello value of hello variable `$Password` with your own password.</span></span>  <span data-ttu-id="f64bb-153">Pubblicare ed eseguire runbook hello gruppo di lavoro ibridi hello che eseguono e l'autenticazione utilizzando l'account RunAs hello runbook di destinazione.</span><span class="sxs-lookup"><span data-stu-id="f64bb-153">Publish and then run hello runbook targeting hello Hybrid Worker group that run and authenticate runbooks using hello Run As account.</span></span>  <span data-ttu-id="f64bb-154">Hello processo flusso report hello tentativo tooimport hello certificato nell'archivio del computer locale hello e segue con più righe, a seconda del numero di account di automazione è definito nella sottoscrizione e se l'autenticazione ha esito positivo.</span><span class="sxs-lookup"><span data-stu-id="f64bb-154">hello job stream reports hello attempt tooimport hello certificate into hello local machine store, and follows with multiple lines depending on how many Automation accounts are defined in your subscription and if authentication is successful.</span></span>  

## <a name="troubleshooting-runbooks-on-hybrid-runbook-worker"></a><span data-ttu-id="f64bb-155">Risoluzione dei problemi relativi ai runbook nel ruolo di lavoro ibrido per runbook</span><span class="sxs-lookup"><span data-stu-id="f64bb-155">Troubleshooting runbooks on Hybrid Runbook Worker</span></span>
<span data-ttu-id="f64bb-156">I log vengono archiviati localmente in ogni ruolo di lavoro ibrido in C:\ProgramData\Microsoft\System Center\Orchestrator\7.2\SMA\Sandboxes.</span><span class="sxs-lookup"><span data-stu-id="f64bb-156">Logs are stored locally on each hybrid worker at C:\ProgramData\Microsoft\System Center\Orchestrator\7.2\SMA\Sandboxes.</span></span>  <span data-ttu-id="f64bb-157">Ruolo di lavoro ibrido registra anche errori ed eventi nel registro eventi di Windows hello in **applicazioni e servizi Logs\Microsoft-SMA\Operational**.</span><span class="sxs-lookup"><span data-stu-id="f64bb-157">Hybrid worker also records errors and events in hello Windows event log under **Application and Services Logs\Microsoft-SMA\Operational**.</span></span>  <span data-ttu-id="f64bb-158">Gli eventi correlati toorunbooks eseguita nel ruolo di lavoro hello vengono scritti troppo**applicazioni e servizi Logs\Microsoft-Automation\Operational**.</span><span class="sxs-lookup"><span data-stu-id="f64bb-158">Events related toorunbooks executed on hello worker are written too**Application and Services Logs\Microsoft-Automation\Operational**.</span></span>  <span data-ttu-id="f64bb-159">Hello **Microsoft SMA** log include molti più eventi toohello correlati runbook processo toohello inserito hello e lavoro elaborazione del runbook hello.</span><span class="sxs-lookup"><span data-stu-id="f64bb-159">hello **Microsoft-SMA** log includes many more events related toohello runbook job pushed toohello worker and hello processing of hello runbook.</span></span>  <span data-ttu-id="f64bb-160">Durante la hello **automazione di Microsoft** registro eventi non dispone di molti eventi con dettagli assistito hello risoluzione dei problemi di esecuzione del runbook, si noterà almeno risultati hello di processo del runbook hello.</span><span class="sxs-lookup"><span data-stu-id="f64bb-160">While hello **Microsoft-Automation** event log does not have many events with details assisting with hello troubleshooting of runbook execution, you will at least find hello results of hello runbook job.</span></span>  

<span data-ttu-id="f64bb-161">[I messaggi e output di runbook](automation-runbook-output-and-messages.md) inviati tooAzure automazione da processi di lavoro ibridi soli come i processi di runbook eseguiti nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="f64bb-161">[Runbook output and messages](automation-runbook-output-and-messages.md) are sent tooAzure Automation from hybrid workers just like runbook jobs run in hello cloud.</span></span>  <span data-ttu-id="f64bb-162">È inoltre possibile abilitare hello dettagliato e flussi di stato di avanzamento hello stesso si farebbe per altri runbook.</span><span class="sxs-lookup"><span data-stu-id="f64bb-162">You can also enable hello Verbose and Progress streams hello same way you would for other runbooks.</span></span>  

<span data-ttu-id="f64bb-163">Se i runbook non vengono completate correttamente e viene visualizzato lo stato processo hello riepilogo **Suspended**, consultare Risoluzione dei problemi di articolo hello [Runbook Worker ibrido: consente di terminare un processo del runbook con lo stato Sospeso](automation-troubleshooting-hybrid-runbook-worker.md#a-runbook-job-terminates-with-a-status-of-suspended).</span><span class="sxs-lookup"><span data-stu-id="f64bb-163">If your runbooks are not completing successfully and hello job summary shows a status of **Suspended**, please review hello troubleshooting article [Hybrid Runbook Worker: A runbook job terminates with a status of Suspended](automation-troubleshooting-hybrid-runbook-worker.md#a-runbook-job-terminates-with-a-status-of-suspended).</span></span>   

## <a name="next-steps"></a><span data-ttu-id="f64bb-164">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f64bb-164">Next steps</span></span>
* <span data-ttu-id="f64bb-165">toolearn informazioni su hello diversi metodi che possono essere utilizzati toostart un runbook, vedere [avvio di un Runbook in automazione di Azure](automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="f64bb-165">toolearn more about hello different methods that can be used toostart a runbook, see [Starting a Runbook in Azure Automation](automation-starting-a-runbook.md).</span></span>  
* <span data-ttu-id="f64bb-166">toounderstand hello procedure diverse per l'utilizzo di PowerShell e flusso di lavoro PowerShell runbook in automazione di Azure utilizzando l'editor di testo hello, vedere [modifica di un Runbook in automazione di Azure](automation-edit-textual-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="f64bb-166">toounderstand hello different procedures for working with PowerShell and PowerShell Workflow runbooks in Azure Automation using hello textual editor, see [Editing a Runbook in Azure Automation](automation-edit-textual-runbook.md)</span></span>
