---
title: Visualizzare le assegnazioni di accesso alle risorse di Azure | Microsoft Docs
description: Visualizzare e gestire tutte le assegnazioni di controllo degli accessi in base al ruolo per qualsiasi utente o gruppo nel portale di Azure
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
ms.openlocfilehash: 72c695d08bdf5de003d51ffb0768184e1e4d00ba
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="view-access-assignments-for-users-and-groups-in-the-azure-portal"></a><span data-ttu-id="d5104-103">Visualizzare le assegnazioni dell'accesso per utenti e gruppi nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="d5104-103">View access assignments for users and groups in the Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d5104-104">Gestire l'accesso per utente o gruppo</span><span class="sxs-lookup"><span data-stu-id="d5104-104">Manage access by user or group</span></span>](role-based-access-control-manage-assignments.md)
> * [<span data-ttu-id="d5104-105">Gestire l'accesso per risorsa</span><span class="sxs-lookup"><span data-stu-id="d5104-105">Manage access by resource</span></span>](role-based-access-control-configure.md)

<span data-ttu-id="d5104-106">Il controllo degli accessi in base al ruolo in Azure Active Directory (Azure AD) permette di gestire l'accesso alle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="d5104-106">With role-based access control (RBAC) in the Azure Active Directory (Azure AD), you can manage access to your Azure resources.</span></span> 

<span data-ttu-id="d5104-107">L'accesso assegnato tramite RBAC è granulare in quanto offre due modalità per limitare le autorizzazioni:</span><span class="sxs-lookup"><span data-stu-id="d5104-107">Access assigned with RBAC is fine-grained because there are two ways you can restrict the permissions:</span></span>

* <span data-ttu-id="d5104-108">**Ambito:** le assegnazioni di ruolo RBAC hanno un ambito riferito a una sottoscrizione, una risorsa o un gruppo di risorse specifici.</span><span class="sxs-lookup"><span data-stu-id="d5104-108">**Scope:** RBAC role assignments are scoped to a specific subscription, resource group, or resource.</span></span> <span data-ttu-id="d5104-109">Un utente al quale è stato concesso l'accesso a una singola risorsa non può accedere alle altre risorse nella stessa sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="d5104-109">A user given access to a single resource cannot access any other resources in the same subscription.</span></span>
* <span data-ttu-id="d5104-110">**Ruolo:** all'interno dell'ambito dell'assegnazione, l'accesso è ulteriormente limitato con l'assegnazione di un ruolo.</span><span class="sxs-lookup"><span data-stu-id="d5104-110">**Role:** Within the scope of the assignment, access is narrowed even further by assigning a role.</span></span> <span data-ttu-id="d5104-111">I ruoli possono essere di livello superiore, ad esempio quello di proprietario, o specifici, ad esempio quello di lettore di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="d5104-111">Roles can be high-level, like owner, or specific, like virtual machine reader.</span></span>

<span data-ttu-id="d5104-112">I ruoli possono essere assegnati solo all'interno della sottoscrizione, del gruppo di risorse o della risorsa che rientra nell'ambito dell'assegnazione.</span><span class="sxs-lookup"><span data-stu-id="d5104-112">Roles can only be assigned from within the subscription, resource group, or resource that is the scope for the assignment.</span></span> <span data-ttu-id="d5104-113">È tuttavia possibile visualizzare in un'unica posizione tutte le assegnazioni di accesso di un determinato utente o gruppo.</span><span class="sxs-lookup"><span data-stu-id="d5104-113">But you can view all the access assignments for a given user or group in a single place.</span></span> <span data-ttu-id="d5104-114">È possibile avere fino a 2000 assegnazioni di ruolo in ogni sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="d5104-114">You can have up to 2000 role assignments in each subscription.</span></span> 

<span data-ttu-id="d5104-115">Altre informazioni su come [Usare le assegnazioni di ruolo per gestire l'accesso alle risorse della sottoscrizione di Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="d5104-115">Get more information about how to [Use role assignments to manage access to your Azure subscription resources](role-based-access-control-configure.md).</span></span>

## <a name="view-access-assignments"></a><span data-ttu-id="d5104-116">Visualizzare le assegnazioni di accesso</span><span class="sxs-lookup"><span data-stu-id="d5104-116">View access assignments</span></span>
<span data-ttu-id="d5104-117">Per individuare le assegnazioni di accesso di un singolo utente o gruppo, avviare Azure Active Directory nel [portale di Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d5104-117">To look up the access assignments for a single user or group, start in Azure Active Directory in the [Azure portal](http://portal.azure.com).</span></span>

1. <span data-ttu-id="d5104-118">Selezionare **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d5104-118">Select **Azure Active Directory**.</span></span> <span data-ttu-id="d5104-119">Se questa opzione non è visibile nell'elenco di navigazione, selezionare **Altri servizi** e scorrere fino ad **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d5104-119">If this option is not visible on your navigation list, select **More Services** and then scroll down to find **Azure Active Directory**.</span></span>
2. <span data-ttu-id="d5104-120">Selezionare **Utenti e gruppi** e **Tutti gli utenti** o **Tutti i gruppi**.</span><span class="sxs-lookup"><span data-stu-id="d5104-120">Select **Users and Groups**, and then either **All users** or **All groups**.</span></span> <span data-ttu-id="d5104-121">Questo esempio si incentra sui singoli utenti.</span><span class="sxs-lookup"><span data-stu-id="d5104-121">For this example, we focus on individual users.</span></span>
    <span data-ttu-id="d5104-122">![Gestire utenti e gruppi in Azure Active Directory - Schermata](./media/role-based-access-control-manage-assignments/rbac_users_groups.png)</span><span class="sxs-lookup"><span data-stu-id="d5104-122">![Manage users and groups in Azure Active Directory - screenshot](./media/role-based-access-control-manage-assignments/rbac_users_groups.png)</span></span>
3. <span data-ttu-id="d5104-123">Cercare l'utente in base al nome o al nome utente.</span><span class="sxs-lookup"><span data-stu-id="d5104-123">Search for the user by name or username.</span></span>
4. <span data-ttu-id="d5104-124">Selezionare **Risorse di Azure** nel pannello dell'utente.</span><span class="sxs-lookup"><span data-stu-id="d5104-124">Select **Azure resources** on the user blade.</span></span> <span data-ttu-id="d5104-125">Vengono visualizzate tutte le assegnazioni di accesso dell'utente.</span><span class="sxs-lookup"><span data-stu-id="d5104-125">All the access assignments for that user appear.</span></span>

### <a name="read-permissions-to-view-assignments"></a><span data-ttu-id="d5104-126">Autorizzazioni di lettura per la visualizzazione delle assegnazioni</span><span class="sxs-lookup"><span data-stu-id="d5104-126">Read permissions to view assignments</span></span>
<span data-ttu-id="d5104-127">Questa pagina mostra solo le assegnazioni di accesso per le quali si dispone dell'autorizzazione di lettura.</span><span class="sxs-lookup"><span data-stu-id="d5104-127">This page only shows the access assignments that you have permission to read.</span></span> <span data-ttu-id="d5104-128">Ad esempio, si ha accesso in lettura alla sottoscrizione A e si apre il pannello delle risorse di Azure per controllare le assegnazioni di un utente.</span><span class="sxs-lookup"><span data-stu-id="d5104-128">For example, you have read access to subscription A and go to the Azure resources blade to check a user's assignments.</span></span> <span data-ttu-id="d5104-129">Vengono visualizzate le assegnazioni di accesso per la sottoscrizione A, ma non sarà possibile vedere che l'utente dispone di assegnazioni di accesso per la sottoscrizione B.</span><span class="sxs-lookup"><span data-stu-id="d5104-129">You can see her access assignments for subscription A, but can't see that she also has access assignments on subscription B.</span></span>

## <a name="delete-access-assignments"></a><span data-ttu-id="d5104-130">Eliminare le assegnazioni di accesso</span><span class="sxs-lookup"><span data-stu-id="d5104-130">Delete access assignments</span></span>
<span data-ttu-id="d5104-131">Da questo pannello è possibile eliminare le assegnazioni di accesso assegnate direttamente a un utente o gruppo.</span><span class="sxs-lookup"><span data-stu-id="d5104-131">From this blade, you can delete access assignments that were assigned directly to a user or group.</span></span> <span data-ttu-id="d5104-132">Se l'assegnazione di accesso è stata ereditato da un gruppo padre, è necessario passare alla risorsa o alla sottoscrizione e gestire da qui l'assegnazione.</span><span class="sxs-lookup"><span data-stu-id="d5104-132">If the access assignment was inherited from a parent group, you need to go to the resource or subscription and manage the assignment there.</span></span>

1. <span data-ttu-id="d5104-133">Dall'elenco di tutte le assegnazioni di accesso di un utente o gruppo, selezionare quella da eliminare.</span><span class="sxs-lookup"><span data-stu-id="d5104-133">From the list of all the access assignments for a user or group, select the one you want to delete.</span></span>
2. <span data-ttu-id="d5104-134">Selezionare **Rimuovi** e **Sì** per confermare.</span><span class="sxs-lookup"><span data-stu-id="d5104-134">Select **Remove** and then **Yes** to confirm.</span></span>
    <span data-ttu-id="d5104-135">![Rimuovere un'assegnazione di accesso - Schermata](./media/role-based-access-control-manage-assignments/delete_assignment.png)</span><span class="sxs-lookup"><span data-stu-id="d5104-135">![Remove access assignment - screenshot](./media/role-based-access-control-manage-assignments/delete_assignment.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="d5104-136">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d5104-136">Next steps</span></span>

* <span data-ttu-id="d5104-137">Per un'introduzione al controllo degli accessi in base al ruolo, vedere [Usare le assegnazioni di ruolo per gestire l'accesso alle risorse della sottoscrizione di Azure](role-based-access-control-configure.md)</span><span class="sxs-lookup"><span data-stu-id="d5104-137">Get started with Role-Based Access Control to [Use role assignments to manage access to your Azure subscription resources](role-based-access-control-configure.md)</span></span>
* <span data-ttu-id="d5104-138">Vedere [Controllo degli accessi in base al ruolo: ruoli predefiniti](role-based-access-built-in-roles.md)</span><span class="sxs-lookup"><span data-stu-id="d5104-138">See the [RBAC built-in roles](role-based-access-built-in-roles.md)</span></span>

