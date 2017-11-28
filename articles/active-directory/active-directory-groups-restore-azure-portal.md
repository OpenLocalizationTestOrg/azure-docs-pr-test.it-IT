---
title: gruppo aaaRestore un eliminato di Office 365 in Azure Active Directory | Documenti Microsoft
description: Come toorestore un gruppo eliminato, Visualizza i gruppi possono ripristinare e permamnently Elimina un gruppo in Azure Active Directory
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
ms.openlocfilehash: 4e6650d64aa19f0c909f1c511f48681de8032f63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="restore-a-deleted-office-365-group-in-azure-active-directory"></a><span data-ttu-id="624f7-103">Ripristinare un gruppo di Office 365 eliminato in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="624f7-103">Restore a deleted Office 365 group in Azure Active Directory</span></span>

<span data-ttu-id="624f7-104">Quando si elimina un gruppo di Office 365 in hello Azure Active Directory (Azure AD), gruppo hello eliminato è mantenuta ma non è visibile per 30 giorni dalla data di eliminazione hello.</span><span class="sxs-lookup"><span data-stu-id="624f7-104">When you delete an Office 365 group in hello Azure Active Directory (Azure AD), hello deleted group is retained but not visible for 30 days from hello deletion date.</span></span> <span data-ttu-id="624f7-105">Si tratta in modo che il gruppo di hello e il relativo contenuto può essere ripristinato se necessario.</span><span class="sxs-lookup"><span data-stu-id="624f7-105">This is so that hello group and its contents can be restored if needed.</span></span> <span data-ttu-id="624f7-106">Questa funzionalità è limitata esclusivamente tooOffice 365 gruppi in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="624f7-106">This functionality is restricted exclusively tooOffice 365 groups in Azure AD.</span></span> <span data-ttu-id="624f7-107">Non è disponibile per i gruppi di sicurezza e i gruppi di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="624f7-107">It is not available for security groups and distribution groups.</span></span>

> [!NOTE] 
> <span data-ttu-id="624f7-108">Non utilizzare `Remove-MsolGroup` perché lo Elimina gruppo hello in modo permanente.</span><span class="sxs-lookup"><span data-stu-id="624f7-108">Don't use `Remove-MsolGroup` because it purges hello group permanently.</span></span> <span data-ttu-id="624f7-109">Utilizzare sempre `Remove-AzureADMSGroup` gruppo toodelete un Office 365.</span><span class="sxs-lookup"><span data-stu-id="624f7-109">Always use `Remove-AzureADMSGroup` toodelete an O365 group.</span></span> 

<span data-ttu-id="624f7-110">autorizzazioni di Hello necessarie toorestore un gruppo può essere una delle seguenti operazioni hello:</span><span class="sxs-lookup"><span data-stu-id="624f7-110">hello permissions required toorestore a group can be any of hello following:</span></span>

<span data-ttu-id="624f7-111">Ruolo</span><span class="sxs-lookup"><span data-stu-id="624f7-111">Role</span></span>  | <span data-ttu-id="624f7-112">autorizzazioni</span><span class="sxs-lookup"><span data-stu-id="624f7-112">Permissions</span></span> 
--------- | ---------
<span data-ttu-id="624f7-113">Amministratore della società, supporto partner di livello 2 e amministratori del servizio di InTune</span><span class="sxs-lookup"><span data-stu-id="624f7-113">Company Administrator, Partner Tier2 support, and InTune Service Admins</span></span> | <span data-ttu-id="624f7-114">Possono ripristinare qualsiasi gruppo di Office 365 eliminato</span><span class="sxs-lookup"><span data-stu-id="624f7-114">Can restore any deleted Office 365 group</span></span> 
<span data-ttu-id="624f7-115">Amministratore dell'account utente e supporto partner di livello 1</span><span class="sxs-lookup"><span data-stu-id="624f7-115">User Account Administrator and Partner Tier1 support</span></span> | <span data-ttu-id="624f7-116">Ripristinare qualsiasi gruppo di Office 365 eliminato, ad eccezione di tali toohello assegnato il ruolo di amministratore della società</span><span class="sxs-lookup"><span data-stu-id="624f7-116">Can restore any deleted Office 365 group except those assigned toohello Company Administrator role</span></span> 
<span data-ttu-id="624f7-117">Utente</span><span class="sxs-lookup"><span data-stu-id="624f7-117">User</span></span> | <span data-ttu-id="624f7-118">Possono ripristinare qualsiasi gruppo di Office 365 eliminato che era di loro proprietà</span><span class="sxs-lookup"><span data-stu-id="624f7-118">Can restore any deleted Office 365 group that they owned</span></span> 


## <a name="view-hello-deleted-office-365-groups-that-are-available-toorestore"></a><span data-ttu-id="624f7-119">Hello vista eliminata gruppi di Office 365 toorestore disponibili</span><span class="sxs-lookup"><span data-stu-id="624f7-119">View hello deleted Office 365 groups that are available toorestore</span></span>
<span data-ttu-id="624f7-120">Hello seguendo i cmdlet può essere utilizzati tooview hello eliminato gruppi tooverify che hello uno o quelli che si è interessati non ancora stati definitivamente eliminati.</span><span class="sxs-lookup"><span data-stu-id="624f7-120">hello following cmdlets can be used tooview hello deleted groups tooverify that hello one or ones you're interested in have not yet been permanently purged.</span></span> <span data-ttu-id="624f7-121">Questi cmdlet sono parte di hello [modulo Azure AD PowerShell](https://www.powershellgallery.com/packages/AzureAD/).</span><span class="sxs-lookup"><span data-stu-id="624f7-121">These cmdlets are part of hello [Azure AD PowerShell module](https://www.powershellgallery.com/packages/AzureAD/).</span></span> <span data-ttu-id="624f7-122">Ulteriori informazioni su questo modulo sono reperibile in hello [Azure Active Directory PowerShell versione 2](/powershell/azure/install-adv2?view=azureadps-2.0) articolo.</span><span class="sxs-lookup"><span data-stu-id="624f7-122">More information about this module can be found in hello [Azure Active Directory PowerShell Version 2](/powershell/azure/install-adv2?view=azureadps-2.0) article.</span></span>

1.  <span data-ttu-id="624f7-123">Eseguire hello cmdlet toodisplay eliminati tutti i gruppi di Office 365 nel tenant che sono ancora disponibili toorestore seguente.</span><span class="sxs-lookup"><span data-stu-id="624f7-123">Run hello following cmdlet toodisplay all deleted Office 365 groups in your tenant that are still available toorestore.</span></span>
  ```
  Get-AzureADMSDeletedGroup
  ```

2.  <span data-ttu-id="624f7-124">In alternativa, se si conosce objectID hello di un gruppo specifico (ed è possibile ottenerlo dal cmdlet hello nel passaggio 1), esecuzione hello seguente tooverify cmdlet che hello specifico gruppo eliminato non ancora definitivamente eliminato.</span><span class="sxs-lookup"><span data-stu-id="624f7-124">Alternately, if you know hello objectID of a specific group (and you can get it from hello cmdlet in step 1), run hello following cmdlet tooverify that hello specific deleted group has not yet been permanently purged.</span></span>
  ```
  Get-AzureADMSDeletedGroup –Id <objectId>
  ```



## <a name="how-toorestore-your-deleted-office-365-group"></a><span data-ttu-id="624f7-125">Come toorestore il gruppo di Office 365 eliminato</span><span class="sxs-lookup"><span data-stu-id="624f7-125">How toorestore your deleted Office 365 group</span></span>
<span data-ttu-id="624f7-126">Dopo avere verificato che tale gruppo hello sia ancora disponibile toorestore, ripristinare il gruppo di hello eliminato con uno di hello alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="624f7-126">Once you have verified that hello group is still available toorestore, restore hello deleted group with one of hello following steps.</span></span> <span data-ttu-id="624f7-127">Se il gruppo di hello contiene documenti, SP siti o altri oggetti persistenti, potrebbe richiedere fino a too24 ore toofully ripristino un gruppo e il relativo contenuto.</span><span class="sxs-lookup"><span data-stu-id="624f7-127">If hello group contains documents, SP sites, or other persistent objects, it might take up too24 hours toofully restore a group and its contents.</span></span>

1.  <span data-ttu-id="624f7-128">Esecuzione hello seguenti gruppo hello toorestore di cmdlet e il relativo contenuto.</span><span class="sxs-lookup"><span data-stu-id="624f7-128">Run hello following cmdlet toorestore hello group and its contents.</span></span>
  
  ```
  Restore-AzureADMSDeletedDirectoryObject –Id <objectId>
  ``` 

<span data-ttu-id="624f7-129">In alternativa, hello cmdlet seguente può essere eseguito toopermanently rimuovere il gruppo di hello eliminato.</span><span class="sxs-lookup"><span data-stu-id="624f7-129">Alternatively, hello following cmdlet can be run toopermanently remove hello deleted group.</span></span>
  ```
  Remove-AzureADMSDeletedDirectoryObject –Id <objectId>
  ```

## <a name="how-do-you-know-this-worked"></a><span data-ttu-id="624f7-130">Come si verifica che l'azione è riuscita?</span><span class="sxs-lookup"><span data-stu-id="624f7-130">How do you know this worked?</span></span>
<span data-ttu-id="624f7-131">che è stato ripristinato correttamente un gruppo di Office 365, eseguire hello tooverify `Get-AzureADGroup –ObjectId <objectId>` toodisplay cmdlet informazioni gruppo hello.</span><span class="sxs-lookup"><span data-stu-id="624f7-131">tooverify that you’ve successfully restored an Office 365 group, run hello `Get-AzureADGroup –ObjectId <objectId>` cmdlet toodisplay information about hello group.</span></span> <span data-ttu-id="624f7-132">Dopo il ripristino di hello completamento della richiesta:</span><span class="sxs-lookup"><span data-stu-id="624f7-132">After hello restore request is completed:</span></span>
- <span data-ttu-id="624f7-133">Hello gruppo verrà visualizzato nella barra di spostamento sinistro hello in Exchange</span><span class="sxs-lookup"><span data-stu-id="624f7-133">hello group will appear in hello Left nav bar on Exchange</span></span>
- <span data-ttu-id="624f7-134">piano di Hello per gruppo hello apparirà nella pianificazione</span><span class="sxs-lookup"><span data-stu-id="624f7-134">hello plan for hello group will appear in Planner</span></span>
- <span data-ttu-id="624f7-135">I siti di Sharepoint e tutti i contenuti saranno disponibili</span><span class="sxs-lookup"><span data-stu-id="624f7-135">Any Sharepoint sites and all of their contents will be available</span></span>
- <span data-ttu-id="624f7-136">gruppo Hello è possibile accedere da qualsiasi endpoint di scambio di hello e altri carichi di lavoro di Office 365 che supportano i gruppi di Office 365</span><span class="sxs-lookup"><span data-stu-id="624f7-136">hello group can be accessed from any of hello Exchange endpoints and other Office 365 workloads that support Office 365 groups</span></span>


## <a name="next-steps"></a><span data-ttu-id="624f7-137">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="624f7-137">Next steps</span></span>
<span data-ttu-id="624f7-138">Questi articoli contengono informazioni aggiuntive sui gruppi di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="624f7-138">These articles provide additional information on Azure Active Directory groups.</span></span>

* [<span data-ttu-id="624f7-139">Vedere i gruppi esistenti</span><span class="sxs-lookup"><span data-stu-id="624f7-139">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="624f7-140">Gestire le impostazioni di un gruppo</span><span class="sxs-lookup"><span data-stu-id="624f7-140">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="624f7-141">Gestire i membri di un gruppo</span><span class="sxs-lookup"><span data-stu-id="624f7-141">Manage members of a group</span></span>](active-directory-groups-members-azure-portal.md)
* [<span data-ttu-id="624f7-142">Gestire le appartenenze di un gruppo</span><span class="sxs-lookup"><span data-stu-id="624f7-142">Manage memberships of a group</span></span>](active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="624f7-143">Gestire le regole dinamiche per gli utenti in un gruppo</span><span class="sxs-lookup"><span data-stu-id="624f7-143">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
