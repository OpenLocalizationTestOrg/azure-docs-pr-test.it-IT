---
title: " Gestire un server di elaborazione in esecuzione in Azure (versione classica) | Microsoft Docs"
description: Questo articolo viene descritto come tooset di un processo Server(Classic) In Azure il failback.
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
ms.openlocfilehash: eadcc0236c77c9ebbbc885c4a7ee81098f1f4e72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-process-server-running-in-azure-classic"></a><span data-ttu-id="ed368-103">Gestire un server di elaborazione in esecuzione in Azure (versione classica)</span><span class="sxs-lookup"><span data-stu-id="ed368-103">Manage a Process Server running in Azure (Classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ed368-104">Azure versione classica</span><span class="sxs-lookup"><span data-stu-id="ed368-104">Azure Classic </span></span>](./site-recovery-vmware-setup-azure-ps-classic.md)
> * [<span data-ttu-id="ed368-105">Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="ed368-105">Resource Manager</span></span>](./site-recovery-vmware-setup-azure-ps-resource-manager.md)

<span data-ttu-id="ed368-106">Durante il failback, è consigliabile toodeploy Server di elaborazione in Azure se è presente una latenza elevata tra hello rete virtuale di Azure e la rete locale.</span><span class="sxs-lookup"><span data-stu-id="ed368-106">During failback, it is recommended toodeploy Process Server in Azure if there is high latency between hello Azure Virtual Network and your on-premises network.</span></span> <span data-ttu-id="ed368-107">Questo articolo descrive come è possibile impostare, configurare e gestire i server di elaborazione hello in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="ed368-107">This article describes how you can set up, configure, and manage hello process servers running in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="ed368-108">Questo articolo è toobe se classica è utilizzata come modello di distribuzione hello per le macchine virtuali hello durante il failover.</span><span class="sxs-lookup"><span data-stu-id="ed368-108">This article is toobe used if you used Classic as hello deployment model for hello virtual machines during failover.</span></span> <span data-ttu-id="ed368-109">Se utilizzato Gestione risorse come passaggi di distribuzione modello seguire hello in hello [come tooset a & configurare un Server di elaborazione di Failback (gestione delle risorse)](./site-recovery-vmware-setup-azure-ps-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="ed368-109">If you used Resource Manager as hello deployment model follow hello steps in [How tooset up & configure a Failback Process Server (Resource Manager)](./site-recovery-vmware-setup-azure-ps-resource-manager.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ed368-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="ed368-110">Prerequisites</span></span>

[!INCLUDE [site-recovery-vmware-process-server-prereq](../../includes/site-recovery-vmware-azure-process-server-prereq.md)]

## <a name="deploy-a-process-server-on-azure"></a><span data-ttu-id="ed368-111">Distribuire un server di elaborazione in Azure</span><span class="sxs-lookup"><span data-stu-id="ed368-111">Deploy a Process Server on Azure</span></span>

1. <span data-ttu-id="ed368-112">In Azure Marketplace, creare una macchina virtuale utilizzando hello **Microsoft Azure Site Recovery processo Server V2**</span><span class="sxs-lookup"><span data-stu-id="ed368-112">In Azure Marketplace, create a virtual machine using hello **Microsoft Azure Site Recovery Process Server V2**</span></span> </br>
    <span data-ttu-id="ed368-113">![Marketplace_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image.png)</span><span class="sxs-lookup"><span data-stu-id="ed368-113">![Marketplace_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image.png)</span></span>
2. <span data-ttu-id="ed368-114">Assicurarsi di selezionare il modello di distribuzione hello come **classico**</span><span class="sxs-lookup"><span data-stu-id="ed368-114">Ensure that you select hello deployment model as **Classic**</span></span> </br><span data-ttu-id="ed368-115">
  ![Marketplace_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image-classic.png)</span><span class="sxs-lookup"><span data-stu-id="ed368-115">
![Marketplace_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image-classic.png)</span></span>
3. <span data-ttu-id="ed368-116">Nella procedura guidata di hello crea macchina virtuale > Impostazioni di base, assicurarsi di selezionare hello toowhere sottoscrizione e il percorso è stato eseguito il failover delle macchine virtuali hello.</span><span class="sxs-lookup"><span data-stu-id="ed368-116">In hello Create virtual machine wizard > Basic Settings, ensure you select hello Subscription and Location toowhere you failed over hello virtual machines.</span></span></br><span data-ttu-id="ed368-117">
  ![create_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-basic-info.png)</span><span class="sxs-lookup"><span data-stu-id="ed368-117">
![create_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-basic-info.png)</span></span>
4. <span data-ttu-id="ed368-118">Verificare che la macchina virtuale hello sia connesso hello toowhich di rete virtuale di Azure toohello failover macchina virtuale è connessa.</span><span class="sxs-lookup"><span data-stu-id="ed368-118">Ensure that hello virtual machine is connected toohello Azure Virtual Network toowhich hello failed over virtual machine is connected.</span></span></br><span data-ttu-id="ed368-119">
  ![create_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-settings.png)</span><span class="sxs-lookup"><span data-stu-id="ed368-119">
![create_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-settings.png)</span></span>
5. <span data-ttu-id="ed368-120">Una volta provisioning hello Server di elaborazione della macchina virtuale, è necessario toolog in e registrarlo con hello del Server di configurazione.</span><span class="sxs-lookup"><span data-stu-id="ed368-120">Once hello Process Server virtual machine is provisioned, you need toolog in and register it with hello Configuration Server.</span></span>

> [!NOTE]
> <span data-ttu-id="ed368-121">toouse in grado di toobe questo Server di elaborazione per il failback, è necessario tooregister con server di configurazione di on-premise hello.</span><span class="sxs-lookup"><span data-stu-id="ed368-121">toobe able toouse this Process Server for failback, you need tooregister it with hello on-premises configuration server.</span></span>

## <a name="registering-hello-process-server-running-in-azure-tooa-configuration-server-running-on-premises"></a><span data-ttu-id="ed368-122">Registrazione hello processo Server (in esecuzione in Azure) tooa Server di configurazione (in esecuzione in locale)</span><span class="sxs-lookup"><span data-stu-id="ed368-122">Registering hello Process Server (running in Azure) tooa Configuration Server (running on-premises)</span></span>

[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

## <a name="upgrading-hello-process-server-toolatest-version"></a><span data-ttu-id="ed368-123">L'aggiornamento di versione di toolatest hello Server di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="ed368-123">Upgrading hello Process Server toolatest version.</span></span>

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-upgrade-process-server.md)]

## <a name="unregistering-hello-process-server-running-in-azure-from-a-configuration-server-running-on-premises"></a><span data-ttu-id="ed368-124">Annullamento della registrazione hello processo Server (in esecuzione in Azure) da un Server di configurazione (in esecuzione in locale)</span><span class="sxs-lookup"><span data-stu-id="ed368-124">Unregistering hello Process Server (running in Azure) from a Configuration Server (running on-premises)</span></span>

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]
