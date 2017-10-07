---
title: 'Esercitazione: Integrazione di Azure Active Directory con Hightail | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Hightail.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e15206ac-74b0-46e4-9329-892c7d242ec0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: jeedes
ms.openlocfilehash: 2b36fcf8d5773255fdf89de2dccdceb95c032bd8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hightail"></a>Esercitazione: Integrazione di Azure Active Directory con Hightail

In questa esercitazione, è illustrato come toointegrate Hightail con Azure Active Directory (Azure AD).

Integrazione Hightail con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooHightail
- È possibile abilitare l'utenti tooautomatically get connesso tooHightail (Single Sign-On) con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

integrazione di Azure AD con Hightail tooconfigure, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione di Hightail abilitata per l'accesso Single Sign-On

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di Hightail dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-hightail-from-hello-gallery"></a>Aggiunta di Hightail dalla raccolta hello
integrazione hello tooconfigure di Hightail in Azure AD, è necessario tooadd Hightail dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd Hightail dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Applicazioni][2]
    
3. tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.

    ![Applicazioni][3]

4. Nella casella di ricerca hello, digitare **Hightail**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_search.png)

5. Nel riquadro dei risultati hello, selezionare **Hightail**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Hightail mediante un utente test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Hightail è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Hightail deve toobe stabilita.

In Hightail, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.

tooconfigure e prova AD Azure single sign-on con Hightail, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creazione di un utente test Hightail](#creating-a-hightail-test-user)**  -toohave un equivalente di Britta Simon in Hightail che è la rappresentazione toohello collegato Azure AD dell'utente.
4. **[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Hightail.

**Azure AD tooconfigure single sign-on con Hightail, eseguire hello alla procedura seguente:**

1. Nel portale di Azure su hello hello **Hightail** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Configura accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_samlbase.png)

3. In hello **Hightail dominio e gli URL** seguire hello alla procedura seguente:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_url.png)

     In hello **URL di risposta** casella di testo, digitare l'URL hello come:`https://www.hightail.com/samlLogin?phi_action=app/samlLogin&subAction=handleSamlResponse`

    > [!NOTE] 
    > Hello valore precedente non è il valore reale. È possibile aggiornare il valore di hello con URL risposta effettivo hello illustrato più avanti nell'esercitazione di hello.
 
4. In hello **Hightail dominio e gli URL** sezione, se si desidera in un'applicazione hello tooconfigure **modalità iniziata da SP**, eseguire hello alla procedura seguente:
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_url1.png)

    a. Fare clic su hello **Mostra URL impostazioni avanzate**.

    b. In hello **URL di accesso** casella di testo, digitare l'URL hello come:`https://www.hightail.com/loginSSO`

4. In hello **certificato di firma SAML** fare clic su **certificato (Base64)** e quindi salvare il file di certificato hello nel computer in uso.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_certificate.png) 

5. Hightail asserzioni SAML hello prevista dall'applicazione in un formato specifico. Configurare hello seguendo le attestazioni per questa applicazione. È possibile gestire i valori hello di questi attributi da hello **"Atrribute"** scheda dell'applicazione hello. Hello seguente schermata mostra un esempio per questo oggetto. 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_attribute.png) 

6. In hello **gli attributi utente** sezione hello **Single sign-on** finestra di dialogo, configurare attributi token SAML, come illustrato nella figura hello ed eseguire hello alla procedura seguente:
    
    | Nome attributo | Valore attributo |
    | ------------------- | -------------------- |
    | FirstName | user.givenname |
    | LastName | user.surname |
    | Email | user.mail |    
    | UserIdentity | user.mail |
    
    a. Fare clic su **Aggiungi attributo** tooopen hello **Aggiungi attributo** finestra di dialogo.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hightail-tutorial/tutorial_officespace_04.png)

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hightail-tutorial/tutorial_officespace_05.png)

    b. In hello **nome** casella di testo, nome dell'attributo di tipo hello mostrato per la riga.

    c. Da hello **valore** elencare, valore dell'attributo di tipo hello mostrato per la riga.

    d. Lasciare hello **Namespace** vuoto.
    
    e. Fare clic su **OK**.

7. Fare clic sul pulsante **Salva** .

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hightail-tutorial/tutorial_general_400.png)

8. In hello **Hightail configurazione** fare clic su **configurare Hightail** tooopen **Configura sign-on** finestra. Hello copia **SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_configure.png) 

    >[!NOTE] 
    >Prima di configurare hello Single Sign-On in app Hightail, elenco approvato il dominio di posta elettronica con Hightail team in modo che tutti gli utenti che utilizzano questo dominio di hello possono utilizzare funzionalità Single Sign-On.


9. tooget SSO configurato per l'applicazione, è necessario toosign-on tooyour Hightail tenant come amministratore.
   
    a. Scegliere hello hello menu in alto hello **Account** e selezionare **configurare SAML**.
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_001.png) 

    b. Selezionare una casella di controllo hello **Abilita autenticazione SAML**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_002.png) 

    c. Aprire il certificato con codifica base 64 nel blocco note scaricato dal portale di Azure, hello copia del contenuto di esso negli Appunti e quindi incollarlo toohello **certificato di firma di Token SAML** casella di testo.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_003.png) 

    d. In hello **autorità SAML (Provider di identità)** casella di testo, hello Incolla valore **SAML Single Sign-On Service URL** copiata dal portale di Azure.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_004.png)

    e. Se si desidera in un'applicazione hello tooconfigure **modalità avviata da IDP** selezionare **"Provider di identità (IdP) avviato Accedi"**. Se si usa la **modalità avviata da SP**, selezionare **"Service Provider (SP) initiated log in"** ("Accesso avviato con provider di servizi (SP)").

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_006.png)

    f. Copiare l'URL di consumer hello SAML per l'istanza e incollarlo in **URL di risposta** nella casella di testo **Hightail dominio e gli URL** sezione nel portale di Azure.
    
    g. Fare clic su **Salva**.

> [!TIP]
> È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!  Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello. È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.

![Creare un utente di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-hightail-tutorial/create_aaduser_01.png) 

2. elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-hightail-tutorial/create_aaduser_02.png) 

3. hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-hightail-tutorial/create_aaduser_03.png) 

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-hightail-tutorial/create_aaduser_04.png) 

    a. In hello **nome** casella tipo **BrittaSimon**.

    b. In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Show Password** e annotare il valore di hello di hello **Password**.

    d. Fare clic su **Crea**.
 
### <a name="creating-a-hightail-test-user"></a>Creazione di un utente test di Hightail

obiettivo di Hello di questa sezione è un utente denominato Britta Simon in Hightail toocreate. 

Non è necessario alcun intervento dell'utente in questa sezione. Hightail supporta il provisioning utenti just-in-time in base alle attestazioni personalizzate hello. Se sono state configurate le attestazioni personalizzate hello, come illustrato nella sezione hello  **[configurazione Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  sopra, viene automaticamente creato un utente in un'applicazione hello non esiste ancora. 

>[!NOTE]
>Se è necessario un utente toocreate manualmente, è necessario hello toocontact [team di supporto Hightail](mailto:support@hightail.com). 

### <a name="assigning-hello-azure-ad-test-user"></a>Assegnazione utente test hello Azure AD

In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooHightail.

![Assegna utente][200] 

**tooassign Britta Simon tooHightail, eseguire hello alla procedura seguente:**

1. Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **Hightail**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_app.png) 

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![Assegna utente][202] 

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

obiettivo di Hello di questa sezione è tootest la configurazione di single sign-on di Azure AD mediante hello Pannello di accesso.

Quando si fa clic su riquadro Hightail hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour Hightail applicazione.


## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_203.png

