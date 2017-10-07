---
title: Architettura di sicurezza con gli ambienti del servizio App aaaLayered
description: "Implementazione di un'architettura di sicurezza su più livelli con ambienti del servizio app."
services: app-service
documentationcenter: 
author: stefsch
manager: erikre
editor: 
ms.assetid: 73ce0213-bd3e-4876-b1ed-5ecad4ad5601
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/30/2016
ms.author: stefsch
ms.openlocfilehash: 0627ba6fa849908506fe62c451c888c147cabc03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="implementing-a-layered-security-architecture-with-app-service-environments"></a>Implementazione di un'architettura di sicurezza su più livelli con ambienti del servizio app
## <a name="overview"></a>Overview
Dato che gli ambienti del servizio app forniscono un ambiente di runtime isolato distribuito in una rete virtuale, gli sviluppatori possono creare un'architettura di sicurezza su più livelli offrendo livelli diversi di accesso alla rete per ogni livello applicazione fisico.

Un comune desiderio è toohide API back-end da accesso generale a Internet e consentire solo le API toobe chiamato dall'App web a monte.  [Rete di sicurezza gruppi] [ NetworkSecurityGroups] può essere utilizzato in subnet contenente gli ambienti del servizio App toorestrict accesso pubblico tooAPI applicazioni.

diagramma Hello riportato di seguito è illustrata un'architettura di esempio con un'applicazione WebAPI basata distribuita in un ambiente del servizio App.  Tre istanze di app web separato, distribuite in tre App servizio ambienti separati, effettuare chiamate di back-end toohello WebAPI alla stessa app.

![Architettura concettuale][ConceptualArchitecture] 

i segni più verde Hello indicare tale hello gruppo di sicurezza di rete nella subnet hello contenente "apiase" consente chiamate in ingresso da hello App web a monte, anche se chiamate da se stessa.  Tuttavia, hello stesso gruppo di sicurezza di rete nega esplicitamente l'accesso toogeneral il traffico da Internet hello in ingresso. 

resto Hello di questo argomento vengono illustrati il gruppo di sicurezza rete hello passaggi necessari tooconfigure hello nella subnet hello contenente "apiase".

## <a name="determining-hello-network-behavior"></a>Determinare il comportamento di rete hello
In ordine tooknow quale sia la sicurezza di rete sono necessarie regole, è necessario toodetermine i client di rete che potrà essere tooreach hello ambiente del servizio App contenente hello app per le API e i client che verranno bloccati.

Poiché [sicurezza gruppi di rete] [ NetworkSecurityGroups] sono toosubnets applicate e gli ambienti del servizio App sono distribuiti in subnet, hello contenuti in un gruppo regole troppo**tutti** App in esecuzione in un ambiente del servizio App.  Utilizzando l'architettura di esempio hello per questo articolo, una volta che un gruppo di sicurezza di rete è applicato toohello subnet contenente "apiase", tutte le App in esecuzione su hello "apiase" ambiente del servizio App saranno protetti da hello stesso insieme di regole di sicurezza. 

* **Determinare l'indirizzo IP in uscita hello dei chiamanti upstream:** che cos'è l'indirizzo IP hello o gli indirizzi dei chiamanti upstream hello?  Questi indirizzi saranno necessario toobe esplicitamente consentito l'accesso in hello gruppo.  Poiché le chiamate tra gli ambienti del servizio App vengono considerate chiamate "Internet", ciò significa hello in uscita IP indirizzo assegnato tooeach di hello tre upstream gli ambienti del servizio App esigenze toobe hello gruppo per la subnet "apiase" hello consentito l'accesso.   Per ulteriori informazioni su come determinare l'indirizzo IP in uscita hello per le applicazioni in esecuzione in un ambiente del servizio App, vedere hello [architettura di rete] [ NetworkArchitecture] articolo introduttivo.
* **App per le API back-end hello necessario toocall stesso?**  Un punto sofisticato e talvolta trascurato è uno scenario di hello in cui un'applicazione hello back-end deve toocall stesso.  Se un'applicazione API back-end in un ambiente del servizio App deve toocall stesso, questo viene considerato come una chiamata di "Internet".  Architettura di esempio hello questa funzionalità richiede che consente l'accesso dall'indirizzo IP in uscita di hello di hello "apiase" ambiente del servizio App anche.

## <a name="setting-up-hello-network-security-group"></a>Impostazione di hello il gruppo di sicurezza di rete
Una volta hello set di indirizzi IP in uscita sono noti, hello è tooconstruct un gruppo di sicurezza di rete.  I gruppi di sicurezza di rete possono essere creati sia per le reti virtuali basate su Resource Manager che per le reti virtuali classiche.  Ecco alcuni esempi di Hello mostrano creazione e configurazione di un gruppo in una rete virtuale classica tramite Powershell.

Per l'architettura di esempio hello, ambienti hello si trovano nel centro-meridionali, quindi viene creato un gruppo vuoto in tale area:

    New-AzureNetworkSecurityGroup -Name "RestrictBackendApi" -Location "South Central US" -Label "Only allow web frontend and loopback traffic"

Esplicita consentire innanzitutto regola viene aggiunto per l'infrastruttura di gestione di Azure hello come indicato nell'articolo hello in [il traffico in ingresso] [ InboundTraffic] per gli ambienti del servizio App.

    #Open ports for access by Azure management infrastructure
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW AzureMngmt" -Type Inbound -Priority 100 -Action Allow -SourceAddressPrefix 'INTERNET' -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '454-455' -Protocol TCP

Successivamente, due regole vengono aggiunte tooallow HTTP e HTTPS chiamate da hello prima upstream ambiente del servizio App ("fe1ase").

    #Grant access toorequests from hello first upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe1ase" -Type Inbound -Priority 200 -Action Allow -SourceAddressPrefix '65.52.xx.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe1ase" -Type Inbound -Priority 300 -Action Allow -SourceAddressPrefix '65.52.xx.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

Sciacquare e ripetere l'operazione per hello secondo e terzo upstream App gli ambienti del servizio ("fe2ase" e "fe3ase").

    #Grant access toorequests from hello second upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe2ase" -Type Inbound -Priority 400 -Action Allow -SourceAddressPrefix '191.238.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe2ase" -Type Inbound -Priority 500 -Action Allow -SourceAddressPrefix '191.238.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

    #Grant access toorequests from hello third upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe3ase" -Type Inbound -Priority 600 -Action Allow -SourceAddressPrefix '23.98.abc.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe3ase" -Type Inbound -Priority 700 -Action Allow -SourceAddressPrefix '23.98.abc.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

Infine, concedere accesso toohello indirizzo IP in uscita dell'ambiente del servizio App dell'API di hello back-end in modo che possa chiamare nuovamente in se stessa.

    #Allow apps on hello apiase environment toocall back into itself
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP apiase" -Type Inbound -Priority 800 -Action Allow -SourceAddressPrefix '70.37.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS apiase" -Type Inbound -Priority 900 -Action Allow -SourceAddressPrefix '70.37.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

Nessun altre regole di sicurezza di rete necessario toobe configurato in quanto ogni gruppo include un set di regole predefinite che bloccano l'accesso in ingresso da Internet hello per impostazione predefinita.

elenco completo di Hello delle regole nel gruppo di sicurezza di rete hello è illustrato di seguito.  Si noti come regola, ultimo hello è evidenziato, blocca l'accesso in ingresso da tutti i chiamanti diversi da quelli di cui è stato esplicitamente concesso l'accesso.

![Configurazione del gruppo di sicurezza di rete][NSGConfiguration] 

passaggio finale Hello è la subnet tooapply hello NSG toohello contenente hello "apiase" ambiente del servizio App.  

     #Apply hello NSG toohello backend API subnet
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityGroupToSubnet -VirtualNetworkName 'yourvnetnamehere' -SubnetName 'API-ASE-Subnet'

Con subnet toohello di gruppo applicato hello, hello tre ambienti di servizio App a monte e hello hello contenitore ambiente del servizio App API back-end, sono consentiti solo toocall nell'ambiente "apiase" hello.

## <a name="additional-links-and-information"></a>Informazioni e collegamenti aggiuntivi
Tutti gli articoli e in che modo-per per gli ambienti del servizio App sono disponibili in hello [file Leggimi per gli ambienti del servizio dell'applicazione](../app-service/app-service-app-service-environments-readme.md).

Informazioni sui [gruppi di sicurezza di rete](../virtual-network/virtual-networks-nsg.md). 

Informazioni sugli [indirizzi IP in uscita][NetworkArchitecture] e sugli ambienti del servizio app.

[Porte di rete][InboundTraffic] usate dagli ambienti del servizio app.

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[NetworkArchitecture]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-architecture-overview/
[InboundTraffic]:  https://azure.microsoft.com/en-us/documentation/articles/app-service-app-service-environment-control-inbound-traffic/

<!-- IMAGES -->
[ConceptualArchitecture]: ./media/app-service-app-service-environment-layered-security/ConceptualArchitecture-1.png
[NSGConfiguration]:  ./media/app-service-app-service-environment-layered-security/NSGConfiguration-1.png
