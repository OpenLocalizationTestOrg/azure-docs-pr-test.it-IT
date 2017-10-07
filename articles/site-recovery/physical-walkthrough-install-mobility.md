---
title: "hello aaaInstall servizio di mobilità per la replica di server fisici tooAzure | Documenti Microsoft"
description: "In questo articolo viene descritto come tooinstall hello agente del servizio di mobilità nei server fisici, replica tooAzure con il servizio di Azure Site Recovery hello."
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
ms.openlocfilehash: 48fd2c0ffe67875ed446c8167c2ae7f90d3f537c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-install-hello-mobility-service"></a><span data-ttu-id="e6ed8-103">Passaggio 9: Installare il servizio di mobilità hello</span><span class="sxs-lookup"><span data-stu-id="e6ed8-103">Step 9: Install hello Mobility service</span></span>


<span data-ttu-id="e6ed8-104">In questo articolo viene descritto come componente del servizio Mobility di hello tooinstall durante la replica locale tooAzure server fisici Windows/Linux, usando hello [Azure Site Recovery](site-recovery-overview.md) di hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="e6ed8-104">This article describes how tooinstall hello Mobility service component when replicating on-premises Windows/Linux physical servers tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="e6ed8-105">servizio di mobilità Hello acquisisce scritture di dati in un computer e li inoltra toohello server di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="e6ed8-105">hello Mobility service captures data writes on a machine, and forwards them toohello process server.</span></span> <span data-ttu-id="e6ed8-106">È necessario installarlo in ogni server che si desidera tooreplicate tooAzure.</span><span class="sxs-lookup"><span data-stu-id="e6ed8-106">It should be installed on each server that you want tooreplicate tooAzure.</span></span>

<span data-ttu-id="e6ed8-107">È possibile installare manualmente il servizio di mobilità hello o utilizzando un'installazione push da hello a elaborare il ripristino del sito quando è abilitata la replica di server o utilizzando uno strumento come System Center Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="e6ed8-107">You can install hello Mobility service manually, or using a push installation from hello Site Recovery process server when replication is enabled, or using a tool such as System Center Configuration Manager.</span></span> <span data-ttu-id="e6ed8-108">Se si utilizza l'installazione push, il servizio di hello è installato nel server di hello quando si abilita la replica.</span><span class="sxs-lookup"><span data-stu-id="e6ed8-108">If you use push installation, hello service is installed on hello server when you enable replication.</span></span>

<span data-ttu-id="e6ed8-109">Inviare commenti e domande nella parte inferiore di hello di questo articolo, o di hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="e6ed8-109">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="install-manually"></a><span data-ttu-id="e6ed8-110">Eseguire l'installazione manuale</span><span class="sxs-lookup"><span data-stu-id="e6ed8-110">Install manually</span></span>

1. <span data-ttu-id="e6ed8-111">Controllare hello [prerequisiti](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) per l'installazione manuale.</span><span class="sxs-lookup"><span data-stu-id="e6ed8-111">Check hello [prerequisites](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) for manual installation.</span></span>
2. <span data-ttu-id="e6ed8-112">Seguire [queste istruzioni](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) per l'installazione manuale tramite il portale di hello.</span><span class="sxs-lookup"><span data-stu-id="e6ed8-112">Follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) for manual installation using hello portal.</span></span>
3. <span data-ttu-id="e6ed8-113">Se si preferisce tooinstall dalla riga di comando hello, seguire [queste istruzioni](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).</span><span class="sxs-lookup"><span data-stu-id="e6ed8-113">If you prefer tooinstall from hello command line, follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).</span></span>

## <a name="install-from-hello-process-server"></a><span data-ttu-id="e6ed8-114">Installare dal server di elaborazione hello</span><span class="sxs-lookup"><span data-stu-id="e6ed8-114">Install from hello process server</span></span>

<span data-ttu-id="e6ed8-115">Se si desidera toopush hello installazione del servizio Mobility dal server di elaborazione hello quando si abilita la replica per un computer, è necessario un account che possa essere usato da hello processo server tooaccess hello macchina.</span><span class="sxs-lookup"><span data-stu-id="e6ed8-115">If you want toopush hello Mobility service installation from hello process server when you enable replication for a machine, you need an account that can be used by hello process server tooaccess hello machine.</span></span> <span data-ttu-id="e6ed8-116">account di Hello viene utilizzato solo per l'installazione push hello.</span><span class="sxs-lookup"><span data-stu-id="e6ed8-116">hello account is only used for hello push installation.</span></span>

1. <span data-ttu-id="e6ed8-117">Se non è stato ancora creato un account, eseguire questa operazione usando le linee guida seguenti:</span><span class="sxs-lookup"><span data-stu-id="e6ed8-117">If you haven't created an account, do so using these guidelines:</span></span>

    - <span data-ttu-id="e6ed8-118">È possibile usare un account di dominio o locale</span><span class="sxs-lookup"><span data-stu-id="e6ed8-118">You can use a domain or local account</span></span>
    - <span data-ttu-id="e6ed8-119">Per Windows, se non si utilizza un account di dominio, è necessario il controllo di accesso remoto nel computer locale hello toodisable.</span><span class="sxs-lookup"><span data-stu-id="e6ed8-119">For Windows, if you're not using a domain account, you need toodisable Remote User Access control on hello local machine.</span></span> <span data-ttu-id="e6ed8-120">toodo, in hello registrare in **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System**, aggiungere una voce DWORD hello **LocalAccountTokenFilterPolicy**, con un valore pari a 1.</span><span class="sxs-lookup"><span data-stu-id="e6ed8-120">toodo this, in hello register under **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System**, add hello DWORD entry **LocalAccountTokenFilterPolicy**, with a value of 1.</span></span>
    - <span data-ttu-id="e6ed8-121">Se si desidera una voce del Registro di sistema di hello tooadd per Windows da CLI, digitare:</span><span class="sxs-lookup"><span data-stu-id="e6ed8-121">If you want tooadd hello registry entry for Windows from a CLI, type:</span></span>

        ```
        REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1.
        ```

    - <span data-ttu-id="e6ed8-122">Per Linux, account hello devono essere radice nel server di hello origine Linux.</span><span class="sxs-lookup"><span data-stu-id="e6ed8-122">For Linux, hello account should be root on hello source Linux server.</span></span>

2. <span data-ttu-id="e6ed8-123">Seguire quindi [queste istruzioni](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) se si desidera servizio di mobilità toopush hello in macchine virtuali in esecuzione Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="e6ed8-123">Then follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) if you want toopush hello Mobility service on VMs running Windows or Linux.</span></span>

## <a name="other-installation-methods"></a><span data-ttu-id="e6ed8-124">Altri metodi di installazione</span><span class="sxs-lookup"><span data-stu-id="e6ed8-124">Other installation methods</span></span>

- <span data-ttu-id="e6ed8-125">[Informazioni su](site-recovery-install-mobility-service-using-sccm.md) installazione del servizio di mobilità hello con Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="e6ed8-125">[Learn about](site-recovery-install-mobility-service-using-sccm.md) installing hello Mobility service using Configuration Manager</span></span>
- <span data-ttu-id="e6ed8-126">[Ulteriori informazioni](site-recovery-automate-mobility-service-install.md) sull'installazione con la piattaforma DSC di Automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="e6ed8-126">[Learn about](site-recovery-automate-mobility-service-install.md) installing with Azure Automation DSC.</span></span>


## <a name="next-steps"></a><span data-ttu-id="e6ed8-127">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e6ed8-127">Next steps</span></span>

<span data-ttu-id="e6ed8-128">Andare troppo[passaggio 10: abilitare la replica](physical-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="e6ed8-128">Go too[Step 10: Enable replication](physical-walkthrough-enable-replication.md)</span></span>
