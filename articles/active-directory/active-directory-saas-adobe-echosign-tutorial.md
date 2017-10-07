---
title: 'Esercitazione: Integrazione di Azure Active Directory con Adobe Sign | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e il segno di Adobe.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f9385723-8fe7-4340-8afb-1508dac3e92b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/24/2017
ms.author: jeedes
ms.openlocfilehash: b4b07907f30a0890003554a02a76d968400b43ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adobe-sign"></a>Esercitazione: Integrazione di Azure Active Directory con Adobe Sign

In questa esercitazione, è illustrato come toointegrate Adobe accedere con Azure Active Directory (Azure AD).

Integrazione di Adobe accesso con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooAdobe Sign
- È possibile abilitare l'utenti tooautomatically get connesso tooAdobe Sign (Single Sign-On) con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

integrazione di Azure AD con il segno di Adobe tooconfigure, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione di Adobe Sign abilitata per l'accesso Single Sign-On

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di accesso Adobe dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-adobe-sign-from-hello-gallery"></a>Aggiunta di accesso Adobe dalla raccolta hello
integrazione hello tooconfigure di Adobe Sign in Azure AD, è necessario tooadd Adobe accesso dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd accesso Adobe dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Applicazioni][2]
    
3. tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.

    ![Applicazioni][3]

4. Nella casella di ricerca hello, digitare **accesso Adobe**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_search.png)

5. Nel riquadro dei risultati hello, selezionare **accesso Adobe**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Adobe Sign usando un utente test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello Adobe segno è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e utente correlato di hello in Adobe Sign richiede toobe stabilita.

Segno di Adobe, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.

tooconfigure e prova AD Azure single sign-on con il segno di Adobe, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creazione di un utente di test di accesso Adobe](#creating-an-adobe-sign-test-user)**  -toohave un equivalente di Britta Simon segno Adobe che è la rappresentazione toohello collegato Azure AD dell'utente.
4. **[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Adobe Sign.

**tooconfigure AD Azure single sign-on con il segno di Adobe, eseguire hello alla procedura seguente:**

1. Nel portale di Azure su hello hello **accesso Adobe** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Configura accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_samlbase.png)

3. In hello **URL e il dominio di accesso Adobe** seguire hello alla procedura seguente:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_url.png)

    a. In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<companyname>.echosign.com/`

    b. In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<companyname>.echosign.com`

    > [!NOTE] 
    > Poiché questi non sono i valori reali, Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore. Contatto [team di supporto Client di accesso Adobe](https://helpx.adobe.com/in/contact/support.html) tooget questi valori. 
 
4. In hello **certificato di firma SAML** fare clic su **Certificate(Base64)** e quindi salvare il file di certificato hello nel computer in uso.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_certificate.png) 

5. Fare clic sul pulsante **Salva** .

    ![Configura accesso Single Sign-On](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_400.png)

6. In hello **configurazione accesso Adobe** fare clic su **configurare accesso Adobe** tooopen **Configura sign-on** finestra. Hello copia **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**

    ![Configura accesso Single Sign-On](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_configure.png) 


7. In una finestra del web browser, accedere come amministratore nel sito della società di accesso Adobe tooyour.

8. Scegliere hello menu in alto hello **Account**, quindi, nel riquadro di spostamento hello sul lato sinistro di hello, fare clic su **impostazioni SAML** in **impostazioni Account**.
   
   ![Account](./media/active-directory-saas-adobe-echosign-tutorial/ic789520.png "Account")

9. Nella sezione Impostazioni SAML hello, eseguire hello alla procedura seguente:
   
   ![Impostazioni SAML](./media/active-directory-saas-adobe-echosign-tutorial/ic789521.png "Impostazioni SAML")
   
   a. Per **SAML Mode** (Modalità SAML), selezionare **SAML Mandatory** (SAML obbligatorio).
   
   b. Selezionare **toolog Allow EchoSign Account Administrators con le credenziali EchoSign**.
   
   c. In **User Creation** (Creazione utente), selezionare **Automatically add users authenticated through SAML** (Aggiungi automaticamente gli utenti autenticati tramite SAML).

10. Spostare, eseguire hello seguendo i passaggi:

       ![Impostazioni SAML](./media/active-directory-saas-adobe-echosign-tutorial/ic789522.png "Impostazioni SAML")

    a. Incolla **ID entità SAML**, che è stato copiato dal portale di Azure in hello **IdP Entity ID** casella di testo.
    
    b. Incolla **SAML Single Sign-On Service URL**, che è stato copiato dal portale di Azure in hello **IdP Login URL** casella di testo.
   
    c. Incolla **Sign-Out URL**, che è stato copiato dal portale di Azure in hello **IdP Logout URL** casella di testo.

    d. Aprire lo scaricato **Certificate(Base64)** file nel blocco note, hello copia del contenuto di esso negli Appunti e quindi incollarlo toohello **IdP Certificate** casella di testo

    e. Fare clic su **Salva modifiche**.

> [!TIP]
> È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!  Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello. È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.

![Creare un utente di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_01.png) 

2. elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_02.png) 

3. hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_03.png) 

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_04.png) 

    a. In hello **nome** casella tipo **BrittaSimon**.

    b. In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Show Password** e annotare il valore di hello di hello **Password**.

    d. Fare clic su **Crea**.
 
### <a name="creating-an-adobe-sign-test-user"></a>Creazione di un utente di test di Adobe Sign

toolog agli utenti di Azure AD tooenable in tooAdobe Sign, è necessario eseguirne il provisioning in Adobe Sign. In caso di hello del segno di Adobe, il provisioning è un'attività manuale.

>[!NOTE]
>È possibile usare qualsiasi altro accesso Adobe utente account strumento di creazione o qualsiasi API fornita da Adobe Sign tooprovision account utente di AAD. 

**tooprovision un account utente, eseguire hello alla procedura seguente:**

1. Accedi tooyour **accesso Adobe** sito aziendale come amministratore.

2. Scegliere dal menu hello in primo piano hello **Account**, quindi, nel riquadro di spostamento hello sul lato sinistro di hello, fare clic su **utenti e gruppi**e quindi fare clic su **creare un nuovo utente**.
   
   ![Account](./media/active-directory-saas-adobe-echosign-tutorial/ic789524.png "Account")
   
3. In hello **Create New User** seguire hello alla procedura seguente:
   
   ![Crea utente](./media/active-directory-saas-adobe-echosign-tutorial/ic789525.png "Crea utente")
   
   a. Hello tipo **indirizzo di posta elettronica**, **nome**, e **cognome** di un account aAd di cui si desidera tooprovision in hello relative caselle di testo.
   
   b. Fare clic su **Create User**.

>[!NOTE]
>titolare dell'account di Azure Active Directory Hello riceve un messaggio di posta elettronica che include un account di hello tooconfirm collegamento prima che diventi attivo. 

### <a name="assigning-hello-azure-ad-test-user"></a>Assegnazione utente test hello Azure AD

In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooAdobe Sign.

![Assegna utente][200] 

**tooassign Britta Simon tooAdobe Sign, eseguire hello alla procedura seguente:**

1. Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **accesso Adobe**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_app.png) 

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![Assegna utente][202] 

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

Quando si fa clic hello accesso Adobe riquadro in hello Pannello di accesso, è necessario ottenere tooyour automaticamente firmato in applicazioni di accesso di Adobe.
Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_203.png

