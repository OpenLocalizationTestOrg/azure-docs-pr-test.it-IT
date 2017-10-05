---
title: Iscriversi a Office 365 con un account Azure | Microsoft Docs
description: Informazioni su come creare un abbonamento a Office 365 con un account Azure
services: 
documentationcenter: 
author: JiangChen79
manager: adpick
editor: 
tags: billing,top-support-issue
ms.assetid: 
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: cjiang
ms.openlocfilehash: 1c6e277e321980aaf30f821dbb41c7eaf296b4cf
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="sign-up-for-an-office-365-subscription-with-your-azure-account"></a><span data-ttu-id="f2b92-103">Iscriversi a un abbonamento a Office 365 con il proprio account Azure</span><span class="sxs-lookup"><span data-stu-id="f2b92-103">Sign up for an Office 365 subscription with your Azure account</span></span>
<span data-ttu-id="f2b92-104">Se si è un sottoscrittore di Azure, è possibile usare l'account Azure per iscriversi a un abbonamento a Office 365.</span><span class="sxs-lookup"><span data-stu-id="f2b92-104">If you're Azure subscriber, you can use your Azure account to sign up for an Office 365 subscription.</span></span> <span data-ttu-id="f2b92-105">Se si fa parte di un'organizzazione che dispone di una sottoscrizione di Azure, è possibile creare abbonamenti a Office 365 per gli utenti nell'istanza esistente di Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f2b92-105">If you're part of an organization that has an Azure subscription, you can create Office 365 subscriptions for users in your existing Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="f2b92-106">Iscriversi a Office 365 tramite un account che dispone dell'autorizzazione Amministratore globale o Amministratore fatturazione nel tenant di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f2b92-106">Sign up to Office 365 using an account that has Global Admin or Billing Admin permissions in your Azure Active Directory tenant.</span></span> <span data-ttu-id="f2b92-107">Per altre informazioni, vedere [Controllare le autorizzazioni dell'account in Azure AD](#RoleInAzureAD) e [Assegnazione dei ruoli di amministratore in Azure Active Directory](../active-directory/active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="f2b92-107">For more information, see [Check my account permissions in Azure AD](#RoleInAzureAD) and [Assigning administrator roles in Azure Active Directory](../active-directory/active-directory-assign-admin-roles.md).</span></span>

<span data-ttu-id="f2b92-108">Se si dispone già sia di un account di Office 365 sia di una sottoscrizione di Azure, vedere [Associare un tenant di Office 365 a una sottoscrizione di Azure](billing-add-office-365-tenant-to-azure-subscription.md).</span><span class="sxs-lookup"><span data-stu-id="f2b92-108">If you already have both an Office 365 account and an Azure subscription, you can [Associate an Office 365 tenant to an Azure subscription](billing-add-office-365-tenant-to-azure-subscription.md).</span></span>

## <a name="get-an-office-365-subscription-by-using-your-azure-account"></a><span data-ttu-id="f2b92-109">Ottenere un abbonamento a Office 365 tramite il proprio account Azure</span><span class="sxs-lookup"><span data-stu-id="f2b92-109">Get an Office 365 subscription by using your Azure account</span></span>

1. <span data-ttu-id="f2b92-110">Andare alla [pagina del prodotto Office 365](https://products.office.com/business) e selezionare un piano.</span><span class="sxs-lookup"><span data-stu-id="f2b92-110">Go to the [Office 365 product page](https://products.office.com/business), and select a plan.</span></span>
2. <span data-ttu-id="f2b92-111">Fare clic su **Accedi** nell'angolo superiore destro della pagina.</span><span class="sxs-lookup"><span data-stu-id="f2b92-111">Click **Sign in** on the upper-right corner of the page.</span></span>

    ![screenshot della pagina della versione di valutazione di Office 365](./media/billing-use-existing-azure-account-office-365-subscription/12-office-365-trial-page.png)
3. <span data-ttu-id="f2b92-113">Accedere con le credenziali dell'account Azure.</span><span class="sxs-lookup"><span data-stu-id="f2b92-113">Sign in with your Azure account credentials.</span></span> <span data-ttu-id="f2b92-114">Se si crea un abbonamento per la propria organizzazione, usare l'account Azure membro del ruolo della directory Amministratore globale o Amministratore fatturazione nel tenant di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f2b92-114">If you're creating a subscription for your organization, use an Azure account that's a member of the Global Admin or Billing Admin directory role in your Azure Active Directory tenant.</span></span>

    ![Screenshot della pagina di accesso a Office 365](./media/billing-use-existing-azure-account-office-365-subscription/13-office-365-sign-in.png)
4. <span data-ttu-id="f2b92-116">Fare clic su **Prova adesso**.</span><span class="sxs-lookup"><span data-stu-id="f2b92-116">Click **Try now**.</span></span>

    ![Screenshot di conferma dell'ordine per Office 365.](./media/billing-use-existing-azure-account-office-365-subscription/14-office-365-confirm-your-order.png)
5. <span data-ttu-id="f2b92-118">Nella pagina di conferma dell'ordine fare clic su **Continua**.</span><span class="sxs-lookup"><span data-stu-id="f2b92-118">On the order receipt page, click **Continue**.</span></span>

    ![Screenshot di ricezione dell'ordine di Office 365](./media/billing-use-existing-azure-account-office-365-subscription/15-office-365-order-receipt.png)

<span data-ttu-id="f2b92-120">Le impostazioni sono state completate.</span><span class="sxs-lookup"><span data-stu-id="f2b92-120">Now you're all set.</span></span> <span data-ttu-id="f2b92-121">Se l'abbonamento a Office 365 è stato creato per la propria organizzazione, seguire questa procedura per controllare che gli utenti di Azure AD siano ora disponibili in Office 365.</span><span class="sxs-lookup"><span data-stu-id="f2b92-121">If you created the Office 365 subscription for your organization, use the following steps to check that your Azure AD users are now in Office 365.</span></span>

1. <span data-ttu-id="f2b92-122">Aprire l'interfaccia di amministrazione di Office 365.</span><span class="sxs-lookup"><span data-stu-id="f2b92-122">Open the Office 365 admin center.</span></span>
2. <span data-ttu-id="f2b92-123">Espandere **UTENTI** e quindi fare clic su **Utenti attivi**.</span><span class="sxs-lookup"><span data-stu-id="f2b92-123">Expand **USERS**, and then click **Active Users**.</span></span>

    ![Screenshot degli utenti nell'interfaccia di amministrazione di Office 365](./media/billing-use-existing-azure-account-office-365-subscription/16-office-365-admin-center-users.png)

<span data-ttu-id="f2b92-125">Dopo avere eseguito l'iscrizione, l'abbonamento a Office 365 viene aggiunto alla stessa istanza di Azure Active Directory a cui appartiene la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="f2b92-125">After you sign up, the Office 365 subscription is added to the same Azure Active Directory instance that your Azure subscription belongs to.</span></span> <span data-ttu-id="f2b92-126">Per altre informazioni, vedere [Altre informazioni su sottoscrizioni di Azure e abbonamenti a Office 365](billing-use-existing-office-365-account-azure-subscription.md#more-about-subs) e [Associare le sottoscrizioni di Azure ad Azure Active Directory](../active-directory/active-directory-how-subscriptions-associated-directory.md).</span><span class="sxs-lookup"><span data-stu-id="f2b92-126">For more information, see [More about Azure and Office 365 subscriptions](billing-use-existing-office-365-account-azure-subscription.md#more-about-subs) and [How Azure subscriptions are associated with Azure Active Directory](../active-directory/active-directory-how-subscriptions-associated-directory.md).</span></span>

## <span data-ttu-id="f2b92-127"><a id="RoleInAzureAD"></a>Controllare le autorizzazioni dell'account Microsoft in Azure AD</span><span class="sxs-lookup"><span data-stu-id="f2b92-127"><a id="RoleInAzureAD"></a>Check my account permissions in Azure AD</span></span>
1. <span data-ttu-id="f2b92-128">Accedere al [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="f2b92-128">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="f2b92-129">Fare clic su **Altri servizi** e quindi cercare **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f2b92-129">Click **More services**, and then search for **Active Directory**.</span></span>

    ![Screenshot di Active Directory nel portale di Azure](./media/billing-use-existing-azure-account-office-365-subscription/billing-more-services-active-directory.png)
3. <span data-ttu-id="f2b92-131">Fare clic su **Utenti e gruppi** > **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="f2b92-131">Click **Users and groups** > **All users**.</span></span>
4. <span data-ttu-id="f2b92-132">Selezionare il nome utente.</span><span class="sxs-lookup"><span data-stu-id="f2b92-132">Select the user name.</span></span> 

    ![Screenshot che mostra gli utenti di Azure Active Directory](./media/billing-use-existing-azure-account-office-365-subscription/billing-users-groups.png)

5. <span data-ttu-id="f2b92-134">Fare clic su **Ruolo directory**.</span><span class="sxs-lookup"><span data-stu-id="f2b92-134">Click **Directory role**.</span></span>
  
    ![Screenshot che mostra il ruolo di directory del portale di Azure](./media/billing-use-existing-azure-account-office-365-subscription/billing-user-directory-role.png)
6.  <span data-ttu-id="f2b92-136">È necessario il ruolo **Amministratore globale** o **Amministratore con limitazioni** > **Amministratore fatturazione** per creare un abbonamento a Office 365 per gli utenti nell'istanza di Azure Active Directory esistente.</span><span class="sxs-lookup"><span data-stu-id="f2b92-136">The role **Global administrator** or **Limited administrator** > **Billing administrator** is required to create an Office 365 subscription for users in your existing Azure Active Directory.</span></span>

    ![Screenshot che mostra il ruolo di directory del portale di Azure Amministratore fatturazione](./media/billing-use-existing-azure-account-office-365-subscription/billing-directoryrole-limited.png)

## <a name="need-help-contact-support"></a><span data-ttu-id="f2b92-138">Richiesta di assistenza</span><span class="sxs-lookup"><span data-stu-id="f2b92-138">Need help?</span></span> <span data-ttu-id="f2b92-139">Contattare il supporto tecnico.</span><span class="sxs-lookup"><span data-stu-id="f2b92-139">Contact support.</span></span>
<span data-ttu-id="f2b92-140">Se si necessita ancora di assistenza, [contattare il supporto tecnico](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) per ottenere una rapida risoluzione del problema.</span><span class="sxs-lookup"><span data-stu-id="f2b92-140">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your issue resolved quickly.</span></span> 
