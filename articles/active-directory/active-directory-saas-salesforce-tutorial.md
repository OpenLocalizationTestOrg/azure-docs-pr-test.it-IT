---
title: 'Esercitazione: Integrazione di Azure Active Directory con Salesforce | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Salesforce.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2d7d420-dc91-41b8-a6b3-59579e043b35
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 1d848518ee30910e051cdc4746c599219f3b5a3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce"></a>Esercitazione: Integrazione di Azure Active Directory con Salesforce

In questa esercitazione, è illustrato come toointegrate Salesforce con Azure Active Directory (Azure AD).

Integrazione di Salesforce con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooSalesforce
- È possibile abilitare l'utenti tooautomatically get connesso tooSalesforce (Single Sign-On) con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

integrazione di Azure AD con Salesforce tooconfigure, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione di Salesforce abilitata per l'accesso Single Sign-On

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di Salesforce da raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-salesforce-from-hello-gallery"></a>Aggiunta di Salesforce da raccolta hello
integrazione hello tooconfigure di Salesforce in Azure AD, è necessario tooadd Salesforce dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd Salesforce dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Applicazioni][2]
    
3. Fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo hello.

    ![Applicazioni][3]

4. Nella casella di ricerca hello, digitare **Salesforce**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_search.png)

5. Nel riquadro dei risultati hello, selezionare **Salesforce**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Salesforce in base a un utente test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Salesforce è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Salesforce richiede toobe stabilita.

Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in Salesforce.

tooconfigure e test Azure single sign-on AD con Salesforce, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creazione di un utente test Salesforce](#creating-a-salesforce-test-user)**  -toohave un equivalente di Britta Simon in Salesforce che è la rappresentazione toohello collegato Azure AD dell'utente.
4. **[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Salesforce.

**Azure AD tooconfigure single sign-on con Salesforce, eseguire hello alla procedura seguente:**

1. Nel portale di Azure su hello hello **Salesforce** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Configura accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_samlbase.png)

3. In hello **URL e il dominio di Salesforce** seguire hello alla procedura seguente:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_url.png)

    In hello **Sign-on URL** casella di testo, valore di tipo hello utilizzando hello modello: 
   * Account aziendale: `https://<subdomain>.my.salesforce.com`
   * Account sviluppatore: `https://<subdomain>-dev-ed.my.salesforce.com`

    > [!NOTE] 
    > Questi valori non sono hello reale. Aggiornare questi valori con URL hello effettivo Sign-on. Contatto [team di supporto Client di Salesforce](https://help.salesforce.com/support) tooget questi valori. 
 
4. In hello **certificato di firma SAML** fare clic su **certificato** e quindi salvare il file di certificato hello nel computer in uso.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_certificate.png) 

5. Fare clic sul pulsante **Salva** .

    ![Configura accesso Single Sign-On](./media/active-directory-saas-salesforce-tutorial/tutorial_general_400.png)

6. In hello **configurazione Salesforce** fare clic su **configurare Salesforce** tooopen **Configura sign-on** finestra. Hello copia **ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.** 

    ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_configure.png) 
<CS>
7.  Aprire una nuova scheda nel browser e accedere tooyour account amministratore Salesforce.

8.  In hello **amministratore** riquadro di spostamento, fare clic su **controlli di sicurezza** tooexpand hello correlati sezione. Fare quindi clic su **Single Sign-On Settings**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso.png)

9.  In hello **Single Sign-On Settings** pagina, fare clic su hello **modifica** pulsante.
    ![Configura accesso Single Sign-On](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso-edit.png)

      > [!NOTE]
      > Se si è grado tooenable Single Sign-On le impostazioni per l'account di Salesforce, potrebbe essere necessario toocontact [team di supporto Client di Salesforce](https://help.salesforce.com/support). 

10. Selezionare **SAML Enabled**, quindi fare clic su **Save**.

      ![Configura accesso Single Sign-On](./media/active-directory-saas-salesforce-tutorial/sf-enable-saml.png)
11. Fare clic su SAML single sign-on impostazioni, tooconfigure **New**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso-new.png)

12. In hello **SAML Single Sign-On Setting Edit** pagina, assicurarsi di hello seguenti configurazioni:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-salesforce-tutorial/sf-saml-config.png)

    a. Per hello **nome** , digitare un nome descrittivo per questa configurazione. Fornisce un valore per **nome** popolare automaticamente hello **nome API** casella di testo.

    b. Incolla **ID entità SMAL** valore in hello **dell'autorità di certificazione** campo Salesforce.

    c. In hello **Id entità textbox**, digitare il nome di dominio di Salesforce utilizzando hello seguente motivo:
      
      * Account aziendale: `https://<subdomain>.my.salesforce.com`
      * Account sviluppatore: `https://<subdomain>-dev-ed.my.salesforce.com`
      
    d. Fare clic su **Sfoglia** o **Scegli File** tooopen hello **tooUpload Scegli File** finestra di dialogo, selezionare il certificato Salesforce e quindi fare clic su **aprire**certificato hello tooupload.

    e. In **SAML Identity Type** selezionare **Assertion contains User's salesforce.com username**.

    f. Per **SAML Identity Location**selezionare **identità si trova nell'elemento NameIdentifier hello di hello istruzione dell'oggetto**

    g. Incolla **URL servizio Single Sign-On** in hello **Identity Provider Login URL** campo Salesforce.
    
    h. Per **Service Provider Initiated Request Binding** selezionare **HTTP Redirect**.
    
    i. Infine, fare clic su **salvare** tooapply SAML single sign-on impostazioni.

13. Nel riquadro di spostamento a sinistra hello in Salesforce, fare clic su **Gestione dominio** tooexpand hello sezione correlata e quindi fare clic su **My Domain**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-salesforce-tutorial/sf-my-domain.png)

14. Scorrere verso il basso toohello **configurazione dell'autenticazione** sezione e fare clic su hello **modifica** pulsante.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-salesforce-tutorial/sf-edit-auth-config.png)

15. In hello **servizio di autenticazione** sezione, selezionare il nome descrittivo della configurazione SSO SAML hello e quindi fare clic su **salvare**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-salesforce-tutorial/sf-auth-config.png)

    > [!NOTE]
    > Se più di un servizio di autenticazione è selezionato, gli utenti sono richieste tooselect quale servizio di autenticazione che desiderano toosign con durante l'avvio di single sign-on tooyour Salesforce ambiente. Se non si desidera che toohappen, quindi è necessario **lasciare deselezionata tutti gli altri servizi di autenticazione**.
<CE>    
> [!TIP]
> È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!  Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello. È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)


### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.

![Creare un utente di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. Nel riquadro di spostamento a sinistra di hello hello **portale di Azure**, fare clic su **Azure Active Directory** icona.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-salesforce-tutorial/create_aaduser_01.png) 

2. elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-salesforce-tutorial/create_aaduser_02.png) 

3. Nella parte superiore di hello della finestra di dialogo hello, fare clic su **Aggiungi** tooopen hello **utente** finestra di dialogo.
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-salesforce-tutorial/create_aaduser_03.png) 

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-salesforce-tutorial/create_aaduser_04.png) 

    a. In hello **nome** casella tipo **BrittaSimon**.

    b. In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Show Password** e annotare il valore di hello di hello **Password**.

    d. Fare clic su **Crea**.
 
### <a name="creating-a-salesforce-test-user"></a>Creazione di un utente test di Salesforce

In questa sezione si crea un utente di nome Britta Simon in Salesforce. Salesforce supporta il provisioning JIT (Just-In-Time) che è abilitato per impostazione predefinita.
Non è necessario alcun intervento dell'utente in questa sezione. Se un utente non esiste già in Salesforce, viene creato uno nuovo quando si tenta di tooaccess Salesforce.

### <a name="assigning-hello-azure-ad-test-user"></a>Assegnazione utente test hello Azure AD

In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooSalesforce.

![Assegna utente][200] 

**tooassign Britta Simon tooSalesforce, eseguire hello alla procedura seguente:**

1. Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **Salesforce**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_app.png) 

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![Assegna utente][202] 

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

tootest le impostazioni single sign-on, aprire il pannello di accesso a hello [https://myapps.microsoft.com](https://myapps.microsoft.com/), quindi accedere all'account di prova hello e fare clic su **Salesforce**.

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)
* [Configura provisioning utenti](active-directory-saas-salesforce-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_203.png

