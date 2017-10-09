---
title: Pianificazione e progettazione per connessioni cross-premise - Gateway VPN di Azure | Documentazione Microsoft
description: Informazioni sulla pianificazione e progettazione del gateway VPN per le connessioni Da rete virtuale a rete virtuale cross-premise e ibride
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: d5aaab83-4e74-4484-8bf0-cc465811e757
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/27/2017
ms.author: cherylmc
ms.openlocfilehash: 3d4587ba31d163384212eca88a7e2c0ba8f3b21f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="planning-and-design-for-vpn-gateway"></a>Pianificazione e progettazione per il gateway VPN

Le operazioni di pianificazione e progettazione di connessioni cross-premise e da rete virtuale a rete virtuale possono essere molto semplici o piuttosto complicate, a seconda delle esigenze di rete. Questo articolo illustra in dettaglio alcune considerazioni di base sulla progettazione e sulla pianificazione.

## <a name="planning"></a>Pianificazione

### <a name="compare"></a>Opzioni di connettività di più sedi locali

Se si desidera tooconnect locale siti in modo sicuro la rete virtuale tooa, è pertanto toodo di tre modi diversi: da sito a sito, Point-to-Site ed ExpressRoute. Confrontare le connessioni cross-premise diversi hello disponibili. opzione che tu scelga determina Hello può dipendere da diverse considerazioni, ad esempio:

* Che tipo di velocità effettiva richiede la soluzione?
* Si desidera toocommunicate su hello rete Internet pubblica tramite VPN sicura o tramite una connessione privata?
* Si dispone di un toouse disponibili di indirizzi IP pubblici?
* Se si sta pianificando toouse un dispositivo VPN? In tal caso, è compatibile?
* Si connette un numero limitato di computer o si desidera una connessione permanente per il sito?
* Il tipo di gateway VPN è necessario per la soluzione hello desiderato toocreate?
* Quale SKU del gateway è opportuno usare?

### <a name="planningtable"></a>Tabella di pianificazione

Hello nella tabella seguente consente di decidere hello connettività migliore per la soluzione.

[!INCLUDE [vpn-gateway-cross-premises](../../includes/vpn-gateway-cross-premises-include.md)]

### <a name="gwsku"></a>SKU del gateway

[!INCLUDE [vpn-gateway-table-gwtype-aggtput](../../includes/vpn-gateway-table-gwtype-aggtput-include.md)]

### <a name="wf"></a>Flusso di lavoro

Hello seguito sono riportati i hello comune del flusso di lavoro per la connettività di cloud:

1. Progettazione e pianificare che il connettività della topologia ed elenco hello gli spazi di indirizzi per tutte le reti si desidera tooconnect.
2. Creare una rete virtuale di Azure 
3. Creare un gateway VPN per rete virtuale hello.
4. Creare e configurare le reti locali tooon di connessioni o altre reti virtuali (se necessario).
5. Creare e configurare una connessione Da punto a sito per il gateway VPN di Azure, se necessario.

## <a name="design"></a>Progettazione
### <a name="topologies"></a>Topologie di connessione

Iniziare esaminando i diagrammi di hello in hello [sul Gateway VPN](vpn-gateway-about-vpngateways.md) articolo. articolo Hello contiene diagrammi di base, i modelli di distribuzione hello per ogni topologia e strumenti di distribuzione disponibili hello è possibile utilizzare la configurazione toodeploy.

### <a name="designbasics"></a>Nozioni di base sulla progettazione

Hello le sezioni seguenti illustrano nozioni di base di hello VPN gateway. 

#### <a name="servicelimits"></a>Limiti dei servizi di rete

Scorrere hello tabelle tooview [networking servizi limiti](../azure-subscription-service-limits.md#networking-limits). limiti di Hello elencati potrebbero compromettere la progettazione.

#### <a name="subnets"></a>Informazioni sulle subnet

Quando si creano le connessioni, è necessario considerare gli intervalli di indirizzi della subnet. Gli intervalli di indirizzi della subnet non possono sovrapporsi. Una subnet sovrapposta è quando un percorso locale o di rete virtuale contiene hello contiene stesso spazio di indirizzi che hello altra posizione. Questo significa che è necessario ai tecnici di rete per il toocarve reti locale out toouse è un intervallo per l'IP di Azure/subnet spazio di indirizzamento. È necessario spazio di indirizzi che non è in uso nella rete locale hello.

È importante evitare che le subnet si sovrappongano anche quando si utilizzano connessioni Da rete virtuale a rete virtuale. Se si sovrappongono le subnet e un indirizzo IP presente in hello l'invio e la destinazione di reti virtuali, le connessioni di rete virtuale a non riuscire. Azure non è possibile indirizzare hello dati toohello altra rete virtuale perché l'indirizzo di destinazione hello fa parte di hello l'invio di rete virtuale.

I gateway VPN richiedono una subnet specifica chiamata subnet del gateway. Tutte le subnet gateway devono essere denominate GatewaySubnet toowork correttamente. Verificare che non tooname la subnet gateway con un altro nome e non distribuire macchine virtuali o qualsiasi altra subnet del gateway toohello. Vedere [Subnet del gateway](vpn-gateway-about-vpn-gateway-settings.md#gwsub).

#### <a name="local"></a>Informazioni sui gateway di rete locali

gateway di rete locale Hello si riferisce solitamente percorso locale tooyour. Nel modello di distribuzione classica hello, gateway di rete locale hello è tooas di cui si fa riferimento un sito di rete locale. Quando si configura un gateway di rete locale, si assegnargli un nome, specifica l'indirizzo IP pubblico hello del dispositivo VPN locale di hello e specificare i prefissi di indirizzo hello presenti nel percorso locale hello. Azure esamina i prefissi di indirizzo di destinazione hello il traffico di rete, consulta configurazione hello che è stato specificato per il gateway di rete locale hello e instrada i pacchetti di conseguenza. È possibile modificare i prefissi di indirizzo hello in base alle esigenze. Per altre informazioni, vedere [Gateway di rete locali](vpn-gateway-about-vpn-gateway-settings.md#lng).

#### <a name="gwtype"></a>Informazioni sui tipi di gateway

Selezione tipo di gateway corretto hello per la topologia è fondamentale. Se si seleziona un tipo non corretto hello, il gateway non funzionerà correttamente. tipo di gateway Hello specifica la modalità gateway hello stesso si connette e un'impostazione di configurazione necessarie per il modello di distribuzione di gestione risorse hello.

i tipi di gateway Hello sono:

* VPN
* ExpressRoute

#### <a name="connectiontype"></a>Informazioni sui tipi di connessione

Ogni configurazione richiede un tipo di connessione specifico. tipi di connessione Hello sono:

* IPsec
* Vnet2Vnet
* ExpressRoute
* VPNClient

#### <a name="vpntype"></a>Informazioni sui tipi di VPN

Ogni configurazione richiede un tipo di VPN specifico. Se si combinano due configurazioni, ad esempio la creazione di una connessione Site-to-Site e un toohello connessione Point-to-Site stessa rete virtuale, è necessario utilizzare un tipo VPN che soddisfa entrambi i requisiti di connessione.

[!INCLUDE [vpn-gateway-vpntype](../../includes/vpn-gateway-vpntype-include.md)]

Hello tabelle seguenti illustrano il tipo di VPN hello come viene eseguito il mapping tooeach configurazione della connessione. Verificare che hello tipo VPN per la configurazione di hello corrispondenze gateway che si desidera toocreate. 

[!INCLUDE [vpn-gateway-table-vpntype](../../includes/vpn-gateway-table-vpntype-include.md)]

### <a name="devices"></a>Dispositivi VPN per connessioni da sito a sito

connessione di un sito a sito tooconfigure, indipendentemente dal modello di distribuzione, è necessario hello seguenti elementi:

* Un dispositivo VPN compatibile con i gateway VPN di Azure
* Un indirizzo IP IPv4 pubblico che non si trovi dietro un NAT

È necessario toohave esperienza di configurazione del dispositivo VPN oppure è necessario che un utente che possono configurare il dispositivo di hello automaticamente.

[!INCLUDE [vpn-gateway-configure-vpn-device-rm](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]

### <a name="forcedtunnel"></a>Prendere in considerazione il routing con tunneling forzato

Per la maggior parte delle configurazioni è possibile impostare il tunneling forzato. Il tunneling consente di reindirizzare o "forzare" tutto associato a Internet traffico tooyour indietro percorso locale tramite un tunnel VPN da sito a sito per l'ispezione e controllo forzato. Si tratta di un requisito di sicurezza critico per la maggior parte dei criteri IT aziendali. 

Senza il tunneling forzato, il traffico Internet dalle macchine virtuali in Azure passerà sempre dall'infrastruttura di rete di Azure direttamente out toohello Internet, senza tooallow opzione hello è traffico hello tooinspect o audit. Accesso a Internet non autorizzato potrebbe provocare la diffusione di tooinformation o altri tipi di violazioni di sicurezza.

È possibile configurare una connessione di tunneling forzato in entrambi i modelli di distribuzione e tramite strumenti diversi. Per altre informazioni, vedere [Configurare il tunneling forzato](vpn-gateway-forced-tunneling-rm.md).

**Diagramma tunneling forzato**

![Diagramma di tunneling forzato di Gateway VPN di Azure](./media/vpn-gateway-plan-design/forced-tunneling-diagram.png)

## <a name="next-steps"></a>Passaggi successivi

Vedere hello [domande frequenti su Gateway VPN](vpn-gateway-vpn-faq.md) e [sul Gateway VPN](vpn-gateway-about-vpngateways.md) sugli articoli per ulteriori informazioni toohelp si con la progettazione.

Per altre informazioni sulle impostazioni specifiche del gateway, vedere [Informazioni sulle impostazioni del gateway VPN](vpn-gateway-about-vpn-gateway-settings.md).