---
title: 'Esercitazione: Integrazione di Azure Active Directory con Perception United States (Non-UltiPro) | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e percezione United States (Non-UltiPro).
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: b4a8f026-cb5f-41eb-9680-68eddc33565e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 874b5da277b9c68504c4af2ac87ed90d2bbd93b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-perception-united-states-non-ultipro"></a>Esercitazione: Integrazione di Azure Active Directory con Perception United States (Non-UltiPro)

In questa esercitazione, è illustrato come toointegrate percezione italy (Non-UltiPro) con Azure Active Directory (Azure AD).

Integrazione percezione United States (Non-UltiPro) con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooPerception United States (Non-UltiPro).
- È possibile abilitare l'utenti tooautomatically get connesso tooPerception United States (Non-UltiPro) (Single Sign-On) con i propri account Azure AD.
- È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure.

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

integrazione di Azure AD con percezione United States (Non-UltiPro) tooconfigure, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione di Perception United States (Non-UltiPro) abilitata per l'accesso Single Sign-On

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di percezione United States (Non-UltiPro) dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-perception-united-states-non-ultipro-from-hello-gallery"></a>Aggiunta di percezione United States (Non-UltiPro) dalla raccolta hello
integrazione di hello di tooconfigure di percezione italy (Non-UltiPro) in Azure AD, è necessario tooadd percezione United States (Non-UltiPro) dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd percezione italy (Non-UltiPro) dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![pulsante di Hello Azure Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Pannello di applicazioni Enterprise Hello][2]
    
3. tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.

    ![Nuovo pulsante dell'applicazione Hello][3]

4. Nella casella di ricerca hello, digitare **percezione United States (Non-UltiPro)**selezionare **percezione United States (Non-UltiPro)** dal pannello risultati quindi fare clic su **Aggiungi** tooadd pulsante applicazione Hello.

    ![Stati Uniti di percezione (Non-UltiPro) nell'elenco risultati hello](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurare e testare l'accesso Single Sign-On di Azure AD

In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Perception United States (Non-UltiPro) usando un utente di test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello percezione United States (Non-UltiPro) è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato hello percezione United States (Non-UltiPro) richiede toobe stabilita.

Nella visualizzazione degli Stati Uniti (Non-UltiPro), assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.

tooconfigure e test di Azure AD single sign-on con percezione United States (Non-UltiPro), è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurare Azure Active Directory Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creare un utente prova AD Azure](#create-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creare un utente test percezione United States (Non-UltiPro)](#create-a-perception-united-states-non-ultipro-test-user)**  -toohave un equivalente di Britta Simon in percezione Stati Uniti (Non-UltiPro) che è la rappresentazione toohello collegato Azure AD dell'utente.
4. **[Assegnare l'utente test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Testare single sign-on](#test-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configure-azure-ad-single-sign-on"></a>Configurare l'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione percezione United States (Non-UltiPro).

**tooconfigure Azure AD accesso single sign-on con percezione United States (Non-UltiPro), eseguire hello alla procedura seguente:**

1. Nel portale di Azure su hello hello **percezione United States (Non-UltiPro)** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Collegamento per la configurazione dell'accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_samlbase.png)

3. In hello **dominio percezione United States (Non-UltiPro) e gli URL** seguire hello alla procedura seguente:

    ![Informazioni su URL e dominio per l'accesso Single Sign-On di Perception United States (Non-UltiPro)](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_url.png)

    a. In hello **identificatore** casella di testo, digitare l'URL hello:`https://perception.kanjoya.com/sp`

    b. In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://perception.kanjoya.com/sso?idp=<entity_id>`

    > [!NOTE] 
    > il valore di Hello non è di tipo real. È possibile aggiornare il valore di hello con URL risposta effettivo hello illustrato più avanti nell'esercitazione di hello.
 
4. In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.

    ![collegamento al download del certificato Hello](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_certificate.png) 

5. Fare clic sul pulsante **Salva** .

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_400.png)

6. In hello **configurazione percezione United States (Non-UltiPro)** fare clic su **configurare percezione United States (Non-UltiPro)** tooopen **Configura sign-on** finestra. Hello copia **ID entità SAML** da hello **sezione di riferimento rapido.**

    a. Hello **percezione United States (Non-UltiPro)** richiede l'applicazione hello **ID entità SAML** valore, che è stato copiato, toobe uri codificato. valore dell'uri con codificata hello tooget, seguente di hello utilizzo collegamento:**http://www.url-encode-decode.com/**.

    b. Dopo aver ottenuto l'uri di hello valore codificato si combinarla con hello **URL di risposta** come indicato di seguito

    `https://perception.kanjoya.com/sso?idp=<URI encooded entity_id>`
    
    c. Hello Incolla sopra valore hello **URL di risposta** nella casella di testo **dominio percezione United States (Non-UltiPro) e gli URL** sezione.

    ![Configurazione di Perception United States (Non-UltiPro)](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_configure.png) 

7. In un'altra finestra del browser, accedere come amministratore nel sito della società di tooyour percezione United States (Non-UltiPro).

8. Nella barra degli strumenti principale hello, fare clic su **impostazioni Account**.

    ![Utente di Perception United States (Non-UltiPro)](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_user.png)

9. In hello **impostazioni Account** eseguire hello alla procedura seguente:

    ![Utente di Perception United States (Non-UltiPro)](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_account.png)

    a. In hello **nome società** casella di testo, nome del tipo hello di hello **società**.
    
    b. In hello **nome Account** casella di testo, nome del tipo hello di hello **Account**.

    c. In **predefinito Reply-tooEmail** casella di testo, hello di tipo valido **posta elettronica**.

    d. Per **SSO Identity Provider** (Provider di identità SSO) selezionare **SAML 2.0**.

10. In hello **configurazione di SSO** eseguire hello alla procedura seguente:

    ![Configurazione SSO di Perception United States (Non-UltiPro)](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_ssoconfig.png)

    a. Per **SAML NameID Type** (Tipo ID nome SAML) selezionare **EMAIL** (POSTA ELETTRONICA).

    b. In hello **nome di configurazione di SSO** casella di testo, hello del tipo il **configurazione**.
    
    c. In **nome Provider di identità** casella di testo, hello Incolla valore **ID entità SAML**, che è stato copiato dal portale di Azure. 

    d. In **dominio SAML textbox**, immettere il dominio hello come  **@contoso.com** .

    e. Fare clic su **caricare nuovamente** hello tooupload **Metadata XML** file.

    f. Fare clic su **Update**.


> [!TIP]
> È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!  Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello. È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Creare un utente test di Azure AD

obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.

   ![Creare un utente test di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. Nel portale di Azure, nel riquadro di sinistra hello, hello fare clic su hello **Azure Active Directory** pulsante.

    ![pulsante di Hello Azure Active Directory](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_01.png)

2. elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi**, quindi fare clic su **tutti gli utenti**.

    ![Hello "Utenti e gruppi" e i collegamenti di "Tutti gli utenti"](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_02.png)

3. hello tooopen **utente** la finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello di hello **tutti gli utenti** la finestra di dialogo.

    ![pulsante Aggiungi Hello](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_03.png)

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:

    ![finestra di dialogo utente Hello](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_04.png)

    a. In hello **nome** digitare **BrittaSimon**.

    b. In hello **nome utente** casella Tipo hello di indirizzo di posta elettronica dell'utente Britta Simon.

    c. Seleziona hello **Show Password** casella di controllo e quindi annotare i valori hello visualizzati in hello **Password** casella.

    d. Fare clic su **Crea**.
  
### <a name="create-a-perception-united-states-non-ultipro-test-user"></a>Creare un utente di test di Perception United States (Non-UltiPro)

In questa sezione viene creato un utente di nome Britta Simon in Perception United States (Non-UltiPro). Lavorare con [team di supporto percezione United States (Non-UltiPro)](http://www.ultimatesoftware.com/Contact/ContactUs) utenti hello tooadd nella piattaforma di hello percezione United States (Non-UltiPro).

### <a name="assign-hello-azure-ad-test-user"></a>Assegnare l'utente test hello Azure AD

In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooPerception United States (Non-UltiPro).

![Assegnazione del ruolo utente hello][200] 

**tooassign Britta Simon tooPerception United States (Non-UltiPro), eseguire hello alla procedura seguente:**

1. Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **percezione United States (Non-UltiPro)**.

    ![collegamento di Hello percezione United States (Non-UltiPro) nell'elenco delle applicazioni hello](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_app.png)  

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![collegamento di "Utenti e gruppi" Hello][202]

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![riquadro assegnazione aggiungere Hello][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="test-single-sign-on"></a>Testare l'accesso Single Sign-On

In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.

Quando si fa clic su riquadro percezione United States (Non-UltiPro) hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour applicazione percezione United States (Non-UltiPro).
Per ulteriori informazioni sul pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_203.png

