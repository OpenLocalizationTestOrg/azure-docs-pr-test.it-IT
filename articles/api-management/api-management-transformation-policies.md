---
title: Criteri di trasformazione di Gestione API di Azure | Documentazione Microsoft
description: Informazioni sui criteri di trasformazione disponibili in Gestione API di Azure.
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
ms.openlocfilehash: c2bed904b82c569b28a6e00d0cc9b49107c148dd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="api-management-transformation-policies"></a><span data-ttu-id="8b3a2-103">Criteri di trasformazione di Gestione API</span><span class="sxs-lookup"><span data-stu-id="8b3a2-103">API Management transformation policies</span></span>
<span data-ttu-id="8b3a2-104">Questo argomento fornisce un riferimento per i criteri di Gestione API seguenti.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-104">This topic provides a reference for the following API Management policies.</span></span> <span data-ttu-id="8b3a2-105">Per informazioni sull'aggiunta e sulla configurazione dei criteri, vedere [Criteri di Gestione API](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="8b3a2-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="8b3a2-106"><a name="TransformationPolicies"></a> Criteri di trasformazione</span><span class="sxs-lookup"><span data-stu-id="8b3a2-106"><a name="TransformationPolicies"></a> Transformation policies</span></span>  
  
-   <span data-ttu-id="8b3a2-107">[json-to-xml](api-management-transformation-policies.md#ConvertJSONtoXML) : converte il corpo della richiesta o della risposta da JSON a XML.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-107">[Convert JSON to XML](api-management-transformation-policies.md#ConvertJSONtoXML) - Converts request or response body from JSON to XML.</span></span>  
  
-   <span data-ttu-id="8b3a2-108">[xml-to-json](api-management-transformation-policies.md#ConvertXMLtoJSON) : converte il corpo della richiesta o della risposta da XML a JSON.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-108">[Convert XML to JSON](api-management-transformation-policies.md#ConvertXMLtoJSON) - Converts request or response body from XML to JSON.</span></span>  
  
-   <span data-ttu-id="8b3a2-109">[find-and-replace](api-management-transformation-policies.md#Findandreplacestringinbody) : trova una sottostringa di richiesta o risposta e la sostituisce con una sottostringa diversa.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-109">[Find and replace string in body](api-management-transformation-policies.md#Findandreplacestringinbody) - Finds a request or response substring and replaces it with a different substring.</span></span>  
  
-   <span data-ttu-id="8b3a2-110">[Maschera URL nel contenuto](api-management-transformation-policies.md#MaskURLSContent) : riscrive (maschera) i collegamenti nel corpo della risposta, in modo che facciano riferimento al collegamento equivalente tramite il gateway.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-110">[Mask URLs in content](api-management-transformation-policies.md#MaskURLSContent) - Re-writes (masks) links in the response body so that they point to the equivalent link via the gateway.</span></span>  
  
-   <span data-ttu-id="8b3a2-111">[set-backend-service](api-management-transformation-policies.md#SetBackendService) : consente di cambiare il servizio back-end per una richiesta in ingresso.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-111">[Set backend service](api-management-transformation-policies.md#SetBackendService) - Changes the backend service for an incoming request.</span></span>  
  
-   <span data-ttu-id="8b3a2-112">[set-body](api-management-transformation-policies.md#SetBody) : consente di impostare il corpo del messaggio per richieste in ingresso e in uscita.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-112">[Set body](api-management-transformation-policies.md#SetBody) - Sets the message body for incoming and outgoing requests.</span></span>  
  
-   <span data-ttu-id="8b3a2-113">[Imposta intestazione HTTP](api-management-transformation-policies.md#SetHTTPheader) : assegna un valore a una intestazione di risposta e/o di richiesta esistente oppure aggiunge una nuova intestazione di risposta e/o di richiesta.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-113">[Set HTTP header](api-management-transformation-policies.md#SetHTTPheader) - Assigns a value to an existing response and/or request header or adds a new response and/or request header.</span></span>  
  
-   <span data-ttu-id="8b3a2-114">[Imposta parametro di stringa della query](api-management-transformation-policies.md#SetQueryStringParameter) : aggiunge, sostituisce il valore di o elimina il parametro di stringa della query di richiesta.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-114">[Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) - Adds, replaces value of, or deletes request query string parameter.</span></span>  
  
-   <span data-ttu-id="8b3a2-115">[rewrite-uri](api-management-transformation-policies.md#RewriteURL) : converte un URL di richiesta dal formato pubblico al formato previsto dal servizio Web.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-115">[Rewrite URL](api-management-transformation-policies.md#RewriteURL) - Converts a request URL from its public form to the form expected by the web service.</span></span>  
  
-   <span data-ttu-id="8b3a2-116">[Trasforma XML usando una trasformazione XSLT](api-management-transformation-policies.md#XSLTransform) - applica una trasformazione da XSL a XML nel corpo della richiesta o della risposta.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-116">[Transform XML using an XSLT](api-management-transformation-policies.md#XSLTransform) - Applies an XSL transformation to XML in the request or response body.</span></span>  
  
##  <span data-ttu-id="8b3a2-117"><a name="ConvertJSONtoXML"></a> Converti JSON in XML</span><span class="sxs-lookup"><span data-stu-id="8b3a2-117"><a name="ConvertJSONtoXML"></a> Convert JSON to XML</span></span>  
 <span data-ttu-id="8b3a2-118">Il criterio `json-to-xml` converte il corpo della richiesta o della risposta da JSON a XML.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-118">The `json-to-xml` policy converts a request or response body from JSON to XML.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="8b3a2-119">Istruzione del criterio</span><span class="sxs-lookup"><span data-stu-id="8b3a2-119">Policy statement</span></span>  
  
```xml  
<json-to-xml apply="always | content-type-json" consider-accept-header="true | false"/>  
```  
  
### <a name="example"></a><span data-ttu-id="8b3a2-120">Esempio</span><span class="sxs-lookup"><span data-stu-id="8b3a2-120">Example</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="8b3a2-121">Elementi</span><span class="sxs-lookup"><span data-stu-id="8b3a2-121">Elements</span></span>  
  
|<span data-ttu-id="8b3a2-122">Nome</span><span class="sxs-lookup"><span data-stu-id="8b3a2-122">Name</span></span>|<span data-ttu-id="8b3a2-123">Descrizione</span><span class="sxs-lookup"><span data-stu-id="8b3a2-123">Description</span></span>|<span data-ttu-id="8b3a2-124">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="8b3a2-124">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="8b3a2-125">json-to-xml</span><span class="sxs-lookup"><span data-stu-id="8b3a2-125">json-to-xml</span></span>|<span data-ttu-id="8b3a2-126">Elemento radice.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-126">Root element.</span></span>|<span data-ttu-id="8b3a2-127">Sì</span><span class="sxs-lookup"><span data-stu-id="8b3a2-127">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="8b3a2-128">Attributi</span><span class="sxs-lookup"><span data-stu-id="8b3a2-128">Attributes</span></span>  
  
|<span data-ttu-id="8b3a2-129">Nome</span><span class="sxs-lookup"><span data-stu-id="8b3a2-129">Name</span></span>|<span data-ttu-id="8b3a2-130">Descrizione</span><span class="sxs-lookup"><span data-stu-id="8b3a2-130">Description</span></span>|<span data-ttu-id="8b3a2-131">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="8b3a2-131">Required</span></span>|<span data-ttu-id="8b3a2-132">Default</span><span class="sxs-lookup"><span data-stu-id="8b3a2-132">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="8b3a2-133">apply</span><span class="sxs-lookup"><span data-stu-id="8b3a2-133">apply</span></span>|<span data-ttu-id="8b3a2-134">Questo attributo deve essere impostato su uno dei valori seguenti.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-134">The attribute must be set to one of the following values.</span></span><br /><br /> <span data-ttu-id="8b3a2-135">-   always - applica sempre la conversione.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-135">-   always - always apply conversion.</span></span><br /><span data-ttu-id="8b3a2-136">-   content-type-json - applica la conversione solo se l'intestazione Content-Type della risposta indica la presenza di JSON.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-136">-   content-type-json - convert only if response Content-Type header indicates presence of JSON.</span></span>|<span data-ttu-id="8b3a2-137">Sì</span><span class="sxs-lookup"><span data-stu-id="8b3a2-137">Yes</span></span>|<span data-ttu-id="8b3a2-138">N/D</span><span class="sxs-lookup"><span data-stu-id="8b3a2-138">N/A</span></span>|  
|<span data-ttu-id="8b3a2-139">consider-accept-header</span><span class="sxs-lookup"><span data-stu-id="8b3a2-139">consider-accept-header</span></span>|<span data-ttu-id="8b3a2-140">Questo attributo deve essere impostato su uno dei valori seguenti.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-140">The attribute must be set to one of the following values.</span></span><br /><br /> <span data-ttu-id="8b3a2-141">-   true - applica la conversione se JSON è richiesto nell'intestazione Accept della richiesta.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-141">-   true - apply conversion if JSON is requested in request Accept header.</span></span><br /><span data-ttu-id="8b3a2-142">-   false - applica sempre la conversione.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-142">-   false -always apply conversion.</span></span>|<span data-ttu-id="8b3a2-143">No</span><span class="sxs-lookup"><span data-stu-id="8b3a2-143">No</span></span>|<span data-ttu-id="8b3a2-144">true</span><span class="sxs-lookup"><span data-stu-id="8b3a2-144">true</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="8b3a2-145">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="8b3a2-145">Usage</span></span>  
 <span data-ttu-id="8b3a2-146">Questo criterio può essere usato nelle [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e negli [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) del criterio seguenti.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-146">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="8b3a2-147">**Sezioni del criterio:** inbound, outbound, on-error</span><span class="sxs-lookup"><span data-stu-id="8b3a2-147">**Policy sections:** inbound, outbound, on-error</span></span>  
  
-   <span data-ttu-id="8b3a2-148">**Ambiti del criterio:** globale, prodotto, API, operazione</span><span class="sxs-lookup"><span data-stu-id="8b3a2-148">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="8b3a2-149"><a name="ConvertXMLtoJSON"></a> Converti XML in JSON</span><span class="sxs-lookup"><span data-stu-id="8b3a2-149"><a name="ConvertXMLtoJSON"></a> Convert XML to JSON</span></span>  
 <span data-ttu-id="8b3a2-150">Il criterio `xml-to-json` converte il corpo della richiesta o della risposta da XML a JSON.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-150">The `xml-to-json` policy converts a request or response body from XML to JSON.</span></span> <span data-ttu-id="8b3a2-151">Il criterio può essere applicato per modernizzare le API basate su servizi Web back-end solo di tipo XML.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-151">This policy can be used to modernize APIs based on XML-only backend web services.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="8b3a2-152">Istruzione del criterio</span><span class="sxs-lookup"><span data-stu-id="8b3a2-152">Policy statement</span></span>  
  
```xml  
<xml-to-json kind="javascript-friendly | direct" apply="always | content-type-xml" consider-accept-header="true | false"/>  
```  
  
### <a name="example"></a><span data-ttu-id="8b3a2-153">Esempio</span><span class="sxs-lookup"><span data-stu-id="8b3a2-153">Example</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="8b3a2-154">Elementi</span><span class="sxs-lookup"><span data-stu-id="8b3a2-154">Elements</span></span>  
  
|<span data-ttu-id="8b3a2-155">Nome</span><span class="sxs-lookup"><span data-stu-id="8b3a2-155">Name</span></span>|<span data-ttu-id="8b3a2-156">Descrizione</span><span class="sxs-lookup"><span data-stu-id="8b3a2-156">Description</span></span>|<span data-ttu-id="8b3a2-157">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="8b3a2-157">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="8b3a2-158">xml-to-json</span><span class="sxs-lookup"><span data-stu-id="8b3a2-158">xml-to-json</span></span>|<span data-ttu-id="8b3a2-159">Elemento radice.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-159">Root element.</span></span>|<span data-ttu-id="8b3a2-160">Sì</span><span class="sxs-lookup"><span data-stu-id="8b3a2-160">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="8b3a2-161">Attributi</span><span class="sxs-lookup"><span data-stu-id="8b3a2-161">Attributes</span></span>  
  
|<span data-ttu-id="8b3a2-162">Nome</span><span class="sxs-lookup"><span data-stu-id="8b3a2-162">Name</span></span>|<span data-ttu-id="8b3a2-163">Descrizione</span><span class="sxs-lookup"><span data-stu-id="8b3a2-163">Description</span></span>|<span data-ttu-id="8b3a2-164">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="8b3a2-164">Required</span></span>|<span data-ttu-id="8b3a2-165">Default</span><span class="sxs-lookup"><span data-stu-id="8b3a2-165">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="8b3a2-166">kind</span><span class="sxs-lookup"><span data-stu-id="8b3a2-166">kind</span></span>|<span data-ttu-id="8b3a2-167">Questo attributo deve essere impostato su uno dei valori seguenti.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-167">The attribute must be set to one of the following values.</span></span><br /><br /> <span data-ttu-id="8b3a2-168">-   javascript-friendly - il JSON convertito ha un formato intuitivo per gli sviluppatori JavaScript.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-168">-   javascript-friendly - the converted JSON has a form friendly to JavaScript developers.</span></span><br /><span data-ttu-id="8b3a2-169">-   direct - il JSON convertito riflette la struttura del documento XML originario.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-169">-   direct - the converted JSON reflects the original XML document's structure.</span></span>|<span data-ttu-id="8b3a2-170">Sì</span><span class="sxs-lookup"><span data-stu-id="8b3a2-170">Yes</span></span>|<span data-ttu-id="8b3a2-171">N/D</span><span class="sxs-lookup"><span data-stu-id="8b3a2-171">N/A</span></span>|  
|<span data-ttu-id="8b3a2-172">apply</span><span class="sxs-lookup"><span data-stu-id="8b3a2-172">apply</span></span>|<span data-ttu-id="8b3a2-173">Questo attributo deve essere impostato su uno dei valori seguenti.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-173">The attribute must be set to one of the following values.</span></span><br /><br /> <span data-ttu-id="8b3a2-174">-   always - esegue sempre la conversione.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-174">-   always - convert always.</span></span><br /><span data-ttu-id="8b3a2-175">-   content-type-xml - applica la conversione solo se l'intestazione Content-Type della risposta indica la presenza di XML.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-175">-   content-type-xml - convert only if response Content-Type header indicates presence of XML.</span></span>|<span data-ttu-id="8b3a2-176">Sì</span><span class="sxs-lookup"><span data-stu-id="8b3a2-176">Yes</span></span>|<span data-ttu-id="8b3a2-177">N/D</span><span class="sxs-lookup"><span data-stu-id="8b3a2-177">N/A</span></span>|  
|<span data-ttu-id="8b3a2-178">consider-accept-header</span><span class="sxs-lookup"><span data-stu-id="8b3a2-178">consider-accept-header</span></span>|<span data-ttu-id="8b3a2-179">Questo attributo deve essere impostato su uno dei valori seguenti.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-179">The attribute must be set to one of the following values.</span></span><br /><br /> <span data-ttu-id="8b3a2-180">-   true - applica la conversione se XML è richiesto nell'intestazione Accept della richiesta.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-180">-   true - apply conversion if XML is requested in request Accept header.</span></span><br /><span data-ttu-id="8b3a2-181">-   false - applica sempre la conversione.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-181">-   false -always apply conversion.</span></span>|<span data-ttu-id="8b3a2-182">No</span><span class="sxs-lookup"><span data-stu-id="8b3a2-182">No</span></span>|<span data-ttu-id="8b3a2-183">true</span><span class="sxs-lookup"><span data-stu-id="8b3a2-183">true</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="8b3a2-184">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="8b3a2-184">Usage</span></span>  
 <span data-ttu-id="8b3a2-185">Questo criterio può essere usato nelle [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e negli [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) del criterio seguenti.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-185">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="8b3a2-186">**Sezioni del criterio:** inbound, outbound, on-error</span><span class="sxs-lookup"><span data-stu-id="8b3a2-186">**Policy sections:** inbound, outbound, on-error</span></span>  
  
-   <span data-ttu-id="8b3a2-187">**Ambiti del criterio:** globale, prodotto, API, operazione</span><span class="sxs-lookup"><span data-stu-id="8b3a2-187">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="8b3a2-188"><a name="Findandreplacestringinbody"></a> Trova e sostituisci stringa nel corpo</span><span class="sxs-lookup"><span data-stu-id="8b3a2-188"><a name="Findandreplacestringinbody"></a> Find and replace string in body</span></span>  
 <span data-ttu-id="8b3a2-189">Il criterio `find-and-replace` trova una sottostringa di richiesta o risposta e la sostituisce con una sottostringa diversa.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-189">The `find-and-replace` policy finds a request or response substring and replaces it with a different substring.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="8b3a2-190">Istruzione del criterio</span><span class="sxs-lookup"><span data-stu-id="8b3a2-190">Policy statement</span></span>  
  
```xml  
<find-and-replace from="what to replace" to="replacement" />  
```  
  
### <a name="example"></a><span data-ttu-id="8b3a2-191">Esempio</span><span class="sxs-lookup"><span data-stu-id="8b3a2-191">Example</span></span>  
  
```xml  
<find-and-replace from="notebook" to="laptop" />  
```  
  
### <a name="elements"></a><span data-ttu-id="8b3a2-192">Elementi</span><span class="sxs-lookup"><span data-stu-id="8b3a2-192">Elements</span></span>  
  
|<span data-ttu-id="8b3a2-193">Nome</span><span class="sxs-lookup"><span data-stu-id="8b3a2-193">Name</span></span>|<span data-ttu-id="8b3a2-194">Descrizione</span><span class="sxs-lookup"><span data-stu-id="8b3a2-194">Description</span></span>|<span data-ttu-id="8b3a2-195">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="8b3a2-195">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="8b3a2-196">find-and-replace</span><span class="sxs-lookup"><span data-stu-id="8b3a2-196">find-and-replace</span></span>|<span data-ttu-id="8b3a2-197">Elemento radice.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-197">Root element.</span></span>|<span data-ttu-id="8b3a2-198">Sì</span><span class="sxs-lookup"><span data-stu-id="8b3a2-198">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="8b3a2-199">Attributi</span><span class="sxs-lookup"><span data-stu-id="8b3a2-199">Attributes</span></span>  
  
|<span data-ttu-id="8b3a2-200">Nome</span><span class="sxs-lookup"><span data-stu-id="8b3a2-200">Name</span></span>|<span data-ttu-id="8b3a2-201">Descrizione</span><span class="sxs-lookup"><span data-stu-id="8b3a2-201">Description</span></span>|<span data-ttu-id="8b3a2-202">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="8b3a2-202">Required</span></span>|<span data-ttu-id="8b3a2-203">Default</span><span class="sxs-lookup"><span data-stu-id="8b3a2-203">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="8b3a2-204">from</span><span class="sxs-lookup"><span data-stu-id="8b3a2-204">from</span></span>|<span data-ttu-id="8b3a2-205">Stringa da cercare.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-205">The string to search for.</span></span>|<span data-ttu-id="8b3a2-206">Sì</span><span class="sxs-lookup"><span data-stu-id="8b3a2-206">Yes</span></span>|<span data-ttu-id="8b3a2-207">N/D</span><span class="sxs-lookup"><span data-stu-id="8b3a2-207">N/A</span></span>|  
|<span data-ttu-id="8b3a2-208">to</span><span class="sxs-lookup"><span data-stu-id="8b3a2-208">to</span></span>|<span data-ttu-id="8b3a2-209">La stringa di sostituzione.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-209">The replacement string.</span></span> <span data-ttu-id="8b3a2-210">Specificare una stringa di sostituzione con lunghezza zero per rimuovere la stringa di ricerca.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-210">Specify a zero length replacement string to remove the search string.</span></span>|<span data-ttu-id="8b3a2-211">Sì</span><span class="sxs-lookup"><span data-stu-id="8b3a2-211">Yes</span></span>|<span data-ttu-id="8b3a2-212">N/D</span><span class="sxs-lookup"><span data-stu-id="8b3a2-212">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="8b3a2-213">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="8b3a2-213">Usage</span></span>  
 <span data-ttu-id="8b3a2-214">Questo criterio può essere usato nelle [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e negli [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) del criterio seguenti.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-214">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="8b3a2-215">**Sezioni del criterio:**in ingresso, in uscita, back-end, on-error</span><span class="sxs-lookup"><span data-stu-id="8b3a2-215">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="8b3a2-216">**Ambiti del criterio:** globale, prodotto, API, operazione</span><span class="sxs-lookup"><span data-stu-id="8b3a2-216">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="8b3a2-217"><a name="MaskURLSContent"></a> Maschera URL nel contenuto</span><span class="sxs-lookup"><span data-stu-id="8b3a2-217"><a name="MaskURLSContent"></a> Mask URLs in content</span></span>  
 <span data-ttu-id="8b3a2-218">Il criterio `redirect-content-urls` riscrive (maschera) i collegamenti nel corpo della risposta, in modo che facciano riferimento al collegamento equivalente tramite il gateway.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-218">The `redirect-content-urls` policy re-writes (masks) links in the response body so that they point to the equivalent link via the gateway.</span></span> <span data-ttu-id="8b3a2-219">Usare la sezione outbound per riscrivere i collegamenti al corpo della risposta affinché facciano riferimento al gateway.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-219">Use in the outbound section to re-write response body links to make them point to the gateway.</span></span> <span data-ttu-id="8b3a2-220">Usare la sezione inbound per ottenere l'effetto opposto.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-220">Use in the inbound section for an opposite effect.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="8b3a2-221">Questo criterio non modifica i valori delle intestazioni, ad esempio le intestazioni `Location`.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-221">This policy does not change any header values such as `Location` headers.</span></span> <span data-ttu-id="8b3a2-222">Per modificare i valori delle intestazioni, usare il criterio [set-header](api-management-transformation-policies.md#SetHTTPheader).</span><span class="sxs-lookup"><span data-stu-id="8b3a2-222">To change header values, use the [set-header](api-management-transformation-policies.md#SetHTTPheader) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="8b3a2-223">Istruzione del criterio</span><span class="sxs-lookup"><span data-stu-id="8b3a2-223">Policy statement</span></span>  
  
```xml  
<redirect-content-urls />  
```  
  
### <a name="example"></a><span data-ttu-id="8b3a2-224">Esempio</span><span class="sxs-lookup"><span data-stu-id="8b3a2-224">Example</span></span>  
  
```xml  
<redirect-content-urls />  
```  
  
### <a name="elements"></a><span data-ttu-id="8b3a2-225">Elementi</span><span class="sxs-lookup"><span data-stu-id="8b3a2-225">Elements</span></span>  
  
|<span data-ttu-id="8b3a2-226">Nome</span><span class="sxs-lookup"><span data-stu-id="8b3a2-226">Name</span></span>|<span data-ttu-id="8b3a2-227">Descrizione</span><span class="sxs-lookup"><span data-stu-id="8b3a2-227">Description</span></span>|<span data-ttu-id="8b3a2-228">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="8b3a2-228">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="8b3a2-229">redirect-content-urls</span><span class="sxs-lookup"><span data-stu-id="8b3a2-229">redirect-content-urls</span></span>|<span data-ttu-id="8b3a2-230">Elemento radice.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-230">Root element.</span></span>|<span data-ttu-id="8b3a2-231">Sì</span><span class="sxs-lookup"><span data-stu-id="8b3a2-231">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="8b3a2-232">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="8b3a2-232">Usage</span></span>  
 <span data-ttu-id="8b3a2-233">Questo criterio può essere usato nelle [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e negli [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) del criterio seguenti.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-233">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="8b3a2-234">**Sezioni del criterio:** inbound, outbound</span><span class="sxs-lookup"><span data-stu-id="8b3a2-234">**Policy sections:** inbound, outbound</span></span>  
  
-   <span data-ttu-id="8b3a2-235">**Ambiti del criterio:** globale, prodotto, API, operazione</span><span class="sxs-lookup"><span data-stu-id="8b3a2-235">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="8b3a2-236"><a name="SetBackendService"></a> Imposta servizio back-end</span><span class="sxs-lookup"><span data-stu-id="8b3a2-236"><a name="SetBackendService"></a> Set backend service</span></span>  
 <span data-ttu-id="8b3a2-237">Usare il criterio `set-backend-service` per reindirizzare una richiesta in ingresso a un back-end diverso da quello specificato nelle impostazioni dell'API per l'operazione.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-237">Use the `set-backend-service` policy to redirect an incoming request to a different backend than the one specified in the API settings for that operation.</span></span> <span data-ttu-id="8b3a2-238">Questo criterio cambia l'URL di base del servizio back-end della richiesta in arrivo con quello specificato nel criterio.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-238">This policy changes the backend service base URL of the incoming request to the one specified in the policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="8b3a2-239">Istruzione del criterio</span><span class="sxs-lookup"><span data-stu-id="8b3a2-239">Policy statement</span></span>  
  
```xml  
<set-backend-service base-url="base URL of the backend service" />  
```  
  
### <a name="example"></a><span data-ttu-id="8b3a2-240">Esempio</span><span class="sxs-lookup"><span data-stu-id="8b3a2-240">Example</span></span>  
  
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
<span data-ttu-id="8b3a2-241">In questo esempio il criterio del servizio back-end indirizza le richieste in base al valore di versione passato nella stringa di query a un servizio back-end diverso rispetto a quello specificato nell'API.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-241">In this example the set backend service policy routes requests based on the version value passed in the query string to a different backend service than the one specified in the API.</span></span>
  
<span data-ttu-id="8b3a2-242">Inizialmente l'URL di base del servizio back-end è quello specificato nelle impostazioni dell'API.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-242">Initially the backend service base URL is derived from the API settings.</span></span> <span data-ttu-id="8b3a2-243">Pertanto, l'URL della richiesta `https://contoso.azure-api.net/api/partners/15?version=2013-05&subscription-key=abcdef` diventa `http://contoso.com/api/10.4/partners/15?version=2013-05&subscription-key=abcdef` dove `http://contoso.com/api/10.4/` è l'URL del servizio back-end specificato nelle impostazioni dell'API.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-243">So the request URL `https://contoso.azure-api.net/api/partners/15?version=2013-05&subscription-key=abcdef` becomes `http://contoso.com/api/10.4/partners/15?version=2013-05&subscription-key=abcdef` where `http://contoso.com/api/10.4/` is the backend service URL specified in the API settings.</span></span>  
  
<span data-ttu-id="8b3a2-244">Quando viene applicata l'istruzione del criterio [<choose\>](api-management-advanced-policies.md#choose), l'URL di base del servizio back-end può essere di nuovo modificato in `http://contoso.com/api/8.2` o `http://contoso.com/api/9.1`, a seconda del valore del parametro della query versione richiesta.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-244">When the [<choose\>](api-management-advanced-policies.md#choose) policy statement is applied the backend service base URL may change again either to `http://contoso.com/api/8.2` or `http://contoso.com/api/9.1`, depending on the value of the version request query parameter.</span></span> <span data-ttu-id="8b3a2-245">Se, ad esempio, il valore è `"2013-15"`, l'URL della richiesta finale sarà `http://contoso.com/api/8.2/partners/15?version=2013-05&subscription-key=abcdef`.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-245">For example, if the value is `"2013-15"` the final request URL becomes `http://contoso.com/api/8.2/partners/15?version=2013-05&subscription-key=abcdef`.</span></span>  
  
<span data-ttu-id="8b3a2-246">Se occorre un'ulteriore trasformazione della richiesta, è possibile usare altri [criteri di trasformazione](api-management-transformation-policies.md#TransformationPolicies).</span><span class="sxs-lookup"><span data-stu-id="8b3a2-246">If further transformation of the request is desired, other [Transformation policies](api-management-transformation-policies.md#TransformationPolicies) can be used.</span></span> <span data-ttu-id="8b3a2-247">Ad esempio, per rimuovere il parametro della query di versione una volta instradata la richiesta verso un back-end specifico, ad esempio, è possibile usare il criterio [Imposta parametro della stringa di query](api-management-transformation-policies.md#SetQueryStringParameter) per rimuovere l'attributo della versione divenuta ridondante.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-247">For example, to remove the version query parameter now that the request is being routed to a version specific backend, the  [Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) policy can be used to remove the now redundant version attribute.</span></span>  
  
### <a name="example"></a><span data-ttu-id="8b3a2-248">Esempio</span><span class="sxs-lookup"><span data-stu-id="8b3a2-248">Example</span></span>  
  
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
<span data-ttu-id="8b3a2-249">In questo esempio il criterio indirizza la richiesta a un back-end dell'infrastruttura del servizio tramite la stringa di query dell'ID utente come chiave di partizione e tramite la replica della partizione primaria.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-249">In this example the policy routes the request to a service fabric backend, using the userId query string as the partition key and using the primary replica of the partition.</span></span>  

### <a name="elements"></a><span data-ttu-id="8b3a2-250">Elementi</span><span class="sxs-lookup"><span data-stu-id="8b3a2-250">Elements</span></span>  
  
|<span data-ttu-id="8b3a2-251">Nome</span><span class="sxs-lookup"><span data-stu-id="8b3a2-251">Name</span></span>|<span data-ttu-id="8b3a2-252">Descrizione</span><span class="sxs-lookup"><span data-stu-id="8b3a2-252">Description</span></span>|<span data-ttu-id="8b3a2-253">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="8b3a2-253">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="8b3a2-254">set-backend-service</span><span class="sxs-lookup"><span data-stu-id="8b3a2-254">set-backend-service</span></span>|<span data-ttu-id="8b3a2-255">Elemento radice.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-255">Root element.</span></span>|<span data-ttu-id="8b3a2-256">Sì</span><span class="sxs-lookup"><span data-stu-id="8b3a2-256">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="8b3a2-257">Attributi</span><span class="sxs-lookup"><span data-stu-id="8b3a2-257">Attributes</span></span>  
  
|<span data-ttu-id="8b3a2-258">Nome</span><span class="sxs-lookup"><span data-stu-id="8b3a2-258">Name</span></span>|<span data-ttu-id="8b3a2-259">Descrizione</span><span class="sxs-lookup"><span data-stu-id="8b3a2-259">Description</span></span>|<span data-ttu-id="8b3a2-260">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="8b3a2-260">Required</span></span>|<span data-ttu-id="8b3a2-261">Default</span><span class="sxs-lookup"><span data-stu-id="8b3a2-261">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="8b3a2-262">base-url</span><span class="sxs-lookup"><span data-stu-id="8b3a2-262">base-url</span></span>|<span data-ttu-id="8b3a2-263">Nuovo URL di base del servizio back-end.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-263">New backend service base URL.</span></span>|<span data-ttu-id="8b3a2-264">No</span><span class="sxs-lookup"><span data-stu-id="8b3a2-264">No</span></span>|<span data-ttu-id="8b3a2-265">N/D</span><span class="sxs-lookup"><span data-stu-id="8b3a2-265">N/A</span></span>|  
|<span data-ttu-id="8b3a2-266">backend-id</span><span class="sxs-lookup"><span data-stu-id="8b3a2-266">backend-id</span></span>|<span data-ttu-id="8b3a2-267">Identificatore del back-end verso cui avviene il routing.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-267">Identifier of the backend to route to.</span></span>|<span data-ttu-id="8b3a2-268">No</span><span class="sxs-lookup"><span data-stu-id="8b3a2-268">No</span></span>|<span data-ttu-id="8b3a2-269">N/D</span><span class="sxs-lookup"><span data-stu-id="8b3a2-269">N/A</span></span>|  
|<span data-ttu-id="8b3a2-270">sf-partition-key</span><span class="sxs-lookup"><span data-stu-id="8b3a2-270">sf-partition-key</span></span>|<span data-ttu-id="8b3a2-271">Applicabile solo quando il back-end è un servizio di Service Fabric e viene specificato tramite "backend-id".</span><span class="sxs-lookup"><span data-stu-id="8b3a2-271">Only applicable when the backend is a Service Fabric service and is specified using 'backend-id'.</span></span> <span data-ttu-id="8b3a2-272">Usato per risolvere una partizione specifica dal servizio di risoluzione del nome.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-272">Used to resolve a specific partition from the name resolution service.</span></span>|<span data-ttu-id="8b3a2-273">No</span><span class="sxs-lookup"><span data-stu-id="8b3a2-273">No</span></span>|<span data-ttu-id="8b3a2-274">N/D</span><span class="sxs-lookup"><span data-stu-id="8b3a2-274">N/A</span></span>|  
|<span data-ttu-id="8b3a2-275">sf-replica-type</span><span class="sxs-lookup"><span data-stu-id="8b3a2-275">sf-replica-type</span></span>|<span data-ttu-id="8b3a2-276">Applicabile solo quando il back-end è un servizio di Service Fabric e viene specificato tramite "backend-id".</span><span class="sxs-lookup"><span data-stu-id="8b3a2-276">Only applicable when the backend is a Service Fabric service and is specified using 'backend-id'.</span></span> <span data-ttu-id="8b3a2-277">Controlla se la richiesta deve passare alla replica primaria o secondaria di una partizione.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-277">Controls if the request should go to the primary or secondary replica of a partition.</span></span> |<span data-ttu-id="8b3a2-278">No</span><span class="sxs-lookup"><span data-stu-id="8b3a2-278">No</span></span>|<span data-ttu-id="8b3a2-279">N/D</span><span class="sxs-lookup"><span data-stu-id="8b3a2-279">N/A</span></span>|    
|<span data-ttu-id="8b3a2-280">sf-resolve-condition</span><span class="sxs-lookup"><span data-stu-id="8b3a2-280">sf-resolve-condition</span></span>|<span data-ttu-id="8b3a2-281">Applicabile solo quando il back-end è un servizio di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-281">Only applicable when the backend is a Service Fabric service.</span></span> <span data-ttu-id="8b3a2-282">Condizione che identifica se la chiamata al back-end di Service Fabric deve essere ripetuta con una nuova risoluzione.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-282">Condition identifying if the call to Service Fabric backend has to be repeated with new resolution.</span></span>|<span data-ttu-id="8b3a2-283">No</span><span class="sxs-lookup"><span data-stu-id="8b3a2-283">No</span></span>|<span data-ttu-id="8b3a2-284">N/D</span><span class="sxs-lookup"><span data-stu-id="8b3a2-284">N/A</span></span>|    
|<span data-ttu-id="8b3a2-285">sf-service-instance-name</span><span class="sxs-lookup"><span data-stu-id="8b3a2-285">sf-service-instance-name</span></span>|<span data-ttu-id="8b3a2-286">Applicabile solo quando il back-end è un servizio di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-286">Only applicable when the backend is a Service Fabric service.</span></span> <span data-ttu-id="8b3a2-287">Consente di modificare le istanze del servizio durante il runtime.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-287">Allows to change service instances at runtime.</span></span> |<span data-ttu-id="8b3a2-288">No</span><span class="sxs-lookup"><span data-stu-id="8b3a2-288">No</span></span>|<span data-ttu-id="8b3a2-289">N/D </span><span class="sxs-lookup"><span data-stu-id="8b3a2-289">N/A</span></span>|    

### <a name="usage"></a><span data-ttu-id="8b3a2-290">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="8b3a2-290">Usage</span></span>  
 <span data-ttu-id="8b3a2-291">Questo criterio può essere usato nelle [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e negli [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) del criterio seguenti.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-291">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="8b3a2-292">**Sezioni del criterio:** inbound, backend</span><span class="sxs-lookup"><span data-stu-id="8b3a2-292">**Policy sections:** inbound, backend</span></span>  
  
-   <span data-ttu-id="8b3a2-293">**Ambiti del criterio:** globale, prodotto, API, operazione</span><span class="sxs-lookup"><span data-stu-id="8b3a2-293">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="8b3a2-294"><a name="SetBody"></a> Imposta corpo</span><span class="sxs-lookup"><span data-stu-id="8b3a2-294"><a name="SetBody"></a> Set body</span></span>  
 <span data-ttu-id="8b3a2-295">Il criterio `set-body` consente di impostare il corpo del messaggio per le richieste in ingresso e in uscita.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-295">Use the `set-body` policy to set the message body for incoming and outgoing requests.</span></span> <span data-ttu-id="8b3a2-296">Per accedere al corpo del messaggio è possibile usare la proprietà `context.Request.Body` o `context.Response.Body`, a seconda che il criterio sia nella sezione inbound o outbound.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-296">To access the message body you can use the `context.Request.Body` property or the `context.Response.Body`, depending on whether the policy is in the inbound or outbound section.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="8b3a2-297">Si noti che, per impostazione predefinita, quando si accede al corpo del messaggio con `context.Request.Body` o `context.Response.Body`, il corpo del messaggio originale viene perso e deve essere impostato riportandolo nell'espressione.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-297">Note that by default when you access the message body using `context.Request.Body` or `context.Response.Body`, the original message body is lost and must be set by returning the body back in the expression.</span></span> <span data-ttu-id="8b3a2-298">Per mantenere il contenuto del corpo, impostare il parametro `preserveContent` su `true` quando si accede al messaggio.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-298">To preserve the body content, set the `preserveContent` parameter to `true` when accessing the message.</span></span> <span data-ttu-id="8b3a2-299">Se `preserveContent` è impostato su `true` e l'espressione restituisce un corpo diverso, viene usato il corpo restituito.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-299">If `preserveContent` is set to `true` and a different body is returned by the expression, the returned body is used.</span></span>  
>   
>  <span data-ttu-id="8b3a2-300">Tenere presente le considerazioni seguenti quando si usa il criterio `set-body`.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-300">Please note the following considerations when using the `set-body` policy.</span></span>  
>   
>  -   <span data-ttu-id="8b3a2-301">Se il criterio `set-body` viene usato per restituire un corpo nuovo o aggiornato non è necessario impostare `preserveContent` su `true`, perché il nuovo contenuto del corpo viene fornito in modo esplicito.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-301">If you are using the `set-body` policy to return a new or updated body you don't need to set `preserveContent` to `true` because you are explicitly supplying the new body contents.</span></span>  
> -   <span data-ttu-id="8b3a2-302">Non ha senso mantenere il contenuto di una risposta nella pipeline in ingresso, poiché non è ancora stata ricevuta alcuna risposta.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-302">Preserving the content of a response in the inbound pipeline doesn't make sense because there is no response yet.</span></span>  
> -   <span data-ttu-id="8b3a2-303">Non ha senso neanche mantenere il contenuto di una risposta nella pipeline in uscita perché a questo punto la richiesta è già stata inviata al back-end.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-303">Preserving the content of a request in the outbound pipeline doesn't make sense because the request has already been sent to the backend at this point.</span></span>  
> -   <span data-ttu-id="8b3a2-304">Se questo criterio viene usato quando non vi è alcun corpo del messaggio, ad esempio in un'operazione GET in ingresso, viene generata un'eccezione.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-304">If this policy is used when there is no message body, for example in an inbound GET, an exception is thrown.</span></span>  
  
 <span data-ttu-id="8b3a2-305">Per altre informazioni, vedere le sezioni `context.Request.Body`, `context.Response.Body`e `IMessage` nella tabella [Variabile di contesto](api-management-policy-expressions.md#ContextVariables).</span><span class="sxs-lookup"><span data-stu-id="8b3a2-305">For more information, see the `context.Request.Body`, `context.Response.Body`, and the `IMessage` sections in the [Context variable](api-management-policy-expressions.md#ContextVariables) table.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="8b3a2-306">Istruzione del criterio</span><span class="sxs-lookup"><span data-stu-id="8b3a2-306">Policy statement</span></span>  
  
```xml  
<set-body>new body value as text</set-body>  
```  
  
### <a name="examples"></a><span data-ttu-id="8b3a2-307">Esempi</span><span class="sxs-lookup"><span data-stu-id="8b3a2-307">Examples</span></span>  
  
#### <a name="literal-text-example"></a><span data-ttu-id="8b3a2-308">Esempio di testo letterale</span><span class="sxs-lookup"><span data-stu-id="8b3a2-308">Literal text example</span></span>  
  
```xml  
<set-body>Hello world!</set-body>  
```  
  
#### <a name="example-accessing-the-body-as-a-string-note-that-we-are-preserving-the-original-request-body-so-that-we-can-access-it-later-in-the-pipeline"></a><span data-ttu-id="8b3a2-309">Esempio di accesso al corpo come stringa.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-309">Example accessing the body as a string.</span></span> <span data-ttu-id="8b3a2-310">Si noti che il corpo della richiesta originale viene mantenuto per potervi accedere più avanti nella pipeline.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-310">Note that we are preserving the original request body so that we can access it later in the pipeline.</span></span>
  
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
  
#### <a name="example-accessing-the-body-as-a-jobject-note-that-since-we-are-not-reserving-the-original-request-body-accesing-it-later-in-the-pipeline-will-result-in-an-exception"></a><span data-ttu-id="8b3a2-311">Esempio di accesso al corpo come JObject.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-311">Example accessing the body as a JObject.</span></span> <span data-ttu-id="8b3a2-312">Si noti che il corpo della richiesta originale non viene mantenuto e l'accesso a tale corpo più avanti nella pipeline genererà un'eccezione.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-312">Note that since we are not reserving the original request body, accesing it later in the pipeline will result in an exception.</span></span>  
  
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
  
#### <a name="filter-response-based-on-product"></a><span data-ttu-id="8b3a2-313">Filtrare la risposta in base al prodotto</span><span class="sxs-lookup"><span data-stu-id="8b3a2-313">Filter response based on product</span></span>  
 <span data-ttu-id="8b3a2-314">Questo esempio mostra come eseguire operazioni di filtro sui contenuti rimuovendo elementi di dati dalla risposta ricevuta dal servizio back-end quando si usa il prodotto `Starter`.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-314">This example shows how to perform content filtering by removing data elements from the response received from the backend service when using the `Starter` product.</span></span> <span data-ttu-id="8b3a2-315">Per una dimostrazione relativa alla configurazione e all'uso di questo criterio, vedere l'[episodio 177 di Cloud Cover su altre funzionalità di Gestione API con Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) e passare direttamente al minuto 34:30.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-315">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 34:30.</span></span> <span data-ttu-id="8b3a2-316">Iniziare dal minuto 31:50 per visualizzare una panoramica di [The Dark Sky Forecast API](https://developer.forecast.io/), l'API usata in questa dimostrazione.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-316">Start  at 31:50 to see an overview of [The Dark Sky Forecast API](https://developer.forecast.io/) used for this demo.</span></span>  
  
```xml  
<!-- Copy this snippet into the outbound section to remove a number of data elements from the response received from the backend service based on the name of the api product -->  
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

### <a name="using-liquid-templates-with-set-body"></a><span data-ttu-id="8b3a2-317">Uso di modelli Liquid con set body</span><span class="sxs-lookup"><span data-stu-id="8b3a2-317">Using Liquid templates with set body</span></span> 
<span data-ttu-id="8b3a2-318">Il criterio `set-body` può essere configurato per l'uso del linguaggio di modellazione [Liquid](https://shopify.github.io/liquid/basics/introduction/) per trasformare il corpo di una richiesta o di una risposta.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-318">The `set-body` policy can be configured to use the [Liquid](https://shopify.github.io/liquid/basics/introduction/) templating language to transfom the body of a request or response.</span></span> <span data-ttu-id="8b3a2-319">Può essere molto efficace se si desidera modificare completamente il formato del messaggio.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-319">This can be very effective if you need to completely reshape the format of your message.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8b3a2-320">L'implementazione di Liquid usato nel criterio `set-body` è configurato in "modalità C#".</span><span class="sxs-lookup"><span data-stu-id="8b3a2-320">The implementation of Liquid used in the `set-body` policy is configured in 'C# mode'.</span></span> <span data-ttu-id="8b3a2-321">Questo è particolarmente importante quando si eseguono operazioni quali l'applicazione del filtro.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-321">This is particularly important when doing things such as filtering.</span></span> <span data-ttu-id="8b3a2-322">Ad esempio, l'uso di un filtro data richiede l'uso della convenzione Pascal e della formattazione delle date C#, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="8b3a2-322">As an example, using a date filter requires the use of Pascal casing and C# date formatting e.g.:</span></span>
>
> <span data-ttu-id="8b3a2-323">{{body.foo.startDateTime| Data:"yyyyMMddTHH:mm:ddZ"}}</span><span class="sxs-lookup"><span data-stu-id="8b3a2-323">{{body.foo.startDateTime| Date:"yyyyMMddTHH:mm:ddZ"}}</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8b3a2-324">Per eseguire correttamente l'associazione a un corpo XML utilizzando il modello Liquid, usare un criterio `set-header` per impostare il tipo di contenuto su application/xml, text/xml (o su qualsiasi tipo che termini con +xml); per un corpo JSON, deve essere application/json, testo/json (o qualsiasi tipo che termini con +json).</span><span class="sxs-lookup"><span data-stu-id="8b3a2-324">In order to correctly bind to an XML body using the Liquid template, use a `set-header` policy to set Content-Type to either application/xml, text/xml (or any type ending with +xml); for a JSON body, it must be application/json, text/json (or any type ending with +json).</span></span>

#### <a name="convert-json-to-soap-using-a-liquid-template"></a><span data-ttu-id="8b3a2-325">Convertire JSON in SOAP usando un modello Liquid</span><span class="sxs-lookup"><span data-stu-id="8b3a2-325">Convert JSON to SOAP using a Liquid template</span></span>
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

#### <a name="tranform-json-using-a-liquid-template"></a><span data-ttu-id="8b3a2-326">Trasformare JSON usando un modello Liquid</span><span class="sxs-lookup"><span data-stu-id="8b3a2-326">Tranform JSON using a Liquid template</span></span>
```xml
{
"order": {
    "id": "{{body.customer.purchase.identifier}}",
    "summary": "{{body.customer.purchase.orderShortDesc}}"
    }
}
```

### <a name="elements"></a><span data-ttu-id="8b3a2-327">Elementi</span><span class="sxs-lookup"><span data-stu-id="8b3a2-327">Elements</span></span>  
  
|<span data-ttu-id="8b3a2-328">Nome</span><span class="sxs-lookup"><span data-stu-id="8b3a2-328">Name</span></span>|<span data-ttu-id="8b3a2-329">Descrizione</span><span class="sxs-lookup"><span data-stu-id="8b3a2-329">Description</span></span>|<span data-ttu-id="8b3a2-330">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="8b3a2-330">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="8b3a2-331">set-body</span><span class="sxs-lookup"><span data-stu-id="8b3a2-331">set-body</span></span>|<span data-ttu-id="8b3a2-332">Elemento radice.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-332">Root element.</span></span> <span data-ttu-id="8b3a2-333">Contiene il testo del corpo o un'espressione che restituisce un corpo.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-333">Contains the body text or an expressions that returns a body.</span></span>|<span data-ttu-id="8b3a2-334">Sì</span><span class="sxs-lookup"><span data-stu-id="8b3a2-334">Yes</span></span>|  

### <a name="properties"></a><span data-ttu-id="8b3a2-335">Proprietà</span><span class="sxs-lookup"><span data-stu-id="8b3a2-335">Properties</span></span>  
  
|<span data-ttu-id="8b3a2-336">Nome</span><span class="sxs-lookup"><span data-stu-id="8b3a2-336">Name</span></span>|<span data-ttu-id="8b3a2-337">Descrizione</span><span class="sxs-lookup"><span data-stu-id="8b3a2-337">Description</span></span>|<span data-ttu-id="8b3a2-338">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="8b3a2-338">Required</span></span>|<span data-ttu-id="8b3a2-339">Default</span><span class="sxs-lookup"><span data-stu-id="8b3a2-339">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="8b3a2-340">template</span><span class="sxs-lookup"><span data-stu-id="8b3a2-340">template</span></span>|<span data-ttu-id="8b3a2-341">Consente di modificare la modalità di modello in cui verrà eseguito il criterio del corpo impostato.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-341">Used to change the templating mode that the set body policy will run in.</span></span> <span data-ttu-id="8b3a2-342">Al momento, l'unico valore supportato è:</span><span class="sxs-lookup"><span data-stu-id="8b3a2-342">Currently the only supported value is:</span></span><br /><br /><span data-ttu-id="8b3a2-343">-liquid - i criteri del corpo impostati useranno il motore del modello liquidi</span><span class="sxs-lookup"><span data-stu-id="8b3a2-343">- liquid - the set body policy will use the liquid templating engine</span></span> |<span data-ttu-id="8b3a2-344">No</span><span class="sxs-lookup"><span data-stu-id="8b3a2-344">No</span></span>|<span data-ttu-id="8b3a2-345">liquid</span><span class="sxs-lookup"><span data-stu-id="8b3a2-345">liquid</span></span>|  

<span data-ttu-id="8b3a2-346">Per accedere alle informazioni sulla richiesta e la risposta, il modello Liquid può essere associato a un oggetto di contesto con le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="8b3a2-346">For accessing information about the request and response, the Liquid template can bind to a context object with the following properties:</span></span> <br />
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



### <a name="usage"></a><span data-ttu-id="8b3a2-347">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="8b3a2-347">Usage</span></span>  
 <span data-ttu-id="8b3a2-348">Questo criterio può essere usato nelle [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e negli [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) del criterio seguenti.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-348">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="8b3a2-349">**Sezioni del criterio:** inbound, outbound, back-end</span><span class="sxs-lookup"><span data-stu-id="8b3a2-349">**Policy sections:** inbound, outbound, backend</span></span>  
  
-   <span data-ttu-id="8b3a2-350">**Ambiti del criterio:** globale, prodotto, API, operazione</span><span class="sxs-lookup"><span data-stu-id="8b3a2-350">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="8b3a2-351"><a name="SetHTTPheader"></a> Imposta intestazione HTTP</span><span class="sxs-lookup"><span data-stu-id="8b3a2-351"><a name="SetHTTPheader"></a> Set HTTP header</span></span>  
 <span data-ttu-id="8b3a2-352">Il criterio `set-header` assegna un valore a un'intestazione di risposta e/o di richiesta esistente oppure aggiunge una nuova intestazione di risposta e/o di richiesta.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-352">The `set-header` policy assigns a value to an existing response and/or request header or adds a new response and/or request header.</span></span>  
  
 <span data-ttu-id="8b3a2-353">Inserisce un elenco di intestazioni HTTP in un messaggio HTTP.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-353">Inserts a list of HTTP headers into an HTTP message.</span></span> <span data-ttu-id="8b3a2-354">Se inserito in una pipeline in entrata, questo criterio imposta le intestazioni HTTP per la richiesta passata al servizio di destinazione.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-354">When placed in an inbound pipeline, this policy sets the HTTP headers for the request being passed to the target service.</span></span> <span data-ttu-id="8b3a2-355">Se inserito in una pipeline in uscita, questo criterio imposta le intestazioni HTTP per la risposta inviata al client del gateway.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-355">When placed in an outbound pipeline, this policy sets the HTTP headers for the response being sent to the gateway’s client.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="8b3a2-356">Istruzione del criterio</span><span class="sxs-lookup"><span data-stu-id="8b3a2-356">Policy statement</span></span>  
  
```xml  
<set-header name="header name" exists-action="override | skip | append | delete">  
    <value>value</value> <!--for multiple headers with the same name add additional value elements-->  
</set-header>  
```  
  
### <a name="examples"></a><span data-ttu-id="8b3a2-357">Esempi</span><span class="sxs-lookup"><span data-stu-id="8b3a2-357">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="8b3a2-358">Esempio</span><span class="sxs-lookup"><span data-stu-id="8b3a2-358">Example</span></span>  
  
```xml  
<set-header name="some header name" exists-action="override">  
    <value>20</value>   
</set-header>  
```  
  
#### <a name="forward-context-information-to-the-backend-service"></a><span data-ttu-id="8b3a2-359">Inoltro di informazioni di contesto al servizio back-end</span><span class="sxs-lookup"><span data-stu-id="8b3a2-359">Forward context information to the backend service</span></span>  
 <span data-ttu-id="8b3a2-360">Questo esempio illustra come applicare criteri a livello di API per fornire informazioni di contesto al servizio back-end.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-360">This example shows how to apply policy at the API level to supply context information to the backend service.</span></span> <span data-ttu-id="8b3a2-361">Per una dimostrazione relativa alla configurazione e all'uso di questo criterio, vedere l'[episodio 177 di Cloud Cover su altre funzionalità di Gestione API con Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) e passare direttamente al minuto 10:30.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-361">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 10:30.</span></span> <span data-ttu-id="8b3a2-362">Al minuto 12:10 è illustrato come richiamare un'operazione nel portale per sviluppatori, dove è possibile vedere all'opera il criterio in questione.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-362">At 12:10 there is a demo of calling an operation in the developer portal where you can see the policy at work.</span></span>  
  
```xml  
<!-- Copy this snippet into the inbound element to forward some context information, user id and the region the gateway is hosted in, to the backend service for logging or evaluation -->  
<set-header name="x-request-context-data" exists-action="override">  
  <value>@(context.User.Id)</value>  
  <value>@(context.Deployment.Region)</value>  
</set-header>  
```  
  
 <span data-ttu-id="8b3a2-363">Per altre informazioni, vedere [Espressioni di criteri](api-management-policy-expressions.md) e [Variabile di contesto](api-management-policy-expressions.md#ContextVariables).</span><span class="sxs-lookup"><span data-stu-id="8b3a2-363">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="8b3a2-364">Elementi</span><span class="sxs-lookup"><span data-stu-id="8b3a2-364">Elements</span></span>  
  
|<span data-ttu-id="8b3a2-365">Nome</span><span class="sxs-lookup"><span data-stu-id="8b3a2-365">Name</span></span>|<span data-ttu-id="8b3a2-366">Descrizione</span><span class="sxs-lookup"><span data-stu-id="8b3a2-366">Description</span></span>|<span data-ttu-id="8b3a2-367">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="8b3a2-367">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="8b3a2-368">set-header</span><span class="sxs-lookup"><span data-stu-id="8b3a2-368">set-header</span></span>|<span data-ttu-id="8b3a2-369">Elemento radice.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-369">Root element.</span></span>|<span data-ttu-id="8b3a2-370">Sì</span><span class="sxs-lookup"><span data-stu-id="8b3a2-370">Yes</span></span>|  
|<span data-ttu-id="8b3a2-371">value</span><span class="sxs-lookup"><span data-stu-id="8b3a2-371">value</span></span>|<span data-ttu-id="8b3a2-372">Specifica il valore dell'intestazione da impostare.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-372">Specifies the value of the header to be set.</span></span> <span data-ttu-id="8b3a2-373">Se occorrono più intestazioni con lo stesso nome, aggiungere altri elementi `value`.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-373">For multiple headers with the same name add additional `value` elements.</span></span>|<span data-ttu-id="8b3a2-374">Sì</span><span class="sxs-lookup"><span data-stu-id="8b3a2-374">Yes</span></span>|  
  
### <a name="properties"></a><span data-ttu-id="8b3a2-375">Proprietà</span><span class="sxs-lookup"><span data-stu-id="8b3a2-375">Properties</span></span>  
  
|<span data-ttu-id="8b3a2-376">Nome</span><span class="sxs-lookup"><span data-stu-id="8b3a2-376">Name</span></span>|<span data-ttu-id="8b3a2-377">Descrizione</span><span class="sxs-lookup"><span data-stu-id="8b3a2-377">Description</span></span>|<span data-ttu-id="8b3a2-378">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="8b3a2-378">Required</span></span>|<span data-ttu-id="8b3a2-379">Default</span><span class="sxs-lookup"><span data-stu-id="8b3a2-379">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="8b3a2-380">exists-action</span><span class="sxs-lookup"><span data-stu-id="8b3a2-380">exists-action</span></span>|<span data-ttu-id="8b3a2-381">Specifica l'azione da eseguire quando l'intestazione è già specificata.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-381">Specifies what action to take when the header is already specified.</span></span> <span data-ttu-id="8b3a2-382">Questo attributo deve avere uno dei valori seguenti.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-382">This attribute must have one of the following values.</span></span><br /><br /> <span data-ttu-id="8b3a2-383">-   override - sostituisce il valore dell'intestazione esistente.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-383">-   override - replaces the value of the existing header.</span></span><br /><span data-ttu-id="8b3a2-384">-   skip - non sostituisce il valore dell'intestazione esistente.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-384">-   skip - does not replace the existing header value.</span></span><br /><span data-ttu-id="8b3a2-385">-   append - aggiunge il valore dell'intestazione esistente.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-385">-   append - appends the value to the existing header value.</span></span><br /><span data-ttu-id="8b3a2-386">-   delete - elimina l'intestazione dalla richiesta.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-386">-   delete - removes the header from the request.</span></span><br /><br /> <span data-ttu-id="8b3a2-387">Se è impostato su `override`, l'integrazione di più voci con lo stesso nome avrà come risultato l'impostazione dell'intestazione in base a tutte le voci, che saranno elencate più volte. Nel risultato saranno impostati solo i valori elencati.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-387">When set to `override` enlisting multiple entries with the same name results in the header being set according to all entries (which will be listed multiple times); only listed values will be set in the result.</span></span>|<span data-ttu-id="8b3a2-388">No</span><span class="sxs-lookup"><span data-stu-id="8b3a2-388">No</span></span>|<span data-ttu-id="8b3a2-389">override</span><span class="sxs-lookup"><span data-stu-id="8b3a2-389">override</span></span>|  
|<span data-ttu-id="8b3a2-390">name</span><span class="sxs-lookup"><span data-stu-id="8b3a2-390">name</span></span>|<span data-ttu-id="8b3a2-391">Specifica il nome dell'intestazione da impostare.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-391">Specifies name of the header to be set.</span></span>|<span data-ttu-id="8b3a2-392">Sì</span><span class="sxs-lookup"><span data-stu-id="8b3a2-392">Yes</span></span>|<span data-ttu-id="8b3a2-393">N/D</span><span class="sxs-lookup"><span data-stu-id="8b3a2-393">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="8b3a2-394">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="8b3a2-394">Usage</span></span>  
 <span data-ttu-id="8b3a2-395">Questo criterio può essere usato nelle [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e negli [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) del criterio seguenti.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-395">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="8b3a2-396">**Sezioni del criterio:**in ingresso, in uscita, back-end, on-error</span><span class="sxs-lookup"><span data-stu-id="8b3a2-396">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="8b3a2-397">**Ambiti del criterio:** globale, prodotto, API, operazione</span><span class="sxs-lookup"><span data-stu-id="8b3a2-397">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="8b3a2-398"><a name="SetQueryStringParameter"></a> Imposta parametro di stringa della query</span><span class="sxs-lookup"><span data-stu-id="8b3a2-398"><a name="SetQueryStringParameter"></a> Set query string parameter</span></span>  
 <span data-ttu-id="8b3a2-399">Il criterio `set-query-parameter` aggiunge, sostituisce il valore di o elimina il parametro di stringa della query di richiesta.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-399">The `set-query-parameter` policy adds, replaces value of, or deletes request query string parameter.</span></span> <span data-ttu-id="8b3a2-400">Può essere usato per passare i parametri di query previsti dal servizio back-end che sono facoltativi o non sono mai presenti nella richiesta.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-400">Can be used to pass query parameters expected by the backend service which are optional or never present in the request.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="8b3a2-401">Istruzione del criterio</span><span class="sxs-lookup"><span data-stu-id="8b3a2-401">Policy statement</span></span>  
  
```xml  
<set-query-parameter name="param name" exists-action="override | skip | append | delete">  
    <value>value</value> <!--for multiple parameters with the same name add additional value elements-->  
</set-query-parameter>  
```  
  
### <a name="examples"></a><span data-ttu-id="8b3a2-402">Esempi</span><span class="sxs-lookup"><span data-stu-id="8b3a2-402">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="8b3a2-403">Esempio</span><span class="sxs-lookup"><span data-stu-id="8b3a2-403">Example</span></span>  
  
```xml  
  
<set-query-parameter>  
  <parameter name="api-key" exists-action="skip">  
    <value>12345678901</value>  
  </parameter>  
  <!-- for multiple parameters with the same name add additional value elements -->  
</set-query-parameter>  
  
```  
  
#### <a name="forward-context-information-to-the-backend-service"></a><span data-ttu-id="8b3a2-404">Inoltro di informazioni di contesto al servizio back-end</span><span class="sxs-lookup"><span data-stu-id="8b3a2-404">Forward context information to the backend service</span></span>  
 <span data-ttu-id="8b3a2-405">Questo esempio illustra come applicare criteri a livello di API per fornire informazioni di contesto al servizio back-end.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-405">This example shows how to apply policy at the API level to supply context information to the backend service.</span></span> <span data-ttu-id="8b3a2-406">Per una dimostrazione relativa alla configurazione e all'uso di questo criterio, vedere l'[episodio 177 di Cloud Cover su altre funzionalità di Gestione API con Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) e passare direttamente al minuto 10:30.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-406">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 10:30.</span></span> <span data-ttu-id="8b3a2-407">Al minuto 12:10 è illustrato come richiamare un'operazione nel portale per sviluppatori, dove è possibile vedere all'opera il criterio in questione.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-407">At 12:10 there is a demo of calling an operation in the developer portal where you can see the policy at work.</span></span>  
  
```xml  
<!-- Copy this snippet into the inbound element to forward a piece of context, product name in this example, to the backend service for logging or evaluation -->  
<set-query-parameter name="x-product-name" exists-action="override">  
  <value>@(context.Product.Name)</value>  
</set-query-parameter>  
  
```  
  
 <span data-ttu-id="8b3a2-408">Per altre informazioni, vedere [Espressioni di criteri](api-management-policy-expressions.md) e [Variabile di contesto](api-management-policy-expressions.md#ContextVariables).</span><span class="sxs-lookup"><span data-stu-id="8b3a2-408">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="8b3a2-409">Elementi</span><span class="sxs-lookup"><span data-stu-id="8b3a2-409">Elements</span></span>  
  
|<span data-ttu-id="8b3a2-410">Nome</span><span class="sxs-lookup"><span data-stu-id="8b3a2-410">Name</span></span>|<span data-ttu-id="8b3a2-411">Descrizione</span><span class="sxs-lookup"><span data-stu-id="8b3a2-411">Description</span></span>|<span data-ttu-id="8b3a2-412">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="8b3a2-412">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="8b3a2-413">set-query-parameter</span><span class="sxs-lookup"><span data-stu-id="8b3a2-413">set-query-parameter</span></span>|<span data-ttu-id="8b3a2-414">Elemento radice.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-414">Root element.</span></span>|<span data-ttu-id="8b3a2-415">Sì</span><span class="sxs-lookup"><span data-stu-id="8b3a2-415">Yes</span></span>|  
|<span data-ttu-id="8b3a2-416">value</span><span class="sxs-lookup"><span data-stu-id="8b3a2-416">value</span></span>|<span data-ttu-id="8b3a2-417">Specifica il valore del parametro di query da impostare.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-417">Specifies the value of the query parameter to be set.</span></span> <span data-ttu-id="8b3a2-418">Se occorrono più parametri di query con lo stesso nome, aggiungere altri elementi `value`.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-418">For multiple query parameters with the same name add additional `value` elements.</span></span>|<span data-ttu-id="8b3a2-419">Sì</span><span class="sxs-lookup"><span data-stu-id="8b3a2-419">Yes</span></span>|  
  
### <a name="properties"></a><span data-ttu-id="8b3a2-420">Proprietà</span><span class="sxs-lookup"><span data-stu-id="8b3a2-420">Properties</span></span>  
  
|<span data-ttu-id="8b3a2-421">Nome</span><span class="sxs-lookup"><span data-stu-id="8b3a2-421">Name</span></span>|<span data-ttu-id="8b3a2-422">Descrizione</span><span class="sxs-lookup"><span data-stu-id="8b3a2-422">Description</span></span>|<span data-ttu-id="8b3a2-423">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="8b3a2-423">Required</span></span>|<span data-ttu-id="8b3a2-424">Default</span><span class="sxs-lookup"><span data-stu-id="8b3a2-424">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="8b3a2-425">exists-action</span><span class="sxs-lookup"><span data-stu-id="8b3a2-425">exists-action</span></span>|<span data-ttu-id="8b3a2-426">Specifica l'azione da eseguire quando il parametro di query è già specificato.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-426">Specifies what action to take when the query parameter is already specified.</span></span> <span data-ttu-id="8b3a2-427">Questo attributo deve avere uno dei valori seguenti.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-427">This attribute must have one of the following values.</span></span><br /><br /> <span data-ttu-id="8b3a2-428">-   override - sostituisce il valore del parametro esistente.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-428">-   override - replaces the value of the existing parameter.</span></span><br /><span data-ttu-id="8b3a2-429">-   skip - non sostituisce il valore del parametro di query esistente.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-429">-   skip - does not replace the existing query parameter value.</span></span><br /><span data-ttu-id="8b3a2-430">-   append - aggiunge il valore del parametro di query esistente.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-430">-   append - appends the value to the existing query parameter value.</span></span><br /><span data-ttu-id="8b3a2-431">-   delete - elimina il parametro di query dalla richiesta.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-431">-   delete - removes the query parameter from the request.</span></span><br /><br /> <span data-ttu-id="8b3a2-432">Se è impostato su `override`, l'integrazione di più voci con lo stesso nome avrà come risultato l'impostazione del parametro di query in base a tutte le voci, che saranno elencate più volte. Nel risultato saranno impostati solo i valori elencati.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-432">When set to `override` enlisting multiple entries with the same name results in the query parameter being set according to all entries (which will be listed multiple times); only listed values will be set in the result.</span></span>|<span data-ttu-id="8b3a2-433">No</span><span class="sxs-lookup"><span data-stu-id="8b3a2-433">No</span></span>|<span data-ttu-id="8b3a2-434">override</span><span class="sxs-lookup"><span data-stu-id="8b3a2-434">override</span></span>|  
|<span data-ttu-id="8b3a2-435">name</span><span class="sxs-lookup"><span data-stu-id="8b3a2-435">name</span></span>|<span data-ttu-id="8b3a2-436">Specifica il nome del parametro di query da impostare.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-436">Specifies name of the query parameter to be set.</span></span>|<span data-ttu-id="8b3a2-437">Sì</span><span class="sxs-lookup"><span data-stu-id="8b3a2-437">Yes</span></span>|<span data-ttu-id="8b3a2-438">N/D</span><span class="sxs-lookup"><span data-stu-id="8b3a2-438">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="8b3a2-439">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="8b3a2-439">Usage</span></span>  
 <span data-ttu-id="8b3a2-440">Questo criterio può essere usato nelle [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e negli [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) del criterio seguenti.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-440">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="8b3a2-441">**Sezioni del criterio:** inbound, backend</span><span class="sxs-lookup"><span data-stu-id="8b3a2-441">**Policy sections:** inbound, backend</span></span>  
  
-   <span data-ttu-id="8b3a2-442">**Ambiti del criterio:** globale, prodotto, API, operazione</span><span class="sxs-lookup"><span data-stu-id="8b3a2-442">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="8b3a2-443"><a name="RewriteURL"></a> Riscrivi URL</span><span class="sxs-lookup"><span data-stu-id="8b3a2-443"><a name="RewriteURL"></a> Rewrite URL</span></span>  
 <span data-ttu-id="8b3a2-444">Il criterio `rewrite-uri` converte un URL di richiesta dal formato pubblico al formato previsto dal servizio Web, come mostrato nell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-444">The `rewrite-uri` policy converts a request URL from its public form to the form expected by the web service, as shown in the following example.</span></span>  
  
-   <span data-ttu-id="8b3a2-445">URL pubblico - `http://api.example.com/storenumber/ordernumber`</span><span class="sxs-lookup"><span data-stu-id="8b3a2-445">Public URL - `http://api.example.com/storenumber/ordernumber`</span></span>  
  
-   <span data-ttu-id="8b3a2-446">URL richiesta - `http://api.example.com/v2/US/hardware/storenumber&ordernumber?City&State`</span><span class="sxs-lookup"><span data-stu-id="8b3a2-446">Request URL - `http://api.example.com/v2/US/hardware/storenumber&ordernumber?City&State`</span></span>  
  
 <span data-ttu-id="8b3a2-447">Il criterio può essere usato quando un URL ideale per utenti e/o per il browser deve essere trasformato nel formato di URL previsto dal servizio Web.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-447">This policy can be used when a human and/or browser-friendly URL should be transformed into the URL format expected by the web service.</span></span> <span data-ttu-id="8b3a2-448">Il criterio deve essere applicato soltanto quando viene esposto un formato di URL alternativo, ad esempio URL semplici, URL RESTful, URL ideali per gli utenti o URL ideali per SEO, che sono URL puramente strutturali, non includono una stringa di query ma contengono solo il percorso della risorsa, dopo lo schema e l'autorità.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-448">This policy only needs to be applied when exposing an alternative URL format, such as clean URLs, RESTful URLs, user-friendly URLs or SEO-friendly URLs that are purely structural URLs that do not contain a query string and instead contain only the path of the resource (after the scheme and the authority).</span></span> <span data-ttu-id="8b3a2-449">Sono spesso usati a fini estetici, di usabilità o di ottimizzazione dei motori di ricerca (SEO, Search Engine Optimization).</span><span class="sxs-lookup"><span data-stu-id="8b3a2-449">This is often done for aesthetic, usability, or search engine optimization (SEO) purposes.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="8b3a2-450">Il criterio consente di aggiungere solo parametri delle stringhe di query.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-450">You can only add query string parameters using the policy.</span></span> <span data-ttu-id="8b3a2-451">Non è possibile aggiungere un parametro di percorso di modello aggiuntivo nell'URL riscritto.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-451">You cannot add extra template path parameters in the rewrite URL.</span></span>  

### <a name="policy-statement"></a><span data-ttu-id="8b3a2-452">Istruzione del criterio</span><span class="sxs-lookup"><span data-stu-id="8b3a2-452">Policy statement</span></span>  
  
```xml  
<rewrite-uri template="uri template" copy-unmatched-params="true | false" />  
```  
  
### <a name="example"></a><span data-ttu-id="8b3a2-453">Esempio</span><span class="sxs-lookup"><span data-stu-id="8b3a2-453">Example</span></span>  
  
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
<!-- Assuming incoming request is /get?a=b&c=d and operation template is set to /get?a={b} -->
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
<!-- Assuming incoming request is /get?a=b&c=d and operation template is set to /get?a={b} -->
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

### <a name="elements"></a><span data-ttu-id="8b3a2-454">Elementi</span><span class="sxs-lookup"><span data-stu-id="8b3a2-454">Elements</span></span>  
  
|<span data-ttu-id="8b3a2-455">Nome</span><span class="sxs-lookup"><span data-stu-id="8b3a2-455">Name</span></span>|<span data-ttu-id="8b3a2-456">Descrizione</span><span class="sxs-lookup"><span data-stu-id="8b3a2-456">Description</span></span>|<span data-ttu-id="8b3a2-457">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="8b3a2-457">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="8b3a2-458">rewrite-uri</span><span class="sxs-lookup"><span data-stu-id="8b3a2-458">rewrite-uri</span></span>|<span data-ttu-id="8b3a2-459">Elemento radice.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-459">Root element.</span></span>|<span data-ttu-id="8b3a2-460">Sì</span><span class="sxs-lookup"><span data-stu-id="8b3a2-460">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="8b3a2-461">Attributi</span><span class="sxs-lookup"><span data-stu-id="8b3a2-461">Attributes</span></span>  
  
|<span data-ttu-id="8b3a2-462">Attributo</span><span class="sxs-lookup"><span data-stu-id="8b3a2-462">Attribute</span></span>|<span data-ttu-id="8b3a2-463">Descrizione</span><span class="sxs-lookup"><span data-stu-id="8b3a2-463">Description</span></span>|<span data-ttu-id="8b3a2-464">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="8b3a2-464">Required</span></span>|<span data-ttu-id="8b3a2-465">Default</span><span class="sxs-lookup"><span data-stu-id="8b3a2-465">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="8b3a2-466">template</span><span class="sxs-lookup"><span data-stu-id="8b3a2-466">template</span></span>|<span data-ttu-id="8b3a2-467">URL effettivo del servizio Web con eventuali parametri delle stringhe di query.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-467">The actual web service URL with any query string parameters.</span></span> <span data-ttu-id="8b3a2-468">Quando si usano le espressioni, l'intero valore deve essere un'espressione.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-468">When using expressions, the whole value must be an expression.</span></span>|<span data-ttu-id="8b3a2-469">Sì</span><span class="sxs-lookup"><span data-stu-id="8b3a2-469">Yes</span></span>|<span data-ttu-id="8b3a2-470">N/D</span><span class="sxs-lookup"><span data-stu-id="8b3a2-470">N/A</span></span>|  
|<span data-ttu-id="8b3a2-471">copy-unmatched-params</span><span class="sxs-lookup"><span data-stu-id="8b3a2-471">copy-unmatched-params</span></span>|<span data-ttu-id="8b3a2-472">Specifica se i parametri di query nella richiesta in ingresso non presenti nel modello di URL originale vengono aggiunti all'URL definito dal modello di riscrittura</span><span class="sxs-lookup"><span data-stu-id="8b3a2-472">Specifies whether query parameters in the incoming request not present in the original URL template are added to the URL defined by the re-write template</span></span>|<span data-ttu-id="8b3a2-473">No</span><span class="sxs-lookup"><span data-stu-id="8b3a2-473">No</span></span>|<span data-ttu-id="8b3a2-474">true</span><span class="sxs-lookup"><span data-stu-id="8b3a2-474">true</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="8b3a2-475">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="8b3a2-475">Usage</span></span>  
 <span data-ttu-id="8b3a2-476">Questo criterio può essere usato nelle [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e negli [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) del criterio seguenti.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-476">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="8b3a2-477">**Sezioni del criterio:** inbound</span><span class="sxs-lookup"><span data-stu-id="8b3a2-477">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="8b3a2-478">**Ambiti del criterio:** prodotto, API, operazione</span><span class="sxs-lookup"><span data-stu-id="8b3a2-478">**Policy scopes:** product, API, operation</span></span>  
  
##  <span data-ttu-id="8b3a2-479"><a name="XSLTransform"></a>Trasforma XML usando XSLT</span><span class="sxs-lookup"><span data-stu-id="8b3a2-479"><a name="XSLTransform"></a> Transform XML using an XSLT</span></span>  
 <span data-ttu-id="8b3a2-480">Il criterio `Transform XML using an XSLT` applica una trasformazione XSL all'XML nel corpo della richiesta o della risposta.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-480">The `Transform XML using an XSLT` policy applies an XSL transformation to XML in the request or response body.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="8b3a2-481">Istruzione del criterio</span><span class="sxs-lookup"><span data-stu-id="8b3a2-481">Policy statement</span></span>  
  
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
  
### <a name="example"></a><span data-ttu-id="8b3a2-482">Esempio</span><span class="sxs-lookup"><span data-stu-id="8b3a2-482">Example</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="8b3a2-483">Elementi</span><span class="sxs-lookup"><span data-stu-id="8b3a2-483">Elements</span></span>  
  
|<span data-ttu-id="8b3a2-484">Nome</span><span class="sxs-lookup"><span data-stu-id="8b3a2-484">Name</span></span>|<span data-ttu-id="8b3a2-485">Descrizione</span><span class="sxs-lookup"><span data-stu-id="8b3a2-485">Description</span></span>|<span data-ttu-id="8b3a2-486">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="8b3a2-486">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="8b3a2-487">xsl-transform</span><span class="sxs-lookup"><span data-stu-id="8b3a2-487">xsl-transform</span></span>|<span data-ttu-id="8b3a2-488">Elemento radice.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-488">Root element.</span></span>|<span data-ttu-id="8b3a2-489">Sì</span><span class="sxs-lookup"><span data-stu-id="8b3a2-489">Yes</span></span>|  
|<span data-ttu-id="8b3a2-490">parametro</span><span class="sxs-lookup"><span data-stu-id="8b3a2-490">parameter</span></span>|<span data-ttu-id="8b3a2-491">Consente di definire le variabili usate nella trasformazione</span><span class="sxs-lookup"><span data-stu-id="8b3a2-491">Used to define variables used in the transform</span></span>|<span data-ttu-id="8b3a2-492">No</span><span class="sxs-lookup"><span data-stu-id="8b3a2-492">No</span></span>|  
|<span data-ttu-id="8b3a2-493">xsl:stylesheet</span><span class="sxs-lookup"><span data-stu-id="8b3a2-493">xsl:stylesheet</span></span>|<span data-ttu-id="8b3a2-494">Elemento del foglio di stile principale.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-494">Root stylesheet element.</span></span> <span data-ttu-id="8b3a2-495">Tutti gli elementi e gli attributi definiti rispettano le [specifiche XSLT](http://www.w3.org/TR/xslt) standard</span><span class="sxs-lookup"><span data-stu-id="8b3a2-495">All elements and attributes defined within follow the standard [XSLT specification](http://www.w3.org/TR/xslt)</span></span>|<span data-ttu-id="8b3a2-496">Sì</span><span class="sxs-lookup"><span data-stu-id="8b3a2-496">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="8b3a2-497">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="8b3a2-497">Usage</span></span>  
 <span data-ttu-id="8b3a2-498">Questo criterio può essere usato nelle [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e negli [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) del criterio seguenti.</span><span class="sxs-lookup"><span data-stu-id="8b3a2-498">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="8b3a2-499">**Sezioni del criterio:** inbound, outbound</span><span class="sxs-lookup"><span data-stu-id="8b3a2-499">**Policy sections:** inbound, outbound</span></span>  
  
-   <span data-ttu-id="8b3a2-500">**Ambiti del criterio:** globale, prodotto, API, operazione</span><span class="sxs-lookup"><span data-stu-id="8b3a2-500">**Policy scopes:** global, product, API, operation</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="8b3a2-501">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8b3a2-501">Next steps</span></span>
<span data-ttu-id="8b3a2-502">Per altre informazioni sull'uso dei criteri, vedere [Criteri di Gestione API](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="8b3a2-502">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  
