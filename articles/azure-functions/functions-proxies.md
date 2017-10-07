---
title: aaaWork di proxy nelle funzioni di Azure | Documenti Microsoft
description: Panoramica di come toouse proxy funzioni di Azure
services: functions
documentationcenter: 
author: mattchenderson
manager: erikre
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 04/11/2017
ms.author: mahender
ms.openlocfilehash: 4d94c89e8f8f2d2c771b01bae142bf9a4f3b7f2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="work-with-azure-functions-proxies-preview"></a>Usare i proxy di Funzioni di Azure (anteprima)

> [!NOTE] 
> I prozy di Funzioni di Azure sono attualmente in anteprima. È disponibile mentre è in anteprima, ma le funzioni standard fatturazione valido tooproxy esecuzioni. Per altre informazioni, vedere [Prezzi di Funzioni](https://azure.microsoft.com/pricing/details/functions/).

Questo articolo viene illustrato come tooconfigure e come utilizzare il proxy di funzioni di Azure. Questa funzionalità consente di specificare gli endpoint nell'app per le funzioni implementati da un'altra risorsa. È possibile usare questi proxy toobreak un'API di grandi dimensioni, in più applicazioni di funzione (ad esempio un'architettura microservizio), pur continuando a presentare una singola superficie dell'API per i client.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]


## <a name="enable"></a>Abilitare i proxy di Funzioni di Azure

I proxy non sono abilitati per impostazione predefinita. È possibile creare proxy mentre hello funzionalità è disabilitata, ma non verranno eseguite. proxy tooenable, hello seguenti:

1. Aprire hello [portale di Azure], quindi andare tooyour funzione app.
2. Selezionare **Impostazioni dell'app per le funzioni**.
3. Opzione **abilitare i proxy di funzioni di Azure (anteprima)** troppo**su**.

È inoltre possibile restituire qui tooupdate hello proxy runtime come diventare disponibili delle nuove funzionalità.


## <a name="create"></a>Creare un proxy

In questa sezione viene illustrato come toocreate un proxy in hello portale funzioni.

1. Aprire hello [portale di Azure], quindi andare tooyour funzione app.
2. Nel riquadro sinistro hello selezionare **nuovo proxy**.
3. Dare un nome al proxy.
4. Configurare l'endpoint di hello che viene esposto in questa app di funzione specificando hello **modello di route** e **metodi HTTP**. Questi parametri si comportano in base regole toohello per [trigger HTTP].
5. Set hello **URL back-end** tooanother endpoint. Questo endpoint potrebbe essere una funzione in un'altra app per le funzioni oppure di qualsiasi altra API. Hello valore non è necessario toobe statica e può fare riferimento [le impostazioni dell'applicazione] e [i parametri dalla richiesta client originale hello].
6. Fare clic su **Crea**.

Il proxy è ora presente come un nuovo endpoint sull'app per le funzioni. Dalla prospettiva del client, è equivalente tooan HttpTrigger nelle funzioni di Azure. È possibile provare il nuovo proxy copiando hello URL del Proxy e di eseguire il test con il client HTTP preferito.

## <a name="modify-requests-responses"></a>Modificare richieste e risposte

Con il proxy di funzioni di Azure, è possibile modificare le risposte tooand richieste dal back-end hello. Queste trasformazioni possono usare le variabili come definito in [Usare le variabili].

### <a name="modify-backend-request"></a>Modificare una richiesta di back-end hello

Per impostazione predefinita, la richiesta di back-end hello viene inizializzata come una copia della richiesta originale hello. Inoltre toosetting hello back-end URL, è possibile apportare metodo HTTP toohello di modifiche, le intestazioni e parametri di stringa di query. Hello valori modificati possono fare riferimento [le impostazioni dell'applicazione] e [i parametri dalla richiesta client originale hello].

Attualmente non esiste un'esperienza del portale per la modifica delle richieste al back-end. toolearn tooapply vedere questa funzionalità, proxies.json [definire un oggetto requestOverrides].

### <a name="modify-response"></a>Modificare la risposta hello

Per impostazione predefinita, risposta client hello viene inizializzato come una copia della risposta di hello back-end. È possibile rendere il codice di stato della risposta di modifiche toohello, frase del motivo, le intestazioni e corpo. Hello valori modificati possono fare riferimento [le impostazioni dell'applicazione], [i parametri dalla richiesta client originale hello], e [parametri dalla risposta back-end hello].

Attualmente non esiste un'esperienza del portale per la modifica delle risposte del back-end. toolearn tooapply vedere questa funzionalità, proxies.json [definire un oggetto responseOverrides].

## <a name="using-variables"></a>Usare le variabili

configurazione di Hello per un proxy non è necessario toobe statico. È possibile, condizione variabili toouse dalla richiesta originale hello, risposta back-end hello o le impostazioni dell'applicazione.

### <a name="request-parameters"></a>Parametri di riferimento della richiesta

È possibile utilizzare i parametri della richiesta come input proprietà URL di back-end toohello o come parte della modifica delle richieste e risposte. È possibile associare alcuni parametri di modello di route hello specificato nella configurazione del proxy base hello e ad altri utenti possono provenire dalle proprietà della richiesta in ingresso hello.

#### <a name="route-template-parameters"></a>Parametri del modello di route
I parametri vengono utilizzati nel modello di route hello sono toobe disponibili a cui fa riferimento in base al nome. i nomi di parametro Hello sono racchiusi tra parentesi graffe ({}).

Ad esempio, se un proxy ha un modello di route, ad esempio `/pets/{petId}`, hello back-end URL può includere il valore di hello di `{petId}`, come in `https://<AnotherApp>.azurewebsites.net/api/pets/{petId}`. Se il modello di route hello termina in un carattere jolly, ad esempio `/api/{*restOfPath}`, hello valore `{restOfPath}` è una rappresentazione di stringa di hello rimanenti segmenti di percorso hello richiesta in ingresso.

#### <a name="additional-request-parameters"></a>Parametri aggiuntivi della richiesta
Inoltre toohello indirizzare i parametri del modello, hello seguente i valori può essere utilizzato nei valori di configurazione:

* **{Request}** : hello metodo HTTP utilizzato nella richiesta originale hello.
* **{Request. Headers. \<HeaderName\>}**: un'intestazione che può essere letto dalla richiesta originale hello. Sostituire  *\<HeaderName\>*  con nome hello dell'intestazione di hello che si desidera tooread. Se l'intestazione hello non è incluso nella richiesta di hello, il valore di hello sarà una stringa vuota hello.
* **{QueryString. \<ParameterName\>}**: un parametro di stringa di query che può essere letti dalla richiesta originale hello. Sostituire  *\<ParameterName\>*  con nome hello del parametro hello che si desidera tooread. Se il parametro hello non è incluso nella richiesta di hello, il valore di hello sarà una stringa vuota hello.

### <a name="response-parameters"></a>Parametri di riferimento della risposta dal back-end

Parametri di risposta è utilizzabile come parte del client di hello risposta toohello di modifica. i valori di configurazione, è possibile utilizzare Hello seguenti valori:

* **{backend.response.statusCode}** : hello codice di stato HTTP restituito nella risposta di hello back-end.
* **{backend.response.statusReason}** : frase del motivo hello HTTP restituito nella risposta di hello back-end.
* **{backend.response.headers. \<HeaderName\>}**: un'intestazione che può essere letto dalla risposta di hello back-end. Sostituire  *\<HeaderName\>*  con nome hello dell'intestazione hello da tooread. Se l'intestazione hello non è incluso nella richiesta di hello, il valore di hello sarà una stringa vuota hello.

### <a name="use-appsettings"></a>Impostazioni di riferimento dell'applicazione

È anche possibile fare riferimento [le impostazioni dell'applicazione definite per app di funzione hello](https://docs.microsoft.com/azure/azure-functions/functions-how-to-use-azure-function-app-settings#develop) racchiudendo il nome dell'impostazione hello con segni di percentuale (%)).

Ad esempio, un URL di back-end di *https://%ORDER_PROCESSING_HOST%/api/orders* avrebbe "ORDER_PROCESSING_HOST %" sostituito con il valore di hello dell'impostazione ORDER_PROCESSING_HOST hello.

> [!TIP] 
> Usare le impostazioni dell'applicazione per gli host di back-end quando si dispone di più distribuzioni o ambienti di test. In questo modo, è possibile assicurarsi che si parla sempre toohello nuovo finale per tale ambiente.

## <a name="advanced-configuration"></a>Configurazione avanzata

proxy Hello configurate vengono archiviati in un file proxies.json, che si trova nella radice di hello di una directory di app di funzione. È possibile manualmente modificare questo file e distribuirlo come parte dell'applicazione quando si usa uno di hello [metodi di distribuzione](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment) che supporta le funzioni. funzionalità di Hello deve essere [abilitato](#enable) per hello toobe di file elaborati. 

> [!TIP] 
> Se non impostati uno dei metodi di distribuzione hello, è anche possibile lavorare con file proxies.json hello nel portale di hello. Passare tooyour funzione app, selezionare **funzionalità della piattaforma**, quindi selezionare **Editor di servizio App**. In questo modo, è possibile visualizzare hello file intera struttura dell'app in funzione e quindi apportare le modifiche.

Il file proxies.JSON è definito da un oggetto proxy, composto da proxy denominati e dalle relative definizioni. È facoltativamente possibile fare riferimento a uno [schema JSON](http://json.schemastore.org/proxies) per il completamento del codice se l'editor lo supporta. Un esempio di file potrebbe essere simile hello seguente:

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "proxy1": {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/{test}"
            },
            "backendUri": "https://<AnotherApp>.azurewebsites.net/api/<FunctionName>"
        }
    }
}
```

Ogni proxy ha un nome descrittivo, ad esempio *proxy1* in hello sopra riportato. oggetto di definizione proxy corrispondente Hello è definito da hello le proprietà seguenti:

* **matchCondition**: obbligatorio--un oggetto che definisce le richieste di hello che attivano l'esecuzione di hello del proxy. Contiene due proprietà condivise con i [trigger HTTP]:
    * _metodi_: una matrice di metodi HTTP hello hello proxy risponde a. Se non è specificato, il proxy di hello risponde metodi HTTP tooall nella route hello.
    * _route_: obbligatorio - definisce il modello di route hello, il controllo cui URL di richiesta del proxy risponde. A differenza dei trigger HTTP, non vi è alcun valore predefinito.
* **backendUri**: hello URL della richiesta di hello risorse back-end toowhich hello devono essere elaborate. Questo valore può fare riferimento le impostazioni dell'applicazione e i parametri di richiesta client originale hello. Se questa proprietà non è inclusa, Funzioni di Azure risponde con un HTTP 200 OK.
* **requestOverrides**: un oggetto che definisce una richiesta di trasformazioni toohello back-end. Vedere [definire un oggetto requestOverrides].
* **responseOverrides**: un oggetto che definisce le trasformazioni toohello client risposta. Vedere [definire un oggetto responseOverrides].

> [!NOTE] 
> proprietà route Hello Azure funzioni proxy non rispetta proprietà routePrefix hello di configurazione dell'host funzioni hello. Se si desidera un prefisso, ad esempio /api tooinclude, deve essere incluso nella proprietà route hello.

### <a name="requestOverrides"></a>Definire un oggetto requestOverrides

l'oggetto requestOverrides Hello definisce le modifiche apportate toohello richiesta quando viene chiamata risorse back-end hello. oggetto Hello è definito da hello le proprietà seguenti:

* **backend.Request.Method**: hello metodo HTTP utilizzato toocall hello back-end.
* **backend.Request.QueryString. \<ParameterName\>**: un parametro di stringa di query che è possibile impostare per hello chiamata toohello back-end. Sostituire  *\<ParameterName\>*  con nome hello del parametro hello che si desidera tooset. Se viene fornita una stringa vuota hello, parametro hello non è incluso nella richiesta di hello back-end.
* **backend.Request.Headers. \<HeaderName\>**: un'intestazione che può essere impostata per hello chiamata toohello back-end. Sostituire  *\<HeaderName\>*  con nome hello dell'intestazione di hello che si desidera tooset. Se si specifica una stringa vuota hello, intestazione hello non è incluso nella richiesta di hello back-end.

I valori possono fare riferimento le impostazioni dell'applicazione e i parametri di richiesta client originale hello.

Una configurazione di esempio potrebbe essere simile hello seguente:

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "proxy1": {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/{test}"
            },
            "backendUri": "https://<AnotherApp>.azurewebsites.net/api/<FunctionName>",
            "requestOverrides": {
                "backend.request.headers.Accept": "application/xml",
                "backend.request.headers.x-functions-key": "%ANOTHERAPP_API_KEY%"
            }
        }
    }
}
```

### <a name="responseOverrides"></a>Definire un oggetto responseOverrides

l'oggetto requestOverrides Hello definisce le modifiche apportate risposta toohello che ha superato i client toohello indietro. oggetto Hello è definito da hello le proprietà seguenti:

* **response.statusCode**: toobe codice di stato HTTP hello restituito toohello client.
* **response.statusReason**: hello HTTP motivo frase toobe restituito toohello client.
* **Response.Body**: rappresentazione di stringa hello di hello corpo toobe restituito toohello client.
* **Response.Headers. \<HeaderName\>**: un'intestazione che può essere impostata per il client di toohello risposta hello. Sostituire  *\<HeaderName\>*  con nome hello dell'intestazione di hello che si desidera tooset. Se si specifica una stringa vuota hello, intestazione hello non è incluso nella risposta hello.

I valori è possono fare riferimento le impostazioni dell'applicazione, i parametri dalla richiesta client originale hello e parametri dalla risposta di hello back-end.

Una configurazione di esempio potrebbe essere simile hello seguente:

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "proxy1": {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/{test}"
            },
            "responseOverrides": {
                "response.body": "Hello, {test}",
                "response.headers.Content-Type": "text/plain"
            }
        }
    }
}
```
> [!NOTE] 
> In questo esempio, il corpo di hello viene impostato direttamente, pertanto non `backendUri` proprietà necessaria. esempio Hello viene illustrato come è possibile utilizzare il proxy di funzioni di Azure per tali API.

[portale di Azure]: https://portal.azure.com
[trigger HTTP]: https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#http-trigger
[Modify hello back-end request]: #modify-backend-request
[Modify hello response]: #modify-response
[definire un oggetto requestOverrides]: #requestOverrides
[definire un oggetto responseOverrides]: #responseOverrides
[le impostazioni dell'applicazione]: #use-appsettings
[Usare le variabili]: #using-variables
[i parametri dalla richiesta client originale hello]: #request-parameters
[parametri dalla risposta back-end hello]: #response-parameters
