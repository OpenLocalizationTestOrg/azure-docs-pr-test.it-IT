---
title: Impostare l'origine e la destinazione per la replica del server fisico in Azure con Azure Site Recovery | Microsoft Docs
description: Vengono riepilogati i passaggi per configurare le impostazioni di origine e di destinazione per la replica dei server fisici in Archiviazione di Azure con il servizio Azure Site Recovery
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
ms.openlocfilehash: e89bbf5a2c1d71852e49da43d3106a05ebfc28a8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="step-7-set-up-the-source-and-target-for-physical-server-replication-to-azure"></a><span data-ttu-id="42fcf-103">Passaggio 7: Configurare l'origine e la destinazione per la replica del server fisico in Azure</span><span class="sxs-lookup"><span data-stu-id="42fcf-103">Step 7: Set up the source and target for physical server replication to Azure</span></span>

<span data-ttu-id="42fcf-104">Questo articolo illustra come configurare le impostazioni di origine e di destinazione per la replica di server fisici locali in Azure, usando il servizio [Azure Site Recovery](site-recovery-overview.md) nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="42fcf-104">This article describes how to configure source and target settings when replicating on-premises physical servers to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="42fcf-105">Inserire commenti e domande nella parte inferiore di questo articolo oppure nel [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="42fcf-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="set-up-the-source-environment"></a><span data-ttu-id="42fcf-106">Configurare l'ambiente di origine</span><span class="sxs-lookup"><span data-stu-id="42fcf-106">Set up the source environment</span></span>

<span data-ttu-id="42fcf-107">Configurare il server di configurazione, registrarlo nell'insieme di credenziali e individuare le macchine.</span><span class="sxs-lookup"><span data-stu-id="42fcf-107">Set up the configuration server, register it in the vault, and discover machines.</span></span>

1. <span data-ttu-id="42fcf-108">Fare clic su **Site Recovery** > **Passaggio 1: Preparare l'infrastruttura** > **Origine**.</span><span class="sxs-lookup"><span data-stu-id="42fcf-108">Click **Site Recovery** > **Step 1: Prepare Infrastructure** > **Source**.</span></span>
2. <span data-ttu-id="42fcf-109">Se non è disponibile un server di configurazione, fare clic su **+Server di configurazione**.</span><span class="sxs-lookup"><span data-stu-id="42fcf-109">If you don’t have a configuration server, click **+Configuration server**.</span></span>
3. <span data-ttu-id="42fcf-110">In **Aggiungi server** verificare che **Tipo di server** contenga **Server di configurazione**.</span><span class="sxs-lookup"><span data-stu-id="42fcf-110">In **Add Server**, check that **Configuration Server** appears in **Server type**.</span></span>
4. <span data-ttu-id="42fcf-111">Scaricare il file di installazione per l'Installazione unificata di Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="42fcf-111">Download the Site Recovery Unified Setup installation file.</span></span>
5. <span data-ttu-id="42fcf-112">Scaricare la chiave di registrazione dell'insieme di credenziali,</span><span class="sxs-lookup"><span data-stu-id="42fcf-112">Download the vault registration key.</span></span> <span data-ttu-id="42fcf-113">che sarà necessaria quando si esegue l'Installazione unificata.</span><span class="sxs-lookup"><span data-stu-id="42fcf-113">You need this when you run Unified Setup.</span></span> <span data-ttu-id="42fcf-114">La chiave è valida per cinque giorni dal momento in cui viene generata.</span><span class="sxs-lookup"><span data-stu-id="42fcf-114">The key is valid for five days after you generate it.</span></span>

   ![Impostare l'origine](./media/vmware-walkthrough-source-target/set-source2.png)


## <a name="register-the-configuration-server-in-the-vault"></a><span data-ttu-id="42fcf-116">Registrare il server di configurazione nell'insieme di credenziali</span><span class="sxs-lookup"><span data-stu-id="42fcf-116">Register the configuration server in the vault</span></span>

<span data-ttu-id="42fcf-117">Seguire questa procedura prima di iniziare, quindi eseguire l'Installazione unificata per installare il server di configurazione, il server di elaborazione e il server di destinazione master.</span><span class="sxs-lookup"><span data-stu-id="42fcf-117">Do the following before you start, then run Unified Setup to install the configuration server, the process server, and the master target server.</span></span> <span data-ttu-id="42fcf-118">Il video illustra l'impostazione dei componenti per la replica della macchina virtuale di VMware in Azure.</span><span class="sxs-lookup"><span data-stu-id="42fcf-118">The video describes setting up the components for VMware VM to Azure replication.</span></span> <span data-ttu-id="42fcf-119">Lo stesso processo, tuttavia, è valido anche per la replica del server fisico in Azure.</span><span class="sxs-lookup"><span data-stu-id="42fcf-119">However, the same process is valid for physical server to Azure replication.</span></span>

- <span data-ttu-id="42fcf-120">Nella VM del server di configurazione verificare che il clock di sistema sia sincronizzato con un [server di riferimento ora](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service).</span><span class="sxs-lookup"><span data-stu-id="42fcf-120">On the configuration server VM, make sure that the system clock is synchronized with a [Time Server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service).</span></span> <span data-ttu-id="42fcf-121">Deve corrispondere.</span><span class="sxs-lookup"><span data-stu-id="42fcf-121">It should match.</span></span> <span data-ttu-id="42fcf-122">Se è avanti o indietro di 15 minuti, l'installazione potrebbe avere esito negativo.</span><span class="sxs-lookup"><span data-stu-id="42fcf-122">If it's 15 minutes in front or behind, setup might fail.</span></span>
- <span data-ttu-id="42fcf-123">Eseguire l'installazione come amministratore locale nel server di configurazione.</span><span class="sxs-lookup"><span data-stu-id="42fcf-123">Run setup as a Local Administrator on the configuration server machine.</span></span>
- <span data-ttu-id="42fcf-124">Verificare che nella VM sia abilitato TLS 1.0.</span><span class="sxs-lookup"><span data-stu-id="42fcf-124">Make sure TLS 1.0 is enabled on the VM.</span></span>


[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> <span data-ttu-id="42fcf-125">Il server di configurazione può essere installato anche [dalla riga di comando](http://aka.ms/installconfigsrv).</span><span class="sxs-lookup"><span data-stu-id="42fcf-125">The configuration server can also be installed [from the command line](http://aka.ms/installconfigsrv).</span></span>




## <a name="set-up-the-target-environment"></a><span data-ttu-id="42fcf-126">Configurare l'ambiente di destinazione</span><span class="sxs-lookup"><span data-stu-id="42fcf-126">Set up the target environment</span></span>

<span data-ttu-id="42fcf-127">Prima di configurare l'ambiente di destinazione, verificare di aver configurato una rete virtuale e un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="42fcf-127">Before you set up the target environment, make sure you have an Azure storage account and virtual network set up.</span></span>

1. <span data-ttu-id="42fcf-128">Fare clic su **Preparare l'infrastruttura** > **Destinazione** e selezionare la sottoscrizione di Azure da usare.</span><span class="sxs-lookup"><span data-stu-id="42fcf-128">Click **Prepare infrastructure** > **Target**, and select the Azure subscription you want to use.</span></span>
2. <span data-ttu-id="42fcf-129">Specificare se per la destinazione deve essere usato il modello di distribuzione classica o Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="42fcf-129">Specify whether your target deployment model is Resource Manager-based, or classic.</span></span>
3. <span data-ttu-id="42fcf-130">Site Recovery verifica la disponibilità di uno o più account di archiviazione di Azure e reti compatibili.</span><span class="sxs-lookup"><span data-stu-id="42fcf-130">Site Recovery checks that you have one or more compatible Azure storage accounts and networks.</span></span>

   ![Destinazione](./media/physical-walkthrough-source-target/gs-target.png)

4. <span data-ttu-id="42fcf-132">Se non si è creato un account di archiviazione o una rete, fare clic su **+Account di archiviazione** o **+Rete** per creare una rete o un account Resource Manager inline.</span><span class="sxs-lookup"><span data-stu-id="42fcf-132">If you haven't created a storage account or network, click **+Storage account** or **+Network**, to create a Resource Manager account or network inline.</span></span>

## <a name="next-steps"></a><span data-ttu-id="42fcf-133">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="42fcf-133">Next steps</span></span>

<span data-ttu-id="42fcf-134">Andare al [Passaggio 8: Configurare i criteri di replica](physical-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="42fcf-134">Go to [Step 8: Set up a replication policy](physical-walkthrough-replication.md)</span></span>
