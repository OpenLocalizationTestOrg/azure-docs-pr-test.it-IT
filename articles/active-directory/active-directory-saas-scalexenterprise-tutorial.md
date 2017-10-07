---
title: 'Esercitazione: Integrazione di Azure Active Directory con ScaleX Enterprise | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e ScaleX Enterprise.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c2379a8d-a659-45f1-87db-9ba156d83183
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/20/2017
ms.author: jeedes
ms.openlocfilehash: e398b98d9e0957b5f92c82359651c345d22c3a54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-scalex-enterprise"></a>Esercitazione: Integrazione di Azure Active Directory con ScaleX Enterprise

In questa esercitazione, è illustrato come toointegrate ScaleX Enterprise con Azure Active Directory (Azure AD).

Integrazione di ScaleX Enterprise con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooScaleX Enterprise
- È possibile abilitare l'utenti tooautomatically get connesso tooScaleX Enterprise (Single Sign-On) con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere. Informazioni sull'accesso alle applicazioni e Single Sign-On con [Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

integrazione di Azure AD con ScaleX Enterprise tooconfigure, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione di ScaleX Enterprise abilitata per l'accesso Single Sign-On

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione, a meno che non sia necessario.
- Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di ScaleX Enterprise dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-scalex-enterprise-from-hello-gallery"></a>Aggiunta di ScaleX Enterprise dalla raccolta hello
integrazione hello tooconfigure di ScaleX Enterprise in tooAzure Active Directory, è necessario tooadd ScaleX Enterprise dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd ScaleX Enterprise dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Applicazioni][2]
    
3. Fare clic su **Aggiungi** pulsante nella parte superiore di hello della finestra di dialogo hello.

    ![Applicazioni][3]

4. Nella casella di ricerca hello, digitare **ScaleX Enterprise**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_search.png)

5. Nel riquadro dei risultati hello, selezionare **ScaleX Enterprise**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con ScaleX Enterprise con un utente test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in ScaleX Enterprise è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure AD e l'utente correlato di hello in ScaleX Enterprise richiede toobe stabilita.

Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in ScaleX Enterprise.

tooconfigure e prova AD Azure single sign-on con ScaleX Enterprise, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creazione di un utente test ScaleX Enterprise](#creating-a-scalex-enterprise-test-user)**  -toohave un equivalente di Britta Simon in azienda ScaleX che è la rappresentazione toohello collegato Azure AD dell'utente.
4. **[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on in applicazioni aziendali ScaleX.

**Azure AD tooconfigure single sign-on con ScaleX Enterprise, eseguire hello alla procedura seguente:**

1. Nel portale di Azure su hello hello **ScaleX Enterprise** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Configura accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo, come **modalità** selezionare **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_samlbase.png)

3. In hello **ScaleX Enterprise dominio e gli URL** seguire hello procedura seguente se si desidera in un'applicazione hello tooconfigure **IDP** modalità iniziata da:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_url1.png)

    a. In hello **identificatore** casella di testo, valore di tipo hello utilizzando hello modello:`https://platform.rescale.com/saml2/<company id>/`

    b. In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://platform.rescale.com/saml2/<company id>/acs/`

4. Controllare **Mostra URL impostazioni avanzate**, se si desidera in un'applicazione hello tooconfigure **SP** modalità iniziata da:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_url2.png)

    In hello **Sign-on URL** casella di testo, valore di tipo hello utilizzando hello modello:`https://platform.rescale.com/saml2/<company id>/sso/`
     
    > [!NOTE] 
    > Non sono valori reali hello. Aggiornare questi valori con hello identificatore effettivo, l'URL di risposta o URL Sign-On. Contatto [team di supporto Client Enterprise ScaleX](http://info.rescale.com/contact_sales) tooget questi valori. 

5. L'applicazione ScaleX prevede asserzioni SAML hello in un formato specifico, che richiede di toomodify attributo personalizzato configurazione dei mapping tooyour SAML degli attributi del token. Fare clic su **visualizzare e modificare tutti gli altri attributi utente** hello tooopen casella di controllo personalizzato di attributi delle impostazioni.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-scalexenterprise-tutorial/scalex_attributes.png)
    
    a. Fare clic con il pulsante destro attributo hello **nome** e fare clic su Elimina.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-scalexenterprise-tutorial/delete_attribute_name.png)

    b. Fare clic su **emailaddress** finestra Modifica attributo hello tooopen di attributo. Modificare il relativo valore da **user.mail** troppo**User** e fare clic su Ok.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-scalexenterprise-tutorial/edit_email_attribute.png)   
    
5. In hello **certificato di firma SAML** fare clic su **certificato (Base64)** e quindi salvare il file di certificato hello nel computer in uso.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_certificate.png) 

6. Fare clic sul pulsante **Salva** .

    ![Configura accesso Single Sign-On](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_400.png)
    
7. In hello **configurazione aziendale ScaleX** fare clic su **configurare ScaleX Enterprise** tooopen **Configura sign-on** finestra. Hello copia **ID entità SAML** e **SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**

    ![Configura accesso Single Sign-On](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_configure.png) 

8. tooconfigure single sign-on sul **ScaleX Enterprise** lato, sito Web aziendale di account di accesso toohello ScaleX Enterprise come amministratore.

9. Fare clic sul menu hello hello superiore, destro e selezionare **amministrazione Contoso**.

    > [!NOTE] 
    > Contoso è solo un esempio. Deve essere il nome effettivo della società. 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-scalexenterprise-tutorial/Test_Admin.png) 

10. Selezionare **integrazioni** dal menu in alto hello e selezionare **Single Sign-On**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-scalexenterprise-tutorial/admin_sso.png) 

11. Completare il modulo hello come segue:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-scalexenterprise-tutorial/scalex_admin_save.png) 
    
    a. Selezionare **Create any user who can authenticate with SSO** (Crea un utente qualsiasi che può eseguire l'autenticazione con SSO).

    b. **Provider del servizio saml**: incollare il valore di hello ***urn: oasis: nomi: tc: SAML:2.0:nameid-formato: persistente***

    c. **Nome del campo messaggio di posta elettronica di Provider di identità in risposta ACS**: incollare il valore di hello`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`

    d. **ID entità EntityDescriptor Provider di identità:** hello Incolla **ID entità SAML** valore copiato dal portale di Azure hello.

    e. **Identity Provider URL SingleSignOnService:** hello Incolla **SAML Single Sign-On Service URL** da hello portale di Azure.

    f. **Certificato X509 pubblico di Provider di identità:** certificato aprire hello X509 scaricato da hello Azure nel blocco note e incollare contenuto hello in questa casella. Verificare che siano che non interruzioni di riga hello intermedia hello contenuto del certificato.
    
    g. Controllare hello seguenti caselle di controllo: **Enabled, crittografare NameID e AuthnRequests Sign.**

    h. Fare clic su **le impostazioni di aggiornamento SSO** impostazioni hello toosave.

> [!TIP]
> È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!  Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello. È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.

![Creare un utente di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_01.png) 

2. Andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti** elenco hello toodisplay degli utenti.
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_02.png) 

3. Nella parte superiore di hello della finestra di dialogo hello, fare clic su **Aggiungi** tooopen hello **utente** finestra di dialogo.
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_03.png) 

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_04.png) 

    a. In hello **nome** casella tipo **BrittaSimon**.

    b. In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Show Password** e annotare il valore di hello di hello **Password**.

    d. Fare clic su **Crea**.
 
### <a name="creating-a-scalex-enterprise-test-user"></a>Creazione di un utente test ScaleX Enterprise

toolog agli utenti di Azure AD tooenable in tooScaleX Enterprise, è necessario eseguirne il provisioning in tooScaleX Enterprise. Nel caso di hello di ScaleX Enterprise, il provisioning è un'attività automatica e non manuali sono necessari passaggi. Tutti gli utenti possono eseguire l'autenticazione con credenziali SSO verranno automaticamente eseguito il provisioning in hello ScaleX lato.

### <a name="assigning-hello-azure-ad-test-user"></a>Assegnazione utente test hello Azure AD

In questa sezione è abilitare Britta Simon toouse single sign-on Azure concedendo Enterprise tooScaleX di accesso utente.

![Assegna utente][200] 

**tooassign Britta Simon tooScaleX Enterprise, eseguire hello alla procedura seguente:**

1. Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **ScaleX Enterprise**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_app.png) 

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![Assegna utente][202] 

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.

### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.

Fare clic su hello ScaleX Enterprise riquadro in hello Pannello di accesso, si otterranno automaticamente firmato in tooyour applicazione ScaleX aziendale. Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](https://msdn.microsoft.com/library/dn308586).


## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_203.png

