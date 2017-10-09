---
title: 'Esercitazione: Integrazione di Azure Active Directory con UserEcho | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e UserEcho.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bedd916b-8f69-4b50-9b8d-56f4ee3bd3ed
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: efe4a94ed6e5d22d153565d4782850eac4dff37b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-userecho"></a>Esercitazione: Integrazione di Azure Active Directory con UserEcho

In questa esercitazione, è illustrato come toointegrate UserEcho con Azure Active Directory (Azure AD).

Integrazione UserEcho con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooUserEcho
- È possibile abilitare l'utenti tooautomatically get connesso tooUserEcho (Single Sign-On) con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

integrazione di Azure AD con UserEcho tooconfigure, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione di UserEcho abilitata per l'accesso Single Sign-On

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese: [offerta prova](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di UserEcho dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-userecho-from-hello-gallery"></a>Aggiunta di UserEcho dalla raccolta hello
integrazione hello tooconfigure di UserEcho in Azure AD, è necessario tooadd UserEcho dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd UserEcho dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Applicazioni][2]
    
3. tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.

    ![Applicazioni][3]

4. Nella casella di ricerca hello, digitare **UserEcho**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_search.png)

5. Nel riquadro dei risultati hello, selezionare **UserEcho**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con UserEcho con un utente test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in UserEcho è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in UserEcho deve toobe stabilita.

In UserEcho, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.

tooconfigure e prova AD Azure single sign-on con UserEcho, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creazione di un utente test UserEcho](#creating-a-userecho-test-user)**  -toohave un equivalente di Britta Simon in UserEcho che è la rappresentazione toohello collegato Azure AD dell'utente.
4. **[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione UserEcho.

**Azure AD tooconfigure single sign-on con UserEcho, eseguire hello alla procedura seguente:**

1. Nel portale di Azure su hello hello **UserEcho** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Configura accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_samlbase.png)

3. In hello **UserEcho dominio e gli URL** seguire hello alla procedura seguente:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_url.png)

    a. In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<companyname>.userecho.com/`

    b. In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<companyname>.userecho.com/saml/metadata/`

    > [!NOTE] 
    > Poiché questi non sono i valori reali, Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore. Contatto [team di supporto UserEcho Client](https://feedback.userecho.com/) tooget questi valori. 

4. In hello **certificato di firma SAML** fare clic su **Certificate(Base64)** e quindi salvare il file di certificato hello nel computer in uso.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_certificate.png) 

5. Fare clic sul pulsante **Salva** .

    ![Configura accesso Single Sign-On](./media/active-directory-saas-userecho-tutorial/tutorial_general_400.png)

6. In hello **UserEcho configurazione** fare clic su **configurare UserEcho** tooopen **Configura sign-on** finestra. Hello copia **Sign-Out URL e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**

    ![Configura accesso Single Sign-On](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_configure.png) 

7. In un'altra finestra del browser, accedere come amministratore nel sito della società di tooyour UserEcho.

8. Nella barra degli strumenti hello in primo piano hello, fare clic su nel menu di hello tooexpand nome utente e quindi fare clic su **installazione**.
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_06.png) 

9. Fare clic su **Integrations**.
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_07.png) 

10. Fare clic su **Sito web** e quindi su **Single sign-on (SAML2)**.
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_08.png) 

11. In hello **Single sign-on (SAML)** eseguire hello alla procedura seguente:
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_09.png)
    
    a. Per **SAML-enabled** (Abilitato per SAML) selezionare **Sì**.
    
    b. Incolla **SAML Single Sign-On Service URL**, che è stato copiato dal portale di Azure hello in hello **URL SSO SAML** casella di testo.
    
    c. Incolla **Sign-Out URL**, che è stato copiato dal portale di Azure hello in hello **URL remoto logoout** casella di testo.
    
    d. Aprire il certificato scaricato nel blocco note, hello copia il contenuto e quindi incollarlo hello **certificato x. 509** casella di testo.
    
    e. Fare clic su **Salva**.

> [!TIP]
> È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!  Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello. È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.

![Creare un utente di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-userecho-tutorial/create_aaduser_01.png) 

2. elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-userecho-tutorial/create_aaduser_02.png) 

3. hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-userecho-tutorial/create_aaduser_03.png) 

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-userecho-tutorial/create_aaduser_04.png) 

    a. In hello **nome** casella tipo **BrittaSimon**.

    b. In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Show Password** e annotare il valore di hello di hello **Password**.

    d. Fare clic su **Crea**.
 
### <a name="creating-a-userecho-test-user"></a>Creazione di un utente test per UserEcho

obiettivo di Hello di questa sezione è un utente denominato Britta Simon in UserEcho toocreate.

**un utente denominato Britta Simon in UserEcho, toocreate eseguire hello alla procedura seguente:**

1. Sito dell'azienda UserEcho tooyour accesso come amministratore.

2. Nella barra degli strumenti hello in primo piano hello, fare clic su nel menu di hello tooexpand nome utente e quindi fare clic su **installazione**.
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_06.png)

3. Fare clic su **utenti**, hello tooexpand **utenti** sezione.
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_10.png)

4. Fare clic su **Users**.
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_11.png)

5. Fare clic su **Invite a new user**.
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_12.png)

6. In hello **invitare un nuovo utente** finestra di dialogo, eseguire hello alla procedura seguente:
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_13.png)

    a. In hello **nome** casella di testo, nome del tipo di utente hello come Britta Simon.
    
    b.  In hello **posta elettronica** casella di testo, digitare hello di indirizzo di posta elettronica dell'utente come Brittasimon@contoso.com.
    
    c. Fare clic su **Invita**.

TooBritta, consentendo la sua toostart utilizzando UserEcho viene inviato un invito. 

### <a name="assigning-hello-azure-ad-test-user"></a>Assegnazione utente test hello Azure AD

In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooUserEcho.

![Assegna utente][200] 

**tooassign Britta Simon tooUserEcho, eseguire hello alla procedura seguente:**

1. Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **UserEcho**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_app.png) 

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![Assegna utente][202] 

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

obiettivo di Hello di questa sezione è tootest la configurazione di SSO AD Azure utilizzando hello Pannello di accesso.  

Quando si fa clic su riquadro UserEcho hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour UserEcho applicazione.

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_203.png

