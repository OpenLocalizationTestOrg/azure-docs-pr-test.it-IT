---
title: "hello aaaInstall servizio di mobilità per la replica VMware tooAzure | Documenti Microsoft"
description: "In questo articolo viene descritto come tooinstall hello agente del servizio di mobilità per la replica tooAzure VMware con il servizio di Azure Site Recovery hello."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 3189fbcd-6b5b-4ffb-b5a9-e2080c37f9d9
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: d3b7bc9c4d84d13317e0b0b47adcf38e8c41d0bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-install-hello-mobility-service"></a><span data-ttu-id="52723-103">Passaggio 10: Installare il servizio di mobilità hello</span><span class="sxs-lookup"><span data-stu-id="52723-103">Step 10: Install hello Mobility service</span></span>


<span data-ttu-id="52723-104">In questo articolo viene descritto come le impostazioni di tooconfigure origine e di destinazione durante la replica locale tooAzure di macchine virtuali VMware, utilizzando hello [Azure Site Recovery](site-recovery-overview.md) di hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="52723-104">This article describes how tooconfigure source and target settings when replicating on-premises VMware virtual machines tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="52723-105">servizio di mobilità Hello acquisisce scritture di dati in un computer e li inoltra toohello server di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="52723-105">hello Mobility service captures data writes on a machine, and forwards them toohello process server.</span></span> <span data-ttu-id="52723-106">È necessario installarlo in ogni computer che si desidera tooreplicate tooAzure.</span><span class="sxs-lookup"><span data-stu-id="52723-106">It should be installed on each machine that you want tooreplicate tooAzure.</span></span>

<span data-ttu-id="52723-107">È possibile eseguire l'installazione manuale del servizio di mobilità hello, un'installazione push dal server di elaborazione di Site Recovery hello quando è abilitata la replica o utilizzare uno strumento di System Center Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="52723-107">You can install hello Mobility service manual, using a push installation from hello Site Recovery process server when replication is enabled, or use a tool System Center Configuration Manager.</span></span> <span data-ttu-id="52723-108">Se si utilizza l'installazione push, servizio hello viene installato nella macchina virtuale hello quando è abilitata la replica.</span><span class="sxs-lookup"><span data-stu-id="52723-108">If you use push installation, hello service is installed on hello VM when replication is enabled.</span></span>

<span data-ttu-id="52723-109">Inviare commenti e domande nella parte inferiore di hello di questo articolo, o di hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="52723-109">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="install-manually"></a><span data-ttu-id="52723-110">Eseguire l'installazione manuale</span><span class="sxs-lookup"><span data-stu-id="52723-110">Install manually</span></span>

1. <span data-ttu-id="52723-111">Controllare hello [prerequisiti](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) per l'installazione manuale.</span><span class="sxs-lookup"><span data-stu-id="52723-111">Check hello [prerequisites](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) for manual installation.</span></span>
2. <span data-ttu-id="52723-112">Seguire [queste istruzioni](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) per l'installazione manuale tramite il portale di hello.</span><span class="sxs-lookup"><span data-stu-id="52723-112">Follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) for manual installation using hello portal.</span></span>
3. <span data-ttu-id="52723-113">Se si preferisce tooinstall dalla riga di comando hello, seguire [queste istruzioni](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).</span><span class="sxs-lookup"><span data-stu-id="52723-113">If you prefer tooinstall from hello command line, follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).</span></span>

## <a name="install-from-hello-process-server"></a><span data-ttu-id="52723-114">Installare dal server di elaborazione hello</span><span class="sxs-lookup"><span data-stu-id="52723-114">Install from hello process server</span></span>

<span data-ttu-id="52723-115">Se si desidera l'installazione del servizio Mobility hello toopush dal server di elaborazione hello quando si abilita la replica per una macchina virtuale, è necessario un account che può essere utilizzato da hello processo server tooaccess hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="52723-115">If you want toopush hello Mobility service installation from hello process server when you enable replication for a VM, you need an account that can be used by hello process server tooaccess hello VM.</span></span> <span data-ttu-id="52723-116">account di Hello viene utilizzato solo per l'installazione push hello.</span><span class="sxs-lookup"><span data-stu-id="52723-116">hello account is only used for hello push installation.</span></span>

1. <span data-ttu-id="52723-117">È necessario aver [creato un account](vmware-walkthrough-prepare-vmware.md) che possa essere usato per l'installazione push.</span><span class="sxs-lookup"><span data-stu-id="52723-117">You should have [created an account](vmware-walkthrough-prepare-vmware.md) that can be used for push installation.</span></span> <span data-ttu-id="52723-118">È quindi possibile specificare account hello da toouse quando si configurano le impostazioni di origine durante la distribuzione di Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="52723-118">You then specify hello account you want toouse when you configure source settings during Site Recovery deployment.</span></span>
2. <span data-ttu-id="52723-119">Seguire quindi [queste istruzioni](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) se si desidera servizio di mobilità toopush hello in macchine virtuali in esecuzione Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="52723-119">Then follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) if you want toopush hello Mobility service on VMs running Windows or Linux.</span></span>

## <a name="other-methods"></a><span data-ttu-id="52723-120">Altri metodi</span><span class="sxs-lookup"><span data-stu-id="52723-120">Other methods</span></span>

<span data-ttu-id="52723-121">Altre informazioni, vedere [installazione del servizio di mobilità hello utilizzando Gestione configurazione](site-recovery-install-mobility-service-using-sccm.md), o tramite [Automation DSC per Azure](site-recovery-automate-mobility-service-install.md).</span><span class="sxs-lookup"><span data-stu-id="52723-121">Learn more about [installing hello Mobility service using Configuration Manager](site-recovery-install-mobility-service-using-sccm.md), or using [Azure Automation DSC](site-recovery-automate-mobility-service-install.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="52723-122">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="52723-122">Next steps</span></span>

<span data-ttu-id="52723-123">Andare troppo[passaggio 11: abilitare la replica](vmware-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="52723-123">Go too[Step 11: Enable replication](vmware-walkthrough-enable-replication.md)</span></span>
