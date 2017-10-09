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
# <a name="using-external-services-from-hello-azure-api-management-service"></a>Tramite servizi esterni da hello servizio Gestione API di Azure
criteri di Hello disponibili nel servizio di gestione API di Azure è possono eseguire un'ampia gamma di operazioni utili basata esclusivamente sul richiesta in ingresso hello, la risposta in uscita hello e informazioni di configurazione di base. Tuttavia, essere in grado di toointeract con i servizi esterni da Gestione API criteri apre molti più opportunità.

Abbiamo già visto come poter interagire con hello [servizio Hub di eventi di Azure per la registrazione, il monitoraggio e analitica](api-management-log-to-eventhub-sample.md). In questo articolo verrà illustrato servizio basato su criteri che consentono di toointeract con qualsiasi HTTP esterno. Questi criteri possono essere usati per l'attivazione di eventi remoti o per il recupero di informazioni che saranno utilizzati toomanipulate hello originale richiesta e la risposta in qualche modo.

## <a name="send-one-way-request"></a>Send-One-Way-Request
Probabilmente hello interazione esterno più semplice è hello fire-and-forget lo stile della richiesta che consente a un servizio esterno di toobe una notifica di un tipo di evento importante. È possibile utilizzare criteri di flusso di controllo hello `choose` toodetect qualsiasi tipo di condizione che si è interessati e se hello condizione è soddisfatta, è possibile rendere una richiesta HTTP esterna utilizzando hello [richiesta unidirezionale di una trasmissione](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) criteri. Potrebbe trattarsi di una richiesta tooa sistema come Hipchat o Slack o un messaggio di posta API SendGrid o MailChimp di messaggistica, o per gli eventi imprevisti supporto critico qualcosa di simile a PagerDuty. Tutti questi sistemi di messaggistica dispongono di API HTTP semplici che possono essere richiamate facilmente.

### <a name="alerting-with-slack"></a>Avvisi con Slack
Hello di esempio seguente viene illustrato come toosend tooa un messaggio margine di flessibilità di chat se il codice di stato di risposta HTTP hello è maggiore o uguale a too500. Un errore di 500 intervallo indica un problema con l'API di back-end che hello client dell'API non è possibile risolvere autonomamente. In genere richiede un intervento da parte dell'utente.  

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

Slack è nozione hello di hook web in ingresso. Quando si configura un hook web in ingresso, il margine di flessibilità genera un URL speciale che consente una semplice richiesta POST toodo e toopass un messaggio nel canale di Slack hello. Hello corpo JSON, creata è basata su un formato definito da Slack.

![Hook Web di Slack](./media/api-management-sample-send-request/api-management-slack-webhook.png)

### <a name="is-fire-and-forget-good-enough"></a>Lo stile di richiesta fire-and-forget è sufficientemente efficace?
Quando si usa uno stile di richiesta fire-and-forget è necessario tenere presenti alcuni svantaggi. Se per qualche motivo, hello richiesta ha esito negativo, quindi non verrà segnalato un errore di hello. In questo caso particolare, non sono garantite complessità hello di disporre di un sistema di segnalazione errori secondario e il costo di prestazioni hello di in attesa di risposta hello. Per gli scenari in cui è risposta hello toocheck essenziali, hello [richiesta di invio](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) criteri sono un'opzione migliore.

## <a name="send-request"></a>send-request
Hello `send-request` criteri consente l'uso di un servizio esterno di tooperform complesse funzioni e servizio di gestione toohello API restituisce i dati che può essere utilizzato per un'ulteriore elaborazione di criteri di elaborazione.

### <a name="authorizing-reference-tokens"></a>Autorizzazione di token di riferimento
Una funzione fondamentale di Gestione API è la protezione delle risorse back-end. Se il server di autorizzazione hello utilizzato per l'API crea [i token JWT](http://jwt.io/) come parte del relativo flusso OAuth2, come [Azure Active Directory](../active-directory/active-directory-aadconnect.md) avviene, è possibile utilizzare hello `validate-jwt` validità hello tooverify di criteri di token Hello. Tuttavia, alcuni server di autorizzazione creare cosiddetti [fanno riferimento a token](http://leastprivilege.com/2015/11/25/reference-tokens-and-introspection/) che non è possibile verificare senza un server di autorizzazione toohello indietro di chiamata.

### <a name="standardized-introspection"></a>Introspezione standardizzata
In hello precedente non si è verificato alcun modo standardizzato verificare se un token di riferimento con un server di autorizzazione. Tuttavia recentemente proposta di standard [7662 RFC](https://tools.ietf.org/html/rfc7662) ha pubblicato hello IETF che definisce come un server delle risorse può verificare la validità hello di un token.

### <a name="extracting-hello-token"></a>L'estrazione dei token hello
primo passaggio Hello è token hello tooextract dall'intestazione di autorizzazione hello. valore dell'intestazione Hello deve essere formattato con hello `Bearer` lo schema di autorizzazione, un singolo spazio e quindi autorizzazione hello token in base [RFC 6750](http://tools.ietf.org/html/rfc6750#section-2.1). Vi sono casi in cui lo schema di autorizzazione hello è omesso. tooaccount per questo durante l'analisi, verranno suddivise valore dell'intestazione hello in uno spazio e stringa ultimo hello selezionare hello ha restituito una matrice di stringhe. Questa rappresenta una soluzione alternativa per le intestazioni di autorizzazione con formato non corretto.

```xml
<set-variable name="token" value="@(context.Request.Headers.GetValueOrDefault("Authorization","scheme param").Split(' ').Last())" />
```

### <a name="making-hello-validation-request"></a>Richiesta di convalida hello
Una volta ottenuto il token di autorizzazione hello, è possibile rendere i token di hello richiesta toovalidate hello. RFC 7662 chiama introspezione questo processo e richiede che si `POST` una risorsa di introspezione toohello di form HTML. Hello form HTML deve contenere almeno una coppia chiave/valore con chiave hello `token`. Questo server di autorizzazione toohello richiesta deve essere autenticato tooensure che client dannosi non è possibile passare dovuti per i token validi.

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

### <a name="checking-hello-response"></a>Controllo risposta hello
Hello `response-variable-name` attributo è usato toogive hello di accesso ha restituito una risposta. Hello nome definito in questa proprietà può essere utilizzato come chiave in hello `context.Variables` hello tooaccess dizionario `IResponse` oggetto.

Oggetto risposta hello è possibile recuperare il corpo di hello e RFC 7622 indica che la risposta hello deve essere un oggetto JSON e deve contenere almeno una proprietà denominata `active` che rappresenta un valore booleano. Quando `active` è true, il token hello è considerato valido.

### <a name="reporting-failure"></a>Creazione di report sull'errore
Utilizziamo un `<choose>` toodetect criteri se hello token non è valido e in tal caso, restituire una risposta 401.

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

In base [RFC 6750](https://tools.ietf.org/html/rfc6750#section-3) che descrive come `bearer` token devono essere utilizzati, anche restituiamo un `WWW-Authenticate` intestazione risposta hello 401. Hello WWW-Authenticate è previsto tooinstruct un client come tooconstruct una richiesta autorizzata correttamente. A causa di toohello vasta gamma di metodi possibili con framework hello OAuth2, risulta difficile toocommunicate tutti hello informazioni necessarie. Per fortuna sono presenti attività in corso toohelp [client individuare come tooproperly autorizzare i server delle risorse richieste tooa](http://tools.ietf.org/html/draft-jones-oauth-discovery-00).

### <a name="final-solution"></a>Soluzione finale
Combinazione di tutti i componenti di hello, si ottiene hello seguenti criteri:

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

Questo è solo uno dei molti esempi di come hello `send-request` criteri possono essere utilizzati toointegrate servizi esterni utili nel processo di hello di richieste e risposte che passano attraverso il servizio Gestione API hello.

## <a name="response-composition"></a>Composizione della risposta
Hello `send-request` criteri possono essere utilizzati per l'ottimizzazione di un sistema back-end tooa richiesta primaria, come illustrato nell'esempio precedente hello, oppure può essere utilizzato come una sostituzione completa della chiamata di hello back-end. Questa tecnica consente di creare facilmente risorse composite che vengono aggregate da più sistemi.

### <a name="building-a-dashboard"></a>Creazione di un dashboard
Talvolta toobe tooexpose in grado di informazioni che esiste in più sistemi back-end, ad esempio, toodrive un dashboard. gli indicatori KPI Hello provengono da tutti i diversi sistemi back-end, ma si preferisce non tooprovide l'accesso diretto toothem e sarebbe utile se è stato possibile recuperare tutte le informazioni di hello in una singola richiesta. Ad esempio alcune delle informazioni di back-end hello necessita di alcuni sezionamento e trasformando e un po' la purificazione degli prima! Essere in grado di toocache tale risorsa composita sarà un utile tooreduce back-end hello caricare come descritto in precedenza gli utenti hanno l'abitudine di hammering tasto F5 hello in ordine toosee se le metriche underperforming potrebbero cambiare.    

### <a name="faking-hello-resource"></a>Falsificare risorse hello
primo passaggio toobuilding Hello la risorsa dashboard sia tooconfigure una nuova operazione nel portale di pubblicazione di gestione API hello. Questo sarà un tooconfigure operazione utilizzata segnaposto nostri toobuild criteri composizione alla risorsa dinamica.

![Operazione dashboard](./media/api-management-sample-send-request/api-management-dashboard-operation.png)

### <a name="making-hello-requests"></a>Effettua richieste hello
Una volta hello `dashboard` è stata creata l'operazione è possibile configurare un criterio per l'operazione. 

![Operazione dashboard](./media/api-management-sample-send-request/api-management-dashboard-policy.png)

primo passaggio Hello è tooextract eventuali parametri di query hello richiesta in ingresso, in modo che possiamo inoltrarli tooour di back-end. In questo esempio il dashboard visualizza informazioni basate su un periodo di tempo e dispone quindi dei parametri `fromDate` e `toDate`. È possibile utilizzare hello `set-variable` criteri tooextract hello informazioni hello URL della richiesta.

```xml
<set-variable name="fromDate" value="@(context.Request.Url.Query["fromDate"].Last())">
<set-variable name="toDate" value="@(context.Request.Url.Query["toDate"].Last())">
```

Una volta che queste informazioni è possibile rendere i sistemi back-end di hello tooall richieste. Ogni richiesta crea un nuovo URL con informazioni sul parametro hello e chiama rispettivo server e archivia la risposta hello in una variabile di contesto.

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

Queste richieste vengono eseguite in sequenza, ma non si tratta della situazione ideale. In una versione futura è verrà introdotto un nuovo criterio denominato `wait` che consentirà di tutti questi tooexecute le richieste in parallelo.

### <a name="responding"></a>Invio delle risposte
risposta composito hello tooconstruct possiamo utilizzare hello [restituito risposta](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) criteri. Hello `set-body` elemento è possibile utilizzare un'espressione tooconstruct un nuovo `JObject` con tutte le rappresentazioni di componente hello incorporate come proprietà.

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

criteri completa Hello è simile al seguente:

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

Nella configurazione di hello dell'operazione di segnaposto hello che è possibile configurare hello dashboard risorse toobe memorizzato nella cache per almeno un'ora perché è comprendere la natura hello dei dati hello significa che anche se si tratta di un'ora aggiornata, che sarà comunque sufficientemente efficace utenti di tooconvey preziosi toohello.

## <a name="summary"></a>Riepilogo
Servizio gestione API di Azure fornisce criteri flessibili che possono essere in modo selettivo applicato tooHTTP traffico e consente di composizione di servizi back-end. Se si desidera che il gateway API con avvisi di funzioni, la verifica, la funzionalità di convalida tooenhance o creano nuove risorse composite in base a più servizi back-end, hello `send-request` e criteri correlati aprire un mondo di possibilità.

## <a name="watch-a-video-overview-of-these-policies"></a>Video contenente una panoramica di questi criteri
Per ulteriori informazioni su hello [richiesta unidirezionale di una trasmissione](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest), [richiesta di invio](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest), e [restituito risposta](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) criteri descritti in questo articolo, guardare hello video seguenti.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Send-Request-and-Return-Response-Policies/player]
> 
> 

