---
title: Disabilitare gli accessi degli utenti per un'app aziendale in Azure Active Directory | Microsoft Docs
description: Come disabilitare un'applicazione aziendale in modo che gli utenti non possano accedervi in Azure Active Directory
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
ms.openlocfilehash: 5d27046370eada0c371c94fb573fa1bcf536f7cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="disable-user-sign-ins-for-an-enterprise-app-in-azure-active-directory"></a><span data-ttu-id="4b5ee-103">Disabilitare gli accessi utente per un'app aziendale in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4b5ee-103">Disable user sign-ins for an enterprise app in Azure Active Directory</span></span>
<span data-ttu-id="4b5ee-104">Disabilitare un'applicazione aziendale in modo da impedirne l'accesso da parte degli utenti in Azure Active Directory (Azure AD) è un'operazione facile.</span><span class="sxs-lookup"><span data-stu-id="4b5ee-104">It's easy to disable an enterprise application so that no users may sign in to it in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="4b5ee-105">È necessario disporre delle autorizzazioni appropriate per gestire l'app aziendale ed essere amministratore globale della directory.</span><span class="sxs-lookup"><span data-stu-id="4b5ee-105">You must have the appropriate permissions to manage the enterprise app, and you must be global admin for the directory.</span></span>

## <a name="how-do-i-disable-user-sign-ins"></a><span data-ttu-id="4b5ee-106">Come è possibile disabilitare l'accesso degli utenti?</span><span class="sxs-lookup"><span data-stu-id="4b5ee-106">How do I disable user sign-ins?</span></span>
1. <span data-ttu-id="4b5ee-107">Accedere al [portale di Azure](https://portal.azure.com) con un account di amministratore globale per la directory.</span><span class="sxs-lookup"><span data-stu-id="4b5ee-107">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="4b5ee-108">Selezionare **Altri servizi**, immettere **Azure Active Directory** nella casella di testo e quindi selezionare **Invio**.</span><span class="sxs-lookup"><span data-stu-id="4b5ee-108">Select **More services**, enter **Azure Active Directory** in the text box, and then select **Enter**.</span></span>
3. <span data-ttu-id="4b5ee-109">Nel pannello **Azure Active Directory** -  ***nomedirectory***, vale a dire il pannello Azure AD per la directory che si sta gestendo, selezionare **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="4b5ee-109">On the **Azure Active Directory** -  ***directoryname*** blade (that is, the Azure AD blade for the directory you are managing), select **Enterprise applications**.</span></span>

    ![Apertura di app aziendali](./media/active-directory-coreapps-disable-app-azure-portal/open-enterprise-apps.png)
4. <span data-ttu-id="4b5ee-111">Nel pannello **Applicazioni aziendali** selezionare **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="4b5ee-111">On the **Enterprise applications** blade, select **All applications**.</span></span> <span data-ttu-id="4b5ee-112">Viene visualizzato un elenco di app che è possibile gestire.</span><span class="sxs-lookup"><span data-stu-id="4b5ee-112">You see a list of the apps you can manage.</span></span>
5. <span data-ttu-id="4b5ee-113">Nel pannello **Applicazioni aziendali - All applications** (Tutte le applicazioni) selezionare un'app.</span><span class="sxs-lookup"><span data-stu-id="4b5ee-113">On the **Enterprise applications - All applications** blade, select an app.</span></span>
6. <span data-ttu-id="4b5ee-114">Nel pannello ***nomeapp***, vale a dire il pannello con il nome dell'app selezionata nel titolo, selezionare **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="4b5ee-114">On the ***appname*** blade (that is, the blade with the name of the selected app in the title), select **Properties**.</span></span>

    ![Selezione del comando All applications (Tutte le applicazioni)](./media/active-directory-coreapps-disable-app-azure-portal/select-app.png)
7. <span data-ttu-id="4b5ee-116">Nel pannello ***nomeapp*** - **Proprietà** selezionare **No** per **Abilitata per l'accesso degli utenti?**</span><span class="sxs-lookup"><span data-stu-id="4b5ee-116">On the ***appname*** - **Properties** blade, select **No** for **Enabled for users to sign-in?**.</span></span>
8. <span data-ttu-id="4b5ee-117">Selezionare il comando **Salva** .</span><span class="sxs-lookup"><span data-stu-id="4b5ee-117">Select the **Save** command.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4b5ee-118">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4b5ee-118">Next steps</span></span>
* [<span data-ttu-id="4b5ee-119">Visualizzare tutti i gruppi personali</span><span class="sxs-lookup"><span data-stu-id="4b5ee-119">See all my groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="4b5ee-120">Assegnare un utente o gruppo a un'app aziendale</span><span class="sxs-lookup"><span data-stu-id="4b5ee-120">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)
* [<span data-ttu-id="4b5ee-121">Rimuovere l'assegnazione di un utente o un gruppo da un'app aziendale</span><span class="sxs-lookup"><span data-stu-id="4b5ee-121">Remove a user or group assignment from an enterprise app</span></span>](active-directory-coreapps-remove-assignment-azure-portal.md)
* [<span data-ttu-id="4b5ee-122">Modificare il nome o il logo di un'app aziendale</span><span class="sxs-lookup"><span data-stu-id="4b5ee-122">Change the name or logo of an enterprise app</span></span>](active-directory-coreapps-change-app-logo-user-azure-portal.md)
