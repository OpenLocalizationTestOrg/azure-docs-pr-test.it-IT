---
title: 'Esercitazione: Integrazione di Azure Active Directory con PagerDuty | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e PagerDuty.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0410456a-76f7-42a7-9bb5-f767de75a0e0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: c3cfbedac3bf075e2d8cd833d5de7ca0bc9468b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pagerduty"></a>Esercitazione: integrazione di Azure Active Directory con PagerDuty

In questa esercitazione, è illustrato come toointegrate PagerDuty con Azure Active Directory (Azure AD).

Integrazione PagerDuty con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooPagerDuty
- È possibile abilitare l'utenti tooautomatically get connesso tooPagerDuty (Single Sign-On) con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

integrazione di Azure AD con PagerDuty tooconfigure, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione di PagerDuty abilitata per l'accesso Single Sign-On

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di PagerDuty dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-pagerduty-from-hello-gallery"></a>Aggiunta di PagerDuty dalla raccolta hello
integrazione hello tooconfigure di PagerDuty in Azure AD, è necessario tooadd PagerDuty dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd PagerDuty dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![pulsante di Hello Azure Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Pannello di applicazioni Enterprise Hello][2]
    
3. tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.

    ![Nuovo pulsante dell'applicazione Hello][3]

4. Nella casella di ricerca hello, digitare **PagerDuty**selezionare **PagerDuty** dal pannello risultati quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurare e testare l'accesso Single Sign-On di Azure AD

In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con PagerDuty in base a un utente test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in PagerDuty è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in PagerDuty deve toobe stabilita.

In PagerDuty, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.

tooconfigure e test Azure single sign-on AD con PagerDuty, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurare Azure Active Directory Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creare un utente prova AD Azure](#create-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creare un utente test PagerDuty](#create-a-pagerduty-test-user)**  -toohave un equivalente di Britta Simon in PagerDuty che è la rappresentazione toohello collegato Azure AD dell'utente.
4. **[Assegnare l'utente test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Testare Single Sign-On](#test-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configure-azure-ad-single-sign-on"></a>Configurare l'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione PagerDuty.

**Azure AD tooconfigure single sign-on con PagerDuty, eseguire hello alla procedura seguente:**

1. Nel portale di Azure su hello hello **PagerDuty** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Collegamento per la configurazione dell'accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_samlbase.png)

3. In hello **PagerDuty dominio e gli URL** seguire hello alla procedura seguente:

    ![Informazioni su URL e dominio per Single Sign-On di PagerDuty](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_url.png)

    a. In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<tenant-name>.pagerduty.com`

    b. In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<tenant-name>.pagerduty.com`

    > [!NOTE] 
    > Poiché questi non sono i valori reali, Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore. Contatto [team di supporto PagerDuty Client](https://www.pagerduty.com/support/) tooget questi valori. 

4. In hello **certificato di firma SAML** fare clic su **Certificate(Base64)** e quindi salvare il file di certificato hello nel computer in uso.

    ![collegamento al download del certificato Hello](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_certificate.png) 

5. Fare clic sul pulsante **Salva** .

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-pagerduty-tutorial/tutorial_general_400.png)

6. In hello **PagerDuty configurazione** fare clic su **configurare PagerDuty** tooopen **Configura sign-on** finestra. Hello copia **Sign-Out URL e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**

    ![Configurazione di PagerDuty](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_configure.png) 

7. In un'altra finestra del Web browser accedere al sito aziendale di Pagerduty come amministratore.

8. Scegliere dal menu hello in primo piano hello **impostazioni Account**.
   
    ![Impostazioni account](./media/active-directory-saas-pagerduty-tutorial/ic778535.png "Impostazioni account")

9. Fare clic su **Single Sign-On**.
   
    ![Single Sign-On](./media/active-directory-saas-pagerduty-tutorial/ic778536.png "Single Sign-On")

10. In hello **abilitare Single Sign-on (SSO)** eseguire hello alla procedura seguente:
   
    ![Abilitare l'accesso Single Sign-On](./media/active-directory-saas-pagerduty-tutorial/ic778537.png "Abilitare l'accesso Single Sign-On")
   
    a. Aprire il certificato con codifica base 64 scaricato dal portale di Azure nel blocco note, hello copia del contenuto di esso negli Appunti e quindi incollarlo toohello **certificato x. 509** casella di testo
  
    b. In hello **URL di accesso** casella di testo, incollare **SAML Single Sign-On Service URL** che è stato copiato dal portale di Azure.
  
    c. In hello **Logout URL** casella di testo, incollare **Sign-Out URL** che è stato copiato dal portale di Azure.
 
    d. Selezionare **Attiva Single Sign-on**.
 
    e. Fare clic su **Salva modifiche**.

> [!TIP]
> È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!  Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello. È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Creare un utente test di Azure AD

obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.

![Creare un utente test di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.

    ![pulsante di Hello Azure Active Directory](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_01.png) 

2. elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.
    
    ![Hello "Utenti e gruppi" e i collegamenti di "Tutti gli utenti"](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_02.png) 

3. hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.
 
    ![pulsante Aggiungi Hello](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_03.png) 

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:
 
    ![finestra di dialogo utente Hello](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_04.png) 

    a. In hello **nome** casella tipo **BrittaSimon**.

    b. In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Show Password** e annotare il valore di hello di hello **Password**.

    d. Fare clic su **Crea**.
 
### <a name="create-a-pagerduty-test-user"></a>Creare un utente test PagerDuty

toolog agli utenti di Azure AD tooenable in tooPagerDuty, è necessario eseguirne il provisioning in PagerDuty.  
Nel caso di hello di PagerDuty, il provisioning è un'attività manuale.

>[!NOTE]
>È possibile usare qualsiasi altro Pagerduty utente account strumento di creazione o le API fornite da Pagerduty tooprovision Azure Active Directory gli account utente.

**tooprovision un account utente, eseguire hello alla procedura seguente:**

1. Accedi tooyour **Pagerduty** tenant.

2. Scegliere dal menu hello in primo piano hello **utenti**.

3. Fare clic su **Aggiungi utenti**.
   
    ![Aggiungere utenti](./media/active-directory-saas-pagerduty-tutorial/ic778539.png "Aggiungere utenti")

4.  In hello **invito del team** finestra di dialogo, eseguire hello alla procedura seguente:
   
    ![Invitare il team](./media/active-directory-saas-pagerduty-tutorial/ic778540.png "Invitare il team")

    a. Hello tipo **First e Last Name** dell'utente come **Britta Simon**. 
   
    b. Immettere l'indirizzo **e-mail** univoco dell'utente, come **brittasimon@contoso.com**.
   
    c. Fare clic su **Add** (Aggiungi) e quindi su **Send Invites** (Invia inviti).
   
    >[!NOTE]
    >Tutti gli utenti aggiunti riceveranno un toocreate invito un account PagerDuty.

### <a name="assign-hello-azure-ad-test-user"></a>Assegnare l'utente test hello Azure AD

In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooPagerDuty.

![Assegnazione del ruolo utente hello][200]

**tooassign Britta Simon tooPagerDuty, eseguire hello alla procedura seguente:**

1. Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **PagerDuty**.

    ![collegamento PagerDuty Hello nell'elenco delle applicazioni hello](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_app.png) 

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![collegamento di "Utenti e gruppi" Hello][202]

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![riquadro assegnazione aggiungere Hello][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="test-single-sign-on"></a>Testare l'accesso Single Sign-On

In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.

Quando fa clic su riquadro PagerDuty hello in hello Panelyou di accesso deve ottenere automaticamente firmato in tooyour PagerDuty applicazione.

Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_203.png

