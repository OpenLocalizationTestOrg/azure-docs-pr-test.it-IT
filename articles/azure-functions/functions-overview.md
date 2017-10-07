---
title: Panoramica delle funzioni aaaAzure | Documenti Microsoft
description: Comprendere come toouse Azure funzioni toooptimize asincrone carichi di lavoro in minuti.
services: functions
documentationcenter: na
author: mattchenderson
manager: erikre
editor: 
tags: 
keywords: Funzioni di Azure, Funzioni, elaborazione eventi, webhook, calcolo dinamico, architettura senza server
ms.assetid: 01d6ca9f-ca3f-44fa-b0b9-7ffee115acd4
ms.service: functions
ms.devlang: multiple
ms.topic: overview
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 02/27/2017
ms.author: glenga
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: 668f9055a007fee662a4c7ec774d3c0a1d847800
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="an-introduction-tooazure-functions"></a>Le funzioni tooAzure un'introduzione  
Funzioni di Azure è una soluzione per l'esecuzione facilmente piccoli frammenti di codice, o "funzioni", nel cloud hello. È possibile scrivere solo il codice hello che è necessario per hello problema, senza preoccuparsi di un intero toorun di infrastruttura dell'applicazione o hello. Le funzioni possono rendere più produttiva l'attività di sviluppo e consentono di usare il linguaggio di sviluppo preferito, ad esempio C#, F#, Node.js, Python o PHP. Paga per ora hello che il codice viene eseguito e trust di Azure tooscale in base alle esigenze. Funzioni di Azure consente di sviluppare applicazioni senza server in Microsoft Azure.

Questo argomento offre una panoramica generale di Funzioni di Azure. Se si desidera toojump destra e iniziare a utilizzare le funzioni di Azure, iniziare con [creare la prima funzione Azure](functions-create-first-azure-function.md). Se si cercano informazioni più tecniche sulle funzioni, vedere hello [di riferimento per sviluppatori](functions-reference.md).

## <a name="features"></a>Funzionalità
Ecco alcune delle principali funzionalità di Funzioni di Azure:

* **Scelta del linguaggio**: è possibile scrivere funzioni con C#, F#, Node.js, Python, PHP, batch, bash o qualsiasi eseguibile.
* **Pagamento in base all'utilizzo del modello di costo** : paga solo per hello tempo impiegato per l'esecuzione del codice. Vedere hello consumo hosting piano opzione hello [prezzi sezione](#pricing).  
* **Trasferimento delle dipendenze** : Funzioni supporta NuGet e NPM, quindi è possibile usare le librerie preferite.  
* **Sicurezza integrata** : è possibile proteggere le funzioni attivate da HTTP con provider OAuth, ad esempio Azure Active Directory, Facebook, Google, Twitter e account Microsoft.  
* **Integrazione semplificata** : è possibile sfruttare facilmente i servizi di Azure e le offerte di software come un servizio (SaaS). Vedere hello [sezione integrazioni](#integrations) per alcuni esempi.  
* **Sviluppo flessibile** : il diritto di funzioni nel portale di hello del codice o configurare l'integrazione continua e distribuire il codice tramite GitHub, Visual Studio Team Services e altri [supportati gli strumenti di sviluppo](../app-service-web/web-sites-deploy.md#deploy-using-an-ide).  
* **Open source** -runtime funzioni hello è open source e [disponibile in GitHub](https://github.com/azure/azure-webjobs-sdk-script).  

## <a name="what-can-i-do-with-functions"></a>Quali operazioni si possono eseguire con Funzioni?
Funzioni di Azure è un'ottima soluzione per l'elaborazione dei dati, l'integrazione di sistemi, l'utilizzo di hello internet delle cose (IoT) e la creazione di API semplice e microservizi. Considerare le funzioni per attività come immagine o l'elaborazione degli ordini, manutenzione di file o per tutte le attività che si desidera toorun in una pianificazione. 

Funzioni fornisce modelli tooget è stato avviato con gli scenari principali, inclusi hello seguenti:

* **BlobTrigger** -processo di archiviazione di Azure quando vengono aggiunte toocontainers i BLOB. Questa funzione può essere usata per il ridimensionamento delle immagini.
* **EventHubTrigger** -rispondere tooevents recapitati tooan Hub di eventi di Azure. È particolarmente utile negli scenari di strumentazione delle applicazioni, elaborazione dei flussi di lavoro o dell'esperienza utente e di Internet delle cose (IoT).
* **Webhook generico** : elabora le richieste HTTP di webhook da qualsiasi servizio che supporti webhook.
* **GitHub webhook** -tooevents risponde che si verificano nei repository GitHub. Per un esempio, vedere [Creare un webhook o una funzione API](functions-create-a-web-hook-or-api-function.md).
* **HTTPTrigger** -attivare l'esecuzione di hello del codice tramite una richiesta HTTP.
* **QueueTrigger** -rispondere toomessages appena arrivano in una coda di archiviazione di Azure. Per un esempio, vedere [creare una funzione di Azure che associa il servizio di Azure tooan](functions-create-an-azure-connected-function.md).
* **ServiceBusQueueTrigger** -tooother il codice dei servizi Azure o servizi locali dalle code toomessage in attesa di connessione. 
* **ServiceBusTopicTrigger** -tooother il codice dei servizi Azure o servizi locali sottoscrivendo tootopics connettersi. 
* **TimerTrigger** : esegue attività di pulizia o altre attività batch secondo una pianificazione predefinita. Per un esempio, vedere [Creare una funzione di Azure di elaborazione di eventi](functions-create-an-event-processing-function.md).

Azure supporta funzioni *trigger*, che sono i modi toostart esecuzione del codice, e *associazioni*, che sono toosimplify modi di codifica per i dati di input e outpui. Per una descrizione dettagliata di trigger hello e associazioni che fornisce funzioni di Azure, vedere [riferimenti per sviluppatori trigger e le associazioni di funzioni di Azure](functions-triggers-bindings.md).

## <a name="integrations"></a>Integrazioni
Funzioni di Azure si integra con un'ampia gamma di servizi di Azure e di terze parti. Questi servizi consentono di attivare la funzione e avviare l'esecuzione o possono essere usati come input e output per il codice. Hello seguenti integrazioni servizio è supportato dalle funzioni di Azure. 

* Azure Cosmos DB
* Hub eventi di Azure 
* App per dispositivi mobili di Azure (tabelle)
* Hub di notifica di Azure
* Bus di servizio di Azure (code e argomenti)
* Archiviazione di Azure (BLOB, code e tabelle) 
* GitHub (webhook)
* Locale (tramite il bus di servizio)
* Twilio (SMS)

## <a name="pricing"></a>Quanto costa Funzioni?
Funzioni di Azure contiene due tipi di piani tariffari, hello di sceglierne uno che meglio si adatta alle esigenze: 

* **Piano di consumo** : se la funzione viene eseguita, Azure fornisce tutte le risorse di calcolo necessarie hello. Non è tooworry sulla gestione delle risorse e si paga solo per volta hello che il codice viene eseguito. 
* **Piano di Servizio app** : consente di eseguire le funzioni esattamente come le app Web, per dispositivi mobili e per le API. Quando si utilizza già servizio App per le altre applicazioni, è possibile eseguire le funzioni in hello stesso piano senza alcun costo aggiuntivo. 

Informazioni sui prezzi complete sono disponibili in hello [pagina prezzi funzioni](https://azure.microsoft.com/pricing/details/functions/). Per ulteriori informazioni sulla scalabilità delle funzioni, vedere [come tooscale Azure funzioni](functions-scale.md).

## <a name="next-steps"></a>Passaggi successivi
* [Creare la prima funzione di Azure](functions-create-first-azure-function.md)  
  Passare subito e creare una funzione primo utilizzo dell'avvio rapido di Azure funzioni hello. 
* [Guida di riferimento per gli sviluppatori di Funzioni di Azure](functions-reference.md)  
  Fornisce altre informazioni tecniche sul runtime di Azure funzioni hello e un riferimento per le funzioni di codifica e la definizione di trigger e le associazioni.
* [Test di Funzioni di Azure](functions-test-a-function.md)  
  Descrive diversi strumenti e tecniche per il test delle funzioni.
* [Come tooscale funzioni di Azure](functions-scale.md)  
  Vengono descritti i piani di servizio disponibili con le funzioni di Azure, piano di hosting consumo hello e come toochoose hello giusta. 
* [Informazioni sul servizio app di Azure](../app-service/app-service-value-prop-what-is.md)  
  Funzioni di Azure si avvale della piattaforma Azure App Service hello per le funzionalità di base come le distribuzioni, le variabili di ambiente e diagnostica. 

