---
title: 'Configurare i criteri IPsec/IKE per le connessioni VPN da sito a sito o da rete virtuale a rete virtuale: Azure Resource Manager: PowerShell | Microsoft Docs'
description: In questo articolo viene illustrata la configurazione di criteri IPsec/IKE per connessioni da sito a sito o da rete virtuale a rete virtuale con i gateway VPN di Azure tramite Azure Resource Manager e PowerShell.
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
ms.date: 05/12/2017
ms.author: yushwang
ms.openlocfilehash: 798014b6e8d4495db99ef2e2d2ea487ae7d02fd0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="configure-ipsecike-policy-for-s2s-vpn-or-vnet-to-vnet-connections"></a><span data-ttu-id="3dddc-103">Configurare criteri IPsec/IKE per connessioni VPN da sito a sito o da rete virtuale a rete virtuale</span><span class="sxs-lookup"><span data-stu-id="3dddc-103">Configure IPsec/IKE policy for S2S VPN or VNet-to-VNet connections</span></span>

<span data-ttu-id="3dddc-104">Questo articolo illustra la procedura di configurazione dei criteri IPsec/IKE per connessioni VPN da sito a sito o da rete virtuale a rete virtuale tramite il modello di distribuzione Resource Manager e PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3dddc-104">This article walks you through the steps to configure IPsec/IKE policy for Site-to-Site VPN or VNet-to-VNet connections using the Resource Manager deployment model and PowerShell.</span></span>

## <span data-ttu-id="3dddc-105"><a name="about"></a>Informazioni sui parametri dei criteri IPsec e IKE per gateway VPN di Azure</span><span class="sxs-lookup"><span data-stu-id="3dddc-105"><a name="about"></a>About IPsec and IKE policy parameters for Azure VPN gateways</span></span>
<span data-ttu-id="3dddc-106">Lo standard di protocollo IPsec e IKE supporta un'ampia gamma di algoritmi di crittografia in varie combinazioni.</span><span class="sxs-lookup"><span data-stu-id="3dddc-106">IPsec and IKE protocol standard supports a wide range of cryptographic algorithms in various combinations.</span></span> <span data-ttu-id="3dddc-107">Vedere l'articolo [About cryptographic requirements and Azure VPN gateways](vpn-gateway-about-compliance-crypto.md) (Informazioni sui requisiti di crittografia e i gateway VPN di Azure) per informazioni su come questo può contribuire ad assicurare che la connettività cross-premise e da rete virtuale a rete virtuale soddisfi i requisiti di conformità o sicurezza.</span><span class="sxs-lookup"><span data-stu-id="3dddc-107">Refer to [About cryptographic requirements and Azure VPN gateways](vpn-gateway-about-compliance-crypto.md) to see how this can help ensuring cross-premises and VNet-to-VNet connectivity satisfy your compliance or security requirements.</span></span>

<span data-ttu-id="3dddc-108">Questo articolo fornisce istruzioni per creare e configurare un criterio IPsec/IKE e applicarlo a una connessione nuova o esistente:</span><span class="sxs-lookup"><span data-stu-id="3dddc-108">This article provides instructions to create and configure an IPsec/IKE policy and apply to a new or existing connection:</span></span>

* [<span data-ttu-id="3dddc-109">Parte 1: Flusso di lavoro per creare e impostare criteri IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="3dddc-109">Part 1 - Workflow to create and set IPsec/IKE policy</span></span>](#workflow)
* [<span data-ttu-id="3dddc-110">Parte 2: Algoritmi di crittografia supportati e vantaggi chiave</span><span class="sxs-lookup"><span data-stu-id="3dddc-110">Part 2 - Supported cryptographic algorithms and key strengths</span></span>](#params)
* [<span data-ttu-id="3dddc-111">Parte 3: Creare una nuova connessione VPN da sito a sito con criteri IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="3dddc-111">Part 3 - Create a new S2S VPN connection with IPsec/IKE policy</span></span>](#crossprem)
* [<span data-ttu-id="3dddc-112">Parte 4: Creare una nuova connessione da rete virtuale a rete virtuale con criteri IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="3dddc-112">Part 4 - Create a new VNet-to-VNet connection with IPsec/IKE policy</span></span>](#vnet2vnet)
* [<span data-ttu-id="3dddc-113">Parte 5: Gestire (creare, aggiungere, rimuovere) criteri IPsec/IKE per una connessione</span><span class="sxs-lookup"><span data-stu-id="3dddc-113">Part 5 - Manage (create, add, remove) IPsec/IKE policy for a connection</span></span>](#managepolicy)

> [!IMPORTANT]
> 1. <span data-ttu-id="3dddc-114">Si noti che il criterio IPsec/IKE funziona solo sugli SKU di gateway seguenti:</span><span class="sxs-lookup"><span data-stu-id="3dddc-114">Note that IPsec/IKE policy only works on the following gateway SKUs:</span></span>
>    * <span data-ttu-id="3dddc-115">***VpnGw1, VpnGw2, VpnGw3*** (basato su route)</span><span class="sxs-lookup"><span data-stu-id="3dddc-115">***VpnGw1, VpnGw2, VpnGw3*** (route-based)</span></span>
>    * <span data-ttu-id="3dddc-116">***Standard*** e ***HighPerformance*** (basato su route)</span><span class="sxs-lookup"><span data-stu-id="3dddc-116">***Standard*** and ***HighPerformance*** (route-based)</span></span>
> 2. <span data-ttu-id="3dddc-117">Per una determinata connessione è possibile specificare ***una*** sola combinazione di criteri.</span><span class="sxs-lookup"><span data-stu-id="3dddc-117">You can only specify ***one*** policy combination for a given connection.</span></span>
> 3. <span data-ttu-id="3dddc-118">È necessario specificare tutti gli algoritmi e i parametri sia per IKE (modalità principale) che per IPsec (modalità rapida).</span><span class="sxs-lookup"><span data-stu-id="3dddc-118">You must specify all algorithms and parameters for both IKE (Main Mode) and IPsec (Quick Mode).</span></span> <span data-ttu-id="3dddc-119">Non è consentito specificare criteri parziali.</span><span class="sxs-lookup"><span data-stu-id="3dddc-119">Partial policy specification is not allowed.</span></span>
> 4. <span data-ttu-id="3dddc-120">Consultare le specifiche del fornitore del dispositivo VPN per verificare che i criteri siano supportati dai dispositivi VPN locali.</span><span class="sxs-lookup"><span data-stu-id="3dddc-120">Consult with your VPN device vendor specifications to ensure the policy is supported on your on-premises VPN devices.</span></span> <span data-ttu-id="3dddc-121">Non è possibile stabilire connessioni da sito a sito o da rete virtuale a rete virtuale se i criteri non sono compatibili.</span><span class="sxs-lookup"><span data-stu-id="3dddc-121">S2S or VNet-to-VNet connections cannot establish if the policies are incompatible.</span></span>

## <span data-ttu-id="3dddc-122"><a name ="workflow"></a>Parte 1: Flusso di lavoro per creare e impostare criteri IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="3dddc-122"><a name ="workflow"></a>Part 1 - Workflow to create and set IPsec/IKE policy</span></span>
<span data-ttu-id="3dddc-123">Questa sezione descrive il flusso di lavoro per creare e aggiornare i criteri IPsec/IKE per una connessione VPN da sito a sito o da rete virtuale a rete virtuale:</span><span class="sxs-lookup"><span data-stu-id="3dddc-123">This section outlines the workflow to create and update IPsec/IKE policy on a S2S VPN or VNet-to-VNet connection:</span></span>
1. <span data-ttu-id="3dddc-124">Creare una rete virtuale e un gateway VPN</span><span class="sxs-lookup"><span data-stu-id="3dddc-124">Create a virtual network and a VPN gateway</span></span>
2. <span data-ttu-id="3dddc-125">Creare un gateway di rete locale per una connessione cross-premises o un'altra rete virtuale e gateway per una connessione da rete virtuale a rete virtuale</span><span class="sxs-lookup"><span data-stu-id="3dddc-125">Create a local network gateway for cross premises connection, or another virtual network and gateway for VNet-to-VNet connection</span></span>
3. <span data-ttu-id="3dddc-126">Creare un criterio IPsec/IKE con gli algoritmi e i parametri selezionati</span><span class="sxs-lookup"><span data-stu-id="3dddc-126">Create an IPsec/IKE policy with selected algorithms and parameters</span></span>
4. <span data-ttu-id="3dddc-127">Creare una connessione (IPsec o da rete virtuale a rete virtuale) con il criterio IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="3dddc-127">Create a connection (IPsec or VNet2VNet) with the IPsec/IKE policy</span></span>
5. <span data-ttu-id="3dddc-128">Aggiungere, aggiornare o rimuovere un criterio IPsec/IKE per una connessione esistente</span><span class="sxs-lookup"><span data-stu-id="3dddc-128">Add/update/remove an IPsec/IKE policy for an existing connection</span></span>

<span data-ttu-id="3dddc-129">Le istruzioni di questo articolo consentono di impostare e configurare criteri IPsec/IKE come illustrato nel diagramma:</span><span class="sxs-lookup"><span data-stu-id="3dddc-129">The instructions in this article helps you set up and configure IPsec/IKE policies as shown in the diagram:</span></span>

![ipsec-ike-policy](./media/vpn-gateway-ipsecikepolicy-rm-powershell/ipsecikepolicy.png)

## <span data-ttu-id="3dddc-131"><a name ="params"></a>Parte 2: Algoritmi di crittografia supportati e vantaggi chiave</span><span class="sxs-lookup"><span data-stu-id="3dddc-131"><a name ="params"></a>Part 2 - Supported cryptographic algorithms & key strengths</span></span>

<span data-ttu-id="3dddc-132">La tabella seguente riporta l'elenco degli algoritmi di crittografia e dei tipi di attendibilità della chiave supportati e configurabili dai clienti:</span><span class="sxs-lookup"><span data-stu-id="3dddc-132">The following table lists the supported cryptographic algorithms and key strengths configurable by the customers:</span></span>

| <span data-ttu-id="3dddc-133">**IPsec/IKEv2**</span><span class="sxs-lookup"><span data-stu-id="3dddc-133">**IPsec/IKEv2**</span></span>  | <span data-ttu-id="3dddc-134">**Opzioni**</span><span class="sxs-lookup"><span data-stu-id="3dddc-134">**Options**</span></span>    |
| ---  | --- 
| <span data-ttu-id="3dddc-135">Crittografia IKEv2</span><span class="sxs-lookup"><span data-stu-id="3dddc-135">IKEv2 Encryption</span></span> | <span data-ttu-id="3dddc-136">AES256, AES192, AES128, DES3, DES</span><span class="sxs-lookup"><span data-stu-id="3dddc-136">AES256, AES192, AES128, DES3, DES</span></span>  
| <span data-ttu-id="3dddc-137">Integrità IKEv2</span><span class="sxs-lookup"><span data-stu-id="3dddc-137">IKEv2 Integrity</span></span>  | <span data-ttu-id="3dddc-138">SHA384, SHA256, SHA1, MD5</span><span class="sxs-lookup"><span data-stu-id="3dddc-138">SHA384, SHA256, SHA1, MD5</span></span>  |
| <span data-ttu-id="3dddc-139">Gruppo DH</span><span class="sxs-lookup"><span data-stu-id="3dddc-139">DH Group</span></span>         | <span data-ttu-id="3dddc-140">DHGroup24, ECP384, ECP256, DHGroup14, DHGroup2048, DHGroup2, DHGroup1, None</span><span class="sxs-lookup"><span data-stu-id="3dddc-140">DHGroup24, ECP384, ECP256, DHGroup14, DHGroup2048, DHGroup2, DHGroup1, None</span></span> |
| <span data-ttu-id="3dddc-141">Crittografia IPsec</span><span class="sxs-lookup"><span data-stu-id="3dddc-141">IPsec Encryption</span></span> | <span data-ttu-id="3dddc-142">GCMAES256, GCMAES192, GCMAES128, AES256, AES192, AES128, DES3, DES, None</span><span class="sxs-lookup"><span data-stu-id="3dddc-142">GCMAES256, GCMAES192, GCMAES128, AES256, AES192, AES128, DES3, DES, None</span></span>    |
| <span data-ttu-id="3dddc-143">Integrità IPsec</span><span class="sxs-lookup"><span data-stu-id="3dddc-143">IPsec Integrity</span></span>  | <span data-ttu-id="3dddc-144">GCMASE256, GCMAES192, GCMAES128, SHA256, SHA1, MD5</span><span class="sxs-lookup"><span data-stu-id="3dddc-144">GCMASE256, GCMAES192, GCMAES128, SHA256, SHA1, MD5</span></span> |
| <span data-ttu-id="3dddc-145">Gruppo PFS</span><span class="sxs-lookup"><span data-stu-id="3dddc-145">PFS Group</span></span>        | <span data-ttu-id="3dddc-146">PFS24, ECP384, ECP256, PFS2048, PFS2, PFS1, None</span><span class="sxs-lookup"><span data-stu-id="3dddc-146">PFS24, ECP384, ECP256, PFS2048, PFS2, PFS1, None</span></span> 
| <span data-ttu-id="3dddc-147">Durata associazione di sicurezza in modalità rapida</span><span class="sxs-lookup"><span data-stu-id="3dddc-147">QM SA Lifetime</span></span>   | <span data-ttu-id="3dddc-148">(**Facoltativo**: se non diversamente specificato, vengono usati i valori predefiniti)</span><span class="sxs-lookup"><span data-stu-id="3dddc-148">(**Optional**: default values are used if not specified)</span></span><br><span data-ttu-id="3dddc-149">Secondi (intero; **min. 300**/valore predefinito di 27000 secondi)</span><span class="sxs-lookup"><span data-stu-id="3dddc-149">Seconds (integer; **min. 300**/default 27000 seconds)</span></span><br><span data-ttu-id="3dddc-150">Kilobyte (intero; **min 1024**/valore predefinito di 102400000 KB)</span><span class="sxs-lookup"><span data-stu-id="3dddc-150">KBytes (integer; **min. 1024**/default 102400000 KBytes)</span></span>   |
| <span data-ttu-id="3dddc-151">Selettore di traffico</span><span class="sxs-lookup"><span data-stu-id="3dddc-151">Traffic Selector</span></span> | <span data-ttu-id="3dddc-152">UsePolicyBasedTrafficSelectors** ($True/$False; **Optional**, $False predefinito, se non diversamente specificato)</span><span class="sxs-lookup"><span data-stu-id="3dddc-152">UsePolicyBasedTrafficSelectors** ($True/$False; **Optional**, default $False if not specified)</span></span>    |
|  |  |

> [!IMPORTANT]
> 1. <span data-ttu-id="3dddc-153">**Se GCMAES viene usato per l'algoritmo di crittografia IPsec, è necessario selezionare lo stesso algoritmo GCMAES e la stessa lunghezza della chiave per l'integrità IPsec, ad esempio, GCMAES128 per entrambi**</span><span class="sxs-lookup"><span data-stu-id="3dddc-153">**If GCMAES is used as for IPsec Encryption algorithm, you must select the same GCMAES algorithm and key length for IPsec Integrity; for example, using GCMAES128 for both**</span></span>
> 2. <span data-ttu-id="3dddc-154">Nei gateway VPN di Azure la durata dell'associazione di sicurezza IKEv2 (modalità principale) è fissata a 28800 secondi</span><span class="sxs-lookup"><span data-stu-id="3dddc-154">IKEv2 Main Mode SA lifetime is fixed at 28,800 seconds on the Azure VPN gateways</span></span>
> 3. <span data-ttu-id="3dddc-155">Impostando "UsePolicyBasedTrafficSelectors" su $True per una connessione, si configura il gateway VPN di Azure per la connessione al firewall VPN locale basato su criteri.</span><span class="sxs-lookup"><span data-stu-id="3dddc-155">Setting "UsePolicyBasedTrafficSelectors" to $True on a connection will configure the Azure VPN gateway to connect to policy-based VPN firewall on premises.</span></span> <span data-ttu-id="3dddc-156">Se si abilita PolicyBasedTrafficSelectors, è necessario verificare che i selettori di traffico corrispondenti siano definiti nel dispositivo VPN con tutte le combinazioni dei prefissi della rete locale (gateway di rete locale) da/verso i prefissi della rete virtuale di Azure, anziché any-to-any.</span><span class="sxs-lookup"><span data-stu-id="3dddc-156">If you enable PolicyBasedTrafficSelectors, you need to ensure your VPN device has the matching traffic selectors defined with all combinations of your on-premises network (local network gateway) prefixes to/from the Azure virtual network prefixes, instead of any-to-any.</span></span> <span data-ttu-id="3dddc-157">Se i prefissi della rete locale sono 10.1.0.0/16 e 10.2.0.0/16 e i prefissi della rete virtuale sono 192.168.0.0/16 e 172.16.0.0/16, ad esempio, è necessario specificare i selettori di traffico seguenti:</span><span class="sxs-lookup"><span data-stu-id="3dddc-157">For example, if your on-premises network prefixes are 10.1.0.0/16 and 10.2.0.0/16, and your virtual network prefixes are 192.168.0.0/16 and 172.16.0.0/16, you need to specify the following traffic selectors:</span></span>
>    * <span data-ttu-id="3dddc-158">10.1.0.0/16 <====> 192.168.0.0/16</span><span class="sxs-lookup"><span data-stu-id="3dddc-158">10.1.0.0/16 <====> 192.168.0.0/16</span></span>
>    * <span data-ttu-id="3dddc-159">10.1.0.0/16 <====> 172.16.0.0/16</span><span class="sxs-lookup"><span data-stu-id="3dddc-159">10.1.0.0/16 <====> 172.16.0.0/16</span></span>
>    * <span data-ttu-id="3dddc-160">10.2.0.0/16 <====> 192.168.0.0/16</span><span class="sxs-lookup"><span data-stu-id="3dddc-160">10.2.0.0/16 <====> 192.168.0.0/16</span></span>
>    * <span data-ttu-id="3dddc-161">10.2.0.0/16 <====> 172.16.0.0/16</span><span class="sxs-lookup"><span data-stu-id="3dddc-161">10.2.0.0/16 <====> 172.16.0.0/16</span></span>

<span data-ttu-id="3dddc-162">Per altre informazioni sui selettori di traffico basati su criteri, vedere [Connettere più dispositivi VPN basati su criteri locali](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="3dddc-162">For more information regarding policy-based traffic selectors, see [Connect multiple on-premises policy-based VPN devices](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span></span>

<span data-ttu-id="3dddc-163">La tabella seguente elenca i gruppi di Diffie-Hellman corrispondenti supportati dal criterio personalizzato:</span><span class="sxs-lookup"><span data-stu-id="3dddc-163">The following table lists the corresponding Diffie-Hellman Groups supported by the custom policy:</span></span>

| <span data-ttu-id="3dddc-164">**Gruppo Diffie-Hellman**</span><span class="sxs-lookup"><span data-stu-id="3dddc-164">**Diffie-Hellman Group**</span></span>  | <span data-ttu-id="3dddc-165">**DHGroup**</span><span class="sxs-lookup"><span data-stu-id="3dddc-165">**DHGroup**</span></span>              | <span data-ttu-id="3dddc-166">**PFSGroup**</span><span class="sxs-lookup"><span data-stu-id="3dddc-166">**PFSGroup**</span></span> | <span data-ttu-id="3dddc-167">**Lunghezza chiave**</span><span class="sxs-lookup"><span data-stu-id="3dddc-167">**Key length**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3dddc-168">1</span><span class="sxs-lookup"><span data-stu-id="3dddc-168">1</span></span>                         | <span data-ttu-id="3dddc-169">DHGroup1</span><span class="sxs-lookup"><span data-stu-id="3dddc-169">DHGroup1</span></span>                 | <span data-ttu-id="3dddc-170">PFS1</span><span class="sxs-lookup"><span data-stu-id="3dddc-170">PFS1</span></span>         | <span data-ttu-id="3dddc-171">MODP a 768 bit</span><span class="sxs-lookup"><span data-stu-id="3dddc-171">768-bit MODP</span></span>   |
| <span data-ttu-id="3dddc-172">2</span><span class="sxs-lookup"><span data-stu-id="3dddc-172">2</span></span>                         | <span data-ttu-id="3dddc-173">DHGroup2</span><span class="sxs-lookup"><span data-stu-id="3dddc-173">DHGroup2</span></span>                 | <span data-ttu-id="3dddc-174">PFS2</span><span class="sxs-lookup"><span data-stu-id="3dddc-174">PFS2</span></span>         | <span data-ttu-id="3dddc-175">MODP a 1024 bit</span><span class="sxs-lookup"><span data-stu-id="3dddc-175">1024-bit MODP</span></span>  |
| <span data-ttu-id="3dddc-176">14</span><span class="sxs-lookup"><span data-stu-id="3dddc-176">14</span></span>                        | <span data-ttu-id="3dddc-177">DHGroup14</span><span class="sxs-lookup"><span data-stu-id="3dddc-177">DHGroup14</span></span><br><span data-ttu-id="3dddc-178">DHGroup2048</span><span class="sxs-lookup"><span data-stu-id="3dddc-178">DHGroup2048</span></span> | <span data-ttu-id="3dddc-179">PFS2048</span><span class="sxs-lookup"><span data-stu-id="3dddc-179">PFS2048</span></span>      | <span data-ttu-id="3dddc-180">MODP a 2048 bit</span><span class="sxs-lookup"><span data-stu-id="3dddc-180">2048-bit MODP</span></span>  |
| <span data-ttu-id="3dddc-181">19</span><span class="sxs-lookup"><span data-stu-id="3dddc-181">19</span></span>                        | <span data-ttu-id="3dddc-182">ECP256</span><span class="sxs-lookup"><span data-stu-id="3dddc-182">ECP256</span></span>                   | <span data-ttu-id="3dddc-183">ECP256</span><span class="sxs-lookup"><span data-stu-id="3dddc-183">ECP256</span></span>       | <span data-ttu-id="3dddc-184">ECP a 256 bit</span><span class="sxs-lookup"><span data-stu-id="3dddc-184">256-bit ECP</span></span>    |
| <span data-ttu-id="3dddc-185">20</span><span class="sxs-lookup"><span data-stu-id="3dddc-185">20</span></span>                        | <span data-ttu-id="3dddc-186">ECP384</span><span class="sxs-lookup"><span data-stu-id="3dddc-186">ECP384</span></span>                   | <span data-ttu-id="3dddc-187">ECP284</span><span class="sxs-lookup"><span data-stu-id="3dddc-187">ECP284</span></span>       | <span data-ttu-id="3dddc-188">ECP a 384 bit</span><span class="sxs-lookup"><span data-stu-id="3dddc-188">384-bit ECP</span></span>    |
| <span data-ttu-id="3dddc-189">24</span><span class="sxs-lookup"><span data-stu-id="3dddc-189">24</span></span>                        | <span data-ttu-id="3dddc-190">DHGroup24</span><span class="sxs-lookup"><span data-stu-id="3dddc-190">DHGroup24</span></span>                | <span data-ttu-id="3dddc-191">PFS24</span><span class="sxs-lookup"><span data-stu-id="3dddc-191">PFS24</span></span>        | <span data-ttu-id="3dddc-192">MODP a 2048 bit</span><span class="sxs-lookup"><span data-stu-id="3dddc-192">2048-bit MODP</span></span>  |

<span data-ttu-id="3dddc-193">Per altre informazioni, vedere [RFC3526](https://tools.ietf.org/html/rfc3526) e [RFC5114](https://tools.ietf.org/html/rfc5114).</span><span class="sxs-lookup"><span data-stu-id="3dddc-193">Refer to [RFC3526](https://tools.ietf.org/html/rfc3526) and [RFC5114](https://tools.ietf.org/html/rfc5114) for more details.</span></span>

## <span data-ttu-id="3dddc-194"><a name ="crossprem"></a>Parte 3: Creare una nuova connessione VPN da sito a sito con criteri IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="3dddc-194"><a name ="crossprem"></a>Part 3 - Create a new S2S VPN connection with IPsec/IKE policy</span></span>

<span data-ttu-id="3dddc-195">Questa sezione illustra i passaggi per la creazione di una connessione VPN da sito a sito con un criterio IPsec/IKE.</span><span class="sxs-lookup"><span data-stu-id="3dddc-195">This section walks you through the steps of creating a S2S VPN connection with an IPsec/IKE policy.</span></span> <span data-ttu-id="3dddc-196">La procedura seguente crea la connessione illustrata nel diagramma:</span><span class="sxs-lookup"><span data-stu-id="3dddc-196">The following steps create the connection as shown in the diagram:</span></span>

![s2s-policy](./media/vpn-gateway-ipsecikepolicy-rm-powershell/s2spolicy.png)

<span data-ttu-id="3dddc-198">Per altre istruzioni dettagliate per la creazione di una connessione VPN da sito a sito, vedere [Creare una connessione VPN da sito a sito](vpn-gateway-create-site-to-site-rm-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="3dddc-198">See [Create a S2S VPN connection](vpn-gateway-create-site-to-site-rm-powershell.md) for more detailed step-by-step instructions for creating a S2S VPN connection.</span></span>

### <span data-ttu-id="3dddc-199"><a name="before"></a>Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="3dddc-199"><a name="before"></a>Before you begin</span></span>

* <span data-ttu-id="3dddc-200">Verificare di possedere una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="3dddc-200">Verify that you have an Azure subscription.</span></span> <span data-ttu-id="3dddc-201">Se non si ha una sottoscrizione di Azure, è possibile attivare i [vantaggi per i sottoscrittori di MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) oppure iscriversi per ottenere un [account gratuito](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3dddc-201">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="3dddc-202">Installare i cmdlet di PowerShell per Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="3dddc-202">Install the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="3dddc-203">Per altre informazioni sull'installazione di cmdlet PowerShell, vedere [Overview of Azure PowerShell](/powershell/azure/overview) (Panoramica di Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="3dddc-203">See [Overview of Azure PowerShell](/powershell/azure/overview) for more information about installing the PowerShell cmdlets.</span></span>

### <span data-ttu-id="3dddc-204"><a name="createvnet1"></a>Passaggio 1: Creare la rete virtuale, il gateway VPN e il gateway di rete locale</span><span class="sxs-lookup"><span data-stu-id="3dddc-204"><a name="createvnet1"></a>Step 1 - Create the virtual network, VPN gateway, and local network gateway</span></span>

#### <a name="1-declare-your-variables"></a><span data-ttu-id="3dddc-205">1. Dichiarare le variabili</span><span class="sxs-lookup"><span data-stu-id="3dddc-205">1. Declare your variables</span></span>

<span data-ttu-id="3dddc-206">Per questo esercizio, si inizierà dichiarando le variabili.</span><span class="sxs-lookup"><span data-stu-id="3dddc-206">For this exercise, we start by declaring our variables.</span></span> <span data-ttu-id="3dddc-207">Assicurarsi di sostituire i valori con quelli reali durante la configurazione per la produzione.</span><span class="sxs-lookup"><span data-stu-id="3dddc-207">Be sure to replace the values with your own when configuring for production.</span></span>

```powershell
$Sub1          = "<YourSubscriptionName>"
$RG1           = "TestPolicyRG1"
$Location1     = "East US 2"
$VNetName1     = "TestVNet1"
$FESubName1    = "FrontEnd"
$BESubName1    = "Backend"
$GWSubName1    = "GatewaySubnet"
$VNetPrefix11  = "10.11.0.0/16"
$VNetPrefix12  = "10.12.0.0/16"
$FESubPrefix1  = "10.11.0.0/24"
$BESubPrefix1  = "10.12.0.0/24"
$GWSubPrefix1  = "10.12.255.0/27"
$DNS1          = "8.8.8.8"
$GWName1       = "VNet1GW"
$GW1IPName1    = "VNet1GWIP1"
$GW1IPconf1    = "gw1ipconf1"
$Connection16  = "VNet1toSite6"

$LNGName6      = "Site6"
$LNGPrefix61   = "10.61.0.0/16"
$LNGPrefix62   = "10.62.0.0/16"
$LNGIP6        = "131.107.72.22"
```

#### <a name="2-connect-to-your-subscription-and-create-a-new-resource-group"></a><span data-ttu-id="3dddc-208">2. Connettersi alla sottoscrizione e creare un nuovo gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="3dddc-208">2. Connect to your subscription and create a new resource group</span></span>

<span data-ttu-id="3dddc-209">Verificare di passare alla modalità PowerShell per usare i cmdlet di Gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="3dddc-209">Make sure you switch to PowerShell mode to use the Resource Manager cmdlets.</span></span> <span data-ttu-id="3dddc-210">Per altre informazioni, vedere [Uso di Windows PowerShell con Gestione risorse](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="3dddc-210">For more information, see [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="3dddc-211">Aprire la console di PowerShell e connettersi al proprio account.</span><span class="sxs-lookup"><span data-stu-id="3dddc-211">Open your PowerShell console and connect to your account.</span></span> <span data-ttu-id="3dddc-212">Per connettersi, usare l'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="3dddc-212">Use the following sample to help you connect:</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="3-create-the-virtual-network-vpn-gateway-and-local-network-gateway"></a><span data-ttu-id="3dddc-213">3. Creare la rete virtuale, il gateway VPN e il gateway di rete locale</span><span class="sxs-lookup"><span data-stu-id="3dddc-213">3. Create the virtual network, VPN gateway, and local network gateway</span></span>

<span data-ttu-id="3dddc-214">L'esempio seguente crea la rete virtuale, TestVNet1 con tre subnet e il gateway VPN.</span><span class="sxs-lookup"><span data-stu-id="3dddc-214">The following sample creates the virtual network, TestVNet1, with three subnets, and the VPN gateway.</span></span> <span data-ttu-id="3dddc-215">Quando si sostituiscono i valori, è importante che la subnet gateway venga denominata sempre esattamente GatewaySubnet.</span><span class="sxs-lookup"><span data-stu-id="3dddc-215">When substituting values, it's important that you always name your gateway subnet specifically GatewaySubnet.</span></span> <span data-ttu-id="3dddc-216">Se si assegnano altri nomi, la creazione del gateway ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="3dddc-216">If you name it something else, your gateway creation fails.</span></span>

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1
$besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1

$gw1pip1    = New-AzureRmPublicIpAddress -Name $GW1IPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic
$vnet1      = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1    = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gw1ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW1IPconf1 -Subnet $subnet1 -PublicIpAddress $gw1pip1

New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gw1ipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku HighPerformance

New-AzureRmLocalNetworkGateway -Name $LNGName6 -ResourceGroupName $RG1 -Location $Location1 -GatewayIpAddress $LNGIP6 -AddressPrefix $LNGPrefix61,$LNGPrefix62
```

### <span data-ttu-id="3dddc-217"><a name="s2sconnection"></a>Passaggio 2: Creare una connessione VPN da sito a sito con un criterio IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="3dddc-217"><a name="s2sconnection"></a>Step 2 - Create a S2S VPN connection with an IPsec/IKE policy</span></span>

#### <a name="1-create-an-ipsecike-policy"></a><span data-ttu-id="3dddc-218">1. Creare un criterio IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="3dddc-218">1. Create an IPsec/IKE policy</span></span>

<span data-ttu-id="3dddc-219">Lo script di esempio che segue crea un criterio IPsec/IKE con gli algoritmi e i parametri seguenti:</span><span class="sxs-lookup"><span data-stu-id="3dddc-219">The following sample script creates an IPsec/IKE policy with the following algorithms and parameters:</span></span>

* <span data-ttu-id="3dddc-220">IKEv2: AES256, SHA384, DHGroup24</span><span class="sxs-lookup"><span data-stu-id="3dddc-220">IKEv2: AES256, SHA384, DHGroup24</span></span>
* <span data-ttu-id="3dddc-221">IPsec: AES256, SHA256, PFS24, durata dell'associazione di sicurezza 7200 secondi e 2048 KB</span><span class="sxs-lookup"><span data-stu-id="3dddc-221">IPsec: AES256, SHA256, PFS24, SA Lifetime 7200 seconds & 2048KB</span></span>

```powershell
$ipsecpolicy6 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption AES256 -IpsecIntegrity SHA256 -PfsGroup PFS24 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 2048
```

<span data-ttu-id="3dddc-222">Se si usa GCMAES per IPsec, è necessario usare lo stesso algoritmo e la stessa lunghezza della chiave GCMAES per la crittografia e l'integrità IPsec, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="3dddc-222">If you use GCMAES for IPsec, you must use the same GCMAES algorithm and key length for both IPsec encryption and integrity, for example:</span></span>

* <span data-ttu-id="3dddc-223">IKEv2: AES256, SHA384, DHGroup24</span><span class="sxs-lookup"><span data-stu-id="3dddc-223">IKEv2: AES256, SHA384, DHGroup24</span></span>
* <span data-ttu-id="3dddc-224">IPsec: **GCMAES256, GCMAES256**, PFS24, durata dell'associazione di sicurezza 7200 secondi e 2048 KB</span><span class="sxs-lookup"><span data-stu-id="3dddc-224">IPsec: **GCMAES256, GCMAES256**, PFS24, SA Lifetime 7200 seconds & 2048KB</span></span>

```powershell
$ipsecpolicy6 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption GCMAES256 -IpsecIntegrity GCMAES256 -PfsGroup PFS24 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 2048
```

#### <a name="2-create-the-s2s-vpn-connection-with-the-ipsecike-policy"></a><span data-ttu-id="3dddc-225">2. Creare la connessione VPN da sito a sito con i criteri IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="3dddc-225">2. Create the S2S VPN connection with the IPsec/IKE policy</span></span>

<span data-ttu-id="3dddc-226">Creare una connessione VPN da sito a sito e applicare il criterio IPsec/IKE creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="3dddc-226">Create an S2S VPN connection and apply the IPsec/IKE policy created earlier.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng6 = Get-AzureRmLocalNetworkGateway  -Name $LNGName6 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng6 -Location $Location1 -ConnectionType IPsec -IpsecPolicies $ipsecpolicy6 -SharedKey 'AzureA1b2C3'
```

<span data-ttu-id="3dddc-227">È possibile aggiungere facoltativamente "-UsePolicyBasedTrafficSelectors $True" al cmdlet di creazione della connessione per abilitare il gateway VPN di Azure per la connessione a dispositivi VPN basati su criteri locali, come descritto sopra.</span><span class="sxs-lookup"><span data-stu-id="3dddc-227">You can optionally add "-UsePolicyBasedTrafficSelectors $True" to the create connection cmdlet to enable Azure VPN gateway to connect to policy-based VPN devices on premises, as described above.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3dddc-228">Dopo aver specificato un criterio IPsec/IKE per una connessione, il gateway VPN di Azure invierà o accetterà la proposta IPsec/IKE con gli algoritmi di crittografia e i principali vantaggi specificati per una particolare connessione.</span><span class="sxs-lookup"><span data-stu-id="3dddc-228">Once an IPsec/IKE policy is specified on a connection, the Azure VPN gateway will only send or accept the IPsec/IKE proposal with specified cryptographic algorithms and key strengths on that particular connection.</span></span> <span data-ttu-id="3dddc-229">Assicurarsi che il dispositivo VPN locale per la connessione usi o accetti l'esatta combinazione di criteri. In caso contrario, il tunnel VPN da sito a sito non verrà stabilito.</span><span class="sxs-lookup"><span data-stu-id="3dddc-229">Make sure your on-premises VPN device for the connection uses or accepts the exact policy combination, otherwise the S2S VPN tunnel will not establish.</span></span>


## <span data-ttu-id="3dddc-230"><a name ="vnet2vnet"></a>Parte 4: Creare una nuova connessione da rete virtuale a rete virtuale con criteri IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="3dddc-230"><a name ="vnet2vnet"></a>Part 4 - Create a new VNet-to-VNet connection with IPsec/IKE policy</span></span>

<span data-ttu-id="3dddc-231">La procedura di creazione di una connessione da rete virtuale a rete virtuale con un criterio IPsec/IKE è simile a quella di una connessione VPN da sito a sito.</span><span class="sxs-lookup"><span data-stu-id="3dddc-231">The steps of creating a VNet-to-VNet connection with an IPsec/IKE policy are similar to that of a S2S VPN connection.</span></span> <span data-ttu-id="3dddc-232">Gli script di esempio seguenti creano la connessione come illustrato nel diagramma:</span><span class="sxs-lookup"><span data-stu-id="3dddc-232">The following sample scripts create the connection as shown in the diagram:</span></span>

![v2v-policy](./media/vpn-gateway-ipsecikepolicy-rm-powershell/v2vpolicy.png)

<span data-ttu-id="3dddc-234">Per la procedura dettagliata di creazione di una connessione da rete virtuale a rete virtuale, vedere [Creare una connessione tra reti virtuali](vpn-gateway-vnet-vnet-rm-ps.md) .</span><span class="sxs-lookup"><span data-stu-id="3dddc-234">See [Create a VNet-to-VNet connection](vpn-gateway-vnet-vnet-rm-ps.md) for more detailed steps for creating a VNet-to-VNet connection.</span></span> <span data-ttu-id="3dddc-235">È necessario completare la [Parte 3](#crossprem) per creare e configurare TestVNet1 e il gateway VPN.</span><span class="sxs-lookup"><span data-stu-id="3dddc-235">You must complete [Part 3](#crossprem) to create and configure TestVNet1 and the VPN Gateway.</span></span>

### <span data-ttu-id="3dddc-236"><a name="createvnet2"></a>Passaggio 1: Creare la seconda rete virtuale e un gateway VPN</span><span class="sxs-lookup"><span data-stu-id="3dddc-236"><a name="createvnet2"></a>Step 1 - Create the second virtual network and VPN gateway</span></span>

#### <a name="1-declare-your-variables"></a><span data-ttu-id="3dddc-237">1. Dichiarare le variabili</span><span class="sxs-lookup"><span data-stu-id="3dddc-237">1. Declare your variables</span></span>

<span data-ttu-id="3dddc-238">Sostituire i valori con quelli desiderati per la propria configurazione.</span><span class="sxs-lookup"><span data-stu-id="3dddc-238">Be sure to replace the values with the ones that you want to use for your configuration.</span></span>

```powershell
$RG2          = "TestPolicyRG2"
$Location2    = "East US 2"
$VNetName2    = "TestVNet2"
$FESubName2   = "FrontEnd"
$BESubName2   = "Backend"
$GWSubName2   = "GatewaySubnet"
$VNetPrefix21 = "10.21.0.0/16"
$VNetPrefix22 = "10.22.0.0/16"
$FESubPrefix2 = "10.21.0.0/24"
$BESubPrefix2 = "10.22.0.0/24"
$GWSubPrefix2 = "10.22.255.0/27"
$DNS2         = "8.8.8.8"
$GWName2      = "VNet2GW"
$GW2IPName1   = "VNet2GWIP1"
$GW2IPconf1   = "gw2ipconf1"
$Connection21 = "VNet2toVNet1"
$Connection12 = "VNet1toVNet2"
```

#### <a name="2-create-the-second-virtual-network-and-vpn-gateway-in-the-new-resource-group"></a><span data-ttu-id="3dddc-239">2. Creare la seconda rete virtuale e un gateway VPN nel nuovo gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="3dddc-239">2. Create the second virtual network and VPN gateway in the new resource group</span></span>

```powershell
New-AzureRmResourceGroup -Name $RG2 -Location $Location2

$fesub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName2 -AddressPrefix $FESubPrefix2
$besub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName2 -AddressPrefix $BESubPrefix2
$gwsub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName2 -AddressPrefix $GWSubPrefix2

New-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2 -Location $Location2 -AddressPrefix $VNetPrefix21,$VNetPrefix22 -Subnet $fesub2,$besub2,$gwsub2

$gw2pip1    = New-AzureRmPublicIpAddress -Name $GW2IPName1 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic
$vnet2      = Get-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2
$subnet2    = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet2
$gw2ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW2IPconf1 -Subnet $subnet2 -PublicIpAddress $gw2pip1

New-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2 -Location $Location2 -IpConfigurations $gw2ipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku HighPerformance
```

### <a name="step-2---create-a-vnet-tovnet-connection-with-the-ipsecike-policy"></a><span data-ttu-id="3dddc-240">Passaggio 2: Creare una connessione da rete virtuale a rete virtuale con il criterio IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="3dddc-240">Step 2 - Create a VNet-toVNet connection with the IPsec/IKE policy</span></span>

<span data-ttu-id="3dddc-241">Come per la connessione VPN da sito a sito, creare un criterio IPsec/IKE e quindi applicare i criteri alla nuova connessione.</span><span class="sxs-lookup"><span data-stu-id="3dddc-241">Similar to the S2S VPN connection, create an IPsec/IKE policy then apply to policy to the new connection.</span></span>

#### <a name="1-create-an-ipsecike-policy"></a><span data-ttu-id="3dddc-242">1. Creare un criterio IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="3dddc-242">1. Create an IPsec/IKE policy</span></span>

<span data-ttu-id="3dddc-243">Lo script di esempio seguente crea un criterio IPsec/IKE diverso con gli algoritmi e i parametri seguenti:</span><span class="sxs-lookup"><span data-stu-id="3dddc-243">The following sample script creates a different IPsec/IKE policy with the following algorithms and parameters:</span></span>
* <span data-ttu-id="3dddc-244">IKEv2: AES128, SHA1, DHGroup14</span><span class="sxs-lookup"><span data-stu-id="3dddc-244">IKEv2: AES128, SHA1, DHGroup14</span></span>
* <span data-ttu-id="3dddc-245">IPsec: GCMAES128, GCMAES128, PFS14, durata dell'associazione di sicurezza 7200 secondi e 4096 KB</span><span class="sxs-lookup"><span data-stu-id="3dddc-245">IPsec: GCMAES128, GCMAES128, PFS14, SA Lifetime 7200 seconds & 4096KB</span></span>

```powershell
$ipsecpolicy2 = New-AzureRmIpsecPolicy -IkeEncryption AES128 -IkeIntegrity SHA1 -DhGroup DHGroup14 -IpsecEncryption GCMAES128 -IpsecIntegrity GCMAES128 -PfsGroup PFS14 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 4096
```

#### <a name="2-create-vnet-to-vnet-connections-with-the-ipsecike-policy"></a><span data-ttu-id="3dddc-246">2. Creare connessioni da rete virtuale a rete virtuale con criteri IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="3dddc-246">2. Create VNet-to-VNet connections with the IPsec/IKE policy</span></span>

<span data-ttu-id="3dddc-247">Creare una connessione da rete virtuale a rete virtuale e applicare il criterio IPsec/IKE creato.</span><span class="sxs-lookup"><span data-stu-id="3dddc-247">Create a VNet-to-VNet connection and apply the IPsec/IKE policy you created.</span></span> <span data-ttu-id="3dddc-248">In questo esempio entrambi i gateway sono nella stessa sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="3dddc-248">In this example, both gateways are in the same subscription.</span></span> <span data-ttu-id="3dddc-249">È possibile creare e configurare entrambe le connessioni con lo stesso criterio IPsec/IKE nella stessa sessione di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3dddc-249">So it is possible to create and configure both connections with the same IPsec/IKE policy in the same PowerShell session.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$vnet2gw = Get-AzureRmVirtualNetworkGateway -Name $GWName2  -ResourceGroupName $RG2

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection12 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet2gw -Location $Location1 -ConnectionType Vnet2Vnet -IpsecPolicies $ipsecpolicy2 -SharedKey 'AzureA1b2C3'

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection21 -ResourceGroupName $RG2 -VirtualNetworkGateway1 $vnet2gw -VirtualNetworkGateway2 $vnet1gw -Location $Location2 -ConnectionType Vnet2Vnet -IpsecPolicies $ipsecpolicy2 -SharedKey 'AzureA1b2C3'
```

> [!IMPORTANT]
> <span data-ttu-id="3dddc-250">Dopo aver specificato un criterio IPsec/IKE per una connessione, il gateway VPN di Azure invierà o accetterà la proposta IPsec/IKE con gli algoritmi di crittografia e i principali vantaggi specificati per una particolare connessione.</span><span class="sxs-lookup"><span data-stu-id="3dddc-250">Once an IPsec/IKE policy is specified on a connection, the Azure VPN gateway will only send or accept the IPsec/IKE proposal with specified cryptographic algorithms and key strengths on that particular connection.</span></span> <span data-ttu-id="3dddc-251">Assicurarsi che i criteri IPsec per entrambe le connessioni siano gli stessi. In caso contrario, la connessione da rete virtuale a rete virtuale non verrà stabilita.</span><span class="sxs-lookup"><span data-stu-id="3dddc-251">Make sure the IPsec policies for both connections are the same, otherwise the VNet-to-VNet connection will not establish.</span></span>

<span data-ttu-id="3dddc-252">Dopo aver completato questi passaggi, la connessione verrà stabilita in pochi minuti e si avrà la topologia di rete seguente, come illustrato all'inizio:</span><span class="sxs-lookup"><span data-stu-id="3dddc-252">After completing these steps, the connection is established in a few minutes, and you will have the following network topology as shown in the beginning:</span></span>

![ipsec-ike-policy](./media/vpn-gateway-ipsecikepolicy-rm-powershell/ipsecikepolicy.png)


## <span data-ttu-id="3dddc-254"><a name ="managepolicy"></a>Parte 5: Aggiornare i criteri IPsec/IKE per una connessione</span><span class="sxs-lookup"><span data-stu-id="3dddc-254"><a name ="managepolicy"></a>Part 5 - Update IPsec/IKE policy for a connection</span></span>

<span data-ttu-id="3dddc-255">L'ultima sezione illustra come gestire criteri IPsec/IKE per una connessione da sito a sito o da rete virtuale a rete virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="3dddc-255">The last section shows you how to manage IPsec/IKE policy for an existing S2S or VNet-to-VNet connection.</span></span> <span data-ttu-id="3dddc-256">La procedura descritta di seguito illustra le operazioni seguenti su una connessione:</span><span class="sxs-lookup"><span data-stu-id="3dddc-256">The exercise below walks you through the following operations on a connection:</span></span>

1. <span data-ttu-id="3dddc-257">Mostrare il criterio IPsec/IKE di una connessione</span><span class="sxs-lookup"><span data-stu-id="3dddc-257">Show the IPsec/IKE policy of a connection</span></span>
2. <span data-ttu-id="3dddc-258">Aggiungere o aggiornare il criterio IPsec/IKE per una connessione</span><span class="sxs-lookup"><span data-stu-id="3dddc-258">Add or update the IPsec/IKE policy to a connection</span></span>
3. <span data-ttu-id="3dddc-259">Rimuovere il criterio IPsec/IKE da una connessione</span><span class="sxs-lookup"><span data-stu-id="3dddc-259">Remove the IPsec/IKE policy from a connection</span></span>

<span data-ttu-id="3dddc-260">Gli stessi passaggi si applicano sia alle connessioni da sito a sito sia alle connessioni da rete virtuale a rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="3dddc-260">The same steps apply to both S2S and VNet-to-VNet connections.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3dddc-261">Il criterio IPsec/IKE è supportato solo nei gateway VPN *Standard* e *Prestazioni elevate* basati su route di Azure.</span><span class="sxs-lookup"><span data-stu-id="3dddc-261">IPsec/IKE policy is supported on *Standard* and *HighPerformance* route-based VPN gateways only.</span></span> <span data-ttu-id="3dddc-262">Non funziona sullo SKU per il gateway Basic o il gateway VPN basato su criteri.</span><span class="sxs-lookup"><span data-stu-id="3dddc-262">It does not work on the Basic gateway SKU or the policy-based VPN gateway.</span></span>

#### <a name="1-show-the-ipsecike-policy-of-a-connection"></a><span data-ttu-id="3dddc-263">1. Mostrare il criterio IPsec/IKE di una connessione</span><span class="sxs-lookup"><span data-stu-id="3dddc-263">1. Show the IPsec/IKE policy of a connection</span></span>

<span data-ttu-id="3dddc-264">L'esempio seguente illustra come ottenere il criterio IPsec/IKE configurato su una connessione.</span><span class="sxs-lookup"><span data-stu-id="3dddc-264">The following example shows how to get the IPsec/IKE policy configured on a connection.</span></span> <span data-ttu-id="3dddc-265">Gli script continuano dagli esercizi precedenti.</span><span class="sxs-lookup"><span data-stu-id="3dddc-265">The scripts also continue from the exercises above.</span></span>

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1
$connection6.IpsecPolicies
```

<span data-ttu-id="3dddc-266">L'ultimo comando elenca i criteri IPsec/IKE correnti configurati per la connessione, se esistenti.</span><span class="sxs-lookup"><span data-stu-id="3dddc-266">The last command lists the current IPsec/IKE policy configured on the connection, if there is any.</span></span> <span data-ttu-id="3dddc-267">L'output di esempio seguente si riferisce alla connessione:</span><span class="sxs-lookup"><span data-stu-id="3dddc-267">The following sample output is for the connection:</span></span>

```powershell
SALifeTimeSeconds   : 3600
SADataSizeKilobytes : 2048
IpsecEncryption     : AES256
IpsecIntegrity      : SHA256
IkeEncryption       : AES256
IkeIntegrity        : SHA384
DhGroup             : DHGroup24
PfsGroup            : PFS24
```

<span data-ttu-id="3dddc-268">Se non c'è alcun criterio IPsec/IKE configurato, il comando (PS> $connection6.policy) non restituisce nulla.</span><span class="sxs-lookup"><span data-stu-id="3dddc-268">If there is no IPsec/IKE policy configured, the command (PS> $connection6.policy) gets an empty return.</span></span> <span data-ttu-id="3dddc-269">Ciò non significa che IPsec/IKE non sia configurato per la connessione, ma che non c'è alcun criterio IPsec/IKE personalizzato.</span><span class="sxs-lookup"><span data-stu-id="3dddc-269">It does not mean IPsec/IKE is not configured on the connection, but that there is no custom IPsec/IKE policy.</span></span> <span data-ttu-id="3dddc-270">La connessione effettiva usa il criterio predefinito negoziato tra il dispositivo VPN locale e il gateway VPN di Azure.</span><span class="sxs-lookup"><span data-stu-id="3dddc-270">The actual connection uses the default policy negotiated between your on-premises VPN device and the Azure VPN gateway.</span></span>

#### <a name="2-add-or-update-an-ipsecike-policy-for-a-connection"></a><span data-ttu-id="3dddc-271">2. Aggiungere o aggiornare un criterio IPsec/IKE per una connessione</span><span class="sxs-lookup"><span data-stu-id="3dddc-271">2. Add or update an IPsec/IKE policy for a connection</span></span>

<span data-ttu-id="3dddc-272">La procedura per aggiungere un nuovo criterio o aggiornare un criterio esistente per una connessione è la stessa: creare un nuovo criterio, quindi applicare il nuovo criterio alla connessione.</span><span class="sxs-lookup"><span data-stu-id="3dddc-272">The steps to add a new policy or update an existing policy on a connection are the same: create a new policy then apply the new policy to the connection.</span></span>

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

$newpolicy6   = New-AzureRmIpsecPolicy -IkeEncryption AES128 -IkeIntegrity SHA1 -DhGroup DHGroup14 -IpsecEncryption GCMAES128 -IpsecIntegrity GCMAES128 -PfsGroup None -SALifeTimeSeconds 3600 -SADataSizeKilobytes 2048

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -IpsecPolicies $newpolicy6
```

<span data-ttu-id="3dddc-273">Per abilitare "UsePolicyBasedTrafficSelectors" quando ci si connette a un dispositivo VPN basato su criteri locale, aggiungere il parametro "-UsePolicyBaseTrafficSelectors" al cmdlet o impostarlo su $False per disabilitare l'opzione:</span><span class="sxs-lookup"><span data-stu-id="3dddc-273">To enable "UsePolicyBasedTrafficSelectors" when connecting to an on-premises policy-based VPN device, add the "-UsePolicyBaseTrafficSelectors" parameter to the cmdlet, or set it to $False to disable the option:</span></span>

```powershell
Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -IpsecPolicies $newpolicy6 -UsePolicyBasedTrafficSelectors $True
```

<span data-ttu-id="3dddc-274">È possibile ottenere di nuovo la connessione per verificare se i criteri sono aggiornati.</span><span class="sxs-lookup"><span data-stu-id="3dddc-274">You can get the connection again to check if the policy is updated.</span></span>

```powershell
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1
$connection6.IpsecPolicies
```

<span data-ttu-id="3dddc-275">Verrà visualizzato l'output dell'ultima riga, come illustrato nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="3dddc-275">You should see the output from the last line, as shown in the following example:</span></span>

```powershell
SALifeTimeSeconds   : 3600
SADataSizeKilobytes : 2048
IpsecEncryption     : GCMAES128
IpsecIntegrity      : GCMAES128
IkeEncryption       : AES128
IkeIntegrity        : SHA1
DhGroup             : DHGroup14--
PfsGroup            : None
```

#### <a name="3-remove-an-ipsecike-policy-from-a-connection"></a><span data-ttu-id="3dddc-276">3. Rimuovere un criterio IPsec/IKE da una connessione</span><span class="sxs-lookup"><span data-stu-id="3dddc-276">3. Remove an IPsec/IKE policy from a connection</span></span>

<span data-ttu-id="3dddc-277">Dopo la rimozione dei criteri personalizzati da una connessione, il gateway VPN di Azure ripristina l'[elenco predefinito delle proposte IPsec/IKE](vpn-gateway-about-vpn-devices.md) e rinegozia l'handshake IKE con il dispositivo VPN locale.</span><span class="sxs-lookup"><span data-stu-id="3dddc-277">Once you remove the custom policy from a connection, the Azure VPN gateway reverts back to the [default list of IPsec/IKE proposals](vpn-gateway-about-vpn-devices.md) and renegotiates again with your on-premises VPN device.</span></span>

```powershell
$RG1           = "TestPolicyRG1"
$Connection16  = "VNet1toSite6"
$connection6   = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

$currentpolicy = $connection6.IpsecPolicies[0]
$connection6.IpsecPolicies.Remove($currentpolicy)

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6
```

<span data-ttu-id="3dddc-278">È possibile usare lo stesso script per verificare se il criterio è stato rimosso dalla connessione.</span><span class="sxs-lookup"><span data-stu-id="3dddc-278">You can use the same script to check if the policy has been removed from the connection.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3dddc-279">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3dddc-279">Next steps</span></span>

<span data-ttu-id="3dddc-280">Per altri dettagli sui selettori di traffico basati su criteri, vedere l'articolo su come [connettere più dispositivi VPN basati su criteri locali](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="3dddc-280">See [Connect multiple on-premises policy-based VPN devices](vpn-gateway-connect-multiple-policybased-rm-ps.md) for more details regarding policy-based traffic selectors.</span></span>

<span data-ttu-id="3dddc-281">Dopo aver completato la connessione, è possibile aggiungere macchine virtuali alle reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="3dddc-281">Once your connection is complete, you can add virtual machines to your virtual networks.</span></span> <span data-ttu-id="3dddc-282">Per i passaggi, vedere [Creare la prima macchina virtuale](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) .</span><span class="sxs-lookup"><span data-stu-id="3dddc-282">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>