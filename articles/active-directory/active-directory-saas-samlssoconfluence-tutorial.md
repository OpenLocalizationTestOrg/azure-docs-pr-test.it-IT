---
title: 'Esercitazione: integrazione di Azure Active Directory con SAML SSO for Confluence di resolution GmbH | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e SAML SSO per confluenza dalla risoluzione GmbH.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6b47d483-d3a3-442d-b123-171e3f0f7486
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: jeedes
ms.openlocfilehash: fe50636709857ec49023e24bdc8c6cd8c58e3c7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-saml-sso-for-confluence-by-resolution-gmbh"></a>Esercitazione: integrazione di Azure Active Directory con SAML SSO for Confluence di resolution GmbH

In questa esercitazione, è illustrato come toointegrate SAML SSO per confluenza dalla risoluzione GmbH con Azure Active Directory (Azure AD).

L'integrazione di SAML SSO per confluenza dalla risoluzione GmbH con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooSAML SSO per confluenza dalla risoluzione GmbH
- È possibile abilitare l'utenti tooautomatically get connesso tooSAML SSO per confluenza dalla risoluzione GmbH (Single Sign-On) con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

integrazione di Azure AD con SAML SSO per confluenza dalla risoluzione GmbH tooconfigure, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Una sottoscrizione attiva del Single Sign-On di SAML SSO for Confluence di resolution GmbH

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di SAML SSO per confluenza dalla risoluzione GmbH dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-saml-sso-for-confluence-by-resolution-gmbh-from-hello-gallery"></a>Aggiunta di SAML SSO per confluenza dalla risoluzione GmbH dalla raccolta hello

tooconfigure hello integrazione di SAML SSO per confluenza dalla risoluzione GmbH in Azure AD, è necessario tooadd SAML SSO per confluenza dalla risoluzione GmbH dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd SAML SSO per confluenza dalla risoluzione GmbH dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Applicazioni][2]
    
3. tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.

    ![Applicazioni][3]

4. Nella casella di ricerca hello, digitare **SAML SSO per confluenza dalla risoluzione GmbH**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_search.png)

5. Nel riquadro dei risultati hello, selezionare **SAML SSO per confluenza dalla risoluzione GmbH**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD

In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con SAML SSO for Confluence di resolution GmbH con un utente test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in SAML SSO per confluenza dalla risoluzione GmbH è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure AD e l'utente correlato hello in SAML SSO per confluenza dalla risoluzione GmbH deve toobe stabilita.

SAML SSO per confluenza dalla risoluzione GmbH, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.

tooconfigure ed eseguire test AD Azure single sign-on con SAML SSO per confluenza dalla risoluzione GmbH, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creazione di un SAML SSO per confluenza dall'utente di prova di risoluzione GmbH](#creating-a-saml-sso-for-confluence-by-resolution-gmbh-test-user)**  -toohave un equivalente di Britta Simon SAML SSO per confluenza dalla risoluzione GmbH che è la rappresentazione toohello collegato Azure AD dell'utente.
4. **[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare single sign-on nel SAML SSO per confluenza dalla risoluzione GmbH applicazione.

**tooconfigure AD Azure single sign-on con SAML SSO per confluenza dalla risoluzione GmbH, eseguire hello alla procedura seguente:**

1. Nel portale di Azure su hello hello **SAML SSO per confluenza dalla risoluzione GmbH** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Configura accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_samlbase.png)

3. In hello **SAML SSO per confluenza dalla risoluzione GmbH dominio e gli URL** sezione, se si desidera in un'applicazione hello tooconfigure **IDP** modalità iniziata da:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_url_1.png)

    a. In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<server-base-url>/plugins/servlet/samlsso`

    b. In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<server-base-url>/plugins/servlet/samlsso`

4. Selezionare **Mostra impostazioni URL avanzate** Se si desidera in un'applicazione hello tooconfigure **SP** modalità iniziata da:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_url_2.png)

    In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<server-base-url>/plugins/servlet/samlsso`
     
    > [!NOTE] 
    > Poiché questi non sono i valori reali, Aggiornare questi valori con hello effettivo identificatore, l'URL di risposta e URL Sign-On. Contatto [team di supporto SAML SSO per confluenza dalla risoluzione GmbH Client](https://www.resolution.de/go/support) tooget questi valori. 

5. In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_certificate.png) 

6. Fare clic sul pulsante **Salva** .

    ![Configura accesso Single Sign-On](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_400.png)  
    
7. In una finestra del web browser, accedere tooyour **SAML SSO per confluenza dal portale di amministrazione di risoluzione GmbH** come amministratore.

8. Passare il mouse su ruota dentata e scegliere hello **componenti aggiuntivi**.
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-samlssoconfluence-tutorial/addon1.png)

9. Si è reindirizzato tooAdministrator pagina di accesso. Immettere la password di hello e fare clic su **conferma** pulsante.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-samlssoconfluence-tutorial/addon2.png)

10. Nella scheda **ATLASSIAN MARKETPLACE** (MARKETPLACE DI ATLASSIAN) fare clic su **Find new add-ons** (Trova nuovi componenti aggiuntivi). 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-samlssoconfluence-tutorial/addon.png)

11. Ricerca **SAML Single Sign On (SSO) per la confluenza** e fare clic su **installare** tooinstall pulsante hello nuovo plug-in SAML.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-samlssoconfluence-tutorial/addon7.png)

12. verrà avviata l'installazione di plug-in di Hello. Fare clic su **Close**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-samlssoconfluence-tutorial/addon8.png)

    ![Configura accesso Single Sign-On](./media/active-directory-saas-samlssoconfluence-tutorial/addon9.png)

13. Fare clic su **Manage**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-samlssoconfluence-tutorial/addon10.png)
    
14. Fare clic su **configura** tooconfigure hello nuovo plug-in.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-samlssoconfluence-tutorial/addon11.png)

15. Questo nuovo plug-in è disponibile anche nella scheda**USERS & SECURITY** (UTENTI E SICUREZZA).

    ![Configura accesso Single Sign-On](./media/active-directory-saas-samlssoconfluence-tutorial/addon3.png)
    
16. In **SAML SingleSignOn plug-in configurazione** pagina, fare clic su **aggiungere Provider di identità aggiuntive** pulsante Impostazioni hello tooconfigure di Provider di identità.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-samlssoconfluence-tutorial/addon4.png)

17. In questa pagina eseguire la procedura seguente:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-samlssoconfluence-tutorial/addon5.png)
 
    a. Aggiungere **nome** di hello Provider di identità (ad esempio, Azure AD).
    
    b. Aggiungere **descrizione** di hello Provider di identità (ad esempio, Azure AD).

    c. Fare clic su **XML** e seleziona hello **metadati** file scaricato dal portale di Azure.

    d. Fare clic sul pulsante **Load** (Carica).

    e. Legge i metadati IdP hello e popola i campi di hello come evidenziato nella schermata di hello.   
18. Fare clic su **salvare impostazioni** pulsante Impostazioni hello toosave.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-samlssoconfluence-tutorial/addon6.png)

> [!TIP]
> È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!  Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello. È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.

![Creare un utente di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-samlssoconfluence-tutorial/create_aaduser_01.png) 

2. elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-samlssoconfluence-tutorial/create_aaduser_02.png) 

3. hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-samlssoconfluence-tutorial/create_aaduser_03.png) 

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-samlssoconfluence-tutorial/create_aaduser_04.png) 

    a. In hello **nome** casella tipo **BrittaSimon**.

    b. In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Show Password** e annotare il valore di hello di hello **Password**.

    d. Fare clic su **Crea**.
 
### <a name="creating-a-saml-sso-for-confluence-by-resolution-gmbh-test-user"></a>Creazione di un utente di test di SAML SSO for Confluence di resolution GmbH

toolog agli utenti di Azure AD tooenable in tooSAML SSO per confluenza dalla risoluzione GmbH, è necessario eseguirne il provisioning in SAML SSO per confluenza dalla risoluzione GmbH.  
In SAML SSO for Confluence di resolution GmbH il provisioning è un'attività manuale.

**tooprovision un account utente, eseguire hello alla procedura seguente:**

1. Accedi tooyour SAML SSO per confluenza dal sito di risoluzione GmbH aziendale come amministratore.

2. Passare il mouse su ruota dentata e scegliere hello **Gestione utenti**.

    ![Aggiungere un dipendente](./media/active-directory-saas-samlssoconfluence-tutorial/user1.png) 

3. Nella sezione Users (Utenti) fare clic sula scheda **Add users** (Aggiungi utenti). In hello **"Aggiungi utente"** finestra di dialogo eseguire hello alla procedura seguente:

    ![Aggiungere un dipendente](./media/active-directory-saas-samlssoconfluence-tutorial/user2.png) 

    a. In hello **Username** casella di testo, posta elettronica hello tipo di utente come Britta Simon.

    b. In hello **nome completo** casella di testo, nome completo del tipo hello dell'utente come Britta Simon.

    c. In hello **posta elettronica** casella di testo, digitare hello di indirizzo di posta elettronica dell'utente come Brittasimon@contoso.com.

    d. In hello **Password** casella di testo, digitare la password per Britta Simon hello.

    e. Fare clic su **Conferma Password** digitare nuovamente la password di hello.
    
    f. Fare clic sul pulsante **Aggiungi**.    

### <a name="assigning-hello-azure-ad-test-user"></a>Assegnazione utente test hello Azure AD

In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooSAML SSO per confluenza dalla risoluzione GmbH.

![Assegna utente][200] 

**tooassign Britta Simon tooSAML SSO per confluenza dalla risoluzione GmbH, eseguire hello alla procedura seguente:**

1. Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **SAML SSO per confluenza dalla risoluzione GmbH**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_app.png) 

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![Assegna utente][202] 

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.

Quando si fa clic hello SAML SSO per confluenza dal riquadro GmbH risoluzione in hello Pannello di accesso, è necessario ottenere tooyour automaticamente firmato-on SAML SSO per confluenza dalla risoluzione GmbH applicazione.
Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_203.png

