---
title: "aaaWhat è un elenco di controllo di accesso di rete di Azure?"
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
ms.openlocfilehash: a2681af035d162362771e6df9864bbe838f16352
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-an-endpoint-access-control-list"></a>Informazioni sugli elenchi di controllo di accesso agli endpoint

> [!IMPORTANT]
> Azure offre due [modelli di distribuzione](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) per creare e usare le risorse: Resource Manager e la distribuzione classica. In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello. Si consiglia di utilizzano modello di distribuzione di gestione risorse di hello più nuove distribuzioni. 

Un elenco di controllo di accesso (ACL) agli endpoint è un miglioramento della sicurezza disponibile per la distribuzione di Azure. Un ACL fornisce hello possibilità tooselectively consentire o negare il traffico per un endpoint della macchina virtuale. Questa funzionalità di filtro per i pacchetti garantisce un ulteriore livello di sicurezza. È possibile specificare elenchi di controllo di accesso di rete solo per gli endpoint e non per una rete virtuale o una subnet specifica in essa contenuta. È consigliabile toouse rete sicurezza gruppi anziché gli ACL, laddove possibile. vedere toolearn ulteriori informazioni su NSGs, [Cenni preliminari sul gruppo di sicurezza di rete](virtual-networks-nsg.md)

ACL possono essere configurati tramite PowerShell o hello portale di Azure. tooconfigure un ACL di rete tramite PowerShell, vedere [gli elenchi di controllo di accesso di gestione per gli endpoint tramite PowerShell](virtual-networks-acl-powershell.md). un ACL di rete tramite tooconfigure hello Azure portale, vedere [come tooset endpoint della macchina virtuale tooa](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

Tramite gli ACL di rete, è possibile eseguire il seguente hello:

* Consentire o negare il traffico in ingresso in base a una subnet remota IPv4 indirizzo intervallo tooa macchina virtuale endpoint di input in modo selettivo.
* Creare una blacklist di indirizzi IP.
* Creare più regole per un endpoint di macchina virtuale.
* Utilizzare regole di ordinamento hello tooensure corretto set di regole vengono applicate a un endpoint di macchina virtuale specificata (toohighest più basso)
* Specificare un elenco di controllo di accesso per un indirizzo IPv4 di una subnet remota specifica.

Vedere hello [Azure limita](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#networking-limits) articolo per i limiti di ACL.

## <a name="how-acls-work"></a>Funzionamento degli elenchi di controllo di accesso
Un elenco di controllo di accesso è un oggetto che contiene un elenco di regole. Quando si crea un ACL e applicarlo tooa endpoint della macchina virtuale, il filtraggio dei pacchetti avviene nel nodo host hello della macchina virtuale. Ciò significa che il traffico di hello da indirizzi IP remoti viene filtrato dal nodo host hello per le regole ACL corrispondente invece che nella macchina virtuale. Ciò impedisce che la macchina virtuale impiegare cicli della CPU preziosi hello nel filtro dei pacchetti.

Quando viene creata una macchina virtuale, un ACL predefinito viene inserito nella posizione tooblock tutto il traffico in ingresso. Tuttavia, se viene creato un endpoint per (porta 3389), quindi hello predefinito che ACL modificato tooallow tutto il traffico in ingresso per l'endpoint. Il traffico in entrata da qualsiasi subnet remota viene quindi consentito toothat endpoint sia alcun provisioning del firewall necessaria. Tutte le altre porte sono bloccate per il traffico in ingresso a meno che non vengano creati endpoint per tali porte. Il traffico in uscita è consentito per impostazione predefinita.

**Tabella di esempio di elenco di controllo di accesso predefinito**

| **N. regola** | **Subnet remota** | **Endpoint** | **Consenti/Nega** |
| --- | --- | --- | --- |
| 100 |0.0.0.0/0 |3389 |Consenti |

## <a name="permit-and-deny"></a>Consentire e negare
È possibile consentire o negare in modo selettivo il traffico di rete per un endpoint di input di macchina virtuale creando regole che specificano "consenti" o "nega". È importante toonote che per impostazione predefinita, quando viene creato un endpoint, tutto il traffico viene consentito toohello endpoint. Per questo motivo, è importante toounderstand come toocreate le regole di autorizzazione o negazione e inserire tali elementi nell'ordine di precedenza hello appropriato se si desidera un controllo granulare rete hello il traffico che si sceglie l'endpoint della macchina virtuale tooallow tooreach hello.

Tooconsider punti:

1. **Nessun ACL –** per impostazione predefinita quando viene creato un endpoint, è consentire tutti per endpoint hello.
2. **Consenti** : quando si aggiungono uno o più intervalli "Consenti", per impostazione predefinita tutti gli altri intervalli vengono negati. Solo i pacchetti hello intervallo IP consentito saranno in grado di toocommunicate con l'endpoint della macchina virtuale hello.
3. **Nega** : quando si aggiungono uno o più intervalli "Nega", per impostazione predefinita tutti gli altri intervalli di traffico vengono consentiti.
4. **Combinazione di Consenti e Nega -** è possibile utilizzare una combinazione di "Consenti" e "Nega" quando si desidera toocarve out un indirizzo IP specifico intervallo toobe consentito o negato.

## <a name="rules-and-rule-precedence"></a>Regole e relativa precedenza
È possibile configurare elenchi di controllo di accesso di rete per endpoint di macchina virtuale specifici. È ad esempio possibile specificare un elenco di controllo di accesso di rete per un endpoint RDP creato in una macchina virtuale che blocca l'accesso a determinati indirizzi IP. Hello tabella riportata di seguito viene illustrato un toopublic di accesso toogrant modo IP virtuale (VIP) di un accesso di determinati toopermit intervallo per RDP. Tutti gli altri indirizzi IP remoti vengono negati. L'ordine di precedenza adottato per le regole è *la più bassa ha la precedenza* .

### <a name="multiple-rules"></a>Regole multiple
Nell'esempio hello seguente, se si desidera tooallow endpoint RDP toohello di accesso solo da due pubblici intervalli di indirizzi IPv4 (65.0.0.0/8 e 159.0.0.0/8), è possibile ottenere questo specificando due *consentire* regole. In questo caso, poiché RDP viene creato per impostazione predefinita per una macchina virtuale, è consigliabile toolock verso il basso accesso toohello la porta RDP in base a una subnet remota. Hello esempio riportato di seguito viene illustrato un toopublic di accesso toogrant modo IP virtuale (VIP) di un accesso di determinati toopermit intervallo per RDP. Tutti gli altri indirizzi IP remoti vengono negati. Questo processo funziona perché è possibile configurare elenchi di controllo di accesso di rete per un endpoint di macchina virtuale specifico e l'accesso viene negato per impostazione predefinita.

**Esempio: regole multiple**

| **N. regola** | **Subnet remota** | **Endpoint** | **Consenti/Nega** |
| --- | --- | --- | --- |
| 100 |65.0.0.0/8 |3389 |Consenti |
| 200 |159.0.0.0/8 |3389 |Consenti |

### <a name="rule-order"></a>Ordine delle regole
Poiché più regole possono essere specificate per un endpoint, in ordine toodetermine quale regola ha la precedenza deve essere una regola di tooorganize modo. ordine delle regole Hello specifica la precedenza. L'ordine di precedenza adottato per gli elenchi di controllo di accesso di rete è *la più bassa ha la precedenza* . Nell'esempio hello seguente endpoint hello sulla porta 80 viene concesso in modo selettivo tooonly accesso determinati intervalli di indirizzi IP. tooconfigure, è necessaria una regola Nega (regola \# 100) per gli indirizzi nello spazio 175.1.0.1/24 hello. Una seconda regola viene quindi specificata con la precedenza 200 che consente di accedere tooall gli altri indirizzi in 175.0.0.0/8.

**Esempio: precedenza delle regole**

| **N. regola** | **Subnet remota** | **Endpoint** | **Consenti/Nega** |
| --- | --- | --- | --- |
| 100 |175.1.0.1/24 |80 |Nega |
| 200 |175.0.0.0/8 |80 |Consenti |

## <a name="network-acls-and-load-balanced-sets"></a>Elenchi di controllo di accesso di rete e set con carico bilanciato
È possibile specificare elenchi di controllo di accesso di rete sull'endpoint di un set con carico bilanciato. Se viene specificato un ACL per un set con carico bilanciato, ACL di rete hello è applicato tooall di macchine virtuali in tale set con carico bilanciato. Ad esempio, se viene creato un set con carico bilanciato con la "Porta 80" e set con carico bilanciato hello contiene 3 VM, rete hello creato ACL sull'endpoint "Porta 80" di una che macchina virtuale verrà automaticamente applicare toohello altre macchine virtuali.

![Elenchi di controllo di accesso di rete e set con carico bilanciato](./media/virtual-networks-acl/IC674733.png)

## <a name="next-steps"></a>Passaggi successivi
[Gestire elenchi di controllo di accesso di endpoint con PowerShell](virtual-networks-acl-powershell.md)

