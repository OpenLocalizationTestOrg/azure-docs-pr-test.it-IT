---
title: aaaGraphical creazione in automazione di Azure | Documenti Microsoft
description: Creazione con interfaccia grafica consente toocreate runbook per l'automazione di Azure senza l'utilizzo del codice. Questo articolo fornisce un'introduzione di toographical creazione e tutti i dettagli di hello necessarie toostart la creazione di un runbook grafico.
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 4b6f840c-e941-4293-a728-b33407317943
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/14/2017
ms.author: magoedte;bwren
ms.openlocfilehash: 6ddf18b992d5e5f7f4af95f344007a63ac498549
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="graphical-authoring-in-azure-automation"></a>Creazione grafica in Automazione di Azure
## <a name="introduction"></a>Introduzione
Creazione e modifica con interfaccia grafica consente toocreate runbook per l'automazione di Azure senza la complessità hello del codice di Windows PowerShell o flusso di lavoro PowerShell sottostante hello. Aggiungere attività toohello area di disegno da una libreria di cmdlet e i runbook, collegarli tra loro e configurare tooform un flusso di lavoro.  Se si è mai utilizzato con System Center Orchestrator o Service Management Automation (SMA), questo dovrebbe essere familiare tooyou.   

Questo articolo fornisce un'introduzione toographical creazione e hello concetti che è necessario tooget avviato per la creazione di un runbook grafico.

## <a name="graphical-runbooks"></a>Runbook grafici
Tutti i Runbook in Automazione di Azure sono flussi di lavoro di Windows PowerShell.  I runbook grafici e con interfaccia grafica del flusso di lavoro PowerShell generano un codice di PowerShell che viene eseguito dal thread di lavoro automazione hello, ma non è in grado di tooview, o modificarlo direttamente.  Un runbook grafico può essere convertito tooa grafica del flusso di lavoro PowerShell runbook e viceversa, ma non possono essere convertiti tooa testuale runbook. Impossibile importare un runbook esistente testuale in editor grafico hello.  

## <a name="overview-of-graphical-editor"></a>Panoramica dell'editor grafico
È possibile aprire l'editor grafico hello nel portale di Azure hello creando o modificando un runbook grafico.

![Area di lavoro grafica](media/automation-graphical-authoring-intro/runbook-graphical-editor.png)

Hello nelle sezioni seguenti vengono descritti i controlli di hello in editor grafico hello.

### <a name="canvas"></a>Canvas
area di disegno Hello è consente di definire il runbook.  Aggiungere le attività da nodi hello hello libreria controllo toohello runbook e connetterle con la logica di hello toodefine di collegamenti di hello runbook.

È possibile utilizzare i controlli di hello nella parte inferiore di hello del toozoom canvas hello.

![Area di lavoro grafica](media/automation-graphical-authoring-intro/runbook-canvas-controls.png)

### <a name="library-control"></a>Controllo Library
controllo della raccolta Hello in è possibile selezionare [attività](#activities) tooadd tooyour runbook.  È necessario aggiungerli toohello area di disegno in cui si connette tooother attività.  Include quattro sezioni descritte nella seguente tabella hello.

| Sezione | Descrizione |
|:--- |:--- |
| Cmdlet |Include tutti i cmdlet di hello che possono essere usati nel runbook.  I cmdlet sono organizzati per modulo.  Tutti i moduli di hello installati nell'account di automazione sarà disponibili. |
| Runbook |Include hello runbook nell'account di automazione. È possibile aggiungere questi runbook toohello canvas toobe usato come runbook figlio. Vengono visualizzati solo i runbook di hello stesso tipo di base come hello runbook in corso di modifica; per grafici runbook basati su PowerShell solo i runbook vengono visualizzati, mentre per i runbook con interfaccia grafica del flusso di lavoro di PowerShell sono visualizzati solo flusso di lavoro-basata su PowerShell runbook. |
| Asset |Include hello [asset di automazione](http://msdn.microsoft.com/library/dn939988.aspx) nell'account di automazione che può essere usato nel runbook.  Quando si aggiunge un runbook tooa asset, aggiungerà un'attività flusso di lavoro che ottiene la risorsa selezionata hello.  In caso di hello degli asset variabili, è possibile selezionare se tooadd tooget un'attività hello variabile hello variabile o è impostata. |
| Runbook Control |Include attività di controllo di Runbook che è possibile usare nel Runbook corrente. Oggetto *giunzione* accetta più input e attende fino a quando non sia stata completata prima del flusso di lavoro hello continua. Oggetto *codice* uno o più righe di codice di PowerShell o del flusso di lavoro di PowerShell in base al tipo runbook grafico hello viene eseguita l'attività.  È possibile utilizzare questa attività per il codice personalizzato o per la funzionalità che è difficile tooachieve con altre attività. |

### <a name="configuration-control"></a>Controllo Configuration
Hello controllo della configurazione è possibile fornire i dettagli per un oggetto selezionato nell'area di disegno hello. proprietà Hello disponibili in questo controllo dipenderanno dal tipo di hello dell'oggetto selezionato.  Quando si seleziona un'opzione nel controllo della configurazione di hello, si aprirà pannelli aggiuntivi informazioni aggiuntive tooprovide di ordine.

### <a name="test-control"></a>Controllo Test
Hello il controllo di Test non viene visualizzata quando l'editor grafico hello è iniziato. Viene aperto quando si [testa un Runbook grafico](#graphical-runbook-procedures)in modo interattivo.  

## <a name="graphical-runbook-procedures"></a>Procedure relative a Runbook grafici
### <a name="exporting-and-importing-a-graphical-runbook"></a>Esportazione e importazione di un runbook con interfaccia grafica
È possibile esportare solo hello versione pubblicata di un runbook grafico.  Se non è ancora stato pubblicato il runbook hello, hello **esportazione pubblicati** pulsante sarà disabilitato.  Quando si fa clic su hello **esportazione pubblicati** pulsante, runbook hello è computer locale tooyour scaricato.  Hello nome del file hello hello di corrisponde runbook hello con un *graphrunbook* estensione.

![esportazione pubblicato](media/automation-graphical-authoring-intro/runbook-export.png)

È possibile importare un file di runbook grafico o grafica del flusso di lavoro PowerShell selezionando hello **importare** opzione durante l'aggiunta di un runbook.   Quando si seleziona tooimport file hello, è possibile mantenere hello stesso **nome** o fornire uno nuovo.  il campo tipo di Runbook Hello verrà visualizzato il tipo di hello di runbook dopo valuta file hello selezionato e se si tenta di tooselect un tipo diverso che non è corretto, che verrà visualizzato un messaggio indicando esistono potenziali conflitti e durante la conversione, è possibile errori di sintassi.  

![Importare runbook](media/automation-graphical-authoring-intro/runbook-import-revised20165.png)

### <a name="testing-a-graphical-runbook"></a>Test di un Runbook grafico
È possibile testare versione di hello bozza di un runbook nel portale di Azure hello mentre lasciando hello versione pubblicata della runbook hello invariata oppure è possibile testare un nuovo runbook prima che è stata pubblicata. In questo modo si tooverify che hello runbook funzioni correttamente prima di sostituire la versione pubblicata di hello. Quando si testa un runbook, runbook bozza hello viene eseguito e vengono completate tutte le azioni eseguite. Viene creata alcuna cronologia processo, ma l'output viene visualizzato nel riquadro di Output Test hello. 

Aprire il controllo di Test per un runbook hello aprendo hello runbook per la modifica e quindi fare clic su hello **riquadro Test** pulsante.

![Pulsante Test pane](media/automation-graphical-authoring-intro/runbook-edit-test-pane.png)

il controllo di Test Hello richiederà per qualsiasi parametro di input, è possibile avviare il runbook hello facendo clic su hello **avviare** pulsante.

![Pulsanti del controllo Test](media/automation-graphical-authoring-intro/runbook-test-start.png)

### <a name="publishing-a-graphical-runbook"></a>Pubblicazione di un Runbook grafico
Ogni Runbook in Automazione di Azure include una versione bozza e una versione pubblicata. Solo versione di hello pubblicato è disponibile toobe eseguire e può essere modificata solo la versione bozza hello. versione di Hello pubblicato è influenzata da una qualsiasi versione bozza toohello di modifiche. Versione bozza hello è pronto toobe disponibili, è pubblicarla, sovrascrivendo così versione di hello pubblicato con la versione bozza hello.

È possibile pubblicare un runbook grafico aprendo hello runbook per la modifica e quindi fare clic sul hello **pubblica** pulsante.

![Pulsante Publish](media/automation-graphical-authoring-intro/runbook-edit-publish.png)

Un Runbook non ancora pubblicato è con stato **New**.  Quando viene pubblicato, lo stato cambia in **Published**.  Se si modifica runbook hello dopo che è stata pubblicata e le versioni, bozza e pubblicato hello sono diverse, hello runbook lo stato di **In modalità di modifica**.

![Stati del Runbook](media/automation-graphical-authoring-intro/runbook-statuses-revised20165.png) 

È inoltre versione hello opzione toorevert toohello pubblicata di un runbook.  In questo modo viene immediatamente tutte le modifiche apportate dall'hello runbook ultima pubblicazione e sostituisce versione di hello bozza di runbook hello con versione di hello pubblicato.

![Ripristinare toopublished pulsante](media/automation-graphical-authoring-intro/runbook-edit-revert-published.png)

## <a name="activities"></a>attività
Le attività sono blocchi predefiniti di hello di un runbook.  Un'attività può essere un cmdlet di PowerShell, un Runbook figlio o un'attività flusso di lavoro.  Si aggiunge un runbook di toohello attività facendo clic destro nel controllo della raccolta hello e selezionando **aggiungere toocanvas**.  È quindi possibile fare clic e trascinare tooplace attività hello in qualsiasi punto sul hello area di disegno che si desidera.  Hello percorso di hello dell'attività hello nell'area di disegno hello non influirà hello funzionamento dei runbook hello in alcun modo.  È possibile layout runbook tuttavia si ritiene più adatto toovisualize l'operazione. 

![Aggiungere toocanvas](media/automation-graphical-authoring-intro/add-to-canvas-revised20165.png)

Selezionare le proprietà e i parametri attività hello hello canvas tooconfigure nel Pannello di configurazione hello.  È possibile modificare hello **etichetta** di hello toosomething di attività che è tooyou descrittivo.  cmdlet originale Hello è ancora in esecuzione e si modifica semplicemente il nome visualizzato che verrà utilizzato nell'editor grafico hello.  Hello etichetta deve essere univoco all'interno di hello runbook. 

### <a name="parameter-sets"></a>Set di parametri
Un set di parametri definisce i parametri obbligatori e facoltativi hello che accettano i valori per un particolare cmdlet.  Tutti i cmdlet dispongono di almeno un set di parametri, altri dispongono di più set di parametri.  Se un cmdlet dispone di più set di parametri, sarà necessario selezionare quello da usare prima di configurare i parametri.  parametri Hello che è possibile configurare dipenderà dal set di parametri hello prescelto.  È possibile modificare il set di parametri hello utilizzato da un'attività selezionando **parametro impostato** e selezionando un altro set.  In questo caso, i valori dei parametri configurati vengono persi.

Nell'esempio seguente di hello, il cmdlet Get-AzureRmVM hello ha tre set di parametri.  I valori dei parametri non è possibile configurare fino a quando non si seleziona uno dei set di parametri hello.  Hello ListVirtualMachineInResourceGroupParamSet set di parametri per la restituzione di tutte le macchine virtuali in un gruppo di risorse con un singolo parametro facoltativo.  Hello GetVirtualMachineInResourceGroupParamSet consente di specificare hello e della macchina virtuale si desidera tooreturn ha due obbligatorio e un parametro facoltativo.

![Parameter Set](media/automation-graphical-authoring-intro/get-azurermvm-parameter-sets.png)

#### <a name="parameter-values"></a>Valori dei parametri
Quando si specifica un valore per un parametro, si seleziona un toodetermine di origine dati come valore hello verrà specificato.  origini dei dati disponibili per un determinato parametro Hello dipenderà i valori validi per il parametro hello.  Null ad esempio non sarà disponibile come opzione di un parametro che non consente valori Null.

| Origine dati | Descrizione |
|:--- |:--- |
| Constant Value |Digitare un valore per il parametro hello.  Questo è disponibile solo per i seguenti tipi di dati hello: Int32, Int64, String, Boolean, DateTime, commutatore. |
| Activity Output |Output di un'attività che precede l'attività corrente hello nel flusso di lavoro hello.  Verranno elencate tutte le attività valide.  Selezionare solo hello attività toouse l'output per il valore di parametro hello.  Se l'attività hello restituisce un oggetto con più proprietà, è possibile digitare nella casella Nome hello della proprietà hello dopo aver selezionato l'attività hello. |
| Input di runbook |Selezionare un parametro di input del runbook come parametro di input toohello attività. |
| Asset della variabile |Selezionare una variabile di Automazione come input. |
| Asset di credenziali |Selezionare una credenziale di Automazione come input. |
| Asset del certificato |Selezionare un certificato di Automazione come input. |
| Asset di connessione |Selezionare una connessione di Automazione come input. |
| PowerShell Expression |Specificare un' [espressione di PowerShell](#powershell-expressions)semplice.  Hello espressione verrà valutata prima di hello attività e hello risultati utilizzati per il valore di parametro hello.  È possibile utilizzare l'output di toohello toorefer le variabili di un'attività o un parametro di input del runbook. |
| Non configurato |Cancella qualsiasi valore precedentemente configurato. |

#### <a name="optional-additional-parameters"></a>Parametri aggiuntivi facoltativi
Tutti i cmdlet avrà parametri aggiuntivi di hello opzione tooprovide.  Si tratta di parametri comuni di PowerShell o di altri parametri personalizzati.  Viene visualizzata una casella di testo in cui è possibile specificare parametri usando la sintassi di PowerShell.  Ad esempio, toouse hello **Verbose** parametro comune, è possibile specificare **"-Verbose: $True"**.

### <a name="retry-activity"></a>Ripetere l'attività
**Ripetere il comportamento** consente un toobe attività eseguire più volte fino a quando non viene soddisfatta una determinata condizione, in modo analogo a un ciclo.  È possibile utilizzare questa funzionalità per le attività che deve essere eseguito più volte, sono soggetta a errori e possono essere necessario più di un tentativo per il successo o informazioni sull'output di hello dell'attività hello per ottenere dati validi dei test.    

Quando si abilita la ripetizione dei tentativi per un'attività, è possibile impostare un ritardo e una condizione.  ritardo Hello è hello tempo (in secondi o minuti) runbook hello attenderà prima di eseguire attività hello nuovamente.  Se non viene specificato alcun ritardo, quindi hello attività verrà eseguita nuovamente immediatamente dopo essere stato completato. 

![Ritardo di ripetizione dei tentativi di attività](media/automation-graphical-authoring-intro/retry-delay.png)

condizione di tentativi di Hello è un'espressione di PowerShell che viene valutata dopo ogni attività hello in fase di esecuzione.  Se l'espressione hello risolve tooTrue, attività hello viene eseguito nuovamente.  Se l'espressione hello risolve tooFalse quindi hello attività non viene eseguito nuovamente e runbook hello Sposta attività successiva toohello. 

![Ritardo di ripetizione dei tentativi di attività](media/automation-graphical-authoring-intro/retry-condition.png)

condizione di tentativi di Hello è possibile utilizzare una variabile denominata $RetryData che fornisce accesso tooinformation sui tentativi attività hello.  Questa variabile non ha proprietà hello in hello nella tabella seguente.

| Proprietà | Descrizione |
|:--- |:--- |
| NumberOfAttempts |Numero di volte in cui è stata eseguita l'attività hello. |
| Output |Output di hello dell'ultima esecuzione dell'attività hello. |
| TotalDuration |Tempo trascorso dall'inizio attività hello hello prima volta. |
| StartedAt |Tempo in attività di hello formato UTC prima di tutto è stato avviato. |

Di seguito sono riportati alcuni esempi di condizioni per la ripetizione dei tentativi dell'attività.

    # Run hello activity exactly 10 times.
    $RetryData.NumberOfAttempts -ge 10 

    # Run hello activity repeatedly until it produces any output.
    $RetryData.Output.Count -ge 1 

    # Run hello activity repeatedly until 2 minutes has elapsed. 
    $RetryData.TotalDuration.TotalMinutes -ge 2

Dopo aver configurato una condizione di ripetizione per un'attività, attività hello include due segnali visivi tooremind è.  Uno viene presentato nell'attività hello e altri hello è quando si verifica configurazione hello dell'attività hello.

![Segnali visivi di ripetizione dei tentativi di attività](media/automation-graphical-authoring-intro/runbook-activity-retry-visual-cue.png)

### <a name="workflow-script-control"></a>Controllo Workflow Script
Un controllo del codice è un'attività speciale che accetta uno script di PowerShell o del flusso di lavoro di PowerShell in base al tipo hello di runbook con interfaccia grafica viene creato in tooprovide funzionalità che potrebbero altrimenti non disponibili.  Non può accettare parametri, ma può usare le variabili per parametri di output di attività e di input di Runbook.  Viene aggiunto alcun output dell'attività hello toohello databus a meno che non dispone di alcun collegamento in uscita nel quale caso viene aggiunto toohello output di hello runbook.

Ad esempio hello codice seguente esegue i calcoli di data utilizzando una variabile di input del runbook denominata $NumberOfDays.  Invia quindi un tempo data calcolata come output toobe utilizzate dalle attività successive nel runbook hello.

    $DateTimeNow = (Get-Date).ToUniversalTime()
    $DateTimeStart = ($DateTimeNow).AddDays(-$NumberOfDays)}
    $DateTimeStart


## <a name="links-and-workflow"></a>Collegamenti e flusso di lavoro
Un **collegamento** in un Runbook grafico connette due attività.  Viene visualizzato nell'area di disegno hello come una freccia che punta da attività di destinazione toohello hello origine attività.  le attività di Hello eseguite nella direzione hello della freccia hello con attività di destinazione hello avvio termine hello origine attività.  

### <a name="create-a-link"></a>Creare un collegamento
Creare un collegamento tra due attività dall'attività di origine selezionando hello e facendo clic su cerchio hello nella parte inferiore di hello della forma hello.  Trascinare l'attività di destinazione toohello freccia hello e di rilascio.

![Creare un collegamento](media/automation-graphical-authoring-intro/create-link-revised20165.png)

Selezionare tooconfigure collegamento hello le relative proprietà nel Pannello di configurazione hello.  Ciò include il tipo di collegamento hello descritta nel hello nella tabella seguente.

| Tipo di collegamento | Descrizione |
|:--- |:--- |
| Pipeline |attività di destinazione Hello viene eseguito una volta per ogni oggetto di output dall'attività di origine hello.  attività di destinazione Hello non viene eseguito se l'attività di origine hello restituito alcun output.  L'output di hello origine attività è disponibile come oggetto. |
| Sequenza |attività di destinazione Hello viene eseguito una sola volta.  Riceve una matrice di oggetti dall'attività di origine hello.  L'output di hello origine attività è disponibile come una matrice di oggetti. |

### <a name="starting-activity"></a>Attività di inizio
Un Runbook grafico inizia con le attività che non dispongono di un collegamento in ingresso.  Si tratterà spesso una sola attività che svolge la stessa funzione hello avvio attività di runbook hello.  Se più attività non dispone di un collegamento in entrata, hello runbook verrà avviato mediante l'esecuzione in parallelo.  Quindi seguirà hello collegamenti toorun altre attività come ognuno viene terminato.

### <a name="conditions"></a>Condizioni
Quando si specifica una condizione su un collegamento, attività di destinazione hello viene eseguito solo se la condizione hello risolve tootrue.  In genere si utilizzerà una variabile $ActivityOutput nell'output di hello tooretrieve condizione dall'attività di origine hello.  

Per un collegamento alla pipeline, specificare una condizione per un singolo oggetto e hello condizione viene valutata per ogni oggetto di output dall'attività di origine hello.  attività di destinazione Hello viene eseguita per ogni oggetto che soddisfa la condizione hello.  Ad esempio, con un'attività di origine di Get-AzureRmVm, hello sintassi avrebbe potuto essere utilizzato un tooretrieve collegamento pipeline condizionale solo hello di macchine virtuali nel gruppo di risorse denominato *Group1*.  

    $ActivityOutput['Get Azure VMs'].Name -match "Group1"

Per un collegamento di sequenza, condizione hello viene valutato solo una volta poiché restituisce una matrice che contiene tutto l'output dall'attività di origine hello oggetti.  Per questo motivo, un collegamento di sequenza non può essere utilizzato per il filtro come un collegamento alla pipeline, ma verrà semplicemente determinare se non viene eseguito l'attività successiva hello. Si consideri ad esempio hello seguente insieme di attività i runbook avvia macchina virtuale.<br> ![Collegamento condizionale con sequenze](media/automation-graphical-authoring-intro/runbook-conditional-links-sequence.png)<br>
Sono presenti tre collegamenti di sequenza diversi che siano verificando i valori sono stati forniti parametri di input runbook tootwo che rappresenta il nome di macchina virtuale e il nome di gruppo di risorse in ordine toodetermine ovvero hello intervenire tootake - avvio di una singola macchina virtuale, avviare tutte le macchine virtuali nel hello gruppo di risorse o tutte le macchine virtuali in una sottoscrizione.  Collegamento di sequenza hello tra tooAzure Connect e Get singola macchina virtuale, ecco logica condizione hello:

    <# 
    Both VMName and ResourceGroupName runbook input parameters have values 
    #>
    (
    (($VMName -ne $null) -and ($VMName.Length -gt 0))
    ) -and (
    (($ResourceGroupName -ne $null) -and ($ResourceGroupName.Length -gt 0))
    )

Quando si utilizza un collegamento condizionale, condizione hello verranno filtrati dati hello disponibili dalle attività di hello origine attività tooother in quel ramo.  Se un'attività è collegamenti toomultiple di hello origine, quindi hello dati tooactivities disponibile in ogni ramo dipenderà dalla condizione hello in collegamento hello toothat ramo.

Ad esempio, hello **inizio AzureRmVm** attività runbook hello seguente avvia tutte le macchine virtuali.  Dispone di due collegamenti condizionali.  collegamenti condizionali prima Hello Usa espressione hello *$ActivityOutput ['Start-AzureRmVM']. IsSuccessStatusCode - eq $true* toofilter se l'attività di avvio AzureRmVm hello completata.  Hello secondo Usa espressione hello *$ActivityOutput ['Start-AzureRmVM']. IsSuccessStatusCode - ne $true* toofilter se attività hello inizio AzureRmVm macchina virtuale di hello toostart non è riuscita.  

![Esempio di collegamento condizionale](media/automation-graphical-authoring-intro/runbook-conditional-links.png)

Qualsiasi attività che segue primo collegamento hello e utilizza hello attività output da Get-AzureVM riceverà solo hello le macchine virtuali che sono state avviate all'ora di hello che Get-AzureVM è stata eseguita.  Qualsiasi attività che segue secondo collegamento hello riceverà solo hello hello le macchine virtuali che erano in esecuzione in fase di hello che Get-AzureVM è stata eseguita.  Qualsiasi attività hello terzo collegamento riceverà tutte le macchine virtuali indipendentemente dal proprio stato in esecuzione.

### <a name="junctions"></a>Giunzioni
Una giunzione è un'attività speciale che attende il completamento di tutti i rami in ingresso.  In questo modo si toorun più attività in parallelo e verificare che sia stata completata prima di proseguire.

Mentre una giunzione può disporre di un numero illimitato di collegamenti in entrata, solo uno di essi può essere una pipeline.  numero di Hello di collegamenti di sequenza in ingresso non è vincolato.  Si potrà essere giunzione hello toocreate con più collegamenti di pipeline in ingresso e salvare hello runbook, ma avrà esito negativo quando viene eseguito.

esempio Hello seguente fa parte di un runbook che avvia una serie di macchine virtuali durante l'applicazione di download contemporaneamente patch toobe toothose macchine.  Giunzione è tooensure utilizzati che entrambi i processi vengono completati prima che il runbook hello continua.

![giunzione](media/automation-graphical-authoring-intro/runbook-junction.png)

### <a name="cycles"></a>Cicli
Un ciclo è quando un'attività di destinazione crea un collegamento nuovamente tooits attività attività o tooanother che infine consente di tornare origine tooits di origine.  I cicli non sono attualmente consentiti nella creazione grafica.  Se un Runbook dispone di un ciclo, verrà salvato correttamente, ma riceverà un errore durante l'esecuzione.

![Ciclo](media/automation-graphical-authoring-intro/runbook-cycle.png)

### <a name="sharing-data-between-activities"></a>Condivisione di dati tra le attività
I dati di output da un'attività con un collegamento in uscita vengono scritti toohello *databus* per hello runbook.  Utilizzare i dati sui valori dei parametri di hello databus toopopulate qualsiasi attività nel runbook hello o inserire nel codice script.  Output di hello di qualsiasi attività precedente nel flusso di lavoro hello accedere a un'attività.     

Modalità di scrittura dati hello toohello databus dipende dal tipo di hello del collegamento attività hello.  Per un **pipeline**, dati hello vengono restituito come oggetti multipli.  Per un **sequenza** collegare, dati hello vengono restituita come matrice.  Se è presente un solo valore, questo verrà restituito come matrice a elemento singolo.

Si può accedere ai dati hello databus utilizzando uno dei due metodi.  Utilizza innanzitutto un **Output attività** toopopulate dell'origine dati un parametro di un'altra attività.  Se l'output di hello è un oggetto, è possibile specificare una singola proprietà.

![Activity Output](media/automation-graphical-authoring-intro/activity-output-datasource-revised20165.png)

È inoltre possibile recuperare l'output di hello di un'attività in un **espressione PowerShell** origine dati o da un **Script del flusso di lavoro** attività con una variabile ActivityOutput.  Se l'output di hello è un oggetto, è possibile specificare una singola proprietà.  Variabili ActivityOutput utilizzano la seguente sintassi hello.

    $ActivityOutput['Activity Label']
    $ActivityOutput['Activity Label'].PropertyName 

### <a name="checkpoints"></a>Checkpoint
È possibile impostare [Checkpoint](automation-powershell-workflow.md#checkpoints) in un runbook grafico del flusso di lavoro PowerShell selezionando *Checkpoint per runbook* in qualsiasi attività.  In questo modo un toobe checkpoint impostata dopo l'esecuzione di attività hello.

![Checkpoint](media/automation-graphical-authoring-intro/set-checkpoint.png)

I checkpoint sono abilitati solo nei runbook grafici del flusso di lavoro PowerShell e non sono disponibili nei runbook grafici.  Se runbook hello utilizza i cmdlet di Azure, è consigliabile eseguire qualsiasi attività relative ai checkpoint con un componente-AzureRMAccount nel caso in cui hello runbook viene sospeso e viene riavviato da questo checkpoint in un altro lavoro. 

## <a name="authenticating-tooazure-resources"></a>L'autenticazione tooAzure risorse
I runbook in automazione di Azure che Gestione risorse di Azure richiede autenticazione tooAzure.  Hello [account RunAs](automation-offering-get-started.md#creating-an-automation-account) (anche noto tooas un'entità servizio) è hello predefinito metodo tooaccess risorse di gestione risorse di Azure nella sottoscrizione con i runbook di automazione.  È possibile aggiungere runbook grafico di tooa questa funzionalità aggiungendo hello **AzureRunAsConnection** asset della connessione, che utilizza hello PowerShell [Get-AutomationConnection](https://technet.microsoft.com/library/dn919922%28v=sc.16%29.aspx) cmdlet e [Aggiungi AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet toohello canvas. Come illustrato nell'esempio seguente hello.<br>![Attività di autenticazione RunAs](media/automation-graphical-authoring-intro/authenticate-run-as-account.png)<br>
Hello attività ottenere eseguire come connessione (ad esempio Get-AutomationConnection), viene configurato con un'origine dati di valore costante denominata AzureRunAsConnection.<br>![Configurazione della connessione RunAs](media/automation-graphical-authoring-intro/authenticate-runas-parameterset.png)<br>
attività successiva Hello, Add-AzureRmAccount, aggiunge hello autenticato account RunAs per l'uso nel runbook hello.<br>
![Set di parametri Add-AzureRmAccount ](media/automation-graphical-authoring-intro/authenticate-conn-to-azure-parameter-set.png)<br>
Per i parametri di hello **APPLICATIONID**, **CERTIFICATETHUMBPRINT**, e **TENANTID** sarà necessario nome hello toospecify della proprietà hello per il percorso campo hello perché attività Hello restituisce un oggetto con più proprietà.  In caso contrario, quando si esegue hello runbook, ne verrà eseguito tooauthenticate durante il tentativo.  Equivale a un minimo tooauthenticate runbook con hello account RunAs è necessario.

toomaintain la compatibilità per i sottoscrittori che hanno creato un'automazione account tramite un [account utente di Azure Active Directory](automation-create-aduser-account.md) toomanage Azure distribuzione classica o per le risorse di gestione risorse di Azure, hello tooauthenticate (metodo) il cmdlet Add-AzureAccount hello con un [asset delle credenziali](automation-credentials.md) che rappresenta un utente di Active Directory con accesso toohello account Azure.

È possibile aggiungere questo runbook grafico tooa di funzionalità mediante l'aggiunta di un'area di toohello asset delle credenziali, seguita da un'attività di Add-AzureAccount.  Aggiungere-AzureAccount utilizza attività credenziali hello per l'input.  Come illustrato nell'esempio seguente hello.

![Attività di autenticazione](media/automation-graphical-authoring-intro/authentication-activities.png)

È necessario tooauthenticate all'inizio di hello del runbook hello e dopo ogni checkpoint.  Questo significa aggiungere un'attività Add-AzureAccount dopo qualsiasi attività Checkpoint-Workflow. Non è necessaria una credenziale di aggiunta attività poiché è possibile utilizzare hello stesso 

![Activity Output](media/automation-graphical-authoring-intro/authentication-activity-output.png)

## <a name="runbook-input-and-output"></a>Input e output di Runbook
### <a name="runbook-input"></a>Input di runbook
Un runbook potrebbe richiedere l'input da un utente all'avvio di runbook hello tramite hello portale di Azure o da un altro runbook se hello corrente viene utilizzato come un elemento figlio.
Ad esempio, se si dispone di un runbook che crea una macchina virtuale, si potrebbe essere necessario tooprovide informazioni quali nome hello della macchina virtuale hello e altre proprietà ogni volta che si avvia runbook hello.  

È possibile accettare l'input per un Runbook definendo uno o più parametri di input.  Fornire valori per questi parametri di che avvio del runbook hello ogni ora.  Quando si avvia un runbook con hello portale di Azure, verrà chiesto valori tooprovide per hello di hello del runbook parametri di input.

È possibile accedere a parametri di input per un runbook, fare clic su hello **Input e output** sulla barra degli strumenti di runbook hello.  

![Input e output di Runbook](media/automation-graphical-authoring-intro/runbook-edit-input-output.png) 

Verrà visualizzata hello **di Input e Output** controllo in cui è possibile modificare un parametro di input esistente o crearne uno nuovo facendo **aggiungere input**. 

![Add input](media/automation-graphical-authoring-intro/runbook-edit-add-input.png)

Ogni parametro di input è definito dalle proprietà hello hello nella tabella seguente.

| Proprietà | Descrizione |
|:--- |:--- |
| Nome |nome univoco di Hello del parametro hello.  Può contenere solo caratteri alfanumerici e non può contenere spazi. |
| Descrizione |Descrizione facoltativa per il parametro di input hello. |
| Tipo |Tipo di dati previsto per il valore di parametro hello.  Quando viene richiesto l'input, Hello portale di Azure fornirà un controllo appropriato per il tipo di dati di hello per ogni parametro. |
| Mandatory |Specifica se è necessario specificare un valore per il parametro hello.  Impossibile avviare runbook Hello se non si fornisce un valore per ogni parametro obbligatorio che non dispone di un valore predefinito. |
| Default Value |Specifica il valore utilizzato per il parametro hello se non viene specificato.  Può essere Null o un valore specifico. |

### <a name="runbook-output"></a>Output del Runbook
Verranno aggiunti altri dati creati da qualsiasi attività che non dispone di un collegamento in uscita toohello [output di hello runbook](http://msdn.microsoft.com/library/azure/dn879148.aspx).  output di Hello viene salvata con il processo di runbook hello ed è disponibile tooa il runbook padre quando hello runbook viene usato come elemento figlio.  

## <a name="powershell-expressions"></a>Espressioni PowerShell
Uno dei vantaggi di hello di grafici per la modifica è offrendo hello possibilità toobuild un runbook con poche informazioni di PowerShell.  Attualmente, è necessario tooknow un bit di PowerShell per popolare determinati [i valori dei parametri](#activities) e per l'impostazione [collegare condizioni](#links-and-workflow).  In questa sezione fornisce una rapida introduzione tooPowerShell espressioni per gli utenti che potrebbero non avere familiari con esso.  I dettagli completi di PowerShell sono disponibili all'indirizzo [Scripting con Windows PowerShell](http://technet.microsoft.com/library/bb978526.aspx). 

### <a name="powershell-expression-data-source"></a>Origine dati delle espressioni PowerShell
È possibile utilizzare un'espressione PowerShell come un valore hello toopopulate dell'origine dati di un [parametro attività](#activities) con risultati hello del codice di PowerShell.  Potrebbe trattarsi di una singola riga di codice che esegue una funzione semplice o più righe che eseguono una logica complessa.  L'output di un comando che non è assegnato tooa variabile è output toohello valore del parametro. 

Ad esempio, hello comando seguente genererebbe hello data corrente. 

    Get-Date

Hello seguenti comandi di compilare una stringa da hello data corrente e la assegna tooa variabile.  il contenuto di Hello di hello variabile viene quindi inviato toohello output 

    $string = "hello current date is " + (Get-Date)
    $string

Hello seguenti comandi valutare hello data corrente e restituiscono una stringa che indica se hello giorno corrente è un fine settimana o giorno della settimana. 

    $date = Get-Date
    if (($date.DayOfWeek = "Saturday") -or ($date.DayOfWeek = "Sunday")) { "Weekend" }
    else { "Weekday" }


### <a name="activity-output"></a>Activity Output
output di hello toouse da una precedente attività runbook hello, utilizzare hello $ActivityOutput variabile con la seguente sintassi hello.

    $ActivityOutput['Activity Label'].PropertyName

Ad esempio, potrebbe essere un'attività con una proprietà che richiede il nome di hello di una macchina virtuale in questo caso è possibile utilizzare l'espressione seguente hello.

    $ActivityOutput['Get-AzureVm'].Name

Se restituisce proprietà hello che l'oggetto macchina virtuale hello anziché semplicemente una proprietà, sarà necessario hello intero oggetto utilizzando hello la seguente sintassi.

    $ActivityOutput['Get-AzureVm']

È inoltre possibile utilizzare l'output di hello di un'attività in un'espressione più complessa, come illustrato di seguito hello che concatena nome della macchina virtuale toohello testo.

    "hello computer name is " + $ActivityOutput['Get-AzureVm'].Name


### <a name="conditions"></a>Condizioni
Utilizzare [gli operatori di confronto](https://technet.microsoft.com/library/hh847759.aspx) toocompare valori o determinare se un valore corrisponde a un modello specificato.  Un confronto restituisce un valore $true o $false.

Ad esempio, hello condizione seguente determina se hello di macchina virtuale da un'attività denominata *Get-AzureVM* attualmente *arrestato*. 

    $ActivityOutput["Get-AzureVM"].PowerState –eq "Stopped"

esempio Hello condizione verifica se hello stessa macchina virtuale è in uno stato diverso da *arrestato*.

    $ActivityOutput["Get-AzureVM"].PowerState –ne "Stopped"

È possibile aggiungere più condizioni usando un [operatore logico](https://technet.microsoft.com/library/hh847789.aspx) ad esempio **-and** o **-or**.  Ad esempio, seguente hello condizione verifica se hello stessa macchina virtuale nell'esempio precedente hello è in uno stato di *arrestato* o *arresto*.

    ($ActivityOutput["Get-AzureVM"].PowerState –eq "Stopped") -or ($ActivityOutput["Get-AzureVM"].PowerState –eq "Stopping") 


### <a name="hashtables"></a>Tabelle hash
[Tabelle hash](http://technet.microsoft.com/library/hh847780.aspx) sono coppie nome/valore utili per la restituzione di un set di valori.  Le proprietà per determinate attività potrebbero prevedere una tabella hash anziché un valore semplice.  È inoltre possibile visualizzare come tabella hash definita tooas un dizionario. 

Si crea una tabella hash con la seguente sintassi hello.  Una tabella hash può contenere qualsiasi numero di voci, ma ciascuna è definita da un nome e valore.

    @{ <name> = <value>; [<name> = <value> ] ...}

Ad esempio, hello espressione seguente crea un toobe hashtable utilizzato nell'origine dati hello per un parametro di attività che prevede una tabella hash con i valori per una ricerca in internet.

    $query = "Azure Automation"
    $count = 10
    $h = @{'q'=$query; 'lr'='lang_ja';  'count'=$Count}
    $h

esempio Hello utilizza l'output di un'attività denominata *ottenere connessione Twitter* toopopulate una tabella hash.

    @{'ApiKey'=$ActivityOutput['Get Twitter Connection'].ConsumerAPIKey;
      'ApiSecret'=$ActivityOutput['Get Twitter Connection'].ConsumerAPISecret;
      'AccessToken'=$ActivityOutput['Get Twitter Connection'].AccessToken;
      'AccessTokenSecret'=$ActivityOutput['Get Twitter Connection'].AccessTokenSecret}



## <a name="next-steps"></a>Passaggi successivi
* tooget avviato con runbook del flusso di lavoro di PowerShell, vedere [il primo runbook del flusso di lavoro di PowerShell](automation-first-runbook-textual.md) 
* tooget avviato con runbook grafici, vedere [il primo runbook grafico](automation-first-runbook-graphical.md)
* tooknow ulteriori informazioni sui tipi di runbook, i relativi vantaggi e limitazioni, vedere [tipi di runbook di automazione di Azure](automation-runbook-types.md)
* toounderstand come tooauthenticate utilizzando hello account RunAs automazione, vedere [configurare Azure Account runas](automation-sec-configure-azure-runas-account.md)

