---
title: 'Azure AD Domain Services: linee guida sulla rete | Documentazione Microsoft'
description: Considerazioni sulla rete per Azure Active Directory Domain Services
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 23a857a5-2720-400a-ab9b-1ba61e7b145a
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: maheshu
ms.openlocfilehash: 804d4ea7d1b3b07b6d224855c7adb90bdfe24022
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="networking-considerations-for-azure-ad-domain-services"></a>Considerazioni sulla rete per Azure AD Domain Services
## <a name="how-tooselect-an-azure-virtual-network"></a>Come tooselect una rete virtuale di Azure
Hello linee guida seguenti consentono di selezionare una rete virtuale di toouse con servizi di dominio Active Directory di Azure.

### <a name="type-of-azure-virtual-network"></a>Tipo di rete virtuale di Azure
* È possibile abilitare Azure AD Domain Services in una rete virtuale di Azure classica.
* La funzionalità Azure AD Domain Services **non può essere abilitata nelle reti virtuali create usando Azure Resource Manager**.
* È possibile connettere una basata su Gestione risorse di rete virtuale tooa classico rete virtuale in cui servizi di dominio Active Directory di Azure è abilitato. Successivamente, è possibile utilizzare servizi di dominio Azure Active Directory nella rete virtuale basato su Gestione risorse hello. Per ulteriori informazioni, vedere hello [connettività di rete](active-directory-ds-networking.md#network-connectivity) sezione.
* **Reti virtuali regionali**: se si prevede di toouse una rete virtuale esistente, assicurarsi che sia una rete virtuale regionale.

  * Reti virtuali che utilizzano il meccanismo di gruppi di affinità legacy hello non possono essere utilizzate con servizi di dominio Active Directory di Azure.
  * Servizi di dominio Active Directory di Azure, toouse [eseguire la migrazione delle reti virtuali di reti virtuali legacy tooregional](../virtual-network/virtual-networks-migrate-to-regional-vnet.md).

### <a name="azure-region-for-hello-virtual-network"></a>Area di Azure per la rete virtuale hello
* I servizi di dominio Active Directory di Azure distribuito in un dominio gestito hello stessa area di rete virtuale di hello in che è scegliere servizio hello tooenable Azure.
* Selezionare una rete virtuale in un'area di Azure supportata da Azure AD Domain Services.
* Vedere hello [servizi di Azure dall'area](https://azure.microsoft.com/regions/#services/) tooknow pagina hello aree di Azure in cui sono disponibili servizi di dominio di Azure AD.

### <a name="requirements-for-hello-virtual-network"></a>Requisiti per la rete virtuale hello
* **Prossimità tooyour Azure carichi di lavoro**: selezionare hello rete virtuale che ospita attualmente/ospiterà le macchine virtuali che devono accedere ai servizi di dominio Active Directory tooAzure.
* **I server DNS personalizzato/portare personali**: verificare che siano non presenti Nessun server DNS personalizzato configurato per la rete virtuale hello.
* **Domini esistenti con stesso nome di dominio di hello**: verificare che non è un dominio esistente con hello stesso nome di dominio sulla rete virtuale. Ad esempio, si supponga di che avere un dominio denominato 'contoso.com' già disponibile nella rete virtuale selezionata hello. In un secondo momento, si tenta di un dominio gestito di servizi di dominio Active Directory di Azure con hello tooenable stesso nome di dominio (ad esempio 'contoso.com') nella rete virtuale. Si verifica un errore durante il tentativo di servizi di dominio tooenable Azure AD. Questo errore è a causa di conflitti tooname hello nome di dominio sulla rete virtuale. In questo caso, è necessario utilizzare tooset un nome diverso, il dominio gestito di servizi di dominio Active Directory di Azure. In alternativa, è possibile annullare il provisioning di dominio esistente hello e quindi procedere servizi di dominio tooenable Azure AD.

> [!WARNING]
> Dopo avere abilitato il servizio di hello non è possibile spostare rete virtuale di servizi di dominio tooa diverso.
>
>

## <a name="network-security-groups-and-subnet-design"></a>Gruppi di sicurezza di rete e struttura della subnet
Oggetto [gruppo di sicurezza (rete)](../virtual-network/virtual-networks-nsg.md) contiene un elenco di regole di elenco di controllo di accesso (ACL) che consentono o negano il traffico di rete tooyour istanze di macchina virtuale in una rete virtuale. I gruppi di sicurezza di rete possono essere associati a subnet o singole istanze VM in una subnet. Quando un gruppo è associata a una subnet, regole ACL hello si applicano le istanze VM hello tooall nella subnet. Inoltre, il traffico tooan singole macchine Virtuali è possibile limitare ulteriormente l'associazione di un gruppo direttamente toothat macchina virtuale.

![Struttura consigliata per la subnet](./media/active-directory-domain-services-design-guide/vnet-subnet-design.png)

### <a name="best-practices-for-choosing-a-subnet"></a>Procedure consigliate per la scelta di una subnet
* Distribuire servizi di dominio Active Directory di Azure tooa **separare subnet dedicata** all'interno della rete virtuale di Azure.
* Non si applicano NSGs toohello dedicato subnet per il dominio gestito. Se è necessario applicare una subnet dedicata toohello NSGs, assicurarsi di **non bloccare hello porte necessarie tooservice e gestire il dominio**.
* Non limitare eccessivamente numero hello di indirizzi IP disponibili all'interno di subnet hello dedicato per il dominio gestito. Questa restrizione impedisce che il servizio di hello rende disponibile per il dominio gestito due controller di dominio.
* **Non abilitare Servizi di dominio Active Directory di Azure nella subnet del gateway hello** della rete virtuale.

> [!WARNING]
> Quando si associa un gruppo con una subnet in cui servizi di dominio Active Directory di Azure è abilitata, è possibile interrompere tooservice possibilità di Microsoft e gestire il dominio hello. Viene inoltre ostacolata la sincronizzazione tra il tenant Azure AD e il dominio gestito. **Hello contratto di servizio non è applicabile toodeployments in un gruppo è stato applicato che blocca i servizi di dominio Active Directory di Azure dall'aggiornamento e la gestione del dominio.**
>
>

### <a name="ports-required-for-azure-ad-domain-services"></a>Porte necessarie per Azure Active Directory Domain Services
Hello porte seguenti sono necessari per i servizi di dominio AD Azure tooservice e gestire il dominio gestito. Verificare che le porte non sono bloccate per subnet hello in cui è stato abilitato il dominio gestito.

| Numero della porta | Scopo |
| --- | --- |
| 443 |Sincronizzazione con il tenant di Azure AD |
| 3389 |Gestione del dominio |
| 5986 |Gestione del dominio |
| 636 |LDAP (LDAPS) accesso tooyour gestito dominio protetto |

### <a name="sample-nsg-for-virtual-networks-with-azure-ad-domain-services"></a>Gruppo di sicurezza di rete (NSG) di esempio per le reti virtuali con Azure AD Domain Services
Hello nella tabella seguente illustra un esempio di gruppo è possibile configurare una rete virtuale con un dominio gestito di servizi di dominio Active Directory di Azure. Questa regola consente il traffico in ingresso da hello sopra le porte specificate tooensure il dominio gestito rimane una patch, aggiornata e possono essere monitorate da Microsoft. Hello predefinito 'DenyAll' regola verrà applicata tooall il traffico in ingresso di hello internet.

Inoltre, hello NSG viene inoltre illustrato come toolock verso il basso l'accesso LDAP sicuro tramite hello internet. Ignora questa regola se non è stato abilitato accesso LDAP sicuro tooyour una dominio gestito tramite hello internet. Hello gruppo contiene un set di regole che consentono l'accesso LDAPS in ingresso sulla porta TCP 636 solo da un set specificato di indirizzi IP. Hello NSG regola tooallow LDAPS tramite hello internet da indirizzi IP specificati ha una priorità maggiore hello regola DenyAll NSG.

![Esempio NSG toosecure LDAPS tramite hello internet](./media/active-directory-domain-services-admin-guide/secure-ldap-sample-nsg.png)

**Altre informazioni** - [Creare un gruppo di sicurezza di rete](../virtual-network/virtual-networks-create-nsg-arm-pportal.md).


## <a name="network-connectivity"></a>Connettività di rete
Un dominio gestito di Azure AD Domain Services può essere abilitato solo in una singola rete virtuale classica di Azure. Le reti virtuali create usando Azure Resource Manager non sono supportate.

### <a name="scenarios-for-connecting-azure-networks"></a>Scenari per la connessione di reti di Azure
Connettere reti virtuali di Azure toouse hello dominio gestito in uno dei seguenti scenari di distribuzione hello:

#### <a name="use-hello-managed-domain-in-more-than-one-azure-classic-virtual-network"></a>Hello utilizzare gestiti nella rete virtuale classica Azure più di un dominio
È possibile connettere altri toohello di reti virtuali di Azure classico Azure classico rete virtuale in cui sono abilitati i servizi di dominio Active Directory di Azure. Questa connessione VPN consente toouse hello gestito dominio con i carichi di lavoro distribuiti in altre reti virtuali.

![Connettività di rete virtuale classica](./media/active-directory-domain-services-design-guide/classic-vnet-connectivity.png)

#### <a name="use-hello-managed-domain-in-a-resource-manager-based-virtual-network"></a>Utilizzare hello dominio gestito in una rete virtuale basato su Gestione risorse
È possibile connettersi toohello una rete virtuale basato su Gestione risorse di Azure classico rete virtuale in cui sono abilitati i servizi di dominio Active Directory di Azure. Questa connessione consente toouse hello gestito dominio con i carichi di lavoro distribuite in hello basate su Gestione risorse di rete virtuale.

![Connettività di rete virtuale di gestione risorse tooclassic](./media/active-directory-domain-services-design-guide/classic-arm-vnet-connectivity.png)

### <a name="network-connection-options"></a>Opzioni per le connessioni di rete
* **Le connessioni di rete virtuale a connessioni VPN da sito a sito**: la connessione di una rete virtuale (VNet a VNet) tooanother di rete virtuale è simile tooconnecting un percorso di rete virtuale tooan locale del sito. Entrambi i tipi di connettività di utilizzare un tooprovide gateway VPN un tunnel sicuro tramite IPsec/IKE.

    ![Connettività di rete virtuale tramite gateway VPN](./media/active-directory-domain-services-design-guide/vnet-connection-vpn-gateway.jpg)

    [Altre informazioni: connettere reti virtuali usando il gateway VPN](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md)
* **Le connessioni di rete virtuale a mediante rete peering**: peering di rete virtuale è un meccanismo che connette due reti virtuali in hello stessa area geografica tramite rete backbone Azure hello. Una volta il peering, due reti virtuali hello appaiono come uno per tutti gli scopi di connettività. Continuano a essere gestite come risorse separate, ma le macchine virtuali in queste reti virtuali possono comunicare direttamente tra di esse usando gli indirizzi IP privati.

    ![Connettività di rete virtuale tramite peering](./media/active-directory-domain-services-design-guide/vnet-peering.png)

    [Altre informazioni: Peering reti virtuali](../virtual-network/virtual-network-peering-overview.md)

<br>

## <a name="related-content"></a>Contenuti correlati
* [Peering reti virtuali](../virtual-network/virtual-network-peering-overview.md)
* [Configurare una connessione di rete virtuale a per il modello di distribuzione classica hello](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md)
* [Che cos'è un gruppo di sicurezza di rete](../virtual-network/virtual-networks-nsg.md)
* [Creare un gruppo di sicurezza di rete](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)
