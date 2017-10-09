---
title: le assegnazioni di accesso di aaaView risorse di Azure | Documenti Microsoft
description: Visualizzare e gestire tutte le assegnazioni di controllo di accesso basato sui ruoli hello per qualsiasi utente o gruppo in hello portale di Azure
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
editor: jeffsta
ms.assetid: e6f9e657-8ee3-4eec-a21c-78fe1b52a005
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/04/2017
ms.author: andredm
ms.openlocfilehash: ec96c9d4b9e2cb4925949b8bac78767bd564c8ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="view-access-assignments-for-users-and-groups-in-hello-azure-portal"></a><span data-ttu-id="0bc66-103">Visualizzare le assegnazioni di accesso per utenti e gruppi in hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="0bc66-103">View access assignments for users and groups in hello Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0bc66-104">Gestire l'accesso per utente o gruppo</span><span class="sxs-lookup"><span data-stu-id="0bc66-104">Manage access by user or group</span></span>](role-based-access-control-manage-assignments.md)
> * [<span data-ttu-id="0bc66-105">Gestire l'accesso per risorsa</span><span class="sxs-lookup"><span data-stu-id="0bc66-105">Manage access by resource</span></span>](role-based-access-control-configure.md)

<span data-ttu-id="0bc66-106">Controllo di accesso basato sui ruoli (RBAC) in hello Azure Active Directory (Azure AD), è possibile gestire l'accesso tooyour Azure le risorse.</span><span class="sxs-lookup"><span data-stu-id="0bc66-106">With role-based access control (RBAC) in hello Azure Active Directory (Azure AD), you can manage access tooyour Azure resources.</span></span> 

<span data-ttu-id="0bc66-107">Accesso assegnato con RBAC è accurato perché è possibile limitare le autorizzazioni di hello in due modi:</span><span class="sxs-lookup"><span data-stu-id="0bc66-107">Access assigned with RBAC is fine-grained because there are two ways you can restrict hello permissions:</span></span>

* <span data-ttu-id="0bc66-108">**Ambito:** le assegnazioni di ruolo RBAC sono tooa con ambito specifico sottoscrizione, gruppo di risorse o risorse.</span><span class="sxs-lookup"><span data-stu-id="0bc66-108">**Scope:** RBAC role assignments are scoped tooa specific subscription, resource group, or resource.</span></span> <span data-ttu-id="0bc66-109">Un utente con accesso tooa singola risorsa non è possibile accedere alle altre risorse hello stessa sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="0bc66-109">A user given access tooa single resource cannot access any other resources in hello same subscription.</span></span>
* <span data-ttu-id="0bc66-110">**Ruolo:** nell'ambito di hello di assegnazione di hello, l'accesso è limitato, ulteriormente tramite l'assegnazione di un ruolo.</span><span class="sxs-lookup"><span data-stu-id="0bc66-110">**Role:** Within hello scope of hello assignment, access is narrowed even further by assigning a role.</span></span> <span data-ttu-id="0bc66-111">I ruoli possono essere di livello superiore, ad esempio quello di proprietario, o specifici, ad esempio quello di lettore di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="0bc66-111">Roles can be high-level, like owner, or specific, like virtual machine reader.</span></span>

<span data-ttu-id="0bc66-112">Ruoli possono essere assegnati solo all'interno di sottoscrizione hello, gruppo di risorse o risorse che sono hello ambito per l'assegnazione di hello.</span><span class="sxs-lookup"><span data-stu-id="0bc66-112">Roles can only be assigned from within hello subscription, resource group, or resource that is hello scope for hello assignment.</span></span> <span data-ttu-id="0bc66-113">Ma è possibile visualizzare tutte le assegnazioni di hello accesso per un determinato utente o gruppo in un'unica posizione.</span><span class="sxs-lookup"><span data-stu-id="0bc66-113">But you can view all hello access assignments for a given user or group in a single place.</span></span> <span data-ttu-id="0bc66-114">È possibile disporre le assegnazioni di ruolo too2000 in ogni sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="0bc66-114">You can have up too2000 role assignments in each subscription.</span></span> 

<span data-ttu-id="0bc66-115">Ottenere altre informazioni su come troppo[utilizzare le risorse di sottoscrizione di Azure tooyour accesso toomanage assegnazioni ruolo](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="0bc66-115">Get more information about how too[Use role assignments toomanage access tooyour Azure subscription resources](role-based-access-control-configure.md).</span></span>

## <a name="view-access-assignments"></a><span data-ttu-id="0bc66-116">Visualizzare le assegnazioni di accesso</span><span class="sxs-lookup"><span data-stu-id="0bc66-116">View access assignments</span></span>
<span data-ttu-id="0bc66-117">toolook le assegnazioni di hello accesso per un singolo utente o gruppo, di avviare in Azure Active Directory hello [portale di Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0bc66-117">toolook up hello access assignments for a single user or group, start in Azure Active Directory in hello [Azure portal](http://portal.azure.com).</span></span>

1. <span data-ttu-id="0bc66-118">Selezionare **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0bc66-118">Select **Azure Active Directory**.</span></span> <span data-ttu-id="0bc66-119">Se questa opzione non è visibile nell'elenco di navigazione, selezionare **più servizi** e quindi scorrere verso il basso toofind **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0bc66-119">If this option is not visible on your navigation list, select **More Services** and then scroll down toofind **Azure Active Directory**.</span></span>
2. <span data-ttu-id="0bc66-120">Selezionare **Utenti e gruppi** e **Tutti gli utenti** o **Tutti i gruppi**.</span><span class="sxs-lookup"><span data-stu-id="0bc66-120">Select **Users and Groups**, and then either **All users** or **All groups**.</span></span> <span data-ttu-id="0bc66-121">Questo esempio si incentra sui singoli utenti.</span><span class="sxs-lookup"><span data-stu-id="0bc66-121">For this example, we focus on individual users.</span></span>
    <span data-ttu-id="0bc66-122">![Gestire utenti e gruppi in Azure Active Directory - Schermata](./media/role-based-access-control-manage-assignments/rbac_users_groups.png)</span><span class="sxs-lookup"><span data-stu-id="0bc66-122">![Manage users and groups in Azure Active Directory - screenshot](./media/role-based-access-control-manage-assignments/rbac_users_groups.png)</span></span>
3. <span data-ttu-id="0bc66-123">Ricerca per utente hello in base al nome o il nome utente.</span><span class="sxs-lookup"><span data-stu-id="0bc66-123">Search for hello user by name or username.</span></span>
4. <span data-ttu-id="0bc66-124">Selezionare **risorse di Azure** nel pannello utente hello.</span><span class="sxs-lookup"><span data-stu-id="0bc66-124">Select **Azure resources** on hello user blade.</span></span> <span data-ttu-id="0bc66-125">Vengono visualizzate tutte le assegnazioni di accesso hello per tale utente.</span><span class="sxs-lookup"><span data-stu-id="0bc66-125">All hello access assignments for that user appear.</span></span>

### <a name="read-permissions-tooview-assignments"></a><span data-ttu-id="0bc66-126">Tooview assegnazioni delle autorizzazioni di lettura</span><span class="sxs-lookup"><span data-stu-id="0bc66-126">Read permissions tooview assignments</span></span>
<span data-ttu-id="0bc66-127">Questa pagina Mostra solo le assegnazioni di accesso hello di disporre dell'autorizzazione tooread.</span><span class="sxs-lookup"><span data-stu-id="0bc66-127">This page only shows hello access assignments that you have permission tooread.</span></span> <span data-ttu-id="0bc66-128">Ad esempio, si hanno accesso in lettura toosubscription A e passare toohello risorse di Azure blade toocheck assegnazioni dell'utente.</span><span class="sxs-lookup"><span data-stu-id="0bc66-128">For example, you have read access toosubscription A and go toohello Azure resources blade toocheck a user's assignments.</span></span> <span data-ttu-id="0bc66-129">Vengono visualizzate le assegnazioni di accesso per la sottoscrizione A, ma non sarà possibile vedere che l'utente dispone di assegnazioni di accesso per la sottoscrizione B.</span><span class="sxs-lookup"><span data-stu-id="0bc66-129">You can see her access assignments for subscription A, but can't see that she also has access assignments on subscription B.</span></span>

## <a name="delete-access-assignments"></a><span data-ttu-id="0bc66-130">Eliminare le assegnazioni di accesso</span><span class="sxs-lookup"><span data-stu-id="0bc66-130">Delete access assignments</span></span>
<span data-ttu-id="0bc66-131">Questo pannello, è possibile eliminare le assegnazioni di accesso che sono state assegnate direttamente tooa utente o gruppo.</span><span class="sxs-lookup"><span data-stu-id="0bc66-131">From this blade, you can delete access assignments that were assigned directly tooa user or group.</span></span> <span data-ttu-id="0bc66-132">Se l'assegnazione di accesso hello è stata ereditata da un gruppo padre, è necessario toogo toohello risorse o una sottoscrizione e gestire l'assegnazione di hello non esiste.</span><span class="sxs-lookup"><span data-stu-id="0bc66-132">If hello access assignment was inherited from a parent group, you need toogo toohello resource or subscription and manage hello assignment there.</span></span>

1. <span data-ttu-id="0bc66-133">Selezionare hello uno desiderato toodelete hello elenco di tutte le assegnazioni di hello accesso per un utente o gruppo.</span><span class="sxs-lookup"><span data-stu-id="0bc66-133">From hello list of all hello access assignments for a user or group, select hello one you want toodelete.</span></span>
2. <span data-ttu-id="0bc66-134">Selezionare **rimuovere** e quindi **Sì** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="0bc66-134">Select **Remove** and then **Yes** tooconfirm.</span></span>
    <span data-ttu-id="0bc66-135">![Rimuovere un'assegnazione di accesso - Schermata](./media/role-based-access-control-manage-assignments/delete_assignment.png)</span><span class="sxs-lookup"><span data-stu-id="0bc66-135">![Remove access assignment - screenshot](./media/role-based-access-control-manage-assignments/delete_assignment.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="0bc66-136">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0bc66-136">Next steps</span></span>

* <span data-ttu-id="0bc66-137">Introduzione a controllo di accesso basato sui ruoli troppo[utilizzare le risorse di sottoscrizione di Azure tooyour accesso toomanage assegnazioni ruolo](role-based-access-control-configure.md)</span><span class="sxs-lookup"><span data-stu-id="0bc66-137">Get started with Role-Based Access Control too[Use role assignments toomanage access tooyour Azure subscription resources](role-based-access-control-configure.md)</span></span>
* <span data-ttu-id="0bc66-138">Vedere hello [ruoli predefiniti RBAC](role-based-access-built-in-roles.md)</span><span class="sxs-lookup"><span data-stu-id="0bc66-138">See hello [RBAC built-in roles](role-based-access-built-in-roles.md)</span></span>

