---
title: Scegliere tra Flow, App per la logica, Funzioni e Processi Web | Microsoft Docs
description: "Mettere a confronto i servizi di integrazione cloud di Microsoft e decidere quali è consigliabile usare."
services: functions,app-service\logic
documentationcenter: na
author: ggailey777
manager: wpickett
tags: 
keywords: microsoft flow, flow, app per la logica, funzioni di azure, funzioni, processi web di azure, processi web, elaborazione di eventi, calcolo dinamico, architettura senza server
ms.assetid: e9ccf7ad-efc4-41af-b9d3-584957b1515d
ms.service: functions
ms.devlang: multiple
ms.topic: overview
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 11/03/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 7ffe44828735a5687008ebc5a7d8d9f017f49daa
ms.sourcegitcommit: be9a42d7b321304d9a33786ed8e2b9b972a5977e
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/19/2018
---
# <a name="choose-between-flow-logic-apps-functions-and-webjobs"></a>Scegliere tra Flow, App per la logica, Funzioni e Processi Web
Questo articolo mette a confronto i servizi seguenti, disponibili in Microsoft Cloud, ognuno dei quali consente di risolvere i problemi di integrazione e automatizzare i processi aziendali:

* [Microsoft Flow](https://flow.microsoft.com/)
* [App per la logica di Azure](https://azure.microsoft.com/services/logic-apps/)
* [Funzioni di Azure](https://azure.microsoft.com/services/functions/)
* [Processi Web del servizio app di Azure](../app-service/web-sites-create-web-jobs.md)

Tutti questi servizi risultano utili quando si "mettono insieme" sistemi diversi. Possono definire input, azioni, condizioni e output e ognuno può essere eseguito in base a una pianificazione o un trigger. Tuttavia, ogni servizio offre vantaggi esclusivi e il confronto non è finalizzato a stabilire qual è il servizio migliore, ma qual è il servizio più adatto per una determinata situazione. Una combinazione di questi servizi è spesso il modo migliore per creare rapidamente una soluzione di integrazione scalabile e con funzionalità complete.

<a name="flow"></a>

## <a name="flow-vs-logic-apps"></a>Flow rispetto ad App per la logica
Microsoft Flow e App per la logica di Azure possono essere affrontati insieme, perché entrambi sono servizi di integrazione *configuration-first*. Semplificano la creazione di processi e flussi di lavoro e l'integrazione con varie applicazioni SaaS e aziendali. 

* Flow si basa sulle app per la logica
* Hanno la stessa funzionalità di progettazione flussi di lavoro
* [connettori](../connectors/apis-list.md) che funzionano in un servizio possono funzionare anche nell'altro

Flow consente a qualsiasi impiegato di eseguire semplici integrazioni, ad esempio un processo di approvazione su una raccolta documenti di SharePoint, senza ricorrere a sviluppatori o professionisti IT. D'altra parte, App per la logica consente di abilitare integrazioni avanzate, come i processi B2B, in cui sono necessarie procedure di sicurezza e la metodologia DevOps a livello di organizzazione. È normale che la complessità di un flusso di lavoro aziendale aumenti nel tempo. Di conseguenza, è possibile iniziare con un flusso e quindi convertirlo in un'app per la logica in base alle esigenze.

La tabella seguente consente di determinare se per una data integrazione è più appropriato usare Flow o App per la logica.

|  | Flusso | App per la logica |
| --- | --- | --- |
| Audience |Impiegati, utenti aziendali, amministratori di SharePoint |Integratori e sviluppatori professionisti, professionisti IT |
| Scenari |Self-service |Integrazioni avanzate |
| Strumento di progettazione |Nel browser e app per dispositivi mobili, solo interfaccia utente |Nel browser e in [Visual Studio](../logic-apps/logic-apps-deploy-from-vs.md) è disponibile la [visualizzazione Codice](../logic-apps/logic-apps-author-definitions.md) |
| Application Lifecycle Management (ALM) |Progettare ed eseguire test in ambienti non di produzione, alzare di livello quando si è pronti. |DevOps: controllo del codice sorgente, test, supporto, automazione e gestibilità in [Azure Resource Manager](../logic-apps/logic-apps-create-deploy-azure-resource-manager-templates.md) |
| Esperienza di amministrazione |Gestire ambienti di Flow e criteri di prevenzione della perdita dei dati, tenere traccia delle licenze [https://admin.flow.microsoft.com](https://admin.flow.microsoft.com) |Gestire gruppi di risorse, connessioni, gestione dell'accesso e registrazione [https://portal.azure.com](https://portal.azure.com) |
| Sicurezza |Log di controllo del Centro sicurezza e conformità di Office 365, prevenzione della perdita dei dati, [crittografia di dati inattivi](https://wikipedia.org/wiki/Data_at_rest#Encryption) per dati sensibili e così via. |Garanzie di sicurezza di Azure: [Sicurezza di Azure](https://www.microsoft.com/trustcenter/Security/AzureSecurity), [Centro sicurezza](https://azure.microsoft.com/services/security-center/), [log di controllo](https://azure.microsoft.com/blog/azure-audit-logs-ux-refresh/) e altro. |

<a name="function"></a>

## <a name="functions-vs-webjobs"></a>Funzioni e WebJobs
Funzioni di Azure e Processi Web del servizio app di Azure possono essere esaminati insieme, essendo entrambi servizi di integrazione di tipo *code first* e progettati per gli sviluppatori. Consentono di eseguire uno script o un frammento di codice in risposta a eventi diversi, ad esempio [nuovi BLOB di archiviazione](functions-bindings-storage.md) o [una richiesta di webhook](functions-bindings-http-webhook.md). Ecco le analogie: 

* Entrambi si basano sul [Servizio app di Azure](../app-service/app-service-web-overview.md) e usano funzionalità come [controllo del codice sorgente](../app-service/app-service-continuous-deployment.md), [autenticazione](../app-service/app-service-authentication-overview.md), e [monitoraggio](../app-service/web-sites-monitor.md).
* Sono entrambi servizi rivolti agli sviluppatori.
* Supportano entrambi linguaggi di scripting e programmazione standard.
* Per entrambi è disponibile il supporto di NuGet e NPM.

Funzioni è l'evoluzione naturale di Processi Web, nel senso che usa gli elementi ottimali di Processi Web come base per il miglioramento. I miglioramenti includono: 

* Modello App [senza server](https://azure.microsoft.com/overview/serverless-computing/).
* Sviluppo, test ed esecuzione di codice più semplici, direttamente nel browser.
* Integrazione predefinita con più servizi di Azure e di terze parti come i [webhook GitHub](https://developer.github.com/webhooks/creating/).
* Pagamento a consumo, non è necessario pagare per un [piano di servizio app](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).
* [Ridimensionamento dinamico](functions-scale.md)automatico.
* I clienti del servizio app esistenti possono comunque scegliere l'esecuzione con un piano di servizio app per sfruttare i vantaggi delle risorse sottoutilizzate.
* Integrazione con App per la logica.

La tabella seguente riepiloga le differenze tra Funzioni e Processi Web:

|  | Funzioni | WebJobs |
| --- | --- | --- |
| Ridimensionamento |Ridimensionamento senza configurazione |Ridimensionamento con il piano di servizio app |
| Prezzi |Pagamento a consumo o parte del piano di servizio app |Parte del piano di servizio app |
| Tipo di esecuzione |Attivata, pianificata (da trigger timer) |Attivata, continua, pianificata |
| Eventi di attivazione |[Timer](functions-bindings-timer.md), [Azure Cosmos DB](functions-bindings-cosmosdb.md), [Hub eventi di Azure](functions-bindings-event-hubs.md), [HTTP/webhook (GitHub, Slack)](functions-bindings-http-webhook.md), [app per dispositivi mobili del servizio app di Azure](functions-bindings-mobile-apps.md), [Hub eventi di Azure](functions-bindings-event-hubs.md), [BLOB e code di archiviazione di Azure](functions-bindings-storage-blob.md), [code e argomenti del bus di servizio di Azure](functions-bindings-service-bus.md) |[BLOB e code di archiviazione di Azure](functions-bindings-storage-blob.md), [code e argomenti del bus di servizio di Azure](functions-bindings-service-bus.md) |
| Sviluppo nel browser |Supportato |Non supportato |
| C# |Supportato |Supportato |
| F# |Supportato |Non supportato |
| JavaScript |Supportato |Supportato |
| Java |Preview | Non supportate |
| Bash |Sperimentale |Supportato |
| Scripting Windows (.cmd, .bat) |Sperimentale |Supportato |
| PowerShell |Sperimentale |Supportato |
| PHP |Sperimentale |Supportato |
| Python |Sperimentale |Supportato |
| TypeScript |Sperimentale |Non supportato |

L'uso di Funzioni o di Processi Web dipende in definitiva dalle operazioni che già si svolgono con il servizio app. Se è disponibile un'app del servizio app per cui si vogliono eseguire frammenti di codice e avere la possibilità di gestirli insieme nello stesso ambiente DevOps, usare Processi Web. Usare Funzioni negli scenari seguenti.

* Eseguire frammenti di codice per altri servizi di Azure o applicazioni di terze parti.
* Gestire separatamente il codice di integrazione delle app del servizio app.
* Chiamare i frammenti di codice da un'app per la logica. 

<a name="together"></a>

## <a name="flow-logic-apps-and-functions-together"></a>Flow, App per la logica e Funzioni insieme
Come accennato in precedenza, il servizio ottimale dipende dalla situazione specifica dell'utente. 

* Per la semplice ottimizzazione aziendale usare Flow.
* Se lo scenario di integrazione è troppo avanzato per Flow o sono necessarie le funzionalità di DevOps, usare App per la logica.
* Se un passaggio nello scenario di integrazione richiede codice specializzato o di trasformazione altamente personalizzato, scrivere una funzione e quindi attivarla come azione nell'app per la logica.

È possibile chiamare un'app per la logica in un flusso. Si può anche chiamare una funzione in un'app per la logica e un'app per la logica in una funzione. L'integrazione tra Flow, App per la logica e Funzioni continua a migliorare nel tempo. È possibile creare un elemento in un servizio e usarlo in altri servizi. Qualsiasi investimento effettuato in queste tre tecnologie risulterà comunque proficuo.

## <a name="next-steps"></a>Passaggi successivi
Per un'introduzione a ognuno di questi servizi, creare il primo flusso, la prima app per la logica, la prima app per le funzioni o il primo processo Web. Fare clic su uno di questi collegamenti:

* [Get started with Microsoft Flow](https://flow.microsoft.com/en-us/documentation/getting-started/) (Introduzione a Microsoft Flow)
* [Creare un'app per la logica](../logic-apps/quickstart-create-first-logic-app-workflow.md)
* [Creare la prima funzione di Azure](functions-create-first-azure-function.md)
* [Distribuzione di processi Web usando Visual Studio](../app-service/websites-dotnet-deploy-webjobs.md)

In alternativa, è possibile ottenere altre informazioni su questi servizi di integrazione usando i collegamenti seguenti:

* [Leveraging Azure Functions & Azure App Service for integration scenarios](http://www.biztalk360.com/integrate-2016-resources/leveraging-azure-functions-azure-app-service-integration-scenarios/) (Sfruttare Funzioni di Azure e Servizio app di Azure per scenari di integrazione) di Christopher Anderson
* [Integrations Made Simple](http://www.biztalk360.com/integrate-2016-resources/integrations-made-simple/)
* [Logic Apps Live Webcast](http://aka.ms/logicappslive)
* [Microsoft Flow Frequently asked question](https://flow.microsoft.com/documentation/frequently-asked-questions/)

