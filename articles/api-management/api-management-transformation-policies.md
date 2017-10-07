---
title: criteri di trasformazione di gestione API aaaAzure | Documenti Microsoft
description: Informazioni sui criteri di trasformazione hello disponibili per l'utilizzo in Gestione API di Azure.
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 7406a8ce-5f9c-4fae-9b0f-e574befb2ee9
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 2891cc52d0017b717b3c12a98bc4941b5fd7ea78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-transformation-policies"></a><span data-ttu-id="497a1-103">Criteri di trasformazione di Gestione API</span><span class="sxs-lookup"><span data-stu-id="497a1-103">API Management transformation policies</span></span>
<span data-ttu-id="497a1-104">In questo argomento fornisce un riferimento per i seguenti criteri di gestione API hello.</span><span class="sxs-lookup"><span data-stu-id="497a1-104">This topic provides a reference for hello following API Management policies.</span></span> <span data-ttu-id="497a1-105">Per informazioni sull'aggiunta e sulla configurazione dei criteri, vedere [Criteri di Gestione API](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="497a1-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="497a1-106"><a name="TransformationPolicies"></a> Criteri di trasformazione</span><span class="sxs-lookup"><span data-stu-id="497a1-106"><a name="TransformationPolicies"></a> Transformation policies</span></span>  
  
-   <span data-ttu-id="497a1-107">[Convertire JSON tooXML](api-management-transformation-policies.md#ConvertJSONtoXML) - richiesta converte o corpo della risposta da JSON tooXML.</span><span class="sxs-lookup"><span data-stu-id="497a1-107">[Convert JSON tooXML](api-management-transformation-policies.md#ConvertJSONtoXML) - Converts request or response body from JSON tooXML.</span></span>  
  
-   <span data-ttu-id="497a1-108">[Convertire XML tooJSON](api-management-transformation-policies.md#ConvertXMLtoJSON) - richiesta converte o corpo della risposta da XML tooJSON.</span><span class="sxs-lookup"><span data-stu-id="497a1-108">[Convert XML tooJSON](api-management-transformation-policies.md#ConvertXMLtoJSON) - Converts request or response body from XML tooJSON.</span></span>  
  
-   <span data-ttu-id="497a1-109">[find-and-replace](api-management-transformation-policies.md#Findandreplacestringinbody) : trova una sottostringa di richiesta o risposta e la sostituisce con una sottostringa diversa.</span><span class="sxs-lookup"><span data-stu-id="497a1-109">[Find and replace string in body](api-management-transformation-policies.md#Findandreplacestringinbody) - Finds a request or response substring and replaces it with a different substring.</span></span>  
  
-   <span data-ttu-id="497a1-110">[Maschera URL nel contenuto](api-management-transformation-policies.md#MaskURLSContent) -riscrive (maschera) i collegamenti nella risposta hello corpo in modo che facciano riferimento toohello collegamento equivalente tramite il gateway hello.</span><span class="sxs-lookup"><span data-stu-id="497a1-110">[Mask URLs in content](api-management-transformation-policies.md#MaskURLSContent) - Re-writes (masks) links in hello response body so that they point toohello equivalent link via hello gateway.</span></span>  
  
-   <span data-ttu-id="497a1-111">[Impostare il servizio back-end](api-management-transformation-policies.md#SetBackendService) -Modifica servizio back-end hello per una richiesta in ingresso.</span><span class="sxs-lookup"><span data-stu-id="497a1-111">[Set backend service](api-management-transformation-policies.md#SetBackendService) - Changes hello backend service for an incoming request.</span></span>  
  
-   <span data-ttu-id="497a1-112">[Impostare corpo](api-management-transformation-policies.md#SetBody) -imposta corpo del messaggio hello per le richieste in ingresso e in uscita.</span><span class="sxs-lookup"><span data-stu-id="497a1-112">[Set body](api-management-transformation-policies.md#SetBody) - Sets hello message body for incoming and outgoing requests.</span></span>  
  
-   <span data-ttu-id="497a1-113">[Intestazione HTTP set](api-management-transformation-policies.md#SetHTTPheader) - assegna una risposta di valore tooan esistente e/o l'intestazione della richiesta o aggiunge una nuova intestazione di risposta e/o di richiesta.</span><span class="sxs-lookup"><span data-stu-id="497a1-113">[Set HTTP header](api-management-transformation-policies.md#SetHTTPheader) - Assigns a value tooan existing response and/or request header or adds a new response and/or request header.</span></span>  
  
-   <span data-ttu-id="497a1-114">[Imposta parametro di stringa della query](api-management-transformation-policies.md#SetQueryStringParameter) : aggiunge, sostituisce il valore di o elimina il parametro di stringa della query di richiesta.</span><span class="sxs-lookup"><span data-stu-id="497a1-114">[Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) - Adds, replaces value of, or deletes request query string parameter.</span></span>  
  
-   <span data-ttu-id="497a1-115">[Riscrittura URL](api-management-transformation-policies.md#RewriteURL) -converte un URL di richiesta dal formato pubblico toohello formato previsto dal servizio web hello.</span><span class="sxs-lookup"><span data-stu-id="497a1-115">[Rewrite URL](api-management-transformation-policies.md#RewriteURL) - Converts a request URL from its public form toohello form expected by hello web service.</span></span>  
  
-   <span data-ttu-id="497a1-116">[Trasformare XML utilizzando XSLT](api-management-transformation-policies.md#XSLTransform) -si applica un tooXML trasformazione XSL nel corpo della richiesta o risposta hello.</span><span class="sxs-lookup"><span data-stu-id="497a1-116">[Transform XML using an XSLT](api-management-transformation-policies.md#XSLTransform) - Applies an XSL transformation tooXML in hello request or response body.</span></span>  
  
##  <span data-ttu-id="497a1-117"><a name="ConvertJSONtoXML"></a>Convertire JSON tooXML</span><span class="sxs-lookup"><span data-stu-id="497a1-117"><a name="ConvertJSONtoXML"></a> Convert JSON tooXML</span></span>  
 <span data-ttu-id="497a1-118">Hello `json-to-xml` criteri converte un corpo della richiesta o risposta da JSON tooXML.</span><span class="sxs-lookup"><span data-stu-id="497a1-118">hello `json-to-xml` policy converts a request or response body from JSON tooXML.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="497a1-119">Istruzione del criterio</span><span class="sxs-lookup"><span data-stu-id="497a1-119">Policy statement</span></span>  
  
```xml  
<json-to-xml apply="always | content-type-json" consider-accept-header="true | false"/>  
```  
  
### <a name="example"></a><span data-ttu-id="497a1-120">Esempio</span><span class="sxs-lookup"><span data-stu-id="497a1-120">Example</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <base />  
    </inbound>  
    <outbound>  
        <base />  
        <json-to-xml apply="always" consider-accept-header="false" />  
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a><span data-ttu-id="497a1-121">Elementi</span><span class="sxs-lookup"><span data-stu-id="497a1-121">Elements</span></span>  
  
|<span data-ttu-id="497a1-122">Nome</span><span class="sxs-lookup"><span data-stu-id="497a1-122">Name</span></span>|<span data-ttu-id="497a1-123">Descrizione</span><span class="sxs-lookup"><span data-stu-id="497a1-123">Description</span></span>|<span data-ttu-id="497a1-124">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="497a1-124">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="497a1-125">json-to-xml</span><span class="sxs-lookup"><span data-stu-id="497a1-125">json-to-xml</span></span>|<span data-ttu-id="497a1-126">Elemento radice.</span><span class="sxs-lookup"><span data-stu-id="497a1-126">Root element.</span></span>|<span data-ttu-id="497a1-127">Sì</span><span class="sxs-lookup"><span data-stu-id="497a1-127">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="497a1-128">Attributi</span><span class="sxs-lookup"><span data-stu-id="497a1-128">Attributes</span></span>  
  
|<span data-ttu-id="497a1-129">Nome</span><span class="sxs-lookup"><span data-stu-id="497a1-129">Name</span></span>|<span data-ttu-id="497a1-130">Descrizione</span><span class="sxs-lookup"><span data-stu-id="497a1-130">Description</span></span>|<span data-ttu-id="497a1-131">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="497a1-131">Required</span></span>|<span data-ttu-id="497a1-132">Default</span><span class="sxs-lookup"><span data-stu-id="497a1-132">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="497a1-133">apply</span><span class="sxs-lookup"><span data-stu-id="497a1-133">apply</span></span>|<span data-ttu-id="497a1-134">attributo di Hello deve essere impostato tooone dei seguenti valori hello.</span><span class="sxs-lookup"><span data-stu-id="497a1-134">hello attribute must be set tooone of hello following values.</span></span><br /><br /> <span data-ttu-id="497a1-135">-   always - applica sempre la conversione.</span><span class="sxs-lookup"><span data-stu-id="497a1-135">-   always - always apply conversion.</span></span><br /><span data-ttu-id="497a1-136">-   content-type-json - applica la conversione solo se l'intestazione Content-Type della risposta indica la presenza di JSON.</span><span class="sxs-lookup"><span data-stu-id="497a1-136">-   content-type-json - convert only if response Content-Type header indicates presence of JSON.</span></span>|<span data-ttu-id="497a1-137">Sì</span><span class="sxs-lookup"><span data-stu-id="497a1-137">Yes</span></span>|<span data-ttu-id="497a1-138">N/D</span><span class="sxs-lookup"><span data-stu-id="497a1-138">N/A</span></span>|  
|<span data-ttu-id="497a1-139">consider-accept-header</span><span class="sxs-lookup"><span data-stu-id="497a1-139">consider-accept-header</span></span>|<span data-ttu-id="497a1-140">attributo di Hello deve essere impostato tooone dei seguenti valori hello.</span><span class="sxs-lookup"><span data-stu-id="497a1-140">hello attribute must be set tooone of hello following values.</span></span><br /><br /> <span data-ttu-id="497a1-141">-   true - applica la conversione se JSON è richiesto nell'intestazione Accept della richiesta.</span><span class="sxs-lookup"><span data-stu-id="497a1-141">-   true - apply conversion if JSON is requested in request Accept header.</span></span><br /><span data-ttu-id="497a1-142">-   false - applica sempre la conversione.</span><span class="sxs-lookup"><span data-stu-id="497a1-142">-   false -always apply conversion.</span></span>|<span data-ttu-id="497a1-143">No</span><span class="sxs-lookup"><span data-stu-id="497a1-143">No</span></span>|<span data-ttu-id="497a1-144">true</span><span class="sxs-lookup"><span data-stu-id="497a1-144">true</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="497a1-145">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="497a1-145">Usage</span></span>  
 <span data-ttu-id="497a1-146">Questo criterio può essere utilizzato hello seguenti criteri [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="497a1-146">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="497a1-147">**Sezioni del criterio:** inbound, outbound, on-error</span><span class="sxs-lookup"><span data-stu-id="497a1-147">**Policy sections:** inbound, outbound, on-error</span></span>  
  
-   <span data-ttu-id="497a1-148">**Ambiti del criterio:** globale, prodotto, API, operazione</span><span class="sxs-lookup"><span data-stu-id="497a1-148">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="497a1-149"><a name="ConvertXMLtoJSON"></a>Convertire XML tooJSON</span><span class="sxs-lookup"><span data-stu-id="497a1-149"><a name="ConvertXMLtoJSON"></a> Convert XML tooJSON</span></span>  
 <span data-ttu-id="497a1-150">Hello `xml-to-json` criteri converte un corpo della richiesta o risposta da XML tooJSON.</span><span class="sxs-lookup"><span data-stu-id="497a1-150">hello `xml-to-json` policy converts a request or response body from XML tooJSON.</span></span> <span data-ttu-id="497a1-151">Questo criterio può essere utilizzato toomodernize API basate su servizi web XML back-end solo.</span><span class="sxs-lookup"><span data-stu-id="497a1-151">This policy can be used toomodernize APIs based on XML-only backend web services.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="497a1-152">Istruzione del criterio</span><span class="sxs-lookup"><span data-stu-id="497a1-152">Policy statement</span></span>  
  
```xml  
<xml-to-json kind="javascript-friendly | direct" apply="always | content-type-xml" consider-accept-header="true | false"/>  
```  
  
### <a name="example"></a><span data-ttu-id="497a1-153">Esempio</span><span class="sxs-lookup"><span data-stu-id="497a1-153">Example</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <base />  
    </inbound>  
    <outbound>  
        <base />  
        <xml-to-json kind="direct" apply="always" consider-accept-header="false" />  
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a><span data-ttu-id="497a1-154">Elementi</span><span class="sxs-lookup"><span data-stu-id="497a1-154">Elements</span></span>  
  
|<span data-ttu-id="497a1-155">Nome</span><span class="sxs-lookup"><span data-stu-id="497a1-155">Name</span></span>|<span data-ttu-id="497a1-156">Descrizione</span><span class="sxs-lookup"><span data-stu-id="497a1-156">Description</span></span>|<span data-ttu-id="497a1-157">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="497a1-157">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="497a1-158">xml-to-json</span><span class="sxs-lookup"><span data-stu-id="497a1-158">xml-to-json</span></span>|<span data-ttu-id="497a1-159">Elemento radice.</span><span class="sxs-lookup"><span data-stu-id="497a1-159">Root element.</span></span>|<span data-ttu-id="497a1-160">Sì</span><span class="sxs-lookup"><span data-stu-id="497a1-160">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="497a1-161">Attributi</span><span class="sxs-lookup"><span data-stu-id="497a1-161">Attributes</span></span>  
  
|<span data-ttu-id="497a1-162">Nome</span><span class="sxs-lookup"><span data-stu-id="497a1-162">Name</span></span>|<span data-ttu-id="497a1-163">Descrizione</span><span class="sxs-lookup"><span data-stu-id="497a1-163">Description</span></span>|<span data-ttu-id="497a1-164">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="497a1-164">Required</span></span>|<span data-ttu-id="497a1-165">Default</span><span class="sxs-lookup"><span data-stu-id="497a1-165">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="497a1-166">kind</span><span class="sxs-lookup"><span data-stu-id="497a1-166">kind</span></span>|<span data-ttu-id="497a1-167">attributo di Hello deve essere impostato tooone dei seguenti valori hello.</span><span class="sxs-lookup"><span data-stu-id="497a1-167">hello attribute must be set tooone of hello following values.</span></span><br /><br /> <span data-ttu-id="497a1-168">hello-javascript friendly: convertita JSON con gli sviluppatori tooJavaScript descrittivo un modulo.</span><span class="sxs-lookup"><span data-stu-id="497a1-168">-   javascript-friendly - hello converted JSON has a form friendly tooJavaScript developers.</span></span><br /><span data-ttu-id="497a1-169">-direct: hello JSON convertito riflette la struttura del documento di hello originale XML.</span><span class="sxs-lookup"><span data-stu-id="497a1-169">-   direct - hello converted JSON reflects hello original XML document's structure.</span></span>|<span data-ttu-id="497a1-170">Sì</span><span class="sxs-lookup"><span data-stu-id="497a1-170">Yes</span></span>|<span data-ttu-id="497a1-171">N/D</span><span class="sxs-lookup"><span data-stu-id="497a1-171">N/A</span></span>|  
|<span data-ttu-id="497a1-172">apply</span><span class="sxs-lookup"><span data-stu-id="497a1-172">apply</span></span>|<span data-ttu-id="497a1-173">attributo di Hello deve essere impostato tooone dei seguenti valori hello.</span><span class="sxs-lookup"><span data-stu-id="497a1-173">hello attribute must be set tooone of hello following values.</span></span><br /><br /> <span data-ttu-id="497a1-174">-   always - esegue sempre la conversione.</span><span class="sxs-lookup"><span data-stu-id="497a1-174">-   always - convert always.</span></span><br /><span data-ttu-id="497a1-175">-   content-type-xml - applica la conversione solo se l'intestazione Content-Type della risposta indica la presenza di XML.</span><span class="sxs-lookup"><span data-stu-id="497a1-175">-   content-type-xml - convert only if response Content-Type header indicates presence of XML.</span></span>|<span data-ttu-id="497a1-176">Sì</span><span class="sxs-lookup"><span data-stu-id="497a1-176">Yes</span></span>|<span data-ttu-id="497a1-177">N/D</span><span class="sxs-lookup"><span data-stu-id="497a1-177">N/A</span></span>|  
|<span data-ttu-id="497a1-178">consider-accept-header</span><span class="sxs-lookup"><span data-stu-id="497a1-178">consider-accept-header</span></span>|<span data-ttu-id="497a1-179">attributo di Hello deve essere impostato tooone dei seguenti valori hello.</span><span class="sxs-lookup"><span data-stu-id="497a1-179">hello attribute must be set tooone of hello following values.</span></span><br /><br /> <span data-ttu-id="497a1-180">-   true - applica la conversione se XML è richiesto nell'intestazione Accept della richiesta.</span><span class="sxs-lookup"><span data-stu-id="497a1-180">-   true - apply conversion if XML is requested in request Accept header.</span></span><br /><span data-ttu-id="497a1-181">-   false - applica sempre la conversione.</span><span class="sxs-lookup"><span data-stu-id="497a1-181">-   false -always apply conversion.</span></span>|<span data-ttu-id="497a1-182">No</span><span class="sxs-lookup"><span data-stu-id="497a1-182">No</span></span>|<span data-ttu-id="497a1-183">true</span><span class="sxs-lookup"><span data-stu-id="497a1-183">true</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="497a1-184">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="497a1-184">Usage</span></span>  
 <span data-ttu-id="497a1-185">Questo criterio può essere utilizzato hello seguenti criteri [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="497a1-185">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="497a1-186">**Sezioni del criterio:** inbound, outbound, on-error</span><span class="sxs-lookup"><span data-stu-id="497a1-186">**Policy sections:** inbound, outbound, on-error</span></span>  
  
-   <span data-ttu-id="497a1-187">**Ambiti del criterio:** globale, prodotto, API, operazione</span><span class="sxs-lookup"><span data-stu-id="497a1-187">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="497a1-188"><a name="Findandreplacestringinbody"></a> Trova e sostituisci stringa nel corpo</span><span class="sxs-lookup"><span data-stu-id="497a1-188"><a name="Findandreplacestringinbody"></a> Find and replace string in body</span></span>  
 <span data-ttu-id="497a1-189">Hello `find-and-replace` criteri trova una sottostringa di richiesta o risposta e lo sostituisce con una sottostringa diversa.</span><span class="sxs-lookup"><span data-stu-id="497a1-189">hello `find-and-replace` policy finds a request or response substring and replaces it with a different substring.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="497a1-190">Istruzione del criterio</span><span class="sxs-lookup"><span data-stu-id="497a1-190">Policy statement</span></span>  
  
```xml  
<find-and-replace from="what tooreplace" to="replacement" />  
```  
  
### <a name="example"></a><span data-ttu-id="497a1-191">Esempio</span><span class="sxs-lookup"><span data-stu-id="497a1-191">Example</span></span>  
  
```xml  
<find-and-replace from="notebook" to="laptop" />  
```  
  
### <a name="elements"></a><span data-ttu-id="497a1-192">Elementi</span><span class="sxs-lookup"><span data-stu-id="497a1-192">Elements</span></span>  
  
|<span data-ttu-id="497a1-193">Nome</span><span class="sxs-lookup"><span data-stu-id="497a1-193">Name</span></span>|<span data-ttu-id="497a1-194">Descrizione</span><span class="sxs-lookup"><span data-stu-id="497a1-194">Description</span></span>|<span data-ttu-id="497a1-195">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="497a1-195">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="497a1-196">find-and-replace</span><span class="sxs-lookup"><span data-stu-id="497a1-196">find-and-replace</span></span>|<span data-ttu-id="497a1-197">Elemento radice.</span><span class="sxs-lookup"><span data-stu-id="497a1-197">Root element.</span></span>|<span data-ttu-id="497a1-198">Sì</span><span class="sxs-lookup"><span data-stu-id="497a1-198">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="497a1-199">Attributi</span><span class="sxs-lookup"><span data-stu-id="497a1-199">Attributes</span></span>  
  
|<span data-ttu-id="497a1-200">Nome</span><span class="sxs-lookup"><span data-stu-id="497a1-200">Name</span></span>|<span data-ttu-id="497a1-201">Descrizione</span><span class="sxs-lookup"><span data-stu-id="497a1-201">Description</span></span>|<span data-ttu-id="497a1-202">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="497a1-202">Required</span></span>|<span data-ttu-id="497a1-203">Default</span><span class="sxs-lookup"><span data-stu-id="497a1-203">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="497a1-204">from</span><span class="sxs-lookup"><span data-stu-id="497a1-204">from</span></span>|<span data-ttu-id="497a1-205">Hello stringa toosearch per.</span><span class="sxs-lookup"><span data-stu-id="497a1-205">hello string toosearch for.</span></span>|<span data-ttu-id="497a1-206">Sì</span><span class="sxs-lookup"><span data-stu-id="497a1-206">Yes</span></span>|<span data-ttu-id="497a1-207">N/D</span><span class="sxs-lookup"><span data-stu-id="497a1-207">N/A</span></span>|  
|<span data-ttu-id="497a1-208">to</span><span class="sxs-lookup"><span data-stu-id="497a1-208">to</span></span>|<span data-ttu-id="497a1-209">stringa di sostituzione Hello.</span><span class="sxs-lookup"><span data-stu-id="497a1-209">hello replacement string.</span></span> <span data-ttu-id="497a1-210">Specificare una sostituzione stringa tooremove hello ricerca stringa di lunghezza zero.</span><span class="sxs-lookup"><span data-stu-id="497a1-210">Specify a zero length replacement string tooremove hello search string.</span></span>|<span data-ttu-id="497a1-211">Sì</span><span class="sxs-lookup"><span data-stu-id="497a1-211">Yes</span></span>|<span data-ttu-id="497a1-212">N/D</span><span class="sxs-lookup"><span data-stu-id="497a1-212">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="497a1-213">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="497a1-213">Usage</span></span>  
 <span data-ttu-id="497a1-214">Questo criterio può essere utilizzato hello seguenti criteri [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="497a1-214">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="497a1-215">**Sezioni del criterio:** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="497a1-215">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="497a1-216">**Ambiti del criterio:** globale, prodotto, API, operazione</span><span class="sxs-lookup"><span data-stu-id="497a1-216">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="497a1-217"><a name="MaskURLSContent"></a> Maschera URL nel contenuto</span><span class="sxs-lookup"><span data-stu-id="497a1-217"><a name="MaskURLSContent"></a> Mask URLs in content</span></span>  
 <span data-ttu-id="497a1-218">Hello `redirect-content-urls` criteri riscrive (maschera) i collegamenti nel corpo della risposta hello in modo che facciano riferimento toohello collegamento equivalente tramite il gateway hello.</span><span class="sxs-lookup"><span data-stu-id="497a1-218">hello `redirect-content-urls` policy re-writes (masks) links in hello response body so that they point toohello equivalent link via hello gateway.</span></span> <span data-ttu-id="497a1-219">Usarli in hello sezione in uscita toore scrittura risposta corpo collegamenti toomake punto toohello gateway.</span><span class="sxs-lookup"><span data-stu-id="497a1-219">Use in hello outbound section toore-write response body links toomake them point toohello gateway.</span></span> <span data-ttu-id="497a1-220">Utilizzo in hello in ingresso di sezione per ottenere l'effetto opposto.</span><span class="sxs-lookup"><span data-stu-id="497a1-220">Use in hello inbound section for an opposite effect.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="497a1-221">Questo criterio non modifica i valori delle intestazioni, ad esempio le intestazioni `Location`.</span><span class="sxs-lookup"><span data-stu-id="497a1-221">This policy does not change any header values such as `Location` headers.</span></span> <span data-ttu-id="497a1-222">i valori di intestazione toochange, utilizzare hello [set intestazione](api-management-transformation-policies.md#SetHTTPheader) criteri.</span><span class="sxs-lookup"><span data-stu-id="497a1-222">toochange header values, use hello [set-header](api-management-transformation-policies.md#SetHTTPheader) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="497a1-223">Istruzione del criterio</span><span class="sxs-lookup"><span data-stu-id="497a1-223">Policy statement</span></span>  
  
```xml  
<redirect-content-urls />  
```  
  
### <a name="example"></a><span data-ttu-id="497a1-224">Esempio</span><span class="sxs-lookup"><span data-stu-id="497a1-224">Example</span></span>  
  
```xml  
<redirect-content-urls />  
```  
  
### <a name="elements"></a><span data-ttu-id="497a1-225">Elementi</span><span class="sxs-lookup"><span data-stu-id="497a1-225">Elements</span></span>  
  
|<span data-ttu-id="497a1-226">Nome</span><span class="sxs-lookup"><span data-stu-id="497a1-226">Name</span></span>|<span data-ttu-id="497a1-227">Descrizione</span><span class="sxs-lookup"><span data-stu-id="497a1-227">Description</span></span>|<span data-ttu-id="497a1-228">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="497a1-228">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="497a1-229">redirect-content-urls</span><span class="sxs-lookup"><span data-stu-id="497a1-229">redirect-content-urls</span></span>|<span data-ttu-id="497a1-230">Elemento radice.</span><span class="sxs-lookup"><span data-stu-id="497a1-230">Root element.</span></span>|<span data-ttu-id="497a1-231">Sì</span><span class="sxs-lookup"><span data-stu-id="497a1-231">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="497a1-232">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="497a1-232">Usage</span></span>  
 <span data-ttu-id="497a1-233">Questo criterio può essere utilizzato hello seguenti criteri [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="497a1-233">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="497a1-234">**Sezioni del criterio:** inbound, outbound</span><span class="sxs-lookup"><span data-stu-id="497a1-234">**Policy sections:** inbound, outbound</span></span>  
  
-   <span data-ttu-id="497a1-235">**Ambiti del criterio:** globale, prodotto, API, operazione</span><span class="sxs-lookup"><span data-stu-id="497a1-235">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="497a1-236"><a name="SetBackendService"></a> Imposta servizio back-end</span><span class="sxs-lookup"><span data-stu-id="497a1-236"><a name="SetBackendService"></a> Set backend service</span></span>  
 <span data-ttu-id="497a1-237">Hello utilizzare `set-backend-service` tooredirect criteri un in ingresso richiesta back-end diverso di tooa rispetto a quello specificato nelle impostazioni di hello API per l'operazione hello.</span><span class="sxs-lookup"><span data-stu-id="497a1-237">Use hello `set-backend-service` policy tooredirect an incoming request tooa different backend than hello one specified in hello API settings for that operation.</span></span> <span data-ttu-id="497a1-238">Questo criterio cambia hello back-end del servizio URL di base toohello richiesta in ingresso hello quello specificato nei criteri di hello.</span><span class="sxs-lookup"><span data-stu-id="497a1-238">This policy changes hello backend service base URL of hello incoming request toohello one specified in hello policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="497a1-239">Istruzione del criterio</span><span class="sxs-lookup"><span data-stu-id="497a1-239">Policy statement</span></span>  
  
```xml  
<set-backend-service base-url="base URL of hello backend service" />  
```  
  
### <a name="example"></a><span data-ttu-id="497a1-240">Esempio</span><span class="sxs-lookup"><span data-stu-id="497a1-240">Example</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <choose>  
            <when condition="@(context.Request.Url.Query.GetValueOrDefault("version") == "2013-05")">  
                <set-backend-service base-url="http://contoso.com/api/8.2/" />  
            </when>  
            <when condition="@(context.Request.Url.Query.GetValueOrDefault("version") == "2014-03")">  
                <set-backend-service base-url="http://contoso.com/api/9.1/" />  
            </when>  
        </choose>  
        <base />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
<span data-ttu-id="497a1-241">In questo hello esempio impostare i criteri del servizio back-end instrada le richieste in base al valore di versione di hello passato al servizio back-end diverso rispetto all'API hello specificato in un hello hello query stringa tooa.</span><span class="sxs-lookup"><span data-stu-id="497a1-241">In this example hello set backend service policy routes requests based on hello version value passed in hello query string tooa different backend service than hello one specified in hello API.</span></span>
  
<span data-ttu-id="497a1-242">Inizialmente hello URL di base del servizio back-end è derivato dalle impostazioni API hello.</span><span class="sxs-lookup"><span data-stu-id="497a1-242">Initially hello backend service base URL is derived from hello API settings.</span></span> <span data-ttu-id="497a1-243">Pertanto hello URL della richiesta `https://contoso.azure-api.net/api/partners/15?version=2013-05&subscription-key=abcdef` diventa `http://contoso.com/api/10.4/partners/15?version=2013-05&subscription-key=abcdef` dove `http://contoso.com/api/10.4/` hello URL del servizio back-end specificato nelle impostazioni di hello API.</span><span class="sxs-lookup"><span data-stu-id="497a1-243">So hello request URL `https://contoso.azure-api.net/api/partners/15?version=2013-05&subscription-key=abcdef` becomes `http://contoso.com/api/10.4/partners/15?version=2013-05&subscription-key=abcdef` where `http://contoso.com/api/10.4/` is hello backend service URL specified in hello API settings.</span></span>  
  
<span data-ttu-id="497a1-244">Quando hello [< scegliere\> ](api-management-advanced-policies.md#choose) istruzione dei criteri viene applicato l'URL di base del servizio back-end hello può cambiare di nuovo troppo`http://contoso.com/api/8.2` o `http://contoso.com/api/9.1`, a seconda del valore di hello hello versione richiesta del parametro della query.</span><span class="sxs-lookup"><span data-stu-id="497a1-244">When hello [<choose\>](api-management-advanced-policies.md#choose) policy statement is applied hello backend service base URL may change again either too`http://contoso.com/api/8.2` or `http://contoso.com/api/9.1`, depending on hello value of hello version request query parameter.</span></span> <span data-ttu-id="497a1-245">Ad esempio, se hello è `"2013-15"` richiesta finale di hello URL diventa `http://contoso.com/api/8.2/partners/15?version=2013-05&subscription-key=abcdef`.</span><span class="sxs-lookup"><span data-stu-id="497a1-245">For example, if hello value is `"2013-15"` hello final request URL becomes `http://contoso.com/api/8.2/partners/15?version=2013-05&subscription-key=abcdef`.</span></span>  
  
<span data-ttu-id="497a1-246">Se un'ulteriore trasformazione della richiesta di hello è desiderato, altri [criteri di trasformazione](api-management-transformation-policies.md#TransformationPolicies) può essere utilizzato.</span><span class="sxs-lookup"><span data-stu-id="497a1-246">If further transformation of hello request is desired, other [Transformation policies](api-management-transformation-policies.md#TransformationPolicies) can be used.</span></span> <span data-ttu-id="497a1-247">Ad esempio, tooremove hello versione query parametro ora che hello richiesta viene indirizzato tooa versione back-end specifico, hello [impostare il parametro di stringa di query](api-management-transformation-policies.md#SetQueryStringParameter) criteri possono essere l'attributo di versione divenuto ridondante hello di tooremove utilizzati.</span><span class="sxs-lookup"><span data-stu-id="497a1-247">For example, tooremove hello version query parameter now that hello request is being routed tooa version specific backend, hello  [Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) policy can be used tooremove hello now redundant version attribute.</span></span>  
  
### <a name="example"></a><span data-ttu-id="497a1-248">Esempio</span><span class="sxs-lookup"><span data-stu-id="497a1-248">Example</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <set-backend-service backend-id="my-sf-service" sf-partition-key="@(context.Request.Url.Query.GetValueOrDefault("userId","")" sf-replica-type="primary" /> 
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
<span data-ttu-id="497a1-249">In questo esempio hello criteri route hello richiesta tooa service fabric back-end, utilizzando una stringa di query userId hello come chiave di partizione hello e utilizzando hello replica primaria di partizione hello.</span><span class="sxs-lookup"><span data-stu-id="497a1-249">In this example hello policy routes hello request tooa service fabric backend, using hello userId query string as hello partition key and using hello primary replica of hello partition.</span></span>  

### <a name="elements"></a><span data-ttu-id="497a1-250">Elementi</span><span class="sxs-lookup"><span data-stu-id="497a1-250">Elements</span></span>  
  
|<span data-ttu-id="497a1-251">Nome</span><span class="sxs-lookup"><span data-stu-id="497a1-251">Name</span></span>|<span data-ttu-id="497a1-252">Descrizione</span><span class="sxs-lookup"><span data-stu-id="497a1-252">Description</span></span>|<span data-ttu-id="497a1-253">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="497a1-253">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="497a1-254">set-backend-service</span><span class="sxs-lookup"><span data-stu-id="497a1-254">set-backend-service</span></span>|<span data-ttu-id="497a1-255">Elemento radice.</span><span class="sxs-lookup"><span data-stu-id="497a1-255">Root element.</span></span>|<span data-ttu-id="497a1-256">Sì</span><span class="sxs-lookup"><span data-stu-id="497a1-256">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="497a1-257">Attributi</span><span class="sxs-lookup"><span data-stu-id="497a1-257">Attributes</span></span>  
  
|<span data-ttu-id="497a1-258">Nome</span><span class="sxs-lookup"><span data-stu-id="497a1-258">Name</span></span>|<span data-ttu-id="497a1-259">Descrizione</span><span class="sxs-lookup"><span data-stu-id="497a1-259">Description</span></span>|<span data-ttu-id="497a1-260">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="497a1-260">Required</span></span>|<span data-ttu-id="497a1-261">Default</span><span class="sxs-lookup"><span data-stu-id="497a1-261">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="497a1-262">base-url</span><span class="sxs-lookup"><span data-stu-id="497a1-262">base-url</span></span>|<span data-ttu-id="497a1-263">Nuovo URL di base del servizio back-end.</span><span class="sxs-lookup"><span data-stu-id="497a1-263">New backend service base URL.</span></span>|<span data-ttu-id="497a1-264">No</span><span class="sxs-lookup"><span data-stu-id="497a1-264">No</span></span>|<span data-ttu-id="497a1-265">N/D</span><span class="sxs-lookup"><span data-stu-id="497a1-265">N/A</span></span>|  
|<span data-ttu-id="497a1-266">backend-id</span><span class="sxs-lookup"><span data-stu-id="497a1-266">backend-id</span></span>|<span data-ttu-id="497a1-267">Identificatore di hello tooroute di back-end per.</span><span class="sxs-lookup"><span data-stu-id="497a1-267">Identifier of hello backend tooroute to.</span></span>|<span data-ttu-id="497a1-268">No</span><span class="sxs-lookup"><span data-stu-id="497a1-268">No</span></span>|<span data-ttu-id="497a1-269">N/D</span><span class="sxs-lookup"><span data-stu-id="497a1-269">N/A</span></span>|  
|<span data-ttu-id="497a1-270">sf-partition-key</span><span class="sxs-lookup"><span data-stu-id="497a1-270">sf-partition-key</span></span>|<span data-ttu-id="497a1-271">Questo campo è applicabile solo quando il back-end hello è un servizio di Service Fabric e viene specificata utilizzando 'id back-end'.</span><span class="sxs-lookup"><span data-stu-id="497a1-271">Only applicable when hello backend is a Service Fabric service and is specified using 'backend-id'.</span></span> <span data-ttu-id="497a1-272">Utilizzare una partizione specifica dal servizio di risoluzione del nome hello tooresolve.</span><span class="sxs-lookup"><span data-stu-id="497a1-272">Used tooresolve a specific partition from hello name resolution service.</span></span>|<span data-ttu-id="497a1-273">No</span><span class="sxs-lookup"><span data-stu-id="497a1-273">No</span></span>|<span data-ttu-id="497a1-274">N/D</span><span class="sxs-lookup"><span data-stu-id="497a1-274">N/A</span></span>|  
|<span data-ttu-id="497a1-275">sf-replica-type</span><span class="sxs-lookup"><span data-stu-id="497a1-275">sf-replica-type</span></span>|<span data-ttu-id="497a1-276">Questo campo è applicabile solo quando il back-end hello è un servizio di Service Fabric e viene specificata utilizzando 'id back-end'.</span><span class="sxs-lookup"><span data-stu-id="497a1-276">Only applicable when hello backend is a Service Fabric service and is specified using 'backend-id'.</span></span> <span data-ttu-id="497a1-277">Controlla se la richiesta hello deve diventare la replica primaria o secondaria di toohello di una partizione.</span><span class="sxs-lookup"><span data-stu-id="497a1-277">Controls if hello request should go toohello primary or secondary replica of a partition.</span></span> |<span data-ttu-id="497a1-278">No</span><span class="sxs-lookup"><span data-stu-id="497a1-278">No</span></span>|<span data-ttu-id="497a1-279">N/D</span><span class="sxs-lookup"><span data-stu-id="497a1-279">N/A</span></span>|    
|<span data-ttu-id="497a1-280">sf-resolve-condition</span><span class="sxs-lookup"><span data-stu-id="497a1-280">sf-resolve-condition</span></span>|<span data-ttu-id="497a1-281">Questo campo è applicabile solo quando il back-end hello è un servizio di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="497a1-281">Only applicable when hello backend is a Service Fabric service.</span></span> <span data-ttu-id="497a1-282">Condizione che identifica se hello chiama back-end dell'infrastruttura tooService ha toobe ripetuto con la risoluzione di nuovo.</span><span class="sxs-lookup"><span data-stu-id="497a1-282">Condition identifying if hello call tooService Fabric backend has toobe repeated with new resolution.</span></span>|<span data-ttu-id="497a1-283">No</span><span class="sxs-lookup"><span data-stu-id="497a1-283">No</span></span>|<span data-ttu-id="497a1-284">N/D</span><span class="sxs-lookup"><span data-stu-id="497a1-284">N/A</span></span>|    
|<span data-ttu-id="497a1-285">sf-service-instance-name</span><span class="sxs-lookup"><span data-stu-id="497a1-285">sf-service-instance-name</span></span>|<span data-ttu-id="497a1-286">Questo campo è applicabile solo quando il back-end hello è un servizio di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="497a1-286">Only applicable when hello backend is a Service Fabric service.</span></span> <span data-ttu-id="497a1-287">Consente toochange le istanze del servizio in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="497a1-287">Allows toochange service instances at runtime.</span></span> |<span data-ttu-id="497a1-288">No</span><span class="sxs-lookup"><span data-stu-id="497a1-288">No</span></span>|<span data-ttu-id="497a1-289">N/D </span><span class="sxs-lookup"><span data-stu-id="497a1-289">N/A</span></span>|    

### <a name="usage"></a><span data-ttu-id="497a1-290">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="497a1-290">Usage</span></span>  
 <span data-ttu-id="497a1-291">Questo criterio può essere utilizzato hello seguenti criteri [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="497a1-291">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="497a1-292">**Sezioni del criterio:** inbound, backend</span><span class="sxs-lookup"><span data-stu-id="497a1-292">**Policy sections:** inbound, backend</span></span>  
  
-   <span data-ttu-id="497a1-293">**Ambiti del criterio:** globale, prodotto, API, operazione</span><span class="sxs-lookup"><span data-stu-id="497a1-293">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="497a1-294"><a name="SetBody"></a> Imposta corpo</span><span class="sxs-lookup"><span data-stu-id="497a1-294"><a name="SetBody"></a> Set body</span></span>  
 <span data-ttu-id="497a1-295">Hello utilizzare `set-body` corpo del messaggio hello tooset criteri per le richieste in ingresso e in uscita.</span><span class="sxs-lookup"><span data-stu-id="497a1-295">Use hello `set-body` policy tooset hello message body for incoming and outgoing requests.</span></span> <span data-ttu-id="497a1-296">tooaccess hello corpo del messaggio è possibile utilizzare hello `context.Request.Body` proprietà o hello `context.Response.Body`, a seconda se i criteri di hello sono hello sezione in ingresso o in uscita.</span><span class="sxs-lookup"><span data-stu-id="497a1-296">tooaccess hello message body you can use hello `context.Request.Body` property or hello `context.Response.Body`, depending on whether hello policy is in hello inbound or outbound section.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="497a1-297">Si noti che per impostazione predefinita quando si accede a hello corpo del messaggio tramite `context.Request.Body` o `context.Response.Body`, messaggio originale viene perso e deve essere impostato riportandolo corpo hello in espressione hello.</span><span class="sxs-lookup"><span data-stu-id="497a1-297">Note that by default when you access hello message body using `context.Request.Body` or `context.Response.Body`, hello original message body is lost and must be set by returning hello body back in hello expression.</span></span> <span data-ttu-id="497a1-298">toopreserve hello contenuto del corpo, impostare hello `preserveContent` parametro troppo`true` quando si accede a messaggio hello.</span><span class="sxs-lookup"><span data-stu-id="497a1-298">toopreserve hello body content, set hello `preserveContent` parameter too`true` when accessing hello message.</span></span> <span data-ttu-id="497a1-299">Se `preserveContent` è troppo`true` e viene restituito un corpo diverso dall'espressione hello, hello restituito corpo viene utilizzato.</span><span class="sxs-lookup"><span data-stu-id="497a1-299">If `preserveContent` is set too`true` and a different body is returned by hello expression, hello returned body is used.</span></span>  
>   
>  <span data-ttu-id="497a1-300">Si noti hello seguenti considerazioni quando si utilizza hello `set-body` criteri.</span><span class="sxs-lookup"><span data-stu-id="497a1-300">Please note hello following considerations when using hello `set-body` policy.</span></span>  
>   
>  -   <span data-ttu-id="497a1-301">Se si utilizza hello `set-body` tooreturn criteri un corpo di nuovo o aggiornato non è necessario tooset `preserveContent` troppo`true` perché in modo esplicito di fornire contenuto del corpo del nuovo hello.</span><span class="sxs-lookup"><span data-stu-id="497a1-301">If you are using hello `set-body` policy tooreturn a new or updated body you don't need tooset `preserveContent` too`true` because you are explicitly supplying hello new body contents.</span></span>  
> -   <span data-ttu-id="497a1-302">Mantenere il contenuto di hello di una risposta in pipeline in ingresso hello non ha senso perché non è ancora stata ricevuta alcuna risposta.</span><span class="sxs-lookup"><span data-stu-id="497a1-302">Preserving hello content of a response in hello inbound pipeline doesn't make sense because there is no response yet.</span></span>  
> -   <span data-ttu-id="497a1-303">Mantenere il contenuto di hello di una richiesta nella pipeline in uscita hello non hanno alcun significato poiché hello richiesta è già stata inviata back-end toohello a questo punto.</span><span class="sxs-lookup"><span data-stu-id="497a1-303">Preserving hello content of a request in hello outbound pipeline doesn't make sense because hello request has already been sent toohello backend at this point.</span></span>  
> -   <span data-ttu-id="497a1-304">Se questo criterio viene usato quando non vi è alcun corpo del messaggio, ad esempio in un'operazione GET in ingresso, viene generata un'eccezione.</span><span class="sxs-lookup"><span data-stu-id="497a1-304">If this policy is used when there is no message body, for example in an inbound GET, an exception is thrown.</span></span>  
  
 <span data-ttu-id="497a1-305">Per ulteriori informazioni, vedere hello `context.Request.Body`, `context.Response.Body`, hello e `IMessage` sezioni hello [variabile di contesto](api-management-policy-expressions.md#ContextVariables) tabella.</span><span class="sxs-lookup"><span data-stu-id="497a1-305">For more information, see hello `context.Request.Body`, `context.Response.Body`, and hello `IMessage` sections in hello [Context variable](api-management-policy-expressions.md#ContextVariables) table.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="497a1-306">Istruzione del criterio</span><span class="sxs-lookup"><span data-stu-id="497a1-306">Policy statement</span></span>  
  
```xml  
<set-body>new body value as text</set-body>  
```  
  
### <a name="examples"></a><span data-ttu-id="497a1-307">Esempi</span><span class="sxs-lookup"><span data-stu-id="497a1-307">Examples</span></span>  
  
#### <a name="literal-text-example"></a><span data-ttu-id="497a1-308">Esempio di testo letterale</span><span class="sxs-lookup"><span data-stu-id="497a1-308">Literal text example</span></span>  
  
```xml  
<set-body>Hello world!</set-body>  
```  
  
#### <a name="example-accessing-hello-body-as-a-string-note-that-we-are-preserving-hello-original-request-body-so-that-we-can-access-it-later-in-hello-pipeline"></a><span data-ttu-id="497a1-309">Esempio di accesso hello corpo sotto forma di stringa.</span><span class="sxs-lookup"><span data-stu-id="497a1-309">Example accessing hello body as a string.</span></span> <span data-ttu-id="497a1-310">Si noti che stiamo lavorando alla conservazione corpo della richiesta originale hello in modo che è possibile accedervi in un secondo momento nella pipeline di hello.</span><span class="sxs-lookup"><span data-stu-id="497a1-310">Note that we are preserving hello original request body so that we can access it later in hello pipeline.</span></span>
  
```xml  
<set-body>  
@{   
    string inBody = context.Request.Body.As<string>(preserveContent: true);   
    if (inBody[0] =='c') {   
        inBody[0] = 'm';   
    }   
    return inBody;   
}  
</set-body>  
```  
  
#### <a name="example-accessing-hello-body-as-a-jobject-note-that-since-we-are-not-reserving-hello-original-request-body-accesing-it-later-in-hello-pipeline-will-result-in-an-exception"></a><span data-ttu-id="497a1-311">Esempio di accesso hello corpo sotto forma di JObject.</span><span class="sxs-lookup"><span data-stu-id="497a1-311">Example accessing hello body as a JObject.</span></span> <span data-ttu-id="497a1-312">Si noti che, poiché si sta riservando non hello originale corpo della richiesta, in un secondo momento nella pipeline di hello causerà un'eccezione di accesso.</span><span class="sxs-lookup"><span data-stu-id="497a1-312">Note that since we are not reserving hello original request body, accesing it later in hello pipeline will result in an exception.</span></span>  
  
```xml  
<set-body>   
@{   
    JObject inBody = context.Request.Body.As<JObject>();   
    if (inBody.attribute == <tag>) {   
        inBody[0] = 'm';   
    }   
    return inBody.ToString();   
}   
</set-body>  
  
```  
  
#### <a name="filter-response-based-on-product"></a><span data-ttu-id="497a1-313">Filtrare la risposta in base al prodotto</span><span class="sxs-lookup"><span data-stu-id="497a1-313">Filter response based on product</span></span>  
 <span data-ttu-id="497a1-314">Questo esempio viene illustrato come tooperform contenuto applicando un filtro per la rimozione degli elementi di dati dalla risposta hello ricevuto dal servizio back-end hello quando si utilizza hello `Starter` prodotto.</span><span class="sxs-lookup"><span data-stu-id="497a1-314">This example shows how tooperform content filtering by removing data elements from hello response received from hello backend service when using hello `Starter` product.</span></span> <span data-ttu-id="497a1-315">Per una dimostrazione della configurazione e l'utilizzo di questo criterio, vedere [Cloud coprire episodio 177: più API le funzionalità di gestione con Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) e far avanzare rapidamente too34:30.</span><span class="sxs-lookup"><span data-stu-id="497a1-315">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too34:30.</span></span> <span data-ttu-id="497a1-316">Inizia dal 31:50 toosee Cenni preliminari [hello scuro Sky previsione API](https://developer.forecast.io/) utilizzato per questa dimostrazione.</span><span class="sxs-lookup"><span data-stu-id="497a1-316">Start  at 31:50 toosee an overview of [hello Dark Sky Forecast API](https://developer.forecast.io/) used for this demo.</span></span>  
  
```xml  
<!-- Copy this snippet into hello outbound section tooremove a number of data elements from hello response received from hello backend service based on hello name of hello api product -->  
<choose>  
  <when condition="@(context.Response.StatusCode == 200 && context.Product.Name.Equals("Starter"))">  
    <set-body>@{  
        var response = context.Response.Body.As<JObject>();  
        foreach (var key in new [] {"minutely", "hourly", "daily", "flags"}) {  
          response.Property (key).Remove ();  
        }  
        return response.ToString();  
      }  
    </set-body>  
  </when>  
</choose>  
```  

### <a name="using-liquid-templates-with-set-body"></a><span data-ttu-id="497a1-317">Uso di modelli Liquid con set body</span><span class="sxs-lookup"><span data-stu-id="497a1-317">Using Liquid templates with set body</span></span> 
<span data-ttu-id="497a1-318">Hello `set-body` criteri possono essere configurato toouse hello [liquide](https://shopify.github.io/liquid/basics/introduction/) modelli linguaggio tootransfom hello corpo di una richiesta o risposta.</span><span class="sxs-lookup"><span data-stu-id="497a1-318">hello `set-body` policy can be configured toouse hello [Liquid](https://shopify.github.io/liquid/basics/introduction/) templating language tootransfom hello body of a request or response.</span></span> <span data-ttu-id="497a1-319">Può essere molto efficace se occorre un formato di hello toocompletely nuova forma del messaggio.</span><span class="sxs-lookup"><span data-stu-id="497a1-319">This can be very effective if you need toocompletely reshape hello format of your message.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="497a1-320">implementazione di soluzione usato in hello Hello `set-body` criterio è configurato in modalità c#.</span><span class="sxs-lookup"><span data-stu-id="497a1-320">hello implementation of Liquid used in hello `set-body` policy is configured in 'C# mode'.</span></span> <span data-ttu-id="497a1-321">Questo è particolarmente importante quando si eseguono operazioni quali l'applicazione del filtro.</span><span class="sxs-lookup"><span data-stu-id="497a1-321">This is particularly important when doing things such as filtering.</span></span> <span data-ttu-id="497a1-322">Ad esempio, utilizzando un filtro data richiede l'uso di hello di Pascal maiuscole e minuscole e c# è data la formattazione, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="497a1-322">As an example, using a date filter requires hello use of Pascal casing and C# date formatting e.g.:</span></span>
>
> <span data-ttu-id="497a1-323">{{body.foo.startDateTime| Data:"yyyyMMddTHH:mm:ddZ"}}</span><span class="sxs-lookup"><span data-stu-id="497a1-323">{{body.foo.startDateTime| Date:"yyyyMMddTHH:mm:ddZ"}}</span></span>

> [!IMPORTANT]
> <span data-ttu-id="497a1-324">In ordine toocorrectly binding tooan corpo XML con modello liquide hello, utilizzare un `set-header` criteri tooset Content-Type tooeither application/xml, testo/xml (o qualsiasi tipo che termina con + xml); per un corpo JSON, deve essere application/json, testo/json (o qualsiasi finale di tipo con + json).</span><span class="sxs-lookup"><span data-stu-id="497a1-324">In order toocorrectly bind tooan XML body using hello Liquid template, use a `set-header` policy tooset Content-Type tooeither application/xml, text/xml (or any type ending with +xml); for a JSON body, it must be application/json, text/json (or any type ending with +json).</span></span>

#### <a name="convert-json-toosoap-using-a-liquid-template"></a><span data-ttu-id="497a1-325">Convertire tooSOAP JSON utilizzando un modello liquido</span><span class="sxs-lookup"><span data-stu-id="497a1-325">Convert JSON tooSOAP using a Liquid template</span></span>
```xml
<set-body template="liquid">
    <soap:Envelope xmlns="http://tempuri.org/" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
        <soap:Body>
            <GetOpenOrders>
                <cust>{{body.getOpenOrders.cust}}</cust>
            </GetOpenOrders>
        </soap:Body>
    </soap:Envelope>
</set-body>
```

#### <a name="tranform-json-using-a-liquid-template"></a><span data-ttu-id="497a1-326">Trasformare JSON usando un modello Liquid</span><span class="sxs-lookup"><span data-stu-id="497a1-326">Tranform JSON using a Liquid template</span></span>
```xml
{
"order": {
    "id": "{{body.customer.purchase.identifier}}",
    "summary": "{{body.customer.purchase.orderShortDesc}}"
    }
}
```

### <a name="elements"></a><span data-ttu-id="497a1-327">Elementi</span><span class="sxs-lookup"><span data-stu-id="497a1-327">Elements</span></span>  
  
|<span data-ttu-id="497a1-328">Nome</span><span class="sxs-lookup"><span data-stu-id="497a1-328">Name</span></span>|<span data-ttu-id="497a1-329">Descrizione</span><span class="sxs-lookup"><span data-stu-id="497a1-329">Description</span></span>|<span data-ttu-id="497a1-330">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="497a1-330">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="497a1-331">set-body</span><span class="sxs-lookup"><span data-stu-id="497a1-331">set-body</span></span>|<span data-ttu-id="497a1-332">Elemento radice.</span><span class="sxs-lookup"><span data-stu-id="497a1-332">Root element.</span></span> <span data-ttu-id="497a1-333">Contiene testo hello o un'espressione che restituisce un corpo.</span><span class="sxs-lookup"><span data-stu-id="497a1-333">Contains hello body text or an expressions that returns a body.</span></span>|<span data-ttu-id="497a1-334">Sì</span><span class="sxs-lookup"><span data-stu-id="497a1-334">Yes</span></span>|  

### <a name="properties"></a><span data-ttu-id="497a1-335">Proprietà</span><span class="sxs-lookup"><span data-stu-id="497a1-335">Properties</span></span>  
  
|<span data-ttu-id="497a1-336">Nome</span><span class="sxs-lookup"><span data-stu-id="497a1-336">Name</span></span>|<span data-ttu-id="497a1-337">Descrizione</span><span class="sxs-lookup"><span data-stu-id="497a1-337">Description</span></span>|<span data-ttu-id="497a1-338">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="497a1-338">Required</span></span>|<span data-ttu-id="497a1-339">Default</span><span class="sxs-lookup"><span data-stu-id="497a1-339">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="497a1-340">template</span><span class="sxs-lookup"><span data-stu-id="497a1-340">template</span></span>|<span data-ttu-id="497a1-341">Verrà eseguito in modalità modello toochange utilizzato hello che hello corpo impostare i criteri in.</span><span class="sxs-lookup"><span data-stu-id="497a1-341">Used toochange hello templating mode that hello set body policy will run in.</span></span> <span data-ttu-id="497a1-342">Il valore di hello solo supportato attualmente è:</span><span class="sxs-lookup"><span data-stu-id="497a1-342">Currently hello only supported value is:</span></span><br /><br /><span data-ttu-id="497a1-343">hello - liquide - impostare i criteri corpo utilizzerà motore del modello liquide hello</span><span class="sxs-lookup"><span data-stu-id="497a1-343">- liquid - hello set body policy will use hello liquid templating engine</span></span> |<span data-ttu-id="497a1-344">No</span><span class="sxs-lookup"><span data-stu-id="497a1-344">No</span></span>|<span data-ttu-id="497a1-345">liquid</span><span class="sxs-lookup"><span data-stu-id="497a1-345">liquid</span></span>|  

<span data-ttu-id="497a1-346">Per l'accesso alle informazioni hello richiesta e risposta, modello liquide hello può associare l'oggetto di contesto tooa con hello le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="497a1-346">For accessing information about hello request and response, hello Liquid template can bind tooa context object with hello following properties:</span></span> <br />
<pre>context.
    Request.
        Url
        Method
        OriginalMethod
        OriginalUrl
        IpAddress
        MatchedParameters
        HasBody
        ClientCertificates
        Headers

    Response.
        StatusCode
        Method
        Headers
Url.
    Scheme
    Host
    Port
    Path
    Query
    QueryString
    ToUri
    ToString

OriginalUrl.
    Scheme
    Host
    Port
    Path
    Query
    QueryString
    ToUri
    ToString
</pre>



### <a name="usage"></a><span data-ttu-id="497a1-347">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="497a1-347">Usage</span></span>  
 <span data-ttu-id="497a1-348">Questo criterio può essere utilizzato hello seguenti criteri [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="497a1-348">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="497a1-349">**Sezioni del criterio:** inbound, outbound, back-end</span><span class="sxs-lookup"><span data-stu-id="497a1-349">**Policy sections:** inbound, outbound, backend</span></span>  
  
-   <span data-ttu-id="497a1-350">**Ambiti del criterio:** globale, prodotto, API, operazione</span><span class="sxs-lookup"><span data-stu-id="497a1-350">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="497a1-351"><a name="SetHTTPheader"></a> Imposta intestazione HTTP</span><span class="sxs-lookup"><span data-stu-id="497a1-351"><a name="SetHTTPheader"></a> Set HTTP header</span></span>  
 <span data-ttu-id="497a1-352">Hello `set-header` criteri assegna una risposta di valore tooan esistente e/o l'intestazione della richiesta oppure aggiunge una nuova intestazione di risposta e/o di richiesta.</span><span class="sxs-lookup"><span data-stu-id="497a1-352">hello `set-header` policy assigns a value tooan existing response and/or request header or adds a new response and/or request header.</span></span>  
  
 <span data-ttu-id="497a1-353">Inserisce un elenco di intestazioni HTTP in un messaggio HTTP.</span><span class="sxs-lookup"><span data-stu-id="497a1-353">Inserts a list of HTTP headers into an HTTP message.</span></span> <span data-ttu-id="497a1-354">Se inserito in una pipeline in ingresso, questo criterio imposta le intestazioni HTTP hello per richiesta hello passati toohello servizio di destinazione.</span><span class="sxs-lookup"><span data-stu-id="497a1-354">When placed in an inbound pipeline, this policy sets hello HTTP headers for hello request being passed toohello target service.</span></span> <span data-ttu-id="497a1-355">Se inserito in una pipeline in uscita, questo criterio imposta le intestazioni HTTP hello per risposta hello inviati client toohello del gateway.</span><span class="sxs-lookup"><span data-stu-id="497a1-355">When placed in an outbound pipeline, this policy sets hello HTTP headers for hello response being sent toohello gateway’s client.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="497a1-356">Istruzione del criterio</span><span class="sxs-lookup"><span data-stu-id="497a1-356">Policy statement</span></span>  
  
```xml  
<set-header name="header name" exists-action="override | skip | append | delete">  
    <value>value</value> <!--for multiple headers with hello same name add additional value elements-->  
</set-header>  
```  
  
### <a name="examples"></a><span data-ttu-id="497a1-357">Esempi</span><span class="sxs-lookup"><span data-stu-id="497a1-357">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="497a1-358">Esempio</span><span class="sxs-lookup"><span data-stu-id="497a1-358">Example</span></span>  
  
```xml  
<set-header name="some header name" exists-action="override">  
    <value>20</value>   
</set-header>  
```  
  
#### <a name="forward-context-information-toohello-backend-service"></a><span data-ttu-id="497a1-359">Inoltrare servizio back-end toohello informazioni di contesto</span><span class="sxs-lookup"><span data-stu-id="497a1-359">Forward context information toohello backend service</span></span>  
 <span data-ttu-id="497a1-360">Questo esempio viene illustrato come il criterio tooapply hello API livello servizio back-end di toosupply contesto informazioni toohello.</span><span class="sxs-lookup"><span data-stu-id="497a1-360">This example shows how tooapply policy at hello API level toosupply context information toohello backend service.</span></span> <span data-ttu-id="497a1-361">Per una dimostrazione della configurazione e l'utilizzo di questo criterio, vedere [Cloud coprire episodio 177: più API le funzionalità di gestione con Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) e far avanzare rapidamente too10:30.</span><span class="sxs-lookup"><span data-stu-id="497a1-361">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too10:30.</span></span> <span data-ttu-id="497a1-362">12:10 è una dimostrazione di chiamata di un'operazione nel portale per sviluppatori hello in cui è possibile visualizzare i criteri di hello al lavoro.</span><span class="sxs-lookup"><span data-stu-id="497a1-362">At 12:10 there is a demo of calling an operation in hello developer portal where you can see hello policy at work.</span></span>  
  
```xml  
<!-- Copy this snippet into hello inbound element tooforward some context information, user id and hello region hello gateway is hosted in, toohello backend service for logging or evaluation -->  
<set-header name="x-request-context-data" exists-action="override">  
  <value>@(context.User.Id)</value>  
  <value>@(context.Deployment.Region)</value>  
</set-header>  
```  
  
 <span data-ttu-id="497a1-363">Per altre informazioni, vedere [Espressioni di criteri](api-management-policy-expressions.md) e [Variabile di contesto](api-management-policy-expressions.md#ContextVariables).</span><span class="sxs-lookup"><span data-stu-id="497a1-363">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="497a1-364">Elementi</span><span class="sxs-lookup"><span data-stu-id="497a1-364">Elements</span></span>  
  
|<span data-ttu-id="497a1-365">Nome</span><span class="sxs-lookup"><span data-stu-id="497a1-365">Name</span></span>|<span data-ttu-id="497a1-366">Descrizione</span><span class="sxs-lookup"><span data-stu-id="497a1-366">Description</span></span>|<span data-ttu-id="497a1-367">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="497a1-367">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="497a1-368">set-header</span><span class="sxs-lookup"><span data-stu-id="497a1-368">set-header</span></span>|<span data-ttu-id="497a1-369">Elemento radice.</span><span class="sxs-lookup"><span data-stu-id="497a1-369">Root element.</span></span>|<span data-ttu-id="497a1-370">Sì</span><span class="sxs-lookup"><span data-stu-id="497a1-370">Yes</span></span>|  
|<span data-ttu-id="497a1-371">value</span><span class="sxs-lookup"><span data-stu-id="497a1-371">value</span></span>|<span data-ttu-id="497a1-372">Specifica il valore di hello di hello intestazione toobe set.</span><span class="sxs-lookup"><span data-stu-id="497a1-372">Specifies hello value of hello header toobe set.</span></span> <span data-ttu-id="497a1-373">Per più intestazioni con hello omonima aggiungere ulteriori `value` elementi.</span><span class="sxs-lookup"><span data-stu-id="497a1-373">For multiple headers with hello same name add additional `value` elements.</span></span>|<span data-ttu-id="497a1-374">Sì</span><span class="sxs-lookup"><span data-stu-id="497a1-374">Yes</span></span>|  
  
### <a name="properties"></a><span data-ttu-id="497a1-375">Proprietà</span><span class="sxs-lookup"><span data-stu-id="497a1-375">Properties</span></span>  
  
|<span data-ttu-id="497a1-376">Nome</span><span class="sxs-lookup"><span data-stu-id="497a1-376">Name</span></span>|<span data-ttu-id="497a1-377">Descrizione</span><span class="sxs-lookup"><span data-stu-id="497a1-377">Description</span></span>|<span data-ttu-id="497a1-378">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="497a1-378">Required</span></span>|<span data-ttu-id="497a1-379">Default</span><span class="sxs-lookup"><span data-stu-id="497a1-379">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="497a1-380">exists-action</span><span class="sxs-lookup"><span data-stu-id="497a1-380">exists-action</span></span>|<span data-ttu-id="497a1-381">Specifica quali tootake azione quando l'intestazione hello è già specificato.</span><span class="sxs-lookup"><span data-stu-id="497a1-381">Specifies what action tootake when hello header is already specified.</span></span> <span data-ttu-id="497a1-382">Questo attributo deve avere uno dei seguenti valori hello.</span><span class="sxs-lookup"><span data-stu-id="497a1-382">This attribute must have one of hello following values.</span></span><br /><br /> <span data-ttu-id="497a1-383">-override - sostituisce hello valore dell'intestazione esistente hello.</span><span class="sxs-lookup"><span data-stu-id="497a1-383">-   override - replaces hello value of hello existing header.</span></span><br /><span data-ttu-id="497a1-384">-skip: non sostituisce il valore dell'intestazione esistente di hello.</span><span class="sxs-lookup"><span data-stu-id="497a1-384">-   skip - does not replace hello existing header value.</span></span><br /><span data-ttu-id="497a1-385">-aggiungere - aggiunge hello valore toohello valore dell'intestazione esistente.</span><span class="sxs-lookup"><span data-stu-id="497a1-385">-   append - appends hello value toohello existing header value.</span></span><br /><span data-ttu-id="497a1-386">-delete - rimuove l'intestazione di hello dalla richiesta hello.</span><span class="sxs-lookup"><span data-stu-id="497a1-386">-   delete - removes hello header from hello request.</span></span><br /><br /> <span data-ttu-id="497a1-387">Quando impostato troppo`override` l'integrazione di più voci con hello stesso nome risultati nell'intestazione di hello viene impostato in base tooall le voci (elencate più volte); solo i valori elencati verranno impostati nel risultato hello.</span><span class="sxs-lookup"><span data-stu-id="497a1-387">When set too`override` enlisting multiple entries with hello same name results in hello header being set according tooall entries (which will be listed multiple times); only listed values will be set in hello result.</span></span>|<span data-ttu-id="497a1-388">No</span><span class="sxs-lookup"><span data-stu-id="497a1-388">No</span></span>|<span data-ttu-id="497a1-389">override</span><span class="sxs-lookup"><span data-stu-id="497a1-389">override</span></span>|  
|<span data-ttu-id="497a1-390">name</span><span class="sxs-lookup"><span data-stu-id="497a1-390">name</span></span>|<span data-ttu-id="497a1-391">Specifica nome del set di toobe intestazione hello.</span><span class="sxs-lookup"><span data-stu-id="497a1-391">Specifies name of hello header toobe set.</span></span>|<span data-ttu-id="497a1-392">Sì</span><span class="sxs-lookup"><span data-stu-id="497a1-392">Yes</span></span>|<span data-ttu-id="497a1-393">N/D</span><span class="sxs-lookup"><span data-stu-id="497a1-393">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="497a1-394">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="497a1-394">Usage</span></span>  
 <span data-ttu-id="497a1-395">Questo criterio può essere utilizzato hello seguenti criteri [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="497a1-395">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="497a1-396">**Sezioni del criterio:** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="497a1-396">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="497a1-397">**Ambiti del criterio:** globale, prodotto, API, operazione</span><span class="sxs-lookup"><span data-stu-id="497a1-397">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="497a1-398"><a name="SetQueryStringParameter"></a> Imposta parametro di stringa della query</span><span class="sxs-lookup"><span data-stu-id="497a1-398"><a name="SetQueryStringParameter"></a> Set query string parameter</span></span>  
 <span data-ttu-id="497a1-399">Hello `set-query-parameter` criteri aggiunge valore sostituisce, o eliminazioni richiesta il parametro di stringa di query.</span><span class="sxs-lookup"><span data-stu-id="497a1-399">hello `set-query-parameter` policy adds, replaces value of, or deletes request query string parameter.</span></span> <span data-ttu-id="497a1-400">È possibile toopass utilizzati parametri di query previsti dal servizio back-end hello, che sono facoltativi o mai presentano nella richiesta di hello.</span><span class="sxs-lookup"><span data-stu-id="497a1-400">Can be used toopass query parameters expected by hello backend service which are optional or never present in hello request.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="497a1-401">Istruzione del criterio</span><span class="sxs-lookup"><span data-stu-id="497a1-401">Policy statement</span></span>  
  
```xml  
<set-query-parameter name="param name" exists-action="override | skip | append | delete">  
    <value>value</value> <!--for multiple parameters with hello same name add additional value elements-->  
</set-query-parameter>  
```  
  
### <a name="examples"></a><span data-ttu-id="497a1-402">Esempi</span><span class="sxs-lookup"><span data-stu-id="497a1-402">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="497a1-403">Esempio</span><span class="sxs-lookup"><span data-stu-id="497a1-403">Example</span></span>  
  
```xml  
  
<set-query-parameter>  
  <parameter name="api-key" exists-action="skip">  
    <value>12345678901</value>  
  </parameter>  
  <!-- for multiple parameters with hello same name add additional value elements -->  
</set-query-parameter>  
  
```  
  
#### <a name="forward-context-information-toohello-backend-service"></a><span data-ttu-id="497a1-404">Inoltrare servizio back-end toohello informazioni di contesto</span><span class="sxs-lookup"><span data-stu-id="497a1-404">Forward context information toohello backend service</span></span>  
 <span data-ttu-id="497a1-405">Questo esempio viene illustrato come il criterio tooapply hello API livello servizio back-end di toosupply contesto informazioni toohello.</span><span class="sxs-lookup"><span data-stu-id="497a1-405">This example shows how tooapply policy at hello API level toosupply context information toohello backend service.</span></span> <span data-ttu-id="497a1-406">Per una dimostrazione della configurazione e l'utilizzo di questo criterio, vedere [Cloud coprire episodio 177: più API le funzionalità di gestione con Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) e far avanzare rapidamente too10:30.</span><span class="sxs-lookup"><span data-stu-id="497a1-406">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too10:30.</span></span> <span data-ttu-id="497a1-407">12:10 è una dimostrazione di chiamata di un'operazione nel portale per sviluppatori hello in cui è possibile visualizzare i criteri di hello al lavoro.</span><span class="sxs-lookup"><span data-stu-id="497a1-407">At 12:10 there is a demo of calling an operation in hello developer portal where you can see hello policy at work.</span></span>  
  
```xml  
<!-- Copy this snippet into hello inbound element tooforward a piece of context, product name in this example, toohello backend service for logging or evaluation -->  
<set-query-parameter name="x-product-name" exists-action="override">  
  <value>@(context.Product.Name)</value>  
</set-query-parameter>  
  
```  
  
 <span data-ttu-id="497a1-408">Per altre informazioni, vedere [Espressioni di criteri](api-management-policy-expressions.md) e [Variabile di contesto](api-management-policy-expressions.md#ContextVariables).</span><span class="sxs-lookup"><span data-stu-id="497a1-408">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="497a1-409">Elementi</span><span class="sxs-lookup"><span data-stu-id="497a1-409">Elements</span></span>  
  
|<span data-ttu-id="497a1-410">Nome</span><span class="sxs-lookup"><span data-stu-id="497a1-410">Name</span></span>|<span data-ttu-id="497a1-411">Descrizione</span><span class="sxs-lookup"><span data-stu-id="497a1-411">Description</span></span>|<span data-ttu-id="497a1-412">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="497a1-412">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="497a1-413">set-query-parameter</span><span class="sxs-lookup"><span data-stu-id="497a1-413">set-query-parameter</span></span>|<span data-ttu-id="497a1-414">Elemento radice.</span><span class="sxs-lookup"><span data-stu-id="497a1-414">Root element.</span></span>|<span data-ttu-id="497a1-415">Sì</span><span class="sxs-lookup"><span data-stu-id="497a1-415">Yes</span></span>|  
|<span data-ttu-id="497a1-416">value</span><span class="sxs-lookup"><span data-stu-id="497a1-416">value</span></span>|<span data-ttu-id="497a1-417">Specifica il valore di hello di hello query parametro toobe set.</span><span class="sxs-lookup"><span data-stu-id="497a1-417">Specifies hello value of hello query parameter toobe set.</span></span> <span data-ttu-id="497a1-418">Per più parametri di query con hello omonima aggiungere ulteriori `value` elementi.</span><span class="sxs-lookup"><span data-stu-id="497a1-418">For multiple query parameters with hello same name add additional `value` elements.</span></span>|<span data-ttu-id="497a1-419">Sì</span><span class="sxs-lookup"><span data-stu-id="497a1-419">Yes</span></span>|  
  
### <a name="properties"></a><span data-ttu-id="497a1-420">Proprietà</span><span class="sxs-lookup"><span data-stu-id="497a1-420">Properties</span></span>  
  
|<span data-ttu-id="497a1-421">Nome</span><span class="sxs-lookup"><span data-stu-id="497a1-421">Name</span></span>|<span data-ttu-id="497a1-422">Descrizione</span><span class="sxs-lookup"><span data-stu-id="497a1-422">Description</span></span>|<span data-ttu-id="497a1-423">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="497a1-423">Required</span></span>|<span data-ttu-id="497a1-424">Default</span><span class="sxs-lookup"><span data-stu-id="497a1-424">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="497a1-425">exists-action</span><span class="sxs-lookup"><span data-stu-id="497a1-425">exists-action</span></span>|<span data-ttu-id="497a1-426">Specifica quali tootake azione quando il parametro di query hello è già specificato.</span><span class="sxs-lookup"><span data-stu-id="497a1-426">Specifies what action tootake when hello query parameter is already specified.</span></span> <span data-ttu-id="497a1-427">Questo attributo deve avere uno dei seguenti valori hello.</span><span class="sxs-lookup"><span data-stu-id="497a1-427">This attribute must have one of hello following values.</span></span><br /><br /> <span data-ttu-id="497a1-428">-override - sostituisce hello valore del parametro esistente hello.</span><span class="sxs-lookup"><span data-stu-id="497a1-428">-   override - replaces hello value of hello existing parameter.</span></span><br /><span data-ttu-id="497a1-429">-skip: non sostituisce il valore esistente query parametro hello.</span><span class="sxs-lookup"><span data-stu-id="497a1-429">-   skip - does not replace hello existing query parameter value.</span></span><br /><span data-ttu-id="497a1-430">-aggiungere - aggiunge hello valore toohello esistente valore del parametro query.</span><span class="sxs-lookup"><span data-stu-id="497a1-430">-   append - appends hello value toohello existing query parameter value.</span></span><br /><span data-ttu-id="497a1-431">-delete - rimuove il parametro di query hello dalla richiesta hello.</span><span class="sxs-lookup"><span data-stu-id="497a1-431">-   delete - removes hello query parameter from hello request.</span></span><br /><br /> <span data-ttu-id="497a1-432">Quando impostato troppo`override` l'integrazione di più voci con hello stesso nome dei risultati nel parametro di query hello viene impostato in base tooall le voci (elencate più volte); solo i valori elencati verranno impostati nel risultato hello.</span><span class="sxs-lookup"><span data-stu-id="497a1-432">When set too`override` enlisting multiple entries with hello same name results in hello query parameter being set according tooall entries (which will be listed multiple times); only listed values will be set in hello result.</span></span>|<span data-ttu-id="497a1-433">No</span><span class="sxs-lookup"><span data-stu-id="497a1-433">No</span></span>|<span data-ttu-id="497a1-434">override</span><span class="sxs-lookup"><span data-stu-id="497a1-434">override</span></span>|  
|<span data-ttu-id="497a1-435">name</span><span class="sxs-lookup"><span data-stu-id="497a1-435">name</span></span>|<span data-ttu-id="497a1-436">Specifica nome del set di toobe parametri query hello.</span><span class="sxs-lookup"><span data-stu-id="497a1-436">Specifies name of hello query parameter toobe set.</span></span>|<span data-ttu-id="497a1-437">Sì</span><span class="sxs-lookup"><span data-stu-id="497a1-437">Yes</span></span>|<span data-ttu-id="497a1-438">N/D</span><span class="sxs-lookup"><span data-stu-id="497a1-438">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="497a1-439">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="497a1-439">Usage</span></span>  
 <span data-ttu-id="497a1-440">Questo criterio può essere utilizzato hello seguenti criteri [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="497a1-440">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="497a1-441">**Sezioni del criterio:** inbound, backend</span><span class="sxs-lookup"><span data-stu-id="497a1-441">**Policy sections:** inbound, backend</span></span>  
  
-   <span data-ttu-id="497a1-442">**Ambiti del criterio:** globale, prodotto, API, operazione</span><span class="sxs-lookup"><span data-stu-id="497a1-442">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="497a1-443"><a name="RewriteURL"></a> Riscrivi URL</span><span class="sxs-lookup"><span data-stu-id="497a1-443"><a name="RewriteURL"></a> Rewrite URL</span></span>  
 <span data-ttu-id="497a1-444">Hello `rewrite-uri` criteri converte un URL di richiesta dal formato pubblico toohello formato previsto dal servizio web hello, come illustrato nell'esempio seguente hello.</span><span class="sxs-lookup"><span data-stu-id="497a1-444">hello `rewrite-uri` policy converts a request URL from its public form toohello form expected by hello web service, as shown in hello following example.</span></span>  
  
-   <span data-ttu-id="497a1-445">URL pubblico - `http://api.example.com/storenumber/ordernumber`</span><span class="sxs-lookup"><span data-stu-id="497a1-445">Public URL - `http://api.example.com/storenumber/ordernumber`</span></span>  
  
-   <span data-ttu-id="497a1-446">URL richiesta - `http://api.example.com/v2/US/hardware/storenumber&ordernumber?City&State`</span><span class="sxs-lookup"><span data-stu-id="497a1-446">Request URL - `http://api.example.com/v2/US/hardware/storenumber&ordernumber?City&State`</span></span>  
  
 <span data-ttu-id="497a1-447">Questo criterio può essere utilizzato quando un URL di risorse umane e/o orientato al browser deve essere trasformato in formato di URL hello previsto dal servizio web hello.</span><span class="sxs-lookup"><span data-stu-id="497a1-447">This policy can be used when a human and/or browser-friendly URL should be transformed into hello URL format expected by hello web service.</span></span> <span data-ttu-id="497a1-448">Questo criterio deve toobe applicato quando si espone un formato di URL alternativo, ad esempio gli URL, gli URL RESTful, gli URL descrittivi o gli URL SEO semplice che sono URL puramente strutturali che non contengono una stringa di query e invece contengono solo hello percorso di hello risorsa (dopo lo schema di hello e autorità hello).</span><span class="sxs-lookup"><span data-stu-id="497a1-448">This policy only needs toobe applied when exposing an alternative URL format, such as clean URLs, RESTful URLs, user-friendly URLs or SEO-friendly URLs that are purely structural URLs that do not contain a query string and instead contain only hello path of hello resource (after hello scheme and hello authority).</span></span> <span data-ttu-id="497a1-449">Sono spesso usati a fini estetici, di usabilità o di ottimizzazione dei motori di ricerca (SEO, Search Engine Optimization).</span><span class="sxs-lookup"><span data-stu-id="497a1-449">This is often done for aesthetic, usability, or search engine optimization (SEO) purposes.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="497a1-450">È possibile aggiungere solo i parametri di stringa di query mediante criteri di hello.</span><span class="sxs-lookup"><span data-stu-id="497a1-450">You can only add query string parameters using hello policy.</span></span> <span data-ttu-id="497a1-451">È possibile aggiungere parametri di percorso modello aggiuntivo in hello riscrive l'URL.</span><span class="sxs-lookup"><span data-stu-id="497a1-451">You cannot add extra template path parameters in hello rewrite URL.</span></span>  

### <a name="policy-statement"></a><span data-ttu-id="497a1-452">Istruzione del criterio</span><span class="sxs-lookup"><span data-stu-id="497a1-452">Policy statement</span></span>  
  
```xml  
<rewrite-uri template="uri template" copy-unmatched-params="true | false" />  
```  
  
### <a name="example"></a><span data-ttu-id="497a1-453">Esempio</span><span class="sxs-lookup"><span data-stu-id="497a1-453">Example</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <rewrite-uri template="/v2/US/hardware/{storenumber}&{ordernumber}?City=city&State=state" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
```xml
<!-- Assuming incoming request is /get?a=b&c=d and operation template is set too/get?a={b} -->
<policies>  
    <inbound>  
        <base />  
        <rewrite-uri template="/put" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
<!-- Resulting URL will be /put?c=d -->
```  
```xml
<!-- Assuming incoming request is /get?a=b&c=d and operation template is set too/get?a={b} -->
<policies>  
    <inbound>  
        <base />  
        <rewrite-uri template="/put" copy-unmatched-params="false" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
<!-- Resulting URL will be /put -->
```

### <a name="elements"></a><span data-ttu-id="497a1-454">Elementi</span><span class="sxs-lookup"><span data-stu-id="497a1-454">Elements</span></span>  
  
|<span data-ttu-id="497a1-455">Nome</span><span class="sxs-lookup"><span data-stu-id="497a1-455">Name</span></span>|<span data-ttu-id="497a1-456">Descrizione</span><span class="sxs-lookup"><span data-stu-id="497a1-456">Description</span></span>|<span data-ttu-id="497a1-457">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="497a1-457">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="497a1-458">rewrite-uri</span><span class="sxs-lookup"><span data-stu-id="497a1-458">rewrite-uri</span></span>|<span data-ttu-id="497a1-459">Elemento radice.</span><span class="sxs-lookup"><span data-stu-id="497a1-459">Root element.</span></span>|<span data-ttu-id="497a1-460">Sì</span><span class="sxs-lookup"><span data-stu-id="497a1-460">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="497a1-461">Attributi</span><span class="sxs-lookup"><span data-stu-id="497a1-461">Attributes</span></span>  
  
|<span data-ttu-id="497a1-462">Attributo</span><span class="sxs-lookup"><span data-stu-id="497a1-462">Attribute</span></span>|<span data-ttu-id="497a1-463">Descrizione</span><span class="sxs-lookup"><span data-stu-id="497a1-463">Description</span></span>|<span data-ttu-id="497a1-464">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="497a1-464">Required</span></span>|<span data-ttu-id="497a1-465">Default</span><span class="sxs-lookup"><span data-stu-id="497a1-465">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="497a1-466">template</span><span class="sxs-lookup"><span data-stu-id="497a1-466">template</span></span>|<span data-ttu-id="497a1-467">URL del servizio web effettivo Hello con i parametri di stringa di query.</span><span class="sxs-lookup"><span data-stu-id="497a1-467">hello actual web service URL with any query string parameters.</span></span> <span data-ttu-id="497a1-468">Quando si utilizzano espressioni, l'intero valore hello deve essere un'espressione.</span><span class="sxs-lookup"><span data-stu-id="497a1-468">When using expressions, hello whole value must be an expression.</span></span>|<span data-ttu-id="497a1-469">Sì</span><span class="sxs-lookup"><span data-stu-id="497a1-469">Yes</span></span>|<span data-ttu-id="497a1-470">N/D</span><span class="sxs-lookup"><span data-stu-id="497a1-470">N/A</span></span>|  
|<span data-ttu-id="497a1-471">copy-unmatched-params</span><span class="sxs-lookup"><span data-stu-id="497a1-471">copy-unmatched-params</span></span>|<span data-ttu-id="497a1-472">Specifica se i parametri di query nella richiesta in ingresso hello non presente nel modello di URL originale hello vengono aggiunti URL toohello definito da hello riscrivere modello</span><span class="sxs-lookup"><span data-stu-id="497a1-472">Specifies whether query parameters in hello incoming request not present in hello original URL template are added toohello URL defined by hello re-write template</span></span>|<span data-ttu-id="497a1-473">No</span><span class="sxs-lookup"><span data-stu-id="497a1-473">No</span></span>|<span data-ttu-id="497a1-474">true</span><span class="sxs-lookup"><span data-stu-id="497a1-474">true</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="497a1-475">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="497a1-475">Usage</span></span>  
 <span data-ttu-id="497a1-476">Questo criterio può essere utilizzato hello seguenti criteri [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="497a1-476">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="497a1-477">**Sezioni del criterio:** inbound</span><span class="sxs-lookup"><span data-stu-id="497a1-477">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="497a1-478">**Ambiti del criterio:** prodotto, API, operazione</span><span class="sxs-lookup"><span data-stu-id="497a1-478">**Policy scopes:** product, API, operation</span></span>  
  
##  <span data-ttu-id="497a1-479"><a name="XSLTransform"></a>Trasforma XML usando XSLT</span><span class="sxs-lookup"><span data-stu-id="497a1-479"><a name="XSLTransform"></a> Transform XML using an XSLT</span></span>  
 <span data-ttu-id="497a1-480">Hello `Transform XML using an XSLT` criterio si applica un tooXML trasformazione XSL nel corpo della richiesta o risposta hello.</span><span class="sxs-lookup"><span data-stu-id="497a1-480">hello `Transform XML using an XSLT` policy applies an XSL transformation tooXML in hello request or response body.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="497a1-481">Istruzione del criterio</span><span class="sxs-lookup"><span data-stu-id="497a1-481">Policy statement</span></span>  
  
```xml  
<xsl-transform>  
    <parameter name="User-Agent">@(context.Request.Headers.GetValueOrDefault("User-Agent","non-specified"))</parameter>  
    <xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">  
        <xsl:output method="xml" indent="yes" />  
        <xsl:param name="User-Agent" />  
        <xsl:template match="* | @* | node()">  
            <xsl:copy>  
                <xsl:if test="self::* and not(parent::*)">  
                    <xsl:attribute name="User-Agent">  
                        <xsl:value-of select="$User-Agent" />  
                    </xsl:attribute>  
                </xsl:if>  
                <xsl:apply-templates select="* | @* | node()" />  
            </xsl:copy>  
        </xsl:template>  
    </xsl:stylesheet>  
  </xsl-transform>  
```  
  
### <a name="example"></a><span data-ttu-id="497a1-482">Esempio</span><span class="sxs-lookup"><span data-stu-id="497a1-482">Example</span></span>  
  
```xml  
<policies>  
  <inbound>  
      <base />  
  </inbound>  
  <outbound>  
      <base />  
      <xsl-transform>  
        <xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">  
            <xsl:output omit-xml-declaration="yes" method="xml" indent="yes" />  
            <!-- Copy all nodes directly-->  
            <xsl:template match="node()| @*|*">  
                <xsl:copy>  
                    <xsl:apply-templates select="@* | node()|*" />  
                </xsl:copy>  
            </xsl:template>  
        </xsl:stylesheet>  
    </xsl-transform>  
  </outbound>  
</policies>  
```  
  
### <a name="elements"></a><span data-ttu-id="497a1-483">Elementi</span><span class="sxs-lookup"><span data-stu-id="497a1-483">Elements</span></span>  
  
|<span data-ttu-id="497a1-484">Nome</span><span class="sxs-lookup"><span data-stu-id="497a1-484">Name</span></span>|<span data-ttu-id="497a1-485">Descrizione</span><span class="sxs-lookup"><span data-stu-id="497a1-485">Description</span></span>|<span data-ttu-id="497a1-486">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="497a1-486">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="497a1-487">xsl-transform</span><span class="sxs-lookup"><span data-stu-id="497a1-487">xsl-transform</span></span>|<span data-ttu-id="497a1-488">Elemento radice.</span><span class="sxs-lookup"><span data-stu-id="497a1-488">Root element.</span></span>|<span data-ttu-id="497a1-489">Sì</span><span class="sxs-lookup"><span data-stu-id="497a1-489">Yes</span></span>|  
|<span data-ttu-id="497a1-490">parametro</span><span class="sxs-lookup"><span data-stu-id="497a1-490">parameter</span></span>|<span data-ttu-id="497a1-491">Variabili toodefine utilizzati utilizzate nella trasformazione hello</span><span class="sxs-lookup"><span data-stu-id="497a1-491">Used toodefine variables used in hello transform</span></span>|<span data-ttu-id="497a1-492">No</span><span class="sxs-lookup"><span data-stu-id="497a1-492">No</span></span>|  
|<span data-ttu-id="497a1-493">xsl:stylesheet</span><span class="sxs-lookup"><span data-stu-id="497a1-493">xsl:stylesheet</span></span>|<span data-ttu-id="497a1-494">Elemento del foglio di stile principale.</span><span class="sxs-lookup"><span data-stu-id="497a1-494">Root stylesheet element.</span></span> <span data-ttu-id="497a1-495">Tutti gli elementi e attributi definiti all'interno di seguono standard hello [specifica XSLT](http://www.w3.org/TR/xslt)</span><span class="sxs-lookup"><span data-stu-id="497a1-495">All elements and attributes defined within follow hello standard [XSLT specification](http://www.w3.org/TR/xslt)</span></span>|<span data-ttu-id="497a1-496">Sì</span><span class="sxs-lookup"><span data-stu-id="497a1-496">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="497a1-497">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="497a1-497">Usage</span></span>  
 <span data-ttu-id="497a1-498">Questo criterio può essere utilizzato hello seguenti criteri [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="497a1-498">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="497a1-499">**Sezioni del criterio:** inbound, outbound</span><span class="sxs-lookup"><span data-stu-id="497a1-499">**Policy sections:** inbound, outbound</span></span>  
  
-   <span data-ttu-id="497a1-500">**Ambiti del criterio:** globale, prodotto, API, operazione</span><span class="sxs-lookup"><span data-stu-id="497a1-500">**Policy scopes:** global, product, API, operation</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="497a1-501">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="497a1-501">Next steps</span></span>
<span data-ttu-id="497a1-502">Per altre informazioni sull'uso dei criteri, vedere [Criteri di Gestione API](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="497a1-502">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  
