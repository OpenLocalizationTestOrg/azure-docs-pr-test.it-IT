---
title: Rimuovere l'assegnazione di un utente o di un gruppo da un'app aziendale in Azure Active Directory | Microsoft Docs
description: Come rimuovere l'assegnazione di accesso di un utente o gruppo da un'app aziendale in anteprima di Azure Active Directory
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 7b2d365b-ae92-477f-9702-353cc6acc5ea
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 02f122acfb53c2107e2b0af66c6195aa127a2c77
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="remove-a-user-or-group-assignment-from-an-enterprise-app-in-azure-active-directory"></a><span data-ttu-id="99001-103">Rimuovere l'assegnazione di un utente o un gruppo da un'app aziendale in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="99001-103">Remove a user or group assignment from an enterprise app in Azure Active Directory</span></span>
<span data-ttu-id="99001-104">Rimuovere un utente o un gruppo dalla possibilità di accedere a una delle applicazioni aziendali in Azure Active Directory (Azure AD) è un'operazione facile.</span><span class="sxs-lookup"><span data-stu-id="99001-104">It's easy to remove a user or a group from being assigned access to one of your enterprise applications in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="99001-105">È necessario disporre delle autorizzazioni appropriate per gestire l'app aziendale ed essere amministratore globale della directory.</span><span class="sxs-lookup"><span data-stu-id="99001-105">You must have the appropriate permissions to manage the enterprise app, and you must be global admin for the directory.</span></span>

## <a name="how-do-i-remove-a-user-or-group-assignment"></a><span data-ttu-id="99001-106">Come è possibile rimuovere l'assegnazione di un utente o un gruppo?</span><span class="sxs-lookup"><span data-stu-id="99001-106">How do I remove a user or group assignment?</span></span>
1. <span data-ttu-id="99001-107">Accedere al [portale di Azure](https://portal.azure.com) con un account di amministratore globale per la directory.</span><span class="sxs-lookup"><span data-stu-id="99001-107">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="99001-108">Selezionare **Altri servizi**, immettere **Azure Active Directory** nella casella di testo e quindi selezionare **Invio**.</span><span class="sxs-lookup"><span data-stu-id="99001-108">Select **More services**, enter **Azure Active Directory** in the text box, and then select **Enter**.</span></span>
3. <span data-ttu-id="99001-109">Nel pannello **Azure Active Directory - *nomedirectory*** vale a dire il pannello Azure AD per la directory che si sta gestendo, selezionare **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="99001-109">On the **Azure Active Directory - *directoryname*** blade (that is, the Azure AD blade for the directory you are managing), select **Enterprise applications**.</span></span>

    ![Apertura di app aziendali](./media/active-directory-coreapps-remove-assignment-user-azure-portal/open-enterprise-apps.png)
4. <span data-ttu-id="99001-111">Nel pannello **Applicazioni aziendali** selezionare **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="99001-111">On the **Enterprise applications** blade, select **All applications**.</span></span> <span data-ttu-id="99001-112">Verrà visualizzato un elenco di app che è possibile gestire.</span><span class="sxs-lookup"><span data-stu-id="99001-112">You'll see a list of the apps you can manage.</span></span>
5. <span data-ttu-id="99001-113">Nel pannello **Applicazioni aziendali - All applications** (Tutte le applicazioni) selezionare un'app.</span><span class="sxs-lookup"><span data-stu-id="99001-113">On the **Enterprise applications - All applications** blade, select an app.</span></span>
6. <span data-ttu-id="99001-114">Nel pannello ***nome app***, ovvero il pannello con il nome dell'app selezionata nel titolo, selezionare **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="99001-114">On the ***appname*** blade (that is, the blade with the name of the selected app in the title), select **Users & Groups**.</span></span>

    ![Selezione di utenti o gruppi](./media/active-directory-coreapps-remove-assignment-user-azure-portal/remove-app-users.png)
7. <span data-ttu-id="99001-116">Nel pannello ***nomeapp*** di **assegnazione utente e gruppo** selezionare uno o più utenti o gruppi e quindi fare clic sul comando **Rimuovi**.</span><span class="sxs-lookup"><span data-stu-id="99001-116">On the ***appname*** **- User & Group Assignment** blade, select one of more users or groups and then select the **Remove** command.</span></span> <span data-ttu-id="99001-117">Confermare la decisione al prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="99001-117">Confirm your decision at the prompt.</span></span>

    ![Selezione del comando Rimuovi](./media/active-directory-coreapps-remove-assignment-user-azure-portal/remove-users.png)

## <a name="next-steps"></a><span data-ttu-id="99001-119">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="99001-119">Next steps</span></span>
* [<span data-ttu-id="99001-120">Visualizzare tutti i gruppi personali</span><span class="sxs-lookup"><span data-stu-id="99001-120">See all of my groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="99001-121">Assegnare un utente o gruppo a un'app aziendale</span><span class="sxs-lookup"><span data-stu-id="99001-121">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)
* [<span data-ttu-id="99001-122">Disabilitare l'accesso degli utenti per un'app aziendale</span><span class="sxs-lookup"><span data-stu-id="99001-122">Disable user sign-ins for an enterprise app</span></span>](active-directory-coreapps-disable-app-azure-portal.md)
* [<span data-ttu-id="99001-123">Modificare il nome o il logo di un'app aziendale</span><span class="sxs-lookup"><span data-stu-id="99001-123">Change the name or logo of an enterprise app</span></span>](active-directory-coreapps-change-app-logo-user-azure-portal.md)
