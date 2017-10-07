---
title: criteri di trasformazione di gestione API aaaAzure | Documenti Microsoft
description: Informazioni sui criteri di trasformazione hello disponibili per l'utilizzo in Gestione API di Azure.
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 7406a8ce-5f9c-4fae-9b0f-e574befb2ee9
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 2891cc52d0017b717b3c12a98bc4941b5fd7ea78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-transformation-policies"></a>Criteri di trasformazione di Gestione API
In questo argomento fornisce un riferimento per i seguenti criteri di gestione API hello. Per informazioni sull'aggiunta e sulla configurazione dei criteri, vedere [Criteri di Gestione API](http://go.microsoft.com/fwlink/?LinkID=398186).  
  
##  <a name="TransformationPolicies"></a> Criteri di trasformazione  
  
-   [Convertire JSON tooXML](api-management-transformation-policies.md#ConvertJSONtoXML) - richiesta converte o corpo della risposta da JSON tooXML.  
  
-   [Convertire XML tooJSON](api-management-transformation-policies.md#ConvertXMLtoJSON) - richiesta converte o corpo della risposta da XML tooJSON.  
  
-   [find-and-replace](api-management-transformation-policies.md#Findandreplacestringinbody) : trova una sottostringa di richiesta o risposta e la sostituisce con una sottostringa diversa.  
  
-   [Maschera URL nel contenuto](api-management-transformation-policies.md#MaskURLSContent) -riscrive (maschera) i collegamenti nella risposta hello corpo in modo che facciano riferimento toohello collegamento equivalente tramite il gateway hello.  
  
-   [Impostare il servizio back-end](api-management-transformation-policies.md#SetBackendService) -Modifica servizio back-end hello per una richiesta in ingresso.  
  
-   [Impostare corpo](api-management-transformation-policies.md#SetBody) -imposta corpo del messaggio hello per le richieste in ingresso e in uscita.  
  
-   [Intestazione HTTP set](api-management-transformation-policies.md#SetHTTPheader) - assegna una risposta di valore tooan esistente e/o l'intestazione della richiesta o aggiunge una nuova intestazione di risposta e/o di richiesta.  
  
-   [Imposta parametro di stringa della query](api-management-transformation-policies.md#SetQueryStringParameter) : aggiunge, sostituisce il valore di o elimina il parametro di stringa della query di richiesta.  
  
-   [Riscrittura URL](api-management-transformation-policies.md#RewriteURL) -converte un URL di richiesta dal formato pubblico toohello formato previsto dal servizio web hello.  
  
-   [Trasformare XML utilizzando XSLT](api-management-transformation-policies.md#XSLTransform) -si applica un tooXML trasformazione XSL nel corpo della richiesta o risposta hello.  
  
##  <a name="ConvertJSONtoXML"></a>Convertire JSON tooXML  
 Hello `json-to-xml` criteri converte un corpo della richiesta o risposta da JSON tooXML.  
  
### <a name="policy-statement"></a>Istruzione del criterio  
  
```xml  
<json-to-xml apply="always | content-type-json" consider-accept-header="true | false"/>  
```  
  
### <a name="example"></a>Esempio  
  
```xml  
<policies>  
    <inbound>  
        <base />  
    </inbound>  
    <outbound>  
        <base />  
        <json-to-xml apply="always" consider-accept-header="false" />  
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a>Elementi  
  
|Nome|Descrizione|Obbligatorio|  
|----------|-----------------|--------------|  
|json-to-xml|Elemento radice.|Sì|  
  
### <a name="attributes"></a>Attributi  
  
|Nome|Descrizione|Obbligatorio|Default|  
|----------|-----------------|--------------|-------------|  
|apply|attributo di Hello deve essere impostato tooone dei seguenti valori hello.<br /><br /> -   always - applica sempre la conversione.<br />-   content-type-json - applica la conversione solo se l'intestazione Content-Type della risposta indica la presenza di JSON.|Sì|N/D|  
|consider-accept-header|attributo di Hello deve essere impostato tooone dei seguenti valori hello.<br /><br /> -   true - applica la conversione se JSON è richiesto nell'intestazione Accept della richiesta.<br />-   false - applica sempre la conversione.|No|true|  
  
### <a name="usage"></a>Utilizzo  
 Questo criterio può essere utilizzato hello seguenti criteri [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sezioni del criterio:** inbound, outbound, on-error  
  
-   **Ambiti del criterio:** globale, prodotto, API, operazione  
  
##  <a name="ConvertXMLtoJSON"></a>Convertire XML tooJSON  
 Hello `xml-to-json` criteri converte un corpo della richiesta o risposta da XML tooJSON. Questo criterio può essere utilizzato toomodernize API basate su servizi web XML back-end solo.  
  
### <a name="policy-statement"></a>Istruzione del criterio  
  
```xml  
<xml-to-json kind="javascript-friendly | direct" apply="always | content-type-xml" consider-accept-header="true | false"/>  
```  
  
### <a name="example"></a>Esempio  
  
```xml  
<policies>  
    <inbound>  
        <base />  
    </inbound>  
    <outbound>  
        <base />  
        <xml-to-json kind="direct" apply="always" consider-accept-header="false" />  
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a>Elementi  
  
|Nome|Descrizione|Obbligatorio|  
|----------|-----------------|--------------|  
|xml-to-json|Elemento radice.|Sì|  
  
### <a name="attributes"></a>Attributi  
  
|Nome|Descrizione|Obbligatorio|Default|  
|----------|-----------------|--------------|-------------|  
|kind|attributo di Hello deve essere impostato tooone dei seguenti valori hello.<br /><br /> hello-javascript friendly: convertita JSON con gli sviluppatori tooJavaScript descrittivo un modulo.<br />-direct: hello JSON convertito riflette la struttura del documento di hello originale XML.|Sì|N/D|  
|apply|attributo di Hello deve essere impostato tooone dei seguenti valori hello.<br /><br /> -   always - esegue sempre la conversione.<br />-   content-type-xml - applica la conversione solo se l'intestazione Content-Type della risposta indica la presenza di XML.|Sì|N/D|  
|consider-accept-header|attributo di Hello deve essere impostato tooone dei seguenti valori hello.<br /><br /> -   true - applica la conversione se XML è richiesto nell'intestazione Accept della richiesta.<br />-   false - applica sempre la conversione.|No|true|  
  
### <a name="usage"></a>Utilizzo  
 Questo criterio può essere utilizzato hello seguenti criteri [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sezioni del criterio:** inbound, outbound, on-error  
  
-   **Ambiti del criterio:** globale, prodotto, API, operazione  
  
##  <a name="Findandreplacestringinbody"></a> Trova e sostituisci stringa nel corpo  
 Hello `find-and-replace` criteri trova una sottostringa di richiesta o risposta e lo sostituisce con una sottostringa diversa.  
  
### <a name="policy-statement"></a>Istruzione del criterio  
  
```xml  
<find-and-replace from="what tooreplace" to="replacement" />  
```  
  
### <a name="example"></a>Esempio  
  
```xml  
<find-and-replace from="notebook" to="laptop" />  
```  
  
### <a name="elements"></a>Elementi  
  
|Nome|Descrizione|Obbligatorio|  
|----------|-----------------|--------------|  
|find-and-replace|Elemento radice.|Sì|  
  
### <a name="attributes"></a>Attributi  
  
|Nome|Descrizione|Obbligatorio|Default|  
|----------|-----------------|--------------|-------------|  
|from|Hello stringa toosearch per.|Sì|N/D|  
|to|stringa di sostituzione Hello. Specificare una sostituzione stringa tooremove hello ricerca stringa di lunghezza zero.|Sì|N/D|  
  
### <a name="usage"></a>Utilizzo  
 Questo criterio può essere utilizzato hello seguenti criteri [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sezioni del criterio:** inbound, outbound, backend, on-error  
  
-   **Ambiti del criterio:** globale, prodotto, API, operazione  
  
##  <a name="MaskURLSContent"></a> Maschera URL nel contenuto  
 Hello `redirect-content-urls` criteri riscrive (maschera) i collegamenti nel corpo della risposta hello in modo che facciano riferimento toohello collegamento equivalente tramite il gateway hello. Usarli in hello sezione in uscita toore scrittura risposta corpo collegamenti toomake punto toohello gateway. Utilizzo in hello in ingresso di sezione per ottenere l'effetto opposto.  
  
> [!NOTE]
>  Questo criterio non modifica i valori delle intestazioni, ad esempio le intestazioni `Location`. i valori di intestazione toochange, utilizzare hello [set intestazione](api-management-transformation-policies.md#SetHTTPheader) criteri.  
  
### <a name="policy-statement"></a>Istruzione del criterio  
  
```xml  
<redirect-content-urls />  
```  
  
### <a name="example"></a>Esempio  
  
```xml  
<redirect-content-urls />  
```  
  
### <a name="elements"></a>Elementi  
  
|Nome|Descrizione|Obbligatorio|  
|----------|-----------------|--------------|  
|redirect-content-urls|Elemento radice.|Sì|  
  
### <a name="usage"></a>Utilizzo  
 Questo criterio può essere utilizzato hello seguenti criteri [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sezioni del criterio:** inbound, outbound  
  
-   **Ambiti del criterio:** globale, prodotto, API, operazione  
  
##  <a name="SetBackendService"></a> Imposta servizio back-end  
 Hello utilizzare `set-backend-service` tooredirect criteri un in ingresso richiesta back-end diverso di tooa rispetto a quello specificato nelle impostazioni di hello API per l'operazione hello. Questo criterio cambia hello back-end del servizio URL di base toohello richiesta in ingresso hello quello specificato nei criteri di hello.  
  
### <a name="policy-statement"></a>Istruzione del criterio  
  
```xml  
<set-backend-service base-url="base URL of hello backend service" />  
```  
  
### <a name="example"></a>Esempio  
  
```xml  
<policies>  
    <inbound>  
        <choose>  
            <when condition="@(context.Request.Url.Query.GetValueOrDefault("version") == "2013-05")">  
                <set-backend-service base-url="http://contoso.com/api/8.2/" />  
            </when>  
            <when condition="@(context.Request.Url.Query.GetValueOrDefault("version") == "2014-03")">  
                <set-backend-service base-url="http://contoso.com/api/9.1/" />  
            </when>  
        </choose>  
        <base />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
In questo hello esempio impostare i criteri del servizio back-end instrada le richieste in base al valore di versione di hello passato al servizio back-end diverso rispetto all'API hello specificato in un hello hello query stringa tooa.
  
Inizialmente hello URL di base del servizio back-end è derivato dalle impostazioni API hello. Pertanto hello URL della richiesta `https://contoso.azure-api.net/api/partners/15?version=2013-05&subscription-key=abcdef` diventa `http://contoso.com/api/10.4/partners/15?version=2013-05&subscription-key=abcdef` dove `http://contoso.com/api/10.4/` hello URL del servizio back-end specificato nelle impostazioni di hello API.  
  
Quando hello [< scegliere\> ](api-management-advanced-policies.md#choose) istruzione dei criteri viene applicato l'URL di base del servizio back-end hello può cambiare di nuovo troppo`http://contoso.com/api/8.2` o `http://contoso.com/api/9.1`, a seconda del valore di hello hello versione richiesta del parametro della query. Ad esempio, se hello è `"2013-15"` richiesta finale di hello URL diventa `http://contoso.com/api/8.2/partners/15?version=2013-05&subscription-key=abcdef`.  
  
Se un'ulteriore trasformazione della richiesta di hello è desiderato, altri [criteri di trasformazione](api-management-transformation-policies.md#TransformationPolicies) può essere utilizzato. Ad esempio, tooremove hello versione query parametro ora che hello richiesta viene indirizzato tooa versione back-end specifico, hello [impostare il parametro di stringa di query](api-management-transformation-policies.md#SetQueryStringParameter) criteri possono essere l'attributo di versione divenuto ridondante hello di tooremove utilizzati.  
  
### <a name="example"></a>Esempio  
  
```xml  
<policies>  
    <inbound>  
        <set-backend-service backend-id="my-sf-service" sf-partition-key="@(context.Request.Url.Query.GetValueOrDefault("userId","")" sf-replica-type="primary" /> 
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
In questo esempio hello criteri route hello richiesta tooa service fabric back-end, utilizzando una stringa di query userId hello come chiave di partizione hello e utilizzando hello replica primaria di partizione hello.  

### <a name="elements"></a>Elementi  
  
|Nome|Descrizione|Obbligatorio|  
|----------|-----------------|--------------|  
|set-backend-service|Elemento radice.|Sì|  
  
### <a name="attributes"></a>Attributi  
  
|Nome|Descrizione|Obbligatorio|Default|  
|----------|-----------------|--------------|-------------|  
|base-url|Nuovo URL di base del servizio back-end.|No|N/D|  
|backend-id|Identificatore di hello tooroute di back-end per.|No|N/D|  
|sf-partition-key|Questo campo è applicabile solo quando il back-end hello è un servizio di Service Fabric e viene specificata utilizzando 'id back-end'. Utilizzare una partizione specifica dal servizio di risoluzione del nome hello tooresolve.|No|N/D|  
|sf-replica-type|Questo campo è applicabile solo quando il back-end hello è un servizio di Service Fabric e viene specificata utilizzando 'id back-end'. Controlla se la richiesta hello deve diventare la replica primaria o secondaria di toohello di una partizione. |No|N/D|    
|sf-resolve-condition|Questo campo è applicabile solo quando il back-end hello è un servizio di Service Fabric. Condizione che identifica se hello chiama back-end dell'infrastruttura tooService ha toobe ripetuto con la risoluzione di nuovo.|No|N/D|    
|sf-service-instance-name|Questo campo è applicabile solo quando il back-end hello è un servizio di Service Fabric. Consente toochange le istanze del servizio in fase di esecuzione. |No|N/D |    

### <a name="usage"></a>Utilizzo  
 Questo criterio può essere utilizzato hello seguenti criteri [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sezioni del criterio:** inbound, backend  
  
-   **Ambiti del criterio:** globale, prodotto, API, operazione  
  
##  <a name="SetBody"></a> Imposta corpo  
 Hello utilizzare `set-body` corpo del messaggio hello tooset criteri per le richieste in ingresso e in uscita. tooaccess hello corpo del messaggio è possibile utilizzare hello `context.Request.Body` proprietà o hello `context.Response.Body`, a seconda se i criteri di hello sono hello sezione in ingresso o in uscita.  
  
> [!IMPORTANT]
>  Si noti che per impostazione predefinita quando si accede a hello corpo del messaggio tramite `context.Request.Body` o `context.Response.Body`, messaggio originale viene perso e deve essere impostato riportandolo corpo hello in espressione hello. toopreserve hello contenuto del corpo, impostare hello `preserveContent` parametro troppo`true` quando si accede a messaggio hello. Se `preserveContent` è troppo`true` e viene restituito un corpo diverso dall'espressione hello, hello restituito corpo viene utilizzato.  
>   
>  Si noti hello seguenti considerazioni quando si utilizza hello `set-body` criteri.  
>   
>  -   Se si utilizza hello `set-body` tooreturn criteri un corpo di nuovo o aggiornato non è necessario tooset `preserveContent` troppo`true` perché in modo esplicito di fornire contenuto del corpo del nuovo hello.  
> -   Mantenere il contenuto di hello di una risposta in pipeline in ingresso hello non ha senso perché non è ancora stata ricevuta alcuna risposta.  
> -   Mantenere il contenuto di hello di una richiesta nella pipeline in uscita hello non hanno alcun significato poiché hello richiesta è già stata inviata back-end toohello a questo punto.  
> -   Se questo criterio viene usato quando non vi è alcun corpo del messaggio, ad esempio in un'operazione GET in ingresso, viene generata un'eccezione.  
  
 Per ulteriori informazioni, vedere hello `context.Request.Body`, `context.Response.Body`, hello e `IMessage` sezioni hello [variabile di contesto](api-management-policy-expressions.md#ContextVariables) tabella.  
  
### <a name="policy-statement"></a>Istruzione del criterio  
  
```xml  
<set-body>new body value as text</set-body>  
```  
  
### <a name="examples"></a>Esempi  
  
#### <a name="literal-text-example"></a>Esempio di testo letterale  
  
```xml  
<set-body>Hello world!</set-body>  
```  
  
#### <a name="example-accessing-hello-body-as-a-string-note-that-we-are-preserving-hello-original-request-body-so-that-we-can-access-it-later-in-hello-pipeline"></a>Esempio di accesso hello corpo sotto forma di stringa. Si noti che stiamo lavorando alla conservazione corpo della richiesta originale hello in modo che è possibile accedervi in un secondo momento nella pipeline di hello.
  
```xml  
<set-body>  
@{   
    string inBody = context.Request.Body.As<string>(preserveContent: true);   
    if (inBody[0] =='c') {   
        inBody[0] = 'm';   
    }   
    return inBody;   
}  
</set-body>  
```  
  
#### <a name="example-accessing-hello-body-as-a-jobject-note-that-since-we-are-not-reserving-hello-original-request-body-accesing-it-later-in-hello-pipeline-will-result-in-an-exception"></a>Esempio di accesso hello corpo sotto forma di JObject. Si noti che, poiché si sta riservando non hello originale corpo della richiesta, in un secondo momento nella pipeline di hello causerà un'eccezione di accesso.  
  
```xml  
<set-body>   
@{   
    JObject inBody = context.Request.Body.As<JObject>();   
    if (inBody.attribute == <tag>) {   
        inBody[0] = 'm';   
    }   
    return inBody.ToString();   
}   
</set-body>  
  
```  
  
#### <a name="filter-response-based-on-product"></a>Filtrare la risposta in base al prodotto  
 Questo esempio viene illustrato come tooperform contenuto applicando un filtro per la rimozione degli elementi di dati dalla risposta hello ricevuto dal servizio back-end hello quando si utilizza hello `Starter` prodotto. Per una dimostrazione della configurazione e l'utilizzo di questo criterio, vedere [Cloud coprire episodio 177: più API le funzionalità di gestione con Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) e far avanzare rapidamente too34:30. Inizia dal 31:50 toosee Cenni preliminari [hello scuro Sky previsione API](https://developer.forecast.io/) utilizzato per questa dimostrazione.  
  
```xml  
<!-- Copy this snippet into hello outbound section tooremove a number of data elements from hello response received from hello backend service based on hello name of hello api product -->  
<choose>  
  <when condition="@(context.Response.StatusCode == 200 && context.Product.Name.Equals("Starter"))">  
    <set-body>@{  
        var response = context.Response.Body.As<JObject>();  
        foreach (var key in new [] {"minutely", "hourly", "daily", "flags"}) {  
          response.Property (key).Remove ();  
        }  
        return response.ToString();  
      }  
    </set-body>  
  </when>  
</choose>  
```  

### <a name="using-liquid-templates-with-set-body"></a>Uso di modelli Liquid con set body 
Hello `set-body` criteri possono essere configurato toouse hello [liquide](https://shopify.github.io/liquid/basics/introduction/) modelli linguaggio tootransfom hello corpo di una richiesta o risposta. Può essere molto efficace se occorre un formato di hello toocompletely nuova forma del messaggio.

> [!IMPORTANT]
> implementazione di soluzione usato in hello Hello `set-body` criterio è configurato in modalità c#. Questo è particolarmente importante quando si eseguono operazioni quali l'applicazione del filtro. Ad esempio, utilizzando un filtro data richiede l'uso di hello di Pascal maiuscole e minuscole e c# è data la formattazione, ad esempio:
>
> {{body.foo.startDateTime| Data:"yyyyMMddTHH:mm:ddZ"}}

> [!IMPORTANT]
> In ordine toocorrectly binding tooan corpo XML con modello liquide hello, utilizzare un `set-header` criteri tooset Content-Type tooeither application/xml, testo/xml (o qualsiasi tipo che termina con + xml); per un corpo JSON, deve essere application/json, testo/json (o qualsiasi finale di tipo con + json).

#### <a name="convert-json-toosoap-using-a-liquid-template"></a>Convertire tooSOAP JSON utilizzando un modello liquido
```xml
<set-body template="liquid">
    <soap:Envelope xmlns="http://tempuri.org/" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
        <soap:Body>
            <GetOpenOrders>
                <cust>{{body.getOpenOrders.cust}}</cust>
            </GetOpenOrders>
        </soap:Body>
    </soap:Envelope>
</set-body>
```

#### <a name="tranform-json-using-a-liquid-template"></a>Trasformare JSON usando un modello Liquid
```xml
{
"order": {
    "id": "{{body.customer.purchase.identifier}}",
    "summary": "{{body.customer.purchase.orderShortDesc}}"
    }
}
```

### <a name="elements"></a>Elementi  
  
|Nome|Descrizione|Obbligatorio|  
|----------|-----------------|--------------|  
|set-body|Elemento radice. Contiene testo hello o un'espressione che restituisce un corpo.|Sì|  

### <a name="properties"></a>Proprietà  
  
|Nome|Descrizione|Obbligatorio|Default|  
|----------|-----------------|--------------|-------------|  
|template|Verrà eseguito in modalità modello toochange utilizzato hello che hello corpo impostare i criteri in. Il valore di hello solo supportato attualmente è:<br /><br />hello - liquide - impostare i criteri corpo utilizzerà motore del modello liquide hello |No|liquid|  

Per l'accesso alle informazioni hello richiesta e risposta, modello liquide hello può associare l'oggetto di contesto tooa con hello le proprietà seguenti: <br />
<pre>context.
    Request.
        Url
        Method
        OriginalMethod
        OriginalUrl
        IpAddress
        MatchedParameters
        HasBody
        ClientCertificates
        Headers

    Response.
        StatusCode
        Method
        Headers
Url.
    Scheme
    Host
    Port
    Path
    Query
    QueryString
    ToUri
    ToString

OriginalUrl.
    Scheme
    Host
    Port
    Path
    Query
    QueryString
    ToUri
    ToString
</pre>



### <a name="usage"></a>Utilizzo  
 Questo criterio può essere utilizzato hello seguenti criteri [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sezioni del criterio:** inbound, outbound, back-end  
  
-   **Ambiti del criterio:** globale, prodotto, API, operazione  
  
##  <a name="SetHTTPheader"></a> Imposta intestazione HTTP  
 Hello `set-header` criteri assegna una risposta di valore tooan esistente e/o l'intestazione della richiesta oppure aggiunge una nuova intestazione di risposta e/o di richiesta.  
  
 Inserisce un elenco di intestazioni HTTP in un messaggio HTTP. Se inserito in una pipeline in ingresso, questo criterio imposta le intestazioni HTTP hello per richiesta hello passati toohello servizio di destinazione. Se inserito in una pipeline in uscita, questo criterio imposta le intestazioni HTTP hello per risposta hello inviati client toohello del gateway.  
  
### <a name="policy-statement"></a>Istruzione del criterio  
  
```xml  
<set-header name="header name" exists-action="override | skip | append | delete">  
    <value>value</value> <!--for multiple headers with hello same name add additional value elements-->  
</set-header>  
```  
  
### <a name="examples"></a>Esempi  
  
#### <a name="example"></a>Esempio  
  
```xml  
<set-header name="some header name" exists-action="override">  
    <value>20</value>   
</set-header>  
```  
  
#### <a name="forward-context-information-toohello-backend-service"></a>Inoltrare servizio back-end toohello informazioni di contesto  
 Questo esempio viene illustrato come il criterio tooapply hello API livello servizio back-end di toosupply contesto informazioni toohello. Per una dimostrazione della configurazione e l'utilizzo di questo criterio, vedere [Cloud coprire episodio 177: più API le funzionalità di gestione con Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) e far avanzare rapidamente too10:30. 12:10 è una dimostrazione di chiamata di un'operazione nel portale per sviluppatori hello in cui è possibile visualizzare i criteri di hello al lavoro.  
  
```xml  
<!-- Copy this snippet into hello inbound element tooforward some context information, user id and hello region hello gateway is hosted in, toohello backend service for logging or evaluation -->  
<set-header name="x-request-context-data" exists-action="override">  
  <value>@(context.User.Id)</value>  
  <value>@(context.Deployment.Region)</value>  
</set-header>  
```  
  
 Per altre informazioni, vedere [Espressioni di criteri](api-management-policy-expressions.md) e [Variabile di contesto](api-management-policy-expressions.md#ContextVariables).  
  
### <a name="elements"></a>Elementi  
  
|Nome|Descrizione|Obbligatorio|  
|----------|-----------------|--------------|  
|set-header|Elemento radice.|Sì|  
|value|Specifica il valore di hello di hello intestazione toobe set. Per più intestazioni con hello omonima aggiungere ulteriori `value` elementi.|Sì|  
  
### <a name="properties"></a>Proprietà  
  
|Nome|Descrizione|Obbligatorio|Default|  
|----------|-----------------|--------------|-------------|  
|exists-action|Specifica quali tootake azione quando l'intestazione hello è già specificato. Questo attributo deve avere uno dei seguenti valori hello.<br /><br /> -override - sostituisce hello valore dell'intestazione esistente hello.<br />-skip: non sostituisce il valore dell'intestazione esistente di hello.<br />-aggiungere - aggiunge hello valore toohello valore dell'intestazione esistente.<br />-delete - rimuove l'intestazione di hello dalla richiesta hello.<br /><br /> Quando impostato troppo`override` l'integrazione di più voci con hello stesso nome risultati nell'intestazione di hello viene impostato in base tooall le voci (elencate più volte); solo i valori elencati verranno impostati nel risultato hello.|No|override|  
|name|Specifica nome del set di toobe intestazione hello.|Sì|N/D|  
  
### <a name="usage"></a>Utilizzo  
 Questo criterio può essere utilizzato hello seguenti criteri [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sezioni del criterio:** inbound, outbound, backend, on-error  
  
-   **Ambiti del criterio:** globale, prodotto, API, operazione  
  
##  <a name="SetQueryStringParameter"></a> Imposta parametro di stringa della query  
 Hello `set-query-parameter` criteri aggiunge valore sostituisce, o eliminazioni richiesta il parametro di stringa di query. È possibile toopass utilizzati parametri di query previsti dal servizio back-end hello, che sono facoltativi o mai presentano nella richiesta di hello.  
  
### <a name="policy-statement"></a>Istruzione del criterio  
  
```xml  
<set-query-parameter name="param name" exists-action="override | skip | append | delete">  
    <value>value</value> <!--for multiple parameters with hello same name add additional value elements-->  
</set-query-parameter>  
```  
  
### <a name="examples"></a>Esempi  
  
#### <a name="example"></a>Esempio  
  
```xml  
  
<set-query-parameter>  
  <parameter name="api-key" exists-action="skip">  
    <value>12345678901</value>  
  </parameter>  
  <!-- for multiple parameters with hello same name add additional value elements -->  
</set-query-parameter>  
  
```  
  
#### <a name="forward-context-information-toohello-backend-service"></a>Inoltrare servizio back-end toohello informazioni di contesto  
 Questo esempio viene illustrato come il criterio tooapply hello API livello servizio back-end di toosupply contesto informazioni toohello. Per una dimostrazione della configurazione e l'utilizzo di questo criterio, vedere [Cloud coprire episodio 177: più API le funzionalità di gestione con Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) e far avanzare rapidamente too10:30. 12:10 è una dimostrazione di chiamata di un'operazione nel portale per sviluppatori hello in cui è possibile visualizzare i criteri di hello al lavoro.  
  
```xml  
<!-- Copy this snippet into hello inbound element tooforward a piece of context, product name in this example, toohello backend service for logging or evaluation -->  
<set-query-parameter name="x-product-name" exists-action="override">  
  <value>@(context.Product.Name)</value>  
</set-query-parameter>  
  
```  
  
 Per altre informazioni, vedere [Espressioni di criteri](api-management-policy-expressions.md) e [Variabile di contesto](api-management-policy-expressions.md#ContextVariables).  
  
### <a name="elements"></a>Elementi  
  
|Nome|Descrizione|Obbligatorio|  
|----------|-----------------|--------------|  
|set-query-parameter|Elemento radice.|Sì|  
|value|Specifica il valore di hello di hello query parametro toobe set. Per più parametri di query con hello omonima aggiungere ulteriori `value` elementi.|Sì|  
  
### <a name="properties"></a>Proprietà  
  
|Nome|Descrizione|Obbligatorio|Default|  
|----------|-----------------|--------------|-------------|  
|exists-action|Specifica quali tootake azione quando il parametro di query hello è già specificato. Questo attributo deve avere uno dei seguenti valori hello.<br /><br /> -override - sostituisce hello valore del parametro esistente hello.<br />-skip: non sostituisce il valore esistente query parametro hello.<br />-aggiungere - aggiunge hello valore toohello esistente valore del parametro query.<br />-delete - rimuove il parametro di query hello dalla richiesta hello.<br /><br /> Quando impostato troppo`override` l'integrazione di più voci con hello stesso nome dei risultati nel parametro di query hello viene impostato in base tooall le voci (elencate più volte); solo i valori elencati verranno impostati nel risultato hello.|No|override|  
|name|Specifica nome del set di toobe parametri query hello.|Sì|N/D|  
  
### <a name="usage"></a>Utilizzo  
 Questo criterio può essere utilizzato hello seguenti criteri [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sezioni del criterio:** inbound, backend  
  
-   **Ambiti del criterio:** globale, prodotto, API, operazione  
  
##  <a name="RewriteURL"></a> Riscrivi URL  
 Hello `rewrite-uri` criteri converte un URL di richiesta dal formato pubblico toohello formato previsto dal servizio web hello, come illustrato nell'esempio seguente hello.  
  
-   URL pubblico - `http://api.example.com/storenumber/ordernumber`  
  
-   URL richiesta - `http://api.example.com/v2/US/hardware/storenumber&ordernumber?City&State`  
  
 Questo criterio può essere utilizzato quando un URL di risorse umane e/o orientato al browser deve essere trasformato in formato di URL hello previsto dal servizio web hello. Questo criterio deve toobe applicato quando si espone un formato di URL alternativo, ad esempio gli URL, gli URL RESTful, gli URL descrittivi o gli URL SEO semplice che sono URL puramente strutturali che non contengono una stringa di query e invece contengono solo hello percorso di hello risorsa (dopo lo schema di hello e autorità hello). Sono spesso usati a fini estetici, di usabilità o di ottimizzazione dei motori di ricerca (SEO, Search Engine Optimization).  
  
> [!NOTE]
>  È possibile aggiungere solo i parametri di stringa di query mediante criteri di hello. È possibile aggiungere parametri di percorso modello aggiuntivo in hello riscrive l'URL.  

### <a name="policy-statement"></a>Istruzione del criterio  
  
```xml  
<rewrite-uri template="uri template" copy-unmatched-params="true | false" />  
```  
  
### <a name="example"></a>Esempio  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <rewrite-uri template="/v2/US/hardware/{storenumber}&{ordernumber}?City=city&State=state" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
```xml
<!-- Assuming incoming request is /get?a=b&c=d and operation template is set too/get?a={b} -->
<policies>  
    <inbound>  
        <base />  
        <rewrite-uri template="/put" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
<!-- Resulting URL will be /put?c=d -->
```  
```xml
<!-- Assuming incoming request is /get?a=b&c=d and operation template is set too/get?a={b} -->
<policies>  
    <inbound>  
        <base />  
        <rewrite-uri template="/put" copy-unmatched-params="false" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
<!-- Resulting URL will be /put -->
```

### <a name="elements"></a>Elementi  
  
|Nome|Descrizione|Obbligatorio|  
|----------|-----------------|--------------|  
|rewrite-uri|Elemento radice.|Sì|  
  
### <a name="attributes"></a>Attributi  
  
|Attributo|Descrizione|Obbligatorio|Default|  
|---------------|-----------------|--------------|-------------|  
|template|URL del servizio web effettivo Hello con i parametri di stringa di query. Quando si utilizzano espressioni, l'intero valore hello deve essere un'espressione.|Sì|N/D|  
|copy-unmatched-params|Specifica se i parametri di query nella richiesta in ingresso hello non presente nel modello di URL originale hello vengono aggiunti URL toohello definito da hello riscrivere modello|No|true|  
  
### <a name="usage"></a>Utilizzo  
 Questo criterio può essere utilizzato hello seguenti criteri [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sezioni del criterio:** inbound  
  
-   **Ambiti del criterio:** prodotto, API, operazione  
  
##  <a name="XSLTransform"></a>Trasforma XML usando XSLT  
 Hello `Transform XML using an XSLT` criterio si applica un tooXML trasformazione XSL nel corpo della richiesta o risposta hello.  
  
### <a name="policy-statement"></a>Istruzione del criterio  
  
```xml  
<xsl-transform>  
    <parameter name="User-Agent">@(context.Request.Headers.GetValueOrDefault("User-Agent","non-specified"))</parameter>  
    <xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">  
        <xsl:output method="xml" indent="yes" />  
        <xsl:param name="User-Agent" />  
        <xsl:template match="* | @* | node()">  
            <xsl:copy>  
                <xsl:if test="self::* and not(parent::*)">  
                    <xsl:attribute name="User-Agent">  
                        <xsl:value-of select="$User-Agent" />  
                    </xsl:attribute>  
                </xsl:if>  
                <xsl:apply-templates select="* | @* | node()" />  
            </xsl:copy>  
        </xsl:template>  
    </xsl:stylesheet>  
  </xsl-transform>  
```  
  
### <a name="example"></a>Esempio  
  
```xml  
<policies>  
  <inbound>  
      <base />  
  </inbound>  
  <outbound>  
      <base />  
      <xsl-transform>  
        <xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">  
            <xsl:output omit-xml-declaration="yes" method="xml" indent="yes" />  
            <!-- Copy all nodes directly-->  
            <xsl:template match="node()| @*|*">  
                <xsl:copy>  
                    <xsl:apply-templates select="@* | node()|*" />  
                </xsl:copy>  
            </xsl:template>  
        </xsl:stylesheet>  
    </xsl-transform>  
  </outbound>  
</policies>  
```  
  
### <a name="elements"></a>Elementi  
  
|Nome|Descrizione|Obbligatorio|  
|----------|-----------------|--------------|  
|xsl-transform|Elemento radice.|Sì|  
|parametro|Variabili toodefine utilizzati utilizzate nella trasformazione hello|No|  
|xsl:stylesheet|Elemento del foglio di stile principale. Tutti gli elementi e attributi definiti all'interno di seguono standard hello [specifica XSLT](http://www.w3.org/TR/xslt)|Sì|  
  
### <a name="usage"></a>Utilizzo  
 Questo criterio può essere utilizzato hello seguenti criteri [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sezioni del criterio:** inbound, outbound  
  
-   **Ambiti del criterio:** globale, prodotto, API, operazione  
  
## <a name="next-steps"></a>Passaggi successivi
Per altre informazioni sull'uso dei criteri, vedere [Criteri di Gestione API](api-management-howto-policies.md).  
