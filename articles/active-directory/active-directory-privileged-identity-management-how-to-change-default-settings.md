---
title: impostazioni di attivazione ruolo toomanage aaaHow | Documenti Microsoft
description: "Informazioni su come toochange hello le impostazioni predefinite per le identità con privilegi con hello estensione di Azure Active Directory Privileged Identity Management."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: f6cbcb6a-8a89-4077-afd8-06c94a64f4aa
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 453bb6f8f8e0fd2598cb073ef86c1dd55458dc72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-role-activation-settings-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="71081-103">Come impostazioni di attivazione toomanage ruolo in Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="71081-103">How toomanage role activation settings in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="71081-104">Un amministratore con privilegi di ruolo è possibile personalizzare Azure AD Privileged Identity Management (PIM) nella propria organizzazione, inclusa la modifica esperienza hello per un utente che è l'attivazione di un'assegnazione di ruolo idoneo.</span><span class="sxs-lookup"><span data-stu-id="71081-104">A privileged role administrator can customize Azure AD Privileged Identity Management (PIM) in their organization, including changing hello experience for a user who is activating an eligible role assignment.</span></span>

## <a name="manage-hello-role-activation-settings"></a><span data-ttu-id="71081-105">Gestire le impostazioni di attivazione di hello ruolo</span><span class="sxs-lookup"><span data-stu-id="71081-105">Manage hello role activation settings</span></span>
1. <span data-ttu-id="71081-106">Passare toohello [portale di Azure](https://portal.azure.com) e seleziona hello **Azure AD Privileged Identity Management** app dal dashboard hello.</span><span class="sxs-lookup"><span data-stu-id="71081-106">Go toohello [Azure portal](https://portal.azure.com) and select hello **Azure AD Privileged Identity Management** app from hello dashboard.</span></span>
2. <span data-ttu-id="71081-107">Selezionare **Gestione dei ruoli con privilegi** > **Impostazioni** > **Ruoli con privilegi**.</span><span class="sxs-lookup"><span data-stu-id="71081-107">Select **Manage privileged roles** > **Settings** > **Privileged Roles**.</span></span>
3. <span data-ttu-id="71081-108">Scegliere il ruolo di hello le cui impostazioni si desidera toomanage.</span><span class="sxs-lookup"><span data-stu-id="71081-108">Choose hello role whose settings you want toomanage.</span></span>

<span data-ttu-id="71081-109">Nella pagina Impostazioni di hello per ogni ruolo, esistono una serie di impostazioni che è possibile configurare.</span><span class="sxs-lookup"><span data-stu-id="71081-109">On hello settings page for each role, there are a number of settings you can configure.</span></span> <span data-ttu-id="71081-110">Queste impostazioni incidono solo sugli utenti che sono amministratori idonei, non sugli amministratori permanenti.</span><span class="sxs-lookup"><span data-stu-id="71081-110">These settings only affect users who are eligible admins, not permanent admins.</span></span>

<span data-ttu-id="71081-111">**Le attivazioni**: tempo hello, espresso in ore, per cui un ruolo rimane attivo prima che scada.</span><span class="sxs-lookup"><span data-stu-id="71081-111">**Activations**: hello time, in hours, that a role stays active before it expires.</span></span> <span data-ttu-id="71081-112">Questo valore può essere compreso tra 1 e 72 ore.</span><span class="sxs-lookup"><span data-stu-id="71081-112">This can be between 1 and 72 hours.</span></span>

<span data-ttu-id="71081-113">**Le notifiche**: È possibile scegliere se consentire o meno inviato dal sistema di hello tooadmins messaggi di posta elettronica conferma che è stato attivato un ruolo.</span><span class="sxs-lookup"><span data-stu-id="71081-113">**Notifications**: You can choose whether or not hello system sends emails tooadmins confirming that they have activated a role.</span></span> <span data-ttu-id="71081-114">Questa opzione può essere utile per il rilevamento di attivazioni non autorizzate o dannose.</span><span class="sxs-lookup"><span data-stu-id="71081-114">This can be useful for detecting unauthorized or illegitimate activations.</span></span>

<span data-ttu-id="71081-115">**Evento imprevisto/richiesta Ticket**: È possibile scegliere se toorequire admins idonei tooinclude un ticket numero quando si attiva il proprio ruolo.</span><span class="sxs-lookup"><span data-stu-id="71081-115">**Incident/Request Ticket**: You can choose whether or not toorequire eligible admins tooinclude a ticket number when they activate their role.</span></span> <span data-ttu-id="71081-116">Questa opzione può essere utile quando si eseguono i controlli di accesso dei ruoli.</span><span class="sxs-lookup"><span data-stu-id="71081-116">This can be useful when you perform role access audits.</span></span>

<span data-ttu-id="71081-117">**Multi-Factor Authentication**: È possibile o meno toorequire utenti tooverify la propria identità con autenticazione a più fattori prima di poter attivare i relativi ruoli.</span><span class="sxs-lookup"><span data-stu-id="71081-117">**Multi-Factor Authentication**: You can choose whether or not toorequire users tooverify their identity with MFA before they can activate their roles.</span></span> <span data-ttu-id="71081-118">Hanno solo una volta per ogni sessione, non ogni volta che si attiva un ruolo tooverify.</span><span class="sxs-lookup"><span data-stu-id="71081-118">They only have tooverify this once per session, not every time they activate a role.</span></span> <span data-ttu-id="71081-119">Esistono due suggerimenti tookeep presente quando si abilita l'autenticazione a più fattori:</span><span class="sxs-lookup"><span data-stu-id="71081-119">There are two tips tookeep in mind when you enable MFA:</span></span>

* <span data-ttu-id="71081-120">Gli utenti che dispongono di account Microsoft per gli indirizzi di posta elettronica (in genere @outlook.com, ma non sempre) non è possibile registrare per Azure MFA.</span><span class="sxs-lookup"><span data-stu-id="71081-120">Users who have Microsoft accounts for their email addresses (typically @outlook.com, but not always) cannot register for Azure MFA.</span></span> <span data-ttu-id="71081-121">Se si desidera tooassign ruoli toousers con account Microsoft, si deve renderli amministratori permanenti o disabilitare l'autenticazione a più fattori per tale ruolo.</span><span class="sxs-lookup"><span data-stu-id="71081-121">If you want tooassign roles toousers with Microsoft accounts, you should either make them permanent admins or disable MFA for that role.</span></span>
* <span data-ttu-id="71081-122">Non è possibile disabilitare l'autenticazione MFA per i ruoli con privilegi elevati per Azure AD e Office365.</span><span class="sxs-lookup"><span data-stu-id="71081-122">You cannot disable MFA for highly privileged roles for Azure AD and Office365.</span></span> <span data-ttu-id="71081-123">Si tratta di una funzionalità di sicurezza poiché è necessaria una protezione elevata per questi ruoli:</span><span class="sxs-lookup"><span data-stu-id="71081-123">This is a safety feature because these roles should be carefully protected:</span></span>  
  
  * <span data-ttu-id="71081-124">Amministratore di applicazioni</span><span class="sxs-lookup"><span data-stu-id="71081-124">Application administrator</span></span>
  * <span data-ttu-id="71081-125">Amministratore server proxy applicazione</span><span class="sxs-lookup"><span data-stu-id="71081-125">Application Proxy server administrator</span></span>
  * <span data-ttu-id="71081-126">Amministratore fatturazione</span><span class="sxs-lookup"><span data-stu-id="71081-126">Billing administrator</span></span>  
  * <span data-ttu-id="71081-127">Amministratore di conformità</span><span class="sxs-lookup"><span data-stu-id="71081-127">Compliance administrator</span></span>  
  * <span data-ttu-id="71081-128">Amministratore del servizio CRM</span><span class="sxs-lookup"><span data-stu-id="71081-128">CRM service administrator</span></span>
  * <span data-ttu-id="71081-129">Responsabile approvazione per l'accesso a Customer Lockbox</span><span class="sxs-lookup"><span data-stu-id="71081-129">Customer LockBox access approver</span></span>
  * <span data-ttu-id="71081-130">Ruolo con autorizzazioni di scrittura nella directory</span><span class="sxs-lookup"><span data-stu-id="71081-130">Directory writer</span></span>  
  * <span data-ttu-id="71081-131">Amministratore di Exchange</span><span class="sxs-lookup"><span data-stu-id="71081-131">Exchange administrator</span></span>  
  * <span data-ttu-id="71081-132">Amministratore globale</span><span class="sxs-lookup"><span data-stu-id="71081-132">Global administrator</span></span>
  * <span data-ttu-id="71081-133">Amministratore del servizio Intune</span><span class="sxs-lookup"><span data-stu-id="71081-133">Intune service administrator</span></span>
  * <span data-ttu-id="71081-134">Amministratore della cassetta postale</span><span class="sxs-lookup"><span data-stu-id="71081-134">Mailbox administrator</span></span>  
  * <span data-ttu-id="71081-135">Supporto partner - Livello 1</span><span class="sxs-lookup"><span data-stu-id="71081-135">Partner tier1 support</span></span>  
  * <span data-ttu-id="71081-136">Supporto partner - Livello 2</span><span class="sxs-lookup"><span data-stu-id="71081-136">Partner tier2 support</span></span>  
  * <span data-ttu-id="71081-137">Amministratore dei ruoli con privilegi</span><span class="sxs-lookup"><span data-stu-id="71081-137">Privileged role administrator</span></span>   
  * <span data-ttu-id="71081-138">Amministratore della sicurezza</span><span class="sxs-lookup"><span data-stu-id="71081-138">Security administrator</span></span>  
  * <span data-ttu-id="71081-139">Amministratore di SharePoint</span><span class="sxs-lookup"><span data-stu-id="71081-139">SharePoint administrator</span></span>  
  * <span data-ttu-id="71081-140">Amministratore di Skype for Business</span><span class="sxs-lookup"><span data-stu-id="71081-140">Skype for Business administrator</span></span>  
  * <span data-ttu-id="71081-141">Amministratore account utente</span><span class="sxs-lookup"><span data-stu-id="71081-141">User account administrator</span></span>  

<span data-ttu-id="71081-142">Per ulteriori informazioni sull'utilizzo di autenticazione a più fattori con PIM vedere [come autenticazione a più fattori tooRequire](active-directory-privileged-identity-management-how-to-require-mfa.md).</span><span class="sxs-lookup"><span data-stu-id="71081-142">For more information about using MFA with PIM see [How tooRequire MFA](active-directory-privileged-identity-management-how-to-require-mfa.md).</span></span>

<!--PLACEHOLDER: Need an explanation of what hello temporary Global Administrator setting is for.-->

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="71081-143">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="71081-143">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

