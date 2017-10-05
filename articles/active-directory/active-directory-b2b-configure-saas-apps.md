---
title: Configurare app SaaS per Collaborazione B2B in Azure Active Directory | Documentazione Microsoft
description: Codici ed esempi di PowerShell per Collaborazione B2B in Azure Active Directory
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/23/2017
ms.author: sasubram
ms.openlocfilehash: 149a493f7b369415f0a2726dd6a576f0195c13d9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="configure-saas-apps-for-b2b-collaboration"></a><span data-ttu-id="9d369-103">Configurare app SaaS per Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="9d369-103">Configure SaaS apps for B2B collaboration</span></span>

<span data-ttu-id="9d369-104">Collaborazione B2B di Azure Active Directory (Azure AD) funziona con la maggior parte delle app che si integrano con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9d369-104">Azure Active Directory (Azure AD) B2B collaboration works with most apps that integrate with Azure AD.</span></span> <span data-ttu-id="9d369-105">Questa sezione contiene istruzioni per configurare alcune popolari app SaaS per l'uso con Collaborazione B2B di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9d369-105">In this section, we walk through instructions for configuring some popular SaaS apps for use with Azure AD B2B.</span></span>

<span data-ttu-id="9d369-106">Prima di esaminare le istruzioni specifiche delle app, ecco alcune regole generali:</span><span class="sxs-lookup"><span data-stu-id="9d369-106">Before you look at app-specific instructions, here are some rules of thumb:</span></span>

* <span data-ttu-id="9d369-107">Per la maggior parte delle app, la configurazione degli utenti deve essere eseguita manualmente.</span><span class="sxs-lookup"><span data-stu-id="9d369-107">For most of the apps, user setup needs to happen manually.</span></span> <span data-ttu-id="9d369-108">Gli utenti devono quindi essere creati manualmente anche nell'app.</span><span class="sxs-lookup"><span data-stu-id="9d369-108">That is, users must be created manually in the app as well.</span></span>

* <span data-ttu-id="9d369-109">Per le app che supportano la configurazione automatica, come Dropbox, vengono creati inviti separati dalle app.</span><span class="sxs-lookup"><span data-stu-id="9d369-109">For apps that support automatic setup, such as Dropbox, separate invitations are created from the apps.</span></span> <span data-ttu-id="9d369-110">Gli utenti devono assicurarsi di accettare ogni invito.</span><span class="sxs-lookup"><span data-stu-id="9d369-110">Users must be sure to accept each invitation.</span></span>

* <span data-ttu-id="9d369-111">Negli attributi utente, per prevenire eventuali problemi con valori del disco del profilo utente (UPD) modificati negli utenti guest impostare sempre **Identificatore utente** su **user.mail**.</span><span class="sxs-lookup"><span data-stu-id="9d369-111">In the user attributes, to mitigate any issues with mangled user profile disk (UPD) in guest users, always set **User Identifier** to **user.mail**.</span></span>


## <a name="dropbox-business"></a><span data-ttu-id="9d369-112">Dropbox Business</span><span class="sxs-lookup"><span data-stu-id="9d369-112">Dropbox Business</span></span>

<span data-ttu-id="9d369-113">Per consentire agli utenti di accedere con il proprio account aziendale, è necessario configurare manualmente Dropbox Business per l'uso di Azure AD come provider di identità SAML (Security Assertion Markup Language).</span><span class="sxs-lookup"><span data-stu-id="9d369-113">To enable users to sign in using their organization account, you must manually configure Dropbox Business to use Azure AD as a Security Assertion Markup Language (SAML) identity provider.</span></span> <span data-ttu-id="9d369-114">Se non è stato appositamente configurato, Dropbox Business non può richiedere o consentire in altro modo agli utenti di accedere con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9d369-114">If Dropbox Business has not been configured to do so, it cannot prompt or otherwise allow users to sign in using Azure AD.</span></span>

1. <span data-ttu-id="9d369-115">Per aggiungere l'app Dropbox Business in Azure AD, selezionare **Applicazioni aziendali** nel riquadro sinistro e quindi fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="9d369-115">To add the Dropbox Business app into Azure AD, select **Enterprise applications** in the left pane, and then click **Add**.</span></span>

  ![Pulsante "Aggiungi" nella pagina Applicazioni aziendali](media/active-directory-b2b-configure-saas-apps/add-dropbox.png)

2. <span data-ttu-id="9d369-117">Nella finestra **Aggiungi applicazione** immettere **dropbox** nella casella di ricerca e quindi selezionare **Dropbox for Business** nell'elenco dei risultati.</span><span class="sxs-lookup"><span data-stu-id="9d369-117">In the **Add an application** window, enter **dropbox** in the search box, and then select **Dropbox for Business** in the results list.</span></span>

  ![Cercare "dropbox" nella pagina Aggiungi applicazione](media/active-directory-b2b-configure-saas-apps/add-app-dialog.png)

3. <span data-ttu-id="9d369-119">Nella pagina **Single Sign-On** selezionare **Single Sign-On** nel riquadro sinistro e quindi immettere **user.mail** nella casella **Identificatore utente**.</span><span class="sxs-lookup"><span data-stu-id="9d369-119">On the **Single sign-on** page, select **Single sign-on** in the left pane, and then enter **user.mail** in the **User Identifier** box.</span></span> <span data-ttu-id="9d369-120">Verrà impostato come nome UPN per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="9d369-120">(It's set as UPN by default.)</span></span>

  ![Configurare l'accesso Single Sign-On per l'app](media/active-directory-b2b-configure-saas-apps/configure-app-sso.png)

4. <span data-ttu-id="9d369-122">Per scaricare il certificato da usare per la configurazione di Dropbox, selezionare **Configura DropBox** e quindi **SAML Single Sign On Service URL** (URL servizio Single Sign-On SAML) nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="9d369-122">To download the certificate to use for Dropbox configuration, select **Configure DropBox**, and then select **SAML Single Sign On Service URL** in the list.</span></span>

  ![Download del certificato per la configurazione di Dropbox](media/active-directory-b2b-configure-saas-apps/download-certificate.png)

5. <span data-ttu-id="9d369-124">Accedere a Dropbox con l'URL di accesso della pagina **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="9d369-124">Sign in to Dropbox with the sign-on URL from the **Single sign-on** page.</span></span>

  ![Pagina di accesso di Dropbox](media/active-directory-b2b-configure-saas-apps/sign-in-to-dropbox.png)

6. <span data-ttu-id="9d369-126">Nel menu selezionare **Admin Console** (Console di amministrazione).</span><span class="sxs-lookup"><span data-stu-id="9d369-126">On the menu, select **Admin Console**.</span></span>

  ![Collegamento "Admin Console" (Console di amministrazione) nel menu di Dropbox](media/active-directory-b2b-configure-saas-apps/dropbox-menu.png)

7. <span data-ttu-id="9d369-128">Nella finestra di dialogo **Authentication** (Autenticazione) selezionare **More** (Altro), caricare il certificato e quindi immettere l'URL di accesso Single Sign-On SAML nella casella **Sign in URL** (URL di accesso).</span><span class="sxs-lookup"><span data-stu-id="9d369-128">In the **Authentication** dialog box, select **More**, upload the certificate and then, in the **Sign in URL** box, enter the SAML single sign-on URL.</span></span>

  ![Collegamento "More" (Altro) nella finestra di dialogo compressa Authentication (Autenticazione)](media/active-directory-b2b-configure-saas-apps/dropbox-auth-01.png)

  ![Collegamento "Sign in URL" (URL di accesso) nella finestra di dialogo compressa Authentication (Autenticazione)](media/active-directory-b2b-configure-saas-apps/paste-single-sign-on-URL.png)

8. <span data-ttu-id="9d369-131">Per impostare la configurazione automatica degli utenti nel portale di Azure, selezionare **Provisioning** nel riquadro sinistro, quindi **Automatico** nella casella **Modalità di provisioning** e infine **Autorizza**.</span><span class="sxs-lookup"><span data-stu-id="9d369-131">To configure automatic user setup in the Azure portal, select **Provisioning** in the left pane, select **Automatic** in the **Provisioning Mode** box, and then select **Authorize**.</span></span>

  ![Configurazione del provisioning utenti automatico nel portale di Azure](media/active-directory-b2b-configure-saas-apps/set-up-automatic-provisioning.png)

<span data-ttu-id="9d369-133">Al termine della configurazione nell'app Dropbox, gli utenti guest o membro ricevono un invito separato da Dropbox.</span><span class="sxs-lookup"><span data-stu-id="9d369-133">After guest or member users have been set up in the Dropbox app, they receive a separate invitation from Dropbox.</span></span> <span data-ttu-id="9d369-134">Per usare l'accesso Single Sign-On in Dropbox, gli invitati devono accettare l'invito facendo clic su un collegamento in esso contenuto.</span><span class="sxs-lookup"><span data-stu-id="9d369-134">To use Dropbox single sign-on, invitees must accept the invitation by clicking a link in it.</span></span>

## <a name="box"></a><span data-ttu-id="9d369-135">Box</span><span class="sxs-lookup"><span data-stu-id="9d369-135">Box</span></span>
<span data-ttu-id="9d369-136">È possibile consentire agli utenti di autenticare utenti guest Box con il proprio account Azure AD usando la federazione basata sul protocollo SAML.</span><span class="sxs-lookup"><span data-stu-id="9d369-136">You can enable users to authenticate Box guest users with their Azure AD account by using federation that's based on the SAML protocol.</span></span> <span data-ttu-id="9d369-137">In questa procedura si caricano metadati in Box.com.</span><span class="sxs-lookup"><span data-stu-id="9d369-137">In this procedure, you upload metadata to Box.com.</span></span>

1. <span data-ttu-id="9d369-138">Aggiungere l'app Box dalle app aziendali.</span><span class="sxs-lookup"><span data-stu-id="9d369-138">Add the Box app from the enterprise apps.</span></span>

2. <span data-ttu-id="9d369-139">Configurare l'accesso Single Sign-On nell'ordine seguente:</span><span class="sxs-lookup"><span data-stu-id="9d369-139">Configure single sign-on in the following order:</span></span>

  ![Configurare Single Sign-On per Box](media/active-directory-b2b-configure-saas-apps/configure-box-sso.png)

 <span data-ttu-id="9d369-141">a.</span><span class="sxs-lookup"><span data-stu-id="9d369-141">a.</span></span> <span data-ttu-id="9d369-142">Nella casella **URL di accesso** assicurarsi che l'URL di accesso sia impostato correttamente per Box nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="9d369-142">In the **Sign on URL** box, ensure that the sign-on URL is set appropriately for Box in the Azure portal.</span></span> <span data-ttu-id="9d369-143">Si tratta dell'URL del tenant di Box.com</span><span class="sxs-lookup"><span data-stu-id="9d369-143">This URL is the URL of your Box.com tenant.</span></span> <span data-ttu-id="9d369-144">e deve seguire la convenzione di denominazione *https://.box.com*.</span><span class="sxs-lookup"><span data-stu-id="9d369-144">It should follow the naming convention *https://.box.com*.</span></span>  
 <span data-ttu-id="9d369-145">Il campo **Identificatore** non si applica a questa app, ma viene comunque visualizzato come obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="9d369-145">The **Identifier** does not apply to this app, but it still appears as a mandatory field.</span></span>

 <span data-ttu-id="9d369-146">b.</span><span class="sxs-lookup"><span data-stu-id="9d369-146">b.</span></span> <span data-ttu-id="9d369-147">Nella casella **Identificatore utente** immettere **user.mail** (per l'accesso SSO per account guest).</span><span class="sxs-lookup"><span data-stu-id="9d369-147">In the **User identifier** box, enter **user.mail** (for SSO for guest accounts).</span></span>

 <span data-ttu-id="9d369-148">c.</span><span class="sxs-lookup"><span data-stu-id="9d369-148">c.</span></span> <span data-ttu-id="9d369-149">In **Certificato di firma SAML** fare clic su **Crea nuovo certificato**.</span><span class="sxs-lookup"><span data-stu-id="9d369-149">Under **SAML Signing Certificate**, click **Create new certificate**.</span></span>

 <span data-ttu-id="9d369-150">d.</span><span class="sxs-lookup"><span data-stu-id="9d369-150">d.</span></span> <span data-ttu-id="9d369-151">Per iniziare a configurare il tenant di Box.com per l'uso di Azure AD come provider di identità, scaricare il file di metadati e quindi salvarlo nell'unità locale.</span><span class="sxs-lookup"><span data-stu-id="9d369-151">To begin configuring your Box.com tenant to use Azure AD as an identity provider, download the metadata file and then save it to your local drive.</span></span>

 <span data-ttu-id="9d369-152">e.</span><span class="sxs-lookup"><span data-stu-id="9d369-152">e.</span></span> <span data-ttu-id="9d369-153">Inoltrare il file di metadati al team di supporto di Box, che configura l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="9d369-153">Forward the metadata file to the Box support team, which configures single sign-on for you.</span></span>

3. <span data-ttu-id="9d369-154">Per la configurazione automatica degli utenti in Azure AD, nel riquadro sinistro selezionare **Provisioning** e quindi **Autorizza**.</span><span class="sxs-lookup"><span data-stu-id="9d369-154">For Azure AD automatic user setup, in the left pane, select **Provisioning**, and then select **Authorize**.</span></span>

  ![Autorizzare la connessione di Azure AD a Box](media/active-directory-b2b-configure-saas-apps/auth-azure-ad-to-connect-to-box.png)

<span data-ttu-id="9d369-156">Così come gli invitati di Dropbox, gli invitati di Box devono riscattare l'invito proveniente dall'app Box.</span><span class="sxs-lookup"><span data-stu-id="9d369-156">Like Dropbox invitees, Box invitees must redeem their invitation from the Box app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9d369-157">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9d369-157">Next steps</span></span>

<span data-ttu-id="9d369-158">Vedere gli articoli seguenti su Collaborazione B2B di Azure AD:</span><span class="sxs-lookup"><span data-stu-id="9d369-158">See the following articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="9d369-159">Che cos'è Azure AD B2B Collaboration?</span><span class="sxs-lookup"><span data-stu-id="9d369-159">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="9d369-160">Proprietà dell'utente di Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="9d369-160">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="9d369-161">Aggiunta di un utente di Collaborazione B2B a un ruolo</span><span class="sxs-lookup"><span data-stu-id="9d369-161">Adding a B2B collaboration user to a role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="9d369-162">Delegare gli inviti a Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="9d369-162">Delegate B2B collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="9d369-163">Gruppi dinamici e Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="9d369-163">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="9d369-164">Codici ed esempi di PowerShell per Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="9d369-164">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="9d369-165">Token utente per Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="9d369-165">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="9d369-166">Mapping delle attestazioni utente per Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="9d369-166">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="9d369-167">Condivisione esterna di Office 365</span><span class="sxs-lookup"><span data-stu-id="9d369-167">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="9d369-168">Limitazioni correnti di Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="9d369-168">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
