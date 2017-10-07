---
title: 'Esercitazione: integrazione di Azure Active Directory con JIRA SAML SSO by Microsoft | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e JIRA SAML SSO da Microsoft.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0dc847b9-eec4-4c31-845e-0144ddedc4a7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 178c4c040d9939bca271ac185ca5c2feb14f1247
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jira-saml-sso-by-microsoft"></a>Esercitazione: integrazione di Azure Active Directory con JIRA SAML SSO by Microsoft

In questa esercitazione, è illustrato come toointegrate JIRA SAML SSO da Microsoft con Azure Active Directory (Azure AD).

Integrazione JIRA SAML SSO da Microsoft Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooJIRA SAML SSO da Microsoft
- È possibile abilitare l'utenti tooautomatically get connesso tooJIRA SAML SSO da Microsoft (Single Sign-On) con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

tooconfigure integrazione di Azure AD con JIRA SAML SSO da Microsoft, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Applicazione server JIRA installato in un server di Windows a 64 bit (in locale o nel cloud hello infrastruttura IaaS)
- Server JIRA abilitato per HTTPS
- Nota hello è supportato nelle versioni del plug-in JIRA indicate nella seguente sezione.
- JIRA server sia raggiungibile nella rete internet particolarmente tooAzure AD account di accesso di pagina per l'autenticazione e deve tooreceive in grado di hello token da Azure AD
- Credenziali di amministratore configurate in JIRA
- WebSudo disabilitato in JIRA
- Utente creato nell'applicazione server JIRA hello test

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione di JIRA. Prima di tutto testare integrazione hello nello sviluppo e gestione temporanea di ambiente dell'applicazione hello e quindi utilizzare hello ambiente di produzione.

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese: [offerta prova](https://azure.microsoft.com/pricing/free-trial/).

## <a name="supported-versions-of-jira"></a>Versioni di JIRA supportate 

A tutt'oggi sono supportate le versioni seguenti di JIRA:

- Software e Core JIRA: too7.2.0 6.0
- JIRA Service Desk: too3.2 3.0

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di JIRA SAML SSO da Microsoft dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-jira-saml-sso-by-microsoft-from-hello-gallery"></a>Aggiunta di JIRA SAML SSO da Microsoft dalla raccolta hello
integrazione hello tooconfigure di JIRA SAML SSO da Microsoft in Azure AD, è necessario tooadd JIRA SAML SSO da Microsoft dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd JIRA SAML SSO da Microsoft dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Applicazioni][2]
    
3. tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.

    ![Applicazioni][3]

4. Nella casella di ricerca hello, digitare **JIRA SAML SSO da Microsoft**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_search.png)

5. Nel riquadro dei risultati hello, selezionare **JIRA SAML SSO da Microsoft**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con JIRA SAML SSO by Microsoft mediante un utente test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in JIRA SAML SSO da Microsoft è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in JIRA SAML SSO da Microsoft richiede toobe stabilita.

In JIRA SAML SSO da Microsoft, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.

tooconfigure e prova AD Azure single sign-on con JIRA SAML SSO da Microsoft, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creazione di un JIRA SAML SSO dall'utente di prova Microsoft](#creating-a-jira-saml-sso-by-microsoft-test-user)**  -toohave un equivalente di Britta Simon JIRA SAML SSO da Microsoft che è la rappresentazione toohello collegato Azure AD dell'utente.
4. **[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare single sign-on nel SAML SSO JIRA dall'applicazione di Microsoft.

**tooconfigure AD Azure single sign-on con JIRA SAML SSO da Microsoft, eseguire hello alla procedura seguente:**

1. Nel portale di Azure su hello hello **JIRA SAML SSO da Microsoft** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Configura accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_samlbase.png)

3. In hello **JIRA SAML SSO URL e di Microsoft Domain** seguire hello alla procedura seguente:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_url.png)

    a. In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<domain:port>/plugins/servlet/saml/auth`

    b. In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<domain:port>/`

    c. In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<domain:port>/plugins/servlet/saml/auth`

    > [!NOTE] 
    > Poiché questi non sono i valori reali, Aggiornare questi valori con hello effettivo identificatore, l'URL di risposta e URL Sign-On. La porta è facoltativa nel caso di un URL denominato. Questi valori vengono ricevuti durante la configurazione del plug-in Jira, illustrato più avanti nell'esercitazione di hello hello.
 
4. hello toogenerate **metadati** url, eseguire hello alla procedura seguente:

    a. Fare clic su **Registrazioni per l'app**.
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-jiramicrosoft-tutorial/appregistrations.png)
   
    b. Fare clic su **endpoint** tooopen **endpoint** la finestra di dialogo.  
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-jiramicrosoft-tutorial/endpointicon.png)

    c. Fare clic su hello copia pulsante toocopy **documento metadati federazione** url e incollarlo nel blocco note.
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-jiramicrosoft-tutorial/endpoint.png)
     
    d. Ora passare toohello pagina delle proprietà di **JIRA SAML SSO da Microsoft** e hello copia **Id applicazione** utilizzando **copia** pulsante e incollarlo nel blocco note.
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-jiramicrosoft-tutorial/appid.png)

    e. Generare hello **URL dei metadati** utilizzando hello seguente motivo: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>` e copiare il valore nel blocco note come viene utilizzato in un secondo momento per la configurazione di hello del plug-in hello.

5. Fare clic sul pulsante **Salva** .

    ![Configura accesso Single Sign-On](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_400.png)

6. Contatto [Microsoft](mailto:waadpartners@microsoft.com) con le seguenti informazioni per i plug-in di hello JIRA hello.
    
    *   Nome del cliente:
    *   Nome del dominio primario:
    *   Azure AD Premium: Sì/No (plug-in è disponibile tooall hello cliente gratuito, Basic e SKU Premium)
    *   Numero di utenti che useranno questa integrazione:
    *   Versione di JIRA:
    *   Commenti:

7. In una finestra del web browser, accedere come amministratore nell'istanza JIRA tooyour.

8. Passare il mouse su ruota dentata e scegliere hello **componenti aggiuntivi**.
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-jiramicrosoft-tutorial/addon1.png)

9. Nella sezione della scheda Add-ons (Componenti aggiuntivi) fare clic su **Manage add-ons** (Gestisci componenti aggiuntivi).

    ![Configura accesso Single Sign-On](./media/active-directory-saas-jiramicrosoft-tutorial/addon7.png)

10. Caricare manualmente i plug-in hello fornito da Microsoft. Una volta installato plug-in di hello, viene visualizzato **utente installato** sezione componenti aggiuntivi di **gestire componenti aggiuntivi** sezione.

11. Fare clic su **configura** tooconfigure hello nuovo plug-in.

12. Seguire questa procedura nella pagina di configurazione:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-jiramicrosoft-tutorial/addon5.png)
 
    a. In **URL dei metadati** incollare hello **URL dei metadati** generato da Azure AD e fare clic su hello **risolvere** pulsante. Legge l'URL dei metadati di hello IdP e inseriscono tutte le informazioni di campi di hello.

    > [!Note]
    > La posizione predefinita dell'ID utente SAML è nell'identificatore del nome. È possibile modificare questa opzione attributo tooan e immettere il nome di attributo appropriato hello.

    > [!TIP]
    > Verificare che sia presente un solo certificato mappato a app hello in modo che non si verificano errori per la risoluzione dei metadati hello. Se sono presenti più certificati, alla risoluzione dei metadati di hello, l'amministratore riceve un errore.
    
    b. Hello copia **identificatore, l'URL di risposta e l'URL di accesso** valori e incollarli in **identificatore, l'URL di risposta e l'URL di accesso** in rispettivamente nelle caselle di testo **JIRA SAML SSO URLediMicrosoftDomain** sezione nel portale di Azure.

    c. In **nome pulsante di accesso** nome hello del tipo di pulsante l'organizzazione vuole hello utenti toosee nella schermata di accesso.

    d. In **percorsi di ID utente SAML** selezionare **è l'ID utente nell'elemento NameIdentifier hello di hello Subject statement** o **ID utente è in un elemento attributo**.  Questo ID è l'id utente hello JIRA toobe. Se non trova corrispondenza id utente hello, sistema non consentirà toolog gli utenti in. 
    
    e. Se si seleziona **ID utente è in un elemento attributo** opzione, quindi nella **nome dell'attributo** nome hello di tipo casella di testo dell'attributo hello è previsto l'Id utente. 

    f. Se si utilizza dominio federato di hello (ad esempio, ecc. ad FS) con Azure AD, fare clic su hello **abilitare Home Realm Discovery** opzione e configurare hello **nome di dominio**.
    
    g. In **nome di dominio** tipo hello nome di dominio qui in caso di accesso basato su ADFS hello.

    h. Controllare **abilitare Single Sign-out** se si desidera toolog fuori da Azure AD quando un utente si disconnette da JIRA. 

    i. Fare clic su **salvare** pulsante Impostazioni hello toosave.

> [!TIP]
> È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!  Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello. È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.

![Creare un utente di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_01.png) 

2. elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_02.png) 

3. hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_03.png) 

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_04.png) 

    a. In hello **nome** casella tipo **BrittaSimon**.

    b. In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Show Password** e annotare il valore di hello di hello **Password**.

    d. Fare clic su **Crea**.
 
### <a name="creating-a-jira-saml-sso-by-microsoft-test-user"></a>Creazione di un utente test di JIRA SAML SSO by Microsoft

toolog agli utenti di Azure AD tooenable in tooJIRA server on-premise, è necessario eseguirne il provisioning in JIRA SAML SSO da Microsoft. In JIRA SAML SSO by Microsoft il provisioning è un'attività manuale.

**tooprovision un account utente, eseguire hello alla procedura seguente:**

1. Accedi tooyour server on-premise JIRA come amministratore.

2. Passare il mouse su ruota dentata e scegliere hello **Gestione utenti**.

    ![Aggiungere un dipendente](./media/active-directory-saas-jiramicrosoft-tutorial/user1.png) 

3. Si è reindirizzato tooAdministrator accesso pagina tooenter **Password** e fare clic su **conferma** pulsante.

    ![Aggiungere un dipendente](./media/active-directory-saas-jiramicrosoft-tutorial/user2.png) 

4. Nella sezione della scheda **User management** (Gestione utenti) fare clic su **Create user** (Crea utente).

    ![Aggiungere un dipendente](./media/active-directory-saas-jiramicrosoft-tutorial/user3.png) 

5. In hello **"Create new user"** finestra di dialogo eseguire hello alla procedura seguente:

    ![Aggiungere un dipendente](./media/active-directory-saas-jiramicrosoft-tutorial/user4.png) 

    a. In hello **indirizzo di posta elettronica** casella di testo, digitare hello di indirizzo di posta elettronica dell'utente come Brittasimon@contoso.com.

    b. In hello **nome completo** casella di testo, nome completo del tipo di utente hello come Britta Simon.

    c. In hello **Username** casella Tipo hello email dell'utente come Brittasimon@contoso.com.

    d. In hello **Password** casella di testo, digitare la password dell'utente hello.

    e. Fare clic su **Create User** (Crea utente).   

### <a name="assigning-hello-azure-ad-test-user"></a>Assegnazione utente test hello Azure AD

In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooJIRA SAML SSO da Microsoft.

![Assegna utente][200] 

**tooassign Britta Simon tooJIRA SAML SSO da Microsoft, eseguire hello alla procedura seguente:**

1. Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **JIRA SAML SSO da Microsoft**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_app.png) 

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![Assegna utente][202] 

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.

Quando si fa clic hello JIRA SAML SSO dal riquadro Microsoft nel Pannello di accesso hello, è necessario ottenere automaticamente firmato in tooyour JIRA SAML SSO dall'applicazione di Microsoft.
Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_203.png

