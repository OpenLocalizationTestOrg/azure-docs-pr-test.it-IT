---
title: "Aggiungere più connessioni gateway VPN da sito a sito a una rete virtuale: portale di Azure: Resource Manager | Documentazione Microsoft"
description: "Come aggiungere più connessioni da sito a sito (S2S) a un gateway VPN con una connessione esistente"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f3e8b165-f20a-42ab-afbb-bf60974bb4b1
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/20/2017
ms.author: cherylmc
ms.openlocfilehash: 7ec57789ee76f4ec54e4f7b68ea75c19522f3d7c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="add-a-site-to-site-connection-to-a-vnet-with-an-existing-vpn-gateway-connection"></a><span data-ttu-id="3d04d-103">Aggiungere una connessione da sito a sito a una rete virtuale con una connessione gateway VPN esistente</span><span class="sxs-lookup"><span data-stu-id="3d04d-103">Add a Site-to-Site connection to a VNet with an existing VPN gateway connection</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="3d04d-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="3d04d-104">Azure portal</span></span>](vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="3d04d-105">PowerShell (classico)</span><span class="sxs-lookup"><span data-stu-id="3d04d-105">PowerShell (classic)</span></span>](vpn-gateway-multi-site.md)
>
> 

<span data-ttu-id="3d04d-106">Questo articolo illustra come usare il portale di Azure per aggiungere connessioni da sito a sito (S2S) a un gateway VPN con una connessione esistente.</span><span class="sxs-lookup"><span data-stu-id="3d04d-106">This article walks you through using the Azure portal to add Site-to-Site (S2S) connections to a VPN gateway that has an existing connection.</span></span> <span data-ttu-id="3d04d-107">Questo tipo di connessione è spesso definito configurazione "multisito".</span><span class="sxs-lookup"><span data-stu-id="3d04d-107">This type of connection is often referred to as a "multi-site" configuration.</span></span> <span data-ttu-id="3d04d-108">È possibile aggiungere una connessione da sito a sito a una rete virtuale che dispone già di una connessione da sito a sito, una connessione da punto a sito o una connessione da rete virtuale a rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="3d04d-108">You can add a S2S connection to a VNet that already has a S2S connection, Point-to-Site connection, or VNet-to-VNet connection.</span></span> <span data-ttu-id="3d04d-109">Quando si aggiungono delle connessioni, esistono alcune limitazioni di cui è necessario tenere conto.</span><span class="sxs-lookup"><span data-stu-id="3d04d-109">There are some limitations when adding connections.</span></span> <span data-ttu-id="3d04d-110">Prima di iniziare la configurazione, verificare quanto riportato nella sezione [Prima di iniziare](#before) di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="3d04d-110">Check the [Before you begin](#before) section in this article to verify before you start your configuration.</span></span> 

<span data-ttu-id="3d04d-111">Questo articolo si applica alle reti virtuali create con il modello di distribuzione Resource Manager e che dispongono di un gateway VPN di tipo RouteBased.</span><span class="sxs-lookup"><span data-stu-id="3d04d-111">This article applies to VNets created using the Resource Manager deployment model that have a RouteBased VPN gateway.</span></span> <span data-ttu-id="3d04d-112">Questi passaggi non si applicano alle configurazioni con connessioni coesistenti ExpressRoute/da sito a sito.</span><span class="sxs-lookup"><span data-stu-id="3d04d-112">These steps do not apply to ExpressRoute/Site-to-Site coexisting connection configurations.</span></span> <span data-ttu-id="3d04d-113">Per informazioni sulle connessioni coesistenti vedere [Creare connessioni coesistenti da sito a sito ed ExpressRoute](../expressroute/expressroute-howto-coexist-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="3d04d-113">See [ExpressRoute/S2S coexisting connections](../expressroute/expressroute-howto-coexist-resource-manager.md) for information about coexisting connections.</span></span>

### <a name="deployment-models-and-methods"></a><span data-ttu-id="3d04d-114">Metodi e modelli di distribuzione</span><span class="sxs-lookup"><span data-stu-id="3d04d-114">Deployment models and methods</span></span>
[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

<span data-ttu-id="3d04d-115">Questa tabella viene aggiornata man mano che per questa configurazione diventano disponibili nuovi articoli e altri strumenti.</span><span class="sxs-lookup"><span data-stu-id="3d04d-115">We update this table as new articles and additional tools become available for this configuration.</span></span> <span data-ttu-id="3d04d-116">Quando un articolo è disponibile, nella tabella sarà presente un collegamento diretto.</span><span class="sxs-lookup"><span data-stu-id="3d04d-116">When an article is available, we link directly to it from this table.</span></span>

[!INCLUDE [vpn-gateway-table-multi-site](../../includes/vpn-gateway-table-multisite-include.md)]

## <span data-ttu-id="3d04d-117"><a name="before"></a>Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="3d04d-117"><a name="before"></a>Before you begin</span></span>
<span data-ttu-id="3d04d-118">Verificare quanto segue:</span><span class="sxs-lookup"><span data-stu-id="3d04d-118">Verify the following items:</span></span>

* <span data-ttu-id="3d04d-119">Non si sta creando una connessione coesistente ExpressRoute/da sito a sito.</span><span class="sxs-lookup"><span data-stu-id="3d04d-119">You are not creating an ExpressRoute/S2S coexisting connection.</span></span>
* <span data-ttu-id="3d04d-120">Si dispone di una rete virtuale creata usando il modello di distribuzione Resource Manager con una connessione esistente.</span><span class="sxs-lookup"><span data-stu-id="3d04d-120">You have a virtual network that was created using the Resource Manager deployment model with an existing connection.</span></span>
* <span data-ttu-id="3d04d-121">Il gateway di rete virtuale per la rete virtuale è di tipo RouteBased.</span><span class="sxs-lookup"><span data-stu-id="3d04d-121">The virtual network gateway for your VNet is RouteBased.</span></span> <span data-ttu-id="3d04d-122">Se si dispone di un gateway VPN basato su criteri, è necessario eliminare il gateway di rete virtuale e creare un nuovo gateway VPN di tipo RouteBased.</span><span class="sxs-lookup"><span data-stu-id="3d04d-122">If you have a PolicyBased VPN gateway, you must delete the virtual network gateway and create a new VPN gateway as RouteBased.</span></span>
* <span data-ttu-id="3d04d-123">Nessuno degli intervalli di indirizzi si sovrappone a una qualsiasi delle reti virtuali a cui si connette questa rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="3d04d-123">None of the address ranges overlap for any of the VNets that this VNet is connecting to.</span></span>
* <span data-ttu-id="3d04d-124">Si dispone di un dispositivo VPN compatibile ed è presente un utente in grado di configurarlo.</span><span class="sxs-lookup"><span data-stu-id="3d04d-124">You have compatible VPN device and someone who is able to configure it.</span></span> <span data-ttu-id="3d04d-125">Vedere [Informazioni sui dispositivi VPN](vpn-gateway-about-vpn-devices.md).</span><span class="sxs-lookup"><span data-stu-id="3d04d-125">See [About VPN Devices](vpn-gateway-about-vpn-devices.md).</span></span> <span data-ttu-id="3d04d-126">Se non si ha familiarità con la configurazione del dispositivo VPN o con gli intervalli di indirizzi IP disponibili nella configurazione di rete locale, è necessario coordinarsi con qualcuno che possa fornire tali dettagli.</span><span class="sxs-lookup"><span data-stu-id="3d04d-126">If you aren't familiar with configuring your VPN device, or are unfamiliar with the IP address ranges located in your on-premises network configuration, you need to coordinate with someone who can provide those details for you.</span></span>
* <span data-ttu-id="3d04d-127">Si dispone di un indirizzo IP pubblico esterno per il dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="3d04d-127">You have an externally facing public IP address for your VPN device.</span></span> <span data-ttu-id="3d04d-128">L'indirizzo IP non può trovarsi dietro un NAT.</span><span class="sxs-lookup"><span data-stu-id="3d04d-128">This IP address cannot be located behind a NAT.</span></span>

## <span data-ttu-id="3d04d-129"><a name="part1"></a>Parte 1: Configurare una connessione</span><span class="sxs-lookup"><span data-stu-id="3d04d-129"><a name="part1"></a>Part 1 - Configure a connection</span></span>
1. <span data-ttu-id="3d04d-130">In un browser passare al [portale di Azure](http://portal.azure.com) e, se necessario, accedere con l'account Azure.</span><span class="sxs-lookup"><span data-stu-id="3d04d-130">From a browser, navigate to the [Azure portal](http://portal.azure.com) and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="3d04d-131">Fare clic su **All resources** (Tutte le risorse), individuare il **gateway di rete virtuale** nell'elenco di risorse e selezionarlo.</span><span class="sxs-lookup"><span data-stu-id="3d04d-131">Click **All resources** and locate your **virtual network gateway** from the list of resources and click it.</span></span>
3. <span data-ttu-id="3d04d-132">Nel pannello **Gateway di rete virtuale** fare clic su **Connessioni**.</span><span class="sxs-lookup"><span data-stu-id="3d04d-132">On the **Virtual network gateway** blade, click **Connections**.</span></span>
   
    <span data-ttu-id="3d04d-133">![Pannello Connessioni](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/connectionsblade.png "Connections blade")</span><span class="sxs-lookup"><span data-stu-id="3d04d-133">![Connections blade](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/connectionsblade.png "Connections blade")</span></span><br>
4. <span data-ttu-id="3d04d-134">Nel pannello **Connessioni** fare clic su **+Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="3d04d-134">On the **Connections** blade, click **+Add**.</span></span>
   
    <span data-ttu-id="3d04d-135">![Pulsante Aggiungi connessione](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addbutton.png "Add connection button")</span><span class="sxs-lookup"><span data-stu-id="3d04d-135">![Add connection button](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addbutton.png "Add connection button")</span></span><br>
5. <span data-ttu-id="3d04d-136">Nel pannello **Aggiungi connessione** compilare i campi seguenti:</span><span class="sxs-lookup"><span data-stu-id="3d04d-136">On the **Add connection** blade, fill out the following fields:</span></span>
   
   * <span data-ttu-id="3d04d-137">**Nome**: nome del sito a cui si sta creando la connessione.</span><span class="sxs-lookup"><span data-stu-id="3d04d-137">**Name:** The name you want to give to the site you are creating the connection to.</span></span>
   * <span data-ttu-id="3d04d-138">**Tipo di connessione**: selezionare **Da sito a sito (IPSec)**.</span><span class="sxs-lookup"><span data-stu-id="3d04d-138">**Connection type:** Select **Site-to-site (IPsec)**.</span></span>
     
     <span data-ttu-id="3d04d-139">![Pannello Aggiungi connessione](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addconnectionblade.png "Add connection blade")</span><span class="sxs-lookup"><span data-stu-id="3d04d-139">![Add connection blade](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addconnectionblade.png "Add connection blade")</span></span><br>

## <span data-ttu-id="3d04d-140"><a name="part2"></a>Parte 2: Aggiungere un gateway di rete locale</span><span class="sxs-lookup"><span data-stu-id="3d04d-140"><a name="part2"></a>Part 2 - Add a local network gateway</span></span>
1. <span data-ttu-id="3d04d-141">Fare clic su **Gateway di rete locale** ***Scegli un gateway di rete locale***.</span><span class="sxs-lookup"><span data-stu-id="3d04d-141">Click **Local network gateway** ***Choose a local network gateway***.</span></span> <span data-ttu-id="3d04d-142">Viene aperto il pannello **Scegli gateway di rete virtuale**.</span><span class="sxs-lookup"><span data-stu-id="3d04d-142">This will open the **Choose local network gateway** blade.</span></span>
   
    <span data-ttu-id="3d04d-143">![Scegli gateway di rete virtuale](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/chooselng.png "Choose local network gateway")</span><span class="sxs-lookup"><span data-stu-id="3d04d-143">![Choose local network gateway](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/chooselng.png "Choose local network gateway")</span></span><br>
2. <span data-ttu-id="3d04d-144">Fare clic su **Crea nuovo** per aprire il pannello **Crea un gateway di rete locale**.</span><span class="sxs-lookup"><span data-stu-id="3d04d-144">Click **Create new** to open the **Create local network gateway** blade.</span></span>
   
    <span data-ttu-id="3d04d-145">![Pannello Crea un gateway di rete locale](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/createlngblade.png "Create local network gateway")</span><span class="sxs-lookup"><span data-stu-id="3d04d-145">![Create local network gateway blade](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/createlngblade.png "Create local network gateway")</span></span><br>
3. <span data-ttu-id="3d04d-146">Nel pannello **Crea un gateway di rete locale** compilare i campi seguenti:</span><span class="sxs-lookup"><span data-stu-id="3d04d-146">On the **Create local network gateway** blade, fill out the following fields:</span></span>
   
   * <span data-ttu-id="3d04d-147">**Nome**: nome da assegnare alla risorsa gateway di rete locale.</span><span class="sxs-lookup"><span data-stu-id="3d04d-147">**Name:** The name you want to give to the local network gateway resource.</span></span>
   * <span data-ttu-id="3d04d-148">**Indirizzo IP**: indirizzo IP pubblico del dispositivo VPN nel sito a cui si vuole connettersi.</span><span class="sxs-lookup"><span data-stu-id="3d04d-148">**IP address:** The public IP address of the VPN device on the site that you want to connect to.</span></span>
   * <span data-ttu-id="3d04d-149">**Spazio indirizzi**: spazio indirizzi che si vuole venga indirizzato al nuovo sito di rete locale.</span><span class="sxs-lookup"><span data-stu-id="3d04d-149">**Address space:** The address space that you want to be routed to the new local network site.</span></span>
4. <span data-ttu-id="3d04d-150">Fare clic su **OK** nel pannello **Crea un gateway di rete locale** per salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="3d04d-150">Click **OK** on the **Create local network gateway** blade to save the changes.</span></span>

## <span data-ttu-id="3d04d-151"><a name="part3"></a>Parte 3: Aggiungere la chiave condivisa e creare la connessione</span><span class="sxs-lookup"><span data-stu-id="3d04d-151"><a name="part3"></a>Part 3 - Add the shared key and create the connection</span></span>
1. <span data-ttu-id="3d04d-152">Nel pannello **Aggiungi connessione** aggiungere la chiave condivisa che si intende usare per creare la connessione.</span><span class="sxs-lookup"><span data-stu-id="3d04d-152">On the **Add connection** blade, add the shared key that you want to use to create your connection.</span></span> <span data-ttu-id="3d04d-153">È possibile ottenere la chiave condivisa dal dispositivo VPN oppure crearne una in questa sede e quindi configurare il dispositivo VPN per l'uso della stessa chiave condivisa.</span><span class="sxs-lookup"><span data-stu-id="3d04d-153">You can either get the shared key from your VPN device, or make one up here and then configure your VPN device to use the same shared key.</span></span> <span data-ttu-id="3d04d-154">È fondamentale che le chiavi siano assolutamente identiche.</span><span class="sxs-lookup"><span data-stu-id="3d04d-154">The important thing is that the keys are exactly the same.</span></span>
   
    <span data-ttu-id="3d04d-155">![Chiave condivisa](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/sharedkey.png "Shared key")</span><span class="sxs-lookup"><span data-stu-id="3d04d-155">![Shared key](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/sharedkey.png "Shared key")</span></span><br>
2. <span data-ttu-id="3d04d-156">Nella parte inferiore del pannello fare clic su **OK** per creare la connessione.</span><span class="sxs-lookup"><span data-stu-id="3d04d-156">At the bottom of the blade, click **OK** to create the connection.</span></span>

## <span data-ttu-id="3d04d-157"><a name="part4"></a>Parte 4: Verificare la connessione VPN</span><span class="sxs-lookup"><span data-stu-id="3d04d-157"><a name="part4"></a>Part 4 - Verify the VPN connection</span></span>


[!INCLUDE [vpn-gateway-verify-connection-ps-rm](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <a name="next-steps"></a><span data-ttu-id="3d04d-158">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3d04d-158">Next steps</span></span>

<span data-ttu-id="3d04d-159">Dopo aver completato la connessione, è possibile aggiungere macchine virtuali alle reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="3d04d-159">Once your connection is complete, you can add virtual machines to your virtual networks.</span></span> <span data-ttu-id="3d04d-160">Per altre informazioni, vedere il [percorso di apprendimento](https://azure.microsoft.com/documentation/learning-paths/virtual-machines) relativo alle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="3d04d-160">See the virtual machines [learning path](https://azure.microsoft.com/documentation/learning-paths/virtual-machines) for more information.</span></span>
