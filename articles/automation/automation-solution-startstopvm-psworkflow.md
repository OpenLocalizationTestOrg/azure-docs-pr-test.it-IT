---
title: aaaStarting e l'arresto di macchine virtuali con automazione di Azure - flusso di lavoro PowerShell | Documenti Microsoft
description: Versione con interfaccia grafica dello scenario di automazione di Azure inclusi runbook toostart e arrestare macchine virtuali classiche.
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
redirect_document_id: False
ms.openlocfilehash: 273631c7fc5ddb989b3bbdc82b470ac3af6ee482
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---starting-and-stopping-virtual-machines"></a><span data-ttu-id="4b4e0-103">Scenario di Automazione di Azure - Avvio e arresto delle macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="4b4e0-103">Azure Automation scenario - starting and stopping virtual machines</span></span>
<span data-ttu-id="4b4e0-104">Questo scenario di automazione di Azure include runbook toostart e arrestare macchine virtuali classiche.</span><span class="sxs-lookup"><span data-stu-id="4b4e0-104">This Azure Automation scenario includes runbooks toostart and stop classic virtual machines.</span></span>  <span data-ttu-id="4b4e0-105">È possibile utilizzare questo scenario per hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="4b4e0-105">You can use this scenario for any of hello following:</span></span>  

* <span data-ttu-id="4b4e0-106">Usare i runbook di hello senza alcuna modifica nel proprio ambiente.</span><span class="sxs-lookup"><span data-stu-id="4b4e0-106">Use hello runbooks without modification in your own environment.</span></span>
* <span data-ttu-id="4b4e0-107">Modificare hello runbook tooperform personalizzato funzionalità.</span><span class="sxs-lookup"><span data-stu-id="4b4e0-107">Modify hello runbooks tooperform customized functionality.</span></span>  
* <span data-ttu-id="4b4e0-108">Chiamare hello runbook da un altro runbook come parte di una soluzione completa.</span><span class="sxs-lookup"><span data-stu-id="4b4e0-108">Call hello runbooks from another runbook as part of an overall solution.</span></span>
* <span data-ttu-id="4b4e0-109">Usare i runbook di hello come creazione concetti dei runbook toolearn esercitazioni.</span><span class="sxs-lookup"><span data-stu-id="4b4e0-109">Use hello runbooks as tutorials toolearn runbook authoring concepts.</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="4b4e0-110">Grafico</span><span class="sxs-lookup"><span data-stu-id="4b4e0-110">Graphical</span></span>](automation-solution-startstopvm-graphical.md)
> * [<span data-ttu-id="4b4e0-111">Flusso di lavoro PowerShell</span><span class="sxs-lookup"><span data-stu-id="4b4e0-111">PowerShell Workflow</span></span>](automation-solution-startstopvm-psworkflow.md)
> 
> 

<span data-ttu-id="4b4e0-112">Si tratta di hello versione del runbook del flusso di lavoro di PowerShell di questo scenario.</span><span class="sxs-lookup"><span data-stu-id="4b4e0-112">This is hello PowerShell Workflow runbook version of this scenario.</span></span> <span data-ttu-id="4b4e0-113">È disponibile anche usando [runbook grafici](automation-solution-startstopvm-graphical.md).</span><span class="sxs-lookup"><span data-stu-id="4b4e0-113">It is also available using [graphical runbooks](automation-solution-startstopvm-graphical.md).</span></span>

## <a name="getting-hello-scenario"></a><span data-ttu-id="4b4e0-114">Scenario di recupero hello</span><span class="sxs-lookup"><span data-stu-id="4b4e0-114">Getting hello scenario</span></span>
<span data-ttu-id="4b4e0-115">Questo scenario è costituito da due runbook del flusso di lavoro di PowerShell che è possibile scaricare da hello seguenti collegamenti.</span><span class="sxs-lookup"><span data-stu-id="4b4e0-115">This scenario consists of two PowerShell Workflow runbooks that you can download from hello following links.</span></span>  <span data-ttu-id="4b4e0-116">Vedere hello [versione grafica](automation-solution-startstopvm-graphical.md) di questo scenario per i runbook grafici toohello di collegamenti.</span><span class="sxs-lookup"><span data-stu-id="4b4e0-116">See hello [graphical version](automation-solution-startstopvm-graphical.md) of this scenario for links toohello graphical runbooks.</span></span>

| <span data-ttu-id="4b4e0-117">Runbook</span><span class="sxs-lookup"><span data-stu-id="4b4e0-117">Runbook</span></span> | <span data-ttu-id="4b4e0-118">Collegamento</span><span class="sxs-lookup"><span data-stu-id="4b4e0-118">Link</span></span> | <span data-ttu-id="4b4e0-119">Tipo</span><span class="sxs-lookup"><span data-stu-id="4b4e0-119">Type</span></span> | <span data-ttu-id="4b4e0-120">Descrizione</span><span class="sxs-lookup"><span data-stu-id="4b4e0-120">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="4b4e0-121">Start-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="4b4e0-121">Start-AzureVMs</span></span> |[<span data-ttu-id="4b4e0-122">Avviare le macchine virtuali classiche di Azure</span><span class="sxs-lookup"><span data-stu-id="4b4e0-122">Start Azure Classic VMs</span></span>](https://gallery.technet.microsoft.com/Start-Azure-Classic-VMs-86ef746b) |<span data-ttu-id="4b4e0-123">Flusso di lavoro PowerShell</span><span class="sxs-lookup"><span data-stu-id="4b4e0-123">PowerShell Workflow</span></span> |<span data-ttu-id="4b4e0-124">Avvia tutte le macchine virtuali classiche in una sottoscrizione di Azure o tutte le macchine virtuali con un nome di servizio specifico.</span><span class="sxs-lookup"><span data-stu-id="4b4e0-124">Starts all classic virtual machines in an Azure subscriptionor all virtual machines with a particular service name.</span></span> |
| <span data-ttu-id="4b4e0-125">Stop-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="4b4e0-125">Stop-AzureVMs</span></span> |[<span data-ttu-id="4b4e0-126">Arrestare le macchine virtuali classiche di Azure</span><span class="sxs-lookup"><span data-stu-id="4b4e0-126">Stop Azure Classic VMs</span></span>](https://gallery.technet.microsoft.com/Stop-Azure-Classic-VMs-7a4ae43e) |<span data-ttu-id="4b4e0-127">Flusso di lavoro PowerShell</span><span class="sxs-lookup"><span data-stu-id="4b4e0-127">PowerShell Workflow</span></span> |<span data-ttu-id="4b4e0-128">Arresta tutte le macchine virtuali in un account di automazione o tutte le macchine virtuali con un nome di servizio specifico.</span><span class="sxs-lookup"><span data-stu-id="4b4e0-128">Stops all virtual machines in an automation account or all virtual machines with a particular service name.</span></span> |

## <a name="installing-and-configuring-hello-scenario"></a><span data-ttu-id="4b4e0-129">Installazione e configurazione di uno scenario di hello</span><span class="sxs-lookup"><span data-stu-id="4b4e0-129">Installing and configuring hello scenario</span></span>
### <a name="1-install-hello-runbooks"></a><span data-ttu-id="4b4e0-130">1. Installare i runbook hello</span><span class="sxs-lookup"><span data-stu-id="4b4e0-130">1. Install hello runbooks</span></span>
<span data-ttu-id="4b4e0-131">Dopo aver scaricato hello runbook, è possibile importarli nella procedura hello in [importazione di un Runbook](http://msdn.microsoft.com/library/dn643637.aspx#ImportRunbook).</span><span class="sxs-lookup"><span data-stu-id="4b4e0-131">After downloading hello runbooks, you can import them using hello procedure in [Importing a Runbook](http://msdn.microsoft.com/library/dn643637.aspx#ImportRunbook).</span></span>

### <a name="2-review-hello-description-and-requirements"></a><span data-ttu-id="4b4e0-132">2. Descrizione di revisione hello e requisiti</span><span class="sxs-lookup"><span data-stu-id="4b4e0-132">2. Review hello description and requirements</span></span>
<span data-ttu-id="4b4e0-133">i runbook Hello includono il testo della Guida in linea impostata come commento che include una descrizione e le risorse necessarie.</span><span class="sxs-lookup"><span data-stu-id="4b4e0-133">hello runbooks include commented help text that includes a description and required assets.</span></span>  <span data-ttu-id="4b4e0-134">È inoltre possibile ottenere hello stesse informazioni in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="4b4e0-134">You can also get hello same information from this article.</span></span>

### <a name="3-configure-assets"></a><span data-ttu-id="4b4e0-135">3. Configurare gli asset</span><span class="sxs-lookup"><span data-stu-id="4b4e0-135">3. Configure assets</span></span>
<span data-ttu-id="4b4e0-136">i runbook di Hello richiedono hello seguenti risorse che è necessario creare e popolare con i valori appropriati.</span><span class="sxs-lookup"><span data-stu-id="4b4e0-136">hello runbooks require hello following assets that you must create and populate with appropriate values.</span></span>

| <span data-ttu-id="4b4e0-137">Tipo di risorsa</span><span class="sxs-lookup"><span data-stu-id="4b4e0-137">Asset Type</span></span> | <span data-ttu-id="4b4e0-138">Nome dell’asset</span><span class="sxs-lookup"><span data-stu-id="4b4e0-138">Asset Name</span></span> | <span data-ttu-id="4b4e0-139">Descrizione</span><span class="sxs-lookup"><span data-stu-id="4b4e0-139">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="4b4e0-140">Credenziali</span><span class="sxs-lookup"><span data-stu-id="4b4e0-140">Credential</span></span> |<span data-ttu-id="4b4e0-141">AzureCredential</span><span class="sxs-lookup"><span data-stu-id="4b4e0-141">AzureCredential</span></span> |<span data-ttu-id="4b4e0-142">Contiene le credenziali per un account che dispone di autorità toostart e arrestare le macchine virtuali nella sottoscrizione di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="4b4e0-142">Contains credentials for an account that has authority toostart and stop virtual machines in hello Azure subscription.</span></span>  <span data-ttu-id="4b4e0-143">In alternativa, è possibile specificare un altro asset delle credenziali in hello **credenziali** parametro di hello **Add-AzureAccount** attività.</span><span class="sxs-lookup"><span data-stu-id="4b4e0-143">Alternatively, you can specify another credential asset in hello **Credential** parameter of hello **Add-AzureAccount** activity.</span></span> |
| <span data-ttu-id="4b4e0-144">Variabile</span><span class="sxs-lookup"><span data-stu-id="4b4e0-144">Variable</span></span> |<span data-ttu-id="4b4e0-145">AzureSubscriptionId</span><span class="sxs-lookup"><span data-stu-id="4b4e0-145">AzureSubscriptionId</span></span> |<span data-ttu-id="4b4e0-146">Contiene l'ID sottoscrizione hello della sottoscrizione Azure.</span><span class="sxs-lookup"><span data-stu-id="4b4e0-146">Contains hello subscription ID of your Azure subscription.</span></span> |

## <a name="using-hello-scenario"></a><span data-ttu-id="4b4e0-147">Uno scenario di hello</span><span class="sxs-lookup"><span data-stu-id="4b4e0-147">Using hello scenario</span></span>
### <a name="parameters"></a><span data-ttu-id="4b4e0-148">parameters</span><span class="sxs-lookup"><span data-stu-id="4b4e0-148">Parameters</span></span>
<span data-ttu-id="4b4e0-149">ogni runbook Hello avere hello seguenti parametri.</span><span class="sxs-lookup"><span data-stu-id="4b4e0-149">hello runbooks each have hello following parameters.</span></span>  <span data-ttu-id="4b4e0-150">È necessario fornire valori per tutti i parametri obbligatori ed è possibile facoltativamente specificare i valori per gli altri parametri a seconda delle esigenze.</span><span class="sxs-lookup"><span data-stu-id="4b4e0-150">You must provide values for any mandatory parameters and can optionally provide values for other parameters depending on your requirements.</span></span>

| <span data-ttu-id="4b4e0-151">Parametro</span><span class="sxs-lookup"><span data-stu-id="4b4e0-151">Parameter</span></span> | <span data-ttu-id="4b4e0-152">Tipo</span><span class="sxs-lookup"><span data-stu-id="4b4e0-152">Type</span></span> | <span data-ttu-id="4b4e0-153">Mandatory</span><span class="sxs-lookup"><span data-stu-id="4b4e0-153">Mandatory</span></span> | <span data-ttu-id="4b4e0-154">Descrizione</span><span class="sxs-lookup"><span data-stu-id="4b4e0-154">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="4b4e0-155">ServiceName</span><span class="sxs-lookup"><span data-stu-id="4b4e0-155">ServiceName</span></span> |<span data-ttu-id="4b4e0-156">string</span><span class="sxs-lookup"><span data-stu-id="4b4e0-156">string</span></span> |<span data-ttu-id="4b4e0-157">No</span><span class="sxs-lookup"><span data-stu-id="4b4e0-157">No</span></span> |<span data-ttu-id="4b4e0-158">Se viene specificato un valore, verranno avviate o arrestate tutte le macchine virtuali con lo stesso nome di servizio.</span><span class="sxs-lookup"><span data-stu-id="4b4e0-158">If a value is provided, then all virtual machines with that service name are started or stopped.</span></span>  <span data-ttu-id="4b4e0-159">Se non viene fornito alcun valore, tutte le macchine virtuali classiche nella sottoscrizione di Azure hello sono avviate o arrestate.</span><span class="sxs-lookup"><span data-stu-id="4b4e0-159">If no value is provided, then all classic virtual machines in hello Azure subscription are started or stopped.</span></span> |
| <span data-ttu-id="4b4e0-160">AzureSubscriptionIdAssetName</span><span class="sxs-lookup"><span data-stu-id="4b4e0-160">AzureSubscriptionIdAssetName</span></span> |<span data-ttu-id="4b4e0-161">string</span><span class="sxs-lookup"><span data-stu-id="4b4e0-161">string</span></span> |<span data-ttu-id="4b4e0-162">No</span><span class="sxs-lookup"><span data-stu-id="4b4e0-162">No</span></span> |<span data-ttu-id="4b4e0-163">Contiene il nome di hello di hello [asset della variabile](#installing-and-configuring-the-scenario) che contiene l'ID sottoscrizione hello della sottoscrizione Azure.</span><span class="sxs-lookup"><span data-stu-id="4b4e0-163">Contains hello name of hello [variable asset](#installing-and-configuring-the-scenario) that contains hello subscription ID of your Azure subscription.</span></span>  <span data-ttu-id="4b4e0-164">Se non si specifica un valore, verrà usato *AzureSubscriptionId* .</span><span class="sxs-lookup"><span data-stu-id="4b4e0-164">If you don't specify a value, *AzureSubscriptionId* is used.</span></span> |
| <span data-ttu-id="4b4e0-165">AzureCredentialAssetName</span><span class="sxs-lookup"><span data-stu-id="4b4e0-165">AzureCredentialAssetName</span></span> |<span data-ttu-id="4b4e0-166">string</span><span class="sxs-lookup"><span data-stu-id="4b4e0-166">string</span></span> |<span data-ttu-id="4b4e0-167">No</span><span class="sxs-lookup"><span data-stu-id="4b4e0-167">No</span></span> |<span data-ttu-id="4b4e0-168">Contiene il nome di hello di hello [asset delle credenziali](#installing-and-configuring-the-scenario) che contiene le credenziali di hello per toouse runbook hello.</span><span class="sxs-lookup"><span data-stu-id="4b4e0-168">Contains hello name of hello [credential asset](#installing-and-configuring-the-scenario) that contains hello credentials for hello runbook toouse.</span></span>  <span data-ttu-id="4b4e0-169">Se non si specifica un valore, verrà usato *AzureCredential* .</span><span class="sxs-lookup"><span data-stu-id="4b4e0-169">If you don't specify a value, *AzureCredential* is used.</span></span> |

### <a name="starting-hello-runbooks"></a><span data-ttu-id="4b4e0-170">Esecuzione dei runbook hello</span><span class="sxs-lookup"><span data-stu-id="4b4e0-170">Starting hello runbooks</span></span>
<span data-ttu-id="4b4e0-171">È possibile utilizzare uno dei metodi di hello in [avvio di un runbook in automazione di Azure](automation-starting-a-runbook.md) toostart uno dei runbook hello in questo scenario.</span><span class="sxs-lookup"><span data-stu-id="4b4e0-171">You can use any of hello methods in [Starting a runbook in Azure Automation](automation-starting-a-runbook.md) toostart either of hello runbooks in this scenario.</span></span>

<span data-ttu-id="4b4e0-172">Hello seguenti comandi di esempio utilizza Windows PowerShell toorun **StartAzureVMs** toostart tutte le macchine virtuali con il nome di servizio hello *MyVMService*.</span><span class="sxs-lookup"><span data-stu-id="4b4e0-172">hello following sample commands uses Windows PowerShell toorun **StartAzureVMs** toostart all virtual machines with hello service name *MyVMService*.</span></span>

    $params = @{"ServiceName"="MyVMService"}
    Start-AzureAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Start-AzureVMs" –Parameters $params

### <a name="output"></a><span data-ttu-id="4b4e0-173">Output</span><span class="sxs-lookup"><span data-stu-id="4b4e0-173">Output</span></span>
<span data-ttu-id="4b4e0-174">i runbook Hello verranno [un messaggio di output](automation-runbook-output-and-messages.md) per ogni macchina virtuale che indica se hello avvio o l'istruzione stop è stata inviata correttamente.</span><span class="sxs-lookup"><span data-stu-id="4b4e0-174">hello runbooks will [output a message](automation-runbook-output-and-messages.md) for each virtual machine indicating whether or not hello start or stop instruction was successfully submitted.</span></span>  <span data-ttu-id="4b4e0-175">È possibile cercare una stringa specifica in hello output toodetermine hello risultato per ogni runbook.</span><span class="sxs-lookup"><span data-stu-id="4b4e0-175">You can look for a specific string in hello output toodetermine hello result for each runbook.</span></span>  <span data-ttu-id="4b4e0-176">Nella hello nella tabella seguente sono elencate le stringhe di output possibili Hello.</span><span class="sxs-lookup"><span data-stu-id="4b4e0-176">hello possible output strings are listed in hello following table.</span></span>

| <span data-ttu-id="4b4e0-177">Runbook</span><span class="sxs-lookup"><span data-stu-id="4b4e0-177">Runbook</span></span> | <span data-ttu-id="4b4e0-178">Condizione</span><span class="sxs-lookup"><span data-stu-id="4b4e0-178">Condition</span></span> | <span data-ttu-id="4b4e0-179">Message</span><span class="sxs-lookup"><span data-stu-id="4b4e0-179">Message</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="4b4e0-180">Start-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="4b4e0-180">Start-AzureVMs</span></span> |<span data-ttu-id="4b4e0-181">Macchina virtuale già in esecuzione</span><span class="sxs-lookup"><span data-stu-id="4b4e0-181">Virtual machine is already running</span></span> |<span data-ttu-id="4b4e0-182">MyVM is already running</span><span class="sxs-lookup"><span data-stu-id="4b4e0-182">MyVM is already running</span></span> |
| <span data-ttu-id="4b4e0-183">Start-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="4b4e0-183">Start-AzureVMs</span></span> |<span data-ttu-id="4b4e0-184">Richiesta di avvio per la macchina virtuale inviata correttamente</span><span class="sxs-lookup"><span data-stu-id="4b4e0-184">Start request for virtual machine successfully submitted</span></span> |<span data-ttu-id="4b4e0-185">MyVM has been started</span><span class="sxs-lookup"><span data-stu-id="4b4e0-185">MyVM has been started</span></span> |
| <span data-ttu-id="4b4e0-186">Start-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="4b4e0-186">Start-AzureVMs</span></span> |<span data-ttu-id="4b4e0-187">Richiesta di avvio per la macchina virtuale non riuscita</span><span class="sxs-lookup"><span data-stu-id="4b4e0-187">Start request for virtual machine failed</span></span> |<span data-ttu-id="4b4e0-188">Toostart MyVM non riuscita</span><span class="sxs-lookup"><span data-stu-id="4b4e0-188">MyVM failed toostart</span></span> |
| <span data-ttu-id="4b4e0-189">Stop-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="4b4e0-189">Stop-AzureVMs</span></span> |<span data-ttu-id="4b4e0-190">Macchina virtuale già arrestata</span><span class="sxs-lookup"><span data-stu-id="4b4e0-190">Virtual machine is already stopped</span></span> |<span data-ttu-id="4b4e0-191">MyVM is already stopped</span><span class="sxs-lookup"><span data-stu-id="4b4e0-191">MyVM is already stopped</span></span> |
| <span data-ttu-id="4b4e0-192">Stop-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="4b4e0-192">Stop-AzureVMs</span></span> |<span data-ttu-id="4b4e0-193">Richiesta di arresto per la macchina virtuale inviata correttamente</span><span class="sxs-lookup"><span data-stu-id="4b4e0-193">Stop request for virtual machine successfully submitted</span></span> |<span data-ttu-id="4b4e0-194">MyVM è stata già arrestata</span><span class="sxs-lookup"><span data-stu-id="4b4e0-194">MyVM has been stopped</span></span> |
| <span data-ttu-id="4b4e0-195">Stop-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="4b4e0-195">Stop-AzureVMs</span></span> |<span data-ttu-id="4b4e0-196">Richiesta di arresto la macchina virtuale non riuscita</span><span class="sxs-lookup"><span data-stu-id="4b4e0-196">Stop request for virtual machine failed</span></span> |<span data-ttu-id="4b4e0-197">Toostop MyVM non riuscita</span><span class="sxs-lookup"><span data-stu-id="4b4e0-197">MyVM failed toostop</span></span> |

<span data-ttu-id="4b4e0-198">Ad esempio, hello seguente frammento di codice da un runbook tenta toostart tutte le macchine virtuali con il nome di servizio hello *MyServiceName*.</span><span class="sxs-lookup"><span data-stu-id="4b4e0-198">For example, hello following code snippet from a runbook attempts toostart all virtual machines with hello service name *MyServiceName*.</span></span>  <span data-ttu-id="4b4e0-199">Se uno di hello avvia le richieste di errore, è possono eseguire le azioni di errore.</span><span class="sxs-lookup"><span data-stu-id="4b4e0-199">If any of hello start requests fail, then error actions can be taken.</span></span>

    $results = Start-AzureVMs -ServiceName "MyServiceName"
    foreach ($result in $results) {
        if ($result -like "* has been started" ) {
            # Action tootake in case of success.
        }
        else {
            # Action tootake in case of error.
        }
    }


## <a name="detailed-breakdown"></a><span data-ttu-id="4b4e0-200">Scomposizione dettagliata</span><span class="sxs-lookup"><span data-stu-id="4b4e0-200">Detailed breakdown</span></span>
<span data-ttu-id="4b4e0-201">Di seguito è una suddivisione dettagliata dei runbook hello in questo scenario.</span><span class="sxs-lookup"><span data-stu-id="4b4e0-201">Following is a detailed breakdown of hello runbooks in this scenario.</span></span>  <span data-ttu-id="4b4e0-202">È possibile utilizzare queste informazioni tooeither personalizzare runbook hello o toolearn solo da essi per la creazione di propri scenari di automazione.</span><span class="sxs-lookup"><span data-stu-id="4b4e0-202">You can use this information tooeither customize hello runbooks or just toolearn from them for authoring your own automation scenarios.</span></span>

### <a name="parameters"></a><span data-ttu-id="4b4e0-203">parameters</span><span class="sxs-lookup"><span data-stu-id="4b4e0-203">Parameters</span></span>
    param (
        [Parameter(Mandatory=$false)]
        [String]  $AzureCredentialAssetName = 'AzureCredential',

        [Parameter(Mandatory=$false)]
        [String] $AzureSubscriptionIdAssetName = 'AzureSubscriptionId',

        [Parameter(Mandatory=$false)]
        [String] $ServiceName
    )

<span data-ttu-id="4b4e0-204">Hello flusso di lavoro viene avviata tramite il recupero dei valori hello per hello [i parametri di input](#using-the-scenario).</span><span class="sxs-lookup"><span data-stu-id="4b4e0-204">hello workflow starts by getting hello values for hello [input parameters](#using-the-scenario).</span></span>  <span data-ttu-id="4b4e0-205">Se non sono specificati i nomi delle risorse hello vengono usati nomi predefiniti.</span><span class="sxs-lookup"><span data-stu-id="4b4e0-205">If hello asset names are not provided then default names are used.</span></span>

### <a name="output"></a><span data-ttu-id="4b4e0-206">Output</span><span class="sxs-lookup"><span data-stu-id="4b4e0-206">Output</span></span>
    # Returns strings with status messages
    [OutputType([String])]

<span data-ttu-id="4b4e0-207">Questa riga dichiara che l'output di hello del runbook hello sarà una stringa.</span><span class="sxs-lookup"><span data-stu-id="4b4e0-207">This line declares that hello output of hello runbook will be a string.</span></span>  <span data-ttu-id="4b4e0-208">Non è obbligatorio ma è consigliabile per quando il runbook hello viene utilizzato come un [runbook figlio](automation-child-runbooks.md) in modo che un runbook padre conoscano l'output di hello digitare tooexpect.</span><span class="sxs-lookup"><span data-stu-id="4b4e0-208">This is not required but is a best practice for when hello runbook is used as a [child runbook](automation-child-runbooks.md) so that a parent runbook will know hello output type tooexpect.</span></span>

### <a name="authentication"></a><span data-ttu-id="4b4e0-209">Autenticazione</span><span class="sxs-lookup"><span data-stu-id="4b4e0-209">Authentication</span></span>
    # Connect tooAzure and select hello subscription toowork against
    $Cred = Get-AutomationPSCredential -Name $AzureCredentialAssetName
    $null = Add-AzureAccount -Credential $Cred -ErrorAction Stop
    $SubId = Get-AutomationVariable -Name $AzureSubscriptionIdAssetName
    $null = Select-AzureSubscription -SubscriptionId $SubId -ErrorAction Stop

<span data-ttu-id="4b4e0-210">set di righe successive Hello hello [credenziali](automation-credentials.md) e sottoscrizione di Azure che verrà utilizzato per il resto di hello del runbook hello.</span><span class="sxs-lookup"><span data-stu-id="4b4e0-210">hello next lines set hello [credentials](automation-credentials.md) and Azure subscription that will be used for hello rest of hello runbook.</span></span>
<span data-ttu-id="4b4e0-211">Prima di tutto utilizziamo **Get-AutomationPSCredential** asset hello tooget che contiene le credenziali di hello con accesso toostart e arrestare le macchine virtuali in hello sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="4b4e0-211">First we use **Get-AutomationPSCredential** tooget hello asset that holds hello credentials with access toostart and stop virtual machines in hello Azure subscription.</span></span> <span data-ttu-id="4b4e0-212">**Aggiungere-AzureAccount** utilizza quindi questo credenziali hello tooset di asset.</span><span class="sxs-lookup"><span data-stu-id="4b4e0-212">**Add-AzureAccount** then uses this asset tooset hello credentials.</span></span>  <span data-ttu-id="4b4e0-213">output di Hello viene assegnato variabile fittizia tooa in modo che non non è incluso nell'output del runbook hello.</span><span class="sxs-lookup"><span data-stu-id="4b4e0-213">hello output is assigned tooa dummy variable so that it isn't included in hello runbook output.</span></span>  

<span data-ttu-id="4b4e0-214">asset della variabile di Hello con sottoscrizione hello ID viene quindi recuperato con **Get-AutomationVariable** e sottoscrizione hello impostata con **Select-AzureSubscription**.</span><span class="sxs-lookup"><span data-stu-id="4b4e0-214">hello variable asset with hello subscription ID is then retrieved with **Get-AutomationVariable** and hello subscription set with **Select-AzureSubscription**.</span></span>

### <a name="get-vms"></a><span data-ttu-id="4b4e0-215">Ottenere le macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="4b4e0-215">Get VMs</span></span>
    # If there is a specific cloud service, then get all VMs in hello service,
    # otherwise get all VMs in hello subscription.
    if ($ServiceName)
    {
        $VMs = Get-AzureVM -ServiceName $ServiceName
    }
    else
    {
        $VMs = Get-AzureVM
    }

<span data-ttu-id="4b4e0-216">**Get-AzureVM** è usato tooretrieve hello hello runbook funzionerà con le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="4b4e0-216">**Get-AzureVM** is used tooretrieve hello virtual machines hello runbook will work with.</span></span>  <span data-ttu-id="4b4e0-217">Se viene fornito un valore in hello **ServiceName** input variabile, quindi solo hello le macchine virtuali con lo stesso nome di servizio vengono recuperate.</span><span class="sxs-lookup"><span data-stu-id="4b4e0-217">If a value is provided in hello **ServiceName** input variable, then only hello virtual machines with that service name are retrieved.</span></span>  <span data-ttu-id="4b4e0-218">Se invece la variabile **ServiceName** è vuota, verranno recuperate tutte le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="4b4e0-218">If **ServiceName** is empty, then all virtual machines are retrieved.</span></span>

### <a name="startstop-virtual-machines-and-send-output"></a><span data-ttu-id="4b4e0-219">Avviare/arrestare le macchine virtuali e inviare l'output</span><span class="sxs-lookup"><span data-stu-id="4b4e0-219">Start/Stop virtual machines and send output</span></span>
    # Start each of hello stopped VMs
    foreach ($VM in $VMs)
    {
        if ($VM.PowerState -eq "Started")
        {
            # hello VM is already started, so send notice
            Write-Output ($VM.InstanceName + " is already running")
        }
        else
        {
            # hello VM needs toobe started
            $StartRtn = Start-AzureVM -Name $VM.Name -ServiceName $VM.ServiceName -ErrorAction Continue

            if ($StartRtn.OperationStatus -ne 'Succeeded')
            {
                # hello VM failed toostart, so send notice
                Write-Output ($VM.InstanceName + " failed toostart")
            }
            else
            {
                # hello VM started, so send notice
                Write-Output ($VM.InstanceName + " has been started")
            }
        }
    }

<span data-ttu-id="4b4e0-220">le righe successive Hello eseguire ogni macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="4b4e0-220">hello next lines step through each virtual machine.</span></span>  <span data-ttu-id="4b4e0-221">Prima di tutto hello **alimentazione** di hello macchina virtuale è toosee selezionata se è già in esecuzione o arrestato, a seconda di hello runbook.</span><span class="sxs-lookup"><span data-stu-id="4b4e0-221">First hello **PowerState** of hello virtual machine is checked toosee if it is already running or stopped, depending on hello runbook.</span></span>  <span data-ttu-id="4b4e0-222">Se è già in stato di destinazione hello, toooutput e si termina di runbook hello viene inviato un messaggio.</span><span class="sxs-lookup"><span data-stu-id="4b4e0-222">If it is already in hello target state, then a message is sent toooutput, and hello runbook ends.</span></span>  <span data-ttu-id="4b4e0-223">In caso contrario, quindi **Start-AzureVM** o **Stop-AzureVM** è utilizzato tooattempt toostart o arrestare hello macchina virtuale con il risultato di hello della variabile di hello richiesta tooa stored.</span><span class="sxs-lookup"><span data-stu-id="4b4e0-223">If not, then **Start-AzureVM** or **Stop-AzureVM** is used tooattempt toostart or stop hello virtual machine with hello result of hello request stored tooa variable.</span></span>  <span data-ttu-id="4b4e0-224">Un messaggio viene quindi inviato toooutput che specifica se hello richiesta toostart o l'arresto è stata inviata correttamente.</span><span class="sxs-lookup"><span data-stu-id="4b4e0-224">A message is then sent toooutput specifying whether hello request toostart or stop was submitted successfully.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4b4e0-225">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4b4e0-225">Next steps</span></span>
* <span data-ttu-id="4b4e0-226">toolearn più sull'utilizzo dei runbook figlio, vedere [figlio runbook in automazione di Azure](automation-child-runbooks.md)</span><span class="sxs-lookup"><span data-stu-id="4b4e0-226">toolearn more about working with child runbooks, see [Child runbooks in Azure Automation](automation-child-runbooks.md)</span></span>
* <span data-ttu-id="4b4e0-227">toolearn altre informazioni sull'output di risolvere i messaggi durante l'esecuzione di runbook e toohelp di registrazione, vedere [Runbook output e i messaggi in automazione di Azure](automation-runbook-output-and-messages.md)</span><span class="sxs-lookup"><span data-stu-id="4b4e0-227">toolearn more about output messages during runbook execution and logging toohelp troubleshoot, see [Runbook output and messages in Azure Automation](automation-runbook-output-and-messages.md)</span></span>

