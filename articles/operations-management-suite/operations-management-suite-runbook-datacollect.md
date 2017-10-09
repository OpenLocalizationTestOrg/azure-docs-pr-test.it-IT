---
title: aaaCollecting dati Analitica Log con un runbook in automazione di Azure | Documenti Microsoft
description: Esercitazione dettagliata che descrive come creare un runbook nei dati di automazione di Azure toocollect nel repository OMS hello per l'analisi da Analitica di Log.
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.assetid: a831fd90-3f55-423b-8b20-ccbaaac2ca75
ms.service: operations-management-suite
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2017
ms.author: bwren
ms.openlocfilehash: e644dc3ef20fb1e930cae02e0fd44ccca31dc13d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="collect-data-in-log-analytics-with-an-azure-automation-runbook"></a><span data-ttu-id="bc211-103">Raccogliere dati in Log Analytics con un runbook di Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="bc211-103">Collect data in Log Analytics with an Azure Automation runbook</span></span>
<span data-ttu-id="bc211-104">È possibile raccogliere una quantità significativa di dati in Log Analytics da una serie di origini, tra cui [origini dati](../log-analytics/log-analytics-data-sources.md) negli agenti e [dati raccolti da Azure](../log-analytics/log-analytics-azure-storage.md).</span><span class="sxs-lookup"><span data-stu-id="bc211-104">You can collect a significant amount of data in Log Analytics from a variety of sources including [data sources](../log-analytics/log-analytics-data-sources.md) on agents and also [data collected from Azure](../log-analytics/log-analytics-azure-storage.md).</span></span>  <span data-ttu-id="bc211-105">Esistono un scenari, sebbene in cui è necessario toocollect dati che non sia accessibile tramite queste origini standard.</span><span class="sxs-lookup"><span data-stu-id="bc211-105">There are a scenarios though where you need toocollect data that isn't accessible through these standard sources.</span></span>  <span data-ttu-id="bc211-106">In questi casi, è possibile utilizzare hello [API dell'agente di raccolta dati di HTTP](../log-analytics/log-analytics-data-collector-api.md) toowrite dati tooLog Analitica da qualsiasi client dell'API REST.</span><span class="sxs-lookup"><span data-stu-id="bc211-106">In these cases, you can use hello [HTTP Data Collector API](../log-analytics/log-analytics-data-collector-api.md) toowrite data tooLog Analytics from any REST API client.</span></span>  <span data-ttu-id="bc211-107">Un esempio di metodo comuni tooperform questa raccolta dati utilizza un runbook in automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="bc211-107">A common method tooperform this data collection is using a runbook in Azure Automation.</span></span>   

<span data-ttu-id="bc211-108">Questa esercitazione viene descritto il processo di hello per la creazione e pianificazione di un runbook in automazione di Azure toowrite dati tooLog Analitica.</span><span class="sxs-lookup"><span data-stu-id="bc211-108">This tutorial walks through hello process for creating and scheduling a runbook in Azure Automation toowrite data tooLog Analytics.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="bc211-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="bc211-109">Prerequisites</span></span>
<span data-ttu-id="bc211-110">Questo scenario richiede hello seguenti risorse configurate nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="bc211-110">This scenario requires hello following resources configured in your Azure subscription.</span></span>  <span data-ttu-id="bc211-111">Per entrambe è possibile usare un account gratuito.</span><span class="sxs-lookup"><span data-stu-id="bc211-111">Both can be a free account.</span></span>

- <span data-ttu-id="bc211-112">[Area di lavoro di Log Analytics](../log-analytics/log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="bc211-112">[Log Analytics workspace](../log-analytics/log-analytics-get-started.md).</span></span>
- <span data-ttu-id="bc211-113">[Account di automazione di Azure](../automation/automation-offering-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="bc211-113">[Azure automation account](../automation/automation-offering-get-started.md).</span></span>

## <a name="overview-of-scenario"></a><span data-ttu-id="bc211-114">Panoramica dello scenario</span><span class="sxs-lookup"><span data-stu-id="bc211-114">Overview of scenario</span></span>
<span data-ttu-id="bc211-115">Per questa esercitazione si scriverà un runbook che raccoglie informazioni sui processi di automazione.</span><span class="sxs-lookup"><span data-stu-id="bc211-115">For this tutorial, you'll write a runbook that collects information about Automation jobs.</span></span>  <span data-ttu-id="bc211-116">I runbook in automazione di Azure sono implementati con PowerShell, pertanto si inizierà da scrittura e il test di uno script nell'editor di automazione di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="bc211-116">Runbooks in Azure Automation are implemented with PowerShell, so you'll start by writing and testing a script in hello Azure Automation editor.</span></span>  <span data-ttu-id="bc211-117">Dopo aver verificato che si raccolgono informazioni hello necessarie, verranno scrivere tale tooLog dati Analitica e verificare il tipo di dati personalizzato hello.</span><span class="sxs-lookup"><span data-stu-id="bc211-117">Once you verify that you're collecting hello required information, you'll write that data tooLog Analytics and verify hello custom data type.</span></span>  <span data-ttu-id="bc211-118">Infine, si creerà un runbook di hello toostart pianificazione a intervalli regolari.</span><span class="sxs-lookup"><span data-stu-id="bc211-118">Finally, you'll create a schedule toostart hello runbook at regular intervals.</span></span>

> [!NOTE]
> <span data-ttu-id="bc211-119">È possibile configurare l'automazione di Azure toosend processo informazioni tooLog Analitica senza questo runbook.</span><span class="sxs-lookup"><span data-stu-id="bc211-119">You can configure Azure Automation toosend job information tooLog Analytics without this runbook.</span></span>  <span data-ttu-id="bc211-120">Questo scenario è principalmente esercitazione di hello toosupport utilizzati e si consiglia di inviare hello tooa test area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="bc211-120">This scenario is primarily used toosupport hello tutorial, and it's recommended that you send hello data tooa test workspace.</span></span>  


## <a name="1-install-data-collector-api-module"></a><span data-ttu-id="bc211-121">1. Installare il modulo dell'API di raccolta dati</span><span class="sxs-lookup"><span data-stu-id="bc211-121">1. Install Data Collector API module</span></span>
<span data-ttu-id="bc211-122">Ogni [richiesta dall'API dell'agente di raccolta dati di HTTP hello](../log-analytics/log-analytics-data-collector-api.md#create-a-request) deve essere formattato in modo appropriato e includere un'intestazione di autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="bc211-122">Every [request from hello HTTP Data Collector API](../log-analytics/log-analytics-data-collector-api.md#create-a-request) must be formatted appropriately and include an authorization header.</span></span>  <span data-ttu-id="bc211-123">È possibile farlo nel runbook, ma è possibile ridurre la quantità hello del codice necessaria tramite un modulo che semplifica questo processo.</span><span class="sxs-lookup"><span data-stu-id="bc211-123">You can do this in your runbook, but you can reduce hello amount of code required by using a module that simplifies this process.</span></span>  <span data-ttu-id="bc211-124">È un modulo che è possibile utilizzare [OMSIngestionAPI modulo](https://www.powershellgallery.com/packages/OMSIngestionAPI) in PowerShell Gallery hello.</span><span class="sxs-lookup"><span data-stu-id="bc211-124">One module that you can use is [OMSIngestionAPI module](https://www.powershellgallery.com/packages/OMSIngestionAPI) in hello PowerShell Gallery.</span></span>

<span data-ttu-id="bc211-125">toouse un [modulo](../automation/automation-integration-modules.md) in un runbook, deve essere installato nell'account di automazione.</span><span class="sxs-lookup"><span data-stu-id="bc211-125">toouse a [module](../automation/automation-integration-modules.md) in a runbook, it must be installed in your Automation account.</span></span>  <span data-ttu-id="bc211-126">Qualsiasi runbook in hello stesso account può quindi utilizzare hello funzioni nel modulo hello.</span><span class="sxs-lookup"><span data-stu-id="bc211-126">Any runbook in hello same account can then use hello functions in hello module.</span></span>  <span data-ttu-id="bc211-127">È possibile installare un nuovo modulo selezionando **Asset** > **Moduli** > **Aggiungi un modulo** nell'account di Automazione.</span><span class="sxs-lookup"><span data-stu-id="bc211-127">You can install a new module by selecting **Assets** > **Modules** > **Add a module** in your Automation account.</span></span>  

<span data-ttu-id="bc211-128">Hello PowerShell Gallery tuttavia offre un toodeploy rapide un modulo direttamente l'account di automazione tooyour pertanto è possibile utilizzare questa opzione per questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="bc211-128">hello PowerShell Gallery though gives you a quick option toodeploy a module directly tooyour automation account so you can use that option for this tutorial.</span></span>  

![Modulo OMSIngestionAPI](media/operations-management-suite-runbook-datacollect/OMSIngestionAPI.png)

1. <span data-ttu-id="bc211-130">Andare troppo[PowerShell Gallery](https://www.powershellgallery.com/).</span><span class="sxs-lookup"><span data-stu-id="bc211-130">Go too[PowerShell Gallery](https://www.powershellgallery.com/).</span></span>
2. <span data-ttu-id="bc211-131">Cercare **OMSIngestionAPI**.</span><span class="sxs-lookup"><span data-stu-id="bc211-131">Search for **OMSIngestionAPI**.</span></span>
3. <span data-ttu-id="bc211-132">Fare clic su hello **distribuire tooAzure automazione** pulsante.</span><span class="sxs-lookup"><span data-stu-id="bc211-132">Click on hello **Deploy tooAzure Automation** button.</span></span>
4. <span data-ttu-id="bc211-133">Selezionare l'account di automazione e fare clic su **OK** modulo hello tooinstall.</span><span class="sxs-lookup"><span data-stu-id="bc211-133">Select your automation account and click **OK** tooinstall hello module.</span></span>


## <a name="2-create-automation-variables"></a><span data-ttu-id="bc211-134">2. Creare variabili di Automazione</span><span class="sxs-lookup"><span data-stu-id="bc211-134">2. Create Automation variables</span></span>
<span data-ttu-id="bc211-135">Le [variabili di Automazione](..\automation\automation-variables.md) contengono valori che possono essere usati da tutti i runbook presenti nell'account di Automazione.</span><span class="sxs-lookup"><span data-stu-id="bc211-135">[Automation variables](..\automation\automation-variables.md) hold values that can be used by all runbooks in your Automation account.</span></span>  <span data-ttu-id="bc211-136">Rendono i runbook più flessibile, consentendo toochange questi valori senza dover modificare hello runbook effettivo.</span><span class="sxs-lookup"><span data-stu-id="bc211-136">They make runbooks more flexible by allowing you toochange these values without editing hello actual runbook.</span></span> <span data-ttu-id="bc211-137">Ogni richiesta da hello API dell'agente di raccolta dati di HTTP richiede hello ID e la chiave dell'area di lavoro OMS hello e gli asset variabili sono toostore ideale queste informazioni.</span><span class="sxs-lookup"><span data-stu-id="bc211-137">Every request from hello HTTP Data Collector API requires hello ID and key of hello OMS workspace, and variable assets are ideal toostore this information.</span></span>  

![variables](media/operations-management-suite-runbook-datacollect/variables.png)

1. <span data-ttu-id="bc211-139">Nel portale di Azure hello, passare tooyour account di automazione.</span><span class="sxs-lookup"><span data-stu-id="bc211-139">In hello Azure portal, navigate tooyour Automation account.</span></span>
2. <span data-ttu-id="bc211-140">Selezionare **Variabili** in **Risorse condivise**.</span><span class="sxs-lookup"><span data-stu-id="bc211-140">Select **Variables** under **Shared Resources**.</span></span>
2. <span data-ttu-id="bc211-141">Fare clic su **aggiungere una variabile** e creare due variabili hello hello nella tabella seguente.</span><span class="sxs-lookup"><span data-stu-id="bc211-141">Click **Add a variable** and create hello two variables in hello following table.</span></span>

| <span data-ttu-id="bc211-142">Proprietà</span><span class="sxs-lookup"><span data-stu-id="bc211-142">Property</span></span> | <span data-ttu-id="bc211-143">Valore ID area di lavoro</span><span class="sxs-lookup"><span data-stu-id="bc211-143">Workspace ID Value</span></span> | <span data-ttu-id="bc211-144">Valore chiave area di lavoro</span><span class="sxs-lookup"><span data-stu-id="bc211-144">Workspace Key Value</span></span> |
|:--|:--|:--|
| <span data-ttu-id="bc211-145">Nome</span><span class="sxs-lookup"><span data-stu-id="bc211-145">Name</span></span> | <span data-ttu-id="bc211-146">WorkspaceId</span><span class="sxs-lookup"><span data-stu-id="bc211-146">WorkspaceId</span></span> | <span data-ttu-id="bc211-147">WorkspaceKey</span><span class="sxs-lookup"><span data-stu-id="bc211-147">WorkspaceKey</span></span> |
| <span data-ttu-id="bc211-148">Tipo</span><span class="sxs-lookup"><span data-stu-id="bc211-148">Type</span></span> | <span data-ttu-id="bc211-149">String</span><span class="sxs-lookup"><span data-stu-id="bc211-149">String</span></span> | <span data-ttu-id="bc211-150">String</span><span class="sxs-lookup"><span data-stu-id="bc211-150">String</span></span> |
| <span data-ttu-id="bc211-151">Valore</span><span class="sxs-lookup"><span data-stu-id="bc211-151">Value</span></span> | <span data-ttu-id="bc211-152">Incollare in hello ID area di lavoro dell'area di lavoro Log Analitica.</span><span class="sxs-lookup"><span data-stu-id="bc211-152">Paste in hello Workspace ID of your Log Analytics workspace.</span></span> | <span data-ttu-id="bc211-153">Incollare con hello primario o secondario chiave dell'area di lavoro Log Analitica.</span><span class="sxs-lookup"><span data-stu-id="bc211-153">Paste in with hello Primary or Secondary Key of your Log Analytics workspace.</span></span> |
| <span data-ttu-id="bc211-154">Crittografato</span><span class="sxs-lookup"><span data-stu-id="bc211-154">Encrypted</span></span> | <span data-ttu-id="bc211-155">No</span><span class="sxs-lookup"><span data-stu-id="bc211-155">No</span></span> | <span data-ttu-id="bc211-156">Sì</span><span class="sxs-lookup"><span data-stu-id="bc211-156">Yes</span></span> |



## <a name="3-create-runbook"></a><span data-ttu-id="bc211-157">3. Creare un runbook</span><span class="sxs-lookup"><span data-stu-id="bc211-157">3. Create runbook</span></span>

<span data-ttu-id="bc211-158">Automazione di Azure offre un editor nel portale di hello in cui è possibile modificare e testare il runbook.</span><span class="sxs-lookup"><span data-stu-id="bc211-158">Azure Automation has an editor in hello portal where you can edit and test your runbook.</span></span>  <span data-ttu-id="bc211-159">Si dispone di hello opzione toouse hello script editor toowork con [PowerShell direttamente](../automation/automation-edit-textual-runbook.md) o [creare un runbook grafico](../automation/automation-graphical-authoring-intro.md).</span><span class="sxs-lookup"><span data-stu-id="bc211-159">You have hello option toouse hello script editor toowork with [PowerShell directly](../automation/automation-edit-textual-runbook.md) or [create a graphical runbook](../automation/automation-graphical-authoring-intro.md).</span></span>  <span data-ttu-id="bc211-160">Per questa esercitazione si userà uno script di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bc211-160">For this tutorial, you will work with a PowerShell script.</span></span> 

![Modificare il runbook](media/operations-management-suite-runbook-datacollect/edit-runbook.png)

1. <span data-ttu-id="bc211-162">Passare tooyour account di automazione.</span><span class="sxs-lookup"><span data-stu-id="bc211-162">Navigate tooyour Automation account.</span></span>  
2. <span data-ttu-id="bc211-163">Fare clic su **Runbook** > **Aggiungi runbook** > **Crea un nuovo runbook**.</span><span class="sxs-lookup"><span data-stu-id="bc211-163">Click **Runbooks** > **Add a runbook** > **Create a new runbook**.</span></span>
3. <span data-ttu-id="bc211-164">Per il nome del runbook hello, digitare **raccolta processi di automazione**.</span><span class="sxs-lookup"><span data-stu-id="bc211-164">For hello runbook name, type **Collect-Automation-jobs**.</span></span>  <span data-ttu-id="bc211-165">Tipo di runbook hello selezionare **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="bc211-165">For hello runbook type, select **PowerShell**.</span></span>
4. <span data-ttu-id="bc211-166">Fare clic su **crea** toocreate hello runbook e avviare hello dell'editor.</span><span class="sxs-lookup"><span data-stu-id="bc211-166">Click **Create** toocreate hello runbook and start hello editor.</span></span>
5. <span data-ttu-id="bc211-167">Copiare e incollare hello seguente codice all'interno di hello runbook.</span><span class="sxs-lookup"><span data-stu-id="bc211-167">Copy and paste hello following code into hello runbook.</span></span>  <span data-ttu-id="bc211-168">Per una spiegazione del codice hello, vedere toohello commenti nello script hello.</span><span class="sxs-lookup"><span data-stu-id="bc211-168">Refer toohello comments in hello script for explanation of hello code.</span></span>
    
        # Get information required for hello automation account from parameter values when hello runbook is started.
        Param
        (
            [Parameter(Mandatory = $True)]
            [string]$resourceGroupName,
            [Parameter(Mandatory = $True)]
            [string]$automationAccountName
        )
        
        # Authenticate toohello Automation account using hello Azure connection created when hello Automation account was created.
        # Code copied from hello runbook AzureAutomationTutorial.
        $connectionName = "AzureRunAsConnection"
        $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         
        Add-AzureRmAccount `
            -ServicePrincipal `
            -TenantId $servicePrincipalConnection.TenantId `
            -ApplicationId $servicePrincipalConnection.ApplicationId `
            -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint 
        
        # Set hello $VerbosePreference variable so that we get verbose output in test environment.
        $VerbosePreference = "Continue"
        
        # Get information required for Log Analytics workspace from Automation variables.
        $customerId = Get-AutomationVariable -Name 'WorkspaceID'
        $sharedKey = Get-AutomationVariable -Name 'WorkspaceKey'
        
        # Set hello name of hello record type.
        $logType = "AutomationJob"
        
        # Get hello jobs from hello past hour.
        $jobs = Get-AzureRmAutomationJob -ResourceGroupName $resourceGroupName -AutomationAccountName $automationAccountName -StartTime (Get-Date).AddHours(-1)
        
        if ($jobs -ne $null) {
            # Convert hello job data toojson
            $body = $jobs | ConvertTo-Json
        
            # Write hello body tooverbose output so we can inspect it if verbose logging is on for hello runbook.
            Write-Verbose $body
        
            # Send hello data tooLog Analytics.
            Send-OMSAPIIngestionFile -customerId $customerId -sharedKey $sharedKey -body $body -logType $logType -TimeStampField CreationTime
        }


## <a name="4-test-runbook"></a><span data-ttu-id="bc211-169">4. Testare il runbook</span><span class="sxs-lookup"><span data-stu-id="bc211-169">4. Test runbook</span></span>
<span data-ttu-id="bc211-170">Automazione di Azure include un ambiente troppo[testare il runbook](../automation/automation-testing-runbook.md) prima della pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="bc211-170">Azure Automation includes an environment too[test your runbook](../automation/automation-testing-runbook.md) before you publish it.</span></span>  <span data-ttu-id="bc211-171">È possibile controllare i dati di hello raccolti dal runbook hello e verificare che la scrittura tooLog Analitica come previsto prima di pubblicarlo tooproduction.</span><span class="sxs-lookup"><span data-stu-id="bc211-171">You can inspect hello data collected by hello runbook and verify that it writes tooLog Analytics as expected before publishing it tooproduction.</span></span> 
 
![Testare il runbook](media/operations-management-suite-runbook-datacollect/test-runbook.png)

6. <span data-ttu-id="bc211-173">Fare clic su **salvare** toosave hello runbook.</span><span class="sxs-lookup"><span data-stu-id="bc211-173">Click **Save** toosave hello runbook.</span></span>
1. <span data-ttu-id="bc211-174">Fare clic su **riquadro Test** tooopen hello runbook nell'ambiente di test hello.</span><span class="sxs-lookup"><span data-stu-id="bc211-174">Click **Test pane** tooopen hello runbook in hello test environment.</span></span>
3. <span data-ttu-id="bc211-175">Poiché il runbook include parametri, è richiesta tooenter valori.</span><span class="sxs-lookup"><span data-stu-id="bc211-175">Since your runbook has parameters, you're prompted tooenter values for them.</span></span>  <span data-ttu-id="bc211-176">Immettere il nome di hello hello del gruppo di risorse e automazione hello conto che le informazioni di processo corso toocollect da.</span><span class="sxs-lookup"><span data-stu-id="bc211-176">Enter hello name of hello resource group and hello automation account that your going toocollect job information from.</span></span>
4. <span data-ttu-id="bc211-177">Fare clic su **avviare** toohello avviare runbook hello.</span><span class="sxs-lookup"><span data-stu-id="bc211-177">Click **Start** toohello start hello runbook.</span></span>
3. <span data-ttu-id="bc211-178">Hello runbook verrà avviato con uno stato di **in coda** prima che diventi troppo**esecuzione**.</span><span class="sxs-lookup"><span data-stu-id="bc211-178">hello runbook will start with a status of **Queued** before it goes too**Running**.</span></span>  
3. <span data-ttu-id="bc211-179">Hello runbook deve essere visualizzato un output dettagliato con i processi di hello raccolti in formato json.</span><span class="sxs-lookup"><span data-stu-id="bc211-179">hello runbook should display verbose output with hello jobs collected in json format.</span></span>  <span data-ttu-id="bc211-180">Se non è elencato alcun processo, quindi non si è verificato alcun processi creati nell'account di automazione hello in hello ultima ora.</span><span class="sxs-lookup"><span data-stu-id="bc211-180">If no jobs are listed, then there may have been no jobs created in hello automation account in hello last hour.</span></span>  <span data-ttu-id="bc211-181">Provare ad avviare qualsiasi runbook nell'account di automazione hello e quindi eseguire di nuovo il test di hello.</span><span class="sxs-lookup"><span data-stu-id="bc211-181">Try starting any runbook in hello automation account and then perform hello test again.</span></span>
4. <span data-ttu-id="bc211-182">Verificare che output di hello non mostra che tutti gli errori nella hello post tooLog comando Analitica.</span><span class="sxs-lookup"><span data-stu-id="bc211-182">Ensure that hello output doesn't show any errors in hello post command tooLog Analytics.</span></span>  <span data-ttu-id="bc211-183">È necessario disporre di seguito toohello simile messaggio.</span><span class="sxs-lookup"><span data-stu-id="bc211-183">You should have a message similar toohello following.</span></span>

    ![Output del comando POST](media/operations-management-suite-runbook-datacollect/post-output.png)

## <a name="5-verify-records-in-log-analytics"></a><span data-ttu-id="bc211-185">5. Verificare i record in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="bc211-185">5. Verify records in Log Analytics</span></span>
<span data-ttu-id="bc211-186">Una volta hello runbook è stata completata nel test e si è verificato che output di hello è stata ricevuta correttamente, è possibile verificare che i record di hello siano stati creati utilizzando un [ricerca dei registri di Log Analitica](../log-analytics/log-analytics-log-searches.md).</span><span class="sxs-lookup"><span data-stu-id="bc211-186">Once hello runbook has completed in test, and you verified that hello output was successfully received, you can verify that hello records were created using a [log search in Log Analytics](../log-analytics/log-analytics-log-searches.md).</span></span>

![Output del log](media/operations-management-suite-runbook-datacollect/log-output.png)

1. <span data-ttu-id="bc211-188">Nel portale di Azure hello, selezionare l'area di lavoro Log Analitica.</span><span class="sxs-lookup"><span data-stu-id="bc211-188">In hello Azure portal, select your Log Analytics workspace.</span></span>
2. <span data-ttu-id="bc211-189">Fare clic su **Ricerca log**.</span><span class="sxs-lookup"><span data-stu-id="bc211-189">Click on **Log Search**.</span></span>
3. <span data-ttu-id="bc211-190">Hello tipo comando seguente `Type=AutomationJob_CL` e fare clic sul pulsante ricerca hello.</span><span class="sxs-lookup"><span data-stu-id="bc211-190">Type hello following command `Type=AutomationJob_CL` and click hello search button.</span></span> <span data-ttu-id="bc211-191">Si noti che tipo di record hello include _CL che non è specificato nello script hello.</span><span class="sxs-lookup"><span data-stu-id="bc211-191">Note that hello record type includes _CL that isn't specified in hello script.</span></span>  <span data-ttu-id="bc211-192">Tale suffisso viene automaticamente aggiunto toohello log tipo tooindicate che è un tipo di log personalizzato.</span><span class="sxs-lookup"><span data-stu-id="bc211-192">That suffix is automatically appended toohello log type tooindicate that it's a custom log type.</span></span>
4. <span data-ttu-id="bc211-193">Verrà visualizzato uno o più record restituito che indica che runbook hello funzioni come previsto.</span><span class="sxs-lookup"><span data-stu-id="bc211-193">You should see one or more records returned indicating that hello runbook is working as expected.</span></span>


## <a name="6-publish-hello-runbook"></a><span data-ttu-id="bc211-194">6. Pubblicare il runbook hello</span><span class="sxs-lookup"><span data-stu-id="bc211-194">6. Publish hello runbook</span></span>
<span data-ttu-id="bc211-195">Dopo aver verificato che runbook hello funzioni correttamente, è necessario toopublish, in modo da eseguire nell'ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="bc211-195">Once you've verified that hello runbook is working correctly, you need toopublish it so you can run it in production.</span></span>  <span data-ttu-id="bc211-196">È possibile continuare tooedit e testare il runbook hello senza modificare la versione pubblicata di hello.</span><span class="sxs-lookup"><span data-stu-id="bc211-196">You can continue tooedit and test hello runbook without modifying hello published version.</span></span>  

![Pubblicare il runbook](media/operations-management-suite-runbook-datacollect/publish-runbook.png)

1. <span data-ttu-id="bc211-198">Restituire tooyour account di automazione.</span><span class="sxs-lookup"><span data-stu-id="bc211-198">Return tooyour automation account.</span></span>
2. <span data-ttu-id="bc211-199">Fare clic su **Runbook** e selezionare **Collect-Automation-jobs**.</span><span class="sxs-lookup"><span data-stu-id="bc211-199">Click on **Runbooks** and select **Collect-Automation-jobs**.</span></span>
3. <span data-ttu-id="bc211-200">Fare clic su **Modifica** e quindi su **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="bc211-200">Click **Edit** and then **Publish**.</span></span>
4. <span data-ttu-id="bc211-201">Fare clic su **Sì** quando tooverify frequenti che si desidera toooverwrite hello precedentemente pubblicata versione.</span><span class="sxs-lookup"><span data-stu-id="bc211-201">Click **Yes** when asked tooverify that you want toooverwrite hello previously published version.</span></span>

## <a name="7-set-logging-options"></a><span data-ttu-id="bc211-202">7. Impostare le opzioni di registrazione</span><span class="sxs-lookup"><span data-stu-id="bc211-202">7. Set logging options</span></span> 
<span data-ttu-id="bc211-203">Per test, è stato in grado di tooview [output dettagliato](../automation/automation-runbook-output-and-messages.md#message-streams) perché è impostata la variabile hello $VerbosePreference nello script hello.</span><span class="sxs-lookup"><span data-stu-id="bc211-203">For test, you were able tooview [verbose output](../automation/automation-runbook-output-and-messages.md#message-streams) because you set hello $VerbosePreference variable in hello script.</span></span>  <span data-ttu-id="bc211-204">Per la produzione, le proprietà di registrazione di hello tooset per runbook hello è necessario se si desidera tooview un output dettagliato.</span><span class="sxs-lookup"><span data-stu-id="bc211-204">For production, you need tooset hello logging properties for hello runbook if you want tooview verbose output.</span></span>  <span data-ttu-id="bc211-205">Per i runbook hello utilizzati in questa esercitazione, verrà visualizzato i dati json hello inviati tooLog Analitica.</span><span class="sxs-lookup"><span data-stu-id="bc211-205">For hello runbook used in this tutorial, this will display hello json data being sent tooLog Analytics.</span></span>

![Registrazione e traccia](media/operations-management-suite-runbook-datacollect/logging.png)

1. <span data-ttu-id="bc211-207">Selezionare la proprietà hello per il runbook **registrazione e traccia** in **delle impostazioni dei Runbook**.</span><span class="sxs-lookup"><span data-stu-id="bc211-207">In hello properties for your runbook select **Logging and tracing** under **Runbook Settings**.</span></span>
2. <span data-ttu-id="bc211-208">Modifica dell'impostazione di hello per **registrazione dei record dettagliati** troppo**su**.</span><span class="sxs-lookup"><span data-stu-id="bc211-208">Change hello setting for **Log verbose records** too**On**.</span></span>
3. <span data-ttu-id="bc211-209">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="bc211-209">Click **Save**.</span></span>

## <a name="8-schedule-runbook"></a><span data-ttu-id="bc211-210">8. Pianificare il runbook</span><span class="sxs-lookup"><span data-stu-id="bc211-210">8. Schedule runbook</span></span>
<span data-ttu-id="bc211-211">più comuni toostart modo un runbook che raccoglie i dati di monitoraggio Hello è tooschedule è toorun automaticamente.</span><span class="sxs-lookup"><span data-stu-id="bc211-211">hello most common way toostart a runbook that collects monitoring data is tooschedule it toorun automatically.</span></span>  <span data-ttu-id="bc211-212">Questo scopo è la creazione di un [pianificazione in automazione di Azure](../automation/automation-schedules.md) e collegarlo tooyour runbook.</span><span class="sxs-lookup"><span data-stu-id="bc211-212">You do this by creating a [schedule in Azure Automation](../automation/automation-schedules.md) and attaching it tooyour runbook.</span></span>

![Pianificare il runbook](media/operations-management-suite-runbook-datacollect/schedule-runbook.png)

1. <span data-ttu-id="bc211-214">Nelle proprietà hello runbook, selezionare **pianificazioni** in **risorse**.</span><span class="sxs-lookup"><span data-stu-id="bc211-214">In hello properties for your runbook, select **Schedules** under **Resources**.</span></span>
2. <span data-ttu-id="bc211-215">Fare clic su **aggiungere una pianificazione** > **collega un runbook tooyour pianificazione** > **creare una nuova pianificazione**.</span><span class="sxs-lookup"><span data-stu-id="bc211-215">Click **Add a schedule** > **Link a schedule tooyour runbook** > **Create a new schedule**.</span></span>
5. <span data-ttu-id="bc211-216">Tipo di hello seguenti valori per la pianificazione hello e fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="bc211-216">Type in hello following values for hello schedule and click **Create**.</span></span>

| <span data-ttu-id="bc211-217">Proprietà</span><span class="sxs-lookup"><span data-stu-id="bc211-217">Property</span></span> | <span data-ttu-id="bc211-218">Valore</span><span class="sxs-lookup"><span data-stu-id="bc211-218">Value</span></span> |
|:--|:--|
| <span data-ttu-id="bc211-219">Nome</span><span class="sxs-lookup"><span data-stu-id="bc211-219">Name</span></span> | <span data-ttu-id="bc211-220">AutomationJobs-Hourly</span><span class="sxs-lookup"><span data-stu-id="bc211-220">AutomationJobs-Hourly</span></span> |
| <span data-ttu-id="bc211-221">Inizia</span><span class="sxs-lookup"><span data-stu-id="bc211-221">Starts</span></span> | <span data-ttu-id="bc211-222">Selezionare qualsiasi tempo di almeno 5 minuti precedenti hello ora corrente.</span><span class="sxs-lookup"><span data-stu-id="bc211-222">Select any time at least 5 minutes past hello current time.</span></span> |
| <span data-ttu-id="bc211-223">Ricorrenza</span><span class="sxs-lookup"><span data-stu-id="bc211-223">Recurrence</span></span> | <span data-ttu-id="bc211-224">Ricorrente</span><span class="sxs-lookup"><span data-stu-id="bc211-224">Recurring</span></span> |
| <span data-ttu-id="bc211-225">Ricorre ogni</span><span class="sxs-lookup"><span data-stu-id="bc211-225">Recur every</span></span> | <span data-ttu-id="bc211-226">1 ora</span><span class="sxs-lookup"><span data-stu-id="bc211-226">1 hour</span></span> |
| <span data-ttu-id="bc211-227">Imposta scadenza</span><span class="sxs-lookup"><span data-stu-id="bc211-227">Set expiration</span></span> | <span data-ttu-id="bc211-228">No</span><span class="sxs-lookup"><span data-stu-id="bc211-228">No</span></span> |

<span data-ttu-id="bc211-229">Dopo aver creata la pianificazione hello, è necessario tooset hello i valori dei parametri da utilizzare ogni volta che la pianificazione avvia runbook hello.</span><span class="sxs-lookup"><span data-stu-id="bc211-229">Once hello schedule is created, you need tooset hello parameter values that will be used each time this schedule starts hello runbook.</span></span>

6. <span data-ttu-id="bc211-230">Fare clic su **Configura i parametri e le impostazioni di esecuzione**.</span><span class="sxs-lookup"><span data-stu-id="bc211-230">Click **Configure parameters and run settings**.</span></span>
7. <span data-ttu-id="bc211-231">Specificare i valori per **ResourceGroupName** e **AutomationAccountName**.</span><span class="sxs-lookup"><span data-stu-id="bc211-231">Fill in values for your **ResourceGroupName** and **AutomationAccountName**.</span></span>
8. <span data-ttu-id="bc211-232">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="bc211-232">Click **OK**.</span></span> 

## <a name="9-verify-runbook-starts-on-schedule"></a><span data-ttu-id="bc211-233">9. Verificare che il runbook venga avviato secondo la pianificazione</span><span class="sxs-lookup"><span data-stu-id="bc211-233">9. Verify runbook starts on schedule</span></span>
<span data-ttu-id="bc211-234">Ogni volta che un runbook viene avviato, [viene creato un processo](../automation/automation-runbook-execution.md) e l'output viene registrato.</span><span class="sxs-lookup"><span data-stu-id="bc211-234">Everytime a runbook is started, [a job is created](../automation/automation-runbook-execution.md) and any output logged.</span></span>  <span data-ttu-id="bc211-235">In realtà, questi sono hello stessi processi che hello runbook è la raccolta.</span><span class="sxs-lookup"><span data-stu-id="bc211-235">In fact, these are hello same jobs that hello runbook is collecting.</span></span>  <span data-ttu-id="bc211-236">È possibile verificare i che runbook hello viene avviato come previsto selezionando i processi di hello per hello runbook dopo che è trascorso l'ora di inizio hello pianificazione hello.</span><span class="sxs-lookup"><span data-stu-id="bc211-236">You can verify that hello runbook starts as expected by checking hello jobs for hello runbook after hello start time for hello schedule has passed.</span></span>

![Processi](media/operations-management-suite-runbook-datacollect/jobs.png)

1. <span data-ttu-id="bc211-238">Nelle proprietà hello runbook, selezionare **processi** in **risorse**.</span><span class="sxs-lookup"><span data-stu-id="bc211-238">In hello properties for your runbook, select **Jobs** under **Resources**.</span></span>
2. <span data-ttu-id="bc211-239">Verrà visualizzato che un elenco di processi per ogni runbook hello ora è stato avviato.</span><span class="sxs-lookup"><span data-stu-id="bc211-239">You should see a listing of jobs for each time hello runbook was started.</span></span>
3. <span data-ttu-id="bc211-240">Fare clic su uno dei hello processi tooview i dettagli.</span><span class="sxs-lookup"><span data-stu-id="bc211-240">Click on one of hello jobs tooview its details.</span></span>
4. <span data-ttu-id="bc211-241">Fare clic su **tutti i log** tooview hello output di hello runbook e registri.</span><span class="sxs-lookup"><span data-stu-id="bc211-241">Click on **All logs** tooview hello logs and output from hello runbook.</span></span>
5. <span data-ttu-id="bc211-242">Scorrere nella parte inferiore di toohello toofind voce simile toohello immagine riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="bc211-242">Scroll toohello bottom toofind an entry similar toohello image below.</span></span><br>![Dettagliato](media/operations-management-suite-runbook-datacollect/verbose.png)
6. <span data-ttu-id="bc211-244">Fare clic su questa voce tooview hello in dettaglio i dati json che è stati inviati tooLog Analitica.</span><span class="sxs-lookup"><span data-stu-id="bc211-244">Click on this entry tooview hello detailed json data  that was sent tooLog Analytics.</span></span>



## <a name="next-steps"></a><span data-ttu-id="bc211-245">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="bc211-245">Next steps</span></span>
- <span data-ttu-id="bc211-246">Utilizzare [Visualizza finestra di progettazione](../log-analytics/log-analytics-view-designer.md) toocreate per la visualizzazione di una visualizzazione dati che raccolti repository Analitica Log toohello di hello.</span><span class="sxs-lookup"><span data-stu-id="bc211-246">Use [View Designer](../log-analytics/log-analytics-view-designer.md) toocreate a view displaying hello data that you've collected toohello Log Analytics repository.</span></span>
- <span data-ttu-id="bc211-247">Creare un pacchetto il runbook in un [soluzione di gestione](operations-management-suite-solutions-creating.md) toodistribute toocustomers.</span><span class="sxs-lookup"><span data-stu-id="bc211-247">Package your runbook in a [management solution](operations-management-suite-solutions-creating.md) toodistribute toocustomers.</span></span>
- <span data-ttu-id="bc211-248">Altre informazioni su [Log Analytics](https://docs.microsoft.com/azure/log-analytics/).</span><span class="sxs-lookup"><span data-stu-id="bc211-248">Learn more about [Log Analytics](https://docs.microsoft.com/azure/log-analytics/).</span></span>
- <span data-ttu-id="bc211-249">Altre informazioni su [Automazione di Azure](https://docs.microsoft.com/azure/automation/).</span><span class="sxs-lookup"><span data-stu-id="bc211-249">Learn more about [Azure Automation](https://docs.microsoft.com/azure/automation/).</span></span>
- <span data-ttu-id="bc211-250">Altre informazioni su hello [API dell'agente di raccolta dati di HTTP](../log-analytics/log-analytics-data-collector-api.md).</span><span class="sxs-lookup"><span data-stu-id="bc211-250">Learn more about hello [HTTP Data Collector API](../log-analytics/log-analytics-data-collector-api.md).</span></span>
