---
title: 'Esercitazione: Integrazione di Azure Active Directory con Velpic SAML| Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Velpic SAML.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 613947d8fe95113382a2cdc0f79ce9eda85a0127
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-velpic-saml"></a>Esercitazione: Integrazione di Azure Active Directory con Velpic SAML

In questa esercitazione, è illustrato come toointegrate Velpic SAML con Azure Active Directory (Azure AD).

Integrazione Velpic SAML con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooVelpic SAML
- È possibile abilitare l'utenti tooautomatically get connesso tooVelpic SAML (Single Sign-On) con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale - portale di gestione di Azure hello

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

integrazione di Azure AD con SAML Velpic tooconfigure, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione di Velpic SAML abilitata per l'accesso Single Sign-On

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione, a meno che non sia necessario.
- Se non è disponibile un ambiente di prova di Azure AD, è possibile ottenere una versione di prova di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di SAML Velpic dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-velpic-saml-from-hello-gallery"></a>Aggiunta di SAML Velpic dalla raccolta hello
integrazione hello tooconfigure di Velpic SAML in Azure AD, è necessario tooadd Velpic SAML dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd Velpic SAML dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[il portale di gestione di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Applicazioni][2]
    
3. Fare clic su **Aggiungi** pulsante nella parte superiore di hello della finestra di dialogo hello.

    ![Applicazioni][3]

4. Nella casella di ricerca hello, digitare **Velpic SAML**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_search.png)

5. Nel riquadro dei risultati hello, selezionare **Velpic SAML**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Velpic SAML in base a un utente test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Velpic SAML è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Velpic SAML deve toobe stabilita.

Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in Velpic SAML.

tooconfigure e prova AD Azure single sign-on con Velpic SAML, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creazione di un utente test SAML Velpic](#creating-a-velpic-saml-test-user)**  -toohave un equivalente di Britta Simon in SAML Velpic toohello collegato AD Azure rappresentazione in seguito.
4. **[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on nel portale di gestione di Azure hello e configurare l'accesso single sign-on SAML Velpic nell'applicazione in uso.

**Azure AD tooconfigure single sign-on con Velpic SAML, eseguire hello alla procedura seguente:**

1. Nel portale di gestione di Azure hello in hello **Velpic SAML** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Configura accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo, come **modalità** selezionare **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_samlbase.png)

3. Immettere i dettagli di hello in hello **Velpic SAML dominio e gli URL** sezione -

    ![Configura accesso Single Sign-On](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_url.png)

    a. In hello **Sign-on URL** casella di testo, tipo di valore hello di:`https://<sub-domain>.velpicsaml.net`

    b. In hello **identificatore** casella di testo, incollare hello **'Single sign-on URL'** valore`https://auth.velpic.com/saml/v2/<entity-id>/login`
    
    > [!NOTE]
    > Si noti che hello URL di accesso verrà fornita dai team Velpic SAML hello e valore dell'identificatore sarà disponibile quando si configura hello SSO di plug-in sul lato Velpic SAML. È necessario toocopy che il valore dalla pagina dell'applicazione Velpic SAML e incollarlo qui.

4. In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file XML hello nel computer in uso.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_certificate.png) 

5. Fare clic sul pulsante **Salva** .

    ![Configura accesso Single Sign-On](./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_400.png)

6. Nella sezione di configurazione di SAML Velpic hello, scegliere Configura SAML Velpic tooopen Configura sign-on finestra. Copiare hello ID entità SAML dalla sezione di riferimento rapido hello.

7. In un'altra finestra del Web browser accedere al sito aziendale di Velpic SAML come amministratore.

8. Fare clic su **Gestisci** scheda e andare troppo**integrazione** sezione in cui è necessario tooclick in **plug-in** pulsante toocreate nuovo plug-in per l'accesso.

    ![Plug-in](./media/active-directory-saas-velpicsaml-tutorial/velpic_1.png)

9. Fare clic su hello **'Aggiungi plug-in'** pulsante.
    
    ![Plug-in](./media/active-directory-saas-velpicsaml-tutorial/velpic_2.png)

10. Fare clic su hello **SAML** riquadro nella pagina Aggiungi plug-in di hello.
    
    ![Plug-in](./media/active-directory-saas-velpicsaml-tutorial/velpic_3.png)

11. Immettere il nome di hello di hello nuovo SAML plug-in e fare clic su hello **'Add'** pulsante.

    ![Plug-in](./media/active-directory-saas-velpicsaml-tutorial/velpic_4.png)

12. Immettere i dettagli di hello come indicato di seguito:

    ![Plug-in](./media/active-directory-saas-velpicsaml-tutorial/velpic_5.png)

    a. In hello **nome** casella di testo Nome hello del tipo di plug-in SAML.

    b. In hello **URL autorità di certificazione** casella di testo, incollare hello **ID entità SAML** copiato dalla hello **Configura sign-on** finestra di hello portale di Azure.

    c. In hello **configurazione di Provider di metadati** caricare hello file Metadata XML che è stato scaricato dal portale di Azure.

    d. È anche possibile scegliere tooenable SAML appena provisioning in-time abilitando hello **'Automatica consente di creare nuovi utenti'** casella di controllo. Se un utente non esiste in Velpic e questo flag non è abilitato, l'account di accesso hello Azure avrà esito negativo. Se il flag di hello è abilitato hello utente verrà automaticamente essere eseguito il provisioning in Velpic in fase di hello dell'account di accesso. 

    e. Hello copia **Single sign-on URL** dalla casella di testo hello e Incolla in hello portale di Azure.
    
    f. Fare clic su **Save**.

### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
obiettivo di Hello di questa sezione è un utente di test nel portale di gestione di Azure hello chiamato Britta Simon toocreate.

![Creare un utente di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di gestione di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_01.png) 

2. Andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti** elenco hello toodisplay degli utenti.
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_02.png) 

3. Nella parte superiore di hello della finestra di dialogo hello fare clic su **Aggiungi** tooopen hello **utente** finestra di dialogo.
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_03.png) 

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_04.png) 

    a. In hello **nome** casella tipo **BrittaSimon**.

    b. In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Show Password** e annotare il valore di hello di hello **Password**.

    d. Fare clic su **Crea**.
 
### <a name="creating-a-velpic-saml-test-user"></a>Creare un utente test di Velpic SAML

Questo passaggio non è in genere necessari come un'applicazione hello supporta just-in tempo il provisioning dell'utente. Se non è abilitato il provisioning utente automatico hello quindi la creazione manuale dell'utente può essere eseguita come descritto di seguito.

Accedere al sito aziendale di Velpic SAML come amministratore e seguire questa procedura:
    
1. Fare clic sulla scheda Gestisci passare tooUsers sezione, quindi fare clic su nuovi utenti di tooadd pulsante.

    ![Aggiungi utente](./media/active-directory-saas-velpicsaml-tutorial/velpic_7.png)

2. In hello **"Create New User"** finestra di dialogo eseguire hello alla procedura seguente.

    ![user](./media/active-directory-saas-velpicsaml-tutorial/velpic_8.png)
    
    a. In hello **nome** casella di testo, hello prima del tipo Britta Simon.

    b. In hello **cognome** casella di testo, digitare hello cognome di Britta Simon.

    c. In hello **nome utente** casella di testo, digitare il nome utente hello di Britta Simon.

    d. In hello **posta elettronica** casella di testo, digitare hello indirizzo di posta elettronica dell'account di Britta Simon.

    e. Resto delle informazioni di hello è facoltativo, che è possibile inserire se necessario.
    
    f. Fare clic su **SAVE**.  

### <a name="assigning-hello-azure-ad-test-user"></a>Assegnazione utente test hello Azure AD

In questa sezione è abilitare Britta Simon toouse single sign-on Azure concedendo proprio tooVelpic accesso SAML.

![Assegna utente][200] 

**tooassign Britta Simon tooVelpic SAML, eseguire hello alla procedura seguente:**

1. Nel portale di gestione di Azure hello, aprire visualizzazione applicazioni hello, quindi selezionare la visualizzazione di directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **Velpic SAML**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_app.png) 

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![Assegna utente][202] 

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.

1. Quando si fa clic hello Velpic SAML riquadro in hello Pannello di accesso, è necessario ottenere la pagina di accesso dell'applicazione Velpic SAML. Dovrebbe essere hello **'Accedi con Azure AD'** pulsante nella pagina di accesso hello.

    ![Plug-in](./media/active-directory-saas-velpicsaml-tutorial/velpic_6.png)

2. Fare clic su hello **'Accedi con Azure AD'** toolog pulsante in tooVelpic con l'account di Azure AD.


## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_203.png

