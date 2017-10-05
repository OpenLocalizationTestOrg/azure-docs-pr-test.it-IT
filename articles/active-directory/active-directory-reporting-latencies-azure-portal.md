---
title: Latenze dei report di Azure Active Directory | Microsoft Docs
description: Informazioni sul tempo necessario per la visualizzazione nel portale di Azure degli eventi dei report
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 9b88958d-94a2-4f4b-a18c-616f0617a24e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi;dhanyahk
ms.reviewer: dhanyahk
ms.openlocfilehash: 93cb0baeab8f13f81257ed1bd32ed08561c54b72
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-reporting-latencies"></a><span data-ttu-id="a2d66-103">Latenze dei report di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a2d66-103">Azure Active Directory reporting latencies</span></span>

<span data-ttu-id="a2d66-104">I [report](active-directory-preview-explainer.md) di Azure Active Directory offrono tutte le informazioni necessarie per determinare lo stato dell'ambiente.</span><span class="sxs-lookup"><span data-stu-id="a2d66-104">With [reporting](active-directory-preview-explainer.md) in the Azure Active Directory, you get all the information you need to determine how your environment is doing.</span></span> <span data-ttu-id="a2d66-105">Il tempo necessario per la visualizzazione dei dati di report nel portale di Azure è nota anche come latenza.</span><span class="sxs-lookup"><span data-stu-id="a2d66-105">The amount of time it takes for reporting data to show up in the Azure portal is also known as latency.</span></span> 

<span data-ttu-id="a2d66-106">Questo argomento elenca le informazioni sulla latenza per tutte le categorie di report nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a2d66-106">This topic lists the latency information for the all reporting categories in the Azure portal.</span></span> 


## <a name="activity-reports"></a><span data-ttu-id="a2d66-107">Report sull’attività</span><span class="sxs-lookup"><span data-stu-id="a2d66-107">Activity reports</span></span>

<span data-ttu-id="a2d66-108">Esistono due aree di reporting sulle attività:</span><span class="sxs-lookup"><span data-stu-id="a2d66-108">There are two areas of activity reporting:</span></span>

- <span data-ttu-id="a2d66-109">**Attività di accesso** : informazioni sull'utilizzo delle applicazioni gestite e sulle attività di accesso utente</span><span class="sxs-lookup"><span data-stu-id="a2d66-109">**Sign-in activities** – Information about the usage of managed applications and user sign-in activities</span></span>
- <span data-ttu-id="a2d66-110">**Log di controllo** : informazioni relative alle attività di sistema sulla gestione di utenti e gruppi, sulle applicazioni gestite e sulle attività di directory</span><span class="sxs-lookup"><span data-stu-id="a2d66-110">**Audit logs** - System activity information about users and group management, your managed applications and directory activities</span></span>

<span data-ttu-id="a2d66-111">Nella tabella seguente sono elencate le informazioni sulla latenza per i report di attività.</span><span class="sxs-lookup"><span data-stu-id="a2d66-111">The following table lists the latency information for activity reports.</span></span>

| <span data-ttu-id="a2d66-112">Report</span><span class="sxs-lookup"><span data-stu-id="a2d66-112">Report</span></span> | <span data-ttu-id="a2d66-113">Minima</span><span class="sxs-lookup"><span data-stu-id="a2d66-113">Minimum</span></span> | <span data-ttu-id="a2d66-114">Media</span><span class="sxs-lookup"><span data-stu-id="a2d66-114">Average</span></span> | <span data-ttu-id="a2d66-115">Massima</span><span class="sxs-lookup"><span data-stu-id="a2d66-115">Maximum</span></span> |
| :-- | --- | --- | --- |
| <span data-ttu-id="a2d66-116">Log di controllo</span><span class="sxs-lookup"><span data-stu-id="a2d66-116">Audit logs</span></span>             | <span data-ttu-id="a2d66-117">30 minuti</span><span class="sxs-lookup"><span data-stu-id="a2d66-117">30 minutes</span></span>  | <span data-ttu-id="a2d66-118">45 minuti</span><span class="sxs-lookup"><span data-stu-id="a2d66-118">45 Minutes</span></span> | <span data-ttu-id="a2d66-119">1 ora</span><span class="sxs-lookup"><span data-stu-id="a2d66-119">1 hour</span></span>     |
| <span data-ttu-id="a2d66-120">Accessi</span><span class="sxs-lookup"><span data-stu-id="a2d66-120">Sign-ins</span></span>               | <span data-ttu-id="a2d66-121">15 minuti</span><span class="sxs-lookup"><span data-stu-id="a2d66-121">15 minutes</span></span>  | <span data-ttu-id="a2d66-122">15 minuti</span><span class="sxs-lookup"><span data-stu-id="a2d66-122">15 minutes</span></span> | <span data-ttu-id="a2d66-123">2 ore*</span><span class="sxs-lookup"><span data-stu-id="a2d66-123">2 hours*</span></span>   |

>[!NOTE]
> <span data-ttu-id="a2d66-124">Per alcuni dati di attività di accesso provenienti da applicazioni legacy di office, potrebbero essere necessarie fino a 8 ore per la visualizzazione dei dati dei report.</span><span class="sxs-lookup"><span data-stu-id="a2d66-124">For some sign-ins activity data coming from legacy office applications, it can take to 8 hours for the reporting data to show up.</span></span> 


## <a name="security-reports"></a><span data-ttu-id="a2d66-125">Report sulla sicurezza</span><span class="sxs-lookup"><span data-stu-id="a2d66-125">Security reports</span></span>

<span data-ttu-id="a2d66-126">Esistono due aree di reporting sulla sicurezza:</span><span class="sxs-lookup"><span data-stu-id="a2d66-126">There are two areas of security reporting:</span></span>

- <span data-ttu-id="a2d66-127">**Accessi a rischio**. Un accesso rischioso è indicativo di un tentativo di accesso che potrebbe essere stato eseguito da qualcuno che non è il legittimo proprietario di un account utente.</span><span class="sxs-lookup"><span data-stu-id="a2d66-127">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not the legitimate owner of a user account.</span></span> 
- <span data-ttu-id="a2d66-128">**Utenti contrassegnati per il rischio**. Un utente rischioso è indicativo di un account utente che potrebbe essere stato compromesso.</span><span class="sxs-lookup"><span data-stu-id="a2d66-128">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> 

<span data-ttu-id="a2d66-129">Nella tabella seguente sono elencate le informazioni sulla latenza per i report di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="a2d66-129">The following table lists the latency information for security reports.</span></span>

| <span data-ttu-id="a2d66-130">Report</span><span class="sxs-lookup"><span data-stu-id="a2d66-130">Report</span></span> | <span data-ttu-id="a2d66-131">Minima</span><span class="sxs-lookup"><span data-stu-id="a2d66-131">Minimum</span></span> | <span data-ttu-id="a2d66-132">Media</span><span class="sxs-lookup"><span data-stu-id="a2d66-132">Average</span></span> | <span data-ttu-id="a2d66-133">Massima</span><span class="sxs-lookup"><span data-stu-id="a2d66-133">Maximum</span></span> |
| :-- | --- | --- | --- |
| <span data-ttu-id="a2d66-134">Utenti a rischio.</span><span class="sxs-lookup"><span data-stu-id="a2d66-134">Users at risk</span></span>          | <span data-ttu-id="a2d66-135">5 minuti</span><span class="sxs-lookup"><span data-stu-id="a2d66-135">5 minutes</span></span>   | <span data-ttu-id="a2d66-136">15 minuti</span><span class="sxs-lookup"><span data-stu-id="a2d66-136">15 minutes</span></span>  | <span data-ttu-id="a2d66-137">2 ore</span><span class="sxs-lookup"><span data-stu-id="a2d66-137">2 hours</span></span>  |
| <span data-ttu-id="a2d66-138">Accessi a rischio</span><span class="sxs-lookup"><span data-stu-id="a2d66-138">Risky sign-ins</span></span>         | <span data-ttu-id="a2d66-139">5 minuti</span><span class="sxs-lookup"><span data-stu-id="a2d66-139">5 minutes</span></span>   | <span data-ttu-id="a2d66-140">15 minuti</span><span class="sxs-lookup"><span data-stu-id="a2d66-140">15 minutes</span></span>  | <span data-ttu-id="a2d66-141">2 ore</span><span class="sxs-lookup"><span data-stu-id="a2d66-141">2 hours</span></span>  |

## <a name="risk-events"></a><span data-ttu-id="a2d66-142">Eventi di rischio</span><span class="sxs-lookup"><span data-stu-id="a2d66-142">Risk events</span></span>

<span data-ttu-id="a2d66-143">Azure Active Directory usa l'euristica e gli algoritmi adattivi di Machine Learning per rilevare azioni sospette correlate agli account dell'utente.</span><span class="sxs-lookup"><span data-stu-id="a2d66-143">Azure Active Directory uses adaptive machine learning algorithms and heuristics to detect suspicious actions that are related to your user accounts.</span></span> <span data-ttu-id="a2d66-144">Ogni azione sospetta rilevata viene archiviata in un record denominato evento di rischio.</span><span class="sxs-lookup"><span data-stu-id="a2d66-144">Each detected suspicious action is stored in a record called risk event.</span></span>

<span data-ttu-id="a2d66-145">Nella tabella seguente sono elencate le informazioni sulla latenza per gli eventi di rischio.</span><span class="sxs-lookup"><span data-stu-id="a2d66-145">The following table lists the latency information for risk events.</span></span>

| <span data-ttu-id="a2d66-146">Report</span><span class="sxs-lookup"><span data-stu-id="a2d66-146">Report</span></span> | <span data-ttu-id="a2d66-147">Minima</span><span class="sxs-lookup"><span data-stu-id="a2d66-147">Minimum</span></span> | <span data-ttu-id="a2d66-148">Media</span><span class="sxs-lookup"><span data-stu-id="a2d66-148">Average</span></span> | <span data-ttu-id="a2d66-149">Massima</span><span class="sxs-lookup"><span data-stu-id="a2d66-149">Maximum</span></span> |
| :-- | --- | --- | --- |
| <span data-ttu-id="a2d66-150">Accessi da indirizzi IP anonimi</span><span class="sxs-lookup"><span data-stu-id="a2d66-150">Sign-ins from anonymous IP addresses</span></span> |<span data-ttu-id="a2d66-151">5 minuti</span><span class="sxs-lookup"><span data-stu-id="a2d66-151">5 minutes</span></span> |<span data-ttu-id="a2d66-152">15 minuti</span><span class="sxs-lookup"><span data-stu-id="a2d66-152">15 Minutes</span></span> |<span data-ttu-id="a2d66-153">2 ore</span><span class="sxs-lookup"><span data-stu-id="a2d66-153">2 hours</span></span> |
| <span data-ttu-id="a2d66-154">Accessi da posizioni non note</span><span class="sxs-lookup"><span data-stu-id="a2d66-154">Sign-ins from unfamiliar locations</span></span> |<span data-ttu-id="a2d66-155">5 minuti</span><span class="sxs-lookup"><span data-stu-id="a2d66-155">5 minutes</span></span> |<span data-ttu-id="a2d66-156">15 minuti</span><span class="sxs-lookup"><span data-stu-id="a2d66-156">15 Minutes</span></span> |<span data-ttu-id="a2d66-157">2 ore</span><span class="sxs-lookup"><span data-stu-id="a2d66-157">2 hours</span></span> |
| <span data-ttu-id="a2d66-158">Utenti con credenziali perse</span><span class="sxs-lookup"><span data-stu-id="a2d66-158">Users with leaked credentials</span></span> |<span data-ttu-id="a2d66-159">2 ore</span><span class="sxs-lookup"><span data-stu-id="a2d66-159">2 hours</span></span> |<span data-ttu-id="a2d66-160">4 ore</span><span class="sxs-lookup"><span data-stu-id="a2d66-160">4 hours</span></span> |<span data-ttu-id="a2d66-161">8 ore</span><span class="sxs-lookup"><span data-stu-id="a2d66-161">8 hours</span></span> |
| <span data-ttu-id="a2d66-162">Trasferimento impossibile a posizioni atipiche</span><span class="sxs-lookup"><span data-stu-id="a2d66-162">Impossible travel to atypical locations</span></span> |<span data-ttu-id="a2d66-163">5 minuti</span><span class="sxs-lookup"><span data-stu-id="a2d66-163">5 minutes</span></span> |<span data-ttu-id="a2d66-164">1 ora</span><span class="sxs-lookup"><span data-stu-id="a2d66-164">1 hour</span></span> |<span data-ttu-id="a2d66-165">8 ore</span><span class="sxs-lookup"><span data-stu-id="a2d66-165">8 hours</span></span>  |
| <span data-ttu-id="a2d66-166">Accessi da dispositivi infetti</span><span class="sxs-lookup"><span data-stu-id="a2d66-166">Sign-ins from infected devices</span></span> |<span data-ttu-id="a2d66-167">2 ore</span><span class="sxs-lookup"><span data-stu-id="a2d66-167">2 hours</span></span> |<span data-ttu-id="a2d66-168">4 ore</span><span class="sxs-lookup"><span data-stu-id="a2d66-168">4 hours</span></span> |<span data-ttu-id="a2d66-169">8 ore</span><span class="sxs-lookup"><span data-stu-id="a2d66-169">8 hours</span></span>  |
| <span data-ttu-id="a2d66-170">Accessi da indirizzi IP con attività sospette</span><span class="sxs-lookup"><span data-stu-id="a2d66-170">Sign-ins from IP addresses with suspicious activity</span></span> |<span data-ttu-id="a2d66-171">2 ore</span><span class="sxs-lookup"><span data-stu-id="a2d66-171">2 hours</span></span> |<span data-ttu-id="a2d66-172">4 ore</span><span class="sxs-lookup"><span data-stu-id="a2d66-172">4 hours</span></span> |<span data-ttu-id="a2d66-173">8 ore</span><span class="sxs-lookup"><span data-stu-id="a2d66-173">8 hours</span></span>  |



## <a name="next-steps"></a><span data-ttu-id="a2d66-174">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a2d66-174">Next steps</span></span>

<span data-ttu-id="a2d66-175">Se si desidera ottenere maggiori informazioni sui report dell’attività nel portale di Azure, vedere:</span><span class="sxs-lookup"><span data-stu-id="a2d66-175">If you want to know more about the activity reports in the Azure portal, see:</span></span>

- [<span data-ttu-id="a2d66-176">Report delle attività di accesso nel portale di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a2d66-176">Sign-in activity reports in the Azure Active Directory portal</span></span>](active-directory-reporting-activity-sign-ins.md)
- [<span data-ttu-id="a2d66-177">Report delle attività di controllo nel portale di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a2d66-177">Audit activity reports in the Azure Active Directory portal</span></span>](active-directory-reporting-activity-audit-logs.md)

<span data-ttu-id="a2d66-178">Se si desidera ottenere maggiori informazioni sui report della sicurezza nel portale di Azure, vedere:</span><span class="sxs-lookup"><span data-stu-id="a2d66-178">If you want to know more about the security reports in the Azure portal, see:</span></span>

- [<span data-ttu-id="a2d66-179">Report della sicurezza per gli utenti a rischio nel portale di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a2d66-179">Users at risk security report in the Azure Active Directory portal</span></span>](active-directory-reporting-security-user-at-risk.md)
- [<span data-ttu-id="a2d66-180">Report degli accessi a rischio nel portale di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a2d66-180">Risky sign-ins report in the Azure Active Directory portal</span></span>](active-directory-reporting-security-risky-sign-ins.md)

<span data-ttu-id="a2d66-181">Se si desidera ottenere maggiori informazioni sugli eventi di rischio, vedere [Eventi di rischio di Azure Active Directory](active-directory-reporting-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="a2d66-181">If you want to know more about risk events, see [Azure Active Directory risk events](active-directory-reporting-risk-events.md).</span></span>
