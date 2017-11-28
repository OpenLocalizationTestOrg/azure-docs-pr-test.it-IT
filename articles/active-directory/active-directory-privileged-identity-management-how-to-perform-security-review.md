---
title: aaaHow tooperform una revisione accesso | Documenti Microsoft
description: Informazioni su come tooperform una revisione con hello applicazione Azure Privileged Identity Management.
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
ms.openlocfilehash: 301a5e9f97b68fedfbf4954e0bd7dadb7f0fc510
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooperform-an-access-review-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="4d654-103">Come tooperform esaminare un accesso in Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="4d654-103">How tooperform an access review in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="4d654-104">Gestione di identità con privilegi di Azure Active Directory (AD) semplifica la modalità di gestione di aziende tooresources di accesso con privilegi in Azure AD e altri Microsoft online services quali Office 365 o Microsoft Intune.</span><span class="sxs-lookup"><span data-stu-id="4d654-104">Azure Active Directory (AD) Privileged Identity Management simplifies how enterprises manage privileged access tooresources in Azure AD and other Microsoft online services like Office 365 or Microsoft Intune.</span></span>  

<span data-ttu-id="4d654-105">Se si sono assegnati ruoli amministrativi tooan, l'amministratore del ruolo con privilegi potrebbe essere richiesto tooregularly confermare che è necessario tale ruolo per il processo.</span><span class="sxs-lookup"><span data-stu-id="4d654-105">If you are assigned tooan administrative role, your organization's privileged role administrator may ask you tooregularly confirm that you still need that role for your job.</span></span> <span data-ttu-id="4d654-106">È possibile che venga visualizzato un messaggio di posta elettronica che include un collegamento oppure è possibile passare retta toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4d654-106">You might get an email that includes a link, or you can go straight toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="4d654-107">Seguire i passaggi di hello in questo articolo di tooperform esaminare automatica dei ruoli assegnati.</span><span class="sxs-lookup"><span data-stu-id="4d654-107">Follow hello steps in this article tooperform a self-review of your assigned roles.</span></span>

<span data-ttu-id="4d654-108">Se si è un ruolo con privilegi di amministratore interessato revisioni di accesso, ottenere ulteriori dettagli in [come toostart un accesso esaminare](active-directory-privileged-identity-management-how-to-start-security-review.md).</span><span class="sxs-lookup"><span data-stu-id="4d654-108">If you're a privileged role administrator interested in access reviews, get more details at [How toostart an access review](active-directory-privileged-identity-management-how-to-start-security-review.md).</span></span>

## <a name="add-hello-privileged-identity-management-application"></a><span data-ttu-id="4d654-109">Aggiungere un'applicazione hello Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="4d654-109">Add hello Privileged Identity Management application</span></span>
<span data-ttu-id="4d654-110">È possibile utilizzare un'applicazione hello Azure AD Privileged Identity Management (PIM) in hello [portale di Azure](https://portal.azure.com/) tooperform la revisione.</span><span class="sxs-lookup"><span data-stu-id="4d654-110">You can use hello Azure AD Privileged Identity Management (PIM) application in hello [Azure portal](https://portal.azure.com/) tooperform your review.</span></span>  <span data-ttu-id="4d654-111">Se non si dispone di un'applicazione hello Azure AD Privileged Identity Management nel portale, seguire questi passaggi tooget avviato.</span><span class="sxs-lookup"><span data-stu-id="4d654-111">If you don't have hello Azure AD Privileged Identity Management application on your portal, follow these steps tooget started.</span></span>

1. <span data-ttu-id="4d654-112">Accedi toohello [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="4d654-112">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="4d654-113">Selezionare il nome utente in hello nell'angolo superiore destro di hello portale di Azure e selezionare hello directory in cui sarà necessario essere operativo.</span><span class="sxs-lookup"><span data-stu-id="4d654-113">Select your username in hello upper right-hand corner of hello Azure portal, and select hello directory where you will you be operating.</span></span>
3. <span data-ttu-id="4d654-114">Selezionare **più servizi** e utilizzare hello filtro textbox toosearch per **Azure AD Privileged Identity Management**.</span><span class="sxs-lookup"><span data-stu-id="4d654-114">Select **More services** and use hello Filter textbox toosearch for **Azure AD Privileged Identity Management**.</span></span>
4. <span data-ttu-id="4d654-115">Controllare **Pin toodashboard** e quindi fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="4d654-115">Check **Pin toodashboard** and then click **Create**.</span></span> <span data-ttu-id="4d654-116">verrà aperto Hello applicazione Privileged Identity Management.</span><span class="sxs-lookup"><span data-stu-id="4d654-116">hello Privileged Identity Management application will open.</span></span>

## <a name="approve-or-deny-access"></a><span data-ttu-id="4d654-117">Approvare o negare l'accesso</span><span class="sxs-lookup"><span data-stu-id="4d654-117">Approve or deny access</span></span>
<span data-ttu-id="4d654-118">Quando si approvare o negare l'accesso, si sta indica semplicemente revisore hello se questo ruolo è comunque usare o non.</span><span class="sxs-lookup"><span data-stu-id="4d654-118">When you approve or deny access, you're just telling hello reviewer whether you still use this role or not.</span></span> <span data-ttu-id="4d654-119">Scegliere **Approva** se si desidera toostay nel ruolo hello o **Deny** se l'accesso non necessario hello più.</span><span class="sxs-lookup"><span data-stu-id="4d654-119">Choose **Approve** if you want toostay in hello role, or **Deny** if you don't need hello access anymore.</span></span> <span data-ttu-id="4d654-120">Lo stato non cambia immediatamente, fino a quando il revisore hello applica risultati hello.</span><span class="sxs-lookup"><span data-stu-id="4d654-120">Your status won't change right away, until hello reviewer applies hello results.</span></span>
<span data-ttu-id="4d654-121">Seguire questi passaggi toofind e completare hello accesso revisione:</span><span class="sxs-lookup"><span data-stu-id="4d654-121">Follow these steps toofind and complete hello access review:</span></span>

1. <span data-ttu-id="4d654-122">Nell'applicazione PIM hello, selezionare **accesso con privilegi di revisione**.</span><span class="sxs-lookup"><span data-stu-id="4d654-122">In hello PIM application, select **Review privileged access**.</span></span> <span data-ttu-id="4d654-123">Nel caso di eventuali revisioni in sospeso di accesso, vengono visualizzate in hello che Azure AD Access revisioni del pannello.</span><span class="sxs-lookup"><span data-stu-id="4d654-123">If you have any pending access reviews, they appear in hello Azure AD Access reviews blade.</span></span>
2. <span data-ttu-id="4d654-124">Selezionare una revisione hello desiderato toocomplete.</span><span class="sxs-lookup"><span data-stu-id="4d654-124">Select hello review you want toocomplete.</span></span>
3. <span data-ttu-id="4d654-125">A meno che non è stata creata la revisione di hello, è visualizzato come hello solo utente in revisione hello.</span><span class="sxs-lookup"><span data-stu-id="4d654-125">Unless you created hello review, you appear as hello only user in hello review.</span></span> <span data-ttu-id="4d654-126">Selezionare il nome tooyour successivo di hello segno di spunta.</span><span class="sxs-lookup"><span data-stu-id="4d654-126">Select hello check mark next tooyour name.</span></span>
4. <span data-ttu-id="4d654-127">Scegliere **Approva** o **Nega**.</span><span class="sxs-lookup"><span data-stu-id="4d654-127">Choose either **Approve** or **Deny**.</span></span> <span data-ttu-id="4d654-128">Potrebbe essere necessario un motivo per la decisione in hello tooinclude **fornire un motivo** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="4d654-128">You may need tooinclude a reason for your decision in hello **Provide a reason** text box.</span></span>  
5. <span data-ttu-id="4d654-129">Chiude hello **ruoli di Azure AD verifica** blade.</span><span class="sxs-lookup"><span data-stu-id="4d654-129">Close hello **Review Azure AD roles** blade.</span></span>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="4d654-130">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4d654-130">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png
