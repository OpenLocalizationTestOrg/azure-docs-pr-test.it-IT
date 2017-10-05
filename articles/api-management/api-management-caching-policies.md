---
title: Criteri di memorizzazione nella cache in Gestione API di Azure | Microsoft Docs
description: Informazioni sui criteri di memorizzazione nella cache disponibili per l'uso in Gestione API di Azure.
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
ms.openlocfilehash: 2a8f012e7e223ef5c1683c8a6c5ecf2f3e96bed8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="api-management-caching-policies"></a><span data-ttu-id="b6bc2-103">Criteri di memorizzazione nella cache in Gestione API</span><span class="sxs-lookup"><span data-stu-id="b6bc2-103">API Management caching policies</span></span>
<span data-ttu-id="b6bc2-104">Questo argomento fornisce un riferimento per i seguenti criteri di Gestione API.</span><span class="sxs-lookup"><span data-stu-id="b6bc2-104">This topic provides a reference for the following API Management policies.</span></span> <span data-ttu-id="b6bc2-105">Per informazioni sull'aggiunta e sulla configurazione dei criteri, vedere [Criteri di Gestione API](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="b6bc2-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="b6bc2-106"><a name="CachingPolicies"></a> Criteri di memorizzazione nella cache</span><span class="sxs-lookup"><span data-stu-id="b6bc2-106"><a name="CachingPolicies"></a> Caching policies</span></span>  
  
-   <span data-ttu-id="b6bc2-107">Criteri di memorizzazione nella cache della risposta</span><span class="sxs-lookup"><span data-stu-id="b6bc2-107">Response caching policies</span></span>  
  
    -   <span data-ttu-id="b6bc2-108">[Recupera dalla cache](api-management-caching-policies.md#GetFromCache): esegue una ricerca nella cache e restituisce risposte valide memorizzate nella cache, se disponibili.</span><span class="sxs-lookup"><span data-stu-id="b6bc2-108">[Get from cache](api-management-caching-policies.md#GetFromCache) - Perform cache look up and return a valid cached responses when available.</span></span>  
  
    -   <span data-ttu-id="b6bc2-109">[Archivia nella cache](api-management-caching-policies.md#StoreToCache): memorizza nella cache le risposte in base alla configurazione del controllo cache specificata.</span><span class="sxs-lookup"><span data-stu-id="b6bc2-109">[Store to cache](api-management-caching-policies.md#StoreToCache) - Caches responses according to the specified cache control configuration.</span></span>  
  
-   <span data-ttu-id="b6bc2-110">Criteri di memorizzazione dei valori nella cache</span><span class="sxs-lookup"><span data-stu-id="b6bc2-110">Value caching policies</span></span>  
  
    -   <span data-ttu-id="b6bc2-111">[Recupera valore dalla cache](#GetFromCacheByKey) : recupera un elemento memorizzato nella cache per chiave.</span><span class="sxs-lookup"><span data-stu-id="b6bc2-111">[Get value from cache](#GetFromCacheByKey) - Retrieve a cached item by key.</span></span>  
  
    -   <span data-ttu-id="b6bc2-112">[Archivia valore nella cache](#StoreToCacheByKey) : archivia un elemento nella cache per chiave.</span><span class="sxs-lookup"><span data-stu-id="b6bc2-112">[Store value in cache](#StoreToCacheByKey) - Store an item in the cache by key.</span></span>  
  
    -   <span data-ttu-id="b6bc2-113">[Rimuovi valore dalla cache](#RemoveCacheByKey) : rimuove un elemento dalla cache in base alla chiave.</span><span class="sxs-lookup"><span data-stu-id="b6bc2-113">[Remove value from cache](#RemoveCacheByKey) - Remove an item in the cache by key.</span></span>  
  
##  <span data-ttu-id="b6bc2-114"><a name="GetFromCache"></a> Recupera dalla cache</span><span class="sxs-lookup"><span data-stu-id="b6bc2-114"><a name="GetFromCache"></a> Get from cache</span></span>  
 <span data-ttu-id="b6bc2-115">Usare il criterio `cache-lookup` per eseguire una ricerca nella cache e restituire una risposta valida memorizzata nella cache, se disponibile.</span><span class="sxs-lookup"><span data-stu-id="b6bc2-115">Use the `cache-lookup` policy to perform cache look up and return a valid cached response when available.</span></span> <span data-ttu-id="b6bc2-116">Questo criterio può essere applicato nei casi in cui il contenuto della risposta rimane statico in un periodo di tempo.</span><span class="sxs-lookup"><span data-stu-id="b6bc2-116">This policy can be applied in cases where response content remains static over a period of time.</span></span> <span data-ttu-id="b6bc2-117">La memorizzazione delle risposte nella cache riduce la larghezza di banda e i requisiti di elaborazione imposti sul server Web back-end e riduce la latenza percepita dagli utenti delle API.</span><span class="sxs-lookup"><span data-stu-id="b6bc2-117">Response caching reduces bandwidth and processing requirements imposed on the backend web server and lowers latency perceived by API consumers.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="b6bc2-118">Questo criterio deve essere associato a un criterio [Archivia nella cache](api-management-caching-policies.md#StoreToCache) corrispondente.</span><span class="sxs-lookup"><span data-stu-id="b6bc2-118">This policy must have a corresponding [Store to cache](api-management-caching-policies.md#StoreToCache) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="b6bc2-119">Istruzione del criterio</span><span class="sxs-lookup"><span data-stu-id="b6bc2-119">Policy statement</span></span>  
  
```xml  
<cache-lookup vary-by-developer="true | false" vary-by-developer-groups="true | false" downstream-caching-type="none | private | public" must-revalidate="true | false" allow-private-response-caching="@(expression to evaluate)">  
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
  
### <a name="examples"></a><span data-ttu-id="b6bc2-120">Esempi</span><span class="sxs-lookup"><span data-stu-id="b6bc2-120">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="b6bc2-121">Esempio</span><span class="sxs-lookup"><span data-stu-id="b6bc2-121">Example</span></span>  
  
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
  
#### <a name="example-using-policy-expressions"></a><span data-ttu-id="b6bc2-122">Esempio con espressioni di criteri</span><span class="sxs-lookup"><span data-stu-id="b6bc2-122">Example using policy expressions</span></span>  
 <span data-ttu-id="b6bc2-123">Questo esempio mostra come per configurare la durata della memorizzazione nella cache di Gestione API corrispondente alla memorizzazione delle risposte nella cache del serivzio back-end, come specificato dalla direttiva `Cache-Control` del servizio in questione.</span><span class="sxs-lookup"><span data-stu-id="b6bc2-123">This example shows how to to configure API Management response caching duration that matches the response caching of the backend service as specified by the backed service's `Cache-Control` directive.</span></span> <span data-ttu-id="b6bc2-124">Per una dimostrazione relativa alla configurazione e all'uso di questi criteri, vedere l' [episodio 177 di Cloud Cover su altre funzionalità di Gestione API con Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) e passare direttamente al minuto 25:25.</span><span class="sxs-lookup"><span data-stu-id="b6bc2-124">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 25:25.</span></span>  
  
```xml  
<!-- The following cache policy snippets demonstrate how to control API Management reponse cache duration with Cache-Control headers sent by the backend service. -->  
  
<!-- Copy this snippet into the inbound section -->  
<cache-lookup vary-by-developer="false" vary-by-developer-groups="false" downstream-caching-type="public" must-revalidate="true" >  
  <vary-by-header>Accept</vary-by-header>  
  <vary-by-header>Accept-Charset</vary-by-header>  
</cache-lookup>  
  
<!-- Copy this snippet into the outbound section. Note that cache duration is set to the max-age value provided in the Cache-Control header received from the backend service or to the deafult value of 5 min if none is found  -->  
<cache-store duration="@{  
    var header = context.Response.Headers.GetValueOrDefault("Cache-Control","");  
    var maxAge = Regex.Match(header, @"max-age=(?<maxAge>\d+)").Groups["maxAge"]?.Value;  
    return (!string.IsNullOrEmpty(maxAge))?int.Parse(maxAge):300;  
  }"  
 />  
```  
  
 <span data-ttu-id="b6bc2-125">Per altre informazioni, vedere [Espressioni di criteri](api-management-policy-expressions.md) e [Variabile di contesto](api-management-policy-expressions.md#ContextVariables).</span><span class="sxs-lookup"><span data-stu-id="b6bc2-125">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="b6bc2-126">Elementi</span><span class="sxs-lookup"><span data-stu-id="b6bc2-126">Elements</span></span>  
  
|<span data-ttu-id="b6bc2-127">Nome</span><span class="sxs-lookup"><span data-stu-id="b6bc2-127">Name</span></span>|<span data-ttu-id="b6bc2-128">Descrizione</span><span class="sxs-lookup"><span data-stu-id="b6bc2-128">Description</span></span>|<span data-ttu-id="b6bc2-129">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="b6bc2-129">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="b6bc2-130">cache-lookup</span><span class="sxs-lookup"><span data-stu-id="b6bc2-130">cache-lookup</span></span>|<span data-ttu-id="b6bc2-131">Elemento radice.</span><span class="sxs-lookup"><span data-stu-id="b6bc2-131">Root element.</span></span>|<span data-ttu-id="b6bc2-132">Sì</span><span class="sxs-lookup"><span data-stu-id="b6bc2-132">Yes</span></span>|  
|<span data-ttu-id="b6bc2-133">vary-by-header</span><span class="sxs-lookup"><span data-stu-id="b6bc2-133">vary-by-header</span></span>|<span data-ttu-id="b6bc2-134">Avviare la memorizzazione delle risposte nella cache per ogni valore dell'intestazione specificata, come ad esempio Accept, Accept-Charset, Accept-Encoding, Accept-Language, Authorization, Expect, From, Host e If-Match.</span><span class="sxs-lookup"><span data-stu-id="b6bc2-134">Start caching responses per value of specified header, such as Accept, Accept-Charset, Accept-Encoding, Accept-Language, Authorization, Expect, From, Host, If-Match.</span></span>|<span data-ttu-id="b6bc2-135">No</span><span class="sxs-lookup"><span data-stu-id="b6bc2-135">No</span></span>|  
|<span data-ttu-id="b6bc2-136">vary-by-query-parameter</span><span class="sxs-lookup"><span data-stu-id="b6bc2-136">vary-by-query-parameter</span></span>|<span data-ttu-id="b6bc2-137">Avvia risposte di memorizzazione nella cache per ogni valore dei parametri di query specificati.</span><span class="sxs-lookup"><span data-stu-id="b6bc2-137">Start caching responses per value of specified query parameters.</span></span> <span data-ttu-id="b6bc2-138">Immettere un singolo parametro o più parametri.</span><span class="sxs-lookup"><span data-stu-id="b6bc2-138">Enter a single or multiple parameters.</span></span> <span data-ttu-id="b6bc2-139">Usare un punto e virgola (;) come separatore.</span><span class="sxs-lookup"><span data-stu-id="b6bc2-139">Use semicolon as a separator.</span></span> <span data-ttu-id="b6bc2-140">Se non è specificato alcun nome, verranno usati tutti i parametri di query.</span><span class="sxs-lookup"><span data-stu-id="b6bc2-140">If none are specified, all query parameters are used.</span></span>|<span data-ttu-id="b6bc2-141">No</span><span class="sxs-lookup"><span data-stu-id="b6bc2-141">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="b6bc2-142">Attributi</span><span class="sxs-lookup"><span data-stu-id="b6bc2-142">Attributes</span></span>  
  
|<span data-ttu-id="b6bc2-143">Nome</span><span class="sxs-lookup"><span data-stu-id="b6bc2-143">Name</span></span>|<span data-ttu-id="b6bc2-144">Descrizione</span><span class="sxs-lookup"><span data-stu-id="b6bc2-144">Description</span></span>|<span data-ttu-id="b6bc2-145">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="b6bc2-145">Required</span></span>|<span data-ttu-id="b6bc2-146">Default</span><span class="sxs-lookup"><span data-stu-id="b6bc2-146">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="b6bc2-147">allow-private-response-caching</span><span class="sxs-lookup"><span data-stu-id="b6bc2-147">allow-private-response-caching</span></span>|<span data-ttu-id="b6bc2-148">Se impostato su `true`, consente la memorizzazione nella cache delle richieste contenenti un'intestazione di autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="b6bc2-148">When set to `true`, allows caching of requests that contain an Authorization header.</span></span>|<span data-ttu-id="b6bc2-149">No</span><span class="sxs-lookup"><span data-stu-id="b6bc2-149">No</span></span>|<span data-ttu-id="b6bc2-150">false</span><span class="sxs-lookup"><span data-stu-id="b6bc2-150">false</span></span>|  
|<span data-ttu-id="b6bc2-151">downstream-caching-type</span><span class="sxs-lookup"><span data-stu-id="b6bc2-151">downstream-caching-type</span></span>|<span data-ttu-id="b6bc2-152">Questo attributo deve essere impostato su uno dei valori seguenti.</span><span class="sxs-lookup"><span data-stu-id="b6bc2-152">This attribute must be set to one of the following values.</span></span><br /><br /> <span data-ttu-id="b6bc2-153">-   none - Non è consentita la memorizzazione nella cache downstream.</span><span class="sxs-lookup"><span data-stu-id="b6bc2-153">-   none - downstream caching is not allowed.</span></span><br /><span data-ttu-id="b6bc2-154">-   private - È consentita la memorizzazione nella cache downstream privata.</span><span class="sxs-lookup"><span data-stu-id="b6bc2-154">-   private - downstream private caching is allowed.</span></span><br /><span data-ttu-id="b6bc2-155">-   public - È consentita la memorizzazione nella cache downstream privata e condivisa.</span><span class="sxs-lookup"><span data-stu-id="b6bc2-155">-   public - private and shared downstream caching is allowed.</span></span>|<span data-ttu-id="b6bc2-156">No</span><span class="sxs-lookup"><span data-stu-id="b6bc2-156">No</span></span>|<span data-ttu-id="b6bc2-157">nessuno</span><span class="sxs-lookup"><span data-stu-id="b6bc2-157">none</span></span>|  
|<span data-ttu-id="b6bc2-158">must-revalidate</span><span class="sxs-lookup"><span data-stu-id="b6bc2-158">must-revalidate</span></span>|<span data-ttu-id="b6bc2-159">Quando è abilitata la memorizzazione nella cache downstream, questo attributo attiva o disattiva la direttiva di controllo di memorizzazione della cache `must-revalidate` nelle risposte del gateway.</span><span class="sxs-lookup"><span data-stu-id="b6bc2-159">When downstream caching is enabled this attribute turns on or off  the `must-revalidate` cache control directive in gateway responses.</span></span>|<span data-ttu-id="b6bc2-160">No</span><span class="sxs-lookup"><span data-stu-id="b6bc2-160">No</span></span>|<span data-ttu-id="b6bc2-161">true</span><span class="sxs-lookup"><span data-stu-id="b6bc2-161">true</span></span>|  
|<span data-ttu-id="b6bc2-162">vary-by-developer</span><span class="sxs-lookup"><span data-stu-id="b6bc2-162">vary-by-developer</span></span>|<span data-ttu-id="b6bc2-163">Impostare su `true` per memorizzare le risposte nella cache per ogni chiave sviluppatore.</span><span class="sxs-lookup"><span data-stu-id="b6bc2-163">Set to `true` to cache responses per developer key.</span></span>|<span data-ttu-id="b6bc2-164">No</span><span class="sxs-lookup"><span data-stu-id="b6bc2-164">No</span></span>|<span data-ttu-id="b6bc2-165">false</span><span class="sxs-lookup"><span data-stu-id="b6bc2-165">false</span></span>|  
|<span data-ttu-id="b6bc2-166">vary-by-developer-groups</span><span class="sxs-lookup"><span data-stu-id="b6bc2-166">vary-by-developer-groups</span></span>|<span data-ttu-id="b6bc2-167">Impostare su `true` per memorizzare le risposte nella cache per ogni ruolo utente.</span><span class="sxs-lookup"><span data-stu-id="b6bc2-167">Set to `true` to cache responses per user role.</span></span>|<span data-ttu-id="b6bc2-168">No</span><span class="sxs-lookup"><span data-stu-id="b6bc2-168">No</span></span>|<span data-ttu-id="b6bc2-169">false</span><span class="sxs-lookup"><span data-stu-id="b6bc2-169">false</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="b6bc2-170">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="b6bc2-170">Usage</span></span>  
 <span data-ttu-id="b6bc2-171">Questo criterio può essere usato nelle [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e negli [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) del criterio seguenti.</span><span class="sxs-lookup"><span data-stu-id="b6bc2-171">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="b6bc2-172">**Sezioni del criterio:** in ingresso</span><span class="sxs-lookup"><span data-stu-id="b6bc2-172">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="b6bc2-173">**Ambiti del criterio:** API, operazione, prodotto</span><span class="sxs-lookup"><span data-stu-id="b6bc2-173">**Policy scopes:** API, operation, product</span></span>  
  
##  <span data-ttu-id="b6bc2-174"><a name="StoreToCache"></a> Archivia nella cache</span><span class="sxs-lookup"><span data-stu-id="b6bc2-174"><a name="StoreToCache"></a> Store to cache</span></span>  
 <span data-ttu-id="b6bc2-175">Il criterio `cache-store` memorizza nella cache le risposte in base alle impostazioni specificate per la cache.</span><span class="sxs-lookup"><span data-stu-id="b6bc2-175">The `cache-store` policy caches responses according to the specified cache settings.</span></span> <span data-ttu-id="b6bc2-176">Questo criterio può essere applicato nei casi in cui il contenuto della risposta rimane statico in un periodo di tempo.</span><span class="sxs-lookup"><span data-stu-id="b6bc2-176">This policy can be applied in cases where response content remains static over a period of time.</span></span> <span data-ttu-id="b6bc2-177">La memorizzazione delle risposte nella cache riduce la larghezza di banda e i requisiti di elaborazione imposti sul server Web back-end e riduce la latenza percepita dagli utenti delle API.</span><span class="sxs-lookup"><span data-stu-id="b6bc2-177">Response caching reduces bandwidth and processing requirements imposed on the backend web server and lowers latency perceived by API consumers.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="b6bc2-178">Questo criterio deve essere associato a un criterio [Recupera dalla cache](api-management-caching-policies.md#GetFromCache) corrispondente.</span><span class="sxs-lookup"><span data-stu-id="b6bc2-178">This policy must have a corresponding [Get from cache](api-management-caching-policies.md#GetFromCache) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="b6bc2-179">Istruzione del criterio</span><span class="sxs-lookup"><span data-stu-id="b6bc2-179">Policy statement</span></span>  
  
```xml  
<cache-store duration="seconds" />  
```  
  
### <a name="examples"></a><span data-ttu-id="b6bc2-180">Esempi</span><span class="sxs-lookup"><span data-stu-id="b6bc2-180">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="b6bc2-181">Esempio</span><span class="sxs-lookup"><span data-stu-id="b6bc2-181">Example</span></span>  
  
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
  
#### <a name="example-using-policy-expressions"></a><span data-ttu-id="b6bc2-182">Esempio con espressioni di criteri</span><span class="sxs-lookup"><span data-stu-id="b6bc2-182">Example using policy expressions</span></span>  
 <span data-ttu-id="b6bc2-183">Questo esempio mostra come per configurare la durata della memorizzazione nella cache di Gestione API corrispondente alla memorizzazione delle risposte nella cache del serivzio back-end, come specificato dalla direttiva `Cache-Control` del servizio in questione.</span><span class="sxs-lookup"><span data-stu-id="b6bc2-183">This example shows how to to configure API Management response caching duration that matches the response caching of the backend service as specified by the backed service's `Cache-Control` directive.</span></span> <span data-ttu-id="b6bc2-184">Per una dimostrazione relativa alla configurazione e all'uso di questi criteri, vedere l' [episodio 177 di Cloud Cover su altre funzionalità di Gestione API con Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) e passare direttamente al minuto 25:25.</span><span class="sxs-lookup"><span data-stu-id="b6bc2-184">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 25:25.</span></span>  
  
```xml  
<!-- The following cache policy snippets demonstrate how to control API Management reponse cache duration with Cache-Control headers sent by the backend service. -->  
  
<!-- Copy this snippet into the inbound section -->  
<cache-lookup vary-by-developer="false" vary-by-developer-groups="false" downstream-caching-type="public" must-revalidate="true" >  
  <vary-by-header>Accept</vary-by-header>  
  <vary-by-header>Accept-Charset</vary-by-header>  
</cache-lookup>  
  
<!-- Copy this snippet into the outbound section. Note that cache duration is set to the max-age value provided in the Cache-Control header received from the backend service or to the deafult value of 5 min if none is found  -->  
<cache-store duration="@{  
    var header = context.Response.Headers.GetValueOrDefault("Cache-Control","");  
    var maxAge = Regex.Match(header, @"max-age=(?<maxAge>\d+)").Groups["maxAge"]?.Value;  
    return (!string.IsNullOrEmpty(maxAge))?int.Parse(maxAge):300;  
  }"  
 />  
```  
  
 <span data-ttu-id="b6bc2-185">Per altre informazioni, vedere [Espressioni di criteri](api-management-policy-expressions.md) e [Variabile di contesto](api-management-policy-expressions.md#ContextVariables).</span><span class="sxs-lookup"><span data-stu-id="b6bc2-185">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="b6bc2-186">Elementi</span><span class="sxs-lookup"><span data-stu-id="b6bc2-186">Elements</span></span>  
  
|<span data-ttu-id="b6bc2-187">Nome</span><span class="sxs-lookup"><span data-stu-id="b6bc2-187">Name</span></span>|<span data-ttu-id="b6bc2-188">Descrizione</span><span class="sxs-lookup"><span data-stu-id="b6bc2-188">Description</span></span>|<span data-ttu-id="b6bc2-189">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="b6bc2-189">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="b6bc2-190">cache-store</span><span class="sxs-lookup"><span data-stu-id="b6bc2-190">cache-store</span></span>|<span data-ttu-id="b6bc2-191">Elemento radice.</span><span class="sxs-lookup"><span data-stu-id="b6bc2-191">Root element.</span></span>|<span data-ttu-id="b6bc2-192">Sì</span><span class="sxs-lookup"><span data-stu-id="b6bc2-192">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="b6bc2-193">Attributi</span><span class="sxs-lookup"><span data-stu-id="b6bc2-193">Attributes</span></span>  
  
|<span data-ttu-id="b6bc2-194">Nome</span><span class="sxs-lookup"><span data-stu-id="b6bc2-194">Name</span></span>|<span data-ttu-id="b6bc2-195">Descrizione</span><span class="sxs-lookup"><span data-stu-id="b6bc2-195">Description</span></span>|<span data-ttu-id="b6bc2-196">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="b6bc2-196">Required</span></span>|<span data-ttu-id="b6bc2-197">Default</span><span class="sxs-lookup"><span data-stu-id="b6bc2-197">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="b6bc2-198">duration</span><span class="sxs-lookup"><span data-stu-id="b6bc2-198">duration</span></span>|<span data-ttu-id="b6bc2-199">Durata (TTL, Time-To-Live) delle voci memorizzate nella cache, in secondi.</span><span class="sxs-lookup"><span data-stu-id="b6bc2-199">Time-to-live of the cached entries, specified in seconds.</span></span>|<span data-ttu-id="b6bc2-200">Sì</span><span class="sxs-lookup"><span data-stu-id="b6bc2-200">Yes</span></span>|<span data-ttu-id="b6bc2-201">N/D</span><span class="sxs-lookup"><span data-stu-id="b6bc2-201">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="b6bc2-202">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="b6bc2-202">Usage</span></span>  
 <span data-ttu-id="b6bc2-203">Questo criterio può essere utilizzato nelle [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e negli [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) di criteri seguenti.</span><span class="sxs-lookup"><span data-stu-id="b6bc2-203">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="b6bc2-204">**Sezioni del criterio:** in uscita</span><span class="sxs-lookup"><span data-stu-id="b6bc2-204">**Policy sections:** outbound</span></span>  
  
-   <span data-ttu-id="b6bc2-205">**Ambiti del criterio:** API, operazione, prodotto</span><span class="sxs-lookup"><span data-stu-id="b6bc2-205">**Policy scopes:** API, operation, product</span></span>  
  
##  <span data-ttu-id="b6bc2-206"><a name="GetFromCacheByKey"></a> Recupera valore dalla cache</span><span class="sxs-lookup"><span data-stu-id="b6bc2-206"><a name="GetFromCacheByKey"></a> Get value from cache</span></span>  
 <span data-ttu-id="b6bc2-207">Usare il criterio `cache-lookup-value` per eseguire la ricerca nella cache in base alla chiave e restituiscono un valore memorizzato nella cache.</span><span class="sxs-lookup"><span data-stu-id="b6bc2-207">Use the `cache-lookup-value` policy to perform cache lookup by key and return a cached value.</span></span> <span data-ttu-id="b6bc2-208">La chiave può avere un valore di stringa arbitrario e viene indicata in genere usando un'espressione di criteri.</span><span class="sxs-lookup"><span data-stu-id="b6bc2-208">The key can have an arbitrary string value and is typically provided using a policy expression.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="b6bc2-209">Questo criterio deve essere associato a un criterio [Archivia valore nella cache](#StoreToCacheByKey) corrispondente.</span><span class="sxs-lookup"><span data-stu-id="b6bc2-209">This policy must have a corresponding [Store value in cache](#StoreToCacheByKey) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="b6bc2-210">Istruzione del criterio</span><span class="sxs-lookup"><span data-stu-id="b6bc2-210">Policy statement</span></span>  
  
```xml  
<cache-lookup-value key="cache key value"   
    default-value="value to use if cache lookup resulted in a miss"   
    variable-name="name of a variable looked up value is assigned to" />  
```  
  
### <a name="example"></a><span data-ttu-id="b6bc2-211">Esempio</span><span class="sxs-lookup"><span data-stu-id="b6bc2-211">Example</span></span>  
 <span data-ttu-id="b6bc2-212">Per ulteriori informazioni ed esempi su questo criterio, vedere [Memorizzazione nella cache personalizzata in Gestione API di Azure](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).</span><span class="sxs-lookup"><span data-stu-id="b6bc2-212">For more information and examples of this policy, see [Custom caching in Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).</span></span>  
  
```xml  
<cache-lookup-value  
    key="@("userprofile-" + context.Variables["enduserid"])"    
    variable-name="userprofile" />  
  
```  
  
### <a name="elements"></a><span data-ttu-id="b6bc2-213">Elementi</span><span class="sxs-lookup"><span data-stu-id="b6bc2-213">Elements</span></span>  
  
|<span data-ttu-id="b6bc2-214">Nome</span><span class="sxs-lookup"><span data-stu-id="b6bc2-214">Name</span></span>|<span data-ttu-id="b6bc2-215">Descrizione</span><span class="sxs-lookup"><span data-stu-id="b6bc2-215">Description</span></span>|<span data-ttu-id="b6bc2-216">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="b6bc2-216">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="b6bc2-217">cache-lookup-value</span><span class="sxs-lookup"><span data-stu-id="b6bc2-217">cache-lookup-value</span></span>|<span data-ttu-id="b6bc2-218">Elemento radice.</span><span class="sxs-lookup"><span data-stu-id="b6bc2-218">Root element.</span></span>|<span data-ttu-id="b6bc2-219">Sì</span><span class="sxs-lookup"><span data-stu-id="b6bc2-219">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="b6bc2-220">Attributi</span><span class="sxs-lookup"><span data-stu-id="b6bc2-220">Attributes</span></span>  
  
|<span data-ttu-id="b6bc2-221">Nome</span><span class="sxs-lookup"><span data-stu-id="b6bc2-221">Name</span></span>|<span data-ttu-id="b6bc2-222">Descrizione</span><span class="sxs-lookup"><span data-stu-id="b6bc2-222">Description</span></span>|<span data-ttu-id="b6bc2-223">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="b6bc2-223">Required</span></span>|<span data-ttu-id="b6bc2-224">Default</span><span class="sxs-lookup"><span data-stu-id="b6bc2-224">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="b6bc2-225">default-value</span><span class="sxs-lookup"><span data-stu-id="b6bc2-225">default-value</span></span>|<span data-ttu-id="b6bc2-226">Un valore che verrà assegnato alla variabile se la ricerca della chiave nella cache non produce risultati.</span><span class="sxs-lookup"><span data-stu-id="b6bc2-226">A value that will be assigned to the variable if the cache key lookup resulted in a miss.</span></span> <span data-ttu-id="b6bc2-227">Se questo attributo viene omesso, viene assegnato `null`.</span><span class="sxs-lookup"><span data-stu-id="b6bc2-227">If this attribute is not specified, `null` is assigned.</span></span>|<span data-ttu-id="b6bc2-228">No</span><span class="sxs-lookup"><span data-stu-id="b6bc2-228">No</span></span>|`null`|  
|<span data-ttu-id="b6bc2-229">key</span><span class="sxs-lookup"><span data-stu-id="b6bc2-229">key</span></span>|<span data-ttu-id="b6bc2-230">Valore della chiave della cache da usare nella ricerca.</span><span class="sxs-lookup"><span data-stu-id="b6bc2-230">Cache key value to use in the lookup.</span></span>|<span data-ttu-id="b6bc2-231">Sì</span><span class="sxs-lookup"><span data-stu-id="b6bc2-231">Yes</span></span>|<span data-ttu-id="b6bc2-232">N/D</span><span class="sxs-lookup"><span data-stu-id="b6bc2-232">N/A</span></span>|  
|<span data-ttu-id="b6bc2-233">variable-name</span><span class="sxs-lookup"><span data-stu-id="b6bc2-233">variable-name</span></span>|<span data-ttu-id="b6bc2-234">Nome della [variabile di contesto](api-management-policy-expressions.md#ContextVariables) a cui verrà assegnato il valore cercato, se la ricerca ha esito positivo.</span><span class="sxs-lookup"><span data-stu-id="b6bc2-234">Name of the [context variable](api-management-policy-expressions.md#ContextVariables) the looked up value will be assigned to, if lookup is successful.</span></span> <span data-ttu-id="b6bc2-235">Se la ricerca non produce risultati, alla variabile sarà assegnato il valore dell'attributo `default-value` o `null`, se l'attributo `default-value` è omesso.</span><span class="sxs-lookup"><span data-stu-id="b6bc2-235">If lookup results in a miss, the variable will be assigned the value of the `default-value` attribute or `null`, if the `default-value` attribute is omitted.</span></span>|<span data-ttu-id="b6bc2-236">Sì</span><span class="sxs-lookup"><span data-stu-id="b6bc2-236">Yes</span></span>|<span data-ttu-id="b6bc2-237">N/D</span><span class="sxs-lookup"><span data-stu-id="b6bc2-237">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="b6bc2-238">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="b6bc2-238">Usage</span></span>  
 <span data-ttu-id="b6bc2-239">Questo criterio può essere usato nelle [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e negli [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) del criterio seguenti.</span><span class="sxs-lookup"><span data-stu-id="b6bc2-239">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="b6bc2-240">**Sezioni del criterio:** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="b6bc2-240">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="b6bc2-241">**Ambiti del criterio:** global, API, operation, product</span><span class="sxs-lookup"><span data-stu-id="b6bc2-241">**Policy scopes:** global, API, operation, product</span></span>  
  
##  <span data-ttu-id="b6bc2-242"><a name="StoreToCacheByKey"></a> Archivia valore nella cache</span><span class="sxs-lookup"><span data-stu-id="b6bc2-242"><a name="StoreToCacheByKey"></a> Store value in cache</span></span>  
 <span data-ttu-id="b6bc2-243">`cache-store-value` esegue l'archiviazione nella cache in base alla chiave.</span><span class="sxs-lookup"><span data-stu-id="b6bc2-243">The `cache-store-value` performs cache storage by key.</span></span> <span data-ttu-id="b6bc2-244">La chiave può avere un valore di stringa arbitrario e viene indicata in genere usando un'espressione di criteri.</span><span class="sxs-lookup"><span data-stu-id="b6bc2-244">The key can have an arbitrary string value and is typically provided using a policy expression.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="b6bc2-245">Questo criterio deve essere associato a un criterio [Recupera valore dalla cache](#GetFromCacheByKey) corrispondente.</span><span class="sxs-lookup"><span data-stu-id="b6bc2-245">This policy must have a corresponding [Get value from cache](#GetFromCacheByKey) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="b6bc2-246">Istruzione del criterio</span><span class="sxs-lookup"><span data-stu-id="b6bc2-246">Policy statement</span></span>  
  
```xml  
<cache-store-value key="cache key value" value="value to cache" duration="seconds" />  
```  
  
### <a name="example"></a><span data-ttu-id="b6bc2-247">Esempio</span><span class="sxs-lookup"><span data-stu-id="b6bc2-247">Example</span></span>  
 <span data-ttu-id="b6bc2-248">Per ulteriori informazioni ed esempi su questo criterio, vedere [Memorizzazione nella cache personalizzata in Gestione API di Azure](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).</span><span class="sxs-lookup"><span data-stu-id="b6bc2-248">For more information and examples of this policy, see [Custom caching in Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).</span></span>  
  
```xml  
<cache-store-value  
    key="@("userprofile-" + context.Variables["enduserid"])"  
    value="@((string)context.Variables["userprofile"])" duration="100000" />  
  
```  
  
### <a name="elements"></a><span data-ttu-id="b6bc2-249">Elementi</span><span class="sxs-lookup"><span data-stu-id="b6bc2-249">Elements</span></span>  
  
|<span data-ttu-id="b6bc2-250">Nome</span><span class="sxs-lookup"><span data-stu-id="b6bc2-250">Name</span></span>|<span data-ttu-id="b6bc2-251">Descrizione</span><span class="sxs-lookup"><span data-stu-id="b6bc2-251">Description</span></span>|<span data-ttu-id="b6bc2-252">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="b6bc2-252">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="b6bc2-253">cache-store-value</span><span class="sxs-lookup"><span data-stu-id="b6bc2-253">cache-store-value</span></span>|<span data-ttu-id="b6bc2-254">Elemento radice.</span><span class="sxs-lookup"><span data-stu-id="b6bc2-254">Root element.</span></span>|<span data-ttu-id="b6bc2-255">Sì</span><span class="sxs-lookup"><span data-stu-id="b6bc2-255">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="b6bc2-256">Attributi</span><span class="sxs-lookup"><span data-stu-id="b6bc2-256">Attributes</span></span>  
  
|<span data-ttu-id="b6bc2-257">Nome</span><span class="sxs-lookup"><span data-stu-id="b6bc2-257">Name</span></span>|<span data-ttu-id="b6bc2-258">Descrizione</span><span class="sxs-lookup"><span data-stu-id="b6bc2-258">Description</span></span>|<span data-ttu-id="b6bc2-259">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="b6bc2-259">Required</span></span>|<span data-ttu-id="b6bc2-260">Default</span><span class="sxs-lookup"><span data-stu-id="b6bc2-260">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="b6bc2-261">duration</span><span class="sxs-lookup"><span data-stu-id="b6bc2-261">duration</span></span>|<span data-ttu-id="b6bc2-262">Il valore verrà memorizzato nella cache per il valore di durata specificato, espresso in secondi.</span><span class="sxs-lookup"><span data-stu-id="b6bc2-262">Value will be cached for the provided duration value, specified in seconds.</span></span>|<span data-ttu-id="b6bc2-263">Sì</span><span class="sxs-lookup"><span data-stu-id="b6bc2-263">Yes</span></span>|<span data-ttu-id="b6bc2-264">N/D</span><span class="sxs-lookup"><span data-stu-id="b6bc2-264">N/A</span></span>|  
|<span data-ttu-id="b6bc2-265">key</span><span class="sxs-lookup"><span data-stu-id="b6bc2-265">key</span></span>|<span data-ttu-id="b6bc2-266">La chiave della cache in cui verrà archiviato il valore.</span><span class="sxs-lookup"><span data-stu-id="b6bc2-266">Cache key the value will be stored under.</span></span>|<span data-ttu-id="b6bc2-267">Sì</span><span class="sxs-lookup"><span data-stu-id="b6bc2-267">Yes</span></span>|<span data-ttu-id="b6bc2-268">N/D</span><span class="sxs-lookup"><span data-stu-id="b6bc2-268">N/A</span></span>|  
|<span data-ttu-id="b6bc2-269">value</span><span class="sxs-lookup"><span data-stu-id="b6bc2-269">value</span></span>|<span data-ttu-id="b6bc2-270">Il valore da memorizzare nella cache.</span><span class="sxs-lookup"><span data-stu-id="b6bc2-270">The value to be cached.</span></span>|<span data-ttu-id="b6bc2-271">Sì</span><span class="sxs-lookup"><span data-stu-id="b6bc2-271">Yes</span></span>|<span data-ttu-id="b6bc2-272">N/D</span><span class="sxs-lookup"><span data-stu-id="b6bc2-272">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="b6bc2-273">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="b6bc2-273">Usage</span></span>  
 <span data-ttu-id="b6bc2-274">Questo criterio può essere usato nelle [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e negli [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) del criterio seguenti.</span><span class="sxs-lookup"><span data-stu-id="b6bc2-274">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="b6bc2-275">**Sezioni del criterio:** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="b6bc2-275">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="b6bc2-276">**Ambiti del criterio:** global, API, operation, product</span><span class="sxs-lookup"><span data-stu-id="b6bc2-276">**Policy scopes:** global, API, operation, product</span></span>  
  
###  <span data-ttu-id="b6bc2-277"><a name="RemoveCacheByKey"></a> Rimuovi valore dalla cache</span><span class="sxs-lookup"><span data-stu-id="b6bc2-277"><a name="RemoveCacheByKey"></a> Remove value from cache</span></span>  
 <span data-ttu-id="b6bc2-278">`cache-remove-value` elimina un elemento memorizzato nella cache identificato in base alla chiave.</span><span class="sxs-lookup"><span data-stu-id="b6bc2-278">The             `cache-remove-value` deletes a cached item identified by its key.</span></span> <span data-ttu-id="b6bc2-279">La chiave può avere un valore di stringa arbitrario e viene indicata in genere usando un'espressione di criteri.</span><span class="sxs-lookup"><span data-stu-id="b6bc2-279">The key can have an arbitrary string value and is typically provided using a policy expression.</span></span>  
  
#### <a name="policy-statement"></a><span data-ttu-id="b6bc2-280">Istruzione del criterio</span><span class="sxs-lookup"><span data-stu-id="b6bc2-280">Policy statement</span></span>  
  
```xml  
  
<cache-remove-value key="cache key value"/>  
  
```  
  
#### <a name="example"></a><span data-ttu-id="b6bc2-281">Esempio</span><span class="sxs-lookup"><span data-stu-id="b6bc2-281">Example</span></span>  
  
```xml  
  
<cache-remove-value key="@("userprofile-" + context.Variables["enduserid"])"/>  
  
```  
  
#### <a name="elements"></a><span data-ttu-id="b6bc2-282">Elementi</span><span class="sxs-lookup"><span data-stu-id="b6bc2-282">Elements</span></span>  
  
|<span data-ttu-id="b6bc2-283">Nome</span><span class="sxs-lookup"><span data-stu-id="b6bc2-283">Name</span></span>|<span data-ttu-id="b6bc2-284">Descrizione</span><span class="sxs-lookup"><span data-stu-id="b6bc2-284">Description</span></span>|<span data-ttu-id="b6bc2-285">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="b6bc2-285">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="b6bc2-286">cache-remove-value</span><span class="sxs-lookup"><span data-stu-id="b6bc2-286">cache-remove-value</span></span>|<span data-ttu-id="b6bc2-287">Elemento radice.</span><span class="sxs-lookup"><span data-stu-id="b6bc2-287">Root element.</span></span>|<span data-ttu-id="b6bc2-288">Sì</span><span class="sxs-lookup"><span data-stu-id="b6bc2-288">Yes</span></span>|  
  
#### <a name="attributes"></a><span data-ttu-id="b6bc2-289">Attributi</span><span class="sxs-lookup"><span data-stu-id="b6bc2-289">Attributes</span></span>  
  
|<span data-ttu-id="b6bc2-290">Nome</span><span class="sxs-lookup"><span data-stu-id="b6bc2-290">Name</span></span>|<span data-ttu-id="b6bc2-291">Descrizione</span><span class="sxs-lookup"><span data-stu-id="b6bc2-291">Description</span></span>|<span data-ttu-id="b6bc2-292">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="b6bc2-292">Required</span></span>|<span data-ttu-id="b6bc2-293">Default</span><span class="sxs-lookup"><span data-stu-id="b6bc2-293">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="b6bc2-294">key</span><span class="sxs-lookup"><span data-stu-id="b6bc2-294">key</span></span>|<span data-ttu-id="b6bc2-295">La chiave del valore memorizzato in precedenza nella cache da rimuovere dalla cache.</span><span class="sxs-lookup"><span data-stu-id="b6bc2-295">The key of the previously cached value to be removed from the cache.</span></span>|<span data-ttu-id="b6bc2-296">Sì</span><span class="sxs-lookup"><span data-stu-id="b6bc2-296">Yes</span></span>|<span data-ttu-id="b6bc2-297">N/D</span><span class="sxs-lookup"><span data-stu-id="b6bc2-297">N/A</span></span>|  
  
#### <a name="usage"></a><span data-ttu-id="b6bc2-298">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="b6bc2-298">Usage</span></span>  
 <span data-ttu-id="b6bc2-299">Questo criterio può essere usato nelle [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e negli [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) del criterio seguenti.</span><span class="sxs-lookup"><span data-stu-id="b6bc2-299">This policy can be used in the following policy                    [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and                   [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span></span>  
  
-   <span data-ttu-id="b6bc2-300">**Sezioni del criterio:** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="b6bc2-300">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="b6bc2-301">**Ambiti del criterio:** global, API, operation, product</span><span class="sxs-lookup"><span data-stu-id="b6bc2-301">**Policy scopes:** global, API, operation, product</span></span>  
  

## <a name="next-steps"></a><span data-ttu-id="b6bc2-302">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b6bc2-302">Next steps</span></span>
<span data-ttu-id="b6bc2-303">Per altre informazioni sull'uso dei criteri, vedere [Criteri di Gestione API](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="b6bc2-303">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  