---
title: Installare Endpoint Protection nel Centro sicurezza di Azure | Documentazione Microsoft
description: "In questo documento è illustrato come implementare la raccomandazione \"**Installa Endpoint Protection**\" del Centro sicurezza di Azure."
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
ms.openlocfilehash: efb86a0ae362c30a6772c391a499154b7ae2a697
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="install-endpoint-protection-in-azure-security-center"></a><span data-ttu-id="2e9b9-103">Installare Endpoint Protection nel Centro sicurezza di Azure</span><span class="sxs-lookup"><span data-stu-id="2e9b9-103">Install Endpoint Protection in Azure Security Center</span></span>
<span data-ttu-id="2e9b9-104">Il Centro sicurezza di Azure consiglia di installare Endpoint Protection nelle macchine virtuali di Azure se non è già abilitato.</span><span class="sxs-lookup"><span data-stu-id="2e9b9-104">Azure Security Center recommends that you install endpoint protection on your Azure virtual machines (VMs) if endpoint protection is not already enabled.</span></span> <span data-ttu-id="2e9b9-105">Questo suggerimento si applica solo alle macchine virtuali Windows.</span><span class="sxs-lookup"><span data-stu-id="2e9b9-105">This recommendation applies to Windows VMs only.</span></span>

> [!NOTE]
> <span data-ttu-id="2e9b9-106">Questo esempio di distribuzione usa Microsoft Antimalware.</span><span class="sxs-lookup"><span data-stu-id="2e9b9-106">This example deployment uses Microsoft Antimalware.</span></span> <span data-ttu-id="2e9b9-107">Vedere [Integrazione di partner nel Centro sicurezza di Azure](security-center-partner-integration.md#partners-that-integrate-with-security-center) per un elenco di partner integrati con il Centro sicurezza.</span><span class="sxs-lookup"><span data-stu-id="2e9b9-107">See [Partner Integration in Azure Security Center](security-center-partner-integration.md#partners-that-integrate-with-security-center) for a list of partners integrated with Security Center.</span></span>  
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="2e9b9-108">Implementare la raccomandazione</span><span class="sxs-lookup"><span data-stu-id="2e9b9-108">Implement the recommendation</span></span>

> [!NOTE]
> <span data-ttu-id="2e9b9-109">Il documento introduce il servizio usando una distribuzione di esempio.</span><span class="sxs-lookup"><span data-stu-id="2e9b9-109">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="2e9b9-110">Questo argomento non costituisce una guida dettagliata.</span><span class="sxs-lookup"><span data-stu-id="2e9b9-110">This document is not a step-by-step guide.</span></span>
>
>

1. <span data-ttu-id="2e9b9-111">Nel pannello **Raccomandazioni** selezionare **Installa Endpoint Protection**.</span><span class="sxs-lookup"><span data-stu-id="2e9b9-111">In the **Recommendations** blade, select **Install Endpoint Protection**.</span></span>
   <span data-ttu-id="2e9b9-112">![Selezionare Installa Endpoint Protection][1]</span><span class="sxs-lookup"><span data-stu-id="2e9b9-112">![Select Install Endpoint Protection][1]</span></span>
2. <span data-ttu-id="2e9b9-113">Viene visualizzato il pannello **Installa Endpoint Protection** che mostra un elenco di macchine virtuali senza Installa Endpoint Protection.</span><span class="sxs-lookup"><span data-stu-id="2e9b9-113">The **Install Endpoint Protection** blade opens displaying a list of VMs without endpoint protection.</span></span> <span data-ttu-id="2e9b9-114">Selezionare dall'elenco le macchine virtuali in cui si vuole installare Endpoint Protection e fare clic su **Install on VMs** (Installa nelle macchine virtuali).</span><span class="sxs-lookup"><span data-stu-id="2e9b9-114">Select from the list the VMs that you want to install endpoint protection on and click **Install on VMs**.</span></span>
   <span data-ttu-id="2e9b9-115">![Selezionare le macchine virtuali su cui installare Endpoint Protection][2]</span><span class="sxs-lookup"><span data-stu-id="2e9b9-115">![Select VMs to install Endpoint Protection on][2]</span></span>
3. <span data-ttu-id="2e9b9-116">Viene visualizzato il pannello **Seleziona Endpoint Protection**, che consente di selezionare la soluzione di Endpoint Protection da usare.</span><span class="sxs-lookup"><span data-stu-id="2e9b9-116">The **Select Endpoint Protection** blade opens to allow you to select the endpoint protection solution you want to use.</span></span> <span data-ttu-id="2e9b9-117">In questo esempio viene selezionato **Microsoft Antimalware**.</span><span class="sxs-lookup"><span data-stu-id="2e9b9-117">In this example, let's select **Microsoft Antimalware**.</span></span>
   <span data-ttu-id="2e9b9-118">![Seleziona Endpoint Protection][3]</span><span class="sxs-lookup"><span data-stu-id="2e9b9-118">![Select Endpoint Protection][3]</span></span>
4. <span data-ttu-id="2e9b9-119">Vengono visualizzate altre informazioni sulla soluzione di Endpoint Protection selezionata.</span><span class="sxs-lookup"><span data-stu-id="2e9b9-119">Additional information about the endpoint protection solution is displayed.</span></span> <span data-ttu-id="2e9b9-120">Selezionare **Crea**.</span><span class="sxs-lookup"><span data-stu-id="2e9b9-120">Select **Create**.</span></span>
   <span data-ttu-id="2e9b9-121">![Creare una soluzione antimalware][4]</span><span class="sxs-lookup"><span data-stu-id="2e9b9-121">![Create antimalware solution][4]</span></span>
5. <span data-ttu-id="2e9b9-122">Specificare le impostazioni di configurazione necessarie nel pannello **Aggiungi estensione** e quindi selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="2e9b9-122">Enter the required configuration settings on the **Add Extension** blade, and then select **OK**.</span></span> <span data-ttu-id="2e9b9-123">Per altre informazioni sulle impostazioni di configurazione, vedere [Configurazione di Antimalware predefinita e personalizzata](../security/azure-security-antimalware.md#default-and-custom-antimalware-configuration).</span><span class="sxs-lookup"><span data-stu-id="2e9b9-123">To learn more about the configuration settings, see [Default and Custom Antimalware Configuration](../security/azure-security-antimalware.md#default-and-custom-antimalware-configuration).</span></span>

<span data-ttu-id="2e9b9-124">[Microsoft Antimalware](../security/azure-security-antimalware.md) è ora attivo nelle VM selezionate.</span><span class="sxs-lookup"><span data-stu-id="2e9b9-124">[Microsoft Antimalware](../security/azure-security-antimalware.md) is now active on the selected VMs.</span></span>

## <a name="see-also"></a><span data-ttu-id="2e9b9-125">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="2e9b9-125">See also</span></span>
<span data-ttu-id="2e9b9-126">Questo documento illustra come implementare la raccomandazione "Installa Endpoint Protection" del Centro sicurezza.</span><span class="sxs-lookup"><span data-stu-id="2e9b9-126">This article showed you how to implement the Security Center recommendation "Install Endpoint Protection."</span></span> <span data-ttu-id="2e9b9-127">Per altre informazioni sull'abilitazione di un programma antimalware di Microsoft in Azure, vedere i documenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="2e9b9-127">To learn more about enabling Microsoft Antimalware in Azure, see the following document:</span></span>

* <span data-ttu-id="2e9b9-128">[Microsoft Antimalware per Servizi cloud e Macchine virtuali di Azure](../security/azure-security-antimalware.md): informazioni su come distribuire la protezione antimalware Microsoft.</span><span class="sxs-lookup"><span data-stu-id="2e9b9-128">[Microsoft Antimalware for Cloud Services and Virtual Machines](../security/azure-security-antimalware.md) -- Learn how to deploy Microsoft Antimalware.</span></span>

<span data-ttu-id="2e9b9-129">Per altre informazioni sul Centro sicurezza, vedere i documenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="2e9b9-129">To learn more about Security Center, see the following documents:</span></span>

* <span data-ttu-id="2e9b9-130">[Impostazione dei criteri di sicurezza nel Centro sicurezza di Azure](security-center-policies.md) : informazioni su come configurare i criteri di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="2e9b9-130">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies.</span></span>
* <span data-ttu-id="2e9b9-131">[Gestione delle raccomandazioni di sicurezza nel Centro sicurezza di Azure](security-center-recommendations.md) : informazioni sul modo in cui le raccomandazioni semplificano la protezione delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="2e9b9-131">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="2e9b9-132">[Monitoraggio dell'integrità della sicurezza nel Centro sicurezza di Azure](security-center-monitoring.md) : informazioni su come monitorare l'integrità delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="2e9b9-132">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="2e9b9-133">[Gestione e risposta agli avvisi di sicurezza nel Centro sicurezza di Azure](security-center-managing-and-responding-alerts.md) : informazioni su come gestire e rispondere agli avvisi di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="2e9b9-133">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="2e9b9-134">[Monitoraggio delle soluzioni dei partner con il Centro sicurezza di Azure](security-center-partner-solutions.md) : informazioni su come monitorare lo stato integrità delle soluzioni dei partner.</span><span class="sxs-lookup"><span data-stu-id="2e9b9-134">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="2e9b9-135">[Domande frequenti sul Centro sicurezza di Azure](security-center-faq.md) : domande frequenti sull'uso del servizio.</span><span class="sxs-lookup"><span data-stu-id="2e9b9-135">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="2e9b9-136">[Blog sulla sicurezza di Azure](http://blogs.msdn.com/b/azuresecurity/) : post di blog sulla sicurezza e sulla conformità di Azure.</span><span class="sxs-lookup"><span data-stu-id="2e9b9-136">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]:./media/security-center-install-endpoint-protection/select-install-endpoint-protection.png
[2]:./media/security-center-install-endpoint-protection/install-endpoint-protection-blade.png
[3]:./media/security-center-install-endpoint-protection/select-endpoint-protection.png
[4]:./media/security-center-install-endpoint-protection/create-antimalware-solution.png
