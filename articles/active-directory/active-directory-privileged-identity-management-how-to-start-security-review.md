---
title: aaaHow toostart una revisione accesso | Documenti Microsoft
description: "Informazioni su come toocreate esaminare un accesso per l'identità con privilegi con hello applicazione Azure Privileged Identity Management."
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
ms.openlocfilehash: 24feac307f77c69b5d68d6ae0623dbcb52416b01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toostart-an-access-review-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="141fa-103">Come toostart esaminare un accesso in Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="141fa-103">How toostart an access review in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="141fa-104">Le assegnazioni dei ruoli diventano "obsolete" quando gli utenti hanno accessi con privilegi di cui non necessitano più.</span><span class="sxs-lookup"><span data-stu-id="141fa-104">Role assignments become "stale" when users have privileged access that they don't need anymore.</span></span> <span data-ttu-id="141fa-105">Ordine tooreduce hello rischio associato a queste assegnazioni di ruolo non aggiornato, gli amministratori di ruolo con privilegi devono esaminare regolarmente ruoli hello che gli utenti sono stati assegnati.</span><span class="sxs-lookup"><span data-stu-id="141fa-105">In order tooreduce hello risk associated with these stale role assignments, privileged role administrators should regularly review hello roles that users have been given.</span></span> <span data-ttu-id="141fa-106">Questo documento descrive i passaggi di hello per l'avvio di una revisione dell'accesso in Azure AD Privileged Identity Management (PIM).</span><span class="sxs-lookup"><span data-stu-id="141fa-106">This document covers hello steps for starting an access review in Azure AD Privileged Identity Management (PIM).</span></span>

## <a name="start-an-access-review"></a><span data-ttu-id="141fa-107">Avviare una verifica dell'accesso</span><span class="sxs-lookup"><span data-stu-id="141fa-107">Start an access review</span></span>
> [!NOTE]
> <span data-ttu-id="141fa-108">Se non si aggiunti dashboard tooyour dell'applicazione di PIM hello in hello portale di Azure, vedere la procedura di hello in [Introduzione a Azure Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md)</span><span class="sxs-lookup"><span data-stu-id="141fa-108">If you haven't added hello PIM application tooyour dashboard in hello Azure portal, see hello steps in  [Getting Started with Azure Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md)</span></span>
> 
> 

<span data-ttu-id="141fa-109">Dalla pagina principale dell'applicazione PIM hello, sono disponibili tre modi toostart una revisione di accesso:</span><span class="sxs-lookup"><span data-stu-id="141fa-109">From hello PIM application main page, there are three ways toostart an access review:</span></span>

* <span data-ttu-id="141fa-110">**Verifiche di accesso** > **Aggiungi**</span><span class="sxs-lookup"><span data-stu-id="141fa-110">**Access reviews** > **Add**</span></span>
* <span data-ttu-id="141fa-111">**Ruoli** > **Verifica**</span><span class="sxs-lookup"><span data-stu-id="141fa-111">**Roles** > **Review** button</span></span>
* <span data-ttu-id="141fa-112">Rivisto toobe ruolo specifico hello selezionare dall'elenco di ruoli hello > **revisione** pulsante</span><span class="sxs-lookup"><span data-stu-id="141fa-112">Select hello specific role toobe reviewed from hello roles list > **Review** button</span></span>

<span data-ttu-id="141fa-113">Quando fa clic su hello **esaminare** pulsante hello **avviare una verifica di accesso** pannello viene visualizzato.</span><span class="sxs-lookup"><span data-stu-id="141fa-113">When you click on hello **Review** button, hello **Start an access review** blade appears.</span></span> <span data-ttu-id="141fa-114">In questo pannello, in corso la revisione di hello tooconfigure con un nome e limite di tempo, scegliere un ruolo tooreview e decidere che eseguirà la revisione di hello.</span><span class="sxs-lookup"><span data-stu-id="141fa-114">On this blade, you're going tooconfigure hello review with a name and time limit, choose a role tooreview, and decide who will perform hello review.</span></span>

![Schermata Inizia una verifica di accesso][1]

### <a name="configure-hello-review"></a><span data-ttu-id="141fa-116">Configurare la revisione di hello</span><span class="sxs-lookup"><span data-stu-id="141fa-116">Configure hello review</span></span>
<span data-ttu-id="141fa-117">esaminare un accesso toocreate, è necessario tooname e impostare una data di inizio e fine.</span><span class="sxs-lookup"><span data-stu-id="141fa-117">toocreate an access review, you need tooname it and set a start and end date.</span></span>

![Schermata di configurazione della verifica][2]

<span data-ttu-id="141fa-119">Verificare che lunghezza hello di hello viene rivisto un tempo sufficiente per gli utenti toocomplete.</span><span class="sxs-lookup"><span data-stu-id="141fa-119">Make hello length of hello review long enough for users toocomplete it.</span></span> <span data-ttu-id="141fa-120">Se termina prima della data di fine hello, è possibile arrestare sempre la revisione di hello in anticipo.</span><span class="sxs-lookup"><span data-stu-id="141fa-120">If you finish before hello end date, you can always stop hello review early.</span></span>

### <a name="choose-a-role-tooreview"></a><span data-ttu-id="141fa-121">Scegliere un ruolo tooreview</span><span class="sxs-lookup"><span data-stu-id="141fa-121">Choose a role tooreview</span></span>
<span data-ttu-id="141fa-122">Ogni verifica è incentrata su un solo ruolo.</span><span class="sxs-lookup"><span data-stu-id="141fa-122">Each review focuses on only one role.</span></span> <span data-ttu-id="141fa-123">A meno che non è stato avviato hello accesso revisione dal pannello ruolo specifico, è necessario ora toochoose un ruolo.</span><span class="sxs-lookup"><span data-stu-id="141fa-123">Unless you started hello access review from a specific role blade, you'll need toochoose a role now.</span></span>

1. <span data-ttu-id="141fa-124">Passare troppo**esaminare l'appartenenza al ruolo**</span><span class="sxs-lookup"><span data-stu-id="141fa-124">Navigate too**Review role membership**</span></span>
   
    ![Schermata Verifica l'appartenenza ai ruoli][3]
2. <span data-ttu-id="141fa-126">Scegliere un ruolo dall'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="141fa-126">Choose one role from hello list.</span></span>

### <a name="decide-who-will-perform-hello-review"></a><span data-ttu-id="141fa-127">Decidere chi eseguirà la revisione di hello</span><span class="sxs-lookup"><span data-stu-id="141fa-127">Decide who will perform hello review</span></span>
<span data-ttu-id="141fa-128">Sono disponibili tre opzioni per l'esecuzione di una verifica.</span><span class="sxs-lookup"><span data-stu-id="141fa-128">There are three options for performing a review.</span></span> <span data-ttu-id="141fa-129">È possibile assegnare hello revisione toosomeone toocomplete altro, è possibile farlo manualmente oppure è possibile esaminare le proprie accesso avere ogni utente.</span><span class="sxs-lookup"><span data-stu-id="141fa-129">You can assign hello review toosomeone else toocomplete, you can do it yourself, or you can have each user review their own access.</span></span>

1. <span data-ttu-id="141fa-130">Passare troppo**selezionare revisori**</span><span class="sxs-lookup"><span data-stu-id="141fa-130">Navigate too**Select reviewers**</span></span>
   
    ![Schermata Selezionare i revisori][4]
2. <span data-ttu-id="141fa-132">Scegliere una delle opzioni di hello:</span><span class="sxs-lookup"><span data-stu-id="141fa-132">Choose one of hello options:</span></span>
   
   * <span data-ttu-id="141fa-133">**Seleziona il revisore**: usare questa opzione quando non è noto chi abbia bisogno dell'accesso.</span><span class="sxs-lookup"><span data-stu-id="141fa-133">**Select reviewer**: Use this option when you don't know who needs access.</span></span> <span data-ttu-id="141fa-134">Con questa opzione, è possibile assegnare proprietario della risorsa hello revisione tooa o toocomplete gestione gruppo.</span><span class="sxs-lookup"><span data-stu-id="141fa-134">With this option, you can assign hello review tooa resource owner or group manager toocomplete.</span></span>
   * <span data-ttu-id="141fa-135">**Me**: utile se si desidera toopreview come accesso revisioni del lavoro o se si desidera tooreview per conto di utenti che non è possibile.</span><span class="sxs-lookup"><span data-stu-id="141fa-135">**Me**: Useful if you want toopreview how access reviews work, or you want tooreview on behalf of people who can't.</span></span>
   * <span data-ttu-id="141fa-136">**I membri esaminare stessi**: usare questa revisione agli utenti di opzione toohave hello assegnazioni di ruolo.</span><span class="sxs-lookup"><span data-stu-id="141fa-136">**Members review themselves**: Use this option toohave hello users review their own role assignments.</span></span>

### <a name="start-hello-review"></a><span data-ttu-id="141fa-137">Avviare hello revisione</span><span class="sxs-lookup"><span data-stu-id="141fa-137">Start hello review</span></span>
<span data-ttu-id="141fa-138">Infine, è necessario toorequire opzione hello agli utenti di fornire un motivo se approvare l'accesso.</span><span class="sxs-lookup"><span data-stu-id="141fa-138">Finally, you have hello option toorequire that users provide a reason if they approve their access.</span></span> <span data-ttu-id="141fa-139">Se si desidera aggiungere una descrizione della revisione hello e selezionare **avviare**.</span><span class="sxs-lookup"><span data-stu-id="141fa-139">Add a description of hello review if you like, and select **Start**.</span></span>

<span data-ttu-id="141fa-140">Assicurarsi che si consente agli utenti a indicare che una revisione accesso attenderne e visualizzarle [come tooperform un accesso esaminare](active-directory-privileged-identity-management-how-to-perform-security-review.md).</span><span class="sxs-lookup"><span data-stu-id="141fa-140">Make sure you let your users know that there's an access review waiting for them, and show them [How tooperform an access review](active-directory-privileged-identity-management-how-to-perform-security-review.md).</span></span>

## <a name="manage-hello-access-review"></a><span data-ttu-id="141fa-141">Gestire hello accesso revisione</span><span class="sxs-lookup"><span data-stu-id="141fa-141">Manage hello access review</span></span>
<span data-ttu-id="141fa-142">È possibile monitorare lo stato di avanzamento hello come revisori hello completare le revisioni nel dashboard di Azure AD PIM hello, sezione esaminate in hello.</span><span class="sxs-lookup"><span data-stu-id="141fa-142">You can track hello progress as hello reviewers complete their reviews in hello Azure AD PIM dashboard, in hello access reviews section.</span></span> <span data-ttu-id="141fa-143">Nessun diritto di accesso verrà modificato nella directory hello finché [revisione hello completa](active-directory-privileged-identity-management-how-to-complete-review.md).</span><span class="sxs-lookup"><span data-stu-id="141fa-143">No access rights will be changed in hello directory until [hello review completes](active-directory-privileged-identity-management-how-to-complete-review.md).</span></span>

<span data-ttu-id="141fa-144">Fino al periodo di revisione hello, è possibile tenere la revisione toocomplete gli utenti o arresto hello revisione tempestivamente dall'accesso di hello esamina sezione.</span><span class="sxs-lookup"><span data-stu-id="141fa-144">Until hello review period is over, you can remind users toocomplete their review, or stop hello review early from hello access reviews section.</span></span>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="pim-table-of-contents"></a><span data-ttu-id="141fa-145">Sommario PIM</span><span class="sxs-lookup"><span data-stu-id="141fa-145">PIM Table of Contents</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_start_review.png
[2]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_configure.png
[3]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_role.png
[4]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_reviewers.png
