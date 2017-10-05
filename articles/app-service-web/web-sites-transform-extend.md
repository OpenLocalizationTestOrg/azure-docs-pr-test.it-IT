---
title: Configurazione avanzata ed estensioni dell'app Web di Servizio app di Azure
description: Utilizzare le dichiarazioni XMDT (XML Document Transformation) per trasformare il file ApplicationHost.config nell'app Web di Servizio Web di Azure e per aggiungere estensioni provate per abilitare azioni di amministrazione personalizzate."
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
ms.openlocfilehash: 314d3a954e712b829e7cf5eb37b23b31670f976b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="azure-app-service-web-app-advanced-config-and-extensions"></a><span data-ttu-id="de4ce-103">Configurazione avanzata ed estensioni dell'app Web di Servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="de4ce-103">Azure App Service web app advanced config and extensions</span></span>
<span data-ttu-id="de4ce-104">Le dichiarazioni XDT [(XML Document Transformation)](http://msdn.microsoft.com/library/dd465326.aspx) consentono di trasformare il file [ApplicationHost.config](http://www.iis.net/learn/get-started/planning-your-iis-architecture/introduction-to-applicationhostconfig) in app Web in Servizio app di Azure.</span><span class="sxs-lookup"><span data-stu-id="de4ce-104">By using [XML Document Transformation](http://msdn.microsoft.com/library/dd465326.aspx) (XDT) declarations, you can transform the [ApplicationHost.config](http://www.iis.net/learn/get-started/planning-your-iis-architecture/introduction-to-applicationhostconfig) file in your web app in Azure App Service.</span></span> <span data-ttu-id="de4ce-105">È inoltre possibile usare le dichiarazioni XDT per aggiungere estensioni private in modo da consentire azioni di amministrazione personalizzate nell'app Web.</span><span class="sxs-lookup"><span data-stu-id="de4ce-105">You can also use XDT declarations to add private extensions to enable custom web app administration actions.</span></span> <span data-ttu-id="de4ce-106">In questo articolo è disponibile un'estensione dell'app PHP Manager di esempio, che consente la gestione di impostazioni PHP mediante un'interfaccia Web.</span><span class="sxs-lookup"><span data-stu-id="de4ce-106">This article includes a sample PHP Manager web app extension that enables management of PHP settings through a web interface.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <span data-ttu-id="de4ce-107"><a id="transform"></a>Configurazione avanzata tramite ApplicationHost.config</span><span class="sxs-lookup"><span data-stu-id="de4ce-107"><a id="transform"></a>Advanced configuration through ApplicationHost.config</span></span>
<span data-ttu-id="de4ce-108">La piattaforma Servizio app offre flessibilità e controllo per la configurazione dell'app Web.</span><span class="sxs-lookup"><span data-stu-id="de4ce-108">The App Service platform provides flexibility and control for web app configuration.</span></span> <span data-ttu-id="de4ce-109">Benché il file di configurazione standard ApplicationHost.config di IIS non sia disponibile per la modifica diretta in Servizio app, la piattaforma supporta un modello di trasformazione dichiarativo di ApplicationHost.config basato su dichiarazioni XDT (XML Document Transformation).</span><span class="sxs-lookup"><span data-stu-id="de4ce-109">Although the standard IIS ApplicationHost.config configuration file is not available for direct editing in App Service, the platform supports a declarative ApplicationHost.config transform model based on XML Document Transformation (XDT).</span></span>

<span data-ttu-id="de4ce-110">Per avvalersi di questa funzionalità per la trasformazione, è necessario creare un file ApplicationHost.xdt con contenuto XDT e posizionarlo sotto la radice del sito (d:\home\site) nella [Console Kudu](https://github.com/projectkudu/kudu/wiki/Kudu-console).</span><span class="sxs-lookup"><span data-stu-id="de4ce-110">To leverage this transform functionality, you create an ApplicationHost.xdt file with XDT content and place under the site root (d:\home\site) in the [Kudu Console](https://github.com/projectkudu/kudu/wiki/Kudu-console).</span></span> <span data-ttu-id="de4ce-111">Potrebbe essere necessario riacciare l'app Web per rendere effettive le modifiche.</span><span class="sxs-lookup"><span data-stu-id="de4ce-111">You may need to restart the Web App for changes to take effect.</span></span>

<span data-ttu-id="de4ce-112">Il seguente esempio di applicationHost.xdt mostra come aggiungere una nuova variabile di ambiente personalizzata a un'app Web che utilizza PHP 5.4.</span><span class="sxs-lookup"><span data-stu-id="de4ce-112">The following applicationHost.xdt sample shows how to add a new custom environment variable to a web app that uses PHP 5.4.</span></span>

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

<span data-ttu-id="de4ce-113">Un file di log che include lo stato e i dettagli relativi alla trasformazione è disponibile nella radice FTP in LogFiles\Transform.</span><span class="sxs-lookup"><span data-stu-id="de4ce-113">A log file with transform status and details is available from the FTP root under LogFiles\Transform.</span></span>

<span data-ttu-id="de4ce-114">Per esempi aggiuntivi, vedere [https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples](https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples).</span><span class="sxs-lookup"><span data-stu-id="de4ce-114">For additional samples, see [https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples](https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples).</span></span>

<span data-ttu-id="de4ce-115">**Nota**</span><span class="sxs-lookup"><span data-stu-id="de4ce-115">**Note**</span></span><br />
<span data-ttu-id="de4ce-116">Non è possibile rimuovere o riordinare gli elementi dell'elenco di moduli in `system.webServer`, ma è possibile aggiungere elementi all'elenco.</span><span class="sxs-lookup"><span data-stu-id="de4ce-116">Elements from the list of modules under `system.webServer` cannot be removed or reordered, but additions to the list are possible.</span></span>

## <span data-ttu-id="de4ce-117"><a id="extend"></a> Estendere l'app Web</span><span class="sxs-lookup"><span data-stu-id="de4ce-117"><a id="extend"></a> Extend your web app</span></span>
### <span data-ttu-id="de4ce-118"><a id="overview"></a> Panoramica delle estensioni di app Web private</span><span class="sxs-lookup"><span data-stu-id="de4ce-118"><a id="overview"></a> Overview of private web app extensions</span></span>
<span data-ttu-id="de4ce-119">Servizi app supporta le estensioni di app Web come punto di estensibilità per le azioni di amministrazione.</span><span class="sxs-lookup"><span data-stu-id="de4ce-119">App Service supports web app extensions as an extensibility point for administrative actions.</span></span> <span data-ttu-id="de4ce-120">Alcune funzionalità della piattaforma Servizio app sono in effetti implementate come estensioni preinstallate.</span><span class="sxs-lookup"><span data-stu-id="de4ce-120">In fact, some App Service platform features are implemented as pre-installed extensions.</span></span> <span data-ttu-id="de4ce-121">Benché non sia possibile modificare le estensioni preinstallate della piattaforma, è possibile creare e configurare estensioni private per le proprie app Web.</span><span class="sxs-lookup"><span data-stu-id="de4ce-121">While the pre-installed platform extensions cannot be modified, you can create and configure private extensions for your own web app.</span></span> <span data-ttu-id="de4ce-122">Questa funzionalità si basa anche sulle dichiarazioni XDT.</span><span class="sxs-lookup"><span data-stu-id="de4ce-122">This functionality also relies on XDT declarations.</span></span> <span data-ttu-id="de4ce-123">Di seguito sono riportati i passaggi chiave per la creazione di un'estensione privata di app Web:</span><span class="sxs-lookup"><span data-stu-id="de4ce-123">The key steps for creating a private web app extension are the following:</span></span>

1. <span data-ttu-id="de4ce-124">Estensione di app Web **content**: creare applicazioni Web supportate da Servizio app</span><span class="sxs-lookup"><span data-stu-id="de4ce-124">Web app extension **content**: create any web application supported by App Service</span></span>
2. <span data-ttu-id="de4ce-125">Estensione di app Web **declaration**: creare un file ApplicationHost.xdt</span><span class="sxs-lookup"><span data-stu-id="de4ce-125">Web app extension **declaration**: create an ApplicationHost.xdt file</span></span>
3. <span data-ttu-id="de4ce-126">**Distribuzione** dell'estensione dell'app Web: inserire il contenuto nella cartella SiteExtensions in `root`</span><span class="sxs-lookup"><span data-stu-id="de4ce-126">Web app extension **deployment**: place content in the SiteExtensions folder under `root`</span></span>

<span data-ttu-id="de4ce-127">È necessario che i collegamenti interni per l'app Web facciano riferimento a un percorso relativo al percorso applicazione specificato nel file ApplicationHost.xdt.</span><span class="sxs-lookup"><span data-stu-id="de4ce-127">Internal links for the web app should point to a path relative to the application path specified in the ApplicationHost.xdt file.</span></span> <span data-ttu-id="de4ce-128">Dopo ogni modifica al file ApplicationHost.xdt sarà necessario il riavvio dell'app Web.</span><span class="sxs-lookup"><span data-stu-id="de4ce-128">Any change to the ApplicationHost.xdt file requires a web app recycle.</span></span>

<span data-ttu-id="de4ce-129">**Nota**: informazioni aggiuntive relative a questi elementi chiave sono disponibili all'indirizzo [https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions](https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions).</span><span class="sxs-lookup"><span data-stu-id="de4ce-129">**Note**: Additional information for these key elements is available at [https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions](https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions).</span></span>

<span data-ttu-id="de4ce-130">L'esempio dettagliato incluso illustra la procedura per la creazione e l'abilitazione di un'estensione privata dell'app Web.</span><span class="sxs-lookup"><span data-stu-id="de4ce-130">A detailed example is included to illustrate the steps for creating and enabling a private web app extension.</span></span> <span data-ttu-id="de4ce-131">Il codice sorgente per l'esempio di PHP Manager seguente è disponibile per il download all'indirizzo [https://github.com/projectkudu/PHPManager](https://github.com/projectkudu/PHPManager).</span><span class="sxs-lookup"><span data-stu-id="de4ce-131">The source code for the PHP Manager example that follows can be downloaded from [https://github.com/projectkudu/PHPManager](https://github.com/projectkudu/PHPManager).</span></span>

### <span data-ttu-id="de4ce-132"><a id="SiteSample"></a> Esempio di estensione app Web: PHP Manager</span><span class="sxs-lookup"><span data-stu-id="de4ce-132"><a id="SiteSample"></a> Web app extension example: PHP Manager</span></span>
<span data-ttu-id="de4ce-133">PHP Manager è un'estensione di app Web che consente agli amministratori di app Web di visualizzare e configurare con facilità le impostazioni PHP mediante un'interfaccia Web, invece di dovere modificare direttamente i file INI di PHP.</span><span class="sxs-lookup"><span data-stu-id="de4ce-133">PHP Manager is a web app extension that allows web app administrators to easily view and configure their PHP settings using a web interface instead of having to modify PHP .ini files directly.</span></span> <span data-ttu-id="de4ce-134">I file di configurazione comuni per PHP includono il file php.ini, disponibile in Programmi, e il file .user.ini, disponibile nella cartella radice dell'app Web.</span><span class="sxs-lookup"><span data-stu-id="de4ce-134">Common configuration files for PHP include the php.ini file located under Program Files and the .user.ini file located in the root folder of your web app.</span></span> <span data-ttu-id="de4ce-135">Poiché non è possibile modificare il file php.ini direttamente nella piattaforma Servizio app, l'estensione PHP Manager usa il file .user.ini per applicare le modifiche relative alle impostazioni.</span><span class="sxs-lookup"><span data-stu-id="de4ce-135">Since the php.ini file is not directly editable on the App Service platform, the PHP Manager extension uses the .user.ini file to apply setting changes.</span></span>

#### <span data-ttu-id="de4ce-136"><a id="PHPwebapp"></a> Applicazione Web PHP Manager</span><span class="sxs-lookup"><span data-stu-id="de4ce-136"><a id="PHPwebapp"></a> The PHP Manager web application</span></span>
<span data-ttu-id="de4ce-137">Di seguito è riportata la home page della distribuzione di PHP Manager:</span><span class="sxs-lookup"><span data-stu-id="de4ce-137">The following is the home page of the PHP Manager deployment:</span></span>

![TransformSitePHPUI][TransformSitePHPUI]

<span data-ttu-id="de4ce-139">Come si può notare, un'estensione di app Web è analoga a una normale applicazione Web, ma include un file ApplicationHost.xdt nella cartella radice dell'app Web. Ulteriori dettagli sul file ApplicationHost.xdt sono disponibili nella sezione successiva di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="de4ce-139">As you can see, a web app extension is just like a regular web application, but with an additional ApplicationHost.xdt file placed in the root folder of the web app (more details about the ApplicationHost.xdt file are available in the next section of this article).</span></span>

<span data-ttu-id="de4ce-140">L'estensione PHP Manager è stata creata mediante il modello di applicazione Web MVC 4 ASP.NET di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="de4ce-140">The PHP Manager extension was created using the Visual Studio ASP.NET MVC 4 Web Application template.</span></span> <span data-ttu-id="de4ce-141">La visualizzazione seguente di Esplora soluzioni mostra la struttura dell'estensione di PHP Manager.</span><span class="sxs-lookup"><span data-stu-id="de4ce-141">The following view from Solution Explorer shows the structure of the PHP Manager extension.</span></span>

![TransformSiteSolEx][TransformSiteSolEx]

<span data-ttu-id="de4ce-143">L'unica logica speciale necessaria per l'I/O file consente di indicare la posizione della directory wwwroot dell'app Web.</span><span class="sxs-lookup"><span data-stu-id="de4ce-143">The only special logic needed for file I/O is to indicate where the wwwroot directory of the web app is located.</span></span> <span data-ttu-id="de4ce-144">Come illustrato nell'esempio seguente, la variabile di ambiente "HOME" indica il percorso della radice dell'app Web e il percorso wwwroot può essere creato mediante l'aggiunta di "site\wwwroot":</span><span class="sxs-lookup"><span data-stu-id="de4ce-144">As the following code example shows, the environment variable "HOME" indicates the web app's root path, and the wwwroot path can be constructed by appending "site\wwwroot":</span></span>

```csharp
/// <summary>
/// Gives the location of the .user.ini file, even if one doesn't exist yet
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


<span data-ttu-id="de4ce-145">Quando si dispone del percorso della directory, sarà possibile usare operazioni normali di I/O file per la lettura e la scrittura nei file.</span><span class="sxs-lookup"><span data-stu-id="de4ce-145">After you have the directory path, you can use regular file I/O operations to read and write to files.</span></span>

<span data-ttu-id="de4ce-146">È tuttavia necessario prestare attenzione alla gestione dei collegamenti interni nelle estensioni di app Web.</span><span class="sxs-lookup"><span data-stu-id="de4ce-146">One point of caution with web app extensions regards the handling of internal links.</span></span>  <span data-ttu-id="de4ce-147">Se sono presenti collegamenti nei file HTML che forniscono i percorsi assoluti per i collegamenti interni nell'app Web, sarà necessario assicurarsi che davanti a tali collegamenti sia aggiunto il nome dell'estensione come radice.</span><span class="sxs-lookup"><span data-stu-id="de4ce-147">If you have any links in your HTML files that give absolute paths to internal links on your web app, you must ensure those links are prepended with your extension name as your root.</span></span> <span data-ttu-id="de4ce-148">poiché la radice del sito per l'estensione è ora "/`[your-extension-name]`/" invece di essere solo "/". È pertanto necessario aggiornare di conseguenza qualsiasi collegamento interno.</span><span class="sxs-lookup"><span data-stu-id="de4ce-148">This is needed because the root for your extension is now "/`[your-extension-name]`/" rather than being just "/", so any internal links must be updated accordingly.</span></span> <span data-ttu-id="de4ce-149">Si supponga ad esempio che il codice includa un collegamento all'elemento seguente:</span><span class="sxs-lookup"><span data-stu-id="de4ce-149">For example, suppose your code includes a link to the following:</span></span>

`"<a href="/Home/Settings">PHP Settings</a>"`

<span data-ttu-id="de4ce-150">Quando il collegamento fa parte di un'estensione dell'app Web, è necessario che abbia il formato seguente:</span><span class="sxs-lookup"><span data-stu-id="de4ce-150">When the link is part of a web app extension, the link must be in the following form:</span></span>

`"<a href="/[your-site-name]/Home/Settings">Settings</a>"`

<span data-ttu-id="de4ce-151">In alternativa è possibile usare solo percorsi relativi nell'applicazione Web oppure, nel caso di applicazioni ASP.NET NET , utilizzando il metodo `@Html.ActionLink` che crea automaticamente i collegamenti appropriati.</span><span class="sxs-lookup"><span data-stu-id="de4ce-151">You can work around this requirement by either using only relative paths within your web application, or in the case of ASP.NET applications, by using the `@Html.ActionLink` method which creates the appropriate links for you.</span></span>

#### <span data-ttu-id="de4ce-152"><a id="XDT"></a> File applicationHost.xdt</span><span class="sxs-lookup"><span data-stu-id="de4ce-152"><a id="XDT"></a> The applicationHost.xdt file</span></span>
<span data-ttu-id="de4ce-153">Il codice per l'estensione dell'app Web deve essere presente sotto %HOME%\SiteExtensions\[your-extension-name].</span><span class="sxs-lookup"><span data-stu-id="de4ce-153">The code for your web app extension goes under %HOME%\SiteExtensions\[your-extension-name].</span></span> <span data-ttu-id="de4ce-154">Questa sarà la radice dell'estensione.</span><span class="sxs-lookup"><span data-stu-id="de4ce-154">We'll call this the extension root.</span></span>  

<span data-ttu-id="de4ce-155">Per registrare l'estensione dell'app Web con il file applicationHost.config, sarà necessario inserire un file denominato ApplicationHost.xdt nella radice dell'estensione.</span><span class="sxs-lookup"><span data-stu-id="de4ce-155">To register your web app extension with the applicationHost.config file, you need to place a file called ApplicationHost.xdt in the extension root.</span></span> <span data-ttu-id="de4ce-156">Il contenuto del file ApplicationHost.xdt deve essere analogo al seguente:</span><span class="sxs-lookup"><span data-stu-id="de4ce-156">The content of the ApplicationHost.xdt file should be as follows:</span></span>

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
  <system.applicationHost>
    <sites>
      <site name="%XDT_SCMSITENAME%" xdt:Locator="Match(name)">
        <!-- NOTE: Add your extension name in the application paths below -->
        <application path="/[your-extension-name]" xdt:Locator="Match(path)" xdt:Transform="Remove" />
        <application path="/[your-extension-name]" applicationPool="%XDT_APPPOOLNAME%" xdt:Transform="Insert">
          <virtualDirectory path="/" physicalPath="%XDT_EXTENSIONPATH%" />
        </application>
      </site>
    </sites>
  </system.applicationHost>
</configuration>
```

<span data-ttu-id="de4ce-157">Il nome selezionato come nome dell'estensione deve essere uguale al nome della cartella radice dell'estensione.</span><span class="sxs-lookup"><span data-stu-id="de4ce-157">The name you select as your extension name should have the same name as your extension root folder.</span></span>

<span data-ttu-id="de4ce-158">In tale modo, un nuovo percorso applicazione verrà aggiunto all'elenco di siti `system.applicationHost` nel sito SCM.</span><span class="sxs-lookup"><span data-stu-id="de4ce-158">This has the effect of adding a new application path to the `system.applicationHost` sites list under the SCM site.</span></span> <span data-ttu-id="de4ce-159">Il sito SCM è un endpoint di amministrazione di siti, con credenziali di accesso specifiche</span><span class="sxs-lookup"><span data-stu-id="de4ce-159">The SCM site is a site administration end point with specific access credentials.</span></span> <span data-ttu-id="de4ce-160">Ha l'URL `https://[your-site-name].scm.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="de4ce-160">It has the URL `https://[your-site-name].scm.azurewebsites.net`.</span></span>  

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
      <!-- Note the custom changes that go here -->
      <application path="/[your-extension-name]" applicationPool="[your-website]">
        <virtualDirectory path="/" physicalPath="C:\DWASFiles\Sites\[your-website]\VirtualDirectory0\SiteExtensions\[your-extension-name]" />
      </application>
    </site>
  </sites>
  ... 
</system.applicationHost>
```

### <span data-ttu-id="de4ce-161"><a id="deploy"></a> Distribuzione dell'estensione di app Web</span><span class="sxs-lookup"><span data-stu-id="de4ce-161"><a id="deploy"></a> Web app extension deployment</span></span>
<span data-ttu-id="de4ce-162">Per installare l'estensione dell'app Web, è possibile utilizzare FTP per copiare tutti i file dell'applicazione Web nella cartella `\SiteExtensions\[your-extension-name]` dell'app Web su cui si desidera installare l'estensione.</span><span class="sxs-lookup"><span data-stu-id="de4ce-162">To install your web app extension, you can use FTP to copy all the files of your web application to the `\SiteExtensions\[your-extension-name]` folder of the web app on which you want to install the extension.</span></span>  <span data-ttu-id="de4ce-163">Assicurarsi di copiare anche il file ApplicationHost.xdt nello stesso percorso.</span><span class="sxs-lookup"><span data-stu-id="de4ce-163">Be sure to copy the ApplicationHost.xdt file to this location as well.</span></span> <span data-ttu-id="de4ce-164">Riavviare l'app Web per abilitare l'estensione.</span><span class="sxs-lookup"><span data-stu-id="de4ce-164">Restart your web app to enable the extension.</span></span>

<span data-ttu-id="de4ce-165">L'estensione dell'app Web dovrebbe essere visibile all'indirizzo:</span><span class="sxs-lookup"><span data-stu-id="de4ce-165">You should be able to see your web app extension at:</span></span>

`https://[your-site-name].scm.azurewebsites.net/[your-extension-name]`

<span data-ttu-id="de4ce-166">Si noti che l'aspetto dell'URL è uguale a quello dell'URL dell'app Web, ad eccezione del fatto che utilizza HTTPS e include ".scm".</span><span class="sxs-lookup"><span data-stu-id="de4ce-166">Note that the URL looks just like the URL for your web app, except that it uses HTTPS and contains ".scm".</span></span>

<span data-ttu-id="de4ce-167">È possibile disabilitare tutte le estensionii provate (non preinstallate) per l'app Web durante sviluppo e analisi aggiungendo impostazioni di un'app con la chiave `WEBSITE_PRIVATE_EXTENSIONS` e il valore `0`.</span><span class="sxs-lookup"><span data-stu-id="de4ce-167">It is possible to disable all private (not pre-installed) extensions for your web app during development and investigations by adding an app settings with the key `WEBSITE_PRIVATE_EXTENSIONS` and a value of `0`.</span></span>

> [!NOTE]
> <span data-ttu-id="de4ce-168">Per iniziare a usare il servizio app di Azure prima di registrarsi per ottenere un account Azure, andare a [Prova il servizio app](https://azure.microsoft.com/try/app-service/), dove è possibile creare un'app Web iniziale temporanea nel servizio app.</span><span class="sxs-lookup"><span data-stu-id="de4ce-168">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="de4ce-169">Non è necessario fornire una carta di credito né impegnarsi in alcun modo.</span><span class="sxs-lookup"><span data-stu-id="de4ce-169">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="de4ce-170">Modifiche apportate</span><span class="sxs-lookup"><span data-stu-id="de4ce-170">What's changed</span></span>
* <span data-ttu-id="de4ce-171">Per una guida relativa al passaggio da Siti Web al servizio app, vedere [Servizio app di Azure e impatto sui servizi di Azure esistenti](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="de4ce-171">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!-- IMAGES -->
[TransformSitePHPUI]: ./media/web-sites-transform-extend/TransformSitePHPUI.png
[TransformSiteSolEx]: ./media/web-sites-transform-extend/TransformSiteSolEx.png

