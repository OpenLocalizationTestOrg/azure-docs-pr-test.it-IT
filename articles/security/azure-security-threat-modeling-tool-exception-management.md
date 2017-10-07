---
title: Gestione - di modellazione strumento Microsoft Threat - Azure aaaException | Documenti Microsoft
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
ms.openlocfilehash: 247096c10deeca94ebb9b19df7ba60e442ca1e4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-exception-management--mitigations"></a>Infrastruttura di sicurezza: gestione delle eccezioni | soluzioni di prevenzione 
| Prodotto o servizio | Articolo |
| --------------- | ------- |
| **WCF** | <ul><li>[WCF - non includere il nodo serviceDebug nel file di configurazione](#servicedebug)</li><li>[WCF - non includere il nodo serviceMetadata nel file di configurazione](#servicemetadata)</li></ul> |
| **API Web** | <ul><li>[Assicurare una gestione appropriata delle eccezioni in API Web ASP.NET](#exception)</li></ul> |
| **Applicazione Web** | <ul><li>[Non esporre informazioni di sicurezza nei messaggi di errore](#messages)</li><li>[Implementare la pagina di gestione degli errori predefiniti ](#default)</li><li>[Impostare il metodo di distribuzione tooRetail in IIS](#deployment)</li><li>[Le eccezioni devono avere esito negativo in modo sicuro](#fail)</li></ul> |

## <a id="servicedebug"></a>WCF - non includere il nodo serviceDebug nel file di configurazione

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | WCF | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico, .NET Framework 3 |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Passaggi** | Servizi Windows Communication Framework (WCF) possono essere configurato tooexpose informazioni di debug. Le informazioni di debug non devono essere usate in ambienti di produzione. Hello `<serviceDebug>` tag definisce se è abilitata la funzionalità di informazioni di debug hello per un servizio WCF. Se hello includeExceptionDetailInFaults di attributo è impostato tootrue, verranno restituite informazioni di eccezione da un'applicazione hello tooclients. Gli utenti malintenzionati possono sfruttare ulteriori informazioni hello che acquisiscono dal debug output toomount attacchi nel framework di hello, database o altre risorse utilizzate da un'applicazione hello. |

### <a name="example"></a>Esempio
file di configurazione seguente Hello include hello `<serviceDebug>` tag: 
```
<configuration> 
<system.serviceModel> 
<behaviors> 
<serviceBehaviors> 
<behavior name=""MyServiceBehavior""> 
<serviceDebug includeExceptionDetailInFaults=""True"" httpHelpPageEnabled=""True""/> 
... 
```
Disabilitare le informazioni di debug nel servizio hello. Questo può essere ottenuto rimuovendo hello `<serviceDebug>` tag dal file di configurazione dell'applicazione. 

## <a id="servicemetadata"></a>WCF - non includere il nodo serviceMetadata nel file di configurazione

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | WCF | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | Generico, .NET Framework 3 |
| **Riferimenti**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Passaggi** | Esporre pubblicamente informazioni relative a un servizio può fornire importanti informazioni su come si può sfruttare servizio hello. Hello `<serviceMetadata>` tag consente di funzionalità di pubblicazione dei metadati di hello. I metadati del servizio potrebbero contenere informazioni riservate che non devono essere accessibili pubblicamente. Come minimo, consentire solo a utenti attendibili tooaccess hello metadati e assicurarsi che le informazioni non necessarie non sono esposta. Ancora meglio, completamente disabilitare hello possibilità toopublish metadati. Una configurazione di WCF provvisoria non conterrà hello `<serviceMetadata>` tag. |

## <a id="exception"></a>Assicurare una gestione appropriata delle eccezioni in API Web ASP.NET

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | API Web | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | MVC 5, MVC 6 |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [Gestione delle eccezioni in API Web ASP.NET](http://www.asp.net/web-api/overview/error-handling/exception-handling), [convalida del modello in API Web ASP.NET](http://www.asp.net/web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api) |
| **Passaggi** | Per impostazione predefinita, la maggior parte delle eccezioni non rilevate in API Web ASP.NET vengono convertite in una risposta HTTP con codice di stato `500, Internal Server Error`|

### <a name="example"></a>Esempio
codice di stato hello toocontrol restituito dall'API, hello `HttpResponseException` può essere utilizzato come illustrato di seguito: 
```C#
public Product GetProduct(int id)
{
    Product item = repository.Get(id);
    if (item == null)
    {
        throw new HttpResponseException(HttpStatusCode.NotFound);
    }
    return item;
}
```

### <a name="example"></a>Esempio
Per controllare ulteriormente sulla risposta eccezione hello, hello `HttpResponseMessage` classe può essere utilizzata come illustrato di seguito: 
```C#
public Product GetProduct(int id)
{
    Product item = repository.Get(id);
    if (item == null)
    {
        var resp = new HttpResponseMessage(HttpStatusCode.NotFound)
        {
            Content = new StringContent(string.Format("No product with ID = {0}", id)),
            ReasonPhrase = "Product ID Not Found"
        }
        throw new HttpResponseException(resp);
    }
    return item;
}
```
toocatch eccezioni non gestite che non sono di tipo hello `HttpResponseException`, è possibile utilizzare i filtri di eccezione. I filtri eccezioni implementano hello `System.Web.Http.Filters.IExceptionFilter` interfaccia. toowrite modo più semplice di Hello un filtro eccezioni è tooderive da hello `System.Web.Http.Filters.ExceptionFilterAttribute` classe ed eseguire l'override di metodo OnException hello. 

### <a name="example"></a>Esempio
Ecco un filtro che converte le eccezioni `NotImplementedException` nel codice di stato HTTP `501, Not Implemented`: 
```C#
namespace ProductStore.Filters
{
    using System;
    using System.Net;
    using System.Net.Http;
    using System.Web.Http.Filters;

    public class NotImplExceptionFilterAttribute : ExceptionFilterAttribute 
    {
        public override void OnException(HttpActionExecutedContext context)
        {
            if (context.Exception is NotImplementedException)
            {
                context.Response = new HttpResponseMessage(HttpStatusCode.NotImplemented);
            }
        }
    }
}
```

Esistono diversi modi tooregister un filtro eccezioni di API Web:
- Tramite un'azione
- Tramite un controller
- A livello globale

### <a name="example"></a>Esempio
hello tooapply filtro azione specifica tooa, aggiungere il filtro hello come azione toohello attributo: 
```C#
public class ProductsController : ApiController
{
    [NotImplExceptionFilter]
    public Contact GetContact(int id)
    {
        throw new NotImplementedException("This method is not implemented");
    }
}
```
### <a name="example"></a>Esempio
tooapply hello filtro tooall azioni hello un `controller`, aggiungere il filtro di hello come un attributo toohello `controller` classe: 

```C#
[NotImplExceptionFilter]
public class ProductsController : ApiController
{
    // ...
}
```

### <a name="example"></a>Esempio
hello tooapply filtro globale controller API Web tooall, aggiungere un'istanza di hello filtro toohello `GlobalConfiguration.Configuration.Filters` insieme. I filtri di eccezioni in questa raccolta si applicano tooany azione del controller API Web. 
```C#
GlobalConfiguration.Configuration.Filters.Add(
    new ProductStore.NotImplExceptionFilterAttribute());
```

### <a name="example"></a>Esempio
Per la convalida del modello, lo stato del modello di hello può essere passato tooCreateErrorResponse metodo come illustrato di seguito: 
```C#
public HttpResponseMessage PostProduct(Product item)
{
    if (!ModelState.IsValid)
    {
        return Request.CreateErrorResponse(HttpStatusCode.BadRequest, ModelState);
    }
    // Implementation not shown...
}
```

Controllo hello collegamenti nella sezione dei riferimenti hello per ulteriori informazioni sulla gestione delle eccezionale e la convalida del modello in ASP.Net Web API 

## <a id="messages"></a>Non esporre informazioni di sicurezza nei messaggi di errore

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Applicazione Web. | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | N/D  |
| **Passaggi** | <p>Messaggi di errore generici sono forniti direttamente toohello utente senza includere dati sensibili dell'applicazione. Esempi di dati sensibili:</p><ul><li>Nomi dei server</li><li>Stringhe di connessione</li><li>Nomi utente</li><li>Password</li><li>Procedure SQL</li><li>Dettagli di errori SQL dinamici</li><li>Analisi dello stack e righe di codice</li><li>Variabili archiviate in memoria</li><li>Percorsi di unità e cartelle</li><li>Punti di installazione dell'applicazione</li><li>Impostazioni di configurazione dell'host</li><li>Altri dettagli di un'applicazione interna</li></ul><p>Intercettando gli errori all'interno di un'applicazione e presentando messaggi di errore generici, nonché abilitando gli errori personalizzati all'interno di IIS, è possibile evitare la divulgazione di informazioni. Database di SQL Server e .NET gestione delle eccezioni, tra le altre architetture, di gestione degli errori sono particolarmente dettagliati ed estremamente utile tooa utente malintenzionato la profilatura dell'applicazione. Eseguire questa operazione non direttamente hello visualizzazione contenuto di una classe derivata dalla classe di eccezione .NET hello e assicurarsi di disporre di eccezioni appropriato in modo che non è un'eccezione imprevista inavvertitamente generato direttamente toohello utente.</p><ul><li>Fornire messaggi di errore generico direttamente utente toohello che astraggono stoccaggi dettagli specifici trovati direttamente nel messaggio di errore o eccezione di hello</li><li>Non visualizzato hello contenuto di un'eccezione .NET direttamente alla classe utente toohello</li><li>Intercettare tutti i messaggi di errore e se necessario informare l'utente di hello tramite l'applicazione client un errore generico messaggio inviato toohello</li><li>Non esporre il contenuto di hello della classe di eccezione hello direttamente toohello utente, in particolare hello restituito da `.ToString()`, o i valori delle proprietà di messaggio o StackTrace hello hello. In modo sicuro le informazioni di log e visualizzare più innocuo utente toohello messaggio</li></ul>|

## <a id="default"></a>Implementare la pagina di gestione degli errori predefiniti

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Applicazione Web. | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [Modificare la finestra di dialogo delle impostazioni pagine di errore ASP.NET](https://technet.microsoft.com/library/dd569096(WS.10).aspx) |
| **Passaggi** | <p>Quando un'applicazione ASP.NET ha esito negativo e causa un errore Server interno HTTP/1.x 500 o una configurazione di funzionalità (ad esempio, il filtro richieste) impedisce la visualizzazione di una pagina, verrà generato un messaggio di errore. Gli amministratori possono scegliere se visualizzare o meno un'applicazione hello deve un messaggio descrittivo toohello client, client toohello messaggio di errore dettagliato o toolocalhost messaggio di errore dettagliati solo. Hello <customErrors> tag nel file Web. config hello presenta tre modalità:</p><ul><li>**On:** specifica che gli errori personalizzati sono attivati. Se non viene specificato alcun attributo defaultRedirect, gli utenti visualizzato un errore generico. vengono visualizzati gli errori personalizzati Hello client remoti toohello e host locale toohello</li><li>**Off:** specifica che gli errori personalizzati sono disattivati. Hello errori ASP.NET dettagliati vengono visualizzati i client remoti toohello e host locale toohello</li><li>**RemoteOnly:** specifica che gli errori personalizzati vengono visualizzati solo i client remoti toohello e che gli errori ASP.NET vengono visualizzati l'host locale toohello. Questo è il valore di predefinito hello</li></ul><p>Aprire hello `web.config` file per sito/applicazione hello e verificare che il tag di hello è `<customErrors mode="RemoteOnly" />` o `<customErrors mode="On" />` definito.</p>|

## <a id="deployment"></a>Impostare il metodo di distribuzione tooRetail in IIS

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Applicazione Web. | 
| **Fase SDL**               | Distribuzione |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [Element distribuzione (schema impostazioni ASP.NET)](https://msdn.microsoft.com/library/ms228298(VS.80).aspx) |
| **Passaggi** | <p>Hello `<deployment retail>` switch deve essere utilizzato dal server IIS di produzione. Questo parametro viene utilizzato toohelp le applicazioni eseguite con prestazioni ottimali hello e informazioni di sicurezza minime perdite disabilitando hello output di traccia toogenerate possibilità dell'applicazione in una pagina, la disattivazione hello possibilità toodisplay dettagli errore gli utenti di messaggi tooend e hello Disabilitazione debug commutatore.</p><p>Spesso, gli switch e le opzioni che sono destinati agli sviluppatori, ad esempio traccia delle richieste no riuscite e debug, sono abilitati durante lo sviluppo attivo. È consigliabile che il metodo di distribuzione hello in qualsiasi server di produzione è possibile impostare tooretail. Aprire il file Machine. config hello e assicurarsi che `<deployment retail="true" />` tootrue. Connection resta impostato.</p>|

## <a id="fail"></a>Le eccezioni devono avere esito negativo in modo sicuro

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Applicazione Web. | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [Esito negativo in modo sicuro](https://www.owasp.org/index.php/Fail_securely) |
| **Passaggi** | L'applicazione deve avere esito negativo in modo sicuro. Per qualsiasi metodo che restituisce un valore booleano, in base al quale vengono prese determinate decisioni, è necessario creare con attenzione un blocco delle eccezioni. Esistono numerosi errori logici a causa di ampliamento di problemi di sicurezza toowhich in, quando il blocco di eccezioni hello viene scritto senza prestare particolare attenzione.|

### <a name="example"></a>Esempio
```C#
        public static bool ValidateDomain(string pathToValidate, Uri currentUrl)
        {
            try
            {
                if (!string.IsNullOrWhiteSpace(pathToValidate))
                {
                    var domain = RetrieveDomain(currentUrl);
                    var replyPath = new Uri(pathToValidate);
                    var replyDomain = RetrieveDomain(replyPath);

                    if (string.Compare(domain, replyDomain, StringComparison.OrdinalIgnoreCase) != 0)
                    {
                        //// Adding additional check tooenable CMS urls if they are not hosted on same domain.
                        if (!string.IsNullOrWhiteSpace(Utilities.CmsBase))
                        {
                            var cmsDomain = RetrieveDomain(new Uri(Utilities.Base.Trim()));
                            if (string.Compare(cmDomain, replyDomain, StringComparison.OrdinalIgnoreCase) != 0)
                            {
                                return false;
                            }
                            else
                            {
                                return true;
                            }
                        }

                        return false;
                    }
                }

                return true;
            }
            catch (UriFormatException ex)
            {
                LogHelper.LogException("Utilities:ValidateDomain", ex);
                return true;
            }
        }
```
Hello sopra metodo restituirà sempre True, in caso di alcune eccezioni. Se l'utente finale di hello fornisce un URL non valido, che hello browser equivalenti, ma hello `Uri()` non costruttore, verrà generata un'eccezione e vittima hello accederà toohello valido, ma non valido in URL. 
