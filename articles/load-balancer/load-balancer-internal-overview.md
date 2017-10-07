---
title: servizio di bilanciamento del carico aaaInternal Panoramica | Documenti Microsoft
description: "Panoramica di bilanciamento del carico interno e delle relative funzionalità. Funzionamento di un servizio di bilanciamento del carico per gli endpoint interni di Azure e possibili scenari tooconfigure"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: tysonn
ms.assetid: 36065bfe-0ef1-46f9-a9e1-80b229105c85
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 9a901aad224d8821c154e130e142699d57282b25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="internal-load-balancer-overview"></a>Panoramica del bilanciamento del carico interno

A differenza di hello Internet rivolto al bilanciamento del carico, bilanciamento del carico interno hello (ILB) indirizza il traffico tooresources solo all'interno del servizio cloud hello o tramite VPN tooaccess hello dell'infrastruttura di Azure. infrastruttura Hello limita accesso toohello con carico bilanciato indirizzi IP virtuali (VIP) di un servizio Cloud o una rete virtuale in modo che non siano mai esposto direttamente tooan Internet endpoint. Questo consente interno line-of-business (LOB) toorun di applicazioni in Azure e accesso dal cloud hello o da risorse locali.

## <a name="why-you-may-need-an-internal-load-balancer"></a>Perché potrebbe servire il bilanciamento del carico interno

Il bilanciamento del carico interno di Azure consente di bilanciare il carico tra macchine virtuali che si trovano in un servizio cloud o una rete virtuale nell'ambito di un'area. Per informazioni sull'uso di hello e la configurazione di reti virtuali con un ambito regionale, vedere [reti virtuali regionali](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/) in hello blog di Azure. Le reti virtuali esistenti che sono state configurate per un gruppo di affinità non possono usare il bilanciamento del carico interno.

ILB consente hello seguenti tipi di bilanciamento del carico:

* All'interno di un servizio cloud, macchine virtuali tooa set di macchine virtuali che risiedono all'interno di hello stesso servizio cloud (vedere la figura 1).
* All'interno di una rete virtuale, da macchine virtuali nel set di tooa hello rete virtuale di macchine virtuali che risiedono all'interno di hello stesso servizio cloud di hello virtuale di rete (vedere la figura 2).
* Per una rete virtuale cross-premise, dal set di tooa computer locale di macchine virtuali che risiedono all'interno di hello stesso servizio cloud di hello virtuale di rete (vedere la figura 3).
* Con connessione Internet applicazioni multilivello in cui i livelli di back-end hello non sono esposti a Internet, ma richiedono il bilanciamento del carico per il traffico dal livello di hello con connessione Internet.
* Bilanciamento del carico per applicazioni LOB ospitate in Azure senza la necessità di applicazioni software o componenti hardware aggiuntivi per il bilanciamento del carico. Tra i server locali nel set di hello di computer il cui traffico è a carico bilanciato.

## <a name="internet-facing-multi-tier-applications"></a>Applicazioni multilivello con connessione Internet

livello web Hello ha endpoint con connessione Internet per client Internet e fa parte di un set con carico bilanciato. servizio di bilanciamento del carico Hello distribuisce il traffico in ingresso dai client web per TCP porta 443 (HTTPS) toohello i server web.

server di database Hello sono protetti da un endpoint di bilanciamento del carico interno che i server web hello utilizzano per l'archiviazione. Endpoint, il tipo di traffico con carico bilanciato tra i server di database hello nel set di bilanciamento del carico interno hello con bilanciamento del carico di servizio in questo database.

Hello seguente immagine Mostra hello applicazione multilivello per Internet all'interno di hello stesso servizio cloud.

![Bilanciamento del carico interno di un singolo servizio cloud](./media/load-balancer-internal-overview/IC736321.png)

Figura 1. Applicazione multilivello con connessione Internet

È possibile inoltre utilizzare un'applicazione multilivello è quando hello ILB distribuito tooa un servizio cloud differente rispetto a un servizio consumer di hello per hello ILB hello.

Cloud services utilizzando hello stessa rete virtuale avranno accesso endpoint ILB toohello. Hello seguente immagine vengono visualizzati i server web front-end in un servizio cloud diverso da hello database back-end e l'utilizzo di hello endpoint ILB all'interno di hello stessa rete virtuale.

![Bilanciamento del carico interno tra servizi cloud](./media/load-balancer-internal-overview/IC744147.png)

Figura 2. Server front-end in un altro servizio cloud

## <a name="intranet-line-of-business-applications"></a>Applicazioni Intranet line-of-business

Il traffico dai client nella rete locale hello viene bilanciato tra set hello del server LOB tramite rete tooAzure di connessione VPN.

computer client Hello avrà indirizzo IP tooan di accesso dal servizio VPN di Azure tramite VPN toosite punto. Consente di hello utilizzare hello applicazione LOB ospitata dietro endpoint ILB hello.

![Interno il bilanciamento del carico tramite VPN toosite punto](./media/load-balancer-internal-overview/IC744148.png)

Figura 3 - applicazioni LOB ospitate dietro endpoint LB hello

Un altro scenario hello LOB è una sito toosite VPN toohello rete virtuale in cui viene configurato l'endpoint di bilanciamento del carico interno hello toohave. In questo modo l'endpoint di rete traffico toobe indirizzato toohello ILB locale.

![Interno il bilanciamento del carico utilizzando toosite sito VPN](./media/load-balancer-internal-overview/IC744150.png)

Figura 4 - il traffico di rete locale indirizzata toohello ILB endpoint

## <a name="limitations"></a>Limitazioni

SNAT non è supportato dalle configurazioni del servizio di bilanciamento del carico interno. Nel contesto di hello di questo documento, SNAT fa riferimento tooport simulazione origine NAT.  Si applica tooscenarios in una macchina virtuale in un pool di bilanciamento del carico richiede l'indirizzo IP del tooreach hello rispettivi interno bilanciamento del carico front-end. Questo scenario non è supportato per il servizio di bilanciamento del carico interno. Quando il flusso di hello è toohello con carico bilanciato macchina virtuale che ha avviato il flusso di hello, si verificheranno errori di connessione. È necessario usare un servizio di bilanciamento del carico di tipo proxy per questi scenari.

## <a name="next-steps"></a>Passaggi successivi

[Supporto di Azure Resource Manager per Azure Load Balancer](load-balancer-arm.md)

[Introduzione alla configurazione del bilanciamento del carico Internet](load-balancer-get-started-internet-arm-ps.md)

[Introduzione alla configurazione del bilanciamento del carico interno](load-balancer-get-started-ilb-arm-ps.md)

[Configurare una modalità di distribuzione del bilanciamento del carico](load-balancer-distribution-mode.md)

[Configurare le impostazioni del timeout di inattività TCP per il bilanciamento del carico](load-balancer-tcp-idle-timeout.md)
