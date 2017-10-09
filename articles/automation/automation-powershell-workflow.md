---
title: flusso di lavoro per l'automazione di Azure PowerShell aaaLearning | Documenti Microsoft
description: "In questo articolo è destinato come una lezione rapida autori familiari con le differenze specifiche di PowerShell toounderstand hello tra PowerShell e flusso di lavoro PowerShell e i concetti applicabili tooAutomation runbook."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 84bf133e-5343-4e0e-8d6c-bb14304a70db
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/21/2017
ms.author: magoedte;bwren
ms.openlocfilehash: 362c504eb96d31b99a826b128e6a591beecaa084
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="learning-key-windows-powershell-workflow-concepts-for-automation-runbooks"></a><span data-ttu-id="3941d-103">Informazioni sui concetti chiave del flusso di lavoro di PowerShell per i runbook di Automazione</span><span class="sxs-lookup"><span data-stu-id="3941d-103">Learning key Windows PowerShell Workflow concepts for Automation runbooks</span></span> 
<span data-ttu-id="3941d-104">I Runbook in Automazione di Azure vengono implementati come flussi di lavoro di Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3941d-104">Runbooks in Azure Automation are implemented as Windows PowerShell Workflows.</span></span>  <span data-ttu-id="3941d-105">Un flusso di lavoro di Windows PowerShell è uno script di Windows PowerShell simile tooa ma presenta alcune differenze significative che possono essere poco chiare tooa nuovo utente.</span><span class="sxs-lookup"><span data-stu-id="3941d-105">A Windows PowerShell Workflow is similar tooa Windows PowerShell script but has some significant differences that can be confusing tooa new user.</span></span>  <span data-ttu-id="3941d-106">Anche se in questo articolo è toohelp previsto scrivere runbook tramite flusso di lavoro PowerShell, è consigliabile che scrivere runbook con PowerShell, a meno che non è necessario checkpoint.</span><span class="sxs-lookup"><span data-stu-id="3941d-106">While this article is intended toohelp you write runbooks using PowerShell workflow, we recommend you write runbooks using PowerShell unless you need checkpoints.</span></span>  <span data-ttu-id="3941d-107">Esistono alcune differenze di sintassi nella creazione dei runbook del flusso di lavoro di PowerShell e queste differenze richiedono un maggiore lavoro toowrite effettivo dei flussi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="3941d-107">There are several syntax differences when authoring PowerShell Workflow runbooks and these differences require a bit more work toowrite effective workflows.</span></span>  

<span data-ttu-id="3941d-108">Un flusso di lavoro è una sequenza di passaggi programmati e connessi che eseguono attività di lunga durata o richiedono il coordinamento di hello di più passaggi tra più dispositivi o nodi gestiti.</span><span class="sxs-lookup"><span data-stu-id="3941d-108">A workflow is a sequence of programmed, connected steps that perform long-running tasks or require hello coordination of multiple steps across multiple devices or managed nodes.</span></span> <span data-ttu-id="3941d-109">vantaggi di un flusso di lavoro rispetto a un normale script Hello includono il possibilità hello toosimultaneously eseguire un'azione su più dispositivi e hello possibilità tooautomatically recupero dagli errori.</span><span class="sxs-lookup"><span data-stu-id="3941d-109">hello benefits of a workflow over a normal script include hello ability toosimultaneously perform an action against multiple devices and hello ability tooautomatically recover from failures.</span></span> <span data-ttu-id="3941d-110">Un flusso di lavoro di Windows PowerShell è uno script di Windows PowerShell che usa Windows Workflow Foundation.</span><span class="sxs-lookup"><span data-stu-id="3941d-110">A Windows PowerShell Workflow is a Windows PowerShell script that uses Windows Workflow Foundation.</span></span> <span data-ttu-id="3941d-111">Mentre il flusso di lavoro hello viene scritta con la sintassi di Windows PowerShell e avviato da Windows PowerShell, viene elaborato da Windows Workflow Foundation.</span><span class="sxs-lookup"><span data-stu-id="3941d-111">While hello workflow is written with Windows PowerShell syntax and launched by Windows PowerShell, it is processed by Windows Workflow Foundation.</span></span>

<span data-ttu-id="3941d-112">Per informazioni dettagliate sugli argomenti hello in questo articolo, vedere [Guida introduttiva a Windows PowerShell Workflow](http://technet.microsoft.com/library/jj134242.aspx).</span><span class="sxs-lookup"><span data-stu-id="3941d-112">For complete details on hello topics in this article, see [Getting Started with Windows PowerShell Workflow](http://technet.microsoft.com/library/jj134242.aspx).</span></span>

## <a name="basic-structure-of-a-workflow"></a><span data-ttu-id="3941d-113">Struttura di base di un flusso di lavoro</span><span class="sxs-lookup"><span data-stu-id="3941d-113">Basic structure of a workflow</span></span>
<span data-ttu-id="3941d-114">Hello primo passaggio tooconverting PowerShell script tooa flusso di lavoro PowerShell è che la contiene con hello **flusso di lavoro** (parola chiave).</span><span class="sxs-lookup"><span data-stu-id="3941d-114">hello first step tooconverting a PowerShell script tooa PowerShell workflow is enclosing it with hello **Workflow** keyword.</span></span>  <span data-ttu-id="3941d-115">Un flusso di lavoro inizia con hello **flusso di lavoro** (parola chiave) seguita dal corpo hello dello script hello racchiuso tra parentesi graffe.</span><span class="sxs-lookup"><span data-stu-id="3941d-115">A workflow starts with hello **Workflow** keyword followed by hello body of hello script enclosed in braces.</span></span> <span data-ttu-id="3941d-116">nome di Hello del flusso di lavoro hello segue hello **flusso di lavoro** (parola chiave), come illustrato nella sintassi hello:</span><span class="sxs-lookup"><span data-stu-id="3941d-116">hello name of hello workflow follows hello **Workflow** keyword as shown in hello following syntax:</span></span>

    Workflow Test-Workflow
    {
       <Commands>
    }

<span data-ttu-id="3941d-117">nome di Hello del flusso di lavoro hello deve corrispondere il nome di hello del runbook di automazione hello.</span><span class="sxs-lookup"><span data-stu-id="3941d-117">hello name of hello workflow must match hello name of hello Automation runbook.</span></span> <span data-ttu-id="3941d-118">Se hello runbook importato, quindi hello filename deve corrispondere al nome del flusso di lavoro hello e deve terminare con *ps1*.</span><span class="sxs-lookup"><span data-stu-id="3941d-118">If hello runbook is being imported, then hello filename must match hello workflow name and must end in *.ps1*.</span></span>

<span data-ttu-id="3941d-119">tooadd parametri toohello flusso di lavoro, utilizzare hello **Param** come script tooa (parola chiave).</span><span class="sxs-lookup"><span data-stu-id="3941d-119">tooadd parameters toohello workflow, use hello **Param** keyword just as you would tooa script.</span></span>

## <a name="code-changes"></a><span data-ttu-id="3941d-120">Modifiche al codice</span><span class="sxs-lookup"><span data-stu-id="3941d-120">Code changes</span></span>
<span data-ttu-id="3941d-121">Codice del flusso di lavoro PowerShell è codice script tooPowerShell quasi identici ad eccezione di alcune modifiche significative.</span><span class="sxs-lookup"><span data-stu-id="3941d-121">PowerShell workflow code looks almost identical tooPowerShell script code except for a few significant changes.</span></span>  <span data-ttu-id="3941d-122">Hello le sezioni seguenti descrivono le modifiche che è necessario uno script di PowerShell tooa toomake per tale toorun in un flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="3941d-122">hello following sections describe changes that you need toomake tooa PowerShell script for it toorun in a workflow.</span></span>

### <a name="activities"></a><span data-ttu-id="3941d-123">attività</span><span class="sxs-lookup"><span data-stu-id="3941d-123">Activities</span></span>
<span data-ttu-id="3941d-124">Un'attività è un'operazione specifica in un flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="3941d-124">An activity is a specific task in a workflow.</span></span> <span data-ttu-id="3941d-125">Così come uno script è costituito da uno o più comandi, un flusso di lavoro è costituito da una o più attività eseguite in sequenza.</span><span class="sxs-lookup"><span data-stu-id="3941d-125">Just as a script is composed of one or more commands, a workflow is composed of one or more activities that are carried out in a sequence.</span></span> <span data-ttu-id="3941d-126">Il flusso di lavoro di Windows PowerShell converte automaticamente numerosi hello tooactivities i cmdlet di Windows PowerShell durante l'esecuzione di un flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="3941d-126">Windows PowerShell Workflow automatically converts many of hello Windows PowerShell cmdlets tooactivities when it runs a workflow.</span></span> <span data-ttu-id="3941d-127">Quando si specifica uno di questi cmdlet nel runbook, l'attività corrispondente hello viene eseguita da Windows Workflow Foundation.</span><span class="sxs-lookup"><span data-stu-id="3941d-127">When you specify one of these cmdlets in your runbook, hello corresponding activity is run by Windows Workflow Foundation.</span></span> <span data-ttu-id="3941d-128">Per i cmdlet senza un'attività corrispondente, il flusso di lavoro di Windows PowerShell esegue automaticamente il cmdlet di hello all'interno di un [InlineScript](#inlinescript) attività.</span><span class="sxs-lookup"><span data-stu-id="3941d-128">For those cmdlets without a corresponding activity, Windows PowerShell Workflow automatically runs hello cmdlet within an [InlineScript](#inlinescript) activity.</span></span> <span data-ttu-id="3941d-129">Esiste un set di cmdlet che sono esclusi e non possono essere usati in un flusso di lavoro, a meno che non vengano inclusi in modo esplicito in un blocco InlineScript.</span><span class="sxs-lookup"><span data-stu-id="3941d-129">There is a set of cmdlets that are excluded and cannot be used in a workflow unless you explicitly include them in an InlineScript block.</span></span> <span data-ttu-id="3941d-130">Per altri dettagli su questi concetti, vedere l'articolo relativo all' [uso di attività in flussi di lavoro di script](http://technet.microsoft.com/library/jj574194.aspx).</span><span class="sxs-lookup"><span data-stu-id="3941d-130">For further details on these concepts, see [Using Activities in Script Workflows](http://technet.microsoft.com/library/jj574194.aspx).</span></span>

<span data-ttu-id="3941d-131">Attività flusso di lavoro condividono un set di tooconfigure parametri comuni del relativo funzionamento.</span><span class="sxs-lookup"><span data-stu-id="3941d-131">Workflow activities share a set of common parameters tooconfigure their operation.</span></span> <span data-ttu-id="3941d-132">Per informazioni dettagliate sui parametri comuni del flusso di lavoro di hello, vedere [about_WorkflowCommonParameters](http://technet.microsoft.com/library/jj129719.aspx).</span><span class="sxs-lookup"><span data-stu-id="3941d-132">For details about hello workflow common parameters, see [about_WorkflowCommonParameters](http://technet.microsoft.com/library/jj129719.aspx).</span></span>

### <a name="positional-parameters"></a><span data-ttu-id="3941d-133">Parametri posizionali</span><span class="sxs-lookup"><span data-stu-id="3941d-133">Positional parameters</span></span>
<span data-ttu-id="3941d-134">Non è possibile utilizzare i parametri posizionali con attività e cmdlet in un flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="3941d-134">You can't use positional parameters with activities and cmdlets in a workflow.</span></span>  <span data-ttu-id="3941d-135">Tutto ciò significa che è necessario utilizzare nomi di parametro.</span><span class="sxs-lookup"><span data-stu-id="3941d-135">All this means is that you must use parameter names.</span></span>

<span data-ttu-id="3941d-136">Si consideri ad esempio hello seguente di codice che ottiene tutti i servizi in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="3941d-136">For example, consider hello following code that gets all running services.</span></span>

     Get-Service | Where-Object {$_.Status -eq "Running"}

<span data-ttu-id="3941d-137">Se si tenta di toorun questo stesso codice in un flusso di lavoro, viene visualizzato un messaggio come "Parametro non è possibile impostare utilizzando hello specificato parametri denominati".</span><span class="sxs-lookup"><span data-stu-id="3941d-137">If you try toorun this same code in a workflow, you receive a message like "Parameter set cannot be resolved using hello specified named parameters."</span></span>  <span data-ttu-id="3941d-138">toocorrect, specificare il nome di parametro hello come illustrato di seguito hello.</span><span class="sxs-lookup"><span data-stu-id="3941d-138">toocorrect this, provide hello parameter name as in hello following.</span></span>

    Workflow Get-RunningServices
    {
        Get-Service | Where-Object -FilterScript {$_.Status -eq "Running"}
    }

### <a name="deserialized-objects"></a><span data-ttu-id="3941d-139">Oggetti deserializzati</span><span class="sxs-lookup"><span data-stu-id="3941d-139">Deserialized objects</span></span>
<span data-ttu-id="3941d-140">Gli oggetti nei flussi di lavoro vengono deserializzati.</span><span class="sxs-lookup"><span data-stu-id="3941d-140">Objects in workflows are deserialized.</span></span>  <span data-ttu-id="3941d-141">Ciò significa che le relative proprietà sono ancora disponibili, ma non i relativi metodi.</span><span class="sxs-lookup"><span data-stu-id="3941d-141">This means that their properties are still available, but not their methods.</span></span>  <span data-ttu-id="3941d-142">Si consideri ad esempio hello seguente codice di PowerShell che consente di arrestare un servizio utilizzando il metodo di arresto hello hello dell'oggetto del servizio.</span><span class="sxs-lookup"><span data-stu-id="3941d-142">For example, consider hello following PowerShell code that stops a service using hello Stop method of hello Service object.</span></span>

    $Service = Get-Service -Name MyService
    $Service.Stop()

<span data-ttu-id="3941d-143">Se si tenta toorun questa operazione in un flusso di lavoro, viene visualizzato un errore indicante che "chiamata al metodo non è supportata in un flusso di lavoro di Windows PowerShell."</span><span class="sxs-lookup"><span data-stu-id="3941d-143">If you try toorun this in a workflow, you receive an error saying "Method invocation is not supported in a Windows PowerShell Workflow."</span></span>  

<span data-ttu-id="3941d-144">Un'opzione è toowrap queste due righe di codice in un [InlineScript](#inlinescript) blocco nel qual caso $Service sarebbe un oggetto servizio all'interno di blocco hello.</span><span class="sxs-lookup"><span data-stu-id="3941d-144">One option is toowrap these two lines of code in an [InlineScript](#inlinescript) block in which case $Service would be a service object within hello block.</span></span>

    Workflow Stop-Service
    {
        InlineScript {
            $Service = Get-Service -Name MyService
            $Service.Stop()
        }
    }

<span data-ttu-id="3941d-145">Un'altra opzione è toouse un altro cmdlet che esegue hello stessa funzionalità come metodo hello, se disponibile.</span><span class="sxs-lookup"><span data-stu-id="3941d-145">Another option is toouse another cmdlet that performs hello same functionality as hello method, if one is available.</span></span>  <span data-ttu-id="3941d-146">In questo esempio, il cmdlet Stop-Service hello fornisce hello stessa funzionalità come metodo di arresto hello e si potrebbe usare hello seguenti informazioni per un flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="3941d-146">In our sample, hello Stop-Service cmdlet provides hello same functionality as hello Stop method, and you could use hello following for a workflow.</span></span>

    Workflow Stop-MyService
    {
        $Service = Get-Service -Name MyService
        Stop-Service -Name $Service.Name
    }


## <a name="inlinescript"></a><span data-ttu-id="3941d-147">InlineScript</span><span class="sxs-lookup"><span data-stu-id="3941d-147">InlineScript</span></span>
<span data-ttu-id="3941d-148">Hello **InlineScript** attività è utile quando è necessario uno o più comandi toorun come script di PowerShell tradizionale anziché del flusso di lavoro di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3941d-148">hello **InlineScript** activity is useful when you need toorun one or more commands as traditional PowerShell script instead of PowerShell workflow.</span></span>  <span data-ttu-id="3941d-149">Mentre i comandi in un flusso di lavoro vengono inviati tooWindows Workflow Foundation per l'elaborazione, i comandi in un blocco InlineScript vengono elaborati da Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3941d-149">While commands in a workflow are sent tooWindows Workflow Foundation for processing, commands in an InlineScript block are processed by Windows PowerShell.</span></span>

<span data-ttu-id="3941d-150">InlineScript utilizza hello segue sintassi riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="3941d-150">InlineScript uses hello following syntax shown below.</span></span>

    InlineScript
    {
      <Script Block>
    } <Common Parameters>

<span data-ttu-id="3941d-151">È possibile restituire l'output da un InlineScript assegnando hello output tooa variabile.</span><span class="sxs-lookup"><span data-stu-id="3941d-151">You can return output from an InlineScript by assigning hello output tooa variable.</span></span> <span data-ttu-id="3941d-152">Hello esempio seguente si arresta un servizio e quindi restituisce il nome di servizio hello.</span><span class="sxs-lookup"><span data-stu-id="3941d-152">hello following example stops a service and then outputs hello service name.</span></span>

    Workflow Stop-MyService
    {
        $Output = InlineScript {
            $Service = Get-Service -Name MyService
            $Service.Stop()
            $Service
        }

        $Output.Name
    }


<span data-ttu-id="3941d-153">È possibile passare i valori in un blocco InlineScript, ma è necessario utilizzare il modificatore di ambito **$Using** .</span><span class="sxs-lookup"><span data-stu-id="3941d-153">You can pass values into an InlineScript block, but you must use **$Using** scope modifier.</span></span>  <span data-ttu-id="3941d-154">Hello esempio seguente è identico toohello precedente esempio ad eccezione del fatto che hello nome del servizio viene fornito da una variabile.</span><span class="sxs-lookup"><span data-stu-id="3941d-154">hello following example is identical toohello previous example except that hello service name is provided by a variable.</span></span>

    Workflow Stop-MyService
    {
        $ServiceName = "MyService"

        $Output = InlineScript {
            $Service = Get-Service -Name $Using:ServiceName
            $Service.Stop()
            $Service
        }

        $Output.Name
    }


<span data-ttu-id="3941d-155">Mentre l'attività InlineScript possono essere critiche determinati flussi di lavoro, non supportano i costrutti del flusso di lavoro e deve essere utilizzati solo quando necessario per hello seguenti motivi:</span><span class="sxs-lookup"><span data-stu-id="3941d-155">While InlineScript activities may be critical in certain workflows, they do not support workflow constructs and should only be used when necessary for hello following reasons:</span></span>

* <span data-ttu-id="3941d-156">Non è possibile usare [checkpoint](#checkpoints) all'interno di un blocco InlineScript.</span><span class="sxs-lookup"><span data-stu-id="3941d-156">You cannot use [checkpoints](#checkpoints) inside an InlineScript block.</span></span> <span data-ttu-id="3941d-157">Se si verifica un errore all'interno di blocco hello, deve essere ripreso dall'inizio di hello del blocco di hello.</span><span class="sxs-lookup"><span data-stu-id="3941d-157">If a failure occurs within hello block, it must be resumed from hello beginning of hello block.</span></span>
* <span data-ttu-id="3941d-158">Non è possibile usare l'[esecuzione parallela](#parallel-processing) all'interno di un blocco InlineScriptBlock.</span><span class="sxs-lookup"><span data-stu-id="3941d-158">You cannot use [parallel execution](#parallel-processing) inside an InlineScriptBlock.</span></span>
* <span data-ttu-id="3941d-159">InlineScript influisce sulla scalabilità del flusso di lavoro hello poiché sospende la sessione di Windows PowerShell hello per l'intera durata di hello del blocco InlineScript hello.</span><span class="sxs-lookup"><span data-stu-id="3941d-159">InlineScript affects scalability of hello workflow since it holds hello Windows PowerShell session for hello entire length of hello InlineScript block.</span></span>

<span data-ttu-id="3941d-160">Per altre informazioni sull'uso di InlineScript, vedere [Esecuzione dei comandi di Windows PowerShell in un flusso di lavoro](http://technet.microsoft.com/library/jj574197.aspx) e [about_InlineScript](http://technet.microsoft.com/library/jj649082.aspx).</span><span class="sxs-lookup"><span data-stu-id="3941d-160">For more information on using InlineScript, see [Running Windows PowerShell Commands in a Workflow](http://technet.microsoft.com/library/jj574197.aspx) and [about_InlineScript](http://technet.microsoft.com/library/jj649082.aspx).</span></span>

## <a name="parallel-processing"></a><span data-ttu-id="3941d-161">Elaborazione parallela</span><span class="sxs-lookup"><span data-stu-id="3941d-161">Parallel processing</span></span>
<span data-ttu-id="3941d-162">Uno dei vantaggi dei flussi di lavoro di Windows PowerShell è hello possibilità tooperform un set di comandi in parallelo anziché in sequenza come un tipico script.</span><span class="sxs-lookup"><span data-stu-id="3941d-162">One advantage of Windows PowerShell Workflows is hello ability tooperform a set of commands in parallel instead of sequentially as with a typical script.</span></span>

<span data-ttu-id="3941d-163">È possibile utilizzare hello **parallela** toocreate (parola chiave) un blocco di script con comandi multipli eseguiti contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="3941d-163">You can use hello **Parallel** keyword toocreate a script block with multiple commands that run concurrently.</span></span> <span data-ttu-id="3941d-164">Questo metodo utilizza hello segue sintassi riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="3941d-164">This uses hello following syntax shown below.</span></span> <span data-ttu-id="3941d-165">In questo caso, Activity1 e Activity2 parte hello contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="3941d-165">In this case, Activity1 and Activity2 starts at hello same time.</span></span> <span data-ttu-id="3941d-166">Activity3 viene avviata solo dopo il completamento di Activity1 e Activity2.</span><span class="sxs-lookup"><span data-stu-id="3941d-166">Activity3 starts only after both Activity1 and Activity2 have completed.</span></span>

    Parallel
    {
      <Activity1>
      <Activity2>
    }
    <Activity3>


<span data-ttu-id="3941d-167">Si consideri ad esempio seguendo i comandi di PowerShell che copiare più destinazioni di rete tooa file hello.</span><span class="sxs-lookup"><span data-stu-id="3941d-167">For example, consider hello following PowerShell commands that copy multiple files tooa network destination.</span></span>  <span data-ttu-id="3941d-168">Questi comandi vengono eseguiti in sequenza in modo che un file deve essere completata la copia prima hello è successivo avvio.</span><span class="sxs-lookup"><span data-stu-id="3941d-168">These commands are run sequentially so that one file must finish copying before hello next is started.</span></span>     

    Copy-Item -Path C:\LocalPath\File1.txt -Destination \\NetworkPath\File1.txt
    Copy-Item -Path C:\LocalPath\File2.txt -Destination \\NetworkPath\File2.txt
    Copy-Item -Path C:\LocalPath\File3.txt -Destination \\NetworkPath\File3.txt

<span data-ttu-id="3941d-169">Hello seguente flusso di lavoro esegue questi stessi comandi in parallelo in modo che tutti iniziare la copia in hello stesso tempo.</span><span class="sxs-lookup"><span data-stu-id="3941d-169">hello following workflow runs these same commands in parallel so that they all start copying at hello same time.</span></span>  <span data-ttu-id="3941d-170">Solo dopo che sono tutti copiati è hello visualizzato messaggio di completamento.</span><span class="sxs-lookup"><span data-stu-id="3941d-170">Only after they are all copied is hello completion message displayed.</span></span>

    Workflow Copy-Files
    {
        Parallel
        {
            Copy-Item -Path "C:\LocalPath\File1.txt" -Destination "\\NetworkPath"
            Copy-Item -Path "C:\LocalPath\File2.txt" -Destination "\\NetworkPath"
            Copy-Item -Path "C:\LocalPath\File3.txt" -Destination "\\NetworkPath"
        }

        Write-Output "Files copied."
    }


<span data-ttu-id="3941d-171">È possibile utilizzare hello **ForEach-Parallel** costruire contemporaneamente tooprocess comandi per ogni elemento in una raccolta.</span><span class="sxs-lookup"><span data-stu-id="3941d-171">You can use hello **ForEach -Parallel** construct tooprocess commands for each item in a collection concurrently.</span></span> <span data-ttu-id="3941d-172">elementi Hello hello raccolta vengono elaborati in parallelo mentre hello comandi hello blocco di script vengono eseguiti in sequenza.</span><span class="sxs-lookup"><span data-stu-id="3941d-172">hello items in hello collection are processed in parallel while hello commands in hello script block run sequentially.</span></span> <span data-ttu-id="3941d-173">Questo metodo utilizza hello segue sintassi riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="3941d-173">This uses hello following syntax shown below.</span></span> <span data-ttu-id="3941d-174">In questo caso, Activity1 inizia hello la stessa ora per tutti gli elementi nella raccolta di hello.</span><span class="sxs-lookup"><span data-stu-id="3941d-174">In this case, Activity1 starts at hello same time for all items in hello collection.</span></span> <span data-ttu-id="3941d-175">Per ogni elemento, Activity2 inizia al termine di Activity1.</span><span class="sxs-lookup"><span data-stu-id="3941d-175">For each item, Activity2 starts after Activity1 is complete.</span></span> <span data-ttu-id="3941d-176">Activity3 si avvia solo dopo il completamento di Activity1 e Activity2 per tutti gli elementi.</span><span class="sxs-lookup"><span data-stu-id="3941d-176">Activity3 starts only after both Activity1 and Activity2 have completed for all items.</span></span>

    ForEach -Parallel ($<item> in $<collection>)
    {
      <Activity1>
      <Activity2>
    }
    <Activity3>

<span data-ttu-id="3941d-177">Hello di esempio seguente è simile toohello precedente esempio la copia dei file in parallelo.</span><span class="sxs-lookup"><span data-stu-id="3941d-177">hello following example is similar toohello previous example copying files in parallel.</span></span>  <span data-ttu-id="3941d-178">In questo caso, viene visualizzato un messaggio per ogni file al termine della copia.</span><span class="sxs-lookup"><span data-stu-id="3941d-178">In this case, a message is displayed for each file after it copies.</span></span>  <span data-ttu-id="3941d-179">Solo dopo che sono tutti copiati completamente è hello finale visualizzato messaggio di completamento.</span><span class="sxs-lookup"><span data-stu-id="3941d-179">Only after they are all completely copied is hello final completion message displayed.</span></span>

    Workflow Copy-Files
    {
        $files = @("C:\LocalPath\File1.txt","C:\LocalPath\File2.txt","C:\LocalPath\File3.txt")

        ForEach -Parallel ($File in $Files)
        {
            Copy-Item -Path $File -Destination \\NetworkPath
            Write-Output "$File copied."
        }

        Write-Output "All files copied."
    }

> [!NOTE]
> <span data-ttu-id="3941d-180">Non è consigliabile eseguire i runbook figlio in parallelo, in quanto ciò è dimostrato risultati inaffidabili toogive.</span><span class="sxs-lookup"><span data-stu-id="3941d-180">We do not recommend running child runbooks in parallel since this has been shown toogive unreliable results.</span></span>  <span data-ttu-id="3941d-181">Hello output dal runbook figlio di hello talvolta non vengono visualizzati e le impostazioni di runbook di un elemento figlio possono influire hello altri runbook figlio parallela</span><span class="sxs-lookup"><span data-stu-id="3941d-181">hello output from hello child runbook sometimes does not show up, and settings in one child runbook can affect hello other parallel child runbooks</span></span>
>

## <a name="checkpoints"></a><span data-ttu-id="3941d-182">Checkpoint</span><span class="sxs-lookup"><span data-stu-id="3941d-182">Checkpoints</span></span>
<span data-ttu-id="3941d-183">Oggetto *checkpoint* è uno snapshot dello stato corrente di hello del flusso di lavoro hello che include il valore corrente di hello per le variabili e qualsiasi output generato toothat punto.</span><span class="sxs-lookup"><span data-stu-id="3941d-183">A *checkpoint* is a snapshot of hello current state of hello workflow that includes hello current value for variables and any output generated toothat point.</span></span> <span data-ttu-id="3941d-184">Se un flusso di lavoro termina in errore o viene sospeso, quindi hello successiva fase di che esecuzione, verrà avviato dall'ultimo checkpoint anziché inizio hello del flusso di lavoro hello.</span><span class="sxs-lookup"><span data-stu-id="3941d-184">If a workflow ends in error or is suspended, then hello next time it is run it will start from its last checkpoint instead of hello start of hello worfklow.</span></span>  <span data-ttu-id="3941d-185">È possibile impostare un checkpoint in un flusso di lavoro con hello **Checkpoint-Workflow** attività.</span><span class="sxs-lookup"><span data-stu-id="3941d-185">You can set a checkpoint in a workflow with hello **Checkpoint-Workflow** activity.</span></span>

<span data-ttu-id="3941d-186">Nel seguente codice di esempio di hello, viene generata un'eccezione dopo Activity2 causando hello tooend del flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="3941d-186">In hello following sample code, an exception occurs after Activity2 causing hello workflow tooend.</span></span> <span data-ttu-id="3941d-187">Quando viene eseguito di nuovo flusso di lavoro hello, inizia eseguendo Activity2 questo stato subito dopo l'ultimo checkpoint hello impostato.</span><span class="sxs-lookup"><span data-stu-id="3941d-187">When hello workflow is run again, it starts by running Activity2 since this was just after hello last checkpoint set.</span></span>

    <Activity1>
    Checkpoint-Workflow
    <Activity2>
    <Exception>
    <Activity3>

<span data-ttu-id="3941d-188">È consigliabile impostare i checkpoint in un flusso di lavoro dopo l'attività che possono essere soggette a tooexception e non deve essere ripetuto se flusso di lavoro hello viene ripreso.</span><span class="sxs-lookup"><span data-stu-id="3941d-188">You should set checkpoints in a workflow after activities that may be prone tooexception and should not be repeated if hello workflow is resumed.</span></span> <span data-ttu-id="3941d-189">Si consideri ad esempio un flusso di lavoro con cui viene creata una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="3941d-189">For example, your workflow may create a virtual machine.</span></span> <span data-ttu-id="3941d-190">È possibile impostare un checkpoint prima e dopo la macchina virtuale hello comandi toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="3941d-190">You could set a checkpoint both before and after hello commands toocreate hello virtual machine.</span></span> <span data-ttu-id="3941d-191">Se la creazione di hello non riesce, verranno ripetuti comandi hello se flusso di lavoro hello viene riavviato.</span><span class="sxs-lookup"><span data-stu-id="3941d-191">If hello creation fails, then hello commands would be repeated if hello workflow is started again.</span></span> <span data-ttu-id="3941d-192">Se il flusso di lavoro hello ha esito negativo dopo la creazione di hello ha esito positivo, quindi hello macchina virtuale verrà non essere creata nuovamente quando il flusso di lavoro hello viene ripreso.</span><span class="sxs-lookup"><span data-stu-id="3941d-192">If hello worfklow fails after hello creation succeeds, then hello virtual machine will not be created again when hello workflow is resumed.</span></span>

<span data-ttu-id="3941d-193">Hello di esempio seguente copia percorso di rete di più file tooa e imposta un checkpoint dopo ogni file.</span><span class="sxs-lookup"><span data-stu-id="3941d-193">hello following example copies multiple files tooa network location and sets a checkpoint after each file.</span></span>  <span data-ttu-id="3941d-194">Se il percorso di rete hello viene perso, flusso di lavoro hello termina in errore.</span><span class="sxs-lookup"><span data-stu-id="3941d-194">If hello network location is lost, then hello workflow ends in error.</span></span>  <span data-ttu-id="3941d-195">Quando viene avviato nuovamente, riprenderà all'ultimo checkpoint hello vale a dire che solo i file hello che sono già stati copiati vengono ignorati.</span><span class="sxs-lookup"><span data-stu-id="3941d-195">When it is started again, it will resume at hello last checkpoint meaning that only hello files that have already been copied are skipped.</span></span>

    Workflow Copy-Files
    {
        $files = @("C:\LocalPath\File1.txt","C:\LocalPath\File2.txt","C:\LocalPath\File3.txt")

        ForEach ($File in $Files)
        {
            Copy-Item -Path $File -Destination \\NetworkPath
            Write-Output "$File copied."
            Checkpoint-Workflow
        }

        Write-Output "All files copied."
    }

<span data-ttu-id="3941d-196">Poiché le credenziali username non vengono mantenute dopo aver chiamato hello [Suspend-Workflow](https://technet.microsoft.com/library/jj733586.aspx) attività o dopo l'ultimo checkpoint hello, è necessario tooset hello credenziali toonull e quindi recuperarli nuovamente dall'archivio di asset hello dopo  **Suspend-Workflow** o checkpoint viene chiamato.</span><span class="sxs-lookup"><span data-stu-id="3941d-196">Because username credentials are not persisted after you call hello [Suspend-Workflow](https://technet.microsoft.com/library/jj733586.aspx) activity or after hello last checkpoint, you need tooset hello credentials toonull and then retrieve them again from hello asset store after **Suspend-Workflow** or checkpoint is called.</span></span>  <span data-ttu-id="3941d-197">In caso contrario, è possibile che venga visualizzato hello seguente messaggio di errore: *non è possibile riprendere il processo del flusso di lavoro hello, perché i dati di persistenza potrebbero non essere completamente salvati, o salvati i dati di persistenza sono stati danneggiati. È necessario riavviare del flusso di lavoro di hello.*</span><span class="sxs-lookup"><span data-stu-id="3941d-197">Otherwise, you may receive hello following error message: *hello workflow job cannot be resumed, either because persistence data could not be saved completely, or saved persistence data has been corrupted. You must restart hello workflow.*</span></span>

<span data-ttu-id="3941d-198">Hello stesso codice seguente viene illustrato come toohandle questo dei runbook del flusso di lavoro di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3941d-198">hello following same code demonstrates how toohandle this in your PowerShell Workflow runbooks.</span></span>

    workflow CreateTestVms
    {
       $Cred = Get-AzureAutomationCredential -Name "MyCredential"
       $null = Add-AzureRmAccount -Credential $Cred

       $VmsToCreate = Get-AzureAutomationVariable -Name "VmsToCreate"

       foreach ($VmName in $VmsToCreate)
         {
          # Do work first toocreate hello VM (code not shown)

          # Now add hello VM
          New-AzureRmVm -VM $Vm -Location "WestUs" -ResourceGroupName "ResourceGroup01"

          # Checkpoint so that VM creation is not repeated if workflow suspends
          $Cred = $null
          Checkpoint-Workflow
          $Cred = Get-AzureAutomationCredential -Name "MyCredential"
          $null = Add-AzureRmAccount -Credential $Cred
         }
     }


<span data-ttu-id="3941d-199">Ciò non è necessario se si esegue l'autenticazione usando un account RunAs configurato con un'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="3941d-199">This is not required if you are authenticating using a Run As account configured with a service principal.</span></span>  

<span data-ttu-id="3941d-200">Per ulteriori informazioni sui checkpoint, vedere [tooa aggiunta di checkpoint del flusso di lavoro di Script](http://technet.microsoft.com/library/jj574114.aspx).</span><span class="sxs-lookup"><span data-stu-id="3941d-200">For more information about checkpoints, see [Adding Checkpoints tooa Script Workflow](http://technet.microsoft.com/library/jj574114.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3941d-201">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3941d-201">Next steps</span></span>
* <span data-ttu-id="3941d-202">tooget avviato con runbook del flusso di lavoro di PowerShell, vedere [il primo runbook del flusso di lavoro di PowerShell](automation-first-runbook-textual.md)</span><span class="sxs-lookup"><span data-stu-id="3941d-202">tooget started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md)</span></span>
