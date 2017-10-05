---
title: Criteri tra domini in Gestione API di Azure | Microsoft Docs
description: Informazioni sui criteri tra domini disponibili per l'uso in Gestione API di Azure.
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
ms.openlocfilehash: ddca9e35b44a21294abbb5eaa4418bcdb85494cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="api-management-cross-domain-policies"></a><span data-ttu-id="42d63-103">Criteri tra domini di Gestione API</span><span class="sxs-lookup"><span data-stu-id="42d63-103">API Management cross domain policies</span></span>
<span data-ttu-id="42d63-104">Questo argomento fornisce un riferimento per i seguenti criteri di Gestione API.</span><span class="sxs-lookup"><span data-stu-id="42d63-104">This topic provides a reference for the following API Management policies.</span></span> <span data-ttu-id="42d63-105">Per informazioni sull'aggiunta e sulla configurazione dei criteri, vedere [Criteri di Gestione API](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="42d63-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="42d63-106"><a name="CrossDomainPolicies"></a> Criteri tra domini</span><span class="sxs-lookup"><span data-stu-id="42d63-106"><a name="CrossDomainPolicies"></a> Cross domain policies</span></span>  
  
-   <span data-ttu-id="42d63-107">[Permetti chiamate tra i domini](api-management-cross-domain-policies.md#AllowCrossDomainCalls) : rende accessibile l'API da client Adobe Flash e Microsoft Silverlight basati su browser.</span><span class="sxs-lookup"><span data-stu-id="42d63-107">[Allow cross-domain calls](api-management-cross-domain-policies.md#AllowCrossDomainCalls) - Makes the API accessible from Adobe Flash and Microsoft Silverlight browser-based clients.</span></span>  
  
-   <span data-ttu-id="42d63-108">[CORS](api-management-cross-domain-policies.md#CORS) : aggiunge il supporto per CORS (Cross-Origin Resource Sharing) a un'operazione o a un'API per permettere le chiamate tra domini da client basati su browser.</span><span class="sxs-lookup"><span data-stu-id="42d63-108">[CORS](api-management-cross-domain-policies.md#CORS) - Adds cross-origin resource sharing (CORS) support to an operation or an API to allow cross-domain calls from browser-based clients.</span></span>  
  
-   <span data-ttu-id="42d63-109">[JSONP](api-management-cross-domain-policies.md#JSONP) : aggiunge il supporto per JSON con riempimento (JSONP) a un'operazione o a un'API per permettere le chiamate tra domini da client JavaScript basati su browser.</span><span class="sxs-lookup"><span data-stu-id="42d63-109">[JSONP](api-management-cross-domain-policies.md#JSONP) - Adds JSON with padding (JSONP) support to an operation or an API to allow cross-domain calls from JavaScript browser-based clients.</span></span>  
  
##  <span data-ttu-id="42d63-110"><a name="AllowCrossDomainCalls"></a> Permetti chiamate tra i domini</span><span class="sxs-lookup"><span data-stu-id="42d63-110"><a name="AllowCrossDomainCalls"></a> Allow cross-domain calls</span></span>  
 <span data-ttu-id="42d63-111">Usare il criterio `cross-domain` pe rendere accessibile l'API da client Adobe Flash e Microsoft Silverlight basati su browser.</span><span class="sxs-lookup"><span data-stu-id="42d63-111">Use the `cross-domain` policy to make the API accessible from Adobe Flash and Microsoft Silverlight browser-based clients.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="42d63-112">Istruzione del criterio</span><span class="sxs-lookup"><span data-stu-id="42d63-112">Policy statement</span></span>  
  
```xml  
<cross-domain>  
   <!-Policy configuration is in the Adobe cross-domain policy file format,   
      see http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html-->  
</cross-domain>  
```  
  
### <a name="example"></a><span data-ttu-id="42d63-113">Esempio</span><span class="sxs-lookup"><span data-stu-id="42d63-113">Example</span></span>  
  
```xml  
<cross-domain>  
    <cross-domain-policy>  
        <allow-http-request-headers-from domain='*' headers='*' />  
    </cross-domain-policy>  
</cross-domain>  
```  
  
### <a name="elements"></a><span data-ttu-id="42d63-114">Elementi</span><span class="sxs-lookup"><span data-stu-id="42d63-114">Elements</span></span>  
  
|<span data-ttu-id="42d63-115">Nome</span><span class="sxs-lookup"><span data-stu-id="42d63-115">Name</span></span>|<span data-ttu-id="42d63-116">Descrizione</span><span class="sxs-lookup"><span data-stu-id="42d63-116">Description</span></span>|<span data-ttu-id="42d63-117">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="42d63-117">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="42d63-118">cross-domain</span><span class="sxs-lookup"><span data-stu-id="42d63-118">cross-domain</span></span>|<span data-ttu-id="42d63-119">Elemento radice.</span><span class="sxs-lookup"><span data-stu-id="42d63-119">Root element.</span></span> <span data-ttu-id="42d63-120">Gli elementi figlio devono essere conformi alla [specifica dei file di criteri tra domini Adobe](http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html).</span><span class="sxs-lookup"><span data-stu-id="42d63-120">Child elements must conform to the [Adobe cross-domain policy file specification](http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html).</span></span>|<span data-ttu-id="42d63-121">Sì</span><span class="sxs-lookup"><span data-stu-id="42d63-121">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="42d63-122">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="42d63-122">Usage</span></span>  
 <span data-ttu-id="42d63-123">Questo criterio può essere usato nelle [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e negli [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) del criterio seguenti.</span><span class="sxs-lookup"><span data-stu-id="42d63-123">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="42d63-124">**Sezioni del criterio:** in ingresso</span><span class="sxs-lookup"><span data-stu-id="42d63-124">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="42d63-125">**Ambiti del criterio:** globali</span><span class="sxs-lookup"><span data-stu-id="42d63-125">**Policy scopes:** global</span></span>  
  
##  <span data-ttu-id="42d63-126"><a name="CORS"></a> CORS</span><span class="sxs-lookup"><span data-stu-id="42d63-126"><a name="CORS"></a> CORS</span></span>  
 <span data-ttu-id="42d63-127">Il criterio `cors` aggiunge il supporto per CORS (Cross-Origin Resource Sharing) a un'operazione o a un'API per permettere le chiamate tra domini da client basati su browser.</span><span class="sxs-lookup"><span data-stu-id="42d63-127">The `cors` policy adds cross-origin resource sharing (CORS) support to an operation or an API to allow cross-domain calls from browser-based clients.</span></span>  
  
 <span data-ttu-id="42d63-128">CORS permette a un browser e a un server di interagire e di determinare se permettere o meno richieste specifiche con origini diverse, ad esempio chiamate XMLHttpRequests effettuate da JavaScript in una pagina Web in altri domini.</span><span class="sxs-lookup"><span data-stu-id="42d63-128">CORS allows a browser and a server to interact and determine whether or not to allow specific cross-origin requests (i.e. XMLHttpRequests calls made from JavaScript on a web page to other domains).</span></span> <span data-ttu-id="42d63-129">Ciò offre una maggiore flessibilità rispetto a permettere solo richieste con la stessa origine e una maggiore sicurezza rispetto a permettere tutte le richieste con origini diverse.</span><span class="sxs-lookup"><span data-stu-id="42d63-129">This allows for more flexibility than only allowing same-origin requests, but is more secure than allowing all cross-origin requests.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="42d63-130">Istruzione del criterio</span><span class="sxs-lookup"><span data-stu-id="42d63-130">Policy statement</span></span>  
  
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
  
### <a name="example"></a><span data-ttu-id="42d63-131">Esempio</span><span class="sxs-lookup"><span data-stu-id="42d63-131">Example</span></span>  
 <span data-ttu-id="42d63-132">In questo esempio viene illustrato come supportare richieste preliminari, ad esempio quelle con intestazioni personalizzate o metodi diversi da GET e POST.</span><span class="sxs-lookup"><span data-stu-id="42d63-132">This example demonstrates how to support pre-flight requests, such as those with custom headers or methods other than GET and POST.</span></span> <span data-ttu-id="42d63-133">Per supportare le intestazioni personalizzate e altri verbi HTTP, consultare le sezioni `allowed-methods` e `allowed-headers` come illustrato nell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="42d63-133">To support custom headers and additional HTTP verbs, use the `allowed-methods` and `allowed-headers` sections as shown in the following example.</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="42d63-134">Elementi</span><span class="sxs-lookup"><span data-stu-id="42d63-134">Elements</span></span>  
  
|<span data-ttu-id="42d63-135">Nome</span><span class="sxs-lookup"><span data-stu-id="42d63-135">Name</span></span>|<span data-ttu-id="42d63-136">Descrizione</span><span class="sxs-lookup"><span data-stu-id="42d63-136">Description</span></span>|<span data-ttu-id="42d63-137">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="42d63-137">Required</span></span>|<span data-ttu-id="42d63-138">Default</span><span class="sxs-lookup"><span data-stu-id="42d63-138">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="42d63-139">CORS</span><span class="sxs-lookup"><span data-stu-id="42d63-139">cors</span></span>|<span data-ttu-id="42d63-140">Elemento radice.</span><span class="sxs-lookup"><span data-stu-id="42d63-140">Root element.</span></span>|<span data-ttu-id="42d63-141">Sì</span><span class="sxs-lookup"><span data-stu-id="42d63-141">Yes</span></span>|<span data-ttu-id="42d63-142">N/D</span><span class="sxs-lookup"><span data-stu-id="42d63-142">N/A</span></span>|  
|<span data-ttu-id="42d63-143">allowed-origins</span><span class="sxs-lookup"><span data-stu-id="42d63-143">allowed-origins</span></span>|<span data-ttu-id="42d63-144">Contiene elementi `origin` che descrivono le origini consentite per le richieste tra domini.</span><span class="sxs-lookup"><span data-stu-id="42d63-144">Contains `origin` elements that describe the allowed origins for cross-domain requests.</span></span> <span data-ttu-id="42d63-145">`allowed-origins` può contenere un unico elemento `origin` che specifichi `*` per consentire qualsiasi origine oppure uno o più elementi `origin` che contengano un URI.</span><span class="sxs-lookup"><span data-stu-id="42d63-145">`allowed-origins` can contain either a single `origin` element that specifies `*` to allow any origin, or one or more `origin` elements that contain a URI.</span></span>|<span data-ttu-id="42d63-146">Sì</span><span class="sxs-lookup"><span data-stu-id="42d63-146">Yes</span></span>|<span data-ttu-id="42d63-147">N/D</span><span class="sxs-lookup"><span data-stu-id="42d63-147">N/A</span></span>|  
|<span data-ttu-id="42d63-148">origin</span><span class="sxs-lookup"><span data-stu-id="42d63-148">origin</span></span>|<span data-ttu-id="42d63-149">Il valore può essere `*` per consentire tutte le origini oppure un URI che specifichi una singola origine.</span><span class="sxs-lookup"><span data-stu-id="42d63-149">The value can be either `*` to allow all origins, or a URI that specifies a single origin.</span></span> <span data-ttu-id="42d63-150">L'URI deve includere uno schema, un host e una porta.</span><span class="sxs-lookup"><span data-stu-id="42d63-150">The URI must include a scheme, host, and port.</span></span>|<span data-ttu-id="42d63-151">Sì</span><span class="sxs-lookup"><span data-stu-id="42d63-151">Yes</span></span>|<span data-ttu-id="42d63-152">Se la porta viene omessa in un URI, vengono utilizzate la porta 80 per HTTP e la porta 443 per HTTPS.</span><span class="sxs-lookup"><span data-stu-id="42d63-152">If the port is omitted in a URI, port 80 is used for HTTP and port 443 is used for HTTPS.</span></span>|  
|<span data-ttu-id="42d63-153">allowed-methods</span><span class="sxs-lookup"><span data-stu-id="42d63-153">allowed-methods</span></span>|<span data-ttu-id="42d63-154">Questo elemento è obbligatorio se sono consentiti metodi diversi da GET o POST.</span><span class="sxs-lookup"><span data-stu-id="42d63-154">This element is required if methods other than GET or POST are allowed.</span></span> <span data-ttu-id="42d63-155">Contiene elementi `method` che specificano i verbi HTTP supportati.</span><span class="sxs-lookup"><span data-stu-id="42d63-155">Contains `method` elements that specify the supported HTTP verbs.</span></span>|<span data-ttu-id="42d63-156">No</span><span class="sxs-lookup"><span data-stu-id="42d63-156">No</span></span>|<span data-ttu-id="42d63-157">Se questa sezione non è presente, sono supportati i metodi GET e POST.</span><span class="sxs-lookup"><span data-stu-id="42d63-157">If this section is not present, GET and POST are supported.</span></span>|  
|<span data-ttu-id="42d63-158">statico</span><span class="sxs-lookup"><span data-stu-id="42d63-158">method</span></span>|<span data-ttu-id="42d63-159">Specifica un verbo HTTP.</span><span class="sxs-lookup"><span data-stu-id="42d63-159">Specifies an HTTP verb.</span></span>|<span data-ttu-id="42d63-160">È richiesto almeno un elemento `method` se è presente la sezione `allowed-methods`.</span><span class="sxs-lookup"><span data-stu-id="42d63-160">At least one `method` element is required if the `allowed-methods` section is present.</span></span>|<span data-ttu-id="42d63-161">N/D</span><span class="sxs-lookup"><span data-stu-id="42d63-161">N/A</span></span>|  
|<span data-ttu-id="42d63-162">allowed-headers</span><span class="sxs-lookup"><span data-stu-id="42d63-162">allowed-headers</span></span>|<span data-ttu-id="42d63-163">Questo elemento contiene elementi `header` che specificano i nomi delle intestazioni che è possibile includere nella richiesta.</span><span class="sxs-lookup"><span data-stu-id="42d63-163">This element contains `header` elements specifying names of the headers that can be included in the request.</span></span>|<span data-ttu-id="42d63-164">No</span><span class="sxs-lookup"><span data-stu-id="42d63-164">No</span></span>|<span data-ttu-id="42d63-165">N/D</span><span class="sxs-lookup"><span data-stu-id="42d63-165">N/A</span></span>|  
|<span data-ttu-id="42d63-166">expose-headers</span><span class="sxs-lookup"><span data-stu-id="42d63-166">expose-headers</span></span>|<span data-ttu-id="42d63-167">Questo elemento contiene elementi `header` che specificano i nomi delle intestazioni accessibili dal client.</span><span class="sxs-lookup"><span data-stu-id="42d63-167">This element contains `header` elements specifying names of the headers that will be accessible by the client.</span></span>|<span data-ttu-id="42d63-168">No</span><span class="sxs-lookup"><span data-stu-id="42d63-168">No</span></span>|<span data-ttu-id="42d63-169">N/D</span><span class="sxs-lookup"><span data-stu-id="42d63-169">N/A</span></span>|  
|<span data-ttu-id="42d63-170">intestazione</span><span class="sxs-lookup"><span data-stu-id="42d63-170">header</span></span>|<span data-ttu-id="42d63-171">Specifica un nome di intestazione.</span><span class="sxs-lookup"><span data-stu-id="42d63-171">Specifies a header name.</span></span>|<span data-ttu-id="42d63-172">È richiesto almeno un elemento `header` in `allowed-headers` se è presente la sezione `expose-headers`.</span><span class="sxs-lookup"><span data-stu-id="42d63-172">At least one `header` element is required in `allowed-headers` or `expose-headers` if the section is present.</span></span>|<span data-ttu-id="42d63-173">N/D</span><span class="sxs-lookup"><span data-stu-id="42d63-173">N/A</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="42d63-174">Attributi</span><span class="sxs-lookup"><span data-stu-id="42d63-174">Attributes</span></span>  
  
|<span data-ttu-id="42d63-175">Nome</span><span class="sxs-lookup"><span data-stu-id="42d63-175">Name</span></span>|<span data-ttu-id="42d63-176">Descrizione</span><span class="sxs-lookup"><span data-stu-id="42d63-176">Description</span></span>|<span data-ttu-id="42d63-177">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="42d63-177">Required</span></span>|<span data-ttu-id="42d63-178">Default</span><span class="sxs-lookup"><span data-stu-id="42d63-178">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="42d63-179">allow-credentials</span><span class="sxs-lookup"><span data-stu-id="42d63-179">allow-credentials</span></span>|<span data-ttu-id="42d63-180">L'intestazione `Access-Control-Allow-Credentials` nella risposta preliminare verrà impostata sul valore di questo attributo e influirà sulla capacità del client di inviare credenziali in richieste tra domini.</span><span class="sxs-lookup"><span data-stu-id="42d63-180">The `Access-Control-Allow-Credentials` header in the preflight response will be set to the value of this attribute and affect the client’s ability to submit credentials in cross-domain requests.</span></span>|<span data-ttu-id="42d63-181">No</span><span class="sxs-lookup"><span data-stu-id="42d63-181">No</span></span>|<span data-ttu-id="42d63-182">false</span><span class="sxs-lookup"><span data-stu-id="42d63-182">false</span></span>|  
|<span data-ttu-id="42d63-183">preflight-result-max-age</span><span class="sxs-lookup"><span data-stu-id="42d63-183">preflight-result-max-age</span></span>|<span data-ttu-id="42d63-184">L'intestazione `Access-Control-Max-Age` nella risposta preliminare verrà impostata sul valore di questo attributo e influirà sulla capacità dell'agente utente di memorizzare nella cache la risposta preliminare.</span><span class="sxs-lookup"><span data-stu-id="42d63-184">The `Access-Control-Max-Age` header in the preflight response will be set to the value of this attribute and affect the user agent’s ability to cache pre-flight response.</span></span>|<span data-ttu-id="42d63-185">No</span><span class="sxs-lookup"><span data-stu-id="42d63-185">No</span></span>|<span data-ttu-id="42d63-186">0</span><span class="sxs-lookup"><span data-stu-id="42d63-186">0</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="42d63-187">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="42d63-187">Usage</span></span>  
 <span data-ttu-id="42d63-188">Questo criterio può essere usato nelle [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e negli [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) del criterio seguenti.</span><span class="sxs-lookup"><span data-stu-id="42d63-188">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="42d63-189">**Sezioni del criterio:** in ingresso</span><span class="sxs-lookup"><span data-stu-id="42d63-189">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="42d63-190">**Ambiti del criterio:** API, operazione</span><span class="sxs-lookup"><span data-stu-id="42d63-190">**Policy scopes:** API, operation</span></span>  
  
##  <span data-ttu-id="42d63-191"><a name="JSONP"></a> JSONP</span><span class="sxs-lookup"><span data-stu-id="42d63-191"><a name="JSONP"></a> JSONP</span></span>  
 <span data-ttu-id="42d63-192">Il criterio `jsonp` aggiunge il supporto per JSON con riempimento (JSONP) a un'operazione o a un'API per permettere le chiamate tra domini da client JavaScript basati su browser.</span><span class="sxs-lookup"><span data-stu-id="42d63-192">The `jsonp` policy adds JSON with padding (JSONP) support to an operation or an API to allow cross-domain calls from JavaScript browser-based clients.</span></span> <span data-ttu-id="42d63-193">JSONP è un metodo usato in programmi JavaScript per richiedere dati da un server in un dominio diverso.</span><span class="sxs-lookup"><span data-stu-id="42d63-193">JSONP is a method used in JavaScript programs to request data from a server in a different domain.</span></span> <span data-ttu-id="42d63-194">JSONP supera le limitazioni applicate dalla maggior parte dei Web browser, in cui l'accesso alle pagine Web deve essere effettuato nello stesso dominio.</span><span class="sxs-lookup"><span data-stu-id="42d63-194">JSONP bypasses the limitation enforced by most web browsers where access to web pages must be in the same domain.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="42d63-195">Istruzione del criterio</span><span class="sxs-lookup"><span data-stu-id="42d63-195">Policy statement</span></span>  
  
```xml  
<jsonp callback-parameter-name="callback function name" />  
```  
  
### <a name="example"></a><span data-ttu-id="42d63-196">Esempio</span><span class="sxs-lookup"><span data-stu-id="42d63-196">Example</span></span>  
  
```xml  
<jsonp callback-parameter-name="cb" />  
```  
  
 <span data-ttu-id="42d63-197">Se si chiama il metodo senza il parametro di callback ?cb=XXX restituirà JSON semplice, senza wrapper di chiamata della funzione.</span><span class="sxs-lookup"><span data-stu-id="42d63-197">If you call the method without the callback parameter ?cb=XXX it will return plain JSON (without a function call wrapper).</span></span>  
  
 <span data-ttu-id="42d63-198">Se si aggiunge il parametro di callback `?cb=XXX`, restituirà un risultato JSONP, eseguendo il wrapping dei risultati JSON originali intorno alla funzione di callback, ad esempio `XYZ('<json result goes here>');`</span><span class="sxs-lookup"><span data-stu-id="42d63-198">If you add the callback parameter `?cb=XXX` it will return a JSONP result, wrapping the original JSON results around the callback function like `XYZ('<json result goes here>');`</span></span>  
  
### <a name="elements"></a><span data-ttu-id="42d63-199">Elementi</span><span class="sxs-lookup"><span data-stu-id="42d63-199">Elements</span></span>  
  
|<span data-ttu-id="42d63-200">Nome</span><span class="sxs-lookup"><span data-stu-id="42d63-200">Name</span></span>|<span data-ttu-id="42d63-201">Descrizione</span><span class="sxs-lookup"><span data-stu-id="42d63-201">Description</span></span>|<span data-ttu-id="42d63-202">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="42d63-202">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="42d63-203">jsonp</span><span class="sxs-lookup"><span data-stu-id="42d63-203">jsonp</span></span>|<span data-ttu-id="42d63-204">Elemento radice.</span><span class="sxs-lookup"><span data-stu-id="42d63-204">Root element.</span></span>|<span data-ttu-id="42d63-205">Sì</span><span class="sxs-lookup"><span data-stu-id="42d63-205">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="42d63-206">Attributi</span><span class="sxs-lookup"><span data-stu-id="42d63-206">Attributes</span></span>  
  
|<span data-ttu-id="42d63-207">Nome</span><span class="sxs-lookup"><span data-stu-id="42d63-207">Name</span></span>|<span data-ttu-id="42d63-208">Descrizione</span><span class="sxs-lookup"><span data-stu-id="42d63-208">Description</span></span>|<span data-ttu-id="42d63-209">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="42d63-209">Required</span></span>|<span data-ttu-id="42d63-210">Default</span><span class="sxs-lookup"><span data-stu-id="42d63-210">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="42d63-211">callback-parameter-name</span><span class="sxs-lookup"><span data-stu-id="42d63-211">callback-parameter-name</span></span>|<span data-ttu-id="42d63-212">Funzione JavaScript tra domini che ha come prefisso il nome completo del dominio in cui si trova la funzione.</span><span class="sxs-lookup"><span data-stu-id="42d63-212">The cross-domain JavaScript function call prefixed with the fully qualified domain name where the function resides.</span></span>|<span data-ttu-id="42d63-213">Sì</span><span class="sxs-lookup"><span data-stu-id="42d63-213">Yes</span></span>|<span data-ttu-id="42d63-214">N/D</span><span class="sxs-lookup"><span data-stu-id="42d63-214">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="42d63-215">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="42d63-215">Usage</span></span>  
 <span data-ttu-id="42d63-216">Questo criterio può essere utilizzato nelle [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e negli [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) di criteri seguenti.</span><span class="sxs-lookup"><span data-stu-id="42d63-216">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="42d63-217">**Sezioni del criterio:** in uscita</span><span class="sxs-lookup"><span data-stu-id="42d63-217">**Policy sections:** outbound</span></span>  
  
-   <span data-ttu-id="42d63-218">**Ambiti del criterio:** globale, prodotto, API, operazione</span><span class="sxs-lookup"><span data-stu-id="42d63-218">**Policy scopes:** global, product, API, operation</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="42d63-219">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="42d63-219">Next steps</span></span>
<span data-ttu-id="42d63-220">Per altre informazioni sull'uso dei criteri, vedere [Criteri di Gestione API](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="42d63-220">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  