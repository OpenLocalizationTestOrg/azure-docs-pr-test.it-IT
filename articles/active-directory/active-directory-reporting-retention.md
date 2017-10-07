---
title: criteri di conservazione dei report di Active Directory aaaAzure | Documenti Microsoft
description: Criteri di conservazione dei dati di report in Azure Active Directory
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 183e53b0-0647-42e7-8abe-3e9ff424de12
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/05/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: c46a68198cb34e9c92662b2f8461010745392c04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-report-retention-policies"></a><span data-ttu-id="99fd5-103">Criteri di conservazione dei report di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="99fd5-103">Azure Active Directory report retention policies</span></span>


<span data-ttu-id="99fd5-104">In questo argomento fornisce le risposte alle domande più comuni di toohello in combinazione con la conservazione dei dati hello per i report di attività differenti hello in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="99fd5-104">This topic provides you with answers toohello most common questions in conjunction with hello data retention for hello different activity reports in Azure Active Directory.</span></span> 

<span data-ttu-id="99fd5-105">**D: come è possibile ottenere la raccolta hello dei dati di attività avviati.**</span><span class="sxs-lookup"><span data-stu-id="99fd5-105">**Q: How can you get hello collection of activity data started?**</span></span>

<span data-ttu-id="99fd5-106">**R:**</span><span class="sxs-lookup"><span data-stu-id="99fd5-106">**A:**</span></span>

| <span data-ttu-id="99fd5-107">Edizione di Azure AD</span><span class="sxs-lookup"><span data-stu-id="99fd5-107">Azure AD Edition</span></span> | <span data-ttu-id="99fd5-108">Avvio della raccolta</span><span class="sxs-lookup"><span data-stu-id="99fd5-108">Collection Start</span></span> |
| :--              | :--   |
| <span data-ttu-id="99fd5-109">Azure AD P1 Premium</span><span class="sxs-lookup"><span data-stu-id="99fd5-109">Azure AD Premium P1</span></span> <br /> <span data-ttu-id="99fd5-110">Azure AD P2 Premium</span><span class="sxs-lookup"><span data-stu-id="99fd5-110">Azure AD Premium P2</span></span> | <span data-ttu-id="99fd5-111">Quando ci si iscrive a una sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="99fd5-111">When you sign-up for a subscription</span></span> |
| <span data-ttu-id="99fd5-112">Azure AD Free</span><span class="sxs-lookup"><span data-stu-id="99fd5-112">Azure AD Free</span></span> | <span data-ttu-id="99fd5-113">Hello prima apertura di hello [Pannello di Azure Active Directory](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) o utilizzare hello [reporting API](https://aka.ms/aadreports)</span><span class="sxs-lookup"><span data-stu-id="99fd5-113">hello first time you open hello [Azure Active Directory blade](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) or use hello [reporting APIs](https://aka.ms/aadreports)</span></span>  |

---
<span data-ttu-id="99fd5-114">**D: quando i dati di attività è disponibile nel portale di Azure hello?**</span><span class="sxs-lookup"><span data-stu-id="99fd5-114">**Q: When is your activity data available in hello Azure portal?**</span></span>

<span data-ttu-id="99fd5-115">**R:**</span><span class="sxs-lookup"><span data-stu-id="99fd5-115">**A:**</span></span>

- <span data-ttu-id="99fd5-116">**Immediatamente** : se sta già utilizzando i report nel portale di Azure classico hello</span><span class="sxs-lookup"><span data-stu-id="99fd5-116">**Immediately** - If you have already been working with reports in hello Azure classic portal</span></span>
- <span data-ttu-id="99fd5-117">**Entro 2 ore** : se è stato attivato reporting in hello portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="99fd5-117">**Within 2 hours** - If you haven’t turned reporting on  in hello Azure classic portal</span></span>

---
<span data-ttu-id="99fd5-118">**D: come è possibile ottenere la raccolta hello dei segnali di sicurezza avviata.**</span><span class="sxs-lookup"><span data-stu-id="99fd5-118">**Q: How can you get hello collection of security signals started?**</span></span>  

<span data-ttu-id="99fd5-119">**R:** per i segnali di sicurezza, viene avviato il processo di raccolta hello quando acconsentire esplicitamente toouse hello Identity Protection Center.</span><span class="sxs-lookup"><span data-stu-id="99fd5-119">**A:** For security signals, hello collection process starts when you opt-in toouse hello Identity Protection Center.</span></span> 


---
<span data-ttu-id="99fd5-120">**D: per quanto tempo è hello archiviati i dati raccolti?**</span><span class="sxs-lookup"><span data-stu-id="99fd5-120">**Q: For how long is hello collected data stored?**</span></span>

<span data-ttu-id="99fd5-121">**R:**</span><span class="sxs-lookup"><span data-stu-id="99fd5-121">**A:**</span></span>

<span data-ttu-id="99fd5-122">**Report attività**</span><span class="sxs-lookup"><span data-stu-id="99fd5-122">**Activity reports**</span></span>    

| <span data-ttu-id="99fd5-123">Report</span><span class="sxs-lookup"><span data-stu-id="99fd5-123">Report</span></span>                 | <span data-ttu-id="99fd5-124">Azure AD Free</span><span class="sxs-lookup"><span data-stu-id="99fd5-124">Azure AD Free</span></span> | <span data-ttu-id="99fd5-125">Azure AD P1 Premium</span><span class="sxs-lookup"><span data-stu-id="99fd5-125">Azure AD Premium P1</span></span> | <span data-ttu-id="99fd5-126">Azure AD P2 Premium</span><span class="sxs-lookup"><span data-stu-id="99fd5-126">Azure AD Premium P2</span></span> |
| :--                    | :--           | :--                 | :--                 |
| <span data-ttu-id="99fd5-127">Directory Audit (Controllo directory)</span><span class="sxs-lookup"><span data-stu-id="99fd5-127">Directory Audit</span></span>        | <span data-ttu-id="99fd5-128">7 giorni</span><span class="sxs-lookup"><span data-stu-id="99fd5-128">7 days</span></span>        | <span data-ttu-id="99fd5-129">30 giorni</span><span class="sxs-lookup"><span data-stu-id="99fd5-129">30 days</span></span>             | <span data-ttu-id="99fd5-130">30 giorni</span><span class="sxs-lookup"><span data-stu-id="99fd5-130">30 days</span></span>             |
| <span data-ttu-id="99fd5-131">Attività di accesso</span><span class="sxs-lookup"><span data-stu-id="99fd5-131">Sign-in Activity</span></span>       | <span data-ttu-id="99fd5-132">7 giorni</span><span class="sxs-lookup"><span data-stu-id="99fd5-132">7 days</span></span>        | <span data-ttu-id="99fd5-133">30 giorni</span><span class="sxs-lookup"><span data-stu-id="99fd5-133">30 days</span></span>             | <span data-ttu-id="99fd5-134">30 giorni</span><span class="sxs-lookup"><span data-stu-id="99fd5-134">30 days</span></span>             |

<span data-ttu-id="99fd5-135">**Segnali di sicurezza**</span><span class="sxs-lookup"><span data-stu-id="99fd5-135">**Security Signals**</span></span>

| <span data-ttu-id="99fd5-136">Report</span><span class="sxs-lookup"><span data-stu-id="99fd5-136">Report</span></span>         | <span data-ttu-id="99fd5-137">Azure AD Free</span><span class="sxs-lookup"><span data-stu-id="99fd5-137">Azure AD Free</span></span> | <span data-ttu-id="99fd5-138">Azure AD P1 Premium</span><span class="sxs-lookup"><span data-stu-id="99fd5-138">Azure AD Premium P1</span></span> | <span data-ttu-id="99fd5-139">Azure AD Premium P2</span><span class="sxs-lookup"><span data-stu-id="99fd5-139">Azure AD Premium P2</span></span> |
| :--            | :--           | :--                 | :--                 |
| <span data-ttu-id="99fd5-140">Utenti a rischio.</span><span class="sxs-lookup"><span data-stu-id="99fd5-140">Users at risk</span></span>  | <span data-ttu-id="99fd5-141">7 giorni</span><span class="sxs-lookup"><span data-stu-id="99fd5-141">7 days</span></span>        | <span data-ttu-id="99fd5-142">30 giorni</span><span class="sxs-lookup"><span data-stu-id="99fd5-142">30 days</span></span>             | <span data-ttu-id="99fd5-143">90 giorni</span><span class="sxs-lookup"><span data-stu-id="99fd5-143">90 days</span></span>             |
| <span data-ttu-id="99fd5-144">Accessi a rischio</span><span class="sxs-lookup"><span data-stu-id="99fd5-144">Risky sign-ins</span></span> | <span data-ttu-id="99fd5-145">7 giorni</span><span class="sxs-lookup"><span data-stu-id="99fd5-145">7 days</span></span>        | <span data-ttu-id="99fd5-146">30 giorni</span><span class="sxs-lookup"><span data-stu-id="99fd5-146">30 days</span></span>             | <span data-ttu-id="99fd5-147">90 giorni</span><span class="sxs-lookup"><span data-stu-id="99fd5-147">90 days</span></span>             |

---