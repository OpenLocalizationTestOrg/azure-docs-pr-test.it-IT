---
title: Installare il servizio Mobility per la replica del server fisico in Azure | Microsoft Docs
description: Questo articolo illustra come installare l'agente del servizio Mobility nei server fisici per la replica in Azure con il servizio Azure Site Recovery.
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
ms.openlocfilehash: d73267d7a64221a3138af19e9a2d5dd15809b927
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="step-9-install-the-mobility-service"></a><span data-ttu-id="a9ab5-103">Passaggio 9: Installare il servizio Mobility</span><span class="sxs-lookup"><span data-stu-id="a9ab5-103">Step 9: Install the Mobility service</span></span>


<span data-ttu-id="a9ab5-104">Questo articolo illustra come installare il componente del servizio Mobility quando si replicano server fisici Windows/Linux locali in Azure usando il servizio [Azure Site Recovery](site-recovery-overview.md) nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a9ab5-104">This article describes how to install the Mobility service component when replicating on-premises Windows/Linux physical servers to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="a9ab5-105">Il servizio Mobility acquisisce le scritture di dati in un computer e le inoltra al server di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="a9ab5-105">The Mobility service captures data writes on a machine, and forwards them to the process server.</span></span> <span data-ttu-id="a9ab5-106">Questo servizio deve essere installato in ogni server di cui si vuole eseguire la replica in Azure.</span><span class="sxs-lookup"><span data-stu-id="a9ab5-106">It should be installed on each server that you want to replicate to Azure.</span></span>

<span data-ttu-id="a9ab5-107">È possibile installare il servizio Mobility manualmente, usando un'installazione push dal server di elaborazione di Site Recovery quando la replica è abilitata o usando uno strumento come System Center Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="a9ab5-107">You can install the Mobility service manually, or using a push installation from the Site Recovery process server when replication is enabled, or using a tool such as System Center Configuration Manager.</span></span> <span data-ttu-id="a9ab5-108">Se si usa l'installazione push, il servizio viene installato nel server quando viene abilitata la replica.</span><span class="sxs-lookup"><span data-stu-id="a9ab5-108">If you use push installation, the service is installed on the server when you enable replication.</span></span>

<span data-ttu-id="a9ab5-109">Inserire commenti e domande nella parte inferiore di questo articolo oppure nel [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="a9ab5-109">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="install-manually"></a><span data-ttu-id="a9ab5-110">Eseguire l'installazione manuale</span><span class="sxs-lookup"><span data-stu-id="a9ab5-110">Install manually</span></span>

1. <span data-ttu-id="a9ab5-111">Controllare i [prerequisiti](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) per l'installazione manuale.</span><span class="sxs-lookup"><span data-stu-id="a9ab5-111">Check the [prerequisites](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) for manual installation.</span></span>
2. <span data-ttu-id="a9ab5-112">Seguire [queste istruzioni](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) per l'installazione manuale tramite il portale.</span><span class="sxs-lookup"><span data-stu-id="a9ab5-112">Follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) for manual installation using the portal.</span></span>
3. <span data-ttu-id="a9ab5-113">Se si preferisce eseguire l'installazione dalla riga di comando, seguire [queste istruzioni](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).</span><span class="sxs-lookup"><span data-stu-id="a9ab5-113">If you prefer to install from the command line, follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).</span></span>

## <a name="install-from-the-process-server"></a><span data-ttu-id="a9ab5-114">Eseguire l'installazione dal server di elaborazione</span><span class="sxs-lookup"><span data-stu-id="a9ab5-114">Install from the process server</span></span>

<span data-ttu-id="a9ab5-115">Se si vuole effettuare il push dell'installazione del servizio Mobility dal server di elaborazione quando si abilita la replica per una macchina, è necessario un account che possa essere usato dal server di elaborazione per accedere alla macchina.</span><span class="sxs-lookup"><span data-stu-id="a9ab5-115">If you want to push the Mobility service installation from the process server when you enable replication for a machine, you need an account that can be used by the process server to access the machine.</span></span> <span data-ttu-id="a9ab5-116">L'account viene usato solo per l'installazione push.</span><span class="sxs-lookup"><span data-stu-id="a9ab5-116">The account is only used for the push installation.</span></span>

1. <span data-ttu-id="a9ab5-117">Se non è stato ancora creato un account, eseguire questa operazione usando le linee guida seguenti:</span><span class="sxs-lookup"><span data-stu-id="a9ab5-117">If you haven't created an account, do so using these guidelines:</span></span>

    - <span data-ttu-id="a9ab5-118">È possibile usare un account di dominio o locale.</span><span class="sxs-lookup"><span data-stu-id="a9ab5-118">You can use a domain or local account</span></span>
    - <span data-ttu-id="a9ab5-119">Per Windows, se non si usa un account di dominio è necessario disabilitare il Controllo dell'accesso utente remoto nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="a9ab5-119">For Windows, if you're not using a domain account, you need to disable Remote User Access control on the local machine.</span></span> <span data-ttu-id="a9ab5-120">A questo scopo, aggiungere la voce DWORD **LocalAccountTokenFilterPolicy** con un valore di 1 nel Registro di sistema in **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System**.</span><span class="sxs-lookup"><span data-stu-id="a9ab5-120">To do this, in the register under **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System**, add the DWORD entry **LocalAccountTokenFilterPolicy**, with a value of 1.</span></span>
    - <span data-ttu-id="a9ab5-121">Per aggiungere la voce del Registro di sistema per Windows da un'interfaccia della riga di comando, digitare:</span><span class="sxs-lookup"><span data-stu-id="a9ab5-121">If you want to add the registry entry for Windows from a CLI, type:</span></span>

        ```
        REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1.
        ```

    - <span data-ttu-id="a9ab5-122">Per Linux, l'account deve essere radice nel server Linux di origine.</span><span class="sxs-lookup"><span data-stu-id="a9ab5-122">For Linux, the account should be root on the source Linux server.</span></span>

2. <span data-ttu-id="a9ab5-123">Seguire [queste istruzioni](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) se si vuole eseguire il push del servizio Mobility nelle VM che eseguono Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="a9ab5-123">Then follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) if you want to push the Mobility service on VMs running Windows or Linux.</span></span>

## <a name="other-installation-methods"></a><span data-ttu-id="a9ab5-124">Altri metodi di installazione</span><span class="sxs-lookup"><span data-stu-id="a9ab5-124">Other installation methods</span></span>

- <span data-ttu-id="a9ab5-125">[Ulteriori informazioni](site-recovery-install-mobility-service-using-sccm.md) sull'installazione del servizio Mobility con Gestione configurazione</span><span class="sxs-lookup"><span data-stu-id="a9ab5-125">[Learn about](site-recovery-install-mobility-service-using-sccm.md) installing the Mobility service using Configuration Manager</span></span>
- <span data-ttu-id="a9ab5-126">[Ulteriori informazioni](site-recovery-automate-mobility-service-install.md) sull'installazione con la piattaforma DSC di Automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="a9ab5-126">[Learn about](site-recovery-automate-mobility-service-install.md) installing with Azure Automation DSC.</span></span>


## <a name="next-steps"></a><span data-ttu-id="a9ab5-127">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a9ab5-127">Next steps</span></span>

<span data-ttu-id="a9ab5-128">Andare a [Passaggio 10: Abilitare la replica](physical-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="a9ab5-128">Go to [Step 10: Enable replication](physical-walkthrough-enable-replication.md)</span></span>
