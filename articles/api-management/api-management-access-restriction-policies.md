---
title: criteri di restrizione accesso Gestione API aaaAzure | Documenti Microsoft
description: Informazioni sui criteri di restrizione accesso hello disponibili per l'utilizzo in Gestione API di Azure.
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 034febe3-465f-4840-9fc6-c448ef520b0f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 0ef368c2781d9a5cf9eaaa41a47489c904ed3198
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-access-restriction-policies"></a>Criteri di limitazione dell'accesso di Gestione API
In questo argomento fornisce un riferimento per i seguenti criteri di gestione API hello. Per informazioni sull'aggiunta e sulla configurazione dei criteri, vedere [Criteri di Gestione API](http://go.microsoft.com/fwlink/?LinkID=398186).  
  
##  <a name="AccessRestrictionPolicies"></a> Criteri di limitazione dell'accesso  
  
-   [check-header](api-management-access-restriction-policies.md#CheckHTTPHeader) : impone l'esistenza e/o il valore di un'intestazione HTTP.  
  
-   [Limita frequenza delle chiamate per sottoscrizione](api-management-access-restriction-policies.md#LimitCallRate) : impedisce picchi di utilizzo delle API limitando la frequenza delle chiamate per ogni sottoscrizione.  
  
-   [Limita frequenza delle chiamate per chiave](#LimitCallRateByKey) : impedisce picchi di utilizzo delle API limitando la frequenza delle chiamata, per ogni chiave.  
  
-   [ip-filter](api-management-access-restriction-policies.md#RestrictCallerIPs) : filtra (permette/rifiuta) le chiamate provenienti da indirizzi IP e/o intervalli di indirizzi IP specifici.  
  
-   [Quota di utilizzo di set da sottoscrizione](api-management-access-restriction-policies.md#SetUsageQuota) -consente tooenforce una quota rinnovabile o permanente chiamata volume e/o della larghezza di banda, in base a una per ogni sottoscrizione.  
  
-   [Quota di utilizzo di set da chiave](#SetUsageQuotaByKey) -consente tooenforce una quota rinnovabile o permanente chiamata volume e/o della larghezza di banda, in una base per ogni chiave.  
  
-   [validate-JWT](api-management-access-restriction-policies.md#ValidateJWT) : impone l'esistenza e la validità di un token JWT estratto da un'intestazione HTTP specificata o da un parametro di query specificato.  
  
##  <a name="CheckHTTPHeader"></a> Intestazione check-header  
 Hello utilizzare `check-header` tooenforce criteri che una richiesta presenta un'intestazione HTTP specificata. È possibile controllare toosee se intestazione hello ha un valore specifico o per un intervallo di valori consentiti. Se il controllo di hello non riesce, criteri hello termina l'elaborazione della richiesta e restituisce hello codice di errore e messaggio di stato HTTP specificato dai criteri di hello.  
  
### <a name="policy-statement"></a>Istruzione del criterio  
  
```xml  
<check-header name="header name" failed-check-httpcode="code" failed-check-error-message="message" ignore-case="True">  
    <value>Value1</value>  
    <value>Value2</value>  
</check-header>  
```  
  
### <a name="example"></a>Esempio  
  
```xml  
<check-header name="Authorization" failed-check-httpcode="401" failed-check-error-message="Not authorized" ignore-case="false">  
    <value>f6dc69a089844cf6b2019bae6d36fac8</value>  
</check-header>  
```  
  
### <a name="elements"></a>Elementi  
  
|Nome|Descrizione|Obbligatorio|  
|----------|-----------------|--------------|  
|check-header|Elemento radice.|Sì|  
|value|Valore dell'intestazione HTTP consentito. Quando vengono specificati più elementi di valore, controllo hello viene considerato un caso di esito positivo se uno dei valori hello è una corrispondenza.|No|  
  
### <a name="attributes"></a>Attributi  
  
|Nome|Descrizione|Obbligatorio|Default|  
|----------|-----------------|--------------|-------------|  
|failed-check-error-message|Tooreturn messaggio di errore nel corpo della risposta HTTP hello se l'intestazione di hello non esiste o non ha un valore non valido. I caratteri speciali eventualmente contenuti in questo messaggio devono essere adeguatamente preceduti da un carattere di escape.|Sì|N/D|  
|failed-check-httpcode|Codice di stato HTTP tooreturn se l'intestazione di hello non esiste o non ha un valore non valido.|Sì|N/D|  
|header-name|nome Hello di hello toocheck intestazione HTTP.|Sì|N/D|  
|ignore-case|Può essere impostato tooTrue o False. Se il case tooTrue set viene ignorato quando il valore di intestazione hello viene confrontato con il set di hello di valori accettabili.|Sì|N/D|  
  
### <a name="usage"></a>Utilizzo  
 Questo criterio può essere utilizzato hello seguenti criteri [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sezioni del criterio:** inbound, outbound  
  
-   **Ambiti del criterio:** globale, prodotto, API, operazione  
  
##  <a name="LimitCallRate"></a> Limita frequenza delle chiamate per sottoscrizione  
 Hello `rate-limit` criteri impediscono l'utilizzo di API picchi in una per ogni singola sottoscrizione limitando hello chiamare tooa di frequenza specificato numero per un periodo di tempo specificato. Quando viene attivato il criterio chiamante hello riceve un `429 Too Many Requests` codice di stato della risposta.  
  
> [!IMPORTANT]
>  Questo criterio può essere impiegato una sola volta per ogni documento dei criteri.  
>   
>  [Espressioni di criteri](api-management-policy-expressions.md) non può essere usata in qualsiasi degli attributi di hello criteri per i criteri.  
  
### <a name="policy-statement"></a>Istruzione del criterio  
  
```xml  
<rate-limit calls="number" renewal-period="seconds">  
    <api name="name" calls="number" renewal-period="seconds">  
        <operation name="name" calls="number" renewal-period="seconds" />  
    </api>  
</rate-limit>  
```  
  
### <a name="example"></a>Esempio  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <rate-limit calls="20" renewal-period="90" />  
    </inbound>  
    <outbound>  
        <base />          
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a>Elementi  
  
|Nome|Descrizione|Obbligatorio|  
|----------|-----------------|--------------|  
|set-limit|Elemento radice.|Sì|  
|api|Aggiungere uno o più di questi tooimpose elementi un limite di frequenza delle chiamate alle API all'interno del prodotto hello. I limiti alla frequenza delle chiamate API e al prodotto vengono applicati in modo indipendente.|No|  
|operation|Aggiungere uno o più di questi tooimpose elementi un limite di frequenza delle chiamate per le operazioni in un'API. I limiti alla frequenza delle chiamate alle operazioni, all'API e al prodotto vengono applicati in modo indipendente.|No|  
  
### <a name="attributes"></a>Attributi  
  
|Nome|Descrizione|Obbligatorio|Default|  
|----------|-----------------|--------------|-------------|  
|name|nome di Hello di hello API per il limite di velocità tooapply hello.|Sì|N/D|  
|calls|numero massimo di chiamate consentite durante l'intervallo di tempo hello specificato in hello Hello `renewal-period`.|Sì|N/D|  
|renewal-period|Hello periodo di tempo in secondi dopo il quale hello quota viene reimpostata.|Sì|N/D|  
  
### <a name="usage"></a>Utilizzo  
 Questo criterio può essere utilizzato hello seguenti criteri [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sezioni del criterio:** inbound  
  
-   **Ambiti del criterio:** prodotto  
  
##  <a name="LimitCallRateByKey"></a> Limita la frequenza delle chiamate per chiave  
 Hello `rate-limit-by-key` criteri impediscono l'utilizzo di API picchi di base per ogni chiave limitando hello chiamare tooa di frequenza specificato numero per un periodo di tempo specificato. chiave di Hello può avere un valore stringa arbitrario e viene in genere fornito con un'espressione di criteri. È possibile aggiungere toospecify le richieste devono essere conteggiate per limite hello condizione incrementale facoltativo. Quando viene attivato il criterio chiamante hello riceve un `429 Too Many Requests` codice di stato della risposta.  
  
 Per altre informazioni ed esempi su questo criterio, vedere [Advanced request throttling with Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/) (Limitazione avanzata delle richieste con Gestione API di Azure).  
  
> [!IMPORTANT]
>  Questo criterio può essere impiegato una sola volta per ogni documento dei criteri.  
  
### <a name="policy-statement"></a>Istruzione del criterio  
  
```xml  
<rate-limit-by-key calls="number"  
                   renewal-period="seconds"   
                   increment-condition="condition"   
                   counter-key="key value" />  
  
```  
  
### <a name="example"></a>Esempio  
 Nel seguente esempio di hello, il limite di velocità di hello è codificato in base all'indirizzo IP hello chiamante.  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <rate-limit-by-key  calls="10"  
              renewal-period="60"  
              increment-condition="@(context.Response.StatusCode == 200)"  
              counter-key="@(context.Request.IpAddress)"/>  
    </inbound>  
    <outbound>  
        <base />          
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a>Elementi  
  
|Nome|Descrizione|Obbligatorio|  
|----------|-----------------|--------------|  
|set-limit|Elemento radice.|Sì|  
  
### <a name="attributes"></a>Attributi  
  
|Nome|Descrizione|Obbligatorio|Default|  
|----------|-----------------|--------------|-------------|  
|calls|numero massimo di chiamate consentite durante l'intervallo di tempo hello specificato in hello Hello `renewal-period`.|Sì|N/D|  
|counter-key|Hello toouse chiave per i criteri di limite di frequenza hello.|Sì|N/D|  
|increment-condition|espressione di Hello booleana che specifica se la richiesta hello conteggiata quota hello (`true`).|No|N/D|  
|renewal-period|Hello periodo di tempo in secondi dopo il quale hello quota viene reimpostata.|Sì|N/D|  
  
### <a name="usage"></a>Utilizzo  
 Questo criterio può essere utilizzato hello seguenti criteri [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sezioni del criterio:** inbound  
  
-   **Ambiti del criterio:** globale, prodotto, API, operazione  
  
##  <a name="RestrictCallerIPs"></a> ip-filter  
 Hello `ip-filter` criteri Filtra (consente/Rifiuta) le chiamate da indirizzi IP specifici e/o intervalli di indirizzi.  
  
### <a name="policy-statement"></a>Istruzione del criterio  
  
```xml  
<ip-filter action="allow | forbid">  
    <address>address</address>  
    <address-range from="address" to="address" />  
</ip-filter>  
```  
  
### <a name="example"></a>Esempio  
  
```xml  
<ip-filter action="allow | forbid">  
    <address>address</address>  
    <address-range from="address" to="address" />  
</ip-filter>  
```  
  
### <a name="elements"></a>Elementi  
  
|Nome|Descrizione|Obbligatorio|  
|----------|-----------------|--------------|  
|ip-filter|Elemento radice.|Sì|  
|Address|Specifica un singolo indirizzo IP su cui toofilter.|È obbligatorio almeno un elemento `address` o `address-range`.|  
|address-range from="address" to="address"|Specifica un intervallo di indirizzi IP in quale toofilter.|È obbligatorio almeno un elemento `address` o `address-range`.|  
  
### <a name="attributes"></a>Attributi  
  
|Nome|Descrizione|Obbligatorio|Default|  
|----------|-----------------|--------------|-------------|  
|address-range from="address" to="address"|Un intervallo di indirizzi IP, indirizzi tooallow o negare l'accesso.|Obbligatorio quando hello `address-range` viene utilizzato l'elemento.|N/D|  
|ip-filter action="allow &#124; forbid"|Specifica se le chiamate devono essere consentite o non per hello specificato gli indirizzi IP e gli intervalli.|Sì|N/D|  
  
### <a name="usage"></a>Utilizzo  
 Questo criterio può essere utilizzato hello seguenti criteri [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sezioni del criterio:** inbound  
  
-   **Ambiti del criterio:** globale, prodotto, API, operazione  
  
##  <a name="SetUsageQuota"></a> Imposta quota di utilizzo per sottoscrizione  
 Hello `quota` criteri consentono di applicare una quota rinnovabile o permanente chiamata volume e/o della larghezza di banda, in base a una per ogni sottoscrizione.  
  
> [!IMPORTANT]
>  Questo criterio può essere impiegato una sola volta per ogni documento dei criteri.  
>   
>  [Espressioni di criteri](api-management-policy-expressions.md) non può essere usata in qualsiasi degli attributi di hello criteri per i criteri.  
  
### <a name="policy-statement"></a>Istruzione del criterio  
  
```xml  
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">  
    <api name="name" calls="number" bandwidth="kilobytes">  
        <operation name="name" calls="number" bandwidth="kilobytes" />  
    </api>  
</quota>  
```  
  
### <a name="example"></a>Esempio  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <quota calls="10000" bandwidth="40000" renewal-period="3600" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a>Elementi  
  
|Nome|Descrizione|Obbligatorio|  
|----------|-----------------|--------------|  
|quota|Elemento radice.|Sì|  
|api|Aggiungere uno o più di questi tooimpose elementi una quota sulle API nel prodotto hello. Le quote delle API e del prodotto vengono applicate in modo indipendente.|No|  
|operation|Aggiungere uno o più di questi tooimpose elementi una quota per le operazioni in un'API. Le quote delle operazioni, delle API e del prodotto vengono applicate in modo indipendente.|No|  
  
### <a name="attributes"></a>Attributi  
  
|Nome|Descrizione|Obbligatorio|Default|  
|----------|-----------------|--------------|-------------|  
|name|nome Hello di hello API o operazione per cui hello quota si applica.|Sì|N/D|  
|bandwidth|numero massimo totale di kilobyte consentiti nell'intervallo di tempo hello specificato in hello Hello `renewal-period`.|Devono essere specificati `calls`, `bandwidth` o entrambi.|N/D|  
|calls|numero massimo di chiamate consentite durante l'intervallo di tempo hello specificato in hello Hello `renewal-period`.|Devono essere specificati `calls`, `bandwidth` o entrambi.|N/D|  
|renewal-period|Hello periodo di tempo in secondi dopo il quale hello quota viene reimpostata.|Sì|N/D|  
  
### <a name="usage"></a>Utilizzo  
 Questo criterio può essere utilizzato hello seguenti criteri [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sezioni del criterio:** inbound  
  
-   **Ambiti del criterio:** prodotto  
  
##  <a name="SetUsageQuotaByKey"></a> Impostare la quota per chiave  
 Hello `quota-by-key` criteri consentono di applicare una quota rinnovabile o permanente chiamata volume e/o della larghezza di banda, in una base per ogni chiave. chiave di Hello può avere un valore stringa arbitrario e viene in genere fornito con un'espressione di criteri. È possibile aggiungere toospecify le richieste devono essere conteggiate quota hello condizione incrementale facoltativo.  
  
 Per altre informazioni ed esempi su questo criterio, vedere [Advanced request throttling with Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/) (Limitazione avanzata delle richieste con Gestione API di Azure).  
  
> [!IMPORTANT]
>  Questo criterio può essere impiegato una sola volta per ogni documento dei criteri.  
>   
>  [Espressioni di criteri](api-management-policy-expressions.md) non può essere usata in qualsiasi degli attributi di hello criteri per i criteri.  
  
### <a name="policy-statement"></a>Istruzione del criterio  
  
```xml  
<quota-by-key calls="number"   
              bandwidth="kilobytes"   
              renewal-period="seconds"  
              increment-condition="condition"   
              counter-key="key value" />  
  
```  
  
### <a name="example"></a>Esempio  
 Nell'esempio seguente di hello, quota hello è codificato in base all'indirizzo IP hello chiamante.  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <quota-by-key calls="10000" bandwidth="40000" renewal-period="3600"  
                      increment-condition="@(context.Response.StatusCode >= 200 && context.Response.StatusCode < 400)"  
                      counter-key="@(context.Request.IpAddress)" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a>Elementi  
  
|Nome|Descrizione|Obbligatorio|  
|----------|-----------------|--------------|  
|quota|Elemento radice.|Sì|  
  
### <a name="attributes"></a>Attributi  
  
|Nome|Descrizione|Obbligatorio|Default|  
|----------|-----------------|--------------|-------------|  
|bandwidth|numero massimo totale di kilobyte consentiti nell'intervallo di tempo hello specificato in hello Hello `renewal-period`.|Devono essere specificati `calls`, `bandwidth` o entrambi.|N/D|  
|calls|numero massimo di chiamate consentite durante l'intervallo di tempo hello specificato in hello Hello `renewal-period`.|Devono essere specificati `calls`, `bandwidth` o entrambi.|N/D|  
|counter-key|Hello toouse chiave per il criterio di quota hello.|Sì|N/D|  
|increment-condition|espressione di Hello booleana che specifica se la richiesta hello conteggiata quota hello (`true`)|No|N/D|  
|renewal-period|Hello periodo di tempo in secondi dopo il quale hello quota viene reimpostata.|Sì|N/D|  
  
### <a name="usage"></a>Utilizzo  
 Questo criterio può essere utilizzato hello seguenti criteri [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sezioni del criterio:** inbound  
  
-   **Ambiti del criterio:** globale, prodotto, API, operazione  
  
##  <a name="ValidateJWT"></a> Convalida token JWT  
 Hello `validate-jwt` criteri impone l'esistenza e validità di un token JWT estratto da un oggetto intestazione HTTP o un parametro di query specificato.  
  
> [!IMPORTANT]
>  Hello `validate-jwt` criteri richiedono tale hello `exp` attestazione registrato è presente nel token JWT hello, a meno che non `require-expiration-time` attributo viene specificato e impostato troppo`false`.  
> Hello `validate-jwt` criteri supporta gli algoritmi di firma HS256 e RS256. Per HS256 chiave hello è necessario specificare inline nel criterio di hello in formato con codificata base64 hello. Per RS256 chiave hello ha toobe fornire tramite un endpoint di configurazione Openid.  
  
### <a name="policy-statement"></a>Istruzione del criterio  
  
```xml  
<validate-jwt   
    header-name="name of http header containing hello token (use query-parameter-name attribute if hello token is passed in hello URL)"   
    failed-validation-httpcode="http status code tooreturn on failure"   
    failed-validation-error-message="error message tooreturn on failure"   
    require-expiration-time="true|false"
    require-scheme="scheme"
    require-signed-tokens="true|false"   
    clock-skew="allowed clock skew in seconds">  
  <issuer-signing-keys>  
    <key>base64 encoded signing key</key>  
    <!-- if there are multiple keys, then add additional key elements -->  
  </issuer-signing-keys>  
  <audiences>  
    <audience>audience string</audience>  
    <!-- if there are multiple possible audiences, then add additional audience elements -->  
  </audiences>  
  <issuers>  
    <issuer>issuer string</issuer>  
    <!-- if there are multiple possible issuers, then add additional issuer elements -->  
  </issuers>  
  <required-claims>  
    <claim name="name of hello claim as it appears in hello token" match="all|any">  
      <value>claim value as it is expected tooappear in hello token</value>  
      <!-- if there is more than one allowed values, then add additional value elements -->  
    </claim>  
    <!-- if there are multiple possible allowed values, then add additional value elements -->  
  </required-claims>  
  <openid-config url="full URL of hello configuration endpoint, e.g. https://login.constoso.com/openid-configuration" />  
  <zumo-master-key id="key identifier">key value</zumo-master-key>  
</validate-jwt>  
  
```  
  
### <a name="examples"></a>Esempi  
  
#### <a name="azure-mobile-services-token-validation"></a>Convalida del token dei Servizi mobili di Azure  
  
```xml  
<validate-jwt header-name="x-zumo-auth" failed-validation-httpcode="401" failed-validation-error-message="Unauthorized. Supplied access token is invalid.">  
    <issuers>  
        <issuer>urn:microsoft:windows-azure:zumo</issuer>  
    </issuers>  
    <audiences>  
        <audience>Facebook</audience>  
    </audiences>  
    <issuer-signing-keys>  
        <zumo-master-key id="0">insert key here</zumo-master-key>  
    </issuer-signing-keys>  
</validate-jwt>  
```  
  
#### <a name="azure-active-directory-token-validation"></a>Convalida del token di Azure Active Directory  
  
```xml  
<validate-jwt header-name="Authorization" failed-validation-httpcode="401" failed-validation-error-message="Unauthorized. Access token is missing or invalid.">  
    <openid-config url="https://login.microsoftonline.com/contoso.onmicrosoft.com/.well-known/openid-configuration" />  
    <audiences>
        <audience>25eef6e4-c905-4a07-8eb4-0d08d5df8b3f</audience>
    </audiences>
    <required-claims>  
        <claim name="id" match="all">  
            <value>insert claim here</value>  
        </claim>  
    </required-claims>  
</validate-jwt>  
```  

  
#### <a name="azure-active-directory-b2c-token-validation"></a>Convalida del token di Azure Active Directory B2C  
  
```xml  
<validate-jwt header-name="Authorization" failed-validation-httpcode="401" failed-validation-error-message="Unauthorized. Access token is missing or invalid.">  
    <openid-config url="https://login.microsoftonline.com/tfp/contoso.onmicrosoft.com/b2c_1_signin/v2.0/.well-known/openid-configuration" />
    <audiences>
        <audience>d313c4e4-de5f-4197-9470-e509a2f0b806</audience>
    </audiences>
    <required-claims>  
        <claim name="id" match="all">  
            <value>insert claim here</value>  
        </claim>  
    </required-claims>  
</validate-jwt>  
```  
  
#### <a name="authorize-access-toooperations-based-on-token-claims"></a>Autorizzare l'accesso toooperations basata sulle attestazioni di token  
 Questo esempio viene illustrato come hello toouse [convalidare JWT](api-management-access-restriction-policies.md#ValidateJWT) toopre criteri-autorizzare l'accesso toooperations basata sulle attestazioni di token. Per una dimostrazione della configurazione e l'utilizzo di questo criterio, vedere [Cloud coprire episodio 177: più API le funzionalità di gestione con Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) e far avanzare rapidamente too13:50. Avanzamento rapido too15:00 criteri hello toosee configurati nell'editor Criteri di hello e quindi too18:50 per una dimostrazione di chiamata di un'operazione dal portale per sviluppatori di hello con e senza hello necessari token di autorizzazione.  
  
```xml  
<!-- Copy hello following snippet into hello inbound section at hello api (or higher) level toopre-authorize access toooperations based on token claims -->  
<set-variable name="signingKey" value="insert signing key here" />  
<choose>  
  <when condition="@(context.Request.Method.Equals("patch",StringComparison.OrdinalIgnoreCase))">  
    <validate-jwt header-name="Authorization">  
      <issuer-signing-keys>  
        <key>@((string)context.Variables["signingKey"])</key>  
      </issuer-signing-keys>  
      <required-claims>  
        <claim name="edit">  
          <value>true</value>  
        </claim>  
      </required-claims>  
    </validate-jwt>  
  </when>  
  <when condition="@(new [] {"post", "put"}.Contains(context.Request.Method,StringComparer.OrdinalIgnoreCase))">  
    <validate-jwt header-name="Authorization">  
      <issuer-signing-keys>  
        <key>@((string)context.Variables["signingKey"])</key>  
      </issuer-signing-keys>  
      <required-claims>  
        <claim name="create">  
          <value>true</value>  
        </claim>  
      </required-claims>  
    </validate-jwt>  
  </when>  
  <otherwise>  
    <validate-jwt header-name="Authorization">  
      <issuer-signing-keys>  
        <key>@((string)context.Variables["signingKey"])</key>  
      </issuer-signing-keys>  
    </validate-jwt>  
  </otherwise>  
</choose>  
```  
  
### <a name="elements"></a>Elementi  
  
|Elemento|Descrizione|Obbligatorio|  
|-------------|-----------------|--------------|  
|validate-jwt|Elemento radice.|Sì|  
|audiences|Contiene un elenco di attestazioni di destinatari accettabili che possono essere presenti nel token hello. Se sono presenti più valori "audience", viene provato ogni valore fino al completamento di tutti i valori (caso in cui la convalida ha esito negativo) o fino a quando un valore non ha esito positivo. È necessario specificare almeno un "audience".|No|  
|issuer-signing-keys|Un elenco di sicurezza con codifica Base64 le chiavi usate toovalidate firmati i token. Se sono presenti più chiavi di sicurezza, viene provata ogni chiave fino al completamento di tutte le chiavi (caso in cui la convalida ha esito negativo) o fino a quando una chiave non ha esito positivo. Gli elementi chiave hanno un parametro facoltativo `id` toomatch attributo utilizzato contro `kid` attestazione.|No|  
|issuers|Un elenco di entità accettabili che ha emesso il token hello. Se sono presenti più valori emittenti, viene provato ogni valore fino al completamento di tutti i valori (caso in cui la convalida ha esito negativo) o fino a quando un valore non ha esito positivo.|No|  
|openid-config|elemento Hello utilizzata per specificare un endpoint di configurazione Openid conforme da cui è possibile ottenere le chiavi e dell'autorità di certificazione di firma.|No|  
|required-claims|Contiene un elenco di attestazioni previste toobe presente nel token hello per tale toobe considerato valido. Quando hello `match` attributo è impostato troppo`all` nei criteri hello ogni valore dell'attestazione deve essere presente nel token hello per toosucceed di convalida. Quando hello `match` attributo è impostato troppo`any` almeno un'attestazione deve essere presente nel token hello per toosucceed di convalida.|No|  
|zumo-master-key|Chiave master per i token rilasciati da Servizi mobili di Azure|No|  
  
### <a name="attributes"></a>Attributi  
  
|Nome|Descrizione|Obbligatorio|Default|  
|----------|-----------------|--------------|-------------|  
|clock-skew|TimeSpan. Fornisce una minima flessibilità nel caso in cui sia presente nel token hello attestazione di scadenza del token hello e oltre hello corrente data / ora.|No|0 secondi|  
|failed-validation-error-message|Tooreturn messaggio di errore nel corpo della risposta HTTP hello se hello JWT non supera la convalida. I caratteri speciali eventualmente contenuti in questo messaggio devono essere adeguatamente preceduti da un carattere di escape.|No|Il messaggio di errore predefinito dipende dal problema della convalida, ad esempio "JWT not present" ("JWT non presente").|  
|failed-validation-httpcode|Codice di stato HTTP tooreturn se hello JWT non supera la convalida.|No|401|  
|header-name|nome di Hello dell'intestazione HTTP hello che contiene il token hello.|È necessario specificare `header-name` o `query-paremeter-name`, ma non entrambi.|N/D|  
|id|Hello `id` attributo hello `key` elemento consente stringa hello toospecify che verrà confrontato con `kid` hello toofind token (se presente) out hello toouse chiave appropriata per la convalida della firma di attestazione.|No|N/D|  
|match|Hello `match` attributo hello `claim` elemento specifica se ogni valore attestazione in Criteri di hello deve essere presenti nel token hello per toosucceed di convalida. I valori possibili sono:<br /><br /> -                          `all`-ogni valore attestazione in Criteri di hello deve essere presente nel token hello per toosucceed di convalida.<br /><br /> -                          `any`-il valore di almeno un'attestazione deve essere presente nel token hello per toosucceed di convalida.|No|tutti|  
|query-paremeter-name|nome Hello hello hello del parametro della query che contiene il token hello.|È necessario specificare `header-name` o `query-paremeter-name`, ma non entrambi.|N/D|  
|require-expiration-time|Booleano. Specifica se un'attestazione di scadenza è necessaria nel token hello.|No|true|
|require-scheme|Hello nome dello schema token hello, ad esempio "Bearer". Quando questo attributo è impostato, i criteri di hello assicura che specifica lo schema è presente nel valore dell'intestazione di autorizzazione hello.|No|N/D|
|require-signed-tokens|Booleano. Specifica se un token è obbligatorio toobe firmato.|No|true|  
|URL|URL dell'endpoint di configurazione Open ID dal quale è possibile ottenere i metadati della configurazione Open ID. Per Azure Active Directory utilizzare hello seguente URL: `https://login.microsoftonline.com/{tenant-name}/.well-known/openid-configuration` sostituendo il nome di tenant di directory, ad esempio `contoso.onmicrosoft.com`.|Sì|N/D|  
  
### <a name="usage"></a>Utilizzo  
 Questo criterio può essere utilizzato hello seguenti criteri [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sezioni del criterio:** inbound  
  
-   **Ambiti del criterio:** globale, prodotto, API, operazione  
  
## <a name="next-steps"></a>Passaggi successivi
Per altre informazioni sull'uso dei criteri, vedere [Criteri di Gestione API](api-management-howto-policies.md).  
