---
title: Panoramica di architettura di App servizio ambienti aaaNetwork
description: Panoramica dell'architettura della topologia di rete degli ambienti del servizio app.
services: app-service
documentationcenter: 
author: stefsch
manager: erikre
editor: 
ms.assetid: 13d03a37-1fe2-4e3e-9d57-46dfb330ba52
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/04/2016
ms.author: stefsch
ms.openlocfilehash: 3cbc86883f5687a9ada35a3ab2f577a450a3fa0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="network-architecture-overview-of-app-service-environments"></a>Panoramica dell'architettura di rete degli ambienti del servizio app
## <a name="introduction"></a>Introduzione
Gli ambienti del servizio App vengono sempre creati all'interno di una subnet di un [rete virtuale] [ virtualnetwork] -le applicazioni in esecuzione in un ambiente del servizio App possono comunicare con privato endpoint si trovano all'interno di hello stesso virtuale topologia di rete.  Poiché i clienti possono bloccare le parti dell'infrastruttura di rete virtuale, è importante toounderstand tipi di hello dei flussi di comunicazione di rete che si verificano con un ambiente del servizio App.

## <a name="general-network-flow"></a>Flusso di rete generale
Quando un ambiente del servizio app usa un indirizzo IP virtuale pubblico (VIP) per le app, tutto il traffico in ingresso viene ricevuto su questo indirizzo VIP pubblico.  Sono inclusi il traffico HTTP e HTTPS per le app, altro traffico per l'FTP, la funzionalità di debug remoto e le operazioni di gestione di Azure.  Per un elenco completo di hello porte specifiche (obbligatori e facoltative) disponibili in VIP pubblico hello vedere l'articolo di hello in [controllare il traffico in entrata] [ controllinginboundtraffic] tooan ambiente del servizio App. 

Gli ambienti del servizio App supportare anche l'esecuzione delle App che sono associate solo tooa virtuale rete indirizzo interno, denominato anche tooas un indirizzo di bilanciamento del carico interno (bilanciamento del carico interno).  In un bilanciamento del carico interno traffico ASE, HTTP e HTTPS abilitato per le app, nonché il debug delle chiamate remote, arrivano sul hello indirizzo di bilanciamento del carico interno.  Per le configurazioni di bilanciamento del carico interno ASE più comuni, il traffico FTP o FTPS anche arriveranno hello indirizzo di bilanciamento del carico interno.  Tuttavia le operazioni di gestione di Azure passeranno tooports 454/455 su hello VIP pubblico di un ILB abilitato ASE.

Hello seguito vengono illustrate una panoramica di hello vari flussi di rete in ingresso e in uscita per un ambiente del servizio App in cui sono associati tooa indirizzo IP virtuale pubblico hello App:

![Flussi di rete generali][GeneralNetworkFlows]

Un ambiente del servizio app può comunicare con svariati endpoint di clienti privati.  Ad esempio, le applicazioni in esecuzione nell'ambiente del servizio App può connettersi toodatabase server in esecuzione nelle macchine virtuali IaaS hello hello stessa topologia di rete virtuale.

> [!IMPORTANT]
> Esaminando il diagramma di rete hello, hello "altre calcolo risorse" vengono distribuite in una Subnet diversa da hello ambiente del servizio App. Distribuzione delle risorse in hello stessa Subnet con hello ASE bloccherà la connettività dalle risorse toothose ASE (ad eccezione di routing specifico intra-ASE). Distribuire tooa Subnet diversa invece (nella stessa rete virtuale hello). Hello ambiente del servizio App sarà quindi in grado di tooconnect. Non è necessaria alcuna configurazione aggiuntiva.
> 
> 

Gli ambienti del servizio app comunicano anche con le risorse database SQL e di archiviazione di Azure necessarie per la gestione e il funzionamento di un ambiente del servizio app.  Alcune delle risorse di archiviazione e Sql hello un ambiente del servizio App con cui comunica si trovano in hello stessa area hello ambiente del servizio App, mentre altri si trovano in aree di Azure remote.  Di conseguenza, la connettività in uscita toohello Internet è sempre necessario per un ambiente del servizio App di toofunction correttamente. 

Poiché un ambiente del servizio App viene distribuito in una subnet, gruppi di sicurezza di rete possono essere utilizzati toocontrol subnet toohello il traffico in ingresso.  Per informazioni dettagliate su come toocontrol in ingresso a traffico tooan ambiente del servizio App, vedere l'esempio hello [articolo][controllinginboundtraffic].

Per informazioni dettagliate su come tooallow la connettività Internet in uscita da un ambiente del servizio App, vedere l'articolo sull'utilizzo di seguente hello [Express Route][ExpressRoute].  il tunneling forzato Hello stesso approccio descritto nell'articolo hello si applica quando si utilizza la connettività da sito a sito e l'uso.

## <a name="outbound-network-addresses"></a>Indirizzi di rete in uscita
Quando un ambiente del servizio App effettua chiamate in uscita, un indirizzo IP è sempre associato a chiamate in uscita hello.  indirizzo IP specifico Hello utilizzato varia a seconda che endpoint hello la chiamata si trova all'interno della topologia di rete virtuale hello o all'esterno di topologia di rete virtuale hello.

Se la chiamata endpoint di hello **esterno** della topologia di rete virtuale hello, hello in uscita indirizzo (noto anche come hello in uscita NAT) utilizzato è hello VIP pubblico di hello ambiente del servizio App.  Questo indirizzo è reperibile nell'interfaccia utente del portale hello per hello ambiente del servizio App nel Pannello proprietà.

![Indirizzo IP in uscita][OutboundIPAddress]

Questo indirizzo può essere determinato anche per ASEs che hanno solo un VIP pubblico creando un'applicazione hello ambiente del servizio App, e quindi eseguendo un *nslookup* sull'indirizzo dell'applicazione hello. l'indirizzo IP Hello risulta sia VIP pubblico hello sia indirizzo NAT in uscita dell'ambiente del servizio App di hello.

Se la chiamata endpoint di hello **all'interno di** della topologia di rete virtuale hello, indirizzo in uscita di hello dell'applicazione chiamante hello sarà l'indirizzo IP interno hello della risorsa di calcolo singole hello in esecuzione app hello.  Tuttavia non è un mapping persistente di tooapps gli indirizzi IP interni di rete virtuale.  App è possono spostarsi tra le risorse di calcolo diverso e pool di risorse di calcolo disponibili in un ambiente del servizio App di hello modificabili a causa di operazioni tooscaling.

Tuttavia, poiché un ambiente del servizio App si trova sempre all'interno di una subnet, si è certi che indirizzo IP interno hello di esecuzione di un'applicazione di una risorsa di calcolo verrà si trovano sempre all'interno di un intervallo di subnet hello CIDR hello.  Di conseguenza, quando vengono utilizzati gli ACL con granularità fine o gruppi di sicurezza di rete toosecure accedere agli endpoint tooother all'interno di rete virtuale hello, hello intervallo di subnet contenente toobe esigenze di ambiente del servizio App hello concesso l'accesso.

Hello diagramma seguente illustra questi concetti in modo più dettagliato:

![Indirizzi di rete in uscita][OutboundNetworkAddresses]

In hello diagramma:

* Poiché hello VIP pubblico di hello ambiente del servizio App è 192.23.1.2, che è hello in uscita degli indirizzi IP utilizzati quando si effettuano chiamate troppo endpoint "Internet".
* Hello intervallo CIDR di hello contenente subnet per hello ambiente del servizio App è 10.0.1.0/26.  Altri endpoint all'interno di hello stessa infrastruttura di rete virtuale verrà visualizzato chiamate dalle applicazioni come proveniente da un punto qualsiasi all'interno di questo intervallo di indirizzi.

## <a name="calls-between-app-service-environments"></a>Chiamate tra gli ambienti del servizio app
Uno scenario più complesso può verificarsi se si distribuiscono più ambienti di servizio App in hello stessa rete virtuale, quindi effettuare chiamate in uscita da un ambiente del servizio App tooanother ambiente del servizio App.  Anche questi tipi di chiamate tra ambienti del servizio app saranno considerati come chiamate "Internet".

Hello seguente diagramma viene illustrato un esempio di un'architettura a più livelli con le App in un ambiente del servizio App (ad esempio Le app web da "Porta principale") la chiamata di App in un ambiente del servizio App secondo (ad esempio applicazioni API back-end interne non previsto toobe accessibile da Internet hello). 

![Chiamate tra gli ambienti del servizio app][CallsBetweenAppServiceEnvironments] 

In hello riportato sopra hello ambiente del servizio App "ASE uno" ha un indirizzo IP in uscita di 192.23.1.2.  Se un'app in esecuzione in questo ambiente del servizio App effettua un'app tooan chiamata in uscita in esecuzione in un secondo ambiente del servizio App ("ASE due") si trova nella stessa virtuale di rete, hello hello in uscita chiamata verrà considerata come una chiamata di "Internet".  Di conseguenza il traffico di rete hello in arrivo sul hello secondo ambiente del servizio App verrà visualizzata come proveniente da 192.23.1.2 (vale a dire non hello subnet intervallo di indirizzi hello prima dell'ambiente del servizio App).

Anche se le chiamate tra ambienti diversi di servizio App vengono considerate come chiamate di "Internet", quando entrambi gli ambienti del servizio App si trovano in hello traffico di rete stessa regione di Azure hello rimarrà nella rete Azure regionale hello e non trasmetterà fisicamente su hello rete Internet pubblica.  Di conseguenza è possibile utilizzare un gruppo di sicurezza di rete nella subnet hello di hello tooonly Consenti chiamate in ingresso dall'ambiente del servizio App secondo hello primo ambiente del servizio App (il cui indirizzo IP in uscita è 192.23.1.2), garantendo così la comunicazione protetta tra hello Ambienti del servizio app.

## <a name="additional-links-and-information"></a>Informazioni e collegamenti aggiuntivi
Tutti gli articoli e in che modo-per per gli ambienti del servizio App sono disponibili in hello [file Leggimi per gli ambienti del servizio dell'applicazione](../app-service/app-service-app-service-environments-readme.md).

Informazioni su dati in ingresso porte usate per gli ambienti del servizio App e toocontrol gruppi di sicurezza rete il traffico in ingresso è possibile utilizzare [qui][controllinginboundtraffic].

Informazioni dettagliate sull'utilizzo definiti dall'utente route toogrant in uscita Internet access tooApp gli ambienti del servizio è disponibile in questa [articolo][ExpressRoute]. 

<!-- LINKS -->
[virtualnetwork]: http://azure.microsoft.com/services/virtual-network/
[controllinginboundtraffic]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/
[ExpressRoute]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-configuration-expressroute/

<!-- IMAGES -->
[GeneralNetworkFlows]: ./media/app-service-app-service-environment-network-architecture-overview/NetworkOverview-1.png
[OutboundIPAddress]: ./media/app-service-app-service-environment-network-architecture-overview/OutboundIPAddress-1.png
[OutboundNetworkAddresses]: ./media/app-service-app-service-environment-network-architecture-overview/OutboundNetworkAddresses-1.png
[CallsBetweenAppServiceEnvironments]: ./media/app-service-app-service-environment-network-architecture-overview/CallsBetweenEnvironments-1.png

