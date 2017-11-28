---
title: Configurare un ambiente di origine hello (tooAzure server fisici) | Documenti Microsoft
description: Questo articolo viene descritto come tooset backup il toostart ambiente locale la replica di server fisici che eseguono Windows o Linux in Azure.
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
ms.openlocfilehash: d4702265bf36910015685d2bba99d6e577531bd0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-hello-source-environment-physical-server-tooazure"></a><span data-ttu-id="b4c24-103">Configurare un ambiente di origine hello (server fisico tooAzure)</span><span class="sxs-lookup"><span data-stu-id="b4c24-103">Set up hello source environment (physical server tooAzure)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b4c24-104">VMware tooAzure</span><span class="sxs-lookup"><span data-stu-id="b4c24-104">VMware tooAzure</span></span>](./site-recovery-set-up-vmware-to-azure.md)
> * [<span data-ttu-id="b4c24-105">TooAzure fisico</span><span class="sxs-lookup"><span data-stu-id="b4c24-105">Physical tooAzure</span></span>](./site-recovery-set-up-physical-to-azure.md)

<span data-ttu-id="b4c24-106">Questo articolo viene descritto come tooset backup il toostart ambiente locale la replica di server fisici che eseguono Windows o Linux in Azure.</span><span class="sxs-lookup"><span data-stu-id="b4c24-106">This article describes how tooset up your on-premises environment toostart replicating physical servers running Windows or Linux into Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b4c24-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b4c24-107">Prerequisites</span></span>

<span data-ttu-id="b4c24-108">articolo Hello si presuppone che esista già:</span><span class="sxs-lookup"><span data-stu-id="b4c24-108">hello article assumes that you already have:</span></span>
1. <span data-ttu-id="b4c24-109">Un insieme di credenziali di servizi di ripristino in hello [portale di Azure](http://portal.azure.com "portale di Azure").</span><span class="sxs-lookup"><span data-stu-id="b4c24-109">A Recovery Services vault in hello [Azure portal](http://portal.azure.com "Azure portal").</span></span>
3. <span data-ttu-id="b4c24-110">Un computer fisico nel quale server di configurazione tooinstall hello.</span><span class="sxs-lookup"><span data-stu-id="b4c24-110">A physical computer on which tooinstall hello configuration server.</span></span>

### <a name="configuration-server-minimum-requirements"></a><span data-ttu-id="b4c24-111">Requisiti minimi per il server di configurazione</span><span class="sxs-lookup"><span data-stu-id="b4c24-111">Configuration server minimum requirements</span></span>
<span data-ttu-id="b4c24-112">Hello nella tabella seguente sono elencati i requisiti hardware minimi hello, software e requisiti di rete per un server di configurazione.</span><span class="sxs-lookup"><span data-stu-id="b4c24-112">hello following table lists hello minimum hardware, software, and network requirements for a configuration server.</span></span>
[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

> [!NOTE]
> <span data-ttu-id="b4c24-113">Server proxy basato su HTTPS non sono supportati dal server di configurazione hello.</span><span class="sxs-lookup"><span data-stu-id="b4c24-113">HTTPS-based proxy servers are not supported by hello configuration server.</span></span>

## <a name="choose-your-protection-goals"></a><span data-ttu-id="b4c24-114">Scegliere gli obiettivi della protezione</span><span class="sxs-lookup"><span data-stu-id="b4c24-114">Choose your protection goals</span></span>

1. <span data-ttu-id="b4c24-115">Nel portale di Azure hello, passare toohello **servizi di ripristino** insiemi di credenziali di blade e selezionare l'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="b4c24-115">In hello Azure portal, go toohello **Recovery Services** vaults blade and select your vault.</span></span>
2. <span data-ttu-id="b4c24-116">In hello **risorse** menu dell'insieme di credenziali di hello, fare clic su **Introduzione** > **Site Recovery** > **passaggio 1: preparare Infrastruttura** > **obiettivi della protezione dati**.</span><span class="sxs-lookup"><span data-stu-id="b4c24-116">In hello **Resource** menu of hello vault, click **Getting Started** > **Site Recovery** > **Step 1: Prepare Infrastructure** > **Protection goal**.</span></span>

    ![Scegliere gli obiettivi](./media/site-recovery-set-up-physical-to-azure/choose-goals.png)
3. <span data-ttu-id="b4c24-118">In **obiettivi della protezione dati**selezionare **tooAzure** e **non virtualizzato/altri**, quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="b4c24-118">In **Protection goal**, select **tooAzure** and **Not virtualized/Other**, and then click **OK**.</span></span>

    ![Scegliere gli obiettivi](./media/site-recovery-set-up-physical-to-azure/physical-protection-goal.PNG)

## <a name="set-up-hello-source-environment"></a><span data-ttu-id="b4c24-120">Configurare un ambiente di origine hello</span><span class="sxs-lookup"><span data-stu-id="b4c24-120">Set up hello source environment</span></span>

1. <span data-ttu-id="b4c24-121">In **origine Prepare**, se non è un server di configurazione, fare clic su **+ server di configurazione** tooadd uno.</span><span class="sxs-lookup"><span data-stu-id="b4c24-121">In **Prepare source**, if you don’t have a configuration server, click **+Configuration server** tooadd one.</span></span>

  ![Impostare l'origine](./media/site-recovery-set-up-physical-to-azure/plus-config-srv.png)
2. <span data-ttu-id="b4c24-123">In hello **Aggiungi Server** pannello, verificare che **Server di configurazione** viene visualizzato **tipo Server**.</span><span class="sxs-lookup"><span data-stu-id="b4c24-123">In hello **Add Server** blade, check that **Configuration Server** appears in **Server type**.</span></span>
4. <span data-ttu-id="b4c24-124">Scaricare i file di installazione di hello installazione unificata di Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="b4c24-124">Download hello Site Recovery Unified Setup installation file.</span></span>
5. <span data-ttu-id="b4c24-125">Scaricare la chiave di registrazione dell'insieme di credenziali di hello.</span><span class="sxs-lookup"><span data-stu-id="b4c24-125">Download hello vault registration key.</span></span> <span data-ttu-id="b4c24-126">Chiave di registrazione hello è necessario quando si esegue il programma di installazione unificata.</span><span class="sxs-lookup"><span data-stu-id="b4c24-126">You need hello registration key when you run Unified Setup.</span></span> <span data-ttu-id="b4c24-127">chiave di Hello è valida per cinque giorni dopo la generazione è.</span><span class="sxs-lookup"><span data-stu-id="b4c24-127">hello key is valid for five days after you generate it.</span></span>

    ![Impostare l'origine](./media/site-recovery-set-up-physical-to-azure/set-source2.png)
6. <span data-ttu-id="b4c24-129">Nel computer in uso come server di configurazione hello hello eseguire **installazione unificata di Azure Site Recovery** tooinstall hello configurazione server, server process hello e master hello server di destinazione.</span><span class="sxs-lookup"><span data-stu-id="b4c24-129">On hello machine you’re using as hello configuration server, run **Azure Site Recovery Unified Setup** tooinstall hello configuration server, hello process server, and hello master target server.</span></span>

#### <a name="run-azure-site-recovery-unified-setup"></a><span data-ttu-id="b4c24-130">Eseguire l'Installazione unificata di Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="b4c24-130">Run Azure Site Recovery Unified Setup</span></span>

> [!TIP]
> <span data-ttu-id="b4c24-131">Registrazione del server di configurazione non riesce se il tempo di hello clock di sistema del computer più di cinque minuti dall'ora locale.</span><span class="sxs-lookup"><span data-stu-id="b4c24-131">Configuration server registration fails if hello time on your computer's system clock is more than five minutes off of local time.</span></span> <span data-ttu-id="b4c24-132">Sincronizzare l'orologio di sistema con un [server ora](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) prima di avviare l'installazione di hello.</span><span class="sxs-lookup"><span data-stu-id="b4c24-132">Synchronize your system clock with a [time server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) before starting hello installation.</span></span>

[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> <span data-ttu-id="b4c24-133">il server di configurazione di Hello può essere installato tramite una riga di comando.</span><span class="sxs-lookup"><span data-stu-id="b4c24-133">hello configuration server can be installed via a command line.</span></span> <span data-ttu-id="b4c24-134">Per altre informazioni, vedere l'argomento relativo all'[installazione del server di configurazione con gli strumenti da riga di comando](http://aka.ms/installconfigsrv).</span><span class="sxs-lookup"><span data-stu-id="b4c24-134">For more information, see [Installing configuration server using command-line tools](http://aka.ms/installconfigsrv).</span></span>


## <a name="common-issues"></a><span data-ttu-id="b4c24-135">Problemi comuni</span><span class="sxs-lookup"><span data-stu-id="b4c24-135">Common issues</span></span>

[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]


## <a name="next-steps"></a><span data-ttu-id="b4c24-136">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b4c24-136">Next steps</span></span>

<span data-ttu-id="b4c24-137">Nel prossimo passaggio viene eseguita la [configurazione dell'ambiente di destinazione](./site-recovery-prepare-target-physical-to-azure.md) in Azure.</span><span class="sxs-lookup"><span data-stu-id="b4c24-137">Next step involves [setting up your target environment](./site-recovery-prepare-target-physical-to-azure.md) in Azure.</span></span>
