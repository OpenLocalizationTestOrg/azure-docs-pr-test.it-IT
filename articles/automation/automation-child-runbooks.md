---
title: aaaChild runbook in automazione di Azure | Documenti Microsoft
description: Descrive hello diversi metodi per l'avvio di un runbook in automazione di Azure da un altro runbook e la condivisione di informazioni tra di essi.
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 919887b9-43e2-4c16-883c-f81807fe37db
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2017
ms.author: magoedte;bwren
ms.openlocfilehash: d3d06818d344b565d53cc4f4705b41dcfcf9a376
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="child-runbooks-in-azure-automation"></a>Runbook figlio in Automazione di Azure
È buona norma in automazione di Azure toowrite runbook modulari riutilizzabili con una funzione discreta che può essere utilizzato da altri runbook. Un runbook padre spesso chiama uno o più runbook figlio funzionalità tooperform richiesto. Esistono due modi toocall un runbook figlio e ognuno presenta delle differenze distinte che è necessario comprendere in modo che è possibile determinare che sarà migliore per i diversi scenari.

## <a name="invoking-a-child-runbook-using-inline-execution"></a>Richiamare un runbook figlio con esecuzione inline
tooinvoke un runbook inline da un altro runbook, utilizzare il nome di hello del runbook hello e fornire valori per i relativi parametri, esattamente come si farebbe un'attività o un cmdlet.  Tutti i runbook hello stesso account di automazione sono disponibili tooall altre toobe usati in questo modo. Hello il runbook padre attenderà hello figlio runbook toocomplete prima di spostare la riga successiva toohello e qualsiasi output verrà restituito direttamente toohello padre.

Quando si richiama un runbook inline, viene eseguito in hello stesso processo come hello del runbook padre. Non ci sarà alcuna indicazione nella cronologia processo hello di hello i runbook figlio eseguito. Tutte le eccezioni e gli output dal runbook figlio hello flusso sarà associati all'oggetto padre hello. Ciò comporta un minor numero di processi e li rende più semplice tootrack e tootroubleshoot poiché le eccezioni generate dal runbook figlio hello e del relativo flusso di output presenti associati al processo padre hello.

Quando viene pubblicato un runbook, tutti i runbook figlio chiamati devono già essere pubblicati. Questo avviene perché l'automazione di Azure crea un'associazione con i runbook figlio quando viene compilato un runbook. In caso contrario, verrà visualizzato correttamente toopublish hello il runbook padre, ma genererà un'eccezione quando viene avviata. In questo caso, è possibile ripubblicare il runbook padre hello in ordine tooproperly riferimento hello figlio runbook. Non è necessario il runbook padre hello toorepublish se uno dei runbook figlio hello viene modificato perché l'associazione di hello è già stata creata.

parametri di Hello di un runbook figlio chiamato inline possono essere qualsiasi tipo di dati, compresi gli oggetti complessi e non esiste alcun [serializzazione JSON](automation-starting-a-runbook.md#runbook-parameters) come avviene quando si avvia runbook hello utilizzando hello portale di gestione di Azure o con hello Cmdlet Start-AzureRmAutomationRunbook.

### <a name="runbook-types"></a>Tipi di runbook
Tipi che possono richiamarsi a vicenda:

* Un [runbook di PowerShell](automation-runbook-types.md#powershell-runbooks) e i [runbook grafici](automation-runbook-types.md#graphical-runbooks) possono chiamarsi reciprocamente inline (entrambi i tipi sono basati su PowerShell).
* Un [runbook del flusso di lavoro PowerShell](automation-runbook-types.md#powershell-workflow-runbooks) e i runbook grafici del flusso di lavoro PowerShell possono richiamarsi a vicenda inline (entrambi i tipi si basano su PowerShell).
* Hello tipi PowerShell e hello che tipi di flusso di lavoro PowerShell non è possibile chiamare loro inline, deve utilizzare AzureRmAutomationRunbook di inizio.

Quando è importante l’ordine di pubblicazione:

* Hello pubblicare l'ordine dei è rilevante solo i runbook per i runbook del flusso di lavoro di PowerShell e con interfaccia grafica del flusso di lavoro di PowerShell.

Quando si chiama un runbook figlio grafico o del flusso di lavoro di PowerShell con l'esecuzione inline, è sufficiente utilizzare il nome di hello di hello runbook.  Quando si chiama un runbook figlio di PowerShell, è necessario preceduto il proprio nome con *.\\*  toospecify che hello script si trova nella directory locale hello. 

### <a name="example"></a>Esempio
Hello di esempio seguente richiama un runbook figlio di prova che accetta tre parametri, un oggetto complesso, un numero intero e un valore booleano. output di Hello del runbook figlio hello viene assegnato tooa variabile.  In questo caso, il runbook figlio hello è un runbook del flusso di lavoro di PowerShell

    $vm = Get-AzureRmVM –ResourceGroupName "LabRG" –Name "MyVM"
    $output = PSWF-ChildRunbook –VM $vm –RepeatCount 2 –Restart $true

Di seguito è hello stesso esempio con un runbook PowerShell come elemento figlio di hello.

    $vm = Get-AzureRmVM –ResourceGroupName "LabRG" –Name "MyVM"
    $output = .\PS-ChildRunbook.ps1 –VM $vm –RepeatCount 2 –Restart $true


## <a name="starting-a-child-runbook-using-cmdlet"></a>Avvio di un runbook figlio utilizzando cmdlet
È possibile utilizzare hello [inizio AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) toostart cmdlet un runbook come descritto in [toostart un runbook con Windows PowerShell](automation-starting-a-runbook.md#starting-a-runbook-with-windows-powershell). Sono disponibili due modalità di utilizzo di questo cmdlet.  In modalità di hello cmdlet restituisce l'id di processo hello non appena viene creato il processo di figlio hello per runbook figlio hello.  In altre modalità, che è abilitare specificando hello di hello **-attendere** parametro hello cmdlet attenderà figlio hello al termine del processo e verrà restituito l'output di hello dal runbook figlio hello.

il processo di Hello da un runbook figlio avviato con un cmdlet verrà eseguito in un processo separato dal runbook padre hello. Questo comporta più processi rispetto al richiamo inline di runbook hello e li rende più difficile tootrack. Hello padre può però avviare più runbook figlio in modo asincrono senza attendere che ogni toocomplete. Per questo stesso tipo di esecuzione parallela chiamando i runbook figlio hello inline, il runbook padre hello sarebbe necessario hello toouse [parola chiave parallel](automation-powershell-workflow.md#parallel-processing).

I parametri per un runbook figlio avviato con un cmdlet vengono forniti come una tabella hash, come descritto in [Parametri di Runbook](automation-starting-a-runbook.md#runbook-parameters). Possono essere utilizzati solo tipi di dati semplici. Se hello runbook dispone di un parametro con un tipo di dati complesso, dovrà essere chiamato inline.

### <a name="example"></a>Esempio
Hello esempio seguente avvia un runbook figlio con parametri e quindi attende toocomplete utilizzando hello inizio AzureRmAutomationRunbook-attendere parametro. Una volta completato, l'output viene raccolto dal runbook figlio hello.

    $params = @{"VMName"="MyVM";"RepeatCount"=2;"Restart"=$true} 
    $joboutput = Start-AzureRmAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Test-ChildRunbook" -ResourceGroupName "LabRG" –Parameters $params –wait


## <a name="comparison-of-methods-for-calling-a-child-runbook"></a>Confronto di metodi per chiamare un runbook figlio
Hello nella tabella seguente sono riepilogate differenze di hello tra hello due metodi per chiamare un runbook da un altro runbook.

|  | Inline | Cmdlet |
|:--- |:--- |:--- |
| Job |Runbook figlio vengono eseguiti nello stesso processo come padre hello hello. |Viene creato un processo separato per runbook figlio hello. |
| Esecuzione |Il runbook padre attende hello figlio runbook toocomplete prima di continuare. |Il runbook padre continua subito dopo l'avvio del runbook figlio *o* runbook padre attende hello figlio processo toofinish. |
| Output |Il runbook padre può ottenere output direttamente dal runbook figlio. |Il runbook padre deve recuperare l'output dal processo del runbook figlio *o* può ottenere direttamente l'output dal runbook figlio. |
| parameters |I valori per parametri del runbook figlio hello vengono specificati separatamente e possono utilizzare qualsiasi tipo di dati. |I valori per il runbook figlio hello parametri devono essere combinati in una singola tabella hash e possono includere solo semplice, matrice e oggetto JSON che sfruttano la serializzazione di tipi di dati. |
| Account di automazione |Il runbook padre può usare solo runbook figlio hello stesso account di automazione. |Il runbook padre può usare runbook figlio da qualsiasi account di automazione da hello stessa sottoscrizione di Azure e anche una sottoscrizione diversa se si dispone di un tooit di connessione. |
| Pubblicazione |Il runbook figlio deve essere pubblicato prima della pubblicazione del runbook padre. |Il runbook figlio deve essere pubblicato prima che il runbook padre venga avviato. |

## <a name="next-steps"></a>Passaggi successivi
* [Avvio di un runbook in Automazione di Azure](automation-starting-a-runbook.md)
* [Output di runbook e messaggi in automazione di Azure](automation-runbook-output-and-messages.md)

