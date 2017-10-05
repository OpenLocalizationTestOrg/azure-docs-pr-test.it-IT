---
title: Come eseguire una verifica dell'accesso | Documentazione Microsoft
description: Informazioni su come eseguire una verifica con l'applicazione Azure Privileged Identity Management.
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 49ee2feb-7d2e-4acf-82c1-40ff23062862
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: a98ed60221eeba1d9c92df846aeae2deafb8ae60
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-perform-an-access-review-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="351ec-103">Come eseguire una verifica dell'accesso in Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="351ec-103">How to perform an access review in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="351ec-104">Azure Active Directory (AD) Privileged Identity Management semplifica la gestione aziendale dell'accesso con privilegi alle risorse in Azure AD e in altri Microsoft Online Services, ad esempio Office 365 o Microsoft Intune.</span><span class="sxs-lookup"><span data-stu-id="351ec-104">Azure Active Directory (AD) Privileged Identity Management simplifies how enterprises manage privileged access to resources in Azure AD and other Microsoft online services like Office 365 or Microsoft Intune.</span></span>  

<span data-ttu-id="351ec-105">Se si è stati assegnati a un ruolo amministrativo, è possibile che l'amministratore dei ruoli con privilegi dell'organizzazione richieda di confermare a intervalli regolari che il ruolo sia ancora necessario.</span><span class="sxs-lookup"><span data-stu-id="351ec-105">If you are assigned to an administrative role, your organization's privileged role administrator may ask you to regularly confirm that you still need that role for your job.</span></span> <span data-ttu-id="351ec-106">È possibile che si riceva un messaggio di posta elettronica contenente un collegamento oppure accedere direttamente al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="351ec-106">You might get an email that includes a link, or you can go straight to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="351ec-107">Per eseguire una verifica automatica dei ruoli assegnati, seguire la procedura descritta in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="351ec-107">Follow the steps in this article to perform a self-review of your assigned roles.</span></span>

<span data-ttu-id="351ec-108">Per gli amministratori dei ruoli con privilegi interessati alle verifiche dell'accesso sono disponibili altre informazioni in [Come avviare una verifica dell'accesso in Azure AD Privileged Identity Management](active-directory-privileged-identity-management-how-to-start-security-review.md).</span><span class="sxs-lookup"><span data-stu-id="351ec-108">If you're a privileged role administrator interested in access reviews, get more details at [How to start an access review](active-directory-privileged-identity-management-how-to-start-security-review.md).</span></span>

## <a name="add-the-privileged-identity-management-application"></a><span data-ttu-id="351ec-109">Aggiungere l'applicazione Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="351ec-109">Add the Privileged Identity Management application</span></span>
<span data-ttu-id="351ec-110">Per eseguire la verifica, è possibile usare l'applicazione Azure AD Privileged Identity Management (PIM) nel [portale di Azure](https://portal.azure.com/) .</span><span class="sxs-lookup"><span data-stu-id="351ec-110">You can use the Azure AD Privileged Identity Management (PIM) application in the [Azure portal](https://portal.azure.com/) to perform your review.</span></span>  <span data-ttu-id="351ec-111">Se l'applicazione Azure AD Privileged Identity Management non è disponibile nel portale, seguire questa procedura per iniziare.</span><span class="sxs-lookup"><span data-stu-id="351ec-111">If you don't have the Azure AD Privileged Identity Management application on your portal, follow these steps to get started.</span></span>

1. <span data-ttu-id="351ec-112">Accedere al [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="351ec-112">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="351ec-113">Selezionare il nome utente nell'angolo superiore destro del portale di Azure e quindi selezionare la directory da usare.</span><span class="sxs-lookup"><span data-stu-id="351ec-113">Select your username in the upper right-hand corner of the Azure portal, and select the directory where you will you be operating.</span></span>
3. <span data-ttu-id="351ec-114">Selezionare **Altri servizi** e usare la casella di testo Filtro per cercare **Azure AD Privileged Identity Management**.</span><span class="sxs-lookup"><span data-stu-id="351ec-114">Select **More services** and use the Filter textbox to search for **Azure AD Privileged Identity Management**.</span></span>
4. <span data-ttu-id="351ec-115">Selezionare **Aggiungi al dashboard** e quindi fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="351ec-115">Check **Pin to dashboard** and then click **Create**.</span></span> <span data-ttu-id="351ec-116">Verrà aperta l'applicazione Privileged Identity Management.</span><span class="sxs-lookup"><span data-stu-id="351ec-116">The Privileged Identity Management application will open.</span></span>

## <a name="approve-or-deny-access"></a><span data-ttu-id="351ec-117">Approvare o negare l'accesso</span><span class="sxs-lookup"><span data-stu-id="351ec-117">Approve or deny access</span></span>
<span data-ttu-id="351ec-118">L'approvazione o la negazione dell'accesso indica semplicemente al revisore se si sta usando ancora il ruolo.</span><span class="sxs-lookup"><span data-stu-id="351ec-118">When you approve or deny access, you're just telling the reviewer whether you still use this role or not.</span></span> <span data-ttu-id="351ec-119">Scegliere **Approva** se si vuole restare nel ruolo o **Nega** se l'accesso non è più necessario.</span><span class="sxs-lookup"><span data-stu-id="351ec-119">Choose **Approve** if you want to stay in the role, or **Deny** if you don't need the access anymore.</span></span> <span data-ttu-id="351ec-120">Lo stato cambierà solo dopo il revisore avrà applicato i risultati.</span><span class="sxs-lookup"><span data-stu-id="351ec-120">Your status won't change right away, until the reviewer applies the results.</span></span>
<span data-ttu-id="351ec-121">Seguire questa procedura per trovare e completare la verifica dell'accesso:</span><span class="sxs-lookup"><span data-stu-id="351ec-121">Follow these steps to find and complete the access review:</span></span>

1. <span data-ttu-id="351ec-122">Nell'applicazione PIM selezionare **Verifica dell'accesso con privilegi**.</span><span class="sxs-lookup"><span data-stu-id="351ec-122">In the PIM application, select **Review privileged access**.</span></span> <span data-ttu-id="351ec-123">Eventuali verifiche di accesso in sospeso verranno visualizzate nel pannello Verifiche di accesso di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="351ec-123">If you have any pending access reviews, they appear in the Azure AD Access reviews blade.</span></span>
2. <span data-ttu-id="351ec-124">Selezionare la verifica da completare.</span><span class="sxs-lookup"><span data-stu-id="351ec-124">Select the review you want to complete.</span></span>
3. <span data-ttu-id="351ec-125">A meno che non abbia creato la verifica, l'utente verrà visualizzato come unico utente nella verifica.</span><span class="sxs-lookup"><span data-stu-id="351ec-125">Unless you created the review, you appear as the only user in the review.</span></span> <span data-ttu-id="351ec-126">Selezionare il segno di spunta accanto al nome.</span><span class="sxs-lookup"><span data-stu-id="351ec-126">Select the check mark next to your name.</span></span>
4. <span data-ttu-id="351ec-127">Scegliere **Approva** o **Nega**.</span><span class="sxs-lookup"><span data-stu-id="351ec-127">Choose either **Approve** or **Deny**.</span></span> <span data-ttu-id="351ec-128">Potrebbe essere necessario includere un motivo per la decisione nella casella di testo **Specifica il motivo** .</span><span class="sxs-lookup"><span data-stu-id="351ec-128">You may need to include a reason for your decision in the **Provide a reason** text box.</span></span>  
5. <span data-ttu-id="351ec-129">Chiudere il pannello **Rivedi ruoli Azure Active Directory** .</span><span class="sxs-lookup"><span data-stu-id="351ec-129">Close the **Review Azure AD roles** blade.</span></span>

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="351ec-130">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="351ec-130">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png
