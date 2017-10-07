---
title: Azure Site-to-Site VPN disconnette in modo intermittente aaaTroubleshoot | Documenti Microsoft
description: Informazioni su come tootroubleshoot hello problema di connessione VPN da sito a sito hello disconnessa regolarmente.
services: vpn-gateway
documentationcenter: na
author: chadmath
manager: cshepard
editor: 
tags: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/21/2017
ms.author: genli
ms.openlocfilehash: 1ce3c4ff9d8f650312e45f33b760ebcc6597fc13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-site-to-site-vpn-disconnects-intermittently"></a>Risoluzione dei problemi: disconnessioni VPN da sito a sito di Azure intermittenti

Si potrebbero riscontrare problemi di hello che una connessione nuova o esistente di Azure Microsoft Point-to-Site VPN non è stabile o si disconnette regolarmente. Questo articolo fornisce passaggi toohelp identificare e risolvere hello causa del problema hello di risoluzione dei problemi. 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-steps"></a>Passaggi per la risoluzione dei problemi

### <a name="prerequisite-step"></a>Passaggio preliminare

Tipo di controllo hello del gateway di rete virtuale di Azure:

1. Andare troppo[portale di Azure](https://portal.azure.com).
2. Controllare hello **Panoramica** pagina hello virtuali del gateway di rete per informazioni sul tipo hello.
    
    ![Panoramica di Hello del gateway hello](media\vpn-gateway-troubleshoot-site-to-site-disconnected-intermittently\gatewayoverview.png)

### <a name="step-1-check-whether-hello-on-premises-vpn-device-is-validated"></a>Passaggio 1 verificare se hello locale viene convalidato il dispositivo VPN

1. Controllare se si usano un [dispositivo VPN e una versione del sistema operativo convalidati](vpn-gateway-about-vpn-devices.md#devicetable). Se il dispositivo VPN hello non viene convalidato, è possibile toocontact hello dispositivo produttore toosee se è presente qualsiasi problema di compatibilità.
2. Verificare che il dispositivo VPN hello sia configurato correttamente. Per altre informazioni, vedere [Esempi di modifica di configurazione dispositivo](vpn-gateway-about-vpn-devices.md#editing).

### <a name="step-2-check-hello-security-association-settingsfor-policy-based-azure-virtual-network-gateways"></a>Passaggio 2 delle impostazioni di associazione di sicurezza hello controllo (per i gateway basato su criteri di rete virtuale di Azure)

1. Verificare che tale rete virtuale hello, subnet e gli intervalli hello **gateway di rete locale** definizione in Microsoft Azure sono uguali a quelli di configurazione di hello sul dispositivo VPN locale di hello.
2. Verificare che soddisfano le impostazioni di associazione di sicurezza hello.

### <a name="step-3-check-for-user-defined-routes-or-network-security-groups-on-gateway-subnet"></a>Passaggio 3 Cercare le route definite dall'utente o i gruppi di sicurezza di rete nella subnet gateway

Una route definita dall'utente nella subnet del gateway hello può essere parte del traffico di limitazione ed altro traffico. In questo modo vengono visualizzate che connessione VPN hello è attendibile per una parte del traffico e consigliabile per gli altri utenti. 

### <a name="step-4-check-hello-one-vpn-tunnel-per-subnet-pair-setting-for-policy-based-virtual-network-gateways"></a>Passaggio 4 controllo hello "un Tunnel VPN per ogni coppia Subnet" impostazione (per i gateway di rete virtuale basata su criteri)

Verificare che tale hello locale dispositivo VPN è impostato toohave **un tunnel VPN per ogni coppia subnet** per gateway di rete virtuale basata su criteri.

### <a name="step-5-check-for-security-association-limitation-for-policy-based-virtual-network-gateways"></a>Passaggio 5 Controllare la limitazione di associazione di sicurezza (per i gateway di rete virtuale basati su criteri)

gateway di rete virtuale basata su criteri Hello ha un limite di 200 coppie di associazione di sicurezza di subnet. Se il numero di hello di subnet di rete virtuale di Azure moltiplicato volte per hello numero di subnet locale è maggiore di 200, subnet sporadici disconnessione.

### <a name="step-6-check-on-premises-vpn-device-external-interface-address"></a>Passaggio 6 Controllare l'indirizzo dell'interfaccia esterna del dispositivo VPN locale

- Se hello indirizzo IP del dispositivo VPN hello è connessa a Internet è incluso in hello **gateway di rete locale** definizione in Azure, potrebbero verificarsi sporadici disconnessioni.
- Hello interfaccia esterna del dispositivo deve essere direttamente su Internet hello. Non deve esistere alcun Network Address Translation (NAT) o un firewall tra hello Internet e il dispositivo di hello.
-  Se si configura Firewall Clustering toohave un indirizzo IP virtuale, è necessario interrompere cluster hello ed esporre un accessorio VPN hello direttamente l'interfaccia pubblica tooa che hello gateway può interfacciarsi con.

### <a name="step-7-check-whether-hello-on-premises-vpn-device-has-perfect-forward-secrecy-enabled"></a>Passaggio 7 di controllo se hello locale dispositivo VPN è l'impostazione di PFS abilitato

Hello **Perfect Forward Secrecy** funzionalità può causare problemi di disconnessione hello. Se il dispositivo VPN hello è **perfetto PFS** abilitato, disabilitare la funzionalità di hello. Quindi [aggiornare i criteri IPsec gateway di rete virtuale hello](vpn-gateway-ipsecikepolicy-rm-powershell.md#managepolicy).

## <a name="next-steps"></a>Passaggi successivi

- [Configurare una connessione Site-to-Site tooa la rete virtuale](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
- [Configure IPsec/IKE policy for Site-to-Site VPN connections (Configurare i criteri IPsec/IKE per le connessioni VPN da sito a sito)](vpn-gateway-ipsecikepolicy-rm-powershell.md)

