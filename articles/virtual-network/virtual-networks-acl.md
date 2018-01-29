---
title: Informazioni sugli elenchi di controllo di accesso di rete di Azure
description: Informazioni sugli elenchi di controllo di accesso in Azure
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 83d66c84-8f6b-4388-8767-cd2de3e72d76
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.openlocfilehash: 9a0c85367968c9b38104012d75b1f3975be82cc1
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/11/2017
---
# <a name="what-is-an-endpoint-access-control-list"></a>Informazioni sugli elenchi di controllo di accesso agli endpoint

> [!IMPORTANT]
> Azure offre due [modelli di distribuzione](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) per creare e usare le risorse: Resource Manager e la distribuzione classica. Questo articolo illustra l'uso del modello di distribuzione classica. Microsoft consiglia di usare il modello di distribuzione Resource Manager per le distribuzioni più recenti. 

Un elenco di controllo di accesso (ACL) agli endpoint è un miglioramento della sicurezza disponibile per la distribuzione di Azure. Offre la possibilità di consentire o negare in modo selettivo il traffico per un endpoint di macchina virtuale. Questa funzionalità di filtro per i pacchetti garantisce un ulteriore livello di sicurezza. È possibile specificare elenchi di controllo di accesso di rete solo per gli endpoint e non per una rete virtuale o una subnet specifica in essa contenuta. È consigliabile usare i gruppi di sicurezza di rete invece degli elenchi di controllo di accesso, laddove possibile. Per altre informazioni sui gruppi di accesso di rete, vedere [Panoramica dei gruppi di sicurezza di rete](virtual-networks-nsg.md).

Gli elenchi di controllo di accesso possono essere configurati tramite PowerShell o il portale di Azure. Per configurare un elenco di controllo di accesso di rete usando PowerShell, vedere [Gestione degli elenchi di controllo di accesso per gli endpoint tramite PowerShell](virtual-networks-acl-powershell.md). Per configurare un elenco di controllo di accesso di rete usando il portale di Azure, vedere [Come configurare gli endpoint in una macchina virtuale](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

Con gli elenchi di controllo di accesso di rete, è possibile effettuare le operazioni seguenti:

* Consentire o negare in modo selettivo il traffico in ingresso in base a un intervallo di indirizzi IPv4 di subnet remota in un endpoint di input di macchina virtuale.
* Creare una blacklist di indirizzi IP.
* Creare più regole per un endpoint di macchina virtuale.
* Usare l'ordinamento delle regole per assicurarsi che venga applicato il set di regole corretto per un endpoint specifico di macchina virtuale (dalla più bassa alla più alta).
* Specificare un elenco di controllo di accesso per un indirizzo IPv4 di una subnet remota specifica.

Per i limiti degli elenchi di controllo di accesso, vedere l'articolo [Limiti di Azure](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#networking-limits).

## <a name="how-acls-work"></a>Funzionamento degli elenchi di controllo di accesso
Un elenco di controllo di accesso è un oggetto che contiene un elenco di regole. Quando si crea e si applica un elenco di controllo di accesso a un endpoint di macchina virtuale, viene eseguito il filtro dei pacchetti nel nodo host della macchina virtuale. Questo significa che il traffico proveniente dagli indirizzi IP remoti non viene filtrato nella macchina virtuale, bensì dal nodo host per la corrispondenza con le regole degli elenchi di controllo di accesso. In questo modo si evita che la macchina virtuale usi preziosi cicli della CPU per filtrare i pacchetti.

Quando viene creata una macchina virtuale, viene creato anche un elenco di controllo di accesso predefinito per bloccare tutto il traffico in ingresso. Se però viene creato un endpoint per la porta 3389, l'elenco di controllo di accesso predefinito viene modificato in modo da consentire tutto il traffico in ingresso per tale endpoint. Il traffico in ingresso proveniente da una subnet remota verso tale endpoint viene quindi consentito e non è necessario il provisioning di alcun firewall. Tutte le altre porte sono bloccate per il traffico in ingresso a meno che non vengano creati endpoint per tali porte. Il traffico in uscita è consentito per impostazione predefinita.

**Tabella di esempio di elenco di controllo di accesso predefinito**

| **N. regola** | **Subnet remota** | **Endpoint** | **Consenti/Nega** |
| --- | --- | --- | --- |
| 100 |0.0.0.0/0 |3389 |Consenti |

## <a name="permit-and-deny"></a>Consentire e negare
È possibile consentire o negare in modo selettivo il traffico di rete per un endpoint di input di macchina virtuale creando regole che specificano "consenti" o "nega". È importante notare che per impostazione predefinita, quando viene creato un endpoint, tutto il traffico per l'endpoint viene consentito. Per questo motivo, è importante capire come creare regole di autorizzazione/rifiuto e posizionarle secondo un ordine di precedenza appropriato per esercitare un controllo granulare sul traffico di rete che si sceglie di consentire per l'endpoint della macchina virtuale.

Elementi da considerare:

1. **Nessun ACL** : per impostazione predefinita quando viene creato un endpoint, tutto il traffico viene consentito.
2. **Consenti** : quando si aggiungono uno o più intervalli "Consenti", per impostazione predefinita tutti gli altri intervalli vengono negati. Solo i pacchetti provenienti dall'intervallo IP consentito saranno in grado di comunicare con l'endpoint della macchina virtuale.
3. **Nega** : quando si aggiungono uno o più intervalli "Nega", per impostazione predefinita tutti gli altri intervalli di traffico vengono consentiti.
4. **Combinazione di Consenti e Nega** : è possibile usare una combinazione di "Consenti" e "Nega" per definire un intervallo IP da consentire o negare.

## <a name="rules-and-rule-precedence"></a>Regole e relativa precedenza
È possibile configurare elenchi di controllo di accesso di rete per endpoint di macchina virtuale specifici. È ad esempio possibile specificare un elenco di controllo di accesso di rete per un endpoint RDP creato in una macchina virtuale che blocca l'accesso a determinati indirizzi IP. La tabella seguente illustra come concedere l'accesso a indirizzi IP virtuali pubblici (VIP) di un determinato intervallo per consentire l'accesso per RDP. Tutti gli altri indirizzi IP remoti vengono negati. L'ordine di precedenza adottato per le regole è *la più bassa ha la precedenza* .

### <a name="multiple-rules"></a>Regole multiple
Nell'esempio seguente se si desidera consentire l'accesso all'endpoint RDP solo da due intervalli di indirizzi IPv4 pubblici (65.0.0.0/8 e 159.0.0.0/8), è possibile specificare due regole *Consenti* . In questo caso poiché RDP viene creato per impostazione predefinita per una macchina virtuale, è possibile bloccare l'accesso alla porta RDP in base a una subnet remota. L'esempio seguente illustra come concedere l'accesso a indirizzi IP virtuali pubblici (VIP) di un determinato intervallo per consentire l'accesso per RDP. Tutti gli altri indirizzi IP remoti vengono negati. Questo processo funziona perché è possibile configurare elenchi di controllo di accesso di rete per un endpoint di macchina virtuale specifico e l'accesso viene negato per impostazione predefinita.

**Esempio: regole multiple**

| **N. regola** | **Subnet remota** | **Endpoint** | **Consenti/Nega** |
| --- | --- | --- | --- |
| 100 |65.0.0.0/8 |3389 |Consenti |
| 200 |159.0.0.0/8 |3389 |Consenti |

### <a name="rule-order"></a>Ordine delle regole
Poiché è possibile specificare più regole per un endpoint, è necessario trovare un modo per organizzare le regole per determinare quale ha la precedenza. L'ordine delle regole specifica la precedenza. L'ordine di precedenza adottato per gli elenchi di controllo di accesso di rete è *la più bassa ha la precedenza* . Nell'esempio seguente all'endpoint sulla porta 80 viene concesso l'accesso in modo selettivo solo a determinati intervalli di indirizzi IP A tale scopo, è necessaria una regola Nega (regola n. 100) per gli indirizzi nello spazio \#175.1.0.1/24. Una seconda regola viene quindi specificata con la precedenza 200 che consente l'accesso a tutti gli altri indirizzi in 175.0.0.0/8.

**Esempio: precedenza delle regole**

| **N. regola** | **Subnet remota** | **Endpoint** | **Consenti/Nega** |
| --- | --- | --- | --- |
| 100 |175.1.0.1/24 |80 |Nega |
| 200 |175.0.0.0/8 |80 |Consenti |

## <a name="network-acls-and-load-balanced-sets"></a>Elenchi di controllo di accesso di rete e set con carico bilanciato
È possibile specificare elenchi di controllo di accesso di rete sull'endpoint di un set con carico bilanciato. Se per un set con carico bilanciato viene specificato un elenco di controllo di accesso, l'elenco di controllo di accesso di rete verrà applicato a tutte le macchine virtuali di tale set con carico bilanciato. Se ad esempio viene creato un set con carico bilanciato con la "porta 80" e 3 macchine virtuali, l'elenco di controllo di accesso di rete creato sulla "porta 80" dell'endpoint di una macchina virtuale verrà applicato automaticamente alle altre macchine virtuali.

![Elenchi di controllo di accesso di rete e set con carico bilanciato](./media/virtual-networks-acl/IC674733.png)

## <a name="next-steps"></a>Passaggi successivi
[Gestire elenchi di controllo di accesso di endpoint con PowerShell](virtual-networks-acl-powershell.md)

