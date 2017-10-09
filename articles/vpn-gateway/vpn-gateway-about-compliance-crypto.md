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
# <a name="about-cryptographic-requirements-and-azure-vpn-gateways"></a><span data-ttu-id="009cf-103">Informazioni sui requisiti di crittografia e i gateway VPN di Azure</span><span class="sxs-lookup"><span data-stu-id="009cf-103">About cryptographic requirements and Azure VPN gateways</span></span>

<span data-ttu-id="009cf-104">In questo articolo viene descritto come configurare toosatisfy gateway VPN di Azure i requisiti di crittografia per i tunnel VPN S2S cross-premise e connessioni di rete virtuale all'interno di Azure.</span><span class="sxs-lookup"><span data-stu-id="009cf-104">This article discusses how you can configure Azure VPN gateways toosatisfy your cryptographic requirements for both cross-premises S2S VPN tunnels and VNet-to-VNet connections within Azure.</span></span> 

## <a name="about-ipsec-and-ike-policy-parameters-for-azure-vpn-gateways"></a><span data-ttu-id="009cf-105">Informazioni sui parametri di criteri IPsec e IKE per gateway VPN di Azure</span><span class="sxs-lookup"><span data-stu-id="009cf-105">About IPsec and IKE policy parameters for Azure VPN gateways</span></span>
<span data-ttu-id="009cf-106">Lo standard di protocollo IPsec e IKE supporta un'ampia gamma di algoritmi di crittografia in varie combinazioni.</span><span class="sxs-lookup"><span data-stu-id="009cf-106">IPsec and IKE protocol standard supports a wide range of cryptographic algorithms in various combinations.</span></span> <span data-ttu-id="009cf-107">Se i clienti non richiedono una combinazione specifica di algoritmi e parametri per la crittografia, i gateway VPN di Azure usano un set di proposte predefinite.</span><span class="sxs-lookup"><span data-stu-id="009cf-107">If customers do not request a specific combination of cryptographic algorithms and parameters, Azure VPN gateways use a set of default proposals.</span></span> <span data-ttu-id="009cf-108">set di criteri predefiniti Hello sono state scelte toomaximize interoperabilità con un'ampia gamma di dispositivi VPN di terze parti in configurazioni predefinite.</span><span class="sxs-lookup"><span data-stu-id="009cf-108">hello default policy sets were chosen toomaximize interoperability with a wide range of third-party VPN devices in default configurations.</span></span> <span data-ttu-id="009cf-109">Di conseguenza, i criteri di hello e numero di hello delle proposte non può coprire tutte le possibili combinazioni di algoritmi di crittografia disponibili e i punti di forza di chiave.</span><span class="sxs-lookup"><span data-stu-id="009cf-109">As a result, hello policies and hello number of proposals cannot cover all possible combinations of available cryptographic algorithms and key strengths.</span></span>

<span data-ttu-id="009cf-110">criterio predefinito impostato per il gateway VPN di Azure è elencato nel documento hello Hello: [informazioni sui dispositivi VPN e i parametri IPsec/IKE per le connessioni Site-to-Site VPN Gateway](vpn-gateway-about-vpn-devices.md).</span><span class="sxs-lookup"><span data-stu-id="009cf-110">hello default policy set for Azure VPN gateway is listed in hello document: [About VPN devices and IPsec/IKE parameters for Site-to-Site VPN Gateway connections](vpn-gateway-about-vpn-devices.md).</span></span>

## <a name="cryptographic-requirements"></a><span data-ttu-id="009cf-111">Requisiti per la crittografia</span><span class="sxs-lookup"><span data-stu-id="009cf-111">Cryptographic requirements</span></span>
<span data-ttu-id="009cf-112">Per le comunicazioni che richiedono gli algoritmi di crittografia specifici o parametri, in genere a causa di requisiti di sicurezza o toocompliance, i clienti ora possono configurare i toouse gateway VPN di Azure criteri IPsec/IKE personalizzati con crittografia specifico gli algoritmi e vantaggi chiave, piuttosto che set di criteri di hello predefinito di Azure.</span><span class="sxs-lookup"><span data-stu-id="009cf-112">For communications that require specific cryptographic algorithms or parameters, typically due toocompliance or security requirements, customers can now configure their Azure VPN gateways toouse a custom IPsec/IKE policy with specific cryptographic algorithms and key strengths, rather than hello Azure default policy sets.</span></span>

<span data-ttu-id="009cf-113">Ad esempio, i criteri di hello IKEv2 in modalità principale per i gateway VPN di Azure utilizzano solo il gruppo Diffie-Hellman di 2 (1024 bit), mentre i clienti potrebbe essere necessario toospecify più forte toobe gruppi utilizzati in IKE, ad esempio gruppo 14 (2048 bit), gruppo 24 (gruppo MODP 2048 bit) o ECP (elliptic curva di gruppi) 384 o 256 bit (gruppo rispettivamente 19 e 20 gruppo).</span><span class="sxs-lookup"><span data-stu-id="009cf-113">For example, hello IKEv2 main mode policies for Azure VPN gateways utilize only Diffie-Hellman Group 2 (1024 bits), whereas customers may need toospecify stronger groups toobe used in IKE, such as Group 14 (2048-bit), Group 24 (2048-bit MODP Group), or ECP (elliptic curve groups) 256 or 384 bit (Group 19 and Group 20, respectively).</span></span> <span data-ttu-id="009cf-114">Requisiti simili si applicano anche i criteri di modalità rapida tooIPsec.</span><span class="sxs-lookup"><span data-stu-id="009cf-114">Similar requirements apply tooIPsec quick mode policies as well.</span></span>

## <a name="custom-ipsecike-policy-with-azure-vpn-gateways"></a><span data-ttu-id="009cf-115">Criteri IPsec/IKE personalizzati con i gateway VPN di Azure</span><span class="sxs-lookup"><span data-stu-id="009cf-115">Custom IPsec/IKE policy with Azure VPN gateways</span></span>
<span data-ttu-id="009cf-116">I gateway VPN di Azure ora supportano i criteri IPsec/IKE personalizzati per connessione.</span><span class="sxs-lookup"><span data-stu-id="009cf-116">Azure VPN gateways now support per-connection, custom IPsec/IKE policy.</span></span> <span data-ttu-id="009cf-117">Per un sito a sito o da rete connessione, è possibile scegliere una combinazione specifica di algoritmi di crittografia per IPsec e IKE con attendibilità della chiave hello desiderato, come illustrato nell'esempio seguente hello:</span><span class="sxs-lookup"><span data-stu-id="009cf-117">For a Site-to-Site or VNet-to-VNet connection, you can choose a specific combination of cryptographic algorithms for IPsec and IKE with hello desired key strength, as shown in hello following example:</span></span>

![ipsec-ike-policy](./media/vpn-gateway-about-compliance-crypto/ipsecikepolicy.png)

<span data-ttu-id="009cf-119">È possibile creare un criterio IPsec/IKE e applicare una connessione nuova o esistente tooa.</span><span class="sxs-lookup"><span data-stu-id="009cf-119">You can create an IPsec/IKE policy and apply tooa new or existing connection.</span></span> 

### <a name="workflow"></a><span data-ttu-id="009cf-120">Flusso di lavoro</span><span class="sxs-lookup"><span data-stu-id="009cf-120">Workflow</span></span>

1. <span data-ttu-id="009cf-121">Creare reti virtuali hello, gateway VPN o gateway di rete locale per la topologia di connettività, come descritto in altre come-toodocuments</span><span class="sxs-lookup"><span data-stu-id="009cf-121">Create hello virtual networks, VPN gateways, or local network gateways for your connectivity topology as described in other how-toodocuments</span></span>
2. <span data-ttu-id="009cf-122">Creare un criterio IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="009cf-122">Create an IPsec/IKE policy</span></span>
3. <span data-ttu-id="009cf-123">È possibile applicare criteri hello quando si crea una connessione S2S o di rete virtuale a</span><span class="sxs-lookup"><span data-stu-id="009cf-123">You can apply hello policy when you create a S2S or VNet-to-VNet connection</span></span>
4. <span data-ttu-id="009cf-124">Se la connessione hello è già stata creata, è possibile applicare o aggiornare la connessione esistente hello criteri tooan</span><span class="sxs-lookup"><span data-stu-id="009cf-124">If hello connection is already created, you can apply or update hello policy tooan existing connection</span></span>


## <a name="ipsecike-policy-faq"></a><span data-ttu-id="009cf-125">Domande frequenti sui criteri IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="009cf-125">IPsec/IKE policy FAQ</span></span>

[!INCLUDE [vpn-gateway-ipsecikepolicy-faq-include](../../includes/vpn-gateway-ipsecikepolicy-faq-include.md)]


## <a name="next-steps"></a><span data-ttu-id="009cf-126">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="009cf-126">Next steps</span></span>
<span data-ttu-id="009cf-127">Vedere [Configurare i criteri IPsec/IKE](vpn-gateway-ipsecikepolicy-rm-powershell.md) per istruzioni dettagliate sulla configurazione dei criteri IPsec/IKE personalizzato su una connessione.</span><span class="sxs-lookup"><span data-stu-id="009cf-127">See [Configure IPsec/IKE policy](vpn-gateway-ipsecikepolicy-rm-powershell.md) for step-by-step instructions on configuring custom IPsec/IKE policy on a connection.</span></span>

<span data-ttu-id="009cf-128">Vedere anche [connettersi più dispositivi VPN basata su criteri](vpn-gateway-connect-multiple-policybased-rm-ps.md) toolearn ulteriori informazioni sull'opzione UsePolicyBasedTrafficSelectors hello.</span><span class="sxs-lookup"><span data-stu-id="009cf-128">See also [Connect multiple policy-based VPN devices](vpn-gateway-connect-multiple-policybased-rm-ps.md) toolearn more about hello UsePolicyBasedTrafficSelectors option.</span></span>
