---
title: Caratteristiche dell'interazione dei tenant di Azure Active Directory | Microsoft Docs
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
ms.openlocfilehash: d25d2c731034d0785bbd404ec693c4c41d913d01
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="understand-how-multiple-azure-active-directory-tenants-interact"></a><span data-ttu-id="18802-103">Informazioni sull'interazione di più tenant di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="18802-103">Understand how multiple Azure Active Directory tenants interact</span></span>

<span data-ttu-id="18802-104">In Azure Active Directory (Azure AD) ogni tenant è una risorsa totalmente indipendente, ovvero un peer logicamente indipendente dagli altri tenant gestiti.</span><span class="sxs-lookup"><span data-stu-id="18802-104">In Azure Active Directory (Azure AD), each tenent is a fully independent resource: a peer that is logically independent from the other tenants that you manage.</span></span> <span data-ttu-id="18802-105">Tra i tenant non esiste alcuna relazione padre-figlio.</span><span class="sxs-lookup"><span data-stu-id="18802-105">There is no parent-child relationship between tenants.</span></span> <span data-ttu-id="18802-106">Questa indipendenza tra i tenant include l'indipendenza delle risorse, l'indipendenza amministrativa e l'indipendenza della sincronizzazione.</span><span class="sxs-lookup"><span data-stu-id="18802-106">This independence between tenants includes resource independence, administrative independence, and synchronization independence.</span></span>

## <a name="resource-independence"></a><span data-ttu-id="18802-107">Indipendenza delle risorse.</span><span class="sxs-lookup"><span data-stu-id="18802-107">Resource independence</span></span>
* <span data-ttu-id="18802-108">Se si crea o si elimina una risorsa in un tenant, ciò non influisce sulle risorse contenute in un altro tenant, con l'eccezione parziale degli utenti esterni.</span><span class="sxs-lookup"><span data-stu-id="18802-108">If you create or delete a resource in one tenant, it has no impact on any resource in another tenant, with the partial exception of external users.</span></span> 
* <span data-ttu-id="18802-109">Se si usa uno dei nomi di dominio con un tenant, questo non potrà essere usato con altri tenant.</span><span class="sxs-lookup"><span data-stu-id="18802-109">If you use one of your domain names with one tenant, it cannot be used with any other tenant.</span></span>

## <a name="administrative-independence"></a><span data-ttu-id="18802-110">Indipendenza amministrativa</span><span class="sxs-lookup"><span data-stu-id="18802-110">Administrative independence</span></span>
<span data-ttu-id="18802-111">Se un utente non amministratore del tenant "Contoso" crea un tenant di test denominato "Test", si verifica quanto segue:</span><span class="sxs-lookup"><span data-stu-id="18802-111">If a non-administrative user of tenant 'Contoso' creates a test tenant 'Test,' then:</span></span>

* <span data-ttu-id="18802-112">Per impostazione predefinita, l'utente che crea un tenant viene aggiunto come utente esterno nel nuovo tenant e gli viene assegnato il ruolo di amministratore globale in quel tenant.</span><span class="sxs-lookup"><span data-stu-id="18802-112">By default, the user who creates a tenant is added as an external user in that new tenant, and assigned the global administrator role in that tenant.</span></span>
* <span data-ttu-id="18802-113">Gli amministratori del tenant "Contoso" non dispongono di privilegi amministrativi diretti per il tenant "Test", a meno che questi privilegi non vengano specificamente concessi da un amministratore di "Test".</span><span class="sxs-lookup"><span data-stu-id="18802-113">The administrators of tenant 'Contoso' have no direct administrative privileges to tenant 'Test,' unless an administrator of 'Test' specifically grants them these privileges.</span></span> <span data-ttu-id="18802-114">Gli amministratori di "Contoso" possono tuttavia controllare l'accesso al tenant "Test" se controllano l'account utente che ha creato "Test".</span><span class="sxs-lookup"><span data-stu-id="18802-114">However, administrators of 'Contoso' can control access to tenant 'Test' if they control the user account that created 'Test.'</span></span>
* <span data-ttu-id="18802-115">Se si aggiunge o si rimuove un ruolo di amministratore per un utente in un tenant, la modifica non influisce sui ruoli di amministratore che l'utente può avere in un altro tenant.</span><span class="sxs-lookup"><span data-stu-id="18802-115">If you add/remove an administrator role for a user in one tenant, the change does not affect the administrator roles that the user has in another tenant.</span></span>

## <a name="synchronization-independence"></a><span data-ttu-id="18802-116">Indipendenza della sincronizzazione</span><span class="sxs-lookup"><span data-stu-id="18802-116">Synchronization independence</span></span>
<span data-ttu-id="18802-117">È possibile configurare ogni tenant di Azure AD in modo indipendente per sincronizzare i dati da una singola istanza di uno degli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="18802-117">You can configure each Azure AD tenant independently to get data synchronized from a single instance of either:</span></span>

* <span data-ttu-id="18802-118">Strumento Azure AD Connect, per sincronizzare i dati con una singola foresta AD.</span><span class="sxs-lookup"><span data-stu-id="18802-118">The Azure AD Connect tool, to synchronize data with a single AD forest.</span></span>
* <span data-ttu-id="18802-119">Connettore dei tenant di Azure Active Directory per Forefront Identity Manager, per sincronizzare i dati con una o più foreste locali e/o origini dati non Azure AD.</span><span class="sxs-lookup"><span data-stu-id="18802-119">The Azure Active tenant Connector for Forefront Identity Manager, to synchronize data with one or more on-premises forests, and/or non-Azure AD data sources.</span></span>

## <a name="add-an-azure-ad-tenant"></a><span data-ttu-id="18802-120">Aggiungere un tenant di Azure AD</span><span class="sxs-lookup"><span data-stu-id="18802-120">Add an Azure AD tenant</span></span>
<span data-ttu-id="18802-121">Per aggiungere un tenant di Azure AD nel portale di Azure, accedere al [portale di Azure](https://portal.azure.com) con un account amministratore globale per Azure AD e selezionare **Nuovo** a sinistra.</span><span class="sxs-lookup"><span data-stu-id="18802-121">To add an Azure AD tenant in the Azure portal, sign in to [the Azure portal](https://portal.azure.com) with an account that is an Azure AD global administrator, and, on the left, select **New**.</span></span>

> [!NOTE]
> <span data-ttu-id="18802-122">A differenza di altre risorse di Azure, i tenant non sono risorse figlio di una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="18802-122">Unlike other Azure resources, your tenants are not child resources of an Azure subscription.</span></span> <span data-ttu-id="18802-123">Se si annulla o si lascia scadere la sottoscrizione di Azure, sarà comunque possibile accedere ai dati del tenant tramite Azure PowerShell, l'API Graph di Azure o l'interfaccia di amministrazione di Office 365.</span><span class="sxs-lookup"><span data-stu-id="18802-123">If your Azure subscription is canceled or expired, you can still access your tenant data using Azure PowerShell, the Azure Graph API, or the Office 365 Admin Center.</span></span> <span data-ttu-id="18802-124">È anche possibile associare un'altra sottoscrizione al tenant.</span><span class="sxs-lookup"><span data-stu-id="18802-124">You can also associate another subscription with the tenant.</span></span>
>

## <a name="next-steps"></a><span data-ttu-id="18802-125">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="18802-125">Next steps</span></span>
<span data-ttu-id="18802-126">Per un'ampia panoramica dei problemi relativi alle licenze di Azure AD e le procedure consigliate, vedere [Informazioni sulle licenze dei tenant di Azure Active Directory](active-directory-licensing-whatis-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="18802-126">For a broad overview of Azure AD licensing issues and best practices, see [What is Azure Active tenant licensing?](active-directory-licensing-whatis-azure-portal.md)</span></span>
