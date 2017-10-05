---
title: Informazioni sui requisiti di crittografia e i gateway VPN di Azure | Microsoft Docs
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
ms.openlocfilehash: c789e6c278fc0c58c64f5d96e57f94aee5a6cefc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="about-cryptographic-requirements-and-azure-vpn-gateways"></a><span data-ttu-id="a6cc7-103">Informazioni sui requisiti di crittografia e i gateway VPN di Azure</span><span class="sxs-lookup"><span data-stu-id="a6cc7-103">About cryptographic requirements and Azure VPN gateways</span></span>

<span data-ttu-id="a6cc7-104">Questo articolo illustra come configurare i gateway VPN di Azure per soddisfare i requisiti di crittografia per i tunnel VPN S2S cross-premise e le connessioni da rete virtuale a rete virtuale all'interno di Azure.</span><span class="sxs-lookup"><span data-stu-id="a6cc7-104">This article discusses how you can configure Azure VPN gateways to satisfy your cryptographic requirements for both cross-premises S2S VPN tunnels and VNet-to-VNet connections within Azure.</span></span> 

## <a name="about-ipsec-and-ike-policy-parameters-for-azure-vpn-gateways"></a><span data-ttu-id="a6cc7-105">Informazioni sui parametri di criteri IPsec e IKE per gateway VPN di Azure</span><span class="sxs-lookup"><span data-stu-id="a6cc7-105">About IPsec and IKE policy parameters for Azure VPN gateways</span></span>
<span data-ttu-id="a6cc7-106">Lo standard di protocollo IPsec e IKE supporta un'ampia gamma di algoritmi di crittografia in varie combinazioni.</span><span class="sxs-lookup"><span data-stu-id="a6cc7-106">IPsec and IKE protocol standard supports a wide range of cryptographic algorithms in various combinations.</span></span> <span data-ttu-id="a6cc7-107">Se i clienti non richiedono una combinazione specifica di algoritmi e parametri per la crittografia, i gateway VPN di Azure usano un set di proposte predefinite.</span><span class="sxs-lookup"><span data-stu-id="a6cc7-107">If customers do not request a specific combination of cryptographic algorithms and parameters, Azure VPN gateways use a set of default proposals.</span></span> <span data-ttu-id="a6cc7-108">I set di criteri predefiniti sono stati scelti per migliorare l'interoperabilità con un'ampia gamma di dispositivi VPN di terze parti in configurazioni predefinite.</span><span class="sxs-lookup"><span data-stu-id="a6cc7-108">The default policy sets were chosen to maximize interoperability with a wide range of third-party VPN devices in default configurations.</span></span> <span data-ttu-id="a6cc7-109">Di conseguenza, i criteri e il numero di proposte non possono coprire tutte le possibili combinazioni degli algoritmi di crittografia disponibili e della complessità delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="a6cc7-109">As a result, the policies and the number of proposals cannot cover all possible combinations of available cryptographic algorithms and key strengths.</span></span>

<span data-ttu-id="a6cc7-110">Il criterio predefinito impostato per il gateway VPN di Azure è elencato nel documento: [Informazioni sui dispositivi VPN e sui parametri IPsec/IKE per connessioni del Gateway VPN da sito a sito](vpn-gateway-about-vpn-devices.md).</span><span class="sxs-lookup"><span data-stu-id="a6cc7-110">The default policy set for Azure VPN gateway is listed in the document: [About VPN devices and IPsec/IKE parameters for Site-to-Site VPN Gateway connections](vpn-gateway-about-vpn-devices.md).</span></span>

## <a name="cryptographic-requirements"></a><span data-ttu-id="a6cc7-111">Requisiti per la crittografia</span><span class="sxs-lookup"><span data-stu-id="a6cc7-111">Cryptographic requirements</span></span>
<span data-ttu-id="a6cc7-112">Per le comunicazioni che richiedono algoritmi o parametri di crittografia specifici, in genere a causa di requisiti di conformità o sicurezza, i clienti possono ora configurare i gateway VPN di Azure per usare un criterio IPsec/IKE personalizzato con algoritmi di crittografia e complessità delle chiavi specifici, invece del set di criteri predefinito di Azure.</span><span class="sxs-lookup"><span data-stu-id="a6cc7-112">For communications that require specific cryptographic algorithms or parameters, typically due to compliance or security requirements, customers can now configure their Azure VPN gateways to use a custom IPsec/IKE policy with specific cryptographic algorithms and key strengths, rather than the Azure default policy sets.</span></span>

<span data-ttu-id="a6cc7-113">Ad esempio, i criteri in modalità principale IKEv2 per i gateway VPN di Azure usano solo il gruppo Diffie-Hellman Group 2 (1024 bit), mentre potrebbe essere necessario specificare gruppi più complessi da usare in IKE, ad esempio gruppo 14 (2048 bit), gruppo 24 (gruppo MODP 2048 bit) o ECP (gruppo a curva ellittica) a 256 o 384 bit (gruppo 19 e gruppo 20 rispettivamente).</span><span class="sxs-lookup"><span data-stu-id="a6cc7-113">For example, the IKEv2 main mode policies for Azure VPN gateways utilize only Diffie-Hellman Group 2 (1024 bits), whereas customers may need to specify stronger groups to be used in IKE, such as Group 14 (2048-bit), Group 24 (2048-bit MODP Group), or ECP (elliptic curve groups) 256 or 384 bit (Group 19 and Group 20, respectively).</span></span> <span data-ttu-id="a6cc7-114">Simili requisiti si applicano anche ai criteri IPsec in modalità rapida.</span><span class="sxs-lookup"><span data-stu-id="a6cc7-114">Similar requirements apply to IPsec quick mode policies as well.</span></span>

## <a name="custom-ipsecike-policy-with-azure-vpn-gateways"></a><span data-ttu-id="a6cc7-115">Criteri IPsec/IKE personalizzati con i gateway VPN di Azure</span><span class="sxs-lookup"><span data-stu-id="a6cc7-115">Custom IPsec/IKE policy with Azure VPN gateways</span></span>
<span data-ttu-id="a6cc7-116">I gateway VPN di Azure ora supportano i criteri IPsec/IKE personalizzati per connessione.</span><span class="sxs-lookup"><span data-stu-id="a6cc7-116">Azure VPN gateways now support per-connection, custom IPsec/IKE policy.</span></span> <span data-ttu-id="a6cc7-117">Per una connessione da sito a sito o da rete virtuale a rete virtuale, è possibile scegliere una combinazione specifica di algoritmi di crittografia per IPsec e IKE con attendibilità della chiave, come illustrato nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="a6cc7-117">For a Site-to-Site or VNet-to-VNet connection, you can choose a specific combination of cryptographic algorithms for IPsec and IKE with the desired key strength, as shown in the following example:</span></span>

![ipsec-ike-policy](./media/vpn-gateway-about-compliance-crypto/ipsecikepolicy.png)

<span data-ttu-id="a6cc7-119">È possibile creare un criterio IPsec/IKE e applicarlo a una connessione nuova o esistente.</span><span class="sxs-lookup"><span data-stu-id="a6cc7-119">You can create an IPsec/IKE policy and apply to a new or existing connection.</span></span> 

### <a name="workflow"></a><span data-ttu-id="a6cc7-120">Flusso di lavoro</span><span class="sxs-lookup"><span data-stu-id="a6cc7-120">Workflow</span></span>

1. <span data-ttu-id="a6cc7-121">Creare le reti virtuali, i gateway VPN o i gateway di rete locale per la topologia di connettività, come descritto in altri documenti sulle procedure</span><span class="sxs-lookup"><span data-stu-id="a6cc7-121">Create the virtual networks, VPN gateways, or local network gateways for your connectivity topology as described in other how-to documents</span></span>
2. <span data-ttu-id="a6cc7-122">Creare criteri IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="a6cc7-122">Create an IPsec/IKE policy</span></span>
3. <span data-ttu-id="a6cc7-123">È possibile applicare i criteri quando si crea una connessione S2S o da rete virtuale a rete virtuale</span><span class="sxs-lookup"><span data-stu-id="a6cc7-123">You can apply the policy when you create a S2S or VNet-to-VNet connection</span></span>
4. <span data-ttu-id="a6cc7-124">Se la connessione è già stata creata, è possibile applicare o aggiornare i criteri per una connessione esistente</span><span class="sxs-lookup"><span data-stu-id="a6cc7-124">If the connection is already created, you can apply or update the policy to an existing connection</span></span>


## <a name="ipsecike-policy-faq"></a><span data-ttu-id="a6cc7-125">Domande frequenti sui criteri IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="a6cc7-125">IPsec/IKE policy FAQ</span></span>

[!INCLUDE [vpn-gateway-ipsecikepolicy-faq-include](../../includes/vpn-gateway-ipsecikepolicy-faq-include.md)]


## <a name="next-steps"></a><span data-ttu-id="a6cc7-126">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a6cc7-126">Next steps</span></span>
<span data-ttu-id="a6cc7-127">Vedere [Configurare i criteri IPsec/IKE](vpn-gateway-ipsecikepolicy-rm-powershell.md) per istruzioni dettagliate sulla configurazione dei criteri IPsec/IKE personalizzato su una connessione.</span><span class="sxs-lookup"><span data-stu-id="a6cc7-127">See [Configure IPsec/IKE policy](vpn-gateway-ipsecikepolicy-rm-powershell.md) for step-by-step instructions on configuring custom IPsec/IKE policy on a connection.</span></span>

<span data-ttu-id="a6cc7-128">Vedere anche [Connettere più dispositivi VPN basati su criteri](vpn-gateway-connect-multiple-policybased-rm-ps.md) per altre informazioni sull'opzione UsePolicyBasedTrafficSelectors.</span><span class="sxs-lookup"><span data-stu-id="a6cc7-128">See also [Connect multiple policy-based VPN devices](vpn-gateway-connect-multiple-policybased-rm-ps.md) to learn more about the UsePolicyBasedTrafficSelectors option.</span></span>