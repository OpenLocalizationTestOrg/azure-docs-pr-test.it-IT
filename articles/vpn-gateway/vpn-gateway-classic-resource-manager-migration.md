---
title: aaaVPN Gateway classico tooResource migrazione Manager | Documenti Microsoft
description: Questa pagina viene fornita una panoramica di hello VPN Gateway classico tooResource migrazione di gestione.
documentationcenter: na
services: vpn-gateway
author: amsriva
manager: rossort
editor: amsriva
ms.assetid: caa8eb19-825a-4031-8b49-18fbf3ebc04e
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/02/2017
ms.author: amsriva
ms.openlocfilehash: c1d84bf5315224c5c8faac53d7957b496ed205ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="vpn-gateway-classic-tooresource-manager-migration"></a>Gateway VPN classico tooResource migration Manager
Gateway VPN possono ora essere migrati da tooResource classico modello di distribuzione di gestione. Altre informazioni su [funzionalità e vantaggi di Azure Resource Manager](../azure-resource-manager/resource-group-overview.md). In questo articolo è descrivere in dettaglio come toomigrate da distribuzioni classico toonewer Gestione risorse basato sul modello. 

Gateway VPN vengono migrate come parte della migrazione di rete virtuale da classico tooResource Manager. Viene eseguita la migrazione di una rete virtuale alla volta. Non è necessario aggiuntivo in termini di toomigration strumenti o i prerequisiti. I passaggi della migrazione sono identici tooexisting la migrazione di rete virtuale e sono documentati in [pagina migrazione di risorse IaaS](../virtual-machines/windows/migration-classic-resource-manager-ps.md). È presente alcun tempo di inattività di percorso di dati durante la migrazione e pertanto i carichi di lavoro esistente continua a toofunction senza perdita di connettività locale durante la migrazione. indirizzo IP pubblico Hello associata al gateway VPN hello rimane invariato durante il processo di migrazione hello. Ciò implica che non è necessario tooreconfigure il router locale dopo aver eseguita la migrazione di hello.  

il modello di Hello in Gestione risorse è diverso dal modello classico ed è composto da gateway di rete virtuale, gateway di rete locale e le risorse di connessione. Questi rappresentano i gateway VPN hello stesso, hello che rappresentano rispettivamente su spazio degli indirizzi locale e la connettività tra hello due siti locali. Dopo il completamento della migrazione, i gateway non saranno disponibili nel modello classico e tutte le operazioni di gestione nei gateway di rete virtuale, nei gateway di rete locale e gli oggetti di connessione devono essere eseguite usando il modello Resource Manager.

## <a name="supported-scenarios"></a>Scenari supportati
Più comuni scenari di connettività VPN rientrano tooResource classico migrazione di gestione. gli scenari di Hello supportato includono:

* Connettività toosite punto
* Connettività toosite con Gateway VPN da sito connesso sede locale tooon
* Connettività di rete virtuale tooVNet tra due reti virtuali mediante gateway VPN
* Più reti virtuali connesse toosame nel percorso locale
* Connessione multisito
* Reti virtuali abilitate per il tunneling forzato

Gli scenari non supportati includono:  

* La rete virtuale con il gateway ExpressRoute e Gateway VPN al momento non è supportata.
* Scenari di transito in cui le estensioni VM sono i server connessi tooon locale. Le limitazioni relative alla connettività VPN di transito sono descritte di seguito.

> [!NOTE]
> Convalida CIDR nel modello di gestione risorse è più rigida hello uno nel modello classico. Prima della migrazione di garantire che gli intervalli di indirizzi classico specificati conformità formato CIDR toovalid prima di iniziare la migrazione di hello. È possibile convalidare CIDR usando qualsiasi validator CIDR comune. La rete virtuale o i siti locali con intervalli CIDR non validi durante la migrazione generano uno stato di errore.
> 
> 

## <a name="vnet-toovnet-connectivity-migration"></a>Migrazione di connettività di rete virtuale tooVNet
Connettività di rete virtuale tooVNet classica è stata ottenuta tramite la creazione di un sito locale rappresentazione hello connessi a reti virtuali. I clienti sono stati necessari toocreate due siti locali rappresentato hello due reti virtuali necessarie toobe connesse tra loro. Questi sono stati quindi connesso toohello corrispondente reti virtuali con connettività di tooestablish tunnel IPsec tra due reti virtuali hello. Questo modello ha problemi di gestibilità in quanto le modifiche di intervallo di indirizzi in una rete virtuale devono anche essere mantenute nella rappresentazione di hello corrispondente sito locale. Nel modello Resource Manager questa soluzione non è più necessaria. connessione Hello tra due reti virtuali possono essere direttamente hello ottenuta usando il tipo di connessione 'Vnet2Vnet' nella risorsa di connessione. 

![Migrazione tooVNet schermata della rete virtuale.](./media/vpn-gateway-migration/migration1.png)

Durante la migrazione di rete virtuale è rilevare che hello entità connessa gateway VPN della rete virtuale toocurrent un'altra rete virtuale e verificare che al termine della migrazione di entrambe le reti virtuali, non sarà più visualizzato due siti locali che rappresenta hello altra rete virtuale. il modello classico di Hello di due gateway VPN, i due siti locali e due connessioni tra di essi è trasformato tooResource modello di gestione con due gateway VPN e due connessioni di tipo Vnet2Vnet.

## <a name="transit-vpn-connectivity"></a>Connettività VPN di transito
È possibile configurare un gateway VPN in una topologia in modo che la connettività locale per una rete virtuale viene ottenuta tramite la connessione di rete virtuale che è direttamente connessi tooon locale tooanother. Si tratta di transito connettività VPN in cui le istanze nella rete virtuale prima sono risorse connessi tooon locale tramite gateway VPN toohello di transito nella rete virtuale connessa che è direttamente connessi tooon locale. tooachieve questa configurazione nel modello di distribuzione classica, occorre toocreate un sito locale che dispone di aggregati di prefissi che rappresenta entrambi spazio indirizzo hello connesso in locale e di rete virtuale. Questo sito locale representational è connettività di transito connesso toohello tooachieve di rete virtuale. Il modello classico presenta problemi di gestibilità simili poiché qualsiasi modifica intervallo di indirizzi locali debba essere gestito anche nel sito locale di hello che rappresenta aggregazione hello di rete virtuale e in locale. L'introduzione del supporto BGP nel gateway di gestione di risorse supportati semplifica la gestibilità poiché hello gateway connessi possono apprendono le route da in locale senza tooprefixes modifica manuale.

![Screenshot dello scenario di routing di transito.](./media/vpn-gateway-migration/migration2.png)

Poiché la connettività di rete virtuale tooVNet trasformare senza siti locali, uno scenario di transito hello perde la connettività locale per la rete virtuale che è indirettamente connessi tooon locale. Hello perdita di connettività può essere ridotti in hello seguenti due modi, dopo aver completata la migrazione: 

* Abilitare BGP nel gateway VPN che sono connesse tra loro e tooon locale. L'abilitazione del protocollo BGP ripristina la connettività senza apportare altre modifiche di configurazione poiché le route vengono apprese e annunciate tra i gateway di rete virtuale. Si noti che l'opzione BGP è disponibile solo per le unità SKU standard e versioni successive.
* Stabilire una connessione esplicita dal gateway di rete locale a toohello interessati rete virtuale che rappresenta il percorso locale. Potrebbe anche richiedere la modifica di configurazione in hello locale router toocreate e configurare tunnel IPsec hello.

## <a name="next-steps"></a>Passaggi successivi
Dopo avere imparare a supporto della migrazione gateway VPN, andare troppo[piattaforma supportata la migrazione di risorse IaaS tooResource classico Manager](../virtual-machines/windows/migration-classic-resource-manager-ps.md) tooget avviato.

