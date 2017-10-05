---
title: Criteri di conservazione dei report di Azure Active Directory | Documentazione Microsoft
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
ms.openlocfilehash: ffeba8a6c32a21c75af21f948bbd6ea88dd9278c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-report-retention-policies"></a><span data-ttu-id="03b60-103">Criteri di conservazione dei report di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="03b60-103">Azure Active Directory report retention policies</span></span>


<span data-ttu-id="03b60-104">Questo argomento offre le risposte alle domande più comuni sulla conservazione dei dati per i diversi report attività in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="03b60-104">This topic provides you with answers to the most common questions in conjunction with the data retention for the different activity reports in Azure Active Directory.</span></span> 

<span data-ttu-id="03b60-105">**D: Come è possibile avviare la raccolta dei dati dell'attività?**</span><span class="sxs-lookup"><span data-stu-id="03b60-105">**Q: How can you get the collection of activity data started?**</span></span>

<span data-ttu-id="03b60-106">**R:**</span><span class="sxs-lookup"><span data-stu-id="03b60-106">**A:**</span></span>

| <span data-ttu-id="03b60-107">Edizione di Azure AD</span><span class="sxs-lookup"><span data-stu-id="03b60-107">Azure AD Edition</span></span> | <span data-ttu-id="03b60-108">Avvio della raccolta</span><span class="sxs-lookup"><span data-stu-id="03b60-108">Collection Start</span></span> |
| :--              | :--   |
| <span data-ttu-id="03b60-109">Azure AD P1 Premium</span><span class="sxs-lookup"><span data-stu-id="03b60-109">Azure AD Premium P1</span></span> <br /> <span data-ttu-id="03b60-110">Azure AD P2 Premium</span><span class="sxs-lookup"><span data-stu-id="03b60-110">Azure AD Premium P2</span></span> | <span data-ttu-id="03b60-111">Quando ci si iscrive a una sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="03b60-111">When you sign-up for a subscription</span></span> |
| <span data-ttu-id="03b60-112">Azure AD Free</span><span class="sxs-lookup"><span data-stu-id="03b60-112">Azure AD Free</span></span> | <span data-ttu-id="03b60-113">La prima volta che si apre il [pannello Azure Active Directory](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) o si usano le [API di creazione report](https://aka.ms/aadreports)</span><span class="sxs-lookup"><span data-stu-id="03b60-113">The first time you open the [Azure Active Directory blade](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) or use the [reporting APIs](https://aka.ms/aadreports)</span></span>  |

---
<span data-ttu-id="03b60-114">**D: Quando i dati dell'attività sono disponibili nel portale di Azure?**</span><span class="sxs-lookup"><span data-stu-id="03b60-114">**Q: When is your activity data available in the Azure portal?**</span></span>

<span data-ttu-id="03b60-115">**R:**</span><span class="sxs-lookup"><span data-stu-id="03b60-115">**A:**</span></span>

- <span data-ttu-id="03b60-116">**Immediatamente**: se si usano già i report nel portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="03b60-116">**Immediately** - If you have already been working with reports in the Azure classic portal</span></span>
- <span data-ttu-id="03b60-117">**Entro 2 ore**: se non si è attivata la creazione di report nel portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="03b60-117">**Within 2 hours** - If you haven’t turned reporting on  in the Azure classic portal</span></span>

---
<span data-ttu-id="03b60-118">**D: Come è possibile avviare la raccolta dei segnali di sicurezza?**</span><span class="sxs-lookup"><span data-stu-id="03b60-118">**Q: How can you get the collection of security signals started?**</span></span>  

<span data-ttu-id="03b60-119">**R:** Per i segnali di sicurezza, il processo di raccolta viene avviato quando si acconsente esplicitamente all'uso di Identity Protection Center.</span><span class="sxs-lookup"><span data-stu-id="03b60-119">**A:** For security signals, the collection process starts when you opt-in to use the Identity Protection Center.</span></span> 


---
<span data-ttu-id="03b60-120">**D: Per quanto tempo rimangono archiviati i dati raccolti?**</span><span class="sxs-lookup"><span data-stu-id="03b60-120">**Q: For how long is the collected data stored?**</span></span>

<span data-ttu-id="03b60-121">**R:**</span><span class="sxs-lookup"><span data-stu-id="03b60-121">**A:**</span></span>

<span data-ttu-id="03b60-122">**Report attività**</span><span class="sxs-lookup"><span data-stu-id="03b60-122">**Activity reports**</span></span>    

| <span data-ttu-id="03b60-123">Report</span><span class="sxs-lookup"><span data-stu-id="03b60-123">Report</span></span>                 | <span data-ttu-id="03b60-124">Azure AD Free</span><span class="sxs-lookup"><span data-stu-id="03b60-124">Azure AD Free</span></span> | <span data-ttu-id="03b60-125">Azure AD P1 Premium</span><span class="sxs-lookup"><span data-stu-id="03b60-125">Azure AD Premium P1</span></span> | <span data-ttu-id="03b60-126">Azure AD P2 Premium</span><span class="sxs-lookup"><span data-stu-id="03b60-126">Azure AD Premium P2</span></span> |
| :--                    | :--           | :--                 | :--                 |
| <span data-ttu-id="03b60-127">Directory Audit (Controllo directory)</span><span class="sxs-lookup"><span data-stu-id="03b60-127">Directory Audit</span></span>        | <span data-ttu-id="03b60-128">7 giorni</span><span class="sxs-lookup"><span data-stu-id="03b60-128">7 days</span></span>        | <span data-ttu-id="03b60-129">30 giorni</span><span class="sxs-lookup"><span data-stu-id="03b60-129">30 days</span></span>             | <span data-ttu-id="03b60-130">30 giorni</span><span class="sxs-lookup"><span data-stu-id="03b60-130">30 days</span></span>             |
| <span data-ttu-id="03b60-131">Attività di accesso</span><span class="sxs-lookup"><span data-stu-id="03b60-131">Sign-in Activity</span></span>       | <span data-ttu-id="03b60-132">7 giorni</span><span class="sxs-lookup"><span data-stu-id="03b60-132">7 days</span></span>        | <span data-ttu-id="03b60-133">30 giorni</span><span class="sxs-lookup"><span data-stu-id="03b60-133">30 days</span></span>             | <span data-ttu-id="03b60-134">30 giorni</span><span class="sxs-lookup"><span data-stu-id="03b60-134">30 days</span></span>             |

<span data-ttu-id="03b60-135">**Segnali di sicurezza**</span><span class="sxs-lookup"><span data-stu-id="03b60-135">**Security Signals**</span></span>

| <span data-ttu-id="03b60-136">Report</span><span class="sxs-lookup"><span data-stu-id="03b60-136">Report</span></span>         | <span data-ttu-id="03b60-137">Azure AD Free</span><span class="sxs-lookup"><span data-stu-id="03b60-137">Azure AD Free</span></span> | <span data-ttu-id="03b60-138">Azure AD P1 Premium</span><span class="sxs-lookup"><span data-stu-id="03b60-138">Azure AD Premium P1</span></span> | <span data-ttu-id="03b60-139">Azure AD Premium P2</span><span class="sxs-lookup"><span data-stu-id="03b60-139">Azure AD Premium P2</span></span> |
| :--            | :--           | :--                 | :--                 |
| <span data-ttu-id="03b60-140">Utenti a rischio.</span><span class="sxs-lookup"><span data-stu-id="03b60-140">Users at risk</span></span>  | <span data-ttu-id="03b60-141">7 giorni</span><span class="sxs-lookup"><span data-stu-id="03b60-141">7 days</span></span>        | <span data-ttu-id="03b60-142">30 giorni</span><span class="sxs-lookup"><span data-stu-id="03b60-142">30 days</span></span>             | <span data-ttu-id="03b60-143">90 giorni</span><span class="sxs-lookup"><span data-stu-id="03b60-143">90 days</span></span>             |
| <span data-ttu-id="03b60-144">Accessi a rischio</span><span class="sxs-lookup"><span data-stu-id="03b60-144">Risky sign-ins</span></span> | <span data-ttu-id="03b60-145">7 giorni</span><span class="sxs-lookup"><span data-stu-id="03b60-145">7 days</span></span>        | <span data-ttu-id="03b60-146">30 giorni</span><span class="sxs-lookup"><span data-stu-id="03b60-146">30 days</span></span>             | <span data-ttu-id="03b60-147">90 giorni</span><span class="sxs-lookup"><span data-stu-id="03b60-147">90 days</span></span>             |

---