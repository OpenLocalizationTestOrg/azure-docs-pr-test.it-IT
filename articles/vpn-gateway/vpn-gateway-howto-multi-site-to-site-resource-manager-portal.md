---
title: "Aggiungere più tooa di connessioni VPN gateway da sito a sito tra reti virtuali: portale di Azure: Gestione risorse | Documenti Microsoft"
description: "Aggiungere più siti S2S connessioni tooa gateway VPN con una connessione esistente"
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
ms.openlocfilehash: b8c9ff454967f509dcef725f8bcec8564fad9b00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-site-to-site-connection-tooa-vnet-with-an-existing-vpn-gateway-connection"></a><span data-ttu-id="cd855-103">Aggiungere un tooa di connessione da sito a sito rete virtuale con una connessione gateway VPN esistente</span><span class="sxs-lookup"><span data-stu-id="cd855-103">Add a Site-to-Site connection tooa VNet with an existing VPN gateway connection</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="cd855-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="cd855-104">Azure portal</span></span>](vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="cd855-105">PowerShell (classico)</span><span class="sxs-lookup"><span data-stu-id="cd855-105">PowerShell (classic)</span></span>](vpn-gateway-multi-site.md)
>
> 

<span data-ttu-id="cd855-106">Questo articolo viene illustrato l'utilizzo di hello tooadd portale Azure da sito a sito (S2S) connessioni tooa gateway VPN con una connessione esistente.</span><span class="sxs-lookup"><span data-stu-id="cd855-106">This article walks you through using hello Azure portal tooadd Site-to-Site (S2S) connections tooa VPN gateway that has an existing connection.</span></span> <span data-ttu-id="cd855-107">Questo tipo di connessione è spesso tooas cui una configurazione "multi-site".</span><span class="sxs-lookup"><span data-stu-id="cd855-107">This type of connection is often referred tooas a "multi-site" configuration.</span></span> <span data-ttu-id="cd855-108">È possibile aggiungere un tooa connessione S2S rete virtuale che dispone già di una connessione S2S, connessione Point-to-Site o rete connessione.</span><span class="sxs-lookup"><span data-stu-id="cd855-108">You can add a S2S connection tooa VNet that already has a S2S connection, Point-to-Site connection, or VNet-to-VNet connection.</span></span> <span data-ttu-id="cd855-109">Quando si aggiungono delle connessioni, esistono alcune limitazioni di cui è necessario tenere conto.</span><span class="sxs-lookup"><span data-stu-id="cd855-109">There are some limitations when adding connections.</span></span> <span data-ttu-id="cd855-110">Controllare hello [prima di iniziare](#before) sezione tooverify questo articolo prima di iniziare la configurazione.</span><span class="sxs-lookup"><span data-stu-id="cd855-110">Check hello [Before you begin](#before) section in this article tooverify before you start your configuration.</span></span> 

<span data-ttu-id="cd855-111">Questo articolo riguarda tooVNets creato con modello di distribuzione di gestione risorse di hello che dispone di un gateway VPN RouteBased.</span><span class="sxs-lookup"><span data-stu-id="cd855-111">This article applies tooVNets created using hello Resource Manager deployment model that have a RouteBased VPN gateway.</span></span> <span data-ttu-id="cd855-112">Questi passaggi non vengono applicano le configurazioni di connessione coesistenti tooExpressRoute/Site-to-Site.</span><span class="sxs-lookup"><span data-stu-id="cd855-112">These steps do not apply tooExpressRoute/Site-to-Site coexisting connection configurations.</span></span> <span data-ttu-id="cd855-113">Per informazioni sulle connessioni coesistenti vedere [Creare connessioni coesistenti da sito a sito ed ExpressRoute](../expressroute/expressroute-howto-coexist-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="cd855-113">See [ExpressRoute/S2S coexisting connections](../expressroute/expressroute-howto-coexist-resource-manager.md) for information about coexisting connections.</span></span>

### <a name="deployment-models-and-methods"></a><span data-ttu-id="cd855-114">Metodi e modelli di distribuzione</span><span class="sxs-lookup"><span data-stu-id="cd855-114">Deployment models and methods</span></span>
[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

<span data-ttu-id="cd855-115">Questa tabella viene aggiornata man mano che per questa configurazione diventano disponibili nuovi articoli e altri strumenti.</span><span class="sxs-lookup"><span data-stu-id="cd855-115">We update this table as new articles and additional tools become available for this configuration.</span></span> <span data-ttu-id="cd855-116">Quando un articolo è disponibile, è un collegamento direttamente tooit da questa tabella.</span><span class="sxs-lookup"><span data-stu-id="cd855-116">When an article is available, we link directly tooit from this table.</span></span>

[!INCLUDE [vpn-gateway-table-multi-site](../../includes/vpn-gateway-table-multisite-include.md)]

## <span data-ttu-id="cd855-117"><a name="before"></a>Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="cd855-117"><a name="before"></a>Before you begin</span></span>
<span data-ttu-id="cd855-118">Verificare hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="cd855-118">Verify hello following items:</span></span>

* <span data-ttu-id="cd855-119">Non si sta creando una connessione coesistente ExpressRoute/da sito a sito.</span><span class="sxs-lookup"><span data-stu-id="cd855-119">You are not creating an ExpressRoute/S2S coexisting connection.</span></span>
* <span data-ttu-id="cd855-120">Si dispone di una rete virtuale che è stata creata con modello di distribuzione di gestione risorse di hello con una connessione esistente.</span><span class="sxs-lookup"><span data-stu-id="cd855-120">You have a virtual network that was created using hello Resource Manager deployment model with an existing connection.</span></span>
* <span data-ttu-id="cd855-121">gateway di rete virtuale Hello per la rete virtuale è di tipo RouteBased.</span><span class="sxs-lookup"><span data-stu-id="cd855-121">hello virtual network gateway for your VNet is RouteBased.</span></span> <span data-ttu-id="cd855-122">Se si dispone di un gateway VPN PolicyBased, è necessario eliminare il gateway di rete virtuale hello e creare un nuovo gateway VPN come tipo RouteBased.</span><span class="sxs-lookup"><span data-stu-id="cd855-122">If you have a PolicyBased VPN gateway, you must delete hello virtual network gateway and create a new VPN gateway as RouteBased.</span></span>
* <span data-ttu-id="cd855-123">Nessuno degli intervalli di indirizzi hello si sovrappongono per uno qualsiasi dei hello reti virtuali che esegue la connessione a questa rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="cd855-123">None of hello address ranges overlap for any of hello VNets that this VNet is connecting to.</span></span>
* <span data-ttu-id="cd855-124">Si dispone di dispositivi VPN con compatibilità e chi è in grado di tooconfigure è.</span><span class="sxs-lookup"><span data-stu-id="cd855-124">You have compatible VPN device and someone who is able tooconfigure it.</span></span> <span data-ttu-id="cd855-125">Vedere [Informazioni sui dispositivi VPN](vpn-gateway-about-vpn-devices.md).</span><span class="sxs-lookup"><span data-stu-id="cd855-125">See [About VPN Devices](vpn-gateway-about-vpn-devices.md).</span></span> <span data-ttu-id="cd855-126">Se si non ha familiarità con la configurazione del dispositivo VPN o si ha familiarità con gli intervalli di indirizzi IP hello nella configurazione di rete locale, è necessario toocoordinate con qualcuno in grado di fornire i dettagli per l'utente.</span><span class="sxs-lookup"><span data-stu-id="cd855-126">If you aren't familiar with configuring your VPN device, or are unfamiliar with hello IP address ranges located in your on-premises network configuration, you need toocoordinate with someone who can provide those details for you.</span></span>
* <span data-ttu-id="cd855-127">Si dispone di un indirizzo IP pubblico esterno per il dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="cd855-127">You have an externally facing public IP address for your VPN device.</span></span> <span data-ttu-id="cd855-128">L'indirizzo IP non può trovarsi dietro un NAT.</span><span class="sxs-lookup"><span data-stu-id="cd855-128">This IP address cannot be located behind a NAT.</span></span>

## <span data-ttu-id="cd855-129"><a name="part1"></a>Parte 1: Configurare una connessione</span><span class="sxs-lookup"><span data-stu-id="cd855-129"><a name="part1"></a>Part 1 - Configure a connection</span></span>
1. <span data-ttu-id="cd855-130">Da un browser, passare toohello [portale di Azure](http://portal.azure.com) e, se necessario, accedere con l'account di Azure.</span><span class="sxs-lookup"><span data-stu-id="cd855-130">From a browser, navigate toohello [Azure portal](http://portal.azure.com) and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="cd855-131">Fare clic su **tutte le risorse** e individuare il **gateway di rete virtuale** dall'elenco di hello delle risorse e farvi clic sopra.</span><span class="sxs-lookup"><span data-stu-id="cd855-131">Click **All resources** and locate your **virtual network gateway** from hello list of resources and click it.</span></span>
3. <span data-ttu-id="cd855-132">In hello **gateway di rete virtuale** pannello, fare clic su **connessioni**.</span><span class="sxs-lookup"><span data-stu-id="cd855-132">On hello **Virtual network gateway** blade, click **Connections**.</span></span>
   
    <span data-ttu-id="cd855-133">![Pannello connessioni](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/connectionsblade.png "Pannello connessioni")</span><span class="sxs-lookup"><span data-stu-id="cd855-133">![Connections blade](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/connectionsblade.png "Connections blade")</span></span><br>
4. <span data-ttu-id="cd855-134">In hello **connessioni** pannello, fare clic su **+ Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="cd855-134">On hello **Connections** blade, click **+Add**.</span></span>
   
    <span data-ttu-id="cd855-135">![Pulsante di connessione Aggiungi](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addbutton.png "Aggiungi pulsante di connessione")</span><span class="sxs-lookup"><span data-stu-id="cd855-135">![Add connection button](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addbutton.png "Add connection button")</span></span><br>
5. <span data-ttu-id="cd855-136">In hello **Aggiungi connessione** pannello, compilare hello seguenti campi:</span><span class="sxs-lookup"><span data-stu-id="cd855-136">On hello **Add connection** blade, fill out hello following fields:</span></span>
   
   * <span data-ttu-id="cd855-137">**Nome:** hello Nome sito toohello toogive si sta creando una connessione hello.</span><span class="sxs-lookup"><span data-stu-id="cd855-137">**Name:** hello name you want toogive toohello site you are creating hello connection to.</span></span>
   * <span data-ttu-id="cd855-138">**Tipo di connessione**: selezionare **Da sito a sito (IPSec)**.</span><span class="sxs-lookup"><span data-stu-id="cd855-138">**Connection type:** Select **Site-to-site (IPsec)**.</span></span>
     
     <span data-ttu-id="cd855-139">![Pannello connessione Aggiungi](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addconnectionblade.png "Pannello di Aggiungi connessione")</span><span class="sxs-lookup"><span data-stu-id="cd855-139">![Add connection blade](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addconnectionblade.png "Add connection blade")</span></span><br>

## <span data-ttu-id="cd855-140"><a name="part2"></a>Parte 2: Aggiungere un gateway di rete locale</span><span class="sxs-lookup"><span data-stu-id="cd855-140"><a name="part2"></a>Part 2 - Add a local network gateway</span></span>
1. <span data-ttu-id="cd855-141">Fare clic su **Gateway di rete locale** ***Scegli un gateway di rete locale***.</span><span class="sxs-lookup"><span data-stu-id="cd855-141">Click **Local network gateway** ***Choose a local network gateway***.</span></span> <span data-ttu-id="cd855-142">Verrà aperta hello **scegliere gateway di rete locale** blade.</span><span class="sxs-lookup"><span data-stu-id="cd855-142">This will open hello **Choose local network gateway** blade.</span></span>
   
    <span data-ttu-id="cd855-143">![Gateway di rete locale scegliere](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/chooselng.png "scegliere gateway di rete locale")</span><span class="sxs-lookup"><span data-stu-id="cd855-143">![Choose local network gateway](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/chooselng.png "Choose local network gateway")</span></span><br>
2. <span data-ttu-id="cd855-144">Fare clic su **Crea nuovo** tooopen hello **gateway di rete locale crea** blade.</span><span class="sxs-lookup"><span data-stu-id="cd855-144">Click **Create new** tooopen hello **Create local network gateway** blade.</span></span>
   
    <span data-ttu-id="cd855-145">![Pannello di gateway di rete locale crea](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/createlngblade.png "crea gateway di rete locale")</span><span class="sxs-lookup"><span data-stu-id="cd855-145">![Create local network gateway blade](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/createlngblade.png "Create local network gateway")</span></span><br>
3. <span data-ttu-id="cd855-146">In hello **gateway di rete locale crea** pannello, compilare hello seguenti campi:</span><span class="sxs-lookup"><span data-stu-id="cd855-146">On hello **Create local network gateway** blade, fill out hello following fields:</span></span>
   
   * <span data-ttu-id="cd855-147">**Nome:** hello Nome risorsa del gateway di rete locale toohello toogive.</span><span class="sxs-lookup"><span data-stu-id="cd855-147">**Name:** hello name you want toogive toohello local network gateway resource.</span></span>
   * <span data-ttu-id="cd855-148">**Indirizzo IP:** hello indirizzo IP pubblico del dispositivo VPN hello nel sito di hello che si desidera tooconnect per.</span><span class="sxs-lookup"><span data-stu-id="cd855-148">**IP address:** hello public IP address of hello VPN device on hello site that you want tooconnect to.</span></span>
   * <span data-ttu-id="cd855-149">**Lo spazio degli indirizzi:** spazio degli indirizzi hello che si desidera toobe indirizzato toohello nuovo sito di rete locale.</span><span class="sxs-lookup"><span data-stu-id="cd855-149">**Address space:** hello address space that you want toobe routed toohello new local network site.</span></span>
4. <span data-ttu-id="cd855-150">Fare clic su **OK** su hello **gateway di rete locale crea** modifiche hello toosave di blade.</span><span class="sxs-lookup"><span data-stu-id="cd855-150">Click **OK** on hello **Create local network gateway** blade toosave hello changes.</span></span>

## <span data-ttu-id="cd855-151"><a name="part3"></a>Parte 3: aggiungere una chiave condivisa hello e creare la connessione hello</span><span class="sxs-lookup"><span data-stu-id="cd855-151"><a name="part3"></a>Part 3 - Add hello shared key and create hello connection</span></span>
1. <span data-ttu-id="cd855-152">In hello **Aggiungi connessione** pannello, aggiungere una chiave condivisa hello che si desidera toouse toocreate la connessione.</span><span class="sxs-lookup"><span data-stu-id="cd855-152">On hello **Add connection** blade, add hello shared key that you want toouse toocreate your connection.</span></span> <span data-ttu-id="cd855-153">È possibile ottenere la chiave condivisa hello dal dispositivo VPN o crearla qui e quindi configurare il hello toouse di dispositivi VPN stessa chiave condivisa.</span><span class="sxs-lookup"><span data-stu-id="cd855-153">You can either get hello shared key from your VPN device, or make one up here and then configure your VPN device toouse hello same shared key.</span></span> <span data-ttu-id="cd855-154">Hello importante aspetto è che le chiavi di hello sono esattamente hello stesso.</span><span class="sxs-lookup"><span data-stu-id="cd855-154">hello important thing is that hello keys are exactly hello same.</span></span>
   
    <span data-ttu-id="cd855-155">![Chiave condivisa](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/sharedkey.png "Chiave condivisa")</span><span class="sxs-lookup"><span data-stu-id="cd855-155">![Shared key](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/sharedkey.png "Shared key")</span></span><br>
2. <span data-ttu-id="cd855-156">Nella parte inferiore di hello del pannello hello, fare clic su **OK** connessione hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="cd855-156">At hello bottom of hello blade, click **OK** toocreate hello connection.</span></span>

## <span data-ttu-id="cd855-157"><a name="part4"></a>Parte 4: verificare una connessione VPN hello</span><span class="sxs-lookup"><span data-stu-id="cd855-157"><a name="part4"></a>Part 4 - Verify hello VPN connection</span></span>


[!INCLUDE [vpn-gateway-verify-connection-ps-rm](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <a name="next-steps"></a><span data-ttu-id="cd855-158">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="cd855-158">Next steps</span></span>

<span data-ttu-id="cd855-159">Una volta completata la connessione, è possibile aggiungere macchine virtuali tooyour le reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="cd855-159">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="cd855-160">Vedere le macchine virtuali hello [percorso di apprendimento](https://azure.microsoft.com/documentation/learning-paths/virtual-machines) per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="cd855-160">See hello virtual machines [learning path](https://azure.microsoft.com/documentation/learning-paths/virtual-machines) for more information.</span></span>
