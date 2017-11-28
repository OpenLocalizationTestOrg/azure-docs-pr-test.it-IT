---
title: aaaHow toocomplete una revisione accesso | Documenti Microsoft
description: "Dopo che è stata avviata una verifica di accesso in Azure AD Privileged Identity Management, informazioni su come toocomplete e Visualizza risultati di hello"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: abc2d3dd-afd5-42cf-8a17-6c11f5674c35
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: kgremban
ms.custom: pim
ms.openlocfilehash: f99ddf3ebcf80b51110326064d584f33d8e1679a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocomplete-an-access-review-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="bb15e-103">Come toocomplete esaminare un accesso in Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="bb15e-103">How toocomplete an access review in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="bb15e-104">Gli amministratori dei ruoli con privilegi possono esaminare l'accesso con privilegi dopo che è stata [avviata una verifica della sicurezza](active-directory-privileged-identity-management-how-to-start-security-review.md).</span><span class="sxs-lookup"><span data-stu-id="bb15e-104">Privileged role administrators can review privileged access once a [security review has been started](active-directory-privileged-identity-management-how-to-start-security-review.md).</span></span> <span data-ttu-id="bb15e-105">Azure AD Privileged Identity Management (PIM) invia automaticamente un messaggio di posta elettronica che richiede tooreview agli utenti l'accesso.</span><span class="sxs-lookup"><span data-stu-id="bb15e-105">Azure AD Privileged Identity Management (PIM) will automatically send an email prompting users tooreview their access.</span></span> <span data-ttu-id="bb15e-106">Se un utente non ha ottenuto un messaggio di posta elettronica, è possibile inviarli istruzioni hello in [come tooperform una sicurezza esaminare](active-directory-privileged-identity-management-how-to-perform-security-review.md).</span><span class="sxs-lookup"><span data-stu-id="bb15e-106">If a user did not get an email, you can send them hello instructions in [how tooperform a security review](active-directory-privileged-identity-management-how-to-perform-security-review.md).</span></span>

<span data-ttu-id="bb15e-107">Dopo la fase di revisione di sicurezza hello o tutti gli utenti di hello hanno terminato loro self-esaminare, seguire i passaggi hello in hello toomanage questo articolo e visualizzare i risultati di hello.</span><span class="sxs-lookup"><span data-stu-id="bb15e-107">After hello security review period is over, or all hello users have finished their self-review, follow hello steps in this article toomanage hello review and see hello results.</span></span>

## <a name="manage-security-reviews"></a><span data-ttu-id="bb15e-108">Gestire le verifiche della sicurezza</span><span class="sxs-lookup"><span data-stu-id="bb15e-108">Manage security reviews</span></span>
1. <span data-ttu-id="bb15e-109">Passare toohello [portale di Azure](https://portal.azure.com/) e seleziona hello **Azure AD Privileged Identity Management** applicazione nel dashboard.</span><span class="sxs-lookup"><span data-stu-id="bb15e-109">Go toohello [Azure portal](https://portal.azure.com/) and select hello **Azure AD Privileged Identity Management** application on your dashboard.</span></span>
2. <span data-ttu-id="bb15e-110">Seleziona hello **accedere revisioni** sezione dashboard hello.</span><span class="sxs-lookup"><span data-stu-id="bb15e-110">Select hello **Access reviews** section of hello dashboard.</span></span>
3. <span data-ttu-id="bb15e-111">Selezionare una revisione accesso hello che si desidera toomanage.</span><span class="sxs-lookup"><span data-stu-id="bb15e-111">Select hello access review that you want toomanage.</span></span>

<span data-ttu-id="bb15e-112">Nel Pannello di dettaglio della revisione accesso hello esistono un numero opzioni per la gestione di tale revisione.</span><span class="sxs-lookup"><span data-stu-id="bb15e-112">On hello access review's detail blade there are a number options for managing that review.</span></span>

![Schermata dei pulsanti di verifica dell'accesso PIM][1]

### <a name="remind"></a><span data-ttu-id="bb15e-114">Promemoria</span><span class="sxs-lookup"><span data-stu-id="bb15e-114">Remind</span></span>
<span data-ttu-id="bb15e-115">Se una revisione di accesso è configurata in modo che gli utenti di hello esaminare autonomamente, hello **promemoria** pulsante Invia una notifica.</span><span class="sxs-lookup"><span data-stu-id="bb15e-115">If an access review is set up so that hello users review themselves, hello **Remind** button sends out a notification.</span></span> 

### <a name="stop"></a><span data-ttu-id="bb15e-116">Arresto</span><span class="sxs-lookup"><span data-stu-id="bb15e-116">Stop</span></span>
<span data-ttu-id="bb15e-117">Tutte le revisioni accesso hanno una data di fine, ma è possibile utilizzare hello **arrestare** toofinish pulsante è all'inizio.</span><span class="sxs-lookup"><span data-stu-id="bb15e-117">All access reviews have an end date, but you can use hello **Stop** button toofinish it early.</span></span> <span data-ttu-id="bb15e-118">Se tutti gli utenti non sono stato implementati entro questo periodo, non sarà in grado di tooafter si arresta la revisione di hello.</span><span class="sxs-lookup"><span data-stu-id="bb15e-118">If any users haven't been reviewed by this time, they won't be able tooafter you stop hello review.</span></span> <span data-ttu-id="bb15e-119">Non è possibile riavviare una verifica dopo che è stata interrotta.</span><span class="sxs-lookup"><span data-stu-id="bb15e-119">You cannot restart a review after it's been stopped.</span></span>

### <a name="apply"></a><span data-ttu-id="bb15e-120">Applica</span><span class="sxs-lookup"><span data-stu-id="bb15e-120">Apply</span></span>
<span data-ttu-id="bb15e-121">Al termine di una revisione di accesso, sia perché si raggiunge la data di fine hello o interrotto manualmente, hello **applica** pulsante implementa risultato hello della revisione hello.</span><span class="sxs-lookup"><span data-stu-id="bb15e-121">After an access review is completed, either because you reached hello end date or stopped it manually, hello **Apply** button implements hello outcome of hello review.</span></span> <span data-ttu-id="bb15e-122">Se nella revisione di hello è stato negato l'accesso dell'utente, questo è passaggio hello rimuoverà l'assegnazione di ruolo.</span><span class="sxs-lookup"><span data-stu-id="bb15e-122">If a user's access was denied in hello review, this is hello step that will remove their role assignment.</span></span>  

### <a name="export"></a><span data-ttu-id="bb15e-123">Esporta</span><span class="sxs-lookup"><span data-stu-id="bb15e-123">Export</span></span>
<span data-ttu-id="bb15e-124">Se si desidera risultati hello tooapply di revisione della sicurezza hello manualmente, è possibile esportare revisione hello.</span><span class="sxs-lookup"><span data-stu-id="bb15e-124">If you want tooapply hello results of hello security review manually, you can export hello review.</span></span> <span data-ttu-id="bb15e-125">Hello **esportare** pulsante verrà avviato il download di un file CSV.</span><span class="sxs-lookup"><span data-stu-id="bb15e-125">hello **Export** button will start downloading a CSV file.</span></span> <span data-ttu-id="bb15e-126">È possibile gestire i risultati di hello in Excel o in altri programmi in cui aprire il file CSV.</span><span class="sxs-lookup"><span data-stu-id="bb15e-126">You can manage hello results in Excel or other programs that open CSV files.</span></span>

### <a name="delete"></a><span data-ttu-id="bb15e-127">Elimina</span><span class="sxs-lookup"><span data-stu-id="bb15e-127">Delete</span></span>
<span data-ttu-id="bb15e-128">Se non si è interessati in hello rivedere le ulteriori, eliminarlo.</span><span class="sxs-lookup"><span data-stu-id="bb15e-128">If you are not interested in hello review any further, delete it.</span></span> <span data-ttu-id="bb15e-129">Hello **eliminare** pulsante rimuove l'applicazione PIM hello hello revisione.</span><span class="sxs-lookup"><span data-stu-id="bb15e-129">hello **Delete** button removes hello review from hello PIM application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bb15e-130">È non verrà visualizzato un avviso prima che l'eliminazione viene eseguita, pertanto è necessario assicurarsi che si desidera toodelete che esaminare.</span><span class="sxs-lookup"><span data-stu-id="bb15e-130">You will not get a warning before deletion occurs, so be sure that you want toodelete that review.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="bb15e-131">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="bb15e-131">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-complete-review/PIM_review_buttons.png
