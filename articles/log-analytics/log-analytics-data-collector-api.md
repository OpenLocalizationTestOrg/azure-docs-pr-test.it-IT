---
title: API dell'agente di raccolta dati di HTTP Analitica aaaLog | Documenti Microsoft
description: "È possibile utilizzare hello API dell'agente di raccolta dati di Log Analitica HTTP tooadd JSON POST toohello Analitica Log repository dei dati da qualsiasi client che possono chiamare l'API REST hello. In questo articolo viene descritto come toouse hello API e vengono riportati alcuni esempi di come dati toopublish utilizzando diversi linguaggi di programmazione."
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
ms.openlocfilehash: c2921082831c49da764d946ac9c4fab975a38185
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="send-data-toolog-analytics-with-hello-http-data-collector-api"></a><span data-ttu-id="9f355-104">Inviare dati tooLog Analitica con hello API dell'agente di raccolta dati di HTTP</span><span class="sxs-lookup"><span data-stu-id="9f355-104">Send data tooLog Analytics with hello HTTP Data Collector API</span></span>
<span data-ttu-id="9f355-105">Questo articolo illustra come toouse hello API dell'agente di raccolta dati di HTTP toosend dati tooLog Analitica da un client di API REST.</span><span class="sxs-lookup"><span data-stu-id="9f355-105">This article shows you how toouse hello HTTP Data Collector API toosend data tooLog Analytics from a REST API client.</span></span>  <span data-ttu-id="9f355-106">Descrive come tooformat dati raccolti dallo script o applicazione, includerlo in una richiesta e tale richiesta autorizzata dal Log Analitica.</span><span class="sxs-lookup"><span data-stu-id="9f355-106">It describes how tooformat data collected by your script or application, include it in a request, and have that request authorized by Log Analytics.</span></span>  <span data-ttu-id="9f355-107">Vengono indicati esempi per PowerShell, C# e Python.</span><span class="sxs-lookup"><span data-stu-id="9f355-107">Examples are provided for PowerShell, C#, and Python.</span></span>

## <a name="concepts"></a><span data-ttu-id="9f355-108">Concetti</span><span class="sxs-lookup"><span data-stu-id="9f355-108">Concepts</span></span>
<span data-ttu-id="9f355-109">È possibile utilizzare l'API dell'agente di raccolta dati di HTTP toosend hello dati tooLog Analitica da qualsiasi client che è possibile chiamare un'API REST.</span><span class="sxs-lookup"><span data-stu-id="9f355-109">You can use hello HTTP Data Collector API toosend data tooLog Analytics from any client that can call a REST API.</span></span>  <span data-ttu-id="9f355-110">Potrebbe trattarsi di un runbook in automazione di Azure che raccoglie gestione dati da Azure o un altro cloud o potrebbero essere un sistema di gestione alternativo che usa tooconsolidate Log Analitica e analizzare i dati.</span><span class="sxs-lookup"><span data-stu-id="9f355-110">This might be a runbook in Azure Automation that collects management data from Azure or another cloud, or it might be an alternate management system that uses Log Analytics tooconsolidate and analyze data.</span></span>

<span data-ttu-id="9f355-111">Tutti i dati nel repository di hello Analitica Log vengono archiviati come un record con un tipo di record specifico.</span><span class="sxs-lookup"><span data-stu-id="9f355-111">All data in hello Log Analytics repository is stored as a record with a particular record type.</span></span>  <span data-ttu-id="9f355-112">Formattare il toohello toosend dati API dell'agente di raccolta dati di HTTP come più record in JSON.</span><span class="sxs-lookup"><span data-stu-id="9f355-112">You format your data toosend toohello HTTP Data Collector API as multiple records in JSON.</span></span>  <span data-ttu-id="9f355-113">Quando si inviano dati hello, viene creato un singolo record nel repository di hello per ciascun record nel payload della richiesta hello.</span><span class="sxs-lookup"><span data-stu-id="9f355-113">When you submit hello data, an individual record is created in hello repository for each record in hello request payload.</span></span>


![Panoramica dell'agente di raccolta dati HTTP](media/log-analytics-data-collector-api/overview.png)



## <a name="create-a-request"></a><span data-ttu-id="9f355-115">Creare una richiesta</span><span class="sxs-lookup"><span data-stu-id="9f355-115">Create a request</span></span>
<span data-ttu-id="9f355-116">API agente di raccolta dati di toouse hello HTTP, si crea una richiesta POST che include toosend dati hello in JavaScript Object Notation (JSON).</span><span class="sxs-lookup"><span data-stu-id="9f355-116">toouse hello HTTP Data Collector API, you create a POST request that includes hello data toosend in JavaScript Object Notation (JSON).</span></span>  <span data-ttu-id="9f355-117">Hello tre tabelle elenco hello che gli attributi necessari per ogni richiesta.</span><span class="sxs-lookup"><span data-stu-id="9f355-117">hello next three tables list hello attributes that are required for each request.</span></span> <span data-ttu-id="9f355-118">Viene descritto ogni attributo in modo più dettagliato più avanti in articolo hello.</span><span class="sxs-lookup"><span data-stu-id="9f355-118">We describe each attribute in more detail later in hello article.</span></span>

### <a name="request-uri"></a><span data-ttu-id="9f355-119">URI della richiesta</span><span class="sxs-lookup"><span data-stu-id="9f355-119">Request URI</span></span>
| <span data-ttu-id="9f355-120">Attributo</span><span class="sxs-lookup"><span data-stu-id="9f355-120">Attribute</span></span> | <span data-ttu-id="9f355-121">Proprietà</span><span class="sxs-lookup"><span data-stu-id="9f355-121">Property</span></span> |
|:--- |:--- |
| <span data-ttu-id="9f355-122">Metodo</span><span class="sxs-lookup"><span data-stu-id="9f355-122">Method</span></span> |<span data-ttu-id="9f355-123">POST</span><span class="sxs-lookup"><span data-stu-id="9f355-123">POST</span></span> |
| <span data-ttu-id="9f355-124">URI</span><span class="sxs-lookup"><span data-stu-id="9f355-124">URI</span></span> |<span data-ttu-id="9f355-125">https://\<IdCliente\>.ods.opinsights.azure.com/api/logs?api-version=2016-04-01</span><span class="sxs-lookup"><span data-stu-id="9f355-125">https://\<CustomerId\>.ods.opinsights.azure.com/api/logs?api-version=2016-04-01</span></span> |
| <span data-ttu-id="9f355-126">Tipo di contenuto</span><span class="sxs-lookup"><span data-stu-id="9f355-126">Content type</span></span> |<span data-ttu-id="9f355-127">application/json</span><span class="sxs-lookup"><span data-stu-id="9f355-127">application/json</span></span> |

### <a name="request-uri-parameters"></a><span data-ttu-id="9f355-128">Parametri URI della richiesta</span><span class="sxs-lookup"><span data-stu-id="9f355-128">Request URI parameters</span></span>
| <span data-ttu-id="9f355-129">Parametro</span><span class="sxs-lookup"><span data-stu-id="9f355-129">Parameter</span></span> | <span data-ttu-id="9f355-130">Description</span><span class="sxs-lookup"><span data-stu-id="9f355-130">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="9f355-131">CustomerID</span><span class="sxs-lookup"><span data-stu-id="9f355-131">CustomerID</span></span> |<span data-ttu-id="9f355-132">Hello identificatore univoco dell'area di lavoro di hello Microsoft Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="9f355-132">hello unique identifier for hello Microsoft Operations Management Suite workspace.</span></span> |
| <span data-ttu-id="9f355-133">Risorsa</span><span class="sxs-lookup"><span data-stu-id="9f355-133">Resource</span></span> |<span data-ttu-id="9f355-134">nome della risorsa API Hello: / api/logs.</span><span class="sxs-lookup"><span data-stu-id="9f355-134">hello API resource name: /api/logs.</span></span> |
| <span data-ttu-id="9f355-135">Versione dell'API</span><span class="sxs-lookup"><span data-stu-id="9f355-135">API Version</span></span> |<span data-ttu-id="9f355-136">versione di Hello del toouse hello API con questa richiesta.</span><span class="sxs-lookup"><span data-stu-id="9f355-136">hello version of hello API toouse with this request.</span></span> <span data-ttu-id="9f355-137">La versione attuale è 2016-04-01.</span><span class="sxs-lookup"><span data-stu-id="9f355-137">Currently, it's 2016-04-01.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="9f355-138">Intestazioni della richiesta</span><span class="sxs-lookup"><span data-stu-id="9f355-138">Request headers</span></span>
| <span data-ttu-id="9f355-139">Intestazione</span><span class="sxs-lookup"><span data-stu-id="9f355-139">Header</span></span> | <span data-ttu-id="9f355-140">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9f355-140">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="9f355-141">Authorization</span><span class="sxs-lookup"><span data-stu-id="9f355-141">Authorization</span></span> |<span data-ttu-id="9f355-142">firma di autorizzazione Hello.</span><span class="sxs-lookup"><span data-stu-id="9f355-142">hello authorization signature.</span></span> <span data-ttu-id="9f355-143">Più avanti in articolo hello, è possibile leggere le procedure intestazione toocreate un HMAC-SHA256.</span><span class="sxs-lookup"><span data-stu-id="9f355-143">Later in hello article, you can read about how toocreate an HMAC-SHA256 header.</span></span> |
| <span data-ttu-id="9f355-144">Log-Type</span><span class="sxs-lookup"><span data-stu-id="9f355-144">Log-Type</span></span> |<span data-ttu-id="9f355-145">Specificare il tipo di record hello di dati hello viene inviati.</span><span class="sxs-lookup"><span data-stu-id="9f355-145">Specify hello record type of hello data that is being submitted.</span></span> <span data-ttu-id="9f355-146">Tipo di log hello attualmente supporta solo caratteri alfabetici.</span><span class="sxs-lookup"><span data-stu-id="9f355-146">Currently, hello log type supports only alpha characters.</span></span> <span data-ttu-id="9f355-147">Non supporta valori numerici o caratteri speciali.</span><span class="sxs-lookup"><span data-stu-id="9f355-147">It does not support numerics or special characters.</span></span> |
| <span data-ttu-id="9f355-148">x-ms-date</span><span class="sxs-lookup"><span data-stu-id="9f355-148">x-ms-date</span></span> |<span data-ttu-id="9f355-149">Data di Hello in cui è stata elaborata la richiesta di hello, nel formato RFC 1123.</span><span class="sxs-lookup"><span data-stu-id="9f355-149">hello date that hello request was processed, in RFC 1123 format.</span></span> |
| <span data-ttu-id="9f355-150">time-generated-field</span><span class="sxs-lookup"><span data-stu-id="9f355-150">time-generated-field</span></span> |<span data-ttu-id="9f355-151">nome Hello di un campo nei dati hello che contiene il timestamp di hello hello elemento dei dati.</span><span class="sxs-lookup"><span data-stu-id="9f355-151">hello name of a field in hello data that contains hello timestamp of hello data item.</span></span> <span data-ttu-id="9f355-152">Se si specifica un campo, il relativo contenuto verrà usato per **TimeGenerated**.</span><span class="sxs-lookup"><span data-stu-id="9f355-152">If you specify a field then its contents are used for **TimeGenerated**.</span></span> <span data-ttu-id="9f355-153">Se questo campo non è specificato, hello predefinito per **TimeGenerated** è ora hello che hello messaggio verrà acquisito.</span><span class="sxs-lookup"><span data-stu-id="9f355-153">If this field isn’t specified, hello default for **TimeGenerated** is hello time that hello message is ingested.</span></span> <span data-ttu-id="9f355-154">il contenuto di Hello del campo messaggio hello deve seguire il formato ISO 8601 hello AAAA-MM-ddTHH.</span><span class="sxs-lookup"><span data-stu-id="9f355-154">hello contents of hello message field should follow hello ISO 8601 format YYYY-MM-DDThh:mm:ssZ.</span></span> |

## <a name="authorization"></a><span data-ttu-id="9f355-155">Authorization</span><span class="sxs-lookup"><span data-stu-id="9f355-155">Authorization</span></span>
<span data-ttu-id="9f355-156">Qualsiasi toohello richiesta API dell'agente di raccolta dati di Log Analitica HTTP deve includere un'intestazione di autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="9f355-156">Any request toohello Log Analytics HTTP Data Collector API must include an authorization header.</span></span> <span data-ttu-id="9f355-157">tooauthenticate una richiesta, è necessario firmare la richiesta di hello con hello primaria o chiave secondaria di hello per area di lavoro hello che effettua la richiesta hello.</span><span class="sxs-lookup"><span data-stu-id="9f355-157">tooauthenticate a request, you must sign hello request with either hello primary or hello secondary key for hello workspace that is making hello request.</span></span> <span data-ttu-id="9f355-158">Quindi, passare la firma come parte della richiesta di hello.</span><span class="sxs-lookup"><span data-stu-id="9f355-158">Then, pass that signature as part of hello request.</span></span>   

<span data-ttu-id="9f355-159">Di seguito è riportato il formato di hello per intestazione authorization hello:</span><span class="sxs-lookup"><span data-stu-id="9f355-159">Here's hello format for hello authorization header:</span></span>

```
Authorization: SharedKey <WorkspaceID>:<Signature>
```

<span data-ttu-id="9f355-160">*Idareadilavoro* è hello identificatore univoco dell'area di lavoro di hello Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="9f355-160">*WorkspaceID* is hello unique identifier for hello Operations Management Suite workspace.</span></span> <span data-ttu-id="9f355-161">*Firma* è un [codice HMAC (Hash-based Message Authentication Code)](https://msdn.microsoft.com/library/system.security.cryptography.hmacsha256.aspx) che viene costruito dalla richiesta hello e quindi calcolato utilizzando hello [algoritmo SHA256](https://msdn.microsoft.com/library/system.security.cryptography.sha256.aspx).</span><span class="sxs-lookup"><span data-stu-id="9f355-161">*Signature* is a [Hash-based Message Authentication Code (HMAC)](https://msdn.microsoft.com/library/system.security.cryptography.hmacsha256.aspx) that is constructed from hello request and then computed by using hello [SHA256 algorithm](https://msdn.microsoft.com/library/system.security.cryptography.sha256.aspx).</span></span> <span data-ttu-id="9f355-162">Viene quindi codificato con la codifica Base64.</span><span class="sxs-lookup"><span data-stu-id="9f355-162">Then, you encode it by using Base64 encoding.</span></span>

<span data-ttu-id="9f355-163">Utilizzare questo hello tooencode formato **SharedKey** stringa di firma:</span><span class="sxs-lookup"><span data-stu-id="9f355-163">Use this format tooencode hello **SharedKey** signature string:</span></span>

```
StringToSign = VERB + "\n" +
                  Content-Length + "\n" +
               Content-Type + "\n" +
                  x-ms-date + "\n" +
                  "/api/logs";
```

<span data-ttu-id="9f355-164">Di seguito è riportato un esempio di stringa della firma:</span><span class="sxs-lookup"><span data-stu-id="9f355-164">Here's an example of a signature string:</span></span>

```
POST\n1024\napplication/json\nx-ms-date:Mon, 04 Apr 2016 08:00:00 GMT\n/api/logs
```

<span data-ttu-id="9f355-165">Quando si dispone di stringa di firma hello, codificarli utilizzando hello l'algoritmo HMAC-SHA256 nella stringa con codifica UTF-8 hello e quindi codificare il risultato di hello come base 64.</span><span class="sxs-lookup"><span data-stu-id="9f355-165">When you have hello signature string, encode it by using hello HMAC-SHA256 algorithm on hello UTF-8-encoded string, and then encode hello result as Base64.</span></span> <span data-ttu-id="9f355-166">Usare il formato seguente:</span><span class="sxs-lookup"><span data-stu-id="9f355-166">Use this format:</span></span>

```
Signature=Base64(HMAC-SHA256(UTF8(StringToSign)))
```

<span data-ttu-id="9f355-167">esempi di Hello nelle sezioni successive di hello è toohelp codice di esempio si crea un'intestazione di autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="9f355-167">hello samples in hello next sections have sample code toohelp you create an authorization header.</span></span>

## <a name="request-body"></a><span data-ttu-id="9f355-168">Corpo della richiesta</span><span class="sxs-lookup"><span data-stu-id="9f355-168">Request body</span></span>
<span data-ttu-id="9f355-169">corpo del messaggio hello del Hello deve essere in JSON.</span><span class="sxs-lookup"><span data-stu-id="9f355-169">hello body of hello message must be in JSON.</span></span> <span data-ttu-id="9f355-170">Deve includere uno o più record con coppie nome / valore di proprietà hello nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="9f355-170">It must include one or more records with hello property name and value pairs in this format:</span></span>

```
{
"property1": "value1",
" property 2": "value2"
" property 3": "value3",
" property 4": "value4"
}
```

<span data-ttu-id="9f355-171">È possibile raggruppare più record in una singola richiesta usando hello seguente formato.</span><span class="sxs-lookup"><span data-stu-id="9f355-171">You can batch multiple records together in a single request by using hello following format.</span></span> <span data-ttu-id="9f355-172">Tutti i record di hello devono essere hello stesso tipo di record.</span><span class="sxs-lookup"><span data-stu-id="9f355-172">All hello records must be hello same record type.</span></span>

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

## <a name="record-type-and-properties"></a><span data-ttu-id="9f355-173">Proprietà e tipo di record</span><span class="sxs-lookup"><span data-stu-id="9f355-173">Record type and properties</span></span>
<span data-ttu-id="9f355-174">Si definisce un tipo di record personalizzato quando si inviano dati tramite l'API dell'agente di raccolta dati di Log Analitica HTTP hello.</span><span class="sxs-lookup"><span data-stu-id="9f355-174">You define a custom record type when you submit data through hello Log Analytics HTTP Data Collector API.</span></span> <span data-ttu-id="9f355-175">Attualmente, non è possibile scrivere dati tooexisting tipi di record che sono stati creati da altri tipi di dati e soluzioni.</span><span class="sxs-lookup"><span data-stu-id="9f355-175">Currently, you can't write data tooexisting record types that were created by other data types and solutions.</span></span> <span data-ttu-id="9f355-176">Log Analitica legge i dati in ingresso hello e quindi crea le proprietà che corrispondono a tipi di dati di hello di valori hello immesso.</span><span class="sxs-lookup"><span data-stu-id="9f355-176">Log Analytics reads hello incoming data and then creates properties that match hello data types of hello values that you enter.</span></span>

<span data-ttu-id="9f355-177">Ogni richiesta toohello Log Analitica API devono includere un **-tipo di Log** intestazione con nome hello per tipo di record di hello.</span><span class="sxs-lookup"><span data-stu-id="9f355-177">Each request toohello Log Analytics API must include a **Log-Type** header with hello name for hello record type.</span></span> <span data-ttu-id="9f355-178">suffisso Hello **_CL** toohello automaticamente aggiunte nome immesso toodistinguish da altri log tipi come un log personalizzato.</span><span class="sxs-lookup"><span data-stu-id="9f355-178">hello suffix **_CL** is automatically appended toohello name you enter toodistinguish it from other log types as a custom log.</span></span> <span data-ttu-id="9f355-179">Ad esempio, se si immette il nome di hello **MyNewRecordType**, Log Analitica crea un record con il tipo di hello **MyNewRecordType_CL**.</span><span class="sxs-lookup"><span data-stu-id="9f355-179">For example, if you enter hello name **MyNewRecordType**, Log Analytics creates a record with hello type **MyNewRecordType_CL**.</span></span> <span data-ttu-id="9f355-180">È così possibile evitare conflitti tra i nomi dei tipi creati dall'utente e i nomi forniti nelle soluzioni Microsoft correnti o future.</span><span class="sxs-lookup"><span data-stu-id="9f355-180">This helps ensure that there are no conflicts between user-created type names and those shipped in current or future Microsoft solutions.</span></span>

<span data-ttu-id="9f355-181">tipo di dati di una proprietà tooidentify, Log Analitica aggiunge un nome di proprietà toohello suffisso.</span><span class="sxs-lookup"><span data-stu-id="9f355-181">tooidentify a property's data type, Log Analytics adds a suffix toohello property name.</span></span> <span data-ttu-id="9f355-182">Se una proprietà contiene un valore null, la proprietà hello non è incluso in tale record.</span><span class="sxs-lookup"><span data-stu-id="9f355-182">If a property contains a null value, hello property is not included in that record.</span></span> <span data-ttu-id="9f355-183">Questa tabella elenca il tipo di dati proprietà hello e il suffisso corrispondente:</span><span class="sxs-lookup"><span data-stu-id="9f355-183">This table lists hello property data type and corresponding suffix:</span></span>

| <span data-ttu-id="9f355-184">Tipo di dati proprietà</span><span class="sxs-lookup"><span data-stu-id="9f355-184">Property data type</span></span> | <span data-ttu-id="9f355-185">Suffisso</span><span class="sxs-lookup"><span data-stu-id="9f355-185">Suffix</span></span> |
|:--- |:--- |
| <span data-ttu-id="9f355-186">String</span><span class="sxs-lookup"><span data-stu-id="9f355-186">String</span></span> |<span data-ttu-id="9f355-187">_s</span><span class="sxs-lookup"><span data-stu-id="9f355-187">_s</span></span> |
| <span data-ttu-id="9f355-188">Boolean</span><span class="sxs-lookup"><span data-stu-id="9f355-188">Boolean</span></span> |<span data-ttu-id="9f355-189">_b</span><span class="sxs-lookup"><span data-stu-id="9f355-189">_b</span></span> |
| <span data-ttu-id="9f355-190">Double</span><span class="sxs-lookup"><span data-stu-id="9f355-190">Double</span></span> |<span data-ttu-id="9f355-191">_d</span><span class="sxs-lookup"><span data-stu-id="9f355-191">_d</span></span> |
| <span data-ttu-id="9f355-192">Data/ora</span><span class="sxs-lookup"><span data-stu-id="9f355-192">Date/time</span></span> |<span data-ttu-id="9f355-193">_t</span><span class="sxs-lookup"><span data-stu-id="9f355-193">_t</span></span> |
| <span data-ttu-id="9f355-194">GUID</span><span class="sxs-lookup"><span data-stu-id="9f355-194">GUID</span></span> |<span data-ttu-id="9f355-195">_g</span><span class="sxs-lookup"><span data-stu-id="9f355-195">_g</span></span> |

<span data-ttu-id="9f355-196">tipo di dati Hello Analitica di Log viene utilizzato per ogni proprietà dipende se il tipo di record hello per il nuovo record di hello esiste già.</span><span class="sxs-lookup"><span data-stu-id="9f355-196">hello data type that Log Analytics uses for each property depends on whether hello record type for hello new record already exists.</span></span>

* <span data-ttu-id="9f355-197">Se il tipo di record hello non esiste, Log Analitica crea uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="9f355-197">If hello record type does not exist, Log Analytics creates a new one.</span></span> <span data-ttu-id="9f355-198">Log Analitica utilizza hello JSON inferenza toodetermine hello dati di tipo per ogni proprietà per il nuovo record di hello.</span><span class="sxs-lookup"><span data-stu-id="9f355-198">Log Analytics uses hello JSON type inference toodetermine hello data type for each property for hello new record.</span></span>
* <span data-ttu-id="9f355-199">Se il tipo di record hello esiste, Analitica Log tenta toocreate un nuovo record in base alle proprietà esistenti.</span><span class="sxs-lookup"><span data-stu-id="9f355-199">If hello record type does exist, Log Analytics attempts toocreate a new record based on existing properties.</span></span> <span data-ttu-id="9f355-200">Se hello tipo di dati per una proprietà nel nuovo record di hello non corrispondono e non può essere convertito toohello tipi esistenti o se hello record include una proprietà che non esiste, Log Analitica crea una nuova proprietà con suffisso rilevanti hello.</span><span class="sxs-lookup"><span data-stu-id="9f355-200">If hello data type for a property in hello new record doesn’t match and can’t be converted toohello existing type, or if hello record includes a property that doesn’t exist, Log Analytics creates a new property that has hello relevant suffix.</span></span>

<span data-ttu-id="9f355-201">Questa voce di invio creerà ad esempio un record con tre proprietà, **number_d**, **boolean_b** e **string_s**:</span><span class="sxs-lookup"><span data-stu-id="9f355-201">For example, this submission entry would create a record with three properties, **number_d**, **boolean_b**, and **string_s**:</span></span>

![Esempio di record 1](media/log-analytics-data-collector-api/record-01.png)

<span data-ttu-id="9f355-203">Se questa voce successiva, è quindi inviata con tutti i valori formattati come stringhe, le proprietà di hello non modificherebbe.</span><span class="sxs-lookup"><span data-stu-id="9f355-203">If you then submitted this next entry, with all values formatted as strings, hello properties would not change.</span></span> <span data-ttu-id="9f355-204">Questi valori possono essere tooexisting convertire i tipi di dati:</span><span class="sxs-lookup"><span data-stu-id="9f355-204">These values can be converted tooexisting data types:</span></span>

![Esempio di record 2](media/log-analytics-data-collector-api/record-02.png)

<span data-ttu-id="9f355-206">Ma, se sono state quindi questo invio successivo, Log Analitica creerebbe hello nuove proprietà **boolean_d** e **string_d**.</span><span class="sxs-lookup"><span data-stu-id="9f355-206">But, if you then made this next submission, Log Analytics would create hello new properties **boolean_d** and **string_d**.</span></span> <span data-ttu-id="9f355-207">Questi valori non possono essere convertiti:</span><span class="sxs-lookup"><span data-stu-id="9f355-207">These values can't be converted:</span></span>

![Esempio di record 3](media/log-analytics-data-collector-api/record-03.png)

<span data-ttu-id="9f355-209">Se è stata inviata quindi hello entrata prima della creazione di tipo di record hello, Log Analitica creerà un record con tre proprietà, **num_successi**, **boolean_s**, e **string_s**.</span><span class="sxs-lookup"><span data-stu-id="9f355-209">If you then submitted hello following entry, before hello record type was created, Log Analytics would create a record with three properties, **number_s**, **boolean_s**, and **string_s**.</span></span> <span data-ttu-id="9f355-210">In questa voce, ognuno dei valori iniziali hello è formattato come una stringa:</span><span class="sxs-lookup"><span data-stu-id="9f355-210">In this entry, each of hello initial values is formatted as a string:</span></span>

![Esempio di record 4](media/log-analytics-data-collector-api/record-04.png)

## <a name="data-limits"></a><span data-ttu-id="9f355-212">Limiti dei dati</span><span class="sxs-lookup"><span data-stu-id="9f355-212">Data limits</span></span>
<span data-ttu-id="9f355-213">Esistono alcune limitazioni di racchiudere i dati di hello registrati toohello raccolta dei dati di Log Analitica API.</span><span class="sxs-lookup"><span data-stu-id="9f355-213">There are some constraints around hello data posted toohello Log Analytics Data collection API.</span></span>

* <span data-ttu-id="9f355-214">Massimo di 30 MB per post tooLog l'API dell'agente di raccolta dati Analitica.</span><span class="sxs-lookup"><span data-stu-id="9f355-214">Maximum of 30 MB per post tooLog Analytics Data Collector API.</span></span> <span data-ttu-id="9f355-215">Questo limite riguarda le dimensioni di ogni messaggio.</span><span class="sxs-lookup"><span data-stu-id="9f355-215">This is a size limit for a single post.</span></span> <span data-ttu-id="9f355-216">Se dati hello da un messaggio che supera i 30 MB, è necessario suddividere hello dati backup toosmaller dimensioni blocchi e li inviano contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="9f355-216">If hello data from a single post that exceeds 30 MB, you should split hello data up toosmaller sized chunks and send them concurrently.</span></span>
* <span data-ttu-id="9f355-217">Limite di 32 KB per i valori dei campi.</span><span class="sxs-lookup"><span data-stu-id="9f355-217">Maximum of 32 KB limit for field values.</span></span> <span data-ttu-id="9f355-218">Se il valore di campo hello è maggiore di 32 KB, dati hello verranno troncati.</span><span class="sxs-lookup"><span data-stu-id="9f355-218">If hello field value is greater than 32 KB, hello data will be truncated.</span></span>
* <span data-ttu-id="9f355-219">Il numero massimo di campi consigliato per un determinato tipo è 50.</span><span class="sxs-lookup"><span data-stu-id="9f355-219">Recommended maximum number of fields for a given type is 50.</span></span> <span data-ttu-id="9f355-220">Si tratta di un limite pratico dal punto di vista dell'usabilità e dell'esperienza di ricerca.</span><span class="sxs-lookup"><span data-stu-id="9f355-220">This is a practical limit from a usability and search experience perspective.</span></span>  

## <a name="return-codes"></a><span data-ttu-id="9f355-221">Codici restituiti</span><span class="sxs-lookup"><span data-stu-id="9f355-221">Return codes</span></span>
<span data-ttu-id="9f355-222">codice di stato HTTP 200 Hello richiesta hello che è stata ricevuta per l'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="9f355-222">hello HTTP status code 200 means that hello request has been received for processing.</span></span> <span data-ttu-id="9f355-223">Ciò indica che operazione hello è stata completata.</span><span class="sxs-lookup"><span data-stu-id="9f355-223">This indicates that hello operation completed successfully.</span></span>

<span data-ttu-id="9f355-224">Questa tabella sono elencati i set di codici di stato che potrebbe restituire servizio hello completo hello:</span><span class="sxs-lookup"><span data-stu-id="9f355-224">This table lists hello complete set of status codes that hello service might return:</span></span>

| <span data-ttu-id="9f355-225">Codice</span><span class="sxs-lookup"><span data-stu-id="9f355-225">Code</span></span> | <span data-ttu-id="9f355-226">Stato</span><span class="sxs-lookup"><span data-stu-id="9f355-226">Status</span></span> | <span data-ttu-id="9f355-227">Codice di errore</span><span class="sxs-lookup"><span data-stu-id="9f355-227">Error code</span></span> | <span data-ttu-id="9f355-228">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9f355-228">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="9f355-229">200</span><span class="sxs-lookup"><span data-stu-id="9f355-229">200</span></span> |<span data-ttu-id="9f355-230">OK</span><span class="sxs-lookup"><span data-stu-id="9f355-230">OK</span></span> | |<span data-ttu-id="9f355-231">richiesta di Hello è stato accettato.</span><span class="sxs-lookup"><span data-stu-id="9f355-231">hello request was successfully accepted.</span></span> |
| <span data-ttu-id="9f355-232">400</span><span class="sxs-lookup"><span data-stu-id="9f355-232">400</span></span> |<span data-ttu-id="9f355-233">Richiesta non valida</span><span class="sxs-lookup"><span data-stu-id="9f355-233">Bad request</span></span> |<span data-ttu-id="9f355-234">InactiveCustomer</span><span class="sxs-lookup"><span data-stu-id="9f355-234">InactiveCustomer</span></span> |<span data-ttu-id="9f355-235">area di lavoro Hello è stato chiuso.</span><span class="sxs-lookup"><span data-stu-id="9f355-235">hello workspace has been closed.</span></span> |
| <span data-ttu-id="9f355-236">400</span><span class="sxs-lookup"><span data-stu-id="9f355-236">400</span></span> |<span data-ttu-id="9f355-237">Richiesta non valida</span><span class="sxs-lookup"><span data-stu-id="9f355-237">Bad request</span></span> |<span data-ttu-id="9f355-238">InvalidApiVersion</span><span class="sxs-lookup"><span data-stu-id="9f355-238">InvalidApiVersion</span></span> |<span data-ttu-id="9f355-239">versione di Hello API specificata non è stato riconosciuto dal servizio hello.</span><span class="sxs-lookup"><span data-stu-id="9f355-239">hello API version that you specified was not recognized by hello service.</span></span> |
| <span data-ttu-id="9f355-240">400</span><span class="sxs-lookup"><span data-stu-id="9f355-240">400</span></span> |<span data-ttu-id="9f355-241">Richiesta non valida</span><span class="sxs-lookup"><span data-stu-id="9f355-241">Bad request</span></span> |<span data-ttu-id="9f355-242">InvalidCustomerId</span><span class="sxs-lookup"><span data-stu-id="9f355-242">InvalidCustomerId</span></span> |<span data-ttu-id="9f355-243">ID dell'area di lavoro Hello specificato non è valido.</span><span class="sxs-lookup"><span data-stu-id="9f355-243">hello workspace ID specified is invalid.</span></span> |
| <span data-ttu-id="9f355-244">400</span><span class="sxs-lookup"><span data-stu-id="9f355-244">400</span></span> |<span data-ttu-id="9f355-245">Richiesta non valida</span><span class="sxs-lookup"><span data-stu-id="9f355-245">Bad request</span></span> |<span data-ttu-id="9f355-246">InvalidDataFormat</span><span class="sxs-lookup"><span data-stu-id="9f355-246">InvalidDataFormat</span></span> |<span data-ttu-id="9f355-247">È stata inviato JSON non valido.</span><span class="sxs-lookup"><span data-stu-id="9f355-247">Invalid JSON was submitted.</span></span> <span data-ttu-id="9f355-248">corpo della risposta Hello potrebbe contenere ulteriori informazioni su come tooresolve hello errore.</span><span class="sxs-lookup"><span data-stu-id="9f355-248">hello response body might contain more information about how tooresolve hello error.</span></span> |
| <span data-ttu-id="9f355-249">400</span><span class="sxs-lookup"><span data-stu-id="9f355-249">400</span></span> |<span data-ttu-id="9f355-250">Richiesta non valida</span><span class="sxs-lookup"><span data-stu-id="9f355-250">Bad request</span></span> |<span data-ttu-id="9f355-251">InvalidLogType</span><span class="sxs-lookup"><span data-stu-id="9f355-251">InvalidLogType</span></span> |<span data-ttu-id="9f355-252">tipo di log Hello specificato contenuti caratteri speciali o valori numerici.</span><span class="sxs-lookup"><span data-stu-id="9f355-252">hello log type specified contained special characters or numerics.</span></span> |
| <span data-ttu-id="9f355-253">400</span><span class="sxs-lookup"><span data-stu-id="9f355-253">400</span></span> |<span data-ttu-id="9f355-254">Richiesta non valida</span><span class="sxs-lookup"><span data-stu-id="9f355-254">Bad request</span></span> |<span data-ttu-id="9f355-255">MissingApiVersion</span><span class="sxs-lookup"><span data-stu-id="9f355-255">MissingApiVersion</span></span> |<span data-ttu-id="9f355-256">versione dell'API Hello non è stato specificato.</span><span class="sxs-lookup"><span data-stu-id="9f355-256">hello API version wasn’t specified.</span></span> |
| <span data-ttu-id="9f355-257">400</span><span class="sxs-lookup"><span data-stu-id="9f355-257">400</span></span> |<span data-ttu-id="9f355-258">Richiesta non valida</span><span class="sxs-lookup"><span data-stu-id="9f355-258">Bad request</span></span> |<span data-ttu-id="9f355-259">MissingContentType</span><span class="sxs-lookup"><span data-stu-id="9f355-259">MissingContentType</span></span> |<span data-ttu-id="9f355-260">non è stato specificato il tipo di contenuto Hello.</span><span class="sxs-lookup"><span data-stu-id="9f355-260">hello content type wasn’t specified.</span></span> |
| <span data-ttu-id="9f355-261">400</span><span class="sxs-lookup"><span data-stu-id="9f355-261">400</span></span> |<span data-ttu-id="9f355-262">Richiesta non valida</span><span class="sxs-lookup"><span data-stu-id="9f355-262">Bad request</span></span> |<span data-ttu-id="9f355-263">MissingLogType</span><span class="sxs-lookup"><span data-stu-id="9f355-263">MissingLogType</span></span> |<span data-ttu-id="9f355-264">Hello richiesto è stato specificato alcun tipo di valore di log.</span><span class="sxs-lookup"><span data-stu-id="9f355-264">hello required value log type wasn’t specified.</span></span> |
| <span data-ttu-id="9f355-265">400</span><span class="sxs-lookup"><span data-stu-id="9f355-265">400</span></span> |<span data-ttu-id="9f355-266">Richiesta non valida</span><span class="sxs-lookup"><span data-stu-id="9f355-266">Bad request</span></span> |<span data-ttu-id="9f355-267">UnsupportedContentType</span><span class="sxs-lookup"><span data-stu-id="9f355-267">UnsupportedContentType</span></span> |<span data-ttu-id="9f355-268">tipo di contenuto Hello non è stato impostato troppo**application/json**.</span><span class="sxs-lookup"><span data-stu-id="9f355-268">hello content type was not set too**application/json**.</span></span> |
| <span data-ttu-id="9f355-269">403</span><span class="sxs-lookup"><span data-stu-id="9f355-269">403</span></span> |<span data-ttu-id="9f355-270">Accesso negato</span><span class="sxs-lookup"><span data-stu-id="9f355-270">Forbidden</span></span> |<span data-ttu-id="9f355-271">InvalidAuthorization</span><span class="sxs-lookup"><span data-stu-id="9f355-271">InvalidAuthorization</span></span> |<span data-ttu-id="9f355-272">Errore del servizio di Hello richiesta hello tooauthenticate.</span><span class="sxs-lookup"><span data-stu-id="9f355-272">hello service failed tooauthenticate hello request.</span></span> <span data-ttu-id="9f355-273">Verificare la chiave di connessione e l'ID dell'area di lavoro hello siano validi.</span><span class="sxs-lookup"><span data-stu-id="9f355-273">Verify that hello workspace ID and connection key are valid.</span></span> |
| <span data-ttu-id="9f355-274">404</span><span class="sxs-lookup"><span data-stu-id="9f355-274">404</span></span> |<span data-ttu-id="9f355-275">Non trovato</span><span class="sxs-lookup"><span data-stu-id="9f355-275">Not Found</span></span> | | <span data-ttu-id="9f355-276">URL di hello fornito non è corretto oppure hello richiesta è troppo grande.</span><span class="sxs-lookup"><span data-stu-id="9f355-276">Either hello URL provided is incorrect, or hello request is too large.</span></span> |
| <span data-ttu-id="9f355-277">429</span><span class="sxs-lookup"><span data-stu-id="9f355-277">429</span></span> |<span data-ttu-id="9f355-278">Troppe richieste</span><span class="sxs-lookup"><span data-stu-id="9f355-278">Too Many Requests</span></span> | | <span data-ttu-id="9f355-279">è presente un'elevata quantità di dati dell'account di servizio di Hello.</span><span class="sxs-lookup"><span data-stu-id="9f355-279">hello service is experiencing a high volume of data from your account.</span></span> <span data-ttu-id="9f355-280">Riprovare più tardi richiesta hello.</span><span class="sxs-lookup"><span data-stu-id="9f355-280">Please retry hello request later.</span></span> |
| <span data-ttu-id="9f355-281">500</span><span class="sxs-lookup"><span data-stu-id="9f355-281">500</span></span> |<span data-ttu-id="9f355-282">Internal Server Error</span><span class="sxs-lookup"><span data-stu-id="9f355-282">Internal Server Error</span></span> |<span data-ttu-id="9f355-283">UnspecifiedError</span><span class="sxs-lookup"><span data-stu-id="9f355-283">UnspecifiedError</span></span> |<span data-ttu-id="9f355-284">servizio Hello ha rilevato un errore interno.</span><span class="sxs-lookup"><span data-stu-id="9f355-284">hello service encountered an internal error.</span></span> <span data-ttu-id="9f355-285">Ritentare la richiesta hello.</span><span class="sxs-lookup"><span data-stu-id="9f355-285">Please retry hello request.</span></span> |
| <span data-ttu-id="9f355-286">503</span><span class="sxs-lookup"><span data-stu-id="9f355-286">503</span></span> |<span data-ttu-id="9f355-287">Servizio non disponibile</span><span class="sxs-lookup"><span data-stu-id="9f355-287">Service Unavailable</span></span> |<span data-ttu-id="9f355-288">ServiceUnavailable</span><span class="sxs-lookup"><span data-stu-id="9f355-288">ServiceUnavailable</span></span> |<span data-ttu-id="9f355-289">servizio Hello è attualmente disponibile tooreceive richieste.</span><span class="sxs-lookup"><span data-stu-id="9f355-289">hello service currently is unavailable tooreceive requests.</span></span> <span data-ttu-id="9f355-290">Si prega di ripetere la richiesta.</span><span class="sxs-lookup"><span data-stu-id="9f355-290">Please retry your request.</span></span> |

## <a name="query-data"></a><span data-ttu-id="9f355-291">Eseguire query sui dati</span><span class="sxs-lookup"><span data-stu-id="9f355-291">Query data</span></span>
<span data-ttu-id="9f355-292">dati tooquery inviati dai hello API dell'agente di raccolta dati HTTP di Analitica Log, cercare i record con **tipo** ovvero uguale toohello **LogType** valore specificato, seguito da **_CL**.</span><span class="sxs-lookup"><span data-stu-id="9f355-292">tooquery data submitted by hello Log Analytics HTTP Data Collector API, search for records with **Type** that is equal toohello **LogType** value that you specified, appended with **_CL**.</span></span> <span data-ttu-id="9f355-293">Usando ad esempio **MyCustomLog** verranno restituiti tutti i record con **Type=MyCustomLog_CL**.</span><span class="sxs-lookup"><span data-stu-id="9f355-293">For example, if you used **MyCustomLog**, then you'd return all records with **Type=MyCustomLog_CL**.</span></span>

>[!NOTE]
> <span data-ttu-id="9f355-294">Se l'area di lavoro è stato aggiornato toohello [Analitica Log nuovo linguaggio di query](log-analytics-log-search-upgrade.md), quindi hello sopra query modificherebbe toohello seguente.</span><span class="sxs-lookup"><span data-stu-id="9f355-294">If your workspace has been upgraded toohello [new Log Analytics query language](log-analytics-log-search-upgrade.md), then hello above query would change toohello following.</span></span>

> `MyCustomLog_CL`

## <a name="sample-requests"></a><span data-ttu-id="9f355-295">Richieste di esempio</span><span class="sxs-lookup"><span data-stu-id="9f355-295">Sample requests</span></span>
<span data-ttu-id="9f355-296">Nelle sezioni successive di hello, sono disponibili esempi di dati di toosubmit toohello API dell'agente di raccolta dati di Log Analitica HTTP utilizzando diversi linguaggi di programmazione.</span><span class="sxs-lookup"><span data-stu-id="9f355-296">In hello next sections, you'll find samples of how toosubmit data toohello Log Analytics HTTP Data Collector API by using different programming languages.</span></span>

<span data-ttu-id="9f355-297">Per ogni esempio, eseguire questi passaggi variabili hello tooset per intestazione authorization hello:</span><span class="sxs-lookup"><span data-stu-id="9f355-297">For each sample, do these steps tooset hello variables for hello authorization header:</span></span>

1. <span data-ttu-id="9f355-298">Nel portale di Operations Management Suite hello selezionare hello **impostazioni** riquadro e quindi selezionare hello **Connected Sources** scheda.</span><span class="sxs-lookup"><span data-stu-id="9f355-298">In hello Operations Management Suite portal, select hello **Settings** tile, and then select hello **Connected Sources** tab.</span></span>
2. <span data-ttu-id="9f355-299">toohello destra **ID area di lavoro**, selezionare l'icona di copia hello e quindi incollare hello ID come valore di hello di hello **ID cliente** variabile.</span><span class="sxs-lookup"><span data-stu-id="9f355-299">toohello right of **Workspace ID**, select hello copy icon, and then paste hello ID as hello value of hello **Customer ID** variable.</span></span>
3. <span data-ttu-id="9f355-300">toohello destra **chiave primaria**, selezionare l'icona di copia hello e quindi incollare hello ID come valore di hello di hello **chiave condivisa** variabile.</span><span class="sxs-lookup"><span data-stu-id="9f355-300">toohello right of **Primary Key**, select hello copy icon, and then paste hello ID as hello value of hello **Shared Key** variable.</span></span>

<span data-ttu-id="9f355-301">In alternativa, è possibile modificare le variabili di hello per il tipo di log hello e i dati JSON.</span><span class="sxs-lookup"><span data-stu-id="9f355-301">Alternatively, you can change hello variables for hello log type and JSON data.</span></span>

### <a name="powershell-sample"></a><span data-ttu-id="9f355-302">Esempio PowerShell</span><span class="sxs-lookup"><span data-stu-id="9f355-302">PowerShell sample</span></span>
```
# Replace with your Workspace ID
$CustomerId = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"  

# Replace with your Primary Key
$SharedKey = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"

# Specify hello name of hello record type that you'll be creating
$LogType = "MyRecordType"

# Specify a field with hello created time for hello records
$TimeStampField = "DateValue"


# Create two records with hello same set of properties toocreate
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

# Create hello function toocreate hello authorization signature
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


# Create hello function toocreate and post hello request
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

# Submit hello data toohello API endpoint
Post-OMSData -customerId $customerId -sharedKey $sharedKey -body ([System.Text.Encoding]::UTF8.GetBytes($json)) -logType $logType  
```

### <a name="c-sample"></a><span data-ttu-id="9f355-303">Esempio C#</span><span class="sxs-lookup"><span data-stu-id="9f355-303">C# sample</span></span>
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

        // Update customerId tooyour Operations Management Suite workspace ID
        static string customerId = "xxxxxxxx-xxx-xxx-xxx-xxxxxxxxxxxx";

        // For sharedKey, use either hello primary or hello secondary Connected Sources client authentication key   
        static string sharedKey = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx";

        // LogName is name of hello event type that is being submitted tooLog Analytics
        static string LogName = "DemoExample";

        // You can use an optional field toospecify hello timestamp from hello data. If hello time field is not specified, Log Analytics assumes hello time is hello message ingestion time
        static string TimeStampField = "";

        static void Main()
        {
            // Create a hash for hello API signature
            var datestring = DateTime.UtcNow.ToString("r");
            string stringToHash = "POST\n" + json.Length + "\napplication/json\n" + "x-ms-date:" + datestring + "\n/api/logs";
            string hashedString = BuildSignature(stringToHash, sharedKey);
            string signature = "SharedKey " + customerId + ":" + hashedString;

            PostData(signature, datestring, json);
        }

        // Build hello API signature
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

        // Send a request toohello POST API endpoint
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

### <a name="python-sample"></a><span data-ttu-id="9f355-304">Esempio Python</span><span class="sxs-lookup"><span data-stu-id="9f355-304">Python sample</span></span>
```
import json
import requests
import datetime
import hashlib
import hmac
import base64

# Update hello customer ID tooyour Operations Management Suite workspace ID
customer_id = 'xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx'

# For hello shared key, use either hello primary or hello secondary Connected Sources client authentication key   
shared_key = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"

# hello log type is hello name of hello event that is being submitted
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

# Build hello API signature
def build_signature(customer_id, shared_key, date, content_length, method, content_type, resource):
    x_headers = 'x-ms-date:' + date
    string_to_hash = method + "\n" + str(content_length) + "\n" + content_type + "\n" + x_headers + "\n" + resource
    bytes_to_hash = bytes(string_to_hash).encode('utf-8')  
    decoded_key = base64.b64decode(shared_key)
    encoded_hash = base64.b64encode(hmac.new(decoded_key, bytes_to_hash, digestmod=hashlib.sha256).digest())
    authorization = "SharedKey {}:{}".format(customer_id,encoded_hash)
    return authorization

# Build and send a request toohello POST API
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

## <a name="next-steps"></a><span data-ttu-id="9f355-305">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9f355-305">Next steps</span></span>
- <span data-ttu-id="9f355-306">Hello utilizzare [API di ricerca Log](log-analytics-log-search-api.md) tooretrieve dati dall'archivio di Log Analitica hello.</span><span class="sxs-lookup"><span data-stu-id="9f355-306">Use hello [Log Search API](log-analytics-log-search-api.md) tooretrieve data from hello Log Analytics repository.</span></span>
