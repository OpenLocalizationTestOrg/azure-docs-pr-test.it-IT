---
title: aaaSet backup hello origine e di destinazione per i server fisici replica tooAzure con Azure Site Recovery | Documenti Microsoft
description: Riepiloga hello passaggi tooset le impostazioni di origine e di destinazione per la replica di archiviazione di server fisici tooAzure con hello servizio Azure Site Recovery
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 2e3d03bc-4e53-4590-8a01-f702d3cc9500
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: e75ef23174d77509bf54380eba8f251a7337a45f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="step-7-set-up-hello-source-and-target-for-physical-server-replication-tooazure"></a><span data-ttu-id="4bf33-103">Passaggio 7: Configurare hello origine e di destinazione per tooAzure replica server fisico</span><span class="sxs-lookup"><span data-stu-id="4bf33-103">Step 7: Set up hello source and target for physical server replication tooAzure</span></span>

<span data-ttu-id="4bf33-104">In questo articolo viene descritto come le impostazioni di tooconfigure origine e di destinazione durante la replica locale tooAzure server fisici, utilizzando hello [Azure Site Recovery](site-recovery-overview.md) di hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="4bf33-104">This article describes how tooconfigure source and target settings when replicating on-premises physical servers tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="4bf33-105">Inviare commenti e domande nella parte inferiore di hello di questo articolo, o di hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="4bf33-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="set-up-hello-source-environment"></a><span data-ttu-id="4bf33-106">Configurare un ambiente di origine hello</span><span class="sxs-lookup"><span data-stu-id="4bf33-106">Set up hello source environment</span></span>

<span data-ttu-id="4bf33-107">Configurare il server di configurazione di hello, registrarla nell'insieme di credenziali hello e individuare i computer.</span><span class="sxs-lookup"><span data-stu-id="4bf33-107">Set up hello configuration server, register it in hello vault, and discover machines.</span></span>

1. <span data-ttu-id="4bf33-108">Fare clic su **Site Recovery** > **Passaggio 1: Preparare l'infrastruttura** > **Origine**.</span><span class="sxs-lookup"><span data-stu-id="4bf33-108">Click **Site Recovery** > **Step 1: Prepare Infrastructure** > **Source**.</span></span>
2. <span data-ttu-id="4bf33-109">Se non è disponibile un server di configurazione, fare clic su **+Server di configurazione**.</span><span class="sxs-lookup"><span data-stu-id="4bf33-109">If you don’t have a configuration server, click **+Configuration server**.</span></span>
3. <span data-ttu-id="4bf33-110">In **Aggiungi server** verificare che **Tipo di server** contenga **Server di configurazione**.</span><span class="sxs-lookup"><span data-stu-id="4bf33-110">In **Add Server**, check that **Configuration Server** appears in **Server type**.</span></span>
4. <span data-ttu-id="4bf33-111">Scaricare i file di installazione di hello installazione unificata di Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="4bf33-111">Download hello Site Recovery Unified Setup installation file.</span></span>
5. <span data-ttu-id="4bf33-112">Scaricare la chiave di registrazione dell'insieme di credenziali di hello.</span><span class="sxs-lookup"><span data-stu-id="4bf33-112">Download hello vault registration key.</span></span> <span data-ttu-id="4bf33-113">che sarà necessaria quando si esegue l'Installazione unificata.</span><span class="sxs-lookup"><span data-stu-id="4bf33-113">You need this when you run Unified Setup.</span></span> <span data-ttu-id="4bf33-114">chiave di Hello è valida per cinque giorni dopo la generazione è.</span><span class="sxs-lookup"><span data-stu-id="4bf33-114">hello key is valid for five days after you generate it.</span></span>

   ![Impostare l'origine](./media/vmware-walkthrough-source-target/set-source2.png)


## <a name="register-hello-configuration-server-in-hello-vault"></a><span data-ttu-id="4bf33-116">Registrare il server di configurazione di hello nell'insieme di credenziali hello</span><span class="sxs-lookup"><span data-stu-id="4bf33-116">Register hello configuration server in hello vault</span></span>

<span data-ttu-id="4bf33-117">Seguito hello prima di avviare, quindi eseguire il programma di installazione unificata tooinstall hello configurazione server, il server di elaborazione hello e il server di destinazione master hello.</span><span class="sxs-lookup"><span data-stu-id="4bf33-117">Do hello following before you start, then run Unified Setup tooinstall hello configuration server, hello process server, and hello master target server.</span></span> <span data-ttu-id="4bf33-118">Hello video viene illustrata l'impostazione per i componenti per la replica VMware VM tooAzure hello.</span><span class="sxs-lookup"><span data-stu-id="4bf33-118">hello video describes setting up hello components for VMware VM tooAzure replication.</span></span> <span data-ttu-id="4bf33-119">Tuttavia, hello stesso processo è valido per la replica tooAzure server fisico.</span><span class="sxs-lookup"><span data-stu-id="4bf33-119">However, hello same process is valid for physical server tooAzure replication.</span></span>

- <span data-ttu-id="4bf33-120">Nel server di configurazione hello VM, verificare che l'orologio di sistema hello è sincronizzato con un [tempo Server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service).</span><span class="sxs-lookup"><span data-stu-id="4bf33-120">On hello configuration server VM, make sure that hello system clock is synchronized with a [Time Server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service).</span></span> <span data-ttu-id="4bf33-121">Deve corrispondere.</span><span class="sxs-lookup"><span data-stu-id="4bf33-121">It should match.</span></span> <span data-ttu-id="4bf33-122">Se è avanti o indietro di 15 minuti, l'installazione potrebbe avere esito negativo.</span><span class="sxs-lookup"><span data-stu-id="4bf33-122">If it's 15 minutes in front or behind, setup might fail.</span></span>
- <span data-ttu-id="4bf33-123">Eseguire l'installazione come amministratore locale nel computer server di configurazione hello.</span><span class="sxs-lookup"><span data-stu-id="4bf33-123">Run setup as a Local Administrator on hello configuration server machine.</span></span>
- <span data-ttu-id="4bf33-124">Assicurarsi che sia abilitato TLS 1.0 su hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="4bf33-124">Make sure TLS 1.0 is enabled on hello VM.</span></span>


[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> <span data-ttu-id="4bf33-125">può anche essere installato il server di configurazione di Hello [dalla riga di comando hello](http://aka.ms/installconfigsrv).</span><span class="sxs-lookup"><span data-stu-id="4bf33-125">hello configuration server can also be installed [from hello command line](http://aka.ms/installconfigsrv).</span></span>




## <a name="set-up-hello-target-environment"></a><span data-ttu-id="4bf33-126">Configurare un ambiente di destinazione hello</span><span class="sxs-lookup"><span data-stu-id="4bf33-126">Set up hello target environment</span></span>

<span data-ttu-id="4bf33-127">Prima configurare un ambiente di destinazione hello, verificare di che disporre di un account di archiviazione di Azure e una configurazione di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="4bf33-127">Before you set up hello target environment, make sure you have an Azure storage account and virtual network set up.</span></span>

1. <span data-ttu-id="4bf33-128">Fare clic su **Prepare infrastruttura** > **destinazione**, e selezionare hello sottoscrizione di Azure da toouse.</span><span class="sxs-lookup"><span data-stu-id="4bf33-128">Click **Prepare infrastructure** > **Target**, and select hello Azure subscription you want toouse.</span></span>
2. <span data-ttu-id="4bf33-129">Specificare se per la destinazione deve essere usato il modello di distribuzione classica o Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="4bf33-129">Specify whether your target deployment model is Resource Manager-based, or classic.</span></span>
3. <span data-ttu-id="4bf33-130">Site Recovery verifica la disponibilità di uno o più account di archiviazione di Azure e reti compatibili.</span><span class="sxs-lookup"><span data-stu-id="4bf33-130">Site Recovery checks that you have one or more compatible Azure storage accounts and networks.</span></span>

   ![Destinazione](./media/physical-walkthrough-source-target/gs-target.png)

4. <span data-ttu-id="4bf33-132">Se è stata creata una rete o un account di archiviazione, fare clic su **+ account di archiviazione** o **+ rete**, toocreate un inline di account o rete di gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="4bf33-132">If you haven't created a storage account or network, click **+Storage account** or **+Network**, toocreate a Resource Manager account or network inline.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4bf33-133">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4bf33-133">Next steps</span></span>

<span data-ttu-id="4bf33-134">Andare troppo[passaggio 8: impostare un criterio di replica](physical-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="4bf33-134">Go too[Step 8: Set up a replication policy](physical-walkthrough-replication.md)</span></span>
