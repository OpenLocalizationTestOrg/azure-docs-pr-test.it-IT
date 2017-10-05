---
title: Ripristinare un gruppo di Office 365 eliminato in Azure Active Directory | Microsoft Docs
description: Come ripristinare un gruppo eliminato, visualizzare i gruppi ripristinabili ed eliminare in modo permanente un gruppo in Azure Active Directory
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: cc5f232a-1e77-45c2-b28b-1fcb4621725c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: curtand
ms.openlocfilehash: 32d36ae96797a59bb47bf782ab038f21f231f046
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="restore-a-deleted-office-365-group-in-azure-active-directory"></a><span data-ttu-id="728ed-103">Ripristinare un gruppo di Office 365 eliminato in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="728ed-103">Restore a deleted Office 365 group in Azure Active Directory</span></span>

<span data-ttu-id="728ed-104">Quando si elimina un gruppo di Office 365 in Azure Active Directory (Azure AD), il gruppo eliminato viene conservato ma non è visibile per 30 giorni dalla data di eliminazione.</span><span class="sxs-lookup"><span data-stu-id="728ed-104">When you delete an Office 365 group in the Azure Active Directory (Azure AD), the deleted group is retained but not visible for 30 days from the deletion date.</span></span> <span data-ttu-id="728ed-105">In questo modo il gruppo e i relativi contenuti possono essere ripristinati se necessario.</span><span class="sxs-lookup"><span data-stu-id="728ed-105">This is so that the group and its contents can be restored if needed.</span></span> <span data-ttu-id="728ed-106">Questa funzionalità è limitata esclusivamente ai gruppi di Office 365 in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="728ed-106">This functionality is restricted exclusively to Office 365 groups in Azure AD.</span></span> <span data-ttu-id="728ed-107">Non è disponibile per i gruppi di sicurezza e i gruppi di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="728ed-107">It is not available for security groups and distribution groups.</span></span>

> [!NOTE] 
> <span data-ttu-id="728ed-108">Non usare `Remove-MsolGroup`, perché elimina definitivamente il gruppo.</span><span class="sxs-lookup"><span data-stu-id="728ed-108">Don't use `Remove-MsolGroup` because it purges the group permanently.</span></span> <span data-ttu-id="728ed-109">Usare sempre `Remove-AzureADMSGroup` per eliminare un gruppo di Office 365.</span><span class="sxs-lookup"><span data-stu-id="728ed-109">Always use `Remove-AzureADMSGroup` to delete an O365 group.</span></span> 

<span data-ttu-id="728ed-110">Per ripristinare un gruppo sono necessarie una delle autorizzazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="728ed-110">The permissions required to restore a group can be any of the following:</span></span>

<span data-ttu-id="728ed-111">Ruolo</span><span class="sxs-lookup"><span data-stu-id="728ed-111">Role</span></span>  | <span data-ttu-id="728ed-112">autorizzazioni</span><span class="sxs-lookup"><span data-stu-id="728ed-112">Permissions</span></span> 
--------- | ---------
<span data-ttu-id="728ed-113">Amministratore della società, supporto partner di livello 2 e amministratori del servizio di InTune</span><span class="sxs-lookup"><span data-stu-id="728ed-113">Company Administrator, Partner Tier2 support, and InTune Service Admins</span></span> | <span data-ttu-id="728ed-114">Possono ripristinare qualsiasi gruppo di Office 365 eliminato</span><span class="sxs-lookup"><span data-stu-id="728ed-114">Can restore any deleted Office 365 group</span></span> 
<span data-ttu-id="728ed-115">Amministratore dell'account utente e supporto partner di livello 1</span><span class="sxs-lookup"><span data-stu-id="728ed-115">User Account Administrator and Partner Tier1 support</span></span> | <span data-ttu-id="728ed-116">Possono ripristinare qualsiasi gruppo di Office 365 eliminato, ad eccezione di quelli assegnati al ruolo di amministratore della società</span><span class="sxs-lookup"><span data-stu-id="728ed-116">Can restore any deleted Office 365 group except those assigned to the Company Administrator role</span></span> 
<span data-ttu-id="728ed-117">Utente</span><span class="sxs-lookup"><span data-stu-id="728ed-117">User</span></span> | <span data-ttu-id="728ed-118">Possono ripristinare qualsiasi gruppo di Office 365 eliminato che era di loro proprietà</span><span class="sxs-lookup"><span data-stu-id="728ed-118">Can restore any deleted Office 365 group that they owned</span></span> 


## <a name="view-the-deleted-office-365-groups-that-are-available-to-restore"></a><span data-ttu-id="728ed-119">Visualizzare i gruppi di Office 365 eliminati che è possibile ripristinare</span><span class="sxs-lookup"><span data-stu-id="728ed-119">View the deleted Office 365 groups that are available to restore</span></span>
<span data-ttu-id="728ed-120">I cmdlet seguenti consente di visualizzare i gruppi eliminati per verificare che il gruppo o i gruppi a cui l'utente è interessato non siano stati ancora eliminati definitivamente.</span><span class="sxs-lookup"><span data-stu-id="728ed-120">The following cmdlets can be used to view the deleted groups to verify that the one or ones you're interested in have not yet been permanently purged.</span></span> <span data-ttu-id="728ed-121">Questi cmdlet fanno parte del modulo [PowerShell di Azure AD](https://www.powershellgallery.com/packages/AzureAD/).</span><span class="sxs-lookup"><span data-stu-id="728ed-121">These cmdlets are part of the [Azure AD PowerShell module](https://www.powershellgallery.com/packages/AzureAD/).</span></span> <span data-ttu-id="728ed-122">Altre informazioni su questo modulo sono reperibili nell'articolo [PowerShell di Azure Active Directory versione 2](/powershell/azure/install-adv2?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="728ed-122">More information about this module can be found in the [Azure Active Directory PowerShell Version 2](/powershell/azure/install-adv2?view=azureadps-2.0) article.</span></span>

1.  <span data-ttu-id="728ed-123">Eseguire il cmdlet seguente per visualizzare tutti i gruppi di Office 365 eliminati nel tenant per cui è ancora possibile il ripristino.</span><span class="sxs-lookup"><span data-stu-id="728ed-123">Run the following cmdlet to display all deleted Office 365 groups in your tenant that are still available to restore.</span></span>
  ```
  Get-AzureADMSDeletedGroup
  ```

2.  <span data-ttu-id="728ed-124">In alternativa, se si conosce l'objectID di un gruppo specifico (ed è possibile ottenerlo dal cmdlet nel passaggio 1), eseguire il cmdlet seguente per verificare che il gruppo eliminato specifico non sia stato ancora definitivamente eliminato.</span><span class="sxs-lookup"><span data-stu-id="728ed-124">Alternately, if you know the objectID of a specific group (and you can get it from the cmdlet in step 1), run the following cmdlet to verify that the specific deleted group has not yet been permanently purged.</span></span>
  ```
  Get-AzureADMSDeletedGroup –Id <objectId>
  ```



## <a name="how-to-restore-your-deleted-office-365-group"></a><span data-ttu-id="728ed-125">Come ripristinare il gruppo di Office 365 eliminato</span><span class="sxs-lookup"><span data-stu-id="728ed-125">How to restore your deleted Office 365 group</span></span>
<span data-ttu-id="728ed-126">Dopo avere verificato che è ancora possibile ripristinare il gruppo, ripristinare il gruppo eliminato con uno dei passaggi seguenti.</span><span class="sxs-lookup"><span data-stu-id="728ed-126">Once you have verified that the group is still available to restore, restore the deleted group with one of the following steps.</span></span> <span data-ttu-id="728ed-127">Se il gruppo contiene documenti, siti SP o altri oggetti persistenti, potrebbero volerci fino a 24 ore per ripristinare completamente un gruppo e il relativo contenuto.</span><span class="sxs-lookup"><span data-stu-id="728ed-127">If the group contains documents, SP sites, or other persistent objects, it might take up to 24 hours to fully restore a group and its contents.</span></span>

1.  <span data-ttu-id="728ed-128">Eseguire il cmdlet seguente per ripristinare il gruppo e il relativo contenuto.</span><span class="sxs-lookup"><span data-stu-id="728ed-128">Run the following cmdlet to restore the group and its contents.</span></span>
  
  ```
  Restore-AzureADMSDeletedDirectoryObject –Id <objectId>
  ``` 

<span data-ttu-id="728ed-129">In alternativa, è possibile eseguire il cmdlet seguente per rimuovere definitivamente il gruppo eliminato.</span><span class="sxs-lookup"><span data-stu-id="728ed-129">Alternatively, the following cmdlet can be run to permanently remove the deleted group.</span></span>
  ```
  Remove-AzureADMSDeletedDirectoryObject –Id <objectId>
  ```

## <a name="how-do-you-know-this-worked"></a><span data-ttu-id="728ed-130">Come si verifica che l'azione è riuscita?</span><span class="sxs-lookup"><span data-stu-id="728ed-130">How do you know this worked?</span></span>
<span data-ttu-id="728ed-131">Per verificare di aver ripristinato correttamente un gruppo di Office 365, eseguire il cmdlet `Get-AzureADGroup –ObjectId <objectId>` per visualizzare informazioni relative al gruppo.</span><span class="sxs-lookup"><span data-stu-id="728ed-131">To verify that you’ve successfully restored an Office 365 group, run the `Get-AzureADGroup –ObjectId <objectId>` cmdlet to display information about the group.</span></span> <span data-ttu-id="728ed-132">Al completamento della richiesta di ripristino:</span><span class="sxs-lookup"><span data-stu-id="728ed-132">After the restore request is completed:</span></span>
- <span data-ttu-id="728ed-133">Il gruppo verrà visualizzato nella barra di navigazione a sinistra su Exchange</span><span class="sxs-lookup"><span data-stu-id="728ed-133">The group will appear in the Left nav bar on Exchange</span></span>
- <span data-ttu-id="728ed-134">In Planner verrà visualizzato il piano per il gruppo</span><span class="sxs-lookup"><span data-stu-id="728ed-134">The plan for the group will appear in Planner</span></span>
- <span data-ttu-id="728ed-135">I siti di Sharepoint e tutti i contenuti saranno disponibili</span><span class="sxs-lookup"><span data-stu-id="728ed-135">Any Sharepoint sites and all of their contents will be available</span></span>
- <span data-ttu-id="728ed-136">È possibile accedere al gruppo da qualsiasi endpoint di Exchange e da altri carichi di lavoro di Office 365 che supportano i gruppi di Office 365</span><span class="sxs-lookup"><span data-stu-id="728ed-136">The group can be accessed from any of the Exchange endpoints and other Office 365 workloads that support Office 365 groups</span></span>


## <a name="next-steps"></a><span data-ttu-id="728ed-137">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="728ed-137">Next steps</span></span>
<span data-ttu-id="728ed-138">Questi articoli contengono informazioni aggiuntive sui gruppi di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="728ed-138">These articles provide additional information on Azure Active Directory groups.</span></span>

* [<span data-ttu-id="728ed-139">Vedere i gruppi esistenti</span><span class="sxs-lookup"><span data-stu-id="728ed-139">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="728ed-140">Gestire le impostazioni di un gruppo</span><span class="sxs-lookup"><span data-stu-id="728ed-140">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="728ed-141">Gestire i membri di un gruppo</span><span class="sxs-lookup"><span data-stu-id="728ed-141">Manage members of a group</span></span>](active-directory-groups-members-azure-portal.md)
* [<span data-ttu-id="728ed-142">Gestire le appartenenze di un gruppo</span><span class="sxs-lookup"><span data-stu-id="728ed-142">Manage memberships of a group</span></span>](active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="728ed-143">Gestire le regole dinamiche per gli utenti in un gruppo</span><span class="sxs-lookup"><span data-stu-id="728ed-143">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
