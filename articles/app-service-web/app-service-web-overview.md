---
title: Panoramica di App aaaWeb | Documenti Microsoft
description: Informazioni sul modo in cui il Servizio app di Azure semplifica lo sviluppo e l'hosting di applicazioni Web
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 94af2caf-a2ec-4415-a097-f60694b860b3
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: overview
ms.date: 01/04/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: ce27519bddd62a7fca6ba1fb23c763d0fc378c2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="web-apps-overview"></a>Panoramica di App Web
*App Web del servizio app* è una piattaforma di calcolo completamente gestita, ottimizzata per l'hosting di siti Web e applicazioni Web. Questo [platform-as-a-service](https://en.wikipedia.org/wiki/Platform_as_a_service) offerta (PaaS) di Microsoft Azure consente di concentrarsi sulla logica di business, mentre Azure si occupa di hello infrastruttura toorun e ridimensionare le app.

Dopo 5 minuti video Hello introduce App Web di servizio App di Azure.

>[!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Azure-App-Service-Web-Apps-with-Yochay-Kiriaty/player]
>
>

> [!INCLUDE [app-service-linux](../../includes/app-service-linux.md)]
> 
> 

## <a name="what-is-a-web-app-in-app-service"></a>Informazioni sull'app Web in un servizio app
Nel servizio App, un *app web* è hello risorse di calcolo forniti da Azure per ospitare una sito o applicazione web.  

risorse di calcolo Hello potrebbero essere in condivise o dedicate macchine virtuali (VM), a seconda di hello tariffario scelto. Il codice dell'applicazione viene eseguito in una VM gestita, isolata da altri clienti.

È possibile usare per il codice qualsiasi linguaggio o framework supportato dal [Servizio app di Azure](../app-service/app-service-value-prop-what-is.md), ad esempio ASP.NET, Node.js, Java, PHP o Python. È anche possibile eseguire script che usano [PowerShell e altri linguaggi di scripting](web-sites-create-web-jobs.md#acceptablefiles) in un'app Web.

Per esempi di scenari di applicazione tipici che è possibile utilizzare le applicazioni Web per, vedere [scenari di app Web](https://azure.microsoft.com/documentation/scenarios/web-app/) hello e **scenari e i consigli** sezione [servizio App di Azure, Virtual Confronto tra le macchine, Service Fabric e servizi Cloud](choose-web-site-cloud-service-vm.md#scenarios).

## <a name="why-use-web-apps"></a>Vantaggi dell'uso di app Web
Ecco alcune delle funzionalità principali di servizio App che si applicano tooWeb App:

* **Più linguaggi e framework** : il servizio app offre un supporto ottimale per ASP.NET, Node.js, Java, PHP e Python. È anche possibile eseguire [PowerShell e altri script o eseguibili](web-sites-create-web-jobs.md) in VM del servizio app.
* **Ottimizzazione della metodologia DevOps**: è possibile configurare [l'integrazione e la distribuzione continua](app-service-continuous-deployment.md) con Visual Studio Team Services, GitHub o BitBucket, alzare di livello gli aggiornamenti tramite [ambienti di testing e di staging](web-sites-staged-publishing.md), eseguire [test A/B](app-service-web-test-in-production-get-start.md) Gestire le app nel servizio App tramite [Azure PowerShell](/powershell/azureps-cmdlets-docs) o hello [interfaccia della riga di comando multipiattaforma (CLI)](../cli-install-nodejs.md).
* **Scalabilità globale con disponibilità elevata**: è possibile [aumentare le prestazioni](web-sites-scale.md) o il [numero di istanze](../monitoring-and-diagnostics/insights-how-to-scale.md) manualmente o automaticamente. Consente di ospitare l'App in un punto qualsiasi nell'infrastruttura di Data Center globali di Microsoft e hello servizio App [contratto di servizio](https://azure.microsoft.com/support/legal/sla/app-service/) promesse la disponibilità elevata.
* **Dati locali e le piattaforme di tooSaaS connessioni** -scegliere da più di 50 [connettori](../connectors/apis-list.md) per i sistemi aziendali (ad esempio SAP, Siebel e Oracle), servizi SaaS (ad esempio, Salesforce e Office 365) e internet servizi (ad esempio Facebook e Twitter). nonché accedere ai dati locali con [connessioni ibride](../biztalk-services/integration-hybrid-connection-overview.md) e [reti virtuali di Azure](web-sites-integrate-with-vnet.md).
* **Sicurezza e conformità** : il servizio app è [conforme a ISO, SOC e PCI](https://www.microsoft.com/TrustCenter/).
* **Modelli di applicazione** -scegliere da un elenco completo di modelli delle applicazioni in hello [Azure Marketplace](https://azure.microsoft.com/marketplace/) che consentono di utilizzare un software di open source più diffusi guidata tooinstall, ad esempio WordPress, Joomla e Drupal.
* **Integrazione di Visual Studio** -strumenti dedicati in Visual Studio semplificano il lavoro hello di creazione, distribuzione e debug.

Un'app Web può anche sfruttare le funzionalità offerte dalle [app per le API](../app-service-api/app-service-api-apps-why-best-platform.md), ad esempio il supporto di CORS, e dalle [app per dispositivi mobili](../app-service-mobile/app-service-mobile-value-prop.md), ad esempio le notifiche push. Per altre informazioni sui tipi di app nel servizio app, vedere [Informazioni sul servizio app di Azure](../app-service/app-service-value-prop-what-is.md).

Oltre ad App Web nel servizio app, Azure offre altri servizi che possono essere usati per l'hosting di siti e applicazioni Web. Per la maggior parte degli scenari, le app Web è migliore di hello.  Per architettura microservizio, prendere in considerazione [Service Fabric](https://azure.microsoft.com/documentation/services/service-fabric)e se è necessario maggiore controllo sulla hello il codice viene eseguito su macchine virtuali, è consigliabile [macchine virtuali di Azure](https://azure.microsoft.com/documentation/services/virtual-machines/). Per ulteriori informazioni su come toochoose tra questi servizi di Azure, vedere [confronto servizi Cloud, macchine virtuali, Service Fabric e Azure App Service](choose-web-site-cloud-service-vm.md).

## <a name="getting-started"></a>introduttiva
tooget avviato tramite la distribuzione di esempio codice tooa nuova app web nel servizio App, seguire una delle esercitazioni di hello in hello seguente nella casella a discesa. Sarà necessario un account Azure gratuito.

> [!div class="op_single_selector"]
> * [Distribuire il primo tooAzure di app web ASP.NET 5 minuti](app-service-web-get-started-dotnet.md)
> * [Distribuire il primo tooAzure app web PHP 5 minuti](app-service-web-get-started-php.md)
> * [Distribuire il primo tooAzure di app web Node. js in 5 minuti](app-service-web-get-started-nodejs.md)
> * [Distribuire il primo tooAzure di app web Java in 5 minuti](app-service-web-get-started-java.md)
> * [Distribuire il primo tooAzure di app web Python in 5 minuti](app-service-web-get-started-python.md)
> * [Distribuire il primo tooAzure sito HTML 5 minuti](app-service-web-get-started-html.md)
> 
> 

> [!NOTE]
> È possibile [provare il servizio app](https://azure.microsoft.com/try/app-service/) senza avere un account Azure. Creare un'app di avvio e riprodurre per tooan orari, è richiesto alcun carta di credito, nessun impegni.
> 
> 
