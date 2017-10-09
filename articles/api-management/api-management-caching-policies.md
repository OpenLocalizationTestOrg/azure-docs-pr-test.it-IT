---
title: criteri di memorizzazione nella cache gestione API aaaAzure | Documenti Microsoft
description: Informazioni sui criteri disponibili per l'utilizzo in Gestione API di Azure di memorizzazione nella cache di hello.
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 8147199c-24d8-439f-b2a9-da28a70a890c
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: bd6b0721945609b28dbf6e7ef0631979c08c8c65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-caching-policies"></a>Criteri di memorizzazione nella cache in Gestione API
In questo argomento fornisce un riferimento per i seguenti criteri di gestione API hello. Per informazioni sull'aggiunta e sulla configurazione dei criteri, vedere [Criteri di Gestione API](http://go.microsoft.com/fwlink/?LinkID=398186).  
  
##  <a name="CachingPolicies"></a> Criteri di memorizzazione nella cache  
  
-   Criteri di memorizzazione nella cache della risposta  
  
    -   [Recupera dalla cache](api-management-caching-policies.md#GetFromCache): esegue una ricerca nella cache e restituisce risposte valide memorizzate nella cache, se disponibili.  
  
    -   [Archiviare toocache](api-management-caching-policies.md#StoreToCache) - risposte memorizza nella cache in base di configurazione del controllo toohello della cache specificata.  
  
-   Criteri di memorizzazione dei valori nella cache  
  
    -   [Recupera valore dalla cache](#GetFromCacheByKey) : recupera un elemento memorizzato nella cache per chiave.  
  
    -   [Valore di memorizzare nella cache](#StoreToCacheByKey) -archiviare un elemento nella cache di hello dalla chiave.  
  
    -   [Rimuovi valore dalla cache](#RemoveCacheByKey) -rimuovere un elemento nella cache di hello dalla chiave.  
  
##  <a name="GetFromCache"></a> Recupera dalla cache  
 Hello utilizzare `cache-lookup` tooperform cache dei criteri di cercare e restituire una risposta memorizzata nella cache valida, se disponibile. Questo criterio può essere applicato nei casi in cui il contenuto della risposta rimane statico in un periodo di tempo. Risposta di memorizzazione nella cache riduce la larghezza di banda e requisiti di elaborazione imposto a hello back-end web server e diminuisce la latenza percepita dagli utenti delle API.  
  
> [!NOTE]
>  Questo criterio deve avere una corrispondente [toocache archivio](api-management-caching-policies.md#StoreToCache) criteri.  
  
### <a name="policy-statement"></a>Istruzione del criterio  
  
```xml  
<cache-lookup vary-by-developer="true | false" vary-by-developer-groups="true | false" downstream-caching-type="none | private | public" must-revalidate="true | false" allow-private-response-caching="@(expression tooevaluate)">  
  <vary-by-header>Accept</vary-by-header>  
  <!-- should be present in most cases -->  
  <vary-by-header>Accept-Charset</vary-by-header>  
  <!-- should be present in most cases -->  
  <vary-by-header>Authorization</vary-by-header>  
  <!-- should be present when allow-authorized-response-caching is "true"-->  
  <vary-by-header>header name</vary-by-header>  
  <!-- optional, can repeated several times -->  
  <vary-by-query-parameter>parameter name</vary-by-query-parameter>  
  <!-- optional, can repeated several times -->  
</cache-lookup>  
```  
  
### <a name="examples"></a>Esempi  
  
#### <a name="example"></a>Esempio  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <cache-lookup vary-by-developer="false" vary-by-developer-groups="false" downstream-caching-type="none" must-revalidate="true">  
            <vary-by-query-parameter>version</vary-by-query-parameter>  
        </cache-lookup>           
    </inbound>  
    <outbound>  
        <cache-store duration="seconds" />  
        <base />          
    </outbound>  
</policies>  
```  
  
#### <a name="example-using-policy-expressions"></a>Esempio con espressioni di criteri  
 Questo esempio viene illustrato come risposta di gestione API tootooconfigure la memorizzazione nella cache di durata che corrispondenze hello la memorizzazione nella cache di risposta del servizio back-end hello come specificato da hello backup del servizio `Cache-Control` direttiva. Per una dimostrazione della configurazione e l'utilizzo di questo criterio, vedere [Cloud coprire episodio 177: più API le funzionalità di gestione con Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) e far avanzare rapidamente too25:25.  
  
```xml  
<!-- hello following cache policy snippets demonstrate how toocontrol API Management reponse cache duration with Cache-Control headers sent by hello backend service. -->  
  
<!-- Copy this snippet into hello inbound section -->  
<cache-lookup vary-by-developer="false" vary-by-developer-groups="false" downstream-caching-type="public" must-revalidate="true" >  
  <vary-by-header>Accept</vary-by-header>  
  <vary-by-header>Accept-Charset</vary-by-header>  
</cache-lookup>  
  
<!-- Copy this snippet into hello outbound section. Note that cache duration is set toohello max-age value provided in hello Cache-Control header received from hello backend service or toohello deafult value of 5 min if none is found  -->  
<cache-store duration="@{  
    var header = context.Response.Headers.GetValueOrDefault("Cache-Control","");  
    var maxAge = Regex.Match(header, @"max-age=(?<maxAge>\d+)").Groups["maxAge"]?.Value;  
    return (!string.IsNullOrEmpty(maxAge))?int.Parse(maxAge):300;  
  }"  
 />  
```  
  
 Per altre informazioni, vedere [Espressioni di criteri](api-management-policy-expressions.md) e [Variabile di contesto](api-management-policy-expressions.md#ContextVariables).  
  
### <a name="elements"></a>Elementi  
  
|Nome|Descrizione|Obbligatorio|  
|----------|-----------------|--------------|  
|cache-lookup|Elemento radice.|Sì|  
|vary-by-header|Avviare la memorizzazione delle risposte nella cache per ogni valore dell'intestazione specificata, come ad esempio Accept, Accept-Charset, Accept-Encoding, Accept-Language, Authorization, Expect, From, Host e If-Match.|No|  
|vary-by-query-parameter|Avvia risposte di memorizzazione nella cache per ogni valore dei parametri di query specificati. Immettere un singolo parametro o più parametri. Usare un punto e virgola (;) come separatore. Se non è specificato alcun nome, verranno usati tutti i parametri di query.|No|  
  
### <a name="attributes"></a>Attributi  
  
|Nome|Descrizione|Obbligatorio|Default|  
|----------|-----------------|--------------|-------------|  
|allow-private-response-caching|Quando impostato troppo`true`, consente la memorizzazione nella cache le richieste che contengono un'intestazione di autorizzazione.|No|false|  
|downstream-caching-type|Questo attributo deve essere impostato tooone dei seguenti valori hello.<br /><br /> -   none - Non è consentita la memorizzazione nella cache downstream.<br />-   private - È consentita la memorizzazione nella cache downstream privata.<br />-   public - È consentita la memorizzazione nella cache downstream privata e condivisa.|No|nessuno|  
|must-revalidate|Quando è abilitata la memorizzazione nella cache downstream questo attributo attiva o disattiva hello `must-revalidate` direttiva di controllo della cache nelle risposte di gateway.|No|true|  
|vary-by-developer|Impostare troppo`true` toocache le risposte per ogni chiave sviluppatore.|No|false|  
|vary-by-developer-groups|Impostare troppo`true` risposte toocache al ruolo utente.|No|false|  
  
### <a name="usage"></a>Utilizzo  
 Questo criterio può essere utilizzato hello seguenti criteri [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sezioni del criterio:** inbound  
  
-   **Ambiti del criterio:** API, operazione, prodotto  
  
##  <a name="StoreToCache"></a>Archivio toocache  
 Hello `cache-store` risposte memorizza nella cache dei criteri in base toohello specificato le impostazioni della cache. Questo criterio può essere applicato nei casi in cui il contenuto della risposta rimane statico in un periodo di tempo. Risposta di memorizzazione nella cache riduce la larghezza di banda e requisiti di elaborazione imposto a hello back-end web server e diminuisce la latenza percepita dagli utenti delle API.  
  
> [!NOTE]
>  Questo criterio deve essere associato a un criterio [Recupera dalla cache](api-management-caching-policies.md#GetFromCache) corrispondente.  
  
### <a name="policy-statement"></a>Istruzione del criterio  
  
```xml  
<cache-store duration="seconds" />  
```  
  
### <a name="examples"></a>Esempi  
  
#### <a name="example"></a>Esempio  
  
```xml  
<policies>  
    <inbound>  
        <base />  
          <cache-lookup vary-by-developer="true | false" vary-by-developer-groups="true | false" downstream-caching-type="none | private | public" must-revalidate="true | false">  
                <vary-by-query-parameter>parameter name</vary-by-query-parameter> <!-- optional, can repeated several times -->  
        </cache-lookup>  
    </inbound>  
    <outbound>  
        <base />  
            <cache-store duration="3600" />  
    </outbound>  
</policies>  
```  
  
#### <a name="example-using-policy-expressions"></a>Esempio con espressioni di criteri  
 Questo esempio viene illustrato come risposta di gestione API tootooconfigure la memorizzazione nella cache di durata che corrispondenze hello la memorizzazione nella cache di risposta del servizio back-end hello come specificato da hello backup del servizio `Cache-Control` direttiva. Per una dimostrazione della configurazione e l'utilizzo di questo criterio, vedere [Cloud coprire episodio 177: più API le funzionalità di gestione con Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) e far avanzare rapidamente too25:25.  
  
```xml  
<!-- hello following cache policy snippets demonstrate how toocontrol API Management reponse cache duration with Cache-Control headers sent by hello backend service. -->  
  
<!-- Copy this snippet into hello inbound section -->  
<cache-lookup vary-by-developer="false" vary-by-developer-groups="false" downstream-caching-type="public" must-revalidate="true" >  
  <vary-by-header>Accept</vary-by-header>  
  <vary-by-header>Accept-Charset</vary-by-header>  
</cache-lookup>  
  
<!-- Copy this snippet into hello outbound section. Note that cache duration is set toohello max-age value provided in hello Cache-Control header received from hello backend service or toohello deafult value of 5 min if none is found  -->  
<cache-store duration="@{  
    var header = context.Response.Headers.GetValueOrDefault("Cache-Control","");  
    var maxAge = Regex.Match(header, @"max-age=(?<maxAge>\d+)").Groups["maxAge"]?.Value;  
    return (!string.IsNullOrEmpty(maxAge))?int.Parse(maxAge):300;  
  }"  
 />  
```  
  
 Per altre informazioni, vedere [Espressioni di criteri](api-management-policy-expressions.md) e [Variabile di contesto](api-management-policy-expressions.md#ContextVariables).  
  
### <a name="elements"></a>Elementi  
  
|Nome|Descrizione|Obbligatorio|  
|----------|-----------------|--------------|  
|cache-store|Elemento radice.|Sì|  
  
### <a name="attributes"></a>Attributi  
  
|Nome|Descrizione|Obbligatorio|Default|  
|----------|-----------------|--------------|-------------|  
|duration|Time-to-live di hello memorizzati nella cache di voci, espresso in secondi.|Sì|N/D|  
  
### <a name="usage"></a>Utilizzo  
 Questo criterio può essere utilizzato hello seguenti criteri [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sezioni del criterio:** in uscita  
  
-   **Ambiti del criterio:** API, operazione, prodotto  
  
##  <a name="GetFromCacheByKey"></a> Recupera valore dalla cache  
 Hello utilizzare `cache-lookup-value` tooperform criteri nella cache di ricerca dalla chiave e restituire un valore memorizzato nella cache. chiave di Hello può avere un valore stringa arbitrario e viene in genere fornito con un'espressione di criteri.  
  
> [!NOTE]
>  Questo criterio deve essere associato a un criterio [Archivia valore nella cache](#StoreToCacheByKey) corrispondente.  
  
### <a name="policy-statement"></a>Istruzione del criterio  
  
```xml  
<cache-lookup-value key="cache key value"   
    default-value="value toouse if cache lookup resulted in a miss"   
    variable-name="name of a variable looked up value is assigned to" />  
```  
  
### <a name="example"></a>Esempio  
 Per ulteriori informazioni ed esempi su questo criterio, vedere [Memorizzazione nella cache personalizzata in Gestione API di Azure](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).  
  
```xml  
<cache-lookup-value  
    key="@("userprofile-" + context.Variables["enduserid"])"    
    variable-name="userprofile" />  
  
```  
  
### <a name="elements"></a>Elementi  
  
|Nome|Descrizione|Obbligatorio|  
|----------|-----------------|--------------|  
|cache-lookup-value|Elemento radice.|Sì|  
  
### <a name="attributes"></a>Attributi  
  
|Nome|Descrizione|Obbligatorio|Default|  
|----------|-----------------|--------------|-------------|  
|default-value|Un valore che verrà assegnato toohello variabile se ricerca chiave nella cache di hello ha prodotto un mancato riscontro. Se questo attributo viene omesso, viene assegnato `null`.|No|`null`|  
|key|Valore della chiave toouse nella ricerca hello la cache.|Sì|N/D|  
|variable-name|Nome di hello [variabile di contesto](api-management-policy-expressions.md#ContextVariables) hello cercato valore verrà assegnato a, se la ricerca ha esito positivo. Se i risultati di ricerca in un mancato riscontro, variabile hello verrà assegnato il valore di hello di hello `default-value` attributo o `null`, se hello `default-value` attributo viene omesso.|Sì|N/D|  
  
### <a name="usage"></a>Utilizzo  
 Questo criterio può essere utilizzato hello seguenti criteri [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sezioni del criterio:** inbound, outbound, backend, on-error  
  
-   **Ambiti del criterio:** global, API, operation, product  
  
##  <a name="StoreToCacheByKey"></a> Archivia valore nella cache  
 Hello `cache-store-value` esegue l'archiviazione cache dalla chiave. chiave di Hello può avere un valore stringa arbitrario e viene in genere fornito con un'espressione di criteri.  
  
> [!NOTE]
>  Questo criterio deve essere associato a un criterio [Recupera valore dalla cache](#GetFromCacheByKey) corrispondente.  
  
### <a name="policy-statement"></a>Istruzione del criterio  
  
```xml  
<cache-store-value key="cache key value" value="value toocache" duration="seconds" />  
```  
  
### <a name="example"></a>Esempio  
 Per ulteriori informazioni ed esempi su questo criterio, vedere [Memorizzazione nella cache personalizzata in Gestione API di Azure](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).  
  
```xml  
<cache-store-value  
    key="@("userprofile-" + context.Variables["enduserid"])"  
    value="@((string)context.Variables["userprofile"])" duration="100000" />  
  
```  
  
### <a name="elements"></a>Elementi  
  
|Nome|Descrizione|Obbligatorio|  
|----------|-----------------|--------------|  
|cache-store-value|Elemento radice.|Sì|  
  
### <a name="attributes"></a>Attributi  
  
|Nome|Descrizione|Obbligatorio|Default|  
|----------|-----------------|--------------|-------------|  
|duration|Valore verrà memorizzato nella cache di hello fornito il valore di durata, espresso in secondi.|Sì|N/D|  
|key|Il valore di chiave hello cache verrà archiviato in.|Sì|N/D|  
|value|Hello toobe di valore memorizzato nella cache.|Sì|N/D|  
  
### <a name="usage"></a>Utilizzo  
 Questo criterio può essere utilizzato hello seguenti criteri [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sezioni del criterio:** inbound, outbound, backend, on-error  
  
-   **Ambiti del criterio:** global, API, operation, product  
  
###  <a name="RemoveCacheByKey"></a> Rimuovi valore dalla cache  
 Hello `cache-remove-value` Elimina un elemento memorizzato nella cache identificato in base alla chiave. chiave di Hello può avere un valore stringa arbitrario e viene in genere fornito con un'espressione di criteri.  
  
#### <a name="policy-statement"></a>Istruzione del criterio  
  
```xml  
  
<cache-remove-value key="cache key value"/>  
  
```  
  
#### <a name="example"></a>Esempio  
  
```xml  
  
<cache-remove-value key="@("userprofile-" + context.Variables["enduserid"])"/>  
  
```  
  
#### <a name="elements"></a>Elementi  
  
|Nome|Descrizione|Obbligatorio|  
|----------|-----------------|--------------|  
|cache-remove-value|Elemento radice.|Sì|  
  
#### <a name="attributes"></a>Attributi  
  
|Nome|Descrizione|Obbligatorio|Default|  
|----------|-----------------|--------------|-------------|  
|key|chiave di Hello di hello memorizzata nella cache toobe valore rimosso dalla cache di hello.|Sì|N/D|  
  
#### <a name="usage"></a>Utilizzo  
 Questo criterio può essere utilizzato hello seguenti criteri [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .  
  
-   **Sezioni del criterio:** inbound, outbound, backend, on-error  
  
-   **Ambiti del criterio:** global, API, operation, product  
  

## <a name="next-steps"></a>Passaggi successivi
Per altre informazioni sull'uso dei criteri, vedere [Criteri di Gestione API](api-management-howto-policies.md).  