---
title: 'Esercitazione: Integrazione di Azure Active Directory con TOPdesk - Public |Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e TOPdesk - Public.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0873299f-ce70-457b-addc-e57c5801275f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: ef0dd06157ecc3b33814590039f5cbae64e8c916
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-topdesk---public"></a>Esercitazione: Integrazione di Azure Active Directory con TOPdesk - Public

In questa esercitazione, è illustrato come toointegrate TOPdesk - Public con Azure Active Directory (Azure AD).

L'integrazione di TOPdesk - Public con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooTOPdesk - pubblico.
- È possibile abilitare l'utenti tooautomatically get connesso tooTOPdesk - Public (Single Sign-On) con i propri account Azure AD.
- È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure.

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

tooconfigure integrazione di Azure Active Directory con TOPdesk - Public, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione di TOPdesk - Public abilitata per l'accesso Single Sign-On

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di TOPdesk - Public dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-topdesk---public-from-hello-gallery"></a>Aggiunta di TOPdesk - Public dalla raccolta hello
integrazione di hello tooconfigure di TOPdesk - Public in Azure AD, è necessario tooadd TOPdesk - Public dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd TOPdesk - Public dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![pulsante di Hello Azure Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Pannello di applicazioni Enterprise Hello][2]
    
3. tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.

    ![Nuovo pulsante dell'applicazione Hello][3]

4. Nella casella di ricerca hello, digitare **TOPdesk - Public**selezionare **TOPdesk - Public** dal pannello risultati quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.

    ![Nell'elenco dei risultati di TOPdesk - Public in hello](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurare e testare l'accesso Single Sign-On di Azure AD

In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con TOPdesk - Public usando un utente di test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in TOPdesk - Public tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in TOPdesk - Public richiede toobe stabilita.

In TOPdesk - Public, assegnare un valore di hello hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.

tooconfigure e testare Azure AD single sign-on con TOPdesk - Public, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurare Azure Active Directory Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creare un utente prova AD Azure](#create-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creare un TOPdesk - pubblico test utente](#create-a-topdesk---public-test-user)**  - toohave un equivalente di Britta Simon in TOPdesk - pubblico che è la rappresentazione toohello collegato Azure AD dell'utente.
4. **[Assegnare l'utente test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Testare single sign-on](#test-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configure-azure-ad-single-sign-on"></a>Configurare l'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on in TOPdesk - Public applicazione.

**tooconfigure AD Azure single sign-on con TOPdesk - Public, eseguire hello alla procedura seguente:**

1. Nel portale di Azure su hello hello **TOPdesk - Public** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Collegamento per la configurazione dell'accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_samlbase.png)

3. In hello **TOPdesk - URL e dominio pubblico** seguire hello alla procedura seguente:

    ![Informazioni sull'accesso Single Sign-On per URL e dominio di TOPdesk - Public](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_url.png)

    a. In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<companyname>.topdesk.net`
    
    b. In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<companyname>.topdesk.net/tas/public/login/verify`

    c. In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<companyname>.topdesk.net/tas/public/login/saml`
     
    > [!NOTE] 
    > Poiché questi non sono i valori reali, Aggiornare questi valori con hello effettivo identificatore, l'URL di risposta e URL Sign-On. L'URL di risposta è descritto più avanti nell'esercitazione. Contatto [TOPdesk - team di supporto Client pubblico](https://help.topdesk.com/saas/enterprise/user/) tooget questi valori.  

4. In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.

    ![collegamento al download del certificato Hello](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_certificate.png) 

5. Fare clic sul pulsante **Salva** .

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_400.png)
    
6. In hello **TOPdesk - Public configurazione** fare clic su **configurare TOPdesk - Public** tooopen **Configura sign-on** finestra. Hello copia **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**

    ![Configurazione di TOPdesk - Public](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_configure.png) 

7. Accesso tooyour **TOPdesk - Public** sito aziendale come amministratore.

8. In hello **TOPdesk** menu, fare clic su **impostazioni**.
   
    ![Impostazioni](./media/active-directory-saas-topdesk-public-tutorial/ic790598.png "Impostazioni")

9. Fare clic su **Login Settings**.
   
    ![Login Settings](./media/active-directory-saas-topdesk-public-tutorial/ic790599.png "Login Settings")

10. Espandere hello **impostazioni di accesso** menu e quindi fare clic su **generale**.
   
    ![General](./media/active-directory-saas-topdesk-public-tutorial/ic790600.png "General")

11. In hello **pubblica** sezione di hello **SAML login** configurazione seguire hello alla procedura seguente:
   
    ![Technical Settings](./media/active-directory-saas-topdesk-public-tutorial/ic790601.png "Technical Settings")
   
    a. Fare clic su **scaricare** toodownload hello file di metadati pubblici e quindi salvarlo in locale nel computer in uso.
   
    b. Aprire il file di metadati scaricato hello e individuare hello **AssertionConsumerService** nodo.

    ![AssertionConsumerService](./media/active-directory-saas-topdesk-public-tutorial/ic790619.png "AssertionConsumerService")
   
    c. Hello copia **AssertionConsumerService** valore, incollare il valore in hello **URL di risposta** nella casella di testo **TOPdesk - URL e dominio pubblico** sezione.      
   
12. toocreate un file di certificato, eseguire hello alla procedura seguente:
    
    ![Certificate](./media/active-directory-saas-topdesk-public-tutorial/ic790606.png "Certificate")
    
    a. Aprire hello scaricata file di metadati dal portale Azure.
    
    b. Espandere hello **RoleDescriptor** nodo che dispone di un **xsi: Type** di **fed: ApplicationServiceType**.
    
    c. Copiare il valore di hello di hello **X509Certificate** nodo.
    
    d. Salva hello copiato **X509Certificate** valore in locale nel computer in un file.

13. In hello **pubblica** fare clic su **Aggiungi**.
    
    ![Login SAML](./media/active-directory-saas-topdesk-public-tutorial/ic790625.png "Login SAML")

14. In hello **Assistente configurazione SAML** finestra di dialogo eseguire hello alla procedura seguente:
    
    ![SAML Configuration Assistant](./media/active-directory-saas-topdesk-public-tutorial/ic790608.png "SAML Configuration Assistant")
    
    a. tooupload i metadati scaricati file dal portale di Azure in **i metadati della federazione**, fare clic su **Sfoglia**.

    b. file del certificato, in tooupload **Certificate (RSA)**, fare clic su **Sfoglia**.

    c. file del logo hello tooupload ottenuto dal team di supporto di TOPdesk hello, in **icona del Logo**, fare clic su **Sfoglia**.

    d. In hello **attributo nome utente** casella tipo `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.

    e. In hello **nome visualizzato** casella di testo, digitare un nome per la configurazione.

    f. Fare clic su **Salva**.

> [!TIP]
> È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!  Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello. È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Creare un utente test di Azure AD

obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.

   ![Creare un utente test di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. Nel portale di Azure, nel riquadro di sinistra hello, hello fare clic su hello **Azure Active Directory** pulsante.

    ![pulsante di Hello Azure Active Directory](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_01.png)

2. elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi**, quindi fare clic su **tutti gli utenti**.

    ![Hello "Utenti e gruppi" e i collegamenti di "Tutti gli utenti"](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_02.png)

3. hello tooopen **utente** la finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello di hello **tutti gli utenti** la finestra di dialogo.

    ![pulsante Aggiungi Hello](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_03.png)

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:

    ![finestra di dialogo utente Hello](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_04.png)

    a. In hello **nome** digitare **BrittaSimon**.

    b. In hello **nome utente** casella Tipo hello di indirizzo di posta elettronica dell'utente Britta Simon.

    c. Seleziona hello **Show Password** casella di controllo e quindi annotare i valori hello visualizzati in hello **Password** casella.

    d. Fare clic su **Crea**.
 
### <a name="create-a-topdesk---public-test-user"></a>Creare un utente di test di TOPdesk - Public

In ordine tooenable Azure AD utenti toolog TopDesk - Public, è necessario eseguirne il provisioning in TOPdesk - Public.  
Nel caso di hello di TOPdesk - Public, il provisioning è un'attività manuale.

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a>tooconfigure provisioning degli utenti, eseguire hello alla procedura seguente:
1. Accesso tooyour **TOPdesk - Public** sito aziendale come amministratore.

2. Scegliere dal menu hello in primo piano hello **TOPdesk \> New \> i file di supporto \> persona**.
   
    ![Person](./media/active-directory-saas-topdesk-public-tutorial/ic790628.png "Person")

3. Nella finestra di dialogo nuova persona hello eseguire hello alla procedura seguente:
   
    ![New Person](./media/active-directory-saas-topdesk-public-tutorial/ic790629.png "New Person")
   
    a. Fare clic sulla scheda Generale hello.

    b. In hello **Surname** casella di testo, digitare il cognome dell'utente hello come Simon
 
    c. Selezionare un **sito** per conto di hello.
 
    d. Fare clic su **Salva**.

> [!NOTE]
> È possibile utilizzare qualsiasi altro TOPdesk - strumento di creazione di account utente pubblica o le API fornite da TOPdesk - pubblico tooprovision Azure AD account.

### <a name="assign-hello-azure-ad-test-user"></a>Assegnare l'utente test hello Azure AD

In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooTOPdesk - pubblico.

![Assegnazione del ruolo utente hello][200] 

**tooassign tooTOPdesk Britta Simon - Public, eseguire hello alla procedura seguente:**

1. Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **TOPdesk - Public**.

    ![Hello TOPdesk - Public collegamento nell'elenco delle applicazioni hello](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_app.png)  

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![collegamento di "Utenti e gruppi" Hello][202]

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![riquadro assegnazione aggiungere Hello][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="test-single-sign-on"></a>Testare l'accesso Single Sign-On

In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.

Quando si fa clic hello TOPdesk - Public riquadro in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour TOPdesk - pubblico dell'applicazione.
Per ulteriori informazioni sul pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_203.png

