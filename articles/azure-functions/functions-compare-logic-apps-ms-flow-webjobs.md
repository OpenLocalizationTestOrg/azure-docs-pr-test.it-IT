---
title: aaaChoose tra flusso, la logica App, funzioni e processi Web | Documenti Microsoft
description: Confronto e contrasto hello per i servizi di integrazione cloud da Microsoft e decidere quali servizi si consiglia di utilizzare.
services: functions,app-service\logic
documentationcenter: na
author: cephalin
manager: wpickett
tags: 
keywords: microsoft flow, flow, app per la logica, funzioni di azure, funzioni, processi web di azure, processi web, elaborazione di eventi, calcolo dinamico, architettura senza server
ms.assetid: e9ccf7ad-efc4-41af-b9d3-584957b1515d
ms.service: functions
ms.devlang: multiple
ms.topic: overview
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 08/03/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 6becc1e389698e517924b18295dac4375542d524
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="choose-between-flow-logic-apps-functions-and-webjobs"></a>Scegliere tra Flow, App per la logica, Funzioni e Processi Web
In questo articolo vengono confrontati i seguenti servizi in cloud di Microsoft hello, che possono tutti risolvere i problemi di integrazione e automazione dei processi di business hello:

* [Microsoft Flow](https://flow.microsoft.com/)
* [App per la logica di Azure](https://azure.microsoft.com/services/logic-apps/)
* [Funzioni di Azure](https://azure.microsoft.com/services/functions/)
* [Processi Web del servizio app di Azure](../app-service-web/web-sites-create-web-jobs.md)

Tutti questi servizi risultano utili quando si "mettono insieme" sistemi diversi. Possono definire input, azioni, condizioni e output e ognuno può essere eseguito in base a una pianificazione o un trigger. Tuttavia, ogni servizio aggiunge un set univoco di valore e il confronto non è una domanda "quale servizio è migliore hello?" ma qual è il servizio più adatto per una determinata situazione. Spesso, una combinazione di questi servizi è migliore hello toorapidly compilare una soluzione di integrazione in primo piano completo, scalabile.

<a name="flow"></a>

## <a name="flow-vs-logic-apps"></a>Flow rispetto ad App per la logica
È possibile discutere Microsoft Flow e App di Azure logica insieme perché entrambi sono *configurazione-first* integration services che rende facile toobuild processi e flussi di lavoro e l'integrazione con vari SaaS ed enterprise applicazioni. 

* Flow si basa sulle app per la logica
* Hanno hello stessa finestra di progettazione del flusso di lavoro
* [Connettori](../connectors/apis-list.md) che il lavoro in una possibile funziona anche in altri hello

Flussi consente a qualsiasi integrazioni di office worker tooperform semplice (ad esempio ottenere SMS per messaggi di posta elettronica importanti) senza passare per gli sviluppatori o IT. In hello invece, la logica App possibile abilitare avanzate o cruciali integrazioni (ad esempio processi B2B) in cui sono necessarie procedure di DevOps e sicurezza a livello aziendale. È tipico per un toogrow del flusso di lavoro di business in straordinario complessità. Di conseguenza, è possibile iniziare con un flusso inizialmente, quindi convertirlo tooa logica app in base alle esigenze.

Hello nella tabella seguente consente di determinare se è migliore per l'integrazione di una determinato flusso o App per la logica.

|  | Flusso | App per la logica |
| --- | --- | --- |
| Destinatari |Impiegati, utenti aziendali |Professionisti IT, sviluppatori |
| Scenari |Self-service |Cruciale |
| Strumento di progettazione |Nel browser e app per dispositivi mobili, solo interfaccia utente |Nel browser e in [Visual Studio](../logic-apps/logic-apps-deploy-from-vs.md) è disponibile la [visualizzazione Codice](../logic-apps/logic-apps-author-definitions.md) |
| DevOps |Ad hoc, sviluppo nell'ambiente di produzione |Controllo del codice sorgente, test, supporto, oltre ad automazione e gestibilità in [Azure Resource Manager](../logic-apps/logic-apps-arm-provision.md) |
| Esperienza di amministrazione |[https://flow.microsoft.com](https://flow.microsoft.com) |[https://portal.azure.com](https://portal.azure.com) |
| Sicurezza |Procedure standard: [sovranità dei dati](https://wikipedia.org/wiki/Technological_Sovereignty), [crittografia dati inattivi](https://wikipedia.org/wiki/Data_at_rest#Encryption) per i dati sensibili e così via. |Garanzie di sicurezza di Azure: [Sicurezza di Azure](https://www.microsoft.com/trustcenter/Security/AzureSecurity), [Centro sicurezza](https://azure.microsoft.com/services/security-center/), [log di controllo](https://azure.microsoft.com/blog/azure-audit-logs-ux-refresh/) e altro. |

<a name="function"></a>

## <a name="functions-vs-webjobs"></a>Funzioni e WebJobs
Funzioni di Azure e Processi Web del servizio app di Azure possono essere esaminati insieme, essendo entrambi servizi di integrazione di tipo *code first* e progettati per gli sviluppatori. Consentono di toorun script o parte di codice negli eventi toovarious risposta, ad esempio [nuovi BLOB di archiviazione](functions-bindings-storage.md) o [una richiesta di WebHook](functions-bindings-http-webhook.md). Ecco le analogie: 

* Entrambi si basano sul [Servizio app di Azure](../app-service/app-service-value-prop-what-is.md) e usano funzionalità come [controllo del codice sorgente](../app-service-web/app-service-continuous-deployment.md), [autenticazione](../app-service/app-service-authentication-overview.md), e [monitoraggio](../app-service-web/web-sites-monitor.md).
* Sono entrambi servizi rivolti agli sviluppatori.
* Supportano entrambi linguaggi di scripting e programmazione standard.
* Per entrambi è disponibile il supporto di NuGet e NPM.

Funzioni è hello naturale evoluzione processi Web accetta migliore hello su processi Web e li rappresenta un miglioramento. Hello i miglioramenti includono: 

* Sviluppo semplificato, testare ed eseguire del codice direttamente nel browser hello.
* Integrazione predefinita con più servizi di Azure e di terze parti come i [webhook GitHub](https://developer.github.com/webhooks/creating/).
* Pagamento in base all'utilizzo, toopay non necessario per un [piano di servizio App](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).
* [Ridimensionamento dinamico](functions-scale.md)automatico.
* Per i clienti esistenti del servizio App, in esecuzione nel piano di servizio App comunque (tootake sfruttare le risorse sottoutilizzate).
* Integrazione con App per la logica.

Hello nella tabella seguente vengono riepilogate le differenze di hello tra funzioni e processi Web:

|  | Funzioni | WebJobs |
| --- | --- | --- |
| Ridimensionamento |Ridimensionamento senza configurazione |Ridimensionamento con il piano di servizio app |
| Prezzi |Pagamento a consumo o parte del piano di servizio app |Parte del piano di servizio app |
| Tipo di esecuzione |Attivata, pianificata (da trigger timer) |Attivata, continua, pianificata |
| Eventi di attivazione |[Timer](functions-bindings-timer.md), [Azure Cosmos DB](functions-bindings-documentdb.md), [Hub eventi di Azure](functions-bindings-event-hubs.md), [HTTP/webhook (GitHub, Slack)](functions-bindings-http-webhook.md), [App per dispositivi mobili del Servizio app di Azure](functions-bindings-mobile-apps.md), [Hub di notifica di Azure](functions-bindings-notification-hubs.md), [Bus di servizio di Azure](functions-bindings-service-bus.md), [Archiviazione di Azure](functions-bindings-storage.md) |[Archiviazione di Azure](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md), [Bus di servizio di Azure](../app-service-web/websites-dotnet-webjobs-sdk-service-bus.md) |
| Sviluppo nel browser |supportato | non supportato |
| Windows Scripting |sperimentale |supportato |
| PowerShell |sperimentale |supportato |
| C# |supportato |supportato |
| F# |supportato |non supportato |
| Bash |sperimentale |supportato |
| PHP |sperimentale |supportato |
| Python |sperimentale |supportato |
| JavaScript |supportato |supportato |

Se le funzioni toouse o processi Web dipende in definitiva operazioni già eseguite con il servizio App. Se si dispone di un'applicazione di servizio App di cui si desidera toorun frammenti di codice, e si desidera toomanage li riuniti in hello stesso DevOps ambiente, è necessario utilizzare i processi Web. Se si desidera toorun frammenti di codice per altri servizi di Azure o anche a 3rd party App, o se si desidera gestire troppo i frammenti di codice di integrazione di applicazioni di servizio App o se si desidera toocall i frammenti di codice da un'app di logica, è necessario trarre vantaggio da tutti miglioramenti di Hello nelle funzioni.  

<a name="together"></a>

## <a name="flow-logic-apps-and-functions-together"></a>Flow, App per la logica e Funzioni insieme
Come accennato in precedenza, il servizio è più adatta tooyou dipende dalla situazione. 

* Per la semplice ottimizzazione aziendale, usare Flow.
* Se lo scenario di integrazione è troppo avanzato per Flow o sono necessarie le funzionalità di DevOps e la conformità ai requisiti di sicurezza, usare App per la logica.
* Se un passaggio nello scenario di integrazione richiede codice specializzato o di trasformazione altamente personalizzato, scrivere un'app per le funzioni e quindi attivare una funzione come azione nell'app per la logica.

È possibile chiamare un'app per la logica in un flusso. Si può anche chiamare una funzione in un'app per la logica e un'app per la logica in una funzione. integrazione di Hello tra flusso di App per la logica e le funzioni continuare tooimprove straordinario. È possibile generare un oggetto in un servizio e utilizzarlo in hello altri servizi. Qualsiasi investimento effettuato in queste tre tecnologie risulterà comunque proficuo.

## <a name="next-steps"></a>Passaggi successivi
Introduzione a ognuno dei servizi hello creando prima del flusso, la logica app, app di funzione o processo Web. Fare clic su uno qualsiasi dei seguenti collegamenti hello:

* [Get started with Microsoft Flow](https://flow.microsoft.com/en-us/documentation/getting-started/) (Introduzione a Microsoft Flow)
* [Creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md)
* [Creare la prima funzione di Azure](functions-create-first-azure-function.md)
* [Distribuzione di processi Web usando Visual Studio](../app-service-web/websites-dotnet-deploy-webjobs.md)

In alternativa, è possibile ottenere ulteriori informazioni su questi servizi di integrazione con hello seguenti collegamenti:

* [Leveraging Azure Functions & Azure App Service for integration scenarios](http://www.biztalk360.com/integrate-2016-resources/leveraging-azure-functions-azure-app-service-integration-scenarios/) (Sfruttare Funzioni di Azure e Servizio app di Azure per scenari di integrazione) di Christopher Anderson
* [Integrations Made Simple](http://www.biztalk360.com/integrate-2016-resources/integrations-made-simple/)
* [Logic Apps Live Webcast](http://aka.ms/logicappslive)
* [Microsoft Flow Frequently asked question](https://flow.microsoft.com/documentation/frequently-asked-questions/)
* [Risorse di documentazione di Processi Web di Azure](../app-service-web/websites-webjobs-resources.md)

