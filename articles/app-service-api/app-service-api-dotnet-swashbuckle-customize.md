---
title: definizioni di aaaCustomize generato Swashbuckle API
description: Informazioni su come le definizioni delle API Swagger toocustomize generati da Swashbuckle per un'app per le API in Azure App Service.
services: app-service\api
documentationcenter: .net
author: bradygaster
manager: erikre
editor: jimbe
ms.assetid: 6b8cbc38-d282-4a0f-b0c5-762631bae6f3
ms.service: app-service-api
ms.workload: web
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 08/29/2016
ms.author: rachelap
ms.openlocfilehash: e31c665f8993533c5ec9a935e42cce34f86a5ade
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="customize-swashbuckle-generated-api-definitions"></a><span data-ttu-id="7ace6-103">Personalizzare le definizioni delle API generate da Swashbuckle</span><span class="sxs-lookup"><span data-stu-id="7ace6-103">Customize Swashbuckle-generated API definitions</span></span>
## <a name="overview"></a><span data-ttu-id="7ace6-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="7ace6-104">Overview</span></span>
<span data-ttu-id="7ace6-105">Questo articolo viene illustrato come toocustomize Swashbuckle toohandle scenari comuni in cui può essere tooalter hello comportamento predefinito:</span><span class="sxs-lookup"><span data-stu-id="7ace6-105">This article explains how toocustomize Swashbuckle toohandle common scenarios where you may want tooalter hello default behavior:</span></span>

* <span data-ttu-id="7ace6-106">Swashbuckle genera identificatori di operazione duplicati per gli overload dei metodi del controller</span><span class="sxs-lookup"><span data-stu-id="7ace6-106">Swashbuckle generates duplicate operation identifiers for overloads of controller methods</span></span>
* <span data-ttu-id="7ace6-107">Swashbuckle si presuppone che hello solo risposta valida da un metodo HTTP 200 (OK)</span><span class="sxs-lookup"><span data-stu-id="7ace6-107">Swashbuckle assumes that hello only valid response from a method is HTTP 200 (OK)</span></span> 

## <a name="customize-operation-identifier-generation"></a><span data-ttu-id="7ace6-108">Personalizzare la generazione di identificatori di operazione</span><span class="sxs-lookup"><span data-stu-id="7ace6-108">Customize operation identifier generation</span></span>
<span data-ttu-id="7ace6-109">Swashbuckle genera identificatori di operazione Swagger concatenando il nome del controller e il nome del metodo.</span><span class="sxs-lookup"><span data-stu-id="7ace6-109">Swashbuckle generates Swagger operation identifiers by concatenating controller name and method name.</span></span> <span data-ttu-id="7ace6-110">Questo modello provoca problemi quando sono presenti più overload di un metodo: Swashbuckle genera ID operazione duplicati, ovvero JSON Swagger non valido.</span><span class="sxs-lookup"><span data-stu-id="7ace6-110">This pattern creates a problem when you have multiple overloads of a method: Swashbuckle generates duplicate operation ids, which is invalid Swagger JSON.</span></span>

<span data-ttu-id="7ace6-111">Ad esempio hello seguente di codice del controller, Swashbuckle toogenerate tre ID operazione di Contact_Get.</span><span class="sxs-lookup"><span data-stu-id="7ace6-111">For example, hello following controller code causes Swashbuckle toogenerate three Contact_Get operation ids.</span></span>

![](./media/app-service-api-dotnet-swashbuckle-customize/multiplegetsincode.png)

![](./media/app-service-api-dotnet-swashbuckle-customize/multiplegetsinjson.png)

<span data-ttu-id="7ace6-112">È possibile risolvere il problema di hello manualmente, assegnando a metodi hello nomi univoci, come illustrato di seguito hello per questo esempio:</span><span class="sxs-lookup"><span data-stu-id="7ace6-112">You can solve hello problem manually by giving hello methods unique names, such as hello following for this example:</span></span>

* <span data-ttu-id="7ace6-113">Get</span><span class="sxs-lookup"><span data-stu-id="7ace6-113">Get</span></span>
* <span data-ttu-id="7ace6-114">GetById</span><span class="sxs-lookup"><span data-stu-id="7ace6-114">GetById</span></span>
* <span data-ttu-id="7ace6-115">GetPage</span><span class="sxs-lookup"><span data-stu-id="7ace6-115">GetPage</span></span>

<span data-ttu-id="7ace6-116">In alternativa Hello è tooextend Swashbuckle toomake genera automaticamente l'ID operazione univoco.</span><span class="sxs-lookup"><span data-stu-id="7ace6-116">hello alternative is tooextend Swashbuckle toomake it automatically generate unique operation ids.</span></span>

<span data-ttu-id="7ace6-117">Hello passaggi seguenti viene illustrato come toocustomize Swashbuckle utilizzando hello *SwaggerConfig.cs* file incluso nel progetto hello dal modello di progetto di Visual Studio API App Preview hello.</span><span class="sxs-lookup"><span data-stu-id="7ace6-117">hello following steps show how toocustomize Swashbuckle by using hello *SwaggerConfig.cs* file that is included in hello project by hello Visual Studio API Apps Preview project template.</span></span>  <span data-ttu-id="7ace6-118">È anche possibile personalizzare Swashbuckle in un progetto API Web configurato per la distribuzione come app per le API.</span><span class="sxs-lookup"><span data-stu-id="7ace6-118">You can also customize Swashbuckle in a Web API project that you configure for deployment as an API app.</span></span>

1. <span data-ttu-id="7ace6-119">Creare un'implementazione personalizzata di `IOperationFilter`</span><span class="sxs-lookup"><span data-stu-id="7ace6-119">Create a custom `IOperationFilter` implementation</span></span> 
   
    <span data-ttu-id="7ace6-120">Hello `IOperationFilter` interfaccia fornisce un punto di estensibilità per Swashbuckle gli utenti toocustomize vari aspetti del processo di metadati Swagger hello.</span><span class="sxs-lookup"><span data-stu-id="7ace6-120">hello `IOperationFilter` interface provides an extensibility point for Swashbuckle users who want toocustomize various aspects of hello Swagger metadata process.</span></span> <span data-ttu-id="7ace6-121">Hello codice riportato di seguito viene illustrato un metodo di modifica di comportamento di hello la generazione di id dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="7ace6-121">hello following code demonstrates one method of changing hello operation-id-generation behavior.</span></span> <span data-ttu-id="7ace6-122">codice Hello Accoda nome id operazione toohello i nomi del parametro.</span><span class="sxs-lookup"><span data-stu-id="7ace6-122">hello code appends parameter names toohello operation id name.</span></span>  
   
        using Swashbuckle.Swagger;
        using System.Web.Http.Description;
   
        namespace ContactsList
        {
            public class MultipleOperationsWithSameVerbFilter : IOperationFilter
            {
                public void Apply(
                    Operation operation,
                    SchemaRegistry schemaRegistry,
                    ApiDescription apiDescription)
                {
                    if (operation.parameters != null)
                    {
                        operation.operationId += "By";
                        foreach (var parm in operation.parameters)
                        {
                            operation.operationId += string.Format("{0}",parm.name);
                        }
                    }
                }
            }
        }
2. <span data-ttu-id="7ace6-123">In *App_Start\SwaggerConfig.cs* file, la chiamata hello `OperationFilter` nuovo hello toouse Swashbuckle toocause metodo `IOperationFilter` implementazione.</span><span class="sxs-lookup"><span data-stu-id="7ace6-123">In *App_Start\SwaggerConfig.cs* file, call hello `OperationFilter` method toocause Swashbuckle toouse hello new `IOperationFilter` implementation.</span></span>
   
        c.OperationFilter<MultipleOperationsWithSameVerbFilter>();
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/usefilter.png)
   
    <span data-ttu-id="7ace6-124">Hello *SwaggerConfig.cs* file che viene rimosso dal pacchetto Swashbuckle NuGet hello contiene molti esempi di commento di punti di estendibilità.</span><span class="sxs-lookup"><span data-stu-id="7ace6-124">hello *SwaggerConfig.cs* file that is dropped in by hello Swashbuckle NuGet package contains many commented-out examples of extensibility points.</span></span> <span data-ttu-id="7ace6-125">commenti aggiuntivi Hello non vengono visualizzati qui.</span><span class="sxs-lookup"><span data-stu-id="7ace6-125">hello additional comments are not shown here.</span></span> 
   
    <span data-ttu-id="7ace6-126">Dopo aver apportato questa modifica, il `IOperationFilter` implementazione viene usata determinando il toobe ID operazione univoco generato.</span><span class="sxs-lookup"><span data-stu-id="7ace6-126">After you make this change, your `IOperationFilter` implementation is used and causes unique operation ids toobe generated.</span></span>
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/uniqueids.png)

<a id="multiple-response-codes" name="multiple-response-codes"></a>

## <a name="allow-response-codes-other-than-200"></a><span data-ttu-id="7ace6-127">Consentire codici di risposta diversi da 200</span><span class="sxs-lookup"><span data-stu-id="7ace6-127">Allow response codes other than 200</span></span>
<span data-ttu-id="7ace6-128">Per impostazione predefinita, Swashbuckle si presuppone che una risposta HTTP 200 (OK) hello *solo* legittimo risposta da un metodo API Web.</span><span class="sxs-lookup"><span data-stu-id="7ace6-128">By default, Swashbuckle assumes that an HTTP 200 (OK) response is hello *only* legitimate response from a Web API method.</span></span> <span data-ttu-id="7ace6-129">In alcuni casi, è consigliabile tooreturn altri codici di risposta senza causare hello client tooraise un'eccezione.</span><span class="sxs-lookup"><span data-stu-id="7ace6-129">In some cases, you may want tooreturn other response codes without causing hello client tooraise an exception.</span></span>  <span data-ttu-id="7ace6-130">Ad esempio, hello API Web codice seguente viene illustrato uno scenario in cui è preferibile hello client tooaccept 200 o 404 come le risposte valide.</span><span class="sxs-lookup"><span data-stu-id="7ace6-130">For example, hello following Web API code demonstrates a scenario in which you would want hello client tooaccept either a 200 or a 404 as valid responses.</span></span>

    [ResponseType(typeof(Contact))]
    public HttpResponseMessage Get(int id)
    {
        var contacts = GetContacts();

        var requestedContact = contacts.FirstOrDefault(x => x.Id == id);

        if (requestedContact == null)
        {
            return Request.CreateResponse(HttpStatusCode.NotFound);
        }
        else
        {
            return Request.CreateResponse<Contact>(HttpStatusCode.OK, requestedContact);
        }
    }

<span data-ttu-id="7ace6-131">In questo scenario, hello Swagger che Swashbuckle genera per impostazione predefinita specifica solo un legittimo HTTP codice di stato HTTP 200.</span><span class="sxs-lookup"><span data-stu-id="7ace6-131">In this scenario, hello Swagger that Swashbuckle generates by default specifies only one legitimate HTTP status code, HTTP 200.</span></span>

![](./media/app-service-api-dotnet-swashbuckle-customize/http-200-output-only.png)

<span data-ttu-id="7ace6-132">Poiché Visual Studio utilizza hello codice toogenerate di definizione Swagger API per client hello, viene creato il codice client che genera un'eccezione per le risposte diverso da HTTP 200.</span><span class="sxs-lookup"><span data-stu-id="7ace6-132">Since Visual Studio uses hello Swagger API definition toogenerate code for hello client, it creates client code that raises an exception for any response other than an HTTP 200.</span></span> <span data-ttu-id="7ace6-133">codice Hello seguente proviene da un client c# generato per questo metodo API Web di esempio.</span><span class="sxs-lookup"><span data-stu-id="7ace6-133">hello code below is from a C# client generated for this sample Web API method.</span></span>

    if (statusCode != HttpStatusCode.OK)
    {
        HttpOperationException<object> ex = new HttpOperationException<object>();
        ex.Request = httpRequest;
        ex.Response = httpResponse;
        ex.Body = null;
        if (shouldTrace)
        {
            ServiceClientTracing.Error(invocationId, ex);
        }
        throw ex;
    } 

<span data-ttu-id="7ace6-134">Swashbuckle fornisce due modalità di personalizzazione di hello elenco dei codici di risposta HTTP previsto da esso generato, usando i commenti XML o hello `SwaggerResponse` attributo.</span><span class="sxs-lookup"><span data-stu-id="7ace6-134">Swashbuckle provides two ways of customizing hello list of expected HTTP response codes that it generates, using XML comments or hello `SwaggerResponse` attribute.</span></span> <span data-ttu-id="7ace6-135">attributo Hello è più semplice, ma è disponibile solo in Swashbuckle 5.1.5 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="7ace6-135">hello attribute is easier, but it is only available in Swashbuckle 5.1.5 or later.</span></span> <span data-ttu-id="7ace6-136">App per le API anteprima nuovo progetto modello in Visual Studio 2013 Hello include Swashbuckle versione 5.0.0, pertanto se si utilizza il modello di hello e non desidera tooupdate Swashbuckle, l'unica possibilità è toouse XML (commenti).</span><span class="sxs-lookup"><span data-stu-id="7ace6-136">hello API Apps preview new-project template in Visual Studio 2013 includes Swashbuckle version 5.0.0, so if you used hello template and don't want tooupdate Swashbuckle, your only option is toouse XML comments.</span></span> 

### <a name="customize-expected-response-codes-using-xml-comments"></a><span data-ttu-id="7ace6-137">Personalizzare i codici di risposta previsti con i commenti XML</span><span class="sxs-lookup"><span data-stu-id="7ace6-137">Customize expected response codes using XML comments</span></span>
<span data-ttu-id="7ace6-138">Utilizzare i codici di risposta toospecify questo metodo se la versione Swashbuckle è precedente a 5.1.5.</span><span class="sxs-lookup"><span data-stu-id="7ace6-138">Use this method toospecify response codes if your Swashbuckle version is earlier than 5.1.5.</span></span>

1. <span data-ttu-id="7ace6-139">Aggiungere innanzitutto i commenti della documentazione XML tramite metodi hello desiderato toospecify codici di risposta HTTP per.</span><span class="sxs-lookup"><span data-stu-id="7ace6-139">First, add XML documentation comments over hello methods you wish toospecify HTTP response codes for.</span></span> <span data-ttu-id="7ace6-140">Eseguire l'azione di API Web di esempio hello tooit di documentazione XML illustrato in precedenza e l'applicazione hello darà origine a codice simile al seguente esempio hello.</span><span class="sxs-lookup"><span data-stu-id="7ace6-140">Taking hello sample Web API action shown above and applying hello XML documentation tooit would result in code like hello following example.</span></span> 
   
        /// <summary>
        /// Returns hello specified contact.
        /// </summary>
        /// <param name="id">hello ID of hello contact.</param>
        /// <returns>A contact record with an HTTP 200, or null with an HTTP 404.</returns>
        /// <response code="200">OK</response>
        /// <response code="404">Not Found</response>
        [ResponseType(typeof(Contact))]
        public HttpResponseMessage Get(int id)
        {
            var contacts = GetContacts();
   
            var requestedContact = contacts.FirstOrDefault(x => x.Id == id);
   
            if (requestedContact == null)
            {
                return Request.CreateResponse(HttpStatusCode.NotFound);
            }
            else
            {
                return Request.CreateResponse<Contact>(HttpStatusCode.OK, requestedContact);
            }
        }
2. <span data-ttu-id="7ace6-141">Aggiungere le istruzioni in hello *SwaggerConfig.cs* toodirect Swashbuckle toomake utilizzo di file di documentazione XML hello del file.</span><span class="sxs-lookup"><span data-stu-id="7ace6-141">Add instructions in hello *SwaggerConfig.cs* file toodirect Swashbuckle toomake use of hello XML documentation file.</span></span>
   
   * <span data-ttu-id="7ace6-142">Aprire *SwaggerConfig.cs* e creare un metodo su hello *SwaggerConfig* classe toospecify hello percorso toohello file XML della documentazione.</span><span class="sxs-lookup"><span data-stu-id="7ace6-142">Open *SwaggerConfig.cs* and create a method on hello *SwaggerConfig* class toospecify hello path toohello documentation XML file.</span></span> 
     
           private static string GetXmlCommentsPath()
           {
               return string.Format(@"{0}\XmlComments.xml", 
                   System.AppDomain.CurrentDomain.BaseDirectory);
           }
   * <span data-ttu-id="7ace6-143">Scorrere verso il basso hello *SwaggerConfig.cs* file finché non viene visualizzata una riga di commento hello di codice simile hello schermata.</span><span class="sxs-lookup"><span data-stu-id="7ace6-143">Scroll down in hello *SwaggerConfig.cs* file until you see hello commented-out line of code resembling hello screen shot below.</span></span> 
     
       ![](./media/app-service-api-dotnet-swashbuckle-customize/xml-comments-commented-out.png)
   * <span data-ttu-id="7ace6-144">Rimuovere il commento hello riga tooenable hello XML elaborazione dei commenti durante la generazione di Swagger.</span><span class="sxs-lookup"><span data-stu-id="7ace6-144">Uncomment hello line tooenable hello XML comments processing during Swagger generation.</span></span> 
     
       ![](./media/app-service-api-dotnet-swashbuckle-customize/xml-comments-uncommented.png)
3. <span data-ttu-id="7ace6-145">Nel file di documentazione XML hello toogenerate ordine, passare la proprietà del progetto hello e abilitare i file di documentazione XML hello come illustrato nella schermata di hello riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="7ace6-145">In order toogenerate hello XML documentation file, go into hello project's properties and enable hello XML documentation file as shown in hello screenshot below.</span></span> 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/enable-xml-documentation-file.png) 

<span data-ttu-id="7ace6-146">Dopo aver eseguito questi passaggi, hello Swagger JSON generato da Swashbuckle rifletterà i codici di risposta HTTP hello specificato nei commenti XML hello.</span><span class="sxs-lookup"><span data-stu-id="7ace6-146">Once you perform these steps, hello Swagger JSON generated by Swashbuckle will reflect hello HTTP response codes that you specified in hello XML comments.</span></span> <span data-ttu-id="7ace6-147">schermata di Hello riportata di seguito viene illustrato questo nuovo payload JSON.</span><span class="sxs-lookup"><span data-stu-id="7ace6-147">hello screenshot below demonstrates this new JSON payload.</span></span> 

![](./media/app-service-api-dotnet-swashbuckle-customize/swagger-multiple-responses.png)

<span data-ttu-id="7ace6-148">Quando si utilizza codice di Visual Studio tooregenerate hello del client per l'API REST, il codice c# di hello accetta i codici di stato HTTP di OK e non trovato entrambi hello senza generare un'eccezione, che consente le decisioni di toomake dispendiosa in termini di codice in modalità toohandle hello restituiscono un valore null Record del contatto.</span><span class="sxs-lookup"><span data-stu-id="7ace6-148">When you use Visual Studio tooregenerate hello client code for your REST API, hello C# code accepts both hello HTTP OK and Not Found status codes without raising an exception, allowing your consuming code toomake decisions on how toohandle hello return of a null Contact record.</span></span> 

        if (statusCode != HttpStatusCode.OK && statusCode != HttpStatusCode.NotFound)
        {
            HttpOperationException<object> ex = new HttpOperationException<object>();
            ex.Request = httpRequest;
            ex.Response = httpResponse;
            ex.Body = null;
            if (shouldTrace)
            {
                ServiceClientTracing.Error(invocationId, ex);
            }
                throw ex;
        }

<span data-ttu-id="7ace6-149">codice Hello per questa dimostrazione è reperibile [questo repository GitHub](https://github.com/Azure-Samples/app-service-api-dotnet-swashbuckle-swaggerresponse).</span><span class="sxs-lookup"><span data-stu-id="7ace6-149">hello code for this demonstration can be found in [this GitHub repository](https://github.com/Azure-Samples/app-service-api-dotnet-swashbuckle-swaggerresponse).</span></span> <span data-ttu-id="7ace6-150">Insieme a Web API hello progetto contrassegnato con commenti della documentazione XML è un progetto di applicazione Console che contiene un client generato per questa API.</span><span class="sxs-lookup"><span data-stu-id="7ace6-150">Along with hello Web API project marked up with XML documentation comments is a Console Application project that contains a generated client for this API.</span></span> 

### <a name="customize-expected-response-codes-using-hello-swaggerresponse-attribute"></a><span data-ttu-id="7ace6-151">Personalizzare i codici di risposta previsto utilizzando l'attributo SwaggerResponse hello</span><span class="sxs-lookup"><span data-stu-id="7ace6-151">Customize expected response codes using hello SwaggerResponse attribute</span></span>
<span data-ttu-id="7ace6-152">Hello [SwaggerResponse](https://github.com/domaindrivendev/Swashbuckle/blob/master/Swashbuckle.Core/Swagger/Annotations/SwaggerResponseAttribute.cs) attributo è disponibile in Swashbuckle 5.1.5 e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="7ace6-152">hello [SwaggerResponse](https://github.com/domaindrivendev/Swashbuckle/blob/master/Swashbuckle.Core/Swagger/Annotations/SwaggerResponseAttribute.cs) attribute is available in Swashbuckle 5.1.5 and later.</span></span> <span data-ttu-id="7ace6-153">Nel caso in cui si dispone di una versione precedente del progetto, in questa sezione viene avviato per spiegare in che modo tooupdate hello Swashbuckle NuGet package in modo che è possibile utilizzare questo attributo.</span><span class="sxs-lookup"><span data-stu-id="7ace6-153">In case you have an earlier version in your project, this section starts by explaining how tooupdate hello Swashbuckle NuGet package so that you can use this attribute.</span></span>

1. <span data-ttu-id="7ace6-154">In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul progetto API Web e scegliere **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="7ace6-154">In **Solution Explorer**, right-click your Web API project and click **Manage NuGet Packages**.</span></span> 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/manage-nuget-packages.png)
2. <span data-ttu-id="7ace6-155">Fare clic su hello *aggiornamento* pulsante Avanti toohello *Swashbuckle* pacchetto NuGet.</span><span class="sxs-lookup"><span data-stu-id="7ace6-155">Click hello *Update* button next toohello *Swashbuckle* NuGet package.</span></span> 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/update-nuget-dialog.png)
3. <span data-ttu-id="7ace6-156">Aggiungere hello *SwaggerResponse* attributi toohello i metodi di azione di API Web per cui si desidera toospecify codici di risposta HTTP validi.</span><span class="sxs-lookup"><span data-stu-id="7ace6-156">Add hello *SwaggerResponse* attributes toohello Web API action methods for which you want toospecify valid HTTP response codes.</span></span> 
   
        [SwaggerResponse(HttpStatusCode.OK)]
        [SwaggerResponse(HttpStatusCode.NotFound)]
        [ResponseType(typeof(Contact))]
        public HttpResponseMessage Get(int id)
        {
            var contacts = GetContacts();
   
            var requestedContact = contacts.FirstOrDefault(x => x.Id == id);
            if (requestedContact == null)
            {
                return Request.CreateResponse(HttpStatusCode.NotFound);
            }
            else
            {
                return Request.CreateResponse<Contact>(HttpStatusCode.OK, requestedContact);
            }
        }
4. <span data-ttu-id="7ace6-157">Aggiungere un `using` istruzione per spazio dei nomi dell'attributo hello:</span><span class="sxs-lookup"><span data-stu-id="7ace6-157">Add a `using` statement for hello attribute's namespace:</span></span>
   
        using Swashbuckle.Swagger.Annotations;
5. <span data-ttu-id="7ace6-158">Sfoglia toohello */swagger/docs/v1* URL del progetto e saranno visibili in vari codici di risposta HTTP hello hello Swagger JSON.</span><span class="sxs-lookup"><span data-stu-id="7ace6-158">Browse toohello */swagger/docs/v1* URL of your project and hello various HTTP response codes will be visible in hello Swagger JSON.</span></span> 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/multiple-responses-post-attributes.png)

<span data-ttu-id="7ace6-159">codice Hello per questa dimostrazione è reperibile [questo repository GitHub](https://github.com/Azure-Samples/API-Apps-DotNet-Swashbuckle-Customization-MultipleResponseCodes-With-Attributes).</span><span class="sxs-lookup"><span data-stu-id="7ace6-159">hello code for this demonstration can be found in [this GitHub repository](https://github.com/Azure-Samples/API-Apps-DotNet-Swashbuckle-Customization-MultipleResponseCodes-With-Attributes).</span></span> <span data-ttu-id="7ace6-160">Insieme a hello progetto API Web decorata con hello *SwaggerResponse* attributo è un progetto di applicazione Console che contiene un client generato per questa API.</span><span class="sxs-lookup"><span data-stu-id="7ace6-160">Along with hello Web API project decorated with hello *SwaggerResponse* attribute is a Console Application project that contains a generated client for this API.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="7ace6-161">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7ace6-161">Next steps</span></span>
<span data-ttu-id="7ace6-162">In questo articolo ha illustrato come modo hello toocustomize Swashbuckle Genera ID operazione e codici di risposta valido.</span><span class="sxs-lookup"><span data-stu-id="7ace6-162">This article has shown how toocustomize hello way Swashbuckle generates operation ids and valid response codes.</span></span> <span data-ttu-id="7ace6-163">Per altre informazioni, vedere [Swashbuckle su GitHub](https://github.com/domaindrivendev/Swashbuckle).</span><span class="sxs-lookup"><span data-stu-id="7ace6-163">For more information, see [Swashbuckle on GitHub](https://github.com/domaindrivendev/Swashbuckle).</span></span>

