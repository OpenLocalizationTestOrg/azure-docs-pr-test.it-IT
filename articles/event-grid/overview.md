---
title: Cenni preliminari sulla griglia di eventi aaaAzure
description: Vengono descritti il servizio Griglia di eventi di Azure e i concetti correlati.
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/18/2017
ms.author: babanisa
ms.openlocfilehash: 95dce22e9335df88e81b134143a6c14994c26b8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="an-introduction-tooazure-event-grid"></a>Un tooAzure introduzione della griglia di eventi

Griglia di eventi Azure consente tooeasily creare applicazioni con le architetture basato su eventi. Selezionare le risorse di Azure desideri toosubscribe per e assegnare il gestore di eventi hello o WebHook endpoint toosend hello evento hello. Griglia di eventi offre il supporto predefinito per gli eventi generati dai servizi di Azure, ad esempio BLOB di archiviazione e gruppi di risorse. Griglia di eventi offre anche il supporto personalizzato per gli eventi dell'applicazione e di terze parti, tramite argomenti personalizzati e webhook personalizzati. 

È possibile utilizzare i filtri tooroute eventi specifici toodifferent endpoint, endpoint multicast toomultiple e assicurarsi che gli eventi vengono recapitati in modo affidabile. Griglia di eventi offre anche il supporto predefinito per eventi personalizzati e di terze parti.

Per la versione di anteprima hello griglia eventi supporta **westus2** e **westcentralus** percorsi. Verranno aggiunte altre aree.

Questo articolo offre una panoramica di Griglia di eventi di Azure. Se si desidera tooget avviato con la griglia di eventi, vedere [route e creare eventi personalizzati con griglia di eventi di Azure](custom-event-quickstart.md).

![Modello funzionale di Griglia di eventi](./media/overview/event-grid-functional-model.png)

Archiviazione Blob non è attualmente disponibile pubblicamente come server di pubblicazione.

## <a name="concepts"></a>Concetti

Per iniziare, è opportuno tenere presenti cinque concetti relativi a Griglia di eventi di Azure:

* **Eventi**: ciò che successo.
* **Origini evento/server di pubblicazione** - evento hello ha avuto luogo.
* **Argomenti** -hello endpoint in cui i server di pubblicazione invia eventi.
* **Le sottoscrizioni di eventi** -hello eventi tooroute meccanismo endpoint o incorporato, talvolta toomultiple gestori. Le sottoscrizioni vengono inoltre utilizzate dagli eventi in ingresso di gestori toointelligently filtro.
* **I gestori eventi** : hello app o reazione toohello eventi del servizio.

Per altre informazioni su questi concetti, vedere [Concepts in Azure Event Grid](concepts.md) (Concetti relativi a Griglia di eventi di Azure).

## <a name="capabilities"></a>Capabilities

Ecco alcune delle funzionalità chiave di hello di griglia di eventi di Azure:

* **Semplicità** -punto e fare clic su eventi tooaim dal gestore dell'evento tooany risorse di Azure o endpoint.
* **Filtro avanzato** -filtro evento di tipo o un evento pubblicare tooensure percorso gestori di ricezione solo eventi rilevanti.
* **Fan-out** -sottoscrizione più endpoint toohello stesso evento toosend copie di hello evento tooas numerose posizioni in base alle esigenze.
* **Affidabilità** -utilizzare 24 ore tentativi con backoff esponenziale tooensure gli eventi vengono recapitati.
* **Per ogni evento di retribuzione** : paga solo per quantità hello è possibile utilizzare la griglia evento.
* **Velocità effettiva elevata**: consente di creare carichi di lavoro con volumi elevati in Griglia di eventi con il supporto per milioni di eventi al secondo.
* **Eventi predefiniti**: consentono di essere operativi rapidamente con gli eventi predefiniti a livello di risorse.
* **Eventi personalizzati**: consentono di usare la route di Griglia di eventi, di filtrare e recapitare in modo affidabile gli eventi personalizzati nell'app.

## <a name="built-in-publisher-and-handler-integration"></a>Integrazione predefinita di gestori e autori

Azure offre il supporto per gli eventi predefiniti grazie a numerosi servizi, inclusi autori e gestori.

### <a name="publishers"></a>Autori

Hello servizi di Azure seguenti sono attualmente supporto dell'autore incorporati per la griglia di eventi:

* Gruppi di risorse (operazioni di gestione)
* Sottoscrizioni di Azure (operazioni di gestione)
* Hub eventi
* Argomenti personalizzati

Quest'anno verranno aggiunti altri servizi di Azure.

### <a name="handlers"></a>Gestori

Hello servizi di Azure seguenti sono attualmente supporto per i gestori predefiniti per la griglia di eventi: 

* Funzioni di Azure
* App per la logica
* Automazione di Azure
* Webhook

Quest'anno verranno aggiunti altri servizi di Azure.

## <a name="what-can-i-do-with-event-grid"></a>Quali operazioni si possono eseguire con Griglia di eventi?

Griglia di eventi di Azure offre diverse funzionalità che migliorano considerevolmente le attività senza server, di automazione delle operazioni e di integrazione: 

### <a name="serverless-application-architectures"></a>Architetture di applicazioni senza server

![Applicazione senza server](./media/overview/serverless_web_app.png)

Griglia di eventi connette le origini dati e i gestori di eventi. Ad esempio, utilizzare trigger di evento griglia tooinstantly un'analisi delle immagini toorun senza funzione ogni volta che è una foto di nuovo aggiunto tooa contenitore di archiviazione blob. 

### <a name="ops-automation"></a>Automazione delle operazioni

![Automazione delle operazioni](./media/overview/Ops_automation.png)

Griglia di eventi consente di automazione toospeed e semplificare l'applicazione dei criteri. Griglia di eventi, ad esempio, può notificare ad Automazione di Azure quando una macchina virtuale viene creata o un database SQL viene attivato. Questi eventi possono essere usati tooautomatically verificare che le configurazioni del servizio sono conformi, inserire i metadati in strumenti di operazioni, le macchine virtuali di tag o gli elementi di lavoro di file.

### <a name="application-integration"></a>Integrazione di applicazioni

![Integrazione di applicazioni](./media/overview/app_integration.png)

Griglia di eventi connette l'app con altri servizi. Ad esempio, creare toosend un argomento personalizzato tooEvent dati di evento dell'app griglia e sfruttare il recapito affidabile, avanzato, routing e integrazione diretta con Azure. In alternativa, è possibile utilizzare la griglia di eventi con i dati in un punto qualsiasi, di App per la logica tooprocess senza scrivere codice. 

## <a name="how-is-event-grid-different-from-other-azure-integration-services"></a>Differenze tra Griglia di eventi e gli altri servizi di integrazione di Azure

Griglia di eventi è un backplane eventi che abilita la programmazione reattiva basata su eventi. È strettamente integrato con i servizi di Azure e può essere integrato con i servizi di terze parti. messaggio evento contiene informazioni hello necessarie toochanges tooreact nei servizi e applicazioni. Griglia di eventi non è una pipeline di dati e il recapito non hello effettivo oggetto che è stato aggiornato.

Il bus di servizio è adatto alle tradizionali applicazioni aziendali che richiedono transazioni, ordinamento, rilevamento duplicati e coerenza immediata. Griglia di eventi è progettato per la velocità, la scalabilità, la varietà e il costo contenuto in un modello reattivo. È particolarmente adatta tooserverless architettura.

Griglia di eventi è complementare agli altri servizi di Azure, ad esempio App per la logica e Hub eventi. I trigger di evento griglia hello logica app toobegin relativo flusso di lavoro. Hub eventi funziona con griglia eventi consentendo tooevents tooreact da acquisire gli hub di eventi e pipeline in ingresso e la trasformazione di dati compilazione.

## <a name="how-much-does-event-grid-cost"></a>Costi di Griglia di eventi

Griglia di eventi di Azure usa un modello di determinazione prezzi basato sul pagamento per evento, quindi si paga solo per le risorse usate.

Griglia eventi costa $0.60 per milione di operazioni ($0,30 durante l'anteprima) e hello 100.000 prima operazione al mese sono gratuiti. Le operazioni vengono definite come inserimento di eventi, corrispondenza avanzata, tentativo di recapito e chiamate di gestione.  Sono disponibili ulteriori dettagli su hello [pagina dei prezzi](https://azure.microsoft.com/pricing/details/event-grid/).

## <a name="next-steps"></a>Passaggi successivi

* [Creare ed eseguire la sottoscrizione degli eventi toocustom](custom-event-quickstart.md) subito e iniziare a inviare il proprio endpoint tooany eventi personalizzati utilizzando hello Guida introduttiva di griglia di eventi di Azure.
* [Utilizzando la logica App come un gestore eventi](monitor-virtual-machine-changes-event-grid-logic-app.md) un'esercitazione sulla creazione di un'app usando l'App per la logica tooreact tooevents inserito dalla griglia di eventi.
* [Event Grid REST API reference (Informazioni di riferimento sulle API REST di Griglia di eventi)](/rest/api/eventgrid)  
  Fornisce informazioni più tecniche hello griglia di eventi di Azure e un riferimento per la gestione di sottoscrizioni di eventi, routing e il filtraggio.
