---
title: un servizio cloud di Azure con la rete CDN Azure aaaIntegrate | Documenti Microsoft
description: Informazioni su come toodeploy un servizio cloud che fornisce contenuto da un endpoint rete CDN di Azure integrato
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
ms.openlocfilehash: f20d60b0b5edc133adf06d010633a15f62e2b8de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="intro"></a> Integrare un servizio cloud con la rete CDN di Azure
Un servizio cloud può essere integrato con una rete CDN di Azure, del contenuto dal percorso del servizio cloud hello. In questo modo di approccio hello seguenti vantaggi:

* Facile distribuzione e aggiornamento di immagini, script e fogli di stile nelle directory del progetto servizio cloud
* Aggiornare facilmente i pacchetti di NuGet hello nel servizio cloud, ad esempio jQuery o le versioni di Bootstrap
* Gestire l'applicazione Web e la rete CDN-serviti contenuti tutte da hello stessa interfaccia di Visual Studio
* Flusso di lavoro di distribuzione unificato per l'applicazione Web e il contenuto gestito dalla rete CDN
* Integrazione di creazione di bundle e minimizzazione ASP.NET con la rete CDN di Azure

## <a name="what-you-will-learn"></a>Contenuto dell'esercitazione
In questa esercitazione si apprenderà come:

* [Integrare un endpoint della rete CDN di Azure con il servizio cloud e rendere disponibile il contenuto statico nella pagine Web dalla rete CDN di Azure](#deploy)
* [Configurare le impostazioni della cache per il contenuto statico nel servizio cloud](#caching)
* [Gestire il contenuto dalle azioni del controller tramite la rete CDN di Azure](#controller)
* [Serve in bundle e minimizzare contenuto tramite rete CDN di Azure mantenendo script hello debug in Visual Studio](#bundling)
* [Configurare il fallback di script e file CSS quando la rete CDN di Azure è offline](#fallback)

## <a name="what-you-will-build"></a>Obiettivo di compilazione
Verrà distribuito un ruolo Web del servizio cloud utilizzando il modello di MVC ASP.NET predefinito di hello, aggiungere il contenuto di tooserve codice di una rete CDN Azure integrata, ad esempio un'immagine, i risultati dell'azione controller e i file di JavaScript e CSS di predefinito hello e anche scrivere hello tooconfigure codice meccanismo di fallback per bundle servita nell'evento hello che hello CDN è offline.

## <a name="what-you-will-need"></a>Prerequisiti
Per questa esercitazione sono hello seguenti prerequisiti:

* Un [account Microsoft Azure](/account/)
* Visual Studio 2015 con [Azure SDK](http://go.microsoft.com/fwlink/?linkid=518003&clcid=0x409)

> [!NOTE]
> È necessario un account di Azure di toocomplete questa esercitazione:
> 
> * È possibile [aprire un account Azure, gratuitamente](https://azure.microsoft.com/pricing/free-trial/) -si ottiene crediti è possibile utilizzare tootry out a pagamento di servizi di Azure e anche dopo che vengono utilizzati fino è possibile tenere conto di hello e liberare di utilizzare servizi di Azure, ad esempio siti Web.
> * È possibile [attivare i benefici della sottoscrizione MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/): con la sottoscrizione MSDN ogni mese si accumulano crediti che è possibile usare per i servizi di Azure a pagamento.
> 
> 

<a name="deploy"></a>

## <a name="deploy-a-cloud-service"></a>Distribuire un servizio cloud
In questa sezione, si verrà distribuito predefinito hello modello di applicazione MVC ASP.NET nel ruolo Web del servizio cloud tooa Visual Studio 2015 e quindi integrarlo con un nuovo endpoint CDN. Seguire le istruzioni di hello seguenti:

1. In Visual Studio 2015, creare un nuovo servizio cloud Azure dalla barra dei menu hello passando troppo**File > Nuovo > progetto > Cloud > servizio Cloud di Azure**. Assegnargli un nome e fare clic su **OK**.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-1-new-project.PNG)
2. Selezionare **ruolo Web ASP.NET** e fare clic su hello  **>**  pulsante. Fare clic su OK.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-2-select-role.PNG)
3. Selezionare **MVC** e fare clic su **OK**.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-3-mvc-template.PNG)
4. A questo punto, pubblicare questo tooan ruolo Web servizio cloud di Azure. Fare clic sul progetto servizio cloud hello e selezionare **pubblica**.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-4-publish-a.png)
5. Se non hanno ancora effettuato l'accesso a Microsoft Azure, fare clic su hello **aggiungere un account...**  hello elenco a discesa e fare clic su **aggiungere un account** voce di menu.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-5-publish-signin.png)
6. In hello-pagina di accesso, accedere con hello account Microsoft usato tooactivate l'account di Azure.
7. Una volta effettuato l'accesso, fare clic su **Avanti**.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-6-publish-signedin.png)
8. Supponendo che non sia stato creato un servizio cloud né un account di archiviazione, Visual Studio aiuterà a crearli entrambi. In hello **Crea servizio Cloud e Account** finestra di dialogo, nome del tipo hello servizio desiderato e la regione desiderata hello selezionare. Fare quindi clic su **Crea**.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-7-publish-createserviceandstorage.png)
9. In hello della pagina di impostazioni di pubblicazione, verificare la configurazione di hello e fare clic su **pubblica**.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-8-publish-finalize.png)
   
   > [!NOTE]
   > processo di pubblicazione per i servizi cloud Hello richiede molto tempo. Hello Abilita distribuzione Web per l'opzione di tutti i ruoli consentono di debug del servizio cloud molto più rapidamente, fornendo tooyour aggiornamenti veloce, ma temporanei, i ruoli Web. Per ulteriori informazioni su questa opzione, vedere [pubblicazione di un servizio Cloud utilizzando strumenti di Azure hello](http://msdn.microsoft.com/library/ff683672.aspx).
   > 
   > 
   
    Quando hello **Log attività di Microsoft Azure** indica che lo stato di pubblicazione è **completato**, si creerà un endpoint rete CDN è integrato con questo servizio cloud.
   
   > [!WARNING]
   > Se, dopo la pubblicazione, servizio cloud distribuito hello Visualizza una schermata di errore, è probabile perché è utilizzato da servizio cloud hello è stato distribuito un [guest del sistema operativo che non include .NET 4.5.2](../cloud-services/cloud-services-guestos-update-matrix.md#news-updates).  È possibile risolvere il problema da [distribuzione .NET 4.5.2 come attività di avvio](../cloud-services/cloud-services-dotnet-install-dotnet.md).
   > 
   > 

## <a name="create-a-new-cdn-profile"></a>Creare un nuovo profilo di rete CDN
Un profilo di rete CDN è una raccolta di endpoint della rete CDN.  Ogni profilo contiene uno o più endpoint della rete CDN.  È preferibile toouse più profili tooorganize gli endpoint CDN dal dominio internet, l'applicazione web o ad altri criteri.

> [!TIP]
> Se si dispone già di un profilo di rete CDN che si desidera toouse per questa esercitazione, andare troppo[creare un nuovo endpoint CDN](#create-a-new-cdn-endpoint).
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]

## <a name="create-a-new-cdn-endpoint"></a>Creare un nuovo endpoint della rete CDN
**toocreate un nuovo endpoint rete CDN per l'account di archiviazione**

1. In hello [il portale di gestione di Azure](https://portal.azure.com), passare il profilo CDN tooyour.  Si potrebbe avere aggiunto toohello dashboard nel passaggio precedente hello.  Se è, non sarà possibile trovarlo facendo **Sfoglia**, quindi **i profili di rete CDN**, e fare clic sul profilo hello prevede tooadd l'endpoint.
   
    verrà visualizzata la finestra di blade profilo rete CDN di Hello.
   
    ![Profilo di rete CDN][cdn-profile-settings]
2. Fare clic su hello **Aggiungi Endpoint** pulsante.
   
    ![Pulsante Aggiungi endpoint][cdn-new-endpoint-button]
   
    Hello **aggiungere un endpoint** pannello viene visualizzato.
   
    ![Pannello Aggiungi endpoint][cdn-add-endpoint]
3. Immettere un **Nome** per questo endpoint della rete CDN.  Questo nome verrà usato tooaccess le risorse memorizzate nella cache nel dominio hello `<EndpointName>.azureedge.net`.
4. In hello **tipo di origine** elenco a discesa Seleziona *servizio Cloud*.  
5. In hello **nome host dell'origine** elenco a discesa selezionare il servizio cloud.
6. Lasciare i valori predefiniti di hello per **il percorso di origine**, **intestazione host di origine**, e **porta protocollo/origine**.  È necessario specificare almeno un protocollo (HTTP o HTTPS).
7. Fare clic su hello **Aggiungi** toocreate pulsante hello nuovo endpoint.
8. Dopo aver creato endpoint hello, viene visualizzato in un elenco di endpoint per il profilo hello. visualizzazione elenco Hello Mostra hello URL toouse tooaccess memorizzati nella cache il contenuto, nonché il dominio di origine hello.
   
    ![Endpoint della rete CDN][cdn-endpoint-success]
   
   > [!NOTE]
   > endpoint di Hello non immediatamente sarà disponibile per l'utilizzo.  Operazione può richiedere minuti too90 hello registrazione toopropagate tramite rete CDN hello. Gli utenti che tentano di nome di dominio della rete CDN hello toouse immediatamente potrebbero ricevere il codice di stato 404 fino a quando non è disponibile tramite hello CDN contenuto hello.
   > 
   > 

## <a name="test-hello-cdn-endpoint"></a>Hello test endpoint rete CDN
Quando lo stato di pubblicazione hello è **completato**, aprire una finestra del browser e passare troppo**http://<cdnName>*.azureedge.net/Content/bootstrap.css**. Nella configurazione illustrata, questo URL è il seguente:

    http://camservice.azureedge.net/Content/bootstrap.css

Che corrisponde a toohello URL di origine all'endpoint rete CDN hello seguente:

    http://camcdnservice.cloudapp.net/Content/bootstrap.css

Quando ci si sposta troppo**http://*&lt;cdnName >*.azureedge.net/Content/bootstrap.css**, a seconda del browser, sarà richiesta toodownload o bootstrap.css hello aperto che proviene da un'applicazione Web pubblicata.

![](media/cdn-cloud-service-with-cdn/cdn-1-browser-access.PNG)

È possibile accedere in maniera simile a qualsiasi URL pubblicamente accessibile all'indirizzo **http://*&lt;nomeServizio>*.cloudapp.net/**, direttamente dall'endpoint della rete CDN. ad esempio:

* Un file. js dal percorso /Script hello
* Qualsiasi file di contenuto da hello /Content percorso
* Qualsiasi controller/azione
* Se la stringa di query hello è abilitata a endpoint della rete CDN, qualsiasi URL con stringhe di query

Infatti, con hello di sopra di configurazione, è possibile ospitare hello intero servizio cloud da  **http://*&lt;cdnName >*.azureedge.net/**. Se passa troppo**http://camservice.azureedge.net/ * *, ottenere il risultato di azione hello da Home/Index.

![](media/cdn-cloud-service-with-cdn/cdn-2-home-page.PNG)

Ciò significa, tuttavia, che è sempre tooserve una buona idea un intero servizio cloud tramite rete CDN di Azure. 

Una rete CDN con l'ottimizzazione di recapito statico non necessariamente velocizzare il recapito di asset dinamico che non sono memorizzati nella cache toobe o vengono aggiornati con una frequenza elevata, poiché hello CDN è necessario inserire una nuova versione di asset hello dal server di origine hello molto spesso. Per questo scenario, è possibile abilitare [accelerazione di sito dinamico](cdn-dynamic-site-acceleration.md) ottimizzazione (DSA) per l'endpoint rete CDN che usa diverse tecniche toospeed le opzioni di distribuzione di asset dinamico non memorizzabile nella cache. 

Se si dispone di un sito con una combinazione di contenuto statico e dinamico, è possibile scegliere tooserve contenuto statico dalla rete CDN con un tipo di ottimizzazione statiche (ad esempio recapito web generali) il contenuto dinamico tooserve direttamente dal server di origine hello o tramite una rete CDN endpoint con l'ottimizzazione DSA attivata caso per caso. toothat fine, è già stato illustrato come i file di contenuto di singoli tooaccess dall'endpoint rete CDN hello. Illustra come tooserve un'azione del controller specifico tramite un endpoint rete CDN specifico in servire contenuto da azioni del controller tramite la rete CDN Azure.

In alternativa Hello è toodetermine quale contenuto tooserve dalla rete CDN di Azure nel caso per caso nel servizio cloud. toothat fine, è già stato illustrato come i file di contenuto di singoli tooaccess dall'endpoint rete CDN hello. Si vedrà come tooserve un'azione del controller specifico tramite hello endpoint rete CDN in [Distribuisci il contenuto da azioni del controller tramite la rete CDN Azure](#controller).

<a name="caching"></a>

## <a name="configure-caching-options-for-static-files-in-your-cloud-service"></a>Configurare le opzioni di memorizzazione nella cache dei file statici nel servizio cloud
Con l'integrazione della rete CDN di Azure nel servizio cloud, è possibile specificare come si desidera statico toobe contenuto memorizzato nella cache in endpoint rete CDN hello. toodo, aprire *Web. config* dal ruolo Web del progetto (ad esempio WebRole1) e aggiungere un `<staticContent>` elemento troppo`<system.webServer>`. Hello XML riportato di seguito consente di configurare tooexpire cache di hello dopo 3 giorni.  

    <system.webServer>
      <staticContent>
        <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="3.00:00:00"/>
      </staticContent>
      ...
    </system.webServer>

Una volta fatto questo, tutti i file statici nel servizio cloud verranno considerato hello stessa regola presenti nella cache della rete CDN. Per un controllo più granulare delle impostazioni della cache, aggiungere un file *Web.config* in una cartella e quindi aggiungervi le impostazioni. Ad esempio, aggiungere un *Web. config* file toohello *\Content* cartella e sostituire hello contenuto con hello XML seguente:

    <?xml version="1.0"?>
    <configuration>
      <system.webServer>
        <staticContent>
          <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="15.00:00:00"/>
        </staticContent>
      </system.webServer>
    </configuration>

Questa impostazione, tutti i file statici dal hello *\Content* toobe cartella memorizzata nella cache per 15 giorni.

Per ulteriori informazioni su come hello tooconfigure `<clientCache>` elemento, vedere [nella Cache del Client &lt;clientCache >](http://www.iis.net/configreference/system.webserver/staticcontent/clientcache).

In [Distribuisci il contenuto da azioni del controller tramite la rete CDN Azure](#controller), apprenderà inoltre come è possibile configurare le impostazioni della cache per i risultati dell'azione controller in hello cache della rete CDN.

<a name="controller"></a>

## <a name="serve-content-from-controller-actions-through-azure-cdn"></a>Gestire il contenuto dalle azioni del controller attraverso la rete CDN di Azure
Quando si integra un ruolo Web del servizio cloud con rete CDN di Azure, è contenuto tooserve relativamente facile da azioni del controller tramite hello rete CDN di Azure. Individuare il cloud service direttamente tramite rete CDN di Azure (illustrato in precedenza), [Maarten Balliauw](https://twitter.com/maartenballiauw) illustra come toodo con una divertente controller MemeGenerator [riducendo la latenza del sito Web hello con hello rete CDN di Azure ](http://channel9.msdn.com/events/TechDays/Techdays-2014-the-Netherlands/Reducing-latency-on-the-web-with-the-Windows-Azure-CDN). che viene riprodotto semplicemente in questo articolo.

Si supponga che nel servizio cloud desiderato memes toogenerate basata su un'immagine di Chuck Norris giovane (foto da [Alan Light](http://www.flickr.com/photos/alan-light/218493788/)) come segue:

![](media/cdn-cloud-service-with-cdn/cdn-5-memegenerator.PNG)

Si dispone di una semplice `Index` azione che consente ai clienti di hello superlatives hello toospecify nell'immagine di hello, quindi genera l'errore hello meme dopo INVIO toohello azione. Poiché si tratta di Chuck Norris, che ci si aspetta toobecome questa pagina notevolmente più diffusi a livello globale. È un ottimo esempio di come gestire contenuto semi dinamico con la rete CDN di Azure.

Seguire i passaggi di hello sopra toosetup questa azione del controller:

1. In hello *\Controllers* cartella, creare un nuovo file con estensione cs denominato *MemeGeneratorController.cs* e hello sostituire il contenuto con hello seguente codice. Impossibile verificare tooreplace hello nella parte evidenziata con il nome della rete CDN.  
   
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
   
                    if (Debugger.IsAttached) // Preserve hello debug experience
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
2. Fare doppio clic nella predefinito hello `Index()` azione e selezionare **Aggiungi visualizzazione**.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-6-addview.PNG)
3. Accettare le impostazioni di hello riportate di seguito e fare clic su **Aggiungi**.
   
   ![](media/cdn-cloud-service-with-cdn/cdn-7-configureview.PNG)
4. Aprire hello nuovo *Views\MemeGenerator\Index.cshtml* e sostituire il contenuto di hello con hello seguente HTML semplice per l'invio di superlatives hello:
   
        <h2>Meme Generator</h2>
   
        <form action="" method="post">
            <input type="text" name="top" placeholder="Enter top text here" />
            <br />
            <input type="text" name="bottom" placeholder="Enter bottom text here" />
            <br />
            <input class="btn" type="submit" value="Generate meme" />
        </form>
5. Pubblicare di nuovo servizio cloud hello e passare troppo**http://*&lt;serviceName >*.cloudapp.net/MemeGenerator/Index** nel browser.

Quando si inviano i valori del form hello troppo`/MemeGenerator/Index`, hello `Index_Post` metodo di azione restituisce un collegamento di toohello `Show` metodo di azione con l'identificatore dell'input rispettivi hello. Quando si fa clic sul collegamento hello, raggiungere hello seguente codice:  

    [OutputCache(VaryByParam = "*", Duration = 1, Location = OutputCacheLocation.Downstream)]
    public ActionResult Show(string id)
    {
        Tuple<string, string> data = null;
        if (!Memes.TryGetValue(id, out data))
        {
            return new HttpStatusCodeResult(HttpStatusCode.NotFound);
        }

        if (Debugger.IsAttached) // Preserve hello debug experience
        {
            return Redirect(string.Format("/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
        }
        else // Get content from Azure CDN
        {
            return Redirect(string.Format("http://<yourCDNName>.azureedge.net/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
        }
    }

Se è collegato il debugger locale, si otterrà esperienza di debug regolare hello con un reindirizzamento locale. Se è in esecuzione nel servizio cloud hello, verrà reindirizzare a:

    http://<yourCDNName>.azureedge.net/MemeGenerator/Generate?top=<formInput>&bottom=<formInput>

Che corrisponde a toohello seguente URL di origine all'endpoint della rete CDN:

    http://<youCloudServiceName>.cloudapp.net/MemeGenerator/Generate?top=<formInput>&bottom=<formInput>


È quindi possibile utilizzare hello `OutputCacheAttribute` attributo hello `Generate` toospecify metodo come risultato dell'azione hello deve essere memorizzato nella cache, che rispetta rete CDN di Azure. codice Hello seguente specificare una scadenza della cache di 1 ora (3.600 secondi).

    [OutputCache(VaryByParam = "*", Duration = 3600, Location = OutputCacheLocation.Downstream)]

Analogamente, può essere utilizzato il contenuto da qualsiasi azione del controller nel servizio cloud tramite la rete CDN di Azure, con l'opzione di memorizzazione nella cache di hello desiderato.

Nella sezione successiva hello, vi mostrerò come tooserve hello in bundle e minimizzare gli script e CSS tramite rete CDN di Azure.

<a name="bundling"></a>

## <a name="integrate-aspnet-bundling-and-minification-with-azure-cdn"></a>Integrazione di creazione di bundle e minimizzazione ASP.NET con la rete CDN di Azure
Fogli di stile CSS e gli script non vengono modificati spesso e sono candidati ideali per hello cache rete CDN di Azure. Servono hello intero ruolo Web tramite la rete CDN di Azure è toointegrate modo più semplice hello minimizzazione con rete CDN di Azure e aggregazione. Tuttavia, come si può non desidera toodo, vi mostrerò come toodo, mantenendo hello desiderato esperienza per sviluppatori di aggregazione di ASP.NET e di riduzione, ad esempio:

* Ottima esperienza della modalità di debug
* Distribuzione semplificata
* Tooclients immediata di aggiornamenti per gli aggiornamenti di versione script/CSS
* Meccanismo di fallback in caso di errore dell'endpoint della rete CDN
* Riduzione delle modifiche del codice

In hello **WebRole1** progetto creato in [integrare un endpoint rete CDN di Azure con il sito Web di Azure e fornire contenuto statico delle pagine Web dalla rete CDN di Azure](#deploy)aprire *App_Start\ BundleConfig.cs* e dare un'occhiata hello `bundles.Add()` chiamate al metodo.

    public static void RegisterBundles(BundleCollection bundles)
    {
        bundles.Add(new ScriptBundle("~/bundles/jquery").Include(
                    "~/Scripts/jquery-{version}.js"));
        ...
    }

prima di Hello `bundles.Add()` istruzione consente di aggiungere un bundle di script alla directory virtuale hello `~/bundles/jquery`. Aprire quindi *Views\Shared\_cshtml* toosee la modalità con cui viene eseguito il rendering di tag di hello script bundle. Dovrebbe essere in grado di toofind hello successiva riga di codice Razor:

    @Scripts.Render("~/bundles/jquery")

Quando questo codice Razor viene eseguito nel ruolo Web Azure hello, esegue il rendering di un `<script>` tag per hello seguente toohello simile bundle di script:

    <script src="/bundles/jquery?v=FVs3ACwOLIVInrAl5sdzR2jrCDmVOWFbZMY6g6Q0ulE1"></script>

Tuttavia, quando viene eseguito in Visual Studio digitando `F5`, esegue il rendering di ogni file di script nel bundle hello singolarmente (in caso di hello precedente, solo un file script è in bundle hello):

    <script src="/Scripts/jquery-1.10.2.js"></script>

In questo modo il codice JavaScript hello toodebug nell'ambiente di sviluppo mentre riducendo le connessioni client simultanee (aggregazione) e file di miglioramento delle prestazioni di scaricamento (minimizzazione) nell'ambiente di produzione. È un toopreserve grande funzionalità con l'integrazione della rete CDN di Azure. Inoltre, poiché bundle hello sottoposto a rendering contiene già una stringa di versione generato automaticamente, si desidera tooreplicate che funzionalità hello pertanto quando si aggiorna la versione di jQuery tramite NuGet, possono essere aggiornato sul lato client hello appena possibili.

Eseguire operazioni di hello seguenti toointegration ASP.NET aggregazione e minimizzazione con l'endpoint CDN.

1. In *App_Start\BundleConfig.cs*, modificare hello `bundles.Add()` toouse metodi un altro [costruttore Bundle](http://msdn.microsoft.com/library/jj646464.aspx), uno che specifica un indirizzo di rete CDN. toodo hello, sostituire `RegisterBundles` definizione di metodo con hello seguente codice:  
   
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
   
            // Use hello development version of Modernizr toodevelop with and learn from. Then, when you're
            // ready for production, use hello build tool at http://modernizr.com toopick only hello tests you need.
            bundles.Add(new ScriptBundle("~/bundles/modernizr", string.Format(cdnUrl, "bundles/modernizer")).Include(
                        "~/Scripts/modernizr-*"));
   
            bundles.Add(new ScriptBundle("~/bundles/bootstrap", string.Format(cdnUrl, "bundles/bootstrap")).Include(
                        "~/Scripts/bootstrap.js",
                        "~/Scripts/respond.js"));
   
            bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css")).Include(
                        "~/Content/bootstrap.css",
                        "~/Content/site.css"));
        }
   
    Tooreplace assicurarsi di essere `<yourCDNName>` con nome hello della rete CDN di Azure.
   
    In parole semplici, si imposta `bundles.UseCdn = true` e aggiunta di un bundle di tooeach appositamente URL della rete CDN. Ad esempio, hello primo costruttore nel codice hello:
   
        new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "bundles/jquery"))
   
    è hello uguale a:
   
        new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "http://<yourCDNName>.azureedge.net/bundles/jquery?v=<W.X.Y.Z>"))
   
    Questo costruttore indica aggregazione ASP.NET e minimizzazione toorender singoli file di script durante il debug in locale, ma utilizzare hello specificato in questione script hello tooaccess indirizzi della rete CDN. Notare tuttavia due importanti caratteristiche di questo URL della rete CDN definito con precisione:
   
   * l'origine per l'URL della rete CDN Hello è `http://<yourCloudService>.cloudapp.net/bundles/jquery?v=<W.X.Y.Z>`, che è effettivamente hello directory virtuale del bundle di script hello nel servizio cloud.
   * Poiché si utilizza il costruttore della rete CDN, hello tag di script della rete CDN per il bundle di hello non contiene la stringa di versione hello generato automaticamente in hello rendering URL. È necessario generare una stringa di versione univoci manualmente ogni volta che l'aggregazione di script hello tooforce modificato non è disponibile una cache all'interno della rete CDN di Azure. AT hello stesso tempo, la stringa di versione univoci deve rimanere costante tramite vita hello di riscontri nella cache di hello distribuzione toomaximize all'interno della rete CDN di Azure dopo aver distribuito il pacchetto di hello.
   * stringa di query v Hello = < w.x.y. z > esegue il pull da *Properties \ AssemblyInfo.cs* nel progetto di ruolo Web. È possibile disporre di un flusso di lavoro di distribuzione che include l'incremento di versione dell'assembly hello ogni volta che si pubblica tooAzure. In alternativa, è possibile solo modificare *Properties \ AssemblyInfo.cs* nella stringa di versione del progetto tooautomatically incremento hello ogni volta che si compila, con carattere jolly hello ' *'. ad esempio:
     
        [assembly: AssemblyVersion("1.0.0.*")]
     
     Altri toostreamline strategia generando una stringa univoca per la durata hello di una distribuzione funzionerà qui.
2. Ripubblicare hello cloud service e accesso hello la home page.
3. Il codice HTML per la pagina hello hello di visualizzazione. È necessario essere in grado di toosee hello URL CDN sottoposto a rendering, con una stringa di versione univoca ogni volta che si ripubblica servizio cloud tooyour di modifiche. ad esempio:  
   
        ...
   
        <link href="http://camservice.azureedge.net/Content/css?v=1.0.0.25449" rel="stylesheet"/>
   
        <script src="http://camservice.azureedge.net/bundles/modernizer?v=1.0.0.25449"></script>
   
        ...
   
        <script src="http://camservice.azureedge.net/bundles/jquery?v=1.0.0.25449"></script>
   
        <script src="http://camservice.azureedge.net/bundles/bootstrap?v=1.0.0.25449"></script>
   
        ...
4. In Visual Studio, eseguire il debug del servizio cloud hello in Visual Studio digitando `F5`.,
5. Il codice HTML per la pagina hello hello di visualizzazione. Sarà ancora possibile visualizzare ciascun file di script di cui sia stato eseguito il rendering, in modo che l'esperienza di debug sia coerente in Visual Studio.  
   
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
Quando l'endpoint rete CDN di Azure non riesce per qualsiasi motivo, è opportuno toobe la pagina Web smart sufficiente tooaccess al server Web di origine come opzione di fallback per il caricamento di JavaScript o Bootstrap hello. È abbastanza grave toolose immagini nel sito Web a causa di mancata disponibilità tooCDN ma molto più gravi funzionalità della pagina fondamentale toolose fornito da script e fogli di stile.

Hello [Bundle](http://msdn.microsoft.com/library/system.web.optimization.bundle.aspx) classe contiene una proprietà denominata [CdnFallbackExpression](http://msdn.microsoft.com/library/system.web.optimization.bundle.cdnfallbackexpression.aspx) che consente di meccanismo di fallback hello tooconfigure di errore della rete CDN. toouse questa proprietà, seguire hello passaggi riportati di seguito:

1. Nel progetto di ruolo Web, aprire *App_Start\BundleConfig.cs*, cui è stato aggiunto un URL della rete CDN in ogni [costruttore Bundle](http://msdn.microsoft.com/library/jj646464.aspx)e seguenti hello evidenziato cambia tooadd meccanismo di fallback toohello bundle predefinita:  
   
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
   
            // Use hello development version of Modernizr toodevelop with and learn from. Then, when you&#39;re
            // ready for production, use hello build tool at http://modernizr.com toopick only hello tests you need.
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
   
    Quando `CdnFallbackExpression` è non null, script, viene inserito nelle tootest hello HTML se è stata caricata bundle hello e, in caso contrario, hello bundle di accedere direttamente dal server Web di origine hello. Questa proprietà deve toobe set tooa JavaScript espressione che controlla se bundle CDN rispettivi hello è caricata correttamente. espressione Hello necessari tootest ogni bundle è diverso in base toohello contenuto. Per i pacchetti predefiniti hello precedente:
   
   * `window.jquery` viene definito nel file jquery-{version}.js
   * `$.validator` viene definito nel file jquery.validate.js
   * `window.Modernizr` viene definito nel file modernizer-{version}.js
   * `$.fn.modal` viene definito nel file bootstrap.js
     
     È possibile notare che non è stata impostata CdnFallbackExpression per hello `~/Cointent/css` bundle. In questo modo è attualmente presente una [bug in System.Web.Optimization](https://aspnetoptimization.codeplex.com/workitem/104) che inserisce un `<script>` tag per hello fallback CSS anziché hello previsto `<link>` tag.
     
     Un'ottima soluzione di [Fallback Style Bundle](https://github.com/EmberConsultingGroup/StyleBundleFallback) è tuttavia offerta da [Ember Consulting Group](https://github.com/EmberConsultingGroup).
2. soluzione alternativa hello toouse per CSS, creare un nuovo file con estensione cs del progetto di ruolo Web *App_Start* cartella denominata *StyleBundleExtensions.cs*e sostituirne il contenuto con hello [il codice da GitHub](https://github.com/EmberConsultingGroup/StyleBundleFallback/blob/master/Website/App_Start/StyleBundleExtensions.cs).
3. In *App_Start\StyleFundleExtensions.cs*, rinominare il nome del ruolo di hello dello spazio dei nomi tooyour Web (ad esempio **WebRole1**).
4. Tornare indietro troppo`App_Start\BundleConfig.cs` e modificare hello ultima `bundles.Add` istruzione con hello codice evidenziato di seguito:  
   
        bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css"))
            <mark>.IncludeFallback("~/Content/css", "sr-only", "width", "1px")</mark>
            .Include(
                  "~/Content/bootstrap.css",
                  "~/Content/site.css"));
   
    Questo nuovo metodo di estensione Usa hello stesso concetto tooinject script in hello HTML toocheck hello DOM per hello un nome di classe corrispondente, il nome della regola e il valore di regola definita in bundle CSS hello e cade toohello indietro server Web di origine in caso di corrispondenza hello toofind.
5. Pubblicare nuovamente i servizi cloud di hello e accesso hello home page.
6. Il codice HTML per la pagina hello hello di visualizzazione. È necessario trovare script inserito simile toohello seguenti:    
   
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

    Si noti che uno script per il bundle CSS hello contiene ancora rimanente e volontariamente hello da hello `CdnFallbackExpression` proprietà nella riga hello:

        }())||document.write('<script src="/Content/css"><\/script>');</script>

    Ma, poiché hello prima parte hello | | espressione restituirà sempre true (nella riga hello direttamente sopra), la funzione Document hello non verrà mai eseguito.

## <a name="more-information"></a>Altre informazioni
* [Panoramica di hello Azure rete CDN (Content Delivery)](http://msdn.microsoft.com/library/azure/ff919703.aspx)
* [Uso della rete CDN di Azure](cdn-create-new-endpoint.md)
* [Creazione di aggregazioni e minimizzazione ASP.NET](http://www.asp.net/mvc/tutorials/mvc-4/bundling-and-minification)

[new-cdn-profile]: ./media/cdn-cloud-service-with-cdn/cdn-new-profile.png
[cdn-profile-settings]: ./media/cdn-cloud-service-with-cdn/cdn-profile-settings.png
[cdn-new-endpoint-button]: ./media/cdn-cloud-service-with-cdn/cdn-new-endpoint-button.png
[cdn-add-endpoint]: ./media/cdn-cloud-service-with-cdn/cdn-add-endpoint.png
[cdn-endpoint-success]: ./media/cdn-cloud-service-with-cdn/cdn-endpoint-success.png
