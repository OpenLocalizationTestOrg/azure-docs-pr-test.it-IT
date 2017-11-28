---
title: server farm di SharePoint aaaCreate in Azure | Documenti Microsoft
description: Creare rapidamente una nuova farm di SharePoint 2013 o SharePoint 2016 in Azure utilizzando hello Azure marketplace portale.
services: virtual-machines-windows
documentationcenter: 
author: JoeDavies-MSFT
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 89b124da-019d-4179-86dd-ad418d05a4f2
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/30/2016
ms.author: josephd
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d71c7177d9b99cf377bab767342508007285b452
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-sharepoint-server-farms-using-hello-azure-portal-marketplace"></a><span data-ttu-id="0a9d3-103">Creare una server farm di SharePoint utilizzando hello Azure marketplace portale</span><span class="sxs-lookup"><span data-stu-id="0a9d3-103">Create SharePoint server farms using hello Azure portal marketplace</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="sharepoint-2013-farms"></a><span data-ttu-id="0a9d3-104">Farm SharePoint 2013</span><span class="sxs-lookup"><span data-stu-id="0a9d3-104">SharePoint 2013 farms</span></span>
<span data-ttu-id="0a9d3-105">Con hello Microsoft Azure portale marketplace, è possibile creare rapidamente le farm di SharePoint Server 2013 preconfigurate.</span><span class="sxs-lookup"><span data-stu-id="0a9d3-105">With hello Microsoft Azure portal marketplace, you can quickly create pre-configured SharePoint Server 2013 farms.</span></span> <span data-ttu-id="0a9d3-106">Ciò consente di risparmiare una notevole quantità di tempo in caso si necessiti di una farm di SharePoint di base o a disponibilità elevata per un ambiente di sviluppo e test o in caso si stia valutando l'opportunità di usare SharePoint Server 2013 come soluzione per la collaborazione all'interno dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="0a9d3-106">This can save you a lot of time when you need a basic or high-availability SharePoint farm for a dev/test environment or if you are evaluating SharePoint Server 2013 as a collaboration solution for your organization.</span></span>

> [!NOTE]
> <span data-ttu-id="0a9d3-107">Hello **Server Farm di SharePoint** elemento hello Azure Marketplace di hello portale di Azure è stato rimosso.</span><span class="sxs-lookup"><span data-stu-id="0a9d3-107">hello **SharePoint Server Farm** item in hello Azure Marketplace of hello Azure portal has been removed.</span></span> <span data-ttu-id="0a9d3-108">È stata sostituita con hello **SharePoint 2013 non a disponibilità elevata Farm** e **Farm a disponibilità elevata di SharePoint 2013** elementi.</span><span class="sxs-lookup"><span data-stu-id="0a9d3-108">It has been replaced with hello **SharePoint 2013 non-HA Farm** and **SharePoint 2013 HA Farm** items.</span></span>
>
>

<span data-ttu-id="0a9d3-109">farm di SharePoint base Hello è costituita da tre macchine virtuali in questa configurazione.</span><span class="sxs-lookup"><span data-stu-id="0a9d3-109">hello basic SharePoint farm consists of three virtual machines in this configuration.</span></span>

![sharepointfarm](./media/sharepoint-farm/Non-HAFarm.png)

<span data-ttu-id="0a9d3-111">È possibile usare questa configurazione di farm per un'installazione semplificata per lo sviluppo di app SharePoint o per la prima valutazione di SharePoint 2013.</span><span class="sxs-lookup"><span data-stu-id="0a9d3-111">You can use this farm configuration for a simplified setup for SharePoint app development or your first-time evaluation of SharePoint 2013.</span></span>

<span data-ttu-id="0a9d3-112">toocreate hello base () SharePoint farm a tre server:</span><span class="sxs-lookup"><span data-stu-id="0a9d3-112">toocreate hello basic (three-server) SharePoint farm:</span></span>

1. <span data-ttu-id="0a9d3-113">Fare clic [qui](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-nonha/)</span><span class="sxs-lookup"><span data-stu-id="0a9d3-113">Click [here](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-nonha/).</span></span>
2. <span data-ttu-id="0a9d3-114">Fare clic su **Distribuisci**.</span><span class="sxs-lookup"><span data-stu-id="0a9d3-114">Click **Deploy**.</span></span>
3. <span data-ttu-id="0a9d3-115">In hello **SharePoint 2013 non a disponibilità elevata Farm** riquadro, fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="0a9d3-115">On hello **SharePoint 2013 non-HA Farm** pane, click **Create**.</span></span>
4. <span data-ttu-id="0a9d3-116">Specificare le impostazioni nei passaggi hello di hello **creare SharePoint 2013 non a disponibilità elevata Farm** riquadro e quindi fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="0a9d3-116">Specify settings on hello steps of hello **Create SharePoint 2013 non-HA Farm** pane, and then click **Create**.</span></span>

<span data-ttu-id="0a9d3-117">farm di SharePoint a disponibilità elevata Hello è costituito da nove macchine virtuali in questa configurazione.</span><span class="sxs-lookup"><span data-stu-id="0a9d3-117">hello high-availability SharePoint farm consists of nine virtual machines in this configuration.</span></span>

![sharepointfarm](./media/sharepoint-farm/HAFarm.png)

<span data-ttu-id="0a9d3-119">È possibile utilizzare questa farm configurazione tootest carichi più client elevati, disponibilità elevata del sito di SharePoint esterno hello e gruppi di disponibilità AlwaysOn di SQL Server per una farm di SharePoint.</span><span class="sxs-lookup"><span data-stu-id="0a9d3-119">You can use this farm configuration tootest higher client loads, high availability of hello external SharePoint site, and SQL Server AlwaysOn Availability Groups for a SharePoint farm.</span></span> <span data-ttu-id="0a9d3-120">È anche possibile usare questa configurazione per lo sviluppo di app SharePoint in un ambiente a disponibilità elevata.</span><span class="sxs-lookup"><span data-stu-id="0a9d3-120">You can also use this configuration for SharePoint app development in a high-availability environment.</span></span>

<span data-ttu-id="0a9d3-121">farm di SharePoint (nove server) a disponibilità elevata hello toocreate:</span><span class="sxs-lookup"><span data-stu-id="0a9d3-121">toocreate hello high-availability (nine-server) SharePoint farm:</span></span>

1. <span data-ttu-id="0a9d3-122">Fare clic [qui](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-ha/)</span><span class="sxs-lookup"><span data-stu-id="0a9d3-122">Click [here](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-ha/).</span></span>
2. <span data-ttu-id="0a9d3-123">Fare clic su **Distribuisci**.</span><span class="sxs-lookup"><span data-stu-id="0a9d3-123">Click **Deploy**.</span></span>
3. <span data-ttu-id="0a9d3-124">In hello **Farm a disponibilità elevata di SharePoint 2013** riquadro, fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="0a9d3-124">On hello **SharePoint 2013 HA Farm** pane, click **Create**.</span></span>
4. <span data-ttu-id="0a9d3-125">Specificare le impostazioni nei passaggi hello sette hello **creare a disponibilità elevata Farm di SharePoint 2013** riquadro e quindi fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="0a9d3-125">Specify settings on hello seven steps of hello **Create SharePoint 2013 HA Farm** pane, and then click **Create**.</span></span>

> [!NOTE]
> <span data-ttu-id="0a9d3-126">Non è possibile creare hello **SharePoint 2013 non a disponibilità elevata Farm** o **Farm a disponibilità elevata di SharePoint 2013** con una versione di valutazione gratuita di Azure.</span><span class="sxs-lookup"><span data-stu-id="0a9d3-126">You cannot create hello **SharePoint 2013 non-HA Farm** or **SharePoint 2013 HA Farm** with an Azure Free Trial.</span></span>
>
>

<span data-ttu-id="0a9d3-127">Hello portale di Azure crea entrambi questi farm in una rete virtuale solo cloud con una presenza web con connessione Internet.</span><span class="sxs-lookup"><span data-stu-id="0a9d3-127">hello Azure portal creates both of these farms in a cloud-only virtual network with an Internet-facing web presence.</span></span> <span data-ttu-id="0a9d3-128">È presente alcuna site-to-site VPN o ExpressRoute connessione back-tooyour organizzazione rete.</span><span class="sxs-lookup"><span data-stu-id="0a9d3-128">There is no site-to-site VPN or ExpressRoute connection back tooyour organization network.</span></span>

> [!NOTE]
> <span data-ttu-id="0a9d3-129">Quando si crea hello base o farm di SharePoint a disponibilità elevata utilizzando hello portale di Azure, è possibile specificare un gruppo di risorse esistente.</span><span class="sxs-lookup"><span data-stu-id="0a9d3-129">When you create hello basic or high-availability SharePoint farms using hello Azure portal, you cannot specify an existing resource group.</span></span> <span data-ttu-id="0a9d3-130">toowork risolvere questa limitazione, creare queste aziende con Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0a9d3-130">toowork around this limitation, create these farms with Azure PowerShell.</span></span> <span data-ttu-id="0a9d3-131">Per altre informazioni, vedere [Creare farm di sviluppo e di testing di SharePoint 2013 con Azure PowerShell](https://technet.microsoft.com/library/mt743093.aspx#powershell).</span><span class="sxs-lookup"><span data-stu-id="0a9d3-131">For more information, see [Create SharePoint 2013 dev/test farms with Azure PowerShell](https://technet.microsoft.com/library/mt743093.aspx#powershell).</span></span>
>
>

## <a name="sharepoint-2016-farms"></a><span data-ttu-id="0a9d3-132">Farm SharePoint 2016</span><span class="sxs-lookup"><span data-stu-id="0a9d3-132">SharePoint 2016 farms</span></span>
<span data-ttu-id="0a9d3-133">Vedere [questo articolo](https://technet.microsoft.com/library/mt723354.aspx) per hello toobuild di istruzioni hello seguente a server singolo SharePoint Server 2016 farm.</span><span class="sxs-lookup"><span data-stu-id="0a9d3-133">See [this article](https://technet.microsoft.com/library/mt723354.aspx) for hello instructions toobuild hello following single-server SharePoint Server 2016 farm.</span></span>

![sharepointfarm](./media/sharepoint-farm/SP2016Farm.png)

## <a name="managing-hello-sharepoint-farms"></a><span data-ttu-id="0a9d3-135">La gestione di farm di SharePoint hello</span><span class="sxs-lookup"><span data-stu-id="0a9d3-135">Managing hello SharePoint farms</span></span>
<span data-ttu-id="0a9d3-136">È possibile amministrare il server di hello di queste aziende tramite le connessioni Desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="0a9d3-136">You can administer hello servers of these farms through Remote Desktop connections.</span></span> <span data-ttu-id="0a9d3-137">Per ulteriori informazioni, vedere [accedere alla macchina virtuale toohello](quick-create-portal.md#connect-to-virtual-machine).</span><span class="sxs-lookup"><span data-stu-id="0a9d3-137">For more information, see [Log on toohello virtual machine](quick-create-portal.md#connect-to-virtual-machine).</span></span>

<span data-ttu-id="0a9d3-138">Dal sito di SharePoint di amministrazione centrale hello, è possibile configurare i siti, applicazioni di SharePoint e altre funzionalità.</span><span class="sxs-lookup"><span data-stu-id="0a9d3-138">From hello Central Administration SharePoint site, you can configure My sites, SharePoint applications, and other functionality.</span></span> <span data-ttu-id="0a9d3-139">Per altre informazioni, vedere [Configurare SharePoint](http://technet.microsoft.com/library/ee836142.aspx).</span><span class="sxs-lookup"><span data-stu-id="0a9d3-139">For more information, see [Configure SharePoint](http://technet.microsoft.com/library/ee836142.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0a9d3-140">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0a9d3-140">Next steps</span></span>
* <span data-ttu-id="0a9d3-141">Altre [configurazioni di SharePoint](https://technet.microsoft.com/library/dn635309.aspx) nei servizi dell'infrastruttura di Azure.</span><span class="sxs-lookup"><span data-stu-id="0a9d3-141">Discover additional [SharePoint configurations](https://technet.microsoft.com/library/dn635309.aspx) in Azure infrastructure services.</span></span>
