---
title: 'Gestione delle eccezioni: Microsoft Threat Modeling Tool - Azure | Microsoft Docs'
description: soluzioni di prevenzione per le minacce esposte in Threat Modeling Tool
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
ms.openlocfilehash: bbf357b902474a1812eb7a5a2c914d0c8b91934b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="security-frame-exception-management--mitigations"></a><span data-ttu-id="e636c-103">Infrastruttura di sicurezza: gestione delle eccezioni | soluzioni di prevenzione</span><span class="sxs-lookup"><span data-stu-id="e636c-103">Security Frame: Exception Management | Mitigations</span></span> 
| <span data-ttu-id="e636c-104">Prodotto o servizio</span><span class="sxs-lookup"><span data-stu-id="e636c-104">Product/Service</span></span> | <span data-ttu-id="e636c-105">Articolo</span><span class="sxs-lookup"><span data-stu-id="e636c-105">Article</span></span> |
| --------------- | ------- |
| <span data-ttu-id="e636c-106">**WCF**</span><span class="sxs-lookup"><span data-stu-id="e636c-106">**WCF**</span></span> | <ul><li>[<span data-ttu-id="e636c-107">WCF - non includere il nodo serviceDebug nel file di configurazione</span><span class="sxs-lookup"><span data-stu-id="e636c-107">WCF- Do not include serviceDebug node in configuration file</span></span>](#servicedebug)</li><li>[<span data-ttu-id="e636c-108">WCF - non includere il nodo serviceMetadata nel file di configurazione</span><span class="sxs-lookup"><span data-stu-id="e636c-108">WCF- Do not include serviceMetadata node in configuration file</span></span>](#servicemetadata)</li></ul> |
| <span data-ttu-id="e636c-109">**API Web**</span><span class="sxs-lookup"><span data-stu-id="e636c-109">**Web API**</span></span> | <ul><li>[<span data-ttu-id="e636c-110">Assicurare una gestione appropriata delle eccezioni in API Web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="e636c-110">Ensure that proper exception handling is done in ASP.NET Web API </span></span>](#exception)</li></ul> |
| <span data-ttu-id="e636c-111">**Applicazione Web**</span><span class="sxs-lookup"><span data-stu-id="e636c-111">**Web Application**</span></span> | <ul><li>[<span data-ttu-id="e636c-112">Non esporre informazioni di sicurezza nei messaggi di errore</span><span class="sxs-lookup"><span data-stu-id="e636c-112">Do not expose security details in error messages </span></span>](#messages)</li><li>[<span data-ttu-id="e636c-113">Implementare la pagina di gestione degli errori predefiniti </span><span class="sxs-lookup"><span data-stu-id="e636c-113">Implement Default error handling page </span></span>](#default)</li><li>[<span data-ttu-id="e636c-114">Impostare il metodo di distribuzione al dettaglio in IIS</span><span class="sxs-lookup"><span data-stu-id="e636c-114">Set Deployment Method to Retail in IIS</span></span>](#deployment)</li><li>[<span data-ttu-id="e636c-115">Le eccezioni devono avere esito negativo in modo sicuro</span><span class="sxs-lookup"><span data-stu-id="e636c-115">Exceptions should fail safely</span></span>](#fail)</li></ul> |

## <span data-ttu-id="e636c-116"><a id="servicedebug"></a>WCF - non includere il nodo serviceDebug nel file di configurazione</span><span class="sxs-lookup"><span data-stu-id="e636c-116"><a id="servicedebug"></a>WCF- Do not include serviceDebug node in configuration file</span></span>

| <span data-ttu-id="e636c-117">Titolo</span><span class="sxs-lookup"><span data-stu-id="e636c-117">Title</span></span>                   | <span data-ttu-id="e636c-118">Dettagli</span><span class="sxs-lookup"><span data-stu-id="e636c-118">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="e636c-119">**Componente**</span><span class="sxs-lookup"><span data-stu-id="e636c-119">**Component**</span></span>               | <span data-ttu-id="e636c-120">WCF</span><span class="sxs-lookup"><span data-stu-id="e636c-120">WCF</span></span> | 
| <span data-ttu-id="e636c-121">**Fase SDL**</span><span class="sxs-lookup"><span data-stu-id="e636c-121">**SDL Phase**</span></span>               | <span data-ttu-id="e636c-122">Compilare</span><span class="sxs-lookup"><span data-stu-id="e636c-122">Build</span></span> |  
| <span data-ttu-id="e636c-123">**Tecnologie applicabili**</span><span class="sxs-lookup"><span data-stu-id="e636c-123">**Applicable Technologies**</span></span> | <span data-ttu-id="e636c-124">Generico, .NET Framework 3</span><span class="sxs-lookup"><span data-stu-id="e636c-124">Generic, NET Framework 3</span></span> |
| <span data-ttu-id="e636c-125">**Attributes (Attributi) (Attributi)**</span><span class="sxs-lookup"><span data-stu-id="e636c-125">**Attributes**</span></span>              | <span data-ttu-id="e636c-126">N/D</span><span class="sxs-lookup"><span data-stu-id="e636c-126">N/A</span></span>  |
| <span data-ttu-id="e636c-127">**Riferimenti**</span><span class="sxs-lookup"><span data-stu-id="e636c-127">**References**</span></span>              | <span data-ttu-id="e636c-128">[MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html)</span><span class="sxs-lookup"><span data-stu-id="e636c-128">[MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html)</span></span> |
| <span data-ttu-id="e636c-129">**Passaggi**</span><span class="sxs-lookup"><span data-stu-id="e636c-129">**Steps**</span></span> | <span data-ttu-id="e636c-130">I servizi Windows Communication Framework (WCF) possono essere configurati per esporre le informazioni di debug.</span><span class="sxs-lookup"><span data-stu-id="e636c-130">Windows Communication Framework (WCF) services can be configured to expose debugging information.</span></span> <span data-ttu-id="e636c-131">Le informazioni di debug non devono essere usate in ambienti di produzione.</span><span class="sxs-lookup"><span data-stu-id="e636c-131">Debug information should not be used in production environments.</span></span> <span data-ttu-id="e636c-132">Il tag `<serviceDebug>` definisce se è abilitata la funzionalità di informazioni di debug per un servizio WCF.</span><span class="sxs-lookup"><span data-stu-id="e636c-132">The `<serviceDebug>` tag defines whether the debug information feature is enabled for a WCF service.</span></span> <span data-ttu-id="e636c-133">Se l'attributo includeExceptionDetailInFaults è impostato su true, le informazioni di eccezione dell'applicazione saranno restituite ai client.</span><span class="sxs-lookup"><span data-stu-id="e636c-133">If the attribute includeExceptionDetailInFaults is set to true, exception information from the application will be returned to clients.</span></span> <span data-ttu-id="e636c-134">Gli utenti malintenzionati possono sfruttare le informazioni aggiuntive che acquisiscono dall'output di debug per sferrare attacchi su framework, database o altre risorse usate dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="e636c-134">Attackers can leverage the additional information they gain from debugging output to mount attacks targeted on the framework, database, or other resources used by the application.</span></span> |

### <a name="example"></a><span data-ttu-id="e636c-135">Esempio</span><span class="sxs-lookup"><span data-stu-id="e636c-135">Example</span></span>
<span data-ttu-id="e636c-136">Il file di configurazione seguente include il tag `<serviceDebug>`:</span><span class="sxs-lookup"><span data-stu-id="e636c-136">The following configuration file includes the `<serviceDebug>` tag:</span></span> 
```
<configuration> 
<system.serviceModel> 
<behaviors> 
<serviceBehaviors> 
<behavior name=""MyServiceBehavior""> 
<serviceDebug includeExceptionDetailInFaults=""True"" httpHelpPageEnabled=""True""/> 
... 
```
<span data-ttu-id="e636c-137">Disabilitare le informazioni di debug nel servizio.</span><span class="sxs-lookup"><span data-stu-id="e636c-137">Disable debugging information in the service.</span></span> <span data-ttu-id="e636c-138">È possibile eseguire questa operazione rimuovendo il tag `<serviceDebug>` dal file di configurazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="e636c-138">This can be accomplished by removing the `<serviceDebug>` tag from your application's configuration file.</span></span> 

## <span data-ttu-id="e636c-139"><a id="servicemetadata"></a>WCF - non includere il nodo serviceMetadata nel file di configurazione</span><span class="sxs-lookup"><span data-stu-id="e636c-139"><a id="servicemetadata"></a>WCF- Do not include serviceMetadata node in configuration file</span></span>

| <span data-ttu-id="e636c-140">Titolo</span><span class="sxs-lookup"><span data-stu-id="e636c-140">Title</span></span>                   | <span data-ttu-id="e636c-141">Dettagli</span><span class="sxs-lookup"><span data-stu-id="e636c-141">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="e636c-142">**Componente**</span><span class="sxs-lookup"><span data-stu-id="e636c-142">**Component**</span></span>               | <span data-ttu-id="e636c-143">WCF</span><span class="sxs-lookup"><span data-stu-id="e636c-143">WCF</span></span> | 
| <span data-ttu-id="e636c-144">**Fase SDL**</span><span class="sxs-lookup"><span data-stu-id="e636c-144">**SDL Phase**</span></span>               | <span data-ttu-id="e636c-145">Compilare</span><span class="sxs-lookup"><span data-stu-id="e636c-145">Build</span></span> |  
| <span data-ttu-id="e636c-146">**Tecnologie applicabili**</span><span class="sxs-lookup"><span data-stu-id="e636c-146">**Applicable Technologies**</span></span> | <span data-ttu-id="e636c-147">Generico</span><span class="sxs-lookup"><span data-stu-id="e636c-147">Generic</span></span> |
| <span data-ttu-id="e636c-148">**Attributes (Attributi) (Attributi)**</span><span class="sxs-lookup"><span data-stu-id="e636c-148">**Attributes**</span></span>              | <span data-ttu-id="e636c-149">Generico, .NET Framework 3</span><span class="sxs-lookup"><span data-stu-id="e636c-149">Generic, NET Framework 3</span></span> |
| <span data-ttu-id="e636c-150">**Riferimenti**</span><span class="sxs-lookup"><span data-stu-id="e636c-150">**References**</span></span>              | <span data-ttu-id="e636c-151">[MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html)</span><span class="sxs-lookup"><span data-stu-id="e636c-151">[MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html)</span></span> |
| <span data-ttu-id="e636c-152">**Passaggi**</span><span class="sxs-lookup"><span data-stu-id="e636c-152">**Steps**</span></span> | <span data-ttu-id="e636c-153">Esponendo pubblicamente informazioni su un servizio è possibile consentire agli hacker di comprendere in che modo possono sfruttare il servizio stesso.</span><span class="sxs-lookup"><span data-stu-id="e636c-153">Publicly exposing information about a service can provide attackers with valuable insight into how they might exploit the service.</span></span> <span data-ttu-id="e636c-154">Il tag `<serviceMetadata>` abilita la funzionalità di pubblicazione dei metadati.</span><span class="sxs-lookup"><span data-stu-id="e636c-154">The `<serviceMetadata>` tag enables the metadata publishing feature.</span></span> <span data-ttu-id="e636c-155">I metadati del servizio potrebbero contenere informazioni riservate che non devono essere accessibili pubblicamente.</span><span class="sxs-lookup"><span data-stu-id="e636c-155">Service metadata could contain sensitive information that should not be publicly accessible.</span></span> <span data-ttu-id="e636c-156">Come minimo, consentire solo agli utenti attendibili di accedere ai metadati e assicurarsi che le informazioni non necessarie non siano esposte.</span><span class="sxs-lookup"><span data-stu-id="e636c-156">At a minimum, only allow trusted users to access the metadata and ensure that unnecessary information is not exposed.</span></span> <span data-ttu-id="e636c-157">Ancora meglio, disabilitare completamente la possibilità di pubblicare metadati.</span><span class="sxs-lookup"><span data-stu-id="e636c-157">Better yet, entirely disable the ability to publish metadata.</span></span> <span data-ttu-id="e636c-158">Una configurazione di WCF sicura non conterrà il tag `<serviceMetadata>`.</span><span class="sxs-lookup"><span data-stu-id="e636c-158">A safe WCF configuration will not contain the `<serviceMetadata>` tag.</span></span> |

## <span data-ttu-id="e636c-159"><a id="exception"></a>Assicurare una gestione appropriata delle eccezioni in API Web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="e636c-159"><a id="exception"></a>Ensure that proper exception handling is done in ASP.NET Web API</span></span>

| <span data-ttu-id="e636c-160">Titolo</span><span class="sxs-lookup"><span data-stu-id="e636c-160">Title</span></span>                   | <span data-ttu-id="e636c-161">Dettagli</span><span class="sxs-lookup"><span data-stu-id="e636c-161">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="e636c-162">**Componente**</span><span class="sxs-lookup"><span data-stu-id="e636c-162">**Component**</span></span>               | <span data-ttu-id="e636c-163">API Web</span><span class="sxs-lookup"><span data-stu-id="e636c-163">Web API</span></span> | 
| <span data-ttu-id="e636c-164">**Fase SDL**</span><span class="sxs-lookup"><span data-stu-id="e636c-164">**SDL Phase**</span></span>               | <span data-ttu-id="e636c-165">Compilare</span><span class="sxs-lookup"><span data-stu-id="e636c-165">Build</span></span> |  
| <span data-ttu-id="e636c-166">**Tecnologie applicabili**</span><span class="sxs-lookup"><span data-stu-id="e636c-166">**Applicable Technologies**</span></span> | <span data-ttu-id="e636c-167">MVC 5, MVC 6</span><span class="sxs-lookup"><span data-stu-id="e636c-167">MVC 5, MVC 6</span></span> |
| <span data-ttu-id="e636c-168">**Attributes (Attributi) (Attributi)**</span><span class="sxs-lookup"><span data-stu-id="e636c-168">**Attributes**</span></span>              | <span data-ttu-id="e636c-169">N/D</span><span class="sxs-lookup"><span data-stu-id="e636c-169">N/A</span></span>  |
| <span data-ttu-id="e636c-170">**Riferimenti**</span><span class="sxs-lookup"><span data-stu-id="e636c-170">**References**</span></span>              | <span data-ttu-id="e636c-171">[Gestione delle eccezioni in API Web ASP.NET](http://www.asp.net/web-api/overview/error-handling/exception-handling), [convalida del modello in API Web ASP.NET](http://www.asp.net/web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api)</span><span class="sxs-lookup"><span data-stu-id="e636c-171">[Exception Handling in ASP.NET Web API](http://www.asp.net/web-api/overview/error-handling/exception-handling), [Model Validation in ASP.NET Web API](http://www.asp.net/web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api)</span></span> |
| <span data-ttu-id="e636c-172">**Passaggi**</span><span class="sxs-lookup"><span data-stu-id="e636c-172">**Steps**</span></span> | <span data-ttu-id="e636c-173">Per impostazione predefinita, la maggior parte delle eccezioni non rilevate in API Web ASP.NET vengono convertite in una risposta HTTP con codice di stato `500, Internal Server Error`</span><span class="sxs-lookup"><span data-stu-id="e636c-173">By default, most uncaught exceptions in ASP.NET Web API are translated into an HTTP response with status code `500, Internal Server Error`</span></span>|

### <a name="example"></a><span data-ttu-id="e636c-174">Esempio</span><span class="sxs-lookup"><span data-stu-id="e636c-174">Example</span></span>
<span data-ttu-id="e636c-175">Per controllare il codice di stato restituito dall'API, è possibile usare `HttpResponseException` come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="e636c-175">To control the status code returned by the API, `HttpResponseException` can be used as shown below:</span></span> 
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

### <a name="example"></a><span data-ttu-id="e636c-176">Esempio</span><span class="sxs-lookup"><span data-stu-id="e636c-176">Example</span></span>
<span data-ttu-id="e636c-177">Per controllare ulteriormente la risposta di eccezione, è possibile usare la classe `HttpResponseMessage` come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="e636c-177">For further control on the exception response, the `HttpResponseMessage` class can be used as shown below:</span></span> 
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
<span data-ttu-id="e636c-178">Per intercettare le eccezioni non gestite che non sono del tipo `HttpResponseException`, è possibile usare filtri eccezioni.</span><span class="sxs-lookup"><span data-stu-id="e636c-178">To catch unhandled exceptions that are not of the type `HttpResponseException`, Exception Filters can be used.</span></span> <span data-ttu-id="e636c-179">I filtri eccezioni implementano l'interfaccia `System.Web.Http.Filters.IExceptionFilter`.</span><span class="sxs-lookup"><span data-stu-id="e636c-179">Exception filters implement the `System.Web.Http.Filters.IExceptionFilter` interface.</span></span> <span data-ttu-id="e636c-180">Il modo più semplice per scrivere un filtro eccezioni è derivare la classe `System.Web.Http.Filters.ExceptionFilterAttribute` ed eseguire l'override del metodo OnException.</span><span class="sxs-lookup"><span data-stu-id="e636c-180">The simplest way to write an exception filter is to derive from the `System.Web.Http.Filters.ExceptionFilterAttribute` class and override the OnException method.</span></span> 

### <a name="example"></a><span data-ttu-id="e636c-181">Esempio</span><span class="sxs-lookup"><span data-stu-id="e636c-181">Example</span></span>
<span data-ttu-id="e636c-182">Ecco un filtro che converte le eccezioni `NotImplementedException` nel codice di stato HTTP `501, Not Implemented`:</span><span class="sxs-lookup"><span data-stu-id="e636c-182">Here is a filter that converts `NotImplementedException` exceptions into HTTP status code `501, Not Implemented`:</span></span> 
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

<span data-ttu-id="e636c-183">Esistono diversi modi per registrare un filtro eccezioni API Web:</span><span class="sxs-lookup"><span data-stu-id="e636c-183">There are several ways to register a Web API exception filter:</span></span>
- <span data-ttu-id="e636c-184">Tramite un'azione</span><span class="sxs-lookup"><span data-stu-id="e636c-184">By action</span></span>
- <span data-ttu-id="e636c-185">Tramite un controller</span><span class="sxs-lookup"><span data-stu-id="e636c-185">By controller</span></span>
- <span data-ttu-id="e636c-186">A livello globale</span><span class="sxs-lookup"><span data-stu-id="e636c-186">Globally</span></span>

### <a name="example"></a><span data-ttu-id="e636c-187">Esempio</span><span class="sxs-lookup"><span data-stu-id="e636c-187">Example</span></span>
<span data-ttu-id="e636c-188">Per applicare il filtro a un'azione specifica, aggiungere il filtro come attributo per l'azione:</span><span class="sxs-lookup"><span data-stu-id="e636c-188">To apply the filter to a specific action, add the filter as an attribute to the action:</span></span> 
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
### <a name="example"></a><span data-ttu-id="e636c-189">Esempio</span><span class="sxs-lookup"><span data-stu-id="e636c-189">Example</span></span>
<span data-ttu-id="e636c-190">Per applicare il filtro a tutte le azioni in un `controller`, aggiungere il filtro come attributo per la classe `controller`:</span><span class="sxs-lookup"><span data-stu-id="e636c-190">To apply the filter to all of the actions on a `controller`, add the filter as an attribute to the `controller` class:</span></span> 

```C#
[NotImplExceptionFilter]
public class ProductsController : ApiController
{
    // ...
}
```

### <a name="example"></a><span data-ttu-id="e636c-191">Esempio</span><span class="sxs-lookup"><span data-stu-id="e636c-191">Example</span></span>
<span data-ttu-id="e636c-192">Per applicare il filtro a livello globale per tutti i controller API Web, aggiungere un'istanza del filtro alla raccolta `GlobalConfiguration.Configuration.Filters`.</span><span class="sxs-lookup"><span data-stu-id="e636c-192">To apply the filter globally to all Web API controllers, add an instance of the filter to the `GlobalConfiguration.Configuration.Filters` collection.</span></span> <span data-ttu-id="e636c-193">I filtri eccezioni in questa raccolta si applicano a qualsiasi azione del controller API Web.</span><span class="sxs-lookup"><span data-stu-id="e636c-193">Exception filters in this collection apply to any Web API controller action.</span></span> 
```C#
GlobalConfiguration.Configuration.Filters.Add(
    new ProductStore.NotImplExceptionFilterAttribute());
```

### <a name="example"></a><span data-ttu-id="e636c-194">Esempio</span><span class="sxs-lookup"><span data-stu-id="e636c-194">Example</span></span>
<span data-ttu-id="e636c-195">Per la convalida del modello, lo stato del modello può essere passato al metodo CreateErrorResponse come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="e636c-195">For model validation, the model state can be passed to CreateErrorResponse method as shown below:</span></span> 
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

<span data-ttu-id="e636c-196">Controllare i collegamenti nella sezione Riferimenti per altre informazioni sulla gestione delle eccezioni e la convalida del modello in API Web ASP.Net</span><span class="sxs-lookup"><span data-stu-id="e636c-196">Check the links in the references section for additional details about exceptional handling and model validation in ASP.Net Web API</span></span> 

## <span data-ttu-id="e636c-197"><a id="messages"></a>Non esporre informazioni di sicurezza nei messaggi di errore</span><span class="sxs-lookup"><span data-stu-id="e636c-197"><a id="messages"></a>Do not expose security details in error messages</span></span>

| <span data-ttu-id="e636c-198">Titolo</span><span class="sxs-lookup"><span data-stu-id="e636c-198">Title</span></span>                   | <span data-ttu-id="e636c-199">Dettagli</span><span class="sxs-lookup"><span data-stu-id="e636c-199">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="e636c-200">**Componente**</span><span class="sxs-lookup"><span data-stu-id="e636c-200">**Component**</span></span>               | <span data-ttu-id="e636c-201">Applicazione Web.</span><span class="sxs-lookup"><span data-stu-id="e636c-201">Web Application</span></span> | 
| <span data-ttu-id="e636c-202">**Fase SDL**</span><span class="sxs-lookup"><span data-stu-id="e636c-202">**SDL Phase**</span></span>               | <span data-ttu-id="e636c-203">Compilare</span><span class="sxs-lookup"><span data-stu-id="e636c-203">Build</span></span> |  
| <span data-ttu-id="e636c-204">**Tecnologie applicabili**</span><span class="sxs-lookup"><span data-stu-id="e636c-204">**Applicable Technologies**</span></span> | <span data-ttu-id="e636c-205">Generico</span><span class="sxs-lookup"><span data-stu-id="e636c-205">Generic</span></span> |
| <span data-ttu-id="e636c-206">**Attributes (Attributi) (Attributi)**</span><span class="sxs-lookup"><span data-stu-id="e636c-206">**Attributes**</span></span>              | <span data-ttu-id="e636c-207">N/D</span><span class="sxs-lookup"><span data-stu-id="e636c-207">N/A</span></span>  |
| <span data-ttu-id="e636c-208">**Riferimenti**</span><span class="sxs-lookup"><span data-stu-id="e636c-208">**References**</span></span>              | <span data-ttu-id="e636c-209">N/D</span><span class="sxs-lookup"><span data-stu-id="e636c-209">N/A</span></span>  |
| <span data-ttu-id="e636c-210">**Passaggi**</span><span class="sxs-lookup"><span data-stu-id="e636c-210">**Steps**</span></span> | <p><span data-ttu-id="e636c-211">I messaggi di errore generici vengono forniti direttamente all'utente senza includere dati sensibili dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="e636c-211">Generic error messages are provided directly to the user without including sensitive application data.</span></span> <span data-ttu-id="e636c-212">Esempi di dati sensibili:</span><span class="sxs-lookup"><span data-stu-id="e636c-212">Examples of sensitive data include:</span></span></p><ul><li><span data-ttu-id="e636c-213">Nomi dei server</span><span class="sxs-lookup"><span data-stu-id="e636c-213">Server names</span></span></li><li><span data-ttu-id="e636c-214">Stringhe di connessione</span><span class="sxs-lookup"><span data-stu-id="e636c-214">Connection strings</span></span></li><li><span data-ttu-id="e636c-215">Nomi utente</span><span class="sxs-lookup"><span data-stu-id="e636c-215">Usernames</span></span></li><li><span data-ttu-id="e636c-216">Password</span><span class="sxs-lookup"><span data-stu-id="e636c-216">Passwords</span></span></li><li><span data-ttu-id="e636c-217">Procedure SQL</span><span class="sxs-lookup"><span data-stu-id="e636c-217">SQL procedures</span></span></li><li><span data-ttu-id="e636c-218">Dettagli di errori SQL dinamici</span><span class="sxs-lookup"><span data-stu-id="e636c-218">Details of dynamic SQL failures</span></span></li><li><span data-ttu-id="e636c-219">Analisi dello stack e righe di codice</span><span class="sxs-lookup"><span data-stu-id="e636c-219">Stack trace and lines of code</span></span></li><li><span data-ttu-id="e636c-220">Variabili archiviate in memoria</span><span class="sxs-lookup"><span data-stu-id="e636c-220">Variables stored in memory</span></span></li><li><span data-ttu-id="e636c-221">Percorsi di unità e cartelle</span><span class="sxs-lookup"><span data-stu-id="e636c-221">Drive and folder locations</span></span></li><li><span data-ttu-id="e636c-222">Punti di installazione dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="e636c-222">Application install points</span></span></li><li><span data-ttu-id="e636c-223">Impostazioni di configurazione dell'host</span><span class="sxs-lookup"><span data-stu-id="e636c-223">Host configuration settings</span></span></li><li><span data-ttu-id="e636c-224">Altri dettagli di un'applicazione interna</span><span class="sxs-lookup"><span data-stu-id="e636c-224">Other internal application details</span></span></li></ul><p><span data-ttu-id="e636c-225">Intercettando gli errori all'interno di un'applicazione e presentando messaggi di errore generici, nonché abilitando gli errori personalizzati all'interno di IIS, è possibile evitare la divulgazione di informazioni.</span><span class="sxs-lookup"><span data-stu-id="e636c-225">Trapping all errors within an application and providing generic error messages, as well as enabling custom errors within IIS will help prevent information disclosure.</span></span> <span data-ttu-id="e636c-226">La gestione delle eccezioni del database di SQL Server e .NET, tra le altre architetture, di gestione degli errori, è particolarmente dettagliata ed estremamente utile a un utente malintenzionato che esegue la profilatura dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="e636c-226">SQL Server database and .NET Exception handling, among other error handling architectures, are especially verbose and extremely useful to a malicious user profiling your application.</span></span> <span data-ttu-id="e636c-227">Non visualizzare direttamente il contenuto di una classe derivata dalla classe di eccezione .NET e assicurarsi di disporre della gestione delle eccezioni appropriata in modo che un'eccezione imprevista non venga generata direttamente a disposizione dell'utente.</span><span class="sxs-lookup"><span data-stu-id="e636c-227">Do not directly display the contents of a class derived from the .NET Exception class, and ensure that you have proper exception handling so that an unexpected exception isn't inadvertently raised directly to the user.</span></span></p><ul><li><span data-ttu-id="e636c-228">Fornire messaggi di errore generici direttamente all'utente che omettono dettagli specifici rilevati direttamente nel messaggio di eccezione o errore</span><span class="sxs-lookup"><span data-stu-id="e636c-228">Provide generic error messages directly to the user that abstract away specific details found directly in the exception/error message</span></span></li><li><span data-ttu-id="e636c-229">Non consentire direttamente all'utente di visualizzare il contenuto di una classe di eccezione .NET</span><span class="sxs-lookup"><span data-stu-id="e636c-229">Do not display the contents of a .NET exception class directly to the user</span></span></li><li><span data-ttu-id="e636c-230">Intercettare tutti i messaggi di errore e se necessario informare l'utente tramite un messaggio di errore generico inviato al client dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="e636c-230">Trap all error messages and if appropriate inform the user via a generic error message sent to the application client</span></span></li><li><span data-ttu-id="e636c-231">Non esporre il contenuto della classe di eccezione direttamente all'utente, in particolare il valore restituito da `.ToString()`, oppure i valori delle proprietà del messaggio o dell'analisi dello stack.</span><span class="sxs-lookup"><span data-stu-id="e636c-231">Do not expose the contents of the Exception class directly to the user, especially the return value from `.ToString()`, or the values of the Message or StackTrace properties.</span></span> <span data-ttu-id="e636c-232">Registrare in modo sicuro queste informazioni e mostrare un messaggio più innocuo all'utente</span><span class="sxs-lookup"><span data-stu-id="e636c-232">Securely log this information and display a more innocuous message to the user</span></span></li></ul>|

## <span data-ttu-id="e636c-233"><a id="default"></a>Implementare la pagina di gestione degli errori predefiniti</span><span class="sxs-lookup"><span data-stu-id="e636c-233"><a id="default"></a>Implement Default error handling page</span></span>

| <span data-ttu-id="e636c-234">Titolo</span><span class="sxs-lookup"><span data-stu-id="e636c-234">Title</span></span>                   | <span data-ttu-id="e636c-235">Dettagli</span><span class="sxs-lookup"><span data-stu-id="e636c-235">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="e636c-236">**Componente**</span><span class="sxs-lookup"><span data-stu-id="e636c-236">**Component**</span></span>               | <span data-ttu-id="e636c-237">Applicazione Web.</span><span class="sxs-lookup"><span data-stu-id="e636c-237">Web Application</span></span> | 
| <span data-ttu-id="e636c-238">**Fase SDL**</span><span class="sxs-lookup"><span data-stu-id="e636c-238">**SDL Phase**</span></span>               | <span data-ttu-id="e636c-239">Compilare</span><span class="sxs-lookup"><span data-stu-id="e636c-239">Build</span></span> |  
| <span data-ttu-id="e636c-240">**Tecnologie applicabili**</span><span class="sxs-lookup"><span data-stu-id="e636c-240">**Applicable Technologies**</span></span> | <span data-ttu-id="e636c-241">Generico</span><span class="sxs-lookup"><span data-stu-id="e636c-241">Generic</span></span> |
| <span data-ttu-id="e636c-242">**Attributes (Attributi) (Attributi)**</span><span class="sxs-lookup"><span data-stu-id="e636c-242">**Attributes**</span></span>              | <span data-ttu-id="e636c-243">N/D</span><span class="sxs-lookup"><span data-stu-id="e636c-243">N/A</span></span>  |
| <span data-ttu-id="e636c-244">**Riferimenti**</span><span class="sxs-lookup"><span data-stu-id="e636c-244">**References**</span></span>              | <span data-ttu-id="e636c-245">[Modificare la finestra di dialogo delle impostazioni pagine di errore ASP.NET](https://technet.microsoft.com/library/dd569096(WS.10).aspx)</span><span class="sxs-lookup"><span data-stu-id="e636c-245">[Edit ASP.NET Error Pages Settings Dialog Box](https://technet.microsoft.com/library/dd569096(WS.10).aspx)</span></span> |
| <span data-ttu-id="e636c-246">**Passaggi**</span><span class="sxs-lookup"><span data-stu-id="e636c-246">**Steps**</span></span> | <p><span data-ttu-id="e636c-247">Quando un'applicazione ASP.NET ha esito negativo e causa un errore Server interno HTTP/1.x 500 o una configurazione di funzionalità (ad esempio, il filtro richieste) impedisce la visualizzazione di una pagina, verrà generato un messaggio di errore.</span><span class="sxs-lookup"><span data-stu-id="e636c-247">When an ASP.NET application fails and causes an HTTP/1.x 500 Internal Server Error, or a feature configuration (such as Request Filtering) prevents a page from being displayed, an error message will be generated.</span></span> <span data-ttu-id="e636c-248">Gli amministratori possono scegliere se nell'applicazione viene visualizzato un messaggio descrittivo per il client, il messaggio di errore dettagliato per il client o il messaggio di errore dettagliato solo a localhost.</span><span class="sxs-lookup"><span data-stu-id="e636c-248">Administrators can choose whether or not the application should display a friendly message to the client, detailed error message to the client, or detailed error message to localhost only.</span></span> <span data-ttu-id="e636c-249">Il tag <customErrors> in web.config ha tre modalità:</span><span class="sxs-lookup"><span data-stu-id="e636c-249">The <customErrors> tag in the web.config has three modes:</span></span></p><ul><li><span data-ttu-id="e636c-250">**On:** specifica che gli errori personalizzati sono attivati.</span><span class="sxs-lookup"><span data-stu-id="e636c-250">**On:** Specifies that custom errors are enabled.</span></span> <span data-ttu-id="e636c-251">Se non viene specificato alcun attributo defaultRedirect, gli utenti visualizzato un errore generico.</span><span class="sxs-lookup"><span data-stu-id="e636c-251">If no defaultRedirect attribute is specified, users see a generic error.</span></span> <span data-ttu-id="e636c-252">Gli errori personalizzati vengono visualizzati sui client remoti e sull'host locale</span><span class="sxs-lookup"><span data-stu-id="e636c-252">The custom errors are shown to the remote clients and to the local host</span></span></li><li><span data-ttu-id="e636c-253">**Off:** specifica che gli errori personalizzati sono disattivati.</span><span class="sxs-lookup"><span data-stu-id="e636c-253">**Off:** Specifies that custom errors are disabled.</span></span> <span data-ttu-id="e636c-254">Gli errori ASP.NET dettagliati vengono visualizzati sui client remoti e sull'host locale</span><span class="sxs-lookup"><span data-stu-id="e636c-254">The detailed ASP.NET errors are shown to the remote clients and to the local host</span></span></li><li><span data-ttu-id="e636c-255">**RemoteOnly:** specifica che gli errori personalizzati vengono visualizzati solo sui client remoti e gli errori ASP.NET vengono visualizzati sull'host locale.</span><span class="sxs-lookup"><span data-stu-id="e636c-255">**RemoteOnly:** Specifies that custom errors are shown only to the remote clients, and that ASP.NET errors are shown to the local host.</span></span> <span data-ttu-id="e636c-256">Si tratta del valore predefinito</span><span class="sxs-lookup"><span data-stu-id="e636c-256">This is the default value</span></span></li></ul><p><span data-ttu-id="e636c-257">Aprire il file `web.config` per il sito/applicazione e assicurarsi che per il tag sia definito `<customErrors mode="RemoteOnly" />` o `<customErrors mode="On" />`.</span><span class="sxs-lookup"><span data-stu-id="e636c-257">Open the `web.config` file for the application/site and ensure that the tag has either `<customErrors mode="RemoteOnly" />` or `<customErrors mode="On" />` defined.</span></span></p>|

## <span data-ttu-id="e636c-258"><a id="deployment"></a>Impostare il metodo di distribuzione al dettaglio in IIS</span><span class="sxs-lookup"><span data-stu-id="e636c-258"><a id="deployment"></a>Set Deployment Method to Retail in IIS</span></span>

| <span data-ttu-id="e636c-259">Titolo</span><span class="sxs-lookup"><span data-stu-id="e636c-259">Title</span></span>                   | <span data-ttu-id="e636c-260">Dettagli</span><span class="sxs-lookup"><span data-stu-id="e636c-260">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="e636c-261">**Componente**</span><span class="sxs-lookup"><span data-stu-id="e636c-261">**Component**</span></span>               | <span data-ttu-id="e636c-262">Applicazione Web.</span><span class="sxs-lookup"><span data-stu-id="e636c-262">Web Application</span></span> | 
| <span data-ttu-id="e636c-263">**Fase SDL**</span><span class="sxs-lookup"><span data-stu-id="e636c-263">**SDL Phase**</span></span>               | <span data-ttu-id="e636c-264">Distribuzione</span><span class="sxs-lookup"><span data-stu-id="e636c-264">Deployment</span></span> |  
| <span data-ttu-id="e636c-265">**Tecnologie applicabili**</span><span class="sxs-lookup"><span data-stu-id="e636c-265">**Applicable Technologies**</span></span> | <span data-ttu-id="e636c-266">Generico</span><span class="sxs-lookup"><span data-stu-id="e636c-266">Generic</span></span> |
| <span data-ttu-id="e636c-267">**Attributes (Attributi) (Attributi)**</span><span class="sxs-lookup"><span data-stu-id="e636c-267">**Attributes**</span></span>              | <span data-ttu-id="e636c-268">N/D</span><span class="sxs-lookup"><span data-stu-id="e636c-268">N/A</span></span>  |
| <span data-ttu-id="e636c-269">**Riferimenti**</span><span class="sxs-lookup"><span data-stu-id="e636c-269">**References**</span></span>              | <span data-ttu-id="e636c-270">[Element distribuzione (schema impostazioni ASP.NET)](https://msdn.microsoft.com/library/ms228298(VS.80).aspx)</span><span class="sxs-lookup"><span data-stu-id="e636c-270">[deployment Element (ASP.NET Settings Schema)](https://msdn.microsoft.com/library/ms228298(VS.80).aspx)</span></span> |
| <span data-ttu-id="e636c-271">**Passaggi**</span><span class="sxs-lookup"><span data-stu-id="e636c-271">**Steps**</span></span> | <p><span data-ttu-id="e636c-272">Lo switch `<deployment retail>` deve essere usato dai server IIS di produzione.</span><span class="sxs-lookup"><span data-stu-id="e636c-272">The `<deployment retail>` switch is intended for use by production IIS servers.</span></span> <span data-ttu-id="e636c-273">Questo switch viene usato per gestire applicazioni con le migliori prestazioni possibili e minime fughe di informazioni di sicurezza disabilitando la capacità dell'applicazione per generare l'output di traccia in una pagina, disattivando la possibilità di visualizzare messaggi di errore dettagliati per gli utenti finali e disattivando l'opzione di debug.</span><span class="sxs-lookup"><span data-stu-id="e636c-273">This switch is used to help applications run with the best possible performance and least possible security information leakages by disabling the application's ability to generate trace output on a page, disabling the ability to display detailed error messages to end users, and disabling the debug switch.</span></span></p><p><span data-ttu-id="e636c-274">Spesso, gli switch e le opzioni che sono destinati agli sviluppatori, ad esempio traccia delle richieste no riuscite e debug, sono abilitati durante lo sviluppo attivo.</span><span class="sxs-lookup"><span data-stu-id="e636c-274">Often times, switches and options that are developer-focused, such as failed request tracing and debugging, are enabled during active development.</span></span> <span data-ttu-id="e636c-275">È consigliabile che il metodo di distribuzione in qualsiasi server di produzione sia impostato su vendita al dettaglio.</span><span class="sxs-lookup"><span data-stu-id="e636c-275">It is recommended that the deployment method on any production server be set to retail.</span></span> <span data-ttu-id="e636c-276">aprire il file machine.config e assicurarsi che `<deployment retail="true" />` resti impostato su true.</span><span class="sxs-lookup"><span data-stu-id="e636c-276">open the machine.config file and ensure that `<deployment retail="true" />` remains set to true.</span></span></p>|

## <span data-ttu-id="e636c-277"><a id="fail"></a>Le eccezioni devono avere esito negativo in modo sicuro</span><span class="sxs-lookup"><span data-stu-id="e636c-277"><a id="fail"></a>Exceptions should fail safely</span></span>

| <span data-ttu-id="e636c-278">Titolo</span><span class="sxs-lookup"><span data-stu-id="e636c-278">Title</span></span>                   | <span data-ttu-id="e636c-279">Dettagli</span><span class="sxs-lookup"><span data-stu-id="e636c-279">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="e636c-280">**Componente**</span><span class="sxs-lookup"><span data-stu-id="e636c-280">**Component**</span></span>               | <span data-ttu-id="e636c-281">Applicazione Web.</span><span class="sxs-lookup"><span data-stu-id="e636c-281">Web Application</span></span> | 
| <span data-ttu-id="e636c-282">**Fase SDL**</span><span class="sxs-lookup"><span data-stu-id="e636c-282">**SDL Phase**</span></span>               | <span data-ttu-id="e636c-283">Compilare</span><span class="sxs-lookup"><span data-stu-id="e636c-283">Build</span></span> |  
| <span data-ttu-id="e636c-284">**Tecnologie applicabili**</span><span class="sxs-lookup"><span data-stu-id="e636c-284">**Applicable Technologies**</span></span> | <span data-ttu-id="e636c-285">Generico</span><span class="sxs-lookup"><span data-stu-id="e636c-285">Generic</span></span> |
| <span data-ttu-id="e636c-286">**Attributes (Attributi) (Attributi)**</span><span class="sxs-lookup"><span data-stu-id="e636c-286">**Attributes**</span></span>              | <span data-ttu-id="e636c-287">N/D</span><span class="sxs-lookup"><span data-stu-id="e636c-287">N/A</span></span>  |
| <span data-ttu-id="e636c-288">**Riferimenti**</span><span class="sxs-lookup"><span data-stu-id="e636c-288">**References**</span></span>              | [<span data-ttu-id="e636c-289">Esito negativo in modo sicuro</span><span class="sxs-lookup"><span data-stu-id="e636c-289">Fail securely</span></span>](https://www.owasp.org/index.php/Fail_securely) |
| <span data-ttu-id="e636c-290">**Passaggi**</span><span class="sxs-lookup"><span data-stu-id="e636c-290">**Steps**</span></span> | <span data-ttu-id="e636c-291">L'applicazione deve avere esito negativo in modo sicuro.</span><span class="sxs-lookup"><span data-stu-id="e636c-291">Application should fail safely.</span></span> <span data-ttu-id="e636c-292">Per qualsiasi metodo che restituisce un valore booleano, in base al quale vengono prese determinate decisioni, è necessario creare con attenzione un blocco delle eccezioni.</span><span class="sxs-lookup"><span data-stu-id="e636c-292">Any method that returns a Boolean value, based on which certain decision is made, should have exception block carefully created.</span></span> <span data-ttu-id="e636c-293">Esistono molti errori logici che causano problemi di sicurezza quando il blocco delle eccezioni è scritto senza fare attenzione.</span><span class="sxs-lookup"><span data-stu-id="e636c-293">There are lot of logical errors due to which security issues creep in, when the exception block is written carelessly.</span></span>|

### <a name="example"></a><span data-ttu-id="e636c-294">Esempio</span><span class="sxs-lookup"><span data-stu-id="e636c-294">Example</span></span>
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
                        //// Adding additional check to enable CMS urls if they are not hosted on same domain.
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
<span data-ttu-id="e636c-295">Il metodo sopra indicato restituirà sempre True, se si verificano alcune eccezioni.</span><span class="sxs-lookup"><span data-stu-id="e636c-295">The above method will always return True, if some exception happens.</span></span> <span data-ttu-id="e636c-296">Se l'utente finale fornisce un URL in formato non valido, che il browser rispetta, ma il costruttore `Uri()` no, verrà generata un'eccezione e la vittima riuscirà ad accedere all'URL valido, ma in formato non valido.</span><span class="sxs-lookup"><span data-stu-id="e636c-296">If the end user provides a malformed URL, that the browser respects, but the `Uri()` constructor doesn't, this will throw an exception, and the victim will be taken to the valid but malformed URL.</span></span> 