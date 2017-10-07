---
title: aaaMigrating da Orchestrator tooAzure automazione | Documenti Microsoft
description: Viene descritto come toomigrate runbook e integration pack da System Center Orchestrator tooAzure automazione.
services: automation
documentationcenter: 
author: bwren
manager: stevenka
editor: tysonn
ms.assetid: 1a7da58c-7a98-49b5-9d9d-001a9f6e631a
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/09/2016
ms.author: bwren
ms.openlocfilehash: 797b50067ef2aa68470760e99d494b89ab7baacf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="migrating-from-orchestrator-tooazure-automation-beta"></a>La migrazione da Orchestrator tooAzure automazione (Beta)
I runbook in [System Center Orchestrator](http://technet.microsoft.com/library/hh237242.aspx) si basano su attività di Integration Pack scritte appositamente per Orchestrator, mentre i runbook di Automazione di Azure si basano su Windows PowerShell.  [I runbook grafici](automation-runbook-types.md#graphical-runbooks) in automazione di Azure dispone di un runbook di tooOrchestrator aspetto simile con le relative attività che rappresenta i cmdlet PowerShell, i runbook figlio e risorse.

Hello [Toolkit di migrazione per System Center Orchestrator](http://www.microsoft.com/download/details.aspx?id=47323&WT.mc_id=rss_alldownloads_all) include strumenti tooassist è la conversione di runbook da Orchestrator tooAzure automazione.  Inoltre i runbook hello tooconverting autonomamente, è necessario convertire hello integration pack con hello attività che runbook hello utilizzare toointegration moduli con i cmdlet di Windows PowerShell.  

Di seguito è il processo di base hello per la conversione di Orchestrator runbook tooAzure automazione.  Ognuno di questi passaggi viene descritto in dettaglio nelle sezioni hello riportato di seguito.

1. Scaricare hello [Toolkit di migrazione per System Center Orchestrator](http://www.microsoft.com/download/details.aspx?id=47323&WT.mc_id=rss_alldownloads_all) che contiene gli strumenti di hello e moduli descritti in questo articolo.
2. Importare il [modulo delle attività standard](#standard-activities-module) in Automazione di Azure.  Questo modulo include versioni convertite di attività standard di Orchestrator che possono essere usate dai runbook convertiti.
3. Importare i [moduli di integrazione di System Center Orchestrator](#system-center-orchestrator-integration-modules) in Automazione di Azure per gli Integration Pack usati dai runbook che accedono a System Center.
4. Convertire i pacchetti di integrazione di terze parti e personalizzati utilizzando hello [Integration Pack convertitore](#integration-pack-converter) e importare in automazione di Azure.
5. Convertire i runbook di Orchestrator utilizzando hello [Runbook convertitore](#runbook-converter) e installare in automazione di Azure.
6. Creare manualmente necessarie risorse di Orchestrator in automazione di Azure poiché hello convertitore Runbook non consente di convertire queste risorse.
7. Configurare un [Runbook Worker ibrido](#hybrid-runbook-worker) dei runbook toorun convertito di centro dati locale che avrà accesso alle risorse locali.

## <a name="service-management-automation"></a>Service Management Automation
[Service Management Automation](http://technet.microsoft.com/library/dn469260.aspx) (SMA) archivia ed esegue i runbook in data center locale come Orchestrator e Usa hello stesso moduli di integrazione di automazione di Azure. Hello [Runbook convertitore](#runbook-converter) converte i runbook di Orchestrator runbook toographical tuttavia che non sono supportati in SMA.  È comunque possibile installare hello [modulo attività Standard](#standard-activities-module) e [moduli di integrazione di System Center Orchestrator](#system-center-orchestrator-integration-modules) in SMA, ma è necessario manualmente [riscrivere i runbook](http://technet.microsoft.com/library/dn469262.aspx).

## <a name="hybrid-runbook-worker"></a>ruolo di lavoro ibrido per runbook
I runbook in Orchestrator sono archiviati in un server di database e vengono eseguiti in server runbook, tutti contenuti nel data center locale.  I runbook in automazione di Azure vengono archiviati in hello cloud di Azure e possono essere eseguiti nel data center locale tramite un [Runbook Worker ibrido](automation-hybrid-runbook-worker.md).  Si tratta come verranno in genere eseguire runbook convertito da Orchestrator poiché sono progettate toorun sui server locali.

## <a name="integration-pack-converter"></a>Integration Pack Converter
Hello Integration Pack convertitore converte integration pack che sono stati creati mediante hello [Orchestrator Integration Toolkit (OIT)](http://technet.microsoft.com/library/hh855853.aspx) toointegration moduli basata su Windows PowerShell che possono essere importati in automazione di Azure o Service Management Automation.  

Quando si esegue hello Integration Pack convertitore, viene visualizzata una procedura guidata che consente di tooselect un file dell'integration pack (con estensione oip).  procedura guidata Hello quindi Elenca le attività di hello incluse in tale integration pack e consente tooselect che verrà eseguita.  Quando si completa la procedura guidata hello, viene creato un modulo di integrazione che include un cmdlet corrispondente per ognuna delle attività hello nel pacchetto di integrazione hello originale.

### <a name="parameters"></a>parameters
Tutte le proprietà di un'attività nel pacchetto di integrazione hello sono tooparameters convertito di hello corrispondenti cmdlet nel modulo di integrazione hello.  I cmdlet di Windows PowerShell dispongono di un set di [parametri comuni](http://technet.microsoft.com/library/hh847884.aspx) che possono essere usati con tutti i cmdlet.  Ad esempio hello - parametro Verbose, un cmdlet toooutput informazioni dettagliate sul suo funzionamento.  Nessun cmdlet potrebbe avere un parametro con stesso nome come parametro comune hello.  Se un'attività dispone di una proprietà con hello stesso nome come parametro comune, la procedura guidata hello richiederà tooprovide è un altro nome per il parametro hello.

### <a name="monitor-activities"></a>Attività di monitoraggio
Monitorare i runbook di avvio di Orchestrator con un [monitorare l'attività](http://technet.microsoft.com/library/hh403827.aspx) ed eseguire continuamente toobe attesa richiamato da un particolare evento.  Automazione di Azure non supporta i runbook di monitoraggio, in modo qualsiasi attività di monitoraggio nel pacchetto di integrazione hello non verrà convertito.  Un cmdlet segnaposto viene invece creato nel modulo di integrazione hello per monitorare l'attività hello.  Questo cmdlet non presenta alcuna funzionalità, ma consente qualsiasi runbook convertito che utilizza tale toobe installato.  Questo runbook non saranno in grado di toorun in automazione di Azure, ma può essere installato in modo da poterlo modificare.

### <a name="integration-packs-that-cannot-be-converted"></a>Integration Pack che non possono essere convertiti
Impossibile convertire i pacchetti di integrazione non sono stati creati con OIT con hello Integration Pack convertitore. Esistono anche alcuni Integration Pack di Microsoft che attualmente non è possibile convertire con questo strumento.  Le versioni convertite di questi Integration Pack sono [disponibili per il download](#system-center-orchestrator-integration-modules) , in modo da poterle installare in Automazione di Azure o in Service Management Automation.

## <a name="standard-activities-module"></a>modulo delle attività standard
Orchestrator contiene un insieme di [attività standard](http://technet.microsoft.com/library/hh403832.aspx) non incluse in un Integration Pack, ma usate da molti runbook.  Attività Standard Hello è un modulo di integrazione che include un cmdlet equivalente per ognuna di queste attività.  È necessario installare questo modulo di integrazione in Automazione di Azure prima di importare eventuali runbook convertiti che usano un'attività standard.

Inoltre toosupporting convertito runbook, hello cmdlet nel modulo di attività standard hello è utilizzabile da chiunque abbia familiarità con Orchestrator toobuild nuovi runbook in automazione di Azure.  Mentre la funzionalità di hello di tutte le attività standard hello può essere eseguita con i cmdlet, possono funzionare in modo diverso.  Hello cmdlet in hello convertito attività standard modulo funzionerà hello stesso come utilizzare e le attività corrispondenti hello stessi parametri.  Questo può aiutare hello Orchestrator runbook autore esistente in loro tooAzure transizione runbook di automazione.

## <a name="system-center-orchestrator-integration-modules"></a>moduli di integrazione di System Center Orchestrator
Microsoft fornisce [integration pack](http://technet.microsoft.com/library/hh295851.aspx) per la creazione di componenti di System Center tooautomate runbook e altri prodotti.  Alcuni di questi pacchetti di integrazione attualmente basati su OIT ma non può essere convertito toointegration moduli attualmente a causa di problemi noti.  [moduli di integrazione di System Center Orchestrator](https://www.microsoft.com/download/details.aspx?id=49555) includono versioni convertite degli Integration Pack che possono essere importate in Automazione di Azure e in Service Management Automation.  

Da versione RTM di hello di questo strumento, versioni aggiornate dei pacchetti di integrazione hello in base a OIT che può essere convertito con hello che Integration Pack convertitore verrà pubblicato.  Linee guida verrà inoltre descritti nella conversione runbook utilizzando attività hello pacchetti di integrazione non in base a OIT tooassist.

## <a name="runbook-converter"></a>Runbook Converter
Hello Runbook convertito dal convertitore i runbook di Orchestrator in [runbook grafici](automation-runbook-types.md#graphical-runbooks) che possono essere importati in automazione di Azure.  

Convertitore runbook viene implementato come un modulo di PowerShell con un cmdlet denominato **ConvertFrom-SCORunbook** che esegue la conversione di hello.  Quando si installa lo strumento di hello, crea una sessione di PowerShell tooa di scelta rapida che carica hello cmdlet.   

Seguente è hello tooconvert di processo di base di un runbook di Orchestrator e importarlo in automazione di Azure.  Hello nelle sezioni seguenti forniscono ulteriori dettagli sull'uso dello strumento hello e utilizzo dei runbook convertito.

1. Esportare uno o più runbook da Orchestrator.
2. Ottenere i moduli di integrazione per tutte le attività nel runbook hello.
3. Convertire i runbook di Orchestrator hello nel file esportato hello.
4. Esaminare le informazioni nel log toovalidate hello conversione e toodetermine qualsiasi attività manuale necessaria.
5. Importare i runbook convertiti in Automazione di Azure.
6. Creare gli eventuali asset necessari in Automazione di Azure.
7. Modificare hello runbook in automazione di Azure toomodify qualsiasi attività necessarie.

### <a name="using-runbook-converter"></a>Uso di Runbook Converter
sintassi per Hello **ConvertFrom-SCORunbook** è indicato di seguito:

    ConvertFrom-SCORunbook -RunbookPath <string> -Module <string[]> -OutputFolder <string>

* RunbookPath - esportazione toohello percorso del file contenente hello runbook tooconvert.
* Modulo - elenco di moduli di integrazione contenente attività runbook hello delimitato da virgole.
* CartellaOutput - percorso toohello cartella toocreate convertito runbook grafici.

Dopo il comando di esempio converte hello i runbook in un file di esportazione chiamato Hello **MyRunbooks.ois_export**.  Questi runbook utilizzano hello Active Directory e Data Protection Manager integration pack.

    ConvertFrom-SCORunbook -RunbookPath "c:\runbooks\MyRunbooks.ois_export" -Module c:\ip\SystemCenter_IntegrationModule_ActiveDirectory.zip,c:\ip\SystemCenter_IntegrationModule_DPM.zip -OutputFolder "c:\runbooks"


### <a name="log-files"></a>File di log
Hello convertitore Runbook verrà creati i seguenti file di log in hello hello stesso percorso hello convertito runbook.  Se il file hello esistono già, quindi verranno sovrascritti con le informazioni di conversione ultimo hello.

| File | Sommario |
|:--- |:--- |
| Runbook Converter - Progress.log |Procedura dettagliata di conversione hello comprese le informazioni per ogni attività di conversione ha esito positivo e avviso per ogni attività non convertito. |
| Runbook Converter - Summary.log |Riepilogo di hello ultimo conversione gli eventuali avvisi e seguire le attività che è necessario tooperform ad esempio la creazione di una variabile per runbook hello convertito. |

### <a name="exporting-runbooks-from-orchestrator"></a>Esportazione di runbook da Orchestrator
Hello Runbook convertitore funziona con un file di esportazione da Orchestrator che contiene uno o più runbook.  Verrà creato un runbook di automazione di Azure corrispondente per ogni runbook di Orchestrator nel file di esportazione hello.  

tooexport un runbook da Orchestrator, fare doppio clic su nome hello di hello runbook in Runbook Designer e selezionare **esportare**.  tooexport tutti i runbook in una cartella, fare doppio clic su nome hello della cartella hello e selezionare **esportare**.

### <a name="runbook-activities"></a>Attività del Runbook
Hello Runbook convertitore converte ogni attività in hello Orchestrator tooa corrispondente attività del runbook in automazione di Azure.  Per le attività che non possono essere convertite, viene creata un'attività di segnaposto hello runbook con il testo di avviso.  Dopo aver importato hello convertito runbook in automazione di Azure, è necessario sostituire qualsiasi di queste attività con attività valida che eseguono la funzionalità di hello necessario.

Qualsiasi attività di Orchestrator nella hello [modulo attività Standard](#standard-activities-module) verrà convertito.  Tuttavia, vi sono alcune attività standard di Orchestrator che non sono in questo modulo e che non vengono convertite.  Ad esempio, **invia evento piattaforma** poiché evento hello tooOrchestrator specifico è presente alcun equivalente di automazione di Azure.

[Monitorare le attività](https://technet.microsoft.com/library/hh403827.aspx) non vengono convertiti poiché non esiste alcun equivalente toothem in automazione di Azure.  Hello eccezione sono monitor attività [convertito integration pack](#integration-pack-converter) che sarà convertito toohello attività di segnaposto.

Qualsiasi attività da un [convertito pack di integrazione](#integration-pack-converter) verrà convertito se si fornisce modulo di integrazione di hello percorso toohello hello **moduli** parametro.  Per System Center Integration Pack, è possibile utilizzare hello [moduli di integrazione di System Center Orchestrator](#system-center-orchestrator-integration-modules).

### <a name="orchestrator-resources"></a>Risorse di Orchestrator
Hello Runbook convertitore converte solo i runbook, non altre risorse di Orchestrator, ad esempio i contatori, variabili o le connessioni.  I contatori non sono supportati in Automazione di Azure.  Le variabili e le connessioni sono supportate, ma è necessario crearle manualmente.  file di log Hello verranno che indicano se hello runbook richiede tali risorse e specificare le risorse corrispondenti che è necessario toocreate in automazione di Azure per hello convertito runbook toooperate correttamente.

Ad esempio, un runbook può utilizzare una variabile toopopulate un valore specifico in un'attività.  Hello runbook convertito convertirà attività hello e specificare un asset della variabile di automazione di Azure con stesso nome di variabile Orchestrator hello hello.  Questo verrà registrato in hello **Runbook convertitore - Summary.log** file creato dopo la conversione di hello.  Sarà necessario toomanually creare questo asset della variabile di automazione di Azure prima di usare runbook hello.

### <a name="input-parameters"></a>Parametri di input
I runbook di Orchestrator accettano parametri di input con hello **Inizializza dati** attività.  Se il runbook hello convertito include questa attività, quindi un [parametro di input](automation-graphical-authoring-intro.md#runbook-input-and-output) in automazione di Azure hello runbook viene creato per ogni parametro nell'attività hello.  Oggetto [controllo Script del flusso di lavoro](automation-graphical-authoring-intro.md#activities) creazione di attività nel runbook hello convertito che recupera e restituisce ogni parametro.  Qualsiasi attività nel runbook hello che utilizzano un parametro di input, output toohello fare riferimento da questa attività.

motivo di Hello viene utilizzata questa strategia è toobest mirror hello funzionalità hello runbook di Orchestrator.  Attività runbook grafica nuovo deve fare riferimento direttamente parametri tooinput utilizzando un'origine dati di input di Runbook.

### <a name="invoke-runbook-activity"></a>Richiamare l'attività del runbook
I runbook di Orchestrator avviare altri runbook con hello **richiama Runbook** attività. Se il runbook hello convertito include questa attività e hello **attendere il completamento** opzione è impostata, quindi viene creata un'attività del runbook per tale runbook hello convertito.  Se hello **attendere il completamento** opzione non è impostata, quindi viene creata un'attività Script del flusso di lavoro che utilizza **Start-AzureAutomationRunbook** toostart hello runbook.  Dopo aver importato hello convertito runbook in automazione di Azure, è necessario modificare questa attività con le informazioni di hello specificate nell'attività hello.

## <a name="related-articles"></a>Articoli correlati
* [System Center 2012 - Orchestrator](http://technet.microsoft.com/library/hh237242.aspx)
* [Service Management Automation](https://technet.microsoft.com/library/dn469260.aspx)
* [Hybrid Runbook Worker](automation-hybrid-runbook-worker.md)
* [Attività Standard di Orchestrator](http://technet.microsoft.com/library/hh403832.aspx)
* [System Center Orchestrator Migration Toolkit](https://www.microsoft.com/en-us/download/details.aspx?id=47323)
