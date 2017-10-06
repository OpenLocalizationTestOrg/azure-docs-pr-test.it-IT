---
title: aaaAzure gestione API di criteri tra domini | Documenti Microsoft
description: Informazioni su hello criteri tra domini disponibili per l'utilizzo in Gestione API di Azure.
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 7689d277-8abe-472a-a78c-e6d4bd43455d
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: dd5ebfd65b92ebd0c1f589a2bac669a3928d40b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-cross-domain-policies"></a>Criteri tra domini di Gestione API
In questo argomento fornisce un riferimento per i seguenti criteri di gestione API hello. Per informazioni sull'aggiunta e sulla configurazione dei criteri, vedere [Criteri di Gestione API](http://go.microsoft.com/fwlink/?LinkID=398186).  
  
##  <a name="CrossDomainPolicies"></a> Criteri tra domini  
  
-   [Consentire le chiamate tra domini](api-management-cross-domain-policies.md#AllowCrossDomainCalls) -rende accessibile hello API da client Adobe Flash e Microsoft Silverlight basati su browser.  
  
-   [CORS](api-management-cross-domain-policies.md#CORS) -aggiunge la condivisione di risorse multiorigine (CORS) supporta l'operazione di tooan o chiama un'API tooallow tra domini da client basati su browser.  
  
-   [JSONP](api-management-cross-domain-policies.md#JSONP) - aggiunge JSON con riempimento (JSONP) supporto tooan operazione o chiama un'API tooallow tra domini da client JavaScript basati su browser.  
  
##  <a name="AllowCrossDomainCalls"></a> Permetti chiamate tra i domini  
 Hello utilizzare `cross-domain` hello toomake criteri API accessibile da client Adobe Flash e Microsoft Silverlight basati su browser.  
  
### <a name="policy-statement"></a>Istruzione del criterio  
  
```xml  
<cross-domain>  
   <!-Policy configuration is in hello Adobe cross-domain policy file format,   
      see http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html-->  
</cross-domain>  
```  
  
### <a name="example"></a>Esempio  
  
```xml  
<cross-domain>  
    <cross-domain-policy>  
        <allow-http-request-headers-from domain='*' headers='*' />  
    </cross-domain-policy>  
</cross-domain>  
```  
  
### <a name="elements"></a>Elementi  
  
|Nome|Descrizione|Obbligatorio|  
|----------|-----------------|--------------|  
|cross-domain|Elemento radice. Gli elementi figlio devono essere conformi toohello [specifica del file di criteri tra domini di Adobe](http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html).|Sì|  
  
### <a name="usage"></a>Utilizzo  
 Questo criterio può essere utilizzato hello seguenti criteri [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sezioni del criterio:** inbound  
  
-   **Ambiti del criterio:** globali  
  
##  <a name="CORS"></a> CORS  
 Hello `cors` criteri aggiunge la condivisione di risorse multiorigine (CORS) supporta l'operazione di tooan o chiama un'API tooallow tra domini da client basati su browser.  
  
 CORS consente un browser e un server toointeract e determinare se tooallow specifico multiorigine richieste (ad esempio chiamate XMLHttpRequests eseguite da JavaScript su domini di tooother una pagina web). Ciò offre una maggiore flessibilità rispetto a permettere solo richieste con la stessa origine e una maggiore sicurezza rispetto a permettere tutte le richieste con origini diverse.  
  
### <a name="policy-statement"></a>Istruzione del criterio  
  
```xml  
<cors allow-credentials="false|true">  
    <allowed-origins>  
        <origin>origin uri</origin>  
    </allowed-origins>  
    <allowed-methods preflight-result-max-age="number of seconds">  
        <method>http verb</method>  
    </allowed-methods>  
    <allowed-headers>  
        <header>header name</header>  
    </allowed-headers>  
    <expose-headers>  
        <header>header name</header>  
    </expose-headers>  
</cors>  
```  
  
### <a name="example"></a>Esempio  
 In questo esempio viene illustrato come le richieste preliminari toosupport, ad esempio quelle con intestazioni personalizzate o metodi diversi da GET e POST. toosupport le intestazioni personalizzate e verbi HTTP aggiuntivi, utilizzare hello `allowed-methods` e `allowed-headers` sezioni come illustrato nell'esempio seguente hello.  
  
```xml  
<cors allow-credentials="true">  
    <allowed-origins>  
        <!-- Localhost useful for development -->  
        <origin>http://localhost:8080/</origin>  
        <origin>http://example.com/</origin>  
    </allowed-origins>  
    <allowed-methods preflight-result-max-age="300">  
        <method>GET</method>  
        <method>POST</method>  
        <method>PATCH</method>  
        <method>DELETE</method>  
    </allowed-methods>  
    <allowed-headers>  
        <!-- Examples below show Azure Mobile Services headers -->  
        <header>x-zumo-installation-id</header>  
        <header>x-zumo-application</header>  
        <header>x-zumo-version</header>  
        <header>x-zumo-auth</header>  
        <header>content-type</header>  
        <header>accept</header>  
    </allowed-headers>  
    <expose-headers>  
        <!-- Examples below show Azure Mobile Services headers -->  
        <header>x-zumo-installation-id</header>  
        <header>x-zumo-application</header>  
    </expose-headers>  
</cors>  
```  
  
### <a name="elements"></a>Elementi  
  
|Nome|Descrizione|Obbligatorio|Default|  
|----------|-----------------|--------------|-------------|  
|CORS|Elemento radice.|Sì|N/D|  
|allowed-origins|Contiene `origin` gli elementi che descrivono hello consentito le origini per le richieste tra domini. `allowed-origins`può contenere un singolo `origin` elemento che specifica `*` tooallow qualsiasi origine o di uno o più `origin` elementi che contengono un URI.|Sì|N/D|  
|origin|Hello valore può essere `*` tooallow tutte le origini, oppure un URI che specifica una singola origine. Hello URI deve includere uno schema, l'host e porta.|Sì|Se la porta hello viene omessa in un URI, viene utilizzata la porta 80 per HTTP e viene utilizzata la porta 443 per HTTPS.|  
|allowed-methods|Questo elemento è obbligatorio se sono consentiti metodi diversi da GET o POST. Contiene `method` elementi che specificano hello verbi HTTP è supportata.|No|Se questa sezione non è presente, sono supportati i metodi GET e POST.|  
|statico|Specifica un verbo HTTP.|Almeno un `method` elemento è obbligatorio se hello `allowed-methods` sezione è presente.|N/D|  
|allowed-headers|Questo elemento contiene `header` gli elementi che specificano i nomi delle intestazioni di hello che possono essere incluso nella richiesta di hello.|No|N/D|  
|expose-headers|Questo elemento contiene `header` gli elementi che specificano i nomi delle intestazioni di hello che saranno accessibili dal client hello.|No|N/D|  
|intestazione|Specifica un nome di intestazione.|Almeno un `header` elemento è obbligatorio in `allowed-headers` o `expose-headers` se hello sezione è presente.|N/D|  
  
### <a name="attributes"></a>Attributi  
  
|Nome|Descrizione|Obbligatorio|Default|  
|----------|-----------------|--------------|-------------|  
|allow-credentials|Hello `Access-Control-Allow-Credentials` intestazione nella risposta preliminare hello verrà toohello impostare il valore di questo attributo e influiscono su hello possibilità toosubmit credenziali client in richieste tra domini.|No|false|  
|preflight-result-max-age|Hello `Access-Control-Max-Age` intestazione nella risposta preliminare hello verrà toohello impostare il valore di questo attributo e influiscono sulla risposta preliminare toocache di capacità dell'agente utente hello.|No|0|  
  
### <a name="usage"></a>Utilizzo  
 Questo criterio può essere utilizzato hello seguenti criteri [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sezioni del criterio:** inbound  
  
-   **Ambiti del criterio:** API, operazione  
  
##  <a name="JSONP"></a> JSONP  
 Hello `jsonp` criteri aggiunge JSON con riempimento operazione tooan di supporto (JSONP) o le chiamate tra domini tooallow un'API da client JavaScript basati su browser. JSONP è un metodo usato nei dati di toorequest programmi JavaScript da un server in un dominio diverso. JSONP supera limitazione hello applicata dalla maggior parte dei browser in cui devono essere pagine di accesso tooweb hello nello stesso dominio.  
  
### <a name="policy-statement"></a>Istruzione del criterio  
  
```xml  
<jsonp callback-parameter-name="callback function name" />  
```  
  
### <a name="example"></a>Esempio  
  
```xml  
<jsonp callback-parameter-name="cb" />  
```  
  
 Se si chiama il metodo hello senza il parametro di callback hello? cb = XXX restituirà JSON semplice (senza un wrapper di chiamata di funzione).  
  
 Se si aggiunge il parametro di callback hello `?cb=XXX` restituirà un risultato JSONP, wrapping risultati JSON originali hello per funzione di callback hello come`XYZ('<json result goes here>');`  
  
### <a name="elements"></a>Elementi  
  
|Nome|Descrizione|Obbligatorio|  
|----------|-----------------|--------------|  
|jsonp|Elemento radice.|Sì|  
  
### <a name="attributes"></a>Attributi  
  
|Nome|Descrizione|Obbligatorio|Default|  
|----------|-----------------|--------------|-------------|  
|callback-parameter-name|Hello chiamata alla funzione JavaScript tra domini con prefisso il nome di dominio completo hello in hello funzione risiede.|Sì|N/D|  
  
### <a name="usage"></a>Utilizzo  
 Questo criterio può essere utilizzato hello seguenti criteri [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sezioni del criterio:** in uscita  
  
-   **Ambiti del criterio:** globale, prodotto, API, operazione  
  
## <a name="next-steps"></a>Passaggi successivi
Per altre informazioni sull'uso dei criteri, vedere [Criteri di Gestione API](api-management-howto-policies.md).  