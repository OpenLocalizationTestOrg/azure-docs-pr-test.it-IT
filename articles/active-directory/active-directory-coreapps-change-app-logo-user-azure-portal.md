---
title: Modificare il nome o il logo di un'app aziendale in Azure Active Directory | Microsoft Docs
description: Come modificare il nome o il logo di un'app aziendale personalizzata in Azure Active Directory
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: d01303ce-e6cb-4f3b-a4d6-ec29dfd68146
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 3e44e876dcbac704a9809ae5b3957bf94be21c48
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="change-the-name-or-logo-of-an-enterprise-app-in-azure-active-directory"></a><span data-ttu-id="cbfc6-103">Modificare il nome o il logo di un'app aziendale in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cbfc6-103">Change the name or logo of an enterprise app in Azure Active Directory</span></span>
<span data-ttu-id="cbfc6-104">Modificare il nome o il logo per un'applicazione aziendale personalizzata in Azure Active Directory (Azure AD) è un'operazione facile.</span><span class="sxs-lookup"><span data-stu-id="cbfc6-104">It's easy to change the name or logo for a custom enterprise application in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="cbfc6-105">È necessario disporre delle autorizzazioni appropriate per apportare queste modifiche ed essere l'autore dell'app personalizzata.</span><span class="sxs-lookup"><span data-stu-id="cbfc6-105">You must have the appropriate permissions to make these changes, and you must be the creator of the custom app.</span></span>

## <a name="how-do-i-change-an-enterprise-apps-name-or-logo"></a><span data-ttu-id="cbfc6-106">Come è possibile modificare il nome o il logo di un'app aziendale?</span><span class="sxs-lookup"><span data-stu-id="cbfc6-106">How do I change an enterprise app's name or logo?</span></span>
1. <span data-ttu-id="cbfc6-107">Accedere al [portale di Azure](https://portal.azure.com) con un account di amministratore globale per la directory.</span><span class="sxs-lookup"><span data-stu-id="cbfc6-107">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="cbfc6-108">Selezionare **Altri servizi**, immettere **Azure Active Directory** nella casella di testo e quindi selezionare **Invio**.</span><span class="sxs-lookup"><span data-stu-id="cbfc6-108">Select **More services**, enter **Azure Active Directory** in the text box, and then select **Enter**.</span></span>
3. <span data-ttu-id="cbfc6-109">Nel pannello **Azure Active Directory - *nomedirectory*** vale a dire il pannello Azure AD per la directory che si sta gestendo, selezionare **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="cbfc6-109">On the **Azure Active Directory - *directoryname*** blade (that is, the Azure AD blade for the directory you are managing), select **Enterprise applications**.</span></span>

    ![Apertura di app aziendali](./media/active-directory-coreapps-change-app-logo-azure-portal/open-enterprise-apps.png)
4. <span data-ttu-id="cbfc6-111">Nel pannello **Applicazioni aziendali** selezionare **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="cbfc6-111">On the **Enterprise applications** blade, select **All applications**.</span></span> <span data-ttu-id="cbfc6-112">Verrà visualizzato un elenco di app che è possibile gestire.</span><span class="sxs-lookup"><span data-stu-id="cbfc6-112">You'll see a list of the apps you can manage.</span></span>
5. <span data-ttu-id="cbfc6-113">Nel pannello **Applicazioni aziendali - All applications** (Tutte le applicazioni) selezionare un'app.</span><span class="sxs-lookup"><span data-stu-id="cbfc6-113">On the **Enterprise applications - All applications** blade, select an app.</span></span>
6. <span data-ttu-id="cbfc6-114">Nel pannello ***nomeapp***, vale a dire il pannello con il nome dell'app selezionata nel titolo, selezionare **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="cbfc6-114">On the ***appname*** blade (that is, the blade with the name of the selected app in the title), select **Properties**.</span></span>

    ![Selezione del comando Proprietà](./media/active-directory-coreapps-change-app-logo-azure-portal/select-app.png)
7. <span data-ttu-id="cbfc6-116">Nel pannello ***nome app*** **- Proprietà** cercare un file da usare come nuovo logo, modificare il nome dell'app o eseguire entrambe le operazioni.</span><span class="sxs-lookup"><span data-stu-id="cbfc6-116">On the ***appname*** **- Properties** blade, browse for a file to use as a new logo, or edit the app name, or both.</span></span>

    ![Modifica del logo dell'app o del comando nameproperties](./media/active-directory-coreapps-change-app-logo-azure-portal/change-logo.png)
8. <span data-ttu-id="cbfc6-118">Selezionare il comando **Salva** .</span><span class="sxs-lookup"><span data-stu-id="cbfc6-118">Select the **Save** command.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cbfc6-119">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="cbfc6-119">Next steps</span></span>
* [<span data-ttu-id="cbfc6-120">Visualizzare tutti i gruppi personali</span><span class="sxs-lookup"><span data-stu-id="cbfc6-120">See all of my groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="cbfc6-121">Assegnare un utente o gruppo a un'app aziendale</span><span class="sxs-lookup"><span data-stu-id="cbfc6-121">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)
* [<span data-ttu-id="cbfc6-122">Rimuovere l'assegnazione di un utente o un gruppo da un'app aziendale</span><span class="sxs-lookup"><span data-stu-id="cbfc6-122">Remove a user or group assignment from an enterprise app</span></span>](active-directory-coreapps-remove-assignment-azure-portal.md)
* [<span data-ttu-id="cbfc6-123">Disabilitare l'accesso degli utenti per un'app aziendale</span><span class="sxs-lookup"><span data-stu-id="cbfc6-123">Disable user sign-ins for an enterprise app</span></span>](active-directory-coreapps-disable-app-azure-portal.md)
