---
title: "Entità, termini e concetti dell'Utilità di pianificazione | Documentazione Microsoft"
description: "Concetti, terminologia e gerarchia di entità dell'Utilità di pianificazione di Azure, inclusi processi e raccolte di processi.  Fornisce un esempio completo di un processo pianificato."
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 3ef16fab-d18a-48ba-8e56-3f3e0a1bcb92
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: get-started-article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: 0f035b58ccd140a5481703df7e184206da2ed651
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="scheduler-concepts-terminology--entity-hierarchy"></a><span data-ttu-id="e8d23-104">Concetti, terminologia e gerarchia di entità dell'Utilità di pianificazione</span><span class="sxs-lookup"><span data-stu-id="e8d23-104">Scheduler concepts, terminology, + entity hierarchy</span></span>
## <a name="scheduler-entity-hierarchy"></a><span data-ttu-id="e8d23-105">Gerarchia di entità dell'Utilità di pianificazione</span><span class="sxs-lookup"><span data-stu-id="e8d23-105">Scheduler entity hierarchy</span></span>
<span data-ttu-id="e8d23-106">Nella tabella seguente vengono descritte le risorse principali esposte o usate dall'API dell'Utilità di pianificazione:</span><span class="sxs-lookup"><span data-stu-id="e8d23-106">The following table describes the main resources exposed or used by the Scheduler API:</span></span>

| <span data-ttu-id="e8d23-107">Risorsa</span><span class="sxs-lookup"><span data-stu-id="e8d23-107">Resource</span></span> | <span data-ttu-id="e8d23-108">Descrizione</span><span class="sxs-lookup"><span data-stu-id="e8d23-108">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e8d23-109">**Raccolta di processi**</span><span class="sxs-lookup"><span data-stu-id="e8d23-109">**Job collection**</span></span> |<span data-ttu-id="e8d23-110">Una raccolta di processi contiene un gruppo di processi e gestisce le impostazioni, le quote e le limitazioni condivise dai processi all'interno della raccolta.</span><span class="sxs-lookup"><span data-stu-id="e8d23-110">A job collection contains a group of jobs and maintains settings, quotas, and throttles that are shared by jobs within the collection.</span></span> <span data-ttu-id="e8d23-111">Le raccolte di processi vengono create dal proprietario della sottoscrizione e raggruppano i processi in base ai limiti di utilizzo o dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="e8d23-111">A job collection is created by a subscription owner and groups jobs together based on usage or application boundaries.</span></span> <span data-ttu-id="e8d23-112">È vincolata a un'area.</span><span class="sxs-lookup"><span data-stu-id="e8d23-112">It’s constrained to one region.</span></span> <span data-ttu-id="e8d23-113">Consente inoltre di applicare quote per vincolare l'uso di tutti i processi in tale raccolta.</span><span class="sxs-lookup"><span data-stu-id="e8d23-113">It also allows the enforcement of quotas to constrain the usage of all jobs in that collection.</span></span> <span data-ttu-id="e8d23-114">Le quote includono MaxJobs e MaxRecurrence.</span><span class="sxs-lookup"><span data-stu-id="e8d23-114">The quotas include MaxJobs and MaxRecurrence.</span></span> |
| <span data-ttu-id="e8d23-115">**Processo**</span><span class="sxs-lookup"><span data-stu-id="e8d23-115">**Job**</span></span> |<span data-ttu-id="e8d23-116">Un processo definisce una singola azione ricorrente, con strategie semplici o complesse per l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="e8d23-116">A job defines a single recurrent action, with simple or complex strategies for execution.</span></span> <span data-ttu-id="e8d23-117">Le azioni possono includere HTTP, coda di archiviazione, coda del bus di servizio o richieste di argomento del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="e8d23-117">Actions may include HTTP, storage queue, service bus queue, or service bus topic requests.</span></span> |
| <span data-ttu-id="e8d23-118">**Cronologia processi**</span><span class="sxs-lookup"><span data-stu-id="e8d23-118">**Job history**</span></span> |<span data-ttu-id="e8d23-119">Una cronologia processi rappresenta i dettagli per l'esecuzione di un processo.</span><span class="sxs-lookup"><span data-stu-id="e8d23-119">A job history represents details for an execution of a job.</span></span> <span data-ttu-id="e8d23-120">Contiene esito positivo o negativo, nonché i dettagli della risposta.</span><span class="sxs-lookup"><span data-stu-id="e8d23-120">It contains success vs. failure, as well as any response details.</span></span> |

## <a name="scheduler-entity-management"></a><span data-ttu-id="e8d23-121">Gestione di entità dell'utilità di pianificazione</span><span class="sxs-lookup"><span data-stu-id="e8d23-121">Scheduler entity management</span></span>
<span data-ttu-id="e8d23-122">A un livello elevato, l'utilità di pianificazione e l'API di gestione servizio espongono le seguenti operazioni sulle risorse:</span><span class="sxs-lookup"><span data-stu-id="e8d23-122">At a high level, the scheduler and the service management API expose the following operations on the resources:</span></span>

| <span data-ttu-id="e8d23-123">Funzionalità</span><span class="sxs-lookup"><span data-stu-id="e8d23-123">Capability</span></span> | <span data-ttu-id="e8d23-124">Descrizione e indirizzo URI</span><span class="sxs-lookup"><span data-stu-id="e8d23-124">Description and URI address</span></span> |
| --- | --- |
| <span data-ttu-id="e8d23-125">**Gestione delle raccolte di processi**</span><span class="sxs-lookup"><span data-stu-id="e8d23-125">**Job collection management**</span></span> |<span data-ttu-id="e8d23-126">Supporto di GET, PUT e DELETE per la creazione e la modifica di raccolte di processi e i processi in essi contenuti.</span><span class="sxs-lookup"><span data-stu-id="e8d23-126">GET, PUT, and DELETE support for creating and modifying job collections and the jobs contained therein.</span></span> <span data-ttu-id="e8d23-127">Una raccolta di processi è un contenitore per i processi, e mappa quote e impostazioni condivise.</span><span class="sxs-lookup"><span data-stu-id="e8d23-127">A job collection is a container for jobs and maps to quotas and shared settings.</span></span> <span data-ttu-id="e8d23-128">Esempi di quote, descritti più avanti, sono il numero massimo di processi e l'intervallo minimo delle ricorrenze.</span><span class="sxs-lookup"><span data-stu-id="e8d23-128">Examples of quotas, described later, are maximum number of jobs and smallest recurrence interval.</span></span> <p><span data-ttu-id="e8d23-129">PUT e DELETE: `https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</span><span class="sxs-lookup"><span data-stu-id="e8d23-129">PUT and DELETE: `https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</span></span></p><p><span data-ttu-id="e8d23-130">GET: `https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</span><span class="sxs-lookup"><span data-stu-id="e8d23-130">GET: `https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</span></span></p> |
| <span data-ttu-id="e8d23-131">**Gestione dei processi**</span><span class="sxs-lookup"><span data-stu-id="e8d23-131">**Job management**</span></span> |<span data-ttu-id="e8d23-132">Supporto di GET, PUT, POST, PATCH e DELETE per la creazione e modifica di processi.</span><span class="sxs-lookup"><span data-stu-id="e8d23-132">GET, PUT, POST, PATCH, and DELETE support for creating and modifying jobs.</span></span> <span data-ttu-id="e8d23-133">Tutti i processi devono appartenere a una raccolta di processi che esiste già, e che non viene creata implicitamente.</span><span class="sxs-lookup"><span data-stu-id="e8d23-133">All jobs must belong to a job collection that already exists, so there is no implicit creation.</span></span> <p>`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}/jobs/{jobName}`</p> |
| <span data-ttu-id="e8d23-134">**Gestione della cronologia dei processi**</span><span class="sxs-lookup"><span data-stu-id="e8d23-134">**Job history management**</span></span> |<span data-ttu-id="e8d23-135">Supporto GET per il recupero di 60 giorni di cronologia di esecuzioni del processo, ad esempio il tempo di esecuzione del processo e i risultati dell'esecuzione del processo.</span><span class="sxs-lookup"><span data-stu-id="e8d23-135">GET support for fetching 60 days of job execution history, such as job elapsed time and job execution results.</span></span> <span data-ttu-id="e8d23-136">Aggiunge il supporto del parametro della stringa di query per filtrare in base a stato e status.</span><span class="sxs-lookup"><span data-stu-id="e8d23-136">Adds query string parameter support for filtering based on state and status.</span></span> <P>`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}/jobs/{jobName}/history`</p> |

## <a name="job-types"></a><span data-ttu-id="e8d23-137">Tipi di processo</span><span class="sxs-lookup"><span data-stu-id="e8d23-137">Job types</span></span>
<span data-ttu-id="e8d23-138">Sono disponibili più tipi di processi: processi HTTP, inclusi quelli che supportano SSL, processi della coda di archiviazione, processi della coda del bus di servizio e processi dell'argomento del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="e8d23-138">There are multiple types of jobs: HTTP jobs (including HTTPS jobs that support SSL), storage queue jobs, service bus queue jobs, and service bus topic jobs.</span></span> <span data-ttu-id="e8d23-139">I processi HTTP sono ideali se si dispone di un endpoint di un carico di lavoro o di un servizio esistente.</span><span class="sxs-lookup"><span data-stu-id="e8d23-139">HTTP jobs are ideal if you have an endpoint of an existing workload or service.</span></span> <span data-ttu-id="e8d23-140">I processi sulle code di archiviazione consentono di inviare messaggi a code di archiviazione, per cui sono processi ideali per i carichi di lavoro che usano le code di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="e8d23-140">You can use storage queue jobs to post messages to storage queues, so those jobs are ideal for workloads that use storage queues.</span></span> <span data-ttu-id="e8d23-141">Analogamente, i processi del bus di servizio sono ideali per carichi di lavoro che usano argomenti e code del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="e8d23-141">Similarly, service bus jobs are ideal for workloads that use service bus queues and topics.</span></span>

## <a name="the-job-entity-in-detail"></a><span data-ttu-id="e8d23-142">L'entità "processo" in dettaglio</span><span class="sxs-lookup"><span data-stu-id="e8d23-142">The "job" entity in detail</span></span>
<span data-ttu-id="e8d23-143">A livello di base, un processo pianificato ha diverse parti:</span><span class="sxs-lookup"><span data-stu-id="e8d23-143">At a basic level, a scheduled job has several parts:</span></span>

* <span data-ttu-id="e8d23-144">L'azione da eseguire quando viene si attiva il timer del processo</span><span class="sxs-lookup"><span data-stu-id="e8d23-144">The action to perform when the job timer fires</span></span>  
* <span data-ttu-id="e8d23-145">(Facoltativo) Il tempo necessario per eseguire il processo</span><span class="sxs-lookup"><span data-stu-id="e8d23-145">(Optional) The time to run the job</span></span>  
* <span data-ttu-id="e8d23-146">(Facoltativo) Quando e quanto spesso ripetere il processo</span><span class="sxs-lookup"><span data-stu-id="e8d23-146">(Optional) When and how often to repeat the job</span></span>  
* <span data-ttu-id="e8d23-147">(Facoltativo) Un'azione da attivare in caso di esito negativo dell'azione primaria</span><span class="sxs-lookup"><span data-stu-id="e8d23-147">(Optional) An action to fire if the primary action fails</span></span>  

<span data-ttu-id="e8d23-148">Internamente, un processo pianificato contiene inoltre dati forniti dal sistema, ad esempio il momento di esecuzione pianificata successivo.</span><span class="sxs-lookup"><span data-stu-id="e8d23-148">Internally, a scheduled job also contains system-provided data such as the next scheduled execution time.</span></span>

<span data-ttu-id="e8d23-149">Il codice seguente fornisce un esempio completo di un processo pianificato.</span><span class="sxs-lookup"><span data-stu-id="e8d23-149">The following code provides a comprehensive example of a scheduled job.</span></span> <span data-ttu-id="e8d23-150">I dettagli vengono forniti nelle sezioni a seguire.</span><span class="sxs-lookup"><span data-stu-id="e8d23-150">Details are provided in subsequent sections.</span></span>

    {
        "startTime": "2012-08-04T00:00Z",               // optional
        "action":
        {
            "type": "http",
            "retryPolicy": { "retryType":"none" },
            "request":
            {
                "uri": "http://contoso.com/foo",        // required
                "method": "PUT",                        // required
                "body": "Posting from a timer",         // optional
                "headers":                              // optional

                {
                    "Content-Type": "application/json"
                },
            },
           "errorAction":
           {
               "type": "http",
               "request":
               {
                   "uri": "http://contoso.com/notifyError",
                   "method": "POST",
               },
           },
        },
        "recurrence":                                   // optional
        {
            "frequency": "week",                        // can be "year" "month" "day" "week" "minute"
            "interval": 1,                              // optional, how often to fire (default to 1)
            "schedule":                                 // optional (advanced scheduling specifics)
            {
                "weekDays": ["monday", "wednesday", "friday"],
                "hours": [10, 22]
            },
            "count": 10,                                 // optional (default to recur infinitely)
            "endTime": "2012-11-04",                     // optional (default to recur infinitely)
        },
        "state": "disabled",                           // enabled or disabled
        "status":                                       // controlled by Scheduler service
        {
            "lastExecutionTime": "2007-03-01T13:00:00Z",
            "nextExecutionTime": "2007-03-01T14:00:00Z ",
            "executionCount": 3,
                                                "failureCount": 0,
                                                "faultedCount": 0
        },
    }

<span data-ttu-id="e8d23-151">Come illustrato nell'utilità di pianificazione di esempio sopra riportato, la definizione di un processo ha diverse parti:</span><span class="sxs-lookup"><span data-stu-id="e8d23-151">As seen in the sample scheduled job above, a job definition has several parts:</span></span>

* <span data-ttu-id="e8d23-152">Ora di inizio ("startTime")</span><span class="sxs-lookup"><span data-stu-id="e8d23-152">Start time (“startTime”)</span></span>  
* <span data-ttu-id="e8d23-153">Azione ("action"), che include l'azione in caso di errore ("errorAction")</span><span class="sxs-lookup"><span data-stu-id="e8d23-153">Action (“action”), which includes error action (“errorAction”)</span></span>
* <span data-ttu-id="e8d23-154">Ricorrenza ("recurrence")</span><span class="sxs-lookup"><span data-stu-id="e8d23-154">Recurrence (“recurrence”)</span></span>  
* <span data-ttu-id="e8d23-155">Stato (“state”)</span><span class="sxs-lookup"><span data-stu-id="e8d23-155">State (“state”)</span></span>  
* <span data-ttu-id="e8d23-156">Status (“status”)</span><span class="sxs-lookup"><span data-stu-id="e8d23-156">Status (“status”)</span></span>  
* <span data-ttu-id="e8d23-157">Criterio di ripetizione (“retryPolicy”)</span><span class="sxs-lookup"><span data-stu-id="e8d23-157">Retry policy (“retryPolicy”)</span></span>  

<span data-ttu-id="e8d23-158">Esaminiamo ciascuna in modo dettagliato:</span><span class="sxs-lookup"><span data-stu-id="e8d23-158">Let’s examine each of these in detail:</span></span>

## <a name="starttime"></a><span data-ttu-id="e8d23-159">startTime</span><span class="sxs-lookup"><span data-stu-id="e8d23-159">startTime</span></span>
<span data-ttu-id="e8d23-160">"startTime" è l'ora di inizio e consente al chiamante di specificare una differenza di fuso orario in transito in [formato ISO-8601](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="e8d23-160">The "startTime” is the start time and allows the caller to specify a time zone offset on the wire in [ISO-8601 format](http://en.wikipedia.org/wiki/ISO_8601).</span></span>

## <a name="action-and-erroraction"></a><span data-ttu-id="e8d23-161">action ed errorAction</span><span class="sxs-lookup"><span data-stu-id="e8d23-161">action and errorAction</span></span>
<span data-ttu-id="e8d23-162">"action" è l'azione richiamata a ogni occorrenza, e descrive un tipo di chiamata di servizio.</span><span class="sxs-lookup"><span data-stu-id="e8d23-162">The “action” is the action invoked on each occurrence and describes a type of service invocation.</span></span> <span data-ttu-id="e8d23-163">L'azione è ciò che verrà eseguito nella pianificazione specificata.</span><span class="sxs-lookup"><span data-stu-id="e8d23-163">The action is what will be executed on the provided schedule.</span></span> <span data-ttu-id="e8d23-164">L'Utilità di pianificazione supporta azioni della coda del bus di servizio, dell'argomento del bus di servizio, della coda di archiviazione e HTTP.</span><span class="sxs-lookup"><span data-stu-id="e8d23-164">Scheduler supports HTTP, storage queue, service bus topic, and service bus queue actions.</span></span>

<span data-ttu-id="e8d23-165">L'azione nell'esempio precedente è un'azione HTTP.</span><span class="sxs-lookup"><span data-stu-id="e8d23-165">The action in the example above is an HTTP action.</span></span> <span data-ttu-id="e8d23-166">Di seguito è riportato un esempio di un'azione in coda di archiviazione:</span><span class="sxs-lookup"><span data-stu-id="e8d23-166">Below is an example of a storage queue action:</span></span>

    {
            "type": "storageQueue",
            "queueMessage":
            {
                "storageAccount": "myStorageAccount",  // required
                "queueName": "myqueue",                // required
                "sasToken": "TOKEN",                   // required
                "message":                             // required
                    "My message body",
            },
    }

<span data-ttu-id="e8d23-167">Di seguito è riportato un esempio di azione dell'argomento del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="e8d23-167">Below is an example of a service bus topic action.</span></span>

  <span data-ttu-id="e8d23-168">"action": { "type": "serviceBusTopic", "serviceBusTopicMessage": { "topicPath": "t1",</span><span class="sxs-lookup"><span data-stu-id="e8d23-168">"action": { "type": "serviceBusTopic", "serviceBusTopicMessage": { "topicPath": "t1",</span></span>  
      <span data-ttu-id="e8d23-169">"namespace": "mySBNamespace", "transportType": "netMessaging", // Can be either netMessaging or AMQP "authentication": { "sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Some message", "brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, }</span><span class="sxs-lookup"><span data-stu-id="e8d23-169">"namespace": "mySBNamespace", "transportType": "netMessaging", // Can be either netMessaging or AMQP "authentication": { "sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Some message", "brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, }</span></span>

<span data-ttu-id="e8d23-170">Di seguito è riportato un esempio di azione di coda del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="e8d23-170">Below is an example of a service bus queue action:</span></span>

  <span data-ttu-id="e8d23-171">"action": { "serviceBusQueueMessage": { "queueName": "q1",</span><span class="sxs-lookup"><span data-stu-id="e8d23-171">"action": { "serviceBusQueueMessage": { "queueName": "q1",</span></span>  
      <span data-ttu-id="e8d23-172">"namespace": "mySBNamespace", "transportType": "netMessaging", // Can be either netMessaging or AMQP "authentication": {</span><span class="sxs-lookup"><span data-stu-id="e8d23-172">"namespace": "mySBNamespace", "transportType": "netMessaging", // Can be either netMessaging or AMQP "authentication": {</span></span>  
        <span data-ttu-id="e8d23-173">"sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Some message",</span><span class="sxs-lookup"><span data-stu-id="e8d23-173">"sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Some message",</span></span>  
      <span data-ttu-id="e8d23-174">"brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, "type": "serviceBusQueue" }</span><span class="sxs-lookup"><span data-stu-id="e8d23-174">"brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, "type": "serviceBusQueue" }</span></span>

<span data-ttu-id="e8d23-175">"errorAction" è il gestore degli errori, l'azione viene richiamata quando l'azione principale ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="e8d23-175">The “errorAction” is the error handler, the action invoked when the primary action fails.</span></span> <span data-ttu-id="e8d23-176">È possibile usare questa variabile per chiamare un endpoint di gestione degli errori o per inviare una notifica all'utente.</span><span class="sxs-lookup"><span data-stu-id="e8d23-176">You can use this variable to call an error-handling endpoint or send a user notification.</span></span> <span data-ttu-id="e8d23-177">Ciò può essere usato per raggiungere un endpoint secondario in caso quello primario non sia disponibile (ad esempio, in caso di emergenza nel sito dell'endpoint) o può essere usato per notificare un endpoint che si occupi di gestire gli errori.</span><span class="sxs-lookup"><span data-stu-id="e8d23-177">This can be used for reaching a secondary endpoint in the case that the primary is not available (e.g., in the case of a disaster at the endpoint’s site) or can be used for notifying an error handling endpoint.</span></span> <span data-ttu-id="e8d23-178">Proprio come l'azione principale, l'azione di errore può essere semplice o a logica composita basata su altre azioni.</span><span class="sxs-lookup"><span data-stu-id="e8d23-178">Just like the primary action, the error action can be simple or composite logic based on other actions.</span></span> <span data-ttu-id="e8d23-179">Per informazione su come creare un token SAS, fare riferimento a [Creare e utilizzare una firma di accesso condiviso](https://msdn.microsoft.com/library/azure/jj721951.aspx).</span><span class="sxs-lookup"><span data-stu-id="e8d23-179">To learn how to create a SAS token, refer to [Create and Use a Shared Access Signature](https://msdn.microsoft.com/library/azure/jj721951.aspx).</span></span>

## <a name="recurrence"></a><span data-ttu-id="e8d23-180">ricorrenza</span><span class="sxs-lookup"><span data-stu-id="e8d23-180">recurrence</span></span>
<span data-ttu-id="e8d23-181">La ricorrenza ha diverse parti:</span><span class="sxs-lookup"><span data-stu-id="e8d23-181">Recurrence has several parts:</span></span>

* <span data-ttu-id="e8d23-182">Frequenza: Un valore tra minuto, ora, giorno, settimana, mese, anno</span><span class="sxs-lookup"><span data-stu-id="e8d23-182">Frequency: One of minute, hour, day, week, month, year</span></span>  
* <span data-ttu-id="e8d23-183">Intervallo: Intervallo alla frequenza specificata per la ricorrenza</span><span class="sxs-lookup"><span data-stu-id="e8d23-183">Interval: Interval at the given frequency for the recurrence</span></span>  
* <span data-ttu-id="e8d23-184">Pianificazione prescritta: Specifica minuti, ore, giorni della settimana, mesi e giorni del mese della ricorrenza</span><span class="sxs-lookup"><span data-stu-id="e8d23-184">Prescribed schedule: Specify minutes, hours, weekdays, months, and monthdays of the recurrence</span></span>  
* <span data-ttu-id="e8d23-185">Conteggio: Conteggio delle occorrenze</span><span class="sxs-lookup"><span data-stu-id="e8d23-185">Count: Count of occurrences</span></span>  
* <span data-ttu-id="e8d23-186">Ora di fine: Nessun processo verrà eseguito dopo l'ora di fine specificata</span><span class="sxs-lookup"><span data-stu-id="e8d23-186">End time: No jobs will execute after the specified end time</span></span>  

<span data-ttu-id="e8d23-187">Un processo è ricorrente se dispone di un oggetto ricorrente specificato nella sua definizione JSON.</span><span class="sxs-lookup"><span data-stu-id="e8d23-187">A job is recurring if it has a recurring object specified in its JSON definition.</span></span> <span data-ttu-id="e8d23-188">Se sono specificati sia conteggio che l'ora di fine, viene applicata la regola di completamento che si verifica per primo.</span><span class="sxs-lookup"><span data-stu-id="e8d23-188">If both count and endTime are specified, the completion rule that occurs first is honored.</span></span>

## <a name="state"></a><span data-ttu-id="e8d23-189">state</span><span class="sxs-lookup"><span data-stu-id="e8d23-189">state</span></span>
<span data-ttu-id="e8d23-190">Lo stato del processo è uno di questi quattro valori: abilitato, disabilitato, completato o in errore.</span><span class="sxs-lookup"><span data-stu-id="e8d23-190">The state of the job is one of four values: enabled, disabled, completed, or faulted.</span></span> <span data-ttu-id="e8d23-191">È possibile eseguire azioni PUT o PATCH sui processi per aggiornarli allo stato abilitato o disabilitato.</span><span class="sxs-lookup"><span data-stu-id="e8d23-191">You can PUT or PATCH jobs so as to update them to the enabled or disabled state.</span></span> <span data-ttu-id="e8d23-192">Se un processo è stato completato o in errore, si trova in uno stato finale che non può essere aggiornato (anche se è comunque possibile eliminare il processo).</span><span class="sxs-lookup"><span data-stu-id="e8d23-192">If a job has been completed or faulted, that is a final state that cannot be updated (though the job can still be DELETED).</span></span> <span data-ttu-id="e8d23-193">Un esempio della proprietà stato è come segue:</span><span class="sxs-lookup"><span data-stu-id="e8d23-193">An example of the state property is as follows:</span></span>

        "state": "disabled", // enabled, disabled, completed, or faulted
<span data-ttu-id="e8d23-194">I processi completati e con errori vengono eliminati dopo 60 giorni.</span><span class="sxs-lookup"><span data-stu-id="e8d23-194">Completed and faulted jobs are deleted after 60 days.</span></span>

## <a name="status"></a><span data-ttu-id="e8d23-195">status</span><span class="sxs-lookup"><span data-stu-id="e8d23-195">status</span></span>
<span data-ttu-id="e8d23-196">Dopo l'avvio dell'Utilità di pianificazione, verranno restituite informazioni sullo stato corrente del processo.</span><span class="sxs-lookup"><span data-stu-id="e8d23-196">Once a Scheduler job has started, information will be returned about the current status of the job.</span></span> <span data-ttu-id="e8d23-197">Questo oggetto non può essere impostato dall'utente: è impostato dal sistema.</span><span class="sxs-lookup"><span data-stu-id="e8d23-197">This object is not settable by the user—it’s set by the system.</span></span> <span data-ttu-id="e8d23-198">Tuttavia, è incluso nell'oggetto processo (anziché in una risorsa collegata separata) in modo da consentire di ottenere semplicemente lo stato di un processo.</span><span class="sxs-lookup"><span data-stu-id="e8d23-198">However, it is included in the job object (rather than a separate linked resource) so that one can obtain the status of a job easily.</span></span>

<span data-ttu-id="e8d23-199">Lo stato del processo include l'ora dell'esecuzione precedente (se presente), l'ora della successiva esecuzione pianificata (per i processi in corso) e il conteggio delle esecuzioni del processo.</span><span class="sxs-lookup"><span data-stu-id="e8d23-199">Job status includes the time of the previous execution (if any), the time of the next scheduled execution (for in-progress jobs), and the execution count of the job.</span></span>

## <a name="retrypolicy"></a><span data-ttu-id="e8d23-200">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="e8d23-200">retryPolicy</span></span>
<span data-ttu-id="e8d23-201">Se un'utilità di pianificazione non riesce, è possibile specificare un criterio di ripetizione per determinare se e come l'azione verrà ripetuta.</span><span class="sxs-lookup"><span data-stu-id="e8d23-201">If a Scheduler job fails, it is possible to specify a retry policy to determine whether and how the action is retried.</span></span> <span data-ttu-id="e8d23-202">Ciò è determinato dall'oggetto **retryType**: è impostato su **nessuno** se non esiste alcun criterio di ripetizione, come illustrato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="e8d23-202">This is determined by the **retryType** object—it is set to **none** if there is no retry policy, as shown above.</span></span> <span data-ttu-id="e8d23-203">Impostato su **fisso** se esiste un criterio di ripetizione.</span><span class="sxs-lookup"><span data-stu-id="e8d23-203">Set it to **fixed** if there is a retry policy.</span></span>

<span data-ttu-id="e8d23-204">Per impostare un criterio di ripetizione, è possibile specificare due impostazioni aggiuntive: un intervallo tra i tentativi (**retryInterval**) e il numero di tentativi (**retryCount**).</span><span class="sxs-lookup"><span data-stu-id="e8d23-204">To set a retry policy, two additional settings may be specified: a retry interval (**retryInterval**) and the number of retries (**retryCount**).</span></span>

<span data-ttu-id="e8d23-205">L'intervallo tra tentativi, specificato con l'oggetto **retryInterval** , è l'intervallo di tempo tra i tentativi.</span><span class="sxs-lookup"><span data-stu-id="e8d23-205">The retry interval, specified with the **retryInterval** object, is the interval between retries.</span></span> <span data-ttu-id="e8d23-206">Il valore predefinito è 30 secondi, il valore minimo configurabile è 15 secondi e il valore massimo è 18 mesi.</span><span class="sxs-lookup"><span data-stu-id="e8d23-206">Its default value is 30 seconds, its minimum configurable value is 15 seconds, and its maximum value is 18 months.</span></span> <span data-ttu-id="e8d23-207">I processi inclusi nelle raccolte di processi del livello Gratuito hanno un valore minimo configurabile di 1 ora.</span><span class="sxs-lookup"><span data-stu-id="e8d23-207">Jobs in Free job collections have a minimum configurable value of 1 hour.</span></span>  <span data-ttu-id="e8d23-208">Viene definito nel formato ISO 8601.</span><span class="sxs-lookup"><span data-stu-id="e8d23-208">It is defined in the ISO 8601 format.</span></span> <span data-ttu-id="e8d23-209">Analogamente, il valore del numero di tentativi è specificato con l'oggetto **retryCount** e specifica quanti tentativi verranno eseguiti.</span><span class="sxs-lookup"><span data-stu-id="e8d23-209">Similarly, the value of the number of retries is specified with the **retryCount** object; it is the number of times a retry is attempted.</span></span> <span data-ttu-id="e8d23-210">Il valore predefinito è 4 e il valore massimo è 20\.</span><span class="sxs-lookup"><span data-stu-id="e8d23-210">Its default value is 4, and its maximum value is 20\.</span></span> <span data-ttu-id="e8d23-211">Entrambi **retryInterval** e **retryCount** sono facoltativi.</span><span class="sxs-lookup"><span data-stu-id="e8d23-211">Both **retryInterval** and **retryCount** are optional.</span></span> <span data-ttu-id="e8d23-212">A questi oggetti vengono assegnati i valori predefiniti se **retryType** è impostato su **fixed** e non sono specificati valori in modo esplicito.</span><span class="sxs-lookup"><span data-stu-id="e8d23-212">They are given their default values if **retryType** is set to **fixed** and no values are specified explicitly.</span></span>

## <a name="see-also"></a><span data-ttu-id="e8d23-213">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="e8d23-213">See also</span></span>
 [<span data-ttu-id="e8d23-214">Che cos'è l'Utilità di pianificazione?</span><span class="sxs-lookup"><span data-stu-id="e8d23-214">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="e8d23-215">Introduzione all'uso dell'Utilità di pianificazione nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="e8d23-215">Get started using Scheduler in the Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="e8d23-216">Piani e fatturazione nell'utilità di pianificazione di Azure</span><span class="sxs-lookup"><span data-stu-id="e8d23-216">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="e8d23-217">Come creare pianificazioni complesse e operazioni ricorrenti avanzate con l'Utilità di pianificazione di Azure</span><span class="sxs-lookup"><span data-stu-id="e8d23-217">How to build complex schedules and advanced recurrence with Azure Scheduler</span></span>](scheduler-advanced-complexity.md)

 [<span data-ttu-id="e8d23-218">Informazioni di riferimento sull'API REST dell'Utilità di pianificazione di Azure</span><span class="sxs-lookup"><span data-stu-id="e8d23-218">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="e8d23-219">Informazioni di riferimento sui cmdlet PowerShell dell'Utilità di pianificazione di Azure</span><span class="sxs-lookup"><span data-stu-id="e8d23-219">Azure Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="e8d23-220">Livelli elevati di disponibilità e affidabilità dell'Utilità di pianificazione di Azure</span><span class="sxs-lookup"><span data-stu-id="e8d23-220">Azure Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="e8d23-221">Limiti, valori predefiniti e codici di errore dell'Utilità di pianificazione di Azure</span><span class="sxs-lookup"><span data-stu-id="e8d23-221">Azure Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

 [<span data-ttu-id="e8d23-222">Autenticazione in uscita dell'Utilità di pianificazione di Azure</span><span class="sxs-lookup"><span data-stu-id="e8d23-222">Azure Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

