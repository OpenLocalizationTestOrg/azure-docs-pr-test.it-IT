---
title: 'Esercitazione: Integrazione di Azure Active Directory con Blackboard Learn - Shibboleth | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e informazioni di lavagna - Shibboleth.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e435cbb4-c0f0-400e-943c-5c923fa8ddf2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: jeedes
ms.openlocfilehash: 40aa3ec5f42b93157af3c56daaadfa66203b21d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-blackboard-learn---shibboleth"></a>Esercitazione: Integrazione di Azure Active Directory con Blackboard Learn - Shibboleth

In questa esercitazione, è illustrato come toointegrate Lavagna informazioni - Shibboleth con Azure Active Directory (Azure AD).

L'integrazione delle informazioni di lavagna - Shibboleth con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooBlackboard informazioni - Shibboleth
- È possibile abilitare l'utenti tooautomatically get connesso tooBlackboard informazioni - Shibboleth (Single Sign-On) con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

tooconfigure integrazione di Azure AD con informazioni Lavagna - Shibboleth, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Una sottoscrizione abilitata all'accesso Single Sign-On di Blackboard Learn - Shibboleth

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di informazioni di lavagna - Shibboleth dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-blackboard-learn---shibboleth-from-hello-gallery"></a>Aggiunta di informazioni di lavagna - Shibboleth dalla raccolta hello
integrazione di hello tooconfigure di lavagna informazioni - Shibboleth in Azure AD, è necessario tooadd Lavagna informazioni - Shibboleth dall'elenco di tooyour hello raccolta di App SaaS gestite.

**informazioni su Lavagna - tooadd Shibboleth dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Applicazioni][2]
    
3. tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.

    ![Applicazioni][3]

4. Nella casella di ricerca hello, digitare **Lavagna informazioni - Shibboleth**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_search.png)

5. Nel riquadro dei risultati hello, selezionare **Lavagna informazioni - Shibboleth**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Blackboard Learn - Shibboleth usando un utente di test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello nella Lavagna informazioni - Shibboleth è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure AD e l'utente correlato hello Lavagna informazioni - Shibboleth deve toobe stabilita.

In informazioni Lavagna - Shibboleth, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.

tooconfigure e prova AD Azure single sign-on con informazioni Lavagna - Shibboleth, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creazione di una lavagna informazioni - utente test Shibboleth](#creating-a-blackboard-learn---shibboleth-test-user)**  - toohave un equivalente di Britta Simon nella Lavagna informazioni - Shibboleth che è la rappresentazione toohello collegato Azure AD dell'utente.
4. **[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nella Lavagna informazioni - applicazione di Shibboleth.

**Azure AD tooconfigure single sign-on con informazioni Lavagna - Shibboleth, eseguire hello alla procedura seguente:**

1. Nel portale di Azure su hello hello **Lavagna informazioni - Shibboleth** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Configura accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_samlbase.png)

3. In hello **Lavagna informazioni - URL e il dominio di Shibboleth** seguire hello alla procedura seguente:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_url.png)

    a. In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<yourblackoardlearnserver>.blackboardlearn.com/Shibboleth.sso/Login`

    b. In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<yourblackoardlearnserver>.blackboardlearn.com/shibboleth-sp`

    c. In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<yourblackoardlearnserver>.blackboardlearn.com/Shibboleth.sso/SAML2/POST`
 
    > [!NOTE] 
    > Poiché questi non sono i valori reali, Aggiornare questi valori con hello effettivo identificatore, l'URL di risposta e URL Sign-On. Contatto [Lavagna informazioni - team di supporto Client di Shibboleth](https://www.blackboard.com/forms/contact-us_form.aspx) tooget questi valori. 

4. In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_certificate.png) 

5. Fare clic sul pulsante **Salva** .

    ![Configura accesso Single Sign-On](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_400.png)
    
6. In hello **Lavagna informazioni - configurazione di Shibboleth** fare clic su **configurare informazioni Lavagna - Shibboleth** tooopen **Configura sign-on** finestra. Hello copia **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**

    ![Configura accesso Single Sign-On](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_configure.png) 

7. tooconfigure single sign-on sul **Lavagna informazioni - Shibboleth** lato, è necessario hello toosend scaricato **Metadata XML** e **Sign-Out URL, l'ID entità SAML e servizio SAML Single Sign-On URL** troppo[Lavagna informazioni - team di supporto di Shibboleth](https://www.blackboard.com/forms/contact-us_form.aspx).

> [!TIP]
> È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!  Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello. È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.

![Creare un utente di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/create_aaduser_01.png) 

2. elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/create_aaduser_02.png) 

3. hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/create_aaduser_03.png) 

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/create_aaduser_04.png) 

    a. In hello **nome** casella tipo **BrittaSimon**.

    b. In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Show Password** e annotare il valore di hello di hello **Password**.

    d. Fare clic su **Crea**.
 
### <a name="creating-a-blackboard-learn---shibboleth-test-user"></a>Creazione di un utente di test di Blackboard Learn - Shibboleth

In questa sezione viene creato un utente di nome Britta Simon in Blackboard Learn - Shibboleth. Utilizzare il [Lavagna informazioni - team di supporto di Shibboleth](https://www.blackboard.com/forms/contact-us_form.aspx) tooadd utenti hello hello Lavagna informazioni - piattaforma Shibboleth.

### <a name="assigning-hello-azure-ad-test-user"></a>Assegnazione utente test hello Azure AD

In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooBlackboard informazioni - Shibboleth.

![Assegna utente][200] 

**tooassign Britta Simon tooBlackboard informazioni - Shibboleth, eseguire hello alla procedura seguente:**

1. Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **Lavagna informazioni - Shibboleth**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_app.png) 

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![Assegna utente][202] 

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.

Quando si fa clic hello Lavagna informazioni - riquadro Shibboleth in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour Lavagna informazioni - applicazione di Shibboleth.

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_203.png

