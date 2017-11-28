---
title: Procedure consigliate per Funzioni di Azure | Documentazione Microsoft
description: Informazioni su modelli e procedure consigliate per Funzioni di Azure.
services: functions
documentationcenter: na
author: wesmc7777
manager: erikre
editor: 
tags: 
keywords: funzioni di azure, modelli, procedure consigliate, funzioni, elaborazione eventi, webhook, calcolo dinamico, architettura senza server
ms.assetid: 9058fb2f-8a93-4036-a921-97a0772f503c
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 06/13/2017
ms.author: glenga
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 645a5dd16e72619e7c2470ab8f03098f0fa6c7f8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="optimize-the-performance-and-reliability-of-azure-functions"></a><span data-ttu-id="f4af7-104">Ottimizzare le prestazioni e l'affidabilità delle funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="f4af7-104">Optimize the performance and reliability of Azure Functions</span></span>

<span data-ttu-id="f4af7-105">Questo articolo fornisce indicazioni per migliorare le prestazioni e l'affidabilità delle app per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="f4af7-105">This article provides guidance to improve the performance and reliability of your function apps.</span></span> 


## <a name="avoid-long-running-functions"></a><span data-ttu-id="f4af7-106">Evitare funzioni con esecuzione prolungata</span><span class="sxs-lookup"><span data-stu-id="f4af7-106">Avoid long running functions</span></span>

<span data-ttu-id="f4af7-107">Le funzioni con esecuzione prolungata e di grandi dimensioni possono causare problemi di timeout imprevisti.</span><span class="sxs-lookup"><span data-stu-id="f4af7-107">Large, long-running functions can cause unexpected timeout issues.</span></span> <span data-ttu-id="f4af7-108">Le dimensioni di una funzione possono diventare grandi a causa della presenza di molte dipendenze di Node.js.</span><span class="sxs-lookup"><span data-stu-id="f4af7-108">A function can become large due to many Node.js dependencies.</span></span> <span data-ttu-id="f4af7-109">L'importazione delle dipendenze può anche fare aumentare i tempi di caricamento causando timeout imprevisti.</span><span class="sxs-lookup"><span data-stu-id="f4af7-109">Importing dependencies can also cause increased load times that result in unexpected timeouts.</span></span> <span data-ttu-id="f4af7-110">Le dipendenze vengono caricate in modo sia esplicito che implicito.</span><span class="sxs-lookup"><span data-stu-id="f4af7-110">Dependencies are loaded both explicitly and implicitly.</span></span> <span data-ttu-id="f4af7-111">Un singolo modulo caricato dal codice potrebbe caricare i propri moduli aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="f4af7-111">A single module loaded by your code may load its own additional modules.</span></span>  

<span data-ttu-id="f4af7-112">Quando è possibile, suddividere le funzioni di grandi dimensioni in gruppi di funzioni più piccoli che possono interagire tra loro e restituire rapidamente le risposte.</span><span class="sxs-lookup"><span data-stu-id="f4af7-112">Whenever possible, refactor large functions into smaller function sets that work together and return responses fast.</span></span> <span data-ttu-id="f4af7-113">Ad esempio, un webhook o una funzione di trigger HTTP potrebbe richiedere una risposta di acknowledgment entro un determinato limite di tempo. È normale per i webhook richiedere una risposta immediata.</span><span class="sxs-lookup"><span data-stu-id="f4af7-113">For example, a webhook or HTTP trigger function might require an acknowledgment response within a certain time limit; it is common for webhooks to require an immediate response.</span></span> <span data-ttu-id="f4af7-114">È possibile passare il payload del trigger HTTP in una coda perché venga elaborato da una funzione di trigger della coda.</span><span class="sxs-lookup"><span data-stu-id="f4af7-114">You can pass the HTTP trigger payload into a queue to be processed by a queue trigger function.</span></span> <span data-ttu-id="f4af7-115">Questo approccio consente di rinviare l'operazione effettiva e di restituire una risposta immediata.</span><span class="sxs-lookup"><span data-stu-id="f4af7-115">This approach allows you to defer the actual work and return an immediate response.</span></span>


## <a name="cross-function-communication"></a><span data-ttu-id="f4af7-116">Comunicazioni tra funzioni</span><span class="sxs-lookup"><span data-stu-id="f4af7-116">Cross function communication</span></span>

<span data-ttu-id="f4af7-117">Quando si integrano più funzioni, in genere è opportuno usare le code di archiviazione per la comunicazione tra funzioni.</span><span class="sxs-lookup"><span data-stu-id="f4af7-117">When integrating multiple functions, it is generally a best practice to use storage queues for cross function communication.</span></span>  <span data-ttu-id="f4af7-118">Il motivo principale è che le code di archiviazione sono più economiche ed è molto più facile sottoporle a provisioning.</span><span class="sxs-lookup"><span data-stu-id="f4af7-118">The main reason is storage queues are cheaper and much easier to provision.</span></span> 

<span data-ttu-id="f4af7-119">Le dimensioni dei singoli messaggi in una coda di archiviazione sono limitate a 64 KB.</span><span class="sxs-lookup"><span data-stu-id="f4af7-119">Individual messages in a storage queue are limited in size to 64 KB.</span></span> <span data-ttu-id="f4af7-120">Se è necessario passare i messaggi di dimensioni superiori tra le funzioni, è possibile usare una coda del bus di servizio di Azure per supportare dimensioni dei messaggi fino a 256 KB.</span><span class="sxs-lookup"><span data-stu-id="f4af7-120">If you need to pass larger messages between functions, an Azure Service Bus queue could be used to support message sizes up to 256 KB.</span></span>

<span data-ttu-id="f4af7-121">Gli argomenti del bus di servizio sono utili se è necessario filtrare i messaggi prima dell'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="f4af7-121">Service Bus topics are useful if you require message filtering before processing.</span></span>

<span data-ttu-id="f4af7-122">Gli hub eventi sono utili per supportare comunicazioni con volumi elevati.</span><span class="sxs-lookup"><span data-stu-id="f4af7-122">Event hubs are useful to support high volume communications.</span></span>


## <a name="write-functions-to-be-stateless"></a><span data-ttu-id="f4af7-123">Scrivere le funzioni in modo che siano senza stato</span><span class="sxs-lookup"><span data-stu-id="f4af7-123">Write functions to be stateless</span></span> 

<span data-ttu-id="f4af7-124">Le funzioni devono essere senza stato e idempotenti se possibile.</span><span class="sxs-lookup"><span data-stu-id="f4af7-124">Functions should be stateless and idempotent if possible.</span></span> <span data-ttu-id="f4af7-125">Associare ai dati eventuali informazioni obbligatorie sullo stato.</span><span class="sxs-lookup"><span data-stu-id="f4af7-125">Associate any required state information with your data.</span></span> <span data-ttu-id="f4af7-126">Ad esempio, un ordine in fase di elaborazione probabilmente ha un membro `state` associato.</span><span class="sxs-lookup"><span data-stu-id="f4af7-126">For example, an order being processed would likely have an associated `state` member.</span></span> <span data-ttu-id="f4af7-127">Una funzione può elaborare un ordine basato su tale stato rimanendo però una funzione senza stato.</span><span class="sxs-lookup"><span data-stu-id="f4af7-127">A function could process an order based on that state while the function itself remains stateless.</span></span> 

<span data-ttu-id="f4af7-128">Le funzioni idempotenti sono consigliate in particolare con i trigger timer.</span><span class="sxs-lookup"><span data-stu-id="f4af7-128">Idempotent functions are especially recommended with timer triggers.</span></span> <span data-ttu-id="f4af7-129">Ad esempio, se si deve assolutamente eseguire un'azione una volta al giorno, scriverla in modo che possa essere eseguita a qualsiasi ora del giorno con gli stessi risultati.</span><span class="sxs-lookup"><span data-stu-id="f4af7-129">For example, if you have something that absolutely must run once a day, write it so it can run any time during the day with the same results.</span></span> <span data-ttu-id="f4af7-130">La funzione può essere chiusa quando non è presente alcun lavoro da svolgere per un determinato giorno.</span><span class="sxs-lookup"><span data-stu-id="f4af7-130">The function can exit when there is no work for a particular day.</span></span> <span data-ttu-id="f4af7-131">Anche se un'esecuzione precedente non è stata completata, l'esecuzione successiva riprenderà da dove era stata interrotta.</span><span class="sxs-lookup"><span data-stu-id="f4af7-131">Also if a previous run failed to complete, the next run should pick up where it left off.</span></span>


## <a name="write-defensive-functions"></a><span data-ttu-id="f4af7-132">Scrivere funzioni difensive</span><span class="sxs-lookup"><span data-stu-id="f4af7-132">Write defensive functions</span></span>

<span data-ttu-id="f4af7-133">Si supponga che la funzione possa rilevare un'eccezione in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="f4af7-133">Assume your function could encounter an exception at any time.</span></span> <span data-ttu-id="f4af7-134">Progettare le funzioni con la possibilità di continuare da un punto di errore precedente durante l'esecuzione successiva.</span><span class="sxs-lookup"><span data-stu-id="f4af7-134">Design your functions with the ability to continue from a previous fail point during the next execution.</span></span> <span data-ttu-id="f4af7-135">Si consideri uno scenario che richiede le azioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="f4af7-135">Consider a scenario that requires the following actions:</span></span>

1. <span data-ttu-id="f4af7-136">Query per 10.000 righe in un database.</span><span class="sxs-lookup"><span data-stu-id="f4af7-136">Query for 10,000 rows in a db.</span></span>
2. <span data-ttu-id="f4af7-137">Creare un messaggio in coda per ognuna delle righe da elaborare ulteriormente in un secondo tempo.</span><span class="sxs-lookup"><span data-stu-id="f4af7-137">Create a queue message for each of those rows to process further down the line.</span></span>
 
<span data-ttu-id="f4af7-138">In base alla complessità del sistema, è possibile che i servizi downstream coinvolti non funzionino correttamente, che si verifichino interruzioni della rete, che vengano raggiunti i limiti di quota e così via. Tutti questi elementi possono influire sulla funzione in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="f4af7-138">Depending on how complex your system is, you may have: involved downstream services behaving badly, networking outages, or quota limits reached, etc. All of these can affect your function at any time.</span></span> <span data-ttu-id="f4af7-139">È necessario progettare le funzioni in modo che siano preparate.</span><span class="sxs-lookup"><span data-stu-id="f4af7-139">You need to design your functions to be prepared for it.</span></span>

<span data-ttu-id="f4af7-140">Come reagisce il codice in caso di errore dopo l'inserimento di 5.000 di tali elementi in una coda per l'elaborazione?</span><span class="sxs-lookup"><span data-stu-id="f4af7-140">How does your code react if a failure occurs after inserting 5,000 of those items into a queue for processing?</span></span> <span data-ttu-id="f4af7-141">Tenere traccia degli elementi in un set già completato.</span><span class="sxs-lookup"><span data-stu-id="f4af7-141">Track items in a set that you’ve completed.</span></span> <span data-ttu-id="f4af7-142">In caso contrario, è possibile inserirli di nuovo la volta successiva.</span><span class="sxs-lookup"><span data-stu-id="f4af7-142">Otherwise, you might insert them again next time.</span></span> <span data-ttu-id="f4af7-143">Ciò può influire in modo negativo sul flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="f4af7-143">This can have a serious impact on your work flow.</span></span> 

<span data-ttu-id="f4af7-144">Se un elemento della coda è già stato elaborato, consentire alla funzione di essere no-op.</span><span class="sxs-lookup"><span data-stu-id="f4af7-144">If a queue item was already processed, allow your function to be a no-op.</span></span>

<span data-ttu-id="f4af7-145">Sfruttare le misure difensive già messe a disposizione per i componenti usati nella piattaforma Funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="f4af7-145">Take advantage of defensive measures already provided for components you use in the Azure Functions platform.</span></span> <span data-ttu-id="f4af7-146">Ad esempio, vedere **Gestione di messaggi della coda non elaborabili** nella documentazione relativa ai [trigger della coda di Archiviazione di Azure](functions-bindings-storage-queue.md#trigger).</span><span class="sxs-lookup"><span data-stu-id="f4af7-146">For example, see **Handling poison queue messages** in the documentation for [Azure Storage Queue triggers](functions-bindings-storage-queue.md#trigger).</span></span>
 

## <a name="dont-mix-test-and-production-code-in-the-same-function-app"></a><span data-ttu-id="f4af7-147">Non combinare codice di test e di produzione nella stessa app per le funzioni</span><span class="sxs-lookup"><span data-stu-id="f4af7-147">Don't mix test and production code in the same function app</span></span>

<span data-ttu-id="f4af7-148">Le funzioni all'interno di un'app per le funzioni condividono le risorse.</span><span class="sxs-lookup"><span data-stu-id="f4af7-148">Functions within a function app share resources.</span></span> <span data-ttu-id="f4af7-149">Ad esempio, la memoria è condivisa.</span><span class="sxs-lookup"><span data-stu-id="f4af7-149">For example, memory is shared.</span></span> <span data-ttu-id="f4af7-150">Se si usa un'app per le funzioni nell'ambiente di produzione, non aggiungere funzioni e risorse relative ai test,</span><span class="sxs-lookup"><span data-stu-id="f4af7-150">If you're using a function app in production, don't add test-related functions and resources to it.</span></span> <span data-ttu-id="f4af7-151">per evitare possibili sovraccarichi imprevisti durante l'esecuzione del codice di produzione.</span><span class="sxs-lookup"><span data-stu-id="f4af7-151">It can cause unexpected overhead during production code execution.</span></span>

<span data-ttu-id="f4af7-152">Prestare attenzione a quello che si carica nelle app per le funzioni di produzione.</span><span class="sxs-lookup"><span data-stu-id="f4af7-152">Be careful what you load in your production function apps.</span></span> <span data-ttu-id="f4af7-153">La memoria viene calcolata in ogni funzione nell'app.</span><span class="sxs-lookup"><span data-stu-id="f4af7-153">Memory is averaged across each function in the app.</span></span>

<span data-ttu-id="f4af7-154">Se si usa un assembly condiviso a cui si fa riferimento in più funzioni di .Net, inserirlo in una cartella condivisa comune.</span><span class="sxs-lookup"><span data-stu-id="f4af7-154">If you have a shared assembly referenced in multiple .Net functions, put it in a common shared folder.</span></span> <span data-ttu-id="f4af7-155">Fare riferimento all'assembly con un'istruzione simile all'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="f4af7-155">Reference the assembly with a statement similar to the following example:</span></span> 

    #r "..\Shared\MyAssembly.dll". 

<span data-ttu-id="f4af7-156">In caso contrario, è facile distribuire accidentalmente più versioni di prova dello stesso binario che si comportano in modo diverso nelle varie funzioni.</span><span class="sxs-lookup"><span data-stu-id="f4af7-156">Otherwise, it is easy to accidentally deploy multiple test versions of the same binary that behave differently between functions.</span></span>

<span data-ttu-id="f4af7-157">Non usare la registrazione dettagliata nel codice di produzione.</span><span class="sxs-lookup"><span data-stu-id="f4af7-157">Don't use verbose logging in production code.</span></span> <span data-ttu-id="f4af7-158">Ha un impatto negativo sulle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="f4af7-158">It has a negative performance impact.</span></span>



## <a name="use-async-code-but-avoid-blocking-calls"></a><span data-ttu-id="f4af7-159">Usare codice asincrono ma evitare di bloccare le chiamate</span><span class="sxs-lookup"><span data-stu-id="f4af7-159">Use async code but avoid blocking calls</span></span>

<span data-ttu-id="f4af7-160">La programmazione asincrona è una procedura consigliata.</span><span class="sxs-lookup"><span data-stu-id="f4af7-160">Asynchronous programming is a recommended best practice.</span></span> <span data-ttu-id="f4af7-161">Evitare sempre, tuttavia, di fare riferimento alla proprietà `Result` o di chiamare il metodo `Wait` su un'istanza di `Task`.</span><span class="sxs-lookup"><span data-stu-id="f4af7-161">However, always avoid referencing the `Result` property or calling `Wait` method on a `Task` instance.</span></span> <span data-ttu-id="f4af7-162">Questo approccio può causare l'esaurimento di un thread.</span><span class="sxs-lookup"><span data-stu-id="f4af7-162">This approach can lead to thread exhaustion.</span></span>


[!INCLUDE [HTTP client best practices](../../includes/functions-http-client-best-practices.md)]

## <a name="next-steps"></a><span data-ttu-id="f4af7-163">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f4af7-163">Next steps</span></span>
<span data-ttu-id="f4af7-164">Per altre informazioni, vedere le seguenti risorse:</span><span class="sxs-lookup"><span data-stu-id="f4af7-164">For more information, see the following resources:</span></span>

<span data-ttu-id="f4af7-165">Poiché Funzioni di Azure usa Servizio app di Azure, è consigliabile vedere anche le linee guida del servizio app.</span><span class="sxs-lookup"><span data-stu-id="f4af7-165">Because Azure Functions uses Azure App Service, you should also be aware of  App Service guidelines.</span></span>
* [<span data-ttu-id="f4af7-166">Schemi e procedure per le ottimizzazioni delle prestazioni HTTP</span><span class="sxs-lookup"><span data-stu-id="f4af7-166">Patterns and Practices HTTP Performance Optimizations</span></span>](https://docs.microsoft.com/azure/architecture/antipatterns/improper-instantiation/)

