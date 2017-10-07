---
title: 'Esercitazione: Integrazione di Azure Active Directory con Adobe Creative Cloud | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Cloud creativi Adobe.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9ba1171e-56b1-4475-b308-58637d35e5a7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 5e66255e9785465974a23cd3ef79c24e28c0250f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adobe-creative-cloud"></a>Esercitazione: Integrazione di Azure Active Directory con Adobe Creative Cloud

In questa esercitazione, è illustrato come toointegrate Adobe Creative Cloud con Azure Active Directory (Azure AD).

Integrazione di Adobe Creative Cloud con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooAdobe Cloud creativi
- È possibile abilitare l'utenti tooautomatically get connesso tooAdobe Cloud creativi (Single Sign-On) con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale - portale di gestione di Azure hello

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

integrazione di Azure AD con Cloud creativi Adobe tooconfigure, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione di Adobe Creative Cloud abilitata per l'accesso Single Sign-On

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione, a meno che non sia necessario.
- Se non è disponibile un ambiente di prova di Azure AD, è possibile ottenere una versione di prova di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di Cloud creativi Adobe dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-adobe-creative-cloud-from-hello-gallery"></a>Aggiunta di Cloud creativi Adobe dalla raccolta hello
integrazione hello tooconfigure di Adobe Creative Cloud in Azure AD, è necessario tooadd Cloud creativi Adobe dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd Adobe Cloud creativi dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[il portale di gestione di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Applicazioni][2]
    
3. Fare clic su **Aggiungi** pulsante nella parte superiore di hello della finestra di dialogo hello.

    ![Applicazioni][3]

4. Nella casella di ricerca hello, digitare **Cloud creativi Adobe**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_000.png)

5. Nel riquadro dei risultati hello, selezionare **Cloud creativi Adobe**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_0001.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Adobe Creative Cloud con un utente test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Cloud creativi Adobe è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Cloud creativi Adobe deve toobe stabilita.

Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** nel Cloud creativi Adobe.

tooconfigure e test Azure single sign-on AD Adobe Creative cloud, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creazione di un utente test Cloud creativi Adobe](#creating-an-adobe-creative-cloud-test-user)**  -toohave un equivalente di Britta Simon in Adobe Creative Cloud rappresentazione toohello collegato Azure AD dell'utente.
4. **[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on nel portale di gestione di Azure hello e configurare l'accesso single sign-on nell'applicazione Cloud creativi Adobe.

**tooconfigure AD Azure single sign-on con Cloud creativi Adobe, eseguire hello alla procedura seguente:**

1. Nel portale di gestione di Azure hello in hello **Cloud creativi Adobe** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Configura accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo, come **modalità** selezionare **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_01.png)

3. In hello **Adobe Creative Cloud dominio e gli URL** seguire hello procedura seguente se si desidera in un'applicazione hello tooconfigure **IDP** modalità iniziata da:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_url1.png)

    a. In hello **identificatore** casella di testo, tipo di valore hello di:`https://www.okta.com/saml2/service-provider/<token>`

    b. In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<company name>.okta.com/auth/saml20/accauthlinktest`

    > [!NOTE] 
    > Si noti che queste non sono valori reali hello. È necessario tooupdate questi valori con URL di risposta e identificatore effettivo hello. In questo caso, è consigliabile si toouse hello valore univoco della stringa nell'identificatore hello. Se è necessario un utente toocreate manualmente, è necessario team di supporto Cloud creativi Adobe toocontact hello.

4. In hello **Adobe Creative Cloud dominio e gli URL** seguire hello procedura seguente se si desidera in un'applicazione hello tooconfigure **SP** modalità iniziata da:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_url2.png)

    a. Fare clic su hello **Mostra URL impostazioni avanzate** opzione

    b. In hello **Sign-on URL** casella di testo, tipo di valore hello di:`https://adobe.com`

5. In hello **certificato di firma SAML** fare clic su **certificato (Base64)** e quindi salvare il file di certificato hello nel computer in uso.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_05.png) 

6. In hello **configurazione Cloud creativi Adobe** fare clic su **Cloud creativi Adobe configurare** tooopen **Configura sign-on** finestra. Copiare hello **Id entità SAML** e **SAML SSO Service URL** dalla sezione di riferimento rapido.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_06.png) 

7. In una finestra del web browser, tenant Cloud creativi Adobe tooyour accesso come amministratore.

8.  Andare troppo**identità** hello riquadro di spostamento a sinistra e selezionare il dominio. Eseguire quindi seguire i passaggi di hello **Single Sign in configurazione necessario** sezione.

    ![Impostazioni](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_001.png "Impostazioni")

9. Fare clic su **Sfoglia** hello tooupload scaricato certificato da Azure AD troppo**IDP Certificate**.

10. In hello **IDP issuer** casella di testo, inserire il valore di hello di **Id entità SAML** che è stato copiato da **Configura sign-on** sezione nel portale di Azure.

11. In hello **IDP Login URL** casella di testo, inserire il valore di hello di **SAML SSO Service URL** che è stato copiato da **Configura sign-on** sezione nel portale di Azure.

12. Selezionare **HTTP - Redirect** (HTTP - Reindirizzamento) per **IDP Binding** (Binding IDP).

13. Selezionare **Email Address** (Indirizzo di posta elettronica) per **User Login Setting** (Impostazione accesso utente).
 
14. Fare clic sul pulsante **Salva** .

15. dashboard Hello mostrerà ora hello XML **"Scaricare i metadati"** file. che contiene l'URL EntityDescriptor e l'URL AssertionConsumerService di Adobe. Aprire file hello e configurarli nel hello applicazione Azure AD.

    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_002.png)

    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_003.png)

    a. Hello utilizzare EntityDescriptor valore Adobe fornita per **identificatore** su hello **Configura impostazioni App** finestra di dialogo.

    b. Hello utilizzare AssertionConsumerService valore Adobe fornita per **URL di risposta** su hello **Configura impostazioni App** finestra di dialogo.
 
### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
obiettivo di Hello di questa sezione è un utente di test nel portale di gestione di Azure hello chiamato Britta Simon toocreate.

![Creare un utente di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di gestione di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_01.png) 

2. Andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti** elenco hello toodisplay degli utenti.
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_02.png) 

3. Nella parte superiore di hello della finestra di dialogo hello fare clic su **Aggiungi** tooopen hello **utente** finestra di dialogo.
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_03.png) 

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_04.png) 

    a. In hello **nome** casella tipo **BrittaSimon**.

    b. In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Show Password** e annotare il valore di hello di hello **Password**.

    d. Fare clic su **Crea**. 

### <a name="creating-an-adobe-creative-cloud-test-user"></a>Creare un utente test di Adobe Creative Cloud

In ordine tooenable Azure AD utenti toolog in Cloud creativi Adobe, è necessario eseguirne il provisioning in Cloud creativi Adobe.  
Nel caso di hello di Cloud creativi Adobe, il provisioning è un'attività manuale.

**eseguire un account utente, tooprovision hello i passaggi seguenti:**

1. Accedi tooyour sito della società Adobe Creative Cloud come amministratore.

2. Fare clic su **Persone**.

    ![Persone](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_001.png "Persone")

3. Fare clic su **Invite User**.

    ![Invitare utenti](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_002.png "Invitare utenti")

4. In hello **Invite People** finestra di dialogo eseguire hello alla procedura seguente:

    ![Invitare persone](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_003.png "Invitare persone")

    a. In hello **posta elettronica** casella di testo, digitare hello indirizzo di posta elettronica dell'account di Britta Simon.
    
    b. Fare clic su **Invita**.

    > [!NOTE]
    > titolare dell'account di Hello Azure Active Directory riceverà un messaggio di posta elettronica e seguire il proprio account tooconfirm un collegamento prima che diventi attivo.

### <a name="assigning-hello-azure-ad-test-user"></a>Assegnazione utente test hello Azure AD

In questa sezione è abilitare Britta Simon toouse single sign-on Azure concedendo proprio tooAdobe accesso Cloud creativi.

![Assegna utente][200] 

**tooassign Britta Simon tooAdobe Cloud creativi, eseguire hello alla procedura seguente:**

1. Nel portale di gestione di Azure hello, aprire visualizzazione applicazioni hello, quindi selezionare la visualizzazione di directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **Cloud creativi Adobe**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_50.png) 

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![Assegna utente][202] 

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.

Quando si fa clic su riquadro Cloud creativi Adobe hello in hello Pannello di accesso, è necessario ottenere l'applicazione Cloud creativi Adobe tooyour automaticamente firmato-on.


## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_203.png