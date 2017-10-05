---
title: Aggiungere nuovi utenti ad Azure Active Directory | Documentazione Microsoft
description: Illustra come aggiungere nuovi utenti o modificare le informazioni sugli utenti in Azure Active Directory.
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: e3673727-6bec-4fdc-87a4-d65b213c4c3c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: curtand
ms.reviewer: jeffsta
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: ff4b742e772a6062885313e9bb49e55907fe125a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="add-new-users-or-users-with-microsoft-accounts-to-azure-active-directory"></a><span data-ttu-id="08f79-103">Aggiungere nuovi utenti o utenti con account Microsoft in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="08f79-103">Add new users or users with Microsoft accounts to Azure Active Directory</span></span>
<span data-ttu-id="08f79-104">Aggiungere utenti per popolare la directory.</span><span class="sxs-lookup"><span data-stu-id="08f79-104">Add users to populate your directory.</span></span> <span data-ttu-id="08f79-105">Questo articolo illustra come aggiungere nuovi utenti dell'organizzazione e come aggiungere utenti con account Microsoft.</span><span class="sxs-lookup"><span data-stu-id="08f79-105">This article explains how to add new users in your organization, and how to add users who have Microsoft accounts.</span></span> <span data-ttu-id="08f79-106">Per altre informazioni sull'aggiunta di utenti da altre directory in Azure Active Directory o l'aggiunta di utenti da società partner, vedere [Aggiungere utenti da altre directory o società partner in Azure Active Directory](active-directory-create-users-external.md).</span><span class="sxs-lookup"><span data-stu-id="08f79-106">For more information about adding users from other directories in Azure Active Directory or adding users from partner companies, see [Add users from other directories or partner companies in Azure Active Directory](active-directory-create-users-external.md).</span></span> <span data-ttu-id="08f79-107">Gli utenti aggiunti non hanno autorizzazioni di amministratore per impostazione predefinita, ma è possibile assegnare loro dei ruoli in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="08f79-107">Added users don't have administrator permissions by default, but you can assign roles to them at any time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="08f79-108">Microsoft consiglia di gestire Azure AD usando l'[interfaccia di amministrazione di Azure AD](https://aad.portal.azure.com) nel portale di Azure invece di usare il portale di Azure classico citato nel presente articolo.</span><span class="sxs-lookup"><span data-stu-id="08f79-108">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span> <span data-ttu-id="08f79-109">Per informazioni su come aggiungere un utente nell'interfaccia di amministrazione di Azure AD, vedere [Aggiungere nuovi utenti in Azure Active Directory](active-directory-users-create-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="08f79-109">For how to add a user in the Azure AD admin center, see [Add new users to Azure Active Directory](active-directory-users-create-azure-portal.md).</span></span>

## <a name="add-a-user"></a><span data-ttu-id="08f79-110">Aggiungere un utente</span><span class="sxs-lookup"><span data-stu-id="08f79-110">Add a user</span></span>
1. <span data-ttu-id="08f79-111">Accedere al [portale di Azure classico](https://manage.windowsazure.com) con un account di amministratore globale per la directory.</span><span class="sxs-lookup"><span data-stu-id="08f79-111">Sign in to the [Azure classic portal](https://manage.windowsazure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="08f79-112">Selezionare **Active Directory**e quindi il nome della directory dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="08f79-112">Select **Active Directory**, and then select the name of your organization directory.</span></span>
3. <span data-ttu-id="08f79-113">Selezionare la scheda **Utenti** e quindi **Aggiungi utente** nella barra dei comandi.</span><span class="sxs-lookup"><span data-stu-id="08f79-113">Select the **Users** tab, and then, in the command bar, select **Add User**.</span></span>
4. <span data-ttu-id="08f79-114">Nella pagina **Informazioni sull'utente** selezionare in **Tipo di utente** una delle opzioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="08f79-114">On the **Tell us about this user** page, under **Type of user**, select either:</span></span>

   * <span data-ttu-id="08f79-115">**Nuovo utente nell'organizzazione** : consente di aggiungere un nuovo account utente nella directory.</span><span class="sxs-lookup"><span data-stu-id="08f79-115">**New user in your organization** – adds a new user account in your directory.</span></span>
   * <span data-ttu-id="08f79-116">**Utente con account Microsoft esistente** : consente di aggiungere un account utente Microsoft esistente alla directory, ad esempio un account Outlook.</span><span class="sxs-lookup"><span data-stu-id="08f79-116">**User with an existing Microsoft account** – adds an existing Microsoft consumer account to your directory (for example, an Outlook account)</span></span>
5. <span data-ttu-id="08f79-117">In base al **Tipo di utente**immettere un nome utente, per un nuovo utente, o un indirizzo di posta elettronica, per un utente con un account Microsoft.</span><span class="sxs-lookup"><span data-stu-id="08f79-117">Depending on **Type of user**, enter a user name (for new user) or an email address (for a user with a Microsoft account).</span></span>
6. <span data-ttu-id="08f79-118">Nella pagina **Profilo** dell'utente specificare nome e cognome, un nome descrittivo e un ruolo utente nell'elenco **Ruoli**.</span><span class="sxs-lookup"><span data-stu-id="08f79-118">On the user **Profile** page, provide a first and last name, a user-friendly name, and a user role from the **Roles** list.</span></span> <span data-ttu-id="08f79-119">Per altre informazioni sui ruoli utente e di amministratore, vedere [Assegnazione dei ruoli di amministratore in Azure Active Directory](active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="08f79-119">For more information about user and administrator roles, see [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md).</span></span> <span data-ttu-id="08f79-120">Specificare eventualmente **Abilita Multi-Factor Authentication** per l'utente.</span><span class="sxs-lookup"><span data-stu-id="08f79-120">Specify whether to **Enable Multi-Factor Authentication** for the user.</span></span>
7. <span data-ttu-id="08f79-121">Nella pagina **Ottieni password temporanea** selezionare **Crea**.</span><span class="sxs-lookup"><span data-stu-id="08f79-121">On the **Get temporary password** page, select **Create**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="08f79-122">Se l'organizzazione usa più di un dominio, è opportuno essere a conoscenza dei problemi seguenti quando si aggiunge un account utente:</span><span class="sxs-lookup"><span data-stu-id="08f79-122">If your organization uses more than one domain, you should know about the following issues when you add a user account:</span></span>
>
> * <span data-ttu-id="08f79-123">Per aggiungere account utente con lo stesso nome dell'entità utente (UPN) in tutti i domini, aggiungere **prima** geoffgrisso@contoso.onmicrosoft.com, ad esempio, **seguito da** geoffgrisso@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="08f79-123">TO add user accounts with the same user principal name (UPN) across domains, **first** add, for example, geoffgrisso@contoso.onmicrosoft.com, **followed by** geoffgrisso@contoso.com.</span></span>
> * <span data-ttu-id="08f79-124">**Non** aggiungere geoffgrisso@contoso.com prima di aggiungere geoffgrisso@contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="08f79-124">**Don't** add geoffgrisso@contoso.com before you add geoffgrisso@contoso.onmicrosoft.com.</span></span> <span data-ttu-id="08f79-125">Quest'ordine è importante e può essere complesso da annullare.</span><span class="sxs-lookup"><span data-stu-id="08f79-125">This order is important, and can be cumbersome to undo.</span></span>
>
>

## <a name="change-user-information"></a><span data-ttu-id="08f79-126">Modificare le informazioni utente</span><span class="sxs-lookup"><span data-stu-id="08f79-126">Change user information</span></span>
<span data-ttu-id="08f79-127">È possibile modificare tutti gli attributi utente tranne l'ID oggetto.</span><span class="sxs-lookup"><span data-stu-id="08f79-127">You can change any user attribute except for the object ID.</span></span>

1. <span data-ttu-id="08f79-128">Aprire la directory.</span><span class="sxs-lookup"><span data-stu-id="08f79-128">Open your directory.</span></span>
2. <span data-ttu-id="08f79-129">Selezionare la scheda **Utenti** e quindi il nome visualizzato dell'utente che si vuole modificare.</span><span class="sxs-lookup"><span data-stu-id="08f79-129">Select the **Users** tab, and then select the display name of the user you want to change.</span></span>
3. <span data-ttu-id="08f79-130">Salvare le modifiche e quindi fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="08f79-130">Complete your changes, and then click **Save**.</span></span>

<span data-ttu-id="08f79-131">Se l'utente che si sta modificando è sincronizzato con il servizio Active Directory locale, non è possibile modificare le informazioni utente con questa procedura.</span><span class="sxs-lookup"><span data-stu-id="08f79-131">If the user that you're changing is synchronized with your on-premises Active Directory service, you can't change the user information using this procedure.</span></span> <span data-ttu-id="08f79-132">Per modificare l'utente, usare gli strumenti di gestione del servizio Active Directory locale.</span><span class="sxs-lookup"><span data-stu-id="08f79-132">To change the user, use your on-premises Active Directory management tools.</span></span>

## <a name="guest-user-management-and-limitations"></a><span data-ttu-id="08f79-133">Gestione e limiti dell'utente guest</span><span class="sxs-lookup"><span data-stu-id="08f79-133">Guest user management and limitations</span></span>
<span data-ttu-id="08f79-134">Gli account guest rappresentano utenti di altre directory che sono stati invitati alla directory per accedere a documenti di SharePoint, applicazioni o altre risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="08f79-134">Guest accounts are users from other directories who were invited to your directory to access SharePoint documents, applications, or other Azure resources.</span></span> <span data-ttu-id="08f79-135">Un account guest nella directory ha l'attributo UserType sottostante impostato su "Guest".</span><span class="sxs-lookup"><span data-stu-id="08f79-135">A guest account in your directory has its underlying UserType attribute set to "Guest."</span></span> <span data-ttu-id="08f79-136">Per gli utenti normali, ovvero i membri della directory, l'attributo UserType è impostato su "Membro".</span><span class="sxs-lookup"><span data-stu-id="08f79-136">Regular users (specifically, members of your directory) have the UserType attribute "Member."</span></span>

<span data-ttu-id="08f79-137">Nella directory gli utenti guest hanno un set di diritti limitato.</span><span class="sxs-lookup"><span data-stu-id="08f79-137">Guests have a limited set of rights in the directory.</span></span> <span data-ttu-id="08f79-138">Questi diritti limitano la possibilità per gli utenti guest di trovare informazioni sugli altri utenti nella directory.</span><span class="sxs-lookup"><span data-stu-id="08f79-138">These rights limit the ability for Guests to discover information about other users in the directory.</span></span> <span data-ttu-id="08f79-139">Gli utenti guest possono comunque interagire con gli utenti e i gruppi associati alle risorse su cui stanno lavorando.</span><span class="sxs-lookup"><span data-stu-id="08f79-139">However, guest users can still interact with the users and groups associated with the resources they're working on.</span></span> <span data-ttu-id="08f79-140">Gli utenti guest possono:</span><span class="sxs-lookup"><span data-stu-id="08f79-140">Guest users can:</span></span>

* <span data-ttu-id="08f79-141">Visualizzare altri utenti e gruppi associati a una sottoscrizione di Azure a cui sono assegnati</span><span class="sxs-lookup"><span data-stu-id="08f79-141">See other users and groups associated with an Azure subscription to which they're assigned</span></span>
* <span data-ttu-id="08f79-142">Visualizzare i membri dei gruppi a cui appartengono</span><span class="sxs-lookup"><span data-stu-id="08f79-142">See the members of groups to which they belong</span></span>
* <span data-ttu-id="08f79-143">Cercare altri utenti nella directory, se conoscono l'indirizzo di posta elettronica completo dell'utente</span><span class="sxs-lookup"><span data-stu-id="08f79-143">Look up other users in the directory, if they know the full email address of the user</span></span>
* <span data-ttu-id="08f79-144">Visualizzare solo un set limitato di attributi degli utenti cercati, ad esempio solo il nome visualizzato, l'indirizzo di posta elettronica, il nome dell'entità utente e la foto di anteprima</span><span class="sxs-lookup"><span data-stu-id="08f79-144">See only a limited set of attributes of the users they look up--limited to display name, email address, user principal name (UPN), and thumbnail photo</span></span>
* <span data-ttu-id="08f79-145">Ottenere un elenco di domini verificati nella directory</span><span class="sxs-lookup"><span data-stu-id="08f79-145">Get a list of verified domains in the directory</span></span>
* <span data-ttu-id="08f79-146">Autorizzare applicazioni, concedendo loro lo stesso accesso disponibile per i membri nella propria directory</span><span class="sxs-lookup"><span data-stu-id="08f79-146">Consent to applications, granting them the same access that Members have in your directory</span></span>

## <a name="set-guest-user-access-policies"></a><span data-ttu-id="08f79-147">Impostare i criteri di accesso degli utenti guest</span><span class="sxs-lookup"><span data-stu-id="08f79-147">Set guest user access policies</span></span>
<span data-ttu-id="08f79-148">La scheda **Configura** di una directory include le opzioni per il controllo dell'accesso per gli utenti guest.</span><span class="sxs-lookup"><span data-stu-id="08f79-148">The **Configure** tab of a directory includes options to control access for guest users.</span></span> <span data-ttu-id="08f79-149">Tali opzioni possono essere modificate unicamente da un amministratore globale di directory nel portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="08f79-149">These options can be changed only in Azure classic portal by a directory global administrator.</span></span> <span data-ttu-id="08f79-150">Al momento non è disponibile alcun metodo di PowerShell o API.</span><span class="sxs-lookup"><span data-stu-id="08f79-150">Currently, there's no PowerShell or API method.</span></span>

<span data-ttu-id="08f79-151">Per aprire la scheda **Configura** nel portale di Azure classico, selezionare **Active Directory** e quindi il nome della directory.</span><span class="sxs-lookup"><span data-stu-id="08f79-151">To open the **Configure** tab in the Azure classic portal, select **Active Directory**, and then select the name of the directory.</span></span>

![Scheda Configura in Azure Active Directory][1]

<span data-ttu-id="08f79-153">Si potranno quindi modificare le opzioni per controllare l'accesso per gli utenti guest.</span><span class="sxs-lookup"><span data-stu-id="08f79-153">Then you can edit the options to control access for guest users.</span></span>

![opzioni di controllo di accesso per gli utenti guest][2]

## <a name="whats-next"></a><span data-ttu-id="08f79-155">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="08f79-155">What's next</span></span>
* [<span data-ttu-id="08f79-156">Aggiungere utenti da altre directory o società partner in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="08f79-156">Add users from other directories or partner companies in Azure Active Directory</span></span>](active-directory-create-users-external.md)
* [<span data-ttu-id="08f79-157">Amministrazione di Azure AD</span><span class="sxs-lookup"><span data-stu-id="08f79-157">Administering Azure AD</span></span>](active-directory-administer.md)
* [<span data-ttu-id="08f79-158">Gestire password in Azure AD</span><span class="sxs-lookup"><span data-stu-id="08f79-158">Manage passwords in Azure AD</span></span>](active-directory-manage-passwords.md)
* [<span data-ttu-id="08f79-159">Gestire gruppi in Azure AD</span><span class="sxs-lookup"><span data-stu-id="08f79-159">Manage groups in Azure AD</span></span>](active-directory-manage-groups.md)

<!--Image references-->
[1]: ./media/active-directory-create-users/RBACDirConfigTab.png
[2]: ./media/active-directory-create-users/RBACGuestAccessControls.png
