---
title: 'Esercitazione: Integrazione di Azure Active Directory con Learning at Work | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e l'apprendimento al lavoro.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1d607174-bea1-4f40-8233-54cabe02c66a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: jeedes
ms.openlocfilehash: fa09d585d57932a95cadba9a66029765d7df3694
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-learning-at-work"></a>Esercitazione: Integrazione di Azure Active Directory con Learning at Work

In questa esercitazione, è illustrato come toointegrate apprendimento al lavoro con Azure Active Directory (Azure AD).

Apprendimento al lavoro di integrazione con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooLearning al lavoro
- È possibile abilitare l'utenti tooautomatically get connesso tooLearning al lavoro (Single Sign-On) con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

tooconfigure integrazione di Azure AD con Learning al lavoro, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione di Learning at Work abilitata per l'accesso Single Sign-On

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di apprendimento in lavoro dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-learning-at-work-from-hello-gallery"></a>Aggiunta di apprendimento in lavoro dalla raccolta hello
integrazione di hello tooconfigure di apprendimento al lavoro in Azure AD, è necessario tooadd apprendimento al lavoro dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd apprendimento al lavoro dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Applicazioni][2]
    
3. tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.

    ![Applicazioni][3]

4. Nella casella di ricerca hello, digitare **apprendimento al lavoro**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_search.png)

5. Nel riquadro dei risultati hello, selezionare **apprendimento al lavoro**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Learning at Work usando un utente test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Learning al lavoro è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Learning al lavoro necessario toobe stabilita.

Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in Learning al lavoro.

tooconfigure e prova AD Azure single sign-on con Learning al lavoro, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creazione di un apprendimento all'utente di prova lavoro](#creating-a-learning-at-work-test-user)**  -toohave un equivalente di Britta Simon in Learning al lavoro che è la rappresentazione toohello collegato Azure AD dell'utente.
4. **[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nella formazione dell'applicazione.

**Azure AD tooconfigure single sign-on con Learning al lavoro, eseguire hello alla procedura seguente:**

1. Nel portale di Azure su hello hello **apprendimento al lavoro** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Configura accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_samlbase.png)

3. In hello **al dominio di lavoro e gli URL di apprendimento** seguire hello alla procedura seguente:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_url.png)

    a. In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<subdomain>.sabacloud.com/Saba/Web/<company code>`

    b. In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<subdomain>.sabacloud.com/Saba/saml/SSO/alias/<company name>`

    > [!NOTE] 
    > Questi valori non sono hello reale. Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore. Contatto [al team di supporto Client di lavoro di apprendimento](https://www.learninga-z.com/site/contact/support) tooget questi valori. 
 
4. In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_certificate.png) 

5. Fare clic sul pulsante **Salva** .

    ![Configura accesso Single Sign-On](./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_400.png)

6. In hello **apprendimento configurazione lavoro** fare clic su **configurare Learning al lavoro** tooopen **Configura sign-on** finestra. Hello copia **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**

    ![Configura accesso Single Sign-On](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_configure.png) 

7. tooconfigure single sign-on sul **apprendimento al lavoro** lato, è necessario hello toosend scaricato **Metadata XML**, **ID entità SAML**, **SAML Single Sign-On URL del servizio**, e **Sign-Out URL** troppo[al supporto tecnico di lavoro di apprendimento](https://www.learninga-z.com/site/contact/support).

> [!TIP]
> È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!  Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello. È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.

![Creare un utente di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-learning-at-work-tutorial/create_aaduser_01.png) 

2. elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-learning-at-work-tutorial/create_aaduser_02.png) 

3. hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-learning-at-work-tutorial/create_aaduser_03.png) 

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-learning-at-work-tutorial/create_aaduser_04.png) 

    a. In hello **nome** casella tipo **BrittaSimon**.

    b. In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Show Password** e annotare il valore di hello di hello **Password**.

    d. Fare clic su **Crea**.
 
### <a name="creating-a-learning-at-work-test-user"></a>Creazione di un utente test di Learning at Work

In questa sezione viene creato un utente di nome Britta Simon in Learning at Work. Lavorare con [al supporto tecnico di lavoro di apprendimento](https://www.learninga-z.com/site/contact/support) utenti hello tooadd hello Learning alla piattaforma di lavoro.

### <a name="assigning-hello-azure-ad-test-user"></a>Assegnazione utente test hello Azure AD

In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooLearning al lavoro.

![Assegna utente][200] 

**tooassign Britta Simon tooLearning al lavoro, eseguire hello alla procedura seguente:**

1. Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **apprendimento al lavoro**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_app.png) 

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![Assegna utente][202] 

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.

Quando si fa clic hello apprendimento nel riquadro di lavoro in hello Pannello di accesso, è necessario ottenere tooyour automaticamente firmato-on all'applicazione di lavoro di apprendimento.
Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_203.png

