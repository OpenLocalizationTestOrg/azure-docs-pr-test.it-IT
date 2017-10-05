---
title: Eseguire runbook nel ruolo di lavoro ibrido per runbook di Automazione di Azure | Microsoft Docs
description: Questo articolo fornisce informazioni sull'esecuzione di runbook su computer presenti nel data center locale o in un provider di servizi cloud con il ruolo di lavoro ibrido per runbook.
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
ms.openlocfilehash: 993bc3ea480a329541ca4ae825189cdb5a2b4a8b
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/29/2017
---
# <a name="running-runbooks-on-a-hybrid-runbook-worker"></a><span data-ttu-id="1e915-103">Esecuzione di runbook in un ruolo di lavoro ibrido per runbook</span><span class="sxs-lookup"><span data-stu-id="1e915-103">Running runbooks on a Hybrid Runbook Worker</span></span> 
<span data-ttu-id="1e915-104">Non esiste alcuna differenza nella struttura dei runbook che vengono eseguiti in Automazione di Azure e di quelli eseguiti in Hybrid Runbook Workers.</span><span class="sxs-lookup"><span data-stu-id="1e915-104">There is no difference in the structure of runbooks that run in Azure Automation and those that run on a Hybrid Runbook Worker.</span></span> <span data-ttu-id="1e915-105">I runbook usati nell'uno o nell'altro caso saranno tuttavia molto diversi perché, mentre i runbook per un ruolo di lavoro ibrido per runbook gestiscono solitamente le risorse nel computer locale o all'interno di risorse nell'ambiente locale in cui sono eseguiti, i runbook in Automazione di Azure gestiscono solitamente le risorse nel cloud Azure.</span><span class="sxs-lookup"><span data-stu-id="1e915-105">Runbooks that you use with each most likely differ significantly though since runbooks targeting a Hybrid Runbook Worker typically manage resources on the local computer itself or against resources in the local environment where it is deployed, while runbooks in Azure Automation typically manage resources in the Azure cloud.</span></span>

<span data-ttu-id="1e915-106">È possibile modificare un runbook per Hybrid Runbook Workers in Automazione di Azure, ma si potrebbero incontrare difficoltà se si tenta di testare il runbook nell'editor.</span><span class="sxs-lookup"><span data-stu-id="1e915-106">You can edit a runbook for Hybrid Runbook Worker in Azure Automation, but you may have difficulties if you try to test the runbook in the editor.</span></span>  <span data-ttu-id="1e915-107">I moduli di PowerShell che accedono alle risorse locali potrebbero non essere installati nell'ambiente di Automazione di Azure e in questo caso il test avrebbe esito negativo.</span><span class="sxs-lookup"><span data-stu-id="1e915-107">The PowerShell modules that access the local resources may not be installed in your Azure Automation environment in which case, the test would fail.</span></span>  <span data-ttu-id="1e915-108">Se si sceglie di installare i moduli necessari, il runbook verrà eseguito, ma non sarà in grado di accedere alle risorse locali per un test completo.</span><span class="sxs-lookup"><span data-stu-id="1e915-108">If you do install the required modules, then the runbook will run, but it will not be able to access local resources for a complete test.</span></span>

## <a name="starting-a-runbook-on-hybrid-runbook-worker"></a><span data-ttu-id="1e915-109">Avvio di un runbook in un ruolo di lavoro ibrido per runbook</span><span class="sxs-lookup"><span data-stu-id="1e915-109">Starting a runbook on Hybrid Runbook Worker</span></span>
<span data-ttu-id="1e915-110">[avvio di un runbook in Automazione di Azure](automation-starting-a-runbook.md) illustra diversi modi in cui è possibile eseguire l'avvio dei runbook.</span><span class="sxs-lookup"><span data-stu-id="1e915-110">[Starting a Runbook in Azure Automation](automation-starting-a-runbook.md) describes different methods for starting a runbook.</span></span>  <span data-ttu-id="1e915-111">Hybrid Runbook Workers aggiunge un'opzione **RunOn** in cui è possibile specificare il nome di un gruppo di computer di lavoro runbook ibridi.</span><span class="sxs-lookup"><span data-stu-id="1e915-111">Hybrid Runbook Worker adds a **RunOn** option where you can specify the name of a Hybrid Runbook Worker Group.</span></span>  <span data-ttu-id="1e915-112">Se si specifica un gruppo, il runbook verrà recuperato ed eseguito dai computer di lavoro inclusi in tale gruppo.</span><span class="sxs-lookup"><span data-stu-id="1e915-112">If a group is specified, then the runbook is retrieved and run by of the workers in that group.</span></span>  <span data-ttu-id="1e915-113">Se non si specifica l'opzione, verrà eseguito come di consueto in Automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="1e915-113">If this option is not specified, then it is run in Azure Automation as normal.</span></span>

<span data-ttu-id="1e915-114">Quando si avvia un runbook nel portale di Azure, viene visualizzata l'opzione **Esegui in**, che consente di scegliere tra **Azure** o **Ruolo di lavoro ibrido**.</span><span class="sxs-lookup"><span data-stu-id="1e915-114">When you start a runbook in the Azure portal, you are presented with a **Run on** option where you can select **Azure** or **Hybrid Worker**.</span></span>  <span data-ttu-id="1e915-115">Se si seleziona **Computer di lavoro ibrido**, sarà quindi possibile selezionare il gruppo da un elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="1e915-115">If you select **Hybrid Worker**, then you can select the group from a dropdown.</span></span>

<span data-ttu-id="1e915-116">Usare il parametro **RunOn**.</span><span class="sxs-lookup"><span data-stu-id="1e915-116">Use the **RunOn** parameter.</span></span>  <span data-ttu-id="1e915-117">È possibile usare il comando seguente per avviare un runbook denominato Test-Runbook in un gruppo di ruoli di lavoro ibridi per runbook denominato MyHybridGroup usando Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1e915-117">You can use the following command to start a runbook named Test-Runbook on a Hybrid Runbook Worker Group named MyHybridGroup using Windows PowerShell.</span></span>

    Start-AzureRmAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Test-Runbook" -RunOn "MyHybridGroup"

> [!NOTE]
> <span data-ttu-id="1e915-118">Il parametro **RunOn** è stato aggiunto al cmdlet **Start-AzureAutomationRunbook** nella versione 0.9.1 di Microsoft Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1e915-118">The **RunOn** parameter was added to the **Start-AzureAutomationRunbook** cmdlet in version 0.9.1 of Microsoft Azure PowerShell.</span></span>  <span data-ttu-id="1e915-119">È consigliabile [scaricare la versione più recente](https://azure.microsoft.com/downloads/) se la versione installata è precedente.</span><span class="sxs-lookup"><span data-stu-id="1e915-119">You should [download the latest version](https://azure.microsoft.com/downloads/) if you have an earlier one installed.</span></span>  <span data-ttu-id="1e915-120">È sufficiente installare questa versione nella workstation in cui si avvierà il runbook da Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1e915-120">You only need to install this version on a workstation where you are starting the runbook from Windows PowerShell.</span></span>  <span data-ttu-id="1e915-121">Non è necessario installarla nel computer di lavoro, a meno che non si intenda avviare i runbook da tale computer.</span><span class="sxs-lookup"><span data-stu-id="1e915-121">You do not need to install it on the worker computer unless you intend to start runbooks from that computer.</span></span>  <span data-ttu-id="1e915-122">Non è attualmente possibile avviare un runbook in un computer di lavoro runbook ibrido da un altro runbook, in quanto nell'account di automazione dovrebbe essere installata la versione più recente di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1e915-122">You cannot currently start a runbook on a Hybrid Runbook Worker from another runbook since this would require the latest version of Azure Powershell to be installed in your Automation account.</span></span>  <span data-ttu-id="1e915-123">Tale versione viene aggiornata automaticamente in Automazione di Azure e viene inviata automaticamente tramite push ai ruoli di lavoro.</span><span class="sxs-lookup"><span data-stu-id="1e915-123">The latest version is automatically updated in Azure Automation and automatically pushed down to the workers soon.</span></span>
>
>

## <a name="runbook-permissions"></a><span data-ttu-id="1e915-124">Autorizzazioni per i runbook</span><span class="sxs-lookup"><span data-stu-id="1e915-124">Runbook permissions</span></span>
<span data-ttu-id="1e915-125">I runbook eseguiti in un ruolo di lavoro ibrido per runbook non possono usare lo stesso metodo in genere usato per l'autenticazione dei runbook per le risorse di Azure, perché accedono a risorse esterne ad Azure.</span><span class="sxs-lookup"><span data-stu-id="1e915-125">Runbooks running on a Hybrid Runbook Worker cannot use the same method that is typically used for runbooks authenticating to Azure resources, since they are accessing resources outside of Azure.</span></span>  <span data-ttu-id="1e915-126">Il runbook può fornire la propria autenticazione alle risorse locali oppure è possibile specificare un account RunAs per fornire un contesto utente per tutti i runbook.</span><span class="sxs-lookup"><span data-stu-id="1e915-126">The runbook can either provide its own authentication to local resources, or you can specify a RunAs account to provide a user context for all runbooks.</span></span>

### <a name="runbook-authentication"></a><span data-ttu-id="1e915-127">Autenticazione dei runbook</span><span class="sxs-lookup"><span data-stu-id="1e915-127">Runbook authentication</span></span>
<span data-ttu-id="1e915-128">Per impostazione predefinita, i runbook vengono eseguiti nel contesto dell'account di sistema locale nel computer locale, quindi devono autenticarsi per le risorse a cui accederanno.</span><span class="sxs-lookup"><span data-stu-id="1e915-128">By default, runbooks will run in the context of the local System account on the on-premises computer, so they must provide their own authentication to resources that they will access.</span></span>  

<span data-ttu-id="1e915-129">Nel proprio runbook è possibile usare asset di tipo [Credenziali](http://msdn.microsoft.com/library/dn940015.aspx) e [Certificato](http://msdn.microsoft.com/library/dn940013.aspx) con cmdlet che consentono di specificare le credenziali per poter eseguire l'autenticazione per risorse diverse.</span><span class="sxs-lookup"><span data-stu-id="1e915-129">You can use [Credential](http://msdn.microsoft.com/library/dn940015.aspx) and [Certificate](http://msdn.microsoft.com/library/dn940013.aspx) assets in your runbook with cmdlets that allow you to specify credentials so you can authenticate to different resources.</span></span>  <span data-ttu-id="1e915-130">L'esempio seguente illustra una parte di un runbook che riavvia un computer.</span><span class="sxs-lookup"><span data-stu-id="1e915-130">The following example shows a portion of a runbook that restarts a computer.</span></span>  <span data-ttu-id="1e915-131">Recupera le credenziali da un asset di tipo credenziale e il nome del computer da un asset di tipo variabile e quindi usa questi valori con il cmdlet Restart-Computer.</span><span class="sxs-lookup"><span data-stu-id="1e915-131">It retrieves credentials from a credential asset and the name of the computer from a variable asset and then uses these values with the Restart-Computer cmdlet.</span></span>

    $Cred = Get-AzureRmAutomationCredential -ResourceGroupName "ResourceGroup01" -Name "MyCredential"
    $Computer = Get-AzureRmAutomationVariable -ResourceGroupName "ResourceGroup01" -Name  "ComputerName"

    Restart-Computer -ComputerName $Computer -Credential $Cred

<span data-ttu-id="1e915-132">È anche possibile usare [InlineScript](automation-powershell-workflow.md#inlinescript), che consente di eseguire blocchi di codice in un altro computer con le credenziali specificate dal [parametro comune PSCredential](http://technet.microsoft.com/library/jj129719.aspx).</span><span class="sxs-lookup"><span data-stu-id="1e915-132">You can also leverage [InlineScript](automation-powershell-workflow.md#inlinescript), which  allows you to run blocks of code on another computer with credentials specified by the [PSCredential common parameter](http://technet.microsoft.com/library/jj129719.aspx).</span></span>

### <a name="runas-account"></a><span data-ttu-id="1e915-133">Account RunAs</span><span class="sxs-lookup"><span data-stu-id="1e915-133">RunAs account</span></span>
<span data-ttu-id="1e915-134">Per evitare che i runbook debbano autenticarsi per le risorse locali, è possibile specificare un account **RunAs** per un gruppo di ruoli di lavoro ibridi.</span><span class="sxs-lookup"><span data-stu-id="1e915-134">Instead of having runbooks provide their own authentication to local resources, you can specify a **RunAs** account for a Hybrid worker group.</span></span>  <span data-ttu-id="1e915-135">Specificare un [asset credenziali](automation-credentials.md) con accesso alle risorse locali. Tutti i runbook useranno queste credenziali durante l'esecuzione in un ruolo di lavoro ibrido per runbook nel gruppo.</span><span class="sxs-lookup"><span data-stu-id="1e915-135">You specify a [credential asset](automation-credentials.md) that has access to local resources, and all runbooks run under these credentials when running on a Hybrid Runbook Worker in the group.</span></span>  

<span data-ttu-id="1e915-136">Il nome utente per le credenziali deve essere in uno dei formati seguenti:</span><span class="sxs-lookup"><span data-stu-id="1e915-136">The user name for the credential must be in one of the following formats:</span></span>

* <span data-ttu-id="1e915-137">dominio\nome utente</span><span class="sxs-lookup"><span data-stu-id="1e915-137">domain\username</span></span>
* username@domain
* <span data-ttu-id="1e915-138">nome utente (per gli account locali nel computer locale)</span><span class="sxs-lookup"><span data-stu-id="1e915-138">username (for accounts local to the on-premises computer)</span></span>

<span data-ttu-id="1e915-139">Usare la procedura seguente per specificare un account RunAs per un gruppo di lavoro ibrido:</span><span class="sxs-lookup"><span data-stu-id="1e915-139">Use the following procedure to specify a RunAs account for a Hybrid worker group:</span></span>

1. <span data-ttu-id="1e915-140">Creare un [asset credenziali](automation-credentials.md) con accesso alle risorse locali.</span><span class="sxs-lookup"><span data-stu-id="1e915-140">Create a [credential asset](automation-credentials.md) with access to local resources.</span></span>
2. <span data-ttu-id="1e915-141">Nel portale di Azure aprire l'account di automazione.</span><span class="sxs-lookup"><span data-stu-id="1e915-141">Open the Automation account in the Azure portal.</span></span>
3. <span data-ttu-id="1e915-142">Selezionare il riquadro **Gruppi di ruoli di lavoro ibridi** e quindi il gruppo.</span><span class="sxs-lookup"><span data-stu-id="1e915-142">Select the **Hybrid Worker Groups** tile, and then select the group.</span></span>
4. <span data-ttu-id="1e915-143">Selezionare **Tutte le impostazioni** e quindi **Impostazioni del gruppo di lavoro ibrido**.</span><span class="sxs-lookup"><span data-stu-id="1e915-143">Select **All settings** and then **Hybrid worker group settings**.</span></span>
5. <span data-ttu-id="1e915-144">Modificare **Esegui come** da **Predefinito** a **Personalizzato**.</span><span class="sxs-lookup"><span data-stu-id="1e915-144">Change **Run As** from **Default** to **Custom**.</span></span>
6. <span data-ttu-id="1e915-145">Selezionare le credenziali e fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="1e915-145">Select the credential and click **Save**.</span></span>

### <a name="automation-run-as-account"></a><span data-ttu-id="1e915-146">Account RunAs di Automazione</span><span class="sxs-lookup"><span data-stu-id="1e915-146">Automation Run As account</span></span>
<span data-ttu-id="1e915-147">Nell'ambito del processo di compilazione automatizzato per la distribuzione di risorse in Azure, è possibile che sia necessario accedere a sistemi locali per supportare un'attività o un set di passaggi nella sequenza di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="1e915-147">As part of your automated build process for deploying resources in Azure, you may require access to on-premise systems to support a task or set of steps in your deployment sequence.</span></span>  <span data-ttu-id="1e915-148">Per supportare l'autenticazione in Azure con l'account RunAs, è necessario installare il certificato dell'account RunAs.</span><span class="sxs-lookup"><span data-stu-id="1e915-148">To support authentication against Azure using the Run As account, you need to install the Run As account certificate.</span></span>  

<span data-ttu-id="1e915-149">Il runbook di PowerShell seguente, *Export-RunAsCertificateToHybridWorker*, esporta il certificato RunAs dall'account di automazione di Azure e lo scarica e lo importa nell'archivio certificati del computer locale in un ruolo di lavoro ibrido connesso allo stesso account.</span><span class="sxs-lookup"><span data-stu-id="1e915-149">The following PowerShell runbook, *Export-RunAsCertificateToHybridWorker*, exports the Run As certificate from your Azure Automation account and downloads and imports it into the local machine certificate store on a Hybrid worker connected to the same account.</span></span>  <span data-ttu-id="1e915-150">Una volta completato questo passaggio, viene verificato che il ruolo di lavoro possa eseguire l'autenticazione in Azure usando l'account RunAs.</span><span class="sxs-lookup"><span data-stu-id="1e915-150">Once that step is completed, it verifies the worker can successfully authenticate to Azure using the Run As account.</span></span>

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
    Exports the Run As certificate from an Azure Automation account to a hybrid worker in that account. 
  
    .DESCRIPTION  
    This runbook exports the Run As certificate from an Azure Automation account to a hybrid worker in that account.
    Run this runbook in the hybrid worker where you want the certificate installed.
    This allows the use of the AzureRunAsConnection to authenticate to Azure and manage Azure resources from runbooks running in the hybrid worker.

    .EXAMPLE
    .\Export-RunAsCertificateToHybridWorker

    .NOTES
    AUTHOR: Azure Automation Team 
    LASTEDIT: 2016.10.13
    #>

    [OutputType([string])] 

    # Set the password used for this certificate
    $Password = "YourStrongPasswordForTheCert"

    # Stop on errors
    $ErrorActionPreference = 'stop'

    # Get the management certificate that will be used to make calls into Azure Service Management resources
    $RunAsCert = Get-AutomationCertificate -Name "AzureRunAsCertificate"
       
    # location to store temporary certificate in the Automation service host
    $CertPath = Join-Path $env:temp  "AzureRunAsCertificate.pfx"
   
    # Save the certificate
    $Cert = $RunAsCert.Export("pfx",$Password)
    Set-Content -Value $Cert -Path $CertPath -Force -Encoding Byte | Write-Verbose 

    Write-Output ("Importing certificate into $env:computername local machine root store from " + $CertPath)
    $SecurePassword = ConvertTo-SecureString $Password -AsPlainText -Force
    Import-PfxCertificate -FilePath $CertPath -CertStoreLocation Cert:\LocalMachine\My -Password $SecurePassword -Exportable | Write-Verbose

    # Test that authentication to Azure Resource Manager is working
    $RunAsConnection = Get-AutomationConnection -Name "AzureRunAsConnection" 
    
    Add-AzureRmAccount `
      -ServicePrincipal `
      -TenantId $RunAsConnection.TenantId `
      -ApplicationId $RunAsConnection.ApplicationId `
      -CertificateThumbprint $RunAsConnection.CertificateThumbprint | Write-Verbose

    Set-AzureRmContext -SubscriptionId $RunAsConnection.SubscriptionID | Write-Verbose

    # List automation accounts to confirm Azure Resource Manager calls are working
    Get-AzureRmAutomationAccount | Select AutomationAccountName

<span data-ttu-id="1e915-151">Salvare il runbook *Export-RunAsCertificateToHybridWorker* nel computer con un'estensione `.ps1`.</span><span class="sxs-lookup"><span data-stu-id="1e915-151">Save the *Export-RunAsCertificateToHybridWorker* runbook to your computer with a `.ps1` extension.</span></span>  <span data-ttu-id="1e915-152">Importarlo nell'account di Automazione e modificare il runbook, cambiando il valore della variabile `$Password` con quello della propria password.</span><span class="sxs-lookup"><span data-stu-id="1e915-152">Import it into your Automation account and edit the runbook, changing the value of the variable `$Password` with your own password.</span></span>  <span data-ttu-id="1e915-153">Pubblicare e quindi eseguire il runbook scegliendo come destinazione il gruppo di ruoli di lavoro ibridi che esegue e autentica i runbook usando l'account RunAs.</span><span class="sxs-lookup"><span data-stu-id="1e915-153">Publish and then run the runbook targeting the Hybrid Worker group that run and authenticate runbooks using the Run As account.</span></span>  <span data-ttu-id="1e915-154">Il flusso di processo segnala il tentativo di importare il certificato nell'archivio del computer locale e visualizza più righe a seconda del numero di account di Automazione definiti nella sottoscrizione e del fatto che l'autenticazione abbia o meno esito positivo.</span><span class="sxs-lookup"><span data-stu-id="1e915-154">The job stream reports the attempt to import the certificate into the local machine store, and follows with multiple lines depending on how many Automation accounts are defined in your subscription and if authentication is successful.</span></span>  

## <a name="troubleshooting-runbooks-on-hybrid-runbook-worker"></a><span data-ttu-id="1e915-155">Risoluzione dei problemi relativi ai runbook nel ruolo di lavoro ibrido per runbook</span><span class="sxs-lookup"><span data-stu-id="1e915-155">Troubleshooting runbooks on Hybrid Runbook Worker</span></span>
<span data-ttu-id="1e915-156">I log vengono archiviati localmente in ogni ruolo di lavoro ibrido in C:\ProgramData\Microsoft\System Center\Orchestrator\7.2\SMA\Sandboxes.</span><span class="sxs-lookup"><span data-stu-id="1e915-156">Logs are stored locally on each hybrid worker at C:\ProgramData\Microsoft\System Center\Orchestrator\7.2\SMA\Sandboxes.</span></span>  <span data-ttu-id="1e915-157">Il ruolo di lavoro ibrido registra anche errori ed eventi nel registro eventi di Windows disponibile in **Registri applicazioni e servizi\Microsoft-SMA\Operational**.</span><span class="sxs-lookup"><span data-stu-id="1e915-157">Hybrid worker also records errors and events in the Windows event log under **Application and Services Logs\Microsoft-SMA\Operational**.</span></span>  <span data-ttu-id="1e915-158">Gli eventi correlati ai runbook eseguiti nel ruolo di lavoro vengono scritti in **Registri applicazioni e servizi\Microsoft-Automation\Operational**.</span><span class="sxs-lookup"><span data-stu-id="1e915-158">Events related to runbooks executed on the worker are written to **Application and Services Logs\Microsoft-Automation\Operational**.</span></span>  <span data-ttu-id="1e915-159">Il registro **Microsoft-SMA** include molti più eventi relativi al processo del runbook inviato al ruolo di lavoro e all'elaborazione del runbook.</span><span class="sxs-lookup"><span data-stu-id="1e915-159">The **Microsoft-SMA** log includes many more events related to the runbook job pushed to the worker and the processing of the runbook.</span></span>  <span data-ttu-id="1e915-160">Sebbene il registro eventi **Microsoft-Automation** non contenga molti eventi con informazioni utili alla risoluzione di problemi relativi all'esecuzione del runbook, include almeno i risultati del processo del runbook.</span><span class="sxs-lookup"><span data-stu-id="1e915-160">While the **Microsoft-Automation** event log does not have many events with details assisting with the troubleshooting of runbook execution, you will at least find the results of the runbook job.</span></span>  

<span data-ttu-id="1e915-161">[output e i messaggi di runbook](automation-runbook-output-and-messages.md) vengono inviati ad Automazione di Azure da ruoli di lavoro ibridi nello stesso modo in cui vengono eseguiti i processi per runbook nel cloud.</span><span class="sxs-lookup"><span data-stu-id="1e915-161">[Runbook output and messages](automation-runbook-output-and-messages.md) are sent to Azure Automation from hybrid workers just like runbook jobs run in the cloud.</span></span>  <span data-ttu-id="1e915-162">È anche possibile abilitare i flussi Verbose e Progress come per qualsiasi altro runbook.</span><span class="sxs-lookup"><span data-stu-id="1e915-162">You can also enable the Verbose and Progress streams the same way you would for other runbooks.</span></span>  

<span data-ttu-id="1e915-163">Se i runbook non vengono completati correttamente e il riepilogo del processo visualizza lo stato **Sospeso**, vedere l'articolo sulla risoluzione dei problemi [Ruolo di lavoro ibrido per runbook: un processo runbook termina con lo stato Sospeso](automation-troubleshooting-hybrid-runbook-worker.md#a-runbook-job-terminates-with-a-status-of-suspended).</span><span class="sxs-lookup"><span data-stu-id="1e915-163">If your runbooks are not completing successfully and the job summary shows a status of **Suspended**, please review the troubleshooting article [Hybrid Runbook Worker: A runbook job terminates with a status of Suspended](automation-troubleshooting-hybrid-runbook-worker.md#a-runbook-job-terminates-with-a-status-of-suspended).</span></span>   

## <a name="next-steps"></a><span data-ttu-id="1e915-164">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1e915-164">Next steps</span></span>
* <span data-ttu-id="1e915-165">Per altre informazioni sui vari modi per avviare un runbook, vedere [Avvio di un runbook in Automazione di Azure](automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="1e915-165">To learn more about the different methods that can be used to start a runbook, see [Starting a Runbook in Azure Automation](automation-starting-a-runbook.md).</span></span>  
* <span data-ttu-id="1e915-166">Per comprendere le diverse procedure per l'uso di PowerShell e dei runbook del flusso di lavoro di PowerShell in Automazione di Azure con l'editor di testo, vedere [Modifica di runbook testuali in Automazione di Azure](automation-edit-textual-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="1e915-166">To understand the different procedures for working with PowerShell and PowerShell Workflow runbooks in Azure Automation using the textual editor, see [Editing a Runbook in Azure Automation](automation-edit-textual-runbook.md)</span></span>