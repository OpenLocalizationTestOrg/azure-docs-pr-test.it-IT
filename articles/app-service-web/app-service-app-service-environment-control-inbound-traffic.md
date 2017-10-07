---
title: aaaHow tooControl il traffico in ingresso tooan ambiente del servizio App
description: Informazioni su come tooconfigure rete sicurezza regole toocontrol in ingresso a traffico tooan ambiente del servizio App.
services: app-service
documentationcenter: 
author: ccompy
manager: erikre
editor: 
ms.assetid: 4cc82439-8791-48a4-9485-de6d8e1d1a08
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2017
ms.author: stefsch
ms.openlocfilehash: e7c6e6201db6a1ea77f7a2eee29a3b5445175495
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocontrol-inbound-traffic-tooan-app-service-environment"></a>Come tooControl il traffico in ingresso tooan ambiente del servizio App
## <a name="overview"></a>Panoramica
Un ambiente del servizio app può essere creato **o** in una rete virtuale di Azure Resource Manager **o** in una [rete virtuale][virtualnetwork] del modello di distribuzione classica.  È possibile definire una nuova rete virtuale e una nuova subnet in fase di hello che viene creato un ambiente del servizio App.  In alternativa, è possibile creare un ambiente del servizio app in una rete virtuale e in una subnet preesistenti.  Con una modifica apportata a giugno 2016, gli ambienti del servizio app possono essere distribuiti nelle reti virtuali che usano intervalli di indirizzi pubblici o spazi di indirizzi RFC1918 (ovvero indirizzi privati).  Per ulteriori informazioni sulla creazione di un ambiente del servizio App vedere [come un ambiente del servizio App tooCreate][HowToCreateAnAppServiceEnvironment].

Un ambiente del servizio App deve sempre essere creato all'interno di una subnet perché una subnet offre un limite di rete che può essere utilizzato toolock verso il basso il traffico in entrata dietro a monte dispositivi e servizi in modo che il traffico HTTP e HTTPS è accettato solo da specifici a monte Indirizzi IP.

Il traffico in ingresso e in uscita diretto verso e proveniente da una subnet è controllato tramite un [gruppo di sicurezza di rete][NetworkSecurityGroups]. Controllare il traffico in entrata richiede la creazione di regole di sicurezza di rete in un gruppo di sicurezza di rete e quindi assegnando hello rete sicurezza gruppo hello subnet contenente hello ambiente del servizio App.

Una volta assegnato un gruppo di sicurezza di rete tooa subnet, il traffico in entrata tooapps nell'ambiente del servizio App è consentita o bloccata in base alle hello hello di negazione e assenso regole definite nel gruppo di sicurezza di rete hello.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="inbound-network-ports-used-in-an-app-service-environment"></a>Porte di rete in ingresso usate in un ambiente del servizio app
Prima di bloccare il traffico di rete in ingresso con un gruppo di sicurezza di rete, è importante tooknow set di hello delle porte di rete obbligatorie e facoltative utilizzate da un ambiente del servizio App.  Chiude involontariamente off porte toosome traffico può comportare la perdita di funzionalità in un ambiente del servizio App.

Hello seguito è riportato un elenco delle porte utilizzate da un ambiente del servizio App. Tutte le porte sono di tipo **TCP**, se non indicato diversamente in modo chiaro:

* 454: **porta obbligatoria** usata dall'infrastruttura di Azure per la gestione e la manutenzione degli ambienti del servizio app tramite SSL.  Non bloccano la porta toothis traffico.  Questa porta è sempre associato toohello VIP pubblico di un tipo di base.
* 455: **porta obbligatoria** usata dall'infrastruttura di Azure per la gestione e la manutenzione degli ambienti del servizio app tramite SSL.  Non bloccano la porta toothis traffico.  Questa porta è sempre associato toohello VIP pubblico di un tipo di base.
* 80: porta per tooapps di traffico HTTP in ingresso e in esecuzione in piani di servizio App in un ambiente del servizio App predefinita.  In un ASE abilitata al bilanciamento del carico interno, questa porta è hello ASE indirizzo ILB toohello associato.
* 443: porta per tooapps di traffico SSL in ingresso e in esecuzione in piani di servizio App in un ambiente del servizio App predefinita.  In un ASE abilitata al bilanciamento del carico interno, questa porta è hello ASE indirizzo ILB toohello associato.
* 21: canale di controllo per il servizio FTP.  Questa porta può essere bloccata, se non si usa un servizio FTP.  In un ASE abilitata al bilanciamento del carico interno, questa porta può essere indirizzi di bilanciamento del carico interno toohello associato per un tipo di base.
* 990: canale di controllo per il servizio FTPS.  Questa porta può essere bloccata, se non si usa un servizio FTPS.  In un ASE abilitata al bilanciamento del carico interno, questa porta può essere indirizzi di bilanciamento del carico interno toohello associato per un tipo di base.
* 10001-10020: canali di dati per il servizio FTP.  Come con il canale di controllo di hello, queste porte possono essere bloccate in modo sicuro se non viene utilizzato FTP.  In un ASE abilitata al bilanciamento del carico interno, questa porta può essere associato toohello dell'ASE indirizzo di bilanciamento del carico interno.
* 4016: porta usata per il debug remoto con Visual Studio 2012.  Questa porta può essere bloccata in modo sicuro se non viene utilizzata la funzione hello.  In un ASE abilitata al bilanciamento del carico interno, questa porta è hello ASE indirizzo ILB toohello associato.
* 4018: porta usata per il debug remoto con Visual Studio 2013.  Questa porta può essere bloccata in modo sicuro se non viene utilizzata la funzione hello.  In un ASE abilitata al bilanciamento del carico interno, questa porta è hello ASE indirizzo ILB toohello associato.
* 4020: porta usata per il debug remoto con Visual Studio 2015.  Questa porta può essere bloccata in modo sicuro se non viene utilizzata la funzione hello.  In un ASE abilitata al bilanciamento del carico interno, questa porta è hello ASE indirizzo ILB toohello associato.

## <a name="outbound-connectivity-and-dns-requirements"></a>Requisiti per DNS e connettività in uscita
Per un ambiente del servizio App di toofunction correttamente, è inoltre necessario endpoint toovarious accesso in uscita. È un elenco completo di endpoint esterni di hello utilizzato da un ASE nella sezione "Necessaria la connettività di rete" di hello hello [configurazione di rete per ExpressRoute](app-service-app-service-environment-network-configuration-expressroute.md#required-network-connectivity) articolo.

Gli ambienti del servizio App richiedono un'infrastruttura DNS valida configurata per la rete virtuale hello.  Se per qualsiasi hello motivo la configurazione del DNS viene modificata dopo aver creato un ambiente del servizio App, gli sviluppatori possono forzare toopick un ambiente del servizio App hello configurazione del nuovo DNS.  Attivazione di un riavvio di ambiente in sequenza utilizzando hello icona "Riavvia" si trova nella parte superiore di hello del pannello Gestione di ambiente del servizio App hello in hello [portale di Azure] [ NewPortal] causerà hello ambiente toopick la nuova configurazione DNS di hello.

È inoltre consigliabile che qualsiasi server DNS personalizzati in rete virtuale hello è necessario installare prima fase precedente toocreating un ambiente del servizio App.  Se la configurazione DNS della rete virtuale viene modificata durante la creazione di un ambiente del servizio App, si avranno esito negativo processo di creazione dell'ambiente del servizio App di hello.  Infine proposta, se esiste un server DNS personalizzato su hello altra entità finale di un gateway VPN e server DNS hello è hello non è raggiungibile o non disponibile, non sarà possibile eseguire il processo di creazione dell'ambiente del servizio App.

## <a name="creating-a-network-security-group"></a>Creazione di un gruppo di sicurezza di rete
Per ottenere informazioni complete sulla sicurezza di rete come gruppi di lavoro, vedere esempio hello [informazioni][NetworkSecurityGroups].  esempio di gestione del servizio Azure Hello seguito ritocchi su Evidenzia dei gruppi di sicurezza di rete, con l'obiettivo di configurazione e applicazione di una subnet di tooa gruppo di sicurezza rete che contiene un ambiente del servizio App.

**Nota:** gruppi di sicurezza di rete possono essere configurati tramite graficamente hello [portale Azure](https://portal.azure.com) o tramite Azure PowerShell.

I gruppi di sicurezza di rete vengono inizialmente creati come un'entità autonoma associata a una sottoscrizione. Poiché in un'area di Azure vengono creati gruppi di sicurezza di rete, verificare che tale gruppo di sicurezza di rete hello viene creato in hello stessa area, come hello ambiente del servizio App.

esempio Hello viene illustrata la creazione di un gruppo di sicurezza di rete:

    New-AzureNetworkSecurityGroup -Name "testNSGexample" -Location "South Central US" -Label "Example network security group for an app service environment"

Dopo aver creato un gruppo di sicurezza di rete, uno o più regole di sicurezza di rete vengono aggiunti tooit.  Poiché set hello di regole potrebbe cambiare nel tempo, è consigliabile toospace out hello schema di numerazione utilizzata per regola priorità toomake regole aggiuntive tooinsert facilmente nel tempo.

esempio Hello riportato di seguito è illustrata una regola che concede porte gestione toohello di accesso necessari per hello toomanage di infrastruttura di Azure e gestione un ambiente del servizio App in modo esplicito.  Si noti che tutto il traffico di gestione flussi tramite SSL ed è protetto dai certificati client, pertanto anche se hello porte siano aperte sono inaccessibili da qualsiasi entità diversa da infrastruttura di gestione di Azure.

    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityRule -Name "ALLOW AzureMngmt" -Type Inbound -Priority 100 -Action Allow -SourceAddressPrefix 'INTERNET'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '454-455' -Protocol TCP


Quando il blocco di accesso tooport 80 e 443 troppo "hide" un ambiente del servizio App dietro a monte dispositivi o servizi, sarà necessario indirizzo IP di tooknow hello a monte.  Ad esempio, se si utilizza un firewall applicazione web (WAF), hello WAF avrà il proprio indirizzo IP (o gli indirizzi) che verrà utilizzato quando l'inoltro dei dati del traffico tooa downstream ambiente del servizio App.  Sarà necessario toouse questo indirizzo IP in hello *SourceAddressPrefix* parametro di una regola di sicurezza di rete.

Nell'esempio hello seguente, è consentito in modo esplicito il traffico in ingresso da uno specifico indirizzo IP a monte.  Hello indirizzo *1.2.3.4* viene utilizzato come segnaposto per indirizzo IP hello di un WAF a monte.  Modificare l'indirizzo di hello valore toomatch hello utilizzato da un dispositivo a monte o di un servizio.

    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityRule -Name "RESTRICT HTTP" -Type Inbound -Priority 200 -Action Allow -SourceAddressPrefix '1.2.3.4/32'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityRule -Name "RESTRICT HTTPS" -Type Inbound -Priority 300 -Action Allow -SourceAddressPrefix '1.2.3.4/32'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

Se si desidera supporto FTP, hello segue le regole può essere utilizzato come una porta di controllo modello toogrant accesso toohello FTP e porte canale dati.  Poiché FTP è un protocollo di stato, potrebbe non essere in grado di tooroute FTP traffico tramite un dispositivo firewall o proxy HTTP/HTTPS tradizionale.  In questo caso sarà necessario hello tooset *SourceAddressPrefix* tooa valore diverso, ad esempio hello IP indirizzo serie di computer di sviluppo o distribuzione su FTP client in esecuzione. 

    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityRule -Name "RESTRICT FTPCtrl" -Type Inbound -Priority 400 -Action Allow -SourceAddressPrefix '1.2.3.4/32'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '21' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityRule -Name "RESTRICT FTPDataRange" -Type Inbound -Priority 500 -Action Allow -SourceAddressPrefix '1.2.3.4/32'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '10001-10020' -Protocol TCP

(**Nota:** intervallo porte canale dati di hello potrebbe cambiare durante il periodo di anteprima di hello.)

Se viene utilizzato il debug remoto con Visual Studio, hello seguendo regole viene illustrato come accedere a toogrant.  Esiste una regola separata per ogni versione supportata di Visual Studio, dal momento che ogni versione usa una porta diversa per il debug remoto.  Come per l'accesso FTP, il traffico di debug remoto potrebbe non transitare correttamente attraverso un dispositivo proxy o un firewall per applicazioni Web tradizionale.  Hello *SourceAddressPrefix* possono invece essere impostate toohello intervallo di indirizzi IP del computer di sviluppo che esegue Visual Studio.

    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityRule -Name "RESTRICT RemoteDebuggingVS2012" -Type Inbound -Priority 600 -Action Allow -SourceAddressPrefix '1.2.3.4/32'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '4016' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityRule -Name "RESTRICT RemoteDebuggingVS2013" -Type Inbound -Priority 700 -Action Allow -SourceAddressPrefix '1.2.3.4/32'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '4018' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityRule -Name "RESTRICT RemoteDebuggingVS2015" -Type Inbound -Priority 800 -Action Allow -SourceAddressPrefix '1.2.3.4/32'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '4020' -Protocol TCP

## <a name="assigning-a-network-security-group-tooa-subnet"></a>L'assegnazione di una Subnet di tooa il gruppo di sicurezza di rete
Un gruppo di sicurezza di rete dispone di una regola di sicurezza predefinita che nega il traffico esterno tooall di accesso.  risultati tramite la combinazione di regole di sicurezza di rete hello descritte in precedenza, Hello e hello regola di sicurezza predefinita che bloccano il traffico in ingresso, che solo il traffico da intervalli di indirizzi di origine è associato un *Consenti* sarà in grado di azione toosend tooapps di traffico in esecuzione in un ambiente del servizio App.

Dopo un gruppo di sicurezza di rete viene popolato con le regole di sicurezza, è necessario toobe assegnato toohello subnet contenente hello ambiente del servizio App.  comando assegnazione Hello fa riferimento sia nome hello della rete virtuale di hello in cui si trova hello ambiente del servizio App, nonché il nome di hello della subnet di hello in cui è stato creato hello ambiente del servizio App.  

esempio Hello riportato di seguito viene illustrato un gruppo di sicurezza di rete viene assegnato tooa subnet e la rete virtuale:

    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityGroupToSubnet -VirtualNetworkName 'testVNet' -SubnetName 'Subnet-test'

Al termine dell'assegnazione del gruppo di sicurezza rete hello (assegnazione hello è operazioni a esecuzione prolungata e può richiedere alcuni minuti toocomplete), solo connessioni in entrata corrispondenti traffico *Consenti* regole completato raggiungerà App in App hello Ambiente del servizio.

Per hello completezza l'esempio seguente viene illustrato come associare DIS hello rete sicurezza tooremove e pertanto gruppo dalla subnet hello:

    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Remove-AzureNetworkSecurityGroupFromSubnet -VirtualNetworkName 'testVNet' -SubnetName 'Subnet-test'

## <a name="special-considerations-for-explicit-ip-ssl"></a>Considerazioni speciali su IP SSL esplicito
Se un'app è configurata con un indirizzo IP SSL esplicito (applicabile *solo* tooASEs che hanno un VIP pubblico), anziché l'indirizzo IP predefinito di hello di hello ambiente del servizio App, HTTP e HTTPS traffico flussi in subnet hello su un set diverso di porte diverse porte 80 e 443.

coppia di singoli Hello delle porte utilizzate da ogni indirizzo IP SSL è reperibile nell'interfaccia utente del portale hello dal pannello UX di dettagli dell'ambiente del servizio App di hello.  Selezionare "Tutte le impostazioni" --> "Indirizzi IP".  Pannello Hello "indirizzi IP" Mostra una tabella di tutti gli indirizzi IP SSL configurati in modo esplicito per hello ambiente del servizio App, insieme a hello porta speciale coppia tooroute utilizzato traffico HTTP e HTTPS associata a ogni indirizzo IP SSL.  È questa coppia di porta che deve toobe utilizzato per i parametri DestinationPortRange hello durante la configurazione di regole in un gruppo di sicurezza di rete.

Quando un'app su un ASE è toouse configurato SSL IP, clienti esterni non saranno visibile e non è necessario tooworry sul mapping di coppia porta speciale hello.  App toohello il traffico verrà trasferito in genere indirizzo IP SSL toohello configurato.  coppia di porte speciali di Hello traduzione toohello automaticamente avviene internamente durante la parte finale di hello di routing del traffico in hello contenente subnet di hello ASE. 

## <a name="getting-started"></a>introduttiva
tooget avviato con gli ambienti del servizio App, vedere [tooApp introduzione dell'ambiente del servizio][IntroToAppServiceEnvironment]

Tutti gli articoli e in che modo-per per gli ambienti del servizio App sono disponibili in hello [file Leggimi per gli ambienti del servizio dell'applicazione](../app-service/app-service-app-service-environments-readme.md).

Per informazioni dettagliate sugli App che si connettono in modo sicuro toobackend risorse da un ambiente del servizio App, vedere [connessione in modo sicuro le risorse tooBackend da un ambiente del servizio App][SecurelyConnecttoBackend]

Per ulteriori informazioni sulla piattaforma Azure App Service hello, vedere [Azure App Service][AzureAppService].

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[virtualnetwork]: https://azure.microsoft.com/documentation/articles/virtual-networks-faq/
[HowToCreateAnAppServiceEnvironment]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-an-app-service-environment/
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/
[IntroToAppServiceEnvironment]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[SecurelyConnecttoBackend]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-securely-connecting-to-backend-resources/
[NewPortal]:  https://portal.azure.com  

<!-- IMAGES -->

