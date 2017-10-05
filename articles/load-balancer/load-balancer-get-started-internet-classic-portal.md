---
title: Creare un servizio di bilanciamento del carico con connessione Internet - Portale di Azure classico | Documentazione Microsoft
description: Informazioni su come creare un servizio di bilanciamento del carico Internet nel modello di distribuzione classica mediante il portale di Azure classico
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: fa3e93c0-968a-472d-a17c-65665c050db2
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: a022154f5eca6de2d2dbfc1b9aa30d2ea0a7d650
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-classic-in-the-azure-classic-portal"></a><span data-ttu-id="02994-103">Introduzione alla creazione del servizio di bilanciamento del carico Internet (classico) nel portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="02994-103">Get started creating an Internet facing load balancer (classic) in the Azure classic portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="02994-104">Portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="02994-104">Azure classic portal</span></span>](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [<span data-ttu-id="02994-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="02994-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [<span data-ttu-id="02994-106">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="02994-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [<span data-ttu-id="02994-107">Servizi cloud di Azure</span><span class="sxs-lookup"><span data-stu-id="02994-107">Azure Cloud Services</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="02994-108">Prima di iniziare a usare le risorse di Azure, è importante comprendere che Azure al momento offre due modelli di distribuzione, la distribuzione classica e Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="02994-108">Before you work with Azure resources, it's important to understand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="02994-109">È importante comprendere i [modelli e strumenti di distribuzione](../azure-classic-rm.md) prima di lavorare con le risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="02994-109">Make sure you understand [deployment models and tools](../azure-classic-rm.md) before you work with any Azure resource.</span></span> <span data-ttu-id="02994-110">È possibile visualizzare la documentazione relativa a diversi strumenti facendo clic sulle schede nella parte superiore di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="02994-110">You can view the documentation for different tools by clicking the tabs at the top of this article.</span></span> <span data-ttu-id="02994-111">In questo articolo viene illustrato il modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="02994-111">This article covers the classic deployment model.</span></span> <span data-ttu-id="02994-112">Vedere [Informazioni su come creare un servizio di bilanciamento del carico Internet in Gestione risorse di Azure](load-balancer-get-started-internet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="02994-112">You can also [Learn how to create an Internet facing load balancer using Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="set-up-an-internet-facing-load-balancer-for-virtual-machines"></a><span data-ttu-id="02994-113">Configurazione del servizio di bilanciamento del carico Internet per le macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="02994-113">Set up an Internet-facing load balancer for virtual machines</span></span>

<span data-ttu-id="02994-114">Per bilanciare il carico del traffico di rete Internet tra le macchine virtuali di un servizio cloud, è necessario creare un set con carico bilanciato.</span><span class="sxs-lookup"><span data-stu-id="02994-114">In order to load balance network traffic from the Internet across the virtual machines of a cloud service, you must create a load-balanced set.</span></span> <span data-ttu-id="02994-115">Questa procedura presuppone che le macchine virtuali siano già state create e che si trovino tutte nello stesso servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="02994-115">This procedure assumes that you have already created the virtual machines and that they are all within the same cloud service.</span></span>

<span data-ttu-id="02994-116">**Per configurare un set con carico bilanciato per le macchine virtuali**</span><span class="sxs-lookup"><span data-stu-id="02994-116">**To configure a load-balanced set for virtual machines**</span></span>

1. <span data-ttu-id="02994-117">Nel portale di Azure classico fare clic su **Macchine virtuali**e quindi sul nome di una macchina virtuale nel set con carico bilanciato.</span><span class="sxs-lookup"><span data-stu-id="02994-117">In the Azure classic portal, click **Virtual Machines**, and then click the name of a virtual machine in the load-balanced set.</span></span>
2. <span data-ttu-id="02994-118">Far clic su **Endpoint** e selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="02994-118">Click **Endpoints**, and then click **Add**.</span></span>
3. <span data-ttu-id="02994-119">Nella pagina **Aggiungi un endpoint a una macchina virtuale** fare clic sulla freccia destra.</span><span class="sxs-lookup"><span data-stu-id="02994-119">On the **Add an endpoint to a virtual machine** page, click the right arrow.</span></span>
4. <span data-ttu-id="02994-120">Nella pagina **Specificare i dettagli dell'endpoint** :</span><span class="sxs-lookup"><span data-stu-id="02994-120">On the **Specify the details of the endpoint** page:</span></span>

   * <span data-ttu-id="02994-121">In **Nome**digitare un nome per l'endpoint o selezionarne uno dall'elenco di endpoint predefiniti per i protocolli comuni.</span><span class="sxs-lookup"><span data-stu-id="02994-121">In **Name**, type a name for the endpoint or select the name from the list of predefined endpoints for common protocols.</span></span>
   * <span data-ttu-id="02994-122">In **Protocol**selezionare il protocollo richiesto dal tipo di endpoint, ossia TCP o UDP.</span><span class="sxs-lookup"><span data-stu-id="02994-122">In **Protocol**, select the protocol required by the type of endpoint, either TCP or UDP, as needed.</span></span>
   * <span data-ttu-id="02994-123">In **Porta pubblica e Porta privata**digitare il numero di porta da utilizzare per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="02994-123">In **Public Port and Private Port**, type the port numbers that you want the virtual machine to use, as needed.</span></span> <span data-ttu-id="02994-124">È possibile usare le regole relative a porte private e firewall sulla macchina virtuale per reindirizzare il traffico in modo appropriato per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="02994-124">You can use the private port and firewall rules on the virtual machine to redirect traffic in a way that is appropriate for your application.</span></span> <span data-ttu-id="02994-125">La porta privata può essere uguale alla porta pubblica.</span><span class="sxs-lookup"><span data-stu-id="02994-125">The private port can be the same as the public port.</span></span> <span data-ttu-id="02994-126">Per un endpoint per il traffico Web (HTTP), è ad esempio possibile assegnare la porta 80 sia come porta pubblica che privata.</span><span class="sxs-lookup"><span data-stu-id="02994-126">For example, for an endpoint for web (HTTP) traffic, you could assign port 80 to both the public and private port.</span></span>

5. <span data-ttu-id="02994-127">Selezionare **Create a load-balanced set**e quindi fare clic sulla freccia destra.</span><span class="sxs-lookup"><span data-stu-id="02994-127">Select **Create a load-balanced set**, and then click the right arrow.</span></span>
6. <span data-ttu-id="02994-128">Nella pagina **Configura il set con carico bilanciato** immettere un nome per il set con carico bilanciato e quindi assegnare i valori per il comportamento del probe del servizio di bilanciamento del carico di Azure.</span><span class="sxs-lookup"><span data-stu-id="02994-128">On the **Configure the load-balanced set** page, type a name for the load-balanced set, and then assign the values for probe behavior of the Azure Load Balancer.</span></span> <span data-ttu-id="02994-129">Il servizio di bilanciamento del carico usa i probe per determinare se le macchine virtuali del set con carico bilanciato sono disponibili a ricevere traffico in ingresso.</span><span class="sxs-lookup"><span data-stu-id="02994-129">The Load Balancer uses probes to determine if the virtual machines in the load-balanced set are available to receive incoming traffic.</span></span>
7. <span data-ttu-id="02994-130">Fare clic sul segno di spunta per creare l'endpoint con carico bilanciato.</span><span class="sxs-lookup"><span data-stu-id="02994-130">Click the check mark to create the load-balanced endpoint.</span></span> <span data-ttu-id="02994-131">Sarà visualizzato **Sì** nella colonna **Nome del set con carico bilanciato** della pagina **Endpoint** relativa alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="02994-131">You will see **Yes** in the **Load-balanced set name** column of the **Endpoints** page for the virtual machine.</span></span>
8. <span data-ttu-id="02994-132">Nel portale fare clic su **Macchine virtuali**, selezionare il nome di una macchina virtuale aggiuntiva nel set con carico bilanciato, fare clic su **Endpoint** e infine su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="02994-132">In the portal, click **Virtual Machines**, click the name of an additional virtual machine in the load-balanced set, click **Endpoints**, and then click **Add**.</span></span>
9. <span data-ttu-id="02994-133">Nella pagina **Aggiungi un endpoint a una macchina virtuale** fare clic su **Aggiungi un endpoint a un set con carico bilanciato esistente**, selezionare il nome del set con carico bilanciato e fare clic sulla freccia destra.</span><span class="sxs-lookup"><span data-stu-id="02994-133">On the **Add an endpoint to a virtual machine** page, click **Add endpoint to an existing load-balanced set**, select the name of the load-balanced set, and then click the right arrow.</span></span>
10. <span data-ttu-id="02994-134">Nella pagina **Specificare i dettagli dell'endpoint** digitare un nome per l'endpoint e quindi fare clic sul segno di spunta.</span><span class="sxs-lookup"><span data-stu-id="02994-134">On the **Specify the details of the endpoint** page, type a name for the endpoint, and then click the check mark.</span></span>

<span data-ttu-id="02994-135">Per le macchine virtuali aggiuntive nel set con carico bilanciato, ripetere i passaggi da 8 a 10.</span><span class="sxs-lookup"><span data-stu-id="02994-135">For the additional virtual machines in the load-balanced set, repeat steps 8-10.</span></span>

## <a name="next-steps"></a><span data-ttu-id="02994-136">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="02994-136">Next steps</span></span>

[<span data-ttu-id="02994-137">Introduzione alla configurazione del bilanciamento del carico interno</span><span class="sxs-lookup"><span data-stu-id="02994-137">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="02994-138">Configurare una modalità di distribuzione del servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="02994-138">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="02994-139">Configurare le impostazioni del timeout di inattività TCP per il bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="02994-139">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
