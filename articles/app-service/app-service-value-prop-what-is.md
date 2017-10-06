---
title: aaaAzure servizio App per dispositivi mobili, web e App per le API | Documenti Microsoft
description: Informazioni su come il servizio app di Azure consente di sviluppare, distribuire e gestire app Web e per dispositivi mobili.
keywords: "servizio app, servizio app di Azure, costo servizio app, scalabilità, scalabile, distribuzione app, distribuzione app Azure, PaaS, piattaforma distribuita come servizio, sito Web, Web, servizi mobili di Azure"
services: app-service
documentationcenter: 
author: omarkmsft
manager: erikre
editor: cephalin
ms.assetid: 979cafa8-eeb6-4d3b-87cf-764a821c3e4f
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 12/02/2016
ms.author: byvinyal
ms.openlocfilehash: 22f414c7d79092d87406a8d3538b946881fb4580
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-app-service"></a>Informazioni sul servizio app di Azure
Il *servizio app* è un'offerta di [piattaforma distribuita come servizio](https://en.wikipedia.org/wiki/Platform_as_a_service) (PaaS) di Microsoft Azure. Consente di creare app Web e per dispositivi mobili per qualsiasi piattaforma o dispositivo, integrare le app con soluzioni SaaS, connettersi con applicazioni locali e automatizzare i processi aziendali. Azure esegue le app in macchine virtuali (VM) completamente gestite, con le risorse di VM condivise o le VM dedicate desiderate.

Servizio App include web hello e funzionalità per dispositivi mobili che è in precedenza distribuiti separatamente come siti Web di Azure e servizi mobili di Azure. Include anche nuove funzionalità per l'automazione dei processi aziendali e l'hosting di API cloud. Come singolo servizio integrato, il servizio app consente di combinare vari componenti (siti Web, back-end di app per dispositivi mobili, API RESTful e processi aziendali) in un'unica soluzione.

Hello seguente 4 minuti video viene fornita una breve spiegazione di correlazione di tooearlier Azure App Service offerte e quali sono le novità in essa contenuti.

> [!VIDEO https://channel9.msdn.com/Series/Windows-Azure-Web-Sites-Tutorials/app-service-history-lesson/player]
> 
> 

## <a name="why-use-app-service"></a>Perché usare il servizio app?
Ecco alcune caratteristiche e funzionalità chiave del servizio app:

* **Più linguaggi e framework** : il servizio app offre un supporto ottimale per ASP.NET, Node.js, Java, PHP e Python. È anche possibile eseguire [Windows PowerShell e altri script o eseguibili](../app-service-web/web-sites-create-web-jobs.md) nelle VM del servizio app.
* **Ottimizzazione della metodologia DevOps**: è possibile configurare [l'integrazione e la distribuzione continua](../app-service-web/app-service-continuous-deployment.md) con Visual Studio Team Services, GitHub o BitBucket, alzare di livello gli aggiornamenti tramite [ambienti di testing e di staging](../app-service-web/web-sites-staged-publishing.md), eseguire [test A/B](../app-service-web/app-service-web-test-in-production-get-start.md) Gestire le app nel servizio App tramite [Azure PowerShell](/powershell/azureps-cmdlets-docs) o hello [interfaccia della riga di comando multipiattaforma (CLI)](../cli-install-nodejs.md).
* **Scalabilità globale con disponibilità elevata**: è possibile [aumentare le prestazioni](../app-service-web/web-sites-scale.md) o il [numero di istanze](../monitoring-and-diagnostics/insights-how-to-scale.md) manualmente o automaticamente. Consente di ospitare l'App in un punto qualsiasi nell'infrastruttura di Data Center globali di Microsoft e hello servizio App [contratto di servizio](https://azure.microsoft.com/support/legal/sla/app-service/) promesse la disponibilità elevata.
* **Dati locali e le piattaforme di tooSaaS connessioni** -scegliere da più di 50 [connettori](../connectors/apis-list.md) per i sistemi aziendali (ad esempio SAP, Siebel e Oracle), servizi SaaS (ad esempio, Salesforce e Office 365) e internet servizi (ad esempio Facebook e Twitter). nonché accedere ai dati locali con [connessioni ibride](../biztalk-services/integration-hybrid-connection-overview.md) e [reti virtuali di Azure](../app-service-web/web-sites-integrate-with-vnet.md).
* **Sicurezza e conformità** : il servizio app è [conforme a ISO, SOC e PCI](https://www.microsoft.com/TrustCenter/).
* **Modelli di applicazione** -scegliere da un elenco completo di modelli di hello [Azure Marketplace](https://azure.microsoft.com/marketplace/) che consentono di utilizzare un software di open source più diffusi guidata tooinstall, ad esempio WordPress, Joomla e Drupal.
* **Integrazione di Visual Studio** -strumenti dedicati in Visual Studio semplificano il lavoro hello di creazione, distribuzione e debug.

## <a name="app-types-in-app-service"></a>Tipi di app nel servizio app
Servizio App offre diversi *tipi di app*, ognuna delle quali è previsto toohost un carico di lavoro specifico:

* [**App Web**](../app-service-web/app-service-web-overview.md): per l'hosting di siti Web e applicazioni Web.
* [**App per dispositivi mobili**](../app-service-mobile/app-service-mobile-value-prop.md): per l'hosting di back-end di app per dispositivi mobili.
* [**App per le API**](../app-service-api/app-service-api-apps-why-best-platform.md): per l'hosting di API cloud.
* [**App per la logica**](../logic-apps/logic-apps-what-are-logic-apps.md): per l'automazione dei processi aziendali e l'integrazione dei sistemi e dei dati nei cloud senza scrivere codice.

Hello word *app* qui si riferisce toohello ospita risorse dedicate toorunning un carico di lavoro. Richiede "web app" ad esempio, probabilmente si è abituati toothinking di un'app web, come risorse di calcolo hello sia le applicazioni browser insieme offrono funzionalità tooa del codice. Ma nel servizio App un *app web* è hello risorse di calcolo forniti da Azure per ospitare il codice dell'applicazione. 

Un'applicazione può essere costituita da più app del servizio app di diversi tipi. Ad esempio se l'applicazione è costituita da un front-end Web e un back-end di API RESTful è possibile:

- Distribuire (front-end e api) tooa singolo web app  
- Distribuire l'app web di front-end codice tooa e app tooan API codice di back-end. 



## <a name="app-service-plans"></a>Piani di servizio app
[Piani di servizio app](azure-web-sites-web-hosting-plans-in-depth-overview.md) rappresentano raccolta hello di risorse fisiche utilizzate toohost app.

I piani di servizio app definiscono:

- **Area** (Stati Uniti occidentali, Stati Uniti orientali e così via)
- **Numero di scala** (uno, due, tre istanze e così via)
- **Dimensione dell'istanza** (Small, Medium, Large)
- **Unità SKU** (Free, Shared, Basic, Standard, Premium)

Tutte le applicazioni assegnate tooan **piano di servizio App** condividere risorse hello da essa consentendo toosave costo quando più applicazioni di hosting definite.

Il **piano di servizio App** possibile scalare da **libero** e **Shared** SKU troppo**base**, **Standard**, e **Premium** SKU è accedere alle risorse di toomore e funzionalità lungo hello modo. Una volta che il piano di servizio App è impostato troppo**base** o versione successiva è inoltre possibile controllare hello **dimensioni** e scala conteggio di hello macchine virtuali.

Hello **SKU** e **scala** di servizio App hello piano determina hello costo e hello non il numero di App ospitate in essa contenuti. 

Se si necessita di maggiore scalabilità e isolamento rete, è possibile eseguire le app in un [ambiente del servizio app](../app-service-web/app-service-app-service-environment-intro.md).

## <a name="pricing"></a>Prezzi
Per informazioni sul costo del servizio app, vedere [Prezzi del servizio app](https://azure.microsoft.com/pricing/details/app-service/).

## <a name="test-drive-app-service"></a>Provare il servizio app
[Creare un'app Web, un'app per dispositivi mobili o un'app per la logica di esempio](https://azure.microsoft.com/try/app-service/) e provarla per un'ora, senza alcun impegno e senza l'uso di una carta di credito.

In alternativa, aprire un [account Azure gratuito](https://azure.microsoft.com/pricing/free-trial/)e provare una delle esercitazioni introduttive:

* [Esercitazione sulla creazione di un'app Web](../app-service-web/app-service-web-get-started.md)
* [Esercitazione sulla creazione di un'app per dispositivi mobili](../app-service-mobile/app-service-mobile-android-get-started.md)
* [Esercitazione sulla creazione di un'app per le API](../app-service-api/app-service-api-dotnet-get-started.md)
* [Esercitazione sulla creazione di un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md)

