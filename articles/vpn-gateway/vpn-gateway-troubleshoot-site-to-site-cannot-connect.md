---
title: "aaaTroubleshoot una connessione VPN da sito a sito Azure non è possibile connettersi | Documenti Microsoft"
description: "Informazioni su come tootroubleshoot una connessione VPN da sito a sito che potrebbe trovarsi improvvisamente smette di funzionare e non può essere riconnessa."
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
ms.openlocfilehash: 632c75bfcfb93a532eeead2855d43e6614569a99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-an-azure-site-to-site-vpn-connection-cannot-connect-and-stops-working"></a>Risoluzione dei problemi: una connessione VPN da sito a sito di Azure non può essere stabilita e smette di funzionare

Dopo aver configurato una connessione VPN da sito a sito tra una rete locale e una rete virtuale di Azure, hello connessione VPN improvvisamente smette di funzionare e non può essere riconnessa. Questo articolo fornisce la risoluzione dei problemi toohelp passaggi risolvere il problema. 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-steps"></a>Passaggi per la risoluzione dei problemi

problema di hello tooresolve, provare troppo[gateway VPN di Azure di reimpostazione hello](vpn-gateway-resetgw-classic.md) e reimpostare il tunnel hello dal dispositivo VPN locale di hello. Se hello problema persiste, seguire questi causa hello tooidentify di passaggi di problema hello.

### <a name="prerequisite-step"></a>Passaggio preliminare

Controllare il tipo di hello del gateway VPN di Azure hello.

1. Passare toohello [portale di Azure](https://portal.azure.com).

2. Controllare hello **Panoramica** pagina del gateway VPN hello per le informazioni sul tipo hello.
    
    ![Panoramica del gateway hello](media\vpn-gateway-troubleshoot-site-to-site-cannot-connect\gatewayoverview.png)

### <a name="step-1-check-whether-hello-on-premises-vpn-device-is-validated"></a>Passaggio 1. Controllare se viene convalidato dispositivo VPN locale di hello

1. Controllare se si usano un [dispositivo VPN e una versione del sistema operativo convalidati](vpn-gateway-about-vpn-devices.md#devicetable). Se il dispositivo di hello non è un dispositivo VPN convalidato, potrebbe essere toocontact hello dispositivo produttore toosee se è presente un problema di compatibilità.

2. Verificare che il dispositivo VPN hello sia configurato correttamente. Per altre informazioni, vedere [Esempi di modifica di configurazione dispositivo](/vpn-gateway-about-vpn-devices.md#editing).

### <a name="step-2-verify-hello-shared-key"></a>Passaggio 2. Verificare la chiave condivisa hello

Confrontare una chiave condivisa per hello locale VPN dispositivo toohello VPN di rete virtuale di Azure toomake che le chiavi di hello corrispondano hello. 

chiave condivisa di hello tooview per hello connessione VPN di Azure, utilizzare uno dei seguenti metodi hello:

**Portale di Azure**

1. Passare toohello VPN site-to-site connessione del gateway creato.

2. In hello **impostazioni** fare clic su **chiave condivisa**.
    
    ![Chiave condivisa](media/vpn-gateway-troubleshoot-site-to-site-cannot-connect/sharedkey.png)

**Azure PowerShell**

Per il modello di distribuzione Azure Resource Manager hello:

    Get-AzureRmVirtualNetworkGatewayConnectionSharedKey -Name <Connection name> -ResourceGroupName <Resource group name>

Per il modello di distribuzione classica hello:

    Get-AzureVNetGatewayKey -VNetName -LocalNetworkSiteName

### <a name="step-3-verify-hello-vpn-peer-ips"></a>Passaggio 3. Verificare il peer VPN hello gli indirizzi IP

-   definizione di IP in hello Hello **Gateway di rete locale** oggetto in Azure deve corrispondere hello IP del dispositivo locale.
-   definizione di IP gateway di Azure che è impostato su hello Hello locale dispositivo deve corrispondere hello Azure gateway IP.

### <a name="step-4-check-udr-and-nsgs-on-hello-gateway-subnet"></a>Passaggio 4. Controllare UDR e NSGs nella subnet del gateway hello

Cercare e rimuovere routing definito dall'utente (UDR) o rete sicurezza gruppi di nella subnet del gateway hello e quindi il risultato di hello del test. Se il problema di hello viene risolto, convalidare le impostazioni di hello che UDR o gruppo applicato.

### <a name="step-5-check-hello-on-premises-vpn-device-external-interface-address"></a>Passaggio 5. Controllare l'indirizzo interfaccia esterna del dispositivo VPN locale hello

- Se hello indirizzo IP con connessione Internet del dispositivo VPN hello è incluso in hello **rete locale** definizione in Azure, potrebbero verificarsi sporadici disconnessioni.
- Hello interfaccia esterna del dispositivo deve essere direttamente su Internet hello. Non deve esistere alcuna conversione indirizzi di rete o un firewall tra hello Internet e il dispositivo di hello.
- tooconfigure firewall clustering toohave un indirizzo IP virtuale, è necessario interrompere cluster hello ed esporre un accessorio VPN hello direttamente l'interfaccia pubblica tooa tale gateway hello può interfacciarsi con.

### <a name="step-6-verify-that-hello-subnets-match-exactly-azure-policy-based-gateways"></a>Passaggio 6. Verificare che corrispondano esattamente a subnet hello (gateway basato su criteri di Azure)

-   Verificare che le subnet hello corrispondano esattamente tra hello rete virtuale di Azure e le definizioni locali per hello rete virtuale di Azure.
-   Verificare che le subnet hello corrispondano esattamente tra hello **Gateway di rete locale** e le definizioni per la rete locale hello in locale.

### <a name="step-7-verify-hello-azure-gateway-health-probe"></a>Passaggio 7. Verificare i probe di integrità hello gateway di Azure

1. Passare toohello [probe di integrità](https://&lt;YourVirtualNetworkGatewayIP&gt;:8081/healthprobe).

2. Fare clic sulle avviso certificato hello.
3. Se si riceve una risposta, i gateway VPN hello è considerato integro. Se si non riceve una risposta, potrebbe non essere integro gateway hello o un gruppo nella subnet del gateway hello problema hello. Dopo il testo Hello è una risposta di esempio:

    &lt;?xml version="1.0"?&gt;  <string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">Primary Instance: GatewayTenantWorker_IN_1 GatewayTenantVersion: 14.7.24.6&lt;/string&gt;

### <a name="step-8-check-whether-hello-on-premises-vpn-device-has-hello-perfect-forward-secrecy-feature-enabled"></a>Passaggio 8. Controllare se hello locale dispositivo VPN è abilitata la funzionalità funzionalità PFS hello

funzionalità di funzionalità PFS Hello può causare problemi di disconnessione. Se il dispositivo VPN hello dispone di funzionalità PFS abilitata, disabilitare funzionalità hello. Aggiornare i criteri IPsec gateway VPN hello.

## <a name="next-steps"></a>Passaggi successivi

-   [Configurare una rete virtuale di tooa connessione site-to-site](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
-   [Configurare criteri IPsec/IKE per connessioni VPN da sito a sito o da rete virtuale a rete virtuale](vpn-gateway-ipsecikepolicy-rm-powershell.md)
