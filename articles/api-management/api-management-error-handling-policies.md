---
title: aaaError Gestione criteri di gestione API di Azure | Documenti Microsoft
description: Informazioni su come toorespond tooerror condizioni che possono verificarsi durante hello l'elaborazione delle richieste in Gestione API di Azure.
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 3c777964-02b2-4f55-8731-8c3bd3c0ae27
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 002c65f21e763fd644da61b6a11685ffd97488c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="error-handling-in-api-management-policies"></a>Gestione degli errori nei criteri di Gestione API
Gestione API di Azure consente ai produttori toorespond tooerror condizioni che possono verificarsi durante l'elaborazione di hello del proxy toohello richieste fornendo un `ProxyError` oggetto. Hello `ProxyError` oggetto avviene tramite hello [contesto. LastError](api-management-policy-expressions.md#ContextVariables) proprietà e può essere usato dai criteri di hello `on-error` sezione relativa ai criteri. In questo argomento fornisce un riferimento per correggere l'errore hello funzionalità di gestione in Gestione API di Azure.  
  
## <a name="error-handling-in-api-management"></a>Gestione degli errori in Gestione API  
 I criteri di gestione API di Azure sono suddivisi in `inbound`, `backend`, `outbound`, e `on-error` sezioni come illustrato nell'esempio seguente hello.  
  
```xml  
<policies>  
  <inbound>  
    <!-- statements toobe applied toohello request go here -->  
  </inbound>  
  <backend>  
    <!-- statements toobe applied before hello request is   
         forwarded toohello backend service go here -->  
    </backend>  
    <outbound>  
      <!-- statements toobe applied toohello response go here -->  
    </outbound>  
    <on-error>  
        <!-- statements toobe applied if there is an error   
             condition go here -->  
  </on-error>  
</policies>  
```  
  
 Durante l'elaborazione di hello di una richiesta, incorporati passaggi vengono eseguiti insieme a tutti i criteri che rientrano nell'ambito per la richiesta hello. Se si verifica un errore, l'elaborazione immediatamente passa toohello `on-error` sezione relativa ai criteri. Hello `on-error` sezione criteri può essere utilizzata in qualsiasi ambito e i server di pubblicazione di API è possibile configurare il comportamento personalizzato, ad esempio gli hub di hello errore tooevent di registrazione o la creazione di un nuovo chiamante toohello tooreturn di risposta.  
  
> [!NOTE]
>  Hello `on-error` sezione non è presente nei criteri per impostazione predefinita. hello tooadd `on-error` sezione tooa criteri, selezionare i criteri toohello desiderato nell'editor Criteri di hello e aggiungerlo. Per ulteriori informazioni sulla configurazione dei criteri, vedere [Criteri di Gestione API](https://azure.microsoft.com/documentation/articles/api-management-howto-policies/).  
>   
>  Se la sezione `on-error` non è presente, il chiamante riceverà dei messaggi di risposta 400 o 500 HTTP in caso di una condizione di errore.  
  
### <a name="policies-allowed-in-on-error"></a>Criteri consentiti in on-error  
 Hello seguenti criteri possono essere usati in hello `on-error` sezione relativa ai criteri.  
  
-   [choose](api-management-advanced-policies.md#choose)  
  
-   [set-variable](api-management-advanced-policies.md#set-variable)  
  
-   [find-and-replace](api-management-transformation-policies.md#Findandreplacestringinbody)  
  
-   [return-response](api-management-advanced-policies.md#ReturnResponse)  
  
-   [set-header](api-management-transformation-policies.md#SetHTTPheader)  
  
-   [set-method](api-management-advanced-policies.md#SetRequestMethod)  
  
-   [set-status](api-management-advanced-policies.md#SetStatus)  
  
-   [send-request](api-management-advanced-policies.md#SendRequest)  
  
-   [send-one-way-request](api-management-advanced-policies.md#SendOneWayRequest)  
  
-   [log-to-eventhub](api-management-advanced-policies.md#log-to-eventhub)  
  
-   [json-to-xml](api-management-transformation-policies.md#ConvertJSONtoXML)  
  
-   [xml-to-json](api-management-transformation-policies.md#ConvertXMLtoJSON)  
  
## <a name="lasterror"></a>LastError  
 Quando si verifica un errore e il controllo passa toohello `on-error` sezione relativa ai criteri, l'errore hello viene archiviato in [contesto. LastError](api-management-policy-expressions.md#ContextVariables) proprietà che è possibile accedere tramite criteri di hello `on-error` sezione e ha hello le proprietà seguenti.  
  
|Nome|Tipo|Descrizione|Obbligatorio|  
|----------|----------|-----------------|--------------|  
|Sorgente|string|Elemento hello nomi in cui si è verificato l'errore hello. Può trattarsi di un criterio o di un nome di passaggio predefinito nella pipeline.|Sì|  
|Motivo|string|Codice errore leggibile tramite computer, da utilizzare se necessario nella gestione degli errori.|No|  
|Message|string|Descrizione dell'errore leggibile dall'utente.|Sì|  
|Scope|string|Nome dell'ambito di hello in errore hello e potrebbe essere uno di "globali", "product", "api" o "operation"|No|  
|Sezione|string|Nome della sezione in cui si è verificato l'errore. Può essere "inbound", "backend", "outbound" o "on-error".|No|  
|Path|string|Specifica i criteri annidati, ad esempio "choose[3]/when[2]".|No|  
|PolicyId|string|Valore di hello `id` attributo, se specificato dal cliente hello, sui criteri hello in cui si è verificato l'errore|No|  
  
> [!NOTE]
>  Tutti i criteri è facoltativa `id` attributo che è possibile aggiungere l'elemento radice toohello dei criteri di hello. Se questo attributo è presente in un criterio quando si verifica una condizione di errore, è possibile recuperare il valore di hello dell'attributo hello utilizzando hello `context.LastError.PolicyId` proprietà.  
  
## <a name="predefined-errors-for-built-in-steps"></a>Errori predefiniti per i passaggi predefiniti  
 gli errori seguenti Hello sono predefiniti per le condizioni di errore che possono verificarsi durante la valutazione di hello dei passaggi di elaborazione predefinite.  
  
|Sorgente|Condizione|Motivo|Message|  
|------------|---------------|------------|-------------|  
|configurazione|URI non corrisponde ad tooany Api o operazione|OperationNotFound|Non è possibile toomatch in ingresso tooan l'operazione di richiesta.|  
|autorizzazione|Chiave di sottoscrizione non fornita|SubscriptionKeyNotFound|Accesso negato a causa di toomissing chiave di sottoscrizione. Verificare che tooinclude chiave della sottoscrizione quando si apportano toothis richieste API.|  
|autorizzazione|Il valore della chiave di sottoscrizione non è valido|SubscriptionKeyInvalid|Accesso negato a causa di tooinvalid chiave di sottoscrizione. Verificare che tooprovide una chiave valida per una sottoscrizione attiva.|  
  
## <a name="predefined-errors-for-policies"></a>Errori predefiniti per i criteri  
 gli errori seguenti Hello sono predefiniti per le condizioni di errore che possono verificarsi durante la valutazione dei criteri.  
  
|Sorgente|Condizione|Motivo|Message|  
|------------|---------------|------------|-------------|  
|rate-limit|Limite di velocità superato|RateLimitExceeded|Il limite di velocità è stato superato|  
|quota|La quota è stata superata|QuotaExceeded|La quota del volume di chiamate è esaurita. La quota verrà ripristinata in xx:xx:xx. -oppure- La quota della larghezza di banda è esaurita. La quota verrà ripristinata in xx:xx:xx.|  
|jsonp|Il valore del parametro callback non è valido (contiene caratteri errati)|CallbackParameterInvalid|Il valore del parametro callback {callback-parameter-name} non è un identificatore JavaScrpit valido.|  
|ip-filter|IP chiamante tooparse non riuscito dalla richiesta|FailedToParseCallerIP|Non è stato possibile indirizzo IP tooestablish chiamante hello. Accesso negato.|  
|ip-filter|L'IP del chiamante non è presente nell'elenco degli IP consentiti|CallerIpNotAllowed|L'indirizzo IP del chiamante {ip-address} non è consentito. Accesso negato.|  
|ip-filter|L'IP del chiamante è presente nell'elenco degli IP bloccati|CallerIpBlocked|L'indirizzo IP del chiamante è bloccato. Accesso negato.|  
|check-header|Intestazione richiesta non presentata o valore mancante|HeaderNotFound|Intestazione {intestazione-name} non è stata trovata nella richiesta di hello. Accesso negato.|  
|check-header|Intestazione richiesta non presentata o valore mancante|HeaderValueNotAllowed|Il valore {header-value} dell'intestazione {header-name} non è consentito. Accesso negato.|  
|validate-jwt|La richiesta non contiene il token JWT|TokenNotFound|JWT non trovato nella richiesta di hello. Accesso negato.|  
|validate-jwt|Convalida della firma non riuscita|TokenSignatureInvalid|<messaggio dalla libreria JWT\>. Accesso negato.|  
|validate-jwt|Destinatari non validi|TokenAudienceNotAllowed|<messaggio dalla libreria JWT\>. Accesso negato.|  
|validate-jwt|Autorità di certificazione non valida|TokenIssuerNotAllowed|<messaggio dalla libreria JWT\>. Accesso negato.|  
|validate-jwt|Token scaduto|TokenExpired|<messaggio dalla libreria JWT\>. Accesso negato.|  
|validate-jwt|La chiave della firma non è stata risolta dall'ID|TokenSignatureKeyNotFound|<messaggio dalla libreria JWT\>. Accesso negato.|  
|validate-jwt|Attestazioni necessarie non presenti nel token|TokenClaimNotFound|Token JWT manca hello seguenti attestazioni: < c1\>, < c2\>,... Accesso negato.|  
|validate-jwt|I valori di attestazione non corrispondono|TokenClaimValueNotAllowed|Il valore {claim-value} dell'attestazione {claim-name} non è consentito. Accesso negato.|  
|validate-jwt|Altri errori di convalida|JwtInvalid|<messaggio dalla libreria JWT\>|

## <a name="next-steps"></a>Passaggi successivi
Per altre informazioni sull'uso dei criteri, vedere [Criteri di Gestione API](api-management-howto-policies.md).  