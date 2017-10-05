---
title: 'Licenze: reimpostazione password self-service di Azure AD | Microsoft Docs'
description: Requisiti di licenza per la reimpostazione password self-service di Azure AD
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: 936134bddad19964f809a17f200ebbeed5aa853c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="licensing-requirements-for-azure-ad-self-service-password-reset"></a><span data-ttu-id="37401-103">Requisiti di licenza per la reimpostazione password self-service di Azure AD</span><span class="sxs-lookup"><span data-stu-id="37401-103">Licensing requirements for Azure AD self-service password reset</span></span>

<span data-ttu-id="37401-104">Per consentire il funzionamento della reimpostazione password di Azure AD, **è necessario che nell'organizzazione sia presente almeno una licenza assegnata**.</span><span class="sxs-lookup"><span data-stu-id="37401-104">In order for Azure AD Password Reset to function, you **must have at least one license assigned in your organization**.</span></span> <span data-ttu-id="37401-105">La reimpostazione password non prevede l'applicazione delle licenze per utente.</span><span class="sxs-lookup"><span data-stu-id="37401-105">We do not enforce per-user licensing on the password reset experience.</span></span> <span data-ttu-id="37401-106">Per mantenere la conformità con il contratto di licenza Microsoft, è necessario assegnare le licenze a tutti gli utenti che usano le funzionalità Premium.</span><span class="sxs-lookup"><span data-stu-id="37401-106">To maintain compliance with your Microsoft licensing agreement, you need to assign licenses to any users that use premium features.</span></span>

* <span data-ttu-id="37401-107">**Solo utenti del cloud** - Office 365 (O365) e SKU a pagamento o Azure AD Basic</span><span class="sxs-lookup"><span data-stu-id="37401-107">**Cloud only users** - Office 365 (O365) any paid SKU, or Azure AD Basic</span></span>
* <span data-ttu-id="37401-108">**Utenti cloud** e/o **utenti locali** - Azure AD P1 Premium o Azure AD P2 Premium, Enterprise Mobility + Security (EMS) o Secure Productive Enterprise (SPE)</span><span class="sxs-lookup"><span data-stu-id="37401-108">**Cloud** and/or **on-premises users** - Azure AD Premium P1 or P2, Enterprise Mobility + Security (EMS), or Secure Productive Enterprise (SPE)</span></span>

## <a name="licenses-required-for-password-writeback"></a><span data-ttu-id="37401-109">Licenze richieste per il writeback delle password</span><span class="sxs-lookup"><span data-stu-id="37401-109">Licenses required for password writeback</span></span>

<span data-ttu-id="37401-110">Per usare il writeback delle password, è necessario disporre una delle licenze seguenti assegnate nel tenant.</span><span class="sxs-lookup"><span data-stu-id="37401-110">To use password writeback, you must have one of the following licenses assigned in your tenant.</span></span>

* <span data-ttu-id="37401-111">Azure AD P1 Premium</span><span class="sxs-lookup"><span data-stu-id="37401-111">Azure AD Premium P1</span></span>
* <span data-ttu-id="37401-112">Azure AD P2 Premium</span><span class="sxs-lookup"><span data-stu-id="37401-112">Azure AD Premium P2</span></span>
* <span data-ttu-id="37401-113">Enterprise Mobility + Security E3</span><span class="sxs-lookup"><span data-stu-id="37401-113">Enterprise Mobility + Security E3</span></span>
* <span data-ttu-id="37401-114">Enterprise Mobility + Security E5</span><span class="sxs-lookup"><span data-stu-id="37401-114">Enterprise Mobility + Security E5</span></span>
* <span data-ttu-id="37401-115">Secure Productive Enterprise E3</span><span class="sxs-lookup"><span data-stu-id="37401-115">Secure Productive Enterprise E3</span></span>
* <span data-ttu-id="37401-116">Secure Productive Enterprise E5</span><span class="sxs-lookup"><span data-stu-id="37401-116">Secure Productive Enterprise E5</span></span>

> [!NOTE]
> <span data-ttu-id="37401-117">I piani di licenza Office 365 autonomi **non supportano il writeback delle password** e richiedono uno dei piani precedenti per l'uso della funzionalità.</span><span class="sxs-lookup"><span data-stu-id="37401-117">Standalone Office 365 licensing plans **do not support password writeback** and require one of the preceding plans for this functionality to work.</span></span>

<span data-ttu-id="37401-118">Informazioni aggiuntive sulle licenze, ad esempio i costi, sono disponibili nelle pagine seguenti.</span><span class="sxs-lookup"><span data-stu-id="37401-118">Additional licensing info including costs can be found on the following pages</span></span>

* [<span data-ttu-id="37401-119">Sito sui prezzi di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="37401-119">Azure Active Directory Pricing site</span></span>](https://azure.microsoft.com/pricing/details/active-directory/)
* [<span data-ttu-id="37401-120">Enterprise Mobility + Security</span><span class="sxs-lookup"><span data-stu-id="37401-120">Enterprise Mobility + Security</span></span>](https://www.microsoft.com/cloud-platform/enterprise-mobility-security)
* [<span data-ttu-id="37401-121">Secure Productive Enterprise</span><span class="sxs-lookup"><span data-stu-id="37401-121">Secure Productive Enterprise</span></span>](https://www.microsoft.com/secure-productive-enterprise/default.aspx)

## <a name="enable-group-or-user-based-licensing"></a><span data-ttu-id="37401-122">Abilitare le licenze per gruppi o per utente</span><span class="sxs-lookup"><span data-stu-id="37401-122">Enable group or user-based licensing</span></span>

<span data-ttu-id="37401-123">Azure AD supporta ora licenze per gruppi che consentono agli amministratori di assegnare le licenze in blocco a un gruppo di utenti, anziché assegnarle loro singolarmente.</span><span class="sxs-lookup"><span data-stu-id="37401-123">Azure AD now supports group-based licensing allowing administrators to assign licenses in bulk to a group of users, rather than assigning them one at a time.</span></span> [<span data-ttu-id="37401-124">Assegnare, verificare e risolvere i problemi relativi alle licenze</span><span class="sxs-lookup"><span data-stu-id="37401-124">Assign, verify, and resolve problems with licenses</span></span>](active-directory-licensing-group-assignment-azure-portal.md#step-1-assign-the-required-licenses)

<span data-ttu-id="37401-125">Alcuni servizi Microsoft non sono disponibili in tutte le posizioni.</span><span class="sxs-lookup"><span data-stu-id="37401-125">Some Microsoft services are not available in all locations.</span></span> <span data-ttu-id="37401-126">Per assegnare una licenza a un utente, l'amministratore deve prima specificare la proprietà relativa alla località di uso per l'utente.</span><span class="sxs-lookup"><span data-stu-id="37401-126">Before a license can be assigned to a user, the administrator must specify the “Usage location” property on the user.</span></span> <span data-ttu-id="37401-127">L'assegnazione delle licenze può essere eseguita nella sezione Utente > Profilo > Impostazioni nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="37401-127">Assignment of licenses can be done under User > Profile > Settings section in the Azure portal.</span></span> <span data-ttu-id="37401-128">**Quando si usa l'assegnazione di licenze ai gruppi, tutti gli utenti per cui non è specificata un percorso d'uso ereditano il percorso della directory**</span><span class="sxs-lookup"><span data-stu-id="37401-128">**When using group license assignment, any users without a usage location specified inherit the location of the directory.**</span></span>

## <a name="next-steps"></a><span data-ttu-id="37401-129">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="37401-129">Next steps</span></span>

<span data-ttu-id="37401-130">I collegamenti seguenti forniscono altre informazioni sull'uso della reimpostazione della password con Azure AD</span><span class="sxs-lookup"><span data-stu-id="37401-130">The following links provide additional information regarding password reset using Azure AD</span></span>

* <span data-ttu-id="37401-131">[**Guida introduttiva**](active-directory-passwords-getting-started.md): iniziare a usare la gestione self-service delle password di Azure AD</span><span class="sxs-lookup"><span data-stu-id="37401-131">[**Quick Start**](active-directory-passwords-getting-started.md) - Get up and running with Azure AD self service password management</span></span> 
* <span data-ttu-id="37401-132">[**Dati** ](active-directory-passwords-data.md): informazioni sui dati necessari e su come vengono usati per la gestione delle password</span><span class="sxs-lookup"><span data-stu-id="37401-132">[**Data**](active-directory-passwords-data.md) - Understand the data that is required and how it is used for password management</span></span>
* <span data-ttu-id="37401-133">[**Implementazione**](active-directory-passwords-best-practices.md): pianificare e distribuire agli utenti la reimpostazione password self-service usando le istruzioni disponibili in questo articolo</span><span class="sxs-lookup"><span data-stu-id="37401-133">[**Rollout**](active-directory-passwords-best-practices.md) - Plan and deploy SSPR to your users using the guidance found here</span></span>
* <span data-ttu-id="37401-134">[**Personalizzazione**](active-directory-passwords-customize.md): personalizzare l'aspetto dell'esperienza della reimpostazione password self-service per l'azienda.</span><span class="sxs-lookup"><span data-stu-id="37401-134">[**Customize**](active-directory-passwords-customize.md) - Customize the look and feel of the SSPR experience for your company.</span></span>
* <span data-ttu-id="37401-135">[**Reporting** ](active-directory-passwords-reporting.md): verificare se, quando e dove gli utenti accedono alla reimpostazione password self-service</span><span class="sxs-lookup"><span data-stu-id="37401-135">[**Reporting**](active-directory-passwords-reporting.md) - Discover if, when, and where your users are accessing SSPR functionality</span></span>
* <span data-ttu-id="37401-136">[**Approfondimento tecnico**](active-directory-passwords-how-it-works.md): approfondimento sul funzionamento</span><span class="sxs-lookup"><span data-stu-id="37401-136">[**Technical Deep Dive**](active-directory-passwords-how-it-works.md) - Go behind the curtain to understand how it works</span></span>
* <span data-ttu-id="37401-137">[**Domande frequenti**](active-directory-passwords-faq.md) - Come</span><span class="sxs-lookup"><span data-stu-id="37401-137">[**Frequently Asked Questions**](active-directory-passwords-faq.md) - How?</span></span> <span data-ttu-id="37401-138">Perché?</span><span class="sxs-lookup"><span data-stu-id="37401-138">Why?</span></span> <span data-ttu-id="37401-139">Cosa?</span><span class="sxs-lookup"><span data-stu-id="37401-139">What?</span></span> <span data-ttu-id="37401-140">Dove?</span><span class="sxs-lookup"><span data-stu-id="37401-140">Where?</span></span> <span data-ttu-id="37401-141">Chi?</span><span class="sxs-lookup"><span data-stu-id="37401-141">Who?</span></span> <span data-ttu-id="37401-142">Quando?</span><span class="sxs-lookup"><span data-stu-id="37401-142">When?</span></span> <span data-ttu-id="37401-143">- Risposte alle domande di maggiore interesse</span><span class="sxs-lookup"><span data-stu-id="37401-143">- Answers to questions you always wanted to ask</span></span>
* <span data-ttu-id="37401-144">[**Risoluzione dei problemi**](active-directory-passwords-troubleshoot.md): informazioni su come risolvere i problemi comuni con la reimpostazione password self-service</span><span class="sxs-lookup"><span data-stu-id="37401-144">[**Troubleshoot**](active-directory-passwords-troubleshoot.md) - Learn how to resolve common issues that we see with SSPR</span></span>

