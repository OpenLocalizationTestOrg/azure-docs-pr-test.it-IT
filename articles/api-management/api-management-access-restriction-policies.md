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
# <a name="api-management-access-restriction-policies"></a><span data-ttu-id="055cf-103">Criteri di limitazione dell'accesso di Gestione API</span><span class="sxs-lookup"><span data-stu-id="055cf-103">API Management access restriction policies</span></span>
<span data-ttu-id="055cf-104">In questo argomento fornisce un riferimento per i seguenti criteri di gestione API hello.</span><span class="sxs-lookup"><span data-stu-id="055cf-104">This topic provides a reference for hello following API Management policies.</span></span> <span data-ttu-id="055cf-105">Per informazioni sull'aggiunta e sulla configurazione dei criteri, vedere [Criteri di Gestione API](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="055cf-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="055cf-106"><a name="AccessRestrictionPolicies"></a> Criteri di limitazione dell'accesso</span><span class="sxs-lookup"><span data-stu-id="055cf-106"><a name="AccessRestrictionPolicies"></a> Access restriction policies</span></span>  
  
-   <span data-ttu-id="055cf-107">[check-header](api-management-access-restriction-policies.md#CheckHTTPHeader) : impone l'esistenza e/o il valore di un'intestazione HTTP.</span><span class="sxs-lookup"><span data-stu-id="055cf-107">[Check HTTP header](api-management-access-restriction-policies.md#CheckHTTPHeader) - Enforces existence and/or value of a HTTP Header.</span></span>  
  
-   <span data-ttu-id="055cf-108">[Limita frequenza delle chiamate per sottoscrizione](api-management-access-restriction-policies.md#LimitCallRate) : impedisce picchi di utilizzo delle API limitando la frequenza delle chiamate per ogni sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="055cf-108">[Limit call rate by subscription](api-management-access-restriction-policies.md#LimitCallRate) - Prevents API usage spikes by limiting call rate, on a per subscription basis.</span></span>  
  
-   <span data-ttu-id="055cf-109">[Limita frequenza delle chiamate per chiave](#LimitCallRateByKey) : impedisce picchi di utilizzo delle API limitando la frequenza delle chiamata, per ogni chiave.</span><span class="sxs-lookup"><span data-stu-id="055cf-109">[Limit call rate by key](#LimitCallRateByKey) - Prevents API usage spikes by limiting call rate, on a per key basis.</span></span>  
  
-   <span data-ttu-id="055cf-110">[ip-filter](api-management-access-restriction-policies.md#RestrictCallerIPs) : filtra (permette/rifiuta) le chiamate provenienti da indirizzi IP e/o intervalli di indirizzi IP specifici.</span><span class="sxs-lookup"><span data-stu-id="055cf-110">[Restrict caller IPs](api-management-access-restriction-policies.md#RestrictCallerIPs) - Filters (allows/denies) calls from specific IP addresses and/or address ranges.</span></span>  
  
-   <span data-ttu-id="055cf-111">[Quota di utilizzo di set da sottoscrizione](api-management-access-restriction-policies.md#SetUsageQuota) -consente tooenforce una quota rinnovabile o permanente chiamata volume e/o della larghezza di banda, in base a una per ogni sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="055cf-111">[Set usage quota by subscription](api-management-access-restriction-policies.md#SetUsageQuota) - Allows you tooenforce a renewable or lifetime call volume and/or bandwidth quota, on a per subscription basis.</span></span>  
  
-   <span data-ttu-id="055cf-112">[Quota di utilizzo di set da chiave](#SetUsageQuotaByKey) -consente tooenforce una quota rinnovabile o permanente chiamata volume e/o della larghezza di banda, in una base per ogni chiave.</span><span class="sxs-lookup"><span data-stu-id="055cf-112">[Set usage quota by key](#SetUsageQuotaByKey) - Allows you tooenforce a renewable or lifetime call volume and/or bandwidth quota, on a per key basis.</span></span>  
  
-   <span data-ttu-id="055cf-113">[validate-JWT](api-management-access-restriction-policies.md#ValidateJWT) : impone l'esistenza e la validità di un token JWT estratto da un'intestazione HTTP specificata o da un parametro di query specificato.</span><span class="sxs-lookup"><span data-stu-id="055cf-113">[Validate JWT](api-management-access-restriction-policies.md#ValidateJWT) - Enforces existence and validity of a JWT extracted from either a specified HTTP Header or a specified query parameter.</span></span>  
  
##  <span data-ttu-id="055cf-114"><a name="CheckHTTPHeader"></a> Intestazione check-header</span><span class="sxs-lookup"><span data-stu-id="055cf-114"><a name="CheckHTTPHeader"></a> Check HTTP header</span></span>  
 <span data-ttu-id="055cf-115">Hello utilizzare `check-header` tooenforce criteri che una richiesta presenta un'intestazione HTTP specificata.</span><span class="sxs-lookup"><span data-stu-id="055cf-115">Use hello `check-header` policy tooenforce that a request has a specified HTTP header.</span></span> <span data-ttu-id="055cf-116">È possibile controllare toosee se intestazione hello ha un valore specifico o per un intervallo di valori consentiti.</span><span class="sxs-lookup"><span data-stu-id="055cf-116">You can optionally check toosee if hello header has a specific value or check for a range of allowed values.</span></span> <span data-ttu-id="055cf-117">Se il controllo di hello non riesce, criteri hello termina l'elaborazione della richiesta e restituisce hello codice di errore e messaggio di stato HTTP specificato dai criteri di hello.</span><span class="sxs-lookup"><span data-stu-id="055cf-117">If hello check fails, hello policy terminates request processing and returns hello HTTP status code and error message specified by hello policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="055cf-118">Istruzione del criterio</span><span class="sxs-lookup"><span data-stu-id="055cf-118">Policy statement</span></span>  
  
```xml  
<check-header name="header name" failed-check-httpcode="code" failed-check-error-message="message" ignore-case="True">  
    <value>Value1</value>  
    <value>Value2</value>  
</check-header>  
```  
  
### <a name="example"></a><span data-ttu-id="055cf-119">Esempio</span><span class="sxs-lookup"><span data-stu-id="055cf-119">Example</span></span>  
  
```xml  
<check-header name="Authorization" failed-check-httpcode="401" failed-check-error-message="Not authorized" ignore-case="false">  
    <value>f6dc69a089844cf6b2019bae6d36fac8</value>  
</check-header>  
```  
  
### <a name="elements"></a><span data-ttu-id="055cf-120">Elementi</span><span class="sxs-lookup"><span data-stu-id="055cf-120">Elements</span></span>  
  
|<span data-ttu-id="055cf-121">Nome</span><span class="sxs-lookup"><span data-stu-id="055cf-121">Name</span></span>|<span data-ttu-id="055cf-122">Descrizione</span><span class="sxs-lookup"><span data-stu-id="055cf-122">Description</span></span>|<span data-ttu-id="055cf-123">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="055cf-123">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="055cf-124">check-header</span><span class="sxs-lookup"><span data-stu-id="055cf-124">check-header</span></span>|<span data-ttu-id="055cf-125">Elemento radice.</span><span class="sxs-lookup"><span data-stu-id="055cf-125">Root element.</span></span>|<span data-ttu-id="055cf-126">Sì</span><span class="sxs-lookup"><span data-stu-id="055cf-126">Yes</span></span>|  
|<span data-ttu-id="055cf-127">value</span><span class="sxs-lookup"><span data-stu-id="055cf-127">value</span></span>|<span data-ttu-id="055cf-128">Valore dell'intestazione HTTP consentito.</span><span class="sxs-lookup"><span data-stu-id="055cf-128">Allowed HTTP header value.</span></span> <span data-ttu-id="055cf-129">Quando vengono specificati più elementi di valore, controllo hello viene considerato un caso di esito positivo se uno dei valori hello è una corrispondenza.</span><span class="sxs-lookup"><span data-stu-id="055cf-129">When multiple value elements are specified, hello check is considered a success if any one of hello values is a match.</span></span>|<span data-ttu-id="055cf-130">No</span><span class="sxs-lookup"><span data-stu-id="055cf-130">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="055cf-131">Attributi</span><span class="sxs-lookup"><span data-stu-id="055cf-131">Attributes</span></span>  
  
|<span data-ttu-id="055cf-132">Nome</span><span class="sxs-lookup"><span data-stu-id="055cf-132">Name</span></span>|<span data-ttu-id="055cf-133">Descrizione</span><span class="sxs-lookup"><span data-stu-id="055cf-133">Description</span></span>|<span data-ttu-id="055cf-134">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="055cf-134">Required</span></span>|<span data-ttu-id="055cf-135">Default</span><span class="sxs-lookup"><span data-stu-id="055cf-135">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="055cf-136">failed-check-error-message</span><span class="sxs-lookup"><span data-stu-id="055cf-136">failed-check-error-message</span></span>|<span data-ttu-id="055cf-137">Tooreturn messaggio di errore nel corpo della risposta HTTP hello se l'intestazione di hello non esiste o non ha un valore non valido.</span><span class="sxs-lookup"><span data-stu-id="055cf-137">Error message tooreturn in hello HTTP response body if hello header doesn't exist or has an invalid value.</span></span> <span data-ttu-id="055cf-138">I caratteri speciali eventualmente contenuti in questo messaggio devono essere adeguatamente preceduti da un carattere di escape.</span><span class="sxs-lookup"><span data-stu-id="055cf-138">This message must have any special characters properly escaped.</span></span>|<span data-ttu-id="055cf-139">Sì</span><span class="sxs-lookup"><span data-stu-id="055cf-139">Yes</span></span>|<span data-ttu-id="055cf-140">N/D</span><span class="sxs-lookup"><span data-stu-id="055cf-140">N/A</span></span>|  
|<span data-ttu-id="055cf-141">failed-check-httpcode</span><span class="sxs-lookup"><span data-stu-id="055cf-141">failed-check-httpcode</span></span>|<span data-ttu-id="055cf-142">Codice di stato HTTP tooreturn se l'intestazione di hello non esiste o non ha un valore non valido.</span><span class="sxs-lookup"><span data-stu-id="055cf-142">HTTP Status code tooreturn if hello header doesn't exist or has an invalid value.</span></span>|<span data-ttu-id="055cf-143">Sì</span><span class="sxs-lookup"><span data-stu-id="055cf-143">Yes</span></span>|<span data-ttu-id="055cf-144">N/D</span><span class="sxs-lookup"><span data-stu-id="055cf-144">N/A</span></span>|  
|<span data-ttu-id="055cf-145">header-name</span><span class="sxs-lookup"><span data-stu-id="055cf-145">header-name</span></span>|<span data-ttu-id="055cf-146">nome Hello di hello toocheck intestazione HTTP.</span><span class="sxs-lookup"><span data-stu-id="055cf-146">hello name of hello HTTP Header toocheck.</span></span>|<span data-ttu-id="055cf-147">Sì</span><span class="sxs-lookup"><span data-stu-id="055cf-147">Yes</span></span>|<span data-ttu-id="055cf-148">N/D</span><span class="sxs-lookup"><span data-stu-id="055cf-148">N/A</span></span>|  
|<span data-ttu-id="055cf-149">ignore-case</span><span class="sxs-lookup"><span data-stu-id="055cf-149">ignore-case</span></span>|<span data-ttu-id="055cf-150">Può essere impostato tooTrue o False.</span><span class="sxs-lookup"><span data-stu-id="055cf-150">Can be set tooTrue or False.</span></span> <span data-ttu-id="055cf-151">Se il case tooTrue set viene ignorato quando il valore di intestazione hello viene confrontato con il set di hello di valori accettabili.</span><span class="sxs-lookup"><span data-stu-id="055cf-151">If set tooTrue case is ignored when hello header value is compared against hello set of acceptable values.</span></span>|<span data-ttu-id="055cf-152">Sì</span><span class="sxs-lookup"><span data-stu-id="055cf-152">Yes</span></span>|<span data-ttu-id="055cf-153">N/D</span><span class="sxs-lookup"><span data-stu-id="055cf-153">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="055cf-154">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="055cf-154">Usage</span></span>  
 <span data-ttu-id="055cf-155">Questo criterio può essere utilizzato hello seguenti criteri [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="055cf-155">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="055cf-156">**Sezioni del criterio:** inbound, outbound</span><span class="sxs-lookup"><span data-stu-id="055cf-156">**Policy sections:** inbound, outbound</span></span>  
  
-   <span data-ttu-id="055cf-157">**Ambiti del criterio:** globale, prodotto, API, operazione</span><span class="sxs-lookup"><span data-stu-id="055cf-157">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="055cf-158"><a name="LimitCallRate"></a> Limita frequenza delle chiamate per sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="055cf-158"><a name="LimitCallRate"></a> Limit call rate by subscription</span></span>  
 <span data-ttu-id="055cf-159">Hello `rate-limit` criteri impediscono l'utilizzo di API picchi in una per ogni singola sottoscrizione limitando hello chiamare tooa di frequenza specificato numero per un periodo di tempo specificato.</span><span class="sxs-lookup"><span data-stu-id="055cf-159">hello `rate-limit` policy prevents API usage spikes on a per subscription basis by limiting hello call rate tooa specified number per a specified time period.</span></span> <span data-ttu-id="055cf-160">Quando viene attivato il criterio chiamante hello riceve un `429 Too Many Requests` codice di stato della risposta.</span><span class="sxs-lookup"><span data-stu-id="055cf-160">When this policy is triggered hello caller receives a `429 Too Many Requests` response status code.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="055cf-161">Questo criterio può essere impiegato una sola volta per ogni documento dei criteri.</span><span class="sxs-lookup"><span data-stu-id="055cf-161">This policy can be used only once per policy document.</span></span>  
>   
>  <span data-ttu-id="055cf-162">[Espressioni di criteri](api-management-policy-expressions.md) non può essere usata in qualsiasi degli attributi di hello criteri per i criteri.</span><span class="sxs-lookup"><span data-stu-id="055cf-162">[Policy expressions](api-management-policy-expressions.md) cannot be used in any of hello policy attributes for this policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="055cf-163">Istruzione del criterio</span><span class="sxs-lookup"><span data-stu-id="055cf-163">Policy statement</span></span>  
  
```xml  
<rate-limit calls="number" renewal-period="seconds">  
    <api name="name" calls="number" renewal-period="seconds">  
        <operation name="name" calls="number" renewal-period="seconds" />  
    </api>  
</rate-limit>  
```  
  
### <a name="example"></a><span data-ttu-id="055cf-164">Esempio</span><span class="sxs-lookup"><span data-stu-id="055cf-164">Example</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="055cf-165">Elementi</span><span class="sxs-lookup"><span data-stu-id="055cf-165">Elements</span></span>  
  
|<span data-ttu-id="055cf-166">Nome</span><span class="sxs-lookup"><span data-stu-id="055cf-166">Name</span></span>|<span data-ttu-id="055cf-167">Descrizione</span><span class="sxs-lookup"><span data-stu-id="055cf-167">Description</span></span>|<span data-ttu-id="055cf-168">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="055cf-168">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="055cf-169">set-limit</span><span class="sxs-lookup"><span data-stu-id="055cf-169">set-limit</span></span>|<span data-ttu-id="055cf-170">Elemento radice.</span><span class="sxs-lookup"><span data-stu-id="055cf-170">Root element.</span></span>|<span data-ttu-id="055cf-171">Sì</span><span class="sxs-lookup"><span data-stu-id="055cf-171">Yes</span></span>|  
|<span data-ttu-id="055cf-172">api</span><span class="sxs-lookup"><span data-stu-id="055cf-172">api</span></span>|<span data-ttu-id="055cf-173">Aggiungere uno o più di questi tooimpose elementi un limite di frequenza delle chiamate alle API all'interno del prodotto hello.</span><span class="sxs-lookup"><span data-stu-id="055cf-173">Add one  or more of these elements tooimpose a call rate limit on APIs within hello product.</span></span> <span data-ttu-id="055cf-174">I limiti alla frequenza delle chiamate API e al prodotto vengono applicati in modo indipendente.</span><span class="sxs-lookup"><span data-stu-id="055cf-174">Product and API call rate limits are applied independently.</span></span>|<span data-ttu-id="055cf-175">No</span><span class="sxs-lookup"><span data-stu-id="055cf-175">No</span></span>|  
|<span data-ttu-id="055cf-176">operation</span><span class="sxs-lookup"><span data-stu-id="055cf-176">operation</span></span>|<span data-ttu-id="055cf-177">Aggiungere uno o più di questi tooimpose elementi un limite di frequenza delle chiamate per le operazioni in un'API.</span><span class="sxs-lookup"><span data-stu-id="055cf-177">Add one  or more of these elements tooimpose a call rate limit on operations within an API.</span></span> <span data-ttu-id="055cf-178">I limiti alla frequenza delle chiamate alle operazioni, all'API e al prodotto vengono applicati in modo indipendente.</span><span class="sxs-lookup"><span data-stu-id="055cf-178">Product, API, and operation call rate limits are applied independently.</span></span>|<span data-ttu-id="055cf-179">No</span><span class="sxs-lookup"><span data-stu-id="055cf-179">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="055cf-180">Attributi</span><span class="sxs-lookup"><span data-stu-id="055cf-180">Attributes</span></span>  
  
|<span data-ttu-id="055cf-181">Nome</span><span class="sxs-lookup"><span data-stu-id="055cf-181">Name</span></span>|<span data-ttu-id="055cf-182">Descrizione</span><span class="sxs-lookup"><span data-stu-id="055cf-182">Description</span></span>|<span data-ttu-id="055cf-183">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="055cf-183">Required</span></span>|<span data-ttu-id="055cf-184">Default</span><span class="sxs-lookup"><span data-stu-id="055cf-184">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="055cf-185">name</span><span class="sxs-lookup"><span data-stu-id="055cf-185">name</span></span>|<span data-ttu-id="055cf-186">nome di Hello di hello API per il limite di velocità tooapply hello.</span><span class="sxs-lookup"><span data-stu-id="055cf-186">hello name of hello API for which tooapply hello rate limit.</span></span>|<span data-ttu-id="055cf-187">Sì</span><span class="sxs-lookup"><span data-stu-id="055cf-187">Yes</span></span>|<span data-ttu-id="055cf-188">N/D</span><span class="sxs-lookup"><span data-stu-id="055cf-188">N/A</span></span>|  
|<span data-ttu-id="055cf-189">calls</span><span class="sxs-lookup"><span data-stu-id="055cf-189">calls</span></span>|<span data-ttu-id="055cf-190">numero massimo di chiamate consentite durante l'intervallo di tempo hello specificato in hello Hello `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="055cf-190">hello maximum total number of calls allowed during hello time interval specified in hello `renewal-period`.</span></span>|<span data-ttu-id="055cf-191">Sì</span><span class="sxs-lookup"><span data-stu-id="055cf-191">Yes</span></span>|<span data-ttu-id="055cf-192">N/D</span><span class="sxs-lookup"><span data-stu-id="055cf-192">N/A</span></span>|  
|<span data-ttu-id="055cf-193">renewal-period</span><span class="sxs-lookup"><span data-stu-id="055cf-193">renewal-period</span></span>|<span data-ttu-id="055cf-194">Hello periodo di tempo in secondi dopo il quale hello quota viene reimpostata.</span><span class="sxs-lookup"><span data-stu-id="055cf-194">hello time period in seconds after which hello quota resets.</span></span>|<span data-ttu-id="055cf-195">Sì</span><span class="sxs-lookup"><span data-stu-id="055cf-195">Yes</span></span>|<span data-ttu-id="055cf-196">N/D</span><span class="sxs-lookup"><span data-stu-id="055cf-196">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="055cf-197">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="055cf-197">Usage</span></span>  
 <span data-ttu-id="055cf-198">Questo criterio può essere utilizzato hello seguenti criteri [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="055cf-198">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="055cf-199">**Sezioni del criterio:** inbound</span><span class="sxs-lookup"><span data-stu-id="055cf-199">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="055cf-200">**Ambiti del criterio:** prodotto</span><span class="sxs-lookup"><span data-stu-id="055cf-200">**Policy scopes:** product</span></span>  
  
##  <span data-ttu-id="055cf-201"><a name="LimitCallRateByKey"></a> Limita la frequenza delle chiamate per chiave</span><span class="sxs-lookup"><span data-stu-id="055cf-201"><a name="LimitCallRateByKey"></a> Limit call rate by key</span></span>  
 <span data-ttu-id="055cf-202">Hello `rate-limit-by-key` criteri impediscono l'utilizzo di API picchi di base per ogni chiave limitando hello chiamare tooa di frequenza specificato numero per un periodo di tempo specificato.</span><span class="sxs-lookup"><span data-stu-id="055cf-202">hello `rate-limit-by-key` policy prevents API usage spikes on a per key basis by limiting hello call rate tooa specified number per a specified time period.</span></span> <span data-ttu-id="055cf-203">chiave di Hello può avere un valore stringa arbitrario e viene in genere fornito con un'espressione di criteri.</span><span class="sxs-lookup"><span data-stu-id="055cf-203">hello key can have an arbitrary string value and is typically provided using a policy expression.</span></span> <span data-ttu-id="055cf-204">È possibile aggiungere toospecify le richieste devono essere conteggiate per limite hello condizione incrementale facoltativo.</span><span class="sxs-lookup"><span data-stu-id="055cf-204">Optional increment condition can be added toospecify which requests should be counted towards hello limit.</span></span> <span data-ttu-id="055cf-205">Quando viene attivato il criterio chiamante hello riceve un `429 Too Many Requests` codice di stato della risposta.</span><span class="sxs-lookup"><span data-stu-id="055cf-205">When this policy is triggered hello caller receives a `429 Too Many Requests` response status code.</span></span>  
  
 <span data-ttu-id="055cf-206">Per altre informazioni ed esempi su questo criterio, vedere [Advanced request throttling with Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/) (Limitazione avanzata delle richieste con Gestione API di Azure).</span><span class="sxs-lookup"><span data-stu-id="055cf-206">For more information and examples of this policy, see [Advanced request throttling with Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="055cf-207">Questo criterio può essere impiegato una sola volta per ogni documento dei criteri.</span><span class="sxs-lookup"><span data-stu-id="055cf-207">This policy can be used only once per policy document.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="055cf-208">Istruzione del criterio</span><span class="sxs-lookup"><span data-stu-id="055cf-208">Policy statement</span></span>  
  
```xml  
<rate-limit-by-key calls="number"  
                   renewal-period="seconds"   
                   increment-condition="condition"   
                   counter-key="key value" />  
  
```  
  
### <a name="example"></a><span data-ttu-id="055cf-209">Esempio</span><span class="sxs-lookup"><span data-stu-id="055cf-209">Example</span></span>  
 <span data-ttu-id="055cf-210">Nel seguente esempio di hello, il limite di velocità di hello è codificato in base all'indirizzo IP hello chiamante.</span><span class="sxs-lookup"><span data-stu-id="055cf-210">In hello following example, hello rate limit is keyed by hello caller IP address.</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="055cf-211">Elementi</span><span class="sxs-lookup"><span data-stu-id="055cf-211">Elements</span></span>  
  
|<span data-ttu-id="055cf-212">Nome</span><span class="sxs-lookup"><span data-stu-id="055cf-212">Name</span></span>|<span data-ttu-id="055cf-213">Descrizione</span><span class="sxs-lookup"><span data-stu-id="055cf-213">Description</span></span>|<span data-ttu-id="055cf-214">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="055cf-214">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="055cf-215">set-limit</span><span class="sxs-lookup"><span data-stu-id="055cf-215">set-limit</span></span>|<span data-ttu-id="055cf-216">Elemento radice.</span><span class="sxs-lookup"><span data-stu-id="055cf-216">Root element.</span></span>|<span data-ttu-id="055cf-217">Sì</span><span class="sxs-lookup"><span data-stu-id="055cf-217">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="055cf-218">Attributi</span><span class="sxs-lookup"><span data-stu-id="055cf-218">Attributes</span></span>  
  
|<span data-ttu-id="055cf-219">Nome</span><span class="sxs-lookup"><span data-stu-id="055cf-219">Name</span></span>|<span data-ttu-id="055cf-220">Descrizione</span><span class="sxs-lookup"><span data-stu-id="055cf-220">Description</span></span>|<span data-ttu-id="055cf-221">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="055cf-221">Required</span></span>|<span data-ttu-id="055cf-222">Default</span><span class="sxs-lookup"><span data-stu-id="055cf-222">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="055cf-223">calls</span><span class="sxs-lookup"><span data-stu-id="055cf-223">calls</span></span>|<span data-ttu-id="055cf-224">numero massimo di chiamate consentite durante l'intervallo di tempo hello specificato in hello Hello `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="055cf-224">hello maximum total number of calls allowed during hello time interval specified in hello `renewal-period`.</span></span>|<span data-ttu-id="055cf-225">Sì</span><span class="sxs-lookup"><span data-stu-id="055cf-225">Yes</span></span>|<span data-ttu-id="055cf-226">N/D</span><span class="sxs-lookup"><span data-stu-id="055cf-226">N/A</span></span>|  
|<span data-ttu-id="055cf-227">counter-key</span><span class="sxs-lookup"><span data-stu-id="055cf-227">counter-key</span></span>|<span data-ttu-id="055cf-228">Hello toouse chiave per i criteri di limite di frequenza hello.</span><span class="sxs-lookup"><span data-stu-id="055cf-228">hello key toouse for hello rate limit policy.</span></span>|<span data-ttu-id="055cf-229">Sì</span><span class="sxs-lookup"><span data-stu-id="055cf-229">Yes</span></span>|<span data-ttu-id="055cf-230">N/D</span><span class="sxs-lookup"><span data-stu-id="055cf-230">N/A</span></span>|  
|<span data-ttu-id="055cf-231">increment-condition</span><span class="sxs-lookup"><span data-stu-id="055cf-231">increment-condition</span></span>|<span data-ttu-id="055cf-232">espressione di Hello booleana che specifica se la richiesta hello conteggiata quota hello (`true`).</span><span class="sxs-lookup"><span data-stu-id="055cf-232">hello boolean expression specifying if hello request should be counted towards hello quota (`true`).</span></span>|<span data-ttu-id="055cf-233">No</span><span class="sxs-lookup"><span data-stu-id="055cf-233">No</span></span>|<span data-ttu-id="055cf-234">N/D</span><span class="sxs-lookup"><span data-stu-id="055cf-234">N/A</span></span>|  
|<span data-ttu-id="055cf-235">renewal-period</span><span class="sxs-lookup"><span data-stu-id="055cf-235">renewal-period</span></span>|<span data-ttu-id="055cf-236">Hello periodo di tempo in secondi dopo il quale hello quota viene reimpostata.</span><span class="sxs-lookup"><span data-stu-id="055cf-236">hello time period in seconds after which hello quota resets.</span></span>|<span data-ttu-id="055cf-237">Sì</span><span class="sxs-lookup"><span data-stu-id="055cf-237">Yes</span></span>|<span data-ttu-id="055cf-238">N/D</span><span class="sxs-lookup"><span data-stu-id="055cf-238">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="055cf-239">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="055cf-239">Usage</span></span>  
 <span data-ttu-id="055cf-240">Questo criterio può essere utilizzato hello seguenti criteri [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="055cf-240">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="055cf-241">**Sezioni del criterio:** inbound</span><span class="sxs-lookup"><span data-stu-id="055cf-241">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="055cf-242">**Ambiti del criterio:** globale, prodotto, API, operazione</span><span class="sxs-lookup"><span data-stu-id="055cf-242">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="055cf-243"><a name="RestrictCallerIPs"></a> ip-filter</span><span class="sxs-lookup"><span data-stu-id="055cf-243"><a name="RestrictCallerIPs"></a> Restrict caller IPs</span></span>  
 <span data-ttu-id="055cf-244">Hello `ip-filter` criteri Filtra (consente/Rifiuta) le chiamate da indirizzi IP specifici e/o intervalli di indirizzi.</span><span class="sxs-lookup"><span data-stu-id="055cf-244">hello `ip-filter` policy filters (allows/denies) calls from specific IP addresses and/or address ranges.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="055cf-245">Istruzione del criterio</span><span class="sxs-lookup"><span data-stu-id="055cf-245">Policy statement</span></span>  
  
```xml  
<ip-filter action="allow | forbid">  
    <address>address</address>  
    <address-range from="address" to="address" />  
</ip-filter>  
```  
  
### <a name="example"></a><span data-ttu-id="055cf-246">Esempio</span><span class="sxs-lookup"><span data-stu-id="055cf-246">Example</span></span>  
  
```xml  
<ip-filter action="allow | forbid">  
    <address>address</address>  
    <address-range from="address" to="address" />  
</ip-filter>  
```  
  
### <a name="elements"></a><span data-ttu-id="055cf-247">Elementi</span><span class="sxs-lookup"><span data-stu-id="055cf-247">Elements</span></span>  
  
|<span data-ttu-id="055cf-248">Nome</span><span class="sxs-lookup"><span data-stu-id="055cf-248">Name</span></span>|<span data-ttu-id="055cf-249">Descrizione</span><span class="sxs-lookup"><span data-stu-id="055cf-249">Description</span></span>|<span data-ttu-id="055cf-250">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="055cf-250">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="055cf-251">ip-filter</span><span class="sxs-lookup"><span data-stu-id="055cf-251">ip-filter</span></span>|<span data-ttu-id="055cf-252">Elemento radice.</span><span class="sxs-lookup"><span data-stu-id="055cf-252">Root element.</span></span>|<span data-ttu-id="055cf-253">Sì</span><span class="sxs-lookup"><span data-stu-id="055cf-253">Yes</span></span>|  
|<span data-ttu-id="055cf-254">Address</span><span class="sxs-lookup"><span data-stu-id="055cf-254">address</span></span>|<span data-ttu-id="055cf-255">Specifica un singolo indirizzo IP su cui toofilter.</span><span class="sxs-lookup"><span data-stu-id="055cf-255">Specifies a single IP address on which toofilter.</span></span>|<span data-ttu-id="055cf-256">È obbligatorio almeno un elemento `address` o `address-range`.</span><span class="sxs-lookup"><span data-stu-id="055cf-256">At least one `address` or `address-range` element is required.</span></span>|  
|<span data-ttu-id="055cf-257">address-range from="address" to="address"</span><span class="sxs-lookup"><span data-stu-id="055cf-257">address-range from="address" to="address"</span></span>|<span data-ttu-id="055cf-258">Specifica un intervallo di indirizzi IP in quale toofilter.</span><span class="sxs-lookup"><span data-stu-id="055cf-258">Specifies a range of IP address on which toofilter.</span></span>|<span data-ttu-id="055cf-259">È obbligatorio almeno un elemento `address` o `address-range`.</span><span class="sxs-lookup"><span data-stu-id="055cf-259">At least one `address` or `address-range` element is required.</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="055cf-260">Attributi</span><span class="sxs-lookup"><span data-stu-id="055cf-260">Attributes</span></span>  
  
|<span data-ttu-id="055cf-261">Nome</span><span class="sxs-lookup"><span data-stu-id="055cf-261">Name</span></span>|<span data-ttu-id="055cf-262">Descrizione</span><span class="sxs-lookup"><span data-stu-id="055cf-262">Description</span></span>|<span data-ttu-id="055cf-263">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="055cf-263">Required</span></span>|<span data-ttu-id="055cf-264">Default</span><span class="sxs-lookup"><span data-stu-id="055cf-264">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="055cf-265">address-range from="address" to="address"</span><span class="sxs-lookup"><span data-stu-id="055cf-265">address-range from="address" to="address"</span></span>|<span data-ttu-id="055cf-266">Un intervallo di indirizzi IP, indirizzi tooallow o negare l'accesso.</span><span class="sxs-lookup"><span data-stu-id="055cf-266">A range of IP addresses tooallow or deny access for.</span></span>|<span data-ttu-id="055cf-267">Obbligatorio quando hello `address-range` viene utilizzato l'elemento.</span><span class="sxs-lookup"><span data-stu-id="055cf-267">Required when hello `address-range` element is used.</span></span>|<span data-ttu-id="055cf-268">N/D</span><span class="sxs-lookup"><span data-stu-id="055cf-268">N/A</span></span>|  
|<span data-ttu-id="055cf-269">ip-filter action="allow &#124; forbid"</span><span class="sxs-lookup"><span data-stu-id="055cf-269">ip-filter action="allow &#124; forbid"</span></span>|<span data-ttu-id="055cf-270">Specifica se le chiamate devono essere consentite o non per hello specificato gli indirizzi IP e gli intervalli.</span><span class="sxs-lookup"><span data-stu-id="055cf-270">Specifies whether calls should be allowed or not for hello specified IP addresses and ranges.</span></span>|<span data-ttu-id="055cf-271">Sì</span><span class="sxs-lookup"><span data-stu-id="055cf-271">Yes</span></span>|<span data-ttu-id="055cf-272">N/D</span><span class="sxs-lookup"><span data-stu-id="055cf-272">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="055cf-273">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="055cf-273">Usage</span></span>  
 <span data-ttu-id="055cf-274">Questo criterio può essere utilizzato hello seguenti criteri [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="055cf-274">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="055cf-275">**Sezioni del criterio:** inbound</span><span class="sxs-lookup"><span data-stu-id="055cf-275">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="055cf-276">**Ambiti del criterio:** globale, prodotto, API, operazione</span><span class="sxs-lookup"><span data-stu-id="055cf-276">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="055cf-277"><a name="SetUsageQuota"></a> Imposta quota di utilizzo per sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="055cf-277"><a name="SetUsageQuota"></a> Set usage quota by subscription</span></span>  
 <span data-ttu-id="055cf-278">Hello `quota` criteri consentono di applicare una quota rinnovabile o permanente chiamata volume e/o della larghezza di banda, in base a una per ogni sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="055cf-278">hello `quota` policy enforces a renewable or lifetime call volume and/or bandwidth quota, on a per subscription basis.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="055cf-279">Questo criterio può essere impiegato una sola volta per ogni documento dei criteri.</span><span class="sxs-lookup"><span data-stu-id="055cf-279">This policy can be used only once per policy document.</span></span>  
>   
>  <span data-ttu-id="055cf-280">[Espressioni di criteri](api-management-policy-expressions.md) non può essere usata in qualsiasi degli attributi di hello criteri per i criteri.</span><span class="sxs-lookup"><span data-stu-id="055cf-280">[Policy expressions](api-management-policy-expressions.md) cannot be used in any of hello policy attributes for this policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="055cf-281">Istruzione del criterio</span><span class="sxs-lookup"><span data-stu-id="055cf-281">Policy statement</span></span>  
  
```xml  
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">  
    <api name="name" calls="number" bandwidth="kilobytes">  
        <operation name="name" calls="number" bandwidth="kilobytes" />  
    </api>  
</quota>  
```  
  
### <a name="example"></a><span data-ttu-id="055cf-282">Esempio</span><span class="sxs-lookup"><span data-stu-id="055cf-282">Example</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="055cf-283">Elementi</span><span class="sxs-lookup"><span data-stu-id="055cf-283">Elements</span></span>  
  
|<span data-ttu-id="055cf-284">Nome</span><span class="sxs-lookup"><span data-stu-id="055cf-284">Name</span></span>|<span data-ttu-id="055cf-285">Descrizione</span><span class="sxs-lookup"><span data-stu-id="055cf-285">Description</span></span>|<span data-ttu-id="055cf-286">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="055cf-286">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="055cf-287">quota</span><span class="sxs-lookup"><span data-stu-id="055cf-287">quota</span></span>|<span data-ttu-id="055cf-288">Elemento radice.</span><span class="sxs-lookup"><span data-stu-id="055cf-288">Root element.</span></span>|<span data-ttu-id="055cf-289">Sì</span><span class="sxs-lookup"><span data-stu-id="055cf-289">Yes</span></span>|  
|<span data-ttu-id="055cf-290">api</span><span class="sxs-lookup"><span data-stu-id="055cf-290">api</span></span>|<span data-ttu-id="055cf-291">Aggiungere uno o più di questi tooimpose elementi una quota sulle API nel prodotto hello.</span><span class="sxs-lookup"><span data-stu-id="055cf-291">Add one  or more of these elements tooimpose a quota on APIs within hello product.</span></span> <span data-ttu-id="055cf-292">Le quote delle API e del prodotto vengono applicate in modo indipendente.</span><span class="sxs-lookup"><span data-stu-id="055cf-292">Product and API quotas are applied independently.</span></span>|<span data-ttu-id="055cf-293">No</span><span class="sxs-lookup"><span data-stu-id="055cf-293">No</span></span>|  
|<span data-ttu-id="055cf-294">operation</span><span class="sxs-lookup"><span data-stu-id="055cf-294">operation</span></span>|<span data-ttu-id="055cf-295">Aggiungere uno o più di questi tooimpose elementi una quota per le operazioni in un'API.</span><span class="sxs-lookup"><span data-stu-id="055cf-295">Add one  or more of these elements tooimpose a quota on operations within an API.</span></span> <span data-ttu-id="055cf-296">Le quote delle operazioni, delle API e del prodotto vengono applicate in modo indipendente.</span><span class="sxs-lookup"><span data-stu-id="055cf-296">Product, API, and operation quotas are applied independently.</span></span>|<span data-ttu-id="055cf-297">No</span><span class="sxs-lookup"><span data-stu-id="055cf-297">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="055cf-298">Attributi</span><span class="sxs-lookup"><span data-stu-id="055cf-298">Attributes</span></span>  
  
|<span data-ttu-id="055cf-299">Nome</span><span class="sxs-lookup"><span data-stu-id="055cf-299">Name</span></span>|<span data-ttu-id="055cf-300">Descrizione</span><span class="sxs-lookup"><span data-stu-id="055cf-300">Description</span></span>|<span data-ttu-id="055cf-301">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="055cf-301">Required</span></span>|<span data-ttu-id="055cf-302">Default</span><span class="sxs-lookup"><span data-stu-id="055cf-302">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="055cf-303">name</span><span class="sxs-lookup"><span data-stu-id="055cf-303">name</span></span>|<span data-ttu-id="055cf-304">nome Hello di hello API o operazione per cui hello quota si applica.</span><span class="sxs-lookup"><span data-stu-id="055cf-304">hello name of hello API or operation for which hello quota applies.</span></span>|<span data-ttu-id="055cf-305">Sì</span><span class="sxs-lookup"><span data-stu-id="055cf-305">Yes</span></span>|<span data-ttu-id="055cf-306">N/D</span><span class="sxs-lookup"><span data-stu-id="055cf-306">N/A</span></span>|  
|<span data-ttu-id="055cf-307">bandwidth</span><span class="sxs-lookup"><span data-stu-id="055cf-307">bandwidth</span></span>|<span data-ttu-id="055cf-308">numero massimo totale di kilobyte consentiti nell'intervallo di tempo hello specificato in hello Hello `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="055cf-308">hello maximum total number of kilobytes allowed during hello time interval specified in hello `renewal-period`.</span></span>|<span data-ttu-id="055cf-309">Devono essere specificati `calls`, `bandwidth` o entrambi.</span><span class="sxs-lookup"><span data-stu-id="055cf-309">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="055cf-310">N/D</span><span class="sxs-lookup"><span data-stu-id="055cf-310">N/A</span></span>|  
|<span data-ttu-id="055cf-311">calls</span><span class="sxs-lookup"><span data-stu-id="055cf-311">calls</span></span>|<span data-ttu-id="055cf-312">numero massimo di chiamate consentite durante l'intervallo di tempo hello specificato in hello Hello `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="055cf-312">hello maximum total number of calls allowed during hello time interval specified in hello `renewal-period`.</span></span>|<span data-ttu-id="055cf-313">Devono essere specificati `calls`, `bandwidth` o entrambi.</span><span class="sxs-lookup"><span data-stu-id="055cf-313">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="055cf-314">N/D</span><span class="sxs-lookup"><span data-stu-id="055cf-314">N/A</span></span>|  
|<span data-ttu-id="055cf-315">renewal-period</span><span class="sxs-lookup"><span data-stu-id="055cf-315">renewal-period</span></span>|<span data-ttu-id="055cf-316">Hello periodo di tempo in secondi dopo il quale hello quota viene reimpostata.</span><span class="sxs-lookup"><span data-stu-id="055cf-316">hello time period in seconds after which hello quota resets.</span></span>|<span data-ttu-id="055cf-317">Sì</span><span class="sxs-lookup"><span data-stu-id="055cf-317">Yes</span></span>|<span data-ttu-id="055cf-318">N/D</span><span class="sxs-lookup"><span data-stu-id="055cf-318">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="055cf-319">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="055cf-319">Usage</span></span>  
 <span data-ttu-id="055cf-320">Questo criterio può essere utilizzato hello seguenti criteri [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="055cf-320">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="055cf-321">**Sezioni del criterio:** inbound</span><span class="sxs-lookup"><span data-stu-id="055cf-321">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="055cf-322">**Ambiti del criterio:** prodotto</span><span class="sxs-lookup"><span data-stu-id="055cf-322">**Policy scopes:** product</span></span>  
  
##  <span data-ttu-id="055cf-323"><a name="SetUsageQuotaByKey"></a> Impostare la quota per chiave</span><span class="sxs-lookup"><span data-stu-id="055cf-323"><a name="SetUsageQuotaByKey"></a> Set usage quota by key</span></span>  
 <span data-ttu-id="055cf-324">Hello `quota-by-key` criteri consentono di applicare una quota rinnovabile o permanente chiamata volume e/o della larghezza di banda, in una base per ogni chiave.</span><span class="sxs-lookup"><span data-stu-id="055cf-324">hello `quota-by-key` policy enforces a renewable or lifetime call volume and/or bandwidth quota, on a per key basis.</span></span> <span data-ttu-id="055cf-325">chiave di Hello può avere un valore stringa arbitrario e viene in genere fornito con un'espressione di criteri.</span><span class="sxs-lookup"><span data-stu-id="055cf-325">hello key can have an arbitrary string value and is typically provided using a policy expression.</span></span> <span data-ttu-id="055cf-326">È possibile aggiungere toospecify le richieste devono essere conteggiate quota hello condizione incrementale facoltativo.</span><span class="sxs-lookup"><span data-stu-id="055cf-326">Optional increment condition can be added toospecify which requests should be counted towards hello quota.</span></span>  
  
 <span data-ttu-id="055cf-327">Per altre informazioni ed esempi su questo criterio, vedere [Advanced request throttling with Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/) (Limitazione avanzata delle richieste con Gestione API di Azure).</span><span class="sxs-lookup"><span data-stu-id="055cf-327">For more information and examples of this policy, see [Advanced request throttling with Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="055cf-328">Questo criterio può essere impiegato una sola volta per ogni documento dei criteri.</span><span class="sxs-lookup"><span data-stu-id="055cf-328">This policy can be used only once per policy document.</span></span>  
>   
>  <span data-ttu-id="055cf-329">[Espressioni di criteri](api-management-policy-expressions.md) non può essere usata in qualsiasi degli attributi di hello criteri per i criteri.</span><span class="sxs-lookup"><span data-stu-id="055cf-329">[Policy expressions](api-management-policy-expressions.md) cannot be used in any of hello policy attributes for this policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="055cf-330">Istruzione del criterio</span><span class="sxs-lookup"><span data-stu-id="055cf-330">Policy statement</span></span>  
  
```xml  
<quota-by-key calls="number"   
              bandwidth="kilobytes"   
              renewal-period="seconds"  
              increment-condition="condition"   
              counter-key="key value" />  
  
```  
  
### <a name="example"></a><span data-ttu-id="055cf-331">Esempio</span><span class="sxs-lookup"><span data-stu-id="055cf-331">Example</span></span>  
 <span data-ttu-id="055cf-332">Nell'esempio seguente di hello, quota hello è codificato in base all'indirizzo IP hello chiamante.</span><span class="sxs-lookup"><span data-stu-id="055cf-332">In hello following example, hello quota is keyed by hello caller IP address.</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="055cf-333">Elementi</span><span class="sxs-lookup"><span data-stu-id="055cf-333">Elements</span></span>  
  
|<span data-ttu-id="055cf-334">Nome</span><span class="sxs-lookup"><span data-stu-id="055cf-334">Name</span></span>|<span data-ttu-id="055cf-335">Descrizione</span><span class="sxs-lookup"><span data-stu-id="055cf-335">Description</span></span>|<span data-ttu-id="055cf-336">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="055cf-336">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="055cf-337">quota</span><span class="sxs-lookup"><span data-stu-id="055cf-337">quota</span></span>|<span data-ttu-id="055cf-338">Elemento radice.</span><span class="sxs-lookup"><span data-stu-id="055cf-338">Root element.</span></span>|<span data-ttu-id="055cf-339">Sì</span><span class="sxs-lookup"><span data-stu-id="055cf-339">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="055cf-340">Attributi</span><span class="sxs-lookup"><span data-stu-id="055cf-340">Attributes</span></span>  
  
|<span data-ttu-id="055cf-341">Nome</span><span class="sxs-lookup"><span data-stu-id="055cf-341">Name</span></span>|<span data-ttu-id="055cf-342">Descrizione</span><span class="sxs-lookup"><span data-stu-id="055cf-342">Description</span></span>|<span data-ttu-id="055cf-343">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="055cf-343">Required</span></span>|<span data-ttu-id="055cf-344">Default</span><span class="sxs-lookup"><span data-stu-id="055cf-344">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="055cf-345">bandwidth</span><span class="sxs-lookup"><span data-stu-id="055cf-345">bandwidth</span></span>|<span data-ttu-id="055cf-346">numero massimo totale di kilobyte consentiti nell'intervallo di tempo hello specificato in hello Hello `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="055cf-346">hello maximum total number of kilobytes allowed during hello time interval specified in hello `renewal-period`.</span></span>|<span data-ttu-id="055cf-347">Devono essere specificati `calls`, `bandwidth` o entrambi.</span><span class="sxs-lookup"><span data-stu-id="055cf-347">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="055cf-348">N/D</span><span class="sxs-lookup"><span data-stu-id="055cf-348">N/A</span></span>|  
|<span data-ttu-id="055cf-349">calls</span><span class="sxs-lookup"><span data-stu-id="055cf-349">calls</span></span>|<span data-ttu-id="055cf-350">numero massimo di chiamate consentite durante l'intervallo di tempo hello specificato in hello Hello `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="055cf-350">hello maximum total number of calls allowed during hello time interval specified in hello `renewal-period`.</span></span>|<span data-ttu-id="055cf-351">Devono essere specificati `calls`, `bandwidth` o entrambi.</span><span class="sxs-lookup"><span data-stu-id="055cf-351">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="055cf-352">N/D</span><span class="sxs-lookup"><span data-stu-id="055cf-352">N/A</span></span>|  
|<span data-ttu-id="055cf-353">counter-key</span><span class="sxs-lookup"><span data-stu-id="055cf-353">counter-key</span></span>|<span data-ttu-id="055cf-354">Hello toouse chiave per il criterio di quota hello.</span><span class="sxs-lookup"><span data-stu-id="055cf-354">hello key toouse for hello quota policy.</span></span>|<span data-ttu-id="055cf-355">Sì</span><span class="sxs-lookup"><span data-stu-id="055cf-355">Yes</span></span>|<span data-ttu-id="055cf-356">N/D</span><span class="sxs-lookup"><span data-stu-id="055cf-356">N/A</span></span>|  
|<span data-ttu-id="055cf-357">increment-condition</span><span class="sxs-lookup"><span data-stu-id="055cf-357">increment-condition</span></span>|<span data-ttu-id="055cf-358">espressione di Hello booleana che specifica se la richiesta hello conteggiata quota hello (`true`)</span><span class="sxs-lookup"><span data-stu-id="055cf-358">hello boolean expression specifying if hello request should be counted towards hello quota (`true`)</span></span>|<span data-ttu-id="055cf-359">No</span><span class="sxs-lookup"><span data-stu-id="055cf-359">No</span></span>|<span data-ttu-id="055cf-360">N/D</span><span class="sxs-lookup"><span data-stu-id="055cf-360">N/A</span></span>|  
|<span data-ttu-id="055cf-361">renewal-period</span><span class="sxs-lookup"><span data-stu-id="055cf-361">renewal-period</span></span>|<span data-ttu-id="055cf-362">Hello periodo di tempo in secondi dopo il quale hello quota viene reimpostata.</span><span class="sxs-lookup"><span data-stu-id="055cf-362">hello time period in seconds after which hello quota resets.</span></span>|<span data-ttu-id="055cf-363">Sì</span><span class="sxs-lookup"><span data-stu-id="055cf-363">Yes</span></span>|<span data-ttu-id="055cf-364">N/D</span><span class="sxs-lookup"><span data-stu-id="055cf-364">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="055cf-365">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="055cf-365">Usage</span></span>  
 <span data-ttu-id="055cf-366">Questo criterio può essere utilizzato hello seguenti criteri [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="055cf-366">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="055cf-367">**Sezioni del criterio:** inbound</span><span class="sxs-lookup"><span data-stu-id="055cf-367">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="055cf-368">**Ambiti del criterio:** globale, prodotto, API, operazione</span><span class="sxs-lookup"><span data-stu-id="055cf-368">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="055cf-369"><a name="ValidateJWT"></a> Convalida token JWT</span><span class="sxs-lookup"><span data-stu-id="055cf-369"><a name="ValidateJWT"></a> Validate JWT</span></span>  
 <span data-ttu-id="055cf-370">Hello `validate-jwt` criteri impone l'esistenza e validità di un token JWT estratto da un oggetto intestazione HTTP o un parametro di query specificato.</span><span class="sxs-lookup"><span data-stu-id="055cf-370">hello `validate-jwt` policy enforces existence and validity of a JWT extracted from either a specified HTTP Header or a specified query parameter.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="055cf-371">Hello `validate-jwt` criteri richiedono tale hello `exp` attestazione registrato è presente nel token JWT hello, a meno che non `require-expiration-time` attributo viene specificato e impostato troppo`false`.</span><span class="sxs-lookup"><span data-stu-id="055cf-371">hello `validate-jwt` policy requires that hello `exp` registered claim is inlcuded in hello JWT token, unless `require-expiration-time` attribute is specified and set too`false`.</span></span>  
> <span data-ttu-id="055cf-372">Hello `validate-jwt` criteri supporta gli algoritmi di firma HS256 e RS256.</span><span class="sxs-lookup"><span data-stu-id="055cf-372">hello `validate-jwt` policy supports HS256 and RS256 signing algorithms.</span></span> <span data-ttu-id="055cf-373">Per HS256 chiave hello è necessario specificare inline nel criterio di hello in formato con codificata base64 hello.</span><span class="sxs-lookup"><span data-stu-id="055cf-373">For HS256 hello key must be provided inline within hello policy in hello base64 encoded form.</span></span> <span data-ttu-id="055cf-374">Per RS256 chiave hello ha toobe fornire tramite un endpoint di configurazione Openid.</span><span class="sxs-lookup"><span data-stu-id="055cf-374">For RS256 hello key has toobe provide via an Open ID configuration endpoint.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="055cf-375">Istruzione del criterio</span><span class="sxs-lookup"><span data-stu-id="055cf-375">Policy statement</span></span>  
  
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
  
### <a name="examples"></a><span data-ttu-id="055cf-376">Esempi</span><span class="sxs-lookup"><span data-stu-id="055cf-376">Examples</span></span>  
  
#### <a name="azure-mobile-services-token-validation"></a><span data-ttu-id="055cf-377">Convalida del token dei Servizi mobili di Azure</span><span class="sxs-lookup"><span data-stu-id="055cf-377">Azure Mobile Services token validation</span></span>  
  
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
  
#### <a name="azure-active-directory-token-validation"></a><span data-ttu-id="055cf-378">Convalida del token di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="055cf-378">Azure Active Directory token validation</span></span>  
  
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

  
#### <a name="azure-active-directory-b2c-token-validation"></a><span data-ttu-id="055cf-379">Convalida del token di Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="055cf-379">Azure Active Directory B2C token validation</span></span>  
  
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
  
#### <a name="authorize-access-toooperations-based-on-token-claims"></a><span data-ttu-id="055cf-380">Autorizzare l'accesso toooperations basata sulle attestazioni di token</span><span class="sxs-lookup"><span data-stu-id="055cf-380">Authorize access toooperations based on token claims</span></span>  
 <span data-ttu-id="055cf-381">Questo esempio viene illustrato come hello toouse [convalidare JWT](api-management-access-restriction-policies.md#ValidateJWT) toopre criteri-autorizzare l'accesso toooperations basata sulle attestazioni di token.</span><span class="sxs-lookup"><span data-stu-id="055cf-381">This example shows how toouse hello [Validate JWT](api-management-access-restriction-policies.md#ValidateJWT) policy toopre-authorize access toooperations based on token claims.</span></span> <span data-ttu-id="055cf-382">Per una dimostrazione della configurazione e l'utilizzo di questo criterio, vedere [Cloud coprire episodio 177: più API le funzionalità di gestione con Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) e far avanzare rapidamente too13:50.</span><span class="sxs-lookup"><span data-stu-id="055cf-382">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too13:50.</span></span> <span data-ttu-id="055cf-383">Avanzamento rapido too15:00 criteri hello toosee configurati nell'editor Criteri di hello e quindi too18:50 per una dimostrazione di chiamata di un'operazione dal portale per sviluppatori di hello con e senza hello necessari token di autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="055cf-383">Fast forward too15:00 toosee hello policies configured in hello policy editor and then too18:50 for a demonstration of calling an operation from hello developer portal both with and without hello required authorization token.</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="055cf-384">Elementi</span><span class="sxs-lookup"><span data-stu-id="055cf-384">Elements</span></span>  
  
|<span data-ttu-id="055cf-385">Elemento</span><span class="sxs-lookup"><span data-stu-id="055cf-385">Element</span></span>|<span data-ttu-id="055cf-386">Descrizione</span><span class="sxs-lookup"><span data-stu-id="055cf-386">Description</span></span>|<span data-ttu-id="055cf-387">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="055cf-387">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="055cf-388">validate-jwt</span><span class="sxs-lookup"><span data-stu-id="055cf-388">validate-jwt</span></span>|<span data-ttu-id="055cf-389">Elemento radice.</span><span class="sxs-lookup"><span data-stu-id="055cf-389">Root element.</span></span>|<span data-ttu-id="055cf-390">Sì</span><span class="sxs-lookup"><span data-stu-id="055cf-390">Yes</span></span>|  
|<span data-ttu-id="055cf-391">audiences</span><span class="sxs-lookup"><span data-stu-id="055cf-391">audiences</span></span>|<span data-ttu-id="055cf-392">Contiene un elenco di attestazioni di destinatari accettabili che possono essere presenti nel token hello.</span><span class="sxs-lookup"><span data-stu-id="055cf-392">Contains a list of acceptable audience claims that can be present on hello token.</span></span> <span data-ttu-id="055cf-393">Se sono presenti più valori "audience", viene provato ogni valore fino al completamento di tutti i valori (caso in cui la convalida ha esito negativo) o fino a quando un valore non ha esito positivo.</span><span class="sxs-lookup"><span data-stu-id="055cf-393">If multiple audience values are present, then each value is tried until either all are exhausted (in which case validation fails) or until one succeeds.</span></span> <span data-ttu-id="055cf-394">È necessario specificare almeno un "audience".</span><span class="sxs-lookup"><span data-stu-id="055cf-394">At least one audience must be specified.</span></span>|<span data-ttu-id="055cf-395">No</span><span class="sxs-lookup"><span data-stu-id="055cf-395">No</span></span>|  
|<span data-ttu-id="055cf-396">issuer-signing-keys</span><span class="sxs-lookup"><span data-stu-id="055cf-396">issuer-signing-keys</span></span>|<span data-ttu-id="055cf-397">Un elenco di sicurezza con codifica Base64 le chiavi usate toovalidate firmati i token.</span><span class="sxs-lookup"><span data-stu-id="055cf-397">A list of Base64-encoded security keys used toovalidate signed tokens.</span></span> <span data-ttu-id="055cf-398">Se sono presenti più chiavi di sicurezza, viene provata ogni chiave fino al completamento di tutte le chiavi (caso in cui la convalida ha esito negativo) o fino a quando una chiave non ha esito positivo.</span><span class="sxs-lookup"><span data-stu-id="055cf-398">If multiple security keys are present, then each key is tried until either all are exhausted (in which case validation fails) or until one succeeds (useful for token rollover).</span></span> <span data-ttu-id="055cf-399">Gli elementi chiave hanno un parametro facoltativo `id` toomatch attributo utilizzato contro `kid` attestazione.</span><span class="sxs-lookup"><span data-stu-id="055cf-399">Key elements have an optional `id` attribute used toomatch against `kid` claim.</span></span>|<span data-ttu-id="055cf-400">No</span><span class="sxs-lookup"><span data-stu-id="055cf-400">No</span></span>|  
|<span data-ttu-id="055cf-401">issuers</span><span class="sxs-lookup"><span data-stu-id="055cf-401">issuers</span></span>|<span data-ttu-id="055cf-402">Un elenco di entità accettabili che ha emesso il token hello.</span><span class="sxs-lookup"><span data-stu-id="055cf-402">A list of acceptable principals that issued hello token.</span></span> <span data-ttu-id="055cf-403">Se sono presenti più valori emittenti, viene provato ogni valore fino al completamento di tutti i valori (caso in cui la convalida ha esito negativo) o fino a quando un valore non ha esito positivo.</span><span class="sxs-lookup"><span data-stu-id="055cf-403">If multiple issuer values are present, then each value is tried until either all are exhausted (in which case validation fails) or until one succeeds.</span></span>|<span data-ttu-id="055cf-404">No</span><span class="sxs-lookup"><span data-stu-id="055cf-404">No</span></span>|  
|<span data-ttu-id="055cf-405">openid-config</span><span class="sxs-lookup"><span data-stu-id="055cf-405">openid-config</span></span>|<span data-ttu-id="055cf-406">elemento Hello utilizzata per specificare un endpoint di configurazione Openid conforme da cui è possibile ottenere le chiavi e dell'autorità di certificazione di firma.</span><span class="sxs-lookup"><span data-stu-id="055cf-406">hello element used for specifying a compliant Open ID configuration endpoint from which signing keys and issuer can be obtained.</span></span>|<span data-ttu-id="055cf-407">No</span><span class="sxs-lookup"><span data-stu-id="055cf-407">No</span></span>|  
|<span data-ttu-id="055cf-408">required-claims</span><span class="sxs-lookup"><span data-stu-id="055cf-408">required-claims</span></span>|<span data-ttu-id="055cf-409">Contiene un elenco di attestazioni previste toobe presente nel token hello per tale toobe considerato valido.</span><span class="sxs-lookup"><span data-stu-id="055cf-409">Contains a list of claims expected toobe present on hello token for it toobe considered valid.</span></span> <span data-ttu-id="055cf-410">Quando hello `match` attributo è impostato troppo`all` nei criteri hello ogni valore dell'attestazione deve essere presente nel token hello per toosucceed di convalida.</span><span class="sxs-lookup"><span data-stu-id="055cf-410">When hello `match` attribute is set too`all` every claim value in hello policy must be present in hello token for validation toosucceed.</span></span> <span data-ttu-id="055cf-411">Quando hello `match` attributo è impostato troppo`any` almeno un'attestazione deve essere presente nel token hello per toosucceed di convalida.</span><span class="sxs-lookup"><span data-stu-id="055cf-411">When hello `match` attribute is set too`any` at least one claim must be present in hello token for validation toosucceed.</span></span>|<span data-ttu-id="055cf-412">No</span><span class="sxs-lookup"><span data-stu-id="055cf-412">No</span></span>|  
|<span data-ttu-id="055cf-413">zumo-master-key</span><span class="sxs-lookup"><span data-stu-id="055cf-413">zumo-master-key</span></span>|<span data-ttu-id="055cf-414">Chiave master per i token rilasciati da Servizi mobili di Azure</span><span class="sxs-lookup"><span data-stu-id="055cf-414">Master key for tokens issued by Azure Mobile Services</span></span>|<span data-ttu-id="055cf-415">No</span><span class="sxs-lookup"><span data-stu-id="055cf-415">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="055cf-416">Attributi</span><span class="sxs-lookup"><span data-stu-id="055cf-416">Attributes</span></span>  
  
|<span data-ttu-id="055cf-417">Nome</span><span class="sxs-lookup"><span data-stu-id="055cf-417">Name</span></span>|<span data-ttu-id="055cf-418">Descrizione</span><span class="sxs-lookup"><span data-stu-id="055cf-418">Description</span></span>|<span data-ttu-id="055cf-419">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="055cf-419">Required</span></span>|<span data-ttu-id="055cf-420">Default</span><span class="sxs-lookup"><span data-stu-id="055cf-420">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="055cf-421">clock-skew</span><span class="sxs-lookup"><span data-stu-id="055cf-421">clock-skew</span></span>|<span data-ttu-id="055cf-422">TimeSpan.</span><span class="sxs-lookup"><span data-stu-id="055cf-422">Timespan.</span></span> <span data-ttu-id="055cf-423">Fornisce una minima flessibilità nel caso in cui sia presente nel token hello attestazione di scadenza del token hello e oltre hello corrente data / ora.</span><span class="sxs-lookup"><span data-stu-id="055cf-423">Provides some small leeway in case hello token's expiration claim is present in hello token and is past hello current date / time.</span></span>|<span data-ttu-id="055cf-424">No</span><span class="sxs-lookup"><span data-stu-id="055cf-424">No</span></span>|<span data-ttu-id="055cf-425">0 secondi</span><span class="sxs-lookup"><span data-stu-id="055cf-425">0 seconds</span></span>|  
|<span data-ttu-id="055cf-426">failed-validation-error-message</span><span class="sxs-lookup"><span data-stu-id="055cf-426">failed-validation-error-message</span></span>|<span data-ttu-id="055cf-427">Tooreturn messaggio di errore nel corpo della risposta HTTP hello se hello JWT non supera la convalida.</span><span class="sxs-lookup"><span data-stu-id="055cf-427">Error message tooreturn in hello HTTP response body if hello JWT does not pass validation.</span></span> <span data-ttu-id="055cf-428">I caratteri speciali eventualmente contenuti in questo messaggio devono essere adeguatamente preceduti da un carattere di escape.</span><span class="sxs-lookup"><span data-stu-id="055cf-428">This message must have any special characters properly escaped.</span></span>|<span data-ttu-id="055cf-429">No</span><span class="sxs-lookup"><span data-stu-id="055cf-429">No</span></span>|<span data-ttu-id="055cf-430">Il messaggio di errore predefinito dipende dal problema della convalida, ad esempio "JWT not present" ("JWT non presente").</span><span class="sxs-lookup"><span data-stu-id="055cf-430">Default error message depends on validation issue, for example "JWT not present."</span></span>|  
|<span data-ttu-id="055cf-431">failed-validation-httpcode</span><span class="sxs-lookup"><span data-stu-id="055cf-431">failed-validation-httpcode</span></span>|<span data-ttu-id="055cf-432">Codice di stato HTTP tooreturn se hello JWT non supera la convalida.</span><span class="sxs-lookup"><span data-stu-id="055cf-432">HTTP Status code tooreturn if hello JWT doesn't pass validation.</span></span>|<span data-ttu-id="055cf-433">No</span><span class="sxs-lookup"><span data-stu-id="055cf-433">No</span></span>|<span data-ttu-id="055cf-434">401</span><span class="sxs-lookup"><span data-stu-id="055cf-434">401</span></span>|  
|<span data-ttu-id="055cf-435">header-name</span><span class="sxs-lookup"><span data-stu-id="055cf-435">header-name</span></span>|<span data-ttu-id="055cf-436">nome di Hello dell'intestazione HTTP hello che contiene il token hello.</span><span class="sxs-lookup"><span data-stu-id="055cf-436">hello name of hello HTTP header holding hello token.</span></span>|<span data-ttu-id="055cf-437">È necessario specificare `header-name` o `query-paremeter-name`, ma non entrambi.</span><span class="sxs-lookup"><span data-stu-id="055cf-437">Either `header-name` or `query-paremeter-name` must be specified; but not both.</span></span>|<span data-ttu-id="055cf-438">N/D</span><span class="sxs-lookup"><span data-stu-id="055cf-438">N/A</span></span>|  
|<span data-ttu-id="055cf-439">id</span><span class="sxs-lookup"><span data-stu-id="055cf-439">id</span></span>|<span data-ttu-id="055cf-440">Hello `id` attributo hello `key` elemento consente stringa hello toospecify che verrà confrontato con `kid` hello toofind token (se presente) out hello toouse chiave appropriata per la convalida della firma di attestazione.</span><span class="sxs-lookup"><span data-stu-id="055cf-440">hello `id` attribute on hello `key` element allows you toospecify hello string that will be matched against `kid` claim in hello token (if present) toofind out hello appropriate key toouse for signature validation.</span></span>|<span data-ttu-id="055cf-441">No</span><span class="sxs-lookup"><span data-stu-id="055cf-441">No</span></span>|<span data-ttu-id="055cf-442">N/D</span><span class="sxs-lookup"><span data-stu-id="055cf-442">N/A</span></span>|  
|<span data-ttu-id="055cf-443">match</span><span class="sxs-lookup"><span data-stu-id="055cf-443">match</span></span>|<span data-ttu-id="055cf-444">Hello `match` attributo hello `claim` elemento specifica se ogni valore attestazione in Criteri di hello deve essere presenti nel token hello per toosucceed di convalida.</span><span class="sxs-lookup"><span data-stu-id="055cf-444">hello `match` attribute on hello `claim` element specifies whether every claim value in hello policy must be present in hello token for validation toosucceed.</span></span> <span data-ttu-id="055cf-445">I valori possibili sono:</span><span class="sxs-lookup"><span data-stu-id="055cf-445">Possible values are:</span></span><br /><br /> <span data-ttu-id="055cf-446">-                          `all`-ogni valore attestazione in Criteri di hello deve essere presente nel token hello per toosucceed di convalida.</span><span class="sxs-lookup"><span data-stu-id="055cf-446">-                          `all` - every claim value in hello policy must be present in hello token for validation toosucceed.</span></span><br /><br /> <span data-ttu-id="055cf-447">-                          `any`-il valore di almeno un'attestazione deve essere presente nel token hello per toosucceed di convalida.</span><span class="sxs-lookup"><span data-stu-id="055cf-447">-                          `any` - at least one claim value must be present in hello token for validation toosucceed.</span></span>|<span data-ttu-id="055cf-448">No</span><span class="sxs-lookup"><span data-stu-id="055cf-448">No</span></span>|<span data-ttu-id="055cf-449">tutti</span><span class="sxs-lookup"><span data-stu-id="055cf-449">all</span></span>|  
|<span data-ttu-id="055cf-450">query-paremeter-name</span><span class="sxs-lookup"><span data-stu-id="055cf-450">query-paremeter-name</span></span>|<span data-ttu-id="055cf-451">nome Hello hello hello del parametro della query che contiene il token hello.</span><span class="sxs-lookup"><span data-stu-id="055cf-451">hello name of hello hello query parameter holding hello token.</span></span>|<span data-ttu-id="055cf-452">È necessario specificare `header-name` o `query-paremeter-name`, ma non entrambi.</span><span class="sxs-lookup"><span data-stu-id="055cf-452">Either `header-name` or `query-paremeter-name` must be specified; but not both.</span></span>|<span data-ttu-id="055cf-453">N/D</span><span class="sxs-lookup"><span data-stu-id="055cf-453">N/A</span></span>|  
|<span data-ttu-id="055cf-454">require-expiration-time</span><span class="sxs-lookup"><span data-stu-id="055cf-454">require-expiration-time</span></span>|<span data-ttu-id="055cf-455">Booleano.</span><span class="sxs-lookup"><span data-stu-id="055cf-455">Boolean.</span></span> <span data-ttu-id="055cf-456">Specifica se un'attestazione di scadenza è necessaria nel token hello.</span><span class="sxs-lookup"><span data-stu-id="055cf-456">Specifies whether an expiration claim is required in hello token.</span></span>|<span data-ttu-id="055cf-457">No</span><span class="sxs-lookup"><span data-stu-id="055cf-457">No</span></span>|<span data-ttu-id="055cf-458">true</span><span class="sxs-lookup"><span data-stu-id="055cf-458">true</span></span>|
|<span data-ttu-id="055cf-459">require-scheme</span><span class="sxs-lookup"><span data-stu-id="055cf-459">require-scheme</span></span>|<span data-ttu-id="055cf-460">Hello nome dello schema token hello, ad esempio "Bearer".</span><span class="sxs-lookup"><span data-stu-id="055cf-460">hello name of hello token scheme, e.g. "Bearer".</span></span> <span data-ttu-id="055cf-461">Quando questo attributo è impostato, i criteri di hello assicura che specifica lo schema è presente nel valore dell'intestazione di autorizzazione hello.</span><span class="sxs-lookup"><span data-stu-id="055cf-461">When this attribute is set, hello policy will ensure that specified scheme is present in hello Authorization header value.</span></span>|<span data-ttu-id="055cf-462">No</span><span class="sxs-lookup"><span data-stu-id="055cf-462">No</span></span>|<span data-ttu-id="055cf-463">N/D</span><span class="sxs-lookup"><span data-stu-id="055cf-463">N/A</span></span>|
|<span data-ttu-id="055cf-464">require-signed-tokens</span><span class="sxs-lookup"><span data-stu-id="055cf-464">require-signed-tokens</span></span>|<span data-ttu-id="055cf-465">Booleano.</span><span class="sxs-lookup"><span data-stu-id="055cf-465">Boolean.</span></span> <span data-ttu-id="055cf-466">Specifica se un token è obbligatorio toobe firmato.</span><span class="sxs-lookup"><span data-stu-id="055cf-466">Specifies whether a token is required toobe signed.</span></span>|<span data-ttu-id="055cf-467">No</span><span class="sxs-lookup"><span data-stu-id="055cf-467">No</span></span>|<span data-ttu-id="055cf-468">true</span><span class="sxs-lookup"><span data-stu-id="055cf-468">true</span></span>|  
|<span data-ttu-id="055cf-469">URL</span><span class="sxs-lookup"><span data-stu-id="055cf-469">url</span></span>|<span data-ttu-id="055cf-470">URL dell'endpoint di configurazione Open ID dal quale è possibile ottenere i metadati della configurazione Open ID.</span><span class="sxs-lookup"><span data-stu-id="055cf-470">Open ID configuration endpoint URL from where Open ID configuration metadata can be obtained.</span></span> <span data-ttu-id="055cf-471">Per Azure Active Directory utilizzare hello seguente URL: `https://login.microsoftonline.com/{tenant-name}/.well-known/openid-configuration` sostituendo il nome di tenant di directory, ad esempio `contoso.onmicrosoft.com`.</span><span class="sxs-lookup"><span data-stu-id="055cf-471">For Azure Active Directory use hello following URL: `https://login.microsoftonline.com/{tenant-name}/.well-known/openid-configuration` substituting your directory tenant name, e.g. `contoso.onmicrosoft.com`.</span></span>|<span data-ttu-id="055cf-472">Sì</span><span class="sxs-lookup"><span data-stu-id="055cf-472">Yes</span></span>|<span data-ttu-id="055cf-473">N/D</span><span class="sxs-lookup"><span data-stu-id="055cf-473">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="055cf-474">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="055cf-474">Usage</span></span>  
 <span data-ttu-id="055cf-475">Questo criterio può essere utilizzato hello seguenti criteri [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="055cf-475">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="055cf-476">**Sezioni del criterio:** inbound</span><span class="sxs-lookup"><span data-stu-id="055cf-476">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="055cf-477">**Ambiti del criterio:** globale, prodotto, API, operazione</span><span class="sxs-lookup"><span data-stu-id="055cf-477">**Policy scopes:** global, product, API, operation</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="055cf-478">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="055cf-478">Next steps</span></span>
<span data-ttu-id="055cf-479">Per altre informazioni sull'uso dei criteri, vedere [Criteri di Gestione API](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="055cf-479">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  
