---
title: aaaWork con trigger e le associazioni in funzioni di Azure | Documenti Microsoft
description: Informazioni su come toouse attiva e le associazioni in funzioni di Azure tooconnect l'eventi tooonline esecuzione di codice e i servizi basati su cloud.
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: Funzioni di Azure, Funzioni, elaborazione eventi, webhook, calcolo dinamico, architettura senza server
ms.assetid: cbc7460a-4d8a-423f-a63e-1cd33fef7252
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/30/2017
ms.author: donnam
ms.openlocfilehash: eb2ebfca172fcc8c0f479adbcfec99e90fc33615
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-triggers-and-bindings-concepts"></a><span data-ttu-id="55b31-104">Concetti di Trigger e associazioni di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="55b31-104">Azure Functions triggers and bindings concepts</span></span>
<span data-ttu-id="55b31-105">Funzioni di Azure consente toowrite codice in risposta tooevents in Azure e altri servizi, tramite *trigger* e *associazioni*.</span><span class="sxs-lookup"><span data-stu-id="55b31-105">Azure Functions allows you toowrite code in response tooevents in Azure and other services, through *triggers* and *bindings*.</span></span> <span data-ttu-id="55b31-106">In questo articolo viene fornita una panoramica concettuale di trigger e associazioni per tutti i linguaggi di programmazione supportati.</span><span class="sxs-lookup"><span data-stu-id="55b31-106">This article is a conceptual overview of triggers and bindings for all supported programming languages.</span></span> <span data-ttu-id="55b31-107">Funzionalità comuni tooall associazioni sono descritte di seguito.</span><span class="sxs-lookup"><span data-stu-id="55b31-107">Features that are common tooall bindings are described here.</span></span>

## <a name="overview"></a><span data-ttu-id="55b31-108">Panoramica</span><span class="sxs-lookup"><span data-stu-id="55b31-108">Overview</span></span>

<span data-ttu-id="55b31-109">I trigger e le associazioni sono toodefine una modalità dichiarativa per la modalità in cui viene richiamata una funzione e i dati che funziona con.</span><span class="sxs-lookup"><span data-stu-id="55b31-109">Triggers and bindings are a declarative way toodefine how a function is invoked and what data it works with.</span></span> <span data-ttu-id="55b31-110">Un *trigger* definisce come viene richiamata una funzione.</span><span class="sxs-lookup"><span data-stu-id="55b31-110">A *trigger* defines how a function is invoked.</span></span> <span data-ttu-id="55b31-111">Una funzione deve avere esattamente un trigger.</span><span class="sxs-lookup"><span data-stu-id="55b31-111">A function must have exactly one trigger.</span></span> <span data-ttu-id="55b31-112">I trigger sono associati dati, ovvero in genere payload hello che ha attivato la funzione hello.</span><span class="sxs-lookup"><span data-stu-id="55b31-112">Triggers have associated data, which is usually hello payload that triggered hello function.</span></span> 

<span data-ttu-id="55b31-113">Input e output *associazioni* forniscono un toodata tooconnect modalità dichiarativa dall'interno del codice.</span><span class="sxs-lookup"><span data-stu-id="55b31-113">Input and output *bindings* provide a declarative way tooconnect toodata from within your code.</span></span> <span data-ttu-id="55b31-114">Tootriggers simile, specificare le stringhe di connessione e altre proprietà nella configurazione di funzione.</span><span class="sxs-lookup"><span data-stu-id="55b31-114">Similar tootriggers, you specify connection strings and other properties in your function configuration.</span></span> <span data-ttu-id="55b31-115">Le associazioni sono facoltative e una funzione può avere più associazioni di input e output.</span><span class="sxs-lookup"><span data-stu-id="55b31-115">Bindings are optional and a function can have multiple input and output bindings.</span></span> 

<span data-ttu-id="55b31-116">Tramite i trigger e le associazioni, è possibile scrivere codice che è più generico e non impostare come hardcoded i dettagli di hello dei servizi di hello con cui interagisce.</span><span class="sxs-lookup"><span data-stu-id="55b31-116">Using triggers and bindings, you can write code that is more generic and does not hardcode hello details of hello services with which it interacts.</span></span> <span data-ttu-id="55b31-117">I dati provenienti dai servizi diventano semplicemente valori di input per il codice della funzione.</span><span class="sxs-lookup"><span data-stu-id="55b31-117">Data coming from services simply become input values for your function code.</span></span> <span data-ttu-id="55b31-118">servizio di tooanother toooutput dati (ad esempio creando una nuova riga nell'archiviazione tabelle di Azure), utilizzare il valore restituito di hello del metodo hello.</span><span class="sxs-lookup"><span data-stu-id="55b31-118">toooutput data tooanother service (such as creating a new row in Azure Table Storage), use hello return value of hello method.</span></span> <span data-ttu-id="55b31-119">In alternativa, se è necessario toooutput più valori, utilizzare un oggetto di supporto.</span><span class="sxs-lookup"><span data-stu-id="55b31-119">Or, if you need toooutput multiple values, use a helper object.</span></span> <span data-ttu-id="55b31-120">I trigger e le associazioni presentano un **nome** proprietà, che è un identificatore è utilizzare nell'associazione di hello tooaccess codice.</span><span class="sxs-lookup"><span data-stu-id="55b31-120">Triggers and bindings have a **name** property, which is an identifier you use in your code tooaccess hello binding.</span></span>

<span data-ttu-id="55b31-121">È possibile configurare i trigger e le associazioni in hello **integrazione** scheda nel portale di Azure funzioni hello.</span><span class="sxs-lookup"><span data-stu-id="55b31-121">You can configure triggers and bindings in hello **Integrate** tab in hello Azure Functions portal.</span></span> <span data-ttu-id="55b31-122">In realtà hello, hello dell'interfaccia utente modifica un file denominato *function.json* file nella directory di funzione hello.</span><span class="sxs-lookup"><span data-stu-id="55b31-122">Under hello covers, hello UI modifies a file called *function.json* file in hello function directory.</span></span> <span data-ttu-id="55b31-123">È possibile modificare questo file modificando toohello **editor avanzato**.</span><span class="sxs-lookup"><span data-stu-id="55b31-123">You can edit this file by changing toohello **Advanced editor**.</span></span>

<span data-ttu-id="55b31-124">Hello nella tabella seguente mostra i trigger di hello e associazioni che sono supportate con le funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="55b31-124">hello following table shows hello triggers and bindings that are supported with Azure Functions.</span></span> 

[!INCLUDE [Full bindings table](../../includes/functions-bindings.md)]

### <a name="example-queue-trigger-and-table-output-binding"></a><span data-ttu-id="55b31-125">Esempio: trigger di coda e tabella di associazione di output</span><span class="sxs-lookup"><span data-stu-id="55b31-125">Example: queue trigger and table output binding</span></span>

<span data-ttu-id="55b31-126">Si supponga toowrite un tooAzure riga nuova archiviazione tabella ogni volta che viene visualizzato un nuovo messaggio nella coda di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="55b31-126">Suppose you want toowrite a new row tooAzure Table Storage whenever a new message appears in Azure Queue Storage.</span></span> <span data-ttu-id="55b31-127">Questo scenario può essere implementato tramite un trigger della coda di Azure e una tabella di associazione di output.</span><span class="sxs-lookup"><span data-stu-id="55b31-127">This scenario can be implemented using an Azure Queue trigger and a Table output binding.</span></span> 

<span data-ttu-id="55b31-128">Un trigger di coda richiede le seguenti informazioni in hello hello **integrazione** scheda:</span><span class="sxs-lookup"><span data-stu-id="55b31-128">A queue trigger requires hello following information in hello **Integrate** tab:</span></span>

* <span data-ttu-id="55b31-129">nome di Hello dell'impostazione di app hello che contiene una stringa di connessione account di archiviazione di hello per coda hello</span><span class="sxs-lookup"><span data-stu-id="55b31-129">hello name of hello app setting that contains hello storage account connection string for hello queue</span></span>
* <span data-ttu-id="55b31-130">nome della coda Hello</span><span class="sxs-lookup"><span data-stu-id="55b31-130">hello queue name</span></span>
* <span data-ttu-id="55b31-131">Hello, ad esempio l'identificatore del contenuto di hello tooread codice del messaggio della coda hello `order`.</span><span class="sxs-lookup"><span data-stu-id="55b31-131">hello identifier in your code tooread hello contents of hello queue message, such as `order`.</span></span>

<span data-ttu-id="55b31-132">toowrite tooAzure archiviazione tabelle, utilizzare un'associazione di output con hello seguenti dettagli:</span><span class="sxs-lookup"><span data-stu-id="55b31-132">toowrite tooAzure Table Storage, use an output binding with hello following details:</span></span>

* <span data-ttu-id="55b31-133">nome di Hello dell'impostazione di app hello che contiene una stringa di connessione account di archiviazione di hello per tabella hello</span><span class="sxs-lookup"><span data-stu-id="55b31-133">hello name of hello app setting that contains hello storage account connection string for hello table</span></span>
* <span data-ttu-id="55b31-134">nome della tabella Hello</span><span class="sxs-lookup"><span data-stu-id="55b31-134">hello table name</span></span>
* <span data-ttu-id="55b31-135">Identificatore Hello in toocreate il codice di output elementi o hello il valore restituito dalla funzione hello.</span><span class="sxs-lookup"><span data-stu-id="55b31-135">hello identifier in your code toocreate output items, or hello return value from hello function.</span></span>

<span data-ttu-id="55b31-136">Associazioni utilizzano le impostazioni dell'app per hello tooenforce di connessione stringhe best practice che *function.json* non contiene i segreti di servizio.</span><span class="sxs-lookup"><span data-stu-id="55b31-136">Bindings use app settings for connection strings tooenforce hello best practice that *function.json* does not contain service secrets.</span></span>

<span data-ttu-id="55b31-137">Quindi, utilizzare gli identificatori di hello toointegrate fornite con l'archiviazione di Azure nel codice.</span><span class="sxs-lookup"><span data-stu-id="55b31-137">Then, use hello identifiers you provided toointegrate with Azure Storage in your code.</span></span>

```cs
#r "Newtonsoft.Json"

using Newtonsoft.Json.Linq;

// From an incoming queue message that is a JSON object, add fields and write tooTable Storage
// hello method return value creates a new row in Table Storage
public static Person Run(JObject order, TraceWriter log)
{
    return new Person() { 
            PartitionKey = "Orders", 
            RowKey = Guid.NewGuid().ToString(),  
            Name = order["Name"].ToString(),
            MobileNumber = order["MobileNumber"].ToString() };  
}
 
public class Person
{
    public string PartitionKey { get; set; }
    public string RowKey { get; set; }
    public string Name { get; set; }
    public string MobileNumber { get; set; }
}
```

```javascript
// From an incoming queue message that is a JSON object, add fields and write tooTable Storage
// hello second parameter toocontext.done is used as hello value for hello new row
module.exports = function (context, order) {
    order.PartitionKey = "Orders";
    order.RowKey = generateRandomId(); 

    context.done(null, order);
};

function generateRandomId() {
    return Math.random().toString(36).substring(2, 15) +
        Math.random().toString(36).substring(2, 15);
}
```

<span data-ttu-id="55b31-138">Ecco hello *function.json* toohello precedente codice corrispondente.</span><span class="sxs-lookup"><span data-stu-id="55b31-138">Here is hello *function.json* that corresponds toohello preceding code.</span></span> <span data-ttu-id="55b31-139">Si noti che è possibile utilizzare configurazione stesso, indipendentemente dal linguaggio hello di implementazione della funzione hello di hello.</span><span class="sxs-lookup"><span data-stu-id="55b31-139">Note that hello same configuration can be used, regardless of hello language of hello function implementation.</span></span>

```json
{
  "bindings": [
    {
      "name": "order",
      "type": "queueTrigger",
      "direction": "in",
      "queueName": "myqueue-items",
      "connection": "MY_STORAGE_ACCT_APP_SETTING"
    },
    {
      "name": "$return",
      "type": "table",
      "direction": "out",
      "tableName": "outTable",
      "connection": "MY_TABLE_STORAGE_ACCT_APP_SETTING"
    }
  ]
}
```
<span data-ttu-id="55b31-140">contenuto di hello tooview e modifica di *function.json* in hello portale di Azure, fare clic su hello **editor avanzato** opzione hello **integrazione** scheda della funzione.</span><span class="sxs-lookup"><span data-stu-id="55b31-140">tooview and edit hello contents of *function.json* in hello Azure portal, click hello **Advanced editor** option on hello **Integrate** tab of your function.</span></span>

<span data-ttu-id="55b31-141">Per altri esempi di codice e informazioni dettagliate sull'integrazione con archiviazione di Azure, vedere [Associazioni del BLOB del servizio di archiviazione di Funzioni di Azure](functions-bindings-storage.md).</span><span class="sxs-lookup"><span data-stu-id="55b31-141">For more code examples and details on integrating with Azure Storage, see [Azure Functions triggers and bindings for Azure Storage](functions-bindings-storage.md).</span></span>

### <a name="binding-direction"></a><span data-ttu-id="55b31-142">Direzione dell'associazione</span><span class="sxs-lookup"><span data-stu-id="55b31-142">Binding direction</span></span>

<span data-ttu-id="55b31-143">Tutti i trigger e le associazioni hanno una proprietà `direction`:</span><span class="sxs-lookup"><span data-stu-id="55b31-143">All triggers and bindings have a `direction` property:</span></span>

- <span data-ttu-id="55b31-144">Per i trigger, è sempre direzione hello`in`</span><span class="sxs-lookup"><span data-stu-id="55b31-144">For triggers, hello direction is always `in`</span></span>
- <span data-ttu-id="55b31-145">Le associazioni di input e di output usano `in` e `out`</span><span class="sxs-lookup"><span data-stu-id="55b31-145">Input and output bindings use `in` and `out`</span></span>
- <span data-ttu-id="55b31-146">Alcune associazioni supportano una direzione speciale `inout`.</span><span class="sxs-lookup"><span data-stu-id="55b31-146">Some bindings support a special direction `inout`.</span></span> <span data-ttu-id="55b31-147">Se si utilizza `inout`, solo hello **editor avanzato** è disponibile in hello **integrazione** scheda.</span><span class="sxs-lookup"><span data-stu-id="55b31-147">If you use `inout`, only hello **Advanced editor** is available in hello **Integrate** tab.</span></span>

## <a name="using-hello-function-return-type-tooreturn-a-single-output"></a><span data-ttu-id="55b31-148">Utilizzando tooreturn tipo restituito di funzione hello un singolo output</span><span class="sxs-lookup"><span data-stu-id="55b31-148">Using hello function return type tooreturn a single output</span></span>

<span data-ttu-id="55b31-149">Hello esempio precedente viene illustrato come toouse hello funzione valore restituito tooprovide output tooa binding, che è possibile utilizzare il parametro di nome speciale hello `$return`.</span><span class="sxs-lookup"><span data-stu-id="55b31-149">hello preceding example shows how toouse hello function return value tooprovide output tooa binding, which is achieved by using hello special name parameter `$return`.</span></span> <span data-ttu-id="55b31-150">(Questa opzione è supportata solo nei linguaggi che dispongono di un valore restituito, ad esempio C#, JavaScript e F#). Se una funzione include più associazioni di output, utilizzare `$return` per solo una delle associazioni di output di hello.</span><span class="sxs-lookup"><span data-stu-id="55b31-150">(This is only supported in languages that have a return value, such as C#, JavaScript, and F#.) If a function has multiple output bindings, use `$return` for only one of hello output bindings.</span></span> 

```json
// excerpt of function.json
{
    "name": "$return",
    "type": "blob",
    "direction": "out",
    "path": "output-container/{id}"
}
```

<span data-ttu-id="55b31-151">esempi di Hello seguente mostra come restituiscono tipi vengono utilizzati con le associazioni di output in c#, JavaScript e F #.</span><span class="sxs-lookup"><span data-stu-id="55b31-151">hello examples below show how return types are used with output bindings in C#, JavaScript, and F#.</span></span>

```cs
// C# example: use method return value for output binding
public static string Run(WorkItem input, TraceWriter log)
{
    string json = string.Format("{{ \"id\": \"{0}\" }}", input.Id);
    log.Info($"C# script processed queue message. Item={json}");
    return json;
}
```

```cs
// C# example: async method, using return value for output binding
public static Task<string> Run(WorkItem input, TraceWriter log)
{
    string json = string.Format("{{ \"id\": \"{0}\" }}", input.Id);
    log.Info($"C# script processed queue message. Item={json}");
    return json;
}
```

```javascript
// JavaScript: return a value in hello second parameter toocontext.done
module.exports = function (context, input) {
    var json = JSON.stringify(input);
    context.log('Node.js script processed queue message', json);
    context.done(null, json);
}
```

```fsharp
// F# example: use return value for output binding
let Run(input: WorkItem, log: TraceWriter) =
    let json = String.Format("{{ \"id\": \"{0}\" }}", input.Id)   
    log.Info(sprintf "F# script processed queue message '%s'" json)
    json
```

## <a name="binding-datatype-property"></a><span data-ttu-id="55b31-152">Proprietà Binding dataType</span><span class="sxs-lookup"><span data-stu-id="55b31-152">Binding dataType property</span></span>

<span data-ttu-id="55b31-153">In .NET, utilizzare hello tipi toodefine hello data type per dati di input.</span><span class="sxs-lookup"><span data-stu-id="55b31-153">In .NET, use hello types toodefine hello data type for input data.</span></span> <span data-ttu-id="55b31-154">Ad esempio, utilizzare `string` toobind toohello testo di un trigger di coda e un tooread di matrice di byte in formato binario.</span><span class="sxs-lookup"><span data-stu-id="55b31-154">For instance, use `string` toobind toohello text of a queue trigger and a byte array tooread as binary.</span></span>

<span data-ttu-id="55b31-155">Per le lingue che vengono digitate in modo dinamico, ad esempio JavaScript, usare hello `dataType` proprietà nella definizione di associazioni hello.</span><span class="sxs-lookup"><span data-stu-id="55b31-155">For languages that are dynamically typed such as JavaScript, use hello `dataType` property in hello binding definition.</span></span> <span data-ttu-id="55b31-156">Ad esempio, tooread hello contenuto di una richiesta HTTP in formato binario, utilizzare il tipo di hello `binary`:</span><span class="sxs-lookup"><span data-stu-id="55b31-156">For example, tooread hello content of an HTTP request in binary format, use hello type `binary`:</span></span>

```json
{
    "type": "httpTrigger",
    "name": "req",
    "direction": "in",
    "dataType": "binary"
}
```

<span data-ttu-id="55b31-157">Altre opzioni per `dataType` sono `stream` e `string`.</span><span class="sxs-lookup"><span data-stu-id="55b31-157">Other options for `dataType` are `stream` and `string`.</span></span>

## <a name="resolving-app-settings"></a><span data-ttu-id="55b31-158">Risoluzione di impostazioni app</span><span class="sxs-lookup"><span data-stu-id="55b31-158">Resolving app settings</span></span>
<span data-ttu-id="55b31-159">Come procedura consigliata, i segreti e le stringhe di connessione devono essere gestiti tramite le impostazioni dell'app, invece dei file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="55b31-159">As a best practice, secrets and connection strings should be managed using app settings, rather than configuration files.</span></span> <span data-ttu-id="55b31-160">Questo limita accesso toothese segreti e rende sicuro toostore *function.json* in un repository di controllo del codice sorgente pubblico.</span><span class="sxs-lookup"><span data-stu-id="55b31-160">This limits access toothese secrets and makes it safe toostore *function.json* in a public source control repository.</span></span>

<span data-ttu-id="55b31-161">Le impostazioni dell'App sono utili anche ogni volta che si desidera configurazione toochange basata sull'ambiente hello.</span><span class="sxs-lookup"><span data-stu-id="55b31-161">App settings are also useful whenever you want toochange configuration based on hello environment.</span></span> <span data-ttu-id="55b31-162">In un ambiente di test, ad esempio, è consigliabile toomonitor un diverso contenitore di archiviazione blob o coda.</span><span class="sxs-lookup"><span data-stu-id="55b31-162">For example, in a test environment, you may want toomonitor a different queue or blob storage container.</span></span>

<span data-ttu-id="55b31-163">Le impostazioni dell'app vengono risolte ogni volta che un valore è racchiuso tra simboli di percentuale, ad esempio `%MyAppSetting%`.</span><span class="sxs-lookup"><span data-stu-id="55b31-163">App settings are resolved whenever a value is enclosed in percent signs, such as `%MyAppSetting%`.</span></span> <span data-ttu-id="55b31-164">Si noti che hello `connection` proprietà delle associazioni e i trigger è un caso speciale e risolve automaticamente i valori come impostazioni dell'app.</span><span class="sxs-lookup"><span data-stu-id="55b31-164">Note that hello `connection` property of triggers and bindings is a special case and automatically resolves values as app settings.</span></span> 

<span data-ttu-id="55b31-165">esempio Hello è un trigger di coda che utilizza un'impostazione app `%input-queue-name%` toodefine hello coda tootrigger in.</span><span class="sxs-lookup"><span data-stu-id="55b31-165">hello following example is a queue trigger that uses an app setting `%input-queue-name%` toodefine hello queue tootrigger on.</span></span>

```json
{
  "bindings": [
    {
      "name": "order",
      "type": "queueTrigger",
      "direction": "in",
      "queueName": "%input-queue-name%",
      "connection": "MY_STORAGE_ACCT_APP_SETTING"
    }
  ]
}
```

## <a name="trigger-metadata-properties"></a><span data-ttu-id="55b31-166">Proprietà dei metadati di trigger</span><span class="sxs-lookup"><span data-stu-id="55b31-166">Trigger metadata properties</span></span>

<span data-ttu-id="55b31-167">In aggiunta toohello payload dei dati forniti da un trigger (ad esempio hello coda dei messaggi che ha attivato una funzione), molti trigger fornire i valori di metadati aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="55b31-167">In addition toohello data payload provided by a trigger (such as hello queue message that triggered a function), many triggers provide additional metadata values.</span></span> <span data-ttu-id="55b31-168">Questi valori possono essere utilizzati come parametri di input in c# e F # o proprietà hello `context.bindings` oggetto in JavaScript.</span><span class="sxs-lookup"><span data-stu-id="55b31-168">These values can be used as input parameters in C# and F# or properties on hello `context.bindings` object in JavaScript.</span></span> 

<span data-ttu-id="55b31-169">Ad esempio, un trigger di coda supporta hello le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="55b31-169">For example, a queue trigger supports hello following properties:</span></span>

* <span data-ttu-id="55b31-170">QueueTrigge: attivazione del contenuto del messaggio, se una stringa valida</span><span class="sxs-lookup"><span data-stu-id="55b31-170">QueueTrigger - triggering message content if a valid string</span></span>
* <span data-ttu-id="55b31-171">DequeueCount</span><span class="sxs-lookup"><span data-stu-id="55b31-171">DequeueCount</span></span>
* <span data-ttu-id="55b31-172">ExpirationTime</span><span class="sxs-lookup"><span data-stu-id="55b31-172">ExpirationTime</span></span>
* <span data-ttu-id="55b31-173">ID</span><span class="sxs-lookup"><span data-stu-id="55b31-173">Id</span></span>
* <span data-ttu-id="55b31-174">InsertionTime</span><span class="sxs-lookup"><span data-stu-id="55b31-174">InsertionTime</span></span>
* <span data-ttu-id="55b31-175">NextVisibleTime</span><span class="sxs-lookup"><span data-stu-id="55b31-175">NextVisibleTime</span></span>
* <span data-ttu-id="55b31-176">PopReceipt</span><span class="sxs-lookup"><span data-stu-id="55b31-176">PopReceipt</span></span>

<span data-ttu-id="55b31-177">Dettagli delle proprietà dei metadati per tutti i trigger sono descritti nell'argomento di riferimento corrispondente hello.</span><span class="sxs-lookup"><span data-stu-id="55b31-177">Details of metadata properties for each trigger are described in hello corresponding reference topic.</span></span> <span data-ttu-id="55b31-178">La documentazione è disponibile anche in hello **integrazione** scheda della finestra del portale hello hello **documentazione** sezione sotto l'area di configurazione dell'associazione hello.</span><span class="sxs-lookup"><span data-stu-id="55b31-178">Documentation is also available in hello **Integrate** tab of hello portal, in hello **Documentation** section below hello binding configuration area.</span></span>  

<span data-ttu-id="55b31-179">Ad esempio, poiché i trigger di blob presentano alcuni ritardi, è possibile utilizzare un toorun trigger coda la funzione (vedere [Trigger di archiviazione Blob](functions-bindings-storage-blob.md#storage-blob-trigger).</span><span class="sxs-lookup"><span data-stu-id="55b31-179">For example, since blob triggers have some delays, you can use a queue trigger toorun your function (see [Blob Storage Trigger](functions-bindings-storage-blob.md#storage-blob-trigger).</span></span> <span data-ttu-id="55b31-180">messaggio della coda di Hello conterrebbe hello blob filename tootrigger in.</span><span class="sxs-lookup"><span data-stu-id="55b31-180">hello queue message would contain hello blob filename tootrigger on.</span></span> <span data-ttu-id="55b31-181">Utilizzo di hello `queueTrigger` proprietà dei metadati, è possibile specificare questo comportamento in configurazione, anziché il codice.</span><span class="sxs-lookup"><span data-stu-id="55b31-181">Using hello `queueTrigger` metadata property, you can specify this behavior all in your configuration, rather than your code.</span></span>

```json
  "bindings": [
    {
      "name": "myQueueItem",
      "type": "queueTrigger",
      "queueName": "myqueue-items",
      "connection": "MyStorageConnection",
    },
    {
      "name": "myInputBlob",
      "type": "blob",
      "path": "samples-workitems/{queueTrigger}",
      "direction": "in",
      "connection": "MyStorageConnection"
    }
  ]
```

<span data-ttu-id="55b31-182">Proprietà di metadati da un trigger possono essere utilizzate anche un *espressione dell'associazione* per l'associazione di un altro, come hello descritto nella sezione seguente.</span><span class="sxs-lookup"><span data-stu-id="55b31-182">Metadata properties from a trigger can also be used in a *binding expression* for another binding, as described in hello following section.</span></span>

## <a name="binding-expressions-and-patterns"></a><span data-ttu-id="55b31-183">Modelli ed espressioni di associazione</span><span class="sxs-lookup"><span data-stu-id="55b31-183">Binding expressions and patterns</span></span>

<span data-ttu-id="55b31-184">Una delle funzionalità più potenti di hello di trigger e le associazioni è *espressioni di associazione*.</span><span class="sxs-lookup"><span data-stu-id="55b31-184">One of hello most powerful features of triggers and bindings is *binding expressions*.</span></span> <span data-ttu-id="55b31-185">All'interno dell'associazione, è possibile definire delle espressioni di modello che possono quindi essere usate in altre associazioni o nel codice.</span><span class="sxs-lookup"><span data-stu-id="55b31-185">Within your binding, you can define pattern expressions which can then be used in other bindings or your code.</span></span> <span data-ttu-id="55b31-186">Metadati di trigger possono essere utilizzati anche nell'associazione di espressioni, come illustrato nell'esempio hello nella precedente sezione hello.</span><span class="sxs-lookup"><span data-stu-id="55b31-186">Trigger metadata can also be used in binding expressions, as show in hello sample in hello preceding section.</span></span>

<span data-ttu-id="55b31-187">Ad esempio, si supponga di voler tooresize immagini nel contenitore di archiviazione blob specifico, simile toohello **dimensioni immagine** modello hello **nuova funzione** pagina.</span><span class="sxs-lookup"><span data-stu-id="55b31-187">For example, suppose you want tooresize images in particular blob storage container, similar toohello **Image Resizer** template in hello **New Function** page.</span></span> <span data-ttu-id="55b31-188">Andare troppo**nuova funzione** -> lingua **c#** -> Scenario **esempi** -> **ImageResizer CSharp**.</span><span class="sxs-lookup"><span data-stu-id="55b31-188">Go too**New Function** -> Language **C#** -> Scenario **Samples** -> **ImageResizer-CSharp**.</span></span> 

<span data-ttu-id="55b31-189">Ecco hello *function.json* definizione:</span><span class="sxs-lookup"><span data-stu-id="55b31-189">Here is hello *function.json* definition:</span></span>

```json
{
  "bindings": [
    {
      "name": "image",
      "type": "blobTrigger",
      "path": "sample-images/{filename}",
      "direction": "in",
      "connection": "MyStorageConnection"
    },
    {
      "name": "imageSmall",
      "type": "blob",
      "path": "sample-images-sm/{filename}",
      "direction": "out",
      "connection": "MyStorageConnection"
    }
  ],
}
```

<span data-ttu-id="55b31-190">Si noti che hello `filename` parametro viene utilizzato nella definizione del trigger blob hello nonché a blob hello associazione di output.</span><span class="sxs-lookup"><span data-stu-id="55b31-190">Notice that hello `filename` parameter is used in both hello blob trigger definition as well as hello blob output binding.</span></span> <span data-ttu-id="55b31-191">Questo parametro può essere usato anche nel codice della funzione.</span><span class="sxs-lookup"><span data-stu-id="55b31-191">This parameter can also be used in function code.</span></span>

```csharp
// C# example of binding too{filename}
public static void Run(Stream image, string filename, Stream imageSmall, TraceWriter log)  
{
    log.Info($"Blob trigger processing: {filename}");
    // ...
} 
```

<!--TODO: add JavaScript example -->
<!-- Blocked by bug https://github.com/Azure/Azure-Functions/issues/248 -->


### <a name="random-guids"></a><span data-ttu-id="55b31-192">GUID casuali</span><span class="sxs-lookup"><span data-stu-id="55b31-192">Random GUIDs</span></span>
<span data-ttu-id="55b31-193">Funzioni di Azure fornisce una sintassi pratici per la generazione di GUID nelle associazioni, tramite hello `{rand-guid}` espressione dell'associazione.</span><span class="sxs-lookup"><span data-stu-id="55b31-193">Azure Functions provides a convenience syntax for generating GUIDs in your bindings, through hello `{rand-guid}` binding expression.</span></span> <span data-ttu-id="55b31-194">Hello esempio seguente viene utilizzato questo toogenerate un nome univoco di blob:</span><span class="sxs-lookup"><span data-stu-id="55b31-194">hello following example uses this toogenerate a unique blob name:</span></span> 

```json
{
  "type": "blob",
  "name": "blobOutput",
  "direction": "out",
  "path": "my-output-container/{rand-guid}"
}
```

### <a name="current-time"></a><span data-ttu-id="55b31-195">Ora corrente</span><span class="sxs-lookup"><span data-stu-id="55b31-195">Current time</span></span>

<span data-ttu-id="55b31-196">È possibile utilizzare l'espressione di associazione hello `DateTime`, che viene risolta troppo`DateTime.UtcNow`.</span><span class="sxs-lookup"><span data-stu-id="55b31-196">You can use hello binding expression `DateTime`, which resolves too`DateTime.UtcNow`.</span></span>

```json
{
  "type": "blob",
  "name": "blobOutput",
  "direction": "out",
  "path": "my-output-container/{DateTime}"
}
```

## <a name="bind-toocustom-input-properties-in-a-binding-expression"></a><span data-ttu-id="55b31-197">Associare le proprietà di input toocustom in un'espressione di associazione</span><span class="sxs-lookup"><span data-stu-id="55b31-197">Bind toocustom input properties in a binding expression</span></span>

<span data-ttu-id="55b31-198">Associazione di espressioni può anche fare riferimento alle proprietà che sono definite nel payload di hello trigger stesso.</span><span class="sxs-lookup"><span data-stu-id="55b31-198">Binding expressions can also reference properties that are defined in hello trigger payload itself.</span></span> <span data-ttu-id="55b31-199">Ad esempio, è consigliabile toodynamically file di archiviazione blob di tooa binding da un nome specificato in un webhook.</span><span class="sxs-lookup"><span data-stu-id="55b31-199">For example, you may want toodynamically bind tooa blob storage file from a filename provided in a webhook.</span></span>

<span data-ttu-id="55b31-200">Ad esempio, hello seguente *function.json* Usa una proprietà denominata `BlobName` dal payload trigger hello:</span><span class="sxs-lookup"><span data-stu-id="55b31-200">For example, hello following *function.json* uses a property called `BlobName` from hello trigger payload:</span></span>

```json
{
  "bindings": [
    {
      "name": "info",
      "type": "httpTrigger",
      "direction": "in",
      "webHookType": "genericJson",
    },
    {
      "name": "blobContents",
      "type": "blob",
      "direction": "in",
      "path": "strings/{BlobName}",
      "connection": "AzureWebJobsStorage"
    },
    {
      "name": "res",
      "type": "http",
      "direction": "out"
    }
  ]
}
```

<span data-ttu-id="55b31-201">tooaccomplish questo in c# e F #, è necessario definire un POCO che definisce i campi di hello che verranno deserializzati payload trigger hello.</span><span class="sxs-lookup"><span data-stu-id="55b31-201">tooaccomplish this in C# and F#, you must define a POCO that defines hello fields that will be deserialized in hello trigger payload.</span></span>

```csharp
using System.Net;

public class BlobInfo
{
    public string BlobName { get; set; }
}
  
public static HttpResponseMessage Run(HttpRequestMessage req, BlobInfo info, string blobContents)
{
    if (blobContents == null) {
        return req.CreateResponse(HttpStatusCode.NotFound);
    } 

    return req.CreateResponse(HttpStatusCode.OK, new {
        data = $"{blobContents}"
    });
}
```

<span data-ttu-id="55b31-202">In JavaScript, viene eseguita automaticamente la deserializzazione JSON ed è possibile utilizzare direttamente le proprietà di hello.</span><span class="sxs-lookup"><span data-stu-id="55b31-202">In JavaScript, JSON deserialization is automatically performed and you can use hello properties directly.</span></span>

```javascript
module.exports = function (context, info) {
    if ('BlobName' in info) {
        context.res = {
            body: { 'data': context.bindings.blobContents }
        }
    }
    else {
        context.res = {
            status: 404
        };
    }
    context.done();
}
```

## <a name="configuring-binding-data-at-runtime"></a><span data-ttu-id="55b31-203">Configurazione dell'associazione di dati in fase di runtime</span><span class="sxs-lookup"><span data-stu-id="55b31-203">Configuring binding data at runtime</span></span>

<span data-ttu-id="55b31-204">In c# e altri linguaggi .NET, è possibile utilizzare un modello di associazione imperativa, come toohello anziché associazioni dichiarativa *function.json*.</span><span class="sxs-lookup"><span data-stu-id="55b31-204">In C# and other .NET languages, you can use an imperative binding pattern, as opposed toohello declarative bindings in *function.json*.</span></span> <span data-ttu-id="55b31-205">Associazione imperativo è utile quando i parametri di associazione necessario toobe calcolato in fase di runtime anziché di progettazione.</span><span class="sxs-lookup"><span data-stu-id="55b31-205">Imperative binding is useful when binding parameters need toobe computed at runtime rather than design time.</span></span> <span data-ttu-id="55b31-206">toolearn informazioni, vedere [associazione in fase di esecuzione tramite i binding imperativo](functions-reference-csharp.md#imperative-bindings) nella Guida di riferimento per sviluppatori hello in c#.</span><span class="sxs-lookup"><span data-stu-id="55b31-206">toolearn more, see [Binding at runtime via imperative bindings](functions-reference-csharp.md#imperative-bindings) in hello C# developer reference.</span></span>

## <a name="next-steps"></a><span data-ttu-id="55b31-207">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="55b31-207">Next steps</span></span>
<span data-ttu-id="55b31-208">Per ulteriori informazioni su una particolare associazione, vedere hello seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="55b31-208">For more information on a specific binding, see hello following articles:</span></span>

- [<span data-ttu-id="55b31-209">HTTP e webhook</span><span class="sxs-lookup"><span data-stu-id="55b31-209">HTTP and webhooks</span></span>](functions-bindings-http-webhook.md)
- [<span data-ttu-id="55b31-210">Timer</span><span class="sxs-lookup"><span data-stu-id="55b31-210">Timer</span></span>](functions-bindings-timer.md)
- [<span data-ttu-id="55b31-211">Archiviazione code</span><span class="sxs-lookup"><span data-stu-id="55b31-211">Queue storage</span></span>](functions-bindings-storage-queue.md)
- [<span data-ttu-id="55b31-212">Archiviazione BLOB</span><span class="sxs-lookup"><span data-stu-id="55b31-212">Blob storage</span></span>](functions-bindings-storage-blob.md)
- [<span data-ttu-id="55b31-213">Archiviazione tabelle</span><span class="sxs-lookup"><span data-stu-id="55b31-213">Table storage</span></span>](functions-bindings-storage-table.md)
- [<span data-ttu-id="55b31-214">Hub eventi</span><span class="sxs-lookup"><span data-stu-id="55b31-214">Event Hub</span></span>](functions-bindings-event-hubs.md)
- [<span data-ttu-id="55b31-215">Bus di servizio</span><span class="sxs-lookup"><span data-stu-id="55b31-215">Service Bus</span></span>](functions-bindings-service-bus.md)
- [<span data-ttu-id="55b31-216">Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="55b31-216">Cosmos DB</span></span>](functions-bindings-documentdb.md)
- [<span data-ttu-id="55b31-217">SendGrid</span><span class="sxs-lookup"><span data-stu-id="55b31-217">SendGrid</span></span>](functions-bindings-sendgrid.md)
- [<span data-ttu-id="55b31-218">Twilio</span><span class="sxs-lookup"><span data-stu-id="55b31-218">Twilio</span></span>](functions-bindings-twilio.md)
- [<span data-ttu-id="55b31-219">Hub di notifica</span><span class="sxs-lookup"><span data-stu-id="55b31-219">Notification Hubs</span></span>](functions-bindings-notification-hubs.md)
- [<span data-ttu-id="55b31-220">App per dispositivi mobili</span><span class="sxs-lookup"><span data-stu-id="55b31-220">Mobile Apps</span></span>](functions-bindings-mobile-apps.md)
- [<span data-ttu-id="55b31-221">File esterno</span><span class="sxs-lookup"><span data-stu-id="55b31-221">External file</span></span>](functions-bindings-external-file.md)
