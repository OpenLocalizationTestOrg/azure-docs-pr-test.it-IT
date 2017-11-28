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
ms.openlocfilehash: 9cecaaac429165346f7082f1965dc8a21063fe7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="licensing-requirements-for-azure-ad-self-service-password-reset"></a><span data-ttu-id="576a8-103">Requisiti di licenza per la reimpostazione password self-service di Azure AD</span><span class="sxs-lookup"><span data-stu-id="576a8-103">Licensing requirements for Azure AD self-service password reset</span></span>

<span data-ttu-id="576a8-104">Affinché la reimpostazione della Password AD Azure toofunction, si **deve avere almeno una licenza assegnata all'interno dell'organizzazione**.</span><span class="sxs-lookup"><span data-stu-id="576a8-104">In order for Azure AD Password Reset toofunction, you **must have at least one license assigned in your organization**.</span></span> <span data-ttu-id="576a8-105">Non si applica sull'esperienza di reimpostazione della password hello di licenza per utente.</span><span class="sxs-lookup"><span data-stu-id="576a8-105">We do not enforce per-user licensing on hello password reset experience.</span></span> <span data-ttu-id="576a8-106">conformità toomaintain con contratto di licenza Microsoft, è necessario agli utenti di tooany licenze tooassign che usano le funzionalità premium.</span><span class="sxs-lookup"><span data-stu-id="576a8-106">toomaintain compliance with your Microsoft licensing agreement, you need tooassign licenses tooany users that use premium features.</span></span>

* <span data-ttu-id="576a8-107">**Solo utenti del cloud** - Office 365 (O365) e SKU a pagamento o Azure AD Basic</span><span class="sxs-lookup"><span data-stu-id="576a8-107">**Cloud only users** - Office 365 (O365) any paid SKU, or Azure AD Basic</span></span>
* <span data-ttu-id="576a8-108">**Utenti cloud** e/o **utenti locali** - Azure AD P1 Premium o Azure AD P2 Premium, Enterprise Mobility + Security (EMS) o Secure Productive Enterprise (SPE)</span><span class="sxs-lookup"><span data-stu-id="576a8-108">**Cloud** and/or **on-premises users** - Azure AD Premium P1 or P2, Enterprise Mobility + Security (EMS), or Secure Productive Enterprise (SPE)</span></span>

## <a name="licenses-required-for-password-writeback"></a><span data-ttu-id="576a8-109">Licenze richieste per il writeback delle password</span><span class="sxs-lookup"><span data-stu-id="576a8-109">Licenses required for password writeback</span></span>

<span data-ttu-id="576a8-110">il writeback delle password toouse, è necessario uno dei seguenti licenze assegnate nel tenant di hello.</span><span class="sxs-lookup"><span data-stu-id="576a8-110">toouse password writeback, you must have one of hello following licenses assigned in your tenant.</span></span>

* <span data-ttu-id="576a8-111">Azure AD Premium P1</span><span class="sxs-lookup"><span data-stu-id="576a8-111">Azure AD Premium P1</span></span>
* <span data-ttu-id="576a8-112">Azure AD P2 Premium</span><span class="sxs-lookup"><span data-stu-id="576a8-112">Azure AD Premium P2</span></span>
* <span data-ttu-id="576a8-113">Enterprise Mobility + Security E3</span><span class="sxs-lookup"><span data-stu-id="576a8-113">Enterprise Mobility + Security E3</span></span>
* <span data-ttu-id="576a8-114">Enterprise Mobility + Security E5</span><span class="sxs-lookup"><span data-stu-id="576a8-114">Enterprise Mobility + Security E5</span></span>
* <span data-ttu-id="576a8-115">Secure Productive Enterprise E3</span><span class="sxs-lookup"><span data-stu-id="576a8-115">Secure Productive Enterprise E3</span></span>
* <span data-ttu-id="576a8-116">Secure Productive Enterprise E5</span><span class="sxs-lookup"><span data-stu-id="576a8-116">Secure Productive Enterprise E5</span></span>

> [!NOTE]
> <span data-ttu-id="576a8-117">I piani di licenza autonoma Office 365 **non supportano il writeback delle password** e richiedono una di hello che precede i piani per toowork questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="576a8-117">Standalone Office 365 licensing plans **do not support password writeback** and require one of hello preceding plans for this functionality toowork.</span></span>

<span data-ttu-id="576a8-118">Informazioni sulle licenze aggiuntive, inclusi i costi di sono reperibili nelle seguenti pagine hello</span><span class="sxs-lookup"><span data-stu-id="576a8-118">Additional licensing info including costs can be found on hello following pages</span></span>

* [<span data-ttu-id="576a8-119">Sito sui prezzi di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="576a8-119">Azure Active Directory Pricing site</span></span>](https://azure.microsoft.com/pricing/details/active-directory/)
* [<span data-ttu-id="576a8-120">Enterprise Mobility + Security</span><span class="sxs-lookup"><span data-stu-id="576a8-120">Enterprise Mobility + Security</span></span>](https://www.microsoft.com/cloud-platform/enterprise-mobility-security)
* [<span data-ttu-id="576a8-121">Secure Productive Enterprise</span><span class="sxs-lookup"><span data-stu-id="576a8-121">Secure Productive Enterprise</span></span>](https://www.microsoft.com/secure-productive-enterprise/default.aspx)

## <a name="enable-group-or-user-based-licensing"></a><span data-ttu-id="576a8-122">Abilitare le licenze per gruppi o per utente</span><span class="sxs-lookup"><span data-stu-id="576a8-122">Enable group or user-based licensing</span></span>

<span data-ttu-id="576a8-123">Azure AD supporta ora in base al gruppo di licenza che consente agli amministratori tooassign licenze gruppo tooa bulk di utenti, anziché assegnando loro uno alla volta.</span><span class="sxs-lookup"><span data-stu-id="576a8-123">Azure AD now supports group-based licensing allowing administrators tooassign licenses in bulk tooa group of users, rather than assigning them one at a time.</span></span> [<span data-ttu-id="576a8-124">Assegnare, verificare e risolvere i problemi relativi alle licenze</span><span class="sxs-lookup"><span data-stu-id="576a8-124">Assign, verify, and resolve problems with licenses</span></span>](active-directory-licensing-group-assignment-azure-portal.md#step-1-assign-the-required-licenses)

<span data-ttu-id="576a8-125">Alcuni servizi Microsoft non sono disponibili in tutte le posizioni.</span><span class="sxs-lookup"><span data-stu-id="576a8-125">Some Microsoft services are not available in all locations.</span></span> <span data-ttu-id="576a8-126">Prima che può essere assegnata una licenza utente tooa, amministratore hello specificare proprietà "Località di utilizzo" hello utente hello.</span><span class="sxs-lookup"><span data-stu-id="576a8-126">Before a license can be assigned tooa user, hello administrator must specify hello “Usage location” property on hello user.</span></span> <span data-ttu-id="576a8-127">Assegnazione delle licenze possa essere consentita nell'ambito di utente > profilo > della sezione Impostazioni hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="576a8-127">Assignment of licenses can be done under User > Profile > Settings section in hello Azure portal.</span></span> <span data-ttu-id="576a8-128">**Quando si utilizza l'assegnazione del gruppo di licenze, tutti gli utenti senza specificata una località di utilizzo ereditano percorso hello della directory di hello.**</span><span class="sxs-lookup"><span data-stu-id="576a8-128">**When using group license assignment, any users without a usage location specified inherit hello location of hello directory.**</span></span>

## <a name="next-steps"></a><span data-ttu-id="576a8-129">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="576a8-129">Next steps</span></span>

<span data-ttu-id="576a8-130">Hello seguenti collegamenti fornisce ulteriori informazioni sull'uso di Azure AD di reimpostazione della password</span><span class="sxs-lookup"><span data-stu-id="576a8-130">hello following links provide additional information regarding password reset using Azure AD</span></span>

* <span data-ttu-id="576a8-131">[**Guida introduttiva**](active-directory-passwords-getting-started.md) - Iniziare a usare la gestione self-service delle password di Azure AD</span><span class="sxs-lookup"><span data-stu-id="576a8-131">[**Quick Start**](active-directory-passwords-getting-started.md) - Get up and running with Azure AD self service password management</span></span> 
* <span data-ttu-id="576a8-132">[**Dati** ](active-directory-passwords-data.md) : comprendere hello i dati necessari e come utilizzarlo per la gestione delle password</span><span class="sxs-lookup"><span data-stu-id="576a8-132">[**Data**](active-directory-passwords-data.md) - Understand hello data that is required and how it is used for password management</span></span>
* <span data-ttu-id="576a8-133">[**Implementazione** ](active-directory-passwords-best-practices.md) -pianificare e distribuire agli utenti di tooyour SSPR utilizzando istruzioni hello disponibili qui</span><span class="sxs-lookup"><span data-stu-id="576a8-133">[**Rollout**](active-directory-passwords-best-practices.md) - Plan and deploy SSPR tooyour users using hello guidance found here</span></span>
* <span data-ttu-id="576a8-134">[**Personalizzare** ](active-directory-passwords-customize.md) -personalizzare hello aspetto di hello SSPR esperienza per l'azienda.</span><span class="sxs-lookup"><span data-stu-id="576a8-134">[**Customize**](active-directory-passwords-customize.md) - Customize hello look and feel of hello SSPR experience for your company.</span></span>
* <span data-ttu-id="576a8-135">[**Creazione di report**](active-directory-passwords-reporting.md) - verificare se, quando e dove gli utenti accedono alla reimpostazione password self-service</span><span class="sxs-lookup"><span data-stu-id="576a8-135">[**Reporting**](active-directory-passwords-reporting.md) - Discover if, when, and where your users are accessing SSPR functionality</span></span>
* <span data-ttu-id="576a8-136">[**Approfondimento tecnico** ](active-directory-passwords-how-it-works.md) -Vai dietro hello pannelli toounderstand come funziona</span><span class="sxs-lookup"><span data-stu-id="576a8-136">[**Technical Deep Dive**](active-directory-passwords-how-it-works.md) - Go behind hello curtain toounderstand how it works</span></span>
* <span data-ttu-id="576a8-137">[**Domande frequenti**](active-directory-passwords-faq.md) - Come</span><span class="sxs-lookup"><span data-stu-id="576a8-137">[**Frequently Asked Questions**](active-directory-passwords-faq.md) - How?</span></span> <span data-ttu-id="576a8-138">Perché?</span><span class="sxs-lookup"><span data-stu-id="576a8-138">Why?</span></span> <span data-ttu-id="576a8-139">Cosa?</span><span class="sxs-lookup"><span data-stu-id="576a8-139">What?</span></span> <span data-ttu-id="576a8-140">Dove?</span><span class="sxs-lookup"><span data-stu-id="576a8-140">Where?</span></span> <span data-ttu-id="576a8-141">Chi?</span><span class="sxs-lookup"><span data-stu-id="576a8-141">Who?</span></span> <span data-ttu-id="576a8-142">Quando?</span><span class="sxs-lookup"><span data-stu-id="576a8-142">When?</span></span> <span data-ttu-id="576a8-143">-Risposte tooquestions si desiderava sempre tooask</span><span class="sxs-lookup"><span data-stu-id="576a8-143">- Answers tooquestions you always wanted tooask</span></span>
* <span data-ttu-id="576a8-144">[**Risoluzione dei problemi** ](active-directory-passwords-troubleshoot.md) -informazioni su come tooresolve comuni problemi che vedremo con SSPR</span><span class="sxs-lookup"><span data-stu-id="576a8-144">[**Troubleshoot**](active-directory-passwords-troubleshoot.md) - Learn how tooresolve common issues that we see with SSPR</span></span>

