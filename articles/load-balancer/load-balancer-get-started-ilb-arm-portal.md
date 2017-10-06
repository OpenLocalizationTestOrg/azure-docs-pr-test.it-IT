---
title: aaaCreate un bilanciamento del carico interno - portale di Azure | Documenti Microsoft
description: Informazioni su come toocreate un interno bilanciamento del carico di gestione risorse utilizzando hello portale di Azure
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 1ac14fb9-8d14-4892-bfe6-8bc74c48ae2c
ms.service: load-balancer
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 80124217a84857b542eb41cb814ec97234176dd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internal-load-balancer-in-hello-azure-portal"></a><span data-ttu-id="22e53-103">Creare un servizio di bilanciamento del carico interno in hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="22e53-103">Create an Internal load balancer in hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="22e53-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="22e53-104">Azure Portal</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [<span data-ttu-id="22e53-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="22e53-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [<span data-ttu-id="22e53-106">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="22e53-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [<span data-ttu-id="22e53-107">Modello</span><span class="sxs-lookup"><span data-stu-id="22e53-107">Template</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="22e53-108">Azure offre due modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="22e53-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="22e53-109">In questo articolo viene illustrato l'utilizzo modello di distribuzione di gestione delle risorse hello, si consiglia di per la maggior parte delle nuove distribuzioni anziché hello [modello di distribuzione classica](load-balancer-get-started-ilb-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="22e53-109">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](load-balancer-get-started-ilb-classic-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="get-started-creating-an-internal-load-balancer-using-azure-portal"></a><span data-ttu-id="22e53-110">Introduzione alla creazione di un servizio di bilanciamento del carico interno tramite il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="22e53-110">Get started creating an Internal load balancer using Azure portal</span></span>

<span data-ttu-id="22e53-111">Utilizzare hello seguendo i passaggi toocreate un bilanciamento del carico interno dalla hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="22e53-111">Use hello following steps toocreate an internal load balancer from hello Azure Portal.</span></span>

1. <span data-ttu-id="22e53-112">Aprire un browser, passare toohello [portale di Azure](http://portal.azure.com)e accedere con l'account di Azure.</span><span class="sxs-lookup"><span data-stu-id="22e53-112">Open a browser, navigate toohello [Azure portal](http://portal.azure.com), and sign in with your Azure account.</span></span>
2. <span data-ttu-id="22e53-113">Nel lato superiore sinistro di hello della schermata ciao, fare clic su **New** > **rete** > **bilanciamento del carico**.</span><span class="sxs-lookup"><span data-stu-id="22e53-113">In hello upper left hand side of hello screen, click **New** > **Networking** > **Load balancer**.</span></span>
3. <span data-ttu-id="22e53-114">In hello **Crea servizio di bilanciamento del carico** pannello, immettere un **nome** per il bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="22e53-114">In hello **Create load balancer** blade, enter a **Name** for your load balancer.</span></span>
4. <span data-ttu-id="22e53-115">In **Schema** fare clic su **Interno**.</span><span class="sxs-lookup"><span data-stu-id="22e53-115">Under **Scheme**, click **Internal**.</span></span>
5. <span data-ttu-id="22e53-116">Fare clic su **rete virtuale**, e quindi selezionare hello rete virtuale in cui si desidera toocreate bilanciamento del carico di hello.</span><span class="sxs-lookup"><span data-stu-id="22e53-116">Click **Virtual network**, and then select hello virtual network where you want toocreate hello load balancer.</span></span>

   > [!NOTE]
   > <span data-ttu-id="22e53-117">Se non si desidera toouse la rete virtuale hello, verificare hello **percorso** utilizza servizio di bilanciamento del carico hello e modificarla di conseguenza.</span><span class="sxs-lookup"><span data-stu-id="22e53-117">If you do not see hello virtual network you want toouse, check hello **Location** you are using for hello load balancer, and change it accordingly.</span></span>

6. <span data-ttu-id="22e53-118">Fare clic su **Subnet**, quindi selezionare subnet hello in cui si desidera toocreate bilanciamento del carico di hello.</span><span class="sxs-lookup"><span data-stu-id="22e53-118">Click **Subnet**, and then select hello subnet where you want toocreate hello load balancer.</span></span>
7. <span data-ttu-id="22e53-119">In **assegnazione di indirizzi IP**, fare clic su **dinamica** o **statico**, a seconda se si desidera l'indirizzo IP hello per hello carico bilanciamento toobe fisso (statico) o meno.</span><span class="sxs-lookup"><span data-stu-id="22e53-119">Under **IP address assignment**, click either **Dynamic** or **Static**, depending on whether you want hello IP address for hello load balancer toobe fixed (static) or not.</span></span>

   > [!NOTE]
   > <span data-ttu-id="22e53-120">Se si seleziona un indirizzo IP statico toouse, sarà necessario tooprovide un indirizzo di bilanciamento del carico hello.</span><span class="sxs-lookup"><span data-stu-id="22e53-120">If you select toouse a static IP address, you will have tooprovide an address for hello load balancer.</span></span>

8. <span data-ttu-id="22e53-121">In **gruppo di risorse** specificare hello nome di un nuovo gruppo di risorse di bilanciamento del carico hello, oppure fare clic su **selezionare esistente** e selezionare un gruppo di risorse esistente.</span><span class="sxs-lookup"><span data-stu-id="22e53-121">Under **Resource group** either specify hello name of a new resource group for hello load balancer, or click **select existing** and select an existing resource group.</span></span>
9. <span data-ttu-id="22e53-122">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="22e53-122">Click **Create**.</span></span>

## <a name="configure-load-balancing-rules"></a><span data-ttu-id="22e53-123">Configurare le regole del servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="22e53-123">Configure load balancing rules</span></span>

<span data-ttu-id="22e53-124">Creazione del servizio di bilanciamento di carico dopo hello, passare tooconfigure risorsa del servizio di bilanciamento carico di toohello è.</span><span class="sxs-lookup"><span data-stu-id="22e53-124">After hello load balancer creation, navigate toohello load balancer resource tooconfigure it.</span></span>
<span data-ttu-id="22e53-125">È necessario tooconfigure prima un pool di indirizzi back-end e un probe prima di configurare una regola di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="22e53-125">You need tooconfigure first a back-end address pool and a probe before configuring a load balancing rule.</span></span>

### <a name="step-1-configure-a-back-end-pool"></a><span data-ttu-id="22e53-126">Passaggio 1: Configurare un pool back-end</span><span class="sxs-lookup"><span data-stu-id="22e53-126">Step 1: Configure a back-end pool</span></span>

1. <span data-ttu-id="22e53-127">Nel portale di Azure hello, fare clic su **Sfoglia** > **bilanciamenti del carico**, quindi fare clic su bilanciamento del carico hello creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="22e53-127">In hello Azure portal, click **Browse** > **Load balancers**, and then click hello load balancer you created above.</span></span>
2. <span data-ttu-id="22e53-128">In hello **impostazioni** pannello, fare clic su **pool back-end**.</span><span class="sxs-lookup"><span data-stu-id="22e53-128">In hello **Settings** blade, click **Backend pools**.</span></span>
3. <span data-ttu-id="22e53-129">In hello **pool di indirizzi back-end** pannello, fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="22e53-129">In hello **Backend address pools** blade, click **Add**.</span></span>
4. <span data-ttu-id="22e53-130">In hello **aggiungere pool back-end** pannello, immettere un **nome** per pool back-end hello e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="22e53-130">In hello **Add backend pool** blade, enter a **Name** for hello backend pool, and then click **OK**.</span></span>

### <a name="step-2-configure-a-probe"></a><span data-ttu-id="22e53-131">Passaggio 2: Configurare un probe</span><span class="sxs-lookup"><span data-stu-id="22e53-131">Step 2: Configure a probe</span></span>

1. <span data-ttu-id="22e53-132">Nel portale di Azure hello, fare clic su **Sfoglia** > **bilanciamenti del carico**, quindi fare clic su bilanciamento del carico hello creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="22e53-132">In hello Azure portal, click **Browse** > **Load balancers**, and then click hello load balancer you created above.</span></span>
2. <span data-ttu-id="22e53-133">In hello **impostazioni** pannello, fare clic su **probe**.</span><span class="sxs-lookup"><span data-stu-id="22e53-133">In hello **Settings** blade, click **Probes**.</span></span>
3. <span data-ttu-id="22e53-134">In hello **probe** pannello, fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="22e53-134">In hello **Probes**  blade, click **Add**.</span></span>
4. <span data-ttu-id="22e53-135">In hello **Aggiungi probe** pannello, immettere un **nome** per il probe hello.</span><span class="sxs-lookup"><span data-stu-id="22e53-135">In hello **Add probe** blade, enter a **Name** for hello probe.</span></span>
5. <span data-ttu-id="22e53-136">In **Protocollo** selezionare **HTTP** per i siti Web o **TCP** per le altre applicazioni basate su TCP.</span><span class="sxs-lookup"><span data-stu-id="22e53-136">Under **Protocol**, select **HTTP** (for web sites) or **TCP** (for other TCP based applications).</span></span>
6. <span data-ttu-id="22e53-137">In **porta**, specificare hello porta toouse quando si accede a probe hello.</span><span class="sxs-lookup"><span data-stu-id="22e53-137">Under **Port**, specify hello port toouse when accessing hello probe.</span></span>
7. <span data-ttu-id="22e53-138">In **percorso** (per HTTP ricerche solo), specificare hello percorso toouse come un probe.</span><span class="sxs-lookup"><span data-stu-id="22e53-138">Under **Path** (for HTTP probes only), specify hello path toouse as a probe.</span></span>
8. <span data-ttu-id="22e53-139">In **intervallo** specificare la frequenza con cui tooprobe hello dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="22e53-139">Under **Interval** specify how frequently tooprobe hello application.</span></span>
9. <span data-ttu-id="22e53-140">In **soglia non integra**, specificare il numero di tentativi devono avere esito negativo prima macchina virtuale back-end di hello è contrassegnato come danneggiato.</span><span class="sxs-lookup"><span data-stu-id="22e53-140">Under **Unhealthy threshold**, specify how many attempts should fail before hello backend virtual machine is marked as unhealthy.</span></span>
10. <span data-ttu-id="22e53-141">Fare clic su **OK** toocreate probe.</span><span class="sxs-lookup"><span data-stu-id="22e53-141">Click **OK** toocreate probe.</span></span>

### <a name="step-3-configure-load-balancing-rules"></a><span data-ttu-id="22e53-142">Passaggio 3: Configurare le regole del servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="22e53-142">Step 3: Configure load balancing rules</span></span>

1. <span data-ttu-id="22e53-143">Nel portale di Azure hello, fare clic su **Sfoglia** > **bilanciamenti del carico**, quindi fare clic su bilanciamento del carico hello creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="22e53-143">In hello Azure portal, click **Browse** > **Load balancers**, and then click hello load balancer you created above.</span></span>
2. <span data-ttu-id="22e53-144">In hello **impostazioni** pannello, fare clic su **regole di bilanciamento del carico**.</span><span class="sxs-lookup"><span data-stu-id="22e53-144">In hello **Settings** blade, click **Load balancing rules**.</span></span>
3. <span data-ttu-id="22e53-145">In hello **regole di bilanciamento del carico** pannello, fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="22e53-145">In hello **Load balancing rules** blade, click **Add**.</span></span>
4. <span data-ttu-id="22e53-146">In hello **regola di bilanciamento del carico di Aggiungi** pannello, immettere un **nome** per regola hello.</span><span class="sxs-lookup"><span data-stu-id="22e53-146">In hello **Add load balancing rule** blade, enter a **Name** for hello rule.</span></span>
5. <span data-ttu-id="22e53-147">In **Protocollo** selezionare **HTTP** per i siti Web o **TCP** per le altre applicazioni basate su TCP.</span><span class="sxs-lookup"><span data-stu-id="22e53-147">Under **Protocol**, select **HTTP** (for web sites) or **TCP** (for other TCP based applications).</span></span>
6. <span data-ttu-id="22e53-148">In **porta**, specificare hello porta client si connettono tooin bilanciamento del carico di hello.</span><span class="sxs-lookup"><span data-stu-id="22e53-148">Under **Port**, specify hello port clients connect tooin hello load balancer.</span></span>
7. <span data-ttu-id="22e53-149">In **porta back-end**, specificare hello porta toobe utilizzati nel pool back-end hello (in genere, la porta del servizio di bilanciamento carico di hello e la porta back-end hello sono hello stesso).</span><span class="sxs-lookup"><span data-stu-id="22e53-149">Under **Backend port**, specify hello port toobe used in hello backend pool (usually, hello load balancer port and hello backend port are hello same).</span></span>
8. <span data-ttu-id="22e53-150">In **pool back-end**, selezionare il pool back-end hello creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="22e53-150">Under **Backend pool**, select hello backend pool you created above.</span></span>
9. <span data-ttu-id="22e53-151">In **persistenza della sessione**, selezionare il metodo toopersist sessioni.</span><span class="sxs-lookup"><span data-stu-id="22e53-151">Under **Session persistence**, select how you want sessions toopersist.</span></span>
10. <span data-ttu-id="22e53-152">In **il timeout di inattività (minuti)**, specificare il timeout di inattività hello.</span><span class="sxs-lookup"><span data-stu-id="22e53-152">Under **Idle timeout (minutes)**, specify hello idle timeout.</span></span>
11. <span data-ttu-id="22e53-153">In **IP mobile (Direct Server Return)** fare clic su **Disabilitato** o **Abilitato**.</span><span class="sxs-lookup"><span data-stu-id="22e53-153">Under **Floating IP (direct server return)**, click **Disabled** or **Enabled**.</span></span>
12. <span data-ttu-id="22e53-154">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="22e53-154">Click **OK**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="22e53-155">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="22e53-155">Next steps</span></span>

[<span data-ttu-id="22e53-156">Configurare una modalità di distribuzione del servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="22e53-156">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="22e53-157">Configurare le impostazioni del timeout di inattività TCP per il bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="22e53-157">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

