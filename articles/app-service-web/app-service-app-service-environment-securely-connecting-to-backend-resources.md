---
title: aaaSecurely connessione tooBackEnd le risorse da un ambiente del servizio App
description: "Informazioni sulle modalità di connessione toobackend risorse toosecurely da un ambiente del servizio App."
services: app-service
documentationcenter: 
author: stefsch
manager: erikre
editor: 
ms.assetid: f82eb283-a6e7-4923-a00b-4b4ccf7c4b5b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/04/2016
ms.author: stefsch
ms.openlocfilehash: 6311d3fc301512ea3c4ed8f14f268f75755aa415
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="securely-connecting-toobackend-resources-from-an-app-service-environment"></a>In modo sicuro connessione tooBackend le risorse da un ambiente del servizio App
## <a name="overview"></a>Panoramica
Poiché un ambiente del servizio App viene sempre creato nello **entrambi** una rete virtuale di Azure Resource Manager, **o** un modello di distribuzione classica [rete virtuale] [ virtualnetwork], le connessioni in uscita dalle risorse di back-end tooother ambiente del servizio App possono scorrere in modo esclusivo la rete virtuale hello.  Con una modifica recente apportata a giugno 2016, gli ambienti del servizio app possono essere distribuiti nelle reti virtuali che usano intervalli di indirizzi pubblici o spazi di indirizzi RFC1918, ovvero indirizzi privati.  

Ad esempio, potrebbe essere in esecuzione un'istanza di SQL Server in un cluster di macchine virtuali con la porta 1433 bloccata.  endpoint Hello potrebbe essere ACLd tooonly consentire l'accesso da altre risorse nella stessa rete virtuale hello.  

Ad esempio, sensibili endpoint potrebbe essere eseguiti in locale e tooAzure connesso tramite [Site-to-Site] [ SiteToSite] o [Azure ExpressRoute] [ ExpressRoute] connessioni.  Di conseguenza, solo le risorse in reti virtuali connesse toohello Site-to-Site o ExpressRoute tunnel saranno endpoint locali in grado di tooaccess.

Per tutti questi scenari, le App in esecuzione in un ambiente del servizio App verrà essere toosecurely in grado di connettere toohello diversi server e le risorse.  Traffico in uscita da applicazioni in esecuzione in un endpoint dell'ambiente del servizio App tooprivate hello stessa rete virtuale (o connesso toohello stessa rete virtuale), sarà solo flusso in rete virtuale hello.  Il traffico in uscita tooprivate endpoint non trasmetterà su hello rete Internet pubblica.

Un'avvertenza si applica toooutbound traffico da un ambiente del servizio App di tooendpoints all'interno di una rete virtuale.  Gli ambienti del servizio App non può raggiungere l'endpoint delle macchine virtuali presenti nella hello **stesso** subnet come hello ambiente del servizio App.  In genere non deve essere un problema, purché gli ambienti del servizio App vengono distribuiti in una subnet riservata per l'uso esclusivo da solo hello ambiente del servizio App.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="outbound-connectivity-and-dns-requirements"></a>Requisiti per DNS e connettività in uscita
Per un ambiente del servizio App di toofunction correttamente, è necessario endpoint toovarious accesso in uscita. È un elenco completo di endpoint esterni di hello utilizzato da un ASE nella sezione "Necessaria la connettività di rete" di hello hello [configurazione di rete per ExpressRoute](app-service-app-service-environment-network-configuration-expressroute.md#required-network-connectivity) articolo.

Gli ambienti del servizio App richiedono un'infrastruttura DNS valida configurata per la rete virtuale hello.  Se per qualsiasi hello motivo la configurazione del DNS viene modificata dopo aver creato un ambiente del servizio App, gli sviluppatori possono forzare toopick un ambiente del servizio App hello configurazione del nuovo DNS.  Attivazione di un riavvio in sequenza di ambiente facendo clic sull'icona "Riavvia" hello che si trova nella parte superiore di hello di hello ambiente del servizio App Pannello di gestione nel portale di hello causerà hello ambiente toopick hello configurazione del nuovo DNS.

È inoltre consigliabile che qualsiasi server DNS personalizzati in rete virtuale hello è necessario installare prima fase precedente toocreating un ambiente del servizio App.  Se la configurazione DNS della rete virtuale viene modificata durante la creazione di un ambiente del servizio App, si avranno esito negativo processo di creazione dell'ambiente del servizio App di hello.  Infine proposta, se esiste un server DNS personalizzato su hello altra entità finale di un gateway VPN e server DNS hello è hello non è raggiungibile o non disponibile, non sarà possibile eseguire il processo di creazione dell'ambiente del servizio App.

## <a name="connecting-tooa-sql-server"></a>Connessione tooa SQL Server
Una configurazione di SQL Server comune prevede un endpoint in ascolto sulla porta 1433:

![Endpoint di SQL Server][SqlServerEndpoint]

Sono disponibili due approcci per la limitazione dell'endpoint toothis traffico:

* [Elenchi di controllo di accesso di rete][NetworkAccessControlLists] (ACL di rete)
* [Gruppi di sicurezza di rete][NetworkSecurityGroups]

## <a name="restricting-access-with-a-network-acl"></a>Limitazione dell'accesso con un elenco di controllo di accesso di rete
È possibile proteggere la porta 1433 usando un elenco di controllo di accesso di rete.  gli indirizzi di esempio Hello di sotto delle whitelist client provenienti da all'interno di una rete virtuale e blocca l'accesso tooall altri client.

![Esempio di elenco di controllo di accesso di rete (ACL)][NetworkAccessControlListExample]

Tutte le applicazioni in esecuzione nell'ambiente del servizio App in hello stessa rete virtuale di SQL Server hello verrà istanza di SQL Server in grado di tooconnect toohello utilizzando hello **rete virtuale interna** indirizzo IP per la macchina virtuale di SQL Server hello.  

stringa di connessione di esempio Hello sotto riferimenti hello SQL Server tramite il relativo indirizzo IP privato.

    Server=tcp:10.0.1.6;Database=MyDatabase;User ID=MyUser;Password=PasswordHere;provider=System.Data.SqlClient

Anche se macchina virtuale hello include anche un endpoint pubblico, tentativi di connessione tramite indirizzo IP pubblico hello verranno rifiutati a causa di ACL di rete hello. 

## <a name="restricting-access-with-a-network-security-group"></a>Limitazione dell'accesso con un gruppo di sicurezza di rete
In alternativa, per proteggere l'accesso è possibile usare un gruppo di sicurezza di rete.  Gruppi di sicurezza di rete possono essere applicato tooindividual le macchine virtuali, o subnet tooa contenenti macchine virtuali.

Un gruppo di sicurezza di rete deve prima toobe creato:

    New-AzureNetworkSecurityGroup -Name "testNSGexample" -Location "South Central US" -Label "Example network security group for an app service environment"

Limitazione dell'accesso tooonly traffico di rete virtuale interna è molto semplice con un gruppo di sicurezza di rete.  le regole predefinite di Hello in un gruppo di sicurezza di rete consentono l'accesso solo da altri client di rete in hello stessa rete virtuale.

Di conseguenza il blocco di tooSQL accesso Server è semplice come l'applicazione di un gruppo di sicurezza di rete con impostazione predefinita le regole tooeither hello macchine virtuali in esecuzione SQL Server o subnet hello contenenti macchine virtuali hello.

esempio Hello seguente si applica a una subnet contenente toohello della rete sicurezza gruppo:

    Get-AzureNetworkSecurityGroup -Name "testNSGExample" | Set-AzureNetworkSecurityGroupToSubnet -VirtualNetworkName 'testVNet' -SubnetName 'Subnet-1'

risultato finale Hello è un set di regole di sicurezza che bloccano l'accesso esterno, pur consentendo l'accesso di rete virtuale interna:

![Regole di sicurezza di rete predefinite][DefaultNetworkSecurityRules]

## <a name="getting-started"></a>introduttiva
Tutti gli articoli e in che modo-per per gli ambienti del servizio App sono disponibili in hello [file Leggimi per gli ambienti del servizio dell'applicazione](../app-service/app-service-app-service-environments-readme.md).

tooget avviato con gli ambienti del servizio App, vedere [tooApp introduzione dell'ambiente del servizio][IntroToAppServiceEnvironment]

Per informazioni dettagliate sugli controllare il traffico in entrata tooyour ambiente del servizio App, vedere [controllare il traffico in entrata tooan ambiente del servizio App][ControlInboundASE]

Per ulteriori informazioni sulla piattaforma Azure App Service hello, vedere [Azure App Service][AzureAppService].

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[virtualnetwork]: https://azure.microsoft.com/documentation/articles/virtual-networks-faq/
[ControlInboundTraffic]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/
[SiteToSite]: https://azure.microsoft.com/documentation/articles/vpn-gateway-site-to-site-create/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
[NetworkAccessControlLists]: https://azure.microsoft.com/documentation/articles/virtual-networks-acl/
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[IntroToAppServiceEnvironment]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/ 
[ControlInboundASE]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/ 

<!-- IMAGES -->
[SqlServerEndpoint]: ./media/app-service-app-service-environment-securely-connecting-to-backend-resources/SqlServerEndpoint01.png
[NetworkAccessControlListExample]: ./media/app-service-app-service-environment-securely-connecting-to-backend-resources/NetworkAcl01.png
[DefaultNetworkSecurityRules]: ./media/app-service-app-service-environment-securely-connecting-to-backend-resources/DefaultNetworkSecurityRules01.png 
