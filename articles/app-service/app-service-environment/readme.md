---
title: file Leggimi di ambiente del servizio App aaaAzure
description: Elenca la documentazione di hello che descrive l'ambiente del servizio App di Azure
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: 77452413-5193-4762-8b3d-5fa8e4edf1ca
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: ccompy
ms.openlocfilehash: 6edc74804ded7497e70c31c9e08252257add4415
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="app-service-environment-documentation"></a>Documentazione relativa all'ambiente del servizio app
 Ambiente del servizio app di Azure è una funzionalità del servizio app di Azure che fornisce un ambiente completamente isolato e dedicato per l'esecuzione sicura di app del servizio app di Azure su vasta scala. Questa funzionalità può ospitare [app Web][webapps], [app per dispositivi mobili][mobileapps], [app per le API][APIApps] e [Funzioni][Functions].

Gli ambienti del servizio app sono ideali per i carichi di lavoro dell'applicazione che richiedono:

* Scalabilità molto elevata.
* Isolamento e accesso alla rete protetto.

I clienti possono creare più ambienti del servizio app sia in una singola area di Azure che in più aree di Azure. Questa versatilità rende gli ambienti del servizio app ideali per i livelli applicazione con scalabilità orizzontale senza stato, nel supportare i carichi di lavoro RPS elevati.

ASEs sono isolati toorunning solo le applicazioni di un singolo cliente e vengono sempre distribuiti in una rete virtuale di Azure. I clienti hanno il controllo con granularità fine del traffico di rete in ingresso e in uscita dell'applicazione tramite [gruppi di sicurezza di rete][NSGs]. Le applicazioni inoltre possono stabilire connessioni protette ad alta velocità sulle risorse di reti virtuali tooon tra più sedi aziendali.

App è spesso necessitano tooaccess alle risorse aziendali, ad esempio servizi web e database interni. Le app in esecuzione in ambienti del servizio app possono accedere alle risorse tramite VPN [da sito a sito][SiteToSite] e connessioni [Azure ExpressRoute][ExpressRoute].

* [Che cos'è un ambiente del servizio app?][Intro]
* [Creare un ambiente del servizio app][MakeExternalASE]
* [Creare un ambiente del servizio app con bilanciamento del carico interno][MakeILBASE]
* [Usare un ambiente del servizio app][UsingASE]
* [Considerazioni sulla rete e hello ambiente del servizio App][ASENetwork]
* [Creare un ambiente del servizio app da un modello][MakeASEfromTemplate]


## <a name="videos"></a>Video
Master moderno PaaS per hello Enterprise con il servizio App di Azure
>[!VIDEO https://channel9.msdn.com/Events/Ignite/2016/BRK3205/player]

Deploying Highly Scalable and Secure Apps (Distribuzione di app altamente scalabili e sicure)
>[!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON325/player]

Running Enterprise Web and Mobile Apps on Azure App Service (Esecuzione di app aziendali Web e per dispositivi mobili nel Servizio app di Azure)
>[!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3715/player]

## <a name="app-service-environment-v1"></a>Ambiente del servizio app 1 ##
Esistono due versioni dell'ambiente del servizio app: ASEv1 e ASEv2. Per informazioni sulla versione ASEv1, vedere [Documentazione relativa agli ambienti del servizio app][ASEv1README].


<!--Links-->
[Intro]: ./intro.md
[MakeExternalASE]: ./create-external-ase.md
[MakeASEfromTemplate]: ./create-from-template.md
[MakeILBASE]: ./create-ilb-ase.md
[ASENetwork]: ./network-info.md
[ASEReadme]: ./readme.md
[UsingASE]: ./using-an-ase.md
[UDRs]: ../../virtual-network/virtual-networks-udr-overview.md
[NSGs]: ../../virtual-network/virtual-networks-nsg.md
[ConfigureASEv1]: ../../app-service-web/app-service-web-configure-an-app-service-environment.md
[ASEv1Intro]: ../../app-service-web/app-service-app-service-environment-intro.md
[webapps]: ../../app-service-web/app-service-web-overview.md
[mobileapps]: ../../app-service-mobile/app-service-mobile-value-prop.md
[APIapps]: ../../app-service-api/app-service-api-apps-why-best-platform.md
[Functions]: ../../azure-functions/index.yml
[Pricing]: http://azure.microsoft.com/pricing/details/app-service/
[ARMOverview]: ../../azure-resource-manager/resource-group-overview.md
[ConfigureSSL]: ../../app-service-web/web-sites-purchase-ssl-web-site.md
[Kudu]: http://azure.microsoft.com/resources/videos/super-secret-kudu-debug-console-for-azure-web-sites/
[AppDeploy]: ../../app-service-web/web-sites-deploy.md
[ASEWAF]: ../../app-service-web/app-service-app-service-environment-web-application-firewall.md
[AppGW]: ../../application-gateway/application-gateway-web-application-firewall-overview.md
[PremiumTier]: http://azure.microsoft.com/pricing/details/app-service/
[ASEv1README]: ../app-service-app-service-environments-readme.md
[SiteToSite]: ../../vpn-gateway/vpn-gateway-site-to-site-create.md
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
