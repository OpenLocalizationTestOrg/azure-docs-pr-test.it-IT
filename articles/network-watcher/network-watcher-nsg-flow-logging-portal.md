---
title: registri aaaManage rete sicurezza gruppo flusso con il Watcher di rete di Azure | Documenti Microsoft
description: Questa pagina viene illustrato come flusso del gruppo di sicurezza di rete toomanage accede Watcher di rete di Azure
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
ms.openlocfilehash: fb250337ab9d1a0c0d0d3569c00bc221dd102a3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-network-security-group-flow-logs-in-hello-azure-portal"></a><span data-ttu-id="797e6-103">Gestire i registri del flusso di rete sicurezza gruppo nel portale di Azure hello</span><span class="sxs-lookup"><span data-stu-id="797e6-103">Manage network security group flow logs in hello Azure portal</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="797e6-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="797e6-104">Azure portal</span></span>](network-watcher-nsg-flow-logging-portal.md)
> - [<span data-ttu-id="797e6-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="797e6-105">PowerShell</span></span>](network-watcher-nsg-flow-logging-powershell.md)
> - [<span data-ttu-id="797e6-106">Interfaccia della riga di comando 1.0</span><span class="sxs-lookup"><span data-stu-id="797e6-106">CLI 1.0</span></span>](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [<span data-ttu-id="797e6-107">Interfaccia della riga di comando 2.0</span><span class="sxs-lookup"><span data-stu-id="797e6-107">CLI 2.0</span></span>](network-watcher-nsg-flow-logging-cli.md)
> - [<span data-ttu-id="797e6-108">API REST</span><span class="sxs-lookup"><span data-stu-id="797e6-108">REST API</span></span>](network-watcher-nsg-flow-logging-rest.md)

<span data-ttu-id="797e6-109">Registri flusso gruppo di sicurezza rete sono una funzionalità del controllo di rete che consente di tooview informazioni sul traffico IP in entrata e in uscita tramite un gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="797e6-109">Network security group flow logs are a feature of Network Watcher that enables you tooview information about ingress and egress IP traffic through a network security group.</span></span> <span data-ttu-id="797e6-110">Questi log di flusso sono scritti in formato JSON e contengono informazioni importanti, tra cui:</span><span class="sxs-lookup"><span data-stu-id="797e6-110">These flow logs are written in JSON format and provide important information, including:</span></span> 

- <span data-ttu-id="797e6-111">Flussi in ingresso e in uscita in base a ciascuna regola.</span><span class="sxs-lookup"><span data-stu-id="797e6-111">Outbound and inbound flows on a per-rule basis.</span></span>
- <span data-ttu-id="797e6-112">scheda di rete che hello flusso Hello si applica a.</span><span class="sxs-lookup"><span data-stu-id="797e6-112">hello NIC that hello flow applies to.</span></span>
- <span data-ttu-id="797e6-113">5 tuple informazioni sul flusso di hello (origine/destinazione IP, porta di origine/destinazione, protocol).</span><span class="sxs-lookup"><span data-stu-id="797e6-113">5-tuple information about hello flow (source/destination IP, source/destination port, protocol).</span></span>
- <span data-ttu-id="797e6-114">Indica se il traffico è stato consentito o negato.</span><span class="sxs-lookup"><span data-stu-id="797e6-114">Information about whether traffic was allowed or denied.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="797e6-115">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="797e6-115">Before you begin</span></span>

<span data-ttu-id="797e6-116">Questo scenario si presuppone che si sono già stati seguiti i passaggi di hello in [creare un'istanza del controllo di rete](network-watcher-create.md).</span><span class="sxs-lookup"><span data-stu-id="797e6-116">This scenario assumes you have already followed hello steps in [Create a Network Watcher instance](network-watcher-create.md).</span></span> <span data-ttu-id="797e6-117">scenario di Hello si presuppone inoltre che si dispone di un gruppo di risorse con una macchina virtuale valida.</span><span class="sxs-lookup"><span data-stu-id="797e6-117">hello scenario also assumes that a you have a resource group with a valid virtual machine.</span></span>

## <a name="register-insights-provider"></a><span data-ttu-id="797e6-118">Registrare il provider di Insight</span><span class="sxs-lookup"><span data-stu-id="797e6-118">Register Insights provider</span></span>

<span data-ttu-id="797e6-119">Per il flusso di registrazione toowork hello correttamente, **Insights** provider deve essere registrato.</span><span class="sxs-lookup"><span data-stu-id="797e6-119">For flow logging toowork successfully, hello **Microsoft.Insights** provider must be registered.</span></span> <span data-ttu-id="797e6-120">provider di hello tooregister, hello take alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="797e6-120">tooregister hello provider, take hello following steps:</span></span> 

1. <span data-ttu-id="797e6-121">Andare troppo**sottoscrizioni**, quindi selezionare hello sottoscrizione per cui si desidera tooenable flusso registri.</span><span class="sxs-lookup"><span data-stu-id="797e6-121">Go too**Subscriptions**, and then select hello subscription for which you want tooenable flow logs.</span></span> 
2. <span data-ttu-id="797e6-122">In hello **sottoscrizione** pannello seleziona **i provider di risorse**.</span><span class="sxs-lookup"><span data-stu-id="797e6-122">On hello **Subscription** blade, select **Resource Providers**.</span></span> 
3. <span data-ttu-id="797e6-123">Esaminare hello elenco dei provider e verificare che hello **Insights** provider è registrato.</span><span class="sxs-lookup"><span data-stu-id="797e6-123">Look at hello list of providers, and verify that hello **microsoft.insights** provider is registered.</span></span> <span data-ttu-id="797e6-124">In caso contrario selezionare **Registra**.</span><span class="sxs-lookup"><span data-stu-id="797e6-124">If not, then select **Register**.</span></span>

![Visualizzare i provider][providers]

## <a name="enable-flow-logs"></a><span data-ttu-id="797e6-126">Abilitare i log di flusso</span><span class="sxs-lookup"><span data-stu-id="797e6-126">Enable flow logs</span></span>

<span data-ttu-id="797e6-127">Questi passaggi vengono illustrati il processo di hello di abilitazione del flusso di log in un gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="797e6-127">These steps take you through hello process of enabling flow logs on a network security group.</span></span>

### <a name="step-1"></a><span data-ttu-id="797e6-128">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="797e6-128">Step 1</span></span>

<span data-ttu-id="797e6-129">Passare l'istanza di tooa Watcher di rete e quindi selezionare **NSG flusso registra**.</span><span class="sxs-lookup"><span data-stu-id="797e6-129">Go tooa Network Watcher instance, and then select **NSG Flow logs**.</span></span>

![Panoramica dei log di flusso][1]

### <a name="step-2"></a><span data-ttu-id="797e6-131">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="797e6-131">Step 2</span></span>

<span data-ttu-id="797e6-132">Selezionare un gruppo di sicurezza di rete dall'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="797e6-132">Select a network security group from hello list.</span></span>

![Panoramica dei log di flusso][2]

### <a name="step-3"></a><span data-ttu-id="797e6-134">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="797e6-134">Step 3</span></span> 

<span data-ttu-id="797e6-135">In hello **delle impostazioni dei log flusso** pannello, impostare lo stato di hello troppo**su**e quindi configurare un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="797e6-135">On hello **Flow logs settings** blade, set hello status too**On**, and then configure a storage account.</span></span>  <span data-ttu-id="797e6-136">Al termine, fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="797e6-136">When you're done, select **OK**.</span></span> <span data-ttu-id="797e6-137">Selezionare quindi **Salva**.</span><span class="sxs-lookup"><span data-stu-id="797e6-137">Then select **Save**.</span></span>

![Panoramica dei log di flusso][3]

## <a name="download-flow-logs"></a><span data-ttu-id="797e6-139">Scaricare i log di flusso</span><span class="sxs-lookup"><span data-stu-id="797e6-139">Download flow logs</span></span>

<span data-ttu-id="797e6-140">I log di flusso vengono salvati in un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="797e6-140">Flow logs are saved in a storage account.</span></span> <span data-ttu-id="797e6-141">Scaricare il tooview registri flusso li.</span><span class="sxs-lookup"><span data-stu-id="797e6-141">Download your flow logs tooview them.</span></span>

### <a name="step-1"></a><span data-ttu-id="797e6-142">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="797e6-142">Step 1</span></span>

<span data-ttu-id="797e6-143">Selezionare i log di flusso, toodownload **è possibile scaricare i log di flusso dagli account di archiviazione configurato**.</span><span class="sxs-lookup"><span data-stu-id="797e6-143">toodownload flow logs, select **You can download flow logs from configured storage accounts**.</span></span> <span data-ttu-id="797e6-144">Questo passaggio consente di visualizzare account di archiviazione tooa in cui è possibile scegliere quali toodownload log.</span><span class="sxs-lookup"><span data-stu-id="797e6-144">This step takes you tooa storage account view where you can choose which logs toodownload.</span></span>

![Impostazioni dei log di flusso][4]

### <a name="step-2"></a><span data-ttu-id="797e6-146">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="797e6-146">Step 2</span></span>

<span data-ttu-id="797e6-147">Passare toohello account di archiviazione corretto.</span><span class="sxs-lookup"><span data-stu-id="797e6-147">Go toohello correct storage account.</span></span> <span data-ttu-id="797e6-148">Selezionare quindi **Contenitori** > **insights-log-networksecuritygroupflowevent**.</span><span class="sxs-lookup"><span data-stu-id="797e6-148">Then select **Containers** > **insights-log-networksecuritygroupflowevent**.</span></span>

![Impostazioni dei log di flusso][5]

### <a name="step-3"></a><span data-ttu-id="797e6-150">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="797e6-150">Step 3</span></span>

<span data-ttu-id="797e6-151">Passare toohello del percorso del Registro di flusso hello, selezionarlo e quindi selezionare **scaricare**.</span><span class="sxs-lookup"><span data-stu-id="797e6-151">Go toohello location of hello flow log, select it, and then select **Download**.</span></span>

![Impostazioni dei log di flusso][6]

<span data-ttu-id="797e6-153">Per informazioni sulla struttura di hello del log di hello, visitare [Cenni preliminari sul registro del flusso di rete sicurezza gruppo](network-watcher-nsg-flow-logging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="797e6-153">For information about hello structure of hello log, visit [Network security group flow log overview](network-watcher-nsg-flow-logging-overview.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="797e6-154">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="797e6-154">Next steps</span></span>

<span data-ttu-id="797e6-155">Informazioni su come troppo[visualizzare i log di flusso NSG con Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="797e6-155">Learn how too[visualize your NSG flow logs with PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md).</span></span>

<!-- Image references -->
[1]: ./media/network-watcher-nsg-flow-logging-portal/figure1.png
[2]: ./media/network-watcher-nsg-flow-logging-portal/figure2.png
[3]: ./media/network-watcher-nsg-flow-logging-portal/figure3.png
[4]: ./media/network-watcher-nsg-flow-logging-portal/figure4.png
[5]: ./media/network-watcher-nsg-flow-logging-portal/figure5.png
[6]: ./media/network-watcher-nsg-flow-logging-portal/figure6.png
[providers]: ./media/network-watcher-nsg-flow-logging-portal/providers.png
