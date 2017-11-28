---
title: 'Servizio di sincronizzazione Azure AD Connect: abilitare il Cestino di Active Directory | Microsoft Docs'
description: "In questo argomento consiglia di utilizzare hello della funzionalità del Cestino di Active Directory con Azure AD Connect."
services: active-directory
keywords: Cestino di Active Directory, eliminazione accidentale, ancoraggio di origine
documentationcenter: 
author: cychua
manager: femila
editor: 
ms.assetid: afec4207-74f7-4cdd-b13a-574af5223a90
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 2bb4827d677ccecfd8d2861f2a2fcf73b8cc2d95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-enable-ad-recycle-bin"></a><span data-ttu-id="52bdb-104">Servizio di sincronizzazione Azure AD Connect: abilitare il Cestino di Active Directory</span><span class="sxs-lookup"><span data-stu-id="52bdb-104">Azure AD Connect sync: Enable AD recycle bin</span></span>
<span data-ttu-id="52bdb-105">È consigliabile abilitare funzionalità Cestino per Active Directory hello per le in Active Directory locali, che sono sincronizzati tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="52bdb-105">It is recommended that you enable hello AD Recycle Bin feature for your on-premises Active Directories, which are synchronized tooAzure AD.</span></span> 

<span data-ttu-id="52bdb-106">Se è stato eliminato accidentalmente una locale oggetto utente di Active Directory e il ripristino utilizzando funzionalità hello, Azure AD Ripristina oggetto utente di Azure AD corrispondente hello.</span><span class="sxs-lookup"><span data-stu-id="52bdb-106">If you accidentally deleted an on-premises AD user object and restore it using hello feature, Azure AD restores hello corresponding Azure AD user object.</span></span>  <span data-ttu-id="52bdb-107">Per informazioni sulla funzionalità del Cestino hello Active Directory, vedere tooarticle [panoramica dello Scenario per il ripristino di oggetti Active Directory eliminati](https://technet.microsoft.com/library/dd379542.aspx).</span><span class="sxs-lookup"><span data-stu-id="52bdb-107">For information about hello AD Recycle Bin feature, refer tooarticle [Scenario Overview for Restoring Deleted Active Directory Objects](https://technet.microsoft.com/library/dd379542.aspx).</span></span>

## <a name="benefits-of-enabling-hello-ad-recycle-bin"></a><span data-ttu-id="52bdb-108">Vantaggi dell'abilitazione hello AD Cestino</span><span class="sxs-lookup"><span data-stu-id="52bdb-108">Benefits of enabling hello AD recycle bin</span></span>
<span data-ttu-id="52bdb-109">Questa funzionalità consente di con il ripristino di oggetti utente di Azure AD effettuando hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="52bdb-109">This feature helps with restoring Azure AD user objects by doing hello following:</span></span>

* <span data-ttu-id="52bdb-110">Se è stato eliminato accidentalmente una locale dell'oggetto utente di Active Directory, hello corrispondente oggetto utente di Azure AD verrà eliminato in hello successivo ciclo di sincronizzazione.</span><span class="sxs-lookup"><span data-stu-id="52bdb-110">If you accidentally deleted an on-premises AD user object, hello corresponding Azure AD user object will be deleted in hello next sync cycle.</span></span> <span data-ttu-id="52bdb-111">Per impostazione predefinita, Azure AD mantiene oggetto utente di Azure AD hello eliminato eliminato per 30 giorni.</span><span class="sxs-lookup"><span data-stu-id="52bdb-111">By default, Azure AD keeps hello deleted Azure AD user object in soft-deleted state for 30 days.</span></span>

* <span data-ttu-id="52bdb-112">Se si dispone di on-premise funzionalità Cestino per Active Directory è abilitata, è possibile ripristinare hello eliminato oggetto utente di Active Directory in locale senza modificarne il valore di ancoraggio di origine.</span><span class="sxs-lookup"><span data-stu-id="52bdb-112">If you have on-premises AD Recycle Bin feature enabled, you can restore hello deleted on-premises AD user object without changing its Source Anchor value.</span></span> <span data-ttu-id="52bdb-113">Quando hello recuperato locale viene sincronizzato l'oggetto utente di Active Directory tooAzure AD, Azure AD verrà ripristinato hello corrispondente eliminato oggetto utente Azure AD.</span><span class="sxs-lookup"><span data-stu-id="52bdb-113">When hello recovered on-premises AD user object is synchronized tooAzure AD, Azure AD will restore hello corresponding soft-deleted Azure AD user object.</span></span> <span data-ttu-id="52bdb-114">Per informazioni sull'attributo di ancoraggio di origine, fare riferimento tooarticle [Azure AD Connect: concetti di progettazione](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-design-concepts#sourceanchor).</span><span class="sxs-lookup"><span data-stu-id="52bdb-114">For information about Source Anchor attribute, refer tooarticle [Azure AD Connect: Design concepts](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-design-concepts#sourceanchor).</span></span>

* <span data-ttu-id="52bdb-115">Se non si dispone di on-premise Cestino di Active Directory abilitata la funzionalità Cestino, potrebbe essere richiesto toocreate un oggetto Active Directory utente oggetto tooreplace hello eliminato.</span><span class="sxs-lookup"><span data-stu-id="52bdb-115">If you do not have on-premises AD Recycle Bin feature enabled, you may be required toocreate an AD user object tooreplace hello deleted object.</span></span> <span data-ttu-id="52bdb-116">Se servizio di sincronizzazione di Azure AD Connect è configurato toouse generato dal sistema attributo di Active Directory (ad esempio ObjectGuid) per l'attributo di ancoraggio di origine hello, hello oggetto utente di Active Directory appena creata verrà non hanno hello stesso valore di ancoraggio di origine come hello eliminato l'oggetto utente di Active Directory.</span><span class="sxs-lookup"><span data-stu-id="52bdb-116">If Azure AD Connect Synchronization Service is configured toouse system-generated AD attribute (such as ObjectGuid) for hello Source Anchor attribute, hello newly created AD user object will not have hello same Source Anchor value as hello deleted AD user object.</span></span> <span data-ttu-id="52bdb-117">Quando hello oggetto utente di Active Directory appena creata viene sincronizzato tooAzure AD, Azure AD crea un nuovo oggetto utente di Azure AD anziché ripristinare l'oggetto utente di Azure AD hello eliminato.</span><span class="sxs-lookup"><span data-stu-id="52bdb-117">When hello newly created AD user object is synchronized tooAzure AD, Azure AD creates a new Azure AD user object instead of restoring hello soft-deleted Azure AD user object.</span></span>

> [!NOTE]
> <span data-ttu-id="52bdb-118">Per impostazione predefinita, Azure AD mantiene gli oggetti utente di Azure AD in uno stato di eliminazione temporanea per 30 giorni, prima che vengano eliminati definitivamente.</span><span class="sxs-lookup"><span data-stu-id="52bdb-118">By default, Azure AD keeps deleted Azure AD user objects in soft-deleted state for 30 days before they are permanently deleted.</span></span> <span data-ttu-id="52bdb-119">Tuttavia, gli amministratori possono accelerare l'eliminazione di hello di tali oggetti.</span><span class="sxs-lookup"><span data-stu-id="52bdb-119">However, administrators can accelerate hello deletion of such objects.</span></span> <span data-ttu-id="52bdb-120">Una volta oggetti hello vengono eliminati definitivamente, non possono essere ripristinati, anche se locale è abilitata la funzionalità Cestino per Active Directory.</span><span class="sxs-lookup"><span data-stu-id="52bdb-120">Once hello objects are permanently deleted, they can no longer be recovered, even if on-premises AD Recycle Bin feature is enabled.</span></span>



## <a name="next-steps"></a><span data-ttu-id="52bdb-121">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="52bdb-121">Next steps</span></span>
<span data-ttu-id="52bdb-122">**Argomenti generali**</span><span class="sxs-lookup"><span data-stu-id="52bdb-122">**Overview topics**</span></span>

* [<span data-ttu-id="52bdb-123">Servizio di sincronizzazione Azure AD Connect: Comprendere e personalizzare la sincronizzazione</span><span class="sxs-lookup"><span data-stu-id="52bdb-123">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)

* [<span data-ttu-id="52bdb-124">Integrazione delle identità locali con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="52bdb-124">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
