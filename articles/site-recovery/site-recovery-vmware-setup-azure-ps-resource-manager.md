---
title: " Gestire un server di elaborazione in esecuzione in Azure (Resource Manager) | Microsoft Docs"
description: Questo articolo descrive come tooset backup un failback processo server (gestione delle risorse) In Azure.
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
ms.openlocfilehash: 70426b96095cc42befff6c4114fb56536284a667
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-process-server-running-in-azure-resource-manager"></a><span data-ttu-id="f1d36-103">Gestire un server di elaborazione in esecuzione in Azure (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="f1d36-103">Manage a process server running in Azure (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f1d36-104">Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="f1d36-104">Resource Manager</span></span>](./site-recovery-vmware-setup-azure-ps-resource-manager.md)
> * [<span data-ttu-id="f1d36-105">Classica</span><span class="sxs-lookup"><span data-stu-id="f1d36-105">Classic </span></span>](./site-recovery-vmware-setup-azure-ps-classic.md)

<span data-ttu-id="f1d36-106">Durante il failback, server process toodeploy in Azure è consigliabile se è presente una latenza elevata tra hello rete virtuale di Azure e la rete locale.</span><span class="sxs-lookup"><span data-stu-id="f1d36-106">During failback, it is recommended toodeploy process server in Azure if there is high latency between hello Azure Virtual Network and your on-premises network.</span></span> <span data-ttu-id="f1d36-107">Questo articolo descrive come è possibile impostare, configurare e gestire i server di elaborazione hello in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="f1d36-107">This article describes how you can set up, configure, and manage hello process servers running in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="f1d36-108">Questo articolo è toobe se è utilizzata **Gestione risorse** come modello di distribuzione hello per le macchine virtuali hello durante il failover.</span><span class="sxs-lookup"><span data-stu-id="f1d36-108">This article is toobe used if you used **Resource Manager** as hello deployment model for hello virtual machines during failover.</span></span> <span data-ttu-id="f1d36-109">Se è stato utilizzato **classico** come modello di distribuzione hello, seguire i passaggi di hello in [come tooset a & configurare un server di elaborazione di Failback (versione classica)](./site-recovery-vmware-setup-azure-ps-classic.md)</span><span class="sxs-lookup"><span data-stu-id="f1d36-109">If you used **Classic** as hello deployment model, follow hello steps in [How tooset up & configure a Failback process server (Classic)](./site-recovery-vmware-setup-azure-ps-classic.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f1d36-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="f1d36-110">Prerequisites</span></span>

[!INCLUDE [site-recovery-vmware-process-server-prerequ](../../includes/site-recovery-vmware-azure-process-server-prereq.md)]

## <a name="deploy-a-process-server-on-azure"></a><span data-ttu-id="f1d36-111">Distribuire un server di elaborazione in Azure</span><span class="sxs-lookup"><span data-stu-id="f1d36-111">Deploy a process server on Azure</span></span>
1. <span data-ttu-id="f1d36-112">Nell'insieme di credenziali hello > **infrastruttura di Site Recovery** (sotto l'intestazione "Manage" hello) > **server di configurazione** (sotto l'intestazione "Per VMware e computer fisici"), selezionare il server di configurazione di hello.</span><span class="sxs-lookup"><span data-stu-id="f1d36-112">In hello Vault > **Site Recovery Infrastructure** (under hello "Manage" heading) > **Configuration Servers** (under "For VMware and Physical Machines" heading), select hello configuration server.</span></span>
2. <span data-ttu-id="f1d36-113">Nella pagina di dettagli di configurazione Server hello visualizzata fare clic su "+ processo server"</span><span class="sxs-lookup"><span data-stu-id="f1d36-113">In hello Configuration Server details page that opens click "+ Process server"</span></span>

  ![Raccolta per l'aggiunta del server di elaborazione](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps.png)

3.  <span data-ttu-id="f1d36-115">In hello **Aggiungi server di elaborazione** pagina, seleziona hello seguenti valori</span><span class="sxs-lookup"><span data-stu-id="f1d36-115">On hello **Add process server** page, select hello following values</span></span>

  ![Elemento della raccolta per l'aggiunta del server di elaborazione](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps-page-1.png)
|<span data-ttu-id="f1d36-117">**Nome campo**</span><span class="sxs-lookup"><span data-stu-id="f1d36-117">**Field Name**</span></span>|<span data-ttu-id="f1d36-118">**Valore**</span><span class="sxs-lookup"><span data-stu-id="f1d36-118">**Value**</span></span>|
|-|-|
|<span data-ttu-id="f1d36-119">Scegliere dove si vuole toodeploy il server di elaborazione</span><span class="sxs-lookup"><span data-stu-id="f1d36-119">Choose where you want toodeploy your process server</span></span>|<span data-ttu-id="f1d36-120">Selezionare il valore di hello **distribuire un server di elaborazione di failback in Azure**</span><span class="sxs-lookup"><span data-stu-id="f1d36-120">Select hello value **Deploy a failback process server in Azure**</span></span> |
|<span data-ttu-id="f1d36-121">Sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="f1d36-121">Subscription</span></span>|<span data-ttu-id="f1d36-122">Selezionare la sottoscrizione di Azure in cui è stato eseguito il failover delle macchine virtuali hello hello</span><span class="sxs-lookup"><span data-stu-id="f1d36-122">Select hello Azure Subscription where you failed over hello virtual machines</span></span>|
|<span data-ttu-id="f1d36-123">Gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="f1d36-123">Resource Group</span></span>|<span data-ttu-id="f1d36-124">È possibile creare un gruppo di risorse di toodeploy questo server di elaborazione o scegliere i server di elaborazione toodeploy hello in un gruppo di risorse esistente</span><span class="sxs-lookup"><span data-stu-id="f1d36-124">You can create a Resource Group toodeploy this process server or choose toodeploy hello process server in an existing Resource Group</span></span>|
|<span data-ttu-id="f1d36-125">Percorso</span><span class="sxs-lookup"><span data-stu-id="f1d36-125">Location</span></span>|<span data-ttu-id="f1d36-126">Selezionare hello Azure Data Center in cui hello di macchine virtuali in cui è stato eseguito il failover in</span><span class="sxs-lookup"><span data-stu-id="f1d36-126">Select hello Azure Data Center into which hello virtual machines where failed over into</span></span>|
|<span data-ttu-id="f1d36-127">Azure Network</span><span class="sxs-lookup"><span data-stu-id="f1d36-127">Azure Network</span></span>|<span data-ttu-id="f1d36-128">Seleziona hello Network(VNet) virtuale di Azure che hello macchine virtuali in cui è stato eseguito il failover in.</span><span class="sxs-lookup"><span data-stu-id="f1d36-128">Select hello Azure Virtual Network(VNet) that hello virtual machines where failed over into.</span></span> <span data-ttu-id="f1d36-129">Se è stato eseguito il failover delle macchine virtuali in più reti virtuali di Azure, è necessario distribuire un server di elaborazione per ogni rete virtuale</span><span class="sxs-lookup"><span data-stu-id="f1d36-129">If you failed over virtual machines into multiple Azure VNets, then you need a process server deployed per VNet</span></span>|

4. <span data-ttu-id="f1d36-130">Compilare il resto di hello delle proprietà di hello del server di elaborazione hello</span><span class="sxs-lookup"><span data-stu-id="f1d36-130">Fill in hello rest of hello properties for hello process server</span></span>

  ![Riepilogo dell'aggiunta del server di elaborazione](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps-page-2.png)
|<span data-ttu-id="f1d36-132">**Nome campo**</span><span class="sxs-lookup"><span data-stu-id="f1d36-132">**Field Name**</span></span>|<span data-ttu-id="f1d36-133">**Valore**</span><span class="sxs-lookup"><span data-stu-id="f1d36-133">**Value**</span></span>|
|-|-|
|<span data-ttu-id="f1d36-134">Server Name</span><span class="sxs-lookup"><span data-stu-id="f1d36-134">Server Name</span></span>|<span data-ttu-id="f1d36-135">Nome visualizzato/nome host per la macchina virtuale del server di elaborazione</span><span class="sxs-lookup"><span data-stu-id="f1d36-135">Display name & Host name for your process server virtual machine</span></span>|
| <span data-ttu-id="f1d36-136">User Name</span><span class="sxs-lookup"><span data-stu-id="f1d36-136">User Name</span></span>|<span data-ttu-id="f1d36-137">Un nome utente che diventa amministratore sulla macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="f1d36-137">A user name that becomes an Administrator on that virtual machine</span></span>|
|<span data-ttu-id="f1d36-138">Account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="f1d36-138">Storage Account</span></span>|<span data-ttu-id="f1d36-139">Nome dell'Account di archiviazione in cui viene inserito del disco virtuale della macchina virtuale hello hello</span><span class="sxs-lookup"><span data-stu-id="f1d36-139">Name of hello Storage Account where hello virtual machine's virtual disk's are placed</span></span>|
|<span data-ttu-id="f1d36-140">Subnet</span><span class="sxs-lookup"><span data-stu-id="f1d36-140">Subnet</span></span>|<span data-ttu-id="f1d36-141">subnet Hello della macchina virtuale di hello rete virtuale di Azure toowhich hello è connesso</span><span class="sxs-lookup"><span data-stu-id="f1d36-141">hello subnet of hello Azure VNet toowhich hello virtual machine is connected</span></span>|
| <span data-ttu-id="f1d36-142">Indirizzo IP</span><span class="sxs-lookup"><span data-stu-id="f1d36-142">IP Address</span></span>|<span data-ttu-id="f1d36-143">Indirizzo IP che si desidera hello processo server tooassume dopo l'avvio</span><span class="sxs-lookup"><span data-stu-id="f1d36-143">IP Address that you would like hello process server tooassume once it boots up</span></span>|
5. <span data-ttu-id="f1d36-144">Fare clic su toostart pulsante OK hello hello processo macchina virtuale del server di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="f1d36-144">Click hello OK button toostart deploying hello process server virtual machine.</span></span>

> [!NOTE]
> <span data-ttu-id="f1d36-145">toouse in grado di toobe questo server di elaborazione per il failback, è necessario tooregister con server di configurazione di on-premise hello.</span><span class="sxs-lookup"><span data-stu-id="f1d36-145">toobe able toouse this process server for failback, you need tooregister it with hello on-premises configuration server.</span></span>

## <a name="registering-hello-process-server-running-in-azure-tooa-configuration-server-running-on-premises"></a><span data-ttu-id="f1d36-146">Registrazione hello processo server (in esecuzione in Azure) tooa Server di configurazione (in esecuzione in locale)</span><span class="sxs-lookup"><span data-stu-id="f1d36-146">Registering hello process server (running in Azure) tooa Configuration Server (running on-premises)</span></span>

[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

## <a name="upgrading-hello-process-server-toolatest-version"></a><span data-ttu-id="f1d36-147">L'aggiornamento di versione di toolatest hello processo server.</span><span class="sxs-lookup"><span data-stu-id="f1d36-147">Upgrading hello process server toolatest version.</span></span>

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-upgrade-process-server.md)]

## <a name="unregistering-hello-process-server-running-in-azure-from-a-configuration-server-running-on-premises"></a><span data-ttu-id="f1d36-148">L'annullamento della registrazione di server di elaborazione hello (in esecuzione in Azure) da un Server di configurazione (in esecuzione in locale)</span><span class="sxs-lookup"><span data-stu-id="f1d36-148">Unregistering hello process server (running in Azure) from a Configuration Server (running on-premises)</span></span>

[!INCLUDE [site-recovery-vmware-unregister-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]
