---
title: Informazioni sul flusso di lavoro di PowerShell per Automazione di Azure | Microsoft Docs
description: "Questo articolo è concepito come una lezione rapida per autori che hanno familiarità con PowerShell per comprendere le differenze specifiche tra PowerShell e il flusso di lavoro di PowerShell e i concetti applicabili ai runbook di Automazione."
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
ms.openlocfilehash: 4de812c7f863e42a6ed10c2312d61b8377e06431
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="learning-key-windows-powershell-workflow-concepts-for-automation-runbooks"></a><span data-ttu-id="536a5-103">Informazioni sui concetti chiave del flusso di lavoro di PowerShell per i runbook di Automazione</span><span class="sxs-lookup"><span data-stu-id="536a5-103">Learning key Windows PowerShell Workflow concepts for Automation runbooks</span></span> 
<span data-ttu-id="536a5-104">I Runbook in Automazione di Azure vengono implementati come flussi di lavoro di Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="536a5-104">Runbooks in Azure Automation are implemented as Windows PowerShell Workflows.</span></span>  <span data-ttu-id="536a5-105">Un flusso di lavoro di Windows PowerShell è simile a uno script Windows PowerShell, ma presenta alcune differenze significative che possono generare confusione in un nuovo utente.</span><span class="sxs-lookup"><span data-stu-id="536a5-105">A Windows PowerShell Workflow is similar to a Windows PowerShell script but has some significant differences that can be confusing to a new user.</span></span>  <span data-ttu-id="536a5-106">Anche se lo scopo di questo articolo è illustrare come scrivere runbook con il flusso di lavoro di PowerShell, è consigliabile scrivere runbook con PowerShell, a meno che non siano necessari checkpoint.</span><span class="sxs-lookup"><span data-stu-id="536a5-106">While this article is intended to help you write runbooks using PowerShell workflow, we recommend you write runbooks using PowerShell unless you need checkpoints.</span></span>  <span data-ttu-id="536a5-107">Esistono numerose differenze sintattiche nella creazione dei runbook del flusso di lavoro di PowerShell e queste differenze richiedono maggiore impegno nella scrittura di flussi di lavoro efficaci.</span><span class="sxs-lookup"><span data-stu-id="536a5-107">There are several syntax differences when authoring PowerShell Workflow runbooks and these differences require a bit more work to write effective workflows.</span></span>  

<span data-ttu-id="536a5-108">Un flusso di lavoro è una sequenza di passaggi programmati connessi che eseguono operazioni a esecuzione prolungata o richiedono il coordinamento di più passaggi tra più dispositivi o nodi gestiti.</span><span class="sxs-lookup"><span data-stu-id="536a5-108">A workflow is a sequence of programmed, connected steps that perform long-running tasks or require the coordination of multiple steps across multiple devices or managed nodes.</span></span> <span data-ttu-id="536a5-109">I vantaggi di un flusso di lavoro rispetto a un normale script includono la possibilità di eseguire simultaneamente un'azione su più dispositivi e di eseguire il ripristino automatico dagli errori.</span><span class="sxs-lookup"><span data-stu-id="536a5-109">The benefits of a workflow over a normal script include the ability to simultaneously perform an action against multiple devices and the ability to automatically recover from failures.</span></span> <span data-ttu-id="536a5-110">Un flusso di lavoro di Windows PowerShell è uno script di Windows PowerShell che usa Windows Workflow Foundation.</span><span class="sxs-lookup"><span data-stu-id="536a5-110">A Windows PowerShell Workflow is a Windows PowerShell script that uses Windows Workflow Foundation.</span></span> <span data-ttu-id="536a5-111">Pur essendo scritto con la sintassi di Windows PowerShell e avviato da Windows PowerShell, un flusso di lavoro viene elaborato da Windows Workflow Foundation.</span><span class="sxs-lookup"><span data-stu-id="536a5-111">While the workflow is written with Windows PowerShell syntax and launched by Windows PowerShell, it is processed by Windows Workflow Foundation.</span></span>

<span data-ttu-id="536a5-112">Per informazioni dettagliate sugli argomenti inclusi in questo articolo, vedere [Informazioni sul flusso di lavoro di Windows PowerShell](http://technet.microsoft.com/library/jj134242.aspx).</span><span class="sxs-lookup"><span data-stu-id="536a5-112">For complete details on the topics in this article, see [Getting Started with Windows PowerShell Workflow](http://technet.microsoft.com/library/jj134242.aspx).</span></span>

## <a name="basic-structure-of-a-workflow"></a><span data-ttu-id="536a5-113">Struttura di base di un flusso di lavoro</span><span class="sxs-lookup"><span data-stu-id="536a5-113">Basic structure of a workflow</span></span>
<span data-ttu-id="536a5-114">Il primo passaggio per la conversione di uno script PowerShell in un flusso di lavoro consiste nell'includerlo con la parola chiave **Flusso di lavoro** .</span><span class="sxs-lookup"><span data-stu-id="536a5-114">The first step to converting a PowerShell script to a PowerShell workflow is enclosing it with the **Workflow** keyword.</span></span>  <span data-ttu-id="536a5-115">Un flusso di lavoro di Windows PowerShell inizia con la parola chiave **Flusso di lavoro** seguita dal corpo dello script racchiuso tra parentesi graffe.</span><span class="sxs-lookup"><span data-stu-id="536a5-115">A workflow starts with the **Workflow** keyword followed by the body of the script enclosed in braces.</span></span> <span data-ttu-id="536a5-116">Il nome del flusso di lavoro segue la parola chiave **Workflow**, come illustrato nella sintassi seguente:</span><span class="sxs-lookup"><span data-stu-id="536a5-116">The name of the workflow follows the **Workflow** keyword as shown in the following syntax:</span></span>

    Workflow Test-Workflow
    {
       <Commands>
    }

<span data-ttu-id="536a5-117">Il nome del flusso di lavoro deve corrispondere al nome del Runbook di Automazione.</span><span class="sxs-lookup"><span data-stu-id="536a5-117">The name of the workflow must match the name of the Automation runbook.</span></span> <span data-ttu-id="536a5-118">Se il runbook viene importato, il nome del file deve corrispondere al nome del flusso di lavoro e terminare con l'estensione *ps1*.</span><span class="sxs-lookup"><span data-stu-id="536a5-118">If the runbook is being imported, then the filename must match the workflow name and must end in *.ps1*.</span></span>

<span data-ttu-id="536a5-119">Per aggiungere parametri al flusso di lavoro, utilizzare la parola chiave **Param** esattamente come si farebbe con uno script.</span><span class="sxs-lookup"><span data-stu-id="536a5-119">To add parameters to the workflow, use the **Param** keyword just as you would to a script.</span></span>

## <a name="code-changes"></a><span data-ttu-id="536a5-120">Modifiche al codice</span><span class="sxs-lookup"><span data-stu-id="536a5-120">Code changes</span></span>
<span data-ttu-id="536a5-121">Il codice del flusso di lavoro di PowerShell è quasi identico al relativo codice di script, fatta eccezione per alcune modifiche significative.</span><span class="sxs-lookup"><span data-stu-id="536a5-121">PowerShell workflow code looks almost identical to PowerShell script code except for a few significant changes.</span></span>  <span data-ttu-id="536a5-122">Le sezioni seguenti descrivono le modifiche che è necessario apportare a uno script di PowerShell per l'esecuzione in un flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="536a5-122">The following sections describe changes that you need to make to a PowerShell script for it to run in a workflow.</span></span>

### <a name="activities"></a><span data-ttu-id="536a5-123">Attività</span><span class="sxs-lookup"><span data-stu-id="536a5-123">Activities</span></span>
<span data-ttu-id="536a5-124">Un'attività è un'operazione specifica in un flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="536a5-124">An activity is a specific task in a workflow.</span></span> <span data-ttu-id="536a5-125">Così come uno script è costituito da uno o più comandi, un flusso di lavoro è costituito da una o più attività eseguite in sequenza.</span><span class="sxs-lookup"><span data-stu-id="536a5-125">Just as a script is composed of one or more commands, a workflow is composed of one or more activities that are carried out in a sequence.</span></span> <span data-ttu-id="536a5-126">Il flusso di lavoro di Windows PowerShell converte automaticamente molti dei cmdlet di Windows PowerShell in attività quando esegue un flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="536a5-126">Windows PowerShell Workflow automatically converts many of the Windows PowerShell cmdlets to activities when it runs a workflow.</span></span> <span data-ttu-id="536a5-127">Quando si specifica uno di questi cmdlet in un runbook, l'attività corrispondente viene eseguita da Windows Workflow Foundation.</span><span class="sxs-lookup"><span data-stu-id="536a5-127">When you specify one of these cmdlets in your runbook, the corresponding activity is run by Windows Workflow Foundation.</span></span> <span data-ttu-id="536a5-128">I cmdlet senza un'attività corrispondente vengono eseguiti automaticamente dal flusso di lavoro di Windows PowerShell in un'attività [InlineScript](#inlinescript) .</span><span class="sxs-lookup"><span data-stu-id="536a5-128">For those cmdlets without a corresponding activity, Windows PowerShell Workflow automatically runs the cmdlet within an [InlineScript](#inlinescript) activity.</span></span> <span data-ttu-id="536a5-129">Esiste un set di cmdlet che sono esclusi e non possono essere usati in un flusso di lavoro, a meno che non vengano inclusi in modo esplicito in un blocco InlineScript.</span><span class="sxs-lookup"><span data-stu-id="536a5-129">There is a set of cmdlets that are excluded and cannot be used in a workflow unless you explicitly include them in an InlineScript block.</span></span> <span data-ttu-id="536a5-130">Per altri dettagli su questi concetti, vedere l'articolo relativo all' [uso di attività in flussi di lavoro di script](http://technet.microsoft.com/library/jj574194.aspx).</span><span class="sxs-lookup"><span data-stu-id="536a5-130">For further details on these concepts, see [Using Activities in Script Workflows](http://technet.microsoft.com/library/jj574194.aspx).</span></span>

<span data-ttu-id="536a5-131">Le attività dei flussi di lavoro condividono un set di parametri comuni per configurare il proprio funzionamento.</span><span class="sxs-lookup"><span data-stu-id="536a5-131">Workflow activities share a set of common parameters to configure their operation.</span></span> <span data-ttu-id="536a5-132">Per informazioni dettagliate sui parametri comuni dei flussi di lavoro, vedere [about_WorkflowCommonParameters](http://technet.microsoft.com/library/jj129719.aspx).</span><span class="sxs-lookup"><span data-stu-id="536a5-132">For details about the workflow common parameters, see [about_WorkflowCommonParameters](http://technet.microsoft.com/library/jj129719.aspx).</span></span>

### <a name="positional-parameters"></a><span data-ttu-id="536a5-133">Parametri posizionali</span><span class="sxs-lookup"><span data-stu-id="536a5-133">Positional parameters</span></span>
<span data-ttu-id="536a5-134">Non è possibile utilizzare i parametri posizionali con attività e cmdlet in un flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="536a5-134">You can't use positional parameters with activities and cmdlets in a workflow.</span></span>  <span data-ttu-id="536a5-135">Tutto ciò significa che è necessario utilizzare nomi di parametro.</span><span class="sxs-lookup"><span data-stu-id="536a5-135">All this means is that you must use parameter names.</span></span>

<span data-ttu-id="536a5-136">Si consideri, ad esempio, il codice seguente per rilevare tutti i servizi in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="536a5-136">For example, consider the following code that gets all running services.</span></span>

     Get-Service | Where-Object {$_.Status -eq "Running"}

<span data-ttu-id="536a5-137">Se si tenta di eseguire lo stesso codice in un flusso di lavoro, viene visualizzato un messaggio simile al seguente: "Impossibile risolvere il set di parametri mediante i parametri denominati specificati".</span><span class="sxs-lookup"><span data-stu-id="536a5-137">If you try to run this same code in a workflow, you receive a message like "Parameter set cannot be resolved using the specified named parameters."</span></span>  <span data-ttu-id="536a5-138">Per risolvere il problema, specificare il nome del parametro come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="536a5-138">To correct this, provide the parameter name as in the following.</span></span>

    Workflow Get-RunningServices
    {
        Get-Service | Where-Object -FilterScript {$_.Status -eq "Running"}
    }

### <a name="deserialized-objects"></a><span data-ttu-id="536a5-139">Oggetti deserializzati</span><span class="sxs-lookup"><span data-stu-id="536a5-139">Deserialized objects</span></span>
<span data-ttu-id="536a5-140">Gli oggetti nei flussi di lavoro vengono deserializzati.</span><span class="sxs-lookup"><span data-stu-id="536a5-140">Objects in workflows are deserialized.</span></span>  <span data-ttu-id="536a5-141">Ciò significa che le relative proprietà sono ancora disponibili, ma non i relativi metodi.</span><span class="sxs-lookup"><span data-stu-id="536a5-141">This means that their properties are still available, but not their methods.</span></span>  <span data-ttu-id="536a5-142">Ad esempio, si consideri il codice PowerShell riportato di seguito che consente di arrestare un servizio utilizzando il metodo Stop dell'oggetto Service.</span><span class="sxs-lookup"><span data-stu-id="536a5-142">For example, consider the following PowerShell code that stops a service using the Stop method of the Service object.</span></span>

    $Service = Get-Service -Name MyService
    $Service.Stop()

<span data-ttu-id="536a5-143">Se si tenta di eseguire questa operazione in un flusso di lavoro, viene visualizzato un errore indicante che la "chiamata al metodo non è supportata in un flusso di lavoro di Windows PowerShell".</span><span class="sxs-lookup"><span data-stu-id="536a5-143">If you try to run this in a workflow, you receive an error saying "Method invocation is not supported in a Windows PowerShell Workflow."</span></span>  

<span data-ttu-id="536a5-144">È possibile eseguire il wrapping di queste due righe di codice in un blocco [InlineScript](#inlinescript). In questo caso, $Service sarà un oggetto Service all'interno del blocco.</span><span class="sxs-lookup"><span data-stu-id="536a5-144">One option is to wrap these two lines of code in an [InlineScript](#inlinescript) block in which case $Service would be a service object within the block.</span></span>

    Workflow Stop-Service
    {
        InlineScript {
            $Service = Get-Service -Name MyService
            $Service.Stop()
        }
    }

<span data-ttu-id="536a5-145">Un'altra opzione consiste nell'utilizzare un altro cmdlet che esegue la stessa funzionalità del metodo, se disponibile.</span><span class="sxs-lookup"><span data-stu-id="536a5-145">Another option is to use another cmdlet that performs the same functionality as the method, if one is available.</span></span>  <span data-ttu-id="536a5-146">Nel presente esempio il cmdlet Stop-Service fornisce la stessa funzionalità del metodo Stop e consente di usare quanto segue per un flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="536a5-146">In our sample, the Stop-Service cmdlet provides the same functionality as the Stop method, and you could use the following for a workflow.</span></span>

    Workflow Stop-MyService
    {
        $Service = Get-Service -Name MyService
        Stop-Service -Name $Service.Name
    }


## <a name="inlinescript"></a><span data-ttu-id="536a5-147">InlineScript</span><span class="sxs-lookup"><span data-stu-id="536a5-147">InlineScript</span></span>
<span data-ttu-id="536a5-148">L'attività **InlineScript** risulta utile quando è necessario eseguire uno o più comandi tradizionali come script piuttosto che flusso di lavoro PowerShell.</span><span class="sxs-lookup"><span data-stu-id="536a5-148">The **InlineScript** activity is useful when you need to run one or more commands as traditional PowerShell script instead of PowerShell workflow.</span></span>  <span data-ttu-id="536a5-149">Mentre i comandi di un flusso di lavoro vengono inviati a Windows Workflow Foundation per l'elaborazione, i comandi in un blocco InlineScript vengono elaborati da Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="536a5-149">While commands in a workflow are sent to Windows Workflow Foundation for processing, commands in an InlineScript block are processed by Windows PowerShell.</span></span>

<span data-ttu-id="536a5-150">InlineScript usa la sintassi indicata di seguito.</span><span class="sxs-lookup"><span data-stu-id="536a5-150">InlineScript uses the following syntax shown below.</span></span>

    InlineScript
    {
      <Script Block>
    } <Common Parameters>

<span data-ttu-id="536a5-151">È possibile restituire l'output di un InlineScript assegnando l'output a una variabile.</span><span class="sxs-lookup"><span data-stu-id="536a5-151">You can return output from an InlineScript by assigning the output to a variable.</span></span> <span data-ttu-id="536a5-152">Nell'esempio seguente viene arrestato un servizio e viene quindi restituito il nome del servizio.</span><span class="sxs-lookup"><span data-stu-id="536a5-152">The following example stops a service and then outputs the service name.</span></span>

    Workflow Stop-MyService
    {
        $Output = InlineScript {
            $Service = Get-Service -Name MyService
            $Service.Stop()
            $Service
        }

        $Output.Name
    }


<span data-ttu-id="536a5-153">È possibile passare i valori in un blocco InlineScript, ma è necessario utilizzare il modificatore di ambito **$Using** .</span><span class="sxs-lookup"><span data-stu-id="536a5-153">You can pass values into an InlineScript block, but you must use **$Using** scope modifier.</span></span>  <span data-ttu-id="536a5-154">L'esempio seguente è identico all'esempio precedente, ad eccezione del fatto che il nome del servizio viene fornito da una variabile.</span><span class="sxs-lookup"><span data-stu-id="536a5-154">The following example is identical to the previous example except that the service name is provided by a variable.</span></span>

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


<span data-ttu-id="536a5-155">Anche se possono rivelarsi di importanza critica in alcuni flussi di lavoro, le attività di InlineScript non supportano costrutti di flussi di lavoro e devono essere usate solo se necessario per i motivi seguenti:</span><span class="sxs-lookup"><span data-stu-id="536a5-155">While InlineScript activities may be critical in certain workflows, they do not support workflow constructs and should only be used when necessary for the following reasons:</span></span>

* <span data-ttu-id="536a5-156">Non è possibile usare [checkpoint](#checkpoints) all'interno di un blocco InlineScript.</span><span class="sxs-lookup"><span data-stu-id="536a5-156">You cannot use [checkpoints](#checkpoints) inside an InlineScript block.</span></span> <span data-ttu-id="536a5-157">Se si verifica un errore nel blocco, è necessario riprendere dall'inizio del blocco.</span><span class="sxs-lookup"><span data-stu-id="536a5-157">If a failure occurs within the block, it must be resumed from the beginning of the block.</span></span>
* <span data-ttu-id="536a5-158">Non è possibile usare l'[esecuzione parallela](#parallel-processing) all'interno di un blocco InlineScriptBlock.</span><span class="sxs-lookup"><span data-stu-id="536a5-158">You cannot use [parallel execution](#parallel-processing) inside an InlineScriptBlock.</span></span>
* <span data-ttu-id="536a5-159">L'attività InlineScript influisce sulla scalabilità del Runbook perché vincola la sessione di Windows PowerShell per l'intera lunghezza del blocco InlineScript.</span><span class="sxs-lookup"><span data-stu-id="536a5-159">InlineScript affects scalability of the workflow since it holds the Windows PowerShell session for the entire length of the InlineScript block.</span></span>

<span data-ttu-id="536a5-160">Per altre informazioni sull'uso di InlineScript, vedere [Esecuzione dei comandi di Windows PowerShell in un flusso di lavoro](http://technet.microsoft.com/library/jj574197.aspx) e [about_InlineScript](http://technet.microsoft.com/library/jj649082.aspx).</span><span class="sxs-lookup"><span data-stu-id="536a5-160">For more information on using InlineScript, see [Running Windows PowerShell Commands in a Workflow](http://technet.microsoft.com/library/jj574197.aspx) and [about_InlineScript](http://technet.microsoft.com/library/jj649082.aspx).</span></span>

## <a name="parallel-processing"></a><span data-ttu-id="536a5-161">Elaborazione parallela</span><span class="sxs-lookup"><span data-stu-id="536a5-161">Parallel processing</span></span>
<span data-ttu-id="536a5-162">Uno dei vantaggi offerti dai flussi di lavoro di Windows PowerShell consiste nella possibilità di eseguire un set di comandi in parallelo anziché in sequenza, come accade invece con uno script tipico.</span><span class="sxs-lookup"><span data-stu-id="536a5-162">One advantage of Windows PowerShell Workflows is the ability to perform a set of commands in parallel instead of sequentially as with a typical script.</span></span>

<span data-ttu-id="536a5-163">È possibile usare la parola chiave **Parallel** per creare un blocco di script con più comandi che vengono eseguiti contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="536a5-163">You can use the **Parallel** keyword to create a script block with multiple commands that run concurrently.</span></span> <span data-ttu-id="536a5-164">Viene usata la sintassi indicata di seguito.</span><span class="sxs-lookup"><span data-stu-id="536a5-164">This uses the following syntax shown below.</span></span> <span data-ttu-id="536a5-165">In questo caso Activity1 e Activity2 iniziano nello stesso momento.</span><span class="sxs-lookup"><span data-stu-id="536a5-165">In this case, Activity1 and Activity2 starts at the same time.</span></span> <span data-ttu-id="536a5-166">Activity3 viene avviata solo dopo il completamento di Activity1 e Activity2.</span><span class="sxs-lookup"><span data-stu-id="536a5-166">Activity3 starts only after both Activity1 and Activity2 have completed.</span></span>

    Parallel
    {
      <Activity1>
      <Activity2>
    }
    <Activity3>


<span data-ttu-id="536a5-167">Ad esempio, considerare i seguenti comandi PowerShell che consentono di copiare più file in una destinazione di rete.</span><span class="sxs-lookup"><span data-stu-id="536a5-167">For example, consider the following PowerShell commands that copy multiple files to a network destination.</span></span>  <span data-ttu-id="536a5-168">Questi comandi vengono eseguiti in sequenza in modo che finisca la copia di un file prima che venga avviata la successiva.</span><span class="sxs-lookup"><span data-stu-id="536a5-168">These commands are run sequentially so that one file must finish copying before the next is started.</span></span>     

    Copy-Item -Path C:\LocalPath\File1.txt -Destination \\NetworkPath\File1.txt
    Copy-Item -Path C:\LocalPath\File2.txt -Destination \\NetworkPath\File2.txt
    Copy-Item -Path C:\LocalPath\File3.txt -Destination \\NetworkPath\File3.txt

<span data-ttu-id="536a5-169">Nel flusso di lavoro seguente vengono eseguiti questi stessi comandi in parallelo in modo che inizi la copia di tutti nello stesso momento.</span><span class="sxs-lookup"><span data-stu-id="536a5-169">The following workflow runs these same commands in parallel so that they all start copying at the same time.</span></span>  <span data-ttu-id="536a5-170">Solo dopo che la copia è terminata, viene visualizzato il messaggio di completamento.</span><span class="sxs-lookup"><span data-stu-id="536a5-170">Only after they are all copied is the completion message displayed.</span></span>

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


<span data-ttu-id="536a5-171">È possibile usare il costrutto **ForEach -Parallel** per elaborare i comandi per ogni elemento di una raccolta simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="536a5-171">You can use the **ForEach -Parallel** construct to process commands for each item in a collection concurrently.</span></span> <span data-ttu-id="536a5-172">Gli elementi della raccolta vengono elaborati in parallelo, mentre i comandi nel blocco di script vengono eseguiti in sequenza.</span><span class="sxs-lookup"><span data-stu-id="536a5-172">The items in the collection are processed in parallel while the commands in the script block run sequentially.</span></span> <span data-ttu-id="536a5-173">Viene usata la sintassi indicata di seguito.</span><span class="sxs-lookup"><span data-stu-id="536a5-173">This uses the following syntax shown below.</span></span> <span data-ttu-id="536a5-174">In questo caso l'avvio di Activity1 è simultaneo a quello di tutti gli altri elementi della raccolta.</span><span class="sxs-lookup"><span data-stu-id="536a5-174">In this case, Activity1 starts at the same time for all items in the collection.</span></span> <span data-ttu-id="536a5-175">Per ogni elemento, Activity2 inizia al termine di Activity1.</span><span class="sxs-lookup"><span data-stu-id="536a5-175">For each item, Activity2 starts after Activity1 is complete.</span></span> <span data-ttu-id="536a5-176">Activity3 si avvia solo dopo il completamento di Activity1 e Activity2 per tutti gli elementi.</span><span class="sxs-lookup"><span data-stu-id="536a5-176">Activity3 starts only after both Activity1 and Activity2 have completed for all items.</span></span>

    ForEach -Parallel ($<item> in $<collection>)
    {
      <Activity1>
      <Activity2>
    }
    <Activity3>

<span data-ttu-id="536a5-177">L'esempio seguente è simile all'esempio precedente in cui vengono copiati i file in parallelo.</span><span class="sxs-lookup"><span data-stu-id="536a5-177">The following example is similar to the previous example copying files in parallel.</span></span>  <span data-ttu-id="536a5-178">In questo caso, viene visualizzato un messaggio per ogni file al termine della copia.</span><span class="sxs-lookup"><span data-stu-id="536a5-178">In this case, a message is displayed for each file after it copies.</span></span>  <span data-ttu-id="536a5-179">Solo dopo che stati tutti copiati completamente, viene visualizzato il messaggio di completamento finale.</span><span class="sxs-lookup"><span data-stu-id="536a5-179">Only after they are all completely copied is the final completion message displayed.</span></span>

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
> <span data-ttu-id="536a5-180">Si sconsiglia l'esecuzione di Runbook figlio in parallelo poiché è stato dimostrato che potrebbe causare risultati inaffidabili.</span><span class="sxs-lookup"><span data-stu-id="536a5-180">We do not recommend running child runbooks in parallel since this has been shown to give unreliable results.</span></span>  <span data-ttu-id="536a5-181">L'output dal runbook figlio talvolta non viene visualizzato e le impostazioni di un runbook figlio possono influire sugli altri runbook figlio paralleli.</span><span class="sxs-lookup"><span data-stu-id="536a5-181">The output from the child runbook sometimes does not show up, and settings in one child runbook can affect the other parallel child runbooks</span></span>
>

## <a name="checkpoints"></a><span data-ttu-id="536a5-182">Checkpoint</span><span class="sxs-lookup"><span data-stu-id="536a5-182">Checkpoints</span></span>
<span data-ttu-id="536a5-183">Un *checkpoint* è uno snapshot dello stato corrente del flusso di lavoro che include il valore corrente per le variabili e gli output generati fino al punto corrispondente.</span><span class="sxs-lookup"><span data-stu-id="536a5-183">A *checkpoint* is a snapshot of the current state of the workflow that includes the current value for variables and any output generated to that point.</span></span> <span data-ttu-id="536a5-184">Se un flusso di lavoro termina con errori o viene sospeso, alla successiva esecuzione verrà avviato dall'ultimo checkpoint anziché dall'inizio del flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="536a5-184">If a workflow ends in error or is suspended, then the next time it is run it will start from its last checkpoint instead of the start of the worfklow.</span></span>  <span data-ttu-id="536a5-185">È possibile impostare un checkpoint in un flusso di lavoro con l'attività **Checkpoint-Workflow** .</span><span class="sxs-lookup"><span data-stu-id="536a5-185">You can set a checkpoint in a workflow with the **Checkpoint-Workflow** activity.</span></span>

<span data-ttu-id="536a5-186">Nel codice di esempio seguente si verifica un'eccezione dopo Activity2 con la conseguente sospensione del Runbook.</span><span class="sxs-lookup"><span data-stu-id="536a5-186">In the following sample code, an exception occurs after Activity2 causing the workflow to end.</span></span> <span data-ttu-id="536a5-187">Quando il flusso di lavoro viene nuovamente avviato, inizierà con l'esecuzione di Activity2, poiché questa attività si trovava immediatamente dopo l'ultimo checkpoint impostato.</span><span class="sxs-lookup"><span data-stu-id="536a5-187">When the workflow is run again, it starts by running Activity2 since this was just after the last checkpoint set.</span></span>

    <Activity1>
    Checkpoint-Workflow
    <Activity2>
    <Exception>
    <Activity3>

<span data-ttu-id="536a5-188">È consigliabile impostare checkpoint in un flusso di lavoro dopo attività che possono essere soggette a eccezioni e che non devono essere ripetute se riprende il flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="536a5-188">You should set checkpoints in a workflow after activities that may be prone to exception and should not be repeated if the workflow is resumed.</span></span> <span data-ttu-id="536a5-189">Si consideri ad esempio un flusso di lavoro con cui viene creata una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="536a5-189">For example, your workflow may create a virtual machine.</span></span> <span data-ttu-id="536a5-190">È possibile impostare un checkpoint sia prima che dopo i comandi di creazione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="536a5-190">You could set a checkpoint both before and after the commands to create the virtual machine.</span></span> <span data-ttu-id="536a5-191">Se la creazione ha esito negativo, i comandi verrebbero ripetuti se il flusso di lavoro viene riavviato.</span><span class="sxs-lookup"><span data-stu-id="536a5-191">If the creation fails, then the commands would be repeated if the workflow is started again.</span></span> <span data-ttu-id="536a5-192">Se il flusso di lavoro ha esito negativo dopo il completamento della creazione, la macchina virtuale non verrà creata nuovamente quando verrà ripreso il flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="536a5-192">If the worfklow fails after the creation succeeds, then the virtual machine will not be created again when the workflow is resumed.</span></span>

<span data-ttu-id="536a5-193">Nell'esempio seguente vengono copiati più file in un percorso di rete e viene impostato un checkpoint dopo ogni file.</span><span class="sxs-lookup"><span data-stu-id="536a5-193">The following example copies multiple files to a network location and sets a checkpoint after each file.</span></span>  <span data-ttu-id="536a5-194">Se il percorso di rete viene perso, il flusso di lavoro termina con errori.</span><span class="sxs-lookup"><span data-stu-id="536a5-194">If the network location is lost, then the workflow ends in error.</span></span>  <span data-ttu-id="536a5-195">Quando viene avviato nuovamente, verrà ripreso dall'ultimo checkpoint, vale a dire che solo i file che sono già stati copiati vengono ignorati.</span><span class="sxs-lookup"><span data-stu-id="536a5-195">When it is started again, it will resume at the last checkpoint meaning that only the files that have already been copied are skipped.</span></span>

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

<span data-ttu-id="536a5-196">Poiché le credenziali nome utente non vengono rese permanenti dopo la chiamata dell'attività [Suspend-Workflow](https://technet.microsoft.com/library/jj733586.aspx) o dopo l'ultimo checkpoint, è necessario impostare le credenziali su Null e quindi recuperarle di nuovo dall'archivio di asset dopo la chiamata di **Suspend-Workflow** o del checkpoint.</span><span class="sxs-lookup"><span data-stu-id="536a5-196">Because username credentials are not persisted after you call the [Suspend-Workflow](https://technet.microsoft.com/library/jj733586.aspx) activity or after the last checkpoint, you need to set the credentials to null and then retrieve them again from the asset store after **Suspend-Workflow** or checkpoint is called.</span></span>  <span data-ttu-id="536a5-197">In caso contrario, è possibile che venga visualizzato il messaggio di errore seguente: *Impossibile riprendere il processo del flusso di lavoro perché i dati di persistenza non sono stati salvati completamente o i dati di persistenza salvati sono danneggiati. È necessario riavviare il flusso di lavoro.*</span><span class="sxs-lookup"><span data-stu-id="536a5-197">Otherwise, you may receive the following error message: *The workflow job cannot be resumed, either because persistence data could not be saved completely, or saved persistence data has been corrupted. You must restart the workflow.*</span></span>

<span data-ttu-id="536a5-198">Il codice seguente mostra come gestire questa situazione nei runbook del flusso di lavoro di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="536a5-198">The following same code demonstrates how to handle this in your PowerShell Workflow runbooks.</span></span>

    workflow CreateTestVms
    {
       $Cred = Get-AzureAutomationCredential -Name "MyCredential"
       $null = Add-AzureRmAccount -Credential $Cred

       $VmsToCreate = Get-AzureAutomationVariable -Name "VmsToCreate"

       foreach ($VmName in $VmsToCreate)
         {
          # Do work first to create the VM (code not shown)

          # Now add the VM
          New-AzureRmVm -VM $Vm -Location "WestUs" -ResourceGroupName "ResourceGroup01"

          # Checkpoint so that VM creation is not repeated if workflow suspends
          $Cred = $null
          Checkpoint-Workflow
          $Cred = Get-AzureAutomationCredential -Name "MyCredential"
          $null = Add-AzureRmAccount -Credential $Cred
         }
     }


<span data-ttu-id="536a5-199">Ciò non è necessario se si esegue l'autenticazione usando un account RunAs configurato con un'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="536a5-199">This is not required if you are authenticating using a Run As account configured with a service principal.</span></span>  

<span data-ttu-id="536a5-200">Per altre informazioni sui checkpoint, vedere l'articolo relativo all' [aggiunta di checkpoint a un flusso di lavoro di script](http://technet.microsoft.com/library/jj574114.aspx).</span><span class="sxs-lookup"><span data-stu-id="536a5-200">For more information about checkpoints, see [Adding Checkpoints to a Script Workflow](http://technet.microsoft.com/library/jj574114.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="536a5-201">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="536a5-201">Next steps</span></span>
* <span data-ttu-id="536a5-202">Per iniziare a usare i runbook del flusso di lavoro PowerShell, vedere [Il primo runbook del flusso di lavoro PowerShell](automation-first-runbook-textual.md)</span><span class="sxs-lookup"><span data-stu-id="536a5-202">To get started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md)</span></span>
