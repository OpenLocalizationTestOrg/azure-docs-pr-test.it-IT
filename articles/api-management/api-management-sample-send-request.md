---
title: richieste di toogenerate HTTP del servizio Gestione API aaaUsing
description: Informazioni su criteri di richiesta e risposta toouse in servizi esterni di gestione API toocall dall'API
services: api-management
documentationcenter: 
author: darrelmiller
manager: erikre
editor: 
ms.assetid: 4539c0fa-21ef-4b1c-a1d4-d89a38c242fa
ms.service: api-management
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 8002ee453057513340328d99f298703c3b3a9531
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-external-services-from-hello-azure-api-management-service"></a><span data-ttu-id="104a5-103">Tramite servizi esterni da hello servizio Gestione API di Azure</span><span class="sxs-lookup"><span data-stu-id="104a5-103">Using external services from hello Azure API Management service</span></span>
<span data-ttu-id="104a5-104">criteri di Hello disponibili nel servizio di gestione API di Azure è possono eseguire un'ampia gamma di operazioni utili basata esclusivamente sul richiesta in ingresso hello, la risposta in uscita hello e informazioni di configurazione di base.</span><span class="sxs-lookup"><span data-stu-id="104a5-104">hello policies available in Azure API Management service can do a wide range of useful work based purely on hello incoming request, hello outgoing response and basic configuration information.</span></span> <span data-ttu-id="104a5-105">Tuttavia, essere in grado di toointeract con i servizi esterni da Gestione API criteri apre molti più opportunità.</span><span class="sxs-lookup"><span data-stu-id="104a5-105">However, being able toointeract with external services from API Management policies opens up many more opportunities.</span></span>

<span data-ttu-id="104a5-106">Abbiamo già visto come poter interagire con hello [servizio Hub di eventi di Azure per la registrazione, il monitoraggio e analitica](api-management-log-to-eventhub-sample.md).</span><span class="sxs-lookup"><span data-stu-id="104a5-106">We have previously seen how we can interact with hello [Azure Event Hub service for logging, monitoring and analytics](api-management-log-to-eventhub-sample.md).</span></span> <span data-ttu-id="104a5-107">In questo articolo verrà illustrato servizio basato su criteri che consentono di toointeract con qualsiasi HTTP esterno.</span><span class="sxs-lookup"><span data-stu-id="104a5-107">In this article we will demonstrate policies that allow you toointeract with any external HTTP based service.</span></span> <span data-ttu-id="104a5-108">Questi criteri possono essere usati per l'attivazione di eventi remoti o per il recupero di informazioni che saranno utilizzati toomanipulate hello originale richiesta e la risposta in qualche modo.</span><span class="sxs-lookup"><span data-stu-id="104a5-108">These policies can be used for triggering remote events or for retrieving information that will be used toomanipulate hello original request and response in some way.</span></span>

## <a name="send-one-way-request"></a><span data-ttu-id="104a5-109">Send-One-Way-Request</span><span class="sxs-lookup"><span data-stu-id="104a5-109">Send-One-Way-Request</span></span>
<span data-ttu-id="104a5-110">Probabilmente hello interazione esterno più semplice è hello fire-and-forget lo stile della richiesta che consente a un servizio esterno di toobe una notifica di un tipo di evento importante.</span><span class="sxs-lookup"><span data-stu-id="104a5-110">Possibly hello simplest external interaction is hello fire-and-forget style of request that allows an external service toobe notified of some kind of important event.</span></span> <span data-ttu-id="104a5-111">È possibile utilizzare criteri di flusso di controllo hello `choose` toodetect qualsiasi tipo di condizione che si è interessati e se hello condizione è soddisfatta, è possibile rendere una richiesta HTTP esterna utilizzando hello [richiesta unidirezionale di una trasmissione](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) criteri.</span><span class="sxs-lookup"><span data-stu-id="104a5-111">We can use hello control flow policy `choose` toodetect any kind of condition that we are interested in and then, if hello condition is satisfied, we can make an external HTTP request using hello [send-one-way-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) policy.</span></span> <span data-ttu-id="104a5-112">Potrebbe trattarsi di una richiesta tooa sistema come Hipchat o Slack o un messaggio di posta API SendGrid o MailChimp di messaggistica, o per gli eventi imprevisti supporto critico qualcosa di simile a PagerDuty.</span><span class="sxs-lookup"><span data-stu-id="104a5-112">This could be a request tooa messaging system like Hipchat or Slack, or a mail API like SendGrid or MailChimp, or for critical support incidents something like PagerDuty.</span></span> <span data-ttu-id="104a5-113">Tutti questi sistemi di messaggistica dispongono di API HTTP semplici che possono essere richiamate facilmente.</span><span class="sxs-lookup"><span data-stu-id="104a5-113">All of these messaging systems have simple HTTP APIs that we can easily invoke.</span></span>

### <a name="alerting-with-slack"></a><span data-ttu-id="104a5-114">Avvisi con Slack</span><span class="sxs-lookup"><span data-stu-id="104a5-114">Alerting with Slack</span></span>
<span data-ttu-id="104a5-115">Hello di esempio seguente viene illustrato come toosend tooa un messaggio margine di flessibilità di chat se il codice di stato di risposta HTTP hello è maggiore o uguale a too500.</span><span class="sxs-lookup"><span data-stu-id="104a5-115">hello following example demonstrates how toosend a message tooa Slack chat room if hello HTTP response status code is greater than or equal too500.</span></span> <span data-ttu-id="104a5-116">Un errore di 500 intervallo indica un problema con l'API di back-end che hello client dell'API non è possibile risolvere autonomamente.</span><span class="sxs-lookup"><span data-stu-id="104a5-116">A 500 range error indicates a problem with our backend API that hello client of our API cannot resolve themselves.</span></span> <span data-ttu-id="104a5-117">In genere richiede un intervento da parte dell'utente.</span><span class="sxs-lookup"><span data-stu-id="104a5-117">It usually requires some kind of intervention on our part.</span></span>  

```xml
<choose>
    <when condition="@(context.Response.StatusCode >= 500)">
      <send-one-way-request mode="new">
        <set-url>https://hooks.slack.com/services/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</set-url>
        <set-method>POST</set-method>
        <set-body>@{
                return new JObject(
                        new JProperty("username","APIM Alert"),
                        new JProperty("icon_emoji", ":ghost:"),
                        new JProperty("text", String.Format("{0} {1}\nHost: {2}\n{3} {4}\n User: {5}",
                                                context.Request.Method,
                                                context.Request.Url.Path + context.Request.Url.QueryString,
                                                context.Request.Url.Host,
                                                context.Response.StatusCode,
                                                context.Response.StatusReason,
                                                context.User.Email
                                                ))
                        ).ToString();
            }</set-body>
      </send-one-way-request>
    </when>
</choose>
```

<span data-ttu-id="104a5-118">Slack è nozione hello di hook web in ingresso.</span><span class="sxs-lookup"><span data-stu-id="104a5-118">Slack has hello notion of inbound web hooks.</span></span> <span data-ttu-id="104a5-119">Quando si configura un hook web in ingresso, il margine di flessibilità genera un URL speciale che consente una semplice richiesta POST toodo e toopass un messaggio nel canale di Slack hello.</span><span class="sxs-lookup"><span data-stu-id="104a5-119">When configuring an inbound web hook, Slack generates a special URL which allows you toodo a simple POST request and toopass a message into hello Slack channel.</span></span> <span data-ttu-id="104a5-120">Hello corpo JSON, creata è basata su un formato definito da Slack.</span><span class="sxs-lookup"><span data-stu-id="104a5-120">hello JSON body that we create is based on a format defined by Slack.</span></span>

![Hook Web di Slack](./media/api-management-sample-send-request/api-management-slack-webhook.png)

### <a name="is-fire-and-forget-good-enough"></a><span data-ttu-id="104a5-122">Lo stile di richiesta fire-and-forget è sufficientemente efficace?</span><span class="sxs-lookup"><span data-stu-id="104a5-122">Is fire and forget good enough?</span></span>
<span data-ttu-id="104a5-123">Quando si usa uno stile di richiesta fire-and-forget è necessario tenere presenti alcuni svantaggi.</span><span class="sxs-lookup"><span data-stu-id="104a5-123">There are certain tradeoffs when using a fire-and-forget style of request.</span></span> <span data-ttu-id="104a5-124">Se per qualche motivo, hello richiesta ha esito negativo, quindi non verrà segnalato un errore di hello.</span><span class="sxs-lookup"><span data-stu-id="104a5-124">If for some reason, hello request fails, then hello failure will not be reported.</span></span> <span data-ttu-id="104a5-125">In questo caso particolare, non sono garantite complessità hello di disporre di un sistema di segnalazione errori secondario e il costo di prestazioni hello di in attesa di risposta hello.</span><span class="sxs-lookup"><span data-stu-id="104a5-125">In this particular situation, hello complexity of having a secondary failure reporting system and hello additional performance cost of waiting for hello response is not warranted.</span></span> <span data-ttu-id="104a5-126">Per gli scenari in cui è risposta hello toocheck essenziali, hello [richiesta di invio](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) criteri sono un'opzione migliore.</span><span class="sxs-lookup"><span data-stu-id="104a5-126">For scenarios where it is essential toocheck hello response, then hello [send-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) policy is a better option.</span></span>

## <a name="send-request"></a><span data-ttu-id="104a5-127">send-request</span><span class="sxs-lookup"><span data-stu-id="104a5-127">Send-Request</span></span>
<span data-ttu-id="104a5-128">Hello `send-request` criteri consente l'uso di un servizio esterno di tooperform complesse funzioni e servizio di gestione toohello API restituisce i dati che può essere utilizzato per un'ulteriore elaborazione di criteri di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="104a5-128">hello `send-request` policy enables using an external service tooperform complex processing functions and return data toohello API management service that can be used for further policy processing.</span></span>

### <a name="authorizing-reference-tokens"></a><span data-ttu-id="104a5-129">Autorizzazione di token di riferimento</span><span class="sxs-lookup"><span data-stu-id="104a5-129">Authorizing reference tokens</span></span>
<span data-ttu-id="104a5-130">Una funzione fondamentale di Gestione API è la protezione delle risorse back-end.</span><span class="sxs-lookup"><span data-stu-id="104a5-130">A major function of API Management is protecting backend resources.</span></span> <span data-ttu-id="104a5-131">Se il server di autorizzazione hello utilizzato per l'API crea [i token JWT](http://jwt.io/) come parte del relativo flusso OAuth2, come [Azure Active Directory](../active-directory/active-directory-aadconnect.md) avviene, è possibile utilizzare hello `validate-jwt` validità hello tooverify di criteri di token Hello.</span><span class="sxs-lookup"><span data-stu-id="104a5-131">If hello authorization server used by your API creates [JWT tokens](http://jwt.io/) as part of its OAuth2 flow, as [Azure Active Directory](../active-directory/active-directory-aadconnect.md) does, then you can use hello `validate-jwt` policy tooverify hello validity of hello token.</span></span> <span data-ttu-id="104a5-132">Tuttavia, alcuni server di autorizzazione creare cosiddetti [fanno riferimento a token](http://leastprivilege.com/2015/11/25/reference-tokens-and-introspection/) che non è possibile verificare senza un server di autorizzazione toohello indietro di chiamata.</span><span class="sxs-lookup"><span data-stu-id="104a5-132">However, some authorization servers create what are called [reference tokens](http://leastprivilege.com/2015/11/25/reference-tokens-and-introspection/) that cannot be verified without making a call back toohello authorization server.</span></span>

### <a name="standardized-introspection"></a><span data-ttu-id="104a5-133">Introspezione standardizzata</span><span class="sxs-lookup"><span data-stu-id="104a5-133">Standardized introspection</span></span>
<span data-ttu-id="104a5-134">In hello precedente non si è verificato alcun modo standardizzato verificare se un token di riferimento con un server di autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="104a5-134">In hello past there has been no standardized way of verifying a reference token with an authorization server.</span></span> <span data-ttu-id="104a5-135">Tuttavia recentemente proposta di standard [7662 RFC](https://tools.ietf.org/html/rfc7662) ha pubblicato hello IETF che definisce come un server delle risorse può verificare la validità hello di un token.</span><span class="sxs-lookup"><span data-stu-id="104a5-135">However a recently proposed standard [RFC 7662](https://tools.ietf.org/html/rfc7662) was published by hello IETF that defines how a resource server can verify hello validity of a token.</span></span>

### <a name="extracting-hello-token"></a><span data-ttu-id="104a5-136">L'estrazione dei token hello</span><span class="sxs-lookup"><span data-stu-id="104a5-136">Extracting hello token</span></span>
<span data-ttu-id="104a5-137">primo passaggio Hello è token hello tooextract dall'intestazione di autorizzazione hello.</span><span class="sxs-lookup"><span data-stu-id="104a5-137">hello first step is tooextract hello token from hello Authorization header.</span></span> <span data-ttu-id="104a5-138">valore dell'intestazione Hello deve essere formattato con hello `Bearer` lo schema di autorizzazione, un singolo spazio e quindi autorizzazione hello token in base [RFC 6750](http://tools.ietf.org/html/rfc6750#section-2.1).</span><span class="sxs-lookup"><span data-stu-id="104a5-138">hello header value should be formatted with hello `Bearer` authorization scheme, a single space and then hello authorization token as per [RFC 6750](http://tools.ietf.org/html/rfc6750#section-2.1).</span></span> <span data-ttu-id="104a5-139">Vi sono casi in cui lo schema di autorizzazione hello è omesso.</span><span class="sxs-lookup"><span data-stu-id="104a5-139">Unfortunately there are cases where hello authorization scheme is omitted.</span></span> <span data-ttu-id="104a5-140">tooaccount per questo durante l'analisi, verranno suddivise valore dell'intestazione hello in uno spazio e stringa ultimo hello selezionare hello ha restituito una matrice di stringhe.</span><span class="sxs-lookup"><span data-stu-id="104a5-140">tooaccount for this when parsing, we split hello header value on a space and select hello last string from hello returned array of strings.</span></span> <span data-ttu-id="104a5-141">Questa rappresenta una soluzione alternativa per le intestazioni di autorizzazione con formato non corretto.</span><span class="sxs-lookup"><span data-stu-id="104a5-141">This provides a workaround for badly formatted authorization headers.</span></span>

```xml
<set-variable name="token" value="@(context.Request.Headers.GetValueOrDefault("Authorization","scheme param").Split(' ').Last())" />
```

### <a name="making-hello-validation-request"></a><span data-ttu-id="104a5-142">Richiesta di convalida hello</span><span class="sxs-lookup"><span data-stu-id="104a5-142">Making hello validation request</span></span>
<span data-ttu-id="104a5-143">Una volta ottenuto il token di autorizzazione hello, è possibile rendere i token di hello richiesta toovalidate hello.</span><span class="sxs-lookup"><span data-stu-id="104a5-143">Once we have hello authorization token, we can make hello request toovalidate hello token.</span></span> <span data-ttu-id="104a5-144">RFC 7662 chiama introspezione questo processo e richiede che si `POST` una risorsa di introspezione toohello di form HTML.</span><span class="sxs-lookup"><span data-stu-id="104a5-144">RFC 7662 calls this process introspection and requires that you `POST` a HTML form toohello introspection resource.</span></span> <span data-ttu-id="104a5-145">Hello form HTML deve contenere almeno una coppia chiave/valore con chiave hello `token`.</span><span class="sxs-lookup"><span data-stu-id="104a5-145">hello HTML form must at least contain a key/value pair with hello key `token`.</span></span> <span data-ttu-id="104a5-146">Questo server di autorizzazione toohello richiesta deve essere autenticato tooensure che client dannosi non è possibile passare dovuti per i token validi.</span><span class="sxs-lookup"><span data-stu-id="104a5-146">This request toohello authorization server must also be authenticated tooensure that malicious clients cannot go trawling for valid tokens.</span></span>

```xml
<send-request mode="new" response-variable-name="tokenstate" timeout="20" ignore-error="true">
  <set-url>https://microsoft-apiappec990ad4c76641c6aea22f566efc5a4e.azurewebsites.net/introspection</set-url>
  <set-method>POST</set-method>
  <set-header name="Authorization" exists-action="override">
    <value>basic dXNlcm5hbWU6cGFzc3dvcmQ=</value>
  </set-header>
  <set-header name="Content-Type" exists-action="override">
    <value>application/x-www-form-urlencoded</value>
  </set-header>
  <set-body>@($"token={(string)context.Variables["token"]}")</set-body>
</send-request>
```

### <a name="checking-hello-response"></a><span data-ttu-id="104a5-147">Controllo risposta hello</span><span class="sxs-lookup"><span data-stu-id="104a5-147">Checking hello response</span></span>
<span data-ttu-id="104a5-148">Hello `response-variable-name` attributo è usato toogive hello di accesso ha restituito una risposta.</span><span class="sxs-lookup"><span data-stu-id="104a5-148">hello `response-variable-name` attribute is used toogive access hello returned response.</span></span> <span data-ttu-id="104a5-149">Hello nome definito in questa proprietà può essere utilizzato come chiave in hello `context.Variables` hello tooaccess dizionario `IResponse` oggetto.</span><span class="sxs-lookup"><span data-stu-id="104a5-149">hello name defined in this property can be used as a key into hello `context.Variables` dictionary tooaccess hello `IResponse` object.</span></span>

<span data-ttu-id="104a5-150">Oggetto risposta hello è possibile recuperare il corpo di hello e RFC 7622 indica che la risposta hello deve essere un oggetto JSON e deve contenere almeno una proprietà denominata `active` che rappresenta un valore booleano.</span><span class="sxs-lookup"><span data-stu-id="104a5-150">From hello response object we can retrieve hello body and RFC 7622 tells us that hello response must be a JSON object and must contain at least a property called `active` that is a boolean value.</span></span> <span data-ttu-id="104a5-151">Quando `active` è true, il token hello è considerato valido.</span><span class="sxs-lookup"><span data-stu-id="104a5-151">When `active` is true then hello token is considered valid.</span></span>

### <a name="reporting-failure"></a><span data-ttu-id="104a5-152">Creazione di report sull'errore</span><span class="sxs-lookup"><span data-stu-id="104a5-152">Reporting failure</span></span>
<span data-ttu-id="104a5-153">Utilizziamo un `<choose>` toodetect criteri se hello token non è valido e in tal caso, restituire una risposta 401.</span><span class="sxs-lookup"><span data-stu-id="104a5-153">We use a `<choose>` policy toodetect if hello token is invalid and if so, return a 401 response.</span></span>

```xml
<choose>
  <when condition="@((bool)((IResponse)context.Variables["tokenstate"]).Body.As<JObject>()["active"] == false)">
    <return-response response-variable-name="existing response variable">
      <set-status code="401" reason="Unauthorized" />
      <set-header name="WWW-Authenticate" exists-action="override">
        <value>Bearer error="invalid_token"</value>
      </set-header>
    </return-response>
  </when>
</choose>
```

<span data-ttu-id="104a5-154">In base [RFC 6750](https://tools.ietf.org/html/rfc6750#section-3) che descrive come `bearer` token devono essere utilizzati, anche restituiamo un `WWW-Authenticate` intestazione risposta hello 401.</span><span class="sxs-lookup"><span data-stu-id="104a5-154">As per [RFC 6750](https://tools.ietf.org/html/rfc6750#section-3) which describes how `bearer` tokens should be used, we also return a `WWW-Authenticate` header with hello 401 response.</span></span> <span data-ttu-id="104a5-155">Hello WWW-Authenticate è previsto tooinstruct un client come tooconstruct una richiesta autorizzata correttamente.</span><span class="sxs-lookup"><span data-stu-id="104a5-155">hello WWW-Authenticate is intended tooinstruct a client on how tooconstruct a properly authorized request.</span></span> <span data-ttu-id="104a5-156">A causa di toohello vasta gamma di metodi possibili con framework hello OAuth2, risulta difficile toocommunicate tutti hello informazioni necessarie.</span><span class="sxs-lookup"><span data-stu-id="104a5-156">Due toohello wide variety of approaches possible with hello OAuth2 framework, it is difficult toocommunicate all hello needed information.</span></span> <span data-ttu-id="104a5-157">Per fortuna sono presenti attività in corso toohelp [client individuare come tooproperly autorizzare i server delle risorse richieste tooa](http://tools.ietf.org/html/draft-jones-oauth-discovery-00).</span><span class="sxs-lookup"><span data-stu-id="104a5-157">Fortunately there are efforts underway toohelp [clients discover how tooproperly authorize requests tooa resource server](http://tools.ietf.org/html/draft-jones-oauth-discovery-00).</span></span>

### <a name="final-solution"></a><span data-ttu-id="104a5-158">Soluzione finale</span><span class="sxs-lookup"><span data-stu-id="104a5-158">Final solution</span></span>
<span data-ttu-id="104a5-159">Combinazione di tutti i componenti di hello, si ottiene hello seguenti criteri:</span><span class="sxs-lookup"><span data-stu-id="104a5-159">Putting all hello pieces together, we get hello following policy:</span></span>

```xml
<inbound>
  <!-- Extract Token from Authorization header parameter -->
  <set-variable name="token" value="@(context.Request.Headers.GetValueOrDefault("Authorization","scheme param").Split(' ').Last())" />

  <!-- Send request tooToken Server toovalidate token (see RFC 7662) -->
  <send-request mode="new" response-variable-name="tokenstate" timeout="20" ignore-error="true">
    <set-url>https://microsoft-apiappec990ad4c76641c6aea22f566efc5a4e.azurewebsites.net/introspection</set-url>
    <set-method>POST</set-method>
    <set-header name="Authorization" exists-action="override">
      <value>basic dXNlcm5hbWU6cGFzc3dvcmQ=</value>
    </set-header>
    <set-header name="Content-Type" exists-action="override">
      <value>application/x-www-form-urlencoded</value>
    </set-header>
    <set-body>@($"token={(string)context.Variables["token"]}")</set-body>
  </send-request>

  <choose>
          <!-- Check active property in response -->
          <when condition="@((bool)((IResponse)context.Variables["tokenstate"]).Body.As<JObject>()["active"] == false)">
              <!-- Return 401 Unauthorized with http-problem payload -->
              <return-response response-variable-name="existing response variable">
                  <set-status code="401" reason="Unauthorized" />
                  <set-header name="WWW-Authenticate" exists-action="override">
                      <value>Bearer error="invalid_token"</value>
                  </set-header>
              </return-response>
          </when>
      </choose>
  <base />
</inbound>
```

<span data-ttu-id="104a5-160">Questo è solo uno dei molti esempi di come hello `send-request` criteri possono essere utilizzati toointegrate servizi esterni utili nel processo di hello di richieste e risposte che passano attraverso il servizio Gestione API hello.</span><span class="sxs-lookup"><span data-stu-id="104a5-160">This is only one of many examples of how hello `send-request` policy can be used toointegrate useful external services into hello process of requests and responses flowing through hello API Management service.</span></span>

## <a name="response-composition"></a><span data-ttu-id="104a5-161">Composizione della risposta</span><span class="sxs-lookup"><span data-stu-id="104a5-161">Response Composition</span></span>
<span data-ttu-id="104a5-162">Hello `send-request` criteri possono essere utilizzati per l'ottimizzazione di un sistema back-end tooa richiesta primaria, come illustrato nell'esempio precedente hello, oppure può essere utilizzato come una sostituzione completa della chiamata di hello back-end.</span><span class="sxs-lookup"><span data-stu-id="104a5-162">hello `send-request` policy can be used for enhancing a primary request tooa backend system, as we saw in hello previous example, or it can be used as a complete replace for of hello backend call.</span></span> <span data-ttu-id="104a5-163">Questa tecnica consente di creare facilmente risorse composite che vengono aggregate da più sistemi.</span><span class="sxs-lookup"><span data-stu-id="104a5-163">Using this technique we can easily create composite resources that are aggregated from multiple different systems.</span></span>

### <a name="building-a-dashboard"></a><span data-ttu-id="104a5-164">Creazione di un dashboard</span><span class="sxs-lookup"><span data-stu-id="104a5-164">Building a dashboard</span></span>
<span data-ttu-id="104a5-165">Talvolta toobe tooexpose in grado di informazioni che esiste in più sistemi back-end, ad esempio, toodrive un dashboard.</span><span class="sxs-lookup"><span data-stu-id="104a5-165">Sometimes you want toobe able tooexpose information that exists in multiple backend systems, for example, toodrive a dashboard.</span></span> <span data-ttu-id="104a5-166">gli indicatori KPI Hello provengono da tutti i diversi sistemi back-end, ma si preferisce non tooprovide l'accesso diretto toothem e sarebbe utile se è stato possibile recuperare tutte le informazioni di hello in una singola richiesta.</span><span class="sxs-lookup"><span data-stu-id="104a5-166">hello KPIs come from all different back-ends, but you would prefer not tooprovide direct access toothem and it would be nice if all hello information could be retrieved in a single request.</span></span> <span data-ttu-id="104a5-167">Ad esempio alcune delle informazioni di back-end hello necessita di alcuni sezionamento e trasformando e un po' la purificazione degli prima!</span><span class="sxs-lookup"><span data-stu-id="104a5-167">Perhaps some of hello backend information needs some slicing and dicing and a little sanitizing first!</span></span> <span data-ttu-id="104a5-168">Essere in grado di toocache tale risorsa composita sarà un utile tooreduce back-end hello caricare come descritto in precedenza gli utenti hanno l'abitudine di hammering tasto F5 hello in ordine toosee se le metriche underperforming potrebbero cambiare.</span><span class="sxs-lookup"><span data-stu-id="104a5-168">Being able toocache that composite resource would be a useful tooreduce hello backend load as you know users have a habit of hammering hello F5 key in order toosee if their underperforming metrics might change.</span></span>    

### <a name="faking-hello-resource"></a><span data-ttu-id="104a5-169">Falsificare risorse hello</span><span class="sxs-lookup"><span data-stu-id="104a5-169">Faking hello resource</span></span>
<span data-ttu-id="104a5-170">primo passaggio toobuilding Hello la risorsa dashboard sia tooconfigure una nuova operazione nel portale di pubblicazione di gestione API hello.</span><span class="sxs-lookup"><span data-stu-id="104a5-170">hello first step toobuilding our dashboard resource is tooconfigure a new operation in hello API Management publisher portal.</span></span> <span data-ttu-id="104a5-171">Questo sarà un tooconfigure operazione utilizzata segnaposto nostri toobuild criteri composizione alla risorsa dinamica.</span><span class="sxs-lookup"><span data-stu-id="104a5-171">This will be a placeholder operation used tooconfigure our composition policy toobuild our dynamic resource.</span></span>

![Operazione dashboard](./media/api-management-sample-send-request/api-management-dashboard-operation.png)

### <a name="making-hello-requests"></a><span data-ttu-id="104a5-173">Effettua richieste hello</span><span class="sxs-lookup"><span data-stu-id="104a5-173">Making hello requests</span></span>
<span data-ttu-id="104a5-174">Una volta hello `dashboard` è stata creata l'operazione è possibile configurare un criterio per l'operazione.</span><span class="sxs-lookup"><span data-stu-id="104a5-174">Once hello `dashboard` operation has been created we can configure a policy specifically for that operation.</span></span> 

![Operazione dashboard](./media/api-management-sample-send-request/api-management-dashboard-policy.png)

<span data-ttu-id="104a5-176">primo passaggio Hello è tooextract eventuali parametri di query hello richiesta in ingresso, in modo che possiamo inoltrarli tooour di back-end.</span><span class="sxs-lookup"><span data-stu-id="104a5-176">hello first step  is tooextract any query parameters from hello incoming request, so that we can forward them tooour backend.</span></span> <span data-ttu-id="104a5-177">In questo esempio il dashboard visualizza informazioni basate su un periodo di tempo e dispone quindi dei parametri `fromDate` e `toDate`.</span><span class="sxs-lookup"><span data-stu-id="104a5-177">In this example our dashboard is showing information based on a period of time an therefore has a `fromDate` and `toDate` parameter.</span></span> <span data-ttu-id="104a5-178">È possibile utilizzare hello `set-variable` criteri tooextract hello informazioni hello URL della richiesta.</span><span class="sxs-lookup"><span data-stu-id="104a5-178">We can use hello `set-variable` policy tooextract hello information from hello request URL.</span></span>

```xml
<set-variable name="fromDate" value="@(context.Request.Url.Query["fromDate"].Last())">
<set-variable name="toDate" value="@(context.Request.Url.Query["toDate"].Last())">
```

<span data-ttu-id="104a5-179">Una volta che queste informazioni è possibile rendere i sistemi back-end di hello tooall richieste.</span><span class="sxs-lookup"><span data-stu-id="104a5-179">Once we have this information we can make requests tooall hello backend systems.</span></span> <span data-ttu-id="104a5-180">Ogni richiesta crea un nuovo URL con informazioni sul parametro hello e chiama rispettivo server e archivia la risposta hello in una variabile di contesto.</span><span class="sxs-lookup"><span data-stu-id="104a5-180">Each request constructs a new URL with hello parameter information and calls its respective server and stores hello response in a context variable.</span></span>

```xml
<send-request mode="new" response-variable-name="revenuedata" timeout="20" ignore-error="true">
  <set-url>@($"https://accounting.acme.com/salesdata?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
  <set-method>GET</set-method>
</send-request>

<send-request mode="new" response-variable-name="materialdata" timeout="20" ignore-error="true">
  <set-url>@($"https://inventory.acme.com/materiallevels?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
  <set-method>GET</set-method>
</send-request>

<send-request mode="new" response-variable-name="throughputdata" timeout="20" ignore-error="true">
<set-url>@($"https://production.acme.com/throughput?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
  <set-method>GET</set-method>
</send-request>

<send-request mode="new" response-variable-name="accidentdata" timeout="20" ignore-error="true">
<set-url>@($"https://production.acme.com/throughput?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
  <set-method>GET</set-method>
</send-request>
```

<span data-ttu-id="104a5-181">Queste richieste vengono eseguite in sequenza, ma non si tratta della situazione ideale.</span><span class="sxs-lookup"><span data-stu-id="104a5-181">These requests will execute in sequence, which is not ideal.</span></span> <span data-ttu-id="104a5-182">In una versione futura è verrà introdotto un nuovo criterio denominato `wait` che consentirà di tutti questi tooexecute le richieste in parallelo.</span><span class="sxs-lookup"><span data-stu-id="104a5-182">In an upcoming release we will be introducing a new policy called `wait` that will enable all of these requests tooexecute in parallel.</span></span>

### <a name="responding"></a><span data-ttu-id="104a5-183">Invio delle risposte</span><span class="sxs-lookup"><span data-stu-id="104a5-183">Responding</span></span>
<span data-ttu-id="104a5-184">risposta composito hello tooconstruct possiamo utilizzare hello [restituito risposta](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) criteri.</span><span class="sxs-lookup"><span data-stu-id="104a5-184">tooconstruct hello composite response we can use hello [return-response](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) policy.</span></span> <span data-ttu-id="104a5-185">Hello `set-body` elemento è possibile utilizzare un'espressione tooconstruct un nuovo `JObject` con tutte le rappresentazioni di componente hello incorporate come proprietà.</span><span class="sxs-lookup"><span data-stu-id="104a5-185">hello `set-body` element can use an expression tooconstruct a new `JObject` with all hello component representations embedded as properties.</span></span>

```xml
<return-response response-variable-name="existing response variable">
  <set-status code="200" reason="OK" />
  <set-header name="Content-Type" exists-action="override">
    <value>application/json</value>
  </set-header>
  <set-body>
    @(new JObject(new JProperty("revenuedata",((IResponse)context.Variables["revenuedata"]).Body.As<JObject>()),
                  new JProperty("materialdata",((IResponse)context.Variables["materialdata"]).Body.As<JObject>()),
                  new JProperty("throughputdata",((IResponse)context.Variables["throughputdata"]).Body.As<JObject>()),
                  new JProperty("accidentdata",((IResponse)context.Variables["accidentdata"]).Body.As<JObject>())
                  ).ToString())
  </set-body>
</return-response>
```

<span data-ttu-id="104a5-186">criteri completa Hello è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="104a5-186">hello complete policy looks as follows:</span></span>

```xml
<policies>
    <inbound>

  <set-variable name="fromDate" value="@(context.Request.Url.Query["fromDate"].Last())">
  <set-variable name="toDate" value="@(context.Request.Url.Query["toDate"].Last())">

    <send-request mode="new" response-variable-name="revenuedata" timeout="20" ignore-error="true">
      <set-url>@($"https://accounting.acme.com/salesdata?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
      <set-method>GET</set-method>
    </send-request>

    <send-request mode="new" response-variable-name="materialdata" timeout="20" ignore-error="true">
      <set-url>@($"https://inventory.acme.com/materiallevels?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
      <set-method>GET</set-method>
    </send-request>

    <send-request mode="new" response-variable-name="throughputdata" timeout="20" ignore-error="true">
    <set-url>@($"https://production.acme.com/throughput?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
      <set-method>GET</set-method>
    </send-request>

    <send-request mode="new" response-variable-name="accidentdata" timeout="20" ignore-error="true">
    <set-url>@($"https://production.acme.com/throughput?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
      <set-method>GET</set-method>
    </send-request>

    <return-response response-variable-name="existing response variable">
      <set-status code="200" reason="OK" />
      <set-header name="Content-Type" exists-action="override">
        <value>application/json</value>
      </set-header>
      <set-body>
        @(new JObject(new JProperty("revenuedata",((IResponse)context.Variables["revenuedata"]).Body.As<JObject>()),
                      new JProperty("materialdata",((IResponse)context.Variables["materialdata"]).Body.As<JObject>()),
                      new JProperty("throughputdata",((IResponse)context.Variables["throughputdata"]).Body.As<JObject>()),
                      new JProperty("accidentdata",((IResponse)context.Variables["accidentdata"]).Body.As<JObject>())
                      ).ToString())
      </set-body>
    </return-response>
    </inbound>
    <backend>
        <base />
    </backend>
    <outbound>
        <base />
    </outbound>
</policies>
```

<span data-ttu-id="104a5-187">Nella configurazione di hello dell'operazione di segnaposto hello che è possibile configurare hello dashboard risorse toobe memorizzato nella cache per almeno un'ora perché è comprendere la natura hello dei dati hello significa che anche se si tratta di un'ora aggiornata, che sarà comunque sufficientemente efficace utenti di tooconvey preziosi toohello.</span><span class="sxs-lookup"><span data-stu-id="104a5-187">In hello configuration of hello placeholder operation we can configure hello dashboard resource toobe cached for at least an hour because we understand hello nature of hello data means that even if it is an hour out of date, it will still be sufficiently effective tooconvey valuable information toohello users.</span></span>

## <a name="summary"></a><span data-ttu-id="104a5-188">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="104a5-188">Summary</span></span>
<span data-ttu-id="104a5-189">Servizio gestione API di Azure fornisce criteri flessibili che possono essere in modo selettivo applicato tooHTTP traffico e consente di composizione di servizi back-end.</span><span class="sxs-lookup"><span data-stu-id="104a5-189">Azure API Management service provides flexible policies that can be selectively applied tooHTTP traffic and enables composition of backend services.</span></span> <span data-ttu-id="104a5-190">Se si desidera che il gateway API con avvisi di funzioni, la verifica, la funzionalità di convalida tooenhance o creano nuove risorse composite in base a più servizi back-end, hello `send-request` e criteri correlati aprire un mondo di possibilità.</span><span class="sxs-lookup"><span data-stu-id="104a5-190">Whether you want tooenhance your API gateway with alerting functions, verification, validation capabilities or create new composite resources based on multiple backend services, hello `send-request` and related policies open a world of possibilities.</span></span>

## <a name="watch-a-video-overview-of-these-policies"></a><span data-ttu-id="104a5-191">Video contenente una panoramica di questi criteri</span><span class="sxs-lookup"><span data-stu-id="104a5-191">Watch a video overview of these policies</span></span>
<span data-ttu-id="104a5-192">Per ulteriori informazioni su hello [richiesta unidirezionale di una trasmissione](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest), [richiesta di invio](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest), e [restituito risposta](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) criteri descritti in questo articolo, guardare hello video seguenti.</span><span class="sxs-lookup"><span data-stu-id="104a5-192">For more information on hello [send-one-way-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest), [send-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest), and [return-response](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) policies covered in this article, please watch hello following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Send-Request-and-Return-Response-Policies/player]
> 
> 

