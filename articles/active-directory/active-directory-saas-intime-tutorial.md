---
title: 'Esercitazione: Integrazione di Azure Active Directory con InTime | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e InTime.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: d4e2c6e1-ae5d-4d2c-8ffc-1b24534d376a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: jeedes
ms.openlocfilehash: 63652f0f098aeac95e89a2500b46a18440e34698
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-intime"></a>Esercitazione: Integrazione di Azure Active Directory con InTime

In questa esercitazione, è illustrato come toointegrate InTime con Azure Active Directory (Azure AD).

Integrazione InTime con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooInTime.
- È possibile abilitare l'utenti tooautomatically get connesso tooInTime (Single Sign-On) con i propri account Azure AD.
- È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure.

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

integrazione di Azure AD con InTime tooconfigure, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione di InTime abilitata per l'accesso Single Sign-On

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di InTime dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-intime-from-hello-gallery"></a>Aggiunta di InTime dalla raccolta hello
integrazione hello tooconfigure di InTime in Azure AD, è necessario tooadd InTime dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd InTime dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![pulsante di Hello Azure Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Pannello di applicazioni Enterprise Hello][2]
    
3. tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.

    ![Nuovo pulsante dell'applicazione Hello][3]

4. Nella casella di ricerca hello, digitare **InTime**selezionare **InTime** dal pannello risultati quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.

    ![Nell'elenco risultati hello InTime](./media/active-directory-saas-intime-tutorial/tutorial_intime_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurare e testare l'accesso Single Sign-On di Azure AD

In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con InTime usando un utente di test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in InTime è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato hello InTime deve toobe stabilita.

In InTime, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.

tooconfigure e prova AD Azure single sign-on con InTime, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurare Azure Active Directory Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creare un utente prova AD Azure](#create-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creare un utente test InTime](#create-a-intime-test-user)**  -toohave un equivalente di Britta Simon in InTime che è la rappresentazione toohello collegato Azure AD dell'utente.
4. **[Assegnare l'utente test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Testare single sign-on](#test-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configure-azure-ad-single-sign-on"></a>Configurare l'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione InTime.

**Azure AD tooconfigure single sign-on con InTime, eseguire hello alla procedura seguente:**

1. Nel portale di Azure su hello hello **InTime** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Collegamento per la configurazione dell'accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-intime-tutorial/tutorial_intime_samlbase.png)

3. In hello **InTime dominio e gli URL** seguire hello alla procedura seguente:

    ![Informazioni su URL e dominio per l'accesso Single Sign-On di InTime](./media/active-directory-saas-intime-tutorial/tutorial_intime_url.png)

    a. In hello **Sign-on URL** casella di testo, digitare l'URL hello:`https://intime6.intimesoft.com/mytime/login/login.xhtml`

    b. In hello **identificatore** casella di testo, digitare l'URL hello:`https://auth.intimesoft.com/auth/realms/master`

4. In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.

    ![collegamento al download del certificato Hello](./media/active-directory-saas-intime-tutorial/tutorial_intime_certificate.png) 

5. L'applicazione InTime prevede asserzioni SAML hello in un formato specifico, che richiede di tooadd attributo personalizzato configurazione dei mapping tooyour SAML degli attributi del token. Hello seguente schermata mostra un esempio per questo oggetto. il valore predefinito di Hello **identificatore utente** è **User** ma InTime prevede che questo toobe mappato con indirizzo di posta elettronica dell'utente hello. A tale scopo è possibile utilizzare **user.mail** attributo dall'elenco hello o utilizzare il valore di attributo appropriato hello in base alla configurazione organizzazione 

    ![Configurazione dell'attributo](./media/active-directory-saas-intime-tutorial/tutorial_intime_attribute.png)

6. Fare clic sul pulsante **Salva** .

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-intime-tutorial/tutorial_general_400.png)

7. In hello **configurazione InTime** fare clic su **configurare InTime** tooopen **Configura sign-on** finestra. Hello copia **Sign-Out URL e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**

    ![Configurazione di InTime](./media/active-directory-saas-intime-tutorial/tutorial_intime_configure.png) 

8. tooconfigure single sign-on sul **InTime** lato, è necessario hello toosend scaricato **Metadata XML**, **Sign-Out URL e SAML Single Sign-On Service URL** troppo[Team di supporto inTime](mailto:hdollard@intimesoft.com). Impostano questo hello toohave impostazione connessione SAML SSO impostato correttamente su entrambi i lati.

> [!TIP]
> È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!  Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello. È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Creare un utente test di Azure AD

obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.

   ![Creare un utente test di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. Nel portale di Azure, nel riquadro di sinistra hello, hello fare clic su hello **Azure Active Directory** pulsante.

    ![pulsante di Hello Azure Active Directory](./media/active-directory-saas-intime-tutorial/create_aaduser_01.png)

2. elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi**, quindi fare clic su **tutti gli utenti**.

    ![Hello "Utenti e gruppi" e i collegamenti di "Tutti gli utenti"](./media/active-directory-saas-intime-tutorial/create_aaduser_02.png)

3. hello tooopen **utente** la finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello di hello **tutti gli utenti** la finestra di dialogo.

    ![pulsante Aggiungi Hello](./media/active-directory-saas-intime-tutorial/create_aaduser_03.png)

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:

    ![finestra di dialogo utente Hello](./media/active-directory-saas-intime-tutorial/create_aaduser_04.png)

    a. In hello **nome** digitare **BrittaSimon**.

    b. In hello **nome utente** casella Tipo hello di indirizzo di posta elettronica dell'utente Britta Simon.

    c. Seleziona hello **Show Password** casella di controllo e quindi annotare i valori hello visualizzati in hello **Password** casella.

    d. Fare clic su **Crea**.
 
### <a name="create-a-intime-test-user"></a>Creare un utente di test di InTime

In questa sezione viene creato un utente di nome Britta Simon in InTime. Lavorare con [team di supporto InTime](mailto:hdollard@intimesoft.com) utenti hello tooadd nella piattaforma InTime hello. Gli utenti devono essere creati e attivati prima di usare l'accesso Single Sign-On.

### <a name="assign-hello-azure-ad-test-user"></a>Assegnare l'utente test hello Azure AD

In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooInTime.

![Assegnazione del ruolo utente hello][200] 

**tooassign Britta Simon tooInTime, eseguire hello alla procedura seguente:**

1. Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **InTime**.

    ![Hello InTime collegamento nell'elenco delle applicazioni hello](./media/active-directory-saas-intime-tutorial/tutorial_intime_app.png)  

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![collegamento di "Utenti e gruppi" Hello][202]

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![riquadro assegnazione aggiungere Hello][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="test-single-sign-on"></a>Testare l'accesso Single Sign-On

In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.

Quando si fa clic sul riquadro InTime hello in hello Pannello di accesso, è necessario ottenere la pagina di accesso hello dell'applicazione InTime. Fare clic su hello **accesso** pulsante, una serie di IdPs sarà visualizzato in un elenco di pulsanti. Fare clic su **nome IDP** fornito da [team di supporto InTime](mailto:hdollard@intimesoft.com) toologin InTime nell'applicazione in uso. Per ulteriori informazioni sul pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-intime-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-intime-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-intime-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-intime-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-intime-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-intime-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-intime-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-intime-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-intime-tutorial/tutorial_general_203.png

