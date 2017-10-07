---
title: 'Esercitazione: Integrazione di Azure Active Directory con ServiceNow | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e ServiceNow e ServiceNow Express.
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 1d8eb99e-8ce5-4ba4-8b54-5c3d9ae573f6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: df6a07dd1aa437198fbdb9d0a04ea14f3a320249
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-servicenow"></a>Esercitazione: Integrazione di Azure Active Directory con ServiceNow
In questa esercitazione, è illustrato come toointegrate ServiceNow ed Express di ServiceNow con Azure Active Directory (Azure AD).

Integrazione di ServiceNow e ServiceNow Express con Azure AD fornisce hello seguenti vantaggi:

* È possibile controllare in Azure AD che ha accesso tooServiceNow e ServiceNow Express
* È possibile abilitare l'utenti tooautomatically get connesso tooServiceNow e ServiceNow Express (Single Sign-On) con i propri account Azure AD
* È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure classico

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti
integrazione di Azure AD con ServiceNow e ServiceNow Express tooconfigure, è necessario hello seguenti elementi:

* Sottoscrizione di Azure AD.
* Per ServiceNow, un'istanza o un tenant di ServiceNow, versione Calgary o successiva
* Per ServiceNow Express, un'istanza di ServiceNow Express, versione Helsinki o successiva
* tenant di ServiceNow Hello deve avere hello [più Provider Single Sign nel plug-in](http://wiki.servicenow.com/index.php?title=Multiple_Provider_Single_Sign-On#gsc.tab=0) abilitato. Questa operazione può essere eseguita [inviando una richiesta di servizio](https://hi.service-now.com). 

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.
> 
> 

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

* Non usare l'ambiente di produzione, a meno che non sia necessario.
* Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di ServiceNow dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD per ServiceNow o ServiceNow Express

## <a name="adding-servicenow-from-hello-gallery"></a>Aggiunta di ServiceNow dalla raccolta hello
integrazione hello tooconfigure di ServiceNow o ServiceNow Express in Azure AD, è necessario tooadd ServiceNow dall'elenco di tooyour hello raccolta di App SaaS gestite. 

**tooadd ServiceNow dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello **portale di Azure classico**via hello riquadro di spostamento a sinistra, fare clic su **Active Directory**. 
   
    ![Active Directory][1]
2. Da hello **Directory** elenco, directory hello selezionare per il quale si desidera l'integrazione di directory tooenable.
3. visualizzazione di applicazioni hello tooopen, nella visualizzazione directory hello, fare clic su **applicazioni** nel menu superiore hello.
   
    ![Applicazioni][2]
4. Fare clic su **Aggiungi** nella parte inferiore di hello della pagina hello.
   
    ![Applicazioni][3]
5. In hello **cosa si desidera toodo** finestra di dialogo, fare clic su **aggiungere un'applicazione dalla raccolta di hello**.
   
    ![Applicazioni][4]
6. Nella casella di ricerca hello, digitare **ServiceNow**.
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_01.png)
7. Nel riquadro risultati hello selezionare **ServiceNow**, quindi fare clic su **completa** tooadd un'applicazione hello.
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_02.png)

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con ServiceNow o ServiceNow Express in base a un utente test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in ServiceNow è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in ServiceNow richiede toobe stabilita.
Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in ServiceNow. tooconfigure e test Azure single sign-on AD con ServiceNow, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurazione di Azure AD Single Sign-On per ServiceNow](#configuring-azure-ad-single-sign-on-for-servicenow)**  -tooenable il toouse utenti questa funzionalità.
2. **[Configurazione di Azure AD Single Sign-On per ServiceNow Express](#configuring-azure-ad-single-sign-on-for-servicenow-express)**  -tooenable il toouse utenti questa funzionalità.
3. **[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
4. **[Creazione di un utente test ServiceNow](#creating-a-servicenow-test-user)**  -toohave un equivalente di Britta Simon in ServiceNow che è la rappresentazione toohello collegato Azure AD dell'utente.
5. **[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
6. **[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

> [!NOTE]
> Se si desidera tooconfigure ServiceNow omettere il passaggio 2. Analogamente, se si desidera tooconfigure ServiceNow Express omettere il passaggio 1.
> 
> 

### <a name="configuring-azure-ad-single-sign-on-for-servicenow"></a>Configurazione dell'accesso Single Sign-On per ServiceNow
1. Nel portale classico hello Azure AD su hello **ServiceNow** pagina di integrazione dell'applicazione, fare clic su **configurare single sign-on** tooopen hello **configurare Single Sign-On** finestra di dialogo .
   
    ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-servicenow-tutorial/IC749323.png "Configurare l'accesso Single Sign-On")

2. In hello **come si sarebbe ad esempio utenti toosign su tooServiceNow** selezionare **Microsoft Azure AD Single Sign-On**e quindi fare clic su **Avanti**.
   
    ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-servicenow-tutorial/IC749324.png "Configurare l'accesso Single Sign-On")

3. In hello **Configura impostazioni App** eseguire hello alla procedura seguente:
   
    ![Configurare l'URL dell'app](./media/active-directory-saas-servicenow-tutorial/IC769497.png "Configurare l'URL dell'app")
   
    a. in hello **ServiceNow URL di accesso** casella di testo digitare l'URL usato dall'applicazione ServiceNow tooyour toosign-on agli utenti il modello di hello: `https://<instance-name>.service-now.com`.
   
    b. In hello **identificatore** casella di testo digitare l'URL usato dall'applicazione ServiceNow tooyour toosign-on agli utenti il modello di hello: `https://<instance-name>.service-now.com`.
   
    c. Fare clic su **Avanti**

4. Azure AD toohave automaticamente configurare ServiceNow per l'autenticazione basata su SAML, immettere il nome dell'istanza ServiceNow, nome utente amministratore e la password di amministratore in hello **configura automaticamente l'accesso single sign-on** formato e fare clic su  *Configurare*. Si noti che nome utente amministratore hello fornito deve avere hello **security_admin** ruolo assegnato in ServiceNow per questo toowork. In caso contrario, toomanually configurare ServiceNow toouse Azure AD come provider di identità SAML, fare clic su **configurare manualmente un'applicazione hello per single sign-on**, quindi fare clic su **Avanti** e hello completo procedura seguente.
   
    ![Configurare l'URL dell'app](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "Configurare l'URL dell'app")

5. In hello **Configura accesso single sign-on in ServiceNow** pagina, fare clic su **Scarica certificato**, salvare il file di certificato hello in locale nel computer.
   
    ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-servicenow-tutorial/IC749325.png "Configurare l'accesso Single Sign-On")

6. Sign-on tooyour ServiceNow applicazione come amministratore.

7. Attivare hello *- integrazione di più Provider Single Sign-On Installer* plug-in seguendo hello passaggi successivi:
   
    a. Nel riquadro di spostamento hello sul lato sinistro di hello, andare troppo**definizione sistema** sezione e quindi fare clic su **plug-in**.
   
    ![Configurare l'URL dell'app](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_03.png "Attivare il plug-in")
   
    b. Cercare *Integration - Multiple Provider Single Sign-On Installer*.
   
    ![Configurare l'URL dell'app](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_04.png "Attivare il plug-in")
   
    c. Selezionare i plug-in hello. Fare clic e selezionare **Activate/Upgrade** (Attiva/Aggiorna).
   
    d. Fare clic su hello **attiva** pulsante.

8. Nel riquadro di spostamento hello sul lato sinistro di hello, fare clic su **proprietà**.  
   
    ![Configurare l'URL dell'app](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_06.png "Configurare l'URL dell'app")

9. In hello **più proprietà del Provider SSO** finestra di dialogo, eseguire hello alla procedura seguente:
   
    ![Configurare l'URL dell'app](./media/active-directory-saas-servicenow-tutorial/IC7694981.png "Configurare l'URL dell'app")
   
    a. Per **Enable multiple provider SSO** selezionare **Yes**.
   
    b. Come **abilita la registrazione di debug ottenuta hello più provider SSO integration**selezionare **Sì**.
   
    c. In **tabella campo hello utente hello...**  casella tipo **nome_utente**.
   
    d. Fare clic su **Salva**.

10. Nel riquadro di spostamento hello sul lato sinistro di hello, fare clic su **certificati x509**.
    
     ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_05.png "Configurare l'accesso Single Sign-On")

11. In hello **certificati x. 509** finestra di dialogo, fare clic su **New**.
    
     ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-servicenow-tutorial/IC7694974.png "Configurare l'accesso Single Sign-On")

12. In hello **certificati x. 509** finestra di dialogo, eseguire hello alla procedura seguente:
    
     ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "Configurare l'accesso Single Sign-On")
    
     a. Fare clic su **New**.
    
     b. In hello **nome** casella di testo, digitare un nome per la configurazione (ad esempio: **TestSAML2.0**).
    
     c. Selezionare **Active**.
    
     d. Per **Format** selezionare **PEM**.
    
     e. Per **Type** selezionare **Trust Store Cert**.
    
     f. Aprire il certificato con codificata base 64 nel blocco note, hello copia del contenuto di esso negli Appunti e quindi incollarlo toohello **certificato PEM** casella di testo.
    
     g. Fare clic su **Update**.

13. Nel riquadro di spostamento hello sul lato sinistro di hello, fare clic su **provider di identità**.
    
     ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_07.png "Configurare l'accesso Single Sign-On")

14. In hello **provider di identità** finestra di dialogo, fare clic su **New**:
    
     ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-servicenow-tutorial/IC7694977.png "Configurare l'accesso Single Sign-On")

15. In hello **provider di identità** finestra di dialogo, fare clic su **SAML2 Update1?**:
    
     ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-servicenow-tutorial/IC7694978.png "Configurare l'accesso Single Sign-On")

16. Nella finestra di dialogo Proprietà Update1 SAML2 hello eseguire hello alla procedura seguente:
    
     ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-servicenow-tutorial/IC7694982.png "Configurare l'accesso Single Sign-On")

    a. in hello **nome** casella di testo, digitare un nome per la configurazione (ad esempio: **SAML 2.0**).

    b. In hello **campo utente** casella tipo **posta elettronica** o **nome_utente**, a seconda di quale campo viene usato toouniquely identificare gli utenti nella distribuzione di ServiceNow. 

    > [!NOTE] 
    > Puoi tooemit configurazione Azure AD l'ID utente hello Azure AD (nome dell'entità utente) o hello indirizzo di posta elettronica come hello identificatore univoco nel token SAML hello da passare toohello **ServiceNow > attributi > Single Sign-On** sezione Hello portale di Azure classico e mapping hello desiderato campo toohello **nameidentifier** attributo. il valore di Hello archiviato per l'attributo selezionato hello in Azure Active Directory (ad esempio nome dell'entità utente) deve corrispondere il valore di hello archiviato in ServiceNow per il campo hello immesso (ad esempio nome_utente)

    c. Nel portale classico di hello Azure AD copiare hello **ID Provider di identità** valore e quindi incollarlo hello **Identity Provider URL** casella di testo.

    d. Nel portale classico di hello Azure AD copiare hello **URL richiesta di autenticazione** valore e quindi incollarlo hello **AuthnRequest del Provider di identità** casella di testo.

    e. Nel portale classico di hello Azure AD copiare hello **URL del servizio Single Sign-Out** valore e quindi incollarlo hello **SingleLogoutRequest Provider identità** casella di testo.

    f. In hello **ServiceNow Homepage** casella di testo, digitare l'URL della home page di istanza di ServiceNow hello.

    > [!NOTE] 
    > Home page dell'istanza ServiceNow Hello è una concatenazione del **URL tenant ServieNow** e **/navpage.do** (ad esempio:`https://fabrikam.service-now.com/navpage.do`).

    g. In hello **ID entità o dell'autorità di certificazione** casella di testo, digitare l'URL del tenant di ServiceNow hello.

    h. In hello **URL pubblico** casella di testo, digitare l'URL del tenant di ServiceNow hello. 

    i. In hello **protocollo di associazione per hello dell'IDP SingleLogoutRequest** casella tipo **urn: oasis: nomi: tc: SAML:2.0:bindings:HTTP-reindirizzamento**.

    j. Nella casella di testo criteri NameID hello, digitare **urn: oasis: nomi: tc: SAML: 1.1 NameID-formato: non specificato**.

    k. Fare clic su **Create an AuthnContextClass**.

    l. In hello **metodo AuthnContextClassRef**, tipo `http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password`. Questa operazione è necessaria soltanto per le organizzazioni basate solo su cloud. Se si usa AD FS o MFA in locale per l'autenticazione, non è necessario configurare questo valore. 

    m. Nella casella di testo **Clock Skew** digitare **60**.

    n. Per **Single Sign On Script** selezionare **MultiSSO_SAML2_Update1**.

    o. Come **x509 certificato**, selezionare il certificato di hello è stato creato nel passaggio precedente di hello.

    p. Fare clic su **Submit**. 

1. Nel portale classico hello Azure AD, selezionare hello conferma della configurazione di single sign-on e quindi fare clic su **Avanti**. 
   
    ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "Configurare l'accesso Single Sign-On")

2. In hello **Single sign-on conferma** pagina, fare clic su **completa**.
   
    ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "Configurare l'accesso Single Sign-On")

### <a name="configuring-azure-ad-single-sign-on-for-servicenow-express"></a>Configurazione dell'accesso Single Sign-On per ServiceNow Express
1. Nel portale classico hello Azure AD su hello **ServiceNow** pagina di integrazione dell'applicazione, fare clic su **configurare single sign-on** tooopen hello **configurare Single Sign-On** finestra di dialogo .
   
    ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-servicenow-tutorial/IC749323.png "Configurare l'accesso Single Sign-On")

2. In hello **come si sarebbe ad esempio utenti toosign su tooServiceNow** selezionare **Microsoft Azure AD Single Sign-On**e quindi fare clic su **Avanti**.
   
    ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-servicenow-tutorial/IC749324.png "Configurare l'accesso Single Sign-On")

3. In hello **Configura impostazioni App** eseguire hello alla procedura seguente:
   
    ![Configurare l'URL dell'app](./media/active-directory-saas-servicenow-tutorial/IC769497.png "Configurare l'URL dell'app")
   
    a. in hello **ServiceNow URL di accesso** casella di testo digitare l'URL usato dall'applicazione ServiceNow tooyour toosign-on agli utenti il modello di hello: `https://<instance-name>.service-now.com`.
   
    b. In hello **URL autorità di certificazione** , digitare l'URL usato dagli utenti toosign-on tooyour ServiceNow applicazione hello modello `https://<instance-name>.service-now.com`.
   
    c. Fare clic su **Avanti**

4. Fare clic su **configurare manualmente un'applicazione hello per single sign-on**, quindi fare clic su **Avanti** e hello completo seguendo i passaggi.
   
    ![Configurare l'URL dell'app](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "Configurare l'URL dell'app")

5. In hello **Configura accesso single sign-on in ServiceNow** pagina, fare clic su **Scarica certificato**, salvare il file di certificato hello in locale nel computer e quindi fare clic su **Avanti**.
   
    ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-servicenow-tutorial/IC749325.png "Configurare l'accesso Single Sign-On")

6. Sign-on tooyour ServiceNow Express applicazione come amministratore.

7. Nel riquadro di spostamento hello sul lato sinistro di hello, fare clic su **Single Sign-On**.  
   
    ![Configurare l'URL dell'app](./media/active-directory-saas-servicenow-tutorial/ic7694980ex.png "Configurare l'URL dell'app")

8. In hello **Single Sign-On** finestra di dialogo, fare clic sull'icona di configurazione hello in alto hello destro e imposta hello le seguenti proprietà:
   
    ![Configurare l'URL dell'app](./media/active-directory-saas-servicenow-tutorial/ic7694981ex.png "Configurare l'URL dell'app")
   
    a. Attiva/disattiva **abilitare più provider SSO** toohello destra.
   
    b. Attiva/disattiva **debug abilitare la registrazione per hello più provider SSO integration** toohello destra.
   
    c. In **tabella campo hello utente hello...**  casella tipo **nome_utente**.
9. In hello **Single Sign-On** finestra di dialogo, fare clic su **Aggiungi nuovo certificato**.
   
    ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-servicenow-tutorial/ic7694973ex.png "Configurare l'accesso Single Sign-On")
10. In hello **certificati x. 509** finestra di dialogo, eseguire hello alla procedura seguente:
    
    ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "Configurare l'accesso Single Sign-On")
    
    a. In hello **nome** casella di testo, digitare un nome per la configurazione (ad esempio: **TestSAML2.0**).
    
    b. Selezionare **Active**.
    
    c. Per **Format** selezionare **PEM**.
    
    d. Per **Type** selezionare **Trust Store Cert**.
    
    e. Creare un file con codifica Base64 dal certificato scaricato.
    
    > [!NOTE]
    > Per ulteriori informazioni, vedere [come tooconvert certificato di un file binario in un file di testo](http://youtu.be/PlgrzUZ-Y1o).
    > 
    > 
    
    f. Aprire il certificato con codificata base 64 nel blocco note, hello copia del contenuto di esso negli Appunti e quindi incollarlo toohello **certificato PEM** casella di testo.
    
    g. Fare clic su **Update**.
11. In hello **Single Sign-On** finestra di dialogo, fare clic su **aggiungere nuovo IdP**.
    
    ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-servicenow-tutorial/ic7694976ex.png "Configurare l'accesso Single Sign-On")
12. In hello **Aggiungi nuovo Provider di identità** finestra di dialogo, in **configurare Provider di identità**, eseguire hello alla procedura seguente:
    
    ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-servicenow-tutorial/ic7694982ex.png "Configurare l'accesso Single Sign-On")

    a. in hello **nome** casella di testo, digitare un nome per la configurazione (ad esempio: **SAML 2.0**).

    b. Nel portale classico di hello Azure AD copiare hello **ID Provider di identità** valore e quindi incollarlo hello **Identity Provider URL** casella di testo.

    c. Nel portale classico di hello Azure AD copiare hello **URL richiesta di autenticazione** valore e quindi incollarlo hello **AuthnRequest del Provider di identità** casella di testo.

    d. Nel portale classico di hello Azure AD copiare hello **URL del servizio Single Sign-Out** valore e quindi incollarlo hello **SingleLogoutRequest Provider identità** casella di testo.

    e. Come **Identity Provider Certificate**, selezionare il certificato di hello è stato creato nel passaggio precedente di hello.


1. Fare clic su **impostazioni avanzate**e in **proprietà Provider di identità aggiuntive**, eseguire hello alla procedura seguente:
   
    ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-servicenow-tutorial/ic7694983ex.png "Configurare l'accesso Single Sign-On")
   
    a. In hello **protocollo di associazione per hello dell'IDP SingleLogoutRequest** casella tipo **urn: oasis: nomi: tc: SAML:2.0:bindings:HTTP-reindirizzamento**.
   
    b. In hello **criteri NameID** casella tipo **urn: oasis: nomi: tc: SAML: 1.1 NameID-formato: non specificato**.    
   
    c. In hello **metodo AuthnContextClassRef**, tipo **http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password**.
   
    d. Fare clic su **Create an AuthnContextClass**.

2. In **ulteriori proprietà Provider del servizio**, eseguire hello alla procedura seguente:
   
    ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-servicenow-tutorial/ic7694984ex.png "Configurare l'accesso Single Sign-On")
   
    a. In hello **ServiceNow Homepage** casella di testo, digitare l'URL della home page di istanza di ServiceNow hello.
   
    > [!NOTE]
    > Home page dell'istanza ServiceNow Hello è una concatenazione del **URL tenant ServieNow** e **/navpage.do** (ad esempio: `https://fabrikam.service-now.com/navpage.do`).
    > 
    > 
   
    b. In hello **ID entità o dell'autorità di certificazione** casella di testo, digitare l'URL del tenant di ServiceNow hello.
   
    c. In hello **URI destinatario** casella di testo, digitare l'URL del tenant di ServiceNow hello. 
   
    d. Nella casella di testo **Clock Skew** digitare **60**.
   
    e. In hello **campo utente** casella tipo **posta elettronica** o **nome_utente**, a seconda di quale campo viene usato toouniquely identificare gli utenti nella distribuzione di ServiceNow.
   
    > [!NOTE]
    > Puoi tooemit configurazione Azure AD l'ID utente hello Azure AD (nome dell'entità utente) o hello indirizzo di posta elettronica come hello identificatore univoco nel token SAML hello da passare toohello **ServiceNow > attributi > Single Sign-On** sezione Hello portale di Azure classico e mapping hello desiderato campo toohello **nameidentifier** attributo. il valore di Hello archiviato per l'attributo selezionato hello in Azure Active Directory (ad esempio nome dell'entità utente) deve corrispondere il valore di hello archiviato in ServiceNow per il campo hello immesso (ad esempio nome_utente)
    > 
    > 
   
    f. Fare clic su **Salva**. 

3. Nel portale classico hello Azure AD, selezionare hello conferma della configurazione di single sign-on e quindi fare clic su **Avanti**. 
   
    ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "Configurare l'accesso Single Sign-On")

4. In hello **Single sign-on conferma** pagina, fare clic su **completa**.
   
    ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "Configurare l'accesso Single Sign-On")

## <a name="configuring-user-provisioning"></a>Configurazione del provisioning utente
obiettivo di Hello di questa sezione è toooutline tooenable provisioning utente dell'utente di Active Directory come account di tooServiceNow.

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a>tooconfigure provisioning degli utenti, eseguire hello alla procedura seguente:
1. Nel portale di gestione di Azure classico hello, su hello **ServiceNow** pagina di integrazione dell'applicazione, fare clic su **Configura provisioning utente**. 
   
    ![Provisioning degli utenti](./media/active-directory-saas-servicenow-tutorial/IC769498.png "Provisioning degli utenti")

2. In hello **immettere i ServiceNow credenziali tooenable il provisioning utente automatico** fornire hello le impostazioni di configurazione seguente:
   
     a. In hello **nome istanza ServiceNow** casella di testo Nome istanza ServiceNow hello del tipo.
   
     b. In hello **nome utente amministratore ServiceNow** casella di testo Nome hello del tipo di account amministratore ServiceNow hello.
   
     c. In hello **Password amministratore ServiceNow** casella di testo, digitare la password hello per questo account.
   
     d. Fare clic su **convalidare** tooverify la configurazione.
   
     e. Fare clic su hello **Avanti** hello tooopen pulsante **passaggi successivi** pagina.
   
     f. Se si desidera tooprovision applicazione di toothis tutti gli utenti, selezionare "**esegue automaticamente il provisioning di tutti gli account utente in un'applicazione hello directory toothis**". 
   
    ![Passaggi successivi](./media/active-directory-saas-servicenow-tutorial/IC698804.png "Passaggi successivi")
   
     g. In hello **passaggi successivi** pagina, fare clic su **completa** toosave la configurazione.

### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
In questa sezione creare un utente test nel portale classico di hello chiamato Britta Simon.

![Creare un utente di Azure AD][20]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di Azure classico**via hello riquadro di spostamento a sinistra, fare clic su **Active Directory**.
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_09.png) 

2. Da hello **Directory** elenco, directory hello selezionare per il quale si desidera l'integrazione di directory tooenable.

3. Fare clic su elenco hello toodisplay di utenti, nel menu hello nella parte superiore di hello, **utenti**.
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_03.png) 

4. hello tooopen **Aggiungi utente** finestra di dialogo, nella barra degli strumenti hello nella parte inferiore di hello, fare clic su **Aggiungi utente**.
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_04.png) 

5. In hello **informazioni sull'utente** finestra di dialogo eseguire hello alla procedura seguente:
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_05.png) 
   
    a. In Tipo di utente selezionare Nuovo utente nell'organizzazione.
   
    b. In nome utente hello **textbox**, tipo **BrittaSimon**.
   
    c. Fare clic su **Avanti**.

6. In hello **profilo utente** finestra di dialogo eseguire hello alla procedura seguente:
   
   ![Creazione di un utente test di Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_06.png) 
   
   a. In hello **nome** casella tipo **Laura**.  
   
   b. In hello **cognome** casella di testo, tipo, **Simon**.
   
   c. In hello **nome visualizzato** casella tipo **Britta Simon**.
   
   d. In hello **ruolo** elenco, selezionare **utente**.
   
   e. Fare clic su **Avanti**.

7. In hello **Ottieni password temporanea** nella pagina, fare clic su **creare**.
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_07.png) 

8. In hello **Ottieni password temporanea** finestra di dialogo eseguire hello alla procedura seguente:
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_08.png) 
   
    a. Annotare il valore di hello di hello **nuova Password**.
   
    b. Fare clic su **Complete**.   

### <a name="creating-a-servicenow-test-user"></a>Creazione di un utente test di ServiceNow
In questa sezione viene creato un utente di nome Britta Simon in ServiceNow. In questa sezione viene creato un utente di nome Britta Simon in ServiceNow. Se non si conosce la modalità tooadd un utente nel ServiceNow o ServiceNow Express account, contattare il team di supporto di ServiceNow.

### <a name="assigning-hello-azure-ad-test-user"></a>Assegnazione utente test hello Azure AD
In questa sezione è abilitare Britta Simon toouse single sign-on Azure concedendo tooServiceNow proprio accesso.

![Assegna utente][200] 

**tooassign Britta Simon tooServiceNow, eseguire hello alla procedura seguente:**

1. Nel portale classico hello, fare clic su visualizzazione di applicazioni hello tooopen, nella visualizzazione directory hello **applicazioni** nel menu superiore hello.
   
    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **ServiceNow**.
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_10.png) 

3. Scegliere dal menu hello in primo piano hello **utenti**.
   
    ![Assegna utente][203] 

4. Selezionare dall'elenco di tutti gli utenti di hello **Britta Simon**.

5. Nella barra degli strumenti di hello nella parte inferiore di hello, fare clic su **assegnare**.
   
    ![Assegna utente][205]

### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On
obiettivo di Hello di questa sezione è tootest la configurazione di single sign-on di Azure AD mediante hello Pannello di accesso.

Quando si fa clic su riquadro ServiceNow hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour ServiceNow applicazione.

## <a name="additional-resources"></a>Risorse aggiuntive
* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_04.png


[5]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_05.png
[6]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_06.png
[7]:  ./media/active-directory-saas-servicenow-tutorial/tutorial_general_050.png
[10]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_060.png
[11]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_070.png
[20]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_205.png
