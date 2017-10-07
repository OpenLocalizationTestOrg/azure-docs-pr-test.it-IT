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
# <a name="security-frame-exception-management--mitigations"></a><span data-ttu-id="5b079-103">Infrastruttura di sicurezza: gestione delle eccezioni | soluzioni di prevenzione</span><span class="sxs-lookup"><span data-stu-id="5b079-103">Security Frame: Exception Management | Mitigations</span></span> 
| <span data-ttu-id="5b079-104">Prodotto o servizio</span><span class="sxs-lookup"><span data-stu-id="5b079-104">Product/Service</span></span> | <span data-ttu-id="5b079-105">Articolo</span><span class="sxs-lookup"><span data-stu-id="5b079-105">Article</span></span> |
| --------------- | ------- |
| <span data-ttu-id="5b079-106">**WCF**</span><span class="sxs-lookup"><span data-stu-id="5b079-106">**WCF**</span></span> | <ul><li>[<span data-ttu-id="5b079-107">WCF - non includere il nodo serviceDebug nel file di configurazione</span><span class="sxs-lookup"><span data-stu-id="5b079-107">WCF- Do not include serviceDebug node in configuration file</span></span>](#servicedebug)</li><li>[<span data-ttu-id="5b079-108">WCF - non includere il nodo serviceMetadata nel file di configurazione</span><span class="sxs-lookup"><span data-stu-id="5b079-108">WCF- Do not include serviceMetadata node in configuration file</span></span>](#servicemetadata)</li></ul> |
| <span data-ttu-id="5b079-109">**API Web**</span><span class="sxs-lookup"><span data-stu-id="5b079-109">**Web API**</span></span> | <ul><li>[<span data-ttu-id="5b079-110">Assicurare una gestione appropriata delle eccezioni in API Web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="5b079-110">Ensure that proper exception handling is done in ASP.NET Web API </span></span>](#exception)</li></ul> |
| <span data-ttu-id="5b079-111">**Applicazione Web**</span><span class="sxs-lookup"><span data-stu-id="5b079-111">**Web Application**</span></span> | <ul><li>[<span data-ttu-id="5b079-112">Non esporre informazioni di sicurezza nei messaggi di errore</span><span class="sxs-lookup"><span data-stu-id="5b079-112">Do not expose security details in error messages </span></span>](#messages)</li><li>[<span data-ttu-id="5b079-113">Implementare la pagina di gestione degli errori predefiniti </span><span class="sxs-lookup"><span data-stu-id="5b079-113">Implement Default error handling page </span></span>](#default)</li><li>[<span data-ttu-id="5b079-114">Impostare il metodo di distribuzione tooRetail in IIS</span><span class="sxs-lookup"><span data-stu-id="5b079-114">Set Deployment Method tooRetail in IIS</span></span>](#deployment)</li><li>[<span data-ttu-id="5b079-115">Le eccezioni devono avere esito negativo in modo sicuro</span><span class="sxs-lookup"><span data-stu-id="5b079-115">Exceptions should fail safely</span></span>](#fail)</li></ul> |

## <span data-ttu-id="5b079-116"><a id="servicedebug"></a>WCF - non includere il nodo serviceDebug nel file di configurazione</span><span class="sxs-lookup"><span data-stu-id="5b079-116"><a id="servicedebug"></a>WCF- Do not include serviceDebug node in configuration file</span></span>

| <span data-ttu-id="5b079-117">Titolo</span><span class="sxs-lookup"><span data-stu-id="5b079-117">Title</span></span>                   | <span data-ttu-id="5b079-118">Dettagli</span><span class="sxs-lookup"><span data-stu-id="5b079-118">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="5b079-119">**Componente**</span><span class="sxs-lookup"><span data-stu-id="5b079-119">**Component**</span></span>               | <span data-ttu-id="5b079-120">WCF</span><span class="sxs-lookup"><span data-stu-id="5b079-120">WCF</span></span> | 
| <span data-ttu-id="5b079-121">**Fase SDL**</span><span class="sxs-lookup"><span data-stu-id="5b079-121">**SDL Phase**</span></span>               | <span data-ttu-id="5b079-122">Compilare</span><span class="sxs-lookup"><span data-stu-id="5b079-122">Build</span></span> |  
| <span data-ttu-id="5b079-123">**Tecnologie applicabili**</span><span class="sxs-lookup"><span data-stu-id="5b079-123">**Applicable Technologies**</span></span> | <span data-ttu-id="5b079-124">Generico, .NET Framework 3</span><span class="sxs-lookup"><span data-stu-id="5b079-124">Generic, NET Framework 3</span></span> |
| <span data-ttu-id="5b079-125">**Attributes (Attributi) (Attributi)**</span><span class="sxs-lookup"><span data-stu-id="5b079-125">**Attributes**</span></span>              | <span data-ttu-id="5b079-126">N/D</span><span class="sxs-lookup"><span data-stu-id="5b079-126">N/A</span></span>  |
| <span data-ttu-id="5b079-127">**Riferimenti**</span><span class="sxs-lookup"><span data-stu-id="5b079-127">**References**</span></span>              | <span data-ttu-id="5b079-128">[MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html)</span><span class="sxs-lookup"><span data-stu-id="5b079-128">[MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html)</span></span> |
| <span data-ttu-id="5b079-129">**Passaggi**</span><span class="sxs-lookup"><span data-stu-id="5b079-129">**Steps**</span></span> | <span data-ttu-id="5b079-130">Servizi Windows Communication Framework (WCF) possono essere configurato tooexpose informazioni di debug.</span><span class="sxs-lookup"><span data-stu-id="5b079-130">Windows Communication Framework (WCF) services can be configured tooexpose debugging information.</span></span> <span data-ttu-id="5b079-131">Le informazioni di debug non devono essere usate in ambienti di produzione.</span><span class="sxs-lookup"><span data-stu-id="5b079-131">Debug information should not be used in production environments.</span></span> <span data-ttu-id="5b079-132">Hello `<serviceDebug>` tag definisce se è abilitata la funzionalità di informazioni di debug hello per un servizio WCF.</span><span class="sxs-lookup"><span data-stu-id="5b079-132">hello `<serviceDebug>` tag defines whether hello debug information feature is enabled for a WCF service.</span></span> <span data-ttu-id="5b079-133">Se hello includeExceptionDetailInFaults di attributo è impostato tootrue, verranno restituite informazioni di eccezione da un'applicazione hello tooclients.</span><span class="sxs-lookup"><span data-stu-id="5b079-133">If hello attribute includeExceptionDetailInFaults is set tootrue, exception information from hello application will be returned tooclients.</span></span> <span data-ttu-id="5b079-134">Gli utenti malintenzionati possono sfruttare ulteriori informazioni hello che acquisiscono dal debug output toomount attacchi nel framework di hello, database o altre risorse utilizzate da un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="5b079-134">Attackers can leverage hello additional information they gain from debugging output toomount attacks targeted on hello framework, database, or other resources used by hello application.</span></span> |

### <a name="example"></a><span data-ttu-id="5b079-135">Esempio</span><span class="sxs-lookup"><span data-stu-id="5b079-135">Example</span></span>
<span data-ttu-id="5b079-136">file di configurazione seguente Hello include hello `<serviceDebug>` tag:</span><span class="sxs-lookup"><span data-stu-id="5b079-136">hello following configuration file includes hello `<serviceDebug>` tag:</span></span> 
```
<configuration> 
<system.serviceModel> 
<behaviors> 
<serviceBehaviors> 
<behavior name=""MyServiceBehavior""> 
<serviceDebug includeExceptionDetailInFaults=""True"" httpHelpPageEnabled=""True""/> 
... 
```
<span data-ttu-id="5b079-137">Disabilitare le informazioni di debug nel servizio hello.</span><span class="sxs-lookup"><span data-stu-id="5b079-137">Disable debugging information in hello service.</span></span> <span data-ttu-id="5b079-138">Questo può essere ottenuto rimuovendo hello `<serviceDebug>` tag dal file di configurazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="5b079-138">This can be accomplished by removing hello `<serviceDebug>` tag from your application's configuration file.</span></span> 

## <span data-ttu-id="5b079-139"><a id="servicemetadata"></a>WCF - non includere il nodo serviceMetadata nel file di configurazione</span><span class="sxs-lookup"><span data-stu-id="5b079-139"><a id="servicemetadata"></a>WCF- Do not include serviceMetadata node in configuration file</span></span>

| <span data-ttu-id="5b079-140">Titolo</span><span class="sxs-lookup"><span data-stu-id="5b079-140">Title</span></span>                   | <span data-ttu-id="5b079-141">Dettagli</span><span class="sxs-lookup"><span data-stu-id="5b079-141">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="5b079-142">**Componente**</span><span class="sxs-lookup"><span data-stu-id="5b079-142">**Component**</span></span>               | <span data-ttu-id="5b079-143">WCF</span><span class="sxs-lookup"><span data-stu-id="5b079-143">WCF</span></span> | 
| <span data-ttu-id="5b079-144">**Fase SDL**</span><span class="sxs-lookup"><span data-stu-id="5b079-144">**SDL Phase**</span></span>               | <span data-ttu-id="5b079-145">Compilare</span><span class="sxs-lookup"><span data-stu-id="5b079-145">Build</span></span> |  
| <span data-ttu-id="5b079-146">**Tecnologie applicabili**</span><span class="sxs-lookup"><span data-stu-id="5b079-146">**Applicable Technologies**</span></span> | <span data-ttu-id="5b079-147">Generico</span><span class="sxs-lookup"><span data-stu-id="5b079-147">Generic</span></span> |
| <span data-ttu-id="5b079-148">**Attributes (Attributi) (Attributi)**</span><span class="sxs-lookup"><span data-stu-id="5b079-148">**Attributes**</span></span>              | <span data-ttu-id="5b079-149">Generico, .NET Framework 3</span><span class="sxs-lookup"><span data-stu-id="5b079-149">Generic, NET Framework 3</span></span> |
| <span data-ttu-id="5b079-150">**Riferimenti**</span><span class="sxs-lookup"><span data-stu-id="5b079-150">**References**</span></span>              | <span data-ttu-id="5b079-151">[MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html)</span><span class="sxs-lookup"><span data-stu-id="5b079-151">[MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html)</span></span> |
| <span data-ttu-id="5b079-152">**Passaggi**</span><span class="sxs-lookup"><span data-stu-id="5b079-152">**Steps**</span></span> | <span data-ttu-id="5b079-153">Esporre pubblicamente informazioni relative a un servizio può fornire importanti informazioni su come si può sfruttare servizio hello.</span><span class="sxs-lookup"><span data-stu-id="5b079-153">Publicly exposing information about a service can provide attackers with valuable insight into how they might exploit hello service.</span></span> <span data-ttu-id="5b079-154">Hello `<serviceMetadata>` tag consente di funzionalità di pubblicazione dei metadati di hello.</span><span class="sxs-lookup"><span data-stu-id="5b079-154">hello `<serviceMetadata>` tag enables hello metadata publishing feature.</span></span> <span data-ttu-id="5b079-155">I metadati del servizio potrebbero contenere informazioni riservate che non devono essere accessibili pubblicamente.</span><span class="sxs-lookup"><span data-stu-id="5b079-155">Service metadata could contain sensitive information that should not be publicly accessible.</span></span> <span data-ttu-id="5b079-156">Come minimo, consentire solo a utenti attendibili tooaccess hello metadati e assicurarsi che le informazioni non necessarie non sono esposta.</span><span class="sxs-lookup"><span data-stu-id="5b079-156">At a minimum, only allow trusted users tooaccess hello metadata and ensure that unnecessary information is not exposed.</span></span> <span data-ttu-id="5b079-157">Ancora meglio, completamente disabilitare hello possibilità toopublish metadati.</span><span class="sxs-lookup"><span data-stu-id="5b079-157">Better yet, entirely disable hello ability toopublish metadata.</span></span> <span data-ttu-id="5b079-158">Una configurazione di WCF provvisoria non conterrà hello `<serviceMetadata>` tag.</span><span class="sxs-lookup"><span data-stu-id="5b079-158">A safe WCF configuration will not contain hello `<serviceMetadata>` tag.</span></span> |

## <span data-ttu-id="5b079-159"><a id="exception"></a>Assicurare una gestione appropriata delle eccezioni in API Web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="5b079-159"><a id="exception"></a>Ensure that proper exception handling is done in ASP.NET Web API</span></span>

| <span data-ttu-id="5b079-160">Titolo</span><span class="sxs-lookup"><span data-stu-id="5b079-160">Title</span></span>                   | <span data-ttu-id="5b079-161">Dettagli</span><span class="sxs-lookup"><span data-stu-id="5b079-161">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="5b079-162">**Componente**</span><span class="sxs-lookup"><span data-stu-id="5b079-162">**Component**</span></span>               | <span data-ttu-id="5b079-163">API Web</span><span class="sxs-lookup"><span data-stu-id="5b079-163">Web API</span></span> | 
| <span data-ttu-id="5b079-164">**Fase SDL**</span><span class="sxs-lookup"><span data-stu-id="5b079-164">**SDL Phase**</span></span>               | <span data-ttu-id="5b079-165">Compilare</span><span class="sxs-lookup"><span data-stu-id="5b079-165">Build</span></span> |  
| <span data-ttu-id="5b079-166">**Tecnologie applicabili**</span><span class="sxs-lookup"><span data-stu-id="5b079-166">**Applicable Technologies**</span></span> | <span data-ttu-id="5b079-167">MVC 5, MVC 6</span><span class="sxs-lookup"><span data-stu-id="5b079-167">MVC 5, MVC 6</span></span> |
| <span data-ttu-id="5b079-168">**Attributes (Attributi) (Attributi)**</span><span class="sxs-lookup"><span data-stu-id="5b079-168">**Attributes**</span></span>              | <span data-ttu-id="5b079-169">N/D</span><span class="sxs-lookup"><span data-stu-id="5b079-169">N/A</span></span>  |
| <span data-ttu-id="5b079-170">**Riferimenti**</span><span class="sxs-lookup"><span data-stu-id="5b079-170">**References**</span></span>              | <span data-ttu-id="5b079-171">[Gestione delle eccezioni in API Web ASP.NET](http://www.asp.net/web-api/overview/error-handling/exception-handling), [convalida del modello in API Web ASP.NET](http://www.asp.net/web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api)</span><span class="sxs-lookup"><span data-stu-id="5b079-171">[Exception Handling in ASP.NET Web API](http://www.asp.net/web-api/overview/error-handling/exception-handling), [Model Validation in ASP.NET Web API](http://www.asp.net/web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api)</span></span> |
| <span data-ttu-id="5b079-172">**Passaggi**</span><span class="sxs-lookup"><span data-stu-id="5b079-172">**Steps**</span></span> | <span data-ttu-id="5b079-173">Per impostazione predefinita, la maggior parte delle eccezioni non rilevate in API Web ASP.NET vengono convertite in una risposta HTTP con codice di stato `500, Internal Server Error`</span><span class="sxs-lookup"><span data-stu-id="5b079-173">By default, most uncaught exceptions in ASP.NET Web API are translated into an HTTP response with status code `500, Internal Server Error`</span></span>|

### <a name="example"></a><span data-ttu-id="5b079-174">Esempio</span><span class="sxs-lookup"><span data-stu-id="5b079-174">Example</span></span>
<span data-ttu-id="5b079-175">codice di stato hello toocontrol restituito dall'API, hello `HttpResponseException` può essere utilizzato come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="5b079-175">toocontrol hello status code returned by hello API, `HttpResponseException` can be used as shown below:</span></span> 
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

### <a name="example"></a><span data-ttu-id="5b079-176">Esempio</span><span class="sxs-lookup"><span data-stu-id="5b079-176">Example</span></span>
<span data-ttu-id="5b079-177">Per controllare ulteriormente sulla risposta eccezione hello, hello `HttpResponseMessage` classe può essere utilizzata come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="5b079-177">For further control on hello exception response, hello `HttpResponseMessage` class can be used as shown below:</span></span> 
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
<span data-ttu-id="5b079-178">toocatch eccezioni non gestite che non sono di tipo hello `HttpResponseException`, è possibile utilizzare i filtri di eccezione.</span><span class="sxs-lookup"><span data-stu-id="5b079-178">toocatch unhandled exceptions that are not of hello type `HttpResponseException`, Exception Filters can be used.</span></span> <span data-ttu-id="5b079-179">I filtri eccezioni implementano hello `System.Web.Http.Filters.IExceptionFilter` interfaccia.</span><span class="sxs-lookup"><span data-stu-id="5b079-179">Exception filters implement hello `System.Web.Http.Filters.IExceptionFilter` interface.</span></span> <span data-ttu-id="5b079-180">toowrite modo più semplice di Hello un filtro eccezioni è tooderive da hello `System.Web.Http.Filters.ExceptionFilterAttribute` classe ed eseguire l'override di metodo OnException hello.</span><span class="sxs-lookup"><span data-stu-id="5b079-180">hello simplest way toowrite an exception filter is tooderive from hello `System.Web.Http.Filters.ExceptionFilterAttribute` class and override hello OnException method.</span></span> 

### <a name="example"></a><span data-ttu-id="5b079-181">Esempio</span><span class="sxs-lookup"><span data-stu-id="5b079-181">Example</span></span>
<span data-ttu-id="5b079-182">Ecco un filtro che converte le eccezioni `NotImplementedException` nel codice di stato HTTP `501, Not Implemented`:</span><span class="sxs-lookup"><span data-stu-id="5b079-182">Here is a filter that converts `NotImplementedException` exceptions into HTTP status code `501, Not Implemented`:</span></span> 
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

<span data-ttu-id="5b079-183">Esistono diversi modi tooregister un filtro eccezioni di API Web:</span><span class="sxs-lookup"><span data-stu-id="5b079-183">There are several ways tooregister a Web API exception filter:</span></span>
- <span data-ttu-id="5b079-184">Tramite un'azione</span><span class="sxs-lookup"><span data-stu-id="5b079-184">By action</span></span>
- <span data-ttu-id="5b079-185">Tramite un controller</span><span class="sxs-lookup"><span data-stu-id="5b079-185">By controller</span></span>
- <span data-ttu-id="5b079-186">A livello globale</span><span class="sxs-lookup"><span data-stu-id="5b079-186">Globally</span></span>

### <a name="example"></a><span data-ttu-id="5b079-187">Esempio</span><span class="sxs-lookup"><span data-stu-id="5b079-187">Example</span></span>
<span data-ttu-id="5b079-188">hello tooapply filtro azione specifica tooa, aggiungere il filtro hello come azione toohello attributo:</span><span class="sxs-lookup"><span data-stu-id="5b079-188">tooapply hello filter tooa specific action, add hello filter as an attribute toohello action:</span></span> 
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
### <a name="example"></a><span data-ttu-id="5b079-189">Esempio</span><span class="sxs-lookup"><span data-stu-id="5b079-189">Example</span></span>
<span data-ttu-id="5b079-190">tooapply hello filtro tooall azioni hello un `controller`, aggiungere il filtro di hello come un attributo toohello `controller` classe:</span><span class="sxs-lookup"><span data-stu-id="5b079-190">tooapply hello filter tooall of hello actions on a `controller`, add hello filter as an attribute toohello `controller` class:</span></span> 

```C#
[NotImplExceptionFilter]
public class ProductsController : ApiController
{
    // ...
}
```

### <a name="example"></a><span data-ttu-id="5b079-191">Esempio</span><span class="sxs-lookup"><span data-stu-id="5b079-191">Example</span></span>
<span data-ttu-id="5b079-192">hello tooapply filtro globale controller API Web tooall, aggiungere un'istanza di hello filtro toohello `GlobalConfiguration.Configuration.Filters` insieme.</span><span class="sxs-lookup"><span data-stu-id="5b079-192">tooapply hello filter globally tooall Web API controllers, add an instance of hello filter toohello `GlobalConfiguration.Configuration.Filters` collection.</span></span> <span data-ttu-id="5b079-193">I filtri di eccezioni in questa raccolta si applicano tooany azione del controller API Web.</span><span class="sxs-lookup"><span data-stu-id="5b079-193">Exception filters in this collection apply tooany Web API controller action.</span></span> 
```C#
GlobalConfiguration.Configuration.Filters.Add(
    new ProductStore.NotImplExceptionFilterAttribute());
```

### <a name="example"></a><span data-ttu-id="5b079-194">Esempio</span><span class="sxs-lookup"><span data-stu-id="5b079-194">Example</span></span>
<span data-ttu-id="5b079-195">Per la convalida del modello, lo stato del modello di hello può essere passato tooCreateErrorResponse metodo come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="5b079-195">For model validation, hello model state can be passed tooCreateErrorResponse method as shown below:</span></span> 
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

<span data-ttu-id="5b079-196">Controllo hello collegamenti nella sezione dei riferimenti hello per ulteriori informazioni sulla gestione delle eccezionale e la convalida del modello in ASP.Net Web API</span><span class="sxs-lookup"><span data-stu-id="5b079-196">Check hello links in hello references section for additional details about exceptional handling and model validation in ASP.Net Web API</span></span> 

## <span data-ttu-id="5b079-197"><a id="messages"></a>Non esporre informazioni di sicurezza nei messaggi di errore</span><span class="sxs-lookup"><span data-stu-id="5b079-197"><a id="messages"></a>Do not expose security details in error messages</span></span>

| <span data-ttu-id="5b079-198">Titolo</span><span class="sxs-lookup"><span data-stu-id="5b079-198">Title</span></span>                   | <span data-ttu-id="5b079-199">Dettagli</span><span class="sxs-lookup"><span data-stu-id="5b079-199">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="5b079-200">**Componente**</span><span class="sxs-lookup"><span data-stu-id="5b079-200">**Component**</span></span>               | <span data-ttu-id="5b079-201">Applicazione Web.</span><span class="sxs-lookup"><span data-stu-id="5b079-201">Web Application</span></span> | 
| <span data-ttu-id="5b079-202">**Fase SDL**</span><span class="sxs-lookup"><span data-stu-id="5b079-202">**SDL Phase**</span></span>               | <span data-ttu-id="5b079-203">Compilare</span><span class="sxs-lookup"><span data-stu-id="5b079-203">Build</span></span> |  
| <span data-ttu-id="5b079-204">**Tecnologie applicabili**</span><span class="sxs-lookup"><span data-stu-id="5b079-204">**Applicable Technologies**</span></span> | <span data-ttu-id="5b079-205">Generico</span><span class="sxs-lookup"><span data-stu-id="5b079-205">Generic</span></span> |
| <span data-ttu-id="5b079-206">**Attributes (Attributi) (Attributi)**</span><span class="sxs-lookup"><span data-stu-id="5b079-206">**Attributes**</span></span>              | <span data-ttu-id="5b079-207">N/D</span><span class="sxs-lookup"><span data-stu-id="5b079-207">N/A</span></span>  |
| <span data-ttu-id="5b079-208">**Riferimenti**</span><span class="sxs-lookup"><span data-stu-id="5b079-208">**References**</span></span>              | <span data-ttu-id="5b079-209">N/D</span><span class="sxs-lookup"><span data-stu-id="5b079-209">N/A</span></span>  |
| <span data-ttu-id="5b079-210">**Passaggi**</span><span class="sxs-lookup"><span data-stu-id="5b079-210">**Steps**</span></span> | <p><span data-ttu-id="5b079-211">Messaggi di errore generici sono forniti direttamente toohello utente senza includere dati sensibili dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="5b079-211">Generic error messages are provided directly toohello user without including sensitive application data.</span></span> <span data-ttu-id="5b079-212">Esempi di dati sensibili:</span><span class="sxs-lookup"><span data-stu-id="5b079-212">Examples of sensitive data include:</span></span></p><ul><li><span data-ttu-id="5b079-213">Nomi dei server</span><span class="sxs-lookup"><span data-stu-id="5b079-213">Server names</span></span></li><li><span data-ttu-id="5b079-214">Stringhe di connessione</span><span class="sxs-lookup"><span data-stu-id="5b079-214">Connection strings</span></span></li><li><span data-ttu-id="5b079-215">Nomi utente</span><span class="sxs-lookup"><span data-stu-id="5b079-215">Usernames</span></span></li><li><span data-ttu-id="5b079-216">Password</span><span class="sxs-lookup"><span data-stu-id="5b079-216">Passwords</span></span></li><li><span data-ttu-id="5b079-217">Procedure SQL</span><span class="sxs-lookup"><span data-stu-id="5b079-217">SQL procedures</span></span></li><li><span data-ttu-id="5b079-218">Dettagli di errori SQL dinamici</span><span class="sxs-lookup"><span data-stu-id="5b079-218">Details of dynamic SQL failures</span></span></li><li><span data-ttu-id="5b079-219">Analisi dello stack e righe di codice</span><span class="sxs-lookup"><span data-stu-id="5b079-219">Stack trace and lines of code</span></span></li><li><span data-ttu-id="5b079-220">Variabili archiviate in memoria</span><span class="sxs-lookup"><span data-stu-id="5b079-220">Variables stored in memory</span></span></li><li><span data-ttu-id="5b079-221">Percorsi di unità e cartelle</span><span class="sxs-lookup"><span data-stu-id="5b079-221">Drive and folder locations</span></span></li><li><span data-ttu-id="5b079-222">Punti di installazione dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="5b079-222">Application install points</span></span></li><li><span data-ttu-id="5b079-223">Impostazioni di configurazione dell'host</span><span class="sxs-lookup"><span data-stu-id="5b079-223">Host configuration settings</span></span></li><li><span data-ttu-id="5b079-224">Altri dettagli di un'applicazione interna</span><span class="sxs-lookup"><span data-stu-id="5b079-224">Other internal application details</span></span></li></ul><p><span data-ttu-id="5b079-225">Intercettando gli errori all'interno di un'applicazione e presentando messaggi di errore generici, nonché abilitando gli errori personalizzati all'interno di IIS, è possibile evitare la divulgazione di informazioni.</span><span class="sxs-lookup"><span data-stu-id="5b079-225">Trapping all errors within an application and providing generic error messages, as well as enabling custom errors within IIS will help prevent information disclosure.</span></span> <span data-ttu-id="5b079-226">Database di SQL Server e .NET gestione delle eccezioni, tra le altre architetture, di gestione degli errori sono particolarmente dettagliati ed estremamente utile tooa utente malintenzionato la profilatura dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="5b079-226">SQL Server database and .NET Exception handling, among other error handling architectures, are especially verbose and extremely useful tooa malicious user profiling your application.</span></span> <span data-ttu-id="5b079-227">Eseguire questa operazione non direttamente hello visualizzazione contenuto di una classe derivata dalla classe di eccezione .NET hello e assicurarsi di disporre di eccezioni appropriato in modo che non è un'eccezione imprevista inavvertitamente generato direttamente toohello utente.</span><span class="sxs-lookup"><span data-stu-id="5b079-227">Do not directly display hello contents of a class derived from hello .NET Exception class, and ensure that you have proper exception handling so that an unexpected exception isn't inadvertently raised directly toohello user.</span></span></p><ul><li><span data-ttu-id="5b079-228">Fornire messaggi di errore generico direttamente utente toohello che astraggono stoccaggi dettagli specifici trovati direttamente nel messaggio di errore o eccezione di hello</span><span class="sxs-lookup"><span data-stu-id="5b079-228">Provide generic error messages directly toohello user that abstract away specific details found directly in hello exception/error message</span></span></li><li><span data-ttu-id="5b079-229">Non visualizzato hello contenuto di un'eccezione .NET direttamente alla classe utente toohello</span><span class="sxs-lookup"><span data-stu-id="5b079-229">Do not display hello contents of a .NET exception class directly toohello user</span></span></li><li><span data-ttu-id="5b079-230">Intercettare tutti i messaggi di errore e se necessario informare l'utente di hello tramite l'applicazione client un errore generico messaggio inviato toohello</span><span class="sxs-lookup"><span data-stu-id="5b079-230">Trap all error messages and if appropriate inform hello user via a generic error message sent toohello application client</span></span></li><li><span data-ttu-id="5b079-231">Non esporre il contenuto di hello della classe di eccezione hello direttamente toohello utente, in particolare hello restituito da `.ToString()`, o i valori delle proprietà di messaggio o StackTrace hello hello.</span><span class="sxs-lookup"><span data-stu-id="5b079-231">Do not expose hello contents of hello Exception class directly toohello user, especially hello return value from `.ToString()`, or hello values of hello Message or StackTrace properties.</span></span> <span data-ttu-id="5b079-232">In modo sicuro le informazioni di log e visualizzare più innocuo utente toohello messaggio</span><span class="sxs-lookup"><span data-stu-id="5b079-232">Securely log this information and display a more innocuous message toohello user</span></span></li></ul>|

## <span data-ttu-id="5b079-233"><a id="default"></a>Implementare la pagina di gestione degli errori predefiniti</span><span class="sxs-lookup"><span data-stu-id="5b079-233"><a id="default"></a>Implement Default error handling page</span></span>

| <span data-ttu-id="5b079-234">Titolo</span><span class="sxs-lookup"><span data-stu-id="5b079-234">Title</span></span>                   | <span data-ttu-id="5b079-235">Dettagli</span><span class="sxs-lookup"><span data-stu-id="5b079-235">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="5b079-236">**Componente**</span><span class="sxs-lookup"><span data-stu-id="5b079-236">**Component**</span></span>               | <span data-ttu-id="5b079-237">Applicazione Web.</span><span class="sxs-lookup"><span data-stu-id="5b079-237">Web Application</span></span> | 
| <span data-ttu-id="5b079-238">**Fase SDL**</span><span class="sxs-lookup"><span data-stu-id="5b079-238">**SDL Phase**</span></span>               | <span data-ttu-id="5b079-239">Compilare</span><span class="sxs-lookup"><span data-stu-id="5b079-239">Build</span></span> |  
| <span data-ttu-id="5b079-240">**Tecnologie applicabili**</span><span class="sxs-lookup"><span data-stu-id="5b079-240">**Applicable Technologies**</span></span> | <span data-ttu-id="5b079-241">Generico</span><span class="sxs-lookup"><span data-stu-id="5b079-241">Generic</span></span> |
| <span data-ttu-id="5b079-242">**Attributes (Attributi) (Attributi)**</span><span class="sxs-lookup"><span data-stu-id="5b079-242">**Attributes**</span></span>              | <span data-ttu-id="5b079-243">N/D</span><span class="sxs-lookup"><span data-stu-id="5b079-243">N/A</span></span>  |
| <span data-ttu-id="5b079-244">**Riferimenti**</span><span class="sxs-lookup"><span data-stu-id="5b079-244">**References**</span></span>              | <span data-ttu-id="5b079-245">[Modificare la finestra di dialogo delle impostazioni pagine di errore ASP.NET](https://technet.microsoft.com/library/dd569096(WS.10).aspx)</span><span class="sxs-lookup"><span data-stu-id="5b079-245">[Edit ASP.NET Error Pages Settings Dialog Box](https://technet.microsoft.com/library/dd569096(WS.10).aspx)</span></span> |
| <span data-ttu-id="5b079-246">**Passaggi**</span><span class="sxs-lookup"><span data-stu-id="5b079-246">**Steps**</span></span> | <p><span data-ttu-id="5b079-247">Quando un'applicazione ASP.NET ha esito negativo e causa un errore Server interno HTTP/1.x 500 o una configurazione di funzionalità (ad esempio, il filtro richieste) impedisce la visualizzazione di una pagina, verrà generato un messaggio di errore.</span><span class="sxs-lookup"><span data-stu-id="5b079-247">When an ASP.NET application fails and causes an HTTP/1.x 500 Internal Server Error, or a feature configuration (such as Request Filtering) prevents a page from being displayed, an error message will be generated.</span></span> <span data-ttu-id="5b079-248">Gli amministratori possono scegliere se visualizzare o meno un'applicazione hello deve un messaggio descrittivo toohello client, client toohello messaggio di errore dettagliato o toolocalhost messaggio di errore dettagliati solo.</span><span class="sxs-lookup"><span data-stu-id="5b079-248">Administrators can choose whether or not hello application should display a friendly message toohello client, detailed error message toohello client, or detailed error message toolocalhost only.</span></span> <span data-ttu-id="5b079-249">Hello <customErrors> tag nel file Web. config hello presenta tre modalità:</span><span class="sxs-lookup"><span data-stu-id="5b079-249">hello <customErrors> tag in hello web.config has three modes:</span></span></p><ul><li><span data-ttu-id="5b079-250">**On:** specifica che gli errori personalizzati sono attivati.</span><span class="sxs-lookup"><span data-stu-id="5b079-250">**On:** Specifies that custom errors are enabled.</span></span> <span data-ttu-id="5b079-251">Se non viene specificato alcun attributo defaultRedirect, gli utenti visualizzato un errore generico.</span><span class="sxs-lookup"><span data-stu-id="5b079-251">If no defaultRedirect attribute is specified, users see a generic error.</span></span> <span data-ttu-id="5b079-252">vengono visualizzati gli errori personalizzati Hello client remoti toohello e host locale toohello</span><span class="sxs-lookup"><span data-stu-id="5b079-252">hello custom errors are shown toohello remote clients and toohello local host</span></span></li><li><span data-ttu-id="5b079-253">**Off:** specifica che gli errori personalizzati sono disattivati.</span><span class="sxs-lookup"><span data-stu-id="5b079-253">**Off:** Specifies that custom errors are disabled.</span></span> <span data-ttu-id="5b079-254">Hello errori ASP.NET dettagliati vengono visualizzati i client remoti toohello e host locale toohello</span><span class="sxs-lookup"><span data-stu-id="5b079-254">hello detailed ASP.NET errors are shown toohello remote clients and toohello local host</span></span></li><li><span data-ttu-id="5b079-255">**RemoteOnly:** specifica che gli errori personalizzati vengono visualizzati solo i client remoti toohello e che gli errori ASP.NET vengono visualizzati l'host locale toohello.</span><span class="sxs-lookup"><span data-stu-id="5b079-255">**RemoteOnly:** Specifies that custom errors are shown only toohello remote clients, and that ASP.NET errors are shown toohello local host.</span></span> <span data-ttu-id="5b079-256">Questo è il valore di predefinito hello</span><span class="sxs-lookup"><span data-stu-id="5b079-256">This is hello default value</span></span></li></ul><p><span data-ttu-id="5b079-257">Aprire hello `web.config` file per sito/applicazione hello e verificare che il tag di hello è `<customErrors mode="RemoteOnly" />` o `<customErrors mode="On" />` definito.</span><span class="sxs-lookup"><span data-stu-id="5b079-257">Open hello `web.config` file for hello application/site and ensure that hello tag has either `<customErrors mode="RemoteOnly" />` or `<customErrors mode="On" />` defined.</span></span></p>|

## <span data-ttu-id="5b079-258"><a id="deployment"></a>Impostare il metodo di distribuzione tooRetail in IIS</span><span class="sxs-lookup"><span data-stu-id="5b079-258"><a id="deployment"></a>Set Deployment Method tooRetail in IIS</span></span>

| <span data-ttu-id="5b079-259">Titolo</span><span class="sxs-lookup"><span data-stu-id="5b079-259">Title</span></span>                   | <span data-ttu-id="5b079-260">Dettagli</span><span class="sxs-lookup"><span data-stu-id="5b079-260">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="5b079-261">**Componente**</span><span class="sxs-lookup"><span data-stu-id="5b079-261">**Component**</span></span>               | <span data-ttu-id="5b079-262">Applicazione Web.</span><span class="sxs-lookup"><span data-stu-id="5b079-262">Web Application</span></span> | 
| <span data-ttu-id="5b079-263">**Fase SDL**</span><span class="sxs-lookup"><span data-stu-id="5b079-263">**SDL Phase**</span></span>               | <span data-ttu-id="5b079-264">Distribuzione</span><span class="sxs-lookup"><span data-stu-id="5b079-264">Deployment</span></span> |  
| <span data-ttu-id="5b079-265">**Tecnologie applicabili**</span><span class="sxs-lookup"><span data-stu-id="5b079-265">**Applicable Technologies**</span></span> | <span data-ttu-id="5b079-266">Generico</span><span class="sxs-lookup"><span data-stu-id="5b079-266">Generic</span></span> |
| <span data-ttu-id="5b079-267">**Attributes (Attributi) (Attributi)**</span><span class="sxs-lookup"><span data-stu-id="5b079-267">**Attributes**</span></span>              | <span data-ttu-id="5b079-268">N/D</span><span class="sxs-lookup"><span data-stu-id="5b079-268">N/A</span></span>  |
| <span data-ttu-id="5b079-269">**Riferimenti**</span><span class="sxs-lookup"><span data-stu-id="5b079-269">**References**</span></span>              | <span data-ttu-id="5b079-270">[Element distribuzione (schema impostazioni ASP.NET)](https://msdn.microsoft.com/library/ms228298(VS.80).aspx)</span><span class="sxs-lookup"><span data-stu-id="5b079-270">[deployment Element (ASP.NET Settings Schema)](https://msdn.microsoft.com/library/ms228298(VS.80).aspx)</span></span> |
| <span data-ttu-id="5b079-271">**Passaggi**</span><span class="sxs-lookup"><span data-stu-id="5b079-271">**Steps**</span></span> | <p><span data-ttu-id="5b079-272">Hello `<deployment retail>` switch deve essere utilizzato dal server IIS di produzione.</span><span class="sxs-lookup"><span data-stu-id="5b079-272">hello `<deployment retail>` switch is intended for use by production IIS servers.</span></span> <span data-ttu-id="5b079-273">Questo parametro viene utilizzato toohelp le applicazioni eseguite con prestazioni ottimali hello e informazioni di sicurezza minime perdite disabilitando hello output di traccia toogenerate possibilità dell'applicazione in una pagina, la disattivazione hello possibilità toodisplay dettagli errore gli utenti di messaggi tooend e hello Disabilitazione debug commutatore.</span><span class="sxs-lookup"><span data-stu-id="5b079-273">This switch is used toohelp applications run with hello best possible performance and least possible security information leakages by disabling hello application's ability toogenerate trace output on a page, disabling hello ability toodisplay detailed error messages tooend users, and disabling hello debug switch.</span></span></p><p><span data-ttu-id="5b079-274">Spesso, gli switch e le opzioni che sono destinati agli sviluppatori, ad esempio traccia delle richieste no riuscite e debug, sono abilitati durante lo sviluppo attivo.</span><span class="sxs-lookup"><span data-stu-id="5b079-274">Often times, switches and options that are developer-focused, such as failed request tracing and debugging, are enabled during active development.</span></span> <span data-ttu-id="5b079-275">È consigliabile che il metodo di distribuzione hello in qualsiasi server di produzione è possibile impostare tooretail.</span><span class="sxs-lookup"><span data-stu-id="5b079-275">It is recommended that hello deployment method on any production server be set tooretail.</span></span> <span data-ttu-id="5b079-276">Aprire il file Machine. config hello e assicurarsi che `<deployment retail="true" />` tootrue. Connection resta impostato.</span><span class="sxs-lookup"><span data-stu-id="5b079-276">open hello machine.config file and ensure that `<deployment retail="true" />` remains set tootrue.</span></span></p>|

## <span data-ttu-id="5b079-277"><a id="fail"></a>Le eccezioni devono avere esito negativo in modo sicuro</span><span class="sxs-lookup"><span data-stu-id="5b079-277"><a id="fail"></a>Exceptions should fail safely</span></span>

| <span data-ttu-id="5b079-278">Titolo</span><span class="sxs-lookup"><span data-stu-id="5b079-278">Title</span></span>                   | <span data-ttu-id="5b079-279">Dettagli</span><span class="sxs-lookup"><span data-stu-id="5b079-279">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="5b079-280">**Componente**</span><span class="sxs-lookup"><span data-stu-id="5b079-280">**Component**</span></span>               | <span data-ttu-id="5b079-281">Applicazione Web.</span><span class="sxs-lookup"><span data-stu-id="5b079-281">Web Application</span></span> | 
| <span data-ttu-id="5b079-282">**Fase SDL**</span><span class="sxs-lookup"><span data-stu-id="5b079-282">**SDL Phase**</span></span>               | <span data-ttu-id="5b079-283">Compilare</span><span class="sxs-lookup"><span data-stu-id="5b079-283">Build</span></span> |  
| <span data-ttu-id="5b079-284">**Tecnologie applicabili**</span><span class="sxs-lookup"><span data-stu-id="5b079-284">**Applicable Technologies**</span></span> | <span data-ttu-id="5b079-285">Generico</span><span class="sxs-lookup"><span data-stu-id="5b079-285">Generic</span></span> |
| <span data-ttu-id="5b079-286">**Attributes (Attributi) (Attributi)**</span><span class="sxs-lookup"><span data-stu-id="5b079-286">**Attributes**</span></span>              | <span data-ttu-id="5b079-287">N/D</span><span class="sxs-lookup"><span data-stu-id="5b079-287">N/A</span></span>  |
| <span data-ttu-id="5b079-288">**Riferimenti**</span><span class="sxs-lookup"><span data-stu-id="5b079-288">**References**</span></span>              | [<span data-ttu-id="5b079-289">Esito negativo in modo sicuro</span><span class="sxs-lookup"><span data-stu-id="5b079-289">Fail securely</span></span>](https://www.owasp.org/index.php/Fail_securely) |
| <span data-ttu-id="5b079-290">**Passaggi**</span><span class="sxs-lookup"><span data-stu-id="5b079-290">**Steps**</span></span> | <span data-ttu-id="5b079-291">L'applicazione deve avere esito negativo in modo sicuro.</span><span class="sxs-lookup"><span data-stu-id="5b079-291">Application should fail safely.</span></span> <span data-ttu-id="5b079-292">Per qualsiasi metodo che restituisce un valore booleano, in base al quale vengono prese determinate decisioni, è necessario creare con attenzione un blocco delle eccezioni.</span><span class="sxs-lookup"><span data-stu-id="5b079-292">Any method that returns a Boolean value, based on which certain decision is made, should have exception block carefully created.</span></span> <span data-ttu-id="5b079-293">Esistono numerosi errori logici a causa di ampliamento di problemi di sicurezza toowhich in, quando il blocco di eccezioni hello viene scritto senza prestare particolare attenzione.</span><span class="sxs-lookup"><span data-stu-id="5b079-293">There are lot of logical errors due toowhich security issues creep in, when hello exception block is written carelessly.</span></span>|

### <a name="example"></a><span data-ttu-id="5b079-294">Esempio</span><span class="sxs-lookup"><span data-stu-id="5b079-294">Example</span></span>
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
<span data-ttu-id="5b079-295">Hello sopra metodo restituirà sempre True, in caso di alcune eccezioni.</span><span class="sxs-lookup"><span data-stu-id="5b079-295">hello above method will always return True, if some exception happens.</span></span> <span data-ttu-id="5b079-296">Se l'utente finale di hello fornisce un URL non valido, che hello browser equivalenti, ma hello `Uri()` non costruttore, verrà generata un'eccezione e vittima hello accederà toohello valido, ma non valido in URL.</span><span class="sxs-lookup"><span data-stu-id="5b079-296">If hello end user provides a malformed URL, that hello browser respects, but hello `Uri()` constructor doesn't, this will throw an exception, and hello victim will be taken toohello valid but malformed URL.</span></span> 
