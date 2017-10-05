---
title: Creare un gruppo per utenti in Azure Active Directory | Microsoft Docs
description: 'Procedura: Creare un gruppo in Azure Active Directory e aggiungere membri al gruppo'
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
ms.date: 08/04/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6d3d37761a9fdf9bd9801396d45f2fcd47efb0be
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-group-and-add-members-in-azure-active-directory"></a><span data-ttu-id="fc46c-103">Creare un gruppo e aggiungere membri in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fc46c-103">Create a group and add members in Azure Active Directory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fc46c-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="fc46c-104">Azure portal</span></span>](active-directory-groups-create-azure-portal.md)
> * [<span data-ttu-id="fc46c-105">Portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="fc46c-105">Azure classic portal</span></span>](active-directory-accessmanagement-manage-groups.md)
> * [<span data-ttu-id="fc46c-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fc46c-106">PowerShell</span></span>](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

<span data-ttu-id="fc46c-107">Questo articolo descrive come creare e popolare un nuovo gruppo in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fc46c-107">This article explains how to create and populate a new group in Azure Active Directory.</span></span> <span data-ttu-id="fc46c-108">Usare un gruppo per eseguire attività di gestione come l'assegnazione di licenze o autorizzazioni per diversi utenti o dispositivi contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="fc46c-108">Use a group to perform management tasks such as assigning licenses or permissions to a number of users or devices at once.</span></span>

## <a name="how-do-i-create-a-group"></a><span data-ttu-id="fc46c-109">Come si crea un gruppo?</span><span class="sxs-lookup"><span data-stu-id="fc46c-109">How do I create a group?</span></span>
1. <span data-ttu-id="fc46c-110">Accedere al [portale di Azure](https://portal.azure.com) con un account di amministratore globale per la directory.</span><span class="sxs-lookup"><span data-stu-id="fc46c-110">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="fc46c-111">Selezionare **Altri servizi**, immettere **Utenti e gruppi** nella casella di testo e quindi selezionare **Invio**.</span><span class="sxs-lookup"><span data-stu-id="fc46c-111">Select **More services**, enter **User and groups** in the text box, and then select **Enter**.</span></span>

   ![Apertura di Gestione utenti](./media/active-directory-groups-create-azure-portal/search-user-management.png)
3. <span data-ttu-id="fc46c-113">Nel pannello **Utenti e gruppi** selezionare **Tutti i gruppi**.</span><span class="sxs-lookup"><span data-stu-id="fc46c-113">On the **Users and groups** blade, select **All groups**.</span></span>

   ![Apertura del pannello Gruppi](./media/active-directory-groups-create-azure-portal/view-groups-blade.png)
4. <span data-ttu-id="fc46c-115">Nel pannello **Utenti e gruppi - Tutti i gruppi** selezionare il comando **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="fc46c-115">On the **Users and groups - All groups** blade, select the **Add** command.</span></span>

   ![Selezione del comando Aggiungi](./media/active-directory-groups-create-azure-portal/add-group-command.png)
5. <span data-ttu-id="fc46c-117">Nel pannello **Gruppo** aggiungere un nome e una descrizione per il gruppo.</span><span class="sxs-lookup"><span data-stu-id="fc46c-117">On the **Group** blade, add a name and description for the group.</span></span>
6. <span data-ttu-id="fc46c-118">Per selezionare i membri da aggiungere al gruppo, selezionare **Assegnato** nella casella **Tipo di appartenenza** e quindi selezionare **Membri**.</span><span class="sxs-lookup"><span data-stu-id="fc46c-118">To select members to add to the group, select **Assigned** in the **Membership type** box, and then select **Members**.</span></span> <span data-ttu-id="fc46c-119">Per altre informazioni su come gestire l'appartenenza di un gruppo in modo dinamico, vedere [Utilizzo degli attributi per creare regole avanzate per l'appartenenza al gruppo](active-directory-groups-dynamic-membership-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="fc46c-119">For more information about how to manage the membership of a group dynamically, see [Using attributes to create advanced rules for group membership](active-directory-groups-dynamic-membership-azure-portal.md).</span></span>

   ![Selezione dei membri da aggiungere](./media/active-directory-groups-create-azure-portal/select-members.png)
7. <span data-ttu-id="fc46c-121">Nel pannello **Membri** selezionare uno o più utenti o dispositivi da aggiungere al gruppo e fare clic sul pulsante **Seleziona** nella parte inferiore del pannello per aggiungerli al gruppo.</span><span class="sxs-lookup"><span data-stu-id="fc46c-121">On the **Members** blade, select one or more users or devices to add to the group and select the **Select** button at the bottom of the blade to add them to the group.</span></span> <span data-ttu-id="fc46c-122">La visualizzazione nella casella **Utente** viene filtrata in base alla corrispondenza con l'immissione di una parte di un nome utente o di dispositivo.</span><span class="sxs-lookup"><span data-stu-id="fc46c-122">The **User** box filters the display based on matching your entry to any part of a user or device name.</span></span> <span data-ttu-id="fc46c-123">I caratteri jolly non sono consentiti nella casella.</span><span class="sxs-lookup"><span data-stu-id="fc46c-123">No wildcard characters are accepted in that box.</span></span>
8. <span data-ttu-id="fc46c-124">Dopo avere aggiunto i membri al gruppo, selezionare **Crea** nel pannello **Gruppo**.</span><span class="sxs-lookup"><span data-stu-id="fc46c-124">When you finish adding members to the group, select **Create** on the **Group** blade.</span></span>    

   ![Creare una conferma del gruppo](./media/active-directory-groups-create-azure-portal/create-group-confirmation.png)


## <a name="next-steps"></a><span data-ttu-id="fc46c-126">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fc46c-126">Next steps</span></span>
<span data-ttu-id="fc46c-127">Questi articoli forniscono informazioni aggiuntive su Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fc46c-127">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="fc46c-128">Vedere i gruppi esistenti</span><span class="sxs-lookup"><span data-stu-id="fc46c-128">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="fc46c-129">Gestire le impostazioni di un gruppo</span><span class="sxs-lookup"><span data-stu-id="fc46c-129">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="fc46c-130">Gestire i membri di un gruppo</span><span class="sxs-lookup"><span data-stu-id="fc46c-130">Manage members of a group</span></span>](active-directory-groups-members-azure-portal.md)
* [<span data-ttu-id="fc46c-131">Gestire le appartenenze di un gruppo</span><span class="sxs-lookup"><span data-stu-id="fc46c-131">Manage memberships of a group</span></span>](active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="fc46c-132">Gestire le regole dinamiche per gli utenti in un gruppo</span><span class="sxs-lookup"><span data-stu-id="fc46c-132">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
