---
title: 'Esercitazione: Integrazione di Azure Active Directory con Cezanne HR Software | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e delle risorse Umane Cezanne software.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: fb8f95bf-c3c1-4e1f-b2b3-3b67526be72d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: 3675acd8871d62c2277def8074f7aa39ac46e2a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-integrate-azure-active-directory-with-cezanne-hr-software"></a>Esercitazione: Eseguire l'integrazione di Azure Active Directory con Cezanne HR Software

In questa esercitazione, è illustrato come toointegrate Cezanne HR software con Azure Active Directory (Azure AD).

Integrazione delle risorse Umane Cezanne software con Azure AD fornisce hello seguenti vantaggi. È possibile:

- Controllo di Azure AD che ha accesso tooCezanne software delle risorse Umane.
- Abilitare l'accesso agli utenti tooautomatically software tooCezanne HR con single sign-on (SSO) con i propri account Azure AD.
- Gestire gli account in un'unica posizione centrale: hello portale di Azure.

toolearn ulteriori informazioni su software come un servizio (SaaS) integrazione dell'applicazione con Azure AD, vedere [novità di accesso all'applicazione e SSO con Azure Active Directory?](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

integrazione di Azure AD con HR Cezanne software tooconfigure, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione di Cezanne HR Software abilitata per l'accesso SSO

> [!NOTE]
> passaggi di hello tootest in questa esercitazione, è consigliabile non utilizzare un ambiente di produzione.

passaggi di hello tootest in questa esercitazione, seguire queste indicazioni:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene testato l'accesso SSO di Azure AD in un ambiente di test. 

scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

* Aggiunta delle risorse Umane Cezanne software dalla raccolta hello
* Configurazione e test dell'accesso Single Sign-On (SSO) di Microsoft Azure AD

## <a name="add-cezanne-hr-software-from-hello-gallery"></a>Aggiungere Cezanne HR software dalla raccolta di hello
integrazione di hello tooconfigure di software Cezanne HR in Azure AD, aggiungere software Cezanne HR hello raccolta tooyour elenco di App SaaS gestite.

tooadd Cezanne HR software dalla raccolta di hello, hello seguenti:

1. In hello  **[portale di Azure](https://portal.azure.com)**, nel riquadro sinistro di hello, selezionare hello **Azure Active Directory** pulsante. 

    ![pulsante "Azure Active Directory" Hello][1]

2. Selezionare **Applicazioni aziendali** > **Tutte le applicazioni**.

    ![collegano Hello "Tutte le applicazioni"][2]
    
3. una nuova applicazione, nella parte superiore di hello di hello tooadd **tutte le applicazioni** nella finestra di dialogo **nuova applicazione**.

    !["Nuova applicazione" Hello pulsante][3]

4. Nella casella di ricerca hello, digitare **Cezanne HR Software**.

    ![casella di ricerca Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_search.png)

5. Selezionare dall'elenco risultati hello **Cezanne HR Software** e quindi selezionare hello **Aggiungi** pulsante applicazione hello tooadd.

    ![elenco dei risultati Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurare e testare l'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Cezanne HR Software usando un utente di test di nome "Britta Simon".

Per toowork SSO, Azure AD deve tooknow hello HR Cezanne software controparte toohello Azure utente di Active Directory. In altre parole, è necessario stabilire una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato hello in hello HR Cezanne software.

relazione di collegamento hello tooestablish, assegnare hello software HR Cezanne **nome utente** valore come hello Azure AD **Username** valore.

tooconfigure e SSO AD Azure tramite software Cezanne HR, hello completo seguenti blocchi predefiniti di test.

### <a name="configure-azure-ad-sso"></a>Configurare l'accesso SSO di Azure AD

In questa sezione, è possibile abilitare SSO AD Azure nel portale di Azure hello e configurare SSO HR Cezanne nell'applicazione in uso eseguendo hello seguenti:

1. Nel portale di Azure su hello hello **Cezanne HR Software** pagina di integrazione dell'applicazione, seleziona **Single sign-on**.

    ![comando "Single sign-on" Hello][4]

2. tooenable SSO, in hello **Single sign-on** la finestra di dialogo, seleziona hello **modalità** come **basato su SAML Sign-on**.
 
    ![casella "Modalità di" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_samlbase.png)

3. In **Cezanne HR Software dominio e gli URL**, hello seguenti:

    ![la sezione "Cezanne HR Software dominio e gli URL" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_url.png)

    a. In hello **Sign-on URL** casella, digitare un URL che ha hello la seguente sintassi:`https://w3.cezanneondemand.com/cezannehr/-/<tenant id>`

    b. In hello **URL di risposta** casella, digitare un URL che ha hello la seguente sintassi:`https://w3.cezanneondemand.com:443/<tenantid>`    
     
    > [!NOTE] 
    > Hello valori precedenti non sono reali. Poterli aggiornare con l'URL di risposta effettivo hello e URL hello-sign-on. i valori hello tooobtain, hello contatto [team di supporto client software HR Cezanne](mailto:info@cezannehr.com).

4. In **certificato di firma SAML**selezionare **certificato (Base64)**e quindi salvare il file di certificato hello nel computer in uso.

    ![la sezione "Certificato di firma SAML" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_certificate.png) 

5. Selezionare **Salva**.

    ![pulsante "Salva" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_400.png)
    
6. In **Cezanne HR Software configurazione**selezionare **Configura Cezanne HR Software** tooopen hello **Configura sign-on** finestra. Hello copia **ID entità SAML** e **SAML Single Sign-On Service** URL da hello **riferimento rapido** sezione.

    ![sezione "Configurazione di Software Cezanne HR" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_configure.png) 

7. In una finestra del web browser, accedere tooyour Cezanne HR di tenant di software come amministratore.

8. Nel riquadro sinistro hello selezionare **installazione System**. Selezionare **Security Settings** > **Single Sign-On Configuration** (Impostazioni di sicurezza > Configurazione Single Sign-on).

    ![collegamento di "Configurazione Single Sign-On" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_000.png)

9. In hello **consentire agli utenti toolog hello seguenti servizi Single Sign-On (SSO) con** riquadro, seleziona hello **SAML 2.0** casella di controllo e seleziona hello **configurazione avanzata** opzione.

    ![Opzioni dei servizi Single Sign-On](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_001.png)

10. Selezionare **Add New** (Aggiungi nuovo).

    ![pulsante "Aggiungi" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_002.png)

11. In **provider di identità SAML 2.0**, hello seguenti:

    ![la sezione "Provider di identità SAML 2.0" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_003.png)
    
    a. In hello **nome visualizzato** , immettere il nome di hello del provider di identità.

    b. In hello **identificatore dell'entità** incollare hello **ID entità SAML** copiato dalla hello portale di Azure. 

    c. In hello **SAML associazione** casella di riepilogo, seleziona **POST**.

    d. In hello **Endpoint del servizio Token di sicurezza** incollare hello **servizio SAML Single Sign-On** URL copiato da hello portale di Azure. 
    
    e. In hello **nome dell'attributo ID utente** immettere `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.
    
    f. hello tooupload scaricato certificato da Azure AD, seleziona hello **caricare** pulsante.
    
    g. Selezionare **OK**. 

12. Selezionare **Salva**.

    ![pulsante "Salva" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_004.png)

> [!TIP]
> Per la configurazione di app hello, è possibile leggere una versione di hello precedenti istruzioni in hello concisa [portale di Azure](https://portal.azure.com). Dopo aver aggiunto l'applicazione hello da hello **Active Directory** > **applicazioni aziendali** sezione, seleziona hello **Single sign-on** scheda. Quindi hello accesso incorporati documentazione da hello **configurazione** sezione. 

toolearn più feature hello documentazione incorporati, vedere [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985).
> 

### <a name="create-an-azure-ad-test-user"></a>Creare un utente test di Azure AD
In questa sezione è creare test utente Britta Simon hello portale di Azure.

![utente test hello Britta Simon][100]

un utente di prova in Azure AD, toocreate hello seguenti:

1. In hello **portale di Azure**, nel riquadro sinistro di hello, selezionare hello **Azure Active Directory** pulsante.

    ![pulsante "Azure Active Directory" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_01.png) 

2. elenco di hello toodisplay di utenti, selezionare **utenti e gruppi** > **tutti gli utenti**.
    
    ![collegano Hello "Tutti gli utenti"](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_02.png) 
    
    Hello **tutti gli utenti** verrà visualizzata la finestra di dialogo.

3. hello tooopen **utente** nella finestra di dialogo **Aggiungi**.
 
    ![pulsante "Aggiungi" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_03.png) 

4. In hello **utente** finestra di dialogo casella, hello seguenti:
 
    ![finestra di dialogo "User" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_04.png) 

    a. In hello **nome** digitare **BrittaSimon**.

    b. In hello **nome utente** digitare utente Britta Simon **indirizzo di posta elettronica**.

    c. Seleziona hello **Show Password** casella di controllo, quindi valore hello si noti che è stato generato in hello **Password** casella.

    d. Selezionare **Crea**.
 
### <a name="create-a-cezanne-hr-software-test-user"></a>Creare un utente di test di Cezanne HR Software

toosign agli utenti di Azure AD tooenable nel software tooCezanne HR, deve disporre delle risorse Umane Cezanne software. In caso di hello del software Cezanne HR, il provisioning è un'attività manuale.

Eseguire il provisioning di un account utente eseguendo hello seguenti:

1.  Accedi tooyour Cezanne HR sito società di software come amministratore.

2.  Nel riquadro sinistro hello selezionare **installazione System** > **Gestisci utenti** > **Add New User**.

    ![collegamento "Aggiungi nuovo utente" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_005.png "nuovo utente")

3.  In **dettagli persona**, hello seguenti:

    ![sezione "Dettagli persona" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_006.png "nuovo utente")
    
    a. Impostare **Internal User** (Utente interno) su **OFF**.
    
    b. In hello **nome** casella, tipo hello nome dell'utente, ad esempio, **Laura**.  
 
    c. In hello **cognome** casella, tipo hello cognome dell'utente, ad esempio, **Simon**.
    
    d. In hello **posta elettronica** , digitare, ad esempio, l'indirizzo di posta elettronica dell'utente hello Brittasimon@contoso.com.

4.  In **informazioni sull'Account**, hello seguenti:

    ![la sezione "Informazioni sull'Account" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_007.png "nuovo utente")
    
    a. In hello **Username** , digitare, ad esempio, l'indirizzo di posta elettronica dell'utente hello Brittasimon@contoso.com.
    
    b. In hello **Password** , digitare la password dell'utente hello.
    
    c. In hello **ruolo di sicurezza** , quindi selezionare **Professional HR**.
    
    d. Selezionare **OK**.

5. In hello **Single sign-on** scheda hello **identificatori di SAML 2.0** selezionare **Aggiungi nuovo**.

    ![pulsante "Aggiungi" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_008.png "utente")

6. In hello **Provider di identità** nella casella di riepilogo, selezionare il provider di identità. In hello **identificatore utente** , immettere l'indirizzo di posta elettronica hello per account di prova utente Britta Simon.

    ![Hello caselle "Provider di identità" e "ID utente"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_009.png "utente")
    
7. Selezionare **Salva**.

    ![pulsante "Salva" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_010.png "utente")

### <a name="assign-hello-azure-ad-test-user"></a>Assegnare l'utente test hello Azure AD

In questa sezione per abilitare l'utente test Britta Simon toouse SSO di Azure concessione dell'accesso tooCezanne HR software.

![Accesso utente di test][200] 

1. Nel portale di Azure hello, aprire visualizzazione applicazioni hello e quindi passare visualizzazione directory toohello. Selezionare **Applicazioni aziendali** > **Tutte le applicazioni**.

    ![collegano Hello "Tutte le applicazioni"][201] 

2. Nell'elenco di applicazioni hello, selezionare **Cezanne HR Software**.

    ![elenco di "applicazioni di" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_app.png) 

3. Dal menu hello hello sinistra, selezionare **utenti e gruppi**.

    ![Assegnare utenti][202] 

4. Selezionare **Aggiungi**. Quindi in hello **Aggiungi** nella finestra di dialogo **utenti e gruppi**.

    ![Collegamento "Utenti e gruppi"][203]

5. In hello **utenti e gruppi** della finestra di dialogo hello **utenti** elenco, selezionare **Britta Simon**.

6. In hello **utenti e gruppi** nella finestra di dialogo **selezionare**.

7. In hello **Aggiungi** nella finestra di dialogo **assegnare**.
    
### <a name="test-sso"></a>Testare l'accesso SSO

In questa sezione verificare la configurazione di SSO AD Azure tramite hello Pannello di accesso.

Quando si seleziona riquadro software Cezanne HR di hello in hello Pannello di accesso, si accede da automaticamente tooyour applicazione software Cezanne HR.

## <a name="next-steps"></a>Passaggi successivi

* [Elenco di esercitazioni sull'App SaaS toointegrate con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_203.png

