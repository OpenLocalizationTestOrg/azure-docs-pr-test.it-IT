---
title: "aaaScheduler entità, concetti e termini | Documenti Microsoft"
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
ms.openlocfilehash: 73e7de7bfd2937e401aeab05e0e10fa292cf37b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="scheduler-concepts-terminology--entity-hierarchy"></a><span data-ttu-id="58acd-104">Concetti, terminologia e gerarchia di entità dell'Utilità di pianificazione</span><span class="sxs-lookup"><span data-stu-id="58acd-104">Scheduler concepts, terminology, + entity hierarchy</span></span>
## <a name="scheduler-entity-hierarchy"></a><span data-ttu-id="58acd-105">Gerarchia di entità dell'Utilità di pianificazione</span><span class="sxs-lookup"><span data-stu-id="58acd-105">Scheduler entity hierarchy</span></span>
<span data-ttu-id="58acd-106">Hello nella tabella seguente descrive hello risorse principali esposte o usate dall'API dell'utilità di pianificazione hello:</span><span class="sxs-lookup"><span data-stu-id="58acd-106">hello following table describes hello main resources exposed or used by hello Scheduler API:</span></span>

| <span data-ttu-id="58acd-107">Risorsa</span><span class="sxs-lookup"><span data-stu-id="58acd-107">Resource</span></span> | <span data-ttu-id="58acd-108">Descrizione</span><span class="sxs-lookup"><span data-stu-id="58acd-108">Description</span></span> |
| --- | --- |
| <span data-ttu-id="58acd-109">**Raccolta di processi**</span><span class="sxs-lookup"><span data-stu-id="58acd-109">**Job collection**</span></span> |<span data-ttu-id="58acd-110">Una raccolta di processi contiene un gruppo di processi e gestisce le impostazioni, le quote e le limitazioni condivise dai processi all'interno di raccolta hello.</span><span class="sxs-lookup"><span data-stu-id="58acd-110">A job collection contains a group of jobs and maintains settings, quotas, and throttles that are shared by jobs within hello collection.</span></span> <span data-ttu-id="58acd-111">Le raccolte di processi vengono create dal proprietario della sottoscrizione e raggruppano i processi in base ai limiti di utilizzo o dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="58acd-111">A job collection is created by a subscription owner and groups jobs together based on usage or application boundaries.</span></span> <span data-ttu-id="58acd-112">È vincolata tooone area.</span><span class="sxs-lookup"><span data-stu-id="58acd-112">It’s constrained tooone region.</span></span> <span data-ttu-id="58acd-113">Consente inoltre l'applicazione hello di quote di utilizzo hello tooconstrain di tutti i processi in tale raccolta.</span><span class="sxs-lookup"><span data-stu-id="58acd-113">It also allows hello enforcement of quotas tooconstrain hello usage of all jobs in that collection.</span></span> <span data-ttu-id="58acd-114">le quote di Hello includono MaxJobs e MaxRecurrence.</span><span class="sxs-lookup"><span data-stu-id="58acd-114">hello quotas include MaxJobs and MaxRecurrence.</span></span> |
| <span data-ttu-id="58acd-115">**Processo**</span><span class="sxs-lookup"><span data-stu-id="58acd-115">**Job**</span></span> |<span data-ttu-id="58acd-116">Un processo definisce una singola azione ricorrente, con strategie semplici o complesse per l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="58acd-116">A job defines a single recurrent action, with simple or complex strategies for execution.</span></span> <span data-ttu-id="58acd-117">Le azioni possono includere HTTP, coda di archiviazione, coda del bus di servizio o richieste di argomento del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="58acd-117">Actions may include HTTP, storage queue, service bus queue, or service bus topic requests.</span></span> |
| <span data-ttu-id="58acd-118">**Cronologia processi**</span><span class="sxs-lookup"><span data-stu-id="58acd-118">**Job history**</span></span> |<span data-ttu-id="58acd-119">Una cronologia processi rappresenta i dettagli per l'esecuzione di un processo.</span><span class="sxs-lookup"><span data-stu-id="58acd-119">A job history represents details for an execution of a job.</span></span> <span data-ttu-id="58acd-120">Contiene esito positivo o negativo, nonché i dettagli della risposta.</span><span class="sxs-lookup"><span data-stu-id="58acd-120">It contains success vs. failure, as well as any response details.</span></span> |

## <a name="scheduler-entity-management"></a><span data-ttu-id="58acd-121">Gestione di entità dell'utilità di pianificazione</span><span class="sxs-lookup"><span data-stu-id="58acd-121">Scheduler entity management</span></span>
<span data-ttu-id="58acd-122">In generale, utilità di pianificazione di hello e API di Gestione servizio hello esporre hello dopo le operazioni sulle risorse hello:</span><span class="sxs-lookup"><span data-stu-id="58acd-122">At a high level, hello scheduler and hello service management API expose hello following operations on hello resources:</span></span>

| <span data-ttu-id="58acd-123">Funzionalità</span><span class="sxs-lookup"><span data-stu-id="58acd-123">Capability</span></span> | <span data-ttu-id="58acd-124">Descrizione e indirizzo URI</span><span class="sxs-lookup"><span data-stu-id="58acd-124">Description and URI address</span></span> |
| --- | --- |
| <span data-ttu-id="58acd-125">**Gestione delle raccolte di processi**</span><span class="sxs-lookup"><span data-stu-id="58acd-125">**Job collection management**</span></span> |<span data-ttu-id="58acd-126">GET, PUT, supporto e DELETE per la creazione e modifica di raccolte di processi e i processi di hello in esso contenuti.</span><span class="sxs-lookup"><span data-stu-id="58acd-126">GET, PUT, and DELETE support for creating and modifying job collections and hello jobs contained therein.</span></span> <span data-ttu-id="58acd-127">Una raccolta di processi è un contenitore per i processi e viene eseguito il mapping tooquotas e le impostazioni condivise.</span><span class="sxs-lookup"><span data-stu-id="58acd-127">A job collection is a container for jobs and maps tooquotas and shared settings.</span></span> <span data-ttu-id="58acd-128">Esempi di quote, descritti più avanti, sono il numero massimo di processi e l'intervallo minimo delle ricorrenze.</span><span class="sxs-lookup"><span data-stu-id="58acd-128">Examples of quotas, described later, are maximum number of jobs and smallest recurrence interval.</span></span> <p><span data-ttu-id="58acd-129">PUT e DELETE: `https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</span><span class="sxs-lookup"><span data-stu-id="58acd-129">PUT and DELETE: `https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</span></span></p><p><span data-ttu-id="58acd-130">GET: `https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</span><span class="sxs-lookup"><span data-stu-id="58acd-130">GET: `https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</span></span></p> |
| <span data-ttu-id="58acd-131">**Gestione dei processi**</span><span class="sxs-lookup"><span data-stu-id="58acd-131">**Job management**</span></span> |<span data-ttu-id="58acd-132">Supporto di GET, PUT, POST, PATCH e DELETE per la creazione e modifica di processi.</span><span class="sxs-lookup"><span data-stu-id="58acd-132">GET, PUT, POST, PATCH, and DELETE support for creating and modifying jobs.</span></span> <span data-ttu-id="58acd-133">Tutti i processi devono appartenere tooa raccolta di processi che esiste già, pertanto non c'è alcuna creazione implicita.</span><span class="sxs-lookup"><span data-stu-id="58acd-133">All jobs must belong tooa job collection that already exists, so there is no implicit creation.</span></span> <p>`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}/jobs/{jobName}`</p> |
| <span data-ttu-id="58acd-134">**Gestione della cronologia dei processi**</span><span class="sxs-lookup"><span data-stu-id="58acd-134">**Job history management**</span></span> |<span data-ttu-id="58acd-135">Supporto GET per il recupero di 60 giorni di cronologia di esecuzioni del processo, ad esempio il tempo di esecuzione del processo e i risultati dell'esecuzione del processo.</span><span class="sxs-lookup"><span data-stu-id="58acd-135">GET support for fetching 60 days of job execution history, such as job elapsed time and job execution results.</span></span> <span data-ttu-id="58acd-136">Aggiunge il supporto del parametro della stringa di query per filtrare in base a stato e status.</span><span class="sxs-lookup"><span data-stu-id="58acd-136">Adds query string parameter support for filtering based on state and status.</span></span> <P>`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}/jobs/{jobName}/history`</p> |

## <a name="job-types"></a><span data-ttu-id="58acd-137">Tipi di processo</span><span class="sxs-lookup"><span data-stu-id="58acd-137">Job types</span></span>
<span data-ttu-id="58acd-138">Sono disponibili più tipi di processi: processi HTTP, inclusi quelli che supportano SSL, processi della coda di archiviazione, processi della coda del bus di servizio e processi dell'argomento del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="58acd-138">There are multiple types of jobs: HTTP jobs (including HTTPS jobs that support SSL), storage queue jobs, service bus queue jobs, and service bus topic jobs.</span></span> <span data-ttu-id="58acd-139">I processi HTTP sono ideali se si dispone di un endpoint di un carico di lavoro o di un servizio esistente.</span><span class="sxs-lookup"><span data-stu-id="58acd-139">HTTP jobs are ideal if you have an endpoint of an existing workload or service.</span></span> <span data-ttu-id="58acd-140">È possibile utilizzare coda processi toopost messaggi toostorage code di archiviazione, pertanto questi processi sono ideali per i carichi di lavoro che usano code di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="58acd-140">You can use storage queue jobs toopost messages toostorage queues, so those jobs are ideal for workloads that use storage queues.</span></span> <span data-ttu-id="58acd-141">Analogamente, i processi del bus di servizio sono ideali per carichi di lavoro che usano argomenti e code del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="58acd-141">Similarly, service bus jobs are ideal for workloads that use service bus queues and topics.</span></span>

## <a name="hello-job-entity-in-detail"></a><span data-ttu-id="58acd-142">entità "processo" Hello in dettaglio</span><span class="sxs-lookup"><span data-stu-id="58acd-142">hello "job" entity in detail</span></span>
<span data-ttu-id="58acd-143">A livello di base, un processo pianificato ha diverse parti:</span><span class="sxs-lookup"><span data-stu-id="58acd-143">At a basic level, a scheduled job has several parts:</span></span>

* <span data-ttu-id="58acd-144">Hello tooperform azione quando il timer di processo hello</span><span class="sxs-lookup"><span data-stu-id="58acd-144">hello action tooperform when hello job timer fires</span></span>  
* <span data-ttu-id="58acd-145">Processo di hello toorun ora hello (facoltativo)</span><span class="sxs-lookup"><span data-stu-id="58acd-145">(Optional) hello time toorun hello job</span></span>  
* <span data-ttu-id="58acd-146">(Facoltativo) Quando e con quale frequenza processo hello toorepeat</span><span class="sxs-lookup"><span data-stu-id="58acd-146">(Optional) When and how often toorepeat hello job</span></span>  
* <span data-ttu-id="58acd-147">(Facoltativo) Toofire un'azione se hello primario azione ha esito negativo</span><span class="sxs-lookup"><span data-stu-id="58acd-147">(Optional) An action toofire if hello primary action fails</span></span>  

<span data-ttu-id="58acd-148">Internamente, un processo pianificato contiene inoltre dati forniti dal sistema, ad esempio il tempo di esecuzione di hello successivo pianificato.</span><span class="sxs-lookup"><span data-stu-id="58acd-148">Internally, a scheduled job also contains system-provided data such as hello next scheduled execution time.</span></span>

<span data-ttu-id="58acd-149">Hello di codice seguente fornisce un esempio completo di un processo pianificato.</span><span class="sxs-lookup"><span data-stu-id="58acd-149">hello following code provides a comprehensive example of a scheduled job.</span></span> <span data-ttu-id="58acd-150">I dettagli vengono forniti nelle sezioni a seguire.</span><span class="sxs-lookup"><span data-stu-id="58acd-150">Details are provided in subsequent sections.</span></span>

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
            "interval": 1,                              // optional, how often toofire (default too1)
            "schedule":                                 // optional (advanced scheduling specifics)
            {
                "weekDays": ["monday", "wednesday", "friday"],
                "hours": [10, 22]
            },
            "count": 10,                                 // optional (default toorecur infinitely)
            "endTime": "2012-11-04",                     // optional (default toorecur infinitely)
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

<span data-ttu-id="58acd-151">Come osservato nel hello esempio processo pianificato precedente, definizione di un processo è costituito da parti diverse:</span><span class="sxs-lookup"><span data-stu-id="58acd-151">As seen in hello sample scheduled job above, a job definition has several parts:</span></span>

* <span data-ttu-id="58acd-152">Ora di inizio ("startTime")</span><span class="sxs-lookup"><span data-stu-id="58acd-152">Start time (“startTime”)</span></span>  
* <span data-ttu-id="58acd-153">Azione ("action"), che include l'azione in caso di errore ("errorAction")</span><span class="sxs-lookup"><span data-stu-id="58acd-153">Action (“action”), which includes error action (“errorAction”)</span></span>
* <span data-ttu-id="58acd-154">Ricorrenza ("recurrence")</span><span class="sxs-lookup"><span data-stu-id="58acd-154">Recurrence (“recurrence”)</span></span>  
* <span data-ttu-id="58acd-155">Stato (“state”)</span><span class="sxs-lookup"><span data-stu-id="58acd-155">State (“state”)</span></span>  
* <span data-ttu-id="58acd-156">Status (“status”)</span><span class="sxs-lookup"><span data-stu-id="58acd-156">Status (“status”)</span></span>  
* <span data-ttu-id="58acd-157">Criterio di ripetizione (“retryPolicy”)</span><span class="sxs-lookup"><span data-stu-id="58acd-157">Retry policy (“retryPolicy”)</span></span>  

<span data-ttu-id="58acd-158">Esaminiamo ciascuna in modo dettagliato:</span><span class="sxs-lookup"><span data-stu-id="58acd-158">Let’s examine each of these in detail:</span></span>

## <a name="starttime"></a><span data-ttu-id="58acd-159">startTime</span><span class="sxs-lookup"><span data-stu-id="58acd-159">startTime</span></span>
<span data-ttu-id="58acd-160">Hello "startTime" è l'ora di inizio hello e consente di hello chiamante toospecify un fuso orario offset durante la trasmissione hello in [formato ISO 8601](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="58acd-160">hello "startTime” is hello start time and allows hello caller toospecify a time zone offset on hello wire in [ISO-8601 format](http://en.wikipedia.org/wiki/ISO_8601).</span></span>

## <a name="action-and-erroraction"></a><span data-ttu-id="58acd-161">action ed errorAction</span><span class="sxs-lookup"><span data-stu-id="58acd-161">action and errorAction</span></span>
<span data-ttu-id="58acd-162">azione"Hello" hello azione richiamata a ogni occorrenza e descrive un tipo di chiamata del servizio.</span><span class="sxs-lookup"><span data-stu-id="58acd-162">hello “action” is hello action invoked on each occurrence and describes a type of service invocation.</span></span> <span data-ttu-id="58acd-163">azione di Hello è ciò che verrà eseguito su hello fornito pianificazione.</span><span class="sxs-lookup"><span data-stu-id="58acd-163">hello action is what will be executed on hello provided schedule.</span></span> <span data-ttu-id="58acd-164">L'Utilità di pianificazione supporta azioni della coda del bus di servizio, dell'argomento del bus di servizio, della coda di archiviazione e HTTP.</span><span class="sxs-lookup"><span data-stu-id="58acd-164">Scheduler supports HTTP, storage queue, service bus topic, and service bus queue actions.</span></span>

<span data-ttu-id="58acd-165">azione di Hello nell'esempio hello precedente è un'azione HTTP.</span><span class="sxs-lookup"><span data-stu-id="58acd-165">hello action in hello example above is an HTTP action.</span></span> <span data-ttu-id="58acd-166">Di seguito è riportato un esempio di un'azione in coda di archiviazione:</span><span class="sxs-lookup"><span data-stu-id="58acd-166">Below is an example of a storage queue action:</span></span>

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

<span data-ttu-id="58acd-167">Di seguito è riportato un esempio di azione dell'argomento del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="58acd-167">Below is an example of a service bus topic action.</span></span>

  <span data-ttu-id="58acd-168">"action": { "type": "serviceBusTopic", "serviceBusTopicMessage": { "topicPath": "t1",</span><span class="sxs-lookup"><span data-stu-id="58acd-168">"action": { "type": "serviceBusTopic", "serviceBusTopicMessage": { "topicPath": "t1",</span></span>  
      <span data-ttu-id="58acd-169">"namespace": "mySBNamespace", "transportType": "netMessaging", // Can be either netMessaging or AMQP "authentication": { "sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Some message", "brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, }</span><span class="sxs-lookup"><span data-stu-id="58acd-169">"namespace": "mySBNamespace", "transportType": "netMessaging", // Can be either netMessaging or AMQP "authentication": { "sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Some message", "brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, }</span></span>

<span data-ttu-id="58acd-170">Di seguito è riportato un esempio di azione di coda del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="58acd-170">Below is an example of a service bus queue action:</span></span>

  <span data-ttu-id="58acd-171">"action": { "serviceBusQueueMessage": { "queueName": "q1",</span><span class="sxs-lookup"><span data-stu-id="58acd-171">"action": { "serviceBusQueueMessage": { "queueName": "q1",</span></span>  
      <span data-ttu-id="58acd-172">"namespace": "mySBNamespace", "transportType": "netMessaging", // Can be either netMessaging or AMQP "authentication": {</span><span class="sxs-lookup"><span data-stu-id="58acd-172">"namespace": "mySBNamespace", "transportType": "netMessaging", // Can be either netMessaging or AMQP "authentication": {</span></span>  
        <span data-ttu-id="58acd-173">"sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Some message",</span><span class="sxs-lookup"><span data-stu-id="58acd-173">"sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Some message",</span></span>  
      <span data-ttu-id="58acd-174">"brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, "type": "serviceBusQueue" }</span><span class="sxs-lookup"><span data-stu-id="58acd-174">"brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, "type": "serviceBusQueue" }</span></span>

<span data-ttu-id="58acd-175">Hello "errorAction" è del gestore degli errori di hello azione hello viene richiamato quando l'azione principale hello ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="58acd-175">hello “errorAction” is hello error handler, hello action invoked when hello primary action fails.</span></span> <span data-ttu-id="58acd-176">È possibile utilizzare questa variabile toocall un endpoint di gestione degli errori o inviare una notifica all'utente.</span><span class="sxs-lookup"><span data-stu-id="58acd-176">You can use this variable toocall an error-handling endpoint or send a user notification.</span></span> <span data-ttu-id="58acd-177">Può essere utilizzato per raggiungere un endpoint secondario in caso di hello che hello primario non è disponibile (ad esempio, in caso di hello un'emergenza nel sito dell'endpoint hello) o può essere utilizzato per la notifica di un endpoint di gestione degli errori.</span><span class="sxs-lookup"><span data-stu-id="58acd-177">This can be used for reaching a secondary endpoint in hello case that hello primary is not available (e.g., in hello case of a disaster at hello endpoint’s site) or can be used for notifying an error handling endpoint.</span></span> <span data-ttu-id="58acd-178">Come azione principale hello, azione di errore hello può essere semplice o composta logica in base ad altre azioni.</span><span class="sxs-lookup"><span data-stu-id="58acd-178">Just like hello primary action, hello error action can be simple or composite logic based on other actions.</span></span> <span data-ttu-id="58acd-179">toolearn come toocreate un token di firma di accesso condiviso, fare riferimento troppo[creare e usare una firma di accesso condiviso](https://msdn.microsoft.com/library/azure/jj721951.aspx).</span><span class="sxs-lookup"><span data-stu-id="58acd-179">toolearn how toocreate a SAS token, refer too[Create and Use a Shared Access Signature](https://msdn.microsoft.com/library/azure/jj721951.aspx).</span></span>

## <a name="recurrence"></a><span data-ttu-id="58acd-180">ricorrenza</span><span class="sxs-lookup"><span data-stu-id="58acd-180">recurrence</span></span>
<span data-ttu-id="58acd-181">La ricorrenza ha diverse parti:</span><span class="sxs-lookup"><span data-stu-id="58acd-181">Recurrence has several parts:</span></span>

* <span data-ttu-id="58acd-182">Frequenza: Un valore tra minuto, ora, giorno, settimana, mese, anno</span><span class="sxs-lookup"><span data-stu-id="58acd-182">Frequency: One of minute, hour, day, week, month, year</span></span>  
* <span data-ttu-id="58acd-183">Intervallo: Intervallo alla hello dato frequenza ricorrenza hello</span><span class="sxs-lookup"><span data-stu-id="58acd-183">Interval: Interval at hello given frequency for hello recurrence</span></span>  
* <span data-ttu-id="58acd-184">Pianificazione prescritta: specificare minuti, ore, giorni della settimana, mesi e giorni del mese hello ricorrenza</span><span class="sxs-lookup"><span data-stu-id="58acd-184">Prescribed schedule: Specify minutes, hours, weekdays, months, and monthdays of hello recurrence</span></span>  
* <span data-ttu-id="58acd-185">Conteggio: Conteggio delle occorrenze</span><span class="sxs-lookup"><span data-stu-id="58acd-185">Count: Count of occurrences</span></span>  
* <span data-ttu-id="58acd-186">Ora di fine: nessun processo verrà eseguito dopo hello specificato ora di fine</span><span class="sxs-lookup"><span data-stu-id="58acd-186">End time: No jobs will execute after hello specified end time</span></span>  

<span data-ttu-id="58acd-187">Un processo è ricorrente se dispone di un oggetto ricorrente specificato nella sua definizione JSON.</span><span class="sxs-lookup"><span data-stu-id="58acd-187">A job is recurring if it has a recurring object specified in its JSON definition.</span></span> <span data-ttu-id="58acd-188">Se vengono specificati sia count ed endTime, regola di completamento hello che si verifica per primo è rispettata.</span><span class="sxs-lookup"><span data-stu-id="58acd-188">If both count and endTime are specified, hello completion rule that occurs first is honored.</span></span>

## <a name="state"></a><span data-ttu-id="58acd-189">state</span><span class="sxs-lookup"><span data-stu-id="58acd-189">state</span></span>
<span data-ttu-id="58acd-190">lo stato di Hello di hello processo è uno dei quattro valori: abilitato, disabilitato, completed o faulted.</span><span class="sxs-lookup"><span data-stu-id="58acd-190">hello state of hello job is one of four values: enabled, disabled, completed, or faulted.</span></span> <span data-ttu-id="58acd-191">È possibile inserire o patch per i processi, come tooupdate li toohello abilitato o disabilitato lo stato.</span><span class="sxs-lookup"><span data-stu-id="58acd-191">You can PUT or PATCH jobs so as tooupdate them toohello enabled or disabled state.</span></span> <span data-ttu-id="58acd-192">Se un processo è stato completato o con errore, che è uno stato finale non può essere aggiornato (sebbene possa comunque eliminare il processo di hello).</span><span class="sxs-lookup"><span data-stu-id="58acd-192">If a job has been completed or faulted, that is a final state that cannot be updated (though hello job can still be DELETED).</span></span> <span data-ttu-id="58acd-193">Un esempio di proprietà state hello è come segue:</span><span class="sxs-lookup"><span data-stu-id="58acd-193">An example of hello state property is as follows:</span></span>

        "state": "disabled", // enabled, disabled, completed, or faulted
<span data-ttu-id="58acd-194">I processi completati e con errori vengono eliminati dopo 60 giorni.</span><span class="sxs-lookup"><span data-stu-id="58acd-194">Completed and faulted jobs are deleted after 60 days.</span></span>

## <a name="status"></a><span data-ttu-id="58acd-195">status</span><span class="sxs-lookup"><span data-stu-id="58acd-195">status</span></span>
<span data-ttu-id="58acd-196">Una volta avviato un processo dell'utilità di pianificazione, verranno restituite informazioni sullo stato corrente di hello del processo di hello.</span><span class="sxs-lookup"><span data-stu-id="58acd-196">Once a Scheduler job has started, information will be returned about hello current status of hello job.</span></span> <span data-ttu-id="58acd-197">Questo oggetto non può essere impostato dall'utente hello, viene impostato dal sistema hello.</span><span class="sxs-lookup"><span data-stu-id="58acd-197">This object is not settable by hello user—it’s set by hello system.</span></span> <span data-ttu-id="58acd-198">Tuttavia, è incluso in hello oggetto processo (anziché una risorsa collegata separata) in modo da consentire di ottenere facilmente stato hello di un processo.</span><span class="sxs-lookup"><span data-stu-id="58acd-198">However, it is included in hello job object (rather than a separate linked resource) so that one can obtain hello status of a job easily.</span></span>

<span data-ttu-id="58acd-199">Lo stato del processo include l'ora hello del hello precedente esecuzione (se presente), hello ora della successiva esecuzione pianificata hello (per i processi in corso) e il conteggio esecuzioni hello del processo di hello.</span><span class="sxs-lookup"><span data-stu-id="58acd-199">Job status includes hello time of hello previous execution (if any), hello time of hello next scheduled execution (for in-progress jobs), and hello execution count of hello job.</span></span>

## <a name="retrypolicy"></a><span data-ttu-id="58acd-200">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="58acd-200">retryPolicy</span></span>
<span data-ttu-id="58acd-201">Se un processo dell'utilità di pianificazione, è possibile toospecify un toodetermine di criteri di tentativi se e come azione di hello viene ripetuta.</span><span class="sxs-lookup"><span data-stu-id="58acd-201">If a Scheduler job fails, it is possible toospecify a retry policy toodetermine whether and how hello action is retried.</span></span> <span data-ttu-id="58acd-202">Ciò è determinato dal hello **retryType** oggetto, viene impostato troppo**Nessuno** se non è presente alcun criterio di ripetizione, come illustrato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="58acd-202">This is determined by hello **retryType** object—it is set too**none** if there is no retry policy, as shown above.</span></span> <span data-ttu-id="58acd-203">Impostarlo troppo**fissa** se è presente un criterio di ripetizione.</span><span class="sxs-lookup"><span data-stu-id="58acd-203">Set it too**fixed** if there is a retry policy.</span></span>

<span data-ttu-id="58acd-204">tooset un criterio di ripetizione, è possibile specificare due impostazioni aggiuntive: un intervallo tra tentativi (**retryInterval**) e il numero di tentativi di hello (**retryCount**).</span><span class="sxs-lookup"><span data-stu-id="58acd-204">tooset a retry policy, two additional settings may be specified: a retry interval (**retryInterval**) and hello number of retries (**retryCount**).</span></span>

<span data-ttu-id="58acd-205">intervallo tra tentativi Hello, specificato con hello **retryInterval** oggetto, hello intervallo tra tentativi.</span><span class="sxs-lookup"><span data-stu-id="58acd-205">hello retry interval, specified with hello **retryInterval** object, is hello interval between retries.</span></span> <span data-ttu-id="58acd-206">Il valore predefinito è 30 secondi, il valore minimo configurabile è 15 secondi e il valore massimo è 18 mesi.</span><span class="sxs-lookup"><span data-stu-id="58acd-206">Its default value is 30 seconds, its minimum configurable value is 15 seconds, and its maximum value is 18 months.</span></span> <span data-ttu-id="58acd-207">I processi inclusi nelle raccolte di processi del livello Gratuito hanno un valore minimo configurabile di 1 ora.</span><span class="sxs-lookup"><span data-stu-id="58acd-207">Jobs in Free job collections have a minimum configurable value of 1 hour.</span></span>  <span data-ttu-id="58acd-208">È definito in formato ISO 8601 hello.</span><span class="sxs-lookup"><span data-stu-id="58acd-208">It is defined in hello ISO 8601 format.</span></span> <span data-ttu-id="58acd-209">Analogamente, viene specificato il valore hello numero hello tentativi con hello **retryCount** ; dell'oggetto è hello numero di volte in cui viene eseguito un tentativo di un nuovo tentativo.</span><span class="sxs-lookup"><span data-stu-id="58acd-209">Similarly, hello value of hello number of retries is specified with hello **retryCount** object; it is hello number of times a retry is attempted.</span></span> <span data-ttu-id="58acd-210">Il valore predefinito è 4 e il valore massimo è 20\.</span><span class="sxs-lookup"><span data-stu-id="58acd-210">Its default value is 4, and its maximum value is 20\.</span></span> <span data-ttu-id="58acd-211">Entrambi **retryInterval** e **retryCount** sono facoltativi.</span><span class="sxs-lookup"><span data-stu-id="58acd-211">Both **retryInterval** and **retryCount** are optional.</span></span> <span data-ttu-id="58acd-212">Vengono loro assegnati valori predefiniti se **retryType** è troppo**fissa** e non sono specificati valori in modo esplicito.</span><span class="sxs-lookup"><span data-stu-id="58acd-212">They are given their default values if **retryType** is set too**fixed** and no values are specified explicitly.</span></span>

## <a name="see-also"></a><span data-ttu-id="58acd-213">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="58acd-213">See also</span></span>
 [<span data-ttu-id="58acd-214">Che cos'è l'Utilità di pianificazione?</span><span class="sxs-lookup"><span data-stu-id="58acd-214">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="58acd-215">Introduzione all'uso dell'utilità di pianificazione nel portale di Azure hello</span><span class="sxs-lookup"><span data-stu-id="58acd-215">Get started using Scheduler in hello Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="58acd-216">Piani e fatturazione nell'utilità di pianificazione di Azure</span><span class="sxs-lookup"><span data-stu-id="58acd-216">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="58acd-217">Come toobuild complesso pianifica e ricorrenza avanzata con utilità di pianificazione di Azure</span><span class="sxs-lookup"><span data-stu-id="58acd-217">How toobuild complex schedules and advanced recurrence with Azure Scheduler</span></span>](scheduler-advanced-complexity.md)

 [<span data-ttu-id="58acd-218">Informazioni di riferimento sull'API REST dell'Utilità di pianificazione di Azure</span><span class="sxs-lookup"><span data-stu-id="58acd-218">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="58acd-219">Informazioni di riferimento sui cmdlet PowerShell dell'Utilità di pianificazione di Azure</span><span class="sxs-lookup"><span data-stu-id="58acd-219">Azure Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="58acd-220">Livelli elevati di disponibilità e affidabilità dell'Utilità di pianificazione di Azure</span><span class="sxs-lookup"><span data-stu-id="58acd-220">Azure Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="58acd-221">Limiti, valori predefiniti e codici di errore dell'Utilità di pianificazione di Azure</span><span class="sxs-lookup"><span data-stu-id="58acd-221">Azure Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

 [<span data-ttu-id="58acd-222">Autenticazione in uscita dell'Utilità di pianificazione di Azure</span><span class="sxs-lookup"><span data-stu-id="58acd-222">Azure Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

