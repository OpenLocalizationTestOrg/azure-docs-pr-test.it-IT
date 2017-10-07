---
title: 'Esercitazione: Integrazione di Azure Active Directory con Salesforce Sandbox | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Salesforce Sandbox.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ee54c39e-ce20-42a4-8531-da7b5f40f57c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 7539f08356568a17ebfcee2764bbbefa129b0553
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce-sandbox"></a>Esercitazione: Integrazione di Azure Active Directory con Salesforce Sandbox

In questa esercitazione, è illustrato come toointegrate Salesforce Sandbox con Azure Active Directory (Azure AD).

Integrazione di Salesforce Sandbox con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooSalesforce Sandbox
- È possibile abilitare l'utenti tooautomatically get connesso tooSalesforce Sandbox (Single Sign-On) con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

integrazione di Azure AD con Salesforce Sandbox tooconfigure, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione di Salesforce Sandbox abilitata per l'accesso Single Sign-On

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di Salesforce Sandbox dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-salesforce-sandbox-from-hello-gallery"></a>Aggiunta di Salesforce Sandbox dalla raccolta hello
integrazione hello tooconfigure di Salesforce Sandbox in Azure AD, è necessario tooadd Salesforce Sandbox dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd Salesforce Sandbox dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Applicazioni][2]
    
3. Fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo hello.

    ![Applicazioni][3]

4. Nella casella di ricerca hello, digitare **Salesforce Sandbox**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_search.png)

5. Nel riquadro dei risultati hello, selezionare **Salesforce Sandbox**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione si configura e si testa l'accesso Single Sign-On di Azure AD con Salesforce Sandbox in base a un utente test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Salesforce Sandbox è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Salesforce Sandbox richiede toobe stabilita.

Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in Salesforce Sandbox.

tooconfigure e test Azure single sign-on AD con Salesforce Sandbox, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creazione di un utente test Salesforce Sandbox](#creating-a-salesforce-sandbox-test-user)**  -toohave un equivalente di Britta Simon in Salesforce Sandbox con rappresentazione toohello collegato Azure AD dell'utente.
4. **[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Salesforce Sandbox.

**Azure AD tooconfigure single sign-on con Salesforce Sandbox, eseguire hello alla procedura seguente:**

1. Nel portale di Azure su hello hello **Salesforce Sandbox** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Configura accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_samlbase.png)

3. In hello **URL e dominio di Salesforce Sandbox** seguire hello alla procedura seguente:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_url.png)

     In hello **Sign-on URL** casella di testo, valore di tipo hello utilizzando hello modello:`https://<subdomain>.my.salesforce.com`

    > [!NOTE] 
    > Questo valore non è hello reale. Aggiornare questo valore con URL hello effettivo Sign-on. Contatto [team di supporto Client di Sandbox Salesforce](https://help.salesforce.com/support) tooget questo valore.


4. Se già stato configurato single sign-on per un'altra istanza di Salesforce Sandbox nella directory, quindi è necessario configurare anche hello **identificatore** toohave hello stesso valore di hello **URL di accesso**. 
    
    >[!Note]
    >Hello **identificatore** trovato controllando hello **Mostra impostazioni avanzate** casella di controllo hello **Configura URL App** pagina della finestra di dialogo hello 


5. In hello **certificato di firma SAML** fare clic su **certificato** e quindi salvare il file di certificato hello nel computer in uso.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_certificate.png) 

6. Fare clic sul pulsante **Salva** .

    ![Configura accesso Single Sign-On](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_400.png)

7. In hello **Salesforce Sandbox configurazione** fare clic su **configurare Salesforce Sandbox** tooopen **Configura sign-on** finestra. Hello copia **ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**

    ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_configure.png) 
<CS>
8. Aprire una nuova scheda nel browser e accedere tooyour account amministratore Salesforce Sandbox.

9. Scegliere dal menu hello in primo piano hello **installazione**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-salesforcesandbox-tutorial/IC781024.png)
10. Nel riquadro di spostamento hello hello sinistra, fare clic su **controlli di sicurezza**, quindi fare clic su **Single Sign-On Settings**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-salesforcesandbox-tutorial/IC781025.png)
11. Nella sezione Impostazioni di Single Sign-On hello, eseguire hello alla procedura seguente: ![configurare Single Sign-On](./media/active-directory-saas-salesforcesandbox-tutorial/IC781026.png)
     
     a.  Selezionare **Abilitato SAML**. 

     b.  Fare clic su **New**.

12. Nella sezione SAML Single Sign-On Settings hello, eseguire hello alla procedura seguente:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-salesforcesandbox-tutorial/IC781027.png)

    casella di testo Nome hello a.In, nome della configurazione hello hello del tipo (ad esempio: *SPSSOWAAD\_Test*). 

    b. Incolla **ID entità SMAL** valore in hello **dell'autorità di certificazione** casella di testo.

    c. In hello **Id entità** casella tipo **https://test.salesforce.com** se hello prima istanza di Salesforce Sandbox, che si sta aggiungendo tooyour directory. Se esiste già un'istanza di Salesforce Sandbox, quindi per hello **ID entità** tipo di hello **URL di accesso**, che deve essere nel formato seguente:`http://company.my.salesforce.com`  
 
    d. Fare clic su **Sfoglia** hello tooupload scaricato certificato.  

    e. Come **tipo di identità SAML**selezionare **l'asserzione contiene l'ID di federazione di hello dall'oggetto utente hello**.
 
    f. Come **SAML Identity Location**selezionare **identità si trova nell'elemento NameIdentifier hello di hello Subject statement**.

    g. Incolla **URL servizio Single Sign-On** in hello **Identity Provider Login URL** casella di testo. 

    h. SFDC non supporta la disconnessione SAML.  In alternativa, incollare 'https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0' in hello **Identity Provider Logout URL** casella di testo.

    i. In **Service Provider Initiated Request Binding** (Binding richiesta avviato dal provider di servizi) selezionare **HTTP POST**. 

    j. Fare clic su **Salva**.

### <a name="enable-your-domain"></a>Abilitare il dominio
In questa sezione si presuppone che sia già stato creato un dominio.  Per altre informazioni, vedere [Definizione del nome di dominio](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).

**tooenable il dominio, eseguire hello alla procedura seguente:**

1. Nel riquadro di spostamento a sinistra di hello, fare clic su **Gestione dominio**, quindi fare clic su **risorse del dominio.**
   
     ![Configura accesso Single Sign-On](./media/active-directory-saas-salesforcesandbox-tutorial/IC781029.png)
   
   >[!NOTE]
   >Assicurarsi che il dominio sia stato configurato correttamente. 

2. In hello **Login Page Settings** fare clic su **modifica**, quindi, come **servizio di autenticazione**, selezionare il nome di hello di hello impostazione SAML Single Sign-On da hello precedente sezione e infine fare clic su **salvare**.
   
   ![Configura accesso Single Sign-On](./media/active-directory-saas-salesforcesandbox-tutorial/IC781030.png)

Non appena si dispone di un dominio configurato, gli utenti devono usare Salesforce sandbox di hello dominio URL toologin toohello.  

valore di hello tooget dell'URL di hello, selezionare il profilo SSO hello creato nella sezione precedente hello.    

> [!TIP]
> È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!  Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello. È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)


### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.

![Creare un utente di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_01.png) 

2. elenco di hello toodisplay utenti andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_02.png) 

3. Nella parte superiore di hello della finestra di dialogo hello, fare clic su **Aggiungi** tooopen hello **utente** finestra di dialogo.
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_03.png) 

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_04.png) 

    a. In hello **nome** casella tipo **BrittaSimon**.

    b. In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Show Password** e annotare il valore di hello di hello **Password**.

    d. Fare clic su **Crea**.
 
### <a name="creating-a-salesforce-sandbox-test-user"></a>Creazione di un utente test di Salesforce Sandbox

In questa sezione si crea un utente di nome Britta Simon in Salesforce Sandbox. Salesforce Sandbox supporta il provisioning JIT (Just-In-Time) che è abilitato per impostazione predefinita.
Non è necessario alcun intervento dell'utente in questa sezione. Se un utente non esiste già nell'ambiente Salesforce Sandbox, viene creato uno nuovo quando si tenta di tooaccess Salesforce Sandbox.

### <a name="assigning-hello-azure-ad-test-user"></a>Assegnazione utente test hello Azure AD

In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooSalesforce Sandbox.

![Assegna utente][200] 

**tooassign Britta Simon tooSalesforce Sandbox, eseguire hello alla procedura seguente:**

1. Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **Salesforce Sandbox**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_app.png) 

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![Assegna utente][202] 

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

Se si desiderano tootest le impostazioni SSO, aprire Pannello di accesso hello. Per ulteriori dettagli su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)
* [Configura provisioning utenti](active-directory-saas-salesforce-sandbox-provisioning-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_203.png

