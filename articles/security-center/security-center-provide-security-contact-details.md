---
title: Specificare i dettagli dei contatti di sicurezza nel Centro sicurezza di Azure | Documentazione Microsoft
description: Questo documento illustra come specificare i dettagli dei contatti di sicurezza nel Centro sicurezza di Azure.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 26b5dcb4-ce3f-4f22-8d56-d2bf743cfc90
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 1a6e5e915745dd3588fbc54b353daa947b1c4289
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="provide-security-contact-details-in-azure-security-center"></a><span data-ttu-id="30ab2-103">Specificare i dettagli dei contatti di sicurezza nel Centro sicurezza di Azure</span><span class="sxs-lookup"><span data-stu-id="30ab2-103">Provide security contact details in Azure Security Center</span></span>
<span data-ttu-id="30ab2-104">Il Centro sicurezza di Azure consiglierà di specificare i dettagli dei contatti di sicurezza per la sottoscrizione di Azure, se non è già stato fatto.</span><span class="sxs-lookup"><span data-stu-id="30ab2-104">Azure Security Center will recommend that you provide security contact details for your Azure subscription if you haven’t already.</span></span> <span data-ttu-id="30ab2-105">Queste informazioni verranno usate da Microsoft per contattare l'utente se il Microsoft Security Response Center (MSRC) rileva che un'entità illegale o non autorizzata ha effettuato l'accesso ai dati del cliente.</span><span class="sxs-lookup"><span data-stu-id="30ab2-105">This information will be used by Microsoft to contact you if the Microsoft Security Response Center (MSRC) discovers that your customer data has been accessed by an unlawful or unauthorized party.</span></span> <span data-ttu-id="30ab2-106">Microsoft Security Response Center esegue il monitoraggio selettivo della sicurezza della rete e dell'infrastruttura di Azure e riceve informazioni sulle minacce e segnalazioni di violazioni da terzi.</span><span class="sxs-lookup"><span data-stu-id="30ab2-106">MSRC performs select security monitoring of the Azure network and infrastructure and receives threat intelligence and abuse complaints from third parties.</span></span>

<span data-ttu-id="30ab2-107">Alla prima occorrenza giornaliera di un avviso e solo per gli avvisi di elevata gravità viene inviata una notifica tramite posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="30ab2-107">An email notification is sent on the first daily occurrence of an alert and only for high severity alerts.</span></span> <span data-ttu-id="30ab2-108">Le preferenze di posta elettronica possono essere configurate solo per i criteri della sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="30ab2-108">Email preferences can only be configured for subscription policies.</span></span> <span data-ttu-id="30ab2-109">I gruppi di risorse all'interno di una sottoscrizione ereditano queste impostazioni.</span><span class="sxs-lookup"><span data-stu-id="30ab2-109">Resource groups within a subscription will inherit these settings.</span></span>

> [!NOTE]
> <span data-ttu-id="30ab2-110">Il documento introduce il servizio usando una distribuzione di esempio.</span><span class="sxs-lookup"><span data-stu-id="30ab2-110">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="30ab2-111">Questa non è una guida dettagliata.</span><span class="sxs-lookup"><span data-stu-id="30ab2-111">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="30ab2-112">Implementare la raccomandazione</span><span class="sxs-lookup"><span data-stu-id="30ab2-112">Implement the recommendation</span></span>
1. <span data-ttu-id="30ab2-113">Nel pannello **Indicazioni** selezionare **Specificare i dettagli dei contatti di sicurezza**.</span><span class="sxs-lookup"><span data-stu-id="30ab2-113">In the **Recommendations** blade, select **Provide security contact details**.</span></span>
   <span data-ttu-id="30ab2-114">![Specificare contatti per la sicurezza][1]</span><span class="sxs-lookup"><span data-stu-id="30ab2-114">![Provide security contact][1]</span></span>
2. <span data-ttu-id="30ab2-115">Verrà visualizzato il pannello **Specificare i dettagli dei contatti di sicurezza**.</span><span class="sxs-lookup"><span data-stu-id="30ab2-115">This opens the blade **Provide security contact details**.</span></span> <span data-ttu-id="30ab2-116">Selezionare la sottoscrizione di Azure per cui specificare le informazioni di contatto.</span><span class="sxs-lookup"><span data-stu-id="30ab2-116">Select the Azure subscription to provide contact information on.</span></span>
   <span data-ttu-id="30ab2-117">![Specificare i dettagli dei contatti di sicurezza][2]</span><span class="sxs-lookup"><span data-stu-id="30ab2-117">![Provide security contact details][2]</span></span>
3. <span data-ttu-id="30ab2-118">Viene visualizzato un altro pannello **Specificare i dettagli dei contatti di sicurezza** .</span><span class="sxs-lookup"><span data-stu-id="30ab2-118">A second **Provide security contact details** blade opens.</span></span>

   * <span data-ttu-id="30ab2-119">Immettere l'indirizzo o gli indirizzi di posta elettronica del contatto di sicurezza, separati da virgole.</span><span class="sxs-lookup"><span data-stu-id="30ab2-119">Enter the security contact email address or addresses separated by commas.</span></span> <span data-ttu-id="30ab2-120">Non è previsto alcun limite per il numero di indirizzi di posta elettronica che è possibile immettere.</span><span class="sxs-lookup"><span data-stu-id="30ab2-120">There is not a limit to the number of email addresses that you can enter.</span></span>
   * <span data-ttu-id="30ab2-121">Immettere un numero di telefono internazionale per il contatto di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="30ab2-121">Enter one security contact international phone number.</span></span>
   * <span data-ttu-id="30ab2-122">Per ricevere messaggi di posta elettronica relativi agli avvisi di elevata gravità, attivare l'opzione **Send me emails about alerts**(Invia messaggi di posta elettronica sugli avvisi).</span><span class="sxs-lookup"><span data-stu-id="30ab2-122">To receive emails about high severity alerts, turn on the option **Send me emails about alerts**.</span></span>
   * <span data-ttu-id="30ab2-123">In futuro, sarà possibile inviare notifiche tramite posta elettronica ai proprietari di sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="30ab2-123">In the future, you will have the option to send email notifications to subscription owners.</span></span> <span data-ttu-id="30ab2-124">Attualmente questa opzione non è disponibile.</span><span class="sxs-lookup"><span data-stu-id="30ab2-124">This option is currently grayed out.</span></span>
   * <span data-ttu-id="30ab2-125">Selezionare **OK** per applicare le informazioni di contatto di sicurezza alla sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="30ab2-125">Select **OK** to apply the security contact information to your subscription.</span></span>

## <a name="see-also"></a><span data-ttu-id="30ab2-126">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="30ab2-126">See also</span></span>
<span data-ttu-id="30ab2-127">Per altre informazioni sul Centro sicurezza, vedere gli argomenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="30ab2-127">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="30ab2-128">[Impostazione dei criteri di sicurezza nel Centro sicurezza di Azure](security-center-policies.md) : informazioni su come configurare i criteri di sicurezza per le sottoscrizioni e i gruppi di risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="30ab2-128">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="30ab2-129">[Gestione delle raccomandazioni di sicurezza nel Centro sicurezza di Azure](security-center-recommendations.md) : informazioni sul modo in cui le raccomandazioni semplificano la protezione delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="30ab2-129">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="30ab2-130">[Monitoraggio dell'integrità della sicurezza nel Centro sicurezza di Azure](security-center-monitoring.md) : informazioni su come monitorare l'integrità delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="30ab2-130">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="30ab2-131">[Gestione e risposta agli avvisi di sicurezza nel Centro sicurezza di Azure](security-center-managing-and-responding-alerts.md) : informazioni su come gestire e rispondere agli avvisi di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="30ab2-131">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="30ab2-132">[Monitoraggio delle soluzioni dei partner con il Centro sicurezza di Azure](security-center-partner-solutions.md) : informazioni su come monitorare lo stato integrità delle soluzioni dei partner.</span><span class="sxs-lookup"><span data-stu-id="30ab2-132">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="30ab2-133">[Domande frequenti sul Centro sicurezza di Azure](security-center-faq.md) : domande frequenti sull'uso del servizio.</span><span class="sxs-lookup"><span data-stu-id="30ab2-133">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="30ab2-134">[Blog sulla sicurezza di Azure](http://blogs.msdn.com/b/azuresecurity/) : informazioni e notizie aggiornate sulla sicurezza di Azure.</span><span class="sxs-lookup"><span data-stu-id="30ab2-134">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-provide-security-contacts/provide-contacts.png
[2]:./media/security-center-provide-security-contacts/provide-contact-details.png
