---
title: 'Esercitazione: Integrazione di Azure Active Directory con GitHub | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e GitHub.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4395bd95-05de-4deb-87a5-dc3bc8ac4d95
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 688779de4e6627e49c0e3e8a7576f2f8c7a81ab1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-github"></a>Esercitazione: Integrazione di Azure Active Directory con GitHub

In questa esercitazione, è illustrato come toointegrate GitHub con Azure Active Directory (Azure AD).

Integrazione di GitHub con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooGitHub
- È possibile abilitare l'utenti tooautomatically get connesso tooGitHub (Single Sign-On) con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale - portale di gestione di Azure hello

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

integrazione di Azure AD con GitHub tooconfigure, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione di GitHub abilitata per l'accesso Single Sign-On


> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.


passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione, a meno che non sia necessario.
- Se non è disponibile un ambiente di prova di Azure AD, è possibile ottenere una versione di prova di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).


## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di GitHub dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD


## <a name="adding-github-from-hello-gallery"></a>Aggiunta di GitHub dalla raccolta hello
integrazione hello tooconfigure di GitHub in Azure AD, è necessario tooadd GitHub dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd GitHub dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[il portale di gestione di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Applicazioni][2]
    
3. Fare clic su **Aggiungi** pulsante nella parte superiore di hello della finestra di dialogo hello.

    ![Applicazioni][3]

4. Nella casella di ricerca hello, digitare **GitHub.com**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-github-tutorial/tutorial_github_search02.png)

5. Nel riquadro dei risultati hello, selezionare **GitHub**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-github-tutorial/tutorial_github_search_result02.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con GitHub in base a un utente test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in GitHub è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in GitHub deve toobe stabilita.

Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in GitHub.

tooconfigure e prova AD Azure single sign-on con GitHub, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creazione di un utente test GitHub](#creating-a-GitHub-test-user)**  -toohave un equivalente di Britta Simon in GitHub che è la rappresentazione toohello collegato Azure AD dell'utente.
4. **[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on nel portale di gestione di Azure hello e configurare l'accesso single sign-on nell'applicazione GitHub.

**Azure AD tooconfigure single sign-on con GitHub, eseguire hello alla procedura seguente:**

1. Nel portale di gestione di Azure hello in hello **GitHub** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Configura accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo, come **modalità** selezionare **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-github-tutorial/tutorial_github_01.png)

3. In hello **GitHub dominio e gli URL** seguire hello alla procedura seguente:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-github-tutorial/tutorial_github_saml011.png)

    a. In hello **Sign-on URL** casella di testo, tipo di valore hello di:`https://github.com/orgs/<entity-id>/sso`

    b. In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://github.com/orgs/<entity-id>`

    > [!NOTE] 
    > Si noti che queste non sono valori reali hello. È necessario tooupdate questi valori con hello effettivo tramite URL e l'identificatore. In questo caso, è consigliabile si toouse hello valore univoco della stringa nell'identificatore hello. Passare tooGitHub Admin sezione tooretrieve questi valori. 

4. In hello **gli attributi utente** selezionare **identificatore utente** come user.mail.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-github-tutorial/tutorial_github_attribute_new01.png)
    
5. In hello **certificato di firma SAML** fare clic su **Crea nuovo certificato**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-github-tutorial/tutorial_github_03.png)

6. In hello **creare nuovo certificato** finestra di dialogo, fare clic sull'icona calendario hello e selezionare un **data di scadenza**. Fare quindi clic sul pulsante **Salva**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-github-tutorial/tutorial_general_300.png)

7. In hello **certificato di firma SAML** selezionare **attivare di nuovo certificato** e fare clic su **salvare** pulsante.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-github-tutorial/tutorial_github_04.png)

8. Nel menu a comparsa hello **il certificato di Rollover** finestra, fare clic su **OK**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-github-tutorial/tutorial_general_400.png)

9. In hello **certificato di firma SAML** fare clic su **certificato (Base64)** e quindi salvare il file di certificato hello nel computer in uso.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-github-tutorial/tutorial_github_05.png) 

10. In hello **GitHub configurazione** fare clic su **configurazione di GitHub** tooopen **Configura sign-on** finestra.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-github-tutorial/tutorial_github_06.png) 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-github-tutorial/tutorial_github_07.png)

11. In un'altra finestra del Web browser accedere al sito aziendale di GitHub come amministratore.

12. Passare troppo**impostazioni** e fare clic su **sicurezza**

    ![Impostazioni](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_03.png)

13. Controllare hello **Enable SAML authentication** casella rivelare hello Single Sign-on i campi della configurazione. Utilizzare quindi hello single sign-on URL valore tooupdate hello URL Single sign-on nella configurazione di Azure AD.

    ![Impostazioni](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_13.png)

14. Configurare hello seguenti campi:

    a. **URL di accesso**: immettere **SAML Single sign-on Service URL** da hello **configurazione di GitHub** sezione su Azure AD

    b. **Autorità di certificazione**: immettere **ID entità SAML** da hello **configurazione di GitHub** sezione su Azure AD

    c. **Certificato pubblico**: hello aprire scaricato certificato da Azure AD in un contenuto di hello in blocco note e copiare inclusi "BEGIN" e "Fine certificato"

    ![Impostazioni](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_051.png)

15. Fare clic su **configurazione SAML del Test** tooconfirm che non gli errori di convalida o errori durante l'accesso SSO.

    ![Impostazioni](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_06.png)

16. Fare clic su **Save**

### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
obiettivo di Hello di questa sezione è un utente di test nel portale di gestione di Azure hello chiamato Britta Simon toocreate.

![Creare un utente di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di gestione di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-github-tutorial/create_aaduser_01.png) 

2. Andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti** elenco hello toodisplay degli utenti.
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-github-tutorial/create_aaduser_02.png) 

3. Nella parte superiore di hello della finestra di dialogo hello fare clic su **Aggiungi** tooopen hello **utente** finestra di dialogo.
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-github-tutorial/create_aaduser_03.png) 

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-github-tutorial/create_aaduser_04.png) 

    a. In hello **nome** casella tipo **BrittaSimon**.

    b. In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Show Password** e annotare il valore di hello di hello **Password**.

    d. Fare clic su **Crea**. 


### <a name="creating-a-github-test-user"></a>Creazione di un utente test GitHub

In ordine tooenable Azure AD utenti toolog in GitHub, è necessario eseguirne il provisioning in GitHub.  
Nel caso di hello di GitHub, il provisioning è un'attività manuale.

**eseguire un account utente, tooprovision hello i passaggi seguenti:**

1. Accedi tooyour sito aziendale GitHub come amministratore.

2. Fare clic su **Persone**.

    ![Persone](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_08.png "Persone")

3. Fare clic su **Invite member** (Invita membro).

    ![Invitare utenti](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_09.png "Invitare utenti")

4. In hello **membro invito** finestra di dialogo eseguire hello alla procedura seguente:

    a. In hello **posta elettronica** casella di testo, digitare hello indirizzo di posta elettronica dell'account di Britta Simon.

    ![Invitare persone](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_10.png "Invitare persone")
    
    b. Fare clic su **Send Invitation** (Invia invito).

    ![Invitare persone](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_11.png "Invitare persone")

    > [!NOTE]
    > titolare dell'account di Hello Azure Active Directory riceverà un messaggio di posta elettronica e seguire il proprio account tooconfirm un collegamento prima che diventi attivo.


### <a name="assigning-hello-azure-ad-test-user"></a>Assegnazione utente test hello Azure AD

In questa sezione è abilitare Britta Simon toouse single sign-on Azure concedendo tooGitHub proprio accesso.

![Assegna utente][200] 

**tooassign Britta Simon tooGitHub, eseguire hello alla procedura seguente:**

1. Nel portale di gestione di Azure hello, aprire visualizzazione applicazioni hello, quindi selezionare la visualizzazione di directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **GitHub.com**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-github-tutorial/tutorial_github_search_result021.png) 

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![Assegna utente][202] 

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    


### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.

Quando si fa clic su riquadro GitHub hello in hello Pannello di accesso, è necessario ottenere tooyour connesso GitHub applicazione. Sarà possibile registrazione come un account aziendale ma toolog necessario con l'account personale.


## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-github-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-github-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-github-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-github-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-github-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-github-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-github-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-github-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-github-tutorial/tutorial_general_203.png
