---
title: Configurare l'ambiente di origine (server fisici in Azure) | Documentazione Microsoft
description: Questo articolo descrive come configurare l'ambiente locale per avviare la replica in Azure di server fisici che eseguono Windows o Linux.
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
ms.openlocfilehash: 49b9d2e21dbcb612828a25f21ed4382327d6f64c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-the-source-environment-physical-server-to-azure"></a><span data-ttu-id="09e00-103">Configurare l'ambiente di origine (server fisico in Azure)</span><span class="sxs-lookup"><span data-stu-id="09e00-103">Set up the source environment (physical server to Azure)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="09e00-104">Da VMware ad Azure</span><span class="sxs-lookup"><span data-stu-id="09e00-104">VMware to Azure</span></span>](./site-recovery-set-up-vmware-to-azure.md)
> * [<span data-ttu-id="09e00-105">Da fisico ad Azure</span><span class="sxs-lookup"><span data-stu-id="09e00-105">Physical to Azure</span></span>](./site-recovery-set-up-physical-to-azure.md)

<span data-ttu-id="09e00-106">Questo articolo descrive come configurare l'ambiente locale per avviare la replica in Azure di server fisici che eseguono Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="09e00-106">This article describes how to set up your on-premises environment to start replicating physical servers running Windows or Linux into Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="09e00-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="09e00-107">Prerequisites</span></span>

<span data-ttu-id="09e00-108">Nell'articolo si presuppone che l'utente disponga di quanto segue:</span><span class="sxs-lookup"><span data-stu-id="09e00-108">The article assumes that you already have:</span></span>
1. <span data-ttu-id="09e00-109">Un insieme di credenziali di Servizi di ripristino nel [portale di Azure](http://portal.azure.com "portale di Azure").</span><span class="sxs-lookup"><span data-stu-id="09e00-109">A Recovery Services vault in the [Azure portal](http://portal.azure.com "Azure portal").</span></span>
3. <span data-ttu-id="09e00-110">Un computer fisico in cui installare il server di configurazione.</span><span class="sxs-lookup"><span data-stu-id="09e00-110">A physical computer on which to install the configuration server.</span></span>

### <a name="configuration-server-minimum-requirements"></a><span data-ttu-id="09e00-111">Requisiti minimi per il server di configurazione</span><span class="sxs-lookup"><span data-stu-id="09e00-111">Configuration server minimum requirements</span></span>
<span data-ttu-id="09e00-112">La tabella seguente elenca i requisiti minimi hardware, software e di rete per un server di configurazione.</span><span class="sxs-lookup"><span data-stu-id="09e00-112">The following table lists the minimum hardware, software, and network requirements for a configuration server.</span></span>
[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

> [!NOTE]
> <span data-ttu-id="09e00-113">I server proxy basati su HTTPS non sono supportati dal server di configurazione.</span><span class="sxs-lookup"><span data-stu-id="09e00-113">HTTPS-based proxy servers are not supported by the configuration server.</span></span>

## <a name="choose-your-protection-goals"></a><span data-ttu-id="09e00-114">Scegliere gli obiettivi della protezione</span><span class="sxs-lookup"><span data-stu-id="09e00-114">Choose your protection goals</span></span>

1. <span data-ttu-id="09e00-115">Nel portale di Azure accedere al pannello relativo agli insiemi di credenziali di **Servizi di ripristino** e selezionare l'insieme di credenziali specifico.</span><span class="sxs-lookup"><span data-stu-id="09e00-115">In the Azure portal, go to the **Recovery Services** vaults blade and select your vault.</span></span>
2. <span data-ttu-id="09e00-116">Nel menu delle **risorse** dell'insieme di credenziali fare clic su **Attività iniziali** > **Site Recovery** > **Passaggio 1: Preparare l'infrastruttura** > **Obiettivo di protezione**.</span><span class="sxs-lookup"><span data-stu-id="09e00-116">In the **Resource** menu of the vault, click **Getting Started** > **Site Recovery** > **Step 1: Prepare Infrastructure** > **Protection goal**.</span></span>

    ![Scegliere gli obiettivi](./media/site-recovery-set-up-physical-to-azure/choose-goals.png)
3. <span data-ttu-id="09e00-118">In **Obiettivo di protezione** selezionare **In Azure** e scegliere **Non virtualizzato/Altro**e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="09e00-118">In **Protection goal**, select **To Azure** and **Not virtualized/Other**, and then click **OK**.</span></span>

    ![Scegliere gli obiettivi](./media/site-recovery-set-up-physical-to-azure/physical-protection-goal.PNG)

## <a name="set-up-the-source-environment"></a><span data-ttu-id="09e00-120">Configurare l'ambiente di origine</span><span class="sxs-lookup"><span data-stu-id="09e00-120">Set up the source environment</span></span>

1. <span data-ttu-id="09e00-121">Se non è disponibile un server di configurazione, in **Prepara origine** fare clic su **+Server di configurazione** per aggiungerne uno.</span><span class="sxs-lookup"><span data-stu-id="09e00-121">In **Prepare source**, if you don’t have a configuration server, click **+Configuration server** to add one.</span></span>

  ![Impostare l'origine](./media/site-recovery-set-up-physical-to-azure/plus-config-srv.png)
2. <span data-ttu-id="09e00-123">Nel pannello **Aggiungi server** verificare che **Server di configurazione** sia visualizzato in **Tipo di server**.</span><span class="sxs-lookup"><span data-stu-id="09e00-123">In the **Add Server** blade, check that **Configuration Server** appears in **Server type**.</span></span>
4. <span data-ttu-id="09e00-124">Scaricare il file di installazione per l'Installazione unificata di Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="09e00-124">Download the Site Recovery Unified Setup installation file.</span></span>
5. <span data-ttu-id="09e00-125">Scaricare la chiave di registrazione dell'insieme di credenziali,</span><span class="sxs-lookup"><span data-stu-id="09e00-125">Download the vault registration key.</span></span> <span data-ttu-id="09e00-126">Per eseguire l'installazione unificata, è necessaria la chiave di registrazione.</span><span class="sxs-lookup"><span data-stu-id="09e00-126">You need the registration key when you run Unified Setup.</span></span> <span data-ttu-id="09e00-127">La chiave è valida per cinque giorni dal momento in cui viene generata.</span><span class="sxs-lookup"><span data-stu-id="09e00-127">The key is valid for five days after you generate it.</span></span>

    ![Impostare l'origine](./media/site-recovery-set-up-physical-to-azure/set-source2.png)
6. <span data-ttu-id="09e00-129">Nel computer usato come server di configurazione, eseguire l'**installazione unificata di Azure Site Recovery** per installare il server di configurazione, il server di elaborazione e il server master di destinazione.</span><span class="sxs-lookup"><span data-stu-id="09e00-129">On the machine you’re using as the configuration server, run **Azure Site Recovery Unified Setup** to install the configuration server, the process server, and the master target server.</span></span>

#### <a name="run-azure-site-recovery-unified-setup"></a><span data-ttu-id="09e00-130">Eseguire l'installazione unificata di Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="09e00-130">Run Azure Site Recovery Unified Setup</span></span>

> [!TIP]
> <span data-ttu-id="09e00-131">La registrazione del server di configurazione non riesce se l'ora del sistema nel computer differisce di oltre cinque minuti dall'ora locale.</span><span class="sxs-lookup"><span data-stu-id="09e00-131">Configuration server registration fails if the time on your computer's system clock is more than five minutes off of local time.</span></span> <span data-ttu-id="09e00-132">Sincronizzare l'ora del sistema con un [server di riferimento ora](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) prima di iniziare l'installazione.</span><span class="sxs-lookup"><span data-stu-id="09e00-132">Synchronize your system clock with a [time server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) before starting the installation.</span></span>

[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> <span data-ttu-id="09e00-133">Il server di configurazione può essere installato tramite una riga di comando.</span><span class="sxs-lookup"><span data-stu-id="09e00-133">The configuration server can be installed via a command line.</span></span> <span data-ttu-id="09e00-134">Per altre informazioni, vedere l'argomento relativo all'[installazione del server di configurazione con gli strumenti da riga di comando](http://aka.ms/installconfigsrv).</span><span class="sxs-lookup"><span data-stu-id="09e00-134">For more information, see [Installing configuration server using command-line tools](http://aka.ms/installconfigsrv).</span></span>


## <a name="common-issues"></a><span data-ttu-id="09e00-135">Problemi comuni</span><span class="sxs-lookup"><span data-stu-id="09e00-135">Common issues</span></span>

[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]


## <a name="next-steps"></a><span data-ttu-id="09e00-136">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="09e00-136">Next steps</span></span>

<span data-ttu-id="09e00-137">Nel prossimo passaggio viene eseguita la [configurazione dell'ambiente di destinazione](./site-recovery-prepare-target-physical-to-azure.md) in Azure.</span><span class="sxs-lookup"><span data-stu-id="09e00-137">Next step involves [setting up your target environment](./site-recovery-prepare-target-physical-to-azure.md) in Azure.</span></span>
