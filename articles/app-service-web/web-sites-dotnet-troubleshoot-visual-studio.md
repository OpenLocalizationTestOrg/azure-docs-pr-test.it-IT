---
title: aaaTroubleshoot un'app web nel servizio App di Azure con Visual Studio
description: Informazioni su come tootroubleshoot un'app web di Azure tramite debug remoto, traccia e registrazione di strumenti che vengono compilati in tooVisual Studio 2013.
services: app-service
documentationcenter: .net
author: tdykstra
manager: erikre
editor: 
ms.assetid: def8e481-7803-4371-aa55-64025d116c97
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/29/2016
ms.author: rachelap
ms.openlocfilehash: 8e3a8a58293f2ebcdc131fbf2534f8ff99b26730
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-web-app-in-azure-app-service-using-visual-studio"></a>Risoluzione dei problemi di un'app Web nel servizio app di Azure tramite Visual Studio
## <a name="overview"></a>Panoramica
Questa esercitazione viene illustrato come toouse gli strumenti di Visual Studio che consentono di eseguire il debug di un'app web nel [servizio App](http://go.microsoft.com/fwlink/?LinkId=529714), eseguendo in [modalità di debug](http://www.visualstudio.com/get-started/debug-your-app-vs.aspx) in modalità remota o visualizzando i registri applicazioni e i registri del server web.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

Si apprenderà come:

* Usare le funzioni di gestione di app Web di Azure disponibili in Visual Studio.
* Come remoto di Visual Studio toouse visualizzare modifiche rapide toomake in un'app web remoto.
* Modalità toorun modalità di debug in modalità remota durante un progetto è in esecuzione in Azure, per un'app web e per un processo Web.
* Modalità di applicazione toocreate registri di traccia e visualizzarle mentre un'applicazione hello è la loro creazione.
* Come i registri del server web tooview, tra cui messaggi di errore dettagliati e delle richieste non riuscite.
* Come diagnostica toosend Registra account di archiviazione Azure tooan e visualizzarli non esiste.

Se si dispone di Visual Studio Ultimate, è possibile usare anche [IntelliTrace](http://msdn.microsoft.com/library/vstudio/dd264915.aspx) per il debug. IntelliTrace non è illustrato in questa esercitazione.

## <a name="prerequisites"></a>Prerequisiti
In questa esercitazione funziona con l'ambiente di sviluppo hello progetto web e app web di Azure che è configurato in [Introduzione a Azure e ASP.NET][GetStarted]. Per le sezioni di processi Web hello, sarà necessario creati in un'applicazione hello [introduzione hello Azure WebJobs SDK][GetStartedWJ].

codice Hello negli esempi illustrati in questa esercitazione sono per un'applicazione web MVC c#, ma hello procedure di risoluzione dei problemi sono hello lo stesso per applicazioni Visual Basic e Web Form.

esercitazione Hello presuppone che si sta utilizzando Visual Studio 2015 o 2013. Se si utilizza Visual Studio 2013, richiedono funzionalità processi Web hello [aggiornamento 4](http://go.microsoft.com/fwlink/?LinkID=510314) o versione successiva.

i log di streaming Hello funzionalità funziona solo per le applicazioni destinate a .NET Framework 4 o versione successiva.

## <a name="sitemanagement"></a>Gestione e configurazione di app Web
Visual Studio fornisce accesso tooa subset di funzioni di gestione di hello web app e impostazioni di configurazione disponibile in hello [portale Azure](http://go.microsoft.com/fwlink/?LinkId=529715). In questa sezione verranno esaminate le opzioni disponibili tramite **Esplora server**. Provare la funzionalità toosee hello più recenti integrazione di Azure, **Cloud Explorer** anche. È possibile aprire finestre da hello **vista** menu.

1. Se non sono già eseguito tooAzure in Visual Studio, fare clic su hello **connettersi tooAzure** pulsante **Esplora Server**.

    In alternativa, è un certificato di gestione che consente di accedere a tooyour account tooinstall. Se si sceglie tooinstall un certificato, fare doppio clic su hello **Azure** nodo **Esplora Server**, quindi fare clic su **Gestisci e filtra sottoscrizioni** nel menu di scelta rapida hello. In hello **Gestisci sottoscrizioni Azure** finestra di dialogo fare clic su hello **certificati** scheda e quindi fare clic su **importazione**. Seguire toodownload direzioni hello e quindi importare un file di sottoscrizione (detto anche un *publishsettings* file) per l'account di Azure.

   > [!NOTE]
   > Se si scarica un file di sottoscrizione, salvarla come cartella tooa all'esterno delle directory del codice sorgente (ad esempio, nella cartella di download hello) e quindi eliminarlo una volta completata l'importazione di hello. Un utente malintenzionato ottiene il file di sottoscrizione toohello accesso possa modificare, creare ed eliminare i servizi di Azure.
   >
   >

    Per ulteriori informazioni sulla connessione tooAzure risorse da Visual Studio, vedere [gestire account, sottoscrizioni e ruoli amministrativi](http://go.microsoft.com/fwlink/?LinkId=324796#BKMK_AccountVCert).
2. In **Esplora server** espandere **Azure** e quindi **Servizio app**.
3. Il gruppo di risorse hello che include l'applicazione hello web creati in [Introduzione a Azure e ASP.NET][GetStarted]e quindi fare doppio clic su nodo di hello web app e fare clic su **leimpostazionidivisualizzazione**.

    ![Visualizza impostazioni in Esplora server](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-viewsettings.png)

    Hello **App Web di Azure** verrà visualizzata la scheda e si può vedere sono hello web app configurazione e Gestione attività disponibili in Visual Studio.

    ![Finestra di Azure Web App](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-configtab.png)

    In questa esercitazione sarà possibile usare la registrazione di hello e traccia elenchi a discesa. Si utilizzerà inoltre il debug remoto, ma si userà tooenable un metodo diverso è.

    Per informazioni sulle finestre di stringhe di connessione e le impostazioni dell'App hello in questa finestra, vedere [App Web di Azure: come le stringhe dell'applicazione e lavoro di stringhe di connessione](http://blogs.msdn.com/b/windowsazure/archive/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work.aspx).

    Se si desidera tooperform un'attività di gestione di app web che non può essere eseguita in questa finestra, fare clic su **Apri nel portale di gestione** tooopen un toohello finestra browser portale di Azure.

## <a name="remoteview"></a>Accedere ai file dell'app Web in Esplora server
In genere distribuisce un progetto web con hello `customErrors` flag nel set di file Web. config hello troppo`On` o `RemoteOnly`, vale a dire che è non ottenere un messaggio di errore utile quando non funziona. Per molti errori ottiene è una pagina simile a quello di hello quelli seguenti.

**Errore del server nell'applicazione '/':**

![Messaggio di errore poco utile](./media/web-sites-dotnet-troubleshoot-visual-studio/genericerror.png)

**Si è verificato un errore:**

![Messaggio di errore poco utile](./media/web-sites-dotnet-troubleshoot-visual-studio/genericerror1.png)

**Hello Impossibile visualizzare la pagina hello**

![Messaggio di errore poco utile](./media/web-sites-dotnet-troubleshoot-visual-studio/genericerror2.png)

Hello più semplice modo toofind hello causa dell'errore hello è spesso tooenable messaggi di errore dettagliati che hello prima di hello screenshot precedente illustra come toodo. Che richiede che una modifica in hello distribuiti file Web. config. È possibile modificare hello *Web. config* il file nel progetto hello e ridistribuzione hello o creare un [trasformazione Web. config](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/web-config-transformations) e distribuire una build di debug, ma non esiste un modo più rapido: in **soluzione Esplora** è direttamente possibile visualizzare e modificare i file nell'app web remota hello utilizzando hello *vista remota* funzionalità.

1. In **Esplora Server**, espandere **Azure**, espandere **servizio App**espandere hello gruppo di risorse che si trova l'app web in e quindi espandere il nodo hello per le app web.

    Vengono mostrati i nodi che consentono di creare file di contenuto e i file di log dell'app web toohello di accesso.
2. Espandere hello **file** nodo, fare doppio clic su hello *Web. config* file.

    ![Apertura di Web.config](./media/web-sites-dotnet-troubleshoot-visual-studio/webconfig.png)

    Visual Studio apre i file Web. config hello dall'app web remota hello e Mostra [remoto] nome del file toohello successivo nella barra del titolo hello.
3. Aggiungere hello seguente riga toohello `system.web` elemento:

    `<customErrors mode="Off"></customErrors>`

    ![Modifica di Web.config](./media/web-sites-dotnet-troubleshoot-visual-studio/webconfigedit.png)
4. Aggiornare il browser hello che viene visualizzato il messaggio di errore poco utile hello e ora con cui viene visualizzato un messaggio di errore dettagliato, ad esempio hello di esempio seguente:

    ![Messaggi di errore dettagliati](./media/web-sites-dotnet-troubleshoot-visual-studio/detailederror.png)

    (errore hello mostrato è stato creato aggiungendo la riga hello mostrata in rosso anche*Views\Home\Index.cshtml*.)

Modifica file Web. config di hello è solo un esempio di scenari in cui possibilità hello tooread e modificare i file nell'app web di Azure apportare risoluzione dei problemi semplificata.

## <a name="remotedebug"></a>Debug remoto di app Web
Se il messaggio di errore dettagliato hello non fornisce informazioni sufficienti e sarà possibile ricreare errore hello in locale, un altro modo tootroubleshoot è toorun in modalità di debug in modalità remota. È possibile impostare i punti di interruzione, modificare direttamente memoria, avanzare nel codice e anche modificare il percorso di codice hello.

Il debug remoto non funziona nelle edizioni Express di Visual Studio.

Questa sezione viene illustrato come progetto toodebug in remoto mediante hello creare in [Introduzione a Azure e ASP.NET][GetStarted].

1. Progetto web aperto hello creati in [Introduzione a Azure e ASP.NET][GetStarted].
2. Aprire il file *Controllers\HomeController.cs*.
3. Eliminare hello `About()` metodo e seguente hello Inserisci codice al suo posto.

        public ActionResult About()
        {
            string currentTime = DateTime.Now.ToLongTimeString();
            ViewBag.Message = "hello current time is " + currentTime;
            return View();
        }
4. [Impostare un punto di interruzione](http://www.visualstudio.com/get-started/debug-your-app-vs.aspx) su hello `ViewBag.Message` riga.
5. In **Esplora**, fare clic sul progetto hello e fare clic su **pubblica**.
6. In hello **profilo** elenco a discesa, seleziona hello stesso profilo che è stato utilizzato [Introduzione a Azure e ASP.NET][GetStarted].
7. Fare clic su hello **impostazioni** e modificare **configurazione** troppo**Debug**, quindi fare clic su **pubblica**.

    ![Pubblicazione in modalità debug](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-publishdebug.png)
8. Dopo la distribuzione al termine e il browser apre toohello Azure URL dell'app web, browser hello Chiudi.
9. In **Esplora server** fare clic con il pulsante destro del mouse sull'app Web, quindi fare clic su **Collega debugger**.

    ![Collega debugger](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-attachdebugger.png)

    browser Hello apre automaticamente tooyour home page in esecuzione in Azure. Potrebbero toowait 20 secondi o così mentre Azure Configura server hello per il debug. Questo ritardo si verifica solo hello prima esecuzione in modalità di debug in un'app web. Tutte le volte successive all'interno di hello prossime 48 ore quando si avvia nuovamente il debug vi sarà un ritardo.

    **Nota:** nel caso di problemi durante l'avvio del debugger hello, provare a toodo usando **Cloud Explorer** anziché **Esplora Server**.
10. Fare clic su **su** nel menu hello.

     Visual Studio si arresta nel punto di interruzione hello e codice hello è in esecuzione in Azure, non nel computer locale.
11. Passare il mouse su hello `currentTime` valore di ora hello toosee variabile.

     ![Visualizzazione della variabile in modalità debug in Azure](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-debugviewinwa.png)

     tempo di Hello che vedrai è ora del server Azure hello, che può essere in un fuso orario diverso nel computer locale.
12. Immettere un nuovo valore per hello `currentTime` variabile, ad esempio "In esecuzione in Azure".
13. Premere F5 toocontinue in esecuzione.

     informazioni sulla pagina in esecuzione in Azure viene visualizzato hello nuovo valore immesso nella variabile di hello currentTime.

     ![Pagina About con il nuovo valore](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-debugchangeinwa.png)

## <a name="remotedebugwj"></a> Debug remoto di processi Web
In questa sezione viene illustrato in remoto mediante l'applicazione web e progetto hello toodebug creare [introduzione hello Azure WebJobs SDK](websites-dotnet-webjobs-sdk.md).

funzionalità di Hello illustrate in questa sezione sono disponibili solo in Visual Studio 2013 con Update 4 o versione successiva.

Il debug remoto funziona solo con processi Web continui. Processi Web pianificata e su richiesta non supporta il debug.

1. Progetto web aperto hello creati in [introduzione hello Azure WebJobs SDK][GetStartedWJ].
2. Nel progetto ContosoAdsWebJob hello aprire *Functions.cs*.
3. [Impostare un punto di interruzione](http://www.visualstudio.com/get-started/debug-your-app-vs.aspx) prima istruzione di hello in hello `GnerateThumbnail` metodo.

    ![Set di punti di interruzione](./media/web-sites-dotnet-troubleshoot-visual-studio/wjbreakpoint.png)
4. In **Esplora**, fare clic sul progetto web hello (non progetto processo Web hello) e fare clic su **pubblica**.
5. In hello **profilo** elenco a discesa, seleziona hello stesso profilo che è stato utilizzato [introduzione hello Azure WebJobs SDK](websites-dotnet-webjobs-sdk.md).
6. Fare clic su hello **impostazioni** e modificare **configurazione** troppo**Debug**, quindi fare clic su **pubblica**.

    Visual Studio distribuisce web hello e progetti processi Web, e il browser apre toohello URL dell'app web di Azure.
7. In **Esplora server** espandere **Azure > Servizio app > gruppo di risorse dell'utente > App Web dell'utente > Processi Web > Continuo**, quindi fare clic con il pulsante destro del mouse su **ContosoAdsWebJob**.
8. Fare clic su **Collega debugger**.

    ![Collega debugger](./media/web-sites-dotnet-troubleshoot-visual-studio/wjattach.png)

    browser Hello apre automaticamente tooyour home page in esecuzione in Azure. Potrebbero toowait 20 secondi o così mentre Azure Configura server hello per il debug. Questo ritardo si verifica solo hello prima esecuzione in modalità di debug in un'app web. Hello successivo si collega debugger hello vi sarà un ritardo, in caso entro 48 ore.
9. Nel browser hello che corrisponde alla home page di annunci di Contoso toohello aperto, creare un nuovo annuncio.

    Creazione di un annuncio fa sì che una coda messaggi toobe creato, che verrà prelevati dal processo Web hello ed elaborati. Quando hello WebJobs SDK chiama messaggio della coda hello tooprocess funzione hello, codice hello verrà raggiunto il punto di interruzione.
10. Quando il debugger hello si interrompe al punto di interruzione, è possibile esaminare e modificare i valori delle variabili durante l'esecuzione di programma hello cloud hello. In hello debugger di hello nella figura seguente viene mostrato il contenuto di hello dell'oggetto blobInfo hello toohello GenerateThumbnail metodo passato.

     ![Oggetto blobInfo nel debugger](./media/web-sites-dotnet-troubleshoot-visual-studio/blobinfo.png)
11. Premere F5 toocontinue in esecuzione.

     metodo GenerateThumbnail Hello termina creazione anteprima hello.
12. In browser hello, pagina di indice hello aggiornamento e visualizzare l'anteprima di hello.
13. In Visual Studio, premere MAIUSC + F5 toostop debug.
14. In **Esplora Server**, fare doppio clic su nodo ContosoAdsWebJob hello e fare clic su **Dashboard View**.
15. Accedere con le credenziali di Azure e quindi fare clic su pagina toohello toogo di hello processo Web nome per il processo Web.

     ![Fare clic su ContosoAdsWebJob](./media/web-sites-dotnet-troubleshoot-visual-studio/clickcaw.png)

     Hello Dashboard Mostra tale funzione GenerateThumbnail eseguito recentemente hello.

     (hello successivo **Dashboard View**, non si dispone di toosign in e browser hello passa direttamente toohello pagina per il processo Web.)
16. Fare clic su dettagli di toosee nome funzione hello sull'esecuzione della funzione hello.

     ![Dettagli funzione](./media/web-sites-dotnet-troubleshoot-visual-studio/funcdetails.png)

Se la funzione [log scritto](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#logs), è possibile fare clic **ToggleOutput** toosee li.

## <a name="notes-about-remote-debugging"></a>Note sul debug remoto
* L'esecuzione in modalità debug in produzione non è una scelta consigliata. Se l'app web di produzione non è scalare orizzontalmente le istanze del server toomultiple, debug impedirà di server web hello risponde tooother richieste. Se non si hanno più istanze del server web, quando si collega il debugger toohello si otterrà un'istanza casuale e si dispone di tooensure alcun modo che successive browser tali richieste passano toothat istanza. Inoltre, in genere non vengono distribuiti un tooproduction build di debug e le ottimizzazioni del compilatore nelle build di rilascio potrebbero rendere impossibile tooshow ciò che accade riga per riga nel codice sorgente. Per la risoluzione dei problemi in produzione, la risorsa ottimale è costituita dai log di traccia dell'applicazione e dai log del server Web.
* Evitare interruzioni prolungate in corrispondenza dei punti di interruzione durante il debug remoto. In Azure i processi interrotti per più di alcuni minuti vengono considerati come processi che non rispondono e vengono arrestati.
* Durante il debug, hello server invia dati tooVisual Studio, che potrebbe influire sui costi di larghezza di banda. Per informazioni sui costi della larghezza di banda, vedere [Prezzi di Azure](https://azure.microsoft.com/pricing/calculator/).
* Verificare che tale hello `debug` attributo di hello `compilation` elemento hello *Web. config* file tootrue è impostato. L'impostazione è tootrue predefinito quando si pubblica una configurazione di build di debug.

        <system.web>
          <compilation debug="true" targetFramework="4.5" />
          <httpRuntime targetFramework="4.5" />
        </system.web>
* Se si ritiene che debugger hello non eseguire codice che si desidera toodebug, potrebbe essere l'impostazione di toochange hello Just My Code.  Per ulteriori informazioni, vedere [limitare l'esecuzione di istruzioni tooJust My Code](http://msdn.microsoft.com/library/vstudio/y740d9d3.aspx#BKMK_Restrict_stepping_to_Just_My_Code).
* Un timer viene avviato nel server di hello quando si attiva la funzionalità di debug remoto di hello e dopo 48 ore funzionalità hello viene disabilitata automaticamente. Questo limite di 48 ore viene impostato per motivi di sicurezza e prestazioni. In tutte le volte che si desidera, è possibile attivare facilmente funzionalità hello. È invece consigliabile lasciarla disabilitata quando non si esegue attivamente il debug.
* È possibile allegare manualmente processo tooany del debugger hello, non solo hello web app processo (w3wp.exe). Per ulteriori informazioni su come eseguire il debug in Visual Studio modalità toouse, vedere [debug in Visual Studio](http://msdn.microsoft.com/library/vstudio/sc65sadd.aspx).

## <a name="logsoverview"></a>Panoramica dei log di diagnostica
Un'applicazione ASP.NET in esecuzione in un'applicazione web di Azure è possibile creare hello seguenti tipi di registri:

* **Log di traccia dell'applicazione**<br/>
  Hello applicazione tali registri vengono creati chiamando i metodi di hello [Trace](http://msdn.microsoft.com/library/system.diagnostics.trace.aspx) classe.
* **Log del server Web**<br/>
  server web Hello crea una voce di log per ogni app di web toohello richiesta HTTP.
* **Log dei messaggi di errore dettagliati**<br/>
  server web Hello crea una pagina HTML con informazioni aggiuntive per le richieste HTTP non riuscite (quelli che generano tale codice di stato 400 o versione successiva).
* **Log di traccia delle richieste non riuscite**<br/>
  server web Hello crea un file XML con informazioni dettagliate sull'analisi per le richieste HTTP non riuscite. server web Hello fornisce inoltre un hello XSL file tooformat XML in un browser.

La registrazione influisce sulle prestazioni di app web, Azure offre hello possibilità tooenable o disabilitare ogni tipo di log in base alle esigenze. Per i log dell'applicazione, è possibile specificare che vengano creati solo quelli superiori a un determinato livello di gravità. Quando si crea una nuova app Web, per impostazione predefinita la registrazione è disabilitata.

Toofiles vengono scritti i log un *LogFiles* cartella nel file system di hello delle app web e sono accessibili tramite FTP. I registri del server Web e i registri applicazioni possono anche essere scritti tooan account di archiviazione Azure. È possibile mantenere un volume maggiore di log in un account di archiviazione rispetto a quello ottenibile nel sistema di file hello. Si è limitato tooa massimo di 100 MB di log quando si utilizza il sistema di file hello. I log del file system sono destinati solo al mantenimento a breve termine. Azure Elimina precedente spazio toomake di file di log per nuovi file una volta raggiunto il limite di hello.)  

## <a name="apptracelogs"></a>Creazione e visualizzazione dei log di traccia dell'applicazione
In questa sezione verranno eseguite hello quanto segue:

* Aggiungere funzionalità di traccia istruzioni toohello web progetto creato in [Introduzione a Azure e ASP.NET][GetStarted].
* Visualizzare i registri di hello quando si esegue il progetto hello localmente.
* Visualizzare i registri di hello come vengono generati da un'applicazione hello in esecuzione in Azure.

Per informazioni sulla modalità di registrazione applicazione toocreate in processi Web, vedere [come toowork con coda di Azure storage utilizzando hello WebJobs SDK - modalità toowrite di registrazione](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#logs). salve le istruzioni seguenti per la visualizzazione dei log e di controllare come vengono archiviati in Azure si applicano anche log tooapplication creati da processi Web.

### <a name="add-tracing-statements-toohello-application"></a>Aggiungere l'applicazione toohello istruzioni di traccia
1. Aprire *controllers\homecontroller.cs.*e sostituire hello `Index`, `About`, e `Contact` metodi con hello seguente di codice in ordine tooadd `Trace` istruzioni e un `using` istruzione per `System.Diagnostics`:

        public ActionResult Index()
        {
            Trace.WriteLine("Entering Index method");
            ViewBag.Message = "Modify this template toojump-start your ASP.NET MVC application.";
            Trace.TraceInformation("Displaying hello Index page at " + DateTime.Now.ToLongTimeString());
            Trace.WriteLine("Leaving Index method");
            return View();
        }

        public ActionResult About()
        {
            Trace.WriteLine("Entering About method");
            ViewBag.Message = "Your app description page.";
            Trace.TraceWarning("Transient error on hello About page at " + DateTime.Now.ToShortTimeString());
            Trace.WriteLine("Leaving About method");
            return View();
        }

        public ActionResult Contact()
        {
            Trace.WriteLine("Entering Contact method");
            ViewBag.Message = "Your contact page.";
            Trace.TraceError("Fatal error on hello Contact page at " + DateTime.Now.ToLongTimeString());
            Trace.WriteLine("Leaving Contact method");
            return View();
        }        
2. Aggiungere un `using System.Diagnostics;` top toohello istruzione del file hello.

### <a name="view-hello-tracing-output-locally"></a>Traccia hello visualizzazione output localmente
1. Premere F5 toorun un'applicazione hello in modalità di debug.

    listener di traccia predefinito Hello scrive tutti toohello di output di traccia **Output** finestra altro output di Debug. Hello nella figura seguente Mostra output di hello dalla hello istruzioni di traccia che è stato aggiunto toohello `Index` metodo.

    ![Visualizzazione dell'output di traccia nella finestra Debug](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-debugtracing.png)

    Hello alla procedura seguente viene illustrato come output di traccia tooview in una pagina web, senza la compilazione in modalità di debug.
2. Aprire Web. config dell'applicazione hello (Buongiorno uno si trova nella cartella di progetto hello) e aggiungere un `<system.diagnostics>` elemento alla fine di hello del file hello prima parentesi di chiusura hello `</configuration>` elemento:

          <system.diagnostics>
            <trace>
              <listeners>
                <add name="WebPageTraceListener"
                    type="System.Web.WebPageTraceListener,
                    System.Web,
                    Version=4.0.0.0,
                    Culture=neutral,
                    PublicKeyToken=b03f5f7f11d50a3a" />
              </listeners>
            </trace>
          </system.diagnostics>

    Hello `WebPageTraceListener` output di traccia consente di visualizzare esplorando troppo`/trace.axd`.
3. Aggiungere un <a href="http://msdn.microsoft.com/library/vstudio/6915t83k(v=vs.100).aspx">elemento trace</a> in `<system.web>` nel file Web. config hello, ad esempio hello di esempio seguente:

        <trace enabled="true" writeToDiagnosticsTrace="true" mostRecent="true" pageOutput="false" />
4. Premere CTRL + F5 toorun un'applicazione hello.
5. Nella barra degli indirizzi hello hello finestra del browser aggiungere *trace.axd* toohello URL, quindi premere INVIO (hello URL sarà simile toohttp://localhost:53370/trace.axd).
6. In hello **traccia dell'applicazione** pagina, fare clic su **Visualizza dettagli** hello della prima riga (non hello BrowserLink riga).

    ![trace.axd](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-traceaxd1.png)

    Hello **dettagli richiesta** verrà visualizzata la pagina e in hello **informazioni di traccia** sezione è visualizzato l'output di hello di istruzioni di traccia hello aggiunto toohello `Index` metodo.

    ![trace.axd](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-traceaxd2.png)

    Per impostazione predefinita, `trace.axd` è disponibile solo in locale. Se si desidera toomake è disponibile da un'app web remoto, è possibile aggiungere `localOnly="false"` toohello `trace` elemento hello *Web. config* file, come illustrato nell'esempio seguente hello:

        <trace enabled="true" writeToDiagnosticsTrace="true" localOnly="false" mostRecent="true" pageOutput="false" />

    Tuttavia, l'attivazione `trace.axd` in un ambiente di produzione app web è in genere sconsigliato per motivi di sicurezza e hello nelle sezioni che seguono si noterà un tooread modo più semplice in un'applicazione web di Azure log di traccia.

### <a name="view-hello-tracing-output-in-azure"></a>Visualizzazione dell'output di traccia hello in Azure
1. In **Esplora**, fare clic sul progetto web hello e fare clic su **pubblica**.
2. In hello **pubblica sul Web** la finestra di dialogo, fare clic su **pubblica**.

    Dopo Visual Studio consente di pubblicare l'aggiornamento, si apre una home page del browser finestra tooyour (presupponendo che non sono state deselezionate **URL di destinazione** su hello **connessione** scheda).
3. In **Esplora server** fare clic con il pulsante destro del mouse sull'app Web e selezionare **Visualizza log in streaming**.

    ![View Streaming Logs nel menu di scelta rapida](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-viewlogsmenu.png)

    Hello **Output** Mostra finestra che si è connesso toohello basate sul flusso di log del servizio e aggiunge una riga di notifica per ogni minuto che va senza toodisplay un log.

    ![View Streaming Logs nel menu di scelta rapida](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-nologsyet.png)
4. Nella finestra del browser hello che mostra la home page dell'applicazione, fare clic su **contatto**.

    Entro pochi secondi hello, l'output di traccia a livello di errore hello aggiunto toohello `Contact` metodo appare in hello **Output** finestra.

    ![Traccia di errore nella finestra Output](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-errortrace.png)

    Visual Studio verrà visualizzati solo le tracce a livello di errore perché è l'impostazione predefinita di hello quando si abilita il log di hello monitoraggio del servizio. Quando si crea una nuova app web di Azure, tutte le registrazioni sono disabilitato per impostazione predefinita, come visto quando aperta la pagina Impostazioni di hello in precedenza:

    ![Registrazione dell'applicazione disabilitata](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-apploggingoff.png)

    Tuttavia, se è selezionata **Visualizza log di Streaming**, verrà automaticamente modificato **applicazione Logging(File System)** troppo**errore**, ovvero i log a livello di errore vengono restituite. In ordine toosee tutti i log di traccia, è possibile modificare questa impostazione troppo**Verbose**. Quando si seleziona un livello di gravità inferiore a errore, vengono segnalati anche tutti i log per livelli di gravità superiori. Quindi se si seleziona Verbose verranno visualizzati anche i log di informazioni, avvisi ed errori.  

1. In **Esplora Server**, fare doppio clic su hello web app e quindi fare clic su **le impostazioni di visualizzazione** come fatto in precedenza.
2. Modifica **registrazione delle applicazioni (File System)** troppo**Verbose**, quindi fare clic su **salvare**.

    ![Impostazione tooVerbose livello di traccia](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-applogverbose.png)
3. Nella finestra del browser hello che risulta ora il **contatto** pagina, fare clic su **Home**, quindi fare clic su **su**e quindi fare clic su **contatto**.

    Entro pochi secondi, hello **Output** finestra vengono mostrati tutti di output di traccia.

    ![Output di traccia dettagliato](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-verbosetraces.png)

    In questa sezione è stato illustrato come abilitare e disabilitare la registrazione tramite le impostazioni dell'app Web di Azure. È inoltre possibile abilitare e disabilitare i listener di traccia modificando il file di Web. config hello. Tuttavia, modifica file Web. config hello determina hello app dominio toorecycle, durante l'abilitazione della registrazione tramite la configurazione di app web hello non che. Se il problema di hello accetta un tooreproduce molto tempo o è intermittente, il riciclo del dominio dell'applicazione hello potrebbe essere "risolvere" e forzare toowait fino a quando non si verifica nuovamente. Se invece si abilita la diagnostica in Azure, è possibile evitare questa situazione e iniziare immediatamente ad acquisire informazioni sugli errori.

### <a name="output-window-features"></a>Funzionalità della finestra Output
Hello **i log di Azure** scheda di hello **Output** finestra dispone di più pulsanti e una casella di testo:

![Pulsanti della scheda Logs](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-icons.png)

Questi eseguire hello seguenti funzioni:

* Crittografato hello **Output** finestra.
* Abilitare o disabilitare il ritorno a capo automatico.
* Avviare o interrompere il monitoraggio dei log.
* Specificare quali registri toomonitor.
* Scaricare i log.
* Filtrare i log in base a una stringa di ricerca o a un'espressione regolare.
* Chiude hello **Output** finestra.

Se si immette una stringa di ricerca o un'espressione regolare, Visual Studio consente di filtrare le informazioni di registrazione client hello. Pertanto, è possibile immettere criteri hello dopo hello registri vengono visualizzati nel hello **Output** finestra ed è possibile modificare i criteri di filtro senza tooregenerate hello registri.

## <a name="webserverlogs"></a>Visualizzazione dei log del server Web
I registri del server Web registrano tutte le attività HTTP per l'app web hello. In ordine toosee nel hello **Output** finestra è tooenable per hello app web e indicare a Visual Studio che si desidera toomonitor li.

1. In hello **configurazione di App Web di Azure** scheda che è stato aperto da **Esplora Server**, modificare la registrazione di Server Web troppo**su**e quindi fare clic su **salvare**.

    ![Abilitazione della registrazione del server Web](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-webserverloggingon.png)
2. In hello **Output** finestra, fare clic su hello **specificare quali toomonitor i log di Azure** pulsante.

    ![Specificare quali toomonitor i log di Azure](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-specifylogs.png)
3. In hello **opzioni di registrazione di Azure** nella finestra di dialogo **i registri del server Web**, quindi fare clic su **OK**.

    ![Monitoraggio dei log del server Web](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-monitorwslogson.png)
4. Nella finestra del browser hello che mostra hello web app, fare clic su **Home**, quindi fare clic su **su**, quindi fare clic su **contatto**.

    log applicazioni Hello in genere visualizzati per primi, seguito da hello i registri del server web. Potrebbe essere toowait un po' di tempo per hello registra tooappear.

    ![Log del server Web nella finestra Output](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-wslogs.png)

Per impostazione predefinita, quando si attiva prima i registri del server web con Visual Studio, Azure scrive hello registri toohello file system. In alternativa, è possibile utilizzare hello Azure toospecify portale che i registri del server web deve essere scritto tooa contenitore di blob in un account di archiviazione.

Se si Usa server web di tooenable portale hello registrazione tooan account di archiviazione Azure e quindi disabilitare la registrazione in Visual Studio, quando si riabilita la registrazione in Visual Studio vengono ripristinate le impostazioni dell'account di archiviazione.

## <a name="detailederrorlogs"></a>Visualizzare i log dei messaggi di errore dettagliati
I log dei messaggi di errore dettagliati forniscono informazioni aggiuntive sulle richieste HTTP che generano codici di risposta di errore (400 o superiore). In ordine toosee nel hello **Output** finestra è tooenable per hello app web e indicare a Visual Studio che si desidera toomonitor li.

1. In hello **configurazione di App Web di Azure** scheda in cui è stato aperto da **Esplora Server**, modificare **messaggi di errore dettagliati** troppo**su**, e quindi fare clic su **salvare**.

    ![Abilitazione dei messaggi di errore dettagliati](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-detailedlogson.png)
2. In hello **Output** finestra, fare clic su hello **specificare quali toomonitor i log di Azure** pulsante.
3. In hello **opzioni di registrazione di Azure** la finestra di dialogo, fare clic su **tutti i log**, quindi fare clic su **OK**.

    ![Monitoraggio di tutti i log](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-monitorall.png)
4. Nella barra degli indirizzi hello hello finestra del browser, aggiungere un toocause di URL toohello carattere aggiuntivo 404 errore (ad esempio, `http://localhost:53370/Home/Contactx`), quindi premere INVIO.

    Dopo alcuni secondi hello registro dettagliato degli errori viene visualizzato in Visual Studio hello **Output** finestra.

    ![Log dei messaggi di errore dettagliati nella finestra Output](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-detailederrorlog.png)

    CTRL + clic su hello collegamento toosee hello log output formattato in un browser:

    ![Log dei messaggi di errore dettagliati in una finestra del browser](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-detailederrorloginbrowser.png)

## <a name="downloadlogs"></a>Download dei log del file system
Tutti i log che è possibile monitorare in hello **Output** finestra può essere scaricata anche come un *zip* file.

1. In hello **Output** finestra, fare clic su **scaricare i log di Streaming**.

    ![Pulsanti della scheda Logs](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-downloadicon.png)

    Esplora file verrà aperto tooyour *Scarica* cartella con hello download del file selezionato.

    ![File scaricato](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-downloadedfile.png)
2. Estrarre hello *zip* file e si vedere hello seguente struttura di cartelle:

    ![File scaricato](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-logfilefolders.png)

   * I log di traccia di applicazioni sono *. txt* file hello *LogFiles\Application* cartella.
   * Log del server Web sono *log* file hello *LogFiles\http\RawLogs* cartella. È possibile utilizzare uno strumento come [Log Parser](http://www.microsoft.com/download/details.aspx?displaylang=en&id=24659) tooview e modificare questi file.
   * I log dei messaggi di errore dettagliati sono *HTML* file hello *LogFiles\DetailedErrors* cartella.

     (hello *distribuzioni* cartella è per i file creati dal controllo del codice sorgente pubblicazione; non dispone di pubblicazione Studio tooVisual nulla correlati. Hello *Git* cartella è per le tracce correlate toosource controllo pubblicazione hello file di registro e servizio di streaming.)  

## <a name="storagelogs"></a>Visualizzare i log di archiviazione
Registri di traccia delle applicazioni possono anche essere inviati tooan account di archiviazione di Azure ed è possibile visualizzarli in Visual Studio. toodo che si sarà creare un account di archiviazione, abilitare i log di archiviazione nel portale classico hello e visualizzarli in hello **registri** scheda di hello **App Web di Azure** finestra.

È possibile inviare i log tooany o tutti i tre destinazioni:

* sistema di file Hello.
* Tabelle dell'account di archiviazione.
* BLOB dell'account di archiviazione.

È possibile specificare un livello di gravità diverso per ogni destinazione.

Tabelle rendono tooview facilmente i dettagli dei log online e supportano il flusso; è possibile eseguire una query log nelle tabelle e vedere i nuovi log come la creazione. BLOB rendono toodownload semplice log nei file e tooanalyze loro tramite HDInsight, poiché HDInsight sa come toowork con archiviazione blob. Per altre informazioni, vedere la sezione relativa a **Hadoop e MapReduce** nell'articolo sulle [opzioni di archiviazione dati durante la creazione di app per cloud funzionanti](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-storage-options).

Si dispone attualmente di livello di file system registri set tooverbose; Hello passaggi seguenti consentono la configurazione delle tabelle di informazioni sui registri livello toogo toostorage account. In questo modo verranno visualizzati tutti i log creati chiamando `Trace.TraceInformation`, `Trace.TraceWarning` e `Trace.TraceError`, ma non quelli creati chiamando `Trace.WriteLine`.

Gli account di archiviazione offrono che ulteriori conservazione di più a lungo per i log e di archiviazione rispetto a system file toohello. Un altro vantaggio dell'applicazione mittente toostorage i registri di traccia è che si ottengano informazioni aggiuntive con ogni log da cui non si ottiene dal Registro di sistema di file.

1. Fare doppio clic su **archiviazione** in hello nodo di Azure e quindi fare clic su **crea Account di archiviazione**.

![Crea account di archiviazione](./media/web-sites-dotnet-troubleshoot-visual-studio/createstor.png)

1. In hello **crea Account di archiviazione** finestra di dialogo immettere un nome per l'account di archiviazione hello.

    nome Hello deve essere univoco (nessun altro account di archiviazione di Azure può avere hello stesso nome). Se specifica un nome hello è già in uso, si otterrà un toochange possibilità è.

    Hello tooaccess URL l'account di archiviazione sarà *{nome}*. c.
2. Set hello **regione o gruppo di affinità** riepilogo toohello area più vicina tooyou.

    Questa impostazione specifica il data center di Azure che ospiterà l'account di archiviazione. Per questa esercitazione la scelta non creare una differenza notevole, ma per un'app web di produzione si desidera che il server web e il toobe di account di archiviazione in hello stesso latenza toominimize di area e i dati in uscita addebiti. app web Hello (che verrà creato in un secondo momento) deve essere eseguito in un'area più vicino possibile toohello browser l'accesso a un'applicazione web della latenza toominimize ordine.
3. Set hello **replica** elenco a discesa elenco troppo**ridondanza locale**.
   
    Quando la replica geografica è abilitata per un account di archiviazione, il contenuto di hello archiviato è posizione tooa replicati Data Center secondario tooenable failover toothat in caso di un errore grave nella posizione primaria hello. La replica geografica può comportare costi aggiuntivi. Per gli account di sviluppo e test, in genere non si desidera toopay per la replica geografica. Per altre informazioni, vedere la pagina relativa alla [creazione, gestione o eliminazione di un account di archiviazione](../storage/common/storage-create-storage-account.md).
4. Fare clic su **Crea**.

    ![Nuovo account di archiviazione](./media/web-sites-dotnet-troubleshoot-visual-studio/newstorage.png)    
5. In Visual Studio hello **App Web di Azure** finestra, fare clic su hello **registri** scheda e quindi fare clic su **configurare la registrazione nel portale di gestione**.

    <!-- todo:screenshot of new portal if hello VS page link goes toonew portal -->
    ![Configurare la registrazione](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-configlogging.png)

    Verrà visualizzata hello **configura** scheda nel portale classico di hello per le app web.
6. In un portale classico hello **configura** , scorrere verso il basso toohello sezione di diagnostica di applicazioni e quindi modificare **registrazione delle applicazioni (archiviazione tabella)** troppo**su**.
7. Modifica **livello di registrazione** troppo**informazioni**.
8. Fare clic su **Manage Table Storage**.

    ![Selezione di Manage TableStorage](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-stgsettingsmgmtportal.png)

    In hello **Gestisci archiviazione tabella per diagnostica applicazioni** casella, è possibile scegliere l'account di archiviazione se si dispone di più di uno. È possibile creare una nuova tabella o utilizzarne una esistente.

    ![Manage Table Storage](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-choosestorageacct.png)
9. In hello **Gestisci archiviazione tabella per diagnostica applicazioni** casella casella hello segno di spunta tooclose hello.
10. In un portale classico hello **configura** scheda, fare clic su **salvare**.
11. Nella finestra del browser hello che visualizza hello applicazione web app, fare clic su **Home**, quindi fare clic su **su**, quindi fare clic su **contatto**.

     informazioni di registrazione Hello prodotte esplorando le pagine web verranno scritto toohello account di archiviazione.
12. In hello **registri** scheda di hello **App Web di Azure** finestra in Visual Studio, fare clic su **aggiornamento** in **riepilogo diagnostica**.

     ![Selezione di Refresh](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-refreshstorage.png)

     Hello **riepilogo diagnostica** sezione illustra i registri per hello ultimi 15 minuti per impostazione predefinita. È possibile modificare toosee periodo hello più log.

     (Se si verifica un errore di "tabella non trovato", verificare che si esplorare pagine toohello hello traccia dopo aver abilitato **registrazione delle applicazioni (archiviazione)** e dopo avere scelto **salvare**.)

     ![Log di archiviazione](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-storagelogs.png)

     Si noti che in questa vista vedere **ID processo** e **ID Thread** per ogni log, che non si ottiene i registri di sistema di file hello. È possibile visualizzare i campi aggiuntivi visualizzando direttamente nella tabella di archiviazione Azure hello.
13. Fare clic su **View all application logs**.

     tabella del log di traccia Hello viene visualizzato in Visualizzatore di tabelle di archiviazione di Azure hello.

     (Se si verifica un errore "sequenza non contiene elementi", aprire **Esplora Server**, espandere il nodo hello dell'account di archiviazione in hello **Azure** nodo e quindi rapida **tabelle**e fare clic su **aggiornamento**.)

     ![Log di archiviazione in visualizzazione tabella](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-tracelogtableview.png)

     Questa visualizzazione contiene campi aggiuntivi non disponibili nelle altre visualizzazioni. Questa vista consente inoltre i registri toofilter tramite interfaccia utente di generatore Query speciale per la creazione di una query. Per ulteriori informazioni, vedere la sezione Utilizzo delle risorse tabella - Filtro delle entità in [Esplorazione delle risorse di archiviazione con Esplora server](http://msdn.microsoft.com/library/ff683677.aspx).
14. toolook dettagli hello per una singola riga, fare doppio clic su una delle righe hello.

     ![Tabella di tracce in Esplora server](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-tracetablerow.png)

## <a name="failedrequestlogs"></a>Visualizzare i log di traccia delle richieste non riuscite
Registri di traccia delle richieste non riuscite sono utili quando è necessario dettagli hello toounderstand di IIS gestisce come una richiesta HTTP, in scenari, ad esempio problemi di autenticazione o di riscrittura degli URL.

Hello uso di App web di Azure stesso non è stato possibile richiedere la funzionalità di traccia che è stata disponibile con IIS 7.0 e versioni successive. Non è tuttavia le impostazioni di IIS che consentono di configurare gli errori vengono registrate, toohello di accesso. Quando si abilita la traccia delle richieste non riuscite, vengono acquisiti tutti gli errori.

È possibile abilitare la traccia delle richieste non riuscite mediante Visual Studio, ma non è possibile visualizzarle in Visual Studio. I log sono file in formato XML. Hello streaming solo il servizio di registrazione consente di monitorare i file che sono considerati come leggibili in modalità testo normale: *. txt*, *HTML*, e *log* file.

È possibile visualizzare i registri di traccia delle richieste non riuscite in un browser direttamente tramite FTP o in locale dopo l'utilizzo di un toodownload strumento FTP li tooyour computer locale. In questa sezione verrà illustrato come visualizzarli direttamente in un browser.

1. In hello **configurazione** scheda di hello **App Web di Azure** finestra aperta da **Esplora Server**, modificare **traccia richieste non riuscite**troppo**su**, quindi fare clic su **salvare**.

    ![Abilitazione della traccia delle richieste non riuscite](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-failedrequeston.png)
2. Nella barra degli indirizzi hello della finestra del browser hello che mostra l'app web hello, aggiungere un URL toohello carattere aggiuntivo e fare clic su invio toocause un errore 404.

    In questo modo un toobe di log di traccia richieste non riuscite creato e hello passaggi seguenti viene illustrato come tooview o download hello log.
3. In Visual Studio, in hello **configurazione** scheda di hello **App Web di Azure** finestra, fare clic su **Apri nel portale di gestione**.
4. In hello [portale Azure](https://portal.azure.com) **impostazioni** pannello per l'app web, fare clic su **le credenziali di distribuzione**, quindi immettere un nuovo nome utente e una password.

    ![Nuovo nome utente e nuova password FTP](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-enterftpcredentials.png)

    * * Quando si accede, è necessario toouse hello nome completo dell'utente con nome prefisso tooit di hello web app. Ad esempio, se si immette "MioID" come nome utente e il sito di hello è "myexample", accedere come "myexample\myid".
5. In una nuova finestra del browser, passare l'URL toohello visualizzata sotto **nome host FTP** o **nome host FTPS** in hello **App Web** pannello per l'app web.
6. Accedere utilizzando le credenziali di hello FTP è stato creato in precedenza (inclusi hello web app nome prefisso per il nome utente hello).

    browser Hello Mostra cartella radice hello dell'app web hello.
7. Aprire hello *LogFiles* cartella.

    ![Apertura della cartella LogFiles.](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-logfilesfolder.png)
8. Aprire una cartella hello denominata W3SVC più di un valore numerico.

    ![Apertura della cartella W3SVC](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-w3svcfolder.png)

    cartella Hello contiene il file XML per individuare eventuali errori che sono stati registrati dopo aver abilitato la traccia richieste non riuscite e un file XSL usato un browser tooformat hello XML.

    ![Cartella W3SVC](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-w3svcfoldercontents.png)
9. Fare clic su file XML di hello per richieste non riuscite hello che si desiderano toosee le informazioni relative.

    Hello nella figura seguente viene illustrata parte hello di informazioni di traccia per un errore di esempio.

    ![Traccia delle richieste non riuscite nel browser](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-failedrequestinbrowser.png)

## <a name="nextsteps"></a>Passaggi successivi
Si è visto come Visual Studio rende facile tooview log creati da un'app web di Azure. Hello sezioni seguenti forniscono collegamenti alle risorse toomore in argomenti correlati:

* Risoluzione dei problemi relativi alle app Web di Azure
* Debug in Visual Studio
* Debug remoto in Azure
* Traccia nelle applicazioni ASP.NET
* Analisi dei log del server Web
* Analisi dei log di traccia delle richieste non riuscite
* Debug di Servizi cloud

### <a name="azure-web-app-troubleshooting"></a>Risoluzione dei problemi relativi alle app Web di Azure
Per ulteriori informazioni sulla risoluzione dei problemi di App web nel servizio App di Azure, vedere hello seguenti risorse:

* [Come le app web toomonitor](/manage/services/web-sites/how-to-monitor-websites/)
* [Analisi delle perdite di memoria in App Web di Azure con Visual Studio 2013](http://blogs.msdn.com/b/visualstudioalm/archive/2013/12/20/investigating-memory-leaks-in-azure-web-sites-with-visual-studio-2013.aspx). Post del blog di Microsoft ALM sulle funzionalità di Visual Studio per l'analisi dei problemi relativi alla memoria gestita.
* [Strumenti online di App Web di Azure che è necessario conoscere](https://azure.microsoft.com/blog/2014/03/28/windows-azure-websites-online-tools-you-should-know-about-2/). Post del blog di Amit Apple.

Per informazioni sulla risoluzione dei problemi domande specifiche, avviare un thread in uno dei seguenti forum hello:

* [forum di Azure nel sito ASP.NET hello Hello](http://forums.asp.net/1247.aspx/1?Azure+and+ASP+NET).
* [forum di Azure su MSDN Hello](http://social.msdn.microsoft.com/Forums/windowsazure/).
* [StackOverflow.com](http://www.stackoverflow.com).

### <a name="debugging-in-visual-studio"></a>Debug in Visual Studio
Per ulteriori informazioni su come eseguire il debug in Visual Studio modalità toouse, vedere hello [debug in Visual Studio](http://msdn.microsoft.com/library/vstudio/sc65sadd.aspx) argomento MSDN e [suggerimenti per il debug con Visual Studio 2010](http://weblogs.asp.net/scottgu/archive/2010/08/18/debugging-tips-with-visual-studio-2010.aspx).

### <a name="remote-debugging-in-azure"></a>Debug remoto in Azure
Per ulteriori informazioni sul debug remoto per App web di Azure e i processi Web, vedere hello seguenti risorse:

* [Introduzione tooRemote debug Azure App Web del servizio app](https://azure.microsoft.com/blog/2014/05/06/introduction-to-remote-debugging-on-azure-web-sites/).
* [Introduzione tooRemote debug Azure App Web del servizio App parte 2 - all'interno di debug remoto](https://azure.microsoft.com/blog/2014/05/07/introduction-to-remote-debugging-azure-web-sites-part-2-inside-remote-debugging/)
* [Introduzione tooRemote debug da parte dell'App Web di servizio App di Azure 3 - ambiente multi-istanza e GIT](https://azure.microsoft.com/blog/2014/05/08/introduction-to-remote-debugging-on-azure-web-sites-part-3-multi-instance-environment-and-git/)
* [Debug di processi Web (video)](https://www.youtube.com/watch?v=ncQm9q5ZFZs&list=UU_SjTh-ZltPmTYzAybypB-g&index=1)

Se l'app web utilizza un back-end servizi mobili o di API Web di Azure ed è necessario toodebug che, vedere [debug back-end .NET in Visual Studio](http://blogs.msdn.com/b/azuremobile/archive/2014/03/14/debugging-net-backend-in-visual-studio.aspx).

### <a name="tracing-in-aspnet-applications"></a>Traccia nelle applicazioni ASP.NET
Non esistono alcun tooASP.NET introduzioni completo e aggiornato traccia disponibile in hello Internet. Hello migliore è possibile eseguire è introduzione precedente materiale introduttivi scritti per Web Form perché non esiste ancora, MVC e che integrano con blog più recenti post che lo stato attivo su problemi specifici. Alcuni toostart valide sono hello seguenti risorse:

* [Monitoraggio e telemetria (creazione di app per cloud funzionanti con Azure)](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry).<br>
  Capitolo di un e-book con suggerimenti per la traccia nelle applicazioni per cloud di Azure.
* [Traccia in ASP.NET](http://msdn.microsoft.com/library/ms972204.aspx)<br/>
  Precedente, ma ancora un'ottima risorsa per l'oggetto toohello introduzione di base.
* [Listener di traccia](http://msdn.microsoft.com/library/4y5y10s7.aspx)<br/>
  Informazioni sui listener di traccia, ma non fanno riferimento ad hello [WebPageTraceListener](http://msdn.microsoft.com/library/system.web.webpagetracelistener.aspx).
* [Procedura detagliata: integrazione della traccia ASP.NET con la traccia System.Diagnostics](http://msdn.microsoft.com/library/b0ectfxd.aspx)<br/>
  Questo troppo vecchio, ma include alcune informazioni aggiuntive non copre tale articolo introduttivo hello.
* [Traccia nelle visualizzazioni Razor ASP.NET MVC](http://blogs.msdn.com/b/webdev/archive/2013/07/16/tracing-in-asp-net-mvc-razor-views.aspx)<br/>
  Oltre alle funzionalità di traccia nelle visualizzazioni Razor, post hello viene inoltre illustrato come filtrare toocreate un errore in ordine toolog eccezioni tutti non gestite in un'applicazione MVC. Per informazioni su come non gestite toolog tutte le eccezioni in un'applicazione Web Form, vedere l'esempio di Global. asax hello in [un esempio completo per i gestori degli errori](http://msdn.microsoft.com/library/bb397417.aspx) su MSDN. In MVC o Web Form, se si desidera toolog determinate eccezioni, ma consentire framework predefinito hello gestisce l'effetto, è possibile intercettare e generi di nuovo come hello di esempio seguente:

        try
        {
           // Your code that might cause an exception toobe thrown.
        }
        catch (Exception ex)
        {
            Trace.TraceError("Exception: " + ex.ToString());
            throw;
        }
* [Il flusso di registrazione di traccia di diagnostica da riga di comando di Azure hello (più sguardo rapido!)](http://www.hanselman.com/blog/StreamingDiagnosticsTraceLoggingFromTheAzureCommandLinePlusGlimpse.aspx)<br/>
  Come toouse hello toodo riga di comando quali questa esercitazione viene illustrato come toodo in Visual Studio. [Glimpse](http://www.hanselman.com/blog/IfYoureNotUsingGlimpseWithASPNETForDebuggingAndProfilingYoureMissingOut.aspx) è uno strumento per il debug di applicazioni ASP.NET.
* [Utilizzo delle funzionalità di registrazione e diagnostica di app Web - con David Ebbo](/documentation/videos/azure-web-site-logging-and-diagnostics/) e [Streaming dei log da app Web - con David Ebbo](/documentation/videos/log-streaming-with-azure-web-sites/)<br>
  Video con David Ebbo, di Scott Hanselman e David Ebbo.

Per la registrazione degli errori, un'alternativa toowriting il proprio codice di traccia è il framework registrazione toouse open source, ad esempio [ELMAH](http://nuget.org/packages/elmah/). Per ulteriori informazioni, vedere i [post di blog di Scott Hanselman su ELMAH](http://www.hanselman.com/blog/NuGetPackageOfTheWeek7ELMAHErrorLoggingModulesAndHandlersWithSQLServerCompact.aspx).

Si noti inoltre che non si dispone di toouse ASP.NET o i log di traccia System. Diagnostics se si desidera tooget streaming da Azure. Hello app web di Azure, servizio di log di streaming trasmetterà qualsiasi *. txt*, *HTML*, o *log* file che si trova in hello *LogFiles* cartella. Pertanto, è possibile creare il sistema di registrazione che scrive toohello file system dell'app web hello e il file verrà automaticamente trasmesso e scaricato. Toodo è scrivere il codice di applicazione che crea i file in hello *d:\home\logfiles* cartella.

### <a name="analyzing-web-server-logs"></a>Analisi dei log del server Web
Per ulteriori informazioni sull'analisi dei log del server, vedere hello seguenti risorse:

* [LogParser](http://www.microsoft.com/download/details.aspx?id=24659)<br/>
  Strumento per la visualizzazione di dati nei log del server Web (file con estensione*log* ).
* [Risoluzione dei problemi di prestazioni di IIS o di errori dell'applicazione mediante Log Parser ](http://www.iis.net/learn/troubleshoot/performance-issues/troubleshooting-iis-performance-issues-or-application-errors-using-logparser)<br/>
  Introduzione toohello Log Parser strumento che è possibile utilizzare un server web tooanalyze Registra.
* [Post di blog di Robert McMurray sull'uso di Log Parser](http://blogs.msdn.com/b/robert_mcmurray/archive/tags/logparser/)<br/>
* [codice di stato HTTP in IIS 7.0, IIS 7.5 e IIS 8.0 Hello](http://support.microsoft.com/kb/943891)

### <a name="analyzing-failed-request-tracing-logs"></a>Analisi dei log di traccia delle richieste non riuscite
sito Web Microsoft TechNet Hello include un [utilizzando traccia richieste non riuscite](http://www.iis.net/learn/troubleshoot/using-failed-request-tracing) sezione in cui può essere utile per comprendere come toouse questi registri. Tuttavia, questa documentazione è incentrata principalmente sulla configurazione della traccia delle richieste non riuscite in IIS, che non è possibile eseguire in App Web di Azure.

[GetStarted]: app-service-web-get-started-dotnet.md
[GetStartedWJ]: websites-dotnet-webjobs-sdk.md
