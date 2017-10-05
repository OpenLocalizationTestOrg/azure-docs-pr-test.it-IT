---
title: Avvio di un runbook in Automazione di Azure | Microsoft Docs
description: "Riepiloga le diverse modalità che è possibile usare per avviare un Runbook in Automazione di Azure e fornisce dettagli sull'uso del portale di Azure e di Windows PowerShell."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 6ee756b4-9200-4eb2-9bda-ec156853803b
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/07/2017
ms.author: magoedte;bwren
ms.openlocfilehash: 844831b63d5263987ed05370125fbe9f01913ab9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="starting-a-runbook-in-azure-automation"></a><span data-ttu-id="e1585-103">Avvio di un Runbook in Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="e1585-103">Starting a runbook in Azure Automation</span></span>
<span data-ttu-id="e1585-104">La tabella seguente consente di determinare la modalità di avvio di un Runbook in Automazione di Azure più appropriata per il proprio scenario.</span><span class="sxs-lookup"><span data-stu-id="e1585-104">The following table will help you determine the method to start a runbook in Azure Automation that is most suitable to your particular scenario.</span></span> <span data-ttu-id="e1585-105">Questo articolo include informazioni dettagliate sull'avvio di un Runbook con il portale di Azure e con Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e1585-105">This article includes details on starting a runbook with the Azure portal and with Windows PowerShell.</span></span> <span data-ttu-id="e1585-106">Le informazioni sulle altre modalità sono contenute in altri documenti accessibili dai collegamenti seguenti.</span><span class="sxs-lookup"><span data-stu-id="e1585-106">Details on the other methods are provided in other documentation that you can access from the links below.</span></span>

| <span data-ttu-id="e1585-107">**METODO**</span><span class="sxs-lookup"><span data-stu-id="e1585-107">**METHOD**</span></span> | <span data-ttu-id="e1585-108">**CARATTERISTICHE**</span><span class="sxs-lookup"><span data-stu-id="e1585-108">**CHARACTERISTICS**</span></span> |
| --- | --- |
| [<span data-ttu-id="e1585-109">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="e1585-109">Azure Portal</span></span>](#starting-a-runbook-with-the-azure-portal) |<li><span data-ttu-id="e1585-110">Metodo più semplice con interfaccia utente interattiva.</span><span class="sxs-lookup"><span data-stu-id="e1585-110">Simplest method with interactive user interface.</span></span><br> <li><span data-ttu-id="e1585-111">Modulo per specificare valori di parametri semplici.</span><span class="sxs-lookup"><span data-stu-id="e1585-111">Form to provide simple parameter values.</span></span><br> <li><span data-ttu-id="e1585-112">Facilità di controllo dello stato dei processi.</span><span class="sxs-lookup"><span data-stu-id="e1585-112">Easily track job state.</span></span><br> <li><span data-ttu-id="e1585-113">Accesso autenticato con l'accesso di Azure.</span><span class="sxs-lookup"><span data-stu-id="e1585-113">Access authenticated with Azure logon.</span></span> |
| [<span data-ttu-id="e1585-114">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="e1585-114">Windows PowerShell</span></span>](https://msdn.microsoft.com/library/dn690259.aspx) |<li><span data-ttu-id="e1585-115">Chiamata mediante cmdlet di Windows PowerShell nella riga di comandi.</span><span class="sxs-lookup"><span data-stu-id="e1585-115">Call from command line with Windows PowerShell cmdlets.</span></span><br> <li><span data-ttu-id="e1585-116">Possibilità di inclusione in una soluzione automatizzata con più passaggi.</span><span class="sxs-lookup"><span data-stu-id="e1585-116">Can be included in automated solution with multiple steps.</span></span><br> <li><span data-ttu-id="e1585-117">Autenticazione della richiesta con un certificato oppure con un'entità utente/entità servizio OAuth.</span><span class="sxs-lookup"><span data-stu-id="e1585-117">Request is authenticated with certificate or OAuth user principal / service principal.</span></span><br> <li><span data-ttu-id="e1585-118">Possibilità di specificare valori di parametri semplici e complessi.</span><span class="sxs-lookup"><span data-stu-id="e1585-118">Provide simple and complex parameter values.</span></span><br> <li><span data-ttu-id="e1585-119">Possibilità di controllare lo stato dei processi.</span><span class="sxs-lookup"><span data-stu-id="e1585-119">Track job state.</span></span><br> <li><span data-ttu-id="e1585-120">Obbligo per il client di supporto dei cmdlet di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e1585-120">Client required to support PowerShell cmdlets.</span></span> |
| [<span data-ttu-id="e1585-121">API di Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="e1585-121">Azure Automation API</span></span>](https://msdn.microsoft.com/library/azure/mt662285.aspx) |<li><span data-ttu-id="e1585-122">Modalità più flessibile, ma anche più complessa.</span><span class="sxs-lookup"><span data-stu-id="e1585-122">Most flexible method but also most complex.</span></span><br> <li><span data-ttu-id="e1585-123">Possibilità di chiamata da qualsiasi codice personalizzato in grado di creare richieste HTTP.</span><span class="sxs-lookup"><span data-stu-id="e1585-123">Call from any custom code that can make HTTP requests.</span></span><br> <li><span data-ttu-id="e1585-124">Autenticazione della richiesta con un certificato oppure con un'entità utente/entità servizio OAuth.</span><span class="sxs-lookup"><span data-stu-id="e1585-124">Request authenticated with certificate, or Oauth user principal / service principal.</span></span><br> <li><span data-ttu-id="e1585-125">Possibilità di specificare valori di parametri semplici e complessi.</span><span class="sxs-lookup"><span data-stu-id="e1585-125">Provide simple and complex parameter values.</span></span><br> <li><span data-ttu-id="e1585-126">Possibilità di controllare lo stato dei processi.</span><span class="sxs-lookup"><span data-stu-id="e1585-126">Track job state.</span></span> |
| [<span data-ttu-id="e1585-127">Webhook</span><span class="sxs-lookup"><span data-stu-id="e1585-127">Webhooks</span></span>](automation-webhooks.md) |<li><span data-ttu-id="e1585-128">Avvio di Runbook da una singola richiesta HTTP.</span><span class="sxs-lookup"><span data-stu-id="e1585-128">Start runbook from single HTTP request.</span></span><br> <li><span data-ttu-id="e1585-129">Autenticazione con token di sicurezza nell'URL.</span><span class="sxs-lookup"><span data-stu-id="e1585-129">Authenticated with security token in URL.</span></span><br> <li><span data-ttu-id="e1585-130">Impossibilità per il client di eseguire l'override dei valori di parametri specificati al momento della creazione del webhook.</span><span class="sxs-lookup"><span data-stu-id="e1585-130">Client cannot override parameter values specified when webhook created.</span></span> <span data-ttu-id="e1585-131">Possibilità per il Runbook di definire un singolo parametro popolato con i dettagli della richiesta HTTP.</span><span class="sxs-lookup"><span data-stu-id="e1585-131">Runbook can define single parameter that is populated with the HTTP request details.</span></span><br> <li><span data-ttu-id="e1585-132">Impossibilità di tenere traccia dello stato dei processi tramite URL webhook.</span><span class="sxs-lookup"><span data-stu-id="e1585-132">No ability to track job state through webhook URL.</span></span> |
| [<span data-ttu-id="e1585-133">Risposta all'avviso di Azure</span><span class="sxs-lookup"><span data-stu-id="e1585-133">Respond to Azure Alert</span></span>](../log-analytics/log-analytics-alerts.md) |<li><span data-ttu-id="e1585-134">Avviare un runbook in risposta all'avviso di Azure.</span><span class="sxs-lookup"><span data-stu-id="e1585-134">Start a runbook in response to Azure alert.</span></span><br> <li><span data-ttu-id="e1585-135">Configurare webhook per runbook e collegare all'avviso.</span><span class="sxs-lookup"><span data-stu-id="e1585-135">Configure webhook for runbook and link to alert.</span></span><br> <li><span data-ttu-id="e1585-136">Autenticazione con token di sicurezza nell'URL.</span><span class="sxs-lookup"><span data-stu-id="e1585-136">Authenticated with security token in URL.</span></span> |
| [<span data-ttu-id="e1585-137">Pianificare</span><span class="sxs-lookup"><span data-stu-id="e1585-137">Schedule</span></span>](automation-schedules.md) |<li><span data-ttu-id="e1585-138">Avvio automatico dei runbook in base a una pianificazione oraria, giornaliera, settimanale o mensile.</span><span class="sxs-lookup"><span data-stu-id="e1585-138">Automatically start runbook on hourly, daily, weekly, or monthly schedule.</span></span><br> <li><span data-ttu-id="e1585-139">Modifica della pianificazione tramite il portale di Azure, i cmdlet di PowerShell o l'API di Azure.</span><span class="sxs-lookup"><span data-stu-id="e1585-139">Manipulate schedule through Azure portal, PowerShell cmdlets, or Azure API.</span></span><br> <li><span data-ttu-id="e1585-140">Possibilità di specificare i valori di parametri da usare con la pianificazione.</span><span class="sxs-lookup"><span data-stu-id="e1585-140">Provide parameter values to be used with schedule.</span></span> |
| [<span data-ttu-id="e1585-141">Da un altro Runbook</span><span class="sxs-lookup"><span data-stu-id="e1585-141">From Another Runbook</span></span>](automation-child-runbooks.md) |<li><span data-ttu-id="e1585-142">Uso di un Runbook come attività in un altro Runbook.</span><span class="sxs-lookup"><span data-stu-id="e1585-142">Use a runbook as an activity in another runbook.</span></span><br> <li><span data-ttu-id="e1585-143">Utile per funzionalità usate da più Runbook.</span><span class="sxs-lookup"><span data-stu-id="e1585-143">Useful for functionality used by multiple runbooks.</span></span><br> <li><span data-ttu-id="e1585-144">Possibilità di specificare valori di parametri per Runbook figlio e usare l'output in Runbook padre.</span><span class="sxs-lookup"><span data-stu-id="e1585-144">Provide parameter values to child runbook and use output in parent runbook.</span></span> |

<span data-ttu-id="e1585-145">L'immagine seguente illustra in dettaglio il processo nel ciclo di vita di un runbook.</span><span class="sxs-lookup"><span data-stu-id="e1585-145">The following image illustrates detailed step-by-step process in the life cycle of a runbook.</span></span> <span data-ttu-id="e1585-146">Include vari metodi di avvio di un runbook in Automazione di Azure, i componenti necessari per il ruolo di lavoro ibrido per runbook per eseguire i runbook di Automazione di Azure e le interazioni tra i vari componenti.</span><span class="sxs-lookup"><span data-stu-id="e1585-146">It includes different ways a runbook is started in Azure Automation, components required for Hybrid Runbook Worker to execute Azure Automation runbooks and interactions between different components.</span></span> <span data-ttu-id="e1585-147">Per altre informazioni sull'esecuzione di runbook di automazione nel proprio data center, vedere [Ruoli di lavoro ibridi per runbook](automation-hybrid-runbook-worker.md)</span><span class="sxs-lookup"><span data-stu-id="e1585-147">To learn about executing Automation runbooks in your datacenter, refer to [hybrid runbook workers](automation-hybrid-runbook-worker.md)</span></span>

![Architettura dei runbook](media/automation-starting-runbook/runbooks-architecture.png)

## <a name="starting-a-runbook-with-the-azure-portal"></a><span data-ttu-id="e1585-149">Avvio di un Runbook con il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="e1585-149">Starting a runbook with the Azure portal</span></span>
1. <span data-ttu-id="e1585-150">Nel portale di Azure selezionare **Automazione** e quindi fare clic sul nome di un account di automazione.</span><span class="sxs-lookup"><span data-stu-id="e1585-150">In the Azure portal, select **Automation** and then then click the name of an automation account.</span></span>
2. <span data-ttu-id="e1585-151">Nel menu Hub selezionare **Runbook**.</span><span class="sxs-lookup"><span data-stu-id="e1585-151">On the Hub menu, select **Runbooks**.</span></span>
3. <span data-ttu-id="e1585-152">Nel pannello **Runbook** selezionare un runbook e quindi fare clic su **Avvia**.</span><span class="sxs-lookup"><span data-stu-id="e1585-152">On the **Runbooks** blade, select a runbook, and then click **Start**.</span></span>
4. <span data-ttu-id="e1585-153">Se il Runbook dispone di parametri, verrà richiesto di specificare i valori con una casella di testo per ogni parametro.</span><span class="sxs-lookup"><span data-stu-id="e1585-153">If the runbook has parameters, you will be prompted to provide values with a text box for each parameter.</span></span> <span data-ttu-id="e1585-154">Per altri dettagli sui parametri, vedere [Parametri di Runbook](#Runbook-parameters) più avanti.</span><span class="sxs-lookup"><span data-stu-id="e1585-154">See [Runbook Parameters](#Runbook-parameters) below for further details on parameters.</span></span>
5. <span data-ttu-id="e1585-155">Nel pannello **Processo** è possibile visualizzare lo stato del processo del runbook.</span><span class="sxs-lookup"><span data-stu-id="e1585-155">On the **Job** blade, you can view the status of the runbook job.</span></span>

## <a name="starting-a-runbook-with-windows-powershell"></a><span data-ttu-id="e1585-156">Avvio di un Runbook con Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="e1585-156">Starting a runbook with Windows PowerShell</span></span>
<span data-ttu-id="e1585-157">È possibile usare [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) per avviare un runbook con Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e1585-157">You can use the [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) to start a runbook with Windows PowerShell.</span></span> <span data-ttu-id="e1585-158">Il codice di esempio seguente avvia un Runbook denominato Test-Runbook.</span><span class="sxs-lookup"><span data-stu-id="e1585-158">The following sample code starts a runbook called Test-Runbook.</span></span>

```
Start-AzureRmAutomationRunbook -AutomationAccountName "MyAutomationAccount" -Name "Test-Runbook" -ResourceGroupName "ResourceGroup01"
```

<span data-ttu-id="e1585-159">Start-AzureRmAutomationRunbook restituisce un oggetto processo che è possibile usare per tenere traccia dello stato dopo l'avvio del runbook.</span><span class="sxs-lookup"><span data-stu-id="e1585-159">Start-AzureRmAutomationRunbook returns a job object that you can use to track its status once the runbook is started.</span></span> <span data-ttu-id="e1585-160">È quindi possibile usare questo oggetto processo con [Get-AzureRmAutomationJob](https://msdn.microsoft.com/library/mt619440.aspx) per determinare lo stato del processo e con [Get-AzureRmAutomationJobOutput](https://msdn.microsoft.com/library/mt603476.aspx) per ottenere il relativo output.</span><span class="sxs-lookup"><span data-stu-id="e1585-160">You can then use this job object with [Get-AzureRmAutomationJob](https://msdn.microsoft.com/library/mt619440.aspx) to determine the status of the job and [Get-AzureRmAutomationJobOutput](https://msdn.microsoft.com/library/mt603476.aspx) to get its output.</span></span> <span data-ttu-id="e1585-161">L'esempio di codice seguente avvia un Runbook denominato Test-Runbook, attende che venga completato e quindi visualizza l'output corrispondente.</span><span class="sxs-lookup"><span data-stu-id="e1585-161">The following sample code starts a runbook called Test-Runbook, waits until it has completed, and then displays its output.</span></span>

```
$runbookName = "Test-Runbook"
$ResourceGroup = "ResourceGroup01"
$AutomationAcct = "MyAutomationAccount"

$job = Start-AzureRmAutomationRunbook –AutomationAccountName $AutomationAcct -Name $runbookName -ResourceGroupName $ResourceGroup

$doLoop = $true
While ($doLoop) {
   $job = Get-AzureRmAutomationJob –AutomationAccountName $AutomationAcct -Id $job.JobId -ResourceGroupName $ResourceGroup
   $status = $job.Status
   $doLoop = (($status -ne "Completed") -and ($status -ne "Failed") -and ($status -ne "Suspended") -and ($status -ne "Stopped"))
}

Get-AzureRmAutomationJobOutput –AutomationAccountName $AutomationAcct -Id $job.JobId -ResourceGroupName $ResourceGroup –Stream Output
```

<span data-ttu-id="e1585-162">Se il Runbook richiede parametri, è necessario fornirli come [tabella hash](http://technet.microsoft.com/library/hh847780.aspx) , dove la chiave della tabella hash corrisponde al nome del parametro e il valore al valore del parametro.</span><span class="sxs-lookup"><span data-stu-id="e1585-162">If the runbook requires parameters, then you must provide them as a [hashtable](http://technet.microsoft.com/library/hh847780.aspx) where the key of the hashtable matches the parameter name and the value is the parameter value.</span></span> <span data-ttu-id="e1585-163">L'esempio seguente illustra come avviare un Runbook con due parametri di stringa denominati FirstName e LastName, un parametro di tipo intero denominato RepeatCount e un parametro booleano denominato Show.</span><span class="sxs-lookup"><span data-stu-id="e1585-163">The following example shows how to start a runbook with two string parameters named FirstName and LastName, an integer named RepeatCount, and a boolean parameter named Show.</span></span> <span data-ttu-id="e1585-164">Per altre informazioni sui parametri, vedere [Parametri di Runbook](#Runbook-parameters) più avanti.</span><span class="sxs-lookup"><span data-stu-id="e1585-164">For additional information on parameters, see [Runbook Parameters](#Runbook-parameters) below.</span></span>

```
$params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
Start-AzureRmAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Test-Runbook" -ResourceGroupName "ResourceGroup01" –Parameters $params
```

## <a name="runbook-parameters"></a><span data-ttu-id="e1585-165">Parametri di Runbook</span><span class="sxs-lookup"><span data-stu-id="e1585-165">Runbook parameters</span></span>
<span data-ttu-id="e1585-166">Quando si avvia un runbook dal portale di Azure o da Windows PowerShell, l'istruzione viene inviata attraverso il servizio Web Automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="e1585-166">When you start a runbook from the Azure Portal or Windows PowerShell, the instruction is sent through the Azure Automation web service.</span></span> <span data-ttu-id="e1585-167">Questo servizio non supporta i parametri con tipi di dati complessi.</span><span class="sxs-lookup"><span data-stu-id="e1585-167">This service does not support parameters with complex data types.</span></span> <span data-ttu-id="e1585-168">Se è necessario specificare un valore per un parametro complesso, eseguire la chiamata inline da un altro Runbook come descritto in [Runbook figlio in Automazione di Azure](automation-child-runbooks.md).</span><span class="sxs-lookup"><span data-stu-id="e1585-168">If you need to provide a value for a complex parameter, then you must call it inline from another runbook as described in [Child runbooks in Azure Automation](automation-child-runbooks.md).</span></span>

<span data-ttu-id="e1585-169">Il servizio Web Automazione di Azure offrirà funzionalità speciali per i parametri che usano determinati tipi di dati, come descritto nelle sezioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="e1585-169">The Azure Automation web service will provide special functionality for parameters using certain data types as described in the following sections.</span></span>

### <a name="named-values"></a><span data-ttu-id="e1585-170">Valori denominati</span><span class="sxs-lookup"><span data-stu-id="e1585-170">Named values</span></span>
<span data-ttu-id="e1585-171">Se il parametro è un tipo di dati [object], è possibile usare il formato JSON seguente per inviargli un elenco di valori denominati: *{Name1:'Value1', Name2:'Value2', Name3:'Value3'}*.</span><span class="sxs-lookup"><span data-stu-id="e1585-171">If the parameter is data type [object], then you can use the following JSON format to send it a list of named values: *{Name1:'Value1', Name2:'Value2', Name3:'Value3'}*.</span></span> <span data-ttu-id="e1585-172">Questi valori devono essere tipi semplici.</span><span class="sxs-lookup"><span data-stu-id="e1585-172">These values must be simple types.</span></span> <span data-ttu-id="e1585-173">Il Runbook riceverà il parametro come [PSCustomObject](https://msdn.microsoft.com/library/system.management.automation.pscustomobject%28v=vs.85%29.aspx) con proprietà che corrispondono a ogni valore denominato.</span><span class="sxs-lookup"><span data-stu-id="e1585-173">The runbook will receive the parameter as a [PSCustomObject](https://msdn.microsoft.com/library/system.management.automation.pscustomobject%28v=vs.85%29.aspx) with properties that correspond to each named value.</span></span>

<span data-ttu-id="e1585-174">Si consideri il Runbook di test seguente che accetta un parametro denominato user.</span><span class="sxs-lookup"><span data-stu-id="e1585-174">Consider the following test runbook that accepts a parameter called user.</span></span>

```
Workflow Test-Parameters
{
   param (
      [Parameter(Mandatory=$true)][object]$user
   )
    $userObject = $user | ConvertFrom-JSON
    if ($userObject.Show) {
        foreach ($i in 1..$userObject.RepeatCount) {
            $userObject.FirstName
            $userObject.LastName
        }
    }
}
```

<span data-ttu-id="e1585-175">È possibile usare il testo seguente per il parametro user.</span><span class="sxs-lookup"><span data-stu-id="e1585-175">The following text could be used for the user parameter.</span></span>

```
{FirstName:'Joe',LastName:'Smith',RepeatCount:'2',Show:'True'}
```

<span data-ttu-id="e1585-176">Si ottiene l'output seguente.</span><span class="sxs-lookup"><span data-stu-id="e1585-176">This results in the following output.</span></span>

```
Joe
Smith
Joe
Smith
```

### <a name="arrays"></a><span data-ttu-id="e1585-177">Matrici</span><span class="sxs-lookup"><span data-stu-id="e1585-177">Arrays</span></span>
<span data-ttu-id="e1585-178">Se il parametro è una matrice, ad esempio [array] o [string[]], è possibile usare il formato JSON seguente per inviargli un elenco di valori: *[Value1,Value2,Value3]*.</span><span class="sxs-lookup"><span data-stu-id="e1585-178">If the parameter is an array such as [array] or [string[]], then you can use the following JSON format to send it a list of values: *[Value1,Value2,Value3]*.</span></span> <span data-ttu-id="e1585-179">Questi valori devono essere tipi semplici.</span><span class="sxs-lookup"><span data-stu-id="e1585-179">These values must be simple types.</span></span>

<span data-ttu-id="e1585-180">Si consideri il Runbook di test seguente che accetta un parametro denominato *user*.</span><span class="sxs-lookup"><span data-stu-id="e1585-180">Consider the following test runbook that accepts a parameter called *user*.</span></span>

```
Workflow Test-Parameters
{
   param (
      [Parameter(Mandatory=$true)][array]$user
   )
    if ($user[3]) {
        foreach ($i in 1..$user[2]) {
            $ user[0]
            $ user[1]
        }
    }
}
```

<span data-ttu-id="e1585-181">È possibile usare il testo seguente per il parametro user.</span><span class="sxs-lookup"><span data-stu-id="e1585-181">The following text could be used for the user parameter.</span></span>

```
["Joe","Smith",2,true]
```

<span data-ttu-id="e1585-182">Si ottiene l'output seguente.</span><span class="sxs-lookup"><span data-stu-id="e1585-182">This results in the following output.</span></span>

```
Joe
Smith
Joe
Smith
```

### <a name="credentials"></a><span data-ttu-id="e1585-183">Credenziali</span><span class="sxs-lookup"><span data-stu-id="e1585-183">Credentials</span></span>
<span data-ttu-id="e1585-184">Se il parametro è un tipo di dati **PSCredential**, è possibile specificare il nome di un [asset credenziali](automation-credentials.md)di Automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="e1585-184">If the parameter is data type **PSCredential**, then you can provide the name of an Azure Automation [credential asset](automation-credentials.md).</span></span> <span data-ttu-id="e1585-185">Il Runbook recupererà le credenziali con il nome specificato.</span><span class="sxs-lookup"><span data-stu-id="e1585-185">The runbook will retrieve the credential with the name that you specify.</span></span>

<span data-ttu-id="e1585-186">Si consideri il Runbook di test seguente che accetta un parametro denominato credential.</span><span class="sxs-lookup"><span data-stu-id="e1585-186">Consider the following test runbook that accepts a parameter called credential.</span></span>

```
Workflow Test-Parameters
{
   param (
      [Parameter(Mandatory=$true)][PSCredential]$credential
   )
   $credential.UserName
}
```

<span data-ttu-id="e1585-187">È possibile usare il testo seguente per il parametro user presumendo l'esistenza di un asset credenziali denominato *My Credential*.</span><span class="sxs-lookup"><span data-stu-id="e1585-187">The following text could be used for the user parameter assuming that there was a credential asset called *My Credential*.</span></span>

```
My Credential
```

<span data-ttu-id="e1585-188">Presupponendo che il nome utente nelle credenziali sia *jsmith*, si ottiene l'output seguente.</span><span class="sxs-lookup"><span data-stu-id="e1585-188">Assuming the username in the credential was *jsmith*, this results in the following output.</span></span>

```
jsmith
```

## <a name="next-steps"></a><span data-ttu-id="e1585-189">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e1585-189">Next steps</span></span>
* <span data-ttu-id="e1585-190">L'architettura runbook nell'articolo corrente offre una panoramica generale delle risorse di gestione di runbook in Azure e in locale con il ruolo di lavoro ibrido per runbook.</span><span class="sxs-lookup"><span data-stu-id="e1585-190">The runbook architecture in current article provides a high-level overview of runbooks managing resources in Azure and on-premises with the Hybrid Runbook Worker.</span></span>  <span data-ttu-id="e1585-191">Per altre informazioni sull'esecuzione di runbook di automazione nel proprio data center, vedere [Ruoli di lavoro ibridi per runbook](automation-hybrid-runbook-worker.md).</span><span class="sxs-lookup"><span data-stu-id="e1585-191">To learn about executing Automation runbooks in your datacenter, refer to [Hybrid Runbook Workers](automation-hybrid-runbook-worker.md).</span></span>
* <span data-ttu-id="e1585-192">Per altre informazioni sulla creazione di runbook modulari che possono essere usati da altri runbook per funzioni comuni o specifiche, fare riferimento a [Runbook figlio](automation-child-runbooks.md).</span><span class="sxs-lookup"><span data-stu-id="e1585-192">To learn more about the creating modular runbooks to be used by other runbooks for specific or common functions, refer to [Child Runbooks](automation-child-runbooks.md).</span></span>

