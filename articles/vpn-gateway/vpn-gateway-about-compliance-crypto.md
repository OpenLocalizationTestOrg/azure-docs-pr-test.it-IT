---
title: aaaAbout requisiti di crittografia e i gateway VPN di Azure | Documenti Microsoft
description: In questo articolo vengono descritti i requisiti di crittografia e i gateway VPN di Azure
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 238cd9b3-f1ce-4341-b18e-7390935604fa
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/22/2017
ms.author: yushwang
ms.openlocfilehash: af5f14d66beeea5316218f9788c4ad7876826162
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="about-cryptographic-requirements-and-azure-vpn-gateways"></a>Informazioni sui requisiti di crittografia e i gateway VPN di Azure

In questo articolo viene descritto come configurare toosatisfy gateway VPN di Azure i requisiti di crittografia per i tunnel VPN S2S cross-premise e connessioni di rete virtuale all'interno di Azure. 

## <a name="about-ipsec-and-ike-policy-parameters-for-azure-vpn-gateways"></a>Informazioni sui parametri di criteri IPsec e IKE per gateway VPN di Azure
Lo standard di protocollo IPsec e IKE supporta un'ampia gamma di algoritmi di crittografia in varie combinazioni. Se i clienti non richiedono una combinazione specifica di algoritmi e parametri per la crittografia, i gateway VPN di Azure usano un set di proposte predefinite. set di criteri predefiniti Hello sono state scelte toomaximize interoperabilità con un'ampia gamma di dispositivi VPN di terze parti in configurazioni predefinite. Di conseguenza, i criteri di hello e numero di hello delle proposte non può coprire tutte le possibili combinazioni di algoritmi di crittografia disponibili e i punti di forza di chiave.

criterio predefinito impostato per il gateway VPN di Azure è elencato nel documento hello Hello: [informazioni sui dispositivi VPN e i parametri IPsec/IKE per le connessioni Site-to-Site VPN Gateway](vpn-gateway-about-vpn-devices.md).

## <a name="cryptographic-requirements"></a>Requisiti per la crittografia
Per le comunicazioni che richiedono gli algoritmi di crittografia specifici o parametri, in genere a causa di requisiti di sicurezza o toocompliance, i clienti ora possono configurare i toouse gateway VPN di Azure criteri IPsec/IKE personalizzati con crittografia specifico gli algoritmi e vantaggi chiave, piuttosto che set di criteri di hello predefinito di Azure.

Ad esempio, i criteri di hello IKEv2 in modalità principale per i gateway VPN di Azure utilizzano solo il gruppo Diffie-Hellman di 2 (1024 bit), mentre i clienti potrebbe essere necessario toospecify più forte toobe gruppi utilizzati in IKE, ad esempio gruppo 14 (2048 bit), gruppo 24 (gruppo MODP 2048 bit) o ECP (elliptic curva di gruppi) 384 o 256 bit (gruppo rispettivamente 19 e 20 gruppo). Requisiti simili si applicano anche i criteri di modalità rapida tooIPsec.

## <a name="custom-ipsecike-policy-with-azure-vpn-gateways"></a>Criteri IPsec/IKE personalizzati con i gateway VPN di Azure
I gateway VPN di Azure ora supportano i criteri IPsec/IKE personalizzati per connessione. Per un sito a sito o da rete connessione, è possibile scegliere una combinazione specifica di algoritmi di crittografia per IPsec e IKE con attendibilità della chiave hello desiderato, come illustrato nell'esempio seguente hello:

![ipsec-ike-policy](./media/vpn-gateway-about-compliance-crypto/ipsecikepolicy.png)

È possibile creare un criterio IPsec/IKE e applicare una connessione nuova o esistente tooa. 

### <a name="workflow"></a>Flusso di lavoro

1. Creare reti virtuali hello, gateway VPN o gateway di rete locale per la topologia di connettività, come descritto in altre come-toodocuments
2. Creare un criterio IPsec/IKE
3. È possibile applicare criteri hello quando si crea una connessione S2S o di rete virtuale a
4. Se la connessione hello è già stata creata, è possibile applicare o aggiornare la connessione esistente hello criteri tooan


## <a name="ipsecike-policy-faq"></a>Domande frequenti sui criteri IPsec/IKE

[!INCLUDE [vpn-gateway-ipsecikepolicy-faq-include](../../includes/vpn-gateway-ipsecikepolicy-faq-include.md)]


## <a name="next-steps"></a>Passaggi successivi
Vedere [Configurare i criteri IPsec/IKE](vpn-gateway-ipsecikepolicy-rm-powershell.md) per istruzioni dettagliate sulla configurazione dei criteri IPsec/IKE personalizzato su una connessione.

Vedere anche [connettersi più dispositivi VPN basata su criteri](vpn-gateway-connect-multiple-policybased-rm-ps.md) toolearn ulteriori informazioni sull'opzione UsePolicyBasedTrafficSelectors hello.
