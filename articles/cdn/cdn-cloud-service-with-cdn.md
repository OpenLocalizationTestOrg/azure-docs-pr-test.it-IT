---
title: Integrare un servizio cloud di Azure con la rete CDN di Azure | Documentazione Microsoft
description: Informazioni su come distribuire un servizio cloud che fornisce contenuti da un endpoint della rete CDN di Azure integrato
services: cdn, cloud-services
documentationcenter: .net
author: zhangmanling
manager: erikre
editor: tysonn
ms.assetid: b3c0108f-9ec5-43a8-8fd0-40eafbd32637
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: f2849fe25fd0d5b3dc26598ffba7591cb7433161
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="intro"></a> Integrare un servizio cloud con la rete CDN di Azure
È possibile integrare un servizio cloud con la rete CDN di Azure, rendendo disponibile qualsiasi contenuto dalla posizione del servizio cloud. Questo approccio offre i vantaggi seguenti:

* Facile distribuzione e aggiornamento di immagini, script e fogli di stile nelle directory del progetto servizio cloud
* Facile aggiornamento dei pacchetti NuGet nel servizio cloud, come le versioni jQuery o Bootstrap
* Gestione dell'applicazione Web e del contenuto gestito dalla rete CDN dalla stessa interfaccia di Visual Studio
* Flusso di lavoro di distribuzione unificato per l'applicazione Web e il contenuto gestito dalla rete CDN
* Integrazione di creazione di bundle e minimizzazione ASP.NET con la rete CDN di Azure

## <a name="what-you-will-learn"></a>Contenuto dell'esercitazione
In questa esercitazione si apprenderà come:

* [Integrare un endpoint della rete CDN di Azure con il servizio cloud e rendere disponibile il contenuto statico nella pagine Web dalla rete CDN di Azure](#deploy)
* [Configurare le impostazioni della cache per il contenuto statico nel servizio cloud](#caching)
* [Gestire il contenuto dalle azioni del controller tramite la rete CDN di Azure](#controller)
* [Rendere disponibile contenuto in bundle e minimizzato attraverso la rete CDN di Azure, mantenendo comunque l'esperienza di debug degli script in Visual Studio](#bundling)
* [Configurare il fallback di script e file CSS quando la rete CDN di Azure è offline](#fallback)

## <a name="what-you-will-build"></a>Obiettivo di compilazione
Verrà distribuito un ruolo Web del servizio cloud usando il modello MVC di ASP.NET predefinito, si aggiungerà il codice per gestire il contenuto da una rete CDN di Azure integrata, ad esempio un'immagine, i risultati dell'azione del controller e i file JavaScript e CSS predefiniti, e si scriverà anche il codice per configurare il meccanismo di fallback per i bundle serviti nel caso in cui la rete CDN non sia in linea.

## <a name="what-you-will-need"></a>Prerequisiti
Per completare questa esercitazione, è necessario disporre dei prerequisiti seguenti:

* Un [account Microsoft Azure](/account/)
* Visual Studio 2015 con [Azure SDK](http://go.microsoft.com/fwlink/?linkid=518003&clcid=0x409)

> [!NOTE]
> Per completare l'esercitazione, è necessario un account Azure.
> 
> * È possibile [aprire un account Azure gratuitamente](https://azure.microsoft.com/pricing/free-trial/): si riceveranno dei crediti da usare per provare i servizi di Azure a pagamento e, anche dopo avere esaurito i crediti, è possibile mantenere l'account per usare i servizi di Azure gratuiti, ad esempio Siti Web.
> * È possibile [attivare i benefici della sottoscrizione MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/): con la sottoscrizione MSDN ogni mese si accumulano crediti che è possibile usare per i servizi di Azure a pagamento.
> 
> 

<a name="deploy"></a>

## <a name="deploy-a-cloud-service"></a>Distribuire un servizio cloud
In questa sezione verrà distribuito il modello di applicazione MVC di ASP.NET predefinito in Visual Studio 2015 a un ruolo Web del servizio cloud, che verrà quindi integrato con un nuovo endpoint CDN. Seguire le istruzioni riportate di seguito:

1. In Visual Studio 2015 creare un nuovo servizio cloud di Azure dalla barra dei menu **File > Nuovo > Progetto > Cloud > Servizio cloud di Azure**. Assegnargli un nome e fare clic su **OK**.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-1-new-project.PNG)
2. Selezionare **Ruolo Web ASP.NET** e fare clic sul pulsante **>**. Fare clic su OK.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-2-select-role.PNG)
3. Selezionare **MVC** e fare clic su **OK**.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-3-mvc-template.PNG)
4. Pubblicare ora questo ruolo Web in un servizio cloud di Azure. Fare clic con il pulsante destro del mouse sul progetto servizio cloud e selezionare **Pubblica**.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-4-publish-a.png)
5. Se non è stata ancora effettuato l’accesso a Microsoft Azure, fare clic su **Aggiungi un account** nell'elenco a discesa e fare clic sulla voce di menu **Aggiungi un account**.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-5-publish-signin.png)
6. Nella pagina di accesso eseguire l'accesso con l'account Microsoft usato per attivare l'account Azure.
7. Una volta effettuato l'accesso, fare clic su **Avanti**.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-6-publish-signedin.png)
8. Supponendo che non sia stato creato un servizio cloud né un account di archiviazione, Visual Studio aiuterà a crearli entrambi. Nella finestra di dialogo **Crea servizio cloud e account di archiviazione** , digitare il nome del servizio desiderato e selezionare l’area desiderata. Fare quindi clic su **Crea**.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-7-publish-createserviceandstorage.png)
9. Nella pagina Impostazioni di pubblicazione, verificare la configurazione e fare clic su **Pubblica**.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-8-publish-finalize.png)
   
   > [!NOTE]
   > Il processo di pubblicazione per i servizi cloud richiede tempi elevati. L'opzione Abilita Distribuzione Web per tutti i ruoli Web può velocizzare il debug del servizio cloud fornendo aggiornamenti rapidi (ma temporanei) dei ruoli Web. Per altre informazioni su questa opzione, vedere [Pubblicazione di un servizio cloud con gli strumenti di Azure](http://msdn.microsoft.com/library/ff683672.aspx).
   > 
   > 
   
    Quando la finestra **Log attività di Microsoft Azure** indica che lo stato di pubblicazione è **Completato**, è possibile creare un endpoint della rete CDN integrato con il servizio cloud.
   
   > [!WARNING]
   > Se, dopo la pubblicazione, il servizio cloud distribuito mostra una schermata di errore, probabilmente è perché il servizio cloud che è stato distribuito usa un [guest del sistema operativo che non include .NET 4.5.2](../cloud-services/cloud-services-guestos-update-matrix.md#news-updates).  È possibile risolvere il problema da [distribuzione .NET 4.5.2 come attività di avvio](../cloud-services/cloud-services-dotnet-install-dotnet.md).
   > 
   > 

## <a name="create-a-new-cdn-profile"></a>Creare un nuovo profilo di rete CDN
Un profilo di rete CDN è una raccolta di endpoint della rete CDN.  Ogni profilo contiene uno o più endpoint della rete CDN.  Si consiglia di usare più profili per organizzare gli endpoint della rete CDN tramite il dominio internet, l’applicazione web o altri criteri.

> [!TIP]
> Se si dispone già di un profilo di rete CDN che si desidera usare per questa esercitazione, passare a [Creare un nuovo endpoint della rete CDN](#create-a-new-cdn-endpoint).
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]

## <a name="create-a-new-cdn-endpoint"></a>Creare un nuovo endpoint della rete CDN
**Per creare un nuovo endpoint della rete CDN per l'account di archiviazione**

1. Nel [portale di gestione di Azure](https://portal.azure.com)passare al profilo di rete CDN.  Lo si potrebbe aver bloccato nel dashboard nel passaggio precedente.  Se così non fosse, è possibile trovarlo facendo clic su **Esplora**, quindi su **Profili rete CDN** e facendo clic sul profilo in cui si prevede di aggiungere l'endpoint.
   
    Viene visualizzato il pannello del profilo di rete CDN.
   
    ![Profilo di rete CDN][cdn-profile-settings]
2. Fare clic sul pulsante **Aggiungi Endpoint** .
   
    ![Pulsante Aggiungi endpoint][cdn-new-endpoint-button]
   
    Viene visualizzato il pannello **Aggiungi un endpoint** .
   
    ![Pannello Aggiungi endpoint][cdn-add-endpoint]
3. Immettere un **Nome** per questo endpoint della rete CDN.  Questo nome verrà usato per accedere alle risorse memorizzate nella cache nel dominio `<EndpointName>.azureedge.net`.
4. Nell'elenco a discesa **Tipo di origine** , selezionare *Servizio cloud*.  
5. Nell'elenco a discesa **Nome host di origine** , selezionare il servizio cloud.
6. Lasciare le impostazioni predefinite per **Percorso dell'origine**, **Intestazione host di origine** e **Protocollo/Porta dell'origine**.  È necessario specificare almeno un protocollo (HTTP o HTTPS).
7. Per creare il nuovo endpoint, fare clic sul pulsante **Aggiungi** .
8. Dopo la creazione, l'endpoint sarà visualizzato in un elenco di endpoint per il profilo. Nella visualizzazione elenco sono mostrati gli URL da usare per accedere a contenuti memorizzati nella cache, oltre al dominio di origine.
   
    ![Endpoint della rete CDN][cdn-endpoint-success]
   
   > [!NOTE]
   > L'endpoint non sarà immediatamente disponibile per l'uso.  Ci possono volere fino a 90 minuti per far sì che la registrazione si propaghi attraverso la rete CDN. È possibile che gli utenti che provano a usare immediatamente il nome di dominio della rete CDN ricevano un errore con codice di stato 404 fino a quando il contenuto non risulterà disponibile tramite la rete CDN.
   > 
   > 

## <a name="test-the-cdn-endpoint"></a>Testare l'endpoint della rete CDN
Quando lo stato di pubblicazione è **Completato**, aprire una finestra del browser e passare a **http://<cdnName>*.azureedge.net/Content/bootstrap.css**. Nella configurazione illustrata, questo URL è il seguente:

    http://camservice.azureedge.net/Content/bootstrap.css

che corrisponde all'URL di origine seguente all'endpoint della rete CDN:

    http://camcdnservice.cloudapp.net/Content/bootstrap.css

Quando si passa a **http://*&lt;cdnName>*.azureedge.net/Content/bootstrap.css**, a seconda del browser, verrà richiesto di scaricare o di aprire il file bootstrap.css disponibile nell'app Web pubblicata.

![](media/cdn-cloud-service-with-cdn/cdn-1-browser-access.PNG)

È possibile accedere in maniera simile a qualsiasi URL pubblicamente accessibile all'indirizzo **http://*&lt;nomeServizio>*.cloudapp.net/**, direttamente dall'endpoint della rete CDN. ad esempio:

* Un file con estensione js dal percorso /Script
* Qualsiasi file di contenuto dal percorso /Content
* Qualsiasi controller/azione
* Se la stringa di query viene abilitata sull'endpoint della rete CDN, qualsiasi URL con stringhe di query

In effetti, con la configurazione precedente, è possibile ospitare l'intero servizio cloud da **http://*&lt;cdnName>*.azureedge.net/**. Se si passa a **http://camservice.azureedge.net/**, si ottiene il risultato dell'azione da Home/Index.

![](media/cdn-cloud-service-with-cdn/cdn-2-home-page.PNG)

Ciò non significa, ad ogni modo, che sia sempre una buona idea rendere disponibile un intero servizio cloud attraverso la rete CDN di Azure. 

Una rete CDN con ottimizzazione della distribuzione statica non velocizza necessariamente la distribuzione degli asset dinamici, che non sono progettati per la memorizzazione nella cache o che vengono aggiornati molto spesso, poiché la rete CDN deve eseguire molto spesso il pull di una nuova versione dell'asset dal server di origine. Per questo scenario è possibile abilitare l'ottimizzazione [Accelerazione sito dinamico](cdn-dynamic-site-acceleration.md) nell'endpoint di rete CDN che usa diverse tecniche per velocizzare la distribuzione di asset dinamici non memorizzabili nella cache. 

Se è presente un sito con una combinazione di contenuto statico e dinamico, è possibile scegliere di fornire il contenuto statico dalla rete CDN con un tipo di ottimizzazione statica, ad esempio la distribuzione generale sul Web, e di fornire il contenuto dinamico direttamente dal server di origine oppure tramite un endpoint di rete CDN con l'ottimizzazione Accelerazione sito dinamico attivata in base al caso specifico. A tale scopo, si è già visto come accedere ai singoli file di contenuto dall'endpoint della rete CDN. Più avanti, in Gestire il contenuto dalle azioni del controller attraverso la rete CDN di Azure, verrà illustrato come gestire una specifica azione del controller attraverso l'endpoint di rete CDN.

L'alternativa consiste nel determinare quale contenuto rendere disponibile dalla rete CDN di Azure, valutando caso per caso nel servizio cloud. A tale scopo, si è già visto come accedere ai singoli file di contenuto dall'endpoint della rete CDN. Più avanti verrà illustrato come gestire una specifica azione del controller attraverso l'endpoint CDN in [Gestire il contenuto dalle azioni del controller attraverso la rete CDN di Azure](#controller).

<a name="caching"></a>

## <a name="configure-caching-options-for-static-files-in-your-cloud-service"></a>Configurare le opzioni di memorizzazione nella cache dei file statici nel servizio cloud
Con l'integrazione della rete CDN di Azure nel servizio cloud è possibile specificare in che modo si vuole memorizzare il contenuto statico nella cache dell'endpoint della rete CDN. A tale scopo, aprire il file *Web.config* dal progetto di ruolo Web (ad esempio, WebRole1) e aggiungere un elemento `<staticContent>` a `<system.webServer>`. Il linguaggio XML seguente configura la scadenza della cache entro tre giorni.  

    <system.webServer>
      <staticContent>
        <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="3.00:00:00"/>
      </staticContent>
      ...
    </system.webServer>

A questo punto, tutti i file statici nel servizio cloud osserveranno la stessa regola nella cache della rete CDN. Per un controllo più granulare delle impostazioni della cache, aggiungere un file *Web.config* in una cartella e quindi aggiungervi le impostazioni. Ad esempio, aggiungere un file *Web.config* alla cartella *\Content* e sostituire il contenuto con il seguente codice XML:

    <?xml version="1.0"?>
    <configuration>
      <system.webServer>
        <staticContent>
          <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="15.00:00:00"/>
        </staticContent>
      </system.webServer>
    </configuration>

Queste impostazioni causano la memorizzazione nella cache di tutti i file statici della cartella *\Content* per 15 giorni.

Per altre informazioni su come configurare l'elemento `<clientCache>`, vedere [Client Cache &lt;clientCache>](http://www.iis.net/configreference/system.webserver/staticcontent/clientcache) (Cache client).

Nella sezione [Gestire il contenuto dalle azioni del controller attraverso la rete CDN di Azure](#controller)verrà illustrato anche come configurare le impostazioni della cache per ottenere i risultati dell'azione del controller nella cache della rete CDN.

<a name="controller"></a>

## <a name="serve-content-from-controller-actions-through-azure-cdn"></a>Gestire il contenuto dalle azioni del controller attraverso la rete CDN di Azure
Quando si integra un ruolo Web del servizio cloud nella rete CDN di Azure, è relativamente facile gestire il contenuto dalle azioni del controller attraverso la rete CDN di Azure. Invece di rendere disponibile il servizio cloud direttamente attraverso la rete CDN (come descritto sopra), [Maarten Balliauw](https://twitter.com/maartenballiauw) mostra come farlo con un divertente controller MemeGenerator nel video sulla [riduzione della latenza sul Web con la rete CDN di Azure](http://channel9.msdn.com/events/TechDays/Techdays-2014-the-Netherlands/Reducing-latency-on-the-web-with-the-Windows-Azure-CDN), che viene riprodotto semplicemente in questo articolo.

Si supponga di volere generare nel servizio cloud dei meme basati su un'immagine di un giovane Chuck Norris (foto di [Alan Light](http://www.flickr.com/photos/alan-light/218493788/)), come questa:

![](media/cdn-cloud-service-with-cdn/cdn-5-memegenerator.PNG)

Si usa una semplice azione `Index` che consente ai clienti di specificare i superlativi nell'immagine, quindi genera il meme dopo aver pubblicato nell'azione. Poiché si tratta di Chuck Norris, ci si aspetta che questa pagina diventi enormemente popolare in tutto il mondo. È un ottimo esempio di come gestire contenuto semi dinamico con la rete CDN di Azure.

Seguire i passaggi precedenti per configurare questa azione del controller:

1. Nella cartella *\Controllers* creare un nuovo file con estensione cs denominato *MemeGeneratorController.cs* e sostituire il contenuto con il codice seguente. Assicurarsi di sostituire la parte evidenziata con il nome della propria rete CDN.  
   
        using System;
        using System.Collections.Generic;
        using System.Diagnostics;
        using System.Drawing;
        using System.IO;
        using System.Net;
        using System.Web.Hosting;
        using System.Web.Mvc;
        using System.Web.UI;
   
        namespace WebRole1.Controllers
        {
            public class MemeGeneratorController : Controller
            {
                static readonly Dictionary<string, Tuple<string ,string>> Memes = new Dictionary<string, Tuple<string, string>>();
   
                public ActionResult Index()
                {
                    return View();
                }
   
                [HttpPost, ActionName("Index")]
                public ActionResult Index_Post(string top, string bottom)
                {
                    var identifier = Guid.NewGuid().ToString();
                    if (!Memes.ContainsKey(identifier))
                    {
                        Memes.Add(identifier, new Tuple<string, string>(top, bottom));
                    }
   
                    return Content("<a href=\"" + Url.Action("Show", new {id = identifier}) + "\">here's your meme</a>");
                }
   
                [OutputCache(VaryByParam = "*", Duration = 1, Location = OutputCacheLocation.Downstream)]
                public ActionResult Show(string id)
                {
                    Tuple<string, string> data = null;
                    if (!Memes.TryGetValue(id, out data))
                    {
                        return new HttpStatusCodeResult(HttpStatusCode.NotFound);
                    }
   
                    if (Debugger.IsAttached) // Preserve the debug experience
                    {
                        return Redirect(string.Format("/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
                    }
                    else // Get content from Azure CDN
                    {
                        return Redirect(string.Format("http://<yourCdnName>.azureedge.net/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
                    }
                }
   
                [OutputCache(VaryByParam = "*", Duration = 3600, Location = OutputCacheLocation.Downstream)]
                public ActionResult Generate(string top, string bottom)
                {
                    string imageFilePath = HostingEnvironment.MapPath("~/Content/chuck.bmp");
                    Bitmap bitmap = (Bitmap)Image.FromFile(imageFilePath);
   
                    using (Graphics graphics = Graphics.FromImage(bitmap))
                    {
                        SizeF size = new SizeF();
                        using (Font arialFont = FindBestFitFont(bitmap, graphics, top.ToUpperInvariant(), new Font("Arial Narrow", 100), out size))
                        {
                            graphics.DrawString(top.ToUpperInvariant(), arialFont, Brushes.White, new PointF(((bitmap.Width - size.Width) / 2), 10f));
                        }
                        using (Font arialFont = FindBestFitFont(bitmap, graphics, bottom.ToUpperInvariant(), new Font("Arial Narrow", 100), out size))
                        {
                            graphics.DrawString(bottom.ToUpperInvariant(), arialFont, Brushes.White, new PointF(((bitmap.Width - size.Width) / 2), bitmap.Height - 10f - arialFont.Height));
                        }
                    }
   
                    MemoryStream ms = new MemoryStream();
                    bitmap.Save(ms, System.Drawing.Imaging.ImageFormat.Png);
                    return File(ms.ToArray(), "image/png");
                }
   
                private Font FindBestFitFont(Image i, Graphics g, String text, Font font, out SizeF size)
                {
                    // Compute actual size, shrink if needed
                    while (true)
                    {
                        size = g.MeasureString(text, font);
   
                        // It fits, back out
                        if (size.Height < i.Height &&
                             size.Width < i.Width) { return font; }
   
                        // Try a smaller font (90% of old size)
                        Font oldFont = font;
                        font = new Font(font.Name, (float)(font.Size * .9), font.Style);
                        oldFont.Dispose();
                    }
                }
            }
        }
2. Fare clic con il pulsante destro del mouse sull'azione `Index()` predefinita e selezionare **Aggiungi visualizzazione**.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-6-addview.PNG)
3. Accettare le impostazioni di seguito e fare clic su **Aggiungi**.
   
   ![](media/cdn-cloud-service-with-cdn/cdn-7-configureview.PNG)
4. Aprire il nuovo file *Views\MemeGenerator\Index.cshtml* e sostituire il contenuto con il semplice HTML seguente per inviare i superlativi:
   
        <h2>Meme Generator</h2>
   
        <form action="" method="post">
            <input type="text" name="top" placeholder="Enter top text here" />
            <br />
            <input type="text" name="bottom" placeholder="Enter bottom text here" />
            <br />
            <input class="btn" type="submit" value="Generate meme" />
        </form>
5. Pubblicare nuovamente il servizio cloud e passare a **http://*&lt;serviceName>*.cloudapp.net/MemeGenerator/Index** nel browser.

Quando si inviano i valori del modulo a `/MemeGenerator/Index`, il metodo di azione `Index_Post` restituisce un collegamento al metodo di azione `Show` con il rispettivo identificatore di input. Facendo clic sul collegamento si raggiunge il codice seguente:  

    [OutputCache(VaryByParam = "*", Duration = 1, Location = OutputCacheLocation.Downstream)]
    public ActionResult Show(string id)
    {
        Tuple<string, string> data = null;
        if (!Memes.TryGetValue(id, out data))
        {
            return new HttpStatusCodeResult(HttpStatusCode.NotFound);
        }

        if (Debugger.IsAttached) // Preserve the debug experience
        {
            return Redirect(string.Format("/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
        }
        else // Get content from Azure CDN
        {
            return Redirect(string.Format("http://<yourCDNName>.azureedge.net/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
        }
    }

Se il debugger locale è collegato, si avrà una normale esperienza di debug con un reindirizzamento locale. Se viene eseguito nel servizio cloud, si verrà reindirizzati a:

    http://<yourCDNName>.azureedge.net/MemeGenerator/Generate?top=<formInput>&bottom=<formInput>

che corrisponde all'URL di origine seguente in corrispondenza dell'endpoint della rete CDN:

    http://<youCloudServiceName>.cloudapp.net/MemeGenerator/Generate?top=<formInput>&bottom=<formInput>


Sarà quindi possibile usare l'attributo `OutputCacheAttribute` sul metodo `Generate` per specificare come memorizzare nella cache il risultato dell'azione, che verrà rispettato dalla rete CDN di Azure. Il codice seguente specifica la scadenza di una cache entro un'ora (3.600 secondi).

    [OutputCache(VaryByParam = "*", Duration = 3600, Location = OutputCacheLocation.Downstream)]

Analogamente, è possibile rendere disponibile il contenuto da qualsiasi azione del controller nel servizio cloud attraverso la rete CDN di Azure, con l'opzione di memorizzazione nella cache desiderata.

Nella sezione successiva verrà illustrato come gestire gli script e i file CSS in bundle e minimizzati attraverso la rete CDN di Azure.

<a name="bundling"></a>

## <a name="integrate-aspnet-bundling-and-minification-with-azure-cdn"></a>Integrazione di creazione di bundle e minimizzazione ASP.NET con la rete CDN di Azure
Gli script e i fogli di stile CSS cambiano in maniera non frequente e sono i principali candidati per la cache della rete CDN di Azure. Il modo più semplice per integrare la creazione di bundle e la minimizzazione con la rete CDN di Azure consiste nel rendere disponibile l'intero ruolo Web. Tuttavia, poiché potrebbe non essere auspicabile, verrà illustrato come procedere pur mantenendo l'esperienza desiderata dallo sviluppatore per quanto riguarda la creazione di bundle e la minimizzazione ASP.NET, ad esempio:

* Ottima esperienza della modalità di debug
* Distribuzione semplificata
* Aggiornamenti immediati delle versioni di script/css dei client
* Meccanismo di fallback in caso di errore dell'endpoint della rete CDN
* Riduzione delle modifiche del codice

Nel progetto **WebRole1** creato nella sezione dedicata all'[integrazione di un endpoint della rete CDN di Azure con il sito Web di Azure e alla pubblicazione di contenuto statico nelle pagine Web di CDN di Azure](#deploy) aprire *App_Start\BundleConfig.cs* e osservare le chiamate del metodo `bundles.Add()`.

    public static void RegisterBundles(BundleCollection bundles)
    {
        bundles.Add(new ScriptBundle("~/bundles/jquery").Include(
                    "~/Scripts/jquery-{version}.js"));
        ...
    }

La prima istruzione `bundles.Add()` aggiunge un'aggregazione di script alla directory virtuale `~/bundles/jquery`. Aprire quindi *Views\Shared\_Layout.cshtml* per verificare come viene eseguito il rendering del bundle di script. Dovrebbe essere possibile trovare la riga di codice Razor seguente:

    @Scripts.Render("~/bundles/jquery")

Quando questo codice Razor viene eseguito nel ruolo Web di Azure, eseguirà il rendering di un tag `<script>` per il bundle di script in modo simile al seguente:

    <script src="/bundles/jquery?v=FVs3ACwOLIVInrAl5sdzR2jrCDmVOWFbZMY6g6Q0ulE1"></script>

Tuttavia, quando il codice viene eseguito in Visual Studio digitando `F5`, comporta il rendering individuale di ogni file di script nell'aggregazione (nel caso sopra citato, l'aggregazione contiene un solo file di script):

    <script src="/Scripts/jquery-1.10.2.js"></script>

Ciò consente di eseguire il debug del codice JavaScript nell'ambiente di sviluppo e allo stesso tempo di ridurre le connessioni client simultanee (creazione di bundle) e migliorare le prestazioni di download dei file (minimizzazione) in produzione. È un'ottima funzionalità da mantenere con l'integrazione nella rete CDN di Azure. Per di più, dal momento che il bundle di cui è stato eseguito il rendering contiene una stringa di versione generata automaticamente, è opportuno replicare tale funzionalità in modo che ogni volta che si aggiorna la versione di jQuery attraverso NuGet è possibile aggiornarla sul lato client non appena possibile.

Attenersi alla procedura seguente per integrare la creazione di bundle e la minimizzazione ASP.NET con l'endpoint della rete CDN.

1. Tornando ad *App_Start\BundleConfig.cs*, modificare i metodi `bundles.Add()` in modo da usare un [costruttore di aggregazioni](http://msdn.microsoft.com/library/jj646464.aspx) diverso, che specifichi un indirizzo di rete CDN. A questo scopo, sostituire la definizione del metodo `RegisterBundles` con il codice seguente:  
   
        public static void RegisterBundles(BundleCollection bundles)
        {
            bundles.UseCdn = true;
            var version = System.Reflection.Assembly.GetAssembly(typeof(Controllers.HomeController))
                .GetName().Version.ToString();
            var cdnUrl = "http://<yourCDNName>.azureedge.net/{0}?v=" + version;
   
            bundles.Add(new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "bundles/jquery")).Include(
                        "~/Scripts/jquery-{version}.js"));
   
            bundles.Add(new ScriptBundle("~/bundles/jqueryval", string.Format(cdnUrl, "bundles/jqueryval")).Include(
                        "~/Scripts/jquery.validate*"));
   
            // Use the development version of Modernizr to develop with and learn from. Then, when you're
            // ready for production, use the build tool at http://modernizr.com to pick only the tests you need.
            bundles.Add(new ScriptBundle("~/bundles/modernizr", string.Format(cdnUrl, "bundles/modernizer")).Include(
                        "~/Scripts/modernizr-*"));
   
            bundles.Add(new ScriptBundle("~/bundles/bootstrap", string.Format(cdnUrl, "bundles/bootstrap")).Include(
                        "~/Scripts/bootstrap.js",
                        "~/Scripts/respond.js"));
   
            bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css")).Include(
                        "~/Content/bootstrap.css",
                        "~/Content/site.css"));
        }
   
    Assicurarsi di sostituire `<yourCDNName>` con il nome della rete CDN.
   
    In altri termini, si imposta `bundles.UseCdn = true` e si aggiunge un URL della rete CDN definito con precisione a ogni aggregazione. Ad esempio, il primo costruttore nel codice:
   
        new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "bundles/jquery"))
   
    è lo stesso di:
   
        new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "http://<yourCDNName>.azureedge.net/bundles/jquery?v=<W.X.Y.Z>"))
   
    Questo costruttore comunica alle operazioni di creazione di bundle e minimizzazione ASP.NET di eseguire il rendering dei singoli file di script quando ne viene eseguito il debug a livello locale, ma di usare l'indirizzo della rete CDN specificato per accedere allo script in questione. Notare tuttavia due importanti caratteristiche di questo URL della rete CDN definito con precisione:
   
   * L'origine per questo URL della rete CDN è `http://<yourCloudService>.cloudapp.net/bundles/jquery?v=<W.X.Y.Z>`, che in realtà è la directory virtuale del bundle di script nel servizio cloud.
   * Poiché si sta usando un costruttore CDN, il tag dello script CDN per il bundle non contiene più la stringa di versione generata automaticamente nell'URL di cui è stato eseguito il rendering. È necessario generare manualmente una stringa di versione univoca ogni volta che il bundle di script viene modificato per forzare un mancato riscontro nella cache nella rete CDN di Azure. Allo stesso tempo, questa stringa di versione univoca deve rimanere costante per tutta la durata della distribuzione per aumentare i riscontri nella cache nella rete CDN di Azure dopo aver distribuito il bundle.
   * La stringa di query v=<W.X.Y.Z> effettua il pull da *Properties\AssemblyInfo.cs* nel progetto di ruolo Web. È possibile prevedere un flusso di lavoro di distribuzione che includa l'incremento della versione di assembly ogni volta che si pubblica su Azure. In alternativa, è possibile modificare solo il file *Properties\AssemblyInfo.cs* nel progetto per incrementare automaticamente la stringa di versione ogni volta che si compila, usando il carattere jolly '*'. ad esempio:
     
        [assembly: AssemblyVersion("1.0.0.*")]
     
     Qualsiasi altra strategia volta a semplificare la generazione di una stringa univoca per la durata della distribuzione avrà esito positivo.
2. Ripubblicare il servizio cloud e accedere alla home page.
3. Visualizzare il codice HTML relativo alla pagina. Dovrebbe essere possibile visualizzare l'URL della rete CDN di cui è stato eseguito il rendering, con una stringa di versione univoca ogni volta che si ripubblicano le modifiche al servizio cloud, Ad esempio:  
   
        ...
   
        <link href="http://camservice.azureedge.net/Content/css?v=1.0.0.25449" rel="stylesheet"/>
   
        <script src="http://camservice.azureedge.net/bundles/modernizer?v=1.0.0.25449"></script>
   
        ...
   
        <script src="http://camservice.azureedge.net/bundles/jquery?v=1.0.0.25449"></script>
   
        <script src="http://camservice.azureedge.net/bundles/bootstrap?v=1.0.0.25449"></script>
   
        ...
4. In Visual Studio eseguire il debug del servizio cloud digitando `F5`.
5. Visualizzare il codice HTML relativo alla pagina. Sarà ancora possibile visualizzare ciascun file di script di cui sia stato eseguito il rendering, in modo che l'esperienza di debug sia coerente in Visual Studio.  
   
        ...
   
            <link href="/Content/bootstrap.css" rel="stylesheet"/>
        <link href="/Content/site.css" rel="stylesheet"/>
   
            <script src="/Scripts/modernizr-2.6.2.js"></script>
   
        ...
   
            <script src="/Scripts/jquery-1.10.2.js"></script>
   
            <script src="/Scripts/bootstrap.js"></script>
        <script src="/Scripts/respond.js"></script>
   
        ...   

<a name="fallback"></a>

## <a name="fallback-mechanism-for-cdn-urls"></a>Meccanismo di fallback per gli URL della rete CDN
Se si verifica un errore nell'endpoint della rete CDN di Azure per un motivo qualsiasi, è consigliabile configurare l'accesso della pagina Web al server Web di origine come opzione di fallback per il caricamento di JavaScript o Bootstrap. Un conto è perdere le immagini nel sito a causa della mancata disponibilità della rete CDN, un altro è perdere funzionalità essenziali della pagina fornite dagli script e dai fogli di stile.

La classe [Bundle](http://msdn.microsoft.com/library/system.web.optimization.bundle.aspx) contiene una proprietà denominata [CdnFallbackExpression](http://msdn.microsoft.com/library/system.web.optimization.bundle.cdnfallbackexpression.aspx) che consente di configurare il meccanismo di fallback per l'errore della rete CDN. Per usare questa proprietà, seguire i passaggi descritti di seguito:

1. Nel progetto di ruolo Web, aprire *App_Start\BundleConfig.cs*, a cui è stato aggiunto un URL della rete CDN a ogni [costruttore di bundle](http://msdn.microsoft.com/library/jj646464.aspx) e apportare le modifiche evidenziate di seguito per aggiungere il meccanismo di fallback ai bundle predefiniti:  
   
        public static void RegisterBundles(BundleCollection bundles)
        {
            var version = System.Reflection.Assembly.GetAssembly(typeof(BundleConfig))
                .GetName().Version.ToString();
            var cdnUrl = "http://cdnurl.azureedge.net/.../{0}?" + version;
            bundles.UseCdn = true;
   
            bundles.Add(new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "bundles/jquery"))
                        { CdnFallbackExpression = "window.jquery" }
                        .Include("~/Scripts/jquery-{version}.js"));
   
            bundles.Add(new ScriptBundle("~/bundles/jqueryval", string.Format(cdnUrl, "bundles/jqueryval"))
                        { CdnFallbackExpression = "$.validator" }
                        .Include("~/Scripts/jquery.validate*"));
   
            // Use the development version of Modernizr to develop with and learn from. Then, when you&#39;re
            // ready for production, use the build tool at http://modernizr.com to pick only the tests you need.
            bundles.Add(new ScriptBundle("~/bundles/modernizr", string.Format(cdnUrl, "bundles/modernizer"))
                        { CdnFallbackExpression = "window.Modernizr" }
                        .Include("~/Scripts/modernizr-*"));
   
            bundles.Add(new ScriptBundle("~/bundles/bootstrap", string.Format(cdnUrl, "bundles/bootstrap"))     
                        { CdnFallbackExpression = "$.fn.modal" }
                        .Include(
                                  "~/Scripts/bootstrap.js",
                                  "~/Scripts/respond.js"));
   
            bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css")).Include(
                        "~/Content/bootstrap.css",
                        "~/Content/site.css"));
        }
   
    Quando `CdnFallbackExpression` non è Null, lo script viene inserito nel linguaggio HTML per provare se l'aggregazione è stata caricata correttamente. In caso contrario, accedere all'aggregazione direttamente dal server Web dell'origine. Questa proprietà deve essere impostata su un'espressione JavaScript che verifichi se il rispettivo bundle CDN è stato caricato correttamente. L'espressione necessaria per testare ogni bundle differisce in base al contenuto. Per i bundle predefiniti sopra riportati:
   
   * `window.jquery` viene definito nel file jquery-{version}.js
   * `$.validator` viene definito nel file jquery.validate.js
   * `window.Modernizr` viene definito nel file modernizer-{version}.js
   * `$.fn.modal` viene definito nel file bootstrap.js
     
     Come è possibile osservare, non è stata impostata la proprietà CdnFallbackExpression per l'aggregazione `~/Cointent/css`, perché attualmente esiste un [bug in System.Web.Optimization](https://aspnetoptimization.codeplex.com/workitem/104) che inserisce un tag `<script>` per il file CSS di fallback invece del tag `<link>` previsto.
     
     Un'ottima soluzione di [Fallback Style Bundle](https://github.com/EmberConsultingGroup/StyleBundleFallback) è tuttavia offerta da [Ember Consulting Group](https://github.com/EmberConsultingGroup).
2. Per usare la soluzione alternativa per CSS, creare un nuovo file .cs nella cartella *App_Start* del progetto di ruolo Web, denominato *StyleBundleExtensions.cs* e sostituirne il contenuto con il [codice di GitHub](https://github.com/EmberConsultingGroup/StyleBundleFallback/blob/master/Website/App_Start/StyleBundleExtensions.cs).
3. Nel file *App_Start\StyleFundleExtensions.cs*, rinominare lo spazio dei nomi con il nome del proprio ruolo Web (ad esempio **WebRole1**).
4. Tornare a `App_Start\BundleConfig.cs` e modificare l’ultima istruzione `bundles.Add` con il seguente codice evidenziato:  
   
        bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css"))
            <mark>.IncludeFallback("~/Content/css", "sr-only", "width", "1px")</mark>
            .Include(
                  "~/Content/bootstrap.css",
                  "~/Content/site.css"));
   
    Questo nuovo metodo di estensione si basa sulla stessa idea di inserire lo script nel linguaggio HTML per cercare in DOM il nome di classe, il nome di regola e il valore di regola corrispondenti definiti nel bundle CSS, eseguendo il fallback sul server Web in caso non riesca a trovare la corrispondenza.
5. Pubblicare di nuovo il servizio cloud e accedere alla home page.
6. Visualizzare il codice HTML relativo alla pagina. Gli script inseriti dovrebbero essere simili al seguente:    
   
        ...
   
        <link href="http://az632148.azureedge.net/Content/css?v=1.0.0.25474" rel="stylesheet"/>
        <script>(function() {
                        var loadFallback,
                            len = document.styleSheets.length;
                        for (var i = 0; i < len; i++) {
                            var sheet = document.styleSheets[i];
                            if (sheet.href.indexOf('http://camservice.azureedge.net/Content/css?v=1.0.0.25474') !== -1) {
                                var meta = document.createElement('meta');
                                meta.className = 'sr-only';
                                document.head.appendChild(meta);
                                var value = window.getComputedStyle(meta).getPropertyValue('width');
                                document.head.removeChild(meta);
                                if (value !== '1px') {
                                    document.write('<link href="/Content/css" rel="stylesheet" type="text/css" />');
                                }
                            }
                        }
                        return true;
                    }())||document.write('<script src="/Content/css"><\/script>');</script>
   
            <script src="http://camservice.azureedge.net/bundles/modernizer?v=1.0.0.25474"></script>
        <script>(window.Modernizr)||document.write('<script src="/bundles/modernizr"><\/script>');</script>
   
        ...
   
            <script src="http://camservice.azureedge.net/bundles/jquery?v=1.0.0.25474"></script>
        <script>(window.jquery)||document.write('<script src="/bundles/jquery"><\/script>');</script>
   
            <script src="http://camservice.azureedge.net/bundles/bootstrap?v=1.0.0.25474"></script>
        <script>($.fn.modal)||document.write('<script src="/bundles/bootstrap"><\/script>');</script>
   
        ...

    Si noti che lo script inserito per l'aggregazione CSS contiene ancora residui della proprietà `CdnFallbackExpression` nella riga:

        }())||document.write('<script src="/Content/css"><\/script>');</script>

    Poiché però la prima parte dell'espressione || restituirà sempre true (nella riga subito sopra), la funzione document.write() non verrà mai eseguita.

## <a name="more-information"></a>Altre informazioni
* [Panoramica della Rete per la distribuzione di contenuti (CDN) di Azure](http://msdn.microsoft.com/library/azure/ff919703.aspx)
* [Uso della rete CDN di Azure](cdn-create-new-endpoint.md)
* [Creazione di aggregazioni e minimizzazione ASP.NET](http://www.asp.net/mvc/tutorials/mvc-4/bundling-and-minification)

[new-cdn-profile]: ./media/cdn-cloud-service-with-cdn/cdn-new-profile.png
[cdn-profile-settings]: ./media/cdn-cloud-service-with-cdn/cdn-profile-settings.png
[cdn-new-endpoint-button]: ./media/cdn-cloud-service-with-cdn/cdn-new-endpoint-button.png
[cdn-add-endpoint]: ./media/cdn-cloud-service-with-cdn/cdn-add-endpoint.png
[cdn-endpoint-success]: ./media/cdn-cloud-service-with-cdn/cdn-endpoint-success.png
