---
title: 'Esercitazione: Integrazione di Azure Active Directory con ThousandEyes | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e ThousandEyes.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 790e3f1e-1591-4dd6-87df-590b7bf8b4ba
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/15/2017
ms.author: jeedes
ms.openlocfilehash: fbfbfb71809355b1b138762757a851907737730b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-thousandeyes"></a>Esercitazione: Integrazione di Azure Active Directory con ThousandEyes

In questa esercitazione, è illustrato come toointegrate ThousandEyes con Azure Active Directory (Azure AD).

Integrazione di ThousandEyes con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooThousandEyes
- È possibile abilitare l'utenti tooautomatically get connesso tooThousandEyes (Single Sign-On) con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

integrazione di Azure AD con ThousandEyes tooconfigure, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Una sottoscrizione di ThousandEyes abilitata per l'accesso Single Sign-On

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese: [offerta prova](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di ThousandEyes dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-thousandeyes-from-hello-gallery"></a>Aggiunta di ThousandEyes dalla raccolta hello
integrazione hello tooconfigure di ThousandEyes in Azure AD, è necessario tooadd ThousandEyes dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd ThousandEyes dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Applicazioni][2]
    
3. tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.

    ![Applicazioni][3]

4. Nella casella di ricerca hello, digitare **ThousandEyes**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_search.png)

5. Nel riquadro dei risultati hello, selezionare **ThousandEyes**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con ThousandEyes usando un utente di test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in ThousandEyes è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in ThousandEyes deve toobe stabilita.

In ThousandEyes, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.

tooconfigure e prova AD Azure single sign-on con ThousandEyes, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creazione di un utente test ThousandEyes](#creating-a-thousandeyes-test-user)**  -toohave un equivalente di Britta Simon in ThousandEyes che è la rappresentazione toohello collegato Azure AD dell'utente.
4. **[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione ThousandEyes.

**Azure AD tooconfigure single sign-on con ThousandEyes, eseguire hello alla procedura seguente:**

1. Nel portale di Azure su hello hello **ThousandEyes** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Configura accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_samlbase.png)

3. In hello **ThousandEyes dominio e gli URL** seguire hello alla procedura seguente:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_url.png)

    In hello **Sign-on URL** casella di testo, digitare un URL come:`https://app.thousandeyes.com/login/sso`

4. In hello **certificato di firma SAML** fare clic su **Certificate(Base64)** e quindi salvare il file di certificato hello nel computer in uso.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_certificate.png) 

5. Fare clic sul pulsante **Salva** .

    ![Configura accesso Single Sign-On](./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_400.png)

6. In hello **ThousandEyes configurazione** fare clic su **configurare ThousandEyes** tooopen **Configura sign-on** finestra. Hello copia **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**

    ![Configura accesso Single Sign-On](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_configure.png) 

7. In una finestra del web browser, accedere tooyour **ThousandEyes** sito aziendale come amministratore.

8. Scegliere dal menu hello in primo piano hello **impostazioni**.
   
    ![Impostazioni](./media/active-directory-saas-thousandeyes-tutorial/ic790066.png "Impostazioni")

9. Fare clic su **Account**
   
    ![Account](./media/active-directory-saas-thousandeyes-tutorial/ic790067.png "Account")

10. Fare clic su hello **sicurezza e autenticazione** scheda.
   
    ![Sicurezza e autenticazione](./media/active-directory-saas-thousandeyes-tutorial/ic790068.png "Security e autenticazione")

11. In hello **Setup Single Sign-On** seguire hello alla procedura seguente:
   
    ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-thousandeyes-tutorial/ic790069.png "Configurare l'accesso Single Sign-On")
  
    a. Selezionare **Enable Single Sign-On**.
  
    b. Nella casella di testo **Login Page URL** (URL pagina di accesso) incollare il valore dell'**URL del servizio Single Sign-On SAML** copiato dal portale di Azure.
  
    c. Nella casella di testo **Logout Page URL** (URL pagina di disconnessione) incollare il valore dell'**URL di disconnessione** copiato dal portale di Azure.
  
    d. Nella casella di testo **Autorità di certificazione del provider di identità** incollare l'**ID di entità SAML** copiato dal portale di Azure.
  
    e. In **certificato di verifica**, fare clic su **Choose file**e quindi caricare il certificato di hello scaricato dal portale di Azure.
  
    f. Fare clic su **Salva**.
 
> [!TIP]
> È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!  Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello. È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.

![Creare un utente di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_01.png) 

2. elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_02.png) 

3. hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_03.png) 

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_04.png) 

    a. In hello **nome** casella tipo **BrittaSimon**.

    b. In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Show Password** e annotare il valore di hello di hello **Password**.

    d. Fare clic su **Crea**.
 
### <a name="creating-a-thousandeyes-test-user"></a>Creazione di un utente di test di ThousandEyes

In ordine tooenable Azure AD utenti toolog a ThousandEyes, è necessario eseguirne il provisioning in ThousandEyes.  
Nel caso di hello di ThousandEyes, il provisioning è un'attività manuale.

>[!NOTE]
>È possibile usare qualsiasi altro ThousandEyes utente account strumento di creazione o le API fornite da ThousandEyes tooprovision Azure Active Directory gli account utente.

**tooprovision tooThousandEyes un account utente, eseguire hello alla procedura seguente:**

1. Accedere al sito aziendale di ThousandEyes come amministratore.

2. Fare clic su **Impostazioni**.
   
    ![Impostazioni](./media/active-directory-saas-thousandeyes-tutorial/IC790066.png "Impostazioni")

3. Fare clic su **Account**.
   
    ![Account](./media/active-directory-saas-thousandeyes-tutorial/IC790067.png "Account")

4. Fare clic su hello **account e utenti** scheda.
   
    ![Account e utenti](./media/active-directory-saas-thousandeyes-tutorial/IC790073.png "Account e utenti")

5. In hello **aggiungere utenti e account** seguire hello alla procedura seguente:
   
    ![Aggiungere account utente](./media/active-directory-saas-thousandeyes-tutorial/IC790074.png "Aggiungere account utente")   
  
    a. In **nome** casella di testo Nome hello del tipo di utente come **Britta Simon**.

    b. In **posta elettronica** casella Tipo hello email dell'utente come  **brittasimon@contoso.com** .
   
    b. Fare clic su **tooAccount Add New User**.
      
     >[!NOTE]
     >titolare dell'account di Azure Active Directory Hello otterrà un messaggio di posta elettronica inclusi tooconfirm un collegamento e attivare hello account.

### <a name="assigning-hello-azure-ad-test-user"></a>Assegnazione utente test hello Azure AD

In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooThousandEyes.

![Assegna utente][200] 

**tooassign Britta Simon tooThousandEyes, eseguire hello alla procedura seguente:**

1. Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **ThousandEyes**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_app.png) 

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![Assegna utente][202] 

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.

Quando si fa clic hello ThousandEyes riquadro in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour applicazione ThousandEyes.

Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_203.png

