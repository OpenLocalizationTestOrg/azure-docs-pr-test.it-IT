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
# <a name="troubleshooting-azure-site-to-site-vpn-disconnects-intermittently"></a><span data-ttu-id="6aabc-103">Risoluzione dei problemi: disconnessioni VPN da sito a sito di Azure intermittenti</span><span class="sxs-lookup"><span data-stu-id="6aabc-103">Troubleshooting: Azure Site-to-Site VPN disconnects intermittently</span></span>

<span data-ttu-id="6aabc-104">Si potrebbero riscontrare problemi di hello che una connessione nuova o esistente di Azure Microsoft Point-to-Site VPN non è stabile o si disconnette regolarmente.</span><span class="sxs-lookup"><span data-stu-id="6aabc-104">You might experience hello problem that a new or existing Microsoft Azure Point-to-Site VPN connection is not stable or disconnects regularly.</span></span> <span data-ttu-id="6aabc-105">Questo articolo fornisce passaggi toohelp identificare e risolvere hello causa del problema hello di risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="6aabc-105">This article provides troubleshoot steps toohelp you identify and resolve hello cause of hello problem.</span></span> 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-steps"></a><span data-ttu-id="6aabc-106">Passaggi per la risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="6aabc-106">Troubleshooting steps</span></span>

### <a name="prerequisite-step"></a><span data-ttu-id="6aabc-107">Passaggio preliminare</span><span class="sxs-lookup"><span data-stu-id="6aabc-107">Prerequisite step</span></span>

<span data-ttu-id="6aabc-108">Tipo di controllo hello del gateway di rete virtuale di Azure:</span><span class="sxs-lookup"><span data-stu-id="6aabc-108">Check hello type of Azure  virtual network gateway:</span></span>

1. <span data-ttu-id="6aabc-109">Andare troppo[portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6aabc-109">Go too[Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="6aabc-110">Controllare hello **Panoramica** pagina hello virtuali del gateway di rete per informazioni sul tipo hello.</span><span class="sxs-lookup"><span data-stu-id="6aabc-110">Check hello **Overview** page of hello virtual network gateway for hello type information.</span></span>
    
    ![Panoramica di Hello del gateway hello](media\vpn-gateway-troubleshoot-site-to-site-disconnected-intermittently\gatewayoverview.png)

### <a name="step-1-check-whether-hello-on-premises-vpn-device-is-validated"></a><span data-ttu-id="6aabc-112">Passaggio 1 verificare se hello locale viene convalidato il dispositivo VPN</span><span class="sxs-lookup"><span data-stu-id="6aabc-112">Step 1 Check whether hello on-premises VPN device is validated</span></span>

1. <span data-ttu-id="6aabc-113">Controllare se si usano un [dispositivo VPN e una versione del sistema operativo convalidati](vpn-gateway-about-vpn-devices.md#devicetable).</span><span class="sxs-lookup"><span data-stu-id="6aabc-113">Check whether you are using a [validated VPN device and operating system version](vpn-gateway-about-vpn-devices.md#devicetable).</span></span> <span data-ttu-id="6aabc-114">Se il dispositivo VPN hello non viene convalidato, è possibile toocontact hello dispositivo produttore toosee se è presente qualsiasi problema di compatibilità.</span><span class="sxs-lookup"><span data-stu-id="6aabc-114">If hello VPN device is not validated, you may have toocontact hello device manufacturer toosee if there is any compatibility issue.</span></span>
2. <span data-ttu-id="6aabc-115">Verificare che il dispositivo VPN hello sia configurato correttamente.</span><span class="sxs-lookup"><span data-stu-id="6aabc-115">Make sure that hello VPN device is correctly configured.</span></span> <span data-ttu-id="6aabc-116">Per altre informazioni, vedere [Esempi di modifica di configurazione dispositivo](vpn-gateway-about-vpn-devices.md#editing).</span><span class="sxs-lookup"><span data-stu-id="6aabc-116">For more information, see [Editing device configuration samples](vpn-gateway-about-vpn-devices.md#editing).</span></span>

### <a name="step-2-check-hello-security-association-settingsfor-policy-based-azure-virtual-network-gateways"></a><span data-ttu-id="6aabc-117">Passaggio 2 delle impostazioni di associazione di sicurezza hello controllo (per i gateway basato su criteri di rete virtuale di Azure)</span><span class="sxs-lookup"><span data-stu-id="6aabc-117">Step 2 Check hello Security Association settings(for policy-based Azure virtual network gateways)</span></span>

1. <span data-ttu-id="6aabc-118">Verificare che tale rete virtuale hello, subnet e gli intervalli hello **gateway di rete locale** definizione in Microsoft Azure sono uguali a quelli di configurazione di hello sul dispositivo VPN locale di hello.</span><span class="sxs-lookup"><span data-stu-id="6aabc-118">Make sure that hello virtual network, subnets and, ranges in hello **Local network gateway** definition in Microsoft Azure are same as hello configuration on hello on-premises VPN device.</span></span>
2. <span data-ttu-id="6aabc-119">Verificare che soddisfano le impostazioni di associazione di sicurezza hello.</span><span class="sxs-lookup"><span data-stu-id="6aabc-119">Verify that hello Security Association settings match.</span></span>

### <a name="step-3-check-for-user-defined-routes-or-network-security-groups-on-gateway-subnet"></a><span data-ttu-id="6aabc-120">Passaggio 3 Cercare le route definite dall'utente o i gruppi di sicurezza di rete nella subnet gateway</span><span class="sxs-lookup"><span data-stu-id="6aabc-120">Step 3 Check for User-Defined Routes or Network Security Groups on Gateway Subnet</span></span>

<span data-ttu-id="6aabc-121">Una route definita dall'utente nella subnet del gateway hello può essere parte del traffico di limitazione ed altro traffico.</span><span class="sxs-lookup"><span data-stu-id="6aabc-121">A user-defined route on hello gateway subnet may be restricting some traffic and allowing other traffic.</span></span> <span data-ttu-id="6aabc-122">In questo modo vengono visualizzate che connessione VPN hello è attendibile per una parte del traffico e consigliabile per gli altri utenti.</span><span class="sxs-lookup"><span data-stu-id="6aabc-122">This makes it appear that hello VPN connection is unreliable for some traffic and good for others.</span></span> 

### <a name="step-4-check-hello-one-vpn-tunnel-per-subnet-pair-setting-for-policy-based-virtual-network-gateways"></a><span data-ttu-id="6aabc-123">Passaggio 4 controllo hello "un Tunnel VPN per ogni coppia Subnet" impostazione (per i gateway di rete virtuale basata su criteri)</span><span class="sxs-lookup"><span data-stu-id="6aabc-123">Step 4 Check hello "one VPN Tunnel per Subnet Pair" setting (for policy-based virtual network gateways)</span></span>

<span data-ttu-id="6aabc-124">Verificare che tale hello locale dispositivo VPN è impostato toohave **un tunnel VPN per ogni coppia subnet** per gateway di rete virtuale basata su criteri.</span><span class="sxs-lookup"><span data-stu-id="6aabc-124">Make sure that hello on-premises VPN device is set toohave **one VPN tunnel per subnet pair** for policy-based virtual network gateways.</span></span>

### <a name="step-5-check-for-security-association-limitation-for-policy-based-virtual-network-gateways"></a><span data-ttu-id="6aabc-125">Passaggio 5 Controllare la limitazione di associazione di sicurezza (per i gateway di rete virtuale basati su criteri)</span><span class="sxs-lookup"><span data-stu-id="6aabc-125">Step 5 Check for Security Association Limitation (for policy-based virtual network gateways)</span></span>

<span data-ttu-id="6aabc-126">gateway di rete virtuale basata su criteri Hello ha un limite di 200 coppie di associazione di sicurezza di subnet.</span><span class="sxs-lookup"><span data-stu-id="6aabc-126">hello Policy-based virtual network gateway has limit of 200 subnet Security Association pairs.</span></span> <span data-ttu-id="6aabc-127">Se il numero di hello di subnet di rete virtuale di Azure moltiplicato volte per hello numero di subnet locale è maggiore di 200, subnet sporadici disconnessione.</span><span class="sxs-lookup"><span data-stu-id="6aabc-127">If hello number of Azure virtual network subnets multiplied times by hello number of local subnets is greater than 200, you see sporadic subnets disconnecting.</span></span>

### <a name="step-6-check-on-premises-vpn-device-external-interface-address"></a><span data-ttu-id="6aabc-128">Passaggio 6 Controllare l'indirizzo dell'interfaccia esterna del dispositivo VPN locale</span><span class="sxs-lookup"><span data-stu-id="6aabc-128">Step 6 Check on-premises VPN device external interface address</span></span>

- <span data-ttu-id="6aabc-129">Se hello indirizzo IP del dispositivo VPN hello è connessa a Internet è incluso in hello **gateway di rete locale** definizione in Azure, potrebbero verificarsi sporadici disconnessioni.</span><span class="sxs-lookup"><span data-stu-id="6aabc-129">If hello Internet facing IP address of hello VPN device is included in hello **Local network gateway** definition in Azure, you may experience sporadic disconnections.</span></span>
- <span data-ttu-id="6aabc-130">Hello interfaccia esterna del dispositivo deve essere direttamente su Internet hello.</span><span class="sxs-lookup"><span data-stu-id="6aabc-130">hello device's external interface must be directly on hello Internet.</span></span> <span data-ttu-id="6aabc-131">Non deve esistere alcun Network Address Translation (NAT) o un firewall tra hello Internet e il dispositivo di hello.</span><span class="sxs-lookup"><span data-stu-id="6aabc-131">There should be no Network Address Translation (NAT) or firewall between hello Internet and hello device.</span></span>
-  <span data-ttu-id="6aabc-132">Se si configura Firewall Clustering toohave un indirizzo IP virtuale, è necessario interrompere cluster hello ed esporre un accessorio VPN hello direttamente l'interfaccia pubblica tooa che hello gateway può interfacciarsi con.</span><span class="sxs-lookup"><span data-stu-id="6aabc-132">If you configure Firewall Clustering toohave a virtual IP, you must break hello cluster and expose hello VPN appliance directly tooa public interface that hello gateway can interface with.</span></span>

### <a name="step-7-check-whether-hello-on-premises-vpn-device-has-perfect-forward-secrecy-enabled"></a><span data-ttu-id="6aabc-133">Passaggio 7 di controllo se hello locale dispositivo VPN è l'impostazione di PFS abilitato</span><span class="sxs-lookup"><span data-stu-id="6aabc-133">Step 7 Check whether hello on-premises VPN device has Perfect Forward Secrecy enabled</span></span>

<span data-ttu-id="6aabc-134">Hello **Perfect Forward Secrecy** funzionalità può causare problemi di disconnessione hello.</span><span class="sxs-lookup"><span data-stu-id="6aabc-134">hello **Perfect Forward Secrecy** feature can cause hello disconnection problems.</span></span> <span data-ttu-id="6aabc-135">Se il dispositivo VPN hello è **perfetto PFS** abilitato, disabilitare la funzionalità di hello.</span><span class="sxs-lookup"><span data-stu-id="6aabc-135">If hello VPN device has **Perfect forward Secrecy** enabled, disable hello feature.</span></span> <span data-ttu-id="6aabc-136">Quindi [aggiornare i criteri IPsec gateway di rete virtuale hello](vpn-gateway-ipsecikepolicy-rm-powershell.md#managepolicy).</span><span class="sxs-lookup"><span data-stu-id="6aabc-136">Then [update hello virtual network gateway IPsec policy](vpn-gateway-ipsecikepolicy-rm-powershell.md#managepolicy).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6aabc-137">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6aabc-137">Next steps</span></span>

- [<span data-ttu-id="6aabc-138">Configurare una connessione Site-to-Site tooa la rete virtuale</span><span class="sxs-lookup"><span data-stu-id="6aabc-138">Configure a Site-to-Site connection tooa virtual network</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
- [<span data-ttu-id="6aabc-139">Configure IPsec/IKE policy for Site-to-Site VPN connections (Configurare i criteri IPsec/IKE per le connessioni VPN da sito a sito)</span><span class="sxs-lookup"><span data-stu-id="6aabc-139">Configure IPsec/IKE policy for Site-to-Site VPN connections</span></span>](vpn-gateway-ipsecikepolicy-rm-powershell.md)

