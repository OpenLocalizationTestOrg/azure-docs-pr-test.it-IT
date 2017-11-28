---
title: aaaHow tooAssign utenti tooapplications | Documenti Microsoft
description: Comprendere come gli utenti vengano assegnati tooan applicazione nel tenant
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 4df60c7d723140d0d1bbd6ba8b34aa4e762d1138
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooassign-users-tooapplications"></a><span data-ttu-id="aaa8b-103">Come tooassign utenti tooapplications</span><span class="sxs-lookup"><span data-stu-id="aaa8b-103">How tooassign users tooapplications</span></span>

<span data-ttu-id="aaa8b-104">Questo articolo è utile toounderstand come gli utenti vengano assegnati tooan applicazione nel tenant.</span><span class="sxs-lookup"><span data-stu-id="aaa8b-104">This article help you toounderstand how users get assigned tooan application in your tenant.</span></span>

## <a name="how-do-users-get-assigned-tooan-application-in-azure-ad"></a><span data-ttu-id="aaa8b-105">Come gli utenti vengano assegnati tooan applicazione in Azure AD?</span><span class="sxs-lookup"><span data-stu-id="aaa8b-105">How do users get assigned tooan application in Azure AD?</span></span>

<span data-ttu-id="aaa8b-106">Per un utente tooaccess un'applicazione, è necessario innanzitutto assegnare tooit in qualche modo.</span><span class="sxs-lookup"><span data-stu-id="aaa8b-106">For a user tooaccess an application, they must first be assigned tooit in some way.</span></span> <span data-ttu-id="aaa8b-107">Assegnazione può essere eseguita da un amministratore, un delegato di business o in alcuni casi, utente hello autonomamente.</span><span class="sxs-lookup"><span data-stu-id="aaa8b-107">Assignment can be performed by an administrator, a business delegate, or sometimes, hello user themselves.</span></span> <span data-ttu-id="aaa8b-108">Di seguito descrive gli utenti possono ottenere assegnati tooapplications modi di hello:</span><span class="sxs-lookup"><span data-stu-id="aaa8b-108">Below describes hello ways users can get assigned tooapplications:</span></span>

1.  <span data-ttu-id="aaa8b-109">Un amministratore [assegna un utente](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) toohello applicazione direttamente</span><span class="sxs-lookup"><span data-stu-id="aaa8b-109">An administrator [assigns a user](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) toohello application directly</span></span>

2.  <span data-ttu-id="aaa8b-110">Un amministratore [assegna un gruppo](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) utente hello è un membro dell'applicazione toohello, tra cui:</span><span class="sxs-lookup"><span data-stu-id="aaa8b-110">An administrator [assigns a group](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) that hello user is a member of toohello application, including:</span></span>

  * <span data-ttu-id="aaa8b-111">Un gruppo che è stato sincronizzato da locale</span><span class="sxs-lookup"><span data-stu-id="aaa8b-111">A group that was synchronized from on-premises</span></span>

  * <span data-ttu-id="aaa8b-112">Un gruppo di sicurezza statico creato in un cloud hello</span><span class="sxs-lookup"><span data-stu-id="aaa8b-112">A static security group created in hello cloud</span></span>

  * <span data-ttu-id="aaa8b-113">Oggetto [gruppo di sicurezza dinamica](https://docs.microsoft.com/azure/active-directory/active-directory-groups-dynamic-membership-azure-portal) create in un cloud hello</span><span class="sxs-lookup"><span data-stu-id="aaa8b-113">A [dynamic security group](https://docs.microsoft.com/azure/active-directory/active-directory-groups-dynamic-membership-azure-portal) created in hello cloud</span></span>

  * <span data-ttu-id="aaa8b-114">Un gruppo di Office 365 creato nel cloud hello</span><span class="sxs-lookup"><span data-stu-id="aaa8b-114">An Office 365 group created in hello cloud</span></span>

  * <span data-ttu-id="aaa8b-115">Hello [tutti gli utenti](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-dedicated-groups) gruppo</span><span class="sxs-lookup"><span data-stu-id="aaa8b-115">hello [All Users](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-dedicated-groups) group</span></span>

3.  <span data-ttu-id="aaa8b-116">Un amministratore abilita [accesso all'applicazione Self-Service](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) tooallow tooadd un utente un'applicazione utilizzando hello [Pannello di accesso dell'applicazione](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **Aggiungi App** funzionalità **senza l'approvazione di business**</span><span class="sxs-lookup"><span data-stu-id="aaa8b-116">An administrator enables [Self-service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) tooallow a user tooadd an application using hello [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **Add App** feature **without business approval**</span></span>

4.  <span data-ttu-id="aaa8b-117">Un amministratore abilita [accesso all'applicazione Self-Service](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) tooallow tooadd un utente un'applicazione utilizzando hello [Pannello di accesso dell'applicazione](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **Aggiungi App** funzionalità, ma solo w **i-esimo preventiva approvazione da un set selezionato di responsabili approvazione di business**</span><span class="sxs-lookup"><span data-stu-id="aaa8b-117">An administrator enables [Self-service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) tooallow a user tooadd an application using hello [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **Add App** feature, but only w**ith prior approval from a selected set of business approvers**</span></span>

5.  <span data-ttu-id="aaa8b-118">Un amministratore abilita [gestione dei gruppi Self-Service](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) tooallow toojoin un utente un gruppo che un'applicazione è troppo**senza l'approvazione di business**</span><span class="sxs-lookup"><span data-stu-id="aaa8b-118">An administrator enables [Self-service Group Management](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) tooallow a user toojoin a group that an application is assigned too**without business approval**</span></span>

6.  <span data-ttu-id="aaa8b-119">Un amministratore abilita [gestione dei gruppi Self-Service](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) tooallow toojoin un utente un gruppo che un'applicazione viene assegnata a, ma solo **previa autorizzazione da un set selezionato di responsabili approvazione di business**</span><span class="sxs-lookup"><span data-stu-id="aaa8b-119">An administrator enables [Self-service Group Management](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) tooallow a user toojoin a group that an application is assigned to, but only **with prior approval from a selected set of business approvers**</span></span>

7.  <span data-ttu-id="aaa8b-120">Un amministratore assegna un utente tooa licenza direttamente per la prima applicazione di terze parti, ad esempio [Microsoft Office 365](http://products.office.com/)</span><span class="sxs-lookup"><span data-stu-id="aaa8b-120">An administrator assigns a license tooa user directly for a first party application, like [Microsoft Office 365](http://products.office.com/)</span></span>

8.  <span data-ttu-id="aaa8b-121">Un amministratore assegna a un gruppo di licenze tooa che hello utente è membro tooa prima applicazione di terze parti, ad esempio [Microsoft Office 365](http://products.office.com/)</span><span class="sxs-lookup"><span data-stu-id="aaa8b-121">An administrator assigns a license tooa group that hello user is a member of tooa first party application, like [Microsoft Office 365](http://products.office.com/)</span></span>

9.  <span data-ttu-id="aaa8b-122">Un [amministratore acconsente applicazione tooan](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) toobe utilizzato da tutti gli utenti e quindi un utente accede toohello applicazione</span><span class="sxs-lookup"><span data-stu-id="aaa8b-122">An [administrator consents tooan application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) toobe used by all users and then a user signs in toohello application</span></span>

10. <span data-ttu-id="aaa8b-123">Un utente [acconsente applicazione tooan](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) stesse effettuando l'accesso dell'applicazione toohello</span><span class="sxs-lookup"><span data-stu-id="aaa8b-123">A user [consents tooan application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) themselves by signing in toohello application</span></span>

## <a name="next-steps"></a><span data-ttu-id="aaa8b-124">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="aaa8b-124">Next steps</span></span>
[<span data-ttu-id="aaa8b-125">Gestione di applicazioni con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="aaa8b-125">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
