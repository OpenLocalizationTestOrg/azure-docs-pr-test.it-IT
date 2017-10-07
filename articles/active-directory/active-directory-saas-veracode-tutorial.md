---
title: 'Esercitazione: Integrazione di Azure Active Directory con Veracode | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Veracode.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 4fe78050-cb6d-4db9-96ec-58cc0779167f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: d17307b3864b7df8ee55f569d8f962e2e315b936
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-veracode"></a>Esercitazione: Integrazione di Azure Active Directory con Veracode

In questa esercitazione, è illustrato come toointegrate Veracode con Azure Active Directory (Azure AD).

Integrazione Veracode con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooVeracode.
- È possibile abilitare l'utenti tooautomatically get connesso tooVeracode (Single Sign-On) con i propri account Azure AD.
- È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure.

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

integrazione di Azure AD con Veracode tooconfigure, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione di Veracode abilitata per l'accesso Single Sign-On

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiungere Veracode dalla raccolta di hello
2. Configurare e testare l'accesso Single Sign-On di Azure AD

## <a name="add-veracode-from-hello-gallery"></a>Aggiungere Veracode dalla raccolta di hello
integrazione hello tooconfigure di Veracode in Azure AD, è necessario tooadd Veracode dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd Veracode dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![pulsante di Hello Azure Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Pannello di applicazioni Enterprise Hello][2]
    
3. tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.

    ![Nuovo pulsante dell'applicazione Hello][3]

4. Nella casella di ricerca hello, digitare **Veracode**selezionare **Veracode** dal pannello risultati quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.

    ![Nell'elenco risultati hello Veracode](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurare e testare l'accesso Single Sign-On di Azure AD

In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Veracode usando un utente di test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Veracode è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Veracode deve toobe stabilita.

In Veracode, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.

tooconfigure e prova AD Azure single sign-on con Veracode, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurare Azure Active Directory Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creare un utente prova AD Azure](#create-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creare un utente test Veracode](#create-a-veracode-test-user)**  -toohave un equivalente di Britta Simon in Veracode che è la rappresentazione toohello collegato Azure AD dell'utente.
4. **[Assegnare l'utente test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Testare single sign-on](#test-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configure-azure-ad-single-sign-on"></a>Configurare l'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Veracode.

**Azure AD tooconfigure single sign-on con Veracode, eseguire hello alla procedura seguente:**

1. Nel portale di Azure su hello hello **Veracode** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Collegamento per la configurazione dell'accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_samlbase.png)

3. In hello **Veracode dominio e gli URL** sezione, l'utente non dispone di tooperform tutte le operazioni di applicazione hello è già pre-integrata con Azure. 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_url.png)

4. In hello **certificato di firma SAML** fare clic su **certificato (Base64)** e quindi salvare il file di certificato hello nel computer in uso.

    ![collegamento al download del certificato Hello](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_certificate.png) 

5. obiettivo di Hello di questa sezione è toooutline come tooenable utenti tooauthenticate tooVeracode con il proprio account in Azure AD usando la federazione basata sul protocollo SAML hello.

    L'applicazione Veracode prevede asserzioni SAML hello in un formato specifico, che richiede il tooyour mapping di attributi personalizzati tooadd **attributi token saml** configurazione. Hello seguente schermata mostra un esempio per questo oggetto.
    
    ![Attributi](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_attr.png "Attributi")

6. mapping di attributi tooadd hello necessario, eseguire hello alla procedura seguente:

    | Nome attributo | Valore attributo |
    |--- |--- |
    | firstname |User.givenname |
    | lastname |User.surname |
    | email |User.mail |
    
    a. Per ogni riga di dati della tabella hello precedente, fare clic su **Aggiungi attributo utente**.
    
    ![Attributi](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr.png "Attributi")
    
    ![Attributi](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr1.png "Attributi")
    
    b. In hello **nome dell'attributo** casella di testo, nome dell'attributo di tipo hello mostrato per la riga.
    
    c. In hello **valore dell'attributo** casella di testo, il valore di attributo hello selezionare mostrato per la riga.
    
    d. Fare clic su **OK**.

7. Fare clic sul pulsante **Salva** .

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-veracode-tutorial/tutorial_general_400.png)

8. In hello **Veracode configurazione** fare clic su **configurare Veracode** tooopen **Configura sign-on** finestra. Hello copia **ID entità SAML** da hello **sezione di riferimento rapido.**

    ![Configurazione di Veracode](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_configure.png) 

9. In un'altra finestra del Web browser accedere al sito aziendale di Veracode come amministratore.

10. Scegliere hello menu in alto hello **impostazioni**, quindi fare clic su **Admin**.
   
    ![Amministrazione](./media/active-directory-saas-veracode-tutorial/ic802911.png "Amministrazione")

11. Fare clic su hello **SAML** scheda.

12. In hello **impostazioni SAML organizzazione** seguire hello alla procedura seguente:
   
    ![Amministrazione](./media/active-directory-saas-veracode-tutorial/ic802912.png "Amministrazione")
   
    a.  In **dell'autorità di certificazione** casella di testo, hello Incolla valore **ID entità SAML** che è stato copiato dal portale di Azure.
    
    b. il certificato scaricato dal portale di Azure, fare clic su tooupload **Scegli File**.
   
    c. Selezionare **Abilita la registrazione automatica**.

13. In hello **Impostazioni registrazione automatica** sezione, eseguire hello alla procedura seguente e quindi fare clic su **salvare**:
   
    ![Amministrazione](./media/active-directory-saas-veracode-tutorial/ic802913.png "Amministrazione")
   
    a. In **New User Activation** (Attivazione nuovo utente) selezionare **No Activation Required** (Nessuna attivazione richiesta).
   
    b. In **User Data Updates** (Aggiornamenti dati utenti) selezionare **Preference Veracode User Data** (Dati utenti Veracode di preferenza).
   
    c. Per **dettagli sugli attributi SAML**, selezionare hello seguenti:
      * **User Roles**
      * **Policy Administrator**
      * **Reviewer**
      * **Security Lead**
      * **Executive**
      * **Submitter**
      * **Creator**
      * **All Scan Types**
      * **Team Memberships**
      * **Default Team**

> [!TIP]
> È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!  Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello. È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Creare un utente test di Azure AD

obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.

   ![Creare un utente test di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. Nel portale di Azure, nel riquadro di sinistra hello, hello fare clic su hello **Azure Active Directory** pulsante.

    ![pulsante di Hello Azure Active Directory](./media/active-directory-saas-veracode-tutorial/create_aaduser_01.png)

2. elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi**, quindi fare clic su **tutti gli utenti**.

    ![Hello "Utenti e gruppi" e i collegamenti di "Tutti gli utenti"](./media/active-directory-saas-veracode-tutorial/create_aaduser_02.png)

3. hello tooopen **utente** la finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello di hello **tutti gli utenti** la finestra di dialogo.

    ![pulsante Aggiungi Hello](./media/active-directory-saas-veracode-tutorial/create_aaduser_03.png)

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:

    ![finestra di dialogo utente Hello](./media/active-directory-saas-veracode-tutorial/create_aaduser_04.png)

    a. In hello **nome** digitare **BrittaSimon**.

    b. In hello **nome utente** casella Tipo hello di indirizzo di posta elettronica dell'utente Britta Simon.

    c. Seleziona hello **Show Password** casella di controllo e quindi annotare i valori hello visualizzati in hello **Password** casella.

    d. Fare clic su **Crea**.
 
### <a name="create-a-veracode-test-user"></a>Creare un utente di test di Veracode
In ordine tooenable Azure AD utenti toolog in Veracode, è necessario eseguirne il provisioning in Veracode. Nel caso di hello di Veracode, il provisioning è un'attività automatica. Non è necessario eseguire alcuna operazione. Gli utenti vengono creati automaticamente se necessario, durante hello primo single sign-on tentativo.

> [!NOTE]
> È possibile usare qualsiasi altro Veracode utente account strumento di creazione o le API fornite da Veracode tooprovision degli account utente di Azure AD.
> 

### <a name="assign-hello-azure-ad-test-user"></a>Assegnare l'utente test hello Azure AD

In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooVeracode.

![Assegnazione del ruolo utente hello][200] 

**tooassign Britta Simon tooVeracode, eseguire hello alla procedura seguente:**

1. Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **Veracode**.

    ![collegamento Veracode Hello nell'elenco delle applicazioni hello](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_app.png)  

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![collegamento di "Utenti e gruppi" Hello][202]

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![riquadro assegnazione aggiungere Hello][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="test-single-sign-on"></a>Testare l'accesso Single Sign-On

In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.

Quando si fa clic su riquadro Veracode hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour Veracode applicazione.
Per ulteriori informazioni sul pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_203.png

