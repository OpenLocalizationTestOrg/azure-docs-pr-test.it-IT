---
title: 'Esercitazione: Integrazione di Azure Active Directory con PlanMyLeave | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e PlanMyLeave.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b0d31cbe-7ae2-488b-9cf3-4927391fa744
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/01/2017
ms.author: jeedes
ms.openlocfilehash: 44a6782e44ef22fc957544960be1742f9eed6e51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-planmyleave"></a>Esercitazione: Integrazione di Azure Active Directory con PlanMyLeave

In questa esercitazione, è illustrato come toointegrate PlanMyLeave con Azure Active Directory (Azure AD).

Integrazione PlanMyLeave con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooPlanMyLeave
- È possibile abilitare l'utenti tooautomatically get connesso tooPlanMyLeave (Single Sign-On) con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale - portale di gestione di Azure hello

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

integrazione di Azure AD con PlanMyLeave tooconfigure, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione di PlanMyLeave abilitata per l'accesso Single Sign-On


> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.


passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione, a meno che non sia necessario.
- Se non è disponibile un ambiente di prova di Azure AD, è possibile ottenere una versione di prova di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).


## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di PlanMyLeave dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD


## <a name="adding-planmyleave-from-hello-gallery"></a>Aggiunta di PlanMyLeave dalla raccolta hello
integrazione hello tooconfigure di PlanMyLeave in Azure AD, è necessario tooadd PlanMyLeave dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd PlanMyLeave dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[il portale di gestione di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Applicazioni][2]
    
3. Fare clic su **Aggiungi** pulsante nella parte superiore di hello della finestra di dialogo hello.

    ![Applicazioni][3]

4. Nella casella di ricerca hello, digitare **PlanMyLeave**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_001.png)

5. Nel riquadro dei risultati hello, selezionare **PlanMyLeave**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con PlanMyLeave in base a un utente test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in PlanMyLeave è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in PlanMyLeave deve toobe stabilita.

Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in PlanMyLeave.

tooconfigure e prova AD Azure single sign-on con PlanMyLeave, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creazione di un utente test PlanMyLeave](#creating-a-planmyleave-test-user)**  -toohave un equivalente di Britta Simon in PlanMyLeave toohello collegato AD Azure rappresentazione in seguito.
4. **[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on nel portale di gestione di Azure hello e configurare l'accesso single sign-on nell'applicazione PlanMyLeave.

**Azure AD tooconfigure single sign-on con PlanMyLeave, eseguire hello alla procedura seguente:**

1. Nel portale di gestione di Azure hello in hello **PlanMyLeave** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Configura accesso Single Sign-On][4]

2. In hello **Single sign-on** nella pagina, come **modalità** selezionare **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_01.png)

3. In hello **PlanMyLeave dominio e gli URL** seguire hello alla procedura seguente:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_02.png)

    a. In hello **URL di accesso** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<company-name>.planmyleave.com/Login.aspx`
    
    b. In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<company-name>.planmyleave.com`

    > [!NOTE] 
    > Si noti che queste non sono valori reali hello. È necessario tooupdate questi valori con hello effettivo accesso URL e l'identificatore. Contatto [team di supporto PlanMyLeave](mailto:support@planmyleave.com) tooget questi valori.

4. In hello **certificato di firma SAML** fare clic su **Crea nuovo certificato**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_03.png)     

5. In hello **creare nuovo certificato** finestra di dialogo, fare clic sull'icona calendario hello e selezionare un **data di scadenza**. Fare quindi clic sul pulsante **Salva**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-planmyleave-tutorial/tutorial_general_300.png)

6. In hello **certificato di firma SAML** selezionare **attivare di nuovo certificato** e fare clic su **salvare** pulsante.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_04.png)

7. Nel menu a comparsa hello **il certificato di Rollover** finestra, fare clic su **OK**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-planmyleave-tutorial/tutorial_general_400.png)

8. In hello **certificato di firma SAML** fare clic su **certificato (base64)** e quindi salvare il file di certificato hello nel computer in uso.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_05.png) 

9. In hello **PlanMyLeave configurazione** fare clic su **configurare PlanMyLeave** tooopen **Configura sign-on** finestra.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_06.png) 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_07.png)

10. In un'altra finestra del browser Web accedere al tenant di PlanMyLeave come amministratore.

11. Andare troppo**installazione System**. Quindi, nella hello **gestione della sicurezza** fare clic su sezione **impostazioni società SAML** .

    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_002.png) 

12. In hello **impostazioni SAML** sezione fare clic sull'icona di editor.

    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_003.png)

13. In hello **impostazioni SAML Update** seguire hello alla procedura seguente:

    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_004.png)

    a.  In hello **URL di accesso** casella di testo, inserire il valore di hello di **SAML Single Sign-On Service URL** dalla finestra di configurazione dell'applicazione Azure AD.

    b.  Aprire il file del certificato scaricato nel blocco note, copiare solo il contenuto di hello tra hello---inizio certificato--- e ---fine certificato---ne negli Appunti e quindi incollarlo toohello **certificato** casella di testo.

    c. Impostare"**è Enable**"troppo"**Sì**".

    d. Fare clic su **Save**.



### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
obiettivo di Hello di questa sezione è un utente di test nel portale di gestione di Azure hello chiamato Britta Simon toocreate.

![Creare un utente di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di gestione di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_01.png) 

2. Andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti** elenco hello toodisplay degli utenti.
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_02.png) 

3. Nella parte superiore di hello della finestra di dialogo hello fare clic su **Aggiungi** tooopen hello **utente** finestra di dialogo.
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_03.png) 

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_04.png) 

    a. In hello **nome** casella tipo **BrittaSimon**.

    b. In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Show Password** e annotare il valore di hello di hello **Password**.

    d. Fare clic su **Create**(Crea). 



### <a name="creating-a-planmyleave-test-user"></a>Creazione di un utente test di PlanMyLeave

obiettivo di Hello di questa sezione è un utente denominato Britta Simon in PlanMyLeave toocreate. PlanMyLeave supporta il provisioning just-in-time, che è abilitato per impostazione predefinita.

Non è necessario alcun intervento dell'utente in questa sezione. Verrà creato un nuovo utente durante una tooaccess tentativo PlanMyLeave se non esiste ancora.

> [!NOTE]
> Se è necessario un utente toocreate manualmente, è necessario toocontact [team di supporto PlanMyLeave](mailto:support@planmyleave.com).



### <a name="assigning-hello-azure-ad-test-user"></a>Assegnazione utente test hello Azure AD

In questa sezione è abilitare Britta Simon toouse single sign-on Azure concedendo tooPlanMyLeave proprio accesso.

![Assegna utente][200] 

**tooassign Britta Simon tooPlanMyLeave, eseguire hello alla procedura seguente:**

1. Nel portale di gestione di Azure hello, aprire visualizzazione applicazioni hello, quindi selezionare la visualizzazione di directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **PlanMyLeave**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_50.png) 

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![Assegna utente][202] 

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    


### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.

Quando si fa clic su riquadro PlanMyLeave hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour PlanMyLeave applicazione.


## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_203.png