---
title: aaaPermissions nel Centro protezione di Azure | Documenti Microsoft
description: In questo articolo illustra come Centro sicurezza di Azure viene usato toousers autorizzazioni tooassign controllo di accesso basato sui ruoli e identifica le azioni per ogni ruolo consentita hello.
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
ms.openlocfilehash: 03e16132dc3d951ef8ad9e86b9970b9e4d15c76b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="permissions-in-azure-security-center"></a><span data-ttu-id="8850a-103">Autorizzazioni nel Centro sicurezza di Azure</span><span class="sxs-lookup"><span data-stu-id="8850a-103">Permissions in Azure Security Center</span></span>

<span data-ttu-id="8850a-104">Centro sicurezza di Azure Usa [controllo di accesso basato sui ruoli (RBAC)](../active-directory/role-based-access-control-configure.md), che fornisce [ruoli predefiniti](../active-directory/role-based-access-built-in-roles.md) che può essere assegnato toousers, gruppi e i servizi in Azure.</span><span class="sxs-lookup"><span data-stu-id="8850a-104">Azure Security Center uses [Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-configure.md), which provides [built-in roles](../active-directory/role-based-access-built-in-roles.md) that can be assigned toousers, groups, and services in Azure.</span></span>

<span data-ttu-id="8850a-105">Centro sicurezza PC valuta configurazione hello di problemi di sicurezza di risorse tooidentify e vulnerabilità.</span><span class="sxs-lookup"><span data-stu-id="8850a-105">Security Center assesses hello configuration of your resources tooidentify security issues and vulnerabilities.</span></span> <span data-ttu-id="8850a-106">Centro sicurezza PC, visualizzare solo le informazioni correlate tooa risorse quando l'utente viene assegnato hello ruolo di proprietario, collaboratore o lettore per il gruppo hello sottoscrizione o la risorsa a cui appartiene una risorsa.</span><span class="sxs-lookup"><span data-stu-id="8850a-106">In Security Center, you only see information related tooa resource when you are assigned hello role of Owner, Contributor, or Reader for hello subscription or resource group that a resource belongs to.</span></span>

<span data-ttu-id="8850a-107">Nei ruoli toothese aggiunta, sono disponibili due ruoli specifici del Centro sicurezza:</span><span class="sxs-lookup"><span data-stu-id="8850a-107">In addition toothese roles, there are two specific Security Center roles:</span></span>

* <span data-ttu-id="8850a-108">**Lettore di sicurezza**: un utente appartenente al ruolo toothis dispone di diritti tooSecurity centro di visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="8850a-108">**Security Reader**: A user that belongs toothis role has viewing rights tooSecurity Center.</span></span> <span data-ttu-id="8850a-109">utente Hello può visualizzare consigli, avvisi, un criterio di sicurezza e gli stati di sicurezza, ma non è possibile apportare modifiche.</span><span class="sxs-lookup"><span data-stu-id="8850a-109">hello user can view recommendations, alerts, a security policy, and security states, but cannot make changes.</span></span>
* <span data-ttu-id="8850a-110">**Amministratore della sicurezza**: un utente appartenente al ruolo toothis hello stessi diritti come lettore sicurezza hello e può anche aggiornare criteri di sicurezza hello e chiudere gli avvisi e i consigli.</span><span class="sxs-lookup"><span data-stu-id="8850a-110">**Security Administrator**: A user that belongs toothis role has hello same rights as hello Security Reader and can also update hello security policy and dismiss alerts and recommendations.</span></span>

> [!NOTE]
> <span data-ttu-id="8850a-111">ruoli di sicurezza Hello, lettore di sicurezza e l'amministratore della sicurezza, hanno accesso solo in Centro sicurezza PC.</span><span class="sxs-lookup"><span data-stu-id="8850a-111">hello security roles, Security Reader and Security Administrator, have access only in Security Center.</span></span> <span data-ttu-id="8850a-112">ruoli di sicurezza Hello non dispone di accesso tooother servizio aree di Azure, ad esempio l'archiviazione, Web e dispositivi mobili o Internet delle cose.</span><span class="sxs-lookup"><span data-stu-id="8850a-112">hello security roles do not have access tooother service areas of Azure such as Storage, Web & Mobile, or Internet of Things.</span></span>
>
>

## <a name="roles-and-allowed-actions"></a><span data-ttu-id="8850a-113">Ruoli e azioni consentite</span><span class="sxs-lookup"><span data-stu-id="8850a-113">Roles and allowed actions</span></span>

<span data-ttu-id="8850a-114">Hello nella tabella seguente vengono visualizzati i ruoli e le azioni consentite in Centro sicurezza PC.</span><span class="sxs-lookup"><span data-stu-id="8850a-114">hello following table displays roles and allowed actions in Security Center.</span></span> <span data-ttu-id="8850a-115">Una X indica che l'azione hello è consentita per tale ruolo.</span><span class="sxs-lookup"><span data-stu-id="8850a-115">An X indicates that hello action is allowed for that role.</span></span>

| <span data-ttu-id="8850a-116">Ruolo</span><span class="sxs-lookup"><span data-stu-id="8850a-116">Role</span></span> | <span data-ttu-id="8850a-117">Modificare i criteri di sicurezza</span><span class="sxs-lookup"><span data-stu-id="8850a-117">Edit security policy</span></span> | <span data-ttu-id="8850a-118">Applicare i suggerimenti per la sicurezza per una risorsa</span><span class="sxs-lookup"><span data-stu-id="8850a-118">Apply security recommendations for a resource</span></span> | <span data-ttu-id="8850a-119">Ignorare gli avvisi e le raccomandazioni</span><span class="sxs-lookup"><span data-stu-id="8850a-119">Dismiss alerts and recommendations</span></span> | <span data-ttu-id="8850a-120">Visualizzare gli avvisi e le raccomandazioni</span><span class="sxs-lookup"><span data-stu-id="8850a-120">View alerts and recommendations</span></span> |
|:--- |:---:|:---:|:---:|:---:|
| <span data-ttu-id="8850a-121">Proprietario della sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="8850a-121">Subscription Owner</span></span> | <span data-ttu-id="8850a-122">X</span><span class="sxs-lookup"><span data-stu-id="8850a-122">X</span></span> | <span data-ttu-id="8850a-123">X</span><span class="sxs-lookup"><span data-stu-id="8850a-123">X</span></span> | <span data-ttu-id="8850a-124">X</span><span class="sxs-lookup"><span data-stu-id="8850a-124">X</span></span> | <span data-ttu-id="8850a-125">X</span><span class="sxs-lookup"><span data-stu-id="8850a-125">X</span></span> |
| <span data-ttu-id="8850a-126">Collaboratore alla sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="8850a-126">Subscription Contributor</span></span> | <span data-ttu-id="8850a-127">X</span><span class="sxs-lookup"><span data-stu-id="8850a-127">X</span></span> | <span data-ttu-id="8850a-128">X</span><span class="sxs-lookup"><span data-stu-id="8850a-128">X</span></span> | <span data-ttu-id="8850a-129">X</span><span class="sxs-lookup"><span data-stu-id="8850a-129">X</span></span> | <span data-ttu-id="8850a-130">X</span><span class="sxs-lookup"><span data-stu-id="8850a-130">X</span></span> |
| <span data-ttu-id="8850a-131">Proprietario del gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="8850a-131">Resource Group Owner</span></span> | -- | <span data-ttu-id="8850a-132">X</span><span class="sxs-lookup"><span data-stu-id="8850a-132">X</span></span> | -- | <span data-ttu-id="8850a-133">X</span><span class="sxs-lookup"><span data-stu-id="8850a-133">X</span></span> |
| <span data-ttu-id="8850a-134">Collaboratore del gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="8850a-134">Resource Group Contributor</span></span> | -- | <span data-ttu-id="8850a-135">X</span><span class="sxs-lookup"><span data-stu-id="8850a-135">X</span></span> | -- | <span data-ttu-id="8850a-136">X</span><span class="sxs-lookup"><span data-stu-id="8850a-136">X</span></span> |
| <span data-ttu-id="8850a-137">Lettore</span><span class="sxs-lookup"><span data-stu-id="8850a-137">Reader</span></span> | -- | -- | -- | <span data-ttu-id="8850a-138">X</span><span class="sxs-lookup"><span data-stu-id="8850a-138">X</span></span> |
| <span data-ttu-id="8850a-139">Amministratore della sicurezza</span><span class="sxs-lookup"><span data-stu-id="8850a-139">Security Administrator</span></span> | <span data-ttu-id="8850a-140">X</span><span class="sxs-lookup"><span data-stu-id="8850a-140">X</span></span> | -- | <span data-ttu-id="8850a-141">X</span><span class="sxs-lookup"><span data-stu-id="8850a-141">X</span></span> | <span data-ttu-id="8850a-142">X</span><span class="sxs-lookup"><span data-stu-id="8850a-142">X</span></span> |
| <span data-ttu-id="8850a-143">Ruolo con autorizzazioni di lettura per la sicurezza</span><span class="sxs-lookup"><span data-stu-id="8850a-143">Security Reader</span></span> | -- | -- | -- | <span data-ttu-id="8850a-144">X</span><span class="sxs-lookup"><span data-stu-id="8850a-144">X</span></span> |

> [!NOTE]
> <span data-ttu-id="8850a-145">È consigliabile assegnare hello restrittivo ruolo necessari per utenti toocomplete le proprie attività.</span><span class="sxs-lookup"><span data-stu-id="8850a-145">We recommend that you assign hello least permissive role needed for users toocomplete their tasks.</span></span> <span data-ttu-id="8850a-146">Ad esempio, assegnare hello lettore ruolo toousers che sufficiente tooview informazioni sullo stato di sicurezza hello di una risorsa ma non eseguire l'azione, ad esempio l'applicazione delle indicazioni o la modifica di criteri.</span><span class="sxs-lookup"><span data-stu-id="8850a-146">For example, assign hello Reader role toousers who only need tooview information about hello security health of a resource but not take action, such as applying recommendations or editing policies.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="8850a-147">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8850a-147">Next steps</span></span>
<span data-ttu-id="8850a-148">Questo articolo è illustrato l'utilizzo di Centro sicurezza PC RBAC tooassign autorizzazioni toousers e identificato hello azioni per ogni ruolo è consentito.</span><span class="sxs-lookup"><span data-stu-id="8850a-148">This article explained how Security Center uses RBAC tooassign permissions toousers and identified hello allowed actions for each role.</span></span> <span data-ttu-id="8850a-149">Ora che si ha familiarità con le assegnazioni di ruolo hello necessari toomonitor hello lo stato di sicurezza della sottoscrizione, modificare i criteri di sicurezza e applica indicazioni, informazioni su come:</span><span class="sxs-lookup"><span data-stu-id="8850a-149">Now that you're familiar with hello role assignments needed toomonitor hello security state of your subscription, edit security policies, and apply recommendations, learn how to:</span></span>

- [<span data-ttu-id="8850a-150">Impostare criteri di sicurezza in Centro sicurezza</span><span class="sxs-lookup"><span data-stu-id="8850a-150">Set security policies in Security Center</span></span>](security-center-policies.md)
- [<span data-ttu-id="8850a-151">Gestire i suggerimenti per la sicurezza in Centro sicurezza</span><span class="sxs-lookup"><span data-stu-id="8850a-151">Manage security recommendations in Security Center</span></span>](security-center-recommendations.md)
- [<span data-ttu-id="8850a-152">Monitorare l'integrità della protezione hello delle risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="8850a-152">Monitor hello security health of your Azure resources</span></span>](security-center-monitoring.md)
- [<span data-ttu-id="8850a-153">Gestire e rispondere toosecurity avvisi del Centro sicurezza PC</span><span class="sxs-lookup"><span data-stu-id="8850a-153">Manage and respond toosecurity alerts in Security Center</span></span>](security-center-managing-and-responding-alerts.md)
- [<span data-ttu-id="8850a-154">Monitorare le soluzioni di sicurezza dei partner</span><span class="sxs-lookup"><span data-stu-id="8850a-154">Monitor partner security solutions</span></span>](security-center-partner-solutions.md)
