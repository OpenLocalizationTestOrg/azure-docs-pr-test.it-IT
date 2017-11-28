---
title: aaaInstall Endpoint Protection in Centro sicurezza di Azure | Documenti Microsoft
description: Questo documento viene illustrato come tooimplement hello raccomandazione Centro sicurezza di Azure * * installare Endpoint Protection * *.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 1599ad5f-d810-421d-aafc-892e831b403f
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: fea891810e042e4d4f6e55094c0cd4de013ba68a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="install-endpoint-protection-in-azure-security-center"></a><span data-ttu-id="aa0fd-103">Installare Endpoint Protection nel Centro sicurezza di Azure</span><span class="sxs-lookup"><span data-stu-id="aa0fd-103">Install Endpoint Protection in Azure Security Center</span></span>
<span data-ttu-id="aa0fd-104">Il Centro sicurezza di Azure consiglia di installare Endpoint Protection nelle macchine virtuali di Azure se non è già abilitato.</span><span class="sxs-lookup"><span data-stu-id="aa0fd-104">Azure Security Center recommends that you install endpoint protection on your Azure virtual machines (VMs) if endpoint protection is not already enabled.</span></span> <span data-ttu-id="aa0fd-105">Questa indicazione si applica solo tooWindows macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="aa0fd-105">This recommendation applies tooWindows VMs only.</span></span>

> [!NOTE]
> <span data-ttu-id="aa0fd-106">Questo esempio di distribuzione usa Microsoft Antimalware.</span><span class="sxs-lookup"><span data-stu-id="aa0fd-106">This example deployment uses Microsoft Antimalware.</span></span> <span data-ttu-id="aa0fd-107">Vedere [Integrazione di partner nel Centro sicurezza di Azure](security-center-partner-integration.md#partners-that-integrate-with-security-center) per un elenco di partner integrati con il Centro sicurezza.</span><span class="sxs-lookup"><span data-stu-id="aa0fd-107">See [Partner Integration in Azure Security Center](security-center-partner-integration.md#partners-that-integrate-with-security-center) for a list of partners integrated with Security Center.</span></span>  
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="aa0fd-108">Implementare la raccomandazione hello</span><span class="sxs-lookup"><span data-stu-id="aa0fd-108">Implement hello recommendation</span></span>

> [!NOTE]
> <span data-ttu-id="aa0fd-109">Questo documento introduce servizio hello utilizzando un esempio di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="aa0fd-109">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="aa0fd-110">Questo argomento non costituisce una guida dettagliata.</span><span class="sxs-lookup"><span data-stu-id="aa0fd-110">This document is not a step-by-step guide.</span></span>
>
>

1. <span data-ttu-id="aa0fd-111">In hello **indicazioni** pannello seleziona **installa Endpoint Protection**.</span><span class="sxs-lookup"><span data-stu-id="aa0fd-111">In hello **Recommendations** blade, select **Install Endpoint Protection**.</span></span>
   <span data-ttu-id="aa0fd-112">![Selezionare Installa Endpoint Protection][1]</span><span class="sxs-lookup"><span data-stu-id="aa0fd-112">![Select Install Endpoint Protection][1]</span></span>
2. <span data-ttu-id="aa0fd-113">Hello **installa Endpoint Protection** pannello verrà aperto un elenco di macchine virtuali senza la protezione di endpoint.</span><span class="sxs-lookup"><span data-stu-id="aa0fd-113">hello **Install Endpoint Protection** blade opens displaying a list of VMs without endpoint protection.</span></span> <span data-ttu-id="aa0fd-114">Selezionare una delle hello elenco hello macchine virtuali che si vuole che tooinstall endpoint protection in e fare clic su **installare nelle macchine virtuali**.</span><span class="sxs-lookup"><span data-stu-id="aa0fd-114">Select from hello list hello VMs that you want tooinstall endpoint protection on and click **Install on VMs**.</span></span>
   <span data-ttu-id="aa0fd-115">![Selezionare le macchine virtuali tooinstall Endpoint Protection in][2]</span><span class="sxs-lookup"><span data-stu-id="aa0fd-115">![Select VMs tooinstall Endpoint Protection on][2]</span></span>
3. <span data-ttu-id="aa0fd-116">Hello **selezionare Endpoint Protection** pannello apre tooallow si tooselect hello endpoint protection soluzione desiderata toouse.</span><span class="sxs-lookup"><span data-stu-id="aa0fd-116">hello **Select Endpoint Protection** blade opens tooallow you tooselect hello endpoint protection solution you want toouse.</span></span> <span data-ttu-id="aa0fd-117">In questo esempio viene selezionato **Microsoft Antimalware**.</span><span class="sxs-lookup"><span data-stu-id="aa0fd-117">In this example, let's select **Microsoft Antimalware**.</span></span>
   <span data-ttu-id="aa0fd-118">![Seleziona Endpoint Protection][3]</span><span class="sxs-lookup"><span data-stu-id="aa0fd-118">![Select Endpoint Protection][3]</span></span>
4. <span data-ttu-id="aa0fd-119">Ulteriori informazioni sulla soluzione di protezione endpoint hello viene visualizzate.</span><span class="sxs-lookup"><span data-stu-id="aa0fd-119">Additional information about hello endpoint protection solution is displayed.</span></span> <span data-ttu-id="aa0fd-120">Selezionare **Crea**.</span><span class="sxs-lookup"><span data-stu-id="aa0fd-120">Select **Create**.</span></span>
   <span data-ttu-id="aa0fd-121">![Creare una soluzione antimalware][4]</span><span class="sxs-lookup"><span data-stu-id="aa0fd-121">![Create antimalware solution][4]</span></span>
5. <span data-ttu-id="aa0fd-122">Immettere le impostazioni di configurazione necessarie hello hello **Aggiungi estensione** blade e quindi selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="aa0fd-122">Enter hello required configuration settings on hello **Add Extension** blade, and then select **OK**.</span></span> <span data-ttu-id="aa0fd-123">toolearn informazioni sulle impostazioni di configurazione hello, vedere [predefiniti e personalizzati Antimalware configurazione](../security/azure-security-antimalware.md#default-and-custom-antimalware-configuration).</span><span class="sxs-lookup"><span data-stu-id="aa0fd-123">toolearn more about hello configuration settings, see [Default and Custom Antimalware Configuration](../security/azure-security-antimalware.md#default-and-custom-antimalware-configuration).</span></span>

<span data-ttu-id="aa0fd-124">[Microsoft Antimalware](../security/azure-security-antimalware.md) è ora attivo in hello selezionate le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="aa0fd-124">[Microsoft Antimalware](../security/azure-security-antimalware.md) is now active on hello selected VMs.</span></span>

## <a name="see-also"></a><span data-ttu-id="aa0fd-125">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="aa0fd-125">See also</span></span>
<span data-ttu-id="aa0fd-126">In questo articolo ha illustrato come tooimplement hello raccomandazione Centro sicurezza PC "Installa Endpoint Protection".</span><span class="sxs-lookup"><span data-stu-id="aa0fd-126">This article showed you how tooimplement hello Security Center recommendation "Install Endpoint Protection."</span></span> <span data-ttu-id="aa0fd-127">toolearn ulteriori informazioni su attivazione di Microsoft Antimalware in Azure, vedere hello seguente documento:</span><span class="sxs-lookup"><span data-stu-id="aa0fd-127">toolearn more about enabling Microsoft Antimalware in Azure, see hello following document:</span></span>

* <span data-ttu-id="aa0fd-128">[Microsoft Antimalware per servizi Cloud e macchine virtuali](../security/azure-security-antimalware.md) -informazioni su come toodeploy Microsoft Antimalware.</span><span class="sxs-lookup"><span data-stu-id="aa0fd-128">[Microsoft Antimalware for Cloud Services and Virtual Machines](../security/azure-security-antimalware.md) -- Learn how toodeploy Microsoft Antimalware.</span></span>

<span data-ttu-id="aa0fd-129">toolearn ulteriori informazioni su Centro di sicurezza, vedere hello seguenti documenti:</span><span class="sxs-lookup"><span data-stu-id="aa0fd-129">toolearn more about Security Center, see hello following documents:</span></span>

* <span data-ttu-id="aa0fd-130">[L'impostazione di criteri di sicurezza nel Centro protezione Azure](security-center-policies.md) -informazioni su come tooconfigure criteri di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="aa0fd-130">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies.</span></span>
* <span data-ttu-id="aa0fd-131">[Gestione delle raccomandazioni di sicurezza nel Centro sicurezza di Azure](security-center-recommendations.md) : informazioni sul modo in cui le raccomandazioni semplificano la protezione delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="aa0fd-131">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="aa0fd-132">[Il monitoraggio dello stato di sicurezza nel Centro protezione Azure](security-center-monitoring.md) -informazioni su come toomonitor hello integrità delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="aa0fd-132">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="aa0fd-133">[La gestione e risponde toosecurity gli avvisi in Centro sicurezza di Azure](security-center-managing-and-responding-alerts.md) -informazioni su come avvisi toosecurity toomanage e rispondere.</span><span class="sxs-lookup"><span data-stu-id="aa0fd-133">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="aa0fd-134">[Monitoraggio di soluzioni dei partner con Centro sicurezza di Azure](security-center-partner-solutions.md) -informazioni su come toomonitor hello lo stato di integrità delle soluzioni di partner.</span><span class="sxs-lookup"><span data-stu-id="aa0fd-134">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="aa0fd-135">[Domande frequenti su Centro sicurezza di Azure](security-center-faq.md) -domande frequenti sull'utilizzo di hello servizio di ricerca.</span><span class="sxs-lookup"><span data-stu-id="aa0fd-135">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="aa0fd-136">[Blog sulla sicurezza di Azure](http://blogs.msdn.com/b/azuresecurity/) : post di blog sulla sicurezza e sulla conformità di Azure.</span><span class="sxs-lookup"><span data-stu-id="aa0fd-136">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]:./media/security-center-install-endpoint-protection/select-install-endpoint-protection.png
[2]:./media/security-center-install-endpoint-protection/install-endpoint-protection-blade.png
[3]:./media/security-center-install-endpoint-protection/select-endpoint-protection.png
[4]:./media/security-center-install-endpoint-protection/create-antimalware-solution.png
