---
title: 'Esercitazione: Integrazione di Azure Active Directory con DocuSign | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e DocuSign.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a691288b-84c1-40fb-84bd-5b06878865f0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: e4ef40b8f5af20d811d8d806d2bd7e2039c55052
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-docusign"></a>Esercitazione: Integrazione di Azure Active Directory con DocuSign

In questa esercitazione, è illustrato come toointegrate DocuSign con Azure Active Directory (Azure AD).

Integrazione di DocuSign con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooDocuSign
- È possibile abilitare l'utenti tooautomatically get connesso tooDocuSign (Single Sign-On) con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

integrazione di Azure AD con DocuSign tooconfigure, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Una sottoscrizione di DocuSign abilitata per l'accesso Single Sign-On

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di DocuSign dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-docusign-from-hello-gallery"></a>Aggiunta di DocuSign dalla raccolta hello
integrazione hello tooconfigure di DocuSign in Azure AD, è necessario tooadd DocuSign dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd DocuSign dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Applicazioni][2]
    
3. Fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo hello.

    ![Applicazioni][3]

4. Nella casella di ricerca hello, digitare **DocuSign**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_search.png)

5. Nel riquadro dei risultati hello, selezionare **DocuSign**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con DocuSign in base a un utente test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in DocuSign è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in DocuSign deve toobe stabilita.

Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in DocuSign.

tooconfigure e test Azure single sign-on AD con DocuSign, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creazione di un utente test DocuSign](#creating-a-docusign-test-user)**  -toohave un equivalente di Britta Simon in DocuSign che è la rappresentazione toohello collegato Azure AD dell'utente.
4. **[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione DocuSign.

**Azure AD tooconfigure single sign-on con DocuSign, eseguire hello alla procedura seguente:**

1. Nel portale di Azure su hello hello **DocuSign** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Configura accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_samlbase.png)

3. In hello **certificato di firma SAML** fare clic su **certificato (Base 64)** e quindi salvare il file di certificato nel computer in uso.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_certificate.png) 

4. In hello **DocuSign configurazione** sezione del portale di Azure, fare clic su **DocuSign configurare** finestra tooopen Configura sign-on. Hello copia **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_configure.png)

5. In una finestra del web browser, account di accesso tooyour **il portale di amministrazione di DocuSign** come amministratore.

6. Nel menu di navigazione hello hello sinistra, fare clic su **domini**.
   
    ![Configurazione dell'accesso Single Sign-On][51]

7. Nel riquadro di destra hello, fare clic su **dominio attestazione**.
   
    ![Configurazione dell'accesso Single Sign-On][52]

8. In hello **un dominio di attestazioni** finestra di dialogo, in hello **nome di dominio** casella di testo, digitare il dominio aziendale e quindi fare clic su **attestazione**. Assicurarsi che si verifica il dominio di hello e hello stato sia attivo.
   
    ![Configurazione dell'accesso Single Sign-On][53]

9. Scegliere dal menu sul lato sinistro hello **provider di identità**  
   
    ![Configurazione dell'accesso Single Sign-On][54]
10. Nel riquadro di destra hello, fare clic su **Add Identity Provider**. 
   
    ![Configurazione dell'accesso Single Sign-On][55]

11. In hello **impostazioni del Provider di identità** eseguire hello alla procedura seguente:
   
    ![Configurazione dell'accesso Single Sign-On][56]

    a. In hello **nome** casella di testo, digitare un nome univoco per la configurazione. Non usare spazi.

    b. Incolla **ID entità SAML** in hello **Identity Provider Issuer** casella di testo.

    c. Incolla **SAML Single Sign-On Service URL** in hello **Identity Provider Login URL** casella di testo.

    d. Incolla **Sign-Out URL** in hello **Identity Provider Logout URL** casella di testo.

    e. Selezionare **Sign AuthN Request**(Firma richiesta di autenticazione).

    f. Per **Invia richiesta di autenticazione da** selezionare **POST**.

    g. Per **Invia richiesta di disconnessione da** selezionare **GET**.

12. In hello **Mapping di attributi personalizzati** , scegliere il campo hello desiderato toomap con Azure AD attestazioni. In questo esempio hello **emailaddress** viene eseguito il mapping di un'attestazione con valore hello **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**. Nome di attestazione predefinito hello da Azure AD per l'attestazione di posta elettronica è. 
   
    > [!NOTE]
    > Hello uso appropriato **identificatore utente** utente hello toomap dal mapping utente tooDocuSign di Azure AD. Selezionare hello campo appropriato e immettere hello valore appropriato in base alle impostazioni dell'organizzazione.
          
    ![Configurazione dell'accesso Single Sign-On][57]

13. In hello **Identity Provider Certificate** fare clic su **Aggiungi certificato**e quindi caricare il certificato di hello scaricato dal portale di Azure AD.   
   
    ![Configurazione dell'accesso Single Sign-On][58]

14. Fare clic su **Salva**.

15. In hello **provider di identità** fare clic su **azioni**, quindi fare clic su **endpoint**.   
   
    ![Configurazione dell'accesso Single Sign-On][59]
 
16. In hello **Visualizza SAML 2.0 endpoint** sezione **il portale di amministrazione di DocuSign**, eseguire hello alla procedura seguente:
   
    ![Configurazione dell'accesso Single Sign-On][60]
   
    a. Hello copia **URL autorità di certificazione di servizio Provider**e quindi incollare in hello **identificatore** nella casella di testo **DocuSign dominio e gli URL** sezione di hello Azure hello seguente del portale motivo: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/login/sp/<uniqueID>`.
   
    b. Hello copia **Service Provider Login URL**e quindi incollare in hello **URL di accesso** nella casella di testo **DocuSign dominio e gli URL** sezione di hello Azure hello seguente del portale motivo: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/`.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_url.png)
      
    c.  Fare clic su **Close**
    
17. Nel portale di Azure hello, fare clic su **salvare**.
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-docusign-tutorial/tutorial_general_400.png)

> [!TIP]
> È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!  Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello. È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.

![Creare un utente di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-docusign-tutorial/create_aaduser_01.png) 

2. elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-docusign-tutorial/create_aaduser_02.png) 

3. Nella parte superiore di hello della finestra di dialogo hello, fare clic su **Aggiungi** tooopen hello **utente** finestra di dialogo.
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-docusign-tutorial/create_aaduser_03.png) 

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-docusign-tutorial/create_aaduser_04.png) 

    a. In hello **nome** casella tipo **BrittaSimon**.

    b. In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Show Password** e annotare il valore di hello di hello **Password**.

    d. Fare clic su **Crea**.
 
### <a name="creating-a-docusign-test-user"></a>Creazione di un utente test di DocuSign

Supporta l'applicazione **immediatamente provisioning in-time utente** e dopo l'autenticazione degli utenti viene creato automaticamente in un'applicazione hello.

### <a name="assigning-hello-azure-ad-test-user"></a>Assegnazione utente test hello Azure AD

In questa sezione è abilitare Britta Simon toouse single sign-on Azure concedendo tooDocuSign proprio accesso.

![Assegna utente][200] 

**tooassign Britta Simon tooDocuSign, eseguire hello alla procedura seguente:**

1. Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **DocuSign**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_app.png) 

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![Assegna utente][202] 

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.

Quando si fa clic su riquadro DocuSign hello in hello Pannello di accesso, è necessario ottenere tooyour automaticamente firmato in DocuSign applicazione.
Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)
* [Configura provisioning utenti](active-directory-saas-docusign-provisioning-tutorial.md)


<!--Image references-->

[1]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_04.png
[51]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_21.png
[52]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_22.png
[53]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_23.png
[54]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_19.png
[55]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_20.png
[56]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_24.png
[57]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_25.png
[58]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_26.png
[59]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_27.png
[60]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_28.png
[61]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_29.png
[100]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_203.png

