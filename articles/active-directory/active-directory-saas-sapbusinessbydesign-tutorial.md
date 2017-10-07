---
title: 'Esercitazione: Integrazione di Azure Active Directory con SAP Business ByDesign | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e SAP Business ByDesign.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 82938920-33ba-47cb-b141-511b46d19e66
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: c14714fd27f8d7fc555f25c7be83fad2b0d7f333
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-business-bydesign"></a>Esercitazione: Integrazione di Azure Active Directory con SAP Business ByDesign

In questa esercitazione, è illustrato come toointegrate SAP Business ByDesign con Azure Active Directory (Azure AD).

Integrazione di SAP Business ByDesign con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooSAP ByDesign di Business.
- È possibile abilitare l'utenti tooautomatically get connesso tooSAP ByDesign di Business (Single Sign-On) con i propri account Azure AD.
- È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure.

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

integrazione di Azure AD con SAP Business ByDesign tooconfigure, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione di SAP Business ByDesign abilitata per l'accesso Single Sign-On

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di SAP Business ByDesign dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-sap-business-bydesign-from-hello-gallery"></a>Aggiunta di SAP Business ByDesign dalla raccolta hello
integrazione hello tooconfigure di SAP Business ByDesign in Azure AD, è necessario tooadd SAP Business ByDesign dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd SAP Business ByDesign dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![pulsante di Hello Azure Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Pannello di applicazioni Enterprise Hello][2]
    
3. tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.

    ![Nuovo pulsante dell'applicazione Hello][3]

4. Nella casella di ricerca hello, digitare **SAP Business ByDesign**selezionare **SAP Business ByDesign** dal pannello risultati quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.

    ![SAP Business ByDesign nell'elenco risultati hello](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurare e testare l'accesso Single Sign-On di Azure AD

In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con SAP Business ByDesign con un utente test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in SAP Business ByDesign è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in SAP Business ByDesign deve toobe stabilita.

In SAP Business ByDesign, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.

tooconfigure e prova AD Azure single sign-on con SAP Business ByDesign, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurare Azure Active Directory Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creare un utente prova AD Azure](#create-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creare un utente test SAP Business ByDesign](#create-an-sap-business-bydesign-test-user)**  -toohave un equivalente di Britta Simon in SAP Business ByDesign che è la rappresentazione toohello collegato Azure AD dell'utente.
4. **[Assegnare l'utente test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Testare single sign-on](#test-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configure-azure-ad-single-sign-on"></a>Configurare l'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione SAP Business ByDesign.

**tooconfigure AD Azure single sign-on con SAP Business ByDesign, eseguire hello alla procedura seguente:**

1. Nel portale di Azure su hello hello **SAP Business ByDesign** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Collegamento per la configurazione dell'accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_samlbase.png)

3. In hello **SAP Business ByDesign dominio e gli URL** seguire hello alla procedura seguente:

    ![Informazioni su URL e dominio per l'accesso Single Sign-On di SAP Business ByDesign](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_url.png)

    a. In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<servername>.sapbydesign.com`

    b. In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<servername>.sapbydesign.com`

    > [!NOTE] 
    > Poiché questi non sono i valori reali, Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore. Contatto [team di supporto Client di SAP Business ByDesign](https://www.sap.com/products/cloud-analytics.support.html) tooget questi valori.

4. In hello **gli attributi utente** seguire hello alla procedura seguente:

    ![Sezione degli attributi di SAP Business ByDesign](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_attribute.png)
    
    a. In **identificatore utente** elenco, seleziona hello **ExtractMailPrefix()** (funzione).
    
    b. Da hello **posta** elenco, l'attributo utente di selezionare hello da toouse per l'implementazione. Ad esempio, se si desidera toouse hello EmployeeID come identificatore utente univoco e archiviato il valore di attributo hello in hello ExtensionAttribute2, quindi selezionare user.extensionattribute2.   

5. In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.

    ![collegamento al download del certificato Hello](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_certificate.png) 

6. Fare clic sul pulsante **Salva** .

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_400.png)

7. In hello **SAP Business ByDesign configurazione** fare clic su **configurare SAP Business ByDesign** tooopen **Configura sign-on** finestra. Hello copia **SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**

    ![Configurazione di SAP Business ByDesign](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_configure.png) 

8. tooget SSO configurato per l'applicazione, eseguire hello alla procedura seguente:
   
    a. Eseguire l'accesso nel portale di SAP Business ByDesign tooyour con diritti di amministratore.
   
    b. Passare troppo**attività comuni di gestione utente e di applicazione** e fare clic su hello **Provider di identità** scheda.
   
    c. Fare clic su **nuovo Provider di identità** hello selezionare file e metadati XML che è stato scaricato dal portale di Azure hello. Tramite l'importazione di metadati hello, sistema hello carica automaticamente il certificato di firma richiesta hello e certificato di crittografia.
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_54.png)
   
    d. hello tooinclude **URL del servizio Consumer di asserzione** nella richiesta SAML hello, selezionare **URL del servizio Consumer di asserzione includono**.
   
    e. Fare clic su **Activate Single Sign-On**(Attiva Single Sign-On).
   
    f. Salvare le modifiche.
   
    g. Fare clic su hello **risorse del sistema** scheda.
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_52.png)
   
    h. Incolla **SAML Single Sign-On Service URL**, che è stato copiato da hello portale di Azure in hello **URL di Azure AD accesso** casella di testo.
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_53.png)
   
    i. Specificare se il dipendente hello manualmente è possibile scegliere tra l'accesso con l'ID utente e password o SSO selezionando **selezione Provider di identità manuale**.
   
    j. In hello **URL SSO** sezione specificare URL hello che deve essere usata dal sistema di hello dipendente toologon toohello. 
    Elenco a discesa tooEmployee URL inviato hello è possibile scegliere tra hello le opzioni seguenti:
   
    **Non-SSO URL**
   
    sistema di Hello Invia solo hello normale sistema URL toohello dipendente. dipendente Hello non è possibile accedere utilizzando SSO e deve utilizzare password o invece del certificato.
   
    **SSO URL** 
   
    sistema di Hello Invia solo dipendente di toohello URL SSO hello. utilizzo di SSO dipendente Hello può accedere. Richiesta di autenticazione viene reindirizzato tramite hello IdP.
   
    **Automatic Selection**
   
    Se SSO non è attivo, il sistema di hello invia dipendente toohello URL normale sistema di hello. Se SSO è attiva, sistema di hello controlla se il dipendente hello dispone di una password. Se è disponibile una password, sia URL SSO e SSO di Non vengono inviati toohello dipendente. Tuttavia, se dipendente hello non dispone di password, solo hello URL SSO viene inviato toohello dipendente.
   
    k. Salvare le modifiche.

> [!TIP]
> È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!  Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello. È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Creare un utente test di Azure AD

obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.

   ![Creare un utente test di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. Nel portale di Azure, nel riquadro di sinistra hello, hello fare clic su hello **Azure Active Directory** pulsante.

    ![pulsante di Hello Azure Active Directory](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_01.png)

2. elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi**, quindi fare clic su **tutti gli utenti**.

    ![Hello "Utenti e gruppi" e i collegamenti di "Tutti gli utenti"](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_02.png)

3. hello tooopen **utente** la finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello di hello **tutti gli utenti** la finestra di dialogo.

    ![pulsante Aggiungi Hello](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_03.png)

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:

    ![finestra di dialogo utente Hello](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_04.png)

    a. In hello **nome** digitare **BrittaSimon**.

    b. In hello **nome utente** casella Tipo hello di indirizzo di posta elettronica dell'utente Britta Simon.

    c. Seleziona hello **Show Password** casella di controllo e quindi annotare i valori hello visualizzati in hello **Password** casella.

    d. Fare clic su **Crea**.
 
### <a name="create-an-sap-business-bydesign-test-user"></a>Creare un utente di test di SAP Business ByDesign

In questa sezione viene creato un utente di nome Britta Simon in SAP Business ByDesign. Rivolgersi [team di supporto SAP Business ByDesign Client](https://www.sap.com/products/cloud-analytics.support.html) utenti hello tooadd nella piattaforma SAP Business ByDesign hello. 

> [!NOTE]
> Assicurarsi che il valore NameID deve corrispondere a campo di nome utente hello nella piattaforma SAP Business ByDesign hello.

### <a name="assign-hello-azure-ad-test-user"></a>Assegnare l'utente test hello Azure AD

In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooSAP ByDesign di Business.

![Assegnazione del ruolo utente hello][200] 

**tooassign tooSAP Britta Simon ByDesign Business, eseguire hello alla procedura seguente:**

1. Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **SAP Business ByDesign**.

    ![collegamento di SAP Business ByDesign Hello nell'elenco delle applicazioni hello](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_app.png)  

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![collegamento di "Utenti e gruppi" Hello][202]

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![riquadro assegnazione aggiungere Hello][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="test-single-sign-on"></a>Testare l'accesso Single Sign-On

In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.

Quando si fa clic su riquadro SAP Business ByDesign hello in hello Pannello di accesso, è necessario ottenere l'applicazione SAP Business ByDesign tooyour automaticamente firmato-on.

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_203.png

