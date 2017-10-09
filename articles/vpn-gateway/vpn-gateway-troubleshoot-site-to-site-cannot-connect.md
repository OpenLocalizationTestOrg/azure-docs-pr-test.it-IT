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
# <a name="troubleshooting-an-azure-site-to-site-vpn-connection-cannot-connect-and-stops-working"></a><span data-ttu-id="23df8-103">Risoluzione dei problemi: una connessione VPN da sito a sito di Azure non può essere stabilita e smette di funzionare</span><span class="sxs-lookup"><span data-stu-id="23df8-103">Troubleshooting: An Azure site-to-site VPN connection cannot connect and stops working</span></span>

<span data-ttu-id="23df8-104">Dopo aver configurato una connessione VPN da sito a sito tra una rete locale e una rete virtuale di Azure, hello connessione VPN improvvisamente smette di funzionare e non può essere riconnessa.</span><span class="sxs-lookup"><span data-stu-id="23df8-104">After you configure a site-to-site VPN connection between an on-premises network and an Azure virtual network, hello VPN connection suddenly stops working and cannot be reconnected.</span></span> <span data-ttu-id="23df8-105">Questo articolo fornisce la risoluzione dei problemi toohelp passaggi risolvere il problema.</span><span class="sxs-lookup"><span data-stu-id="23df8-105">This article provides troubleshooting steps toohelp you resolve this problem.</span></span> 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-steps"></a><span data-ttu-id="23df8-106">Passaggi per la risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="23df8-106">Troubleshooting steps</span></span>

<span data-ttu-id="23df8-107">problema di hello tooresolve, provare troppo[gateway VPN di Azure di reimpostazione hello](vpn-gateway-resetgw-classic.md) e reimpostare il tunnel hello dal dispositivo VPN locale di hello.</span><span class="sxs-lookup"><span data-stu-id="23df8-107">tooresolve hello problem, first try too[reset hello Azure VPN gateway](vpn-gateway-resetgw-classic.md) and reset hello tunnel from hello on-premises VPN device.</span></span> <span data-ttu-id="23df8-108">Se hello problema persiste, seguire questi causa hello tooidentify di passaggi di problema hello.</span><span class="sxs-lookup"><span data-stu-id="23df8-108">If hello problem persists, follow these steps tooidentify hello cause of hello problem.</span></span>

### <a name="prerequisite-step"></a><span data-ttu-id="23df8-109">Passaggio preliminare</span><span class="sxs-lookup"><span data-stu-id="23df8-109">Prerequisite step</span></span>

<span data-ttu-id="23df8-110">Controllare il tipo di hello del gateway VPN di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="23df8-110">Check hello type of hello Azure VPN gateway.</span></span>

1. <span data-ttu-id="23df8-111">Passare toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="23df8-111">Go toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="23df8-112">Controllare hello **Panoramica** pagina del gateway VPN hello per le informazioni sul tipo hello.</span><span class="sxs-lookup"><span data-stu-id="23df8-112">Check hello **Overview** page of hello VPN gateway for hello type information.</span></span>
    
    ![Panoramica del gateway hello](media\vpn-gateway-troubleshoot-site-to-site-cannot-connect\gatewayoverview.png)

### <a name="step-1-check-whether-hello-on-premises-vpn-device-is-validated"></a><span data-ttu-id="23df8-114">Passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="23df8-114">Step 1.</span></span> <span data-ttu-id="23df8-115">Controllare se viene convalidato dispositivo VPN locale di hello</span><span class="sxs-lookup"><span data-stu-id="23df8-115">Check whether hello on-premises VPN device is validated</span></span>

1. <span data-ttu-id="23df8-116">Controllare se si usano un [dispositivo VPN e una versione del sistema operativo convalidati](vpn-gateway-about-vpn-devices.md#devicetable).</span><span class="sxs-lookup"><span data-stu-id="23df8-116">Check whether you are using a [validated VPN device and operating system version](vpn-gateway-about-vpn-devices.md#devicetable).</span></span> <span data-ttu-id="23df8-117">Se il dispositivo di hello non è un dispositivo VPN convalidato, potrebbe essere toocontact hello dispositivo produttore toosee se è presente un problema di compatibilità.</span><span class="sxs-lookup"><span data-stu-id="23df8-117">If hello device is not a validated VPN device, you might have toocontact hello device manufacturer toosee if there is a compatibility issue.</span></span>

2. <span data-ttu-id="23df8-118">Verificare che il dispositivo VPN hello sia configurato correttamente.</span><span class="sxs-lookup"><span data-stu-id="23df8-118">Make sure that hello VPN device is correctly configured.</span></span> <span data-ttu-id="23df8-119">Per altre informazioni, vedere [Esempi di modifica di configurazione dispositivo](/vpn-gateway-about-vpn-devices.md#editing).</span><span class="sxs-lookup"><span data-stu-id="23df8-119">For more information, see [Edit device configuration samples](/vpn-gateway-about-vpn-devices.md#editing).</span></span>

### <a name="step-2-verify-hello-shared-key"></a><span data-ttu-id="23df8-120">Passaggio 2.</span><span class="sxs-lookup"><span data-stu-id="23df8-120">Step 2.</span></span> <span data-ttu-id="23df8-121">Verificare la chiave condivisa hello</span><span class="sxs-lookup"><span data-stu-id="23df8-121">Verify hello shared key</span></span>

<span data-ttu-id="23df8-122">Confrontare una chiave condivisa per hello locale VPN dispositivo toohello VPN di rete virtuale di Azure toomake che le chiavi di hello corrispondano hello.</span><span class="sxs-lookup"><span data-stu-id="23df8-122">Compare hello shared key for hello on-premises VPN device toohello Azure Virtual Network VPN toomake sure that hello keys match.</span></span> 

<span data-ttu-id="23df8-123">chiave condivisa di hello tooview per hello connessione VPN di Azure, utilizzare uno dei seguenti metodi hello:</span><span class="sxs-lookup"><span data-stu-id="23df8-123">tooview hello shared key for hello Azure VPN connection, use one of hello following methods:</span></span>

<span data-ttu-id="23df8-124">**Portale di Azure**</span><span class="sxs-lookup"><span data-stu-id="23df8-124">**Azure portal**</span></span>

1. <span data-ttu-id="23df8-125">Passare toohello VPN site-to-site connessione del gateway creato.</span><span class="sxs-lookup"><span data-stu-id="23df8-125">Go toohello VPN gateway site-to-site connection that you created.</span></span>

2. <span data-ttu-id="23df8-126">In hello **impostazioni** fare clic su **chiave condivisa**.</span><span class="sxs-lookup"><span data-stu-id="23df8-126">In hello **Settings** section, click **Shared key**.</span></span>
    
    ![Chiave condivisa](media/vpn-gateway-troubleshoot-site-to-site-cannot-connect/sharedkey.png)

<span data-ttu-id="23df8-128">**Azure PowerShell**</span><span class="sxs-lookup"><span data-stu-id="23df8-128">**Azure PowerShell**</span></span>

<span data-ttu-id="23df8-129">Per il modello di distribuzione Azure Resource Manager hello:</span><span class="sxs-lookup"><span data-stu-id="23df8-129">For hello Azure Resource Manager deployment model:</span></span>

    Get-AzureRmVirtualNetworkGatewayConnectionSharedKey -Name <Connection name> -ResourceGroupName <Resource group name>

<span data-ttu-id="23df8-130">Per il modello di distribuzione classica hello:</span><span class="sxs-lookup"><span data-stu-id="23df8-130">For hello classic deployment model:</span></span>

    Get-AzureVNetGatewayKey -VNetName -LocalNetworkSiteName

### <a name="step-3-verify-hello-vpn-peer-ips"></a><span data-ttu-id="23df8-131">Passaggio 3.</span><span class="sxs-lookup"><span data-stu-id="23df8-131">Step 3.</span></span> <span data-ttu-id="23df8-132">Verificare il peer VPN hello gli indirizzi IP</span><span class="sxs-lookup"><span data-stu-id="23df8-132">Verify hello VPN peer IPs</span></span>

-   <span data-ttu-id="23df8-133">definizione di IP in hello Hello **Gateway di rete locale** oggetto in Azure deve corrispondere hello IP del dispositivo locale.</span><span class="sxs-lookup"><span data-stu-id="23df8-133">hello IP definition in hello **Local Network Gateway** object in Azure should match hello on-premises device IP.</span></span>
-   <span data-ttu-id="23df8-134">definizione di IP gateway di Azure che è impostato su hello Hello locale dispositivo deve corrispondere hello Azure gateway IP.</span><span class="sxs-lookup"><span data-stu-id="23df8-134">hello Azure gateway IP definition that is set on hello on-premises device should match hello Azure gateway IP.</span></span>

### <a name="step-4-check-udr-and-nsgs-on-hello-gateway-subnet"></a><span data-ttu-id="23df8-135">Passaggio 4.</span><span class="sxs-lookup"><span data-stu-id="23df8-135">Step 4.</span></span> <span data-ttu-id="23df8-136">Controllare UDR e NSGs nella subnet del gateway hello</span><span class="sxs-lookup"><span data-stu-id="23df8-136">Check UDR and NSGs on hello gateway subnet</span></span>

<span data-ttu-id="23df8-137">Cercare e rimuovere routing definito dall'utente (UDR) o rete sicurezza gruppi di nella subnet del gateway hello e quindi il risultato di hello del test.</span><span class="sxs-lookup"><span data-stu-id="23df8-137">Check for and remove user-defined routing (UDR) or Network Security Groups (NSGs) on hello gateway subnet, and then test hello result.</span></span> <span data-ttu-id="23df8-138">Se il problema di hello viene risolto, convalidare le impostazioni di hello che UDR o gruppo applicato.</span><span class="sxs-lookup"><span data-stu-id="23df8-138">If hello problem is resolved, validate hello settings that UDR or NSG applied.</span></span>

### <a name="step-5-check-hello-on-premises-vpn-device-external-interface-address"></a><span data-ttu-id="23df8-139">Passaggio 5.</span><span class="sxs-lookup"><span data-stu-id="23df8-139">Step 5.</span></span> <span data-ttu-id="23df8-140">Controllare l'indirizzo interfaccia esterna del dispositivo VPN locale hello</span><span class="sxs-lookup"><span data-stu-id="23df8-140">Check hello on-premises VPN device external interface address</span></span>

- <span data-ttu-id="23df8-141">Se hello indirizzo IP con connessione Internet del dispositivo VPN hello è incluso in hello **rete locale** definizione in Azure, potrebbero verificarsi sporadici disconnessioni.</span><span class="sxs-lookup"><span data-stu-id="23df8-141">If hello Internet-facing IP address of hello VPN device is included in hello **Local network** definition in Azure, you might experience sporadic disconnections.</span></span>
- <span data-ttu-id="23df8-142">Hello interfaccia esterna del dispositivo deve essere direttamente su Internet hello.</span><span class="sxs-lookup"><span data-stu-id="23df8-142">hello device's external interface must be directly on hello Internet.</span></span> <span data-ttu-id="23df8-143">Non deve esistere alcuna conversione indirizzi di rete o un firewall tra hello Internet e il dispositivo di hello.</span><span class="sxs-lookup"><span data-stu-id="23df8-143">There should be no network address translation or firewall between hello Internet and hello device.</span></span>
- <span data-ttu-id="23df8-144">tooconfigure firewall clustering toohave un indirizzo IP virtuale, è necessario interrompere cluster hello ed esporre un accessorio VPN hello direttamente l'interfaccia pubblica tooa tale gateway hello può interfacciarsi con.</span><span class="sxs-lookup"><span data-stu-id="23df8-144">tooconfigure firewall clustering toohave a virtual IP, you must break hello cluster and expose hello VPN appliance directly tooa public interface that hello gateway can interface with.</span></span>

### <a name="step-6-verify-that-hello-subnets-match-exactly-azure-policy-based-gateways"></a><span data-ttu-id="23df8-145">Passaggio 6.</span><span class="sxs-lookup"><span data-stu-id="23df8-145">Step 6.</span></span> <span data-ttu-id="23df8-146">Verificare che corrispondano esattamente a subnet hello (gateway basato su criteri di Azure)</span><span class="sxs-lookup"><span data-stu-id="23df8-146">Verify that hello subnets match exactly (Azure policy-based gateways)</span></span>

-   <span data-ttu-id="23df8-147">Verificare che le subnet hello corrispondano esattamente tra hello rete virtuale di Azure e le definizioni locali per hello rete virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="23df8-147">Verify that hello subnets match exactly between hello Azure virtual network and on-premises definitions for hello Azure virtual network.</span></span>
-   <span data-ttu-id="23df8-148">Verificare che le subnet hello corrispondano esattamente tra hello **Gateway di rete locale** e le definizioni per la rete locale hello in locale.</span><span class="sxs-lookup"><span data-stu-id="23df8-148">Verify that hello subnets match exactly between hello **Local Network Gateway** and on-premises definitions for hello on-premises network.</span></span>

### <a name="step-7-verify-hello-azure-gateway-health-probe"></a><span data-ttu-id="23df8-149">Passaggio 7.</span><span class="sxs-lookup"><span data-stu-id="23df8-149">Step 7.</span></span> <span data-ttu-id="23df8-150">Verificare i probe di integrità hello gateway di Azure</span><span class="sxs-lookup"><span data-stu-id="23df8-150">Verify hello Azure gateway health probe</span></span>

1. <span data-ttu-id="23df8-151">Passare toohello [probe di integrità](https://&lt;YourVirtualNetworkGatewayIP&gt;:8081/healthprobe).</span><span class="sxs-lookup"><span data-stu-id="23df8-151">Go toohello [health probe](https://&lt;YourVirtualNetworkGatewayIP&gt;:8081/healthprobe).</span></span>

2. <span data-ttu-id="23df8-152">Fare clic sulle avviso certificato hello.</span><span class="sxs-lookup"><span data-stu-id="23df8-152">Click through hello certificate warning.</span></span>
3. <span data-ttu-id="23df8-153">Se si riceve una risposta, i gateway VPN hello è considerato integro.</span><span class="sxs-lookup"><span data-stu-id="23df8-153">If you receive a response, hello VPN gateway is considered healthy.</span></span> <span data-ttu-id="23df8-154">Se si non riceve una risposta, potrebbe non essere integro gateway hello o un gruppo nella subnet del gateway hello problema hello.</span><span class="sxs-lookup"><span data-stu-id="23df8-154">If you don't receive a response, hello gateway might not be healthy or an NSG on hello gateway subnet is causing hello problem.</span></span> <span data-ttu-id="23df8-155">Dopo il testo Hello è una risposta di esempio:</span><span class="sxs-lookup"><span data-stu-id="23df8-155">hello following text is a sample response:</span></span>

    <span data-ttu-id="23df8-156">&lt;?xml version="1.0"?&gt;  <string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">Primary Instance: GatewayTenantWorker_IN_1 GatewayTenantVersion: 14.7.24.6&lt;/string&gt;</span><span class="sxs-lookup"><span data-stu-id="23df8-156">&lt;?xml version="1.0"?>  <string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">Primary Instance: GatewayTenantWorker_IN_1 GatewayTenantVersion: 14.7.24.6</string&gt;</span></span>

### <a name="step-8-check-whether-hello-on-premises-vpn-device-has-hello-perfect-forward-secrecy-feature-enabled"></a><span data-ttu-id="23df8-157">Passaggio 8.</span><span class="sxs-lookup"><span data-stu-id="23df8-157">Step 8.</span></span> <span data-ttu-id="23df8-158">Controllare se hello locale dispositivo VPN è abilitata la funzionalità funzionalità PFS hello</span><span class="sxs-lookup"><span data-stu-id="23df8-158">Check whether hello on-premises VPN device has hello perfect forward secrecy feature enabled</span></span>

<span data-ttu-id="23df8-159">funzionalità di funzionalità PFS Hello può causare problemi di disconnessione.</span><span class="sxs-lookup"><span data-stu-id="23df8-159">hello perfect forward secrecy feature can cause disconnection problems.</span></span> <span data-ttu-id="23df8-160">Se il dispositivo VPN hello dispone di funzionalità PFS abilitata, disabilitare funzionalità hello.</span><span class="sxs-lookup"><span data-stu-id="23df8-160">If hello VPN device has perfect forward secrecy enabled, disable hello feature.</span></span> <span data-ttu-id="23df8-161">Aggiornare i criteri IPsec gateway VPN hello.</span><span class="sxs-lookup"><span data-stu-id="23df8-161">Then update hello VPN gateway IPsec policy.</span></span>

## <a name="next-steps"></a><span data-ttu-id="23df8-162">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="23df8-162">Next steps</span></span>

-   [<span data-ttu-id="23df8-163">Configurare una rete virtuale di tooa connessione site-to-site</span><span class="sxs-lookup"><span data-stu-id="23df8-163">Configure a site-to-site connection tooa virtual network</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
-   [<span data-ttu-id="23df8-164">Configurare criteri IPsec/IKE per connessioni VPN da sito a sito o da rete virtuale a rete virtuale</span><span class="sxs-lookup"><span data-stu-id="23df8-164">Configure an IPsec/IKE policy for site-to-site VPN connections</span></span>](vpn-gateway-ipsecikepolicy-rm-powershell.md)
