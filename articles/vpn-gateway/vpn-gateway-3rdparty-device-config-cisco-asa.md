---
title: configurazione aaaSample - dispositivi ASA Cisco connessione gateway VPN tooAzure | Documenti Microsoft
description: Questo articolo fornisce un esempio di configurazione per dispositivi Cisco ASA connessione gateway VPN tooAzure.
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: 
ms.assetid: a8bfc955-de49-4172-95ac-5257e262d7ea
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/20/2017
ms.author: yushwang
ms.openlocfilehash: dad13e02afe8dad2379db750eb09602e08e8ea99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="sample-configuration-cisco-asa-device-ikev2no-bgp"></a>Configurazione di esempio: dispositivo Cisco ASA (IKEv2/senza BGP)
Questo articolo fornisce le configurazioni di esempio per i dispositivi ASA Cisco connessione gateway VPN tooAzure.

## <a name="device-at-a-glance"></a>Informazioni sul dispositivo

|                        |                                   |
| ---                    | ---                               |
| Fornitore del dispositivo          | Cisco                             |
| Modello del dispositivo           | ASA (Adaptive Security Appliance) |
| Versione finale         | 8.4+                              |
| Modello testato           | ASA 5505                          |
| Versione testata         | 9.2                               |
| Versione IKE            | **IKEv2**                         |
| BGP                    | **No**                            |
| Tipo di gateway VPN di Azure | Gateway VPN **basato su route**       |
|                        |                                   |

> [!NOTE]
> 1. configurazione di Hello indicata di seguito si connette un tooan di dispositivi ASA Cisco Azure **basato su route** gateway VPN usando i criteri IPsec/IKE personalizzate con l'opzione "UserPolicyBasedTrafficSelectors", come descritto in [in questo articolo](vpn-gateway-connect-multiple-policybased-rm-ps.md).
> 2. È necessario toouse di dispositivi ASA **IKEv2** con configurazioni basata sull'elenco di accesso, non basato su VTI.
> 3. Consultare con le specifiche del fornitore dispositivo VPN criteri hello tooensure sono supportato nei dispositivi VPN locali.

## <a name="vpn-device-requirements"></a>Requisiti del dispositivo VPN
I gateway VPN di Azure usare tunnel VPN S2S standard IPsec/IKE protocollo gruppi tooestablish. Fare riferimento troppo[informazioni sui dispositivi VPN](vpn-gateway-about-vpn-devices.md) per hello dettagliato i parametri del protocollo IPsec/IKE e gli algoritmi di crittografia predefinita per i gateway VPN di Azure. È possibile specificare facoltativamente l'esatta combinazione di hello di algoritmi di crittografia e vantaggi chiave per una connessione specifica come descritto in [sui requisiti di crittografia](vpn-gateway-about-compliance-crypto.md). Se si seleziona una specifica combinazione di algoritmi di crittografia e i punti di forza di chiave, verificare che si utilizzano specifiche corrispondenti hello nei dispositivi VPN.

## <a name="single-vpn-tunnel"></a>Tunnel per VPN unico
Questa topologia consiste in un unico tunnel per VPN S2S tra un gateway VPN di Azure e il dispositivo VPN locale. È possibile configurare BGP attraverso i tunnel VPN hello.

![tunnel unico](./media/vpn-gateway-3rdparty-device-config-cisco-asa/singletunnel.png)

Fare riferimento troppo[il programma di installazione singolo tunnel](vpn-gateway-3rdparty-device-config-overview.md#singletunnel) per dettagliate, istruzioni dettagliate toobuild hello Azure configurazioni.

### <a name="network-and-vpn-gateway-information"></a>Informazioni sul gateway di rete e VPN
In questa sezione elenca i parametri di hello per hello in questo esempio.

| **Parametro**                | **Valore**                    |
| ---                          | ---                          |
| Prefissi di indirizzi di rete virtuale        | 10.11.0.0/16<br>10.12.0.0/16 |
| Indirizzo IP del gateway VPN di Azure         | Azure_Gateway_Public_IP      |
| Prefissi di indirizzi locali | 10.51.0.0/16<br>10.52.0.0/16 |
| Indirizzo IP del dispositivo VPN locale    | OnPrem_Device_Public_IP     |
| *BGP ASN della rete virtuale                | 65010                        |
| *Indirizzo IP del peer BGP di Azure           | 10.12.255.30                 |
| *ASN BGP locale         | 65050                        |
| *Indirizzo IP del peer BGP locale     | 10.52.255.254                |
|                              |                              |

* (*) Parametri facoltativi solo per BGP.

### <a name="ipsecike-policy--parameters"></a>Criteri e parametri IPsec/IKE

tabella Hello riportata di seguito sono elencati gli algoritmi IPsec/IKE hello e parametri utilizzati nell'esempio hello. Consultare il toomake specifiche di dispositivo VPN che tutti gli algoritmi elencati sopra sono supportati i modelli del dispositivo VPN e le versioni del firmware.

| **IPsec/IKEv2**  | **Valore**                            |
| ---              | ---                                  |
| Crittografia IKEv2 | AES256                               |
| Integrità IKEv2  | SHA384                               |
| Gruppo DH         | DHGroup24                            |
| Crittografia IPsec | AES256                               |
| Integrità IPsec  | SHA1                                 |
| Gruppo PFS        | PFS24                                |
| Durata associazione di sicurezza QM   | 7200 secondi                         |
| Selettore di traffico | UsePolicyBasedTrafficSelectors $True |
| Chiave precondivisa   | PreSharedKey                         |
|                  |                                      |

- (*) Su alcuni dispositivi, l'integrità IPsec deve essere "null" se GCM-AES viene usato come algoritmo di crittografia IPsec.

### <a name="device-notes"></a>Note sul dispositivo

>[!NOTE]
>
> 1. Il supporto per IKEv2 richiede ASA 8.4 e versioni successive.
> 2. Il supporto del gruppo PFS e DH superiore, superiore al gruppo 5, richiede la versione ASA 9.x.
> 3. La crittografia IPsec con l'integrità IPsec e AES-GCM con il supporto SHA-256, SHA-384, SHA-512 richiede la versione ASA 9.x sull'hardware ASA più recente; ASA 5505, 5510, 5520, 5540, 5550, 5580 **non** sono supportati. (Verificare hello fornitore specifiche tooconfirm).
>


### <a name="sample-device-configurations"></a>Esempi di configurazioni del dispositivo
script Hello riportato di seguito fornisce un esempio di configurazione in base alla topologia hello e parametri sopra elencati. configurazione di tunnel VPN S2S Hello è costituita da hello seguenti parti:

1. Interfacce e route
2. Elenchi di accesso
3. Criterio IKE e parametri (fase 1 o in modalità principale)
4. Criterio IKE e parametri (fase 2 o in modalità rapida)
5. Altri parametri (fissaggio MSS TCP e così via)

>[!IMPORTANT] 
>Assicurarsi di aver completato elencata di seguito la configurazione aggiuntiva hello e sostituire i segnaposto hello con i valori effettivi hello:
> 
> - Configurazione dell'interfaccia per le interfacce interne ed esterne
> - Route per le reti esterne/pubbliche e interne/private
> - Assicurarsi che tutti i nomi e i numeri dei criteri siano univoci nel dispositivo hello
> - Verificare che nel dispositivo sono supportati gli algoritmi di crittografia di hello
> - Sostituire i seguenti segnaposto con valori effettivi hello hello
>   - Nome dell'interfaccia esterna: "esterno"
>   - Azure_Gateway_Public_IP
>   - OnPrem_Device_Public_IP
>   - IKE Pre_Shared_Key
>   - Nomi per i gateway di rete locale e virtuale (VNetName, LNGName)
>   - Prefissi dell'indirizzo di rete locale e virtuale
>   - Netmask appropriate

#### <a name="sample-configuration"></a>Configurazione di esempio

```
! Sample ASA configuration for connecting tooAzure VPN gateway
!
! Tested hardware: ASA 5505
! Tested version:  ASA version 9.2(4)
!
! Replace hello following place holders with your actual values:
!   - Interface names - default are "outside" and "inside"
!   - <Azure_Gateway_Public_IP>
!   - <OnPrem_Device_Public_IP>
!   - <Pre_Shared_Key>
!   - <VNetName>*
!   - <LNGName>* ==> LocalNetworkGateway - hello Azure resource that represents the
!     on-premises network, specifies network prefixes, device public IP, BGP info, etc.
!   - <PrivateIPAddress> ==> Replace it with a private IP address if applicable
!   - <Netmask> ==> Replace it with appropriate netmasks
!   - <Nexthop> ==> Replace it with hello actual nexthop IP address
!
! (*) Must be unique names in hello device configuration
!
! ==> Interface & route configurations
!
!     > <OnPrem_Device_Public_IP> address on hello outside interface or vlan
!     > <PrivateIPAddress> on hello inside interface or vlan; e.g., 10.51.0.1/24
!     > Route tooconnect too<Azure_Gateway_Public_IP> address
!
!     > Example:
!
!       interface Ethernet0/0
!        switchport access vlan 2
!       exit
!
!       interface vlan 1
!        nameif inside
!        security-level 100
!        ip address <PrivateIPAddress> <Netmask>
!       exit
!
!       interface vlan 2
!        nameif outside
!        security-level 0
!        ip address <OnPrem_Device_Public_IP> <Netmask>
!       exit
!
!       route outside 0.0.0.0 0.0.0.0 <NextHop IP> 1
!
! ==> Access lists
!
!     > Most firewall devices deny all traffic by default. Create access lists to
!       (1) Allow S2S VPN tunnels between hello ASA and hello Azure gateway public IP address
!       (2) Construct traffic selectors as part of IPsec policy or proposal
!
access-list outside_access_in extended permit ip host <Azure_Gateway_Public_IP> host <OnPrem_Device_Public_IP>
!
!     > Object group that consists of all VNet prefixes (e.g., 10.11.0.0/16 &
!       10.12.0.0/16)
!
object-group network Azure-<VNetName>
 description Azure virtual network <VNetName> prefixes
 network-object 10.11.0.0 255.255.0.0
 network-object 10.12.0.0 255.255.0.0
exit
!
!     > Object group that corresponding toohello <LNGName> prefixes.
!       E.g., 10.51.0.0/16 and 10.52.0.0/16. Note that LNG = "local network gateway".
!       In Azure network resource, a local network gateway defines hello on-premises
!       network properties (address prefixes, VPN device IP, BGP ASN, etc.)
!
object-group network <LNGName>
 description On-Premises network <LNGName> prefixes
 network-object 10.51.0.0 255.255.0.0
 network-object 10.52.0.0 255.255.0.0
exit
!
!     > Specify hello access-list between hello Azure VNet and your on-premises network.
!       This access list defines hello IPsec SA traffic selectors.
!
access-list Azure-<VNetName>-acl extended permit ip object-group <LNGName> object-group Azure-<VNetName>
!
!     > No NAT required between hello on-premises network and Azure VNet
!
nat (inside,outside) source static <LNGName> <LNGName> destination static Azure-<VNetName> Azure-<VNetName>
!
! ==> IKEv2 configuration
!
!     > General IKEv2 configuration - enable IKEv2 for VPN
!
group-policy DfltGrpPolicy attributes
 vpn-tunnel-protocol ikev1 ikev2
exit
!
crypto isakmp identity address
crypto ikev2 enable outside
!
!     > Define IKEv2 Phase 1/Main Mode policy
!       - Make sure hello policy number is not used
!       - integrity and prf must be hello same
!       - DH group 14 and above require ASA version 9.x.
!
crypto ikev2 policy 1
 encryption       aes-256
 integrity        sha384
 prf              sha384
 group            24
 lifetime seconds 86400
exit
!
!     > Set connection type and pre-shared key
!
tunnel-group <Azure_Gateway_Public_IP> type ipsec-l2l
tunnel-group <Azure_Gateway_Public_IP> ipsec-attributes
 ikev2 remote-authentication pre-shared-key <Pre_Shared_Key> 
 ikev2 local-authentication  pre-shared-key <Pre_Shared_Key> 
exit
!
! ==> IPsec configuration
!
!     > IKEv2 Phase 2/Quick Mode proposal
!       - AES-GCM and SHA-2 requires ASA version 9.x on newer ASA models. ASA
!         5505, 5510, 5520, 5540, 5550, 5580 are not supported.
!       - ESP integrity must be null if AES-GCM is configured as ESP encryption
!
crypto ipsec ikev2 ipsec-proposal AES-256
 protocol esp encryption aes-256
 protocol esp integrity  sha-1
exit
!
!     > Set access list & traffic selectors, PFS, IPsec protposal, SA lifetime
!       - This sample uses "Azure-<VNetName>-map" as hello crypto map name
!       - ASA supports only one crypto map per interface, if you already have
!         an existing crypto map assigned tooyour outside interface, you must use
!         hello same crypto map name, but with a different sequence number for
!         this policy
!       - "match address" policy uses hello access-list "Azure-<VNetName>-acl" defined 
!         previously
!       - "ipsec-proposal" uses hello proposal "AES-256" defined previously 
!       - PFS groups 14 and beyond requires ASA version 9.x.
!
crypto map Azure-<VNetName>-map 1 match address Azure-<VNetName>-acl
crypto map Azure-<VNetName>-map 1 set pfs group24
crypto map Azure-<VNetName>-map 1 set peer <Azure_Gateway_Public_IP>
crypto map Azure-<VNetName>-map 1 set ikev2 ipsec-proposal AES-256
crypto map Azure-<VNetName>-map 1 set security-association lifetime seconds 7200
crypto map Azure-<VNetName>-map interface outside
!
! ==> Set TCP MSS too1350
!
sysopt connection tcpmss 1350
!
```

## <a name="simple-debugging-commands"></a>Semplici comandi di debug

Ecco alcuni comandi ASA a scopo di debug:

1. Mostra hello IPsec e IKE dell'account SA
    - "show crypto ipsec sa"
    - "show crypto ikev2 sa"
2. Se si immette la modalità di debug, si può ottenere molto poco significativi nella console di hello
    - "debug crypto ikev2 platform <level>"
    - "debug crypto ikev2 protocol <level>"
3. Elenco delle configurazioni attuali
    - "Mostra esecuzione" - Mostra hello configurazioni correnti sul dispositivo hello è possibile utilizzare varie parti specifiche in toolist sottocomandi della configurazione hello hello. Ad esempio "show run crypto", "show run access-list", "show run tunnel-group" e così via.


## <a name="next-steps"></a>Passaggi successivi
Vedere [la configurazione di gateway VPN attivo-attivo per Cross-premise e le connessioni di rete virtuale a](vpn-gateway-activeactive-rm-powershell.md) per passaggi tooconfigure attivo-attivo cross-premise e connessioni di rete virtuale a.

