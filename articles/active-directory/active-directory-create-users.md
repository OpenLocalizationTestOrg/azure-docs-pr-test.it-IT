---
title: aaaAdd nuovi utenti tooAzure Active Directory | Documenti Microsoft
description: Viene illustrato come tooadd nuovi utenti o modificare le informazioni utente in Azure Active Directory.
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
ms.openlocfilehash: 72f67ad41022fd19fd94c8e1301943b0db1e57bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-new-users-or-users-with-microsoft-accounts-tooazure-active-directory"></a><span data-ttu-id="a98a7-103">Aggiungere nuovi utenti o gli utenti con account di Microsoft tooAzure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a98a7-103">Add new users or users with Microsoft accounts tooAzure Active Directory</span></span>
<span data-ttu-id="a98a7-104">Aggiungere gli utenti toopopulate la directory.</span><span class="sxs-lookup"><span data-stu-id="a98a7-104">Add users toopopulate your directory.</span></span> <span data-ttu-id="a98a7-105">Questo articolo viene illustrato come tooadd nuovi utenti nell'organizzazione e come tooadd utenti che dispongono di account Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a98a7-105">This article explains how tooadd new users in your organization, and how tooadd users who have Microsoft accounts.</span></span> <span data-ttu-id="a98a7-106">Per altre informazioni sull'aggiunta di utenti da altre directory in Azure Active Directory o l'aggiunta di utenti da società partner, vedere [Aggiungere utenti da altre directory o società partner in Azure Active Directory](active-directory-create-users-external.md).</span><span class="sxs-lookup"><span data-stu-id="a98a7-106">For more information about adding users from other directories in Azure Active Directory or adding users from partner companies, see [Add users from other directories or partner companies in Azure Active Directory](active-directory-create-users-external.md).</span></span> <span data-ttu-id="a98a7-107">Gli utenti aggiunti non dispongono delle autorizzazioni di amministratore per impostazione predefinita, ma è possibile assegnare ruoli toothem in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="a98a7-107">Added users don't have administrator permissions by default, but you can assign roles toothem at any time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a98a7-108">Si consiglia di gestire Azure AD usando la hello [centro di amministrazione di Azure AD](https://aad.portal.azure.com) in hello portale di Azure anziché hello portale di Azure classico a cui fa riferimento in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="a98a7-108">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span> <span data-ttu-id="a98a7-109">Per la modalità tooadd un utente nell'interfaccia di amministrazione di hello Azure AD, vedere [aggiungere nuovi utenti tooAzure Active Directory](active-directory-users-create-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a98a7-109">For how tooadd a user in hello Azure AD admin center, see [Add new users tooAzure Active Directory](active-directory-users-create-azure-portal.md).</span></span>

## <a name="add-a-user"></a><span data-ttu-id="a98a7-110">Aggiungere un utente</span><span class="sxs-lookup"><span data-stu-id="a98a7-110">Add a user</span></span>
1. <span data-ttu-id="a98a7-111">Accedi toohello [portale di Azure classico](https://manage.windowsazure.com) con un account che sia un amministratore globale per la directory di hello.</span><span class="sxs-lookup"><span data-stu-id="a98a7-111">Sign in toohello [Azure classic portal](https://manage.windowsazure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="a98a7-112">Selezionare **Active Directory**, quindi selezionare il nome di hello della directory dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="a98a7-112">Select **Active Directory**, and then select hello name of your organization directory.</span></span>
3. <span data-ttu-id="a98a7-113">Seleziona hello **utenti** scheda e quindi nella barra dei comandi di hello, selezionare **Aggiungi utente**.</span><span class="sxs-lookup"><span data-stu-id="a98a7-113">Select hello **Users** tab, and then, in hello command bar, select **Add User**.</span></span>
4. <span data-ttu-id="a98a7-114">In hello **informazioni sull'utente** pagina **tipo di utente**, selezionare:</span><span class="sxs-lookup"><span data-stu-id="a98a7-114">On hello **Tell us about this user** page, under **Type of user**, select either:</span></span>

   * <span data-ttu-id="a98a7-115">**Nuovo utente nell'organizzazione** : consente di aggiungere un nuovo account utente nella directory.</span><span class="sxs-lookup"><span data-stu-id="a98a7-115">**New user in your organization** – adds a new user account in your directory.</span></span>
   * <span data-ttu-id="a98a7-116">**Utente con un account Microsoft esistente** : aggiunge un consumer account tooyour directory di Microsoft esistente (ad esempio, un account di Outlook)</span><span class="sxs-lookup"><span data-stu-id="a98a7-116">**User with an existing Microsoft account** – adds an existing Microsoft consumer account tooyour directory (for example, an Outlook account)</span></span>
5. <span data-ttu-id="a98a7-117">In base al **Tipo di utente**immettere un nome utente, per un nuovo utente, o un indirizzo di posta elettronica, per un utente con un account Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a98a7-117">Depending on **Type of user**, enter a user name (for new user) or an email address (for a user with a Microsoft account).</span></span>
6. <span data-ttu-id="a98a7-118">Utente hello **profilo** pagina, fornire un nome e cognome, un nome descrittivo e un ruolo utente da hello **ruoli** elenco.</span><span class="sxs-lookup"><span data-stu-id="a98a7-118">On hello user **Profile** page, provide a first and last name, a user-friendly name, and a user role from hello **Roles** list.</span></span> <span data-ttu-id="a98a7-119">Per altre informazioni sui ruoli utente e di amministratore, vedere [Assegnazione dei ruoli di amministratore in Azure Active Directory](active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="a98a7-119">For more information about user and administrator roles, see [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md).</span></span> <span data-ttu-id="a98a7-120">Specificare se troppo**abilitare multi-Factor Authentication** per utente hello.</span><span class="sxs-lookup"><span data-stu-id="a98a7-120">Specify whether too**Enable Multi-Factor Authentication** for hello user.</span></span>
7. <span data-ttu-id="a98a7-121">In hello **Ottieni password temporanea** selezionare **crea**.</span><span class="sxs-lookup"><span data-stu-id="a98a7-121">On hello **Get temporary password** page, select **Create**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a98a7-122">Se l'organizzazione utilizza più di un dominio, che è necessario conoscere i seguenti problemi quando si aggiunge un account utente di hello:</span><span class="sxs-lookup"><span data-stu-id="a98a7-122">If your organization uses more than one domain, you should know about hello following issues when you add a user account:</span></span>
>
> * <span data-ttu-id="a98a7-123">gli account utente tooadd con hello stesso nome dell'entità utente (UPN) tra i domini, **prima** aggiungere, ad esempio, geoffgrisso@contoso.onmicrosoft.com, **seguito da** geoffgrisso@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="a98a7-123">tooadd user accounts with hello same user principal name (UPN) across domains, **first** add, for example, geoffgrisso@contoso.onmicrosoft.com, **followed by** geoffgrisso@contoso.com.</span></span>
> * <span data-ttu-id="a98a7-124">**Non** aggiungere geoffgrisso@contoso.com prima di aggiungere geoffgrisso@contoso.onmicrosoft.com. Questo ordine è importante e può essere complesso tooundo.</span><span class="sxs-lookup"><span data-stu-id="a98a7-124">**Don't** add geoffgrisso@contoso.com before you add geoffgrisso@contoso.onmicrosoft.com. This order is important, and can be cumbersome tooundo.</span></span>
>
>

## <a name="change-user-information"></a><span data-ttu-id="a98a7-125">Modificare le informazioni utente</span><span class="sxs-lookup"><span data-stu-id="a98a7-125">Change user information</span></span>
<span data-ttu-id="a98a7-126">È possibile modificare qualsiasi attributo utente, ad eccezione di ID di oggetto hello.</span><span class="sxs-lookup"><span data-stu-id="a98a7-126">You can change any user attribute except for hello object ID.</span></span>

1. <span data-ttu-id="a98a7-127">Aprire la directory.</span><span class="sxs-lookup"><span data-stu-id="a98a7-127">Open your directory.</span></span>
2. <span data-ttu-id="a98a7-128">Seleziona hello **utenti** scheda e il nome visualizzato selezionare hello di hello utente desiderato toochange.</span><span class="sxs-lookup"><span data-stu-id="a98a7-128">Select hello **Users** tab, and then select hello display name of hello user you want toochange.</span></span>
3. <span data-ttu-id="a98a7-129">Salvare le modifiche e quindi fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="a98a7-129">Complete your changes, and then click **Save**.</span></span>

<span data-ttu-id="a98a7-130">Se l'utente hello che si desidera modificare è sincronizzato con il servizio Active Directory locale, è possibile modificare le informazioni utente hello mediante questa procedura.</span><span class="sxs-lookup"><span data-stu-id="a98a7-130">If hello user that you're changing is synchronized with your on-premises Active Directory service, you can't change hello user information using this procedure.</span></span> <span data-ttu-id="a98a7-131">utente hello toochange, utilizzare gli strumenti di gestione di Active Directory locale.</span><span class="sxs-lookup"><span data-stu-id="a98a7-131">toochange hello user, use your on-premises Active Directory management tools.</span></span>

## <a name="guest-user-management-and-limitations"></a><span data-ttu-id="a98a7-132">Gestione e limiti dell'utente guest</span><span class="sxs-lookup"><span data-stu-id="a98a7-132">Guest user management and limitations</span></span>
<span data-ttu-id="a98a7-133">Account guest sono utenti da altre directory che sono stati invitati tooyour directory tooaccess SharePoint documenti, applicazioni o altre risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="a98a7-133">Guest accounts are users from other directories who were invited tooyour directory tooaccess SharePoint documents, applications, or other Azure resources.</span></span> <span data-ttu-id="a98a7-134">Un account guest nella directory di dispone dell'attributo di UserType sottostante impostato troppo "Guest".</span><span class="sxs-lookup"><span data-stu-id="a98a7-134">A guest account in your directory has its underlying UserType attribute set too"Guest."</span></span> <span data-ttu-id="a98a7-135">Gli utenti standard (in particolare, i membri della directory) hanno l'attributo UserType hello "Member".</span><span class="sxs-lookup"><span data-stu-id="a98a7-135">Regular users (specifically, members of your directory) have hello UserType attribute "Member."</span></span>

<span data-ttu-id="a98a7-136">Gli utenti guest dispongono di un set limitato di diritti nella directory hello.</span><span class="sxs-lookup"><span data-stu-id="a98a7-136">Guests have a limited set of rights in hello directory.</span></span> <span data-ttu-id="a98a7-137">Questi diritti limitano il possibilità hello per altri utenti nella directory hello informazioni toodiscover guest.</span><span class="sxs-lookup"><span data-stu-id="a98a7-137">These rights limit hello ability for Guests toodiscover information about other users in hello directory.</span></span> <span data-ttu-id="a98a7-138">Tuttavia, gli utenti guest ancora possono interagire con gli utenti di hello e gruppi associati alle risorse di hello che cui stai lavorando.</span><span class="sxs-lookup"><span data-stu-id="a98a7-138">However, guest users can still interact with hello users and groups associated with hello resources they're working on.</span></span> <span data-ttu-id="a98a7-139">Gli utenti guest possono:</span><span class="sxs-lookup"><span data-stu-id="a98a7-139">Guest users can:</span></span>

* <span data-ttu-id="a98a7-140">Vedere altri utenti e gruppi associati toowhich una sottoscrizione di Azure che sono state assegnate</span><span class="sxs-lookup"><span data-stu-id="a98a7-140">See other users and groups associated with an Azure subscription toowhich they're assigned</span></span>
* <span data-ttu-id="a98a7-141">Visualizzare i membri di gruppi toowhich che appartengono hello</span><span class="sxs-lookup"><span data-stu-id="a98a7-141">See hello members of groups toowhich they belong</span></span>
* <span data-ttu-id="a98a7-142">Cercare altri utenti nella directory di hello, se si conosce l'indirizzo di posta elettronica completo hello dell'utente hello</span><span class="sxs-lookup"><span data-stu-id="a98a7-142">Look up other users in hello directory, if they know hello full email address of hello user</span></span>
* <span data-ttu-id="a98a7-143">Vedere solo un set limitato di attributi di utenti hello che sono cercare - toodisplay limitato nome, indirizzo di posta elettronica, nome dell'entità utente (UPN) e foto di anteprima</span><span class="sxs-lookup"><span data-stu-id="a98a7-143">See only a limited set of attributes of hello users they look up--limited toodisplay name, email address, user principal name (UPN), and thumbnail photo</span></span>
* <span data-ttu-id="a98a7-144">Ottenere un elenco dei domini verificati nella directory hello</span><span class="sxs-lookup"><span data-stu-id="a98a7-144">Get a list of verified domains in hello directory</span></span>
* <span data-ttu-id="a98a7-145">Consenso tooapplications, concedere loro hello stessi diritti di accesso che dispongono di membri nella directory</span><span class="sxs-lookup"><span data-stu-id="a98a7-145">Consent tooapplications, granting them hello same access that Members have in your directory</span></span>

## <a name="set-guest-user-access-policies"></a><span data-ttu-id="a98a7-146">Impostare i criteri di accesso degli utenti guest</span><span class="sxs-lookup"><span data-stu-id="a98a7-146">Set guest user access policies</span></span>
<span data-ttu-id="a98a7-147">Hello **configura** scheda di una directory include opzioni toocontrol accesso per gli utenti guest.</span><span class="sxs-lookup"><span data-stu-id="a98a7-147">hello **Configure** tab of a directory includes options toocontrol access for guest users.</span></span> <span data-ttu-id="a98a7-148">Tali opzioni possono essere modificate unicamente da un amministratore globale di directory nel portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="a98a7-148">These options can be changed only in Azure classic portal by a directory global administrator.</span></span> <span data-ttu-id="a98a7-149">Al momento non è disponibile alcun metodo di PowerShell o API.</span><span class="sxs-lookup"><span data-stu-id="a98a7-149">Currently, there's no PowerShell or API method.</span></span>

<span data-ttu-id="a98a7-150">hello tooopen **configura** scheda hello Azure selezionare portale classico **Active Directory**, quindi selezionare il nome di hello della directory hello.</span><span class="sxs-lookup"><span data-stu-id="a98a7-150">tooopen hello **Configure** tab in hello Azure classic portal, select **Active Directory**, and then select hello name of hello directory.</span></span>

![Scheda Configura in Azure Active Directory][1]

<span data-ttu-id="a98a7-152">È quindi possibile modificare l'accesso toocontrol hello opzioni per gli utenti guest.</span><span class="sxs-lookup"><span data-stu-id="a98a7-152">Then you can edit hello options toocontrol access for guest users.</span></span>

![opzioni di controllo di accesso per gli utenti guest][2]

## <a name="whats-next"></a><span data-ttu-id="a98a7-154">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a98a7-154">What's next</span></span>
* [<span data-ttu-id="a98a7-155">Aggiungere utenti da altre directory o società partner in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a98a7-155">Add users from other directories or partner companies in Azure Active Directory</span></span>](active-directory-create-users-external.md)
* [<span data-ttu-id="a98a7-156">Amministrazione di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a98a7-156">Administering Azure AD</span></span>](active-directory-administer.md)
* [<span data-ttu-id="a98a7-157">Gestire password in Azure AD</span><span class="sxs-lookup"><span data-stu-id="a98a7-157">Manage passwords in Azure AD</span></span>](active-directory-manage-passwords.md)
* [<span data-ttu-id="a98a7-158">Gestire gruppi in Azure AD</span><span class="sxs-lookup"><span data-stu-id="a98a7-158">Manage groups in Azure AD</span></span>](active-directory-manage-groups.md)

<!--Image references-->
[1]: ./media/active-directory-create-users/RBACDirConfigTab.png
[2]: ./media/active-directory-create-users/RBACGuestAccessControls.png
