---
title: aggiornamenti del sistema aaaApply in Centro sicurezza di Azure | Documenti Microsoft
description: Questo documento viene illustrato come tooimplement hello indicazioni Centro sicurezza di Azure * * applicare gli aggiornamenti di sistema * * e * * riavviare il sistema dopo gli aggiornamenti di sistema * *.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: e5bd7f55-38fd-4ebb-84ab-32bd60e9fa7a
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/03/2017
ms.author: terrylan
ms.openlocfilehash: 02024f1558b4758c09141fe1934c2e1a9845cc96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="apply-system-updates-in-azure-security-center"></a><span data-ttu-id="c7d82-103">Applicare gli aggiornamenti del sistema nel Centro sicurezza di Azure</span><span class="sxs-lookup"><span data-stu-id="c7d82-103">Apply system updates in Azure Security Center</span></span>
<span data-ttu-id="c7d82-104">Il Centro sicurezza di Azure monitora ogni giorno le macchine virtuali (VM) Windows e Linux alla ricerca di eventuali aggiornamenti mancanti del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="c7d82-104">Azure Security Center monitors daily Windows and  Linux virtual machines (VMs) for missing operating system updates.</span></span> <span data-ttu-id="c7d82-105">Il Centro sicurezza recupera un elenco di aggiornamenti di sicurezza e critici disponibili da Windows Update o Windows Server Update Services (WSUS), in base al servizio configurato nella macchina virtuale Windows.</span><span class="sxs-lookup"><span data-stu-id="c7d82-105">Security Center retrieves a list of available security and critical updates from Windows Update or Windows Server Update Services (WSUS), depending on which service is configured on a Windows VM.</span></span>  <span data-ttu-id="c7d82-106">Centro sicurezza PC controlla anche per gli aggiornamenti più recenti di hello nei sistemi Linux.</span><span class="sxs-lookup"><span data-stu-id="c7d82-106">Security Center also checks for hello latest updates in Linux systems.</span></span> <span data-ttu-id="c7d82-107">Se nella macchina virtuale non è stato applicato un aggiornamento del sistema, il Centro sicurezza ne consiglierà l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c7d82-107">If your VM is missing a system update, Security Center will recommend that you apply system updates</span></span>

> [!NOTE]
> <span data-ttu-id="c7d82-108">Questo documento introduce servizio hello utilizzando un esempio di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="c7d82-108">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="c7d82-109">Questa non è una guida dettagliata.</span><span class="sxs-lookup"><span data-stu-id="c7d82-109">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="c7d82-110">Implementare la raccomandazione hello</span><span class="sxs-lookup"><span data-stu-id="c7d82-110">Implement hello recommendation</span></span>
1. <span data-ttu-id="c7d82-111">In hello **indicazioni** pannello seleziona **applicare gli aggiornamenti di sistema**.</span><span class="sxs-lookup"><span data-stu-id="c7d82-111">In hello **Recommendations** blade, select **Apply system updates**.</span></span>

   ![Applicare gli aggiornamenti di sistema][1]
2. <span data-ttu-id="c7d82-113">Hello **applicare gli aggiornamenti di sistema** pannello verrà aperto un elenco di macchine virtuali privi di aggiornamenti di sistema.</span><span class="sxs-lookup"><span data-stu-id="c7d82-113">hello **Apply system updates** blade opens displaying a list of VMs missing system updates.</span></span> <span data-ttu-id="c7d82-114">Selezionare una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c7d82-114">Select a VM.</span></span>

   ![Selezionare una macchina virtuale][2]
3. <span data-ttu-id="c7d82-116">Viene visualizzato un pannello che mostra un elenco di aggiornamenti mancanti per la VM.</span><span class="sxs-lookup"><span data-stu-id="c7d82-116">A blade opens displaying a list of missing updates for that VM.</span></span> <span data-ttu-id="c7d82-117">Selezionare un aggiornamento del sistema.</span><span class="sxs-lookup"><span data-stu-id="c7d82-117">Select a system update.</span></span> <span data-ttu-id="c7d82-118">In questo esempio viene selezionato l'aggiornamento KB3156016.</span><span class="sxs-lookup"><span data-stu-id="c7d82-118">In this example, let’s select KB3156016.</span></span>

   ![Aggiornamenti della sicurezza mancanti][3]

4. <span data-ttu-id="c7d82-120">Seguire i passaggi hello hello **aggiornamento della sicurezza** tooapply pannello hello aggiornamento mancante.</span><span class="sxs-lookup"><span data-stu-id="c7d82-120">Follow hello steps in hello **Security Update** blade tooapply hello missing update.</span></span>

   ![Aggiornamento della sicurezza][4]

## <a name="reboot-after-system-updates"></a><span data-ttu-id="c7d82-122">Riavviare dopo gli aggiornamenti del sistema</span><span class="sxs-lookup"><span data-stu-id="c7d82-122">Reboot after system updates</span></span>
1. <span data-ttu-id="c7d82-123">Restituire toohello **indicazioni** blade.</span><span class="sxs-lookup"><span data-stu-id="c7d82-123">Return toohello **Recommendations** blade.</span></span> <span data-ttu-id="c7d82-124">Dopo l'applicazione degli aggiornamenti del sistema è stata generata una nuova voce, denominata **Riavvia dopo gli aggiornamenti del sistema**.</span><span class="sxs-lookup"><span data-stu-id="c7d82-124">A new entry was generated after you applied system updates, called **Reboot after system updates**.</span></span> <span data-ttu-id="c7d82-125">Questa voce indica che è necessario che il processo tooreboot hello VM toocomplete hello di applicazione degli aggiornamenti di sistema.</span><span class="sxs-lookup"><span data-stu-id="c7d82-125">This entry lets you know that you need tooreboot hello VM toocomplete hello process of applying system updates.</span></span>

   ![Riavviare dopo gli aggiornamenti del sistema][5]
2. <span data-ttu-id="c7d82-127">Selezionare **Riavvia dopo gli aggiornamenti del sistema**.</span><span class="sxs-lookup"><span data-stu-id="c7d82-127">Select **Reboot after system updates**.</span></span> <span data-ttu-id="c7d82-128">Verrà visualizzata **è un riavvio in sospeso toocomplete gli aggiornamenti del sistema** blade che visualizza un elenco di macchine virtuali che è necessario toorestart toocomplete hello applica il processo di aggiornamento del sistema.</span><span class="sxs-lookup"><span data-stu-id="c7d82-128">This opens **A restart is pending toocomplete system updates** blade displaying a list of VMs that you need toorestart toocomplete hello apply system updates process.</span></span>

   ![Riavvio in sospeso][6]

<span data-ttu-id="c7d82-130">Riavviare hello VM dal processo di hello toocomplete Azure.</span><span class="sxs-lookup"><span data-stu-id="c7d82-130">Restart hello VM from Azure toocomplete hello process.</span></span>

## <a name="see-also"></a><span data-ttu-id="c7d82-131">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c7d82-131">See also</span></span>
<span data-ttu-id="c7d82-132">toolearn ulteriori informazioni su Centro di sicurezza, vedere l'esempio hello:</span><span class="sxs-lookup"><span data-stu-id="c7d82-132">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="c7d82-133">[L'impostazione di criteri di sicurezza nel Centro protezione Azure](security-center-policies.md) -informazioni su come tooconfigure i criteri di sicurezza per le sottoscrizioni di Azure e i gruppi di risorse.</span><span class="sxs-lookup"><span data-stu-id="c7d82-133">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="c7d82-134">[Gestione delle raccomandazioni di sicurezza nel Centro sicurezza di Azure](security-center-recommendations.md) : informazioni sul modo in cui le raccomandazioni semplificano la protezione delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="c7d82-134">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="c7d82-135">[Il monitoraggio dello stato di sicurezza nel Centro protezione Azure](security-center-monitoring.md) -informazioni su come toomonitor hello integrità delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="c7d82-135">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="c7d82-136">[La gestione e risponde toosecurity gli avvisi in Centro sicurezza di Azure](security-center-managing-and-responding-alerts.md) -informazioni su come avvisi toosecurity toomanage e rispondere.</span><span class="sxs-lookup"><span data-stu-id="c7d82-136">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="c7d82-137">[Monitoraggio di soluzioni dei partner con Centro sicurezza di Azure](security-center-partner-solutions.md) -informazioni su come toomonitor hello lo stato di integrità delle soluzioni di partner.</span><span class="sxs-lookup"><span data-stu-id="c7d82-137">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="c7d82-138">[Domande frequenti su Centro sicurezza di Azure](security-center-faq.md) -domande frequenti sull'utilizzo di hello servizio di ricerca.</span><span class="sxs-lookup"><span data-stu-id="c7d82-138">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="c7d82-139">[Blog sulla sicurezza di Azure](http://blogs.msdn.com/b/azuresecurity/) : post di blog sulla sicurezza e sulla conformità di Azure.</span><span class="sxs-lookup"><span data-stu-id="c7d82-139">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-apply-system-updates/recommendation.png
[2]:./media/security-center-apply-system-updates/select-vm.png
[3]: ./media/security-center-apply-system-updates/missing-security-updates.png
[4]: ./media/security-center-apply-system-updates/security-update.png
[5]: ./media/security-center-apply-system-updates/reboot-after-system-updates.png
[6]: ./media/security-center-apply-system-updates/restart-pending.png
