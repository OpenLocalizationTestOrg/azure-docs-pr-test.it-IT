---
title: aaaIntroduction tooApp v1 ambiente del servizio
description: "Informazioni sulla funzionalità hello v1 ambiente del servizio App che fornisce l'unità di scala sicura, dedicata appartenenti a un rete virtuale per l'esecuzione di tutte le app."
services: app-service
documentationcenter: 
author: stefsch
manager: erikre
editor: 
ms.assetid: 78e6d4f5-da46-4eb5-a632-b5fdc17d2394
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: ccompy
ms.openlocfilehash: 6e3cd1909b241887b5ec19412b9f7884d870cc3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooapp-service-environment-v1"></a>Introduzione tooApp v1 ambiente del servizio

> [!NOTE]
> Questo articolo è sull'ambiente del servizio App v1 hello.  È una versione più recente di hello ambiente del servizio App che è più facile toouse e viene eseguito sull'infrastruttura più potente. informazioni sulla nuova versione di hello iniziare con hello toolearn [toohello introduzione ambiente del servizio App](../app-service/app-service-environment/intro.md).
> 

## <a name="overview"></a>Panoramica
Un ambiente di servizio app è un'opzione del piano di servizio [Premium][PremiumTier] di Servizio app di Azure che fornisce un ambiente completamente isolato e dedicato all'esecuzione sicura delle app di Servizio di Azure su larga scala, tra cui [app Web][WebApps], [app per dispositivi mobili][MobileApps], e [app per le API][APIApps].  

Gli ambienti di servizi di app sono ideali per i carichi di lavoro dell'applicazione che richiedono:

* Scalabilità molto elevata
* Isolamento e accesso alla rete protetto

I clienti possono creare più ambienti di servizi di applicazione in una singola area di Azure, nonché in più aree di Azure.  Questo rende gli Ambienti di servizio dell’App ideali per i livelli dell’applicazione con scalabilità orizzontale senza stato, nel supportare i carichi di lavoro elevati RPS.

Gli ambienti del servizio App sono isolati toorunning solo le applicazioni di un singolo cliente e vengono sempre distribuiti in una rete virtuale.  Sono dotate di un controllo accurato sul traffico di rete sia in ingresso e in uscita dell'applicazione e le applicazioni possono stabilire connessioni protette ad alta velocità su alle risorse aziendali locali tooon reti virtuali.

Tutti gli articoli e in che modo-per informazioni su degli ambienti del servizio App sono disponibili in hello [file Leggimi per gli ambienti del servizio dell'applicazione](../app-service/app-service-app-service-environments-readme.md).

Per una panoramica di come gli ambienti del servizio App abilitare su larga scala e proteggere l'accesso alla rete, vedere hello [approfondimento AzureCon] [ AzureConDeepDive] negli ambienti di servizio App.

Per un'analisi approfondita sulla scalabilità orizzontale utilizzando più ambienti di servizio App vedere l'articolo di hello sul toosetup un [footprint app distribuita geograficamente][GeodistributedAppFootprint].

toosee come è stato configurato l'architettura di sicurezza hello illustrata in hello AzureCon analisi approfondita, vedere l'articolo hello sull'implementazione di un [a più livelli di architettura di sicurezza](app-service-app-service-environment-layered-security.md) con gli ambienti del servizio App.

Le app in esecuzione in ambienti di servizio app possono avere l'accesso controllato da dispositivi upstream, quali i firewall di applicazione web (WAF).  articolo Hello in [configurazione di un WAF per gli ambienti del servizio App](app-service-app-service-environment-web-application-firewall.md) illustra questo scenario. 

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="dedicated-compute-resources"></a>Risorse di calcolo dedicate
Calcolo hello le risorse in un ambiente del servizio App sono tutte dedicato esclusivamente tooa singola sottoscrizione e un ambiente del servizio App può essere configurato con le risorse di calcolo toofifty (50) per l'uso esclusivo da un'unica applicazione.

Un ambiente del servizio App è costituito da un pool di risorse di calcolo front-end, nonché i pool di risorse di calcolo lavoro uno toothree. 

pool di server front-end Hello contiene risorse di calcolo responsabile della terminazione SSL come il bilanciamento del carico automatico e di richieste di app all'interno di un ambiente del servizio App. 

Ogni pool di lavoro contiene le risorse di calcolo allocate troppo[piani di servizio App][AppServicePlan], che a sua volta contiene uno o più applicazioni di servizio App di Azure.  Poiché possono essere i pool di lavoro diverso toothree in un ambiente del servizio App, è necessario hello flessibilità toochoose diversi le risorse di calcolo per ogni pool di lavoro.  

Ad esempio, questo consente di pool di lavoro uno toocreate con risorse di calcolo meno potenti per piani di servizio App previsto per le applicazioni di sviluppo o test.  Un secondo (o perfino un terzo) pool di lavoro potrebbe usare risorse di calcolo più potenti dedicate ai piani di servizio app che eseguono le app di produzione.

Per ulteriori informazioni sulla quantità di hello di calcolo risorse disponibili toohello front-end e i pool di lavoro, vedere [come un ambiente del servizio App tooConfigure][HowToConfigureanAppServiceEnvironment].  

Per informazioni dettagliate su hello disponibile calcolano le dimensioni delle risorse supportati in un ambiente del servizio App, consultare hello [prezzi del servizio App] [ AppServicePricing] pagina ed esaminare le opzioni disponibili hello per gli ambienti del servizio App hello Premium piano tariffario.

## <a name="virtual-network-support"></a>Supporto della rete virtuale
Un ambiente del servizio app può essere creato **in** una rete virtuale di Azure Resource Manager **o** in una rete virtuale del modello di distribuzione classica. [Altre informazioni sulle reti virtuali][MoreInfoOnVirtualNetworks].  Poiché un ambiente del servizio App è sempre presente in una rete virtuale e, in modo più preciso all'interno di una subnet di una rete virtuale, è possibile sfruttare le funzionalità di sicurezza hello di reti virtuali toocontrol entrambe le comunicazioni di rete in ingresso e in uscita.  

Un ambiente del servizio app può avere connessione a Internet con un indirizzo IP pubblico o connessione interna con un indirizzo del Servizio di bilanciamento del carico interno di Azure.

È possibile utilizzare [gruppi di sicurezza di rete] [ NetworkSecurityGroups] toorestrict in ingresso subnet toohello le comunicazioni di rete in cui si trova un ambiente del servizio App.  In questo modo le app toorun dietro a monte dispositivi e servizi, ad esempio i firewall applicazione web e i provider SaaS di rete.

Le applicazioni inoltre spesso necessitano tooaccess alle risorse aziendali, ad esempio servizi web e database interni.  Un approccio comune è toomake flusso all'interno di una rete virtuale di Azure il traffico di rete disponibili toointernal solo questi endpoint.  Una volta che un ambiente del servizio App è unita in join toohello stessa rete virtuale come hello interno servizi delle applicazioni in esecuzione nell'ambiente di hello può accedervi, inclusi gli endpoint raggiungibili tramite [Site-to-Site] [ SiteToSite]e [Azure ExpressRoute] [ ExpressRoute] connessioni.

Per ulteriori dettagli sul funzionamento gli ambienti del servizio App con le reti virtuali e reti locali consultare i seguenti articoli hello [architettura di rete][NetworkArchitectureOverview], [controllo in ingresso Traffico][ControllingInboundTraffic], e [connessione in modo sicuro tooBackends][SecurelyConnectingToBackends]. 

## <a name="getting-started"></a>introduttiva
tooget avviato con gli ambienti del servizio App, vedere [come tooCreate un ambiente del servizio App][HowToCreateAnAppServiceEnvironment]

Tutti gli articoli e in che modo-per per gli ambienti del servizio App sono disponibili in hello [file Leggimi per gli ambienti del servizio dell'applicazione](../app-service/app-service-app-service-environments-readme.md).

Per ulteriori informazioni sulla piattaforma Azure App Service hello, vedere [Azure App Service][AzureAppService].

Per una panoramica dell'architettura di rete dell'ambiente del servizio App hello, vedere hello [Cenni preliminari sull'architettura di rete] [ NetworkArchitectureOverview] articolo.

Per ulteriori informazioni sull'uso di un ambiente del servizio App con ExpressRoute, vedere hello articolo seguente [Express Route e gli ambienti del servizio App][NetworkConfigDetailsForExpressRoute].

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[PremiumTier]: http://azure.microsoft.com/pricing/details/app-service/
[MoreInfoOnVirtualNetworks]: https://azure.microsoft.com/documentation/articles/virtual-networks-faq/
[AppServicePlan]: http://azure.microsoft.com/documentation/articles/azure-web-sites-web-hosting-plans-in-depth-overview/
[HowToCreateAnAppServiceEnvironment]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-an-app-service-environment/
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/
[WebApps]: http://azure.microsoft.com/documentation/articles/app-service-web-overview/
[MobileApps]: http://azure.microsoft.com/documentation/articles/app-service-mobile-value-prop-preview/
[APIApps]: http://azure.microsoft.com/documentation/articles/app-service-api-apps-why-best-platform/
[LogicApps]: http://azure.microsoft.com/documentation/articles/app-service-logic-what-are-logic-apps/
[AzureConDeepDive]:  https://azure.microsoft.com/documentation/videos/azurecon-2015-deploying-highly-scalable-and-secure-web-and-mobile-apps/
[GeodistributedAppFootprint]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-geo-distributed-scale/
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[SiteToSite]: https://azure.microsoft.com/documentation/articles/vpn-gateway-site-to-site-create/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
[HowToConfigureanAppServiceEnvironment]:  http://azure.microsoft.com/documentation/articles/app-service-web-configure-an-app-service-environment/
[ControllingInboundTraffic]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/
[SecurelyConnectingToBackends]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-securely-connecting-to-backend-resources/
[NetworkArchitectureOverview]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-architecture-overview/
[NetworkConfigDetailsForExpressRoute]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-configuration-expressroute/
[AppServicePricing]: http://azure.microsoft.com/pricing/details/app-service/ 

<!-- IMAGES -->


