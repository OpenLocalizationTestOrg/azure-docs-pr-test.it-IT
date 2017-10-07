---
title: 'Esercitazione: Integrazione di Azure Active Directory con Kantega SSO for Confluence | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Kantega SSO per confluenza.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d0d99c14-a6ca-45f2-bb84-633126095e7a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: b35eb8757e41e86228a3a9ee10869086cc801c9b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kantega-sso-for-confluence"></a>Esercitazione: Integrazione di Azure Active Directory con Kantega SSO for Confluence

In questa esercitazione, è illustrato come toointegrate Kantega SSO per confluenza con Azure Active Directory (Azure AD).

Kantega SSO per la confluenza di integrazione con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooKantega SSO per confluenza
- È possibile abilitare l'utenti tooautomatically get connesso tooKantega SSO per confluenza (Single Sign-On) con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

integrazione di Azure AD con Kantega SSO per confluenza tooconfigure, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione di Kantega SSO for Confluence abilitata per l'accesso Single Sign-On

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di Kantega SSO per confluenza dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-kantega-sso-for-confluence-from-hello-gallery"></a>Aggiunta di Kantega SSO per confluenza dalla raccolta hello
integrazione di hello tooconfigure di Kantega SSO per confluenza in Azure AD, è necessario tooadd Kantega SSO per confluenza dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd Kantega SSO per confluenza dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Applicazioni][2]
    
3. tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.

    ![Applicazioni][3]

4. Nella casella di ricerca hello, digitare **Kantega SSO per confluenza**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_kantegassoforconfluence_search.png)

5. Nel riquadro dei risultati hello, selezionare **Kantega SSO per confluenza**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_kantegassoforconfluence_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Kantega SSO for Confluence mediante un utente test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Kantega SSO per confluenza è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure AD e l'utente correlato di hello in Kantega SSO per confluenza deve toobe stabilita.

In Kantega SSO per confluenza, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.

tooconfigure e prova AD Azure single sign-on con Kantega SSO per confluenza, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creazione di un SSO Kantega per utente test confluenza](#creating-a-kantega-sso-for-confluence-test-user)**  -toohave un equivalente di Britta Simon Kantega SSO per la confluenza di rappresentazione toohello collegato Azure AD dell'utente.
4. **[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on in SSO il Kantega per applicazione confluenza.

**tooconfigure AD Azure single sign-on con Kantega SSO per confluenza, eseguire hello alla procedura seguente:**

1. Nel portale di Azure su hello hello **Kantega SSO per confluenza** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Configura accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_kantegassoforconfluence_samlbase.png)

3. In **IDP** avviato modalità, hello **Kantega SSO per confluenza dominio e gli URL** sezione eseguire hello seguente passaggio:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_kantegassoforconfluence_url1.png)

    a. In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`

    b. In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`

4. In **SP** modalità avviata, controllo **Mostra URL impostazioni avanzate** ed eseguire hello seguente passaggio:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_kantegassoforconfluence_url2.png)

    In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`

    > [!NOTE] 
    > Poiché questi non sono i valori reali, Aggiornare questi valori con hello effettivo identificatore, l'URL di risposta e URL Sign-On. Questi valori vengono ricevuti durante la configurazione del plug-in confluenza, illustrato più avanti nell'esercitazione di hello hello.

5. In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_kantegassoforconfluence_certificate.png) 

6. Fare clic sul pulsante **Salva** .

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_general_400.png)
    
7. In una finestra del web browser, accedere tooyour **portale di amministrazione confluenza** come amministratore.

8. Passare il mouse su ruota dentata e scegliere hello **componenti aggiuntivi**.
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon1.png)

9. Nella scheda **ATLASSIAN MARKETPLACE** (MARKETPLACE DI ATLASSIAN) fare clic su **Find new add-ons** (Trova nuovi componenti aggiuntivi). 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon.png)

10. Ricerca **Kantega SSO per Kerberos SAML confluenza** e fare clic su **installare** tooinstall pulsante hello nuovo plug-in SAML.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon2.png)

11. verrà avviata l'installazione di plug-in di Hello.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon3.png)

12. Al termine dell'installazione di hello. Fare clic su **Close**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon33.png)

13. Fare clic su **Manage**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon34.png)
    
14. Fare clic su **configura** tooconfigure hello nuovo plug-in.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon35.png)

15. Questo nuovo plug-in è disponibile anche nella scheda**USERS & SECURITY** (UTENTI E SICUREZZA).

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon36.png)
    
16. In hello **SAML** sezione. Selezionare **Azure Active Directory (Azure AD)** da hello **Aggiungi provider di identità** elenco a discesa.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon4.png)

17. Selezionare il livello di sottoscrizione **Basic** (Di base).

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon5.png)       

18. In hello **proprietà App** sezione, eseguire la procedura seguente: 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon6.png)

    a. Hello copia **URI ID App** valore e utilizzarlo come **URL Sign-On, l'URL di risposta e identificatore** su hello **Kantega SSO per confluenza dominio e gli URL** sezione nel portale di Azure.

    b. Fare clic su **Avanti**.

19. In hello **importazione dei metadati** sezione, eseguire la procedura seguente: 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon7.png)

    a. Selezionare **Metadata file on my computer** (File metadati in questo computer) e caricare il file di metadati scaricato dal portale di Azure.

    b. Fare clic su **Avanti**.

20. In hello **nome e SSO percorso** sezione, eseguire la procedura seguente:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon8.png)
    
    a. Aggiungi nome del Provider di identità hello in **nome provider di identità** casella di testo (ad esempio, Azure AD).

    b. Fare clic su **Avanti**.

21. Verificare il certificato di firma hello e fare clic su **Avanti**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon9.png)

22. In hello **gli account utente confluenza** sezione, eseguire la procedura seguente:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon10.png)

    a. Selezionare **creare gli utenti nella Directory interna del confluenza eventualmente** e immettere il nome appropriato del gruppo di hello hello per gli utenti (può essere più no. gruppi separati da virgola).

    b. Fare clic su **Avanti**.

23. Fare clic su **Fine**.   

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon11.png)

24. In hello **noto domini per Azure AD** sezione, eseguire la procedura seguente: 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon12.png)

    a. Selezionare **noto domini** dal riquadro sinistro di hello della pagina hello.

    b. Immettere un nome di dominio in hello **noto domini** casella di testo.

    c. Fare clic su **Salva**. 

> [!TIP]
> È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!  Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello. È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.

![Creare un utente di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kantegassoforconfluence-tutorial/create_aaduser_01.png) 

2. elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kantegassoforconfluence-tutorial/create_aaduser_02.png) 

3. hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kantegassoforconfluence-tutorial/create_aaduser_03.png) 

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kantegassoforconfluence-tutorial/create_aaduser_04.png) 

    a. In hello **nome** casella tipo **BrittaSimon**.

    b. In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Show Password** e annotare il valore di hello di hello **Password**.

    d. Fare clic su **Crea**.
 
### <a name="creating-a-kantega-sso-for-confluence-test-user"></a>Creazione di un utente test di Kantega SSO for Confluence

toolog agli utenti di Azure AD tooenable in tooConfluence, è necessario eseguirne il provisioning in confluenza. In caso di hello Kantega SSO per confluenza, il provisioning è un'attività manuale.

**tooprovision un account utente, eseguire hello alla procedura seguente:**

1. Accedere come amministratore tooyour Kantega SSO per il sito della società confluenza.

2. Passare il mouse su ruota dentata e scegliere hello **Gestione utenti**.

    ![Aggiungere un dipendente](./media/active-directory-saas-kantegassoforconfluence-tutorial/user1.png) 

3. Nella sezione Users (Utenti) fare clic sula scheda **Add users** (Aggiungi utenti). In hello **"Aggiungi utente"** finestra di dialogo eseguire hello alla procedura seguente:

    ![Aggiungere un dipendente](./media/active-directory-saas-kantegassoforconfluence-tutorial/user2.png) 

    a. In hello **Username** casella Tipo hello email dell'utente come Brittasimon@contoso.com.

    b. In hello **nome completo** casella di testo, nome completo del tipo hello dell'utente come Britta Simon.

    c. In hello **posta elettronica** casella di testo, digitare hello di indirizzo di posta elettronica dell'utente come Brittasimon@contoso.com.

    d. In hello **Password** casella di testo, digitare la password per l'utente hello.

    e. Fare clic su **Conferma Password** digitare nuovamente la password di hello.
    
    f. Fare clic sul pulsante **Aggiungi**.

### <a name="assigning-hello-azure-ad-test-user"></a>Assegnazione utente test hello Azure AD

In questa sezione per abilitare Britta Simon toouse single sign-on Azure tooKantega accesso SSO per la confluenza di concessione.

![Assegna utente][200] 

**tooassign Britta Simon tooKantega SSO per confluenza, eseguire hello alla procedura seguente:**

1. Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **Kantega SSO per confluenza**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_kantegassoforconfluence_app.png) 

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![Assegna utente][202] 

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.

Quando si fa clic hello Kantega SSO riquadro confluenza in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour Kantega SSO per applicazione confluenza.
Per ulteriori informazioni sul pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_general_203.png

