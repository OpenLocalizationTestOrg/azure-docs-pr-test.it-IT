---
title: gruppi di Office 365 aaaPreview scadenza in Azure Active Directory | Documenti Microsoft
description: Come i gruppi tooset di scadenza per Office 365 in Azure Active Directory (anteprima)
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: curtand
ms.reviewer: kairaz.contractor
ms.custom: it-pro
ms.openlocfilehash: a8c99961cff3aad3f4d8b0cc1b2eb8e8a4c9ba95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-office-365-groups-expiration-preview"></a><span data-ttu-id="7de77-103">Configurare la scadenza dei gruppi di Office 365 (anteprima)</span><span class="sxs-lookup"><span data-stu-id="7de77-103">Configure Office 365 groups expiration (preview)</span></span>

<span data-ttu-id="7de77-104">È ora possibile gestire hello del ciclo di vita dei gruppi di Office 365 tramite l'impostazione di scadenza per i gruppi di Office 365 selezionato.</span><span class="sxs-lookup"><span data-stu-id="7de77-104">You can now manage hello lifecycle of Office 365 groups by setting expiration for any Office 365 groups that you select.</span></span> <span data-ttu-id="7de77-105">Dopo la scadenza è impostata, i proprietari di tali gruppi sono frequenti toorenew i relativi gruppi se devono comunque gruppi hello.</span><span class="sxs-lookup"><span data-stu-id="7de77-105">Once this expiration is set, owners of those groups are asked toorenew their groups if they still need hello groups.</span></span> <span data-ttu-id="7de77-106">Qualsiasi gruppo di Office 365 che non viene rinnovato sarà eliminato.</span><span class="sxs-lookup"><span data-stu-id="7de77-106">Any Office 365 group that is not renewed will be deleted.</span></span> <span data-ttu-id="7de77-107">È possibile ripristinare alcun gruppo di Office 365 è stata eliminata entro 30 giorni per i proprietari del gruppo hello o un amministratore di hello.</span><span class="sxs-lookup"><span data-stu-id="7de77-107">Any Office 365 group that was deleted can be restored within 30 days by hello group owners or hello administrator.</span></span>  


> [!NOTE]
> <span data-ttu-id="7de77-108">È possibile impostare la scadenza solo per i gruppi di Office 365.</span><span class="sxs-lookup"><span data-stu-id="7de77-108">You can set expiration for only Office 365 groups.</span></span>
>
> <span data-ttu-id="7de77-109">Per impostare la scadenza per i gruppi di Office 365, è necessario che venga assegnata una licenza di Azure AD Premium a</span><span class="sxs-lookup"><span data-stu-id="7de77-109">Setting expiration for O365 groups requires that an Azure AD Premium license is assigned to</span></span>
>   - <span data-ttu-id="7de77-110">messaggio per l'amministratore che configura le impostazioni di scadenza hello per tenant hello</span><span class="sxs-lookup"><span data-stu-id="7de77-110">hello administrator who configures hello expiration settings for hello tenant</span></span>
>   - <span data-ttu-id="7de77-111">Tutti i membri dei gruppi di hello selezionati per questa impostazione</span><span class="sxs-lookup"><span data-stu-id="7de77-111">All members of hello groups selected for this setting</span></span>

## <a name="set-office-365-groups-expiration"></a><span data-ttu-id="7de77-112">Impostare la scadenza dei gruppi di Office 365</span><span class="sxs-lookup"><span data-stu-id="7de77-112">Set Office 365 groups expiration</span></span>

1. <span data-ttu-id="7de77-113">Aprire hello [centro di amministrazione di Azure AD](https://aad.portal.azure.com) con un account che sia un amministratore globale nel tenant di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7de77-113">Open hello [Azure AD admin center](https://aad.portal.azure.com) with an account that is a global administrator in your Azure AD tenant.</span></span>

2. <span data-ttu-id="7de77-114">Aprire Azure AD e selezionare **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="7de77-114">Open Azure AD, select **Users and groups**.</span></span>

3. <span data-ttu-id="7de77-115">Selezionare **impostazioni gruppo** e quindi selezionare **scadenza** tooopen le impostazioni di scadenza hello.</span><span class="sxs-lookup"><span data-stu-id="7de77-115">Select **Group settings** and then select **Expiration** tooopen hello expiration settings.</span></span>
  
  ![Pannello Scadenza](./media/active-directory-groups-lifecycle-azure-portal/expiration-settings.png)

4. <span data-ttu-id="7de77-117">In hello **scadenza** pannello, è possibile:</span><span class="sxs-lookup"><span data-stu-id="7de77-117">On hello **Expiration** blade, you can:</span></span>

  * <span data-ttu-id="7de77-118">Impostare una durata di un gruppo hello in giorni.</span><span class="sxs-lookup"><span data-stu-id="7de77-118">Set hello group lifetime in days.</span></span> <span data-ttu-id="7de77-119">È possibile selezionare uno dei set di impostazioni hello valori o un valore personalizzato (dovrebbe essere 31 giorni o più).</span><span class="sxs-lookup"><span data-stu-id="7de77-119">You could select one of hello preset values, or a custom value (should be 31 days or more).</span></span> 
  * <span data-ttu-id="7de77-120">Specificare un indirizzo di posta elettronica in cui le notifiche di rinnovo e scadenza hello devono essere inviate quando un gruppo non ha un proprietario.</span><span class="sxs-lookup"><span data-stu-id="7de77-120">Specify an email address where hello renewal and expiration notifications should be sent when a group has no owner.</span></span> 
  * <span data-ttu-id="7de77-121">Selezionare i gruppi di Office 365 che scadono.</span><span class="sxs-lookup"><span data-stu-id="7de77-121">Select which Office 365 groups expire.</span></span> <span data-ttu-id="7de77-122">È possibile abilitare la scadenza per **tutti** gruppi di Office 365, è possibile selezionare tra i gruppi di Office 365 hello o si seleziona **Nessuno** per disabilitare la scadenza per tutti i gruppi.</span><span class="sxs-lookup"><span data-stu-id="7de77-122">You can enable expiration for **All** Office 365 groups, you can select from among hello Office 365 groups, or you select **None** to disable expiration for all groups.</span></span>
  * <span data-ttu-id="7de77-123">Al termine salvare le impostazioni facendo clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="7de77-123">Save your settings when you're done by selecting **Save**.</span></span>

<span data-ttu-id="7de77-124">Per istruzioni su come toodownload e installare hello scadenza tooconfigure modulo di PowerShell di Microsoft per i gruppi di Office 365 tramite PowerShell, vedere [modulo Azure Active Directory V2 PowerShell - versione di anteprima pubblica 2.0.0.137](https://www.powershellgallery.com/packages/AzureADPreview/2.0.0.137).</span><span class="sxs-lookup"><span data-stu-id="7de77-124">For instructions on how toodownload and install hello Microsoft PowerShell module tooconfigure expiration for Office 365 groups via PowerShell, see [Azure Active Directory V2 PowerShell Module - Public Preview Release 2.0.0.137](https://www.powershellgallery.com/packages/AzureADPreview/2.0.0.137).</span></span>

<span data-ttu-id="7de77-125">Notifiche di posta elettronica, ad esempio quello vengono inviate a 30 giorni, 15 giorni, i proprietari del gruppo toohello Office 365 e 1 giorno tooexpiration precedente del gruppo di hello.</span><span class="sxs-lookup"><span data-stu-id="7de77-125">Email notifications such as this one are sent toohello Office 365 group owners 30 days, 15 days, and 1 day prior tooexpiration of hello group.</span></span>

![Notifica di scadenza tramite posta elettronica](./media/active-directory-groups-lifecycle-azure-portal/expiration-notification.png)

<span data-ttu-id="7de77-127">quindi è possibile selezionare il proprietario del gruppo Hello **gruppo rinnovo** toorenew hello gruppo Office 365, oppure è possibile selezionare **passare toogroup** membri hello toosee e altri dettagli sulla hello gruppo.</span><span class="sxs-lookup"><span data-stu-id="7de77-127">hello group owner can then select **Renew group** toorenew hello Office 365 group, or can select **Go toogroup** toosee hello members and other details about hello group.</span></span>

<span data-ttu-id="7de77-128">Alla scadenza di un gruppo, il gruppo di hello viene eliminato un giorno alla data di scadenza hello.</span><span class="sxs-lookup"><span data-stu-id="7de77-128">When a group expires, hello group is deleted one day after hello expiration date.</span></span> <span data-ttu-id="7de77-129">I proprietari del gruppo toohello Office 365 informa sulla scadenza hello e successiva eliminazione dei relativi gruppi di Office 365 verrà inviata una notifica di posta elettronica, ad esempio quello.</span><span class="sxs-lookup"><span data-stu-id="7de77-129">An email notification such as this one is sent toohello Office 365 group owners informing them about hello expiration and subsequent deletion of their Office 365 group.</span></span>

![Notifica tramite posta elettronica per l'eliminazione del gruppo](./media/active-directory-groups-lifecycle-azure-portal/deletion-notification.png)

<span data-ttu-id="7de77-131">gruppo Hello può essere ripristinato selezionando **ripristino gruppo** o utilizzando i cmdlet di PowerShell, come descritto in [gruppo di ripristino un eliminato di Office 365 in Azure Active Directory] (https://docs.microsoft.com/azure/active-directory/ Active-Directory-Groups-Restore-Azure-Portal).</span><span class="sxs-lookup"><span data-stu-id="7de77-131">hello group can be restored by selecting **Restore group** or by using PowerShell cmdlets, as described in [Restore a deleted Office 365 group in Azure Active Directory] (https://docs.microsoft.com/azure/active-directory/active-directory-groups-restore-azure-portal).</span></span>
    
<span data-ttu-id="7de77-132">Se il gruppo di hello che si sta ripristinando contiene documenti, siti di SharePoint o altri oggetti permanenti, operazione può richiedere too24 ore toofully ripristino hello gruppo e il relativo contenuto.</span><span class="sxs-lookup"><span data-stu-id="7de77-132">If hello group you're restoring contains documents, SharePoint sites, or other persistent objects, it might take up too24 hours toofully restore hello group and its contents.</span></span>

> [!NOTE]
> * <span data-ttu-id="7de77-133">Quando si distribuiscono le impostazioni di scadenza hello, potrebbero essere presenti alcuni gruppi che sono più vecchi di finestra di scadenza hello.</span><span class="sxs-lookup"><span data-stu-id="7de77-133">When deploying hello expiration settings, there might be some groups that are older than hello expiration window.</span></span> <span data-ttu-id="7de77-134">Questi gruppi non vengono eliminati immediatamente, ma sono impostare too30 giorni fino alla scadenza.</span><span class="sxs-lookup"><span data-stu-id="7de77-134">These groups are not be immediately deleted, but are set too30 days until expiration.</span></span> <span data-ttu-id="7de77-135">Hello primo rinnovo notifica tramite posta elettronica viene inviato all'interno di un giorno.</span><span class="sxs-lookup"><span data-stu-id="7de77-135">hello first renewal notification email is sent out within a day.</span></span> <span data-ttu-id="7de77-136">Ad esempio, un gruppo è stato creato 400 giorni fa e hello intervallo di scadenza è impostato too180 giorni.</span><span class="sxs-lookup"><span data-stu-id="7de77-136">For example, Group A was created 400 days ago, and hello expiration interval is set too180 days.</span></span> <span data-ttu-id="7de77-137">Quando si applicano le impostazioni di scadenza, un gruppo è 30 giorni prima di essere eliminate, a meno che lo rinnova proprietario hello.</span><span class="sxs-lookup"><span data-stu-id="7de77-137">When you apply expiration settings, Group A has 30 days before it is deleted, unless hello owner renews it.</span></span>
> * <span data-ttu-id="7de77-138">Quando un gruppo dinamico viene eliminato e viene ripristinato, viene considerata un nuovo gruppo e nuovamente popolato regola toohello secondo.</span><span class="sxs-lookup"><span data-stu-id="7de77-138">When a dynamic group is deleted and restored, it is seen as a new group and re-populated according toohello rule.</span></span> <span data-ttu-id="7de77-139">Questo processo può richiedere ore too24.</span><span class="sxs-lookup"><span data-stu-id="7de77-139">This process might take up too24 hours.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7de77-140">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7de77-140">Next steps</span></span>
<span data-ttu-id="7de77-141">Questi articoli forniscono informazioni aggiuntive sui gruppi di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7de77-141">These articles provide additional information on Azure AD groups.</span></span>

* [<span data-ttu-id="7de77-142">Vedere i gruppi esistenti</span><span class="sxs-lookup"><span data-stu-id="7de77-142">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="7de77-143">Gestire le impostazioni di un gruppo</span><span class="sxs-lookup"><span data-stu-id="7de77-143">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="7de77-144">Gestire i membri di un gruppo</span><span class="sxs-lookup"><span data-stu-id="7de77-144">Manage members of a group</span></span>](active-directory-groups-members-azure-portal.md)
* [<span data-ttu-id="7de77-145">Gestire le appartenenze di un gruppo</span><span class="sxs-lookup"><span data-stu-id="7de77-145">Manage memberships of a group</span></span>](active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="7de77-146">Gestire le regole dinamiche per gli utenti in un gruppo</span><span class="sxs-lookup"><span data-stu-id="7de77-146">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
