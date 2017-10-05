---
title: Gestire i log di flusso del gruppo di sicurezza di rete con Network Watcher di Azure | Microsoft Docs
description: Questa pagina illustra come gestire i log di flusso del gruppo di sicurezza di rete in Network Watcher di Azure
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 01606cbf-d70b-40ad-bc1d-f03bb642e0af
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 41cb5ffab9bd3a3bed75ffdb6a7383ca1690f810
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="manage-network-security-group-flow-logs-in-the-azure-portal"></a><span data-ttu-id="e182f-103">Gestire i log di flusso del gruppo di sicurezza di rete nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="e182f-103">Manage network security group flow logs in the Azure portal</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="e182f-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="e182f-104">Azure portal</span></span>](network-watcher-nsg-flow-logging-portal.md)
> - [<span data-ttu-id="e182f-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e182f-105">PowerShell</span></span>](network-watcher-nsg-flow-logging-powershell.md)
> - [<span data-ttu-id="e182f-106">Interfaccia della riga di comando 1.0</span><span class="sxs-lookup"><span data-stu-id="e182f-106">CLI 1.0</span></span>](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [<span data-ttu-id="e182f-107">Interfaccia della riga di comando 2.0</span><span class="sxs-lookup"><span data-stu-id="e182f-107">CLI 2.0</span></span>](network-watcher-nsg-flow-logging-cli.md)
> - [<span data-ttu-id="e182f-108">API REST</span><span class="sxs-lookup"><span data-stu-id="e182f-108">REST API</span></span>](network-watcher-nsg-flow-logging-rest.md)

<span data-ttu-id="e182f-109">I log di flusso del gruppo di sicurezza di rete sono una funzionalità di Network Watcher che consente di visualizzare le informazioni sul traffico IP in entrata e in uscita tramite un gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="e182f-109">Network security group flow logs are a feature of Network Watcher that enables you to view information about ingress and egress IP traffic through a network security group.</span></span> <span data-ttu-id="e182f-110">Questi log di flusso sono scritti in formato JSON e contengono informazioni importanti, tra cui:</span><span class="sxs-lookup"><span data-stu-id="e182f-110">These flow logs are written in JSON format and provide important information, including:</span></span> 

- <span data-ttu-id="e182f-111">Flussi in ingresso e in uscita in base a ciascuna regola.</span><span class="sxs-lookup"><span data-stu-id="e182f-111">Outbound and inbound flows on a per-rule basis.</span></span>
- <span data-ttu-id="e182f-112">La scheda di interfaccia di rete che si applica al flusso.</span><span class="sxs-lookup"><span data-stu-id="e182f-112">The NIC that the flow applies to.</span></span>
- <span data-ttu-id="e182f-113">Informazioni a 5 tuple sul flusso, IP di origine/destinazione, porta di origine/destinazione, protocollo.</span><span class="sxs-lookup"><span data-stu-id="e182f-113">5-tuple information about the flow (source/destination IP, source/destination port, protocol).</span></span>
- <span data-ttu-id="e182f-114">Indica se il traffico è stato consentito o negato.</span><span class="sxs-lookup"><span data-stu-id="e182f-114">Information about whether traffic was allowed or denied.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="e182f-115">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="e182f-115">Before you begin</span></span>

<span data-ttu-id="e182f-116">Questo scenario presuppone il completamento dei passaggi descritti in [Creare un'istanza di Azure Network Watcher](network-watcher-create.md).</span><span class="sxs-lookup"><span data-stu-id="e182f-116">This scenario assumes you have already followed the steps in [Create a Network Watcher instance](network-watcher-create.md).</span></span> <span data-ttu-id="e182f-117">Lo scenario presuppone anche che l'utente possieda un gruppo di risorse con una macchina virtuale valida.</span><span class="sxs-lookup"><span data-stu-id="e182f-117">The scenario also assumes that a you have a resource group with a valid virtual machine.</span></span>

## <a name="register-insights-provider"></a><span data-ttu-id="e182f-118">Registrare il provider Insights</span><span class="sxs-lookup"><span data-stu-id="e182f-118">Register Insights provider</span></span>

<span data-ttu-id="e182f-119">Per il corretto funzionamento della registrazione dei flussi, è necessario registrare il provider **Microsoft.Insights**.</span><span class="sxs-lookup"><span data-stu-id="e182f-119">For flow logging to work successfully, the **Microsoft.Insights** provider must be registered.</span></span> <span data-ttu-id="e182f-120">Registrare il provider seguendo la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="e182f-120">To register the provider, take the following steps:</span></span> 

1. <span data-ttu-id="e182f-121">Passare a **Sottoscrizioni** e selezionare la sottoscrizione per la quale si vuole abilitare i log dei flussi.</span><span class="sxs-lookup"><span data-stu-id="e182f-121">Go to **Subscriptions**, and then select the subscription for which you want to enable flow logs.</span></span> 
2. <span data-ttu-id="e182f-122">Nel pannello **Sottoscrizione** selezionare **Provider di risorse**.</span><span class="sxs-lookup"><span data-stu-id="e182f-122">On the **Subscription** blade, select **Resource Providers**.</span></span> 
3. <span data-ttu-id="e182f-123">Osservare l'elenco di provider e verificare che il provider **microsoft.insights** sia registrato.</span><span class="sxs-lookup"><span data-stu-id="e182f-123">Look at the list of providers, and verify that the **microsoft.insights** provider is registered.</span></span> <span data-ttu-id="e182f-124">In caso contrario selezionare **Registra**.</span><span class="sxs-lookup"><span data-stu-id="e182f-124">If not, then select **Register**.</span></span>

![Visualizzare i provider][providers]

## <a name="enable-flow-logs"></a><span data-ttu-id="e182f-126">Abilitare i log di flusso</span><span class="sxs-lookup"><span data-stu-id="e182f-126">Enable flow logs</span></span>

<span data-ttu-id="e182f-127">Questi passaggi descrivono il processo di abilitazione dei log di flusso in un gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="e182f-127">These steps take you through the process of enabling flow logs on a network security group.</span></span>

### <a name="step-1"></a><span data-ttu-id="e182f-128">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="e182f-128">Step 1</span></span>

<span data-ttu-id="e182f-129">Passare a un'istanza di Network Watcher e selezionare **Log del flusso del NSG**.</span><span class="sxs-lookup"><span data-stu-id="e182f-129">Go to a Network Watcher instance, and then select **NSG Flow logs**.</span></span>

![Panoramica dei log di flusso][1]

### <a name="step-2"></a><span data-ttu-id="e182f-131">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="e182f-131">Step 2</span></span>

<span data-ttu-id="e182f-132">Selezionare un gruppo di sicurezza di rete dall'elenco.</span><span class="sxs-lookup"><span data-stu-id="e182f-132">Select a network security group from the list.</span></span>

![Panoramica dei log di flusso][2]

### <a name="step-3"></a><span data-ttu-id="e182f-134">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="e182f-134">Step 3</span></span> 

<span data-ttu-id="e182f-135">Nel pannello **Impostazioni dei log dei flussi** impostare lo stato su **On** (Attivo) e configurare un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="e182f-135">On the **Flow logs settings** blade, set the status to **On**, and then configure a storage account.</span></span>  <span data-ttu-id="e182f-136">Al termine, fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="e182f-136">When you're done, select **OK**.</span></span> <span data-ttu-id="e182f-137">Selezionare quindi **Salva**.</span><span class="sxs-lookup"><span data-stu-id="e182f-137">Then select **Save**.</span></span>

![Panoramica dei log di flusso][3]

## <a name="download-flow-logs"></a><span data-ttu-id="e182f-139">Scaricare i log di flusso</span><span class="sxs-lookup"><span data-stu-id="e182f-139">Download flow logs</span></span>

<span data-ttu-id="e182f-140">I log di flusso vengono salvati in un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="e182f-140">Flow logs are saved in a storage account.</span></span> <span data-ttu-id="e182f-141">Scaricare i log di flusso per visualizzarli.</span><span class="sxs-lookup"><span data-stu-id="e182f-141">Download your flow logs to view them.</span></span>

### <a name="step-1"></a><span data-ttu-id="e182f-142">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="e182f-142">Step 1</span></span>

<span data-ttu-id="e182f-143">Per scaricare i log di flusso, fare clic su **È possibile scaricare i log dei flussi dagli account di archiviazione configurati**.</span><span class="sxs-lookup"><span data-stu-id="e182f-143">To download flow logs, select **You can download flow logs from configured storage accounts**.</span></span> <span data-ttu-id="e182f-144">Con questo passaggio si accede a una visualizzazione dell'account di archiviazione in cui è possibile scegliere i log per il download.</span><span class="sxs-lookup"><span data-stu-id="e182f-144">This step takes you to a storage account view where you can choose which logs to download.</span></span>

![Impostazioni dei log di flusso][4]

### <a name="step-2"></a><span data-ttu-id="e182f-146">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="e182f-146">Step 2</span></span>

<span data-ttu-id="e182f-147">Passare all'account di archiviazione corretto.</span><span class="sxs-lookup"><span data-stu-id="e182f-147">Go to the correct storage account.</span></span> <span data-ttu-id="e182f-148">Selezionare quindi **Contenitori** > **insights-log-networksecuritygroupflowevent**.</span><span class="sxs-lookup"><span data-stu-id="e182f-148">Then select **Containers** > **insights-log-networksecuritygroupflowevent**.</span></span>

![Impostazioni dei log di flusso][5]

### <a name="step-3"></a><span data-ttu-id="e182f-150">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="e182f-150">Step 3</span></span>

<span data-ttu-id="e182f-151">Passare al percorso del log di flusso, selezionarlo e quindi selezionare **Scarica**.</span><span class="sxs-lookup"><span data-stu-id="e182f-151">Go to the location of the flow log, select it, and then select **Download**.</span></span>

![Impostazioni dei log di flusso][6]

<span data-ttu-id="e182f-153">Per informazioni sulla struttura del log, leggere [Panoramica sul log di flusso del gruppo di sicurezza di rete](network-watcher-nsg-flow-logging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e182f-153">For information about the structure of the log, visit [Network security group flow log overview](network-watcher-nsg-flow-logging-overview.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e182f-154">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e182f-154">Next steps</span></span>

<span data-ttu-id="e182f-155">Informazioni su come [visualizzare i log di flusso NSG con Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="e182f-155">Learn how to [visualize your NSG flow logs with PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md).</span></span>

<!-- Image references -->
[1]: ./media/network-watcher-nsg-flow-logging-portal/figure1.png
[2]: ./media/network-watcher-nsg-flow-logging-portal/figure2.png
[3]: ./media/network-watcher-nsg-flow-logging-portal/figure3.png
[4]: ./media/network-watcher-nsg-flow-logging-portal/figure4.png
[5]: ./media/network-watcher-nsg-flow-logging-portal/figure5.png
[6]: ./media/network-watcher-nsg-flow-logging-portal/figure6.png
[providers]: ./media/network-watcher-nsg-flow-logging-portal/providers.png
