---
title: Come assegnare gli utenti alle applicazioni | Microsoft Docs
description: Comprendere come vengono assegnati gli utenti a un'applicazione nel tenant
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
ms.openlocfilehash: 916238ba402a2555bac620d7f08e02799d981ae0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-assign-users-to-applications"></a><span data-ttu-id="01e63-103">Come assegnare gli utenti alle applicazioni</span><span class="sxs-lookup"><span data-stu-id="01e63-103">How to assign users to applications</span></span>

<span data-ttu-id="01e63-104">Questo articolo consente di comprendere come vengono assegnati gli utenti a un'applicazione nel tenant.</span><span class="sxs-lookup"><span data-stu-id="01e63-104">This article help you to understand how users get assigned to an application in your tenant.</span></span>

## <a name="how-do-users-get-assigned-to-an-application-in-azure-ad"></a><span data-ttu-id="01e63-105">Come vengono assegnati gli utenti a un'applicazione in Azure AD?</span><span class="sxs-lookup"><span data-stu-id="01e63-105">How do users get assigned to an application in Azure AD?</span></span>

<span data-ttu-id="01e63-106">Un utente deve prima essere assegnato a un'applicazione per potervi accedere.</span><span class="sxs-lookup"><span data-stu-id="01e63-106">For a user to access an application, they must first be assigned to it in some way.</span></span> <span data-ttu-id="01e63-107">L'assegnazione può essere eseguita da un amministratore, da un delegato aziendale o, talvolta, dall'utente stesso.</span><span class="sxs-lookup"><span data-stu-id="01e63-107">Assignment can be performed by an administrator, a business delegate, or sometimes, the user themselves.</span></span> <span data-ttu-id="01e63-108">Di seguito vengono descritti i modi in cui gli utenti possono essere assegnati alle applicazioni:</span><span class="sxs-lookup"><span data-stu-id="01e63-108">Below describes the ways users can get assigned to applications:</span></span>

1.  <span data-ttu-id="01e63-109">Un amministratore [assegna un utente](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) direttamente all'applicazione</span><span class="sxs-lookup"><span data-stu-id="01e63-109">An administrator [assigns a user](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) to the application directly</span></span>

2.  <span data-ttu-id="01e63-110">Un amministratore [assegna un gruppo](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal), del quale l'utente è membro, all'applicazione, inclusi:</span><span class="sxs-lookup"><span data-stu-id="01e63-110">An administrator [assigns a group](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) that the user is a member of to the application, including:</span></span>

  * <span data-ttu-id="01e63-111">Un gruppo che è stato sincronizzato da locale</span><span class="sxs-lookup"><span data-stu-id="01e63-111">A group that was synchronized from on-premises</span></span>

  * <span data-ttu-id="01e63-112">Un gruppo di sicurezza statico creato nel cloud</span><span class="sxs-lookup"><span data-stu-id="01e63-112">A static security group created in the cloud</span></span>

  * <span data-ttu-id="01e63-113">Un [gruppo di sicurezza dinamico](https://docs.microsoft.com/azure/active-directory/active-directory-groups-dynamic-membership-azure-portal) creato nel cloud</span><span class="sxs-lookup"><span data-stu-id="01e63-113">A [dynamic security group](https://docs.microsoft.com/azure/active-directory/active-directory-groups-dynamic-membership-azure-portal) created in the cloud</span></span>

  * <span data-ttu-id="01e63-114">Un gruppo di Office 365 creato nel cloud</span><span class="sxs-lookup"><span data-stu-id="01e63-114">An Office 365 group created in the cloud</span></span>

  * <span data-ttu-id="01e63-115">Il gruppo [Tutti gli utenti](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-dedicated-groups)</span><span class="sxs-lookup"><span data-stu-id="01e63-115">The [All Users](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-dedicated-groups) group</span></span>

3.  <span data-ttu-id="01e63-116">Un amministratore abilita l'[Accesso all'applicazione self-service](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) per consentire all'utente di aggiungere un'applicazione usando la funzionalità **Aggiungi app** del [Pannello di accesso dell'applicazione](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **senza l'approvazione aziendale**</span><span class="sxs-lookup"><span data-stu-id="01e63-116">An administrator enables [Self-service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) to allow a user to add an application using the [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **Add App** feature **without business approval**</span></span>

4.  <span data-ttu-id="01e63-117">Un amministratore abilita l'[Accesso all'applicazione self-service](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) per consentire all'utente di aggiungere un'applicazione usando la funzionalità **Aggiungi app** del [Pannello di accesso dell'applicazione](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction), ma solo **con l'approvazione previa di una serie di responsabili approvazione aziendali selezionati**</span><span class="sxs-lookup"><span data-stu-id="01e63-117">An administrator enables [Self-service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) to allow a user to add an application using the [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **Add App** feature, but only w**ith prior approval from a selected set of business approvers**</span></span>

5.  <span data-ttu-id="01e63-118">Un amministratore abilita la [Gestione gruppi self-service](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) per consentire a un utente di partecipare a un gruppo assegnato a un'applicazione **senza l'approvazione aziendale**</span><span class="sxs-lookup"><span data-stu-id="01e63-118">An administrator enables [Self-service Group Management](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) to allow a user to join a group that an application is assigned to **without business approval**</span></span>

6.  <span data-ttu-id="01e63-119">Un amministratore abilita la [Gestione gruppi self-service](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) per consentire a un utente di partecipare a un gruppo assegnato a un'applicazione, ma solo **con l'approvazione previa di una serie di responsabili approvazione aziendali selezionati**</span><span class="sxs-lookup"><span data-stu-id="01e63-119">An administrator enables [Self-service Group Management](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) to allow a user to join a group that an application is assigned to, but only **with prior approval from a selected set of business approvers**</span></span>

7.  <span data-ttu-id="01e63-120">Un amministratore assegna una licenza direttamente a un utente per un'applicazione prodotta per esempio da [Microsoft Office 365](http://products.office.com/)</span><span class="sxs-lookup"><span data-stu-id="01e63-120">An administrator assigns a license to a user directly for a first party application, like [Microsoft Office 365](http://products.office.com/)</span></span>

8.  <span data-ttu-id="01e63-121">Un amministratore assegna una licenza a un gruppo del quale l'utente è membro a un'applicazione prodotta per esempio da [Microsoft Office 365](http://products.office.com/)</span><span class="sxs-lookup"><span data-stu-id="01e63-121">An administrator assigns a license to a group that the user is a member of to a first party application, like [Microsoft Office 365](http://products.office.com/)</span></span>

9.  <span data-ttu-id="01e63-122">Un [amministratore dà il consenso a un'applicazione](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) per essere usata da tutti gli utenti e quindi un utente effettua l'accesso all'applicazione</span><span class="sxs-lookup"><span data-stu-id="01e63-122">An [administrator consents to an application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) to be used by all users and then a user signs in to the application</span></span>

10. <span data-ttu-id="01e63-123">Un utente [dà il consenso a un'applicazione](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) da solo effettuando l'accesso all'applicazione</span><span class="sxs-lookup"><span data-stu-id="01e63-123">A user [consents to an application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) themselves by signing in to the application</span></span>

## <a name="next-steps"></a><span data-ttu-id="01e63-124">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="01e63-124">Next steps</span></span>
[<span data-ttu-id="01e63-125">Gestione di applicazioni con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="01e63-125">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
