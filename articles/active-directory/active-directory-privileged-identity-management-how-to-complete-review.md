---
title: Come completare una verifica dell'accesso | Documentazione Microsoft
description: "Dopo che è stata avviata una verifica di accesso in Azure AD Privileged Identity Management, leggere le informazioni su come completare la verifica e visualizzare i risultati"
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
ms.openlocfilehash: ca2a1c7c287e4cf6b1b50cfb0068861b6f525596
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-complete-an-access-review-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="8edcd-103">Come completare una verifica dell'accesso in Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="8edcd-103">How to complete an access review in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="8edcd-104">Gli amministratori dei ruoli con privilegi possono esaminare l'accesso con privilegi dopo che è stata [avviata una verifica della sicurezza](active-directory-privileged-identity-management-how-to-start-security-review.md).</span><span class="sxs-lookup"><span data-stu-id="8edcd-104">Privileged role administrators can review privileged access once a [security review has been started](active-directory-privileged-identity-management-how-to-start-security-review.md).</span></span> <span data-ttu-id="8edcd-105">Azure AD Privileged Identity Management (PIM) invia automaticamente un messaggio di posta elettronica che richiede agli utenti di controllare l'accesso.</span><span class="sxs-lookup"><span data-stu-id="8edcd-105">Azure AD Privileged Identity Management (PIM) will automatically send an email prompting users to review their access.</span></span> <span data-ttu-id="8edcd-106">Agli utenti che non hanno ricevuto il messaggio di posta elettronica, è possibile inviare le istruzioni descritte in [Come eseguire una verifica della sicurezza](active-directory-privileged-identity-management-how-to-perform-security-review.md).</span><span class="sxs-lookup"><span data-stu-id="8edcd-106">If a user did not get an email, you can send them the instructions in [how to perform a security review](active-directory-privileged-identity-management-how-to-perform-security-review.md).</span></span>

<span data-ttu-id="8edcd-107">Trascorso il periodo della verifica della sicurezza o al termine della verifica automatica di tutti gli utenti, seguire la procedura descritta in questo articolo per gestire la verifica e visualizzare i risultati.</span><span class="sxs-lookup"><span data-stu-id="8edcd-107">After the security review period is over, or all the users have finished their self-review, follow the steps in this article to manage the review and see the results.</span></span>

## <a name="manage-security-reviews"></a><span data-ttu-id="8edcd-108">Gestire le verifiche della sicurezza</span><span class="sxs-lookup"><span data-stu-id="8edcd-108">Manage security reviews</span></span>
1. <span data-ttu-id="8edcd-109">Accedere al [portale di Azure](https://portal.azure.com/) e selezionare l'applicazione **Azure AD Privileged Identity Management** nel dashboard.</span><span class="sxs-lookup"><span data-stu-id="8edcd-109">Go to the [Azure portal](https://portal.azure.com/) and select the **Azure AD Privileged Identity Management** application on your dashboard.</span></span>
2. <span data-ttu-id="8edcd-110">Selezionare la sezione **Verifiche dell'accesso** del dashboard.</span><span class="sxs-lookup"><span data-stu-id="8edcd-110">Select the **Access reviews** section of the dashboard.</span></span>
3. <span data-ttu-id="8edcd-111">Fare clic sulla verifica dell'accesso che si vuole gestire.</span><span class="sxs-lookup"><span data-stu-id="8edcd-111">Select the access review that you want to manage.</span></span>

<span data-ttu-id="8edcd-112">Nel pannello dei dettagli della verifica dell'accesso sono disponibili alcune opzioni per la gestione della verifica.</span><span class="sxs-lookup"><span data-stu-id="8edcd-112">On the access review's detail blade there are a number options for managing that review.</span></span>

![Schermata dei pulsanti di verifica dell'accesso PIM][1]

### <a name="remind"></a><span data-ttu-id="8edcd-114">Promemoria</span><span class="sxs-lookup"><span data-stu-id="8edcd-114">Remind</span></span>
<span data-ttu-id="8edcd-115">Se una verifica di accesso è stata impostata in modo che gli utenti verifichino se stessi, il pulsante **Promemoria** invia una notifica.</span><span class="sxs-lookup"><span data-stu-id="8edcd-115">If an access review is set up so that the users review themselves, the **Remind** button sends out a notification.</span></span> 

### <a name="stop"></a><span data-ttu-id="8edcd-116">Arresto</span><span class="sxs-lookup"><span data-stu-id="8edcd-116">Stop</span></span>
<span data-ttu-id="8edcd-117">Tutte le verifiche di accesso hanno una data di fine, ma il pulsante **Interrompi** consente di completare l'operazione in anticipo.</span><span class="sxs-lookup"><span data-stu-id="8edcd-117">All access reviews have an end date, but you can use the **Stop** button to finish it early.</span></span> <span data-ttu-id="8edcd-118">Eventuali utenti non sottoposti a verifica fino a questo momento, non potranno essere controllati dopo l'interruzione della verifica.</span><span class="sxs-lookup"><span data-stu-id="8edcd-118">If any users haven't been reviewed by this time, they won't be able to after you stop the review.</span></span> <span data-ttu-id="8edcd-119">Non è possibile riavviare una verifica dopo che è stata interrotta.</span><span class="sxs-lookup"><span data-stu-id="8edcd-119">You cannot restart a review after it's been stopped.</span></span>

### <a name="apply"></a><span data-ttu-id="8edcd-120">Applica</span><span class="sxs-lookup"><span data-stu-id="8edcd-120">Apply</span></span>
<span data-ttu-id="8edcd-121">Al termine di una verifica di accesso in corrispondenza della data di fine o in caso di interruzione manuale, il pulsante **Applica** implementa il risultato della verifica.</span><span class="sxs-lookup"><span data-stu-id="8edcd-121">After an access review is completed, either because you reached the end date or stopped it manually, the **Apply** button implements the outcome of the review.</span></span> <span data-ttu-id="8edcd-122">Se l'accesso di un utente è stato negato nel corso della verifica, questo passaggio consente di rimuovere l'assegnazione di ruolo.</span><span class="sxs-lookup"><span data-stu-id="8edcd-122">If a user's access was denied in the review, this is the step that will remove their role assignment.</span></span>  

### <a name="export"></a><span data-ttu-id="8edcd-123">Esporta</span><span class="sxs-lookup"><span data-stu-id="8edcd-123">Export</span></span>
<span data-ttu-id="8edcd-124">Per applicare manualmente i risultati della verifica della sicurezza, è possibile esportare la verifica.</span><span class="sxs-lookup"><span data-stu-id="8edcd-124">If you want to apply the results of the security review manually, you can export the review.</span></span> <span data-ttu-id="8edcd-125">Il pulsante **Esporta** avvia il download di un file con estensione csv.</span><span class="sxs-lookup"><span data-stu-id="8edcd-125">The **Export** button will start downloading a CSV file.</span></span> <span data-ttu-id="8edcd-126">È possibile gestire i risultati in Excel o in altri programmi in grado di aprire i file con estensione csv.</span><span class="sxs-lookup"><span data-stu-id="8edcd-126">You can manage the results in Excel or other programs that open CSV files.</span></span>

### <a name="delete"></a><span data-ttu-id="8edcd-127">Delete</span><span class="sxs-lookup"><span data-stu-id="8edcd-127">Delete</span></span>
<span data-ttu-id="8edcd-128">Se la verifica non è più necessaria, eliminarla.</span><span class="sxs-lookup"><span data-stu-id="8edcd-128">If you are not interested in the review any further, delete it.</span></span> <span data-ttu-id="8edcd-129">Il pulsante **Elimina** rimuove la verifica dall'applicazione PIM.</span><span class="sxs-lookup"><span data-stu-id="8edcd-129">The **Delete** button removes the review from the PIM application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8edcd-130">Poiché non verrà visualizzato alcun avviso prima dell'eliminazione, assicurarsi di voler eliminare la verifica.</span><span class="sxs-lookup"><span data-stu-id="8edcd-130">You will not get a warning before deletion occurs, so be sure that you want to delete that review.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="8edcd-131">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8edcd-131">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-complete-review/PIM_review_buttons.png
