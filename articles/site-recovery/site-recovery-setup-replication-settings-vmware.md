---
title: Configurare le impostazioni di replica per Azure Site Recovery| Documentazione Microsoft
description: Descrive come distribuire Site Recovery per orchestrare la replica, il failover e il ripristino di macchine virtuali Hyper-V nei cloud VMM in Azure.
services: site-recovery
documentationcenter: 
author: sujayt
manager: rochakm
editor: rayne-wiselman
ms.assetid: 8e7d868e-00f3-4e8b-9a9e-f23365abf6ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 06/05/2017
ms.author: sutalasi
ms.openlocfilehash: 73a1f19177f23441f5f7165cf2bc92ba85e62aa5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="manage-replication-policy-for-vmware-to-azure"></a><span data-ttu-id="eb13a-103">Gestire i criteri di replica per VMware in Azure</span><span class="sxs-lookup"><span data-stu-id="eb13a-103">Manage replication policy for VMware to Azure</span></span>


## <a name="create-a-replication-policy"></a><span data-ttu-id="eb13a-104">Creare un criterio di replica</span><span class="sxs-lookup"><span data-stu-id="eb13a-104">Create a replication policy</span></span>

1. <span data-ttu-id="eb13a-105">Selezionare **Gestisci** > **Site Recovery Infrastructure** (Infrastruttura di Site Recovery).</span><span class="sxs-lookup"><span data-stu-id="eb13a-105">Select **Manage** > **Site Recovery Infrastructure**.</span></span>
2. <span data-ttu-id="eb13a-106">Selezionare **Criteri di replica** in **For VMware and Physical machines** (Per VMware e computer fisici).</span><span class="sxs-lookup"><span data-stu-id="eb13a-106">Select **Replication policies** under **For VMware and Physical machines**.</span></span>
3. <span data-ttu-id="eb13a-107">Selezionare **+Replication policy** (+Criteri di replica).</span><span class="sxs-lookup"><span data-stu-id="eb13a-107">Select **+Replication policy**.</span></span>

    ![Creare criteri di replica](./media/site-recovery-setup-replication-settings-vmware/createpolicy.png)

4. <span data-ttu-id="eb13a-109">Immettere il nome del criterio.</span><span class="sxs-lookup"><span data-stu-id="eb13a-109">Enter the policy name.</span></span>

5. <span data-ttu-id="eb13a-110">In **Soglia RPO**specificare il limite per RPO.</span><span class="sxs-lookup"><span data-stu-id="eb13a-110">In **RPO threshold**, specify the RPO limit.</span></span> <span data-ttu-id="eb13a-111">Quando la replica continua supera questo limite, verranno generati avvisi.</span><span class="sxs-lookup"><span data-stu-id="eb13a-111">Alerts will be generated when continuous replication exceeds this limit.</span></span>
6. <span data-ttu-id="eb13a-112">In **Conservazione del punto di ripristino** specificare la durata in ore dell'intervallo di conservazione per ogni punto di ripristino.</span><span class="sxs-lookup"><span data-stu-id="eb13a-112">In **Recovery point retention**, specify (in hours) the duration of the retention window for each recovery point.</span></span> <span data-ttu-id="eb13a-113">I computer protetti possono essere ripristinati in qualsiasi punto all'interno di un intervallo di conservazione.</span><span class="sxs-lookup"><span data-stu-id="eb13a-113">Protected machines can be recovered to any point within a retention window.</span></span>

    > [!NOTE]
    > <span data-ttu-id="eb13a-114">Per le macchine replicate nell'archiviazione Premium è supportato un intervallo di conservazione fino a 24 ore.</span><span class="sxs-lookup"><span data-stu-id="eb13a-114">Up to 24 hours of retention is supported for machines replicated to premium storage.</span></span> <span data-ttu-id="eb13a-115">Per le macchine replicate nell'archiviazione standard è supportato un intervallo di conservazione fino a 72 ore.</span><span class="sxs-lookup"><span data-stu-id="eb13a-115">Up to 72 hours of retention is supported for machines replicated to standard storage.</span></span>

    > [!NOTE]
    > <span data-ttu-id="eb13a-116">Viene creato automaticamente un criterio di replica per il failback.</span><span class="sxs-lookup"><span data-stu-id="eb13a-116">A replication policy for failback is automatically created.</span></span>

7. <span data-ttu-id="eb13a-117">In **Frequenza snapshot coerenti con l'app**specificare la frequenza, in minuti, per la creazione di punti di ripristino contenenti snapshot coerenti con l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="eb13a-117">In **App-consistent snapshot frequency**, specify how often (in minutes) recovery points that contain application-consistent snapshots will be created.</span></span>

8. <span data-ttu-id="eb13a-118">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="eb13a-118">Click **OK**.</span></span> <span data-ttu-id="eb13a-119">La creazione del criterio dovrebbe richiedere dai 30 secondi ai 60 secondi.</span><span class="sxs-lookup"><span data-stu-id="eb13a-119">The policy should be created in 30 to 60 seconds.</span></span>

![Generazione dei criteri di replica](./media/site-recovery-setup-replication-settings-vmware/Creating-Policy.png)

## <a name="associate-a-configuration-server-with-a-replication-policy"></a><span data-ttu-id="eb13a-121">Associare un server di configurazione ai criteri di replica</span><span class="sxs-lookup"><span data-stu-id="eb13a-121">Associate a configuration server with a replication policy</span></span>
1. <span data-ttu-id="eb13a-122">Scegliere il criterio di replica a cui si desidera associare il server di configurazione.</span><span class="sxs-lookup"><span data-stu-id="eb13a-122">Choose the replication policy to which you want to associate the configuration server.</span></span>
2. <span data-ttu-id="eb13a-123">Fare clic su **Associa**.</span><span class="sxs-lookup"><span data-stu-id="eb13a-123">Click **Associate**.</span></span>
<span data-ttu-id="eb13a-124">![Associare i server di configurazione](./media/site-recovery-setup-replication-settings-vmware/Associate-CS-1.PNG)</span><span class="sxs-lookup"><span data-stu-id="eb13a-124">![Associate configuration server](./media/site-recovery-setup-replication-settings-vmware/Associate-CS-1.PNG)</span></span>

3. <span data-ttu-id="eb13a-125">Selezionare il server di configurazione nell'elenco dei server.</span><span class="sxs-lookup"><span data-stu-id="eb13a-125">Select the configuration server from the list of servers.</span></span>
4. <span data-ttu-id="eb13a-126">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="eb13a-126">Click **OK**.</span></span> <span data-ttu-id="eb13a-127">L'associazione del server di configurazione dovrebbe richiedere da 1 a 2 minuti.</span><span class="sxs-lookup"><span data-stu-id="eb13a-127">The configuration server should be associated in one to two minutes.</span></span>

![Associazione del server di configurazione](./media/site-recovery-setup-replication-settings-vmware/Associate-CS-2.png)

## <a name="edit-a-replication-policy"></a><span data-ttu-id="eb13a-129">Modificare un criterio di replica</span><span class="sxs-lookup"><span data-stu-id="eb13a-129">Edit a replication policy</span></span>
1. <span data-ttu-id="eb13a-130">Scegliere il criterio per cui si desidera modificare le impostazioni di replica.</span><span class="sxs-lookup"><span data-stu-id="eb13a-130">Choose the replication policy for which you want to edit replication settings.</span></span>
<span data-ttu-id="eb13a-131">![Modificare i criteri di replica](./media/site-recovery-setup-replication-settings-vmware/Select-Policy.png)</span><span class="sxs-lookup"><span data-stu-id="eb13a-131">![Edit replication policy](./media/site-recovery-setup-replication-settings-vmware/Select-Policy.png)</span></span>

2. <span data-ttu-id="eb13a-132">Fare clic su **Edit Settings**.</span><span class="sxs-lookup"><span data-stu-id="eb13a-132">Click **Edit Settings**.</span></span>
<span data-ttu-id="eb13a-133">![Modificare le impostazioni dei criteri di replica](./media/site-recovery-setup-replication-settings-vmware/Edit-Policy.png)</span><span class="sxs-lookup"><span data-stu-id="eb13a-133">![Edit replication policy settings](./media/site-recovery-setup-replication-settings-vmware/Edit-Policy.png)</span></span>

3. <span data-ttu-id="eb13a-134">Modificare le impostazioni in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="eb13a-134">Change the settings based on your need.</span></span>
4. <span data-ttu-id="eb13a-135">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="eb13a-135">Click **Save**.</span></span> <span data-ttu-id="eb13a-136">Il salvataggio del criterio dovrebbe richiedere approssimativamente 5 minuti, a seconda del numero di macchine virtuali che usano il criterio di replica.</span><span class="sxs-lookup"><span data-stu-id="eb13a-136">The policy should be saved in two to five minutes, depending on how many VMs are using that replication policy.</span></span>

![Salvare i criteri di replica](./media/site-recovery-setup-replication-settings-vmware/Save-Policy.png)

## <a name="dissociate-a-configuration-server-from-a-replication-policy"></a><span data-ttu-id="eb13a-138">Annullare l'associazione del server di configurazione dai criteri di replica</span><span class="sxs-lookup"><span data-stu-id="eb13a-138">Dissociate a configuration server from a replication policy</span></span>
1. <span data-ttu-id="eb13a-139">Scegliere il criterio di replica a cui si desidera associare il server di configurazione.</span><span class="sxs-lookup"><span data-stu-id="eb13a-139">Choose the replication policy to which you want to associate the configuration server.</span></span>
2. <span data-ttu-id="eb13a-140">Fare clic su **Annulla associazione**.</span><span class="sxs-lookup"><span data-stu-id="eb13a-140">Click **Dissociate**.</span></span>
3. <span data-ttu-id="eb13a-141">Selezionare il server di configurazione nell'elenco dei server.</span><span class="sxs-lookup"><span data-stu-id="eb13a-141">Select the configuration server from the list of servers.</span></span>
4. <span data-ttu-id="eb13a-142">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="eb13a-142">Click **OK**.</span></span> <span data-ttu-id="eb13a-143">L'annullamento dell'associazione del server di configurazione dovrebbe richiedere 2 minuti.</span><span class="sxs-lookup"><span data-stu-id="eb13a-143">The configuration server should be dissociated in one to two minutes.</span></span>

    > [!NOTE]
    > <span data-ttu-id="eb13a-144">Non è possibile annullare l'associazione di un server di configurazione se i criteri vengono usati da almeno un elemento replicato.</span><span class="sxs-lookup"><span data-stu-id="eb13a-144">You cannot dissociate a configuration server if there is at least one replicated item using the policy.</span></span> <span data-ttu-id="eb13a-145">Prima di annullare l'associazione del server di configurazione, verificare che nessun elemento replicato usi i criteri.</span><span class="sxs-lookup"><span data-stu-id="eb13a-145">Make sure there are no replicated items using the policy before you dissociate the configuration server.</span></span>

## <a name="delete-a-replication-policy"></a><span data-ttu-id="eb13a-146">Eliminare un criterio di replica</span><span class="sxs-lookup"><span data-stu-id="eb13a-146">Delete a replication policy</span></span>

1. <span data-ttu-id="eb13a-147">Scegliere il criterio di replica che si desidera eliminare.</span><span class="sxs-lookup"><span data-stu-id="eb13a-147">Choose the replication policy that you want to delete.</span></span>
2. <span data-ttu-id="eb13a-148">Fare clic su **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="eb13a-148">Click **Delete**.</span></span> <span data-ttu-id="eb13a-149">L'eliminazione del criterio dovrebbe richiedere dai 30 secondi ai 60 secondi.</span><span class="sxs-lookup"><span data-stu-id="eb13a-149">The policy should be deleted in 30 to 60 seconds.</span></span>

    > [!NOTE]
    > <span data-ttu-id="eb13a-150">Non è possibile eliminare criteri di replica a cui è associato almeno 1 server di configurazione.</span><span class="sxs-lookup"><span data-stu-id="eb13a-150">You cannot delete a replication policy if it has at least one configuration server associated to it.</span></span> <span data-ttu-id="eb13a-151">Prima di eliminare i criteri, verificare che nessun elemento replicato li usi ed eliminare tutti server di configurazione associati.</span><span class="sxs-lookup"><span data-stu-id="eb13a-151">Make sure there are no replicated items using the policy and delete all the associated configuration servers before you delete the policy.</span></span>
