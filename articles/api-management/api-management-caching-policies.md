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
# <a name="api-management-caching-policies"></a><span data-ttu-id="c106e-103">Criteri di memorizzazione nella cache in Gestione API</span><span class="sxs-lookup"><span data-stu-id="c106e-103">API Management caching policies</span></span>
<span data-ttu-id="c106e-104">In questo argomento fornisce un riferimento per i seguenti criteri di gestione API hello.</span><span class="sxs-lookup"><span data-stu-id="c106e-104">This topic provides a reference for hello following API Management policies.</span></span> <span data-ttu-id="c106e-105">Per informazioni sull'aggiunta e sulla configurazione dei criteri, vedere [Criteri di Gestione API](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="c106e-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="c106e-106"><a name="CachingPolicies"></a> Criteri di memorizzazione nella cache</span><span class="sxs-lookup"><span data-stu-id="c106e-106"><a name="CachingPolicies"></a> Caching policies</span></span>  
  
-   <span data-ttu-id="c106e-107">Criteri di memorizzazione nella cache della risposta</span><span class="sxs-lookup"><span data-stu-id="c106e-107">Response caching policies</span></span>  
  
    -   <span data-ttu-id="c106e-108">[Recupera dalla cache](api-management-caching-policies.md#GetFromCache): esegue una ricerca nella cache e restituisce risposte valide memorizzate nella cache, se disponibili.</span><span class="sxs-lookup"><span data-stu-id="c106e-108">[Get from cache](api-management-caching-policies.md#GetFromCache) - Perform cache look up and return a valid cached responses when available.</span></span>  
  
    -   <span data-ttu-id="c106e-109">[Archiviare toocache](api-management-caching-policies.md#StoreToCache) - risposte memorizza nella cache in base di configurazione del controllo toohello della cache specificata.</span><span class="sxs-lookup"><span data-stu-id="c106e-109">[Store toocache](api-management-caching-policies.md#StoreToCache) - Caches responses according toohello specified cache control configuration.</span></span>  
  
-   <span data-ttu-id="c106e-110">Criteri di memorizzazione dei valori nella cache</span><span class="sxs-lookup"><span data-stu-id="c106e-110">Value caching policies</span></span>  
  
    -   <span data-ttu-id="c106e-111">[Recupera valore dalla cache](#GetFromCacheByKey) : recupera un elemento memorizzato nella cache per chiave.</span><span class="sxs-lookup"><span data-stu-id="c106e-111">[Get value from cache](#GetFromCacheByKey) - Retrieve a cached item by key.</span></span>  
  
    -   <span data-ttu-id="c106e-112">[Valore di memorizzare nella cache](#StoreToCacheByKey) -archiviare un elemento nella cache di hello dalla chiave.</span><span class="sxs-lookup"><span data-stu-id="c106e-112">[Store value in cache](#StoreToCacheByKey) - Store an item in hello cache by key.</span></span>  
  
    -   <span data-ttu-id="c106e-113">[Rimuovi valore dalla cache](#RemoveCacheByKey) -rimuovere un elemento nella cache di hello dalla chiave.</span><span class="sxs-lookup"><span data-stu-id="c106e-113">[Remove value from cache](#RemoveCacheByKey) - Remove an item in hello cache by key.</span></span>  
  
##  <span data-ttu-id="c106e-114"><a name="GetFromCache"></a> Recupera dalla cache</span><span class="sxs-lookup"><span data-stu-id="c106e-114"><a name="GetFromCache"></a> Get from cache</span></span>  
 <span data-ttu-id="c106e-115">Hello utilizzare `cache-lookup` tooperform cache dei criteri di cercare e restituire una risposta memorizzata nella cache valida, se disponibile.</span><span class="sxs-lookup"><span data-stu-id="c106e-115">Use hello `cache-lookup` policy tooperform cache look up and return a valid cached response when available.</span></span> <span data-ttu-id="c106e-116">Questo criterio può essere applicato nei casi in cui il contenuto della risposta rimane statico in un periodo di tempo.</span><span class="sxs-lookup"><span data-stu-id="c106e-116">This policy can be applied in cases where response content remains static over a period of time.</span></span> <span data-ttu-id="c106e-117">Risposta di memorizzazione nella cache riduce la larghezza di banda e requisiti di elaborazione imposto a hello back-end web server e diminuisce la latenza percepita dagli utenti delle API.</span><span class="sxs-lookup"><span data-stu-id="c106e-117">Response caching reduces bandwidth and processing requirements imposed on hello backend web server and lowers latency perceived by API consumers.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="c106e-118">Questo criterio deve avere una corrispondente [toocache archivio](api-management-caching-policies.md#StoreToCache) criteri.</span><span class="sxs-lookup"><span data-stu-id="c106e-118">This policy must have a corresponding [Store toocache](api-management-caching-policies.md#StoreToCache) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="c106e-119">Istruzione del criterio</span><span class="sxs-lookup"><span data-stu-id="c106e-119">Policy statement</span></span>  
  
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
  
### <a name="examples"></a><span data-ttu-id="c106e-120">Esempi</span><span class="sxs-lookup"><span data-stu-id="c106e-120">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="c106e-121">Esempio</span><span class="sxs-lookup"><span data-stu-id="c106e-121">Example</span></span>  
  
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
  
#### <a name="example-using-policy-expressions"></a><span data-ttu-id="c106e-122">Esempio con espressioni di criteri</span><span class="sxs-lookup"><span data-stu-id="c106e-122">Example using policy expressions</span></span>  
 <span data-ttu-id="c106e-123">Questo esempio viene illustrato come risposta di gestione API tootooconfigure la memorizzazione nella cache di durata che corrispondenze hello la memorizzazione nella cache di risposta del servizio back-end hello come specificato da hello backup del servizio `Cache-Control` direttiva.</span><span class="sxs-lookup"><span data-stu-id="c106e-123">This example shows how tootooconfigure API Management response caching duration that matches hello response caching of hello backend service as specified by hello backed service's `Cache-Control` directive.</span></span> <span data-ttu-id="c106e-124">Per una dimostrazione della configurazione e l'utilizzo di questo criterio, vedere [Cloud coprire episodio 177: più API le funzionalità di gestione con Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) e far avanzare rapidamente too25:25.</span><span class="sxs-lookup"><span data-stu-id="c106e-124">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too25:25.</span></span>  
  
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
  
 <span data-ttu-id="c106e-125">Per altre informazioni, vedere [Espressioni di criteri](api-management-policy-expressions.md) e [Variabile di contesto](api-management-policy-expressions.md#ContextVariables).</span><span class="sxs-lookup"><span data-stu-id="c106e-125">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="c106e-126">Elementi</span><span class="sxs-lookup"><span data-stu-id="c106e-126">Elements</span></span>  
  
|<span data-ttu-id="c106e-127">Nome</span><span class="sxs-lookup"><span data-stu-id="c106e-127">Name</span></span>|<span data-ttu-id="c106e-128">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c106e-128">Description</span></span>|<span data-ttu-id="c106e-129">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="c106e-129">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="c106e-130">cache-lookup</span><span class="sxs-lookup"><span data-stu-id="c106e-130">cache-lookup</span></span>|<span data-ttu-id="c106e-131">Elemento radice.</span><span class="sxs-lookup"><span data-stu-id="c106e-131">Root element.</span></span>|<span data-ttu-id="c106e-132">Sì</span><span class="sxs-lookup"><span data-stu-id="c106e-132">Yes</span></span>|  
|<span data-ttu-id="c106e-133">vary-by-header</span><span class="sxs-lookup"><span data-stu-id="c106e-133">vary-by-header</span></span>|<span data-ttu-id="c106e-134">Avviare la memorizzazione delle risposte nella cache per ogni valore dell'intestazione specificata, come ad esempio Accept, Accept-Charset, Accept-Encoding, Accept-Language, Authorization, Expect, From, Host e If-Match.</span><span class="sxs-lookup"><span data-stu-id="c106e-134">Start caching responses per value of specified header, such as Accept, Accept-Charset, Accept-Encoding, Accept-Language, Authorization, Expect, From, Host, If-Match.</span></span>|<span data-ttu-id="c106e-135">No</span><span class="sxs-lookup"><span data-stu-id="c106e-135">No</span></span>|  
|<span data-ttu-id="c106e-136">vary-by-query-parameter</span><span class="sxs-lookup"><span data-stu-id="c106e-136">vary-by-query-parameter</span></span>|<span data-ttu-id="c106e-137">Avvia risposte di memorizzazione nella cache per ogni valore dei parametri di query specificati.</span><span class="sxs-lookup"><span data-stu-id="c106e-137">Start caching responses per value of specified query parameters.</span></span> <span data-ttu-id="c106e-138">Immettere un singolo parametro o più parametri.</span><span class="sxs-lookup"><span data-stu-id="c106e-138">Enter a single or multiple parameters.</span></span> <span data-ttu-id="c106e-139">Usare un punto e virgola (;) come separatore.</span><span class="sxs-lookup"><span data-stu-id="c106e-139">Use semicolon as a separator.</span></span> <span data-ttu-id="c106e-140">Se non è specificato alcun nome, verranno usati tutti i parametri di query.</span><span class="sxs-lookup"><span data-stu-id="c106e-140">If none are specified, all query parameters are used.</span></span>|<span data-ttu-id="c106e-141">No</span><span class="sxs-lookup"><span data-stu-id="c106e-141">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="c106e-142">Attributi</span><span class="sxs-lookup"><span data-stu-id="c106e-142">Attributes</span></span>  
  
|<span data-ttu-id="c106e-143">Nome</span><span class="sxs-lookup"><span data-stu-id="c106e-143">Name</span></span>|<span data-ttu-id="c106e-144">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c106e-144">Description</span></span>|<span data-ttu-id="c106e-145">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="c106e-145">Required</span></span>|<span data-ttu-id="c106e-146">Default</span><span class="sxs-lookup"><span data-stu-id="c106e-146">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="c106e-147">allow-private-response-caching</span><span class="sxs-lookup"><span data-stu-id="c106e-147">allow-private-response-caching</span></span>|<span data-ttu-id="c106e-148">Quando impostato troppo`true`, consente la memorizzazione nella cache le richieste che contengono un'intestazione di autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="c106e-148">When set too`true`, allows caching of requests that contain an Authorization header.</span></span>|<span data-ttu-id="c106e-149">No</span><span class="sxs-lookup"><span data-stu-id="c106e-149">No</span></span>|<span data-ttu-id="c106e-150">false</span><span class="sxs-lookup"><span data-stu-id="c106e-150">false</span></span>|  
|<span data-ttu-id="c106e-151">downstream-caching-type</span><span class="sxs-lookup"><span data-stu-id="c106e-151">downstream-caching-type</span></span>|<span data-ttu-id="c106e-152">Questo attributo deve essere impostato tooone dei seguenti valori hello.</span><span class="sxs-lookup"><span data-stu-id="c106e-152">This attribute must be set tooone of hello following values.</span></span><br /><br /> <span data-ttu-id="c106e-153">-   none - Non è consentita la memorizzazione nella cache downstream.</span><span class="sxs-lookup"><span data-stu-id="c106e-153">-   none - downstream caching is not allowed.</span></span><br /><span data-ttu-id="c106e-154">-   private - È consentita la memorizzazione nella cache downstream privata.</span><span class="sxs-lookup"><span data-stu-id="c106e-154">-   private - downstream private caching is allowed.</span></span><br /><span data-ttu-id="c106e-155">-   public - È consentita la memorizzazione nella cache downstream privata e condivisa.</span><span class="sxs-lookup"><span data-stu-id="c106e-155">-   public - private and shared downstream caching is allowed.</span></span>|<span data-ttu-id="c106e-156">No</span><span class="sxs-lookup"><span data-stu-id="c106e-156">No</span></span>|<span data-ttu-id="c106e-157">nessuno</span><span class="sxs-lookup"><span data-stu-id="c106e-157">none</span></span>|  
|<span data-ttu-id="c106e-158">must-revalidate</span><span class="sxs-lookup"><span data-stu-id="c106e-158">must-revalidate</span></span>|<span data-ttu-id="c106e-159">Quando è abilitata la memorizzazione nella cache downstream questo attributo attiva o disattiva hello `must-revalidate` direttiva di controllo della cache nelle risposte di gateway.</span><span class="sxs-lookup"><span data-stu-id="c106e-159">When downstream caching is enabled this attribute turns on or off  hello `must-revalidate` cache control directive in gateway responses.</span></span>|<span data-ttu-id="c106e-160">No</span><span class="sxs-lookup"><span data-stu-id="c106e-160">No</span></span>|<span data-ttu-id="c106e-161">true</span><span class="sxs-lookup"><span data-stu-id="c106e-161">true</span></span>|  
|<span data-ttu-id="c106e-162">vary-by-developer</span><span class="sxs-lookup"><span data-stu-id="c106e-162">vary-by-developer</span></span>|<span data-ttu-id="c106e-163">Impostare troppo`true` toocache le risposte per ogni chiave sviluppatore.</span><span class="sxs-lookup"><span data-stu-id="c106e-163">Set too`true` toocache responses per developer key.</span></span>|<span data-ttu-id="c106e-164">No</span><span class="sxs-lookup"><span data-stu-id="c106e-164">No</span></span>|<span data-ttu-id="c106e-165">false</span><span class="sxs-lookup"><span data-stu-id="c106e-165">false</span></span>|  
|<span data-ttu-id="c106e-166">vary-by-developer-groups</span><span class="sxs-lookup"><span data-stu-id="c106e-166">vary-by-developer-groups</span></span>|<span data-ttu-id="c106e-167">Impostare troppo`true` risposte toocache al ruolo utente.</span><span class="sxs-lookup"><span data-stu-id="c106e-167">Set too`true` toocache responses per user role.</span></span>|<span data-ttu-id="c106e-168">No</span><span class="sxs-lookup"><span data-stu-id="c106e-168">No</span></span>|<span data-ttu-id="c106e-169">false</span><span class="sxs-lookup"><span data-stu-id="c106e-169">false</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="c106e-170">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="c106e-170">Usage</span></span>  
 <span data-ttu-id="c106e-171">Questo criterio può essere utilizzato hello seguenti criteri [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="c106e-171">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="c106e-172">**Sezioni del criterio:** inbound</span><span class="sxs-lookup"><span data-stu-id="c106e-172">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="c106e-173">**Ambiti del criterio:** API, operazione, prodotto</span><span class="sxs-lookup"><span data-stu-id="c106e-173">**Policy scopes:** API, operation, product</span></span>  
  
##  <span data-ttu-id="c106e-174"><a name="StoreToCache"></a>Archivio toocache</span><span class="sxs-lookup"><span data-stu-id="c106e-174"><a name="StoreToCache"></a> Store toocache</span></span>  
 <span data-ttu-id="c106e-175">Hello `cache-store` risposte memorizza nella cache dei criteri in base toohello specificato le impostazioni della cache.</span><span class="sxs-lookup"><span data-stu-id="c106e-175">hello `cache-store` policy caches responses according toohello specified cache settings.</span></span> <span data-ttu-id="c106e-176">Questo criterio può essere applicato nei casi in cui il contenuto della risposta rimane statico in un periodo di tempo.</span><span class="sxs-lookup"><span data-stu-id="c106e-176">This policy can be applied in cases where response content remains static over a period of time.</span></span> <span data-ttu-id="c106e-177">Risposta di memorizzazione nella cache riduce la larghezza di banda e requisiti di elaborazione imposto a hello back-end web server e diminuisce la latenza percepita dagli utenti delle API.</span><span class="sxs-lookup"><span data-stu-id="c106e-177">Response caching reduces bandwidth and processing requirements imposed on hello backend web server and lowers latency perceived by API consumers.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="c106e-178">Questo criterio deve essere associato a un criterio [Recupera dalla cache](api-management-caching-policies.md#GetFromCache) corrispondente.</span><span class="sxs-lookup"><span data-stu-id="c106e-178">This policy must have a corresponding [Get from cache](api-management-caching-policies.md#GetFromCache) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="c106e-179">Istruzione del criterio</span><span class="sxs-lookup"><span data-stu-id="c106e-179">Policy statement</span></span>  
  
```xml  
<cache-store duration="seconds" />  
```  
  
### <a name="examples"></a><span data-ttu-id="c106e-180">Esempi</span><span class="sxs-lookup"><span data-stu-id="c106e-180">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="c106e-181">Esempio</span><span class="sxs-lookup"><span data-stu-id="c106e-181">Example</span></span>  
  
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
  
#### <a name="example-using-policy-expressions"></a><span data-ttu-id="c106e-182">Esempio con espressioni di criteri</span><span class="sxs-lookup"><span data-stu-id="c106e-182">Example using policy expressions</span></span>  
 <span data-ttu-id="c106e-183">Questo esempio viene illustrato come risposta di gestione API tootooconfigure la memorizzazione nella cache di durata che corrispondenze hello la memorizzazione nella cache di risposta del servizio back-end hello come specificato da hello backup del servizio `Cache-Control` direttiva.</span><span class="sxs-lookup"><span data-stu-id="c106e-183">This example shows how tootooconfigure API Management response caching duration that matches hello response caching of hello backend service as specified by hello backed service's `Cache-Control` directive.</span></span> <span data-ttu-id="c106e-184">Per una dimostrazione della configurazione e l'utilizzo di questo criterio, vedere [Cloud coprire episodio 177: più API le funzionalità di gestione con Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) e far avanzare rapidamente too25:25.</span><span class="sxs-lookup"><span data-stu-id="c106e-184">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too25:25.</span></span>  
  
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
  
 <span data-ttu-id="c106e-185">Per altre informazioni, vedere [Espressioni di criteri](api-management-policy-expressions.md) e [Variabile di contesto](api-management-policy-expressions.md#ContextVariables).</span><span class="sxs-lookup"><span data-stu-id="c106e-185">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="c106e-186">Elementi</span><span class="sxs-lookup"><span data-stu-id="c106e-186">Elements</span></span>  
  
|<span data-ttu-id="c106e-187">Nome</span><span class="sxs-lookup"><span data-stu-id="c106e-187">Name</span></span>|<span data-ttu-id="c106e-188">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c106e-188">Description</span></span>|<span data-ttu-id="c106e-189">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="c106e-189">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="c106e-190">cache-store</span><span class="sxs-lookup"><span data-stu-id="c106e-190">cache-store</span></span>|<span data-ttu-id="c106e-191">Elemento radice.</span><span class="sxs-lookup"><span data-stu-id="c106e-191">Root element.</span></span>|<span data-ttu-id="c106e-192">Sì</span><span class="sxs-lookup"><span data-stu-id="c106e-192">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="c106e-193">Attributi</span><span class="sxs-lookup"><span data-stu-id="c106e-193">Attributes</span></span>  
  
|<span data-ttu-id="c106e-194">Nome</span><span class="sxs-lookup"><span data-stu-id="c106e-194">Name</span></span>|<span data-ttu-id="c106e-195">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c106e-195">Description</span></span>|<span data-ttu-id="c106e-196">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="c106e-196">Required</span></span>|<span data-ttu-id="c106e-197">Default</span><span class="sxs-lookup"><span data-stu-id="c106e-197">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="c106e-198">duration</span><span class="sxs-lookup"><span data-stu-id="c106e-198">duration</span></span>|<span data-ttu-id="c106e-199">Time-to-live di hello memorizzati nella cache di voci, espresso in secondi.</span><span class="sxs-lookup"><span data-stu-id="c106e-199">Time-to-live of hello cached entries, specified in seconds.</span></span>|<span data-ttu-id="c106e-200">Sì</span><span class="sxs-lookup"><span data-stu-id="c106e-200">Yes</span></span>|<span data-ttu-id="c106e-201">N/D</span><span class="sxs-lookup"><span data-stu-id="c106e-201">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="c106e-202">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="c106e-202">Usage</span></span>  
 <span data-ttu-id="c106e-203">Questo criterio può essere utilizzato hello seguenti criteri [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="c106e-203">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="c106e-204">**Sezioni del criterio:** in uscita</span><span class="sxs-lookup"><span data-stu-id="c106e-204">**Policy sections:** outbound</span></span>  
  
-   <span data-ttu-id="c106e-205">**Ambiti del criterio:** API, operazione, prodotto</span><span class="sxs-lookup"><span data-stu-id="c106e-205">**Policy scopes:** API, operation, product</span></span>  
  
##  <span data-ttu-id="c106e-206"><a name="GetFromCacheByKey"></a> Recupera valore dalla cache</span><span class="sxs-lookup"><span data-stu-id="c106e-206"><a name="GetFromCacheByKey"></a> Get value from cache</span></span>  
 <span data-ttu-id="c106e-207">Hello utilizzare `cache-lookup-value` tooperform criteri nella cache di ricerca dalla chiave e restituire un valore memorizzato nella cache.</span><span class="sxs-lookup"><span data-stu-id="c106e-207">Use hello `cache-lookup-value` policy tooperform cache lookup by key and return a cached value.</span></span> <span data-ttu-id="c106e-208">chiave di Hello può avere un valore stringa arbitrario e viene in genere fornito con un'espressione di criteri.</span><span class="sxs-lookup"><span data-stu-id="c106e-208">hello key can have an arbitrary string value and is typically provided using a policy expression.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="c106e-209">Questo criterio deve essere associato a un criterio [Archivia valore nella cache](#StoreToCacheByKey) corrispondente.</span><span class="sxs-lookup"><span data-stu-id="c106e-209">This policy must have a corresponding [Store value in cache](#StoreToCacheByKey) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="c106e-210">Istruzione del criterio</span><span class="sxs-lookup"><span data-stu-id="c106e-210">Policy statement</span></span>  
  
```xml  
<cache-lookup-value key="cache key value"   
    default-value="value toouse if cache lookup resulted in a miss"   
    variable-name="name of a variable looked up value is assigned to" />  
```  
  
### <a name="example"></a><span data-ttu-id="c106e-211">Esempio</span><span class="sxs-lookup"><span data-stu-id="c106e-211">Example</span></span>  
 <span data-ttu-id="c106e-212">Per ulteriori informazioni ed esempi su questo criterio, vedere [Memorizzazione nella cache personalizzata in Gestione API di Azure](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).</span><span class="sxs-lookup"><span data-stu-id="c106e-212">For more information and examples of this policy, see [Custom caching in Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).</span></span>  
  
```xml  
<cache-lookup-value  
    key="@("userprofile-" + context.Variables["enduserid"])"    
    variable-name="userprofile" />  
  
```  
  
### <a name="elements"></a><span data-ttu-id="c106e-213">Elementi</span><span class="sxs-lookup"><span data-stu-id="c106e-213">Elements</span></span>  
  
|<span data-ttu-id="c106e-214">Nome</span><span class="sxs-lookup"><span data-stu-id="c106e-214">Name</span></span>|<span data-ttu-id="c106e-215">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c106e-215">Description</span></span>|<span data-ttu-id="c106e-216">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="c106e-216">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="c106e-217">cache-lookup-value</span><span class="sxs-lookup"><span data-stu-id="c106e-217">cache-lookup-value</span></span>|<span data-ttu-id="c106e-218">Elemento radice.</span><span class="sxs-lookup"><span data-stu-id="c106e-218">Root element.</span></span>|<span data-ttu-id="c106e-219">Sì</span><span class="sxs-lookup"><span data-stu-id="c106e-219">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="c106e-220">Attributi</span><span class="sxs-lookup"><span data-stu-id="c106e-220">Attributes</span></span>  
  
|<span data-ttu-id="c106e-221">Nome</span><span class="sxs-lookup"><span data-stu-id="c106e-221">Name</span></span>|<span data-ttu-id="c106e-222">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c106e-222">Description</span></span>|<span data-ttu-id="c106e-223">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="c106e-223">Required</span></span>|<span data-ttu-id="c106e-224">Default</span><span class="sxs-lookup"><span data-stu-id="c106e-224">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="c106e-225">default-value</span><span class="sxs-lookup"><span data-stu-id="c106e-225">default-value</span></span>|<span data-ttu-id="c106e-226">Un valore che verrà assegnato toohello variabile se ricerca chiave nella cache di hello ha prodotto un mancato riscontro.</span><span class="sxs-lookup"><span data-stu-id="c106e-226">A value that will be assigned toohello variable if hello cache key lookup resulted in a miss.</span></span> <span data-ttu-id="c106e-227">Se questo attributo viene omesso, viene assegnato `null`.</span><span class="sxs-lookup"><span data-stu-id="c106e-227">If this attribute is not specified, `null` is assigned.</span></span>|<span data-ttu-id="c106e-228">No</span><span class="sxs-lookup"><span data-stu-id="c106e-228">No</span></span>|`null`|  
|<span data-ttu-id="c106e-229">key</span><span class="sxs-lookup"><span data-stu-id="c106e-229">key</span></span>|<span data-ttu-id="c106e-230">Valore della chiave toouse nella ricerca hello la cache.</span><span class="sxs-lookup"><span data-stu-id="c106e-230">Cache key value toouse in hello lookup.</span></span>|<span data-ttu-id="c106e-231">Sì</span><span class="sxs-lookup"><span data-stu-id="c106e-231">Yes</span></span>|<span data-ttu-id="c106e-232">N/D</span><span class="sxs-lookup"><span data-stu-id="c106e-232">N/A</span></span>|  
|<span data-ttu-id="c106e-233">variable-name</span><span class="sxs-lookup"><span data-stu-id="c106e-233">variable-name</span></span>|<span data-ttu-id="c106e-234">Nome di hello [variabile di contesto](api-management-policy-expressions.md#ContextVariables) hello cercato valore verrà assegnato a, se la ricerca ha esito positivo.</span><span class="sxs-lookup"><span data-stu-id="c106e-234">Name of hello [context variable](api-management-policy-expressions.md#ContextVariables) hello looked up value will be assigned to, if lookup is successful.</span></span> <span data-ttu-id="c106e-235">Se i risultati di ricerca in un mancato riscontro, variabile hello verrà assegnato il valore di hello di hello `default-value` attributo o `null`, se hello `default-value` attributo viene omesso.</span><span class="sxs-lookup"><span data-stu-id="c106e-235">If lookup results in a miss, hello variable will be assigned hello value of hello `default-value` attribute or `null`, if hello `default-value` attribute is omitted.</span></span>|<span data-ttu-id="c106e-236">Sì</span><span class="sxs-lookup"><span data-stu-id="c106e-236">Yes</span></span>|<span data-ttu-id="c106e-237">N/D</span><span class="sxs-lookup"><span data-stu-id="c106e-237">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="c106e-238">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="c106e-238">Usage</span></span>  
 <span data-ttu-id="c106e-239">Questo criterio può essere utilizzato hello seguenti criteri [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="c106e-239">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="c106e-240">**Sezioni del criterio:** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="c106e-240">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="c106e-241">**Ambiti del criterio:** global, API, operation, product</span><span class="sxs-lookup"><span data-stu-id="c106e-241">**Policy scopes:** global, API, operation, product</span></span>  
  
##  <span data-ttu-id="c106e-242"><a name="StoreToCacheByKey"></a> Archivia valore nella cache</span><span class="sxs-lookup"><span data-stu-id="c106e-242"><a name="StoreToCacheByKey"></a> Store value in cache</span></span>  
 <span data-ttu-id="c106e-243">Hello `cache-store-value` esegue l'archiviazione cache dalla chiave.</span><span class="sxs-lookup"><span data-stu-id="c106e-243">hello `cache-store-value` performs cache storage by key.</span></span> <span data-ttu-id="c106e-244">chiave di Hello può avere un valore stringa arbitrario e viene in genere fornito con un'espressione di criteri.</span><span class="sxs-lookup"><span data-stu-id="c106e-244">hello key can have an arbitrary string value and is typically provided using a policy expression.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="c106e-245">Questo criterio deve essere associato a un criterio [Recupera valore dalla cache](#GetFromCacheByKey) corrispondente.</span><span class="sxs-lookup"><span data-stu-id="c106e-245">This policy must have a corresponding [Get value from cache](#GetFromCacheByKey) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="c106e-246">Istruzione del criterio</span><span class="sxs-lookup"><span data-stu-id="c106e-246">Policy statement</span></span>  
  
```xml  
<cache-store-value key="cache key value" value="value toocache" duration="seconds" />  
```  
  
### <a name="example"></a><span data-ttu-id="c106e-247">Esempio</span><span class="sxs-lookup"><span data-stu-id="c106e-247">Example</span></span>  
 <span data-ttu-id="c106e-248">Per ulteriori informazioni ed esempi su questo criterio, vedere [Memorizzazione nella cache personalizzata in Gestione API di Azure](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).</span><span class="sxs-lookup"><span data-stu-id="c106e-248">For more information and examples of this policy, see [Custom caching in Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).</span></span>  
  
```xml  
<cache-store-value  
    key="@("userprofile-" + context.Variables["enduserid"])"  
    value="@((string)context.Variables["userprofile"])" duration="100000" />  
  
```  
  
### <a name="elements"></a><span data-ttu-id="c106e-249">Elementi</span><span class="sxs-lookup"><span data-stu-id="c106e-249">Elements</span></span>  
  
|<span data-ttu-id="c106e-250">Nome</span><span class="sxs-lookup"><span data-stu-id="c106e-250">Name</span></span>|<span data-ttu-id="c106e-251">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c106e-251">Description</span></span>|<span data-ttu-id="c106e-252">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="c106e-252">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="c106e-253">cache-store-value</span><span class="sxs-lookup"><span data-stu-id="c106e-253">cache-store-value</span></span>|<span data-ttu-id="c106e-254">Elemento radice.</span><span class="sxs-lookup"><span data-stu-id="c106e-254">Root element.</span></span>|<span data-ttu-id="c106e-255">Sì</span><span class="sxs-lookup"><span data-stu-id="c106e-255">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="c106e-256">Attributi</span><span class="sxs-lookup"><span data-stu-id="c106e-256">Attributes</span></span>  
  
|<span data-ttu-id="c106e-257">Nome</span><span class="sxs-lookup"><span data-stu-id="c106e-257">Name</span></span>|<span data-ttu-id="c106e-258">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c106e-258">Description</span></span>|<span data-ttu-id="c106e-259">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="c106e-259">Required</span></span>|<span data-ttu-id="c106e-260">Default</span><span class="sxs-lookup"><span data-stu-id="c106e-260">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="c106e-261">duration</span><span class="sxs-lookup"><span data-stu-id="c106e-261">duration</span></span>|<span data-ttu-id="c106e-262">Valore verrà memorizzato nella cache di hello fornito il valore di durata, espresso in secondi.</span><span class="sxs-lookup"><span data-stu-id="c106e-262">Value will be cached for hello provided duration value, specified in seconds.</span></span>|<span data-ttu-id="c106e-263">Sì</span><span class="sxs-lookup"><span data-stu-id="c106e-263">Yes</span></span>|<span data-ttu-id="c106e-264">N/D</span><span class="sxs-lookup"><span data-stu-id="c106e-264">N/A</span></span>|  
|<span data-ttu-id="c106e-265">key</span><span class="sxs-lookup"><span data-stu-id="c106e-265">key</span></span>|<span data-ttu-id="c106e-266">Il valore di chiave hello cache verrà archiviato in.</span><span class="sxs-lookup"><span data-stu-id="c106e-266">Cache key hello value will be stored under.</span></span>|<span data-ttu-id="c106e-267">Sì</span><span class="sxs-lookup"><span data-stu-id="c106e-267">Yes</span></span>|<span data-ttu-id="c106e-268">N/D</span><span class="sxs-lookup"><span data-stu-id="c106e-268">N/A</span></span>|  
|<span data-ttu-id="c106e-269">value</span><span class="sxs-lookup"><span data-stu-id="c106e-269">value</span></span>|<span data-ttu-id="c106e-270">Hello toobe di valore memorizzato nella cache.</span><span class="sxs-lookup"><span data-stu-id="c106e-270">hello value toobe cached.</span></span>|<span data-ttu-id="c106e-271">Sì</span><span class="sxs-lookup"><span data-stu-id="c106e-271">Yes</span></span>|<span data-ttu-id="c106e-272">N/D</span><span class="sxs-lookup"><span data-stu-id="c106e-272">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="c106e-273">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="c106e-273">Usage</span></span>  
 <span data-ttu-id="c106e-274">Questo criterio può essere utilizzato hello seguenti criteri [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="c106e-274">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="c106e-275">**Sezioni del criterio:** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="c106e-275">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="c106e-276">**Ambiti del criterio:** global, API, operation, product</span><span class="sxs-lookup"><span data-stu-id="c106e-276">**Policy scopes:** global, API, operation, product</span></span>  
  
###  <span data-ttu-id="c106e-277"><a name="RemoveCacheByKey"></a> Rimuovi valore dalla cache</span><span class="sxs-lookup"><span data-stu-id="c106e-277"><a name="RemoveCacheByKey"></a> Remove value from cache</span></span>  
 <span data-ttu-id="c106e-278">Hello `cache-remove-value` Elimina un elemento memorizzato nella cache identificato in base alla chiave.</span><span class="sxs-lookup"><span data-stu-id="c106e-278">hello             `cache-remove-value` deletes a cached item identified by its key.</span></span> <span data-ttu-id="c106e-279">chiave di Hello può avere un valore stringa arbitrario e viene in genere fornito con un'espressione di criteri.</span><span class="sxs-lookup"><span data-stu-id="c106e-279">hello key can have an arbitrary string value and is typically provided using a policy expression.</span></span>  
  
#### <a name="policy-statement"></a><span data-ttu-id="c106e-280">Istruzione del criterio</span><span class="sxs-lookup"><span data-stu-id="c106e-280">Policy statement</span></span>  
  
```xml  
  
<cache-remove-value key="cache key value"/>  
  
```  
  
#### <a name="example"></a><span data-ttu-id="c106e-281">Esempio</span><span class="sxs-lookup"><span data-stu-id="c106e-281">Example</span></span>  
  
```xml  
  
<cache-remove-value key="@("userprofile-" + context.Variables["enduserid"])"/>  
  
```  
  
#### <a name="elements"></a><span data-ttu-id="c106e-282">Elementi</span><span class="sxs-lookup"><span data-stu-id="c106e-282">Elements</span></span>  
  
|<span data-ttu-id="c106e-283">Nome</span><span class="sxs-lookup"><span data-stu-id="c106e-283">Name</span></span>|<span data-ttu-id="c106e-284">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c106e-284">Description</span></span>|<span data-ttu-id="c106e-285">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="c106e-285">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="c106e-286">cache-remove-value</span><span class="sxs-lookup"><span data-stu-id="c106e-286">cache-remove-value</span></span>|<span data-ttu-id="c106e-287">Elemento radice.</span><span class="sxs-lookup"><span data-stu-id="c106e-287">Root element.</span></span>|<span data-ttu-id="c106e-288">Sì</span><span class="sxs-lookup"><span data-stu-id="c106e-288">Yes</span></span>|  
  
#### <a name="attributes"></a><span data-ttu-id="c106e-289">Attributi</span><span class="sxs-lookup"><span data-stu-id="c106e-289">Attributes</span></span>  
  
|<span data-ttu-id="c106e-290">Nome</span><span class="sxs-lookup"><span data-stu-id="c106e-290">Name</span></span>|<span data-ttu-id="c106e-291">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c106e-291">Description</span></span>|<span data-ttu-id="c106e-292">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="c106e-292">Required</span></span>|<span data-ttu-id="c106e-293">Default</span><span class="sxs-lookup"><span data-stu-id="c106e-293">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="c106e-294">key</span><span class="sxs-lookup"><span data-stu-id="c106e-294">key</span></span>|<span data-ttu-id="c106e-295">chiave di Hello di hello memorizzata nella cache toobe valore rimosso dalla cache di hello.</span><span class="sxs-lookup"><span data-stu-id="c106e-295">hello key of hello previously cached value toobe removed from hello cache.</span></span>|<span data-ttu-id="c106e-296">Sì</span><span class="sxs-lookup"><span data-stu-id="c106e-296">Yes</span></span>|<span data-ttu-id="c106e-297">N/D</span><span class="sxs-lookup"><span data-stu-id="c106e-297">N/A</span></span>|  
  
#### <a name="usage"></a><span data-ttu-id="c106e-298">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="c106e-298">Usage</span></span>  
 <span data-ttu-id="c106e-299">Questo criterio può essere utilizzato hello seguenti criteri [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span><span class="sxs-lookup"><span data-stu-id="c106e-299">This policy can be used in hello following policy                    [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and                   [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span></span>  
  
-   <span data-ttu-id="c106e-300">**Sezioni del criterio:** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="c106e-300">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="c106e-301">**Ambiti del criterio:** global, API, operation, product</span><span class="sxs-lookup"><span data-stu-id="c106e-301">**Policy scopes:** global, API, operation, product</span></span>  
  

## <a name="next-steps"></a><span data-ttu-id="c106e-302">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c106e-302">Next steps</span></span>
<span data-ttu-id="c106e-303">Per altre informazioni sull'uso dei criteri, vedere [Criteri di Gestione API](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="c106e-303">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  