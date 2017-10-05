---
title: API di raccolta dati HTTP di Log Analytics | Microsoft Docs
description: "È possibile usare l'API di raccolta dati HTTP di Log Analytics per aggiungere dati POST JSON nel repository di Log Analytics da qualunque client possa chiamare l'API REST. Questo articolo illustra come usare l'API e descrive esempi di come pubblicare i dati con diversi linguaggi di programmazione."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: 
ms.assetid: a831fd90-3f55-423b-8b20-ccbaaac2ca75
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: bwren
ms.openlocfilehash: b0c45ff8c1d4c9d35fbb3c8839b38a20df277055
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="send-data-to-log-analytics-with-the-http-data-collector-api"></a><span data-ttu-id="4cf19-104">Inviare dati a Log Analytics con l'API dell'agente di raccolta dati HTTP</span><span class="sxs-lookup"><span data-stu-id="4cf19-104">Send data to Log Analytics with the HTTP Data Collector API</span></span>
<span data-ttu-id="4cf19-105">Questo articolo illustra come usare l'API dell'agente di raccolta dati HTTP per inviare dati a Log Analytics da un client dell'API REST.</span><span class="sxs-lookup"><span data-stu-id="4cf19-105">This article shows you how to use the HTTP Data Collector API to send data to Log Analytics from a REST API client.</span></span>  <span data-ttu-id="4cf19-106">L'articolo descrive come formattare i dati raccolti dall'applicazione o dallo script, come includerli in una richiesta e come autorizzare tale richiesta in Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="4cf19-106">It describes how to format data collected by your script or application, include it in a request, and have that request authorized by Log Analytics.</span></span>  <span data-ttu-id="4cf19-107">Vengono indicati esempi per PowerShell, C# e Python.</span><span class="sxs-lookup"><span data-stu-id="4cf19-107">Examples are provided for PowerShell, C#, and Python.</span></span>

## <a name="concepts"></a><span data-ttu-id="4cf19-108">Concetti</span><span class="sxs-lookup"><span data-stu-id="4cf19-108">Concepts</span></span>
<span data-ttu-id="4cf19-109">È possibile usare l'API dell'agente di raccolta dati HTTP per inviare dati a Log Analytics da qualsiasi client in grado di chiamare un'API REST.</span><span class="sxs-lookup"><span data-stu-id="4cf19-109">You can use the HTTP Data Collector API to send data to Log Analytics from any client that can call a REST API.</span></span>  <span data-ttu-id="4cf19-110">Potrebbe trattarsi di un runbook in Automazione di Azure che raccoglie dati di gestione da Azure o da un altro sistema cloud o di un sistema di gestione alternativo che usa Log Analytics per consolidare e analizzare i dati.</span><span class="sxs-lookup"><span data-stu-id="4cf19-110">This might be a runbook in Azure Automation that collects management data from Azure or another cloud, or it might be an alternate management system that uses Log Analytics to consolidate and analyze data.</span></span>

<span data-ttu-id="4cf19-111">Tutti i dati nel repository di Log Analytics vengono archiviati come un record con un tipo specifico.</span><span class="sxs-lookup"><span data-stu-id="4cf19-111">All data in the Log Analytics repository is stored as a record with a particular record type.</span></span>  <span data-ttu-id="4cf19-112">I dati da inviare all'API dell'agente di raccolta dati HTTP devono essere formattati come più record in JSON.</span><span class="sxs-lookup"><span data-stu-id="4cf19-112">You format your data to send to the HTTP Data Collector API as multiple records in JSON.</span></span>  <span data-ttu-id="4cf19-113">Quando si inviano i dati, nel repository viene creato un record singolo per ogni record presente nel payload della richiesta.</span><span class="sxs-lookup"><span data-stu-id="4cf19-113">When you submit the data, an individual record is created in the repository for each record in the request payload.</span></span>


![Panoramica dell'agente di raccolta dati HTTP](media/log-analytics-data-collector-api/overview.png)



## <a name="create-a-request"></a><span data-ttu-id="4cf19-115">Creare una richiesta</span><span class="sxs-lookup"><span data-stu-id="4cf19-115">Create a request</span></span>
<span data-ttu-id="4cf19-116">Per usare l'API dell'agente di raccolta dati HTTP, creare una richiesta POST che include i dati da inviare in formato JSON (JavaScript Object Notation).</span><span class="sxs-lookup"><span data-stu-id="4cf19-116">To use the HTTP Data Collector API, you create a POST request that includes the data to send in JavaScript Object Notation (JSON).</span></span>  <span data-ttu-id="4cf19-117">Le tre tabelle successive indicano gli attributi necessari per ogni richiesta.</span><span class="sxs-lookup"><span data-stu-id="4cf19-117">The next three tables list the attributes that are required for each request.</span></span> <span data-ttu-id="4cf19-118">Ogni attributo viene descritto con maggiori dettagli più avanti nell'articolo.</span><span class="sxs-lookup"><span data-stu-id="4cf19-118">We describe each attribute in more detail later in the article.</span></span>

### <a name="request-uri"></a><span data-ttu-id="4cf19-119">URI della richiesta</span><span class="sxs-lookup"><span data-stu-id="4cf19-119">Request URI</span></span>
| <span data-ttu-id="4cf19-120">Attributo</span><span class="sxs-lookup"><span data-stu-id="4cf19-120">Attribute</span></span> | <span data-ttu-id="4cf19-121">Proprietà</span><span class="sxs-lookup"><span data-stu-id="4cf19-121">Property</span></span> |
|:--- |:--- |
| <span data-ttu-id="4cf19-122">Metodo</span><span class="sxs-lookup"><span data-stu-id="4cf19-122">Method</span></span> |<span data-ttu-id="4cf19-123">POST</span><span class="sxs-lookup"><span data-stu-id="4cf19-123">POST</span></span> |
| <span data-ttu-id="4cf19-124">URI</span><span class="sxs-lookup"><span data-stu-id="4cf19-124">URI</span></span> |<span data-ttu-id="4cf19-125">https://\<IdCliente\>.ods.opinsights.azure.com/api/logs?api-version=2016-04-01</span><span class="sxs-lookup"><span data-stu-id="4cf19-125">https://\<CustomerId\>.ods.opinsights.azure.com/api/logs?api-version=2016-04-01</span></span> |
| <span data-ttu-id="4cf19-126">Tipo di contenuto</span><span class="sxs-lookup"><span data-stu-id="4cf19-126">Content type</span></span> |<span data-ttu-id="4cf19-127">application/json</span><span class="sxs-lookup"><span data-stu-id="4cf19-127">application/json</span></span> |

### <a name="request-uri-parameters"></a><span data-ttu-id="4cf19-128">Parametri URI della richiesta</span><span class="sxs-lookup"><span data-stu-id="4cf19-128">Request URI parameters</span></span>
| <span data-ttu-id="4cf19-129">Parametro</span><span class="sxs-lookup"><span data-stu-id="4cf19-129">Parameter</span></span> | <span data-ttu-id="4cf19-130">Description</span><span class="sxs-lookup"><span data-stu-id="4cf19-130">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="4cf19-131">CustomerID</span><span class="sxs-lookup"><span data-stu-id="4cf19-131">CustomerID</span></span> |<span data-ttu-id="4cf19-132">Identificatore univoco dell'area di lavoro di Microsoft Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="4cf19-132">The unique identifier for the Microsoft Operations Management Suite workspace.</span></span> |
| <span data-ttu-id="4cf19-133">Risorsa</span><span class="sxs-lookup"><span data-stu-id="4cf19-133">Resource</span></span> |<span data-ttu-id="4cf19-134">Nome della risorsa API: /api/logs.</span><span class="sxs-lookup"><span data-stu-id="4cf19-134">The API resource name: /api/logs.</span></span> |
| <span data-ttu-id="4cf19-135">Versione dell'API</span><span class="sxs-lookup"><span data-stu-id="4cf19-135">API Version</span></span> |<span data-ttu-id="4cf19-136">Versione dell'API da usare con questa richiesta.</span><span class="sxs-lookup"><span data-stu-id="4cf19-136">The version of the API to use with this request.</span></span> <span data-ttu-id="4cf19-137">La versione attuale è 2016-04-01.</span><span class="sxs-lookup"><span data-stu-id="4cf19-137">Currently, it's 2016-04-01.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="4cf19-138">Intestazioni della richiesta</span><span class="sxs-lookup"><span data-stu-id="4cf19-138">Request headers</span></span>
| <span data-ttu-id="4cf19-139">Intestazione</span><span class="sxs-lookup"><span data-stu-id="4cf19-139">Header</span></span> | <span data-ttu-id="4cf19-140">Descrizione</span><span class="sxs-lookup"><span data-stu-id="4cf19-140">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="4cf19-141">Authorization</span><span class="sxs-lookup"><span data-stu-id="4cf19-141">Authorization</span></span> |<span data-ttu-id="4cf19-142">Firma di autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="4cf19-142">The authorization signature.</span></span> <span data-ttu-id="4cf19-143">Più avanti nell'articolo sono disponibili informazioni sulla creazione di un'intestazione HMAC-SHA256.</span><span class="sxs-lookup"><span data-stu-id="4cf19-143">Later in the article, you can read about how to create an HMAC-SHA256 header.</span></span> |
| <span data-ttu-id="4cf19-144">Log-Type</span><span class="sxs-lookup"><span data-stu-id="4cf19-144">Log-Type</span></span> |<span data-ttu-id="4cf19-145">Specificare il tipo di record dei dati inviati.</span><span class="sxs-lookup"><span data-stu-id="4cf19-145">Specify the record type of the data that is being submitted.</span></span> <span data-ttu-id="4cf19-146">Il tipo di log supporta attualmente solo caratteri alfabetici.</span><span class="sxs-lookup"><span data-stu-id="4cf19-146">Currently, the log type supports only alpha characters.</span></span> <span data-ttu-id="4cf19-147">Non supporta valori numerici o caratteri speciali.</span><span class="sxs-lookup"><span data-stu-id="4cf19-147">It does not support numerics or special characters.</span></span> |
| <span data-ttu-id="4cf19-148">x-ms-date</span><span class="sxs-lookup"><span data-stu-id="4cf19-148">x-ms-date</span></span> |<span data-ttu-id="4cf19-149">Data di elaborazione della richiesta, in formato RFC 1123.</span><span class="sxs-lookup"><span data-stu-id="4cf19-149">The date that the request was processed, in RFC 1123 format.</span></span> |
| <span data-ttu-id="4cf19-150">time-generated-field</span><span class="sxs-lookup"><span data-stu-id="4cf19-150">time-generated-field</span></span> |<span data-ttu-id="4cf19-151">Nome di un campo nei dati che contiene il timestamp dell'elemento di dati.</span><span class="sxs-lookup"><span data-stu-id="4cf19-151">The name of a field in the data that contains the timestamp of the data item.</span></span> <span data-ttu-id="4cf19-152">Se si specifica un campo, il relativo contenuto verrà usato per **TimeGenerated**.</span><span class="sxs-lookup"><span data-stu-id="4cf19-152">If you specify a field then its contents are used for **TimeGenerated**.</span></span> <span data-ttu-id="4cf19-153">Se questo campo non è specificato, il valore predefinito di **TimeGenerated** sarà la data/ora di inserimento del messaggio.</span><span class="sxs-lookup"><span data-stu-id="4cf19-153">If this field isn’t specified, the default for **TimeGenerated** is the time that the message is ingested.</span></span> <span data-ttu-id="4cf19-154">Il contenuto del campo del messaggio deve seguire il formato ISO 8601 AAAA-MM-GGThh:mm:ssZ.</span><span class="sxs-lookup"><span data-stu-id="4cf19-154">The contents of the message field should follow the ISO 8601 format YYYY-MM-DDThh:mm:ssZ.</span></span> |

## <a name="authorization"></a><span data-ttu-id="4cf19-155">Authorization</span><span class="sxs-lookup"><span data-stu-id="4cf19-155">Authorization</span></span>
<span data-ttu-id="4cf19-156">Qualsiasi richiesta inviata all'API di raccolta dati HTTP di Log Analytics deve includere l'intestazione dell'autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="4cf19-156">Any request to the Log Analytics HTTP Data Collector API must include an authorization header.</span></span> <span data-ttu-id="4cf19-157">Per autenticare una richiesta è necessario firmarla con la chiave primaria o secondaria dell'area di lavoro che effettua la richiesta.</span><span class="sxs-lookup"><span data-stu-id="4cf19-157">To authenticate a request, you must sign the request with either the primary or the secondary key for the workspace that is making the request.</span></span> <span data-ttu-id="4cf19-158">Passare quindi la firma come parte della richiesta.</span><span class="sxs-lookup"><span data-stu-id="4cf19-158">Then, pass that signature as part of the request.</span></span>   

<span data-ttu-id="4cf19-159">Il formato dell'intestazione dell'autorizzazione è il seguente:</span><span class="sxs-lookup"><span data-stu-id="4cf19-159">Here's the format for the authorization header:</span></span>

```
Authorization: SharedKey <WorkspaceID>:<Signature>
```

<span data-ttu-id="4cf19-160">*WorkspaceID* è l'identificatore univoco dell'area di lavoro di Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="4cf19-160">*WorkspaceID* is the unique identifier for the Operations Management Suite workspace.</span></span> <span data-ttu-id="4cf19-161">*Signature* è un codice [HMAC](https://msdn.microsoft.com/library/system.security.cryptography.hmacsha256.aspx) (Hash-based Message Authentication Code) che viene creato dalla richiesta e quindi calcolato con l'[algoritmo SHA256](https://msdn.microsoft.com/library/system.security.cryptography.sha256.aspx).</span><span class="sxs-lookup"><span data-stu-id="4cf19-161">*Signature* is a [Hash-based Message Authentication Code (HMAC)](https://msdn.microsoft.com/library/system.security.cryptography.hmacsha256.aspx) that is constructed from the request and then computed by using the [SHA256 algorithm](https://msdn.microsoft.com/library/system.security.cryptography.sha256.aspx).</span></span> <span data-ttu-id="4cf19-162">Viene quindi codificato con la codifica Base64.</span><span class="sxs-lookup"><span data-stu-id="4cf19-162">Then, you encode it by using Base64 encoding.</span></span>

<span data-ttu-id="4cf19-163">Usare questo formato per codificare la stringa di firma **SharedKey**:</span><span class="sxs-lookup"><span data-stu-id="4cf19-163">Use this format to encode the **SharedKey** signature string:</span></span>

```
StringToSign = VERB + "\n" +
                  Content-Length + "\n" +
               Content-Type + "\n" +
                  x-ms-date + "\n" +
                  "/api/logs";
```

<span data-ttu-id="4cf19-164">Di seguito è riportato un esempio di stringa della firma:</span><span class="sxs-lookup"><span data-stu-id="4cf19-164">Here's an example of a signature string:</span></span>

```
POST\n1024\napplication/json\nx-ms-date:Mon, 04 Apr 2016 08:00:00 GMT\n/api/logs
```

<span data-ttu-id="4cf19-165">La stringa della firma deve essere codificata usando l'algoritmo HMAC-SHA256 sulla stringa con codifica UTF-8. Il risultato deve essere quindi codificato in Base64.</span><span class="sxs-lookup"><span data-stu-id="4cf19-165">When you have the signature string, encode it by using the HMAC-SHA256 algorithm on the UTF-8-encoded string, and then encode the result as Base64.</span></span> <span data-ttu-id="4cf19-166">Usare il formato seguente:</span><span class="sxs-lookup"><span data-stu-id="4cf19-166">Use this format:</span></span>

```
Signature=Base64(HMAC-SHA256(UTF8(StringToSign)))
```

<span data-ttu-id="4cf19-167">Gli esempi nelle sezioni successive indicano il codice di esempio per creare l'intestazione dell'autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="4cf19-167">The samples in the next sections have sample code to help you create an authorization header.</span></span>

## <a name="request-body"></a><span data-ttu-id="4cf19-168">Corpo della richiesta</span><span class="sxs-lookup"><span data-stu-id="4cf19-168">Request body</span></span>
<span data-ttu-id="4cf19-169">Il corpo del messaggio deve essere in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="4cf19-169">The body of the message must be in JSON.</span></span> <span data-ttu-id="4cf19-170">Deve includere uno o più record con coppie di nome e valore di proprietà nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="4cf19-170">It must include one or more records with the property name and value pairs in this format:</span></span>

```
{
"property1": "value1",
" property 2": "value2"
" property 3": "value3",
" property 4": "value4"
}
```

<span data-ttu-id="4cf19-171">È possibile creare batch di più record in una singola richiesta usando il formato seguente.</span><span class="sxs-lookup"><span data-stu-id="4cf19-171">You can batch multiple records together in a single request by using the following format.</span></span> <span data-ttu-id="4cf19-172">Tutti i record devono essere dello stesso tipo.</span><span class="sxs-lookup"><span data-stu-id="4cf19-172">All the records must be the same record type.</span></span>

```
{
"property1": "value1",
" property 2": "value2"
" property 3": "value3",
" property 4": "value4"
},
{
"property1": "value1",
" property 2": "value2"
" property 3": "value3",
" property 4": "value4"
}
```

## <a name="record-type-and-properties"></a><span data-ttu-id="4cf19-173">Proprietà e tipo di record</span><span class="sxs-lookup"><span data-stu-id="4cf19-173">Record type and properties</span></span>
<span data-ttu-id="4cf19-174">Quando si inviano dati con l'API di raccolta dati HTTP di Log Analytics si definisce un tipo di record personalizzato.</span><span class="sxs-lookup"><span data-stu-id="4cf19-174">You define a custom record type when you submit data through the Log Analytics HTTP Data Collector API.</span></span> <span data-ttu-id="4cf19-175">È attualmente possibile scrivere dati nei tipi di record esistenti creati da altri tipi di dati e soluzioni.</span><span class="sxs-lookup"><span data-stu-id="4cf19-175">Currently, you can't write data to existing record types that were created by other data types and solutions.</span></span> <span data-ttu-id="4cf19-176">Log Analytics legge i dati in ingresso e quindi crea le proprietà che corrispondono ai tipi di dati dei valori immessi.</span><span class="sxs-lookup"><span data-stu-id="4cf19-176">Log Analytics reads the incoming data and then creates properties that match the data types of the values that you enter.</span></span>

<span data-ttu-id="4cf19-177">Ogni richiesta all'API di Log Analytics deve includere un'intestazione **Log-Type** con il nome del tipo di record.</span><span class="sxs-lookup"><span data-stu-id="4cf19-177">Each request to the Log Analytics API must include a **Log-Type** header with the name for the record type.</span></span> <span data-ttu-id="4cf19-178">Il suffisso **_CL** viene aggiunto automaticamente al nome immesso per distinguerlo da altri tipi di log come log personalizzato.</span><span class="sxs-lookup"><span data-stu-id="4cf19-178">The suffix **_CL** is automatically appended to the name you enter to distinguish it from other log types as a custom log.</span></span> <span data-ttu-id="4cf19-179">Se ad esempio si immette il nome **MyNewRecordType**, Log Analytics crea un record di tipo **MyNewRecordType_CL**.</span><span class="sxs-lookup"><span data-stu-id="4cf19-179">For example, if you enter the name **MyNewRecordType**, Log Analytics creates a record with the type **MyNewRecordType_CL**.</span></span> <span data-ttu-id="4cf19-180">È così possibile evitare conflitti tra i nomi dei tipi creati dall'utente e i nomi forniti nelle soluzioni Microsoft correnti o future.</span><span class="sxs-lookup"><span data-stu-id="4cf19-180">This helps ensure that there are no conflicts between user-created type names and those shipped in current or future Microsoft solutions.</span></span>

<span data-ttu-id="4cf19-181">Per identificare il tipo di dati di una proprietà, Log Analytics aggiunge un suffisso al nome della proprietà.</span><span class="sxs-lookup"><span data-stu-id="4cf19-181">To identify a property's data type, Log Analytics adds a suffix to the property name.</span></span> <span data-ttu-id="4cf19-182">Una proprietà con un valore null non viene inclusa in tale record.</span><span class="sxs-lookup"><span data-stu-id="4cf19-182">If a property contains a null value, the property is not included in that record.</span></span> <span data-ttu-id="4cf19-183">Questa tabella elenca il tipo di dati proprietà e il suffisso corrispondente:</span><span class="sxs-lookup"><span data-stu-id="4cf19-183">This table lists the property data type and corresponding suffix:</span></span>

| <span data-ttu-id="4cf19-184">Tipo di dati proprietà</span><span class="sxs-lookup"><span data-stu-id="4cf19-184">Property data type</span></span> | <span data-ttu-id="4cf19-185">Suffisso</span><span class="sxs-lookup"><span data-stu-id="4cf19-185">Suffix</span></span> |
|:--- |:--- |
| <span data-ttu-id="4cf19-186">String</span><span class="sxs-lookup"><span data-stu-id="4cf19-186">String</span></span> |<span data-ttu-id="4cf19-187">_s</span><span class="sxs-lookup"><span data-stu-id="4cf19-187">_s</span></span> |
| <span data-ttu-id="4cf19-188">Boolean</span><span class="sxs-lookup"><span data-stu-id="4cf19-188">Boolean</span></span> |<span data-ttu-id="4cf19-189">_b</span><span class="sxs-lookup"><span data-stu-id="4cf19-189">_b</span></span> |
| <span data-ttu-id="4cf19-190">Double</span><span class="sxs-lookup"><span data-stu-id="4cf19-190">Double</span></span> |<span data-ttu-id="4cf19-191">_d</span><span class="sxs-lookup"><span data-stu-id="4cf19-191">_d</span></span> |
| <span data-ttu-id="4cf19-192">Data/ora</span><span class="sxs-lookup"><span data-stu-id="4cf19-192">Date/time</span></span> |<span data-ttu-id="4cf19-193">_t</span><span class="sxs-lookup"><span data-stu-id="4cf19-193">_t</span></span> |
| <span data-ttu-id="4cf19-194">GUID</span><span class="sxs-lookup"><span data-stu-id="4cf19-194">GUID</span></span> |<span data-ttu-id="4cf19-195">_g</span><span class="sxs-lookup"><span data-stu-id="4cf19-195">_g</span></span> |

<span data-ttu-id="4cf19-196">Il tipo di dati usato da Log Analytics per ogni proprietà dipende dall'eventuale esistenza di un tipo di record per il nuovo record.</span><span class="sxs-lookup"><span data-stu-id="4cf19-196">The data type that Log Analytics uses for each property depends on whether the record type for the new record already exists.</span></span>

* <span data-ttu-id="4cf19-197">Se il tipo di record non esiste, Log Analytics ne creerà uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="4cf19-197">If the record type does not exist, Log Analytics creates a new one.</span></span> <span data-ttu-id="4cf19-198">Log Analytics usa l'inferenza del tipo JSON per determinare il tipo di dati per ogni proprietà del nuovo record.</span><span class="sxs-lookup"><span data-stu-id="4cf19-198">Log Analytics uses the JSON type inference to determine the data type for each property for the new record.</span></span>
* <span data-ttu-id="4cf19-199">Se il tipo di record esiste, Log Analytics prova a creare un nuovo record in base alle proprietà esistenti.</span><span class="sxs-lookup"><span data-stu-id="4cf19-199">If the record type does exist, Log Analytics attempts to create a new record based on existing properties.</span></span> <span data-ttu-id="4cf19-200">Se il tipo di dati di una proprietà nel nuovo record non corrisponde e non può essere convertito nel tipo esistente, oppure se il record include una proprietà che non esiste, Log Analytics crea una nuova proprietà con il suffisso pertinente.</span><span class="sxs-lookup"><span data-stu-id="4cf19-200">If the data type for a property in the new record doesn’t match and can’t be converted to the existing type, or if the record includes a property that doesn’t exist, Log Analytics creates a new property that has the relevant suffix.</span></span>

<span data-ttu-id="4cf19-201">Questa voce di invio creerà ad esempio un record con tre proprietà, **number_d**, **boolean_b** e **string_s**:</span><span class="sxs-lookup"><span data-stu-id="4cf19-201">For example, this submission entry would create a record with three properties, **number_d**, **boolean_b**, and **string_s**:</span></span>

![Esempio di record 1](media/log-analytics-data-collector-api/record-01.png)

<span data-ttu-id="4cf19-203">Inviando la voce seguente, con tutti i valori formattati come stringhe, le proprietà non cambieranno.</span><span class="sxs-lookup"><span data-stu-id="4cf19-203">If you then submitted this next entry, with all values formatted as strings, the properties would not change.</span></span> <span data-ttu-id="4cf19-204">Questi valori possono essere convertiti in tipi di dati esistenti:</span><span class="sxs-lookup"><span data-stu-id="4cf19-204">These values can be converted to existing data types:</span></span>

![Esempio di record 2](media/log-analytics-data-collector-api/record-02.png)

<span data-ttu-id="4cf19-206">Con l'invio seguente, tuttavia, Log Analytics creerebbe le nuove proprietà **boolean_d** e **string_d**.</span><span class="sxs-lookup"><span data-stu-id="4cf19-206">But, if you then made this next submission, Log Analytics would create the new properties **boolean_d** and **string_d**.</span></span> <span data-ttu-id="4cf19-207">Questi valori non possono essere convertiti:</span><span class="sxs-lookup"><span data-stu-id="4cf19-207">These values can't be converted:</span></span>

![Esempio di record 3](media/log-analytics-data-collector-api/record-03.png)

<span data-ttu-id="4cf19-209">Inviando la voce seguente, prima della creazione del tipo di record Log Analytics creerebbe un record con tre proprietà, **number_s**, **boolean_s** e **string_s**.</span><span class="sxs-lookup"><span data-stu-id="4cf19-209">If you then submitted the following entry, before the record type was created, Log Analytics would create a record with three properties, **number_s**, **boolean_s**, and **string_s**.</span></span> <span data-ttu-id="4cf19-210">In questa voce, ognuno dei valori iniziali viene formattato come stringa:</span><span class="sxs-lookup"><span data-stu-id="4cf19-210">In this entry, each of the initial values is formatted as a string:</span></span>

![Esempio di record 4](media/log-analytics-data-collector-api/record-04.png)

## <a name="data-limits"></a><span data-ttu-id="4cf19-212">Limiti dei dati</span><span class="sxs-lookup"><span data-stu-id="4cf19-212">Data limits</span></span>
<span data-ttu-id="4cf19-213">Esistono alcune limitazioni riguardo ai dati pubblicati nell'API per la raccolta dei dati di Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="4cf19-213">There are some constraints around the data posted to the Log Analytics Data collection API.</span></span>

* <span data-ttu-id="4cf19-214">Limite di 30 MB per post nell'API per la raccolta dei dati di Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="4cf19-214">Maximum of 30 MB per post to Log Analytics Data Collector API.</span></span> <span data-ttu-id="4cf19-215">Questo limite riguarda le dimensioni di ogni messaggio.</span><span class="sxs-lookup"><span data-stu-id="4cf19-215">This is a size limit for a single post.</span></span> <span data-ttu-id="4cf19-216">Se i dati di un singolo post superano i 30 MB, è necessario suddividerli in blocchi di dimensioni inferiori, che andranno inviati contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="4cf19-216">If the data from a single post that exceeds 30 MB, you should split the data up to smaller sized chunks and send them concurrently.</span></span>
* <span data-ttu-id="4cf19-217">Limite di 32 KB per i valori dei campi.</span><span class="sxs-lookup"><span data-stu-id="4cf19-217">Maximum of 32 KB limit for field values.</span></span> <span data-ttu-id="4cf19-218">Se il valore di un campo è superiore a 32 KB, i dati verranno troncati.</span><span class="sxs-lookup"><span data-stu-id="4cf19-218">If the field value is greater than 32 KB, the data will be truncated.</span></span>
* <span data-ttu-id="4cf19-219">Il numero massimo di campi consigliato per un determinato tipo è 50.</span><span class="sxs-lookup"><span data-stu-id="4cf19-219">Recommended maximum number of fields for a given type is 50.</span></span> <span data-ttu-id="4cf19-220">Si tratta di un limite pratico dal punto di vista dell'usabilità e dell'esperienza di ricerca.</span><span class="sxs-lookup"><span data-stu-id="4cf19-220">This is a practical limit from a usability and search experience perspective.</span></span>  

## <a name="return-codes"></a><span data-ttu-id="4cf19-221">Codici restituiti</span><span class="sxs-lookup"><span data-stu-id="4cf19-221">Return codes</span></span>
<span data-ttu-id="4cf19-222">Il codice di stato HTTP 200 indica che è stata ricevuta la richiesta per l'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="4cf19-222">The HTTP status code 200 means that the request has been received for processing.</span></span> <span data-ttu-id="4cf19-223">L'operazione è stata completata correttamente.</span><span class="sxs-lookup"><span data-stu-id="4cf19-223">This indicates that the operation completed successfully.</span></span>

<span data-ttu-id="4cf19-224">Questa tabella elenca il set completo di codici di stato che il servizio può restituire:</span><span class="sxs-lookup"><span data-stu-id="4cf19-224">This table lists the complete set of status codes that the service might return:</span></span>

| <span data-ttu-id="4cf19-225">Codice</span><span class="sxs-lookup"><span data-stu-id="4cf19-225">Code</span></span> | <span data-ttu-id="4cf19-226">Stato</span><span class="sxs-lookup"><span data-stu-id="4cf19-226">Status</span></span> | <span data-ttu-id="4cf19-227">Codice di errore</span><span class="sxs-lookup"><span data-stu-id="4cf19-227">Error code</span></span> | <span data-ttu-id="4cf19-228">Descrizione</span><span class="sxs-lookup"><span data-stu-id="4cf19-228">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="4cf19-229">200</span><span class="sxs-lookup"><span data-stu-id="4cf19-229">200</span></span> |<span data-ttu-id="4cf19-230">OK</span><span class="sxs-lookup"><span data-stu-id="4cf19-230">OK</span></span> | |<span data-ttu-id="4cf19-231">La richiesta è stata accettata.</span><span class="sxs-lookup"><span data-stu-id="4cf19-231">The request was successfully accepted.</span></span> |
| <span data-ttu-id="4cf19-232">400</span><span class="sxs-lookup"><span data-stu-id="4cf19-232">400</span></span> |<span data-ttu-id="4cf19-233">Richiesta non valida</span><span class="sxs-lookup"><span data-stu-id="4cf19-233">Bad request</span></span> |<span data-ttu-id="4cf19-234">InactiveCustomer</span><span class="sxs-lookup"><span data-stu-id="4cf19-234">InactiveCustomer</span></span> |<span data-ttu-id="4cf19-235">L'area di lavoro è stata chiusa.</span><span class="sxs-lookup"><span data-stu-id="4cf19-235">The workspace has been closed.</span></span> |
| <span data-ttu-id="4cf19-236">400</span><span class="sxs-lookup"><span data-stu-id="4cf19-236">400</span></span> |<span data-ttu-id="4cf19-237">Richiesta non valida</span><span class="sxs-lookup"><span data-stu-id="4cf19-237">Bad request</span></span> |<span data-ttu-id="4cf19-238">InvalidApiVersion</span><span class="sxs-lookup"><span data-stu-id="4cf19-238">InvalidApiVersion</span></span> |<span data-ttu-id="4cf19-239">La versione API specificata non è stata riconosciuta dal servizio.</span><span class="sxs-lookup"><span data-stu-id="4cf19-239">The API version that you specified was not recognized by the service.</span></span> |
| <span data-ttu-id="4cf19-240">400</span><span class="sxs-lookup"><span data-stu-id="4cf19-240">400</span></span> |<span data-ttu-id="4cf19-241">Richiesta non valida</span><span class="sxs-lookup"><span data-stu-id="4cf19-241">Bad request</span></span> |<span data-ttu-id="4cf19-242">InvalidCustomerId</span><span class="sxs-lookup"><span data-stu-id="4cf19-242">InvalidCustomerId</span></span> |<span data-ttu-id="4cf19-243">L'ID area di lavoro specificato non è valido.</span><span class="sxs-lookup"><span data-stu-id="4cf19-243">The workspace ID specified is invalid.</span></span> |
| <span data-ttu-id="4cf19-244">400</span><span class="sxs-lookup"><span data-stu-id="4cf19-244">400</span></span> |<span data-ttu-id="4cf19-245">Richiesta non valida</span><span class="sxs-lookup"><span data-stu-id="4cf19-245">Bad request</span></span> |<span data-ttu-id="4cf19-246">InvalidDataFormat</span><span class="sxs-lookup"><span data-stu-id="4cf19-246">InvalidDataFormat</span></span> |<span data-ttu-id="4cf19-247">È stata inviato JSON non valido.</span><span class="sxs-lookup"><span data-stu-id="4cf19-247">Invalid JSON was submitted.</span></span> <span data-ttu-id="4cf19-248">Il corpo della risposta può contenere altre informazioni sulla risoluzione dell'errore.</span><span class="sxs-lookup"><span data-stu-id="4cf19-248">The response body might contain more information about how to resolve the error.</span></span> |
| <span data-ttu-id="4cf19-249">400</span><span class="sxs-lookup"><span data-stu-id="4cf19-249">400</span></span> |<span data-ttu-id="4cf19-250">Richiesta non valida</span><span class="sxs-lookup"><span data-stu-id="4cf19-250">Bad request</span></span> |<span data-ttu-id="4cf19-251">InvalidLogType</span><span class="sxs-lookup"><span data-stu-id="4cf19-251">InvalidLogType</span></span> |<span data-ttu-id="4cf19-252">Il tipo di log specificato conteneva caratteri speciali o numeri.</span><span class="sxs-lookup"><span data-stu-id="4cf19-252">The log type specified contained special characters or numerics.</span></span> |
| <span data-ttu-id="4cf19-253">400</span><span class="sxs-lookup"><span data-stu-id="4cf19-253">400</span></span> |<span data-ttu-id="4cf19-254">Richiesta non valida</span><span class="sxs-lookup"><span data-stu-id="4cf19-254">Bad request</span></span> |<span data-ttu-id="4cf19-255">MissingApiVersion</span><span class="sxs-lookup"><span data-stu-id="4cf19-255">MissingApiVersion</span></span> |<span data-ttu-id="4cf19-256">La versione API non è stata specificata.</span><span class="sxs-lookup"><span data-stu-id="4cf19-256">The API version wasn’t specified.</span></span> |
| <span data-ttu-id="4cf19-257">400</span><span class="sxs-lookup"><span data-stu-id="4cf19-257">400</span></span> |<span data-ttu-id="4cf19-258">Richiesta non valida</span><span class="sxs-lookup"><span data-stu-id="4cf19-258">Bad request</span></span> |<span data-ttu-id="4cf19-259">MissingContentType</span><span class="sxs-lookup"><span data-stu-id="4cf19-259">MissingContentType</span></span> |<span data-ttu-id="4cf19-260">Il tipo di contenuto non è stato specificato.</span><span class="sxs-lookup"><span data-stu-id="4cf19-260">The content type wasn’t specified.</span></span> |
| <span data-ttu-id="4cf19-261">400</span><span class="sxs-lookup"><span data-stu-id="4cf19-261">400</span></span> |<span data-ttu-id="4cf19-262">Richiesta non valida</span><span class="sxs-lookup"><span data-stu-id="4cf19-262">Bad request</span></span> |<span data-ttu-id="4cf19-263">MissingLogType</span><span class="sxs-lookup"><span data-stu-id="4cf19-263">MissingLogType</span></span> |<span data-ttu-id="4cf19-264">Il tipo di log dei valori non è stato specificato.</span><span class="sxs-lookup"><span data-stu-id="4cf19-264">The required value log type wasn’t specified.</span></span> |
| <span data-ttu-id="4cf19-265">400</span><span class="sxs-lookup"><span data-stu-id="4cf19-265">400</span></span> |<span data-ttu-id="4cf19-266">Richiesta non valida</span><span class="sxs-lookup"><span data-stu-id="4cf19-266">Bad request</span></span> |<span data-ttu-id="4cf19-267">UnsupportedContentType</span><span class="sxs-lookup"><span data-stu-id="4cf19-267">UnsupportedContentType</span></span> |<span data-ttu-id="4cf19-268">Il tipo di contenuto non è stato impostato su **application/json**.</span><span class="sxs-lookup"><span data-stu-id="4cf19-268">The content type was not set to **application/json**.</span></span> |
| <span data-ttu-id="4cf19-269">403</span><span class="sxs-lookup"><span data-stu-id="4cf19-269">403</span></span> |<span data-ttu-id="4cf19-270">Accesso negato</span><span class="sxs-lookup"><span data-stu-id="4cf19-270">Forbidden</span></span> |<span data-ttu-id="4cf19-271">InvalidAuthorization</span><span class="sxs-lookup"><span data-stu-id="4cf19-271">InvalidAuthorization</span></span> |<span data-ttu-id="4cf19-272">Il servizio non è riuscito ad autenticare la richiesta.</span><span class="sxs-lookup"><span data-stu-id="4cf19-272">The service failed to authenticate the request.</span></span> <span data-ttu-id="4cf19-273">Verificare che l'ID dell'area di lavoro e la chiave di connessione siano validi.</span><span class="sxs-lookup"><span data-stu-id="4cf19-273">Verify that the workspace ID and connection key are valid.</span></span> |
| <span data-ttu-id="4cf19-274">404</span><span class="sxs-lookup"><span data-stu-id="4cf19-274">404</span></span> |<span data-ttu-id="4cf19-275">Non trovato</span><span class="sxs-lookup"><span data-stu-id="4cf19-275">Not Found</span></span> | | <span data-ttu-id="4cf19-276">L'URL specificato non è corretto o la richiesta è di dimensioni eccessive.</span><span class="sxs-lookup"><span data-stu-id="4cf19-276">Either the URL provided is incorrect, or the request is too large.</span></span> |
| <span data-ttu-id="4cf19-277">429</span><span class="sxs-lookup"><span data-stu-id="4cf19-277">429</span></span> |<span data-ttu-id="4cf19-278">Troppe richieste</span><span class="sxs-lookup"><span data-stu-id="4cf19-278">Too Many Requests</span></span> | | <span data-ttu-id="4cf19-279">Il servizio sta ricevendo un elevato volume di dati dall'account.</span><span class="sxs-lookup"><span data-stu-id="4cf19-279">The service is experiencing a high volume of data from your account.</span></span> <span data-ttu-id="4cf19-280">Si prega di ripetere la richiesta più tardi.</span><span class="sxs-lookup"><span data-stu-id="4cf19-280">Please retry the request later.</span></span> |
| <span data-ttu-id="4cf19-281">500</span><span class="sxs-lookup"><span data-stu-id="4cf19-281">500</span></span> |<span data-ttu-id="4cf19-282">Internal Server Error</span><span class="sxs-lookup"><span data-stu-id="4cf19-282">Internal Server Error</span></span> |<span data-ttu-id="4cf19-283">UnspecifiedError</span><span class="sxs-lookup"><span data-stu-id="4cf19-283">UnspecifiedError</span></span> |<span data-ttu-id="4cf19-284">Errore interno del servizio.</span><span class="sxs-lookup"><span data-stu-id="4cf19-284">The service encountered an internal error.</span></span> <span data-ttu-id="4cf19-285">Si prega di ripetere la richiesta.</span><span class="sxs-lookup"><span data-stu-id="4cf19-285">Please retry the request.</span></span> |
| <span data-ttu-id="4cf19-286">503</span><span class="sxs-lookup"><span data-stu-id="4cf19-286">503</span></span> |<span data-ttu-id="4cf19-287">Servizio non disponibile</span><span class="sxs-lookup"><span data-stu-id="4cf19-287">Service Unavailable</span></span> |<span data-ttu-id="4cf19-288">ServiceUnavailable</span><span class="sxs-lookup"><span data-stu-id="4cf19-288">ServiceUnavailable</span></span> |<span data-ttu-id="4cf19-289">Il servizio non è attualmente disponibile per la ricezione delle richieste.</span><span class="sxs-lookup"><span data-stu-id="4cf19-289">The service currently is unavailable to receive requests.</span></span> <span data-ttu-id="4cf19-290">Si prega di ripetere la richiesta.</span><span class="sxs-lookup"><span data-stu-id="4cf19-290">Please retry your request.</span></span> |

## <a name="query-data"></a><span data-ttu-id="4cf19-291">Eseguire query sui dati</span><span class="sxs-lookup"><span data-stu-id="4cf19-291">Query data</span></span>
<span data-ttu-id="4cf19-292">Per eseguire query sui dati inviati dall'API di raccolta dati HTTP di Log Analytics, cercare i record con valore di **Type** uguale al valore **LogType** specificato, con l'aggiunta di **_CL**.</span><span class="sxs-lookup"><span data-stu-id="4cf19-292">To query data submitted by the Log Analytics HTTP Data Collector API, search for records with **Type** that is equal to the **LogType** value that you specified, appended with **_CL**.</span></span> <span data-ttu-id="4cf19-293">Usando ad esempio **MyCustomLog** verranno restituiti tutti i record con **Type=MyCustomLog_CL**.</span><span class="sxs-lookup"><span data-stu-id="4cf19-293">For example, if you used **MyCustomLog**, then you'd return all records with **Type=MyCustomLog_CL**.</span></span>

>[!NOTE]
> <span data-ttu-id="4cf19-294">Se l'area di lavoro è stata aggiornata al [nuovo linguaggio di query di Log Analytics](log-analytics-log-search-upgrade.md), la query precedente verrà sostituita dalla seguente.</span><span class="sxs-lookup"><span data-stu-id="4cf19-294">If your workspace has been upgraded to the [new Log Analytics query language](log-analytics-log-search-upgrade.md), then the above query would change to the following.</span></span>

> `MyCustomLog_CL`

## <a name="sample-requests"></a><span data-ttu-id="4cf19-295">Richieste di esempio</span><span class="sxs-lookup"><span data-stu-id="4cf19-295">Sample requests</span></span>
<span data-ttu-id="4cf19-296">Nelle sezioni successive sono disponibili esempi di come inviare dati all'API di raccolta dati HTTP di Log Analytics usando diversi linguaggi di programmazione.</span><span class="sxs-lookup"><span data-stu-id="4cf19-296">In the next sections, you'll find samples of how to submit data to the Log Analytics HTTP Data Collector API by using different programming languages.</span></span>

<span data-ttu-id="4cf19-297">Per ogni esempio, seguire questa procedura per impostare le variabili per l'intestazione dell'autorizzazione:</span><span class="sxs-lookup"><span data-stu-id="4cf19-297">For each sample, do these steps to set the variables for the authorization header:</span></span>

1. <span data-ttu-id="4cf19-298">Nel portale di Operations Management Suite selezionare il riquadro **Impostazioni** e quindi la scheda **Origini connesse**.</span><span class="sxs-lookup"><span data-stu-id="4cf19-298">In the Operations Management Suite portal, select the **Settings** tile, and then select the **Connected Sources** tab.</span></span>
2. <span data-ttu-id="4cf19-299">A destra di **ID area di lavoro** selezionare l'icona di copia e quindi incollare l'ID come valore della variabile **ID cliente**.</span><span class="sxs-lookup"><span data-stu-id="4cf19-299">To the right of **Workspace ID**, select the copy icon, and then paste the ID as the value of the **Customer ID** variable.</span></span>
3. <span data-ttu-id="4cf19-300">A destra di **Chiave primaria** selezionare l'icona di copia e quindi incollare l'ID come valore della variabile **Chiave condivisa**.</span><span class="sxs-lookup"><span data-stu-id="4cf19-300">To the right of **Primary Key**, select the copy icon, and then paste the ID as the value of the **Shared Key** variable.</span></span>

<span data-ttu-id="4cf19-301">In alternativa è possibile modificare le variabili per il tipo di log e i dati JSON.</span><span class="sxs-lookup"><span data-stu-id="4cf19-301">Alternatively, you can change the variables for the log type and JSON data.</span></span>

### <a name="powershell-sample"></a><span data-ttu-id="4cf19-302">Esempio PowerShell</span><span class="sxs-lookup"><span data-stu-id="4cf19-302">PowerShell sample</span></span>
```
# Replace with your Workspace ID
$CustomerId = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"  

# Replace with your Primary Key
$SharedKey = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"

# Specify the name of the record type that you'll be creating
$LogType = "MyRecordType"

# Specify a field with the created time for the records
$TimeStampField = "DateValue"


# Create two records with the same set of properties to create
$json = @"
[{  "StringValue": "MyString1",
    "NumberValue": 42,
    "BooleanValue": true,
    "DateValue": "2016-05-12T20:00:00.625Z",
    "GUIDValue": "9909ED01-A74C-4874-8ABF-D2678E3AE23D"
},
{   "StringValue": "MyString2",
    "NumberValue": 43,
    "BooleanValue": false,
    "DateValue": "2016-05-12T20:00:00.625Z",
    "GUIDValue": "8809ED01-A74C-4874-8ABF-D2678E3AE23D"
}]
"@

# Create the function to create the authorization signature
Function Build-Signature ($customerId, $sharedKey, $date, $contentLength, $method, $contentType, $resource)
{
    $xHeaders = "x-ms-date:" + $date
    $stringToHash = $method + "`n" + $contentLength + "`n" + $contentType + "`n" + $xHeaders + "`n" + $resource

    $bytesToHash = [Text.Encoding]::UTF8.GetBytes($stringToHash)
    $keyBytes = [Convert]::FromBase64String($sharedKey)

    $sha256 = New-Object System.Security.Cryptography.HMACSHA256
    $sha256.Key = $keyBytes
    $calculatedHash = $sha256.ComputeHash($bytesToHash)
    $encodedHash = [Convert]::ToBase64String($calculatedHash)
    $authorization = 'SharedKey {0}:{1}' -f $customerId,$encodedHash
    return $authorization
}


# Create the function to create and post the request
Function Post-OMSData($customerId, $sharedKey, $body, $logType)
{
    $method = "POST"
    $contentType = "application/json"
    $resource = "/api/logs"
    $rfc1123date = [DateTime]::UtcNow.ToString("r")
    $contentLength = $body.Length
    $signature = Build-Signature `
        -customerId $customerId `
        -sharedKey $sharedKey `
        -date $rfc1123date `
        -contentLength $contentLength `
        -fileName $fileName `
        -method $method `
        -contentType $contentType `
        -resource $resource
    $uri = "https://" + $customerId + ".ods.opinsights.azure.com" + $resource + "?api-version=2016-04-01"

    $headers = @{
        "Authorization" = $signature;
        "Log-Type" = $logType;
        "x-ms-date" = $rfc1123date;
        "time-generated-field" = $TimeStampField;
    }

    $response = Invoke-WebRequest -Uri $uri -Method $method -ContentType $contentType -Headers $headers -Body $body -UseBasicParsing
    return $response.StatusCode

}

# Submit the data to the API endpoint
Post-OMSData -customerId $customerId -sharedKey $sharedKey -body ([System.Text.Encoding]::UTF8.GetBytes($json)) -logType $logType  
```

### <a name="c-sample"></a><span data-ttu-id="4cf19-303">Esempio C#</span><span class="sxs-lookup"><span data-stu-id="4cf19-303">C# sample</span></span>
```
using System;
using System.Net;
using System.Net.Http;
using System.Net.Http.Headers;
using System.Security.Cryptography;
using System.Text;
using System.Threading.Tasks;

namespace OIAPIExample
{
    class ApiExample
    {
        // An example JSON object, with key/value pairs
        static string json = @"[{""DemoField1"":""DemoValue1"",""DemoField2"":""DemoValue2""},{""DemoField3"":""DemoValue3"",""DemoField4"":""DemoValue4""}]";

        // Update customerId to your Operations Management Suite workspace ID
        static string customerId = "xxxxxxxx-xxx-xxx-xxx-xxxxxxxxxxxx";

        // For sharedKey, use either the primary or the secondary Connected Sources client authentication key   
        static string sharedKey = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx";

        // LogName is name of the event type that is being submitted to Log Analytics
        static string LogName = "DemoExample";

        // You can use an optional field to specify the timestamp from the data. If the time field is not specified, Log Analytics assumes the time is the message ingestion time
        static string TimeStampField = "";

        static void Main()
        {
            // Create a hash for the API signature
            var datestring = DateTime.UtcNow.ToString("r");
            string stringToHash = "POST\n" + json.Length + "\napplication/json\n" + "x-ms-date:" + datestring + "\n/api/logs";
            string hashedString = BuildSignature(stringToHash, sharedKey);
            string signature = "SharedKey " + customerId + ":" + hashedString;

            PostData(signature, datestring, json);
        }

        // Build the API signature
        public static string BuildSignature(string message, string secret)
        {
            var encoding = new System.Text.ASCIIEncoding();
            byte[] keyByte = Convert.FromBase64String(secret);
            byte[] messageBytes = encoding.GetBytes(message);
            using (var hmacsha256 = new HMACSHA256(keyByte))
            {
                byte[] hash = hmacsha256.ComputeHash(messageBytes);
                return Convert.ToBase64String(hash);
            }
        }

        // Send a request to the POST API endpoint
        public static void PostData(string signature, string date, string json)
        {
            try
            {
                string url = "https://" + customerId + ".ods.opinsights.azure.com/api/logs?api-version=2016-04-01";

                System.Net.Http.HttpClient client = new System.Net.Http.HttpClient();
                client.DefaultRequestHeaders.Add("Accept", "application/json");
                client.DefaultRequestHeaders.Add("Log-Type", LogName);
                client.DefaultRequestHeaders.Add("Authorization", signature);
                client.DefaultRequestHeaders.Add("x-ms-date", date);
                client.DefaultRequestHeaders.Add("time-generated-field", TimeStampField);

                System.Net.Http.HttpContent httpContent = new StringContent(json, Encoding.UTF8);
                httpContent.Headers.ContentType = new MediaTypeHeaderValue("application/json");
                Task<System.Net.Http.HttpResponseMessage> response = client.PostAsync(new Uri(url), httpContent);

                System.Net.Http.HttpContent responseContent = response.Result.Content;
                string result = responseContent.ReadAsStringAsync().Result;
                Console.WriteLine("Return Result: " + result);
            }
            catch (Exception excep)
            {
                Console.WriteLine("API Post Exception: " + excep.Message);
            }
        }
    }
}

```

### <a name="python-sample"></a><span data-ttu-id="4cf19-304">Esempio Python</span><span class="sxs-lookup"><span data-stu-id="4cf19-304">Python sample</span></span>
```
import json
import requests
import datetime
import hashlib
import hmac
import base64

# Update the customer ID to your Operations Management Suite workspace ID
customer_id = 'xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx'

# For the shared key, use either the primary or the secondary Connected Sources client authentication key   
shared_key = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"

# The log type is the name of the event that is being submitted
log_type = 'WebMonitorTest'

# An example JSON web monitor object
json_data = [{
   "slot_ID": 12345,
    "ID": "5cdad72f-c848-4df0-8aaa-ffe033e75d57",
    "availability_Value": 100,
    "performance_Value": 6.954,
    "measurement_Name": "last_one_hour",
    "duration": 3600,
    "warning_Threshold": 0,
    "critical_Threshold": 0,
    "IsActive": "true"
},
{   
    "slot_ID": 67890,
    "ID": "b6bee458-fb65-492e-996d-61c4d7fbb942",
    "availability_Value": 100,
    "performance_Value": 3.379,
    "measurement_Name": "last_one_hour",
    "duration": 3600,
    "warning_Threshold": 0,
    "critical_Threshold": 0,
    "IsActive": "false"
}]
body = json.dumps(json_data)

#####################
######Functions######  
#####################

# Build the API signature
def build_signature(customer_id, shared_key, date, content_length, method, content_type, resource):
    x_headers = 'x-ms-date:' + date
    string_to_hash = method + "\n" + str(content_length) + "\n" + content_type + "\n" + x_headers + "\n" + resource
    bytes_to_hash = bytes(string_to_hash).encode('utf-8')  
    decoded_key = base64.b64decode(shared_key)
    encoded_hash = base64.b64encode(hmac.new(decoded_key, bytes_to_hash, digestmod=hashlib.sha256).digest())
    authorization = "SharedKey {}:{}".format(customer_id,encoded_hash)
    return authorization

# Build and send a request to the POST API
def post_data(customer_id, shared_key, body, log_type):
    method = 'POST'
    content_type = 'application/json'
    resource = '/api/logs'
    rfc1123date = datetime.datetime.utcnow().strftime('%a, %d %b %Y %H:%M:%S GMT')
    content_length = len(body)
    signature = build_signature(customer_id, shared_key, rfc1123date, content_length, method, content_type, resource)
    uri = 'https://' + customer_id + '.ods.opinsights.azure.com' + resource + '?api-version=2016-04-01'

    headers = {
        'content-type': content_type,
        'Authorization': signature,
        'Log-Type': log_type,
        'x-ms-date': rfc1123date
    }

    response = requests.post(uri,data=body, headers=headers)
    if (response.status_code >= 200 and response.status_code <= 299):
        print 'Accepted'
    else:
        print "Response code: {}".format(response.status_code)

post_data(customer_id, shared_key, body, log_type)
```

## <a name="next-steps"></a><span data-ttu-id="4cf19-305">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4cf19-305">Next steps</span></span>
- <span data-ttu-id="4cf19-306">Usare l'[API di ricerca nei log](log-analytics-log-search-api.md) per recuperare dati dal repository di Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="4cf19-306">Use the [Log Search API](log-analytics-log-search-api.md) to retrieve data from the Log Analytics repository.</span></span>
