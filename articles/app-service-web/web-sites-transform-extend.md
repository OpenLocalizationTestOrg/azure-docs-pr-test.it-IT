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
# <a name="azure-app-service-web-app-advanced-config-and-extensions"></a>Configurazione avanzata ed estensioni dell'app Web di Servizio app di Azure
Utilizzando [trasformazione di documenti XML](http://msdn.microsoft.com/library/dd465326.aspx) dichiarazioni (XDT), è possibile trasformare hello [applicationHost. config](http://www.iis.net/learn/get-started/planning-your-iis-architecture/introduction-to-applicationhostconfig) file nell'app web in Azure App Service. È possibile utilizzare anche XDT dichiarazioni tooadd le estensioni private tooenable web personalizzato app le azioni di amministrazione. In questo articolo è disponibile un'estensione dell'app PHP Manager di esempio, che consente la gestione di impostazioni PHP mediante un'interfaccia Web.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a id="transform"></a>Configurazione avanzata tramite ApplicationHost.config
piattaforma del servizio App Hello offre flessibilità e controllo per la configurazione di app web. Anche se i file di configurazione applicationHost. config IIS standard hello non è disponibile per la modifica diretta nel servizio App, piattaforma hello supporta un modello di trasformazione applicationHost. config dichiarativo basato su XML documento trasformazione (XDT).

tooleverage questa funzionalità di trasformazione, creare un file ApplicationHost.xdt con XDT contenuto e inserire nella radice del sito hello (d:\home\site) hello [Kudu Console](https://github.com/projectkudu/kudu/wiki/Kudu-console). Per effetto di tootake modifiche potrebbe essere necessario toorestart hello App Web.

Hello applicationHost.xdt esempio seguente viene illustrato come un nuovo tooa variabile di ambiente personalizzato tooadd web app che utilizza PHP 5.4.

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

È disponibile dalla radice FTP hello in LogFiles\Transform un file di log con lo stato di trasformazione e dettagli.

Per esempi aggiuntivi, vedere [https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples](https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples).

**Nota**<br />
Gli elementi dall'elenco di hello dei moduli in `system.webServer` non possono essere rimossi o riordinati, ma è possibile elenco toohello aggiunte.

## <a id="extend"></a> Estendere l'app Web
### <a id="overview"></a> Panoramica delle estensioni di app Web private
Servizi app supporta le estensioni di app Web come punto di estensibilità per le azioni di amministrazione. Alcune funzionalità della piattaforma Servizio app sono in effetti implementate come estensioni preinstallate. Mentre hello piattaforma pre-installate estensioni non possono essere modificate, è possibile creare e configurare le estensioni private per un'app web. Questa funzionalità si basa anche sulle dichiarazioni XDT. Hello chiave per la creazione di un'estensione dell'app web privata passaggi seguenti hello:

1. Estensione di app Web **content**: creare applicazioni Web supportate da Servizio app
2. Estensione di app Web **declaration**: creare un file ApplicationHost.xdt
3. Estensione app Web **distribuzione**: posizionare il contenuto nella cartella SiteExtensions hello in`root`

I collegamenti interni per l'app web hello devono puntare tooa toohello relativo applicazione percorso specificato nel file ApplicationHost.xdt hello. Qualsiasi file ApplicationHost.xdt toohello delle modifiche richiede un riciclo di app web.

**Nota**: informazioni aggiuntive relative a questi elementi chiave sono disponibili all'indirizzo [https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions](https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions).

Un esempio dettagliato è incluso tooillustrate hello passaggi per la creazione e l'abilitazione di un'estensione dell'app web privato. codice sorgente, ad esempio Gestione PHP hello che indicato di seguito può essere scaricati da Hello [https://github.com/projectkudu/PHPManager](https://github.com/projectkudu/PHPManager).

### <a id="SiteSample"></a> Esempio di estensione app Web: PHP Manager
Gestione PHP è un'estensione di app web che consente agli amministratori di app web tooeasily visualizzazione e configura le impostazioni di PHP utilizzando un'interfaccia web anziché direttamente i file con estensione ini toomodify PHP. File di configurazione comuni per PHP includono file php.ini hello in file di programma e hello. user.ini file si trova nella cartella radice hello dell'app web. Poiché il file php.ini hello non è direttamente modificabile hello piattaforma del servizio App, hello estensione PHP Manager utilizza hello. user.ini file tooapply modifiche alle impostazioni.

#### <a id="PHPwebapp"></a>applicazione web gestione PHP Hello
di seguito Hello è hello home page della distribuzione di gestione PHP hello:

![TransformSitePHPUI][TransformSitePHPUI]

Come si può notare, un'estensione dell'app web è esattamente come un'applicazione web regolari, ma con un altro file ApplicationHost.xdt nella cartella radice hello di hello web app (ulteriori dettagli sul file ApplicationHost.xdt hello sono disponibili nella sezione di questo hello articolo).

estensione di PHP Manager Hello è stato creato utilizzando il modello di applicazione Web Visual Studio ASP.NET MVC 4 hello. Hello visualizzazione seguente da Esplora soluzioni Mostra struttura hello di hello estensione Gestione PHP.

![TransformSiteSolEx][TransformSiteSolEx]

Hello solo una logica speciale del file i/o è tooindicate hello directory wwwroot dell'app web hello in cui si trova. Come illustrato di esempio di codice seguente, hello hello variabile di ambiente "HOME" indica hello percorso radice dell'applicazione web e percorso wwwroot hello può essere costruita aggiungendo "site\wwwroot":

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


Dopo aver creato il percorso di directory hello, è possibile utilizzare un file regolare tooread operazioni dei / o e scrivere toofiles.

Un punto di prestare attenzione con estensioni dell'app web per quanto riguarda la gestione di hello dei collegamenti interni.  Se si dispone di tutti i collegamenti nei file HTML che forniscono i percorsi assoluti toointernal collegamenti nell'app web, è necessario assicurarsi di che tali collegamenti vengono anteposti con il nome di estensione come la radice. Ciò è necessario perché hello cartella principale per l'estensione è "/`[your-extension-name]`/" anziché collegamenti semplicemente "/", pertanto qualsiasi interni devono essere aggiornati di conseguenza. Si supponga, ad esempio, che il codice include un esempio di toohello collegamento:

`"<a href="/Home/Settings">PHP Settings</a>"`

Se il collegamento hello fa parte di un'estensione dell'app web, collegamento hello deve essere hello seguente formato:

`"<a href="/[your-site-name]/Home/Settings">Settings</a>"`

È possibile aggirare questo requisito, ovvero usando solo i percorsi relativi all'interno dell'applicazione web o in hello caso delle applicazioni ASP.NET, utilizzando hello `@Html.ActionLink` metodo che crea collegamenti appropriati hello automaticamente.

#### <a id="XDT"></a>file applicationHost.xdt Hello
codice di Hello per l'estensione app web viene inserito in %HOME%\SiteExtensions\[your-estensione-name]. Verrà chiamato questa radice estensione hello.  

tooregister dell'estensione dell'app web con file ApplicationHost. config hello, è necessario un file denominato ApplicationHost.xdt nella radice di estensione hello tooplace. il contenuto di Hello del file ApplicationHost.xdt hello deve essere come segue:

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

nome Hello che è selezionato come il nome di estensione deve essere hello stesso nome della cartella radice di estensione.

L'aggiunta di un nuovo toohello percorso applicazione hello effetto è `system.applicationHost` elenco dei siti nel sito di Gestione controllo servizi hello. sito di Gestione controllo servizi Hello è un punto finale di amministrazione del sito con le credenziali di accesso specifico. Contiene l'URL di hello `https://[your-site-name].scm.azurewebsites.net`.  

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

### <a id="deploy"></a> Distribuzione dell'estensione di app Web
tooinstall dell'estensione app web, è possibile utilizzare tutti i file hello del toohello di applicazione web FTP toocopy `\SiteExtensions\[your-extension-name]` cartella dell'app web hello in cui si desidera estensione hello tooinstall.  Impossibile verificare toocopy hello ApplicationHost.xdt toothis percorso del file anche. Riavviare l'estensione di hello tooenable app web.

Dovrebbe essere in grado di toosee l'estensione dell'app web a:

`https://[your-site-name].scm.azurewebsites.net/[your-extension-name]`

Si noti che hello che URL è simile a quello hello URL per l'app web, ad eccezione del fatto che usa il protocollo HTTPS e contiene ".scm".

È possibile toodisable tutti privati (non preinstallato) estensioni per l'app web durante lo sviluppo e indagini aggiungendo un oggetto impostazioni app con la chiave hello `WEBSITE_PRIVATE_EXTENSIONS` e il valore `0`.

> [!NOTE]
> Se si desidera tooget avviato con il servizio App di Azure prima di effettuare l'iscrizione per un account Azure, andare troppo[tenta di servizio App](https://azure.microsoft.com/try/app-service/), in cui è possibile creare subito un'app web di breve durata starter nel servizio App. Non è necessario fornire una carta di credito né impegnarsi in alcun modo.
> 
> 

## <a name="whats-changed"></a>Modifiche apportate
* Per una Guida toohello modifica da siti Web tooApp servizio vedere: [relativo impatto sui servizi di Azure esistente e servizio App di Azure](http://go.microsoft.com/fwlink/?LinkId=529714)

<!-- IMAGES -->
[TransformSitePHPUI]: ./media/web-sites-transform-extend/TransformSitePHPUI.png
[TransformSiteSolEx]: ./media/web-sites-transform-extend/TransformSiteSolEx.png

