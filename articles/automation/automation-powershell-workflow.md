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
# <a name="learning-key-windows-powershell-workflow-concepts-for-automation-runbooks"></a>Informazioni sui concetti chiave del flusso di lavoro di PowerShell per i runbook di Automazione 
I Runbook in Automazione di Azure vengono implementati come flussi di lavoro di Windows PowerShell.  Un flusso di lavoro di Windows PowerShell è uno script di Windows PowerShell simile tooa ma presenta alcune differenze significative che possono essere poco chiare tooa nuovo utente.  Anche se in questo articolo è toohelp previsto scrivere runbook tramite flusso di lavoro PowerShell, è consigliabile che scrivere runbook con PowerShell, a meno che non è necessario checkpoint.  Esistono alcune differenze di sintassi nella creazione dei runbook del flusso di lavoro di PowerShell e queste differenze richiedono un maggiore lavoro toowrite effettivo dei flussi di lavoro.  

Un flusso di lavoro è una sequenza di passaggi programmati e connessi che eseguono attività di lunga durata o richiedono il coordinamento di hello di più passaggi tra più dispositivi o nodi gestiti. vantaggi di un flusso di lavoro rispetto a un normale script Hello includono il possibilità hello toosimultaneously eseguire un'azione su più dispositivi e hello possibilità tooautomatically recupero dagli errori. Un flusso di lavoro di Windows PowerShell è uno script di Windows PowerShell che usa Windows Workflow Foundation. Mentre il flusso di lavoro hello viene scritta con la sintassi di Windows PowerShell e avviato da Windows PowerShell, viene elaborato da Windows Workflow Foundation.

Per informazioni dettagliate sugli argomenti hello in questo articolo, vedere [Guida introduttiva a Windows PowerShell Workflow](http://technet.microsoft.com/library/jj134242.aspx).

## <a name="basic-structure-of-a-workflow"></a>Struttura di base di un flusso di lavoro
Hello primo passaggio tooconverting PowerShell script tooa flusso di lavoro PowerShell è che la contiene con hello **flusso di lavoro** (parola chiave).  Un flusso di lavoro inizia con hello **flusso di lavoro** (parola chiave) seguita dal corpo hello dello script hello racchiuso tra parentesi graffe. nome di Hello del flusso di lavoro hello segue hello **flusso di lavoro** (parola chiave), come illustrato nella sintassi hello:

    Workflow Test-Workflow
    {
       <Commands>
    }

nome di Hello del flusso di lavoro hello deve corrispondere il nome di hello del runbook di automazione hello. Se hello runbook importato, quindi hello filename deve corrispondere al nome del flusso di lavoro hello e deve terminare con *ps1*.

tooadd parametri toohello flusso di lavoro, utilizzare hello **Param** come script tooa (parola chiave).

## <a name="code-changes"></a>Modifiche al codice
Codice del flusso di lavoro PowerShell è codice script tooPowerShell quasi identici ad eccezione di alcune modifiche significative.  Hello le sezioni seguenti descrivono le modifiche che è necessario uno script di PowerShell tooa toomake per tale toorun in un flusso di lavoro.

### <a name="activities"></a>attività
Un'attività è un'operazione specifica in un flusso di lavoro. Così come uno script è costituito da uno o più comandi, un flusso di lavoro è costituito da una o più attività eseguite in sequenza. Il flusso di lavoro di Windows PowerShell converte automaticamente numerosi hello tooactivities i cmdlet di Windows PowerShell durante l'esecuzione di un flusso di lavoro. Quando si specifica uno di questi cmdlet nel runbook, l'attività corrispondente hello viene eseguita da Windows Workflow Foundation. Per i cmdlet senza un'attività corrispondente, il flusso di lavoro di Windows PowerShell esegue automaticamente il cmdlet di hello all'interno di un [InlineScript](#inlinescript) attività. Esiste un set di cmdlet che sono esclusi e non possono essere usati in un flusso di lavoro, a meno che non vengano inclusi in modo esplicito in un blocco InlineScript. Per altri dettagli su questi concetti, vedere l'articolo relativo all' [uso di attività in flussi di lavoro di script](http://technet.microsoft.com/library/jj574194.aspx).

Attività flusso di lavoro condividono un set di tooconfigure parametri comuni del relativo funzionamento. Per informazioni dettagliate sui parametri comuni del flusso di lavoro di hello, vedere [about_WorkflowCommonParameters](http://technet.microsoft.com/library/jj129719.aspx).

### <a name="positional-parameters"></a>Parametri posizionali
Non è possibile utilizzare i parametri posizionali con attività e cmdlet in un flusso di lavoro.  Tutto ciò significa che è necessario utilizzare nomi di parametro.

Si consideri ad esempio hello seguente di codice che ottiene tutti i servizi in esecuzione.

     Get-Service | Where-Object {$_.Status -eq "Running"}

Se si tenta di toorun questo stesso codice in un flusso di lavoro, viene visualizzato un messaggio come "Parametro non è possibile impostare utilizzando hello specificato parametri denominati".  toocorrect, specificare il nome di parametro hello come illustrato di seguito hello.

    Workflow Get-RunningServices
    {
        Get-Service | Where-Object -FilterScript {$_.Status -eq "Running"}
    }

### <a name="deserialized-objects"></a>Oggetti deserializzati
Gli oggetti nei flussi di lavoro vengono deserializzati.  Ciò significa che le relative proprietà sono ancora disponibili, ma non i relativi metodi.  Si consideri ad esempio hello seguente codice di PowerShell che consente di arrestare un servizio utilizzando il metodo di arresto hello hello dell'oggetto del servizio.

    $Service = Get-Service -Name MyService
    $Service.Stop()

Se si tenta toorun questa operazione in un flusso di lavoro, viene visualizzato un errore indicante che "chiamata al metodo non è supportata in un flusso di lavoro di Windows PowerShell."  

Un'opzione è toowrap queste due righe di codice in un [InlineScript](#inlinescript) blocco nel qual caso $Service sarebbe un oggetto servizio all'interno di blocco hello.

    Workflow Stop-Service
    {
        InlineScript {
            $Service = Get-Service -Name MyService
            $Service.Stop()
        }
    }

Un'altra opzione è toouse un altro cmdlet che esegue hello stessa funzionalità come metodo hello, se disponibile.  In questo esempio, il cmdlet Stop-Service hello fornisce hello stessa funzionalità come metodo di arresto hello e si potrebbe usare hello seguenti informazioni per un flusso di lavoro.

    Workflow Stop-MyService
    {
        $Service = Get-Service -Name MyService
        Stop-Service -Name $Service.Name
    }


## <a name="inlinescript"></a>InlineScript
Hello **InlineScript** attività è utile quando è necessario uno o più comandi toorun come script di PowerShell tradizionale anziché del flusso di lavoro di PowerShell.  Mentre i comandi in un flusso di lavoro vengono inviati tooWindows Workflow Foundation per l'elaborazione, i comandi in un blocco InlineScript vengono elaborati da Windows PowerShell.

InlineScript utilizza hello segue sintassi riportata di seguito.

    InlineScript
    {
      <Script Block>
    } <Common Parameters>

È possibile restituire l'output da un InlineScript assegnando hello output tooa variabile. Hello esempio seguente si arresta un servizio e quindi restituisce il nome di servizio hello.

    Workflow Stop-MyService
    {
        $Output = InlineScript {
            $Service = Get-Service -Name MyService
            $Service.Stop()
            $Service
        }

        $Output.Name
    }


È possibile passare i valori in un blocco InlineScript, ma è necessario utilizzare il modificatore di ambito **$Using** .  Hello esempio seguente è identico toohello precedente esempio ad eccezione del fatto che hello nome del servizio viene fornito da una variabile.

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


Mentre l'attività InlineScript possono essere critiche determinati flussi di lavoro, non supportano i costrutti del flusso di lavoro e deve essere utilizzati solo quando necessario per hello seguenti motivi:

* Non è possibile usare [checkpoint](#checkpoints) all'interno di un blocco InlineScript. Se si verifica un errore all'interno di blocco hello, deve essere ripreso dall'inizio di hello del blocco di hello.
* Non è possibile usare l'[esecuzione parallela](#parallel-processing) all'interno di un blocco InlineScriptBlock.
* InlineScript influisce sulla scalabilità del flusso di lavoro hello poiché sospende la sessione di Windows PowerShell hello per l'intera durata di hello del blocco InlineScript hello.

Per altre informazioni sull'uso di InlineScript, vedere [Esecuzione dei comandi di Windows PowerShell in un flusso di lavoro](http://technet.microsoft.com/library/jj574197.aspx) e [about_InlineScript](http://technet.microsoft.com/library/jj649082.aspx).

## <a name="parallel-processing"></a>Elaborazione parallela
Uno dei vantaggi dei flussi di lavoro di Windows PowerShell è hello possibilità tooperform un set di comandi in parallelo anziché in sequenza come un tipico script.

È possibile utilizzare hello **parallela** toocreate (parola chiave) un blocco di script con comandi multipli eseguiti contemporaneamente. Questo metodo utilizza hello segue sintassi riportata di seguito. In questo caso, Activity1 e Activity2 parte hello contemporaneamente. Activity3 viene avviata solo dopo il completamento di Activity1 e Activity2.

    Parallel
    {
      <Activity1>
      <Activity2>
    }
    <Activity3>


Si consideri ad esempio seguendo i comandi di PowerShell che copiare più destinazioni di rete tooa file hello.  Questi comandi vengono eseguiti in sequenza in modo che un file deve essere completata la copia prima hello è successivo avvio.     

    Copy-Item -Path C:\LocalPath\File1.txt -Destination \\NetworkPath\File1.txt
    Copy-Item -Path C:\LocalPath\File2.txt -Destination \\NetworkPath\File2.txt
    Copy-Item -Path C:\LocalPath\File3.txt -Destination \\NetworkPath\File3.txt

Hello seguente flusso di lavoro esegue questi stessi comandi in parallelo in modo che tutti iniziare la copia in hello stesso tempo.  Solo dopo che sono tutti copiati è hello visualizzato messaggio di completamento.

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


È possibile utilizzare hello **ForEach-Parallel** costruire contemporaneamente tooprocess comandi per ogni elemento in una raccolta. elementi Hello hello raccolta vengono elaborati in parallelo mentre hello comandi hello blocco di script vengono eseguiti in sequenza. Questo metodo utilizza hello segue sintassi riportata di seguito. In questo caso, Activity1 inizia hello la stessa ora per tutti gli elementi nella raccolta di hello. Per ogni elemento, Activity2 inizia al termine di Activity1. Activity3 si avvia solo dopo il completamento di Activity1 e Activity2 per tutti gli elementi.

    ForEach -Parallel ($<item> in $<collection>)
    {
      <Activity1>
      <Activity2>
    }
    <Activity3>

Hello di esempio seguente è simile toohello precedente esempio la copia dei file in parallelo.  In questo caso, viene visualizzato un messaggio per ogni file al termine della copia.  Solo dopo che sono tutti copiati completamente è hello finale visualizzato messaggio di completamento.

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
> Non è consigliabile eseguire i runbook figlio in parallelo, in quanto ciò è dimostrato risultati inaffidabili toogive.  Hello output dal runbook figlio di hello talvolta non vengono visualizzati e le impostazioni di runbook di un elemento figlio possono influire hello altri runbook figlio parallela
>

## <a name="checkpoints"></a>Checkpoint
Oggetto *checkpoint* è uno snapshot dello stato corrente di hello del flusso di lavoro hello che include il valore corrente di hello per le variabili e qualsiasi output generato toothat punto. Se un flusso di lavoro termina in errore o viene sospeso, quindi hello successiva fase di che esecuzione, verrà avviato dall'ultimo checkpoint anziché inizio hello del flusso di lavoro hello.  È possibile impostare un checkpoint in un flusso di lavoro con hello **Checkpoint-Workflow** attività.

Nel seguente codice di esempio di hello, viene generata un'eccezione dopo Activity2 causando hello tooend del flusso di lavoro. Quando viene eseguito di nuovo flusso di lavoro hello, inizia eseguendo Activity2 questo stato subito dopo l'ultimo checkpoint hello impostato.

    <Activity1>
    Checkpoint-Workflow
    <Activity2>
    <Exception>
    <Activity3>

È consigliabile impostare i checkpoint in un flusso di lavoro dopo l'attività che possono essere soggette a tooexception e non deve essere ripetuto se flusso di lavoro hello viene ripreso. Si consideri ad esempio un flusso di lavoro con cui viene creata una macchina virtuale. È possibile impostare un checkpoint prima e dopo la macchina virtuale hello comandi toocreate hello. Se la creazione di hello non riesce, verranno ripetuti comandi hello se flusso di lavoro hello viene riavviato. Se il flusso di lavoro hello ha esito negativo dopo la creazione di hello ha esito positivo, quindi hello macchina virtuale verrà non essere creata nuovamente quando il flusso di lavoro hello viene ripreso.

Hello di esempio seguente copia percorso di rete di più file tooa e imposta un checkpoint dopo ogni file.  Se il percorso di rete hello viene perso, flusso di lavoro hello termina in errore.  Quando viene avviato nuovamente, riprenderà all'ultimo checkpoint hello vale a dire che solo i file hello che sono già stati copiati vengono ignorati.

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

Poiché le credenziali username non vengono mantenute dopo aver chiamato hello [Suspend-Workflow](https://technet.microsoft.com/library/jj733586.aspx) attività o dopo l'ultimo checkpoint hello, è necessario tooset hello credenziali toonull e quindi recuperarli nuovamente dall'archivio di asset hello dopo  **Suspend-Workflow** o checkpoint viene chiamato.  In caso contrario, è possibile che venga visualizzato hello seguente messaggio di errore: *non è possibile riprendere il processo del flusso di lavoro hello, perché i dati di persistenza potrebbero non essere completamente salvati, o salvati i dati di persistenza sono stati danneggiati. È necessario riavviare del flusso di lavoro di hello.*

Hello stesso codice seguente viene illustrato come toohandle questo dei runbook del flusso di lavoro di PowerShell.

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


Ciò non è necessario se si esegue l'autenticazione usando un account RunAs configurato con un'entità servizio.  

Per ulteriori informazioni sui checkpoint, vedere [tooa aggiunta di checkpoint del flusso di lavoro di Script](http://technet.microsoft.com/library/jj574114.aspx).

## <a name="next-steps"></a>Passaggi successivi
* tooget avviato con runbook del flusso di lavoro di PowerShell, vedere [il primo runbook del flusso di lavoro di PowerShell](automation-first-runbook-textual.md)
