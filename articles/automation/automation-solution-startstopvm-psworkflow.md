---
title: Avvio e arresto di macchine virtuali con Automazione di Azure - Flusso di lavoro PowerShell | Documentazione Microsoft
description: Versione grafica dello scenario di Automazione di Azure che include runbook per l'avvio e l'arresto di macchine virtuali classiche.
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: d380bd43-d45d-45af-a5b2-78e7f66263c3
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/06/2016
ms.author: magoedte;bwren
redirect_url: https://docs.microsoft.com/azure/automation/automation-solution-vm-management
redirect_document_id: FALSE
ms.openlocfilehash: 95a7b02b0d11bf18c398daea48d16e0ead30b543
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-automation-scenario---starting-and-stopping-virtual-machines"></a><span data-ttu-id="494b8-103">Scenario di Automazione di Azure - Avvio e arresto delle macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="494b8-103">Azure Automation scenario - starting and stopping virtual machines</span></span>
<span data-ttu-id="494b8-104">Questo scenario di Automazione di Azure include runbook per l'avvio e l'arresto di macchine virtuali classiche.</span><span class="sxs-lookup"><span data-stu-id="494b8-104">This Azure Automation scenario includes runbooks to start and stop classic virtual machines.</span></span>  <span data-ttu-id="494b8-105">È possibile usare questo scenario per le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="494b8-105">You can use this scenario for any of the following:</span></span>  

* <span data-ttu-id="494b8-106">Usare i runbook senza modifiche nell'ambiente in uso.</span><span class="sxs-lookup"><span data-stu-id="494b8-106">Use the runbooks without modification in your own environment.</span></span>
* <span data-ttu-id="494b8-107">Modificare i runbook per eseguire funzionalità personalizzate.</span><span class="sxs-lookup"><span data-stu-id="494b8-107">Modify the runbooks to perform customized functionality.</span></span>  
* <span data-ttu-id="494b8-108">Chiamare i runbook da un altro runbook come parte di una soluzione completa.</span><span class="sxs-lookup"><span data-stu-id="494b8-108">Call the runbooks from another runbook as part of an overall solution.</span></span>
* <span data-ttu-id="494b8-109">Usare i runbook come esercitazioni per acquisire familiarità con i concetti di creazione dei runbook.</span><span class="sxs-lookup"><span data-stu-id="494b8-109">Use the runbooks as tutorials to learn runbook authoring concepts.</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="494b8-110">Grafico</span><span class="sxs-lookup"><span data-stu-id="494b8-110">Graphical</span></span>](automation-solution-startstopvm-graphical.md)
> * [<span data-ttu-id="494b8-111">Flusso di lavoro PowerShell</span><span class="sxs-lookup"><span data-stu-id="494b8-111">PowerShell Workflow</span></span>](automation-solution-startstopvm-psworkflow.md)
> 
> 

<span data-ttu-id="494b8-112">Questa è la versione del flusso di lavoro PowerShell per lo scenario con runbook.</span><span class="sxs-lookup"><span data-stu-id="494b8-112">This is the PowerShell Workflow runbook version of this scenario.</span></span> <span data-ttu-id="494b8-113">È disponibile anche usando [runbook grafici](automation-solution-startstopvm-graphical.md).</span><span class="sxs-lookup"><span data-stu-id="494b8-113">It is also available using [graphical runbooks](automation-solution-startstopvm-graphical.md).</span></span>

## <a name="getting-the-scenario"></a><span data-ttu-id="494b8-114">Come ottenere lo scenario</span><span class="sxs-lookup"><span data-stu-id="494b8-114">Getting the scenario</span></span>
<span data-ttu-id="494b8-115">Questo scenario è costituito da due runbook del flusso di lavoro PowerShell che è possibile scaricare dai collegamenti seguenti.</span><span class="sxs-lookup"><span data-stu-id="494b8-115">This scenario consists of two PowerShell Workflow runbooks that you can download from the following links.</span></span>  <span data-ttu-id="494b8-116">Per i collegamenti ai runbook grafici, vedere la [versione grafica](automation-solution-startstopvm-graphical.md) di questo scenario.</span><span class="sxs-lookup"><span data-stu-id="494b8-116">See the [graphical version](automation-solution-startstopvm-graphical.md) of this scenario for links to the graphical runbooks.</span></span>

| <span data-ttu-id="494b8-117">Runbook</span><span class="sxs-lookup"><span data-stu-id="494b8-117">Runbook</span></span> | <span data-ttu-id="494b8-118">Collegamento</span><span class="sxs-lookup"><span data-stu-id="494b8-118">Link</span></span> | <span data-ttu-id="494b8-119">Tipo</span><span class="sxs-lookup"><span data-stu-id="494b8-119">Type</span></span> | <span data-ttu-id="494b8-120">Descrizione</span><span class="sxs-lookup"><span data-stu-id="494b8-120">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="494b8-121">Start-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="494b8-121">Start-AzureVMs</span></span> |[<span data-ttu-id="494b8-122">Avviare le macchine virtuali classiche di Azure</span><span class="sxs-lookup"><span data-stu-id="494b8-122">Start Azure Classic VMs</span></span>](https://gallery.technet.microsoft.com/Start-Azure-Classic-VMs-86ef746b) |<span data-ttu-id="494b8-123">Flusso di lavoro PowerShell</span><span class="sxs-lookup"><span data-stu-id="494b8-123">PowerShell Workflow</span></span> |<span data-ttu-id="494b8-124">Avvia tutte le macchine virtuali classiche in una sottoscrizione di Azure o tutte le macchine virtuali con un nome di servizio specifico.</span><span class="sxs-lookup"><span data-stu-id="494b8-124">Starts all classic virtual machines in an Azure subscriptionor all virtual machines with a particular service name.</span></span> |
| <span data-ttu-id="494b8-125">Stop-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="494b8-125">Stop-AzureVMs</span></span> |[<span data-ttu-id="494b8-126">Arrestare le macchine virtuali classiche di Azure</span><span class="sxs-lookup"><span data-stu-id="494b8-126">Stop Azure Classic VMs</span></span>](https://gallery.technet.microsoft.com/Stop-Azure-Classic-VMs-7a4ae43e) |<span data-ttu-id="494b8-127">Flusso di lavoro PowerShell</span><span class="sxs-lookup"><span data-stu-id="494b8-127">PowerShell Workflow</span></span> |<span data-ttu-id="494b8-128">Arresta tutte le macchine virtuali in un account di automazione o tutte le macchine virtuali con un nome di servizio specifico.</span><span class="sxs-lookup"><span data-stu-id="494b8-128">Stops all virtual machines in an automation account or all virtual machines with a particular service name.</span></span> |

## <a name="installing-and-configuring-the-scenario"></a><span data-ttu-id="494b8-129">Installazione e configurazione dello scenario</span><span class="sxs-lookup"><span data-stu-id="494b8-129">Installing and configuring the scenario</span></span>
### <a name="1-install-the-runbooks"></a><span data-ttu-id="494b8-130">1. Installare i runbook</span><span class="sxs-lookup"><span data-stu-id="494b8-130">1. Install the runbooks</span></span>
<span data-ttu-id="494b8-131">Dopo aver scaricato i runbook, è possibile importarli usando la procedura descritta nell'articolo relativo all' [importazione di un runbook](http://msdn.microsoft.com/library/dn643637.aspx#ImportRunbook).</span><span class="sxs-lookup"><span data-stu-id="494b8-131">After downloading the runbooks, you can import them using the procedure in [Importing a Runbook](http://msdn.microsoft.com/library/dn643637.aspx#ImportRunbook).</span></span>

### <a name="2-review-the-description-and-requirements"></a><span data-ttu-id="494b8-132">2. Esaminare la descrizione e i requisiti</span><span class="sxs-lookup"><span data-stu-id="494b8-132">2. Review the description and requirements</span></span>
<span data-ttu-id="494b8-133">I runbook includono testo di supporto commentato contenente una descrizione e gli asset necessari.</span><span class="sxs-lookup"><span data-stu-id="494b8-133">The runbooks include commented help text that includes a description and required assets.</span></span>  <span data-ttu-id="494b8-134">Le stesse informazioni sono disponibili anche in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="494b8-134">You can also get the same information from this article.</span></span>

### <a name="3-configure-assets"></a><span data-ttu-id="494b8-135">3. Configurare gli asset</span><span class="sxs-lookup"><span data-stu-id="494b8-135">3. Configure assets</span></span>
<span data-ttu-id="494b8-136">I runbook richiedono gli asset seguenti, che devono essere creati e popolati con i valori appropriati.</span><span class="sxs-lookup"><span data-stu-id="494b8-136">The runbooks require the following assets that you must create and populate with appropriate values.</span></span>

| <span data-ttu-id="494b8-137">Tipo di risorsa</span><span class="sxs-lookup"><span data-stu-id="494b8-137">Asset Type</span></span> | <span data-ttu-id="494b8-138">Nome dell’asset</span><span class="sxs-lookup"><span data-stu-id="494b8-138">Asset Name</span></span> | <span data-ttu-id="494b8-139">Descrizione</span><span class="sxs-lookup"><span data-stu-id="494b8-139">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="494b8-140">Credenziali</span><span class="sxs-lookup"><span data-stu-id="494b8-140">Credential</span></span> |<span data-ttu-id="494b8-141">AzureCredential</span><span class="sxs-lookup"><span data-stu-id="494b8-141">AzureCredential</span></span> |<span data-ttu-id="494b8-142">Contiene le credenziali per un account che dispone delle autorizzazioni per avviare e arrestare le macchine virtuali nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="494b8-142">Contains credentials for an account that has authority to start and stop virtual machines in the Azure subscription.</span></span>  <span data-ttu-id="494b8-143">In alternativa, è possibile specificare un altro asset di tipo credenziali nel parametro **Credential** dell'attività **Add-AzureAccount**.</span><span class="sxs-lookup"><span data-stu-id="494b8-143">Alternatively, you can specify another credential asset in the **Credential** parameter of the **Add-AzureAccount** activity.</span></span> |
| <span data-ttu-id="494b8-144">Variabile</span><span class="sxs-lookup"><span data-stu-id="494b8-144">Variable</span></span> |<span data-ttu-id="494b8-145">AzureSubscriptionId</span><span class="sxs-lookup"><span data-stu-id="494b8-145">AzureSubscriptionId</span></span> |<span data-ttu-id="494b8-146">Contiene l'ID sottoscrizione della sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="494b8-146">Contains the subscription ID of your Azure subscription.</span></span> |

## <a name="using-the-scenario"></a><span data-ttu-id="494b8-147">Uso dello scenario</span><span class="sxs-lookup"><span data-stu-id="494b8-147">Using the scenario</span></span>
### <a name="parameters"></a><span data-ttu-id="494b8-148">Parametri</span><span class="sxs-lookup"><span data-stu-id="494b8-148">Parameters</span></span>
<span data-ttu-id="494b8-149">Ogni runbook è associato ai parametri seguenti.</span><span class="sxs-lookup"><span data-stu-id="494b8-149">The runbooks each have the following parameters.</span></span>  <span data-ttu-id="494b8-150">È necessario fornire valori per tutti i parametri obbligatori ed è possibile facoltativamente specificare i valori per gli altri parametri a seconda delle esigenze.</span><span class="sxs-lookup"><span data-stu-id="494b8-150">You must provide values for any mandatory parameters and can optionally provide values for other parameters depending on your requirements.</span></span>

| <span data-ttu-id="494b8-151">Parametro</span><span class="sxs-lookup"><span data-stu-id="494b8-151">Parameter</span></span> | <span data-ttu-id="494b8-152">Tipo</span><span class="sxs-lookup"><span data-stu-id="494b8-152">Type</span></span> | <span data-ttu-id="494b8-153">Mandatory</span><span class="sxs-lookup"><span data-stu-id="494b8-153">Mandatory</span></span> | <span data-ttu-id="494b8-154">Descrizione</span><span class="sxs-lookup"><span data-stu-id="494b8-154">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="494b8-155">ServiceName</span><span class="sxs-lookup"><span data-stu-id="494b8-155">ServiceName</span></span> |<span data-ttu-id="494b8-156">string</span><span class="sxs-lookup"><span data-stu-id="494b8-156">string</span></span> |<span data-ttu-id="494b8-157">No</span><span class="sxs-lookup"><span data-stu-id="494b8-157">No</span></span> |<span data-ttu-id="494b8-158">Se viene specificato un valore, verranno avviate o arrestate tutte le macchine virtuali con lo stesso nome di servizio.</span><span class="sxs-lookup"><span data-stu-id="494b8-158">If a value is provided, then all virtual machines with that service name are started or stopped.</span></span>  <span data-ttu-id="494b8-159">Se invece non viene specificato alcun valore, verranno avviate o arrestate tutte le macchine virtuali classiche della sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="494b8-159">If no value is provided, then all classic virtual machines in the Azure subscription are started or stopped.</span></span> |
| <span data-ttu-id="494b8-160">AzureSubscriptionIdAssetName</span><span class="sxs-lookup"><span data-stu-id="494b8-160">AzureSubscriptionIdAssetName</span></span> |<span data-ttu-id="494b8-161">string</span><span class="sxs-lookup"><span data-stu-id="494b8-161">string</span></span> |<span data-ttu-id="494b8-162">No</span><span class="sxs-lookup"><span data-stu-id="494b8-162">No</span></span> |<span data-ttu-id="494b8-163">Contiene il nome dell' [asset di tipo variabile](#installing-and-configuring-the-scenario) che include l'ID sottoscrizione della sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="494b8-163">Contains the name of the [variable asset](#installing-and-configuring-the-scenario) that contains the subscription ID of your Azure subscription.</span></span>  <span data-ttu-id="494b8-164">Se non si specifica un valore, verrà usato *AzureSubscriptionId* .</span><span class="sxs-lookup"><span data-stu-id="494b8-164">If you don't specify a value, *AzureSubscriptionId* is used.</span></span> |
| <span data-ttu-id="494b8-165">AzureCredentialAssetName</span><span class="sxs-lookup"><span data-stu-id="494b8-165">AzureCredentialAssetName</span></span> |<span data-ttu-id="494b8-166">string</span><span class="sxs-lookup"><span data-stu-id="494b8-166">string</span></span> |<span data-ttu-id="494b8-167">No</span><span class="sxs-lookup"><span data-stu-id="494b8-167">No</span></span> |<span data-ttu-id="494b8-168">Contiene il nome dell' [asset di tipo credenziali](#installing-and-configuring-the-scenario) che include le credenziali per il runbook da usare.</span><span class="sxs-lookup"><span data-stu-id="494b8-168">Contains the name of the [credential asset](#installing-and-configuring-the-scenario) that contains the credentials for the runbook to use.</span></span>  <span data-ttu-id="494b8-169">Se non si specifica un valore, verrà usato *AzureCredential* .</span><span class="sxs-lookup"><span data-stu-id="494b8-169">If you don't specify a value, *AzureCredential* is used.</span></span> |

### <a name="starting-the-runbooks"></a><span data-ttu-id="494b8-170">Avvio dei runbook</span><span class="sxs-lookup"><span data-stu-id="494b8-170">Starting the runbooks</span></span>
<span data-ttu-id="494b8-171">È possibile usare uno dei metodi descritti in [Avvio di un Runbook in Automazione di Azure](automation-starting-a-runbook.md) per avviare uno dei runbook di questo scenario.</span><span class="sxs-lookup"><span data-stu-id="494b8-171">You can use any of the methods in [Starting a runbook in Azure Automation](automation-starting-a-runbook.md) to start either of the runbooks in this scenario.</span></span>

<span data-ttu-id="494b8-172">I comandi di esempio seguenti usano Windows PowerShell per eseguire **StartAzureVMs** per avviare tutte le macchine virtuali con nome di servizio *MyVMService*.</span><span class="sxs-lookup"><span data-stu-id="494b8-172">The following sample commands uses Windows PowerShell to run **StartAzureVMs** to start all virtual machines with the service name *MyVMService*.</span></span>

    $params = @{"ServiceName"="MyVMService"}
    Start-AzureAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Start-AzureVMs" –Parameters $params

### <a name="output"></a><span data-ttu-id="494b8-173">Output</span><span class="sxs-lookup"><span data-stu-id="494b8-173">Output</span></span>
<span data-ttu-id="494b8-174">I runbook [restituiranno un messaggio](automation-runbook-output-and-messages.md) per ogni macchina virtuale indicando se l'istruzione di avvio o di arresto è stata inviata correttamente.</span><span class="sxs-lookup"><span data-stu-id="494b8-174">The runbooks will [output a message](automation-runbook-output-and-messages.md) for each virtual machine indicating whether or not the start or stop instruction was successfully submitted.</span></span>  <span data-ttu-id="494b8-175">È possibile cercare una stringa specifica nell'output per determinare il risultato per ogni runbook.</span><span class="sxs-lookup"><span data-stu-id="494b8-175">You can look for a specific string in the output to determine the result for each runbook.</span></span>  <span data-ttu-id="494b8-176">Nella tabella seguente sono elencate le stringhe di output possibili.</span><span class="sxs-lookup"><span data-stu-id="494b8-176">The possible output strings are listed in the following table.</span></span>

| <span data-ttu-id="494b8-177">Runbook</span><span class="sxs-lookup"><span data-stu-id="494b8-177">Runbook</span></span> | <span data-ttu-id="494b8-178">Condizione</span><span class="sxs-lookup"><span data-stu-id="494b8-178">Condition</span></span> | <span data-ttu-id="494b8-179">Message</span><span class="sxs-lookup"><span data-stu-id="494b8-179">Message</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="494b8-180">Start-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="494b8-180">Start-AzureVMs</span></span> |<span data-ttu-id="494b8-181">Macchina virtuale già in esecuzione</span><span class="sxs-lookup"><span data-stu-id="494b8-181">Virtual machine is already running</span></span> |<span data-ttu-id="494b8-182">MyVM is already running</span><span class="sxs-lookup"><span data-stu-id="494b8-182">MyVM is already running</span></span> |
| <span data-ttu-id="494b8-183">Start-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="494b8-183">Start-AzureVMs</span></span> |<span data-ttu-id="494b8-184">Richiesta di avvio per la macchina virtuale inviata correttamente</span><span class="sxs-lookup"><span data-stu-id="494b8-184">Start request for virtual machine successfully submitted</span></span> |<span data-ttu-id="494b8-185">MyVM has been started</span><span class="sxs-lookup"><span data-stu-id="494b8-185">MyVM has been started</span></span> |
| <span data-ttu-id="494b8-186">Start-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="494b8-186">Start-AzureVMs</span></span> |<span data-ttu-id="494b8-187">Richiesta di avvio per la macchina virtuale non riuscita</span><span class="sxs-lookup"><span data-stu-id="494b8-187">Start request for virtual machine failed</span></span> |<span data-ttu-id="494b8-188">MyVM failed to start</span><span class="sxs-lookup"><span data-stu-id="494b8-188">MyVM failed to start</span></span> |
| <span data-ttu-id="494b8-189">Stop-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="494b8-189">Stop-AzureVMs</span></span> |<span data-ttu-id="494b8-190">Macchina virtuale già arrestata</span><span class="sxs-lookup"><span data-stu-id="494b8-190">Virtual machine is already stopped</span></span> |<span data-ttu-id="494b8-191">MyVM is already stopped</span><span class="sxs-lookup"><span data-stu-id="494b8-191">MyVM is already stopped</span></span> |
| <span data-ttu-id="494b8-192">Stop-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="494b8-192">Stop-AzureVMs</span></span> |<span data-ttu-id="494b8-193">Richiesta di arresto per la macchina virtuale inviata correttamente</span><span class="sxs-lookup"><span data-stu-id="494b8-193">Stop request for virtual machine successfully submitted</span></span> |<span data-ttu-id="494b8-194">MyVM è stata già arrestata</span><span class="sxs-lookup"><span data-stu-id="494b8-194">MyVM has been stopped</span></span> |
| <span data-ttu-id="494b8-195">Stop-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="494b8-195">Stop-AzureVMs</span></span> |<span data-ttu-id="494b8-196">Richiesta di arresto la macchina virtuale non riuscita</span><span class="sxs-lookup"><span data-stu-id="494b8-196">Stop request for virtual machine failed</span></span> |<span data-ttu-id="494b8-197">Errore di avvio di MyVM</span><span class="sxs-lookup"><span data-stu-id="494b8-197">MyVM failed to stop</span></span> |

<span data-ttu-id="494b8-198">Il frammento di codice di un runbook seguente ad esempio tenta di avviare tutte le macchine virtuali con nome di servizio *MyServiceName*.</span><span class="sxs-lookup"><span data-stu-id="494b8-198">For example, the following code snippet from a runbook attempts to start all virtual machines with the service name *MyServiceName*.</span></span>  <span data-ttu-id="494b8-199">Se una delle azioni di avvio ha esito negativo, è possibile eseguire le azioni di errore.</span><span class="sxs-lookup"><span data-stu-id="494b8-199">If any of the start requests fail, then error actions can be taken.</span></span>

    $results = Start-AzureVMs -ServiceName "MyServiceName"
    foreach ($result in $results) {
        if ($result -like "* has been started" ) {
            # Action to take in case of success.
        }
        else {
            # Action to take in case of error.
        }
    }


## <a name="detailed-breakdown"></a><span data-ttu-id="494b8-200">Scomposizione dettagliata</span><span class="sxs-lookup"><span data-stu-id="494b8-200">Detailed breakdown</span></span>
<span data-ttu-id="494b8-201">Di seguito è riportata una scomposizione dettagliata dei runbook di questo scenario.</span><span class="sxs-lookup"><span data-stu-id="494b8-201">Following is a detailed breakdown of the runbooks in this scenario.</span></span>  <span data-ttu-id="494b8-202">È possibile usare queste informazioni per personalizzare i runbook o semplicemente per acquisire familiarità per la creazione di scenari di automazione personalizzati.</span><span class="sxs-lookup"><span data-stu-id="494b8-202">You can use this information to either customize the runbooks or just to learn from them for authoring your own automation scenarios.</span></span>

### <a name="parameters"></a><span data-ttu-id="494b8-203">Parametri</span><span class="sxs-lookup"><span data-stu-id="494b8-203">Parameters</span></span>
    param (
        [Parameter(Mandatory=$false)]
        [String]  $AzureCredentialAssetName = 'AzureCredential',

        [Parameter(Mandatory=$false)]
        [String] $AzureSubscriptionIdAssetName = 'AzureSubscriptionId',

        [Parameter(Mandatory=$false)]
        [String] $ServiceName
    )

<span data-ttu-id="494b8-204">Il flusso di lavoro inizia ottenendo i valori per i [parametri di input](#using-the-scenario).</span><span class="sxs-lookup"><span data-stu-id="494b8-204">The workflow starts by getting the values for the [input parameters](#using-the-scenario).</span></span>  <span data-ttu-id="494b8-205">Se non sono specificati i nomi degli asset verranno usati i nomi predefiniti.</span><span class="sxs-lookup"><span data-stu-id="494b8-205">If the asset names are not provided then default names are used.</span></span>

### <a name="output"></a><span data-ttu-id="494b8-206">Output</span><span class="sxs-lookup"><span data-stu-id="494b8-206">Output</span></span>
    # Returns strings with status messages
    [OutputType([String])]

<span data-ttu-id="494b8-207">Questa riga dichiara che l'output del runbook sarà una stringa.</span><span class="sxs-lookup"><span data-stu-id="494b8-207">This line declares that the output of the runbook will be a string.</span></span>  <span data-ttu-id="494b8-208">Non è obbligatoria, ma è una procedura consigliata se il runbook viene usato come [runbook figlio](automation-child-runbooks.md) , affinché un runbook padre conosca il tipo di output previsto.</span><span class="sxs-lookup"><span data-stu-id="494b8-208">This is not required but is a best practice for when the runbook is used as a [child runbook](automation-child-runbooks.md) so that a parent runbook will know the output type to expect.</span></span>

### <a name="authentication"></a><span data-ttu-id="494b8-209">Autenticazione</span><span class="sxs-lookup"><span data-stu-id="494b8-209">Authentication</span></span>
    # Connect to Azure and select the subscription to work against
    $Cred = Get-AutomationPSCredential -Name $AzureCredentialAssetName
    $null = Add-AzureAccount -Credential $Cred -ErrorAction Stop
    $SubId = Get-AutomationVariable -Name $AzureSubscriptionIdAssetName
    $null = Select-AzureSubscription -SubscriptionId $SubId -ErrorAction Stop

<span data-ttu-id="494b8-210">Le righe successive impostano le [credenziali](automation-credentials.md) e la sottoscrizione di Azure che verranno usate per il resto del runbook.</span><span class="sxs-lookup"><span data-stu-id="494b8-210">The next lines set the [credentials](automation-credentials.md) and Azure subscription that will be used for the rest of the runbook.</span></span>
<span data-ttu-id="494b8-211">Viene usato prima **Get-AutomationPSCredential** per ottenere l'asset contenente le credenziali con l'accesso per l'avvio e l'arresto delle macchine virtuali nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="494b8-211">First we use **Get-AutomationPSCredential** to get the asset that holds the credentials with access to start and stop virtual machines in the Azure subscription.</span></span> <span data-ttu-id="494b8-212">**Add-AzureAccount** usa quindi questo asset per impostare le credenziali.</span><span class="sxs-lookup"><span data-stu-id="494b8-212">**Add-AzureAccount** then uses this asset to set the credentials.</span></span>  <span data-ttu-id="494b8-213">L'output viene assegnato a una variabile fittizia in modo da non essere incluso nell'output del runbook.</span><span class="sxs-lookup"><span data-stu-id="494b8-213">The output is assigned to a dummy variable so that it isn't included in the runbook output.</span></span>  

<span data-ttu-id="494b8-214">L'asset di tipo variabile con l'ID sottoscrizione viene quindi recuperato con **Get-AutomationVariable** e il set di sottoscrizioni con **Select-AzureSubscription**.</span><span class="sxs-lookup"><span data-stu-id="494b8-214">The variable asset with the subscription ID is then retrieved with **Get-AutomationVariable** and the subscription set with **Select-AzureSubscription**.</span></span>

### <a name="get-vms"></a><span data-ttu-id="494b8-215">Ottenere le macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="494b8-215">Get VMs</span></span>
    # If there is a specific cloud service, then get all VMs in the service,
    # otherwise get all VMs in the subscription.
    if ($ServiceName)
    {
        $VMs = Get-AzureVM -ServiceName $ServiceName
    }
    else
    {
        $VMs = Get-AzureVM
    }

<span data-ttu-id="494b8-216">**Get-AzureVM** viene usato per recuperare le macchine virtuali che verranno usate dal runbook.</span><span class="sxs-lookup"><span data-stu-id="494b8-216">**Get-AzureVM** is used to retrieve the virtual machines the runbook will work with.</span></span>  <span data-ttu-id="494b8-217">Se viene specificato un valore nella variabile di input **ServiceName** , verranno recuperate solo le macchine virtuali con lo stesso nome di servizio.</span><span class="sxs-lookup"><span data-stu-id="494b8-217">If a value is provided in the **ServiceName** input variable, then only the virtual machines with that service name are retrieved.</span></span>  <span data-ttu-id="494b8-218">Se invece la variabile **ServiceName** è vuota, verranno recuperate tutte le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="494b8-218">If **ServiceName** is empty, then all virtual machines are retrieved.</span></span>

### <a name="startstop-virtual-machines-and-send-output"></a><span data-ttu-id="494b8-219">Avviare/arrestare le macchine virtuali e inviare l'output</span><span class="sxs-lookup"><span data-stu-id="494b8-219">Start/Stop virtual machines and send output</span></span>
    # Start each of the stopped VMs
    foreach ($VM in $VMs)
    {
        if ($VM.PowerState -eq "Started")
        {
            # The VM is already started, so send notice
            Write-Output ($VM.InstanceName + " is already running")
        }
        else
        {
            # The VM needs to be started
            $StartRtn = Start-AzureVM -Name $VM.Name -ServiceName $VM.ServiceName -ErrorAction Continue

            if ($StartRtn.OperationStatus -ne 'Succeeded')
            {
                # The VM failed to start, so send notice
                Write-Output ($VM.InstanceName + " failed to start")
            }
            else
            {
                # The VM started, so send notice
                Write-Output ($VM.InstanceName + " has been started")
            }
        }
    }

<span data-ttu-id="494b8-220">Le righe successive eseguono i passaggi per ogni macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="494b8-220">The next lines step through each virtual machine.</span></span>  <span data-ttu-id="494b8-221">Viene prima verificata l'impostazione di **PowerState** della macchina virtuale per controllare se è già in esecuzione o arrestata, a seconda del runbook.</span><span class="sxs-lookup"><span data-stu-id="494b8-221">First the **PowerState** of the virtual machine is checked to see if it is already running or stopped, depending on the runbook.</span></span>  <span data-ttu-id="494b8-222">Se lo stato è già quello di destinazione, viene restituito un messaggio per l'output e il runbook termina.</span><span class="sxs-lookup"><span data-stu-id="494b8-222">If it is already in the target state, then a message is sent to output, and the runbook ends.</span></span>  <span data-ttu-id="494b8-223">In caso contrario, viene usato **Start-AzureVM** o **Stop-AzureVM** per tentare di avviare o arrestare la macchina virtuale con il risultato della richiesta archiviato in una variabile.</span><span class="sxs-lookup"><span data-stu-id="494b8-223">If not, then **Start-AzureVM** or **Stop-AzureVM** is used to attempt to start or stop the virtual machine with the result of the request stored to a variable.</span></span>  <span data-ttu-id="494b8-224">Verrà quindi restituito all'output un messaggio che specifica se la richiesta di avvio o di arresto è stata inviata correttamente.</span><span class="sxs-lookup"><span data-stu-id="494b8-224">A message is then sent to output specifying whether the request to start or stop was submitted successfully.</span></span>

## <a name="next-steps"></a><span data-ttu-id="494b8-225">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="494b8-225">Next steps</span></span>
* <span data-ttu-id="494b8-226">Per ulteriori informazioni sull’utilizzo dei runbook figlio, vedere [Runbook figlio in Automazione di Azure](automation-child-runbooks.md)</span><span class="sxs-lookup"><span data-stu-id="494b8-226">To learn more about working with child runbooks, see [Child runbooks in Azure Automation](automation-child-runbooks.md)</span></span>
* <span data-ttu-id="494b8-227">Per ulteriori informazioni sui messaggi di output durante l'esecuzione di runbook e la registrazione per la risoluzione dei problemi, vedere [Output di runbook e messaggi in Automazione di Azure](automation-runbook-output-and-messages.md)</span><span class="sxs-lookup"><span data-stu-id="494b8-227">To learn more about output messages during runbook execution and logging to help troubleshoot, see [Runbook output and messages in Azure Automation](automation-runbook-output-and-messages.md)</span></span>

