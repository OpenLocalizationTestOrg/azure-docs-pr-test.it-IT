---
title: App del servizio web app aaaAzure estensioni e configurazioni avanzate
description: Utilizzare file ApplicationHost. config del servizio App di Azure web app tooadd le estensioni private tooenable amministrazione personalizzato azioni e Transformation(XDT) documento XML dichiarazioni tootransform hello.
author: cephalin
writer: cephalin
editor: mollybos
manager: erikre
services: app-service
documentationcenter: 
ms.assetid: b441a286-ef38-4abc-b102-cdb249baf5bc
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/25/2016
ms.author: cephalin
ms.openlocfilehash: 873347ac13113d1ac989cba29128382c81dcfcca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-web-app-advanced-config-and-extensions"></a><span data-ttu-id="5a39a-103">Configurazione avanzata ed estensioni dell'app Web di Servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="5a39a-103">Azure App Service web app advanced config and extensions</span></span>
<span data-ttu-id="5a39a-104">Utilizzando [trasformazione di documenti XML](http://msdn.microsoft.com/library/dd465326.aspx) dichiarazioni (XDT), è possibile trasformare hello [applicationHost. config](http://www.iis.net/learn/get-started/planning-your-iis-architecture/introduction-to-applicationhostconfig) file nell'app web in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="5a39a-104">By using [XML Document Transformation](http://msdn.microsoft.com/library/dd465326.aspx) (XDT) declarations, you can transform hello [ApplicationHost.config](http://www.iis.net/learn/get-started/planning-your-iis-architecture/introduction-to-applicationhostconfig) file in your web app in Azure App Service.</span></span> <span data-ttu-id="5a39a-105">È possibile utilizzare anche XDT dichiarazioni tooadd le estensioni private tooenable web personalizzato app le azioni di amministrazione.</span><span class="sxs-lookup"><span data-stu-id="5a39a-105">You can also use XDT declarations tooadd private extensions tooenable custom web app administration actions.</span></span> <span data-ttu-id="5a39a-106">In questo articolo è disponibile un'estensione dell'app PHP Manager di esempio, che consente la gestione di impostazioni PHP mediante un'interfaccia Web.</span><span class="sxs-lookup"><span data-stu-id="5a39a-106">This article includes a sample PHP Manager web app extension that enables management of PHP settings through a web interface.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <span data-ttu-id="5a39a-107"><a id="transform"></a>Configurazione avanzata tramite ApplicationHost.config</span><span class="sxs-lookup"><span data-stu-id="5a39a-107"><a id="transform"></a>Advanced configuration through ApplicationHost.config</span></span>
<span data-ttu-id="5a39a-108">piattaforma del servizio App Hello offre flessibilità e controllo per la configurazione di app web.</span><span class="sxs-lookup"><span data-stu-id="5a39a-108">hello App Service platform provides flexibility and control for web app configuration.</span></span> <span data-ttu-id="5a39a-109">Anche se i file di configurazione applicationHost. config IIS standard hello non è disponibile per la modifica diretta nel servizio App, piattaforma hello supporta un modello di trasformazione applicationHost. config dichiarativo basato su XML documento trasformazione (XDT).</span><span class="sxs-lookup"><span data-stu-id="5a39a-109">Although hello standard IIS ApplicationHost.config configuration file is not available for direct editing in App Service, hello platform supports a declarative ApplicationHost.config transform model based on XML Document Transformation (XDT).</span></span>

<span data-ttu-id="5a39a-110">tooleverage questa funzionalità di trasformazione, creare un file ApplicationHost.xdt con XDT contenuto e inserire nella radice del sito hello (d:\home\site) hello [Kudu Console](https://github.com/projectkudu/kudu/wiki/Kudu-console).</span><span class="sxs-lookup"><span data-stu-id="5a39a-110">tooleverage this transform functionality, you create an ApplicationHost.xdt file with XDT content and place under hello site root (d:\home\site) in hello [Kudu Console](https://github.com/projectkudu/kudu/wiki/Kudu-console).</span></span> <span data-ttu-id="5a39a-111">Per effetto di tootake modifiche potrebbe essere necessario toorestart hello App Web.</span><span class="sxs-lookup"><span data-stu-id="5a39a-111">You may need toorestart hello Web App for changes tootake effect.</span></span>

<span data-ttu-id="5a39a-112">Hello applicationHost.xdt esempio seguente viene illustrato come un nuovo tooa variabile di ambiente personalizzato tooadd web app che utilizza PHP 5.4.</span><span class="sxs-lookup"><span data-stu-id="5a39a-112">hello following applicationHost.xdt sample shows how tooadd a new custom environment variable tooa web app that uses PHP 5.4.</span></span>

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
  <system.webServer>
    <fastCgi>
      <application>
        <environmentVariables>
          <environmentVariable name="CONFIGTEST" value="TEST" xdt:Transform="Insert" xdt:Locator="XPath(/configuration/system.webServer/fastCgi/application[contains(@fullPath,'5.4')]/environmentVariables)" />
        </environmentVariables>
      </application>
    </fastCgi>
  </system.webServer>
</configuration>
```

<span data-ttu-id="5a39a-113">È disponibile dalla radice FTP hello in LogFiles\Transform un file di log con lo stato di trasformazione e dettagli.</span><span class="sxs-lookup"><span data-stu-id="5a39a-113">A log file with transform status and details is available from hello FTP root under LogFiles\Transform.</span></span>

<span data-ttu-id="5a39a-114">Per esempi aggiuntivi, vedere [https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples](https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples).</span><span class="sxs-lookup"><span data-stu-id="5a39a-114">For additional samples, see [https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples](https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples).</span></span>

<span data-ttu-id="5a39a-115">**Nota**</span><span class="sxs-lookup"><span data-stu-id="5a39a-115">**Note**</span></span><br />
<span data-ttu-id="5a39a-116">Gli elementi dall'elenco di hello dei moduli in `system.webServer` non possono essere rimossi o riordinati, ma è possibile elenco toohello aggiunte.</span><span class="sxs-lookup"><span data-stu-id="5a39a-116">Elements from hello list of modules under `system.webServer` cannot be removed or reordered, but additions toohello list are possible.</span></span>

## <span data-ttu-id="5a39a-117"><a id="extend"></a> Estendere l'app Web</span><span class="sxs-lookup"><span data-stu-id="5a39a-117"><a id="extend"></a> Extend your web app</span></span>
### <span data-ttu-id="5a39a-118"><a id="overview"></a> Panoramica delle estensioni di app Web private</span><span class="sxs-lookup"><span data-stu-id="5a39a-118"><a id="overview"></a> Overview of private web app extensions</span></span>
<span data-ttu-id="5a39a-119">Servizi app supporta le estensioni di app Web come punto di estensibilità per le azioni di amministrazione.</span><span class="sxs-lookup"><span data-stu-id="5a39a-119">App Service supports web app extensions as an extensibility point for administrative actions.</span></span> <span data-ttu-id="5a39a-120">Alcune funzionalità della piattaforma Servizio app sono in effetti implementate come estensioni preinstallate.</span><span class="sxs-lookup"><span data-stu-id="5a39a-120">In fact, some App Service platform features are implemented as pre-installed extensions.</span></span> <span data-ttu-id="5a39a-121">Mentre hello piattaforma pre-installate estensioni non possono essere modificate, è possibile creare e configurare le estensioni private per un'app web.</span><span class="sxs-lookup"><span data-stu-id="5a39a-121">While hello pre-installed platform extensions cannot be modified, you can create and configure private extensions for your own web app.</span></span> <span data-ttu-id="5a39a-122">Questa funzionalità si basa anche sulle dichiarazioni XDT.</span><span class="sxs-lookup"><span data-stu-id="5a39a-122">This functionality also relies on XDT declarations.</span></span> <span data-ttu-id="5a39a-123">Hello chiave per la creazione di un'estensione dell'app web privata passaggi seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="5a39a-123">hello key steps for creating a private web app extension are hello following:</span></span>

1. <span data-ttu-id="5a39a-124">Estensione di app Web **content**: creare applicazioni Web supportate da Servizio app</span><span class="sxs-lookup"><span data-stu-id="5a39a-124">Web app extension **content**: create any web application supported by App Service</span></span>
2. <span data-ttu-id="5a39a-125">Estensione di app Web **declaration**: creare un file ApplicationHost.xdt</span><span class="sxs-lookup"><span data-stu-id="5a39a-125">Web app extension **declaration**: create an ApplicationHost.xdt file</span></span>
3. <span data-ttu-id="5a39a-126">Estensione app Web **distribuzione**: posizionare il contenuto nella cartella SiteExtensions hello in`root`</span><span class="sxs-lookup"><span data-stu-id="5a39a-126">Web app extension **deployment**: place content in hello SiteExtensions folder under `root`</span></span>

<span data-ttu-id="5a39a-127">I collegamenti interni per l'app web hello devono puntare tooa toohello relativo applicazione percorso specificato nel file ApplicationHost.xdt hello.</span><span class="sxs-lookup"><span data-stu-id="5a39a-127">Internal links for hello web app should point tooa path relative toohello application path specified in hello ApplicationHost.xdt file.</span></span> <span data-ttu-id="5a39a-128">Qualsiasi file ApplicationHost.xdt toohello delle modifiche richiede un riciclo di app web.</span><span class="sxs-lookup"><span data-stu-id="5a39a-128">Any change toohello ApplicationHost.xdt file requires a web app recycle.</span></span>

<span data-ttu-id="5a39a-129">**Nota**: informazioni aggiuntive relative a questi elementi chiave sono disponibili all'indirizzo [https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions](https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions).</span><span class="sxs-lookup"><span data-stu-id="5a39a-129">**Note**: Additional information for these key elements is available at [https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions](https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions).</span></span>

<span data-ttu-id="5a39a-130">Un esempio dettagliato è incluso tooillustrate hello passaggi per la creazione e l'abilitazione di un'estensione dell'app web privato.</span><span class="sxs-lookup"><span data-stu-id="5a39a-130">A detailed example is included tooillustrate hello steps for creating and enabling a private web app extension.</span></span> <span data-ttu-id="5a39a-131">codice sorgente, ad esempio Gestione PHP hello che indicato di seguito può essere scaricati da Hello [https://github.com/projectkudu/PHPManager](https://github.com/projectkudu/PHPManager).</span><span class="sxs-lookup"><span data-stu-id="5a39a-131">hello source code for hello PHP Manager example that follows can be downloaded from [https://github.com/projectkudu/PHPManager](https://github.com/projectkudu/PHPManager).</span></span>

### <span data-ttu-id="5a39a-132"><a id="SiteSample"></a> Esempio di estensione app Web: PHP Manager</span><span class="sxs-lookup"><span data-stu-id="5a39a-132"><a id="SiteSample"></a> Web app extension example: PHP Manager</span></span>
<span data-ttu-id="5a39a-133">Gestione PHP è un'estensione di app web che consente agli amministratori di app web tooeasily visualizzazione e configura le impostazioni di PHP utilizzando un'interfaccia web anziché direttamente i file con estensione ini toomodify PHP.</span><span class="sxs-lookup"><span data-stu-id="5a39a-133">PHP Manager is a web app extension that allows web app administrators tooeasily view and configure their PHP settings using a web interface instead of having toomodify PHP .ini files directly.</span></span> <span data-ttu-id="5a39a-134">File di configurazione comuni per PHP includono file php.ini hello in file di programma e hello. user.ini file si trova nella cartella radice hello dell'app web.</span><span class="sxs-lookup"><span data-stu-id="5a39a-134">Common configuration files for PHP include hello php.ini file located under Program Files and hello .user.ini file located in hello root folder of your web app.</span></span> <span data-ttu-id="5a39a-135">Poiché il file php.ini hello non è direttamente modificabile hello piattaforma del servizio App, hello estensione PHP Manager utilizza hello. user.ini file tooapply modifiche alle impostazioni.</span><span class="sxs-lookup"><span data-stu-id="5a39a-135">Since hello php.ini file is not directly editable on hello App Service platform, hello PHP Manager extension uses hello .user.ini file tooapply setting changes.</span></span>

#### <span data-ttu-id="5a39a-136"><a id="PHPwebapp"></a>applicazione web gestione PHP Hello</span><span class="sxs-lookup"><span data-stu-id="5a39a-136"><a id="PHPwebapp"></a> hello PHP Manager web application</span></span>
<span data-ttu-id="5a39a-137">di seguito Hello è hello home page della distribuzione di gestione PHP hello:</span><span class="sxs-lookup"><span data-stu-id="5a39a-137">hello following is hello home page of hello PHP Manager deployment:</span></span>

![TransformSitePHPUI][TransformSitePHPUI]

<span data-ttu-id="5a39a-139">Come si può notare, un'estensione dell'app web è esattamente come un'applicazione web regolari, ma con un altro file ApplicationHost.xdt nella cartella radice hello di hello web app (ulteriori dettagli sul file ApplicationHost.xdt hello sono disponibili nella sezione di questo hello articolo).</span><span class="sxs-lookup"><span data-stu-id="5a39a-139">As you can see, a web app extension is just like a regular web application, but with an additional ApplicationHost.xdt file placed in hello root folder of hello web app (more details about hello ApplicationHost.xdt file are available in hello next section of this article).</span></span>

<span data-ttu-id="5a39a-140">estensione di PHP Manager Hello è stato creato utilizzando il modello di applicazione Web Visual Studio ASP.NET MVC 4 hello.</span><span class="sxs-lookup"><span data-stu-id="5a39a-140">hello PHP Manager extension was created using hello Visual Studio ASP.NET MVC 4 Web Application template.</span></span> <span data-ttu-id="5a39a-141">Hello visualizzazione seguente da Esplora soluzioni Mostra struttura hello di hello estensione Gestione PHP.</span><span class="sxs-lookup"><span data-stu-id="5a39a-141">hello following view from Solution Explorer shows hello structure of hello PHP Manager extension.</span></span>

![TransformSiteSolEx][TransformSiteSolEx]

<span data-ttu-id="5a39a-143">Hello solo una logica speciale del file i/o è tooindicate hello directory wwwroot dell'app web hello in cui si trova.</span><span class="sxs-lookup"><span data-stu-id="5a39a-143">hello only special logic needed for file I/O is tooindicate where hello wwwroot directory of hello web app is located.</span></span> <span data-ttu-id="5a39a-144">Come illustrato di esempio di codice seguente, hello hello variabile di ambiente "HOME" indica hello percorso radice dell'applicazione web e percorso wwwroot hello può essere costruita aggiungendo "site\wwwroot":</span><span class="sxs-lookup"><span data-stu-id="5a39a-144">As hello following code example shows, hello environment variable "HOME" indicates hello web app's root path, and hello wwwroot path can be constructed by appending "site\wwwroot":</span></span>

```csharp
/// <summary>
/// Gives hello location of hello .user.ini file, even if one doesn't exist yet
/// </summary>
private static string GetUserSettingsFilePath()
{
  var rootPath = Environment.GetEnvironmentVariable("HOME"); // For use on Azure Websites
  if (rootPath == null)
  {
    rootPath = System.IO.Path.GetTempPath(); // For testing purposes
  };
  var userSettingsFile = Path.Combine(rootPath, @"site\wwwroot\.user.ini");
  return userSettingsFile;
}
```


<span data-ttu-id="5a39a-145">Dopo aver creato il percorso di directory hello, è possibile utilizzare un file regolare tooread operazioni dei / o e scrivere toofiles.</span><span class="sxs-lookup"><span data-stu-id="5a39a-145">After you have hello directory path, you can use regular file I/O operations tooread and write toofiles.</span></span>

<span data-ttu-id="5a39a-146">Un punto di prestare attenzione con estensioni dell'app web per quanto riguarda la gestione di hello dei collegamenti interni.</span><span class="sxs-lookup"><span data-stu-id="5a39a-146">One point of caution with web app extensions regards hello handling of internal links.</span></span>  <span data-ttu-id="5a39a-147">Se si dispone di tutti i collegamenti nei file HTML che forniscono i percorsi assoluti toointernal collegamenti nell'app web, è necessario assicurarsi di che tali collegamenti vengono anteposti con il nome di estensione come la radice.</span><span class="sxs-lookup"><span data-stu-id="5a39a-147">If you have any links in your HTML files that give absolute paths toointernal links on your web app, you must ensure those links are prepended with your extension name as your root.</span></span> <span data-ttu-id="5a39a-148">Ciò è necessario perché hello cartella principale per l'estensione è "/`[your-extension-name]`/" anziché collegamenti semplicemente "/", pertanto qualsiasi interni devono essere aggiornati di conseguenza.</span><span class="sxs-lookup"><span data-stu-id="5a39a-148">This is needed because hello root for your extension is now "/`[your-extension-name]`/" rather than being just "/", so any internal links must be updated accordingly.</span></span> <span data-ttu-id="5a39a-149">Si supponga, ad esempio, che il codice include un esempio di toohello collegamento:</span><span class="sxs-lookup"><span data-stu-id="5a39a-149">For example, suppose your code includes a link toohello following:</span></span>

`"<a href="/Home/Settings">PHP Settings</a>"`

<span data-ttu-id="5a39a-150">Se il collegamento hello fa parte di un'estensione dell'app web, collegamento hello deve essere hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="5a39a-150">When hello link is part of a web app extension, hello link must be in hello following form:</span></span>

`"<a href="/[your-site-name]/Home/Settings">Settings</a>"`

<span data-ttu-id="5a39a-151">È possibile aggirare questo requisito, ovvero usando solo i percorsi relativi all'interno dell'applicazione web o in hello caso delle applicazioni ASP.NET, utilizzando hello `@Html.ActionLink` metodo che crea collegamenti appropriati hello automaticamente.</span><span class="sxs-lookup"><span data-stu-id="5a39a-151">You can work around this requirement by either using only relative paths within your web application, or in hello case of ASP.NET applications, by using hello `@Html.ActionLink` method which creates hello appropriate links for you.</span></span>

#### <span data-ttu-id="5a39a-152"><a id="XDT"></a>file applicationHost.xdt Hello</span><span class="sxs-lookup"><span data-stu-id="5a39a-152"><a id="XDT"></a> hello applicationHost.xdt file</span></span>
<span data-ttu-id="5a39a-153">codice di Hello per l'estensione app web viene inserito in %HOME%\SiteExtensions\[your-estensione-name].</span><span class="sxs-lookup"><span data-stu-id="5a39a-153">hello code for your web app extension goes under %HOME%\SiteExtensions\[your-extension-name].</span></span> <span data-ttu-id="5a39a-154">Verrà chiamato questa radice estensione hello.</span><span class="sxs-lookup"><span data-stu-id="5a39a-154">We'll call this hello extension root.</span></span>  

<span data-ttu-id="5a39a-155">tooregister dell'estensione dell'app web con file ApplicationHost. config hello, è necessario un file denominato ApplicationHost.xdt nella radice di estensione hello tooplace.</span><span class="sxs-lookup"><span data-stu-id="5a39a-155">tooregister your web app extension with hello applicationHost.config file, you need tooplace a file called ApplicationHost.xdt in hello extension root.</span></span> <span data-ttu-id="5a39a-156">il contenuto di Hello del file ApplicationHost.xdt hello deve essere come segue:</span><span class="sxs-lookup"><span data-stu-id="5a39a-156">hello content of hello ApplicationHost.xdt file should be as follows:</span></span>

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
  <system.applicationHost>
    <sites>
      <site name="%XDT_SCMSITENAME%" xdt:Locator="Match(name)">
        <!-- NOTE: Add your extension name in hello application paths below -->
        <application path="/[your-extension-name]" xdt:Locator="Match(path)" xdt:Transform="Remove" />
        <application path="/[your-extension-name]" applicationPool="%XDT_APPPOOLNAME%" xdt:Transform="Insert">
          <virtualDirectory path="/" physicalPath="%XDT_EXTENSIONPATH%" />
        </application>
      </site>
    </sites>
  </system.applicationHost>
</configuration>
```

<span data-ttu-id="5a39a-157">nome Hello che è selezionato come il nome di estensione deve essere hello stesso nome della cartella radice di estensione.</span><span class="sxs-lookup"><span data-stu-id="5a39a-157">hello name you select as your extension name should have hello same name as your extension root folder.</span></span>

<span data-ttu-id="5a39a-158">L'aggiunta di un nuovo toohello percorso applicazione hello effetto è `system.applicationHost` elenco dei siti nel sito di Gestione controllo servizi hello.</span><span class="sxs-lookup"><span data-stu-id="5a39a-158">This has hello effect of adding a new application path toohello `system.applicationHost` sites list under hello SCM site.</span></span> <span data-ttu-id="5a39a-159">sito di Gestione controllo servizi Hello è un punto finale di amministrazione del sito con le credenziali di accesso specifico.</span><span class="sxs-lookup"><span data-stu-id="5a39a-159">hello SCM site is a site administration end point with specific access credentials.</span></span> <span data-ttu-id="5a39a-160">Contiene l'URL di hello `https://[your-site-name].scm.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="5a39a-160">It has hello URL `https://[your-site-name].scm.azurewebsites.net`.</span></span>  

```xml
<system.applicationHost>
  ...       
  <sites>
    <site name="~1[your-website]" id="1716402716">
      <bindings>
        <binding protocol="http" bindingInformation="*:80: [your-website].scm.azurewebsites.net" />
        <binding protocol="https" bindingInformation="*:443: [your-website].scm.azurewebsites.net" />
      </bindings>
      <traceFailedRequestsLogging enabled="false" directory="C:\DWASFiles\Sites\[your-website]\VirtualDirectory0\LogFiles" />
      <detailedErrorLogging enabled="false" directory="C:\DWASFiles\Sites\[your-website]\VirtualDirectory0\LogFiles\DetailedErrors" />
      <logFile logSiteId="false" />
      <application path="/" applicationPool="[your-website]">
        <virtualDirectory path="/" physicalPath="D:\Program Files (x86)\SiteExtensions\Kudu\1.24.20926.5" />
      </application>
      <!-- Note hello custom changes that go here -->
      <application path="/[your-extension-name]" applicationPool="[your-website]">
        <virtualDirectory path="/" physicalPath="C:\DWASFiles\Sites\[your-website]\VirtualDirectory0\SiteExtensions\[your-extension-name]" />
      </application>
    </site>
  </sites>
  ... 
</system.applicationHost>
```

### <span data-ttu-id="5a39a-161"><a id="deploy"></a> Distribuzione dell'estensione di app Web</span><span class="sxs-lookup"><span data-stu-id="5a39a-161"><a id="deploy"></a> Web app extension deployment</span></span>
<span data-ttu-id="5a39a-162">tooinstall dell'estensione app web, è possibile utilizzare tutti i file hello del toohello di applicazione web FTP toocopy `\SiteExtensions\[your-extension-name]` cartella dell'app web hello in cui si desidera estensione hello tooinstall.</span><span class="sxs-lookup"><span data-stu-id="5a39a-162">tooinstall your web app extension, you can use FTP toocopy all hello files of your web application toohello `\SiteExtensions\[your-extension-name]` folder of hello web app on which you want tooinstall hello extension.</span></span>  <span data-ttu-id="5a39a-163">Impossibile verificare toocopy hello ApplicationHost.xdt toothis percorso del file anche.</span><span class="sxs-lookup"><span data-stu-id="5a39a-163">Be sure toocopy hello ApplicationHost.xdt file toothis location as well.</span></span> <span data-ttu-id="5a39a-164">Riavviare l'estensione di hello tooenable app web.</span><span class="sxs-lookup"><span data-stu-id="5a39a-164">Restart your web app tooenable hello extension.</span></span>

<span data-ttu-id="5a39a-165">Dovrebbe essere in grado di toosee l'estensione dell'app web a:</span><span class="sxs-lookup"><span data-stu-id="5a39a-165">You should be able toosee your web app extension at:</span></span>

`https://[your-site-name].scm.azurewebsites.net/[your-extension-name]`

<span data-ttu-id="5a39a-166">Si noti che hello che URL è simile a quello hello URL per l'app web, ad eccezione del fatto che usa il protocollo HTTPS e contiene ".scm".</span><span class="sxs-lookup"><span data-stu-id="5a39a-166">Note that hello URL looks just like hello URL for your web app, except that it uses HTTPS and contains ".scm".</span></span>

<span data-ttu-id="5a39a-167">È possibile toodisable tutti privati (non preinstallato) estensioni per l'app web durante lo sviluppo e indagini aggiungendo un oggetto impostazioni app con la chiave hello `WEBSITE_PRIVATE_EXTENSIONS` e il valore `0`.</span><span class="sxs-lookup"><span data-stu-id="5a39a-167">It is possible toodisable all private (not pre-installed) extensions for your web app during development and investigations by adding an app settings with hello key `WEBSITE_PRIVATE_EXTENSIONS` and a value of `0`.</span></span>

> [!NOTE]
> <span data-ttu-id="5a39a-168">Se si desidera tooget avviato con il servizio App di Azure prima di effettuare l'iscrizione per un account Azure, andare troppo[tenta di servizio App](https://azure.microsoft.com/try/app-service/), in cui è possibile creare subito un'app web di breve durata starter nel servizio App.</span><span class="sxs-lookup"><span data-stu-id="5a39a-168">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="5a39a-169">Non è necessario fornire una carta di credito né impegnarsi in alcun modo.</span><span class="sxs-lookup"><span data-stu-id="5a39a-169">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="5a39a-170">Modifiche apportate</span><span class="sxs-lookup"><span data-stu-id="5a39a-170">What's changed</span></span>
* <span data-ttu-id="5a39a-171">Per una Guida toohello modifica da siti Web tooApp servizio vedere: [relativo impatto sui servizi di Azure esistente e servizio App di Azure](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="5a39a-171">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!-- IMAGES -->
[TransformSitePHPUI]: ./media/web-sites-transform-extend/TransformSitePHPUI.png
[TransformSiteSolEx]: ./media/web-sites-transform-extend/TransformSiteSolEx.png

