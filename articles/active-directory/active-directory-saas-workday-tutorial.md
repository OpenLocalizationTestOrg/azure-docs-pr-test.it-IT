---
title: 'Esercitazione: Integrazione di Azure Active Directory con Workday | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Workday.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e9da692e-4a65-4231-8ab3-bc9a87b10bca
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: aaa41e372e45f464c4540a70fc79c98dbc06d6b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workday"></a>Esercitazione: Integrazione di Azure Active Directory con Workday

In questa esercitazione, è illustrato come toointegrate Workday con Azure Active Directory (Azure AD).

Integrazione Workday con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooWorkday
- È possibile abilitare l'utenti tooautomatically get connesso tooWorkday (Single Sign-On) con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

integrazione di Azure AD con Workday tooconfigure, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione di Workday abilitata per l'accesso Single Sign-On

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di Workday dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-workday-from-hello-gallery"></a>Aggiunta di Workday dalla raccolta hello
integrazione hello tooconfigure di Workday in Azure AD, è necessario tooadd Workday dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd Workday dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Applicazioni][2]
    
3. tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.

    ![Applicazioni][3]

4. Nella casella di ricerca hello, digitare **Workday**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-workday-tutorial/tutorial_workday_search.png)

5. Nel riquadro dei risultati hello, selezionare **Workday**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-workday-tutorial/tutorial_workday_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Workday in base a un utente test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Workday è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Workday richiede toobe stabilita.

Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in Workday.

tooconfigure e test Azure single sign-on AD con Workday, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creazione di un utente test Workday](#creating-a-workday-test-user)**  -toohave un equivalente di Britta Simon in Workday che è la rappresentazione toohello collegato Azure AD dell'utente.
4. **[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Workday.

**Azure AD tooconfigure single sign-on con Workday, eseguire hello alla procedura seguente:**

1. Nel portale di Azure su hello hello **Workday** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Configura accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-workday-tutorial/tutorial_workday_samlbase.png)

3. In hello **Workday dominio e gli URL** seguire hello alla procedura seguente:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-workday-tutorial/tutorial_workday_url.png)

    a. In hello **Sign-on URL** casella di testo, tipo di valore hello di:`https://impl.workday.com/<tenant>/login-saml2.htmld`

    b. In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://impl.workday.com/<tenant>/login-saml.htmld`

    > [!NOTE] 
    > Questi valori non sono hello reale. Aggiornare questi valori con URL hello effettivo Sign-on e URL di risposta. L'URL di risposta deve avere un sottodominio, ad esempio www, wd2, wd3, wd3-impl, wd5, wd5-impl. Usare qualcosa come "*http://www.myworkday.com*" funziona mentre "*http://myworkday.com*" non funziona. Contatto [team di supporto Client di Workday](https://www.workday.com/en-us/partners-services/services/support.html) tooget questi valori. 
 

4. In hello **certificato di firma SAML** fare clic su **certificato (Base64)** e quindi salvare il file di certificato hello nel computer in uso.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-workday-tutorial/tutorial_workday_certificate.png) 

5. Fare clic sul pulsante **Salva** .

    ![Configura accesso Single Sign-On](./media/active-directory-saas-workday-tutorial/tutorial_general_400.png)

6. In hello **configurazione di Workday** fare clic su **configurare Workday** tooopen **Configura sign-on** finestra. Hello copia **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**

    ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-workday-tutorial/tutorial_workday_configure.png) 
<CS>
7. In una finestra del web browser, accedere come amministratore nel sito della società di tooyour Workday.

8. Andare troppo**Menu \> Workbench**.
   
    ![Workbench](./media/active-directory-saas-workday-tutorial/IC782923.png "Workbench")

9. Andare troppo**Account amministrazione**.
   
    ![Account Administration](./media/active-directory-saas-workday-tutorial/IC782924.png "Account Administration")

10. Andare troppo**Modifica configurazione Tenant-sicurezza**.
   
    ![Edit Tenant Security](./media/active-directory-saas-workday-tutorial/IC782925.png "Edit Tenant Security")

11. In hello **gli URL di reindirizzamento** seguire hello alla procedura seguente:
   
    ![Redirection URLs](./media/active-directory-saas-workday-tutorial/IC7829581.png "Redirection URLs")
   
    a. Fare clic su **Aggiungi riga**.
   
    b. In hello **Login Redirect URL** casella di testo e hello **Mobile Redirect URL** casella di testo, hello tipo **URL Sign-on** immesso in hello **Workday dominio e URL** sezione di hello portale di Azure.
   
    c. Nel portale di Azure su hello hello **Configura sign-on** finestra, hello copia **Sign-Out URL**e quindi incollarlo hello **l'URL di reindirizzamento disconnessione** casella di testo.
   
    d.  In **ambiente** casella di testo, nome del tipo hello ambiente.  

    >[!NOTE]
    > Hello valore dell'attributo di ambiente hello è associato il valore toohello hello dell'URL del tenant:  
    >-Se il nome di dominio hello di hello l'URL tenant Workday inizia con impl, ad esempio: *https://impl.workday.com/\<tenant\>/login-saml2.htmld*), hello **ambiente** attributo deve essere impostato tooImplementation.  
    >-Se il nome di dominio hello inizia con un altro elemento, è necessario toocontact [team di supporto Client di Workday](https://www.workday.com/en-us/partners-services/services/support.html) tooget hello corrispondenza **ambiente** valore.

12. In hello **SAML Setup** seguire hello alla procedura seguente:
   
    ![Configurazione SAML](./media/active-directory-saas-workday-tutorial/IC782926.png "Configurazione SAML")
   
    a.  Selezionare **Enable SAML authentication**.
   
    b.  Fare clic su **Aggiungi riga**.

13. Nella sezione relativa ai provider di identità SAML hello, eseguire hello alla procedura seguente:
   
    ![SAML Identity Providers](./media/active-directory-saas-workday-tutorial/IC7829271.png "SAML Identity Providers")
   
    a. Nella casella di testo Nome Provider di identità hello, digitare un nome di provider (ad esempio: *SPInitiatedSSO*).
   
    b. Nel portale di Azure su hello hello **Configura sign-on** finestra, hello copia **ID entità SAML** valore e quindi incollarlo hello **dell'autorità di certificazione** casella di testo.
   
    c. Selezionare **Enable Workday Initiated Logout** (Abilita disconnessione avviata da Workday).
   
    d. Nel portale di Azure su hello hello **Configura sign-on** finestra, hello copia **Sign-Out URL** valore e quindi incollarlo hello **URL richiesta di disconnessione** casella di testo.

    e. Fare clic su **Certificato di chiave pubblica del provider di identità** e quindi su **Crea**. 

    ![Creare](./media/active-directory-saas-workday-tutorial/IC782928.png "Creare")

    f. Fare clic su **Crea chiave pubblica x509**. 

    ![Creare](./media/active-directory-saas-workday-tutorial/IC782929.png "Creare")


14. In hello **View x509 Public Key** seguire hello alla procedura seguente: 
   
    ![View x509 Public Key](./media/active-directory-saas-workday-tutorial/IC782930.png "View x509 Public Key") 
   
    a. In hello **nome** casella di testo, digitare un nome per il certificato (ad esempio: *DPI\_SP*).
   
    b. In hello **valido dal** casella di testo, hello di tipo valido dal valore dell'attributo del certificato.
   
    c.  In hello **valido per** casella di testo, valore di tipo hello tooattribute valido del certificato.
   
    > [!NOTE]
    > È possibile ottenere hello valido dalla data e hello toodate valido dal certificato scaricato hello facendovi doppio clic.  le date di Hello sono elencate sotto hello **dettagli** scheda.
    > 
    >
   
    d.  Aprire il certificato con codifica base 64 nel blocco note e quindi hello copia del contenuto di esso.
   
    e.  In hello **certificato** casella di testo, incollare hello contenuto degli Appunti.
   
    f.  Fare clic su **OK**.

15. Eseguire hello alla procedura seguente: 
   
    ![SSO configuration](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguratio.png "SSO configuration")
   
    a.  Abilitare hello **x509 Private Key Pair**.
   
    b.  In hello **ID Provider di servizi** casella tipo **http://www.workday.com**.
   
    c.  Selezionare **Abilita autenticazione SAML SP initiated**.
   
    d.  Nel portale di Azure su hello hello **Configura sign-on** finestra, hello copia **SAML Single Sign-On Service URL** valore e quindi incollarlo hello **URL servizio SSO IdP** casella di testo.
   
    e. Selezionare **Do Not Deflate SP-initiated Authentication Request**.
   
    f. In **Authentication Request Signature Method** selezionare **SHA256**. 
   
    ![Authentication Request Signature Method](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguration.png "Authentication Request Signature Method") 
   
    g. Fare clic su **OK**. 
   
    ![OK](./media/active-directory-saas-workday-tutorial/IC782933.png "OK")
<CE>

> [!TIP]
> È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!  Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello. È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)
>

### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.

![Creare un utente di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-workday-tutorial/create_aaduser_01.png) 

2. elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-workday-tutorial/create_aaduser_02.png) 

3. hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-workday-tutorial/create_aaduser_03.png) 

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-workday-tutorial/create_aaduser_04.png) 

    a. In hello **nome** casella tipo **BrittaSimon**.

    b. In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Show Password** e annotare il valore di hello di hello **Password**.

    d. Fare clic su **Crea**.
 
### <a name="creating-a-workday-test-user"></a>Creazione di un utente test di Workday

tooget un utente di test, il provisioning in Workday, è necessario hello toocontact [team di supporto Client di Workday](https://www.workday.com/en-us/partners-services/services/support.html).
Hello [team di supporto Client di Workday](https://www.workday.com/en-us/partners-services/services/support.html) Crea utente hello automaticamente.

### <a name="assigning-hello-azure-ad-test-user"></a>Assegnazione utente test hello Azure AD

In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooWorkday.

![Assegna utente][200] 

**tooassign Britta Simon tooWorkday, eseguire hello alla procedura seguente:**

1. Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **Workday**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-workday-tutorial/tutorial_workday_app.png) 

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![Assegna utente][202] 

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

Se si desiderano tootest le impostazioni di single sign-on, aprire Pannello di accesso hello. Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)
* [Configura provisioning utenti](active-directory-saas-workday-inbound-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workday-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workday-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workday-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workday-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workday-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workday-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workday-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workday-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workday-tutorial/tutorial_general_203.png

