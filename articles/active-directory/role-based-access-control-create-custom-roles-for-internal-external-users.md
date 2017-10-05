---
title: Creare ruoli personalizzati di controllo degli accessi in base al ruolo e assegnarli a utenti interni ed esterni in Azure | Microsoft Docs
description: Assegnare ruoli personalizzati di controllo degli accessi in base al ruolo creati con PowerShell e l'interfaccia della riga di comando per utenti interni ed esterni
services: active-directory
documentationcenter: 
author: andreicradu
manager: catadinu
editor: kgremban
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/10/2017
ms.author: a-crradu
ms.openlocfilehash: d687f94bebfd0b6c1ec0690da798be5409640954
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
## <a name="intro-on-role-based-access-control"></a><span data-ttu-id="be9c5-103">Introduzione al controllo degli accessi in base al ruolo</span><span class="sxs-lookup"><span data-stu-id="be9c5-103">Intro on role-based access control</span></span>

<span data-ttu-id="be9c5-104">La funzionalità di controllo degli accessi in base al ruolo, disponibile solo nel portale di Azure, consente ai proprietari di una sottoscrizione di assegnare ruoli granulari ad altri utenti, i quali possono gestire ambiti di risorse specifici nel proprio ambiente.</span><span class="sxs-lookup"><span data-stu-id="be9c5-104">Role-based access control is an Azure portal only feature allowing the owners of a subscription to assign granular roles to other users who can manage specific resource scopes in their environment.</span></span>

<span data-ttu-id="be9c5-105">Il controllo degli accessi in base al ruolo consente una migliore gestione della sicurezza nelle organizzazioni di grandi dimensioni e nelle piccole e medie imprese che si avvalgono di collaboratori esterni, fornitori o freelance che hanno necessità di accedere a risorse specifiche nell'ambiente, ma non necessariamente all'intera infrastruttura o agli ambiti correlati alla fatturazione.</span><span class="sxs-lookup"><span data-stu-id="be9c5-105">RBAC allows better security management for large organizations and for SMBs working with external collaborators, vendors or freelancers which need access to specific resources in your environment but not necessarily to the entire infrastructure or any billing-related scopes.</span></span> <span data-ttu-id="be9c5-106">Il controllo degli accessi in base al ruolo consente la flessibilità di possedere una sottoscrizione di Azure gestita dall'account di amministratore (ruolo di amministratore del servizio a livello di sottoscrizione) e di invitare più utenti a usare la stessa sottoscrizione ma senza i diritti amministrativi.</span><span class="sxs-lookup"><span data-stu-id="be9c5-106">RBAC allows the flexibility of owning one Azure subscription managed by the administrator account (service administrator role at a subscription level) and have multiple users invited to work under the same subscription but without any administrative rights for it.</span></span> <span data-ttu-id="be9c5-107">Dal punto di vista della gestione e della fatturazione, la funzionalità di controllo degli accessi in base al ruolo è senza dubbio un'opzione molto efficiente in termini di gestione e tempo per l'uso di Azure in vari scenari.</span><span class="sxs-lookup"><span data-stu-id="be9c5-107">From a management and billing perspective, the RBAC feature proves to be a time and management efficient option for using Azure in various scenarios.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="be9c5-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="be9c5-108">Prerequisites</span></span>
<span data-ttu-id="be9c5-109">L'uso del controllo degli accessi in base al ruolo nell'ambiente di Azure richiede:</span><span class="sxs-lookup"><span data-stu-id="be9c5-109">Using RBAC in the Azure environment requires:</span></span>

* <span data-ttu-id="be9c5-110">Una sottoscrizione di Azure autonoma assegnata all'utente come proprietario (ruolo di sottoscrizione)</span><span class="sxs-lookup"><span data-stu-id="be9c5-110">Having a standalone Azure subscription assigned to the user as owner (subscription role)</span></span>
* <span data-ttu-id="be9c5-111">Il ruolo di proprietario della sottoscrizione di Azure</span><span class="sxs-lookup"><span data-stu-id="be9c5-111">Have the Owner role of the Azure subscription</span></span>
* <span data-ttu-id="be9c5-112">L'accesso al [portale di Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="be9c5-112">Have access to the [Azure portal](https://portal.azure.com)</span></span>
* <span data-ttu-id="be9c5-113">Verificare che i provider di risorse seguenti siano registrati per la sottoscrizione dell'utente: **Microsoft.Authorization**.</span><span class="sxs-lookup"><span data-stu-id="be9c5-113">Make sure to have the following Resource Providers registered for the user subscription: **Microsoft.Authorization**.</span></span> <span data-ttu-id="be9c5-114">Per altre informazioni su come registrare i provider di risorse, vedere [Provider, aree, versioni API e schemi di Resource Manager](/azure-resource-manager/resource-manager-supported-services.md).</span><span class="sxs-lookup"><span data-stu-id="be9c5-114">For more information on how to register the resource providers, see [Resource Manager providers, regions, API versions and schemas](/azure-resource-manager/resource-manager-supported-services.md).</span></span>

> [!NOTE]
> <span data-ttu-id="be9c5-115">Le sottoscrizioni di Office 365 o le licenze di Azure Active Directory, ad esempio l'accesso ad Azure Active Directory, fornite dal portale di Office 365 non danno diritto all'uso del controllo degli accessi in base al ruolo.</span><span class="sxs-lookup"><span data-stu-id="be9c5-115">Office 365 subscriptions or Azure Active Directory licenses (for example: Access to Azure Active Directory) provisioned from the O365 portal don't quality for using RBAC.</span></span>

## <a name="how-can-rbac-be-used"></a><span data-ttu-id="be9c5-116">Modalità d'uso del controllo degli accessi in base al ruolo</span><span class="sxs-lookup"><span data-stu-id="be9c5-116">How can RBAC be used</span></span>
<span data-ttu-id="be9c5-117">Il controllo degli accessi in base al ruolo può essere applicato in tre ambiti diversi in Azure.</span><span class="sxs-lookup"><span data-stu-id="be9c5-117">RBAC can be applied at three different scopes in Azure.</span></span> <span data-ttu-id="be9c5-118">Dal livello più alto al più basso, gli ambiti sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="be9c5-118">From the highest scope to the lowest one, they are as follows:</span></span>

* <span data-ttu-id="be9c5-119">Sottoscrizione (più alto)</span><span class="sxs-lookup"><span data-stu-id="be9c5-119">Subscription (highest)</span></span>
* <span data-ttu-id="be9c5-120">Gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="be9c5-120">Resource group</span></span>
* <span data-ttu-id="be9c5-121">Ambito delle risorse (più basso) che fornisce autorizzazioni mirate per un singolo ambito di risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="be9c5-121">Resource scope (the lowest access level offering targeted permissions to an individual Azure resource scope)</span></span>

## <a name="assign-rbac-roles-at-the-subscription-scope"></a><span data-ttu-id="be9c5-122">Assegnare i ruoli di controllo degli accessi in base al ruolo all'ambito della sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="be9c5-122">Assign RBAC roles at the subscription scope</span></span>
<span data-ttu-id="be9c5-123">Ecco due esempi comuni di uso del controllo degli accessi in base al ruolo:</span><span class="sxs-lookup"><span data-stu-id="be9c5-123">There are two common examples when RBAC is used (but not limited to):</span></span>

* <span data-ttu-id="be9c5-124">Utenti esterni alle organizzazioni (non inclusi nel tenant di Azure Active Directory dell'utente amministratore) invitati a gestire risorse specifiche o l'intera sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="be9c5-124">Having external users from the organizations (not part of the admin user's Azure Active Directory tenant) invited to manage certain resources or the whole subscription</span></span>
* <span data-ttu-id="be9c5-125">Collaborazione con utenti all'interno dell'organizzazione (inclusi nel tenant di Azure Active Directory dell'utente), ma appartenenti a team o gruppi diversi che necessitano di un accesso granulare all'intera sottoscrizione o a determinati ambiti o gruppi di risorse nell'ambiente</span><span class="sxs-lookup"><span data-stu-id="be9c5-125">Working with users inside the organization (they are part of the user's Azure Active Directory tenant) but part of different teams or groups which need granular access either to the whole subscription or to certain resource groups or resource scopes in the environment</span></span>

## <a name="grant-access-at-a-subscription-level-for-a-user-outside-of-azure-active-directory"></a><span data-ttu-id="be9c5-126">Concedere l'accesso a livello di sottoscrizione per un utente all'esterno di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="be9c5-126">Grant access at a subscription level for a user outside of Azure Active Directory</span></span>
<span data-ttu-id="be9c5-127">I ruoli di controllo degli accessi in base al ruolo possono essere concessi solo dai **proprietari** della sottoscrizione; l'utente amministratore deve essere registrato con un nome utente che ha preassegnato questo ruolo o che ha creato la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="be9c5-127">RBAC roles can be granted only by **Owners** of the subscription therefore the admin user must be logged with a username which has this role pre-assigned or has created the Azure subscription.</span></span>

<span data-ttu-id="be9c5-128">Dopo avere eseguito l'accesso come amministratore dal portale di Azure selezionare "Sottoscrizioni" e scegliere quella desiderata.</span><span class="sxs-lookup"><span data-stu-id="be9c5-128">From the Azure portal, after you sign-in as admin, select “Subscriptions” and chose the desired one.</span></span>
<span data-ttu-id="be9c5-129">![Pannello delle sottoscrizioni nel portale di Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/0.png) Per impostazione predefinita, se l'utente amministratore ha acquistato la sottoscrizione di Azure, l'utente verrà visualizzato come **amministratore dell'account**, vale a dire con il ruolo di sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="be9c5-129">![subscription blade in Azure portal](./media/role-based-access-control-create-custom-roles-for-internal-external-users/0.png) By default, if the admin user has purchased the Azure subscription, the user will show up as **Account Admin**, this being the subscription role.</span></span> <span data-ttu-id="be9c5-130">Per altri dettagli sui ruoli di sottoscrizione di Azure, vedere [Aggiungere o modificare i ruoli di amministratore di Azure che gestiscono la sottoscrizione o i servizi](/billing/billing-add-change-azure-subscription-administrator.md).</span><span class="sxs-lookup"><span data-stu-id="be9c5-130">For more details on the Azure subscription roles, see [Add or change Azure administrator roles that manage the subscription or services](/billing/billing-add-change-azure-subscription-administrator.md).</span></span>

<span data-ttu-id="be9c5-131">In questo esempio l'utente "alflanigan@outlook.com" è **Proprietario** della sottoscrizione nella "versione di valutazione gratuita" nel tenant AAD "Default tenant Azure".</span><span class="sxs-lookup"><span data-stu-id="be9c5-131">In this example, the user "alflanigan@outlook.com" is the **Owner** of the "Free Trial" subscription in the AAD tenant "Default tenant Azure".</span></span> <span data-ttu-id="be9c5-132">Poiché questo utente ha creato la sottoscrizione di Azure con l'account Microsoft iniziale "Outlook" (account Microsoft = Outlook, Live e così via), il nome di dominio predefinito per tutti gli altri utenti aggiunti in questo tenant sarà **"@alflaniganuoutlook.onmicrosoft.com"**.</span><span class="sxs-lookup"><span data-stu-id="be9c5-132">Since this user is the creator of the Azure subscription with the initial Microsoft Account “Outlook” (Microsoft Account = Outlook, Live etc.) the default domain name for all other users added in this tenant will be **"@alflaniganuoutlook.onmicrosoft.com"**.</span></span> <span data-ttu-id="be9c5-133">Per impostazione predefinita, la sintassi del nuovo dominio è costituita dalla combinazione di nome utente e nome dominio dell'utente che ha creato il tenant con l'aggiunta dell'estensione **".onmicrosoft.com"**.</span><span class="sxs-lookup"><span data-stu-id="be9c5-133">By design, the syntax of the new domain is formed by putting together the username and domain name of the user who created the tenant and adding the extension **".onmicrosoft.com"**.</span></span>
<span data-ttu-id="be9c5-134">Inoltre gli utenti possono accedere con un nome di dominio personalizzato nel tenant dopo averlo aggiunto e verificato per il nuovo tenant.</span><span class="sxs-lookup"><span data-stu-id="be9c5-134">Furthermore, users can sign-in with a custom domain name in the tenant after adding and verifying it for the new tenant.</span></span> <span data-ttu-id="be9c5-135">Per altre informazioni su come verificare un nome di dominio personalizzato in un tenant di Azure Active Directory, vedere [Aggiungere un nome di dominio personalizzato alla directory](/active-directory/active-directory-add-domain).</span><span class="sxs-lookup"><span data-stu-id="be9c5-135">For more details on how to verify a custom domain name in an Azure Active Directory tenant, see [Add a custom domain name to your directory](/active-directory/active-directory-add-domain).</span></span>

<span data-ttu-id="be9c5-136">In questo esempio la directory "Default tenant Azure" contiene solo gli utenti con il nome di dominio "@alflanigan.onmicrosoft.com".</span><span class="sxs-lookup"><span data-stu-id="be9c5-136">In this example, the "Default tenant Azure" directory contains only users with the domain name "@alflanigan.onmicrosoft.com".</span></span>

<span data-ttu-id="be9c5-137">Dopo avere selezionato la sottoscrizione, l'utente amministratore deve fare clic su **Controllo di accesso (IAM)** e quindi su **Aggiungi nuovo ruolo**.</span><span class="sxs-lookup"><span data-stu-id="be9c5-137">After selecting the subscription, the admin user must click **Access Control (IAM)** and then **Add a new role**.</span></span>





![funzione IAM di controllo di accesso nel portale di Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/1.png)





![aggiungere un nuovo utente nella funzione IAM di controllo di accesso nel portale di Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/2.png)

<span data-ttu-id="be9c5-140">Il passaggio successivo consiste nel selezionare il ruolo da assegnare e l'utente a cui verrà assegnato il ruolo di controllo degli accessi in base al ruolo.</span><span class="sxs-lookup"><span data-stu-id="be9c5-140">The next step is to select the role to be assigned and the user whom the RBAC role will be assigned to.</span></span> <span data-ttu-id="be9c5-141">Nel menu a discesa **Ruolo** l'utente amministratore vede solo i ruoli predefiniti di controllo degli accessi in base al ruolo disponibili in Azure.</span><span class="sxs-lookup"><span data-stu-id="be9c5-141">In the **Role** dropdown menu the admin user sees only the built-in RBAC roles which are available in Azure.</span></span> <span data-ttu-id="be9c5-142">Per altre descrizioni di ogni ruolo e dei relativi ambiti assegnabili, vedere [Ruoli predefiniti per il controllo degli accessi in base al ruolo di Azure](/active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="be9c5-142">For more detailed explanations of each role and their assignable scopes, see [Built-in roles for Azure Role-Based Access Control](/active-directory/role-based-access-built-in-roles.md).</span></span>

<span data-ttu-id="be9c5-143">L'utente amministratore deve quindi aggiungere l'indirizzo e-mail dell'utente esterno.</span><span class="sxs-lookup"><span data-stu-id="be9c5-143">The admin user then needs to add the email address of the external user.</span></span> <span data-ttu-id="be9c5-144">Per l'utente esterno il comportamento previsto è quello di non essere visibile nel tenant esistente.</span><span class="sxs-lookup"><span data-stu-id="be9c5-144">The expected behavior is for the external user to not show up in the existing tenant.</span></span> <span data-ttu-id="be9c5-145">Dopo che è stato invitato, l'utente esterno sarà visibile in **Sottoscrizioni > Controllo di accesso (IAM)** con tutti gli utenti correnti assegnati attualmente a un ruolo di controllo degli accessi in base al ruolo nell'ambito della sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="be9c5-145">After the external user has been invited, he will be visible under **Subscriptions > Access Control (IAM)** with all the current users which are currently assigned an RBAC role at the Subscription scope.</span></span>





![aggiungere autorizzazioni al nuovo ruolo di controllo degli accessi in base al ruolo](./media/role-based-access-control-create-custom-roles-for-internal-external-users/3.png)





![elenco di ruoli di controllo degli accessi in base al ruolo a livello di sottoscrizione](./media/role-based-access-control-create-custom-roles-for-internal-external-users/4.png)

<span data-ttu-id="be9c5-148">L'utente "chessercarlton@gmail.com" è stato inviato ad essere un **proprietario** per la sottoscrizione nella "versione di valutazione gratuita".</span><span class="sxs-lookup"><span data-stu-id="be9c5-148">The user "chessercarlton@gmail.com" has been invited to be an **Owner** for the “Free Trial” subscription.</span></span> <span data-ttu-id="be9c5-149">Dopo avere inviato l'invito, l'utente esterno riceverà una conferma tramite posta elettronica con un collegamento di attivazione.</span><span class="sxs-lookup"><span data-stu-id="be9c5-149">After sending the invitation, the external user will receive an email confirmation with an activation link.</span></span>
<span data-ttu-id="be9c5-150">![Invito tramite posta elettronica per il ruolo di controllo degli accessi in base al ruolo](./media/role-based-access-control-create-custom-roles-for-internal-external-users/5.png)</span><span class="sxs-lookup"><span data-stu-id="be9c5-150">![email invitation for RBAC role](./media/role-based-access-control-create-custom-roles-for-internal-external-users/5.png)</span></span>

<span data-ttu-id="be9c5-151">Essendo esterno all'organizzazione, il nuovo utente non dispone degli attributi esistenti nella directory "Default tenant Azure".</span><span class="sxs-lookup"><span data-stu-id="be9c5-151">Being external to the organization, the new user does not have any existing attributes in the "Default tenant Azure" directory.</span></span> <span data-ttu-id="be9c5-152">Questi verranno creati previo consenso dell'utente esterno alla registrazione nella directory associata alla sottoscrizione per cui gli è stato assegnato un ruolo.</span><span class="sxs-lookup"><span data-stu-id="be9c5-152">They will be created after the external user has given consent to be recorded in the directory which is associated with the subscription which he has been assigned a role to.</span></span>





![messaggio di invito tramite posta elettronica per il ruolo di controllo degli accessi in base al ruolo](./media/role-based-access-control-create-custom-roles-for-internal-external-users/6.png)

<span data-ttu-id="be9c5-154">L'utente esterno diventa visibile nel tenant di Azure Active Directory da questo momento in poi come utente esterno e può essere visualizzato sia nel portale di Azure sia nel portale classico.</span><span class="sxs-lookup"><span data-stu-id="be9c5-154">The external user shows in the Azure Active Directory tenant from now on as external user and this can be viewed both in the Azure portal and in the classic portal.</span></span>





![pannello utenti azure active directory portale di Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/7.png)





![pannello utenti azure active directory portale di Azure classico](./media/role-based-access-control-create-custom-roles-for-internal-external-users/8.png)

<span data-ttu-id="be9c5-157">Nella visualizzazione **Utenti** in entrambi i portali gli utenti esterni possono essere riconosciuti da:</span><span class="sxs-lookup"><span data-stu-id="be9c5-157">In the **Users** view in both portals the external users can be recognized by:</span></span>

* <span data-ttu-id="be9c5-158">Il tipo di icona diverso nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="be9c5-158">The different icon type in the Azure portal</span></span>
* <span data-ttu-id="be9c5-159">Il punto di origine diverso nel portale classico</span><span class="sxs-lookup"><span data-stu-id="be9c5-159">The different sourcing point in the classic portal</span></span>

<span data-ttu-id="be9c5-160">Tuttavia, la concessione dell'accesso come **Proprietario** o **Collaboratore** a un utente esterno nell'ambito della **sottoscrizione**, non consente l'accesso alla directory dell'utente amministratore, a meno che ciò non sia consentito dall'opzione di **amministrazione globale**.</span><span class="sxs-lookup"><span data-stu-id="be9c5-160">However, granting **Owner** or **Contributor** access to an external user at the **Subscription** scope, does not allow the access to the admin user's directory, unless the **Global Admin** allows it.</span></span> <span data-ttu-id="be9c5-161">Nelle proprietà dell'utente è possibile identificare il **tipo di utente** che dispone di due parametri comuni, **Membro** e **Guest**.</span><span class="sxs-lookup"><span data-stu-id="be9c5-161">In the user proprieties,  the **User Type** which has two common parameters, **Member** and **Guest** can be identified.</span></span> <span data-ttu-id="be9c5-162">Un membro è un utente registrato nella directory, mentre un utente guest è un utente invitato nella directory da un'origine esterna.</span><span class="sxs-lookup"><span data-stu-id="be9c5-162">A member is a user which is registered in the directory while a guest is a user invited to the directory from an external source.</span></span> <span data-ttu-id="be9c5-163">Per altre informazioni, vedere [Procedura per aggiungere utenti di Collaborazione B2B ad Azure Active Directory da parte degli amministratori](/active-directory/active-directory-b2b-admin-add-users).</span><span class="sxs-lookup"><span data-stu-id="be9c5-163">For more information, see [How do Azure Active Directory admins add B2B collaboration users](/active-directory/active-directory-b2b-admin-add-users).</span></span>

> [!NOTE]
> <span data-ttu-id="be9c5-164">Assicurarsi che dopo avere immesso le credenziali nel portale, l'utente esterno selezioni la directory corretta a cui accedere.</span><span class="sxs-lookup"><span data-stu-id="be9c5-164">Make sure that after entering the credentials in the portal, the external user selects the correct directory to sign-in to.</span></span> <span data-ttu-id="be9c5-165">Lo stesso utente può avere accesso a più directory e selezionarne una facendo clic sul nome utente nella parte superiore destra nel portale di Azure e quindi scegliere la directory appropriata nell'elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="be9c5-165">The same user can have access to multiple directories and can select either one of  them by clicking the username in the top right-hand side in the Azure portal and then choose the appropriate directory from the dropdown list.</span></span>

<span data-ttu-id="be9c5-166">Pur essendo un utente guest nella directory, l'utente esterno può gestire tutte le risorse per la sottoscrizione di Azure, ma non è in grado di accedere alla directory.</span><span class="sxs-lookup"><span data-stu-id="be9c5-166">While being a guest in the directory, the external user can manage all resources for the Azure subscription, but can't access the directory.</span></span>





![accesso limitato ad Azure Active Directory nel portale di Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/9.png)

<span data-ttu-id="be9c5-168">Azure Active Directory e una sottoscrizione di Azure non hanno una relazione padre-figlio come quella che hanno altre risorse di Azure, ad esempio le macchine virtuali, le reti virtuali, le app Web, le risorse di archiviazione e così via, con una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="be9c5-168">Azure Active Directory and an Azure subscription don't have a child-parent relation like other Azure resources (for example: virtual machines, virtual networks, web apps, storage etc.) have with an Azure subscription.</span></span> <span data-ttu-id="be9c5-169">Tutte queste ultime vengono create, gestite e fatturate in una sottoscrizione di Azure, mentre una sottoscrizione di Azure viene usata per gestire l'accesso a una directory di Azure.</span><span class="sxs-lookup"><span data-stu-id="be9c5-169">All the latter is created, managed and billed under an Azure subscription while an Azure subscription is used to manage the access to an Azure directory.</span></span> <span data-ttu-id="be9c5-170">Per altre informazioni, vedere [Associare le sottoscrizioni di Azure ad Azure Active Directory](/active-directory/active-directory-how-subscriptions-associated-directory).</span><span class="sxs-lookup"><span data-stu-id="be9c5-170">For more details, see [How an Azure subscription is related to Azure AD](/active-directory/active-directory-how-subscriptions-associated-directory).</span></span>

<span data-ttu-id="be9c5-171">Da tutti i ruoli predefiniti di controllo degli accessi in base al ruolo, **Proprietario** e **Collaboratore** offrono l'accesso completo a livello di gestione a tutte le risorse nell'ambiente, ma il ruolo Collaboratore non può creare ed eliminare nuovi ruoli di controllo degli accessi in base al ruolo.</span><span class="sxs-lookup"><span data-stu-id="be9c5-171">From all the built-in RBAC roles, **Owner** and **Contributor** offer full management access to all resources in the environment, the difference being that a Contributor can't create and delete new RBAC roles.</span></span> <span data-ttu-id="be9c5-172">Altri ruoli predefiniti, come **Collaboratore Macchina Virtuale**, offrono l'accesso completo a livello di gestione solo alle risorse indicate dal nome, indipendentemente dal **gruppo di risorse** in cui sono state create.</span><span class="sxs-lookup"><span data-stu-id="be9c5-172">The other built-in roles like **Virtual Machine Contributor** offer full management access only to the resources indicated by the name, regardless of the **Resource Group** they are being created into.</span></span>

<span data-ttu-id="be9c5-173">L'assegnazione del ruolo predefinito di controllo degli accessi in base al ruolo **Collaboratore Macchina Virtuale** a livello di sottoscrizione implica che all'utente a cui è stato assegnato il ruolo seguente:</span><span class="sxs-lookup"><span data-stu-id="be9c5-173">Assigning the built-in RBAC role of **Virtual Machine Contributor** at a subscription level, means that the user assigned the role:</span></span>

* <span data-ttu-id="be9c5-174">Può visualizzare tutte le macchine virtuali indipendentemente dalla data di distribuzione e dai gruppi di risorse di appartenenza</span><span class="sxs-lookup"><span data-stu-id="be9c5-174">Can view all virtual machines regardless their deployment date and the resource groups they are part of</span></span>
* <span data-ttu-id="be9c5-175">Ha accesso completo a livello di gestione alle macchine virtuali nella sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="be9c5-175">Has full management access to the virtual machines in the subscription</span></span>
* <span data-ttu-id="be9c5-176">Non può visualizzare gli altri tipi di risorse nella sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="be9c5-176">Can't view any other resource types in the subscription</span></span>
* <span data-ttu-id="be9c5-177">Non può applicare modifiche dalla prospettiva della fatturazione</span><span class="sxs-lookup"><span data-stu-id="be9c5-177">Can't operate any changes from a billing perspective</span></span>

> [!NOTE]
> <span data-ttu-id="be9c5-178">Il controllo degli accessi in base al ruolo non concede l'accesso al portale classico poiché è una funzionalità disponibile solo nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="be9c5-178">RBAC being an Azure portal only feature, it doesn't grant access to the classic portal.</span></span>

## <a name="assign-a-built-in-rbac-role-to-an-external-user"></a><span data-ttu-id="be9c5-179">Assegnare un ruolo predefinito di controllo degli accessi in base al ruolo a un utente esterno</span><span class="sxs-lookup"><span data-stu-id="be9c5-179">Assign a built-in RBAC role to an external user</span></span>
<span data-ttu-id="be9c5-180">Per uno scenario diverso in questo test, l'utente esterno "alflanigan@gmail.com" viene aggiunto come **Collaboratore Macchina virtuale**.</span><span class="sxs-lookup"><span data-stu-id="be9c5-180">For a different scenario in this test, the external user "alflanigan@gmail.com" is added as a **Virtual Machine Contributor**.</span></span>




![ruolo predefinito collaboratore macchina virtuale](./media/role-based-access-control-create-custom-roles-for-internal-external-users/11.png)

<span data-ttu-id="be9c5-182">Il comportamento normale per questo utente esterno con questo ruolo predefinito è visualizzare e gestire solo le macchine virtuali e solo le risorse di Resource Manager adiacenti necessarie durante la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="be9c5-182">The normal behavior for this external user with this built-in role is to see and manage only virtual machines and their adjacent Resource Manager only resources necessary while deploying.</span></span> <span data-ttu-id="be9c5-183">Per impostazione predefinita, questi ruoli limitati consentono l'accesso solo alle risorse corrispondenti create nel portale di Azure, indipendentemente dal fatto che alcune possano essere distribuite anche nel portale classico, ad esempio le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="be9c5-183">By design, these limited roles offer access only to their correspondent resources created in the Azure portal, regardless some can still be deployed in the classic portal as well (for example: virtual machines).</span></span>





![Panoramica del ruolo Collaboratore macchina virtuale nel portale di Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/12.png)

## <a name="grant-access-at-a-subscription-level-for-a-user-in-the-same-directory"></a><span data-ttu-id="be9c5-185">Concedere l'accesso a livello di sottoscrizione per un utente nella stessa directory</span><span class="sxs-lookup"><span data-stu-id="be9c5-185">Grant access at a subscription level for a user in the same directory</span></span>
<span data-ttu-id="be9c5-186">Il flusso del processo è identico all'aggiunta di un utente esterno sia dal punto di vista dell'amministratore che concede il ruolo di controllo degli accessi in base al ruolo sia dal punto di vista dell'utente a cui viene concesso l'accesso al ruolo.</span><span class="sxs-lookup"><span data-stu-id="be9c5-186">The process flow is identical to adding an external user, both from the admin perspective granting the RBAC role as well as the user being granted access to the role.</span></span> <span data-ttu-id="be9c5-187">La differenza è che l'utente invitato non riceverà gli inviti tramite posta elettronica e tutti gli ambiti di risorse nella sottoscrizione saranno disponibili nel dashboard dopo l'accesso.</span><span class="sxs-lookup"><span data-stu-id="be9c5-187">The difference here is that the invited user will not receive any email invitations as all the resource scopes within the subscription will be available in the dashboard after signing in.</span></span>

## <a name="assign-rbac-roles-at-the-resource-group-scope"></a><span data-ttu-id="be9c5-188">Assegnare ruoli di controllo degli accessi in base al ruolo nell'ambito del gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="be9c5-188">Assign RBAC roles at the resource group scope</span></span>
<span data-ttu-id="be9c5-189">L'assegnazione di un ruolo di controllo degli accessi in base al ruolo nell'ambito del **gruppo di risorse** prevede un processo identico per l'assegnazione del ruolo a livello di sottoscrizione per entrambi i tipi di utenti: esterni o interni (appartenenti alla stessa directory).</span><span class="sxs-lookup"><span data-stu-id="be9c5-189">Assigning an RBAC role at a **Resource Group** scope has an identical process for assigning the role at the subscription level, for both types of users - either external or internal (part of the same directory).</span></span> <span data-ttu-id="be9c5-190">Gli utenti a cui viene assegnato il ruolo di controllo degli accessi in base al ruolo vedono nel proprio ambiente solo il gruppo di risorse per cui gli è stato assegnato l'accesso dall'icona **Gruppi di risorse** nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="be9c5-190">The users which are assigned the RBAC role is to see in their environment only the resource group they have been assigned access from the **Resource Groups** icon in the Azure portal.</span></span>

## <a name="assign-rbac-roles-at-the-resource-scope"></a><span data-ttu-id="be9c5-191">Assegnare ruoli di controllo degli accessi in base al ruolo nell'ambito delle risorse</span><span class="sxs-lookup"><span data-stu-id="be9c5-191">Assign RBAC roles at the resource scope</span></span>
<span data-ttu-id="be9c5-192">Il processo di assegnazione di un ruolo di controllo degli accessi in base al ruolo nell'ambito delle risorse in Azure è identico per l'assegnazione del ruolo a livello di sottoscrizione o di gruppo di risorse, seguendo lo stesso flusso di lavoro per entrambi gli scenari.</span><span class="sxs-lookup"><span data-stu-id="be9c5-192">Assigning an RBAC role at a resource scope in Azure has an identical process for assigning the role at the subscription level or at the resource group level, following the same workflow for both scenarios.</span></span> <span data-ttu-id="be9c5-193">Anche in questo caso, gli utenti assegnati al ruolo di controllo degli accessi in base al ruolo possono vedere solo gli elementi per cui gli è stato assegnato l'accesso nella scheda **Tutte le risorse** o direttamente nel dashboard.</span><span class="sxs-lookup"><span data-stu-id="be9c5-193">Again, the users which are assigned the RBAC role can see only the items that they have been assigned access to, either in the **All Resources** tab or directly in their dashboard.</span></span>

<span data-ttu-id="be9c5-194">Un aspetto importante per il controllo degli accessi in base al ruolo nell'ambito del gruppo di risorse o delle risorse è che gli utenti devono eseguire l'accesso alla directory corretta.</span><span class="sxs-lookup"><span data-stu-id="be9c5-194">An important aspect for RBAC both at resource group scope or resource scope is for the users to make sure to sign-in to the correct directory.</span></span>





![accesso alla directory nel portale di Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/13.png)

## <a name="assign-rbac-roles-for-an-azure-active-directory-group"></a><span data-ttu-id="be9c5-196">Assegnare ruoli di controllo degli accessi in base al ruolo per un gruppo di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="be9c5-196">Assign RBAC roles for an Azure Active Directory group</span></span>
<span data-ttu-id="be9c5-197">Tutti gli scenari che usano il controllo degli accessi in base al ruolo nei tre ambiti diversi in Azure offrono il privilegio di gestione, distribuzione e amministrazione di varie risorse come utente assegnato, senza la necessità di gestire una sottoscrizione personale.</span><span class="sxs-lookup"><span data-stu-id="be9c5-197">All the scenarios using RBAC at the three different scopes in Azure offer the privilege of managing, deploying and administering various resources as an assigned user without the need of managing a personal subscription.</span></span> <span data-ttu-id="be9c5-198">Indipendentemente dal fatto che venga assegnato il ruolo di controllo degli accessi in base al ruolo nell'ambito di una sottoscrizione, di un gruppo di risorse o delle risorse, tutte le risorse create successivamente dagli utenti assegnati vengono fatturate per la sottoscrizione di Azure a cui gli utenti hanno accesso.</span><span class="sxs-lookup"><span data-stu-id="be9c5-198">Regardless the RBAC role is assigned for a subscription, resource group or resource scope, all the resources created further on by the assigned users are billed under the one Azure subscription where the users have access to.</span></span> <span data-ttu-id="be9c5-199">In questo modo gli utenti con autorizzazioni di amministratore per la fatturazione per l'intera sottoscrizione di Azure hanno una panoramica completa sul consumo, indipendentemente da chi gestisce le risorse.</span><span class="sxs-lookup"><span data-stu-id="be9c5-199">This way, the users who have billing administrator permissions for that entire Azure subscription has a complete overview on the consumption, regardless who is managing the resources.</span></span>

<span data-ttu-id="be9c5-200">Per le organizzazioni di dimensioni maggiori, i ruoli di controllo degli accessi in base al ruolo possono essere applicati allo stesso modo per i gruppi di Azure Active Directory considerando la prospettiva che l'utente amministratore intenda concedere l'accesso granulare a team o a interi reparti, non singolarmente per ogni utente; si tratta quindi di un'opzione molto efficiente in termini di gestione e tempo.</span><span class="sxs-lookup"><span data-stu-id="be9c5-200">For larger organizations, RBAC roles can be applied in the same way for Azure Active Directory groups considering the perspective that the admin user wants to grant the granular access for teams or entire departments, not individually for each user, thus considering it as an extremely time and management efficient option.</span></span> <span data-ttu-id="be9c5-201">Per illustrare questo esempio, il ruolo **Collaboratore** è stato aggiunto a uno dei gruppi nel tenant a livello di sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="be9c5-201">To illustrate this example, the **Contributor** role has been added to one of the groups in the tenant at the subscription level.</span></span>





![aggiungere il ruolo di controllo degli accessi in base al ruolo per i gruppi AAD](./media/role-based-access-control-create-custom-roles-for-internal-external-users/14.png)

<span data-ttu-id="be9c5-203">Questi gruppi sono gruppi di sicurezza di cui viene eseguito il provisioning e la gestione solo all'interno di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="be9c5-203">These groups are security groups which are provisioned and managed only within Azure Active Directory.</span></span>

## <a name="create-a-custom-rbac-role-to-open-support-requests-using-powershell"></a><span data-ttu-id="be9c5-204">Creare un ruolo personalizzato di controllo degli accessi in base al ruolo per aprire richieste di supporto usando PowerShell</span><span class="sxs-lookup"><span data-stu-id="be9c5-204">Create a custom RBAC role to open support requests using PowerShell</span></span>
<span data-ttu-id="be9c5-205">I ruoli predefiniti di controllo degli accessi in base al ruolo disponibili in Azure assicurano determinati livelli di autorizzazione in base alle risorse disponibili nell'ambiente.</span><span class="sxs-lookup"><span data-stu-id="be9c5-205">The built-in RBAC roles which are available in Azure ensure certain permission levels based on the available resources in the environment.</span></span> <span data-ttu-id="be9c5-206">Se tuttavia nessuno di questi ruoli è adatto alle esigenze dell'utente amministratore, è possibile limitare ulteriormente l'accesso creando ruoli personalizzati di controllo degli accessi in base al ruolo.</span><span class="sxs-lookup"><span data-stu-id="be9c5-206">However, if none of these roles suit the admin user's needs, there is the option to limit access even more by creating custom RBAC roles.</span></span>

<span data-ttu-id="be9c5-207">Per la creazione di ruoli personalizzati è necessario usare un ruolo predefinito, modificarlo e importarlo di nuovo nell'ambiente.</span><span class="sxs-lookup"><span data-stu-id="be9c5-207">Creating custom RBAC roles requires to take one built-in role, edit it and then import it back in the environment.</span></span> <span data-ttu-id="be9c5-208">Il download e l'upload del ruolo vengono gestiti usando PowerShell o l'interfaccia della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="be9c5-208">The download and upload of the role are managed using either PowerShell or CLI.</span></span>

<span data-ttu-id="be9c5-209">È importante comprendere i prerequisiti per la creazione di un ruolo personalizzato che può concedere l'accesso granulare a livello di sottoscrizione e consentire all'utente invitato la flessibilità di aprire richieste di supporto.</span><span class="sxs-lookup"><span data-stu-id="be9c5-209">It is important to understand the prerequisites of creating a custom role which can grant granular access at the subscription level and also allow the invited user the flexibility of opening support requests.</span></span>

<span data-ttu-id="be9c5-210">In questo esempio è stato personalizzato il ruolo predefinito **Lettore**, che consente agli utenti di accedere di visualizzare tutti gli ambiti di risorse ma non di modificarli o di crearne uno nuovo, per consentire all'utente di aprire richieste di supporto.</span><span class="sxs-lookup"><span data-stu-id="be9c5-210">For this example the built-in role **Reader** which allows users access to view all the resource scopes but not to edit them or create new ones has been customized to allow the user the option of opening support requests.</span></span>

<span data-ttu-id="be9c5-211">La prima azione di esportazione del ruolo **Lettore** deve essere completata in PowerShell con autorizzazioni elevate come amministratore.</span><span class="sxs-lookup"><span data-stu-id="be9c5-211">The first action of exporting the **Reader** role needs to be completed in PowerShell ran with elevated permissions as administrator.</span></span>

```
Login-AzureRMAccount

Get-AzureRMRoleDefinition -Name "Reader"

Get-AzureRMRoleDefinition -Name "Reader" | ConvertTo-Json | Out-File C:\rbacrole2.json

```





![Screenshot di PowerShell per il ruolo Lettore di controllo degli accessi in base al ruolo](./media/role-based-access-control-create-custom-roles-for-internal-external-users/15.png)

<span data-ttu-id="be9c5-213">È quindi necessario estrarre il modello JSON del ruolo.</span><span class="sxs-lookup"><span data-stu-id="be9c5-213">Then you need to extract the JSON template of the role.</span></span>





![Modello JSON per il ruolo personalizzato Lettore di controllo degli accessi in base al ruolo](./media/role-based-access-control-create-custom-roles-for-internal-external-users/16.png)

<span data-ttu-id="be9c5-215">Un tipico ruolo di controllo degli accessi in base al ruolo è composto da tre sezioni principali, **Actions**, **NotActions** e **AssignableScopes**.</span><span class="sxs-lookup"><span data-stu-id="be9c5-215">A typical RBAC role is composed out of three main sections, **Actions**, **NotActions** and **AssignableScopes**.</span></span>

<span data-ttu-id="be9c5-216">Nella sezione **Azione** vengono elencate tutte le operazioni consentite per questo ruolo.</span><span class="sxs-lookup"><span data-stu-id="be9c5-216">In the **Action** section are listed all the permitted operations for this role.</span></span> <span data-ttu-id="be9c5-217">È importante tenere presente che ogni azione viene assegnata da un provider di risorse.</span><span class="sxs-lookup"><span data-stu-id="be9c5-217">It's important to understand that each action is assigned from a resource provider.</span></span> <span data-ttu-id="be9c5-218">In questo caso per la creazione di ticket di supporto è necessario che sia elencato il provider di risorse **Microsoft.Support**.</span><span class="sxs-lookup"><span data-stu-id="be9c5-218">In this case, for creating support tickets the **Microsoft.Support** resource provider must be listed.</span></span>

<span data-ttu-id="be9c5-219">Per poter visualizzare tutti i provider di risorse disponibili e registrati nella sottoscrizione, è possibile usare PowerShell.</span><span class="sxs-lookup"><span data-stu-id="be9c5-219">To be able to see all the resource providers available and registered in your subscription, you can use PowerShell.</span></span>
```
Get-AzureRMResourceProvider

```
<span data-ttu-id="be9c5-220">Inoltre è possibile cercare di tutti i cmdlet di PowerShell disponibili per gestire i provider di risorse.</span><span class="sxs-lookup"><span data-stu-id="be9c5-220">Additionally, you can check for the all the available PowerShell cmdlets to manage the resource providers.</span></span>
    <span data-ttu-id="be9c5-221">![Screenshot di PowerShell per la gestione dei provider di risorse](./media/role-based-access-control-create-custom-roles-for-internal-external-users/17.png)</span><span class="sxs-lookup"><span data-stu-id="be9c5-221">![PowerShell screenshot for resource provider management](./media/role-based-access-control-create-custom-roles-for-internal-external-users/17.png)</span></span>

<span data-ttu-id="be9c5-222">Per limitare tutte le azioni di uno specifico ruolo di controllo degli accessi in base al ruolo, i provider di risorse sono elencati nella sezione **NotActions**.</span><span class="sxs-lookup"><span data-stu-id="be9c5-222">To restrict all the actions for a particular RBAC role, resource providers are listed under the section **NotActions**.</span></span>
<span data-ttu-id="be9c5-223">Infine è obbligatorio che il ruolo di controllo degli accessi in base al ruolo contenga gli ID di sottoscrizione espliciti in cui viene usato.</span><span class="sxs-lookup"><span data-stu-id="be9c5-223">Last, it's mandatory that the RBAC role contains the explicit subscription IDs where it is used.</span></span> <span data-ttu-id="be9c5-224">Gli ID di sottoscrizione sono elencati in **AssignableScopes**; in caso contrario non sarà possibile importare il ruolo nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="be9c5-224">The subscription IDs are listed under the **AssignableScopes**, otherwise you will not be allowed to import the role in your subscription.</span></span>

<span data-ttu-id="be9c5-225">Dopo la creazione e la personalizzazione del ruolo di controllo degli accessi in base al ruolo, è necessario reimportarlo nell'ambiente.</span><span class="sxs-lookup"><span data-stu-id="be9c5-225">After creating and customizing the RBAC role, it needs to be imported back the environment.</span></span>

```
New-AzureRMRoleDefinition -InputFile "C:\rbacrole2.json"

```

<span data-ttu-id="be9c5-226">In questo esempio il nome personalizzato per questo ruolo di controllo degli accessi in base al ruolo è "Reader support tickets access level" che consente all'utente di visualizzare tutti gli elementi nella sottoscrizione e di aprire le richieste di supporto.</span><span class="sxs-lookup"><span data-stu-id="be9c5-226">In this example, the custom name for this RBAC role is "Reader support tickets access level" allowing the user to view everything in the subscription and also to open support requests.</span></span>

> [!NOTE]
> <span data-ttu-id="be9c5-227">Esistono solo due ruoli predefiniti di controllo degli accessi in base al ruolo che consentono di aprire richieste di supporto: **Proprietario** e **Collaboratore**.</span><span class="sxs-lookup"><span data-stu-id="be9c5-227">The only two built-in RBAC roles allowing the action of opening of support requests are **Owner** and **Contributor**.</span></span> <span data-ttu-id="be9c5-228">Per consentire a un utente di aprire richieste di supporto, è necessario che gli sia stato assegnato un ruolo di controllo degli accessi in base al ruolo solo nell'ambito della sottoscrizione perché tutte le richieste di supporto vengono create in base a una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="be9c5-228">For a user to be able to open support requests, he must be assigned an RBAC role only at the subscription scope, because all support requests are created based on an Azure subscription.</span></span>

<span data-ttu-id="be9c5-229">Questo nuovo ruolo personalizzato è stato assegnato a un utente della stessa directory.</span><span class="sxs-lookup"><span data-stu-id="be9c5-229">This new custom role has been assigned to an user from the same directory.</span></span>





![screenshot del ruolo di controllo degli accessi in base al ruolo importati nel portale di Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/18.png)





![screenshot dell'assegnazione dei ruoli di controllo degli accessi in base al ruolo importati personalizzati all'utente della stessa directory](./media/role-based-access-control-create-custom-roles-for-internal-external-users/19.png)





![screenshot delle autorizzazioni per il ruolo personalizzato importato di controllo degli accessi in base al ruolo](./media/role-based-access-control-create-custom-roles-for-internal-external-users/20.png)

<span data-ttu-id="be9c5-233">Altri dettagli nell'esempio evidenziano i limiti di questo ruolo personalizzato, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="be9c5-233">The example has been further detailed to emphasize the limits of this custom RBAC role as follows:</span></span>
* <span data-ttu-id="be9c5-234">Può creare nuove richieste di supporto</span><span class="sxs-lookup"><span data-stu-id="be9c5-234">Can create new support requests</span></span>
* <span data-ttu-id="be9c5-235">Non può creare nuovi ambiti di risorse, ad esempio la macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="be9c5-235">Can't create new resource scopes (for example: virtual machine)</span></span>
* <span data-ttu-id="be9c5-236">Non può creare nuovi gruppi di risorse</span><span class="sxs-lookup"><span data-stu-id="be9c5-236">Can't create new resource groups</span></span>





![screenshot del ruolo personalizzato di controllo degli accessi in base al ruolo che crea richieste di supporto](./media/role-based-access-control-create-custom-roles-for-internal-external-users/21.png)





![screenshot del ruolo personalizzato di controllo degli accessi in base al ruolo che non può creare VM](./media/role-based-access-control-create-custom-roles-for-internal-external-users/22.png)





![screenshot del ruolo personalizzato di controllo degli accessi in base al ruolo che non può creare nuovi gruppi di risorse](./media/role-based-access-control-create-custom-roles-for-internal-external-users/23.png)

## <a name="create-a-custom-rbac-role-to-open-support-requests-using-azure-cli"></a><span data-ttu-id="be9c5-240">Creare un ruolo personalizzato di controllo degli accessi in base al ruolo per aprire richieste di supporto usando l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="be9c5-240">Create a custom RBAC role to open support requests using Azure CLI</span></span>
<span data-ttu-id="be9c5-241">Per l'esecuzione su un Mac e senza dover accedere a PowerShell, l'interfaccia della riga di comando di Azure è la soluzione adatta.</span><span class="sxs-lookup"><span data-stu-id="be9c5-241">Running on a Mac and without having access to PowerShell, Azure CLI is the way to go.</span></span>

<span data-ttu-id="be9c5-242">I passaggi per creare un ruolo personalizzato sono gli stessi, con l'unica eccezione che quando si usa l'interfaccia della riga di comando non è possibile scaricare il ruolo in un modello JSON, ma è possibile visualizzarlo nell'interfaccia della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="be9c5-242">The steps to create a custom role are the same, with the sole exception that using CLI the role can't be downloaded in a JSON template, but it can be viewed in the CLI.</span></span>

<span data-ttu-id="be9c5-243">In questo esempio è stato scelto il ruolo predefinito **Lettore di backup**.</span><span class="sxs-lookup"><span data-stu-id="be9c5-243">For this example I have chosen the built-in role of **Backup Reader**.</span></span>

```

azure role show "backup reader" --json

```





![Screenshot dell'interfaccia della riga di comando del ruolo di lettore backup](./media/role-based-access-control-create-custom-roles-for-internal-external-users/24.png)

<span data-ttu-id="be9c5-245">Modificando il ruolo in Visual Studio dopo la copia delle proprietà in un modello JSON, il provider di risorse **Microsoft.Support** è stato aggiunto nelle sezioni **Azioni** in modo che questo utente possa aprire le richieste di supporto pur continuando a essere un lettore per gli insiemi di credenziali di backup.</span><span class="sxs-lookup"><span data-stu-id="be9c5-245">Editing the role in Visual Studio after copying the proprieties in a JSON template, the **Microsoft.Support** resource provider has been added in the **Actions** sections so that this user can open support requests while continuing to be a reader for the backup vaults.</span></span> <span data-ttu-id="be9c5-246">Anche in questo caso è necessario aggiungere l'ID sottoscrizione in cui verrà usato questo ruolo nella sezione **AssignableScopes**.</span><span class="sxs-lookup"><span data-stu-id="be9c5-246">Again it is necessary to add the subscription ID where this role will be used in the **AssignableScopes** section.</span></span>

```

azure role create --inputfile <path>

```





![Screenshot dell'interfaccia della riga di comando di importazione del ruolo personalizzato di controllo degli accessi in base al ruolo](./media/role-based-access-control-create-custom-roles-for-internal-external-users/25.png)

<span data-ttu-id="be9c5-248">Il nuovo ruolo è ora disponibile nel portale di Azure e il processo di assegnazione è lo stesso descritto negli esempi precedenti.</span><span class="sxs-lookup"><span data-stu-id="be9c5-248">The new role is now available in the Azure portal and the assignation process is the same as in the previous examples.</span></span>





![Screenshot del portale di Azure del ruolo personalizzato di controllo degli accessi in base al ruolo creato usando l'interfaccia della riga di comando 1.0](./media/role-based-access-control-create-custom-roles-for-internal-external-users/26.png)

<span data-ttu-id="be9c5-250">Al momento della build 2017 aggiornata, Azure Cloud Shell è disponibile a livello generale.</span><span class="sxs-lookup"><span data-stu-id="be9c5-250">As of the latest Build 2017, the Azure Cloud Shell is generally available.</span></span> <span data-ttu-id="be9c5-251">Azure Cloud Shell è complementare all'ambiente IDE e al portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="be9c5-251">Azure Cloud Shell is a complement to IDE and the Azure Portal.</span></span> <span data-ttu-id="be9c5-252">Con questo servizio si ottiene una shell basata su browser autenticata e ospitata in Azure che è possibile usare al posto dell'interfaccia della riga di comando installata nel computer.</span><span class="sxs-lookup"><span data-stu-id="be9c5-252">With this service, you get a browser-based shell that is authenticated and hosted within Azure and you can use it instead of CLI installed on your machine.</span></span>





![Azure Cloud Shell](./media/role-based-access-control-create-custom-roles-for-internal-external-users/27.png)
