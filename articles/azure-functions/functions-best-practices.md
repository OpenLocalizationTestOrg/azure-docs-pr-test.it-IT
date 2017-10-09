---
title: aaaBest procedure consigliate per le funzioni di Azure | Documenti Microsoft
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
ms.openlocfilehash: bd3d826b75267a740e355b008943a48f71ebd339
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-hello-performance-and-reliability-of-azure-functions"></a><span data-ttu-id="af3b5-104">Ottimizzare le prestazioni di hello e l'affidabilità delle funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="af3b5-104">Optimize hello performance and reliability of Azure Functions</span></span>

<span data-ttu-id="af3b5-105">Questo articolo fornisce informazioni aggiuntive tooimprove hello prestazioni e affidabilità delle app di funzione.</span><span class="sxs-lookup"><span data-stu-id="af3b5-105">This article provides guidance tooimprove hello performance and reliability of your function apps.</span></span> 


## <a name="avoid-long-running-functions"></a><span data-ttu-id="af3b5-106">Evitare funzioni con esecuzione prolungata</span><span class="sxs-lookup"><span data-stu-id="af3b5-106">Avoid long running functions</span></span>

<span data-ttu-id="af3b5-107">Le funzioni con esecuzione prolungata e di grandi dimensioni possono causare problemi di timeout imprevisti.</span><span class="sxs-lookup"><span data-stu-id="af3b5-107">Large, long-running functions can cause unexpected timeout issues.</span></span> <span data-ttu-id="af3b5-108">Una funzione può risultare lungo a causa di dipendenze di Node.js toomany.</span><span class="sxs-lookup"><span data-stu-id="af3b5-108">A function can become large due toomany Node.js dependencies.</span></span> <span data-ttu-id="af3b5-109">L'importazione delle dipendenze può anche fare aumentare i tempi di caricamento causando timeout imprevisti.</span><span class="sxs-lookup"><span data-stu-id="af3b5-109">Importing dependencies can also cause increased load times that result in unexpected timeouts.</span></span> <span data-ttu-id="af3b5-110">Le dipendenze vengono caricate in modo sia esplicito che implicito.</span><span class="sxs-lookup"><span data-stu-id="af3b5-110">Dependencies are loaded both explicitly and implicitly.</span></span> <span data-ttu-id="af3b5-111">Un singolo modulo caricato dal codice potrebbe caricare i propri moduli aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="af3b5-111">A single module loaded by your code may load its own additional modules.</span></span>  

<span data-ttu-id="af3b5-112">Quando è possibile, suddividere le funzioni di grandi dimensioni in gruppi di funzioni più piccoli che possono interagire tra loro e restituire rapidamente le risposte.</span><span class="sxs-lookup"><span data-stu-id="af3b5-112">Whenever possible, refactor large functions into smaller function sets that work together and return responses fast.</span></span> <span data-ttu-id="af3b5-113">Ad esempio, un webhook o una funzione di attivazione HTTP potrebbe richiedere una risposta di riconoscimento all'interno di un determinato limite di tempo; è comune per webhook toorequire un intervento immediato.</span><span class="sxs-lookup"><span data-stu-id="af3b5-113">For example, a webhook or HTTP trigger function might require an acknowledgment response within a certain time limit; it is common for webhooks toorequire an immediate response.</span></span> <span data-ttu-id="af3b5-114">È possibile passare i payload di hello HTTP trigger in una coda toobe elaborati da una funzione di attivazione coda.</span><span class="sxs-lookup"><span data-stu-id="af3b5-114">You can pass hello HTTP trigger payload into a queue toobe processed by a queue trigger function.</span></span> <span data-ttu-id="af3b5-115">Questo approccio consente il lavoro effettivo toodefer hello e restituire una risposta immediata.</span><span class="sxs-lookup"><span data-stu-id="af3b5-115">This approach allows you toodefer hello actual work and return an immediate response.</span></span>


## <a name="cross-function-communication"></a><span data-ttu-id="af3b5-116">Comunicazioni tra funzioni</span><span class="sxs-lookup"><span data-stu-id="af3b5-116">Cross function communication</span></span>

<span data-ttu-id="af3b5-117">Quando si integra più funzioni, è in genere un best practice toouse le code di archiviazione per le comunicazioni di funzione tra.</span><span class="sxs-lookup"><span data-stu-id="af3b5-117">When integrating multiple functions, it is generally a best practice toouse storage queues for cross function communication.</span></span>  <span data-ttu-id="af3b5-118">Hello principale, infatti, le code di archiviazione sono più economiche e tooprovision molto più semplice.</span><span class="sxs-lookup"><span data-stu-id="af3b5-118">hello main reason is storage queues are cheaper and much easier tooprovision.</span></span> 

<span data-ttu-id="af3b5-119">Singoli messaggi in una coda di archiviazione sono limitati in dimensioni too64 KB.</span><span class="sxs-lookup"><span data-stu-id="af3b5-119">Individual messages in a storage queue are limited in size too64 KB.</span></span> <span data-ttu-id="af3b5-120">Se è necessario toopass i messaggi di grandi dimensioni tra le funzioni, una coda di Service Bus di Azure potrebbe essere le dimensioni dei messaggi utilizzati toosupport too256 KB.</span><span class="sxs-lookup"><span data-stu-id="af3b5-120">If you need toopass larger messages between functions, an Azure Service Bus queue could be used toosupport message sizes up too256 KB.</span></span>

<span data-ttu-id="af3b5-121">Gli argomenti del bus di servizio sono utili se è necessario filtrare i messaggi prima dell'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="af3b5-121">Service Bus topics are useful if you require message filtering before processing.</span></span>

<span data-ttu-id="af3b5-122">Gli hub eventi sono utili toosupport le comunicazioni di volumi elevati.</span><span class="sxs-lookup"><span data-stu-id="af3b5-122">Event hubs are useful toosupport high volume communications.</span></span>


## <a name="write-functions-toobe-stateless"></a><span data-ttu-id="af3b5-123">Scrivere funzioni toobe senza stato</span><span class="sxs-lookup"><span data-stu-id="af3b5-123">Write functions toobe stateless</span></span> 

<span data-ttu-id="af3b5-124">Le funzioni devono essere senza stato e idempotenti se possibile.</span><span class="sxs-lookup"><span data-stu-id="af3b5-124">Functions should be stateless and idempotent if possible.</span></span> <span data-ttu-id="af3b5-125">Associare ai dati eventuali informazioni obbligatorie sullo stato.</span><span class="sxs-lookup"><span data-stu-id="af3b5-125">Associate any required state information with your data.</span></span> <span data-ttu-id="af3b5-126">Ad esempio, un ordine in fase di elaborazione probabilmente ha un membro `state` associato.</span><span class="sxs-lookup"><span data-stu-id="af3b5-126">For example, an order being processed would likely have an associated `state` member.</span></span> <span data-ttu-id="af3b5-127">Una funzione è riuscito a elaborare un ordine in base a tale stato mentre funzione hello stessa rimane senza stato.</span><span class="sxs-lookup"><span data-stu-id="af3b5-127">A function could process an order based on that state while hello function itself remains stateless.</span></span> 

<span data-ttu-id="af3b5-128">Le funzioni idempotenti sono consigliate in particolare con i trigger timer.</span><span class="sxs-lookup"><span data-stu-id="af3b5-128">Idempotent functions are especially recommended with timer triggers.</span></span> <span data-ttu-id="af3b5-129">Ad esempio, se si dispone di un elemento che è assolutamente necessario eseguire una volta al giorno, viene scritto in modo è possibile eseguire qualsiasi momento durante il giorno hello con hello stessi risultati.</span><span class="sxs-lookup"><span data-stu-id="af3b5-129">For example, if you have something that absolutely must run once a day, write it so it can run any time during hello day with hello same results.</span></span> <span data-ttu-id="af3b5-130">funzione Hello può uscire quando non sono presenti operazioni per un determinato giorno.</span><span class="sxs-lookup"><span data-stu-id="af3b5-130">hello function can exit when there is no work for a particular day.</span></span> <span data-ttu-id="af3b5-131">Anche se un'esecuzione precedente non è riuscito toocomplete hello prossima esecuzione deve prelevare dove era stata interrotta.</span><span class="sxs-lookup"><span data-stu-id="af3b5-131">Also if a previous run failed toocomplete, hello next run should pick up where it left off.</span></span>


## <a name="write-defensive-functions"></a><span data-ttu-id="af3b5-132">Scrivere funzioni difensive</span><span class="sxs-lookup"><span data-stu-id="af3b5-132">Write defensive functions</span></span>

<span data-ttu-id="af3b5-133">Si supponga che la funzione possa rilevare un'eccezione in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="af3b5-133">Assume your function could encounter an exception at any time.</span></span> <span data-ttu-id="af3b5-134">Durante l'esecuzione successiva hello, progettare le funzioni con hello possibilità toocontinue da un punto di errore precedente.</span><span class="sxs-lookup"><span data-stu-id="af3b5-134">Design your functions with hello ability toocontinue from a previous fail point during hello next execution.</span></span> <span data-ttu-id="af3b5-135">Si consideri uno scenario che richiede hello seguenti azioni:</span><span class="sxs-lookup"><span data-stu-id="af3b5-135">Consider a scenario that requires hello following actions:</span></span>

1. <span data-ttu-id="af3b5-136">Query per 10.000 righe in un database.</span><span class="sxs-lookup"><span data-stu-id="af3b5-136">Query for 10,000 rows in a db.</span></span>
2. <span data-ttu-id="af3b5-137">Creare un messaggio nella coda per ognuna di tali righe tooprocess ulteriormente verso il basso la riga hello.</span><span class="sxs-lookup"><span data-stu-id="af3b5-137">Create a queue message for each of those rows tooprocess further down hello line.</span></span>
 
<span data-ttu-id="af3b5-138">In base alla complessità del sistema, è possibile che i servizi downstream coinvolti non funzionino correttamente, che si verifichino interruzioni della rete, che vengano raggiunti i limiti di quota e così via. Tutti questi elementi possono influire sulla funzione in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="af3b5-138">Depending on how complex your system is, you may have: involved downstream services behaving badly, networking outages, or quota limits reached, etc. All of these can affect your function at any time.</span></span> <span data-ttu-id="af3b5-139">È necessario toodesign toobe le funzioni pronti a.</span><span class="sxs-lookup"><span data-stu-id="af3b5-139">You need toodesign your functions toobe prepared for it.</span></span>

<span data-ttu-id="af3b5-140">Come reagisce il codice in caso di errore dopo l'inserimento di 5.000 di tali elementi in una coda per l'elaborazione?</span><span class="sxs-lookup"><span data-stu-id="af3b5-140">How does your code react if a failure occurs after inserting 5,000 of those items into a queue for processing?</span></span> <span data-ttu-id="af3b5-141">Tenere traccia degli elementi in un set già completato.</span><span class="sxs-lookup"><span data-stu-id="af3b5-141">Track items in a set that you’ve completed.</span></span> <span data-ttu-id="af3b5-142">In caso contrario, è possibile inserirli di nuovo la volta successiva.</span><span class="sxs-lookup"><span data-stu-id="af3b5-142">Otherwise, you might insert them again next time.</span></span> <span data-ttu-id="af3b5-143">Ciò può influire in modo negativo sul flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="af3b5-143">This can have a serious impact on your work flow.</span></span> 

<span data-ttu-id="af3b5-144">Se un elemento della coda è già stato elaborato, consentire toobe la funzione alcuna operazione.</span><span class="sxs-lookup"><span data-stu-id="af3b5-144">If a queue item was already processed, allow your function toobe a no-op.</span></span>

<span data-ttu-id="af3b5-145">È possibile sfruttare le misure di difesa già fornito per i componenti che si utilizza nella piattaforma Azure funzioni hello.</span><span class="sxs-lookup"><span data-stu-id="af3b5-145">Take advantage of defensive measures already provided for components you use in hello Azure Functions platform.</span></span> <span data-ttu-id="af3b5-146">Ad esempio, vedere **la gestione dei messaggi di coda non elaborabile** nella documentazione di hello per [coda di archiviazione di Azure attiva](functions-bindings-storage-queue.md#trigger).</span><span class="sxs-lookup"><span data-stu-id="af3b5-146">For example, see **Handling poison queue messages** in hello documentation for [Azure Storage Queue triggers](functions-bindings-storage-queue.md#trigger).</span></span>
 

## <a name="dont-mix-test-and-production-code-in-hello-same-function-app"></a><span data-ttu-id="af3b5-147">Non combinazione di test e produzione di codice in hello stesso app (funzione)</span><span class="sxs-lookup"><span data-stu-id="af3b5-147">Don't mix test and production code in hello same function app</span></span>

<span data-ttu-id="af3b5-148">Le funzioni all'interno di un'app per le funzioni condividono le risorse.</span><span class="sxs-lookup"><span data-stu-id="af3b5-148">Functions within a function app share resources.</span></span> <span data-ttu-id="af3b5-149">Ad esempio, la memoria è condivisa.</span><span class="sxs-lookup"><span data-stu-id="af3b5-149">For example, memory is shared.</span></span> <span data-ttu-id="af3b5-150">Se si usa un'app di funzione nell'ambiente di produzione, non aggiungere funzioni relative ai test e tooit risorse.</span><span class="sxs-lookup"><span data-stu-id="af3b5-150">If you're using a function app in production, don't add test-related functions and resources tooit.</span></span> <span data-ttu-id="af3b5-151">per evitare possibili sovraccarichi imprevisti durante l'esecuzione del codice di produzione.</span><span class="sxs-lookup"><span data-stu-id="af3b5-151">It can cause unexpected overhead during production code execution.</span></span>

<span data-ttu-id="af3b5-152">Prestare attenzione a quello che si carica nelle app per le funzioni di produzione.</span><span class="sxs-lookup"><span data-stu-id="af3b5-152">Be careful what you load in your production function apps.</span></span> <span data-ttu-id="af3b5-153">Memoria Media viene calcolata in ogni funzione nell'app hello.</span><span class="sxs-lookup"><span data-stu-id="af3b5-153">Memory is averaged across each function in hello app.</span></span>

<span data-ttu-id="af3b5-154">Se si usa un assembly condiviso a cui si fa riferimento in più funzioni di .Net, inserirlo in una cartella condivisa comune.</span><span class="sxs-lookup"><span data-stu-id="af3b5-154">If you have a shared assembly referenced in multiple .Net functions, put it in a common shared folder.</span></span> <span data-ttu-id="af3b5-155">Assembly di riferimento hello con un toohello simile istruzione esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="af3b5-155">Reference hello assembly with a statement similar toohello following example:</span></span> 

    #r "..\Shared\MyAssembly.dll". 

<span data-ttu-id="af3b5-156">In caso contrario, è facile tooaccidentally distribuire più versioni di test dello stesso file binario che si comportano in modo diverso tra le funzioni hello.</span><span class="sxs-lookup"><span data-stu-id="af3b5-156">Otherwise, it is easy tooaccidentally deploy multiple test versions of hello same binary that behave differently between functions.</span></span>

<span data-ttu-id="af3b5-157">Non usare la registrazione dettagliata nel codice di produzione.</span><span class="sxs-lookup"><span data-stu-id="af3b5-157">Don't use verbose logging in production code.</span></span> <span data-ttu-id="af3b5-158">Ha un impatto negativo sulle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="af3b5-158">It has a negative performance impact.</span></span>



## <a name="use-async-code-but-avoid-blocking-calls"></a><span data-ttu-id="af3b5-159">Usare codice asincrono ma evitare di bloccare le chiamate</span><span class="sxs-lookup"><span data-stu-id="af3b5-159">Use async code but avoid blocking calls</span></span>

<span data-ttu-id="af3b5-160">La programmazione asincrona è una procedura consigliata.</span><span class="sxs-lookup"><span data-stu-id="af3b5-160">Asynchronous programming is a recommended best practice.</span></span> <span data-ttu-id="af3b5-161">Tuttavia, non sempre fare riferimento a hello `Result` proprietà o chiamare `Wait` metodo su un `Task` istanza.</span><span class="sxs-lookup"><span data-stu-id="af3b5-161">However, always avoid referencing hello `Result` property or calling `Wait` method on a `Task` instance.</span></span> <span data-ttu-id="af3b5-162">Questo approccio può causare un esaurimento toothread.</span><span class="sxs-lookup"><span data-stu-id="af3b5-162">This approach can lead toothread exhaustion.</span></span>


[!INCLUDE [HTTP client best practices](../../includes/functions-http-client-best-practices.md)]

## <a name="next-steps"></a><span data-ttu-id="af3b5-163">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="af3b5-163">Next steps</span></span>
<span data-ttu-id="af3b5-164">Per ulteriori informazioni, vedere hello seguenti risorse:</span><span class="sxs-lookup"><span data-stu-id="af3b5-164">For more information, see hello following resources:</span></span>

<span data-ttu-id="af3b5-165">Poiché Funzioni di Azure usa Servizio app di Azure, è consigliabile vedere anche le linee guida del servizio app.</span><span class="sxs-lookup"><span data-stu-id="af3b5-165">Because Azure Functions uses Azure App Service, you should also be aware of  App Service guidelines.</span></span>
* [<span data-ttu-id="af3b5-166">Schemi e procedure per le ottimizzazioni delle prestazioni HTTP</span><span class="sxs-lookup"><span data-stu-id="af3b5-166">Patterns and Practices HTTP Performance Optimizations</span></span>](https://docs.microsoft.com/azure/architecture/antipatterns/improper-instantiation/)

