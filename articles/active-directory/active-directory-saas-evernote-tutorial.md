---
title: 'Esercitazione: Integrazione di Azure Active Directory con Evernote | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory ed Evernote.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 4d7017e571ed12a0b155aa188c6b0ecb3c9898a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-evernote"></a>Esercitazione: Integrazione di Azure Active Directory con Evernote

In questa esercitazione, è illustrato come toointegrate Evernote con Azure Active Directory (Azure AD).

Integrazione Evernote con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooEvernote.
- È possibile abilitare l'utenti tooautomatically get connesso tooEvernote (Single Sign-On) con i propri account Azure AD.
- È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure.

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

integrazione di Azure AD con Evernote tooconfigure, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione di Evernote abilitata per l'accesso Single Sign-On.

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di Evernote dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-evernote-from-hello-gallery"></a>Aggiunta di Evernote dalla raccolta hello
integrazione hello tooconfigure di Evernote in Azure AD, è necessario tooadd Evernote dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd Evernote dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![pulsante di Hello Azure Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Pannello di applicazioni Enterprise Hello][2]
    
3. tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.

    ![Nuovo pulsante dell'applicazione Hello][3]

4. Nella casella di ricerca hello, digitare **Evernote**selezionare **Evernote** dal pannello risultati quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.

    ![Nell'elenco risultati hello Evernote](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurare e testare l'accesso Single Sign-On di Azure AD

In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Evernote in base a un utente test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Evernote è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Evernote deve toobe stabilita.

In Evernote, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.

tooconfigure e prova AD Azure single sign-on con Evernote, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurare Azure Active Directory Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creare un utente prova AD Azure](#create-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creare un utente test Evernote](#create-an-evernote-test-user)**  -toohave un equivalente di Britta Simon in Evernote che è la rappresentazione toohello collegato Azure AD dell'utente.
4. **[Assegnare l'utente test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Testare single sign-on](#test-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configure-azure-ad-single-sign-on"></a>Configurare l'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Evernote.

**Azure AD tooconfigure single sign-on con Evernote, eseguire hello alla procedura seguente:**

1. Nel portale di Azure su hello hello **Evernote** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Collegamento per la configurazione dell'accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_samlbase.png)

3. In hello **Evernote dominio e gli URL** seguire passaggi se si desidera modalità iniziata da un'applicazione hello tooconfigure in IDP hello:

    ![Informazioni su URL e dominio per Single Sign-On di Evernote](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_url.png)

    In hello **identificatore** casella di testo, digitare l'URL hello:`https://www.evernote.com/saml2`

4. Controllare **Mostra URL impostazioni avanzate** ed eseguire hello riportata dopo il passaggio se si desidera in un'applicazione hello tooconfigure **SP** modalità iniziata da:

    ![Informazioni su URL e dominio per Single Sign-On di Evernote](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_url1.png)

    In hello **URL di accesso** casella di testo, digitare l'URL hello:`https://www.evernote.com/Login.action`   

5. In hello **certificato di firma SAML** fare clic su **Certificate(Base64)** e quindi salvare il file di certificato hello nel computer in uso.

    ![collegamento al download del certificato Hello](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_certificate.png) 

6. Fare clic sul pulsante **Salva** .

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-evernote-tutorial/tutorial_general_400.png)

7. In hello **Evernote configurazione** fare clic su **configurare Evernote** tooopen **Configura sign-on** finestra. Hello copia **SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**

    ![Configurazione di Evernote](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_configure.png) 

8. In un'altra finestra del Web browser accedere al sito aziendale di Evernote come amministratore.

9. Andare troppo**'Console di amministrazione di '**

    ![Admin-Console](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_adminconsole.png)

10. Da hello **'Console di amministrazione'**, andare troppo**'Security'** e selezionare **' Single Sign-On'**

    ![SSO-Setting](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_sso.png)

11. Configurare hello seguenti valori:

    ![Certificate-Setting](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_certx.png)
    
    a.  **Abilitare SSO:** SSO è abilitato per impostazione predefinita (fare clic su **disabilitare Single Sign-on** requisito di SSO hello tooremove)

    b. Incolla **SAML Single sign-on Service URL** valore, che è stato copiato dal portale di Azure hello in hello **URL di richiesta HTTP SAML** casella di testo.

    c. Aprire certificato scaricato hello da Azure AD in un contenuto di hello in blocco note e copiare inclusi "BEGIN" e "Fine certificato" e incollarlo in hello **certificato x. 509** casella di testo. 

    Fare clic su **Save Changes** (Salva modifiche).

> [!TIP]
> È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!  Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello. È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Creare un utente test di Azure AD

obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.

   ![Creare un utente test di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. Nel portale di Azure, nel riquadro di sinistra hello, hello fare clic su hello **Azure Active Directory** pulsante.

    ![pulsante di Hello Azure Active Directory](./media/active-directory-saas-evernote-tutorial/create_aaduser_01.png)

2. elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi**, quindi fare clic su **tutti gli utenti**.

    ![Hello "Utenti e gruppi" e i collegamenti di "Tutti gli utenti"](./media/active-directory-saas-evernote-tutorial/create_aaduser_02.png)

3. hello tooopen **utente** la finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello di hello **tutti gli utenti** la finestra di dialogo.

    ![pulsante Aggiungi Hello](./media/active-directory-saas-evernote-tutorial/create_aaduser_03.png)

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:

    ![finestra di dialogo utente Hello](./media/active-directory-saas-evernote-tutorial/create_aaduser_04.png)

    a. In hello **nome** digitare **BrittaSimon**.

    b. In hello **nome utente** casella Tipo hello di indirizzo di posta elettronica dell'utente Britta Simon.

    c. Seleziona hello **Show Password** casella di controllo e quindi annotare i valori hello visualizzati in hello **Password** casella.

    d. Fare clic su **Crea**.
 
### <a name="create-an-evernote-test-user"></a>Creare un utente test di Evernote

In ordine tooenable Azure AD utenti toolog in Evernote, è necessario eseguirne il provisioning in Evernote.  
Nel caso di hello di Evernote, il provisioning è un'attività manuale.

**eseguire un account utente, tooprovision hello i passaggi seguenti:**

1. Accedi tooyour sito della società Evernote come amministratore.

2. Fare clic su hello **'Console di amministrazione'**.

    ![Admin-Console](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_adminconsole.png)

3. Da hello **'Console di amministrazione'**, andare troppo**'Aggiungi utenti'**.

    ![Add-testUser](./media/active-directory-saas-evernote-tutorial/create_aaduser_0001.png)

4. **Aggiungere membri del team** in hello **posta elettronica** casella di testo, digitare l'indirizzo di posta elettronica hello dell'account utente e fare clic su **dell'invito.**

    ![Add-testUser](./media/active-directory-saas-evernote-tutorial/create_aaduser_0002.png)
    
5. Dopo che viene inviato l'invito, titolare dell'account di Azure Active Directory hello riceveranno un invito di hello tooaccept di posta elettronica.

### <a name="assign-hello-azure-ad-test-user"></a>Assegnare l'utente test hello Azure AD

In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooEvernote.

![Assegnazione del ruolo utente hello][200] 

**tooassign Britta Simon tooEvernote, eseguire hello alla procedura seguente:**

1. Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **Evernote**.

    ![collegamento Evernote Hello nell'elenco delle applicazioni hello](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_app.png)  

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![collegamento di "Utenti e gruppi" Hello][202]

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![riquadro assegnazione aggiungere Hello][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="test-single-sign-on"></a>Testare l'accesso Single Sign-On

In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.

Quando si fa clic su riquadro Evernote hello in hello Pannello di accesso, è necessario ottenere connesso tooyour Evernote applicazione. Sarà possibile registrazione come un account aziendale ma toolog necessario con l'account personale. 

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_203.png

