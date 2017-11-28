---
title: aaaSet un criterio di replica per tooAzure replica server fisico con Azure Site Recovery | Documenti Microsoft
description: "Vengono riepilogati i passaggi di hello è necessario tooset un criterio di replica quando la replica locale server fisici tooAzure di archiviazione utilizzando il servizio di Azure Site Recovery hello"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d7874bd8-6626-4668-9ec9-dbd2d26f8f81
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: d6bdeeffc24ffc8eaba24311f7c76452edb65648
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="step-8-set-up-a-replication-policy-for-physical-server-replication-tooazure"></a><span data-ttu-id="ffc67-103">Passaggio 8: Impostare un criterio di replica per tooAzure replica server fisico</span><span class="sxs-lookup"><span data-stu-id="ffc67-103">Step 8: Set up a replication policy for physical server replication tooAzure</span></span>


<span data-ttu-id="ffc67-104">Questo articolo viene descritto come tooset un criterio di replica quando si esegue la replica tooAzure server fisici Windows/Linux utilizzando hello [Azure Site Recovery](site-recovery-overview.md) di hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="ffc67-104">This article describes how tooset up a replication policy when you're replicating Windows/Linux physical servers tooAzure using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>


<span data-ttu-id="ffc67-105">Inviare commenti e domande nella parte inferiore di hello di questo articolo, o di hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="ffc67-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="configure-a-policy"></a><span data-ttu-id="ffc67-106">Configurare i criteri</span><span class="sxs-lookup"><span data-stu-id="ffc67-106">Configure a policy</span></span>

1. <span data-ttu-id="ffc67-107">Fare clic su **Infrastruttura di Site Recovery** > **Criteri di replica** > **+Criteri di replica**.</span><span class="sxs-lookup"><span data-stu-id="ffc67-107">Click **Site Recovery infrastructure** > **Replication Policies** > **+Replication Policy**.</span></span>
2. <span data-ttu-id="ffc67-108">In **Creare i criteri di replica** specificare un nome per i criteri.</span><span class="sxs-lookup"><span data-stu-id="ffc67-108">In **Create replication policy**, specify a policy name.</span></span>
3. <span data-ttu-id="ffc67-109">In **soglia RPO**, specificare il limite RPO hello.</span><span class="sxs-lookup"><span data-stu-id="ffc67-109">In **RPO threshold**, specify hello RPO limit.</span></span> <span data-ttu-id="ffc67-110">Questo valore indica la frequenza con cui vengono creati punti di ripristino dei dati.</span><span class="sxs-lookup"><span data-stu-id="ffc67-110">This value indicates how often data recovery points are created.</span></span> <span data-ttu-id="ffc67-111">Se la replica continua supera questo limite, viene generato un avviso.</span><span class="sxs-lookup"><span data-stu-id="ffc67-111">An alert is generated if continuous replication exceeds this limit.</span></span>
4. <span data-ttu-id="ffc67-112">In **conservazione del punto di ripristino**, specificare per quanto tempo (in ore) è un intervallo di conservazione hello per ogni punto di ripristino.</span><span class="sxs-lookup"><span data-stu-id="ffc67-112">In **Recovery point retention**, specify (in hours) how long hello retention window is for each recovery point.</span></span> <span data-ttu-id="ffc67-113">Macchine virtuali replicate possono essere ripristinati tooany punto in una finestra.</span><span class="sxs-lookup"><span data-stu-id="ffc67-113">Replicated VMs can be recovered tooany point in a window.</span></span> <span data-ttu-id="ffc67-114">Backup too24 conservazione ore è supportata per i computer replicati archiviazione toopremium e 72 ore per l'archiviazione standard.</span><span class="sxs-lookup"><span data-stu-id="ffc67-114">Up too24 hours retention is supported for machines replicated toopremium storage, and 72 hours for standard storage.</span></span>
5. <span data-ttu-id="ffc67-115">In **Frequenza snapshot coerenti con l'app**specificare la frequenza, in minuti, per la creazione di punti di ripristino contenenti snapshot coerenti con l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="ffc67-115">In **App-consistent snapshot frequency**, specify how often (in minutes) recovery points containing application-consistent snapshots will be created.</span></span> <span data-ttu-id="ffc67-116">Fare clic su **OK** criteri hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="ffc67-116">Click **OK** toocreate hello policy.</span></span>

    ![Criteri di replica](./media/physical-walkthrough-replication/gs-replication2.png)
8. <span data-ttu-id="ffc67-118">Quando si crea un nuovo criterio associata automaticamente con il server di configurazione di hello.</span><span class="sxs-lookup"><span data-stu-id="ffc67-118">When you create a new policy it's automatically associated with hello configuration server.</span></span> <span data-ttu-id="ffc67-119">Per impostazione predefinita vengono creati automaticamente criteri corrispondenti per il failback.</span><span class="sxs-lookup"><span data-stu-id="ffc67-119">By default, a matching policy is automatically created for failback.</span></span> <span data-ttu-id="ffc67-120">Ad esempio, se hello criterio di replica è **rep criteri** verrà utilizzato come criterio di failback hello **rep-criteri-failback**.</span><span class="sxs-lookup"><span data-stu-id="ffc67-120">For example, if hello replication policy is **rep-policy** then hello failback policy will be **rep-policy-failback**.</span></span> <span data-ttu-id="ffc67-121">Questi criteri non vengono usati fino a quando non si avvia un failback da Azure.</span><span class="sxs-lookup"><span data-stu-id="ffc67-121">This policy isn't used until you initiate a failback from Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ffc67-122">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ffc67-122">Next steps</span></span>

<span data-ttu-id="ffc67-123">Andare troppo[passaggio 9: installare il servizio Mobility hello](physical-walkthrough-install-mobility.md)</span><span class="sxs-lookup"><span data-stu-id="ffc67-123">Go too[Step 9: Install hello Mobility service](physical-walkthrough-install-mobility.md)</span></span>
