---
title: bilanciamento del carico con una connessione Internet aaaCreate - portale di Azure classico | Documenti Microsoft
description: Informazioni su come toocreate un Internet rivolto al bilanciamento del carico in modello di distribuzione classica utilizzando hello portale di Azure classico
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
ms.openlocfilehash: 27b0d5af6e7b493fa94a9dfbfa260483ae95a2fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-classic-in-hello-azure-classic-portal"></a><span data-ttu-id="1b21e-103">Introduzione alla creazione di un bilanciamento del carico (classico) nel portale di Azure classico hello per Internet</span><span class="sxs-lookup"><span data-stu-id="1b21e-103">Get started creating an Internet facing load balancer (classic) in hello Azure classic portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="1b21e-104">portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="1b21e-104">Azure classic portal</span></span>](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [<span data-ttu-id="1b21e-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1b21e-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [<span data-ttu-id="1b21e-106">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="1b21e-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [<span data-ttu-id="1b21e-107">Servizi cloud di Azure</span><span class="sxs-lookup"><span data-stu-id="1b21e-107">Azure Cloud Services</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="1b21e-108">Prima di lavorare con le risorse di Azure, è importante toounderstand che Azure ha due modelli di distribuzione: Gestione risorse di Azure e classica.</span><span class="sxs-lookup"><span data-stu-id="1b21e-108">Before you work with Azure resources, it's important toounderstand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="1b21e-109">È importante comprendere i [modelli e strumenti di distribuzione](../azure-classic-rm.md) prima di lavorare con le risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="1b21e-109">Make sure you understand [deployment models and tools](../azure-classic-rm.md) before you work with any Azure resource.</span></span> <span data-ttu-id="1b21e-110">È possibile visualizzare la documentazione di hello per diversi strumenti facendo clic sulle schede hello nella parte superiore di hello di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="1b21e-110">You can view hello documentation for different tools by clicking hello tabs at hello top of this article.</span></span> <span data-ttu-id="1b21e-111">Questo articolo descrive il modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="1b21e-111">This article covers hello classic deployment model.</span></span> <span data-ttu-id="1b21e-112">È anche possibile [informazioni su come una connessione Internet toocreate bilanciamento del carico con Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="1b21e-112">You can also [Learn how toocreate an Internet facing load balancer using Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="set-up-an-internet-facing-load-balancer-for-virtual-machines"></a><span data-ttu-id="1b21e-113">Configurazione del servizio di bilanciamento del carico Internet per le macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="1b21e-113">Set up an Internet-facing load balancer for virtual machines</span></span>

<span data-ttu-id="1b21e-114">In ordine tooload bilanciare il traffico di rete da hello Internet tra macchine virtuali hello di un servizio cloud, è necessario creare un set con carico bilanciato.</span><span class="sxs-lookup"><span data-stu-id="1b21e-114">In order tooload balance network traffic from hello Internet across hello virtual machines of a cloud service, you must create a load-balanced set.</span></span> <span data-ttu-id="1b21e-115">Questa procedura si presuppone che sia stato già creato le macchine virtuali hello e che siano tutti all'interno di hello stesso servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="1b21e-115">This procedure assumes that you have already created hello virtual machines and that they are all within hello same cloud service.</span></span>

<span data-ttu-id="1b21e-116">**tooconfigure un set con carico bilanciato per le macchine virtuali**</span><span class="sxs-lookup"><span data-stu-id="1b21e-116">**tooconfigure a load-balanced set for virtual machines**</span></span>

1. <span data-ttu-id="1b21e-117">Nel portale di Azure classico hello, fare clic su **macchine virtuali**, quindi fare clic su nome hello di una macchina virtuale nel set di bilanciamento del carico hello.</span><span class="sxs-lookup"><span data-stu-id="1b21e-117">In hello Azure classic portal, click **Virtual Machines**, and then click hello name of a virtual machine in hello load-balanced set.</span></span>
2. <span data-ttu-id="1b21e-118">Far clic su **Endpoint** e selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="1b21e-118">Click **Endpoints**, and then click **Add**.</span></span>
3. <span data-ttu-id="1b21e-119">In hello **aggiungere una macchina virtuale di endpoint tooa** pagina, fare clic sulla freccia a destra di hello.</span><span class="sxs-lookup"><span data-stu-id="1b21e-119">On hello **Add an endpoint tooa virtual machine** page, click hello right arrow.</span></span>
4. <span data-ttu-id="1b21e-120">In hello **specificare hello i dettagli dell'endpoint hello** pagina:</span><span class="sxs-lookup"><span data-stu-id="1b21e-120">On hello **Specify hello details of hello endpoint** page:</span></span>

   * <span data-ttu-id="1b21e-121">In **nome**, digitare un nome per l'endpoint di hello o selezionare il nome di hello hello elenco degli endpoint predefiniti per i protocolli comuni.</span><span class="sxs-lookup"><span data-stu-id="1b21e-121">In **Name**, type a name for hello endpoint or select hello name from hello list of predefined endpoints for common protocols.</span></span>
   * <span data-ttu-id="1b21e-122">In **protocollo**, selezionare il protocollo di hello richiesto dal tipo di hello dell'endpoint, TCP o UDP, in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="1b21e-122">In **Protocol**, select hello protocol required by hello type of endpoint, either TCP or UDP, as needed.</span></span>
   * <span data-ttu-id="1b21e-123">In **porta pubblica e privata**, digitare i numeri di porta hello che si desidera hello toouse macchina virtuale, in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="1b21e-123">In **Public Port and Private Port**, type hello port numbers that you want hello virtual machine toouse, as needed.</span></span> <span data-ttu-id="1b21e-124">È possibile utilizzare la porta privata hello e regole del firewall al traffico tooredirect hello macchina virtuale in modo appropriato per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1b21e-124">You can use hello private port and firewall rules on hello virtual machine tooredirect traffic in a way that is appropriate for your application.</span></span> <span data-ttu-id="1b21e-125">porta privata Hello può essere hello come porta pubblica hello.</span><span class="sxs-lookup"><span data-stu-id="1b21e-125">hello private port can be hello same as hello public port.</span></span> <span data-ttu-id="1b21e-126">Per un endpoint per il traffico web (HTTP), ad esempio, è Impossibile assegnare la porta 80 tooboth hello porta pubblica e privata.</span><span class="sxs-lookup"><span data-stu-id="1b21e-126">For example, for an endpoint for web (HTTP) traffic, you could assign port 80 tooboth hello public and private port.</span></span>

5. <span data-ttu-id="1b21e-127">Selezionare **creare un set con carico bilanciato**e quindi fare clic sulla freccia a destra di hello.</span><span class="sxs-lookup"><span data-stu-id="1b21e-127">Select **Create a load-balanced set**, and then click hello right arrow.</span></span>
6. <span data-ttu-id="1b21e-128">In hello **configurare il set di bilanciamento del carico hello** pagina, digitare un nome per il set di bilanciamento del carico hello e quindi assegnare valori hello per il comportamento di probe di bilanciamento del carico di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="1b21e-128">On hello **Configure hello load-balanced set** page, type a name for hello load-balanced set, and then assign hello values for probe behavior of hello Azure Load Balancer.</span></span> <span data-ttu-id="1b21e-129">Hello bilanciamento del carico utilizza probe toodetermine se hello di macchine virtuali nel set di bilanciamento del carico hello sono disponibili tooreceive il traffico in entrata.</span><span class="sxs-lookup"><span data-stu-id="1b21e-129">hello Load Balancer uses probes toodetermine if hello virtual machines in hello load-balanced set are available tooreceive incoming traffic.</span></span>
7. <span data-ttu-id="1b21e-130">Fare clic su endpoint con bilanciamento del carico toocreate hello di hello segno di spunta.</span><span class="sxs-lookup"><span data-stu-id="1b21e-130">Click hello check mark toocreate hello load-balanced endpoint.</span></span> <span data-ttu-id="1b21e-131">Si noterà **Sì** in hello **nome set con carico bilanciato** colonna di hello **endpoint** pagina per la macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="1b21e-131">You will see **Yes** in hello **Load-balanced set name** column of hello **Endpoints** page for hello virtual machine.</span></span>
8. <span data-ttu-id="1b21e-132">Nel portale di hello, fare clic su **macchine virtuali**, fare clic sul nome di una macchina virtuale aggiuntiva nel set di bilanciamento del carico hello hello, fare clic su **endpoint**, quindi fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="1b21e-132">In hello portal, click **Virtual Machines**, click hello name of an additional virtual machine in hello load-balanced set, click **Endpoints**, and then click **Add**.</span></span>
9. <span data-ttu-id="1b21e-133">In hello **aggiungere una macchina virtuale di endpoint tooa** pagina, fare clic su **aggiungere set di bilanciamento del carico esistente di endpoint tooan**, selezionare il nome del set di bilanciamento del carico hello hello e quindi fare clic sulla freccia a destra di hello.</span><span class="sxs-lookup"><span data-stu-id="1b21e-133">On hello **Add an endpoint tooa virtual machine** page, click **Add endpoint tooan existing load-balanced set**, select hello name of hello load-balanced set, and then click hello right arrow.</span></span>
10. <span data-ttu-id="1b21e-134">In hello **specificare hello i dettagli dell'endpoint hello** pagina, digitare un nome per l'endpoint di hello e quindi fare clic su hello segno di spunta.</span><span class="sxs-lookup"><span data-stu-id="1b21e-134">On hello **Specify hello details of hello endpoint** page, type a name for hello endpoint, and then click hello check mark.</span></span>

<span data-ttu-id="1b21e-135">Per hello altre macchine virtuali nel set di bilanciamento del carico hello, ripetere i passaggi da 8 a 10.</span><span class="sxs-lookup"><span data-stu-id="1b21e-135">For hello additional virtual machines in hello load-balanced set, repeat steps 8-10.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1b21e-136">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1b21e-136">Next steps</span></span>

[<span data-ttu-id="1b21e-137">Introduzione alla configurazione del bilanciamento del carico interno</span><span class="sxs-lookup"><span data-stu-id="1b21e-137">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="1b21e-138">Configurare una modalità di distribuzione del servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="1b21e-138">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="1b21e-139">Configurare le impostazioni del timeout di inattività TCP per il bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="1b21e-139">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
