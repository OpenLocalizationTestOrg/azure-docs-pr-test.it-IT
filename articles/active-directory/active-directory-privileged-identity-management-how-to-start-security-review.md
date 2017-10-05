---
title: Come iniziare una verifica dell'accesso | Microsoft Docs
description: "Informazioni su come creare una verifica dell'accesso per le identità con privilegi con l'applicazione Azure Privileged Identity Management."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 3e52b731-55f4-4c8a-ba87-9fd34033f52f
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/04/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 2b516e2f05aa883c5e37f5864e5ee8a2b37d3a46
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-start-an-access-review-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="e748e-103">Come avviare una verifica dell'accesso in Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="e748e-103">How to start an access review in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="e748e-104">Le assegnazioni dei ruoli diventano "obsolete" quando gli utenti hanno accessi con privilegi di cui non necessitano più.</span><span class="sxs-lookup"><span data-stu-id="e748e-104">Role assignments become "stale" when users have privileged access that they don't need anymore.</span></span> <span data-ttu-id="e748e-105">Per ridurre il rischio associato alle assegnazioni dei ruoli obsolete, gli amministratori dei ruoli con privilegi devono esaminare periodicamente i ruoli assegnati agli utenti.</span><span class="sxs-lookup"><span data-stu-id="e748e-105">In order to reduce the risk associated with these stale role assignments, privileged role administrators should regularly review the roles that users have been given.</span></span> <span data-ttu-id="e748e-106">Questo documento illustra i passaggi per l'avvio di una verifica dell'accesso in Azure AD Privileged Identity Management (PIM).</span><span class="sxs-lookup"><span data-stu-id="e748e-106">This document covers the steps for starting an access review in Azure AD Privileged Identity Management (PIM).</span></span>

## <a name="start-an-access-review"></a><span data-ttu-id="e748e-107">Avviare una verifica dell'accesso</span><span class="sxs-lookup"><span data-stu-id="e748e-107">Start an access review</span></span>
> [!NOTE]
> <span data-ttu-id="e748e-108">Se l'applicazione PIM non è stata aggiunta al dashboard nel portale di Azure, vedere i passaggi descritti in [Introduzione ad Azure AD Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md)</span><span class="sxs-lookup"><span data-stu-id="e748e-108">If you haven't added the PIM application to your dashboard in the Azure portal, see the steps in  [Getting Started with Azure Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md)</span></span>
> 
> 

<span data-ttu-id="e748e-109">Nella pagina principale dell'applicazione PIM sono disponibili tre opzioni per avviare una verifica dell'accesso:</span><span class="sxs-lookup"><span data-stu-id="e748e-109">From the PIM application main page, there are three ways to start an access review:</span></span>

* <span data-ttu-id="e748e-110">**Verifiche di accesso** > **Aggiungi**</span><span class="sxs-lookup"><span data-stu-id="e748e-110">**Access reviews** > **Add**</span></span>
* <span data-ttu-id="e748e-111">**Ruoli** > **Verifica**</span><span class="sxs-lookup"><span data-stu-id="e748e-111">**Roles** > **Review** button</span></span>
* <span data-ttu-id="e748e-112">Selezionare il ruolo specifico da verificare dall'elenco dei ruoli > **Verifica**</span><span class="sxs-lookup"><span data-stu-id="e748e-112">Select the specific role to be reviewed from the roles list > **Review** button</span></span>

<span data-ttu-id="e748e-113">Quando si fa clic sul pulsante **Verifica**, viene visualizzato il pannello **Inizia una verifica di accesso**.</span><span class="sxs-lookup"><span data-stu-id="e748e-113">When you click on the **Review** button, the **Start an access review** blade appears.</span></span> <span data-ttu-id="e748e-114">In questo pannello configurare la verifica assegnando un nome e un limite temporale, scegliere un ruolo da verificare e decidere chi eseguirà la verifica.</span><span class="sxs-lookup"><span data-stu-id="e748e-114">On this blade, you're going to configure the review with a name and time limit, choose a role to review, and decide who will perform the review.</span></span>

![Schermata Inizia una verifica di accesso][1]

### <a name="configure-the-review"></a><span data-ttu-id="e748e-116">Configurare la verifica</span><span class="sxs-lookup"><span data-stu-id="e748e-116">Configure the review</span></span>
<span data-ttu-id="e748e-117">Per creare una verifica di accesso, è necessario assegnare un nome e impostare le date di inizio e di fine.</span><span class="sxs-lookup"><span data-stu-id="e748e-117">To create an access review, you need to name it and set a start and end date.</span></span>

![Schermata di configurazione della verifica][2]

<span data-ttu-id="e748e-119">Definire una durata della verifica che consenta agli utenti di completare l'operazione.</span><span class="sxs-lookup"><span data-stu-id="e748e-119">Make the length of the review long enough for users to complete it.</span></span> <span data-ttu-id="e748e-120">Se la verifica termina prima della data di fine, è sempre possibile arrestare la verifica in anticipo.</span><span class="sxs-lookup"><span data-stu-id="e748e-120">If you finish before the end date, you can always stop the review early.</span></span>

### <a name="choose-a-role-to-review"></a><span data-ttu-id="e748e-121">Scegliere un ruolo da verificare</span><span class="sxs-lookup"><span data-stu-id="e748e-121">Choose a role to review</span></span>
<span data-ttu-id="e748e-122">Ogni verifica è incentrata su un solo ruolo.</span><span class="sxs-lookup"><span data-stu-id="e748e-122">Each review focuses on only one role.</span></span> <span data-ttu-id="e748e-123">A meno che non si abbia avviato la verifica di accesso dal pannello di un ruolo specifico, è ora necessario scegliere un ruolo.</span><span class="sxs-lookup"><span data-stu-id="e748e-123">Unless you started the access review from a specific role blade, you'll need to choose a role now.</span></span>

1. <span data-ttu-id="e748e-124">Passare a **Verifica l'appartenenza ai ruoli**</span><span class="sxs-lookup"><span data-stu-id="e748e-124">Navigate to **Review role membership**</span></span>
   
    ![Schermata Verifica l'appartenenza ai ruoli][3]
2. <span data-ttu-id="e748e-126">Scegliere un ruolo dall'elenco.</span><span class="sxs-lookup"><span data-stu-id="e748e-126">Choose one role from the list.</span></span>

### <a name="decide-who-will-perform-the-review"></a><span data-ttu-id="e748e-127">Decidere chi eseguirà la verifica</span><span class="sxs-lookup"><span data-stu-id="e748e-127">Decide who will perform the review</span></span>
<span data-ttu-id="e748e-128">Sono disponibili tre opzioni per l'esecuzione di una verifica.</span><span class="sxs-lookup"><span data-stu-id="e748e-128">There are three options for performing a review.</span></span> <span data-ttu-id="e748e-129">La revisione può essere assegnata a un altro utente, essere eseguita personalmente oppure ogni utente può verificare il proprio accesso.</span><span class="sxs-lookup"><span data-stu-id="e748e-129">You can assign the review to someone else to complete, you can do it yourself, or you can have each user review their own access.</span></span>

1. <span data-ttu-id="e748e-130">Passare a **Selezionare i revisori**</span><span class="sxs-lookup"><span data-stu-id="e748e-130">Navigate to **Select reviewers**</span></span>
   
    ![Schermata Selezionare i revisori][4]
2. <span data-ttu-id="e748e-132">Scegliere una delle opzioni disponibili:</span><span class="sxs-lookup"><span data-stu-id="e748e-132">Choose one of the options:</span></span>
   
   * <span data-ttu-id="e748e-133">**Seleziona il revisore**: usare questa opzione quando non è noto chi abbia bisogno dell'accesso.</span><span class="sxs-lookup"><span data-stu-id="e748e-133">**Select reviewer**: Use this option when you don't know who needs access.</span></span> <span data-ttu-id="e748e-134">Con questa opzione è possibile assegnare l'esecuzione della revisione a un proprietario delle risorse o a un gestore del gruppo.</span><span class="sxs-lookup"><span data-stu-id="e748e-134">With this option, you can assign the review to a resource owner or group manager to complete.</span></span>
   * <span data-ttu-id="e748e-135">**Me**(Io): utile se si vuole visualizzare in anteprima come funzionano le verifiche dell'accesso o se si vuole eseguire una verifica per conto di utenti che non possono eseguire questa operazione.</span><span class="sxs-lookup"><span data-stu-id="e748e-135">**Me**: Useful if you want to preview how access reviews work, or you want to review on behalf of people who can't.</span></span>
   * <span data-ttu-id="e748e-136">**Members review themselves**(I membri verificano se stessi): usare questa opzione per fare in modo che gli utenti verifichino le proprie assegnazioni di ruoli.</span><span class="sxs-lookup"><span data-stu-id="e748e-136">**Members review themselves**: Use this option to have the users review their own role assignments.</span></span>

### <a name="start-the-review"></a><span data-ttu-id="e748e-137">Avviare la verifica</span><span class="sxs-lookup"><span data-stu-id="e748e-137">Start the review</span></span>
<span data-ttu-id="e748e-138">Infine è disponibile l'opzione per richiedere agli utenti di fornire un motivo se approvano l'accesso.</span><span class="sxs-lookup"><span data-stu-id="e748e-138">Finally, you have the option to require that users provide a reason if they approve their access.</span></span> <span data-ttu-id="e748e-139">Se si vuole, aggiungere una descrizione della verifica e selezionare **Start**(Avvia).</span><span class="sxs-lookup"><span data-stu-id="e748e-139">Add a description of the review if you like, and select **Start**.</span></span>

<span data-ttu-id="e748e-140">È necessario informare gli utenti che è presente una verifica dell'accesso in attesa e illustrare [come eseguire una verifica dell'accesso](active-directory-privileged-identity-management-how-to-perform-security-review.md).</span><span class="sxs-lookup"><span data-stu-id="e748e-140">Make sure you let your users know that there's an access review waiting for them, and show them [How to perform an access review](active-directory-privileged-identity-management-how-to-perform-security-review.md).</span></span>

## <a name="manage-the-access-review"></a><span data-ttu-id="e748e-141">Gestire la verifica di accesso</span><span class="sxs-lookup"><span data-stu-id="e748e-141">Manage the access review</span></span>
<span data-ttu-id="e748e-142">È possibile tenere traccia dello stato di avanzamento delle verifiche eseguite dai revisori nella sezione Verifiche di accesso del dashboard di Azure AD PIM.</span><span class="sxs-lookup"><span data-stu-id="e748e-142">You can track the progress as the reviewers complete their reviews in the Azure AD PIM dashboard, in the access reviews section.</span></span> <span data-ttu-id="e748e-143">Nessun diritto di accesso verrà modificato nella directory fino al [completamento della verifica](active-directory-privileged-identity-management-how-to-complete-review.md).</span><span class="sxs-lookup"><span data-stu-id="e748e-143">No access rights will be changed in the directory until [the review completes](active-directory-privileged-identity-management-how-to-complete-review.md).</span></span>

<span data-ttu-id="e748e-144">Fino al termine del periodo di verifica, è possibile ricordare agli utenti di completare la verifica o arrestare la verifica in anticipo nella sezione Verifiche di accesso.</span><span class="sxs-lookup"><span data-stu-id="e748e-144">Until the review period is over, you can remind users to complete their review, or stop the review early from the access reviews section.</span></span>

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="pim-table-of-contents"></a><span data-ttu-id="e748e-145">Sommario PIM</span><span class="sxs-lookup"><span data-stu-id="e748e-145">PIM Table of Contents</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_start_review.png
[2]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_configure.png
[3]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_role.png
[4]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_reviewers.png
