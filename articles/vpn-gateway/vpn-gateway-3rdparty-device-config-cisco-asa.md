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
# <a name="sample-configuration-cisco-asa-device-ikev2no-bgp"></a><span data-ttu-id="f35cc-103">Configurazione di esempio: dispositivo Cisco ASA (IKEv2/senza BGP)</span><span class="sxs-lookup"><span data-stu-id="f35cc-103">Sample configuration: Cisco ASA device (IKEv2/no BGP)</span></span>
<span data-ttu-id="f35cc-104">Questo articolo fornisce le configurazioni di esempio per i dispositivi ASA Cisco connessione gateway VPN tooAzure.</span><span class="sxs-lookup"><span data-stu-id="f35cc-104">This article provides sample configurations for Cisco ASA devices connecting tooAzure VPN gateways.</span></span>

## <a name="device-at-a-glance"></a><span data-ttu-id="f35cc-105">Informazioni sul dispositivo</span><span class="sxs-lookup"><span data-stu-id="f35cc-105">Device at a glance</span></span>

|                        |                                   |
| ---                    | ---                               |
| <span data-ttu-id="f35cc-106">Fornitore del dispositivo</span><span class="sxs-lookup"><span data-stu-id="f35cc-106">Device vendor</span></span>          | <span data-ttu-id="f35cc-107">Cisco</span><span class="sxs-lookup"><span data-stu-id="f35cc-107">Cisco</span></span>                             |
| <span data-ttu-id="f35cc-108">Modello del dispositivo</span><span class="sxs-lookup"><span data-stu-id="f35cc-108">Device model</span></span>           | <span data-ttu-id="f35cc-109">ASA (Adaptive Security Appliance)</span><span class="sxs-lookup"><span data-stu-id="f35cc-109">ASA (Adaptive Security Appliance)</span></span> |
| <span data-ttu-id="f35cc-110">Versione finale</span><span class="sxs-lookup"><span data-stu-id="f35cc-110">Target version</span></span>         | <span data-ttu-id="f35cc-111">8.4+</span><span class="sxs-lookup"><span data-stu-id="f35cc-111">8.4+</span></span>                              |
| <span data-ttu-id="f35cc-112">Modello testato</span><span class="sxs-lookup"><span data-stu-id="f35cc-112">Tested model</span></span>           | <span data-ttu-id="f35cc-113">ASA 5505</span><span class="sxs-lookup"><span data-stu-id="f35cc-113">ASA 5505</span></span>                          |
| <span data-ttu-id="f35cc-114">Versione testata</span><span class="sxs-lookup"><span data-stu-id="f35cc-114">Tested version</span></span>         | <span data-ttu-id="f35cc-115">9.2</span><span class="sxs-lookup"><span data-stu-id="f35cc-115">9.2</span></span>                               |
| <span data-ttu-id="f35cc-116">Versione IKE</span><span class="sxs-lookup"><span data-stu-id="f35cc-116">IKE version</span></span>            | <span data-ttu-id="f35cc-117">**IKEv2**</span><span class="sxs-lookup"><span data-stu-id="f35cc-117">**IKEv2**</span></span>                         |
| <span data-ttu-id="f35cc-118">BGP</span><span class="sxs-lookup"><span data-stu-id="f35cc-118">BGP</span></span>                    | <span data-ttu-id="f35cc-119">**No**</span><span class="sxs-lookup"><span data-stu-id="f35cc-119">**No**</span></span>                            |
| <span data-ttu-id="f35cc-120">Tipo di gateway VPN di Azure</span><span class="sxs-lookup"><span data-stu-id="f35cc-120">Azure VPN gateway type</span></span> | <span data-ttu-id="f35cc-121">Gateway VPN **basato su route**</span><span class="sxs-lookup"><span data-stu-id="f35cc-121">**Route-based** VPN gateway</span></span>       |
|                        |                                   |

> [!NOTE]
> 1. <span data-ttu-id="f35cc-122">configurazione di Hello indicata di seguito si connette un tooan di dispositivi ASA Cisco Azure **basato su route** gateway VPN usando i criteri IPsec/IKE personalizzate con l'opzione "UserPolicyBasedTrafficSelectors", come descritto in [in questo articolo](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="f35cc-122">hello configuration below connects a Cisco ASA device tooan Azure **route-based** VPN gateway using custom IPsec/IKE policy with "UserPolicyBasedTrafficSelectors" option, as described in [this article](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span></span>
> 2. <span data-ttu-id="f35cc-123">È necessario toouse di dispositivi ASA **IKEv2** con configurazioni basata sull'elenco di accesso, non basato su VTI.</span><span class="sxs-lookup"><span data-stu-id="f35cc-123">It requires ASA devices toouse **IKEv2** with access-list-based configurations, not VTI-based.</span></span>
> 3. <span data-ttu-id="f35cc-124">Consultare con le specifiche del fornitore dispositivo VPN criteri hello tooensure sono supportato nei dispositivi VPN locali.</span><span class="sxs-lookup"><span data-stu-id="f35cc-124">Please consult with your VPN device vendor specifications tooensure hello policy is supported on your on-premises VPN devices.</span></span>

## <a name="vpn-device-requirements"></a><span data-ttu-id="f35cc-125">Requisiti del dispositivo VPN</span><span class="sxs-lookup"><span data-stu-id="f35cc-125">VPN device requirements</span></span>
<span data-ttu-id="f35cc-126">I gateway VPN di Azure usare tunnel VPN S2S standard IPsec/IKE protocollo gruppi tooestablish.</span><span class="sxs-lookup"><span data-stu-id="f35cc-126">Azure VPN gateways use standard IPsec/IKE protocol suites tooestablish S2S VPN tunnels.</span></span> <span data-ttu-id="f35cc-127">Fare riferimento troppo[informazioni sui dispositivi VPN](vpn-gateway-about-vpn-devices.md) per hello dettagliato i parametri del protocollo IPsec/IKE e gli algoritmi di crittografia predefinita per i gateway VPN di Azure.</span><span class="sxs-lookup"><span data-stu-id="f35cc-127">Refer too[About VPN devices](vpn-gateway-about-vpn-devices.md) for hello detailed IPsec/IKE protocol parameters and default cryptographic algorithms for Azure VPN gateways.</span></span> <span data-ttu-id="f35cc-128">È possibile specificare facoltativamente l'esatta combinazione di hello di algoritmi di crittografia e vantaggi chiave per una connessione specifica come descritto in [sui requisiti di crittografia](vpn-gateway-about-compliance-crypto.md).</span><span class="sxs-lookup"><span data-stu-id="f35cc-128">You can optionally specify hello exact combination of cryptographic algorithms and key strengths for a specific connection as described in [About cryptographic requirements](vpn-gateway-about-compliance-crypto.md).</span></span> <span data-ttu-id="f35cc-129">Se si seleziona una specifica combinazione di algoritmi di crittografia e i punti di forza di chiave, verificare che si utilizzano specifiche corrispondenti hello nei dispositivi VPN.</span><span class="sxs-lookup"><span data-stu-id="f35cc-129">If you select a specific combination of cryptographic algorithms and key strengths, please make sure you use hello corresponding specifications on your VPN devices.</span></span>

## <a name="single-vpn-tunnel"></a><span data-ttu-id="f35cc-130">Tunnel per VPN unico</span><span class="sxs-lookup"><span data-stu-id="f35cc-130">Single VPN tunnel</span></span>
<span data-ttu-id="f35cc-131">Questa topologia consiste in un unico tunnel per VPN S2S tra un gateway VPN di Azure e il dispositivo VPN locale.</span><span class="sxs-lookup"><span data-stu-id="f35cc-131">This topology consists of a single S2S VPN tunnel between an Azure VPN gateway and your on-premises VPN device.</span></span> <span data-ttu-id="f35cc-132">È possibile configurare BGP attraverso i tunnel VPN hello.</span><span class="sxs-lookup"><span data-stu-id="f35cc-132">You can optionally configure BGP across hello VPN tunnel.</span></span>

![tunnel unico](./media/vpn-gateway-3rdparty-device-config-cisco-asa/singletunnel.png)

<span data-ttu-id="f35cc-134">Fare riferimento troppo[il programma di installazione singolo tunnel](vpn-gateway-3rdparty-device-config-overview.md#singletunnel) per dettagliate, istruzioni dettagliate toobuild hello Azure configurazioni.</span><span class="sxs-lookup"><span data-stu-id="f35cc-134">Refer too[Single tunnel setup](vpn-gateway-3rdparty-device-config-overview.md#singletunnel) for detailed, step-by-step instructions toobuild hello Azure configurations.</span></span>

### <a name="network-and-vpn-gateway-information"></a><span data-ttu-id="f35cc-135">Informazioni sul gateway di rete e VPN</span><span class="sxs-lookup"><span data-stu-id="f35cc-135">Network and VPN gateway information</span></span>
<span data-ttu-id="f35cc-136">In questa sezione elenca i parametri di hello per hello in questo esempio.</span><span class="sxs-lookup"><span data-stu-id="f35cc-136">This section list hello parameters for hello this sample.</span></span>

| <span data-ttu-id="f35cc-137">**Parametro**</span><span class="sxs-lookup"><span data-stu-id="f35cc-137">**Parameter**</span></span>                | <span data-ttu-id="f35cc-138">**Valore**</span><span class="sxs-lookup"><span data-stu-id="f35cc-138">**Value**</span></span>                    |
| ---                          | ---                          |
| <span data-ttu-id="f35cc-139">Prefissi di indirizzi di rete virtuale</span><span class="sxs-lookup"><span data-stu-id="f35cc-139">VNet address prefixes</span></span>        | <span data-ttu-id="f35cc-140">10.11.0.0/16</span><span class="sxs-lookup"><span data-stu-id="f35cc-140">10.11.0.0/16</span></span><br><span data-ttu-id="f35cc-141">10.12.0.0/16</span><span class="sxs-lookup"><span data-stu-id="f35cc-141">10.12.0.0/16</span></span> |
| <span data-ttu-id="f35cc-142">Indirizzo IP del gateway VPN di Azure</span><span class="sxs-lookup"><span data-stu-id="f35cc-142">Azure VPN gateway IP</span></span>         | <span data-ttu-id="f35cc-143">Azure_Gateway_Public_IP</span><span class="sxs-lookup"><span data-stu-id="f35cc-143">Azure_Gateway_Public_IP</span></span>      |
| <span data-ttu-id="f35cc-144">Prefissi di indirizzi locali</span><span class="sxs-lookup"><span data-stu-id="f35cc-144">On-premises address prefixes</span></span> | <span data-ttu-id="f35cc-145">10.51.0.0/16</span><span class="sxs-lookup"><span data-stu-id="f35cc-145">10.51.0.0/16</span></span><br><span data-ttu-id="f35cc-146">10.52.0.0/16</span><span class="sxs-lookup"><span data-stu-id="f35cc-146">10.52.0.0/16</span></span> |
| <span data-ttu-id="f35cc-147">Indirizzo IP del dispositivo VPN locale</span><span class="sxs-lookup"><span data-stu-id="f35cc-147">On-premises VPN device IP</span></span>    | <span data-ttu-id="f35cc-148">OnPrem_Device_Public_IP</span><span class="sxs-lookup"><span data-stu-id="f35cc-148">OnPrem_Device_Public_IP</span></span>     |
| <span data-ttu-id="f35cc-149">*BGP ASN della rete virtuale</span><span class="sxs-lookup"><span data-stu-id="f35cc-149">*VNet BGP ASN</span></span>                | <span data-ttu-id="f35cc-150">65010</span><span class="sxs-lookup"><span data-stu-id="f35cc-150">65010</span></span>                        |
| <span data-ttu-id="f35cc-151">*Indirizzo IP del peer BGP di Azure</span><span class="sxs-lookup"><span data-stu-id="f35cc-151">*Azure BGP peer IP</span></span>           | <span data-ttu-id="f35cc-152">10.12.255.30</span><span class="sxs-lookup"><span data-stu-id="f35cc-152">10.12.255.30</span></span>                 |
| <span data-ttu-id="f35cc-153">*ASN BGP locale</span><span class="sxs-lookup"><span data-stu-id="f35cc-153">*On-premises BGP ASN</span></span>         | <span data-ttu-id="f35cc-154">65050</span><span class="sxs-lookup"><span data-stu-id="f35cc-154">65050</span></span>                        |
| <span data-ttu-id="f35cc-155">*Indirizzo IP del peer BGP locale</span><span class="sxs-lookup"><span data-stu-id="f35cc-155">*On-premises BGP peer IP</span></span>     | <span data-ttu-id="f35cc-156">10.52.255.254</span><span class="sxs-lookup"><span data-stu-id="f35cc-156">10.52.255.254</span></span>                |
|                              |                              |

* <span data-ttu-id="f35cc-157">(*) Parametri facoltativi solo per BGP.</span><span class="sxs-lookup"><span data-stu-id="f35cc-157">(*) Optional parameters for BGP only.</span></span>

### <a name="ipsecike-policy--parameters"></a><span data-ttu-id="f35cc-158">Criteri e parametri IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="f35cc-158">IPsec/IKE policy & parameters</span></span>

<span data-ttu-id="f35cc-159">tabella Hello riportata di seguito sono elencati gli algoritmi IPsec/IKE hello e parametri utilizzati nell'esempio hello.</span><span class="sxs-lookup"><span data-stu-id="f35cc-159">hello table below lists hello IPsec/IKE algorithms and parameters used in hello sample.</span></span> <span data-ttu-id="f35cc-160">Consultare il toomake specifiche di dispositivo VPN che tutti gli algoritmi elencati sopra sono supportati i modelli del dispositivo VPN e le versioni del firmware.</span><span class="sxs-lookup"><span data-stu-id="f35cc-160">Please consult your VPN device specifications toomake sure all algorithms listed above are supported by your VPN device models and firmware versions.</span></span>

| <span data-ttu-id="f35cc-161">**IPsec/IKEv2**</span><span class="sxs-lookup"><span data-stu-id="f35cc-161">**IPsec/IKEv2**</span></span>  | <span data-ttu-id="f35cc-162">**Valore**</span><span class="sxs-lookup"><span data-stu-id="f35cc-162">**Value**</span></span>                            |
| ---              | ---                                  |
| <span data-ttu-id="f35cc-163">Crittografia IKEv2</span><span class="sxs-lookup"><span data-stu-id="f35cc-163">IKEv2 Encryption</span></span> | <span data-ttu-id="f35cc-164">AES256</span><span class="sxs-lookup"><span data-stu-id="f35cc-164">AES256</span></span>                               |
| <span data-ttu-id="f35cc-165">Integrità IKEv2</span><span class="sxs-lookup"><span data-stu-id="f35cc-165">IKEv2 Integrity</span></span>  | <span data-ttu-id="f35cc-166">SHA384</span><span class="sxs-lookup"><span data-stu-id="f35cc-166">SHA384</span></span>                               |
| <span data-ttu-id="f35cc-167">Gruppo DH</span><span class="sxs-lookup"><span data-stu-id="f35cc-167">DH Group</span></span>         | <span data-ttu-id="f35cc-168">DHGroup24</span><span class="sxs-lookup"><span data-stu-id="f35cc-168">DHGroup24</span></span>                            |
| <span data-ttu-id="f35cc-169">Crittografia IPsec</span><span class="sxs-lookup"><span data-stu-id="f35cc-169">IPsec Encryption</span></span> | <span data-ttu-id="f35cc-170">AES256</span><span class="sxs-lookup"><span data-stu-id="f35cc-170">AES256</span></span>                               |
| <span data-ttu-id="f35cc-171">Integrità IPsec</span><span class="sxs-lookup"><span data-stu-id="f35cc-171">IPsec Integrity</span></span>  | <span data-ttu-id="f35cc-172">SHA1</span><span class="sxs-lookup"><span data-stu-id="f35cc-172">SHA1</span></span>                                 |
| <span data-ttu-id="f35cc-173">Gruppo PFS</span><span class="sxs-lookup"><span data-stu-id="f35cc-173">PFS Group</span></span>        | <span data-ttu-id="f35cc-174">PFS24</span><span class="sxs-lookup"><span data-stu-id="f35cc-174">PFS24</span></span>                                |
| <span data-ttu-id="f35cc-175">Durata associazione di sicurezza QM</span><span class="sxs-lookup"><span data-stu-id="f35cc-175">QM SA Lifetime</span></span>   | <span data-ttu-id="f35cc-176">7200 secondi</span><span class="sxs-lookup"><span data-stu-id="f35cc-176">7200 seconds</span></span>                         |
| <span data-ttu-id="f35cc-177">Selettore di traffico</span><span class="sxs-lookup"><span data-stu-id="f35cc-177">Traffic Selector</span></span> | <span data-ttu-id="f35cc-178">UsePolicyBasedTrafficSelectors $True</span><span class="sxs-lookup"><span data-stu-id="f35cc-178">UsePolicyBasedTrafficSelectors $True</span></span> |
| <span data-ttu-id="f35cc-179">Chiave precondivisa</span><span class="sxs-lookup"><span data-stu-id="f35cc-179">Pre-Shared Key</span></span>   | <span data-ttu-id="f35cc-180">PreSharedKey</span><span class="sxs-lookup"><span data-stu-id="f35cc-180">PreSharedKey</span></span>                         |
|                  |                                      |

- <span data-ttu-id="f35cc-181">(*) Su alcuni dispositivi, l'integrità IPsec deve essere "null" se GCM-AES viene usato come algoritmo di crittografia IPsec.</span><span class="sxs-lookup"><span data-stu-id="f35cc-181">(*) On some device, IPsec integrity must be "null" if GCM-AES is used as IPsec encryption algorithm.</span></span>

### <a name="device-notes"></a><span data-ttu-id="f35cc-182">Note sul dispositivo</span><span class="sxs-lookup"><span data-stu-id="f35cc-182">Device notes</span></span>

>[!NOTE]
>
> 1. <span data-ttu-id="f35cc-183">Il supporto per IKEv2 richiede ASA 8.4 e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="f35cc-183">IKEv2 support requires ASA version 8.4 and above.</span></span>
> 2. <span data-ttu-id="f35cc-184">Il supporto del gruppo PFS e DH superiore, superiore al gruppo 5, richiede la versione ASA 9.x.</span><span class="sxs-lookup"><span data-stu-id="f35cc-184">Higher DH and PFS group support (beyond Group 5) requires ASA version 9.x.</span></span>
> 3. <span data-ttu-id="f35cc-185">La crittografia IPsec con l'integrità IPsec e AES-GCM con il supporto SHA-256, SHA-384, SHA-512 richiede la versione ASA 9.x sull'hardware ASA più recente; ASA 5505, 5510, 5520, 5540, 5550, 5580 **non** sono supportati.</span><span class="sxs-lookup"><span data-stu-id="f35cc-185">IPsec encryption with AES-GCM and IPsec integrity with SHA-256, SHA-384, SHA-512 support requires ASA version 9.x on newer ASA hardware; ASA 5505, 5510, 5520, 5540, 5550, 5580 are **not** supported.</span></span> <span data-ttu-id="f35cc-186">(Verificare hello fornitore specifiche tooconfirm).</span><span class="sxs-lookup"><span data-stu-id="f35cc-186">(Please check hello vendor specifications tooconfirm.)</span></span>
>


### <a name="sample-device-configurations"></a><span data-ttu-id="f35cc-187">Esempi di configurazioni del dispositivo</span><span class="sxs-lookup"><span data-stu-id="f35cc-187">Sample device configurations</span></span>
<span data-ttu-id="f35cc-188">script Hello riportato di seguito fornisce un esempio di configurazione in base alla topologia hello e parametri sopra elencati.</span><span class="sxs-lookup"><span data-stu-id="f35cc-188">hello script below provides a sample configuration based on hello topology and parameters listed above.</span></span> <span data-ttu-id="f35cc-189">configurazione di tunnel VPN S2S Hello è costituita da hello seguenti parti:</span><span class="sxs-lookup"><span data-stu-id="f35cc-189">hello S2S VPN tunnel configuration consists of hello following parts:</span></span>

1. <span data-ttu-id="f35cc-190">Interfacce e route</span><span class="sxs-lookup"><span data-stu-id="f35cc-190">Interfaces & routes</span></span>
2. <span data-ttu-id="f35cc-191">Elenchi di accesso</span><span class="sxs-lookup"><span data-stu-id="f35cc-191">Access lists</span></span>
3. <span data-ttu-id="f35cc-192">Criterio IKE e parametri (fase 1 o in modalità principale)</span><span class="sxs-lookup"><span data-stu-id="f35cc-192">IKE policy and parameters (Phase 1 or Main Mode)</span></span>
4. <span data-ttu-id="f35cc-193">Criterio IKE e parametri (fase 2 o in modalità rapida)</span><span class="sxs-lookup"><span data-stu-id="f35cc-193">IPsec policy and parameters (Phase 2 or Quick Mode)</span></span>
5. <span data-ttu-id="f35cc-194">Altri parametri (fissaggio MSS TCP e così via)</span><span class="sxs-lookup"><span data-stu-id="f35cc-194">Other parameters (TCP MSS clamping, etc.)</span></span>

>[!IMPORTANT] 
><span data-ttu-id="f35cc-195">Assicurarsi di aver completato elencata di seguito la configurazione aggiuntiva hello e sostituire i segnaposto hello con i valori effettivi hello:</span><span class="sxs-lookup"><span data-stu-id="f35cc-195">Please make sure you complete hello additional configuration listed below and replace hello placeholders with hello actual values:</span></span>
> 
> - <span data-ttu-id="f35cc-196">Configurazione dell'interfaccia per le interfacce interne ed esterne</span><span class="sxs-lookup"><span data-stu-id="f35cc-196">Interface configuration for both inside and outside interfaces</span></span>
> - <span data-ttu-id="f35cc-197">Route per le reti esterne/pubbliche e interne/private</span><span class="sxs-lookup"><span data-stu-id="f35cc-197">Routes for your inside/private and outside/public networks</span></span>
> - <span data-ttu-id="f35cc-198">Assicurarsi che tutti i nomi e i numeri dei criteri siano univoci nel dispositivo hello</span><span class="sxs-lookup"><span data-stu-id="f35cc-198">Ensure all names and policy numbers are unique on hello device</span></span>
> - <span data-ttu-id="f35cc-199">Verificare che nel dispositivo sono supportati gli algoritmi di crittografia di hello</span><span class="sxs-lookup"><span data-stu-id="f35cc-199">Ensure hello cryptographic algorithms are supported on your device</span></span>
> - <span data-ttu-id="f35cc-200">Sostituire i seguenti segnaposto con valori effettivi hello hello</span><span class="sxs-lookup"><span data-stu-id="f35cc-200">Replace hello following place holders with hello actual values</span></span>
>   - <span data-ttu-id="f35cc-201">Nome dell'interfaccia esterna: "esterno"</span><span class="sxs-lookup"><span data-stu-id="f35cc-201">Outside interface name: "outside"</span></span>
>   - <span data-ttu-id="f35cc-202">Azure_Gateway_Public_IP</span><span class="sxs-lookup"><span data-stu-id="f35cc-202">Azure_Gateway_Public_IP</span></span>
>   - <span data-ttu-id="f35cc-203">OnPrem_Device_Public_IP</span><span class="sxs-lookup"><span data-stu-id="f35cc-203">OnPrem_Device_Public_IP</span></span>
>   - <span data-ttu-id="f35cc-204">IKE Pre_Shared_Key</span><span class="sxs-lookup"><span data-stu-id="f35cc-204">IKE Pre_Shared_Key</span></span>
>   - <span data-ttu-id="f35cc-205">Nomi per i gateway di rete locale e virtuale (VNetName, LNGName)</span><span class="sxs-lookup"><span data-stu-id="f35cc-205">VNet and local network gateway names (VNetName, LNGName)</span></span>
>   - <span data-ttu-id="f35cc-206">Prefissi dell'indirizzo di rete locale e virtuale</span><span class="sxs-lookup"><span data-stu-id="f35cc-206">VNet and on-premises network address prefixes</span></span>
>   - <span data-ttu-id="f35cc-207">Netmask appropriate</span><span class="sxs-lookup"><span data-stu-id="f35cc-207">Proper netmasks</span></span>

#### <a name="sample-configuration"></a><span data-ttu-id="f35cc-208">Configurazione di esempio</span><span class="sxs-lookup"><span data-stu-id="f35cc-208">Sample configuration</span></span>

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

## <a name="simple-debugging-commands"></a><span data-ttu-id="f35cc-209">Semplici comandi di debug</span><span class="sxs-lookup"><span data-stu-id="f35cc-209">Simple debugging commands</span></span>

<span data-ttu-id="f35cc-210">Ecco alcuni comandi ASA a scopo di debug:</span><span class="sxs-lookup"><span data-stu-id="f35cc-210">Here are some ASA commands for debugging purposes:</span></span>

1. <span data-ttu-id="f35cc-211">Mostra hello IPsec e IKE dell'account SA</span><span class="sxs-lookup"><span data-stu-id="f35cc-211">Show hello IPsec and IKE SA's</span></span>
    - <span data-ttu-id="f35cc-212">"show crypto ipsec sa"</span><span class="sxs-lookup"><span data-stu-id="f35cc-212">"show crypto ipsec sa"</span></span>
    - <span data-ttu-id="f35cc-213">"show crypto ikev2 sa"</span><span class="sxs-lookup"><span data-stu-id="f35cc-213">"show crypto ikev2 sa"</span></span>
2. <span data-ttu-id="f35cc-214">Se si immette la modalità di debug, si può ottenere molto poco significativi nella console di hello</span><span class="sxs-lookup"><span data-stu-id="f35cc-214">Entering debug mode - this can get very noisy on hello console</span></span>
    - <span data-ttu-id="f35cc-215">"debug crypto ikev2 platform <level>"</span><span class="sxs-lookup"><span data-stu-id="f35cc-215">"debug crypto ikev2 platform <level>"</span></span>
    - <span data-ttu-id="f35cc-216">"debug crypto ikev2 protocol <level>"</span><span class="sxs-lookup"><span data-stu-id="f35cc-216">"debug crypto ikev2 protocol <level>"</span></span>
3. <span data-ttu-id="f35cc-217">Elenco delle configurazioni attuali</span><span class="sxs-lookup"><span data-stu-id="f35cc-217">List current configurations</span></span>
    - <span data-ttu-id="f35cc-218">"Mostra esecuzione" - Mostra hello configurazioni correnti sul dispositivo hello è possibile utilizzare varie parti specifiche in toolist sottocomandi della configurazione hello hello.</span><span class="sxs-lookup"><span data-stu-id="f35cc-218">"show run" - shows hello current configurations on hello device; you can use hello various sub-commands toolist specific parts of hello configuration.</span></span> <span data-ttu-id="f35cc-219">Ad esempio "show run crypto", "show run access-list", "show run tunnel-group" e così via.</span><span class="sxs-lookup"><span data-stu-id="f35cc-219">E.g., "show run crypto", "show run access-list", "show run tunnel-group", etc.</span></span>


## <a name="next-steps"></a><span data-ttu-id="f35cc-220">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f35cc-220">Next steps</span></span>
<span data-ttu-id="f35cc-221">Vedere [la configurazione di gateway VPN attivo-attivo per Cross-premise e le connessioni di rete virtuale a](vpn-gateway-activeactive-rm-powershell.md) per passaggi tooconfigure attivo-attivo cross-premise e connessioni di rete virtuale a.</span><span class="sxs-lookup"><span data-stu-id="f35cc-221">See [Configuring Active-Active VPN Gateways for Cross-Premises and VNet-to-VNet Connections](vpn-gateway-activeactive-rm-powershell.md) for steps tooconfigure active-active cross-premises and VNet-to-VNet connections.</span></span>

