---
title: 'Esercitazione: Integrazione di Azure Active Directory con LockPath Keyligh | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e LockPath Keylight.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 234a32f1-9f56-4650-9e31-7b38ad734b1a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: 5485aeb068ba6fbdb4ea9bfc89d401e00c5b1d29
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lockpath-keylight"></a>Esercitazione: Integrazione di Azure Active Directory con LockPath Keylight

In questa esercitazione, è illustrato come toointegrate LockPath Keylight con Azure Active Directory (Azure AD).

Integrazione LockPath Keylight con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooLockPath Keylight
- È possibile abilitare l'utenti tooautomatically get connesso tooLockPath Keylight (Single Sign-On) con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

integrazione di Azure AD con LockPath Keylight tooconfigure, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione di LockPath Keylight abilitata per l'accesso Single Sign-On

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di LockPath Keylight dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-lockpath-keylight-from-hello-gallery"></a>Aggiunta di LockPath Keylight dalla raccolta hello
integrazione hello tooconfigure di LockPath Keylight in Azure AD, è necessario tooadd LockPath Keylight dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd LockPath Keylight dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Applicazioni][2]
    
3. tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.

    ![Applicazioni][3]

4. Nella casella di ricerca hello, digitare **LockPath Keylight**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_search.png)

5. Nel riquadro dei risultati hello, selezionare **LockPath Keylight**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con LockPath Keylight in base a un utente test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in LockPath Keylight è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure AD e l'utente correlato di hello in LockPath Keylight deve toobe stabilita.

In LockPath Keylight, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.

tooconfigure e prova AD Azure single sign-on con LockPath Keylight, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creazione di un utente test LockPath Keylight](#creating-a-lockpath-keylight-test-user)**  -toohave un equivalente di Britta Simon in LockPath Keylight che è la rappresentazione toohello collegato Azure AD dell'utente.
4. **[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione LockPath Keylight.

**Azure AD tooconfigure single sign-on con LockPath Keylight, eseguire hello alla procedura seguente:**

1. Nel portale di Azure su hello hello **LockPath Keylight** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Configura accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_samlbase.png)

3. In hello **LockPath Keylight dominio e gli URL** seguire hello alla procedura seguente:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_url.png)

    a. In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<company name>.keylightgrc.com/`

    b. In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<company name>.keylightgrc.com`

    c. In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<company name>.keylightgrc.com/Login.aspx`
    
    > [!NOTE] 
    > Poiché questi non sono i valori reali, Aggiornare questi valori con hello effettivo identificatore, l'URL di risposta e URL Sign-On. Contatto [team di supporto Keylight Client LockPath](https://www.lockpath.com/contact/) tooget questi valori. 

4. In hello **certificato di firma SAML** fare clic su **Certificate(Raw)** e quindi salvare il file di certificato hello nel computer in uso.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_certificate.png) 

5. Fare clic sul pulsante **Salva** .

    ![Configura accesso Single Sign-On](./media/active-directory-saas-keylight-tutorial/tutorial_general_400.png)
    
6. In hello **LockPath Keylight configurazione** fare clic su **configurare LockPath Keylight** tooopen **Configura sign-on** finestra. Hello copia **Sign-Out URL e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**

    ![Configura accesso Single Sign-On](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_configure.png) 

7. tooenable SSO in LockPath Keylight, eseguire hello alla procedura seguente:
   
    a. Sign-on tooyour LockPath Keylight account come amministratore.
    
    b. Scegliere dal menu hello in primo piano hello **persona**e selezionare **Keylight installazione**.
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-keylight-tutorial/401.png) 

    c. Nella visualizzazione albero hello hello sinistra, fare clic su **SAML**.
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-keylight-tutorial/402.png) 

    d. In hello **impostazioni SAML** finestra di dialogo, fare clic su **modifica**.
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-keylight-tutorial/404.png) 

8. In hello **Modifica impostazioni di SAML** finestra di dialogo eseguire hello alla procedura seguente:
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-keylight-tutorial/405.png) 
   
    a. Impostare **SAML authentication** troppo**Active**.

    b. Hello Incolla **SAML Single Sign-On Service URL** valore a cui è stato copiato dal portale di Azure hello in hello **Identity Provider Login URL** casella di testo.

    c. Hello Incolla **URL del servizio Single Sign-Out** valore a cui è stato copiato dal portale di Azure hello in hello **Identity Provider Logout URL** casella di testo.

    d. Fare clic su **Scegli File** tooselect certificato i LockPath Keylight scaricato, quindi fare clic su **aprire** certificato hello tooupload.

    e. Impostare **Id utente SAML location** troppo**elemento NameIdentifier dell'istruzione subject hello**.
    
    f. Fornire hello **Provider del servizio Keylight** utilizzando hello seguente modello: **https://&lt;CompanyName&gt;. keylightgrc.com**.
    
    g. Impostare **agli utenti di eseguire il provisioning automatico** troppo**Active**.

    h. Impostare **il tipo di account di provisioning automatico** troppo**utente completa**.

    i. Impostare **Auto-provision security role** (Ruolo di sicurezza del provisioning automatico) selezionando **Standard User with SAML** (Utente standard con SAML).
    
    j. Impostare **Auto-provision security config** (Configurazione di sicurezza del provisioning automatico) selezionando **Standard User Configuration** (Configurazione utente standard).
     
    k. In hello **Email attribute** casella tipo `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.
    
    l. In hello **nome attributo** casella tipo `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.
    
    m. In hello **ultimo attributo nome** casella tipo `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.
    
    n. Fare clic su **Salva**.

> [!TIP]
> È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!  Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello. È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.

![Creare un utente di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-keylight-tutorial/create_aaduser_01.png) 

2. elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-keylight-tutorial/create_aaduser_02.png) 

3. hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-keylight-tutorial/create_aaduser_03.png) 

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-keylight-tutorial/create_aaduser_04.png) 

    a. In hello **nome** casella tipo **BrittaSimon**.

    b. In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Show Password** e annotare il valore di hello di hello **Password**.

    d. Fare clic su **Crea**.
 
### <a name="creating-a-lockpath-keylight-test-user"></a>Creazione di un utente test di LockPath Keylight

In questa sezione si crea un utente chiamato Britta Simon in LockPath Keylight. LockPath Keylight supporta il provisioning JIT, abilitato per impostazione predefinita.

Non è necessario alcun intervento dell'utente in questa sezione. Quando si accede a LockPath Keylight se utente hello non esiste ancora, viene creato un nuovo utente. 

>[!NOTE]
>Se è necessario un utente toocreate manualmente, è necessario hello toocontact [team di supporto Keylight Client LockPath](https://www.lockpath.com/contact/). 

### <a name="assigning-hello-azure-ad-test-user"></a>Assegnazione utente test hello Azure AD

In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooLockPath Keylight.

![Assegna utente][200] 

**tooassign Britta Simon tooLockPath Keylight, eseguire hello alla procedura seguente:**

1. Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **LockPath Keylight**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_app.png) 

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![Assegna utente][202] 

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.

Quando si fa clic hello LockPath Keylight riquadro in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour LockPath Keylight applicazione. 

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_203.png

