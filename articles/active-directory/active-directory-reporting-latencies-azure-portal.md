---
title: le latenze reporting di Active Directory aaaAzure | Documenti Microsoft
description: "Informazioni sulle quantità hello di tempo impiegato per la segnalazione di eventi tooshow backup nel portale di Azure"
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
ms.openlocfilehash: eee959331262ba59b313dd038cb54699dbef48a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-reporting-latencies"></a><span data-ttu-id="87261-103">Latenze dei report di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="87261-103">Azure Active Directory reporting latencies</span></span>

<span data-ttu-id="87261-104">Con [reporting](active-directory-preview-explainer.md) in hello Azure Active Directory, si ottengono tutte le informazioni di hello è necessario toodetermine, svolgimento dell'ambiente.</span><span class="sxs-lookup"><span data-stu-id="87261-104">With [reporting](active-directory-preview-explainer.md) in hello Azure Active Directory, you get all hello information you need toodetermine how your environment is doing.</span></span> <span data-ttu-id="87261-105">quantità di Hello di tempo impiegato per la segnalazione dei dati tooshow backup nel portale di Azure hello è noto anche come latenza.</span><span class="sxs-lookup"><span data-stu-id="87261-105">hello amount of time it takes for reporting data tooshow up in hello Azure portal is also known as latency.</span></span> 

<span data-ttu-id="87261-106">Questo argomento elenca le informazioni sulla latenza hello per hello tutte le categorie di report nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="87261-106">This topic lists hello latency information for hello all reporting categories in hello Azure portal.</span></span> 


## <a name="activity-reports"></a><span data-ttu-id="87261-107">Report sull’attività</span><span class="sxs-lookup"><span data-stu-id="87261-107">Activity reports</span></span>

<span data-ttu-id="87261-108">Esistono due aree di reporting sulle attività:</span><span class="sxs-lookup"><span data-stu-id="87261-108">There are two areas of activity reporting:</span></span>

- <span data-ttu-id="87261-109">**Le attività di accesso** – informazioni sull'utilizzo di hello di applicazioni gestite e le attività di accesso dell'utente</span><span class="sxs-lookup"><span data-stu-id="87261-109">**Sign-in activities** – Information about hello usage of managed applications and user sign-in activities</span></span>
- <span data-ttu-id="87261-110">**Log di controllo** : informazioni relative alle attività di sistema sulla gestione di utenti e gruppi, sulle applicazioni gestite e sulle attività di directory</span><span class="sxs-lookup"><span data-stu-id="87261-110">**Audit logs** - System activity information about users and group management, your managed applications and directory activities</span></span>

<span data-ttu-id="87261-111">Hello nella tabella seguente elenca le informazioni sulla latenza hello per i report di attività.</span><span class="sxs-lookup"><span data-stu-id="87261-111">hello following table lists hello latency information for activity reports.</span></span>

| <span data-ttu-id="87261-112">Report</span><span class="sxs-lookup"><span data-stu-id="87261-112">Report</span></span> | <span data-ttu-id="87261-113">Minima</span><span class="sxs-lookup"><span data-stu-id="87261-113">Minimum</span></span> | <span data-ttu-id="87261-114">Media</span><span class="sxs-lookup"><span data-stu-id="87261-114">Average</span></span> | <span data-ttu-id="87261-115">Massima</span><span class="sxs-lookup"><span data-stu-id="87261-115">Maximum</span></span> |
| :-- | --- | --- | --- |
| <span data-ttu-id="87261-116">Log di controllo</span><span class="sxs-lookup"><span data-stu-id="87261-116">Audit logs</span></span>             | <span data-ttu-id="87261-117">30 minuti</span><span class="sxs-lookup"><span data-stu-id="87261-117">30 minutes</span></span>  | <span data-ttu-id="87261-118">45 minuti</span><span class="sxs-lookup"><span data-stu-id="87261-118">45 Minutes</span></span> | <span data-ttu-id="87261-119">1 ora</span><span class="sxs-lookup"><span data-stu-id="87261-119">1 hour</span></span>     |
| <span data-ttu-id="87261-120">Accessi</span><span class="sxs-lookup"><span data-stu-id="87261-120">Sign-ins</span></span>               | <span data-ttu-id="87261-121">15 minuti</span><span class="sxs-lookup"><span data-stu-id="87261-121">15 minutes</span></span>  | <span data-ttu-id="87261-122">15 minuti</span><span class="sxs-lookup"><span data-stu-id="87261-122">15 minutes</span></span> | <span data-ttu-id="87261-123">2 ore*</span><span class="sxs-lookup"><span data-stu-id="87261-123">2 hours*</span></span>   |

>[!NOTE]
> <span data-ttu-id="87261-124">Per alcuni dati di attività accessi provenienti da applicazioni di office legacy, può richiedere ore too8 hello reporting dati tooshow backup.</span><span class="sxs-lookup"><span data-stu-id="87261-124">For some sign-ins activity data coming from legacy office applications, it can take too8 hours for hello reporting data tooshow up.</span></span> 


## <a name="security-reports"></a><span data-ttu-id="87261-125">Report sulla sicurezza</span><span class="sxs-lookup"><span data-stu-id="87261-125">Security reports</span></span>

<span data-ttu-id="87261-126">Esistono due aree di reporting sulla sicurezza:</span><span class="sxs-lookup"><span data-stu-id="87261-126">There are two areas of security reporting:</span></span>

- <span data-ttu-id="87261-127">**Accessi rischiosi** -un rischiosa l'accesso è un indicatore per un tentativo di accesso che siano stato eseguito da un utente che non è proprietario di legittimo hello di un account utente.</span><span class="sxs-lookup"><span data-stu-id="87261-127">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not hello legitimate owner of a user account.</span></span> 
- <span data-ttu-id="87261-128">**Utenti contrassegnati per il rischio**. Un utente rischioso è indicativo di un account utente che potrebbe essere stato compromesso.</span><span class="sxs-lookup"><span data-stu-id="87261-128">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> 

<span data-ttu-id="87261-129">Hello nella tabella seguente elenca le informazioni sulla latenza hello per i report di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="87261-129">hello following table lists hello latency information for security reports.</span></span>

| <span data-ttu-id="87261-130">Report</span><span class="sxs-lookup"><span data-stu-id="87261-130">Report</span></span> | <span data-ttu-id="87261-131">Minima</span><span class="sxs-lookup"><span data-stu-id="87261-131">Minimum</span></span> | <span data-ttu-id="87261-132">Media</span><span class="sxs-lookup"><span data-stu-id="87261-132">Average</span></span> | <span data-ttu-id="87261-133">Massima</span><span class="sxs-lookup"><span data-stu-id="87261-133">Maximum</span></span> |
| :-- | --- | --- | --- |
| <span data-ttu-id="87261-134">Utenti a rischio.</span><span class="sxs-lookup"><span data-stu-id="87261-134">Users at risk</span></span>          | <span data-ttu-id="87261-135">5 minuti</span><span class="sxs-lookup"><span data-stu-id="87261-135">5 minutes</span></span>   | <span data-ttu-id="87261-136">15 minuti</span><span class="sxs-lookup"><span data-stu-id="87261-136">15 minutes</span></span>  | <span data-ttu-id="87261-137">2 ore</span><span class="sxs-lookup"><span data-stu-id="87261-137">2 hours</span></span>  |
| <span data-ttu-id="87261-138">Accessi a rischio</span><span class="sxs-lookup"><span data-stu-id="87261-138">Risky sign-ins</span></span>         | <span data-ttu-id="87261-139">5 minuti</span><span class="sxs-lookup"><span data-stu-id="87261-139">5 minutes</span></span>   | <span data-ttu-id="87261-140">15 minuti</span><span class="sxs-lookup"><span data-stu-id="87261-140">15 minutes</span></span>  | <span data-ttu-id="87261-141">2 ore</span><span class="sxs-lookup"><span data-stu-id="87261-141">2 hours</span></span>  |

## <a name="risk-events"></a><span data-ttu-id="87261-142">Eventi di rischio</span><span class="sxs-lookup"><span data-stu-id="87261-142">Risk events</span></span>

<span data-ttu-id="87261-143">Azure Active Directory Usa adattivo di machine learning algoritmi euristica toodetect sospette azioni e che sono account utente tooyour correlati.</span><span class="sxs-lookup"><span data-stu-id="87261-143">Azure Active Directory uses adaptive machine learning algorithms and heuristics toodetect suspicious actions that are related tooyour user accounts.</span></span> <span data-ttu-id="87261-144">Ogni azione sospetta rilevata viene archiviata in un record denominato evento di rischio.</span><span class="sxs-lookup"><span data-stu-id="87261-144">Each detected suspicious action is stored in a record called risk event.</span></span>

<span data-ttu-id="87261-145">Hello nella tabella seguente elenca le informazioni di latenza hello per gli eventi di rischio.</span><span class="sxs-lookup"><span data-stu-id="87261-145">hello following table lists hello latency information for risk events.</span></span>

| <span data-ttu-id="87261-146">Report</span><span class="sxs-lookup"><span data-stu-id="87261-146">Report</span></span> | <span data-ttu-id="87261-147">Minima</span><span class="sxs-lookup"><span data-stu-id="87261-147">Minimum</span></span> | <span data-ttu-id="87261-148">Media</span><span class="sxs-lookup"><span data-stu-id="87261-148">Average</span></span> | <span data-ttu-id="87261-149">Massima</span><span class="sxs-lookup"><span data-stu-id="87261-149">Maximum</span></span> |
| :-- | --- | --- | --- |
| <span data-ttu-id="87261-150">Accessi da indirizzi IP anonimi</span><span class="sxs-lookup"><span data-stu-id="87261-150">Sign-ins from anonymous IP addresses</span></span> |<span data-ttu-id="87261-151">5 minuti</span><span class="sxs-lookup"><span data-stu-id="87261-151">5 minutes</span></span> |<span data-ttu-id="87261-152">15 minuti</span><span class="sxs-lookup"><span data-stu-id="87261-152">15 Minutes</span></span> |<span data-ttu-id="87261-153">2 ore</span><span class="sxs-lookup"><span data-stu-id="87261-153">2 hours</span></span> |
| <span data-ttu-id="87261-154">Accessi da posizioni non note</span><span class="sxs-lookup"><span data-stu-id="87261-154">Sign-ins from unfamiliar locations</span></span> |<span data-ttu-id="87261-155">5 minuti</span><span class="sxs-lookup"><span data-stu-id="87261-155">5 minutes</span></span> |<span data-ttu-id="87261-156">15 minuti</span><span class="sxs-lookup"><span data-stu-id="87261-156">15 Minutes</span></span> |<span data-ttu-id="87261-157">2 ore</span><span class="sxs-lookup"><span data-stu-id="87261-157">2 hours</span></span> |
| <span data-ttu-id="87261-158">Utenti con credenziali perse</span><span class="sxs-lookup"><span data-stu-id="87261-158">Users with leaked credentials</span></span> |<span data-ttu-id="87261-159">2 ore</span><span class="sxs-lookup"><span data-stu-id="87261-159">2 hours</span></span> |<span data-ttu-id="87261-160">4 ore</span><span class="sxs-lookup"><span data-stu-id="87261-160">4 hours</span></span> |<span data-ttu-id="87261-161">8 ore</span><span class="sxs-lookup"><span data-stu-id="87261-161">8 hours</span></span> |
| <span data-ttu-id="87261-162">Comunicazione Impossibile tooatypical percorsi</span><span class="sxs-lookup"><span data-stu-id="87261-162">Impossible travel tooatypical locations</span></span> |<span data-ttu-id="87261-163">5 minuti</span><span class="sxs-lookup"><span data-stu-id="87261-163">5 minutes</span></span> |<span data-ttu-id="87261-164">1 ora</span><span class="sxs-lookup"><span data-stu-id="87261-164">1 hour</span></span> |<span data-ttu-id="87261-165">8 ore</span><span class="sxs-lookup"><span data-stu-id="87261-165">8 hours</span></span>  |
| <span data-ttu-id="87261-166">Accessi da dispositivi infetti</span><span class="sxs-lookup"><span data-stu-id="87261-166">Sign-ins from infected devices</span></span> |<span data-ttu-id="87261-167">2 ore</span><span class="sxs-lookup"><span data-stu-id="87261-167">2 hours</span></span> |<span data-ttu-id="87261-168">4 ore</span><span class="sxs-lookup"><span data-stu-id="87261-168">4 hours</span></span> |<span data-ttu-id="87261-169">8 ore</span><span class="sxs-lookup"><span data-stu-id="87261-169">8 hours</span></span>  |
| <span data-ttu-id="87261-170">Accessi da indirizzi IP con attività sospette</span><span class="sxs-lookup"><span data-stu-id="87261-170">Sign-ins from IP addresses with suspicious activity</span></span> |<span data-ttu-id="87261-171">2 ore</span><span class="sxs-lookup"><span data-stu-id="87261-171">2 hours</span></span> |<span data-ttu-id="87261-172">4 ore</span><span class="sxs-lookup"><span data-stu-id="87261-172">4 hours</span></span> |<span data-ttu-id="87261-173">8 ore</span><span class="sxs-lookup"><span data-stu-id="87261-173">8 hours</span></span>  |



## <a name="next-steps"></a><span data-ttu-id="87261-174">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="87261-174">Next steps</span></span>

<span data-ttu-id="87261-175">Se si desidera tooknow ulteriori informazioni sui report di attività hello in hello portale di Azure, vedere:</span><span class="sxs-lookup"><span data-stu-id="87261-175">If you want tooknow more about hello activity reports in hello Azure portal, see:</span></span>

- [<span data-ttu-id="87261-176">Report attività di accesso nel portale di Azure Active Directory hello</span><span class="sxs-lookup"><span data-stu-id="87261-176">Sign-in activity reports in hello Azure Active Directory portal</span></span>](active-directory-reporting-activity-sign-ins.md)
- [<span data-ttu-id="87261-177">Report attività nel portale di Azure Active Directory hello di controllo</span><span class="sxs-lookup"><span data-stu-id="87261-177">Audit activity reports in hello Azure Active Directory portal</span></span>](active-directory-reporting-activity-audit-logs.md)

<span data-ttu-id="87261-178">Se si desidera tooknow ulteriori informazioni sui report di sicurezza hello in hello portale di Azure, vedere:</span><span class="sxs-lookup"><span data-stu-id="87261-178">If you want tooknow more about hello security reports in hello Azure portal, see:</span></span>

- [<span data-ttu-id="87261-179">Utenti dei report di rischio per la sicurezza nel portale di Azure Active Directory hello</span><span class="sxs-lookup"><span data-stu-id="87261-179">Users at risk security report in hello Azure Active Directory portal</span></span>](active-directory-reporting-security-user-at-risk.md)
- [<span data-ttu-id="87261-180">Report accessi rischiosa nel portale di Azure Active Directory hello</span><span class="sxs-lookup"><span data-stu-id="87261-180">Risky sign-ins report in hello Azure Active Directory portal</span></span>](active-directory-reporting-security-risky-sign-ins.md)

<span data-ttu-id="87261-181">Se si desidera tooknow ulteriori sugli eventi di rischio, vedere [gli eventi di rischio di Azure Active Directory](active-directory-reporting-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="87261-181">If you want tooknow more about risk events, see [Azure Active Directory risk events](active-directory-reporting-risk-events.md).</span></span>
