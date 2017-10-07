---
title: aaaNetwork i dettagli di configurazione per l'utilizzo di Express Route
description: Dettagli di configurazione di rete per l'esecuzione di App gli ambienti del servizio in una rete virtuale connessa tooan circuito ExpressRoute.
services: app-service
documentationcenter: 
author: stefsch
manager: nirma
editor: 
ms.assetid: 34b49178-2595-4d32-9b41-110c96dde6bf
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/14/2016
ms.author: stefsch
ms.openlocfilehash: 85bbc45cfed619485957ee2a898aa0a7604173cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="network-configuration-details-for-app-service-environments-with-expressroute"></a>Dettagli della configurazione di rete per gli ambienti del servizio app con ExpressRoute
## <a name="overview"></a>Panoramica
I clienti possono collegare un [Azure ExpressRoute] [ ExpressRoute] infrastruttura di rete virtuale tootheir circuito, e quindi di estendere i tooAzure di rete locale.  Un ambiente del servizio app può essere creato in una subnet di questa infrastruttura di [rete virtuale][virtualnetwork].  App in esecuzione su hello ambiente del servizio App può quindi stabilire connessioni protette tooback fine risorse accessibili solo tramite hello connessione ExpressRoute.  

Un ambiente del servizio app può essere creato in una rete virtuale di Azure Resource Manager ******o** in una rete virtuale del modello di distribuzione classica.  Con una modifica recente apportata a giugno 2016, gli ambienti del servizio app possono essere distribuiti nelle reti virtuali che usano intervalli di indirizzi pubblici o spazi di indirizzi RFC1918, ovvero indirizzi privati. 

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="required-network-connectivity"></a>Requisiti della connettività di rete
Esistono requisiti di connettività di rete per gli ambienti del servizio App che non può essere soddisfatto inizialmente in tooan una rete virtuale connessa ExpressRoute.  Gli ambienti del servizio App richiedono tutti hello seguenti nell'ordine toofunction correttamente:

* In uscita connettività tooAzure archiviazione gli endpoint di rete in tutto il mondo in entrambe le porte 80 e 443.  Sono inclusi gli endpoint si trova in hello stessa area hello ambiente del servizio App, nonché gli endpoint di archiviazione si trova **altri** aree di Azure.  Endpoint di archiviazione Azure risolvere in hello seguenti domini DNS: *t*, *>.BLOB.Core.Windows.NET*, *queue.core.windows.net* e *file.core.windows.net*.  
* Toohello di connettività di rete in uscita del servizio file di Azure sulla porta 445.
* Gli endpoint tooSql DB di connettività di rete in uscita si trovano in hello stessa area, come hello ambiente del servizio App.  Risolvere gli endpoint di database di SQL Server in seguito dominio hello: *database.windows.net*.  Ciò comporta l'apertura di accesso tooports 1433, 11000 11999 e 14000 14999.  Per altri dettagli, vedere [questo articolo sull'uso delle porte per il database SQL versione 12](../sql-database/sql-database-develop-direct-route-ports-adonet-v12.md).
* In uscita connettività toohello gestione di Azure piano gli endpoint di rete (endpoint sia ASM e ARM).  Ciò include la connettività in uscita tooboth *management.core.windows.net* e *management.azure.com*. 
* In uscita connettività di rete troppo*ocsp.msocsp.com*, *mscrl.microsoft.com* e *crl.microsoft.com*.  Si tratta di funzionalità SSL toosupport necessari.
* configurazione del DNS per la rete virtuale hello Hello deve essere in grado di risolvere tutti gli endpoint hello e domini indicati hello punti precedenti.  Se questi endpoint non possono essere risolti, il tentativo di creazione dell’ambiente del servizio App avrà esito negativo, e gli ambienti del servizio App esistenti verranno contrassegnati come non integri.
* L'accesso in uscita sulla porta 53 è necessario per la comunicazione con i server DNS.
* Se esiste un server DNS personalizzato su hello altra entità finale di un gateway VPN, server DNS hello deve essere raggiungibile dalla subnet hello contenente hello ambiente del servizio App. 
* percorso di rete in uscita Hello non è possibile attraversare proxy aziendale interno, né può essere force tunneled tooon locale.  In tal modo le modifiche hello indirizzo NAT effettiva del traffico di rete in uscita da hello ambiente del servizio App.  Modifica dell'indirizzo NAT hello di traffico di rete in uscita dell'ambiente del servizio App causerà connettività toomany errori di endpoint hello elencate in precedenza.  Ciò comporta dei tentativi non riusciti nella creazione dell’ambiente di servizio app, così come il fatto che ambienti di servizio app che prima erano integri vengano contrassegnati come non integri.  
* Porte di toorequired accesso di rete in ingresso per gli ambienti del servizio App devono essere consentiti come descritto in questo [articolo][requiredports].

i requisiti DNS Hello possono essere soddisfatto garantendo un'infrastruttura DNS valida viene configurata e gestita per la rete virtuale hello.  Se per qualsiasi hello motivo la configurazione del DNS viene modificata dopo aver creato un ambiente del servizio App, gli sviluppatori possono forzare toopick un ambiente del servizio App hello configurazione del nuovo DNS.  Attivazione di un riavvio di ambiente in sequenza utilizzando hello icona "Riavvia" si trova nella parte superiore di hello del pannello Gestione di ambiente del servizio App hello in hello [portale di Azure] [ NewPortal] causerà hello ambiente toopick la nuova configurazione DNS di hello.

Hello i requisiti di accesso di rete in ingresso possono essere soddisfatto mediante la configurazione di un [il gruppo di sicurezza di rete] [ NetworkSecurityGroups] dell'ambiente del servizio App di hello subnet tooallow hello richiesto l'accesso come descritto in questo [articolo][requiredports].

## <a name="enabling-outbound-network-connectivity-for-an-app-service-environment"></a>Abilitazione della connettività di rete in uscita per un ambiente del servizio app
Per impostazione predefinita, un circuito ExpressRoute appena creato annuncia una route predefinita che consente la connettività Internet in uscita.  Con questa configurazione di un ambiente del servizio App sarà in grado di tooconnect tooother endpoint di Azure.

Tuttavia una configurazione personalizzata comune è toodefine i propri route predefinita (0.0.0.0/0) impone in uscita Internet tooinstead il flusso del traffico locale.  Questo flusso di traffico interrompe sempre gli ambienti del servizio App perché il traffico in uscita hello è bloccato in locale o NAT certificati tooan Impossibile riconoscere gli indirizzi che non funzionano con vari endpoint di Azure.

soluzione hello è toodefine (più) il route definite dall'utente (UDRs) nella subnet hello contenente hello ambiente del servizio App.  Un UDR definisce le route di subnet specifiche che verranno utilizzato il valore anziché route predefinita hello.

Se possibile, è consigliabile hello toouse seguente configurazione:

* configurazione di ExpressRoute Hello annuncia 0.0.0.0/0 e per impostazione predefinita force tunnel tutto il traffico in uscita in locale.
* Hello UDR applicato toohello subnet contenente hello ambiente del servizio App definisce 0.0.0.0/0 con un tipo di hop successivo di Internet (un esempio di questo oggetto è più basso in questo articolo).

Hello effetto combinato di questi passaggi è che il livello di subnet hello UDR avrà la precedenza su hello garantendo l'accesso a Internet in uscita da hello ambiente del servizio App, tunneling forzato ExpressRoute.

> [!IMPORTANT]
> Hello route definite in un UDR **deve** essere sufficientemente specifica troppo hanno la precedenza su tutte le route annunciate da hello configurazione ExpressRoute.  esempio Hello seguente utilizza l'intervallo di indirizzi 0.0.0.0/0 ampie hello e di conseguenza possa accidentalmente sottoposto a override dagli annunci della route utilizzando più specifici intervalli di indirizzi.
> 
> Gli ambienti del servizio App non sono supportati con le configurazioni di ExpressRoute che **cross-annunciare le route da hello peering percorso toohello privata percorso di peering pubblico**.  Le configurazioni di ExpressRoute che dispongono di peering pubblico configurato, riceveranno gli annunci di route da Microsoft per un elevato numero di intervalli di indirizzi IP di Microsoft Azure.  Se questi intervalli di indirizzi tra annunciati nel percorso di peering privato hello, risultato finale hello è che tutti i pacchetti di rete in uscita dalla subnet dell'hello ambiente del servizio App infrastruttura di rete locale del cliente tooa il tunneling forzato.  Questo flusso di rete non è attualmente supportato con ambienti del servizio app.  Un problema di toothis soluzione è toostop le route tra annunci hello peering percorso toohello privata percorso di peering pubblico.
> 
> 

Le informazioni generali sulle route definite dall'utente sono disponibili in questa [panoramica][UDROverview].  

Dettagli sulla creazione e configurazione delle route definite dall'utente è disponibile in questa [come tooGuide][UDRHowTo].

## <a name="example-udr-configuration-for-an-app-service-environment"></a>Esempio di configurazione UDR per un ambiente del servizio app
**Prerequisiti**

1. Installare Azure Powershell da hello [pagina di download di Azure] [ AzureDownloads] (datato giugno 2015 o versione successiva).  In "Strumenti da riga di comando" è un collegamento "Installa" in "Windows Powershell" che consentirà di installare i cmdlet di Powershell più recenti hello.
2. È consigliabile creare una subnet univoca da usare esclusivamente in un ambiente del servizio app.  In questo modo hello UDRs applicato toohello subnet verrà aperta solo il traffico in uscita per hello ambiente del servizio App.
3. **Importante**: non distribuire hello ambiente del servizio App finché **dopo** hello seguendo i passaggi di configurazione viene seguito.  Ciò garantisce che la connettività di rete in uscita sia disponibile prima di tentare di toodeploy un ambiente del servizio App.

**Passaggio 1: Creare una tabella di route denominata**

Hello frammento di codice seguente crea una tabella di route denominata "DirectInternetRouteTable" regione occidentale ci Azure hello:

    New-AzureRouteTable -Name 'DirectInternetRouteTable' -Location uswest

**Passaggio 2: Creare una o più route nella tabella di route hello**

Sarà necessario tooadd uno o più route toohello RouteTable in ordine tooenable in uscita l'accesso a Internet.  

Hello consigliabile approccio per la configurazione dell'accesso in uscita toohello che Internet è toodefine una route per 0.0.0.0/0 come mostrato di seguito.

    Get-AzureRouteTable -Name 'DirectInternetRouteTable' | Set-AzureRoute -RouteName 'Direct Internet Range 0' -AddressPrefix 0.0.0.0/0 -NextHopType Internet

Ricordare che 0.0.0.0/0 è un intervallo di indirizzi generali e di conseguenza verrà sostituito dal più specifici intervalli di indirizzi annunciati da hello ExpressRoute.  toore-eseguire l'iterazione hello consigliato in precedenza, un UDR con una route 0.0.0.0/0 deve essere utilizzato in combinazione con una configurazione ExressRoute che ne annuncia solo nonché 0.0.0.0/0. 

In alternativa, è possibile scaricare un elenco completo e aggiornato di intervalli CIDR utilizzato da Azure.  Hello file Xml contenente tutti gli intervalli di indirizzi IP Azure hello è disponibile da hello [Microsoft Download Center][DownloadCenterAddressRanges].  

Si noti tuttavia che questi intervalli cambiano nel tempo, è necessario eseguire aggiornamenti manuali periodica toohello definito dall'utente tookeep route sincronizzati.  Inoltre, poiché non esiste valore predefinito è superiore toofit entro il limite di route hello 100 intervalli di limite di 100 route in un singolo UDR, è necessario troppo "riepiloga" indirizzo IP di Azure hello, tenendo presente che UDR route definite necessario toobe più specifiche rispetto alle route hello annunciate dal ExpressRoute.  

**Passaggio 3: Associare hello route tabella toohello subnet contenente hello ambiente del servizio App**

ultimo passaggio di configurazione Hello è la subnet toohello tooassociate hello route nella tabella in cui verrà distribuito hello ambiente del servizio App.  Hello comando che segue associa toohello "DirectInternetRouteTable" hello "ASESubnet" che alla fine conterrà un ambiente del servizio App.

    Set-AzureSubnetRouteTable -VirtualNetworkName 'YourVirtualNetworkNameHere' -SubnetName 'ASESubnet' -RouteTableName 'DirectInternetRouteTable'


**Passaggio 4: Procedura finale**

Una volta la tabella di route hello subnet toohello associato, è consigliabile toofirst test e lo conferma hello destinato effetto.  Ad esempio, distribuire una macchina virtuale nella subnet hello e verificare che:

* Il traffico in uscita tooboth Azure e gli endpoint di Azure non indicato in precedenza in questo articolo è **non** flusso verso il basso hello circuito ExpressRoute.  È molto importante tooverify questo comportamento, in quanto se il traffico in uscita dalla subnet hello è ancora viene forzato il tunneling in locale, la creazione dell'ambiente del servizio App verrà sempre esito negativo. 
* Le ricerche DNS per gli endpoint hello citato in precedenza sono tutti risolvere correttamente. 

Quando vengono confermate hello sopra passaggi, sarà necessario macchina virtuale di hello toodelete perché subnet hello deve toobe "vuoto" in hello ora hello che viene creato l'ambiente del servizio App.

Procedere quindi con la creazione di un ambiente di servizio app.

## <a name="getting-started"></a>introduttiva
Tutti gli articoli e in che modo-per per gli ambienti del servizio App sono disponibili in hello [file Leggimi per gli ambienti del servizio dell'applicazione](../app-service/app-service-app-service-environments-readme.md).

tooget avviato con gli ambienti del servizio App, vedere [tooApp introduzione dell'ambiente del servizio][IntroToAppServiceEnvironment]

Per ulteriori informazioni sulla piattaforma Azure App Service hello, vedere [Azure App Service][AzureAppService].

<!-- LINKS -->
[virtualnetwork]: http://azure.microsoft.com/services/virtual-network/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
[requiredports]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/
[NetworkSecurityGroups]: http://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[UDROverview]: http://azure.microsoft.com/documentation/articles/virtual-networks-udr-overview/
[UDRHowTo]: http://azure.microsoft.com/documentation/articles/virtual-networks-udr-how-to/
[HowToCreateAnAppServiceEnvironment]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-an-app-service-environment/
[AzureDownloads]: http://azure.microsoft.com/en-us/downloads/ 
[DownloadCenterAddressRanges]: http://www.microsoft.com/download/details.aspx?id=41653  
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/
[IntroToAppServiceEnvironment]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[NewPortal]:  https://portal.azure.com


<!-- IMAGES -->
