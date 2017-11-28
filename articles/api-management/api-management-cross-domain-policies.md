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
# <a name="api-management-cross-domain-policies"></a><span data-ttu-id="16a4f-103">Criteri tra domini di Gestione API</span><span class="sxs-lookup"><span data-stu-id="16a4f-103">API Management cross domain policies</span></span>
<span data-ttu-id="16a4f-104">In questo argomento fornisce un riferimento per i seguenti criteri di gestione API hello.</span><span class="sxs-lookup"><span data-stu-id="16a4f-104">This topic provides a reference for hello following API Management policies.</span></span> <span data-ttu-id="16a4f-105">Per informazioni sull'aggiunta e sulla configurazione dei criteri, vedere [Criteri di Gestione API](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="16a4f-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="16a4f-106"><a name="CrossDomainPolicies"></a> Criteri tra domini</span><span class="sxs-lookup"><span data-stu-id="16a4f-106"><a name="CrossDomainPolicies"></a> Cross domain policies</span></span>  
  
-   <span data-ttu-id="16a4f-107">[Consentire le chiamate tra domini](api-management-cross-domain-policies.md#AllowCrossDomainCalls) -rende accessibile hello API da client Adobe Flash e Microsoft Silverlight basati su browser.</span><span class="sxs-lookup"><span data-stu-id="16a4f-107">[Allow cross-domain calls](api-management-cross-domain-policies.md#AllowCrossDomainCalls) - Makes hello API accessible from Adobe Flash and Microsoft Silverlight browser-based clients.</span></span>  
  
-   <span data-ttu-id="16a4f-108">[CORS](api-management-cross-domain-policies.md#CORS) -aggiunge la condivisione di risorse multiorigine (CORS) supporta l'operazione di tooan o chiama un'API tooallow tra domini da client basati su browser.</span><span class="sxs-lookup"><span data-stu-id="16a4f-108">[CORS](api-management-cross-domain-policies.md#CORS) - Adds cross-origin resource sharing (CORS) support tooan operation or an API tooallow cross-domain calls from browser-based clients.</span></span>  
  
-   <span data-ttu-id="16a4f-109">[JSONP](api-management-cross-domain-policies.md#JSONP) - aggiunge JSON con riempimento (JSONP) supporto tooan operazione o chiama un'API tooallow tra domini da client JavaScript basati su browser.</span><span class="sxs-lookup"><span data-stu-id="16a4f-109">[JSONP](api-management-cross-domain-policies.md#JSONP) - Adds JSON with padding (JSONP) support tooan operation or an API tooallow cross-domain calls from JavaScript browser-based clients.</span></span>  
  
##  <span data-ttu-id="16a4f-110"><a name="AllowCrossDomainCalls"></a> Permetti chiamate tra i domini</span><span class="sxs-lookup"><span data-stu-id="16a4f-110"><a name="AllowCrossDomainCalls"></a> Allow cross-domain calls</span></span>  
 <span data-ttu-id="16a4f-111">Hello utilizzare `cross-domain` hello toomake criteri API accessibile da client Adobe Flash e Microsoft Silverlight basati su browser.</span><span class="sxs-lookup"><span data-stu-id="16a4f-111">Use hello `cross-domain` policy toomake hello API accessible from Adobe Flash and Microsoft Silverlight browser-based clients.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="16a4f-112">Istruzione del criterio</span><span class="sxs-lookup"><span data-stu-id="16a4f-112">Policy statement</span></span>  
  
```xml  
<cross-domain>  
   <!-Policy configuration is in hello Adobe cross-domain policy file format,   
      see http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html-->  
</cross-domain>  
```  
  
### <a name="example"></a><span data-ttu-id="16a4f-113">Esempio</span><span class="sxs-lookup"><span data-stu-id="16a4f-113">Example</span></span>  
  
```xml  
<cross-domain>  
    <cross-domain-policy>  
        <allow-http-request-headers-from domain='*' headers='*' />  
    </cross-domain-policy>  
</cross-domain>  
```  
  
### <a name="elements"></a><span data-ttu-id="16a4f-114">Elementi</span><span class="sxs-lookup"><span data-stu-id="16a4f-114">Elements</span></span>  
  
|<span data-ttu-id="16a4f-115">Nome</span><span class="sxs-lookup"><span data-stu-id="16a4f-115">Name</span></span>|<span data-ttu-id="16a4f-116">Descrizione</span><span class="sxs-lookup"><span data-stu-id="16a4f-116">Description</span></span>|<span data-ttu-id="16a4f-117">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="16a4f-117">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="16a4f-118">cross-domain</span><span class="sxs-lookup"><span data-stu-id="16a4f-118">cross-domain</span></span>|<span data-ttu-id="16a4f-119">Elemento radice.</span><span class="sxs-lookup"><span data-stu-id="16a4f-119">Root element.</span></span> <span data-ttu-id="16a4f-120">Gli elementi figlio devono essere conformi toohello [specifica del file di criteri tra domini di Adobe](http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html).</span><span class="sxs-lookup"><span data-stu-id="16a4f-120">Child elements must conform toohello [Adobe cross-domain policy file specification](http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html).</span></span>|<span data-ttu-id="16a4f-121">Sì</span><span class="sxs-lookup"><span data-stu-id="16a4f-121">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="16a4f-122">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="16a4f-122">Usage</span></span>  
 <span data-ttu-id="16a4f-123">Questo criterio può essere utilizzato hello seguenti criteri [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="16a4f-123">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="16a4f-124">**Sezioni del criterio:** inbound</span><span class="sxs-lookup"><span data-stu-id="16a4f-124">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="16a4f-125">**Ambiti del criterio:** globali</span><span class="sxs-lookup"><span data-stu-id="16a4f-125">**Policy scopes:** global</span></span>  
  
##  <span data-ttu-id="16a4f-126"><a name="CORS"></a> CORS</span><span class="sxs-lookup"><span data-stu-id="16a4f-126"><a name="CORS"></a> CORS</span></span>  
 <span data-ttu-id="16a4f-127">Hello `cors` criteri aggiunge la condivisione di risorse multiorigine (CORS) supporta l'operazione di tooan o chiama un'API tooallow tra domini da client basati su browser.</span><span class="sxs-lookup"><span data-stu-id="16a4f-127">hello `cors` policy adds cross-origin resource sharing (CORS) support tooan operation or an API tooallow cross-domain calls from browser-based clients.</span></span>  
  
 <span data-ttu-id="16a4f-128">CORS consente un browser e un server toointeract e determinare se tooallow specifico multiorigine richieste (ad esempio chiamate XMLHttpRequests eseguite da JavaScript su domini di tooother una pagina web).</span><span class="sxs-lookup"><span data-stu-id="16a4f-128">CORS allows a browser and a server toointeract and determine whether or not tooallow specific cross-origin requests (i.e. XMLHttpRequests calls made from JavaScript on a web page tooother domains).</span></span> <span data-ttu-id="16a4f-129">Ciò offre una maggiore flessibilità rispetto a permettere solo richieste con la stessa origine e una maggiore sicurezza rispetto a permettere tutte le richieste con origini diverse.</span><span class="sxs-lookup"><span data-stu-id="16a4f-129">This allows for more flexibility than only allowing same-origin requests, but is more secure than allowing all cross-origin requests.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="16a4f-130">Istruzione del criterio</span><span class="sxs-lookup"><span data-stu-id="16a4f-130">Policy statement</span></span>  
  
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
  
### <a name="example"></a><span data-ttu-id="16a4f-131">Esempio</span><span class="sxs-lookup"><span data-stu-id="16a4f-131">Example</span></span>  
 <span data-ttu-id="16a4f-132">In questo esempio viene illustrato come le richieste preliminari toosupport, ad esempio quelle con intestazioni personalizzate o metodi diversi da GET e POST.</span><span class="sxs-lookup"><span data-stu-id="16a4f-132">This example demonstrates how toosupport pre-flight requests, such as those with custom headers or methods other than GET and POST.</span></span> <span data-ttu-id="16a4f-133">toosupport le intestazioni personalizzate e verbi HTTP aggiuntivi, utilizzare hello `allowed-methods` e `allowed-headers` sezioni come illustrato nell'esempio seguente hello.</span><span class="sxs-lookup"><span data-stu-id="16a4f-133">toosupport custom headers and additional HTTP verbs, use hello `allowed-methods` and `allowed-headers` sections as shown in hello following example.</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="16a4f-134">Elementi</span><span class="sxs-lookup"><span data-stu-id="16a4f-134">Elements</span></span>  
  
|<span data-ttu-id="16a4f-135">Nome</span><span class="sxs-lookup"><span data-stu-id="16a4f-135">Name</span></span>|<span data-ttu-id="16a4f-136">Descrizione</span><span class="sxs-lookup"><span data-stu-id="16a4f-136">Description</span></span>|<span data-ttu-id="16a4f-137">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="16a4f-137">Required</span></span>|<span data-ttu-id="16a4f-138">Default</span><span class="sxs-lookup"><span data-stu-id="16a4f-138">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="16a4f-139">CORS</span><span class="sxs-lookup"><span data-stu-id="16a4f-139">cors</span></span>|<span data-ttu-id="16a4f-140">Elemento radice.</span><span class="sxs-lookup"><span data-stu-id="16a4f-140">Root element.</span></span>|<span data-ttu-id="16a4f-141">Sì</span><span class="sxs-lookup"><span data-stu-id="16a4f-141">Yes</span></span>|<span data-ttu-id="16a4f-142">N/D</span><span class="sxs-lookup"><span data-stu-id="16a4f-142">N/A</span></span>|  
|<span data-ttu-id="16a4f-143">allowed-origins</span><span class="sxs-lookup"><span data-stu-id="16a4f-143">allowed-origins</span></span>|<span data-ttu-id="16a4f-144">Contiene `origin` gli elementi che descrivono hello consentito le origini per le richieste tra domini.</span><span class="sxs-lookup"><span data-stu-id="16a4f-144">Contains `origin` elements that describe hello allowed origins for cross-domain requests.</span></span> <span data-ttu-id="16a4f-145">`allowed-origins`può contenere un singolo `origin` elemento che specifica `*` tooallow qualsiasi origine o di uno o più `origin` elementi che contengono un URI.</span><span class="sxs-lookup"><span data-stu-id="16a4f-145">`allowed-origins` can contain either a single `origin` element that specifies `*` tooallow any origin, or one or more `origin` elements that contain a URI.</span></span>|<span data-ttu-id="16a4f-146">Sì</span><span class="sxs-lookup"><span data-stu-id="16a4f-146">Yes</span></span>|<span data-ttu-id="16a4f-147">N/D</span><span class="sxs-lookup"><span data-stu-id="16a4f-147">N/A</span></span>|  
|<span data-ttu-id="16a4f-148">origin</span><span class="sxs-lookup"><span data-stu-id="16a4f-148">origin</span></span>|<span data-ttu-id="16a4f-149">Hello valore può essere `*` tooallow tutte le origini, oppure un URI che specifica una singola origine.</span><span class="sxs-lookup"><span data-stu-id="16a4f-149">hello value can be either `*` tooallow all origins, or a URI that specifies a single origin.</span></span> <span data-ttu-id="16a4f-150">Hello URI deve includere uno schema, l'host e porta.</span><span class="sxs-lookup"><span data-stu-id="16a4f-150">hello URI must include a scheme, host, and port.</span></span>|<span data-ttu-id="16a4f-151">Sì</span><span class="sxs-lookup"><span data-stu-id="16a4f-151">Yes</span></span>|<span data-ttu-id="16a4f-152">Se la porta hello viene omessa in un URI, viene utilizzata la porta 80 per HTTP e viene utilizzata la porta 443 per HTTPS.</span><span class="sxs-lookup"><span data-stu-id="16a4f-152">If hello port is omitted in a URI, port 80 is used for HTTP and port 443 is used for HTTPS.</span></span>|  
|<span data-ttu-id="16a4f-153">allowed-methods</span><span class="sxs-lookup"><span data-stu-id="16a4f-153">allowed-methods</span></span>|<span data-ttu-id="16a4f-154">Questo elemento è obbligatorio se sono consentiti metodi diversi da GET o POST.</span><span class="sxs-lookup"><span data-stu-id="16a4f-154">This element is required if methods other than GET or POST are allowed.</span></span> <span data-ttu-id="16a4f-155">Contiene `method` elementi che specificano hello verbi HTTP è supportata.</span><span class="sxs-lookup"><span data-stu-id="16a4f-155">Contains `method` elements that specify hello supported HTTP verbs.</span></span>|<span data-ttu-id="16a4f-156">No</span><span class="sxs-lookup"><span data-stu-id="16a4f-156">No</span></span>|<span data-ttu-id="16a4f-157">Se questa sezione non è presente, sono supportati i metodi GET e POST.</span><span class="sxs-lookup"><span data-stu-id="16a4f-157">If this section is not present, GET and POST are supported.</span></span>|  
|<span data-ttu-id="16a4f-158">statico</span><span class="sxs-lookup"><span data-stu-id="16a4f-158">method</span></span>|<span data-ttu-id="16a4f-159">Specifica un verbo HTTP.</span><span class="sxs-lookup"><span data-stu-id="16a4f-159">Specifies an HTTP verb.</span></span>|<span data-ttu-id="16a4f-160">Almeno un `method` elemento è obbligatorio se hello `allowed-methods` sezione è presente.</span><span class="sxs-lookup"><span data-stu-id="16a4f-160">At least one `method` element is required if hello `allowed-methods` section is present.</span></span>|<span data-ttu-id="16a4f-161">N/D</span><span class="sxs-lookup"><span data-stu-id="16a4f-161">N/A</span></span>|  
|<span data-ttu-id="16a4f-162">allowed-headers</span><span class="sxs-lookup"><span data-stu-id="16a4f-162">allowed-headers</span></span>|<span data-ttu-id="16a4f-163">Questo elemento contiene `header` gli elementi che specificano i nomi delle intestazioni di hello che possono essere incluso nella richiesta di hello.</span><span class="sxs-lookup"><span data-stu-id="16a4f-163">This element contains `header` elements specifying names of hello headers that can be included in hello request.</span></span>|<span data-ttu-id="16a4f-164">No</span><span class="sxs-lookup"><span data-stu-id="16a4f-164">No</span></span>|<span data-ttu-id="16a4f-165">N/D</span><span class="sxs-lookup"><span data-stu-id="16a4f-165">N/A</span></span>|  
|<span data-ttu-id="16a4f-166">expose-headers</span><span class="sxs-lookup"><span data-stu-id="16a4f-166">expose-headers</span></span>|<span data-ttu-id="16a4f-167">Questo elemento contiene `header` gli elementi che specificano i nomi delle intestazioni di hello che saranno accessibili dal client hello.</span><span class="sxs-lookup"><span data-stu-id="16a4f-167">This element contains `header` elements specifying names of hello headers that will be accessible by hello client.</span></span>|<span data-ttu-id="16a4f-168">No</span><span class="sxs-lookup"><span data-stu-id="16a4f-168">No</span></span>|<span data-ttu-id="16a4f-169">N/D</span><span class="sxs-lookup"><span data-stu-id="16a4f-169">N/A</span></span>|  
|<span data-ttu-id="16a4f-170">intestazione</span><span class="sxs-lookup"><span data-stu-id="16a4f-170">header</span></span>|<span data-ttu-id="16a4f-171">Specifica un nome di intestazione.</span><span class="sxs-lookup"><span data-stu-id="16a4f-171">Specifies a header name.</span></span>|<span data-ttu-id="16a4f-172">Almeno un `header` elemento è obbligatorio in `allowed-headers` o `expose-headers` se hello sezione è presente.</span><span class="sxs-lookup"><span data-stu-id="16a4f-172">At least one `header` element is required in `allowed-headers` or `expose-headers` if hello section is present.</span></span>|<span data-ttu-id="16a4f-173">N/D</span><span class="sxs-lookup"><span data-stu-id="16a4f-173">N/A</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="16a4f-174">Attributi</span><span class="sxs-lookup"><span data-stu-id="16a4f-174">Attributes</span></span>  
  
|<span data-ttu-id="16a4f-175">Nome</span><span class="sxs-lookup"><span data-stu-id="16a4f-175">Name</span></span>|<span data-ttu-id="16a4f-176">Descrizione</span><span class="sxs-lookup"><span data-stu-id="16a4f-176">Description</span></span>|<span data-ttu-id="16a4f-177">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="16a4f-177">Required</span></span>|<span data-ttu-id="16a4f-178">Default</span><span class="sxs-lookup"><span data-stu-id="16a4f-178">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="16a4f-179">allow-credentials</span><span class="sxs-lookup"><span data-stu-id="16a4f-179">allow-credentials</span></span>|<span data-ttu-id="16a4f-180">Hello `Access-Control-Allow-Credentials` intestazione nella risposta preliminare hello verrà toohello impostare il valore di questo attributo e influiscono su hello possibilità toosubmit credenziali client in richieste tra domini.</span><span class="sxs-lookup"><span data-stu-id="16a4f-180">hello `Access-Control-Allow-Credentials` header in hello preflight response will be set toohello value of this attribute and affect hello client’s ability toosubmit credentials in cross-domain requests.</span></span>|<span data-ttu-id="16a4f-181">No</span><span class="sxs-lookup"><span data-stu-id="16a4f-181">No</span></span>|<span data-ttu-id="16a4f-182">false</span><span class="sxs-lookup"><span data-stu-id="16a4f-182">false</span></span>|  
|<span data-ttu-id="16a4f-183">preflight-result-max-age</span><span class="sxs-lookup"><span data-stu-id="16a4f-183">preflight-result-max-age</span></span>|<span data-ttu-id="16a4f-184">Hello `Access-Control-Max-Age` intestazione nella risposta preliminare hello verrà toohello impostare il valore di questo attributo e influiscono sulla risposta preliminare toocache di capacità dell'agente utente hello.</span><span class="sxs-lookup"><span data-stu-id="16a4f-184">hello `Access-Control-Max-Age` header in hello preflight response will be set toohello value of this attribute and affect hello user agent’s ability toocache pre-flight response.</span></span>|<span data-ttu-id="16a4f-185">No</span><span class="sxs-lookup"><span data-stu-id="16a4f-185">No</span></span>|<span data-ttu-id="16a4f-186">0</span><span class="sxs-lookup"><span data-stu-id="16a4f-186">0</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="16a4f-187">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="16a4f-187">Usage</span></span>  
 <span data-ttu-id="16a4f-188">Questo criterio può essere utilizzato hello seguenti criteri [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="16a4f-188">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="16a4f-189">**Sezioni del criterio:** inbound</span><span class="sxs-lookup"><span data-stu-id="16a4f-189">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="16a4f-190">**Ambiti del criterio:** API, operazione</span><span class="sxs-lookup"><span data-stu-id="16a4f-190">**Policy scopes:** API, operation</span></span>  
  
##  <span data-ttu-id="16a4f-191"><a name="JSONP"></a> JSONP</span><span class="sxs-lookup"><span data-stu-id="16a4f-191"><a name="JSONP"></a> JSONP</span></span>  
 <span data-ttu-id="16a4f-192">Hello `jsonp` criteri aggiunge JSON con riempimento operazione tooan di supporto (JSONP) o le chiamate tra domini tooallow un'API da client JavaScript basati su browser.</span><span class="sxs-lookup"><span data-stu-id="16a4f-192">hello `jsonp` policy adds JSON with padding (JSONP) support tooan operation or an API tooallow cross-domain calls from JavaScript browser-based clients.</span></span> <span data-ttu-id="16a4f-193">JSONP è un metodo usato nei dati di toorequest programmi JavaScript da un server in un dominio diverso.</span><span class="sxs-lookup"><span data-stu-id="16a4f-193">JSONP is a method used in JavaScript programs toorequest data from a server in a different domain.</span></span> <span data-ttu-id="16a4f-194">JSONP supera limitazione hello applicata dalla maggior parte dei browser in cui devono essere pagine di accesso tooweb hello nello stesso dominio.</span><span class="sxs-lookup"><span data-stu-id="16a4f-194">JSONP bypasses hello limitation enforced by most web browsers where access tooweb pages must be in hello same domain.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="16a4f-195">Istruzione del criterio</span><span class="sxs-lookup"><span data-stu-id="16a4f-195">Policy statement</span></span>  
  
```xml  
<jsonp callback-parameter-name="callback function name" />  
```  
  
### <a name="example"></a><span data-ttu-id="16a4f-196">Esempio</span><span class="sxs-lookup"><span data-stu-id="16a4f-196">Example</span></span>  
  
```xml  
<jsonp callback-parameter-name="cb" />  
```  
  
 <span data-ttu-id="16a4f-197">Se si chiama il metodo hello senza il parametro di callback hello? cb = XXX restituirà JSON semplice (senza un wrapper di chiamata di funzione).</span><span class="sxs-lookup"><span data-stu-id="16a4f-197">If you call hello method without hello callback parameter ?cb=XXX it will return plain JSON (without a function call wrapper).</span></span>  
  
 <span data-ttu-id="16a4f-198">Se si aggiunge il parametro di callback hello `?cb=XXX` restituirà un risultato JSONP, wrapping risultati JSON originali hello per funzione di callback hello come`XYZ('<json result goes here>');`</span><span class="sxs-lookup"><span data-stu-id="16a4f-198">If you add hello callback parameter `?cb=XXX` it will return a JSONP result, wrapping hello original JSON results around hello callback function like `XYZ('<json result goes here>');`</span></span>  
  
### <a name="elements"></a><span data-ttu-id="16a4f-199">Elementi</span><span class="sxs-lookup"><span data-stu-id="16a4f-199">Elements</span></span>  
  
|<span data-ttu-id="16a4f-200">Nome</span><span class="sxs-lookup"><span data-stu-id="16a4f-200">Name</span></span>|<span data-ttu-id="16a4f-201">Descrizione</span><span class="sxs-lookup"><span data-stu-id="16a4f-201">Description</span></span>|<span data-ttu-id="16a4f-202">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="16a4f-202">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="16a4f-203">jsonp</span><span class="sxs-lookup"><span data-stu-id="16a4f-203">jsonp</span></span>|<span data-ttu-id="16a4f-204">Elemento radice.</span><span class="sxs-lookup"><span data-stu-id="16a4f-204">Root element.</span></span>|<span data-ttu-id="16a4f-205">Sì</span><span class="sxs-lookup"><span data-stu-id="16a4f-205">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="16a4f-206">Attributi</span><span class="sxs-lookup"><span data-stu-id="16a4f-206">Attributes</span></span>  
  
|<span data-ttu-id="16a4f-207">Nome</span><span class="sxs-lookup"><span data-stu-id="16a4f-207">Name</span></span>|<span data-ttu-id="16a4f-208">Descrizione</span><span class="sxs-lookup"><span data-stu-id="16a4f-208">Description</span></span>|<span data-ttu-id="16a4f-209">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="16a4f-209">Required</span></span>|<span data-ttu-id="16a4f-210">Default</span><span class="sxs-lookup"><span data-stu-id="16a4f-210">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="16a4f-211">callback-parameter-name</span><span class="sxs-lookup"><span data-stu-id="16a4f-211">callback-parameter-name</span></span>|<span data-ttu-id="16a4f-212">Hello chiamata alla funzione JavaScript tra domini con prefisso il nome di dominio completo hello in hello funzione risiede.</span><span class="sxs-lookup"><span data-stu-id="16a4f-212">hello cross-domain JavaScript function call prefixed with hello fully qualified domain name where hello function resides.</span></span>|<span data-ttu-id="16a4f-213">Sì</span><span class="sxs-lookup"><span data-stu-id="16a4f-213">Yes</span></span>|<span data-ttu-id="16a4f-214">N/D</span><span class="sxs-lookup"><span data-stu-id="16a4f-214">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="16a4f-215">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="16a4f-215">Usage</span></span>  
 <span data-ttu-id="16a4f-216">Questo criterio può essere utilizzato hello seguenti criteri [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="16a4f-216">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="16a4f-217">**Sezioni del criterio:** in uscita</span><span class="sxs-lookup"><span data-stu-id="16a4f-217">**Policy sections:** outbound</span></span>  
  
-   <span data-ttu-id="16a4f-218">**Ambiti del criterio:** globale, prodotto, API, operazione</span><span class="sxs-lookup"><span data-stu-id="16a4f-218">**Policy scopes:** global, product, API, operation</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="16a4f-219">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="16a4f-219">Next steps</span></span>
<span data-ttu-id="16a4f-220">Per altre informazioni sull'uso dei criteri, vedere [Criteri di Gestione API](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="16a4f-220">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  