---
title: 'Esercitazione: integrazione di Azure Active Directory con Google Apps in Azure| Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Google Apps.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 38a6ca75-7fd0-4cdc-9b9f-fae080c5a016
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 2093b5ab605ec0d7bbefe7a78e1eede34d756f53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-google-apps"></a>Esercitazione: Integrazione di Azure Active Directory con Google Apps

In questa esercitazione, è illustrato come toointegrate Google Apps con Azure Active Directory (Azure AD).

Integrazione di Google Apps con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooGoogle App
- È possibile abilitare l'utenti tooautomatically get connesso tooGoogle App (Single Sign-On) con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure

Se si desiderano tooknow ulteriori informazioni sull'integrazione di app SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

tooconfigure integrazione di Azure AD con Google Apps, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione di Google Apps abilitata per l'accesso Single Sign-On

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese: [offerta prova](https://azure.microsoft.com/pricing/free-trial/).

## <a name="video-tutorial"></a>Esercitazione video
Come tooEnable Single Sign-On tooGoogle App in 2 minuti:

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Enable-single-sign-on-to-Google-Apps-in-2-minutes-with-Azure-AD/player]

## <a name="frequently-asked-questions"></a>Domande frequenti
1. **D: I dispositivi Chromebooks e altri dispositivi Chrome sono compatibili con Single Sign-On di Azure AD?**
   
    R: Sì, gli utenti sono in grado di toosign in dispositivi Chromebook utilizzando le proprie credenziali di Azure AD. Per informazioni sui motivi per cui agli utenti può essere richiesto di immettere le credenziali due volte, vedere questo [articolo del supporto tecnico di Google Apps](https://support.google.com/chrome/a/answer/6060880) .

2. **D: se Abilita l'accesso single sign-on, sarà possibile toouse in grado di loro toosign le credenziali di Azure AD in qualsiasi prodotto di Google, ad esempio Google corsi, GMail, Google Drive, YouTube e così via?**
   
    R: Sì, in base alle [quali Google apps](https://support.google.com/a/answer/182442?hl=en&ref_topic=1227583) si sceglie tooenable o disabilitare per l'organizzazione.

3. **D: È possibile abilitare il Single Sign-On solo per un sottoinsieme di utenti di Google Apps?**
   
    R: no, attivazione di accesso single sign-on immediatamente richiede tutti i tooauthenticate agli utenti di Google Apps con le proprie credenziali di Azure AD. Provider di identità hello per l'ambiente di Google Apps perché Google Apps non supporta più provider di identità, può essere AD Azure o Google, ma non entrambi hello contemporaneamente.

4. **D: se un utente è connesso tramite Windows, vengono che automaticamente l'autenticazione tooGoogle App senza richiesta di immettere una password?**
   
    R: Sono disponibili due opzioni per l'abilitazione di questo scenario. Nel primo caso gli utenti possono accedere ai dispositivi Windows 10 tramite [Aggiunta ad Azure Active Directory](active-directory-azureadjoin-overview.md). In alternativa, gli utenti accesso è riuscito in dispositivi Windows che tooan appartenenti a un dominio Active Directory a cui è stata abilitata per single sign-on tooAzure AD tramite in locale un [Active Directory Federation Services (ADFS)](active-directory-aadconnect-user-signin.md) distribuzione. Entrambe le opzioni richiedono passaggi hello tooperform hello successivo dell'esercitazione tooenable single sign-on tra Azure AD e Google Apps.

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di Google Apps dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-google-apps-from-hello-gallery"></a>Aggiunta di Google Apps dalla raccolta hello
integrazione hello tooconfigure di Google Apps in Azure AD, è necessario tooadd Google Apps dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd Google Apps dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Applicazioni][2]
    
3. tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.

    ![Applicazioni][3]

4. Nella casella di ricerca hello, digitare **Google Apps**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_search.png)

5. Nel riquadro dei risultati hello, selezionare **Google Apps**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Google Apps usando un utente test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Google Apps è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Google Apps richiede toobe stabilita.

Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in Google Apps.

tooconfigure e test Azure single sign-on AD con Google Apps, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creazione di un utente di test di Google Apps](#creating-a-google-apps-test-user)**  -toohave un equivalente di Britta Simon in Google Apps che è la rappresentazione toohello collegato Azure AD dell'utente.
4. **[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Google Apps.

**Azure AD tooconfigure single sign-on con Google Apps, eseguire hello alla procedura seguente:**

1. Nel portale di Azure su hello hello **Google Apps** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Configura accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_samlbase.png)

3. In hello **dominio Google Apps e gli URL** seguire hello alla procedura seguente:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_url.png)

    In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://mail.google.com/a/<yourdomain>`

    > [!NOTE] 
    > Poiché non è reale, Aggiornare il valore di hello con URL hello effettivo Sign-on. contattare hello [team di supporto di Google](https://www.google.com/contact/).
 
4. In hello **certificato di firma SAML** fare clic su **certificato** e quindi salvare il certificato di hello nel computer in uso.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_certificate.png) 

5. Fare clic sul pulsante **Salva** .

    ![Configura accesso Single Sign-On](./media/active-directory-saas-google-apps-tutorial/tutorial_general_400.png)

6. In hello **Google Apps configurazione** fare clic su **configurare Google Apps** tooopen **Configura sign-on** finestra. Hello copia **Sign-Out URL, SAML Single Sign-On Service URL e Modifica URL password** da hello **sezione di riferimento rapido.**

    ![Configura accesso Single Sign-On](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_configure.png) 

7. Aprire una nuova scheda nel browser e accedere a hello [Console di amministrazione di Google Apps](http://admin.google.com/) con l'account amministratore.

8. Fare clic su **Security**. Se non viene visualizzato il collegamento hello, possono essere nascosti in hello **più controlli** menu in basso hello hello.
   
    ![Fare clic su sicurezza.][10]

9. In hello **sicurezza** pagina, fare clic su **configurare single sign-on (SSO).**
   
    ![Fare clic su SSO.][11]

10. Eseguire hello dopo le modifiche di configurazione:
   
    ![Configurare SSL][12]
   
    a. Selezionare **Setup SSO with third party identity provider** (Configurare l'accesso SSO con un provider di terze parti).

    b. Nel **accesso URL della pagina** campo in Google Apps, incollare il valore di hello di **URL servizio Single Sign-On**, che è stato copiato dal portale di Azure.

    c. In hello **URL pagina di disconnessione** campo in Google Apps, incollare il valore di hello di **Sign-Out URL**, che è stato copiato dal portale di Azure. 

    d. In hello **Modifica URL password** campo in Google Apps, incollare il valore di hello di **Modifica URL password**, che è stato copiato dal portale di Azure. 

    e. In Google Apps, per hello **certificato di verifica**, carica certificato hello scaricato dal portale di Azure.

    f. Fare clic su **Salva modifiche**.

> [!TIP]
> È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!  Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello. È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)
 
### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.

![Creare un utente di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-google-apps-tutorial/create_aaduser_01.png) 

2. elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-google-apps-tutorial/create_aaduser_02.png) 

3. hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-google-apps-tutorial/create_aaduser_03.png) 

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-google-apps-tutorial/create_aaduser_04.png) 

    a. In hello **nome** casella tipo **BrittaSimon**.

    b. In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Show Password** e annotare il valore di hello di hello **Password**.

    d. Fare clic su **Crea**.
 
### <a name="creating-a-google-apps-test-user"></a>Creazione di un utente test di Google Apps

obiettivo di Hello di questa sezione è un utente denominato Britta Simon in Google Apps Software toocreate. Google Apps supporta il provisioning automatico abilitato per impostazione predefinita. Non è necessaria alcuna azione dell'utente in questa sezione. Se un utente non esiste già nel Software di Google Apps, quando si tenta di Google Apps Software tooaccess uno nuovo.

>[!NOTE] 
>Se è necessario un utente toocreate manualmente, contattare hello [team di supporto di Google](https://www.google.com/contact/).

### <a name="assigning-hello-azure-ad-test-user"></a>Assegnazione utente test hello Azure AD

In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooGoogle app.

![Assegna utente][200] 

**tooassign Britta Simon tooGoogle App, eseguire hello alla procedura seguente:**

1. Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **Google Apps**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_app.png) 

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![Assegna utente][202] 

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

In questa sezione, tootest le impostazioni single sign-on, aprire Pannello di accesso a hello [https://myapps.microsoft.com](active-directory-saas-access-panel-introduction.md), quindi accedere all'account di prova hello e fare clic su **Google Apps** riquadro in hello Pannello di accesso.

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)
* [Configura provisioning utenti](active-directory-saas-google-apps-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_203.png

[0]: ./media/active-directory-saas-google-apps-tutorial/azure-active-directory.png

[5]: ./media/active-directory-saas-google-apps-tutorial/gapps-added.png
[6]: ./media/active-directory-saas-google-apps-tutorial/config-sso.png
[7]: ./media/active-directory-saas-google-apps-tutorial/sso-gapps.png
[8]: ./media/active-directory-saas-google-apps-tutorial/sso-url.png
[9]: ./media/active-directory-saas-google-apps-tutorial/download-cert.png
[10]: ./media/active-directory-saas-google-apps-tutorial/gapps-security.png
[11]: ./media/active-directory-saas-google-apps-tutorial/security-gapps.png
[12]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-config.png
[13]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-confirm.png
[14]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-email.png
[15]: ./media/active-directory-saas-google-apps-tutorial/gapps-api.png
[16]: ./media/active-directory-saas-google-apps-tutorial/gapps-api-enabled.png
[17]: ./media/active-directory-saas-google-apps-tutorial/add-custom-domain.png
[18]: ./media/active-directory-saas-google-apps-tutorial/specify-domain.png
[19]: ./media/active-directory-saas-google-apps-tutorial/verify-domain.png
[20]: ./media/active-directory-saas-google-apps-tutorial/gapps-domains.png
[21]: ./media/active-directory-saas-google-apps-tutorial/gapps-add-domain.png
[22]: ./media/active-directory-saas-google-apps-tutorial/gapps-add-another.png
[23]: ./media/active-directory-saas-google-apps-tutorial/apps-gapps.png
[24]: ./media/active-directory-saas-google-apps-tutorial/gapps-provisioning.png
[25]: ./media/active-directory-saas-google-apps-tutorial/gapps-provisioning-auth.png
[26]: ./media/active-directory-saas-google-apps-tutorial/gapps-admin.png
[27]: ./media/active-directory-saas-google-apps-tutorial/gapps-admin-privileges.png
[28]: ./media/active-directory-saas-google-apps-tutorial/gapps-auth.png
[29]: ./media/active-directory-saas-google-apps-tutorial/assign-users.png
[30]: ./media/active-directory-saas-google-apps-tutorial/assign-confirm.png