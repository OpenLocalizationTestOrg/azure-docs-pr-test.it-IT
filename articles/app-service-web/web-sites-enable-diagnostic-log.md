---
title: aaaEnable la registrazione diagnostica per App web nel servizio App di Azure
description: "Informazioni su come la registrazione diagnostica tooenable e aggiungere strumentazione tooyour applicazione, nonché come tooaccess hello informazioni registrate da Azure."
services: app-service
documentationcenter: .net
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: c9da27b2-47d4-4c33-a3cb-1819955ee43b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/06/2016
ms.author: cephalin
ms.openlocfilehash: 4b2903ff31cc93180552cf51196c33505ffbaf07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-diagnostics-logging-for-web-apps-in-azure-app-service"></a>Abilitare la registrazione diagnostica per le app Web nel servizio app di Azure
## <a name="overview"></a>Panoramica
Azure offre tooassist di diagnostica con il debug di un [App del servizio web app](http://go.microsoft.com/fwlink/?LinkId=529714). In questo articolo si apprenderà come la registrazione diagnostica tooenable e aggiungere strumentazione tooyour applicazione, nonché come tooaccess hello informazioni registrate da Azure.

Questo articolo Usa hello [portale Azure](https://portal.azure.com), Azure PowerShell e hello interfaccia della riga di comando di Azure (Azure CLI) toowork con i log di diagnostica. Per informazioni sull'elaborazione dei log di diagnostica in Visual Studio vedere [Risoluzione dei problemi di Azure in Visual Studio](web-sites-dotnet-troubleshoot-visual-studio.md).

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="whatisdiag"></a>Diagnostica del server Web e diagnostica dell'applicazione
Le applicazioni di servizio App web forniscono funzionalità di diagnostica per la registrazione delle informazioni dal server web hello e un'applicazione web hello. logicamente separate in **diagnostica server Web** e **diagnostica applicazioni**.

### <a name="web-server-diagnostics"></a>Diagnostica del server Web
È possibile abilitare o disabilitare i seguenti tipi di registri hello:

* **Registrazione degli errori dettagliata**: consente di registrare informazioni dettagliate sugli errori relativi ai codici di stato HTTP che indicano un'operazione non riuscita (codice di stato 400 o superiore), Può contenere informazioni utili per determinare perché i server di hello ha restituito il codice di errore hello.
* **Non è stato possibile traccia richiesta** -informazioni dettagliate sulle richieste non riuscite, tra cui una traccia di hello IIS componenti utilizzati tooprocess hello richiesta e tempo hello in ogni componente. Può essere utile se si siano tentando di prestazioni del sito tooincrease o isolare la causa un toobe specifico di errore HTTP restituito.
* **Registrazione del Server Web** -informazioni sulle transazioni HTTP tramite hello [formato di file registro esteso W3C](http://msdn.microsoft.com/library/windows/desktop/aa814385.aspx). Ciò è utile quando si determinano le metriche di generale del sito, ad esempio il numero di hello di richieste gestite o il numero di richieste provengono da un indirizzo IP specifico.

### <a name="application-diagnostics"></a>Diagnostica applicazioni
Diagnostica delle applicazioni consente informazioni toocapture prodotte da un'applicazione web. Applicazioni ASP.NET possono usare hello [Trace](http://msdn.microsoft.com/library/36hhw2t6.aspx) classe toolog informazioni toohello application diagnostics log. ad esempio:

    System.Diagnostics.Trace.TraceError("If you're seeing this, something bad happened");

In fase di esecuzione è possibile recuperare queste toohelp i log di risoluzione dei problemi. Per altre informazioni, vedere [Risoluzione dei problemi delle app Web di Azure in Visual Studio](web-sites-dotnet-troubleshoot-visual-studio.md).

App del servizio web App registrare anche informazioni sulla distribuzione, quando si pubblica l'app web tooa contenuto. Ciò avviene automaticamente e non sono disponibili impostazioni di configurazione per la registrazione di distribuzione. Registrazione di distribuzione consente toodetermine perché una distribuzione non è riuscita. Ad esempio, se si utilizza uno script di distribuzione personalizzati, è possibile utilizzare distribuzione registrazione toodetermine perché hello script non riesce.

## <a name="enablediag"></a>La diagnostica tooenable
diagnostica tooenable in hello [portale Azure](https://portal.azure.com), toohello pannello per l'app web, fare clic su **Impostazioni > log di diagnostica**.

<!-- todo:cleanup dogfood addresses in screenshot -->
![Parte del log](./media/web-sites-enable-diagnostic-log/logspart.png)

Quando si abilita **diagnostica applicazioni** inoltre è hello **livello**. Questa impostazione consente di informazioni di hello toofilter acquisite troppo**informativo**, **avviso** o **errore** informazioni. L'impostazione troppo**verbose** registrerà tutte le informazioni prodotte da un'applicazione hello.

> [!NOTE]
> A differenza di modifica di Web. config hello file, l'abilitazione di diagnostica dell'applicazione o modifica dei livelli di log di diagnostica non la ricicli dominio applicazione hello eseguita all'interno di un'applicazione hello.
>
>

In hello [portale classico](https://manage.windowsazure.com) app Web **configura** scheda, è possibile selezionare **archiviazione** o **del file system** per **server web registrazione**. Selezione **archiviazione** consente tooselect un account di archiviazione, quindi selezionare un contenitore blob che verranno scritti i log di hello. Tutti gli altri log per **diagnostica sito** vengono scritti toohello file solo per il sistema.

Hello [portale classico](https://manage.windowsazure.com) app Web **configura** scheda contiene anche le impostazioni aggiuntive per la diagnostica delle applicazioni:

* **File di sistema** -hello di archivi di sistema di file di applicazione diagnostica informazioni toohello web app. Questi file possono essere accessibile tramite FTP, o scaricati come archivio Zip utilizzando hello Azure PowerShell o l'interfaccia della riga di comando di Azure (Azure CLI).
* **Archiviazione tabelle** -archivi hello informazioni di diagnostica dell'applicazione nel nome di Account di archiviazione di Azure e di tabella specificato hello.
* **Archiviazione BLOB** -archivi hello informazioni di diagnostica applicazione contenitore di blob e Account di archiviazione di Azure specificato hello.
* **Periodo di conservazione**: per impostazione predefinita, i log non vengono eliminati automaticamente dall'**archiviazione BLOB**. Selezionare **di conservazione impostato** e immettere hello numero di giorni tookeep log se si desidera tooautomatically eliminare i log.

> [!NOTE]
> Se si [rigenerare le chiavi di accesso dell'account di archiviazione](../storage/common/storage-create-storage-account.md), è necessario reimpostare le chiavi di hello aggiornato toouse configurazione hello registrazione corrispondente. toodo questo:
>
> 1. In hello **configura** scheda, impostare la funzionalità di registrazione dei rispettivi hello troppo**Off**. Salvare l’impostazione.
> 2. Abilitare la registrazione toohello blob dell'account di archiviazione o una tabella. Salvare l’impostazione.
>
>

Qualsiasi combinazione di file system, archiviazione tabelle o nell'archiviazione blob può essere abilitata in hello stesso tempo, mentre sono le configurazioni a livello di singolo registro. Ad esempio, si consiglia toolog errori e avvisi tooblob archiviazione a lungo termine della registrazione, durante l'abilitazione di registrazione nel file system con un livello di dettaglio.

Mentre tutte e tre i percorsi di archiviazione forniscono hello stesse informazioni di base per gli eventi registrati, **archivio tabelle** e **nell'archiviazione blob** registrare informazioni aggiuntive, ad esempio l'ID istanza hello, ID thread e più timestamp granulare (formato tick) di registrazione troppo**del file system**.

> [!NOTE]
> Le informazioni memorizzate nell'**archiviazione tabelle** o **nell'archiviazione BLOB** sono accessibili solo tramite un client o un'applicazione di archiviazione che possano funzionare direttamente con questi sistemi di archiviazione. Ad esempio, Visual Studio 2013 contiene una finestra di esplorazione di archiviazione che possono essere utilizzati tooexplore tabella o archiviazione blob e HDInsight può accedere ai dati archiviati nell'archiviazione blob. È anche possibile scrivere un'applicazione che accede all'archiviazione di Azure utilizzando uno dei hello [Azure SDK](/downloads/#).
>
> [!NOTE]
> Diagnostica può anche essere attivata da Azure PowerShell utilizzando hello **Set-AzureWebsite** cmdlet. Se non è stato installato Azure PowerShell o non configurati toouse la sottoscrizione di Azure, vedere [come tooUse Azure PowerShell](/develop/nodejs/how-to-guides/powershell-cmdlets/).
>
>

## <a name="download"></a> Procedura: Scaricare i log
Il file system di informazioni di diagnostica archiviate toohello web app è possibile accedere direttamente tramite FTP. Può essere scaricato anche come archivio Zip utilizzando Azure PowerShell o hello interfaccia della riga di comando di Azure.

struttura di directory Hello hello log vengono archiviati in è la seguente:

* **Application logs** - /LogFiles/Application/. In questa cartella sono presenti uno o più file di testo contenenti le informazioni generate dalla registrazione dell'applicazione.
* **Failed Request Traces** - /LogFiles/W3SVC#########/. Questa cartella contiene un file XSL e uno o più file XML. Assicurarsi di scaricare file XSL hello in hello stessa directory hello che XML file perché il file XSL hello fornisce funzionalità per la formattazione e filtrare il contenuto di hello di hello XML file quando viene visualizzato in Internet Explorer.
* **Detailed Error Logs** - /LogFiles/DetailedErrors/. Questa cartella contiene uno o più file HTM che forniscono informazioni dettagliate relative agli eventuali errori HTTP che si sono verificati.
* **Web Server Logs** - /LogFiles/http/RawLogs. Questa cartella contiene uno o più file di testo formattati utilizzando hello [formato di file registro esteso W3C](http://msdn.microsoft.com/library/windows/desktop/aa814385.aspx).
* **Deployment logs** - /LogFiles/Git. Questa cartella contiene i log generati da processi di distribuzione interna hello usati da app web di Azure, nonché log per le distribuzioni Git.

### <a name="ftp"></a>FTP
informazioni di diagnostica tooaccess tramite FTP, visitare hello **Dashboard** dell'app web in hello [portale classico](https://manage.windowsazure.com). In hello **riepilogo rapido** sezione, utilizzare hello **registri di diagnostica FTP** collegare i file di log hello tooaccess tramite FTP. Hello **utente distribuzione/FTP** nome utente hello che deve essere sito FTP hello tooaccess usato è elencata.

> [!NOTE]
> Se hello **utente distribuzione/FTP** voce non è impostata, o hello password per l'utente è stata dimenticata, è possibile creare un nuovo utente e una password utilizzando hello **reimpostare le credenziali di distribuzione** collegamento hello **riepilogo rapido** sezione di hello **Dashboard**.
>
>

### <a name="download-with-azure-powershell"></a>Download con Azure PowerShell
file di log toodownload hello, avviare una nuova istanza di Azure PowerShell e utilizzare hello comando seguente:

    Save-AzureWebSiteLog -Name webappname

Ciò consentirà di registri hello per l'app web hello specificato da hello **-nome** file tooa parametro denominato **logs.zip** nella directory corrente hello.

> [!NOTE]
> Se non è stato installato Azure PowerShell o non configurati toouse la sottoscrizione di Azure, vedere [come tooUse Azure PowerShell](/develop/nodejs/how-to-guides/powershell-cmdlets/).
>
>

### <a name="download-with-azure-command-line-interface"></a>Download con l'interfaccia della riga di comando di Azure
file di log hello toodownload utilizzando hello Azure interfaccia della riga di comando, aprire un nuovo prompt dei comandi, PowerShell, Bash o sessione Terminal e immettere hello comando seguente:

    azure site log download webappname

Ciò consentirà di registri hello per l'app web hello denominato 'webappname' tooa file denominato **diagnostics.zip** nella directory corrente hello.

> [!NOTE]
> Se non è stato installato hello interfaccia della riga di comando di Azure (Azure CLI), o non configurato toouse la sottoscrizione di Azure, vedere [come tooUse CLI di Azure](../cli-install-nodejs.md).
>
>

## <a name="how-to-view-logs-in-application-insights"></a>Procedura: visualizza i registri in Application Insights
Visual Studio Application Insights offre strumenti per il filtro e ricerca log e per la correlazione registri hello con le richieste e altri eventi.

1. Aggiungi progetto tooyour di Application Insights SDK hello in Visual Studio.
   * Fare clic con il pulsante destro del mouse in Esplora soluzioni e scegliere Aggiungi Application Insights. Informazioni dettagliate dei passaggi che includono la creazione di una risorsa di Application Insights. [Altre informazioni](../application-insights/app-insights-asp-net.md)
2. Aggiungi progetto tooyour pacchetto di hello Listener di traccia.
   * In Visual Studio fare clic con il pulsante destro del mouse sul progetto e scegliere Gestisci pacchetti NuGet. Selezionare `Microsoft.ApplicationInsights.TraceListener` [ulteriori](../application-insights/app-insights-asp-net-trace-logs.md)
3. Caricare il progetto ed eseguire toogenerate dati del log.
4. In hello [portale Azure](https://portal.azure.com/)esplorazione tooyour nuova risorsa di Application Insights e aprire **ricerca**. Verranno visualizzati i dati dei log insieme a quelli relativi alle richieste, all'utilizzo e alla telemetria. Alcuni dati di telemetria potrebbe richiedere alcuni minuti tooarrive: fare clic su Aggiorna. [Altre informazioni](../application-insights/app-insights-diagnostic-search.md)

[Ulteriori informazioni sulle prestazioni di rilevamento con Application Insights](../application-insights/app-insights-azure-web-apps.md)

## <a name="streamlogs"></a> Procedura: Eseguire lo streaming dei log
Durante lo sviluppo di un'applicazione, è spesso utile toosee informazioni di registrazione in tempo quasi reale. Questo può essere eseguito dal flusso di registrazione ambiente di sviluppo tooyour informazioni utilizzando Azure PowerShell o hello interfaccia della riga di comando di Azure.

> [!NOTE]
> Alcuni tipi di buffer di registrazione scrivere file di log toohello, che può generare eventi nel flusso di hello non in ordine. Ad esempio, una voce del Registro applicazione che si verifica quando un utente visita una pagina potrebbe essere visualizzata nel flusso di hello prima hello corrispondente HTTP voce di log per la richiesta di pagina hello.
>
> [!NOTE]
> Log di streaming anche trasmetterà informazioni scritte tooany file di testo archiviati in hello **unità d:\\home\\LogFiles\\**  cartella.
>
>

### <a name="streaming-with-azure-powershell"></a>Streaming con Azure PowerShell
informazioni di registrazione toostream, avviare una nuova istanza di Azure PowerShell e utilizzare hello comando seguente:

    Get-AzureWebSiteLog -Name webappname -Tail

Verrà connessa toohello web app specificato dal hello **-nome** parametro e avviare il flusso di finestra di PowerShell toohello informazioni nel registro eventi si verificano nell'applicazione web hello. Le informazioni scritte toofiles che terminano con estensione txt, log o con estensione htm che vengono archiviati nella directory /LogFiles hello (d/home/logfiles) verranno trasmesso toohello console locale.

eventi specifici toofilter, ad esempio gli errori, utilizzano hello **-messaggio** parametro. ad esempio:

    Get-AzureWebSiteLog -Name webappname -Tail -Message Error

tipi di log specifico toofilter, ad esempio HTTP, utilizzano hello **-percorso** parametro. ad esempio:

    Get-AzureWebSiteLog -Name webappname -Tail -Path http

un elenco di percorsi disponibili, utilizzare hello - ListPath parametro toosee.

> [!NOTE]
> Se non è stato installato Azure PowerShell o non configurati toouse la sottoscrizione di Azure, vedere [come tooUse Azure PowerShell](/develop/nodejs/how-to-guides/powershell-cmdlets/).
>
>

### <a name="streaming-with-azure-command-line-interface"></a>Streaming con l'interfaccia della riga di comando di Azure
informazioni di registrazione toostream, aprire un nuovo prompt dei comandi, PowerShell, Bash o sessione Terminal e immettere hello comando seguente:

    azure site log tail webappname

Questo si connetterà app web toohello denominato 'webappname' e avviare il flusso finestra toohello informazioni nel registro eventi si verificano nell'applicazione web hello. Le informazioni scritte toofiles che terminano con estensione txt, log o con estensione htm che vengono archiviati nella directory /LogFiles hello (d/home/logfiles) verranno trasmesso toohello console locale.

eventi specifici toofilter, ad esempio gli errori, utilizzano hello **-filtro** parametro. ad esempio:

    azure site log tail webappname --filter Error

tipi di log specifico toofilter, ad esempio HTTP, utilizzano hello **-percorso** parametro. ad esempio:

    azure site log tail webappname --path http

> [!NOTE]
> Se non è stato installato hello interfaccia della riga di comando di Azure, o non configurato toouse la sottoscrizione di Azure, vedere [come tooUse interfaccia della riga di comando di Azure](../cli-install-nodejs.md).
>
>

## <a name="understandlogs"></a> Procedura: Comprendere i log di diagnostica
### <a name="application-diagnostics-logs"></a>Log di diagnostica applicazioni
Diagnostica applicazioni archivia le informazioni in un formato specifico per le applicazioni .NET, a seconda se si archiviano i registri toohello file system, archiviazione tabelle, o nell'archiviazione blob. set di dati archiviati base Hello è hello stesso in tutti i tre tipi di archiviazione - evento di hello hello data e ora si è verificato, hello ID di processo che ha generato l'evento hello, tipo di evento hello (informazioni, avviso o errore) e il messaggio di evento hello.

**File system**

Ogni riga toohello registrato del file system o ricevuti mediante il flusso si trovano hello seguente formato:

    {Date}  PID[{process id}] {event type/level} {message}

Ad esempio, un evento di errore appariranno simili toohello seguenti:

    2014-01-30T16:36:59  PID[3096] Error       Fatal error on hello page!

Registrazione sistema file toohello offre informazioni di base di hello tre metodi disponibili, fornire solo il tempo di hello, id di processo, livello evento e messaggio hello.

**Archiviazione tabelle**

Durante la registrazione archiviazione tootable, sono utilizzati toofacilitate ricerca di hello dati archiviati nella tabella hello nonché più granulare informazioni sull'evento hello proprietà aggiuntive. Hello seguente proprietà (colonne) vengono utilizzate per ogni entità (righe) archiviate nella tabella hello.

| Nome proprietà | Valore/formato |
| --- | --- |
| PartitionKey |Data/ora dell'evento hello in formato yyyyMMddHH |
| RowKey |Valore GUID che identifica questa entità in modo univoco |
| Timestamp |si è verificato Hello data e ora di hello evento |
| EventTickCount |Hello data e ora di hello evento si è verificato, nel formato Tick (la precisione maggiore di) |
| ApplicationName |nome dell'applicazione web Hello |
| Level |Livello dell'evento (ad esempio, errore, avviso, informazione) |
| EventId |ID evento Hello dell'evento<p><p>Per impostazione predefinita too0 se non specificato |
| InstanceId |Si è verificato l'istanza dell'app web hello che hello anche in |
| Pid |ID di processo |
| Tid |Hello ID del thread di hello che ha generato hello evento |
| Message |Messaggio dettagliato sull'evento |

**Archiviazione BLOB**

Durante la registrazione archiviazione tooblob, i dati vengono archiviati in formato con valori delimitati da virgole (CSV). Archiviazione tootable simile, i campi aggiuntivi siano registrati tooprovide più granulare informazioni sull'evento hello. Hello seguenti vengono utilizzate per ogni riga hello CSV:

| Nome proprietà | Valore/formato |
| --- | --- |
| Date |si è verificato Hello data e ora di hello evento |
| Level |Livello dell'evento (ad esempio, errore, avviso, informazione) |
| ApplicationName |nome dell'applicazione web Hello |
| InstanceId |Istanza dell'app web hello che hello evento si è verificato in |
| EventTickCount |Hello data e ora di hello evento si è verificato, nel formato Tick (la precisione maggiore di) |
| EventId |ID evento Hello dell'evento<p><p>Per impostazione predefinita too0 se non specificato |
| Pid |ID di processo |
| Tid |Hello ID del thread di hello che ha generato hello evento |
| Message |Messaggio dettagliato sull'evento |

dati Hello archiviati in un blob avrà un aspetto simile toohello seguenti:

    date,level,applicationName,instanceId,eventTickCount,eventId,pid,tid,message
    2014-01-30T16:36:52,Error,mywebapp,6ee38a,635266966128818593,0,3096,9,An error occurred

> [!NOTE]
> prima riga di Hello del log hello conterrà le intestazioni di colonna hello come indicato in questo esempio.
>
>

### <a name="failed-request-traces"></a>Failed Request Traces
Le tracce delle richieste non riuscite vengono memorizzate nei file XML denominati **fr######.xml**. toomake, informazioni di registrazione hello tooview più semplice, un foglio di stile XSL denominato **freb.xsl** viene fornito in hello stessa directory come file XML di hello. Apertura di uno dei file XML di hello in Internet Explorer utilizzerà tooprovide di foglio di stile XSL hello una visualizzazione formattata hello di informazioni di traccia. Questo nome verrà visualizzato simile toohello seguenti:

![richieste non riuscite, visualizzate in browser hello](./media/web-sites-enable-diagnostic-log/tws-failedrequestinbrowser.png)

### <a name="detailed-error-logs"></a>Detailed Error Logs
I log di errore dettagliati sono documenti HTML che offrono informazioni più approfondite sugli errori HTTP verificatisi. Poiché si tratta di semplici documenti HTML, è possibile visualizzarli in un browser Web.

### <a name="web-server-logs"></a>Web Server Logs
Hello i registri del server web devono essere formattati utilizzando hello [formato di file registro esteso W3C](http://msdn.microsoft.com/library/windows/desktop/aa814385.aspx). È possibile leggere queste informazioni con un editor di testo oppure analizzarle con utilità come [Log Parser](http://go.microsoft.com/fwlink/?LinkId=246619).

> [!NOTE]
> Hello i log generati dall'App web di Azure non supportano hello **s-computername**, **s-ip**, o **cs-version** campi.
>
>

## <a name="nextsteps"></a> Passaggi successivi
* [Come tooMonitor App Web](http://docs.microsoft.com/en-us/azure/app-service-web/web-sites-monitor)
* [Risoluzione dei problemi delle app Web di Azure in Visual Studio](web-sites-dotnet-troubleshoot-visual-studio.md)
* [Analisi dei log delle app Web in HDInsight](http://gallery.technet.microsoft.com/scriptcenter/Analyses-Windows-Azure-web-0b27d413)

> [!NOTE]
> Se si desidera tooget avviato con il servizio App di Azure prima di effettuare l'iscrizione per un account Azure, andare troppo[tenta di servizio App](https://azure.microsoft.com/try/app-service/), in cui è possibile creare subito un'app web di breve durata starter nel servizio App. Non è necessario fornire una carta di credito né impegnarsi in alcun modo.
>
>

## <a name="whats-changed"></a>Modifiche apportate
* Per una Guida toohello modifica da siti Web tooApp servizio vedere: [relativo impatto sui servizi di Azure esistente e servizio App di Azure](http://go.microsoft.com/fwlink/?LinkId=529714)
* Per una Guida toohello change hello vecchio portale toohello nuovo portale, vedere: [riferimento per la navigazione hello portale di Azure](http://go.microsoft.com/fwlink/?LinkId=529715)
