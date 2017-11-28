---
title: aaaMigrate macchine virtuali da AWS tooAzure | Documenti Microsoft
description: In questo articolo viene descritto come toomigrate virtuale dei computer in esecuzione in tooAzure Amazon Web Services (AWS) usando Azure Site Recovery.
services: site-recovery
documentationcenter: 
author: bsiva
manager: jwhit
editor: 
ms.assetid: ddb412fd-32a8-4afa-9e39-738b11b91118
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/31/2017
ms.author: bsiva
ms.openlocfilehash: c99b781ec9cca5b8f9a847d3fc48408062b120b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-virtual-machines-in-amazon-web-services-aws-tooazure-with-azure-site-recovery"></a><span data-ttu-id="fe6b7-103">Eseguire la migrazione di macchine virtuali in tooAzure Amazon Web Services (AWS) con Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="fe6b7-103">Migrate virtual machines in Amazon Web Services (AWS) tooAzure with Azure Site Recovery</span></span>

<span data-ttu-id="fe6b7-104">In questo articolo viene descritto come toomigrate Windows AWS istanze tooAzure le macchine virtuali con hello [Azure Site Recovery](site-recovery-overview.md) servizio.</span><span class="sxs-lookup"><span data-stu-id="fe6b7-104">This article describes how toomigrate AWS Windows instances tooAzure virtual machines with hello [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="fe6b7-105">La migrazione è in realtà un failover da AWS tooAzure.</span><span class="sxs-lookup"><span data-stu-id="fe6b7-105">Migration is effectively a failover from AWS tooAzure.</span></span> <span data-ttu-id="fe6b7-106">Non è possibile eseguire il failback macchine tooAWS e non vi è alcuna replica in corso.</span><span class="sxs-lookup"><span data-stu-id="fe6b7-106">You can't failback machines tooAWS, and there's no ongoing replication.</span></span> <span data-ttu-id="fe6b7-107">In questo articolo vengono descritti i passaggi hello per la migrazione in hello portale di Azure e sono basati su istruzioni hello per [la replica di un computer fisico di tooAzure](site-recovery-vmware-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="fe6b7-107">This article describes hello steps for migration in hello Azure portal, and are based on hello instructions for [replicating a physical machine tooAzure](site-recovery-vmware-to-azure.md).</span></span>

<span data-ttu-id="fe6b7-108">Inviare eventuali commenti o domande nella parte inferiore di hello di questo articolo, o di hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span><span class="sxs-lookup"><span data-stu-id="fe6b7-108">Post any comments or questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span></span>

## <a name="supported-operating-systems"></a><span data-ttu-id="fe6b7-109">Sistemi operativi supportati</span><span class="sxs-lookup"><span data-stu-id="fe6b7-109">Supported operating systems</span></span>

<span data-ttu-id="fe6b7-110">Il ripristino del sito può essere utilizzato toomigrate EC2 istanze in esecuzione uno dei seguenti sistemi operativi hello:</span><span class="sxs-lookup"><span data-stu-id="fe6b7-110">Site Recovery can be used toomigrate EC2 instances running any of hello following operating systems:</span></span>

- <span data-ttu-id="fe6b7-111">Windows (solo versione a 64 bit)</span><span class="sxs-lookup"><span data-stu-id="fe6b7-111">Windows(64 bit only)</span></span>
    - <span data-ttu-id="fe6b7-112">Windows Server 2008 R2 SP1+ (solo driver Citrix PV o driver AWS PV:</span><span class="sxs-lookup"><span data-stu-id="fe6b7-112">Windows Server 2008 R2 SP1+ (Citrix PV drivers or AWS PV drivers only.</span></span> <span data-ttu-id="fe6b7-113">**le istanze con driver RedHat PV non sono supportate**) Windows Server 2012 Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="fe6b7-113">**Instances running RedHat PV drivers are not supported**) Windows Server 2012 Windows Server 2012 R2</span></span>
- <span data-ttu-id="fe6b7-114">Linux (solo versione a 64 bit)</span><span class="sxs-lookup"><span data-stu-id="fe6b7-114">Linux (64 bit only)</span></span>
    - <span data-ttu-id="fe6b7-115">Red Hat Enterprise Linux 6.7 (solo per istanze HVM virtualizzate)</span><span class="sxs-lookup"><span data-stu-id="fe6b7-115">Red Hat Enterprise Linux 6.7 (HVM virtualized instances only)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fe6b7-116">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="fe6b7-116">Prerequisites</span></span>

<span data-ttu-id="fe6b7-117">Per la distribuzione è necessario quanto segue:</span><span class="sxs-lookup"><span data-stu-id="fe6b7-117">Here's what you need for this deployment:</span></span>

* <span data-ttu-id="fe6b7-118">**Server di configurazione**: una macchina virtuale di EC2 Amazon che esegue Windows Server 2012 R2 viene distribuito come server di configurazione hello.</span><span class="sxs-lookup"><span data-stu-id="fe6b7-118">**Configuration server**: An Amazon EC2 VM running Windows Server 2012 R2 is deployed as hello configuration server.</span></span> <span data-ttu-id="fe6b7-119">Per impostazione predefinita, hello altri componenti di Azure Site Recovery (server di elaborazione e il server di destinazione master) vengono installati quando si distribuisce il server di configurazione hello.</span><span class="sxs-lookup"><span data-stu-id="fe6b7-119">By default, hello other Azure Site Recovery components (process server and master target server) are installed when you deploy hello configuration server.</span></span> <span data-ttu-id="fe6b7-120">In questo articolo vengono descritti i passaggi hello per la migrazione in hello portale di Azure e sono basati su istruzioni hello per [maggiori informazioni](site-recovery-components.md)</span><span class="sxs-lookup"><span data-stu-id="fe6b7-120">This article describes hello steps for migration in hello Azure portal, and are based on hello instructions for  [Learn more](site-recovery-components.md)</span></span>

* <span data-ttu-id="fe6b7-121">**Le istanze di EC2**: hello Amazon EC2 le istanze di macchine virtuali che si desidera toomigrate.</span><span class="sxs-lookup"><span data-stu-id="fe6b7-121">**EC2 instances**: hello Amazon EC2 virtual machines instances that you want toomigrate.</span></span>

## <a name="deployment-steps"></a><span data-ttu-id="fe6b7-122">Passaggi di distribuzione</span><span class="sxs-lookup"><span data-stu-id="fe6b7-122">Deployment steps</span></span>

1. <span data-ttu-id="fe6b7-123">Creare un insieme di credenziali dei servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="fe6b7-123">Create a Recovery Services vault.</span></span>
2. <span data-ttu-id="fe6b7-124">Gruppo di sicurezza delle istanze EC2 Hello deve disporre di regole configurate tooallow comunicazione tra l'istanza di EC2 hello che si desidera toomigrate e hello istanza su cui si prevede di toodeploy hello del Server di configurazione.</span><span class="sxs-lookup"><span data-stu-id="fe6b7-124">hello Security Group of your EC2 instances should have rules configured tooallow communication between hello EC2 instance that you want toomigrate, and hello instance on which you plan toodeploy hello Configuration Server.</span></span>

3. <span data-ttu-id="fe6b7-125">In hello stesso Amazon di Cloud privato virtuale come le istanze di EC2, distribuire un server di configurazione di ripristino automatico di sistema.</span><span class="sxs-lookup"><span data-stu-id="fe6b7-125">On hello same Amazon Virtual Private Cloud as your EC2 instances, deploy an ASR configuration server.</span></span> <span data-ttu-id="fe6b7-126">Fare riferimento hello VMware / fisici tooAzure prerequisiti per i requisiti di distribuzione server di configurazione.</span><span class="sxs-lookup"><span data-stu-id="fe6b7-126">Refer hello VMware / Physical tooAzure prerequisites for configuration server deployment requirements.</span></span>

    ![DeployCS](./media/site-recovery-migrate-aws-to-azure/migration_pic2.png)

4.  <span data-ttu-id="fe6b7-128">Dopo che il server di configurazione è distribuito in AWS e registrato con l'insieme di credenziali di servizi di ripristino, verrà visualizzato il server di configurazione di hello e server di elaborazione in dell'infrastruttura di Site Recovery come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="fe6b7-128">Once your configuration server is deployed in AWS and registered with your Recovery Services vault, you should see hello configuration server and process server under Site Recovery infrastructure as shown below:</span></span>

    ![CSinVault](./media/site-recovery-migrate-aws-to-azure/migration_pic3.png)

5. <span data-ttu-id="fe6b7-130">Dopo aver distribuito il server di configurazione di hello (operazione può richiedere per tale too15 minustes tooappear), convalidare in grado di comunicare con le macchine virtuali hello che si desidera toomigrate.</span><span class="sxs-lookup"><span data-stu-id="fe6b7-130">After you've deployed hello configuration server (it might take up too15 minustes for it tooappear), validate that it can communicate with hello VMs that you want toomigrate.</span></span>

6. <span data-ttu-id="fe6b7-131">[Configurare le impostazioni di replica](site-recovery-setup-replication-settings-vmware.md).</span><span class="sxs-lookup"><span data-stu-id="fe6b7-131">[Set up replication settings](site-recovery-setup-replication-settings-vmware.md).</span></span>

7. <span data-ttu-id="fe6b7-132">Abilitare la replica: abilitare la replica per le macchine virtuali desiderate toomigrate hello.</span><span class="sxs-lookup"><span data-stu-id="fe6b7-132">Enable replication: Enable replication for hello VMs you want toomigrate.</span></span> <span data-ttu-id="fe6b7-133">È possibile individuare le istanze di EC2 hello utilizzando indirizzi IP privati hello, che è possibile ottenere dalla console EC2 hello.</span><span class="sxs-lookup"><span data-stu-id="fe6b7-133">You can discover hello EC2 instances using hello private IP addresses, which you can get from hello EC2 console.</span></span>

    ![SelectVM](./media/site-recovery-migrate-aws-to-azure/migration_pic4.png)

8. <span data-ttu-id="fe6b7-135">Dopo che sono stati protetti istanze hello EC2 e hello tooAzure di replica è stata completata, [eseguire un Failover di Test](site-recovery-test-failover-to-azure.md) toovalidate le prestazioni dell'applicazione in Azure.</span><span class="sxs-lookup"><span data-stu-id="fe6b7-135">Once hello EC2 instances have been protected and hello replication tooAzure is complete, [run a Test Failover](site-recovery-test-failover-to-azure.md) toovalidate your application's performance in Azure.</span></span>

    ![TFI](./media/site-recovery-migrate-aws-to-azure/migration_pic5.png)

9. <span data-ttu-id="fe6b7-137">Eseguire un Failover da AWS tooAzure per ogni macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="fe6b7-137">Run a Failover from AWS tooAzure for each VM.</span></span> <span data-ttu-id="fe6b7-138">Facoltativamente, è possibile creare un piano di ripristino ed eseguire un Failover, toomigrate più macchine virtuali da AWS tooAzure.</span><span class="sxs-lookup"><span data-stu-id="fe6b7-138">Optionally, you can create a recovery plan and run a Failover, toomigrate multiple virtual machines from AWS tooAzure.</span></span> <span data-ttu-id="fe6b7-139">[Ulteriori informazioni](site-recovery-create-recovery-plans.md) sui piani di ripristino.</span><span class="sxs-lookup"><span data-stu-id="fe6b7-139">[Learn more](site-recovery-create-recovery-plans.md) about recovery plans.</span></span>

10. <span data-ttu-id="fe6b7-140">Per la migrazione, non è necessario toocommit un failover.</span><span class="sxs-lookup"><span data-stu-id="fe6b7-140">For migration, you don't need toocommit a failover.</span></span> <span data-ttu-id="fe6b7-141">Invece si seleziona l'opzione di completare la migrazione di hello per ogni computer si desidera toomigrate.</span><span class="sxs-lookup"><span data-stu-id="fe6b7-141">Instead, you select hello Complete Migration option for each machine you want toomigrate.</span></span> <span data-ttu-id="fe6b7-142">Hello azione di completare la migrazione termina il processo di migrazione hello, rimuove la replica per macchina hello e interrompe il ripristino del sito per la macchina hello di fatturazione.</span><span class="sxs-lookup"><span data-stu-id="fe6b7-142">hello Complete Migration action finishes up hello migration process, removes replication for hello machine, and stops Site Recovery billing for hello machine.</span></span>

    ![Migrazione](./media/site-recovery-migrate-aws-to-azure/migration_pic6.png)

## <a name="next-steps"></a><span data-ttu-id="fe6b7-144">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fe6b7-144">Next steps</span></span>

- <span data-ttu-id="fe6b7-145">[Preparare la migrazione di macchine tooenable replica](site-recovery-azure-to-azure-after-migration.md) tooanother area per esigenze di ripristino di emergenza.</span><span class="sxs-lookup"><span data-stu-id="fe6b7-145">[Prepare migrated machines tooenable replication](site-recovery-azure-to-azure-after-migration.md) tooanother region for disaster recovery needs.</span></span>
- <span data-ttu-id="fe6b7-146">Iniziare a proteggere i carichi di lavoro [replicando le macchine virtuali di Azure](site-recovery-azure-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="fe6b7-146">Start protecting your workloads by [replicating Azure virtual machines.](site-recovery-azure-to-azure.md)</span></span>
