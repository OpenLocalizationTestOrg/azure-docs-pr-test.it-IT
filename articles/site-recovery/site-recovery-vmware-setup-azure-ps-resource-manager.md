---
title: " Gestire un server di elaborazione in esecuzione in Azure (Resource Manager) | Microsoft Docs"
description: Questo articolo descrive come configurare un server di elaborazione failback (Resource Manager) in Azure.
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
ms.openlocfilehash: 2b9b31abd5d11d02935a74e47d26be9803cdc920
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="manage-a-process-server-running-in-azure-resource-manager"></a><span data-ttu-id="37bbb-103">Gestire un server di elaborazione in esecuzione in Azure (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="37bbb-103">Manage a process server running in Azure (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="37bbb-104">Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="37bbb-104">Resource Manager</span></span>](./site-recovery-vmware-setup-azure-ps-resource-manager.md)
> * [<span data-ttu-id="37bbb-105">Classica</span><span class="sxs-lookup"><span data-stu-id="37bbb-105">Classic </span></span>](./site-recovery-vmware-setup-azure-ps-classic.md)

<span data-ttu-id="37bbb-106">Durante il failback è consigliabile distribuire un server di elaborazione in Azure se è presente una latenza elevata tra la rete virtuale di Azure e la rete locale.</span><span class="sxs-lookup"><span data-stu-id="37bbb-106">During failback, it is recommended to deploy process server in Azure if there is high latency between the Azure Virtual Network and your on-premises network.</span></span> <span data-ttu-id="37bbb-107">Questo articolo descrive come impostare, configurare e gestire i server di elaborazione in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="37bbb-107">This article describes how you can set up, configure, and manage the process servers running in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="37bbb-108">Questo articolo è utile se è stato usato **Resource Manager** come modello di distribuzione per le macchine virtuali durante il failover.</span><span class="sxs-lookup"><span data-stu-id="37bbb-108">This article is to be used if you used **Resource Manager** as the deployment model for the virtual machines during failover.</span></span> <span data-ttu-id="37bbb-109">Se è stato usato il modello di distribuzione **classica**, seguire i passaggi indicati in [Come impostare e configurare un server di elaborazione failback (modalità classica)](./site-recovery-vmware-setup-azure-ps-classic.md)</span><span class="sxs-lookup"><span data-stu-id="37bbb-109">If you used **Classic** as the deployment model, follow the steps in [How to set up & configure a Failback process server (Classic)](./site-recovery-vmware-setup-azure-ps-classic.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="37bbb-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="37bbb-110">Prerequisites</span></span>

[!INCLUDE [site-recovery-vmware-process-server-prerequ](../../includes/site-recovery-vmware-azure-process-server-prereq.md)]

## <a name="deploy-a-process-server-on-azure"></a><span data-ttu-id="37bbb-111">Distribuire un server di elaborazione in Azure</span><span class="sxs-lookup"><span data-stu-id="37bbb-111">Deploy a process server on Azure</span></span>
1. <span data-ttu-id="37bbb-112">Selezionare il server di configurazione in Insieme di credenziali > **Infrastruttura di Site Recovery** (sotto l'intestazione "Gestisci") > **Server di configurazione**, sotto l'intestazione "For VMware and Physical Machines" (Per VMware e computer fisici).</span><span class="sxs-lookup"><span data-stu-id="37bbb-112">In the Vault > **Site Recovery Infrastructure** (under the "Manage" heading) > **Configuration Servers** (under "For VMware and Physical Machines" heading), select the configuration server.</span></span>
2. <span data-ttu-id="37bbb-113">Nella pagina dei dettagli del server di configurazione, fare clic su "+ Server di elaborazione"</span><span class="sxs-lookup"><span data-stu-id="37bbb-113">In the Configuration Server details page that opens click "+ Process server"</span></span>

  ![Raccolta per l'aggiunta del server di elaborazione](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps.png)

3.  <span data-ttu-id="37bbb-115">Nella pagina **Aggiungere il server di elaborazione** selezionare i valori seguenti</span><span class="sxs-lookup"><span data-stu-id="37bbb-115">On the **Add process server** page, select the following values</span></span>

  ![Elemento della raccolta per l'aggiunta del server di elaborazione](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps-page-1.png)
|<span data-ttu-id="37bbb-117">**Nome campo**</span><span class="sxs-lookup"><span data-stu-id="37bbb-117">**Field Name**</span></span>|<span data-ttu-id="37bbb-118">**Valore**</span><span class="sxs-lookup"><span data-stu-id="37bbb-118">**Value**</span></span>|
|-|-|
|<span data-ttu-id="37bbb-119">Scegliere la posizione in cui distribuire il server di elaborazione</span><span class="sxs-lookup"><span data-stu-id="37bbb-119">Choose where you want to deploy your process server</span></span>|<span data-ttu-id="37bbb-120">Selezionare il valore **Distribuire un server di elaborazione di failback in Azure**</span><span class="sxs-lookup"><span data-stu-id="37bbb-120">Select the value **Deploy a failback process server in Azure**</span></span> |
|<span data-ttu-id="37bbb-121">Subscription</span><span class="sxs-lookup"><span data-stu-id="37bbb-121">Subscription</span></span>|<span data-ttu-id="37bbb-122">Selezionare la sottoscrizione di Azure in cui è stato eseguito il failover delle macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="37bbb-122">Select the Azure Subscription where you failed over the virtual machines</span></span>|
|<span data-ttu-id="37bbb-123">Gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="37bbb-123">Resource Group</span></span>|<span data-ttu-id="37bbb-124">È possibile creare un gruppo di risorse per distribuire il server di elaborazione o scegliere di distribuire il server di elaborazione in un gruppo di risorse esistente</span><span class="sxs-lookup"><span data-stu-id="37bbb-124">You can create a Resource Group to deploy this process server or choose to deploy the process server in an existing Resource Group</span></span>|
|<span data-ttu-id="37bbb-125">Percorso</span><span class="sxs-lookup"><span data-stu-id="37bbb-125">Location</span></span>|<span data-ttu-id="37bbb-126">Selezionare il data center di Azure in cui è stato eseguito il failover delle macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="37bbb-126">Select the Azure Data Center into which the virtual machines where failed over into</span></span>|
|<span data-ttu-id="37bbb-127">Azure Network</span><span class="sxs-lookup"><span data-stu-id="37bbb-127">Azure Network</span></span>|<span data-ttu-id="37bbb-128">Selezionare la rete virtuale di Azure in cui è stato eseguito il failover delle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="37bbb-128">Select the Azure Virtual Network(VNet) that the virtual machines where failed over into.</span></span> <span data-ttu-id="37bbb-129">Se è stato eseguito il failover delle macchine virtuali in più reti virtuali di Azure, è necessario distribuire un server di elaborazione per ogni rete virtuale</span><span class="sxs-lookup"><span data-stu-id="37bbb-129">If you failed over virtual machines into multiple Azure VNets, then you need a process server deployed per VNet</span></span>|

4. <span data-ttu-id="37bbb-130">Compilare le altre proprietà per il server di elaborazione</span><span class="sxs-lookup"><span data-stu-id="37bbb-130">Fill in the rest of the properties for the process server</span></span>

  ![Riepilogo dell'aggiunta del server di elaborazione](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps-page-2.png)
|<span data-ttu-id="37bbb-132">**Nome campo**</span><span class="sxs-lookup"><span data-stu-id="37bbb-132">**Field Name**</span></span>|<span data-ttu-id="37bbb-133">**Valore**</span><span class="sxs-lookup"><span data-stu-id="37bbb-133">**Value**</span></span>|
|-|-|
|<span data-ttu-id="37bbb-134">Server Name</span><span class="sxs-lookup"><span data-stu-id="37bbb-134">Server Name</span></span>|<span data-ttu-id="37bbb-135">Nome visualizzato/nome host per la macchina virtuale del server di elaborazione</span><span class="sxs-lookup"><span data-stu-id="37bbb-135">Display name & Host name for your process server virtual machine</span></span>|
| <span data-ttu-id="37bbb-136">User Name</span><span class="sxs-lookup"><span data-stu-id="37bbb-136">User Name</span></span>|<span data-ttu-id="37bbb-137">Un nome utente che diventa amministratore sulla macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="37bbb-137">A user name that becomes an Administrator on that virtual machine</span></span>|
|<span data-ttu-id="37bbb-138">Account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="37bbb-138">Storage Account</span></span>|<span data-ttu-id="37bbb-139">Nome dell'account di archiviazione in cui si trovano i dischi virtuali della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="37bbb-139">Name of the Storage Account where the virtual machine's virtual disk's are placed</span></span>|
|<span data-ttu-id="37bbb-140">Subnet</span><span class="sxs-lookup"><span data-stu-id="37bbb-140">Subnet</span></span>|<span data-ttu-id="37bbb-141">Subnet della rete virtuale di Azure a cui è collegata la macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="37bbb-141">The subnet of the Azure VNet to which the virtual machine is connected</span></span>|
| <span data-ttu-id="37bbb-142">Indirizzo IP</span><span class="sxs-lookup"><span data-stu-id="37bbb-142">IP Address</span></span>|<span data-ttu-id="37bbb-143">Indirizzo IP che il server di elaborazione dovrà assumere dopo l'avvio</span><span class="sxs-lookup"><span data-stu-id="37bbb-143">IP Address that you would like the process server to assume once it boots up</span></span>|
5. <span data-ttu-id="37bbb-144">Fare clic sul pulsante OK per avviare la distribuzione della macchina virtuale del server di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="37bbb-144">Click the OK button to start deploying the process server virtual machine.</span></span>

> [!NOTE]
> <span data-ttu-id="37bbb-145">Per poter usare questo server di elaborazione per il failback è necessario registrarlo con il server di configurazione locale.</span><span class="sxs-lookup"><span data-stu-id="37bbb-145">To be able to use this process server for failback, you need to register it with the on-premises configuration server.</span></span>

## <a name="registering-the-process-server-running-in-azure-to-a-configuration-server-running-on-premises"></a><span data-ttu-id="37bbb-146">Registrazione del server di elaborazione in esecuzione in Azure con un server di configurazione locale</span><span class="sxs-lookup"><span data-stu-id="37bbb-146">Registering the process server (running in Azure) to a Configuration Server (running on-premises)</span></span>

[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

## <a name="upgrading-the-process-server-to-latest-version"></a><span data-ttu-id="37bbb-147">Aggiornamento del server di elaborazione alla versione più recente.</span><span class="sxs-lookup"><span data-stu-id="37bbb-147">Upgrading the process server to latest version.</span></span>

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-upgrade-process-server.md)]

## <a name="unregistering-the-process-server-running-in-azure-from-a-configuration-server-running-on-premises"></a><span data-ttu-id="37bbb-148">Annullamento della registrazione del server di elaborazione in esecuzione in Azure con un server di configurazione locale</span><span class="sxs-lookup"><span data-stu-id="37bbb-148">Unregistering the process server (running in Azure) from a Configuration Server (running on-premises)</span></span>

[!INCLUDE [site-recovery-vmware-unregister-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]
