---
title: 'Esercitazione: Integrazione di Azure Active Directory con Kantega SSO for FishEye/Crucible | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Kantega SSO per FishEye/crogiolo.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9fe951fd-1530-4d33-a1a4-390385b99ce9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: fdd68b5e90c3e2893887650735429a33e21ffa68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kantega-sso-for-fisheyecrucible"></a>Esercitazione: Integrazione di Azure Active Directory con Kantega SSO for FishEye/Crucible

In questa esercitazione, è illustrato come toointegrate Kantega SSO per FishEye/crogiolo con Azure Active Directory (Azure AD).

Integrazione Kantega SSO per FishEye/crogiolo con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooKantega SSO per FishEye/crogiolo
- È possibile abilitare l'utenti tooautomatically get connesso tooKantega SSO per FishEye/crogiolo (Single Sign-On) con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

integrazione di Azure AD con Kantega SSO per FishEye/crogiolo tooconfigure, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione di Kantega SSO for FishEye/Crucible abilitata per l'accesso Single Sign-On

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di Kantega SSO per FishEye/crogiolo dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-kantega-sso-for-fisheyecrucible-from-hello-gallery"></a>Aggiunta di Kantega SSO per FishEye/crogiolo dalla raccolta hello
integrazione hello tooconfigure di Kantega SSO per FishEye/crogiolo in Azure AD, è necessario tooadd Kantega SSO per FishEye/crogiolo dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd Kantega SSO per FishEye/crogiolo dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Applicazioni][2]
    
3. tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.

    ![Applicazioni][3]

4. Nella casella di ricerca hello, digitare **Kantega SSO per FishEye/crogiolo**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_search.png)

5. Nel riquadro dei risultati hello, selezionare **Kantega SSO per FishEye/crogiolo**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Kantega SSO for FishEye/Crucible mediante un utente test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Kantega SSO per FishEye/crogiolo è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure AD e l'utente correlato di hello in Kantega SSO per FishEye/crogiolo deve toobe stabilita.

In Kantega SSO per FishEye/crogiolo, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.

tooconfigure e test Azure AD single sign-on con Kantega SSO per FishEye/crogiolo, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creazione di un SSO Kantega per utente test FishEye/crogiolo](#creating-a-kantega-sso-for-fisheyecrucible-test-user)**  -toohave un equivalente di Britta Simon Kantega SSO per FishEye/crogiolo che è la rappresentazione toohello collegato Azure AD dell'utente.
4. **[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare single sign-on in SSO il Kantega per applicazione FishEye/crogiolo.

**tooconfigure AD Azure single sign-on con Kantega SSO per FishEye/crogiolo, eseguire hello alla procedura seguente:**

1. Nel portale di Azure su hello hello **Kantega SSO per FishEye/crogiolo** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Configura accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_samlbase.png)

3. In **IDP** avviato modalità, hello **Kantega SSO per dominio FishEye/crogiolo e gli URL** sezione eseguire hello seguente passaggio:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_url1.png)

    a. In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`

    b. In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`

4. In **SP** modalità avviata, controllo **Mostra URL impostazioni avanzate** ed eseguire hello seguente passaggio:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_url2.png)

    In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`
     
    > [!NOTE] 
    > Poiché questi non sono i valori reali, Aggiornare questi valori con hello effettivo identificatore, l'URL di risposta e URL Sign-On. Questi valori vengono ricevuti durante la configurazione del plug-in FishEye/crogiolo illustrato più avanti nell'esercitazione di hello hello.

5. In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_certificate.png) 

6. Fare clic sul pulsante **Salva** .

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_400.png)
    
7. In una finestra del web browser, accedere tooyour FishEye/crogiolo nel server locale come amministratore.

8. Passare il mouse su ruota dentata e scegliere hello **componenti aggiuntivi**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon1.png)

9. Nella sezione System Settings (Impostazioni di sistema) fare clic su **Find new add-ons** (Trova nuovi componenti aggiuntivi). 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/add-on2.png)

10. Ricerca **Kantega SSO per crogiolo** e fare clic su **installare** tooinstall pulsante hello nuovo plug-in SAML.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon2.png)

11. verrà avviata l'installazione di plug-in di Hello. 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon33.png)

12. Al termine dell'installazione di hello. Fare clic su **Close**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon34.png)

13. Fare clic su **Manage**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon35.png)

14. Fare clic su **configura** tooconfigure hello nuovo plug-in.  

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon3.png)

15. In hello **SAML** sezione. Selezionare **Azure Active Directory (Azure AD)** da hello **Aggiungi provider di identità** elenco a discesa.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon4.png)

16. Selezionare il livello di sottoscrizione **Basic** (Di base).

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon5.png)

17. In hello **proprietà App** sezione, eseguire la procedura seguente:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon6.png)

    a. Hello copia **URI ID App** valore e utilizzarlo come **URL Sign-On, l'URL di risposta e identificatore** su hello **Kantega SSO per dominio FishEye/crogiolo e gli URL** sezione nel portale di Azure.

    b. Fare clic su **Avanti**.

18. In hello **importazione dei metadati** sezione, eseguire la procedura seguente:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon7.png)

    a. Selezionare **Metadata file on my computer** (File metadati in questo computer) e caricare il file di metadati scaricato dal portale di Azure.

    b. Fare clic su **Avanti**.

19. In hello **nome e SSO percorso** sezione, eseguire la procedura seguente:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon8.png)

    a. Aggiungi nome del Provider di identità hello in **nome provider di identità** casella di testo (ad esempio, Azure AD).

    b. Fare clic su **Avanti**.

20. Verificare il certificato di firma hello e fare clic su **Avanti**.    

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon9.png)

21. In hello **gli account utente FishEye** sezione, eseguire la procedura seguente:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon10.png)

    a. Selezionare **creare gli utenti nella Directory interna del FishEye eventualmente** e immettere il nome appropriato del gruppo di hello hello per gli utenti (può essere più no. gruppi separati da virgola).

    b. Fare clic su **Avanti**.

22. Fare clic su **Fine**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon11.png)

23. In hello **noto domini per Azure AD** sezione, eseguire la procedura seguente:   

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon12.png)

    a. Selezionare **noto domini** dal riquadro sinistro di hello della pagina hello.

    b. Immettere un nome di dominio in hello **noto domini** casella di testo.

    c. Fare clic su **Salva**.  

> [!TIP]
> È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!  Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello. È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.

![Creare un utente di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/create_aaduser_01.png) 

2. elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/create_aaduser_02.png) 

3. hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/create_aaduser_03.png) 

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/create_aaduser_04.png) 

    a. In hello **nome** casella tipo **BrittaSimon**.

    b. In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Show Password** e annotare il valore di hello di hello **Password**.

    d. Fare clic su **Crea**.
 
### <a name="creating-a-kantega-sso-for-fisheyecrucible-test-user"></a>Creazione di un utente test di Kantega SSO for FishEye/Crucible

toolog agli utenti di Azure AD tooenable in tooFishEye/crogiolo, è necessario eseguirne il provisioning in FishEye/crogiolo. In Kantega SSO for FishEye/Crucible il provisioning è un'attività manuale.

**tooprovision un account utente, eseguire hello alla procedura seguente:**

1. Accedere come amministratore tooyour crogiolo nel server locale.

2. Passare il mouse su ruota dentata e scegliere hello **utenti**.

    ![Aggiungere un dipendente](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/user1.png) 

3. Nella scheda **Users** (Utenti) fare clic su **Add user** (Aggiungi utente).

    ![Aggiungere un dipendente](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/user2.png)

4. In hello **Add New User** finestra di dialogo eseguire hello alla procedura seguente:

    ![Aggiungere un dipendente](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/user3.png) 

    a. In hello **Username** casella Tipo hello email dell'utente come Brittasimon@contoso.com.
    
    b. In hello **nome visualizzato** casella di testo Nome visualizzato del tipo di utente hello come Britta Simon.
    
    c. In hello **indirizzo di posta elettronica** casella di testo, digitare hello di indirizzo di posta elettronica dell'utente come Brittasimon@contoso.com.

    d. In hello **Password** casella di testo, digitare la password dell'utente hello.  

    e. In hello **Conferma Password** casella di testo, hello immettere nuovamente la password dell'utente.

    f. Fare clic su **Aggiungi**.   

### <a name="assigning-hello-azure-ad-test-user"></a>Assegnazione utente test hello Azure AD

In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooKantega SSO per FishEye/crogiolo.

![Assegna utente][200] 

**tooassign Britta Simon tooKantega SSO per FishEye/crogiolo, eseguire hello alla procedura seguente:**

1. Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **Kantega SSO per FishEye/crogiolo**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_app.png) 

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![Assegna utente][202] 

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.

Quando si fa clic hello Kantega SSO riquadro FishEye/crogiolo in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour Kantega SSO per applicazione FishEye/crogiolo.
Per ulteriori informazioni sul pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_203.png

