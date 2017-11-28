---
title: App SaaS aaaConfigure per la collaborazione B2B di Azure Active Directory | Documenti Microsoft
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
ms.openlocfilehash: c3f22f81567c04ac23ef2316c09de718ecb15d26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-saas-apps-for-b2b-collaboration"></a><span data-ttu-id="74728-103">Configurare app SaaS per Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="74728-103">Configure SaaS apps for B2B collaboration</span></span>

<span data-ttu-id="74728-104">Collaborazione B2B di Azure Active Directory (Azure AD) funziona con la maggior parte delle app che si integrano con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="74728-104">Azure Active Directory (Azure AD) B2B collaboration works with most apps that integrate with Azure AD.</span></span> <span data-ttu-id="74728-105">Questa sezione contiene istruzioni per configurare alcune popolari app SaaS per l'uso con Collaborazione B2B di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="74728-105">In this section, we walk through instructions for configuring some popular SaaS apps for use with Azure AD B2B.</span></span>

<span data-ttu-id="74728-106">Prima di esaminare le istruzioni specifiche delle app, ecco alcune regole generali:</span><span class="sxs-lookup"><span data-stu-id="74728-106">Before you look at app-specific instructions, here are some rules of thumb:</span></span>

* <span data-ttu-id="74728-107">Per la maggior parte delle App hello, configurazione utente deve toohappen manualmente.</span><span class="sxs-lookup"><span data-stu-id="74728-107">For most of hello apps, user setup needs toohappen manually.</span></span> <span data-ttu-id="74728-108">Vale a dire utenti devono essere creati manualmente in anche l'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="74728-108">That is, users must be created manually in hello app as well.</span></span>

* <span data-ttu-id="74728-109">Per le applicazioni che supportano l'installazione automatica, ad esempio Dropbox, inviti distinti vengono creati da app hello.</span><span class="sxs-lookup"><span data-stu-id="74728-109">For apps that support automatic setup, such as Dropbox, separate invitations are created from hello apps.</span></span> <span data-ttu-id="74728-110">Gli utenti devono essere tooaccept che ogni invito.</span><span class="sxs-lookup"><span data-stu-id="74728-110">Users must be sure tooaccept each invitation.</span></span>

* <span data-ttu-id="74728-111">Gli attributi utente hello, eventuali problemi con il disco di profilo utente modificato (UDP) in utenti guest toomitigate sempre impostato **identificatore utente** troppo**user.mail**.</span><span class="sxs-lookup"><span data-stu-id="74728-111">In hello user attributes, toomitigate any issues with mangled user profile disk (UPD) in guest users, always set **User Identifier** too**user.mail**.</span></span>


## <a name="dropbox-business"></a><span data-ttu-id="74728-112">Dropbox Business</span><span class="sxs-lookup"><span data-stu-id="74728-112">Dropbox Business</span></span>

<span data-ttu-id="74728-113">tooenable toosign di utenti con l'account dell'organizzazione, è necessario configurare manualmente toouse Business dell'area di sincronizzazione Azure AD come provider di identità Security Assertion Markup Language (SAML).</span><span class="sxs-lookup"><span data-stu-id="74728-113">tooenable users toosign in using their organization account, you must manually configure Dropbox Business toouse Azure AD as a Security Assertion Markup Language (SAML) identity provider.</span></span> <span data-ttu-id="74728-114">Se Business Dropbox non è stato configurato toodo in tal caso, non può richiedere o in caso contrario consentire toosign gli utenti con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="74728-114">If Dropbox Business has not been configured toodo so, it cannot prompt or otherwise allow users toosign in using Azure AD.</span></span>

1. <span data-ttu-id="74728-115">tooadd hello Business Dropbox app in Azure AD, selezionare **applicazioni aziendali** in hello riquadro sinistro e quindi fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="74728-115">tooadd hello Dropbox Business app into Azure AD, select **Enterprise applications** in hello left pane, and then click **Add**.</span></span>

  ![pulsante "Aggiungi" Hello nella pagina applicazioni di Enterprise hello](media/active-directory-b2b-configure-saas-apps/add-dropbox.png)

2. <span data-ttu-id="74728-117">In hello **aggiungere un'applicazione** finestra immettere **dropbox** in hello casella di ricerca e quindi selezionare **Dropbox for Business** nell'elenco risultati hello.</span><span class="sxs-lookup"><span data-stu-id="74728-117">In hello **Add an application** window, enter **dropbox** in hello search box, and then select **Dropbox for Business** in hello results list.</span></span>

  ![Cercare "dropbox" su hello aggiungere una pagina dell'applicazione](media/active-directory-b2b-configure-saas-apps/add-app-dialog.png)

3. <span data-ttu-id="74728-119">In hello **Single sign-on** selezionare **Single sign-on** in hello riquadro sinistro e quindi immettere **user.mail** in hello **identificatore utente** casella.</span><span class="sxs-lookup"><span data-stu-id="74728-119">On hello **Single sign-on** page, select **Single sign-on** in hello left pane, and then enter **user.mail** in hello **User Identifier** box.</span></span> <span data-ttu-id="74728-120">Verrà impostato come nome UPN per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="74728-120">(It's set as UPN by default.)</span></span>

  ![Configurazione di single sign-on per app hello](media/active-directory-b2b-configure-saas-apps/configure-app-sso.png)

4. <span data-ttu-id="74728-122">toodownload hello certificato toouse per la configurazione dell'area di sincronizzazione, selezionare **configurare DropBox**, quindi selezionare **SAML Single Sign On Service URL** nell'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="74728-122">toodownload hello certificate toouse for Dropbox configuration, select **Configure DropBox**, and then select **SAML Single Sign On Service URL** in hello list.</span></span>

  ![Download del certificato di hello per la configurazione dell'area di sincronizzazione](media/active-directory-b2b-configure-saas-apps/download-certificate.png)

5. <span data-ttu-id="74728-124">Accedi tooDropbox con hello sign-on URL da hello **Single sign-on** pagina.</span><span class="sxs-lookup"><span data-stu-id="74728-124">Sign in tooDropbox with hello sign-on URL from hello **Single sign-on** page.</span></span>

  ![pagina Hello Accedi Dropbox](media/active-directory-b2b-configure-saas-apps/sign-in-to-dropbox.png)

6. <span data-ttu-id="74728-126">Selezionare menu hello **Console di amministrazione**.</span><span class="sxs-lookup"><span data-stu-id="74728-126">On hello menu, select **Admin Console**.</span></span>

  ![collegamento "Console di amministrazione" Hello menu Dropbox hello](media/active-directory-b2b-configure-saas-apps/dropbox-menu.png)

7. <span data-ttu-id="74728-128">In hello **autenticazione** nella finestra di dialogo **più**, caricare il certificato di hello e quindi nel hello **URL accesso** , immettere l'URL di hello SAML single sign-on.</span><span class="sxs-lookup"><span data-stu-id="74728-128">In hello **Authentication** dialog box, select **More**, upload hello certificate and then, in hello **Sign in URL** box, enter hello SAML single sign-on URL.</span></span>

  ![Hello collegamento "Informazioni" nella finestra di dialogo autenticazione hello compresso](media/active-directory-b2b-configure-saas-apps/dropbox-auth-01.png)

  ![Ciao "Sign in URL" hello espanso la finestra di dialogo di autenticazione](media/active-directory-b2b-configure-saas-apps/paste-single-sign-on-URL.png)

8. <span data-ttu-id="74728-131">Selezionare il programma di installazione di tooconfigure automatico degli utenti nel portale di Azure hello **Provisioning** nel riquadro sinistro hello selezionare **automatica** in hello **modalità di Provisioning** e quindi selezionare **Autorizzare**.</span><span class="sxs-lookup"><span data-stu-id="74728-131">tooconfigure automatic user setup in hello Azure portal, select **Provisioning** in hello left pane, select **Automatic** in hello **Provisioning Mode** box, and then select **Authorize**.</span></span>

  ![Configurazione del provisioning utente automatico nel portale di Azure hello](media/active-directory-b2b-configure-saas-apps/set-up-automatic-provisioning.png)

<span data-ttu-id="74728-133">Dopo aver impostati gli utenti guest o un membro hello Dropbox App, ricevono un invito separato da Dropbox.</span><span class="sxs-lookup"><span data-stu-id="74728-133">After guest or member users have been set up in hello Dropbox app, they receive a separate invitation from Dropbox.</span></span> <span data-ttu-id="74728-134">toouse Dropbox single sign-on, concedere agli invitati deve accettare invito hello facendo clic su un collegamento in essa contenuti.</span><span class="sxs-lookup"><span data-stu-id="74728-134">toouse Dropbox single sign-on, invitees must accept hello invitation by clicking a link in it.</span></span>

## <a name="box"></a><span data-ttu-id="74728-135">Box</span><span class="sxs-lookup"><span data-stu-id="74728-135">Box</span></span>
<span data-ttu-id="74728-136">È possibile abilitare gli utenti guest di utenti tooauthenticate casella con il proprio account Azure AD usando la federazione basata sul protocollo SAML hello.</span><span class="sxs-lookup"><span data-stu-id="74728-136">You can enable users tooauthenticate Box guest users with their Azure AD account by using federation that's based on hello SAML protocol.</span></span> <span data-ttu-id="74728-137">In questa procedura è caricare tooBox.com metadati.</span><span class="sxs-lookup"><span data-stu-id="74728-137">In this procedure, you upload metadata tooBox.com.</span></span>

1. <span data-ttu-id="74728-138">Aggiungere le app aziendali hello hello casella app.</span><span class="sxs-lookup"><span data-stu-id="74728-138">Add hello Box app from hello enterprise apps.</span></span>

2. <span data-ttu-id="74728-139">Configurare l'accesso single sign-on in hello seguente ordine:</span><span class="sxs-lookup"><span data-stu-id="74728-139">Configure single sign-on in hello following order:</span></span>

  ![Configurare Single Sign-On per Box](media/active-directory-b2b-configure-saas-apps/configure-box-sso.png)

 <span data-ttu-id="74728-141">a.</span><span class="sxs-lookup"><span data-stu-id="74728-141">a.</span></span> <span data-ttu-id="74728-142">In hello **URL di accesso** , verificare che URL hello-sign-on sia impostato in modo appropriato per casella in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="74728-142">In hello **Sign on URL** box, ensure that hello sign-on URL is set appropriately for Box in hello Azure portal.</span></span> <span data-ttu-id="74728-143">Questo URL è hello del tenant di Box.com.</span><span class="sxs-lookup"><span data-stu-id="74728-143">This URL is hello URL of your Box.com tenant.</span></span> <span data-ttu-id="74728-144">Deve seguire convenzioni di denominazione hello *https://.box.com*.</span><span class="sxs-lookup"><span data-stu-id="74728-144">It should follow hello naming convention *https://.box.com*.</span></span>  
 <span data-ttu-id="74728-145">Hello **identificatore** non si applica toothis app, ma viene comunque visualizzato come un campo obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="74728-145">hello **Identifier** does not apply toothis app, but it still appears as a mandatory field.</span></span>

 <span data-ttu-id="74728-146">b.</span><span class="sxs-lookup"><span data-stu-id="74728-146">b.</span></span> <span data-ttu-id="74728-147">In hello **identificatore utente** immettere **user.mail** (per SSO per gli account guest).</span><span class="sxs-lookup"><span data-stu-id="74728-147">In hello **User identifier** box, enter **user.mail** (for SSO for guest accounts).</span></span>

 <span data-ttu-id="74728-148">c.</span><span class="sxs-lookup"><span data-stu-id="74728-148">c.</span></span> <span data-ttu-id="74728-149">In **Certificato di firma SAML** fare clic su **Crea nuovo certificato**.</span><span class="sxs-lookup"><span data-stu-id="74728-149">Under **SAML Signing Certificate**, click **Create new certificate**.</span></span>

 <span data-ttu-id="74728-150">d.</span><span class="sxs-lookup"><span data-stu-id="74728-150">d.</span></span> <span data-ttu-id="74728-151">toobegin configurazione il toouse tenant di Box.com Azure AD come provider di identità, scaricare il file di metadati hello e quindi salvarlo tooyour di unità locale.</span><span class="sxs-lookup"><span data-stu-id="74728-151">toobegin configuring your Box.com tenant toouse Azure AD as an identity provider, download hello metadata file and then save it tooyour local drive.</span></span>

 <span data-ttu-id="74728-152">e.</span><span class="sxs-lookup"><span data-stu-id="74728-152">e.</span></span> <span data-ttu-id="74728-153">Inoltrare hello metadati file toohello casella team di supporto, che consente di configurare single sign-on.</span><span class="sxs-lookup"><span data-stu-id="74728-153">Forward hello metadata file toohello Box support team, which configures single sign-on for you.</span></span>

3. <span data-ttu-id="74728-154">Per l'installazione automatico degli utenti di Azure AD, nel riquadro di sinistra hello, selezionare **Provisioning**, quindi selezionare **Authorize**.</span><span class="sxs-lookup"><span data-stu-id="74728-154">For Azure AD automatic user setup, in hello left pane, select **Provisioning**, and then select **Authorize**.</span></span>

  ![Autorizzare Azure AD tooconnect tooBox](media/active-directory-b2b-configure-saas-apps/auth-azure-ad-to-connect-to-box.png)

<span data-ttu-id="74728-156">Come concedere agli invitati Dropbox, concedere agli invitati casella necessario riscattare loro invito da app Box hello.</span><span class="sxs-lookup"><span data-stu-id="74728-156">Like Dropbox invitees, Box invitees must redeem their invitation from hello Box app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="74728-157">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="74728-157">Next steps</span></span>

<span data-ttu-id="74728-158">Vedere i seguenti articoli in collaborazione B2B di Azure AD hello:</span><span class="sxs-lookup"><span data-stu-id="74728-158">See hello following articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="74728-159">Che cos'è Azure AD B2B Collaboration?</span><span class="sxs-lookup"><span data-stu-id="74728-159">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="74728-160">Proprietà dell'utente di Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="74728-160">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="74728-161">Aggiunta di un ruolo di tooa utente collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="74728-161">Adding a B2B collaboration user tooa role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="74728-162">Delegare gli inviti a Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="74728-162">Delegate B2B collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="74728-163">Gruppi dinamici e Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="74728-163">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="74728-164">Codici ed esempi di PowerShell per Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="74728-164">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="74728-165">Token utente per Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="74728-165">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="74728-166">Mapping delle attestazioni utente per Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="74728-166">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="74728-167">Condivisione esterna di Office 365</span><span class="sxs-lookup"><span data-stu-id="74728-167">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="74728-168">Limitazioni correnti di Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="74728-168">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
