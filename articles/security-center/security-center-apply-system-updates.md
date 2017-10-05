---
title: Applicare gli aggiornamenti del sistema nel Centro sicurezza di Azure | Microsoft Docs
description: Questo documento illustra come implementare le raccomandazioni **Applica gli aggiornamenti del sistema** e **Riavvia dopo gli aggiornamenti del sistema** del Centro sicurezza di Azure.
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
ms.openlocfilehash: 50cdea437db5387813c6a3905d14b6904d2aba34
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="apply-system-updates-in-azure-security-center"></a><span data-ttu-id="5135e-103">Applicare gli aggiornamenti del sistema nel Centro sicurezza di Azure</span><span class="sxs-lookup"><span data-stu-id="5135e-103">Apply system updates in Azure Security Center</span></span>
<span data-ttu-id="5135e-104">Il Centro sicurezza di Azure monitora ogni giorno le macchine virtuali (VM) Windows e Linux alla ricerca di eventuali aggiornamenti mancanti del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="5135e-104">Azure Security Center monitors daily Windows and  Linux virtual machines (VMs) for missing operating system updates.</span></span> <span data-ttu-id="5135e-105">Il Centro sicurezza recupera un elenco di aggiornamenti di sicurezza e critici disponibili da Windows Update o Windows Server Update Services (WSUS), in base al servizio configurato nella macchina virtuale Windows.</span><span class="sxs-lookup"><span data-stu-id="5135e-105">Security Center retrieves a list of available security and critical updates from Windows Update or Windows Server Update Services (WSUS), depending on which service is configured on a Windows VM.</span></span>  <span data-ttu-id="5135e-106">Il Centro sicurezza cerca anche gli aggiornamenti più recenti nei sistemi Linux.</span><span class="sxs-lookup"><span data-stu-id="5135e-106">Security Center also checks for the latest updates in Linux systems.</span></span> <span data-ttu-id="5135e-107">Se nella macchina virtuale non è stato applicato un aggiornamento del sistema, il Centro sicurezza ne consiglierà l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="5135e-107">If your VM is missing a system update, Security Center will recommend that you apply system updates</span></span>

> [!NOTE]
> <span data-ttu-id="5135e-108">Il documento introduce il servizio usando una distribuzione di esempio.</span><span class="sxs-lookup"><span data-stu-id="5135e-108">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="5135e-109">Questa non è una guida dettagliata.</span><span class="sxs-lookup"><span data-stu-id="5135e-109">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="5135e-110">Implementare la raccomandazione</span><span class="sxs-lookup"><span data-stu-id="5135e-110">Implement the recommendation</span></span>
1. <span data-ttu-id="5135e-111">Nel pannello **Consigli** selezionare **Applica gli aggiornamenti del sistema**.</span><span class="sxs-lookup"><span data-stu-id="5135e-111">In the **Recommendations** blade, select **Apply system updates**.</span></span>

   ![Applicare gli aggiornamenti di sistema][1]
2. <span data-ttu-id="5135e-113">Viene visualizzato il pannello **Applica gli aggiornamenti del sistema** , che mostra un elenco di macchine virtuali prive di alcuni aggiornamenti del sistema.</span><span class="sxs-lookup"><span data-stu-id="5135e-113">The **Apply system updates** blade opens displaying a list of VMs missing system updates.</span></span> <span data-ttu-id="5135e-114">Selezionare una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="5135e-114">Select a VM.</span></span>

   ![Selezionare una macchina virtuale][2]
3. <span data-ttu-id="5135e-116">Viene visualizzato un pannello che mostra un elenco di aggiornamenti mancanti per la VM.</span><span class="sxs-lookup"><span data-stu-id="5135e-116">A blade opens displaying a list of missing updates for that VM.</span></span> <span data-ttu-id="5135e-117">Selezionare un aggiornamento del sistema.</span><span class="sxs-lookup"><span data-stu-id="5135e-117">Select a system update.</span></span> <span data-ttu-id="5135e-118">In questo esempio viene selezionato l'aggiornamento KB3156016.</span><span class="sxs-lookup"><span data-stu-id="5135e-118">In this example, let’s select KB3156016.</span></span>

   ![Aggiornamenti della sicurezza mancanti][3]

4. <span data-ttu-id="5135e-120">Seguire la procedura illustrata nel pannello **Aggiornamento per la sicurezza** per applicare l'aggiornamento mancante.</span><span class="sxs-lookup"><span data-stu-id="5135e-120">Follow the steps in the **Security Update** blade to apply the missing update.</span></span>

   ![Aggiornamento della sicurezza][4]

## <a name="reboot-after-system-updates"></a><span data-ttu-id="5135e-122">Riavviare dopo gli aggiornamenti del sistema</span><span class="sxs-lookup"><span data-stu-id="5135e-122">Reboot after system updates</span></span>
1. <span data-ttu-id="5135e-123">Tornare al pannello **Raccomandazioni** .</span><span class="sxs-lookup"><span data-stu-id="5135e-123">Return to the **Recommendations** blade.</span></span> <span data-ttu-id="5135e-124">Dopo l'applicazione degli aggiornamenti del sistema è stata generata una nuova voce, denominata **Riavvia dopo gli aggiornamenti del sistema**.</span><span class="sxs-lookup"><span data-stu-id="5135e-124">A new entry was generated after you applied system updates, called **Reboot after system updates**.</span></span> <span data-ttu-id="5135e-125">Questa voce indica che è necessario avviare la VM per completare il processo di applicazione degli aggiornamenti del sistema.</span><span class="sxs-lookup"><span data-stu-id="5135e-125">This entry lets you know that you need to reboot the VM to complete the process of applying system updates.</span></span>

   ![Riavviare dopo gli aggiornamenti del sistema][5]
2. <span data-ttu-id="5135e-127">Selezionare **Riavvia dopo gli aggiornamenti del sistema**.</span><span class="sxs-lookup"><span data-stu-id="5135e-127">Select **Reboot after system updates**.</span></span> <span data-ttu-id="5135e-128">Verrà visualizzato il pannello **In attesa di un riavvio per completare gli aggiornamenti del sistema** che mostra un elenco di macchine virtuali che devono essere riavviate per completare il processo di aggiornamento del sistema.</span><span class="sxs-lookup"><span data-stu-id="5135e-128">This opens **A restart is pending to complete system updates** blade displaying a list of VMs that you need to restart to complete the apply system updates process.</span></span>

   ![Riavvio in sospeso][6]

<span data-ttu-id="5135e-130">Riavviare la VM da Azure per completare il processo.</span><span class="sxs-lookup"><span data-stu-id="5135e-130">Restart the VM from Azure to complete the process.</span></span>

## <a name="see-also"></a><span data-ttu-id="5135e-131">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="5135e-131">See also</span></span>
<span data-ttu-id="5135e-132">Per altre informazioni sul Centro sicurezza, vedere gli argomenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="5135e-132">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="5135e-133">[Impostazione dei criteri di sicurezza nel Centro sicurezza di Azure](security-center-policies.md) : informazioni su come configurare i criteri di sicurezza per le sottoscrizioni e i gruppi di risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="5135e-133">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="5135e-134">[Gestione delle raccomandazioni di sicurezza nel Centro sicurezza di Azure](security-center-recommendations.md) : informazioni sul modo in cui le raccomandazioni semplificano la protezione delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="5135e-134">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="5135e-135">[Monitoraggio dell'integrità della sicurezza nel Centro sicurezza di Azure](security-center-monitoring.md) : informazioni su come monitorare l'integrità delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="5135e-135">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="5135e-136">[Gestione e risposta agli avvisi di sicurezza nel Centro sicurezza di Azure](security-center-managing-and-responding-alerts.md) : informazioni su come gestire e rispondere agli avvisi di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="5135e-136">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="5135e-137">[Monitoraggio delle soluzioni dei partner con il Centro sicurezza di Azure](security-center-partner-solutions.md) : informazioni su come monitorare lo stato integrità delle soluzioni dei partner.</span><span class="sxs-lookup"><span data-stu-id="5135e-137">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="5135e-138">[Domande frequenti sul Centro sicurezza di Azure](security-center-faq.md) : domande frequenti sull'uso del servizio.</span><span class="sxs-lookup"><span data-stu-id="5135e-138">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="5135e-139">[Blog sulla sicurezza di Azure](http://blogs.msdn.com/b/azuresecurity/) : post di blog sulla sicurezza e sulla conformità di Azure.</span><span class="sxs-lookup"><span data-stu-id="5135e-139">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-apply-system-updates/recommendation.png
[2]:./media/security-center-apply-system-updates/select-vm.png
[3]: ./media/security-center-apply-system-updates/missing-security-updates.png
[4]: ./media/security-center-apply-system-updates/security-update.png
[5]: ./media/security-center-apply-system-updates/reboot-after-system-updates.png
[6]: ./media/security-center-apply-system-updates/restart-pending.png
