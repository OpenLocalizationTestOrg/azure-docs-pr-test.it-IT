---
title: Raccolta di dati di Log Analytics con un runbook in Automazione di Azure | Microsoft Docs
description: Esercitazione dettagliata che illustra la creazione di un runbook in Automazione di Azure per la raccolta di dati nel repository OMS per la successiva analisi da parte di Log Analytics.
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
ms.openlocfilehash: 59f674c9c6404da7f5384539189f41a4ba1a939a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="collect-data-in-log-analytics-with-an-azure-automation-runbook"></a><span data-ttu-id="dc735-103">Raccogliere dati in Log Analytics con un runbook di Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="dc735-103">Collect data in Log Analytics with an Azure Automation runbook</span></span>
<span data-ttu-id="dc735-104">È possibile raccogliere una quantità significativa di dati in Log Analytics da una serie di origini, tra cui [origini dati](../log-analytics/log-analytics-data-sources.md) negli agenti e [dati raccolti da Azure](../log-analytics/log-analytics-azure-storage.md).</span><span class="sxs-lookup"><span data-stu-id="dc735-104">You can collect a significant amount of data in Log Analytics from a variety of sources including [data sources](../log-analytics/log-analytics-data-sources.md) on agents and also [data collected from Azure](../log-analytics/log-analytics-azure-storage.md).</span></span>  <span data-ttu-id="dc735-105">Esistono tuttavia scenari in cui è necessario raccogliere dati non accessibili tramite queste origini standard.</span><span class="sxs-lookup"><span data-stu-id="dc735-105">There are a scenarios though where you need to collect data that isn't accessible through these standard sources.</span></span>  <span data-ttu-id="dc735-106">In questi casi è possibile usare l'[API di raccolta dati HTTP](../log-analytics/log-analytics-data-collector-api.md) per inviare dati a Log Analytics da qualsiasi client dell'API REST.</span><span class="sxs-lookup"><span data-stu-id="dc735-106">In these cases, you can use the [HTTP Data Collector API](../log-analytics/log-analytics-data-collector-api.md) to write data to Log Analytics from any REST API client.</span></span>  <span data-ttu-id="dc735-107">Un modo comune per eseguire questa raccolta dati è usare un runbook in Automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="dc735-107">A common method to perform this data collection is using a runbook in Azure Automation.</span></span>   

<span data-ttu-id="dc735-108">Questa esercitazione illustra il processo di creazione e pianificazione di un runbook in Automazione di Azure per l'invio di dati a Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="dc735-108">This tutorial walks through the process for creating and scheduling a runbook in Azure Automation to write data to Log Analytics.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="dc735-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="dc735-109">Prerequisites</span></span>
<span data-ttu-id="dc735-110">Questo scenario richiede la configurazione delle risorse seguenti nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="dc735-110">This scenario requires the following resources configured in your Azure subscription.</span></span>  <span data-ttu-id="dc735-111">Per entrambe è possibile usare un account gratuito.</span><span class="sxs-lookup"><span data-stu-id="dc735-111">Both can be a free account.</span></span>

- <span data-ttu-id="dc735-112">[Area di lavoro di Log Analytics](../log-analytics/log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="dc735-112">[Log Analytics workspace](../log-analytics/log-analytics-get-started.md).</span></span>
- <span data-ttu-id="dc735-113">[Account di automazione di Azure](../automation/automation-offering-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="dc735-113">[Azure automation account](../automation/automation-offering-get-started.md).</span></span>

## <a name="overview-of-scenario"></a><span data-ttu-id="dc735-114">Panoramica dello scenario</span><span class="sxs-lookup"><span data-stu-id="dc735-114">Overview of scenario</span></span>
<span data-ttu-id="dc735-115">Per questa esercitazione si scriverà un runbook che raccoglie informazioni sui processi di automazione.</span><span class="sxs-lookup"><span data-stu-id="dc735-115">For this tutorial, you'll write a runbook that collects information about Automation jobs.</span></span>  <span data-ttu-id="dc735-116">I runbook in Automazione di Azure vengono implementati con PowerShell, quindi si inizia scrivendo e testando uno script nell'editor di Automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="dc735-116">Runbooks in Azure Automation are implemented with PowerShell, so you'll start by writing and testing a script in the Azure Automation editor.</span></span>  <span data-ttu-id="dc735-117">Dopo aver verificato che vengano raccolte le informazioni necessarie, si invieranno i dati a Log Analytics e si verificherà il tipo di dati personalizzato.</span><span class="sxs-lookup"><span data-stu-id="dc735-117">Once you verify that you're collecting the required information, you'll write that data to Log Analytics and verify the custom data type.</span></span>  <span data-ttu-id="dc735-118">Si creerà infine una pianificazione per avviare il runbook a intervalli regolari.</span><span class="sxs-lookup"><span data-stu-id="dc735-118">Finally, you'll create a schedule to start the runbook at regular intervals.</span></span>

> [!NOTE]
> <span data-ttu-id="dc735-119">È possibile configurare Automazione di Azure per l'invio di informazioni sui processi a Log Analytics senza questo runbook.</span><span class="sxs-lookup"><span data-stu-id="dc735-119">You can configure Azure Automation to send job information to Log Analytics without this runbook.</span></span>  <span data-ttu-id="dc735-120">Questo scenario viene usato principalmente a supporto dell'esercitazione e si consiglia di inviare i dati a un'area di lavoro di test.</span><span class="sxs-lookup"><span data-stu-id="dc735-120">This scenario is primarily used to support the tutorial, and it's recommended that you send the data to a test workspace.</span></span>  


## <a name="1-install-data-collector-api-module"></a><span data-ttu-id="dc735-121">1. Installare il modulo dell'API di raccolta dati</span><span class="sxs-lookup"><span data-stu-id="dc735-121">1. Install Data Collector API module</span></span>
<span data-ttu-id="dc735-122">Ogni [richiesta inviata dall'API di raccolta dati HTTP](../log-analytics/log-analytics-data-collector-api.md#create-a-request) deve essere nel formato corretto e includere un'intestazione dell'autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="dc735-122">Every [request from the HTTP Data Collector API](../log-analytics/log-analytics-data-collector-api.md#create-a-request) must be formatted appropriately and include an authorization header.</span></span>  <span data-ttu-id="dc735-123">Questa operazione può essere eseguita nel runbook, ma è possibile ridurre la quantità di codice necessario usando un modulo che semplifica questo processo.</span><span class="sxs-lookup"><span data-stu-id="dc735-123">You can do this in your runbook, but you can reduce the amount of code required by using a module that simplifies this process.</span></span>  <span data-ttu-id="dc735-124">Uno dei moduli che è possibile usare è [OMSIngestionAPI](https://www.powershellgallery.com/packages/OMSIngestionAPI) in PowerShell Gallery.</span><span class="sxs-lookup"><span data-stu-id="dc735-124">One module that you can use is [OMSIngestionAPI module](https://www.powershellgallery.com/packages/OMSIngestionAPI) in the PowerShell Gallery.</span></span>

<span data-ttu-id="dc735-125">Per usare un [modulo](../automation/automation-integration-modules.md) in un runbook, il modulo deve essere installato nell'account di Automazione.</span><span class="sxs-lookup"><span data-stu-id="dc735-125">To use a [module](../automation/automation-integration-modules.md) in a runbook, it must be installed in your Automation account.</span></span>  <span data-ttu-id="dc735-126">Qualsiasi runbook presente nello stesso account potrà quindi usare le funzioni disponibili nel modulo.</span><span class="sxs-lookup"><span data-stu-id="dc735-126">Any runbook in the same account can then use the functions in the module.</span></span>  <span data-ttu-id="dc735-127">È possibile installare un nuovo modulo selezionando **Asset** > **Moduli** > **Aggiungi un modulo** nell'account di Automazione.</span><span class="sxs-lookup"><span data-stu-id="dc735-127">You can install a new module by selecting **Assets** > **Modules** > **Add a module** in your Automation account.</span></span>  

<span data-ttu-id="dc735-128">PowerShell Gallery offre tuttavia un'opzione rapida per distribuire un modulo direttamente nell'account di Automazione, quindi è possibile usare questa opzione per l'esercitazione.</span><span class="sxs-lookup"><span data-stu-id="dc735-128">The PowerShell Gallery though gives you a quick option to deploy a module directly to your automation account so you can use that option for this tutorial.</span></span>  

![Modulo OMSIngestionAPI](media/operations-management-suite-runbook-datacollect/OMSIngestionAPI.png)

1. <span data-ttu-id="dc735-130">Passare a [PowerShell Gallery](https://www.powershellgallery.com/).</span><span class="sxs-lookup"><span data-stu-id="dc735-130">Go to [PowerShell Gallery](https://www.powershellgallery.com/).</span></span>
2. <span data-ttu-id="dc735-131">Cercare **OMSIngestionAPI**.</span><span class="sxs-lookup"><span data-stu-id="dc735-131">Search for **OMSIngestionAPI**.</span></span>
3. <span data-ttu-id="dc735-132">Fare clic sul pulsante **Deploy to Azure Automation** (Distribuisci in Automazione di Azure).</span><span class="sxs-lookup"><span data-stu-id="dc735-132">Click on the **Deploy to Azure Automation** button.</span></span>
4. <span data-ttu-id="dc735-133">Selezionare l'account di Automazione e fare clic su **OK** per installare il modulo.</span><span class="sxs-lookup"><span data-stu-id="dc735-133">Select your automation account and click **OK** to install the module.</span></span>


## <a name="2-create-automation-variables"></a><span data-ttu-id="dc735-134">2. Creare variabili di Automazione</span><span class="sxs-lookup"><span data-stu-id="dc735-134">2. Create Automation variables</span></span>
<span data-ttu-id="dc735-135">Le [variabili di Automazione](..\automation\automation-variables.md) contengono valori che possono essere usati da tutti i runbook presenti nell'account di Automazione.</span><span class="sxs-lookup"><span data-stu-id="dc735-135">[Automation variables](..\automation\automation-variables.md) hold values that can be used by all runbooks in your Automation account.</span></span>  <span data-ttu-id="dc735-136">Rendono i runbook più flessibili perché consentono di modificare questi valori senza modificare il runbook vero e proprio.</span><span class="sxs-lookup"><span data-stu-id="dc735-136">They make runbooks more flexible by allowing you to change these values without editing the actual runbook.</span></span> <span data-ttu-id="dc735-137">Ogni richiesta inviata dall'API di raccolta dati HTTP richiede l'ID e la chiave dell'area di lavoro OMS e gli asset di tipo variabile sono ideali per archiviare queste informazioni.</span><span class="sxs-lookup"><span data-stu-id="dc735-137">Every request from the HTTP Data Collector API requires the ID and key of the OMS workspace, and variable assets are ideal to store this information.</span></span>  

![Variabili](media/operations-management-suite-runbook-datacollect/variables.png)

1. <span data-ttu-id="dc735-139">Nel portale di Azure passare all'account di Automazione.</span><span class="sxs-lookup"><span data-stu-id="dc735-139">In the Azure portal, navigate to your Automation account.</span></span>
2. <span data-ttu-id="dc735-140">Selezionare **Variabili** in **Risorse condivise**.</span><span class="sxs-lookup"><span data-stu-id="dc735-140">Select **Variables** under **Shared Resources**.</span></span>
2. <span data-ttu-id="dc735-141">Fare clic su **Aggiungi variabile** e creare le due variabili nella tabella seguente.</span><span class="sxs-lookup"><span data-stu-id="dc735-141">Click **Add a variable** and create the two variables in the following table.</span></span>

| <span data-ttu-id="dc735-142">Proprietà</span><span class="sxs-lookup"><span data-stu-id="dc735-142">Property</span></span> | <span data-ttu-id="dc735-143">Valore ID area di lavoro</span><span class="sxs-lookup"><span data-stu-id="dc735-143">Workspace ID Value</span></span> | <span data-ttu-id="dc735-144">Valore chiave area di lavoro</span><span class="sxs-lookup"><span data-stu-id="dc735-144">Workspace Key Value</span></span> |
|:--|:--|:--|
| <span data-ttu-id="dc735-145">Nome</span><span class="sxs-lookup"><span data-stu-id="dc735-145">Name</span></span> | <span data-ttu-id="dc735-146">WorkspaceId</span><span class="sxs-lookup"><span data-stu-id="dc735-146">WorkspaceId</span></span> | <span data-ttu-id="dc735-147">WorkspaceKey</span><span class="sxs-lookup"><span data-stu-id="dc735-147">WorkspaceKey</span></span> |
| <span data-ttu-id="dc735-148">Tipo</span><span class="sxs-lookup"><span data-stu-id="dc735-148">Type</span></span> | <span data-ttu-id="dc735-149">String</span><span class="sxs-lookup"><span data-stu-id="dc735-149">String</span></span> | <span data-ttu-id="dc735-150">String</span><span class="sxs-lookup"><span data-stu-id="dc735-150">String</span></span> |
| <span data-ttu-id="dc735-151">Valore</span><span class="sxs-lookup"><span data-stu-id="dc735-151">Value</span></span> | <span data-ttu-id="dc735-152">Incollare l'ID dell'area di lavoro di Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="dc735-152">Paste in the Workspace ID of your Log Analytics workspace.</span></span> | <span data-ttu-id="dc735-153">Incollare la chiave primaria o secondaria dell'area di lavoro di Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="dc735-153">Paste in with the Primary or Secondary Key of your Log Analytics workspace.</span></span> |
| <span data-ttu-id="dc735-154">Crittografato</span><span class="sxs-lookup"><span data-stu-id="dc735-154">Encrypted</span></span> | <span data-ttu-id="dc735-155">No</span><span class="sxs-lookup"><span data-stu-id="dc735-155">No</span></span> | <span data-ttu-id="dc735-156">Sì</span><span class="sxs-lookup"><span data-stu-id="dc735-156">Yes</span></span> |



## <a name="3-create-runbook"></a><span data-ttu-id="dc735-157">3. Creare un runbook</span><span class="sxs-lookup"><span data-stu-id="dc735-157">3. Create runbook</span></span>

<span data-ttu-id="dc735-158">Automazione di Azure offre un editor nel portale in cui è possibile modificare e testare il runbook.</span><span class="sxs-lookup"><span data-stu-id="dc735-158">Azure Automation has an editor in the portal where you can edit and test your runbook.</span></span>  <span data-ttu-id="dc735-159">È possibile usare l'editor di script [direttamente con PowerShell](../automation/automation-edit-textual-runbook.md) oppure [creare un runbook grafico](../automation/automation-graphical-authoring-intro.md).</span><span class="sxs-lookup"><span data-stu-id="dc735-159">You have the option to use the script editor to work with [PowerShell directly](../automation/automation-edit-textual-runbook.md) or [create a graphical runbook](../automation/automation-graphical-authoring-intro.md).</span></span>  <span data-ttu-id="dc735-160">Per questa esercitazione si userà uno script di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dc735-160">For this tutorial, you will work with a PowerShell script.</span></span> 

![Modificare il runbook](media/operations-management-suite-runbook-datacollect/edit-runbook.png)

1. <span data-ttu-id="dc735-162">Passare all'account di Automazione.</span><span class="sxs-lookup"><span data-stu-id="dc735-162">Navigate to your Automation account.</span></span>  
2. <span data-ttu-id="dc735-163">Fare clic su **Runbook** > **Aggiungi runbook** > **Crea un nuovo runbook**.</span><span class="sxs-lookup"><span data-stu-id="dc735-163">Click **Runbooks** > **Add a runbook** > **Create a new runbook**.</span></span>
3. <span data-ttu-id="dc735-164">Per il nome del runbook digitare **Collect-Automation-jobs**.</span><span class="sxs-lookup"><span data-stu-id="dc735-164">For the runbook name, type **Collect-Automation-jobs**.</span></span>  <span data-ttu-id="dc735-165">Per il tipo di runbook selezionare **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="dc735-165">For the runbook type, select **PowerShell**.</span></span>
4. <span data-ttu-id="dc735-166">Fare clic su **Crea** per creare il runbook e avviare l'editor.</span><span class="sxs-lookup"><span data-stu-id="dc735-166">Click **Create** to create the runbook and start the editor.</span></span>
5. <span data-ttu-id="dc735-167">Copiare e incollare il codice seguente nel runbook.</span><span class="sxs-lookup"><span data-stu-id="dc735-167">Copy and paste the following code into the runbook.</span></span>  <span data-ttu-id="dc735-168">Vedere i commenti nello script per la spiegazione del codice.</span><span class="sxs-lookup"><span data-stu-id="dc735-168">Refer to the comments in the script for explanation of the code.</span></span>
    
        # Get information required for the automation account from parameter values when the runbook is started.
        Param
        (
            [Parameter(Mandatory = $True)]
            [string]$resourceGroupName,
            [Parameter(Mandatory = $True)]
            [string]$automationAccountName
        )
        
        # Authenticate to the Automation account using the Azure connection created when the Automation account was created.
        # Code copied from the runbook AzureAutomationTutorial.
        $connectionName = "AzureRunAsConnection"
        $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         
        Add-AzureRmAccount `
            -ServicePrincipal `
            -TenantId $servicePrincipalConnection.TenantId `
            -ApplicationId $servicePrincipalConnection.ApplicationId `
            -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint 
        
        # Set the $VerbosePreference variable so that we get verbose output in test environment.
        $VerbosePreference = "Continue"
        
        # Get information required for Log Analytics workspace from Automation variables.
        $customerId = Get-AutomationVariable -Name 'WorkspaceID'
        $sharedKey = Get-AutomationVariable -Name 'WorkspaceKey'
        
        # Set the name of the record type.
        $logType = "AutomationJob"
        
        # Get the jobs from the past hour.
        $jobs = Get-AzureRmAutomationJob -ResourceGroupName $resourceGroupName -AutomationAccountName $automationAccountName -StartTime (Get-Date).AddHours(-1)
        
        if ($jobs -ne $null) {
            # Convert the job data to json
            $body = $jobs | ConvertTo-Json
        
            # Write the body to verbose output so we can inspect it if verbose logging is on for the runbook.
            Write-Verbose $body
        
            # Send the data to Log Analytics.
            Send-OMSAPIIngestionFile -customerId $customerId -sharedKey $sharedKey -body $body -logType $logType -TimeStampField CreationTime
        }


## <a name="4-test-runbook"></a><span data-ttu-id="dc735-169">4. Testare il runbook</span><span class="sxs-lookup"><span data-stu-id="dc735-169">4. Test runbook</span></span>
<span data-ttu-id="dc735-170">Automazione di Azure include un ambiente che consente di [testare il runbook](../automation/automation-testing-runbook.md) prima di pubblicarlo.</span><span class="sxs-lookup"><span data-stu-id="dc735-170">Azure Automation includes an environment to [test your runbook](../automation/automation-testing-runbook.md) before you publish it.</span></span>  <span data-ttu-id="dc735-171">È possibile esaminare i dati raccolti dal runbook e verificare che il runbook invii i dati a Log Analytics come previsto prima della pubblicazione nell'ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="dc735-171">You can inspect the data collected by the runbook and verify that it writes to Log Analytics as expected before publishing it to production.</span></span> 
 
![Testare il runbook](media/operations-management-suite-runbook-datacollect/test-runbook.png)

6. <span data-ttu-id="dc735-173">Fare clic su **Salva** per salvare il runbook.</span><span class="sxs-lookup"><span data-stu-id="dc735-173">Click **Save** to save the runbook.</span></span>
1. <span data-ttu-id="dc735-174">Fare clic su **Riquadro di test** per aprire il runbook nell'ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="dc735-174">Click **Test pane** to open the runbook in the test environment.</span></span>
3. <span data-ttu-id="dc735-175">Il runbook include parametri, quindi verrà chiesto di inserire i relativi valori.</span><span class="sxs-lookup"><span data-stu-id="dc735-175">Since your runbook has parameters, you're prompted to enter values for them.</span></span>  <span data-ttu-id="dc735-176">Immettere il nome del gruppo di risorse e l'account di Automazione dal quale verranno raccolte le informazioni sui processi.</span><span class="sxs-lookup"><span data-stu-id="dc735-176">Enter the name of the resource group and the automation account that your going to collect job information from.</span></span>
4. <span data-ttu-id="dc735-177">Fare clic su **Avvia** per avviare il runbook.</span><span class="sxs-lookup"><span data-stu-id="dc735-177">Click **Start** to the start the runbook.</span></span>
3. <span data-ttu-id="dc735-178">Il runbook verrà avviato con lo stato **In coda** prima di passare allo stato **In esecuzione** e</span><span class="sxs-lookup"><span data-stu-id="dc735-178">The runbook will start with a status of **Queued** before it goes to **Running**.</span></span>  
3. <span data-ttu-id="dc735-179">Il runbook visualizzerà un output dettagliato con i processi raccolti in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="dc735-179">The runbook should display verbose output with the jobs collected in json format.</span></span>  <span data-ttu-id="dc735-180">Se non è elencato alcun processo, probabilmente non sono stati creati processi nell'account di Automazione nell'ultima ora.</span><span class="sxs-lookup"><span data-stu-id="dc735-180">If no jobs are listed, then there may have been no jobs created in the automation account in the last hour.</span></span>  <span data-ttu-id="dc735-181">Provare ad avviare un runbook nell'account di Automazione e quindi eseguire di nuovo il test.</span><span class="sxs-lookup"><span data-stu-id="dc735-181">Try starting any runbook in the automation account and then perform the test again.</span></span>
4. <span data-ttu-id="dc735-182">Assicurarsi che l'output non visualizzi eventuali errori nel comando POST per Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="dc735-182">Ensure that the output doesn't show any errors in the post command to Log Analytics.</span></span>  <span data-ttu-id="dc735-183">Verrà visualizzato un messaggio simile al seguente.</span><span class="sxs-lookup"><span data-stu-id="dc735-183">You should have a message similar to the following.</span></span>

    ![Output del comando POST](media/operations-management-suite-runbook-datacollect/post-output.png)

## <a name="5-verify-records-in-log-analytics"></a><span data-ttu-id="dc735-185">5. Verificare i record in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="dc735-185">5. Verify records in Log Analytics</span></span>
<span data-ttu-id="dc735-186">Dopo aver completato il test del runbook e aver verificato che l'output sia stato ricevuto correttamente, è possibile verificare che i record siano stati creati usando una [ricerca log in Log Analytics](../log-analytics/log-analytics-log-searches.md).</span><span class="sxs-lookup"><span data-stu-id="dc735-186">Once the runbook has completed in test, and you verified that the output was successfully received, you can verify that the records were created using a [log search in Log Analytics](../log-analytics/log-analytics-log-searches.md).</span></span>

![Output del log](media/operations-management-suite-runbook-datacollect/log-output.png)

1. <span data-ttu-id="dc735-188">Nel portale di Azure selezionare l'area di lavoro di Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="dc735-188">In the Azure portal, select your Log Analytics workspace.</span></span>
2. <span data-ttu-id="dc735-189">Fare clic su **Ricerca log**.</span><span class="sxs-lookup"><span data-stu-id="dc735-189">Click on **Log Search**.</span></span>
3. <span data-ttu-id="dc735-190">Digitare il comando `Type=AutomationJob_CL` e fare clic sul pulsante di ricerca.</span><span class="sxs-lookup"><span data-stu-id="dc735-190">Type the following command `Type=AutomationJob_CL` and click the search button.</span></span> <span data-ttu-id="dc735-191">Si noti che il tipo di record include _CL, non specificato nello script.</span><span class="sxs-lookup"><span data-stu-id="dc735-191">Note that the record type includes _CL that isn't specified in the script.</span></span>  <span data-ttu-id="dc735-192">Tale suffisso viene aggiunto automaticamente al tipo di log per indicare che si tratta di un tipo di log personalizzato.</span><span class="sxs-lookup"><span data-stu-id="dc735-192">That suffix is automatically appended to the log type to indicate that it's a custom log type.</span></span>
4. <span data-ttu-id="dc735-193">Verranno restituiti uno o più record, a indicare che il runbook funziona come previsto.</span><span class="sxs-lookup"><span data-stu-id="dc735-193">You should see one or more records returned indicating that the runbook is working as expected.</span></span>


## <a name="6-publish-the-runbook"></a><span data-ttu-id="dc735-194">6. Pubblicare il runbook</span><span class="sxs-lookup"><span data-stu-id="dc735-194">6. Publish the runbook</span></span>
<span data-ttu-id="dc735-195">Dopo aver verificato che il runbook funzioni correttamente, è necessario pubblicarlo per eseguirlo nell'ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="dc735-195">Once you've verified that the runbook is working correctly, you need to publish it so you can run it in production.</span></span>  <span data-ttu-id="dc735-196">È possibile continuare a modificare e testare il runbook senza modificare la versione pubblicata.</span><span class="sxs-lookup"><span data-stu-id="dc735-196">You can continue to edit and test the runbook without modifying the published version.</span></span>  

![Pubblicare il runbook](media/operations-management-suite-runbook-datacollect/publish-runbook.png)

1. <span data-ttu-id="dc735-198">Tornare all'account di Automazione.</span><span class="sxs-lookup"><span data-stu-id="dc735-198">Return to your automation account.</span></span>
2. <span data-ttu-id="dc735-199">Fare clic su **Runbook** e selezionare **Collect-Automation-jobs**.</span><span class="sxs-lookup"><span data-stu-id="dc735-199">Click on **Runbooks** and select **Collect-Automation-jobs**.</span></span>
3. <span data-ttu-id="dc735-200">Fare clic su **Modifica** e quindi su **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="dc735-200">Click **Edit** and then **Publish**.</span></span>
4. <span data-ttu-id="dc735-201">Fare clic su **Sì** quando viene chiesto di confermare l'intenzione di sovrascrivere la versione pubblicata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="dc735-201">Click **Yes** when asked to verify that you want to overwrite the previously published version.</span></span>

## <a name="7-set-logging-options"></a><span data-ttu-id="dc735-202">7. Impostare le opzioni di registrazione</span><span class="sxs-lookup"><span data-stu-id="dc735-202">7. Set logging options</span></span> 
<span data-ttu-id="dc735-203">Per l'ambiente di test è stato possibile esaminare l'[output dettagliato](../automation/automation-runbook-output-and-messages.md#message-streams) perché è stata impostata la variabile $VerbosePreference nello script.</span><span class="sxs-lookup"><span data-stu-id="dc735-203">For test, you were able to view [verbose output](../automation/automation-runbook-output-and-messages.md#message-streams) because you set the $VerbosePreference variable in the script.</span></span>  <span data-ttu-id="dc735-204">Per l'ambiente di produzione è necessario impostare le proprietà di registrazione per il runbook se si intende visualizzare l'output dettagliato.</span><span class="sxs-lookup"><span data-stu-id="dc735-204">For production, you need to set the logging properties for the runbook if you want to view verbose output.</span></span>  <span data-ttu-id="dc735-205">Per il runbook usato in questa esercitazione, verranno visualizzati i dati JSON inviati a Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="dc735-205">For the runbook used in this tutorial, this will display the json data being sent to Log Analytics.</span></span>

![Registrazione e traccia](media/operations-management-suite-runbook-datacollect/logging.png)

1. <span data-ttu-id="dc735-207">Nelle proprietà del runbook selezionare **Registrazione e traccia** in **Impostazioni del runbook**.</span><span class="sxs-lookup"><span data-stu-id="dc735-207">In the properties for your runbook select **Logging and tracing** under **Runbook Settings**.</span></span>
2. <span data-ttu-id="dc735-208">Impostare **Registra record dettagliati** su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="dc735-208">Change the setting for **Log verbose records** to **On**.</span></span>
3. <span data-ttu-id="dc735-209">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="dc735-209">Click **Save**.</span></span>

## <a name="8-schedule-runbook"></a><span data-ttu-id="dc735-210">8. Pianificare il runbook</span><span class="sxs-lookup"><span data-stu-id="dc735-210">8. Schedule runbook</span></span>
<span data-ttu-id="dc735-211">Il modo più comune per avviare un runbook che raccoglie dati di monitoraggio è di pianificarne l'esecuzione automatica.</span><span class="sxs-lookup"><span data-stu-id="dc735-211">The most common way to start a runbook that collects monitoring data is to schedule it to run automatically.</span></span>  <span data-ttu-id="dc735-212">Per eseguire questa operazione, creare una [pianificazione in Automazione di Azure](../automation/automation-schedules.md) e associarla al runbook.</span><span class="sxs-lookup"><span data-stu-id="dc735-212">You do this by creating a [schedule in Azure Automation](../automation/automation-schedules.md) and attaching it to your runbook.</span></span>

![Pianificare il runbook](media/operations-management-suite-runbook-datacollect/schedule-runbook.png)

1. <span data-ttu-id="dc735-214">Nelle proprietà del runbook selezionare **Pianificazioni** in **Risorse**.</span><span class="sxs-lookup"><span data-stu-id="dc735-214">In the properties for your runbook, select **Schedules** under **Resources**.</span></span>
2. <span data-ttu-id="dc735-215">Fare clic su **Aggiungi pianificazione** > **Collegare una pianificazione al runbook** > **Crea una nuova pianificazione**.</span><span class="sxs-lookup"><span data-stu-id="dc735-215">Click **Add a schedule** > **Link a schedule to your runbook** > **Create a new schedule**.</span></span>
5. <span data-ttu-id="dc735-216">Immettere i valori seguenti per la pianificazione e fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="dc735-216">Type in the following values for the schedule and click **Create**.</span></span>

| <span data-ttu-id="dc735-217">Proprietà</span><span class="sxs-lookup"><span data-stu-id="dc735-217">Property</span></span> | <span data-ttu-id="dc735-218">Valore</span><span class="sxs-lookup"><span data-stu-id="dc735-218">Value</span></span> |
|:--|:--|
| <span data-ttu-id="dc735-219">Nome</span><span class="sxs-lookup"><span data-stu-id="dc735-219">Name</span></span> | <span data-ttu-id="dc735-220">AutomationJobs-Hourly</span><span class="sxs-lookup"><span data-stu-id="dc735-220">AutomationJobs-Hourly</span></span> |
| <span data-ttu-id="dc735-221">Inizia</span><span class="sxs-lookup"><span data-stu-id="dc735-221">Starts</span></span> | <span data-ttu-id="dc735-222">Selezionare un orario successivo di almeno 5 minuti all'ora corrente.</span><span class="sxs-lookup"><span data-stu-id="dc735-222">Select any time at least 5 minutes past the current time.</span></span> |
| <span data-ttu-id="dc735-223">Ricorrenza</span><span class="sxs-lookup"><span data-stu-id="dc735-223">Recurrence</span></span> | <span data-ttu-id="dc735-224">Ricorrente</span><span class="sxs-lookup"><span data-stu-id="dc735-224">Recurring</span></span> |
| <span data-ttu-id="dc735-225">Ricorre ogni</span><span class="sxs-lookup"><span data-stu-id="dc735-225">Recur every</span></span> | <span data-ttu-id="dc735-226">1 ora</span><span class="sxs-lookup"><span data-stu-id="dc735-226">1 hour</span></span> |
| <span data-ttu-id="dc735-227">Imposta scadenza</span><span class="sxs-lookup"><span data-stu-id="dc735-227">Set expiration</span></span> | <span data-ttu-id="dc735-228">No</span><span class="sxs-lookup"><span data-stu-id="dc735-228">No</span></span> |

<span data-ttu-id="dc735-229">Dopo aver creato la pianificazione è necessario impostare i valori dei parametri che verranno usati ogni volta che la pianificazione avvia il runbook.</span><span class="sxs-lookup"><span data-stu-id="dc735-229">Once the schedule is created, you need to set the parameter values that will be used each time this schedule starts the runbook.</span></span>

6. <span data-ttu-id="dc735-230">Fare clic su **Configura i parametri e le impostazioni di esecuzione**.</span><span class="sxs-lookup"><span data-stu-id="dc735-230">Click **Configure parameters and run settings**.</span></span>
7. <span data-ttu-id="dc735-231">Specificare i valori per **ResourceGroupName** e **AutomationAccountName**.</span><span class="sxs-lookup"><span data-stu-id="dc735-231">Fill in values for your **ResourceGroupName** and **AutomationAccountName**.</span></span>
8. <span data-ttu-id="dc735-232">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="dc735-232">Click **OK**.</span></span> 

## <a name="9-verify-runbook-starts-on-schedule"></a><span data-ttu-id="dc735-233">9. Verificare che il runbook venga avviato secondo la pianificazione</span><span class="sxs-lookup"><span data-stu-id="dc735-233">9. Verify runbook starts on schedule</span></span>
<span data-ttu-id="dc735-234">Ogni volta che un runbook viene avviato, [viene creato un processo](../automation/automation-runbook-execution.md) e l'output viene registrato.</span><span class="sxs-lookup"><span data-stu-id="dc735-234">Everytime a runbook is started, [a job is created](../automation/automation-runbook-execution.md) and any output logged.</span></span>  <span data-ttu-id="dc735-235">Si tratta in realtà degli stessi processi che vengono raccolti dal runbook.</span><span class="sxs-lookup"><span data-stu-id="dc735-235">In fact, these are the same jobs that the runbook is collecting.</span></span>  <span data-ttu-id="dc735-236">È possibile verificare che il runbook si avvii come previsto controllando i processi del runbook quando è trascorsa l'ora di inizio della pianificazione.</span><span class="sxs-lookup"><span data-stu-id="dc735-236">You can verify that the runbook starts as expected by checking the jobs for the runbook after the start time for the schedule has passed.</span></span>

![Processi](media/operations-management-suite-runbook-datacollect/jobs.png)

1. <span data-ttu-id="dc735-238">Nelle proprietà del runbook selezionare **Processi** in **Risorse**.</span><span class="sxs-lookup"><span data-stu-id="dc735-238">In the properties for your runbook, select **Jobs** under **Resources**.</span></span>
2. <span data-ttu-id="dc735-239">Verrà visualizzato un elenco di processi per ogni volta in cui è stato avviato il runbook.</span><span class="sxs-lookup"><span data-stu-id="dc735-239">You should see a listing of jobs for each time the runbook was started.</span></span>
3. <span data-ttu-id="dc735-240">Fare clic su un processo per visualizzarne i dettagli.</span><span class="sxs-lookup"><span data-stu-id="dc735-240">Click on one of the jobs to view its details.</span></span>
4. <span data-ttu-id="dc735-241">Fare clic su **Tutti i log** per visualizzare i log e l'output del runbook.</span><span class="sxs-lookup"><span data-stu-id="dc735-241">Click on **All logs** to view the logs and output from the runbook.</span></span>
5. <span data-ttu-id="dc735-242">Scorrere verso il basso per trovare una voce simile a quella riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="dc735-242">Scroll to the bottom to find an entry similar to the image below.</span></span><br>![Dettagliato](media/operations-management-suite-runbook-datacollect/verbose.png)
6. <span data-ttu-id="dc735-244">Fare clic su questa voce per visualizzare i dati JSON dettagliati che sono stati inviati a Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="dc735-244">Click on this entry to view the detailed json data  that was sent to Log Analytics.</span></span>



## <a name="next-steps"></a><span data-ttu-id="dc735-245">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="dc735-245">Next steps</span></span>
- <span data-ttu-id="dc735-246">Usare [Progettazione viste](../log-analytics/log-analytics-view-designer.md) per creare una vista con i dati raccolti nel repository di Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="dc735-246">Use [View Designer](../log-analytics/log-analytics-view-designer.md) to create a view displaying the data that you've collected to the Log Analytics repository.</span></span>
- <span data-ttu-id="dc735-247">Creare il pacchetto del runbook in una [soluzione di gestione](operations-management-suite-solutions-creating.md) da distribuire ai clienti.</span><span class="sxs-lookup"><span data-stu-id="dc735-247">Package your runbook in a [management solution](operations-management-suite-solutions-creating.md) to distribute to customers.</span></span>
- <span data-ttu-id="dc735-248">Altre informazioni su [Log Analytics](https://docs.microsoft.com/azure/log-analytics/).</span><span class="sxs-lookup"><span data-stu-id="dc735-248">Learn more about [Log Analytics](https://docs.microsoft.com/azure/log-analytics/).</span></span>
- <span data-ttu-id="dc735-249">Altre informazioni su [Automazione di Azure](https://docs.microsoft.com/azure/automation/).</span><span class="sxs-lookup"><span data-stu-id="dc735-249">Learn more about [Azure Automation](https://docs.microsoft.com/azure/automation/).</span></span>
- <span data-ttu-id="dc735-250">Altre informazioni sull'[API di raccolta dati HTTP](../log-analytics/log-analytics-data-collector-api.md).</span><span class="sxs-lookup"><span data-stu-id="dc735-250">Learn more about the [HTTP Data Collector API](../log-analytics/log-analytics-data-collector-api.md).</span></span>