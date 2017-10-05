---
title: Usare trigger e associazioni in Funzioni di Azure | Microsoft Docs
description: Informazioni su come usare trigger e associazioni in Funzioni di Azure per connettere l'esecuzione del codice a eventi online e servizi basati su cloud.
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
ms.openlocfilehash: cc41debb2523df77be4db05817a4c7ac55604439
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-functions-triggers-and-bindings-concepts"></a><span data-ttu-id="b1bd0-104">Concetti di Trigger e associazioni di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="b1bd0-104">Azure Functions triggers and bindings concepts</span></span>
<span data-ttu-id="b1bd0-105">Funzioni di Azure consente di scrivere codice in risposta agli eventi in Azure e in altri servizi, tramite *trigger* e *associazioni*.</span><span class="sxs-lookup"><span data-stu-id="b1bd0-105">Azure Functions allows you to write code in response to events in Azure and other services, through *triggers* and *bindings*.</span></span> <span data-ttu-id="b1bd0-106">In questo articolo viene fornita una panoramica concettuale di trigger e associazioni per tutti i linguaggi di programmazione supportati.</span><span class="sxs-lookup"><span data-stu-id="b1bd0-106">This article is a conceptual overview of triggers and bindings for all supported programming languages.</span></span> <span data-ttu-id="b1bd0-107">Le funzionalità comuni a tutte le associazioni sono descritte di seguito.</span><span class="sxs-lookup"><span data-stu-id="b1bd0-107">Features that are common to all bindings are described here.</span></span>

## <a name="overview"></a><span data-ttu-id="b1bd0-108">Panoramica</span><span class="sxs-lookup"><span data-stu-id="b1bd0-108">Overview</span></span>

<span data-ttu-id="b1bd0-109">I trigger e le associazioni sono un modo dichiarativo per definire come viene invocata una funzione e con quali dati opera.</span><span class="sxs-lookup"><span data-stu-id="b1bd0-109">Triggers and bindings are a declarative way to define how a function is invoked and what data it works with.</span></span> <span data-ttu-id="b1bd0-110">Un *trigger* definisce come viene richiamata una funzione.</span><span class="sxs-lookup"><span data-stu-id="b1bd0-110">A *trigger* defines how a function is invoked.</span></span> <span data-ttu-id="b1bd0-111">Una funzione deve avere esattamente un trigger.</span><span class="sxs-lookup"><span data-stu-id="b1bd0-111">A function must have exactly one trigger.</span></span> <span data-ttu-id="b1bd0-112">I trigger hanno dei dati associati, ovvero in genere il payload che ha attivato la funzione.</span><span class="sxs-lookup"><span data-stu-id="b1bd0-112">Triggers have associated data, which is usually the payload that triggered the function.</span></span> 

<span data-ttu-id="b1bd0-113">Le *associazioni* di input e output forniscono una modalità dichiarativa per connettersi ai dati dall'interno del codice.</span><span class="sxs-lookup"><span data-stu-id="b1bd0-113">Input and output *bindings* provide a declarative way to connect to data from within your code.</span></span> <span data-ttu-id="b1bd0-114">Analogamente ai trigger, specificare le stringhe di connessione e le altre proprietà nella configurazione della funzione.</span><span class="sxs-lookup"><span data-stu-id="b1bd0-114">Similar to triggers, you specify connection strings and other properties in your function configuration.</span></span> <span data-ttu-id="b1bd0-115">Le associazioni sono facoltative e una funzione può avere più associazioni di input e output.</span><span class="sxs-lookup"><span data-stu-id="b1bd0-115">Bindings are optional and a function can have multiple input and output bindings.</span></span> 

<span data-ttu-id="b1bd0-116">Usando i trigger e le associazioni, è possibile scrivere codice più generico e non impostare come hardcoded i dettagli dei servizi con cui interagisce.</span><span class="sxs-lookup"><span data-stu-id="b1bd0-116">Using triggers and bindings, you can write code that is more generic and does not hardcode the details of the services with which it interacts.</span></span> <span data-ttu-id="b1bd0-117">I dati provenienti dai servizi diventano semplicemente valori di input per il codice della funzione.</span><span class="sxs-lookup"><span data-stu-id="b1bd0-117">Data coming from services simply become input values for your function code.</span></span> <span data-ttu-id="b1bd0-118">Per restituire i dati a un altro servizio (ad esempio la creazione di una nuova riga nell'archiviazione tabelle di Azure), usare il valore restituito del metodo.</span><span class="sxs-lookup"><span data-stu-id="b1bd0-118">To output data to another service (such as creating a new row in Azure Table Storage), use the return value of the method.</span></span> <span data-ttu-id="b1bd0-119">In alternativa, se è necessario restituire più valori, usare un oggetto di supporto.</span><span class="sxs-lookup"><span data-stu-id="b1bd0-119">Or, if you need to output multiple values, use a helper object.</span></span> <span data-ttu-id="b1bd0-120">I trigger e le associazioni presentano una proprietà **nome**, che è un identificatore che si usa nel codice per accedere all'associazione.</span><span class="sxs-lookup"><span data-stu-id="b1bd0-120">Triggers and bindings have a **name** property, which is an identifier you use in your code to access the binding.</span></span>

<span data-ttu-id="b1bd0-121">È possibile configurare i trigger e le associazioni nella scheda **Integrazione** nel portale delle Funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="b1bd0-121">You can configure triggers and bindings in the **Integrate** tab in the Azure Functions portal.</span></span> <span data-ttu-id="b1bd0-122">Dietro le quinte, l'interfaccia utente modifica un file denominato file *function.json* nella directory della funzione.</span><span class="sxs-lookup"><span data-stu-id="b1bd0-122">Under the covers, the UI modifies a file called *function.json* file in the function directory.</span></span> <span data-ttu-id="b1bd0-123">È possibile modificare questo file passando all'**Editor avanzato**.</span><span class="sxs-lookup"><span data-stu-id="b1bd0-123">You can edit this file by changing to the **Advanced editor**.</span></span>

<span data-ttu-id="b1bd0-124">La tabella seguente mostra i trigger e le associazioni supportate con le Funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="b1bd0-124">The following table shows the triggers and bindings that are supported with Azure Functions.</span></span> 

[!INCLUDE [Full bindings table](../../includes/functions-bindings.md)]

### <a name="example-queue-trigger-and-table-output-binding"></a><span data-ttu-id="b1bd0-125">Esempio: trigger di coda e tabella di associazione di output</span><span class="sxs-lookup"><span data-stu-id="b1bd0-125">Example: queue trigger and table output binding</span></span>

<span data-ttu-id="b1bd0-126">Si supponga di voler scrivere una nuova riga in archiviazione tabelle di Azure ogni volta che viene visualizzato un messaggio nuovo in archiviazione code di Azure.</span><span class="sxs-lookup"><span data-stu-id="b1bd0-126">Suppose you want to write a new row to Azure Table Storage whenever a new message appears in Azure Queue Storage.</span></span> <span data-ttu-id="b1bd0-127">Questo scenario può essere implementato tramite un trigger della coda di Azure e una tabella di associazione di output.</span><span class="sxs-lookup"><span data-stu-id="b1bd0-127">This scenario can be implemented using an Azure Queue trigger and a Table output binding.</span></span> 

<span data-ttu-id="b1bd0-128">Un trigger della coda richiede le informazioni seguenti nella scheda **Integrazione**:</span><span class="sxs-lookup"><span data-stu-id="b1bd0-128">A queue trigger requires the following information in the **Integrate** tab:</span></span>

* <span data-ttu-id="b1bd0-129">Il nome dell'impostazione dell'app che contiene la stringa di connessione dell'account di archiviazione per la coda</span><span class="sxs-lookup"><span data-stu-id="b1bd0-129">The name of the app setting that contains the storage account connection string for the queue</span></span>
* <span data-ttu-id="b1bd0-130">Il nome della coda</span><span class="sxs-lookup"><span data-stu-id="b1bd0-130">The queue name</span></span>
* <span data-ttu-id="b1bd0-131">L'identificatore nel codice per leggere il contenuto del messaggio in coda, ad esempio `order`.</span><span class="sxs-lookup"><span data-stu-id="b1bd0-131">The identifier in your code to read the contents of the queue message, such as `order`.</span></span>

<span data-ttu-id="b1bd0-132">Per scrivere in archiviazione tabelle di Azure, usare un'associazione di output con i dettagli seguenti:</span><span class="sxs-lookup"><span data-stu-id="b1bd0-132">To write to Azure Table Storage, use an output binding with the following details:</span></span>

* <span data-ttu-id="b1bd0-133">Il nome dell'impostazione dell'app che contiene la stringa di connessione dell'account di archiviazione per la tabella</span><span class="sxs-lookup"><span data-stu-id="b1bd0-133">The name of the app setting that contains the storage account connection string for the table</span></span>
* <span data-ttu-id="b1bd0-134">Il nome della tabella</span><span class="sxs-lookup"><span data-stu-id="b1bd0-134">The table name</span></span>
* <span data-ttu-id="b1bd0-135">L'identificatore nel codice per creare elementi di output o il valore restituito dalla funzione.</span><span class="sxs-lookup"><span data-stu-id="b1bd0-135">The identifier in your code to create output items, or the return value from the function.</span></span>

<span data-ttu-id="b1bd0-136">Le associazioni usano le impostazioni app per le stringhe di connessione per applicare la migliore pratica in base alla quale *function.json* non contiene i segreti di servizio.</span><span class="sxs-lookup"><span data-stu-id="b1bd0-136">Bindings use app settings for connection strings to enforce the best practice that *function.json* does not contain service secrets.</span></span>

<span data-ttu-id="b1bd0-137">Quindi, usare gli identificatori che vengono forniti per l'integrazione con archiviazione di Azure nel codice.</span><span class="sxs-lookup"><span data-stu-id="b1bd0-137">Then, use the identifiers you provided to integrate with Azure Storage in your code.</span></span>

```cs
#r "Newtonsoft.Json"

using Newtonsoft.Json.Linq;

// From an incoming queue message that is a JSON object, add fields and write to Table Storage
// The method return value creates a new row in Table Storage
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
// From an incoming queue message that is a JSON object, add fields and write to Table Storage
// The second parameter to context.done is used as the value for the new row
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

<span data-ttu-id="b1bd0-138">Ecco il *function.json* che corrisponde al codice precedente.</span><span class="sxs-lookup"><span data-stu-id="b1bd0-138">Here is the *function.json* that corresponds to the preceding code.</span></span> <span data-ttu-id="b1bd0-139">Si noti che si può usare la stessa configurazione, indipendentemente dal linguaggio di implementazione della funzione.</span><span class="sxs-lookup"><span data-stu-id="b1bd0-139">Note that the same configuration can be used, regardless of the language of the function implementation.</span></span>

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
<span data-ttu-id="b1bd0-140">Per visualizzare e modificare i contenuti della *funzione .json* nel portale di Azure, fare clic sull'opzione **Editor avanzato** nella scheda **Integrazione** della funzione.</span><span class="sxs-lookup"><span data-stu-id="b1bd0-140">To view and edit the contents of *function.json* in the Azure portal, click the **Advanced editor** option on the **Integrate** tab of your function.</span></span>

<span data-ttu-id="b1bd0-141">Per altri esempi di codice e informazioni dettagliate sull'integrazione con archiviazione di Azure, vedere [Associazioni del BLOB del servizio di archiviazione di Funzioni di Azure](functions-bindings-storage.md).</span><span class="sxs-lookup"><span data-stu-id="b1bd0-141">For more code examples and details on integrating with Azure Storage, see [Azure Functions triggers and bindings for Azure Storage](functions-bindings-storage.md).</span></span>

### <a name="binding-direction"></a><span data-ttu-id="b1bd0-142">Direzione dell'associazione</span><span class="sxs-lookup"><span data-stu-id="b1bd0-142">Binding direction</span></span>

<span data-ttu-id="b1bd0-143">Tutti i trigger e le associazioni hanno una proprietà `direction`:</span><span class="sxs-lookup"><span data-stu-id="b1bd0-143">All triggers and bindings have a `direction` property:</span></span>

- <span data-ttu-id="b1bd0-144">Per i trigger, la direzione è sempre `in`</span><span class="sxs-lookup"><span data-stu-id="b1bd0-144">For triggers, the direction is always `in`</span></span>
- <span data-ttu-id="b1bd0-145">Le associazioni di input e di output usano `in` e `out`</span><span class="sxs-lookup"><span data-stu-id="b1bd0-145">Input and output bindings use `in` and `out`</span></span>
- <span data-ttu-id="b1bd0-146">Alcune associazioni supportano una direzione speciale `inout`.</span><span class="sxs-lookup"><span data-stu-id="b1bd0-146">Some bindings support a special direction `inout`.</span></span> <span data-ttu-id="b1bd0-147">Se si usa `inout`, solo l'**Editor avanzato** è disponibile nelle scheda **Integrazione**.</span><span class="sxs-lookup"><span data-stu-id="b1bd0-147">If you use `inout`, only the **Advanced editor** is available in the **Integrate** tab.</span></span>

## <a name="using-the-function-return-type-to-return-a-single-output"></a><span data-ttu-id="b1bd0-148">Uso del tipo restituito della funzione per restituire un singolo output</span><span class="sxs-lookup"><span data-stu-id="b1bd0-148">Using the function return type to return a single output</span></span>

<span data-ttu-id="b1bd0-149">Nell'esempio precedente viene illustrato come usare il valore restituito della funzione per offrire l'output a un'associazione, che si può fare tramite il parametro nome speciale `$return`.</span><span class="sxs-lookup"><span data-stu-id="b1bd0-149">The preceding example shows how to use the function return value to provide output to a binding, which is achieved by using the special name parameter `$return`.</span></span> <span data-ttu-id="b1bd0-150">(Questa opzione è supportata solo nei linguaggi che dispongono di un valore restituito, ad esempio C#, JavaScript e F#). Se una funzione dispone di più associazioni di output, usare `$return` per una sola delle associazioni di output.</span><span class="sxs-lookup"><span data-stu-id="b1bd0-150">(This is only supported in languages that have a return value, such as C#, JavaScript, and F#.) If a function has multiple output bindings, use `$return` for only one of the output bindings.</span></span> 

```json
// excerpt of function.json
{
    "name": "$return",
    "type": "blob",
    "direction": "out",
    "path": "output-container/{id}"
}
```

<span data-ttu-id="b1bd0-151">Gli esempi seguenti mostrano come i tipi restituiti vengono usati con le associazioni di output in C#, JavaScript e F#.</span><span class="sxs-lookup"><span data-stu-id="b1bd0-151">The examples below show how return types are used with output bindings in C#, JavaScript, and F#.</span></span>

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
// JavaScript: return a value in the second parameter to context.done
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

## <a name="binding-datatype-property"></a><span data-ttu-id="b1bd0-152">Proprietà Binding dataType</span><span class="sxs-lookup"><span data-stu-id="b1bd0-152">Binding dataType property</span></span>

<span data-ttu-id="b1bd0-153">In .NET usare i tipi per definire il tipo di dati per i dati di input.</span><span class="sxs-lookup"><span data-stu-id="b1bd0-153">In .NET, use the types to define the data type for input data.</span></span> <span data-ttu-id="b1bd0-154">Ad esempio, usare `string` da associare al testo di un trigger di coda e una matrice di byte da leggere in formato binario.</span><span class="sxs-lookup"><span data-stu-id="b1bd0-154">For instance, use `string` to bind to the text of a queue trigger and a byte array to read as binary.</span></span>

<span data-ttu-id="b1bd0-155">Per le lingue che vengono digitate in modo dinamico, ad esempio JavaScript, usare la proprietà `dataType` nella definizione di associazione.</span><span class="sxs-lookup"><span data-stu-id="b1bd0-155">For languages that are dynamically typed such as JavaScript, use the `dataType` property in the binding definition.</span></span> <span data-ttu-id="b1bd0-156">Ad esempio, per leggere il contenuto di una richiesta HTTP in formato binario, usare il tipo `binary`:</span><span class="sxs-lookup"><span data-stu-id="b1bd0-156">For example, to read the content of an HTTP request in binary format, use the type `binary`:</span></span>

```json
{
    "type": "httpTrigger",
    "name": "req",
    "direction": "in",
    "dataType": "binary"
}
```

<span data-ttu-id="b1bd0-157">Altre opzioni per `dataType` sono `stream` e `string`.</span><span class="sxs-lookup"><span data-stu-id="b1bd0-157">Other options for `dataType` are `stream` and `string`.</span></span>

## <a name="resolving-app-settings"></a><span data-ttu-id="b1bd0-158">Risoluzione di impostazioni app</span><span class="sxs-lookup"><span data-stu-id="b1bd0-158">Resolving app settings</span></span>
<span data-ttu-id="b1bd0-159">Come procedura consigliata, i segreti e le stringhe di connessione devono essere gestiti tramite le impostazioni dell'app, invece dei file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="b1bd0-159">As a best practice, secrets and connection strings should be managed using app settings, rather than configuration files.</span></span> <span data-ttu-id="b1bd0-160">Ciò limita l'accesso a questi segreti e rende sicuro archiviare *function.json* in un repository di controllo sorgente pubblico.</span><span class="sxs-lookup"><span data-stu-id="b1bd0-160">This limits access to these secrets and makes it safe to store *function.json* in a public source control repository.</span></span>

<span data-ttu-id="b1bd0-161">Le impostazioni dell'app sono utili anche ogni volta che si desidera modificare la configurazione in base all'ambiente.</span><span class="sxs-lookup"><span data-stu-id="b1bd0-161">App settings are also useful whenever you want to change configuration based on the environment.</span></span> <span data-ttu-id="b1bd0-162">Ad esempio, in un ambiente di test, si potrebbe voler monitorare un contenitore di archiviazione BLOB o di coda diverso.</span><span class="sxs-lookup"><span data-stu-id="b1bd0-162">For example, in a test environment, you may want to monitor a different queue or blob storage container.</span></span>

<span data-ttu-id="b1bd0-163">Le impostazioni dell'app vengono risolte ogni volta che un valore è racchiuso tra simboli di percentuale, ad esempio `%MyAppSetting%`.</span><span class="sxs-lookup"><span data-stu-id="b1bd0-163">App settings are resolved whenever a value is enclosed in percent signs, such as `%MyAppSetting%`.</span></span> <span data-ttu-id="b1bd0-164">Si noti che la proprietà `connection` di trigger e associazioni è un caso speciale e risolve automaticamente i valori come impostazioni dell'app.</span><span class="sxs-lookup"><span data-stu-id="b1bd0-164">Note that the `connection` property of triggers and bindings is a special case and automatically resolves values as app settings.</span></span> 

<span data-ttu-id="b1bd0-165">L'esempio seguente è un trigger di coda che usa un'impostazione dell'app `%input-queue-name%` per definire la coda di trigger.</span><span class="sxs-lookup"><span data-stu-id="b1bd0-165">The following example is a queue trigger that uses an app setting `%input-queue-name%` to define the queue to trigger on.</span></span>

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

## <a name="trigger-metadata-properties"></a><span data-ttu-id="b1bd0-166">Proprietà dei metadati di trigger</span><span class="sxs-lookup"><span data-stu-id="b1bd0-166">Trigger metadata properties</span></span>

<span data-ttu-id="b1bd0-167">Oltre al payload dei dati offerto da un trigger (ad esempio, il messaggio di coda che ha attivato una funzione), molti trigger forniscono i valori dei metadati aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="b1bd0-167">In addition to the data payload provided by a trigger (such as the queue message that triggered a function), many triggers provide additional metadata values.</span></span> <span data-ttu-id="b1bd0-168">Questi valori possono essere usati come parametri di input in C# e F# o come proprietà nell'oggetto `context.bindings` in JavaScript.</span><span class="sxs-lookup"><span data-stu-id="b1bd0-168">These values can be used as input parameters in C# and F# or properties on the `context.bindings` object in JavaScript.</span></span> 

<span data-ttu-id="b1bd0-169">Ad esempio, un trigger di coda supporta le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="b1bd0-169">For example, a queue trigger supports the following properties:</span></span>

* <span data-ttu-id="b1bd0-170">QueueTrigge: attivazione del contenuto del messaggio, se una stringa valida</span><span class="sxs-lookup"><span data-stu-id="b1bd0-170">QueueTrigger - triggering message content if a valid string</span></span>
* <span data-ttu-id="b1bd0-171">DequeueCount</span><span class="sxs-lookup"><span data-stu-id="b1bd0-171">DequeueCount</span></span>
* <span data-ttu-id="b1bd0-172">ExpirationTime</span><span class="sxs-lookup"><span data-stu-id="b1bd0-172">ExpirationTime</span></span>
* <span data-ttu-id="b1bd0-173">ID</span><span class="sxs-lookup"><span data-stu-id="b1bd0-173">Id</span></span>
* <span data-ttu-id="b1bd0-174">InsertionTime</span><span class="sxs-lookup"><span data-stu-id="b1bd0-174">InsertionTime</span></span>
* <span data-ttu-id="b1bd0-175">NextVisibleTime</span><span class="sxs-lookup"><span data-stu-id="b1bd0-175">NextVisibleTime</span></span>
* <span data-ttu-id="b1bd0-176">PopReceipt</span><span class="sxs-lookup"><span data-stu-id="b1bd0-176">PopReceipt</span></span>

<span data-ttu-id="b1bd0-177">I dettagli delle proprietà dei metadati per ogni trigger sono descritti nell'argomento di riferimento corrispondente.</span><span class="sxs-lookup"><span data-stu-id="b1bd0-177">Details of metadata properties for each trigger are described in the corresponding reference topic.</span></span> <span data-ttu-id="b1bd0-178">La documentazione è disponibile anche nella scheda **Integrazione** del portale nella sezione **Documentazione** sotto l'area di configurazione dell'associazione.</span><span class="sxs-lookup"><span data-stu-id="b1bd0-178">Documentation is also available in the **Integrate** tab of the portal, in the **Documentation** section below the binding configuration area.</span></span>  

<span data-ttu-id="b1bd0-179">Ad esempio, poiché i trigger BLOB presentano alcuni ritardi, è possibile usare un trigger della coda per l'esecuzione della funzione (vedere [Trigger del BLOB del servizio di archiviazione](functions-bindings-storage-blob.md#storage-blob-trigger).</span><span class="sxs-lookup"><span data-stu-id="b1bd0-179">For example, since blob triggers have some delays, you can use a queue trigger to run your function (see [Blob Storage Trigger](functions-bindings-storage-blob.md#storage-blob-trigger).</span></span> <span data-ttu-id="b1bd0-180">Il messaggio della coda contiene il filename del BLOB da attivare.</span><span class="sxs-lookup"><span data-stu-id="b1bd0-180">The queue message would contain the blob filename to trigger on.</span></span> <span data-ttu-id="b1bd0-181">Con l'uso della proprietà dei metadati `queueTrigger`, è possibile specificareper intero questo comportamento nella configurazione, invece che nel codice.</span><span class="sxs-lookup"><span data-stu-id="b1bd0-181">Using the `queueTrigger` metadata property, you can specify this behavior all in your configuration, rather than your code.</span></span>

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

<span data-ttu-id="b1bd0-182">Le proprietà dei metadati da un trigger possono anche essere usate in una *espressione dell'associazione* per un'altra associazione, come descritto nella sezione seguente.</span><span class="sxs-lookup"><span data-stu-id="b1bd0-182">Metadata properties from a trigger can also be used in a *binding expression* for another binding, as described in the following section.</span></span>

## <a name="binding-expressions-and-patterns"></a><span data-ttu-id="b1bd0-183">Modelli ed espressioni di associazione</span><span class="sxs-lookup"><span data-stu-id="b1bd0-183">Binding expressions and patterns</span></span>

<span data-ttu-id="b1bd0-184">Una delle funzionalità più potenti di trigger e associazioni sono le *espressioni di associazione*.</span><span class="sxs-lookup"><span data-stu-id="b1bd0-184">One of the most powerful features of triggers and bindings is *binding expressions*.</span></span> <span data-ttu-id="b1bd0-185">All'interno dell'associazione, è possibile definire delle espressioni di modello che possono quindi essere usate in altre associazioni o nel codice.</span><span class="sxs-lookup"><span data-stu-id="b1bd0-185">Within your binding, you can define pattern expressions which can then be used in other bindings or your code.</span></span> <span data-ttu-id="b1bd0-186">I metadati del trigger possono essere usati anche nelle espressioni di associazione, come illustrato nell'esempio nella sezione precedente.</span><span class="sxs-lookup"><span data-stu-id="b1bd0-186">Trigger metadata can also be used in binding expressions, as show in the sample in the preceding section.</span></span>

<span data-ttu-id="b1bd0-187">Ad esempio, si supponga che si desidera ridimensionare le immagini in un contenitore di archiviazione BLOB specifico, simile al modello di **ridimensionamento immagine** nella pagina **Nuova funzione**.</span><span class="sxs-lookup"><span data-stu-id="b1bd0-187">For example, suppose you want to resize images in particular blob storage container, similar to the **Image Resizer** template in the **New Function** page.</span></span> <span data-ttu-id="b1bd0-188">Passare a **Nuova funzione** -> Linguaggio **C#** -> Scenario **Esempi** -> **ImageResizer-CSharp**.</span><span class="sxs-lookup"><span data-stu-id="b1bd0-188">Go to **New Function** -> Language **C#** -> Scenario **Samples** -> **ImageResizer-CSharp**.</span></span> 

<span data-ttu-id="b1bd0-189">Ecco la definizione di *function.json*:</span><span class="sxs-lookup"><span data-stu-id="b1bd0-189">Here is the *function.json* definition:</span></span>

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

<span data-ttu-id="b1bd0-190">Si noti che il parametro `filename` viene usato nella definizione del trigger BLOB e anche nell'associazione output di BLOB.</span><span class="sxs-lookup"><span data-stu-id="b1bd0-190">Notice that the `filename` parameter is used in both the blob trigger definition as well as the blob output binding.</span></span> <span data-ttu-id="b1bd0-191">Questo parametro può essere usato anche nel codice della funzione.</span><span class="sxs-lookup"><span data-stu-id="b1bd0-191">This parameter can also be used in function code.</span></span>

```csharp
// C# example of binding to {filename}
public static void Run(Stream image, string filename, Stream imageSmall, TraceWriter log)  
{
    log.Info($"Blob trigger processing: {filename}");
    // ...
} 
```

<!--TODO: add JavaScript example -->
<!-- Blocked by bug https://github.com/Azure/Azure-Functions/issues/248 -->


### <a name="random-guids"></a><span data-ttu-id="b1bd0-192">GUID casuali</span><span class="sxs-lookup"><span data-stu-id="b1bd0-192">Random GUIDs</span></span>
<span data-ttu-id="b1bd0-193">Funzioni di Azure fornisce una sintassi utile per la generazione di GUID nelle associazioni, tramite l'espressione dell'associazione `{rand-guid}`.</span><span class="sxs-lookup"><span data-stu-id="b1bd0-193">Azure Functions provides a convenience syntax for generating GUIDs in your bindings, through the `{rand-guid}` binding expression.</span></span> <span data-ttu-id="b1bd0-194">Nell'esempio seguente questa operazione viene usata per generare un nome del BLOB univoco:</span><span class="sxs-lookup"><span data-stu-id="b1bd0-194">The following example uses this to generate a unique blob name:</span></span> 

```json
{
  "type": "blob",
  "name": "blobOutput",
  "direction": "out",
  "path": "my-output-container/{rand-guid}"
}
```

### <a name="current-time"></a><span data-ttu-id="b1bd0-195">Ora corrente</span><span class="sxs-lookup"><span data-stu-id="b1bd0-195">Current time</span></span>

<span data-ttu-id="b1bd0-196">È possibile usare l'espressione di associazione `DateTime`, che viene risolta in `DateTime.UtcNow`.</span><span class="sxs-lookup"><span data-stu-id="b1bd0-196">You can use the binding expression `DateTime`, which resolves to `DateTime.UtcNow`.</span></span>

```json
{
  "type": "blob",
  "name": "blobOutput",
  "direction": "out",
  "path": "my-output-container/{DateTime}"
}
```

## <a name="bind-to-custom-input-properties-in-a-binding-expression"></a><span data-ttu-id="b1bd0-197">Associare le proprietà di input personalizzate in un'espressione di associazione</span><span class="sxs-lookup"><span data-stu-id="b1bd0-197">Bind to custom input properties in a binding expression</span></span>

<span data-ttu-id="b1bd0-198">Le espressioni di associazione possono anche fare riferimento alle proprietà definite nel payload del trigger stesso.</span><span class="sxs-lookup"><span data-stu-id="b1bd0-198">Binding expressions can also reference properties that are defined in the trigger payload itself.</span></span> <span data-ttu-id="b1bd0-199">Ad esempio, si potrebbe voler associare in modo dinamico ad un file di archiviazione BLOB un filename fornito da un webhook.</span><span class="sxs-lookup"><span data-stu-id="b1bd0-199">For example, you may want to dynamically bind to a blob storage file from a filename provided in a webhook.</span></span>

<span data-ttu-id="b1bd0-200">Ad esempio, la seguente *function.json* usa una proprietà denominata `BlobName` dal payload del trigger:</span><span class="sxs-lookup"><span data-stu-id="b1bd0-200">For example, the following *function.json* uses a property called `BlobName` from the trigger payload:</span></span>

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

<span data-ttu-id="b1bd0-201">A tale scopo in C# e F #, è necessario definire un POCO che definisce i campi che saranno deserializzati nel payload del trigger.</span><span class="sxs-lookup"><span data-stu-id="b1bd0-201">To accomplish this in C# and F#, you must define a POCO that defines the fields that will be deserialized in the trigger payload.</span></span>

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

<span data-ttu-id="b1bd0-202">In JavaScript, viene eseguita automaticamente la deserializzazione di JSON ed è possibile usare direttamente le proprietà.</span><span class="sxs-lookup"><span data-stu-id="b1bd0-202">In JavaScript, JSON deserialization is automatically performed and you can use the properties directly.</span></span>

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

## <a name="configuring-binding-data-at-runtime"></a><span data-ttu-id="b1bd0-203">Configurazione dell'associazione di dati in fase di runtime</span><span class="sxs-lookup"><span data-stu-id="b1bd0-203">Configuring binding data at runtime</span></span>

<span data-ttu-id="b1bd0-204">In C# e altri linguaggi .NET, è possibile usare un metodo di associazione imperativa anziché dichiarativa in *function.json*.</span><span class="sxs-lookup"><span data-stu-id="b1bd0-204">In C# and other .NET languages, you can use an imperative binding pattern, as opposed to the declarative bindings in *function.json*.</span></span> <span data-ttu-id="b1bd0-205">L'associazione imperativa è utile quando i parametri di associazione devono essere calcolati in fase di runtime invece che in fase di progettazione.</span><span class="sxs-lookup"><span data-stu-id="b1bd0-205">Imperative binding is useful when binding parameters need to be computed at runtime rather than design time.</span></span> <span data-ttu-id="b1bd0-206">Per altre informazioni, vedere [Associazione in fase di runtime tramite le associazioni imperative](functions-reference-csharp.md#imperative-bindings) nel riferimento per sviluppatori C#.</span><span class="sxs-lookup"><span data-stu-id="b1bd0-206">To learn more, see [Binding at runtime via imperative bindings](functions-reference-csharp.md#imperative-bindings) in the C# developer reference.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b1bd0-207">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b1bd0-207">Next steps</span></span>
<span data-ttu-id="b1bd0-208">Per altre informazioni su questi elementi, vedere gli articoli indicati di seguito:</span><span class="sxs-lookup"><span data-stu-id="b1bd0-208">For more information on a specific binding, see the following articles:</span></span>

- [<span data-ttu-id="b1bd0-209">HTTP e webhook</span><span class="sxs-lookup"><span data-stu-id="b1bd0-209">HTTP and webhooks</span></span>](functions-bindings-http-webhook.md)
- [<span data-ttu-id="b1bd0-210">Timer</span><span class="sxs-lookup"><span data-stu-id="b1bd0-210">Timer</span></span>](functions-bindings-timer.md)
- [<span data-ttu-id="b1bd0-211">Archiviazione code</span><span class="sxs-lookup"><span data-stu-id="b1bd0-211">Queue storage</span></span>](functions-bindings-storage-queue.md)
- [<span data-ttu-id="b1bd0-212">Archiviazione BLOB</span><span class="sxs-lookup"><span data-stu-id="b1bd0-212">Blob storage</span></span>](functions-bindings-storage-blob.md)
- [<span data-ttu-id="b1bd0-213">Archiviazione tabelle</span><span class="sxs-lookup"><span data-stu-id="b1bd0-213">Table storage</span></span>](functions-bindings-storage-table.md)
- [<span data-ttu-id="b1bd0-214">Hub eventi</span><span class="sxs-lookup"><span data-stu-id="b1bd0-214">Event Hub</span></span>](functions-bindings-event-hubs.md)
- [<span data-ttu-id="b1bd0-215">Bus di servizio</span><span class="sxs-lookup"><span data-stu-id="b1bd0-215">Service Bus</span></span>](functions-bindings-service-bus.md)
- [<span data-ttu-id="b1bd0-216">Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="b1bd0-216">Cosmos DB</span></span>](functions-bindings-documentdb.md)
- [<span data-ttu-id="b1bd0-217">SendGrid</span><span class="sxs-lookup"><span data-stu-id="b1bd0-217">SendGrid</span></span>](functions-bindings-sendgrid.md)
- [<span data-ttu-id="b1bd0-218">Twilio</span><span class="sxs-lookup"><span data-stu-id="b1bd0-218">Twilio</span></span>](functions-bindings-twilio.md)
- [<span data-ttu-id="b1bd0-219">Hub di notifica</span><span class="sxs-lookup"><span data-stu-id="b1bd0-219">Notification Hubs</span></span>](functions-bindings-notification-hubs.md)
- [<span data-ttu-id="b1bd0-220">App per dispositivi mobili</span><span class="sxs-lookup"><span data-stu-id="b1bd0-220">Mobile Apps</span></span>](functions-bindings-mobile-apps.md)
- [<span data-ttu-id="b1bd0-221">File esterno</span><span class="sxs-lookup"><span data-stu-id="b1bd0-221">External file</span></span>](functions-bindings-external-file.md)
