---
title: Creare un servizio di bilanciamento del carico interno - Portale di Azure | Documentazione Microsoft
description: Informazioni su come creare un servizio di bilanciamento del carico interno in Resource Manager con il portale di Azure
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
ms.openlocfilehash: 8fbe9d5d04d745de51e0e41516d6c12683c98637
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-internal-load-balancer-in-the-azure-portal"></a><span data-ttu-id="82e36-103">Creare un servizio di bilanciamento del carico interno nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="82e36-103">Create an Internal load balancer in the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="82e36-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="82e36-104">Azure Portal</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [<span data-ttu-id="82e36-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="82e36-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [<span data-ttu-id="82e36-106">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="82e36-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [<span data-ttu-id="82e36-107">Modello</span><span class="sxs-lookup"><span data-stu-id="82e36-107">Template</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="82e36-108">Azure offre due modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="82e36-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="82e36-109">Questo articolo illustra l'uso del modello di distribuzione Resource Manager che Microsoft consiglia di usare invece del [modello di distribuzione classica](load-balancer-get-started-ilb-classic-ps.md) per le distribuzioni più recenti.</span><span class="sxs-lookup"><span data-stu-id="82e36-109">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the [classic deployment model](load-balancer-get-started-ilb-classic-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="get-started-creating-an-internal-load-balancer-using-azure-portal"></a><span data-ttu-id="82e36-110">Introduzione alla creazione di un servizio di bilanciamento del carico interno tramite il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="82e36-110">Get started creating an Internal load balancer using Azure portal</span></span>

<span data-ttu-id="82e36-111">Per creare un servizio di bilanciamento del carico interno dal portale di Azure, seguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="82e36-111">Use the following steps to create an internal load balancer from the Azure Portal.</span></span>

1. <span data-ttu-id="82e36-112">Aprire un browser, passare al [portale di Azure](http://portal.azure.com) e accedere con l'account Azure.</span><span class="sxs-lookup"><span data-stu-id="82e36-112">Open a browser, navigate to the [Azure portal](http://portal.azure.com), and sign in with your Azure account.</span></span>
2. <span data-ttu-id="82e36-113">Sul lato superiore sinistro della schermata fare clic su **Nuovo** > **Rete** > **Servizio di bilanciamento del carico**.</span><span class="sxs-lookup"><span data-stu-id="82e36-113">In the upper left hand side of the screen, click **New** > **Networking** > **Load balancer**.</span></span>
3. <span data-ttu-id="82e36-114">Nel pannello **Crea servizio di bilanciamento del carico** immettere un **nome** per il servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="82e36-114">In the **Create load balancer** blade, enter a **Name** for your load balancer.</span></span>
4. <span data-ttu-id="82e36-115">In **Schema** fare clic su **Interno**.</span><span class="sxs-lookup"><span data-stu-id="82e36-115">Under **Scheme**, click **Internal**.</span></span>
5. <span data-ttu-id="82e36-116">Fare clic su **Rete virtuale**, quindi selezionare la rete virtuale in cui si desidera creare il servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="82e36-116">Click **Virtual network**, and then select the virtual network where you want to create the load balancer.</span></span>

   > [!NOTE]
   > <span data-ttu-id="82e36-117">Se la rete virtuale che si desidera usare non viene visualizzata, controllare il **Percorso** per il servizio di bilanciamento del carico e modificarlo di conseguenza.</span><span class="sxs-lookup"><span data-stu-id="82e36-117">If you do not see the virtual network you want to use, check the **Location** you are using for the load balancer, and change it accordingly.</span></span>

6. <span data-ttu-id="82e36-118">Fare clic su **Subnet**e scegliere la subnet in cui creare il servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="82e36-118">Click **Subnet**, and then select the subnet where you want to create the load balancer.</span></span>
7. <span data-ttu-id="82e36-119">In **Assegnazione indirizzo IP** fare clic su **Dinamico** o **Statico**, a seconda che si voglia un servizio di bilanciamento del carico con indirizzo IP fisso, cioè statico, o dinamico.</span><span class="sxs-lookup"><span data-stu-id="82e36-119">Under **IP address assignment**, click either **Dynamic** or **Static**, depending on whether you want the IP address for the load balancer to be fixed (static) or not.</span></span>

   > [!NOTE]
   > <span data-ttu-id="82e36-120">Se si sceglie un indirizzo IP statico, sarà necessario fornire un indirizzo per il servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="82e36-120">If you select to use a static IP address, you will have to provide an address for the load balancer.</span></span>

8. <span data-ttu-id="82e36-121">In **Gruppo di risorse** specificare il nome di un nuovo gruppo di risorse per il servizio di bilanciamento del carico oppure fare clic su **Seleziona esistente** e scegliere un gruppo di risorse esistente.</span><span class="sxs-lookup"><span data-stu-id="82e36-121">Under **Resource group** either specify the name of a new resource group for the load balancer, or click **select existing** and select an existing resource group.</span></span>
9. <span data-ttu-id="82e36-122">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="82e36-122">Click **Create**.</span></span>

## <a name="configure-load-balancing-rules"></a><span data-ttu-id="82e36-123">Configurare le regole del servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="82e36-123">Configure load balancing rules</span></span>

<span data-ttu-id="82e36-124">Dopo la creazione del servizio di bilanciamento di carico, individuare la risorsa di bilanciamento del carico per configurarla.</span><span class="sxs-lookup"><span data-stu-id="82e36-124">After the load balancer creation, navigate to the load balancer resource to configure it.</span></span>
<span data-ttu-id="82e36-125">Prima di configurare una regola di bilanciamento del carico, è necessario innanzitutto configurare un pool di indirizzi back-end e un probe.</span><span class="sxs-lookup"><span data-stu-id="82e36-125">You need to configure first a back-end address pool and a probe before configuring a load balancing rule.</span></span>

### <a name="step-1-configure-a-back-end-pool"></a><span data-ttu-id="82e36-126">Passaggio 1: Configurare un pool back-end</span><span class="sxs-lookup"><span data-stu-id="82e36-126">Step 1: Configure a back-end pool</span></span>

1. <span data-ttu-id="82e36-127">Nel portale di Azure fare clic su **Sfoglia** > **Servizi di bilanciamento del carico** e fare clic sul servizio di bilanciamento del carico creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="82e36-127">In the Azure portal, click **Browse** > **Load balancers**, and then click the load balancer you created above.</span></span>
2. <span data-ttu-id="82e36-128">Nel pannello **Impostazioni** fare clic su **Pool back-end**.</span><span class="sxs-lookup"><span data-stu-id="82e36-128">In the **Settings** blade, click **Backend pools**.</span></span>
3. <span data-ttu-id="82e36-129">Nel pannello **Pool di indirizzi back-end** fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="82e36-129">In the **Backend address pools** blade, click **Add**.</span></span>
4. <span data-ttu-id="82e36-130">Nel pannello **Aggiungi pool back-end** immettere un **nome** per il pool back-end e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="82e36-130">In the **Add backend pool** blade, enter a **Name** for the backend pool, and then click **OK**.</span></span>

### <a name="step-2-configure-a-probe"></a><span data-ttu-id="82e36-131">Passaggio 2: Configurare un probe</span><span class="sxs-lookup"><span data-stu-id="82e36-131">Step 2: Configure a probe</span></span>

1. <span data-ttu-id="82e36-132">Nel portale di Azure fare clic su **Sfoglia** > **Servizi di bilanciamento del carico** e fare clic sul servizio di bilanciamento del carico creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="82e36-132">In the Azure portal, click **Browse** > **Load balancers**, and then click the load balancer you created above.</span></span>
2. <span data-ttu-id="82e36-133">Nel pannello **Impostazioni** fare clic su **Probe**.</span><span class="sxs-lookup"><span data-stu-id="82e36-133">In the **Settings** blade, click **Probes**.</span></span>
3. <span data-ttu-id="82e36-134">Nel pannello **Probe** fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="82e36-134">In the **Probes**  blade, click **Add**.</span></span>
4. <span data-ttu-id="82e36-135">Nel pannello **Aggiungi probe** immettere un **nome** per il probe.</span><span class="sxs-lookup"><span data-stu-id="82e36-135">In the **Add probe** blade, enter a **Name** for the probe.</span></span>
5. <span data-ttu-id="82e36-136">In **Protocollo** selezionare **HTTP** per i siti Web o **TCP** per le altre applicazioni basate su TCP.</span><span class="sxs-lookup"><span data-stu-id="82e36-136">Under **Protocol**, select **HTTP** (for web sites) or **TCP** (for other TCP based applications).</span></span>
6. <span data-ttu-id="82e36-137">In **Porta**specificare la porta da usare per accedere al probe.</span><span class="sxs-lookup"><span data-stu-id="82e36-137">Under **Port**, specify the port to use when accessing the probe.</span></span>
7. <span data-ttu-id="82e36-138">Solo per i probe HTTP, in **Percorso** specificare il percorso da usare come probe.</span><span class="sxs-lookup"><span data-stu-id="82e36-138">Under **Path** (for HTTP probes only), specify the path to use as a probe.</span></span>
8. <span data-ttu-id="82e36-139">In **Intervallo** specificare la frequenza di probe per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="82e36-139">Under **Interval** specify how frequently to probe the application.</span></span>
9. <span data-ttu-id="82e36-140">In **Soglia di non integrità**specificare il numero di tentativi con esito negativo ammessi prima che la macchina virtuale back-end sia contrassegnata come danneggiata.</span><span class="sxs-lookup"><span data-stu-id="82e36-140">Under **Unhealthy threshold**, specify how many attempts should fail before the backend virtual machine is marked as unhealthy.</span></span>
10. <span data-ttu-id="82e36-141">Fare clic su **OK** per creare il probe.</span><span class="sxs-lookup"><span data-stu-id="82e36-141">Click **OK** to create probe.</span></span>

### <a name="step-3-configure-load-balancing-rules"></a><span data-ttu-id="82e36-142">Passaggio 3: Configurare le regole del servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="82e36-142">Step 3: Configure load balancing rules</span></span>

1. <span data-ttu-id="82e36-143">Nel portale di Azure fare clic su **Sfoglia** > **Servizi di bilanciamento del carico** e fare clic sul servizio di bilanciamento del carico creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="82e36-143">In the Azure portal, click **Browse** > **Load balancers**, and then click the load balancer you created above.</span></span>
2. <span data-ttu-id="82e36-144">Nel pannello **Impostazioni** fare clic su **Regole di bilanciamento del carico**.</span><span class="sxs-lookup"><span data-stu-id="82e36-144">In the **Settings** blade, click **Load balancing rules**.</span></span>
3. <span data-ttu-id="82e36-145">Nel pannello **Regole di bilanciamento del carico** fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="82e36-145">In the **Load balancing rules** blade, click **Add**.</span></span>
4. <span data-ttu-id="82e36-146">Nel pannello **Aggiungi regola di bilanciamento del carico** immettere un **nome** per la regola.</span><span class="sxs-lookup"><span data-stu-id="82e36-146">In the **Add load balancing rule** blade, enter a **Name** for the rule.</span></span>
5. <span data-ttu-id="82e36-147">In **Protocollo** selezionare **HTTP** per i siti Web o **TCP** per le altre applicazioni basate su TCP.</span><span class="sxs-lookup"><span data-stu-id="82e36-147">Under **Protocol**, select **HTTP** (for web sites) or **TCP** (for other TCP based applications).</span></span>
6. <span data-ttu-id="82e36-148">In **Porta** specificare la porta del servizio di bilanciamento del carico a cui i client devono connettersi.</span><span class="sxs-lookup"><span data-stu-id="82e36-148">Under **Port**, specify the port clients connect to in the load balancer.</span></span>
7. <span data-ttu-id="82e36-149">In **Porta back-end** specificare la porta da usare nel pool di back-end. La porta del servizio di bilanciamento del carico e la porta di back-end sono solitamente la stessa.</span><span class="sxs-lookup"><span data-stu-id="82e36-149">Under **Backend port**, specify the port to be used in the backend pool (usually, the load balancer port and the backend port are the same).</span></span>
8. <span data-ttu-id="82e36-150">In **Pool back-end**selezionare il pool back-end creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="82e36-150">Under **Backend pool**, select the backend pool you created above.</span></span>
9. <span data-ttu-id="82e36-151">In **Salvataggio permanente sessione** selezionare la modalità di salvataggio delle sessioni.</span><span class="sxs-lookup"><span data-stu-id="82e36-151">Under **Session persistence**, select how you want sessions to persist.</span></span>
10. <span data-ttu-id="82e36-152">In **Timeout di inattività (minuti)**specificare il timeout di inattività.</span><span class="sxs-lookup"><span data-stu-id="82e36-152">Under **Idle timeout (minutes)**, specify the idle timeout.</span></span>
11. <span data-ttu-id="82e36-153">In **IP mobile (Direct Server Return)** fare clic su **Disabilitato** o **Abilitato**.</span><span class="sxs-lookup"><span data-stu-id="82e36-153">Under **Floating IP (direct server return)**, click **Disabled** or **Enabled**.</span></span>
12. <span data-ttu-id="82e36-154">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="82e36-154">Click **OK**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="82e36-155">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="82e36-155">Next steps</span></span>

[<span data-ttu-id="82e36-156">Configurare una modalità di distribuzione del servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="82e36-156">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="82e36-157">Configurare le impostazioni del timeout di inattività TCP per il bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="82e36-157">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

