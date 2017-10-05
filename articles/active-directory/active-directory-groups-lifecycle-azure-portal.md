---
title: "Funzionalità di anteprima di scadenza dei gruppi di Office 365 in Azure Active Directory | Microsoft Docs"
description: Come configurare la scadenza dei gruppi di Office 365 in Azure Active Directory (anteprima)
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
ms.openlocfilehash: 8a43df84fd050d7b4bd8d937b8c55e744cb805d3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="configure-office-365-groups-expiration-preview"></a><span data-ttu-id="9decd-103">Configurare la scadenza dei gruppi di Office 365 (anteprima)</span><span class="sxs-lookup"><span data-stu-id="9decd-103">Configure Office 365 groups expiration (preview)</span></span>

<span data-ttu-id="9decd-104">È ora possibile gestire il ciclo di vita dei gruppi di Office 365 impostando la scadenza per qualsiasi gruppo di Office 365 selezionato.</span><span class="sxs-lookup"><span data-stu-id="9decd-104">You can now manage the lifecycle of Office 365 groups by setting expiration for any Office 365 groups that you select.</span></span> <span data-ttu-id="9decd-105">Dopo che la scadenza è stata impostata, ai proprietari dei gruppi viene chiesto di rinnovare il gruppo, se è ancora necessario.</span><span class="sxs-lookup"><span data-stu-id="9decd-105">Once this expiration is set, owners of those groups are asked to renew their groups if they still need the groups.</span></span> <span data-ttu-id="9decd-106">Qualsiasi gruppo di Office 365 che non viene rinnovato sarà eliminato.</span><span class="sxs-lookup"><span data-stu-id="9decd-106">Any Office 365 group that is not renewed will be deleted.</span></span> <span data-ttu-id="9decd-107">Qualsiasi gruppo di Office 365 eliminato può essere ripristinato entro 30 giorni dall'amministratore o dai proprietari del gruppo.</span><span class="sxs-lookup"><span data-stu-id="9decd-107">Any Office 365 group that was deleted can be restored within 30 days by the group owners or the administrator.</span></span>  


> [!NOTE]
> <span data-ttu-id="9decd-108">È possibile impostare la scadenza solo per i gruppi di Office 365.</span><span class="sxs-lookup"><span data-stu-id="9decd-108">You can set expiration for only Office 365 groups.</span></span>
>
> <span data-ttu-id="9decd-109">Per impostare la scadenza per i gruppi di Office 365, è necessario che venga assegnata una licenza di Azure AD Premium a</span><span class="sxs-lookup"><span data-stu-id="9decd-109">Setting expiration for O365 groups requires that an Azure AD Premium license is assigned to</span></span>
>   - <span data-ttu-id="9decd-110">L'amministratore che configura le impostazioni di scadenza per il tenant</span><span class="sxs-lookup"><span data-stu-id="9decd-110">The administrator who configures the expiration settings for the tenant</span></span>
>   - <span data-ttu-id="9decd-111">Tutti i membri dei gruppi selezionati per questa impostazione</span><span class="sxs-lookup"><span data-stu-id="9decd-111">All members of the groups selected for this setting</span></span>

## <a name="set-office-365-groups-expiration"></a><span data-ttu-id="9decd-112">Impostare la scadenza dei gruppi di Office 365</span><span class="sxs-lookup"><span data-stu-id="9decd-112">Set Office 365 groups expiration</span></span>

1. <span data-ttu-id="9decd-113">Aprire l'[interfaccia di amministrazione di Azure AD](https://aad.portal.azure.com) con un account di amministratore globale per il tenant di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9decd-113">Open the [Azure AD admin center](https://aad.portal.azure.com) with an account that is a global administrator in your Azure AD tenant.</span></span>

2. <span data-ttu-id="9decd-114">Aprire Azure AD e selezionare **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="9decd-114">Open Azure AD, select **Users and groups**.</span></span>

3. <span data-ttu-id="9decd-115">Selezionare **Impostazioni di gruppo** e quindi **Scadenza** per aprire le impostazioni di scadenza.</span><span class="sxs-lookup"><span data-stu-id="9decd-115">Select **Group settings** and then select **Expiration** to open the expiration settings.</span></span>
  
  ![Pannello Scadenza](./media/active-directory-groups-lifecycle-azure-portal/expiration-settings.png)

4. <span data-ttu-id="9decd-117">Nel pannello **Scadenza** è possibile:</span><span class="sxs-lookup"><span data-stu-id="9decd-117">On the **Expiration** blade, you can:</span></span>

  * <span data-ttu-id="9decd-118">Impostare la durata del gruppo in giorni.</span><span class="sxs-lookup"><span data-stu-id="9decd-118">Set the group lifetime in days.</span></span> <span data-ttu-id="9decd-119">È possibile selezionare uno dei valori predefiniti oppure un valore personalizzato (che deve essere di 31 giorni o più).</span><span class="sxs-lookup"><span data-stu-id="9decd-119">You could select one of the preset values, or a custom value (should be 31 days or more).</span></span> 
  * <span data-ttu-id="9decd-120">Specificare un indirizzo e-mail per l'invio delle notifiche di rinnovo e di scadenza quando un gruppo non ha un proprietario.</span><span class="sxs-lookup"><span data-stu-id="9decd-120">Specify an email address where the renewal and expiration notifications should be sent when a group has no owner.</span></span> 
  * <span data-ttu-id="9decd-121">Selezionare i gruppi di Office 365 che scadono.</span><span class="sxs-lookup"><span data-stu-id="9decd-121">Select which Office 365 groups expire.</span></span> <span data-ttu-id="9decd-122">È possibile abilitare la scadenza per **tutti** i gruppi di Office 365, selezionare alcuni tra i gruppi di Office 365 oppure selezionare **Nessuno** per disabilitare la scadenza per tutti i gruppi.</span><span class="sxs-lookup"><span data-stu-id="9decd-122">You can enable expiration for **All** Office 365 groups, you can select from among the Office 365 groups, or you select **None** to disable expiration for all groups.</span></span>
  * <span data-ttu-id="9decd-123">Al termine salvare le impostazioni facendo clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="9decd-123">Save your settings when you're done by selecting **Save**.</span></span>

<span data-ttu-id="9decd-124">Per istruzioni su come scaricare e installare il modulo di Microsoft PowerShell per configurare la scadenza per i gruppi di Office 365 tramite PowerShell, vedere [Azure Active Directory V2 PowerShell Module - Public Preview Release 2.0.0.137](https://www.powershellgallery.com/packages/AzureADPreview/2.0.0.137) (Modulo di PowerShell per Azure Active Directory V2 - Versione di anteprima pubblica 2.0.0.137).</span><span class="sxs-lookup"><span data-stu-id="9decd-124">For instructions on how to download and install the Microsoft PowerShell module to configure expiration for Office 365 groups via PowerShell, see [Azure Active Directory V2 PowerShell Module - Public Preview Release 2.0.0.137](https://www.powershellgallery.com/packages/AzureADPreview/2.0.0.137).</span></span>

<span data-ttu-id="9decd-125">Le notifiche tramite posta elettronica di questo tipo vengono inviate ai proprietari del gruppo di Office 365 30 giorni, 15 giorni e 1 giorno prima della scadenza del gruppo.</span><span class="sxs-lookup"><span data-stu-id="9decd-125">Email notifications such as this one are sent to the Office 365 group owners 30 days, 15 days, and 1 day prior to expiration of the group.</span></span>

![Notifica di scadenza tramite posta elettronica](./media/active-directory-groups-lifecycle-azure-portal/expiration-notification.png)

<span data-ttu-id="9decd-127">Il proprietario del gruppo può quindi selezionare **Renew group** (Rinnova gruppo) per rinnovare il gruppo di Office 365 oppure **Go to group** (Vai al gruppo) per visualizzare i membri del gruppo e altri dettagli.</span><span class="sxs-lookup"><span data-stu-id="9decd-127">The group owner can then select **Renew group** to renew the Office 365 group, or can select **Go to group** to see the members and other details about the group.</span></span>

<span data-ttu-id="9decd-128">Alla scadenza il gruppo viene eliminato, un giorno dopo la data di scadenza.</span><span class="sxs-lookup"><span data-stu-id="9decd-128">When a group expires, the group is deleted one day after the expiration date.</span></span> <span data-ttu-id="9decd-129">Viene inviata una notifica tramite posta elettronica simile alla seguente ai proprietari del gruppo di Office 365 per informarli della scadenza e della conseguente eliminazione del gruppo di Office 365.</span><span class="sxs-lookup"><span data-stu-id="9decd-129">An email notification such as this one is sent to the Office 365 group owners informing them about the expiration and subsequent deletion of their Office 365 group.</span></span>

![Notifica tramite posta elettronica per l'eliminazione del gruppo](./media/active-directory-groups-lifecycle-azure-portal/deletion-notification.png)

<span data-ttu-id="9decd-131">Il gruppo può essere ripristinato selezionando **Restore group** (Ripristina gruppo) oppure usando i cmdlet di PowerShell, come descritto in [Ripristinare un gruppo di Office 365 eliminato in Azure Active Directory] (https://docs.microsoft.com/azure/active-directory/active-directory-groups-restore-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="9decd-131">The group can be restored by selecting **Restore group** or by using PowerShell cmdlets, as described in [Restore a deleted Office 365 group in Azure Active Directory] (https://docs.microsoft.com/azure/active-directory/active-directory-groups-restore-azure-portal).</span></span>
    
<span data-ttu-id="9decd-132">Se il gruppo che si sta ripristinando contiene documenti, siti di SharePoint o altri oggetti persistenti, potrebbero essere necessarie fino a 24 ore per ripristinare completamente il gruppo e il relativo contenuto.</span><span class="sxs-lookup"><span data-stu-id="9decd-132">If the group you're restoring contains documents, SharePoint sites, or other persistent objects, it might take up to 24 hours to fully restore the group and its contents.</span></span>

> [!NOTE]
> * <span data-ttu-id="9decd-133">Quando si distribuiscono le impostazioni di scadenza, potrebbero esserci alcuni gruppi anteriori all'intervallo di scadenza.</span><span class="sxs-lookup"><span data-stu-id="9decd-133">When deploying the expiration settings, there might be some groups that are older than the expiration window.</span></span> <span data-ttu-id="9decd-134">Questi gruppi non vengono eliminati immediatamente, ma ne viene impostata la scadenza dopo 30 giorni.</span><span class="sxs-lookup"><span data-stu-id="9decd-134">These groups are not be immediately deleted, but are set to 30 days until expiration.</span></span> <span data-ttu-id="9decd-135">La prima notifica di rinnovo viene inviata tramite posta elettronica entro un giorno.</span><span class="sxs-lookup"><span data-stu-id="9decd-135">The first renewal notification email is sent out within a day.</span></span> <span data-ttu-id="9decd-136">Ad esempio, il gruppo A è stato creato da 400 giorni e l'intervallo di scadenza è impostato su 180 giorni.</span><span class="sxs-lookup"><span data-stu-id="9decd-136">For example, Group A was created 400 days ago, and the expiration interval is set to 180 days.</span></span> <span data-ttu-id="9decd-137">Quando si applicano le impostazioni di scadenza, il gruppo A ha 30 giorni prima di essere eliminato, a meno che il proprietario non lo rinnovi.</span><span class="sxs-lookup"><span data-stu-id="9decd-137">When you apply expiration settings, Group A has 30 days before it is deleted, unless the owner renews it.</span></span>
> * <span data-ttu-id="9decd-138">Quando un gruppo dinamico viene eliminato e ripristinato, viene considerato come un nuovo gruppo e popolato nuovamente in base alla regola.</span><span class="sxs-lookup"><span data-stu-id="9decd-138">When a dynamic group is deleted and restored, it is seen as a new group and re-populated according to the rule.</span></span> <span data-ttu-id="9decd-139">Questo processo può richiedere fino a 24 ore.</span><span class="sxs-lookup"><span data-stu-id="9decd-139">This process might take up to 24 hours.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9decd-140">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9decd-140">Next steps</span></span>
<span data-ttu-id="9decd-141">Questi articoli forniscono informazioni aggiuntive sui gruppi di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9decd-141">These articles provide additional information on Azure AD groups.</span></span>

* [<span data-ttu-id="9decd-142">Vedere i gruppi esistenti</span><span class="sxs-lookup"><span data-stu-id="9decd-142">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="9decd-143">Gestire le impostazioni di un gruppo</span><span class="sxs-lookup"><span data-stu-id="9decd-143">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="9decd-144">Gestire i membri di un gruppo</span><span class="sxs-lookup"><span data-stu-id="9decd-144">Manage members of a group</span></span>](active-directory-groups-members-azure-portal.md)
* [<span data-ttu-id="9decd-145">Gestire le appartenenze di un gruppo</span><span class="sxs-lookup"><span data-stu-id="9decd-145">Manage memberships of a group</span></span>](active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="9decd-146">Gestire le regole dinamiche per gli utenti in un gruppo</span><span class="sxs-lookup"><span data-stu-id="9decd-146">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
