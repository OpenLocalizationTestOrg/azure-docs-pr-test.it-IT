---
title: i trigger di app API del servizio aaaApp | Documenti Microsoft
description: Come tooimplement attivi in un'applicazione API in Azure App Service
services: logic-apps
documentationcenter: .net
author: guangyang
manager: erikre
editor: jimbe
ms.assetid: 493c3703-786d-4434-9dca-8f77744b2f5d
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 08/25/2016
ms.author: rachelap
ms.openlocfilehash: 2d6b6a942a23c0a93987e9c48b69ecc739bfd814
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-api-app-triggers"></a>Trigger delle app per le API del servizio app di Azure
> [!NOTE]
> Questa versione di hello articolo applica versione dello schema di tooAPI App 2014-12-01-preview.
>
>

## <a name="overview"></a>Panoramica
Questo articolo spiega come app tooimplement API attiva e utilizzarli da un'app di logica.

Tutti i frammenti di codice hello in questo argomento vengono copiati dal hello [nell'esempio di codice App per le API FileWatcher](http://go.microsoft.com/fwlink/?LinkId=534802).

Si noti che è necessario hello toodownload seguendo il pacchetto nuget per il codice hello in questo articolo di toobuild ed eseguire: [http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/](http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/).

## <a name="what-are-api-app-triggers"></a>Cosa sono i trigger delle app per le API?
È uno scenario comune per un toofire app API un evento in modo che i client di app per le API hello possono intraprendere l'azione appropriata hello nell'evento toohello di risposta. Hello meccanismo API REST in base che supporta questo scenario viene chiamato un trigger di app di API.

Ad esempio, supponiamo che il codice client utilizza hello [Twitter API connettore app](../connectors/connectors-create-api-twitter.md) e il codice deve tooperform un'azione in base alle nuove TWEET contenenti parole specifiche. In questo caso, è possibile impostare un toofacilitate trigger polling o di push questa esigenza.

## <a name="poll-trigger-versus-push-trigger"></a>Trigger di polling e trigger di push
Attualmente sono supportati due tipi di trigger:

* Trigger di polling - Client esegue il polling app hello per le API per la notifica di un evento che è stata attivata
* Trigger di push - Client riceve una notifica tramite app hello API quando viene generato un evento

### <a name="poll-trigger"></a>Trigger di polling
Un trigger di polling viene implementato come un'API REST regolari e prevede toopoll relativo client (ad esempio un'app di logica) nella notifica tooget ordine. Mentre il client hello può mantenere lo stato, i trigger di polling hello stesso è senza stato.

le seguenti informazioni riguardanti i pacchetti di richiesta e risposta hello Hello vengono illustrati alcuni aspetti chiave del contratto di hello polling trigger:

* Richiesta
  * Metodo HTTP: GET
  * parameters
    * Questo parametro facoltativo di triggerState - consente ai client toospecify il proprio stato in modo che i trigger di polling di hello correttamente è possibile decidere se tooreturn notifica o hello non in base a stato specificato.
    * Parametri specifici dell'API
* Response
  * Codice di stato **200** - richiesta è valida e vi è una notifica da trigger hello. il contenuto di Hello della notifica hello sarà corpo della risposta hello. Un'intestazione "Retry-After" in risposta hello indica che è necessario recuperare i dati di notifica aggiuntivo con una chiamata di richiesta successiva.
  * Codice di stato **202** : richiesta è valida, ma non è presente alcuna notifica nuovo da un trigger di hello.
  * Codice di stato **4xx** : la richiesta non è valida. client Hello non deve ripetere la richiesta hello.
  * Codice di stato **5xx** : durante la richiesta si è verificato un errore interno del server e/o un problema temporaneo. Hello client deve tentare nuovamente hello richieste.

Hello frammento di codice seguente è riportato un esempio di come un sondaggio tooimplement trigger.

    // Implement a poll trigger.
    [HttpGet]
    [Route("api/files/poll/TouchedFiles")]
    public HttpResponseMessage TouchedFilesPollTrigger(
        // triggerState is a UTC timestamp
        string triggerState,
        // Additional parameters
        string searchPattern = "*")
    {
        // Check toosee whether there is any file touched after hello timestamp.
        var lastTriggerTimeUtc = DateTime.Parse(triggerState).ToUniversalTime();
        var touchedFiles = Directory.EnumerateFiles(rootPath, searchPattern, SearchOption.AllDirectories)
            .Select(f => FileInfoWrapper.FromFileInfo(new FileInfo(f)))
            .Where(fi => fi.LastAccessTimeUtc > lastTriggerTimeUtc);

        // If there are files touched after hello timestamp, return their information.
        if (touchedFiles != null && touchedFiles.Count() != 0)
        {
            // Extension method provided by hello AppService service SDK.
            return this.Request.EventTriggered(new { files = touchedFiles });
        }
        // If there are no files touched after hello timestamp, tell hello caller toopoll again after 1 mintue.
        else
        {
            // Extension method provided by hello AppService service SDK.
            return this.Request.EventWaitPoll(new TimeSpan(0, 1, 0));
        }
    }

attivare il polling di tootest, seguire questi passaggi:

1. Distribuire hello API App con un'impostazione di autenticazione di **pubblico anonimo**.
2. Chiamare hello **tocco** tootouch operazione un file. Hello seguente immagine mostra una richiesta di esempio tramite Postman.
   ![Chiamata dell'operazione Touch tramite Postman](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)
3. Chiamata hello polling trigger con hello **triggerState** parametro impostato tooa ora timbro precedente tooStep #2. Hello immagine seguente mostra la richiesta di esempio hello tramite Postman.
   ![Chiamata del trigger di polling tramite Postman](./media/app-service-api-dotnet-triggers/callpolltriggerfrompostman.PNG)

### <a name="push-trigger"></a>Trigger di push
Un trigger di push viene implementato come un'API REST regolari che effettua il push delle notifiche tooclients che hanno registrato toobe una notifica quando vengono generati eventi specifici.

le seguenti informazioni riguardanti i pacchetti di richiesta e risposta hello Hello vengono illustrati alcuni aspetti chiave del contratto di trigger push hello.

* Richiesta
  * Metodo HTTP: PUT
  * parameters
    * triggerId: obbligatorio - opaco stringa (ad esempio un GUID) che rappresenta hello registrazione di un trigger di push.
    * callbackUrl: obbligatorio - URL di hello callback tooinvoke quando viene generato l'evento hello. chiamata di Hello è una semplice chiamata HTTP POST.
    * Parametri specifici dell'API
* Response
  * Codice di stato **200** -client tooregister richiesta ha esito positivo.
  * Codice di stato **4xx** : la richiesta non è valida. client Hello non deve ripetere la richiesta hello.
  * Codice di stato **5xx** : durante la richiesta si è verificato un errore interno del server e/o un problema temporaneo. Hello client deve tentare nuovamente hello richieste.
* Callback
  * Metodo HTTP: POST
  * Corpo della richiesta: contenuto della notifica.

Hello seguente frammento di codice è riportato un esempio di come un push tooimplement trigger:

    // Implement a push trigger.
    [HttpPut]
    [Route("api/files/push/TouchedFiles/{triggerId}")]
    public HttpResponseMessage TouchedFilesPushTrigger(
        // triggerId is an opaque string.
        string triggerId,
        // A helper class provided by hello AppService service SDK.
        // Here it defines hello input of hello push trigger is a string and hello output toohello callback is a FileInfoWrapper object.
        [FromBody]TriggerInput<string, FileInfoWrapper> triggerInput)
    {
        // Register hello trigger toosome trigger store.
        triggerStore.RegisterTrigger(triggerId, rootPath, triggerInput);

        // Extension method provided by hello AppService service SDK indicating hello registration is completed.
        return this.Request.PushTriggerRegistered(triggerInput.GetCallback());
    }

    // A simple in-memory trigger store.
    public class InMemoryTriggerStore
    {
        private static InMemoryTriggerStore instance;

        private IDictionary<string, FileSystemWatcher> _store;

        private InMemoryTriggerStore()
        {
            _store = new Dictionary<string, FileSystemWatcher>();
        }

        public static InMemoryTriggerStore Instance
        {
            get
            {
                if (instance == null)
                {
                    instance = new InMemoryTriggerStore();
                }
                return instance;
            }
        }

        // Register a push trigger.
        public void RegisterTrigger(string triggerId, string rootPath,
            TriggerInput<string, FileInfoWrapper> triggerInput)
        {
            // Use FileSystemWatcher toolisten toofile change event.
            var filter = string.IsNullOrEmpty(triggerInput.inputs) ? "*" : triggerInput.inputs;
            var watcher = new FileSystemWatcher(rootPath, filter);
            watcher.IncludeSubdirectories = true;
            watcher.EnableRaisingEvents = true;
            watcher.NotifyFilter = NotifyFilters.LastAccess;

            // When some file is changed, fire hello push trigger.
            watcher.Changed +=
                (sender, e) => watcher_Changed(sender, e,
                    Runtime.FromAppSettings(),
                    triggerInput.GetCallback());

            // Assoicate hello FileSystemWatcher object with hello triggerId.
            _store[triggerId] = watcher;

        }

        // Fire hello assoicated push trigger when some file is changed.
        void watcher_Changed(object sender, FileSystemEventArgs e,
            // AppService runtime object needed tooinvoke hello callback.
            Runtime runtime,
            // hello callback tooinvoke.
            ClientTriggerCallback<FileInfoWrapper> callback)
        {
            // Helper method provided by AppService service SDK tooinvoke a push trigger callback.
            callback.InvokeAsync(runtime, FileInfoWrapper.FromFileInfo(new FileInfo(e.FullPath)));
        }
    }

attivare il polling di tootest, seguire questi passaggi:

1. Distribuire hello API App con un'impostazione di autenticazione di **pubblico anonimo**.
2. Sfoglia troppo[http://requestb.in/](http://requestb.in/) toocreate un RequestBin che verrà utilizzata come l'URL callback.
3. Chiamare il trigger di push hello con un GUID come **triggerId** e hello RequestBin URL come **callbackUrl**.
   ![Chiamata del trigger di push tramite Postman](./media/app-service-api-dotnet-triggers/callpushtriggerfrompostman.PNG)
4. Chiamare hello **tocco** tootouch operazione un file. Hello seguente immagine mostra una richiesta di esempio tramite Postman.
   ![Chiamata dell'operazione Touch tramite Postman](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)
5. Controllo hello RequestBin tooconfirm che hello push trigger callback viene richiamato con l'output di proprietà.
   ![Chiamare il trigger di polling tramite Postman](./media/app-service-api-dotnet-triggers/pushtriggercallbackinrequestbin.PNG)

### <a name="describe-triggers-in-api-definition"></a>Descrivere i trigger nella definizione dell'API
Dopo l'implementazione di trigger hello e distribuendo il tooAzure app API, passare toohello **di definizione dell'API** pannello nel portale di anteprima di Azure hello e si noterà che i trigger vengono riconosciuti automaticamente nell'interfaccia utente, che si basa sulle hello Hello definizione Swagger 2.0 API dell'applicazione hello API.

![Pannello Definizione API](./media/app-service-api-dotnet-triggers/apidefinitionblade.PNG)

Se si fa clic hello **scaricare Swagger** pulsante e i file JSON hello aperto, si noterà toohello simile di risultati seguente:

    "/api/files/poll/TouchedFiles": {
      "get": {
        "operationId": "Files_TouchedFilesPollTrigger",
        ...
        "x-ms-scheduler-trigger": "poll"
      }
    },
    "/api/files/push/TouchedFiles/{triggerId}": {
      "put": {
        "operationId": "Files_TouchedFilesPushTrigger",
        ...
        "x-ms-scheduler-trigger": "push"
      }
    }

proprietà di estensione Hello **x-ms-schedular-trigger** è come i trigger sono descritti nella definizione dell'API e viene aggiunta automaticamente dal gateway app hello API quando si richiede la definizione hello API tramite il gateway hello se hello richiesta tooone di Hello seguenti criteri. È anche possibile aggiungere questa proprietà manualmente.

* Trigger di polling
  * Se il metodo HTTP hello **ottenere**.
  * Se hello **operationId** proprietà contiene la stringa hello **trigger**.
  * Se hello **parametri** proprietà include un parametro con un **nome** impostata troppo**triggerState**.
* Trigger di push
  * Se il metodo HTTP hello **inserire**.
  * Se hello **operationId** proprietà contiene la stringa hello **trigger**.
  * Se hello **parametri** proprietà include un parametro con un **nome** impostata troppo**triggerId**.

## <a name="use-api-app-triggers-in-logic-apps"></a>Usare i trigger di app per le API nelle app per la logica
### <a name="list-and-configure-api-app-triggers-in-hello-logic-apps-designer"></a>Elencare e configurare i trigger di app API nella finestra di progettazione di hello logica App
Se si crea un'app per la logica in hello app per le API di hello stesso gruppo di risorse, sarà in grado di tooadd è canvas di progettazione toohello semplicemente facendovi clic sopra. Hello seguenti immagini illustrare questo concetto:

![Trigger nella finestra di progettazione di app per la logica](./media/app-service-api-dotnet-triggers/triggersinlogicappdesigner.PNG)

![Configurazione del trigger di polling nella finestra di progettazione di app per la logica](./media/app-service-api-dotnet-triggers/configurepolltriggerinlogicappdesigner.PNG)

![Configurazione del trigger di push nella finestra di progettazione di app per la logica](./media/app-service-api-dotnet-triggers/configurepushtriggerinlogicappdesigner.PNG)

## <a name="optimize-api-app-triggers-for-logic-apps"></a>Ottimizzare i trigger di app per le API per le app per la logica
Dopo aver aggiunto i trigger tooan API app, esistono alcuni aspetti, è possibile eseguire analisi hello tooimprove quando si utilizza l'applicazione hello API in un'app di logica.

Ad esempio, hello **triggerState** parametro per i trigger di polling deve essere impostato toohello espressione hello logica App seguente. Questa espressione deve valutare l'ultima chiamata di hello del trigger hello dall'app logica hello e restituiscono tale valore.  

    @coalesce(triggers()?.outputs?.body?['triggerState'], '')

Nota: Per una spiegazione delle funzioni hello utilizzate nell'espressione hello precedente, vedere la documentazione di toohello su [linguaggio di definizione del flusso di lavoro logica App](https://msdn.microsoft.com/library/azure/dn948512.aspx).

Logica app utenti devono espressione hello tooprovide sopra per hello **triggerState** parametro durante l'utilizzo di trigger hello. È possibile toohave questo valore predefinito dalla finestra di progettazione di hello logica app tramite proprietà di estensione hello **raccomandazione x-ms-utilità di pianificazione**.  Hello **x-ms-visibilità** estensione può essere impostata tooa valore *interno* in modo che il parametro hello stesso non viene visualizzato nella finestra di progettazione hello.  Hello frammento di codice seguente è illustrata il.

    "/api/Messages/poll": {
      "get": {
        "operationId": "Messages_NewMessageTrigger",
        "parameters": [
          {
            "name": "triggerState",
            "in": "query",
            "required": true,
            "x-ms-visibility": "internal",
            "x-ms-scheduler-recommendation": "@coalesce(triggers()?.outputs?.body?['triggerState'], '')",
            "type": "string"
          }
        ]
        ...
        "x-ms-scheduler-trigger": "poll"
      }
    }

Per i trigger di push, hello **triggerId** parametro deve identificare in modo univoco hello logica app. Una procedura consigliata è tooset questo nome della proprietà toohello del flusso di lavoro hello utilizzando hello l'espressione seguente:

    @workflow().name

Utilizzando hello **raccomandazione x-ms-utilità di pianificazione** e **x-ms-visibilità** possono trasmettere le proprietà di estensione nella relativa definizione API, hello app per le API toohello logica app progettazione tooautomatically impostare espressione per l'utente hello.

        "parameters":[  
          {  
            "name":"triggerId",
            "in":"path",
            "required":true,
            "x-ms-visibility":"internal",
            "x-ms-scheduler-recommendation":"@workflow().name",
            "type":"string"
          },


### <a name="add-extension-properties-in-api-defintion"></a>Aggiungere le proprietà di estensione nella definizione dell'API
Informazioni aggiuntive sui metadati, ad esempio le proprietà di estensione hello **raccomandazione x-ms-utilità di pianificazione** e **x-ms-visibilità** -possono essere aggiunti nella definizione di hello API in uno dei due modi: statico o dinamico.

Per i metadati statici, è possibile modificare direttamente hello */metadata/apiDefinition.swagger.json* file nel progetto e aggiungere manualmente le proprietà di hello.

Per App per le API tramite i metadati dinamici, è possibile modificare hello SwaggerConfig.cs file tooadd un filtro di operazione che è possibile aggiungere queste estensioni.

    GlobalConfiguration.Configuration
        .EnableSwagger(c =>
            {
                ...
                c.OperationFilter<TriggerStateFilter>();
                ...
            }


Hello Ecco un esempio di come questa classe è possibile scenario di metadati dinamici hello toofacilitate implementato.

    // Add extension properties on hello triggerState parameter
    public class TriggerStateFilter : IOperationFilter
    {

        public void Apply(Operation operation, SchemaRegistry schemaRegistry, System.Web.Http.Description.ApiDescription apiDescription)
        {
            if (operation.operationId.IndexOf("Trigger", StringComparison.InvariantCultureIgnoreCase) >= 0)
            {
                // this is a possible trigger
                var triggerStateParam = operation.parameters.FirstOrDefault(x => x.name.Equals("triggerState"));
                if (triggerStateParam != null)
                {
                    if (triggerStateParam.vendorExtensions == null)
                    {
                        triggerStateParam.vendorExtensions = new Dictionary<string, object>();
                    }

                    // add 2 vendor extensions
                    // x-ms-visibility: set too'internal' toosignify this is an internal field
                    // x-ms-scheduler-recommendation: set tooa value that logic app can use
                    triggerStateParam.vendorExtensions.Add("x-ms-visibility", "internal");
                    triggerStateParam.vendorExtensions.Add("x-ms-scheduler-recommendation",
                                                           "@coalesce(triggers()?.outputs?.body?['triggerState'], '')");
                }
            }
        }
    }
