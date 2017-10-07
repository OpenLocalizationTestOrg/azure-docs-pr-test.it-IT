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
# <a name="customize-swashbuckle-generated-api-definitions"></a>Personalizzare le definizioni delle API generate da Swashbuckle
## <a name="overview"></a>Panoramica
Questo articolo viene illustrato come toocustomize Swashbuckle toohandle scenari comuni in cui può essere tooalter hello comportamento predefinito:

* Swashbuckle genera identificatori di operazione duplicati per gli overload dei metodi del controller
* Swashbuckle si presuppone che hello solo risposta valida da un metodo HTTP 200 (OK) 

## <a name="customize-operation-identifier-generation"></a>Personalizzare la generazione di identificatori di operazione
Swashbuckle genera identificatori di operazione Swagger concatenando il nome del controller e il nome del metodo. Questo modello provoca problemi quando sono presenti più overload di un metodo: Swashbuckle genera ID operazione duplicati, ovvero JSON Swagger non valido.

Ad esempio hello seguente di codice del controller, Swashbuckle toogenerate tre ID operazione di Contact_Get.

![](./media/app-service-api-dotnet-swashbuckle-customize/multiplegetsincode.png)

![](./media/app-service-api-dotnet-swashbuckle-customize/multiplegetsinjson.png)

È possibile risolvere il problema di hello manualmente, assegnando a metodi hello nomi univoci, come illustrato di seguito hello per questo esempio:

* Get
* GetById
* GetPage

In alternativa Hello è tooextend Swashbuckle toomake genera automaticamente l'ID operazione univoco.

Hello passaggi seguenti viene illustrato come toocustomize Swashbuckle utilizzando hello *SwaggerConfig.cs* file incluso nel progetto hello dal modello di progetto di Visual Studio API App Preview hello.  È anche possibile personalizzare Swashbuckle in un progetto API Web configurato per la distribuzione come app per le API.

1. Creare un'implementazione personalizzata di `IOperationFilter` 
   
    Hello `IOperationFilter` interfaccia fornisce un punto di estensibilità per Swashbuckle gli utenti toocustomize vari aspetti del processo di metadati Swagger hello. Hello codice riportato di seguito viene illustrato un metodo di modifica di comportamento di hello la generazione di id dell'operazione. codice Hello Accoda nome id operazione toohello i nomi del parametro.  
   
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
2. In *App_Start\SwaggerConfig.cs* file, la chiamata hello `OperationFilter` nuovo hello toouse Swashbuckle toocause metodo `IOperationFilter` implementazione.
   
        c.OperationFilter<MultipleOperationsWithSameVerbFilter>();
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/usefilter.png)
   
    Hello *SwaggerConfig.cs* file che viene rimosso dal pacchetto Swashbuckle NuGet hello contiene molti esempi di commento di punti di estendibilità. commenti aggiuntivi Hello non vengono visualizzati qui. 
   
    Dopo aver apportato questa modifica, il `IOperationFilter` implementazione viene usata determinando il toobe ID operazione univoco generato.
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/uniqueids.png)

<a id="multiple-response-codes" name="multiple-response-codes"></a>

## <a name="allow-response-codes-other-than-200"></a>Consentire codici di risposta diversi da 200
Per impostazione predefinita, Swashbuckle si presuppone che una risposta HTTP 200 (OK) hello *solo* legittimo risposta da un metodo API Web. In alcuni casi, è consigliabile tooreturn altri codici di risposta senza causare hello client tooraise un'eccezione.  Ad esempio, hello API Web codice seguente viene illustrato uno scenario in cui è preferibile hello client tooaccept 200 o 404 come le risposte valide.

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

In questo scenario, hello Swagger che Swashbuckle genera per impostazione predefinita specifica solo un legittimo HTTP codice di stato HTTP 200.

![](./media/app-service-api-dotnet-swashbuckle-customize/http-200-output-only.png)

Poiché Visual Studio utilizza hello codice toogenerate di definizione Swagger API per client hello, viene creato il codice client che genera un'eccezione per le risposte diverso da HTTP 200. codice Hello seguente proviene da un client c# generato per questo metodo API Web di esempio.

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

Swashbuckle fornisce due modalità di personalizzazione di hello elenco dei codici di risposta HTTP previsto da esso generato, usando i commenti XML o hello `SwaggerResponse` attributo. attributo Hello è più semplice, ma è disponibile solo in Swashbuckle 5.1.5 o versioni successive. App per le API anteprima nuovo progetto modello in Visual Studio 2013 Hello include Swashbuckle versione 5.0.0, pertanto se si utilizza il modello di hello e non desidera tooupdate Swashbuckle, l'unica possibilità è toouse XML (commenti). 

### <a name="customize-expected-response-codes-using-xml-comments"></a>Personalizzare i codici di risposta previsti con i commenti XML
Utilizzare i codici di risposta toospecify questo metodo se la versione Swashbuckle è precedente a 5.1.5.

1. Aggiungere innanzitutto i commenti della documentazione XML tramite metodi hello desiderato toospecify codici di risposta HTTP per. Eseguire l'azione di API Web di esempio hello tooit di documentazione XML illustrato in precedenza e l'applicazione hello darà origine a codice simile al seguente esempio hello. 
   
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
2. Aggiungere le istruzioni in hello *SwaggerConfig.cs* toodirect Swashbuckle toomake utilizzo di file di documentazione XML hello del file.
   
   * Aprire *SwaggerConfig.cs* e creare un metodo su hello *SwaggerConfig* classe toospecify hello percorso toohello file XML della documentazione. 
     
           private static string GetXmlCommentsPath()
           {
               return string.Format(@"{0}\XmlComments.xml", 
                   System.AppDomain.CurrentDomain.BaseDirectory);
           }
   * Scorrere verso il basso hello *SwaggerConfig.cs* file finché non viene visualizzata una riga di commento hello di codice simile hello schermata. 
     
       ![](./media/app-service-api-dotnet-swashbuckle-customize/xml-comments-commented-out.png)
   * Rimuovere il commento hello riga tooenable hello XML elaborazione dei commenti durante la generazione di Swagger. 
     
       ![](./media/app-service-api-dotnet-swashbuckle-customize/xml-comments-uncommented.png)
3. Nel file di documentazione XML hello toogenerate ordine, passare la proprietà del progetto hello e abilitare i file di documentazione XML hello come illustrato nella schermata di hello riportata di seguito. 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/enable-xml-documentation-file.png) 

Dopo aver eseguito questi passaggi, hello Swagger JSON generato da Swashbuckle rifletterà i codici di risposta HTTP hello specificato nei commenti XML hello. schermata di Hello riportata di seguito viene illustrato questo nuovo payload JSON. 

![](./media/app-service-api-dotnet-swashbuckle-customize/swagger-multiple-responses.png)

Quando si utilizza codice di Visual Studio tooregenerate hello del client per l'API REST, il codice c# di hello accetta i codici di stato HTTP di OK e non trovato entrambi hello senza generare un'eccezione, che consente le decisioni di toomake dispendiosa in termini di codice in modalità toohandle hello restituiscono un valore null Record del contatto. 

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

codice Hello per questa dimostrazione è reperibile [questo repository GitHub](https://github.com/Azure-Samples/app-service-api-dotnet-swashbuckle-swaggerresponse). Insieme a Web API hello progetto contrassegnato con commenti della documentazione XML è un progetto di applicazione Console che contiene un client generato per questa API. 

### <a name="customize-expected-response-codes-using-hello-swaggerresponse-attribute"></a>Personalizzare i codici di risposta previsto utilizzando l'attributo SwaggerResponse hello
Hello [SwaggerResponse](https://github.com/domaindrivendev/Swashbuckle/blob/master/Swashbuckle.Core/Swagger/Annotations/SwaggerResponseAttribute.cs) attributo è disponibile in Swashbuckle 5.1.5 e versioni successive. Nel caso in cui si dispone di una versione precedente del progetto, in questa sezione viene avviato per spiegare in che modo tooupdate hello Swashbuckle NuGet package in modo che è possibile utilizzare questo attributo.

1. In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul progetto API Web e scegliere **Gestisci pacchetti NuGet**. 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/manage-nuget-packages.png)
2. Fare clic su hello *aggiornamento* pulsante Avanti toohello *Swashbuckle* pacchetto NuGet. 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/update-nuget-dialog.png)
3. Aggiungere hello *SwaggerResponse* attributi toohello i metodi di azione di API Web per cui si desidera toospecify codici di risposta HTTP validi. 
   
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
4. Aggiungere un `using` istruzione per spazio dei nomi dell'attributo hello:
   
        using Swashbuckle.Swagger.Annotations;
5. Sfoglia toohello */swagger/docs/v1* URL del progetto e saranno visibili in vari codici di risposta HTTP hello hello Swagger JSON. 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/multiple-responses-post-attributes.png)

codice Hello per questa dimostrazione è reperibile [questo repository GitHub](https://github.com/Azure-Samples/API-Apps-DotNet-Swashbuckle-Customization-MultipleResponseCodes-With-Attributes). Insieme a hello progetto API Web decorata con hello *SwaggerResponse* attributo è un progetto di applicazione Console che contiene un client generato per questa API. 

## <a name="next-steps"></a>Passaggi successivi
In questo articolo ha illustrato come modo hello toocustomize Swashbuckle Genera ID operazione e codici di risposta valido. Per altre informazioni, vedere [Swashbuckle su GitHub](https://github.com/domaindrivendev/Swashbuckle).

