---
title: aaaStarting un runbook in automazione di Azure | Documenti Microsoft
description: Riepiloga hello diversi metodi che possono essere utilizzati toostart un runbook in automazione di Azure e fornisce informazioni dettagliate sull'utilizzo di entrambi hello portale di Azure e Windows PowerShell.
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
ms.openlocfilehash: e44bce5b56b8e803f9247fbb4f3d4db7ab35c913
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="starting-a-runbook-in-azure-automation"></a><span data-ttu-id="2749e-103">Avvio di un Runbook in Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="2749e-103">Starting a runbook in Azure Automation</span></span>
<span data-ttu-id="2749e-104">Hello nella tabella seguente consentono di determinare hello metodo toostart un runbook in automazione di Azure che è più adatto tooyour particolare scenario.</span><span class="sxs-lookup"><span data-stu-id="2749e-104">hello following table will help you determine hello method toostart a runbook in Azure Automation that is most suitable tooyour particular scenario.</span></span> <span data-ttu-id="2749e-105">In questo articolo include informazioni dettagliate su come avviare un runbook con hello portale di Azure e con Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2749e-105">This article includes details on starting a runbook with hello Azure portal and with Windows PowerShell.</span></span> <span data-ttu-id="2749e-106">Dettagli su hello altri metodi vengono forniti in altra documentazione di cui è possibile accedere dai collegamenti hello riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="2749e-106">Details on hello other methods are provided in other documentation that you can access from hello links below.</span></span>

| <span data-ttu-id="2749e-107">**METODO**</span><span class="sxs-lookup"><span data-stu-id="2749e-107">**METHOD**</span></span> | <span data-ttu-id="2749e-108">**CARATTERISTICHE**</span><span class="sxs-lookup"><span data-stu-id="2749e-108">**CHARACTERISTICS**</span></span> |
| --- | --- |
| [<span data-ttu-id="2749e-109">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="2749e-109">Azure Portal</span></span>](#starting-a-runbook-with-the-azure-portal) |<li><span data-ttu-id="2749e-110">Metodo più semplice con interfaccia utente interattiva.</span><span class="sxs-lookup"><span data-stu-id="2749e-110">Simplest method with interactive user interface.</span></span><br> <li><span data-ttu-id="2749e-111">I valori dei parametri semplice tooprovide del modulo.</span><span class="sxs-lookup"><span data-stu-id="2749e-111">Form tooprovide simple parameter values.</span></span><br> <li><span data-ttu-id="2749e-112">Facilità di controllo dello stato dei processi.</span><span class="sxs-lookup"><span data-stu-id="2749e-112">Easily track job state.</span></span><br> <li><span data-ttu-id="2749e-113">Accesso autenticato con l'accesso di Azure.</span><span class="sxs-lookup"><span data-stu-id="2749e-113">Access authenticated with Azure logon.</span></span> |
| [<span data-ttu-id="2749e-114">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="2749e-114">Windows PowerShell</span></span>](https://msdn.microsoft.com/library/dn690259.aspx) |<li><span data-ttu-id="2749e-115">Chiamata mediante cmdlet di Windows PowerShell nella riga di comandi.</span><span class="sxs-lookup"><span data-stu-id="2749e-115">Call from command line with Windows PowerShell cmdlets.</span></span><br> <li><span data-ttu-id="2749e-116">Possibilità di inclusione in una soluzione automatizzata con più passaggi.</span><span class="sxs-lookup"><span data-stu-id="2749e-116">Can be included in automated solution with multiple steps.</span></span><br> <li><span data-ttu-id="2749e-117">Autenticazione della richiesta con un certificato oppure con un'entità utente/entità servizio OAuth.</span><span class="sxs-lookup"><span data-stu-id="2749e-117">Request is authenticated with certificate or OAuth user principal / service principal.</span></span><br> <li><span data-ttu-id="2749e-118">Possibilità di specificare valori di parametri semplici e complessi.</span><span class="sxs-lookup"><span data-stu-id="2749e-118">Provide simple and complex parameter values.</span></span><br> <li><span data-ttu-id="2749e-119">Possibilità di controllare lo stato dei processi.</span><span class="sxs-lookup"><span data-stu-id="2749e-119">Track job state.</span></span><br> <li><span data-ttu-id="2749e-120">I cmdlet di PowerShell toosupport necessario client.</span><span class="sxs-lookup"><span data-stu-id="2749e-120">Client required toosupport PowerShell cmdlets.</span></span> |
| [<span data-ttu-id="2749e-121">API di Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="2749e-121">Azure Automation API</span></span>](https://msdn.microsoft.com/library/azure/mt662285.aspx) |<li><span data-ttu-id="2749e-122">Modalità più flessibile, ma anche più complessa.</span><span class="sxs-lookup"><span data-stu-id="2749e-122">Most flexible method but also most complex.</span></span><br> <li><span data-ttu-id="2749e-123">Possibilità di chiamata da qualsiasi codice personalizzato in grado di creare richieste HTTP.</span><span class="sxs-lookup"><span data-stu-id="2749e-123">Call from any custom code that can make HTTP requests.</span></span><br> <li><span data-ttu-id="2749e-124">Autenticazione della richiesta con un certificato oppure con un'entità utente/entità servizio OAuth.</span><span class="sxs-lookup"><span data-stu-id="2749e-124">Request authenticated with certificate, or Oauth user principal / service principal.</span></span><br> <li><span data-ttu-id="2749e-125">Possibilità di specificare valori di parametri semplici e complessi.</span><span class="sxs-lookup"><span data-stu-id="2749e-125">Provide simple and complex parameter values.</span></span><br> <li><span data-ttu-id="2749e-126">Possibilità di controllare lo stato dei processi.</span><span class="sxs-lookup"><span data-stu-id="2749e-126">Track job state.</span></span> |
| [<span data-ttu-id="2749e-127">Webhook</span><span class="sxs-lookup"><span data-stu-id="2749e-127">Webhooks</span></span>](automation-webhooks.md) |<li><span data-ttu-id="2749e-128">Avvio di Runbook da una singola richiesta HTTP.</span><span class="sxs-lookup"><span data-stu-id="2749e-128">Start runbook from single HTTP request.</span></span><br> <li><span data-ttu-id="2749e-129">Autenticazione con token di sicurezza nell'URL.</span><span class="sxs-lookup"><span data-stu-id="2749e-129">Authenticated with security token in URL.</span></span><br> <li><span data-ttu-id="2749e-130">Impossibilità per il client di eseguire l'override dei valori di parametri specificati al momento della creazione del webhook.</span><span class="sxs-lookup"><span data-stu-id="2749e-130">Client cannot override parameter values specified when webhook created.</span></span> <span data-ttu-id="2749e-131">Runbook può definire singolo parametro che viene popolata con i dettagli della richiesta HTTP hello.</span><span class="sxs-lookup"><span data-stu-id="2749e-131">Runbook can define single parameter that is populated with hello HTTP request details.</span></span><br> <li><span data-ttu-id="2749e-132">Stato del processo non tootrack possibilità tramite l'URL del webhook.</span><span class="sxs-lookup"><span data-stu-id="2749e-132">No ability tootrack job state through webhook URL.</span></span> |
| [<span data-ttu-id="2749e-133">Rispondere tooAzure avviso</span><span class="sxs-lookup"><span data-stu-id="2749e-133">Respond tooAzure Alert</span></span>](../log-analytics/log-analytics-alerts.md) |<li><span data-ttu-id="2749e-134">Avviare un runbook nell'avviso tooAzure di risposta.</span><span class="sxs-lookup"><span data-stu-id="2749e-134">Start a runbook in response tooAzure alert.</span></span><br> <li><span data-ttu-id="2749e-135">Configurare webhook per runbook e il collegamento tooalert.</span><span class="sxs-lookup"><span data-stu-id="2749e-135">Configure webhook for runbook and link tooalert.</span></span><br> <li><span data-ttu-id="2749e-136">Autenticazione con token di sicurezza nell'URL.</span><span class="sxs-lookup"><span data-stu-id="2749e-136">Authenticated with security token in URL.</span></span> |
| [<span data-ttu-id="2749e-137">Pianificare</span><span class="sxs-lookup"><span data-stu-id="2749e-137">Schedule</span></span>](automation-schedules.md) |<li><span data-ttu-id="2749e-138">Avvio automatico dei runbook in base a una pianificazione oraria, giornaliera, settimanale o mensile.</span><span class="sxs-lookup"><span data-stu-id="2749e-138">Automatically start runbook on hourly, daily, weekly, or monthly schedule.</span></span><br> <li><span data-ttu-id="2749e-139">Modifica della pianificazione tramite il portale di Azure, i cmdlet di PowerShell o l'API di Azure.</span><span class="sxs-lookup"><span data-stu-id="2749e-139">Manipulate schedule through Azure portal, PowerShell cmdlets, or Azure API.</span></span><br> <li><span data-ttu-id="2749e-140">Fornire toobe di valori di parametro utilizzato con una pianificazione.</span><span class="sxs-lookup"><span data-stu-id="2749e-140">Provide parameter values toobe used with schedule.</span></span> |
| [<span data-ttu-id="2749e-141">Da un altro Runbook</span><span class="sxs-lookup"><span data-stu-id="2749e-141">From Another Runbook</span></span>](automation-child-runbooks.md) |<li><span data-ttu-id="2749e-142">Uso di un Runbook come attività in un altro Runbook.</span><span class="sxs-lookup"><span data-stu-id="2749e-142">Use a runbook as an activity in another runbook.</span></span><br> <li><span data-ttu-id="2749e-143">Utile per funzionalità usate da più Runbook.</span><span class="sxs-lookup"><span data-stu-id="2749e-143">Useful for functionality used by multiple runbooks.</span></span><br> <li><span data-ttu-id="2749e-144">Fornire runbook toochild valori di parametro e utilizzare l'output in runbook padre.</span><span class="sxs-lookup"><span data-stu-id="2749e-144">Provide parameter values toochild runbook and use output in parent runbook.</span></span> |

<span data-ttu-id="2749e-145">Hello immagine seguente illustra procedura dettagliata hello ciclo di vita di un runbook.</span><span class="sxs-lookup"><span data-stu-id="2749e-145">hello following image illustrates detailed step-by-step process in hello life cycle of a runbook.</span></span> <span data-ttu-id="2749e-146">Offre diversi modi che viene avviato un runbook in automazione di Azure, i componenti necessari per i runbook di automazione di Azure di Runbook Worker ibrido tooexecute e le interazioni tra i diversi componenti.</span><span class="sxs-lookup"><span data-stu-id="2749e-146">It includes different ways a runbook is started in Azure Automation, components required for Hybrid Runbook Worker tooexecute Azure Automation runbooks and interactions between different components.</span></span> <span data-ttu-id="2749e-147">toolearn sull'esecuzione di runbook di automazione nel Data Center, fare riferimento troppo[ibridi per runbook](automation-hybrid-runbook-worker.md)</span><span class="sxs-lookup"><span data-stu-id="2749e-147">toolearn about executing Automation runbooks in your datacenter, refer too[hybrid runbook workers](automation-hybrid-runbook-worker.md)</span></span>

![Architettura dei runbook](media/automation-starting-runbook/runbooks-architecture.png)

## <a name="starting-a-runbook-with-hello-azure-portal"></a><span data-ttu-id="2749e-149">Avvio di un runbook con hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="2749e-149">Starting a runbook with hello Azure portal</span></span>
1. <span data-ttu-id="2749e-150">Nel portale di Azure hello, selezionare **automazione** e quindi scegliere il nome di hello di un account di automazione.</span><span class="sxs-lookup"><span data-stu-id="2749e-150">In hello Azure portal, select **Automation** and then then click hello name of an automation account.</span></span>
2. <span data-ttu-id="2749e-151">Nel menu Hub hello, selezionare **runbook**.</span><span class="sxs-lookup"><span data-stu-id="2749e-151">On hello Hub menu, select **Runbooks**.</span></span>
3. <span data-ttu-id="2749e-152">In hello **runbook** pannello selezionare un runbook e quindi fare clic su **avviare**.</span><span class="sxs-lookup"><span data-stu-id="2749e-152">On hello **Runbooks** blade, select a runbook, and then click **Start**.</span></span>
4. <span data-ttu-id="2749e-153">Hello runbook include parametri, sarà richiesta tooprovide valori con una casella di testo per ogni parametro.</span><span class="sxs-lookup"><span data-stu-id="2749e-153">If hello runbook has parameters, you will be prompted tooprovide values with a text box for each parameter.</span></span> <span data-ttu-id="2749e-154">Per altri dettagli sui parametri, vedere [Parametri di Runbook](#Runbook-parameters) più avanti.</span><span class="sxs-lookup"><span data-stu-id="2749e-154">See [Runbook Parameters](#Runbook-parameters) below for further details on parameters.</span></span>
5. <span data-ttu-id="2749e-155">In hello **processo** pannello, è possibile visualizzare lo stato di hello di processo del runbook hello.</span><span class="sxs-lookup"><span data-stu-id="2749e-155">On hello **Job** blade, you can view hello status of hello runbook job.</span></span>

## <a name="starting-a-runbook-with-windows-powershell"></a><span data-ttu-id="2749e-156">Avvio di un Runbook con Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="2749e-156">Starting a runbook with Windows PowerShell</span></span>
<span data-ttu-id="2749e-157">È possibile utilizzare hello [inizio AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) toostart un runbook con Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2749e-157">You can use hello [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) toostart a runbook with Windows PowerShell.</span></span> <span data-ttu-id="2749e-158">Hello codice di esempio seguente avvia un runbook denominato Test-Runbook.</span><span class="sxs-lookup"><span data-stu-id="2749e-158">hello following sample code starts a runbook called Test-Runbook.</span></span>

```
Start-AzureRmAutomationRunbook -AutomationAccountName "MyAutomationAccount" -Name "Test-Runbook" -ResourceGroupName "ResourceGroup01"
```

<span data-ttu-id="2749e-159">Inizio AzureRmAutomationRunbook restituisce un processo dell'oggetto che è possibile utilizzare tootrack lo stato dopo l'avvio del runbook hello.</span><span class="sxs-lookup"><span data-stu-id="2749e-159">Start-AzureRmAutomationRunbook returns a job object that you can use tootrack its status once hello runbook is started.</span></span> <span data-ttu-id="2749e-160">È quindi possibile utilizzare questo oggetto processo con [Get AzureRmAutomationJob](https://msdn.microsoft.com/library/mt619440.aspx) stato hello toodetermine del processo di hello e [Get AzureRmAutomationJobOutput](https://msdn.microsoft.com/library/mt603476.aspx) tooget l'output.</span><span class="sxs-lookup"><span data-stu-id="2749e-160">You can then use this job object with [Get-AzureRmAutomationJob](https://msdn.microsoft.com/library/mt619440.aspx) toodetermine hello status of hello job and [Get-AzureRmAutomationJobOutput](https://msdn.microsoft.com/library/mt603476.aspx) tooget its output.</span></span> <span data-ttu-id="2749e-161">Hello codice di esempio seguente avvia un runbook denominato Test-Runbook, ne attende il completamento e quindi Visualizza il relativo output.</span><span class="sxs-lookup"><span data-stu-id="2749e-161">hello following sample code starts a runbook called Test-Runbook, waits until it has completed, and then displays its output.</span></span>

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

<span data-ttu-id="2749e-162">Se hello runbook richiede parametri, quindi sarà necessario fornirli come un [hashtable](http://technet.microsoft.com/library/hh847780.aspx) in chiave hello di hello hashtable corrisponde a nome di parametro hello e il valore di hello è il valore di parametro hello.</span><span class="sxs-lookup"><span data-stu-id="2749e-162">If hello runbook requires parameters, then you must provide them as a [hashtable](http://technet.microsoft.com/library/hh847780.aspx) where hello key of hello hashtable matches hello parameter name and hello value is hello parameter value.</span></span> <span data-ttu-id="2749e-163">Hello esempio seguente viene illustrato come toostart un runbook con due parametri stringa denominati FirstName e LastName, un numero intero denominato RepeatCount e un parametro booleano denominato Show.</span><span class="sxs-lookup"><span data-stu-id="2749e-163">hello following example shows how toostart a runbook with two string parameters named FirstName and LastName, an integer named RepeatCount, and a boolean parameter named Show.</span></span> <span data-ttu-id="2749e-164">Per altre informazioni sui parametri, vedere [Parametri di Runbook](#Runbook-parameters) più avanti.</span><span class="sxs-lookup"><span data-stu-id="2749e-164">For additional information on parameters, see [Runbook Parameters](#Runbook-parameters) below.</span></span>

```
$params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
Start-AzureRmAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Test-Runbook" -ResourceGroupName "ResourceGroup01" –Parameters $params
```

## <a name="runbook-parameters"></a><span data-ttu-id="2749e-165">Parametri di Runbook</span><span class="sxs-lookup"><span data-stu-id="2749e-165">Runbook parameters</span></span>
<span data-ttu-id="2749e-166">Quando si avvia un runbook da hello portale di Azure o Windows PowerShell, istruzione hello viene inviato tramite hello servizio web di automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="2749e-166">When you start a runbook from hello Azure Portal or Windows PowerShell, hello instruction is sent through hello Azure Automation web service.</span></span> <span data-ttu-id="2749e-167">Questo servizio non supporta i parametri con tipi di dati complessi.</span><span class="sxs-lookup"><span data-stu-id="2749e-167">This service does not support parameters with complex data types.</span></span> <span data-ttu-id="2749e-168">Se è necessario tooprovide un valore per un parametro complesso, è necessario chiamarlo inline da un altro runbook come descritto in [figlio runbook in automazione di Azure](automation-child-runbooks.md).</span><span class="sxs-lookup"><span data-stu-id="2749e-168">If you need tooprovide a value for a complex parameter, then you must call it inline from another runbook as described in [Child runbooks in Azure Automation](automation-child-runbooks.md).</span></span>

<span data-ttu-id="2749e-169">servizio web di automazione di Azure Hello fornirà funzionalità speciali per i parametri che usano determinati tipi di dati come descritto in hello le sezioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="2749e-169">hello Azure Automation web service will provide special functionality for parameters using certain data types as described in hello following sections.</span></span>

### <a name="named-values"></a><span data-ttu-id="2749e-170">Valori denominati</span><span class="sxs-lookup"><span data-stu-id="2749e-170">Named values</span></span>
<span data-ttu-id="2749e-171">Se il parametro hello è il tipo di dati [object], quindi è possibile utilizzare hello seguente toosend formato JSON è un elenco di valori denominati: *{nome1: 'Valore1', Nome2: 'Valore2', Nome3: 'Value3'}*.</span><span class="sxs-lookup"><span data-stu-id="2749e-171">If hello parameter is data type [object], then you can use hello following JSON format toosend it a list of named values: *{Name1:'Value1', Name2:'Value2', Name3:'Value3'}*.</span></span> <span data-ttu-id="2749e-172">Questi valori devono essere tipi semplici.</span><span class="sxs-lookup"><span data-stu-id="2749e-172">These values must be simple types.</span></span> <span data-ttu-id="2749e-173">Hello runbook riceverà il parametro hello come un [PSCustomObject](https://msdn.microsoft.com/library/system.management.automation.pscustomobject%28v=vs.85%29.aspx) con proprietà corrispondenti tooeach denominato value.</span><span class="sxs-lookup"><span data-stu-id="2749e-173">hello runbook will receive hello parameter as a [PSCustomObject](https://msdn.microsoft.com/library/system.management.automation.pscustomobject%28v=vs.85%29.aspx) with properties that correspond tooeach named value.</span></span>

<span data-ttu-id="2749e-174">Prendere in considerazione hello seguente runbook di test che accetta un parametro denominato utente.</span><span class="sxs-lookup"><span data-stu-id="2749e-174">Consider hello following test runbook that accepts a parameter called user.</span></span>

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

<span data-ttu-id="2749e-175">Hello testo seguente può essere utilizzato per il parametro utente hello.</span><span class="sxs-lookup"><span data-stu-id="2749e-175">hello following text could be used for hello user parameter.</span></span>

```
{FirstName:'Joe',LastName:'Smith',RepeatCount:'2',Show:'True'}
```

<span data-ttu-id="2749e-176">Il risultato successivo output di hello.</span><span class="sxs-lookup"><span data-stu-id="2749e-176">This results in hello following output.</span></span>

```
Joe
Smith
Joe
Smith
```

### <a name="arrays"></a><span data-ttu-id="2749e-177">Matrici</span><span class="sxs-lookup"><span data-stu-id="2749e-177">Arrays</span></span>
<span data-ttu-id="2749e-178">Se il parametro hello è una matrice, ad esempio [array] o [string []], è possibile utilizzare hello seguenti toosend formato JSON è un elenco di valori: *[valore1, valore2, valore3]*.</span><span class="sxs-lookup"><span data-stu-id="2749e-178">If hello parameter is an array such as [array] or [string[]], then you can use hello following JSON format toosend it a list of values: *[Value1,Value2,Value3]*.</span></span> <span data-ttu-id="2749e-179">Questi valori devono essere tipi semplici.</span><span class="sxs-lookup"><span data-stu-id="2749e-179">These values must be simple types.</span></span>

<span data-ttu-id="2749e-180">Prendere in considerazione hello seguente runbook di test che accetta un parametro denominato *utente*.</span><span class="sxs-lookup"><span data-stu-id="2749e-180">Consider hello following test runbook that accepts a parameter called *user*.</span></span>

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

<span data-ttu-id="2749e-181">Hello testo seguente può essere utilizzato per il parametro utente hello.</span><span class="sxs-lookup"><span data-stu-id="2749e-181">hello following text could be used for hello user parameter.</span></span>

```
["Joe","Smith",2,true]
```

<span data-ttu-id="2749e-182">Il risultato successivo output di hello.</span><span class="sxs-lookup"><span data-stu-id="2749e-182">This results in hello following output.</span></span>

```
Joe
Smith
Joe
Smith
```

### <a name="credentials"></a><span data-ttu-id="2749e-183">Credenziali</span><span class="sxs-lookup"><span data-stu-id="2749e-183">Credentials</span></span>
<span data-ttu-id="2749e-184">Se il parametro hello è di tipo di dati **PSCredential**, sarà possibile specificare il nome di hello di un'automazione di Azure [asset delle credenziali](automation-credentials.md).</span><span class="sxs-lookup"><span data-stu-id="2749e-184">If hello parameter is data type **PSCredential**, then you can provide hello name of an Azure Automation [credential asset](automation-credentials.md).</span></span> <span data-ttu-id="2749e-185">Hello runbook recupererà credenziale hello con nome hello specificato.</span><span class="sxs-lookup"><span data-stu-id="2749e-185">hello runbook will retrieve hello credential with hello name that you specify.</span></span>

<span data-ttu-id="2749e-186">Prendere in considerazione hello seguente runbook di test che accetta un parametro denominato di credenziali.</span><span class="sxs-lookup"><span data-stu-id="2749e-186">Consider hello following test runbook that accepts a parameter called credential.</span></span>

```
Workflow Test-Parameters
{
   param (
      [Parameter(Mandatory=$true)][PSCredential]$credential
   )
   $credential.UserName
}
```

<span data-ttu-id="2749e-187">Hello seguente è possibile usare testo per il parametro utente hello supponendo che sia disponibile un asset credenziali denominato *My Credential*.</span><span class="sxs-lookup"><span data-stu-id="2749e-187">hello following text could be used for hello user parameter assuming that there was a credential asset called *My Credential*.</span></span>

```
My Credential
```

<span data-ttu-id="2749e-188">Supponendo che sia nome utente hello nella credenziale hello *jsmith*, di conseguenza, dopo l'output di hello.</span><span class="sxs-lookup"><span data-stu-id="2749e-188">Assuming hello username in hello credential was *jsmith*, this results in hello following output.</span></span>

```
jsmith
```

## <a name="next-steps"></a><span data-ttu-id="2749e-189">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2749e-189">Next steps</span></span>
* <span data-ttu-id="2749e-190">architettura di runbook Hello corrente dell'articolo fornisce una panoramica generale del runbook la gestione delle risorse in Azure e locali con hello Runbook Worker ibrido.</span><span class="sxs-lookup"><span data-stu-id="2749e-190">hello runbook architecture in current article provides a high-level overview of runbooks managing resources in Azure and on-premises with hello Hybrid Runbook Worker.</span></span>  <span data-ttu-id="2749e-191">toolearn sull'esecuzione di runbook di automazione nel Data Center, fare riferimento troppo[Runbook worker ibridi](automation-hybrid-runbook-worker.md).</span><span class="sxs-lookup"><span data-stu-id="2749e-191">toolearn about executing Automation runbooks in your datacenter, refer too[Hybrid Runbook Workers](automation-hybrid-runbook-worker.md).</span></span>
* <span data-ttu-id="2749e-192">toolearn ulteriori informazioni sulla creazione di runbook modulari toobe usata da altri runbook per le funzioni specifiche o comuni, hello vedere troppo[runbook figlio](automation-child-runbooks.md).</span><span class="sxs-lookup"><span data-stu-id="2749e-192">toolearn more about hello creating modular runbooks toobe used by other runbooks for specific or common functions, refer too[Child Runbooks](automation-child-runbooks.md).</span></span>

