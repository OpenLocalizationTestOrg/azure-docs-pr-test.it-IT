---
title: aaaSet le impostazioni di replica per Azure Site Recovery | Documenti Microsoft
description: "Descrive la modalità di cloud di tooAzure toodeploy Site Recovery tooorchestrate replica, il failover e ripristino di macchine virtuali Hyper-V in VMM."
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
ms.openlocfilehash: 618e92e42411732a2a1bb75c5e5ea8a433cd7d58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-replication-policy-for-vmware-tooazure"></a><span data-ttu-id="9976c-103">Gestire i criteri di replica per VMware tooAzure</span><span class="sxs-lookup"><span data-stu-id="9976c-103">Manage replication policy for VMware tooAzure</span></span>


## <a name="create-a-replication-policy"></a><span data-ttu-id="9976c-104">Creare un criterio di replica</span><span class="sxs-lookup"><span data-stu-id="9976c-104">Create a replication policy</span></span>

1. <span data-ttu-id="9976c-105">Selezionare **Gestisci** > **Site Recovery Infrastructure** (Infrastruttura di Site Recovery).</span><span class="sxs-lookup"><span data-stu-id="9976c-105">Select **Manage** > **Site Recovery Infrastructure**.</span></span>
2. <span data-ttu-id="9976c-106">Selezionare **Criteri di replica** in **For VMware and Physical machines** (Per VMware e computer fisici).</span><span class="sxs-lookup"><span data-stu-id="9976c-106">Select **Replication policies** under **For VMware and Physical machines**.</span></span>
3. <span data-ttu-id="9976c-107">Selezionare **+Replication policy** (+Criteri di replica).</span><span class="sxs-lookup"><span data-stu-id="9976c-107">Select **+Replication policy**.</span></span>

    ![Creare criteri di replica](./media/site-recovery-setup-replication-settings-vmware/createpolicy.png)

4. <span data-ttu-id="9976c-109">Immettere il nome di criterio hello.</span><span class="sxs-lookup"><span data-stu-id="9976c-109">Enter hello policy name.</span></span>

5. <span data-ttu-id="9976c-110">In **soglia RPO**, specificare il limite RPO hello.</span><span class="sxs-lookup"><span data-stu-id="9976c-110">In **RPO threshold**, specify hello RPO limit.</span></span> <span data-ttu-id="9976c-111">Quando la replica continua supera questo limite, verranno generati avvisi.</span><span class="sxs-lookup"><span data-stu-id="9976c-111">Alerts will be generated when continuous replication exceeds this limit.</span></span>
6. <span data-ttu-id="9976c-112">In **conservazione del punto di ripristino**, specificare (in ore) hello durata del periodo di memorizzazione hello per ogni punto di ripristino.</span><span class="sxs-lookup"><span data-stu-id="9976c-112">In **Recovery point retention**, specify (in hours) hello duration of hello retention window for each recovery point.</span></span> <span data-ttu-id="9976c-113">Macchine virtuali protette possono essere ripristinati tooany punto all'interno di un periodo di memorizzazione.</span><span class="sxs-lookup"><span data-stu-id="9976c-113">Protected machines can be recovered tooany point within a retention window.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9976c-114">Ore too24 periodo di conservazione è supportato per l'archiviazione replicata toopremium macchine.</span><span class="sxs-lookup"><span data-stu-id="9976c-114">Up too24 hours of retention is supported for machines replicated toopremium storage.</span></span> <span data-ttu-id="9976c-115">Ore too72 periodo di conservazione è supportato per l'archiviazione replicata toostandard macchine.</span><span class="sxs-lookup"><span data-stu-id="9976c-115">Up too72 hours of retention is supported for machines replicated toostandard storage.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9976c-116">Viene creato automaticamente un criterio di replica per il failback.</span><span class="sxs-lookup"><span data-stu-id="9976c-116">A replication policy for failback is automatically created.</span></span>

7. <span data-ttu-id="9976c-117">In **Frequenza snapshot coerenti con l'app**specificare la frequenza, in minuti, per la creazione di punti di ripristino contenenti snapshot coerenti con l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="9976c-117">In **App-consistent snapshot frequency**, specify how often (in minutes) recovery points that contain application-consistent snapshots will be created.</span></span>

8. <span data-ttu-id="9976c-118">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="9976c-118">Click **OK**.</span></span> <span data-ttu-id="9976c-119">criteri di Hello devono essere creato in 30 secondi too60.</span><span class="sxs-lookup"><span data-stu-id="9976c-119">hello policy should be created in 30 too60 seconds.</span></span>

![Generazione dei criteri di replica](./media/site-recovery-setup-replication-settings-vmware/Creating-Policy.png)

## <a name="associate-a-configuration-server-with-a-replication-policy"></a><span data-ttu-id="9976c-121">Associare un server di configurazione ai criteri di replica</span><span class="sxs-lookup"><span data-stu-id="9976c-121">Associate a configuration server with a replication policy</span></span>
1. <span data-ttu-id="9976c-122">Scegliere toowhich criteri di replica hello si desidera tooassociate hello configurazione server.</span><span class="sxs-lookup"><span data-stu-id="9976c-122">Choose hello replication policy toowhich you want tooassociate hello configuration server.</span></span>
2. <span data-ttu-id="9976c-123">Fare clic su **Associa**.</span><span class="sxs-lookup"><span data-stu-id="9976c-123">Click **Associate**.</span></span>
<span data-ttu-id="9976c-124">![Associare i server di configurazione](./media/site-recovery-setup-replication-settings-vmware/Associate-CS-1.PNG)</span><span class="sxs-lookup"><span data-stu-id="9976c-124">![Associate configuration server](./media/site-recovery-setup-replication-settings-vmware/Associate-CS-1.PNG)</span></span>

3. <span data-ttu-id="9976c-125">Selezionare il server di configurazione di hello hello elenco dei server.</span><span class="sxs-lookup"><span data-stu-id="9976c-125">Select hello configuration server from hello list of servers.</span></span>
4. <span data-ttu-id="9976c-126">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="9976c-126">Click **OK**.</span></span> <span data-ttu-id="9976c-127">il server di configurazione di Hello deve essere associato una tootwo minuti.</span><span class="sxs-lookup"><span data-stu-id="9976c-127">hello configuration server should be associated in one tootwo minutes.</span></span>

![Associazione del server di configurazione](./media/site-recovery-setup-replication-settings-vmware/Associate-CS-2.png)

## <a name="edit-a-replication-policy"></a><span data-ttu-id="9976c-129">Modificare un criterio di replica</span><span class="sxs-lookup"><span data-stu-id="9976c-129">Edit a replication policy</span></span>
1. <span data-ttu-id="9976c-130">Scegliere il criterio di replica hello per cui si desidera tooedit le impostazioni di replica.</span><span class="sxs-lookup"><span data-stu-id="9976c-130">Choose hello replication policy for which you want tooedit replication settings.</span></span>
<span data-ttu-id="9976c-131">![Modificare i criteri di replica](./media/site-recovery-setup-replication-settings-vmware/Select-Policy.png)</span><span class="sxs-lookup"><span data-stu-id="9976c-131">![Edit replication policy](./media/site-recovery-setup-replication-settings-vmware/Select-Policy.png)</span></span>

2. <span data-ttu-id="9976c-132">Fare clic su **Edit Settings**.</span><span class="sxs-lookup"><span data-stu-id="9976c-132">Click **Edit Settings**.</span></span>
<span data-ttu-id="9976c-133">![Modificare le impostazioni dei criteri di replica](./media/site-recovery-setup-replication-settings-vmware/Edit-Policy.png)</span><span class="sxs-lookup"><span data-stu-id="9976c-133">![Edit replication policy settings](./media/site-recovery-setup-replication-settings-vmware/Edit-Policy.png)</span></span>

3. <span data-ttu-id="9976c-134">Modificare le impostazioni di hello in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="9976c-134">Change hello settings based on your need.</span></span>
4. <span data-ttu-id="9976c-135">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="9976c-135">Click **Save**.</span></span> <span data-ttu-id="9976c-136">criteri di Hello deve essere salvato in due toofive minuti, a seconda di quanti macchine virtuali utilizza tale criterio di replica.</span><span class="sxs-lookup"><span data-stu-id="9976c-136">hello policy should be saved in two toofive minutes, depending on how many VMs are using that replication policy.</span></span>

![Salvare i criteri di replica](./media/site-recovery-setup-replication-settings-vmware/Save-Policy.png)

## <a name="dissociate-a-configuration-server-from-a-replication-policy"></a><span data-ttu-id="9976c-138">Annullare l'associazione del server di configurazione dai criteri di replica</span><span class="sxs-lookup"><span data-stu-id="9976c-138">Dissociate a configuration server from a replication policy</span></span>
1. <span data-ttu-id="9976c-139">Scegliere toowhich criteri di replica hello si desidera tooassociate hello configurazione server.</span><span class="sxs-lookup"><span data-stu-id="9976c-139">Choose hello replication policy toowhich you want tooassociate hello configuration server.</span></span>
2. <span data-ttu-id="9976c-140">Fare clic su **Annulla associazione**.</span><span class="sxs-lookup"><span data-stu-id="9976c-140">Click **Dissociate**.</span></span>
3. <span data-ttu-id="9976c-141">Selezionare il server di configurazione di hello hello elenco dei server.</span><span class="sxs-lookup"><span data-stu-id="9976c-141">Select hello configuration server from hello list of servers.</span></span>
4. <span data-ttu-id="9976c-142">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="9976c-142">Click **OK**.</span></span> <span data-ttu-id="9976c-143">il server di configurazione di Hello deve dissociato in uno tootwo minuti.</span><span class="sxs-lookup"><span data-stu-id="9976c-143">hello configuration server should be dissociated in one tootwo minutes.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9976c-144">Se è presente almeno un elemento replicato mediante criteri di hello è non è possibile annullare l'associazione di un server di configurazione.</span><span class="sxs-lookup"><span data-stu-id="9976c-144">You cannot dissociate a configuration server if there is at least one replicated item using hello policy.</span></span> <span data-ttu-id="9976c-145">Assicurarsi che non sono presenti elementi replicati mediante criteri di hello prima annullare l'associazione del server di configurazione hello.</span><span class="sxs-lookup"><span data-stu-id="9976c-145">Make sure there are no replicated items using hello policy before you dissociate hello configuration server.</span></span>

## <a name="delete-a-replication-policy"></a><span data-ttu-id="9976c-146">Eliminare un criterio di replica</span><span class="sxs-lookup"><span data-stu-id="9976c-146">Delete a replication policy</span></span>

1. <span data-ttu-id="9976c-147">Scegliere il criterio di replica hello che si desidera toodelete.</span><span class="sxs-lookup"><span data-stu-id="9976c-147">Choose hello replication policy that you want toodelete.</span></span>
2. <span data-ttu-id="9976c-148">Fare clic su **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="9976c-148">Click **Delete**.</span></span> <span data-ttu-id="9976c-149">criteri di Hello devono essere eliminati in 30 secondi too60.</span><span class="sxs-lookup"><span data-stu-id="9976c-149">hello policy should be deleted in 30 too60 seconds.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9976c-150">Se dispone di almeno una configurazione server associato tooit, è possibile eliminare un criterio di replica.</span><span class="sxs-lookup"><span data-stu-id="9976c-150">You cannot delete a replication policy if it has at least one configuration server associated tooit.</span></span> <span data-ttu-id="9976c-151">Verificare che non sono presenti elementi replicati mediante criteri di hello e di eliminare che tutti hello associati server di configurazione prima di eliminare i criteri di hello.</span><span class="sxs-lookup"><span data-stu-id="9976c-151">Make sure there are no replicated items using hello policy and delete all hello associated configuration servers before you delete hello policy.</span></span>
