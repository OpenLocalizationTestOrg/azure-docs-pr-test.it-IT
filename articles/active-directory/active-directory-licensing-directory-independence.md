---
title: aaaCharacteristics di Azure Active Directory del tenant intercaction | Documenti Microsoft
description: Gestire i tenant di Azure Active Directory considerando i tenant come risorse completamente indipendenti
services: active-tenant
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 2b862b75-14df-45f2-a8ab-2a3ff1e2eb08
ms.service: active-tenant
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/27/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017;it-pro
ms.reviewer: piotrci
ms.openlocfilehash: 57b677665c7cb4aee63f518c39d26754fe71a999
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="understand-how-multiple-azure-active-directory-tenants-interact"></a><span data-ttu-id="f3f2f-103">Informazioni sull'interazione di più tenant di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f3f2f-103">Understand how multiple Azure Active Directory tenants interact</span></span>

<span data-ttu-id="f3f2f-104">In Azure Active Directory (Azure AD), ogni tenant è una risorsa totalmente indipendente: hello di un peer logicamente indipendente da altri tenant gestiti.</span><span class="sxs-lookup"><span data-stu-id="f3f2f-104">In Azure Active Directory (Azure AD), each tenent is a fully independent resource: a peer that is logically independent from hello other tenants that you manage.</span></span> <span data-ttu-id="f3f2f-105">Tra i tenant non esiste alcuna relazione padre-figlio.</span><span class="sxs-lookup"><span data-stu-id="f3f2f-105">There is no parent-child relationship between tenants.</span></span> <span data-ttu-id="f3f2f-106">Questa indipendenza tra i tenant include l'indipendenza delle risorse, l'indipendenza amministrativa e l'indipendenza della sincronizzazione.</span><span class="sxs-lookup"><span data-stu-id="f3f2f-106">This independence between tenants includes resource independence, administrative independence, and synchronization independence.</span></span>

## <a name="resource-independence"></a><span data-ttu-id="f3f2f-107">Indipendenza delle risorse.</span><span class="sxs-lookup"><span data-stu-id="f3f2f-107">Resource independence</span></span>
* <span data-ttu-id="f3f2f-108">Se si crea o si elimina una risorsa in un unico tenant, ha alcun impatto sulle risorse in un altro tenant, con l'eccezione parziale di hello di utenti esterni.</span><span class="sxs-lookup"><span data-stu-id="f3f2f-108">If you create or delete a resource in one tenant, it has no impact on any resource in another tenant, with hello partial exception of external users.</span></span> 
* <span data-ttu-id="f3f2f-109">Se si usa uno dei nomi di dominio con un tenant, questo non potrà essere usato con altri tenant.</span><span class="sxs-lookup"><span data-stu-id="f3f2f-109">If you use one of your domain names with one tenant, it cannot be used with any other tenant.</span></span>

## <a name="administrative-independence"></a><span data-ttu-id="f3f2f-110">Indipendenza amministrativa</span><span class="sxs-lookup"><span data-stu-id="f3f2f-110">Administrative independence</span></span>
<span data-ttu-id="f3f2f-111">Se un utente non amministratore del tenant "Contoso" crea un tenant di test denominato "Test", si verifica quanto segue:</span><span class="sxs-lookup"><span data-stu-id="f3f2f-111">If a non-administrative user of tenant 'Contoso' creates a test tenant 'Test,' then:</span></span>

* <span data-ttu-id="f3f2f-112">Per impostazione predefinita, gli utenti hello crea un tenant viene aggiunto come utente esterno di tale nuovo tenant e il ruolo di amministratore globale hello assegnato nel tenant.</span><span class="sxs-lookup"><span data-stu-id="f3f2f-112">By default, hello user who creates a tenant is added as an external user in that new tenant, and assigned hello global administrator role in that tenant.</span></span>
* <span data-ttu-id="f3f2f-113">gli amministratori di Hello del tenant 'Contoso' non possono tootenant di privilegi amministrativi diretti 'Test', a meno che un amministratore di "Test" vengono loro concessi specificamente questi privilegi.</span><span class="sxs-lookup"><span data-stu-id="f3f2f-113">hello administrators of tenant 'Contoso' have no direct administrative privileges tootenant 'Test,' unless an administrator of 'Test' specifically grants them these privileges.</span></span> <span data-ttu-id="f3f2f-114">Tuttavia, gli amministratori di 'Contoso' possono controllare accesso tootenant 'Test' Se si ha il controllo account utente di hello creato 'Test'.</span><span class="sxs-lookup"><span data-stu-id="f3f2f-114">However, administrators of 'Contoso' can control access tootenant 'Test' if they control hello user account that created 'Test.'</span></span>
* <span data-ttu-id="f3f2f-115">Se si installazione un ruolo di amministratore per un utente in un unico tenant, modifica hello non non interessano hello i ruoli di amministratore che hello utente dispone di un altro tenant.</span><span class="sxs-lookup"><span data-stu-id="f3f2f-115">If you add/remove an administrator role for a user in one tenant, hello change does not affect hello administrator roles that hello user has in another tenant.</span></span>

## <a name="synchronization-independence"></a><span data-ttu-id="f3f2f-116">Indipendenza della sincronizzazione</span><span class="sxs-lookup"><span data-stu-id="f3f2f-116">Synchronization independence</span></span>
<span data-ttu-id="f3f2f-117">È possibile configurare ogni Azure Active Directory del tenant in modo indipendente tooget sincronizzare i dati da una singola istanza di uno:</span><span class="sxs-lookup"><span data-stu-id="f3f2f-117">You can configure each Azure AD tenant independently tooget data synchronized from a single instance of either:</span></span>

* <span data-ttu-id="f3f2f-118">strumento di Hello Azure AD Connect, toosynchronize dati con una singola foresta di Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f3f2f-118">hello Azure AD Connect tool, toosynchronize data with a single AD forest.</span></span>
* <span data-ttu-id="f3f2f-119">Hello tenant Azure Active Connector per Forefront Identity Manager, toosynchronize dati con uno o più in locale gli insiemi di strutture e/o le origini dati diverse da Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f3f2f-119">hello Azure Active tenant Connector for Forefront Identity Manager, toosynchronize data with one or more on-premises forests, and/or non-Azure AD data sources.</span></span>

## <a name="add-an-azure-ad-tenant"></a><span data-ttu-id="f3f2f-120">Aggiungere un tenant di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f3f2f-120">Add an Azure AD tenant</span></span>
<span data-ttu-id="f3f2f-121">un tenant di Azure AD nel portale di Azure hello tooadd Accedi troppo[hello Azure portal](https://portal.azure.com) con un account di amministratore globale di Azure AD e, a sinistra di hello, selezionare **New**.</span><span class="sxs-lookup"><span data-stu-id="f3f2f-121">tooadd an Azure AD tenant in hello Azure portal, sign in too[hello Azure portal](https://portal.azure.com) with an account that is an Azure AD global administrator, and, on hello left, select **New**.</span></span>

> [!NOTE]
> <span data-ttu-id="f3f2f-122">A differenza di altre risorse di Azure, i tenant non sono risorse figlio di una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="f3f2f-122">Unlike other Azure resources, your tenants are not child resources of an Azure subscription.</span></span> <span data-ttu-id="f3f2f-123">Se la sottoscrizione di Azure viene annullata o è scaduta, è comunque possibile accedere ai dati di tenant usando Azure PowerShell, hello API Graph di Azure o centro di amministrazione di hello Office 365.</span><span class="sxs-lookup"><span data-stu-id="f3f2f-123">If your Azure subscription is canceled or expired, you can still access your tenant data using Azure PowerShell, hello Azure Graph API, or hello Office 365 Admin Center.</span></span> <span data-ttu-id="f3f2f-124">È anche possibile associare un'altra sottoscrizione tenant hello.</span><span class="sxs-lookup"><span data-stu-id="f3f2f-124">You can also associate another subscription with hello tenant.</span></span>
>

## <a name="next-steps"></a><span data-ttu-id="f3f2f-125">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f3f2f-125">Next steps</span></span>
<span data-ttu-id="f3f2f-126">Per un'ampia panoramica dei problemi relativi alle licenze di Azure AD e le procedure consigliate, vedere [Informazioni sulle licenze dei tenant di Azure Active Directory](active-directory-licensing-whatis-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="f3f2f-126">For a broad overview of Azure AD licensing issues and best practices, see [What is Azure Active tenant licensing?](active-directory-licensing-whatis-azure-portal.md)</span></span>
