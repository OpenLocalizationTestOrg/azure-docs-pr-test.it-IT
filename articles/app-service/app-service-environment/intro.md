---
title: ambienti di servizio App tooAzure aaaIntroduction
description: Breve panoramica degli ambienti del servizio app di Azure
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: 3c7eaefa-1850-4643-8540-428e8982b7cb
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: ccompy
ms.openlocfilehash: 9261041333cf59374974a039edf89c4983c45cdd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooapp-service-environments"></a>Ambienti del servizio tooApp introduzione #
 
## <a name="overview"></a>Panoramica ##

Ambiente del servizio app di Azure è una funzionalità del servizio app di Azure che fornisce un ambiente completamente isolato e dedicato per l'esecuzione sicura di app del servizio app di Azure su vasta scala. Questa funzionalità può ospitare [app Web][webapps], [app per dispositivi mobili][mobileapps], [app per le API][APIapps] e [Funzioni][Functions].

Gli ambienti del servizio app sono adatti ai carichi di lavoro dell'applicazione che richiedono:

- Scalabilità molto elevata.
- Isolamento e accesso alla rete protetto.
- Uso intensivo della memoria.

I clienti possono creare più ambienti del servizio app in una singola area di Azure o in più aree di Azure. Questa flessibilità rende gli ambienti del servizio app ideali per i livelli applicazione con scalabilità orizzontale senza stato, nel supportare i carichi di lavoro RPS elevati.

ASEs sono isolati toorunning solo le applicazioni di un singolo cliente e vengono sempre distribuiti in una rete virtuale. I clienti hanno il controllo con granularità fine del traffico di rete in ingresso e in uscita dell'applicazione. Le applicazioni è possono stabilire connessioni protette ad alta velocità tramite VPN alle risorse aziendali tooon locale.

Tutti gli articoli e come-tooinstructions su ASEs sono disponibili in hello [file Leggimi per gli ambienti del servizio App][ASEReadme]:

* Gli ambienti del servizio app consentono l'hosting di app su vasta scala con accesso di rete protetto. Per ulteriori informazioni, vedere hello [AzureCon approfondimento](https://azure.microsoft.com/documentation/videos/azurecon-2015-deploying-highly-scalable-and-secure-web-and-mobile-apps/) su ASEs.
* Più ASEs può essere utilizzato tooscale orizzontalmente. Per ulteriori informazioni, vedere [come tooset un footprint di app distribuita geograficamente](https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-geo-distributed-scale/).
* ASEs possono essere utilizzati tooconfigure architettura di sicurezza, come illustrato in hello AzureCon approfondimento. come è stato configurato l'architettura di sicurezza hello illustrata in hello approfondimento AzureCon, toosee vedere hello [articolo su come tooimplement un'architettura di sicurezza a più livelli](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-app-service-environment-layered-security) con gli ambienti del servizio App.
* Le app in esecuzione in ambienti del servizio app possono avere l'accesso controllato da dispositivi upstream, quali Web application firewall. Per altre informazioni, vedere [Configurazione di un Web application firewall (WAF) per l'ambiente del servizio app](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-app-service-environment-web-application-firewall).

## <a name="dedicated-environment"></a>Ambiente dedicato ##

Un ASE è dedicato esclusivamente tooa singola sottoscrizione e possono ospitare 100 istanze. intervallo di Hello può estendersi su 100 istanze in un singolo servizio App piano too100 a istanza singola App i piani di servizio e tutti gli elementi intermedi.

Un ambiente del servizio app è composto da front-end e ruoli di lavoro. I front-end sono responsabili della terminazione HTTP/HTTPS e del bilanciamento del carico automatico delle richieste di app all'interno di un ambiente del servizio app. Front-end vengono aggiunti automaticamente come piani di servizio App di hello ASE sono scalati hello.

I ruoli di lavoro ospitano app di clienti e sono disponibili in tre dimensioni fisse:

* Un core/3,5 GB di RAM
* Due core/7 GB di RAM
* Quattro core/14 GB di RAM

I clienti non devono worker e toomanage front-end. Tutta l'infrastruttura viene aggiunta automaticamente nel momento in cui i clienti aumentano il numero di istanze nei rispettivi piani di servizio app. Servizio App sono stati creati o ridimensionati in un ASE piani, hello necessario infrastruttura viene aggiunto o rimosso come appropriato.

È presente una frequenza mensile per un ASE che paga per infrastruttura hello e non cambia con dimensione hello di hello ASE. A questa si aggiunge il costo previsto per ogni core del piano di servizio app. Tutte le app ospitate in un ASE presenti hello isolato prezzi SKU. Per informazioni sui prezzi per un tipo di base, vedere hello [servizio App prezzi] [ Pricing] pagina ed esaminare le opzioni disponibili hello per ASEs.

## <a name="virtual-network-support"></a>Supporto della rete virtuale ##

È possibile creare un ambiente del servizio app solo in una rete virtuale di Azure Resource Manager. toolearn sulle reti virtuali di Azure, vedere hello [domande frequenti di reti virtuali di Azure](https://azure.microsoft.com/documentation/articles/virtual-networks-faq/). Un ambiente del servizio app esiste sempre in una rete virtuale e, più precisamente, all'interno di una subnet di una rete virtuale. È possibile utilizzare la funzionalità di sicurezza hello di reti virtuali toocontrol in ingresso e in uscita le comunicazioni per le applicazioni di rete.

Un ambiente del servizio app può avere una connessione a Internet con un indirizzo IP pubblico o una connessione interna con il solo indirizzo del servizio di bilanciamento del carico interno di Azure.

[Gruppi di sicurezza di rete] [ NSGs] limitare subnet toohello le comunicazioni di rete in ingresso in cui si trova un ASE. È possibile usare le app toorun NSGs dietro a monte dispositivi e servizi, ad esempio WAFs e i provider SaaS di rete.

Le applicazioni inoltre spesso necessitano tooaccess alle risorse aziendali, ad esempio servizi web e database interni. Se si distribuisce ASE hello in una rete virtuale che dispone di una rete di on-premise toohello connessione VPN, App hello in hello ASE possono accedere alle risorse locali di hello. Questa funzionalità è true indipendentemente dal fatto hello VPN sia un [site-to-site](https://azure.microsoft.com/documentation/articles/vpn-gateway-site-to-site-create/) o [Azure ExpressRoute](http://azure.microsoft.com/services/expressroute/) VPN.

Per altre informazioni sul funzionamento degli ambienti del servizio app con reti virtuali e reti locali, vedere [Considerazioni sulla rete per un ambiente del servizio app][ASENetwork].

## <a name="app-service-environment-v1"></a>Ambiente del servizio app 1 ##

Esistono due versioni dell'ambiente del servizio app: ASEv1 e ASEv2. Hello precedenti informazioni è basato su ASEv2. Questa sezione viene illustrata hello ASEv1 e ASEv2 differenze. 

In ASEv1, è necessario toomanage tutti hello risorse manualmente. Che include gli indirizzi IP usati per SSL basato su IP front-end hello e processi di lavoro. È possibile scalare orizzontalmente il piano di servizio App, è necessario toofirst scalabilità orizzontale in cui si desidera toohost pool di lavoro di hello.

ASEv1 usa un modello tariffario diverso rispetto a ASEv2. Nella versione ASEv1, in particolare, si paga per tutti i core allocati, inclusi i core usati per i front-end o i ruoli di lavoro in cui non sono ospitati carichi di lavoro. In ASEv1, hello predefinito della scala massima pari a un ASE sono 55 host totale. inclusi ruoli di lavoro e front-end. Un vantaggio tooASEv1 è che possono essere distribuito in una rete virtuale classica e una rete virtuale di gestione risorse. vedere toolearn ulteriori informazioni su ASEv1, [introduzione v1 ambiente del servizio App][ASEv1Intro].

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
