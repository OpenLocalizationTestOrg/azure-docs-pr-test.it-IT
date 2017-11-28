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
ms.openlocfilehash: f8d2e29276efdec7071f2aa0d463b1abd64a5253
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-ipsecike-policy-for-s2s-vpn-or-vnet-to-vnet-connections"></a><span data-ttu-id="5761d-103">Configurare criteri IPsec/IKE per connessioni VPN da sito a sito o da rete virtuale a rete virtuale</span><span class="sxs-lookup"><span data-stu-id="5761d-103">Configure IPsec/IKE policy for S2S VPN or VNet-to-VNet connections</span></span>

<span data-ttu-id="5761d-104">In questo articolo illustra i passaggi di hello tooconfigure criteri IPsec/IKE per le connessioni VPN da sito a sito o di rete virtuale a con modello di distribuzione di gestione risorse di hello e PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5761d-104">This article walks you through hello steps tooconfigure IPsec/IKE policy for Site-to-Site VPN or VNet-to-VNet connections using hello Resource Manager deployment model and PowerShell.</span></span>

## <span data-ttu-id="5761d-105"><a name="about"></a>Informazioni sui parametri dei criteri IPsec e IKE per gateway VPN di Azure</span><span class="sxs-lookup"><span data-stu-id="5761d-105"><a name="about"></a>About IPsec and IKE policy parameters for Azure VPN gateways</span></span>
<span data-ttu-id="5761d-106">Lo standard di protocollo IPsec e IKE supporta un'ampia gamma di algoritmi di crittografia in varie combinazioni.</span><span class="sxs-lookup"><span data-stu-id="5761d-106">IPsec and IKE protocol standard supports a wide range of cryptographic algorithms in various combinations.</span></span> <span data-ttu-id="5761d-107">Fare riferimento troppo[sui requisiti di crittografia e i gateway VPN di Azure](vpn-gateway-about-compliance-crypto.md) toosee come questo consente di garantire cross-premise e la connettività di rete virtuale a soddisfare i requisiti di conformità o la sicurezza.</span><span class="sxs-lookup"><span data-stu-id="5761d-107">Refer too[About cryptographic requirements and Azure VPN gateways](vpn-gateway-about-compliance-crypto.md) toosee how this can help ensuring cross-premises and VNet-to-VNet connectivity satisfy your compliance or security requirements.</span></span>

<span data-ttu-id="5761d-108">In questo articolo fornisce istruzioni toocreate e configurare un criterio IPsec/IKE e applicare una connessione nuova o esistente tooa:</span><span class="sxs-lookup"><span data-stu-id="5761d-108">This article provides instructions toocreate and configure an IPsec/IKE policy and apply tooa new or existing connection:</span></span>

* [<span data-ttu-id="5761d-109">Parte 1 - toocreate del flusso di lavoro e impostare i criteri IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="5761d-109">Part 1 - Workflow toocreate and set IPsec/IKE policy</span></span>](#workflow)
* [<span data-ttu-id="5761d-110">Parte 2: Algoritmi di crittografia supportati e vantaggi chiave</span><span class="sxs-lookup"><span data-stu-id="5761d-110">Part 2 - Supported cryptographic algorithms and key strengths</span></span>](#params)
* [<span data-ttu-id="5761d-111">Parte 3: Creare una nuova connessione VPN da sito a sito con criteri IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="5761d-111">Part 3 - Create a new S2S VPN connection with IPsec/IKE policy</span></span>](#crossprem)
* [<span data-ttu-id="5761d-112">Parte 4: Creare una nuova connessione da rete virtuale a rete virtuale con criteri IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="5761d-112">Part 4 - Create a new VNet-to-VNet connection with IPsec/IKE policy</span></span>](#vnet2vnet)
* [<span data-ttu-id="5761d-113">Parte 5: Gestire (creare, aggiungere, rimuovere) criteri IPsec/IKE per una connessione</span><span class="sxs-lookup"><span data-stu-id="5761d-113">Part 5 - Manage (create, add, remove) IPsec/IKE policy for a connection</span></span>](#managepolicy)

> [!IMPORTANT]
> 1. <span data-ttu-id="5761d-114">Si noti che i criteri IPsec/IKE funziona solo su hello SKU di gateway di seguito:</span><span class="sxs-lookup"><span data-stu-id="5761d-114">Note that IPsec/IKE policy only works on hello following gateway SKUs:</span></span>
>    * <span data-ttu-id="5761d-115">***VpnGw1, VpnGw2, VpnGw3*** (basato su route)</span><span class="sxs-lookup"><span data-stu-id="5761d-115">***VpnGw1, VpnGw2, VpnGw3*** (route-based)</span></span>
>    * <span data-ttu-id="5761d-116">***Standard*** e ***HighPerformance*** (basato su route)</span><span class="sxs-lookup"><span data-stu-id="5761d-116">***Standard*** and ***HighPerformance*** (route-based)</span></span>
> 2. <span data-ttu-id="5761d-117">Per una determinata connessione è possibile specificare ***una*** sola combinazione di criteri.</span><span class="sxs-lookup"><span data-stu-id="5761d-117">You can only specify ***one*** policy combination for a given connection.</span></span>
> 3. <span data-ttu-id="5761d-118">È necessario specificare tutti gli algoritmi e i parametri sia per IKE (modalità principale) che per IPsec (modalità rapida).</span><span class="sxs-lookup"><span data-stu-id="5761d-118">You must specify all algorithms and parameters for both IKE (Main Mode) and IPsec (Quick Mode).</span></span> <span data-ttu-id="5761d-119">Non è consentito specificare criteri parziali.</span><span class="sxs-lookup"><span data-stu-id="5761d-119">Partial policy specification is not allowed.</span></span>
> 4. <span data-ttu-id="5761d-120">Consultare le specifiche di fornitore dispositivo VPN criteri hello tooensure sono supportato nei dispositivi VPN locali.</span><span class="sxs-lookup"><span data-stu-id="5761d-120">Consult with your VPN device vendor specifications tooensure hello policy is supported on your on-premises VPN devices.</span></span> <span data-ttu-id="5761d-121">S2S o connessioni di rete virtuale a non è possibile stabilire se i criteri di hello non sono compatibili.</span><span class="sxs-lookup"><span data-stu-id="5761d-121">S2S or VNet-to-VNet connections cannot establish if hello policies are incompatible.</span></span>

## <span data-ttu-id="5761d-122"><a name ="workflow"></a>Parte 1 - toocreate del flusso di lavoro e impostare i criteri IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="5761d-122"><a name ="workflow"></a>Part 1 - Workflow toocreate and set IPsec/IKE policy</span></span>
<span data-ttu-id="5761d-123">Questa sezione vengono descritti hello del flusso di lavoro toocreate e aggiornamento IPsec/IKE criteri su una connessione VPN S2S o di rete virtuale a:</span><span class="sxs-lookup"><span data-stu-id="5761d-123">This section outlines hello workflow toocreate and update IPsec/IKE policy on a S2S VPN or VNet-to-VNet connection:</span></span>
1. <span data-ttu-id="5761d-124">Creare una rete virtuale e un gateway VPN</span><span class="sxs-lookup"><span data-stu-id="5761d-124">Create a virtual network and a VPN gateway</span></span>
2. <span data-ttu-id="5761d-125">Creare un gateway di rete locale per una connessione cross-premises o un'altra rete virtuale e gateway per una connessione da rete virtuale a rete virtuale</span><span class="sxs-lookup"><span data-stu-id="5761d-125">Create a local network gateway for cross premises connection, or another virtual network and gateway for VNet-to-VNet connection</span></span>
3. <span data-ttu-id="5761d-126">Creare un criterio IPsec/IKE con gli algoritmi e i parametri selezionati</span><span class="sxs-lookup"><span data-stu-id="5761d-126">Create an IPsec/IKE policy with selected algorithms and parameters</span></span>
4. <span data-ttu-id="5761d-127">Creare una connessione VNet2VNet (IPsec) con i criteri IPsec/IKE hello</span><span class="sxs-lookup"><span data-stu-id="5761d-127">Create a connection (IPsec or VNet2VNet) with hello IPsec/IKE policy</span></span>
5. <span data-ttu-id="5761d-128">Aggiungere, aggiornare o rimuovere un criterio IPsec/IKE per una connessione esistente</span><span class="sxs-lookup"><span data-stu-id="5761d-128">Add/update/remove an IPsec/IKE policy for an existing connection</span></span>

<span data-ttu-id="5761d-129">istruzioni di Hello in questo articolo consente di impostare e configurare i criteri IPsec/IKE, come illustrato nel diagramma hello:</span><span class="sxs-lookup"><span data-stu-id="5761d-129">hello instructions in this article helps you set up and configure IPsec/IKE policies as shown in hello diagram:</span></span>

![ipsec-ike-policy](./media/vpn-gateway-ipsecikepolicy-rm-powershell/ipsecikepolicy.png)

## <span data-ttu-id="5761d-131"><a name ="params"></a>Parte 2: Algoritmi di crittografia supportati e vantaggi chiave</span><span class="sxs-lookup"><span data-stu-id="5761d-131"><a name ="params"></a>Part 2 - Supported cryptographic algorithms & key strengths</span></span>

<span data-ttu-id="5761d-132">Hello nella tabella seguente sono elencati gli algoritmi di crittografia supportato hello e vantaggi chiave configurabile da parte dei clienti hello:</span><span class="sxs-lookup"><span data-stu-id="5761d-132">hello following table lists hello supported cryptographic algorithms and key strengths configurable by hello customers:</span></span>

| <span data-ttu-id="5761d-133">**IPsec/IKEv2**</span><span class="sxs-lookup"><span data-stu-id="5761d-133">**IPsec/IKEv2**</span></span>  | <span data-ttu-id="5761d-134">**Opzioni**</span><span class="sxs-lookup"><span data-stu-id="5761d-134">**Options**</span></span>    |
| ---  | --- 
| <span data-ttu-id="5761d-135">Crittografia IKEv2</span><span class="sxs-lookup"><span data-stu-id="5761d-135">IKEv2 Encryption</span></span> | <span data-ttu-id="5761d-136">AES256, AES192, AES128, DES3, DES</span><span class="sxs-lookup"><span data-stu-id="5761d-136">AES256, AES192, AES128, DES3, DES</span></span>  
| <span data-ttu-id="5761d-137">Integrità IKEv2</span><span class="sxs-lookup"><span data-stu-id="5761d-137">IKEv2 Integrity</span></span>  | <span data-ttu-id="5761d-138">SHA384, SHA256, SHA1, MD5</span><span class="sxs-lookup"><span data-stu-id="5761d-138">SHA384, SHA256, SHA1, MD5</span></span>  |
| <span data-ttu-id="5761d-139">Gruppo DH</span><span class="sxs-lookup"><span data-stu-id="5761d-139">DH Group</span></span>         | <span data-ttu-id="5761d-140">DHGroup24, ECP384, ECP256, DHGroup14, DHGroup2048, DHGroup2, DHGroup1, None</span><span class="sxs-lookup"><span data-stu-id="5761d-140">DHGroup24, ECP384, ECP256, DHGroup14, DHGroup2048, DHGroup2, DHGroup1, None</span></span> |
| <span data-ttu-id="5761d-141">Crittografia IPsec</span><span class="sxs-lookup"><span data-stu-id="5761d-141">IPsec Encryption</span></span> | <span data-ttu-id="5761d-142">GCMAES256, GCMAES192, GCMAES128, AES256, AES192, AES128, DES3, DES, None</span><span class="sxs-lookup"><span data-stu-id="5761d-142">GCMAES256, GCMAES192, GCMAES128, AES256, AES192, AES128, DES3, DES, None</span></span>    |
| <span data-ttu-id="5761d-143">Integrità IPsec</span><span class="sxs-lookup"><span data-stu-id="5761d-143">IPsec Integrity</span></span>  | <span data-ttu-id="5761d-144">GCMASE256, GCMAES192, GCMAES128, SHA256, SHA1, MD5</span><span class="sxs-lookup"><span data-stu-id="5761d-144">GCMASE256, GCMAES192, GCMAES128, SHA256, SHA1, MD5</span></span> |
| <span data-ttu-id="5761d-145">Gruppo PFS</span><span class="sxs-lookup"><span data-stu-id="5761d-145">PFS Group</span></span>        | <span data-ttu-id="5761d-146">PFS24, ECP384, ECP256, PFS2048, PFS2, PFS1, None</span><span class="sxs-lookup"><span data-stu-id="5761d-146">PFS24, ECP384, ECP256, PFS2048, PFS2, PFS1, None</span></span> 
| <span data-ttu-id="5761d-147">Durata associazione di sicurezza in modalità rapida</span><span class="sxs-lookup"><span data-stu-id="5761d-147">QM SA Lifetime</span></span>   | <span data-ttu-id="5761d-148">(**Facoltativo**: se non diversamente specificato, vengono usati i valori predefiniti)</span><span class="sxs-lookup"><span data-stu-id="5761d-148">(**Optional**: default values are used if not specified)</span></span><br><span data-ttu-id="5761d-149">Secondi (intero; **min. 300**/valore predefinito di 27000 secondi)</span><span class="sxs-lookup"><span data-stu-id="5761d-149">Seconds (integer; **min. 300**/default 27000 seconds)</span></span><br><span data-ttu-id="5761d-150">Kilobyte (intero; **min 1024**/valore predefinito di 102400000 KB)</span><span class="sxs-lookup"><span data-stu-id="5761d-150">KBytes (integer; **min. 1024**/default 102400000 KBytes)</span></span>   |
| <span data-ttu-id="5761d-151">Selettore di traffico</span><span class="sxs-lookup"><span data-stu-id="5761d-151">Traffic Selector</span></span> | <span data-ttu-id="5761d-152">UsePolicyBasedTrafficSelectors** ($True/$False; **Optional**, $False predefinito, se non diversamente specificato)</span><span class="sxs-lookup"><span data-stu-id="5761d-152">UsePolicyBasedTrafficSelectors** ($True/$False; **Optional**, default $False if not specified)</span></span>    |
|  |  |

> [!IMPORTANT]
> 1. <span data-ttu-id="5761d-153">**Se GCMAES viene usato per l'algoritmo di crittografia IPsec, è necessario selezionare hello stesso algoritmo GCMAES e lunghezza della chiave per l'integrità IPsec; ad esempio, l'uso di GCMAES128 per entrambe**</span><span class="sxs-lookup"><span data-stu-id="5761d-153">**If GCMAES is used as for IPsec Encryption algorithm, you must select hello same GCMAES algorithm and key length for IPsec Integrity; for example, using GCMAES128 for both**</span></span>
> 2. <span data-ttu-id="5761d-154">Durata SA modalità principale di IKEv2 è fissata a 28.800 secondi nei gateway VPN di Azure hello</span><span class="sxs-lookup"><span data-stu-id="5761d-154">IKEv2 Main Mode SA lifetime is fixed at 28,800 seconds on hello Azure VPN gateways</span></span>
> 3. <span data-ttu-id="5761d-155">L'impostazione "UsePolicyBasedTrafficSelectors" troppo$ True in una connessione configurerà hello Azure VPN gateway tooconnect toopolicy firewall basato su VPN in locale.</span><span class="sxs-lookup"><span data-stu-id="5761d-155">Setting "UsePolicyBasedTrafficSelectors" too$True on a connection will configure hello Azure VPN gateway tooconnect toopolicy-based VPN firewall on premises.</span></span> <span data-ttu-id="5761d-156">Se si abilita PolicyBasedTrafficSelectors, è necessario il dispositivo VPN è hello corrispondente selettori di traffico definiti con tutte le combinazioni del locale (gateway di rete locale) dei prefissi di rete da e verso i prefissi di rete virtuale di Azure, hello tooensure anziché any-a-qualsiasi.</span><span class="sxs-lookup"><span data-stu-id="5761d-156">If you enable PolicyBasedTrafficSelectors, you need tooensure your VPN device has hello matching traffic selectors defined with all combinations of your on-premises network (local network gateway) prefixes to/from hello Azure virtual network prefixes, instead of any-to-any.</span></span> <span data-ttu-id="5761d-157">Ad esempio, se i prefissi di rete locale sono 10.1.0.0/16 e 10.2.0.0/16 e i prefissi di rete virtuale sono 192.168.0.0/16 e 172.16.0.0/16, è necessario hello toospecify selettori di traffico seguenti:</span><span class="sxs-lookup"><span data-stu-id="5761d-157">For example, if your on-premises network prefixes are 10.1.0.0/16 and 10.2.0.0/16, and your virtual network prefixes are 192.168.0.0/16 and 172.16.0.0/16, you need toospecify hello following traffic selectors:</span></span>
>    * <span data-ttu-id="5761d-158">10.1.0.0/16 <====> 192.168.0.0/16</span><span class="sxs-lookup"><span data-stu-id="5761d-158">10.1.0.0/16 <====> 192.168.0.0/16</span></span>
>    * <span data-ttu-id="5761d-159">10.1.0.0/16 <====> 172.16.0.0/16</span><span class="sxs-lookup"><span data-stu-id="5761d-159">10.1.0.0/16 <====> 172.16.0.0/16</span></span>
>    * <span data-ttu-id="5761d-160">10.2.0.0/16 <====> 192.168.0.0/16</span><span class="sxs-lookup"><span data-stu-id="5761d-160">10.2.0.0/16 <====> 192.168.0.0/16</span></span>
>    * <span data-ttu-id="5761d-161">10.2.0.0/16 <====> 172.16.0.0/16</span><span class="sxs-lookup"><span data-stu-id="5761d-161">10.2.0.0/16 <====> 172.16.0.0/16</span></span>

<span data-ttu-id="5761d-162">Per altre informazioni sui selettori di traffico basati su criteri, vedere [Connettere più dispositivi VPN basati su criteri locali](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="5761d-162">For more information regarding policy-based traffic selectors, see [Connect multiple on-premises policy-based VPN devices](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span></span>

<span data-ttu-id="5761d-163">Nella seguente sono elencati nella tabella Hello hello corrispondente gruppi Diffie-Hellman supportato dai criteri personalizzati di hello:</span><span class="sxs-lookup"><span data-stu-id="5761d-163">hello following table lists hello corresponding Diffie-Hellman Groups supported by hello custom policy:</span></span>

| <span data-ttu-id="5761d-164">**Gruppo Diffie-Hellman**</span><span class="sxs-lookup"><span data-stu-id="5761d-164">**Diffie-Hellman Group**</span></span>  | <span data-ttu-id="5761d-165">**DHGroup**</span><span class="sxs-lookup"><span data-stu-id="5761d-165">**DHGroup**</span></span>              | <span data-ttu-id="5761d-166">**PFSGroup**</span><span class="sxs-lookup"><span data-stu-id="5761d-166">**PFSGroup**</span></span> | <span data-ttu-id="5761d-167">**Lunghezza chiave**</span><span class="sxs-lookup"><span data-stu-id="5761d-167">**Key length**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="5761d-168">1</span><span class="sxs-lookup"><span data-stu-id="5761d-168">1</span></span>                         | <span data-ttu-id="5761d-169">DHGroup1</span><span class="sxs-lookup"><span data-stu-id="5761d-169">DHGroup1</span></span>                 | <span data-ttu-id="5761d-170">PFS1</span><span class="sxs-lookup"><span data-stu-id="5761d-170">PFS1</span></span>         | <span data-ttu-id="5761d-171">MODP a 768 bit</span><span class="sxs-lookup"><span data-stu-id="5761d-171">768-bit MODP</span></span>   |
| <span data-ttu-id="5761d-172">2</span><span class="sxs-lookup"><span data-stu-id="5761d-172">2</span></span>                         | <span data-ttu-id="5761d-173">DHGroup2</span><span class="sxs-lookup"><span data-stu-id="5761d-173">DHGroup2</span></span>                 | <span data-ttu-id="5761d-174">PFS2</span><span class="sxs-lookup"><span data-stu-id="5761d-174">PFS2</span></span>         | <span data-ttu-id="5761d-175">MODP a 1024 bit</span><span class="sxs-lookup"><span data-stu-id="5761d-175">1024-bit MODP</span></span>  |
| <span data-ttu-id="5761d-176">14</span><span class="sxs-lookup"><span data-stu-id="5761d-176">14</span></span>                        | <span data-ttu-id="5761d-177">DHGroup14</span><span class="sxs-lookup"><span data-stu-id="5761d-177">DHGroup14</span></span><br><span data-ttu-id="5761d-178">DHGroup2048</span><span class="sxs-lookup"><span data-stu-id="5761d-178">DHGroup2048</span></span> | <span data-ttu-id="5761d-179">PFS2048</span><span class="sxs-lookup"><span data-stu-id="5761d-179">PFS2048</span></span>      | <span data-ttu-id="5761d-180">MODP a 2048 bit</span><span class="sxs-lookup"><span data-stu-id="5761d-180">2048-bit MODP</span></span>  |
| <span data-ttu-id="5761d-181">19</span><span class="sxs-lookup"><span data-stu-id="5761d-181">19</span></span>                        | <span data-ttu-id="5761d-182">ECP256</span><span class="sxs-lookup"><span data-stu-id="5761d-182">ECP256</span></span>                   | <span data-ttu-id="5761d-183">ECP256</span><span class="sxs-lookup"><span data-stu-id="5761d-183">ECP256</span></span>       | <span data-ttu-id="5761d-184">ECP a 256 bit</span><span class="sxs-lookup"><span data-stu-id="5761d-184">256-bit ECP</span></span>    |
| <span data-ttu-id="5761d-185">20</span><span class="sxs-lookup"><span data-stu-id="5761d-185">20</span></span>                        | <span data-ttu-id="5761d-186">ECP384</span><span class="sxs-lookup"><span data-stu-id="5761d-186">ECP384</span></span>                   | <span data-ttu-id="5761d-187">ECP284</span><span class="sxs-lookup"><span data-stu-id="5761d-187">ECP284</span></span>       | <span data-ttu-id="5761d-188">ECP a 384 bit</span><span class="sxs-lookup"><span data-stu-id="5761d-188">384-bit ECP</span></span>    |
| <span data-ttu-id="5761d-189">24</span><span class="sxs-lookup"><span data-stu-id="5761d-189">24</span></span>                        | <span data-ttu-id="5761d-190">DHGroup24</span><span class="sxs-lookup"><span data-stu-id="5761d-190">DHGroup24</span></span>                | <span data-ttu-id="5761d-191">PFS24</span><span class="sxs-lookup"><span data-stu-id="5761d-191">PFS24</span></span>        | <span data-ttu-id="5761d-192">MODP a 2048 bit</span><span class="sxs-lookup"><span data-stu-id="5761d-192">2048-bit MODP</span></span>  |

<span data-ttu-id="5761d-193">Fare riferimento troppo[RFC3526](https://tools.ietf.org/html/rfc3526) e [RFC5114](https://tools.ietf.org/html/rfc5114) per altri dettagli.</span><span class="sxs-lookup"><span data-stu-id="5761d-193">Refer too[RFC3526](https://tools.ietf.org/html/rfc3526) and [RFC5114](https://tools.ietf.org/html/rfc5114) for more details.</span></span>

## <span data-ttu-id="5761d-194"><a name ="crossprem"></a>Parte 3: Creare una nuova connessione VPN da sito a sito con criteri IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="5761d-194"><a name ="crossprem"></a>Part 3 - Create a new S2S VPN connection with IPsec/IKE policy</span></span>

<span data-ttu-id="5761d-195">In questa sezione vengono illustrati i passaggi hello di creazione di una connessione VPN S2S con un criterio IPsec/IKE.</span><span class="sxs-lookup"><span data-stu-id="5761d-195">This section walks you through hello steps of creating a S2S VPN connection with an IPsec/IKE policy.</span></span> <span data-ttu-id="5761d-196">Hello seguito crea hello connessione come illustrato nel diagramma hello:</span><span class="sxs-lookup"><span data-stu-id="5761d-196">hello following steps create hello connection as shown in hello diagram:</span></span>

![s2s-policy](./media/vpn-gateway-ipsecikepolicy-rm-powershell/s2spolicy.png)

<span data-ttu-id="5761d-198">Per altre istruzioni dettagliate per la creazione di una connessione VPN da sito a sito, vedere [Creare una connessione VPN da sito a sito](vpn-gateway-create-site-to-site-rm-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="5761d-198">See [Create a S2S VPN connection](vpn-gateway-create-site-to-site-rm-powershell.md) for more detailed step-by-step instructions for creating a S2S VPN connection.</span></span>

### <span data-ttu-id="5761d-199"><a name="before"></a>Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="5761d-199"><a name="before"></a>Before you begin</span></span>

* <span data-ttu-id="5761d-200">Verificare di possedere una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="5761d-200">Verify that you have an Azure subscription.</span></span> <span data-ttu-id="5761d-201">Se non si ha una sottoscrizione di Azure, è possibile attivare i [vantaggi per i sottoscrittori di MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) oppure iscriversi per ottenere un [account gratuito](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5761d-201">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="5761d-202">Installare i cmdlet di PowerShell di gestione risorse di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="5761d-202">Install hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="5761d-203">Vedere [Panoramica di Azure PowerShell](/powershell/azure/overview) per ulteriori informazioni sull'installazione dei cmdlet di PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="5761d-203">See [Overview of Azure PowerShell](/powershell/azure/overview) for more information about installing hello PowerShell cmdlets.</span></span>

### <span data-ttu-id="5761d-204"><a name="createvnet1"></a>Passaggio 1: creare una rete virtuale hello gateway VPN e gateway di rete locale</span><span class="sxs-lookup"><span data-stu-id="5761d-204"><a name="createvnet1"></a>Step 1 - Create hello virtual network, VPN gateway, and local network gateway</span></span>

#### <a name="1-declare-your-variables"></a><span data-ttu-id="5761d-205">1. Dichiarare le variabili</span><span class="sxs-lookup"><span data-stu-id="5761d-205">1. Declare your variables</span></span>

<span data-ttu-id="5761d-206">Per questo esercizio, si inizierà dichiarando le variabili.</span><span class="sxs-lookup"><span data-stu-id="5761d-206">For this exercise, we start by declaring our variables.</span></span> <span data-ttu-id="5761d-207">Essere certi tooreplace hello i valori con valori personalizzati durante la configurazione per la produzione.</span><span class="sxs-lookup"><span data-stu-id="5761d-207">Be sure tooreplace hello values with your own when configuring for production.</span></span>

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

#### <a name="2-connect-tooyour-subscription-and-create-a-new-resource-group"></a><span data-ttu-id="5761d-208">2. Connettere tooyour sottoscrizione e creare un nuovo gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="5761d-208">2. Connect tooyour subscription and create a new resource group</span></span>

<span data-ttu-id="5761d-209">Accertarsi di passare hello toouse di modalità tooPowerShell cmdlet di gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="5761d-209">Make sure you switch tooPowerShell mode toouse hello Resource Manager cmdlets.</span></span> <span data-ttu-id="5761d-210">Per altre informazioni, vedere [Uso di Windows PowerShell con Gestione risorse](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="5761d-210">For more information, see [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="5761d-211">Aprire la console di PowerShell e tooyour account di connessione.</span><span class="sxs-lookup"><span data-stu-id="5761d-211">Open your PowerShell console and connect tooyour account.</span></span> <span data-ttu-id="5761d-212">Utilizzare hello toohelp esempio che ci si connette seguenti:</span><span class="sxs-lookup"><span data-stu-id="5761d-212">Use hello following sample toohelp you connect:</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="3-create-hello-virtual-network-vpn-gateway-and-local-network-gateway"></a><span data-ttu-id="5761d-213">3. Creare la rete virtuale hello, gateway VPN e gateway di rete locale</span><span class="sxs-lookup"><span data-stu-id="5761d-213">3. Create hello virtual network, VPN gateway, and local network gateway</span></span>

<span data-ttu-id="5761d-214">Hello seguente esempio crea rete virtuale di hello, TestVNet1, con tre subnet e il gateway VPN hello.</span><span class="sxs-lookup"><span data-stu-id="5761d-214">hello following sample creates hello virtual network, TestVNet1, with three subnets, and hello VPN gateway.</span></span> <span data-ttu-id="5761d-215">Quando si sostituiscono i valori, è importante che la subnet gateway venga denominata sempre esattamente GatewaySubnet.</span><span class="sxs-lookup"><span data-stu-id="5761d-215">When substituting values, it's important that you always name your gateway subnet specifically GatewaySubnet.</span></span> <span data-ttu-id="5761d-216">Se si assegnano altri nomi, la creazione del gateway ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="5761d-216">If you name it something else, your gateway creation fails.</span></span>

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

### <span data-ttu-id="5761d-217"><a name="s2sconnection"></a>Passaggio 2: Creare una connessione VPN da sito a sito con un criterio IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="5761d-217"><a name="s2sconnection"></a>Step 2 - Create a S2S VPN connection with an IPsec/IKE policy</span></span>

#### <a name="1-create-an-ipsecike-policy"></a><span data-ttu-id="5761d-218">1. Creare un criterio IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="5761d-218">1. Create an IPsec/IKE policy</span></span>

<span data-ttu-id="5761d-219">Hello lo script di esempio seguente crea un criterio IPsec/IKE con hello seguenti algoritmi e parametri:</span><span class="sxs-lookup"><span data-stu-id="5761d-219">hello following sample script creates an IPsec/IKE policy with hello following algorithms and parameters:</span></span>

* <span data-ttu-id="5761d-220">IKEv2: AES256, SHA384, DHGroup24</span><span class="sxs-lookup"><span data-stu-id="5761d-220">IKEv2: AES256, SHA384, DHGroup24</span></span>
* <span data-ttu-id="5761d-221">IPsec: AES256, SHA256, PFS24, durata dell'associazione di sicurezza 7200 secondi e 2048 KB</span><span class="sxs-lookup"><span data-stu-id="5761d-221">IPsec: AES256, SHA256, PFS24, SA Lifetime 7200 seconds & 2048KB</span></span>

```powershell
$ipsecpolicy6 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption AES256 -IpsecIntegrity SHA256 -PfsGroup PFS24 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 2048
```

<span data-ttu-id="5761d-222">Se si utilizza GCMAES per IPsec, è necessario utilizzare hello stesso algoritmo GCMAES e lunghezza della chiave per la crittografia di IPsec e integrità, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="5761d-222">If you use GCMAES for IPsec, you must use hello same GCMAES algorithm and key length for both IPsec encryption and integrity, for example:</span></span>

* <span data-ttu-id="5761d-223">IKEv2: AES256, SHA384, DHGroup24</span><span class="sxs-lookup"><span data-stu-id="5761d-223">IKEv2: AES256, SHA384, DHGroup24</span></span>
* <span data-ttu-id="5761d-224">IPsec: **GCMAES256, GCMAES256**, PFS24, durata dell'associazione di sicurezza 7200 secondi e 2048 KB</span><span class="sxs-lookup"><span data-stu-id="5761d-224">IPsec: **GCMAES256, GCMAES256**, PFS24, SA Lifetime 7200 seconds & 2048KB</span></span>

```powershell
$ipsecpolicy6 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption GCMAES256 -IpsecIntegrity GCMAES256 -PfsGroup PFS24 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 2048
```

#### <a name="2-create-hello-s2s-vpn-connection-with-hello-ipsecike-policy"></a><span data-ttu-id="5761d-225">2. Creare una connessione VPN S2S hello con hello criteri IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="5761d-225">2. Create hello S2S VPN connection with hello IPsec/IKE policy</span></span>

<span data-ttu-id="5761d-226">Creare una connessione VPN S2S e applicare i criteri IPsec/IKE hello creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="5761d-226">Create an S2S VPN connection and apply hello IPsec/IKE policy created earlier.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng6 = Get-AzureRmLocalNetworkGateway  -Name $LNGName6 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng6 -Location $Location1 -ConnectionType IPsec -IpsecPolicies $ipsecpolicy6 -SharedKey 'AzureA1b2C3'
```

<span data-ttu-id="5761d-227">È possibile aggiungere facoltativamente "-UsePolicyBasedTrafficSelectors $True" toohello creare connessione cmdlet tooenable Azure VPN gateway tooconnect toopolicy dispositivi basati su VPN in locale, come descritto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="5761d-227">You can optionally add "-UsePolicyBasedTrafficSelectors $True" toohello create connection cmdlet tooenable Azure VPN gateway tooconnect toopolicy-based VPN devices on premises, as described above.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5761d-228">Una volta specificato una connessione di un criterio IPsec/IKE, gateway VPN di Azure hello solo invierà o accettare hello IPsec/IKE proposta con gli algoritmi di crittografia specificati e per i livelli di chiave in tale particolare connessione.</span><span class="sxs-lookup"><span data-stu-id="5761d-228">Once an IPsec/IKE policy is specified on a connection, hello Azure VPN gateway will only send or accept hello IPsec/IKE proposal with specified cryptographic algorithms and key strengths on that particular connection.</span></span> <span data-ttu-id="5761d-229">Assicurarsi che il dispositivo VPN locale per la connessione hello utilizza o accetta combinazione esatta criteri hello, in caso contrario non stabilisce tunnel VPN S2S hello.</span><span class="sxs-lookup"><span data-stu-id="5761d-229">Make sure your on-premises VPN device for hello connection uses or accepts hello exact policy combination, otherwise hello S2S VPN tunnel will not establish.</span></span>


## <span data-ttu-id="5761d-230"><a name ="vnet2vnet"></a>Parte 4: Creare una nuova connessione da rete virtuale a rete virtuale con criteri IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="5761d-230"><a name ="vnet2vnet"></a>Part 4 - Create a new VNet-to-VNet connection with IPsec/IKE policy</span></span>

<span data-ttu-id="5761d-231">passaggi di Hello di creazione di una connessione di rete virtuale a con un criterio IPsec/IKE sono simili toothat di una connessione VPN S2S.</span><span class="sxs-lookup"><span data-stu-id="5761d-231">hello steps of creating a VNet-to-VNet connection with an IPsec/IKE policy are similar toothat of a S2S VPN connection.</span></span> <span data-ttu-id="5761d-232">Hello seguente script di esempio creare hello connessione come illustrato nel diagramma hello:</span><span class="sxs-lookup"><span data-stu-id="5761d-232">hello following sample scripts create hello connection as shown in hello diagram:</span></span>

![v2v-policy](./media/vpn-gateway-ipsecikepolicy-rm-powershell/v2vpolicy.png)

<span data-ttu-id="5761d-234">Per la procedura dettagliata di creazione di una connessione da rete virtuale a rete virtuale, vedere [Creare una connessione tra reti virtuali](vpn-gateway-vnet-vnet-rm-ps.md) .</span><span class="sxs-lookup"><span data-stu-id="5761d-234">See [Create a VNet-to-VNet connection](vpn-gateway-vnet-vnet-rm-ps.md) for more detailed steps for creating a VNet-to-VNet connection.</span></span> <span data-ttu-id="5761d-235">È necessario completare [parte 3](#crossprem) toocreate e configurare TestVNet1 e hello Gateway VPN.</span><span class="sxs-lookup"><span data-stu-id="5761d-235">You must complete [Part 3](#crossprem) toocreate and configure TestVNet1 and hello VPN Gateway.</span></span>

### <span data-ttu-id="5761d-236"><a name="createvnet2"></a>Passaggio 1: creare una seconda rete virtuale hello e gateway VPN</span><span class="sxs-lookup"><span data-stu-id="5761d-236"><a name="createvnet2"></a>Step 1 - Create hello second virtual network and VPN gateway</span></span>

#### <a name="1-declare-your-variables"></a><span data-ttu-id="5761d-237">1. Dichiarare le variabili</span><span class="sxs-lookup"><span data-stu-id="5761d-237">1. Declare your variables</span></span>

<span data-ttu-id="5761d-238">Essere tooreplace che i valori hello con hello quelli che si desidera toouse per la configurazione.</span><span class="sxs-lookup"><span data-stu-id="5761d-238">Be sure tooreplace hello values with hello ones that you want toouse for your configuration.</span></span>

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

#### <a name="2-create-hello-second-virtual-network-and-vpn-gateway-in-hello-new-resource-group"></a><span data-ttu-id="5761d-239">2. Creare seconda rete virtuale hello e gateway VPN nel nuovo gruppo di risorse hello</span><span class="sxs-lookup"><span data-stu-id="5761d-239">2. Create hello second virtual network and VPN gateway in hello new resource group</span></span>

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

### <a name="step-2---create-a-vnet-tovnet-connection-with-hello-ipsecike-policy"></a><span data-ttu-id="5761d-240">Passaggio 2: creare una connessione di rete virtuale toVNet con hello criteri IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="5761d-240">Step 2 - Create a VNet-toVNet connection with hello IPsec/IKE policy</span></span>

<span data-ttu-id="5761d-241">Toohello simile connessione VPN S2S, creare un criterio IPsec/IKE, applicare toopolicy toohello nuova connessione.</span><span class="sxs-lookup"><span data-stu-id="5761d-241">Similar toohello S2S VPN connection, create an IPsec/IKE policy then apply toopolicy toohello new connection.</span></span>

#### <a name="1-create-an-ipsecike-policy"></a><span data-ttu-id="5761d-242">1. Creare un criterio IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="5761d-242">1. Create an IPsec/IKE policy</span></span>

<span data-ttu-id="5761d-243">Hello lo script di esempio seguente crea un criterio IPsec/IKE diverso con hello seguenti algoritmi e parametri:</span><span class="sxs-lookup"><span data-stu-id="5761d-243">hello following sample script creates a different IPsec/IKE policy with hello following algorithms and parameters:</span></span>
* <span data-ttu-id="5761d-244">IKEv2: AES128, SHA1, DHGroup14</span><span class="sxs-lookup"><span data-stu-id="5761d-244">IKEv2: AES128, SHA1, DHGroup14</span></span>
* <span data-ttu-id="5761d-245">IPsec: GCMAES128, GCMAES128, PFS14, durata dell'associazione di sicurezza 7200 secondi e 4096 KB</span><span class="sxs-lookup"><span data-stu-id="5761d-245">IPsec: GCMAES128, GCMAES128, PFS14, SA Lifetime 7200 seconds & 4096KB</span></span>

```powershell
$ipsecpolicy2 = New-AzureRmIpsecPolicy -IkeEncryption AES128 -IkeIntegrity SHA1 -DhGroup DHGroup14 -IpsecEncryption GCMAES128 -IpsecIntegrity GCMAES128 -PfsGroup PFS14 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 4096
```

#### <a name="2-create-vnet-to-vnet-connections-with-hello-ipsecike-policy"></a><span data-ttu-id="5761d-246">2. Creare connessioni di rete virtuale a con hello criteri IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="5761d-246">2. Create VNet-to-VNet connections with hello IPsec/IKE policy</span></span>

<span data-ttu-id="5761d-247">Creare una connessione di rete e applicare criteri IPsec/IKE hello creati.</span><span class="sxs-lookup"><span data-stu-id="5761d-247">Create a VNet-to-VNet connection and apply hello IPsec/IKE policy you created.</span></span> <span data-ttu-id="5761d-248">In questo esempio, entrambi i gateway sono in hello stessa sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="5761d-248">In this example, both gateways are in hello same subscription.</span></span> <span data-ttu-id="5761d-249">È possibile toocreate e configurare entrambe le connessioni con hello stesso criterio IPsec/IKE in hello stessa sessione di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5761d-249">So it is possible toocreate and configure both connections with hello same IPsec/IKE policy in hello same PowerShell session.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$vnet2gw = Get-AzureRmVirtualNetworkGateway -Name $GWName2  -ResourceGroupName $RG2

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection12 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet2gw -Location $Location1 -ConnectionType Vnet2Vnet -IpsecPolicies $ipsecpolicy2 -SharedKey 'AzureA1b2C3'

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection21 -ResourceGroupName $RG2 -VirtualNetworkGateway1 $vnet2gw -VirtualNetworkGateway2 $vnet1gw -Location $Location2 -ConnectionType Vnet2Vnet -IpsecPolicies $ipsecpolicy2 -SharedKey 'AzureA1b2C3'
```

> [!IMPORTANT]
> <span data-ttu-id="5761d-250">Una volta specificato una connessione di un criterio IPsec/IKE, gateway VPN di Azure hello solo invierà o accettare hello IPsec/IKE proposta con gli algoritmi di crittografia specificati e per i livelli di chiave in tale particolare connessione.</span><span class="sxs-lookup"><span data-stu-id="5761d-250">Once an IPsec/IKE policy is specified on a connection, hello Azure VPN gateway will only send or accept hello IPsec/IKE proposal with specified cryptographic algorithms and key strengths on that particular connection.</span></span> <span data-ttu-id="5761d-251">Verificare che hello criteri IPsec per entrambe le connessioni sono hello stesso, in caso contrario non stabilisce la connessione di rete virtuale a.</span><span class="sxs-lookup"><span data-stu-id="5761d-251">Make sure hello IPsec policies for both connections are hello same, otherwise the VNet-to-VNet connection will not establish.</span></span>

<span data-ttu-id="5761d-252">Dopo aver completato questi passaggi, hello connessione tra qualche minuto e sarà necessario dopo la topologia della rete, come illustrato in inizio hello hello:</span><span class="sxs-lookup"><span data-stu-id="5761d-252">After completing these steps, hello connection is established in a few minutes, and you will have hello following network topology as shown in hello beginning:</span></span>

![ipsec-ike-policy](./media/vpn-gateway-ipsecikepolicy-rm-powershell/ipsecikepolicy.png)


## <span data-ttu-id="5761d-254"><a name ="managepolicy"></a>Parte 5: Aggiornare i criteri IPsec/IKE per una connessione</span><span class="sxs-lookup"><span data-stu-id="5761d-254"><a name ="managepolicy"></a>Part 5 - Update IPsec/IKE policy for a connection</span></span>

<span data-ttu-id="5761d-255">ultima sezione Hello illustra come toomanage criteri IPsec/IKE per una connessione esistente S2S o di rete virtuale a.</span><span class="sxs-lookup"><span data-stu-id="5761d-255">hello last section shows you how toomanage IPsec/IKE policy for an existing S2S or VNet-to-VNet connection.</span></span> <span data-ttu-id="5761d-256">esercizio Hello riportato di seguito illustra hello dopo le operazioni su una connessione:</span><span class="sxs-lookup"><span data-stu-id="5761d-256">hello exercise below walks you through hello following operations on a connection:</span></span>

1. <span data-ttu-id="5761d-257">Mostra i criteri IPsec/IKE hello di una connessione</span><span class="sxs-lookup"><span data-stu-id="5761d-257">Show hello IPsec/IKE policy of a connection</span></span>
2. <span data-ttu-id="5761d-258">Aggiungere o aggiornare la connessione di tooa criteri IPsec/IKE hello</span><span class="sxs-lookup"><span data-stu-id="5761d-258">Add or update hello IPsec/IKE policy tooa connection</span></span>
3. <span data-ttu-id="5761d-259">Rimuovere i criteri IPsec/IKE hello da una connessione</span><span class="sxs-lookup"><span data-stu-id="5761d-259">Remove hello IPsec/IKE policy from a connection</span></span>

<span data-ttu-id="5761d-260">Hello stessi passaggi si applicano tooboth S2S e le connessioni di rete virtuale a.</span><span class="sxs-lookup"><span data-stu-id="5761d-260">hello same steps apply tooboth S2S and VNet-to-VNet connections.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5761d-261">Il criterio IPsec/IKE è supportato solo nei gateway VPN *Standard* e *Prestazioni elevate* basati su route di Azure.</span><span class="sxs-lookup"><span data-stu-id="5761d-261">IPsec/IKE policy is supported on *Standard* and *HighPerformance* route-based VPN gateways only.</span></span> <span data-ttu-id="5761d-262">Non funziona su gateway Basic hello SKU o gateway VPN basata su criteri di hello.</span><span class="sxs-lookup"><span data-stu-id="5761d-262">It does not work on hello Basic gateway SKU or hello policy-based VPN gateway.</span></span>

#### <a name="1-show-hello-ipsecike-policy-of-a-connection"></a><span data-ttu-id="5761d-263">1. Mostra i criteri IPsec/IKE hello di una connessione</span><span class="sxs-lookup"><span data-stu-id="5761d-263">1. Show hello IPsec/IKE policy of a connection</span></span>

<span data-ttu-id="5761d-264">Hello di esempio seguente viene illustrato come tooget hello criteri IPsec/IKE configurato su una connessione.</span><span class="sxs-lookup"><span data-stu-id="5761d-264">hello following example shows how tooget hello IPsec/IKE policy configured on a connection.</span></span> <span data-ttu-id="5761d-265">gli script di Hello continuano anche da esercizi hello precedenti.</span><span class="sxs-lookup"><span data-stu-id="5761d-265">hello scripts also continue from hello exercises above.</span></span>

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1
$connection6.IpsecPolicies
```

<span data-ttu-id="5761d-266">ultimo comando Hello sono elencati i criteri IPsec/IKE correnti hello configurato nella connessione hello, se è presente uno.</span><span class="sxs-lookup"><span data-stu-id="5761d-266">hello last command lists hello current IPsec/IKE policy configured on hello connection, if there is any.</span></span> <span data-ttu-id="5761d-267">Hello output di esempio seguente è per la connessione hello:</span><span class="sxs-lookup"><span data-stu-id="5761d-267">hello following sample output is for hello connection:</span></span>

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

<span data-ttu-id="5761d-268">Se non è configurato alcun criterio IPsec/IKE, hello comando (PS > $connection6.policy) Ottiene un oggetto vuoto restituito.</span><span class="sxs-lookup"><span data-stu-id="5761d-268">If there is no IPsec/IKE policy configured, hello command (PS> $connection6.policy) gets an empty return.</span></span> <span data-ttu-id="5761d-269">Ciò significa IPsec/IKE non è configurato nella connessione di hello, ma che non vi sia alcun criterio IPsec/IKE personalizzato.</span><span class="sxs-lookup"><span data-stu-id="5761d-269">It does not mean IPsec/IKE is not configured on hello connection, but that there is no custom IPsec/IKE policy.</span></span> <span data-ttu-id="5761d-270">connessione effettiva Hello utilizza criteri predefiniti hello negoziato tra il dispositivo VPN locale e hello gateway VPN di Azure.</span><span class="sxs-lookup"><span data-stu-id="5761d-270">hello actual connection uses hello default policy negotiated between your on-premises VPN device and hello Azure VPN gateway.</span></span>

#### <a name="2-add-or-update-an-ipsecike-policy-for-a-connection"></a><span data-ttu-id="5761d-271">2. Aggiungere o aggiornare un criterio IPsec/IKE per una connessione</span><span class="sxs-lookup"><span data-stu-id="5761d-271">2. Add or update an IPsec/IKE policy for a connection</span></span>

<span data-ttu-id="5761d-272">Hello passaggi tooadd un nuovo criterio o aggiornamento di un criterio esistente in una connessione sono hello stesso: creare un nuovo criterio, quindi applicare una nuova connessione di toohello criteri hello.</span><span class="sxs-lookup"><span data-stu-id="5761d-272">hello steps tooadd a new policy or update an existing policy on a connection are hello same: create a new policy then apply hello new policy toohello connection.</span></span>

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

$newpolicy6   = New-AzureRmIpsecPolicy -IkeEncryption AES128 -IkeIntegrity SHA1 -DhGroup DHGroup14 -IpsecEncryption GCMAES128 -IpsecIntegrity GCMAES128 -PfsGroup None -SALifeTimeSeconds 3600 -SADataSizeKilobytes 2048

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -IpsecPolicies $newpolicy6
```

<span data-ttu-id="5761d-273">tooenable "UsePolicyBasedTrafficSelectors" quando la connessione tooan locale dispositivo VPN basata su criteri, aggiungere hello "-UsePolicyBaseTrafficSelectors" parametro toohello cmdlet o impostarlo troppo opzione hello di $ toodisable False:</span><span class="sxs-lookup"><span data-stu-id="5761d-273">tooenable "UsePolicyBasedTrafficSelectors" when connecting tooan on-premises policy-based VPN device, add hello "-UsePolicyBaseTrafficSelectors" parameter toohello cmdlet, or set it too$False toodisable hello option:</span></span>

```powershell
Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -IpsecPolicies $newpolicy6 -UsePolicyBasedTrafficSelectors $True
```

<span data-ttu-id="5761d-274">È possibile ottenere la connessione hello nuovamente toocheck se hello criteri vengono aggiornati.</span><span class="sxs-lookup"><span data-stu-id="5761d-274">You can get hello connection again toocheck if hello policy is updated.</span></span>

```powershell
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1
$connection6.IpsecPolicies
```

<span data-ttu-id="5761d-275">Verrà visualizzato l'output di hello dall'ultima riga hello, come illustrato nell'esempio seguente hello:</span><span class="sxs-lookup"><span data-stu-id="5761d-275">You should see hello output from hello last line, as shown in hello following example:</span></span>

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

#### <a name="3-remove-an-ipsecike-policy-from-a-connection"></a><span data-ttu-id="5761d-276">3. Rimuovere un criterio IPsec/IKE da una connessione</span><span class="sxs-lookup"><span data-stu-id="5761d-276">3. Remove an IPsec/IKE policy from a connection</span></span>

<span data-ttu-id="5761d-277">Dopo aver rimosso i criteri personalizzati di hello da una connessione, gateway VPN di Azure hello torna indietro toohello [elenco predefinito delle proposte di IPsec/IKE](vpn-gateway-about-vpn-devices.md) e nuovamente negozia con il dispositivo VPN locale.</span><span class="sxs-lookup"><span data-stu-id="5761d-277">Once you remove hello custom policy from a connection, hello Azure VPN gateway reverts back toohello [default list of IPsec/IKE proposals](vpn-gateway-about-vpn-devices.md) and renegotiates again with your on-premises VPN device.</span></span>

```powershell
$RG1           = "TestPolicyRG1"
$Connection16  = "VNet1toSite6"
$connection6   = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

$currentpolicy = $connection6.IpsecPolicies[0]
$connection6.IpsecPolicies.Remove($currentpolicy)

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6
```

<span data-ttu-id="5761d-278">È possibile utilizzare hello toocheck script stesso, se il criterio di hello è stato rimosso dalla connessione hello.</span><span class="sxs-lookup"><span data-stu-id="5761d-278">You can use hello same script toocheck if hello policy has been removed from hello connection.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5761d-279">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5761d-279">Next steps</span></span>

<span data-ttu-id="5761d-280">Per altri dettagli sui selettori di traffico basati su criteri, vedere l'articolo su come [connettere più dispositivi VPN basati su criteri locali](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="5761d-280">See [Connect multiple on-premises policy-based VPN devices](vpn-gateway-connect-multiple-policybased-rm-ps.md) for more details regarding policy-based traffic selectors.</span></span>

<span data-ttu-id="5761d-281">Una volta completata la connessione, è possibile aggiungere macchine virtuali tooyour le reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="5761d-281">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="5761d-282">Per i passaggi, vedere [Creare la prima macchina virtuale](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) .</span><span class="sxs-lookup"><span data-stu-id="5761d-282">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>
