---
title: 'Connettere il tooan di rete locale rete virtuale di Azure: VPN Site-to-Site: portale | Documenti Microsoft'
description: Passaggi toocreate una connessione IPsec da locale rete tooan rete virtuale di Azure su hello rete Internet pubblica. Questi passaggi consentono di creare una connessione Site-to-Site VPN Gateway cross-premise usando il portale di hello.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 827a4db7-7fa5-4eaf-b7e1-e1518c51c815
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: cherylmc
ms.openlocfilehash: 6f0acbaf1bf016026cefade048a116e94686103d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-site-to-site-connection-in-hello-azure-portal"></a><span data-ttu-id="ed513-104">Creare una connessione Site-to-Site nel portale di Azure hello</span><span class="sxs-lookup"><span data-stu-id="ed513-104">Create a Site-to-Site connection in hello Azure portal</span></span>

<span data-ttu-id="ed513-105">Questo articolo illustra come toouse hello toocreate portale Azure una connessione gateway VPN da sito a sito dal toohello di rete locale rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="ed513-105">This article shows you how toouse hello Azure portal toocreate a Site-to-Site VPN gateway connection from your on-premises network toohello VNet.</span></span> <span data-ttu-id="ed513-106">passaggi di Hello in questo articolo si applicano al modello di distribuzione di gestione delle risorse toohello.</span><span class="sxs-lookup"><span data-stu-id="ed513-106">hello steps in this article apply toohello Resource Manager deployment model.</span></span> <span data-ttu-id="ed513-107">È inoltre possibile creare questa configurazione tramite uno strumento di distribuzione diverso o un modello di distribuzione selezionando un'opzione diversa da hello seguente elenco:</span><span class="sxs-lookup"><span data-stu-id="ed513-107">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="ed513-108">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="ed513-108">Azure portal</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="ed513-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ed513-109">PowerShell</span></span>](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [<span data-ttu-id="ed513-110">CLI</span><span class="sxs-lookup"><span data-stu-id="ed513-110">CLI</span></span>](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [<span data-ttu-id="ed513-111">Portale di Azure (classico)</span><span class="sxs-lookup"><span data-stu-id="ed513-111">Azure portal (classic)</span></span>](vpn-gateway-howto-site-to-site-classic-portal.md)
> 
>

<span data-ttu-id="ed513-112">Una connessione gateway VPN da sito a sito viene usato tooconnect tooan rete virtuale di Azure di rete locale tramite un tunnel VPN IPsec/IKE (IKEv1 o IKEv2).</span><span class="sxs-lookup"><span data-stu-id="ed513-112">A Site-to-Site VPN gateway connection is used tooconnect your on-premises network tooan Azure virtual network over an IPsec/IKE (IKEv1 or IKEv2) VPN tunnel.</span></span> <span data-ttu-id="ed513-113">Questo tipo di connessione richiede un VPN dispositivo si trova in locale che dispone di un tooit di indirizzo IP pubblico accessibile pubblicamente.</span><span class="sxs-lookup"><span data-stu-id="ed513-113">This type of connection requires a VPN device located on-premises that has an externally facing public IP address assigned tooit.</span></span> <span data-ttu-id="ed513-114">Per altre informazioni sui gateway VPN, vedere [Informazioni sul gateway VPN](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="ed513-114">For more information about VPN gateways, see [About VPN gateway](vpn-gateway-about-vpngateways.md).</span></span>

![Diagramma della connessione cross-premise gateway VPN da sito a sito](./media/vpn-gateway-howto-site-to-site-resource-manager-portal/site-to-site-diagram.png)

## <a name="before-you-begin"></a><span data-ttu-id="ed513-116">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="ed513-116">Before you begin</span></span>

<span data-ttu-id="ed513-117">Verificare che siano stati soddisfatti i seguenti criteri prima di iniziare la configurazione di hello:</span><span class="sxs-lookup"><span data-stu-id="ed513-117">Verify that you have met hello following criteria before beginning your configuration:</span></span>

* <span data-ttu-id="ed513-118">Assicurarsi di disporre di un dispositivo VPN compatibile e un utente che è in grado di tooconfigure è.</span><span class="sxs-lookup"><span data-stu-id="ed513-118">Make sure you have a compatible VPN device and someone who is able tooconfigure it.</span></span> <span data-ttu-id="ed513-119">Per altre informazioni sui dispositivi VPN compatibili e sulla configurazione dei dispositivi, vedere [Informazioni sui dispositivi VPN](vpn-gateway-about-vpn-devices.md).</span><span class="sxs-lookup"><span data-stu-id="ed513-119">For more information about compatible VPN devices and device configuration, see [About VPN Devices](vpn-gateway-about-vpn-devices.md).</span></span>
* <span data-ttu-id="ed513-120">Verificare di avere un indirizzo IPv4 pubblico esterno per il dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="ed513-120">Verify that you have an externally facing public IPv4 address for your VPN device.</span></span> <span data-ttu-id="ed513-121">L'indirizzo IP non può trovarsi dietro un NAT.</span><span class="sxs-lookup"><span data-stu-id="ed513-121">This IP address cannot be located behind a NAT.</span></span>
* <span data-ttu-id="ed513-122">Se non si ha familiarità con gli intervalli di indirizzi IP hello nello configurazione di rete locale, è necessario toocoordinate con qualcuno in grado di fornire i dettagli per l'utente.</span><span class="sxs-lookup"><span data-stu-id="ed513-122">If you are unfamiliar with hello IP address ranges located in your on-premises network configuration, you need toocoordinate with someone who can provide those details for you.</span></span> <span data-ttu-id="ed513-123">Quando si crea questa configurazione, è necessario specificare i prefissi intervallo indirizzi IP hello che Azure indirizzerà percorso locale tooyour.</span><span class="sxs-lookup"><span data-stu-id="ed513-123">When you create this configuration, you must specify hello IP address range prefixes that Azure will route tooyour on-premises location.</span></span> <span data-ttu-id="ed513-124">Nessuna delle subnet hello della rete locale può in giro con subnet della rete virtuale che si desidera tooconnect per hello.</span><span class="sxs-lookup"><span data-stu-id="ed513-124">None of hello subnets of your on-premises network can over lap with hello virtual network subnets that you want tooconnect to.</span></span> 

### <span data-ttu-id="ed513-125"><a name="values"></a>Valori di esempio</span><span class="sxs-lookup"><span data-stu-id="ed513-125"><a name="values"></a>Example values</span></span>

<span data-ttu-id="ed513-126">esempi di Hello in questo articolo utilizzano hello seguenti valori.</span><span class="sxs-lookup"><span data-stu-id="ed513-126">hello examples in this article use hello following values.</span></span> <span data-ttu-id="ed513-127">È possibile utilizzare questi toocreate valori un ambiente di test, o fare riferimento toothem toobetter comprendere esempi hello in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="ed513-127">You can use these values toocreate a test environment, or refer toothem toobetter understand hello examples in this article.</span></span>

* <span data-ttu-id="ed513-128">**Nome della rete virtuale:** TestVNet1</span><span class="sxs-lookup"><span data-stu-id="ed513-128">**VNet Name:** TestVNet1</span></span>
* <span data-ttu-id="ed513-129">**Spazio di indirizzi:**</span><span class="sxs-lookup"><span data-stu-id="ed513-129">**Address Space:**</span></span> 
  * <span data-ttu-id="ed513-130">10.11.0.0/16</span><span class="sxs-lookup"><span data-stu-id="ed513-130">10.11.0.0/16</span></span>
  * <span data-ttu-id="ed513-131">10.12.0.0/16 (facoltativo per questo esercizio)</span><span class="sxs-lookup"><span data-stu-id="ed513-131">10.12.0.0/16 (optional for this exercise)</span></span>
* <span data-ttu-id="ed513-132">**Subnet:**</span><span class="sxs-lookup"><span data-stu-id="ed513-132">**Subnets:**</span></span>
  * <span data-ttu-id="ed513-133">FrontEnd: 10.11.0.0/24</span><span class="sxs-lookup"><span data-stu-id="ed513-133">FrontEnd: 10.11.0.0/24</span></span>
  * <span data-ttu-id="ed513-134">BackEnd: 10.12.0.0/24 (facoltativo per questo esercizio)</span><span class="sxs-lookup"><span data-stu-id="ed513-134">BackEnd: 10.12.0.0/24 (optional for this exercise)</span></span>
* <span data-ttu-id="ed513-135">**GatewaySubnet:** 10.11.255.0/27</span><span class="sxs-lookup"><span data-stu-id="ed513-135">**GatewaySubnet:** 10.11.255.0/27</span></span>
* <span data-ttu-id="ed513-136">**Gruppo di risorse:** TestRG1</span><span class="sxs-lookup"><span data-stu-id="ed513-136">**Resource Group:** TestRG1</span></span>
* <span data-ttu-id="ed513-137">**Località:** Stati Uniti orientali</span><span class="sxs-lookup"><span data-stu-id="ed513-137">**Location:** East US</span></span>
* <span data-ttu-id="ed513-138">**Server DNS:** facoltativo.</span><span class="sxs-lookup"><span data-stu-id="ed513-138">**DNS Server:** Optional.</span></span> <span data-ttu-id="ed513-139">indirizzo IP di Hello del server DNS.</span><span class="sxs-lookup"><span data-stu-id="ed513-139">hello IP address of your DNS server.</span></span>
* <span data-ttu-id="ed513-140">**Nome gateway di rete virtuale:** VNet1GW</span><span class="sxs-lookup"><span data-stu-id="ed513-140">**Virtual Network Gateway Name:** VNet1GW</span></span>
* <span data-ttu-id="ed513-141">**IP pubblico:** VNet1GWIP</span><span class="sxs-lookup"><span data-stu-id="ed513-141">**Public IP:** VNet1GWIP</span></span>
* <span data-ttu-id="ed513-142">**Tipo VPN:** Basato su route</span><span class="sxs-lookup"><span data-stu-id="ed513-142">**VPN Type:** Route-based</span></span>
* <span data-ttu-id="ed513-143">**Tipo di connessione:** Da sito a sito (IPSec)</span><span class="sxs-lookup"><span data-stu-id="ed513-143">**Connection Type:** Site-to-site (IPsec)</span></span>
* <span data-ttu-id="ed513-144">**Tipo di gateway:** VPN</span><span class="sxs-lookup"><span data-stu-id="ed513-144">**Gateway Type:** VPN</span></span>
* <span data-ttu-id="ed513-145">**Nome del gateway di rete locale:** Site2</span><span class="sxs-lookup"><span data-stu-id="ed513-145">**Local Network Gateway Name:** Site2</span></span>
* <span data-ttu-id="ed513-146">**Nome connessione:** VNet1toSite2</span><span class="sxs-lookup"><span data-stu-id="ed513-146">**Connection Name:** VNet1toSite2</span></span>

## <span data-ttu-id="ed513-147"><a name="CreatVNet"></a>1. Crea rete virtuale</span><span class="sxs-lookup"><span data-stu-id="ed513-147"><a name="CreatVNet"></a>1. Create a virtual network</span></span>

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-basic-vnet-s2s-rm-portal-include.md)]

## <span data-ttu-id="ed513-148"><a name="dns"></a>2. Specificare un server DNS</span><span class="sxs-lookup"><span data-stu-id="ed513-148"><a name="dns"></a>2. Specify a DNS server</span></span>

<span data-ttu-id="ed513-149">DNS non è necessario toocreate una Site-to-Site connessione.</span><span class="sxs-lookup"><span data-stu-id="ed513-149">DNS is not required toocreate a Site-to-Site connection.</span></span> <span data-ttu-id="ed513-150">Tuttavia, se si desidera la risoluzione dei nomi toohave per le risorse di rete virtuale tooyour distribuito, specificare un server DNS.</span><span class="sxs-lookup"><span data-stu-id="ed513-150">However, if you want toohave name resolution for resources that are deployed tooyour virtual network, you should specify a DNS server.</span></span> <span data-ttu-id="ed513-151">Questa impostazione consente di specificare i server DNS hello che si vuole toouse per la risoluzione dei nomi per la rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="ed513-151">This setting lets you specify hello DNS server that you want toouse for name resolution for this virtual network.</span></span> <span data-ttu-id="ed513-152">Non comporta la creazione di un server DNS.</span><span class="sxs-lookup"><span data-stu-id="ed513-152">It does not create a DNS server.</span></span> <span data-ttu-id="ed513-153">Per altre informazioni sulla risoluzione dei nomi, vedere [Risoluzione dei nomi per le macchine virtuali e le istanze del ruolo](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span><span class="sxs-lookup"><span data-stu-id="ed513-153">For more information about name resolution, see [Name Resolution for VMs and role instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>

[!INCLUDE [vpn-gateway-add-dns-rm-portal](../../includes/vpn-gateway-add-dns-rm-portal-include.md)]

## <span data-ttu-id="ed513-154"><a name="gatewaysubnet"></a>3. Creare subnet del gateway hello</span><span class="sxs-lookup"><span data-stu-id="ed513-154"><a name="gatewaysubnet"></a>3. Create hello gateway subnet</span></span>

[!INCLUDE [vpn-gateway-aboutgwsubnet](../../includes/vpn-gateway-about-gwsubnet-include.md)]

[!INCLUDE [vpn-gateway-add-gwsubnet-rm-portal](../../includes/vpn-gateway-add-gwsubnet-s2s-rm-portal-include.md)]

## <span data-ttu-id="ed513-155"><a name="VNetGateway"></a>4. Creare il gateway VPN hello</span><span class="sxs-lookup"><span data-stu-id="ed513-155"><a name="VNetGateway"></a>4. Create hello VPN gateway</span></span>

[!INCLUDE [vpn-gateway-add-gw-s2s-rm-portal](../../includes/vpn-gateway-add-gw-s2s-rm-portal-include.md)]

## <span data-ttu-id="ed513-156"><a name="LocalNetworkGateway"></a>5. Creare il gateway di rete locale hello</span><span class="sxs-lookup"><span data-stu-id="ed513-156"><a name="LocalNetworkGateway"></a>5. Create hello local network gateway</span></span>

<span data-ttu-id="ed513-157">gateway di rete locale Hello si riferisce solitamente percorso locale tooyour.</span><span class="sxs-lookup"><span data-stu-id="ed513-157">hello local network gateway typically refers tooyour on-premises location.</span></span> <span data-ttu-id="ed513-158">Assegnare un nome mediante il quale Azure può fare riferimento tooit, quindi specificare l'indirizzo IP hello a sito di hello di toowhich di dispositivo VPN locale hello verrà creata una connessione.</span><span class="sxs-lookup"><span data-stu-id="ed513-158">You give hello site a name by which Azure can refer tooit, then specify hello IP address of hello on-premises VPN device toowhich you will create a connection.</span></span> <span data-ttu-id="ed513-159">È inoltre possibile specificare i prefissi di indirizzo IP hello che verranno distribuiti tramite il dispositivo VPN toohello di hello VPN gateway.</span><span class="sxs-lookup"><span data-stu-id="ed513-159">You also specify hello IP address prefixes that will be routed through hello VPN gateway toohello VPN device.</span></span> <span data-ttu-id="ed513-160">specificare i prefissi di indirizzo Hello sono prefissi hello presenti nella rete locale.</span><span class="sxs-lookup"><span data-stu-id="ed513-160">hello address prefixes you specify are hello prefixes located on your on-premises network.</span></span> <span data-ttu-id="ed513-161">Se le modifiche di rete locale o è necessario toochange hello indirizzo IP dispositivo VPN hello, è possibile aggiornare facilmente valori hello in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="ed513-161">If your on-premises network changes or you need toochange hello public IP address for hello VPN device, you can easily update hello values later.</span></span>

[!INCLUDE [Add local network gateway](../../includes/vpn-gateway-add-lng-s2s-rm-portal-include.md)]

## <span data-ttu-id="ed513-162"><a name="VPNDevice"></a>6. Configurare il dispositivo VPN</span><span class="sxs-lookup"><span data-stu-id="ed513-162"><a name="VPNDevice"></a>6. Configure your VPN device</span></span>

<span data-ttu-id="ed513-163">Rete locale tooan di connessioni da sito a sito richiedono un dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="ed513-163">Site-to-Site connections tooan on-premises network require a VPN device.</span></span> <span data-ttu-id="ed513-164">In questo passaggio viene configurato il dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="ed513-164">In this step, you configure your VPN device.</span></span> <span data-ttu-id="ed513-165">Quando si configura il dispositivo VPN, è necessario hello segue:</span><span class="sxs-lookup"><span data-stu-id="ed513-165">When configuring your VPN device, you need hello following:</span></span>

- <span data-ttu-id="ed513-166">Chiave condivisa.</span><span class="sxs-lookup"><span data-stu-id="ed513-166">A shared key.</span></span> <span data-ttu-id="ed513-167">Questo è hello stesso condiviso chiave specificate al momento della creazione della connessione VPN da sito a sito.</span><span class="sxs-lookup"><span data-stu-id="ed513-167">This is hello same shared key that you specify when creating your Site-to-Site VPN connection.</span></span> <span data-ttu-id="ed513-168">In questi esempi viene usata una chiave condivisa semplice.</span><span class="sxs-lookup"><span data-stu-id="ed513-168">In our examples, we use a basic shared key.</span></span> <span data-ttu-id="ed513-169">Si consiglia di generare un toouse chiave più complesse.</span><span class="sxs-lookup"><span data-stu-id="ed513-169">We recommend that you generate a more complex key toouse.</span></span>
- <span data-ttu-id="ed513-170">Hello indirizzo IP pubblico del gateway di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="ed513-170">hello Public IP address of your virtual network gateway.</span></span> <span data-ttu-id="ed513-171">È possibile visualizzare l'indirizzo IP pubblico hello utilizzando hello portale di Azure, PowerShell o CLI.</span><span class="sxs-lookup"><span data-stu-id="ed513-171">You can view hello public IP address by using hello Azure portal, PowerShell, or CLI.</span></span> <span data-ttu-id="ed513-172">hello toofind indirizzo IP pubblico del gateway VPN usando il portale di Azure, hello passare troppo**gateway di rete virtuale**, quindi fare clic su nome hello del gateway.</span><span class="sxs-lookup"><span data-stu-id="ed513-172">toofind hello Public IP address of your VPN gateway using hello Azure portal, navigate too**Virtual network gateways**, then click hello name of your gateway.</span></span>

[!INCLUDE [Configure a VPN device](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]

## <span data-ttu-id="ed513-173"><a name="CreateConnection"></a>7. Creare la connessione VPN hello</span><span class="sxs-lookup"><span data-stu-id="ed513-173"><a name="CreateConnection"></a>7. Create hello VPN connection</span></span>

<span data-ttu-id="ed513-174">Creare la connessione VPN Site-to-Site hello tra il gateway di rete virtuale e il dispositivo VPN locale.</span><span class="sxs-lookup"><span data-stu-id="ed513-174">Create hello Site-to-Site VPN connection between your virtual network gateway and your on-premises VPN device.</span></span>

[!INCLUDE [Add connections](../../includes/vpn-gateway-add-site-to-site-connection-s2s-rm-portal-include.md)]

## <span data-ttu-id="ed513-175"><a name="VerifyConnection"></a>8. Verificare una connessione VPN hello</span><span class="sxs-lookup"><span data-stu-id="ed513-175"><a name="VerifyConnection"></a>8. Verify hello VPN connection</span></span>

[!INCLUDE [Verify - Azure portal](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <span data-ttu-id="ed513-176"><a name="connectVM"></a>macchina virtuale di tooconnect tooa</span><span class="sxs-lookup"><span data-stu-id="ed513-176"><a name="connectVM"></a>tooconnect tooa virtual machine</span></span>

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-s2s-include.md)]

## <span data-ttu-id="ed513-177"><a name="reset"></a>Come tooreset un gateway VPN</span><span class="sxs-lookup"><span data-stu-id="ed513-177"><a name="reset"></a>How tooreset a VPN gateway</span></span>

<span data-ttu-id="ed513-178">La reimpostazione del gateway VPN di Azure è utile se si perde la connettività VPN cross-premise in uno o più tunnel VPN da sito a sito.</span><span class="sxs-lookup"><span data-stu-id="ed513-178">Resetting an Azure VPN gateway is helpful if you lose cross-premises VPN connectivity on one or more Site-to-Site VPN tunnels.</span></span> <span data-ttu-id="ed513-179">In questo caso, i dispositivi VPN locali sono tutte le funzioni correttamente, ma sono tooestablish non è possibile tunnel IPsec con gateway VPN di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="ed513-179">In this situation, your on-premises VPN devices are all working correctly, but are not able tooestablish IPsec tunnels with hello Azure VPN gateways.</span></span> <span data-ttu-id="ed513-180">Per la procedura da seguire, vedere [Reimpostare un gateway VPN](vpn-gateway-resetgw-classic.md).</span><span class="sxs-lookup"><span data-stu-id="ed513-180">For steps, see [Reset a VPN gateway](vpn-gateway-resetgw-classic.md).</span></span>

## <span data-ttu-id="ed513-181"><a name="resize"></a>Come toochange un gateway SKU (ridimensionare un gateway)</span><span class="sxs-lookup"><span data-stu-id="ed513-181"><a name="resize"></a>How toochange a gateway SKU (resize a gateway)</span></span>

<span data-ttu-id="ed513-182">Per hello passaggi toochange un SKU di gateway, vedere [SKU di Gateway](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span><span class="sxs-lookup"><span data-stu-id="ed513-182">For hello steps toochange a gateway SKU, see [Gateway SKUs](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ed513-183">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ed513-183">Next steps</span></span>

* <span data-ttu-id="ed513-184">Per informazioni su BGP, vedere hello [BGP Panoramica](vpn-gateway-bgp-overview.md) e [come tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span><span class="sxs-lookup"><span data-stu-id="ed513-184">For information about BGP, see hello [BGP Overview](vpn-gateway-bgp-overview.md) and [How tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span></span>
* <span data-ttu-id="ed513-185">Per informazioni sul tunneling forzato, vedere [Informazioni sul tunneling forzato](vpn-gateway-forced-tunneling-rm.md).</span><span class="sxs-lookup"><span data-stu-id="ed513-185">For information about Forced Tunneling, see [About Forced Tunneling](vpn-gateway-forced-tunneling-rm.md).</span></span>
* <span data-ttu-id="ed513-186">Per informazioni sulle connessioni da rete attiva a rete attiva a disponibilità elevata, vedere [Connettività cross-premise e da rete virtuale a rete virtuale a disponibilità elevata](vpn-gateway-highlyavailable.md).</span><span class="sxs-lookup"><span data-stu-id="ed513-186">For information about Highly Available Active-Active connections, see [Highly Available cross-premises and VNet-to-VNet connectivity](vpn-gateway-highlyavailable.md).</span></span>
