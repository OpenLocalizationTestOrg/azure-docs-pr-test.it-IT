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
# <a name="scheduler-concepts-terminology--entity-hierarchy"></a>Concetti, terminologia e gerarchia di entità dell'Utilità di pianificazione
## <a name="scheduler-entity-hierarchy"></a>Gerarchia di entità dell'Utilità di pianificazione
Hello nella tabella seguente descrive hello risorse principali esposte o usate dall'API dell'utilità di pianificazione hello:

| Risorsa | Descrizione |
| --- | --- |
| **Raccolta di processi** |Una raccolta di processi contiene un gruppo di processi e gestisce le impostazioni, le quote e le limitazioni condivise dai processi all'interno di raccolta hello. Le raccolte di processi vengono create dal proprietario della sottoscrizione e raggruppano i processi in base ai limiti di utilizzo o dell'applicazione. È vincolata tooone area. Consente inoltre l'applicazione hello di quote di utilizzo hello tooconstrain di tutti i processi in tale raccolta. le quote di Hello includono MaxJobs e MaxRecurrence. |
| **Processo** |Un processo definisce una singola azione ricorrente, con strategie semplici o complesse per l'esecuzione. Le azioni possono includere HTTP, coda di archiviazione, coda del bus di servizio o richieste di argomento del bus di servizio. |
| **Cronologia processi** |Una cronologia processi rappresenta i dettagli per l'esecuzione di un processo. Contiene esito positivo o negativo, nonché i dettagli della risposta. |

## <a name="scheduler-entity-management"></a>Gestione di entità dell'utilità di pianificazione
In generale, utilità di pianificazione di hello e API di Gestione servizio hello esporre hello dopo le operazioni sulle risorse hello:

| Funzionalità | Descrizione e indirizzo URI |
| --- | --- |
| **Gestione delle raccolte di processi** |GET, PUT, supporto e DELETE per la creazione e modifica di raccolte di processi e i processi di hello in esso contenuti. Una raccolta di processi è un contenitore per i processi e viene eseguito il mapping tooquotas e le impostazioni condivise. Esempi di quote, descritti più avanti, sono il numero massimo di processi e l'intervallo minimo delle ricorrenze. <p>PUT e DELETE: `https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</p><p>GET: `https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</p> |
| **Gestione dei processi** |Supporto di GET, PUT, POST, PATCH e DELETE per la creazione e modifica di processi. Tutti i processi devono appartenere tooa raccolta di processi che esiste già, pertanto non c'è alcuna creazione implicita. <p>`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}/jobs/{jobName}`</p> |
| **Gestione della cronologia dei processi** |Supporto GET per il recupero di 60 giorni di cronologia di esecuzioni del processo, ad esempio il tempo di esecuzione del processo e i risultati dell'esecuzione del processo. Aggiunge il supporto del parametro della stringa di query per filtrare in base a stato e status. <P>`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}/jobs/{jobName}/history`</p> |

## <a name="job-types"></a>Tipi di processo
Sono disponibili più tipi di processi: processi HTTP, inclusi quelli che supportano SSL, processi della coda di archiviazione, processi della coda del bus di servizio e processi dell'argomento del bus di servizio. I processi HTTP sono ideali se si dispone di un endpoint di un carico di lavoro o di un servizio esistente. È possibile utilizzare coda processi toopost messaggi toostorage code di archiviazione, pertanto questi processi sono ideali per i carichi di lavoro che usano code di archiviazione. Analogamente, i processi del bus di servizio sono ideali per carichi di lavoro che usano argomenti e code del bus di servizio.

## <a name="hello-job-entity-in-detail"></a>entità "processo" Hello in dettaglio
A livello di base, un processo pianificato ha diverse parti:

* Hello tooperform azione quando il timer di processo hello  
* Processo di hello toorun ora hello (facoltativo)  
* (Facoltativo) Quando e con quale frequenza processo hello toorepeat  
* (Facoltativo) Toofire un'azione se hello primario azione ha esito negativo  

Internamente, un processo pianificato contiene inoltre dati forniti dal sistema, ad esempio il tempo di esecuzione di hello successivo pianificato.

Hello di codice seguente fornisce un esempio completo di un processo pianificato. I dettagli vengono forniti nelle sezioni a seguire.

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

Come osservato nel hello esempio processo pianificato precedente, definizione di un processo è costituito da parti diverse:

* Ora di inizio ("startTime")  
* Azione ("action"), che include l'azione in caso di errore ("errorAction")
* Ricorrenza ("recurrence")  
* Stato (“state”)  
* Status (“status”)  
* Criterio di ripetizione (“retryPolicy”)  

Esaminiamo ciascuna in modo dettagliato:

## <a name="starttime"></a>startTime
Hello "startTime" è l'ora di inizio hello e consente di hello chiamante toospecify un fuso orario offset durante la trasmissione hello in [formato ISO 8601](http://en.wikipedia.org/wiki/ISO_8601).

## <a name="action-and-erroraction"></a>action ed errorAction
azione"Hello" hello azione richiamata a ogni occorrenza e descrive un tipo di chiamata del servizio. azione di Hello è ciò che verrà eseguito su hello fornito pianificazione. L'Utilità di pianificazione supporta azioni della coda del bus di servizio, dell'argomento del bus di servizio, della coda di archiviazione e HTTP.

azione di Hello nell'esempio hello precedente è un'azione HTTP. Di seguito è riportato un esempio di un'azione in coda di archiviazione:

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

Di seguito è riportato un esempio di azione dell'argomento del bus di servizio.

  "action": { "type": "serviceBusTopic", "serviceBusTopicMessage": { "topicPath": "t1",  
      "namespace": "mySBNamespace", "transportType": "netMessaging", // Can be either netMessaging or AMQP "authentication": { "sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Some message", "brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, }

Di seguito è riportato un esempio di azione di coda del bus di servizio.

  "action": { "serviceBusQueueMessage": { "queueName": "q1",  
      "namespace": "mySBNamespace", "transportType": "netMessaging", // Can be either netMessaging or AMQP "authentication": {  
        "sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Some message",  
      "brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, "type": "serviceBusQueue" }

Hello "errorAction" è del gestore degli errori di hello azione hello viene richiamato quando l'azione principale hello ha esito negativo. È possibile utilizzare questa variabile toocall un endpoint di gestione degli errori o inviare una notifica all'utente. Può essere utilizzato per raggiungere un endpoint secondario in caso di hello che hello primario non è disponibile (ad esempio, in caso di hello un'emergenza nel sito dell'endpoint hello) o può essere utilizzato per la notifica di un endpoint di gestione degli errori. Come azione principale hello, azione di errore hello può essere semplice o composta logica in base ad altre azioni. toolearn come toocreate un token di firma di accesso condiviso, fare riferimento troppo[creare e usare una firma di accesso condiviso](https://msdn.microsoft.com/library/azure/jj721951.aspx).

## <a name="recurrence"></a>ricorrenza
La ricorrenza ha diverse parti:

* Frequenza: Un valore tra minuto, ora, giorno, settimana, mese, anno  
* Intervallo: Intervallo alla hello dato frequenza ricorrenza hello  
* Pianificazione prescritta: specificare minuti, ore, giorni della settimana, mesi e giorni del mese hello ricorrenza  
* Conteggio: Conteggio delle occorrenze  
* Ora di fine: nessun processo verrà eseguito dopo hello specificato ora di fine  

Un processo è ricorrente se dispone di un oggetto ricorrente specificato nella sua definizione JSON. Se vengono specificati sia count ed endTime, regola di completamento hello che si verifica per primo è rispettata.

## <a name="state"></a>state
lo stato di Hello di hello processo è uno dei quattro valori: abilitato, disabilitato, completed o faulted. È possibile inserire o patch per i processi, come tooupdate li toohello abilitato o disabilitato lo stato. Se un processo è stato completato o con errore, che è uno stato finale non può essere aggiornato (sebbene possa comunque eliminare il processo di hello). Un esempio di proprietà state hello è come segue:

        "state": "disabled", // enabled, disabled, completed, or faulted
I processi completati e con errori vengono eliminati dopo 60 giorni.

## <a name="status"></a>status
Una volta avviato un processo dell'utilità di pianificazione, verranno restituite informazioni sullo stato corrente di hello del processo di hello. Questo oggetto non può essere impostato dall'utente hello, viene impostato dal sistema hello. Tuttavia, è incluso in hello oggetto processo (anziché una risorsa collegata separata) in modo da consentire di ottenere facilmente stato hello di un processo.

Lo stato del processo include l'ora hello del hello precedente esecuzione (se presente), hello ora della successiva esecuzione pianificata hello (per i processi in corso) e il conteggio esecuzioni hello del processo di hello.

## <a name="retrypolicy"></a>retryPolicy
Se un processo dell'utilità di pianificazione, è possibile toospecify un toodetermine di criteri di tentativi se e come azione di hello viene ripetuta. Ciò è determinato dal hello **retryType** oggetto, viene impostato troppo**Nessuno** se non è presente alcun criterio di ripetizione, come illustrato in precedenza. Impostarlo troppo**fissa** se è presente un criterio di ripetizione.

tooset un criterio di ripetizione, è possibile specificare due impostazioni aggiuntive: un intervallo tra tentativi (**retryInterval**) e il numero di tentativi di hello (**retryCount**).

intervallo tra tentativi Hello, specificato con hello **retryInterval** oggetto, hello intervallo tra tentativi. Il valore predefinito è 30 secondi, il valore minimo configurabile è 15 secondi e il valore massimo è 18 mesi. I processi inclusi nelle raccolte di processi del livello Gratuito hanno un valore minimo configurabile di 1 ora.  È definito in formato ISO 8601 hello. Analogamente, viene specificato il valore hello numero hello tentativi con hello **retryCount** ; dell'oggetto è hello numero di volte in cui viene eseguito un tentativo di un nuovo tentativo. Il valore predefinito è 4 e il valore massimo è 20\. Entrambi **retryInterval** e **retryCount** sono facoltativi. Vengono loro assegnati valori predefiniti se **retryType** è troppo**fissa** e non sono specificati valori in modo esplicito.

## <a name="see-also"></a>Vedere anche
 [Che cos'è l'Utilità di pianificazione?](scheduler-intro.md)

 [Introduzione all'uso dell'utilità di pianificazione nel portale di Azure hello](scheduler-get-started-portal.md)

 [Piani e fatturazione nell'utilità di pianificazione di Azure](scheduler-plans-billing.md)

 [Come toobuild complesso pianifica e ricorrenza avanzata con utilità di pianificazione di Azure](scheduler-advanced-complexity.md)

 [Informazioni di riferimento sull'API REST dell'Utilità di pianificazione di Azure](https://msdn.microsoft.com/library/mt629143)

 [Informazioni di riferimento sui cmdlet PowerShell dell'Utilità di pianificazione di Azure](scheduler-powershell-reference.md)

 [Livelli elevati di disponibilità e affidabilità dell'Utilità di pianificazione di Azure](scheduler-high-availability-reliability.md)

 [Limiti, valori predefiniti e codici di errore dell'Utilità di pianificazione di Azure](scheduler-limits-defaults-errors.md)

 [Autenticazione in uscita dell'Utilità di pianificazione di Azure](scheduler-outbound-authentication.md)

