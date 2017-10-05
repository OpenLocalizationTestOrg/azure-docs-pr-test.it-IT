---
title: 'Configurazione di esempio: connessione del dispositivo Cisco ASA ai gateway VPN di Azure | Microsoft Docs'
description: Questo articolo contiene un esempio di configurazione per la connessione di un dispositivo Cisco ASA ai gateway VPN di Azure.
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
ms.openlocfilehash: 10466b8928e2cd687f7961a2956b6d60823b82be
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="sample-configuration-cisco-asa-device-ikev2no-bgp"></a><span data-ttu-id="a69e6-103">Configurazione di esempio: dispositivo Cisco ASA (IKEv2/senza BGP)</span><span class="sxs-lookup"><span data-stu-id="a69e6-103">Sample configuration: Cisco ASA device (IKEv2/no BGP)</span></span>
<span data-ttu-id="a69e6-104">Questo articolo contiene esempi di configurazione per la connessione di dispositivi Cisco ASA ai gateway VPN di Azure.</span><span class="sxs-lookup"><span data-stu-id="a69e6-104">This article provides sample configurations for Cisco ASA devices connecting to Azure VPN gateways.</span></span>

## <a name="device-at-a-glance"></a><span data-ttu-id="a69e6-105">Informazioni sul dispositivo</span><span class="sxs-lookup"><span data-stu-id="a69e6-105">Device at a glance</span></span>

|                        |                                   |
| ---                    | ---                               |
| <span data-ttu-id="a69e6-106">Fornitore del dispositivo</span><span class="sxs-lookup"><span data-stu-id="a69e6-106">Device vendor</span></span>          | <span data-ttu-id="a69e6-107">Cisco</span><span class="sxs-lookup"><span data-stu-id="a69e6-107">Cisco</span></span>                             |
| <span data-ttu-id="a69e6-108">Modello del dispositivo</span><span class="sxs-lookup"><span data-stu-id="a69e6-108">Device model</span></span>           | <span data-ttu-id="a69e6-109">ASA (Adaptive Security Appliance)</span><span class="sxs-lookup"><span data-stu-id="a69e6-109">ASA (Adaptive Security Appliance)</span></span> |
| <span data-ttu-id="a69e6-110">Versione finale</span><span class="sxs-lookup"><span data-stu-id="a69e6-110">Target version</span></span>         | <span data-ttu-id="a69e6-111">8.4+</span><span class="sxs-lookup"><span data-stu-id="a69e6-111">8.4+</span></span>                              |
| <span data-ttu-id="a69e6-112">Modello testato</span><span class="sxs-lookup"><span data-stu-id="a69e6-112">Tested model</span></span>           | <span data-ttu-id="a69e6-113">ASA 5505</span><span class="sxs-lookup"><span data-stu-id="a69e6-113">ASA 5505</span></span>                          |
| <span data-ttu-id="a69e6-114">Versione testata</span><span class="sxs-lookup"><span data-stu-id="a69e6-114">Tested version</span></span>         | <span data-ttu-id="a69e6-115">9.2</span><span class="sxs-lookup"><span data-stu-id="a69e6-115">9.2</span></span>                               |
| <span data-ttu-id="a69e6-116">Versione IKE</span><span class="sxs-lookup"><span data-stu-id="a69e6-116">IKE version</span></span>            | <span data-ttu-id="a69e6-117">**IKEv2**</span><span class="sxs-lookup"><span data-stu-id="a69e6-117">**IKEv2**</span></span>                         |
| <span data-ttu-id="a69e6-118">BGP</span><span class="sxs-lookup"><span data-stu-id="a69e6-118">BGP</span></span>                    | <span data-ttu-id="a69e6-119">**No**</span><span class="sxs-lookup"><span data-stu-id="a69e6-119">**No**</span></span>                            |
| <span data-ttu-id="a69e6-120">Tipo di gateway VPN di Azure</span><span class="sxs-lookup"><span data-stu-id="a69e6-120">Azure VPN gateway type</span></span> | <span data-ttu-id="a69e6-121">Gateway VPN **basato su route**</span><span class="sxs-lookup"><span data-stu-id="a69e6-121">**Route-based** VPN gateway</span></span>       |
|                        |                                   |

> [!NOTE]
> 1. <span data-ttu-id="a69e6-122">La configurazione indicata di seguito connette un dispositivo Cisco ASA a un gateway VPN **basato su route** di Azure usando i criteri IPsec/IKE personalizzati con l'opzione "UserPolicyBasedTrafficSelectors", come descritto in [questo articolo](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="a69e6-122">The configuration below connects a Cisco ASA device to an Azure **route-based** VPN gateway using custom IPsec/IKE policy with "UserPolicyBasedTrafficSelectors" option, as described in [this article](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span></span>
> 2. <span data-ttu-id="a69e6-123">Per usare **IKEv2** con configurazioni basate sull'elenco di accesso, non su VTI sono necessari i dispositivi ASA.</span><span class="sxs-lookup"><span data-stu-id="a69e6-123">It requires ASA devices to use **IKEv2** with access-list-based configurations, not VTI-based.</span></span>
> 3. <span data-ttu-id="a69e6-124">Consultare le specifiche del fornitore del dispositivo VPN per verificare che i criteri siano supportati nei dispositivi VPN locali.</span><span class="sxs-lookup"><span data-stu-id="a69e6-124">Please consult with your VPN device vendor specifications to ensure the policy is supported on your on-premises VPN devices.</span></span>

## <a name="vpn-device-requirements"></a><span data-ttu-id="a69e6-125">Requisiti del dispositivo VPN</span><span class="sxs-lookup"><span data-stu-id="a69e6-125">VPN device requirements</span></span>
<span data-ttu-id="a69e6-126">Per stabilire i tunnel VPN S2S i gateway VPN di Azure usano gruppi di protocollo IPsec/IKE standard.</span><span class="sxs-lookup"><span data-stu-id="a69e6-126">Azure VPN gateways use standard IPsec/IKE protocol suites to establish S2S VPN tunnels.</span></span> <span data-ttu-id="a69e6-127">Fare riferimento a [Informazioni sui dispositivi VPN](vpn-gateway-about-vpn-devices.md) per i parametri di protocollo IPsec/IKE dettagliati e gli algoritmi di crittografia predefinita per i gateway VPN di Azure.</span><span class="sxs-lookup"><span data-stu-id="a69e6-127">Refer to [About VPN devices](vpn-gateway-about-vpn-devices.md) for the detailed IPsec/IKE protocol parameters and default cryptographic algorithms for Azure VPN gateways.</span></span> <span data-ttu-id="a69e6-128">È possibile specificare facoltativamente l'esatta combinazione di algoritmi di crittografia e la complessità della chiave per una connessione specifica come descritto in [Informazioni sui requisiti di crittografia](vpn-gateway-about-compliance-crypto.md).</span><span class="sxs-lookup"><span data-stu-id="a69e6-128">You can optionally specify the exact combination of cryptographic algorithms and key strengths for a specific connection as described in [About cryptographic requirements](vpn-gateway-about-compliance-crypto.md).</span></span> <span data-ttu-id="a69e6-129">Se si seleziona una combinazione specifica di complessità delle chiavi e algoritmi di crittografia, assicurarsi di usare le specifiche corrispondenti nei dispositivi VPN.</span><span class="sxs-lookup"><span data-stu-id="a69e6-129">If you select a specific combination of cryptographic algorithms and key strengths, please make sure you use the corresponding specifications on your VPN devices.</span></span>

## <a name="single-vpn-tunnel"></a><span data-ttu-id="a69e6-130">Tunnel per VPN unico</span><span class="sxs-lookup"><span data-stu-id="a69e6-130">Single VPN tunnel</span></span>
<span data-ttu-id="a69e6-131">Questa topologia consiste in un unico tunnel per VPN S2S tra un gateway VPN di Azure e il dispositivo VPN locale.</span><span class="sxs-lookup"><span data-stu-id="a69e6-131">This topology consists of a single S2S VPN tunnel between an Azure VPN gateway and your on-premises VPN device.</span></span> <span data-ttu-id="a69e6-132">È possibile configurare BGP nel tunnel VPN.</span><span class="sxs-lookup"><span data-stu-id="a69e6-132">You can optionally configure BGP across the VPN tunnel.</span></span>

![Tunnel unico](./media/vpn-gateway-3rdparty-device-config-cisco-asa/singletunnel.png)

<span data-ttu-id="a69e6-134">Fare riferimento a [Single tunnel setup](vpn-gateway-3rdparty-device-config-overview.md#singletunnel) (Configurazione del tunnel singolo) per avere istruzioni dettagliate e creare le configurazioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="a69e6-134">Refer to [Single tunnel setup](vpn-gateway-3rdparty-device-config-overview.md#singletunnel) for detailed, step-by-step instructions to build the Azure configurations.</span></span>

### <a name="network-and-vpn-gateway-information"></a><span data-ttu-id="a69e6-135">Informazioni sul gateway di rete e VPN</span><span class="sxs-lookup"><span data-stu-id="a69e6-135">Network and VPN gateway information</span></span>
<span data-ttu-id="a69e6-136">Questa sezione elenca i parametri per questo esempio.</span><span class="sxs-lookup"><span data-stu-id="a69e6-136">This section list the parameters for the this sample.</span></span>

| <span data-ttu-id="a69e6-137">**Parametro**</span><span class="sxs-lookup"><span data-stu-id="a69e6-137">**Parameter**</span></span>                | <span data-ttu-id="a69e6-138">**Valore**</span><span class="sxs-lookup"><span data-stu-id="a69e6-138">**Value**</span></span>                    |
| ---                          | ---                          |
| <span data-ttu-id="a69e6-139">Prefissi di indirizzi di rete virtuale</span><span class="sxs-lookup"><span data-stu-id="a69e6-139">VNet address prefixes</span></span>        | <span data-ttu-id="a69e6-140">10.11.0.0/16</span><span class="sxs-lookup"><span data-stu-id="a69e6-140">10.11.0.0/16</span></span><br><span data-ttu-id="a69e6-141">10.12.0.0/16</span><span class="sxs-lookup"><span data-stu-id="a69e6-141">10.12.0.0/16</span></span> |
| <span data-ttu-id="a69e6-142">Indirizzo IP del gateway VPN di Azure</span><span class="sxs-lookup"><span data-stu-id="a69e6-142">Azure VPN gateway IP</span></span>         | <span data-ttu-id="a69e6-143">Azure_Gateway_Public_IP</span><span class="sxs-lookup"><span data-stu-id="a69e6-143">Azure_Gateway_Public_IP</span></span>      |
| <span data-ttu-id="a69e6-144">Prefissi di indirizzi locali</span><span class="sxs-lookup"><span data-stu-id="a69e6-144">On-premises address prefixes</span></span> | <span data-ttu-id="a69e6-145">10.51.0.0/16</span><span class="sxs-lookup"><span data-stu-id="a69e6-145">10.51.0.0/16</span></span><br><span data-ttu-id="a69e6-146">10.52.0.0/16</span><span class="sxs-lookup"><span data-stu-id="a69e6-146">10.52.0.0/16</span></span> |
| <span data-ttu-id="a69e6-147">Indirizzo IP del dispositivo VPN locale</span><span class="sxs-lookup"><span data-stu-id="a69e6-147">On-premises VPN device IP</span></span>    | <span data-ttu-id="a69e6-148">OnPrem_Device_Public_IP</span><span class="sxs-lookup"><span data-stu-id="a69e6-148">OnPrem_Device_Public_IP</span></span>     |
| <span data-ttu-id="a69e6-149">*BGP ASN della rete virtuale</span><span class="sxs-lookup"><span data-stu-id="a69e6-149">*VNet BGP ASN</span></span>                | <span data-ttu-id="a69e6-150">65010</span><span class="sxs-lookup"><span data-stu-id="a69e6-150">65010</span></span>                        |
| <span data-ttu-id="a69e6-151">*Indirizzo IP del peer BGP di Azure</span><span class="sxs-lookup"><span data-stu-id="a69e6-151">*Azure BGP peer IP</span></span>           | <span data-ttu-id="a69e6-152">10.12.255.30</span><span class="sxs-lookup"><span data-stu-id="a69e6-152">10.12.255.30</span></span>                 |
| <span data-ttu-id="a69e6-153">*ASN BGP locale</span><span class="sxs-lookup"><span data-stu-id="a69e6-153">*On-premises BGP ASN</span></span>         | <span data-ttu-id="a69e6-154">65050</span><span class="sxs-lookup"><span data-stu-id="a69e6-154">65050</span></span>                        |
| <span data-ttu-id="a69e6-155">*Indirizzo IP del peer BGP locale</span><span class="sxs-lookup"><span data-stu-id="a69e6-155">*On-premises BGP peer IP</span></span>     | <span data-ttu-id="a69e6-156">10.52.255.254</span><span class="sxs-lookup"><span data-stu-id="a69e6-156">10.52.255.254</span></span>                |
|                              |                              |

* <span data-ttu-id="a69e6-157">(*) Parametri facoltativi solo per BGP.</span><span class="sxs-lookup"><span data-stu-id="a69e6-157">(*) Optional parameters for BGP only.</span></span>

### <a name="ipsecike-policy--parameters"></a><span data-ttu-id="a69e6-158">Criteri e parametri IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="a69e6-158">IPsec/IKE policy & parameters</span></span>

<span data-ttu-id="a69e6-159">Nella tabella seguente sono elencati gli algoritmi e i parametri IPsec/IKE usati nell'esempio.</span><span class="sxs-lookup"><span data-stu-id="a69e6-159">The table below lists the IPsec/IKE algorithms and parameters used in the sample.</span></span> <span data-ttu-id="a69e6-160">Consultare le specifiche del dispositivo VPN per assicurarsi che tutti gli algoritmi elencati sopra siano supportati dai modelli del dispositivo VPN e dalle versioni del firmware.</span><span class="sxs-lookup"><span data-stu-id="a69e6-160">Please consult your VPN device specifications to make sure all algorithms listed above are supported by your VPN device models and firmware versions.</span></span>

| <span data-ttu-id="a69e6-161">**IPsec/IKEv2**</span><span class="sxs-lookup"><span data-stu-id="a69e6-161">**IPsec/IKEv2**</span></span>  | <span data-ttu-id="a69e6-162">**Valore**</span><span class="sxs-lookup"><span data-stu-id="a69e6-162">**Value**</span></span>                            |
| ---              | ---                                  |
| <span data-ttu-id="a69e6-163">Crittografia IKEv2</span><span class="sxs-lookup"><span data-stu-id="a69e6-163">IKEv2 Encryption</span></span> | <span data-ttu-id="a69e6-164">AES256</span><span class="sxs-lookup"><span data-stu-id="a69e6-164">AES256</span></span>                               |
| <span data-ttu-id="a69e6-165">Integrità IKEv2</span><span class="sxs-lookup"><span data-stu-id="a69e6-165">IKEv2 Integrity</span></span>  | <span data-ttu-id="a69e6-166">SHA384</span><span class="sxs-lookup"><span data-stu-id="a69e6-166">SHA384</span></span>                               |
| <span data-ttu-id="a69e6-167">Gruppo DH</span><span class="sxs-lookup"><span data-stu-id="a69e6-167">DH Group</span></span>         | <span data-ttu-id="a69e6-168">DHGroup24</span><span class="sxs-lookup"><span data-stu-id="a69e6-168">DHGroup24</span></span>                            |
| <span data-ttu-id="a69e6-169">Crittografia IPsec</span><span class="sxs-lookup"><span data-stu-id="a69e6-169">IPsec Encryption</span></span> | <span data-ttu-id="a69e6-170">AES256</span><span class="sxs-lookup"><span data-stu-id="a69e6-170">AES256</span></span>                               |
| <span data-ttu-id="a69e6-171">Integrità IPsec</span><span class="sxs-lookup"><span data-stu-id="a69e6-171">IPsec Integrity</span></span>  | <span data-ttu-id="a69e6-172">SHA1</span><span class="sxs-lookup"><span data-stu-id="a69e6-172">SHA1</span></span>                                 |
| <span data-ttu-id="a69e6-173">Gruppo PFS</span><span class="sxs-lookup"><span data-stu-id="a69e6-173">PFS Group</span></span>        | <span data-ttu-id="a69e6-174">PFS24</span><span class="sxs-lookup"><span data-stu-id="a69e6-174">PFS24</span></span>                                |
| <span data-ttu-id="a69e6-175">Durata associazione di sicurezza QM</span><span class="sxs-lookup"><span data-stu-id="a69e6-175">QM SA Lifetime</span></span>   | <span data-ttu-id="a69e6-176">7200 secondi</span><span class="sxs-lookup"><span data-stu-id="a69e6-176">7200 seconds</span></span>                         |
| <span data-ttu-id="a69e6-177">Selettore di traffico</span><span class="sxs-lookup"><span data-stu-id="a69e6-177">Traffic Selector</span></span> | <span data-ttu-id="a69e6-178">UsePolicyBasedTrafficSelectors $True</span><span class="sxs-lookup"><span data-stu-id="a69e6-178">UsePolicyBasedTrafficSelectors $True</span></span> |
| <span data-ttu-id="a69e6-179">Chiave precondivisa</span><span class="sxs-lookup"><span data-stu-id="a69e6-179">Pre-Shared Key</span></span>   | <span data-ttu-id="a69e6-180">PreSharedKey</span><span class="sxs-lookup"><span data-stu-id="a69e6-180">PreSharedKey</span></span>                         |
|                  |                                      |

- <span data-ttu-id="a69e6-181">(*) Su alcuni dispositivi, l'integrità IPsec deve essere "null" se GCM-AES viene usato come algoritmo di crittografia IPsec.</span><span class="sxs-lookup"><span data-stu-id="a69e6-181">(*) On some device, IPsec integrity must be "null" if GCM-AES is used as IPsec encryption algorithm.</span></span>

### <a name="device-notes"></a><span data-ttu-id="a69e6-182">Note sul dispositivo</span><span class="sxs-lookup"><span data-stu-id="a69e6-182">Device notes</span></span>

>[!NOTE]
>
> 1. <span data-ttu-id="a69e6-183">Il supporto per IKEv2 richiede ASA 8.4 e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="a69e6-183">IKEv2 support requires ASA version 8.4 and above.</span></span>
> 2. <span data-ttu-id="a69e6-184">Il supporto del gruppo PFS e DH superiore, superiore al gruppo 5, richiede la versione ASA 9.x.</span><span class="sxs-lookup"><span data-stu-id="a69e6-184">Higher DH and PFS group support (beyond Group 5) requires ASA version 9.x.</span></span>
> 3. <span data-ttu-id="a69e6-185">La crittografia IPsec con l'integrità IPsec e AES-GCM con il supporto SHA-256, SHA-384, SHA-512 richiede la versione ASA 9.x sull'hardware ASA più recente; ASA 5505, 5510, 5520, 5540, 5550, 5580 **non** sono supportati.</span><span class="sxs-lookup"><span data-stu-id="a69e6-185">IPsec encryption with AES-GCM and IPsec integrity with SHA-256, SHA-384, SHA-512 support requires ASA version 9.x on newer ASA hardware; ASA 5505, 5510, 5520, 5540, 5550, 5580 are **not** supported.</span></span> <span data-ttu-id="a69e6-186">Verificare le specifiche del fornitore per confermare.</span><span class="sxs-lookup"><span data-stu-id="a69e6-186">(Please check the vendor specifications to confirm.)</span></span>
>


### <a name="sample-device-configurations"></a><span data-ttu-id="a69e6-187">Esempi di configurazioni del dispositivo</span><span class="sxs-lookup"><span data-stu-id="a69e6-187">Sample device configurations</span></span>
<span data-ttu-id="a69e6-188">Lo script seguente è un esempio di configurazione basato sulla topologia e i parametri elencati precedentemente.</span><span class="sxs-lookup"><span data-stu-id="a69e6-188">The script below provides a sample configuration based on the topology and parameters listed above.</span></span> <span data-ttu-id="a69e6-189">La configurazione del tunnel VPN S2S è costituita dai seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="a69e6-189">The S2S VPN tunnel configuration consists of the following parts:</span></span>

1. <span data-ttu-id="a69e6-190">Interfacce e route</span><span class="sxs-lookup"><span data-stu-id="a69e6-190">Interfaces & routes</span></span>
2. <span data-ttu-id="a69e6-191">Elenchi di accesso</span><span class="sxs-lookup"><span data-stu-id="a69e6-191">Access lists</span></span>
3. <span data-ttu-id="a69e6-192">Criterio IKE e parametri (fase 1 o in modalità principale)</span><span class="sxs-lookup"><span data-stu-id="a69e6-192">IKE policy and parameters (Phase 1 or Main Mode)</span></span>
4. <span data-ttu-id="a69e6-193">Criterio IKE e parametri (fase 2 o in modalità rapida)</span><span class="sxs-lookup"><span data-stu-id="a69e6-193">IPsec policy and parameters (Phase 2 or Quick Mode)</span></span>
5. <span data-ttu-id="a69e6-194">Altri parametri (fissaggio MSS TCP e così via)</span><span class="sxs-lookup"><span data-stu-id="a69e6-194">Other parameters (TCP MSS clamping, etc.)</span></span>

>[!IMPORTANT] 
><span data-ttu-id="a69e6-195">Assicurarsi di aver completato la configurazione aggiuntiva elencata di seguito e sostituire i segnaposto con i valori effettivi:</span><span class="sxs-lookup"><span data-stu-id="a69e6-195">Please make sure you complete the additional configuration listed below and replace the placeholders with the actual values:</span></span>
> 
> - <span data-ttu-id="a69e6-196">Configurazione dell'interfaccia per le interfacce interne ed esterne</span><span class="sxs-lookup"><span data-stu-id="a69e6-196">Interface configuration for both inside and outside interfaces</span></span>
> - <span data-ttu-id="a69e6-197">Route per le reti esterne/pubbliche e interne/private</span><span class="sxs-lookup"><span data-stu-id="a69e6-197">Routes for your inside/private and outside/public networks</span></span>
> - <span data-ttu-id="a69e6-198">Assicurarsi che tutti i nomi e i numeri dei criteri siano univoci nel dispositivo</span><span class="sxs-lookup"><span data-stu-id="a69e6-198">Ensure all names and policy numbers are unique on the device</span></span>
> - <span data-ttu-id="a69e6-199">Verificare che gli algoritmi di crittografia siano supportati nel dispositivo</span><span class="sxs-lookup"><span data-stu-id="a69e6-199">Ensure the cryptographic algorithms are supported on your device</span></span>
> - <span data-ttu-id="a69e6-200">Sostituire i segnaposto seguenti con i valori effettivi</span><span class="sxs-lookup"><span data-stu-id="a69e6-200">Replace the following place holders with the actual values</span></span>
>   - <span data-ttu-id="a69e6-201">Nome dell'interfaccia esterna: "esterno"</span><span class="sxs-lookup"><span data-stu-id="a69e6-201">Outside interface name: "outside"</span></span>
>   - <span data-ttu-id="a69e6-202">Azure_Gateway_Public_IP</span><span class="sxs-lookup"><span data-stu-id="a69e6-202">Azure_Gateway_Public_IP</span></span>
>   - <span data-ttu-id="a69e6-203">OnPrem_Device_Public_IP</span><span class="sxs-lookup"><span data-stu-id="a69e6-203">OnPrem_Device_Public_IP</span></span>
>   - <span data-ttu-id="a69e6-204">IKE Pre_Shared_Key</span><span class="sxs-lookup"><span data-stu-id="a69e6-204">IKE Pre_Shared_Key</span></span>
>   - <span data-ttu-id="a69e6-205">Nomi per i gateway di rete locale e virtuale (VNetName, LNGName)</span><span class="sxs-lookup"><span data-stu-id="a69e6-205">VNet and local network gateway names (VNetName, LNGName)</span></span>
>   - <span data-ttu-id="a69e6-206">Prefissi dell'indirizzo di rete locale e virtuale</span><span class="sxs-lookup"><span data-stu-id="a69e6-206">VNet and on-premises network address prefixes</span></span>
>   - <span data-ttu-id="a69e6-207">Netmask appropriate</span><span class="sxs-lookup"><span data-stu-id="a69e6-207">Proper netmasks</span></span>

#### <a name="sample-configuration"></a><span data-ttu-id="a69e6-208">Configurazione di esempio</span><span class="sxs-lookup"><span data-stu-id="a69e6-208">Sample configuration</span></span>

```
! Sample ASA configuration for connecting to Azure VPN gateway
!
! Tested hardware: ASA 5505
! Tested version:  ASA version 9.2(4)
!
! Replace the following place holders with your actual values:
!   - Interface names - default are "outside" and "inside"
!   - <Azure_Gateway_Public_IP>
!   - <OnPrem_Device_Public_IP>
!   - <Pre_Shared_Key>
!   - <VNetName>*
!   - <LNGName>* ==> LocalNetworkGateway - the Azure resource that represents the
!     on-premises network, specifies network prefixes, device public IP, BGP info, etc.
!   - <PrivateIPAddress> ==> Replace it with a private IP address if applicable
!   - <Netmask> ==> Replace it with appropriate netmasks
!   - <Nexthop> ==> Replace it with the actual nexthop IP address
!
! (*) Must be unique names in the device configuration
!
! ==> Interface & route configurations
!
!     > <OnPrem_Device_Public_IP> address on the outside interface or vlan
!     > <PrivateIPAddress> on the inside interface or vlan; e.g., 10.51.0.1/24
!     > Route to connect to <Azure_Gateway_Public_IP> address
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
!       (1) Allow S2S VPN tunnels between the ASA and the Azure gateway public IP address
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
!     > Object group that corresponding to the <LNGName> prefixes.
!       E.g., 10.51.0.0/16 and 10.52.0.0/16. Note that LNG = "local network gateway".
!       In Azure network resource, a local network gateway defines the on-premises
!       network properties (address prefixes, VPN device IP, BGP ASN, etc.)
!
object-group network <LNGName>
 description On-Premises network <LNGName> prefixes
 network-object 10.51.0.0 255.255.0.0
 network-object 10.52.0.0 255.255.0.0
exit
!
!     > Specify the access-list between the Azure VNet and your on-premises network.
!       This access list defines the IPsec SA traffic selectors.
!
access-list Azure-<VNetName>-acl extended permit ip object-group <LNGName> object-group Azure-<VNetName>
!
!     > No NAT required between the on-premises network and Azure VNet
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
!       - Make sure the policy number is not used
!       - integrity and prf must be the same
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
!       - This sample uses "Azure-<VNetName>-map" as the crypto map name
!       - ASA supports only one crypto map per interface, if you already have
!         an existing crypto map assigned to your outside interface, you must use
!         the same crypto map name, but with a different sequence number for
!         this policy
!       - "match address" policy uses the access-list "Azure-<VNetName>-acl" defined 
!         previously
!       - "ipsec-proposal" uses the proposal "AES-256" defined previously 
!       - PFS groups 14 and beyond requires ASA version 9.x.
!
crypto map Azure-<VNetName>-map 1 match address Azure-<VNetName>-acl
crypto map Azure-<VNetName>-map 1 set pfs group24
crypto map Azure-<VNetName>-map 1 set peer <Azure_Gateway_Public_IP>
crypto map Azure-<VNetName>-map 1 set ikev2 ipsec-proposal AES-256
crypto map Azure-<VNetName>-map 1 set security-association lifetime seconds 7200
crypto map Azure-<VNetName>-map interface outside
!
! ==> Set TCP MSS to 1350
!
sysopt connection tcpmss 1350
!
```

## <a name="simple-debugging-commands"></a><span data-ttu-id="a69e6-209">Semplici comandi di debug</span><span class="sxs-lookup"><span data-stu-id="a69e6-209">Simple debugging commands</span></span>

<span data-ttu-id="a69e6-210">Ecco alcuni comandi ASA a scopo di debug:</span><span class="sxs-lookup"><span data-stu-id="a69e6-210">Here are some ASA commands for debugging purposes:</span></span>

1. <span data-ttu-id="a69e6-211">Mostrare l'associazione di sicurezza IPsec e IKE</span><span class="sxs-lookup"><span data-stu-id="a69e6-211">Show the IPsec and IKE SA's</span></span>
    - <span data-ttu-id="a69e6-212">"show crypto ipsec sa"</span><span class="sxs-lookup"><span data-stu-id="a69e6-212">"show crypto ipsec sa"</span></span>
    - <span data-ttu-id="a69e6-213">"show crypto ikev2 sa"</span><span class="sxs-lookup"><span data-stu-id="a69e6-213">"show crypto ikev2 sa"</span></span>
2. <span data-ttu-id="a69e6-214">Attivazione della modalità di debug. La console può diventare molto rumorosa</span><span class="sxs-lookup"><span data-stu-id="a69e6-214">Entering debug mode - this can get very noisy on the console</span></span>
    - <span data-ttu-id="a69e6-215">"debug crypto ikev2 platform <level>"</span><span class="sxs-lookup"><span data-stu-id="a69e6-215">"debug crypto ikev2 platform <level>"</span></span>
    - <span data-ttu-id="a69e6-216">"debug crypto ikev2 protocol <level>"</span><span class="sxs-lookup"><span data-stu-id="a69e6-216">"debug crypto ikev2 protocol <level>"</span></span>
3. <span data-ttu-id="a69e6-217">Elenco delle configurazioni attuali</span><span class="sxs-lookup"><span data-stu-id="a69e6-217">List current configurations</span></span>
    - <span data-ttu-id="a69e6-218">"show run": mostra le configurazioni correnti nel dispositivo; è possibile usare diversi comandi secondari per elencare parti specifiche della configurazione.</span><span class="sxs-lookup"><span data-stu-id="a69e6-218">"show run" - shows the current configurations on the device; you can use the various sub-commands to list specific parts of the configuration.</span></span> <span data-ttu-id="a69e6-219">Ad esempio "show run crypto", "show run access-list", "show run tunnel-group" e così via.</span><span class="sxs-lookup"><span data-stu-id="a69e6-219">E.g., "show run crypto", "show run access-list", "show run tunnel-group", etc.</span></span>


## <a name="next-steps"></a><span data-ttu-id="a69e6-220">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a69e6-220">Next steps</span></span>
<span data-ttu-id="a69e6-221">Per informazioni sulla procedura per configurare connessioni cross-premise e da rete virtuale a rete virtuale di tipo attivo/attivo, vedere [Configurazione di gateway VPN di tipo attivo/attivo per connessioni cross-premise e da rete virtuale a rete virtuale](vpn-gateway-activeactive-rm-powershell.md) .</span><span class="sxs-lookup"><span data-stu-id="a69e6-221">See [Configuring Active-Active VPN Gateways for Cross-Premises and VNet-to-VNet Connections](vpn-gateway-activeactive-rm-powershell.md) for steps to configure active-active cross-premises and VNet-to-VNet connections.</span></span>

