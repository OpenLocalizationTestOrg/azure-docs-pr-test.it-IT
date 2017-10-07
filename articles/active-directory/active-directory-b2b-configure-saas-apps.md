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
# <a name="configure-saas-apps-for-b2b-collaboration"></a>Configurare app SaaS per Collaborazione B2B

Collaborazione B2B di Azure Active Directory (Azure AD) funziona con la maggior parte delle app che si integrano con Azure AD. Questa sezione contiene istruzioni per configurare alcune popolari app SaaS per l'uso con Collaborazione B2B di Azure AD.

Prima di esaminare le istruzioni specifiche delle app, ecco alcune regole generali:

* Per la maggior parte delle App hello, configurazione utente deve toohappen manualmente. Vale a dire utenti devono essere creati manualmente in anche l'applicazione hello.

* Per le applicazioni che supportano l'installazione automatica, ad esempio Dropbox, inviti distinti vengono creati da app hello. Gli utenti devono essere tooaccept che ogni invito.

* Gli attributi utente hello, eventuali problemi con il disco di profilo utente modificato (UDP) in utenti guest toomitigate sempre impostato **identificatore utente** troppo**user.mail**.


## <a name="dropbox-business"></a>Dropbox Business

tooenable toosign di utenti con l'account dell'organizzazione, è necessario configurare manualmente toouse Business dell'area di sincronizzazione Azure AD come provider di identità Security Assertion Markup Language (SAML). Se Business Dropbox non è stato configurato toodo in tal caso, non può richiedere o in caso contrario consentire toosign gli utenti con Azure AD.

1. tooadd hello Business Dropbox app in Azure AD, selezionare **applicazioni aziendali** in hello riquadro sinistro e quindi fare clic su **Aggiungi**.

  ![pulsante "Aggiungi" Hello nella pagina applicazioni di Enterprise hello](media/active-directory-b2b-configure-saas-apps/add-dropbox.png)

2. In hello **aggiungere un'applicazione** finestra immettere **dropbox** in hello casella di ricerca e quindi selezionare **Dropbox for Business** nell'elenco risultati hello.

  ![Cercare "dropbox" su hello aggiungere una pagina dell'applicazione](media/active-directory-b2b-configure-saas-apps/add-app-dialog.png)

3. In hello **Single sign-on** selezionare **Single sign-on** in hello riquadro sinistro e quindi immettere **user.mail** in hello **identificatore utente** casella. Verrà impostato come nome UPN per impostazione predefinita.

  ![Configurazione di single sign-on per app hello](media/active-directory-b2b-configure-saas-apps/configure-app-sso.png)

4. toodownload hello certificato toouse per la configurazione dell'area di sincronizzazione, selezionare **configurare DropBox**, quindi selezionare **SAML Single Sign On Service URL** nell'elenco di hello.

  ![Download del certificato di hello per la configurazione dell'area di sincronizzazione](media/active-directory-b2b-configure-saas-apps/download-certificate.png)

5. Accedi tooDropbox con hello sign-on URL da hello **Single sign-on** pagina.

  ![pagina Hello Accedi Dropbox](media/active-directory-b2b-configure-saas-apps/sign-in-to-dropbox.png)

6. Selezionare menu hello **Console di amministrazione**.

  ![collegamento "Console di amministrazione" Hello menu Dropbox hello](media/active-directory-b2b-configure-saas-apps/dropbox-menu.png)

7. In hello **autenticazione** nella finestra di dialogo **più**, caricare il certificato di hello e quindi nel hello **URL accesso** , immettere l'URL di hello SAML single sign-on.

  ![Hello collegamento "Informazioni" nella finestra di dialogo autenticazione hello compresso](media/active-directory-b2b-configure-saas-apps/dropbox-auth-01.png)

  ![Ciao "Sign in URL" hello espanso la finestra di dialogo di autenticazione](media/active-directory-b2b-configure-saas-apps/paste-single-sign-on-URL.png)

8. Selezionare il programma di installazione di tooconfigure automatico degli utenti nel portale di Azure hello **Provisioning** nel riquadro sinistro hello selezionare **automatica** in hello **modalità di Provisioning** e quindi selezionare **Autorizzare**.

  ![Configurazione del provisioning utente automatico nel portale di Azure hello](media/active-directory-b2b-configure-saas-apps/set-up-automatic-provisioning.png)

Dopo aver impostati gli utenti guest o un membro hello Dropbox App, ricevono un invito separato da Dropbox. toouse Dropbox single sign-on, concedere agli invitati deve accettare invito hello facendo clic su un collegamento in essa contenuti.

## <a name="box"></a>Box
È possibile abilitare gli utenti guest di utenti tooauthenticate casella con il proprio account Azure AD usando la federazione basata sul protocollo SAML hello. In questa procedura è caricare tooBox.com metadati.

1. Aggiungere le app aziendali hello hello casella app.

2. Configurare l'accesso single sign-on in hello seguente ordine:

  ![Configurare Single Sign-On per Box](media/active-directory-b2b-configure-saas-apps/configure-box-sso.png)

 a. In hello **URL di accesso** , verificare che URL hello-sign-on sia impostato in modo appropriato per casella in hello portale di Azure. Questo URL è hello del tenant di Box.com. Deve seguire convenzioni di denominazione hello *https://.box.com*.  
 Hello **identificatore** non si applica toothis app, ma viene comunque visualizzato come un campo obbligatorio.

 b. In hello **identificatore utente** immettere **user.mail** (per SSO per gli account guest).

 c. In **Certificato di firma SAML** fare clic su **Crea nuovo certificato**.

 d. toobegin configurazione il toouse tenant di Box.com Azure AD come provider di identità, scaricare il file di metadati hello e quindi salvarlo tooyour di unità locale.

 e. Inoltrare hello metadati file toohello casella team di supporto, che consente di configurare single sign-on.

3. Per l'installazione automatico degli utenti di Azure AD, nel riquadro di sinistra hello, selezionare **Provisioning**, quindi selezionare **Authorize**.

  ![Autorizzare Azure AD tooconnect tooBox](media/active-directory-b2b-configure-saas-apps/auth-azure-ad-to-connect-to-box.png)

Come concedere agli invitati Dropbox, concedere agli invitati casella necessario riscattare loro invito da app Box hello.

## <a name="next-steps"></a>Passaggi successivi

Vedere i seguenti articoli in collaborazione B2B di Azure AD hello:

* [Che cos'è Azure AD B2B Collaboration?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Proprietà dell'utente di Collaborazione B2B](active-directory-b2b-user-properties.md)
* [Aggiunta di un ruolo di tooa utente collaborazione B2B](active-directory-b2b-add-guest-to-role.md)
* [Delegare gli inviti a Collaborazione B2B](active-directory-b2b-delegate-invitations.md)
* [Gruppi dinamici e Collaborazione B2B](active-directory-b2b-dynamic-groups.md)
* [Codici ed esempi di PowerShell per Collaborazione B2B](active-directory-b2b-code-samples.md)
* [Token utente per Collaborazione B2B](active-directory-b2b-user-token.md)
* [Mapping delle attestazioni utente per Collaborazione B2B](active-directory-b2b-claims-mapping.md)
* [Condivisione esterna di Office 365](active-directory-b2b-o365-external-user.md)
* [Limitazioni correnti di Collaborazione B2B](active-directory-b2b-current-limitations.md)
