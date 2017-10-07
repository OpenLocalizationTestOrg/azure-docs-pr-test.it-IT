---
title: Configurare un ambiente di origine hello (VMware tooAzure) | Documenti Microsoft
description: In questo articolo viene descritto come tooset backup il toostart ambiente locale la replica VMware virtual macchine tooAzure.
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
ms.openlocfilehash: cbeeffc1061b11223e12ff3e237fa7e55b999aca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-hello-source-environment-vmware-tooazure"></a><span data-ttu-id="3eb1d-103">Configurare un ambiente di origine hello (tooAzure VMware)</span><span class="sxs-lookup"><span data-stu-id="3eb1d-103">Set up hello source environment (VMware tooAzure)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3eb1d-104">VMware tooAzure</span><span class="sxs-lookup"><span data-stu-id="3eb1d-104">VMware tooAzure</span></span>](./site-recovery-set-up-vmware-to-azure.md)
> * [<span data-ttu-id="3eb1d-105">TooAzure fisico</span><span class="sxs-lookup"><span data-stu-id="3eb1d-105">Physical tooAzure</span></span>](./site-recovery-set-up-physical-to-azure.md)

<span data-ttu-id="3eb1d-106">In questo articolo viene descritto come tooset backup il toostart ambiente locale replica virtuale dei computer in esecuzione su VMware tooAzure.</span><span class="sxs-lookup"><span data-stu-id="3eb1d-106">This article describes how tooset up your on-premises environment toostart replicating virtual machines running on VMware tooAzure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3eb1d-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="3eb1d-107">Prerequisites</span></span>

<span data-ttu-id="3eb1d-108">Hello si presume che sia già stato creato:</span><span class="sxs-lookup"><span data-stu-id="3eb1d-108">hello article assumes that you have already created:</span></span>
- <span data-ttu-id="3eb1d-109">Un archivio di servizi di ripristino in hello [portale di Azure](http://portal.azure.com "portale di Azure").</span><span class="sxs-lookup"><span data-stu-id="3eb1d-109">A Recovery Services Vault in hello [Azure portal](http://portal.azure.com "Azure portal").</span></span>
- <span data-ttu-id="3eb1d-110">Account dedicato in VMware vCenter che può essere usato per l'[individuazione automatica](./site-recovery-vmware-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="3eb1d-110">A dedicated account in your VMware vCenter that can be used for [automatic discovery](./site-recovery-vmware-to-azure.md).</span></span>
- <span data-ttu-id="3eb1d-111">Una macchina virtuale nel server di configurazione che tooinstall hello.</span><span class="sxs-lookup"><span data-stu-id="3eb1d-111">A virtual machine on which tooinstall hello configuration server.</span></span>

## <a name="configuration-server-minimum-requirements"></a><span data-ttu-id="3eb1d-112">Requisiti minimi per il server di configurazione</span><span class="sxs-lookup"><span data-stu-id="3eb1d-112">Configuration server minimum requirements</span></span>
<span data-ttu-id="3eb1d-113">software server di configurazione Hello deve essere distribuiti in una macchina virtuale di VMware a disponibilità elevata.</span><span class="sxs-lookup"><span data-stu-id="3eb1d-113">hello configuration server software should be deployed on a highly available VMware virtual machine.</span></span> <span data-ttu-id="3eb1d-114">Hello nella tabella seguente sono elencati i requisiti hardware minimi hello, software e requisiti di rete per un server di configurazione.</span><span class="sxs-lookup"><span data-stu-id="3eb1d-114">hello following table lists hello minimum hardware, software, and network requirements for a configuration server.</span></span>
[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

> [!NOTE]
> <span data-ttu-id="3eb1d-115">Server proxy basato su HTTPS non sono supportati dal server di configurazione hello.</span><span class="sxs-lookup"><span data-stu-id="3eb1d-115">HTTPS-based proxy servers are not supported by hello configuration server.</span></span>

## <a name="choose-your-protection-goals"></a><span data-ttu-id="3eb1d-116">Scegliere gli obiettivi della protezione</span><span class="sxs-lookup"><span data-stu-id="3eb1d-116">Choose your protection goals</span></span>

1. <span data-ttu-id="3eb1d-117">Nel portale di Azure hello, passare toohello **servizi di ripristino** pannello dell'insieme di credenziali e selezionare l'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="3eb1d-117">In hello Azure portal, go toohello **Recovery Services** vault blade and select your vault.</span></span>
2. <span data-ttu-id="3eb1d-118">Menu hello risorsa dell'insieme di credenziali hello andare troppo**Introduzione** > **Site Recovery** > **passaggio 1: preparare l'infrastruttura**  >  **Obiettivi della protezione dati**.</span><span class="sxs-lookup"><span data-stu-id="3eb1d-118">On hello resource menu of hello vault, go too**Getting Started** > **Site Recovery** > **Step 1: Prepare Infrastructure** > **Protection goal**.</span></span>

    ![Scegliere gli obiettivi](./media/site-recovery-set-up-vmware-to-azure/choose-goals.png)
3. <span data-ttu-id="3eb1d-120">In **obiettivi della protezione dati**selezionare **tooAzure**e scegliere **Sì, con VMware vSphere Hypervisor**.</span><span class="sxs-lookup"><span data-stu-id="3eb1d-120">In **Protection goal**, select **tooAzure**, and choose **Yes, with VMware vSphere Hypervisor**.</span></span> <span data-ttu-id="3eb1d-121">Fare quindi clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="3eb1d-121">Then click **OK**.</span></span>

    ![Scegliere gli obiettivi](./media/site-recovery-set-up-vmware-to-azure/choose-goals2.png)

## <a name="set-up-hello-source-environment"></a><span data-ttu-id="3eb1d-123">Configurare un ambiente di origine hello</span><span class="sxs-lookup"><span data-stu-id="3eb1d-123">Set up hello source environment</span></span>
<span data-ttu-id="3eb1d-124">L'impostazione di ambiente di origine hello comporta due attività principali:</span><span class="sxs-lookup"><span data-stu-id="3eb1d-124">Setting up hello source environment involves two main activities:</span></span>

- <span data-ttu-id="3eb1d-125">Installare e registrare un server di configurazione con Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="3eb1d-125">Install and register a configuration server with Site Recovery.</span></span>
- <span data-ttu-id="3eb1d-126">Individuare le macchine virtuali in locale tramite la connessione a Site Recovery tooyour locale VMware vCenter o vSphere EXSi host.</span><span class="sxs-lookup"><span data-stu-id="3eb1d-126">Discover your on-premises virtual machines by connecting Site Recovery tooyour on-premises VMware vCenter or vSphere EXSi hosts.</span></span>

### <a name="step-1-install-and-register-a-configuration-server"></a><span data-ttu-id="3eb1d-127">Passaggio 1: Installare e registrare un server di configurazione</span><span class="sxs-lookup"><span data-stu-id="3eb1d-127">Step 1: Install and register a configuration server</span></span>

1. <span data-ttu-id="3eb1d-128">Fare clic su **Passaggio 1: Preparare l'infrastruttura** > **Origine**.</span><span class="sxs-lookup"><span data-stu-id="3eb1d-128">Click **Step 1: Prepare Infrastructure** > **Source**.</span></span> <span data-ttu-id="3eb1d-129">In **origine Prepare**, se non è un server di configurazione, fare clic su **+ server di configurazione** tooadd uno.</span><span class="sxs-lookup"><span data-stu-id="3eb1d-129">In **Prepare source**, if you don’t have a configuration server, click **+Configuration server** tooadd one.</span></span>

    ![Impostare l'origine](./media/site-recovery-set-up-vmware-to-azure/set-source1.png)
2. <span data-ttu-id="3eb1d-131">In hello **Aggiungi Server** pannello, verificare che **Server di configurazione** viene visualizzato **tipo Server**.</span><span class="sxs-lookup"><span data-stu-id="3eb1d-131">On hello **Add Server** blade, check that **Configuration Server** appears in **Server type**.</span></span>
4. <span data-ttu-id="3eb1d-132">Scaricare i file di installazione di hello installazione unificata di Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="3eb1d-132">Download hello Site Recovery Unified Setup installation file.</span></span>
5. <span data-ttu-id="3eb1d-133">Scaricare la chiave di registrazione dell'insieme di credenziali di hello.</span><span class="sxs-lookup"><span data-stu-id="3eb1d-133">Download hello vault registration key.</span></span> <span data-ttu-id="3eb1d-134">Chiave di registrazione hello è necessario quando si esegue il programma di installazione unificata.</span><span class="sxs-lookup"><span data-stu-id="3eb1d-134">You need hello registration key when you run Unified Setup.</span></span> <span data-ttu-id="3eb1d-135">chiave di Hello è valida per cinque giorni dopo la generazione è.</span><span class="sxs-lookup"><span data-stu-id="3eb1d-135">hello key is valid for five days after you generate it.</span></span>

    ![Impostare l'origine](./media/site-recovery-set-up-vmware-to-azure/set-source2.png)
6. <span data-ttu-id="3eb1d-137">Nel computer in uso come server di configurazione hello hello eseguire **installazione unificata di Azure Site Recovery** tooinstall hello configurazione server, server process hello e master hello server di destinazione.</span><span class="sxs-lookup"><span data-stu-id="3eb1d-137">On hello machine you’re using as hello configuration server, run **Azure Site Recovery Unified Setup** tooinstall hello configuration server, hello process server, and hello master target server.</span></span>

#### <a name="run-azure-site-recovery-unified-setup"></a><span data-ttu-id="3eb1d-138">Eseguire l'Installazione unificata di Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="3eb1d-138">Run Azure Site Recovery Unified Setup</span></span>

> [!TIP]
> <span data-ttu-id="3eb1d-139">Registrazione del server di configurazione non riesce se il tempo di hello clock di sistema del computer è diverso dall'ora locale da più di cinque minuti.</span><span class="sxs-lookup"><span data-stu-id="3eb1d-139">Configuration server registration fails if hello time on your computer's system clock differs from local time by more than five minutes.</span></span> <span data-ttu-id="3eb1d-140">Sincronizzare l'orologio di sistema con un [Server ora](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) prima di avviare l'installazione di hello.</span><span class="sxs-lookup"><span data-stu-id="3eb1d-140">Synchronize your system clock with a [Time Server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) before starting hello installation.</span></span>

[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> <span data-ttu-id="3eb1d-141">il server di configurazione di Hello può essere installato tramite riga di comando.</span><span class="sxs-lookup"><span data-stu-id="3eb1d-141">hello configuration server can be installed via command line.</span></span> <span data-ttu-id="3eb1d-142">Per ulteriori informazioni, vedere [installare server di configurazione di hello utilizzando gli strumenti da riga di comando](http://aka.ms/installconfigsrv).</span><span class="sxs-lookup"><span data-stu-id="3eb1d-142">For more information, see [Installing hello configuration server using Command-line tools](http://aka.ms/installconfigsrv).</span></span>

#### <a name="add-hello-vmware-account-for-automatic-discovery"></a><span data-ttu-id="3eb1d-143">Aggiungere hello VMware account per l'individuazione automatica</span><span class="sxs-lookup"><span data-stu-id="3eb1d-143">Add hello VMware account for automatic discovery</span></span>

[!INCLUDE [site-recovery-add-vcenter-account](../../includes/site-recovery-add-vcenter-account.md)]

### <a name="step-2-add-a-vcenter"></a><span data-ttu-id="3eb1d-144">Passaggio 2 - Aggiungere un vCenter</span><span class="sxs-lookup"><span data-stu-id="3eb1d-144">Step 2: Add a vCenter</span></span>
<span data-ttu-id="3eb1d-145">macchine virtuali toodiscover Azure Site Recovery tooallow in esecuzione nell'ambiente locale, è necessario tooconnect il Server VMware vCenter o l'host ESXi vSphere con il ripristino del sito.</span><span class="sxs-lookup"><span data-stu-id="3eb1d-145">tooallow Azure Site Recovery toodiscover virtual machines running in your on-premises environment, you need tooconnect your VMware vCenter Server or vSphere ESXi hosts with Site Recovery.</span></span>

<span data-ttu-id="3eb1d-146">Selezionare **+ vCenter** toostart la connessione a un server VMware vCenter o un host VMware vSphere ESXi.</span><span class="sxs-lookup"><span data-stu-id="3eb1d-146">Select **+vCenter** toostart connecting a VMware vCenter server or a VMware vSphere ESXi host.</span></span>

[!INCLUDE [site-recovery-add-vcenter](../../includes/site-recovery-add-vcenter.md)]


## <a name="common-issues"></a><span data-ttu-id="3eb1d-147">Problemi comuni</span><span class="sxs-lookup"><span data-stu-id="3eb1d-147">Common issues</span></span>
[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]


## <a name="next-steps"></a><span data-ttu-id="3eb1d-148">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3eb1d-148">Next steps</span></span>
<span data-ttu-id="3eb1d-149">[Configurare l'ambiente di destinazione](./site-recovery-prepare-target-vmware-to-azure.md) in Azure.</span><span class="sxs-lookup"><span data-stu-id="3eb1d-149">[Set up your target environment](./site-recovery-prepare-target-vmware-to-azure.md) in Azure.</span></span>
