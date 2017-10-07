---
title: aaaRunbook Output e i messaggi in automazione di Azure | Documenti Microsoft
description: Viene descritto come errore e output toocreate e recuperare i messaggi generati dal runbook in automazione di Azure.
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 13a414f5-0e2c-4be2-9558-a3e3ec84b6b2
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/11/2016
ms.author: magoedte;bwren
ms.openlocfilehash: c1505fa889473766bfa47e43aaed2449d60ad851
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="runbook-output-and-messages-in-azure-automation"></a>Output di runbook e messaggi in automazione di Azure
La maggior parte dei runbook di automazione di Azure conterrà un tipo di output, ad esempio un utente toohello messaggio di errore o un oggetto complesso toobe utilizzato da un altro flusso di lavoro. Windows PowerShell fornisce [più flussi](http://blogs.technet.com/heyscriptingguy/archive/2014/03/30/understanding-streams-redirection-and-write-host-in-powershell.aspx) toosend output da uno script o un flusso di lavoro. Automazione di Azure gestisce ognuno di questi flussi in modo diverso, ed è necessario seguire le procedure consigliate per informazioni su come toouse ogni durante la creazione di un runbook.

Hello nella tabella seguente fornisce una breve descrizione di ognuno dei flussi di hello e relativo comportamento nel portale di gestione Azure hello sia durante l'esecuzione di un runbook pubblicato che per [test di un runbook](automation-testing-runbook.md). Nelle sezioni successive vengono forniti ulteriori dettagli su ogni flusso.

| Flusso | Descrizione | Pubblicato | Test |
|:--- |:--- |:--- |:--- |
| Output |Oggetti destinato toobe usati da altri runbook. |Cronologia processo toohello scritta. |Visualizzato nel riquadro di Output Test hello. |
| Avviso |Messaggio di avviso per l'utente hello. |Cronologia processo toohello scritta. |Visualizzato nel riquadro di Output Test hello. |
| Errore |Messaggio di errore per utente hello. A differenza di un'eccezione, hello runbook continua dopo un messaggio di errore per impostazione predefinita. |Cronologia processo toohello scritta. |Visualizzato nel riquadro di Output Test hello. |
| Dettagliato |Messaggi che forniscono informazioni generali o di debug. |Scritto toojob cronologia solo se è attivata la registrazione dettagliata per il runbook hello. |Viene visualizzata nel riquadro di Output del Test hello solo se $VerbosePreference è impostato tooContinue hello runbook. |
| Avanzamento |Record generati automaticamente prima e dopo ogni attività nel runbook hello. Hello runbook non deve provare toocreate i propri record di stato poiché è destinato a un utente interattivo. |Scritto toojob cronologia solo se è attivata la registrazione di stato di avanzamento per hello runbook. |Non è visualizzato nel riquadro di Output Test hello. |
| Debug |Messaggi destinati a un utente interattivo. Non devono essere utilizzati nei runbook. |Non viene scritto toojob cronologia. |Non viene scritto tooTest riquadro di Output. |

## <a name="output-stream"></a>Flusso di output
flusso di Output di Hello è destinato all'output degli oggetti creati da uno script o un flusso di lavoro quando viene eseguito correttamente. In automazione di Azure, il flusso viene usato principalmente per gli oggetti toobe utilizzati da [runbook padre che chiamano runbook corrente hello](automation-child-runbooks.md). Quando si [chiamare un runbook inline](automation-child-runbooks.md#invoking-a-child-runbook-using-inline-execution) da un runbook padre, vengono restituiti i dati dall'elemento padre toohello flusso di output hello. Utilizzare utente toohello indietro di hello output flusso toocommunicate informazioni generali solo se si conosce hello runbook non verrà mai chiamato da un altro runbook. Come procedura consigliata, tuttavia, è consigliabile usare hello [flusso dettagliato](#Verbose) utente toohello di toocommunicate informazioni generali.

È possibile scrivere dati toohello output flusso tramite [Write-Output](http://technet.microsoft.com/library/hh849921.aspx) o specificando l'oggetto hello su una riga nel runbook hello.

    #hello following lines both write an object toohello output stream.
    Write-Output –InputObject $object
    $object

### <a name="output-from-a-function"></a>Output da una funzione
Quando si scrive nel flusso di output toohello in una funzione inclusa nel runbook, output di hello viene passato runbook toohello indietro. Se runbook hello assegna tale variabile tooa output, quindi non verrà più scritto nel flusso di output toohello. La scrittura di altri flussi funzione hello tooany scriverà toohello flusso corrispondente hello runbook.

Prendere in considerazione hello seguente runbook di esempio.

    Workflow Test-Runbook
    {
        Write-Verbose "Verbose outside of function" -Verbose
        Write-Output "Output outside of function"
        $functionOutput = Test-Function
        $functionOutput

    Function Test-Function
     {
        Write-Verbose "Verbose inside of function" -Verbose
        Write-Output "Output inside of function"
      }
    }


flusso di output di Hello del processo del runbook hello sarebbe:

    Output inside of function
    Output outside of function

Hello flusso dettagliato del processo di hello runbook sarà:

    Verbose outside of function
    Verbose inside of function

Dopo aver pubblicato il runbook hello e prima di avviare, è anche necessario attivare la registrazione nelle impostazioni runbook hello hello tooget ordine output flusso dettagliato dettagliata.

### <a name="declaring-output-data-type"></a>Dichiarazione del tipo di dati di output
Un flusso di lavoro è possibile specificare il tipo di dati hello del relativo output mediante hello [attributo OutputType](http://technet.microsoft.com/library/hh847785.aspx). Questo attributo non ha effetto in fase di esecuzione, ma fornisce un autore di indicazione toohello runbook in fase di progettazione di output di hello previsto del runbook hello. Come set di strumenti di hello per runbook continua tooevolve, importante hello dichiarare tipi di dati di output in fase di progettazione aumenta l'importanza. Di conseguenza, è una procedura consigliata tooinclude questa dichiarazione in tutti i runbook creati.

Di seguito è riportato un elenco di tipi di output di esempio:

* System.String
* System.Int32
* System.Collections.Hashtable
* Microsoft.Azure.Commands.Compute.Models.PSVirtualMachine

Hello runbook di esempio seguente restituisce un oggetto stringa e include una dichiarazione del relativo tipo di output. Se il runbook restituisce una matrice di un determinato tipo, è comunque necessario specificare il tipo di hello come matrice di tooan anziché di tipo hello.

    Workflow Test-Runbook
    {
       [OutputType([string])]

       $output = "This is some string output."
       Write-Output $output
    }

toodeclare un output di tipo nei runbook Grapical o grafica del flusso di lavoro di PowerShell, è possibile selezionare hello **di Input e Output** opzione di menu e digitare il nome di hello di hello tipo di output.  Si consiglia di usare toomake nome classe hello completo .NET è facilmente identificabile quando farvi riferimento da un runbook padre.  Questo espone tutte le proprietà di hello del bus di dati toohello tale classe runbook hello e fornisce una notevole flessibilità quando vengono utilizzate per la logica condizionale, registrazione e di riferimento come valori di altre attività nel runbook hello.<br> ![Opzione Input e output del runbook](media/automation-runbook-output-and-messages/runbook-menu-input-and-output-option.png)

Nell'esempio seguente di hello, sono disponibili due runbook grafici toodemonstrate questa funzionalità.  Se si applica il modello di progettazione di hello runbook modulari, abbiamo un runbook che funge da hello *modello autenticazione Runbook* Gestione autenticazione con Azure hello account RunAs.  In questo caso il secondo runbook, che normalmente eseguirebbe hello core logica tooautomate uno scenario specifico, verrà hello tooexecute *modello autenticazione Runbook* e visualizzare hello risultati tooyour **Test** riquadro di output.  In circostanze normali, si sarebbe necessario eseguire un'operazione su un output di hello sfruttando risorsa dal runbook figlio hello questo runbook.    

Ecco la logica di base di hello hello **AuthenticateTo Azure** runbook.<br> ![Esempio di modello di runbook di autenticazione](media/automation-runbook-output-and-messages/runbook-authentication-template.png).  

Include il tipo di output di hello *Microsoft.Azure.Commands.Profile.Models.PSAzureContext*, che restituisce le proprietà del profilo di autenticazione hello.<br> ![Esempio di tipo di output del runbook](media/automation-runbook-output-and-messages/runbook-input-and-output-add-blade.png) 

Mentre il runbook è molto semplice, sussiste una toocall di elemento di configurazione informazioni qui.  ultima attività Hello è in esecuzione hello **Write-Output** cmdlet e le scritture hello variabile profilo dati tooa $_ usando un'espressione PowerShell per hello **Inputobject** parametro, è necessario per tale cmdlet.  

Per i runbook di secondo hello in questo esempio, denominato *Test ChildOutputType*, abbiamo semplicemente due attività.<br> ![Esempio di runbook di tipo di output figlio](media/automation-runbook-output-and-messages/runbook-display-authentication-results-example.png) 

prima attività Hello chiama hello **AuthenticateTo Azure** runbook e hello seconda attività è in esecuzione hello **Write-Verbose** cmdlet con hello **origine dati** di  **Output attività** e il valore hello **percorso campo** è **Context.Subscription.SubscriptionName**, che è specifica di output di hello contesto da hello  **AuthenticateTo Azure** runbook.<br> ![Origine dati per il cmdlet Write-Verbose](media/automation-runbook-output-and-messages/runbook-write-verbose-parameters-config.png)    

output di Hello risultante è il nome di hello di sottoscrizione hello.<br> ![Risultati del runbook Test-ChildOutputType](media/automation-runbook-output-and-messages/runbook-test-childoutputtype-results.png)

Una nota sul comportamento di hello di hello controllo tipo di Output.  Quando si digita un valore nel campo di tipo di Output di hello in hello Input e un pannello Proprietà di Output, è necessario tooclick di fuori controllo hello dopo aver digitato, affinché il toobe voce riconosciuto dal controllo hello.  

## <a name="message-streams"></a>Flussi di messaggi
A differenza di flusso di output di hello, flussi di messaggi sono previsti toocommunicate informazioni toohello utente. Sono presenti più flussi di messaggi per diversi tipi di informazioni e ciascuno viene gestito diversamente dall'automazione di Azure.

### <a name="warning-and-error-streams"></a>Flussi di avviso ed errore
i flussi di errore e avviso di Hello sono previsti toolog problemi che si verificano in un runbook. Cronologia processo toohello vengono scritti quando viene eseguito un runbook e vengono inclusi nel riquadro di Output Test Ciao hello portale di gestione di Azure quando viene testato un runbook. Per impostazione predefinita, hello runbook continuerà l'esecuzione dopo un avviso o errore. È possibile specificare tale runbook hello deve essere sospeso in un avviso o errore impostando una [variabile di preferenza](#PreferenceVariables) hello runbook prima di creare il messaggio hello. Ad esempio, toocause toosuspend un runbook in caso di errore come se si trattasse di un'eccezione, imposta **$ErrorActionPreference** tooStop.

Creare un messaggio di avviso o errore tramite hello [Write-Warning](https://technet.microsoft.com/library/hh849931.aspx) o [Write-Error](http://technet.microsoft.com/library/hh849962.aspx) cmdlet. Le attività possono anche scrivere flussi toothese.

    #hello following lines create a warning message and then an error message that will suspend hello runbook.

    $ErrorActionPreference = "Stop"
    Write-Warning –Message "This is a warning message."
    Write-Error –Message "This is an error message that will stop hello runbook because of hello preference variable."

### <a name="verbose-stream"></a>Flusso dettagliato
flusso di messaggi dettagliati Hello è per informazioni generali sull'operazione di runbook hello. Poiché hello [flusso di Debug](#Debug) non è disponibile in un runbook, i messaggi dettagliati devono essere usati per le informazioni di debug. Per impostazione predefinita, i messaggi dettagliati dei runbook pubblicati non verranno essere archiviati nella cronologia processo hello. Nella scheda Configura hello di hello runbook nel portale di gestione Azure hello, toostore i messaggi dettagliati, configurare i runbook pubblicati tooLog record dettagliati. Nella maggior parte dei casi, è consigliabile mantenere l'impostazione di valore predefinito di hello di non registrare i record dettagliati per un runbook per motivi di prestazioni. Attivare questa tootroubleshoot solo opzione o eseguire il debug di un runbook.

Quando [test di un runbook](automation-testing-runbook.md), i messaggi dettagliati non vengono visualizzati anche se hello runbook è configurato toolog i record dettagliati. i messaggi dettagliati durante toodisplay [test di un runbook](automation-testing-runbook.md), è necessario impostare tooContinue variabile hello $VerbosePreference. Con l'impostazione di tale variabile, i messaggi dettagliati verranno visualizzati nel riquadro di Output di hello Azure portal Test hello.

Creare un messaggio dettagliato con hello [Write-Verbose](http://technet.microsoft.com/library/hh849951.aspx) cmdlet.

    #hello following line creates a verbose message.

    Write-Verbose –Message "This is a verbose message."

### <a name="debug-stream"></a>Flusso di Debug 
flusso di Debug di Hello è destinata all'utilizzo con un utente interattivo e non deve essere usato nei runbook.

## <a name="progress-records"></a>Record di stato
Se si configura un corso toolog runbook Registra (nella scheda Configura di hello di hello runbook nel portale di Azure hello), quindi un record verrà scritto Cronologia processo toohello prima e dopo l'esecuzione di ogni attività. Nella maggior parte dei casi, è consigliabile mantenere l'impostazione di valore predefinito di hello di non registrare record di stato per un runbook prestazioni toomaximize ordine. Attivare questa tootroubleshoot solo opzione o eseguire il debug di un runbook. Quando si testa un runbook, è possibile che i messaggi di stato non vengono visualizzati anche se hello runbook è configurato toolog record di stato.

Hello [Write-Progress](http://technet.microsoft.com/library/hh849902.aspx) cmdlet non è valido in un runbook, poiché viene usato per l'utilizzo con un utente interattivo.

## <a name="preference-variables"></a>Variabili di preferenza
Windows PowerShell Usa [variabili di preferenza](http://technet.microsoft.com/library/hh847796.aspx) toodetermine come toorespond toodata inviato toodifferent flussi di output. È possibile impostare queste variabili in un runbook toocontrol la modalità di risposta toodata inviati ai diversi flussi.

Hello nella tabella seguente elenca le variabili di preferenza hello che possono essere usate nei runbook con i relativi validi e valori predefiniti. Si noti che questa tabella include solo i valori hello validi in un runbook. Altri valori sono validi per le variabili di preferenza hello quando utilizzato in Windows PowerShell all'esterno di automazione di Azure.

| Variabile | Valore predefinito | Valori validi |
|:--- |:--- |:--- |
| WarningPreference |Continue |Stop<br>Continue<br>SilentlyContinue |
| ErrorActionPreference |Continue |Stop<br>Continue<br>SilentlyContinue |
| VerbosePreference |SilentlyContinue |Stop<br>Continue<br>SilentlyContinue |

Hello nella tabella seguente elenca il comportamento di hello per hello preferenza variabile i valori validi nei runbook.

| Valore | Comportamento |
|:--- |:--- |
| Continue |Registra il messaggio hello e continua l'esecuzione di runbook hello. |
| SilentlyContinue |Continua l'esecuzione di hello runbook senza registrare il messaggio hello. In questo modo hello ignora il messaggio hello. |
| Arresto |Registra il messaggio hello e sospende il runbook hello. |

## <a name="retrieving-runbook-output-and-messages"></a>Recupero di messaggi e output di runbook
### <a name="azure-portal"></a>Portale di Azure
È possibile visualizzare i dettagli di hello di un processo del runbook nel portale di Azure dalla scheda processi hello di un runbook hello. Riepilogo del processo di hello Hello visualizzerà i parametri di input hello e hello [flusso di Output](#Output) aggiunta toogeneral informazioni processo hello ed eventuali eccezioni, se si sono verificate. Hello cronologia includerà i messaggi di hello [flusso di Output](#Output) e [Warning and Error Streams](#WarningError) in aggiunta toohello [flusso dettagliato](#Verbose) e [lo stato di avanzamento Record](#Progress) se hello runbook è configurato toolog dettagliato e record di stato.

### <a name="windows-powershell"></a>Windows PowerShell
In Windows PowerShell, è possibile recuperare i messaggi e output da un runbook con hello [Get-AzureAutomationJobOutput](https://msdn.microsoft.com/library/mt603476.aspx) cmdlet. Questo cmdlet richiede l'ID del processo di hello hello e contiene un parametro denominato flusso in cui si specifica quale tooreturn di flusso. È possibile specificare qualsiasi tooreturn tutti i flussi per il processo di hello.

Hello di esempio seguente avvia un runbook di esempio e quindi attende toocomplete. Al termine, il flusso di output viene raccolto dal processo hello.

    $job = Start-AzureRmAutomationRunbook -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name "Test-Runbook"

    $doLoop = $true
    While ($doLoop) {
       $job = Get-AzureRmAutomationJob -ResourceGroupName "ResourceGroup01" `
       –AutomationAccountName "MyAutomationAccount" -Id $job.JobId
       $status = $job.Status
       $doLoop = (($status -ne "Completed") -and ($status -ne "Failed") -and ($status -ne "Suspended") -and ($status -ne "Stopped")
    }

    Get-AzureRmAutomationJobOutput -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName "MyAutomationAccount" -Id $job.JobId –Stream Output

### <a name="graphical-authoring"></a>Creazione grafica
Per i runbook grafici, la registrazione aggiuntiva è disponibile sotto forma di hello di analisi a livello di attività.  Sono disponibili due livelli di traccia: base e dettagliato.  Traccia di base, è possibile vedere hello avvio e ora di fine di ogni attività nel runbook hello più informazioni correlate tooany tentativi di attività, ad esempio numero di tentativi e l'ora di inizio dell'attività hello.  Nella traccia dettagliata sono indicate le informazioni della traccia di base e i dati di input e output di ogni attività.  Si noti che attualmente i record di traccia hello vengono scritti utilizzando flusso dettagliato hello, pertanto è necessario abilitare la registrazione dettagliata quando si abilita la traccia.  Per i runbook grafici con traccia attivata non è necessario toolog record di stato, in quanto funge da base traccia hello hello allo stesso scopo e risulta più informativi.

![Visualizzazione dei flussi dei processi di creazione grafica](media/automation-runbook-output-and-messages/job-streams-view-blade.png)

È possibile visualizzare da hello sopra schermata quando si abilita dettagliato di registrazione e analisi per i runbook grafici, molte più informazioni sono disponibile nell'ambiente di produzione hello che visualizzare flussi di lavoro.  Queste informazioni aggiuntive possono essere essenziali per la risoluzione dei problemi di produzione di un runbook e pertanto è consigliabile attivarle solo a tale scopo e non come regola generale.    
record di traccia Hello può essere particolarmente numerosi.  Con runbook grafico traccia è possibile ottenere due toofour record per ogni attività a seconda che sia stato configurato l'analisi di base o dettagliato.  A meno che non è necessario lo stato di avanzamento hello tootrack informazioni di un runbook per la risoluzione dei problemi, è possibile tookeep che la traccia è disattivata.

**tooenable attività a livello di traccia, eseguire hello alla procedura seguente.**

1. Nel portale di Azure hello, aprire l'account di automazione.
2. Fare clic su hello **runbook** riquadro tooopen hello elenco di runbook.
3. Nel Pannello di hello runbook, fare clic su tooselect un runbook grafico dall'elenco dei runbook.
4. Nel pannello delle impostazioni hello per runbook hello selezionato, fare clic su **registrazione e analisi**.
5. In hello Logging and Tracing pannello, Registra record dettagliati, fare clic su **su** tooenable la registrazione dettagliata e la traccia udner a livello di attività, modificare il livello di traccia hello troppo**base** o **Detailed**  in base a livello di hello di traccia è necessario.<br>
   
   ![Pannello Registrazione e traccia della creazione grafica](media/automation-runbook-output-and-messages/logging-and-tracing-settings-blade.png)

### <a name="microsoft-operations-management-suite-oms-log-analytics"></a>Log Analytics di Microsoft Operations Management Suite (OMS)
Automazione può inviare runbook processo lo stato e processo flussi tooyour Analitica di Log di Microsoft Operations Management Suite (OMS) dell'area di lavoro.  Con Log Analytics è possibile:

* Ottenere informazioni dettagliate sui processi di Automazione. 
* Attivare un messaggio di posta elettronica o un avviso in base allo stato del processo del runbook, ad esempio non riuscito o sospeso. 
* Scrivere query avanzate nei flussi del processo. 
* Correlare i processi tra account di Automazione. 
* Visualizzare la cronologia dei processi nel tempo.    

Per ulteriori informazioni sulla modalità di integrazione tooconfigure con toocollect Log Analitica, correlare e agire sui dati di processo, vedere [inoltra lo stato del processo e i flussi di lavoro da automazione tooLog Analitica (OMS)](automation-manage-send-joblogs-log-analytics.md).

## <a name="next-steps"></a>Passaggi successivi
* ulteriori sull'esecuzione di runbook, come i processi del runbook toomonitor e altri dettagli tecnici, vedere toolearn [tenere traccia di un processo del runbook](automation-runbook-execution.md)
* toounderstand toodesign e utilizzare i runbook figlio, vedere [figlio runbook in automazione di Azure](automation-child-runbooks.md)

