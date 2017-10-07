---
title: aaaDisable accessi degli utenti per un'applicazione aziendale in Azure Active Directory | Documenti Microsoft
description: Come toodisable un'applicazione aziendale in modo che nessun utente possono accedere tooit in Azure Active Directory
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: a27562f9-18dc-42e8-9fee-5419566f8fd7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 4c560b59359d433b0852a7606cc2cc0204866234
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="disable-user-sign-ins-for-an-enterprise-app-in-azure-active-directory"></a><span data-ttu-id="74f09-103">Disabilitare gli accessi utente per un'app aziendale in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="74f09-103">Disable user sign-ins for an enterprise app in Azure Active Directory</span></span>
<span data-ttu-id="74f09-104">È facile toodisable un'applicazione aziendale in modo che nessun utente possono accedere tooit in Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="74f09-104">It's easy toodisable an enterprise application so that no users may sign in tooit in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="74f09-105">È necessario hello delle autorizzazioni appropriate toomanage hello enterprise app, che è necessario essere amministratore globale per la directory di hello.</span><span class="sxs-lookup"><span data-stu-id="74f09-105">You must have hello appropriate permissions toomanage hello enterprise app, and you must be global admin for hello directory.</span></span>

## <a name="how-do-i-disable-user-sign-ins"></a><span data-ttu-id="74f09-106">Come è possibile disabilitare l'accesso degli utenti?</span><span class="sxs-lookup"><span data-stu-id="74f09-106">How do I disable user sign-ins?</span></span>
1. <span data-ttu-id="74f09-107">Accedi toohello [portale di Azure](https://portal.azure.com) con un account che sia un amministratore globale per la directory di hello.</span><span class="sxs-lookup"><span data-stu-id="74f09-107">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="74f09-108">Selezionare **più servizi**, immettere **Azure Active Directory** nella casella di testo hello e quindi selezionare **invio**.</span><span class="sxs-lookup"><span data-stu-id="74f09-108">Select **More services**, enter **Azure Active Directory** in hello text box, and then select **Enter**.</span></span>
3. <span data-ttu-id="74f09-109">In hello **Azure Active Directory** -  ***nomedirectory*** blade (vale a dire hello Azure AD pannello per directory hello gestiti), selezionare **leapplicazioniaziendali**.</span><span class="sxs-lookup"><span data-stu-id="74f09-109">On hello **Azure Active Directory** -  ***directoryname*** blade (that is, hello Azure AD blade for hello directory you are managing), select **Enterprise applications**.</span></span>

    ![Apertura di app aziendali](./media/active-directory-coreapps-disable-app-azure-portal/open-enterprise-apps.png)
4. <span data-ttu-id="74f09-111">In hello **applicazioni aziendali** pannello seleziona **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="74f09-111">On hello **Enterprise applications** blade, select **All applications**.</span></span> <span data-ttu-id="74f09-112">Viene visualizzato un elenco di App hello che è possibile gestire.</span><span class="sxs-lookup"><span data-stu-id="74f09-112">You see a list of hello apps you can manage.</span></span>
5. <span data-ttu-id="74f09-113">In hello **applicazioni aziendali - tutte le applicazioni** pannello, selezionare un'app.</span><span class="sxs-lookup"><span data-stu-id="74f09-113">On hello **Enterprise applications - All applications** blade, select an app.</span></span>
6. <span data-ttu-id="74f09-114">In hello ***appname*** blade (vale a dire hello pannello con il nome di hello di hello app selezionata nel titolo hello), selezionare **proprietà**.</span><span class="sxs-lookup"><span data-stu-id="74f09-114">On hello ***appname*** blade (that is, hello blade with hello name of hello selected app in hello title), select **Properties**.</span></span>

    ![Selezione di hello tutti i comandi di applicazioni](./media/active-directory-coreapps-disable-app-azure-portal/select-app.png)
7. <span data-ttu-id="74f09-116">In hello ***appname*** - **proprietà** pannello seleziona **n** per **abilitato per gli utenti toosign?**.</span><span class="sxs-lookup"><span data-stu-id="74f09-116">On hello ***appname*** - **Properties** blade, select **No** for **Enabled for users toosign-in?**.</span></span>
8. <span data-ttu-id="74f09-117">Seleziona hello **salvare** comando.</span><span class="sxs-lookup"><span data-stu-id="74f09-117">Select hello **Save** command.</span></span>

## <a name="next-steps"></a><span data-ttu-id="74f09-118">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="74f09-118">Next steps</span></span>
* [<span data-ttu-id="74f09-119">Visualizzare tutti i gruppi personali</span><span class="sxs-lookup"><span data-stu-id="74f09-119">See all my groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="74f09-120">Assegnare un'applicazione aziendale tooan utente o gruppo</span><span class="sxs-lookup"><span data-stu-id="74f09-120">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)
* [<span data-ttu-id="74f09-121">Rimuovere l'assegnazione di un utente o un gruppo da un'app aziendale</span><span class="sxs-lookup"><span data-stu-id="74f09-121">Remove a user or group assignment from an enterprise app</span></span>](active-directory-coreapps-remove-assignment-azure-portal.md)
* [<span data-ttu-id="74f09-122">Modificare il nome di hello o logo di un'applicazione aziendale</span><span class="sxs-lookup"><span data-stu-id="74f09-122">Change hello name or logo of an enterprise app</span></span>](active-directory-coreapps-change-app-logo-user-azure-portal.md)
