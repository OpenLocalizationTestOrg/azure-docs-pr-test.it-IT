---
title: 'Esercitazione: Integrazione di Azure Active Directory con Clarizen | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Clarizen.
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
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: f24ccda3b90e5df9a203a444dfda905043b30276
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-clarizen"></a>Esercitazione: Integrazione di Azure Active Directory con Clarizen

In questa esercitazione, è illustrato come toointegrate Azure Active Directory (Azure AD) con Clarizen. In questo modo di integrazione hello seguenti vantaggi:

- È possibile controllare, in Azure AD, che dispone di accesso tooClarizen.
- È possibile abilitare il toobe gli utenti connessi automaticamente tooClarizen (single sign-on) con i propri account Azure AD.
- È possibile gestire gli account in un'unica posizione centrale, hello portale di Azure.

scenario di Hello in questa esercitazione è costituita da due attività principali:

1. Aggiungere Clarizen dalla raccolta di hello.
2. Configurare e testare l'accesso Single Sign-On di Azure AD.

Per altre informazioni sull'integrazione di app SaaS (Software as a Service) con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti
integrazione di Azure AD con Clarizen tooconfigure, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Una sottoscrizione di Clarizen abilitata per Single Sign-On

passaggi di hello tootest in questa esercitazione, seguire queste indicazioni:

- Testare l'accesso Single Sign-On di Azure AD in un ambiente di test. Non usare l'ambiente di produzione, a meno che non sia necessario.
- Se non è disponibile un ambiente di test di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).

## <a name="add-clarizen-from-hello-gallery"></a>Aggiungere Clarizen dalla raccolta di hello
integrazione di hello tooconfigure di Clarizen in Azure AD, aggiungere Clarizen hello raccolta tooyour elenco di App SaaS gestite.

1. In hello [portale di Azure](https://portal.azure.com)in hello riquadro sinistro, fare clic su hello **Azure Active Directory** icona.

    ![Icona Azure Active Directory][1]

2. Fare clic su **Applicazioni aziendali**. Fare quindi clic su **Tutte le applicazioni**.

    ![Clic su "Applicazioni aziendali" e su "Tutte le applicazioni"][2]

3. Fare clic su hello **Aggiungi** pulsante nella parte superiore di hello della finestra di dialogo hello.

    ![pulsante "Aggiungi" Hello][3]

4. Nella casella di ricerca hello, digitare **Clarizen**.

    ![Digitare "Clarizen" nella casella di ricerca hello](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_000.png)

5. Nel riquadro risultati hello selezionare **Clarizen**, quindi fare clic su **Aggiungi** tooadd un'applicazione hello.

    ![Selezione di Clarizen nel riquadro dei risultati di hello](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_0001.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurare e testare l'accesso Single Sign-On di Azure AD
Nelle seguenti sezioni di hello, configurare e testare Azure AD single sign-on con Clarizen in base all'utente di test hello Britta Simon.

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Clarizen è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Clarizen deve toobe stabilita. Per stabilire questa relazione di collegamento, assegnando il valore di hello del **nome utente** in Azure AD come valore hello **Username** in Clarizen.

tooconfigure e prova AD Azure single sign-on con Clarizen, hello completo seguenti blocchi predefiniti:

1. **[Configurare Azure AD single sign-on](#configure-azure-ad-single-sign-on)**  tooenable il toouse utenti questa funzionalità.
2. **[Creare un utente prova AD Azure](#create-an-azure-ad-test-user)**  tootest AD Azure single sign-on con Britta Simon.
3. **[Creare un utente test Clarizen](#create-a-clarizen-test-user)**  toohave un equivalente di Britta Simon in Clarizen toohello collegato AD Azure rappresentazione in seguito.
4. **[Assegnare l'utente test hello Azure AD](#assign-the-azure-ad-test-user)**  tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Testare single sign-on](#test-single-sign-on)**  tooverify hello se funzionamento della configurazione.

### <a name="configure-azure-ad-single-sign-on"></a>Configurare l'accesso Single Sign-On di Azure AD
Abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Clarizen.

1. Nel portale di Azure su hello hello **Clarizen** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Clic su "Single Sign-On"][4]

2. In hello **Single sign-on** nella finestra di dialogo per **modalità**selezionare **basato su SAML Sign-on** tooenable single sign-on.

    ![Selezione di "Accesso basato su SAML"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_01.png)

3. In hello **Clarizen dominio e gli URL** seguire hello alla procedura seguente:

    ![Caselle per identificatore e URL di risposta](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_02.png)

    a. In hello **identificatore** casella Tipo di un valore di hello: **Clarizen**

    b. In hello **URL di risposta** , digitare un URL con modello di hello: **https://<company name>.clarizen.com/Clarizen/Pages/Integrations/SAML/SamlResponse.aspx**

    > [!NOTE]
    > Non sono valori reali hello. Si dispone di toouse hello effettivo identificatore e URL di risposta. In questo caso è consigliabile utilizzare hello valore univoco di una stringa come identificatore hello. i valori effettivi, hello contatto di hello tooget [team di supporto di Clarizen](https://success.clarizen.com/hc/en-us/requests/new).

4. In hello **certificato di firma SAML** fare clic su **Crea nuovo certificato**.

    ![Clic su "Crea nuovo certificato"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_03.png)  

5. In hello **creare nuovo certificato** finestra di dialogo fare clic sull'icona calendario hello e selezionare una data di scadenza. Fare quindi clic su **Salva**.

    ![Selezione e salvataggio di una data di scadenza](./media/active-directory-saas-clarizen-tutorial/tutorial_general_300.png)

6. In hello **certificato di firma SAML** sezione, selezionare **attivare di nuovo certificato**, quindi fare clic su **salvare**.

    ![Selezionando la casella di controllo hello per rendere il nuovo certificato di hello attivo](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_04.png)

7. In hello **il certificato di Rollover** la finestra di dialogo, fare clic su **OK**.

    ![Fare clic su "OK" tooconfirm che si desidera toomake hello certificato active](./media/active-directory-saas-clarizen-tutorial/tutorial_general_400.png)

8. In hello **certificato di firma SAML** fare clic su **certificato (Base64)** e quindi salvare il file di certificato hello nel computer in uso.

    ![Fare clic su download di hello toostart "Certificato (Base64)"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_05.png)

9. In hello **Clarizen configurazione** fare clic su **configurare Clarizen** tooopen hello **Configura sign-on** finestra.

    ![Clic su "Configure Clarizen"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_06.png)

    ![Finestra "Configura accesso", con i file e gli URL](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_07.png)

10. In una finestra del web browser, accedere come amministratore nel sito della società Clarizen di tooyour.

11. Fare clic sul nome utente e quindi su **Settings** (Impostazioni).

    ![Clic su "Settings" (Impostazioni) sotto il nome utente](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_001.png "Settings (Impostazioni)")

12. Fare clic su hello **impostazioni globali** scheda. Quindi, Avanti troppo**autenticazione federata**, fare clic su **modifica**.

    ![Scheda "Global Settings" (Impostazioni globali)](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_002.png "Global Settings (Impostazioni globali)")

13. In hello **autenticazione federata** finestra di dialogo eseguire hello alla procedura seguente:

    ![Finestra di dialogo "Federated Authentication"(Autenticazione federata)](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_003.png "Federated Authentication (Autenticazione federata)")

    a. Selezionare **Enable Federated Authentication** (Abilita autenticazione federata).

    b. Fare clic su **caricare** tooupload il certificato scaricato.

    c. In hello **URL di accesso** , immettere il valore di hello di **SAML Single Sign-On Service URL** dalla finestra di configurazione dell'applicazione hello Azure AD.

    d. In hello **Sign-Out URL** , immettere il valore di hello di **Sign-Out URL** dalla finestra di configurazione dell'applicazione hello Azure AD.

    e. Selezionare **Utilizza POST**.

    f. Fare clic su **Save**.

### <a name="create-an-azure-ad-test-user"></a>Creare un utente test di Azure AD
Nel portale di Azure hello, creare un utente di test denominato Britta Simon.

![Nome e l'indirizzo e-mail dell'utente di prova hello Azure AD][100]

1. Nel portale di Azure, nel riquadro di sinistra hello, hello fare clic su hello **Azure Active Directory** icona.

    ![Icona Azure Active Directory](./media/active-directory-saas-clarizen-tutorial/create_aaduser_01.png)

2. Fare clic su **utenti e gruppi**, quindi fare clic su **tutti gli utenti** elenco hello toodisplay degli utenti.

    ![Clic su "Utenti e gruppi" e su "Tutti gli utenti"](./media/active-directory-saas-clarizen-tutorial/create_aaduser_02.png)

3. Nella parte superiore di hello della finestra di dialogo hello, fare clic su **Aggiungi** tooopen hello **utente** la finestra di dialogo.

    ![pulsante "Aggiungi" Hello](./media/active-directory-saas-clarizen-tutorial/create_aaduser_03.png)

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:

    ![Finestra di dialogo "Utente" con nome, indirizzo di posta elettronica e password inseriti](./media/active-directory-saas-clarizen-tutorial/create_aaduser_04.png)

    a. In hello **nome** digitare **BrittaSimon**.

    b. In hello **nome utente** casella Indirizzo di posta elettronica hello tipo di account di Britta Simon hello.

    c. Selezionare **Show Password** e annotare il valore di hello di **Password**.

    d. Fare clic su **Crea**.

### <a name="create-a-clarizen-test-user"></a>Creare un utente di test di Clarizen
tooenable toosign agli utenti di Azure AD in tooClarizen, è necessario eseguire il provisioning degli account utente. Nel caso di hello di Clarizen, il provisioning è un'attività manuale.

1. Accedi tooyour sito della società Clarizen come amministratore.

2. Fare clic su **Persone**.

    ![Clic su "People" (Persone)](./media/active-directory-saas-clarizen-tutorial/create_aaduser_001.png "People (Persone)")

3. Fare clic su **Invite User**.

    ![Pulsante "Invite User" (Invita l'utente)](./media/active-directory-saas-clarizen-tutorial/create_aaduser_002.png "Invitare utenti")

4. In hello **Invite People** finestra di dialogo eseguire hello alla procedura seguente:

    ![Finestra di dialogo "Invite People" (Invita persone)](./media/active-directory-saas-clarizen-tutorial/create_aaduser_003.png "Invite People (Invita persone)")

    a. In hello **posta elettronica** casella Indirizzo di posta elettronica hello tipo di account di Britta Simon hello.

    b. Fare clic su **Invita**.

    > [!NOTE]
    > titolare dell'account di Hello Azure Active Directory riceverà un messaggio di posta elettronica e seguire il proprio account tooconfirm un collegamento prima che diventi attivo.

### <a name="assign-hello-azure-ad-test-user"></a>Assegnare l'utente test hello Azure AD
Abilitare Britta Simon toouse single sign-on Azure concedendo tooClarizen proprio accesso.

![Utente di test assegnato][200]

1. Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello visualizzazione directory toohello browse, fare clic su **applicazioni aziendali**, quindi fare clic su **tutte le applicazioni**.

    ![Clic su "Applicazioni aziendali" e su "Tutte le applicazioni"][201]

2. Nell'elenco di applicazioni hello, selezionare **Clarizen**.

    ![Selezione di Clarizen nell'elenco di hello](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_50.png)

3. Nel riquadro di sinistra hello, fare clic su **utenti e gruppi**.

    ![Clic su "Utenti e gruppi"][202]

4. Fare clic su hello **Aggiungi** pulsante. Quindi, nel hello **Aggiungi** nella finestra di dialogo **utenti e gruppi**.

    ![pulsante "Aggiungi" Hello e finestra di dialogo "Aggiungi assegnazione" hello][203]

5. In hello **utenti e gruppi** nella finestra di dialogo **Britta Simon** elenco hello degli utenti.

6. In hello **utenti e gruppi** finestra di dialogo fare clic su hello **selezionare** pulsante.

7. In hello **Aggiungi** finestra di dialogo fare clic su hello **assegnare** pulsante.

### <a name="test-single-sign-on"></a>Testare l'accesso Single Sign-On
Test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.

Quando si fa clic su riquadro Clarizen hello in hello Pannello di accesso, devono essere connessi automaticamente tooyour applicazione Clarizen.

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sull'App SaaS toointegrate con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_203.png
