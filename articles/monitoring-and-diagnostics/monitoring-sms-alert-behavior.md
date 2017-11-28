---
title: comportamento di avviso aaaSMS in gruppi di azioni | Documenti Microsoft
description: Formato del messaggio SMS e risponde tooSMS messaggi toounsubscribe, ripetuta o richiedere assistenza.
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: ancav
ms.openlocfilehash: 3cd09b1903e3472f6402f62b74409d97e7e7ea97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="sms-alert-behavior-in-action-groups"></a><span data-ttu-id="8b9a8-103">Comportamento degli avvisi SMS nei gruppi di azione</span><span class="sxs-lookup"><span data-stu-id="8b9a8-103">SMS Alert Behavior in Action Groups</span></span>
## <a name="overview"></a><span data-ttu-id="8b9a8-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="8b9a8-104">Overview</span></span> ##
<span data-ttu-id="8b9a8-105">Gruppi di azioni consentono di tooconfigure un elenco di destinatari.</span><span class="sxs-lookup"><span data-stu-id="8b9a8-105">Action groups enable you tooconfigure a list of receivers.</span></span> <span data-ttu-id="8b9a8-106">Questi gruppi possono quindi essere utilizzati quando si definiscono gli avvisi del registro attività; verifica che un gruppo particolare azione riceve una notifica quando viene attivato l'avviso di log attività hello.</span><span class="sxs-lookup"><span data-stu-id="8b9a8-106">These groups can then be leveraged when defining activity log alerts; ensuring that a particular action group is notified when hello activity log alert is triggered.</span></span> <span data-ttu-id="8b9a8-107">Uno degli avvisi meccanismi supportati hello è SMS; gli avvisi di Hello supportano la comunicazione bidirezionale.</span><span class="sxs-lookup"><span data-stu-id="8b9a8-107">One of hello alerting mechanisms supported is SMS; hello alerts support bi-directional communication.</span></span> <span data-ttu-id="8b9a8-108">Un utente può rispondere tooan avviso:</span><span class="sxs-lookup"><span data-stu-id="8b9a8-108">A user can respond tooan alert to:</span></span>

- <span data-ttu-id="8b9a8-109">**Annullare la sottoscrizione agli avvisi:** un utente può annullare la sottoscrizione a tutti gli avvisi SMS per tutti i gruppi di azione o per un singolo gruppo di azioni.</span><span class="sxs-lookup"><span data-stu-id="8b9a8-109">**Unsubscribe from alerts:** A user can unsubscribe from all SMS alerts for all action groups, or a singular action group.</span></span>  
- <span data-ttu-id="8b9a8-110">**Ripetuta tooalerts:** un utente può ripetuta tooall gli avvisi SMS per tutti i gruppi di azioni o un gruppo di azioni singolare.</span><span class="sxs-lookup"><span data-stu-id="8b9a8-110">**Resubscribe tooalerts:** A user can resubscribe tooall SMS alerts for all action groups, or a singular action group.</span></span>  
- <span data-ttu-id="8b9a8-111">**Richiedere assistenza:** un utente può chiedere ulteriori informazioni su hello SMS.</span><span class="sxs-lookup"><span data-stu-id="8b9a8-111">**Request help:** A user can ask for more information on hello SMS.</span></span> <span data-ttu-id="8b9a8-112">Sarà reindirizzato toothis articolo</span><span class="sxs-lookup"><span data-stu-id="8b9a8-112">They will be redirected toothis article</span></span>

<span data-ttu-id="8b9a8-113">Questo articolo descrive il comportamento di hello degli avvisi SMS hello e hello risposta azioni hello utente può eseguire in base alle impostazioni locali di hello dell'utente hello:</span><span class="sxs-lookup"><span data-stu-id="8b9a8-113">This article covers hello behavior of hello SMS alerts and hello response actions hello user can take based on hello locale of hello user:</span></span>

## <a name="usacanada-sms-behavior"></a><span data-ttu-id="8b9a8-114">Comportamento SMS per Stati Uniti e Canada</span><span class="sxs-lookup"><span data-stu-id="8b9a8-114">USA/Canada SMS behavior</span></span>
### <a name="receiving-an-sms-alert"></a><span data-ttu-id="8b9a8-115">Ricezione di un avviso SMS</span><span class="sxs-lookup"><span data-stu-id="8b9a8-115">Receiving an SMS Alert</span></span>
<span data-ttu-id="8b9a8-116">Un ricevitore di SMS, configurato come parte di un gruppo di azioni, riceverà un SMS quando viene generato un avviso.</span><span class="sxs-lookup"><span data-stu-id="8b9a8-116">An SMS receiver, who is configured as part of an action group, will receive an SMS when an alert fires.</span></span> <span data-ttu-id="8b9a8-117">Hello SMS trasporterà hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="8b9a8-117">hello SMS will carry hello following information:</span></span>
* <span data-ttu-id="8b9a8-118">ShortName del gruppo di azioni hello questo avviso è stato inviato a</span><span class="sxs-lookup"><span data-stu-id="8b9a8-118">Shortname of hello action group this alert was sent to</span></span>
- <span data-ttu-id="8b9a8-119">Titolo dell'avviso hello</span><span class="sxs-lookup"><span data-stu-id="8b9a8-119">Title of hello alert</span></span>

### <a name="unsubscribing-from-sms-alerts-for-one-action-group"></a><span data-ttu-id="8b9a8-120">Annullamento della sottoscrizione agli avvisi SMS per un gruppo di azioni</span><span class="sxs-lookup"><span data-stu-id="8b9a8-120">Unsubscribing from SMS alerts for one action group</span></span>
<span data-ttu-id="8b9a8-121">Un utente può annullare la sottoscrizione SMS per gli avvisi per gruppo di un'azione risponde toohello 20873 con parole chiave hello: "DISABILITARE &lt;Shortname del gruppo di azioni&gt;".</span><span class="sxs-lookup"><span data-stu-id="8b9a8-121">A user can unsubscribe from SMS for alerts for one action group by responding toohello shortcode 20873 with hello keywords: “DISABLE &lt;Shortname of action group&gt;”.</span></span>

<span data-ttu-id="8b9a8-122">Esempio:</span><span class="sxs-lookup"><span data-stu-id="8b9a8-122">Ex.</span></span> <span data-ttu-id="8b9a8-123">Un utente che desiderano toounsubscribe dagli avvisi per un gruppo di azioni con shortname hello "Azure", viene inviato un toohello SMS 20873 indicante "DISABILITARE Azure"</span><span class="sxs-lookup"><span data-stu-id="8b9a8-123">A user wishing toounsubscribe from alerts for an action group with hello shortname “Azure”, would send an SMS toohello shortcode 20873 that says “DISABLE Azure”</span></span>

### <a name="unsubscribing-from-sms-alerts-for-all-action-groups"></a><span data-ttu-id="8b9a8-124">Annullamento della sottoscrizione agli avvisi SMS per tutti i gruppi di azioni</span><span class="sxs-lookup"><span data-stu-id="8b9a8-124">Unsubscribing from SMS alerts for all action groups</span></span>
<span data-ttu-id="8b9a8-125">Un utente può annullare la sottoscrizione tutti gli avvisi SMS per tutti i gruppi di azione risponde toohello 20873 con uno qualsiasi di hello parole chiave seguenti:</span><span class="sxs-lookup"><span data-stu-id="8b9a8-125">A user can unsubscribe from all SMS alerts for all action groups by responding toohello shortcode 20873 with any of hello following keywords:</span></span>
* <span data-ttu-id="8b9a8-126">STOP</span><span class="sxs-lookup"><span data-stu-id="8b9a8-126">STOP</span></span>

<span data-ttu-id="8b9a8-127">Esempio:</span><span class="sxs-lookup"><span data-stu-id="8b9a8-127">Ex.</span></span> <span data-ttu-id="8b9a8-128">Un utente che desiderano toounsubscribe da tutti gli avvisi SMS per tutti i gruppi di azioni, viene inviato un toohello SMS 20873 indicante "STOP"</span><span class="sxs-lookup"><span data-stu-id="8b9a8-128">A user wishing toounsubscribe from all SMS alerts for all action groups, would send an SMS toohello shortcode 20873 that says “STOP”</span></span>

>[!NOTE]
><span data-ttu-id="8b9a8-129">Se un utente ha annullato la sottoscrizione da SMS avvisi, ma viene quindi aggiunto tooa azione al gruppo precedente. si verrà ricevere gli avvisi SMS per il nuovo gruppo di azioni, ma rimangono annullate da tutti i gruppi di azione precedente.</span><span class="sxs-lookup"><span data-stu-id="8b9a8-129">If a user has unsubscribed from SMS alerts, but is then added tooa new action group; they WILL receive SMS alerts for that new action group, but remain unsubscribed from all previous action groups.</span></span>
>
>

### <a name="resubscribing-toosms-alerts-for-one-action-group"></a><span data-ttu-id="8b9a8-130">Ripetere la sottoscrizione tooSMS gli avvisi per un gruppo di azioni</span><span class="sxs-lookup"><span data-stu-id="8b9a8-130">Resubscribing tooSMS alerts for one action group</span></span>
<span data-ttu-id="8b9a8-131">Un utente può ripetuta tooSMS per gli avvisi per gruppo di un'azione da risponde toohello 20873 con parole chiave hello: "abilitare &lt;Shortname del gruppo di azioni&gt;".</span><span class="sxs-lookup"><span data-stu-id="8b9a8-131">A user can resubscribe tooSMS for alerts for one action group by responding toohello shortcode 20873 with hello keywords: “ENABLE &lt;Shortname of action group&gt;”.</span></span>

<span data-ttu-id="8b9a8-132">Esempio:</span><span class="sxs-lookup"><span data-stu-id="8b9a8-132">Ex.</span></span> <span data-ttu-id="8b9a8-133">Un utente che desiderano tooalerts tooresubscribe per un gruppo di azioni con shortname hello "Azure", viene inviato un toohello SMS 20873 indicante "Abilitare Azure"</span><span class="sxs-lookup"><span data-stu-id="8b9a8-133">A user wishing tooresubscribe tooalerts for an action group with hello shortname “Azure”, would send an SMS toohello shortcode 20873 that says “ENABLE Azure”</span></span>

### <a name="resubscribing-toosms-alerts-for-all-action-groups"></a><span data-ttu-id="8b9a8-134">Ripetere la sottoscrizione tooSMS gli avvisi per tutti i gruppi di azioni</span><span class="sxs-lookup"><span data-stu-id="8b9a8-134">Resubscribing tooSMS alerts for all action groups</span></span>
<span data-ttu-id="8b9a8-135">Un utente può ripetuta tooall SMS per gli avvisi per tutti i gruppi di azioni da risponde toohello 20873 con uno qualsiasi di hello parole chiave seguenti:</span><span class="sxs-lookup"><span data-stu-id="8b9a8-135">A user can resubscribe tooall SMS for alerts for all action groups by responding toohello shortcode 20873 with any of hello following keywords:</span></span>

* <span data-ttu-id="8b9a8-136">START</span><span class="sxs-lookup"><span data-stu-id="8b9a8-136">START</span></span>

<span data-ttu-id="8b9a8-137">Esempio:</span><span class="sxs-lookup"><span data-stu-id="8b9a8-137">Ex.</span></span> <span data-ttu-id="8b9a8-138">Un utente che desiderano toounsubscribe da tutti gli avvisi SMS per tutti i gruppi di azioni, viene inviato un toohello SMS 20873 indicante "START"</span><span class="sxs-lookup"><span data-stu-id="8b9a8-138">A user wishing toounsubscribe from all SMS alerts for all action groups, would send an SMS toohello shortcode 20873 that says “START”</span></span>

### <a name="requesting-help-via-sms"></a><span data-ttu-id="8b9a8-139">Richiesta di assistenza tramite SMS</span><span class="sxs-lookup"><span data-stu-id="8b9a8-139">Requesting help via SMS</span></span>
<span data-ttu-id="8b9a8-140">Un utente può chiedere per ulteriori informazioni su hello SMS ricevuti da risponde toohello 20873 con una delle seguenti parole chiave hello:</span><span class="sxs-lookup"><span data-stu-id="8b9a8-140">A user can ask for more information about hello SMS they have received by responding toohello shortcode 20873 with any of hello following keywords:</span></span>
* <span data-ttu-id="8b9a8-141">HELP</span><span class="sxs-lookup"><span data-stu-id="8b9a8-141">HELP</span></span>

<span data-ttu-id="8b9a8-142">Verrà inviata una risposta toohello utente con un articolo toothis di collegamento.</span><span class="sxs-lookup"><span data-stu-id="8b9a8-142">A response will be sent toohello user with a link toothis article.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8b9a8-143">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8b9a8-143">Next Steps</span></span>
<span data-ttu-id="8b9a8-144">Ottenere un [panoramica degli avvisi di log attività](monitoring-overview-alerts.md) e informazioni su come viene generato un avviso di tooget</span><span class="sxs-lookup"><span data-stu-id="8b9a8-144">Get an [overview of activity log alerts](monitoring-overview-alerts.md) and learn how tooget alerted</span></span>  
<span data-ttu-id="8b9a8-145">Altre informazioni sulla [limitazione della frequenza degli SMS](monitoring-alerts-rate-limiting.md)</span><span class="sxs-lookup"><span data-stu-id="8b9a8-145">Learn more about [SMS rate limiting](monitoring-alerts-rate-limiting.md)</span></span>  
<span data-ttu-id="8b9a8-146">Altre informazioni sui [gruppi di azioni](monitoring-action-groups.md)</span><span class="sxs-lookup"><span data-stu-id="8b9a8-146">Learn more about [action groups](monitoring-action-groups.md)</span></span>
