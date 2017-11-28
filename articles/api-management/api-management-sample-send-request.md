---
title: Uso del servizio Gestione API per generare richieste HTTP
description: Informazioni sull'uso dei criteri di richiesta e risposta in Gestione API per chiamare servizi esterni dall'API
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
ms.openlocfilehash: e778943715d6ca5256ad612d82bdc1f82197df0d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="using-external-services-from-the-azure-api-management-service"></a><span data-ttu-id="53867-103">Uso di servizi esterni dal servizio Gestione API di Azure</span><span class="sxs-lookup"><span data-stu-id="53867-103">Using external services from the Azure API Management service</span></span>
<span data-ttu-id="53867-104">I criteri disponibili nel servizio Gestione API di Azure possono essere usati per una vasta gamma di attività basate esclusivamente su richieste in ingresso, risposte in uscita e informazioni di configurazione di base.</span><span class="sxs-lookup"><span data-stu-id="53867-104">The policies available in Azure API Management service can do a wide range of useful work based purely on the incoming request, the outgoing response and basic configuration information.</span></span> <span data-ttu-id="53867-105">Tuttavia, la possibilità di interagire con i servizi esterni dai criteri di Gestione API offre molte altre opportunità.</span><span class="sxs-lookup"><span data-stu-id="53867-105">However, being able to interact with external services from API Management policies opens up many more opportunities.</span></span>

<span data-ttu-id="53867-106">In precedenza è stata analizzata l'interazione con il [servizio Hub eventi di Azure per la registrazione, il monitoraggio e l'analisi](api-management-log-to-eventhub-sample.md).</span><span class="sxs-lookup"><span data-stu-id="53867-106">We have previously seen how we can interact with the [Azure Event Hub service for logging, monitoring and analytics](api-management-log-to-eventhub-sample.md).</span></span> <span data-ttu-id="53867-107">In questo articolo verranno descritti i criteri che consentono di interagire con qualsiasi servizio esterno basato su HTTP.</span><span class="sxs-lookup"><span data-stu-id="53867-107">In this article we will demonstrate policies that allow you to interact with any external HTTP based service.</span></span> <span data-ttu-id="53867-108">Questi criteri possono essere usati per l'attivazione di eventi remoti o per il recupero di informazioni che verranno usate per gestire la richiesta e la risposta originali.</span><span class="sxs-lookup"><span data-stu-id="53867-108">These policies can be used for triggering remote events or for retrieving information that will be used to manipulate the original request and response in some way.</span></span>

## <a name="send-one-way-request"></a><span data-ttu-id="53867-109">Send-One-Way-Request</span><span class="sxs-lookup"><span data-stu-id="53867-109">Send-One-Way-Request</span></span>
<span data-ttu-id="53867-110">Probabilmente l'interazione esterna più semplice è lo stile fire-and-forget della richiesta, che consente a un servizio esterno di ricevere una notifica se si verifica un evento importante.</span><span class="sxs-lookup"><span data-stu-id="53867-110">Possibly the simplest external interaction is the fire-and-forget style of request that allows an external service to be notified of some kind of important event.</span></span> <span data-ttu-id="53867-111">È possibile usare i criteri del flusso di controllo `choose` per rilevare qualsiasi tipo di condizione di interesse e quindi, se la condizione è soddisfatta, inviare una richiesta HTTP esterna usando i criteri [send-one-way-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) .</span><span class="sxs-lookup"><span data-stu-id="53867-111">We can use the control flow policy `choose` to detect any kind of condition that we are interested in and then, if the condition is satisfied, we can make an external HTTP request using the [send-one-way-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) policy.</span></span> <span data-ttu-id="53867-112">Può trattarsi di una richiesta a un sistema di messaggistica, ad esempio Hipchat o Slack, o a un'API di posta elettronica, ad esempio SendGrid o MailChimp, o per eventi che richiedono interventi di supporto critico, ad esempio PagerDuty.</span><span class="sxs-lookup"><span data-stu-id="53867-112">This could be a request to a messaging system like Hipchat or Slack, or a mail API like SendGrid or MailChimp, or for critical support incidents something like PagerDuty.</span></span> <span data-ttu-id="53867-113">Tutti questi sistemi di messaggistica dispongono di API HTTP semplici che possono essere richiamate facilmente.</span><span class="sxs-lookup"><span data-stu-id="53867-113">All of these messaging systems have simple HTTP APIs that we can easily invoke.</span></span>

### <a name="alerting-with-slack"></a><span data-ttu-id="53867-114">Avvisi con Slack</span><span class="sxs-lookup"><span data-stu-id="53867-114">Alerting with Slack</span></span>
<span data-ttu-id="53867-115">L'esempio seguente illustra come inviare un messaggio a una chat di Slack, se il codice di stato della risposta HTTP è maggiore o uguale a 500.</span><span class="sxs-lookup"><span data-stu-id="53867-115">The following example demonstrates how to send a message to a Slack chat room if the HTTP response status code is greater than or equal to 500.</span></span> <span data-ttu-id="53867-116">Un errore di intervallo 500 indica un problema con l'API back-end che il client dell'API non può risolvere automaticamente.</span><span class="sxs-lookup"><span data-stu-id="53867-116">A 500 range error indicates a problem with our backend API that the client of our API cannot resolve themselves.</span></span> <span data-ttu-id="53867-117">In genere richiede un intervento da parte dell'utente.</span><span class="sxs-lookup"><span data-stu-id="53867-117">It usually requires some kind of intervention on our part.</span></span>  

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

<span data-ttu-id="53867-118">In Slack sono disponibili gli hook Web in ingresso.</span><span class="sxs-lookup"><span data-stu-id="53867-118">Slack has the notion of inbound web hooks.</span></span> <span data-ttu-id="53867-119">Quando si configura un hook Web in ingresso, Slack genera un URL specifico che consente di eseguire una semplice richiesta POST e di passare un messaggio nel canale di Slack.</span><span class="sxs-lookup"><span data-stu-id="53867-119">When configuring an inbound web hook, Slack generates a special URL which allows you to do a simple POST request and to pass a message into the Slack channel.</span></span> <span data-ttu-id="53867-120">Il corpo JSON creato è basato su un formato definito da Slack.</span><span class="sxs-lookup"><span data-stu-id="53867-120">The JSON body that we create is based on a format defined by Slack.</span></span>

![Hook Web di Slack](./media/api-management-sample-send-request/api-management-slack-webhook.png)

### <a name="is-fire-and-forget-good-enough"></a><span data-ttu-id="53867-122">Lo stile di richiesta fire-and-forget è sufficientemente efficace?</span><span class="sxs-lookup"><span data-stu-id="53867-122">Is fire and forget good enough?</span></span>
<span data-ttu-id="53867-123">Quando si usa uno stile di richiesta fire-and-forget è necessario tenere presenti alcuni svantaggi.</span><span class="sxs-lookup"><span data-stu-id="53867-123">There are certain tradeoffs when using a fire-and-forget style of request.</span></span> <span data-ttu-id="53867-124">Se per qualche motivo la richiesta ha esito negativo, l'errore non viene segnalato.</span><span class="sxs-lookup"><span data-stu-id="53867-124">If for some reason, the request fails, then the failure will not be reported.</span></span> <span data-ttu-id="53867-125">In questo caso, la complessità di disporre di un sistema secondario di segnalazione dell'errore e il costo aggiuntivo delle prestazioni per l'attesa della risposta non sono garantiti.</span><span class="sxs-lookup"><span data-stu-id="53867-125">In this particular situation, the complexity of having a secondary failure reporting system and the additional performance cost of waiting for the response is not warranted.</span></span> <span data-ttu-id="53867-126">Per gli scenari in cui è fondamentale verificare la risposta, i criteri [send-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) rappresentano un'opzione migliore.</span><span class="sxs-lookup"><span data-stu-id="53867-126">For scenarios where it is essential to check the response, then the [send-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) policy is a better option.</span></span>

## <a name="send-request"></a><span data-ttu-id="53867-127">send-request</span><span class="sxs-lookup"><span data-stu-id="53867-127">Send-Request</span></span>
<span data-ttu-id="53867-128">I criteri `send-request` consentono l'utilizzo di un servizio esterno per eseguire funzioni di elaborazione complesse e restituire dati al servizio Gestione API, che può essere usato per un'elaborazione successiva dei criteri.</span><span class="sxs-lookup"><span data-stu-id="53867-128">The `send-request` policy enables using an external service to perform complex processing functions and return data to the API management service that can be used for further policy processing.</span></span>

### <a name="authorizing-reference-tokens"></a><span data-ttu-id="53867-129">Autorizzazione di token di riferimento</span><span class="sxs-lookup"><span data-stu-id="53867-129">Authorizing reference tokens</span></span>
<span data-ttu-id="53867-130">Una funzione fondamentale di Gestione API è la protezione delle risorse back-end.</span><span class="sxs-lookup"><span data-stu-id="53867-130">A major function of API Management is protecting backend resources.</span></span> <span data-ttu-id="53867-131">Se il server di autorizzazione usato dall'API crea [token JWT](http://jwt.io/) come parte del flusso OAuth2, in modo analogo ad [Azure Active Directory](../active-directory/active-directory-aadconnect.md), è possibile usare i criteri `validate-jwt` per verificare la validità del token.</span><span class="sxs-lookup"><span data-stu-id="53867-131">If the authorization server used by your API creates [JWT tokens](http://jwt.io/) as part of its OAuth2 flow, as [Azure Active Directory](../active-directory/active-directory-aadconnect.md) does, then you can use the `validate-jwt` policy to verify the validity of the token.</span></span> <span data-ttu-id="53867-132">Tuttavia, alcuni server di autorizzazione creano i cosiddetti [token di riferimento](http://leastprivilege.com/2015/11/25/reference-tokens-and-introspection/) , che non possono essere verificati senza eseguire il callback al server di autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="53867-132">However, some authorization servers create what are called [reference tokens](http://leastprivilege.com/2015/11/25/reference-tokens-and-introspection/) that cannot be verified without making a call back to the authorization server.</span></span>

### <a name="standardized-introspection"></a><span data-ttu-id="53867-133">Introspezione standardizzata</span><span class="sxs-lookup"><span data-stu-id="53867-133">Standardized introspection</span></span>
<span data-ttu-id="53867-134">In passato non era disponibile alcuna modalità standardizzata per verificare un token di riferimento con un server di autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="53867-134">In the past there has been no standardized way of verifying a reference token with an authorization server.</span></span> <span data-ttu-id="53867-135">L'IETF, tuttavia, ha recentemente proposto e pubblicato lo standard [RFC 7662](https://tools.ietf.org/html/rfc7662) , che definisce le modalità con cui un server di risorse può verificare la validità di un token.</span><span class="sxs-lookup"><span data-stu-id="53867-135">However a recently proposed standard [RFC 7662](https://tools.ietf.org/html/rfc7662) was published by the IETF that defines how a resource server can verify the validity of a token.</span></span>

### <a name="extracting-the-token"></a><span data-ttu-id="53867-136">Estrazione del token</span><span class="sxs-lookup"><span data-stu-id="53867-136">Extracting the token</span></span>
<span data-ttu-id="53867-137">Il primo passaggio consiste nell'estrarre il token dall'intestazione di autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="53867-137">The first step is to extract the token from the Authorization header.</span></span> <span data-ttu-id="53867-138">Il valore dell'intestazione deve essere costituito dallo schema di autorizzazione `Bearer` , uno spazio singolo e il token di autorizzazione, in base allo standard [RFC 6750](http://tools.ietf.org/html/rfc6750#section-2.1).</span><span class="sxs-lookup"><span data-stu-id="53867-138">The header value should be formatted with the `Bearer` authorization scheme, a single space and then the authorization token as per [RFC 6750](http://tools.ietf.org/html/rfc6750#section-2.1).</span></span> <span data-ttu-id="53867-139">Purtroppo esistono casi in cui lo schema di autorizzazione viene omesso.</span><span class="sxs-lookup"><span data-stu-id="53867-139">Unfortunately there are cases where the authorization scheme is omitted.</span></span> <span data-ttu-id="53867-140">Per questo motivo, durante l'analisi il valore dell'intestazione viene suddiviso su uno spazio e viene selezionata l'ultima stringa dalla matrice di stringhe restituita.</span><span class="sxs-lookup"><span data-stu-id="53867-140">To account for this when parsing, we split the header value on a space and select the last string from the returned array of strings.</span></span> <span data-ttu-id="53867-141">Questa rappresenta una soluzione alternativa per le intestazioni di autorizzazione con formato non corretto.</span><span class="sxs-lookup"><span data-stu-id="53867-141">This provides a workaround for badly formatted authorization headers.</span></span>

```xml
<set-variable name="token" value="@(context.Request.Headers.GetValueOrDefault("Authorization","scheme param").Split(' ').Last())" />
```

### <a name="making-the-validation-request"></a><span data-ttu-id="53867-142">Invio della richiesta di convalida</span><span class="sxs-lookup"><span data-stu-id="53867-142">Making the validation request</span></span>
<span data-ttu-id="53867-143">Dopo aver ottenuto il token di autorizzazione, è possibile inviare la richiesta per la convalida del token.</span><span class="sxs-lookup"><span data-stu-id="53867-143">Once we have the authorization token, we can make the request to validate the token.</span></span> <span data-ttu-id="53867-144">Lo standard RFC 7662 definisce questa procedura introspezione e richiede che venga inviata una richiesta `POST` per un modulo HTML alla risorsa di introspezione.</span><span class="sxs-lookup"><span data-stu-id="53867-144">RFC 7662 calls this process introspection and requires that you `POST` a HTML form to the introspection resource.</span></span> <span data-ttu-id="53867-145">Il modulo HTML deve contenere almeno una coppia chiave/valore con la chiave `token`.</span><span class="sxs-lookup"><span data-stu-id="53867-145">The HTML form must at least contain a key/value pair with the key `token`.</span></span> <span data-ttu-id="53867-146">La richiesta al server di autorizzazione deve essere autenticata anche per assicurarsi che client non autorizzati non vengano passati come token validi.</span><span class="sxs-lookup"><span data-stu-id="53867-146">This request to the authorization server must also be authenticated to ensure that malicious clients cannot go trawling for valid tokens.</span></span>

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

### <a name="checking-the-response"></a><span data-ttu-id="53867-147">Verifica della risposta</span><span class="sxs-lookup"><span data-stu-id="53867-147">Checking the response</span></span>
<span data-ttu-id="53867-148">L'attributo `response-variable-name` viene usato per concedere l'accesso alla risposta restituita.</span><span class="sxs-lookup"><span data-stu-id="53867-148">The `response-variable-name` attribute is used to give access the returned response.</span></span> <span data-ttu-id="53867-149">Il nome definito in questa proprietà può essere usato come chiave nel dizionario `context.Variables` per accedere all'oggetto `IResponse`.</span><span class="sxs-lookup"><span data-stu-id="53867-149">The name defined in this property can be used as a key into the `context.Variables` dictionary to access the `IResponse` object.</span></span>

<span data-ttu-id="53867-150">Dall'oggetto della risposta è possibile recuperare il corpo e lo standard RFC 7622 indica che la risposta deve essere un oggetto JSON e deve contenere almeno una proprietà denominata `active` che rappresenta un valore booleano.</span><span class="sxs-lookup"><span data-stu-id="53867-150">From the response object we can retrieve the body and RFC 7622 tells us that the response must be a JSON object and must contain at least a property called `active` that is a boolean value.</span></span> <span data-ttu-id="53867-151">Se `active` è true, il token è considerato valido.</span><span class="sxs-lookup"><span data-stu-id="53867-151">When `active` is true then the token is considered valid.</span></span>

### <a name="reporting-failure"></a><span data-ttu-id="53867-152">Creazione di report sull'errore</span><span class="sxs-lookup"><span data-stu-id="53867-152">Reporting failure</span></span>
<span data-ttu-id="53867-153">Per individuare un token non valido, si usano i criteri `<choose>` e, in questo caso, viene restituita una risposta 401.</span><span class="sxs-lookup"><span data-stu-id="53867-153">We use a `<choose>` policy to detect if the token is invalid and if so, return a 401 response.</span></span>

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

<span data-ttu-id="53867-154">In base allo standard [RFC 6750](https://tools.ietf.org/html/rfc6750#section-3), in cui viene descritto come usare i token `bearer`, viene inoltre restituita un'intestazione `WWW-Authenticate` con la risposta 401.</span><span class="sxs-lookup"><span data-stu-id="53867-154">As per [RFC 6750](https://tools.ietf.org/html/rfc6750#section-3) which describes how `bearer` tokens should be used, we also return a `WWW-Authenticate` header with the 401 response.</span></span> <span data-ttu-id="53867-155">L'intestazione WWW-Authenticate è progettata per indicare a un client come realizzare una richiesta correttamente autorizzata.</span><span class="sxs-lookup"><span data-stu-id="53867-155">The WWW-Authenticate is intended to instruct a client on how to construct a properly authorized request.</span></span> <span data-ttu-id="53867-156">A causa dell'ampia gamma di approcci possibili con il framework di OAuth2, è difficile comunicare tutte le informazioni necessarie.</span><span class="sxs-lookup"><span data-stu-id="53867-156">Due to the wide variety of approaches possible with the OAuth2 framework, it is difficult to communicate all the needed information.</span></span> <span data-ttu-id="53867-157">Fortunatamente, sono disponibili soluzioni che consentono ai [client di definire le modalità per autorizzare correttamente le richieste a un server di risorse](http://tools.ietf.org/html/draft-jones-oauth-discovery-00).</span><span class="sxs-lookup"><span data-stu-id="53867-157">Fortunately there are efforts underway to help [clients discover how to properly authorize requests to a resource server](http://tools.ietf.org/html/draft-jones-oauth-discovery-00).</span></span>

### <a name="final-solution"></a><span data-ttu-id="53867-158">Soluzione finale</span><span class="sxs-lookup"><span data-stu-id="53867-158">Final solution</span></span>
<span data-ttu-id="53867-159">Combinando tutte le parti descritte, si ottengono i criteri seguenti:</span><span class="sxs-lookup"><span data-stu-id="53867-159">Putting all the pieces together, we get the following policy:</span></span>

```xml
<inbound>
  <!-- Extract Token from Authorization header parameter -->
  <set-variable name="token" value="@(context.Request.Headers.GetValueOrDefault("Authorization","scheme param").Split(' ').Last())" />

  <!-- Send request to Token Server to validate token (see RFC 7662) -->
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

<span data-ttu-id="53867-160">Questo è solo uno dei numerosi esempi che illustrano come usare i criteri `send-request` per integrare utili servizi esterni nel processo delle richieste e delle risposte che passano attraverso il servizio Gestione API.</span><span class="sxs-lookup"><span data-stu-id="53867-160">This is only one of many examples of how the `send-request` policy can be used to integrate useful external services into the process of requests and responses flowing through the API Management service.</span></span>

## <a name="response-composition"></a><span data-ttu-id="53867-161">Composizione della risposta</span><span class="sxs-lookup"><span data-stu-id="53867-161">Response Composition</span></span>
<span data-ttu-id="53867-162">I criteri `send-request` possono essere usati per l'ottimizzazione di una richiesta primaria a un sistema back-end, come illustrato nell'esempio precedente, oppure come sostituzione completa della chiamata al back-end.</span><span class="sxs-lookup"><span data-stu-id="53867-162">The `send-request` policy can be used for enhancing a primary request to a backend system, as we saw in the previous example, or it can be used as a complete replace for of the backend call.</span></span> <span data-ttu-id="53867-163">Questa tecnica consente di creare facilmente risorse composite che vengono aggregate da più sistemi.</span><span class="sxs-lookup"><span data-stu-id="53867-163">Using this technique we can easily create composite resources that are aggregated from multiple different systems.</span></span>

### <a name="building-a-dashboard"></a><span data-ttu-id="53867-164">Creazione di un dashboard</span><span class="sxs-lookup"><span data-stu-id="53867-164">Building a dashboard</span></span>
<span data-ttu-id="53867-165">A volte può essere utile saper esporre le informazioni presenti in più sistemi back-end, ad esempio, per creare un dashboard.</span><span class="sxs-lookup"><span data-stu-id="53867-165">Sometimes you want to be able to expose information that exists in multiple backend systems, for example, to drive a dashboard.</span></span> <span data-ttu-id="53867-166">Gli indicatori KPI provengono da diversi sistemi back-end, ma può essere opportuno evitare di fornire accesso diretto a questi ultimi e può essere utile recuperare tutte le informazioni in un'unica richiesta.</span><span class="sxs-lookup"><span data-stu-id="53867-166">The KPIs come from all different back-ends, but you would prefer not to provide direct access to them and it would be nice if all the information could be retrieved in a single request.</span></span> <span data-ttu-id="53867-167">Ad esempio, può essere innanzitutto necessario sezionare e ripulire alcune delle informazioni di back-end.</span><span class="sxs-lookup"><span data-stu-id="53867-167">Perhaps some of the backend information needs some slicing and dicing and a little sanitizing first!</span></span> <span data-ttu-id="53867-168">La possibilità di memorizzare nella cache tale risorsa complessa può essere utile per ridurre il carico del back-end, dato che gli utenti tendono a premere F5 per verificare se è possibile modificare le prestazioni limitate delle metriche.</span><span class="sxs-lookup"><span data-stu-id="53867-168">Being able to cache that composite resource would be a useful to reduce the backend load as you know users have a habit of hammering the F5 key in order to see if their underperforming metrics might change.</span></span>    

### <a name="faking-the-resource"></a><span data-ttu-id="53867-169">Simulazione della risorsa</span><span class="sxs-lookup"><span data-stu-id="53867-169">Faking the resource</span></span>
<span data-ttu-id="53867-170">Il primo passaggio per la creazione della risorsa dashboard consiste nella configurazione di una nuova operazione nel portale di pubblicazione di Gestione API.</span><span class="sxs-lookup"><span data-stu-id="53867-170">The first step to building our dashboard resource is to configure a new operation in the API Management publisher portal.</span></span> <span data-ttu-id="53867-171">Si tratta di un'operazione di segnaposto usata per configurare i criteri di composizione per creare la risorsa dinamica.</span><span class="sxs-lookup"><span data-stu-id="53867-171">This will be a placeholder operation used to configure our composition policy to build our dynamic resource.</span></span>

![Operazione dashboard](./media/api-management-sample-send-request/api-management-dashboard-operation.png)

### <a name="making-the-requests"></a><span data-ttu-id="53867-173">Invio delle richieste</span><span class="sxs-lookup"><span data-stu-id="53867-173">Making the requests</span></span>
<span data-ttu-id="53867-174">Dopo aver creato l'operazione `dashboard` , è possibile configurare criteri specifici per tale operazione.</span><span class="sxs-lookup"><span data-stu-id="53867-174">Once the `dashboard` operation has been created we can configure a policy specifically for that operation.</span></span> 

![Operazione dashboard](./media/api-management-sample-send-request/api-management-dashboard-policy.png)

<span data-ttu-id="53867-176">Il primo passaggio consiste nell'estrarre eventuali parametri di query dalla richiesta in ingresso, in modo da poterli inoltrare al back-end.</span><span class="sxs-lookup"><span data-stu-id="53867-176">The first step  is to extract any query parameters from the incoming request, so that we can forward them to our backend.</span></span> <span data-ttu-id="53867-177">In questo esempio il dashboard visualizza informazioni basate su un periodo di tempo e dispone quindi dei parametri `fromDate` e `toDate`.</span><span class="sxs-lookup"><span data-stu-id="53867-177">In this example our dashboard is showing information based on a period of time an therefore has a `fromDate` and `toDate` parameter.</span></span> <span data-ttu-id="53867-178">È possibile usare i criteri `set-variable` per estrarre le informazioni dall'URL della richiesta.</span><span class="sxs-lookup"><span data-stu-id="53867-178">We can use the `set-variable` policy to extract the information from the request URL.</span></span>

```xml
<set-variable name="fromDate" value="@(context.Request.Url.Query["fromDate"].Last())">
<set-variable name="toDate" value="@(context.Request.Url.Query["toDate"].Last())">
```

<span data-ttu-id="53867-179">Quando le informazioni sono disponibili, è possibile inviare le richieste a tutti i sistemi back-end.</span><span class="sxs-lookup"><span data-stu-id="53867-179">Once we have this information we can make requests to all the backend systems.</span></span> <span data-ttu-id="53867-180">Ogni richiesta crea un nuovo URL con le informazioni sul parametro, chiama il rispettivo server e archivia la risposta in una variabile di contesto.</span><span class="sxs-lookup"><span data-stu-id="53867-180">Each request constructs a new URL with the parameter information and calls its respective server and stores the response in a context variable.</span></span>

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

<span data-ttu-id="53867-181">Queste richieste vengono eseguite in sequenza, ma non si tratta della situazione ideale.</span><span class="sxs-lookup"><span data-stu-id="53867-181">These requests will execute in sequence, which is not ideal.</span></span> <span data-ttu-id="53867-182">In una versione futura verranno introdotti nuovi criteri denominati `wait` che consentiranno l'esecuzione in parallelo di tutte le richieste.</span><span class="sxs-lookup"><span data-stu-id="53867-182">In an upcoming release we will be introducing a new policy called `wait` that will enable all of these requests to execute in parallel.</span></span>

### <a name="responding"></a><span data-ttu-id="53867-183">Invio delle risposte</span><span class="sxs-lookup"><span data-stu-id="53867-183">Responding</span></span>
<span data-ttu-id="53867-184">Per costruire la risposta composita è possibile usare i criteri [return-response](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) .</span><span class="sxs-lookup"><span data-stu-id="53867-184">To construct the composite response we can use the [return-response](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) policy.</span></span> <span data-ttu-id="53867-185">L'elemento `set-body` può usare un'espressione per creare un nuovo oggetto `JObject` con tutte le rappresentazioni di componenti incorporate come proprietà.</span><span class="sxs-lookup"><span data-stu-id="53867-185">The `set-body` element can use an expression to construct a new `JObject` with all the component representations embedded as properties.</span></span>

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

<span data-ttu-id="53867-186">I criteri completi saranno simili ai seguenti:</span><span class="sxs-lookup"><span data-stu-id="53867-186">The complete policy looks as follows:</span></span>

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

<span data-ttu-id="53867-187">Nella configurazione dell'operazione segnaposto è possibile impostare la risorsa dashboard in modo che venga memorizzata nella cache per almeno un'ora, perché la natura dei dati implica che anche se scaduta, è comunque sufficientemente efficace per fornire informazioni utili agli utenti.</span><span class="sxs-lookup"><span data-stu-id="53867-187">In the configuration of the placeholder operation we can configure the dashboard resource to be cached for at least an hour because we understand the nature of the data means that even if it is an hour out of date, it will still be sufficiently effective to convey valuable information to the users.</span></span>

## <a name="summary"></a><span data-ttu-id="53867-188">Summary</span><span class="sxs-lookup"><span data-stu-id="53867-188">Summary</span></span>
<span data-ttu-id="53867-189">Il servizio Gestione API di Azure offre criteri flessibili che possono essere applicati in modo selettivo al traffico HTTP e consentono la realizzazione di servizi back-end.</span><span class="sxs-lookup"><span data-stu-id="53867-189">Azure API Management service provides flexible policies that can be selectively applied to HTTP traffic and enables composition of backend services.</span></span> <span data-ttu-id="53867-190">Se si desidera migliorare il gateway API con funzioni di avviso, verifica e convalida o creare nuove risorse complesse basate su più servizi back-end, `send-request` e i criteri correlati offrono numerose possibilità.</span><span class="sxs-lookup"><span data-stu-id="53867-190">Whether you want to enhance your API gateway with alerting functions, verification, validation capabilities or create new composite resources based on multiple backend services, the `send-request` and related policies open a world of possibilities.</span></span>

## <a name="watch-a-video-overview-of-these-policies"></a><span data-ttu-id="53867-191">Video contenente una panoramica di questi criteri</span><span class="sxs-lookup"><span data-stu-id="53867-191">Watch a video overview of these policies</span></span>
<span data-ttu-id="53867-192">Per altre informazioni sui criteri [send-one-way-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest), [send-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) e [return-response](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) presentati in questo articolo, guardare il video seguente.</span><span class="sxs-lookup"><span data-stu-id="53867-192">For more information on the [send-one-way-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest), [send-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest), and [return-response](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) policies covered in this article, please watch the following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Send-Request-and-Return-Response-Policies/player]
> 
> 

