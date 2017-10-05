---
title: Creare farm di SharePoint Server in Azure | Documentazione Microsoft
description: Creare rapidamente una nuova farm di SharePoint 2013 o SharePoint 2016 in Azure tramite il marketplace del portale di Azure.
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
ms.openlocfilehash: 00648ee35962b22fb7eeceaa6d9df7305c801abf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-sharepoint-server-farms-using-the-azure-portal-marketplace"></a><span data-ttu-id="46e7e-103">Creare farm di SharePoint Server usando il marketplace del portale di Azure</span><span class="sxs-lookup"><span data-stu-id="46e7e-103">Create SharePoint server farms using the Azure portal marketplace</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="sharepoint-2013-farms"></a><span data-ttu-id="46e7e-104">Farm SharePoint 2013</span><span class="sxs-lookup"><span data-stu-id="46e7e-104">SharePoint 2013 farms</span></span>
<span data-ttu-id="46e7e-105">Con il marketplace del portale di Microsoft Azure, è possibile creare rapidamente delle farm pre-configurate di SharePoint Server 2013.</span><span class="sxs-lookup"><span data-stu-id="46e7e-105">With the Microsoft Azure portal marketplace, you can quickly create pre-configured SharePoint Server 2013 farms.</span></span> <span data-ttu-id="46e7e-106">Ciò consente di risparmiare una notevole quantità di tempo in caso si necessiti di una farm di SharePoint di base o a disponibilità elevata per un ambiente di sviluppo e test o in caso si stia valutando l'opportunità di usare SharePoint Server 2013 come soluzione per la collaborazione all'interno dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="46e7e-106">This can save you a lot of time when you need a basic or high-availability SharePoint farm for a dev/test environment or if you are evaluating SharePoint Server 2013 as a collaboration solution for your organization.</span></span>

> [!NOTE]
> <span data-ttu-id="46e7e-107">L'elemento **SharePoint Farm** nella sezione Marketplace del portale di Azure è stato rimosso.</span><span class="sxs-lookup"><span data-stu-id="46e7e-107">The **SharePoint Server Farm** item in the Azure Marketplace of the Azure portal has been removed.</span></span> <span data-ttu-id="46e7e-108">È stato sostituito dagli elementi **SharePoint 2013 non-HA Farm** e **SharePoint 2013 HA Farm**.</span><span class="sxs-lookup"><span data-stu-id="46e7e-108">It has been replaced with the **SharePoint 2013 non-HA Farm** and **SharePoint 2013 HA Farm** items.</span></span>
>
>

<span data-ttu-id="46e7e-109">La farm di SharePoint di base è costituita da tre macchine virtuali in questa configurazione.</span><span class="sxs-lookup"><span data-stu-id="46e7e-109">The basic SharePoint farm consists of three virtual machines in this configuration.</span></span>

![sharepointfarm](./media/sharepoint-farm/Non-HAFarm.png)

<span data-ttu-id="46e7e-111">È possibile usare questa configurazione di farm per un'installazione semplificata per lo sviluppo di app SharePoint o per la prima valutazione di SharePoint 2013.</span><span class="sxs-lookup"><span data-stu-id="46e7e-111">You can use this farm configuration for a simplified setup for SharePoint app development or your first-time evaluation of SharePoint 2013.</span></span>

<span data-ttu-id="46e7e-112">Per creare la farm di SharePoint (tre server) di base:</span><span class="sxs-lookup"><span data-stu-id="46e7e-112">To create the basic (three-server) SharePoint farm:</span></span>

1. <span data-ttu-id="46e7e-113">Fare clic [qui](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-nonha/)</span><span class="sxs-lookup"><span data-stu-id="46e7e-113">Click [here](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-nonha/).</span></span>
2. <span data-ttu-id="46e7e-114">Fare clic su **Distribuisci**.</span><span class="sxs-lookup"><span data-stu-id="46e7e-114">Click **Deploy**.</span></span>
3. <span data-ttu-id="46e7e-115">Nel riquadro **SharePoint 2013 non-HA Farm**, fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="46e7e-115">On the **SharePoint 2013 non-HA Farm** pane, click **Create**.</span></span>
4. <span data-ttu-id="46e7e-116">Specificare le impostazioni nei passaggi del riquadro **Creare una SharePoint 2013 non-HA Farm** e quindi fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="46e7e-116">Specify settings on the steps of the **Create SharePoint 2013 non-HA Farm** pane, and then click **Create**.</span></span>

<span data-ttu-id="46e7e-117">La farm di SharePoint a disponibilità elevata è costituita da nove macchine virtuali in questa configurazione.</span><span class="sxs-lookup"><span data-stu-id="46e7e-117">The high-availability SharePoint farm consists of nine virtual machines in this configuration.</span></span>

![sharepointfarm](./media/sharepoint-farm/HAFarm.png)

<span data-ttu-id="46e7e-119">È possibile usare questa configurazione di farm per testare carichi client più elevati, la disponibilità elevata del sito di SharePoint esterno e i gruppi di disponibilità AlwaysOn di SQL Server per una farm di SharePoint.</span><span class="sxs-lookup"><span data-stu-id="46e7e-119">You can use this farm configuration to test higher client loads, high availability of the external SharePoint site, and SQL Server AlwaysOn Availability Groups for a SharePoint farm.</span></span> <span data-ttu-id="46e7e-120">È anche possibile usare questa configurazione per lo sviluppo di app SharePoint in un ambiente a disponibilità elevata.</span><span class="sxs-lookup"><span data-stu-id="46e7e-120">You can also use this configuration for SharePoint app development in a high-availability environment.</span></span>

<span data-ttu-id="46e7e-121">Per creare la farm di SharePoint a disponibilità elevata (nove server):</span><span class="sxs-lookup"><span data-stu-id="46e7e-121">To create the high-availability (nine-server) SharePoint farm:</span></span>

1. <span data-ttu-id="46e7e-122">Fare clic [qui](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-ha/)</span><span class="sxs-lookup"><span data-stu-id="46e7e-122">Click [here](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-ha/).</span></span>
2. <span data-ttu-id="46e7e-123">Fare clic su **Distribuisci**.</span><span class="sxs-lookup"><span data-stu-id="46e7e-123">Click **Deploy**.</span></span>
3. <span data-ttu-id="46e7e-124">Nel riquadro **SharePoint 2013 HA Farm**, fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="46e7e-124">On the **SharePoint 2013 HA Farm** pane, click **Create**.</span></span>
4. <span data-ttu-id="46e7e-125">Specificare le impostazioni nei sette passaggi del riquadro di creazione di **SharePoint 2013 HA Farm** e quindi fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="46e7e-125">Specify settings on the seven steps of the **Create SharePoint 2013 HA Farm** pane, and then click **Create**.</span></span>

> [!NOTE]
> <span data-ttu-id="46e7e-126">Non è possibile creare l'elemento **SharePoint 2013 non-HA Farm** o **SharePoint 2013 HA Farm** con una versione di prova gratuita di Azure.</span><span class="sxs-lookup"><span data-stu-id="46e7e-126">You cannot create the **SharePoint 2013 non-HA Farm** or **SharePoint 2013 HA Farm** with an Azure Free Trial.</span></span>
>
>

<span data-ttu-id="46e7e-127">Il portale di Azure crea entrambe queste farm in una rete virtuale solo cloud con una presenza Web con connessione Internet.</span><span class="sxs-lookup"><span data-stu-id="46e7e-127">The Azure portal creates both of these farms in a cloud-only virtual network with an Internet-facing web presence.</span></span> <span data-ttu-id="46e7e-128">Non esiste alcuna connessione VPN o ExpressRoute da sito a sito alla rete dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="46e7e-128">There is no site-to-site VPN or ExpressRoute connection back to your organization network.</span></span>

> [!NOTE]
> <span data-ttu-id="46e7e-129">Quando si creano le farm di SharePoint di base o a disponibilità elevata tramite il portale di Azure, non è possibile specificare un gruppo di risorse esistente.</span><span class="sxs-lookup"><span data-stu-id="46e7e-129">When you create the basic or high-availability SharePoint farms using the Azure portal, you cannot specify an existing resource group.</span></span> <span data-ttu-id="46e7e-130">Per superare questa limitazione, creare tali farm con Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="46e7e-130">To work around this limitation, create these farms with Azure PowerShell.</span></span> <span data-ttu-id="46e7e-131">Per altre informazioni, vedere [Creare farm di sviluppo e di testing di SharePoint 2013 con Azure PowerShell](https://technet.microsoft.com/library/mt743093.aspx#powershell).</span><span class="sxs-lookup"><span data-stu-id="46e7e-131">For more information, see [Create SharePoint 2013 dev/test farms with Azure PowerShell](https://technet.microsoft.com/library/mt743093.aspx#powershell).</span></span>
>
>

## <a name="sharepoint-2016-farms"></a><span data-ttu-id="46e7e-132">Farm SharePoint 2016</span><span class="sxs-lookup"><span data-stu-id="46e7e-132">SharePoint 2016 farms</span></span>
<span data-ttu-id="46e7e-133">Vedere [questo articolo](https://technet.microsoft.com/library/mt723354.aspx) per istruzioni sulla creazione della seguente farm di SharePoint Server 2016 a server singolo.</span><span class="sxs-lookup"><span data-stu-id="46e7e-133">See [this article](https://technet.microsoft.com/library/mt723354.aspx) for the instructions to build the following single-server SharePoint Server 2016 farm.</span></span>

![sharepointfarm](./media/sharepoint-farm/SP2016Farm.png)

## <a name="managing-the-sharepoint-farms"></a><span data-ttu-id="46e7e-135">Gestire le farm di SharePoint</span><span class="sxs-lookup"><span data-stu-id="46e7e-135">Managing the SharePoint farms</span></span>
<span data-ttu-id="46e7e-136">È possibile amministrare i server di queste farm tramite connessioni Desktop Remoto.</span><span class="sxs-lookup"><span data-stu-id="46e7e-136">You can administer the servers of these farms through Remote Desktop connections.</span></span> <span data-ttu-id="46e7e-137">Per altre informazioni, vedere [Accedere alla macchina virtuale](quick-create-portal.md#connect-to-virtual-machine).</span><span class="sxs-lookup"><span data-stu-id="46e7e-137">For more information, see [Log on to the virtual machine](quick-create-portal.md#connect-to-virtual-machine).</span></span>

<span data-ttu-id="46e7e-138">Dal sito Amministrazione centrale di SharePoint è possibile configurare i siti personali, le applicazioni di SharePoint e altre funzionalità.</span><span class="sxs-lookup"><span data-stu-id="46e7e-138">From the Central Administration SharePoint site, you can configure My sites, SharePoint applications, and other functionality.</span></span> <span data-ttu-id="46e7e-139">Per altre informazioni, vedere [Configurare SharePoint](http://technet.microsoft.com/library/ee836142.aspx).</span><span class="sxs-lookup"><span data-stu-id="46e7e-139">For more information, see [Configure SharePoint](http://technet.microsoft.com/library/ee836142.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="46e7e-140">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="46e7e-140">Next steps</span></span>
* <span data-ttu-id="46e7e-141">Altre [configurazioni di SharePoint](https://technet.microsoft.com/library/dn635309.aspx) nei servizi dell'infrastruttura di Azure.</span><span class="sxs-lookup"><span data-stu-id="46e7e-141">Discover additional [SharePoint configurations](https://technet.microsoft.com/library/dn635309.aspx) in Azure infrastructure services.</span></span>
