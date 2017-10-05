---
title: Risolvere i problemi relativi alle disconnessioni VPN da sito a sito di Azure intermittenti | Microsoft Docs
description: Informazioni su come risolvere il problema per cui la connessione VPN da sito a sito viene periodicamente interrotta.
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
ms.openlocfilehash: 99a790617baa65116bfba976cd9279627e8775f3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshooting-azure-site-to-site-vpn-disconnects-intermittently"></a><span data-ttu-id="98450-103">Risoluzione dei problemi: disconnessioni VPN da sito a sito di Azure intermittenti</span><span class="sxs-lookup"><span data-stu-id="98450-103">Troubleshooting: Azure Site-to-Site VPN disconnects intermittently</span></span>

<span data-ttu-id="98450-104">Può verificarsi un problema a causa del quale una connessione VPN da punto a sito di Microsoft Azure nuova o esistente non è stabile o si interrompe periodicamente.</span><span class="sxs-lookup"><span data-stu-id="98450-104">You might experience the problem that a new or existing Microsoft Azure Point-to-Site VPN connection is not stable or disconnects regularly.</span></span> <span data-ttu-id="98450-105">Questo articolo illustra la procedura per identificare e risolvere la causa del problema.</span><span class="sxs-lookup"><span data-stu-id="98450-105">This article provides troubleshoot steps to help you identify and resolve the cause of the problem.</span></span> 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-steps"></a><span data-ttu-id="98450-106">Passaggi per la risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="98450-106">Troubleshooting steps</span></span>

### <a name="prerequisite-step"></a><span data-ttu-id="98450-107">Passaggio preliminare</span><span class="sxs-lookup"><span data-stu-id="98450-107">Prerequisite step</span></span>

<span data-ttu-id="98450-108">Controllare il tipo di gateway di rete virtuale di Azure:</span><span class="sxs-lookup"><span data-stu-id="98450-108">Check the type of Azure  virtual network gateway:</span></span>

1. <span data-ttu-id="98450-109">Accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="98450-109">Go to [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="98450-110">Per le informazioni sul tipo, controllare la pagina **Panoramica** del gateway di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="98450-110">Check the **Overview** page of the virtual network gateway for the type information.</span></span>
    
    ![Panoramica del gateway](media\vpn-gateway-troubleshoot-site-to-site-disconnected-intermittently\gatewayoverview.png)

### <a name="step-1-check-whether-the-on-premises-vpn-device-is-validated"></a><span data-ttu-id="98450-112">Passaggio 1 Controllare se il dispositivo VPN locale è convalidato</span><span class="sxs-lookup"><span data-stu-id="98450-112">Step 1 Check whether the on-premises VPN device is validated</span></span>

1. <span data-ttu-id="98450-113">Controllare se si usano un [dispositivo VPN e una versione del sistema operativo convalidati](vpn-gateway-about-vpn-devices.md#devicetable).</span><span class="sxs-lookup"><span data-stu-id="98450-113">Check whether you are using a [validated VPN device and operating system version](vpn-gateway-about-vpn-devices.md#devicetable).</span></span> <span data-ttu-id="98450-114">Se il dispositivo VPN non è convalidato, potrebbe essere necessario contattare il produttore del dispositivo per verificare se esiste qualche problema di compatibilità.</span><span class="sxs-lookup"><span data-stu-id="98450-114">If the VPN device is not validated, you may have to contact the device manufacturer to see if there is any compatibility issue.</span></span>
2. <span data-ttu-id="98450-115">Verificare che il dispositivo VPN sia configurato correttamente.</span><span class="sxs-lookup"><span data-stu-id="98450-115">Make sure that the VPN device is correctly configured.</span></span> <span data-ttu-id="98450-116">Per altre informazioni, vedere [Esempi di modifica di configurazione dispositivo](vpn-gateway-about-vpn-devices.md#editing).</span><span class="sxs-lookup"><span data-stu-id="98450-116">For more information, see [Editing device configuration samples](vpn-gateway-about-vpn-devices.md#editing).</span></span>

### <a name="step-2-check-the-security-association-settingsfor-policy-based-azure-virtual-network-gateways"></a><span data-ttu-id="98450-117">Passaggio 2 Controllare le impostazioni di associazione di sicurezza (per i gateway di rete virtuale di Azure basati su criteri)</span><span class="sxs-lookup"><span data-stu-id="98450-117">Step 2 Check the Security Association settings(for policy-based Azure virtual network gateways)</span></span>

1. <span data-ttu-id="98450-118">Verificare che la rete virtuale, le subnet e gli intervalli nella definizione **Gateway di rete locale** in Microsoft Azure siano gli stessi della configurazione sul dispositivo VPN locale.</span><span class="sxs-lookup"><span data-stu-id="98450-118">Make sure that the virtual network, subnets and, ranges in the **Local network gateway** definition in Microsoft Azure are same as the configuration on the on-premises VPN device.</span></span>
2. <span data-ttu-id="98450-119">Verificare che le impostazioni di associazione di sicurezza corrispondano.</span><span class="sxs-lookup"><span data-stu-id="98450-119">Verify that the Security Association settings match.</span></span>

### <a name="step-3-check-for-user-defined-routes-or-network-security-groups-on-gateway-subnet"></a><span data-ttu-id="98450-120">Passaggio 3 Cercare le route definite dall'utente o i gruppi di sicurezza di rete nella subnet gateway</span><span class="sxs-lookup"><span data-stu-id="98450-120">Step 3 Check for User-Defined Routes or Network Security Groups on Gateway Subnet</span></span>

<span data-ttu-id="98450-121">Una route definita dall'utente nella subnet gateway potrebbe limitare parte del traffico e consentirne un'altra.</span><span class="sxs-lookup"><span data-stu-id="98450-121">A user-defined route on the gateway subnet may be restricting some traffic and allowing other traffic.</span></span> <span data-ttu-id="98450-122">La connessione VPN appare quindi non affidabile per parte del traffico e valida per un'altra.</span><span class="sxs-lookup"><span data-stu-id="98450-122">This makes it appear that the VPN connection is unreliable for some traffic and good for others.</span></span> 

### <a name="step-4-check-the-one-vpn-tunnel-per-subnet-pair-setting-for-policy-based-virtual-network-gateways"></a><span data-ttu-id="98450-123">Passaggio 4 Controllare l'impostazione "un tunnel VPN per ogni coppia di subnet" (per i gateway di rete virtuale basati su criteri)</span><span class="sxs-lookup"><span data-stu-id="98450-123">Step 4 Check the "one VPN Tunnel per Subnet Pair" setting (for policy-based virtual network gateways)</span></span>

<span data-ttu-id="98450-124">Verificare che il dispositivo VPN locale sia impostato in modo da avere **un tunnel VPN per ogni coppia di subnet** per i gateway di rete virtuale basati su criteri.</span><span class="sxs-lookup"><span data-stu-id="98450-124">Make sure that the on-premises VPN device is set to have **one VPN tunnel per subnet pair** for policy-based virtual network gateways.</span></span>

### <a name="step-5-check-for-security-association-limitation-for-policy-based-virtual-network-gateways"></a><span data-ttu-id="98450-125">Passaggio 5 Controllare la limitazione di associazione di sicurezza (per i gateway di rete virtuale basati su criteri)</span><span class="sxs-lookup"><span data-stu-id="98450-125">Step 5 Check for Security Association Limitation (for policy-based virtual network gateways)</span></span>

<span data-ttu-id="98450-126">Il gateway di rete virtuale basato su criteri ha un limite di 200 coppie di associazione di sicurezza di subnet.</span><span class="sxs-lookup"><span data-stu-id="98450-126">The Policy-based virtual network gateway has limit of 200 subnet Security Association pairs.</span></span> <span data-ttu-id="98450-127">Se il numero di subnet di rete virtuale di Azure moltiplicato per il numero di subnet locali è superiore a 200, si osservano sporadiche disconnessioni delle subnet.</span><span class="sxs-lookup"><span data-stu-id="98450-127">If the number of Azure virtual network subnets multiplied times by the number of local subnets is greater than 200, you see sporadic subnets disconnecting.</span></span>

### <a name="step-6-check-on-premises-vpn-device-external-interface-address"></a><span data-ttu-id="98450-128">Passaggio 6 Controllare l'indirizzo dell'interfaccia esterna del dispositivo VPN locale</span><span class="sxs-lookup"><span data-stu-id="98450-128">Step 6 Check on-premises VPN device external interface address</span></span>

- <span data-ttu-id="98450-129">Se l'indirizzo IP per Internet del dispositivo VPN è incluso nella definizione del **gateway di rete locale** in Azure potrebbero verificarsi sporadiche disconnessioni.</span><span class="sxs-lookup"><span data-stu-id="98450-129">If the Internet facing IP address of the VPN device is included in the **Local network gateway** definition in Azure, you may experience sporadic disconnections.</span></span>
- <span data-ttu-id="98450-130">L'interfaccia esterna del dispositivo deve essere direttamente su Internet.</span><span class="sxs-lookup"><span data-stu-id="98450-130">The device's external interface must be directly on the Internet.</span></span> <span data-ttu-id="98450-131">Non devono essere presenti Network Address Translation (NAT) o firewall tra Internet e il dispositivo.</span><span class="sxs-lookup"><span data-stu-id="98450-131">There should be no Network Address Translation (NAT) or firewall between the Internet and the device.</span></span>
-  <span data-ttu-id="98450-132">Se si configura il clustering di firewall in modo che abbia un IP virtuale, è necessario interrompere il cluster ed esporre il dispositivo VPN direttamente a un'interfaccia pubblica con cui il gateway può interfacciarsi.</span><span class="sxs-lookup"><span data-stu-id="98450-132">If you configure Firewall Clustering to have a virtual IP, you must break the cluster and expose the VPN appliance directly to a public interface that the gateway can interface with.</span></span>

### <a name="step-7-check-whether-the-on-premises-vpn-device-has-perfect-forward-secrecy-enabled"></a><span data-ttu-id="98450-133">Passaggio 7 Controllare se il dispositivo VPN locale ha PFS (Perfect Forward Secrecy) abilitato</span><span class="sxs-lookup"><span data-stu-id="98450-133">Step 7 Check whether the on-premises VPN device has Perfect Forward Secrecy enabled</span></span>

<span data-ttu-id="98450-134">La funzionalità **PFS (Perfect Forward Secrecy)** può causare i problemi di disconnessione.</span><span class="sxs-lookup"><span data-stu-id="98450-134">The **Perfect Forward Secrecy** feature can cause the disconnection problems.</span></span> <span data-ttu-id="98450-135">Se il dispositivo VPN ha la funzionalità **PFS (Perfect Forward Secrecy)** abilitata, disabilitarla,</span><span class="sxs-lookup"><span data-stu-id="98450-135">If the VPN device has **Perfect forward Secrecy** enabled, disable the feature.</span></span> <span data-ttu-id="98450-136">quindi [aggiornare i criteri IPsec del gateway di rete virtuale](vpn-gateway-ipsecikepolicy-rm-powershell.md#managepolicy).</span><span class="sxs-lookup"><span data-stu-id="98450-136">Then [update the virtual network gateway IPsec policy](vpn-gateway-ipsecikepolicy-rm-powershell.md#managepolicy).</span></span>

## <a name="next-steps"></a><span data-ttu-id="98450-137">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="98450-137">Next steps</span></span>

- [<span data-ttu-id="98450-138">Configurare una connessione da sito a sito a una rete virtuale</span><span class="sxs-lookup"><span data-stu-id="98450-138">Configure a Site-to-Site connection to a virtual network</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
- [<span data-ttu-id="98450-139">Configure IPsec/IKE policy for Site-to-Site VPN connections (Configurare i criteri IPsec/IKE per le connessioni VPN da sito a sito)</span><span class="sxs-lookup"><span data-stu-id="98450-139">Configure IPsec/IKE policy for Site-to-Site VPN connections</span></span>](vpn-gateway-ipsecikepolicy-rm-powershell.md)

