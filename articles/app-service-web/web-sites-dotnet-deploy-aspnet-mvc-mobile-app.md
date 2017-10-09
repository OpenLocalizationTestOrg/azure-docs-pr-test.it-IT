---
title: app web per dispositivi mobili aaaDeploy un MVC ASP.NET 5 in Azure App Service
description: "Un'esercitazione che illustra come funzionalità toodeploy un tooAzure app web del servizio App tramite dispositivi mobili in ASP.NET MVC 5 applicazione web."
services: app-service
documentationcenter: .net
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: 0752c802-8609-4956-a755-686116913645
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/12/2016
ms.author: cephalin
ms.openlocfilehash: 01119c07246c0252fd357562774a2e90b3ef77d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-aspnet-mvc-5-mobile-web-app-in-azure-app-service"></a>Distribuzione di un'app Web ASP.NET MVC 5 per dispositivi mobili nel servizio app di Azure
Questa esercitazione verrà illustrato è hello nozioni di base di ricerca toobuild un MVC ASP.NET 5 web app mobile descrittivi e distribuirlo tooAzure servizio App. Per questa esercitazione, è necessario [Visual Studio Express 2013 per Web] [ Visual Studio Express 2013] hello versione o professional di Visual Studio se si dispone già di. È possibile utilizzare [Visual Studio 2015] ma catture di schermata hello saranno diversi ed è necessario utilizzare modelli di hello ASP.NET 4. x.

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="what-youll-build"></a>Scopo dell'esercitazione
Per questa esercitazione si aggiungerà funzionalità mobili toohello conferenza listato applicazione semplice che viene fornito nella hello [progetto iniziale][StarterProject]. Hello schermata seguente mostra le sessioni ASP.NET hello in un'applicazione hello completata, come illustrato nell'emulatore di browser hello negli strumenti di sviluppo F12 di Internet Explorer 11.

![][FixedSessionsByTag]

È possibile utilizzare gli strumenti di sviluppo F12 di Internet Explorer 11 hello e hello [strumento Fiddler] [ Fiddler] toohelp il debug dell'applicazione. 

## <a name="skills-youll-learn"></a>Acquisizione di competenze
In questa esercitazione si apprenderà:

* Come toopublish toouse Visual Studio 2013 l'applicazione web direttamente tooa app web in Azure App Service.
* Utilizzano modelli ASP.NET MVC 5 hello framework Bootstrap CSS hello per migliorare la visualizzazione su dispositivi mobili
* Come toocreate mobile specifiche viste tootarget specifico browser per dispositivi mobili, come iPhone hello e Android
* Come toocreate reattiva viste (viste che rispondono toodifferent browser tra i dispositivi)

## <a name="set-up-hello-development-environment"></a>Configurare un ambiente di sviluppo hello
Configurare l'ambiente di sviluppo installando hello Azure SDK per .NET 2.5.1 o versione successiva. 

1. tooinstall hello Azure SDK per .NET, fare clic su collegamento hello riportato di seguito. Se non si dispone di Visual Studio 2013, è ancora stato installato, si verrà installato dal collegamento hello. Per completare questa esercitazione, è necessario disporre di Visual Studio 2013. [Azure SDK per Visual Studio 2013][AzureSDKVs2013]
2. Nella finestra di installazione guidata piattaforma Web hello, fare clic su **installare** e continuare l'installazione di hello.

Sarà inoltre necessario disporre di un emulatore del browser per dispositivi mobili. Uno dei seguenti hello funzionerà:

* Emulatore di browser disponibile negli [strumenti di sviluppo F12 di Internet Explorer 11][EmulatorIE11] (usato in tutte le schermate del browser per dispositivi mobili). Dispone di set di impostazioni della stringa agente utente per Windows Phone 8, Windows Phone 7 e Apple iPad.
* Emulatore di browser disponibile in [Google Chrome DevTools][EmulatorChrome]. Sono disponibili set di impostazioni per diversi dispositivi Android, oltre che per Apple iPhone, Apple iPad e Amazon Kindle Fire. Emula anche gli eventi tocco.
* [Emulatore mobile di Opera][EmulatorOpera]

Progetti di Visual Studio c\# codice sorgente sono tooaccompany disponibili in questo argomento:

* [Download progetto iniziale][StarterProject]
* [Download progetto completato][CompletedProject]

## <a name="bkmk_DeployStarterProject"></a>Distribuire l'app web di Azure di hello starter progetto tooan
1. Scarica un'applicazione hello conferenza listato [progetto iniziale][StarterProject].
2. Quindi in Esplora risorse, fare clic sul file con estensione ZIP scaricato hello e scegliere *proprietà*.
3. In hello **proprietà** finestra di dialogo scegliere hello **Unblock** pulsante. (Lo sblocco di un avviso di sicurezza che si verifica quando si tenta di toouse impedisce un *zip* file scaricato dal web hello.)
4. Fare clic sul file ZIP hello e selezionare **Estrai tutto** per decomprimere file hello. 
5. In Visual Studio, aprire hello *C#\Mvc5Mobile.sln* file.
6. In Esplora soluzioni, fare clic sul progetto hello e fare clic su **pubblica**.
   
   ![][DeployClickPublish]
7. In Pubblica sito Web fare clic su **Servizio app di Microsoft Azure**.
   
   ![][DeployClickWebSites]
8. Se non è già stato effettuato l'accesso ad Azure, fare clic su **Aggiungi un account**.
   
   ![][DeploySignIn]
9. Seguire hello richieste toolog all'account Azure.
10. finestra di dialogo di servizio App Hello vengono visualizzati è firmato. Fare clic su **New**.
    
    ![][DeployNewWebsite]  
11. In hello **nome dell'applicazione Web** , specificare un prefisso del nome applicazione univoco. Il nome completo dell'app sarà *&lt;prefix>*.azurewebsites.net. Selezionare inoltre un gruppo di risorse o specificarne uno nuovo in **Gruppo di risorse**. Quindi, fare clic su **New** toocreate un nuovo piano di servizio App.
    
    ![][DeploySiteSettings]
12. Configurare il nuovo piano di servizio App hello e fare clic su **OK**. 
    
    ![](./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-7a.png)
13. Nella finestra di dialogo Crea servizio App hello, fare clic su **crea**.
    
    ![](./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-7b.png) 
14. Dopo hello Azure le risorse vengono create, finestra di dialogo Pubblica sito Web hello verrà compilato con le impostazioni di hello per le nuove applicazioni. Fare clic su **Pubblica**.
    
    ![][DeployPublishSite]
    
    Al termine della pubblicazione hello starter progetto toohello Azure web app, Visual Studio browser desktop hello apre l'app web in tempo reale di hello toodisplay.
15. Avviare l'emulatore di browser per dispositivi mobili, copiare l'URL di hello per un'applicazione hello conferenza (*<prefix>*. azurewebsites.net) in un emulatore hello e quindi fare clic sul pulsante superiore destro e selezionare **Sfoglia per tag**. Se si utilizza Internet Explorer 11 come browser predefinito hello, è sufficiente tootype `F12`, quindi `Ctrl+8`e quindi modificare il profilo di browser hello troppo**Windows Phone**. L'immagine seguente mostra hello *AllTags* vista in modalità verticale (dalla scelta di **Sfoglia per tag**).
    
    ![][AllTags]

> [!TIP]
> Mentre l'applicazione MVC 5 da Visual Studio è possibile eseguire il debug, è possibile pubblicare il tooAzure app web nuovamente tooverify hello web in tempo reale app direttamente dal browser per dispositivi mobili o un emulatore del browser.
> 
> 

visualizzazione di Hello è molto leggibile in un dispositivo mobile. È possibile visualizzare anche già alcuni effetti hello visual applicato dal framework Bootstrap CSS hello.
Fare clic su hello **ASP.NET** collegamento.

![][SessionsByTagASP.NET]

Hello visualizzazione tag ASP.NET è montato zoom toohello schermata Bootstrap esegue automaticamente per l'utente. Tuttavia, è possibile migliorare il browser per dispositivi mobili vista toobetter seme hello. Ad esempio, hello **data** colonna è difficile da leggere. Più avanti nell'esercitazione di hello si modificherà hello *AllTags* visualizzare toomake è mobile descrittivi.

## <a name="bkmk_bootstrap"></a> Framework CSS Bootstrap
Novità hello MVC 5 modello è il supporto incorporato di Bootstrap. È già stato illustrato come è immediatamente possibile migliorare le visualizzazioni hello nell'applicazione. Ad esempio, la barra di spostamento hello nella parte superiore di hello è comprimibile automaticamente quando larghezza browser hello è minore. Nel browser desktop hello, provare a ridimensionare una finestra del browser hello e vedere come barra di spostamento hello modifica dell'aspetto. Si tratta di progettazione web reattiva hello è incorporata nel programma di avvio.

toosee come app Web hello apparirebbe senza Bootstrap, aprire *App\_avviare\\BundleConfig.cs* e impostare come commento le righe di hello contenenti *bootstrap.js* e *bootstrap.css*. Hello codice seguente viene illustrato hello ultime due istruzioni di hello `RegisterBundles` metodo dopo la modifica di hello:

     bundles.Add(new ScriptBundle("~/bundles/bootstrap").Include(
              //"~/Scripts/bootstrap.js",
              "~/Scripts/respond.js"));

    bundles.Add(new StyleBundle("~/Content/css").Include(
              //"~/Content/bootstrap.css",
              "~/Content/site.css"));

Premere `Ctrl+F5` toorun un'applicazione hello.

Osservare che se la barra di spostamento comprimibile hello è semplicemente un elenco non ordinato normale. Fare ancora clic su **Browse by tag**, quindi su **ASP.NET**.
Nella visualizzazione dell'emulatore di dispositivi mobili hello, si noterà che non è più montati zoom toohello schermata, è necessario scorrere lateralmente in ordine toosee hello destra della tabella hello.

![][SessionsByTagASP.NETNoBootstrap]

Annullare le modifiche e aggiornare hello tooverify di browser per dispositivi mobili che è stato ripristinato visualizzazione mobile descrittivi hello.

Bootstrap non specifico tooASP.NET MVC 5, ed è possibile sfruttare queste funzionalità in qualsiasi applicazione web. Ora, tuttavia, Bootstrap è integrato nel modello di progetto ASP.NET MVC 5 per consentire all'applicazione Web MVC 5 di sfruttarne i vantaggi per impostazione predefinita.

Per ulteriori informazioni sull'avvio, visitare toothe [Bootstrap] [ BootstrapSite] sito.

Nella sezione successiva hello si noterà come le viste specifiche tooprovide browser mobile.

## <a name="bkmk_overrideviews"></a>Eseguire l'override di viste di hello, layout e le visualizzazioni parziali
È possibile eseguire l'override di una visualizzazione (inclusi i layout e le visualizzazioni parziali) per i browser per dispositivi mobili in generale, per un singolo browser per dispositivi mobili o per un qualsiasi browser specifico. visualizzare uno specifico di dispositivi mobili tooprovide, è possibile copiare un file di visualizzazione e aggiungere *. Mobile* toohello nome del file. Ad esempio, toocreate mobili *indice* vista, è possibile copiare *viste\\Home\\cshtml* a *viste\\Home\\ Index.Mobile.cshtml*.

In questa sezione verrà illustrato come creare un file di layout specifico per dispositivi mobili.

toostart, copia *viste\\Shared\\\_cshtml* a *viste\\Shared\\\_Layout.Mobile.cshtml* . Aprire  *\_Layout.Mobile.cshtml* e modificare il titolo di hello da **MVC5 applicazione** troppo**MVC5 applicazione (Mobile)**.

In ogni `Html.ActionLink` chiamata per la barra di spostamento hello, rimuovere "Sfoglia per" in ogni collegamento *ActionLink*. Hello codice seguente viene illustrato hello completato `<ul class="nav navbar-nav">` tag del file di layout per dispositivi mobili hello.

    <ul class="nav navbar-nav">
        <li>@Html.ActionLink("Home", "Index", "Home")</li>
        <li>@Html.ActionLink("Date", "AllDates", "Home")</li>
        <li>@Html.ActionLink("Speaker", "AllSpeakers", "Home")</li>
        <li>@Html.ActionLink("Tag", "AllTags", "Home")</li>
    </ul>

Hello copia *viste\\Home\\AllTags.cshtml* file *viste\\Home\\AllTags.Mobile.cshtml*. Aprire il file nuovo hello e modificare il `<h2>` elemento da "Tags" troppo "tag (M)":

    <h2>Tags (M)</h2>

Sfoglia toohello tag pagina utilizzando un browser per desktop e l'utilizzo dell'emulatore di browser per dispositivi mobili. emulatore di browser per dispositivi mobili Hello Mostra hello due modifiche apportate (hello titolo da  *\_Layout.Mobile.cshtml* e titolo hello da *AllTags.Mobile.cshtml*).

![][AllTagsMobile_LayoutMobile]

Al contrario, non è cambiato display desktop hello (con titoli da  *\_cshtml* e *AllTags.cshtml*).

![][AllTagsMobile_LayoutMobileDesktop]

## <a name="bkmk_browserviews"></a> Creazione di visualizzazioni specifiche del browser
Inoltre visualizzazioni specifiche di desktop e toomobile, è possibile creare viste per un determinato browser. Ad esempio, è possibile creare viste che sono specifici per iPhone hello o browser Android hello. In questa sezione si creerà un layout per browser iPhone hello e una versione di iPhone di hello *AllTags* visualizzazione.

Aprire hello *Global. asax* file e aggiungere hello seguendo il toohello a fondo codice il `Application_Start` metodo.

    DisplayModeProvider.Instance.Modes.Insert(0, new DefaultDisplayMode("iPhone")
    {
        ContextCondition = (context => context.GetOverriddenUserAgent().IndexOf
            ("iPhone", StringComparison.OrdinalIgnoreCase) >= 0)
    });

Questo codice definisce una nuova modalità di visualizzazione denominata "iPhone" che verrà associata a ciascuna richiesta in ingresso. Se la richiesta in ingresso hello soddisfa la condizione che è stato definito (vale a dire, se l'agente utente hello contiene la stringa hello "iPhone"), il cui nome contiene il suffisso "iPhone" viste verranno ricercati ASP.NET MVC.

> [!NOTE]
> Quando aggiunta specifiche del browser per dispositivi mobili le modalità di visualizzazione, ad esempio per iPhone e Android, è troppo che primo argomento hello tooset`0` toomake (inserimento all'inizio di hello dell'elenco di hello) assicurarsi che la modalità specifiche del browser hello ha la precedenza sul modello mobile hello (*. Mobile.cshtml). Se hello mobili modello all'inizio di hello dell'elenco di hello al contrario, verrà selezionato tramite la modalità di visualizzazione desiderata (hello prima corrispondenza wins e modello mobile hello corrisponde a tutti i browser per dispositivi mobili). 
> 
> 

Nel codice hello, fare doppio clic su `DefaultDisplayMode`, scegliere **risolvere**, quindi scegliere `using System.Web.WebPages;`. Aggiunge un riferimento toothe `System.Web.WebPages` spazio dei nomi, dove il `DisplayModeProvider` e `DefaultDisplayMode` tipi sono definiti.

![][ResolveDefaultDisplayMode]

In alternativa, è possibile aggiungere solo manualmente hello seguente riga toothe `using` sezione del file hello.

    using System.Web.WebPages;

Salvare le modifiche di hello. Copiare il file *Views\\Shared\\\_Layout.Mobile.cshtml* in *Views\\Shared\\\_Layout.iPhone.cshtml*. Aprire il file nuovo hello e quindi modificare il titolo di hello da `MVC5 Application (Mobile)` a `MVC5 Application (iPhone)`.

Hello copia *viste\\Home\\AllTags.Mobile.cshtml* file *viste\\Home\\AllTags.iPhone.cshtml*. Nel nuovo file hello, modificare hello `<h2>` tag dell'elemento da "tag (M)" troppo"(iPhone)".

Eseguire un'applicazione hello. Eseguire un emulatore del browser per dispositivi mobili, assicurarsi che l'agente utente è stato impostato troppo "iPhone" e passare toohello *AllTags* visualizzazione. Se si utilizza l'emulatore hello negli strumenti di sviluppo F12 di Internet Explorer 11, configurare seguente toohello emulazione:

* Profilo del browser = **Windows Phone**
* Stringa agente utente = **Custom**
* Stringa personalizzata = **Apple-iPhone5C1/1001.525**

Hello schermata riportata di seguito viene illustrato hello *AllTags* rendering della visualizzazione nell'emulatore negli strumenti di sviluppo F12 di Internet Explorer 11 con stringa agente utente personalizzata di hello (si tratta di una stringa agente utente di iPhone 5 C).

![][AllTagsIPhone_LayoutIPhone]

Nel browser per dispositivi mobili hello, selezionare hello **altoparlanti** collegamento. Poiché non vi è una vista mobile (*AllSpeakers.Mobile.cshtml*), visualizzare altoparlanti predefinito hello (*AllSpeakers.cshtml*) viene eseguito il rendering visualizzazione layout mobili hello ( *\_ Layout.Mobile.cshtml*). Come illustrato di seguito, il titolo di hello **MVC5 applicazione (Mobile)** è definito in  *\_Layout.Mobile.cshtml*.

![][AllSpeakers_LayoutMobile]

A livello globale, è possibile disabilitare una visualizzazione (non mobile) predefinito per il rendering all'interno di un layout per dispositivi mobili impostando `RequireConsistentDisplayMode` a `true` in hello *viste\\\_ViewStart.cshtml* file, simile al seguente:

    @{
        Layout = "~/Views/Shared/_Layout.cshtml";
        DisplayModeProvider.Instance.RequireConsistentDisplayMode = true;
    }

Quando `RequireConsistentDisplayMode` è troppo`true`, layout mobili hello (*\_Layout.Mobile.cshtml*) viene utilizzato solo per le visualizzazioni mobili (ad esempio quando il file della visualizzazione è formato hello  ***ViewName** . Mobile.cshtml*). Potrebbe essere necessario tooset `RequireConsistentDisplayMode` troppo`true` se il layout per dispositivi mobili non funziona bene con le visualizzazioni non mobili. Hello schermata seguente viene illustrato come hello *altoparlanti* pagina esegue il rendering quando `RequireConsistentDisplayMode` è troppo`true` (senza stringa hello "(Mobile)" nella navigazione barra nella parte superiore di hello hello).

![][AllSpeakers_LayoutMobileOverridden]

È possibile disabilitare la modalità di visualizzazione coerente in una visualizzazione specifica impostando `RequireConsistentDisplayMode` troppo`false` nel file di visualizzazione hello. Il markup seguente in hello *viste\\Home\\AllSpeakers.cshtml* file imposta `RequireConsistentDisplayMode` troppo`false`:

    @model IEnumerable<string>

    @{
        ViewBag.Title = "All speakers";
        DisplayModeProvider.Instance.RequireConsistentDisplayMode = false;
    }

In questa sezione abbiamo visto come toocreate come toocreate layout e le visualizzazioni per i dispositivi specifici, ad esempio hello iPhone e le visualizzazioni e layout per dispositivi mobili.
Tuttavia, hello principale sfruttare framework Bootstrap CSS hello è il layout reattivo, il che significa che un singolo foglio di stile può essere applicata ai desktop, telefono e tablet browser toocreate un aspetto coerente. Nella sezione successiva hello verrà visualizzato come tooleverage Bootstrap toocreate mobile-friendly viste.

## <a name="bkmk_Improvespeakerslist"></a>Migliorare hello altoparlanti elenco
Come già visto hello *altoparlanti* visualizzazione è leggibile, ma hello collegamenti sono piccoli e sono di difficile tootap su un dispositivo mobile. In questa sezione si renderanno hello *AllSpeakers* mobile-friendly, che vengono visualizzati i collegamenti di grandi dimensioni, facile tap e contiene un tooquickly casella di ricerca trovare altoparlanti.

È possibile utilizzare hello Bootstrap [gruppo dell'elenco collegato] [ linked list group] stili per migliorare hello *altoparlanti* visualizzazione. In *viste\\Home\\AllSpeakers.cshtml*, sostituire il contenuto di hello del file Razor hello con codice hello riportato di seguito.

     @model IEnumerable<string>

    @{
        ViewBag.Title = "All Speakers";
    }

    <h2>Speakers</h2>

    <div class="list-group">
        @foreach (var speaker in Model)
        {
            @Html.ActionLink(speaker, "SessionsBySpeaker", new { speaker }, new { @class = "list-group-item" })
        }
    </div>

Hello `class="list-group"` attributo hello `<div>` tag si applica lo stile di elenco Bootstrap e hello `class="input-group-item"` attributo si applica tooeach collegamento lo stile di elemento di elenco Bootstrap.

Aggiornamento del browser per dispositivi mobili hello. Hello aggiornamento vista ha un aspetto simile al seguente:

![][AllSpeakersFixed]

Hello Bootstrap [gruppo dell'elenco collegato] [ linked list group] stile rende hello intera casella per ciascun collegamento selezionabile, ovvero una quantità migliore esperienza utente. Passare a vista desktop toothe e osservare hello un aspetto coerente.

![][AllSpeakersFixedDesktop]

Anche se è stata migliorata del browser per dispositivi mobili hello risulta difficile spostarsi lungo elenco di hello degli altoparlanti. Bootstrap non fornisce un filtro di ricerca pronto all'uso, ma è possibile aggiungere questa funzionalità con poche righe di codice. Verrà innanzitutto aggiungere una visualizzazione toohello casella di ricerca, quindi collegare il codice JavaScript per la funzione di filtro hello hello. In *viste\\Home\\AllSpeakers.cshtml*, aggiungere un \<modulo\> tag appena hello \<h2\> tag, come illustrato di seguito:

    @model IEnumerable<string>

    @{
        ViewBag.Title = "All Speakers";
    }

    <h2>Speakers</h2>

    <form class="input-group">
        <span class="input-group-addon"><span class="glyphicon glyphicon-search"></span></span>
        <input type="text" class="form-control" placeholder="Search speaker">
    </form>
    <br />
    <div class="list-group">
        @foreach (var speaker in Model)
        {
            @Html.ActionLink(speaker, 
                             "SessionsBySpeaker", 
                             new { speaker }, 
                             new { @class = "list-group-item" })
        }
    </div>

Si noti che hello `<form>` e `<input>` tag entrambi hanno toothem Bootstrap stili applicati hello. Hello `<span>` elemento aggiunge un Bootstrap [glyphicon] [ glyphicon] toothe casella di ricerca.

In hello *script* cartella, aggiungere un file JavaScript denominato *filter.js*. Aprire il file hello e incollare hello seguente codice al suo interno:

    $(function () {

        // reset hello search form when hello page loads
        $("form").each(function () {
            this.reset();
        });

        // wire up hello events toohello <input> element for search/filter
        $("input").bind("keyup change", function () {
            var searchtxt = this.value.toLowerCase();
            var items = $(".list-group-item");

            // show all speakers that begin with hello typed text and hide others
            for (var i = 0; i < items.length; i++) {
                var val = items[i].text.toLowerCase();
                val = val.substring(0, searchtxt.length);
                if (val == searchtxt) {
                    $(items[i]).show();
                }
                else {
                    $(items[i]).hide();
                }
            }
        });
    });

È inoltre necessario tooinclude filter.js nei bundle registrati. Aprire *App\_avviare\\BundleConfig.cs* e modificare i pacchetti prima di hello. Modificare il primo `bundles.Add` istruzione (per hello **jquery** bundle) tooinclude *script\\filter.js*, come segue:

     bundles.Add(new ScriptBundle("~/bundles/jquery").Include(
                "~/Scripts/jquery-{version}.js",
                "~/Scripts/filter.js"));

Hello **jquery** bundle è già stato eseguito per impostazione predefinita hello  *\_Layout* visualizzazione. In un secondo momento, è possibile utilizzare hello JavaScript stesso codice tooapply visualizzazioni elenco tooother funzionalità filtro.

Aggiornamento del browser per dispositivi mobili hello e passare toohello *AllSpeakers* visualizzazione. Nella casella di ricerca digitare "sc". elenco degli altoparlanti Hello ora deve essere filtrato in base tooyour stringa di ricerca.

![][AllSpeakersFixedSearchBySC]

## <a name="bkmk_improvetags"></a>Migliorare hello elenco tag
Ad esempio hello *altoparlanti* visualizzare, hello *tag* visualizzazione è leggibile, ma i collegamenti di hello sono di piccole dimensioni e difficili tootap su un dispositivo mobile. È possibile correggere hello *tag* visualizzazione hello stesso modo risolvere hello *altoparlanti* visualizzare, se si utilizzano le modifiche al codice hello descritti in precedenza, ma con i seguenti hello `Html.ActionLink` la sintassi del metodo in  *Viste\\Home\\AllTags.cshtml*:

    @Html.ActionLink(tag, 
                     "SessionsByTag", 
                     new { tag }, 
                     new { @class = "list-group-item" })

Hello aggiornato ha un aspetto browser desktop come indicato di seguito:

![][AllTagsFixedDesktop]

E hello aggiornato ha un aspetto browser per dispositivi mobili, come indicato di seguito: 

![][AllTagsFixed]

> [!NOTE]
> Se si nota la formattazione elenco hello originale è ancora disponibile in hello browser per dispositivi mobili e chiedersi quali stile Bootstrap nice tooyour verificato anomalo, si tratta di un elemento le viste precedenti azione toocreate mobili specifico. Tuttavia, ora che si utilizza hello Bootstrap CSS framework toocreate una progettazione reattiva web, andare a capo e rimuovere queste visualizzazioni specifiche di dispositivi mobili e viste di hello layout specifici dispositivi mobili. Dopo aver eseguito questa operazione, i browser per dispositivi mobili aggiornati hello visualizzerà lo stile di Bootstrap hello.
> 
> 

## <a name="bkmk_improvedates"></a>Migliorare hello elenco date
È possibile migliorare hello *date* visualizzare come migliori hello *altoparlanti* e *tag* viste se si utilizza hello modifiche al codice descritti in precedenza, ma con hello seguente `Html.ActionLink` la sintassi del metodo in *viste\\Home\\AllDates.cshtml*:

    @Html.ActionLink(date.ToString("ddd, MMM dd, h:mm tt"), 
                     "SessionsByDate", 
                     new { date }, 
                     new { @class = "list-group-item" })

Si otterrà una visualizzazione del browser per dispositivi mobili aggiornato simile a quella riportata di seguito:

![][AllDatesFixed]

È possibile migliorare ulteriormente hello *date* Visualizza per organizzare i valori di data e ora hello per Data. Questa operazione può essere eseguita con hello Bootstrap [pannelli] [ panels] stile. Sostituire il contenuto di hello di hello *viste\\Home\\AllDates.cshtml* file con il codice seguente:

    @model IEnumerable<DateTime>

    @{
        ViewBag.Title = "All Dates";
    }

    <h2>Dates</h2>

    @foreach (var dategroup in Model.GroupBy(x=>x.Date))
    {
        <div class="panel panel-primary">
            <div class="panel-heading">
                @dategroup.Key.ToString("ddd, MMM dd")
            </div>
            <div class="panel-body list-group">
                @foreach (var date in dategroup)
                {
                    @Html.ActionLink(date.ToString("h:mm tt"), 
                                     "SessionsByDate", 
                                     new { date }, 
                                     new { @class = "list-group-item" })
                }
            </div>
        </div>
    }

Questo codice crea un oggetto separato `<div class="panel panel-primary">` tag per ogni data distinct nell'elenco di hello e utilizza hello [gruppo dell'elenco collegato] [ linked list group] per la rispettiva collega come prima. Di seguito è riportato il browser per dispositivi mobili hello aspetto quando si esegue questo codice:

![][AllDatesFixed2]

Browser desktop toohello commutatore. Nuovamente, nota hello coerente.

![][AllDatesFixed2Desktop]

## <a name="bkmk_improvesessionstable"></a>Migliorare la visualizzazione SessionsTable hello
In questa sezione si renderanno hello *SessionsTable* visualizzare altre mobile-friendly. Questa modifica è modifiche precedenti hello più estese.

Nel browser per dispositivi mobili hello, toccare hello **Tag** pulsante, quindi immettere `asp` nella casella di ricerca.

![][AllTagsFixedSearchByASP]

Toccare hello **ASP.NET** collegamento.

![][SessionsTableTagASP.NET]

Come si può notare, visualizzazione hello viene formattata come una tabella, ovvero toobe progettato attualmente visualizzati in browser desktop hello. Tuttavia, è un po' difficile tooread in un browser per dispositivi mobili. toofix, aprire *viste\\Home\\SessionsTable.cshtml* quindi sostituire il contenuto di hello del file con hello seguente codice:

    @model IEnumerable<Mvc5Mobile.Models.Session>

    <h2>@ViewBag.Title</h2>

    <div class="container">
        <div class="row">
            @foreach (var session in Model)
            {
                <div class="col-md-4">
                    <div class="list-group">
                        @Html.ActionLink(session.Title, 
                                         "SessionByCode", 
                                         new { session.Code }, 
                                         new { @class="list-group-item active" })
                        <div class="list-group-item">
                            <div class="list-group-item-text">
                                @Html.Partial("_SpeakersLinks", session)
                            </div>
                            <div class="list-group-item-info">
                                @session.DateText
                            </div>
                            <div class="list-group-item-info small hidden-xs">
                                @Html.Partial("_TagsLinks", session)
                            </div>
                        </div>
                    </div>
                </div>
            }
        </div>
    </div>

codice Hello esegue 3 operazioni:

* Usa hello Bootstrap [gruppo personalizzato di elenco collegato] [ custom linked list group] tooformat hello in verticale, le informazioni sulla sessione in modo che tutte queste informazioni sono leggibile in un browser per dispositivi mobili (utilizzando le classi, ad esempio elenco-gruppo-elemento-text)
* si applica hello [sistema griglia] [ grid system] toothe layout, pertanto tale sessione hello elementi flusso orizzontalmente in browser desktop hello e verticalmente in browser per dispositivi mobili di hello (mediante la classe di hello col-md-4)
* Usa hello [utilità reattiva] [ responsive utilities] per nascondere i tag di sessione hello quando viene visualizzato nel browser per dispositivi mobili di hello (mediante la classe nascosto-xs hello)

È anche possibile toccare una titolo collegamento toogo toohello rispettivi della sessione. immagine di Hello seguente riflette le modifiche al codice hello.

![][FixedSessionsByTag]

sistema di griglia Bootstrap Hello applicati automaticamente dispone le sessioni in senso verticale in browser per dispositivi mobili hello. Si noti inoltre che non vengono visualizzati i tag hello. Browser desktop toohello commutatore.

![][SessionsTableFixedTagASP.NETDesktop]

Nel browser desktop hello, si noti che hello vengono ora visualizzati. Inoltre, si noterà che il sistema di griglia Bootstrap hello che è applicato dispone gli elementi di sessione hello in due colonne. Se si ingrandisce il browser, si noterà che disposizione hello cambia toothree colonne.

## <a name="bkmk_improvesessionbycode"></a>Migliorare la visualizzazione SessionByCode hello
Infine, sarà possibile risolvere hello *SessionByCode* visualizzare toomake è mobile descrittivi.

Nel browser per dispositivi mobili hello, toccare hello **Tag** pulsante, quindi immettere `asp` nella casella di ricerca.

![][AllTagsFixedSearchByASP]

Toccare hello **ASP.NET** collegamento. Vengono visualizzate le sessioni per il tag ASP.NET hello.

![][FixedSessionsByTag]

Scegliere hello **la creazione di un'applicazione a pagina singola con ASP.NET e AngularJS** collegamento.

![][SessionByCode3-644]

visualizzazione desktop predefinita di Hello è correttamente, ma è possibile migliorare aspetto hello facilmente con alcuni componenti GUI di Bootstrap.

Aprire *viste\\Home\\SessionByCode.cshtml* e sostituire il contenuto di hello con hello markup seguente:

    @model Mvc5Mobile.Models.Session

    @{
        ViewBag.Title = "Session details";
    }
    <h3>@Model.Title (@Model.Code)</h3>
    <p>
        <strong>@Model.DateText</strong> in <strong>@Model.Room</strong>
    </p>

    <div class="panel panel-primary">
        <div class="panel-heading">
            Speakers
        </div>
        @foreach (var speaker in Model.Speakers)
        {
            @Html.ActionLink(speaker, 
                             "SessionsBySpeaker", 
                             new { speaker }, 
                             new { @class="panel-body" })
        }
    </div>

    <p>@Model.Abstract</p>

    <div class="panel panel-primary">
        <div class="panel-heading">
            Tags
        </div>
        @foreach (var tag in Model.Tags)
        {
            @Html.ActionLink(tag, 
                             "SessionsByTag", 
                             new { tag }, 
                             new { @class = "panel-body" })
        }
    </div>

Nuovo markup Hello Usa stile di visualizzazione di tooimprove hello mobili i pannelli Bootstrap. 

Aggiornamento del browser per dispositivi mobili hello. Hello immagine seguente riflette le modifiche di codice hello appena apportate:

![][SessionByCodeFixed3-644]

## <a name="wrap-up-and-review"></a>Riepilogo e revisione
In questa esercitazione è stato illustrato come le applicazioni Web ASP.NET MVC 5 toodevelop mobile-friendly toouse. incluse le seguenti:

* Distribuire un tooan applicazione ASP.NET MVC 5 App del servizio web app
* Utilizzare layout web reattiva toocreate Bootstrap nell'applicazione MVC 5
* Override di layout, visualizzazioni e visualizzazioni parziali, sia in modo globale sia per una singola visualizzazione
* Controllo del layout ed esecuzione di un override parziale usando la proprietà `RequireConsistentDisplayMode`
* Creazione di viste che utilizzano browser specifico, ad esempio browser iPhone hello
* Applicazione di stili Bootstrap in codice Razor

## <a name="see-also"></a>Vedere anche
* [9 principi di base della progettazione Web reattiva](http://blog.froont.com/9-basic-principles-of-responsive-web-design/)
* [Bootstrap][BootstrapSite]
* [Blog ufficiale di Bootstrap][Official Bootstrap Blog]
* [Tutorial Twitter Bootstrap su Tutorial Republic][Twitter Bootstrap Tutorial from Tutorial Republic]
* [Hello palestra per Bootstrap][hello Bootstrap Playground]
* [Procedure consigliate per applicazioni Web W3C per dispositivi mobili][W3C Recommendation Mobile Web Application Best Practices]
* [Candidate Recommendation W3C per query sui supporti][W3C Candidate Recommendation for media queries]

## <a name="whats-changed"></a>Modifiche apportate
* Per una Guida toohello modifica da siti Web tooApp servizio vedere: [relativo impatto sui servizi di Azure esistente e servizio App di Azure](http://go.microsoft.com/fwlink/?LinkId=529714)

<!-- Internal Links -->
[Deploy hello starter project tooan Azure web app]: #bkmk_DeployStarterProject
[Bootstrap CSS Framework]: #bkmk_bootstrap
[Override hello Views, Layouts, and Partial Views]: #bkmk_overrideviews
[Create Browser-Specific Views]:#bkmk_browserviews
[Improve hello Speakers List]: #bkmk_Improvespeakerslist
[Improve hello Tags List]: #bkmk_improvetags
[Improve hello Dates List]: #bkmk_improvedates
[Improve hello SessionsTable View]: #bkmk_improvesessionstable
[Improve hello SessionByCode View]: #bkmk_improvesessionbycode

<!-- External Links -->
[Visual Studio Express 2013]: http://www.visualstudio.com/downloads/download-visual-studio-vs#d-express-web
[Visual Studio 2015]: https://www.visualstudio.com/downloads/download-visual-studio-vs
[AzureSDKVs2013]: http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409
[Fiddler]: http://www.fiddler2.com/fiddler2/
[EmulatorIE11]: http://msdn.microsoft.com/library/ie/dn255001.aspx
[EmulatorChrome]: https://developers.google.com/chrome-developer-tools/docs/mobile-emulation
[EmulatorOpera]: http://www.opera.com/developer/tools/mobile/
[StarterProject]: http://go.microsoft.com/fwlink/?LinkID=398780&clcid=0x409
[CompletedProject]: http://go.microsoft.com/fwlink/?LinkID=398781&clcid=0x409
[BootstrapSite]: http://getbootstrap.com/
[WebPIAzureSdk23NetVS13]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/WebPIAzureSdk23NetVS13.png
[linked list group]: http://getbootstrap.com/components/#list-group-linked
[glyphicon]: http://getbootstrap.com/components/#glyphicons
[panels]: http://getbootstrap.com/components/#panels
[custom linked list group]: http://getbootstrap.com/components/#list-group-custom-content
[grid system]: http://getbootstrap.com/css/#grid
[responsive utilities]: http://getbootstrap.com/css/#responsive-utilities
[Official Bootstrap Blog]: http://blog.getbootstrap.com/
[Twitter Bootstrap Tutorial from Tutorial Republic]: http://www.tutorialrepublic.com/twitter-bootstrap-tutorial/
[hello Bootstrap Playground]: http://www.bootply.com/
[W3C Recommendation Mobile Web Application Best Practices]: http://www.w3.org/TR/mwabp/
[W3C Candidate Recommendation for media queries]: http://www.w3.org/TR/css3-mediaqueries/

<!-- Images -->
[DeployClickPublish]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-1.png
[DeployClickWebSites]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-2.png
[DeploySignIn]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-3.png
[DeployUsername]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-4.png
[DeployPassword]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-5.png
[DeployNewWebsite]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-6.png
[DeploySiteSettings]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-7.png
[DeployPublishSite]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-8.png
[MobileHomePage]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/mobile-home-page.png
[FixedSessionsByTag]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsByTag-ASP.NET-Fixed.png
[AllTags]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTags.png
[SessionsByTagASP.NET]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsByTag-ASP.NET.png
[SessionsByTagASP.NETNoBootstrap]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsByTag-ASP.NET-NoBootstrap.png
[AllTagsMobile_LayoutMobile]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTagsMobile-_LayoutMobile.png
[AllTagsMobile_LayoutMobileDesktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTagsMobile-_LayoutMobile-Desktop.png
[ResolveDefaultDisplayMode]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/Resolve-DefaultDisplayMode.png
[AllTagsIPhone_LayoutIPhone]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTagsIPhone-_LayoutIPhone.png
[AllSpeakers_LayoutMobile]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-_LayoutMobile.png
[AllSpeakers_LayoutMobileOverridden]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-_LayoutMobile-Overridden.png
[AllSpeakersFixed]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-Fixed.png
[AllSpeakersFixedDesktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-Fixed-Desktop.png
[AllSpeakersFixedSearchBySC]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-Fixed-SearchBySC.png
[AllTagsFixedDesktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTags-Fixed-Desktop.png 
[AllTagsFixed]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTags-Fixed.png
[AllDatesFixed]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllDates-Fixed.png
[AllDatesFixed2]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllDates-Fixed2.png
[AllDatesFixed2Desktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllDates-Fixed2-Desktop.png
[AllTagsFixedSearchByASP]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTags-Fixed-SearchByASP.png
[SessionsTableTagASP.NET]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsTable-Tag-ASP.NET.png
[SessionsTableFixedTagASP.NETDesktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsTable-Fixed-Tag-ASP.NET-Desktop.png
[SessionByCode3-644]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionByCode-3-644.png
[SessionByCodeFixed3-644]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionByCode-Fixed-3-644.png

