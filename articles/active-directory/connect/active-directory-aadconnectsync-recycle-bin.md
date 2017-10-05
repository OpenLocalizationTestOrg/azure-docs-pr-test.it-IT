---
title: 'Servizio di sincronizzazione Azure AD Connect: abilitare il Cestino di Active Directory | Microsoft Docs'
description: "Questo argomento consiglia l'utilizzo della funzionalità Cestino di Active Directory con Azure AD Connect."
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
ms.openlocfilehash: eb455477547f3db8245cf3601576eba9c6fdc56f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-sync-enable-ad-recycle-bin"></a><span data-ttu-id="8fa4c-104">Servizio di sincronizzazione Azure AD Connect: abilitare il Cestino di Active Directory</span><span class="sxs-lookup"><span data-stu-id="8fa4c-104">Azure AD Connect sync: Enable AD recycle bin</span></span>
<span data-ttu-id="8fa4c-105">È consigliabile abilitare la funzionalità Cestino di Active Directory per le Active Directory locali che vengono sincronizzate con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8fa4c-105">It is recommended that you enable the AD Recycle Bin feature for your on-premises Active Directories, which are synchronized to Azure AD.</span></span> 

<span data-ttu-id="8fa4c-106">Se si elimina accidentalmente un oggetto utente di AD locale e lo si ripristina usando la funzionalità, Azure AD ripristina l'oggetto utente Azure AD corrispondente.</span><span class="sxs-lookup"><span data-stu-id="8fa4c-106">If you accidentally deleted an on-premises AD user object and restore it using the feature, Azure AD restores the corresponding Azure AD user object.</span></span>  <span data-ttu-id="8fa4c-107">Per informazioni sulla funzionalità Cestino di Active Directory, fare riferimento all'articolo [Scenario Overview for Restoring Deleted Active Directory Objects (Panoramica sullo scenario per il ripristino di oggetti di Active Directory eliminati)](https://technet.microsoft.com/library/dd379542.aspx).</span><span class="sxs-lookup"><span data-stu-id="8fa4c-107">For information about the AD Recycle Bin feature, refer to article [Scenario Overview for Restoring Deleted Active Directory Objects](https://technet.microsoft.com/library/dd379542.aspx).</span></span>

## <a name="benefits-of-enabling-the-ad-recycle-bin"></a><span data-ttu-id="8fa4c-108">Vantaggi dell'abilitazione del Cestino di Active Directory</span><span class="sxs-lookup"><span data-stu-id="8fa4c-108">Benefits of enabling the AD recycle bin</span></span>
<span data-ttu-id="8fa4c-109">Questa funzionalità consente di ripristinare gli oggetti utente di Azure AD effettuando le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="8fa4c-109">This feature helps with restoring Azure AD user objects by doing the following:</span></span>

* <span data-ttu-id="8fa4c-110">Se si elimina accidentalmente un oggetto utente di AD locale, l’oggetto utente di Azure AD corrispondente verrà eliminato nel ciclo di sincronizzazione successivo.</span><span class="sxs-lookup"><span data-stu-id="8fa4c-110">If you accidentally deleted an on-premises AD user object, the corresponding Azure AD user object will be deleted in the next sync cycle.</span></span> <span data-ttu-id="8fa4c-111">Per impostazione predefinita, Azure AD mantiene per 30 giorni l'oggetto utente di Azure AD eliminato in uno stato di eliminazione temporanea.</span><span class="sxs-lookup"><span data-stu-id="8fa4c-111">By default, Azure AD keeps the deleted Azure AD user object in soft-deleted state for 30 days.</span></span>

* <span data-ttu-id="8fa4c-112">Se la funzionalità Cestino di Active Directory locale è abilitata, è possibile ripristinare l'oggetto utente di AD locale eliminato senza modificarne il valore di ancoraggio di origine.</span><span class="sxs-lookup"><span data-stu-id="8fa4c-112">If you have on-premises AD Recycle Bin feature enabled, you can restore the deleted on-premises AD user object without changing its Source Anchor value.</span></span> <span data-ttu-id="8fa4c-113">Quando l’oggetto utente di AD locale ripristinato viene sincronizzato con Azure AD, quest’ultimo ripristinerà il corrispondente oggetto utente di Azure AD che si trova nello stato di eliminazione temporanea.</span><span class="sxs-lookup"><span data-stu-id="8fa4c-113">When the recovered on-premises AD user object is synchronized to Azure AD, Azure AD will restore the corresponding soft-deleted Azure AD user object.</span></span> <span data-ttu-id="8fa4c-114">Per informazioni sull'attributo di ancoraggio di origine, fare riferimento all'articolo [Azure AD Connect: Concetti relativi alla progettazione](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-design-concepts#sourceanchor).</span><span class="sxs-lookup"><span data-stu-id="8fa4c-114">For information about Source Anchor attribute, refer to article [Azure AD Connect: Design concepts](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-design-concepts#sourceanchor).</span></span>

* <span data-ttu-id="8fa4c-115">Se la funzionalità Cestino di Active Directory locale non è abilitata, potrebbe essere necessario creare un oggetto utente AD per sostituire l'oggetto eliminato.</span><span class="sxs-lookup"><span data-stu-id="8fa4c-115">If you do not have on-premises AD Recycle Bin feature enabled, you may be required to create an AD user object to replace the deleted object.</span></span> <span data-ttu-id="8fa4c-116">Se il servizio di sincronizzazione di Azure AD Connect è configurato per usare l'attributo di AD generato dal sistema (ad esempio ObjectGuid) per l'attributo di ancoraggio di origine, l'oggetto utente di AD appena creato non avrà lo stesso valore di ancoraggio di origine dell'oggetto utente di AD eliminato.</span><span class="sxs-lookup"><span data-stu-id="8fa4c-116">If Azure AD Connect Synchronization Service is configured to use system-generated AD attribute (such as ObjectGuid) for the Source Anchor attribute, the newly created AD user object will not have the same Source Anchor value as the deleted AD user object.</span></span> <span data-ttu-id="8fa4c-117">Quando l'oggetto utente di AD appena creato viene sincronizzato con Azure AD, quest’ultimo crea un nuovo oggetto utente di Azure AD anziché ripristinare l'oggetto utente di Azure AD in stato di eliminazione temporanea.</span><span class="sxs-lookup"><span data-stu-id="8fa4c-117">When the newly created AD user object is synchronized to Azure AD, Azure AD creates a new Azure AD user object instead of restoring the soft-deleted Azure AD user object.</span></span>

> [!NOTE]
> <span data-ttu-id="8fa4c-118">Per impostazione predefinita, Azure AD mantiene gli oggetti utente di Azure AD in uno stato di eliminazione temporanea per 30 giorni, prima che vengano eliminati definitivamente.</span><span class="sxs-lookup"><span data-stu-id="8fa4c-118">By default, Azure AD keeps deleted Azure AD user objects in soft-deleted state for 30 days before they are permanently deleted.</span></span> <span data-ttu-id="8fa4c-119">Tuttavia, gli amministratori possono accelerare l'eliminazione di tali oggetti.</span><span class="sxs-lookup"><span data-stu-id="8fa4c-119">However, administrators can accelerate the deletion of such objects.</span></span> <span data-ttu-id="8fa4c-120">Dopo che gli oggetti sono stati eliminati in modo permanente, non possono più essere ripristinati, anche se è abilitata la funzionalità Cestino di Active Directory locale.</span><span class="sxs-lookup"><span data-stu-id="8fa4c-120">Once the objects are permanently deleted, they can no longer be recovered, even if on-premises AD Recycle Bin feature is enabled.</span></span>



## <a name="next-steps"></a><span data-ttu-id="8fa4c-121">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8fa4c-121">Next steps</span></span>
<span data-ttu-id="8fa4c-122">**Argomenti generali**</span><span class="sxs-lookup"><span data-stu-id="8fa4c-122">**Overview topics**</span></span>

* [<span data-ttu-id="8fa4c-123">Servizio di sincronizzazione Azure AD Connect: Comprendere e personalizzare la sincronizzazione</span><span class="sxs-lookup"><span data-stu-id="8fa4c-123">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)

* [<span data-ttu-id="8fa4c-124">Integrazione delle identità locali con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8fa4c-124">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
