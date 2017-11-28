---
title: Autorizzazioni nel Centro sicurezza di Azure | Documentazione Microsoft
description: Questo articolo illustra come Centro sicurezza di Azure usa il controllo degli accessi in base al ruolo per assegnare autorizzazioni agli utenti e identificare le azioni consentite per ogni ruolo.
services: security-center
cloud: na
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
ms.assetid: 
ms.service: security-center
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: terrylan
ms.openlocfilehash: 0aaa99dda44d2020afd3e841e84020eb4ff87a85
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="permissions-in-azure-security-center"></a><span data-ttu-id="8f7d6-103">Autorizzazioni nel Centro sicurezza di Azure</span><span class="sxs-lookup"><span data-stu-id="8f7d6-103">Permissions in Azure Security Center</span></span>

<span data-ttu-id="8f7d6-104">Il Centro sicurezza di Azure usa il [controllo degli accessi in base al ruolo](../active-directory/role-based-access-control-configure.md), con [ruoli predefiniti](../active-directory/role-based-access-built-in-roles.md) che possono essere assegnati a utenti, gruppi e servizi in Azure.</span><span class="sxs-lookup"><span data-stu-id="8f7d6-104">Azure Security Center uses [Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-configure.md), which provides [built-in roles](../active-directory/role-based-access-built-in-roles.md) that can be assigned to users, groups, and services in Azure.</span></span>

<span data-ttu-id="8f7d6-105">Centro sicurezza consente di valutare la configurazione delle risorse per identificare problemi di sicurezza e vulnerabilità.</span><span class="sxs-lookup"><span data-stu-id="8f7d6-105">Security Center assesses the configuration of your resources to identify security issues and vulnerabilities.</span></span> <span data-ttu-id="8f7d6-106">In Centro sicurezza gli utenti possono visualizzare solo informazioni relative a una risorsa quando dispongono del ruolo di proprietario, collaboratore o lettore per la sottoscrizione o il gruppo di risorse cui tali risorse appartengono.</span><span class="sxs-lookup"><span data-stu-id="8f7d6-106">In Security Center, you only see information related to a resource when you are assigned the role of Owner, Contributor, or Reader for the subscription or resource group that a resource belongs to.</span></span>

<span data-ttu-id="8f7d6-107">Oltre a questi ruoli, esistono due ruoli specifici del Centro sicurezza:</span><span class="sxs-lookup"><span data-stu-id="8f7d6-107">In addition to these roles, there are two specific Security Center roles:</span></span>

* <span data-ttu-id="8f7d6-108">**Ruolo con autorizzazioni di lettura per la sicurezza**: un utente che appartiene a questo ruolo dispone dei diritti di visualizzazione nel Centro sicurezza.</span><span class="sxs-lookup"><span data-stu-id="8f7d6-108">**Security Reader**: A user that belongs to this role has viewing rights to Security Center.</span></span> <span data-ttu-id="8f7d6-109">L'utente può visualizzare raccomandazioni, avvisi, criteri di sicurezza e stati di sicurezza, ma non può apportare modifiche.</span><span class="sxs-lookup"><span data-stu-id="8f7d6-109">The user can view recommendations, alerts, a security policy, and security states, but cannot make changes.</span></span>
* <span data-ttu-id="8f7d6-110">**Amministratore della protezione**: un utente che appartiene a questo ruolo ha gli stessi diritti del Ruolo con autorizzazioni di lettura per la sicurezza e può anche aggiornare i criteri di sicurezza e rimuovere gli avvisi e le raccomandazioni.</span><span class="sxs-lookup"><span data-stu-id="8f7d6-110">**Security Administrator**: A user that belongs to this role has the same rights as the Security Reader and can also update the security policy and dismiss alerts and recommendations.</span></span>

> [!NOTE]
> <span data-ttu-id="8f7d6-111">I ruoli di sicurezza, Ruolo con autorizzazioni di lettura per la sicurezza e Amministratore della protezione, hanno accesso solo al Centro sicurezza.</span><span class="sxs-lookup"><span data-stu-id="8f7d6-111">The security roles, Security Reader and Security Administrator, have access only in Security Center.</span></span> <span data-ttu-id="8f7d6-112">I ruoli di sicurezza non hanno accesso ad altre aree del servizio di Azure come Archiviazione, Web e dispositivi mobili o Internet delle cose.</span><span class="sxs-lookup"><span data-stu-id="8f7d6-112">The security roles do not have access to other service areas of Azure such as Storage, Web & Mobile, or Internet of Things.</span></span>
>
>

## <a name="roles-and-allowed-actions"></a><span data-ttu-id="8f7d6-113">Ruoli e azioni consentite</span><span class="sxs-lookup"><span data-stu-id="8f7d6-113">Roles and allowed actions</span></span>

<span data-ttu-id="8f7d6-114">La tabella seguente contiene i ruoli e le azioni consentite in Centro sicurezza.</span><span class="sxs-lookup"><span data-stu-id="8f7d6-114">The following table displays roles and allowed actions in Security Center.</span></span> <span data-ttu-id="8f7d6-115">Un simbolo X indica che l'azione è consentita per il ruolo.</span><span class="sxs-lookup"><span data-stu-id="8f7d6-115">An X indicates that the action is allowed for that role.</span></span>

| <span data-ttu-id="8f7d6-116">Ruolo</span><span class="sxs-lookup"><span data-stu-id="8f7d6-116">Role</span></span> | <span data-ttu-id="8f7d6-117">Modificare i criteri di sicurezza</span><span class="sxs-lookup"><span data-stu-id="8f7d6-117">Edit security policy</span></span> | <span data-ttu-id="8f7d6-118">Applicare i suggerimenti per la sicurezza per una risorsa</span><span class="sxs-lookup"><span data-stu-id="8f7d6-118">Apply security recommendations for a resource</span></span> | <span data-ttu-id="8f7d6-119">Ignorare gli avvisi e le raccomandazioni</span><span class="sxs-lookup"><span data-stu-id="8f7d6-119">Dismiss alerts and recommendations</span></span> | <span data-ttu-id="8f7d6-120">Visualizzare gli avvisi e le raccomandazioni</span><span class="sxs-lookup"><span data-stu-id="8f7d6-120">View alerts and recommendations</span></span> |
|:--- |:---:|:---:|:---:|:---:|
| <span data-ttu-id="8f7d6-121">Proprietario della sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="8f7d6-121">Subscription Owner</span></span> | <span data-ttu-id="8f7d6-122">X</span><span class="sxs-lookup"><span data-stu-id="8f7d6-122">X</span></span> | <span data-ttu-id="8f7d6-123">X</span><span class="sxs-lookup"><span data-stu-id="8f7d6-123">X</span></span> | <span data-ttu-id="8f7d6-124">X</span><span class="sxs-lookup"><span data-stu-id="8f7d6-124">X</span></span> | <span data-ttu-id="8f7d6-125">X</span><span class="sxs-lookup"><span data-stu-id="8f7d6-125">X</span></span> |
| <span data-ttu-id="8f7d6-126">Collaboratore alla sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="8f7d6-126">Subscription Contributor</span></span> | <span data-ttu-id="8f7d6-127">X</span><span class="sxs-lookup"><span data-stu-id="8f7d6-127">X</span></span> | <span data-ttu-id="8f7d6-128">X</span><span class="sxs-lookup"><span data-stu-id="8f7d6-128">X</span></span> | <span data-ttu-id="8f7d6-129">X</span><span class="sxs-lookup"><span data-stu-id="8f7d6-129">X</span></span> | <span data-ttu-id="8f7d6-130">X</span><span class="sxs-lookup"><span data-stu-id="8f7d6-130">X</span></span> |
| <span data-ttu-id="8f7d6-131">Proprietario del gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="8f7d6-131">Resource Group Owner</span></span> | -- | <span data-ttu-id="8f7d6-132">X</span><span class="sxs-lookup"><span data-stu-id="8f7d6-132">X</span></span> | -- | <span data-ttu-id="8f7d6-133">X</span><span class="sxs-lookup"><span data-stu-id="8f7d6-133">X</span></span> |
| <span data-ttu-id="8f7d6-134">Collaboratore del gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="8f7d6-134">Resource Group Contributor</span></span> | -- | <span data-ttu-id="8f7d6-135">X</span><span class="sxs-lookup"><span data-stu-id="8f7d6-135">X</span></span> | -- | <span data-ttu-id="8f7d6-136">X</span><span class="sxs-lookup"><span data-stu-id="8f7d6-136">X</span></span> |
| <span data-ttu-id="8f7d6-137">Lettore</span><span class="sxs-lookup"><span data-stu-id="8f7d6-137">Reader</span></span> | -- | -- | -- | <span data-ttu-id="8f7d6-138">X</span><span class="sxs-lookup"><span data-stu-id="8f7d6-138">X</span></span> |
| <span data-ttu-id="8f7d6-139">Amministratore della sicurezza</span><span class="sxs-lookup"><span data-stu-id="8f7d6-139">Security Administrator</span></span> | <span data-ttu-id="8f7d6-140">X</span><span class="sxs-lookup"><span data-stu-id="8f7d6-140">X</span></span> | -- | <span data-ttu-id="8f7d6-141">X</span><span class="sxs-lookup"><span data-stu-id="8f7d6-141">X</span></span> | <span data-ttu-id="8f7d6-142">X</span><span class="sxs-lookup"><span data-stu-id="8f7d6-142">X</span></span> |
| <span data-ttu-id="8f7d6-143">Ruolo con autorizzazioni di lettura per la sicurezza</span><span class="sxs-lookup"><span data-stu-id="8f7d6-143">Security Reader</span></span> | -- | -- | -- | <span data-ttu-id="8f7d6-144">X</span><span class="sxs-lookup"><span data-stu-id="8f7d6-144">X</span></span> |

> [!NOTE]
> <span data-ttu-id="8f7d6-145">È consigliabile assegnare il ruolo con il minor numero di autorizzazioni che permetta agli utenti di completare le attività.</span><span class="sxs-lookup"><span data-stu-id="8f7d6-145">We recommend that you assign the least permissive role needed for users to complete their tasks.</span></span> <span data-ttu-id="8f7d6-146">Assegnare ad esempio il ruolo di lettore agli utenti che devono visualizzare solo le informazioni sull'integrità della sicurezza di una risorsa, ma non eseguono alcuna azione, come l'applicazione di consigli e la modifica di criteri.</span><span class="sxs-lookup"><span data-stu-id="8f7d6-146">For example, assign the Reader role to users who only need to view information about the security health of a resource but not take action, such as applying recommendations or editing policies.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="8f7d6-147">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8f7d6-147">Next steps</span></span>
<span data-ttu-id="8f7d6-148">In questo articolo è stato descritto come Centro sicurezza usa PC usa il controllo degli accessi in base al ruolo per assegnare autorizzazioni agli utenti e sono state identificate le azioni consentite per ogni ruolo.</span><span class="sxs-lookup"><span data-stu-id="8f7d6-148">This article explained how Security Center uses RBAC to assign permissions to users and identified the allowed actions for each role.</span></span> <span data-ttu-id="8f7d6-149">Ora che è stata acquisita familiarità con le assegnazioni di ruolo necessari per monitorare lo stato di sicurezza della sottoscrizione, modificare i criteri di sicurezza e applicare i consigli, si apprenderà come eseguire queste operazioni:</span><span class="sxs-lookup"><span data-stu-id="8f7d6-149">Now that you're familiar with the role assignments needed to monitor the security state of your subscription, edit security policies, and apply recommendations, learn how to:</span></span>

- [<span data-ttu-id="8f7d6-150">Impostare criteri di sicurezza in Centro sicurezza</span><span class="sxs-lookup"><span data-stu-id="8f7d6-150">Set security policies in Security Center</span></span>](security-center-policies.md)
- [<span data-ttu-id="8f7d6-151">Gestire i suggerimenti per la sicurezza in Centro sicurezza</span><span class="sxs-lookup"><span data-stu-id="8f7d6-151">Manage security recommendations in Security Center</span></span>](security-center-recommendations.md)
- [<span data-ttu-id="8f7d6-152">Monitorare l'integrità della sicurezza delle risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="8f7d6-152">Monitor the security health of your Azure resources</span></span>](security-center-monitoring.md)
- [<span data-ttu-id="8f7d6-153">Gestire e rispondere agli avvisi di sicurezza in Centro sicurezza</span><span class="sxs-lookup"><span data-stu-id="8f7d6-153">Manage and respond to security alerts in Security Center</span></span>](security-center-managing-and-responding-alerts.md)
- [<span data-ttu-id="8f7d6-154">Monitorare le soluzioni di sicurezza dei partner</span><span class="sxs-lookup"><span data-stu-id="8f7d6-154">Monitor partner security solutions</span></span>](security-center-partner-solutions.md)
