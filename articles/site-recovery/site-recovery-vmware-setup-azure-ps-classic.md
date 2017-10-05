---
title: " Gestire un server di elaborazione in esecuzione in Azure (versione classica) | Microsoft Docs"
description: Questo articolo descrive come configurare un server di elaborazione failback (versione classica) in Azure.
services: site-recovery
documentationcenter: 
author: AnoopVasudavan
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/29/2017
ms.author: anoopkv
ms.openlocfilehash: 479bbd207bcf715138c340f9e4d2634120bab85c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="manage-a-process-server-running-in-azure-classic"></a><span data-ttu-id="d5c97-103">Gestire un server di elaborazione in esecuzione in Azure (versione classica)</span><span class="sxs-lookup"><span data-stu-id="d5c97-103">Manage a Process Server running in Azure (Classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d5c97-104">Azure versione classica</span><span class="sxs-lookup"><span data-stu-id="d5c97-104">Azure Classic </span></span>](./site-recovery-vmware-setup-azure-ps-classic.md)
> * [<span data-ttu-id="d5c97-105">Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="d5c97-105">Resource Manager</span></span>](./site-recovery-vmware-setup-azure-ps-resource-manager.md)

<span data-ttu-id="d5c97-106">Durante il failback è consigliabile distribuire un server di elaborazione in Azure se è presente una latenza elevata tra la rete virtuale di Azure e la rete locale.</span><span class="sxs-lookup"><span data-stu-id="d5c97-106">During failback, it is recommended to deploy Process Server in Azure if there is high latency between the Azure Virtual Network and your on-premises network.</span></span> <span data-ttu-id="d5c97-107">Questo articolo descrive come impostare, configurare e gestire i server di elaborazione in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="d5c97-107">This article describes how you can set up, configure, and manage the process servers running in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="d5c97-108">Questo articolo è utile se è stato usato la versione classica come modello di distribuzione per le macchine virtuali durante il failover.</span><span class="sxs-lookup"><span data-stu-id="d5c97-108">This article is to be used if you used Classic as the deployment model for the virtual machines during failover.</span></span> <span data-ttu-id="d5c97-109">Se è stato usato il modello di distribuzione di Resource Manager, seguire la procedura indicata in [How to set up & configure a Failback Process Server (Resource Manager)](./site-recovery-vmware-setup-azure-ps-resource-manager.md) (Come impostare e configurare un server di elaborazione di failback (Resource Manager)).</span><span class="sxs-lookup"><span data-stu-id="d5c97-109">If you used Resource Manager as the deployment model follow the steps in [How to set up & configure a Failback Process Server (Resource Manager)](./site-recovery-vmware-setup-azure-ps-resource-manager.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d5c97-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d5c97-110">Prerequisites</span></span>

[!INCLUDE [site-recovery-vmware-process-server-prereq](../../includes/site-recovery-vmware-azure-process-server-prereq.md)]

## <a name="deploy-a-process-server-on-azure"></a><span data-ttu-id="d5c97-111">Distribuire un server di elaborazione in Azure</span><span class="sxs-lookup"><span data-stu-id="d5c97-111">Deploy a Process Server on Azure</span></span>

1. <span data-ttu-id="d5c97-112">In Azure Marketplace creare una macchina virtuale usando **Microsoft Azure Site Recovery Process Server V2**</span><span class="sxs-lookup"><span data-stu-id="d5c97-112">In Azure Marketplace, create a virtual machine using the **Microsoft Azure Site Recovery Process Server V2**</span></span> </br>
    <span data-ttu-id="d5c97-113">![Marketplace_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image.png)</span><span class="sxs-lookup"><span data-stu-id="d5c97-113">![Marketplace_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image.png)</span></span>
2. <span data-ttu-id="d5c97-114">Assicurarsi di selezionare il modello di distribuzione **classica**</span><span class="sxs-lookup"><span data-stu-id="d5c97-114">Ensure that you select the deployment model as **Classic**</span></span> </br><span data-ttu-id="d5c97-115">
  ![Marketplace_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image-classic.png)</span><span class="sxs-lookup"><span data-stu-id="d5c97-115">
![Marketplace_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image-classic.png)</span></span>
3. <span data-ttu-id="d5c97-116">In Creazione guidata macchina virtuale > Impostazioni di base, selezionare la sottoscrizione e la posizione in cui è stato eseguito il failover delle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="d5c97-116">In the Create virtual machine wizard > Basic Settings, ensure you select the Subscription and Location to where you failed over the virtual machines.</span></span></br><span data-ttu-id="d5c97-117">
  ![create_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-basic-info.png)</span><span class="sxs-lookup"><span data-stu-id="d5c97-117">
![create_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-basic-info.png)</span></span>
4. <span data-ttu-id="d5c97-118">Assicurarsi che la macchina virtuale sia connessa alla rete virtuale di Azure a cui è collegata la macchina virtuale della quale è stato eseguito il failover.</span><span class="sxs-lookup"><span data-stu-id="d5c97-118">Ensure that the virtual machine is connected to the Azure Virtual Network to which the failed over virtual machine is connected.</span></span></br><span data-ttu-id="d5c97-119">
  ![create_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-settings.png)</span><span class="sxs-lookup"><span data-stu-id="d5c97-119">
![create_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-settings.png)</span></span>
5. <span data-ttu-id="d5c97-120">Dopo aver eseguito il provisioning della macchina virtuale del server di elaborazione è necessario accedere e registrarla con il server di configurazione.</span><span class="sxs-lookup"><span data-stu-id="d5c97-120">Once the Process Server virtual machine is provisioned, you need to log in and register it with the Configuration Server.</span></span>

> [!NOTE]
> <span data-ttu-id="d5c97-121">Per poter usare questo server di elaborazione per il failback è necessario registrarlo con il server di configurazione locale.</span><span class="sxs-lookup"><span data-stu-id="d5c97-121">To be able to use this Process Server for failback, you need to register it with the on-premises configuration server.</span></span>

## <a name="registering-the-process-server-running-in-azure-to-a-configuration-server-running-on-premises"></a><span data-ttu-id="d5c97-122">Registrazione del server di elaborazione in esecuzione in Azure con un server di configurazione locale</span><span class="sxs-lookup"><span data-stu-id="d5c97-122">Registering the Process Server (running in Azure) to a Configuration Server (running on-premises)</span></span>

[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

## <a name="upgrading-the-process-server-to-latest-version"></a><span data-ttu-id="d5c97-123">Aggiornamento del server di elaborazione alla versione più recente.</span><span class="sxs-lookup"><span data-stu-id="d5c97-123">Upgrading the Process Server to latest version.</span></span>

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-upgrade-process-server.md)]

## <a name="unregistering-the-process-server-running-in-azure-from-a-configuration-server-running-on-premises"></a><span data-ttu-id="d5c97-124">Annullamento della registrazione del server di elaborazione in esecuzione in Azure con un server di configurazione locale</span><span class="sxs-lookup"><span data-stu-id="d5c97-124">Unregistering the Process Server (running in Azure) from a Configuration Server (running on-premises)</span></span>

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]
