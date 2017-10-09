---
title: 'Connettere i siti di toomultiple una rete virtuale tramite il Gateway VPN e PowerShell: classico | Documenti Microsoft'
description: "In questo articolo verrà illustrata la connessione più locale siti tooa rete virtuale usando un Gateway VPN per il modello di distribuzione classica hello."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-service-management
ms.assetid: b043df6e-f1e8-4a4d-8467-c06079e2c093
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/20/2017
ms.author: yushwang
ms.openlocfilehash: 5404b1c55ed3453b4dbc94dfd93e47c0812025f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-site-to-site-connection-tooa-vnet-with-an-existing-vpn-gateway-connection-classic"></a><span data-ttu-id="e3ad1-103">Aggiungere un tooa di connessione da sito a sito rete virtuale con una connessione di gateway VPN esistente (classica)</span><span class="sxs-lookup"><span data-stu-id="e3ad1-103">Add a Site-to-Site connection tooa VNet with an existing VPN gateway connection (classic)</span></span>

[!INCLUDE [deployment models](../../includes/vpn-gateway-classic-deployment-model-include.md)]

> [!div class="op_single_selector"]
> * [<span data-ttu-id="e3ad1-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="e3ad1-104">Azure portal</span></span>](vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="e3ad1-105">PowerShell (classico)</span><span class="sxs-lookup"><span data-stu-id="e3ad1-105">PowerShell (classic)</span></span>](vpn-gateway-multi-site.md)
>
>

<span data-ttu-id="e3ad1-106">Questo articolo viene illustrato l'utilizzo di PowerShell tooadd da sito a sito (S2S) connessioni tooa gateway VPN con una connessione esistente.</span><span class="sxs-lookup"><span data-stu-id="e3ad1-106">This article walks you through using PowerShell tooadd Site-to-Site (S2S) connections tooa VPN gateway that has an existing connection.</span></span> <span data-ttu-id="e3ad1-107">Questo tipo di connessione è spesso tooas cui una configurazione "multi-site".</span><span class="sxs-lookup"><span data-stu-id="e3ad1-107">This type of connection is often referred tooas a "multi-site" configuration.</span></span> <span data-ttu-id="e3ad1-108">Hello passaggi in questo articolo si applicano le reti toovirtual create utilizzando il modello di distribuzione classica hello (noto anche come servizio di gestione).</span><span class="sxs-lookup"><span data-stu-id="e3ad1-108">hello steps in this article apply toovirtual networks created using hello classic deployment model (also known as Service Management).</span></span> <span data-ttu-id="e3ad1-109">Questi passaggi non vengono applicano le configurazioni di connessione coesistenti tooExpressRoute/Site-to-Site.</span><span class="sxs-lookup"><span data-stu-id="e3ad1-109">These steps do not apply tooExpressRoute/Site-to-Site coexisting connection configurations.</span></span>

### <a name="deployment-models-and-methods"></a><span data-ttu-id="e3ad1-110">Metodi e modelli di distribuzione</span><span class="sxs-lookup"><span data-stu-id="e3ad1-110">Deployment models and methods</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

<span data-ttu-id="e3ad1-111">Questa tabella viene aggiornata man mano che per questa configurazione diventano disponibili nuovi articoli e altri strumenti.</span><span class="sxs-lookup"><span data-stu-id="e3ad1-111">We update this table as new articles and additional tools become available for this configuration.</span></span> <span data-ttu-id="e3ad1-112">Quando un articolo è disponibile, è un collegamento direttamente tooit da questa tabella.</span><span class="sxs-lookup"><span data-stu-id="e3ad1-112">When an article is available, we link directly tooit from this table.</span></span>

[!INCLUDE [vpn-gateway-table-multi-site](../../includes/vpn-gateway-table-multisite-include.md)]

## <a name="about-connecting"></a><span data-ttu-id="e3ad1-113">Informazioni sulla connessione</span><span class="sxs-lookup"><span data-stu-id="e3ad1-113">About connecting</span></span>

<span data-ttu-id="e3ad1-114">È possibile connettere più locale siti tooa singola rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="e3ad1-114">You can connect multiple on-premises sites tooa single virtual network.</span></span> <span data-ttu-id="e3ad1-115">Ciò è particolarmente interessante per la creazione di soluzioni per cloud ibride.</span><span class="sxs-lookup"><span data-stu-id="e3ad1-115">This is especially attractive for building hybrid cloud solutions.</span></span> <span data-ttu-id="e3ad1-116">Creazione di un gateway di rete virtuale di Azure tooyour connessione multisito è simile toocreating altre connessioni da sito a sito.</span><span class="sxs-lookup"><span data-stu-id="e3ad1-116">Creating a multi-site connection tooyour Azure virtual network gateway is similar toocreating other Site-to-Site connections.</span></span> <span data-ttu-id="e3ad1-117">In effetti, è possibile utilizzare un gateway VPN di Azure esistente, purché il gateway hello è dinamico (basato su route).</span><span class="sxs-lookup"><span data-stu-id="e3ad1-117">In fact, you can use an existing Azure VPN gateway, as long as hello gateway is dynamic (route-based).</span></span>

<span data-ttu-id="e3ad1-118">Se si dispone già di una rete virtuale connessa tooyour di gateway statico, è possibile modificare hello gateway tipo toodynamic senza la necessità di rete virtuale di toorebuild hello in più siti di ordine tooaccommodate.</span><span class="sxs-lookup"><span data-stu-id="e3ad1-118">If you already have a static gateway connected tooyour virtual network, you can change hello gateway type toodynamic without needing toorebuild hello virtual network in order tooaccommodate multi-site.</span></span> <span data-ttu-id="e3ad1-119">Prima di modificare il tipo di routing hello, assicurarsi che il gateway VPN locale supporta le configurazioni VPN basate su route.</span><span class="sxs-lookup"><span data-stu-id="e3ad1-119">Before changing hello routing type, make sure that your on-premises VPN gateway supports route-based VPN configurations.</span></span>

<span data-ttu-id="e3ad1-120">![diagramma multisito](./media/vpn-gateway-multi-site/multisite.png "multisito")</span><span class="sxs-lookup"><span data-stu-id="e3ad1-120">![multi-site diagram](./media/vpn-gateway-multi-site/multisite.png "multi-site")</span></span>

## <a name="points-tooconsider"></a><span data-ttu-id="e3ad1-121">Tooconsider punti</span><span class="sxs-lookup"><span data-stu-id="e3ad1-121">Points tooconsider</span></span>

<span data-ttu-id="e3ad1-122">**Non sarà di rete virtuale di toouse in grado di hello toomake portale modifiche toothis.**</span><span class="sxs-lookup"><span data-stu-id="e3ad1-122">**You won't be able toouse hello portal toomake changes toothis virtual network.**</span></span> <span data-ttu-id="e3ad1-123">È necessario toomake file di configurazione di rete toohello a modifiche anziché portale hello.</span><span class="sxs-lookup"><span data-stu-id="e3ad1-123">You need toomake changes toohello network configuration file instead of using hello portal.</span></span> <span data-ttu-id="e3ad1-124">Se si apportano modifiche nel portale di hello, queste sovrascrivono le impostazioni di riferimenti multisito per la rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="e3ad1-124">If you make changes in hello portal, they'll overwrite your multi-site reference settings for this virtual network.</span></span>

<span data-ttu-id="e3ad1-125">È consigliabile familiarizzare tramite file di configurazione di rete hello ora hello termine procedura multisito hello.</span><span class="sxs-lookup"><span data-stu-id="e3ad1-125">You should feel comfortable using hello network configuration file by hello time you've completed hello multi-site procedure.</span></span> <span data-ttu-id="e3ad1-126">Tuttavia, se si dispone di più persone che lavorano alla configurazione di rete, è necessario assicurarsi che siano tutte a conoscenza questa limitazione toomake.</span><span class="sxs-lookup"><span data-stu-id="e3ad1-126">However, if you have multiple people working on your network configuration, you'll need toomake sure that everyone knows about this limitation.</span></span> <span data-ttu-id="e3ad1-127">Questo non significa che è possibile usare il portale di hello affatto.</span><span class="sxs-lookup"><span data-stu-id="e3ad1-127">This doesn't mean that you can't use hello portal at all.</span></span> <span data-ttu-id="e3ad1-128">È possibile utilizzare, per tutti gli altri, ad eccezione di rete virtuale specifica toothis configurazione modifiche apportare.</span><span class="sxs-lookup"><span data-stu-id="e3ad1-128">You can use it for everything else, except making configuration changes toothis particular virtual network.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="e3ad1-129">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="e3ad1-129">Before you begin</span></span>

<span data-ttu-id="e3ad1-130">Prima di iniziare la configurazione, verificare di aver seguito hello:</span><span class="sxs-lookup"><span data-stu-id="e3ad1-130">Before you begin configuration, verify that you have hello following:</span></span>

* <span data-ttu-id="e3ad1-131">Hardware VPN compatibile per ogni sede locale.</span><span class="sxs-lookup"><span data-stu-id="e3ad1-131">Compatible VPN hardware for each on-premises location.</span></span> <span data-ttu-id="e3ad1-132">Controllare [informazioni sui dispositivi VPN per la connettività di rete virtuale](vpn-gateway-about-vpn-devices.md) tooverify se hello periferica che si desidera toouse noto toobe compatibile.</span><span class="sxs-lookup"><span data-stu-id="e3ad1-132">Check [About VPN Devices for Virtual Network Connectivity](vpn-gateway-about-vpn-devices.md) tooverify if hello device that you want toouse is something that is known toobe compatible.</span></span>
* <span data-ttu-id="e3ad1-133">Un indirizzo IP IPv4 pubblico esterno per ogni dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="e3ad1-133">An externally facing public IPv4 IP address for each VPN device.</span></span> <span data-ttu-id="e3ad1-134">indirizzo IP di Hello non può trovarsi dietro un NAT.</span><span class="sxs-lookup"><span data-stu-id="e3ad1-134">hello IP address cannot be located behind a NAT.</span></span> <span data-ttu-id="e3ad1-135">Questo è un requisito.</span><span class="sxs-lookup"><span data-stu-id="e3ad1-135">This is requirement.</span></span>
* <span data-ttu-id="e3ad1-136">È necessario tooinstall hello più recente di hello cmdlet di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e3ad1-136">You'll need tooinstall hello latest version of hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="e3ad1-137">Assicurarsi di installare versione di gestione del servizio (SM) hello nella versione di gestione risorse toohello aggiunta.</span><span class="sxs-lookup"><span data-stu-id="e3ad1-137">Make sure you install hello Service Management (SM) version in addition toohello Resource Manager version.</span></span> <span data-ttu-id="e3ad1-138">Vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview) per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="e3ad1-138">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information.</span></span>
* <span data-ttu-id="e3ad1-139">Una persona esperta nella configurazione di hardware VPN.</span><span class="sxs-lookup"><span data-stu-id="e3ad1-139">Someone who is proficient at configuring your VPN hardware.</span></span> <span data-ttu-id="e3ad1-140">È necessario toohave un'ottima conoscenza delle procedure tooconfigure il dispositivo VPN o con un utente che esegue il lavoro.</span><span class="sxs-lookup"><span data-stu-id="e3ad1-140">You'll have toohave a strong understanding of how tooconfigure your VPN device, or work with someone who does.</span></span>
* <span data-ttu-id="e3ad1-141">intervalli di indirizzi IP Hello che si desidera toouse per la rete virtuale (se è ancora stato creato uno).</span><span class="sxs-lookup"><span data-stu-id="e3ad1-141">hello IP address ranges that you want toouse for your virtual network (if you haven't already created one).</span></span>
* <span data-ttu-id="e3ad1-142">intervalli di indirizzi IP Hello per ognuno dei siti di rete locale hello che si sarà possibile connettersi.</span><span class="sxs-lookup"><span data-stu-id="e3ad1-142">hello IP address ranges for each of hello local network sites that you'll be connecting to.</span></span> <span data-ttu-id="e3ad1-143">È necessario assicurarsi che per ognuno dei siti di rete locale hello che si desidera tooconnect toodo non si sovrappongono gli intervalli di indirizzi IP di hello toomake.</span><span class="sxs-lookup"><span data-stu-id="e3ad1-143">You'll need toomake sure that hello IP address ranges for each of hello local network sites that you want tooconnect toodo not overlap.</span></span> <span data-ttu-id="e3ad1-144">In caso contrario, il portale di hello o hello API REST rifiuterà configurazione hello in fase di caricamento.</span><span class="sxs-lookup"><span data-stu-id="e3ad1-144">Otherwise, hello portal or hello REST API will reject hello configuration being uploaded.</span></span><br><span data-ttu-id="e3ad1-145">Ad esempio, se si dispone di due siti di rete locale che contengono entrambe hello IP indirizzo intervallo 10.2.3.0/24 e di disporre di un pacchetto con un indirizzo di destinazione 10.2.3.3, Azure non saprà quale sito sono intervalli di indirizzi hello toosend hello pacchetto toobecause sovrapposti.</span><span class="sxs-lookup"><span data-stu-id="e3ad1-145">For example, if you have two local network sites that both contain hello IP address range 10.2.3.0/24 and you have a package with a destination address 10.2.3.3, Azure wouldn't know which site you want toosend hello package toobecause hello address ranges are overlapping.</span></span> <span data-ttu-id="e3ad1-146">problemi di routing tooprevent, Azure non consente tooupload un file di configurazione con intervalli sovrapposti.</span><span class="sxs-lookup"><span data-stu-id="e3ad1-146">tooprevent routing issues, Azure doesn't allow you tooupload a configuration file that has overlapping ranges.</span></span>

## <a name="1-create-a-site-to-site-vpn"></a><span data-ttu-id="e3ad1-147">1. Creare una VPN da sito a sito</span><span class="sxs-lookup"><span data-stu-id="e3ad1-147">1. Create a Site-to-Site VPN</span></span>
<span data-ttu-id="e3ad1-148">Se già si dispone di una VPN da sito a sito con un gateway di routing dinamico, eseguire l'operazione seguente.</span><span class="sxs-lookup"><span data-stu-id="e3ad1-148">If you already have a Site-to-Site VPN with a dynamic routing gateway, great!</span></span> <span data-ttu-id="e3ad1-149">È possibile procedere troppo[esportare le impostazioni di configurazione di rete virtuale hello](#export).</span><span class="sxs-lookup"><span data-stu-id="e3ad1-149">You can proceed too[Export hello virtual network configuration settings](#export).</span></span> <span data-ttu-id="e3ad1-150">In caso contrario, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="e3ad1-150">If not, do hello following:</span></span>

### <a name="if-you-already-have-a-site-to-site-virtual-network-but-it-has-a-static-policy-based-routing-gateway"></a><span data-ttu-id="e3ad1-151">Se già si ha a disposizione una rete virtuale da sito a sito, ma con un gateway di routing statico basato su criteri:</span><span class="sxs-lookup"><span data-stu-id="e3ad1-151">If you already have a Site-to-Site virtual network, but it has a static (policy-based) routing gateway:</span></span>
1. <span data-ttu-id="e3ad1-152">Modificare il ciclo di gateway tipo toodynamic.</span><span class="sxs-lookup"><span data-stu-id="e3ad1-152">Change your gateway type toodynamic routing.</span></span> <span data-ttu-id="e3ad1-153">Una VPN multisito richiede un gateway di routing dinamico, ovvero basato su route.</span><span class="sxs-lookup"><span data-stu-id="e3ad1-153">A multi-site VPN requires a dynamic (also known as route-based) routing gateway.</span></span> <span data-ttu-id="e3ad1-154">digitare il gateway toochange, sarà necessario toofirst delete hello esistente gateway, quindi crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="e3ad1-154">toochange your gateway type, you'll need toofirst delete hello existing gateway, then create a new one.</span></span> <span data-ttu-id="e3ad1-155">Per istruzioni, vedere [come toochange hello tipo per il gateway di routing VPN](vpn-gateway-configure-vpn-gateway-mp.md).</span><span class="sxs-lookup"><span data-stu-id="e3ad1-155">For instructions, see [How toochange hello VPN routing type for your gateway](vpn-gateway-configure-vpn-gateway-mp.md).</span></span>  
2. <span data-ttu-id="e3ad1-156">Configurare il nuovo gateway e creare il proprio tunnel VPN.</span><span class="sxs-lookup"><span data-stu-id="e3ad1-156">Configure your new gateway and create your VPN tunnel.</span></span> <span data-ttu-id="e3ad1-157">Per istruzioni, vedere [configurare un Gateway VPN nel portale di Azure classico hello](vpn-gateway-configure-vpn-gateway-mp.md).</span><span class="sxs-lookup"><span data-stu-id="e3ad1-157">For instructions, see [Configure a VPN Gateway in hello Azure Classic Portal](vpn-gateway-configure-vpn-gateway-mp.md).</span></span> <span data-ttu-id="e3ad1-158">In primo luogo, modificare il ciclo di gateway tipo toodynamic.</span><span class="sxs-lookup"><span data-stu-id="e3ad1-158">First, change your gateway type toodynamic routing.</span></span>

### <a name="if-you-dont-have-a-site-to-site-virtual-network"></a><span data-ttu-id="e3ad1-159">Se non si ha a disposizione una rete virtuale da sito a sito:</span><span class="sxs-lookup"><span data-stu-id="e3ad1-159">If you don't have a Site-to-Site virtual network:</span></span>
1. <span data-ttu-id="e3ad1-160">Creare la rete virtuale da sito a sito usando queste istruzioni: [creare una rete virtuale con una connessione VPN da sito a sito nel portale di Azure classico hello](vpn-gateway-site-to-site-create.md).</span><span class="sxs-lookup"><span data-stu-id="e3ad1-160">Create your Site-to-Site virtual network using these instructions: [Create a Virtual Network with a Site-to-Site VPN Connection in hello Azure Classic Portal](vpn-gateway-site-to-site-create.md).</span></span>  
2. <span data-ttu-id="e3ad1-161">Configurare un gateway di routing dinamico usando le istruzioni seguenti: [Configurare un gateway VPN](vpn-gateway-configure-vpn-gateway-mp.md).</span><span class="sxs-lookup"><span data-stu-id="e3ad1-161">Configure a dynamic routing gateway using these instructions: [Configure a VPN Gateway](vpn-gateway-configure-vpn-gateway-mp.md).</span></span> <span data-ttu-id="e3ad1-162">Tooselect assicurarsi di essere **routing dinamico** per il tipo di gateway.</span><span class="sxs-lookup"><span data-stu-id="e3ad1-162">Be sure tooselect **dynamic routing** for your gateway type.</span></span>

## <span data-ttu-id="e3ad1-163"><a name="export"></a>2. Esportare i file di configurazione di rete hello</span><span class="sxs-lookup"><span data-stu-id="e3ad1-163"><a name="export"></a>2. Export hello network configuration file</span></span>
<span data-ttu-id="e3ad1-164">Esportare il file di configurazione di rete di Azure eseguendo hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="e3ad1-164">Export your Azure network configuration file by running hello following command.</span></span> <span data-ttu-id="e3ad1-165">È possibile modificare il percorso di hello hello tooexport tooa diversi della posizione del file se necessario.</span><span class="sxs-lookup"><span data-stu-id="e3ad1-165">You can change hello location of hello file tooexport tooa different location if necessary.</span></span>

```powershell
Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
```

## <a name="3-open-hello-network-configuration-file"></a><span data-ttu-id="e3ad1-166">3. File di configurazione di rete aprire hello</span><span class="sxs-lookup"><span data-stu-id="e3ad1-166">3. Open hello network configuration file</span></span>
<span data-ttu-id="e3ad1-167">Aprire i file di configurazione di rete hello scaricato nell'ultimo passaggio hello.</span><span class="sxs-lookup"><span data-stu-id="e3ad1-167">Open hello network configuration file that you downloaded in hello last step.</span></span> <span data-ttu-id="e3ad1-168">Usare qualsiasi editor xml desiderato.</span><span class="sxs-lookup"><span data-stu-id="e3ad1-168">Use any xml editor that you like.</span></span> <span data-ttu-id="e3ad1-169">file Hello dovrebbe essere simile toohello seguenti:</span><span class="sxs-lookup"><span data-stu-id="e3ad1-169">hello file should look similar toohello following:</span></span>

        <NetworkConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
          <VirtualNetworkConfiguration>
            <LocalNetworkSites>
              <LocalNetworkSite name="Site1">
                <AddressSpace>
                  <AddressPrefix>10.0.0.0/16</AddressPrefix>
                  <AddressPrefix>10.1.0.0/16</AddressPrefix>
                </AddressSpace>
                <VPNGatewayAddress>131.2.3.4</VPNGatewayAddress>
              </LocalNetworkSite>
              <LocalNetworkSite name="Site2">
                <AddressSpace>
                  <AddressPrefix>10.2.0.0/16</AddressPrefix>
                  <AddressPrefix>10.3.0.0/16</AddressPrefix>
                </AddressSpace>
                <VPNGatewayAddress>131.4.5.6</VPNGatewayAddress>
              </LocalNetworkSite>
            </LocalNetworkSites>
            <VirtualNetworkSites>
              <VirtualNetworkSite name="VNet1" AffinityGroup="USWest">
                <AddressSpace>
                  <AddressPrefix>10.20.0.0/16</AddressPrefix>
                  <AddressPrefix>10.21.0.0/16</AddressPrefix>
                </AddressSpace>
                <Subnets>
                  <Subnet name="FE">
                    <AddressPrefix>10.20.0.0/24</AddressPrefix>
                  </Subnet>
                  <Subnet name="BE">
                    <AddressPrefix>10.20.1.0/24</AddressPrefix>
                  </Subnet>
                  <Subnet name="GatewaySubnet">
                    <AddressPrefix>10.20.2.0/29</AddressPrefix>
                  </Subnet>
                </Subnets>
                <Gateway>
                  <ConnectionsToLocalNetwork>
                    <LocalNetworkSiteRef name="Site1">
                      <Connection type="IPsec" />
                    </LocalNetworkSiteRef>
                  </ConnectionsToLocalNetwork>
                </Gateway>
              </VirtualNetworkSite>
            </VirtualNetworkSites>
          </VirtualNetworkConfiguration>
        </NetworkConfiguration>

## <a name="4-add-multiple-site-references"></a><span data-ttu-id="e3ad1-170">4. Aggiungere riferimenti a più siti</span><span class="sxs-lookup"><span data-stu-id="e3ad1-170">4. Add multiple site references</span></span>
<span data-ttu-id="e3ad1-171">Quando si aggiungono o rimuovono informazioni di riferimento del sito, si apportano modifiche di configurazione toohello ConnectionsToLocalNetwork/LocalNetworkSiteRef.</span><span class="sxs-lookup"><span data-stu-id="e3ad1-171">When you add or remove site reference information, you'll make configuration changes toohello ConnectionsToLocalNetwork/LocalNetworkSiteRef.</span></span> <span data-ttu-id="e3ad1-172">Aggiunta di un nuovo riferimento al sito locale attiva toocreate Azure un nuovo tunnel.</span><span class="sxs-lookup"><span data-stu-id="e3ad1-172">Adding a new local site reference triggers Azure toocreate a new tunnel.</span></span> <span data-ttu-id="e3ad1-173">Nell'esempio hello seguente la configurazione di rete hello è per la connessione a un singolo sito.</span><span class="sxs-lookup"><span data-stu-id="e3ad1-173">In hello example below, hello network configuration is for a single-site connection.</span></span> <span data-ttu-id="e3ad1-174">Dopo aver apportato le modifiche, salvare file hello.</span><span class="sxs-lookup"><span data-stu-id="e3ad1-174">Save hello file once you have finished making your changes.</span></span>

```
  <Gateway>
    <ConnectionsToLocalNetwork>
      <LocalNetworkSiteRef name="Site1"><Connection type="IPsec" /></LocalNetworkSiteRef>
    </ConnectionsToLocalNetwork>
  </Gateway>
```

<span data-ttu-id="e3ad1-175">tooadd altri riferimenti a siti (creare una configurazione multisita), è sufficiente aggiungere le righe aggiuntive "LocalNetworkSiteRef", come illustrato nell'esempio hello riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="e3ad1-175">tooadd additional site references (create a multi-site configuration), simply add additional "LocalNetworkSiteRef" lines, as shown in hello example below:</span></span>

```
  <Gateway>
    <ConnectionsToLocalNetwork>
      <LocalNetworkSiteRef name="Site1"><Connection type="IPsec" /></LocalNetworkSiteRef>
      <LocalNetworkSiteRef name="Site2"><Connection type="IPsec" /></LocalNetworkSiteRef>
    </ConnectionsToLocalNetwork>
  </Gateway>
```

## <a name="5-import-hello-network-configuration-file"></a><span data-ttu-id="e3ad1-176">5. File di configurazione di rete hello importazione</span><span class="sxs-lookup"><span data-stu-id="e3ad1-176">5. Import hello network configuration file</span></span>
<span data-ttu-id="e3ad1-177">Importare i file di configurazione di rete hello.</span><span class="sxs-lookup"><span data-stu-id="e3ad1-177">Import hello network configuration file.</span></span> <span data-ttu-id="e3ad1-178">Quando si importa questo file con modifiche hello, verranno aggiunti nuovi tunnel hello.</span><span class="sxs-lookup"><span data-stu-id="e3ad1-178">When you import this file with hello changes, hello new tunnels will be added.</span></span> <span data-ttu-id="e3ad1-179">Hello che useranno gateway dinamico hello creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="e3ad1-179">hello tunnels will use hello dynamic gateway that you created earlier.</span></span> <span data-ttu-id="e3ad1-180">È possibile utilizzare portale classico hello o file hello tooimport di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e3ad1-180">You can either use hello classic portal, or PowerShell tooimport hello file.</span></span>

## <a name="6-download-keys"></a><span data-ttu-id="e3ad1-181">6. Chiavi di download</span><span class="sxs-lookup"><span data-stu-id="e3ad1-181">6. Download keys</span></span>
<span data-ttu-id="e3ad1-182">Dopo aver aggiunto i nuovi tunnel, usare hello PowerShell cmdlet 'Get-AzureVNetGatewayKey' tooget hello chiavi IPsec/IKE già condivise per ogni tunnel.</span><span class="sxs-lookup"><span data-stu-id="e3ad1-182">Once your new tunnels have been added, use hello PowerShell cmdlet 'Get-AzureVNetGatewayKey' tooget hello IPsec/IKE pre-shared keys for each tunnel.</span></span>

<span data-ttu-id="e3ad1-183">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="e3ad1-183">For example:</span></span>

```powershell
Get-AzureVNetGatewayKey –VNetName "VNet1" –LocalNetworkSiteName "Site1"
Get-AzureVNetGatewayKey –VNetName "VNet1" –LocalNetworkSiteName "Site2"
```

<span data-ttu-id="e3ad1-184">Se si preferisce, è possibile utilizzare anche hello *Get Virtual Network Gateway Shared Key* tooget API REST hello chiavi già condivise.</span><span class="sxs-lookup"><span data-stu-id="e3ad1-184">If you prefer, you can also use hello *Get Virtual Network Gateway Shared Key* REST API tooget hello pre-shared keys.</span></span>

## <a name="7-verify-your-connections"></a><span data-ttu-id="e3ad1-185">7. Verificare le connessioni</span><span class="sxs-lookup"><span data-stu-id="e3ad1-185">7. Verify your connections</span></span>
<span data-ttu-id="e3ad1-186">Controllare lo stato di hello tunnel multisito.</span><span class="sxs-lookup"><span data-stu-id="e3ad1-186">Check hello multi-site tunnel status.</span></span> <span data-ttu-id="e3ad1-187">Dopo aver scaricato le chiavi di hello per ogni tunnel, è opportuno tooverify connessioni.</span><span class="sxs-lookup"><span data-stu-id="e3ad1-187">After downloading hello keys for each tunnel, you'll want tooverify connections.</span></span> <span data-ttu-id="e3ad1-188">Utilizzare tooget 'Get-AzureVnetConnection' tunnel un elenco di rete virtuale, come illustrato nel seguente esempio hello.</span><span class="sxs-lookup"><span data-stu-id="e3ad1-188">Use 'Get-AzureVnetConnection' tooget a list of virtual network tunnels, as shown in hello example below.</span></span> <span data-ttu-id="e3ad1-189">VNet1 è il nome di hello di hello rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="e3ad1-189">VNet1 is hello name of hello VNet.</span></span>

```powershell
Get-AzureVnetConnection -VNetName VNET1
```

<span data-ttu-id="e3ad1-190">Esempio restituito:</span><span class="sxs-lookup"><span data-stu-id="e3ad1-190">Example return:</span></span>

```
    ConnectivityState         : Connected
    EgressBytesTransferred    : 661530
    IngressBytesTransferred   : 519207
    LastConnectionEstablished : 5/2/2014 2:51:40 PM
    LastEventID               : 23401
    LastEventMessage          : hello connectivity state for hello local network site 'Site1' changed from Not Connected tooConnected.
    LastEventTimeStamp        : 5/2/2014 2:51:40 PM
    LocalNetworkSiteName      : Site1
    OperationDescription      : Get-AzureVNetConnection
    OperationId               : 7f68a8e6-51e9-9db4-88c2-16b8067fed7f
    OperationStatus           : Succeeded

    ConnectivityState         : Connected
    EgressBytesTransferred    : 789398
    IngressBytesTransferred   : 143908
    LastConnectionEstablished : 5/2/2014 3:20:40 PM
    LastEventID               : 23401
    LastEventMessage          : hello connectivity state for hello local network site 'Site2' changed from Not Connected tooConnected.
    LastEventTimeStamp        : 5/2/2014 2:51:40 PM
    LocalNetworkSiteName      : Site2
    OperationDescription      : Get-AzureVNetConnection
    OperationId               : 7893b329-51e9-9db4-88c2-16b8067fed7f
    OperationStatus           : Succeeded
```

## <a name="next-steps"></a><span data-ttu-id="e3ad1-191">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e3ad1-191">Next steps</span></span>

<span data-ttu-id="e3ad1-192">toolearn ulteriori informazioni sui gateway VPN, vedere [sul gateway VPN](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="e3ad1-192">toolearn more about VPN Gateways, see [About VPN Gateways](vpn-gateway-about-vpngateways.md).</span></span>
