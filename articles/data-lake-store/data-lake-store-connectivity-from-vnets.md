---
title: aaaConnect tooAzure archivio Data Lake da reti virtuali | Documenti Microsoft
description: La connessione di archivio Data Lake di tooAzure da reti virtuali di Azure
services: data-lake-store,data-catalog
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 683fcfdc-cf93-46c3-b2d2-5cb79f5e9ea5
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: c695dcf49fe4e1a87a90729cf085a938f3b51fe3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="access-azure-data-lake-store-from-vms-within-an-azure-vnet"></a>Accedere ad Azure Data Lake Store dalle macchine virtuali di una rete virtuale di Azure
Azure Data Lake Store è un servizio PaaS eseguito su indirizzi IP Internet pubblici. Qualsiasi server in grado di connettersi in genere possibile Internet pubblico toohello connettersi tooAzure anche gli endpoint archivio Data Lake. Per impostazione predefinita, tutte le macchine virtuali in reti virtuali di Azure possono accedere hello Internet e pertanto possono archivio Azure Data Lake. Tuttavia, è possibile tooconfigure macchine virtuali in una rete virtuale di toonot hanno accesso toohello Internet. Per tali macchine virtuali, archivio Data Lake di accesso tooAzure è limitata anche. Bloccare l'accesso pubblico a Internet per le macchine virtuali in reti virtuali di Azure può essere eseguita utilizzando uno dei seguenti approccio hello.

* Configurando gruppi di sicurezza di rete
* Configurando route definite dall'utente
* Mediante lo scambio delle route tramite il protocollo BGP (settore standard protocollo di routing dinamico) quando si utilizza tale blocco ExpressRoute accedere toohello Internet

In questo articolo si apprenderà come tooenable accedere archivio Azure Data Lake di toohello da macchine virtuali di Azure che sono stati limitati tooaccess risorse usando uno dei tre metodi hello elencate in precedenza.

## <a name="enabling-connectivity-tooazure-data-lake-store-from-vms-with-restricted-connectivity"></a>Abilitazione di connettività tooAzure archivio Data Lake da macchine virtuali con connettività limitata
Archiviazione di Azure Data Lake tooaccess da tali macchine virtuali, è necessario configurarli indirizzo IP di hello tooaccess in cui sono disponibile account archivio Azure Data Lake hello. È possibile identificare gli indirizzi IP hello per gli account archivio Data Lake per la risoluzione dei nomi DNS hello degli account in uso (`<account>.azuredatalakestore.net`). A questo scopo, è possibile usare strumenti come **nslookup**. Aprire un prompt dei comandi nel computer ed eseguire hello comando seguente.

    nslookup mydatastore.azuredatalakestore.net

output di Hello analogo al seguente hello. valore in base a Hello **indirizzo** proprietà è l'indirizzo IP hello associato all'account archivio Data Lake.

    Non-authoritative answer:
    Name:    1434ceb1-3a4b-4bc0-9c69-a0823fd69bba-mydatastore.projectcabostore.net
    Address:  104.44.88.112
    Aliases:  mydatastore.azuredatalakestore.net


### <a name="enabling-connectivity-from-vms-restricted-by-using-nsg"></a>Abilitare la connettività da macchine virtuali limitatamente all'uso di NSG
Quando viene utilizzata una regola gruppo tooblock accedere toohello Internet, è possibile creare un altro gruppo che consente accesso toohello indirizzo IP di Data Lake archivio. Altre informazioni sulle regole NSG sono disponibili nell'articolo [Gruppi di sicurezza di rete](../virtual-network/virtual-networks-nsg.md). Per istruzioni su come toocreate NSGs vedere [come NSGs toomanage utilizzando hello Azure portal](../virtual-network/virtual-networks-create-nsg-arm-pportal.md).

### <a name="enabling-connectivity-from-vms-restricted-by-using-udr-or-expressroute"></a>Abilitare la connettività da macchine virtuali limitatamente all'uso di UDR o ExpressRoute
Quando si route, UDRs o scambiati BGP route, vengono utilizzati tooblock accesso toohello Internet, una route speciale deve toobe configurato in modo che le macchine virtuali in tali subnet possono accedere agli endpoint di archivio Data Lake. Per altre informazioni, vedere [Cosa sono le route definite dall'utente](../virtual-network/virtual-networks-udr-overview.md). Per istruzioni sulla creazione di UDR, vedere [Creare route definite dall'utente in Resource Manager](../virtual-network/virtual-network-create-udr-arm-ps.md).

### <a name="enabling-connectivity-from-vms-restricted-by-using-expressroute"></a>Abilitare la connettività dalle macchine virtuali con ExpressRoute
Quando è configurato un circuito ExpressRoute, hello ai server locali possono accedere archivio Data Lake tramite il peering pubblico. Per altre informazioni sulla configurazione di ExpressRoute per il peering pubblico, consultare le [Domande frequenti su ExpressRoute](../expressroute/expressroute-faqs.md).

## <a name="see-also"></a>Vedere anche
* [Panoramica di Data Lake Store di Azure](data-lake-store-overview.md)
* [Sicurezza in Azure Data Lake Store](data-lake-store-security-overview.md)

