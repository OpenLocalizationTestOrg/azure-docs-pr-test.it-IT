---
title: Come gestire le impostazioni di attivazione del ruolo | Microsoft Docs
description: "Informazioni su come modificare le impostazioni predefinite per identità con privilegi con l'estensione Azure Active Directory Privileged Identity Management."
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
ms.openlocfilehash: 23605e89cd1846d2e06e48cb5d3e0191cb9e9b4a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-manage-role-activation-settings-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="38056-103">Come gestire le impostazioni di attivazione del ruolo in Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="38056-103">How to manage role activation settings in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="38056-104">Un amministratore dei ruoli con privilegi può personalizzare Azure AD Privileged Identity Management (PIM) nell'organizzazione, ad esempio modificando l'esperienza di un utente che attiva l'assegnazione di idoneo al ruolo.</span><span class="sxs-lookup"><span data-stu-id="38056-104">A privileged role administrator can customize Azure AD Privileged Identity Management (PIM) in their organization, including changing the experience for a user who is activating an eligible role assignment.</span></span>

## <a name="manage-the-role-activation-settings"></a><span data-ttu-id="38056-105">Gestire le impostazioni di attivazione del ruolo</span><span class="sxs-lookup"><span data-stu-id="38056-105">Manage the role activation settings</span></span>
1. <span data-ttu-id="38056-106">Accedere al [portale di Azure](https://portal.azure.com) e selezionare l'app **Azure AD Privileged Identity Management** dal dashboard.</span><span class="sxs-lookup"><span data-stu-id="38056-106">Go to the [Azure portal](https://portal.azure.com) and select the **Azure AD Privileged Identity Management** app from the dashboard.</span></span>
2. <span data-ttu-id="38056-107">Selezionare **Gestione dei ruoli con privilegi** > **Impostazioni** > **Ruoli con privilegi**.</span><span class="sxs-lookup"><span data-stu-id="38056-107">Select **Manage privileged roles** > **Settings** > **Privileged Roles**.</span></span>
3. <span data-ttu-id="38056-108">Selezionare il ruolo del quale gestire le impostazioni.</span><span class="sxs-lookup"><span data-stu-id="38056-108">Choose the role whose settings you want to manage.</span></span>

<span data-ttu-id="38056-109">La pagina Impostazioni per ogni ruolo contiene numerose impostazioni che è possibile configurare.</span><span class="sxs-lookup"><span data-stu-id="38056-109">On the settings page for each role, there are a number of settings you can configure.</span></span> <span data-ttu-id="38056-110">Queste impostazioni incidono solo sugli utenti che sono amministratori idonei, non sugli amministratori permanenti.</span><span class="sxs-lookup"><span data-stu-id="38056-110">These settings only affect users who are eligible admins, not permanent admins.</span></span>

<span data-ttu-id="38056-111">**Attivazioni**: tempo in ore per cui un ruolo rimane attivo prima della scadenza.</span><span class="sxs-lookup"><span data-stu-id="38056-111">**Activations**: The time, in hours, that a role stays active before it expires.</span></span> <span data-ttu-id="38056-112">Questo valore può essere compreso tra 1 e 72 ore.</span><span class="sxs-lookup"><span data-stu-id="38056-112">This can be between 1 and 72 hours.</span></span>

<span data-ttu-id="38056-113">**Notifiche**: è possibile scegliere se il sistema invia messaggi di posta elettronica agli amministratori per confermare che hanno attivato un ruolo.</span><span class="sxs-lookup"><span data-stu-id="38056-113">**Notifications**: You can choose whether or not the system sends emails to admins confirming that they have activated a role.</span></span> <span data-ttu-id="38056-114">Questa opzione può essere utile per il rilevamento di attivazioni non autorizzate o dannose.</span><span class="sxs-lookup"><span data-stu-id="38056-114">This can be useful for detecting unauthorized or illegitimate activations.</span></span>

<span data-ttu-id="38056-115">**Ticket di evento imprevisto/richiesta**: è possibile scegliere se si vuole richiedere che gli amministratori idonei includano un numero di ticket quando attivano il proprio ruolo.</span><span class="sxs-lookup"><span data-stu-id="38056-115">**Incident/Request Ticket**: You can choose whether or not to require eligible admins to include a ticket number when they activate their role.</span></span> <span data-ttu-id="38056-116">Questa opzione può essere utile quando si eseguono i controlli di accesso dei ruoli.</span><span class="sxs-lookup"><span data-stu-id="38056-116">This can be useful when you perform role access audits.</span></span>

<span data-ttu-id="38056-117">**Multi-Factor Authentication**: è possibile scegliere se richiedere agli utenti di verificare la propria identità con MFA prima di attivare i ruoli.</span><span class="sxs-lookup"><span data-stu-id="38056-117">**Multi-Factor Authentication**: You can choose whether or not to require users to verify their identity with MFA before they can activate their roles.</span></span> <span data-ttu-id="38056-118">La verifica è necessaria solo una volta per ogni sessione, non ogni volta che si attiva un ruolo.</span><span class="sxs-lookup"><span data-stu-id="38056-118">They only have to verify this once per session, not every time they activate a role.</span></span> <span data-ttu-id="38056-119">Tenere presente due suggerimenti quando si abilita l'autenticazione MFA:</span><span class="sxs-lookup"><span data-stu-id="38056-119">There are two tips to keep in mind when you enable MFA:</span></span>

* <span data-ttu-id="38056-120">Gli utenti che dispongono di account Microsoft per gli indirizzi di posta elettronica (in genere @outlook.com, ma non sempre) non è possibile registrare per Azure MFA.</span><span class="sxs-lookup"><span data-stu-id="38056-120">Users who have Microsoft accounts for their email addresses (typically @outlook.com, but not always) cannot register for Azure MFA.</span></span> <span data-ttu-id="38056-121">Se si vuole assegnare ruoli agli utenti con account Microsoft, renderli amministratori permanenti o disabilitare l'autenticazione MFA per il ruolo.</span><span class="sxs-lookup"><span data-stu-id="38056-121">If you want to assign roles to users with Microsoft accounts, you should either make them permanent admins or disable MFA for that role.</span></span>
* <span data-ttu-id="38056-122">Non è possibile disabilitare l'autenticazione MFA per i ruoli con privilegi elevati per Azure AD e Office365.</span><span class="sxs-lookup"><span data-stu-id="38056-122">You cannot disable MFA for highly privileged roles for Azure AD and Office365.</span></span> <span data-ttu-id="38056-123">Si tratta di una funzionalità di sicurezza poiché è necessaria una protezione elevata per questi ruoli:</span><span class="sxs-lookup"><span data-stu-id="38056-123">This is a safety feature because these roles should be carefully protected:</span></span>  
  
  * <span data-ttu-id="38056-124">Amministratore di applicazioni</span><span class="sxs-lookup"><span data-stu-id="38056-124">Application administrator</span></span>
  * <span data-ttu-id="38056-125">Amministratore server proxy applicazione</span><span class="sxs-lookup"><span data-stu-id="38056-125">Application Proxy server administrator</span></span>
  * <span data-ttu-id="38056-126">Amministratore fatturazione</span><span class="sxs-lookup"><span data-stu-id="38056-126">Billing administrator</span></span>  
  * <span data-ttu-id="38056-127">Amministratore di conformità</span><span class="sxs-lookup"><span data-stu-id="38056-127">Compliance administrator</span></span>  
  * <span data-ttu-id="38056-128">Amministratore del servizio CRM</span><span class="sxs-lookup"><span data-stu-id="38056-128">CRM service administrator</span></span>
  * <span data-ttu-id="38056-129">Responsabile approvazione per l'accesso a Customer Lockbox</span><span class="sxs-lookup"><span data-stu-id="38056-129">Customer LockBox access approver</span></span>
  * <span data-ttu-id="38056-130">Ruolo con autorizzazioni di scrittura nella directory</span><span class="sxs-lookup"><span data-stu-id="38056-130">Directory writer</span></span>  
  * <span data-ttu-id="38056-131">Amministratore di Exchange</span><span class="sxs-lookup"><span data-stu-id="38056-131">Exchange administrator</span></span>  
  * <span data-ttu-id="38056-132">Amministratore globale</span><span class="sxs-lookup"><span data-stu-id="38056-132">Global administrator</span></span>
  * <span data-ttu-id="38056-133">Amministratore del servizio Intune</span><span class="sxs-lookup"><span data-stu-id="38056-133">Intune service administrator</span></span>
  * <span data-ttu-id="38056-134">Amministratore della cassetta postale</span><span class="sxs-lookup"><span data-stu-id="38056-134">Mailbox administrator</span></span>  
  * <span data-ttu-id="38056-135">Supporto partner - Livello 1</span><span class="sxs-lookup"><span data-stu-id="38056-135">Partner tier1 support</span></span>  
  * <span data-ttu-id="38056-136">Supporto partner - Livello 2</span><span class="sxs-lookup"><span data-stu-id="38056-136">Partner tier2 support</span></span>  
  * <span data-ttu-id="38056-137">Amministratore dei ruoli con privilegi</span><span class="sxs-lookup"><span data-stu-id="38056-137">Privileged role administrator</span></span>   
  * <span data-ttu-id="38056-138">Amministratore della sicurezza</span><span class="sxs-lookup"><span data-stu-id="38056-138">Security administrator</span></span>  
  * <span data-ttu-id="38056-139">Amministratore di SharePoint</span><span class="sxs-lookup"><span data-stu-id="38056-139">SharePoint administrator</span></span>  
  * <span data-ttu-id="38056-140">Amministratore di Skype for Business</span><span class="sxs-lookup"><span data-stu-id="38056-140">Skype for Business administrator</span></span>  
  * <span data-ttu-id="38056-141">Amministratore account utente</span><span class="sxs-lookup"><span data-stu-id="38056-141">User account administrator</span></span>  

<span data-ttu-id="38056-142">Per ulteriori informazioni sull'utilizzo dell’MFA con PIM, vedere [Come richiedere l’MFA](active-directory-privileged-identity-management-how-to-require-mfa.md).</span><span class="sxs-lookup"><span data-stu-id="38056-142">For more information about using MFA with PIM see [How to Require MFA](active-directory-privileged-identity-management-how-to-require-mfa.md).</span></span>

<!--PLACEHOLDER: Need an explanation of what the temporary Global Administrator setting is for.-->

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="38056-143">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="38056-143">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

